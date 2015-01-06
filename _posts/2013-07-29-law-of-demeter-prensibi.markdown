---
layout: post
title: "Rails: Law of demeter Prensibi"
date: 2013-07-29 05:49
comments: true
categories: [ yazılım, ruby, rails ]
tags: [ ruby on rails, ruby, yazılım, teknik ]
# asides: []
# author:
---
Örneğin elimizde `Customer`, `Address`, `Invoice` modelleri olan bir proje olsun.

<!-- more -->

Şu şekilde birbileri ile bağlantıları olsun.

{% highlight ruby %}
#   app/model/customer.rb
class Customer < ActiveRecord::Base
  has_one :address
  has_many :invoices
end

{% endhighlight %}


{% highlight ruby %}
#   app/model/address.rb
class Address < ActiveRecord::Base
  belongs_to :customer
end
{% endhighlight %}


{% highlight ruby %}
#   app/model/invoice.rb
class Invoice < ActiveRecord::Base
  belongs_to :customer
end
{% endhighlight %}

Invoice view'lerinden birinde faturanın sahibinin adını öğrenmek isteyelim, veya
faturanın sahibine ait adres tablosundan cadde, şehir.. vs. görmek
isteyelim. Yani lafı uzatmadan:

{% highlight ruby %}
@invoice.customer.name
@invoice.customer.address.street
@invoice.customer.address.city
{% endhighlight %}

Okurken bile insan yoruldu değil mi `:P`.

Law of demeter prensibine göre

- Her yapı kendisi ile ilgili yapılarla konuşmalı, yabancı yapılarla konuşmamalı
- Her birim diğer birimler hakkında sınırlı bilgiye sahip olmalı

Olabildiğince az nokta koymalıyız. Peki ama nasıl ?

{% highlight ruby %}
#   app/model/customer.rb
class Customer < ActiveRecord::Base
  has_one :address
  has_many :invoices

  def street
    address.street
  end

  def city
    address.city
  end
end
{% endhighlight %}


{% highlight ruby %}
#   app/model/address.rb
class Address < ActiveRecord::Base
  belongs_to :customer
end
{% endhighlight %}


{% highlight ruby %}
#   app/model/invoice.rb
class Invoice < ActiveRecord::Base
  belongs_to :customer

  def customer_street
    customer.street
  end

  def customer_city
    customer.city
  end

  def customer_name
    customer.name
  end
end
{% endhighlight %}

Peki view'de nasıl kullanılıyor şimdi görelim.

{% highlight ruby %}
@invoice.customer_name
@invoice.customer_street
@invoice.customer_city
{% endhighlight %}

Noktaları, alt tirelerle değiştirdik.
Baya anlamlı, kolay okunan kod oldu işimizi görür. Fakat aklınıza malum soru
geldi hemen. Modelde böyle elli tane fonksiyon mu yazacağım ben. Tabi ki hayır
görelim, oynat uğuorcuumm.

{% highlight ruby %}
#   app/model/customer.rb
class Customer < ActiveRecord::Base
  has_one :address
  has_many :invoices

  delegate :street,
           :city,
           to: :address
end

{% endhighlight %}


{% highlight ruby %}
#   app/model/address.rb
class Address < ActiveRecord::Base
  belongs_to :customer
end
{% endhighlight %}


{% highlight ruby %}
#   app/model/invoice.rb
class Invoice < ActiveRecord::Base
  belongs_to :customer

  delegate :street,
           :city,
           :name,
           to: :customer,
           prefix: true
end
{% endhighlight %}

View'de tekrar görelim.

{% highlight ruby %}
@invoice.customer_name
@invoice.customer_street
@invoice.customer_city
{% endhighlight %}

`delegate`'i çaktın mı işlem tamam `:P`

### Kaynaklar

- [Rails Antipatterns Kitabı]()
- [Law of demeter prensibi](http://www.tanerdiler.com/article/5-law-of-demeter-prensibi)
- [haacked.com](http://haacked.com/archive/2009/07/13/law-of-demeter-dot-counting.aspx)
