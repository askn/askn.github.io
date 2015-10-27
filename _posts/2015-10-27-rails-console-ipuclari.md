---
layout: post
title: "Rails: Console ipuçları"
date: 2015-10-27 21:51
comments: true
---

Bugün sizlere öğrenince ufkunuzu iki katına çıkaracak bir kaç minik ipucu göstereceğim.

#### Arama

Daha önce yazdığınız bir komutu yukarı, aşağı tuşları ile history'den getirmek yerine **CTRL + R** tuş kombinasyonu sayesinde bash history'de arar gibi rails console'da da arama yapabilirsiniz.

#### Yeniden Yükle

**reload!** ile uygulamayı tekrar yükleyebiliriz.

{% highlight ruby %}
> reload!
Reloading...
true
{% endhighlight %}

#### Son işlem

**_** ile son işlenen komutun değerine erişebilirsiniz.

{% highlight ruby %}
> 1 + 2 * 4
# 9
> _ + 123
# 132
{% endhighlight %}

#### Daha İyi Oku

**to_yaml** ile aynı işe yarayan **y**'yi kullanabilirsiniz.

{% highlight ruby %}
object.to_yaml
y object
{% endhighlight %}

#### View Helperlarını Kullan

**ActionView::Base** objesi olan **helper** ile view helper methodlarını kullanabiliriz. Aslında helper, ActionView::Base class'ının ilklenmiş hali. Burada kafalar yandı anlatamadım göstereyim.

{% highlight ruby %}
helper
foo = ActionView::Base.new # Aynı bok
{% endhighlight %}

Bir kaç örnekte göstereyim.

{% highlight ruby %}
helper.link_to "Home", app.root_path
# "<a href=\"/\">Home</a>"

helper.pluralize(3, 'mouse')
#"3 mice"

helper.time_ago_in_words 3.days.ago
"3 days"
{% endhighlight %}

#### ?!(başlık bulamadım :D)

**ActionDispatch::Integration::Session** objesi olan **app** sayesinde ise uygulama içinde sahte request yapabilir, route helperlarına erişebilirsiniz.

{% highlight ruby %}
> app.root_path
# "/"
> app.get "/"
# 200
> app.response.body
# "<!DOCTYPE html><html>Home!</html>"
> app.response.success?
# true
{% endhighlight %}

#### Kaynak Kodu

**source_location** methodun tanımlı olduğu dosyanın ismini ve tanımlandığı satırı veriyor.

{% highlight ruby %}
 > location = User.instance_method(:update).source_location
[
  [0] "/Users/askingedik/.rvm/gems/ruby-2.2.1/gems/activerecord-4.2.0/lib/active_record/persistence.rb",
  [1] 245
]

> User.method(:update).source_location
[
    [0] "/Users/askingedik/.rvm/gems/ruby-2.2.1/gems/activerecord-4.2.0/lib/active_record/querying.rb",
    [1] 8
]

# Şöyle de sublime editorde açtıralım dosyayı of of of
> `subl #{location[0]}:#{location[1]}`
{% endhighlight %}

Çok iyi lan!

Aslında bugün bu konuyu yazmayacaktım, farklı bir konu yazacaktım ama uykum var. Yarına artık. (Meraklandırma işlemi tamamlandı...)

### Kaynaklar
- [Source Location](http://ruby-doc.org/core-2.2.2/Method.html#method-i-source_location)
- [pragmaticstudio](https://pragmaticstudio.com/blog/2014/3/11/console-shortcuts-tips-tricks)
- [signalvnoise](https://signalvnoise.com/posts/3176-three-quick-rails-console-tips)
