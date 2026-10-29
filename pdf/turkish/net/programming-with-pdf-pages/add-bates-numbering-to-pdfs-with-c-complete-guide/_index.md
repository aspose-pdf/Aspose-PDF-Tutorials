---
category: general
date: 2026-06-24
description: C# ve Aspose.PDF kullanarak PDF dosyalarına Bates numaralandırması ekleyin.
  Özelleştirilmiş sayfa numaralarını, sıralı sayfa numaralarını ve başlık‑altbilgi
  numaralandırmasını dakikalar içinde öğrenin.
draft: false
keywords:
- add bates numbering
- custom page numbers
- sequential page numbers
- bates numbering pdf
- header footer numbering
language: tr
og_description: C# ve Aspose.PDF kullanarak PDF dosyalarına Bates numaralandırması
  ekleyin. Birkaç kolay adımda özel sayfa numaraları ve üst‑alt bilgi numaralandırmasını
  ustalaşın.
og_title: C# ile PDF'lere Bates Numaralandırması Ekle – Tam Rehber
schemas:
- author: Aspose
  dateModified: '2026-06-24'
  description: Add bates numbering to PDF files using C# and Aspose.PDF. Learn custom
    page numbers, sequential page numbers, and header footer numbering in minutes.
  headline: Add Bates Numbering to PDFs with C# – Complete Guide
  type: TechArticle
- description: Add bates numbering to PDF files using C# and Aspose.PDF. Learn custom
    page numbers, sequential page numbers, and header footer numbering in minutes.
  name: Add Bates Numbering to PDFs with C# – Complete Guide
  steps:
  - name: Load the Source PDF Document
    text: First we need a `Document` object that represents the file we want to modify.
  - name: Configure Bates Numbering Options (custom page numbers)
    text: Now we set up a `BatesNumberingOptions` object. This is where you define
      **custom page numbers**, the font, colors, and margins.
  - name: Apply the Bates Numbering to the Entire Document
    text: With the options prepared, the actual insertion is a single method call.
  - name: Save the PDF with Bates Numbers Applied
    text: Finally, write the modified document back to disk.
  - name: Limiting the Page Range
    text: 'Sometimes you only want to number a subset, such as pages 3‑10 of a 25‑page
      contract. Adjust `StartingPage` and `EndingPage` accordingly:'
  - name: Changing the Placement to Footer
    text: 'If your workflow requires **header footer numbering** at the bottom left,
      tweak the `Margin`:'
  - name: Using a Different Format
    text: 'Legal teams sometimes use “2024‑A‑001”. Just change the format string:'
  - name: Handling Transparent Backgrounds
    text: The `BackgroundColor = Color.Transparent` ensures the number doesn’t obscure
      existing content. If you need a light gray box behind the text for readability,
      replace it with `Color.LightGray`.
  type: HowTo
- questions:
  - answer: Yes—load the document with the password first (`pdfDocument = new Document("file.pdf",
      new LoadOptions { Password = "pwd" })`) then apply the same steps.
    question: Will this work with password‑protected PDFs?
  - answer: You can run `AddBatesNumbering` twice with two separate `BatesNumberingOptions`,
      each targeting either odd (`StartingPage = 1; EndingPage = pdfDocument.Pages.Count;
      PageSequence = PageSequence.Odd`) or even pages.
    question: Can I add different numbers to odd and even pages?
  - answer: A trial works for evaluation, but the trial adds a watermark. For production
      use you’ll need a valid license to get a clean **bates numbering pdf**.
    question: Do I need a license for Aspose.PDF?
  type: FAQPage
tags:
- Aspose.PDF
- C#
- PDF manipulation
title: C# ile PDF'lere Bates Numaralandırması Ekleyin – Tam Rehber
url: /tr/net/programming-with-pdf-pages/add-bates-numbering-to-pdfs-with-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# ile PDF'lere Bates Numaralandırması Ekle – Tam Kılavuz

