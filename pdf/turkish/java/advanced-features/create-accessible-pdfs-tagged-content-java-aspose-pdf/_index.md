---
date: '2025-12-01'
description: Aspise.PDF for Java kullanarak erişilebilir PDF dosyaları oluşturmayı,
  PDF tabloları üretmeyi ve ekran okuyucular için PDF'leri etiketlemeyi öğrenin.
keywords:
- accessible PDFs with Java
- Aspose.PDF for Java
- tagged PDF creation
title: Aspose.PDF Kullanarak Java'da Etiketli İçerikli Erişilebilir PDF Oluşturma
url: /tr/java/advanced-features/create-accessible-pdfs-tagged-content-java-aspose-pdf/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}
# Aspose.PDF Kullanarak Java'da Etiketli İçerikli Erişilebilir PDF Oluşturma

**Erişilebilir PDF** belgeleri oluşturmak, yardımcı teknolojilere bağlı kullanıcılar da dahil olmak üzere tüm kullanıcıların içeriğinizi okuyup etkileşimde bulunabilmesini sağlamak açısından önemlidir. Bu öğreticide, **erişilebilir PDF** dosyalarını etiketli içerikle nasıl oluşturacağınızı, PDF tabloları oluşturmayı ve ekran okuyucuların yapıyı doğru yorumlaması için belge dilini nasıl ayarlayacağınızı öğreneceksiniz.

## Hızlı Yanıtlar
- **Hangi kütüphaneyi kullanmalıyım?** Aspose.PDF for Java.  
- **Uygulama ne kadar sürer?** Temel bir etiketli PDF için yaklaşık 15‑20 dakika.  
- **Lisans gerekir mi?** Geliştirme için ücretsiz deneme sürümü yeterlidir; üretim için kalıcı bir lisans gereklidir.  
- **Tablolar oluşturabilir miyim?** Evet – API, etiketli yapı ile PDF tabloları oluşturmanıza ve biçimlendirmenize olanak tanır.  
- **PDF'i ekran okuyucuların okuyabilmesini nasıl sağlarım?** İçeriği etiketleyin, dili ayarlayın ve yapısal öğeler için alternatif metin sağlayın.

## “create accessible pdf” nedir?
Bir **erişilebilir PDF**, başlıklar, tablolar, paragraflar ve diğer öğeleri tanımlayan mantıksal bir yapı (etiketler) içerir. Bu yapı, görsel veya bilişsel engelli kullanıcılar için belgeyi anlamlı bir şekilde sunmak üzere ekran okuyucular ve diğer yardımcı araçlar tarafından kullanılır.

## Neden PDF etiketlenir?
PDF etiketleme (**how to tag pdf** süreci) size şunları sağlar:
- **Ekran okuyucular ve klavye kullanıcıları için geliştirilmiş gezinme**.  
- **WCAG 2.1 ve PDF/UA erişilebilirlik standartlarına uyum**.  
- **Metnin anlamsal olarak indekslenmesi sayesinde daha iyi aranabilirlik**.  

## Önkoşullar
Başlamadan önce şunların yüklü olduğundan emin olun:
- Java Development Kit (JDK).  
- IntelliJ IDEA veya Eclipse gibi bir IDE.  
- Temel Java bilgisi ve PDF kavramlarına aşinalık.  

### Gerekli Kütüphaneler ve Bağımlılıklar
Aspose.PDF for Java'yi projenize Maven veya Gradle kullanarak ekleyin.

**Maven**  
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-pdf</artifactId>
    <version>25.3</version>
</dependency>
```

**Gradle**  
```gradle
implementation 'com.aspose:aspose-pdf:25.3'
```

### Lisans Edinme
Aspose.PDF for Java ücretsiz bir deneme sunar. Geçici bir lisans alabilirsiniz: [buradan](https://purchase.aspose.com/temporary-license/). Üretim kullanımı için tam lisans satın alın.

## Aspose.PDF for Java Kurulumu
Maven/Gradle kullanmıyorsanız, JAR dosyasını [Aspose sürüm sitesinden](https://releases.aspose.com/pdf/java/) indirip projenizin derleme yoluna ekleyin.

Aşağıdaki basit kod parçacığı, boş bir PDF oluşturarak kurulumunuzu doğrular:

```java
import com.aspose.pdf.Document;

