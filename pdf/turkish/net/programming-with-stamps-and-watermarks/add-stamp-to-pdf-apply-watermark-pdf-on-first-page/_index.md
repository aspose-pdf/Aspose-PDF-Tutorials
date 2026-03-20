---
category: general
date: 2026-03-19
description: PDF'nin ilk sayfasına damga ekleyin ve Aspose.Pdf kullanarak C# ile PDF'ye
  filigran uygulayın. PDF'ye not eklemeyi öğrenin ve tam çalışan bir örnek görün.
draft: false
keywords:
- add stamp to pdf
- apply watermark pdf
- add note to pdf
- how to add stamp
- add stamp first page
language: tr
og_description: Aspose.Pdf kullanarak C# ile PDF'in ilk sayfasına damga ekleyin ve
  PDF'e filigran uygulayın. Tam adım adım rehber.
og_title: PDF'ye Damga Ekle – İlk Sayfada PDF Filigranı Uygula
tags:
- aspnet
- csharp
- pdf
- aspose
title: PDF'ye Damga Ekle – İlk Sayfada PDF Filigranı Uygula
url: /tr/net/programming-with-stamps-and-watermarks/add-stamp-to-pdf-apply-watermark-pdf-on-first-page/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PDF'ye Damga Ekle – İlk Sayfada PDF Üzerine Filigran Uygula

Ever needed to **add stamp to PDF** but weren't sure where to start? Maybe you also want to **apply watermark PDF** on that same page, or just drop a quick **add note to PDF** for reviewers. In this tutorial we'll walk through a complete, ready‑to‑run C# example that does exactly that, and we’ll explain the “why” behind each line so you can adapt it to any scenario.

We’ll cover everything from loading the source document to saving the stamped version, plus a few tips for handling multi‑page PDFs, scaling issues, and customizing the stamp appearance. By the end you’ll be able to answer “**how to add stamp**?” with confidence and know how to **add stamp first page** without breaking a sweat.

---

## Gereksinimler

- **Aspose.Pdf for .NET** (any recent version, e.g., 23.10) – PDF manipülasyonunu zahmetsiz hale getiren kütüphane.  
- .NET geliştirme ortamı (Visual Studio, VS Code, Rider – istediğiniz herhangi biri).  
- Bir giriş PDF dosyası (`input.pdf` olarak adlandıracağız) erişebileceğiniz bir klasöre yerleştirilmiş.  

Aspose.Pdf dışındaki ekstra NuGet paketlerine gerek yoktur ve kod .NET 6+ ile .NET Framework 4.7.2'de de çalışır.

