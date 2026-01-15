---
category: general
date: 2026-01-15
description: C# ile Aspose.Pdf kullanarak etiketli PDF oluşturun. PDF'ye başlık eklemeyi,
  erişilebilir metin ayarlamayı ve PDF'ye sayfa eklemeyi adım adım öğrenin.
draft: false
keywords:
- create tagged pdf
- add heading to pdf
- how to add heading
- add page to pdf
- set accessible text
language: tr
og_description: Aspose.Pdf ile C#'ta etiketli PDF oluşturun. Bu kılavuz, PDF'ye başlık
  eklemeyi, erişilebilir metin ayarlamayı ve PDF'ye sayfa eklemeyi gösterir.
og_title: C#'ta Etiketli PDF Oluştur – Başlık ve Erişilebilir Metin Ekle
tags:
- Aspose.Pdf
- C#
- PDF accessibility
title: C#'ta Etiketli PDF Oluşturma – Başlık ve Erişilebilir Metin Ekle
url: /tr/net/programming-with-tagged-pdf/create-tagged-pdf-in-c-add-heading-accessible-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# ile Etiketli PDF Oluşturma – Başlık ve Erişilebilir Metin Ekleme

Hiç **etiketli PDF** dosyaları oluşturmanız gerekti ama nereden başlayacağınızı bilemediğiniz oldu mu? Bu öğreticide, PDF'e başlık ekleme, erişilebilir metin ayarlama ve hatta PDF'e yeni bir sayfa ekleme adımlarını Aspose.Pdf for .NET kullanarak adım adım göstereceğiz.  

Ekran okuyucuların anlayabileceği *başlık ekleme* konusunda merak ettikleriniz varsa, doğru yerdesiniz. Sonunda, uyumluluk odaklı müşterilere veya iç denetçilere sunabileceğiniz tam etiketli, erişilebilir bir PDF elde edeceksiniz.

## Öğrenecekleriniz

- Aspose.Pdf ile sıfırdan **etiketli pdf** oluşturma  
- **pdf'e başlık ekleme** ve altına bir paragraf yerleştirme kodu  
- Yardımcı teknolojilerin doğru içeriği okuması için **erişilebilir metin ayarlama** yolları  
- Daha fazla alana ihtiyaç duyduğunuzda **pdf'e sayfa ekleme** için hızlı bir ipucu  
- Kaçınılması gereken en iyi uygulama tuzakları (ve birkaç profesyonel ipucu)

> **Önkoşul:** .NET 6+ (veya .NET Framework 4.6+) ve geçerli bir Aspose.Pdf lisansı ya da deneme DLL'i. Başka bir kütüphane gerekmez.

![Create tagged PDF example](image.png "Başlık ve paragraf içeren etiketli bir PDF ekran görüntüsü – create tagged pdf")

## Etiketli PDF Oluşturma – Genel Bakış

Bireysel adımlara geçmeden önce büyük resmi anlayalım. **Etiketli bir PDF**, okuma sırasını ve anlamsal yapıyı (başlıklar, paragraflar, tablolar vb.) tanımlayan mantıksal bir yapı ağacına sahiptir. Bu ağaç, ekran okuyucuların görme engelli kullanıcılara anlamı aktarmak için kullandığı şeydir.  

Aspose.Pdf, bu ağacı programatik olarak oluşturmanızı sağlayan bir `TaggedContent` nesnesi sunar. Bunu bir LEGO seti gibi düşünün: parçaları (başlık, paragraf) oluşturur ve doğru sırada birleştirirsiniz.

### Tam Çalışan Örnek (Tüm Adımlar Birleştirilmiş)

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Tagged;

