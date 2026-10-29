---
category: general
date: 2026-08-14
description: Aspose.Pdf kullanarak C#'te boş PDF sözlüğü oluşturun – ExtGState koleksiyonuna
  bir grafik durumu eklemeyi ve PDF'leri programlı olarak değiştirmeyi öğrenin.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create empty PDF dictionary
- Aspose.Pdf Document
- PDF graphics state
- ExtGState dictionary
- CosPdfDictionary usage
language: tr
lastmod: 2026-08-14
og_description: Aspose.Pdf ile C#’ta boş PDF sözlüğü oluşturun. PDF’nin ExtGState
  koleksiyonuna özel bir grafik durumu eklemek için bu kapsamlı kılavuzu izleyin.
og_image_alt: Screenshot showing C# code that creates an empty PDF dictionary with
  Aspose.Pdf
og_title: C#'ta boş PDF sözlüğü oluşturma – Aspose.Pdf adım adım rehberi
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: Create empty PDF dictionary in C# using Aspose.Pdf – learn how to add
    a graphics state to the ExtGState collection and modify PDFs programmatically.
  headline: Create empty PDF dictionary in C# with Aspose.Pdf
  type: TechArticle
- description: Create empty PDF dictionary in C# using Aspose.Pdf – learn how to add
    a graphics state to the ExtGState collection and modify PDFs programmatically.
  name: Create empty PDF dictionary in C# with Aspose.Pdf
  steps:
  - name: Create a new **Console App** project in Visual Studio.
    text: Create a new **Console App** project in Visual Studio.
  - name: 'Open the **NuGet Package Manager** and install `Aspose.Pdf`:'
    text: 'Open the **NuGet Package Manager** and install `Aspose.Pdf`:'
  - name: 'Add the following `using` directives at the top of `Program.cs`:'
    text: 'Add the following `using` directives at the top of `Program.cs`:'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Aspose.Pdf ile C#’ta boş PDF sözlüğü oluştur
url: /tr/net/programming-with-operators/create-empty-pdf-dictionary-in-c-with-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Boş PDF sözlüğü oluşturma C# ile Aspose.Pdf

PDF dosyalarıyla çalışırken **create empty PDF dictionary** nesneleri oluşturmanız gerekiyorsa, bu kılavuz C# ve Aspose.Pdf kütüphanesini kullanarak bunu tam olarak nasıl yapacağınızı gösterir. İster özel bir grafik durumu oluşturuyor olun, yeni bir kaynak ekliyor olun ya da daha sonra kullanmak üzere bir şablon hazırlıyor olun, aşağıdaki adımlar size eksiksiz, çalıştırılabilir bir çözüm sunar.

PDF'yi nasıl yükleyeceğinizi, ilk sayfanın kaynak sözlüğüne nasıl erişeceğinizi, yepyeni bir `CosPdfDictionary` oluşturacağınızı ve bunu `ExtGState` koleksiyonuna nasıl ekleyeceğinizi öğreneceksiniz. Öğreticinin sonunda yeni oluşturulan sözlüğü içeren çalışan bir `output.pdf` elde edeceksiniz.

## Önkoşullar

- .NET 6.0 veya daha yenisi (kod ayrıca .NET Framework 4.6+ ile de çalışır)
- Visual Studio 2022 veya tercih ettiğiniz herhangi bir C# IDE
- Aspose.Pdf for .NET lisansı (veya geçici bir değerlendirme anahtarı)
- **input.pdf** adlı örnek bir PDF, kontrol ettiğiniz bir klasöre yerleştirilmiş (klasör yolu `dataDir` olarak kullanılacak)

Ek bir NuGet paketi `Aspose.Pdf` dışında gerekli değildir.

## Adım 1: Projeyi kurun ve Aspose.Pdf referansını ekleyin

1. Visual Studio'da yeni bir **Console App** projesi oluşturun.  
2. **NuGet Package Manager**'ı açın ve `Aspose.Pdf` paketini yükleyin:

   ```bash
   dotnet add package Aspose.Pdf
   ```

3. `Program.cs` dosyasının en üstüne aşağıdaki `using` yönergelerini ekleyin:

   ```csharp
   using Aspose.Pdf;
   using Aspose.Pdf.Text;
   using Aspose.Pdf.Operators;
   using Aspose.Pdf.Facades;
   using Aspose.Pdf.InteractiveFeatures;
   using Aspose.Pdf.Xmp;
   using Aspose.Pdf.Operators.Filters;
   using Aspose.Pdf.Operators.Gfx;
   ```

   *Neden bu ad alanları?* `Aspose.Pdf` temel `Document` sınıfını içerirken, `Aspose.Pdf.Operators.Gfx` **create empty PDF dictionary** yapılarına ihtiyaç duyulan `CosPdfDictionary`, `CosPdfNumber` ve ilgili düşük seviyeli PDF nesnelerini sağlar.

