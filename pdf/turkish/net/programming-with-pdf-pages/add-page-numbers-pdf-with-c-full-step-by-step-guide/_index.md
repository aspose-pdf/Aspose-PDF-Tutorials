---
category: general
date: 2026-01-02
description: Aspose.Pdf kullanarak C#'ta PDF sayfa numaralarını hızlıca ekleyin. Bates
  numaralandırma, altbilgi metni, özel filigran eklemeyi ve tek bir scriptte PDF sayfaları
  arasında döngü yapmayı öğrenin.
draft: false
keywords:
- add page numbers pdf
- add bates numbering
- add footer text
- add custom watermark
- loop through pdf pages
language: tr
og_description: Aspose.Pdf ile PDF sayfa numaralarını anında ekleyin. Bu kılavuz ayrıca
  Bates numaralandırması, alt bilgi metni, özel filigran ve PDF sayfalarında döngü
  oluşturmayı da kapsar.
og_title: C# ile PDF'e sayfa numaraları ekleme – Tam Programlama Öğreticisi
tags:
- C#
- Aspose.Pdf
- PDF manipulation
title: C# ile PDF'ye Sayfa Numaraları Ekle – Tam Adım Adım Kılavuz
url: /tr/net/programming-with-pdf-pages/add-page-numbers-pdf-with-c-full-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# ile PDF sayfa numarası ekleme – Tam Programlama Öğreticisi

Hiç **add page numbers pdf** dosyalarına sayfa numarası eklemeniz gerektiğinde nereden başlayacağınızı bilemediniz mi? Tek başınıza değilsiniz—geliştiriciler sürekli olarak bir PDF’in her sayfasına numara, alt bilgi ya da bir Bates‑stili tanımlayıcı eklemenin nasıl yapılacağını soruyor.  

Bu öğreticide, **pdf sayfaları arasında döngü** kuran, bir sayfa‑numarası alt bilgisi damgalayan ve (isteğe bağlı olarak) özel bir filigran ekleyen hazır bir C# örneği göreceksiniz. Damgayı bir Bates numarasına dönüştürmeyi de göstereceğiz; bu, yasal ya da adli belgeler için “bates numaralandırması ekle” demenin şık bir yolu. Sonunda, tüm bu görevleri zahmetsizce yerine getiren tek bir yeniden kullanılabilir metoda sahip olacaksınız.

## Add page numbers pdf – Genel Bakış

Koda girmeden önce, “add page numbers pdf” ifadesinin Aspose.Pdf dünyasında ne anlama geldiğini netleştirelim. Kütüphane, bir sayfaya yerleştirdiğiniz herhangi bir metni **TextStamp** olarak kabul eder. `{page}` yer tutucusuyla bir damga oluşturup bunu her sayfaya uygularsanız, otomatik olarak artan bir numaralandırma elde edersiniz. Aynı damga ek **footer text** (alt bilgi metni) de taşıyabilir, böylece “Confidential” gibi bir ifade ya da dava‑özel bir tanımlayıcı ekleyebilirsiniz.

> **Neden PDF içerik akışını düzenlemek yerine damga kullanmalı?**  
> Damgalar, sayfa kenar boşluklarını, döndürmeyi ve mevcut grafikleri dikkate alan yüksek‑seviye nesnelerdir. Ayrıca bakım açısından çok daha kolaydır—sadece birkaç özelliği değiştirin ve betiği yeniden çalıştırın.

## PDF sayfaları arasında döngü kurarak damgaları uygulama

İlk pratik adım, kaynak PDF’i açıp sayfaları üzerinde döngü kurmaktır. Bu, çoğu Aspose örneğinde kullanılan klasik **loop through pdf pages** desenidir.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Paths – change these to match your environment
string sourcePdfPath = @"C:\Docs\input.pdf";
string outputPdfPath = @"C:\Docs\PageNumbered.pdf";

