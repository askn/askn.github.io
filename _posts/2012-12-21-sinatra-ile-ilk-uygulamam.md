---
layout: post
title: Sinatra ile Tanışalım
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

### Sinatra nedir ?

Sinatra ruby ile yazılmış özgür ve açık kaynaklı bir web kütüphanesidir.
Kullanımı çok esnek ve kolaydır.

<!-- more -->

### Sinatra kurulumu

`Ruby` kurulu bir makine de sinatra `gem`'ini kurmanız yeterli.

    sudo gem install sinatra

### Sinatra ile Merhaba Dünya

`hello.rb` dosyamıza gerekli kodları yazalım.

{% highlight ruby %}

# encoding: utf-8
require 'sinatra'

get '/' do
  'Merhaba Dünya!'
end
{% endhighlight %}


`$ ruby hello.rb` ile betiği çalıştıralım.

    == Sinatra/1.3.3 has taken the stage on 4567 for development with backup from Thin
    >> Thin web server (v1.5.0 codename Knife)
    >> Maximum connections set to 1024
    >> Listening on 0.0.0.0:4567, CTRL+C to stop

Düzgün çalıştı. Web tarayıcımızda `http://0.0.0.0:4567/` adresinde 'Merhaba
Dünya!' yazısını görmemiz mümkün. Bu kadar basit.

### Benim ilk uygulamam!

Benim ilk sinatra [uygulamam](http://aykun.herokuapp.com).
Uygulamada ki amaç kategorilere göre gruplanmış kelimelerin bulunduğu bir [yaml](http://askingedik.net/2012/12/04/yaml-for-ruby/) dosyasından seçilen koşullara göre rastgele kelimeleri birleştirmek.
Kaynak kodları [github](http://github.com/askn/aykun)'tan inceleyebilirsiniz.

###   Kaynak

- [Sinatra](http://www.sinatrarb.com/intro.html)
