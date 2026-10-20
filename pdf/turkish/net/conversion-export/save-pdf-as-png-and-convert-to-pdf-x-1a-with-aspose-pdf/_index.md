---
category: general
date: 2026-02-09
description: Aspose PDF kullanarak C#'de PDF'yi PNG olarak kaydedin, ardından PDF'yi
  HTML'ye dışa aktarın, PDF'ye filigran damgası ekleyin ve ASP.NET PDF dönüşümü için
  PDFX‑1a nasıl dönüştürüleceğini öğrenin.
draft: false
keywords:
- save pdf as png
- export pdf to html
- add watermark stamp pdf
- how to convert pdfx-1a
- asp.net pdf conversion
language: tr
og_description: C#'ta Aspose PDF ile PDF'yi PNG olarak kaydedin, ardından PDF'yi HTML'ye
  dışa aktarın, PDF'ye filigran damgası ekleyin ve ASP.NET PDF dönüşümü için PDFX‑1a
  nasıl dönüştürüleceğini keşfedin.
og_title: PDF'yi PNG olarak kaydedin ve Aspose PDF ile PDF/X‑1a'ya dönüştürün
tags:
- aspnet
- pdf
- csharp
title: PDF'yi PNG olarak kaydedin ve Aspose PDF ile PDF/X‑1a'ya dönüştürün
url: /tr/net/conversion-export/save-pdf-as-png-and-convert-to-pdf-x-1a-with-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Save PDF as PNG and Convert to PDF/X‑1a with Aspose PDF

PDF'yi **PNG olarak kaydetmek** istediğinizde saçlarınızın çekilmesinden bıktınız mı? Tek başınıza değilsiniz—geliştiriciler sürekli olarak sayfayı rasterleştirip orijinal PDF'i korumanın hızlı bir yolunu soruyor. Bu rehberde tam olarak bunu yapacağız, ayrıca **PDF'yi HTML'e dışa aktarma**, **watermark stamp PDF** ekleme ve **PDFX‑1a** dönüştürme işlemlerini **ASP.NET PDF conversion** hattı içinde nasıl gerçekleştireceğinizi göstereceğiz.

Bu öğreticiden elde edeceğiniz şey, bir PDF dosyasını yükleyen, PDF/X‑1a uyumlu bir dosyaya dönüştüren, ilk sayfayı PNG olarak render eden, dinamik bir metin damgası ekleyen ve sonunda font kodlamasını koruyan bir HTML sürümü üreten, kopyala‑yapıştır hazır bir C# programıdır. Belirsiz referanslar yok, sadece somut kod ve her satırın “neden”i.

## Prerequisites

- .NET 6.0 veya üzeri (kod .NET Framework 4.7+ üzerinde de çalışır)
- Aspose.Pdf for .NET NuGet paketi (`Install-Package Aspose.Pdf`)
- PDF/X‑1a uyumluluğu için bir ICC profil dosyası (`profile.icc`)
- Dönüştürmek istediğiniz kaynak PDF (`input.pdf`)

Hepsi bu—başka bir kütüphane, gizli adım yok. Bu öğelere sahipseniz hazırsınız.

## Step 1: Load the Source PDF Document

Herhangi bir işlem yapmadan önce PDF'i belleğe almamız gerekiyor.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Devices;

// Load the PDF you’ll be working with
Document pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");
```

**Neden önemli:** `Document` temel nesnedir; sayfalara, fontlara ve meta verilere erişim sağlar. Tek sefer yüklemek, sonraki aşamaların hızlı çalışmasını sağlar.

## Step 2: Convert to PDF/X‑1a (How to Convert PDFX‑1a)

PDF/X‑1a, baskıya hazır dosyalar için tercih edilen standarttır. Dönüştürmek, tüm fontların gömülmesini ve renklerin tanımlanmasını garanti eder.

```csharp
// Set up conversion options for PDF/X‑1a
PdfFormatConversionOptions conversionOptions = new PdfFormatConversionOptions(
    PdfFormat.PDF_X_1A,               // Target format
    ConvertErrorAction.Delete)       // What to do on errors
{
    IccProfileFileName = "YOUR_DIRECTORY/profile.icc", // External ICC profile
    OutputIntent = new OutputIntent("FOGRA39")        // Output intent for printing
};

