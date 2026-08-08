---
category: general
date: 2026-06-08
description: Aspose.PDF kullanarak C#'ta PDF'de resmi kırpın. Görüntülü PDF oluşturmayı,
  görüntülü PDF kaydetmeyi ve sadece birkaç satırla PDF'ye resim eklemeyi öğrenin.
draft: false
keywords:
- crop image in pdf
- create pdf with image
- save pdf with image
- how to add image to pdf
- how to crop image pdf
language: tr
og_description: Aspose.PDF ve C# kullanarak PDF'de resmi kırpın. Bu öğretici, görüntülü
  PDF oluşturmayı, görüntülü PDF'yi kaydetmeyi ve görüntüyü PDF'ye hızlıca eklemeyi
  gösterir.
og_title: Aspose.PDF ile PDF'de Görüntüyü Kırpma – Tam Rehber
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Crop image in PDF using Aspose.PDF in C#. Learn how to create PDF with
    image, save PDF with image, and add image to PDF in just a few lines.
  headline: Crop Image in PDF with Aspose.PDF – Complete Guide
  type: TechArticle
- description: Crop image in PDF using Aspose.PDF in C#. Learn how to create PDF with
    image, save PDF with image, and add image to PDF in just a few lines.
  name: Crop Image in PDF with Aspose.PDF – Complete Guide
  steps:
  - name: '**Image stream** – the raw bytes of your picture.'
    text: '**Image stream** – the raw bytes of your picture.'
  - name: '**Placement rectangle** – where on the page the image lives.'
    text: '**Placement rectangle** – where on the page the image lives.'
  - name: '**Crop rectangle** – the portion of the image you actually want to render.'
    text: '**Crop rectangle** – the portion of the image you actually want to render.'
  type: HowTo
tags:
- Aspose.PDF
- C#
- PDF manipulation
- Image processing
title: Aspose.PDF ile PDF'de Görüntüyü Kırpma – Tam Kılavuz
url: /tr/net/programming-with-images/crop-image-in-pdf-with-aspose-pdf-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.PDF ile PDF'de Görüntüyü Kırpma – Tam Kılavuz

Grafik editörü açmadan **PDF'de görüntüyü kırpmayı** hiç merak ettiniz mi? Tek başınıza değilsiniz. Birçok rapor, fatura veya e‑kitapta sadece bir resim dilimi gerekir—belki logo köşesi ya da bir grafik parçası—ve bunu doğrudan PDF içinde istiyorsunuz.  

Bu kılavuz tam da bunu gösteriyor: **görsel ile PDF oluşturma**, **PDF'ye görsel ekleme** ve ardından **PDF'de görüntüyü kırpma** işlemlerini Aspose.PDF C# kütüphanesiyle yapacağız. Sonunda **görsel ile PDF kaydetme** yöntemini de öğrenecek ve dosyayı istediğiniz kişiye gönderebileceksiniz.

---

## Gereksinimler

- .NET 6.0 veya üzeri (kod .NET Framework 4.6+ ile de çalışır)  
- Lisanslı veya deneme sürümü **Aspose.PDF for .NET** (NuGet `Install-Package Aspose.PDF` ile kurun)  
- Diskte bir görüntü dosyası (JPEG/PNG) – buna `image.jpg` diyeceğiz  
- İstediğiniz IDE (Visual Studio, Rider, VS Code)

Hepsi bu. Ek hizmet ya da dış araç gerekmez.

---

## Adım 1: Projeyi ve İçe Aktarmaları Ayarlama

İlk olarak bir console uygulaması oluşturun ve kullanacağımız ad alanlarını ekleyin. `using` ifadeleri kodu düzenli tutar ve sonraki adımları okumayı kolaylaştırır.

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;   // for text fragments if you want captions later
```

> **Pro tip:** Visual Studio kullanıyorsanız, proje üzerine sağ‑tıklayın → *Manage NuGet Packages* → “Aspose.PDF” aratın ve kurun. Kütüphane hem görüntü yerleştirmeyi hem de kırpmayı dahili olarak yönetir, bu yüzden üçüncü‑taraf görüntü kütüphanelerine ihtiyacınız olmaz.

---

## Adım 2: Görüntülü PDF Oluşturma

Şimdi gerçekten **görsel ile pdf oluşturma** yapıyoruz. Aşağıdaki kod parçası yeni bir `Document` oluşturur, boş bir sayfa ekler ve bir görüntü akışı hazırlar.

```csharp
// Initialize a new PDF document
Document pdf = new Document();

// Add a blank page – think of it as a clean canvas
Page page = pdf.Pages.Add();

