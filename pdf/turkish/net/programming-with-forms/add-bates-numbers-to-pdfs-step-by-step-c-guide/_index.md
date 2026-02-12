---
category: general
date: 2026-02-12
description: PDF dosyalarına hızlıca Bates numaraları ekleyin. Aspose.PDF kullanarak
  metin alanı PDF eklemeyi, form alanı PDF eklemeyi ve sayfa numaraları PDF eklemeyi
  öğrenin.
draft: false
keywords:
- add bates numbers
- add text field pdf
- add form field pdf
- add page numbers pdf
- how to add bates
language: tr
og_description: C#'ta PDF belgelerine Bates numaraları ekleyin. Bu kılavuz, Aspose.PDF
  ile PDF'ye metin alanı ekleme, form alanı ekleme ve sayfa numaraları ekleme yöntemlerini
  gösterir.
og_title: PDF'lere Bates Numaraları Ekle – Tam C# Öğreticisi
tags:
- PDF
- C#
- Aspose.PDF
title: PDF'lere Bates Numaraları Ekleyin – Adım Adım C# Rehberi
url: /tr/net/programming-with-forms/add-bates-numbers-to-pdfs-step-by-step-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PDF'lere Bates Numaraları Ekle – Tam C# Rehberi

Bir yığın yasal PDF'e **bates numaraları eklemeniz** gerektiğinde nereden başlayacağınızı bilemediniz mi? Yalnız değilsiniz. Birçok hukuk bürosu ve e‑keşif projesinde, her sayfayı benzersiz bir tanımlayıcıyla damgalamak günlük bir görevdir ve bunu manuel olarak yapmak bir kabustur.  

İyi haber? Birkaç C# satırı ve Aspose.PDF ile tüm süreci otomatikleştirebilirsiniz. Bu öğreticide **bates numaraları eklemenin** nasıl yapılacağını adım adım gösterecek, her sayfaya bir metin alanı ekleyecek ve temiz, aranabilir bir PDF olarak kaydedeceğiz—hiç ter dökmeyecek şekilde.  

> **Ne elde edeceksiniz:** tamamen çalıştırılabilir bir kod örneği, her satırın neden önemli olduğuna dair açıklamalar, uç durumlar için ipuçları ve çıktınızı doğrulamak için hızlı bir kontrol listesi.  

İlgili görevlerden de bahsedeceğiz: **add text field pdf**, **add form field pdf**, ve **add page numbers pdf**, böylece her türlü belge‑otomasyon zorluğu için hazır bir araç kutunuz olacak.

---

## Önkoşullar

- .NET 6.0 veya üzeri (kod .NET Framework 4.6+ ile de çalışır)  
- Visual Studio 2022 (veya tercih ettiğiniz herhangi bir IDE)  
- Geçerli bir Aspose.PDF for .NET lisansı (ücretsiz deneme sürümü test için çalışır)  
- `source.pdf` adlı bir kaynak PDF, başvurabileceğiniz bir klasöre yerleştirilmiş  

Bu maddelerden herhangi biri size yabancı geliyorsa, ilerlemeden önce eksik parçayı kurun. Aşağıdaki adımlar, Aspose.PDF NuGet paketini zaten eklediğinizi varsayar:

```bash
dotnet add package Aspose.Pdf
```

---

## Aspose.PDF ile bir PDF'e Bates Numaraları Nasıl Eklenir

Aşağıda, tamamen kopyala‑yapıştır hazır program bulunmaktadır. PDF'i yükler, her sayfada bir **text box field** oluşturur, biçimlendirilmiş bir Bates numarası yazar ve sonunda değiştirilmiş dosyayı kaydeder.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Forms;

