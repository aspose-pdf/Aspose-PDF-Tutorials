---
category: general
date: 2026-08-04
description: C# ile yeni PDF belgesi oluşturun ve Aspose.Pdf kullanarak Bates numaralandırmasını
  hızlıca ekleyin – boş sayfa PDF eklemeyi ve özel sayfa numaralarını öğrenin.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create new pdf document
- add bates numbering pdf
- how to add bates
- add blank page pdf
- add custom page numbers
language: tr
lastmod: 2026-08-04
og_description: C#'ta yeni bir PDF belgesi oluşturun ve yasal dava yönetimi için otomatik
  olarak Bates numaralandırması ekleyin – tam kod örneği dahil.
og_image_alt: Screenshot of a C# program creating a PDF document with Bates numbers
  applied
og_title: C# ile Bates numaralandırmalı yeni PDF belgesi oluştur
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Create new PDF document in C# and add Bates numbering pdf quickly using
    Aspose.Pdf – learn to add blank page pdf and custom page numbers.
  headline: Create new PDF document with Bates numbering in C#
  type: TechArticle
tags:
- C#
- PDF
- Aspose.Pdf
- Bates numbering
title: C# ile Bates numaralandırmalı yeni PDF belgesi oluştur
url: /tr/net/document-creation/create-new-pdf-document-with-bates-numbering-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#'ta Bates numaralandırmalı yeni PDF belgesi oluşturma

Eğer C#'ta **yeni PDF belgesi oluşturmanız** gerekiyorsa, bu kılavuz Aspose.Pdf kullanarak **Bates numaralandırmalı PDF eklemeyi** gösterir. **Boş sayfa PDF eklemeyi**, **özel sayfa numaraları eklemeyi** yapılandırmayı ve son dosyayı kaydetmeyi öğreneceksiniz.

Bu öğretici, kütüphaneyi kurmaktan yasal dava dosyası standartlarına uygun bir PDF oluşturmaya kadar tüm adımları kapsar. Sonunda tek bir çalıştırılabilir programla PDF oluşturabilir, boş bir sayfa ekleyebilir, Bates numaralarını uygulayabilir ve numaralandırma formatını özelleştirebilirsiniz.

## Önkoşullar

