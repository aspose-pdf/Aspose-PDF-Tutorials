---
category: general
date: 2026-06-18
description: Aspose.PDF kullanarak C#'de PDF'ye şekil ekleme – PDF'yi yükle, bir dikdörtgen
  çiz ve kaydet.
draft: false
keywords:
- how to add shape to pdf
- load pdf document in c#
- how to draw shapes in pdf
- aspose pdf add rectangle
language: tr
og_description: C# ile Aspose.PDF kullanarak PDF'ye şekil nasıl eklenir? Bir PDF belgesini
  yüklemeyi, bir dikdörtgen çizmeyi ve güncellenmiş dosyayı kaydetmeyi öğrenin.
og_title: C#'ta Aspose.PDF ile PDF'ye Şekil Ekleme
schemas:
- author: Aspose
  dateModified: '2026-06-18'
  description: How to add shape to PDF using Aspose.PDF in C# – load a PDF, draw a
    rectangle, and save it.
  headline: How to Add Shape to PDF with Aspose.PDF in C# – Step‑by‑Step Guide
  type: TechArticle
- description: How to add shape to PDF using Aspose.PDF in C# – load a PDF, draw a
    rectangle, and save it.
  name: How to Add Shape to PDF with Aspose.PDF in C# – Step‑by‑Step Guide
  steps:
  - name: What if I need to draw on multiple pages?
    text: Simply loop over `pdfDoc.Pages` and call `AddRectangle` (or any other shape)
      for each page. Remember to adjust coordinates if pages have different sizes.
  - name: Can I fill the rectangle with a color?
    text: Absolutely. Change `FillColor` from `Transparent` to any `Color` you like,
      e.g., `Color.Yellow`. The shape will appear as a solid block.
  - name: Does this work with password‑protected PDFs?
    text: 'Aspose.PDF can open encrypted files if you supply the password:'
  - name: How to add a rectangle with rounded corners?
    text: Use the `RoundedRectangle` class instead of `Rectangle`. The rest of the
      steps stay identical.
  type: HowTo
tags:
- Aspose.PDF
- C#
- PDF manipulation
title: C# ile Aspose.PDF Kullanarak PDF'e Şekil Ekleme – Adım Adım Rehber
url: /tr/net/images-graphics/how-to-add-shape-to-pdf-with-aspose-pdf-in-c-step-by-step-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#’ta Aspose.PDF ile PDF’e Şekil Ekleme – Tam Kılavuz

Düşük seviyeli bayt akışlarıyla uğraşmadan **PDF’e şekil nasıl eklenir** diye hiç merak ettiniz mi? Gerçek dünyadaki birçok uygulamada bir bölgeyi vurgulamanız, bir maddeyi altını çizmeniz ya da sadece bir imza alanı için bir sınırlayıcı kutu çizmeniz gerekir. İyi haber, Aspose.PDF bu işi çocuk oyuncağı haline getiriyor. Bu rehberde bir PDF belgesini C#’ta nasıl yükleyeceğimizi, bir dikdörtgen çizeceğimizi ve sonucu nasıl kaydedeceğimizi adım adım göstereceğiz—başka bir şey eklemeden, eksiksiz.

Her kod satırını inceleyecek, *neden* önemli olduğunu açıklayacak ve şeklin gerçekten istediğiniz yerde olup olmadığını hızlıca kontrol etmenin bir yolunu göstereceğiz. Sonunda **PDF dosyalarında şekil nasıl çizilir** konusunda rahatlayacaksınız ve .NET projenize dilediğiniz zaman ekleyebileceğiniz yeniden kullanılabilir bir snippet elde edeceksiniz.

## Önkoşullar

Başlamadan önce şunların yüklü olduğundan emin olun:

