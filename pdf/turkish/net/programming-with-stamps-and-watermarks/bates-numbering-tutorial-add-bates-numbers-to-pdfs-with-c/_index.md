---
category: general
date: 2026-02-25
description: Bates numaralandırma öğreticisi – PDF'e sayfa numarası eklemeyi ve Aspose.Pdf
  kullanarak C#'ta özel Bates numaralandırması uygulamayı öğrenin. Tam kodlu adım
  adım rehber.
draft: false
keywords:
- bates numbering tutorial
- add page numbers pdf
- how to add bates
- add bates numbering
language: tr
og_description: Bates numaralandırma öğreticisi, C#'ta PDF sayfa numaraları ve özel
  Bates numaralandırması eklemeyi gösterir. Tam kod, açıklamalar ve ipuçları.
og_title: Bates numaralandırma öğreticisi – PDF'lere C# ile Bates numaraları ekleyin
tags:
- PDF
- C#
- Aspose.Pdf
title: 'Bates numaralandırma öğreticisi: C# ile PDF''lere Bates numaraları ekleyin'
url: /tr/net/programming-with-stamps-and-watermarks/bates-numbering-tutorial-add-bates-numbers-to-pdfs-with-c/
---

codes at bottom.

Let's craft final output.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Bates numaralandırma öğreticisi – PDF'lere C# ile Bates Numaraları Ekleme

PDF'lere sayfa numarası eklerken aynı zamanda yasal‑stil bir Bates numarası gömmeyi hiç merak ettiniz mi? Tek başınıza değilsiniz. Bu **bates numbering tutorial**'da, bir PDF'in her sayfasını özel bir önek, sıfır doldurma ve kesin konumlandırma ile damgalamak için bilmeniz gereken her şeyi—Aspose.Pdf for .NET kullanarak—adım adım anlatacağız.

İyi haber? Temel kavramları kavradığınızda oldukça basit. Bu rehberin sonunda, *input.pdf* dosyasını alıp her sayfada “ABC‑01000” tarzı şık bir etiketle *bates_out.pdf* olarak çıkaran çalıştırılabilir bir programınız olacak. Hadi başlayalım.

## Gereksinimler

- **Aspose.Pdf for .NET** (sürüm 23.10 veya daha yeni). Kütüphane ticari, ancak ücretsiz deneme sürümü öğrenmek için yeterli.
- .NET 6+ SDK (herhangi bir güncel sürüm yeterli).
- Temel bir C# geliştirme ortamı—Visual Studio, VS Code veya Rider.
- Deney yapabileceğiniz bir giriş PDF'i (herhangi çok sayfalı belge etkisini gösterecektir).

Aspose.Pdf dışındaki ek NuGet paketlerine gerek yoktur ve kod Windows, Linux veya macOS üzerinde değişiklik yapmadan çalışır.

## Adım 1: Kaynak PDF Belgesini Yükleyin (bates numbering tutorial – initialization)

İlk olarak, değiştirmek istediğimiz PDF'i temsil eden bir `Document` nesnesi oluştururuz. Bunu, üzerine çizebileceğiniz boş bir tuval yüklemek gibi düşünün.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Annotations;

// Load the source PDF – replace the path with your actual file location
Document pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");

