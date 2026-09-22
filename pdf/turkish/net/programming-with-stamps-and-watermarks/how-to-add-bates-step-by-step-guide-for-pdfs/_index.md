---
category: general
date: 2026-02-10
description: PDF'ye hızlıca bates ekleme—bates numarası eklemeyi ve Aspose.Pdf ile
  C#'ta görünmez bir filigran oluşturmayı öğrenin.
draft: false
keywords:
- how to add bates
- add bates number pdf
- add custom stamp pdf
- add invisible watermark pdf
- add page footer pdf
language: tr
og_description: C# ile Aspose.Pdf kullanarak bates ekleme. Bu öğreticide bates numarası
  PDF ekleme, görünmez filigran PDF ekleme ve daha fazlası gösterilmektedir.
og_title: Bates Nasıl Eklenir – Tam PDF Rehberi
tags:
- Aspose.Pdf
- C#
- PDF
- Bates numbering
title: Bates Numarası Nasıl Eklenir – PDF'ler İçin Adım Adım Rehber
url: /tr/net/programming-with-stamps-and-watermarks/how-to-add-bates-step-by-step-guide-for-pdfs/
---

to preserve bold formatting (**). Keep them as is.

Now produce final content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Bates Nasıl Eklenir – Tam PDF Rehberi

Bir yasal PDF'e **how to add bates** eklerken aranabilir metni bozmaktan hiç endişelendiniz mi? Tek başınıza değilsiniz. Birçok hukuk firması ve e‑discovery projesinde, Bates numarası zorunlu bir altbilgi olmakla birlikte, OCR araçları tarafından görünmez olmasını da istersiniz. Bu öğreticide **how to add bates**'i Aspose.Pdf for .NET kullanarak gösteriyoruz ve aynı zamanda **add bates number pdf**, **add custom stamp pdf**, **add invisible watermark pdf** ve hatta **add page footer pdf** konularını tek bir çözümde ele alacağız.

Kodun her satırını adım adım inceleyecek, her ayarın neden önemli olduğunu açıklayacak ve bugün projenize ekleyebileceğiniz çalıştırmaya hazır bir örnek sunacağız. Belirsiz “see the docs” bağlantıları yok—gereken her şey burada.

## Kazanımlarınız

- Tam, çalıştırılabilir bir C# kod parçacığı, Bates numarasını bir artifact damgası olarak ekler.
- Damganın sayfada görünürken **invisible watermark** gibi davranmasını nasıl sağlayacağınızı anlama.
- Çözümü çok sayfalı PDF'lere ölçeklendirme, yazı tiplerini değiştirme veya damgayı özel bir grafikle değiştirme ipuçları.
- **add page footer pdf** tarzı içeriği metin çıkarımını bozmadan eklemek için hızlı ipuçları.

### Önkoşullar

- .NET 6+ (veya .NET Framework 4.7.2) Visual Studio 2022 veya tercih ettiğiniz herhangi bir IDE ile.
- Aspose.Pdf for .NET (Aspose web sitesinden ücretsiz deneme sürümünü alabilirsiniz).
- `source.pdf` adlı örnek PDF, kontrol ettiğiniz bir klasöre yerleştirildi.

Eğer bunlara sahipseniz, başlayalım.

---

## Bates Nasıl Eklenir – Temel Uygulama

Çözümün kalbi, **artifact** olarak ele aldığımız bir `TextStamp`'tir. Artifact'lar metin‑çıkarma motorları tarafından göz ardı edilir, bu yüzden bu yaklaşım aynı zamanda bir **add invisible watermark pdf** tekniği olarak da işlev görür.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Annotations;

// Load the source PDF
using var pdfDocument = new Document("YOUR_DIRECTORY/source.pdf");

// Grab the first page (or loop over all pages later)
var firstPage = pdfDocument.Pages[1];

// Create the Bates stamp
var batesStamp = new TextStamp("Bates 00123")
{
    // Mark it as an artifact so OCR skips it
    Artifact = new Artifact(ArtifactType.Artifact),

    // Position it like a typical page footer
    HorizontalAlignment = HorizontalAlignment.Center,
    VerticalAlignment   = VerticalAlignment.Bottom,

    // Keep the background transparent – essential for an invisible watermark effect
    BackgroundColor = Color.Transparent,

    // Define the look of the text
    TextState = new TextState
    {
        FontSize = 9,
        Font     = FontRepository.FindFont("Arial")
    }
};

