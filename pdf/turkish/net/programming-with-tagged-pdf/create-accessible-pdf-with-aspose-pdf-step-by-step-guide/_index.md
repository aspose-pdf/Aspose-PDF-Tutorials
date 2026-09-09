---
category: general
date: 2026-02-10
description: C#'ta Aspose.Pdf kullanarak erişilebilir PDF oluşturun. Boş sayfa PDF
  eklemeyi, erişilebilirlik etiketleri eklemeyi, metni PDF'de konumlandırmayı ve PDF
  sayfasını programlı olarak oluşturmayı öğrenin.
draft: false
keywords:
- create accessible pdf
- add blank page pdf
- add accessibility tags
- position text pdf
- create pdf page programmatically
language: tr
og_description: C#'ta erişilebilir PDF oluşturun. Bu öğretici, boş bir sayfa PDF ekleme,
  içeriği etiketleme, metni PDF içinde konumlandırma ve PDF sayfasını programlı olarak
  oluşturma konularında size rehberlik eder.
og_title: Aspose.Pdf ile Erişilebilir PDF Oluşturma – Tam Rehber
tags:
- Aspose.Pdf
- C#
- PDF Accessibility
title: Aspose.Pdf ile Erişilebilir PDF Oluşturma – Adım Adım Rehber
url: /tr/net/programming-with-tagged-pdf/create-accessible-pdf-with-aspose-pdf-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Pdf ile Erişilebilir PDF Oluşturma – Adım Adım Kılavuz

Erişilebilir PDF **dosyaları oluşturmanız** gerektiğinde ama nereden başlayacağınızı bilemediğiniz oldu mu? Birçok projede—uygulama raporları veya e‑öğrenme modüllerini düşünün—erişilebilirlik isteğe bağlı değil, zorunludur. Neyse ki, Aspose.Pdf size boş bir sayfa PDF eklemek, erişilebilirlik etiketleri eklemek ve metni tam olarak konumlandırmak için temiz bir API sunar, tüm bunları C# kod tabananızdan çıkmadan yapabilirsiniz.

Bu öğreticide, **erişilebilir PDF** belgelerini programlı olarak nasıl **oluşturacağınızı**, boş bir sayfa PDF eklemeyi, içeriği ekran okuyucular için etiketlemeyi ve metnin bulunduğu görsel dikdörtgeni nasıl kontrol edeceğinizi tam olarak göreceksiniz. Sonunda, herhangi bir PDF okuyucusunda açabileceğiniz ve etiketlerin mevcut olduğunu doğrulayabileceğiniz çalışan bir dosyanız olacak.

## Gerekenler

- .NET 6.0 veya daha yeni bir sürüm (kod .NET Core ile de çalışır)  
- Aspose.Pdf for .NET NuGet paketi (`Aspose.Pdf`) – sürüm 23.12 veya daha yenisi  
- Visual Studio, Rider veya tercih ettiğiniz IDE’de basit bir console ya da class‑library projesi  

Hepsi bu. Ekstra framework yok, gizli konfigürasyon dosyası yok—sadece düz C# ve Aspose.Pdf.

## Erişilebilir PDF Oluşturma – Genel Bakış

Genel akış oldukça basit:

1. **Initialize** yeni bir `Document` nesnesi (PDF konteyneri).  
2. **Add a blank page PDF** ekleyerek üzerine çalışabileceğiniz bir tuval oluşturun.  
3. **Create a paragraph** oluşturun ve erişilebilir olmasını istediğiniz metni ekleyin.  
4. **Define a rectangle** ile PDF’nin paragrafın nerede görüneceğini belirleyin—bu “position text PDF” adımıdır.  
5. **Wrap the paragraph in an accessibility tag** ve bunu sayfanın etiketli içerik ağacına ekleyin.  
6. **Save** dosyayı kaydedin, etiketleri yardımcı teknolojiler için koruyun.

Aşağıda bu adımları tek tek inceleyecek, *neden* önemli olduklarını açıklayacak ve doğrudan kopyalayıp yapıştırabileceğiniz kodları göstereceğiz.

## Adım 1: Document’i Başlatma (Programatik Olarak PDF Sayfası Oluşturma)

İlk iş olarak bir `Document` örneğine ihtiyacınız var. Bunu, daha sonra doldireceğiniz boş bir kitap gibi düşünün.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Tags;