- **.NET 6.0** (veya daha yeni bir .NET sürümü)  
- **Geçerli bir Aspose.PDF for .NET lisansı** (veya ücretsiz değerlendirme anahtarı)  
- Visual Studio 2022, Rider veya tercih ettiğiniz herhangi bir editör  
- Referans verebileceğiniz bir klasörde bulunan bir PDF dosyası (`input.pdf`)

> **İpucu:** Sadece test ediyorsanız, ücretsiz değerlendirme sürümü gayet yeterlidir—küçük bir filigran ekler ama diğer tüm özellikleri tam ürün gibi çalışır.

## Adım 1: Projeyi Oluşturun ve Namespace’leri İçeri Aktarın

Öncelikle yeni bir konsol projesi oluşturun (veya mevcut bir projeye ekleyin) ve gerekli namespace’leri kodunuza dahil edin.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;   // Required for shape classes
```

Neden önemli: `Aspose.Pdf` temel belge modelini sağlar, `Aspose.Pdf.Drawing` ise daha sonra kullanacağımız `Rectangle` şekil sınıfını içerir. İkincisi olmadan derleyici `Rectangle` tanımlı değil hatası verir.

## Adım 2: PDF Belgesini C#’ta Yükleyin

Şimdi **c#’ta pdf belgesi nasıl yüklenir** sorusunun cevabını göreceksiniz. Bu, mevcut bir dosyayı değiştirmeye başlamadan önce her zaman yaptığınız ilk işlemdir.

```csharp
// Step 2: Load the PDF document
string inputPath = @"YOUR_DIRECTORY\input.pdf";
Document pdfDoc = new Document(inputPath);
Console.WriteLine($"Loaded PDF with {pdfDoc.Pages.Count} page(s).");
```

*Açıklama*:  
- `Document` Aspose’un tüm dosyayı temsil eden sınıfıdır.  
- Yapıcıya tam yolu vermek dosyayı belleğe okur.  
- `Console.WriteLine` satırı isteğe bağlıdır, ancak sayfa sayısı sıfır ise erken bir sorun olduğunu gösterir.

## Adım 3: Dikdörtgen Şekli Tanımlayın

İşte **pdf’e şekil nasıl eklenir** sorusunun kalbine ulaştık. Koordinat sistemi (0,0)’ın sayfanın sol‑alt köşesi olduğu bir konum ve boyut belirten bir `Rectangle` nesnesi oluşturuyoruz.

```csharp
// Step 3: Define a rectangle (left, bottom, right, top)
Rectangle rect = new Rectangle(0, 0, 200, 100)
{
    // Optional styling – you can tweak these as needed
    FillColor = Color.Transparent,          // No fill, just the border
    Border = new Border(BorderStyle.Solid, 2, Color.Red)
};
```

`FillColor`’ı şeffaf olarak ayarlamamızın nedeni: çoğu senaryoda sadece bir kontur istenir (vurgulama kutusu gibi). `Border` özelliği kalınlık ve rengi kontrol etmenizi sağlar; kırmızı renk dikdörtgenin tipik beyaz bir sayfada öne çıkmasını sağlar.

## Adım 4: Şeklin Sayfa Sınırları İçinde Olduğunu Doğrulayın

**Dikdörtgen eklemeden** önce şeklin sayfa kenarlarını aşmadığından emin olmak iyi bir alışkanlıktır. Aspose bu amaçla `ValidateShapeBounds` metodunu sunar.

```csharp
// Step 4: Validate that the rectangle fits on the first page
bool fits = pdfDoc.Pages[1].ValidateShapeBounds(rect);
if (!fits)
{
    Console.WriteLine("Rectangle exceeds page dimensions – adjusting...");
    // Simple fallback: shrink to fit the page width
    rect.Right = pdfDoc.Pages[1].PageInfo.Width - 10;
    rect.Top  = pdfDoc.Pages[1].PageInfo.Height - 10;
}
```

*Neden*: Sayfanın dışına çizim yapmak render hatalarına ya da istisna fırlatılmasına yol açabilir. Bu kontrol, herhangi bir boyuttaki PDF için öğreticiyi daha dayanıklı kılar.

## Adım 5: Dikdörtgeni İstenen Sayfaya Ekleyin

Şimdi nihayet **pdf’e şekil ekle** işlemini yapıyoruz. `AddRectangle` metodu şekli sayfanın annotation koleksiyonuna ekler, bu da PDF görüntüleyicilerin şekli diğer çizimler gibi render etmesini sağlar.

```csharp
// Step 5: Add the rectangle to the first page
pdfDoc.Pages[1].AddRectangle(rect);
Console.WriteLine("Rectangle added to page 1.");
```

Farklı bir sayfayı hedeflemek isterseniz, indeks `1` yerine uygun sayfa numarasını (Aspose 1‑tabanlı indeksleme kullanır) koymanız yeterlidir.

## Adım 6: Değiştirilmiş PDF’i Kaydedin

Son adım değişiklikleri diske yazmaktır. Orijinal dosyanın üzerine yazabilir ya da yeni bir dosya oluşturabilirsiniz—burada `output.pdf` üretelim.

```csharp
// Step 6: Save the updated PDF
string outputPath = @"YOUR_DIRECTORY\output.pdf";
pdfDoc.Save(outputPath);
Console.WriteLine($"PDF saved as {outputPath}");
```

*Beklenen sonuç*: `output.pdf` dosyasını Adobe Reader ya da herhangi bir görüntüleyicide açtığınızda, ilk sayfanın sol‑alt köşesine sabitlenmiş net kırmızı bir dikdörtgen görmelisiniz.

![PDF’e eklenen dikdörtgeni gösteren diyagram](https://example.com/rectangle-diagram.png "pdf’e şekil ekleme örneği")

*Alt metin*: "pdf’e şekil ekleme – bir PDF dosyasının ilk sayfasına çizilen dikdörtgen"

## Adım 7: Tam Çalışan Örnek (Kopyala‑Yapıştır Hazır)

Aşağıda hemen derleyip çalıştırabileceğiniz tam program yer alıyor. `YOUR_DIRECTORY` kısmını makinenizdeki gerçek klasör yolu ile değiştirin.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using Aspose.Pdf.Color;   // For color definitions

namespace PdfShapeDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Load the PDF document in C#
            string inputPath = @"YOUR_DIRECTORY\input.pdf";
            Document pdfDoc = new Document(inputPath);
            Console.WriteLine($"Loaded PDF with {pdfDoc.Pages.Count} page(s).");

            // Define the rectangle shape
            Rectangle rect = new Rectangle(0, 0, 200, 100)
            {
                FillColor = Color.Transparent,
                Border = new Border(BorderStyle.Solid, 2, Color.Red)
            };

            // Validate bounds on the first page
            if (!pdfDoc.Pages[1].ValidateShapeBounds(rect))
            {
                Console.WriteLine("Rectangle exceeds page dimensions – adjusting...");
                rect.Right = pdfDoc.Pages[1].PageInfo.Width - 10;
                rect.Top  = pdfDoc.Pages[1].PageInfo.Height - 10;
            }

            // Add the rectangle (how to add shape to pdf)
            pdfDoc.Pages[1].AddRectangle(rect);
            Console.WriteLine("Rectangle added to page 1.");

            // Save the modified PDF
            string outputPath = @"YOUR_DIRECTORY\output.pdf";
            pdfDoc.Save(outputPath);
            Console.WriteLine($"PDF saved as {outputPath}");
        }
    }
}
```

