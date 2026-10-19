---
category: general
date: 2026-10-13
description: Aspose.PDF kullanarak .NET’te PDF/X‑1 belgesi oluşturma – ICC profilleriyle
  PDF’yi PDF/X‑1’e dönüştürmeyi de gösteren adım adım bir rehber.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create pdfx-1 document
- convert pdf to pdfx-1
- how to convert pdfx-1
language: tr
lastmod: 2026-10-13
og_description: Aspose.PDF for .NET ile PDF/X‑1 belgesi oluşturun. PDF'yi PDF/X‑1'e
  nasıl dönüştüreceğinizi, ICC profillerini nasıl ayarlayacağınızı öğrenin ve sonucu
  dakikalar içinde kaydedin.
og_image_alt: Screenshot of code that creates a PDF/X‑1 document using Aspose.PDF
og_title: PDF/X‑1 belgesini .NET’te oluşturun – kapsamlı Aspose.PDF rehberi
schemas:
- author: Aspose
  dateModified: '2026-10-13'
  description: Create PDF/X‑1 document in .NET using Aspose.PDF – a step‑by‑step guide
    that also shows how to convert PDF to PDF/X‑1 with ICC profiles.
  headline: How to create PDF/X‑1 document with Aspose.PDF for .NET
  type: TechArticle
- description: Create PDF/X‑1 document in .NET using Aspose.PDF – a step‑by‑step guide
    that also shows how to convert PDF to PDF/X‑1 with ICC profiles.
  name: How to create PDF/X‑1 document with Aspose.PDF for .NET
  steps:
  - name: Open the file in Adobe Acrobat Pro and check **File → Properties → Standards**.
      It should list **PDF/X‑1a:2001** (or PDF/X‑1a:2003) as the compliance level.
    text: Open the file in Adobe Acrobat Pro and check **File → Properties → Standards**.
      It should list **PDF/X‑1a:2001** (or PDF/X‑1a:2003) as the compliance level.
  - name: Use a free validator such as **VeraPDF** to run an automated compliance
      test. The tool will report any missing OutputIntent or disallowed features.
    text: Use a free validator such as **VeraPDF** to run an automated compliance
      test. The tool will report any missing OutputIntent or disallowed features.
  - name: If validation fails, double‑check that the ICC profile path is correct and
      that the source PDF does not contain prohibited elements (e.g., embedded multimedia).
    text: If validation fails, double‑check that the ICC profile path is correct and
      that the source PDF does not contain prohibited elements (e.g., embedded multimedia).
  type: HowTo
tags:
- Aspose.PDF
- .NET
- PDF/X‑1
title: Aspose.PDF for .NET ile PDF/X‑1 belgesi nasıl oluşturulur
url: /tr/net/document-creation/how-to-create-pdf-x-1-document-with-aspose-pdf-for-net/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.PDF for .NET ile PDF/X‑1 belgesi nasıl oluşturulur

Programlı olarak **PDF/X‑1 belgesi oluşturmanız** gerekiyorsa, bu kılavuz tam olarak nasıl yapılacağını gösterir. Aşağıdaki adımları izleyerek **PDF'yi PDF/X‑1'e dönüştürebilir** ve ICC profilini kontrol edebilirsiniz; tüm bunlar sadece birkaç C# satırıyla yapılır. Ayrıca her adımın neden önemli olduğunu, yaygın sorunların nasıl ele alınacağını ve son dosyanın nasıl göründüğünü öğreneceksiniz. Aspose.PDF for .NET kütüphanesi dışındaki herhangi bir harici araca ihtiyaç yoktur.

## Neler Başaracaksınız

- Mevcut bir PDF dosyasını yükleyin.  
- PDF/X‑1 uyumluluğu için gerekli ICC profilini (FOGRA39) tanımlayın.  
- Profili OutputIntent olarak gömen dönüşüm seçeneklerini oluşturun.  
- Kaynak PDF'yi **PDF/X‑1** belgesine dönüştürün.  
- Sonucu diske kaydedin.

> **Önkoşul** – **Aspose.PDF for .NET**'in lisanslı bir kopyasına (sürüm 23.4 veya sonrası) ve Visual Studio 2022 gibi bir .NET geliştirme ortamına sahip olmalısınız.

## Adım 1: Kaynak PDF belgesini yükleyin

İlk işlem, dönüştürmek istediğiniz PDF'yi açmaktır. Aspose.PDF, tüm dosyayı bellekte temsil eden bir `Document` nesnesi kullanır.

