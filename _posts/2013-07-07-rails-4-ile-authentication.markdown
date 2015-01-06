---
layout: post
title: "Rails 4 ile Authentication İşlemleri - Model"
date: 2013-07-07 14:29
comments: true
categories: [ yazılım, ruby, rails ]
tags: [ ruby on rails, ruby, yazılım, teknik ]
description: "rails 4 için bcrypt-ruby gemi ile authentication işlemleri"
keywords: "has_secure_password, bcrypt-ruby, authentication, kimlik doğrulama"
# asides: []
# author:
---
Rails 4 ile kimlik doğrulama işlemleri nasıl
yapılıyor bu yazıda onu anlatacağım.

<!-- more -->

İlk adım olarak *Gemfile* içine parolaları şifrelemek için gerekli *bcrypt-ruby* gem'ini ekliyoruz. Ardından *bundle install* ile gemi kuruyoruz.

*email* ve *password_digest* alanları olan bir User modeli
üretelim. *password_digest* şifrelenmiş parolanın tutulacağı alan.

{% highlight sh %}

$ rails generate model User email:string password_digest:string
{% endhighlight %}


Daha sonra veritabanında tablomuzu oluşturalım.

{% highlight sh %}

$ rake db:migrate
{% endhighlight %}

User modelimize `has_secure_password` satırını ekliyoruz. Bu sayede `password`
ve `password_confirmation` şeklinde iki tane sanal özelliğimiz olacak. Bu
özellikler veritabanında tutulmamakta.

{% highlight ruby %}
# app/model/user.rb
class User < ActiveRecord::Base
  has_secure_password

  validates :password, length: { minimum: 6 }
end
{% endhighlight %}

Bu arada bu sanal özelliklere yukarıdaki gibi doğrulamalar(validates) eklemek
mümkün. Parola için `presence` kontrolü has_secure_password ile gelir, eklemenize gerek
yoktur.

{% highlight sh %}

 $ rails console
{% endhighlight %}

Test edelim.

{% highlight ruby %}

pry(main)> User
=> User(id: integer, email: string, password_digest: string, created_at: datetime, updated_at: datetime)
pry(main)> u = User.new
=> #<User id: nil, email: nil, password_digest: nil, created_at: nil, updated_at: nil>
{% endhighlight %}

Görüldüğü gibi User tablomuzda password ve password_confirmation yok.

{% highlight ruby %}

pry(main)> u.password = 123123
=> 123123
pry(main)> u.password_confirmation = 123123
=> 123123
{% endhighlight %}

Fakat atama yapabiliyorum. Eğer **has_secure_password** modelimizden silinirse
atama yapılırken hata verecektir. Password ve password_confirmation alanları yok
olacaktır. Deneyerek görmenizde fayda var.

{% highlight ruby %}

pry(main)> u.save
=> true
pry(main)> u.password_digest
=> "$2a$10$oS6bKhpkG9IMo5F1QMPTNe4esVwKRAj2FBveEbDG/M/vCF99nmtcW"
{% endhighlight %}

Parolayı boş veya eşlenmeyen şekilde girmeyi deneyelim.

{% highlight ruby %}

pry(main)> u = User.create(password:"", password_confirmation:"")
=> #<User id: nil, email: nil, password_digest: "", created_at: nil, updated_at: nil>
pry(main)> u.errors.full_messages
=> ["Password can't be blank", "Password is too short (minimum is 6 characters)"]

pry(main)> u = User.create(password: "123123", password_confirmation: "123345")
=> #<User id: nil, email: nil, password_digest: "$2a$10$j.CAyJMyIR4lBFn8bJrMDOSvP/XMXcFgTZQvPfQnXUC5...", created_at: nil, updated_at: nil>
pry(main)> u.errors.full_messages
=> ["Password confirmation doesn't match Password"]

pry(main)> u = User.create(password: "213", password_confirmation: "")
=> #<User id: nil, email: nil, password_digest: "$2a$10$NZUe5Ad3TC1a.6vT6XLYe.AHEEfvrjn4q3KZn.lfL0Gq...", created_at: nil, updated_at: nil>
pry(main)> u.errors.full_messages
=> ["Password confirmation doesn't match Password",
"Password confirmation can't be blank",
"Password is too short (minimum is 6 characters)"]
{% endhighlight %}

### Authenticate işlemi

    email: 'askn@bil.omu.edu.tr'
    parola: 123123

olan bir kullanıcı oluşturalım ve kimlik doğrulaması yapalım.

{% highlight ruby %}

pry(main)> User.create(email: "askn@bil.omu.edu.tr", password: 123123, password_confirmation:123123)
=> #<User id: 3, email: "askn@bil.omu.edu.tr", password_digest: "$2a$10$QLFKbd35ON0DRKn6TmxGIOKiJ9ELyvOIhnaE05CZJExT...", created_at: "2013-07-07 13:47:15", updated_at: "2013-07-07 13:47:15">
{% endhighlight %}

`authenticate` işlemi de has_secure_password ile gelmektedir.

{% highlight ruby %}

pry(main)> u = User.find_by(email: "askn@bil.omu.edu.tr")
=> #<User id: 3, email: "askn@bil.omu.edu.tr", password_digest: "$2a$10$QLFKbd35ON0DRKn6TmxGIOKiJ9ELyvOIhnaE05CZJExT...", created_at: "2013-07-07 13:47:15", updated_at: "2013-07-07 13:47:15">

pry(main)> u.authenticate(123123)
=> #<User id: 3, email: "askn@bil.omu.edu.tr", password_digest: "$2a$10$QLFKbd35ON0DRKn6TmxGIOKiJ9ELyvOIhnaE05CZJExT...", created_at: "2013-07-07 13:47:15", updated_at: "2013-07-07 13:47:15">

pry(main)> u.authenticate(12312)
=> false
{% endhighlight %}


Kimlik doğrulama işlemi için gerekli User modelimizi oluşturmayı bu yazımda öğrendik.

Not: `Like` atalım, attıralım *:-P*.

### Kaynaklar

- [ruby.railstutorial](http://ruby.railstutorial.org/chapters/modeling-users?version=4.0#sec-adding_a_secure_password)
- [using-hassecurepassword for rails authentication](http://www.millwoodonline.co.uk/blog/using-hassecurepassword-for-rails-authentication)
