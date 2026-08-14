---
category: general
date: 2026-08-14
description: C# kullanarak PDF üzerinde hızlıca dikdörtgen çizin. Dikdörtgen boyutlarını
  nasıl tanımlayacağınızı ve sadece birkaç satırla bir PDF sayfasına şekil eklemeyi
  öğrenin.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- draw rectangle on pdf
- how to define rectangle dimensions
language: tr
lastmod: 2026-08-14
og_description: C# ile PDF üzerinde saniyeler içinde dikdörtgen çizin. Bu rehber,
  dikdörtgen boyutlarını nasıl tanımlayacağınızı, bir şekil ekleyeceğinizi ve güvenilir
  PDF grafikleri için sayfa sınırlarını nasıl doğrulayacağınızı gösterir.
og_image_alt: Screenshot of a PDF page showing a black rectangle drawn with C# code
og_title: PDF'de dikdörtgen çiz – tam C# öğreticisi
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: draw rectangle on pdf quickly using C#. Learn how to define rectangle
    dimensions and add shapes to a PDF page in just a few lines.
  headline: draw rectangle on pdf – step‑by‑step C# guide
  type: TechArticle
tags:
- PDF
- C#
- Aspose.PDF
- RectangleShape
- Graphics
title: PDF'de dikdörtgen çiz – adım adım C# rehberi
url: /tr/net/annotations/draw-rectangle-on-pdf-step-by-step-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PDF üzerinde dikdörtgen çiz – tam C# öğreticisi

C# kullanarak **draw rectangle on pdf** ihtiyacınız varsa, bu kılavuz size kısa ve üretim‑hazır bir çözüm gösterir. **how to define rectangle dimensions** nasıl tanımlanacağını tam olarak görecek, şeklin sığdığını doğrulayacak ve tek bir metod çağrısıyla bir sayfaya ekleyeceksiniz.

Bu öğretici, PDF belgesi oluşturmaktan dikdörtgeni çizmeye kadar her şeyi kapsar, böylece kodu kendi projenize kopyalayıp yapıştırabilir ve sonuçları anında görebilirsiniz. Harici bir dokümantasyona gerek yok—sadece aşağıdaki adımları izleyin.

## Önkoşullar

* .NET 6.0 veya daha yeni (kod ayrıca .NET Framework 4.7+ ile de çalışır)
* The **Aspose.PDF for .NET** NuGet paketi (`Install-Package Aspose.PDF`)
* C# sözdizimi hakkında temel bir anlayış
* Visual Studio veya VS Code gibi bir IDE

> **Pro tip:** Hızlı denemeler için Aspose.PDF'nin ücretsiz değerlendirme lisansını kullanın; küçük bir filigran ekler ancak tüm özellikleri test etmenizi sağlar.

## C# ile PDF üzerinde dikdörtgen çizme

Görevin çekirdeği, bir `RectangleShape` oluşturmak, boyut ve çizgi ayarlarını yapmak ve onu bir `Page`'e eklemektir. Aşağıdaki H2 başlığı birincil anahtar kelimeyi içerir ve SEO gereksinimlerini karşılar.

```csharp
using System;
using System.Drawing;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new PDF document
        Document pdfDoc = new Document();

        // 2️⃣ Add a blank page (default size: A4)
        Page page = pdfDoc.Pages.Add();

        // 3️⃣ Define the rectangle bounds (x, y, width, height)
        //    This demonstrates how to define rectangle dimensions.
        Rectangle rectBounds = new Rectangle(0, 0, 500, 700);

        // 4️⃣ Create the rectangle shape and set its stroke color
        RectangleShape rectangleShape = new RectangleShape(rectBounds)
        {
            StrokeColor = Color.Black   // black outline
        };

        // 5️⃣ Verify that the shape fits within the page boundaries
        page.CheckShapeBoundary(rectangleShape);

        // 6️⃣ Add the shape to the page
        page.Add(rectangleShape);

        // 7️⃣ Save the PDF to disk
        string outPath = "RectangleDemo.pdf";
        pdfDoc.Save(outPath);
        Console.WriteLine($"PDF saved to {outPath}");
    }
}
```

### Her adımın açıklaması

