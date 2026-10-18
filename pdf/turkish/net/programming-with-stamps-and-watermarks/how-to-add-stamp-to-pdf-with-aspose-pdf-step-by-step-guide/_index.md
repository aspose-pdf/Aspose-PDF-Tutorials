---
category: general
date: 2026-03-24
description: C#'ta Aspose.Pdf kullanarak bir PDF'ye damga ekleme. Bir damga PDF'si
  yerleştirmeyi ve otomatik boyutlandırmalı metin damgası PDF'si eklemeyi birkaç kolay
  adımda öğrenin.
draft: false
keywords:
- how to add stamp
- place stamp pdf
- add text stamp pdf
- Aspose.Pdf stamp example
- C# PDF annotation
language: tr
og_description: C#'ta bir PDF'ye damga nasıl eklenir? Bu rehber, Aspose.Pdf kullanarak
  damga PDF'si yerleştirmeyi ve otomatik yazı tipi boyutlandırmasıyla metin damgası
  eklemeyi gösterir.
og_title: Aspose.Pdf ile PDF'ye Damga Ekleme – Hızlı Rehber
tags:
- pdf
- csharp
- aspose
- stamping
title: Aspose.Pdf ile PDF'e Damga Ekleme – Adım Adım Rehber
url: /tr/net/programming-with-stamps-and-watermarks/how-to-add-stamp-to-pdf-with-aspose-pdf-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Pdf ile PDF'ye Damga Ekleme – Adım Adım Kılavuz

**How to add stamp** to a PDF, bir belgeyi markalamak, onaylamak ya da sadece açıklama eklemek istediğinizde yaygın bir ihtiyaçtır. Düşük seviyeli grafiklerle uğraşmadan bir damgayı PDF'ye yerleştirmenin en kolay yolunu hiç merak ettiniz mi? Bu öğreticide, sadece **how to add stamp** göstermekle kalmayıp, her satırın *neden* önemli olduğunu da açıklayan, tamamen çalıştırılabilir bir çözümü adım adım inceleyeceğiz.

Herhangi bir sayfaya **place stamp PDF** eklemeyi, dikdörtgenine otomatik olarak sığacak şekilde küçülen **add text stamp PDF** nasıl ekleyeceğinizi ve metin çok uzun olduğunda kaçınılması gereken tuzakları öğreneceksiniz. Sonunda projenize ekleyebileceğiniz tek bir C# dosyanız olacak ve PDF'lere hemen damga eklemeye başlayacaksınız.

## Önkoşullar

* .NET 6.0 veya daha yeni bir sürüm (kod .NET Core ve .NET Framework ile de çalışır).
* Aspose.Pdf for .NET NuGet paketi (`Aspose.Pdf`) yüklü.
* `input.pdf` adlı bir PDF dosyası, başvurabileceğiniz bir klasörde (herhangi basit tek sayfalı PDF yeterlidir).

Ek bir yapılandırma gerekmez—Aspose.Pdf tüm zor işleri halleder.

## Adım 1: Projeyi Kurun ve Kaynak PDF'yi Yükleyin

