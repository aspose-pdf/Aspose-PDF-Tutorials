---
category: general
date: 2026-03-27
description: Aspose.Pdf for C# kullanarak PDF'de nasıl dikdörtgen çizileceğini öğrenin.
  PDF'ye dikdörtgen ekleyin, PDF'ye şekil ekleyin ve net kod örnekleriyle PDF'de şekil
  çizin.
draft: false
keywords:
- how to draw rectangle
- add rectangle to pdf
- add shape to pdf
- draw shape on pdf
- draw rectangle in pdf
language: tr
og_description: Aspose.Pdf kullanarak PDF'de dikdörtgen çizmeyi öğrenin. Bu öğreticide
  PDF'ye dikdörtgen ekleme, PDF'ye şekil ekleme ve PDF'de şekil çizme adım adım gösterilmektedir.
og_title: C# ile PDF'de Dikdörtgen Çizme – Tam Kılavuz
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: C# ile PDF'de Dikdörtgen Çizmek – Adım Adım Rehber
url: /tr/net/images-graphics/how-to-draw-rectangle-in-pdf-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# ile PDF'de Dikdörtgen Çizme – Adım Adım Kılavuz

Ever wondered **how to draw rectangle** in a PDF without wrestling with low‑level PDF syntax? You're not the only one. Many developers hit a wall when they need to visualise a bounding box, a highlight area, or a simple decorative element inside a generated document. The good news? With Aspose.Pdf for .NET the process is a piece of cake.

In this tutorial we’ll walk through everything you need to **add rectangle to PDF**, **add shape to PDF**, and ultimately **draw rectangle in PDF** using clean, idiomatic C#. By the end you’ll have a runnable program that produces a PDF file containing a crisp rectangle—no external tools required.

## Gereksinimler

- .NET 6.0 veya daha yeni (kod .NET Core ve .NET Framework ile de çalışır)
- Aspose.Pdf for .NET NuGet paketi (`Install-Package Aspose.Pdf`)
- Temel bir C# geliştirme ortamı (Visual Studio, VS Code, Rider, vb.)

No other libraries are needed; everything else is handled by Aspose.Pdf itself.

## Adım 1: Projeyi Kurun ve Ad Alanlarını İçe Aktarın

First, create a new console application and pull in the Aspose.Pdf namespace.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

namespace PdfRectangleDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll place the rest of the code here.
        }
    }
}
```

**Neden önemli:** `Aspose.Pdf.Drawing`'i içe aktarmak, **draw shape on PDF** için kullanacağımız `Rectangle` şekil sınıfına erişim sağlar. Giriş noktasını düzenli tutmak, sonraki adımları takip etmeyi kolaylaştırır.

## Adım 2: Yeni Bir PDF Belgesi ve Sayfa Oluşturun

A PDF without pages is meaningless, so we start by creating a document object and adding a single page.

```csharp
// Step 2: Initialize a new PDF document
Document pdfDoc = new Document();

// Add a blank page to the document (size defaults to A4)
Page page = pdfDoc.Pages.Add();
```

**Açıklama:** `Document` sınıfı tüm dosyayı temsil eder, `Pages.Add()` ise daha sonra **add rectangle to PDF** yapacağımız yeni bir `Page` nesnesi döndürür. Varsayılan A4 boyutu çoğu durumda işe yarar, ancak özel bir tuval gerekiyorsa genişlik/yükseklik belirtebilirsiniz.

## Adım 3: Dikdörtgen Şekli Tanımlayın

Now comes the core of **how to draw rectangle**—defining its position and dimensions.

```csharp
// Step 3: Define a rectangle shape (x, y, width, height)
// Coordinates are measured from the lower‑left corner of the page.
var rectangleShape = new Rectangle(100, 500, 300, 200)
{
    // Optional: set line color and fill color
    BorderColor = Color.Black,
    BorderWidth = 2,
    FillColor = Color.LightGray
};
```

**Bu özellikleri neden ayarlıyoruz:**  
- `BorderColor` ve `BorderWidth` konturu kontrol eder, dikdörtgeni görünür kılar.  
- `FillColor` ona hafif bir arka plan verir, bir bölgeyi vurgulamak istediğinizde faydalıdır.  
- `(x, y, width, height)` yapıcı, **draw rectangle in PDF**'i tam olarak ihtiyacınız olan yere çizebilmenizi sağlar.

## Adım 4: Dikdörtgeni Sayfaya Ekleyin

With the shape ready, we now **add shape to PDF** by attaching it to the page’s `Annotations` collection. Aspose.Pdf validates the bounds automatically, so you don’t have to worry about overflow.

```csharp
// Step 4: Add the rectangle shape to the page
page.Annotations.Add(rectangleShape);
```

**Arka planda neler oluyor:** `Annotations` koleksiyonu dikdörtgeni bir vektör grafiği olarak ele alır. PDF render edildiğinde, kütüphane koordinatlarımızı PDF içerik akışına dönüştürür.

## Adım 5: Belgeyi Kaydedin

Finally, write the PDF to disk so you can open it in any viewer.

```csharp
// Step 5: Save the PDF file
string outputPath = "RectangleDemo.pdf";
pdfDoc.Save(outputPath);
Console.WriteLine($"PDF saved to {outputPath}");
```

**Sonuç:** `RectangleDemo.pdf` dosyasını açtığınızda, sayfanın solundan 100 pt, altından 500 pt uzaklıkta, siyah kenarlı ve açık gri bir dikdörtgen görürsünüz. Bu, C# kullanarak PDF'de **how to draw rectangle** için tam çözümdür.

## Tam Çalışan Örnek

Putting all the pieces together, here’s the complete, ready‑to‑run program:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using Aspose.Pdf.Color;

namespace PdfRectangleDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Initialize a new PDF document
            Document pdfDoc = new Document();

            // Add a blank page (A4 by default)
            Page page = pdfDoc.Pages.Add();

            // Define a rectangle shape (x, y, width, height)
            var rectangleShape = new Rectangle(100, 500, 300, 200)
            {
                BorderColor = Color.Black,
                BorderWidth = 2,
                FillColor = Color.LightGray
            };

            // Add the rectangle to the page
            page.Annotations.Add(rectangleShape);

            // Save the document
            string outputPath = "RectangleDemo.pdf";
            pdfDoc.Save(outputPath);
            Console.WriteLine($"PDF saved to {outputPath}");
        }
    }
}
```

