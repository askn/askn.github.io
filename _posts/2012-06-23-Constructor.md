---
layout: post
title: Constructor – C#
comments: true
categories: [ yazılım ]
tags: [ c#, constructor ]
description: "c#, constructor"
keywords: "c#, constructor"
# asides: []
# author:
---

Constructor(yapılandırıcı) nesne yönelimli programlamaya ait bir terimdir.Bir nesne oluşturulduğu anda ilk çalışan fonksiyondur.
Nesnenin kullanımı için alt yapıyı hazırlar. Constructor’larda geri dönüş değeri olmaz. Sınıf ismi ile aynı isimde ki fonksiyonlardır.

c#’ta genel yapısı şu şekildedir.

<!-- more -->

{% highlight c %}
erisim Sinifismi()
{
	// kodlar
}
{% endhighlight %}

Tanımlama biçimine göre parametreli veya parametresiz kullanılabilir.

{% highlight c %}
class Hayvan
{
	public string cins;
	public int yas;
	public Hayvan()
	{
		yas = 2;
		cins = "kopek";
	}
	public Hayvan(int x, string y)
	{
		yas = x;
		cins = y;
	}
}

class Program
{
	static void Main(string[] args)
	{
		Hayvan kopek = new Hayvan();
		Console.WriteLine(kopek.cins + kopek.yas.ToString());
		Hayvan kedi = new Hayvan(3,"kedi");
		Console.WriteLine(kedi.cins + kedi.yas.ToString());
		Console.ReadKey();
	}
}
{% endhighlight %}

Her ne kadar kullanışlı bir örnek olmasa da konunun anlaşılması için yeterli.
