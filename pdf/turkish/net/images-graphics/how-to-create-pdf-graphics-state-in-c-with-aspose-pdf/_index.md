---
category: general
date: 2026-11-16
description: Aspose.Pdf kullanarak C#'de PDF grafik durumunu nasıl oluşturacağınızı
  öğrenin. Bu rehber opaklık, karıştırma modu ve tam kod örneğini kapsar.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create pdf graphics state
- Aspose.Pdf ExtGState
- PDF opacity
- C# PDF manipulation
- PDF blend mode
- Aspose.Pdf graphics state
language: tr
lastmod: 2026-11-16
og_description: Aspose.Pdf ile C#'ta PDF grafik durumunu oluşturun. Opaklığı ve karışım
  modunu programlı olarak ayarlamak için bu kapsamlı öğreticiyi izleyin.
og_image_alt: Illustration of how to create PDF graphics state with Aspose.Pdf in
  C#
og_title: C#'ta PDF grafik durumunu oluşturma – adım adım Aspose.Pdf rehberi
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Learn how to create PDF graphics state in C# using Aspose.Pdf. This
    guide covers opacity, blend mode, and full code example.
  headline: How to create PDF graphics state in C# with Aspose.Pdf
  type: TechArticle
tags:
- Aspose.Pdf
- C#
- PDF
title: C# ve Aspose.Pdf ile PDF grafik durumunu nasıl oluşturulur
url: /tr/net/images-graphics/how-to-create-pdf-graphics-state-in-c-with-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# ile Aspose.Pdf kullanarak PDF grafik durumu nasıl oluşturulur

Bir .NET projesinde **PDF grafik durumu** oluşturmanız gerekiyorsa, bu öğretici Aspose.Pdf ile bunu tam olarak nasıl yapacağınızı gösterir. Opaklığı kontrol etmek, karışım modunu değiştirmek veya özel bir grafik durumunu sayfalar arasında yeniden kullanmak istiyorsanız, aşağıdaki adımlar eksiksiz, çalıştırmaya hazır bir çözüm sunar.

Bu kılavuzda sayfa kaynaklarına nasıl erişileceğini, bir **ExtGState** girdisi eklemeyi ve değişiklikleri yeni bir dosyaya nasıl kaydedeceğinizi öğreneceksiniz. Örnek Aspose.Pdf 23.12 (veya daha yeni) sürümüyle çalışır ve .NET 6+ hedefler, ancak kavramlar daha eski sürümler için de geçerlidir.

## Gereksinimler

Başlamadan önce şunların yüklü olduğundan emin olun:

* .NET 6 SDK yüklü Visual Studio 2022 (veya herhangi bir C# IDE).  
* Aspose.Pdf for .NET lisansı ya da geçici bir değerlendirme anahtarı.  
* Koddaki yolu referans alabileceğiniz bir klasörde bulunan `input.pdf` adlı bir PDF dosyası.  

`Aspose.Pdf` dışındaki ek NuGet paketlerine ihtiyaç yoktur.

## Öğrenecekleriniz

* Mevcut bir PDF belgesinin yüklenmesi.  
* İlk sayfanın kaynak sözlüğüne (resources dictionary) ulaşılması.  
* Çizgi opaklığı (`CA`), dolgu opaklığı (`ca`) ve karışım modu (`BM`) tanımlayan yeni bir grafik durumu sözlüğünün oluşturulması.  
* Yeni grafik durumunun **ExtGState** koleksiyonuna özel bir ad (`GS0`) ile eklenmesi.  
* Güncellenen PDF’nin kaydedilmesi, böylece sonraki çizim komutları yeni durumu referans alabilir.

Bu öğreticinin sonunda **PDF grafik durumu** nesnelerini programatik olarak oluşturabilecek ve herhangi bir çizim işleminde yeniden kullanabilecek duruma geleceksiniz.

## Adım 1: Projeyi kurun ve ad alanlarını içe aktarın

Yeni bir konsol uygulaması oluşturun (veya kodu mevcut bir projeye entegre edin). Aspose.Pdf referansını ekleyin ve gerekli ad alanlarını içe aktarın:

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Operators;
using Aspose.Pdf.Generator;
```

> **İpucu:** Ücretsiz değerlendirme sürümünü kullanıyorsanız, belgeyi yüklemeden önce `Aspose.Pdf.License license = new Aspose.Pdf.License(); license.SetLicense("Aspose.Pdf.lic");` satırını ekleyerek filigran mesajlarından kaçının.

## Adım 2: PDF belgesini yükleyin

Dosyanın açılması oldukça basittir. `Document` sınıfı tüm PDF’i temsil eder ve sayfalara ve kaynaklara erişim sağlar.

```csharp
// Step 2: Load the PDF document
string inputPath = @"YOUR_DIRECTORY\input.pdf";

using (var document = new Document(inputPath))
{
    // All subsequent steps run inside this using block
```

Kodun bir `using` bloğu içinde yer alması, dosya tutamacının işlem sonrası serbest bırakılmasını garantiler; bu, üretim hizmetlerinde **C# PDF manipulation** için kritiktir.

## Adım 3: İlk sayfanın kaynak sözlüğünü alın

Her PDF sayfasının *Resources* sözlüğü, yazı tipleri, görseller ve grafik durumlarını depolar. Bu yapıyı düzenlemek için bir `DictionaryEditor` gerekir.

```csharp
    // Step 3: Get the first page and its resources dictionary
    var page = document.Pages[1];
    var resourcesEditor = new DictionaryEditor(page.Resources);
```

PDF zaten bir `ExtGState` girdisi içeriyorsa, `resourcesEditor["ExtGState"]` onu döndürür; aksi takdirde, ilk girişi eklediğimizde Aspose.Pdf bizim için boş bir sözlük oluşturur.

## Adım 4: ExtGState sözlüğüne erişin veya oluşturun

**ExtGState** sözlüğü, adlandırılmış grafik durumu nesnelerini tutar. Mevcut birini alabilir ya da yeni bir kapsayıcı oluşturabilirsiniz.

```csharp
    // Step 4: Access (or create) the ExtGState dictionary within the resources
    var extGState = resourcesEditor["ExtGState"].ToCosPdfDictionary();
```

`ExtGState` mevcut değilse, `resourcesEditor["ExtGState"]` otomatik olarak yeni bir boş sözlük döndürür; bu sayede kod herhangi bir PDF’de çalışır.

## Adım 5: Yeni grafik durumu sözlüğünü oluşturun

Bir grafik durumu, belirli anahtarları içeren bir `CosPdfDictionary`’dir:

* `CA` – çizgi (stroke) opaklığı (0‑1)  
* `ca` – dolgu (fill) opaklığı (0‑1)  
* `BM` – karışım modu (`Normal`, `Multiply` vb.)

Boş bir sözlük oluşturup dolduruyor ve ardından `ExtGState`’e ekliyoruz.

```csharp
    // Step 5: Create a new graphics state dictionary with desired parameters
    var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(document);
    var parameters = new[]
    {
        new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),   // Stroke opacity (fully opaque)
        new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // Fill opacity (50% transparent)
        new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // Blend mode
    };

    foreach (var p in parameters)
        newGraphicsState.Add(p);
```

`0.5` değerini `0` ile `1` arasında istediğiniz bir değere değiştirebilir, `"Normal"` yerine `"Multiply"` yazarak farklı bir **PDF blend mode** seçebilirsiniz. Bu esneklik, **Aspose.Pdf graphics state** yönetiminde özelleştirilmiş bir grafik durumu oluşturmayı güçlü bir teknik haline getirir.

## Adım 6: Grafik durumunu bir adla kaydedin

PDF içerik akışları grafik durumlarını adlarıyla referans alır. Burada `GS0` kullandık, ancak benzersiz herhangi bir ad yeterlidir.

```csharp
    // Step 6: Add the new graphics state to the ExtGState dictionary with a name (e.g., GS0)
    extGState.Add("GS0", newGraphicsState);
```

Birden fazla durum gerekiyorsa, farklı parametrelerle oluşturma adımını tekrarlayın ve `GS1`, `GS2` gibi adlarla ekleyin. Bu desen, farklı katmanlarda değişik opaklık veya karışım ayarları gerektiren karmaşık belgeler için iyi ölçeklenir.

## Adım 7: Değiştirilen PDF’yi kaydedin

Son olarak, güncellenen belgeyi yeni bir dosyaya yazın. Orijinali korumak hata ayıklamayı kolaylaştırır.

```csharp
    // Step 7: Save the updated PDF document
    string outputPath = @"YOUR_DIRECTORY\output.pdf";
    document.Save(outputPath);
}
```

Çalıştırdıktan sonra `output.pdf` içinde `GS0` adlı bir `ExtGState` girdisi bulunur. Sonraki herhangi bir çizim operatörü, `gs` operatörüyle (ör. içerik akışında `GS0 gs`) bu durumu referans alabilir.  

> **Neden Önemli:** Tekrar kullanılabilir bir grafik durumu oluşturarak, her çizim komutu için opaklık ve karışım ayarlarını tekrarlamaktan kaçınır, bu da performans ve bakım kolaylığı sağlar.

## Yeni grafik durumunu bir içerik akışında kullanma (isteğe bağlı)

Etkisini hemen görmek istiyorsanız, az önce oluşturduğumuz durumu kullanan basit bir dikdörtgen ekleyebilirsiniz:

```csharp
using (var document = new Document(outputPath))
{
    var page = document.Pages[1];
    var content = page.Contents[1]; // Get the first content stream

    // Insert graphics state selection and a semi‑transparent rectangle
    var operators = new List<Operator>
    {
        new Operator("GS0", "gs"),                     // Select our custom graphics state
        new Operator("0.5", "w"),                      // Set line width (optional)
        new Operator("100", "100", "200", "150", "re"), // Rectangle (x, y, width, height)
        new Operator("B")                              // Stroke the rectangle
    };

    foreach (var op in operators)
        content.Operators.Add(op);

    document.Save(@"YOUR_DIRECTORY\final_output.pdf");
}
```

Dikdörtgen, dolgu opaklığı %50 iken çizgi tamamen opak olarak çizilir; bu, **create PDF graphics state** sözlüğünde tanımlandığı gibi çalışır.

## Yaygın hatalar ve nasıl önlenir

| Issue | Why it happens | Fix |
|-------|----------------|-----|
| `ExtGState` entry not found | Some PDFs omit the dictionary entirely. | The `DictionaryEditor` automatically creates it when you add the first entry, so no extra check is needed. |
| Opacity values > 1 or < 0 | PDF spec limits opacity to the range `[0,1]`. | Clamp values before creating `CosPdfNumber`. |
| Blend mode typo | PDF blend mode names are case‑sensitive. | Use exact names like `"Normal"`, `"Multiply"`, `"Screen"`. |
| License watermark | Evaluation version adds a watermark on the first page. | Apply a valid license file before opening the document. |

Bu kenar durumlarını ele alarak **create PDF graphics state** uygulamanızın farklı PDF kaynaklarıyla güvenilir çalışmasını sağlarsınız.

## Tam, çalıştırılabilir örnek

Aşağıda kopyalayıp yapıştırarak çalıştırabileceğiniz, bağımsız bir program yer alıyor. `YOUR_DIRECTORY` kısmını makinenizdeki gerçek klasör yolu ile değiştirin.

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Generator;

class Program
{
    static void Main()
    {
        // Optional: apply license to remove evaluation watermark
        // var license = new Aspose.Pdf.License();
        // license.SetLicense("Aspose.Pdf.lic");

        string inputPath = @"YOUR_DIRECTORY\input.pdf";
        string outputPath = @"YOUR_DIRECTORY\output.pdf";

        using (var document = new Document(inputPath))
        {
            // 1️⃣ Get first page and its resources
            var page = document.Pages[1];
            var resourcesEditor = new DictionaryEditor(page.Resources);

            // 2️⃣ Access (or create) ExtGState dictionary
            var extGState = resourcesEditor["ExtGState"].ToCosPdfDictionary();

            // 3️⃣ Build new graphics state
            var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(document);
            var parameters = new[]
            {
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),   // Stroke opacity
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // Fill opacity
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // Blend mode
            };
            foreach (var p in parameters) newGraphicsState.Add(p);

            // 4️⃣ Register the state with a name (GS0)
            extGState.Add("


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Create custom graphics state in PDF using Aspose.Pdf](/pdf/english/net/programming-with-operators/create-custom-graphics-state-in-pdf-using-aspose-pdf/)
- [Add graphics state to PDF using Aspose.PDF for .NET (C#)](/pdf/english/net/programming-with-operators/how-to-add-graphics-state-pdf-using-aspose-pdf-in-c/)
- [How to create empty graphics state in a PDF with C#](/pdf/english/net/programming-with-operators/how-to-create-empty-graphics-state-in-a-pdf-with-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}