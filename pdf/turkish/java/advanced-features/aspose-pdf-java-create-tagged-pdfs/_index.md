---
date: '2025-11-28'
description: Aspose PDF geçici lisansını kullanarak Java ile erişilebilir etiketli
  PDF'ler oluşturmayı öğrenin. Adım adım rehber, kod örnekleri ve en iyi uygulamalar.
keywords:
- aspose pdf temporary license
- tagged PDFs
- accessibility with Aspose.PDF
- create structured PDFs
title: Aspose PDF Geçici Lisansı – Java'da Etiketli PDF'ler
url: /tr/java/advanced-features/aspose-pdf-java-create-tagged-pdfs/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}
# Aspose PDF Geçici Lisansı – Java'da Etiketli PDF'ler

## Giriş
Bu kılavuzda, **Aspose PDF geçici lisansını** nasıl kullanarak **Aspose.PDF for Java** ile erişilebilir etiketli PDF'ler oluşturacağınızı öğreneceksiniz. PDF'leri erişilebilir hâle getirmek, ekran okuyuculara güvenen kullanıcılar için çok önemlidir ve geçici bir lisans, tam özellik setini ön ödeme yapmadan değerlendirmenizi sağlar. Kurulum, mantıksal yapı oluşturma ve son belgeyi kaydetme adımlarını, kodu basit ve üretime hazır tutarak adım adım göstereceğiz.

**Öğrenecekleriniz**
- Aspose PDF geçici lisansını nasıl alıp uygulayacağınız
- Maven veya Gradle ile Aspose.PDF for Java kurulumu
- Başlıklar, dil ayarları, bölümler ve bölümlendirmelerle mantıksal bir yapı oluşturma
- Yardımcı teknolojiler için hazır, tam etiketli bir PDF kaydetme
- Etiketli PDF'lerin değer kattığı gerçek dünya senaryoları

---

## Hızlı Yanıtlar
- **Aspose PDF geçici lisansı nedir?** Değerlendirme için tüm Aspose.PDF özelliklerini açan kısa vadeli, ücretsiz bir lisans.  
- **Etiketli PDF oluşturmak için lisansa ihtiyacım var mı?** Evet, etiketleme özelliklerini etkinleştirmek için geçici veya tam bir lisans gereklidir.  
- **Hangi Java yapı araçları destekleniyor?** Maven ve Gradle tamamen desteklenmektedir.  
- **Belge dilini ve başlığını ayarlayabilir miyim?** Kesinlikle – API, erişilebilirlik için her ikisini de tanımlamanıza olanak tanır.  
- **Oluşturulan PDF PDF/UA ile uyumlu mu?** Etiketli yapı, PDF/UA önerilerine uygun olarak uyumluluğu artırır.

---

## Aspose PDF Geçici Lisansı Nedir?
Bir **Aspose PDF geçici lisansı**, Aspose.PDF for Java'nın tam işlevselliğine, etiketleme, dil ayarları ve mantıksal yapı manipülasyonu gibi gelişmiş erişilebilirlik özelliklerine erişmenizi sağlayan zaman sınırlı bir anahtardır. Test, kanıt konsepti projeleri veya kalıcı bir lisans almadan kütüphaneyi değerlendirmek için idealdir.

## Etiketli PDF'ler İçin Geçici Lisans Neden Kullanılmalı?
- **Sıfır maliyetli değerlendirme:** Etiketleme, yapı ve uyumluluk özelliklerini ödeme yapmadan deneyin.  
- **Tam özellik seti:** Özellik kısıtlaması yok – ücretli lisansla aynı API yüzeyine sahipsiniz.  
- **Hızlı entegrasyon:** Kütüphaneyi çabucak entegre edin, erişilebilir PDF'ler oluşturun ve paydaşlara değeri gösterin.  
- **Uyumluluk testi:** Lisans almadan önce PDF/UA veya WCAG standartlarına uygunluğunuzu doğrulayın.

## Önkoşullar
Başlamadan önce aşağıdakilerin kurulu olduğundan emin olun:

- **Java Development Kit (JDK):** 8 veya üzeri sürüm.  
- **Aspose.PDF for Java Kütüphanesi:** 25.3 veya daha yeni bir sürüm (geçici lisans, son sürümlerle çalışır).  
- **Maven veya Gradle:** Bağımlılık yönetimi için.  
- **Geçici lisans dosyası:** Aspose lisans sayfasından temin edin (aşağıdaki bağlantıya bakın).

