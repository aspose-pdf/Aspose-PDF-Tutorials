---
category: general
date: 2026-04-06
description: JPG'den hızlıca PDF oluşturun ve PDF içinde resmi nasıl kırpacağınızı,
  yeni PDF sayfası eklemeyi ve C# kullanarak kırpma ile JPG'yi PDF'ye dönüştürmeyi
  öğrenin.
draft: false
keywords:
- create pdf from jpg
- crop image in pdf
- how to add new pdf page
- convert jpg to pdf with crop
- insert image into pdf c#
language: tr
og_description: JPG'den PDF oluşturun ve PDF içinde resmi C# ile kırpın. Yeni PDF
  sayfası eklemeyi ve JPG'yi kırpmalı olarak PDF'ye dönüştürmeyi öğrenin.
og_title: C#'ta JPG'den PDF Oluşturma – Adım Adım Rehber
tags:
- Aspose.Pdf
- C#
- PDF generation
title: C#'ta JPG'den PDF Oluşturma – Kırpma ve Yeni Sayfalarla Tam Kılavuz
url: /tr/net/document-conversion/create-pdf-from-jpg-in-c-full-guide-with-cropping-and-new-pa/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# JPG'den PDF Oluşturma C#'ta – Kırpma ve Yeni Sayfalarla Tam Kılavuz

Hiç **create PDF from JPG** yapmanız gerekti ama sadece istediğiniz kısmı nasıl tutacağınızdan emin olamadınız mı? Yalnız değilsiniz. Birçok uygulamada—faturalar, makbuzlar veya fotoğraf‑kitapları düşünün—geliştiriciler bir resmi PDF'e dönüştürürken istenmeyen kenarları atmak zorunda kalıyor.  

Bu öğreticide, **creates PDF from JPG** yapan, **crop image in PDF** nasıl yapılır gösteren ve birden fazla resim gerektiğinde **how to add new pdf page** nasıl eklenir konularını kapsayan eksiksiz, çalıştırılabilir bir çözümü adım adım inceleyeceğiz. Sonunda **convert JPG to PDF with crop** ve **insert image into PDF C#** işlemlerini Aspose.Pdf kütüphanesiyle nasıl yapacağınızı da öğreneceksiniz.

## What You’ll Learn

- Aspose.Pdf'i bir .NET projesine kurma (ağır yapılandırma gerektirmez).  
- JPEG'i yükleme, tutmak istediğiniz alanı tanımlama ve PDF sayfasına eklerken kırpma.  
- Aynı belgeye ek sayfalar ekleyerek birçok görüntüden çok‑sayfalı PDF'ler oluşturma.  
- Son dosyayı kaydetme ve çıktıyı doğrulama.  

**Prerequisites:** .NET 6+ (veya .NET Framework 4.6+), Visual Studio 2022 veya tercih ettiğiniz herhangi bir editör, ve `Aspose.Pdf` NuGet referansı. Başka bir dış hizmete ihtiyaç yok.

![Create PDF from JPG example](image.jpg){: .align-center alt="Kırpılmış bir görüntünün PDF sayfasına yerleştirildiğini gösteren JPG'den PDF oluşturma örneği"}

---

## Step 1: Install Aspose.Pdf and Prepare Your Project

İlk olarak—Aspose.Pdf paketini ekleyin. Çözüm klasörünüzde bir terminal açın ve şu komutu çalıştırın:

```bash
dotnet add package Aspose.Pdf
```

Bu tek satır, daha sonra kullanacağımız `Document`, `Rectangle` ve `Page` sınıflarını da içeren her şeyi indirir. Benim deneyimime göre, NuGet yolu DLL'lerle uğraşmadan güncel kalmanın en temiz yoludur.

> **İpucu:** .NET Framework hedefliyorsanız, `Aspose.Pdf.NET` paketini kullanın; API yapısı aynı kalır.

---

## Step 2: Load the JPEG and Define the Page Size

Son PDF sayfası için istediğimiz boyutlarla eşleşen bir tuval (canvas) ihtiyacımız var. Aşağıdaki kod yeni bir `Document` oluşturur ve kaynak görüntüyü bir akış (stream) olarak açar.

```csharp
using Aspose.Pdf;
using System.IO;

// Create a new PDF document – this will hold our pages.
using var pdfDocument = new Document();

// Open the JPEG you want to convert.
using var imageStream = File.OpenRead(@"C:\Images\photo.jpg");

// Define the full‑size rectangle (the page) – 600 × 800 points works well for most photos.
var pageBounds = new Rectangle(0, 0, 600, 800);
```

