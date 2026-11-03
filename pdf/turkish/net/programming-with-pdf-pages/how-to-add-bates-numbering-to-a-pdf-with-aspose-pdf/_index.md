---
category: general
date: 2026-10-07
description: C# kullanarak bir PDF'ye Bates numaralandırması eklemeyi öğrenin. Bu
  adım adım rehber, PDF sayfa numaralandırmasını ve diğer numaralandırma ipuçlarını
  da kapsar.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add bates numbering
- pdf page numbering
- number pdf pages
- how to add bates
- bates numbering pdf
language: tr
lastmod: 2026-10-07
og_description: Bir PDF'ye hızlıca Bates numaralandırması ekleyin. PDF sayfa numaralandırmasını
  öğrenmek, PDF sayfalarını numaralandırmak ve belge takibini otomatikleştirmek için
  bu öğreticiyi izleyin.
og_image_alt: Screenshot of a PDF with Bates numbers added using Aspose.Pdf
og_title: C#'ta PDF'lere Bates numaralandırması ekleyin – tam Aspose rehberi
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Learn how to add bates numbering to a PDF using C#. This step‑by‑step
    guide also covers pdf page numbering and other numbering tricks.
  headline: How to add bates numbering to a PDF with Aspose.Pdf
  type: TechArticle
- description: Learn how to add bates numbering to a PDF using C#. This step‑by‑step
    guide also covers pdf page numbering and other numbering tricks.
  name: How to add bates numbering to a PDF with Aspose.Pdf
  steps:
  - name: 1. Can I change the location of the numbers?
    text: Yes. Set `batesOptions.Position = new Position(10, 10, 10, 10);` where the
      four values represent margins from the top, bottom, left, and right edges. Aspose
      also provides predefined enums such as `BatesNumberingPosition.BottomCenter`.
  - name: 2. What if my PDF already contains page numbers?
    text: Adding Bates numbers will **stack** on top of existing numbers. To avoid
      visual clutter, either hide the original numbers (if they are part of a text
      layer) or adjust the `batesOptions` font size and position.
  - name: 3. Does this work with encrypted PDFs?
    text: 'Aspose can open password‑protected PDFs if you supply the password:'
  - name: 4. How do I **number pdf pages** with a simple sequential counter (no prefix/suffix)?
    text: 'Just set `Prefix = string.Empty` and `Suffix = string.Empty`:'
  - name: 5. Can I use this approach in ASP.NET Core to serve PDFs on‑the‑fly?
    text: 'Absolutely. Load the document, apply the numbering, then write the stream
      to the HTTP response:'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Aspose.Pdf ile bir PDF'ye Bates numaralandırması nasıl eklenir
url: /tr/net/programming-with-pdf-pages/how-to-add-bates-numbering-to-a-pdf-with-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PDF'ye Aspose.Pdf ile bates numaralandırması ekleme

Bir PDF'ye **bates numaralandırması eklemeniz** gerekiyorsa, bu kılavuz C#'ta bunu tam olarak nasıl yapacağınızı gösterir. Hukuki paketler hazırlıyor, dava dosyalarını yönetiyor ya da sadece güvenilir **pdf sayfa numaralandırması** istiyorsanız, aşağıdaki adımlar size eksiksiz, çalıştırılabilir bir çözüm sunar.

Bu öğreticide şunları öğreneceksiniz:

* Mevcut bir PDF dosyasını yükleyin.
* Önek, başlangıç numarası, basamak doldurma, ayırıcı ve sonek gibi Bates numaralandırma seçeneklerini yapılandırın.
* Numaranı her sayfaya uygulayın.
* Güncellenen belgeyi kaydedin.

Aspose.Pdf for .NET kütüphanesi dışındaki herhangi bir harici araca gerek yoktur ve kod .NET 6+ ile .NET Framework 4.7.2+ üzerinde çalışır.  

---

## Önkoşullar

Başlamadan önce aşağıdakilere sahip olduğunuzdan emin olun:

