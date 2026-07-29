---
category: general
date: 2026-07-14
description: Aspose.Pdf kullanarak PDF'yi HTML olarak kaydedin – PDF belgesi oluşturmayı,
  dikdörtgen şekli eklemeyi ve görüntüsüz temiz HTML'ye dışa aktarmayı öğrenin.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save pdf as html
- how to create pdf document
- add rectangle shape pdf
language: tr
lastmod: 2026-07-14
og_description: Aspose.Pdf ile PDF'yi HTML olarak kaydedin. PDF belgesi oluşturmayı,
  PDF üzerine dikdörtgen şekli çizmeyi ve dakikalar içinde görüntüsüz HTML üretmeyi
  keşfedin.
og_image_alt: Screenshot of a PDF saved as HTML showing a rectangle shape
og_title: PDF'yi HTML olarak kaydet – PDF oluşturma ve Dikdörtgen Şekil Ekleme Hızlı
  Rehberi
schemas:
- author: Aspose
  dateModified: '2026-07-14'
  description: Save PDF as HTML using Aspose.Pdf – learn how to create PDF document,
    add rectangle shape PDF, and export to clean HTML without images.
  headline: Save PDF as HTML – Create PDF, add rectangle shape
  type: TechArticle
tags:
- pdf
- aspnet
- csharp
- html-export
title: PDF'yi HTML olarak kaydet – PDF oluştur, dikdörtgen şekli ekle
url: /tr/net/conversion-export/save-pdf-as-html-create-pdf-add-rectangle-shape/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PDF'yi HTML olarak kaydet – PDF oluştur, dikdörtgen şekli ekle

PDF'yi **HTML olarak kaydet**mek ve aynı zamanda kaynak PDF üzerinde grafik çizebilmek ister misiniz? Tek başınıza değilsiniz. Birçok iç araçta, özel şekiller içeren bir PDF'nin temiz bir HTML önizlemesine ihtiyacımız var ve geleneksel dönüştürücüler ya ağır raster görüntüler ekliyor ya da vektör verisini tamamen kaldırıyor.  

Bu öğreticide **Aspose.Pdf** ile programlı olarak **PDF belgesi oluşturmayı**, **dikdörtgen şekli PDF eklemeyi**, Bates numaralandırmayı yapılandırmayı ve sonunda **HTML olarak PDF kaydetmeyi** raster görüntüler olmadan nasıl yapacağınızı adım adım göstereceğiz. Sonunda, herhangi bir tarayıcıda açabileceğiniz, ekstra görüntü dosyalarına ihtiyaç duymayan bir HTML dosyası üreten tam çalışır bir C# konsol uygulamanız olacak.

> **Pro ipucu:** Aspose.Pdf, .NET 6+, .NET Framework 4.6+ ve hatta .NET Core ile çalışır, bu yüzden bu kodu eski bir Windows servisine ya da yepyeni bir mikroservise sorunsuzca ekleyebilirsiniz.

---

## Önkoşullar

- **Visual Studio 2022** (Community veya daha üstü) ya da herhangi bir C# uyumlu IDE.  
- **Aspose.Pdf for .NET** NuGet paketi (sürüm 23.11 veya daha yeni). Paketi Package Manager Console üzerinden kurun:

```powershell
Install-Package Aspose.Pdf
```

- C# sözdizimine temel aşinalık; önceden PDF deneyimi gerekmiyor.

---

## Aspose.Pdf ile PDF'yi HTML olarak kaydet

Aşağıda tamamen kopyala‑yapıştır‑hazır kod yer alıyor. Orijinal snippet'teki adımları aynı şekilde izliyor, ancak yorumlar, hata yönetimi ve ana akışı okunabilir tutmak için küçük bir yardımcı metod ekliyor.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using Aspose.Pdf.Text;