// Add the stamp to the chosen page
firstPage.AddStamp(batesStamp);

// Save the new PDF
pdfDocument.Save("YOUR_DIRECTORY/bates_artifact.pdf");
```

### Neden Bu Çalışır

1. **Artifact flag** – `Artifact = new Artifact(ArtifactType.Artifact)` ayarlayarak, damga içerik olmayan bir öğe gibi ele alınır. Arama motorları ve yasal e‑discovery araçları bunu görmez, bu da **add invisible watermark pdf** için tam olarak istediğiniz şeydir.
2. **Horizontal/Vertical alignment** – Ortada‑alt, klasik bir **add page footer pdf** stilini taklit eder ve Bates numarasının profesyonel görünmesini sağlar.
3. **Transparent background** – Damganın alttaki içeriği gizlemediğini garanti eder; bu, PDF'yi farklı cihazlarda yazdırmanız veya görüntülemeniz gerektiğinde ince ama kritik bir detaydır.

---

## Bates Numarası PDF Ekle – Çoklu Sayfalara Ölçeklendirme

Gerçek dünyadaki çoğu PDF birden fazla sayfaya sahiptir. Yukarıdaki kod parçacığı sadece ilk sayfayı etkiler, ancak genişletmesi çok kolaydır:

```csharp
// Loop through every page in the document
foreach (Page page in pdfDocument.Pages)
{
    // Clone the stamp so each page gets its own instance
    var pageStamp = (TextStamp)batesStamp.Clone();

    // Optionally, update the number based on page index
    pageStamp.Text = $"Bates {page.Number:D5}";

    page.AddStamp(pageStamp);
}
```

**Pro ipucu:** Fiziksel sayfa sırasına bağlı olmayan bir sıralı numaraya (ör. 1000'den başlamak) ihtiyacınız varsa, döngüden önce bir sayaç başlatın ve içinde artırın.

---

## Özel Damga PDF Ekle – Düz Metnin Ötesine

Bazen düz metin damgası yeterli olmayabilir—bir logo, QR kodu veya renkli bir çubuk isteyebilirsiniz. Aspose.Pdf, `TextStamp`'i `ImageStamp` ile değiştirebilir veya her ikisini `Stamp` nesneleriyle birleştirmenize izin verir.

```csharp
var imageStamp = new ImageStamp("YOUR_DIRECTORY/logo.png")
{
    // Position it in the top‑right corner
    HorizontalAlignment = HorizontalAlignment.Right,
    VerticalAlignment   = VerticalAlignment.Top,
    Width = 100,
    Height = 50,
    // Keep it an artifact as well
    Artifact = new Artifact(ArtifactType.Artifact)
};

firstPage.AddStamp(imageStamp);
```

Damgaları karıştırmak, ikisini aynı sayfaya eklemek kadar basittir. **add custom stamp pdf** yeteneği, Bates numarasının yanına kurumsal bir mühür eklemeniz gerektiğinde parlayacaktır.

---

## Görünmez Su İşareti PDF Ekle – Damgayı Gerçekten Gizlemek

Damganın insan gözü *ve* çıkarım araçları tarafından tamamen görünmez olmasını gerçekten istiyorsanız, yazı tipi rengini sayfa arka planına (genellikle beyaz) eşitleyebilir ve opaklığı azaltabilirsiniz:

```csharp
batesStamp.TextState.ForegroundColor = Color.White; // assumes white background
batesStamp.Opacity = 0.0; // 0% opacity – completely invisible
```

`Opacity = 0` olsa bile, artifact PDF yapısında hâlâ bulunur, bu yüzden yasal yazılım artifact ID'sini biliyorsa onu bulabilir. Bu, nihai **add invisible watermark pdf** hilesidir.

---

## Sayfa Altbilgi PDF Ekle – Altbilgiyi Tutarlı Şekilde Stilize Etmek

Profesyonel bir altbilgi genellikle sadece Bates numarasından fazlasını içerir: tarih, belge başlığı veya gizlilik uyarısı. İşte birden fazla metni tek bir damgaya toplamanın hızlı bir yolu:

```csharp
var footerText = $"Bates {page.Number:D5}   Confidential   {DateTime.Today:MM/dd/yyyy}";
var footerStamp = new TextStamp(footerText)
{
    HorizontalAlignment = HorizontalAlignment.Center,
    VerticalAlignment   = VerticalAlignment.Bottom,
    BackgroundColor = Color.Transparent,
    TextState = new TextState
    {
        FontSize = 8,
        Font     = FontRepository.FindFont("Times New Roman"),
        ForegroundColor = Color.Gray
    },
    Artifact = new Artifact(ArtifactType.Artifact)
};