İlk olarak ihtiyacımız olan, eklemek istediğimiz PDF'yi temsil eden bir `Document` nesnesidir. Bunu, daha sonra üzerine damga çizeceğimiz boş bir tuval olarak düşünebilirsiniz.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Load the source PDF document
// The using statement ensures the file is closed automatically.
using var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");
```

> **Neden önemli:** `Document`, Aspose.Pdf'de herhangi bir PDF manipülasyonu için giriş noktasıdır. `using` desenini kullanarak dosya tutamacının serbest bırakılmasını garanti ederiz; bu da değiştirilmiş PDF'yi daha sonra kaydetmeye çalıştığınızda dosya kilitlenmesi sorunlarını önler.

## Adım 2: Otomatik Boyut Ayarlamalı Yazı Damgası Oluşturun

Şimdi bir `TextStamp` oluşturuyoruz. Bu örneği öne çıkaran püf noktası, `AutoAdjustFontSizeToFitStampRectangle` bayrağıdır—bu, Aspose'a metni tanımladığımız dikdörtgen içine sığana kadar küçültmesini söyler.

```csharp
// Create a text stamp that will automatically resize to fit its rectangle
var textStamp = new TextStamp("Long text that must fit")
{
    // Let Aspose shrink the text if it overflows
    AutoAdjustFontSizeToFitStampRectangle = true,
    // Precision of the auto‑adjust algorithm (lower = more accurate)
    AutoAdjustFontSizePrecision = 0.01f,
    // Define the stamp's bounding box (in points)
    Width = 300,
    Height = 100,
    // Word‑wrap by whole words so we don’t split in the middle of a word
    WordWrapMode = TextFormattingOptions.WordWrapMode.ByWords,
    // Optional: set background color or opacity if you want a visible box
    Background = new Background()
    {
        Color = Color.LightGray,
        Opacity = 0.5
    }
};
```

> **Pro ipucu:** Metin yerine bir logo veya görüntüye ihtiyacınız varsa, `ImageStamp` kullanın—görüntü ölçeklendirme için aynı otomatik ayarlama mantığı mevcuttur.

## Adım 3: **Place Stamp PDF**'nin Nerede Olacağını Seçin – İlk Sayfa, Son Sayfa veya Özel İndeks

Aspose.Pdf, sayfaları 1‑tabanlı bir koleksiyonda saklar (`pdfDocument.Pages[1]` ilk sayfadır). İndeksi değiştirerek **place stamp PDF**'yi istediğiniz sayfaya ekleyebilirsiniz.

```csharp
// Place the stamp on the first page (index 1)
// To stamp the last page use pdfDocument.Pages[pdfDocument.Pages.Count]
pdfDocument.Pages[1].AddStamp(textStamp);
```

> **Neden esnek:** `Pages` koleksiyonu değiştirilebilir olduğu için, tüm sayfalarda döngü yaparak aynı damgayı her birine ekleyebilir ya da iş mantığına göre belirli bir sayfayı hedefleyebilirsiniz (ör. sadece kapak sayfası).

## Adım 4: Değiştirilmiş Belgeyi Kaydedin

Damga ekledikten sonra değişiklikleri diske yazmanız gerekir. Orijinal dosyanın üzerine yazabilir ya da yeni bir dosya oluşturabilirsiniz—size kalmış.

```csharp
// Save the stamped PDF – change the path if you don’t want to overwrite
pdfDocument.Save("YOUR_DIRECTORY/output-stamped.pdf");
```

`output-stamped.pdf` dosyasını açtığınızda, ilk sayfada “Long text that must fit” metnini içeren açık gri bir dikdörtgen göreceksiniz. Metin daha uzun olsaydı, Aspose otomatik olarak metni 300 × 100 pt dikdörtgenin içine mükemmel şekilde sığana kadar küçültecekti.

## Tam Çalışan Örnek

Aşağıda, bir konsol uygulamasına (`Program.cs`) kopyalayıp yapıştırabileceğiniz tam program bulunmaktadır. Tartıştığımız tüm parçaları ve damganın göründüğünü doğrulamak için küçük bir yardımcıyı içerir.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Drawing;   // Needed for Background and Color

namespace PdfStampDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the source PDF
            using var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");

            // 2️⃣ Create a text stamp with auto‑adjusting font size
            var textStamp = new TextStamp("Long text that must fit")
            {
                AutoAdjustFontSizeToFitStampRectangle = true,
                AutoAdjustFontSizePrecision = 0.01f,
                Width = 300,
                Height = 100,
                WordWrapMode = TextFormattingOptions.WordWrapMode.ByWords,
                Background = new Background()
                {
                    Color = Color.LightGray,
                    Opacity = 0.5
                }
            };

            // 3️⃣ Place the stamp on the first page (you can change the index)
            pdfDocument.Pages[1].AddStamp(textStamp);

            // 4️⃣ Save the result
            string outputPath = "YOUR_DIRECTORY/output-stamped.pdf";
            pdfDocument.Save(outputPath);

            Console.WriteLine($"Stamp added successfully! Check the file at: {outputPath}");
        }
    }
}
```

### Beklenen Sonuç

