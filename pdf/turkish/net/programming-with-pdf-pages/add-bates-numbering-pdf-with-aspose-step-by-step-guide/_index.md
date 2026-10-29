---
category: general
date: 2026-08-08
description: Aspose.Pdf kullanarak C# ile Bates numaralandırmalı PDF ekleyin. Bu öğreticide
  ayrıca boş sayfa PDF ekleme ve PDF'yi programlı olarak oluşturma gösterilmektedir.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add bates numbering pdf
- add blank page pdf
- generate pdf programmatically
- create pdf aspose
language: tr
lastmod: 2026-08-08
og_description: C# ile Aspose.Pdf kullanarak Bates numaralandırmalı PDF ekleyin. Boş
  sayfa PDF eklemeyi, PDF'yi programlı olarak oluşturmayı ve son belgeyi dakikalar
  içinde kaydetmeyi öğrenin.
og_image_alt: Screenshot of C# code adding Bates numbering and a blank page to a PDF
  using Aspose.Pdf
og_title: Aspose ile PDF'e Bates Numarası Ekleme – Tam C# Rehberi
schemas:
- author: Aspose
  dateModified: '2026-08-08'
  description: Add bates numbering pdf using Aspose.Pdf in C#. This tutorial also
    shows how to add blank page pdf and generate pdf programmatically.
  headline: Add bates numbering pdf with Aspose – step‑by‑step guide
  type: TechArticle
- description: Add bates numbering pdf using Aspose.Pdf in C#. This tutorial also
    shows how to add blank page pdf and generate pdf programmatically.
  name: Add bates numbering pdf with Aspose – step‑by‑step guide
  steps:
  - name: What if I need a different font or position?
    text: 'The `BatesNumberingArtifact` exposes properties such as `FontSize`, `FontColor`,
      `HorizontalAlignment`, and `VerticalAlignment`. For example:'
  - name: How do I exclude a specific page from numbering?
    text: Create a separate `BatesNumberingArtifact` for the pages you want to number
      and add it only to those pages. Pages without an attached artifact will remain
      unnumbered.
  - name: Does this work with existing PDFs?
    text: 'Yes. Instead of `new Document()`, load an existing file:'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF generation
- Bates numbering
title: Aspose ile PDF'e Bates Numaralandırması Ekleme – Adım Adım Kılavuz
url: /tr/net/programming-with-pdf-pages/add-bates-numbering-pdf-with-aspose-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose ile bates numaralandırmalı PDF ekleme – adım adım kılavuz

Aspose.Pdf ile bates numaralandırmalı PDF eklemek, temel adımları anladığınızda oldukça basittir. Boş sayfa PDF ekleme veya PDF'i programlı olarak oluşturma ihtiyacınız da varsa, bu kılavuz ihtiyacınız olan her şeyi kapsar.

Bu öğreticide şunları yapacaksınız:

* Sıfırdan yeni bir PDF belgesi oluşturma.  
* Bates numaralarını barındıracak bir boş sayfa PDF ekleme.  
* Özel bir önekle Bates numaralandırma nesnesini yapılandırma.  
* Sayıların oluşturulan dosyada görünmesi için PDF'i kaydetme.  

Sonunda, **CASE‑1000**, **CASE‑1001**, … gibi Bates numaraları içeren bir PDF üreten tam işlevsel bir C# konsol uygulamanız olacak – bu, hukuk ve e‑keşif iş akışları için yaygın bir gereksinimdir.

## Önkoşullar

* .NET 6.0 SDK veya daha yenisi (kod .NET Framework 4.8 ile de çalışır).  
* Visual Studio 2022 veya herhangi bir C# uyumlu IDE.  
* Geçerli bir Aspose.Pdf for .NET lisansı (veya ücretsiz bir değerlendirme anahtarı).  
* C# sözdizimi hakkında temel bilgi.

> **İpucu:** Kodu lisans olmadan çalıştırırsanız, Aspose çıktıya küçük bir filigran ekleyecektir.

## Adım 1: Projeyi kurun ve Aspose.Pdf'i içe aktarın

