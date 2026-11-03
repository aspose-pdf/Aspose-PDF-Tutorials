---
category: general
date: 2026-10-10
description: Aspose.PDF kullanarak PDF'ye dikdörtgen eklemeyi, PDF üzerinde şekil
  çizmeyi ve değiştirilmiş PDF'yi kaydetmeyi öğrenin. Belirli bir PDF sayfasına erişim
  için adım adım kılavuz içerir.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add rectangle to PDF
- draw shape on PDF
- save modified PDF
- add shape to PDF
- access specific PDF page
language: tr
lastmod: 2026-10-10
og_description: Aspose.PDF kullanarak C#'de PDF'ye dikdörtgen ekleyin. Bu öğreticide
  PDF üzerinde şekil çizmeyi, belirli bir PDF sayfasına erişmeyi ve değiştirilmiş
  PDF'yi kaydetmeyi gösterir.
og_image_alt: Screenshot of a PDF page with a blue rectangle overlay created by Aspose.PDF
og_title: Aspose.PDF ile PDF'ye dikdörtgen ekleyin – tam C# rehberi
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Learn how to add rectangle to PDF, draw shape on PDF, and save modified
    PDF using Aspose.PDF. Includes step‑by‑step guide to access specific PDF page.
  headline: How to add rectangle to PDF with Aspose.PDF in C#
  type: TechArticle
- description: Learn how to add rectangle to PDF, draw shape on PDF, and save modified
    PDF using Aspose.PDF. Includes step‑by‑step guide to access specific PDF page.
  name: How to add rectangle to PDF with Aspose.PDF in C#
  steps:
  - name: Expected output
    text: 'Running the program prints:'
  - name: What if the PDF has only one page?
    text: Attempting to access `pdfDocument.Pages[1]` throws an `ArgumentOutOfRangeException`.
      Guard against this by checking `pdfDocument.Pages.Count` before indexing.
  - name: How to add multiple rectangles on different pages?
    text: Repeat Steps 2‑4 for each target page, adjusting the rectangle’s coordinates
      as needed. You can place the logic inside a loop that iterates over `pdfDocument.Pages`.
  - name: Can I use other shapes such as circles or polygons?
    text: Yes. Aspose.PDF provides `Ellipse`, `Polygon`, and `Polyline` classes that
      follow the same pattern as `Rectangle`. Replace the `new Aspose.Pdf.Drawing.Rectangle`
      call with the desired shape class.
  - name: Does the library support PDFs with rotated pages?
    text: Aspose.PDF automatically respects page rotation when rendering shapes. The
      rectangle’s coordinates are interpreted in the page’s native coordinate system,
      so no extra transformation is required.
  type: HowTo
tags:
- Aspose.PDF
- C#
- PDF manipulation
title: C#'ta Aspose.PDF ile PDF'e dikdörtgen nasıl eklenir
url: /tr/net/images-graphics/how-to-add-rectangle-to-pdf-with-aspose-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# ile Aspose.PDF kullanarak PDF'ye dikdörtgen ekleme

Programlı olarak **add rectangle to PDF** dosyalarına dikdörtgen eklemeniz gerekiyorsa, bu kılavuz tam olarak nasıl yapılacağını gösterir. **draw shape on PDF** öğesini nasıl çizeceğinizi, belirli bir sayfayı nasıl hedefleyeceğinizi ve **save modified PDF** işlemini hatasız nasıl kaydedeceğinizi öğreneceksiniz.

PDF belgeleriyle çalışmak, raporlama, faturalama veya belge açıklaması için yaygın bir gereksinimdir. Bu öğreticinin sonunda, **add shape to PDF** dosyalarına güvenle ekleyebilir, out‑of‑bounds hatalarını ele alabilir ve çözümü herhangi bir .NET projesine entegre edebilirsiniz.

## Önkoşullar

