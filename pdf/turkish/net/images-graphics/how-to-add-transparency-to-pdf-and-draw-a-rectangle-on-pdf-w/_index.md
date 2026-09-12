---
category: general
date: 2026-09-12
description: Aspose.PDF ve C# kullanarak PDF'ye şeffaflık eklemeyi, PDF üzerinde bir
  dikdörtgen çizmeyi ve şeffaflıkla PDF'yi kaydetmeyi adım adım öğrenin – rehber.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add transparency to pdf
- draw rectangle on pdf
- save pdf with transparency
language: tr
lastmod: 2026-09-12
og_description: PDF'ye şeffaflık ekleyin, PDF üzerinde bir dikdörtgen çizin ve Aspose.PDF
  kullanarak C# ile şeffaflık içeren PDF'yi kaydedin. Bu eksiksiz öğreticiyi izleyin.
og_image_alt: Screenshot of a PDF page showing a semi‑transparent rectangle drawn
  with Aspose.PDF
og_title: PDF'ye şeffaflık ekleyin ve PDF üzerinde bir dikdörtgen çizin – tam C# rehberi
schemas:
- author: Aspose
  dateModified: '2026-09-12'
  description: Learn how to add transparency to PDF, draw a rectangle on PDF, and
    save PDF with transparency using Aspose.PDF in C# – step‑by‑step guide.
  headline: How to add transparency to PDF and draw a rectangle on PDF with Aspose.PDF
  type: TechArticle
tags:
- Aspose.PDF
- C#
- PDF manipulation
title: PDF'ye şeffaflık ekleme ve Aspose.PDF ile PDF üzerine dikdörtgen çizme
url: /tr/net/images-graphics/how-to-add-transparency-to-pdf-and-draw-a-rectangle-on-pdf-w/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PDF'ye şeffaflık ekleme ve Aspose.PDF ile PDF üzerine dikdörtgen çizme

PDF dosyalarına **şeffaflık eklemek** istiyorsanız, bu kılavuz C#'ta bunu tam olarak nasıl yapacağınızı gösterir. Ayrıca **PDF üzerine dikdörtgen çizme** ve sonunda **şeffaflıkla PDF kaydetme** konularını öğrenecek ve sonuçları raporlar, faturalar veya herhangi bir belge‑otomasyon iş akışında yeniden kullanabileceksiniz.

Bu öğreticide şunları yapacaksınız:

* Mevcut bir PDF belgesini yükleme.
* Çizgi ve dolgu opaklığını tanımlayan özel bir grafik durum (graphics state) oluşturma.
* Bu grafik durumunu kanvasa uygulama ve bir dikdörtgen çizme.
* Değişiklikleri şeffaflık ayarları korunarak kaydetme.

Aspose.PDF for .NET kütüphanesi dışındaki hiçbir araç gerekmez ve her kod satırı, *neden* önemli olduğunu anlamanız için açıklanmıştır.

## Önkoşullar

* .NET 6.0 veya üzeri (kod .NET Framework 4.7+ ile de çalışır).
* **Aspose.PDF for .NET**'in lisanslı veya deneme sürümü. NuGet üzerinden kurun:

```bash
dotnet add package Aspose.Pdf
```

* Projenizden referans verebileceğiniz bir klasörde bulunan bir giriş PDF'i (`input.pdf`).

## Adım 1: PDF belgesini yükleme

İlk işlem kaynak dosyayı açmaktır. `using` ifadesi, belgenin doğru şekilde serbest bırakılmasını sağlar; bu da daha sonra kaydetmeye çalıştığınızda dosya kilitlenmesi sorunlarını önler.

```csharp
// Step 1: Load the PDF document
string pdfPath = @"YOUR_DIRECTORY\input.pdf";
using var pdfDocument = new Aspose.Pdf.Document(pdfPath);
```

*Neden önemli*: Belgeyi yüklemek, sayfa koleksiyonuna, kaynak sözlüklerine ve çizim için gerekli kanvas nesnelerine erişim sağlar.

## Adım 2: İlk sayfanın kaynak sözlüğüne erişme

Her PDF sayfasının **kaynak sözlüğü** (resource dictionary) vardır; burada fontlar, resimler ve grafik durumları gibi nesneler saklanır. Yeni bir şeffaflık ayarı eklemek için `ExtGState` girişini düzenlememiz gerekir.

```csharp
// Step 2: Access the first page and its resource dictionary
var firstPage = pdfDocument.Pages[1];               // PDF pages are 1‑based
var resourcesEditor = new Aspose.Pdf.DictionaryEditor(firstPage.Resources);
```

*Neden önemli*: `DictionaryEditor`, belge yapısını bozmadan düşük seviyeli PDF nesnelerini okur ve değiştirir.

