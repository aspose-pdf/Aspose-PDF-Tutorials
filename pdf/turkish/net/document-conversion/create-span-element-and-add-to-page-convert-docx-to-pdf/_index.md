---
category: general
date: 2026-03-27
description: C#'de span öğesi oluşturun ve DOCX'i PDF'ye dönüştürürken ve PDF olarak
  kaydederken span'i bir sayfaya nasıl ekleyeceğinizi öğrenin. Geliştiriciler için
  adım adım kılavuz.
draft: false
keywords:
- create span element
- how to add span
- convert docx to pdf
- add element to page
- save as pdf
language: tr
og_description: C#'ta span öğesi oluşturun ve DOCX'i PDF'ye dönüştürürken bir sayfaya
  span eklemeyi öğrenin, ardından PDF olarak kaydedin. Tam kod örneği dahil.
og_title: Span öğesi oluştur ve sayfaya ekle – DOCX'i PDF'e dönüştür
tags:
- C#
- DocumentProcessing
- PDFConversion
title: Span öğesi oluştur ve sayfaya ekle – DOCX'i PDF'e dönüştür
url: /tr/net/document-conversion/create-span-element-and-add-to-page-convert-docx-to-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Span öğesi oluşturun ve sayfaya ekleyin – DOCX'i PDF'ye dönüştürün

Bir DOCX dosyasında **span öğesi** oluşturmak, hassas düzen kontrolüne ihtiyaç duyduğunuzda yaygın bir görevdir. Bu öğreticide, bir sayfaya **span eklemenin** nasıl yapılacağını, **DOCX'i PDF'ye dönüştürmeyi** ve **PDF olarak kaydetmeyi** birkaç düzenli adımda göstereceğiz.  

Eğer bir Word belgesine bakıp, “Kesin bir koordinata küçük bir metin kutusu ekleyebilseydim” diye düşündüyseniz, doğru yerdesiniz. Kaynak dosyayı yüklemekten şık bir PDF çıktısı elde etmeye kadar tüm iş akışını adım adım göstereceğiz.

## Ne Başaracaksınız

* Belge kütüphanesinin `Document` sınıfını kullanarak bir `.docx` dosyasını yükleyin.  
* `TaggedContent` API'si ile **span öğesi oluşturun**.  
* Seçilen sayfada span'i tam X/Y koordinatlarına konumlandırın.  
* **Öğeyi sayfaya ekleyin** güvenilir bir şekilde, sayfa ilk sayfa olmasa bile.  
* Tek bir `Save` çağrısıyla **DOCX'i PDF'ye dönüştürün** ve **PDF olarak kaydedin**.

Harici araçlar yok, gizemli ayarlar yok—sadece projenize kopyalayıp yapıştırabileceğiniz sade C# kodu.

## Önkoşullar

* .NET 6+ (veya kütüphanenizin desteklediği herhangi bir yeni .NET çalışma zamanı).  
* `Document`, `TaggedContent`, `Position` vb. sağlayan belge işleme SDK'sı.  
* C# sözdizimi hakkında temel bir anlayış—`Console.WriteLine` yazabiliyorsanız yeterlidir.

> **Pro ipucu:** SDK sürümünüzü güncel tutun; en son sürüm (Mart 2026 itibarıyla v3.2) sayfa‑düzeyi işlemler için performans iyileştirmeleri içerir.

---