PDF dosyalarınıza sadece birkaç satır kodla bates numaralandırması ekleyin. Hukuki özetler için özel sayfa numaralarına ya da bir sözleşme paketinde ardışık sayfa numaralarına ihtiyacınız olduysa, bu öğretici size yardımcı olacak.

Önümüzdeki birkaç dakikada, bir PDF'i yükleme, numaralandırma stilini yapılandırma, numaraları uygulama ve son olarak güncellenmiş dosyayı kaydetme konularını adım adım inceleyeceğiz. Sonunda, tek bir dosya ya da bir klasör içindeki belgeler olsun, **bates numbering pdf** oluşturabileceksiniz.

## Gereksinimler

İlerlemeye başlamadan önce aşağıdaki ön koşullara sahip olduğunuzdan emin olun:

- **.NET 6.0 veya üzeri** – kod .NET 6 hedefli, ancak daha eski .NET Framework sürümleri de çalışır.
- **Aspose.PDF for .NET** – bu rehberde kullanılan `Document` ve `BatesNumberingOptions` sınıflarını sağlayan ticari bir kütüphane (ücretsiz deneme mevcut).
- Bir **C# IDE** (Visual Studio, Rider veya VS Code) – .NET projelerini derleyebilen herhangi bir editör yeterli.
- Kodunuzdan referans verebileceğiniz bir klasörde bulunan `input.pdf` adlı giriş PDF'i.

Her şey hazır mı? Harika—başlayalım.

## Bates Numaralandırması Ekle – Genel Bakış

**add bates numbering** mantığının temelinde PDF'i bir kanvas olarak ele alıp, her sayfanın üst ya da alt kısmına “DOC‑001” gibi bir dizeyi boyamak yatar. Aspose.PDF ağır işi yapar: sadece formatı, sayfa aralığını ve görsel stili tanımlarsınız, kütüphane sizin için numaraları yazar.

Aşağıda, bir konsol uygulamasına kopyalayıp‑yapıştırabileceğiniz tam, çalıştırılabilir bir örnek bulunuyor. Her satır açıklanmıştır, böylece sadece *ne* yazmanız gerektiğini değil, *neden* her parçanın önemli olduğunu da anlayacaksınız.

### Adım 1: Kaynak PDF Belgesini Yükleyin

İlk olarak, değiştirmek istediğimiz dosyayı temsil eden bir `Document` nesnesine ihtiyacımız var.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Facades;
using System.Drawing;

