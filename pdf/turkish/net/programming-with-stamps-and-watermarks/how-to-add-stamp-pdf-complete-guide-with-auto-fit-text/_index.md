---
category: general
date: 2026-06-30
description: Aspose.PDF kullanarak PDF'ye damga ekleme ve PDF'de metni otomatik sığdırma.
  Tam kod, açıklamalar ve ipuçlarıyla adım adım öğretici.
draft: false
keywords:
- how to add stamp pdf
- adjust font size to fit
- auto‑fit text in pdf
language: tr
og_description: Damga PDF ekleme kolaylaştı. Aspose.PDF ile dakikalar içinde PDF’de
  metni sığdırmak ve otomatik sığdırmak için yazı tipi boyutunu ayarlamayı öğrenin.
og_title: PDF'ye damga ekleme – Otomatik Sığdırma Metin Öğreticisi
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: How to add stamp pdf using Aspose.PDF and auto‑fit text in pdf. Step‑by‑step
    tutorial with full code, explanations, and tips.
  headline: How to add stamp pdf – Complete guide with auto‑fit text
  type: TechArticle
- description: How to add stamp pdf using Aspose.PDF and auto‑fit text in pdf. Step‑by‑step
    tutorial with full code, explanations, and tips.
  name: How to add stamp pdf – Complete guide with auto‑fit text
  steps:
  - name: Expected Output
    text: Open `autoFontStamp.pdf` in any PDF viewer. You should see a rectangular
      label on the first page, **exactly 300 × 100 points**, containing the phrase
      “Long text that must fit”. If the original string is longer than the rectangle
      can accommodate at the default font size, you’ll notice the text has sh
  - name: 1. Multiple Stamps on One Page
    text: If you need several annotations, simply repeat the `AddStamp` call with
      different `TextStamp` instances. Remember to adjust `XIndent` and `YIndent`
      to position each stamp.
  - name: 2. Changing Font Family or Color
    text: 'You can customize the appearance via the `TextState` property:'
  - name: 3. Using Images Instead of Text
    text: Aspose also supports `ImageStamp`. The same auto‑fit logic doesn’t apply,
      but you can manually size the image to the stamp rectangle.
  type: HowTo
tags:
- pdf
- aspnet
- stamp
- font-size
title: PDF'ye damga ekleme – Otomatik sığdırma metniyle tam rehber
url: /tr/net/programming-with-stamps-and-watermarks/how-to-add-stamp-pdf-complete-guide-with-auto-fit-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PDF'ye Damga Ekleme – Otomatik Uyumlu Metin ile Tam Kılavuz

PDF'ye damga eklemek, bir belgeyi GUI editörü açmadan açıklama eklemeniz gerektiğinde sıkça sorulan bir sorudur. Uzun bir etiketi bir PDF sayfasına bırakıp kenarlardan taşmasını izlediniz mi? Bu öğreticide **Aspose.PDF for .NET** kullanarak bu sorunu çözecek ve **yazı tipini otomatik olarak sığdırma** özelliğini nasıl etkinleştireceğinizi göstereceğiz.

Kodun her satırını adım adım inceleyecek, her ayarın neden önemli olduğunu açıklayacak ve damganın gerçekten dikdörtgeni içinde kalacak şekilde küçülüp (veya büyüyüp) kaldığını kanıtlayan tam çalışan bir PDF ile bitireceğiz. Belirsiz referanslar yok – bugün çalıştırabileceğiniz somut bir kopyala‑yapıştır çözümü.

## Gereksinimler

İlerlemeye başlamadan önce şunların yüklü olduğundan emin olun:

* **.NET 6.0** veya daha yeni bir sürüm (kod .NET Framework 4.7+ üzerinde de çalışır).  
* **Aspose.Pdf** NuGet paketi (`Install-Package Aspose.Pdf`).  
* `input.pdf` adlı bir PDF dosyası, referans verebileceğiniz bir klasörde bulunmalı (biz buna `YOUR_DIRECTORY` diyeceğiz).  
* İstediğiniz herhangi bir IDE – Visual Studio, Rider ya da hatta VS Code yeterli.

Hepsi bu. Harici hizmetler, lisans hileleri yok (Aspose, test için gömebileceğiniz ücretsiz bir deneme anahtarı sunar). Hazır mısınız? Başlayalım.

## PDF'ye Damga Ekleme – Adım 1: Kaynak Belgeyi Yükleyin