Neden bir dikdörtgen? Aspose.Pdf'te bir `Rectangle`, hem sayfa boyutlarını hem de görüntünün gösterilmek istenen bölgesini temsil eder. *sayfayı* *kırpma alanından* ayırarak PDF üzerinde neyin görüneceği üzerinde ince ayar yapabilirsiniz.

---

## Step 3: Choose the Crop Area (Upper‑Left Quarter)

Sadece fotoğrafın sol‑üst çeyreğine ihtiyacınız olduğunu varsayalım. Bu bölgeyi sayfa boyutuna göre şöyle hesaplarız:

```csharp
// Crop the upper‑left quarter of the image.
var cropArea = new Rectangle(
    pageBounds.LLX,                                 // left X (0)
    pageBounds.LLY + pageBounds.Height / 2,         // bottom Y (halfway up)
    pageBounds.LLX + pageBounds.Width / 2,          // right X (halfway across)
    pageBounds.URY);                                // top Y (full height)
```

`Rectangle` yapıcı (constructor) **lower‑left X/Y** ve **upper‑right X/Y** değerlerini alır. Yüksekliğin yarısını `LLY`'ye ekleyerek kırpmanın alt kısmını yukarı kaydırır, böylece görüntünün alt yarısı atılır. Farklı bir bölüm isterseniz bu hesaplamaları ayarlayın.

> **Neden eklemeden önce kırpma yapılır?**  
> PDF tarafında kırpma, diskte geçici bir bitmap oluşturmayı önler, hem I/O hem de bellek tasarrufu sağlar. Aspose matematiği sizin yerinize halleder ve sonuç temiz, vektör‑dostu bir PDF olur.

---

## Step 4: Add a New Page and Insert the Cropped Image

Şimdi görüntüyü bir PDF sayfasına yerleştiriyoruz. İşte **how to add new pdf page** ifadesinin devreye girdiği nokta.

```csharp
// Add a new page to the document.
var page = pdfDocument.Pages.Add();

// Insert the image using both the page bounds and the crop rectangle.
page.AddImage(imageStream, pageBounds, cropArea);
```

`AddImage` üç argüman alır:

1. **Stream** – kaynak JPEG.  
2. **Page rectangle** – sayfanın boyutunu tanımlar (bizim `pageBounds`).  
3. **Crop rectangle** – Aspose'a görüntünün hangi kısmını render edeceğini söyler.

Daha fazla sayfa eklemeniz gerekiyorsa, her seferinde yeni bir `imageStream` ile `Add` + `AddImage` desenini tekrarlayın. Bu, **how to add new pdf page** gereksinimini karşılarken kodunuzu düzenli tutar.

---

## Step 5: Save the PDF and Verify the Result

Son adım tek satırlık bir komut, ama küçümsemeyin—doğru yola kaydetmek dosyanın herhangi bir PDF görüntüleyiciyle açılmasını sağlar.

```csharp
// Save the PDF to disk.
pdfDocument.Save(@"C:\Output\cropped_image.pdf");

// Optional: open the file automatically (Windows only).
System.Diagnostics.Process.Start(@"C:\Output\cropped_image.pdf");
```

`cropped_image.pdf` dosyasını açtığınızda, orijinal JPEG'in sadece sol‑üst çeyreğini içeren, 600 × 800 sayfasına tam ortalanmış tek bir sayfa görmelisiniz.

---

## Full Working Example (All Steps Combined)

Aşağıda, bir konsol uygulamasına kopyalayıp yapıştırabileceğiniz tam program yer alıyor. Aspose.Pdf'i kurduğunuz ve belirtilen konumda bir JPEG dosyanız olduğu sürece doğrudan derlenir.

```csharp
using Aspose.Pdf;
using System.IO;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new PDF document.
        using var pdfDocument = new Document();

        // 2️⃣ Open the source JPEG.
        using var imageStream = File.OpenRead(@"C:\Images\photo.jpg");

        // 3️⃣ Define the page size (600 × 800 points).
        var pageBounds = new Rectangle(0, 0, 600, 800);

        // 4️⃣ Calculate the crop area – upper‑left quarter.
        var cropArea = new Rectangle(
            pageBounds.LLX,
            pageBounds.LLY + pageBounds.Height / 2,
            pageBounds.LLX + pageBounds.Width / 2,
            pageBounds.URY);

        // 5️⃣ Add a new page and insert the cropped image.
        var page = pdfDocument.Pages.Add();
        page.AddImage(imageStream, pageBounds, cropArea);

        // 6️⃣ Save the resulting PDF.
        pdfDocument.Save(@"C:\Output\cropped_image.pdf");

        // 7️⃣ (Optional) Open the PDF automatically.
        System.Diagnostics.Process.Start(@"C:\Output\cropped_image.pdf");
    }
}
```

