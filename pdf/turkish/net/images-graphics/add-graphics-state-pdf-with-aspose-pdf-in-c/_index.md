---
category: general
date: 2026-10-07
description: C#'ta Aspose.Pdf kullanarak grafik durumu ekleyerek PDF şeffaflığını
  değiştirin. Özel grafik durumlarını gömmek ve opaklığı kontrol etmek için bu adım
  adım kılavuzu izleyin.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add graphics state pdf
- modify pdf transparency
language: tr
lastmod: 2026-10-07
og_description: Aspose.Pdf ile C#'ta grafik durumu PDF ekleyin. Özel bir grafik durumu
  sözlüğü oluşturarak PDF şeffaflığını nasıl değiştireceğinizi öğrenin.
og_image_alt: Screenshot showing the add graphics state pdf code editor in Visual
  Studio
og_title: Aspose.Pdf ile grafik durumunu PDF'ye ekleyin – PDF şeffaflığını kontrol
  edin
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Add graphics state pdf using Aspose.Pdf in C# to modify PDF transparency.
    Follow this step‑by‑step guide to embed custom graphics states and control opacity.
  headline: Add graphics state pdf with Aspose.Pdf in C#
  type: TechArticle
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: C#'ta Aspose.Pdf ile grafik durumunu PDF'ye ekleyin
url: /tr/net/images-graphics/add-graphics-state-pdf-with-aspose-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Pdf ile C#'ta PDF'e grafik durumu ekleme

Eğer bir belgeye **PDF grafik durumu eklemek** istiyorsanız, bu öğretici Aspose.Pdf for .NET ile bunu nasıl yapacağınızı adım adım gösterir. Rehberin sonunda **PDF şeffaflığını değiştirme** konusunda da bilgi sahibi olacak ve istediğiniz çizim işlemine özel opaklık değerleri uygulayabileceksiniz.

PDF grafik durumlarıyla çalışmak, çizgi kalınlığı, karışım modu ve bu makale için en önemli olan içerik şeffaflığı gibi parametreleri kontrol etmenizi sağlar. Aşağıdaki adımlar, C# konusunda rahat olan ve resmi SDK belgelerini incelemeden çalıştırılabilir bir çözüm arayan geliştiriciler için hazırlanmıştır.

## Öğrenecekleriniz

* `CA`, `ca` ve `BM` girişleriyle yeni bir grafik durumu sözlüğü oluşturup doldurmayı.  
* Bu sözlüğü sayfanın `ExtGState` kaynağına ekleyerek PDF'in tanımasını sağlamayı.  
* `ca` (çizgi) ve `CA` (dolgu) değerlerinin sonraki çizim komutları için **PDF şeffaflığını değiştirme** üzerindeki etkisini.  
* İsim çakışmaları ve sürüm uyumluluğu gibi yaygın tuzaklar ve grafik durumunu ileride genişletmek için ipuçları.

**Önkoşullar**

* .NET 6.0 veya üzeri (kod .NET Framework 4.7+ ile de çalışır).  
* Geçerli bir Aspose.Pdf for .NET lisansı (ücretsiz deneme sürümü test için yeterlidir).  
* Visual Studio 2022 veya tercih ettiğiniz herhangi bir C# IDE.

---

## 1. Adım: Aspose.Pdf for .NET'i Yükleyin

Projeye NuGet paketini ekleyin:

```bash
dotnet add package Aspose.Pdf
```

Paket, daha sonra kullanılacak `Document`, `DictionaryEditor` ve `CosPdfDictionary` sınıflarını içeren `Aspose.Pdf` ad alanını sağlar.

> **Pro ipucu:** Birden çok PDF'i toplu olarak işleme planlıyorsanız, `Program.cs` içinde **License** (lisans) satırını erken ekleyerek değerlendirme filigranından kaçının.

```csharp
// Apply your license (optional for evaluation)
Aspose.Pdf.License license = new Aspose.Pdf.License();
license.SetLicense("Aspose.Pdf.lic");
```

## 2. Adım: Giriş ve çıkış yollarını tanımlayın

SDK'yı mevcut bir PDF (`input.pdf`) ile çalıştırmalı ve değiştirilmiş dosyanın nereye kaydedileceğini (`output.pdf`) belirtmelisiniz.

```csharp
// Define input and output PDF file paths
string inputPath = @"C:\MyPdfs\input.pdf";
string outputPath = @"C:\MyPdfs\output.pdf";
```

> **Neden önemli?** Mutlak yollar kullanmak, SDK'nın yanlış çalışma dizininde dosya aramasını engeller; bu da sıkça karşılaşılan `FileNotFoundException` hatasının önüne geçer.

## 3. Adım: PDF'i açın ve ilk sayfanın kaynaklarını bulun

`ExtGState` sözlüğü, her sayfanın kaynak sözlüğünün içinde yer alır. Basitlik açısından ilk sayfayı düzenleyeceğiz, ancak aynı yaklaşım herhangi bir sayfa indeksi için geçerlidir.

```csharp
using (var pdfDocument = new Aspose.Pdf.Document(inputPath))
{
    // Get the first page (pages are 1‑based)
    var firstPage = pdfDocument.Pages[1];

    // Access the page’s resource dictionary via DictionaryEditor
    var resourcesEditor = new Aspose.Pdf.DictionaryEditor(firstPage.Resources);

    // Retrieve (or create) the ExtGState entry
    var extGStateDict = resourcesEditor["ExtGState"]
        .ToCosPdfDictionary(); // Throws if ExtGState does not exist
```