### Gerekli Kütüphaneler ve Bağımlılıklar
Aspose.PDF'yi projenize aşağıdaki yapı araçlarından biriyle ekleyin.

#### Maven
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-pdf</artifactId>
    <version>25.3</version>
</dependency>
```

#### Gradle
```gradle
implementation 'com.aspose:aspose-pdf:25.3'
```

### Lisans Edinimi
Ücretsiz denemeler için **geçici lisans** alın veya tüm özellikleri açmak için tam lisans satın alın. Daha fazla bilgi için [Aspose'un lisans sayfasını](https://purchase.aspose.com/temporary-license/) ziyaret edin.

## Aspose.PDF for Java'ı Kurma
Proje yönetim aracınıza (Maven/Gradle) bağımlılığı ekleyin. Ardından kütüphaneyi başlatın:

```java
import com.aspose.pdf.Document;

public class SetupAspose {
    public static void main(String[] args) {
        // Initialize the Document object
        Document document = new Document();
        System.out.println("Aspose.PDF Initialized Successfully!");
    }
}
```

## Uygulama Kılavuzu

### Etiketli PDF Belgesi Oluşturma ve Yapılandırma
**Genel Bakış:** Erişilebilirliği sağlamak için etiketli bir PDF oluşturun.

#### Adım 1: Gerekli Paketleri İçe Aktarın
```java
import com.aspose.pdf.Document;
import com.aspose.pdf.tagged.ITaggedContent;
```

#### Adım 2: Belge Dizinini Ayarlayın
Çıktı dosyalarınızı kaydedeceğiniz belge dizinini tanımlayın.

```java
String dataDir = "YOUR_DOCUMENT_DIRECTORY";
Document document = new Document();
ITaggedContent taggedContent = document.getTaggedContent();

// Configure title and language for accessibility
taggedContent.setTitle("Tagged Pdf Document");
taggedContent.setLanguage("en-US");
```
- **Neden:** Başlık ve dil ayarları, ekran okuyucuların belgenizi doğru yorumlamasını sağlar.

### Bölümler ve Bölümlendirmeler İçin Mantıksal Bir Yapı Oluşturma
**Genel Bakış:** Daha iyi gezinme için içerikleri bölümler ve bölümlendirmeler içinde mantıksal olarak düzenleyin.

#### Adım 1: Mantıksal Yapı Öğelerini İçe Aktarın
```java
import com.aspose.pdf.tagged.logicalstructure.elements.StructureElement;
import com.aspose.pdf.tagged.logicalstructure.elements.grouping.DivElement;
import com.aspose.pdf.tagged.logicalstructure.elements.grouping.SectElement;
```

#### Adım 2: Belge Yapısını Oluşturun
PDF'nizde bölümler ve bölümlendirmeler oluşturun.

```java
String outputDir = "YOUR_OUTPUT_DIRECTORY";
StructureElement rootElement = taggedContent.getRootElement();

// Create sections
SectElement sect1 = taggedContent.createSectElement();
rootElement.appendChild(sect1);

SectElement sect2 = taggedContent.createSectElement();
rootElement.appendChild(sect2);

// Add divisions to sections
DivElement div11 = taggedContent.createDivElement();
sect1.appendChild(div11);
DivElement div12 = taggedContent.createDivElement();
sect1.appendChild(div12);

ArtElement art21 = taggedContent.createArtElement();
sect2.appendChild(art21);
ArtElement art22 = taggedContent.createArtElement();
sect2.appendChild(art22);

// Further divide sections
DivElement div211 = taggedContent.createDivElement();
art21.appendChild(div211);
DivElement div212 = taggedContent.createDivElement();
art21.appendChild(div212);

DivElement div221 = taggedContent.createDivElement();
art22.appendChild(div221);
DivElement div222 = taggedContent.createDivElement();
art22.appendChild(div222);

// Add another section
SectElement sect3 = taggedContent.createSectElement();
rootElement.appendChild(sect3);