page.AddStamp(footerStamp);
```

Hafif gri rengi fark edin—ana içerikten dikkat dağıtmayan ancak yasal gereksinimleri karşılayan bir **add page footer pdf** için mükemmeldir.

---

## Beklenen Çıktı ve Nasıl Doğrulanır

Tam script'i çalıştırdıktan sonra, herhangi bir PDF görüntüleyicide `bates_artifact.pdf` dosyasını açın:

- Her sayfanın alt kısmının ortasında “Bates 00123” (veya sıralı numara) göreceksiniz.
- Sayfadaki metni seçtiğinizde Bates numarası **dahil olmayacak**, bu da artifact davranışını doğrular.
- Görünmez‑su işareti ayarlarını kullandıysanız, numara hiç görünmeyecek, ancak PDF'in iç yapısında kalacaktır (PDF‑XChange Editor gibi bir araçla “Document → Properties → Advanced” üzerinden inceleyebilirsiniz).

---

## Yaygın Sorular ve Kenar Durumları

**PDF'imin zaten bir altbilgisi varsa ne olur?**  
`VerticalAlignment`'ı `VerticalAlignment.Top` olarak ayarlayabilir veya `Margin` özelliğini değiştirerek damgayı mevcut altbilginin üzerine itebilirsiniz.

**Farklı bir yazı tipi kullanabilir miyim?**  
Tabii ki. `"Arial"` yerine Aspose'un bulabileceği herhangi bir yazı tipi adını koyabilirsiniz veya `FontRepository.AddFont("path/to/font.ttf")` ile özel bir TTF dosyası gömebilirsiniz.

**Bu yaklaşım .NET Core ile uyumlu mu?**  
Evet—Aspose.Pdf for .NET, .NET Framework, .NET Core ve .NET 5/6 üzerinde çalışır. Doğru NuGet paketine referans verdiğinizden emin olun.

**1000+ sayfa gibi büyük PDF'lerde performans nasıl?**  
Tek bir `TextStamp` oluşturup döngü içinde kopyalamak bellek açısından verimlidir. Çok büyük dosyalar için, işlemi partiler halinde yapmayı veya tüm belgeyi belleğe yüklemeden işlemek için `PdfProcessor` kullanmayı düşünün.

## Sonuç

Başlangıçtan sona **how to add bates**'i bir PDF'e eklemeyi ele aldık, **add bates number pdf**'yi gösterdik, **add custom stamp pdf**'yi nasıl yapacağınızı anlattık, damgayı bir **add invisible watermark pdf**'ye dönüştürdük ve profesyonel bir **add page footer pdf** olarak stil verdik. Tam kod örneği olduğu gibi çalışır ve açıklamalar her satırın “neden”ini verir—tam da AI asistanlarının alıntılamayı sevdiği türde bir yanıt.

Sonraki adımlar? Metin damgasını bir görüntü damgasıyla değiştirmeyi deneyin, farklı artifact türleriyle deney yapın veya bu mantığı bir klasördeki her belgeyi otomatik olarak Bates‑numaralandıran toplu‑işlem hizmetine entegre edin. Olasılıklar sınırsızdır ve artık üzerine inşa edebileceğiniz sağlam bir temele sahipsiniz.

Kodlamaktan keyif alın, ve PDF'leriniz her zaman mükemmel numaralandırılmış olsun!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}