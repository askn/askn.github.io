---
layout: post
title: "Test: Vcr Kullanımı"
date: 2016-03-07 22:58
comments: true
---

Merhabalar bugünün programı şöyle:

- Balıklama Dalış
- Tanıtımlar
- İlk kaset
- Adeta Gerçek Bir Kesit
- İstiklal Marşı ve Kapanış

<center> *** </center>

Eğer 3. parti web servisleri ile çalışıyor/veya çalışmak zorunda kalıyorsanız internetinizin olmadığı, rate limite takılabileceğiniz, cevap süresinin uzun olduğu veya
3.parti servisin kapattık hacı bugün beş saat diyerek cevap alamayabileceğiniz anlar olabilir. Test yazarken bu tür bağımlılıklardan kurtulmak için `stubbing with vcr`.

#### Stub nedir?

Kısaca sahteleme diyebiliriz. Test yazarken bağımlılıkları gidermek için servis ile aynı sonucu döndüren bir methodla değiştirme işlemi

#### Vcr nedir?

HTTP etkileşimlerini kaydedip/kasete sarıp testleriniz esnasında hızlıca, aynı response ile defalarca kullanmanıza yarayan bir gem.

#### Kurulum

Vcr gem'ini ve kullanacağınız http kütüphanesine ait gem'i Gemfile ekleyin ve kurun. webmock, fakeweb, faraday, httparty gibi birçok aracı destekliyormuş vcr.

{% highlight ruby %}
# Gemfile
group :test do
  gem 'webmock'
  gem 'vcr'
end
{% endhighlight %}

#### Bana oradan bir ayar çek

Bu arada benim verdiğim örnekler rspec için.

{% highlight ruby %}
# spec/rails_helper.rb
VCR.configure do |c|
  # Kasetlerin bulunacağı yer
  c.cassette_library_dir = 'spec/fixtures/vcr_cassettes'
  # Kullanılacak http request servisi
  c.hook_into :webmock # or :fakeweb ..
end
{% endhighlight %}

### İlk Vcr Kaseti

Eğer `blog_kaseti` daha önce oluşturulmamışsa ilk kez çalıştığında oluşacak eğer varsa kasetten okuyacak.

{% highlight ruby %}
require 'rails_helper'

describe 'Blog', type: :request do
  it "return 200" do
    VCR.use_cassette('blog_kaseti') do
      response = Net::HTTP.get_response(URI('http://askingedik.net'))
      expect(response.code).to eq '200'
    end
  end
end
{% endhighlight %}

Bu test sonucunda `spec/fixtures/vcr_cassettes/` dizini altında `blog_kaseti.yml` dosyası oluştu. İçinde yapılan istekle ilgili bilgiler var.
Aynı sorguyu farklı cevaplar alacak şekilde farklı isimlerle kaydedebilirsiniz.

#### Tavsiyeler

Kasetin bozuk veya eski bir istek olmadığından emin olun. Mesela ben bir kez servisten gelen hatalı mesajı kaydedip ulan bozuk geliyor niye geliyor tribine girmiştim.
Dalgınlık işte :/

Biz Protel'de rspec ile birlikte vcr gem'ini neredeyse her projede kullanıyoruz ve çok memnunuz sizinde bir göz atmanızı tavsiye ederim.


### Kaynaklar

- [Stub programlamada ne demek](http://stackoverflow.com/questions/9777822/what-does-to-stub-mean-in-programming)
- [Mock ve Stub farkı](http://stackoverflow.com/questions/3459287/whats-the-difference-between-a-mock-stub)
- [Github: VCR](https://github.com/vcr/vcr)
