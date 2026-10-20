---
category: general
date: 2026-08-04
description: C# kullanarak PDF'ye dikdörtgen ekleyin. Aspose.Pdf ile PDF'de şekil
  çizmeyi açık ve eksiksiz bir örnekle öğrenin.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add rectangle to pdf
- how to draw shape in pdf c#
language: tr
lastmod: 2026-08-04
og_description: C# kullanarak PDF'ye dikdörtgen ekleyin. Bu öğretici, PDF'de C# ile
  şekil çizmeyi hızlı ve güvenilir bir şekilde gösterir.
og_image_alt: Screenshot of a PDF page with a blue rectangle drawn by C# code
og_title: C# ile PDF'ye Dikdörtgen Ekle – Tam Programlama Rehberi
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Add rectangle to PDF using C#. Learn how to draw shape in PDF C# with
    Aspose.Pdf in a clear, complete example.
  headline: Add rectangle to PDF with C# – step‑by‑step guide
  type: TechArticle
- description: Add rectangle to PDF using C#. Learn how to draw shape in PDF C# with
    Aspose.Pdf in a clear, complete example.
  name: Add rectangle to PDF with C# – step‑by‑step guide
  steps:
  - name: '**Create a new console project**'
    text: '**Create a new console project**'
  - name: '**Add the Aspose.Pdf package**'
    text: '**Add the Aspose.Pdf package**'
  - name: '**Place `input.pdf`** in the project directory (or any folder you reference
      later).'
    text: '**Place `input.pdf`** in the project directory (or any folder you reference
      later).'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: C# ile PDF'ye dikdörtgen ekleyin – adım adım rehber
url: /tr/net/images-graphics/add-rectangle-to-pdf-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# ile PDF'ye Dikdörtgen Ekle – Adım Adım Kılavuz

Eğer bir C# uygulamasından **PDF'ye dikdörtgen ekle**meniz gerekiyorsa, bu kılavuz tam olarak nasıl yapılacağını gösterir. Aspose.Pdf kütüphanesini kullanarak PDF C# içinde bir şekil çizen tam, çalıştırılabilir bir örnek görecek ve kodun her satırının neden önemli olduğunu anlayacaksınız.

PDF'lerde şekil çizmek, rapor oluşturucular, fatura şablonları ve özel belge markalaşması için yaygın bir gereksinimdir. Bu öğreticinin sonunda herhangi bir dikdörtgen açıklama ekleyebilir, boyutunu, rengini veya konumunu değiştirebilir ve mevcut içeriği kaybetmeden değiştirilmiş belgeyi kaydedebilirsiniz.

**Neler Öğreneceksiniz**

* Aspose.Pdf ile mevcut bir PDF nasıl yüklenir.
* Dikdörtgen sınırları nasıl tanımlanır ve bir dikdörtgen şekli nasıl oluşturulur.
* Dikdörtgen bir sayfanın paragraf koleksiyonuna nasıl eklenir.
* Güncellenen PDF nasıl kaydedilir ve sonuç nasıl doğrulanır.
* Çoklu sayfalar, şeffaflık ve özel çizgi stilleri için varyasyonlar.

**Ön Koşullar**

* .NET 6.0 veya üzeri (kod .NET Framework 4.7+ ile de çalışır).
* Visual Studio 2022 veya herhangi bir C# IDE'si.
* `Aspose.Pdf` NuGet referansı (ücretsiz deneme veya lisanslı sürüm).
* Proje içinde kontrol ettiğiniz bir klasöre yerleştirilmiş `input.pdf` adlı bir giriş PDF dosyası.

---

## PDF C# içinde şekil çizme – projeyi kurma

1. **Yeni bir konsol projesi oluşturun**  

   ```bash
   dotnet new console -n PdfRectangleDemo
   cd PdfRectangleDemo
   ```

2. **Aspose.Pdf paketini ekleyin**  

   ```bash
   dotnet add package Aspose.Pdf
   ```

3. **`input.pdf`** dosyasını proje dizinine (veya daha sonra referans vereceğiniz herhangi bir klasöre) yerleştirin.

Proje artık **PDF'ye dikdörtgen ekle** dosyalarını derleyecek koda hazır.

---

## Step 1: Load the PDF document

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

