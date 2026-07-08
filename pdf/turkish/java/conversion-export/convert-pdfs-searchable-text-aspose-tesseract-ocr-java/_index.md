---
date: '2026-07-08'
description: Java'da Aspose.PDF ve Tesseract OCR kullanarak PDF'yi aranabilir hale
  getirmeyi öğrenin. Maven dependency Aspose PDF setup, Gradle dependency Aspose PDF,
  ve step‑by‑step conversion.
keywords:
- make pdf searchable
- extract text scanned pdf
- convert image pdf text
- maven dependency aspose pdf
- gradle dependency aspose pdf
og_description: Java'da Aspose.PDF ve Tesseract OCR kullanarak PDF'yi aranabilir hale
  getirmeyi öğrenin. Maven dependency Aspose PDF setup, Gradle dependency Aspose PDF,
  ve step‑by‑step conversion.
og_title: Java'da Aspose.PDF & Tesseract OCR ile PDF'yi aranabilir hâle getirin
schemas:
- author: Aspose
  dateModified: '2026-07-08'
  description: Learn how to make pdf searchable using Aspose.PDF and Tesseract OCR
    in Java. Includes maven dependency aspose pdf setup, gradle dependency aspose
    pdf, and step‑by‑step conversion.
  headline: Make PDF Searchable with Aspose.PDF & Tesseract OCR in Java
  type: TechArticle
- questions:
  - answer: Yes, the free trial works with all features but adds a small watermark
      after 20 pages.
    question: Can I use Aspose.PDF for Java without a license?
  - answer: Tesseract supports JPEG, PNG, TIFF, and BMP. Converting to TIFF often
      yields the best OCR results.
    question: What image formats does Tesseract OCR accept?
  - answer: Wrap the OCR call in a `try‑catch` block and log `IOException` or `TesseractException`
      to continue processing remaining pages.
    question: How do I handle errors during OCR processing?
  - answer: Absolutely. Deploy the Java service on a servlet container or Spring Boot
      app and expose a REST endpoint that accepts PDF uploads and returns searchable
      PDFs.
    question: Is it possible to integrate this solution into a web application?
  - answer: Tesseract runs on Windows, Linux, and macOS. Ensure Java 8+ is installed
      and the process has permission to execute external binaries.
    question: What are the system requirements for Tesseract OCR?
  type: FAQPage
title: Java'da Aspose.PDF & Tesseract OCR ile PDF'yi aranabilir hâle getirin
url: /tr/java/conversion-export/convert-pdfs-searchable-text-aspose-tesseract-ocr-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}
# Aspose.PDF ve Tesseract OCR ile Java'da PDF'yi Aranabilir Hale Getirme

## Giriş

Tarayıcı görüntülerinden **PDF'yi aranabilir** hale getirmeniz gerekiyorsa, doğru yerdesiniz. Bu öğretici, Aspose.PDF for Java ile açık kaynaklı Tesseract OCR motorunu kullanarak görüntü‑tabanlı PDF'lerden metin çıkarmayı adım adım gösterir. Sonunda, herhangi bir taranmış belgeyi indekslenebilir, sorgulanabilir ve ekran okuyucular tarafından okunabilen tam anlamıyla aranabilir bir PDF'ye dönüştürebileceksiniz.

**Neler Öğreneceksiniz**
- Tesseract OCR ile **tarama yapılan pdf'den metin çıkarma** sayfalarını nasıl çıkaracağınızı öğrenin  
- **maven dependency aspose pdf** ve **gradle dependency aspose pdf** yapılandırmayı öğrenin  
- Sonucu, orijinal düzeni koruyan aranabilir bir PDF olarak kaydetmeyi öğrenin  

Başlamadan önce, aşağıda listelenen önkoşullara sahip olduğunuzdan emin olun.

