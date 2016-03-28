---
layout: post
title: "Bi gıdım feyz #1"
date: 2016-03-28 09:36
comments: true
---

Elimizdeki string sadece pozitif tam sayılardan mı oluşuyor veya string içinde herhangi bir rakam geçiyor mu?
Bu tarz soruları minik bir regex ile çözebiliriz. Örneğin sadece sayılardan mı oluşuyor sorusu için:

{% highlight ruby %}
"123abc" !~ /\D/ # => false
"123" !~ /\D/ # => true
{% endhighlight %}

Bu örnekler ile hafiften regexe alıştığınıza göre ana konuya geçeyim mi [ne dersiniz](https://www.youtube.com/watch?v=_N0RUD-tEZY)?

Bilmeyenler için codewars kod kata yapabileceğiniz eğlenirken öğreten muhteşem bir servis. Oradaki sorulardan biri de:

> Bir fonksiyon yazın verilen string içindeki tüm kelimelerin çift indexli karakterlerini büyütsün, tek indexli olanları küçültsün.

Yani beklenen

{% highlight ruby %}
weirdcase( "String" )#=> returns "StRiNg"
weirdcase( "Weird string case" );#=> returns "WeIrD StRiNg CaSe"
{% endhighlight %}

Hemen aklınıza boşluklardan kelimelere parçalayıp döngü ile indeksi çift ise büyüt tek ise küçült şeklinde basit bir çözüm gelmiştir. Yalnız değilsiniz, codewars üzerinde de bu şekilde çözüm yapan onlarca insan var.
Ruby ile bunu uygularsak şöyle bir şey oluyor.

{% highlight ruby %}
def weirdcase string
  string.split.map do |s|
    s.chars.each_with_index.map do |y,i|
      i.odd? ? y.downcase : y.upcase
    end.join
  end.join(' ')
end
{% endhighlight %}

Ama codewars üzerinde ki diğer çözümleri incelediğinizde feyz dolu bir cevap görüyorsunuz.

{% highlight ruby %}
def weirdcase string
  string.gsub(/\w{1,2}/) { $&.capitalize }
end
{% endhighlight %}

Hoayda!!

Ruby'de test yazarken fake data oluşturmak için kullandığımız [faker](https://github.com/stympy/faker/blob/master/lib/faker/internet.rb#L59-L61)'da şöyle bir kod parçası var.

{% highlight ruby %}
temp.chars.each_with_index do |char, index|
  temp[index] = char.upcase if index % 2 == 0
end
{% endhighlight %}

Bilmeyenler için ben de bu gem'i crystale [port ediyorum](https://github.com/askn/faker) <small>(varsa alırım bi starınızı)</small>. Aynı örneği dün eklerken minik bir gülümseme eşliğinde crystal ile [şu şekilde](https://github.com/askn/faker/blob/master/src/faker/internet.cr#L106) çözdüm:

{% highlight ruby %}
temp.gsub(/.{1,2}/) { |s| s.capitalize }
{% endhighlight %}

#### Kaynaklar

- [stackoverflow](http://stackoverflow.com/questions/19859282/check-if-a-string-contains-a-number)
- [ilk örnek](http://solidfoundationwebdev.com/blog/posts/check-if-a-string-only-contains-a-number-in-ruby)
- [codewars sorusu](http://www.codewars.com/kata/52b757663a95b11b3d00062d)
