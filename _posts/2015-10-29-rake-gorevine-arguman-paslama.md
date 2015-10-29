---
layout: post
title: "Rake Görevine Arguman Paslama"
date: 2015-10-29 22:42
comments: true
---

Her gün blog yazmak çok zormuş. Şaka şaka bi zorluğu yok girince alışıyor insan, dokunmuyor yazdıkça yazası geliyor. Zaten kısa kısa yazıyorum. İstek konu kabul edilir.

Bu arada [Mert](https://twitter.com/mert_akkaya_) ve [Barış](https://twitter.com/home_baris) ile beraber [Crystal Dokümanlarını](https://github.com/crystaltr/tr.crystal-lang.org) çevirmeye başladık. Coşacazz oloooummm cuppa cuppa. (**patladılar**)


> <img width="150px" src="{{ site.baseurl }}public/images/cuppa.gif">
> Coşarken temsili.

Ahah küçük tüplü bir televizyon gibi durmadı mı?

Çok dağılmadan asıl konu neydi bakalım hemen.

#### Yöntem 1

{% highlight ruby %}
task :print do
  name = ENV['name']
  p name
end
{% endhighlight %}

{% highlight sh %}
$ rake print
nil

$ rake print name="askin"
"askin"
{% endhighlight %}


#### Yöntem 2

{% highlight ruby %}
task :print, [:name, :age] do |task, args|
  puts task
  puts "name is: #{args.name}"
  puts "age is: #{args.age}"
end
{% endhighlight %}

{% highlight sh %}
$ rake print["osman",8]
print
name is: osman
age is: 8
{% endhighlight %}

*Atlar depişirdi gafamın içinde atlar, biz yine de blog yazardık...
Saygı bizden efendim.*