DivElement div31 = taggedContent.createDivElement();
sect3.appendChild(div31);
```
- **Neden:** Mantıksal bir yapı, kullanıcıların içeriği verimli bir şekilde gezebilmesi için erişilebilirliğin temelidir.

### Etiketli PDF Belgesini Kaydet
**Genel Bakış:** Yapılandırılmış belgenizi belirlenen dizine kaydederek işlemi tamamlayın.

```java
document.save(outputDir + "/StructureElementsTree.pdf");
```

## Pratik Uygulamalar
Etiketli PDF'ler çeşitli senaryolarda faydalıdır:

1. **Eğitim Materyalleri:** Yardımcı teknolojileri kullanan öğrenciler için erişilebilirliği artırır.  
2. **Kamu Yayınları:** PDF/UA gibi erişilebilirlik standartlarına uyumu sağlar.  
3. **Kurumsal Raporlar:** Paydaşlar için gezinmeyi ve kullanıcı deneyimini iyileştirir.

Aspose.PDF'yi iş akışınıza entegre etmek, bu kullanım durumları boyunca belge yönetimini kolaylaştırır.

## Performans Düşünceleri
- **Bellek Kullanımını Optimize Edin:** Büyük belgelerle çalışırken verimli veri yapıları kullanın.  
- **Kaynak Yönetimi:** Kullanılmayan nesneleri hemen serbest bırakarak belleği boşaltın.  
- **Güncel Kalın:** Performans iyileştirmeleri ve hata düzeltmeleri için en son Aspose.PDF sürümüne düzenli olarak yükseltin.

## Yaygın Sorunlar ve Çözümler
| Sorun | Çözüm |
|-------|----------|
| **Lisans uygulanmadı** | Geçici lisans dosyasının belge oluşturulmadan önce doğru yüklendiğini doğrulayın. |
| **Çıktıda etiket eksik** | `document.getTaggedContent()` metodunu çağırdığınızdan ve yapı öğeleri eklemeden önce başlık/dil ayarlarını yaptığınızdan emin olun. |
| **Büyük PDF'lerde OutOfMemoryError** | `Document.optimizeResources()` metodunu kullanın ve mümkünse PDF'yi parçalara bölerek işleyin. |
| **Yanlış dil kodu** | Ekran okuyucu beklentileriyle uyumlu olması için ISO‑639‑1 kodlarını (ör. `en-US`, `fr-FR`) kullanın. |

## Sık Sorulan Sorular

**S: Etiketli PDF nedir?**  
C: Etiketli bir PDF, ekran okuyucuların belgeyi doğru yorumlamasını sağlayan anlamsal bir yapı içerir.

**S: Aspose.PDF'yi diğer Java çerçeveleriyle kullanabilir miyim?**  
C: Evet, Aspose.PDF, popüler Java çerçeveleri ve Maven, Gradle gibi yapı araçlarıyla sorunsuz entegrasyon sağlar.

**S: Büyük belgeleri verimli bir şekilde nasıl yönetirim?**  
C: Kaynakları dikkatli yöneterek ve kütüphaneyi güncel tutarak bellek kullanımını optimize edin.

**S: Etiketli PDF'ler için Aspose.PDF kullanmanın faydaları nelerdir?**  
C: Erişilebilir belgeler oluşturmayı basitleştirir, manuel etiket yönetimine gerek kalmadan erişilebilirlik standartlarına uyumu sağlar.

**S: Sorun yaşarsam destek alabilir miyim?**  
C: Evet, topluluk ve Aspose uzmanlarından yardım almak için [Aspose'un Destek Forumunu](https://forum.aspose.com/c/pdf/10) ziyaret edebilirsiniz.

## Kaynaklar
- **Dokümantasyon:** Ayrıntılı kılavuzlar için [Aspose PDF Java Documentation](https://reference.aspose.com/pdf/java/) adresini inceleyin.  
- **Kütüphane İndirme:** En son sürümleri [Aspose Downloads](https://releases.aspose.com/pdf/java/) üzerinden alın.  
- **Satın Alma:** Lisans için [Aspose Purchase Page](https://purchase.aspose.com/buy) adresini ziyaret edin.  
- **Ücretsiz Deneme:** [Aspose Free Trials](https://releases.aspose.com/pdf/java/) üzerinden deneme sürümüne başlayın.  
- **Geçici Lisans:** Değerlendirme için geçici erişim sağlayan [Aspose Temporary License](https://purchase.aspose.com/temporary-license/) sayfasına göz atın.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

---

**Son Güncelleme:** 2025-11-28  
**Test Edilen Versiyon:** Aspose.PDF for Java 25.3  
**Yazar:** Aspose  

---