---
date: '2025-12-19'
description: Aspose.PDF for Java ile PDF sayfa düzenini nasıl değiştireceğinizi, PDF
  yer imlerini nasıl düzenleyeceğinizi ve görüntüleyici ayarlarını nasıl özelleştireceğinizi
  öğrenin. Daha sorunsuz bir kullanıcı deneyimi için gezinme ve düzen tercihlerini
  ustalaştırın.
keywords:
- edit PDF bookmarks Java
- Aspose.PDF viewer settings
- configure PDF navigation Java
title: 'Java''da PDF Sayfa Düzenini Değiştir: Yer İmlerini ve Ayarları Düzenle'
url: /tr/java/bookmarks-navigation/edit-pdf-bookmarks-viewer-settings-aspose-pdf-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}
# Java'da PDF Sayfa Düzenini Değiştirin: Yer İmlerini ve Ayarları Düzenleyin

## Giriş
Karmaşık PDF belgelerinde gezinmek zorlayıcı olabilir, özellikle **change PDF page layout** ayarı doğru yapılandırılmadığında veya yer imleri yanlış noktalara işaret ettiğinde. Bu öğreticide Aspose.PDF for Java kullanarak **change PDF page layout**, **PDF yer imlerini düzenleme** ve **PDF görüntüleyici ayarlarını yapılandırma** konularını öğreneceksiniz. Sonunda, gezinme, yer imi hedefleri ve belgenin okuyuculara nasıl sunulduğu üzerinde tam kontrole sahip olacaksınız.

**Neler Öğreneceksiniz**
- Mevcut PDF yer imlerini bir sayfanın başlangıcına işaret edecek şekilde nasıl düzenleyeceğinizi.  
- PDF oluştururken yer imi hedeflerini nasıl ayarlayacağınızı.  
- Sayfa düzeni gibi görüntüleyici tercihlerini nasıl değiştireceğinizi.  
- Java'da bir PDF belgesi yüklemek ve performansı optimize etmek için pratik ipuçları.

### Hızlı Yanıtlar
- **PDF sayfa düzenini değiştirmek için birincil yöntem nedir?** `PdfContentEditor.changeViewerPreference()` metodunu `ViewerPreference.PAGE_LAYOUT_SINGLE_PAGE` ile kullanın.  
- **Bir PDF oluşturulduktan sonra yer imi hedeflerini düzenleyebilir miyim?** Evet – belgeyi yükleyin, taslağa (outline) erişin ve yeni bir `ExplicitDestination` ayarlayın.  
- **Bu özellikler için lisansa ihtiyacım var mı?** Değerlendirme için ücretsiz deneme çalışır; tam lisans tüm sınırlamaları kaldırır.  
- **Hangi Maven bağımlılığı gereklidir?** `com.aspose:aspose-pdf:25.3` (veya daha yeni).  
- **Bu, Java 11 ve üzeriyle uyumlu mu?** Kesinlikle – Aspose.PDF, Java 8+ destekler.

## “change PDF page layout” nedir?
PDF sayfa düzenini değiştirmek, sayfaların bir görüntüleyicide nasıl gösterileceğini kontrol eder—tek sayfa, sürekli, iki sayfa görünümü vb. Bu ayarın ayarlanması, özellikle uzun raporlar veya kataloglar için okunabilirliği artırır.

## Neden PDF yer imlerini düzenleyip yer imi hedeflerini ayarlamalıyız?
Yer imleri, bir içindekiler tablosu gibi çalışır. Kesin hedefler, okuyucuların doğrudan istenen bölüme atlamasını sağlar, hayal kırıklığını azaltır ve genel kullanıcı deneyimini iyileştirir.

## Önkoşullar
- **Kütüphaneler ve Bağımlılıklar**: Aspose.PDF for Java v25.3 veya daha yeni.  
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
**Lisans Edinimi**: Tam özellik erişimi için ücretsiz deneme ile başlayın veya geçici bir lisans isteyin. Üretim kullanımı için kalıcı bir lisans satın almayı düşünün.

### Temel Başlatma
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
### Java'da PDF Sayfa Düzenini Değiştirme
**Genel Bakış**: Görüntüleyici tercihlerini istediğiniz şekilde sayfaları gösterecek şekilde ayarlayın.

#### PdfContentEditor Başlatma
```java
import com.aspose.pdf.facades.PdfContentEditor;
import com.aspose.pdf.facades.ViewerPreference;

PdfContentEditor editor = new PdfContentEditor();
editor.bindPdf("YOUR_DOCUMENT_DIRECTORY/input.pdf");
```
#### Görüntüleyici Tercihlerini Değiştirme
```java
editor.changeViewerPreference(ViewerPreference.PAGE_LAYOUT_SINGLE_PAGE);
```
#### Güncellenmiş Belgeyi Kaydetme
```java
String outputDir = "YOUR_OUTPUT_DIRECTORY/settingViewerPreferences.pdf";
editor.save(outputDir);
```

### PDF Yer İmlerini Düzenleme
**Genel Bakış**: Mevcut yer imlerini belirli bir sayfanın başlangıcına doğru şekilde işaret edecek şekilde ayarlayın.