using (var pdfDocument = new Document(sourcePdfPath))
{
    // The loop – every Page object lives in pdfDocument.Pages
    foreach (Page page in pdfDocument.Pages)
    {
        // We'll attach a stamp later (see next section)
    }

    // Save the modified document
    pdfDocument.Save(outputPdfPath);
}
```

> **İpucu:** PDF’iniz yüzlerce sayfa içeriyorsa, bellek kullanımını düşük tutmak için işleme partiler halinde yapmayı düşünün. Aspose.Pdf sayfaları tembel (lazy) olarak akıtır, bu yüzden döngü zaten oldukça verimlidir.

## Bates numaralandırması ve alt bilgi metni ekleme

Şimdi her sayfayı gezebildiğimize göre, hem sayfa numarasını hem de isteğe bağlı alt bilgi metnini taşıyan **yeniden kullanılabilir TextStamp** oluşturalım. `{page}` yer tutucusu, mevcut sayfa indeksine otomatik olarak dönüşür.

```csharp
// Create a stamp that will be reused for every page
var batesStamp = new TextStamp("Bates-{page} – Confidential")
{
    // Position the stamp 20 points from the left and bottom edges
    XIndent = 20,
    YIndent = 20,
    // Align left‑bottom so it behaves like a traditional footer
    HorizontalAlignment = HorizontalAlignment.Left,
    VerticalAlignment   = VerticalAlignment.Bottom,
    // Font styling – Times New Roman, 10pt, bold, gray
    Font = new Font(FontFamily.TimesRoman, 10, FontStyle.Bold),
    TextState = { ForegroundColor = Color.Gray }
};

// Attach the stamp to every page
foreach (Page page in pdfDocument.Pages)
    page.AddStamp(batesStamp);
```

### Neden bu şekilde çalışıyor

* **`Bates-{page}`** – Aspose, `{page}` ifadesini gerçek sayfa numarasıyla değiştirir ve size otomatik bir Bates numarası sağlar.
* **`Confidential`** – Bu, **add footer text** kısmıdır. İstediğiniz herhangi bir dizeyle değiştirebilir, hatta bir veritabanından veri çekebilirsiniz.
* **Stil** – `TextState` kullanarak renk, opaklık ve hatta döndürmeyi PDF’in iç akışına dokunmadan ayarlayabilirsiniz.

Sadece düz sayılar istiyorsanız, “Bates‑” önekini ve ekstra metni kaldırın:

```csharp
var simpleStamp = new TextStamp("{page}")
{
    XIndent = 20,
    YIndent = 20,
    HorizontalAlignment = HorizontalAlignment.Center,
    VerticalAlignment   = VerticalAlignment.Bottom,
    Font = new Font(FontFamily.Helvetica, 12, FontStyle.Regular),
    TextState = { ForegroundColor = Color.Black }
};
```

## Özel bir filigran ekleme (isteğe bağlı)

Bazen sadece bir alt bilgi yeterli olmaz—yarı‑saydam bir logo ya da tüm sayfa üzerine bir “DRAFT” katmanı eklemeniz gerekir. İşte **add custom watermark** burada devreye girer. Aynı `TextStamp` sınıfı yeniden kullanılabilir; sadece hizalama ve opaklığını değiştirin.

```csharp
var watermark = new TextStamp("DRAFT")
{
    // Center it both horizontally and vertically
    HorizontalAlignment = HorizontalAlignment.Center,
    VerticalAlignment   = VerticalAlignment.Center,
    // Make it big and light
    Font = new Font(FontFamily.Helvetica, 72, FontStyle.Bold),
    TextState = { ForegroundColor = Color.Red, FontSize = 72, FontStyle = FontStyle.Bold, 
                  Transparency = 0.5f }   // 50% transparent
};

// Apply the watermark on top of the page‑number stamp
foreach (Page page in pdfDocument.Pages)
{
    page.AddStamp(watermark);   // watermark on top
    page.AddStamp(batesStamp);  // then the footer
}
```

> **Not:** Sıra önemlidir. Filigranı önce eklemek, sayfa numaralarının yarı‑saydam metnin üstünde okunabilir kalmasını sağlar.

## PDF’i kaydetme ve sonuçları doğrulama

Damgalama işlemi tamamlandıktan sonra son adım, değişiklikleri diske yazmaktır. Daha önce eklediğimiz `Save` çağrısı işi halleder, ancak yeni dosyayı açıp kaç sayfanın işlendiğini yazdıran kısa bir doğrulama kodu ekleyelim.

```csharp
pdfDocument.Save(outputPdfPath);

