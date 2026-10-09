---
category: general
date: 2026-02-22
description: Aspose.Pdf kullanarak gizli filigran PDF öğreticisi – herhangi bir PDF'in
  ilk sayfasına gizli bir etiket olarak metin damgası eklemeyi öğrenin.
draft: false
keywords:
- confidential watermark pdf
- add confidential label
- aspose pdf watermark
- add stamp first page
- add text stamp pdf
language: tr
og_description: 'Gizli filigran PDF rehberi: Aspose.Pdf for .NET kullanarak ilk sayfaya
  gizli etiketi metin damgası olarak eklemek için adım adım talimatlar.'
og_title: Aspose ile Gizli Filigranlı PDF – Metin Damgası Ekle
tags:
- aspose
- pdf
- watermark
- csharp
title: 'Aspose ile Gizli Filigran PDF: İlk Sayfaya Metin Damgası Ekle'
url: /tr/net/programming-with-stamps-and-watermarks/confidential-watermark-pdf-with-aspose-add-a-text-stamp-to-f/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Confidential watermark PDF – İlk Sayfaya Metin Damgası Nasıl Eklenir

Hiç **confidential watermark PDF**'ye ihtiyaç duydunuz ama sadece ilk sayfaya bir etiket eklemenin nasıl yapılacağını bilemediniz mi? Yalnız değilsiniz—birçok geliştirici “Düzeni bozmadan gizli bir etiket nasıl eklerim?” sorusuyla boğuşuyor.  

İyi haber? Aspose.Pdf for .NET ile bunu sadece birkaç satırda yapabilirsiniz ve sizi sürecin tamamı boyunca adım adım yönlendireceğim. Belirsiz referanslar yok, sadece bugün çalışan tam bir kopyala‑yapıştır çözüm.

## Öğrenecekleriniz

Bu öğreticide şunları ele alacağız:

* Aspose.Pdf NuGet paketinin kurulumu (tek önkoşul).
* Mevcut bir PDF'nin yüklenmesi.
* `TextStamp` kullanarak bir **confidential watermark PDF** oluşturulması.
* **Yalnızca ilk sayfaya** damganın eklenmesi (“add stamp first page” gereksinimi).
* Sonucun kaydedilmesi ve çıktının doğrulanması.

Sonunda, herhangi bir C# projesine ekleyebileceğiniz hazır bir kod parçacığına sahip olacaksınız; ayrıca bu yaklaşımı birden fazla sayfaya ya da farklı damga stillerine ölçeklendirme ipuçları da bulacaksınız.

## Önkoşullar

* .NET 6+ (kod .NET Core ve .NET Framework’te de çalışır).
* Visual Studio 2022 ya da tercih ettiğiniz herhangi bir IDE.
* Aspose.Pdf for .NET – en yeni hata düzeltmeleri için sürüm 23.10 veya üzeri önerilir.

Aspose.Pdf’i projenize henüz eklemediyseniz, şu komutu çalıştırın:

```bash
dotnet add package Aspose.Pdf
```

Hepsi bu—ekstra DLL gerekmez, deneme sürümü için lisans derdi yok (sürüm öncesi lisans anahtarınızı uygulamayı unutmayın).

## Adım 1: Kaynak PDF Belgesini Yükleyin

İlk olarak korumak istediğimiz dosyayı açmamız gerekiyor. `Document` sınıfı tüm PDF’yi temsil eder ve yüklemek sadece yolu vermek kadar basittir.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Path to the PDF you want to watermark
string inputPdfPath = @"C:\MyDocs\input.pdf";