// Quick sanity check – make sure the document actually has pages
if (pdfDocument.Pages.Count == 0)
{
    throw new InvalidOperationException("The PDF you provided contains no pages.");
}
```

**Neden önemli:** Dosyayı yüklemeden anotasyon eklemek mümkün değildir. Bu kontrol, var olmayan bir sayfa koleksiyonuna öğe eklemeye çalıştığınızda sessiz bir hatayı önler.

## Adım 2: Bates Numara Artefaktını Tanımlayın (how to add bates)

Bir *BatesNumberingArtifact*, Aspose'a tanımlayıcıyı nerede ve nasıl çizeceğini söyler. Önek, başlangıç numarası, sıfır doldurma, yazı tipi boyutu ve kesin X/Y koordinatlarını kontrol edebilirsiniz.

```csharp
// Configure the Bates numbering artifact
BatesNumberingArtifact batesArtifact = new BatesNumberingArtifact
{
    Prefix = "ABC",          // Text that appears before the number
    Start = 1000,            // First number in the sequence
    LeadingZeros = 5,        // Pad the number with zeros (e.g., 01000)
    FontSize = 9,            // Small enough to sit in the margin
    Position = new Position   // Position measured from the lower‑left corner
    {
        X = 50,               // Horizontal offset (points)
        Y = 30                // Vertical offset (points)
    }
};
```

**Neden önemli:** `LeadingZeros` özelliği, her etiketin aynı uzunlukta olmasını sağlar; bu, hizalamanın kritik olduğu yasal belgeler için hayati önemdedir. `X` ve `Y` değerlerini değiştirerek damgayı sağ‑üst, sol‑alt veya iş akışınızın istediği herhangi bir konuma taşıyabilirsiniz.

## Adım 3: Artefakti Her Sayfaya Ekleyin (add page numbers pdf)

Şimdi her sayfayı döngüye alıp aynı artefakti ekliyoruz. Bu, *add page numbers pdf* gereksiniminin karşılandığı yerdir—her sayfa otomatik olarak kendi sıralı etiketini alır.

```csharp
// Iterate over each page and add the Bates artifact
foreach (Page page in pdfDocument.Pages)
{
    // The artifact is added to the page's Artifacts collection.
    // Aspose will handle the incrementing of the number for us.
    page.Artifacts.Add(batesArtifact);
}
```

**Neden önemli:** Artefakti `Artifacts` koleksiyonuna eklemek, metni manuel olarak çizmeye kıyasla Aspose'ın numaralandırma mantığını, sıfır doldurmayı ve renderlamayı yönetmesini sağlar. Bu, hataları azaltır ve kodu özlü tutar.

## Adım 4: Değiştirilen PDF'i Kaydedin (add bates numbering)

Son olarak değişiklikleri yeni bir dosyaya kalıcı hâle getiriyoruz. Orijinali bozulmasın diye farklı bir dosya adıyla kaydetmek iyi bir alışkanlıktır.

```csharp
// Save the PDF with Bates numbers applied
pdfDocument.Save("YOUR_DIRECTORY/bates_out.pdf");

// Optional: let the user know we succeeded
Console.WriteLine("Bates numbering applied successfully! Output saved to bates_out.pdf");
```

**Neden önemli:** `Save` yöntemi, artefaktları sayfa içerik akışının bir parçası olarak gömerek tüm PDF'i yazar. Ortaya çıkan dosya herhangi bir PDF görüntüleyicide açılabilir ve Bates numaralarını tam olarak belirtilen şekilde gösterir.

## Tam Çalışan Örnek (Tüm Adımlar Birleştirildi)

Aşağıda, tamamen hazır‑çalıştırılabilir program yer alıyor. Bir konsol uygulaması projesine kopyalayıp yapıştırın, yer tutucu yolları değiştirin ve **F5** tuşuna basın.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the source PDF
            Document pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");
            if (pdfDocument.Pages.Count == 0)
                throw new InvalidOperationException("The PDF you provided contains no pages.");

            // 2️⃣ Configure the Bates numbering artifact
            BatesNumberingArtifact batesArtifact = new BatesNumberingArtifact
            {
                Prefix = "ABC",
                Start = 1000,
                LeadingZeros = 5,
                FontSize = 9,
                Position = new Position { X = 50, Y = 30 }
            };

            // 3️⃣ Attach the artifact to every page
            foreach (Page page in pdfDocument.Pages)
            {
                page.Artifacts.Add(batesArtifact);
            }

            // 4️⃣ Save the modified PDF
            pdfDocument.Save("YOUR_DIRECTORY/bates_out.pdf");
            Console.WriteLine("Bates numbering applied successfully! Output saved to bates_out.pdf");
        }
    }
}
```