// Open the source image file
using (FileStream imgStream = new FileStream("YOUR_DIRECTORY/image.jpg", FileMode.Open))
{
    // We'll place the whole image first; cropping comes next
    // Define where the image should sit on the page (in points; 1 point = 1/72 inch)
    Rectangle placement = new Rectangle(0, 0, 600, 800); // width=600pt, height=800pt

    // Add the image without cropping yet – just to see the full picture
    page.AddImage(imgStream, placement);
}
```

Bu kodu çalıştırdığınızda, belirttiğiniz boyutlara göre tüm resim uzatılmış bir PDF elde edersiniz. Kesmeye başlamadan önce iyi bir kontrol noktasıdır.

---

## Adım 3: PDF'ye Görüntü Ekleme (ve Kırpmaya Hazırlık)

İstediğiniz bölgeyi zaten biliyorsanız, tam‑boyut adımını atlayıp doğrudan **pdf'ye görsel ekleme** kısmına geçebilirsiniz. `AddImage` metodu üç parametre alır:

1. **Image stream** – resminizin ham baytları.  
2. **Placement rectangle** – sayfada görüntünün konumlandığı alan.  
3. **Crop rectangle** – gerçekte render edilmesini istediğiniz görüntü bölgesi.

Aşağıda, yerleştirme **ve** kırpmayı tek bir çağrıda yapan kompakt bir örnek bulunuyor.

```csharp
using (FileStream imgStream = new FileStream("YOUR_DIRECTORY/image.jpg", FileMode.Open))
{
    // Full‑size placement rectangle (you can adjust X/Y if you need margins)
    Rectangle placement = new Rectangle(0, 0, 600, 800);

    // Crop area: upper‑left quarter of the original image
    Rectangle crop = new Rectangle(0, 0, placement.Width / 2, placement.Height / 2);

    // This single line both adds the image and crops it
    page.AddImage(imgStream, placement, crop);
}
```

> **Neden işe yarıyor:** Aspose.PDF, kırpma dikdörtgenini görüntünün piksel boyutlarına eşler ve sadece bu dilimi `placement` alanı içinde render eder. Ek bitmap işleme gerekmez, bu da PDF boyutunun küçük kalmasını sağlar.

---

## Adım 4: PDF'de Görüntüyü Kırpma – Gelişmiş Seçenekler

Bazen çeyrek‑kırpma yeterli olmaz. Özel bir dikdörtgen gerekebilir ya da görüntünün en‑boy oranını korumak isteyebilirsiniz. İşte daha esnek bir yaklaşım:

```csharp
using (FileStream imgStream = new FileStream("YOUR_DIRECTORY/image.jpg", FileMode.Open))
{
    // Placement on the page (centered, 300pt wide, keep original height)
    Rectangle placement = new Rectangle(150, 400, 450, 1200);

    // Suppose you want a 200 × 150 pixel region starting at (50, 30) in the source image
    // First, convert pixel coordinates to points (assuming 72 DPI)
    float dpi = 72f;
    float left   = 50  / dpi * 72; // = 50 points
    float bottom = 30  / dpi * 72; // = 30 points
    float width  = 200 / dpi * 72; // = 200 points
    float height = 150 / dpi * 72; // = 150 points

    Rectangle crop = new Rectangle(left, bottom, left + width, bottom + height);

    page.AddImage(imgStream, placement, crop);
}
```

**Köşe durumları yönetimi:**  
- **Null akışlar** – sızıntıyı önlemek için `FileStream`i `using` bloğu içinde sarın, örnekte gösterildiği gibi.  
- **Büyük görüntüler** – kaynak görüntü çok büyükse, `placement` dikdörtgenini küçültmeyi düşünün; Aspose otomatik olarak downsample yapar.  
- **Şeffaf PNG'ler** – kütüphane alfa kanallarını korur, bu yüzden kırpılan alan şeffaflığını korur.

---

## Adım 5: Görüntülü PDF'yi Kaydetme (ve Doğrulama)

Son olarak **görsel ile pdf kaydetme** işlemini yapıyoruz. `Save` metodu belgeyi diske yazar. Bir API geliştiriyorsanız, belgeyi web istemcisine akış olarak da gönderebilirsiniz.

```csharp
// Save the final PDF to the output folder
pdf.Save("YOUR_DIRECTORY/output.pdf");

