---
date: '2026-07-03'
description: Aspose PDF Maven bağımlılığını nasıl ekleyeceğinizi ve Aspose.PDF for
  Java kullanarak seçilebilir metinle PDF'yi XPS'ye nasıl dönüştüreceğinizi öğrenin.
  Önkoşullar ve SSS'lerle adım adım rehber.
keywords:
- aspose pdf maven dependency
- how to convert pdf to xps
- java convert pdf xps
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Learn how to add the Aspose PDF Maven dependency and convert PDF to
    XPS with selectable text using Aspose.PDF for Java. Step‑by‑step guide with prerequisites
    and FAQs.
  headline: Aspose PDF Maven Dependency – Convert PDF to XPS (Java)
  type: TechArticle
- description: Learn how to add the Aspose PDF Maven dependency and convert PDF to
    XPS with selectable text using Aspose.PDF for Java. Step‑by‑step guide with prerequisites
    and FAQs.
  name: Aspose PDF Maven Dependency – Convert PDF to XPS (Java)
  steps:
  - name: Load the PDF Document
    text: 'First, load your PDF document from its directory:'
  - name: Configure Save Options
    text: 'Create an instance of `XpsSaveOptions` to set up the XPS conversion options:'
  - name: Save as XPS File
    text: 'Finally, save the document in XPS format to your desired output directory:'
  type: HowTo
- questions:
  - answer: Yes—pass the password to the `Document` constructor or use `Document.open(String
      path, String password)` before conversion.
    question: Can I convert password‑protected PDFs?
  - answer: Absolutely. All vector shapes, images, and text are preserved, and the
      text remains selectable.
    question: Does the XPS retain vector graphics?
  - answer: The trial works without a license but adds a watermark to the output;
      a permanent license removes all restrictions.
    question: Is a license mandatory for the trial version?
  - answer: It processes files in a streaming manner, allowing conversion of PDFs
      with hundreds of pages without loading the entire document into memory.
    question: How does Aspose.PDF handle large files?
  - answer: The library runs on any OS with a compatible JDK, including Windows, Linux,
      and macOS.
    question: Which platforms are supported?
  type: FAQPage
title: Aspose PDF Maven Bağımlılığı – PDF'yi XPS'ye Dönüştür (Java)
url: /tr/java/conversion-export/convert-pdf-to-xps-aspose-pdf-java-selectable-text/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}
# Aspose PDF Maven Bağımlılığı – PDF'yi XPS'ye Dönüştür (Java)

## Giriş

If you need to **add the Aspose PDF Maven dependency** and then convert PDF documents to XPS while keeping the text selectable, you’re in the right place. This tutorial walks you through every step—from configuring Maven or Gradle, to loading a PDF, configuring XPS options, and finally saving a selectable‑text XPS file. By the end you’ll have a reusable snippet you can drop into any Java project.

## Hızlı Yanıtlar
- **Hangi bağımlılık gerekiyor?** `com.aspose:aspose-pdf` (Maven) or the equivalent Gradle artifact.  
- **XPS seçilebilir metni koruyabilir mi?** Yes—Aspose.PDF preserves text layers automatically.  
- **Hangi Java sürümü gerekiyor?** JDK 8 or newer.  
- **Üretim için lisansa ihtiyacım var mı?** A valid Aspose.PDF license is required for unlimited use.  
- **Dönüşüm ne kadar sürer?** Typically under a second for files under 100 pages on standard hardware.

## Aspose PDF Maven Bağımlılığı Nedir?
The `aspose-pdf` Maven artifact provides the full Aspose.PDF for Java API, enabling PDF creation, manipulation, and conversion without external software. Adding this dependency to your `pom.xml` or `build.gradle` pulls in all required binaries, so you can start coding immediately without manual JAR management.

## PDF'yi seçilebilir metinle XPS'ye neden dönüştürmeliyiz?
Aspose.PDF supports **50+ input and output formats** and can generate XPS files that retain a searchable, selectable text layer. This is crucial for workflows that require archival‑grade documents, exact layout fidelity, or downstream editing in XPS‑aware tools. Conversions complete in under a second for typical 20‑page PDFs on a modern CPU.

## Önkoşullar

- **Java Development Kit (JDK) 8+** yüklü ve `JAVA_HOME` yapılandırılmış.  
- **Maven 3.6+** or **Gradle 6+** for dependency management.  
- Basic familiarity with Java file I/O and exception handling.  

### Gerekli Kütüphaneler ve Bağımlılıklar

You’ll need the Aspose.PDF for Java library version 25.3 or later. Include it using one of the following build tools:

**Maven:**  
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-pdf</artifactId>
    <version>25.3</version>
