---
layout: post
title: "Ruby ipucu: define_method"
date: 2013-07-31 19:43
comments: true
categories: [ yazılım, ruby, rails ]
tags: [ ruby on rails, ruby, yazılım, teknik ]
# asides: []
# author:
---
Class yapılarımızda aşağıdakine benzer yöntemlerin tanımlanması ayrıntılı ve
gereksizdir.

<!-- more -->

{% highlight ruby %}
def failure
  self.state = :failure
end

def error
  self.state = :error
end

def success
  self.state = :success
end
{% endhighlight %}

Bunun yerine şöyle bir kod işimizi görür.

{% highlight ruby %}
[:failure, :error, :success].each do |method|
  define_method method do
    self.state = method
  end
end
{% endhighlight %}

Başka bir örnek görelim. Rails uygulamamızda Post modelimizdeki `state` alanındaki verilere göre örneğin `published?`, `draft?`, `archived?` şeklinde metodlara ihtiyacımız var.

{% highlight ruby %}
# app/model/post.rb
class Post < ActiveRecord::Base
  STATES = %w(published, draft, archived)

  STATES.each do |s|
    define_method "#{s}?" do
      self.state == s
    end
  end
end
{% endhighlight %}

Son olarak bunları öğrenince ben:

<iframe width="620" height="360"
src="http://www.youtube.com/v/0irBWD0x-ls&start=49&end=70" frameborder="0" > </iframe>

### Kaynaklar

- [Rails Antipatterns]()
- [Refactoring Ruby Edition]()
