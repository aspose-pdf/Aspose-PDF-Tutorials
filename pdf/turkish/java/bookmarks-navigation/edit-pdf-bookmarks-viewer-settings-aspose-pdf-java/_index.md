---
date: '2026-05-28'
description: Aspose.PDF for Java kullanarak tek sayfa görünümü PDF ayarlamayı, görüntüleyici
  tercihlerini değiştirmeyi, yer imlerini düzenlemeyi ve PDF ayarlarını yapılandırmayı
  öğrenin.
keywords:
- single page view pdf
- aspose pdf maven dependency
- change pdf viewer preference
- configure pdf viewer settings
- set pdf bookmark destination
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: Learn how to set single page view PDF, change viewer preferences, edit
    bookmarks, and configure PDF settings using Aspose.PDF for Java.
  headline: Single Page View PDF in Java – Change Layout & Edit Bookmarks
  type: TechArticle
- description: Learn how to set single page view PDF, change viewer preferences, edit
    bookmarks, and configure PDF settings using Aspose.PDF for Java.
  name: Single Page View PDF in Java – Change Layout & Edit Bookmarks
  steps:
  - name: '**Digital Books** – Ensure each chapter bookmark lands at the top of the
      page for a seamless reading experience.'
    text: '**Digital Books** – Ensure each chapter bookmark lands at the top of the
      page for a seamless reading experience.'
  - name: '**Technical Manuals** – Precise navigation helps engineers find sections
      quickly, especially in large PDFs.'
    text: '**Technical Manuals** – Precise navigation helps engineers find sections
      quickly, especially in large PDFs.'
  - name: '**Product Catalogs** – Single‑page layout makes browsing catalogs on tablets
      more intuitive.'
    text: '**Product Catalogs** – Single‑page layout makes browsing catalogs on tablets
      more intuitive.'
  type: HowTo
- questions:
  - answer: Use `new Document("path/to/file.pdf")`; Aspose.PDF automatically detects
      the file format.
    question: What is the easiest way to load a PDF document in Java?
  - answer: Yes, you can set viewer preferences directly on the `Document` object
      via `pdfDocument.getViewerPreferences().setPageLayout(...)`.
    question: Can I change the page layout without using PdfContentEditor?
  - answer: Viewer layout only influences on‑screen display; it does not alter the
      printed output.
    question: Does changing the viewer layout affect printing?
  - answer: No explicit limit, but extremely large outline trees may impact performance;
      keep them organized.
    question: Are there limits on the number of bookmarks I can create?
  - answer: Re‑calculate destinations using the current page indices after any structural
      changes.
    question: How do I ensure bookmark destinations are accurate after adding or removing
      pages?
  type: FAQPage
title: Java'da Tek Sayfa Görünümü PDF – Düzeni Değiştir ve Yer İmlerini Düzenle
url: /tr/java/bookmarks-navigation/edit-pdf-bookmarks-viewer-settings-aspose-pdf-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/products-backtop-button >}}
# Java'da Tek Sayfa Görünümü PDF – Düzeni Değiştir ve Yer İmlerini Düzenle

## Giriş
Okuyucular büyük bir PDF'yi açtıklarında, varsayılan görüntüleyici düzeni sürekli kaydırma yapabilir ve tek bir sayfaya odaklanmayı zorlaştırır. **single page view pdf** ayarını yapılandırarak, görüntüleyiciyi bir seferde yalnızca bir sayfa gösterecek şekilde zorlayabilirsiniz; bu, raporlar, e‑kitaplar ve kataloglar için idealdir. Bu öğreticide ayrıca mevcut PDF yer imlerini nasıl düzenleyeceğinizi, bir belge oluştururken yer imi hedeflerini nasıl ayarlayacağınızı ve Aspose.PDF for Java kullanarak diğer görüntüleyici tercihlerini nasıl ayarlayacağınızı öğreneceksiniz. Sonunda, gezinme, yer imi doğruluğu ve ekran üzerindeki düzen üzerinde tam kontrol sahibi olacaksınız.

**Öğrenecekleriniz**
- Mevcut PDF yer imlerini, bir sayfanın başlangıcına işaret edecek şekilde nasıl düzenleyeceğinizi.  
- PDF oluştururken yer imi hedeflerini nasıl ayarlayacağınızı.  
- Tek sayfa düzeni gibi görüntüleyici tercihlerini nasıl değiştireceğinizi.  
- Java'da bir PDF belgesi yüklemek ve performansı optimize etmek için pratik ipuçları.