namespace TaggedPdfDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create a new PDF document and add a page (add page to pdf)
            Document pdfDocument = new Document();
            Page pdfPage = pdfDocument.Pages.Add();

            // 2️⃣ Access the tagged content and create a level‑1 heading (add heading to pdf)
            TaggedContent taggedContent = pdfDocument.TaggedContent;
            HeadingElement heading = taggedContent.CreateHeadingElement(1);
            heading.Position = new Position { X = 50, Y = 750 }; // coordinates in points

            // 3️⃣ Create a paragraph and set its accessible text (set accessible text)
            ParagraphElement paragraph = taggedContent.CreateParagraphElement();
            paragraph.Text = "This is an accessible paragraph.";

            // 4️⃣ Build the hierarchy – heading contains the paragraph
            heading.AppendChild(paragraph);
            taggedContent.RootElement.AppendChild(heading);

            // 5️⃣ Save the tagged PDF to disk
            pdfDocument.Save("tagged_out.pdf");
        }
    }
}
```

Programı çalıştırın ve `tagged_out.pdf` dosyasını etiketleri gösteren bir PDF okuyucusunda açın (ör. Adobe Acrobat → View → Show/Hide → Navigation Panes → Tags). **Heading 1** ardından bir paragraf görmelisiniz – tam olarak planladığımız gibi.

Aşağıda her adımı ayrıntılı olarak açıklıyor, *neden* önemli olduğunu belirtiyor ve birkaç ekstra seçeneği ekliyoruz.

## PDF'e Sayfa Ekleme

Tek sayfalık bir belge de etiketlenebilir, ancak çoğu gerçek dünya PDF'i daha fazla alana ihtiyaç duyar. Sayfa eklemek çok basittir:

```csharp
// Add a new page – this is the “add page to pdf” step
Page newPage = pdfDocument.Pages.Add();
```

> **Sayfa ekleme nedeni:**  
> Etiketler belirli sayfa koordinatlarına bağlanır. Y koordinatları sayfa yüksekliğini aşarsa metin kırpılır. Yeni bir sayfa eklemek temiz bir tuval sağlar ve düzeninizin tutarlı kalmasını garantiler.

**Pro ipucu:** Yatay bir sayfa ihtiyacınız varsa, öğeleri konumlandırmadan önce `newPage.PageInfo.Orientation = PageOrientation.Landscape;` satırını ekleyin.

## PDF'e Başlık Ekleme

Başlıklar yapıyı oluşturur. Yukarıdaki kodda `CreateHeadingElement(1)` kullanarak **Seviye‑1** başlık oluşturduk. Alt bölümler için daha derin seviyeler (2, 3, …) oluşturabilirsiniz.

```csharp
HeadingElement heading = taggedContent.CreateHeadingElement(1);
heading.Position = new Position { X = 50, Y = 750 };
```

- **X** ve **Y** noktalar (point) cinsindendir (1 pt = 1/72 in).  
- `Y` değerini ayarlayarak başlığı yukarı ya da aşağı taşıyabilirsiniz; daha düşük değerler başlığı sayfanın altına yaklaştırır.

> **Yaygın hata:** `heading.Position` ayarlamayı unutmak. Koordinatlar olmadan başlık etiket ağacında yer alır ama sayfada görünmez, bu da ekran okuyucuları şaşırtır.

Kalın bir stil isterseniz, bir `TextState` ekleyebilirsiniz:

```csharp
heading.TextState = new TextState { FontSize = 18, FontStyle = FontStyles.Bold };
```

## Paragraf İçin Erişilebilir Metin Ayarlama

Paragraflar içeriğinizin büyük kısmını oluşturur. Yardımcı teknolojiler tarafından okunabilir olmaları için *erişilebilir metin* sağlamalısınız:

```csharp
ParagraphElement paragraph = taggedContent.CreateParagraphElement();
paragraph.Text = "This is an accessible paragraph.";
```

`Text` özelliği, bir ekran okuyucunun duyuracağı metindir. Unicode karakterler, emoji'ler ya da sağ‑dan‑sola script'ler ekleyebilirsiniz—Aspose.Pdf bunları sorunsuz işler.

**Köşe durumu:** Paragrafta bir hiperlink bulunuyorsa, paragraf içinde `LinkElement` kullanın ve açıklayıcı bir etiket için `Alt` özniteliğini ayarlayın.

## Etiketli PDF'i Kaydetme

Son adım belgeyi kalıcı hâle getirmektir:

```csharp
pdfDocument.Save("tagged_out.pdf");
```

PDF'i doğrudan bir web yanıtına akıtmak da mümkündür:

```csharp
using (MemoryStream ms = new MemoryStream())
{
    pdfDocument.Save(ms);
    // return File(ms.ToArray(), "application/pdf", "report.pdf");
}
```

> **Neden sadece `pdfDocument.Save("output.pdf")` kullanılmaz?**  
> PDF'leri HTTP üzerinden sunmayı planlıyorsanız, akış (stream) kullanmak geçici dosyaların diske yazılmasını önler ve I/O yükünü azaltır.

## Etiket Yapısını Doğrulama (Opsiyonel ama Tavsiye Edilir)

Dosyayı oluşturduktan sonra Adobe Acrobat'ta açın:

1. **View → Show/Hide → Navigation Panes → Tags**  
2. Ağacı genişletin; `H1` (başlığınız) altında bir `P` (paragraf) görmelisiniz.  

Hiyerarşi doğruysa, **create[d] tagged pdf** oluşturmuş ve WCAG 2.1 AA belge erişilebilirliği gereksinimlerini karşılamış olursunuz.

## Yaygın Tuzaklar & Pro İpuçları

| Tuzak | Nasıl Önlenir |
|---------|--------------|
| Kök öğeye `AppendChild` çağırmayı unutmak | Her zaman `taggedContent.RootElement.AppendChild(heading);` ile bitirin |
| Sayfa sınırları dışındaki koordinatlar | Güvenli aralıkları hesaplamak için `pdfPage.PageInfo.Width/Height` kullanın |
| Okunabilirlik için `TextState` ayarlamamak | Varsayılan bir yazı tipi boyutu (12‑14 pt) ve yeterli kontrast tanımlayın |
| Gereksiz öğeler ekleyerek aşırı etiketleme | Sadece anlamsal etiketleri kullanın: heading, paragraph, list, table |
| Dil meta verisini göz ardı etmek | Ekran okuyucu algısını iyileştirmek için `pdfDocument.Language = "en-US";` ayarlayın |

## Sonraki Adımlar

- **Daha fazla içerik türü ekleyin:** tablolar (`TableElement`), görseller (`ImageElement`) ve listeler (`ListElement`).  
- **Uluslararasılaştırma:** `pdfDocument.Language` değerini değiştirin ve Unicode metin sağlayın.  
- **Dijital imzalar:** `SignatureField` ile etiketli PDF'inizi güvence altına alın.  

Tüm bunlar, **create tagged pdf** dosyaları oluşturmak için şimdi sahip olduğunuz temelin üzerine inşa edilecektir; hem makine‑okunur hem de insan‑dostu.

---

### TL;DR

Artık Aspose.Pdf kullanarak **create tagged pdf**, **add heading to pdf**, **set accessible text** ve gerektiğinde **add page to pdf** nasıl yapılır biliyorsunuz. Yukarıdaki tam, çalıştırılabilir örnek herhangi bir .NET projesine eklenmeye hazır. Farklı başlık seviyeleri, yazı tipleri ve ek etiketlerle deneyler yapın—bir sonraki erişilebilir PDF'iniz sadece birkaç satır uzakta. Kodlamanın tadını çıkarın!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}