class Program
{
    static void Main()
    {
        // Load the existing PDF file.
        Document pdfDoc = new Document("input.pdf");
```

*`Document` sınıfı dosyayı ayrıştırır ve bir `Pages` koleksiyonu sunar. Çizim yapılmadan önce yükleme ilk gerekli işlemdir.*

---

## Step 2: Choose the target page

```csharp
        // Get the first page (pages are 1‑based).
        Page firstPage = pdfDoc.Pages[1];
```

*Dikdörtgeni farklı bir sayfaya eklemeniz gerekiyorsa, indeksi istediğiniz sayfa numarasıyla değiştirin. Kütüphane, indeks aralık dışı olduğunda bir istisna fırlatır; bu yüzden PDF'nin yeterli sayfaya sahip olduğundan emin olun.*

---

## Step 3: Define rectangle bounds

```csharp
        // Define the rectangle's position and size (points).
        // (left, bottom, right, top) – origin is bottom‑left.
        Rectangle bounds = new Rectangle(50, 700, 300, 800);
```

*Kooridinat sistemi puan (point) kullanır (1 pt = 1/72 inç). Örnek, sayfanın üst kısmına yakın 250 pt genişliğinde ve 100 pt yüksekliğinde bir dikdörtgen oluşturur. Sayfanıza uygun olacak şekilde sayıları ayarlayın.*

---

## Step 4: Create the rectangle shape

```csharp
        // Create a rectangle shape with the defined bounds.
        Rectangle rectangleShape = new Rectangle(bounds)
        {
            // Optional styling – a semi‑transparent blue fill.
            FillColor = Color.FromRgb(0, 120, 215),
            FillOpacity = 0.4,

            // Optional border – 2 pt thick, dark gray.
            Border = new Border
            {
                Width = 2,
                Color = Color.FromRgb(50, 50, 50)
            }
        };
```

*`Rectangle` sınıfı `GraphicalObject` sınıfından türetilir. `FillColor` ve `Border` ayarlamaları isteğe bağlıdır, ancak **how to draw shape in PDF C#** konusunu sadece basit bir konturun ötesinde nasıl kontrol edebileceğinizi gösterir.*

---

## Step 5: Add the rectangle to the page

```csharp
        // Add the rectangle shape to the page's paragraph collection.
        firstPage.Paragraphs.Add(rectangleShape);
```

*Paragraflar, çizilebilir herhangi bir nesnenin konteyneridir. Şekli `Paragraphs` içine ekleyerek, Aspose.Pdf belge kaydedildiğinde şekli render eder.*

---

## Step 6: Save the modified PDF

```csharp
        // Save the updated PDF to a new file.
        pdfDoc.Save("output.pdf");

        // Inform the user.
        Console.WriteLine("Rectangle added and saved to output.pdf");
    }
}
```

*Kaydetme yeni bir dosya oluşturur, böylece orijinal `input.pdf` değişmeden kalır. Aynı yolu vererek kaynak dosyanın üzerine yazabilirsiniz, ancak bir yedek tutmak en iyi uygulamadır.*

---

## Full source code (runnable)

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using System.Drawing;   // For Color struct

class Program
{
    static void Main()
    {
        // Step 1: Load the PDF document
        Document pdfDoc = new Document("input.pdf");

        // Step 2: Get the first page (pages are 1‑based)
        Page firstPage = pdfDoc.Pages[1];

        // Step 3: Define rectangle bounds (left, bottom, right, top)
        Rectangle bounds = new Rectangle(50, 700, 300, 800);

        // Step 4: Create a rectangle shape with optional styling
        Rectangle rectangleShape = new Rectangle(bounds)
        {
            FillColor = Color.FromArgb(102, 0, 120, 215), // 40 % opacity blue
            FillOpacity = 0.4,
            Border = new Border
            {
                Width = 2,
                Color = Color.FromRgb(50, 50, 50)
            }
        };

        // Step 5: Add the rectangle shape to the page
        firstPage.Paragraphs.Add(rectangleShape);

        // Step 6: Save the modified PDF
        pdfDoc.Save("output.pdf");

        Console.WriteLine("Rectangle added to PDF successfully.");
    }
}
```

**Beklenen çıktı** – `output.pdf` dosyasını herhangi bir PDF görüntüleyicide açın. İlk sayfanın sağ üst köşesine yakın, koyu gri bir kenarlıkla çevrelenmiş mavi doldurulmuş bir dikdörtgen görmelisiniz.

---

## PDF C# içinde şekil çizme – birden çok sayfada

Eğer her sayfada **PDF'ye dikdörtgen ekle**meniz gerekiyorsa, `Pages` koleksiyonunu döngüye alın:

```csharp
foreach (Page page in pdfDoc.Pages)
{
    Rectangle rect = new Rectangle(50, 700, 300, 800);
    Rectangle shape = new Rectangle(rect)
    {
        FillColor = Color.FromArgb(80, 255, 0, 0), // semi‑transparent red
        Border = new Border { Width = 1, Color = Color.Black }
    };
    page.Paragraphs.Add(shape);
}
```

*Bu desen aynı sınırları her sayfada yeniden kullanır. Farklı konumlar gerekiyorsa koordinatları sayfaya göre ayarlayın.*

---

## Common pitfalls and best‑practice tips

| Sorun | Neden oluşur | Çözüm |
|-------|--------------|------|
| Dikdörtgen sayfanın dışına çıkıyor | Koordinatlar sol‑alt köşeden ölçülür; üst‑yönlü bir koordinat sistemi kullanmak karışıklığa neden olabilir. | Y‑ekseninin yukarı doğru büyüdüğünü unutmayın. Değerlerin sayfa boyutuna (`page.PageInfo.Width`, `page.PageInfo.Height`) sığdığından emin olun. |
| Şekil görünmüyor | `FillOpacity` değeri `0` veya kenar kalınlığı `0` olarak ayarlanmış. | `FillOpacity` değerinin `0`'dan büyük ve `Border.Width` değerinin en az `0.5` olduğundan emin olun. |
| Kaydetme sırasında `AccessDeniedException` hatası | Çıktı dosyası başka bir programda açık. | Kodu çalıştırmadan önce tüm görüntüleyicileri kapatın veya farklı bir yola kaydedin. |
| Dikdörtgen mevcut içeriğin üzerine geliyor | Katmanlama kontrolü ayarlanmamış. | Katmanlamayı kontrol etmek için `ZIndex` özelliğini (daha yüksek değerler üstte render eder) kullanın. |

---

## Extending the rectangle – gradients, rotation, and transparency

Aspose.Pdf gelişmiş grafik özelliklerini destekler. Döndürülmüş bir dikdörtgeni lineer bir degrade ile oluşturmak için:

```csharp
Rectangle gradientRect = new Rectangle(bounds)
{
    // Gradient fill from left (blue) to right (green)
    FillColor = Color.Blue,
    FillColor2 = Color.Green,
    FillMode = FillMode.LinearGradient,
    // Rotate 45 degrees around the rectangle's center
    Rotation = 45
};
firstPage.Paragraphs.Add(gradientRect);
```

*Aynı kod deseni, **how to draw shape in PDF C#** konusunu daha zengin görsel efektlerle nasıl uygulayabileceğinizi gösterir.*

---

## Verify the result programmatically

Dikdörtgenin eklendiğini, sayfanın paragraf sayısını kontrol ederek doğrulayabilirsiniz:

```csharp
int shapeCount = firstPage.Paragraphs.Count;
Console.WriteLine($"Page 1 now contains {shapeCount} paragraph objects.");
```

Eklemeden sonra sayım bir artmışsa, işlem başarılı demektir.

---

## Conclusion

Artık C# kullanarak **PDF'ye dikdörtgen ekle**me konusunda bilgi sahibisiniz. Öğreticide bir belgeyi yükleme, sınırları tanımlama, bir dikdörtgen şekli oluşturma, sayfaya ekleme ve sonucu kaydetme adımları ele alındı. Ayrıca çoklu sayfalarla nasıl çalışılacağını, yaygın hatalardan nasıl kaçınılacağını ve gelişmiş stil uygulamalarını gördünüz.

Sonraki adımda, **how to draw shape in PDF C#** konusunu daireler, çokgenler veya serbest biçimli yollar için keşfedin ve şekilleri metin ve görsellerle birleştirerek tam özellikli PDF raporları oluşturmayı öğrenin.

Kodlamanın tadını çıkarın!

## What Should You Learn Next?

Aşağıdaki öğreticiler, bu kılavuzda gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini ustalaşmanıza ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak tam çalışan kod örnekleri ve adım adım açıklamalar içerir.

- [How to Add Page Stamps in PDFs Using Aspose.PDF for .NET | Watermarks & Backgrounds Guide](/pdf/english/net/watermarks-backgrounds/implement-page-stamps-aspose-pdf-dotnet/)
- [How to Add an Image Stamp to a PDF Using Aspose.PDF for .NET: A Comprehensive Guide](/pdf/english/net/images-graphics/add-image-stamp-pdf-aspose-dotnet/)
- [How to Add a Rotating Image Watermark to PDFs Using Aspose.PDF for .NET](/pdf/english/net/watermarks-backgrounds/add-rotating-image-watermark-aspose-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}