</dependency>
```  

**Gradle:**  
```gradle
implementation 'com.aspose:aspose-pdf:25.3'
```  

### Ortam Kurulumu

Make sure your IDE or build environment points to the correct JDK and that the network can reach Maven Central or your private repository.

## Aspose PDF Maven Bağımlılığı Nasıl Eklenir?

`aspose-pdf` is the artifact you add to your project’s build file, then refresh the dependencies so the JARs are downloaded automatically. For Maven, insert the `<dependency>` block inside `<dependencies>`; for Gradle, place the `implementation` line inside the `dependencies` block. After the refresh, the Aspose classes become available on the classpath, and you can start coding without manual JAR handling.

## Aspose.PDF for Java Kurulumu

### Kurulum Adımları

1. **Maven/Gradle Setup:** Add the dependency as shown above and run `mvn clean install` or `gradle build` to pull the library.  
2. **License Acquisition:**  
   - Download a [free trial](https://releases.aspose.com/pdf/java/) or obtain a [temporary license](https://purchase.aspose.com/temporary-license/).  
   - Place the license file (`Aspose.Pdf.lic`) in a folder accessible to your application and load it at startup.

### Basic Initialization

`License` applies an Aspose license file to unlock full functionality.  
Load the license (if you have one) and create a `Document` object to work with PDFs.  
`Document` represents a PDF file and provides methods to manipulate its contents.

```java
import com.aspose.pdf.Document;
import com.aspose.pdf.License;

// Initialize a License object
License license = new License();

// Set the license file path
license.setLicense("path/to/Aspose.Total.Java.lic");
```  

## PDF'yi seçilebilir metinle XPS'ye Nasıl Dönüştürülür?

`XpsSaveOptions` configures the settings for saving a PDF as an XPS document, including text preservation.  
Load the source PDF, configure `XpsSaveOptions` to preserve text, and invoke `save` with the `.xps` extension. The API automatically embeds a text layer, so the resulting XPS can be searched and copied just like the original PDF. This whole process typically requires only three lines of code after the library is set up.

## Uygulama Kılavuzu

### PDF'yi XPS'ye Dönüştür

This feature enables you to convert a PDF document into an XPS file using Aspose.PDF for Java.

#### Step 1: Load the PDF Document

First, load your PDF document from its directory:

```java
import com.aspose.pdf.Document;

String dataDir = "YOUR_DOCUMENT_DIRECTORY";
Document pdfDocument = new Document(dataDir + "/input.pdf");
```  

#### Step 2: Configure Save Options

Create an instance of `XpsSaveOptions` to set up the XPS conversion options:

```java
import com.aspose.pdf.XpsSaveOptions;

XpsSaveOptions saveOptions = new XpsSaveOptions();
```  

#### Step 3: Save as XPS File

Finally, save the document in XPS format to your desired output directory:

```java
String outputDir = "YOUR_OUTPUT_DIRECTORY";
pdfDocument.save(outputDir + "/ConvertPDFtoXPS_out.xps\
```  

## Yaygın Sorunlar ve Çözümler

- **Blank pages in the XPS output:** Ensure the PDF does not use encrypted streams; if it does, provide the password when loading the `Document`.  
- **Memory errors on large PDFs:** Use `Document.optimizeResources()` before saving to reduce memory footprint.  
- **Missing fonts:** Install the required fonts on the server or embed them in the PDF before conversion.

## Sıkça Sorulan Sorular

**Q: Can I convert password‑protected PDFs?**  
A: Yes—pass the password to the `Document` constructor or use `Document.open(String path, String password)` before conversion.

**Q: Does the XPS retain vector graphics?**  
A: Absolutely. All vector shapes, images, and text are preserved, and the text remains selectable.

**Q: Is a license mandatory for the trial version?**  
A: The trial works without a license but adds a watermark to the output; a permanent license removes all restrictions.

**Q: How does Aspose.PDF handle large files?**  
A: It processes files in a streaming manner, allowing conversion of PDFs with hundreds of pages without loading the entire document into memory.

**Q: Which platforms are supported?**  
A: The library runs on any OS with a compatible JDK, including Windows, Linux, and macOS.

---

**Last Updated:** 2026-07-03  
**Tested With:** Aspose.PDF for Java 25.3  
**Author:** Aspose  

{{< blocks/products/products-backtop-button >}}

## İlgili Eğitimler

- [Aspose.PDF for Java kullanarak PDF'yi JPEG'e Dönüştür: Adım Adım Kılavuz](/pdf/java/conversion-export/convert-pdf-to-jpeg-aspose-java-tutorial/)
- [Aspose.PDF for Java kullanarak PDF'yi Excel'e Dönüştürme | Adım Adım Kılavuz](/pdf/java/conversion-export/convert-pdf-excel-aspose-java-tutorial/)
- [Aspose.PDF in Java kullanarak XPS Dosyalarını PDF'e Dönüştürme: Tam Kılavuz](/pdf/java/conversion-export/convert-xps-pdf-aspose-java-guide/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}