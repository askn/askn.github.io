---
layout: post
title: "Garantisi Benim Kardeşim"
date: 2017-12-19 00:23
comments: true
---

Selam herkese. Bugün sizlere test yazmayı öveyim diyorum. Test yazmak çok güzel mantıklı bir şey lan. Valla bak. Yazın şunu yahu.

Genelde program yazarken bir şeyler yazarsınız sonra kodu terminal, browser, postman vs her ne boksa bir şey üzerinde çalıştırır, denersiniz.
Sonrasında her yeni özellik eklediğinizde tekrar çalıştırır bir göz kontrolü yapar hah tamam süper oldu hazzı yaşayıp devam edersiniz bu döngüye.
Uygulamanız küçükse böyle devam edebilir hatta `Test neaymiş eski köye yeni adet mi getireceğiz şimdi,
ne gerek var böyle şeytan işi şeylere yahu. Bak ben daha hızlı test ediyorum zaten. Ağbi garantisi benim yaa bozulmaz diyorum bu kod.` diye savunabilirsiniz.

Uygulamanız büyümeye başladıkça daha da fena bir hal almaya başlar yavaştan. Birçok özellik ekliyorsunuz ve belki farketmeden eskilerini parçalıyorsunuz kim bilir.
Peki kod çorba oldu içinize sinmiyor ama çalışıyor refactor etmek istediniz ama aynı işlevselliği koruyabilecek misiniz yoksa `çalışıyorsa elleme` mi?

#### Zamandan Kazan

Programlamayı, bilgisayara yaptıracağın işi sen yapma felsefesi ile öğrendim ve benimsedim. Bu yüzden neden çalışıyor mu kontrolünü
ben deneyeyim ki bilgisayar denesin düşüncesindeyim. Beyin bedava ya!

Üstelik herhangi bir güncelleme yaptığımda sadece testleri çalıştırmam yeterli, benim elle test edebileceğimden çok daha hızlı bir şekilde tüm senaryoları test edecek.

Hiç düşünmediğiniz bir konuda daha zaman tasarrufu sağlayabiliyor testler. Nasıl mı hemen anlatiiim. Size bug var diye gelindi, dinlediniz ve sizin testiniz var.
Kodu açmadan geleni gönderebilirsiniz. Bizde hata olmaz aslanım!

#### Doküman

Mesela ben Crystal kodunda bir şeyin nasıl çalıştığına bakmak istersem direkt testini açıyordum.
Aynı şekilde Ruby paketleri içinde testlerine bakarak neyin nasıl çalıştığı konusunda birçok fikir sahibi oldum/oluyorum. Adeta her fonksiyona ait birer doküman hazinesi var.

### Kısa bir anı molası

Projenizde şu an çalışıyorsanız olaya hakimsinizdir. Her türlü bir şekilde götürürsünüz. Peki ya bir yıl sonra? Bir yıl önce yazılmış yere değiştirme talebi gelirse?

Çok yakın zamanda yaşadığım bir örneği aktarayım. Bir yıl önce bir özellik ekledik projelerden birine ve 3. parti bir servisle çalışıyor, fakat
canlıya alınmadı bazı sebeplerden ötürü. Bu özellik şu an tekrar gündeme geldi. Şimdi araki bulasın o servisin dokümanlarını
tekrar zaman ayırayım servis nasıl çalışıyordu vs. özellik nasıl çalışıyordu ki? Ya bozarsam tanrım ben ne yapacağım? Sizce bunları sordum mu tabii ki hayır. HAHA! Açtım testi babalar gibi yaslandım arkama baktım şöyle sonra iki üç dokunuş ve işlem tamam.

### Bir Tavsiye

Zamanla edindiğim bir alışkanlık olarak bug olarak gelen bir durumu direkt test olarak ekliyorum.
Bir de şöyle bir şey farkettim ne zaman bu çalışır yeağ deyip testi atlasam orada bir şeyler ters gitti ve düzeltmek için zaman kaybettim.

Düşünce yapımda da değişikliklere yol açtı test mevzusu. Ben bunu nasıl test edebilirim ki sorusu kod yazma şeklinizi değiştiriyor.

#### Son Söz

Testler programınızın şu an çalıştığını doğruluyor ve ileride çalışmaya devam edeceklerini garanti ediyor.
Üstelik herhangi birinin bunu elle test etmesine gerek kalmadan. Daha ne olsun.

Yazı ilginizi çektiyse belki [TDD Yaklaşımı](https://www.youtube.com/watch?v=CI_pfxHVfIk) videoma göz atarsınız?

---

> Test yazmayanlara da tepkiliyim!

<video width="300" controls="controls">
<source src="/public/cok_tepkiliyim.mp4" type="video/mp4">
</video>
