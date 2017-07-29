---
layout: post
title: "Introduction To Type Systems"
date: 2013-10-13 15:17
comments: true
categories: [ yazılım ]
tags: [ teknik, yazılım ]
description: "Programlamada Tip Sistemleri"
keywords: "strong, dynamic, weak, static, programming, type systems"
---

Python dinamik ve güçlü, Java statik ve güçlü, Php dinamik ve zayıf tipli dildir.
Peki statik, dinamik, güçlü, zayıf tipli ne demek ?

<!-- more -->

### Statik Tip

<img src="/public/images/static_type.jpg"  width="250" height="350">

Java, Go ,C ve C++ statik tipli dillerdir. Statik tipli dillerde değer üreten herşeyin tipi belirtilmek
zorundadır. Bu dillerde tip denetlemesi derleme zamanında yapılır.

{% highlight c %}
int i;
i = 5;

int hop () {
        return 0;
}
{% endhighlight %}

### Dinamik Tip

Dinamik tipli dillerde değerlerin tipleri çalışma zamanında belli olur. Bu tür
dillere python, ruby, php gösterilebilir.

{% highlight ruby %}
x = 5
name = "askn"
{% endhighlight %}

### Strong(Güçlü) Tip

Değişkenler mutlaka veri tipine bağlıdır. Java, Python, Go, Ruby güçlü tipli dillerdir.

{% highlight ruby %}
[1] pry(main)> a = "askn"
=> "askn"
[2] pry(main)> a = a + 1
TypeError: can't convert Fixnum into String
from (pry):2:in `+'
{% endhighlight %}

Yukarıdaki ruby örneğinde bir stringe sayı eklememize izin vermedi.
`TypeError` hatası verdi.

{% highlight java %}
public class Hop {
        public static void main (String args[]) {
                String a = 1;
                System.out.printf(a);
        }
}
{% endhighlight %}

Java örneğinde ise string olarak deklare ettiğimiz a
değişkenine integer bir değer atamaya çalışıyoruz. Tahmin ettiğiniz üzere
derlenirken hata verecek.
Yani strong tipli dillerde değişken türleri ile yaptığınız işlemler sıkı kontrol
altındadır.

### Weak(Zayıf) Tip

Bu tipe örnek olarak php gösterilebilir.

{% highlight php %}
<?php
$foo = "x";
$foo = $foo + 2; // not an error
echo $foo;
?>
{% endhighlight %}

Gördüğünüz üzere bir hata vermedi. Güçlü tipli dillerde olduğu gibi değişkenlerle yapılan işlemler sıkı kontrol
edilmiyor.

### Kaynaklar
- [Karikatür](http://geekandpoke.typepad.com/geekandpoke/2012/03/static-typing.html)
- [Wikipedia](http://en.wikipedia.org/)
- [Programming type systems](http://significantinsignificance.wordpress.com/2010/03/17/programming-type-systems/)
- [Introduction to Static and Dynamic Typing](http://www.sitepoint.com/typing-versus-dynamic-typing)
