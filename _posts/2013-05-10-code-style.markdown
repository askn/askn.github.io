---
layout: post
title: "Kodlama Stili"
date: 2013-05-10 21:34
comments: true
categories: [ yazılım, teknik ]
tags: [ programlama, java, c ]
description: "Kodlama Stili, Java Code Style, C Code Style, python, ruby"
keywords: "java, c#, programming style, astyle, allman, k&r, linux, pep8, rubocop gem"
# asides: []
# author:
---
Programlamada yazdığımız kodun okunabilirliğini arttıran faktörlerden biride kodlama
stilidir.

<!-- more -->

Kodlama stili yazdığımız programlama dilinde genel kabul görmüş isimlendirme, girintileme gibi konulardaki kurallar kümesidir diyebiliriz.

Şiir gibi kod yazmak için uymanız gereken bazı kodlama stilleri:

- Python: [PEP8](http://www.python.org/dev/peps/pep-0008/)
- C: [Linux kernel coding style](https://www.kernel.org/doc/Documentation/CodingStyle)
- Ruby: [Ruby](https://github.com/bbatsov/ruby-style-guide)

Bu kodlama stillerini kontrol eden çeşitli araçlar mevcut.

###  Örneğin:
Ruby için [Rubocop](https://github.com/bbatsov/rubocop) size hangi satırlarda ne yapmanız gerektiğini söyler.

Kurulumu:

    $ sudo gem install rubocop

Kullanımı:

    $ rubocop foo/bar.rb

Java, c#, c, c++ için yazılmış [Artistic Style'ı](http://astyle.sourceforge.net/astyle.html) çalıştırdığınızda kodunuzu standartlara uygun düzeltir. Eski kodlarınızı `.orig` uzantılı bir dosyaya koyar.

Kurulumu:

    $ sudo apt-get install astyle

Kullanımı:

    $ astyle --style=linux example.c

Python için kodlarınızı pep8'leyen [autopep8](https://github.com/hhatto/autopep8)

Kurulumu:

    $ sudo easy_install -ZU autopep8

Kullanımı:

    $ autopep8 -ia foo.py

### Kaynaklar:

- [Programlama Stili](http://en.wikipedia.org/wiki/Programming_style)
- [astyle](http://astyle.sourceforge.net/)
- [rubocop](https://github.com/bbatsov/rubocop/blob/master/README.md)
- [autopep8](http://sayz.github.io/blog/2013/04/07/otomatik-pep8-leyici-autopep8/)
