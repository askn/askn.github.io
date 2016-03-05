---
layout: post
title: Sinatra Uygulamasını Herokuya Deploy Etme
comments: true
categories: [ yazılım, ruby ]
tags: [ heroku, sinatra ]
description: "Heroku Kullanımı, Heroku Türkçe, Heroku ayarları, Herokuya
gönderme, sinatra türkçe, sinatra nedir, sinatra kurulumu, ruby türkçe, ruby
dersleri"
keywords: "Heroku Kullanımı, Heroku Türkçe, Heroku ayarları, Herokuya
gönderme sinatra türkçe, sinatra nedir, sinatra kurulumu, ruby türkçe, ruby
dersleri"
# asides: []
# author:
---

Daha önceki yazımda heroku ayarlarını ve herokuda uygulama oluşturmayı [anlatmıştım.](http://askingedik.net/2012/12/21/heroku-setup-and-deploy/)

Bugün ise sinatra uygulamızı herokuya deploy etmek için gereken
yapılandırmalardan bahsedeceğim.

Öncelikle uygulamamızın ana dizininde `config.ru` dosyası olmalı ve içeriği

<!-- more -->

{% highlight ruby %}
require "./hello.rb"
run Sinatra::Application
{% endhighlight %}

şeklinde olmalıdır. Burada dikkat edilecek husus `hello.rb` bizim ana uygulama dosyamız olmasıdır.

İkinci olarak ise `Gemfile` gereklidir.

{% highlight ruby %}
source 'http://rubygems.org'
gem 'sinatra'
{% endhighlight %}

Bu iki dosyayı oluşturduktan sonra gönül rahatlığı ile deploy edebilirsiniz.
`=P`


###   Kaynak

- [sinatra](http://sinatra-book.gittr.com/#heroku)
- [heroku](https://devcenter.heroku.com/articles/rack#pure-rack-apps)