// Step 1: Create a new PDF document (this is the programmatic page creation)
using var pdfDocument = new Document();
```

> **Neden?**  
> `Document`, sayfaları, kaynakları ve etiketli‑içerik ağacını tutan kök nesnedir. Onsuz boş bir sayfa PDF ekleyemez veya herhangi bir etiket ekleyemezsiniz.

## Adım 2: Boş Bir Sayfa PDF Ekleme

Sayfası olmayan bir PDF temelde görünmezdir. Boş bir sayfa eklemek, içeriğinizi konumlandırabileceğiniz bir yüzey sağlar.

```csharp
// Step 2: Add a blank page PDF to the document
var pdfPage = pdfDocument.Pages.Add();
```

> **İpucu:**  
> Birden fazla sayfaya ihtiyacınız varsa, `pdfDocument.Pages.Add()` metodunu tekrar tekrar çağırın. Her çağrı, ayrı ayrı manipüle edebileceğiniz yeni bir `Page` nesnesi döndürür.

## Adım 3: Erişilebilir Bir Paragraf Oluşturma (Erişilebilirlik Etiketleri Ekleme)

Şimdi ekran okuyucular tarafından okunacak gerçek metni oluşturuyoruz. Bunu bir `Paragraph` nesnesine sararak etiketlemeye hazır hâle getiriyoruz.

```csharp
// Step 3: Build a paragraph that contains accessible text
var accessibleParagraph = new Paragraph
{
    // The text that will be announced by assistive tech
    Text = "Accessible paragraph"
};
```

> **Neden etiket?**  
> Erişilebilirlik etiketleri (`Add accessibility tags`) eklemek, NVDA veya VoiceOver gibi araçlara mantıksal okuma sırasının nereden başlayacağını söyler ve PDF’nin herkes için gerçekten kullanılabilir olmasını sağlar.

## Adım 4: Metni Görsel Bir Dikdörtgenle Konumlandırma (Position Text PDF)

 PDF koordinatları bir dikdörtgenle ifade edilir: lower‑left‑x (LLX), lower‑left‑y (LLY), upper‑right‑x (URX), upper‑right‑y (URY). İşte “position text PDF” adımı.

```csharp
// Step 4: Define where the paragraph will appear on the page
var visualRect = new Rectangle(50, 700, 550, 720);
```

> **Bu ne anlama geliyor?**  
> Dikdörtgen, sol kenardan 50 puan ve alttan 700 puan uzaklıkta başlar, yatayda 550 puan, dikeyde 720 puan uzanır. Bu sayıları düzenleyerek tasarımınıza göre ayarlayabilirsiniz.

## Adım 5: Paragrafı Etiketle ve Etiketli İçerik Ağacına Ekle

İşte **add accessibility tags** işleminin özü: hem mantıksal içeriğini hem de görsel konumunu bilen bir paragraf öğesi oluşturur, ardından bunu sayfanın kök etiket öğesine ekleriz.

```csharp
// Step 5: Create a tagged paragraph element with position info
var taggedParagraph = pdfPage.TaggedContent.CreateParagraphElement(accessibleParagraph, visualRect);

// Append the tagged element to the page's root element
pdfPage.TaggedContent.RootElement.AppendChild(taggedParagraph);
```

> **Neden bu önemli:**  
> `TaggedContent` API’si, PDF okuyucuların gezinmesi için bir yapı ağacı oluşturur. Öğeyi `RootElement`’e ekleyerek paragrafın doğru okuma sırasına yerleşmesini sağlarsınız.

## Adım 6: Belgeyi Kaydet (Tüm Etiketleri Koru)

Son olarak dosyayı kalıcı hâle getiriyoruz. `Save` metodu, görsel sayfayı ve gizli erişilebilirlik bilgilerini birlikte yazar.

```csharp
// Step 6: Save the PDF with all tags intact
pdfDocument.Save("YOUR_DIRECTORY/tagged_with_position.pdf");
```

> **Doğrulama ipucu:**  
> Oluşan dosyayı Adobe Acrobat Reader’da açın, *View → Show/Hide → Navigation Panes → Tags* yolunu izleyin. Sayfanın altında bir `P` (Paragraph) düğümü görmelisiniz—bu, etiketlerin mevcut olduğunu doğrular.

## Tam Çalışan Örnek

Aşağıda, tüm importları, yorumları ve yukarıda anlatılan adımları içeren, kopyala‑yapıştır‑hazır program yer alıyor.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Tags;

namespace AccessiblePdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize the PDF document
            using var pdfDocument = new Document();

            // 2️⃣ Add a blank page PDF
            var pdfPage = pdfDocument.Pages.Add();

            // 3️⃣ Create an accessible paragraph
            var accessibleParagraph = new Paragraph
            {
                Text = "Accessible paragraph"
            };

            // 4️⃣ Define the visual rectangle (LLX, LLY, URX, URY)
            var visualRect = new Rectangle(50, 700, 550, 720);

            // 5️⃣ Tag the paragraph with its position
            var taggedParagraph = pdfPage.TaggedContent.CreateParagraphElement(
                accessibleParagraph, visualRect);
            pdfPage.TaggedContent.RootElement.AppendChild(taggedParagraph);

            // 6️⃣ Save the PDF (ensure the output folder exists)
            pdfDocument.Save("tagged_with_position.pdf");

            // Optional: let the user know we're done
            System.Console.WriteLine("Accessible PDF created successfully!");
        }
    }
}
```