Yeni bir konsol projesi oluşturun ve Aspose.Pdf NuGet paketini ekleyin:

```bash
dotnet new console -n BatesNumberingDemo
cd BatesNumberingDemo
dotnet add package Aspose.Pdf
```

Örnekte gereken `using` yönergeleri şunlardır:

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Artifacts;
```

Bu ad alanları, daha sonra kullanılacak `Document`, `Page` ve `BatesNumberingArtifact` sınıflarına erişim sağlar.

## Adım 2: Boş bir sayfa PDF ekleyin

Bates numarası bir sayfaya eklenmelidir, bu yüzden önce numaralandırma nesnesini alacak boş bir sayfa oluştururuz.

```csharp
// Step 2: Add a blank page pdf
Document pdfDocument = new Document();          // creates an empty PDF
Page pdfPage = pdfDocument.Pages.Add();         // adds the first (blank) page
```

`Document` sınıfı tüm PDF dosyasını temsil ederken, `Pages.Add()` belge sayfa koleksiyonunun sonuna yeni, boş bir sayfa ekler. Belge başlangıçta boş olduğundan, bu çağrı aynı zamanda ilk sayfayı da oluşturur.

## Adım 3: Bates numaralandırma nesnesini yapılandırın

Şimdi Bates numaralarının nasıl görüneceğini tanımlıyoruz. `BatesNumberingArtifact`, başlangıç numarası, önek, sonek ve biçimlendirme seçeneklerini ayarlamanıza olanak tanır.

```csharp
// Step 3: Define Bates numbering settings
BatesNumberingArtifact batesArtifact = new BatesNumberingArtifact(pdfPage)
{
    StartNumber = 1000,          // first number in the sequence
    Prefix = "CASE-",            // custom prefix before each number
    // Optional: you can also set Suffix, FontSize, FontColor, etc.
};
```

**Neden önemli:**  
`StartNumber` değerini **1000** olarak ayarlamak, tipik hukuk dosyası konvansiyonlarıyla eşleşir. `Prefix` her sayının **CASE‑1000**, **CASE‑1001**, … şeklinde görünmesini sağlar; bu da aramayı ve sıralamayı kolaylaştırır.

## Adım 4: Nesneyi sayfaya ekleyin

Nesne, Aspose'un kaydetme sırasında her sayfada render etmesi için sayfanın `Artifacts` koleksiyonuna eklenmelidir.

```csharp
// Step 4: Attach the Bates numbering artifact to the PDF page
pdfPage.Artifacts.Add(batesArtifact);
```

Belge kaydedildiğinde, Aspose otomatik olarak nesneyi tüm sayfalara tekrarlar ve sonraki her sayfa için numarayı artırır.

## Adım 5: (İsteğe bağlı) Ek sayfalar ekleyin

Daha fazla sayfaya ihtiyacınız varsa, sadece `pdfDocument.Pages.Add()` ifadesini tekrarlayın. Önceki adımda eklediğiniz Bates numaralandırma nesnesi, her yeni sayfada otomatik olarak görünecektir.

```csharp
// Example: add two more pages
pdfDocument.Pages.Add();
pdfDocument.Pages.Add();
```

## Adım 6: PDF'i kaydedin – programlı olarak pdf oluşturma

Son olarak belgeyi diske kalıcı olarak kaydedin. İşte Bates numaralarının sayfalara işlendiği nokta.

```csharp
// Step 6: Save the PDF – generate pdf programmatically
string outputPath = Path.Combine(
    Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
    "BatesNumberedDocument.pdf");

// Ensure the directory exists
Directory.CreateDirectory(Path.GetDirectoryName(outputPath)!);

