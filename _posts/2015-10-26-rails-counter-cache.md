---
layout: post
title: "Rails: Counter Cache"
date: 2015-10-26 21:35
comments: true
---

Merhabalar, bugün sizlere içinde binlerce ibret olan diyemeyeceğim ama bir kaç ufak titreme yaşatacak bir şeyler anlatacağım.

Rails ile bir blog uygulaması yazdığımızı hayal edelim. Elimizde **Post** ve **Comment** şeklinde modellerimiz olsun. Biz de anasayfada yazıların başlıklarını ve yorum sayılarını listelemek isteyelim.

{% highlight ruby %}
class PostsController < ApplicationController
  def index
    @posts = Post.all
  end
end
{% endhighlight %}

    Processing by PostsController#index as HTML
    Post Load (0.2ms)  SELECT "posts".* FROM "posts"
    (0.1ms)  SELECT COUNT(*) FROM "comments" WHERE "comments"."post_id" = ?  [["post_id", 1]]
    (0.1ms)  SELECT COUNT(*) FROM "comments" WHERE "comments"."post_id" = ?  [["post_id", 2]]
    (0.1ms)  SELECT COUNT(*) FROM "comments" WHERE "comments"."post_id" = ?  [["post_id", 3]]
    (0.1ms)  SELECT COUNT(*) FROM "comments" WHERE "comments"."post_id" = ?  [["post_id", 4]]
    (0.1ms)  SELECT COUNT(*) FROM "comments" WHERE "comments"."post_id" = ?  [["post_id", 5]]

Hooaayyydaaaa!!!?!1?

{% highlight ruby %}
class PostsController < ApplicationController
  def index
    @posts = Post.all.includes(:comments)
  end
end
{% endhighlight %}

    Processing by PostsController#index as HTML
      Post Load (0.3ms)  SELECT "posts".* FROM "posts"
        Comment Load (0.2ms)  SELECT "comments".* FROM "comments" WHERE "comments"."post_id" IN (1, 2, 3, 4, 5, 6, 7, 8, 9, 10)

Şükür 2 sorguya düşürdük.`n+1` query problemini de giderdik. Bu arada `n+1` query probleminin tespiti için [Bullet](https://github.com/flyerhzm/bullet) gem'ini kullanabilirsiniz.

### Counter Cache

Fakat bunun yerine başka bambaşka bir olay var. **counter_cache** kullanarak yazıya bağlı yorumların sayısını daha verimli bir şekilde öğrenebiliriz.

**posts** tablosuna **comments_count** sütunu ekleyecek bir migration yazalım ve ardından **Comment** modelimizde düzenleme yapalım.

{% highlight ruby %}
class Comment < ActiveRecord::Base
  belongs_to :post, counter_cache: true
  ...
end
{% endhighlight %}

Counter cache ekledikten sonra **size** veya **comments_count** ile tek sorgu yaparak yorum sayısını öğrenebiliriz. Eğer **count** kullanırsak comments tablosuna sorgu atar.

    > Post.first.comments.count
    SELECT  "posts".* FROM "posts"  ORDER BY "posts"."id" ASC LIMIT 1
    SELECT COUNT(*) FROM "comments" WHERE "comments"."post_id" = ?  [["post_id", 1]]
    4

    > Post.first.comments_count
    SELECT  "posts".* FROM "posts"  ORDER BY "posts"."id" ASC LIMIT 1
    4

    > Post.first.comments.size
    SELECT  "posts".* FROM "posts"  ORDER BY "posts"."id" ASC LIMIT 1
    4

### Size - Count - Length

{% highlight ruby %}
post = Post.first       # post'u belleğe yükler
post.comments.size      # sorgu yok, comments_count sütununu okur
post.comments.count     # sorgu, sql count
post.comments.length    # sorgu, yorumları belleğe yükler
{% endhighlight %}


<center>
<img src="{{ site.baseurl }}public/images/ibretalindi.gif">
</center>

### Kaynaklar

- [Jumpstartlab](http://tutorials.jumpstartlab.com/topics/performance/queries.html)
- [Stackoverflow](http://stackoverflow.com/questions/6083219/activerecord-size-vs-count)
- [Rails Guides](http://guides.rubyonrails.org/association_basics.html)
