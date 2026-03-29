---
category: general
date: 2026-03-29
description: pdf'yi pdf/x-1a'ya dönüştür ve pdf sayfasını png olarak tek bir akışta
  dışa aktar – ayrıca Aspose.Pdf (C#) kullanarak pdf'ye metin damgası eklemeyi öğren.
draft: false
keywords:
- convert pdf to pdf/x-1a
- export pdf page png
- add text stamp pdf
- Aspose.Pdf conversion
- PDF/X‑1a workflow
language: tr
og_description: pdf'yi pdf/x-1a'ya dönüştür ve pdf sayfasını png olarak dışa aktarırken
  metin damgası ekle – Aspose.Pdf ile tam C# rehberi.
og_title: PDF'yi PDF/X-1a'ya dönüştür, sayfayı PNG olarak dışa aktar ve metin damgası
  ekle
tags:
- Aspose.Pdf
- C#
- PDF processing
title: PDF'yi PDF/X-1a'ya dönüştür, sayfayı PNG olarak dışa aktar ve metin damgası
  ekle
url: /tr/net/conversion-export/convert-pdf-to-pdf-x-1a-export-page-png-add-text-stamp/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# pdf'yi pdf/x-1a'ya dönüştür, sayfa png olarak dışa aktar ve metin damgası ekle – Tam C# Kılavuzu

PDF'yi **pdf/x-1a'ya dönüştürmek** isteyip aynı zamanda ilk sayfanın hızlı bir PNG önizlemesini ve aynı belgeye özel bir metin damgası eklemek istemiş miydiniz? Yalnız değilsiniz. Birçok üretim hattında—baskıya hazır ön‑kontrol ya da otomatik rapor oluşturma gibi—bu tam kombinasyona sıkça rastlarsınız.

Bu öğreticide, art arda üç işi yapan tek, bütünleşik bir iş akışını adım adım inceleyeceğiz: **pdf'yi pdf/x-1a'ya dönüştür**, **pdf sayfasını png olarak dışa aktar**, ve **pdf'ye metin damgası ekle**. Kod, .NET için Aspose.Pdf kütüphanesini kullanır, böylece düşük seviyeli PDF iç detaylarıyla uğraşmadan profesyonel bir çözüm elde edersiniz. Sonunda, herhangi bir console uygulamasına, Azure Function'a veya CI adımına ekleyebileceğiniz çalıştırılabilir bir C# programınız olacak.

> **Ne elde edeceksiniz** – tam kaynak dosyası, adım adım açıklamalar, yaygın tuzaklar için ipuçları ve çıktıyı hızlıca doğrulamanın bir yolu.

## Önkoşullar

- .NET 6.0 veya daha yenisi (API, .NET Framework 4.x ile de çalışır).  
- Aspose.Pdf for .NET NuGet paketi (`Aspose.Pdf`) – yazı zamanı itibarıyla sürüm 23.10 günceldir.  
- Bir giriş PDF'i (`input.pdf`) ve bir ICC profil dosyası (`Coated_Fogra39L_VIGC_300.icc`) kontrol ettiğiniz bir klasöre yerleştirilmiş.  
- C# ve Visual Studio (veya tercih ettiğiniz IDE) hakkında temel bilgi.

Eğer bunlardan herhangi biri size yabancı geliyorsa, NuGet paketini şu şekilde kurabilirsiniz:

```bash
dotnet add package Aspose.Pdf --version 23.10.0
```

Şimdi başlayalım.

## Adım 1: Kaynak PDF belgesini yükle

İlk olarak çalışmak istediğimiz PDF'i açıyoruz. Aspose.Pdf’in `Document` sınıfı tüm dosyayı temsil eder ve içeriği tembel bir şekilde yükler, böylece sayfalara dokunana kadar performans cezası ödemezsiniz.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Devices;
using Aspose.Pdf.Text;
using Aspose.Pdf.Conversion;

// Adjust these paths to match your environment
string baseDir = @"C:\MyProjects\PdfDemo\";
string inputPath = Path.Combine(baseDir, "input.pdf");

// Load the PDF – this is where any file‑not‑found errors will surface
Document pdfDoc = new Document(inputPath);
```

*Bu neden önemlidir*: Belgeyi erken yüklemek, dönüşüm, render ve damga ekleme işlemleri için tek bir nesne kullanmamızı sağlar. Açık bir yükleme yapmaz ve var olmayan bir dosya üzerinde çalışmaya çalışırsanız, daha sonra gizemli bir `FileNotFoundException` alırsınız.

## Adım 2: Belgeyi özel bir ICC profili kullanarak PDF/X‑1a'ya dönüştür

PDF/X‑1a, baskıya hazır PDF'lerin de‑facto standardıdır. Dönüştürme adımı aynı zamanda bir **Output Intent** (ICC profili) eklemenizi sağlar, böylece sonraki RIP'ler renklerin nasıl yorumlanacağını tam olarak bilir.

```csharp
// Prepare conversion options – we ask Aspose to delete any objects that would break PDF/X‑1a compliance
PdfFormatConversionOptions conversionOptions = new PdfFormatConversionOptions(
    PdfFormat.PDF_X_1A,               // Target format
    ConvertErrorAction.Delete)       // Drop non‑compliant objects automatically
{
    IccProfileFileName = Path.Combine(baseDir, "Coated_Fogra39L_VIGC_300.icc"),
    OutputIntent = new OutputIntent("FOGRA39") // Human‑readable name for the intent
};

// Perform the conversion in‑place
pdfDoc.Convert(conversionOptions);
```

*Pro ipucu*: Daha katı hata yönetimi istiyorsanız, `ConvertErrorAction.Delete` yerine `ConvertErrorAction.Throw` kullanın. Böylece dönüşüm, ilk uyumsuzlukta durur ve otomatik QA hat hatları için kullanışlıdır.

## Adım 3: İlk sayfayı PNG olarak dışa aktar ve yazı tiplerini analiz et

PNG önizlemesi, hızlı görsel kontroller veya küçük resim oluşturma için sıkça gerekir. `AnalyzeFonts` özelliğini etkinleştirerek Aspose, gömülü yazı tiplerinin doğru rasterleştirildiğinden emin olur, eksik glif sürprizlerini önler.

```csharp
// Configure the PNG device – you can tweak resolution, color depth, etc.
PngDevice pngDevice = new PngDevice
{
    RenderingOptions = new RenderingOptions
    {
        AnalyzeFonts = true,          // Guarantees faithful text rendering
        Resolution = 300              // 300 DPI is a good trade‑off for quality vs. size
    }
};

// Export the first page (index is 1‑based)
string pngPath = Path.Combine(baseDir, "page1.png");
pngDevice.Process(pdfDoc.Pages[1], pngPath);
```

Bu işlem tamamlandığında, kaynak dosyalarınızın yanında `page1.png` dosyasını bulacaksınız. Dönüşümün doğru göründüğünden emin olmak için herhangi bir görüntü görüntüleyicide açın.

## Adım 4: Yazı tipi boyutunu otomatik ayarlayan bir metin damgası ekle

**Metin damgası**, içeriği değiştirmeden PDF'ye filigran veya açıklama eklemenin pratik bir yoludur. `AutoAdjustFontSizeToFitStampRectangle` ayarı, kütüphanenin metni tanımladığınız dikdörtgen içinde taşmadan küçültüp büyütmesini sağlar.

```csharp
// Create a stamp with the desired text
TextStamp autoSizeStamp = new TextStamp("Auto‑size")
{
    AutoAdjustFontSizeToFitStampRectangle = true,
    Width = 400,        // Width of the stamp rectangle (points)
    Height = 200,       // Height of the stamp rectangle (points)
    // Optional: position the stamp – here we center it on the page
    HorizontalAlignment = HorizontalAlignment.Center,
    VerticalAlignment = VerticalAlignment.Center,
    // Optional: give it a semi‑transparent background for readability
    Background = new BackgroundInfo(Color.FromRgb(255, 255, 0), 0.3f)
};

// Attach the stamp to the first page (you could loop over all pages if needed)
pdfDoc.Pages[1].AddStamp(autoSizeStamp);
```

*Neden otomatik‑boyut?* Daha sonra damga metnini daha uzun bir şeyle (ör. dinamik zaman damgası) değiştirirseniz, font boyutlarını manuel olarak yeniden hesaplamanıza gerek kalmaz—damga anında uyum sağlar.

## Adım 5: Güncellenmiş PDF belgesini kaydet

Son olarak her şeyi diske yazıyoruz. Orijinal dosyanın üzerine yazabilir ya da tamamen yeni bir dosya oluşturabilirsiniz; aşağıdaki örnek `output.pdf` oluşturur.

```csharp
string outputPath = Path.Combine(baseDir, "output.pdf");
pdfDoc.Save(outputPath);
```

Kaydetme tamamlandığında şunlara sahip olacaksınız:

1. **PDF/X‑1a** uyumlu bir dosya (`output.pdf`).  
2. İlk sayfanın **PNG önizlemesi** (`page1.png`).  
3. Dikdörtgenine mükemmel oturan bir **metin damgası**.

### Hızlı doğrulama kontrol listesi

| ✅ Kontrol | Nasıl doğrulanır |
|-----------|-------------------|
| PDF/X‑1a uyumluluğu | `output.pdf` dosyasını Adobe Acrobat'ta Aç → *Print Production* → *Preflight* ve “PDF/X‑1a:2001” seçeneğini seçin. |
| PNG doğru görünüyor | `page1.png` dosyasını Windows Fotoğraf Görüntüleyicisi'nde ya da herhangi bir görüntü düzenleyicide açın. |
| Damga görünüyor | `output.pdf` içinde kaydırın – “Auto‑size” metni sayfa 1'de ortalanmış olmalı. |

![pdf'yi pdf/x-1a'ya dönüştürme önizlemesi](image.png "pdf'yi pdf/x-1a'ya dönüştürme önizlemesi, damgalı sayfayı gösteriyor")

*Görsel alt metni*: **pdf'yi pdf/x-1a'ya dönüştürme önizlemesi, otomatik boyutlu metin damgası** – tüm adımlardan sonra oluşan son PDF'i gösterir.

## Yaygın Varyasyonlar ve Kenar Durumları

- **Birden fazla sayfa** – Her sayfaya damga eklemeniz gerekiyorsa, `pdfDoc.Pages` üzerinde döngü yapın ve döngü içinde `AddStamp` çağırın.  
- **Farklı çıktı formatı** – Arşiv PDF'leri için `PdfFormat.PDF_X_1A` yerine `PdfFormat.PDF_A_1B` kullanın.  
- **Yüksek çözünürlüklü PNG** – Baskı kalitesinde küçük resimler için `RenderingOptions` içinde `Resolution = 600` ayarlayın.  
- **Damga için özel yazı tipi** – Damgayı eklemeden önce `autoSizeStamp.Font = FontRepository.FindFont("Arial")` atayın.  
- **Hata yönetimi** – Her ana adımı bir `try/catch` bloğuna alın ve daha kolay hata ayıklama için `ConversionException` veya `FileNotFoundException` kaydedin.

## Tam Çalışan Örnek (Kopyala‑Yapıştır Hazır)

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Devices;
using Aspose.Pdf.Text;
using Aspose.Pdf.Conversion;
using Aspose.Pdf.Color; // For BackgroundInfo color

class PdfX1aWorkflow
{
    static void Main()
    {
        // -----------------------------------------------------------------
        // 1️⃣ Setup paths
        // -----------------------------------------------------------------
        string baseDir = @"C:\MyProjects\PdfDemo\";
        string inputPdf = Path.Combine(baseDir, "input.pdf");
        string iccProfile = Path.Combine(baseDir, "Coated_Fogra39L_VIGC_300.icc");
        string pngOutput = Path.Combine(baseDir, "page1.png");
        string finalPdf = Path.Combine(baseDir, "output.pdf");

        // -----------------------------------------------------------------
        // 2️⃣ Load the source document
        // -----------------------------------------------------------------
        Document pdfDoc = new Document(inputPdf);

        // -----------------------------------------------------------------
        // 3️⃣ Convert to PDF/X‑1a (print‑ready)
        // -----------------------------------------------------------------
        PdfFormatConversionOptions convOpts = new PdfFormatConversionOptions(
            PdfFormat.PDF_X_1A,
            ConvertErrorAction.Delete)
        {
            IccProfileFileName = iccProfile,
            OutputIntent = new OutputIntent("FOGRA39")
        };
        pdfDoc.Convert(convOpts);

        // -----------------------------------------------------------------
        // 4️⃣ Export first page as PNG (export pdf page png)
        // -----------------------------------------------------------------
        PngDevice pngDevice = new PngDevice
        {
            RenderingOptions = new RenderingOptions
            {
                AnalyzeFonts = true,
                Resolution = 300
            }
        };
        pngDevice.Process(pdfDoc.Pages[1], pngOutput);

        // -----------------------------------------------------------------
        // 5️⃣ Add auto‑sizing text stamp (add text stamp pdf)
        // -----------------------------------------------------------------
        TextStamp stamp = new TextStamp("Auto‑size")
        {
            AutoAdjustFontSizeToFitStampRectangle = true,
            Width = 400,
            Height = 200,
            HorizontalAlignment = HorizontalAlignment.Center,
            VerticalAlignment = VerticalAlignment.Center,
            Background = new BackgroundInfo(Color.From

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}