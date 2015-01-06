---
layout: post
title: vidir - edit directory
comments: true
categories: [ yazılım ]
tags: [ linux ]
description: "dizin düzenleme, Unix Linux Araçlar "
keywords: "dizin düzenleme, Unix Linux Araçlar "
# asides: []
# author:
---

Vidir bir metin düzenleyicisinde dizin içeriği düzenlemeye yarar. Satırları
silerek dosyadan kurtulabilir, dosya veya dizinin ismi ile oynayabilirsiniz.

Örnek bir kaç kullanım:

<!-- more -->

    vidir _includes/
    1	_includes/archive.html
    2	_includes/disqus.html
    3	_includes/footer.html
    4	_includes/ga.html
    5	_includes/sidebar.html


    vidir *.md
    1       deneme.md
    2       foobar.md

Unutmadan severek kullandığımız canımız kanımız `vim`'in özelliklerini de kullanabiliyoruz.

###  Kaynaklar

- man vidir