// Optional: Open the file automatically (only works on Windows)
System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo
{
    FileName = "YOUR_DIRECTORY/output.pdf",
    UseShellExecute = true
});
```

`output.pdf` dosyasını açtığınızda, `image.jpg` dosyasının yalnızca kırpılmış kısmının tanımladığınız konumda göründüğünü görmelisiniz. Görüntü uzamış görünüyorsa, kırpma dikdörtgeninin en‑boy oranına uyması için `placement` dikdörtgeninin genişlik/yüksekliğini ayarlayın.

---

## Yaygın Sorular ve Tuzaklar

| Soru | Cevap |
|----------|--------|
| **Aynı sayfada birden fazla görüntüyü kırpabilir miyim?** | Kesinlikle. Her görüntü için kendi placement ve crop dikdörtgenleriyle `page.AddImage` çağırın. |
| **Görüntüm farklı bir formatta (ör. BMP) ise ne olur?** | Aspose.PDF JPEG, PNG, BMP, GIF ve TIFF formatlarını kutudan çıkar çıkmaz destekler. Sadece dosya uzantısını değiştirin. |
| **Üretim ortamında lisansa ihtiyacım var mı?** | Deneme sürümü en fazla 5 sayfa için çalışır. Gerçek dağıtımlar için filigranı kaldırmak üzere lisans satın alın. |
| **Kırpılmış görüntüyü nasıl döndürürüm?** | Görüntüyü ekledikten sonra `Image` nesnesini alın ve `Rotate` özelliğini ayarlayın (`Rotate = RotationAngle.Rotate90`). |
| **Yüzdelik değerlerle kırpma yapabilir miyim, mutlak puanlar yerine?** | Evet—dikdörtgen boyutlarını `image.Width * 0.25` gibi hesaplayıp, ardından Step 4'te gösterildiği gibi puana dönüştürün. |

---

## Tam Çalışan Örnek (Kopyala‑Yapıştır Hazır)

```csharp
using System;
using System.IO;
using Aspose.Pdf;

namespace CropImageInPdfDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create a new PDF document and add a blank page
            Document pdf = new Document();
            Page page = pdf.Pages.Add();

            // 2️⃣ Open the image that will be placed on the page
            using (FileStream imgStream = new FileStream("YOUR_DIRECTORY/image.jpg", FileMode.Open))
            {
                // 3️⃣ Define where the image will sit on the page (points)
                Rectangle placement = new Rectangle(0, 0, 600, 800);

                // 4️⃣ Define the crop area – upper‑left quarter of the image
                Rectangle crop = new Rectangle(0, 0, placement.Width / 2, placement.Height / 2);

                // 5️⃣ Add the image using both placement and crop rectangles
                page.AddImage(imgStream, placement, crop);
            }

            // (Optional) Save the PDF to verify the result
            pdf.Save("YOUR_DIRECTORY/output.pdf");

            Console.WriteLine("PDF created and image cropped successfully!");
        }
    }
}
```

Programı çalıştırın, `output.pdf` dosyasını açın ve sayfanın sol‑üst köşesinde yalnızca `image.jpg` dosyasının sol‑üst çeyreğinin render edildiğini görün. Farklı dilimler denemek için `crop` dikdörtgeni değerlerini değiştirin.

---

## Sonuç

Aspose.PDF for C# kullanarak **pdf'de görüntüyü kırpma** sürecini baştan sona ele aldık. Yeni bir belge oluşturup **görsel ile pdf oluşturma**, **pdf'ye görsel ekleme**, özel bir **pdf'de görüntüyü kırpma** dikdörtgeni uygulama ve sonunda **görsel ile pdf kaydetme** adımlarını gösterdik.  

Artık ürettiğiniz herhangi bir PDF'ye tam olarak kırpılmış resimler ekleyebilir, faturalar, pazarlama broşürleri veya otomatik raporlar için mükemmel bir çözüm elde edebilirsiniz. Bir sonraki adımda, kırpılmış görüntünün etrafına metin başlıkları (`TextFragment`) eklemeyi veya şekiller çizmeyi düşünerek vurgusunu artırabilirsiniz.  

Daha fazla senaryoyu merak ediyor musunuz? Yorum bırakın, iyi kodlamalar!

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanarak yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak tam çalışan kod örnekleri ve adım‑adım açıklamalar içerir.

- [Aspose.PDF for .NET Kullanarak PDF'de Görüntü Boyutunu Ayarlama](/pdf/english/net/images-graphics/set-image-size-pdf-aspose-dotnet/)
- [Aspose.PDF for .NET Kullanarak PDF'ye Görüntü Damgası Ekleme: Kapsamlı Kılavuz](/pdf/english/net/images-graphics/add-image-stamp-pdf-aspose-dotnet/)
- [Aspose.PDF for .NET Kullanarak PDF'lerden Görüntü Bilgilerini Çıkarma](/pdf/english/net/images-graphics/extract-image-info-pdf-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}