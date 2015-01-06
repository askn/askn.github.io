---
layout: post
title: Project Euler Problem-5
comments: true
categories: [ yazılım, ruby ]
tags: [ ruby, Project Euler ]
description: "ruby, programlama örnekleri, programlama soruları"
keywords: "ruby, programlama örnekleri, programlama soruları"
# asides: []
# author:
---

Sorumuz: 2520 is the smallest number that can be divided by each of the numbers from 1 to 10
 without any remainder.What is the smallest positive number that is evenly divisible by all of the numbers from 1 to 20?
(<a href="http://projecteuler.net/problem=5" target="_blank">soruya buradan ulaşabilirsiniz</a>)

<!-- more -->

Yani diyor ki: 1′den 10′a kadar tüm sayılara kalansız bölünen en küçük sayı 2520.
1′den 20′ye kadar tüm sayılara tam bölünen en küçük pozitif sayı nedir ?

ruby programlama dili ile benim çözümüm:

{% highlight ruby %}

def main
   puts (1..21).inject(1) { |a, b| (a*b) / a.gcd(b) }
end

if __FILE__ == $0
   main
end
{% endhighlight %}

Peki ben bu kodla ne yapmak istedim ? 1′den 20 ye kadar tüm sayıların ekokunu bulmaya çalıştım.
Bu arada sorunun cevabı: 232792560

<strong><em>Edit</em></strong>

{% highlight ruby %}

(a*b)/a.gcd(b)
{% endhighlight %}


ile ekok bulmaya çalışmıştım. Bunun rubyde hazır fonksiyonu varmış yeni öğrendim.

{% highlight ruby %}

a.lcm(b)
{% endhighlight %}


lcm:least common multiple
