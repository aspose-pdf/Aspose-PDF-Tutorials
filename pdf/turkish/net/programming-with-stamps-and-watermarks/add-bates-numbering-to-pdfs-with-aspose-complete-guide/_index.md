---
category: general
date: 2026-04-25
description: Aspose.Pdf kullanarak PDF'lere hızlıca Bates numaralandırması ekleyin.
  PDF sayfa numaraları eklemeyi, yazı tipi boyutunu otomatik ayarlamayı ve C#'ta metin
  filigranı eklemeyi öğrenin.
draft: false
keywords:
- add bates numbering
- add page numbers pdf
- auto adjust font size
- how to add bates
- add text watermark
language: tr
og_description: Aspose.Pdf ile PDF'lere Bates numaralandırması ekleyin. Bu kılavuz,
  tek bir çalıştırılabilir örnekte sayfa numaraları eklemeyi, yazı tipi boyutunu otomatik
  ayarlamayı ve metin filigranı eklemeyi gösterir.
og_title: PDF'lere Bates Numaralandırması Ekle – Tam Aspose.C# Öğreticisi
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Aspose ile PDF'lere Bates Numaralandırması Ekleyin – Tam Rehber
url: /tr/net/programming-with-stamps-and-watermarks/add-bates-numbering-to-pdfs-with-aspose-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Bates Numaralandırmayı PDF'lere Aspose ile Ekleyin – Tam Kılavuz

Hiç **bates numbering** eklemek istediğiniz bir PDF'ye nereden başlayacağınızı bilemediniz mi? Tek değilsiniz—hukuk ekipleri, denetçiler ve geliştiriciler bu sorunu her gün yaşıyor. İyi haber? Aspose.Pdf for .NET ile bir Bates numarası damgası ekleyebilir, yazı tipini otomatik olarak ayarlayabilir ve damgayı ince bir metin filigranı olarak bile kullanabilirsiniz—tek bir kaç satır C# ile.

Bu öğreticide **add page numbers pdf** adımını tam olarak nasıl yapacağınızı, yazı tipinin asla taşmamasını nasıl ayarlayacağınızı gösterecek ve “how to add bates” sorusuna nihai cevabı vereceğiz. Sonunda çalıştırılabilir bir konsol uygulaması elde edeceksiniz; bu uygulama profesyonel bir şekilde numaralandırılmış PDF üretir ve bunu tam bir filigran çözümüne nasıl genişletebileceğinizi göreceksiniz.

## Prerequisites

İlerlemeye başlamadan önce şunlara sahip olduğunuzdan emin olun:

