---
layout: post
title: "Rails: Model ilişkilerini öğrenme"
date: 2015-10-25 18:48
comments: true
---

<img align="right" src="{{ site.baseurl }}public/images/beyle.jpg" width="100px">

ActiveRecord'un Reflection modülünü kullanarak modellerin ilişkilerini nasıl öğrenebileceğimizi (beyle) ve bir kaç method ile nasıl at koşturabileceğimizi anlatacağım.

**reflections** methodu sayesinde bir modelin hash olarak tüm ilişkilerini görebiliriz.

{% highlight ruby %}
2.2.1 :051 > Post.reflections
{
    "user" => #<ActiveRecord::Reflection::BelongsToReflection:0x007fb474a5ed50 @name=:user, @scope=nil, @options={}, @active_record=Post(id: integer, title: string, body: string, author_id: integer, is_published: boolean, created_at: datetime, updated_at: datetime), @klass=nil, @plural_name="users", @automatic_inverse_of=nil, @type=nil, @foreign_type="user_type", @constructable=true, @association_scope_cache={}, @scope_lock=#<Mutex:0x007fb474a5eaa8>>,
    
    "comments" => #<ActiveRecord::Reflection::HasManyReflection .....,
    
    "tags" => #<ActiveRecord::Reflection::ThroughReflection ......
}
{% endhighlight %}

<i>:has_many</i>, <i>:has_one</i>, <i>:belongs_to</i> argumanlarından birini alan **reflect_on_all_associations** methodu sayesinde ilişki tipine göre sonuçları görebiliriz. Bu methodun çıktısı bir array.

{% highlight ruby %}
2.2.1 :007 > Post.reflect_on_all_associations(:belongs_to)
[
    [0] #<ActiveRecord::Reflection::BelongsToReflection:0x007fb478871610 @name=:user, @scope=nil, @options={}, @active_record=Post(id: integer, title: string, body: string, author_id: integer, is_published: boolean, created_at: datetime, updated_at: datetime), @klass=nil, @plural_name="users", @automatic_inverse_of=nil, @type=nil, @foreign_type="user_type", @constructable=true, @association_scope_cache={}, @scope_lock=#<Mutex:0x007fb4788713e0>>
]
{% endhighlight %}

**klass** methodu ile direkt bağlı olduğu modele erişebilirken, **class_name** ile ismini öğrenebiliriz ve **options** ile daha neler neler var.

{% highlight ruby %}
2.2.1 :032 > Post.reflect_on_all_associations(:belongs_to).first.klass
class User < ActiveRecord::Base {
            :id => :integer,
    :first_name => :string,
     :last_name => :string,
        :active => :boolean,
    :created_at => :datetime,
    :updated_at => :datetime
}

2.2.1 :033 > Post.reflect_on_all_associations(:belongs_to).first.class_name
"User"

2.2.1 :050 > User.reflections["comments"].options
{
    :dependent => :destroy
}
{% endhighlight %}

<center>
<blockquote class="twitter-tweet" lang="tr"><p lang="tr" dir="ltr">Hala anlamadıysan senin için yapacağım bir şey yok. İstersen yazılı sor cevaplayayım, istersen ulak gönder soru işaretlerini gidereyim.</p>&mdash; Devlet Bahçeli (@dbdevletbahceli) <a href="https://twitter.com/dbdevletbahceli/status/637324210315108352">28 Ağustos 2015</a></blockquote>
</center>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

### Kaynaklar

- [viget](https://viget.com/extend/identifying-foreign-key-dependencies-from-activerecordbase-classes)
- [Devlet Bey'in tweeti](https://twitter.com/dbdevletbahceli/status/637324210315108352)
- [reflection.rb](https://github.com/rails/rails/blob/master/activerecord/lib/active_record/reflection.rb)
