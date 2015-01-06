---
layout: post
title: "Mysql Komutları: limit"
date: 2013-06-07 22:35
comments: true
categories: [ yazılım ]
tags: [ mysql ]
description: "mysql komutları limit komutu"
keywords: "mysql, mysql dersleri, mysql komutları"
# asides: []
# author:
---

Sql sorgularında belli kayıt aralıklarını göstermek için kullanırız.

<!-- more -->

Örneğin ilk beş kaydı göstermek için:

    select * from tablo limit 5

Onuncu kayıttan itibaren beş(11,12,13,14,15) kayıt göstermek için:

    select * from tablo limit 10, 5
