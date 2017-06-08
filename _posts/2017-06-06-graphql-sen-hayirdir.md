---
layout: post
title: "GraphQL Sen Hayırdır?"
date: 2017-06-06 23:27
comments: true
---

<center>
Tamamını okumak istemeyenler için özeti
<blockquote class="twitter-tweet" data-lang="en"><p lang="tr" dir="ltr">Bizde data ortaya konur. Herkes ihtiyacı kadarını alır. <a href="https://twitter.com/hashtag/GraphQL?src=hash">#GraphQL</a> <a href="https://t.co/iegLlfPI2G">pic.twitter.com/iegLlfPI2G</a></p>&mdash; Aşkın Gedik (@askngdk) <a href="https://twitter.com/askngdk/status/835856426958467073">February 26, 2017</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>
</center>

<br />

GraphQL; Facebook tarafından geliştirilen, API'ler için bir data sorgulama dili olarak tanımlanabilir. Yani
GraphQL sorgunuz ile (backend tarafında tanımlanan)dataya client üzerinden şekil verebiliyorsunuz. Dönen dataya şekil verdiğiniz için daha **ürün** ve **ihtiyaç** odaklı bir yapıya sahip, client'lar için daha **esnek** bir yapı sunuyor.

API ile dönen data içerisinde ihtiyacınız olmayan onlarca veri olabiliyor ve bu size kilobaytlar kaybettiriyor.
Örneğin [github v3 API'sini](https://api.github.com/users/askn/repos) kullanarak
bir kişiye ait repo isimlerini listeleyen bir app yazmak istediğimizde gelen dataya **(104 KB)** ve [github'ın v4 graphql API'si](https://developer.github.com/v4/explorer/) ile deneyebileceğiniz aşağıdaki graphql sorgusunun çıktısına **(3 KB)** bakın.

{% highlight graphql %}
{
  user(login: "askn") {
    repositories(first: 100) {
      edges {
        node {
          name
        }
      }
    }
  }
}
{% endhighlight %}

GraphQL üzerinde tip sistemi mevcut. (Strongly typed)
Tip sistemi olduğu için bir GraphQL sorgusunun geçerli olup olmadığı önceden belirlenebilir.

Vereceğiniz alias'lar ile API'den dönen json'ı şöyle bir formata dahi dönüştürebilirsiniz.
Dönen cevap zorunuza mı gidiyor basın alias'ı.

<center>
<img src="{{ site.baseurl }}public/images/kemale_star_atan.png" />
</center>

GraphQL, istediğiniz verileri getirmek için birden fazla REST isteğini tek bir sorgu ile değiştirmenize olanak sağlar. Örneğin twitter anasayfasını inceleyelim.

<center>
<img src="{{ site.baseurl }}public/images/twitter-graphql.png" />
</center>

- 1 - Profil bilginiz
- 2 - Takip etmeniz için önerilen kişiler
- 3 - Akış üzerindeki twitler
- 4 - Gündem

Her bir endpointten data çekmek için sorgu atılıyor bunun yerine graphql ile kaba taslak aşağıdaki gibi bir şeyler yazıp tek bir sorgu ile istediğimiz datayı istediğimiz formatta elde edebiliriz.

{% highlight graphql %}
{
  me {
    ...user
    header_photo {
      # buraya bir şeyler daha
    }
    tweet_count
    following_count
    follower_count
  }

  trends {
    name
    slug
  }

  suggestions(limit: 3) {
    ...user
  }

  tweets(limit: 25) {
    user {
      ...user
    }
    text
    retweet_count
    favorite_count
    favorited
    retweeted
    # buraya bir şeyler daha
  }
}

fragment user on User {
  id
  name
  screen_name
  profil_photo {
    # buraya bir şeyler daha
  }
}

{% endhighlight %}

Dikkatinizi çekmek istediğim iki şey var burada. İlk olarak ortak kullandığım user alanları için bir `fragment` tanımlayarak DRY hale getirdim. Diğer nokta ise `tweets` ve `suggestions` field resolver'ına parametre geçtim.
Bunları diğer blog yazılarımda ayrıntılı aktaracağım. Şimdilik hoş, kolay kullanımına bir göz atmanızı istedim. Gerisi kolayca anlaşılabiliyor zaten json'ın sadece key'lerinin olduğu bir şey gibi.

GraphQL içinde bulunan şemanızdan otomatik oluşturulan introspection sayesinde hangi sorguların nasıl desteklendiğini kendisi dokümante ediyor. Örneğin: [Github API v4'ü](https://developer.github.com/v4/explorer/) deneyebileceğiniz graphiql editorünün sağ kısmındaki dokümanı inceleyebilirsiniz.

Şu an github, shopify, facebook, coursera, yelp, protel(🙃) gibi bir çok şirket graphql kullanıyor ve destekliyor.

Kullanmanız için en önemli bir diğer sebep ise şu an oldukça HYPE bir teknoloji olması. Ortamlarda `ağğbii siz hala mı rest yazıyorsunuz? ya ne gada çağ dışısınız` diyebilirsiniz.

Okuduğunuz için
Tşk.

#### Kaynaklar

- [github](https://developer.github.com/)
- [githubengineering](https://githubengineering.com/the-github-graphql-api)
- [graphql](http://graphql.org/)
