---
layout: post
title: "Rails: Dosya Yükleme Nasıl Test Edilir"
date: 2016-03-08 23:52
comments: true
---

Rails içinde yer alan `Rack::Test::UploadedFile.new` kısayolu [fixture_file_upload](http://api.rubyonrails.org/classes/ActionDispatch/TestProcess.html#method-i-fixture_file_upload)
methodu sayesinde testlerinizde dosya yükleme işlemi için mock data oluşturabilirsiniz.

Örnek kullanım:

{% highlight ruby %}
post '/test_url', avatar: fixture_file_upload('dizin_adi/ali_baba_ve_tatar_ramazan.png', 'image/png')
{% endhighlight %}

Ayrıca factory_girl kullanıyorsanız da factory'ler içinde de rahatlıkla kullanabilirsiniz.

#### Kaynaklar

- [apidock](http://apidock.com/rails/ActionDispatch/TestProcess/fixture_file_upload)
- [thoughtbot](https://robots.thoughtbot.com/muck-focking)