```csharp
// Step 1: Load the source PDF document
string dataDir = "YOUR_DIRECTORY/";                     // folder that contains input.pdf and the ICC profile
using (var doc = new Aspose.Pdf.Document(dataDir + "input.pdf"))
{
    // The Document object is now ready for conversion.
```

**Neden Önemlidir:** Dosyayı bir `using` bloğu içinde açmak, dönüşüm tamamlandığında tüm yönetilmeyen kaynakların serbest bırakılmasını garanti eder ve dosya tutamağı sızıntılarını önler.

## Adım 2: PDF/X‑1 için dönüşüm seçeneklerini oluşturun

Aspose.PDF, hedef formatı ve ek uyumluluk verilerini belirtmek için bir `PdfFormatConversionOptions` örneği gerektirir.

```csharp
    // Step 2: Create conversion options for PDF/X‑1
    var conversionOptions = new Aspose.Pdf.PdfFormatConversionOptions();
```

**Neden Önemlidir:** Seçenekler nesnesi, kütüphaneye sadece basit bir PDF kopyası istemediğinizi, **PDF/X‑1** uyumlu bir çıktı gerektiğini ve bunun sıkı renk yönetimi kuralları getirdiğini bildirir.

## Adım 3: Harici ICC profilini (FOGRA39) ekleyin

PDF/X‑1, renk uzayını tanımlayan gömülü bir ICC profili zorunluluğu getirir. Burada dönüşüm seçeneklerini yerel bir `.icc` dosyasına yönlendiriyoruz.

```csharp
    // Step 3: Specify the external ICC profile (FOGRA39)
    conversionOptions.IccProfileFileName = dataDir + "FOGRA39.icc";
```

**Neden Önemlidir:** Geçerli bir ICC profili olmadan, ortaya çıkan dosya PDF/X‑1 doğrulama araçlarında başarısız olur. FOGRA39, Avrupa baskı standartları için yaygın bir CMYK profilidir.

## Adım 4: Bir OutputIntent oluşturun ve seçeneklere ekleyin

Bir `OutputIntent`, ICC profilini sarar ve PDF'nin meta verilerinin bir parçası haline getirir.

```csharp
    // Step 4: Create an OutputIntent using the ICC profile and add it to the options
    var outputIntent = new Aspose.Pdf.OutputIntent(conversionOptions.IccProfileFileName);
    conversionOptions.OutputIntents.Add(outputIntent);
```

**Neden Önemlidir:** PDF/X‑1 en az bir OutputIntent gerektirir. Bunu açıkça eklemek, dönüşüm motorunun profili doğru şekilde gömmesini sağlar ve doğrulama hatalarını önler.

## Adım 5: Belgeyi PDF/X‑1 formatına dönüştürün

Şimdi gerçek dönüşümü tetikliyoruz. `Convert` yöntemi, seçenek nesnesini ve hedef enum değerini alır.

```csharp
    // Step 5: Convert the document to PDF/X‑1 format
    doc.Convert(conversionOptions, Aspose.Pdf.PdfFormat.PdfX_1);
```

**Neden Önemlidir:** `PdfX_1` enumu, Aspose'a tüm PDF/X‑1 kısıtlamalarını (ör. şeffaf nesneler yok, gömülü yazı tipleri, doğru renk uzayları) uygulamasını söyler. PDF/X‑4 ihtiyacınız varsa, bunun yerine `PdfX_4` kullanmalısınız.

## Adım 6: Dönüştürülen PDF/X‑1 dosyasını kaydedin

Son olarak, uyumlu dosyayı diske geri yazın.

```csharp
    // Step 6: Save the converted PDF/X‑1 file
    doc.Save(dataDir + "output_pdfx1.pdf");
}
```

**Neden Önemlidir:** Aynı `using` bloğu içinde kaydetmek, dosya tutamacı serbest bırakılmadan önce belgenin tamamen yazıldığını garanti eder. Çıktı dosyası artık herhangi bir PDF/X doğrulayıcı ile kontrol edilebilir.

---

![PDF/X‑1 belgesinin oluşturulmasını gösteren diyagram](/images/create-pdfx1-workflow.png){.align-center width=600 alt="Aspose.PDF ile PDF/X‑1 belgesinin nasıl oluşturulacağını gösteren diyagram"}

## PDF/X‑1 belgesinin geçerli olduğunu nasıl doğrularsınız

