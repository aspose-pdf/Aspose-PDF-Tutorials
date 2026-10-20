---
category: general
date: 2026-10-13
description: Aspose.Pdf for C# ile bir PDF'de şeffaflığı nasıl ayarlayacağınızı öğrenin.
  Ayrıca değiştirilmiş PDF'yi nasıl kaydedeceğinizi ve doldurma alfasını nasıl değiştireceğinizi
  görün.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to set transparency
- save modified pdf
- change fill alpha
- set fill opacity
- edit pdf resources
language: tr
lastmod: 2026-10-13
og_description: Aspose.Pdf for C# ile bir PDF'de şeffaflığı nasıl ayarlarsınız? PDF
  kaynaklarını düzenlemek, doldurma alfa değerini değiştirmek ve değiştirilmiş PDF
  dosyalarını kaydetmek için bu kılavuzu izleyin.
og_image_alt: Screenshot of a PDF page showing transparent graphics applied with Aspose.Pdf
  in C#
og_title: Aspose.Pdf C# ile PDF'de şeffaflığı ayarlama – adım adım rehber
schemas:
- author: Aspose
  dateModified: '2026-10-13'
  description: Learn how to set transparency in a PDF with Aspose.Pdf for C#. Also
    see how to save modified PDF and change fill alpha.
  headline: How to set transparency in a PDF with Aspose.Pdf C#
  type: TechArticle
- description: Learn how to set transparency in a PDF with Aspose.Pdf for C#. Also
    see how to save modified PDF and change fill alpha.
  name: How to set transparency in a PDF with Aspose.Pdf C#
  steps:
  - name: Load the PDF document
    text: '```csharp using Aspose.Pdf; using System.Collections.Generic;'
  - name: Edit PDF resources to add a graphics state
    text: '```csharp // Get the first page (pages are 1‑based) Page firstPage = pdfDocument.Pages[1];'
  - name: Change fill alpha and set fill opacity
    text: '```csharp // Create an empty graphics state dictionary CosPdfDictionary
      newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);'
  - name: Add the new graphics state to the ExtGState dictionary
    text: '```csharp // Register the new state under the name "GS0" extGStateDict.Add("GS0",
      newGraphicsState); ```'
  - name: (Optional) Apply the graphics state in a content stream
    text: 'If you want to draw a rectangle using the new fill opacity, add the following
      after the previous steps:'
  - name: Save modified PDF
    text: '```csharp // Persist the changes to a new file pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
      ```'
  - name: Next steps
    text: '* Explore other blend modes (`Multiply`, `Screen`, etc.) by changing the
      `BM` entry. * Adjust stroke alpha (`CA`) to create semi‑transparent outlines.
      * Combine multiple graphics states to build a library of reusable visual effects.'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF manipulation
- Transparency
title: Aspose.Pdf C# ile PDF'de şeffaflık nasıl ayarlanır
url: /tr/net/images-graphics/how-to-set-transparency-in-a-pdf-with-aspose-pdf-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Pdf C# ile bir PDF'de şeffaflık nasıl ayarlanır?

C# kullanarak bir PDF'de şeffaflık ayarlamanız gerekiyorsa, bu öğretici tam adımları gösterir. Ayrıca, değiştirilmiş PDF dosyalarını nasıl kaydedeceğinizi ve Aspose.Pdf ortamından çıkmadan doldurma alfa değerini nasıl değiştireceğinizi öğreneceksiniz.

Kılavuz, bir belgeyi yüklemeyi, PDF kaynaklarını düzenlemeyi, doldurma opaklığını tanımlayan bir grafik durumunu oluşturmayı ve değişiklikleri kalıcı hale getirmeyi adım adım anlatır. Harici araçlara gerek yoktur; her şey standart bir .NET projesi içinde çalışır.

## Önkoşullar

Başlamadan önce şunların yüklü olduğundan emin olun:

* .NET 6.0 veya daha yeni bir sürüm  
* Geçerli bir Aspose.Pdf for .NET lisansı (veya ücretsiz deneme anahtarı)  
* Bilinen bir dizinde bulunan bir giriş PDF dosyası  

Aspose.Pdf paketini NuGet üzerinden ekleyebilirsiniz:

```bash
dotnet add package Aspose.Pdf
```

## Bir PDF'de şeffaflık nasıl ayarlanır

Bu bölüm, temel uygulamayı içerir. Her adım, kodun **neden** gerekli olduğunu, sadece **ne** yaptığını açıklamaktadır.

### Adım 1: PDF belgesini yükleyin

```csharp
using Aspose.Pdf;
using System.Collections.Generic;