### Hızlı Yanıtlar
- **Tek sayfa görünümü PDF'yi etkinleştirmenin temel yolu nedir?** Call `PdfContentEditor.changeViewerPreference()` with `ViewerPreference.PAGE_LAYOUT_SINGLE_PAGE`.  
- **PDF oluşturulduktan sonra yer imi hedefleri düzenlenebilir mi?** Yes – load the document, retrieve the outline, and assign a new `ExplicitDestination`.  
- **Bu özellikler için lisansa ihtiyacım var mı?** A free trial works for evaluation; a full license removes all limitations.  
- **Hangi Maven bağımlılığı gereklidir?** `com.aspose:aspose-pdf:25.3` (or later).  
- **Bu, Java 11 ve üzeriyle uyumlu mu?** Absolutely – Aspose.PDF supports Java 8+.

## “PDF sayfa düzenini değiştirme” nedir?
PDF sayfa düzenini değiştirmek, sayfaların bir görüntüleyicide nasıl gösterileceğini kontrol eder—tek sayfa, sürekli, iki sayfa görünümü vb. **single page view pdf**'yi etkinleştirmek, uzun belgeler için okunabilirliği artırır ve her sayfanın izole bir şekilde sunulmasını sağlar; bu özellikle mobil cihazlar ve tabletlerde çok faydalıdır.

## PDF yer imlerini düzenlemek ve yer imi hedeflerini ayarlamak neden önemlidir?
Yer imleri dinamik bir içindekiler tablosu gibi çalışır. Kesin hedefler, okuyucuların doğrudan istenen bölüme atlamasını sağlar, ekstra kaydırmayı ortadan kaldırır ve kullanıcı hayal kırıklığını azaltır. Bu, teknik kılavuzlar, ürün katalogları ve dijital kitaplar için daha akıcı bir gezinme deneyimi ve daha yüksek memnuniyet getirir.

## Önkoşullar
- **Kütüphaneler ve Bağımlılıklar**: Aspose.PDF for Java v25.3 veya daha yeni sürüm.  
- **Ortam**: JDK 8 veya daha yeni, Maven veya Gradle yapı aracı.  
- **Bilgi**: Temel Java programlama ve PDF kavramlarına aşinalık.

## Aspose.PDF for Java Kurulumu
### Maven Kurulumu
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-pdf</artifactId>
    <version>25.3</version>
</dependency>
```
### Gradle Kurulumu
```gradle
implementation 'com.aspose:aspose-pdf:25.3'
```
**Lisans Edinme**: Ücretsiz deneme ile başlayın veya tam özellik erişimi için geçici bir lisans isteyin. Üretim kullanımı için kalıcı bir lisans satın almayı düşünün.

### Temel Başlatma
`Document` sınıfı, Aspose.PDF'nin bellekte bir PDF dosyasını temsil eden temel nesnesidir. Bir örnek oluşturduktan sonra, tüm okuma/yazma işlemleri bu nesne üzerinden gerçekleşir.  
```java
import com.aspose.pdf.Document;

public class PDFSetup {
    public static void main(String[] args) {
        // Initialize document object
        Document pdfDocument = new Document("path/to/your/pdf");
        
        System.out.println("Aspose.PDF for Java initialized successfully.");
    }
}
```

## Uygulama Kılavuzu
### Java'da PDF Sayfa Düzenini Nasıl Değiştirilir
**Genel Bakış**: Görüntüleyici tercihlerini, sayfaları istediğiniz şekilde gösterecek şekilde ayarlayın.

#### PdfContentEditor Başlatma
`PdfContentEditor`, tüm belgeyi yeniden yazmadan görüntüleyici ayarlarını değiştirmenizi sağlayan bir yardımcı sınıftır.  
```java
import com.aspose.pdf.facades.PdfContentEditor;
import com.aspose.pdf.facades.ViewerPreference;

