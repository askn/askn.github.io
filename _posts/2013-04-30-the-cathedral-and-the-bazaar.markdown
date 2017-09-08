---
layout: post
title: "The Cathedral and the Bazaar"
date: 2013-04-30 00:28
comments: true
categories: [ linux, yazılım, teknik ]
tags: [ Eric Raymond, Açık Kaynak, Unix Felsefesi ]
description: "Linux Kültürü ve Eric Raymond'un Katedral ve pazar kitabı"
keywords: "linux, eric raymond, açık kaynak, linux felsefesi, linux kültürü,
unix, yazılım"
# asides: []
# author:
---

Linus Torvalds, henüz daha öğrenciyken Tanenbaum'un Minix'ini geliştirmeye başlıyor ve
bir müddet sonra nette "Minix'te hangi özellikleri görmek isterdiniz ?" konu
başlığı ile özgür bir işletim sistemi yaptığını duyuruyor. Cevap olarak birçok
öneri ile beraber yardım teklifi geliyor. Bir müddet sonra Linus kodlarınıda
açarak herkesi ona katılmaları için çağırıyor. Eric Raymond ise bu açık yapı ile
kapalı model yapısını katedral ve pazara benzeterek anlatıyor.

<!-- more -->

Vizeler de bitmişken bayağı uzun süredir aklımda olan Raymond'un Katedral ve
Pazar denemesini okudum. Linux ve açık kaynak adına binlerce ibret var. :D Okurken
not aldığım bazı kısımların kaybolmaması için buraya da koymaya karar verdim.

Katedral: Bir kişi veya grubun daha önceden planladığı ve kendi güçleriyle planı
gerçekleştirdiği bir model. Gelişim kapalı kapılar ardında olur ve herkes sadece
bitmiş çalışmayı görür.

Pazar: düşünce üretme süreci herkese açık olan baştan itibaren test edilmek üzere
herkese dağıtılan bir model.

Katedralde bitmiş bir proje yayınlandığı için daha sonraki süreçte temellerinin değişmesi oldukça güç. Pazarda ise
geliştirilen ürün değişik yaklaşımlar ile birbirinden harika fikirlerin üzerine inşa edilir.

Eric Raymond'un denemesi şöyle başlıyor. "Kim derdi ki gezegenin orasına burasına dağılmış binlerce programcının parça parça çalışmaları büyü yapılmış gibi birleşsin ve dünya çapında bir işletim sistemi ortaya çıksın."

Raymond Linus'un izlediği yapıyı yaptığı bir açık kaynak projede uyguluyor ve oldukça başarılı sonuçlar elde ediyor. Bu zaman zarfında edindiği tecrübeleri maddeler halinde okuyucu ile paylaşıyor.

> Her iyi yazılım, programcısının kendi yarasını kaşımasıyla başlar.

Yazılım dünyasında öyle veya böyle yazılımcılar sevmedikleri programlarla
uğraşıyorlar. Ama linux dünyasında böyle değil. Belkide bu kalitenin yüksek
olmasını sağlayan en önemli etkenlerden biri.

> İyi programcı, ne yapacağını bilen programcıdır. Ama neyi yeniden yazacağını
ve kullanacağını bilen programcı, büyük programcıdır.

En yüksek not sonuca değil çabaya verilir. Ayrıca eldekiyle başlamak
sıfırdan başlamaktan iyidir. Örneğin Torvalds da sıfırdan başlamak yerine temel olarak Minix'i
kullanmıştır.

> Heba etmek hesap dahilindeyse bir şekilde heba edersin.

Bir işi hakkıyla yapmayı öğrenmek belki ikinci üçüncü denemede mümkün olur. Bir işi hakkıyla yapmak istiyorsak bir kere daha başlamaya hazır olmamız lazım.

>  Doğru yoldaysan birbirinden ilginç problemlerle karşılacaksın. 

>  Programın oluşumunda kullanıcıların katkısına başvurmak, kod geliştirmede ve
hata gidermede en etkili ve rahat yoldur. 

Biraz teşvikle kullanıcılar sorunları teşhis eder ve çözüm önerileri sunar. Linux ta kullanıcıların çoğunun programcı olması ve kaynak kodunun el altında olması hata giderme süresini oldukça kısaltıyor.
Linus, Raymond'a bir sohbet sırasında: "Ben aslında, başkalarının yaptıklarını kendime yontmaktan hoşlanan aşırı
tembel biriyim." demiş.  ( Tilki gibi tembel yani ). Not: Aynı ben :D

>  Geliştirme ortağı ve beta sınayıcı havuzu yeterince büyükse sorunlar çabucak belirlenir ve halledilir. 
Ne kadar gözden geçirirsek hatalar o kadar azalır. Her sorun zamanı geldiğinde muhakkak biri tarafından keşfedilir. Linuxta sorunu farketme ve giderme işlemi çok hızlı gerçekleşmektedir. Katedral ve pazar arasındaki temel farklardan biride budur. Katedralde hata
belirleme ve giderme işlemi gizli olarak yürütülür. Buda projede çalışanların aylarca emek harcayarak sürümler arası zamanın uzamasına neden olur ve onca zaman beklenen sürümün kusursuz olmaması hayal kırıklığı yaşatır.

Pazarda ise her sürümde birbirinden hevesli geliştirme ortaklarının elinden geçecektir. Sürümler arası zamanı kısa tutarak bu gözlemleme işini katkıyı hat safhada tutabiliriz. Ayrıca Linuxta katkı yapan kişiler o projeye kendi isteği ile girmiş o projeyi
öğrenmek isteyen, kullanan ve karşılaştığı sorunlara çözüm arayan kişilerdir. Daha fazla kullanıcı daha fazla hata bulur ayrıca kullanıcıların geliştirici ortağı olması bu etkiyi daha da güçlendirir.

