---
layout: post
title: "Ruby: Private Methodlara Nasıl Erişilir"
date: 2016-03-10 10:49
comments: true
---

Bazen objelerin private methodlarını konsol üzerinde vs. çalıştırmaya ihtiyaç duyabilirsiniz.

{% highlight ruby %}
class Foo
  private

  def bar
    "foo bar baz"
  end
end
{% endhighlight %}

Ama gizli methoda erişmeye çalışırsak kardeş sen ne yapıyorsun bu private method hatası dönüyor.

{% highlight ruby %}
> Foo.new.bar
# NoMethodError: private method `bar' called for #<Foo:0x007fed14294628>
{% endhighlight %}

Ama `send` ile çağırırsak ?

{% highlight ruby %}
> Foo.new.send(:bar)
# "foo bar baz"
{% endhighlight %}

Yuppi!

#### Kaynaklar

- [solidfoundationwebdev](http://solidfoundationwebdev.com/blog/posts/how-to-call-an-objects-private-methods-in-ruby)
- [rubyquicktips](http://rubyquicktips.com/post/2681282667/how-to-call-private-methods-on-objects)
