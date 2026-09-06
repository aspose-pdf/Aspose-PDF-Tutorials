---
category: general
date: 2026-09-05
description: C#'ta boş bir sayfa ekleyerek, bir dikdörtgen çizerek ve PDF dosyasını
  kaydederek PDF belgesi oluşturun. Adım adım bir Aspose.PDF örneğini izleyin.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create pdf document
- add blank page pdf
- draw rectangle pdf
- save pdf file
- how to add rectangle
language: tr
lastmod: 2026-09-05
og_description: C#'ta boş bir sayfa ekleyerek, bir dikdörtgen çizerek ve PDF dosyasını
  kaydederek PDF belgesi oluşturun. Aspose.PDF ile bu tam örneği izleyin.
og_image_alt: Screenshot showing a PDF document with a drawn rectangle on a blank
  page
og_title: Boş sayfa ve dikdörtgen içeren PDF belgesi oluşturma – C# rehberi
schemas:
- author: Aspose
  dateModified: '2026-09-05'
  description: Create PDF document in C# by adding a blank page, drawing a rectangle,
    and saving the PDF file. Follow a step‑by‑step Aspose.PDF example.
  headline: How to create PDF document with a blank page and rectangle
  type: TechArticle
- description: Create PDF document in C# by adding a blank page, drawing a rectangle,
    and saving the PDF file. Follow a step‑by‑step Aspose.PDF example.
  name: How to create PDF document with a blank page and rectangle
  steps:
  - name: 'Edge case: custom page size'
    text: 'If your layout requires a 6 × 9 inch page, replace the default call with:'
  - name: 'Pro tip: styling the rectangle'
    text: 'You can change the stroke color and line width:'
  - name: 'Edge case: overwriting existing files'
    text: 'Aspose.PDF overwrites an existing file by default. To protect previous
      outputs, check for file existence first:'
  - name: Expected output
    text: Running the program creates a single‑page PDF. When you open `output.pdf`
      you will see a blank white page with a red rectangle positioned 100 points from
      the left and bottom edges, measuring 200 × 200 points.
  type: HowTo
tags:
- PDF
- C#
- Aspose.PDF
- PDF generation
title: Boş sayfa ve dikdörtgen içeren PDF belgesi nasıl oluşturulur
url: /tr/net/document-creation/how-to-create-pdf-document-with-a-blank-page-and-rectangle/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Boş sayfa ve dikdörtgen ile PDF belgesi nasıl oluşturulur

Programmatically **PDF belgesi oluşturma** gerekiyorsa, bu kılavuz C#'ta tam bir çözüm gösterir. Boş bir sayfa eklemeyi, o sayfada bir dikdörtgen çizmeyi ve sonunda PDF dosyasını kaydetmeyi öğreneceksiniz. Örnek, .NET 6+ ve .NET Framework 4.5+ ile çalışan Aspose.PDF kütüphanesini kullanır.

Boş bir sayfa eklemek ve şekil çizmek, faturalar, sertifikalar veya özel raporlar için yaygın bir gereksinimdir. Bu öğreticinin sonunda, (100, 100) konumunda ve 200 × 200 puan boyutunda tek bir dikdörtgen içeren bir PDF üreten çalıştırılabilir bir projeye sahip olacaksınız.

## Önkoşullar

