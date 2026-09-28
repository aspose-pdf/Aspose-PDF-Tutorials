---
category: general
date: 2026-02-09
description: Aspose.PDF ile C#'ta PDF imzasını doğrulayın. Dikdörtgen PDF eklemeyi,
  güncellenmiş PDF'yi kaydetmeyi ve Aspose PDF imza özelliklerini kullanmayı öğrenin.
draft: false
keywords:
- verify pdf signature
- add rectangle pdf
- save updated pdf
- aspose pdf signature
- add graphics pdf
language: tr
og_description: PDF imzasını C#'ta hızlıca doğrulayın. Bu kılavuz, PDF'e grafik eklemeyi,
  güncellenmiş PDF'i kaydetmeyi ve Aspose PDF imza API'lerini kullanmayı gösterir.
og_title: PDF imzasını doğrula ve PDF'ye dikdörtgen ekle – Tam Aspose Rehberi
tags:
- Aspose.PDF
- C#
- Digital Signature
- PDF Manipulation
title: Aspose ile PDF imzasını doğrula ve PDF'ye dikdörtgen ekle
url: /tr/net/digital-signatures/verify-pdf-signature-and-add-rectangle-pdf-with-aspose/
---

dikdörtgen ekleme". Keep same heading level.

Proceed.

Paragraphs.

We'll translate accordingly.

Make sure to keep code block placeholders unchanged.

Let's craft final answer.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose ile PDF imzasını doğrulama ve PDF'ye dikdörtgen ekleme

Hiç **pdf imzasını doğrulama** ihtiyacı duydunuz mu ve nereden başlayacağınızı bilemediniz mi? Yalnız değilsiniz—dijital imzalar uyumluluk için zorunlu, ancak birçok geliştirici belgeyi sonradan değiştirmeleri gerektiğinde zorlanıyor.  

Bu öğreticide, **pdf imzasını doğrulayan**, ilk sayfaya bir **dikdörtgen** ekleyen, şeklin sayfa sınırları içinde kaldığını kontrol eden ve sonunda **güncellenmiş pdf'yi kaydeden** tam, çalıştırılabilir bir örnek üzerinden ilerleyeceğiz—hepsi modern Aspose.PDF API'si kullanılarak. Sonunda, herhangi bir .NET çözümüne ekleyebileceğiniz tek bir, bağımsız programınız olacak.

## Öğrenecekleriniz

- Aspose.PDF ile imzalı bir PDF yükleme.
- **aspose pdf signature** sınıflarını kullanarak her imzayı doğrulama ve bozulmaları tespit etme.
- **Add rectangle pdf** grafiklerini güvenli bir şekilde ekleme, sayfaya sığdırma.
- **Save updated pdf** yaparken mevcut imzaları koruma.
- İpuçları, kenar‑durum yönetimi ve yaygın tuzaklar.

Harici dokümanlara ihtiyaç yok—gereken her şey burada.

## Önkoşullar

- .NET 6.0 veya üzeri (kod .NET Framework 4.7+ üzerinde de çalışır).
- Aspose.PDF for .NET NuGet paketi (≥ 23.10). Şu komutla kurun:

```bash
dotnet add package Aspose.Pdf
```

- `signed.pdf` adında, kontrol ettiğiniz bir klasörde bulunan imzalı bir PDF dosyası (koddaki `YOUR_DIRECTORY` kısmını kendi yolunuzla değiştirin).
- C# ve Visual Studio ya da VS Code konusunda temel bilgi.

> **Pro ipucu:** Elinizde imzalı bir PDF yoksa, Aspose sitesinden ücretsiz bir demo dosyası indirip test amaçlı kullanabilirsiniz.

---

## verify pdf signature – Adım Adım

İlk yapmamız gereken belgeyi açmak ve her dijital imzayı döngüyle kontrol etmektir. Aspose.PDF iki kullanışlı yöntem sunar: `VerifySignature` kriptografik kontrolün geçip geçmediğini söylerken, yeni `IsSignatureCompromised` imzadan sonra gerçekleşmiş olabilecek herhangi bir müdahaleyi işaret eder.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Facades;

// Load the signed PDF document
Document pdfDocument = new Document("YOUR_DIRECTORY/signed.pdf");

// Create a signature handler for the document
PdfFileSignature signatureHandler = new PdfFileSignature(pdfDocument);