* PDF, ilk sayfada yarı saydam gri bir kutu ile açılır.
* Kutu içinde sağlanan metin mükemmel şekilde sığar, daha uzun bir cümleyle değiştirseniz bile.
* Manuel yazı tipi boyutu hesaplamalarına gerek yok—Aspose işi halleder.

## **Place Stamp PDF** Kullanırken Yaygın Tuzaklar

| Belirti | Muhtemel Neden | Çözüm |
|---------|----------------|-------|
| Metin kesiliyor | `AutoAdjustFontSizeToFitStampRectangle` **false** veya dikdörtgen çok küçük. | Bayrağı etkinleştirin ve `Width`/`Height` değerlerini artırın ya da metin uzunluğunu azaltın. |
| Damga merkezin dışında görünüyor | Varsayılan `HorizontalAlignment`/`VerticalAlignment` `Left`/`Top`. | `HorizontalAlignment = HorizontalAlignment.Center` ve `VerticalAlignment = VerticalAlignment.Center` olarak ayarlayın. |
| Damga bazı görüntüleyicilerde görünmüyor | Arka plan opaklığı 0 olarak ayarlanmış veya damga rengi sayfa arka planıyla aynı. | Çelişkili bir `Background.Color` kullanın veya `Opacity` > 0.3 ayarlayın. |
| Birden fazla damga üst üste geliyor | Koordinatlar ayarlanmadan döngü içinde damgalar ekleniyor. | Her damgayı kaydırmak için `textStamp.XIndent` ve `textStamp.YIndent` kullanın. |

Bu sorunları erken ele almak, ileride çok fazla hata ayıklamaktan sizi kurtarır.

## Örneği Genişletmek: Görüntü Damgası Ekleme

Eğer **add text stamp PDF** *ve* bir görüntü (ör. şirket logosu) eklemeniz gerekiyorsa, ikisini birleştirebilirsiniz:

```csharp
var imageStamp = new ImageStamp("YOUR_DIRECTORY/logo.png")
{
    Width = 100,
    Height = 50,
    XIndent = 400,          // Position to the right of the text stamp
    YIndent = 20,
    Background = new Background()
    {
        Color = Color.Transparent
    }
};

pdfDocument.Pages[1].AddStamp(imageStamp);
```

Şimdi sayfa, yan yana bir dinamik metin damgası ve statik bir görüntü damgası gösteriyor.

## Uygulamanızı Test Etme

1. Konsol uygulamasını çalıştırın.  
2. `output-stamped.pdf` dosyasını Adobe Reader, Edge veya herhangi bir PDF görüntüleyicide açın.  
3. Damga dikdörtgeninin mevcut olduğunu ve metnin tamamen görünür olduğunu doğrulayın.  
4. Metni daha uzun bir ifadeye değiştirin, yeniden çalıştırın ve yazı tipinin otomatik olarak küçüldüğünü onaylayın.

Herhangi bir şey yanlış görünüyorsa, dikdörtgen boyutlarını ve `AutoAdjustFontSizePrecision` ayarını tekrar kontrol edin.

## Sonuç

Artık Aspose.Pdf kullanarak bir PDF'ye **how to add stamp** eklemeyi, belirli bir sayfaya **place stamp PDF** yerleştirmeyi ve yazı tipini otomatik olarak ayarlayan **add text stamp PDF** oluşturmayı biliyorsunuz. Yukarıdaki tam, çalıştırılabilir örnek tahminleri ortadan kaldırır ve dosyaları toplu işleme veya koşullu filigran ekleme gibi daha gelişmiş damga senaryoları için sağlam bir temel sağlar.

Bir sonraki adıma hazır mısınız? Her sayfada döngü içinde damga eklemeyi deneyin, farklı yazı tipleriyle oynayın veya profesyonel bir mühür oluşturmak için görüntü ve metin damgalarını birleştirin. Gökyüzü sınırdır ve Aspose.Pdf ile motorunuz güvenilir bir şekilde çalışır.

Herhangi bir sorunla karşılaşırsanız, bir yorum bırakın veya daha derin özelleştirme seçenekleri için Aspose.Pdf belgelerine göz atın. Damgalama keyifli olsun!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}