// Load the PDF into memory
using var pdfDocument = new Document(inputPdfPath);
```

*Neden önemli*: Belgeyi yüklemek, damgayı ekleyeceğimiz `Pages` koleksiyonuna erişim sağlar. `using var` kullanmak dosya tutamacının hızlıca serbest bırakılmasını garantiler—büyük toplu işlemler için kritik.

## Adım 2: Gizli Metin Damgası Oluşturun

Şimdi görsel etiketi tasarlıyoruz. `TextStamp` sayesinde boyut, kaydırma ve ölçekleme kontrolü sağlanır. Aşağıdaki ayarlar, *Confidential* kelimesinin taşmadan güzel oturmasını garantiler.

```csharp
// Build a text stamp that says "Confidential"
var confidentialStamp = new TextStamp("Confidential")
{
    // Auto‑adjust the font so it never exceeds the rectangle
    AutoAdjustFontSizeToFitStampRectangle = true,
    AutoAdjustFontSizePrecision = 0.01f,

    // Wrap by whole words—no broken words in the middle
    WordWrapMode = TextFormattingOptions.WordWrapMode.ByWords,

    // Define the stamp rectangle (you can tweak width/height)
    Width = 300,
    Height = 100,

    // Keep the stamp size constant even if the page is resized
    Scale = false
};
```

**Pro ipucu**: Farklı bir font ya da renk ihtiyacınız varsa `confidentialStamp.TextState.Font` ve `confidentialStamp.TextState.ForegroundColor` değerlerini ayarlayın. Örneğin, `confidentialStamp.TextState.Font = FontRepository.FindFont("Arial")` ve `confidentialStamp.TextState.ForegroundColor = Color.Red`.

## Adım 3: Damgayı Yalnızca İlk Sayfaya Ekleyin

Aspose sayfa indekslemesini 1‑tabanlı yapar, bu yüzden `Pages[1]` ilk sayfadır. Damgayı oraya eklemek **add stamp first page** gereksinimini karşılar.

```csharp
// Attach the stamp to the very first page
pdfDocument.Pages[1].AddStamp(confidentialStamp);
```

Tüm sayfalara filigran eklemeniz gerekirse `pdfDocument.Pages` üzerinde döngü kurabilirsiniz. Tek sayfalık etiket için bu tek satır yeterlidir.

## Adım 4: Filigranlı PDF'yi Kaydedin

Son olarak, değiştirilmiş belgeyi diske yazın. Orijinali üzerine yazabilir ya da yeni bir dosya oluşturabilirsiniz—size kalmış.

```csharp
// Destination path for the watermarked PDF
string outputPdfPath = @"C:\MyDocs\Stamped.pdf";

// Persist the changes
pdfDocument.Save(outputPdfPath);
```

`Stamped.pdf` dosyasını açtığınızda, *Confidential* ifadesinin sayfa 1’in sol‑üst köşesinde (veya damgayı konumlandırdığınız yerde) göründüğünü fark edeceksiniz. Belgenin geri kalanı dokunulmamış olarak kalır.

## Beklenen Sonuç

| Önce | Sonra (ilk sayfa) |
|--------|-------------------|
| ![Orijinal PDF sayfası](/images/original.png "Orijinal PDF sayfası") | ![gizli filigran PDF örneği](/images/confidential-watermark.png "gizli filigran PDF örneği") |

*Image alt text*: **gizli filigran PDF örneği** (anahtar kelimeyi içerir).

## Kenar Durumları ve Yaygın Sorular

### PDF'nin sayfaları yoksa ne olur?

`Pages[1]`e erişmeye çalışmak bir `ArgumentOutOfRangeException` fırlatır. Bunun önüne geçmek için:

```csharp
if (pdfDocument.Pages.Count == 0)
    throw new InvalidOperationException("The PDF is empty.");
