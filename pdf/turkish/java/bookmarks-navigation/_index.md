---
date: 2026-08-06
description: Aspose.PDF kullanarak Java'da PDF yer imleri eklemeyi öğrenin. Bu adım
  adım kılavuz, bir TOC oluşturmayı, yer imlerini yönetmeyi ve sorunsuz gezinme için
  viewer settings yapılandırmayı kapsar.
keywords:
- how to add pdf bookmarks
- pdf navigation java
- aspose pdf bookmarks
- pdf toc java
- java pdf viewer settings
lastmod: 2026-08-06
og_description: Aspose.PDF kullanarak Java'da PDF yer imleri eklemeyi öğrenin. Bu
  adım adım kılavuz, bir TOC oluşturmayı, yer imlerini yönetmeyi ve sorunsuz gezinme
  için viewer settings yapılandırmayı kapsar.
og_image_alt: Guide to adding PDF bookmarks and navigation using Aspose.PDF for Java
og_title: Java'da Aspose.PDF ile PDF yer imleri ekleme
schemas:
- author: Aspose
  dateModified: '2026-08-06'
  description: Learn how to add PDF bookmarks in Java using Aspose.PDF. This step‑by‑step
    guide covers creating a TOC, managing bookmarks, and configuring viewer settings
    for seamless navigation.
  headline: How to add PDF bookmarks in Java with Aspose.PDF
  type: TechArticle
- questions:
  - answer: Yes. Open the encrypted document by providing the password, then generate
      the TOC as usual.
    question: Can I create a TOC for encrypted PDFs?
  - answer: Most modern readers respect the PDF OpenAction and ViewerPreferences entries,
      though a few lightweight viewers may ignore them.
    question: Does “edit PDF viewer settings” affect all PDF readers?
  - answer: The library can handle PDFs up to **5 GB**; for very large files, call
      `document.optimizeResources()` to keep memory consumption low.
    question: How large a PDF can I process with Aspose.PDF?
  - answer: Absolutely. Load each document, extract its bookmark tree, and combine
      them into a single hierarchical structure before saving.
    question: Is it possible to merge multiple TOCs from different PDFs?
  - answer: A single license covers all applications on the same machine, but review
      the licensing terms for deployment scenarios.
    question: Do I need a separate license for each Java application?
  type: FAQPage
tags:
- pdf bookmarks
- aspose.pdf
- java pdf processing
- pdf navigation
- table of contents
title: Java'da Aspose.PDF ile PDF yer imleri ekleme
url: /tr/java/bookmarks-navigation/
weight: 14
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}
# Java ile Aspose.PDF'de PDF yer imleri nasıl eklenir

PDF yer imlerini programlı olarak eklemek, statik bir belgeyi etkileşimli, kolay‑navigasyonlu bir kaynağa dönüştürmenizi sağlar. Bu rehberde Aspose.PDF for Java kullanarak **PDF yer imlerini nasıl ekleyeceğinizi** öğrenecek, bir İçindekiler Tablosu (TOC) oluşturacak, görüntüleyici tercihlerini düzenleyecek ve güncellenmiş dosyayı kaydedeceksiniz — manuel düzenleme veya üçüncü‑taraf araçları olmadan.

## Hızlı cevaplar
- **“create PDF TOC Java” ne anlama geliyor?**  
  Bu, Java ve Aspose.PDF kullanarak bir PDF içinde hiyerarşik bir İçindekiler Tablosu oluşturmak anlamına gelir, böylece okuyucular doğrudan bölümlere atlayabilir.  
- **Neden Aspose.PDF'yi gezinme için kullanmalısınız?**  
  API, yer imleri, hiperlinkler ve görüntüleyici ayarları üzerinde tam programlı kontrol sağlar, Adobe Acrobat ihtiyacını ortadan kaldırır.  
- **Bir lisansa ihtiyacım var mı?**  
  Geçici bir lisans test için çalışır; üretim dağıtımları için tam lisans gereklidir.  
- **Hangi Java sürümleri destekleniyor?**  
  Java 8 ve üzeri, en son Aspose.PDF for Java sürümleriyle tam uyumludur.  
- **Yer imlerini görüntüleyici ayarlarıyla birleştirebilir miyim?**  
  Evet—aynı API'yi kullanarak yer imlerini oluştururken veya güncellerken PDF görüntüleyici ayarlarını düzenleyebilirsiniz.

## “create PDF TOC Java” nedir?