// Load the source PDF (replace the path with your actual folder)
Document pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");
```

> **Neden önemli:** `Document` sınıfı tüm PDF işlemlerinin giriş noktasıdır. Dosyayı belleğe yükler ve `Pages` koleksiyonuna erişim sağlar; sayılara ekleme yaparken bu koleksiyon üzerinde döneceğiz.

### Adım 2: Bates Numaralandırma Seçeneklerini Yapılandırın (özel sayfa numaraları)

Şimdi bir `BatesNumberingOptions` nesnesi oluşturuyoruz. Burada **özel sayfa numaraları**, yazı tipi, renkler ve kenar boşlukları tanımlanır.

```csharp
BatesNumberingOptions batesOptions = new BatesNumberingOptions
{
    NumberingFormat = "DOC-{0:D3}",          // e.g., DOC-001, DOC-002 …
    StartNumber = 1,
    StartingPage = 1,
    EndingPage = pdfDocument.Pages.Count,
    Font = new Font(FontFamily.Helvetica, 12, FontStyle.Bold),
    ForegroundColor = Color.Black,
    BackgroundColor = Color.Transparent,
    Margin = new Margin(0, 20, 20, 0)        // top, right, bottom, left (points)
};
```

- **NumberingFormat** – `{0:D3}` yer tutucu, Aspose'a sayıları üç basamakla doldurmasını söyler.
- **StartNumber** – dizinin başladığı sayı; mevcut bir pakete ekleme yapıyorsanız değiştirin.
- **StartingPage / EndingPage** – sayfa aralığını tanımlar; ihtiyacınız olan alt küme için 2‑5 gibi bir aralık belirleyebilir, böylece sadece gerekli yerlerde **sequential page numbers** elde edersiniz.
- **Font & Colors** – **header footer numbering** için görsel stil; Helvetica, temiz ve okunaklı olduğu için hukuki belgelerde iyi çalışır.
- **Margin** – metni üst ve sağ kenarlardan 20 pt uzaklıkta konumlandırır; isterseniz bu değerleri değiştirerek sayıyı alt ya da sola taşıyabilirsiniz.

> **İpucu:** Sayıları üst kısım yerine alt kısma koymak isterseniz, `Margin` değerlerini `new Margin(0, 0, 20, 20)` (alt, sol) gibi değiştirin.

### Adım 3: Bates Numaralandırmasını Tüm Belgeye Uygulayın

Seçenekler hazır olduğunda, gerçek ekleme tek bir metod çağrısıdır.

```csharp
// Apply the numbering to every page in the defined range
pdfDocument.AddBatesNumbering(batesOptions);
```

Arka planda Aspose, seçilen sayfalar üzerinde döner, her sayıyı `NumberingFormat`a göre biçimlendirir ve dizeyi sayfa kanvasına çizer. Bu, **add bates numbering** işleminin kalbidir—manuel döngü gerekmez.

### Adım 4: Bates Numaralarıyla PDF'i Kaydedin

Son olarak, değiştirilmiş belgeyi diske yazın.

```csharp
// Save the output file (choose a different name to avoid overwriting the source)
pdfDocument.Save("YOUR_DIRECTORY/BatesNumbered.pdf");
```

`BatesNumbered.pdf` dosyasını açtığınızda, her sayfanın sağ‑üst köşesinde “DOC‑001”, “DOC‑002”, … gibi bir metin göreceksiniz. Bu, dosyalama ya da e‑keşif için hazır, tam işlevsel bir **bates numbering pdf** olur.

## Beklenen Sonuç

| Sayfa | Üst Bilgi (örnek) |
|------|-------------------|
| 1    | DOC‑001 |
| 2    | DOC‑002 |
| …    | … |
| N    | DOC‑00N |

Numaralar, `Margin` tarafından belirlenen konumda, Helvetica Bold 12‑pt yazı tipiyle görünür. Dosyayı Adobe Acrobat'ta açarsanız, sayıların sayfa içeriğinin bir parçası olduğunu—ayrı bir açıklama (annotation) olmadığını fark edersiniz; bu sayede baskı ve düzleştirme (flattening) sırasında da kalırlar.

## Kenar Durumları ve Varyasyonlar

### Sayfa Aralığını Sınırlama

Bazen sadece bir alt küme numaralandırmak istersiniz; örneğin 25 sayfalık bir sözleşmenin 3‑10. sayfaları. `StartingPage` ve `EndingPage` değerlerini buna göre ayarlayın:

```csharp
batesOptions.StartingPage = 3;
batesOptions.EndingPage = 10;
batesOptions.StartNumber = 1; // reset numbering for the subset
```

### Yerleşimi Alt Kısma Değiştirme

İş akışınız **header footer numbering**i alt sol köşeye koymayı gerektiriyorsa, `Margin` değerini şu şekilde değiştirin:

```csharp
batesOptions.Margin = new Margin(20, 0, 0, 20); // top, right, bottom, left
```

### Farklı Bir Biçim Kullanma

Hukuk ekipleri bazen “2024‑A‑001” gibi bir format kullanır. Sadece format dizesini değiştirin:

```csharp
batesOptions.NumberingFormat = "2024-A-{0:D3}";
```

### Şeffaf Arka Planı Ele Alma

`BackgroundColor = Color.Transparent` ayarı, sayının mevcut içeriği gizlemesini önler. Okunabilirliği artırmak için metnin arkasına açık gri bir kutu eklemek isterseniz, `Color.LightGray` ile değiştirin.

## Sık Sorulan Sorular (Cevaplandı)

- **Şifre korumalı PDF'lerde çalışır mı?**  
  Evet—önce belgeyi şifreyle yükleyin (`pdfDocument = new Document("file.pdf", new LoadOptions { Password = "pwd" })`) ardından aynı adımları izleyin.

- **Tek tek tek sayfalara farklı numaralar ekleyebilir miyim?**  
  Evet, iki ayrı `BatesNumberingOptions` ile `AddBatesNumbering` metodunu iki kez çalıştırabilirsiniz; biri tek sayfalar (`StartingPage = 1; EndingPage = pdfDocument.Pages.Count; PageSequence = PageSequence.Odd`), diğeri çift sayfalar için.

- **Aspose.PDF için lisansa ihtiyacım var mı?**  
  Değerlendirme için bir deneme sürümü yeterli, ancak deneme sürümü filigran ekler. Üretim ortamında temiz bir **bates numbering pdf** elde etmek için geçerli bir lisans gerekir.

## Tam Çalışan Örnek (Kopyala‑Yapıştır Hazır)

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Facades;
using System.Drawing;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source PDF
        Document pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");

        // 2️⃣ Set up numbering options (custom page numbers, sequential page numbers)
        BatesNumberingOptions batesOptions = new BatesNumberingOptions
        {
            NumberingFormat = "DOC-{0:D3}",
            StartNumber = 1,
            StartingPage = 1,
            EndingPage = pdfDocument.Pages.Count,
            Font = new Font(FontFamily.Helvetica, 12, FontStyle.Bold),
            ForegroundColor = Color.Black,
            BackgroundColor = Color.Transparent,
            Margin = new Margin(0, 20, 20, 0) // top, right, bottom, left
        };

        // 3️⃣ Apply the numbering (header footer numbering)
        pdfDocument.AddBatesNumbering(batesOptions);

        // 4️⃣ Save the result
        pdfDocument.Save("YOUR_DIRECTORY/BatesNumbered.pdf");

        System.Console.WriteLine("Bates numbering added successfully!");
    }
}
```