public class PdfCreator {
    public static void main(String[] args) {
        // Initialize Aspose.PDF
        Document doc = new Document();
        
        // Save the empty document to check setup
        doc.save("output/EmptyDocument.pdf");
        
        System.out.println("Setup complete and document created successfully.");
    }
}
```

## Uygulama Kılavuzu

### Etiketli İçerikli Yeni PDF Oluşturma
**Genel Bakış** – Etiketli içerik, erişilebilirliği artıran mantıksal bir hiyerarşi sağlar. Aşağıdaki adımlar, bir PDF oluşturmayı, etiketlemeyi etkinleştirmeyi ve biçimlendirilmiş bir tablo doldurmayı gösterir.

#### Adım 1: Belgeyi Başlatma ve Etiketlemeyi Etkinleştirme
İlk olarak bir `Document` örneği oluşturun ve `ITaggedContent` arayüzünü alın. Ayrıca **PDF dilini ayarlıyoruz** (**set pdf language** adımı) böylece ekran okuyucular belge yerelini bilir.

```java
import com.aspose.pdf.*;

public class TaggedPdfCreator {
    public static void main(String[] args) {
        String outputDir = "YOUR_OUTPUT_DIRECTORY";

        // Create a new PDF document
        Document document = new Document();

        // Obtain tagged content
        ITaggedContent taggedContent = document.getTaggedContent();
        
        // Set the title and language for accessibility purposes
        taggedContent.setTitle("Example table row style");
        taggedContent.setLanguage("en-US");

        // Proceed to add structured elements
    }
}
```

#### Adım 2: Yapısal Öğeler Ekleme (How to generate PDF table)
Sonra kök öğeyi tanımlayın ve bir başlık, gövde ve alt bilgi içeren tablo yapısı oluşturun. Bu, **generate pdf table** işlevselliğini gösterirken içeriğin tamamen etiketli kalmasını sağlar.

```java
import com.aspose.pdf.tagged.logicalstructure.elements.bls.*;

// Get root structure element
StructureElement rootElement = taggedContent.getRootElement();

// Create a new table structure element
TableElement tableElement = taggedContent.createTableElement();
rootElement.appendChild(tableElement);

// Add header, body, and footer to the table
TableTHeadElement tableTHeadElement = tableElement.createTHead();
TableTBodyElement tableTBodyElement = tableElement.createTBody();
TableTFootElement tableTFootElement = tableElement.createTFoot();
```

#### Adım 3: Tablo Öğelerini Doldurma (Styling rows for screen reader PDF)
Şimdi satırları ekliyor, stil veriyor ve alternatif metin sağlıyoruz. Alternatif metin, tablonun **screen reader PDF** kullanıcıları tarafından anlaşılmasını sağlar.

```java
int rowCount = 7;
int colCount = 3;

// Add a header row with column titles
TableTRElement headTrElement = tableTHeadElement.createTR();
headTrElement.setAlternativeText("Head Row");
for (int colIndex = 0; colIndex < colCount; colIndex++) {
    TableTHElement thElement = headTrElement.createTH();
    thElement.setText(String.format("Head %s", colIndex));
}

// Add rows to the table body with styled cells
for (int rowIndex = 0; rowIndex < rowCount; rowIndex++) {
    TableTRElement trElement = tableTBodyElement.createTR();
    trElement.setAlternativeText(String.format("Row %s", rowIndex));

    // Set row styles
    trElement.setBackgroundColor(Color.getLightSeaGreen());
    trElement.setBorder(new BorderInfo(BorderSide.All, 0.75F, Color.getDarkGray()));
    trElement.setDefaultCellBorder(new BorderInfo(BorderSide.All, 0.50F, Color.getBlue()));
    trElement.setMinRowHeight(100.0);
    trElement.setFixedRowHeight(120.0);

    // Set default text state for cells in this row
    TextState cellTextState = new TextState();
    cellTextState.setForegroundColor(Color.getRed());
    trElement.setDefaultCellTextState(cellTextState);

    // Add cells to the row
    for (int colIndex = 0; colIndex < colCount; colIndex++) {
        TableTDElement tdElement = trElement.createTD();
        tdElement.setText(String.format("Cell [{0}, {1}]", rowIndex, colIndex));
    }
}