// Perform the conversion
pdfDocument.Convert(conversionOptions);
```

**İpucu:** ICC profilini atlamazsanız Aspose varsayılan bir profil ekler, ancak yazıcınızın beklediği profil tam olarak kullanıldığında renk kaymaları önlenir.

## Step 3: Save the PDF/X‑1a‑Compliant File

Belge artık PDF/X‑1a spesifikasyonuna uygun olduğuna göre dosyayı kaydediyoruz.

```csharp
pdfDocument.Save("YOUR_DIRECTORY/pdfx1a.pdf");
```

Dosya boyutunun artabileceğini fark edeceksiniz—ekstra kaynaklar gömülüyor, bu da güvenilir baskı çıktısı için tam olarak istediğiniz şey.

## Step 4: Render the First Page to PNG (Save PDF as PNG)

İşte ana anahtar kelime devreye giriyor: **save PDF as PNG** sayesinde küçük önizlemeler ya da web gösterimi yapacağız.

```csharp
// Configure PNG device with font analysis (helps with text extraction later)
PngDevice pngDevice = new PngDevice
{
    RenderingOptions = new RenderingOptions { AnalyzeFonts = true }
};

// Render only the first page
pngDevice.Process(pdfDocument.Pages[1], "YOUR_DIRECTORY/page1.png");
```

![Save PDF as PNG example](https://example.com/images/save-pdf-as-png.png "Example of a PDF page saved as PNG")

`AnalyzeFonts` bayrağı, Aspose'un PNG meta verisine font bilgisi eklemesini sağlar; bu, daha sonra orijinal metne geri dönmek istediğinizde kullanışlı bir hiledir.

## Step 5: Add a Watermark Stamp PDF

**watermark stamp PDF** eklemek, Aspose’un `TextStamp` sınıfı ile çok basittir. Damgayı bir dikdörtgene sığacak şekilde otomatik boyutlandıracağız.

```csharp
// Create a text stamp that auto‑adjusts its font size
TextStamp textStamp = new TextStamp("Important notice")
{
    AutoAdjustFontSizeToFitStampRectangle = true,
    AutoAdjustFontSizePrecision = 0.01f,
    Width = 400,               // Width of the stamp rectangle
    Height = 200,              // Height of the stamp rectangle
    WordWrapMode = TextFormattingOptions.WordWrapMode.ByWords
};

// Place the stamp on the first page
pdfDocument.Pages[1].AddStamp(textStamp);
```

**Neden otomatik ayarlama?** Sayfalar farklı yoğunluklara sahip olabilir; API’nin optimal font boyutunu hesaplamasına izin vermek, metnin dikdörtgeni aşmasını engeller.

## Step 6: Save the Stamped PDF

Damga ekledikten sonra değişiklikleri kalıcı hâle getiriyoruz.

```csharp
pdfDocument.Save("YOUR_DIRECTORY/stamped.pdf");
```

`stamped.pdf` dosyasını herhangi bir görüntüleyicide açtığınızda “Important notice” kutusunun düzgün bir şekilde ortalandığını göreceksiniz—manuel ayar gerekmez.

## Step 7: Export PDF to HTML (Export PDF to HTML)

Son olarak **export PDF to HTML** yapalım ve font kodlaması için CMap tercih edelim. Bu, oluşturulan HTML’in mümkün olduğunca Unicode kullanmasını sağlar ve metnin aranabilir kalmasını temin eder.

```csharp
HtmlSaveOptions htmlOptions = new HtmlSaveOptions
{
    FontEncodingStrategy = HtmlSaveOptions.FontEncodingRules.DecreaseToUnicodePriorityLevel
};

