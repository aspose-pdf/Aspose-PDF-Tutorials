---
category: general
date: 2026-09-27
description: Aspose.PDF kullanarak C#'de PDF'ye Bates numaralandırması ekleyin. Bir
  PDF belgesini nasıl yükleyeceğinizi, Bates numaralandırma seçeneklerini nasıl ayarlayacağınızı
  ve güncellenmiş dosyayı nasıl kaydedeceğinizi öğrenin.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add bates numbering
- load pdf document
- how to add bates numbering
- Aspose.PDF C#
- PDF Bates numbering example
language: tr
lastmod: 2026-09-27
og_description: Aspose.PDF kullanarak C#'de PDF'ye Bates numaralandırması ekleyin.
  Bu öğreticide bir PDF belgesini nasıl yükleyeceğinizi, Bates numaralandırmasını
  nasıl yapılandıracağınızı ve sonucu nasıl kaydedeceğinizi gösterir.
og_image_alt: Screenshot of a PDF page displaying Bates numbers in the footer
og_title: Aspose.PDF ile PDF'e Bates numaralandırması ekleyin – C# rehberi
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Add bates numbering to PDF using Aspose.PDF in C#. Learn how to load
    a PDF document, set Bates numbering options, and save the updated file.
  headline: Add bates numbering to PDF using Aspose.PDF in C#
  type: TechArticle
tags:
- Aspose.PDF
- C#
- PDF processing
title: C#'de Aspose.PDF kullanarak PDF'ye Bates numaralandırması ekleyin
url: /tr/net/programming-with-text/add-bates-numbering-to-pdf-using-aspose-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.PDF ile C#'ta PDF'ye Bates Numaralandırması Ekleme

Eğer bir PDF dosyasına **Bates numaralandırması eklemeniz** gerekiyorsa, bu rehber size tamamen çalıştırılabilir bir çözüm sunar. **PDF belgesini nasıl yükleyeceğinizi**, Bates numaralandırma seçeneklerini nasıl yapılandıracağınızı ve numaralandırılmış dosyayı diske nasıl geri yazacağınızı Aspose.PDF for .NET ile göreceksiniz.

Bates numaraları, hukuk, kolluk kuvvetleri ve arşivleme iş akışlarında yaygın olarak kullanılır. Bu öğreticinin sonunda her sayfaya sıralı bir tanımlayıcı gömebilir, önek (prefix) özelleştirebilir ve sayımı istediğiniz herhangi bir sayıdan başlatabilirsiniz.

## Öğrenecekleriniz

* `Aspose.Pdf.Document` nesnesine **PDF belgesi** içeriğini nasıl **yükleyeceğinizi**.  
* `BatesNumberingOptions` ile **Bates numaralandırması** nasıl ekleyeceğinize dair tam adımlar.  
* Değiştirilmiş dosyayı orijinal düzeni ve kalitesi korunarak nasıl kaydedeceğinizi.  

Harici araç gerekmez—sadece Aspose.PDF NuGet paketi ve bir .NET geliştirme ortamı (Visual Studio, VS Code veya Rider) yeterlidir.  

---

## 1. Adım: Aspose.PDF for .NET'i Yükleyin

Proje klasörünüzü bir terminalde açın ve şu komutu çalıştırın:

```bash
dotnet add package Aspose.PDF
```

Paket, bu öğreticide kullanılan tüm sınıfları sağlayan `Aspose.Pdf` ad alanını içerir. Yüklemeden sonra IDE'nin yeni referansı algılaması için projeyi yeniden yükleyin.

## 2. Adım: PDF Belgesini Yükleyin

Kaynak dosyayı yüklemek, Bates numaralandırma motorunun mevcut bir `Document` örneği üzerinde çalışması gerektiği için ilk işlemdir.

```csharp
using Aspose.Pdf;

// ...

// Replace with the path to your input PDF
string inputPath = @"YOUR_DIRECTORY\input.pdf";

// Load the PDF document into memory
Document doc = new Document(inputPath);
```

**Neden Önemlidir:** `Document` sınıfı PDF yapısını ayrıştırır, sayfalara, açıklamalara ve meta verilere erişim sağlar. Dosyayı önce yüklemezseniz hiçbir numaralandırma uygulayamazsınız.

## 3. Adım: Bates Numaralandırma Seçeneklerini Yapılandırın

Bir `BatesNumberingOptions` nesnesi oluşturun ve istediğiniz önek, başlangıç sayısı ve isteğe bağlı biçimlendirme parametrelerini ayarlayın.

```csharp
using Aspose.Pdf;

// ...

BatesNumberingOptions batesOptions = new BatesNumberingOptions
{
    // Text that appears before the numeric part
    Prefix = "CASE01",

    // First number to use (1 means the first page gets CASE01-1)
    StartNumber = 1,

    // Optional: customize the appearance
    // The default places the number in the footer, centered.
    // You can change Font, FontSize, Color, and Position if needed.
    // Example:
    // Font = FontRepository.FindFont("Arial"),
    // FontSize = 10,
    // Color = Color.Black,
    // Margin = new Margin(0, 0, 0, 20)
};
```

**Neden Önemlidir:** `BatesNumberingOptions`, Aspose.PDF'e her sayfa için etiketi nasıl oluşturacağını söyler. `Prefix`, ilgili davaları gruplamanıza yardımcı olurken, `StartNumber` önceki bir partiden devam etmenizi sağlar.

## 4. Adım: Bates Numaraları Uygulanmış PDF'yi Kaydedin