İlk yapmanız gereken, değiştirmek istediğiniz PDF’i açmaktır. Aspose.PDF bir dosyayı `Document` nesnesi olarak ele alır; bu sayede sayfalara, açıklamalara ve tabii ki damgalara erişebilirsiniz.

```csharp
using Aspose.Pdf;

// Step 1: Open the source PDF document
using (var document = new Document(@"YOUR_DIRECTORY\input.pdf"))
{
    // The using‑statement ensures the file is closed properly.
```

> **Neden önemli:**  
> Belgeyi bir `using` bloğu içinde açmak, tüm dosya tutucularının serbest bırakılmasını garanti eder ve PDF’i daha sonra kaydetmeye ya da silmeye çalıştığınızda “dosya kilitli” hatalarının oluşmasını önler.

## Yazı Tipini Otomatik Sığdır – TextStamp’i Yapılandırma

Şimdi bir `TextStamp` nesnesi oluşturacağız. Bu, sayfada gerçekten görünecek parçadır. **AutoAdjustFontSizeToFitStampRectangle** özelliğini etkinleştirip bir hassasiyet değeri ayarladığımızda sihir gerçekleşir.

```csharp
    // Step 2: Create a text stamp and enable automatic font size adjustment
    var stamp = new TextStamp("Long text that must fit")
    {
        // Shrink or expand text to fit the stamp area automatically
        AutoAdjustFontSizeToFitStampRectangle = true,

        // Precision for the size calculation (0.01 = 1% tolerance)
        AutoAdjustFontSizePrecision = 0.01f,

        // Define the rectangle that the stamp must stay inside
        Width = 300,   // points (approx 4.2 inches)
        Height = 100,  // points (approx 1.4 inches)

        // Keep the original text scaling; we only want font size to change
        Scale = false
    };
```

> **İpucu:** Çok dilli metinle çalışıyorsanız, eksik glif sorunlarından kaçınmak için `stamp.TextState.Font = FontRepository.FindFont("Arial Unicode MS");` satırını da ekleyin.

> **Neden işe yarar:**  
> `AutoAdjustFontSizeToFitStampRectangle`, Aspose’a `Width` ve `Height` ile tanımlanan dikdörtgenin içine hâlâ sığacak en büyük yazı tipi boyutunu hesaplamasını söyler. `AutoAdjustFontSizePrecision` ise bu hesabın ne kadar ince ayarlı olacağını belirler – daha küçük sayılar daha sıkı bir uyum sağlar ancak işlem süresi biraz artar.

## PDF'de Otomatik Uyumlu Metin – Damgayı Sayfaya Ekleyin

Damga yapılandırıldıktan sonra bir sonraki adım, onu belirli bir sayfaya yerleştirmektir. Bu örnek için ilk sayfayı kullanacağız, ancak istediğiniz herhangi bir indeksi hedefleyebilirsiniz (`document.Pages[3]` üçüncü sayfa için gibi).

```csharp
    // Step 3: Add the stamp to the first page of the PDF
    document.Pages[1].AddStamp(stamp);
```

> **Sık sorulan soru:** *PDF’de hiç sayfa yoksa ne olur?*  
> Aspose bir `ArgumentOutOfRangeException` fırlatır. Kodu daha dayanıklı hâle getirmek için hızlı bir koruma satırı ekleyin (`if (document.Pages.Count == 0) throw new InvalidOperationException("PDF is empty.");`).

## PDF’yi Kaydet – Sonucu Doğrulayın

Son olarak değişiklikleri diske yazıyoruz. Çıktı dosya adı, damganın yazı tipi boyutunun otomatik ayarlandığını açıkça gösterir.

```csharp
    // Step 4: Save the modified PDF with the auto‑adjusted stamp
    document.Save(@"YOUR_DIRECTORY\autoFontStamp.pdf");
} // End of using block – document is disposed here
```

### Beklenen Çıktı

`autoFontStamp.pdf` dosyasını herhangi bir PDF görüntüleyicide açın. İlk sayfada **tam olarak 300 × 100 point** boyutunda bir dikdörtgen etiket görmelisiniz; içinde “Long text that must fit” ifadesi yer alır. Orijinal metin, dikdörtgenin varsayılan yazı tipi boyutunda sığamayacak kadar uzunsa, metnin tam olarak sığacak şekilde küçüldüğünü fark edeceksiniz – kesilme ya da taşma yok.