## Adım 2: Kaynak PDF'yi yükleyin

İlk işlem, mevcut PDF dosyasını bir `Document` örneğine yüklemektir. Bu, tüm sayfalara, kaynaklara ve düşük seviyeli sözlüklere erişmenizi sağlar.

```csharp
// Step 2: Load the PDF document
string dataDir = @"C:\MyPdfFolder\";               // Change to your folder
using var pdfDocument = new Document(dataDir + "input.pdf");
```

*Açıklama*: `Document` dosyayı belleğe okur ve iç yapılarını hazırlar. `using` ifadesi, işleme tamamlandıktan sonra dosya tutamacının serbest bırakılmasını sağlar.

## Adım 3: İlk sayfanın kaynak sözlüğüne erişin

Her PDF sayfasının, yazı tipleri, görseller, ExtGState nesneleri ve diğer ortak kaynakları gruplandıran bir **Resources** sözlüğü vardır. Yeni bir grafik durumu eklemek için bu sözlüğü düzenlememiz gerekir.

```csharp
// Step 3: Get the first page and its Resources dictionary
Page firstPage = pdfDocument.Pages[1];                     // PDF pages are 1‑based
DictionaryEditor resourcesEditor = new DictionaryEditor(firstPage.Resources);
```

`DictionaryEditor`, bir PDF sözlüğünü C# `Dictionary<string, object>` gibi kullanmanıza olanak tanıyan yardımcı bir sınıftır.

## Adım 4: ExtGState koleksiyonunu alın (veya oluşturun)

`ExtGState`, opaklık, karışım modu ve çizgi kalınlığı gibi grafik durumu nesnelerini tutar. Kaynak PDF zaten bir `ExtGState` girdisi içeriyorsa, onu yeniden kullanırız; aksi takdirde yeni bir boş sözlük oluştururuz.

```csharp
// Step 4: Ensure an ExtGState dictionary exists
CosPdfDictionary extGStateDict;
if (resourcesEditor.ContainsKey("ExtGState"))
{
    extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
}
else
{
    // Create a brand‑new ExtGState dictionary and add it to Resources
    extGStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
    resourcesEditor["ExtGState"] = extGStateDict;
}
```

*Neden bu kontrol?* Bazı PDF'ler `ExtGState` girdisini tamamen atlayabilir. Her iki durumu da ele alarak, öğretici herhangi bir giriş dosyası için dayanıklı kalır.

## Adım 5: Yeni bir grafik durumu için **Create empty PDF dictionary** oluşturun

Şimdi gerçekten **create empty PDF dictionary** nesnelerini oluşturuyoruz; bu nesneler grafik durumu parametrelerini tanımlar. Sözlük başlangıçta boştur ve gerekli anahtarları ekleriz:

```csharp
// Step 5: Build a new graphics state dictionary (empty PDF dictionary + entries)
CosPdfDictionary newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

// Stroke opacity (CA) – 1 means fully opaque strokes
newGraphicsState.Add("CA", new CosPdfNumber(1));

// Fill opacity (ca) – 0.5 makes semi‑transparent fills
newGraphicsState.Add("ca", new CosPdfNumber(0.5));

// Blend mode (BM) – "Normal" is the default compositing mode
newGraphicsState.Add("BM", new CosPdfName("Normal"));
```

### Her bir girdinin yaptığı şey

| Anahtar | Tür | Anlam |
|-----|------|---------|
| **CA** | `CosPdfNumber` | Çizgi opaklığı (aralık 0‑1). |
| **ca** | `CosPdfNumber` | Dolgu opaklığı (aralık 0‑1). |
| **BM** | `CosPdfName`   | Karışım modu; `"Normal"` en yaygın olanıdır. |

Bir **empty PDF dictionary** ile başladığımız için, eklenen girdiler üzerinde tam kontrol sahibiyiz. İhtiyaç duyduğunuzda bu sözlüğü `LW` (çizgi kalınlığı) veya `LC` (çizgi ucu) gibi ek grafik durumu parametreleriyle genişletebilirsiniz.

## Adım 6: Yeni grafik durumunu ExtGState içine ekleyin

`ExtGState` sözlüğü, her girdinin bir ad (ör. `GS0`, `GS1`) ile tanımlandığı bir harita gibi çalışır. Yeni oluşturduğumuz sözlüğü benzersiz bir anahtar altında ekliyoruz.

```csharp
// Step 6: Add the graphics state to the ExtGState collection
extGStateDict.Add("GS0", newGraphicsState);
```

Birden fazla durum eklemeyi planlıyorsanız, ad çakışmalarını önlemek için soneki (`GS1`, `GS2`, …) artırın.

## Adım 7: Değiştirilen PDF'yi kaydedin

Son olarak, değişiklikleri diske geri yazın. `Save` yöntemi güncellenen sözlükleri otomatik olarak serileştirir.