Seçenek nesnesini `Save` metoduna geçirin. Aspose.PDF sayılar doğrudan her sayfaya yazar.

```csharp
// Replace with the desired output path
string outputPath = @"YOUR_DIRECTORY\output.pdf";

// Save the document, applying the Bates numbering
doc.Save(outputPath, batesOptions);
```

**Neden Önemlidir:** `Save(string, BatesNumberingOptions)` aşırı yüklemesi, render adımını numaralandırma süreciyle birleştirir ve çıktının görünür tanımlayıcıları içermesini garanti eder.

## Tam örnek – hepsi bir arada

Aşağıda kopyalayıp yapıştırıp çalıştırabileceğiniz tek bir, bağımsız program bulunmaktadır. **Bates numaralandırması** eklemenin baştan sona nasıl yapılacağını gösterir.

```csharp
using System;
using Aspose.Pdf;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the PDF document
            string inputPath = @"YOUR_DIRECTORY\input.pdf";
            Document doc = new Document(inputPath);

            // 2️⃣ Set up Bates numbering options
            BatesNumberingOptions batesOptions = new BatesNumberingOptions
            {
                Prefix = "CASE01",
                StartNumber = 1,
                // Optional appearance tweaks:
                // Font = FontRepository.FindFont("Times New Roman"),
                // FontSize = 9,
                // Color = Color.DarkBlue,
                // Margin = new Margin(0, 0, 0, 15)
            };

            // 3️⃣ Save the document with Bates numbers
            string outputPath = @"YOUR_DIRECTORY\output.pdf";
            doc.Save(outputPath, batesOptions);

            Console.WriteLine($"Bates numbering added. Output saved to: {outputPath}");
        }
    }
}
```

### Beklenen çıktı

Programı çalıştırdığınızda, her sayfada aşağıdakine benzer bir etiket gösteren `output.pdf` oluşturulur:

```
CASE01-1
CASE01-2
CASE01-3
...
```

Sayılar varsayılan olarak alt bilgi (footer) kısmında görünür, ancak `BatesNumberingOptions` içindeki `Margin` özelliğini ayarlayarak konumlarını değiştirebilirsiniz.

## Köşe durumları ve yaygın varyasyonlar

| Durum | Ne ayarlanmalı |
|-----------|----------------|
| **Parti başına farklı önek** | `Save` çağırmadan önce `Prefix` değerini değiştirin. Farklı öneklerle birden çok belgeyi döngü içinde işleyebilirsiniz. |
| **Önceki bir dosyadan numaralandırmaya devam** | `StartNumber` değerini son kullanılan sayı + 1 olarak ayarlayın. |
| **Sayıları üst bilgiye (header) yerleştir** | `batesOptions.Margin = new Margin(20, 0, 0, 0);` (üst kenar boşluğu) kullanın veya `batesOptions.Position` özelliğini özelleştirin. |
| **Özel yazı tipi veya renk** | Yorum satırında gösterildiği gibi `Font`, `FontSize` ve `Color` özelliklerini atayın. |
| **Büyük PDF'ler (1000+ sayfa)** | İşlem bellek‑verimli; ancak dosya boyutunu azaltmak için kaydetmeden önce `doc.OptimizeResources()` çağırmak isteyebilirsiniz. |

**İpucu:** İş akışınız belge başına farklı numaralandırma şemaları gerektiriyorsa, mantığı bir yardımcı metoda kapsülleyin:

```csharp
static void ApplyBatesNumbering(string src, string dst, string prefix, int start)
{
    var doc = new Document(src);
    var opts = new BatesNumberingOptions { Prefix = prefix, StartNumber = start };
    doc.Save(dst, opts);
}
```

## Sonuç

Artık **Aspose.PDF ile C#'ta herhangi bir PDF'ye Bates numaralandırması eklemeyi** biliyorsunuz. Eğitim, PDF belgesini yükleme, numaralandırma seçeneklerini yapılandırma ve son dosyayı kaydetme adımlarını tek bir çalıştırılabilir programda ele aldı.  

Bundan sonra **su su işareti ekleme**, **birden çok PDF birleştirme** veya **metin çıkarma** gibi ilgili konuları keşfedebilirsiniz. Farklı yazı tipleri, renkler ve konumlarla deney yaparak organizasyonunuzun biçimlendirme standartlarına uyum sağlayın.

Yasal belge iş akışınızı otomatikleştirmeye hazır mısınız? Kodu derleme hattınıza ekleyin, dosya partileri üzerinde çalıştırın ve Aspose.PDF'in ağır işi halletmesine izin verin. İyi kodlamalar!


## Sonraki Öğrenmeniz Gerekenler


Aşağıdaki öğreticiler, bu kılavuzda gösterilen tekniklere dayanarak yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini ustalaşmanız ve projelerinizde alternatif uygulama yaklaşımlarını keşfetmeniz için adım adım açıklamalı tam çalışan kod örnekleri içerir.

- [PDF Belgesi Oluştur C# – Bates Numaralandırması Ekle](/pdf/english/net/programming-with-pdf-pages/create-pdf-document-c-add-bates-numbering/)
- [Bates Numaralandırması PDF – PDF Sayfalarını Numaralandırma Adım Adım Kılavuzu](/pdf/english/net/programming-with-pdf-pages/add-bates-numbering-pdf-step-by-step-guide-to-number-pdf-pag/)
- [Aspose PDF Öğreticisi – Boş Sayfa Ekle ve Bates Numaralandırmasını Güncelle](/pdf/english/net/programming-with-pdf-pages/aspose-pdf-tutorial-insert-a-blank-page-and-update-bates-num/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}