Bir İçindekiler Tablosu (TOC), PDF içindeki bölümlere bağlanan hiyerarşik bir giriş listesidir.  
Java'da bir PDF TOC oluşturmak, bu listeyi programlı olarak oluşturup bir dizi yer imi olarak eklemekle yapılır. Aspose.PDF, her girişin başlığını, hedef sayfasını ve iç içeleme seviyesini tanımlamanıza izin verir, ardından sadece birkaç API çağrısıyla yapıyı belgeye yazar.

## Neden Aspose.PDF'yi gezinme için kullanmalısınız?

Aspose.PDF for Java, dış bağımlılıklar olmadan yer imleri ve hiperlinkler eklemenize, düzenlemenize veya silmenize olanak tanıyan tam yönetilen bir kütüphanedir.  
**50+ giriş ve çıkış formatını** destekler ve **5 GB**'a kadar PDF'leri tüm dosyayı belleğe yüklemeden işleyebilir, Windows, Linux veya macOS üzerinde yüksek performanslı gezinme kontrolü sağlar.

## Önkoşullar
- Java Development Kit (JDK) 8 veya daha yenisi.  
- Aspose.PDF for Java kütüphanesi (resmi siteden indirin).  
- Değerlendirme sınırlamalarından kaçınmak için geçici veya tam lisans dosyası.

## Mevcut eğitimler

### [Aspose.PDF for Java Kullanarak PDF'lere JavaScript Bağlantıları Ekle&#58; Belgelerde Etkileşimi Artırın](./aspose-pdf-java-javascript-links-pdfs/)
### [Aspose.PDF for Java Kullanarak PDF'lerde İçindekiler Tablosu (TOC) Oluştur&#58; Geliştirici Rehberi](./aspose-pdf-java-create-toc-in-pdfs/)
### [Aspose.PDF Java Kullanarak PDF Yer İmlerini Verimli Bir Şekilde Yönet](./manage-pdf-bookmarks-aspose-pdf-java/)
### [Aspose.PDF in Java Kullanarak PDF Yer İmlerini Genişlet&#58; Tam Kılavuz](./expand-pdf-bookmarks-aspose-java/)
### [Aspose.PDF for Java Kullanarak PDF Yer İmlerini Oluşturma ve Yönetme&#58; Kapsamlı Rehber](./create-manage-pdf-bookmarks-aspose-java/)
### [Aspose.PDF for Java Kullanarak PDF'den Hiperlinkleri Çıkarma](./extract-hyperlinks-pdf-aspose-java/)
### [Aspose.PDF for Java Kullanarak PDF Yer İmlerini Alıp Görüntüleme](./retrieve-display-pdf-bookmarks-aspose-pdf-java/)
### [Aspose.PDF for Java Kullanarak PDF Yer İmlerini Güncelleme&#58; Adım‑Adım Kılavuz](./update-pdf-bookmarks-aspose-java-tutorial/)
### [Aspose.PDF Java Kullanarak XML Yer İmlerini PDF'lere Aktarma&#58; Kapsamlı Rehber](./import-xml-bookmarks-aspose-pdf-java/)
### [Aspose.PDF for Java Kullanarak PDF'leri Bağlama&#58; Belgeler Arasında Hiperlinkleri Kolayca Oluşturun](./link-pdfs-aspose-pdf-java/)
### [Aspose.PDF Java'da Uzmanlaş&#58; PDF Yer İmlerini Düzenle & Görüntüleyici Ayarlarını Yapılandır](./edit-pdf-bookmarks-viewer-settings-aspose-pdf-java/)
### [Aspose.PDF for Java ile PDF Yer İmi Yönetimini Uzmanlaş&#58; Yer İmlerini Verimli Bir Şekilde Sil ve Yönet](./aspose-pdf-java-bookmark-management/)
### [Aspose.PDF for Java'da Uzmanlaş&#58; PDF'leri Aç, Kaydet & Yer İmleri Ekle](./master-aspose-pdf-java-open-save-bookmarks/)

## PDF Görüntüleyici Ayarlarını Daha İyi Gezinti İçin Düzenle
`ViewerPreferences` nesnesi, bir PDF'nin okuyucuda nasıl açılacağını tanımlar.  
Yer imi panelini varsayılan olarak görünür şekilde ayarlayabilir, başlangıç yakınlaştırma seviyesini belirleyebilir ve tek‑sayfa veya sürekli görünüm gibi bir sayfa düzeni seçebilirsiniz. Bu ayarlar, özellikle yüzlerce sayfalı raporlarda kullanıcıların içerik arama süresini azaltır.