> 
Akıllı veri yapıları ve aptal kodlar, kodların akıllanması ve veri yapısının
aptallaşmasından çok daha iyi işler.


Doğru bir yapı kurmak en önemli noktalardan biridir.

Raymond projesinde Linus'un yaptıklarını sınamak için onun izlediği yolu takip ediyor.

- Sürümleri erken 10 günde 1 hatta bazen günde 1 yayınlıyor.
- Temasa geçen herkesi listesine ekleyerek beta listesini genişletiyor.
- Her yeni sürümde beta listesine bir duyuru geçiyor.
- Beta listesindeki kişilerin fikirlerini alıyor.

Bu sayede gıpta edilecek cinste hata düzeltme öneriler geliyor.

> 
Beta sınayıcılarınıza en değerli kaynaklarınız olarak muamele ederseniz, en
değerli karşılığı vereceklerdir.


Hatta Raymond'un projesinde belli bir süre sonra listedeki kişiler yapının çok iyi işlediği artık mailleri görmelerine gerek kalmadığı gerekçesi ile kendilerini listeden çıkarıyorlar.

> 
İyi fikirlere ulaşmada bir sonraki en iyi adım, kullanıcılardan gelen iyi
fikirleri elde etmektir. Bazı durumlarda bir sonraki daha iyidir.


Alçakgönüllülük ile yapılan içten teşekkürler sayesinde dünya size sanki bütün
herşeyi siz keşfetmişsiniz gibi davranır.

> 
Genellikle en çarpıcı ve yenilikçi çözümlere, problem konseptinizin yanlış
olduğunu fark etmekle kavuşursunuz.


Geliştirme sürecinde duvara toslarsan, doğru yanıta ulaşıp ulaşmadığını değil
doğru soruyu sorup sormadığını sorgulamanın vakti gelmiştir. Problemi yeniden
belirlemelisin.

Eğer verimlilik kaybı olmayacaksa miyadı dolan özellikleri silmekten korkmayın.
> 
Mükemmele (tasarıma) eklenecek bir şey kalmadığında değil, eksiltilecek bir şey
kalmadığında ulaşılır.


Kod daha iyi ve yalın olduğunda doğru yolda olduğunuzu bilirsiniz.

> 
Her aletin işlevi doğrultusunda iş görmesi gerekir; ama müthiş bir alet,
işlevlerinin çok ötesinde iş görür.


> 
Bir güvenlik sistemi ancak sırrı kadar güvendedir.


###   Pazar Tarzının Gerekli Önkoşulları

Kod pazar tarzında geliştirilemez. Sınama, arıza giderme ve iyileştirme pazar
tarzında yapılabilir fakat üretim mümkün değildir. Büyüyen geliştirme
topluluğunun oynayacağı, işleyen ve sınanabilir bir şeye ihtiyacı vardır. Bir topluluğu kurmaya başladığınızda elinizde olması gereken şey makul bir
vaattir. Herşeyiniz eksik olsa bile başarısız olmamanız için gereken iki şey vardır.

- Programınız işler olmalı ve
- Gelecekte temiz bir program olacağına geliştirme ortaklarınızı ikna
etmelisiniz.

Ayrıca iletişim kurmakta geliştirici ortakları ikna etmek açısından oldukça
önemlidir.

Birşeyin sağlam ve sade olması gerektiğinde insan onu sevimli ve karmaşık hale
getirmeye başlıyor. Bu hatadan kaçınmak gerekir.

En iyi programlar yazarının bir sorununa bulduğu çözümlerle başlar ve yayılır.

> 
İlginç bir sorunu çözmek için; işe ilginç olabilecek bir sorunu bulmakla
başlayın.


> 
En az İnternet seviyesinde bir iletişim ortamıyla donatılmış bir geliştirme
koordinatörü, dayatmacı olmadan önderlik yapabilirse, çok sesliliğin tek
seslilikten iyi olacağı kesindir.


Yazılım yönetiminin beş tane fonksiyonu vardır.

- Hedef koymak ve insanları hedefe yöneltmek.
- İzlemek ve önemli ayrıntıları gözden kaçırmamak.
- Sıkıcı ve angarya işlerde insanları motive etmek.
- En yüksek verimliliği elde etmek için insan dağılımını örgütlemek.
- Projeyi sürdürmek için gereken kaynakları düzenlemek.

Özgür yazılımlarda ise bu kurallar bir nevi gereksiz duruma düşüyor. Sondan
başlayarak katılımcılar kendi isteği ile gelmişlerdir. Yani kaynak düzenlemenin
gerekliliği kendiliğinden ortadan kalkmaktadır. Çünkü herkes kendi kaynağını
ortaya koymaktadır.

Açık kaynak projelerin batma sebebi genelde geliştiricilerin isteklerini
kaybetmesidir. Açık kaynak projelerin başarısı örgütlenmekten geçiyor.

Açık kaynak projelerde herkes kendine göre seksi ( Aklıma Ünal Aysal geldi. :D ) gelen işlerle uğraşır. Sizde
bilirsiniz ki kullandığınız programda sıkıcı gördüğünüz işi bile cazip gören bir kişi yapmıştır.

İzleme ve gözden geçirme konusunda ise açık kaynak projelerin güçlü olduğu aşikar.

### Kaynak
- [The Kathedral and the bazaar](http://tr.wikipedia.org/wiki/Katedral_ve_Pazar)