| Gereksinim | Neden önemlidir |
|-------------|----------------|
| **Aspose.Pdf for .NET** (NuGet paketi `Aspose.Pdf`) | Kodda kullanılan `Document` ve `BatesNumberingOptions` sınıflarını sağlar. |
| **.NET SDK** (6.0 veya daha yeni sürüm önerilir) | C# konsol uygulamasını derlemenizi ve çalıştırmanızı sağlar. |
| **A source PDF** you want to number | Kılavuz `source.pdf` örneğini kullanır; yolu kendi dosyanızla değiştirin. |
| **Write permission** to the output folder | `Save` çağrısının yeni dosyayı yazması gerekir. |

Kütüphaneyi aşağıdaki CLI komutuyla kurabilirsiniz:

```bash
dotnet add package Aspose.Pdf
```

---

## Adım 1: Yeni bir konsol projesi oluşturun

Bir terminal açın ve şu komutu çalıştırın:

```bash
dotnet new console -n BatesNumberingDemo
cd BatesNumberingDemo
```

Bu, **bates numaralandırması eklemek** için gerekli kodu ekleyeceğimiz minimal bir C# projesi oluşturur.

---

## Adım 2: Gerekli `using` yönergelerini ekleyin

`Program.cs` dosyasını açın ve dosyanın en üstüne aşağıdaki ad alanlarını ekleyin:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;
```

* `Aspose.Pdf`, PDF'leri yüklemek ve kaydetmek için `Document` sınıfına erişim sağlar.  
* `Aspose.Pdf.Text` ise sayılar nasıl görüneceğini tanımlayan `BatesNumberingOptions` nesnesini içerir.

---

## Adım 3: Kaynak PDF'yi yükleyin

İlk işlem satırı, numaralandırmak istediğiniz PDF'yi yükler. `"YOUR_DIRECTORY/source.pdf"` ifadesini dosyanızın gerçek yolu ile değiştirin.

```csharp
// Load the source PDF
Document pdf = new Document("YOUR_DIRECTORY/source.pdf");
```

Dosya bulunamazsa Aspose bir `FileNotFoundException` fırlatır. Bunu önlemek için yolu önceden doğrulamak isteyebilirsiniz:

```csharp
if (!System.IO.File.Exists("YOUR_DIRECTORY/source.pdf"))
{
    Console.WriteLine("Source PDF not found.");
    return;
}
```

---

## Adım 4: Bates numaralandırma seçeneklerini tanımlayın

`BatesNumberingOptions`, numaralandırmanın her görsel unsurunu kontrol etmenizi sağlar. Aşağıdaki örnek, hukuki dava dosyaları için tipik bir yapılandırma gösterir:

```csharp
// Define Bates numbering options
BatesNumberingOptions batesOptions = new BatesNumberingOptions
{
    Prefix = "CASE-",          // Text before the numeric part
    StartNumber = 1000,       // First number to use
    Digits = 6,               // Pad with leading zeros (e.g., 001000)
    Separator = "-",          // Character between prefix, number, and suffix
    Suffix = "-2025"          // Text after the numeric part
};
```

**Her özelliğin önemi**

| Özellik | Amaç |
|----------|---------|
| `Prefix` | Belgeleri proje, müşteri veya dava bazında gruplamanıza yardımcı olur. |
| `StartNumber` | Başlangıç sayacını ayarlar; zaten numaralandırılmış dosyalarınız varsa faydalıdır. |
| `Digits` | Tekdüze bir genişlik sağlar, sıralamayı kolaylaştırır. |
| `Separator` | Özellikle önek ve sonek birleştirildiğinde okunabilirliği artırır. |
| `Suffix` | Yıl, sürüm veya herhangi bir ek tanımlayıcı eklemenizi sağlar. |

Yerleşimi (üst, alt, sol, sağ) ve yazı tipi stilini `batesOptions.Position` ve `batesOptions.Font` üzerinden de kontrol edebilirsiniz. Çoğu senaryo için varsayılanlar (alt‑sağ, 12‑pt Times New Roman) iyi çalışır.

---

## Adım 5: Numaralandırmayı her sayfaya uygulayın

`pdf.BatesNumbering.Add` çağrısı, sayfalar göründükleri sırayla numaraları ekler.

```csharp
// Apply Bates numbering to every page
pdf.BatesNumbering.Add(batesOptions);
```

Sadece bir alt küme üzerinde **pdf sayfalarını numaralandırmak** (ör. kapak sayfasını atlamak) istiyorsanız, bunun yerine bir `PageCollection` geçirebilirsiniz:

```csharp
// Example: skip the first page
pdf.BatesNumbering.Add(batesOptions, pdf.Pages.Skip(1));
```

---

## Adım 6: Güncellenen PDF'yi kaydedin

Son olarak, değiştirilmiş belgeyi diske yazın. Dosya adı genellikle PDF'nin artık Bates numaraları içerdiğini yansıtır.

```csharp
// Save the PDF with Bates numbers applied
pdf.Save("YOUR_DIRECTORY/bates_numbered.pdf");
Console.WriteLine("Bates numbering added successfully.");
```

Çıktı klasörü yoksa Aspose otomatik olarak oluşturur. Ancak bir `UnauthorizedAccessException` almamak için yazma izninizin olduğundan emin olun.

---

## Tam, çalıştırılabilir örnek

Tüm parçaları bir araya getirdiğimizde, kopyalayıp yapıştırıp çalıştırabileceğiniz eksiksiz bir program aşağıdadır:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Load the source PDF
        // -------------------------------------------------
        const string inputPath = "YOUR_DIRECTORY/source.pdf";
        if (!System.IO.File.Exists(inputPath))
        {
            Console.WriteLine($"Input file not found: {inputPath}");
            return;
        }

        Document pdf = new Document(inputPath);

        // -------------------------------------------------
        // 2️⃣ Configure Bates numbering
        // -------------------------------------------------
        BatesNumberingOptions batesOptions = new BatesNumberingOptions
        {
            Prefix = "CASE-",
            StartNumber = 1000,
            Digits = 6,
            Separator = "-",
            Suffix = "-2025"
        };

        // -------------------------------------------------
        // 3️⃣ Apply the numbering to every page
        // -------------------------------------------------
        pdf.BatesNumbering.Add(batesOptions);

        // -------------------------------------------------
        // 4️⃣ Save the result
        // -------------------------------------------------
        const string outputPath = "YOUR_DIRECTORY/bates_numbered.pdf";
        pdf.Save(outputPath);
        Console.WriteLine($"Bates numbering added. Saved to {outputPath}");
    }
}
```

