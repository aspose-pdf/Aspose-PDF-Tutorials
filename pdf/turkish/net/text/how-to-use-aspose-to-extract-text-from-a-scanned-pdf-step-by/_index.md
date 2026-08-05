---
category: general
date: 2026-08-04
description: Aspose kullanarak taranmış PDF metnini nasıl çıkarılır ve PDF'yi C# ile
  metne dönüştürülür. Taranmış PDF dosyalarını okumayı öğrenin ve güvenilir OCR sonuçları
  elde edin.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use aspose
- extract scanned pdf text
- convert pdf to text
- read scanned pdf
- how to extract text
language: tr
lastmod: 2026-08-04
og_description: Aspose'ı kullanarak taranmış PDF dosyalarını okuma, taranmış PDF metnini
  çıkarma ve PDF'yi metne dönüştürme, tam ve çalıştırılabilir bir örnekle.
og_image_alt: Screenshot showing how to use Aspose OCR copilot to extract text from
  a scanned PDF
og_title: Aspose nasıl kullanılır – C# ile taranmış PDF'lerden metin çıkarma
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: How to use Aspose to extract scanned PDF text and convert PDF to text
    with C#. Learn to read scanned PDF files and get reliable OCR results.
  headline: How to use Aspose to extract text from a scanned PDF – step‑by‑step guide
  type: TechArticle
- questions:
  - answer: Yes. Add `.WithPassword("yourPassword")` to the options builder before
      creating the copilot.
    question: Does this work with password‑protected PDFs?
  - answer: Use `GetTextStructureAsync()` instead of `GetTextAsync()`. The method
      returns a JSON payload that includes page indices, bounding boxes, and confidence
      scores.
    question: Can I extract text in a structured format (e.g., JSON with page numbers)?
  - answer: 'The plain‑text extraction flattens tables into line‑break‑separated rows.
      For richer data, request the PDF‑to‑HTML conversion (`GetHtmlAsync`) and parse
      the HTML table elements. ## Conclusion You now know **how to use Aspose** to
      read a scanned PDF, extract scanned PDF text, and **convert PDF to tex'
    question: What if the PDF contains tables?
  type: FAQPage
tags:
- Aspose.PDF.AI
- OCR
- C#
- PDF processing
title: Taranmış PDF'den metin çıkarmak için Aspose kullanma – adım adım rehber
url: /tr/net/text/how-to-use-aspose-to-extract-text-from-a-scanned-pdf-step-by/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose kullanarak taranmış PDF'ten metin çıkarma – adım adım rehber

OCR için **Aspose nasıl kullanılır** bilmeniz gerekiyorsa, bu rehber C#'ta birkaç satırla taranmış PDF metnini nasıl çıkaracağınızı gösterir. İster bir belge arşivleme hizmeti ister eski evraklar için bir arama indeksi oluşturuyor olun, çözüm Aspose.Pdf.AI hizmetine gönderdiğiniz herhangi bir taranmış PDF ile çalışır.

Bu öğreticide şunları yapacaksınız:

* Taranmış bir PDF okuyan bir OCR yardımcı programı oluşturun.
* Tanımlanan metni asenkron olarak çıkarın.
* Çıkarılan dizeyi gösterin veya daha fazla işleyin.

Tek gereksinim, aktif bir Aspose.Pdf.AI aboneliği ve .NET 6 (veya daha yeni) geliştirme ortamıdır.

## Önkoşullar

| Gereksinim | Neden Önemlidir |
|-------------|----------------|
| .NET 6 SDK veya daha yeni | `async Main` ve modern dil özelliklerini sağlar. |
| Aspose.Pdf.AI NuGet paketi (`Aspose.Pdf.AI`) | `AICopilotFactory` ve OCR seçeneklerini içerir. |
| Geçerli bir Aspose.Pdf.AI `client` örneği (API anahtarı) | İsteklerinizi bulut hizmetine kimlik doğrular. |
| Taranmış bir PDF dosyası (ör., `Scanned.pdf`) | Metnin çıkarılacağı kaynak belge. |

Paketi .NET CLI ile kurun:

```bash
dotnet add package Aspose.Pdf.AI
```

## Adım 1: Aspose.Pdf.AI istemcisini kurun

Herhangi bir OCR uç noktasını çağırmadan önce API kimlik bilgilerinizi tutan bir istemci oluşturmanız gerekir. İstemci iş parçacığı‑güvenlidir ve birden fazla belge için yeniden kullanılabilir.

```csharp
using Aspose.Pdf.AI;
using Aspose.Pdf.AI.Models;

// Replace with your actual API key and base URL if you use a private cloud.
var client = new PdfAiClient(new PdfAiConfiguration
{
    ApiKey = "YOUR_API_KEY",
    // BaseUrl = "https://api.aspose.cloud" // default, change only if needed
});
```

