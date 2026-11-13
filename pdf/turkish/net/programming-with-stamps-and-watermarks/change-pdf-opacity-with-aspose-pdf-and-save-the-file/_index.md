---
category: general
date: 2026-11-12
description: Aspose.Pdf kullanarak PDF opaklığını nasıl değiştireceğinizi, şeffaflık
  eklemeyi, harmanlama modunu ayarlamayı ve C#'ta değiştirilmiş PDF'yi kaydetmeyi
  öğrenin.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- change PDF opacity
- how to add transparency
- save modified PDF
- how to set blend mode
- set fill opacity
language: tr
lastmod: 2026-11-12
og_description: Aspose.Pdf ile PDF opaklığını değiştirin, şeffaflık eklemeyi, harmanlama
  modunu ayarlamayı öğrenin ve C#'ta değiştirilmiş PDF dosyalarını kaydedin.
og_image_alt: Screenshot of a PDF page with altered opacity using Aspose.Pdf
og_title: Aspose.Pdf ile PDF saydamlığını değiştirin – şeffaflık ekleyin ve kaydedin
schemas:
- author: Aspose
  dateModified: '2026-11-12'
  description: Learn how to change PDF opacity using Aspose.Pdf, add transparency,
    set blend mode, and save modified PDF in C#.
  headline: Change PDF opacity with Aspose.Pdf and save the file
  type: TechArticle
- description: Learn how to change PDF opacity using Aspose.Pdf, add transparency,
    set blend mode, and save modified PDF in C#.
  name: Change PDF opacity with Aspose.Pdf and save the file
  steps:
  - name: Load the PDF document
    text: Start by creating a `Document` instance that points to your source file.
      The constructor reads the entire PDF into memory, allowing you to manipulate
      its internal objects.
  - name: Access the first page’s resources
    text: Each PDF page stores a *resource dictionary* that holds objects such as
      fonts, images, and graphics states. You need to edit this dictionary to inject
      a new `ExtGState` entry.
  - name: Ensure an ExtGState dictionary exists
    text: The `ExtGState` dictionary holds custom graphics states. If it does not
      exist, the code creates one automatically.
  - name: Define a new graphics state (ExtGState)
    text: A graphics state defines how drawing operations behave. The following dictionary
      sets stroke opacity (`CA`), fill opacity (`ca`), and blend mode (`BM`).
  - name: Register the graphics state in the resource dictionary
    text: Give the new state a name (e.g., `GS0`) and add it to the `ExtGState` dictionary.
      This name will be referenced later in the page content stream.
  - name: Apply the graphics state to page content
    text: To actually see the opacity effect, insert the `/GS0 gs` operator before
      the drawing commands you want to affect. The example below draws a semi‑transparent
      rectangle.
  - name: Save the modified PDF
    text: Finally, write the updated document to disk. The `Save` method overwrites
      the target file or creates a new one if it does not exist.
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Aspose.Pdf ile PDF şeffaflığını değiştirin ve dosyayı kaydedin
url: /tr/net/programming-with-stamps-and-watermarks/change-pdf-opacity-with-aspose-pdf-and-save-the-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Pdf ile PDF Opaklığını Değiştirin ve Dosyayı Kaydedin

Bir belgede **PDF opaklığını değiştirmek** istiyorsanız, Aspose.Pdf hem çizgi hem de dolgu şeffaflığını ayarlamak için basit bir API sunar. Bu öğreticide **şeffaflık nasıl eklenir**, **karıştırma modu nasıl ayarlanır** ve **değiştirilmiş PDF** dosyalarının sadece birkaç C# kod satırıyla nasıl kaydedileceği gösterilmektedir.

Mevcut bir PDF'yi yüklemekten yeni bir grafik durumunu tanımlamaya ve değişiklikleri kalıcı hale getirmeye kadar her adımı öğreneceksiniz. Bu rehberin sonunda şunları yapabilirsiniz:

* Vektör grafiklerin veya görüntülerin görünürlüğünü azaltın.
* *Normal* veya *Multiply* gibi özel bir karıştırma modu uygulayın.
* Diğer içeriği kaybetmeden güncellenmiş dosyayı dışa aktarın.

Tek ön koşul, çalışan bir .NET geliştirme ortamı ve Aspose.Pdf kütüphanesine (versiyon 23.9 veya daha yeni) referansdır. Harici araçlara gerek yoktur.

## Ön Koşullar

| Gereksinim | Neden Önemli |
|-------------|----------------|
| .NET 6.0 SDK or later | En son Aspose.Pdf API'leriyle uyumluluğu garanti eder. |
| Aspose.Pdf for .NET NuGet package | `Document`, `CosPdfDictionary` ve kodda kullanılan ilgili sınıfları sağlar. |
| A PDF file to edit (e.g., `input.pdf`) | Opaklık değişiklikleri için kaynak olarak hizmet eder. |

Install the NuGet package with:

```bash
dotnet add package Aspose.Pdf
```

## Aspose.Pdf ile PDF Opaklığını Değiştirin

### Adım 1: PDF belgesini yükleyin

Öncelikle kaynak dosyanıza işaret eden bir `Document` örneği oluşturun. Yapıcı, tüm PDF'yi belleğe okur ve iç nesnelerini manipüle etmenize olanak tanır.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Operators;
using Aspose.Pdf.XObjects;
using Aspose.Pdf.Facades;

// Load the existing PDF
var pdfDoc = new Document(@"YOUR_DIRECTORY\input.pdf");
```

> **Bu adım neden?** Dosyanın yüklenmesi, manipüle edilebilir bir nesne modeli oluşturur. Sonraki tüm değişiklikler bu bellek içi temsilde gerçekleşir ve orijinal dosya, açıkça kaydedene kadar dokunulmaz kalır.

### Adım 2: İlk sayfanın kaynaklarına erişin

Her PDF sayfası, yazı tipleri, görüntüler ve grafik durumları gibi nesneleri tutan bir *resource dictionary* (kaynak sözlüğü) saklar. Yeni bir `ExtGState` girdisi eklemek için bu sözlüğü düzenlemeniz gerekir.

```csharp
// Retrieve the first page (pages are 1‑based)
var page = pdfDoc.Pages[1];

// The DictionaryEditor simplifies access to the page's resource dictionary
var resourcesEditor = new DictionaryEditor(page.Resources);
```

> **İpucu:** PDF'niz aynı opaklığa ihtiyaç duyan birden fazla sayfa içeriyorsa, bu adımı her sayfa için tekrarlayın veya sayfalar arasında tek bir `ExtGState` paylaşın.

### Adım 3: ExtGState sözlüğünün var olduğundan emin olun

`ExtGState` sözlüğü, özel grafik durumlarını tutar. Eğer yoksa, kod otomatik olarak bir tane oluşturur.

```csharp
// Get or create the ExtGState dictionary
var extGStateDict = resourcesEditor["ExtGState"]?.ToCosPdfDictionary()
                     ?? new CosPdfDictionary(pdfDoc);
resourcesEditor["ExtGState"] = extGStateDict;
```

> **Bu adım neden?** `ExtGState` konteyneri olmadan, yeni bir grafik durumuna referans vermeye çalışmak başarısız olur ve PDF opaklık ayarlarınızı görmezden gelir.

### Adım 4: Yeni bir grafik durumu tanımlayın (ExtGState)

Bir grafik durumu, çizim işlemlerinin nasıl davranacağını tanımlar. Aşağıdaki sözlük, çizgi opaklığını (`CA`), dolgu opaklığını (`ca`) ve karıştırma modunu (`BM`) ayarlar.

```csharp
// Create an empty dictionary for the new graphics state
var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDoc);

// Set desired parameters
var parameters = new[]
{
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),   // Stroke opacity (1 = opaque)
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // Fill opacity (0.5 = 50% transparent)
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // Blend mode
};

foreach (var param in parameters)
    newGraphicsState.Add(param);