// Load the source PDF
using var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");
```

*Bu adım neden?*  
`Document` PDF dosyasının tamamını bellekte temsil eder. Dosyayı açmak, sayfalara, kaynaklara ve değiştireceğiniz düşük seviyeli nesnelere erişim sağlar.

### Adım 2: Grafik durumu eklemek için PDF kaynaklarını düzenleyin

```csharp
// Get the first page (pages are 1‑based)
Page firstPage = pdfDocument.Pages[1];

// Create an editor for the page's resource dictionary
DictionaryEditor resourceEditor = new DictionaryEditor(firstPage.Resources);

// Retrieve the ExtGState dictionary; it holds graphics state objects
CosPdfDictionary extGStateDict = resourceEditor["ExtGState"].ToCosPdfDictionary();
```

*Bu adım neden?*  
PDF sayfaları, fontlar, görüntüler ve grafik durumları gibi yeniden kullanılabilir nesneleri bir kaynak sözlüğünde saklar. `ExtGState` girdisi şeffaflık ayarlarını içerir. Bu sözlüğü düzenleyerek sayfanın başvurabileceği yeni bir durum tanımlayabilirsiniz.

### Adım 3: Doldurma alfasını değiştirin ve doldurma opaklığını ayarlayın

```csharp
// Create an empty graphics state dictionary
CosPdfDictionary newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

// Define the graphics state entries
var graphicsStateEntries = new[]
{
    // Stroke alpha (CA) – fully opaque
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
    // Fill alpha (ca) – 50 % transparent
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
    // Blend mode (BM) – normal composition
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
};

// Populate the new graphics state
foreach (var entry in graphicsStateEntries)
    newGraphicsState.Add(entry);
```

*Bu adım neden?*  
`ca` **doldurma opaklığını**, `CA` ise **çizgi (stroke) opaklığını** kontrol eder. `ca` değerini `0.5` olarak ayarlamak, doldurulmuş şekilleri %50 şeffaf yapar. `BM` girdisi karıştırma modunu seçer; `"Normal"` standart şeffaflık için en yaygın seçimdir.

### Adım 4: Yeni grafik durumunu ExtGState sözlüğüne ekleyin

```csharp
// Register the new state under the name "GS0"
extGStateDict.Add("GS0", newGraphicsState);
```

*Bu adım neden?*  
Grafik durumuna (`"GS0"`) bir ad vermek, sayfadaki içerik akışlarının `gs` operatörüyle ona başvurmasını sağlar. Bu kayıttan sonra sayfa, az önce tanımladığınız şeffaflığı uygulayabilir.

### Adım 5: (İsteğe bağlı) İçerik akışında grafik durumunu uygulayın

Yeni doldurma opaklığını kullanarak bir dikdörtgen çizmek istiyorsanız, önceki adımlardan sonra aşağıdakileri ekleyin:

```csharp
// Create a content stream that uses the new graphics state
string cs = @"
q               % Save graphics state
/GS0 gs         % Apply the graphics state defined earlier
0 0 200 100 re  % Define a rectangle (x, y, width, height)
0.2 0.6 0.8 rg  % Set fill color (RGB)
f               % Fill the rectangle using the current graphics state
Q               % Restore graphics state
";

firstPage.Contents.Add(new Aspose.Pdf.Operator.GsContent(cs));
```

*Bu adım neden?*  
`q`/`Q` operatörleri grafik durumunu kaydeder ve geri yükler, böylece şeffaflık yalnızca amaçlanan çizim komutlarını etkiler. `gs` operatörü, `"GS0"` adlı grafik durumuna geçiş yapar.

### Adım 6: Değiştirilmiş PDF'i kaydedin

```csharp
// Persist the changes to a new file
pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
```

*Bu adım neden?*  
Kaydetme, güncellenmiş kaynak sözlüğünü ve yeni içerik akışlarını diske yazar. Ortaya çıkan dosya (`output.pdf`) önceki adımda tanımlanan şeffaf dikdörtgeni içerir.

## Tam çalıştırılabilir örnek

Parçaları bir araya getirerek, derleyip çalıştırabileceğiniz tam bir program aşağıdadır:

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Operators;
using System.Collections.Generic;

class SetTransparencyDemo
{
    static void Main()
    {
        // Load the source PDF
        using var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");

        // Access the first page and its resources
        Page firstPage = pdfDocument.Pages[1];
        var resourceEditor = new DictionaryEditor(firstPage.Resources);
        var extGStateDict = resourceEditor["ExtGState"].ToCosPdfDictionary();

        // Create a new graphics state with 50 % fill opacity
        var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
        var graphicsStateEntries = new[]
        {
            new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),   // stroke alpha
            new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // fill alpha
            new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
        };
        foreach (var entry in graphicsStateEntries)
            newGraphicsState.Add(entry);

        // Register the graphics state as "GS0"
        extGStateDict.Add("GS0", newGraphicsState);

        // Optional: draw a rectangle using the new transparency
        string cs = @"
q
/GS0 gs
0 0 200 100 re
0.2 0.6 0.8 rg
f
Q
";
        firstPage.Contents.Add(new GsContent(cs));

        // Save the modified PDF
        pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
    }
}
```

