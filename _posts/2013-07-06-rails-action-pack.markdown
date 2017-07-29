---
layout: post
title: "Rails Action Pack"
date: 2013-07-06 16:12
comments: true
categories: [ yazılım, ruby, rails ]
tags: [ ruby on rails, ruby, action pack, yazılım, teknik ]
description: "Ruby on rails uygulamasında Action Pack"
keywords: "ruby on rails, action pack, action view, action controller, action
dispatch, rails request cycle, rails türkçe ders notları"
# asides: []
# author:
---
Action Pack web isteklerini işleyen ve yanıtlayan bir frameworktür.

<!-- more -->

Yönlendirme mekanizmasını sağlar, controller'lardaki action'ları uygular, viewleri
oluşturur, kısaca Action Pack MVC(Model-View-Controller) yapısındaki view ve controller katmanlarını
sunar.
Birkaç modülden oluşur.

**ActionController:** rails uygulamalarında controller'ları yöneten yapıdır. Gelen
istekleri işler, parametreleri çeker ve istenilen controller'lardaki action'lara
gönderir. Session management, template rendering, ve redirect management'tan
sorumludur.

**ActionView:** viewleri yöneten bileşendir. Html, xml, ajax desteği sağlar. Parça
halindeki şablonları(layout..vb.) birleştirir.

**ActionDispatch:**Uygulamada gelen web isteklerini(request) çözümleyen ve dağıtan, yönlendiren
bileşendir. Session, cache ve cookie'leri taşır.

ActionPack için bir requestin yaşam döngüsü

- Rails tarayıcı aracılığı ile gelen isteği(request) alır.
- Routing isteğin hangi controller'ın hangi action'ına gideceğini seçer.
- Controller nesnesi ve ilgili action methodu çağrılır.
- Controller model ile etkileşimli çalışır. ( Genellikle CRUD işlemleri gerçekleştirilir. )
- Yanıt(Response) yönlendirme veya render şeklinde tarayıcıya geri gönderilir.

<img src="/public/images/action-pack-request-cycle.png" width="620px" />

### Kaynaklar

- [github/rails](https://github.com/rails/rails/blob/master/actionpack/README.rdoc)
- [beginnig rails 3](http://beginningrails.com/)
- [guides ruby on rails](http://guides.rubyonrails.org/v3.2.13/getting_started.html)