* Visual Studio 2022 (veya herhangi bir C# IDE)
* .NET 6 SDK veya .NET Framework 4.5+
* Aspose.PDF for .NET NuGet paketi  
  ```bash
  dotnet add package Aspose.PDF
  ```
* Çıktı dizinine yazma izni

Ek bir yapılandırma gerekmez; kod doğrudan çalışır.

## PDF belgesi oluşturma – genel bakış

Tüm süreç dört mantıksal adımdan oluşur:

1. **Instantiate** bir `Document` nesnesi – bu PDF dosyasını temsil eder.
2. **Add a blank page** – sayfa çizim için bir tuval sağlar.
3. **Draw a rectangle** – bir `Path` nesnesi şekli tanımlar.
4. **Save the PDF file** – belgeyi diske kaydeder.

Her adım kendi bölümünde izole edilmiştir, böylece gerektiğinde parçaları yeniden kullanabilir veya değiştirebilirsiniz.

![Diagram of a PDF with a rectangle on a blank page](https://example.com/placeholder-image.png){.img-fluid alt="Boş bir sayfada çizilmiş bir dikdörtgen içeren PDF belgesinin ekran görüntüsü"}

## Boş sayfa ekleme pdf

Herhangi bir grafik yerleştirilebilmesi için PDF en az bir sayfa içermelidir. `Pages.Add()` yöntemi varsayılan boyutlarda (A4) boş bir sayfa oluşturur. Farklı bir boyuta ihtiyacınız varsa, bir `PageSize` argümanı geçirin.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

// Step 1: Create a new PDF document
using var pdfDocument = new Document();

// Step 2: Add a blank page to the document
Page pdfPage = pdfDocument.Pages.Add();   // adds an A4 page by default
```

*Bu adımın önemi* – Sayfa nesnesi metin, görüntü ve vektör grafik koleksiyonlarını tutar. Sayfa olmadan bir dikdörtgen ekleme girişimi bir istisna oluşturur.

### Kenar durumu: özel sayfa boyutu

Düzeniniz 6 × 9 inç bir sayfa gerektiriyorsa, varsayılan çağrıyı şununla değiştirin:

```csharp
var pageSize = new Size(432, 648); // 72 points per inch
Page pdfPage = pdfDocument.Pages.Add(pageSize);
```

## Dikdörtgen çizme pdf

Dikdörtgen çizmek, bir `Rectangle` geometrisi oluşturup bunu bir `Path` içinde sarmakla ilgilidir. `ValidateBounds()` çağrısı, şeklin sayfa kenar boşlukları içinde kalmasını sağlayarak kırpılmayı önler.

```csharp
// Step 3: Define a rectangle shape (x, y, width, height)
Rectangle shapeRect = new Rectangle(100, 100, 200, 200);

// Step 4: Add the rectangle to the page contents
Path rectanglePath = new Path(shapeRect).ValidateBounds();
pdfPage.Contents.Add(rectanglePath);
```

*Bu adımın önemi* – `Path` nesnesi, Aspose.PDF tarafından kullanılan düşük seviyeli vektör ilkelidir. Kenar boşluklarını doğrulayarak, dikdörtgen sayfa sınırlarını aştığında çalışma zamanı hatalarını önlersiniz.

### Pro ipucu: dikdörtgeni stilize etme

Çizgi rengini ve çizgi kalınlığını değiştirebilirsiniz:

```csharp
rectanglePath.GraphInfo = new GraphInfo
{
    StrokeColor = Color.Red,
    LineWidth = 2
};
```

Bu, 2 puan kalınlığında kırmızı bir kontur oluşturur.

## PDF dosyasını kaydet

Belgeyi kalıcı hale getirmek, dosyayı diske yazar. `Save` yöntemi bir dosya yolu veya akış kabul eder. Mutlak bir yol sağlamak konumu açıkça belirtir; bu, otomasyon betikleri için faydalıdır.

```csharp
// Step 5: Save the PDF to a file
string outputPath = Path.Combine(Environment.CurrentDirectory, "output.pdf");
pdfDocument.Save(outputPath);
Console.WriteLine($"PDF saved to {outputPath}");
```

*Bu adımın önemi* – Kaydetme, bellek içi temsiliyin fiziksel bir dosyaya dönüştüğü tek noktadır. PDF'i bir web API'den döndürmeniz gerekiyorsa, dosya yolunu bir `MemoryStream` ile değiştirin.

### Kenar durumu: mevcut dosyaların üzerine yazma

Aspose.PDF varsayılan olarak mevcut bir dosyanın üzerine yazar. Önceki çıktıları korumak için önce dosyanın varlığını kontrol edin:

```csharp
if (File.Exists(outputPath))
{
    File.Delete(outputPath);
}
pdfDocument.Save(outputPath);
```

## Dikdörtgen ekleme – en iyi uygulamalar

* **Keep coordinates within the page margins** – `ValidateBounds()` kullanın veya kenar boşluklarını manuel olarak hesaplayın.
* **Reuse `GraphInfo` objects** birden fazla şekil çizerken; bu bellek tahsisatını azaltır.
* **Dispose of the `Document` object** (`using var` ile gösterildiği gibi) yerel kaynakları hızlıca serbest bırakmak için.
* **Test with different DPI settings** daha sonra raster görüntüler ekleyecekseniz; dikdörtgen gibi vektör şekilleri herhangi bir çözünürlükte net kalır.

## Tam çalışan örnek

Aşağıda, bir konsol uygulamasına kopyalayabileceğiniz tam program bulunmaktadır. Değişiklik yapmadan derlenir ve proje klasöründe `output.pdf` üretir.

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using Aspose.Pdf.Color;

class Program
{
    static void Main()
    {
        // Create a new PDF document
        using var pdfDocument = new Document();

        // Add a blank page to the document
        Page pdfPage = pdfDocument.Pages.Add();

        // Define a rectangle shape (x, y, width, height)
        Rectangle shapeRect = new Rectangle(100, 100, 200, 200);

        // Create a path for the rectangle and validate its bounds
        Path rectanglePath = new Path(shapeRect).ValidateBounds();

        // Optional: style the rectangle (red outline, 2‑pt width)
        rectanglePath.GraphInfo = new GraphInfo
        {
            StrokeColor = Color.Red,
            LineWidth = 2
        };

        // Add the rectangle to the page contents
        pdfPage.Contents.Add(rectanglePath);

        // Determine output path
        string outputPath = Path.Combine(Environment.CurrentDirectory, "output.pdf");

        // Ensure no leftover file blocks the save operation
        if (File.Exists(outputPath))
        {
            File.Delete(outputPath);
        }

        // Save the PDF to a file
        pdfDocument.Save(outputPath);
        Console.WriteLine($"PDF saved to {outputPath}");
    }
}
```

### Beklenen çıktı

Programı çalıştırmak tek sayfalı bir PDF oluşturur. `output.pdf` dosyasını açtığınızda, sol ve alt kenarlardan 100 puan uzakta konumlandırılmış, 200 × 200 puan ölçülerinde kırmızı bir dikdörtgen içeren boş beyaz bir sayfa göreceksiniz.

## Sonuç

Artık Aspose.PDF kullanarak C#'ta **create PDF document**, **add blank page pdf**, **draw rectangle pdf**, ve **save pdf file** konularını biliyorsunuz. Örnek temel API çağrılarını kapsar, her çağrının neden gerekli olduğunu açıklar ve özel sayfa boyutları veya dikdörtgen stilizasyonu gibi yaygın varyasyonlar için ipuçları sunar.  

Sonra, **metin ekleme**, **görüntü gömme** veya **çok sayfalı raporlar oluşturma** gibi ilgili konuları keşfedin. Aynı desen—bir `Document` nesnesi oluşturma, sayfaları manipüle etme, vektör veya raster içerik ekleme, ardından `Save`—tüm bu senaryolara uygulanır. Projenizin ihtiyaçlarına uygun farklı şekiller, renkler ve sayfa düzenleriyle denemeler yapmaktan çekinmeyin.

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanarak yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olmak için adım adım açıklamalar içeren tam çalışan kod örnekleri sunar.

- [PDF Belgesi Oluşturma C# – Sayfa Ekle, Dikdörtgen Çiz ve Kaydet](/pdf/english/net/document-creation/create-pdf-document-c-add-page-draw-rectangle-save/)
- [Aspose.PDF ile PDF Belgesi Oluşturma – Adım Adım Kılavuz](/pdf/english/net/document-creation/create-pdf-document-with-aspose-pdf-step-by-step-guide/)
- [Aspose ile PDF Belgesi Oluşturma – Sayfa Ekle, Metin Kutusu ve Form](/pdf/english/net/forms-annotations/create-pdf-document-with-aspose-add-page-text-box-and-form/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}