---
layout: post
title: "Rails: Hash With Indifferent Access"
date: 2015-10-24 22:35
comments: true
---

572 gün aradan sonra gelen yazımla birlikte hepinize merhaba diyor ve kucaklıyorum sevgili okuyucular.
Bugün sizlerle rails ile ilgili birkaç ufak şey paylaşacağım.

<!-- more -->

Bildiğiniz gibi ruby yazarken bir hash'in key'lerine hem sembol hem string ile erişemiyoruz. Yani ne diyor bu Tatar Ramazan ?!

{% highlight ruby %}
kac = {"arabada" => 5, "evde" => 15}
kac["arabada"] #=> 5
kac[:arabada] #=> nil
{% endhighlight %}

Eğer rails kullanıyorsanız ve böyle bir şeye ihtiyacınız varsa ActiveSupport modülünün [HashWithIndifferentAccess](https://github.com/rails/rails/blob/master/activesupport/lib/active_support/hash_with_indifferent_access.rb) sınıfı sayesinde bu çok kolay.

{% highlight ruby %}
kac = HashWithIndifferentAccess.new("arabada" => 5, "evde" => 15)
kac["arabada"] #=> 5
kac[:arabada] #=> 5
{% endhighlight %}

Yine bir cici method daha göstereyim. 

{% highlight ruby %}
kac = {"arabada" => 5, "evde" => 15}
ne_kadar = kac.with_indifferent_access
ne_kadar["arabada"] #=> 5
ne_kadar[:arabada] #=> 5
{% endhighlight %}

Söyleyeceklerim bu kadar.

**not:** Evet, saydım.

**not 2:** Ulan neyi sayacağım günden başka.