**Beklenen çıktı:** `RectangleDemo.pdf` adlı dosya, ortalanmış açık gri bir dikdörtgenin siyah kenarlığıyla tek bir sayfa içerir. Adobe Reader, Chrome veya herhangi bir PDF görüntüleyici ile açabilirsiniz.

## Yaygın Varyasyonlar ve Kenar Durumları

### 1. Birden Çok Dikdörtgen Çizme

If you need to **add rectangle to PDF** more than once, simply create additional `Rectangle` objects and add each to `page.Annotations`. Looping over a collection of coordinates makes this trivial.

```csharp
foreach (var rectInfo in rectangles)
{
    var rect = new Rectangle(rectInfo.X, rectInfo.Y, rectInfo.Width, rectInfo.Height)
    {
        BorderColor = Color.Blue,
        BorderWidth = 1,
        FillColor = Color.Transparent
    };
    page.Annotations.Add(rect);
}
```

### 2. Farklı Birimler Kullanma

Aspose.Pdf works in points (1 pt = 1/72 inch). If you prefer millimeters, convert them first:

```csharp
double mmToPt = 72.0 / 25.4;
float x = (float)(20 * mmToPt); // 20 mm from left
float y = (float)(150 * mmToPt);
```

### 3. Dikdörtgeni Form Alanı Olarak Eklemek

When you need an interactive rectangle (e.g., a clickable area), use a `LinkAnnotation` instead of a plain `Rectangle`. The code is similar but adds a URL or JavaScript action.

### 4. Uyumluluk Endişeleri

Aspose.Pdf version 23.9 (released early 2026) fully supports the APIs shown above. Older versions may require `page.AddAnnotation(rectangleShape)` instead of `page.Annotations.Add`. Always check the release notes if you encounter compile errors.

## Profesyonel İpuçları ve Tuzaklar

- **Pro ipucu:** Sadece bir kontur ihtiyacınız varsa `FillColor = Color.Transparent` ayarlayın. Bu, dosya boyutunu biraz azaltır.
- **Dikkat edilmesi gereken:** Sayfa boyutlarını aşan koordinatlar kullanmak. Aspose.Pdf şekli sessizce kırpar, bu da hata ayıklarken kafa karıştırıcı olabilir.
- **Performans notu:** Binlerce dikdörtgen eklemek sorun değil, ancak büyük raporlar üretiyorsanız, yükü azaltmak için şekilleri tek bir `Graphics` nesnesinde toplamak düşünün.

## Görsel Referans

Below is a quick screenshot of the generated PDF (the rectangle is highlighted in light gray). The alt text includes the primary keyword for SEO.

![how to draw rectangle in PDF example](https://example.com/images/rectangle-demo.png "how to draw rectangle in PDF example")

## Sonuç

We’ve covered **how to draw rectangle** in a PDF using Aspose.Pdf for C#. By creating a `Document`, adding a `Page`, defining a `Rectangle` shape, and finally **add shape to PDF**, you can generate vector‑based graphics with just a handful of lines. Whether you need to **add rectangle to pdf** for highlighting, layout debugging, or UI overlays, the approach scales nicely.

Next, you might explore **draw shape on pdf** beyond rectangles—think circles, polylines, or even custom SVG paths. Or dive into text rendering, image insertion, and PDF form manipulation to build full‑featured reports. The Aspose.Pdf library offers a rich API, and with the fundamentals covered here you’re ready to experiment.

Happy coding, and may your PDFs always look exactly how you envision!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}