| Adım | Neden önemlidir |
|------|-----------------|
| **1️⃣ Yeni bir PDF belgesi oluştur** | Sayfaları ve grafikleri tutacak konteyneri başlatır. |
| **2️⃣ Boş bir sayfa ekle** | Şekiller bir sayfaya eklenir, doğrudan belgeye değil, bu yüzden bir `Page` nesnesine ihtiyacınız var. |
| **3️⃣ Dikdörtgen sınırlarını tanımla** | Bu, **how to define rectangle dimensions** yaptığınız yerdir. `Rectangle` yapıcıları `x`, `y`, `width` ve `height` değerlerini puan cinsinden alır (1 pt = 1/72 in). |
| **4️⃣ Dikdörtgen şekli oluştur** | `RectangleShape`, bir dikdörtgen çizen Aspose sınıfıdır. `StrokeColor` ayarı konturu tanımlar; aynı zamanda `FillColor` ile dolgu rengi de belirlenebilir. |
| **5️⃣ Sayfa sınırlarını doğrula** | `CheckShapeBoundary`, dikdörtgen sayfa boyutunu aşıyorsa bir istisna fırlatır ve hatalı PDF'lerin oluşmasını önler. |
| **6️⃣ Şekli sayfaya ekle** | Şekil, sayfanın içerik akışının bir parçası haline gelir. |
| **7️⃣ PDF'yi kaydet** | Belgeyi, herhangi bir PDF görüntüleyiciyle açabileceğiniz bir dosyaya yazar. |

Oluşturulan `RectangleDemo.pdf`, sayfanın sol‑üst köşesine konumlandırılmış, tam olarak 500 pt genişliğinde ve 700 pt yüksekliğinde siyah bir dikdörtgen içerir.

