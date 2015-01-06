---
layout: post
title: "Ruby Arrays"
date: 2013-07-01 18:22
comments: true
categories: [ ruby, yazılım ]
tags: [ ruby, array ]
description: "Ruby programlama dilinde dizi yapısı - Array"
keywords: "ruby öğren, türkçe ruby notları, ruby dersleri, ruby diziler, ruby
array"
# asides: []
# author:
---

Diziler, tam sayı indexli bir şekilde farklı nesnelerin tutulabileceği bir veri
yapısıdır.
C, Java vb. dillerde olduğu gibi dizi indexi `0`'dan başlar. `-1` son elemanı
temsil eder.

<!-- more -->

### Boş bir dizi oluşturma

{% highlight ruby %}

arr = Array.new
=> []

arr = []
=> []
{% endhighlight %}


### Dizi oluşturma

{% highlight ruby %}

ary = [1, "two", 3.0]
=> [1, "two", 3.0]

Array.new(3)
=> [nil, nil, nil]

Array.new(3, true)
=> [true, true, true]

Array.new(4) { Hash.new }
=> [{}, {}, {}, {}]

empty_table = Array.new(3) { Array.new(3) }
=> [[nil, nil, nil], [nil, nil, nil], [nil, nil, nil]]

arr = %w[a b c]
=> ["a", "b", "c"]
{% endhighlight %}


### Dizideki elemanlar

{% highlight ruby %}

arr = [1, 2, 3, 4, 5, 6]

arr[2]
=> 3

arr[-1]
=> 6

arr[-3, 2]
=> 4, 5

arr[1...4]
=> 2, 3, 4

arr.at(0)
=> 1
{% endhighlight %}


###   Dizi hakkında bilgi edinme

Boyutu öğrenme

{% highlight ruby %}

browsers = ['Chrome', 'Firefox', 'Safari', 'Opera', 'IE']

browsers.length
=> 5

browsers.count
=> 5

browsers.size
=> 5
{% endhighlight %}

Bu elemandan kaç tane var ?

{% highlight ruby %}

ary = [1, 2, 4, 2]
ary.count(2)
=> 2
{% endhighlight %}

Koşula uyan kaç eleman var ?

{% highlight ruby %}

ary.count { |x| x%2 == 0 }
=> 3

{% endhighlight %}


Boş mu ?

{% highlight ruby %}

browsers.empty?
=> false
{% endhighlight %}


Bu eleman var mı ?

{% highlight ruby %}

browsers.include?('Konqueror')
=> false
{% endhighlight %}

İndexi ne ?

{% highlight ruby %}

a = [ "a", "b", "c" ]
a.index("b")
=> 1
a.index("z")
=> nil
{% endhighlight %}


### Diziye eleman ekleme

{% highlight ruby %}

arr = [1, 2, 3, 4]
arr.push(5)
=> [1, 2, 3, 4, 5]

arr << 6
=> [1, 2, 3, 4, 5, 6]
{% endhighlight %}


Belirtilen index'e elemanı ekle

{% highlight ruby %}

arr.insert(3, 'apple')
=> [0, 1, 2, 'apple', 3, 4, 5, 6]
{% endhighlight %}


Belirtilen index'e birden fazla eleman ekle

{% highlight ruby %}

arr.insert(3, 'orange', 'pear', 'grapefruit')
=> [0, 1, 2, "orange", "pear", "grapefruit", "apple", 3, 4, 5, 6]
{% endhighlight %}

### Diziden eleman silme

{% highlight ruby %}

arr = [1, 2, 3, 4, 5, 6]
arr.pop
=> 6
arr
=> [1, 2, 3, 4, 5]
{% endhighlight %}

Belirtilen indexten eleman silme

{% highlight ruby %}

arr.delete_at(2)
=> 4
arr
=> [2, 3, 5]
{% endhighlight %}

Belirtilen elemanı dizideki heryerden silme

{% highlight ruby %}

arr = [1, 2, 2, 3, 2]
arr.delete 2
=> [1, 3]
{% endhighlight %}


Dizideki `nil` değerleri kaldır

{% highlight ruby %}

arr = ['foo', 0, nil, 'bar', 7, 'baz', nil]
arr.compact
=> ['foo', 0, 'bar', 7, 'baz']
arr
=> ['foo', 0, nil, 'bar', 7, 'baz', nil]

arr.compact!
=> ['foo', 0, 'bar', 7, 'baz']
arr
=> ['foo', 0, 'bar', 7, 'baz']
{% endhighlight %}


Dizideki tekrar eden elemanları sil

{% highlight ruby %}

arr = [2, 5, 6, 556, 6, 6, 8, 9, 0, 123, 556]
arr.uniq
=> [2, 5, 6, 556, 8, 9, 0, 123]
{% endhighlight %}

### Dizilerde döngü

{% highlight ruby %}

arr = [1, 2, 3, 4, 5]
arr.each { |a| print a -= 10, " " }
-9 -8 -7 -6 -5
{% endhighlight %}


{% highlight ruby %}

arr.reverse_each { |a| print a }
54321
{% endhighlight %}


Dizideki elemanları modifiye ederek yeni bir dizi oluşturma

`map` ve `collect` metodları aynı işi görür.

{% highlight ruby %}

arr.map { |a| 2*a }   #=> [2, 4, 6, 8, 10]
arr                   #=> [1, 2, 3, 4, 5]
arr.map! { |a| a**2 } #=> [1, 4, 9, 16, 25]
arr                   #=> [1, 4, 9, 16, 25]
{% endhighlight %}

### Dizide belli koşullara uyan elemanları seçme

{% highlight ruby %}

arr = [1, 2, 3, 4, 5, 6]

# 3 ten büyükleri seç
arr.select { |a| a > 3 }
=> [4, 5, 6]

# 3 ten küçükleri çıkar
arr.reject { |a| a < 3 }
=> [3, 4, 5, 6]

# 4 ten küçükleri çıkar
arr.drop_while { |a| a < 4 }
=> [4, 5, 6]

arr
=> [1, 2, 3, 4, 5, 6]
{% endhighlight %}


### Elemanları birleştirme

{% highlight ruby %}

[ "a", "b", "c" ].join("-")
=> "a-b-c"
{% endhighlight %}

### Dizideki elemanların kombinasyonları

{% highlight ruby %}

a = [1, 2, 3]
a.permutation.to_a
=> [[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]

a.permutation(1).to_a
=> [[1],[2],[3]]

a.permutation(2).to_a
=> [[1,2],[1,3],[2,1],[2,3],[3,1],[3,2]]

a.permutation(3).to_a
=> [[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]

a.permutation(0).to_a
=> [[]] # one permutation of length 0

a.permutation(4).to_a
=> []   # no permutations of length 4
{% endhighlight %}

### Dizideki elemanlardan rastgele seçim

{% highlight ruby %}

a = [ 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 ]
a.sample
=> 7
a.sample(4)
=> [6, 4, 2, 5]
{% endhighlight %}

### Diziyi karıştır

{% highlight ruby %}

a = [ 1, 2, 3 ]
a.shuffle
=> [2, 3, 1]
{% endhighlight %}


### Kaynaklar
[ruby-doc](http://www.ruby-doc.org/core-2.0/Array.html)
