---
layout: post
title: Uygulamanızı Herokuya Deploy Edin
comments: true
categories: [ yazılım ]
tags: [ heroku ]
description: "Heroku Kullanımı, Heroku Türkçe, Heroku ayarları, Herokuya
gönderme"
keywords: "Heroku Kullanımı, Heroku Türkçe, Heroku ayarları, Herokuya
gönderme"
# asides: []
# author:
---

### Heroku Kullanımı

Heroku kullanmak için ihtiyacımız olan [heroku toolbelt](https://toolbelt.heroku.com/)'i kuralım. Herokuyu kullanmak için ihtiyacımız olan her şey burada mevcut.

<!-- more -->

    $ wget -qO- https://toolbelt.heroku.com/install-ubuntu.sh | sh

Herokuya kayıt olurken kullandığımız email ve şifre ile giriş yapalım.

    $ heroku login
    Enter your Heroku credentials.
    Email: askn@example.com
    Password:
    Could not find an existing public key.
    Would you like to generate one? [Yn]
    Generating new SSH public key.
    Uploading ssh public key /Users/adam/.ssh/id_rsa.pub

Tüm ayarlar bitti bu kadar. `:D`

### Herokuda uygulama oluşturma

Github kullanların yakından bildiği üzere `git` çok güçlü bir sürüm takip sistemidir ve heroku uygulamaları dağıtmak için
`git`'i kullanır. Proje dizinimizdeyken!

    $ git init
    Initialized empty Git repository in .git/
    $ git add .
    $ git commit -am "ilk"
    $ heroku create my_app

Eğer uygulamamız github'ta da mevcutsa sadece

    $ heroku create my_app

ile herokuda uygulamamızı oluşturmamız yeterli.

### Deploy etme

    $ git push heroku master

Eğer ugulamamızı açmak istersek

    $ heroku open


###  Kaynaklar

- [Deploy](http://ruby.railstutorial.org/ruby-on-rails-tutorial-book#sec-deploying)
- [Heroku](https://devcenter.heroku.com/articles/git#tracking-your-app-in-git)
