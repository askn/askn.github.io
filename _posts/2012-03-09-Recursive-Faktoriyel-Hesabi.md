---
layout: post
title: Özyinelemeli(Recursive) Faktoriyel Hesabı
comments: true
categories: [ yazılım ]
tags: [ C Programlama Dili, Programlama Soruları, Özyinemeli Fonksiyonlar ]
description: "C Programlama Dili, Programlama Soruları, Özyinemeli Fonksiyonlar"
keywords: "C Programlama Dili, Programlama Soruları, Özyinemeli Fonksiyonlar"
# asides: []
# author:
---

Özyinelemeli fonksiyonlar kendi içinde kendini çağıran fonksiyonlardır. 
Örneğin faktoriyel hesabının C programlama dilinde özyinelemeli çözümü şu şekildedir.

<!-- more -->

{% highlight c %}
#include <stdio.h>

int faktoriyel (int sayi)
{
        if (sayi == 1 || sayi == 0)
                return 1;
        else
                return sayi * faktoriyel(sayi - 1);
}

int main (void)
{
        printf("%d", faktoriyel(5));
        return 0;
}
{% endhighlight %}

