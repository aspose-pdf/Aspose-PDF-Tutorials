---
category: general
date: 2026-07-20
description: 'Aspose.Pdf ile C#''ta PDF belgesi oluşturun: PDF''de metni konumlandırın
  ve erişilebilirlik için yapısal ağaç ekleyin. Bu adım adım kılavuzu izleyin.'
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create pdf document c#
- position text in pdf
- add structural tree
- Aspose.Pdf tagging
- PDF/A‑2b generation
language: tr
lastmod: 2026-07-20
og_description: C# ile PDF belgesini anında oluşturun. PDF'de metni nasıl konumlandıracağınızı
  ve PDF/A‑2b uyumluluğu için Aspose.Pdf kullanarak yapısal ağaç nasıl ekleyeceğinizi
  öğrenin.
og_image_alt: Screenshot showing positioned text inside a PDF generated with Aspose.Pdf
  in C#
og_title: C# ile PDF Belgesi Oluşturma – Metni Konumlandırma ve Etiket Yapısı İçin
  Tam Kılavuz
schemas:
- author: Aspose
  dateModified: '2026-07-20'
  description: 'Create PDF document C# with Aspose.Pdf: position text in PDF and add
    structural tree for accessibility. Follow this step‑by‑step guide.'
  headline: Create PDF Document C# – Position Text and Add Structural Tree
  type: TechArticle
- description: 'Create PDF document C# with Aspose.Pdf: position text in PDF and add
    structural tree for accessibility. Follow this step‑by‑step guide.'
  name: Create PDF Document C# – Position Text and Add Structural Tree
  steps:
  - name: Can I use other units (mm, cm) for positioning?
    text: Aspose.Pdf works natively with points. If you prefer millimeters, convert
      using `1 mm ≈ 2.83465 pt`. For example, `Position(25.4, 254)` places the paragraph
      1 cm from the left and 9 cm from the bottom.
  - name: What if I need to add multiple tags (headings, tables)?
    text: Simply create additional `StructureElement` objects with tags like `"H1"`
      for headings or `"Table"` for tables, and add the corresponding content as kids.
      Nesting works the same way—children inherit the parent’s logical order.
  - name: Does this approach work for PDF/A‑1b or PDF/A‑3b?
    text: Yes. Replace `SaveFormat.PdfA2b` with `SaveFormat.PdfA1b` or `SaveFormat.PdfA3b`.
      Keep in mind that each PDF/A version has its own set of required metadata; Aspose.Pdf
      will prompt you if something is missing.
  type: HowTo
tags:
- C#
- PDF
- Aspose.Pdf
title: PDF Belgesi Oluşturma C# – Metni Konumlandır ve Yapısal Ağaç Ekle
url: /tr/net/programming-with-tagged-pdf/create-pdf-document-c-position-text-and-add-structural-tree/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PDF Belgesi Oluşturma C# – Metni Konumlandırma ve Yapısal Ağaç Ekleme

Hiç **create PDF document C#** oluşturmanız gerektiğinde, metni tam istediğiniz yere yerleştirmenin yanı sıra erişilebilirlik için uygun bir yapısal ağaç da eklemek istediniz mi? Tek başınıza değilsiniz—faturalar, raporlar veya e‑kitaplar hazırlayan geliştiriciler bu ihtiyacı sık sık karşılaşıyor. Bu öğreticide, güçlü Aspose.Pdf kütüphanesini kullanarak tam olarak bunu yapan, çalıştırmaya hazır bir örneği adım adım inceleyeceğiz.

**PDF içinde metni konumlandırma**, **yapısal ağaç ekleme** adımını ve sonunda dosyayı PDF/A‑2b uyumlu bir belge olarak kaydetmeyi ele alacağız. Sonunda, herhangi bir .NET projesine ekleyebileceğiniz yeniden kullanılabilir bir kod parçacığına sahip olacaksınız.

---

## Gereksinimler

- **.NET 6.0** veya üzeri (kod .NET Framework 4.6+ ile de çalışır)  
- **Aspose.Pdf for .NET** NuGet paketi (`Install-Package Aspose.Pdf`)  
- Temel bir C# geliştirme ortamı (Visual Studio, Rider veya VS Code)  

Ek bir üçüncü‑taraf aracı gerekmez; kütüphane sayfa düzeninden PDF/A uyumluluğuna kadar her şeyi halleder.

---

## Adım 1: PDF Belgesini Başlatma (Create PDF Document C#)

İlk yaptığımız şey yeni bir `Document` nesnesi oluşturmak. Bunu temiz bir tuval gibi düşünün—henüz üzerinde hiçbir şey yok, ama sayfalar, metin ve yapısal meta verileri eklemeye hazır.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Struct;

// Create a new PDF document – this is the core of our create pdf document c# workflow
Document pdfDoc = new Document();