namespace PdfToHtmlDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create a fresh PDF document.
            Document pdfDoc = new Document();
            Page pdfPage = pdfDoc.Pages.Add();

            // 2️⃣ Draw a rectangle shape on the page.
            //    This demonstrates the "add rectangle shape pdf" requirement.
            var rectangle = new Rectangle(100, 500, 300, 700)
            {
                // Optional visual tweaks
                FillColor = Color.GetYellow(),
                Border = new Border
                {
                    Width = 2,
                    Color = Color.GetRed()
                }
            };
            pdfPage.Paragraphs.Add(rectangle);
            pdfPage.ValidateGraphicsState(); // Ensures the shape fits within page bounds

            // 3️⃣ Configure Bates numbering – useful for legal documents.
            var bates = new BatesNumbering { StartNumber = 1, Prefix = "DOC-" };
            pdfDoc.BatesNumbering = bates;

            // 4️⃣ Add a tagged element with an explicit position.
            //    Tagging is important for accessibility (PDF/UA).
            var taggedElement = new TagStructure();
            taggedElement.PositionSettings = new TagPositionSettings { X = 150, Y = 600 };
            pdfPage.TagStructure.Add(taggedElement);

            // 5️⃣ Enable detection of compromised signatures.
            pdfDoc.SecurityOptions.DetectCompromisedSignatures = true;
            bool hasCompromisedSignature = pdfDoc.SecurityOptions.HasCompromisedSignature;
            Console.WriteLine($"Compromised signature? {hasCompromisedSignature}");

            // 6️⃣ Finally, save the PDF as HTML *without* embedding raster images.
            var htmlOptions = new HtmlSaveOptions
            {
                SkipImages = true,               // Removes <img> tags for raster data
                FixedLayout = true,              // Preserves the original page layout
                ExportEmbeddedFonts = false      // Keeps the HTML lightweight
            };

            string outputPath = @"output.html";
            pdfDoc.Save(outputPath, htmlOptions);
            Console.WriteLine($"✅ PDF successfully saved as HTML at: {outputPath}");
        }
    }
}
```

### Kodun yaptığı şey, adım adım

| Adım | Neden önemlidir |
|------|-----------------|
| **PDF belgesi oluştur** | Bu temel; bir `Document` nesnesi olmadan hiçbir şey ekleyemezsiniz. |
| **Dikdörtgen şekli PDF ekle** | Vektör çizimini gösterir; dikdörtgen en basit şekil ama aynı API daire, çokgen vb. destekler. |
| **Bates numaralandırmayı yapılandır** | Dava süreçlerinde ya da toplu iş senaryolarında sayfaları benzersiz tanımlamak için sıkça gerekir. |
| **Etiket yapısı** | Erişilebilirliği artırır; ekran okuyucular okuma sırasını iletmek için etiketlere güvenir. |
| **Bozulmuş imzaları tespit et** | Güvenlik‑bilinçli uygulamalar dijital imzanın manipüle edilip edilmediğini bilmelidir. |
| **PDF'yi HTML olarak kaydet** | Son hedef — PDF düzenini yansıtan, büyük görüntü dosyaları içermeyen temiz HTML üretmek. |

> **Neden `SkipImages = true`?**  
> Vektör grafikler (örneğin bizim dikdörtgenimiz) içeren bir PDF'yi dönüştürdüğünüzde genellikle raster yedekleme gerekmez. `SkipImages` ayarı, aksi takdirde base‑64 blob'lara referans veren `<img>` öğelerini kaldırır ve HTML dosyasını birkaç kilobayt altında tutar.

---

## Aspose.Pdf ile PDF belgesi nasıl oluşturulur

Aspose'a yeniyseniz, kütüphane bir PDF'yi Word belgesi gibi ele alır: **sayfalar** ekler, ardından bu sayfalara **paragraflar**, **şekiller** ya da **notlar** eklersiniz. `Document` sınıfı giriş noktasıdır ve her `Page` bir `Paragraphs` koleksiyonu barındırır. `TextFragmentAbsorber`, `Image`, `Rectangle` vb. sınıflardan türeyen her şey bu koleksiyona eklenebilir.

Aşağıda sadece boş bir PDF oluşturan minimal bir snippet yer alıyor — sıfırdan başlamak istediğinizde işe yarar:

```csharp
Document emptyPdf = new Document();
Page firstPage = emptyPdf.Pages.Add();   // Adds a default‑size A4 page
emptyPdf.Save("empty.pdf");
```

Ek sayfaları basit bir `for` döngüsüyle zincirleyebilir ya da sayfa‑düzeyi ayarları (kenar boşluğu, boyut) `PageInfo` aracılığıyla uygulayabilirsiniz. Esneklik, Aspose.Pdf'nin sunucu‑tarafı PDF üretiminde neden favori olduğunun başlıca nedenidir.

---

## Dikdörtgen şekli PDF ekle – grafik çizimi

`Rectangle` sınıfı `Aspose.Pdf.Annotations` içinde bulunur. Dört koordinat alır: **sol‑alt X**, **sol‑alt Y**, **sağ‑üst X**, **sağ‑üst Y**. PDF koordinat sistemini şu şekilde düşünün:

## Sonraki Öğrenmeniz Gerekenler


Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanarak yakından ilgili konuları kapsar. Her kaynak, adım adım açıklamalarla tam çalışan kod örnekleri içerir; böylece ek API özelliklerini ustalaşabilir ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfedebilirsiniz.

- [Create PDF Document with Aspose.PDF – Add Page, Shape & Save](/pdf/english/net/document-creation/create-pdf-document-with-aspose-pdf-add-page-shape-save/)
- [Convert PDF to HTML in .NET Using Aspose.PDF Without Saving Images](/pdf/english/net/conversion-export/convert-pdf-html-net-asposepdf-no-images/)
- [PDF to HTML Conversion Using Aspose.PDF .NET&#58; Save Images as External PNGs](/pdf/english/net/conversion-export/pdf-to-html-conversion-external-png-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}