**Köşe durumu:** Sayfada `ExtGState` girişi yoksa, onu oluşturmanız gerekir:

```csharp
if (!resourcesEditor.ContainsKey("ExtGState"))
{
    var emptyDict = Aspose.Pdf.CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
    resourcesEditor.Add("ExtGState", emptyDict);
    extGStateDict = emptyDict;
}
```

## 4. Adım: Yeni bir grafik durumu sözlüğü oluşturun

Grafik durumu, çizim işlemlerinin nasıl davranacağını tanımlayan anahtar/değer çiftlerinden oluşur. Şeffaflık için üç anahtar gerekir:

| Anahtar | Anlam | Tipik değer |
|---------|-------|-------------|
| `CA` | Dolgu opaklığı (0 = şeffaf, 1 = opak) | `1` (tamamen opak) |
| `ca` | Çizgi (stroke) opaklığı (aynı ölçek) | `0.5` (%50 şeffaf) |
| `BM` | Karışım modu (örn. `Normal`, `Multiply`) | `Normal` |

```csharp
    // Create an empty dictionary that will hold the graphics state
    var newGraphicsState = Aspose.Pdf.CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

    // Populate the dictionary with transparency and blend mode entries
    var graphicsStateEntries = new[]
    {
        new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
            "CA", new Aspose.Pdf.CosPdfNumber(1)),
        new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
            "ca", new Aspose.Pdf.CosPdfNumber(0.5)),
        new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
            "BM", new Aspose.Pdf.CosPdfName("Normal"))
    };

    foreach (var entry in graphicsStateEntries)
        newGraphicsState.Add(entry);
```

**Bu değerler neden?**  
`ca = 0.5` herhangi bir çizgi (çizgi, kenarlık) yolunu %50 şeffaf gösterirken, `CA = 1` dolgu şekillerini tamamen opak bırakır. İhtiyacınız olan **PDF şeffaflığını değiştirme** etkisini elde etmek için her iki sayıyı da ayarlayabilirsiniz.

## 5. Adım: Grafik durumunu ExtGState sözlüğüne ekleyin

Yeni duruma benzersiz bir ad vermelisiniz (ör. `GS0`). Aynı ad zaten mevcutsa, Aspose.Pdf mevcut girişi üzerine yazar ve bu da ona bağlı diğer içeriklerin bozulmasına yol açabilir.

```csharp
    // Add the new graphics state under a custom name
    const string stateName = "GS0";

    // Ensure we don’t clash with an existing entry
    if (extGStateDict.ContainsKey(stateName))
        extGStateDict.Remove(stateName);

    extGStateDict.Add(stateName, newGraphicsState);
```

Artık sayfanın kaynakları `GS0`'ı tanıyor. Bunu gerçekten kullanmak için içerik akışında `gs` operatörüyle (ör. `GS0 gs`) referans vermeniz gerekir. Aspose.Pdf, özel şekiller çizerken ham PDF operatörleri eklemenize izin verir.

## 6. Adım: Değiştirilmiş PDF'i kaydedin

```csharp
    // Persist the changes to a new file
    pdfDocument.Save(outputPath);
}
```

Oluşan `output.pdf`, orijinal ile aynı görsel içeriği taşır, ancak `GS0` seçildiğinde şeffaflık ayarlarınıza uyan sonraki çizim komutları uygulanır.

### Beklenen sonuç

`output.pdf` dosyasını Adobe Acrobat ya da herhangi bir PDF görüntüleyicide açın. `GS0` grafik durumu kullanılarak yeni bir çizgi eklediğinizde (ör. `pdfDocument.Pages[1].Contents.Add(...)`), çizgi yarı şeffaf, dolgu ise opak görünür. Bu, **PDF grafik durumu ekleme** ve **PDF şeffaflığını değiştirme** işlemlerini başarıyla gerçekleştirdiğinizi gösterir.

---

## Tam çalıştırılabilir örnek

Aşağıda, bir konsol uygulamasına kopyalayıp yapıştırabileceğiniz tam program yer alıyor. Lisans yükleme, hata yönetimi ve her adımı açıklayan yorumlar içerir.



## Sonraki Öğrenmeniz Gerekenler

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan ve ilgili konuları derinlemesine ele alan içeriklerdir. Her kaynak, adım adım açıklamalar ve tam çalışan kod örnekleri sunar; böylece API özelliklerini daha iyi kavrayabilir ve projelerinizde alternatif uygulama yaklaşımlarını keşfedebilirsiniz.

- [Add Transparency to PDF with Aspose PDF in C# – Step‑by‑Step Guide](/pdf/english/net/images-graphics/add-transparency-to-pdf-with-aspose-pdf-in-c-step-by-step-gu/)
- [Add Transparency to PDF using Aspose – Complete C# Guide](/pdf/english/net/programming-with-operators/add-transparency-to-pdf-using-aspose-complete-c-guide/)
- [How to Add an Image Stamp to a PDF Using Aspose.PDF for .NET: A Comprehensive Guide](/pdf/english/net/images-graphics/add-image-stamp-pdf-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}