// Add a blank page to the document; the page will host our positioned text
Page pdfPage = pdfDoc.Pages.Add();
```

> **Neden önemli:** `Document` sınıfı, tüm Aspose.Pdf işlemlerinin giriş noktasıdır. Erken bir sayfa eklemek, hem görsel içeriği hem de daha sonra ekleyeceğimiz yapısal ağacı bağlamak için bir yüzey sağlar.

---

## Adım 2: Bir Paragraf Tanımlama ve Konumlandırma (Position Text in PDF)

Şimdi bir `Paragraph` nesnesi oluşturup Aspose'a sayfa üzerinde tam olarak nerede görünmesi gerektiğini söylüyoruz. PDF koordinatları nokta biriminde ölçülür (1 inç = 72 pt), bu yüzden `Position(72, 720)` ifadesi paragrafı sol kenardan 1 inç, alt kenardan 10 inç yukarıya yerleştirir.

```csharp
// Define a paragraph positioned 1 inch from the left and 10 inches from the bottom
Paragraph positionedParagraph = new Paragraph
{
    // Position(x, y) – X is horizontal, Y is vertical from the bottom-left corner
    Position = new Position(72, 720) // 72 pt = 1 inch, 720 pt = 10 inch
};

// Add the actual text we want to display
positionedParagraph.Segments.Add(
    new TextFragment("Tagged paragraph at a specific location.")
);
```

> **İpucu:** Birden fazla satırı konumlandırmanız gerekiyorsa, sonraki her paragraf için `Y` koordinatını ayarlayın ya da daha ince kontrol için bir `TextBuilder` kullanın.

---

## Adım 3: Yapısal Bir Eleman Oluşturma (Add Structural Tree)

Erişilebilirlik‑odaklı PDF’ler, içeriğin mantıksal sırasını tanımlayan bir *yapı ağacına* dayanır. Burada `"P"` (paragraph) etiketiyle bir `StructureElement` oluşturup konumlandırılmış paragrafımızı çocuğu olarak ekliyoruz.

```csharp
// Create a structural element (tag) for the paragraph – this is the add structural tree step
StructureElement structElement = new StructureElement("P");

// Attach the paragraph as a child of the structural element
structElement.AddKid(positionedParagraph);
```

> **Neden yapısal ağaç ekliyoruz:** Ekran okuyucular ve diğer yardımcı teknolojiler bu etiketleri belge içinde gezinmek için kullanır. Etiketler olmadan PDF’niz görsel olarak mükemmel olabilir ama erişilebilir olmayabilir.

---

## Adım 4: Yapısal Elemanı Sayfaya Bağlama

Her sayfa, kendi yapısal eleman koleksiyonunu tutar. `structElement`i `pdfPage.StructElements` koleksiyonuna ekleyerek mantıksal hiyerarşiyi görsel yerleşimle bütünleştiriyoruz.

```csharp
// Attach the structural element to the page's structure tree
pdfPage.StructElements.Add(structElement);
```

> **Yaygın tuzak:** Bu adımı atlamak, etiketin bellekte var olduğu ama hiçbir sayfaya bağlanmadığı anlamına gelir; bu da erişilebilirlik bilgisinin okuyucular tarafından görülmemesine yol açar.

---

## Adım 5: PDF/A‑2b Olarak Kaydetme (Uzun Süreli Saklama)

PDF/A‑2b, arşivleme için tasarlanmış bir PDF alt kümesidir. Aspose.Pdf, bu formatı tek bir çağrıyla üretebilir. `"YOUR_DIRECTORY"` ifadesini makinenizdeki gerçek bir yol ile değiştirin.

```csharp
// Save the document as a PDF/A‑2b file – ideal for long‑term storage and compliance
pdfDoc.Save("YOUR_DIRECTORY/TaggedWithPosition.pdf", SaveFormat.PdfA2b);
```

> **Sonuç:** Metnin tam olarak konumlandırıldığı ve belgenin erişilebilirlik araçları için uygun bir yapısal ağaç içerdiği bir PDF elde ettiniz.

---

## Tam Çalışan Örnek

Aşağıda, bir konsol uygulamasına kopyalayıp yapıştırabileceğiniz tam program yer alıyor. Aspose.Pdf NuGet referansını ekledikten sonra olduğu gibi derlenir ve çalışır.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Struct;

namespace PdfPositioningDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Initialize the document
            Document pdfDoc = new Document();
            Page pdfPage = pdfDoc.Pages.Add();

            // Step 2: Define and position the paragraph
            Paragraph positionedParagraph = new Paragraph
            {
                Position = new Position(72, 720) // 1 inch left, 10 inches up
            };
            positionedParagraph.Segments.Add(
                new TextFragment("Tagged paragraph at a specific location.")
            );

            // Step 3: Create the structural element (tag)
            StructureElement structElement = new StructureElement("P");
            structElement.AddKid(positionedParagraph);

            // Step 4: Attach the structural element to the page
            pdfPage.StructElements.Add(structElement);

            // Step 5: Save as PDF/A‑2b
            string outputPath = @"C:\Temp\TaggedWithPosition.pdf";
            pdfDoc.Save(outputPath, SaveFormat.PdfA2b);

            Console.WriteLine($"PDF created successfully at: {outputPath}");
        }
    }
}
```

