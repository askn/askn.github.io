---
layout: post
title: "GraphQL Sorgularına Genel Bakış"
date: 2017-06-27 21:19
comments: true
---

Selamlar, bu blog yazımda siz değerli okurlarıma GraphQL ile sorgular nasıl yazılabilir ve daha etkili kullanım teknikleri nelerdir onlardan bahsedeceğim.

Örneklerimi [github v4 apisi](https://developer.github.com/v4/explorer/) üzerinden anlatacağım.

İlk olarak davranış ilkelerinin isimlerini çektiğimiz basit bir sorgu ile başlayalım. Sol tarafta isteği sağ tarafta gelen cevabı görüyorsunuz. Gördüğünüz gibi birbirine oldukça benzeyen istek ve cevap.

<div class="graphql">
{% highlight graphql %}
{
  codesOfConduct {
    name
  }
}
{% endhighlight %}
{% highlight json %}
{
  "data": {
    "codesOfConduct": [
      {
        "name": "Citizen Code of Conduct"
      },
      {
        "name": "Contributor Covenant"
      }
    ]
  }
}
{% endhighlight %}
</div>

## Argümanlar

Github'ın v3 REST Api'sinde alttaki url, verilen username parametresine ait datayı dönüyordu. Klasik REST yapısı.

    GET /users
    GET /users/:username

Peki bu argüman paslama işini graphQL sorgumuzda nasıl yapacağız görelim.

<div class="graphql">
{% highlight graphql %}
{
  user(login: "askn") {
    url
    createdAt
    avatarUrl(size: 333)
  }
}
{% endhighlight %}
{% highlight json %}
{
  "data": {
    "user": {
      "url": "https://github.com/askn",
      "createdAt": "2011-02-22T21:53:39Z",
      "avatarUrl": "https://avatars0.githubusercontent.com/u/632820?v=3&s=333"
    }
  }
}
{% endhighlight %}
</div>

`username` dışında `avatarUrl`'e verilen size parametresi gibi graphQL ile her field'a (tanımlandıysa) argüman verebilirsiniz. Adeta fonksiyona parametre vermek gibi 😇


## Nested

<div class="graphql">
{% highlight graphql %}
{
  topic(name: "orm") {
    name
    relatedTopics {
      name
    }
  }
}
{% endhighlight %}
{% highlight json %}
{
  "data": {
    "topic": {
      "name": "orm",
      "relatedTopics": [
        {
          "name": "database"
        },
        {
          "name": "activerecord"
        },
        {
          "name": "ruby"
        }
      ]
    }
  }
}
{% endhighlight %}
</div>

`Topic` tipinde ki `topic`, `Topic` array tipinde `relatedTopics` dönüyor. Tekerleme gibi oldu. Bunu birbiriyle ilişkili user'ın repoları, reponun sahibi, takımın üyeleri vs. gibi nested sorgu örnekleri ile de çoğaltabiliriz.


## Alias
Aynı field'ları farklı argümanlarla çağırmaya çalıştığımızda aynı keyde iki data dönemediği için bir çakışma hatası fırlatır.

<div class="graphql">
{% highlight graphql %}
{
  user(login: "askn") {
    name
  }
  user(login: "f") {
    name
  }
}
{% endhighlight %}
{% highlight json %}
{
  "data": null,
  "errors": [
    {
      "message": "Field 'user' has an argument conflict: {login:\"\\\"askn\\\"\"} or {login:\"\\\"f\\\"\"}?",
      "locations": [
        {
          "line": 2,
          "column": 3
        },
        {
          "line": 5,
          "column": 3
        }
      ]
    }
  ]
}
{% endhighlight %}
</div>

Bunu alias kullanarak çözebiliriz. Yine tek bir sorgu ile birden fazla sonuç alabildik.

<div class="graphql">
{% highlight graphql %}
{
  askn: user(login: "askn") {
    adiSoyadi: name
  }
  fka: user(login: "f") {
    name
  }
  sdogruyol: user(login: "sdogruyol") {
    name
  }
}
{% endhighlight %}
{% highlight json %}
{
  "data": {
    "askn": {
      "adiSoyadi": "Aşkın Gedik"
    },
    "fka": {
      "name": "Fatih Kadir Akın"
    },
    "sdogruyol": {
      "name": "Serdar Dogruyol"
    }
  }
}
{% endhighlight %}
</div>

Her field'a alias verebilirsiniz. Yukarıda `adiSoyadi` örneğinde gördüğünüz gibi.

## Fragment

<img align="right" src="/public/images/abuzer.jpg" width="110">

Mesela yukarıdaki örnekte 3 kişinin datasına ulaştığım bir sorgu var. Sadece name alanına değil de birçok alana ihtiyacım olduğunu varsayalım. Bu da demek oluyor ki aynı şeyi 3 kez tekrar edeceğiz.

Şaka Şaka

<div class="graphql">
{% highlight graphql %}
{
  askn: user(login: "askn") {
    ...user_datasi
  }
  fka: user(login: "f") {
    ...user_datasi
  }
  sdogruyol: user(login: "sdogruyol") {
    ...user_datasi
  }
}

fragment user_datasi on User {
  name
  createdAt
}
{% endhighlight %}
{% highlight json %}
{
  "data": {
    "askn": {
      "name": "Aşkın Gedik",
      "createdAt": "2011-02-22T21:53:39Z"
    },
    "fka": {
      "name": "Fatih Kadir Akın",
      "createdAt": "2010-02-04T09:04:51Z"
    },
    "sdogruyol": {
      "name": "Serdar Dogruyol",
      "createdAt": "2011-08-19T07:25:58Z"
    }
  }
}
{% endhighlight %}
</div>

`user_datasi` adında `User` tipi içine dağılmış, ihtiyaç halinde kullanılmak üzere bir fragment tanımladım. Sadece tekrarlı işler için değil, sorgularınızı yönetilebilir küçük parçalara bölmek için de fragmentları kullanabilirsiniz.


## Değişkenler

Şu ana kadar ki sorgularda her şeyi sorgu içine yazdık. Ama çoğu uygulama da sorguya değişken vermemiz gereken durumlar oluşabilir.

- Sorgudaki statik değeri $degisken ile değiştir. *(login: $name)*
- $degisken öğesini, sorgu tarafından kabul edilen değişkenlerden biri olarak tanımlayın. *($name: String!)*
- $degisken: değerini ayrı, ulaşıma özgü (genellikle JSON) değişkenler sözlüğüne geçirin. *{ "name": "askn" }*

<div class="graphql">
{% highlight graphql %}
query user_data($name: String!){
  user(login: $name) {
    name
  }
}

# Variables
{
  "name": "askn"
}
{% endhighlight %}
{% highlight json %}
{
  "data": {
    "user": {
      "name": "Aşkın Gedik"
    }
  }
}
{% endhighlight %}
</div>

Değişkenler hep **$** ile başlamak zorundadır. Burada String! yanında ki ünlem o değişkenin zorunlu olduğunu ifade ediyor. ünlem konulmasaydı isteğe bağlı olurdu.

Tabii ki varsayılan bir değer ataması da yapabiliyoruz.
{% highlight graphql %}
query user_data($name: String = "askn"){
  user(login: $name) {
    name
  }
}
{% endhighlight %}

Bu örnek için sorgu denerken öğrendim ki, eğer zorunlu olarak tanımlanmışsa varsayılan değer ataması yapamıyormuşuz.

`Non-null variable $name can't have a default value`

Bu arada yukarıdaki örnekte *user_data* bir *operation name*. Anlamlı isimlerle kullanırsanız debug ve loglama konusunda size yardımı dokucaktır.

Bu sorgunun request payload'ına inspect element üzerinden baktığımızda şöyle atıldığını görüyoruz.

<img src="/public/images/graphql-request-payload.png">

Yani sizde bunu curl gibi herhangi bir istemci kullanarak şu şekil atabilirsiniz.

    $ curl 'https://..../bilobalabolo' \
      -d '{
        "operation_name": "user_data",
        "query": "query user_data($name: String!){
          user(login: $name) {
            name
          }
        }",
        "variables": {
          "name": "askn"
        }
      }'