// Quick verification
using (var resultDoc = new Document(outputPdfPath))
{
    Console.WriteLine($"✅ Successfully added page numbers to {resultDoc.Pages.Count} pages.");
}
```

Programı tam olarak çalıştırdığınızda, her sayfanın sonunda **“Bates‑3 – Confidential”** (veya basit damga kullandıysanız sadece “3”) gibi bir ifade göreceksiniz; ayrıca filigranı etkinleştirdiyseniz, ortada hafif bir “DRAFT” görünecektir.

### Beklenen çıktı

| Sayfa | Alt Bilgi (örnek) |
|------|-------------------|
| 1    | Bates‑1 – Confidential |
| 2    | Bates‑2 – Confidential |
| …    | … |
| N    | Bates‑N – Confidential |

Dosyayı bir görüntüleyicide açtığınızda, numaralar sol ve alt kenar boşluklarından 20 pt uzakta, tipik yasal‑belge konvansiyonlarına uygun şekilde yer alacaktır.

## Tam çalışan örnek (kopyala‑yapıştır hazır)

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

string sourcePdfPath = @"C:\Docs\input.pdf";
string outputPdfPath = @"C:\Docs\PageNumbered.pdf";

using (var pdfDocument = new Document(sourcePdfPath))
{
    // ---------- Create the page‑number/footer stamp ----------
    var batesStamp = new TextStamp("Bates-{page} – Confidential")
    {
        XIndent = 20,
        YIndent = 20,
        HorizontalAlignment = HorizontalAlignment.Left,
        VerticalAlignment   = VerticalAlignment.Bottom,
        Font = new Font(FontFamily.TimesRoman, 10, FontStyle.Bold),
        TextState = { ForegroundColor = Color.Gray }
    };

    // ---------- Optional watermark ----------
    var watermark = new TextStamp("DRAFT")
    {
        HorizontalAlignment = HorizontalAlignment.Center,
        VerticalAlignment   = VerticalAlignment.Center,
        Font = new Font(FontFamily.Helvetica, 72, FontStyle.Bold),
        TextState = { ForegroundColor = Color.Red, Transparency = 0.5f }
    };

    // ---------- Apply stamps to every page ----------
    foreach (Page page in pdfDocument.Pages)
    {
        page.AddStamp(watermark);   // comment out if you don't need a watermark
        page.AddStamp(batesStamp);
    }

    // ---------- Save and verify ----------
    pdfDocument.Save(outputPdfPath);
    Console.WriteLine($"✅ Added page numbers and watermark to {pdfDocument.Pages.Count} pages.");
}
```

Bunu `AddPageNumbers.cs` olarak kaydedin, Aspose.Pdf NuGet paketini geri yükleyin (`Install-Package Aspose.Pdf`), ve çalıştırın. **add page numbers pdf** dosyası elde edeceksiniz; aynı zamanda **add bates numbering**, **add footer text**, **add custom watermark** ve klasik **loop through pdf pages** desenini tek bir düzenli betikte gösterir.

![add page numbers pdf örneği](https://example.com/images/add-page-numbers-pdf.png "Numaralı PDF sayfalarını ve filigranı gösteren ekran görüntüsü")

## Sonuç

Aspose.Pdf kullanarak C# ile **add page numbers pdf** dosyaları eklemek için ihtiyacınız olan her şeyi kapsadık. Her sayfada döngü kurmaktan Bates numaraları damgalamaya, özel alt bilgi metni eklemeye ve yarı‑saydam bir filigran katmanı oluşturmaya kadar, kod mevcut projelere kolayca entegre edilebilecek kadar kompakt.  

Sonraki adımda, alt bilgi metnini bir veritabanından çekmek, bölüm‑bazlı farklı fontlar uygulamak ya da tüm Bates numaralarını listeleyen ayrı bir indeks PDF’i oluşturmak gibi daha ileri senaryoları keşfedebilirsiniz. Bu uzantıların tümü, burada gösterdiğimiz temel fikirler üzerine inşa edildiği için, gereksinimleriniz büyüdükçe çözümü rahatlıkla genişletebilirsiniz.  

Deneyin, stil ayarlarını değiştirin ve yorumlarda nasıl çalıştığını bize bildirin. Mutlu kodlamalar!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}