**Beklenen sonuç:**  
- `tagged_with_position.pdf` adlı tek sayfalı bir PDF.  
- “Accessible paragraph” metni sayfanın üst kısmına yakın bir konumda görünecek.  
- Belge, ekran okuyucu yazılımları tarafından okunabilir bir mantıksal etiket ağacına sahip olacak.

## Sık Sorulan Sorular ve Kenar Durumları

### Aynı sayfada birden fazla paragraf ihtiyacım olsaydı?

Ek `Paragraph` nesneleri oluşturun, her biri için ayrı `Rectangle` tanımlayın ve her biri için `CreateParagraphElement` metodunu çağırın. Okuma sırasını istediğiniz gibi belirlemek için onları ekleme sırasına göre ekleyin.

### Etiketleri korurken yazı tipi stillerini ayarlayabilir miyim?

Kesinlikle. `Paragraph` oluşturduktan sonra bir `TextState` atayabilirsiniz:

```csharp
accessibleParagraph.TextState.Font = FontRepository.FindFont("Arial");
accessibleParagraph.TextState.FontSize = 12;
accessibleParagraph.TextState.FontStyle = FontStyles.Bold;
```

Etiket aynı kalır çünkü stil sadece görsel bir özelliktir, yapısal bir değişiklik değildir.

### Bu, PDF/A‑2b (arşiv) uyumluluğu ile çalışır mı?

Evet. Aspose.Pdf, kaydetmeden önce PDF/A uyumluluk seviyesini ayarlamanıza izin verir:

```csharp
pdfDocument.Convert(new PdfFormatConversionOptions { ConvertToPdfA = PdfAStandard.PdfA2b });
```

Erişilebilirlik etiketleri PDF/A sürümünde korunur.

### Etiketleri programlı olarak nasıl doğrularım?

Etiket ağacını şu şekilde döngüye alabilirsiniz:

```csharp
var root = pdfPage.TaggedContent.RootElement;
foreach (var child in root.ChildElements)
{
    System.Console.WriteLine($"Tag: {child.ElementType}");
}
```

`Paragraph` girdileri görürseniz, her şey yolunda demektir.

## Sonuç

Aspose.Pdf kullanarak **erişilebilir PDF** dosyaları **oluşturma**, **boş sayfa PDF ekleme**, **erişilebilirlik etiketleri ekleme**, **metni PDF’de konumlandırma** ve **programatik olarak PDF sayfası oluşturma** süreçlerini adım adım inceledik. Kod çalıştırılmaya hazır, kavramlar açıklanmış ve .NET projenizde uyumlu PDF’ler üretmek için sağlam bir temeliniz var.

Sırada ne var? `ImageFragment` ile görseller ekleyebilir, tablolar oluşturabilir ya da çok sayfalı bir erişilebilir rapor üretebilirsiniz. Her yeni öğe, paragraf için yaptığımız gibi etiketlenebilir, böylece belgeleriniz her zaman kapsayıcı kalır.

Burada ele alınmayan bir senaryonuz mu var? Yorum bırakın, birlikte çözümleyelim. Mutlu kodlamalar ve PDF’lerinizi erişilebilir tutun!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}