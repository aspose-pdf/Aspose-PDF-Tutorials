---
category: general
date: 2026-08-04
description: PDF dosyaları için görüntü açıklaması oluşturacak AI Copilot'u oluşturun.
  OpenAI görüntü seçeneklerini nasıl yapılandıracağınızı ve görüntü açıklamasını verimli
  bir şekilde nasıl çıkaracağınızı öğrenin.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create AI copilot
- generate image description
- image description PDF
- OpenAI image options
- extract image description
language: tr
lastmod: 2026-08-04
og_description: PDF dosyaları için görüntü açıklaması oluşturacak bir AI Copilot oluşturun.
  Bu öğreticide, OpenAI görüntü seçeneklerini nasıl yapılandıracağınızı, copilotu
  nasıl çalıştıracağınızı ve C#'ta görüntü açıklamasını nasıl çıkaracağınızı gösteriyoruz.
og_image_alt: Screenshot of C# code that creates an AI copilot for PDF image description
og_title: PDF Görüntü Açıklaması İçin AI Copilot Oluşturma – Tam Kılavuz
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Create AI Copilot to generate image description for PDF files. Learn
    how to configure OpenAI image options and extract image description efficiently.
  headline: Create AI Copilot for PDF image description – step‑by‑step guide
  type: TechArticle
tags:
- Aspose.Pdf.AI
- C#
- PDF processing
title: PDF Görsel Açıklaması İçin AI Copilot Oluşturma – Adım Adım Rehber
url: /tr/net/programming-with-images/create-ai-copilot-for-pdf-image-description-step-by-step-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PDF Görüntü Açıklaması için AI Copilot Oluşturma – Tam Kılavuz

PDF içinde gömülü görüntüler için otomatik olarak açıklamalar yazan bir **AI Copilot** oluşturmanız gerekiyorsa, bu kılavuz tam olarak nasıl yapılacağını gösterir. OpenAI görüntü seçeneklerini yapılandırmayı, copilotu çalıştırmayı ve **görüntü açıklamasını** C# projenizden çıkmadan öğrenebileceksiniz.

PDF görüntüleri için metin içeriği oluşturmak, erişilebilirlik, içerik indeksleme ve otomatik raporlama için yaygın bir gereksinimdir. Bu öğreticinin sonunda, işaret ettiğiniz herhangi bir PDF belgesi için **görüntü açıklaması** üreten yeniden kullanılabilir bir bileşene sahip olacaksınız.

## Prerequisites

Başlamadan önce şunların yüklü olduğundan emin olun:

* .NET 6.0 veya daha yeni bir sürüm yüklü  
* Bir Aspose.Pdf.AI lisansı (veya ücretsiz deneme)  
* Aspose istemcisinin kullanabileceği bir OpenAI API anahtarı  
* Visual Studio 2022 (veya C# destekleyen herhangi bir IDE)  

`Aspose.Pdf.AI` dışındaki ek NuGet paketlerine gerek yok.

## Step 1: Set up the Aspose.Pdf.AI client

İlk adım, kimlik doğrulama bilgilerinizle AI istemcisini örneklemektir. İstemci, OpenAI hizmetiyle iletişimi arka planda yönetir.

```csharp
using Aspose.Pdf.AI;
using Aspose.Pdf.AI.Models;

// Replace with your actual credentials
var client = new AiClient(new AiClientOptions
{
    ApiKey = Environment.GetEnvironmentVariable("OPENAI_API_KEY"),
    // Optional: set a custom endpoint if you use Azure OpenAI
    // Endpoint = "https://my-openai-instance.openai.azure.com/"
});
```

**Neden Önemlidir:** `AiClient`, istek‑seviyesi ayarların (API anahtarı, zaman aşımı, yeniden deneme politikası) tamamını kapsar. Bunu bir kez oluşturup birden çok copilot örneği arasında yeniden kullanmak, yükü azaltır ve tutarlı kimlik doğrulamayı sağlar.

## Step 2: Create an Image Description Copilot

Şimdi PDF'i okuyacak ve her görüntü için bir açıklama üretecek **AI copilot**'u oluşturacaksınız. `CreateImageDescriptionCopilot` fabrikası, istemciyi ve açıklamanın nasıl üretileceğini tanımlayan bir dizi seçeneği kabul eder.

```csharp
// Configure OpenAI image options – this is where you control model, temperature, etc.
var imageOptions = OpenAIImageDescriptionOptions.Create()
    .WithModel("gpt-4o-mini")           // Choose a model that balances cost and quality
    .WithTemperature(0.7)               // Controls creativity; 0 = deterministic
    .WithMaxTokens(150);                // Maximum length of each description

// Point the copilot at the PDF you want to process
var imgCopilot = AICopilotFactory.CreateImageDescriptionCopilot(
    client,
    imageOptions.WithDocument(@"C:\Reports\AnnualReport.pdf"));
```

**Neden Önemlidir:**  
* `OpenAIImageDescriptionOptions` (**OpenAI image options**) dil modelini ince ayar yapmanızı sağlar. Sıcaklık veya model ayarlarını değiştirerek teknik diyagramlar ile doğal fotoğraflar arasındaki alaka düzeyini artırabilirsiniz.  
* Belge yolunu belirtmek, copilotun hangi PDF'i tarayacağını söyler. Copilot, her raster görüntüyü çıkarır, modele gönderir ve insan tarafından okunabilir bir açıklama döndürür.

## Step 3: Retrieve the generated description asynchronously

Copilot, birkaç megabaytlık görüntü verisini yüklemesi ve modelin yanıtını beklemesi gerektiği için asenkron çalışır. Sonucu almadan önce çağrının tamamlanmasını sağlamak için `await` kullanın.

```csharp
try
{
    // Get a dictionary where the key is the page number and the value is the description
    var descriptionMap = await imgCopilot.GetDescriptionAsync();

    // Example: iterate over each image description
    foreach (var entry in descriptionMap)
    {
        Console.WriteLine($"Page {entry.Key}: {entry.Value}");
    }
}
catch (AiException ex)
{
    Console.Error.WriteLine($"AI service error: {ex.Message}");
}
```

**Neden Önemlidir:** Metot, her sayfa (veya görüntü indeksi) ile açıklamasını eşleyen bir `Dictionary<int, string>` döndürür. `AiException` yakalamak, uygulamanın çökmesi yerine ağ veya kota hatalarını ortaya çıkarmanızı sağlar.

## Step 4: Display or store the description

Açıklamaları konsola, bir günlük dosyasına yazabilir veya erişilebilirlik için PDF'e alt‑metin olarak gömebilirsiniz. Aşağıda, çıktıyı daha sonra tüketmek üzere bir JSON dosyasına yazan hızlı bir örnek yer alıyor.

```csharp
using System.Text.Json;

// Serialize the map to JSON
var json = JsonSerializer.Serialize(descriptionMap, new JsonSerializerOptions { WriteIndented = true });
File.WriteAllText(@"C:\Reports\ImageDescriptions.json", json);

Console.WriteLine("Image descriptions saved to ImageDescriptions.json");
```

**Neden Önemlidir:** Çıktıyı JSON olarak saklamak, her sayfa ile açıklama arasındaki ilişkiyi korur ve sonraki süreçlerin (arama indeksleme, UI render etme vb.) veriyi kolayca tüketmesini sağlar.

## Handling multiple images per page

Bir sayfada birkaç görüntü varsa, copilot açıklamaları satır sonlarıyla ayrılmış birleştirilmiş bir metin olarak döndürür. Bunları ayırmak için ham sonucu inceleyin ve `\n\n` (çift yeni satır) üzerinden bölün. İşte yardımcı bir yöntem:

```csharp
static IEnumerable<string> SplitDescriptions(string combined)
{
    return combined.Split(new[] { "\n\n" }, StringSplitOptions.RemoveEmptyEntries);
}
```

Gerekirse her bir görüntü açıklaması üzerinde döngü kurabilir ve ayrı ayrı depolayabilirsiniz.

## Edge case: Large PDFs and timeout management

100 MB'den büyük bir PDF işlemek, varsayılan HTTP zaman aşımını aşabilir. `AiClient` oluştururken istemcinin zaman aşımı ayarını şu şekilde değiştirin:

```csharp
var client = new AiClient(new AiClientOptions
{
    ApiKey = Environment.GetEnvironmentVariable("OPENAI_API_KEY"),
    Timeout = TimeSpan.FromMinutes(5)   // Increase timeout for heavy workloads
});
```

Zaman aşımını artırmak, hizmet yüksek çözünürlüklü görüntüleri işlerken erken sonlandırmayı önler.

## Pro tip: Cache results to reduce cost

OpenAI, token başına ücret alır ve aynı raporun farklı sürümlerinde görüntü açıklamaları tekrarlayabilir. JSON çıktısını önbelleğe alın ve PDF hash'i daha önce işlenmiş bir dosyayla eşleştiğinde yeniden kullanın. Bu uygulama maliyeti düşürür ve sonraki çalıştırmaları hızlandırır.

```csharp
static string ComputeFileHash(string path)
{
    using var sha256 = System.Security.Cryptography.SHA256.Create();
    using var stream = File.OpenRead(path);
    var hash = sha256.ComputeHash(stream);
    return Convert.ToHexString(hash);
}
```

Hash'i JSON dosyasıyla birlikte saklayın; daha sonraki bir çalıştırmada hash eşleşirse AI çağrısını atlayın.

## Full runnable example

Her şeyi bir araya getirerek, yeni bir .NET projesine yapıştırabileceğiniz bağımsız bir konsol uygulaması aşağıdadır.

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using System.Text.Json;
using System.Threading.Tasks;
using Aspose.Pdf.AI;
using Aspose.Pdf.AI.Models;

class Program
{
    static async Task Main()
    {
        // 1️⃣ Initialize AI client
        var client = new AiClient(new AiClientOptions
        {
            ApiKey = Environment.GetEnvironmentVariable("OPENAI_API_KEY"),
            Timeout = TimeSpan.FromMinutes(5)
        });

        // 2️⃣ Configure OpenAI image options and create copilot
        var imageOptions = OpenAIImageDescriptionOptions.Create()
            .WithModel("gpt-4o-mini")
            .WithTemperature(0.7)
            .WithMaxTokens(150);

        string pdfPath = @"C:\Reports\AnnualReport.pdf";

        var imgCopilot = AICopilotFactory.CreateImageDescriptionCopilot(
            client,
            imageOptions.WithDocument(pdfPath));

        // 3️⃣ Retrieve descriptions
        Dictionary<int, string> descriptionMap;
        try
        {
            descriptionMap = await imgCopilot.GetDescriptionAsync();
        }
        catch (AiException ex)
        {
            Console.Error.WriteLine($"Error from AI service: {ex.Message}");
            return;
        }

        // 4️⃣ Output results
        foreach (var entry in descriptionMap)
        {
            Console.WriteLine($"Page {entry.Key}:");
            Console.WriteLine(entry.Value);
            Console.WriteLine(new string('-', 40));
        }

        // 5️⃣ Save to JSON for later use
        string json = JsonSerializer.Serialize(descriptionMap, new JsonSerializerOptions { WriteIndented = true });
        string jsonPath = Path.ChangeExtension(pdfPath, ".descriptions.json");
        await File.WriteAllTextAsync(jsonPath, json);
        Console.WriteLine($"Descriptions saved to {jsonPath}");
    }
}
```

**Beklenen çıktı (kısaltılmış)**

```
Page 2:
A bar chart showing quarterly revenue growth, with blue bars representing Q1–Q4.
----------------------------------------
Page 5:
A high‑resolution photograph of the new manufacturing facility, showing the assembly line in operation.
...
Descriptions saved to C:\Reports\AnnualReport.descriptions.json
```

Program `AnnualReport.pdf` dosyasını okur, bir **AI copilot** oluşturur ve her sayfayı oluşturulan açıklamasıyla eşleyen bir JSON dosyası yazar.

## Common questions

* **Şifreli PDF'lerde çalışır mı?**  
  Evet, ancak copilot oluştururken şifreyi sağlamalısınız:  
  `imageOptions.WithPassword("mySecret")`.

* **İşlemeyi belirli sayfalara sınırlayabilir miyim?**  
  Copilotu 1‑10 sayfalarına sınırlamak için `imageOptions.WithPageRange(1, 10)` kullanın.

* **Bir görüntü metin içeriyorsa ne olur?**  
  Model görsel içeriği tanımlamaya çalışır; OCR‑tarzı metin çıkarımı için `CreateTextExtractionCopilot` kullanmalısınız.

## Conclusion

Artık PDF dosyaları için **görüntü açıklaması** üreten **AI Copilot** oluşturmayı, **OpenAI image options** yapılandırmayı ve **görüntü açıklamasını** C# içinde programatik olarak çıkarmayı biliyorsunuz. Tam örnek, async işleme, hata yönetimi ve sonuç önbellekleme gibi en iyi uygulamaları gösterir.

Sonraki adımda şunları keşfedebilirsiniz:

* Oluşturulan açıklamaları PDF'e alt‑metin olarak ekleyerek erişilebilirliği artırmak (`PdfDocument` → `PdfImage.AlternativeText`).  
* Aynı copilot desenini toplu işleme için **görüntü açıklaması PDF** raporları oluşturmak amacıyla kullanmak.  
* Farklı OpenAI modelleri veya sıcaklık ayarlarıyla deney yaparak açıklama stilini ince ayarlamak.

Kodu istediğiniz gibi uyarlamaktan, daha büyük belgelerle denemeler yapmaktan ve çıktıyı indeksleme hattınıza entegre etmekten çekinmeyin. İyi kodlamalar!

## What Should You Learn Next?

Aşağıdaki öğreticiler, bu kılavuzda gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini ustalaşmanız ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmeniz için adım adım açıklamalar içeren tam çalışan kod örnekleri sunar.

- [Java'da Etiketli Görüntülü PDF Oluştur](/pdf/hindi/java/pdf-structure-elements/create-pdf-with-tagged-image-in-java/)
- [Etiketli Görüntülü PDF Oluştur](/pdf/hindi/net/programming-with-tagged-pdf/create-pdf-with-tagged-image/)
- [Dotnet'te Etiketli PDF Görüntüsü Oluştur](/pdf/hindi/net/images-graphics/create-tagged-pdf-image-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}