// Iterate over each signature name in the PDF
foreach (var signatureName in signatureHandler.GetSignNames())
{
    // Verify the cryptographic integrity
    bool isValid = signatureHandler.VerifySignature(signatureName);
    
    // Detect if the signature has been compromised (e.g., document altered)
    bool isCompromised = signatureHandler.IsSignatureCompromised(signatureName);
    
    Console.WriteLine($"{signatureName}: valid={isValid}, compromised={isCompromised}");
}
```

**Neden önemli:**  
- `VerifySignature` yalnızca imzalayanın sertifikasının hâlâ güvenilir olduğunu onaylar.  
- `IsSignatureCompromised` gizli bir nesne eklenmesi gibi ince değişiklikleri yakalar; böylece PDF'nin görsel içeriğinin imzadan sonra değiştirilip değiştirilmediğini bilirsiniz.

**Beklenen çıktı** (iki imza örneği):

```
Signature1: valid=True, compromised=False
Signature2: valid=True, compromised=True
```

Herhangi bir imza `compromised=True` döndürürse, daha fazla işlem yapmamalı ya da kullanıcıyı uyarmalısınız; çünkü belgenin bütünlüğü garanti edilemez.

---

## add rectangle pdf to a page

İmzaların sağlam olduğunu (veya olası bir bozulmayı fark ettiğimizi) onayladıktan sonra, basit bir dikdörtgen grafik ekleyelim. Bu, “İncelendi” damgası koymak, bölümleri vurgulamak ya da sadece bir bölgeye dikkat çekmek için faydalıdır.

```csharp
// Access the first page (pages are 1‑based in Aspose)
Page firstPage = pdfDocument.Pages[1];

// Define a rectangle shape (coordinates: lower-left X, lower-left Y, upper-right X, upper-right Y)
Rectangle shapeRect = new Rectangle(100, 500, 200, 600);

// Add the rectangle to the page's graphics collection
firstPage.AddRectangle(shapeRect);
```

**Sayısal değerlerin anlamı:**  
- PDF koordinat sistemi sol‑alt köşeden başlar.  
- Örnekte, dikdörtgen yatayda 100 puan, dikeyde 100 puan genişliğinde ve tipik bir A4 sayfasının ortasına yerleştirilmiştir.

> **Not:** Daha zengin şekiller istiyorsanız Aspose ayrıca `AddEllipse`, `AddPolygon` vb. yöntemleri de destekler.

---

## check graphics bounds – ensure the rectangle fits

Değişiklikleri kalıcı hale getirmeden önce, grafiklerimizin sayfanın yazdırılabilir alanı içinde kalıp kalmadığını doğrulamak akıllıca olur. Yeni `CheckGraphicsBounds` metodu tam da bunu yapar.

```csharp
// Verify that the rectangle does not exceed page limits
bool shapeFits = firstPage.CheckGraphicsBounds(shapeRect);
Console.WriteLine($"Shape fits page: {shapeFits}");
```

`shapeFits` `false` döndürürse, dikdörtgenin koordinatlarını ayarlamanız gerekir—belki küçültüp sayfanın daha altına taşımalısınız. Bu, özellikle PDF daha sonra yazdırıldığında profesyonel olmayan kırpılmaları önler.

---

## save updated pdf – preserve signatures and new graphics

Son olarak, değiştirilmiş belgeyi diske yazıyoruz. `Save` metodu mevcut imzaları korur; içerik gerçekten değişmediyse (biz zaten `IsSignatureCompromised` ile kontrol ettik) imzaları geçersiz kılmaz.

```csharp
// Save the updated PDF to a new file
pdfDocument.Save("YOUR_DIRECTORY/output.pdf");

// Inform the user
Console.WriteLine("PDF saved as output.pdf with new rectangle.");
```

**Neden yeni bir dosya?**  
Orijinali üzerine kaydetmek, orijinal imzaları silebilir ve önce/sonra durumlarını karşılaştırmayı imkânsız hâle getirebilir. `output.pdf` olarak kaydederek denetim amaçlı kaynağı tutmuş olursunuz.

---

## Full, runnable example

Aşağıda, bir konsol uygulamasına kopyalayıp yapıştırabileceğiniz tam program yer alıyor. Tüm adımlar birleştirilmiş, yorumlar her bloğu açıklıyor ve sonunda beklenen konsol çıktısını göreceksiniz.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Facades;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Load the signed PDF document
        // -------------------------------------------------
        string inputPath = "YOUR_DIRECTORY/signed.pdf";
        Document pdfDocument = new Document(inputPath);
        Console.WriteLine($"Loaded PDF: {inputPath}");

        // -------------------------------------------------
        // 2️⃣ Verify each digital signature and detect compromise
        // -------------------------------------------------
        PdfFileSignature signatureHandler = new PdfFileSignature(pdfDocument);
        foreach (var signatureName in signatureHandler.GetSignNames())
        {
            bool isValid = signatureHandler.VerifySignature(signatureName);
            bool isCompromised = signatureHandler.IsSignatureCompromised(signatureName);
            Console.WriteLine($"{signatureName}: valid={isValid}, compromised={isCompromised}");
        }

        // -------------------------------------------------
        // 3️⃣ Access the first page and add a rectangle
        // -------------------------------------------------
        Page firstPage = pdfDocument.Pages[1];
        Rectangle shapeRect = new Rectangle(100, 500, 200, 600);
        firstPage.AddRectangle(shapeRect);
        Console.WriteLine("Added rectangle to page 1.");

        // -------------------------------------------------
        // 4️⃣ Ensure the rectangle fits inside the page bounds
        // -------------------------------------------------
        bool shapeFits = firstPage.CheckGraphicsBounds(shapeRect);
        Console.WriteLine($"Shape fits page: {shapeFits}");

        // -------------------------------------------------
        // 5️⃣ Save the updated PDF
        // -------------------------------------------------
        string outputPath = "YOUR_DIRECTORY/output.pdf";
        pdfDocument.Save(outputPath);
        Console.WriteLine($"Saved updated PDF as: {outputPath}");
    }
}
```