## Adım 3: Şeffaflık değerleriyle özel bir grafik durumu oluşturma

Bir grafik durumu (`ExtGState`), çizim işlemlerinin nasıl işlendiğini kontrol eder. İki opaklık parametresi tanımlıyoruz:

* **CA** – çizgi (stroke) opaklığı (şekillerin dış çizgisi).
* **ca** – dolgu (fill) opaklığı (şekillerin iç kısmı).

Ayrıca karışım modunu (`BM`) “Normal” olarak ayarlıyoruz; bu en yaygın birleştirme (compositing) işlemidir.

```csharp
// Step 3: Create a custom graphics state (ExtGState) with transparency settings
var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
var customGs = Aspose.Pdf.Cos.CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

var parameters = new[]
{
    new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
        "CA", new Aspose.Pdf.Cos.CosPdfNumber(1)),          // stroke opacity = 100 %
    new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
        "ca", new Aspose.Pdf.Cos.CosPdfNumber(0.5)),        // fill opacity = 50 %
    new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
        "BM", new Aspose.Pdf.Cos.CosPdfName("Normal"))      // normal blend mode
};

foreach (var p in parameters)
    customGs.Add(p);

// Register the new graphics state under the name "GS0"
extGStateDict.Add("GS0", customGs);
```

*Neden önemli*: `ExtGState` sözlüğüne `GS0` ekleyerek, kanvasın çizimden önce etkinleştirebileceği yeniden kullanılabilir bir referans oluştururuz. `0.5` dolgu opaklığı, dikdörtgeni yarı‑şeffaf hâle getirerek **PDF'ye şeffaflık ekleme** hedefini gerçekleştirir.

## Adım 4: Grafik durumunu uygulama ve bir dikdörtgen çizme

Şimdi sayfanın kanvasına az önce oluşturduğumuz grafik durumunu kullanmasını söylüyoruz, ardından bir dikdörtgen çiziyoruz. Koordinatlar PDF koordinat sistemine (orijin sol‑alt köşede) göre verilir.

```csharp
// Step 4: Apply the custom graphics state and draw a rectangle
var canvas = firstPage.Canvas;

// Activate the transparency graphics state
canvas.SetGraphicsState("GS0");

// Draw a rectangle from (100, 500) to (200, 600)
canvas.Rectangle(100, 500, 200, 600);

// Render the rectangle outline using the current graphics state
canvas.Stroke();
```

*Neden önemli*: `SetGraphicsState("GS0")` çizim bağlamını daha önce tanımlanan şeffaflık ayarlarına geçirir. `Rectangle` metodu şekli tanımlar, `Stroke` ise belirtilen opaklıkla dış çizgiyi çizer. Dolu bir dikdörtgen isterseniz `Stroke()` yerine `FillAndStroke()` kullanın.

## Adım 5: Şeffaflığı koruyarak değiştirilmiş PDF'i kaydetme

Son olarak belgeyi diske geri yazıyoruz. Çıktı dosyası yeni grafik durumunu, çizilen dikdörtgeni ve şeffaflık bilgisini içerir.

```csharp
// Step 5: Save the modified PDF
string outputPath = @"YOUR_DIRECTORY\output_with_extgstate.pdf";
pdfDocument.Save(outputPath);
```

*Neden önemli*: Belgeyi kaydetmek tüm değişiklikleri sonlandırır. Ortaya çıkan dosya herhangi bir PDF görüntüleyicide açılabilir ve dikdörtgen %50 dolgu opaklığıyla görünecektir.

### Beklenen sonuç

`output_with_extgstate.pdf` dosyasını açtığınızda, kenarı tamamen opak ve içi yarı‑şeffaf bir dikdörtgen görmelisiniz; bu sayede altındaki sayfa içeriği görünür olacaktır.

## Kenar durumları ve pratik ipuçları

| Durum | Önerilen ayarlama |
|-----------|------------------------|
| **Birden fazla sayfa** | `pdfDocument.Pages` üzerinde döngü kurarak 2‑4 adımları her hedef sayfa için tekrarlayın. |
| **Farklı opaklık değerleri** | `CA` (çizgi) ve `ca` (dolgu) için `CosPdfNumber` değerlerini `0` (tamamen şeffaf) ile `1` (tamamen opak) arasında istediğiniz bir sayıya değiştirin. |
| **Özel karışım modları** | `"Normal"` yerine `"Multiply"`, `"Screen"` veya görüntüleyicinizin desteklediği herhangi bir PDF‑standart karışım modunu kullanın. |
| **Dolu dikdörtgen** | `canvas.FillAndStroke()` çağrısını `canvas.Stroke()` yerine kullanarak hem dolgu hem de dış çizgi uygulayın. |
| **Aynı grafik durumunu yeniden kullanma** | Aynı sayfada birden çok şekil çizerken `canvas.SetGraphicsState("GS0")` ifadesini istediğiniz kadar tekrarlayabilirsiniz. |

