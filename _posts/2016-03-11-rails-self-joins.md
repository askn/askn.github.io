---
layout: post
title: "Rails: Self Joins"
date: 2016-03-11 11:02
comments: true
---

Hepiniz fight club filmini izlemişsinizdir veya duymuşsunuzdur. `self join` filmin sonunda ana karakter için Tyler'ın<small>(Brad Pitt)</small> kendisi çıkması gibi bir olay.
Aslında kendisiymiş ya la diyorsunuz.

> Az önce spoiler yediniz. Afiyet olsun.

<center> *** </center>

Hepimiz günlük hayatta çalışanların birbirine bağlı olduğu bir sistem içindeyiz. Herkes aslında bir çalışan ama başka bir çalışana da bağlı.

Yemek söylerken gördüğümüz çoğu menü'de kategoriler var onların altında onlara bağlı başka kategoriler var.

Herkesin sosyal medya üzerinde yüzlerce arkadaşı var, sisteme tepeden baktığımızda hepimiz birer kullanıcıyız, diğer kullanıcılara bağlıyız.
(Yine mühendis kafasıyla açıklama yaptım kahrolsun!)

Ben sizlere kendi kendine bağlı olan bu sistemlerin veri modellemesini nasıl yapacağız onu anlatacağım.

###  One to Many (1-M)

Örneğin, bir tabloda tüm çalışanlarımızı tutmak istiyoruz ve her çalışanın bir yöneticisi olsun.

{% highlight ruby %}
class Employee < ActiveRecord::Base
  has_many :subordinates, class_name: "Employee",
                          foreign_key: "manager_id"

  belongs_to :manager, class_name: "Employee"
end
{% endhighlight %}

Modelimizi bu şekilde güncelledikten sonra artık çalışanın yöneticisine ve ona bağlı olan çalışanlara erişebiliyoruz.

{% highlight ruby %}
@employee.subordinates
@employee.manager
{% endhighlight %}

Tabii gerekli migration'ları eklemeyi unutmayın.

### Many to Many (M-N)

Bir arkadaşlık sistemi yazacağımızı düşünelim, elimizde User isminde bir modelimiz var. User'lar User'lar ile eşleşiyor. Burada şöyle bir yol izleyebiliriz.

Friendship isminde ara bir model oluşturalım ve içinde `user_id` ile `friend_id` alanları olsun. Gerekli migration'ları ekledikten sonra modellerimizi de şöyle ilişkilendirelim.

{% highlight ruby %}
# app/models/friendship.rb
class Friendship < ActiveRecord::Base
  belongs_to :user
  belongs_to :friend, class_name: "User"
end
{% endhighlight %}

{% highlight ruby %}
# app/models/user.rb
class User < ActiveRecord::Base
  has_many :friendships
  has_many :friends, through: :friendships
end
{% endhighlight %}

{% highlight ruby %}
ali = User.find_by(email: 'ali@example.com')
ayse = User.find_by(email: 'ayse@example.com')
ali.friends << ayse
ali.friends # => [ayse]

ayse.friends # => []
{% endhighlight %}

Hoayda! Bunu callback düzenlemeleri ile arkadaşlık ilişkisi kurulduğunda çift taraflı oluşturabiliriz. Peki nasıl?

{% highlight ruby %}
# app/models/friend.rb
class Friend < ActiveRecord::Base
  belongs_to :user
  belongs_to :friends, class_name: "User"

  after_create :create_inverse, unless: :has_inverse?
  after_destroy :destroy_inverses, if: :has_inverse?

  def create_inverse
    self.class.create(inverse_friend_options)
  end

  def destroy_inverses
    inverses.destroy_all
  end

  def has_inverse?
    self.class.exists?(inverse_friend_options)
  end

  def inverses
    self.class.where(inverse_friend_options)
  end

  def inverse_friend_options
    { friend_id: user_id, user_id: friend_id }
  end
end
{% endhighlight %}

<img align="right" src="/public/images/self.png" width="220px">
Bu eklemeler sonrası artık bir arkadaşlık kurulduğunda iki taraflı oluşacak. Silindiğinde de iki taraflı silinecek. Bu aslında biraz takip sistemine benziyor.

Facebook üzerinden konuşacak olursak, bir kişiyi takip edebilirsiniz, eğer o da sizi takip ederse arkadaş olursunuz. Şu anki haliyle ilerde böyle bir yapı da oldukça kolay bir şekilde kurulabilir.

[Railscasts](http://railscasts.com/episodes/163-self-referential-association) videosunda ise foreign_key değiştirilerek başka bir ilişki daha kuruluyor senin eklediklerin ve seni ekleyenler gibi iki ayrı ilişki var.

Kolay gelsin.

#### Kaynaklar

- [guides.rubyonrails](http://guides.rubyonrails.org/association_basics.html#self-joins)
- [youtube](https://www.youtube.com/watch?v=6ap6iLMuqJ8)
- [collectiveidea](http://collectiveidea.com/blog/archives/2015/07/30/bi-directional-and-self-referential-associations-in-rails/)
- [railscasts](http://railscasts.com/episodes/163-self-referential-association)
