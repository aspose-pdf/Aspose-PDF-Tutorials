---
category: general
date: 2026-07-20
description: Aspose.Pdf kullanarak bir PDF'ye bates numaralandırması nasıl eklenir.
  Bates numaralarını PDF'ye eklemeyi ve her sayfaya hızlı ve güvenilir bir şekilde
  damga eklemeyi öğrenin.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to add bates numbering
- add bates numbers pdf
- add stamp to each page
language: tr
lastmod: 2026-07-20
og_description: Aspose.Pdf ile bir PDF'e Bates numaralandırması nasıl eklenir. Bu
  kılavuz, Bates numaralarını PDF'e eklemeyi ve her sayfayı sadece birkaç C# satırıyla
  damgalamayı gösterir.
og_image_alt: Screenshot of a PDF page displaying Bates numbering added by Aspose.Pdf
og_title: PDF'ye Bates Numaralandırması Nasıl Eklenir – Tam Aspose.Pdf Öğreticisi
schemas:
- author: Aspose
  dateModified: '2026-07-20'
  description: How to add bates numbering to a PDF using Aspose.Pdf. Learn to add
    bates numbers pdf and add stamp to each page quickly and reliably.
  headline: How to Add Bates Numbering in PDF with Aspose – Step‑by‑Step Guide
  type: TechArticle
- questions:
  - answer: Yes. Load the document with a `PdfLoadOptions` object that supplies the
      password, then proceed exactly as shown.
    question: Does this work with password‑protected PDFs?
  - answer: Create multiple `BatesNumberingStamp` instances, configure each with its
      own `Prefix`, and apply them only to the appropriate page ranges.
    question: What if I need different prefixes per case?
  - answer: 'Aspose.Pdf offers a 30‑day trial. For production use you’ll need a license,
      but the API surface remains identical. --- ## Conclusion We’ve just covered
      **how to add bates numbering** to any PDF using Aspose.Pdf, demonstrated how
      to **add bates numbers pdf** in a clean, repeatable fashion, and showed'
    question: Is the library free?
  type: FAQPage
tags:
- Aspose.Pdf
- Bates numbering
- PDF automation
title: Aspose ile PDF'ye Bates Numaralandırması Nasıl Eklenir – Adım Adım Rehber
url: /tr/net/programming-with-stamps-and-watermarks/how-to-add-bates-numbering-in-pdf-with-aspose-step-by-step-g/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose ile PDF'ye Bates Numaralandırması Ekleme – Adım Adım Kılavuz

Bir hukuk belgesine **bates numaralandırması nasıl eklenir** sorusunu, bir GUI'de saatler harcamadan merak ettiniz mi? Tek başınıza değilsiniz. Birçok hukuk bürosunda, devlet kurumunda ve hatta büyük işletmelerde, her sayfayı benzersiz bir tanımlayıcıyla damgalamak günlük bir görevdir—ama tek bir C# satırı bunu çok kolay hâle getirebilir.

Bu öğreticide, Aspose.Pdf kütüphanesini kullanarak **bates numaralandırması nasıl eklenir** gösteren tam, çalıştırılabilir bir örnek üzerinden adım adım ilerleyeceğiz. Sonunda sadece birkaç satır kodla **bates numbers pdf** dosyalarına **her sayfaya damga ekleme** işlemini de bileceksiniz. Sihir yok, sadece net mantık ve pratik ipuçları.

## Öğrenecekleriniz

- Aspose.Pdf ile mevcut bir PDF yükleyin.
- `BatesNumberingStamp` oluşturun ve görünümünü özelleştirin.
- Her sayfayı döngüye alarak **her sayfaya damga ekleyin** otomatik olarak.
- Sonucu, her sayfada profesyonel bir Bates numarası taşıyan yeni bir PDF olarak kaydedin.

### Önkoşullar

- .NET 6.0 veya üzeri (kod .NET Framework 4.7+ üzerinde de çalışır).
- Geçerli bir Aspose.Pdf for .NET lisansı (veya geçici bir değerlendirme anahtarı).
- Numaralandırmak istediğiniz orijinal PDF dosyası (biz ona `Original.pdf` diyeceğiz).

Bu üç öğeyi karşılıyorsanız, başlayabilirsiniz.

---

## Adım 1: Projenizi Kurun ve Aspose.Pdf'yi Yükleyin

İlk olarak, yeni bir konsol projesi oluşturun (veya kodu mevcut bir projeye ekleyin). Ardından NuGet paketini çekin:

```bash
dotnet add package Aspose.Pdf
```