pdfDocument.Save(outputPath);
Console.WriteLine($"PDF saved to: {outputPath}");
```

**Beklenen sonuç:**  
*BatesNumberedDocument.pdf* dosyasını açtığınızda üç sayfalı bir PDF göreceksiniz. Her sayfa sağ alt köşede bir Bates numarası gösterir:

* Sayfa 1 → **CASE‑1000**  
* Sayfa 2 → **CASE‑1001**  
* Sayfa 3 → **CASE‑1002**

Nesne sayfa koleksiyonuna eklendiği için numaralar otomatik olarak artırılır.

## Tam, çalıştırılabilir örnek

Her şeyi bir araya getirdiğimizde, kopyalayıp yapıştırıp çalıştırabileceğiniz eksiksiz bir konsol programı aşağıdadır:

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Artifacts;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main()
        {
            // Create a new PDF document
            Document pdfDocument = new Document();

            // Add a blank page pdf
            Page pdfPage = pdfDocument.Pages.Add();

            // Define Bates numbering settings (add bates numbering pdf)
            BatesNumberingArtifact batesArtifact = new BatesNumberingArtifact(pdfPage)
            {
                StartNumber = 1000,
                Prefix = "CASE-"
            };

            // Attach the artifact to the page
            pdfPage.Artifacts.Add(batesArtifact);

            // (Optional) add more pages to see incremented numbers
            pdfDocument.Pages.Add(); // page 2
            pdfDocument.Pages.Add(); // page 3

            // Save the PDF – generate pdf programmatically
            string outputPath = Path.Combine(
                Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
                "BatesNumberedDocument.pdf");

            Directory.CreateDirectory(Path.GetDirectoryName(outputPath)!);
            pdfDocument.Save(outputPath);

            Console.WriteLine($"PDF saved to: {outputPath}");
        }
    }
}
```

Programı `dotnet run` ile çalıştırın. Çalıştırdıktan sonra dosyayı masaüstünüzde bulun ve Bates numaralarını doğrulayın.

![Add bates numbering pdf example](/images/bates-numbering.png "Add bates numbering pdf example")

## Yaygın sorular ve kenar durumları

### Farklı bir yazı tipi veya konum gerekirse ne yapmalıyım?

`BatesNumberingArtifact` `FontSize`, `FontColor`, `HorizontalAlignment` ve `VerticalAlignment` gibi özellikler sunar. Örneğin:

```csharp
batesArtifact.FontSize = 12;
batesArtifact.FontColor = Color.Blue;
batesArtifact.HorizontalAlignment = HorizontalAlignment.Left;
batesArtifact.VerticalAlignment = VerticalAlignment.Top;
```

### Belirli bir sayfayı numaralandırmadan dışarıda bırakmak nasıl olur?

Numaralandırmak istediğiniz sayfalar için ayrı bir `BatesNumberingArtifact` oluşturun ve sadece o sayfalara ekleyin. Artefakt eklenmemiş sayfalar numarasız kalır.

### Mevcut PDF'lerle çalışabilir mi?

Evet. `new Document()` yerine mevcut bir dosyayı yükleyin:

```csharp
Document pdfDocument = new Document("input.pdf");
```

Ardından artefaktı istediğiniz sayfalara ekleyin ve kaydedin.

## Sonuç

Artık **add bates numbering pdf** işlemini Aspose.Pdf kullanarak nasıl yapacağınızı, **add blank page pdf** eklemeyi ve **generate pdf programmatically** işlemini temiz, yeniden kullanılabilir bir C# çözümünde nasıl gerçekleştireceğinizi biliyorsunuz. Yaklaşım, sayfa sayısı, özel önekler ve stil seçenekleri ne olursa olsun çalışır ve nihai belge üzerinde tam kontrol sağlar.

İleride keşfedebileceğiniz adımlar:

* Use **create pdf as


## What Should You Learn Next?


Aşağıdaki öğreticiler, bu kılavuzda gösterilen tekniklere dayanarak yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak tam çalışan kod örnekleri ve adım adım açıklamalar içerir.

- [How to Add and Customize Page Numbers in PDFs Using Aspose.PDF for .NET | Document Manipulation Guide](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [How to Add an Empty Page at the End of a PDF Using Aspose.PDF for .NET | Step-by-Step Guide](/pdf/english/net/document-manipulation/add-empty-page-end-pdf-aspose-pdf-net/)
- [Create PDF Document with Aspose.PDF – Add Page, Shape & Save](/pdf/english/net/document-creation/create-pdf-document-with-aspose-pdf-add-page-shape-save/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}