PdfContentEditor editor = new PdfContentEditor();
editor.bindPdf("YOUR_DOCUMENT_DIRECTORY/input.pdf");
```
#### Görüntüleyici Tercihlerini Değiştirme
**single page view pdf**'yi etkinleştirmek için, uygun enum değeriyle `changeViewerPreference()` metodunu çağırın. Bu çağrı, PDF'in içindeki görüntüleyici tercihleri sözlüğünü günceller.  
```java
editor.changeViewerPreference(ViewerPreference.PAGE_LAYOUT_SINGLE_PAGE);
```
#### Güncellenmiş Belgeyi Kaydetme
Tercihler değiştirildikten sonra, değişiklikleri diske yazmak için `save()` metodunu çağırın.  
```java
String outputDir = "YOUR_OUTPUT_DIRECTORY/settingViewerPreferences.pdf";
editor.save(outputDir);
```

## PDF Yer İmlerini Nasıl Düzenlenir
**Cevap**: Mevcut yer imlerini değiştirmek için PDF'i `Document` ile yükleyin, outline (taslak) koleksiyonunu alın, istenen `OutlineItem`'ı bulun ve doğru sayfa ve koordinatları gösteren yeni bir `ExplicitDestination` atayın. Her yer imi güncellendikten sonra belgeyi kaydederek değişiklikleri kalıcı hale getirin. Bu, kullanıcıların ekstra kaydırma yapmadan tam olarak hedeflenen bölümlere yönlendirilmesini sağlar.

#### Yer İmlerine Erişim
`OutlineItemCollection`, hiyerarşik yer imi ağacını temsil eder. Bireysel girişlerle çalışmak için bunu `Document` nesnesinden alın.  
```java
import com.aspose.pdf.Document;
import com.aspose.pdf.ExplicitDestination;
import com.aspose.pdf.OutlineItemCollection;

Document pdfDocument = new Document("YOUR_DOCUMENT_DIRECTORY/input.pdf");
OutlineItemCollection pdfOutline = pdfDocument.getOutlines().get_Item(1);
```
#### Yeni Bir Hedef Ayarlama
`ExplicitDestination`, bir yer iminin atlaması gereken kesin sayfa ve konumu tanımlar. Bunu outline (taslak) öğesinin `Destination` özelliğine atayın.  
```java
pdfOutline.setDestination(
    ExplicitDestination.createDestination(pdfDocument.getPages().get_Item(1),
        ExplicitDestinationType.FitH,
        pdfDocument.getPages().get_Item(1).getMediaBox().getHeight())
);
```
#### Değişiklikleri Kaydetme
Güncellenmiş yer imi ağacını `document.save()` metodunu çağırarak kalıcı hale getirin.  
```java
String outputDir = "YOUR_OUTPUT_DIRECTORY/bookmarkShouldPointToStartOfPage.pdf";
pdfDocument.save(outputDir);
```

## PDF Oluştururken Yer İmi Hedefi Nasıl Ayarlanır
**Cevap**: PDF oluştururken, `OutlineItem` nesneleri oluşturarak, başlıklarını ayarlayarak ve belirli bir sayfa ve görünüm modunu hedefleyen bir `ExplicitDestination` tanımlayarak yer imlerini anında oluşturabilirsiniz. Her yer imini belge taslak koleksiyonuna ekleyin ve belgeyi kaydedin; böylece ortaya çıkan dosya kullanıma hazır bir gezinme ağacına sahip olur.

#### Yer İmi Oluşturma ve Yapılandırma
`OutlineItem`, PDF taslağındaki tek bir yer imi girişini temsil eder. Sıfırdan bir PDF oluştururken, yeni bir `OutlineItem` örneği oluşturup belge taslak koleksiyonuna ekleyin.  
```java
import com.aspose.pdf.GoToAction;
import com.aspose.pdf.FitVExplicitDestination;

OutlineItemCollection pdfOutline_new = new OutlineItemCollection(pdfDocument.getOutlines());
pdfOutline_new.setTitle("Test Bookmark");
pdfOutline_new.setItalic(true);
pdfOutline_new.setBold(true);
```
#### Yer İmi Hedefini Tanımlama
Hedef sayfanın üst kısmına görüntüyü konumlandırmak için `ExplicitDestination.createFitH(page, top)` metodunu kullanın.  
```java
pdfOutline_new.setAction(new GoToAction(
    new FitVExplicitDestination(pdfDocument.getPages().get_Item(2), 0)));
```
#### PDF'yi Ekleyip Kaydetme
Son olarak, yer imini outline'a ekleyin ve belgeyi kaydedin.  
```java
pdfDocument.getOutlines().add(pdfOutline_new);