1. Dosyayı Adobe Acrobat Pro'da açın ve **File → Properties → Standards** bölümünü kontrol edin. Uyumluluk seviyesi olarak **PDF/X‑1a:2001** (veya PDF/X‑1a:2003) listelenmelidir.  
2. **VeraPDF** gibi ücretsiz bir doğrulayıcı kullanarak otomatik bir uyumluluk testi çalıştırın. Araç, eksik OutputIntent veya izin verilmeyen özellikleri raporlayacaktır.  
3. Doğrulama başarısız olursa, ICC profil yolunun doğru olduğundan ve kaynak PDF'nin yasaklanmış öğeler (ör. gömülü multimedya) içermediğinden emin olun.

## Yaygın kenar durumları ve nasıl ele alınır

| Durum | Çözüm |
|-----------|----------|
| **Kaynak PDF şeffaf nesneler içeriyor** | Şeffaf nesneler PDF/X‑1'de izin verilmez. Dönüşümden önce, sayfaları rasterleştirerek veya `doc.FlattenPages();` ile şeffaflığı kaldırarak PDF'yi düzleştirin. |
| **Yazı tipi gömme eksik** | Dönüşümden önce `doc.FontEmbeddingMode = Aspose.Pdf.FontEmbeddingMode.Always;` ayarlandığından emin olun. |
| **Büyük ICC profil dosyası** | Son PDF boyutunun makul kalması için sıkıştırılmış bir profil (ör. `.icc` < 1 MB) kullanın. |
| **Dönüşüm `ArgumentException` hatası veriyor** | ICC dosya yolunun mutlak olduğundan ve dosyanın çalışan süreç tarafından erişilebilir olduğundan emin olun. |

## Pro ipucu: Toplu işleme için dönüşüm seçeneklerini yeniden kullanma

Birçok PDF'yi PDF/X‑1'e dönüştürmeniz gerekiyorsa, `PdfFormatConversionOptions` nesnesini bir kez oluşturun, ICC profilini yapılandırın ve bir döngü içinde yeniden kullanın. Bu, nesne oluşturma yükünü azaltır ve tüm dosyalarda tutarlı renk yönetimini garanti eder.

```csharp
var options = new Aspose.Pdf.PdfFormatConversionOptions
{
    IccProfileFileName = dataDir + "FOGRA39.icc"
};
options.OutputIntents.Add(new Aspose.Pdf.OutputIntent(options.IccProfileFileName));

foreach (string file in Directory.GetFiles(dataDir, "*.pdf"))
{
    using (var doc = new Aspose.Pdf.Document(file))
    {
        doc.Convert(options, Aspose.Pdf.PdfFormat.PdfX_1);
        string outPath = Path.Combine(dataDir, Path.GetFileNameWithoutExtension(file) + "_pdfx1.pdf");
        doc.Save(outPath);
    }
}
```

## Sonuç

Artık Aspose.PDF for .NET ile programlı olarak **PDF/X‑1 belgesi oluşturmayı** biliyorsunuz ve ICC profil yönetimi, OutputIntent oluşturma ve doğrulama ipuçları dahil olmak üzere tam **PDF'yi PDF/X‑1'e dönüştürme** iş akışını da anlıyorsunuz. Bu adımları, herhangi bir .NET uygulamasında baskıya hazır PDF üretimini otomatikleştirmek için uygulayın.

**Sonraki adımlar**

- **`PdfFormatConversionOptions`** özelliklerini keşfederek PDF/X‑4 veya PDF/A dönüşümlerini ince ayar yapın.  
- Bu iş akışını **Aspose.PDF’nin görüntü çıkarma** özelliğiyle birleştirerek dönüşümden önce yüksek çözünürlüklü grafikler ekleyin.  
- ICC profil seçimi hakkında daha derin bilgiler için resmi Aspose.PDF belgelerinde **renk yönetimi** konusunu okuyun.

Kodlamaktan keyif alın ve PDF'lerinizin artık katı PDF/X‑1 standardına uyduğundan emin olmanın rahatlığını yaşayın!

## Sonraki Öğrenmeniz Gerekenler

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olmak için adım adım açıklamalar içeren tam çalışan kod örnekleri sunar.

- [Aspose.PDF for .NET Kullanarak PDF'leri PDF/X-4'e Dönüştürme: Adım Adım Kılavuz](/pdf/english/net/pdfa-compliance/convert-pdfs-to-pdf-x4-aspose-dotnet-guide/)
- [Aspose.PDF for .NET Kullanarak PDF'yi XML'e Dönüştürme: Adım Adım Kılavuz](/pdf/english/net/conversion-export/pdf-to-xml-conversion-aspose-pdf-net/)
- [Aspose.PDF for .NET Kullanarak PDF Sayfalarını Görsellere Dönüştürme (Adım Adım Kılavuz)]( /pdf/english/net/conversion-export/convert-pdf-pages-to-images-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}