**Pro ipucu:** Yeni bir `ExtGState` ekledikten sonra kaynak sözlüğünü her zaman kontrol edin. Sözlük mevcut değilse önce oluşturun:

```csharp
if (!resourcesEditor.ContainsKey("ExtGState"))
    resourcesEditor.Add("ExtGState", new Aspose.Pdf.Cos.CosPdfDictionary(pdfDocument));
```

## Tam, çalıştırılabilir örnek

Aşağıda, bir konsol uygulamasına kopyalayıp hemen çalıştırabileceğiniz, kendi yolunuzu (`YOUR_DIRECTORY`) belirteceğiniz bağımsız bir program yer alıyor.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Cos;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the PDF document
        string pdfPath = @"YOUR_DIRECTORY\input.pdf";
        using var pdfDocument = new Document(pdfPath);

        // 2️⃣ Access the first page’s resources
        var firstPage = pdfDocument.Pages[1];
        var resourcesEditor = new DictionaryEditor(firstPage.Resources);

        // Ensure ExtGState dictionary exists
        if (!resourcesEditor.ContainsKey("ExtGState"))
            resourcesEditor.Add("ExtGState", new CosPdfDictionary(pdfDocument));

        // 3️⃣ Create a custom graphics state with transparency
        var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
        var customGs = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

        var parameters = new[]
        {
            new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),   // stroke opacity
            new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // fill opacity
            new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
        };

        foreach (var p in parameters)
            customGs.Add(p);

        extGStateDict.Add("GS0", customGs);

        // 4️⃣ Apply the graphics state and draw a rectangle
        var canvas = firstPage.Canvas;
        canvas.SetGraphicsState("GS0");
        canvas.Rectangle(100, 500, 200, 600);
        canvas.Stroke(); // use FillAndStroke() for a filled shape

        // 5️⃣ Save the PDF with transparency
        string outputPath = @"YOUR_DIRECTORY\output_with_extgstate.pdf";
        pdfDocument.Save(outputPath);

        Console.WriteLine("PDF saved with a transparent rectangle at: " + outputPath);
    }
}
```

Programı çalıştırdığınızda `output_with_extgstate.pdf` oluşturulur; bu dosya **PDF'ye şeffaflık ekleme**, **PDF üzerine dikdörtgen çizme** ve **şeffaflıkla PDF kaydetme** işlemlerini tek bir akışta gösterir.

## Sonuç

Artık Aspose.PDF for .NET kullanarak **PDF'ye şeffaflık ekleme**, **PDF üzerine dikdörtgen çizme** ve **şeffaflıkla PDF kaydetme** konularını biliyorsunuz. Süreç, özel bir `ExtGState` oluşturmayı, bunu kanvasa uygulamayı ve değişiklikleri kalıcı hâle getirmeyi içerir. Bu temel blokları diğer şekiller, çoklu sayfalar veya dinamik opaklık değerleri için genişletebilirsiniz.

**Sonraki adımlar**

* `canvas.Ellipse`, `canvas.Path` veya `canvas.TextFragment` gibi diğer çizim primitive'lerini aynı grafik durumunu yeniden kullanarak keşfedin.
* Şeffaflığı resim bindirmeleriyle birleştirerek filigranlar oluşturun (`canvas.Image` + özel `ExtGState`).
* Gelişmiş birleştirme efektleri için Aspose.PDF belgelerinde **graphics state parameters** bölümünü inceleyin.

Kodlamanın tadını çıkarın ve şeffaflığın PDF iş akışlarınıza getirdiği görsel esnekliğin keyfini sürün!


## Sonraki Öğrenmeniz Gerekenler


Aşağıdaki öğreticiler, bu kılavuzda gösterilen tekniklere dayanarak yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini ustalaşmanız ve projelerinizde alternatif uygulama yaklaşımları keşfetmeniz için adım‑adım açıklamalı tam çalışan kod örnekleri içerir.

- [How to Create PDF in C# – Add Page, Draw Rectangle & Save](/pdf/english/net/document-creation/how-to-create-pdf-in-c-add-page-draw-rectangle-save/)
- [How to Add a Line Object in PDF Using Aspose.PDF for .NET: A Step-by-Step Guide](/pdf/english/net/document-manipulation/add-line-aspose-pdf-dotnet-tutorial/)
- [Add Image Stamps to PDFs Using Aspose.PDF for .NET: A Step-by-Step Guide](/pdf/english/net/images-graphics/add-image-stamp-to-pdf-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}