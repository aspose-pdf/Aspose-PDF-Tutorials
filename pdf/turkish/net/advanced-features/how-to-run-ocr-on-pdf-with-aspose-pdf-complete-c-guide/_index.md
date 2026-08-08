---
category: general
date: 2026-03-22
description: C#'ta Aspose.Pdf kullanarak PDF dosyalarında OCR nasıl çalıştırılır.
  Tarama ile oluşturulmuş PDF'yi dönüştürmeyi, PDF'yi aranabilir hâle getirmeyi ve
  PDF belgesini zahmetsizce yüklemeyi öğrenin.
draft: false
keywords:
- how to run OCR
- run OCR on pdf
- convert scanned pdf
- make pdf searchable
- load pdf document
language: tr
og_description: Aspose.Pdf ile PDF dosyalarında OCR nasıl çalıştırılır? Bu öğreticide
  taranmış PDF'yi nasıl dönüştüreceğinizi, PDF'yi aranabilir hâle getireceğinizi ve
  C#'ta PDF belgesini nasıl yükleyeceğinizi gösteriyoruz.
og_title: PDF'de OCR Nasıl Çalıştırılır – Tam C# Rehberi
tags:
- OCR
- Aspose.Pdf
- C#
- PDF processing
title: Aspose.Pdf ile PDF'de OCR Nasıl Çalıştırılır – Tam C# Rehberi
url: /tr/net/advanced-features/how-to-run-ocr-on-pdf-with-aspose-pdf-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PDF Üzerinde OCR Çalıştırma – Tam C# Kılavuzu

PDF dosyalarında OCR çalıştırmak, taranmış evraklarla uğraşırken sıkça karşılaşılan bir engeldir. Taranmış bir faturada arama yapmaya çalıştığınızda bir duvara çarptınız mı? Yalnız değilsiniz. Bu öğreticide, Aspose.Pdf kullanarak **run OCR on PDF** adımlarını tam olarak göstereceğiz, bulanık bir taramayı tamamen aranabilir bir belgeye dönüştüreceğiz. Sonunda ayrıca **convert scanned PDF**, **make PDF searchable** ve tabii ki **load PDF document** nesnelerini sorunsuz bir şekilde nasıl kullanacağınızı da öğreneceksiniz.

Projeyi kurmaktan çıktıyı doğrulamaya kadar her şeyi ele alacağız. El sallama, “belgelere bak” kısayolları yok—bugün Visual Studio’ya yapıştırabileceğiniz tam, çalıştırılabilir bir örnek. .NET 6 ya da .NET Framework 4.8 ile çalışıp çalışmadığını merak ediyorsanız, cevap evet; Aspose.Pdf her ikisini de destekliyor ve aşağıdaki kod otomatik olarak uyum sağlıyor.

## Önkoşullar