**Bu adımın neden gerekli olduğu** – Aspose hizmeti, her isteği aboneliğinize göre doğrular. İstemciyi bir kez oluşturmak, tekrarlanan ağ el sıkışmalarını önler ve kodun temiz kalmasını sağlar.

## Adım 2: Taranmış PDF belgesi için bir OCR yardımcı programı oluşturun

`AICopilotFactory`, belirttiğiniz dosyayı işleyebilen özel bir OCR yardımcı programı oluşturur. `client` ve PDF yolunu gösteren bir `OpenAIOcrOptions` nesnesi sağlarsınız.

```csharp
using Aspose.Pdf.AI;

// Step 2: Build the OCR copilot
var ocrCopilot = AICopilotFactory.CreateOcrCopilot(
    client,                                   // Your Aspose.Pdf.AI client instance
    OpenAIOcrOptions.Create()
        .WithDocument("YOUR_DIRECTORY/Scanned.pdf") // Path to the scanned PDF
);
```

**Açıklama** – `CreateOcrCopilot`, tüm düşük seviyeli HTTP çağrılarını kapsüller. `WithDocument` yöntemi, hizmete hangi dosyanın analiz edileceğini söyler; PDF bellekte ise bir `Stream` de sağlayabilirsiniz.

## Adım 3: Tanımlanan metni asenkron olarak çıkarın

`GetTextAsync` çağrısı, OCR işlemini bulutta çalıştırır ve düz metin sonucunu döndürür. İşlem birkaç saniye sürebileceği için yöntem asenkrondur.

```csharp
// Step 3: Perform OCR and get the text
string ocrText = await ocrCopilot.GetTextAsync();
```

**Neden asenkron?** – Ağ gecikmesi ve OCR işleme süresi öngörülemez. `await` kullanmak, uygulamanızın ana iş parçacığını engellemesini önler; bu, UI veya web‑servis senaryoları için özellikle önemlidir.

## Adım 4: Çıkarılan metni kullanın

Bu aşamada, taranmış PDF'in tam transkripsiyonunu içeren normal bir .NET `string`'e sahipsiniz. Bu dizeyi konsola yazabilir, bir veritabanına kaydedebilir veya bir arama motoruna besleyebilirsiniz.

```csharp
// Step 4: Display the result
Console.WriteLine("=== OCR Result ===");
Console.WriteLine(ocrText);
```

### Beklenen çıktı

`Scanned.pdf` tek bir sayfada “Hello, world!” cümlesini içeriyorsa, konsol şu çıktıyı gösterir:

```
=== OCR Result ===
Hello, world!
```

Çok sayfalı belgeler için çıktı, her sayfanın metnini birleştirir ve satır sonlarını korur.

## Tam, çalıştırılabilir örnek

Aşağıda, yeni bir konsol projesine (`dotnet new console`) yapıştırabileceğiniz eksiksiz bir program bulunmaktadır. **Aspose nasıl kullanılır** konusunu baştan sona gösterir ve yaygın hatalar için hata yönetimini içerir.

```csharp
using System;
using System.Threading.Tasks;
using Aspose.Pdf.AI;
using Aspose.Pdf.AI.Models;

namespace AsposeOcrDemo
{
    class Program
    {
        static async Task Main(string[] args)
        {
            // 1️⃣ Initialize the Aspose.Pdf.AI client
            var client = new PdfAiClient(new PdfAiConfiguration
            {
                ApiKey = "YOUR_API_KEY"
                // BaseUrl = "https://api.aspose.cloud" // optional
            });

            // 2️⃣ Build the OCR copilot for the target PDF
            var pdfPath = "YOUR_DIRECTORY/Scanned.pdf";
            var ocrCopilot = AICopilotFactory.CreateOcrCopilot(
                client,
                OpenAIOcrOptions.Create().WithDocument(pdfPath)
            );

            try
            {
                // 3️⃣ Extract text asynchronously
                string ocrText = await ocrCopilot.GetTextAsync();

                // 4️⃣ Use the extracted text (display in console)
                Console.WriteLine("=== OCR Result ===");
                Console.WriteLine(ocrText);
            }
            catch (Exception ex)
            {
                // Common errors: invalid API key, missing file, unsupported PDF version
                Console.Error.WriteLine($"Error during OCR: {ex.Message}");
            }
        }
    }
}
```

**Örnekteki ana noktalar**