class Program
{
    static void Main()
    {
        // 👉 Step 1: Load the source PDF document
        using (var pdfDocument = new Document(@"YOUR_DIRECTORY\source.pdf"))
        {
            // 👉 Step 2: Add a Bates number text field to each page
            for (int pageNumber = 1; pageNumber <= pdfDocument.Pages.Count; pageNumber++)
            {
                // Define the rectangle where the field will appear (10,10) = lower‑left corner
                var fieldRect = new Rectangle(10, 10, 150, 30);

                // Create the TextBoxField – this is the “add text field pdf” part
                var batesField = new TextBoxField(pdfDocument.Pages[pageNumber], fieldRect)
                {
                    // Format the number: BATES-00001, BATES-00002, …
                    Value = $"BATES-{pageNumber:D5}"
                };

                // Register the field with the form collection – “add form field pdf”
                pdfDocument.Form.Add(batesField, $"Bates_{pageNumber}", pageNumber);
            }

            // 👉 Step 3: Save the modified PDF with Bates numbers
            pdfDocument.Save(@"YOUR_DIRECTORY\bates.pdf");
        }

        Console.WriteLine("✅ Bates numbers added successfully!");
    }
}
```

### Neden Bu Çalışır

- **`Document`** giriş noktasıdır; tüm PDF dosyasını temsil eder.  
- **`Rectangle`** alanın sayfada nerede konumlandığını tanımlar. Sayılar puan cinsindendir (1 pt ≈ 1/72 in). Sayıyı farklı bir köşeye yerleştirmeniz gerekiyorsa koordinatları ayarlayın.  
- **`TextBoxField`** herhangi bir dizeyi tutabilen bir *form alanıdır*. `Value` atayarak özelleştirilmiş bir ön ekle **add page numbers pdf** işlemini etkili bir şekilde gerçekleştiririz.  
- **`pdfDocument.Form.Add`** alanı PDF'in AcroForm'una kaydeder, böylece Adobe Acrobat gibi görüntüleyicilerde görünür.  

Eğer görünümü (yazı tipi, renk, boyut) değiştirmeniz gerekirse `TextBoxField` özelliklerini ayarlayabilirsiniz—`DefaultAppearance` ve `Border` için Aspose belgelerine bakın.

---

## Her PDF sayfasına bir metin alanı ekleme ("add text field pdf" adımı)

Bazen sadece görünür bir etiket istersiniz, etkileşimli bir form alanı değil. Bu durumda `TextBoxField` yerine `TextFragment` kullanabilir ve doğrudan sayfanın `Paragraphs` koleksiyonuna ekleyebilirsiniz. İşte hızlı bir alternatif:

```csharp
var fragment = new TextFragment($"BATES-{pageNumber:D5}")
{
    // Position the text using a TextState (font, size, color)
    TextState = new TextState
    {
        Font = FontRepository.FindFont("Arial"),
        FontSize = 12,
        ForegroundColor = Color.Black
    }
};