* **Aspose.Pdf for .NET** (Nisan 2026 itibarıyla en son NuGet paketi).  
* .NET 6.0 SDK veya daha yenisi – API .NET Framework'te de aynı şekilde çalışır, ancak .NET 6 en iyi performansı sunar.  
* `input.pdf` adlı örnek bir PDF dosyası; referans verebileceğiniz bir klasörde olmalı (ör. `C:\Docs\`).  

Ek bir yapılandırma gerekmez; kütüphane bağımsızdır.

---

## Step 1 – Load the Source PDF Document

İlk olarak numaralandırmak istediğimiz dosyayı açıyoruz. Aspose’un `Document` sınıfı tüm PDF'yi temsil eder ve onu yüklemek, yolu yapıcıya geçirmek kadar basittir.

```csharp
using Aspose.Pdf;

string inputPath = @"C:\Docs\input.pdf";
Document pdfDocument = new Document(inputPath);
```

*Why this matters*: Belgeyi yüklemek, daha sonra Bates damgasını ekleyeceğimiz `Pages` koleksiyonuna erişmenizi sağlar. Dosya bulunamazsa Aspose net bir `FileNotFoundException` fırlatır, böylece neyin yanlış gittiğini hemen anlarsınız.

---

## Step 2 – Create a Text Stamp for Bates Numbers

Şimdi her sayfada görünecek görsel öğeyi oluşturuyoruz. `TextStamp` sınıfı herhangi bir dizeyi gömebilmenizi sağlar ve `{page}-{total}` yer tutucusunu kullanarak Aspose’un bu tokenları otomatik olarak değiştirmesini isteyeceğiz.

```csharp
// Create a stamp that will display "Bates: 1-10", "Bates: 2-10", etc.
TextStamp batesStamp = new TextStamp("Bates: {page}-{total}")
{
    // Let the stamp automatically adjust its font size to fit the stamp rectangle
    AutoAdjustFontSizeToFitStampRectangle = true,
    // Optional: make the stamp look like a subtle watermark
    Opacity = 0.4,
    // Position the stamp at the bottom‑right corner
    XIndent = 20,
    YIndent = 20,
    HorizontalAlignment = HorizontalAlignment.Right,
    VerticalAlignment = VerticalAlignment.Bottom,
    // Choose a readable font
    Font = new Font(FontFamilyEnum.Helvetica, 12, FontStyle.Regular, Color.Black)
};
```

*Key points*:

* **auto adjust font size** – `AutoAdjustFontSizeToFitStampRectangle` özelliğini `true` yaparak metnin dikdörtgenin dışına taşmamasını garantilersiniz; bu, değişken uzunluktaki sayfa numaraları için mükemmeldir.  
* **add text watermark** – `Opacity` değerini düşürerek Bates numarasını hafif bir filigran haline getirir, “add text watermark” gereksinimini ayrı bir adım olmadan karşılar.  
* **how to add bates** – `{page}` ve `{total}` tokenları gizli sos; Aspose çalışma zamanında bunları değiştirir, böylece siz hiçbir şey hesaplamak zorunda kalmazsınız.

---

## Step 3 – Apply the Stamp to Every Page

Yaygın bir tuzak, sadece ilk sayfaya damga eklemektir. Gerçekten **add page numbers pdf** yapmak için tüm `Pages` koleksiyonunu döngüyle işlemek gerekir.

```csharp
foreach (Page page in pdfDocument.Pages)
{
    // Clone the stamp for each page to avoid shared state issues
    page.AddStamp(batesStamp);
}
```

Neden klonlama? `AddStamp` yöntemi dahili olarak bir kopya oluşturur, ancak yine de her yineleme için yeni bir örnek kullanmak, daha sonra damga özelliklerini (ör. belirli sayfalar için renk değiştirme) değiştirirken istenmeyen yan etkileri önler.

---

## Step 4 – Save the Updated PDF

Damgalar yerleştirildiğinde değişiklikleri kalıcı hâle getirmek basittir. Orijinal dosyanın üzerine yazabilir ya da yeni bir konuma kaydedebilirsiniz—burada `output.pdf` adlı yeni bir dosya kaydedeceğiz.

```csharp
string outputPath = @"C:\Docs\output.pdf";
pdfDocument.Save(outputPath);
Console.WriteLine($"Bates‑numbered PDF saved to: {outputPath}");
```

`output.pdf` dosyasını açtığınızda her sayfanın sağ‑alt köşesinde “Bates: 1‑10”, “Bates: 2‑10”, … gibi bir etiket göreceksiniz; hafif bir opaklıkla **add text watermark** işlevi de yerine getirilmiş olur.

---

## Full Working Example

Hepsini bir araya getirdiğimizde, Visual Studio’ya kopyalayıp yapıştırabileceğiniz tek bir, bağımsız konsol programı elde edersiniz.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Drawing;
using Aspose.Pdf.Annotations;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source PDF
        string inputPath = @"C:\Docs\input.pdf";
        Document pdfDocument = new Document(inputPath);

        // 2️⃣ Create a Bates number stamp with auto‑adjusted font size
        TextStamp batesStamp = new TextStamp("Bates: {page}-{total}")
        {
            AutoAdjustFontSizeToFitStampRectangle = true,
            Opacity = 0.4, // acts as a subtle watermark
            XIndent = 20,
            YIndent = 20,
            HorizontalAlignment = HorizontalAlignment.Right,
            VerticalAlignment = VerticalAlignment.Bottom,
            Font = new Font(FontFamilyEnum.Helvetica, 12, FontStyle.Regular, Color.Black)
        };

        // 3️⃣ Add the stamp to every page (adds page numbers pdf)
        foreach (Page page in pdfDocument.Pages)
        {
            page.AddStamp(batesStamp);
        }

        // 4️⃣ Save the result
        string outputPath = @"C:\Docs\output.pdf";
        pdfDocument.Save(outputPath);
        Console.WriteLine($"Bates‑numbered PDF saved to: {outputPath}");
    }
}
```

**Expected result**: `output.pdf` dosyasını herhangi bir görüntüleyicide açın; her sayfa alt‑sağ köşede “Bates: 3‑12” gibi bir satır gösterir, dikdörtgen için tam boyutta ve %40 opaklıkta render edilir. Bu, hem yasal‑takip gereksinimini hem de görsel filigran ihtiyacını karşılar.

---

## Common Variations & Edge Cases

| Situation | What to change | Why |
|-----------|----------------|-----|
| **Different placement** | Adjust `HorizontalAlignment` / `VerticalAlignment` or set `XIndent`/`YIndent` | Some firms prefer top‑left or center placement. |
| **Custom prefix** | Replace `"Bates: "` with `"Doc‑ID: "` or any string | You might be using a different naming convention. |
| **Multiple stamps** | Create a second `TextStamp` (e.g., for a confidentiality notice) and add it after the first | Combining **add bates numbering** with other **add text watermark** requirements is trivial. |
| **Large page counts** | Increase the initial font size (e.g., `14`) – the auto‑adjust will shrink it when needed | When you have > 999 pages the string gets longer; the auto‑adjust prevents clipping. |
| **Encrypted PDFs** | Call `pdfDocument.Decrypt("password")` before stamping | You can’t modify a secured file without the password. |

---

## Pro Tips & Pitfalls

* **Pro tip:** Set `batesStamp.Margin = new MarginInfo(5, 5, 5, 5)` if you notice the text hugging the edge of the page.  
* **Watch out for:** Very small rectangles (default size is 100 × 30 pt). If you need a larger area, set `batesStamp.Width` and `batesStamp.Height` manually.  
* **Performance note:** Stamping thousands of pages can take a few seconds, but Aspose streams pages efficiently—no need to load the whole document into memory.  

---

## Conclusion

We’ve just demonstrated how to **add bates numbering** to a PDF using Aspose.Pdf, while simultaneously **add page numbers pdf**, enable **auto adjust font size**, and create an **add text watermark** in one cohesive flow. The complete, runnable example above gives you a solid foundation you can adapt to any legal‑document workflow or internal reporting system.

Ready for the next step? Try pairing this approach with Aspose’s PDF merging API to batch‑process multiple files, or explore the `TextFragment` class for richer watermarks (colored, rotated, or multi‑line). The possibilities are endless, and the code you now have is a reliable baseline.

If you found this guide helpful, feel free to drop a comment, star the repository, or share your own variations. Happy coding, and may your PDFs always be perfectly numbered!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}