* `await`, engellemeyen yürütmeyi sağlar.
* `try/catch` bloğu, ağ veya hizmet hatalarını ortaya çıkarır; bu, ölçekli **taranmış PDF** dosyaları okurken esastır.
* Çalıştırmadan önce `YOUR_API_KEY` ve `YOUR_DIRECTORY/Scanned.pdf` değerlerini gerçek değerlerle değiştirin.

## Kenar durumları ve en iyi uygulama ipuçları

| Durum | Önerilen yaklaşım |
|-----------|----------------------|
| **Büyük PDF'ler ( > 50 MB )** | Belgeyi istemci tarafında daha küçük parçalara bölün ve her parçayı ayrı bir yardımcı programla işleyin. Bu, bellek baskısını azaltır ve güvenilirliği artırır. |
| **Düşük kalite taramalar** | OCR kalitesini, `OpenAIOcrOptions`'a `.WithLanguage("eng")` veya `.WithEnhanceImage(true)` ekleyerek ayarlayın. Hizmet, doğruluğu artıran dil ipuçlarını destekler. |
| **Birden fazla dil** | Virgülle ayrılmış bir liste sağlayın, ör. `.WithLanguage("eng,spa")`. OCR motoru her iki dili de algılayıp transkribe eder. |
| **PDF olmayan görüntü dosyaları** | Görüntüyü önce bir PDF'ye dönüştürün (`Aspose.Pdf` kütüphanesi) veya görüntüyü doğrudan göndermek için `OpenAIOcrOptions.WithImage` kullanın. |
| **Hız sınırı aşıldı** | Üstel geri çekilme ve yeniden deneme mantığını uygulayın; Aspose API, kotayı aştığınızda HTTP 429 döndürür. |

### Profesyonel ipucu

Daha sonra yeniden kullanmayı planlıyorsanız `ocrText` sonucunu önbelleğe alın. OCR işlemi, iş akışının en maliyetli kısmıdır ve dizeyi yeniden kullanmak, yinelenen API çağrılarını önler ve kredi tasarrufu sağlar.

## Sıkça Sorulan Sorular

**S: Bu, şifre korumalı PDF'lerde çalışır mı?**  
C: Evet. Yardımcı programı oluşturmadan önce seçenek oluşturucuya `.WithPassword("yourPassword")` ekleyin.

**S: Metni yapılandırılmış bir formatta (ör. sayfa numaralı JSON) çıkarabilir miyim?**  
C: `GetTextAsync()` yerine `GetTextStructureAsync()` kullanın. Yöntem, sayfa indeksleri, sınırlama kutuları ve güven skorlarını içeren bir JSON yükü döndürür.

**S: PDF tablolar içeriyorsa ne olur?**  
C: Düz metin çıkarımı, tabloları satır‑sonu‑ayırılmış satırlara düzleştirir. Daha zengin veri için PDF‑to‑HTML dönüşümünü (`GetHtmlAsync`) isteyin ve HTML tablo öğelerini ayrıştırın.

## Sonuç

Artık **Aspose nasıl kullanılır** bilerek bir taranmış PDF'i okuyabilir, taranmış PDF metnini çıkarabilir ve minimal bir C# programı ile **PDF'yi metne dönüştürebilirsiniz**. Süreç, bir OCR yardımcı programı oluşturmayı, `GetTextAsync`'i çağırmayı ve elde edilen dizeyi işlemeyi içerir. Kenar‑durum önerilerini izleyerek çözümü büyük belge grupları, çok dilli içerik ve güvenli PDF'ler için ölçeklendirebilirsiniz.

Sonraki adımda şunları keşfedebilirsiniz:

* **Metni çıkarma** ve düzen koruması (`GetHtmlAsync`).
* Aspose.Pdf.AI kullanarak **tabloları çıkarmak** ve CSV'ye aktarmak.
* OCR çıktısını Azure Cognitive Search ile bütünleştirerek aranabilir belge arşivleri oluşturmak.

Kodlamaktan keyif alın ve Aspose'un AI destekli OCR'ının taranmış PDF iş akışlarınıza getirdiği doğrulukla mutlu olun!

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan yakından ilgili konuları kapsar. Her kaynak, adım adım açıklamalarla birlikte eksiksiz çalışan kod örnekleri içerir ve ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olur.

- [Aspose.PDF for .NET ile PDF Dosyalarından Metin Çıkarma](/pdf/english/net/text-operations/extract-text-pdf-aspose-dotnet/)
- [Aspose.PDF for .NET ile PDF'lerde Belirli Bölgelerden Metin Çıkarma](/pdf/english/net/text-operations/extract-text-specific-region-aspose-pdf-net/)
- [Aspose.PDF for .NET ile PDF'lerden Vurgulanan Metin Çıkarma](/pdf/english/net/text-operations/extract-highlighted-text-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}