```

> **Dolgu opaklığı nasıl ayarlanır:** `ca` girişi, doldurulmuş şekillerin (metin, yollar) opaklığını kontrol eder. Tasarım gereksinimlerinize göre `0` (tamamen şeffaf) ile `1` (tamamen opak) arasında sayısal değeri ayarlayın.

> **Karıştırma modu nasıl ayarlanır:** `BM` girişi, birleştirme algoritmasını seçer. Yaygın değerler `Normal`, `Multiply`, `Screen` ve `Overlay`'dir. Görsel amacınıza uyanı seçin.

### Adım 5: Grafik durumunu kaynak sözlüğüne kaydedin

Yeni duruma bir ad verin (ör. `GS0`) ve `ExtGState` sözlüğüne ekleyin. Bu ad, sayfa içerik akışında daha sonra referans alınacaktır.

```csharp
// Add the graphics state with a symbolic name
extGStateDict.Add("GS0", newGraphicsState);
```

> **Pro ipucu:** Birden fazla durum oluştururken `GS0`, `GS1`, … gibi bir adlandırma kuralı kullanın. Bu, ad çakışmalarını önler ve hata ayıklamayı kolaylaştırır.

### Adım 6: Grafik durumunu sayfa içeriğine uygulayın

Opaklık etkisini gerçekten görmek için, etkilemek istediğiniz çizim komutlarından önce `/GS0 gs` operatörünü ekleyin. Aşağıdaki örnek yarı şeffaf bir dikdörtgen çizer.

```csharp
// Build a content stream that uses the new graphics state
var content = new MemoryStream();
var writer = new StreamWriter(content);

// Activate the graphics state
writer.WriteLine("q");                 // Save graphics state
writer.WriteLine("/GS0 gs");           // Apply custom ExtGState
writer.WriteLine("0.2 0.5 0.8 rg");    // Set fill color (RGB)
writer.WriteLine("100 500 200 100 re"); // Rectangle (x y width height)
writer.WriteLine("f");                 // Fill rectangle
writer.WriteLine("Q");                 // Restore graphics state
writer.Flush();

content.Position = 0;
page.Contents.Add(new ContentStream(content));
```

> **`q` ve `Q` operatörleri neden?** Grafik durum yığınına itme ve çıkarma yaparlar, böylece opaklık değişikliği sadece dikdörtgene ve sayfanın geri kalanına etki etmez.

### Adım 7: Değiştirilmiş PDF'i kaydedin

Son olarak, güncellenmiş belgeyi diske yazın. `Save` yöntemi hedef dosyayı üzerine yazar veya yoksa yeni bir dosya oluşturur.

```csharp
// Persist the changes
pdfDoc.Save(@"YOUR_DIRECTORY\output.pdf");
```

> **Değiştirilmiş PDF'i nasıl kaydedilir:** `Save` çağrısı, yeni `ExtGState` dahil tüm bellek içi değişiklikleri belirtilen yola yazar. Sonucu bir `MemoryStream`'e akıtıp web yanıtları olarak da kullanabilirsiniz.

## Tam Çalışan Örnek

Aşağıda, yukarıda açıklanan tüm adımları içeren tek bir, bağımsız program bulunmaktadır. Bir konsol uygulamasına kopyalayın ve opaklık değişikliğini doğrulamak için çalıştırın.



## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak adım adım açıklamalar içeren tam çalışan kod örnekleri sunar.

- [Değiştirilmiş PDF'i Aspose.Pdf ile kaydetme ve şeffaflık ekleme](/pdf/english/net/document-manipulation/how-to-save-modified-pdf-with-aspose-pdf-and-add-transparenc/)
- [Aspose.PDF kullanarak C#'ta PDF'e şeffaflık ekleme](/pdf/english/net/images-graphics/how-to-add-transparency-to-pdf-using-aspose-pdf-in-c/)
- [Aspose.PDF ile grafik durumu ekleme ve şeffaflığı kontrol etme](/pdf/english/net/images-graphics/how-to-add-graphics-state-pdf-and-control-transparency-with/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}