```csharp
// Step 7: Persist the changes
pdfDocument.Save(dataDir + "output.pdf");
```

Herhangi bir PDF görüntüleyicide `output.pdf` dosyasını açın ve **Resources → ExtGState** girdisini inceleyin (çoğu görüntüleyici bunu gizler, ancak Adobe Acrobat Preflight veya PDF‑Tron gibi araçlar gösterebilir). Tanımladığınız opaklık ve karışım modu değerlerini içeren bir `GS0` girdisi görmelisiniz.

## Tam çalışan örnek

Tüm parçaları bir araya getirerek, `Program.cs` içine kopyalayıp çalıştırabileceğiniz tam program aşağıdadır:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Operators.Gfx;

class Program
{
    static void Main()
    {
        // -----------------------------------------------------------------
        // 1️⃣ Load the PDF document
        // -----------------------------------------------------------------
        string dataDir = @"C:\MyPdfFolder\"; // <-- change to your folder
        using var pdfDocument = new Document(dataDir + "input.pdf");

        // -----------------------------------------------------------------
        // 2️⃣ Access the first page’s Resources dictionary
        // -----------------------------------------------------------------
        Page firstPage = pdfDocument.Pages[1];
        var resourcesEditor = new DictionaryEditor(firstPage.Resources);

        // -----------------------------------------------------------------
        // 3️⃣ Retrieve or create the ExtGState dictionary
        // -----------------------------------------------------------------
        CosPdfDictionary extGStateDict;
        if (resourcesEditor.ContainsKey("ExtGState"))
        {
            extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
        }
        else
        {
            extGStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            resourcesEditor["ExtGState"] = extGStateDict;
        }

        // -----------------------------------------------------------------
        // 4️⃣ **Create empty PDF dictionary** for a new graphics state
        // -----------------------------------------------------------------
        var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
        newGraphicsState.Add("CA", new CosPdfNumber(1));          // Stroke opacity
        newGraphicsState.Add("ca", new CosPdfNumber(0.5));        // Fill opacity
        newGraphicsState.Add("BM", new CosPdfName("Normal"));    // Blend mode

        // -----------------------------------------------------------------
        // 5️⃣ Add the graphics state to ExtGState
        // -----------------------------------------------------------------
        extGStateDict.Add("GS0", newGraphicsState);

        // -----------------------------------------------------------------
        // 6️⃣ Save the modified PDF
        // -----------------------------------------------------------------
        pdfDocument.Save(dataDir + "output.pdf");

        Console.WriteLine("PDF saved with new empty dictionary at: " + dataDir + "output.pdf");
    }
}
```

**Beklenen çıktı** – Konsol bir onay satırı yazdırır ve `output.pdf` `ExtGState` altında yeni `GS0` girdisini içerir. `GS0`'a başvuran bir sayfayı (ör. içerik akışı operatörü `gs` ile) renderladığınızda, çizgiler tamamen opak, dolgu ise %50 şeffaf olacaktır.

## Yaygın sorular ve kenar‑durumları ele alma

| Soru | Cevap |
|----------|--------|
| *PDF'nin birden fazla sayfası olsaydı ne olur?* | Örnek ilk sayfayı hedefler (`Pages[1]`). Tüm sayfaları etkilemek için `pdfDocument.Pages` üzerinde döngü yapın ve her sayfanın kaynakları için adım 3‑5'i tekrarlayın. |
| *Zaten “GS0” adlı bir ExtGState girdisine sahip bir sayfaya sözlüğü ekleyebilir miyim?* | Evet, ancak mevcut girdiyi üzerine yazmamak için farklı bir anahtar (`GS1`, `GS2`, …) kullanmanız gerekir. |
| *Kaydetmeden sonra sözlüğü değiştirmek güvenli mi?* | `Save` metodunu çağırdığınızda, bellek içindeki temsil dosyadan ayrılır. Gerektiğinde `Document` nesnesini düzenlemeye devam edebilir ve tekrar `Save` çağırabilirsiniz. |
| *Aspose.Pdf'i kullanmak için lisansa ihtiyacım var mı?* |  |

## Sonraki Öğrenmeniz Gerekenler

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak adım adım açıklamalar içeren eksiksiz çalışan kod örnekleri sunar.

- [Aspose.PDF for .NET ile PDF'lerde Kesikli Çizgiler Oluşturma: Adım Adım Kılavuz](/pdf/english/net/images-graphics/create-dashed-lines-aspose-pdf-net/)
- [Aspose.PDF .NET ile PDF'lerden Grafikleri Kaldırma: Tam Kılavuz](/pdf/english/net/images-graphics/remove-graphics-aspose-pdf-net/)
- [Aspose.PDF for .NET ile Çok Katmanlı PDF'ler Oluşturma: Kapsamlı Kılavuz](/pdf/english/net/advanced-features/create-multi-layer-pdfs-aspose-pdf-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}