* .NET 6.0 SDK veya daha yeni bir sürüm yüklü  
* Visual Studio 2022 (veya herhangi bir C# IDE'si)  
* Aktif bir Aspose.Pdf for .NET lisansı veya ücretsiz bir değerlendirme anahtarı  

Ek bir NuGet paketi yüklemenize gerek yok; öğretici her şeyi otomatik olarak kurar.

## Adım 1: Aspose.Pdf'i NuGet üzerinden kurun

Proje klasörünüzde bir terminal açın ve şu komutu çalıştırın:

```bash
dotnet add package Aspose.Pdf
```

Bu komut, projenize en son kararlı Aspose.Pdf sürümünü ekler; bu sürüm `Document`, `BatesNumbering` ve kullanacağınız diğer PDF‑manipülasyon sınıflarını sağlar.

## Adım 2: Yeni PDF belgesi oluşturma – başlangıç ayarları

PDF dosyasını oluşturmak, sonraki tüm işlemlerin temelidir. `Document` sınıfı, tüm PDF konteynerini temsil eder.

```csharp
using Aspose.Pdf;

// Step 2: Create a new PDF document
using var doc = new Document();
```

*Neden önemli*: `Document` nesnesi oluşturmak, sayfalar, yazı tipleri ve grafikler için gerekli iç yapıların ayrılmasını sağlar. `using var` kullanmak, dosyanın kaydedildikten sonra düzgün bir şekilde serbest bırakılmasını garantiler.

## Adım 3: Boş sayfa PDF ekleme

Bir PDF, üzerine içerik ekleyebilmek için en az bir sayfa içermelidir. Boş bir sayfa eklemek, Bates numaraları için temiz bir tuval sağlar.

```csharp
// Step 3: Add a blank page to the document
Page page = doc.Pages.Add();
```

`Pages.Add()` yöntemi, belgenin sayfa koleksiyonunun sonuna yeni, boş bir sayfa ekler. Daha sonra birden fazla sayfada **özel sayfa numaraları eklemeniz** gerekirse bu çağrıyı tekrarlayarak daha fazla sayfa ekleyebilirsiniz.

## Adım 4: Bates numaralandırmayı yapılandırma – nasıl bates eklenir

Bates numaralandırma, yasal belgelerde yaygın olarak kullanılan sıralı bir tanımlayıcıdır. Bunu `BatesNumbering` sınıfı aracılığıyla yapılandırırsınız.

```csharp
// Step 4: Set up Bates numbering options
var bates = new BatesNumbering
{
    StartNumber = 1000,      // Starting number for the sequence
    Prefix = "CaseA-",       // Text to prepend to each number
    Increment = 1,           // Increment between consecutive numbers
    // Optional: Set the location, font size, etc.
};
```

*Neden önemli*: `StartNumber` ilk sayıyı tanımlar, `Prefix` okunabilir bir etiket ekler ve `Increment` adım boyutunu kontrol eder. Ayrıca `HorizontalAlignment`, `VerticalAlignment`, `FontSize` ve `Margins` ayarlarını değiştirerek sayfadaki sayının görünümünü kontrol edebilirsiniz.

## Adım 5: Bates numaralandırmayı PDF sayfasına uygulama

Numaralandırma seçenekleri hazır olduğuna göre, bunları sayfaya (veya tüm belgeye) uygulayın.

```csharp
// Step 5: Apply the Bates numbering to the page
bates.Apply(page);
```

`Apply` çağrısı, varsayılan olarak biçimlendirilmiş sayıyı sayfanın altbilgisine ekler. Sayıyı başka bir yere koymanız gerekiyorsa, `Apply` çağırmadan önce `bates.Position` değerini ayarlayın.

## Adım 6: Bates numaraları uygulanmış PDF'i kaydetme

Son olarak, bellek içindeki belgeyi diske yazın.

```csharp
// Step 6: Save the PDF with Bates numbers applied
string outputPath = Path.Combine(
    Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
    "BatesNumbered.pdf");

doc.Save(outputPath);
Console.WriteLine($"PDF saved to {outputPath}");
```

Kaydedilen dosya artık alt kısımda **CaseA-1000** Bates numarası gösteren tek bir sayfa içerir. Numaralandırmayı doğrulamak için PDF'i herhangi bir görüntüleyicide açın.

## Beklenen çıktı

`BatesNumbered.pdf` dosyasını açtığınızda şunları görmelisiniz:

* Bir boş sayfa (veya ek sayfalar eklediyseniz daha fazla)  
* Sayfanın alt kısmına (varsayılan konum) yerleştirilmiş **CaseA-1000** metni  

Daha fazla sayfa ekleyip aynı `BatesNumbering` örneğini yeniden kullanırsanız, sayılar otomatik olarak artar (CaseA-1001, CaseA-1002, …).

## Pro ipucu: Bates numaralarına ek olarak özel sayfa numaraları ekleme

Bazen hem Bates numaralarına hem de geleneksel sayfa numaralarına ihtiyaç duyarsınız. Bates numaralandırmayı uyguladıktan sonra bir `TextFragment` ekleyerek ikisini birleştirebilirsiniz:

```csharp
// Add a traditional page number in the header
var pageNumber = new TextFragment($"Page {page.Number}")
{
    HorizontalAlignment = HorizontalAlignment.Center,
    VerticalAlignment = VerticalAlignment.Top,
    FontSize = 12,
    Font = FontRepository.FindFont("Arial")
};
page.Paragraphs.Add(pageNumber);
```

Bu kod parçacığı, Bates etiketini korurken **özel sayfa numaraları eklemeyi** gösterir.

## Kenar durumu: Bates numaralandırmayı birden çok sayfaya uygulama

Belgeniz birden fazla sayfa içeriyorsa, aynı `BatesNumbering` örneğini bir döngü içinde her sayfaya uygulayabilirsiniz:

```csharp
for (int i = 1; i <= doc.Pages.Count; i++)
{
    bates.Apply(doc.Pages[i]);
}
```

Döngü, her sayfanın tanımladığınız `StartNumber` ve `Increment` değerlerine göre sıralı bir numara almasını sağlar.

## Yaygın tuzaklar ve nasıl önlenir

| Sorun | Neden oluşur | Çözüm |
|-------|----------------|-----|
| Numaralar ortalanmamış görünüyor | Varsayılan hizalama tasarımınıza uymayabilir | `bates.HorizontalAlignment` ve `bates.VerticalAlignment` değerlerini açıkça ayarlayın |
| Numaralar mevcut içeriğin üzerine geliyor | Margin tanımlı değil | `bates.Margin` değerini ayarlayın veya sayıyı taşımak için `bates.Position` kullanın |
| Çalışma zamanında lisans istisnası | Değerlendirme sürümü çıktıyı kısıtlar | Belgeyi oluşturmadan önce geçerli bir Aspose.Pdf lisansı uygulayın (`License license = new License(); license.SetLicense("Aspose.Pdf.lic");`) |

## Tam çalışan örnek

Aşağıda, kopyalayıp yapıştırıp çalıştırabileceğiniz bağımsız bir program bulunmaktadır.

```csharp
using System;
using System.IO;
using Aspose.Pdf;

class Program
{
    static void Main()
    {
        // 1. Create a new PDF document
        using var doc = new Document();

        // 2. Add a blank page pdf
        Page page = doc.Pages.Add();

        // 3. Configure Bates numbering – how to add bates
        var bates = new BatesNumbering
        {
            StartNumber = 1000,
            Prefix = "CaseA-",
            Increment = 1,
            HorizontalAlignment = HorizontalAlignment.Right,
            VerticalAlignment = VerticalAlignment.Bottom,
            Margin = new MarginInfo(20, 20, 20, 20),
            FontSize =


## Sonraki Öğrenmeniz Gerekenler

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olmak için adım adım açıklamalar içeren tam çalışan kod örnekleri sunar.

- [How to Add and Customize Page Numbers in PDFs Using Aspose.PDF for .NET | Document Manipulation Guide](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [Aspose.PDF .NET&#58; Add Page Numbers to PDFs Using FloatingBox](/pdf/english/net/text-operations/aspose-pdf-net-floatingbox-page-numbering/)
- [Create PDF Document with Aspose.PDF – Add Page, Shape & Save](/pdf/english/net/document-creation/create-pdf-document-with-aspose-pdf-add-page-shape-save/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}