![Screenshot of PDF with auto‑fit stamp](https://example.com/auto-fit-stamp.png "auto‑fit text in pdf example")
*Alt metin: Otomatik uyumlu damga ile PDF ekran görüntüsü, ayarlanmış yazı tipi boyutunu gösteriyor.*

## Kenar Durumları ve Varyasyonlar

### 1. Tek Sayfada Birden Çok Damga

Birden fazla açıklama eklemeniz gerekiyorsa, farklı `TextStamp` örnekleriyle `AddStamp` çağrısını tekrarlamanız yeterlidir. Her damgayı konumlandırmak için `XIndent` ve `YIndent` değerlerini ayarlamayı unutmayın.

```csharp
stamp.XIndent = 50;   // horizontal offset from the left edge
stamp.YIndent = 150;  // vertical offset from the bottom edge
document.Pages[1].AddStamp(stamp);
```

### 2. Yazı Tipi Ailesi veya Renk Değiştirme

Görünümü `TextState` özelliği üzerinden özelleştirebilirsiniz:

```csharp
stamp.TextState.Font = FontRepository.FindFont("Times New Roman");
stamp.TextState.FontSize = 12; // base size; auto‑adjust will override if needed
stamp.TextState.ForegroundColor = Color.FromRgb(255, 0, 0); // red text
```

### 3. Metin Yerine Görüntü Kullanma

Aspose ayrıca `ImageStamp`’i destekler. Aynı otomatik‑uyum mantığı geçerli değildir, ancak görüntüyü damga dikdörtgenine manuel olarak boyutlandırabilirsiniz.

```csharp
var imgStamp = new ImageStamp(@"YOUR_DIRECTORY\logo.png")
{
    Width = 200,
    Height = 80,
    XIndent = 20,
    YIndent = 20
};
document.Pages[1].AddStamp(imgStamp);
```

## Uygulamalı İpuçları

* **Yolları sabit kodlamayın** – taşınabilirlik için `Path.Combine(Environment.CurrentDirectory, "input.pdf")` kullanın.  
* **Toplu işleme** – tüm prosedürü `foreach (var file in Directory.GetFiles(...))` döngüsü içinde sararak yüzlerce PDF’i otomatik olarak damgalayın.  
* **Performans** – büyük PDF’ler işliyorsanız, `AutoAdjustFontSizePrecision` değerini `0.05f` olarak ayarlayarak görsel farkı ihmal edip hesaplamayı hızlandırabilirsiniz.  
* **Test** – ilk çalıştırmadan sonra oluşan PDF’i mutlaka açın ve dikdörtgen boyutlarının beklentinizle eşleştiğini doğrulayın. Hızlı bir görsel kontrol, ileride saatler süren hata ayıklamayı önler.

## Sonuç

Artık **PDF'ye damga ekleme** ve **yazı tipini otomatik sığdırma** işlemlerini Aspose.PDF kullanarak tamamen kopyala‑yapıştır bir çözümle yapabiliyorsunuz. Belgeyi yükleyip, otomatik ayarlı bir `TextStamp` yapılandırıp, istediğiniz sayfaya yerleştirip ve dosyayı kaydederek, metin taşması konusunda endişe duymadan programatik olarak PDF’leri açıklayabilirsiniz.

Sırada ne var? Bu tekniği veri‑odaklı iş akışlarıyla birleştirin – veritabanından müşteri adlarını çekip her faturayı bir döngü içinde damgalayın. Ya da farklı dikdörtgen boyutlarıyla deney yaparak otomatik‑uyum algoritmasının çok kısa ve çok uzun metinlerde nasıl davrandığını keşfedin.

Paylaşmak istediğiniz bir varyasyon mu var? Yorum bırakın ya da yeni bir proje başlatın ve otomatik‑uyum sihrinin işini görmesine izin verin. Mutlu kodlamalar!

## Sonraki Öğrenmeniz Gerekenler

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak tam çalışan kod örnekleri ve adım‑adım açıklamalar içerir.

- [Aspose.PDF for .NET Kullanarak PDF’lere Metin Damgası Ekleme](/pdf/english/net/document-manipulation/add-text-stamp-pdf-aspose-dotnet/)
- [Aspose.PDF for .NET Kullanarak PDF’lerde Metin Damgalarını Ekleyip Hizalama | Watermarks & Backgrounds](/pdf/english/net/watermarks-backgrounds/add-text-stamp-aspose-pdf-dotnet/)
- [Aspose.PDF for .NET Kullanarak PDF’e Görüntü Damgası Ekleme: Kapsamlı Rehber](/pdf/english/net/images-graphics/add-image-stamp-pdf-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}