> **Pro ipucu:** Kurumsal bir ağda iseniz, NuGet kaynağınızın `https://www.nuget.org` adresine ulaşacak şekilde yapılandırıldığından emin olun.

## Adım 2: Kaynak PDF Belgesini Yükleyin

Bir PDF'i yüklemek, Aspose'u dosya yoluna işaret ettirmek kadar basittir. `Document` sınıfı tüm dosyayı temsil eder.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Load the source PDF (replace the path with your own)
var document = new Document(@"C:\Temp\Original.pdf");

// Quick sanity check – how many pages are we dealing with?
Console.WriteLine($"Document contains {document.Pages.Count} pages.");
```

Sayfa sayısını neden kaydediyoruz? Çünkü Bates numaralandırması *tüm* sayfalarda sıralı olmalıdır ve yanlışlıkla farklı bir dosya yüklemediğinizi doğrulamak iyidir.

## Adım 3: Bates Numaralandırma Damgası Oluşturun

İşlemin kalbi `BatesNumberingStamp`'tir. Ön ek, ayırıcı, basamak doldurma ve damganın bir *artifact* (yani metin çıkarma araçları için görünmez) olarak ele alınıp alınmayacağını tanımlamanıza olanak verir.

```csharp
var batesStamp = new BatesNumberingStamp
{
    // Starting number – change this to whatever your workflow requires
    StartingNumber = 1000,

    // A human‑readable prefix, often a case or project code
    Prefix = "ABC-",

    // Separator between the running number and the total page count
    Separator = "/",

    // Pad the number with leading zeros to a fixed width (5 digits here)
    NumberOfDigits = 5,

    // Mark the stamp as an artifact so it won’t be indexed by search
    Artifact = true
};
```

**Bu ayarlar neden?**  
- `StartingNumber = 1000` tipik bir yasal dosyanın zaten bir birikime sahip olduğunu taklit eder.  
- `NumberOfDigits = 5` `01000`, `01001` gibi sayıların düzgün hizalanmasını sağlar.  
- `Artifact = true` PDF OCR veya e‑discovery boru hatlarına gönderildiğinde çok önemlidir; sayılar insanlar için görünür kalır ancak metin‑arama motorları tarafından yok sayılır.

## Adım 4: Damgayı Her Sayfaya Ekleyin

Şimdi `document.Pages` üzerinde döngü yaparak aynı damgayı her sayfaya uyguluyoruz. Aspose sayıyı sizin için otomatik olarak artırır.

```csharp
foreach (Page page in document.Pages)
{
    // The AddStamp method clones the stamp for the current page,
    // updates the running number, and positions it at the default location.
    page.AddStamp(batesStamp);
}
```

> **Sık sorulan soru:** *Damganın nerede görüneceğini kontrol edebilir miyim?*  
> Kesinlikle. `BatesNumberingStamp`, `Stamp` sınıfından miras alır, bu yüzden döngüden önce `HorizontalAlignment`, `VerticalAlignment`, `XIndent` ve `YIndent` gibi özellikleri ayarlayabilirsiniz. Kısalık olması için varsayılan alt‑sağ köşeyi kullanacağız.

## Adım 5: Değiştirilmiş PDF'yi Kaydedin

Son olarak, değişiklikleri kalıcı hale getirin. Orijinal dosyanın üzerine yazabilir veya yeni bir konuma kaydedebilirsiniz—burada her iki kopyayı da tutacağız.

```csharp
// Save the new PDF with Bates numbers
document.Save(@"C:\Temp\BatesNumbered.pdf");

// Inform the user
Console.WriteLine("Bates numbering added successfully!");
```

`BatesNumbered.pdf` dosyasını açtığınızda, her sayfa aşağıdakine benzer bir damga gösterecek:

```
ABC-01000/00123
ABC-01001/00123
…
ABC-01122/00123
```

`00123` toplam sayfa sayısını, `ABC-` önekini ise sabit kalır.

---

## Tam Çalışan Örnek

Aşağıdaki tüm bloğu yeni bir `Program.cs` dosyasına kopyalayın ve çalıştırın. Dosya yollarını ortamınıza göre ayarlayın.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the source PDF
            var srcPath = @"C:\Temp\Original.pdf";
            var document = new Document(srcPath);
            Console.WriteLine($"Loaded '{srcPath}' with {document.Pages.Count} pages.");

            // 2️⃣ Configure the Bates numbering stamp
            var batesStamp = new BatesNumberingStamp
            {
                StartingNumber = 1000,
                Prefix = "ABC-",
                Separator = "/",
                NumberOfDigits = 5,
                Artifact = true,
                // Optional: change alignment if you need a different location
                // HorizontalAlignment = HorizontalAlignment.Left,
                // VerticalAlignment = VerticalAlignment.Top,
                // XIndent = 20,
                // YIndent = 20
            };

            // 3️⃣ Apply the stamp to every page
            foreach (Page page in document.Pages)
            {
                page.AddStamp(batesStamp);
            }

            // 4️⃣ Save the new PDF
            var outPath = @"C:\Temp\BatesNumbered.pdf";
            document.Save(outPath);
            Console.WriteLine($"Saved Bates‑numbered PDF to '{outPath}'.");
        }
    }
}
```