### Beklenen Sonuç

*bates_out.pdf* dosyasını Adobe Reader, Foxit veya herhangi bir görüntüleyicide açın. İlk sayfada **ABC‑01000**, ikinci sayfada **ABC‑01001** gibi bir etiket görmelisiniz; etiket sol kenardan 50 pt, alttan 30 pt uzaklıkta konumlandırılmıştır. Sıfır doldurma sayesinde sayılar sağa hizalanır, bu da belgeye temiz ve profesyonel bir görünüm kazandırır.

## Yaygın Varyasyonlar ve Kenar Durumları

| Senaryo | Nasıl Ayarlanır |
|----------|---------------|
| **Farklı önek** | Artefakt tanımında `Prefix = "XYZ"` değiştirin. |
| **Özel bir sayıdan başlat** | `Start = 5000` (veya istediğiniz herhangi bir tamsayı) ayarlayın. |
| **Numarayı sağ‑üst köşeye yerleştir** | `Position = new Position { X = pdfDocument.PageInfo.Width - 50, Y = pdfDocument.PageInfo.Height - 30 }` kullanın. |
| **Daha büyük belgeler için yazı tipi boyutunu değiştir** | `FontSize = 12` (veya istediğiniz boyut) olarak değiştirin. |
| **Arka plan dikdörtgeni ekle** | `RectangleArtifact` oluşturup `BatesNumberingArtifact`'tan önce ekleyin. |
| **Belirli sayfaları atla** | `foreach` döngüsü içinde `if (page.Number % 2 == 0) continue;` ekleyerek çift sayfaları atlayın. |

**Pro ipucu:** Öncelikle kısa bir PDF ile test edin. Pozisyonlamayı doğrulamak, 200 sayfalık bir dava dosyasında scripti çalıştırmadan önce zaman kazandırır.

## Sık Sorulan Sorular

- **Şifreli PDF'lerle çalışır mı?**  
  Aspose.Pdf, `Document(string, string)` ile şifreyi sağlayarak parola korumalı dosyaları açabilir. Bates artefakti şifre çözme sonrası da uygulanır.

- **Hem Bates numarası hem de normal sayfa numarası ekleyebilir miyim?**  
  Evet. `BatesNumberingArtifact` ile birlikte bir `PageNumberArtifact` ekleyin. Her artefakt kendi sayacını tutar.

- **PDF'im farklı sayfa boyutlarına sahip ise ne olur?**  
  `Position` değerleri mutlak puan cinsindendir. Karışık boyutlu belgeler için döngü içinde `page.PageInfo.Width` ve `page.PageInfo.Height` kullanarak konumu sayfaya göre hesaplayın.

## Sonraki Adımlar ve İlgili Konular

**bates numbering tutorial**'ı öğrendikten sonra şunları keşfedebilirsiniz:

- **Filigran ekleme** – `TextArtifact` ile benzer artefakt yaklaşımı.
- **Birden fazla PDF birleştirme** – `Document.AppendDocument` kullanın.
- **Arama indekslemesi için metin çıkarma** – `TextAbsorber` sınıfı.
- **Toplu işleme otomasyonu** – bir klasördeki PDF'ler üzerinde döngü kurup aynı artefakti uygulayın.

Tüm bu konular, az önce öğrendiğiniz kavramların üzerine inşa edilmiştir; böylece PDF otomasyon araç setinizi genişletmeye hazırsınız.

---

*Kodlamanın tadını çıkarın! Herhangi bir sorunla karşılaşırsanız veya daha fazla özelleştirme fikriniz olursa, aşağıya yorum bırakın. PDF manipülasyonu geniş bir alan, ancak sağlam bir **bates numbering tutorial** elinizde olduğunda zaten bir adım öndesiniz.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}