* .NET 6.0 SDK veya daha yeni bir sürüm yüklü  
* Visual Studio 2022 (veya herhangi bir C# IDE'si)  
* Aspose.PDF for .NET lisansı veya ücretsiz bir değerlendirme anahtarı – API her iki modda da aynı şekilde çalışır  
* `input.pdf` adlı bir PDF dosyası, kodunuzdan referans verebileceğiniz bir klasöre yerleştirilmiş  

Bu öğeler, örnek için tek dış bağımlılıklardır.

## Adım 1: Aspose.PDF NuGet paketini kurun

Aspose.PDF kütüphanesi, ihtiyacınız olan `Document`, `Rectangle` ve diğer çizim sınıflarını sağlar.

```bash
dotnet add package Aspose.PDF
```

Bu komutu çalıştırmak, Aspose.PDF'in en son kararlı sürümünü projenize ekler ve PDF sınıflarının derleme sırasında kullanılabilir olmasını sağlar.

## Adım 2: PDF belgesini yükleyin

İlk işlem, kaynak dosyayı yüklemektir. Bu, üzerinde değişiklik yapabileceğiniz bellek içi bir temsil oluşturur.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using System;

class PdfRectangleExample
{
    static void Main()
    {
        // Load the PDF document from disk
        var pdfDocument = new Document(@"YOUR_DIRECTORY\input.pdf");
```

*Neden önemli*: Belgeyi yüklemek, sayfalar koleksiyonuna erişmenizi sağlar; bu, daha sonra **access specific PDF page** için gereklidir.

## Adım 3: İkinci sayfaya erişin (sıfır‑tabanlı indeks)

PDF sayfaları `0`'dan başlar. İkinci sayfaya bir dikdörtgen yerleştirmek için `1` indeksindeki sayfayı alın.

```csharp
        // Access the second page (pages are zero‑based)
        var page = pdfDocument.Pages[1];
```

Belge iki sayfadan az içeriyorsa, bir `ArgumentOutOfRangeException` fırlatılır ve üretim kodunda bir koruma koşuluna ihtiyaç duyulduğunu bildirir.

## Adım 4: Dikdörtgen şekli oluşturun

`Rectangle` yapısını kullanarak dikdörtgenin konum ve boyutunu tanımlayın, ardından bir Aspose çizim nesnesi içinde paketleyin.

```csharp
        // Define rectangle bounds: (x, y, width, height)
        var rectangleBounds = new Rectangle(100, 100, 300, 200);
        var rectangleShape = new Aspose.Pdf.Drawing.Rectangle(rectangleBounds)
        {
            // Optional visual styling
            Border = new BorderInfo(BorderSide.All, 2f, Color.Blue),
            FillColor = Color.FromArgb(30, 0, 0, 255) // semi‑transparent blue
        };
```

*Neden önemli*: `BorderInfo` ve `FillColor` özellikleri, **draw shape on PDF** işlemini görünür bir kenarlık ve isteğe bağlı dolgu ile yapmanıza olanak tanır, böylece dikdörtgen okuyucular için öne çıkar.

## Adım 5: Dikdörtgeni sayfanın paragraf koleksiyonuna ekleyin

Aspose.PDF, çizim nesnelerini paragraf öğeleri olarak kabul eder. Dikdörtgeni sayfanın `Paragraphs` koleksiyonuna eklemek, onu sayfada render eder.

```csharp
        // Add the rectangle shape to the page
        page.Paragraphs.Add(rectangleShape);
```

Bu noktada bellek içindeki PDF belgesi yeni şekli içerir, ancak diskteki dosya, kaydedene kadar değişmez.

## Adım 6: Değiştirilmiş PDF'yi kaydedin ve out‑of‑bounds hatalarını yönetin

`Save` çağrısı, güncellenen belgeyi yeni bir dosyaya yazar. Dikdörtgen sayfa boyutlarını aşarsa, Aspose bir `PdfException` fırlatır. Bu istisna yakalanarak sorunu temiz bir şekilde raporlayabilirsiniz.

```csharp
        try
        {
            // Save the altered PDF to a new file
            pdfDocument.Save(@"YOUR_DIRECTORY\output.pdf");
            Console.WriteLine("PDF saved successfully with rectangle added.");
        }
        catch (Aspose.Pdf.Exceptions.PdfException ex)
        {
            // Handle shape that does not fit on the page
            Console.WriteLine($"Shape out of bounds: {ex.Message}");
        }
    }
}
```

*Neden önemli*: `try/catch` bloğu, uygulamanızın **save modified PDF** işlemini güvenli bir şekilde yapmasını sağlar ve hata mesajı, gerekirse dikdörtgenin koordinatlarını ayarlamanıza yardımcı olur.

## Tam çalışan örnek

Tüm adımları bir araya getirerek, işte eksiksiz, çalıştırmaya hazır program:

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using System;
using System.Drawing; // Required for Color

class PdfRectangleExample
{
    static void Main()
    {
        // Step 1: Load the PDF document
        var pdfDocument = new Document(@"YOUR_DIRECTORY\input.pdf");

        // Step 2: Access the second page (zero‑based)
        var page = pdfDocument.Pages[1];

        // Step 3: Create a rectangle shape positioned at (100,100) with width 300 and height 200
        var rectangleBounds = new Rectangle(100, 100, 300, 200);
        var rectangleShape = new Aspose.Pdf.Drawing.Rectangle(rectangleBounds)
        {
            Border = new BorderInfo(BorderSide.All, 2f, Color.Blue),
            FillColor = Color.FromArgb(30, 0, 0, 255) // semi‑transparent blue
        };

        // Step 4: Add the rectangle shape to the page's paragraph collection
        page.Paragraphs.Add(rectangleShape);

        // Step 5: Save the modified PDF, handling out‑of‑bounds cases
        try
        {
            pdfDocument.Save(@"YOUR_DIRECTORY\output.pdf");
            Console.WriteLine("PDF saved successfully with rectangle added.");
        }
        catch (Aspose.Pdf.Exceptions.PdfException ex)
        {
            Console.WriteLine($"Shape out of bounds: {ex.Message}");
        }
    }
}
```

### Beklenen çıktı

Programı çalıştırmak şu çıktıyı verir:

```
PDF saved successfully with rectangle added.
```

ve `output.pdf` dosyasını oluşturur; bu dosya, ikinci sayfada belirtilen koordinatlarda mavi bir dikdörtgenle birlikte orijinal içeriği gösterir.

Dikdörtgen sayfadan daha büyük olsaydı, şu hatayı görürdünüz:

```
Shape out of bounds: The shape exceeds page margins.
```

## Yaygın sorular ve uç durumlar

### PDF sadece bir sayfa içeriyorsa ne olur?

`pdfDocument.Pages[1]` erişmeye çalışmak bir `ArgumentOutOfRangeException` fırlatır. Bu durumu önlemek için indekslemeden önce `pdfDocument.Pages.Count` değerini kontrol edin.

```csharp
if (pdfDocument.Pages.Count < 2)
{
    Console.WriteLine("Document does not contain a second page.");
    return;
}
```

### Farklı sayfalara birden fazla dikdörtgen nasıl eklenir?

Her hedef sayfa için Adım 2‑4'ü tekrarlayın, dikdörtgenin koordinatlarını gerektiği gibi ayarlayın. Mantığı, `pdfDocument.Pages` üzerinde dönen bir döngü içinde yerleştirebilirsiniz.

### Daireler veya çokgenler gibi başka şekiller kullanabilir miyim?

Evet. Aspose.PDF, `Rectangle` ile aynı deseni izleyen `Ellipse`, `Polygon` ve `Polyline` sınıflarını sağlar. `new Aspose.Pdf.Drawing.Rectangle` çağrısını istediğiniz şekil sınıfıyla değiştirin.

### Kütüphane döndürülmüş sayfalara sahip PDF'leri destekliyor mu?

Aspose.PDF, şekilleri render ederken sayfa dönüşünü otomatik olarak dikkate alır. Dikdörtgenin koordinatları, sayfanın yerel koordinat sisteminde yorumlanır; bu yüzden ek bir dönüşüm gerekmez.

## Performans değerlendirmeleri

* **Memory usage** – Büyük bir PDF (yüzlerce megabayt) yüklemek, orantılı bellek tüketir. Yalnızca tek bir sayfayı değiştirmeniz gerekiyorsa, o sayfayı çıkarmak, değiştirmek ve ardından geri birleştirmek için `PdfFileInfo` kullanmayı düşünün.  
* **Batch processing** – Birçok belgeye şekil eklerken, tekrar eden lisans doğrulama yükünden kaçınmak için tek bir `License` örneğini yeniden kullanın.

## Sonraki adımlar

Artık **add rectangle to PDF** yapabildiğinize göre, aşağıdaki ilgili konuları keşfedin:

* **draw shape on PDF** – metin, resim ve filigranları üst üste bindirmeyi öğrenin  
* **add shape to PDF** – birden fazla şekli tek bir açıklama katmanında birleştirin  
* **save modified PDF** – akışları (`MemoryStream`) kullanarak PDF'leri doğrudan web API'lerinden döndürün  
* **access specific PDF page** – özel raporlar için sayfa aralığı çıkarımını uygulayın  

Marka yönergelerinize uygun olacak şekilde farklı renkler, çizgi stilleri ve şeffaflık seviyeleriyle deneyler yapın.

---

*Kodlamaktan keyif alın! Bu öğretici **add rectangle to PDF** konusunda size yardımcı olduysa, ekibinizle paylaşmayı veya topluluğa iyileştirmeler katkıda bulunmayı düşünün.*

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olmak için adım adım açıklamalar içeren eksiksiz çalışan kod örnekleri sunar.

- [How to Add Shape to PDF with Aspose.PDF in C# – Step‑by‑Step Guide](/pdf/english/net/images-graphics/how-to-add-shape-to-pdf-with-aspose-pdf-in-c-step-by-step-gu/)
- [How to Add a Line Object in PDF Using Aspose.PDF for .NET&#58; A Step-by-Step Guide](/pdf/english/net/document-manipulation/add-line-aspose-pdf-dotnet-tutorial/)
- [How to Create PDF in C# – Add Page, Draw Rectangle & Save](/pdf/english/net/document-creation/how-to-create-pdf-in-c-add-page-draw-rectangle-save/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}