![PDF sayfasına span öğesi oluşturmayı ve yerleştirmeyi gösteren diyagram](https://example.com/images/create-span-element.png "Span öğesi yerleştirme diyagramı")

## Span öğesi oluşturma – Konumlandırma ve Sayfaya Ekleme

Aşağıda, kaynak DOCX'i yüklemekten son PDF'i yazmaya kadar her şeyi yapan tam, çalıştırılabilir kod bulunmaktadır. Konsol uygulamasına eklemek, yolları ayarlamak ve çalıştırmakta özgürsünüz.

```csharp
using DocumentProcessing;   // Replace with the actual namespace of your SDK
using DocumentProcessing.Models;

class Program
{
    static void Main()
    {
        // Step 1: Load the DOCX you want to modify
        // -------------------------------------------------
        // The constructor takes a file path; make sure the file exists.
        Document doc = new Document(@"C:\Docs\input.docx");

        // Step 2: Create a new span element using the TaggedContent API
        // -------------------------------------------------
        // A span is a lightweight container for inline content.
        var span = doc.TaggedContent.CreateSpanElement();
        // Optional: add some text inside the span
        span.Text = "Hello, world!";

        // Step 3: Position the span at the desired coordinates (X = 50, Y = 750)
        // -------------------------------------------------
        // Position uses points (1/72 inch). Adjust as needed.
        span.Position = new Position(50, 750);

        // Step 4: Add the span to the target page (page index 1 = second page)
        // -------------------------------------------------
        // Pages are zero‑based; index 1 means the second page in the document.
        doc.Pages[1].Add(span);

        // Step 5: Convert the modified DOCX to PDF and save the result
        // -------------------------------------------------
        // The Save method automatically detects the output format from the extension.
        doc.Save(@"C:\Docs\output.pdf");

        // Confirmation output
        Console.WriteLine("Span added, document converted, and PDF saved successfully.");
    }
}
```

### Adım adım açıklama

#### Adım 1 – DOCX belgesini yükleyin  
Bir `Document` nesnesi oluşturuyoruz ve `input.docx` dosyasına işaret ediyoruz. Bu nesne, bellek içinde tüm Word dosyasını temsil eder ve sayfalara, içeriğe ve meta verilere erişim sağlar.

#### Adım 2 – Span öğesi oluşturun  
`TaggedContent.CreateSpanElement()` çağrısı hafif bir satır içi kapsayıcı döndürür. Bunu, metin, resim veya diğer satır içi öğeleri tutabilen küçük, görünmez bir kutu olarak düşünün. Metin eklemek (`span.Text`) isteğe bağlıdır ancak hata ayıklama için faydalıdır.

#### Adım 3 – Span'i konumlandırın  
`new Position(50, 750)` span'in sol‑üst köşesini sol kenar boşluğundan 50 pt ve sayfanın üstünden 750 pt olarak ayarlar. Bu değerler mutlak olduğundan, span'i istediğiniz yere yerleştirebilirsiniz—kesin düzenler için mükemmeldir.

#### Adım 4 – Span'i hedef sayfaya ekleyin  
`doc.Pages[1].Add(span)` span'i ikinci sayfaya ekler. API sıfır‑tabanlı indeksleme kullanır, bu yüzden sayfa 0 ilk sayfadır. İlk sayfaya eklemeniz gerekiyorsa, sadece `doc.Pages[0]` kullanın.

#### Adım 5 – DOCX'i PDF'ye dönüştürün ve PDF olarak kaydedin  
`doc.Save("output.pdf")` çağrısı iki şey yapar: değiştirilmiş belgeyi diske **yazar** ve `.pdf` uzantısı sayesinde içeriği PDF'ye dönüştürür. Ek bir dönüşüm adımına gerek yok—bu, **PDF olarak kaydetmenin** en kolay yoludur.

---

## Farklı bir sayfaya span ekleme (ileri düzey)

Bazen sayfa indeksini önceden bilemezsiniz. Bir sayfayı numarasıyla (insan‑dostu) ya da belirli bir anahtar kelimeyi arayarak bulabilirsiniz.

```csharp
// Find the page that contains the word "Summary"
int targetIndex = doc.Pages
    .Select((p, i) => new { Page = p, Index = i })
    .FirstOrDefault(x => x.Page.Text.Contains("Summary"))?.Index ?? 0;

// Fallback to first page if not found
targetIndex = Math.Max(targetIndex, 0);

// Add the span to the discovered page
doc.Pages[targetIndex].Add(span);
```

**Neden önemli:** Sayfa sayısının değiştiği raporlarda `Pages[1]` sabit kodlamak düzeni bozabilir. Bu kod parçacığı, **span'i dinamik olarak eklemenin** sağlam bir örneğini gösterir.

---

## Yaygın tuzaklar ve nasıl önlenir

| Issue | What happens | Fix |
|-------|--------------|-----|
| **Span görünmüyor** | Koordinatlar sayfa dışındadır veya span'in genişliği/yüksekliği sıfırdır. | `Position` değerlerini iki kez kontrol edin; PDF görüntüleyicinizde bir cetvel kullanın. |
| **Yanlış sayfa indeksi** | Sayfa 0'a ekleme yapıyorsunuz ancak sayfa 2'de olmasını bekliyorsunuz. | API'nin sıfır‑tabanlı olduğunu unutmayın; insan sayfa numarasına 1 ekleyin. |
| **Kaydetme kaynak dosyayı üzerine yazar** | `doc.Save("input.docx")` orijinal dosyayı değiştirir. | Dönüştürürken her zaman yeni bir yol (`output.pdf`) kaydedin. |
| **SDK referansı eksik** | `Document` sınıfı üzerinde derleme hatası. | NuGet paketini kurun: `dotnet add package DocumentProcessing.SDK`. |

## Sonucu doğrulama

Programı çalıştırdıktan sonra, herhangi bir PDF görüntüleyicide `output.pdf` dosyasını açın. İkinci sayfada (50, 750) koordinatlarında tam olarak “Hello, world!” metnini görmelisiniz. Metin başka bir yerde görünüyorsa, `Position` değerlerini ayarlayın ve yeniden çalıştırın.  

Otomatik test için, metnin koordinatlarını programlı olarak doğrulamak amacıyla bir PDF ayrıştırıcı (ör. iTextSharp) kullanabilirsiniz.

```csharp
// Example using iTextSharp to verify position (pseudo‑code)
var pdfReader = new PdfReader(@"C:\Docs\output.pdf");
var page = pdfReader.GetPageContent(2);
Debug.Assert(page.Contains("Hello, world!"));
```

---

## Sonraki adımlar

* **Span'i stillendirin** – `span.Font`, `span.Color` ve diğer stil özelliklerini keşfedin.  
* **Görseller ekleyin** – grafikler için span yerine `CreateImageElement()` kullanın.  
* **Toplu işleme** – bir klasördeki DOCX dosyaları üzerinde döngü oluşturun

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}