#### Yer İmlerine Erişim
```java
import com.aspose.pdf.Document;
import com.aspose.pdf.ExplicitDestination;
import com.aspose.pdf.OutlineItemCollection;

Document pdfDocument = new Document("YOUR_DOCUMENT_DIRECTORY/input.pdf");
OutlineItemCollection pdfOutline = pdfDocument.getOutlines().get_Item(1);
```
#### Yeni Bir Hedef Ayarlama
```java
pdfOutline.setDestination(
    ExplicitDestination.createDestination(pdfDocument.getPages().get_Item(1),
        ExplicitDestinationType.FitH,
        pdfDocument.getPages().get_Item(1).getMediaBox().getHeight())
);
```
#### Değişiklikleri Kaydetme
```java
String outputDir = "YOUR_OUTPUT_DIRECTORY/bookmarkShouldPointToStartOfPage.pdf";
pdfDocument.save(outputDir);
```

### PDF Oluştururken Yer İmi Hedefi Ayarlama
**Genel Bakış**: Kullanıcıları yeni oluşturulan PDF içinde istenen konumlara doğrudan yönlendiren yer imleri oluşturun.

#### Yer İmi Oluşturma ve Yapılandırma
```java
import com.aspose.pdf.GoToAction;
import com.aspose.pdf.FitVExplicitDestination;

OutlineItemCollection pdfOutline_new = new OutlineItemCollection(pdfDocument.getOutlines());
pdfOutline_new.setTitle("Test Bookmark");
pdfOutline_new.setItalic(true);
pdfOutline_new.setBold(true);
```
#### Yer İmi Hedefini Tanımlama
```java
pdfOutline_new.setAction(new GoToAction(
    new FitVExplicitDestination(pdfDocument.getPages().get_Item(2), 0)));
```
#### PDF'yi Ekleyip Kaydetme
```java
pdfDocument.getOutlines().add(pdfOutline_new);

String outputDir = "YOUR_OUTPUT_DIRECTORY/setDestinationWhileCreatingPDF.pdf";
pdfDocument.save(outputDir);
```

## Pratik Uygulamalar
1. **Dijital Kitaplar** – Her bölüm yer iminin sayfanın üst kısmına gelmesini sağlayarak kesintisiz bir okuma deneyimi sunun.  
2. **Teknik Kılavuzlar** – Kesin gezinme, mühendislerin bölümleri hızlı bulmasını sağlar, özellikle büyük PDF'lerde.  
3. **Ürün Katalogları** – Tek sayfa düzeni, tabletlerde katalogları göz atmayı daha sezgisel kılar.

## Performans Düşünceleri
- **Kaynakları Optimize Etme**: Büyük PDF'lerle çalışırken bellek tüketimini azaltmak için `Document.optimizeResources()` kullanın.  
- **Java Bellek Yönetimi**: İşlem sonrası akışları açıkça kapatın ve çöp toplayıcının nesneleri geri almasına izin verin.

## Yaygın Sorunlar ve Çözümler
- **Yer İmleri Güncellenmiyor**: Doğru taslak (outline) indeksini (`get_Item(1)` ilk üst‑seviye yer imine işaret eder) düzenlediğinizden emin olun.  
- **Görüntüleyici Tercihi Uygulanmadı**: Tercihleri değiştirdikten sonra `editor.save()` çağırdığınızdan emin olun; aksi takdirde değişiklikler yalnızca bellekte kalır.  
- **Lisans İstisnaları**: Deneme lisansı su işaretleri ekleyebilir; üretim için tam lisans alın.

## Sıkça Sorulan Sorular
**S: Java'da bir PDF belgesini yüklemenin en kolay yolu nedir?**  
**C:** `new Document("path/to/file.pdf")` kullanın; Aspose.PDF dosya formatını otomatik olarak algılar.

**S: PdfContentEditor kullanmadan sayfa düzenini değiştirebilir miyim?**  
**C:** Evet, `Document` nesnesi üzerinde `pdfDocument.getViewerPreferences().setPageLayout(...)` ile doğrudan görüntüleyici tercihlerini ayarlayabilirsiniz.

**S: Görüntüleyici düzenini değiştirmek baskıyı etkiler mi?**  
**C:** Görüntüleyici düzeni yalnızca ekrandaki gösterimi etkiler; baskı çıktısını değiştirmez.

**S: Oluşturabileceğim yer imi sayısında bir sınırlama var mı?**  
**C:** Açık bir sınırlama yok, ancak çok büyük taslak ağaçları performansı etkileyebilir; düzenli tutun.

**S: Sayfa ekleyip çıkardıktan sonra yer imi hedeflerinin doğru olmasını nasıl sağlarız?**  
**C:** Herhangi bir yapısal değişiklikten sonra mevcut sayfa indekslerini kullanarak hedefleri yeniden hesaplayın.

## Kaynaklar
- **Documentation**: [Aspose.PDF Java Reference](https://reference.aspose.com/pdf/java/)
- **Download**: [Latest Releases for Java](https://releases.aspose.com/pdf/java/)
- **Purchase**: [Buy Aspose.PDF License](https://purchase.aspose.com/buy)
- **Free Trial**: [Try Aspose.PDF Free](https://releases.aspose.com/pdf/java/)
- **Temporary License**: [Request Temporary License](https://purchase.aspose.com/temporary-license)

---

**Last Updated:** 2025-12-19  
**Tested With:** Aspose.PDF for Java v25.3  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}