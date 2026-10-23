---
category: general
date: 2026-10-23
description: Aspose.PDF for .NET kullanarak PDF'ye erişilebilirlik etiketleri ekleyin.
  Aspose.Pdf erişilebilirliği, C# PDF etiketleme ve PDF/UA en iyi uygulamalarını kapsayan
  eksiksiz, adım adım bir kılavuzu izleyin.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add accessibility tags to pdf
- Aspose.Pdf accessibility
- C# PDF tagging
- tagged PDF creation
- PDF accessibility best practices
- PDF document structure
language: tr
lastmod: 2026-10-23
og_description: Aspose.PDF for .NET ile PDF'ye erişilebilirlik etiketleri ekleyin.
  Bu öğreticide, PDF/UA standartlarına uygun etiketli bir PDF nasıl oluşturulacağını
  gösteriyoruz.
og_image_alt: Screenshot of a PDF page with a highlighted accessibility tag overlay
og_title: Aspose.PDF ile PDF'ye erişilebilirlik etiketleri ekleyin – tam C# rehberi
schemas:
- author: Aspose
  dateModified: '2026-10-23'
  description: Add accessibility tags to PDF using Aspose.PDF for .NET. Follow a complete,
    step‑by‑step guide that covers Aspose.Pdf accessibility, C# PDF tagging, and PDF/UA
    best practices.
  headline: How to add accessibility tags to PDF using Aspose.PDF
  type: TechArticle