### Expected Output

- **Dosya:** `cropped_image.pdf` (≈ 30 KB).  
- **İçerik:** 600 × 800 puanlık bir sayfa, `photo.jpg`'in sol‑üst çeyreğini gösterir.  
- **Davranış:** Bozulma yok; görüntü kırpılmış sınırlar içinde orijinal çözünürlüğünü korur.

---

## Frequently Asked Questions & Edge Cases

### Tüm resmi, sadece çeyrek kısmını değil, saklamam gerekirse ne yapmalıyım?

`cropArea`'yı `pageBounds` ile aynı yapın:

```csharp
var cropArea = pageBounds; // No cropping – full image.
```

### Farklı bir sayfa boyutu (ör. A4) kullanabilir miyim?

Tabii ki. `pageBounds` değerlerini A4 sayfasının puan cinsinden boyutları (595 × 842) ile değiştirin:

```csharp
var pageBounds = new Rectangle(0, 0, 595, 842);
```

Kırpma dikdörtgeni aynı kalabilir ya da yeni en‑boy oranına göre yeniden hesaplanabilir.

### Her bir sayfada ayrı bir görüntü eklemek istiyorum, nasıl yaparım?

Dosya yolu koleksiyonunu döngüye alın:

```csharp
foreach (var path in imagePaths)
{
    using var stream = File.OpenRead(path);
    var page = pdfDocument.Pages.Add();
    page.AddImage(stream, pageBounds, pageBounds); // No crop for each image.
}
```

### Şeffaflık veya PNG görüntüleriyle ne olur?

Aspose.Pdf PNG'yi JPEG gibi işler. Kaynakta bir alfa kanalı varsa, PDF şeffaflığı destekleyen sürümde (varsayılan yeterli) korunur.

### .NET Core Linux üzerinde çalışır mı?

Evet. Aspose.Pdf çapraz‑platformdur; sadece `imageStream`'in hedef OS'de geçerli bir dosya yoluna işaret ettiğinden emin olun. Windows‑özel API'ler kullanılmaz.

---

## Tips & Best Practices

- **Bellek Yönetimi:** Akışları (streams) `using` blokları içinde tutarak dosya kilitlenmelerini önleyin (örneklerde gösterildiği gibi).  
- **Performans:** Onlarca görüntü işliyorsanız, tek bir `Document` örneğini yeniden kullanıp her görüntü için `pdfDocument.Pages.Add()` çağırın.  
- **Hata Yönetimi:** Tüm prosedürü bir `try/catch` bloğuna alın ve sorun giderme için `PdfException` kaydedin.  
- **Kalite Kontrolü:** Aspose.Pdf, `ImageFragment` aracılığıyla görüntü çözünürlüğü ayarlamanıza izin verir. Yüksek‑dpi taramalar için `ImageFragment.Resolution = 300;` ayarlayın.  
- **Güvenlik:** PDF dışarı paylaşılacaksa, `pdfDocument.Encrypt("ownerPwd", "userPwd", Permission.All);` ile şifreleme ekleyebilirsiniz.

---

## Conclusion

**create PDF from JPG** işlemini C#'ta nasıl yapacağınızı, **crop image in PDF** ve **add new PDF page** ile çok‑sayfalı belgeler oluşturmayı öğrendik. Aynı desen, **convert JPG to PDF with crop** ve **insert image into PDF C#** gibi senaryolar için de geçerli.  

Deneyin: kırpma mantığını değiştirin, A4 sayfalarıyla oynayın ya da birkaç görüntüyü zincirleyin. Aspose.Pdf bu görevleri zahmetsiz kılıyor ve yukarıdaki kod, herhangi bir projeye yapıştırabileceğiniz sağlam, referans niteliğinde bir örnek sunuyor.

---

### What’s Next?

- PDF'e **metin ek açıklamaları** ekleyin (ör. her görüntünün altına başlık).  
- Çok‑sayfalı PDF'ler için **içindekiler tablosu** otomatik oluşturun.  
- `pdfDocument.Pages.AddRange(otherDoc.Pages);` kullanarak **birden fazla PDF'i birleştirin**.  

Bu konular, yeni edindiğiniz temeller üzerine inşa edilecek, böylece keşfetmeye hazır bir konumda olacaksınız.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}