// Set the fragment’s rectangle (same coordinates as before)
fragment.Position = new Position(10, 10);
pdfDocument.Pages[pageNumber].Paragraphs.Add(fragment);
```

**add text field pdf** yaklaşımı, son belgenin yalnızca okunur olacağı durumlarda faydalıdır, **add form field pdf** yöntemi ise numaraların daha sonra düzenlenebilir kalmasını sağlar.

---

## PDF'i Bates Numaralarıyla Kaydetme ("add page numbers pdf" anı)

Döngü tamamlandıktan sonra `pdfDocument.Save` çağrısı her şeyi diske yazar. Orijinal dosyayı korumanız gerekiyorsa, çıktı yolunu değiştirin veya `pdfDocument.Save` aşırı yüklemelerini kullanarak sonucu doğrudan bir web API yanıtına akıtın.

```csharp
// Example: stream to HTTP response (ASP.NET Core)
Response.ContentType = "application/pdf";
pdfDocument.Save(Response.Body);
```

İşte bu kısım güzel—geçici dosyalar yok, ekstra kütüphane yok, sadece Aspose ağır işi hallediyor.

---

## Beklenen Sonuç ve Hızlı Doğrulama

Herhangi bir PDF görüntüleyicide `bates.pdf` dosyasını açın. Her sayfanın sol‑alt köşesinde şu metni içeren küçük bir kutu görmelisiniz:

```
BATES-00001
BATES-00002
…
```

Belge özelliklerini incelerseniz, `Bates_1`, `Bates_2` vb. adlarda alanlar içeren bir AcroForm olduğunu göreceksiniz. Bu, **add form field pdf** adımının başarılı olduğunu doğrular.

---

## Yaygın Tuzaklar ve Profesyonel İpuçları

| Sorun | Neden Oluşur | Çözüm |
|-------|----------------|-----|
| Numaralar ortalanmamış görünüyor | Rectangle koordinatları sayfanın sol‑alt köşesine göre görecelidir. | Y‑değerini (`pageHeight - marginTop`) ters çevirin veya üst‑kenar boşluğu konumlandırması için `page.PageInfo.Height` kullanın. |
| Alanlar Adobe Reader'da görünmez | Varsayılan kenarlık “Hayır” olarak ayarlanmıştır. | `batesField.Border = new Border { Width = 0.5f, Color = Color.Black };` ayarlayın |
| Büyük PDF'ler bellek baskısına neden olur | `using` döngü bitene kadar belgeyi serbest bırakmaz. | Sayfaları parçalar halinde işleyin veya akışı etkinleştiren `SaveOptions` ile `pdfDocument.Save` kullanın. |
| Lisans uygulanmadı | Aspose ilk sayfada bir filigran ekler. | Lisansınızı erken kaydedin: `License lic = new License(); lic.SetLicense("Aspose.Pdf.lic");` |

---

## Çözümü Genişletmek

- **Özel ön ekler:** `"BATES-"` yerine herhangi bir dize (`"DOC-"`, `"CASE-"`, …) koyun.  
- **Sıfır doldurma uzunluğu:** Üç haneli için `{pageNumber:D5}` yerine `{pageNumber:D3}` kullanın.  
- **Dinamik konumlandırma:** Alanı sağ tarafta konumlandırmak için `pdfDocument.Pages[pageNumber].PageInfo.Width` kullanın.  
- **Koşullu numaralandırma:** Boş sayfaları `pdfDocument.Pages[pageNumber].IsBlank` kontrol ederek atlayın.  

Bu tüm varyasyonlar, **add bates numbers**, **add text field pdf**, ve **add form field pdf** temel desenini bozmadan korur.

---

## Tam Çalışan Örnek (Hepsi Bir Arada)

Aşağıda, yukarıdaki ipuçlarını içeren son, çalıştırmaya hazır program bulunmaktadır. Yeni bir console uygulamasına kopyalayıp F5 tuşuna basın.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Forms;
using Aspose.Pdf.Text;
using Aspose.Pdf.Drawing;

class AddBatesNumbers
{
    static void Main()
    {
        // Register your license here (optional for trial)
        // var license = new License();
        // license.SetLicense("Aspose.Pdf.lic");

        string inputPath = @"YOUR_DIRECTORY\source.pdf";
        string outputPath = @"YOUR_DIRECTORY\bates.pdf";

        using (var pdfDocument = new Document(inputPath))
        {
            int totalPages = pdfDocument.Pages.Count;

            for (int i = 1; i <= totalPages; i++)
            {
                // Position the field 10 pts from left and 10 pts from bottom
                var rect = new Rectangle(10, 10, 150, 30);

                var batesField = new TextBoxField(pdfDocument.Pages[i], rect)
                {
                    Value = $"BATES-{i:D5}"
                };

                // Optional: make the field look nicer
                batesField.Border = new Border
                {
                    Width = 0.5f,
                    Color = Color.Gray
                };
                batesField.DefaultAppearance = new DefaultAppearance
                {
                    Font = FontRepository.FindFont("Arial"),
                    FontSize = 10,
                    ForegroundColor = Color.DarkBlue
                };

                pdfDocument.Form.Add(batesField, $"Bates_{i}", i);
            }

            pdfDocument.Save(outputPath);
        }

        Console.WriteLine($"✅ Finished! Bates numbers saved to: {outputPath}");
    }
}
```

Çalıştırın, sonucu açın ve her sayfada profesyonel bir tanımlayıcı göreceksiniz—tam da bir dava destek uzmanının beklediği gibi.

---

## Sonuç

Biz sadece C# ve Aspose.PDF kullanarak herhangi bir PDF'e **bates numaraları eklemenin** nasıl yapılacağını gösterdik. Her sayfada bir **text box field** oluşturarak aynı anda **add text field pdf**, **add form field pdf**, ve **add page numbers pdf** işlemlerini tek bir geçişte gerçekleştirdik. Yaklaşım hızlı, ölçeklenebilir ve özel ön ekler, farklı düzenler veya koşullu mantık için kolayca ayarlanabilir.  

Bir sonraki zorluğa hazır mısınız? Orijinal dava dosyasına bağlanan bir QR kodu eklemeyi deneyin ya da tüm Bates numaralarını ve ilgili sayfa başlıklarını listeleyen ayrı bir indeks sayfası oluşturun. Aynı API, PDF'leri birleştirmenize, sayfaları çıkarmanıza ve hatta hassas verileri gizlemenize olanak tanır—dolayısıyla sınır yok.  

Bir sorunla karşılaşırsanız, aşağıya yorum bırakın ya da daha derinlemesine bilgi için Aspose'un resmi belgelerine bakın. Kodlamanız keyifli olsun ve PDF'leriniz her zaman mükemmel numaralandırılmış olsun!  

---  

![add bates numbers screenshot](https://example.com/images/add-bates-numbers.png "add bates numbers example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}