---
layout: post
title: Ruby için Yaml
comments: true
categories: [ yazılım, ruby ]
tags: [ yaml, ruby ]
description: "Ruby Türkçe, Ruby öğren, Ruby Yaml "
keywords: "Ruby Türkçe, Ruby öğren, Ruby Yaml "
# asides: []
# author:
---

[YAML](http://yaml.org): kendi sitesine göre "Tüm programlama dilleri için,
insan dostu veri sıralama standardıdır."

<!-- more -->

Bir kaç basit yaml ve onun ruby karşılıkları.

### Liste

Yaml

{% highlight ruby %}

- foo
- bar
- baz
{% endhighlight %}


Ruby

{% highlight ruby %}

['foo', 'bar', 'baz']
{% endhighlight %}


### İç içe liste

Yaml

{% highlight ruby %}

- zaa
-
  - foo
-
  - bar
  - baz
{% endhighlight %}


Ruby

{% highlight ruby %}

['zaa', ['foo'], ['bar', 'baz']]
{% endhighlight %}

### Sözlük

Yaml

{% highlight ruby %}

foo: hey
:bar:
  - baz
  - zaa
{% endhighlight %}


Ruby

{% highlight ruby %}

{"foo" => 'hey', :bar => ['baz', 'zaa']}
{% endhighlight %}




###  Kaynaklar

- [Yaml_for_ruby](http://www.yaml.org/YAML_for_ruby.html)