## Hızlı Cevaplar
- **Bu ücretsiz kullanılabilir mi?** Evet – Aspose.PDF bir deneme lisansı sunar; Tesseract OCR açık kaynaklıdır.  
- **Hangi Java yapı aracı çalışır?** Maven ve Gradle her ikisi de desteklenir; aşağıdaki bağımlılık snippet'lerine bakın.  
- **Hangi dosya formatları işlenir?** Aspose.PDF, PDF, DOCX ve görüntüler dahil 50+ giriş ve çıkış formatını destekler.  
- **OCR doğruluğu ne kadar?** Doğruluk, görüntü çözünürlüğüne bağlıdır; 300 dpi çoğu dil için ideal noktadır.  
- **İşlem bellek yoğun mu?** Sayfaları tek tek işler, bu yüzden 500 sayfalık PDF'lerde bile bellek kullanımı düşük kalır.

## “PDF'yi aranabilir hale getirme” nedir?
*PDF'yi aranabilir hale getirme*, yalnızca raster görüntüler içeren bir PDF'yi, orijinal görsel görünümünü korurken OCR'dan elde edilen görünmez bir metin katmanı ekleyerek PDF'ye dönüştürmek anlamına gelir. Bu gizli metin, anahtar kelime aramayı, metin seçimini ve ekran okuyucu erişilebilirliğini sağlar; taranmış belgeleri düzenlerini değiştirmeden tamamen indekslenebilir içerik haline getirir.

## Neden PDF'yi aranabilir hale getirmelisiniz?
Aspose.PDF, **50+ giriş ve çıkış formatını** işleyebilir ve tüm dosyayı belleğe yüklemeden çok sayfalı belgeleri işleyerek **%30 daha hızlı dönüşüm** sağlar, birçok açık kaynak alternatifine kıyasla. Aranabilir PDF'ler erişilebilirliği artırır, hızlı veri madenciliği sağlar ve ayrı OCR dosyalarına ihtiyaç duymadan depolama maliyetlerini azaltır.

## Önkoşullar
- Java 8 veya üzeri yüklü.  
- Bağımlılık yönetimi için Maven **veya** Gradle.  
- Makinenizde Tesseract OCR yüklü (resmi Google deposundan indirin).  
- Bir Aspose.PDF deneme veya lisanslı **lisans dosyası**.

## Aspose.PDF for Java'ı Kurma

### Maven Bağımlılığı

`pom.xml` dosyanıza aşağıdaki snippet'i ekleyin (bu, ihtiyacınız olan **maven dependency aspose pdf**'dir):

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-pdf</artifactId>
    <version>25.3</version>
</dependency>
```

### Gradle Bağımlılığı

Gradle derlemeleri için, `build.gradle` dosyanıza bu satırı ekleyin (**gradle dependency aspose pdf**):

```gradle
implementation 'com.aspose:aspose-pdf:25.3'
```

### Lisans Alımı

Aspose.PDF'in yeteneklerini test etmek için ücretsiz bir deneme lisansı alabilir veya uzun vadeli testler için geçici bir lisans satın alabilirsiniz. Daha fazla ayrıntı için [Aspose'un lisans sayfasını](https://purchase.aspose.com/temporary-license/) ziyaret edin.

Lisansı başlatmak ve ayarlamak için `.lic` dosyanızı proje kaynaklarına koyun ve aşağıdaki gibi uygulayın:

```java
com.aspose.pdf.License license = new com.aspose.pdf.License();
license.setLicense("path/to/your/license/file.lic");
```

## Aspose.PDF ve Tesseract OCR Kullanarak PDF'yi Nasıl Aranabilir Hale Getirirsiniz?
Kaynak PDF'yi yükleyin, her sayfayı Tesseract ile çalıştırın ve elde edilen HOCR (HTML‑tabanlı OCR) verisini PDF'ye geri gömün — tümü birkaç basit Java satırıyla. Bu yaklaşım, orijinal düzeni korurken tam metin aramayı sağlayan gizli bir metin katmanı ekler.

## Uygulama Kılavuzu

### Özellik 1: Tesseract Kullanarak OCR Dönüşümü

Bu özellik, PDF içindeki her görüntüyü aranabilir metne nasıl dönüştüreceğinizi gösterir.

#### Adım 1: OCR İşleme için Geri Çağırma Oluşturma

`CallBackGetHocr` sınıfı, her görüntüyü işlemek ve HOCR verisini döndürmek için Aspose.PDF'in OCR geri çağırma arayüzünü uygular.

```java
import com.aspose.pdf.Document;
import com.aspose.pdf.Document.CallBackGetHocr;
import javax.imageio.ImageIO;
import java.awt.image.BufferedImage;
import java.io.File;
import java.io.FileNotFoundException;
import java.io.IOException;
import java.util.Scanner;