**Konsolda beklenen çıktı:**

```
Loaded 'C:\Temp\Original.pdf' with 12 pages.
Saved Bates-numbered PDF to 'C:\Temp\BatesNumbered.pdf'.
```

Kaydedilen dosyayı açtığınızda, her sayfada sıralı numaraları göreceksiniz—tam da **bates numbers pdf** eklediğinizde beklediğiniz şey.

---

## Gelişmiş Ayarlamalar (İsteğe Bağlı)

| Goal | How to achieve it |
|------|-------------------|
| **Damga rengini değiştir** | Set `batesStamp.Color = Color.FromRgb(255, 0, 0);` before the loop. |
| **Damgayı başlıkta konumlandır** | Adjust `HorizontalAlignment` and `VerticalAlignment` properties as shown in the commented code. |
| **Belirli sayfaları atla** | Add an `if (page.Number % 2 == 0) continue;` condition inside the `foreach`. |
| **Özel bir yazı tipi kullan** | Assign `batesStamp.Font = FontRepository.FindFont("Arial");`. |
| **Damgayı OCR için görünür yap** | Set `Artifact = false`. |

Bu varyasyonlar, temel mantığı düzenli tutarken **her sayfaya damga eklemenizi** sağlar.

## Sıkça Sorulan Sorular

**S: Bu, şifre korumalı PDF'lerle çalışır mı?**  
C: Evet. Belgeyi şifreyi sağlayan bir `PdfLoadOptions` nesnesiyle yükleyin, ardından gösterildiği gibi devam edin.

**S: Her dava için farklı ön eklere ihtiyacım olursa ne yapmalıyım?**  
C: Birden fazla `BatesNumberingStamp` örneği oluşturun, her birini kendi `Prefix`iyle yapılandırın ve yalnızca ilgili sayfa aralıklarına uygulayın.

**S: Kütüphane ücretsiz mi?**  
C: Aspose.Pdf 30 günlük bir deneme sürümü sunar. Üretim kullanımında bir lisansa ihtiyacınız olacak, ancak API aynı kalır.

## Sonuç

Aspose.Pdf kullanarak herhangi bir PDF'ye **bates numaralandırması nasıl eklenir** konusunu ele aldık, **bates numbers pdf** eklemenin temiz ve tekrarlanabilir bir yolunu gösterdik ve tek bir döngüyle **her sayfaya damga eklemenin** en basit yolunu sunduk. Kod tamamen bağımsızdır, saniyeler içinde çalışır ve büyük belge‑işleme boru hatlarına değişiklik yapmadan eklenebilir.

Bir sonraki meydan okumaya hazır mısınız? Bates aralığını listeleyen bir kapak sayfası oluşturmayı deneyin ya da her damganın yanına bir QR kodu ekleyin. Olasılıklar sonsuzdur ve bugün öğrendiğiniz aynı desen, PDF meta verilerini otomatikleştirmeniz gereken her yerde size yardımcı olacaktır.

Bu kılavuzu faydalı bulduysanız, paylaşın, yorum bırakın veya PDF birleştirme, filigran ekleme ve dijital imzalarla ilgili diğer öğreticilerimize göz atın. Kodlamanın tadını çıkarın!

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanarak yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olmak için adım adım açıklamalar içeren tam çalışan kod örnekleri sunar.

- [Aspose.PDF for .NET Kullanarak PDF'lerde Sayfa Damgaları Ekleme: Tam Kılavuz](/pdf/english/net/watermarks-backgrounds/add-page-stamp-aspose-pdf-dotnet-guide/)
- [Aspose.PDF for .NET Kullanarak PDF'lerde Sayfa Numarası Damgaları Ekleme | Filigranlar ve Arka Planlar](/pdf/english/net/watermarks-backgrounds/add-page-number-stamp-using-aspose-pdf-dotnet/)
- [Aspose.PDF for .NET Kullanarak PDF'lerde Sayfa Numaralarını Ekleme ve Özelleştirme | Belge Manipülasyonu Kılavuzu](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}