Burada bir aydınlanma molası verip bir çay içiniz.

## Directives

Değişkenler ile daha dinamik sorgular yazabiliyoruz. Fakat yine de bazen tüm ihtiyacımızı görmediği durumlar oluyor.

<div class="graphql">
{% highlight graphql %}
query($name: String!, $withFollowers: Boolean!) {
  user(login: $name) {
    name
    followers(first: 100) @include(if: $withFollowers) {
      edges {
        node {
          name
        }
      }
    }
  }
}

# Variables
{
  "name": "askn",
  "withFollowers": false
}
{% endhighlight %}
{% highlight json %}
{
  "data": {
    "user": {
      "name": "Aşkın Gedik"
    }
  }
}
{% endhighlight %}
</div>

Örneğin yukarıdaki sorgu için `withFollowers` değişkeni aracılığı ile takipçi datasının gelip gelmeyeceğine karar verebiliriz.

**@include(if: Boolean)** Sadece true gelirse dahil edilsin

**@skip(if: Boolean)** Sadece false gelirse dahil edilsin.

Kendinizde mesela sadece ilk beş karakteri döndürecek custom *directive* tanımlayabilirsiniz.

# Mutations

REST üzerinde get, post, put, delete methodlarından şimdiye kadar anlattıklarımın sadece GET ile alakalı olduğunu anlamışsınızdır. Peki ya data üzerinde değişiklik yapacağımız post, put, delete.