**Beklenen çıktı** (konsol):

```
Bates numbering added. Saved to YOUR_DIRECTORY/bates_numbered.pdf
```

`bates_numbered.pdf` dosyasını açtığınızda, her sayfanın `CASE-001000-2025`, `CASE-001001-2025` gibi bir etiketle, varsayılan alt‑sağ köşede konumlandırıldığını göreceksiniz.

---

## Sıkça Sorulan Sorular (SSS)

### 1. Sayıların konumunu değiştirebilir miyim?
Evet. `batesOptions.Position = new Position(10, 10, 10, 10);` şeklinde dört değer, üst, alt, sol ve sağ kenarlardan olan boşlukları temsil eder. Aspose ayrıca `BatesNumberingPosition.BottomCenter` gibi önceden tanımlı enum'lar da sunar.

### 2. PDF'imde zaten sayfa numaraları varsa ne olur?
Bates numaraları mevcut sayılar üzerine **üst üste** eklenir. Görsel karmaşayı önlemek için orijinal sayıları gizleyebilir (metin katmanının bir parçasıysa) veya `batesOptions` yazı tipi boyutu ve konumunu ayarlayabilirsiniz.

### 3. Bu şifreli PDF'lerle çalışır mı?
Aspose, şifre korumalı PDF'leri şifreyi sağladığınız sürece açabilir:

```csharp
Document pdf = new Document("source.pdf", new LoadOptions { Password = "mySecret" });
```

Bates numaralandırma aynı şekilde uygulanır.

### 4. Basit bir sıralı sayaçla **pdf sayfalarını numaralandırmak** (önek/sonek olmadan) nasıl yapılır?
`Prefix = string.Empty` ve `Suffix = string.Empty` olarak ayarlayın:

```csharp
BatesNumberingOptions simple = new BatesNumberingOptions
{
    StartNumber = 1,
    Digits = 4   // 0001, 0002, …
};
pdf.BatesNumbering.Add(simple);
```

### 5. Bu yaklaşımı ASP.NET Core içinde PDF'leri anlık olarak sunmak için kullanabilir miyim?
Kesinlikle. Belgeyi yükleyin, numaralandırmayı uygulayın, ardından akışı HTTP yanıtına yazın:

```csharp
using (var ms = new MemoryStream())
{
    pdf.Save(ms);
    ms.Position = 0;
    return File(ms, "application/pdf", "bates_numbered.pdf");
}
```

---

## Kenar durumları ve en iyi uygulama ipuçları

| Durum | Önerilen yaklaşım |
|-----------|----------------------|
| **Büyük PDF'ler (yüzlerce sayfa)** | Aynı sayfaların birden fazla işlenmesini önlemek için sayfa‑seviyesi dönüşümlerini yaptıktan **sonra** `pdf.BatesNumbering.Add` çağırın. |
| **Özel yazı tipleri** | Tarama belgelerinde daha iyi okunabilirlik için `batesOptions.Font = FontRepository.FindFont("Arial")` ayarlayın ve `batesOptions.FontSize` değerini düzenleyin. |
| **Performans‑kritik toplu işler** | Döngü içinde birden çok dosya işlerken tek bir `Document` örneğini yeniden kullanın; her yinelemeden sonra bellek serbest bırakmak için nesneyi dispose edin. |
| **Uluslararası karakterler** | Önek veya sonek'in doğru görüntülenmesi için Unicode uyumlu yazı tipleri (ör. `Times New Roman Unicode`) kullanın. |
| **Sürüm uyumluluğu** | Kod Aspose.Pdf 23.10 ve üzeri sürümlerle çalışır. Daha eski bir sürüm hedefliyorsanız, özellik adı değişiklikleri için API referansına bakın. |

---

## Sonuç

Artık Aspose.Pdf for .NET kullanarak bir PDF'ye **bates numaralandırması eklemeyi** biliyorsunuz. Öğreticide PDF'yi yükleme, `BatesNumberingOptions` yapılandırma, sayfalara numaraları uygulama ve sonucu kaydetme adımları yer aldı. Bu temel bloklarla aynı zamanda genel **pdf sayfa numaralandırma**, **pdf sayfalarını numaralandırma** gibi işlemleri de özelleştirerek otomasyon hatlarına entegre edebilirsiniz.

**Sonraki adımlar**

* Font, renk ve konumu özelleştirmek için **bates numbering pdf** API'sini daha fazla keşfedin.  
* Bu tekniği **dijital imzalar** ile birleştirerek müdahale tespitli yasal paketler oluşturun.  
* Numaralandırmadan önce birden fazla dava dosyasını birleştirmeniz gerekiyorsa Aspose'un **PDF birleştirme** özelliklerine bakın.

Farklı önekler, sonekler ve basamak uzunlukları deneyerek kuruluşunuzun dosyalama standartlarına uygun hale getirin. Kodlamanın tadını çıkarın!

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanarak ilgili konuları ayrıntılı örnek kodlarla ve adım‑adım açıklamalarla ele alır.

- [PDF Belgesi Oluşturma C# – Bates Numaralandırma Rehberi](/pdf/english/net/document-creation/create-pdf-document-c-add-bates-numbering-guide/)
- [PDF'de C# ile Bates Numaralandırma Nasıl Eklenir – Tam Rehber](/pdf/english/net/programming-with-stamps-and-watermarks/how-to-add-bates-numbering-in-pdf-with-c-complete-guide/)
- [Aspose PDF Öğreticisi – Boş Sayfa Ekleme ve Bates Numaralandırmayı Güncelleme](/pdf/english/net/programming-with-pdf-pages/aspose-pdf-tutorial-insert-a-blank-page-and-update-bates-num/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}