- description: Add accessibility tags to PDF using Aspose.PDF for .NET. Follow a complete,
    step‑by‑step guide that covers Aspose.Pdf accessibility, C# PDF tagging, and PDF/UA
    best practices.
  name: How to add accessibility tags to PDF using Aspose.PDF
  steps:
  - name: Prepare your development environment
    text: '1. Install the Aspose.PDF NuGet package:'
  - name: Load the source PDF
    text: The first operation opens the existing PDF that you want to tag.
  - name: Create a tagged content element (C# PDF tagging)
    text: A tagged content element describes the logical role of the text (e.g., paragraph,
      heading). Here we create a paragraph tag.
  - name: Define the tag’s location on the page
    text: Accessibility tags also need a geometric location so that the visual layout
      matches the logical structure.
  - name: Add the tag to the first page (tagged PDF creation)
    text: Now attach the tag to a specific page. In this example we use the first
      page, but you can iterate over `pdfDocument.Pages` for multi‑page documents.
  - name: Save the modified PDF
    text: Finally, write the updated document to disk. The saved file now contains
      the accessibility tag.
  - name: Verify the accessibility tags
    text: You can confirm that the tag was added by opening the PDF in a viewer that
      supports structure inspection (e.g., Adobe Acrobat Pro > Tools > Accessibility
      > Read Order). The paragraph should appear in the logical structure tree.
  type: HowTo
tags:
- PDF
- C#
- Accessibility
title: Aspose.PDF kullanarak PDF'ye erişilebilirlik etiketleri nasıl eklenir
url: /tr/net/programming-with-tagged-pdf/how-to-add-accessibility-tags-to-pdf-using-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.PDF kullanarak PDF'ye erişilebilirlik etiketleri ekleme

PDF dosyalarına **erişilebilirlik etiketleri eklemeniz** gerekiyorsa, bu kılavuz Aspose.PDF for .NET ile tam bir çözüm sunar. Hukuki belgeler, e‑kitaplar veya PDF/UA uyumluluğu gerektiren raporlar hazırlıyor olun, ekran okuyucularının yorumlayabileceği etiketli bir PDF oluşturmayı öğreneceksiniz.

Bu öğretici, gerekli geliştirme ortamını, etiketli bir içerik öğesinin oluşturulmasını, etiketin sayfada konumlandırılmasını ve son belgenin kaydedilmesini kapsar. Harici referanslara gerek yoktur; her kod parçacığı kopyalanıp çalıştırılmaya hazırdır.

## İhtiyacınız olanlar

Başlamadan önce şunların yüklü olduğundan emin olun:

- .NET 6.0 veya daha yeni bir sürüm (kod .NET Framework 4.6+ ile de çalışır)
- Aktif bir Aspose.PDF for .NET lisansı (veya geçici bir değerlendirme anahtarı)
- Visual Studio 2022 veya tercih ettiğiniz herhangi bir C# editörü
- Diskte bulunan bir kaynak PDF dosyası (örnek `source.pdf` dosyasını kullanır)

Bu ön koşullar, kodun ek yapılandırma olmadan çalışmasını sağlar.

## PDF'ye erişilebilirlik etiketleri ekleme – adım adım kılavuz

Aşağıdaki bölümler, **PDF'ye erişilebilirlik etiketleri eklemek** için gereken her işlemi adım adım gösterir. Her adımda tam bir kod bloğu, adımın neden önemli olduğuna dair bir açıklama ve gerçek projelerden alınmış pratik ipuçları bulunur.

### Geliştirme ortamınızı hazırlayın

1. Aspose.PDF NuGet paketini kurun:

```bash
dotnet add package Aspose.PDF
```

2. Yeni bir konsol projesi oluşturun (veya kodu mevcut bir projeye ekleyin):

```bash
dotnet new console -n PdfTagger
cd PdfTagger
```

> **Pro ipucu:** `-n` bayrağını kullanarak proje klasör adını kodun amacına uygun tutun; bu, projeyi daha sonra aradığınızda işinizi kolaylaştırır.

### Kaynak PDF'yi yükleyin

İlk işlem, etiketlemek istediğiniz mevcut PDF'yi açar.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Tagged;

// Step 1: Load the PDF document
var pdfDocument = new Document(@"YOUR_DIRECTORY\source.pdf");
```

**Neden önemli:** Belgeyi açmak, sayfaları, ek açıklamaları ve etiketleri manipüle edebileceğiniz bellek içi bir temsil oluşturur. Dosya yüklenmeden hiçbir erişilebilirlik bilgisi ekleyemezsiniz.

### Etiketli içerik öğesi oluşturma (C# PDF etiketleme)

Etiketli bir içerik öğesi, metnin mantıksal rolünü tanımlar (ör. paragraf, başlık). Burada bir paragraf etiketi oluşturuyoruz.

```csharp
// Step 2: Create a tagged content element
var paragraphTag = new TaggedContent
{
    Role = TaggedRoles.Paragraph, // defines the logical role
    Text = "Hello, tagged world!" // visible text that screen readers will announce
};
```

**Neden önemli:** `TaggedRoles` enum'ı doğrudan PDF/UA rollerine eşlenir. Doğru rolün kullanılması, içeriğin yardımcı teknolojiler tarafından nasıl yorumlanacağını belirlediği için PDF erişilebilirliği en iyi uygulamaları açısından kritiktir.

### Etiketin sayfadaki konumunu tanımlayın

Erişilebilirlik etiketlerinin, görsel düzenle mantıksal yapının eşleşmesi için geometrik bir konuma da ihtiyacı vardır.

```csharp
// Step 3: Define the location on the page (in points)
// Rectangle(left, bottom, right, top)
var tagLocation = new Rectangle(100, 500, 400, 550);
```

**Neden önemli:** Dikdörtgen, paragrafın sayfada nerede görüneceğini tanımlar. Konum görsel metinle eşleşmezse, ekran okuyucular yanlış bilgi aktarabilir ve PDF erişilebilirliği en iyi uygulamalarını ihlal eder.

### Etiketi ilk sayfaya ekleyin (etiketli PDF oluşturma)

Şimdi etiketi belirli bir sayfaya ekleyin. Bu örnekte ilk sayfayı kullanıyoruz, ancak çok sayfalı belgeler için `pdfDocument.Pages` üzerinden döngü yapabilirsiniz.

```csharp
// Step 4: Access the first page
var firstPage = pdfDocument.Pages[1];

// Step 5: Add the tagged content to the page at the specified position
firstPage.AddTag(paragraphTag, tagLocation);
```

> **Dikkat:** Aspose.PDF'de `Pages` 1‑tabanlıdır. İndeks 0 kullanılmaya çalışılırsa `ArgumentOutOfRangeException` hatası atılır.

### Değiştirilmiş PDF'yi kaydedin

Güncellenen belgeyi diske yazın. Kaydedilen dosya artık erişilebilirlik etiketini içerir.

```csharp
// Step 6: Save the modified PDF with the new tag
pdfDocument.Save(@"YOUR_DIRECTORY\tagged_out.pdf");
```

**Neden önemli:** Kaydetme, etiket bilgisini PDF'in yapı akışına (`/StructTreeRoot`) kalıcı olarak yazar. Ortaya çıkan dosya, PAC (PDF Accessibility Checker) gibi PDF/UA denetleyicileriyle doğrulanabilir.

### Erişilebilirlik etiketlerini doğrulayın

Etiketin eklendiğini, yapı incelemesini destekleyen bir görüntüleyicide (ör. Adobe Acrobat Pro > Tools > Accessibility > Read Order) açarak doğrulayabilirsiniz. Paragraf, mantıksal yapı ağacında görünmelidir.

Alternatif olarak, Aspose.PDF API'sini kullanarak etiketi geri okuyabilirsiniz:

```csharp
var savedDoc = new Document(@"YOUR_DIRECTORY\tagged_out.pdf");
var savedPage = savedDoc.Pages[1];
var tags = savedPage.Tags; // collection of TaggedContent objects

foreach (var tag in tags)
{
    Console.WriteLine($"Role: {tag.Role}, Text: {tag.Text}");
}
```

**Beklenen çıktı:**

```
Role: Paragraph, Text: Hello, tagged world!
```

Çıktı yukarıdaki kodla eşleşiyorsa, erişilebilirlik etiketi başarıyla eklenmiştir.

## Tam, çalıştırılabilir örnek

Aşağıda her adımı içeren tam program yer almaktadır. Kodu `Program.cs` dosyasına kopyalayın ve `dotnet run` komutunu çalıştırın.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Tagged;

namespace PdfTagger
{
    class Program
    {
        static void Main()
        {
            // Load the source PDF
            var pdfDocument = new Document(@"YOUR_DIRECTORY\source.pdf");

            // Create a paragraph tag
            var paragraphTag = new TaggedContent
            {
                Role = TaggedRoles.Paragraph,
                Text = "Hello, tagged world!"
            };

            // Define where the tag should appear
            var tagLocation = new Rectangle(100, 500, 400, 550);

            // Attach the tag to the first page
            var firstPage = pdfDocument.Pages[1];
            firstPage.AddTag(paragraphTag, tagLocation);

            // Save the tagged PDF
            var outputPath = @"YOUR_DIRECTORY\tagged_out.pdf";
            pdfDocument.Save(outputPath);

            // Verify the tag was added
            var savedDoc = new Document(outputPath);
            var savedPage = savedDoc.Pages[1];
            foreach (var tag in savedPage.Tags)
            {
                Console.WriteLine($"Role: {tag.Role}, Text: {tag.Text}");
            }

            Console.WriteLine("Accessibility tag added successfully.");
        }
    }
}
```

Programı çalıştırdığınızda `tagged_out.pdf` oluşturulur; bu PDF artık bir paragraf etiketi içerir. NVDA veya JAWS gibi ekran okuyucular, bu bölgeye geldiklerinde “Hello, tagged world!” ifadesini okuyacaktır.

## Yaygın varyasyonlar ve uç durumlar

| Durum | Kodu nasıl uyarlarsınız | Sebep |
|-----------|----------------------|--------|
| **Birden fazla sayfa** | `pdfDocument.Pages` üzerinden döngü yapın ve gerektiğinde her sayfaya etiket uygulayın. | Her sayfanın etiketlenmesini sağlar |

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu kılavuzda gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak tam çalışan kod örnekleri ve adım adım açıklamalar içerir.

- [Aspose.PDF for .NET ile Etiketli PDF'ler Oluşturma: Erişilebilirliği ve Belge Yapısını Geliştirmek İçin Tam Kılavuz](/pdf/english/net/advanced-features/create-tagged-pdfs-aspose-pdf-net/)
- [Aspose.PDF for .NET ile Etiketli PDF'ler Oluşturma ve Yönetme: Erişilebilirliği ve SEO'yu Geliştirin](/pdf/english/net/advanced-features/create-manage-tagged-pdfs-aspose-pdf-dotnet/)
- [Aspose.PDF .NET: Etiketleme ile PDF Erişilebilirliğini Artırma](/pdf/english/net/advanced-features/aspose-pdf-net-accessible-tagging-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}