**Beklenen çıktı:** Çalıştırdıktan sonra `TaggedWithPosition.pdf` dosyasını açın. “Tagged paragraph at a specific location.” cümlesinin ilk sayfanın sağ‑alt köşesine yakın bir konumda durduğunu göreceksiniz. PDF’nin etiketlerini (ör. Adobe Acrobat’ın “Tags” paneli) incelerseniz, bu paragrafla ilişkilendirilmiş bir `<P>` elemanı bulacaksınız.

---

![Screenshot of positioned text in a PDF generated with Aspose.Pdf](/images/pdf-positioned.png){: .align-center }

*Görsel alt metni:* **create pdf document c#** – Aspose.Pdf ile oluşturulmuş bir PDF içinde konumlandırılmış metni gösteren ekran görüntüsü.

---

## Yaygın Sorular & Kenar Durumları

### Başka bir birim (mm, cm) kullanabilir miyim?

Aspose.Pdf yerel olarak nokta birimini kullanır. Milimetre tercih ediyorsanız `1 mm ≈ 2.83465 pt` dönüşümünü uygulayın. Örneğin, `Position(25.4, 254)` ifadesi paragrafı sol kenardan 1 cm, alt kenardan 9 cm yukarıya yerleştirir.

### Birden fazla etiket (başlıklar, tablolar) eklemem gerekirse?

Basitçe `"H1"` gibi başlıklar veya `"Table"` gibi tablolar için ek `StructureElement` nesneleri oluşturup ilgili içeriği çocuk olarak ekleyin. İç içe yapı aynı şekilde çalışır—çocuklar, ebeveynin mantıksal sırasını devralır.

### Bu yöntem PDF/A‑1b veya PDF/A‑3b için de geçerli mi?

Evet. `SaveFormat.PdfA2b` yerine `SaveFormat.PdfA1b` veya `SaveFormat.PdfA3b` kullanın. Her PDF/A sürümünün kendine özgü zorunlu meta verileri vardır; eksik bir şey varsa Aspose.Pdf sizi uyarır.

---

## Özet

**create pdf document c#** senaryosunu şu adımlarla tamamladık:

1. Aspose.Pdf kullanarak yeni bir PDF nesnesi oluşturduk.  
2. **Position text in PDF** adımıyla tam koordinatlar belirleyerek metni konumlandırdık.  
3. **Add structural tree** adımıyla erişilebilirlik için yapı elemanları ekledik.  
4. Sonucu standart‑uyumlu PDF/A‑2b dosyası olarak kaydettik.

Tüm adımlar bağımsızdır ve daha karmaşık düzenler, çoklu sayfalar veya farklı etiket türleri için kolayca uyarlanabilir.

---

## Sıradaki Adımlar

- **Metin biçimlendirme** – `TextState` ile yazı tiplerini, renkleri ve boyutları değiştirin.  
- **Görsel ekleme** – `ImageFragment` kullanarak paragrafın yanına resim yerleştirin.  
- **Tablo oluşturma** – `Table` nesneleri yaratın ve `"Table"` etiketiyle işaretleyerek daha zengin semantik sağlayın.  
- **Otomasyon hatları** – Bu kodu, faturaları gece yarısı otomatik olarak üreten bir arka plan hizmetine entegre edin.

Denemeler yapın ve hangi varyasyonların sizin için en faydalı olduğunu bize bildirin. İyi kodlamalar!

## Bir Sonraki Öğrenmeniz Gerekenler

Aşağıdaki öğreticiler, bu rehberde gösterilen teknikleri temel alan ve ilgili konuları derinlemesine ele alan kaynaklardır. Her biri, kendi projelerinizde ek API özelliklerini keşfetmeniz ve alternatif uygulama yaklaşımları denemeniz için adım adım kod örnekleri içerir.

- [Create Tagged PDFs with Aspose.PDF for .NET: A Complete Guide to Enhancing Accessibility and Document Structure](/pdf/english/net/advanced-features/create-tagged-pdfs-aspose-pdf-net/)
- [Create PDF Document with Aspose.PDF – Step‑by‑Step Guide](/pdf/english/net/document-creation/create-pdf-document-with-aspose-pdf-step-by-step-guide/)
- [Create & Rotate Text in PDFs Using Aspose.PDF .NET: A Comprehensive Guide for Developers](/pdf/english/net/text-operations/create-rotate-text-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}