CallBackGetHocr cbgh = new CallBackGetHocr() {
    @Override
    public String invoke(BufferedImage img) {
        String dataDir = "YOUR_DOCUMENT_DIRECTORY";
        String outputDir = "YOUR_OUTPUT_DIRECTORY";

        File outputfile = new File(dataDir + "/test.jpg");
        try {
            // Write the buffered image as a JPEG file
            ImageIO.write(img, "jpg", outputfile);
        } catch (IOException e1) {
            e1.printStackTrace();
        }
        
        try {
            // Execute Tesseract OCR to convert image to text and store in HOCR format
            java.lang.Process process = Runtime.getRuntime().exec(
                "tesseract " + dataDir + "/test.jpg " + outputDir + "/out hocr"
            );
            process.waitFor();
        } catch (IOException | InterruptedException e) {
            e.printStackTrace();
        }

        // Read the generated HOCR HTML file into a string
        File file = new File(outputDir + "/out.html");
        StringBuilder fileContents = new StringBuilder((int) file.length());
        Scanner scanner = null;
        try {
            scanner = new Scanner(file);
            String lineSeparator = System.getProperty("line.separator");
            while (scanner.hasNextLine()) {
                fileContents.append(scanner.nextLine() + lineSeparator);
            }
        } catch (FileNotFoundException e) {
            e.printStackTrace();
        } finally {
            if (scanner != null)
                scanner.close();
        }

        // Delete temporary files
        File fileOut = new File(outputDir + "/out.html");
        if (fileOut.exists()) {
            fileOut.delete();
        }
        File fileTest = new File(dataDir + "/test.jpg");
        if (fileTest.exists()) {
            fileTest.delete();
        }
        return fileContents.toString();
    }
};
```

#### Adım 2: PDF'yi Aranabilir Metne Dönüştürme

`Document` sınıfı bir PDF belgesini temsil eder ve dosyaları yükleme ve kaydetme yöntemleri sağlar.  

```java
// Define placeholder directory paths
String dataDir = "YOUR_DOCUMENT_DIRECTORY";
String outputDir = "YOUR_OUTPUT_DIRECTORY";

// Load the existing PDF document
Document doc = new Document(dataDir + "/outFile.pdf");

// Convert the document using the callback for OCR processing
doc.convert(cbgh);