// Save the HTML representation
pdfDocument.Save("YOUR_DIRECTORY/cmap.html", htmlOptions);
```

Ortaya çıkan `cmap.html` dosyası, karmaşık grafikler için `<canvas>` öğeleri ve metin için uygun `<span>` etiketleri içerir; böylece SEO‑dostu web sayfalarına hazır olur.

## Full Working Example

Aşağıda, bir konsol uygulamasına yapıştırabileceğiniz tam program yer alıyor. Yalnızca yer tutucu yolları kendi dosyalarınıza göre değiştirin, hepsi bu kadar.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Devices;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source PDF
        Document pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");

        // 2️⃣ Convert to PDF/X‑1a (how to convert pdfx‑1a)
        PdfFormatConversionOptions conversionOptions = new PdfFormatConversionOptions(
            PdfFormat.PDF_X_1A,
            ConvertErrorAction.Delete)
        {
            IccProfileFileName = "YOUR_DIRECTORY/profile.icc",
            OutputIntent = new OutputIntent("FOGRA39")
        };
        pdfDocument.Convert(conversionOptions);

        // 3️⃣ Save the PDF/X‑1a file
        pdfDocument.Save("YOUR_DIRECTORY/pdfx1a.pdf");

        // 4️⃣ Render first page as PNG (save pdf as png)
        PngDevice pngDevice = new PngDevice
        {
            RenderingOptions = new RenderingOptions { AnalyzeFonts = true }
        };
        pngDevice.Process(pdfDocument.Pages[1], "YOUR_DIRECTORY/page1.png");

        // 5️⃣ Add a dynamic watermark stamp (add watermark stamp pdf)
        TextStamp textStamp = new TextStamp("Important notice")
        {
            AutoAdjustFontSizeToFitStampRectangle = true,
            AutoAdjustFontSizePrecision = 0.01f,
            Width = 400,
            Height = 200,
            WordWrapMode = TextFormattingOptions.WordWrapMode.ByWords
        };
        pdfDocument.Pages[1].AddStamp(textStamp);

        // 6️⃣ Save the stamped PDF
        pdfDocument.Save("YOUR_DIRECTORY/stamped.pdf");

        // 7️⃣ Export to HTML (export pdf to html)
        HtmlSaveOptions htmlOptions = new HtmlSaveOptions
        {
            FontEncodingStrategy = HtmlSaveOptions.FontEncodingRules.DecreaseToUnicodePriorityLevel
        };
        pdfDocument.Save("YOUR_DIRECTORY/cmap.html", htmlOptions);

        Console.WriteLine("All operations completed successfully.");
    }
}
```

**Beklenen çıktı**

- `pdfx1a.pdf` – baskıya hazır PDF/X‑1a dosyası
- `page1.png` – ilk sayfanın raster görüntüsü (küçük önizlemeler için ideal)
- `stamped.pdf` – ölçeklenebilir “Important notice” watermark’ı eklenmiş orijinal PDF
- `cmap.html` – Unicode fontlarla web‑dostu HTML sürümü

## Common Questions & Edge Cases

- **Kaynak PDF şifreli sayfalara sahip ise ne olur?**  
  Şifreyle yükleyin: `new Document("input.pdf", new LoadOptions { Password = "secret" })`.

- **Her dönüşümde ICC profiline ihtiyacım var mı?**  
  Kesinlikle değil—Aspose genel bir profil kullanabilir, ancak katı PDF/X‑1a uyumluluğu için baskı evinizin kullandığı profilin tam olarak sağlanması önerilir.

- **Birden fazla sayfayı PNG olarak render edebilir miyim?**  
  Tabii ki. `pdfDocument.Pages` üzerinde döngü kurup `pngDevice.Process(page, $"page{page.Number}.png")` çağrısı yapın.

- **HTML çıktısı mobil cihazlara uygun mu?**  
  Oluşturulan HTML, duyarlı `<canvas>` öğeleri içerir. Saf CSS‑tabanlı metin isterseniz `htmlOptions.SplitIntoPages = false` ayarlayın ve `htmlOptions.PartsEmbeddingMode` değerini ihtiyacınıza göre değiştirin.

## Tips for ASP.NET PDF Conversion

Bu kodu bir ASP.NET Core denetleyicisine entegre ederken şunları unutmayın:

1. **Sonucu diske yazmak yerine akış olarak gönderin**—`MemoryStream` kullanın ve `FileResult` döndürün.
2. **Document ve cihaz nesnelerini `using` bloğu içinde **dispose** edin

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}