```

### Birden fazla sayfaya nasıl filigran eklenir?

```csharp
foreach (Page page in pdfDocument.Pages)
{
    page.AddStamp(confidentialStamp);
}
```

Farklı köşelere damga koymak istiyorsanız `confidentialStamp` konumunu sıfırlamayı unutmayın.

### Damganın konumu değiştirilebilir mi?

Evet—`confidentialStamp.HorizontalAlignment` ve `confidentialStamp.VerticalAlignment` ayarlarını kullanın ya da piksel‑tam yerleştirme için `confidentialStamp.XIndent` / `YIndent` değerlerini belirleyin.

### Şifre korumalı PDF'lerde çalışır mı?

Aspose, şifreyi sağladığınız sürece şifreli dosyaları açabilir:

```csharp
var pdfDocument = new Document(inputPdfPath, new LoadOptions { Password = "mySecret" });
```

### Büyük toplu işlemlerde performans nasıl?

Her belgeyi ayrı ayrı yüklemek ve kaydetmek I/O‑ağır olabilir. Tek bir `Document` örneğini bellek içinde yeniden kullanıp, toplu işlem sonunda sadece bir kez kalıcı olarak kaydetmeyi düşünün.

## Tam Çalışan Örnek

Aşağıda, bir konsol uygulamasına kopyala‑yapıştır yapabileceğiniz tam program yer alıyor. Tüm adımları, hata yönetimini ve basit bir doğrulama mesajını içerir.

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
        string inputPdfPath = @"C:\MyDocs\input.pdf";
        if (!System.IO.File.Exists(inputPdfPath))
        {
            Console.WriteLine("Input file not found.");
            return;
        }

        using var pdfDocument = new Document(inputPdfPath);

        if (pdfDocument.Pages.Count == 0)
        {
            Console.WriteLine("The PDF contains no pages.");
            return;
        }

        // -------------------------------------------------
        // 2️⃣ Create the confidential text stamp
        // -------------------------------------------------
        var confidentialStamp = new TextStamp("Confidential")
        {
            AutoAdjustFontSizeToFitStampRectangle = true,
            AutoAdjustFontSizePrecision = 0.01f,
            WordWrapMode = TextFormattingOptions.WordWrapMode.ByWords,
            Width = 300,
            Height = 100,
            Scale = false,
            // Optional styling
            TextState = { FontSize = 24, Font = FontRepository.FindFont("Arial"), ForegroundColor = Color.Red }
        };

        // -------------------------------------------------
        // 3️⃣ Add the stamp to the first page only
        // -------------------------------------------------
        pdfDocument.Pages[1].AddStamp(confidentialStamp);

        // -------------------------------------------------
        // 4️⃣ Save the result
        // -------------------------------------------------
        string outputPdfPath = @"C:\MyDocs\Stamped.pdf";
        pdfDocument.Save(outputPdfPath);

        Console.WriteLine($"Successfully added a confidential watermark PDF. Saved to: {outputPdfPath}");
    }
}
```

Programı çalıştırın, `Stamped.pdf` dosyasını açın ve **confidential watermark PDF**’in tam istediğimiz yerde uygulandığını görün.

## Sonuç

Artık Aspose.Pdf kullanarak herhangi bir PDF’in **ilk sayfasına** **metin damgası** olarak **gizli bir etiket** eklemenin sağlam, üretim‑hazır bir yoluna sahipsiniz. Çözüm tamamen bağımsız, en yeni .NET sürümleriyle çalışıyor ve birden fazla sayfaya, özel fontlara ya da farklı renklere kolayca genişletilebilir.

**Sonraki adımlar** keşfedebileceğiniz şeyler:

* Metin damgasını bir resim damgası (`ImageStamp`) ile değiştirerek bir logo ekleyin.
* Bu yaklaşımı bir döngüyle birleştirerek bir **aspose pdf watermark** oluşturun ve tüm belgeye yayılmasını sağlayın.
* Kodu bir ASP.NET Core API’ye entegre edin; böylece kullanıcılar PDF yükleyebilir ve anında filigranlı sürüm alabilir.

Deneyin, boyutları ayarlayın ve **add text stamp pdf** tekniğinin belge‑güvenliği araç kutunuzda temel bir parça haline gelmesine izin verin. Mutlu kodlamalar!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}