**Beklenen sonuç** – `output.pdf` dosyası, %50 şeffaf bir açık mor renkle doldurulmuş bir dikdörtgen gösterir; bu sayede arka plan içeriği kısmen görünür olur.

## Yaygın sorular ve kenar durumları

* **Dolgu opaklığı yerine çizgi opaklığını değiştirebilir miyim?**  
  `CA` (büyük harf) değerini `0` (tamamen şeffaf) ile `1` (tamamen opak) arasında bir sayıya ayarlayın. Örnekte `CA` zaten `1` olarak ayarlanmıştır, bu da çizgilerin opak kalmasını sağlar.

* **Sayfada zaten bir ExtGState sözlüğü yoksa ne olur?**  
  `resourceEditor["ExtGState"]` otomatik olarak boş bir sözlük oluşturur. `"GS0"` eklemek aynı şekilde çalışır.

* **Grafik durumu birden fazla sayfada yeniden kullanılabilir mi?**  
  Evet. Girişi belge kaynak sözlüğüne eklediğinizde, `"GS0"` başvurusunda bulunan herhangi bir sayfa aynı şeffaflık ayarlarını miras alır.

* **Bu yaklaşım yüksek seviyeli `Graphics` API'si kullanmaktan nasıl farklıdır?**  
  Düşük seviyeli kaynak sözlüğünü düzenlemek, PDF iç yapıları üzerinde kesin kontrol sağlar ve ekstra nesneler eklemediği için dosya boyutunu küçültür.

## Sonuç

Artık Aspose.Pdf for C# ile **bir PDF'de şeffaflık nasıl ayarlanır** biliyorsunuz. Öğreticide PDF kaynaklarını düzenleme, doldurma alfasını değiştirme, doldurma opaklığını ayarlama ve değiştirilmiş PDF'i kaydetme konuları ele alındı. Bu temelle, farklı karıştırma modlarını deneyebilir, metne şeffaflık uygulayabilir veya karmaşık belgeler için yeniden kullanılabilir grafik durumları oluşturabilirsiniz.

### Sonraki adımlar

* `BM` girdisini değiştirerek diğer karıştırma modlarını (`Multiply`, `Screen` vb.) keşfedin.  
* Çizgi alfasını (`CA`) ayarlayarak yarı şeffaf konturlar oluşturun.  
* Birden fazla grafik durumu birleştirerek yeniden kullanılabilir görsel efektler kütüphanesi oluşturun.  

Sonuçlarınızı paylaşmaktan veya yorumlarda soru sormaktan çekinmeyin. İyi kodlamalar!

## Bir sonraki öğrenmeniz gerekenler

Aşağıdaki öğreticiler, bu kılavuzda gösterilen tekniklere dayanarak yakından ilgili konuları kapsar. Her kaynak, adım adım açıklamalarla birlikte tam çalışan kod örnekleri içerir; böylece ek API özelliklerini ustalaşabilir ve projelerinizde alternatif uygulama yaklaşımlarını keşfedebilirsiniz.

- [How to Customize PDFs with Aspose.PDF for .NET&#58; Set Page Margins and Draw Lines](/pdf/english/net/document-manipulation/customize-pdfs-aspose-pdf-set-margins-draw-lines/)
- [How to Set Image Size in a PDF Using Aspose-PDF for .NET](/pdf/english/net/images-graphics/set-image-size-pdf-aspose-dotnet/)
- [How to Set PDF Permissions Using Aspose.PDF for .NET&#58; A Comprehensive Guide](/pdf/english/net/security-permissions/set-pdf-privileges-aspose-pdf-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}