---
layout: post
title: Model View Controller (MVC) Nedir?
comments: true
categories: [ yazılım, rails ]
tags: [ MVC, ASP.NET MVC, Ruby on rails ]
description: "MVC, MVC nedir, ASP.NET MVC, Ruby on rails"
keywords: "MVC, MVC nedir, ASP.NET MVC, Ruby on rails"
# asides: []
# author:
---

1970′lerde ortaya çıkan bir tasarım şablonudur.
<p>Oluşturulan katmanlı yapı sayesinde:</p>

<!-- more -->

<ul>
<li>Kodların daha temiz, düzenli, anlaşılır olması sağlanır.</li>
<li>Büyük projelerde kodların daha hızlı geliştirilmesine olanak tanır.</li>
<li>Görev paylaşımını kolaylaştırır.</li>
<li>Modüler bir yapı sağlar.</li>
<li>Hata tespit ve çözüm kolaylaşır.</li>
</ul>
<p>Bu katmanlı yapı adında anlaşılacağı gibi üç kısımdan oluşur.</p>
<ol>
<li><strong>Model</strong>: veritabanı ile ilgili işlemlerin yapıldığı bölümdür. Sadece controller katmanı ile çalışır.</li>
<li><strong>View</strong>: Kullanıcılara gösterilen arayüzün bulunduğu katmandır. Sadece controller katmanı ile çalışır.</li>
<li><strong>Controller</strong>: Kullanıcı ile iletişimi sağlayan katmandır. Kullanıcının isteklerini ve kullanıcıya dönen verileri kontrol eder.</li>
</ol>