![PDF'ye Damga Ekle örneği](/images/add-stamp-to-pdf.png "Metin damgası içeren bir PDF'nin ekran görüntüsü – add stamp to pdf")

*Alt metin: add stamp to pdf – PDF'nin ilk sayfasına uygulanan bir metin damgasının görsel örneği.*

## Adım 1 – Kaynak PDF Belgesini Yükle

To **add stamp to PDF**, we first need an in‑memory representation of the file. The `Aspose.Pdf.Document` class does the heavy lifting.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;

class PdfStampDemo
{
    static void Main()
    {
        // Load the original PDF (replace YOUR_DIRECTORY with your actual path)
        var pdfPath = @"YOUR_DIRECTORY\input.pdf";
        using var pdfDocument = new Document(pdfPath);
```

**Neden önemli:**  
`Document` dosya yapısını ayrıştırır, sayfalara, açıklamalara ve kaynaklara erişim sağlar. Bir `using` bloğu kullanmak dosya tutamacının hızlıca serbest bırakılmasını garantiler—daha sonra aynı dosyanın üzerine yazmaya çalıştığınızda bu önemlidir.

## Adım 2 – Metin Damgasını Oluştur ve Yapılandır

Now we’ll **add note to PDF** by creating a `TextStamp`. This object behaves like a watermark, but you can control size, font, and word‑wrap.

```csharp
        // Step 2: Create a text stamp that will serve as a note/watermark
        var textStamp = new TextStamp("Important note")
        {
            // Auto‑adjust font size so the text fits inside the stamp rectangle
            AutoAdjustFontSizeToFitStampRectangle = true,
            AutoAdjustFontSizePrecision = 0.01f,

            // Wrap words rather than breaking them mid‑word
            WordWrapMode = TextFormattingOptions.WordWrapMode.ByWords,

            // Define the stamp rectangle (you can tweak these values)
            Width = 400,
            Height = 200,

            // Turn off scaling – we want the stamp to keep its exact size
            Scale = false
        };
```

**Unutulmaması gereken önemli noktalar:**

- `AutoAdjustFontSizeToFitStampRectangle`, damganın metni asla taşmayacak şekilde küçülmesini veya büyümesini sağlar – farklı sayfa boyutlarına **applying watermark PDF** uygularken kullanışlıdır.  
- `WordWrapMode.ByWords`, metnin kelime sınırlarında kaydırılmasını sağlayarak notun okunabilir olmasını garantiler.  
- `Scale = false` ayarı, sayfa DPI'si değiştiğinde damganın gerilmesini önler.

## Adım 3 – Damgayı İlk Sayfaya Ekle

If you’re wondering **how to add stamp** specifically to the first page, this is the spot. The `Pages` collection is 1‑based, so `Pages[1]` is the frontmost page.

```csharp
        // Step 3: Add the configured stamp to the first page
        pdfDocument.Pages[1].AddStamp(textStamp);
```

**Neden ilk sayfa?**  
Birçok yasal veya marka gereksinimi yalnızca kapak sayfasında görünür bir filigran ister. `Pages[1]` hedefleyerek **add stamp first page** senaryosunu tüm belgeyi döngüye sokmadan karşılarız.

## Adım 4 – Değiştirilen PDF'yi Kaydet

Finally, write the changes back to disk. You can overwrite the original or create a new file; here we’ll generate `Stamped.pdf`.

```csharp
        // Step 4: Save the stamped PDF
        var outputPath = @"YOUR_DIRECTORY\Stamped.pdf";
        pdfDocument.Save(outputPath);
        Console.WriteLine($"Stamp added successfully! Output saved to {outputPath}");
    }
}
```

Running the program will produce a PDF where the first page displays the “Important note” stamp, effectively **adding a stamp to pdf** and also **applying watermark pdf** in one go.

## Opsiyonel: Farklı Senaryolar İçin Damgayı Ayarlama

### Birden Çok Sayfa

If you later decide you need the same note on *every* page, replace the single‑page line with a loop:

```csharp
foreach (var page in pdfDocument.Pages)
{
    page.AddStamp(textStamp);
}
```

### Görsel Damgalar

Aspose also supports `ImageStamp` if you prefer a logo over text. The same properties (size, position, scaling) apply.

### Damganın Konumlandırılması

By default the stamp appears at the top‑left corner of the rectangle. To move it, set `HorizontalAlignment` and `VerticalAlignment`:

```csharp
textStamp.HorizontalAlignment = HorizontalAlignment.Center;
textStamp.VerticalAlignment = VerticalAlignment.Middle;
```

## Yaygın Tuzaklar ve Profesyonel İpuçları

- **Dosya kilitleri:** `IOException` alıp dosyanın kullanımda olduğunu söylüyorsa, başka bir işlem (Explorer dahil) PDF'yi açık tutmadığından emin olun. `using` bloğu yardımcı olur, ancak iki kez kontrol edin.  
- **Yazı tipi sorunları:** Aspose varsayılan olarak sistem yazı tiplerini kullanır. Latin dışı scriptler için gerekli yazı tipini gömün veya `textStamp.Font`'u açıkça ayarlayın.  
- **Büyük PDF'ler:** 100 MB üzerindeki PDF'ler için kaydetmeden önce `pdfDocument.Optimize()` kullanarak dosya boyutunu küçültmeyi düşünün.  
- **Test:** Oluşan `Stamped.pdf`'yi birden fazla görüntüleyicide (Adobe Reader, Edge, Chrome) açarak damganın tutarlı render edildiğini doğrulayın.  

## Tam Çalışan Örnek (Kopyala‑Yapıştır Hazır)

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;

class PdfStampDemo
{
    static void Main()
    {
        // 1️⃣ Load the source PDF
        var pdfPath = @"YOUR_DIRECTORY\input.pdf";
        using var pdfDocument = new Document(pdfPath);

        // 2️⃣ Create a configurable text stamp (our note/watermark)
        var textStamp = new TextStamp("Important note")
        {
            AutoAdjustFontSizeToFitStampRectangle = true,
            AutoAdjustFontSizePrecision = 0.01f,
            WordWrapMode = TextFormattingOptions.WordWrapMode.ByWords,
            Width = 400,
            Height = 200,
            Scale = false,
            HorizontalAlignment = HorizontalAlignment.Center,
            VerticalAlignment = VerticalAlignment.Middle
        };

        // 3️⃣ Add the stamp to the first page (add stamp first page)
        pdfDocument.Pages[1].AddStamp(textStamp);

        // 4️⃣ Save the stamped PDF
        var outputPath = @"YOUR_DIRECTORY\Stamped.pdf";
        pdfDocument.Save(outputPath);

        Console.WriteLine($"Stamp added successfully! Output saved to {outputPath}");
    }
}
```

**Beklenen sonuç:**  
Open `Stamped.pdf`; the first page shows a centered “Important note” box sized 400 × 200 points, with the text automatically resized to fit. All other pages remain untouched.

## Sonuç

We’ve just demonstrated how to **add stamp to pdf** and **apply watermark pdf** in a clean, reusable way. By loading the document, configuring a `TextStamp`, attaching it to the **add stamp first page**, and saving, you get a professional‑looking note without fiddling with low‑level PDF streams.

From here you can explore adding stamps to every page, swapping in images, or even stacking multiple stamps for complex branding. The same pattern—create, configure, attach, save—holds true across most Aspose.Pdf tasks, so you’ll find it easy to extend.

Got a different use case, like stamping a confidential label on dozens of PDFs in a batch job? Try wrapping the above logic in a `foreach` that iterates over a folder of files. Or, if you need to **add note to pdf** conditionally based on page content, check out Aspose’s `TextFragmentAbsorber` for searching text before stamping.

Happy coding, and may your PDFs always be stamped exactly the way you need! 

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}