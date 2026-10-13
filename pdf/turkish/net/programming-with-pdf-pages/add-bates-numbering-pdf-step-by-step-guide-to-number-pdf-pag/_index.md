---
category: general
date: 2026-03-03
description: Bates numaralandırmasını PDF'e hızlıca ekleyin ve Aspose.Pdf kullanarak
  C#'ta PDF sayfalarını nasıl numaralandıracağınızı veya sıralı PDF numaraları ekleyeceğinizi
  öğrenin.
draft: false
keywords:
- add bates numbering pdf
- number pdf pages
- add sequential pdf numbers
- pdf bates numbering tutorial
- aspnet pdf automation
language: tr
og_description: C# ile PDF sayfalarına Bates numaralandırması ekleyin ve sıralı PDF
  numaraları ekleyin. Tam kod, açıklamalar ve en iyi uygulamalar.
og_title: Bates Numaralandırması PDF Ekle – Tam C# Öğreticisi
tags:
- PDF
- C#
- Aspose.Pdf
- Document Automation
title: PDF'ye Bates Numaralandırması Ekle – PDF Sayfalarını Numaralandırma Adım Adım
  Kılavuzu
url: /tr/net/programming-with-pdf-pages/add-bates-numbering-pdf-step-by-step-guide-to-number-pdf-pag/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Bates Numaralandırma PDF Ekle – Tam C# Öğreticisi

Hiç **add bates numbering pdf** dosyalarını eklemeniz gerekti, ama nereden başlayacağınızı bilmiyor muydunuz? Tek başınıza değilsiniz—hukuk ekipleri, denetçiler ve arşivciler aynı sorunla mücadele ediyor. İyi haber? Birkaç C# satırı ve Aspose.Pdf kütüphanesiyle **number pdf pages** otomatik olarak yapabilir ve **add sequential pdf numbers** için özel önekler, sonekler ve konumlandırma esnekliğine sahip olabilirsiniz.

Bu rehberde gerçek bir örnek üzerinden ilerleyecek, her ayarın neden önemli olduğunu açıklayacak ve farklı sayfa boyutları ya da özel basamak sayıları gibi uç durumlar için kodu nasıl ayarlayacağınızı göstereceğiz. Sonunda, elinizdeki herhangi bir PDF’ye Bates numaraları ekleyen, çalıştırmaya hazır bir kod parçacığı olacak ve her seçeneğin “neden”ini anlayacaksınız.

## Prerequisites

Başlamadan önce şunlara sahip olduğunuzdan emin olun:

- .NET 6.0 veya daha yeni bir sürüm (kod .NET Framework 4.6+ ile de çalışır)
- Geçerli bir Aspose.Pdf for .NET lisansı (veya ücretsiz deneme anahtarı)
- Visual Studio 2022 (veya tercih ettiğiniz herhangi bir C# editörü)
- `source.pdf` adlı bir kaynak PDF, referans verebileceğiniz bir klasörde

Hepsi bu—Aspose.Pdf dışındaki ekstra NuGet paketlerine gerek yok.

## Step 1 – Open the Source PDF Document

İlk olarak damgalamak istediğiniz PDF’yi yüklemeniz gerekir. Bir `using` bloğu kullanmak, dosya tutamacının doğru bir şekilde serbest bırakılmasını garanti eder ve böylece sonraki kilitlenme sorunlarını önler.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Step 1: Load the original PDF
using (var pdfDocument = new Document(@"C:\MyDocs\source.pdf"))
{
    // The rest of the steps will go inside this block.
}
```

> **Why this matters:** `using` ifadesi içinde belgeyi açmak, belirli bir atama (deterministic disposal) sağlar. Bunu atlar ve dosya kilitli kalırsa, PDF’yi kaydetme veya silme girişimleriniz başarısız olur—bu, üretim hatlarında baş ağrısına neden olduğunu gördüğüm bir durumdur.

## Step 2 – Configure Bates Numbering Options

Şimdi Aspose’a Bates numaralarının nasıl görünmesini istediğimizi söylüyoruz. Her özellik doğrudan sayfadaki görsel bir öğeye karşılık gelir.

```csharp
// Step 2: Set up Bates numbering preferences
var batesOptions = new BatesNumberingOptions
{
    Prefix = "2025-",               // Text before the number
    Suffix = "-A",                  // Text after the number
    Start = 5000,                   // First number in the sequence
    NumberOfDigits = 5,             // Pads with leading zeros (e.g., 05000)
    Placement = BatesNumberPlacement.BottomRight // Where the number appears
};
```

### Quick tips for the options

| Property | What it does | When to change it |
|----------|--------------|-------------------|
| **Prefix / Suffix** | Sayısal kısmın önüne/sonuna sabit metin ekler. | Bir dava kimliği, proje kodu veya gizli belgeler için “CONF‑” gibi bir önek kullanın. |
| **Start** | Serideki ilk sayı. | Önceki bir partiden numaralandırma şemasına devam ediyorsanız, buna göre ayarlayın. |
| **NumberOfDigits** | Sıfır doldurmayı (zero‑padding) kontrol eder. | Hukuki dosyalarda genellikle tam 6 basamak gerekir; `6` olarak ayarlayın. |
| **Placement** | BottomRight, BottomLeft, TopRight, TopLeft, Center. | Belge düzeninize göre seçin; BottomRight Bates numaraları için en yaygın konumdur. |

> **Pro tip:** Birden fazla sütunda **number pdf pages** yapmanız gerekiyorsa, farklı `Placement` değerleri ve ayrı `Prefix` dizeleriyle `pdfDocument.AddBatesNumbering` metodunu iki kez çağırabilirsiniz.

## Step 3 – Apply the Bates Numbering to the Document

Seçenekler hazır olduğunda, damgalama tek bir metod çağrısı ile gerçekleşir. Aspose, sayfalama, döndürme ve kenar boşluğu hesaplamalarını dahili olarak yönetir.

```csharp
// Step 3: Apply the numbering to every page
pdfDocument.AddBatesNumbering(batesOptions);
```

> **Why a single call works:** Aspose, `pdfDocument.Pages` üzerinde döner, her sayfa için bir `TextFragment` oluşturur ve seçtiğiniz `Placement` temelinde konumlandırır. Bu soyutlama, manuel bir döngü yazmanızı ve koordinat dönüşümleriyle uğraşmanızı engeller.

## Step 4 – Save the Updated PDF

Son olarak, değiştirilmiş dosyayı diske yazın. Orijinali üzerine yazabilir ya da yeni bir dosya oluşturabilirsiniz; aşağıdaki örnek yeni bir kopya yaratır.

```csharp
// Step 4: Persist the changes
pdfDocument.Save(@"C:\MyDocs\bates_numbered.pdf");
```

Eğer **add sequential pdf numbers** işlemini bir akışa (ör. bir API üzerinden dosya gönderirken) eklemeniz gerekiyorsa, dosya yolunu bir `MemoryStream` ile değiştirin:

```csharp
using var output = new MemoryStream();
pdfDocument.Save(output);
output.Position = 0; // Reset for downstream consumption
```

## Full Working Example

Hepsini bir araya getirdiğimizde, tam çalışır bir program şu şekildedir:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;

class Program
{
    static void Main()
    {
        // Open the source PDF
        using (var pdfDocument = new Document(@"C:\MyDocs\source.pdf"))
        {
            // Configure Bates numbering
            var batesOptions = new BatesNumberingOptions
            {
                Prefix = "2025-",
                Suffix = "-A",
                Start = 5000,
                NumberOfDigits = 5,
                Placement = BatesNumberPlacement.BottomRight
            };

            // Apply the numbering
            pdfDocument.AddBatesNumbering(batesOptions);

            // Save the result
            pdfDocument.Save(@"C:\MyDocs\bates_numbered.pdf");
        }

        Console.WriteLine("Bates numbering added successfully!");
    }
}
```

### Expected Output

- `C:\MyDocs` içinde yeni bir `bates_numbered.pdf` dosyası oluşur.
- Her sayfa, alt‑sağ köşede `2025-05000-A`, `2025-05001-A`, … gibi bir şey gösterir.
- Sayılar, `NumberOfDigits` ayarına uygun olarak beş basamağa sıfır doldurulur.

## Handling Common Variations

### 1. Different Page Sizes

PDF’niz portre ve manzara sayfalarını karıştırıyorsa, numaranın geniş tarafta kesildiğini görebilirsiniz. Bunu düzeltmek için `AutoFit` özelliğini etkinleştirin:

```csharp
batesOptions.AutoFit = true; // Adjusts font size to fit within page margins
```

### 2. Custom Font or Color

Bates numaraları varsayılan olarak siyah, 12‑pt Times New Roman’dır. Görünümü değiştirmek için `TextState`’e erişin:

```csharp
batesOptions.TextState = new TextState
{
    FontSize = 10,
    Font = FontRepository.FindFont("Courier New"),
    ForegroundColor = Color.GetBlue()
};
```

### 3. Skipping Pages

Başlık sayfasını atlayarak **number pdf pages** yapmak istediğinizi varsayalım. Bir sayfa aralığı kullanın:

```csharp
pdfDocument.AddBatesNumbering(batesOptions, new PageNumbering { Start = 2 });
```

### 4. Adding Multiple Numbering Schemes

Hukuk ekipleri bazen hem bir Bates numarası hem de gizli bir filigran ister. Farklı `Placement` değerleriyle iki ayrı `AddBatesNumbering` çağrısı çalıştırın:

```csharp
// First scheme – bottom right
pdfDocument.AddBatesNumbering(batesOptions);

// Second scheme – top left, different prefix
var confidentialOptions = new BatesNumberingOptions
{
    Prefix = "CONF-",
    Start = 1,
    NumberOfDigits = 4,
    Placement = BatesNumberPlacement.TopLeft,
    TextState = new TextState { FontSize = 8, ForegroundColor = Color.GetRed() }
};
pdfDocument.AddBatesNumbering(confidentialOptions);
```

## Frequently Asked Questions

**Q: Does this work with PDFs that already have existing text?**  
A: Yes. Aspose adds the Bates number as a separate layer, so existing content stays untouched. If you need the numbers to appear *behind* existing text (rare), you’d have to manipulate the page’s content streams manually.

**Q: What if the PDF is password‑protected?**  
A: Load it with the password first: `new Document(path, new LoadOptions { Password = "secret" })`. After stamping, you can re‑apply encryption via `pdfDocument.Encrypt(...)`.

**Q: Can I use this in a .NET Core console app?**  
A: Absolutely. The same code works in .NET Core, .NET 5+, and .NET Framework. Just reference the appropriate Aspose.Pdf NuGet package.

## Conclusion

**add bates numbering pdf** dosyalarını nasıl ekleyeceğinizi, **number pdf pages** nasıl yapacağınızı ve **add sequential pdf numbers** ile biçimlendirme, konumlandırma ve uç‑durum yönetimi üzerinde tam kontrol sağlayarak nasıl uygulayacağınızı yeni öğrendiniz. Yukarıdaki kısa kod parçacığı işi büyük ölçüde hallederken, ek seçenekler çözümü her türlü yasal, arşiv veya uyumluluk iş akışına uyarlamanıza olanak tanır.

Bir sonraki adıma hazır mısınız? Bu yaklaşımı şu senaryolarla birleştirin:

- **Batch processing** – bir klasördeki PDF’leri döngüyle işleyip aynı numaralandırma şemasını uygulayın.
- **Dynamic prefixes** – veritabanından dava kimliklerini çekip belge başına ekleyin.
- **PDF/A compliance** – numaralandırmadan sonra `pdfDocument.Convert(..., PdfFormat.PdfA2b)` çağırarak uzun vadeli koruma sağlayın.

Deney yapmaktan, bulgularınızı paylaşmaktan ya da yorumlarda sorular sormaktan çekinmeyin. İyi kodlamalar, ve PDF’leriniz her zaman mükemmel şekilde indekslenmiş olsun! 

![Alt köşede Bates numaraları bulunan bir PDF sayfasının ekran görüntüsü](https://example.com/images/bates-numbered.png "add bates numbering pdf örneği")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}