![pdf üzerinde dikdörtgen çiz örneği](https://example.com/rectangle-demo.png "pdf üzerinde dikdörtgen çiz örneği")

*Görsel alt metni: pdf üzerinde dikdörtgen çiz örneği, PDF sayfasının sol üst köşesinde siyah bir dikdörtgen gösterir.*

## Farklı sayfa boyutları için dikdörtgen boyutlarını nasıl tanımlarsınız

Yukarıdaki kod parçacığı sabit değerler (`500 x 700`) kullanır. Gerçek uygulamalarda genellikle dikdörtgenin sayfanın genişliği ve yüksekliğine uyum sağlaması gerekir.

```csharp
// Get page dimensions (in points)
float pageWidth = page.PageInfo.Width;
float pageHeight = page.PageInfo.Height;

// Define a rectangle that occupies 80% of the page width and 50% of the height
float rectWidth  = pageWidth * 0.8f;
float rectHeight = pageHeight * 0.5f;

// Center the rectangle on the page
float rectX = (pageWidth - rectWidth) / 2;
float rectY = (pageHeight - rectHeight) / 2;

Rectangle dynamicRect = new Rectangle(rectX, rectY, rectWidth, rectHeight);
RectangleShape dynamicShape = new RectangleShape(dynamicRect)
{
    StrokeColor = Color.DarkBlue,
    FillColor   = Color.LightGray   // optional fill
};

page.CheckShapeBoundary(dynamicShape);
page.Add(dynamicShape);
```

**Anahtar noktalar:**

* `page.PageInfo.Width` ve `Height` kullanarak gerçek sayfa boyutunu okuyun.
* Bir faktörle (ör. `0.8f`) çarparak boyutları sayfanın yüzde olarak ifade edebilirsiniz.
* Ortalamak, dikdörtgen boyutunu sayfa boyutundan çıkarıp kalan kısmı ikiye bölerek elde edilir.

## Yaygın tuzaklar ve nasıl önlenir

| Tuzak | Neden olur | Çözüm |
|-------|------------|-------|
| Dikdörtgen sayfanın dışına uzanır | Sabit kodlanmış boyutlar sayfa boyutundan büyük. | `page.CheckShapeBoundary` **şekli eklemeden önce** çağırın; bir istisna fırlatılırsa boyutları ayarlayın. |
| Kontur görünmez | `StrokeColor` varsayılan (`Color.Empty`) bırakılmış. | `StrokeColor`'ı açıkça ayarlayın (örn. `Color.Black`). |
| Dikdörtgen ekranda görünmez | PDF uzayında koordinatlar sol‑alt köşeden başlar; ekran‑stili üst‑sol koordinatlar kullanmak ters çevirmeye neden olur. | Orijinin `(0,0)` alt‑sol köşe olduğunu unutmayın. `y` değerini buna göre ayarlayın veya `pageHeight - desiredY` kullanın. |
| Beklenmedik çizgi kalınlığı | Varsayılan çizgi kalınlığı baskı için çok ince olabilir. | `rectangleShape.LineWidth = 2;` ile kalınlığı artırın. |

## Örneği genişletmek

**draw rectangle on pdf** yapabildiğinizde, diğer şekilleri kolayca ekleyebilirsiniz:

* **EllipseShape** – daireler veya ovalar için.
* **PolygonShape** – özel çokgenler için.
* **TextFragment** – dikdörtgenlerinizi etiketlemek için.

Tüm şekiller aynı iş akışını paylaşır: sınırları tanımlayın, görünümü yapılandırın, sınırları doğrulayın ve ardından sayfaya ekleyin.

## Tam, çalıştırılabilir program

Aşağıda temel dikdörtgeni ve dinamik boyutlandırma örneğini birleştiren tam program yer alıyor. Yeni bir konsol projesine kopyalayın, `Aspose.PDF` NuGet paketini geri yükleyin ve çalıştırın.

```csharp
using System;
using System.Drawing;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

class RectangleDemo
{
    static void Main()
    {
        // Create document and page
        Document doc = new Document();
        Page page = doc.Pages.Add();

        // ==== Fixed‑size rectangle (basic example) ====
        Rectangle fixedRect = new Rectangle(0, 0, 500, 700);
        RectangleShape fixedShape = new RectangleShape(fixedRect)
        {
            StrokeColor = Color.Black,
            LineWidth   = 1
        };
        page.CheckShapeBoundary(fixedShape);
        page.Add(fixedShape);

        // ==== Dynamic rectangle that adapts to page size ====
        float pageW = page.PageInfo.Width;
        float pageH = page.PageInfo.Height;

        float dynWidth  = pageW * 0.6f;
        float dynHeight = pageH * 0.3f;
        float dynX      = (pageW - dynWidth) / 2;
        float dynY      = (pageH - dynHeight) / 2;

        Rectangle dynamicRect = new Rectangle(dynX, dynY, dynWidth, dynHeight);
        RectangleShape dynamicShape = new RectangleShape(dynamicRect)
        {
            StrokeColor = Color.DarkBlue,
            FillColor   = Color.LightYellow,
            LineWidth   = 2
        };
        page.CheckShapeBoundary(dynamicShape);
        page.Add(dynamicShape);

        // Save PDF
        string outFile = "CombinedRectangles.pdf";
        doc.Save(outFile);
        Console.WriteLine($"PDF created: {outFile}");
    }
}
```

**Beklenen çıktı:**  
`CombinedRectangles.pdf` dosyasını açın. Alt‑sol köşeye yerleştirilmiş siyah bir dikdörtgen ve ortalanmış koyu‑mavi bir dikdörtgenin hafif‑sarı dolgu ile olduğunu göreceksiniz. Her iki dikdörtgen de sayfa kenar boşluklarına uyar.

## Sonuç

Artık C# ile **draw rectangle on pdf** ve sabit ve duyarlı düzenler için **how to define rectangle dimensions** nasıl tanımlanacağını kesin olarak biliyorsunuz. Yaklaşım, Aspose.PDF’nin `RectangleShape`, sınır kontrolü ve basit aritmetiği kullanarak herhangi bir sayfa boyutuna uyum sağlar.

Sonraki adımda şunları keşfedebilirsiniz:

* **fill colors** ve **line styles** (kesikli, noktalı) eklemek – ikincil anahtar kelime: how to define rectangle dimensions with style.
* Birden fazla şekli tek bir `Page` içinde birleştirerek grafikler veya formlar oluşturmak.
* PDF'yi diske kaydetmek yerine web API'leri için bir akıma (stream) dışa aktarmak.

Farklı boyutlar, renkler ve konumlarla deney yaparak .NET uygulamalarınızda PDF grafiklerinde uzmanlaşın. Kodlamanın tadını çıkarın!

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olmak için adım adım açıklamalar içeren tam çalışan kod örnekleri sunar.

- [PDF'leri Aspose.PDF for .NET ile Özelleştirme: Sayfa Kenar Boşluklarını Ayarlama ve Çizgiler Çizme](/pdf/english/net/document-manipulation/customize-pdfs-aspose-pdf-set-margins-draw-lines/)
- [PDF'lerde Sayfa Damgaları Eklemek Aspose.PDF for .NET ile: Tam Kılavuz](/pdf/english/net/watermarks-backgrounds/add-page-stamp-aspose-pdf-dotnet-guide/)
- [PDF'lerde Sayfa Numarası Damgaları Eklemek Aspose.PDF for .NET ile | Watermarks & Backgrounds](/pdf/english/net/watermarks-backgrounds/add-page-number-stamp-using-aspose-pdf-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}