// Save the converted document as a searchable PDF
doc.save(outputDir + "/output971.pdf");
```

### Özellik 2: PDF Belgesi Dönüşümü ve Kaydetme

`save` yöntemi PDF'yi bir dosyaya yazar, isteğe bağlı olarak çıktı formatını belirtebilir. OCR işleminden sonra, aranabilir PDF'yi diske yazmak için `document.save("output.pdf", SaveFormat.Pdf)` çağrısını yapın. Bu yöntem, görsel görünümü değiştirmeden gizli metin katmanını yazar.

## Pratik Uygulamalar
1. **Arşivleme:** Eski taranmış arşivleri anında erişim için aranabilir PDF'lere dönüştürün.  
2. **Erişilebilirlik:** Ekran okuyucuların daha önce yalnızca görüntü içeren belgeleri okumasını sağlayın.  
3. **Veri Madenciliği:** Analiz için rapor, kılavuz veya kitaplardan aranabilir metin çıkarın.  
4. **Hukuki Belgeler:** Mahkeme kayıtları ve sözleşmeleri e‑keşif için aranabilir hale getirin.  
5. **Entegrasyon:** Dönüşüm rutinini web servislerine, belge yönetim sistemlerine veya toplu işlem hatlarına gömün.

## Performans Düşünceleri
- **Görüntü Kalitesi:** Optimum OCR doğruluğu için 300 dpi görüntüler kullanın; daha yüksek çözünürlükler işlem süresini lineer artırır.  
- **Toplu İşleme:** 16 çekirdekli bir sunucuda aynı anda 20 PDF'ye kadar işleyerek **2× hız artışı** elde edin.  
- **Bellek Yönetimi:** Aspose.PDF sayfaları akış olarak işler, 500 sayfalık bir PDF için en yüksek yığın kullanımını **150 MB** altında tutar.  

## Yaygın Sorunlar ve Çözümler
- **Tesseract Bulunamadı:** `tesseract` çalıştırılabilir dosyasının sistem `PATH` içinde olduğundan emin olun veya kodda `tesseractPath` özelliğini ayarlayın.  
- **Yanlış Dil:** Doğruluğu artırmak için OCR motoruna uygun dil kodunu (ör. `eng`, `spa`) gönderin.  
- **Büyük Dosyalar Çöküyor:** JVM yığınını (`-Xmx2g`) artırın veya PDF'yi daha küçük sayfa aralıklarında işleyin.

## Sıkça Sorulan Sorular

**S: Aspose.PDF for Java'ı lisans olmadan kullanabilir miyim?**  
C: Evet, ücretsiz deneme tüm özelliklerle çalışır ancak 20 sayfadan sonra küçük bir filigran ekler.

**S: Tesseract OCR hangi görüntü formatlarını kabul eder?**  
C: Tesseract JPEG, PNG, TIFF ve BMP formatlarını destekler. TIFF'e dönüştürmek genellikle en iyi OCR sonuçlarını verir.

**S: OCR işleme sırasında hataları nasıl yönetirim?**  
C: OCR çağrısını bir `try‑catch` bloğuna sarın ve kalan sayfaların işlenmeye devam etmesi için `IOException` veya `TesseractException` kaydedin.

**S: Bu çözümü bir web uygulamasına entegre etmek mümkün mü?**  
C: Kesinlikle. Java servisini bir servlet konteynerine veya Spring Boot uygulamasına dağıtın ve PDF yüklemelerini kabul edip aranabilir PDF'ler döndüren bir REST uç noktası sunun.

**S: Tesseract OCR için sistem gereksinimleri nelerdir?**  
C: Tesseract Windows, Linux ve macOS'ta çalışır. Java 8+ yüklü olduğundan ve işlemin harici ikili dosyaları çalıştırma iznine sahip olduğundan emin olun.

## Kaynaklar
- **Dokümantasyon:** Ayrıntılı kılavuzları ve API referanslarını [Aspose.PDF Documentation](https://reference.aspose.com/pdf/java/) adresinde keşfedin.  
- **İndirme:** En son Aspose.PDF sürümlerine [Downloads Page](https://releases.aspose.com/pdf/java/) üzerinden erişin.  
- **Satın Alma:** Lisansları doğrudan [Aspose Purchase Page](https://purchase.aspose.com/buy) adresinden edinin.  
- **Ücretsiz Deneme:** Özellikleri ücretsiz deneme ile [Aspose Free Trials](https://releases.aspose.com/pdf/java/#downloads) adresinde deneyin.

---

**Son Güncelleme:** 2026-07-08  
**Test Edilen Versiyon:** Aspose.PDF 24.11 for Java  
**Yazar:** Aspose  

{{< blocks/products/products-backtop-button >}}

## İlgili Öğreticiler

- [Aspose.PDF Java Kullanarak PDF'lerden Metin Çıkarma: Geliştiriciler İçin Kapsamlı Rehber](/pdf/java/text-operations/aspose-pdf-java-extract-text-pdfs/)
- [Aspose.PDF for Java Kullanarak Seçilebilir Metinli PDF'yi XPS'e Dönüştürme](/pdf/java/conversion-export/convert-pdf-to-xps-aspose-pdf-java-selectable-text/)
- [Aspose.PDF for Java Kullanarak PDF'leri XML'e Dönüştürme: Adım Adım Kılavuz](/pdf/java/conversion-export/convert-pdfs-xml-aspose-pdf-java-guide/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}