## PDF Yer İmlerini Programlı Olarak Aç ve Kaydet
`Document` sınıfı, bellekte bir PDF dosyasını temsil eder.  
`new Document("input.pdf")` ile bir PDF açarsınız, `document.getBookmarks()` ile yer imi ağacını değiştirirsiniz ve ardından `document.save("output.pdf")` çağrısını yaparsınız. Bu iş akışı, dinamik bir TOC eklemenize, bölümleri yeniden düzenlemenize veya eski girişleri manuel düzenleme olmadan temizlemenize olanak tanır.

## Yaygın sorunlar ve çözümler
`LinkAction`, PDF içinde bir sayfaya yönlendiren bir hiperlink eylemini belirtir.  
`optimizeResources()`, PDF kaynaklarını optimize ederek bellek kullanımını azaltır.  

- **Kaydetme sonrası yer imleri görünmüyor** – Yer imi koleksiyonunu değiştirdikten sonra `document.save()` çağırdığınızdan emin olun.  
- **Hiperlinkler yanlış sayfalara yönlendiriyor** – `LinkAction` kullanırken hedef sayfa numaralarının sıfır‑tabanlı olduğunu doğrulayın.  
- **Görüntüleyici ayarları yoksayılıyor** – Bazı PDF okuyucular gömülü ayarları geçersiz kılar; doğrulamak için Adobe Acrobat Reader ile test edin.  
- **Büyük PDF işleme başarısız oluyor** – 2 GB'den büyük dosyalar için bellek kullanımını azaltmak amacıyla `document.optimizeResources()` kullanın.

## Sıkça Sorulan Sorular

**Q: Şifreli PDF'ler için TOC oluşturabilir miyim?**  
**A:** Evet. Şifreli belgeyi şifreyi sağlayarak açın, ardından TOC'yi normal şekilde oluşturun.

**Q: “PDF görüntüleyici ayarlarını düzenle” tüm PDF okuyucuları etkiler mi?**  
**A:** Çoğu modern okuyucu PDF OpenAction ve ViewerPreferences girişlerine saygı gösterir, ancak bazı hafif okuyucular bunları göz ardı edebilir.

**Q: Aspose.PDF ile ne kadar büyük bir PDF işleyebilirim?**  
**A:** Kütüphane **5 GB**'a kadar PDF'leri işleyebilir; çok büyük dosyalar için bellek tüketimini düşük tutmak amacıyla `document.optimizeResources()` çağırın.

**Q: Farklı PDF'lerden birden fazla TOC'yi birleştirmek mümkün mü?**  
**A:** Kesinlikle. Her belgeyi yükleyin, yer imi ağacını çıkarın ve kaydetmeden önce tek bir hiyerarşik yapıda birleştirin.

**Q: Her Java uygulaması için ayrı bir lisansa ihtiyacım var mı?**  
**A:** Tek bir lisans aynı makinedeki tüm uygulamaları kapsar, ancak dağıtım senaryoları için lisans koşullarını gözden geçirin.

## Ek kaynaklar

- [Aspose.PDF for Java Dokümantasyonu](https://docs.aspose.com/pdf/java/)
- [Aspose.PDF for Java API Referansı](https://reference.aspose.com/pdf/java/)
- [Aspose.PDF for Java'ı İndir](https://releases.aspose.com/pdf/java/)
- [Ücretsiz Destek](https://forum.aspose.com/)
- [Geçici Lisans](https://purchase.aspose.com/temporary-license/)

---

**Son Güncelleme:** 2026-08-06  
**Test Edilen:** Aspose.PDF for Java 24.12  
**Yazar:** Aspose

## İlgili Eğitimler

- [Aspose.PDF for Java API Kullanarak PDF Yer İmlerini Güncelleme: Adım‑Adım Kılavuz](/pdf/java/bookmarks-navigation/update-pdf-bookmarks-aspose-java-tutorial/)
- [Aspose.PDF for Java Kullanarak PDF'lerde İçindekiler Tablosu (TOC) Oluşturma: Geliştirici Rehberi](/pdf/java/bookmarks-navigation/aspose-pdf-java-create-toc-in-pdfs/)
- [Aspose.PDF ile Java'da PDF Yer İmlerini Al – Tam Kılavuz](/pdf/java/bookmarks-navigation/retrieve-display-pdf-bookmarks-aspose-pdf-java/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}