GraphQL üzerinde bu işlemler mutation'lar aracılığı ile yapılıyor.

<div class="graphql">
{% highlight graphql %}
mutation {
  addStar(input: { starrableId: "MDEwOlJlcG9zaXRvcnk0OTA3MjEwMQ==" }) {
    starrable {
      id
    }
  }
}
{% endhighlight %}
{% highlight json %}
{
  "data": {
    "addStar": {
      "starrable": {
        "id": "MDEwOlJlcG9zaXRvcnk0OTA3MjEwMQ=="
      }
    }
  }
}
{% endhighlight %}
</div>

Gördüğünüz gibi query ile neredeyse aynı yapıya sahip. `addStar` mutation'ı argüman olarak starrableId almış ve
Starrable tipinde bir alan dönmüş. Tabii ki burada da değişkenleri sorgu içine yazmak yerine variable'ları kullanarak daha temiz bir yapı kurabilirsiniz.

## Inline Fragments ve Meta Fields

GraphQL union type sistemine sahip. Yani dönecek data farklı tiplerde gelebilir. Bu tarz sorgularda inline fragment'ları kullanabiliriz.

Bu tarz durumlarda dönen verinin hangi tipte geldiğini client bilemez, bu yüzden nasıl davranacağını kestiremez. GraphQL ile **__typename** gibi değerin adını içeren meta field'lar bu konuda imdadımıza yetişiyor.

<div class="graphql">
{% highlight graphql %}
{
  search(query: "askn", type: USER, first: 3) {
    edges {
      node {
        __typename
        ... on User {
          name
        }
        ... on Organization {
          name
        }
      }
    }
  }
}
{% endhighlight %}
{% highlight json %}
{
  "data": {
    "search": {
      "edges": [
        {
          "node": {
            "__typename": "User",
            "name": "Aşkın Gedik"
          }
        },
        {
          "node": {
            "__typename": "User",
            "name": "Amando Nudo"
          }
        },
        {
          "node": {
            "__typename": "Organization",
            "name": "asknative"
          }
        }
      ]
    }
  }
}
{% endhighlight %}
</div>

User veya Organization tipinde dönerse çağrılacak fieldları blok içinde yazdık.

<br />
<center>***</center>
<br />

Bu anlattıklarımın tamamı client tarafından sorguların graphql ile yazılmış bir sisteme nasıl atılacağı ile alakalı idi.
"*İyi de kardeşim bunun backend'i yok mu, bunca sorguyu nereye atacaklar?*" dediğinizi duyar gibiyim. Meraklanmayın, diğer blog yazılarımda (Ruby ile) backend tarafını da aktaracağım.

<img src="/public/images/graphql-kapanis.png">
<marquee><a href="https://twitter.com/meryemmekinci" alt="Görsel İçin Teşekkürler">Meryem Ekinci</a> ve <a href="https://twitter.com/saidozcan" alt="Görsel İçin Teşekkürler">Said Özcan'a</a> fotoğrafa yaptıkları katkılar için teşekkürler.</marquee>

Bu yazının tamamını okuma zahmetinde bulunduysanız siz de GraphQL'in tadına baktınız demektir. Yazıların devamı gelene dek [şurada](https://goo.gl/M8YEYN) bekleyebilirsiniz.

#### Kaynaklar

- [Github V4 API](https://developer.github.com/v4/explorer/)
- [GraphQL.org](http://graphql.org/learn/queries/)

#### Teşekkür

- [Meryem Ekinci](https://twitter.com/meryemmekinci "Görsel İçin Teşekkürler")