Programı çalıştırın, çıktı dosyasını açın ve sayıların kodun Aspose'a söylediği yerde göründüğünü fark edin. Ek döngüler, manuel çizimler yok—sadece dört özlü adımda **add bates numbering** gerçekleştirilir.

## Sonuç

Artık C# ve Aspose.PDF kullanarak herhangi bir PDF'e **add bates numbering** eklemek için sağlam, üretim‑hazır bir yönteme sahipsiniz. Belgeyi yüklemekten **custom page numbers** yapılandırmaya, **sequential page numbers** uygulamaya ve temiz bir **bates numbering pdf** kaydetmeye kadar tüm iş akışı tek bir metod çağrısına sığar.

Sırada ne var? Bu tekniği diğer Aspose özellikleriyle birleştirin—örneğin bir logo damgası eklemek, birden çok PDF birleştirmek ya da yeni eklediğiniz numaralara göre sayfaları çıkarmak. **header footer numbering**i filigranlarla birleştirerek daha kapsamlı çözümler oluşturabilirsiniz.

## Bir Sonraki Öğrenmeniz Gerekenler


Aşağıdaki öğreticiler, bu kılavuzda gösterilen tekniklere dayanarak ilgili konuları derinleştirir. Her kaynak, adım adım açıklamalarla tam çalışan kod örnekleri içerir ve kendi projelerinizde ek API özelliklerini keşfetmenize yardımcı olur.

- [Aspose.PDF .NET: FloatingBox Kullanarak PDF'lere Sayfa Numarası Ekleme](/pdf/english/net/text-operations/aspose-pdf-net-floatingbox-page-numbering/)
- [Aspose.PDF for .NET ile PDF'lere Sayfa Numarası Ekleme ve Özelleştirme | Belge Manipülasyonu Kılavuzu](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [Aspose.PDF for .NET ile PDF'lere Görüntü ve Sayfa Numarası Ekleme: Tam Kılavuz](/pdf/english/net/document-manipulation/enhance-pdfs-images-page-numbers-aspose-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}