String outputDir = "YOUR_OUTPUT_DIRECTORY/setDestinationWhileCreatingPDF.pdf";
pdfDocument.save(outputDir);
```

## Pratik Uygulamalar
1. **Dijital Kitaplar** – Her bölüm yer iminin sayfanın üst kısmına gelmesini sağlayarak kesintisiz bir okuma deneyimi sunun.  
2. **Teknik Kılavuzlar** – Kesin gezinme, mühendislerin büyük PDF'lerde bölümleri hızlıca bulmasını sağlar.  
3. **Ürün Katalogları** – Tek sayfa düzeni, tabletlerde katalogları gezinmeyi daha sezgisel hâle getirir.

## Performans Düşünceleri
- **Kaynakları Optimize Etme**: Aspose.PDF, akış mimarisi sayesinde tüm dosyayı belleğe yüklemeden 2 GB'a kadar PDF işleyebilir. Bellek kullanımını daha da azaltmak için `Document.optimizeResources()` metodunu kullanın.  
- **Java Bellek Yönetimi**: İşlem sonrası akışları açıkça kapatın ve çöp toplayıcının nesneleri geri almasına izin verin; böylece bellek sızıntılarını önlersiniz.

## Yaygın Sorunlar ve Çözümler
- **Yer İmleri Güncellenmiyor**: Doğru outline indeksini ( `get_Item(1)` ilk üst‑seviye yer imine işaret eder) değiştirdiğinizden emin olun.  
- **Görüntüleyici Tercihi Uygulanmadı**: Tercihleri değiştirdikten sonra `editor.save()` metodunu çağırdığınızdan emin olun; aksi takdirde değişiklikler yalnızca bellekte kalır.  
- **Lisans İstisnaları**: Deneme lisansı filigran ekleyebilir; üretim için tam lisans edinin.

## Sıkça Sorulan Sorular
**S: Java'da bir PDF belgesini yüklemenin en kolay yolu nedir?**  
C: `new Document("path/to/file.pdf")` kullanın; Aspose.PDF dosya formatını otomatik olarak algılar.

**S: PdfContentEditor kullanmadan sayfa düzenini değiştirebilir miyim?**  
C: Evet, `Document` nesnesi üzerinden `pdfDocument.getViewerPreferences().setPageLayout(...)` ile doğrudan görüntüleyici tercihlerini ayarlayabilirsiniz.

**S: Görüntüleyici düzenini değiştirmek baskıyı etkiler mi?**  
C: Görüntüleyici düzeni yalnızca ekrandaki görüntüyü etkiler; basılan çıktıyı değiştirmez.

**S: Oluşturabileceğim yer imi sayısında bir sınırlama var mı?**  
C: Açık bir sınırlama yoktur, ancak çok büyük outline ağaçları performansı etkileyebilir; yer imlerini düzenli tutun.

**S: Sayfalar ekleyip/çıkarıldıktan sonra yer imi hedeflerinin doğru olmasını nasıl sağlarız?**  
C: Yapısal değişikliklerden sonra mevcut sayfa indekslerini kullanarak hedefleri yeniden hesaplayın.

## Kaynaklar
- **Documentation**: [Aspose.PDF Java Reference](https://reference.aspose.com/pdf/java/)
- **Download**: [Latest Releases for Java](https://releases.aspose.com/pdf/java/)
- **Purchase**: [Buy Aspose.PDF License](https://purchase.aspose.com/buy)
- **Free Trial**: [Try Aspose.PDF Free](https://releases.aspose.com/pdf/java/)
- **Temporary License**: [Request Temporary License](https://purchase.aspose.com/temporary-license)

---

**Son Güncelleme:** 2026-05-28  
**Tested With:** Aspose.PDF for Java v25.3  
**Author:** Aspose

## İlgili Öğreticiler

- [Aspose.PDF for Java Kullanarak PDF Görüntüleyici Tercihlerini Değiştirme: Kapsamlı Bir Rehber](/pdf/java/printing-rendering/modify-pdf-viewer-preferences-aspose-pdf-java/)
- [Aspose.PDF for Java Kullanarak PDF Yer İmleri Oluşturma ve Gezintiyi Yönetme](/pdf/java/bookmarks-navigation/create-manage-pdf-bookmarks-aspose-java/)
- [Aspose.PDF Java için PDF Yer İmleri ve Gezinti Öğreticileri](/pdf/java/bookmarks-navigation/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}