**Beklenen konsol çıktısı** (tek geçerli, bozulmamış bir imza varsayımı):

```
Loaded PDF: YOUR_DIRECTORY/signed.pdf
Signature1: valid=True, compromised=False
Added rectangle to page 1.
Shape fits page: True
Saved updated PDF as: YOUR_DIRECTORY/output.pdf
```

İmza bozulmuşsa, `compromised=True` görecek ve devam edip etmeyeceğinize karar verebileceksiniz.

---

## Common questions & edge‑case handling

| Question | Answer |
|----------|--------|
| **What if the PDF has no signatures?** | `GetSignNames()` boş bir koleksiyon döndürür; döngü atlanır ve yine de grafik ekleyebilirsiniz. |
| **Can I add multiple rectangles?** | Evet—farklı `Rectangle` nesneleriyle `AddRectangle` metodunu tekrar tekrar çağırabilirsiniz. |
| **What about password‑protected PDFs?** | Doğrulamadan önce `pdfDocument = new Document("file.pdf", new LoadOptions("password"));` ile yükleyin. |
| **Will adding graphics invalidate a valid signature?** | Yalnızca imzanın kapsadığı sayfaya grafik eklenirse geçersiz olur. Bunu `IsSignatureCompromised` ile tespit edin; aksi takdirde imza aynı kalır. |
| **Do I need to close resources?** | Aspose.PDF nesneleri yönetilir; `using` bloğu eklemek isteğe bağlıdır ancak ekstra güvenlik için kullanılabilir. |

---

## Pro tips for production use

- **Batch processing:** Tüm prosedürü giriş/çıkış yollarını alan bir metoda sarın; ardından dosya listelerini `Parallel.ForEach` ile işleyerek hızı artırın.  
- **Logging:** `Console.WriteLine` yerine bir logger (ör. Serilog) kullanarak doğrulama sonuçlarını denetim izlerine kaydedin.  
- **Signature policy:** Daha katı uyumluluk için `VerifySignature` ile birlikte sertifika iptal kontrolü (OCSP/CRL) ekleyin.  
- **Graphics styling:** `firstPage.AddRectangle(shapeRect, new GraphicState { StrokeColor = Color.Red, FillColor = Color.Yellow });` gibi stil ayarlarıyla dikdörtgeni öne çıkarın.  
- **Version lock:** Kütüphane güncellemelerinde kırılma riskini önlemek için Aspose.PDF NuGet sürümünü sabitleyin.

---

## Conclusion

Artık **verify pdf signature**, **add rectangle pdf** ve **save updated pdf** işlemlerini en yeni Aspose.PDF API'leriyle gerçekleştiren sağlam, uç‑uç örneğe sahipsiniz. Kod, bozulmuş imzaları kontrol eder, grafiklerin sayfa sınırları içinde kalmasını sağlar ve orijinal dijital imzaları korur—gerçek dünya uyumluluk akışının tam ihtiyacını karşılar.

Sonraki adımlarınız şunlar olabilir:

- **add graphics pdf** gibi filigranlar veya QR kodları eklemek.  
- **aspose pdf signature** API'sini kullanarak programatik yeni imzalar oluşturmak.  
- ASP.NET Core web servisi içinde süreci otomatikleştirerek anlık belge doğrulama sağlamak.

Deneyin, dikdörtgen koordinatlarını ayarlayın ve kütüphanenin farklı PDF yapılarıyla nasıl davrandığını görün. İyi kodlamalar, PDF'leriniz hem imzalı hem de şık olsun! 

![verify pdf signature example](image.png "verify pdf signature example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}