// Add a footer row to the table
TableTRElement footTrElement = tableTFootElement.createTR();
footTrElement.setAlternativeText("Foot Row");
for (int colIndex = 0; colIndex < colCount; colIndex++) {
    TableTDElement tdElement = footTrElement.createTD();
    tdElement.setText(String.format("Foot %s", colIndex));
}
```

### PDF Belgesini Kaydetme
Son olarak belgeyi kaydedin. Kaydedilen dosya tüm etiketleri, dil ayarlarını ve tablo yapısını korur, böylece dağıtıma hazır **create accessible pdf** olur.

```java
// Save the tagged PDF document
document.save(outputDir + "/StyleTableRow.pdf");
System.out.println("Document saved successfully.");
```

## Pratik Uygulamalar
Erişilebilir PDF'ler birçok gerçek dünya senaryosunda kritik öneme sahiptir:

1. **Eğitim Materyalleri** – Tüm öğrenciler için kapsayıcı ders kitapları ve el kitapları sağlayın.  
2. **Kamu Yayınları** – Kamu belgeleri için yasal erişilebilirlik zorunluluklarını karşılayın.  
3. **Kurumsal Raporlar** – Paydaşların ve çalışanların finansal tabloları ekran okuyucularla erişebilmesini sağlayın.  

## Performans Düşünceleri
Büyük PDF'lerle çalışırken:

- Bellek kullanımını izleyin; kaynakları zamanında serbest bırakın.  
- Eklediğiniz dinamik öğe sayısını en aza indirin.  
- Çöp toplama ve nesne yeniden kullanımı için Java en iyi uygulamalarını izleyin.  

## Yaygın Sorunlar ve Çözümler
| Sorun | Çözüm |
|-------|----------|
| PDF okuyucuda etiketler görünmüyor | `taggedContent` alındığını ve `setTitle`/`setLanguage` öğeler eklenmeden önce çağrıldığını doğrulayın. |
| Tablo hücrelerinde alternatif metin eksik | Her `TableTRElement` ve başlık/alt bilgi satırları için `setAlternativeText` kullanın. |
| Büyük dosyalar OutOfMemoryError veriyor | Belgeyi bölümlere ayırarak işleyin veya JVM yığın boyutunu (`-Xmx`) artırın. |

## Sık Sorulan Sorular

**S: PDF'imin gerçekten erişilebilir olduğunu nasıl doğrularım?**  
C: Adobe Acrobat’ın Erişilebilirlik Denetleyicisi gibi araçları kullanın veya dosyayı bir ekran okuyucu (NVDA, JAWS) ile açarak doğru gezinmeyi kontrol edin.

**S: Aspose.PDF İngilizce dışındaki dilleri destekliyor mu?**  
C: Evet. `taggedContent.setLanguage("fr-FR")` ile Fransızca, `es-ES` ile İspanyolca vb. dil kodlarını ayarlayabilirsiniz.

**S: Etiketli bir PDF'e alt metinli resim ekleyebilir miyim?**  
C: Kesinlikle. `Image` sınıfını kullanın ve görsel içeriği tanımlamak için `AlternativeText` özelliğini ayarlayın.

**S: PDF tablosunda oluşturabileceğim satır sayısında bir limit var mı?**  
C: Katı bir limit yok, ancak çok büyük tablolar bellek tüketimini artırabilir; sayfalama veya belgeyi bölme yöntemlerini düşünün.

**S: Oluşturulan PDF tüm ekran okuyucularda çalışır mı?**  
C: Etiketler, dil ve alternatif metin doğru ayarlandığında PDF, PDF/UA standardına uygundur ve büyük çoğunlukta ekran okuyucu tarafından okunabilir.

## Sonuç
Artık **create accessible pdf** belgelerini etiketli içerikle oluşturma, biçimlendirilmiş tablolar üretme ve ekran okuyucularla uyumluluğu sağlama konusunda adım adım tam bir kılavuza sahipsiniz. Aspose.PDF for Java’yı kullanarak PDF üretim hattınıza erişilebilirliği doğrudan entegre edebilir, her kitleye kapsayıcı içerik sunabilirsiniz.

### Sonraki Adımlar
- Başlıklar, listeler ve bağlantılar gibi ek etiketleme özelliklerini keşfedin.  
- Bu iş akışını mevcut Java servislerinize veya toplu işleme görevlerinize entegre edin.  
- Deneyimlerinizi paylaşın ve sorularınızı [Aspose PDF forumunda](https://forum.aspose.com/c/pdf/10) sorun.

---

**Son Güncelleme:** 2025-12-01  
**Test Edilen Sürüm:** Aspose.PDF for Java 25.3  
**Yazar:** Aspose

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}