- **Aspose.Pdf for .NET** (Mart 2026 itibarıyla en yeni sürüm). NuGet üzerinden alabilirsiniz: `Install-Package Aspose.Pdf`.
- İşlemek istediğiniz bir **scanned PDF** (örneğin `YOUR_DIRECTORY/input.pdf` gibi referans verebileceğiniz bir klasöre koyun).
- .NET 6 SDK veya daha yenisi (sözdizimi `using var` C# 8 ve üzeri tarafından desteklenir).
- Seçtiğiniz bir IDE—Visual Studio, Rider veya VS Code hepsi sorunsuz çalışır.

Hepsi bu. Ek OCR motorları, harici hizmetler yok. Aspose’un yerleşik `OcrPlugin`i işi halleder.

## OCR Çalıştırma – Temel Adımlar

Aşağıda tam, bağımsız bir program yer alıyor. `Program.cs` olarak kaydedin ve çalıştırın; konsol sessizce sonlanacak ve giriş dosyasının yanında aranabilir bir PDF bulacaksınız.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Plugins;

class Program
{
    static void Main()
    {
        // Step 1: Load the PDF document you want to OCR
        using var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");

        // Step 2: Create a PluginManager – this is the hub for all PDF plugins
        var pluginManager = new PluginManager();

        // Step 3: Register the built‑in OCR plugin (the one that actually reads the image)
        pluginManager.RegisterPlugin(new OcrPlugin());

        // Step 4: Prepare execution options – here we set English as the language.
        // You can add more languages by comma‑separating them, e.g., "eng,spa".
        var ocrOptions = new PluginExecutionOptions
        {
            Parameters = { ["Language"] = "eng" }
        };

        // Step 5: Execute the OCR plugin on the loaded document.
        // This mutates pdfDocument in‑place, turning each scanned page into searchable text.
        pluginManager.Execute(pdfDocument, ocrOptions);

        // Step 6: Save the OCR‑processed PDF to a new file.
        pdfDocument.Save("YOUR_DIRECTORY/ocr-output.pdf");

        Console.WriteLine("OCR complete! Output saved to ocr-output.pdf");
    }
}
```

### Kodun yaptığı şey, adım adım

1. **Load PDF Document** – `Document` yapıcısı dosyayı belleğe okur. Bu, “load pdf document” gereksinimini karşılar ve üzerinde çalışabileceğimiz değiştirilebilir bir nesne sağlar.
2. **Plugin Manager** – Aspose, isteğe bağlı özellikleri (ör. OCR) bir yönetici aracılığıyla izole eder. Bunu, doğru çekiçte bulunabileceğiniz bir alet kutusu gibi düşünün.
3. **Register OCR Plugin** – `RegisterPlugin(new OcrPlugin())` çağrısıyla Aspose’a optik karakter tanıma (OCR) yapacağımızı bildiririz.
4. **Execution Options** – `PluginExecutionOptions` işlemi ince ayar yapmanıza olanak tanır. `Language`ı `"eng"` olarak ayarlamak, motorun İngilizce karakterlere bakmasını sağlar. İsterseniz `"spa"` (İspanyolca) ya da `"deu"` (Almanca) ekleyebilirsiniz.
5. **Run the OCR** – `pluginManager.Execute` her sayfayı dolaşır, raster görüntüyü çıkarır, OCR motorunu çalıştırır ve görünmez bir metin katmanı ekler. Bu, **run OCR on pdf**in özüdür.
6. **Save the Result** – Son PDF artık gizli bir metin katmanı içerir ve **make PDF searchable** olur. Adobe Reader’da Bul (Find) aracını kullanarak yazdığınız herhangi bir kelimeyi bulabilirsiniz.

## Adım 1: PDF Belgesi Yükleme

`using var` yerine düz `new Document()` kullanmadığımızı merak edebilirsiniz. `using` ifadesi, işimiz bittiğinde dosya tutamacının hemen serbest bırakılmasını garantiler; bu, Windows’ta aynı dosyanın üzerine daha sonra yazmaya çalıştığınızda kritik öneme sahiptir.

```csharp
using var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");
```

Yol hatalıysa, Aspose bir `FileNotFoundException` fırlatır. Klasör izinlerinizi iki kez kontrol edin—özellikle Linux’ta büyük/küçük harf duyarlılığı sizi yakalayabilir.

## Adım 2: OCR Eklentisini Kaydet ve Yapılandır

OCR eklentisi, çekirdek kütüphaneyi hafif tutmak için varsayılan olarak yüklenmez. Kaydetmek tek satırdır, ancak iş akışınız gerektiriyorsa birden fazla eklentiyi (ör. filigran kaldırıcı) zincirleyebilirsiniz.

```csharp
var pluginManager = new PluginManager();
pluginManager.RegisterPlugin(new OcrPlugin());
```

> **Pro tip:** Yüzlerce PDF’i toplu olarak işlemek istiyorsanız, `PluginManager`ı bir kez örnekleyip yeniden kullanın. Dosya başına oluşturmak gereksiz yük getirir.

## Adım 3: OCR İşlemini Çalıştır (Convert Scanned PDF)

Şimdi asıl iş burada. `Execute` metodu her sayfayı tarar, OCR’u çalıştırır ve metni PDF’e yazar. Verimli—Aspose görüntü verisini akış olarak işler, bu sayede 200 sayfalık taramalarda bile belleğiniz tükenmez.

```csharp
var ocrOptions = new PluginExecutionOptions
{
    Parameters = { ["Language"] = "eng" }
};

pluginManager.Execute(pdfDocument, ocrOptions);
```

**Why set the language?** OCR doğruluğu büyük ölçüde dil modeline bağlıdır. `"eng"` sağlamak, motorun İngilizce karakter şekillerine öncelik vermesini sağlar ve yanlış pozitifleri azaltır.

## Adım 4: Aranabilir PDF'yi Kaydet ve Doğrula

Kaydetmek basittir, ancak doğrulama birçok geliştiricinin takıldığı yerdir. Çalıştırdıktan sonra çıktıyı herhangi bir PDF görüntüleyicide açın ve **Ctrl + F** kısayolunu deneyin. Başlangıçta sadece görüntü olan kelimeleri bulabiliyorsanız, **make PDF searchable** işlemini başarıyla tamamlamışsınız demektir.

```csharp
pdfDocument.Save("YOUR_DIRECTORY/ocr-output.pdf");
```

![OCR sonrası Aranabilir PDF – PDF üzerinde OCR nasıl çalıştırılır](/images/ocr-searchable.png "PDF üzerinde OCR nasıl çalıştırılır sonrasında oluşan aranabilir PDF")

*Yukarıdaki ekran görüntüsü, bir terim aradığınızda gizli metin katmanının vurgulandığını gösterir.*

## Yaygın Tuzaklar ve Pro İpuçları

| Sorun | Neden Oluşur | Çözüm |
|-------|--------------|-------|
| **Blank output** | Dil parametresi eksik veya desteklenmeyen bir kodla ayarlanmış. | `["Language"] = "eng"` (veya başka bir ISO‑639‑2 kodu) olduğundan emin olun. |
| **Slow processing** | Küçültülmemiş büyük görüntüler. | `Parameters["Resolution"] = "300"` ekleyerek OCR’un daha düşük DPI’da çalışmasını sağlayın. |
| **Missing fonts** | OCR metin oluşturur ancak görüntüleyici fontu render edemez. | `pdfDocument.FontEmbeddingMode = FontEmbeddingMode.Always` ayarıyla fontları gömün. |
| **Memory leaks** | `Document` nesnesi serbest bırakılmıyor. | Gösterildiği gibi `using var` kullanın veya `pdfDocument.Dispose()` manuel olarak çağırın. |

### Kenar Durumları

- **Multi‑language PDFs:** Karışık içerik için `"eng,spa,fra"` gibi virgülle ayrılmış bir liste gönderin.
- **Password‑protected files:** `new Document("file.pdf", new LoadOptions { Password = "secret" })` ile yükleyin.
- **Selective OCR:** Sadece belirli sayfaları OCRlamak istiyorsanız, bir `PageRange` nesnesi oluşturup `Parameters["Pages"] = "1-3,5"` şeklinde geçin.

## Özet: Ne Başardık

- **How to run OCR on PDF** using Aspose.Pdf’s built‑in plugin.
- **Convert scanned PDF** into a searchable version without external services.
- **Make PDF searchable** so end‑users can find text instantly.
- **Load PDF document** safely and release resources promptly.

Tüm bunlar temiz C# koduyla 30 satırın altında.

## Sonraki Denemeler

- Çok dilli sözleşmeleri OCRlamak için farklı dilleri deneyin.
- OCR’u **text extraction** (`pdfDocument.Pages[i].ExtractText()`) ile birleştirerek otomatik veri girişi sağlayın.
- OCR’dan önce hassas bilgileri temizlemek için **Redaction plugin**i kullanın, uyumluluğu sağlayın.
- Kodu bir mikroservis olarak bir API uç noktasının arkasına dağıtın; böylece geliştirici olmayanlar taramaları yükleyip anında aranabilir PDF alabilir.

Bulut ortamına ölçeklendirme veya Azure Functions entegrasyonu hakkında sorularınız mı var? Yorum bırakın, bu senaryoları birlikte keşfedelim. Mutlu kodlamalar!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}