Programı çalıştırın, `output.pdf` dosyasını açın ve kırmızı dikdörtgenin tam olarak yerleştirdiğimiz yerde olduğunu görün. Farklı bir şekle ihtiyacınız varsa—elips, çizgi ya da çokgen—`Rectangle` yerine `Ellipse`, `Line` ya da `Polygon` kullanıp aynı akışı izleyebilirsiniz. İşte bu, Aspose kullanarak **pdf’de şekil nasıl çizilir** sorusunun temel cevabı.

## Yaygın Sorular & Kenar Durumları

### Birden fazla sayfada çizim yapmak istersem ne yapmalıyım?
`pdfDoc.Pages` üzerinde döngü kurup her sayfa için `AddRectangle` (veya başka bir şekil) çağırın. Sayfalar farklı boyutlardaysa koordinatları ona göre ayarlamayı unutmayın.

```csharp
foreach (Page page in pdfDoc.Pages)
{
    page.AddRectangle(rect);
}
```

### Dikdörtgeni bir renk ile doldurabilir miyim?
Kesinlikle. `FillColor` değerini `Transparent` yerine istediğiniz bir `Color` (ör. `Color.Yellow`) yapın. Şekil katı bir blok olarak görünecektir.

### Şifre korumalı PDF’lerde çalışır mı?
Aspose.PDF, şifreyi sağladığınız takdirde şifreli dosyaları açabilir:

```csharp
Document pdfDoc = new Document(inputPath, new LoadOptions { Password = "mySecret" });
```

### Köşeleri yuvarlatılmış bir dikdörtgen eklemek istersem?
`Rectangle` yerine `RoundedRectangle` sınıfını kullanın. Diğer adımlar aynı kalır.

## Özet

**Aspose.PDF ile C#’ta pdf’e şekil ekleme** konusunu ele aldık. İş akışı şu şekildeydi:

1. **c#’ta pdf belgesi nasıl yüklenir** – bir `Document` nesnesi oluşturun.  
2. **Bir dikdörtgen (veya başka bir şekil) tanımlayın**.  
3. **Sınırları doğrulayın** ve taşmayı önleyin.  
4. **Dikdörtgeni** hedef sayfaya ekleyin.  
5. **Kaydedin** değiştirilen dosyayı.

Bu, **aspose pdf add rectangle** işleminin tüm adımlarıdır ve artık daire, çizgi ya da özel çokgenler için bir şablonunuz var.

## Sıradaki Adımlarınız Ne Olmalı?

- **Diğer çizim primitive’lerini keşfedin**: `Ellipse`, `Line`, `Polygon`.  
- **Şekillerin yanına metin açıklamaları ekleyin** ve etkileşimi artırın.  
- **PDF form alanlarıyla birleştirin** eğer doldurulabilir bir sözleşme oluşturuyorsanız.  
- **Aspose’un PDF dönüşüm özelliklerine göz atın** ve anotasyonlu PDF’lerinizi ön izleme küçük resimlerine dönüştürün.

Denemeler yapın—belki bir filigran çizin, bir tablo hücresini vurgulayın ya da bir imza alanını çizin. API esnek ve artık temelleri biliyorsunuz.

İyi kodlamalar, PDF’leriniz her zaman istediğiniz gibi görünsün!

## Bir Sonraki Öğrenmeniz Gerekenler

Aşağıdaki öğreticiler, bu kılavuzda gösterilen tekniklere dayanarak ilgili konuları derinleştirir. Her kaynak, adım adım açıklamalar ve tam çalışan kod örnekleri içerir, böylece API özelliklerini daha iyi kavrayabilir ve projelerinizde alternatif uygulama yaklaşımları keşfedebilirsiniz.

- [Create PDF Document with Aspose.PDF – Add Page, Shape & Save](/pdf/english/net/document-creation/create-pdf-document-with-aspose-pdf-add-page-shape-save/)
- [How to Add and Customize Page Numbers in PDFs Using Aspose.PDF for .NET | Document Manipulation Guide](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [How to Add Hyperlinks in PDFs Using Aspose.PDF for .NET&#58; A Comprehensive Guide](/pdf/english/net/bookmarks-navigation/add-hyperlinks-pdf-aspose-net-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}