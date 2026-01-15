---
category: general
date: 2026-01-15
description: Aspose.Pdf ile PDF'nize hızlıca Bates numaraları ekleyin. PDF'ye alt
  bilgi eklemeyi, sayfa numaraları eklemeyi ve özel sayfa numaralandırmayı öğrenin.
draft: false
keywords:
- add bates numbers
- bates numbering pdf
- add footer to pdf
- add page numbers pdf
- add custom page numbering
language: tr
og_description: Aspose.Pdf ile PDF'nize hızlıca Bates numaraları ekleyin. PDF'ye alt
  bilgi eklemeyi, sayfa numaraları eklemeyi ve özel sayfa numaralandırma eklemeyi
  öğrenin.
og_title: PDF'ye Bates Numaraları Ekle – bates numbering pdf
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: PDF'ye Bates Numaraları Ekle – bates numaralandırma pdf
url: /tr/net/programming-with-text/add-bates-numbers-to-pdf-bates-numbering-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PDF'ye Bates Numaraları Ekle – Tam Kılavuz

PDF'ye **bates numbers** eklemeniz gerektiğinde nereden başlayacağınızı bilemediniz mi? Yalnız değilsiniz—hukuk ekipleri, denetçiler ve büyük belge setleriyle uğraşan herkes bu sorunu günlük olarak yaşıyor. İyi haber? Aspose.Pdf for .NET ile bu numaraları sadece birkaç satır kodla her sayfaya serpiştirebilirsiniz.

Bu öğreticide tüm süreci adım adım inceleyeceğiz: Aspose.Pdf kütüphanesini eklemek, kaynak dosyanızı yüklemek, bir *BatesNumberingArtifact* yapılandırmak, bunu alt bilgi olarak eklemek ve sonunda sonucu kaydetmek. Sonuna geldiğinizde **add footer to pdf**, **add page numbers pdf** ve hatta zor durumlar için **add custom page numbering** nasıl yapılır, öğreneceksiniz.

## Gereksinimler

- .NET 6+ (veya hâlâ klasik yığını kullanıyorsanız .NET Framework 4.8)  
- **Aspose.Pdf** NuGet paketine referans (`Install-Package Aspose.Pdf`)  
- Damgalamak istediğiniz bir PDF dosyası (biz ona `source.pdf` diyeceğiz)

Hepsi bu—ekstra araç yok, ağır PDF editörleri de yok. Hadi başlayalım.

![bates numaraları ekleme örneği](https://example.com/images/add-bates-numbers.png "bates numaraları ekleme örneği")

## Adım 1: Bates Numaraları Ekle – PDF Belgesini Yükle

İlk olarak, üzerinde değişiklik yapacağımız PDF'yi temsil eden bir `Document` nesnesine ihtiyacımız var. Bunu, yazmaya başlamadan önce bir Word belgesi açmak gibi düşünün.

```csharp
using Aspose.Pdf;
using System;

class Program
{
    static void Main()
    {
        // Load the PDF you want to add bates numbers to
        var pdfDocument = new Document(@"YOUR_DIRECTORY\source.pdf");

        // The rest of the steps go here...
    }
}
```

> **Neden önemli:** Dosyayı yüklemek, `Pages` koleksiyonuna erişmenizi sağlar; Bates numaralandırma artefaktını daha sonra buraya ekleyeceğiz. Dosya bulunamazsa, Aspose net bir `FileNotFoundException` fırlatır, bu yüzden yolu iki kez kontrol edin.

## Adım 2: Bates Numaralandırma PDF Ayarlarını Yapılandır

Şimdi sayıların nasıl görüneceğini tanımlıyoruz. `BatesNumberingArtifact` bir ön ek, başlangıç numarası, basamak doldurma, son ek ve konum ayarlamanıza izin verir. Bu, **bates numbering pdf**'in özüdür.

```csharp
// Step 2: Create and configure the Bates numbering artifact
var batesArtifact = new BatesNumberingArtifact
{
    Prefix = "CASE-",
    StartNumber = 1000,
    NumberDigits = 5,          // forces 5 digits, e.g., 01000
    Suffix = "-A",
    Placement = BatesNumberingArtifact.PlacementLocation.BottomCenter
};
```

> **Pro ipucu:** Sayıların başlıkta görünmesini istiyorsanız, `BottomCenter` yerine `TopCenter` kullanın. Konum enum'ı ayrıca `BottomLeft`, `BottomRight` vb. değerleri destekler; bu da farklı **add footer to pdf** stilleri için esneklik sağlar.

## Adım 3: PDF Sayfa Numaraları Ekle – Artefaktı Her Sayfaya Ekle

Artefakt hazır olduğunda, her sayfayı döngüyle gezerek `Artifacts` koleksiyonuna ekliyoruz. Bu adım, **adds page numbers pdf** işlemini gerçekleştirir.

```csharp
// Step 3: Attach the artifact to each page
foreach (Page page in pdfDocument.Pages)
{
    page.Artifacts.Add(batesArtifact);
}
```

> **Arka planda ne oluyor?** `Artifacts` koleksiyonu, sayfanın ana içeriğinden sonra işlenir; böylece Bates numarası mevcut metnin üstünde ama açıklamaların altında yer alır. Numarayı içeriğin arkasına (nadir) koymanız gerekirse, `page.Artifacts.Insert(0, batesArtifact)` kullanmanız gerekir.

## Adım 4: Özel Sayfa Numaralandırma Ekle – Güncellenmiş PDF'yi Kaydet

Son olarak, değiştirilmiş belgeyi diske yazıyoruz. Çıktı dosyası, Bates numaralarını her sayfanın kalıcı bir parçası olarak içerecek.

```csharp
// Step 4: Save the PDF with the new numbering
pdfDocument.Save(@"YOUR_DIRECTORY\bates_out.pdf");

Console.WriteLine("Bates numbers added successfully! Check bates_out.pdf.");
```

> **Doğrulama ipucu:** `bates_out.pdf` dosyasını herhangi bir görüntüleyicide açın. Her sayfanın alt ortasında `CASE-01000-A` gibi bir şey görmelisiniz. Numaralar eksikse, `Placement` özelliğinin istediğiniz konuma eşleştiğini iki kez kontrol edin.

## Tam Çalışan Örnek

Hepsini bir araya getirdiğimizde, işte tam ve çalıştırmaya hazır program:

```csharp
using Aspose.Pdf;
using System;

class Program
{
    static void Main()
    {
        // Load the source PDF
        var pdfDocument = new Document(@"YOUR_DIRECTORY\source.pdf");

        // Configure Bates numbering artifact
        var batesArtifact = new BatesNumberingArtifact
        {
            Prefix = "CASE-",
            StartNumber = 1000,
            NumberDigits = 5,
            Suffix = "-A",
            Placement = BatesNumberingArtifact.PlacementLocation.BottomCenter
        };

        // Attach artifact to each page (adds page numbers pdf)
        foreach (Page page in pdfDocument.Pages)
        {
            page.Artifacts.Add(batesArtifact);
        }

        // Save the new PDF (adds footer to pdf)
        pdfDocument.Save(@"YOUR_DIRECTORY\bates_out.pdf");

        Console.WriteLine("Bates numbers added successfully! Check bates_out.pdf.");
    }
}
```

### Beklenen Sonuç

- **Dosya:** `bates_out.pdf`, `source.pdf` ile aynı klasörde  
- **Görsel:** Alt‑ortada `CASE-01000-A`, `CASE-01001-A`, … metni, sonraki her sayfa için  
- **Davranış:** Numaralar kalıcı olarak gömülüdür; baskı, düzleştirme ve sonraki düzenlemelerden etkilenmez.

## Yaygın Varyasyonlar ve Kenar Durumları

| Durum | Nasıl Ayarlanır |
|-----------|---------------|
| **Farklı başlangıç numarası** | `StartNumber` değerini istediğiniz tam sayıya değiştirin (ör. `StartNumber = 500`). |
| **Hacim başına harf son ekleri** | Her sayfada `Suffix` değerini değiştirmek için bir döngü kullanın veya farklı son eklerle birden fazla artefakt oluşturun. |
| **Sağa hizalanmış numaralandırma** | `Placement = BatesNumberingArtifact.PlacementLocation.BottomRight` olarak ayarlayın. |
| **Büyük belgeler (10k+ sayfa)** | Sayfaları toplu işleyin veya taşmayı önlemek için `NumberDigits` değerini artırın. |
| **Belirli sayfalarda numaraları gizleme ihtiyacı** | `foreach` döngüsünde bu sayfaları atlayın (ör. `if (page.Number != 1) page.Artifacts.Add(batesArtifact);`). |

> **Dikkat edin:** `Prefix` veya `Suffix` içinde geçersiz dosya adı karakterleri (ör. `*` veya `?`) kullanmak. Aspose bunları yine de gömer, ancak daha sonra metni çıkardığınızda sorunlara yol açabilir.

## Üretim Kullanımı için Pro İpuçları

- **Artefakti önbellekle:** Ardışık olarak birçok PDF işliyorsanız, bir kez oluşturmak dosya başına birkaç milisaniye tasarruf sağlar.  
- **İş parçacığı güvenliği:** `BatesNumberingArtifact` örneği iş parçacığı güvenli değildir; bu yüzden her iş parçacığına kendi kopyasını verin.  
- **Performans:** Büyük toplu işlemler için, kaydetmeden önce PDF sıkıştırmasını devre dışı bırakın (`pdfDocument.Compress = false`), ardından gerekirse yeniden etkinleştirin.  
- **Test:** İlk oluşturulan PDF'de hızlı bir görsel kontrol yapın; konumun hukuk ekibinizin standartlarıyla eşleştiğinden emin olun.

## Sonuç

Artık Aspose.Pdf kullanarak herhangi bir PDF'ye **add bates numbers** eklemek için sağlam, uçtan uca bir tarifiniz var; **add footer to pdf**, **add page numbers pdf** ve **add custom page numbering** seçenekleriyle birlikte. Kod tamamen bağımsızdır, .NET 6 ve üzeriyle çalışır ve mevcut herhangi bir otomasyon hattına kolayca entegre edilebilir.

Sırada ne var? `BottomCenter` konumunu bir başlık stiline değiştirin, dinamik ön eklerle (ör. veritabanından gelen dava kimlikleri) deney yapın veya bunu Aspose'un metin‑çıkarma özellikleriyle birleştirerek yeni numaralandırılmış belgeleriniz için aranabilir bir indeks oluşturun. Gökyüzü sınırdır ve belge kontrolü için güçlü bir araca sahip oldunuzKodlamaktan keyif alın ve PDF'leriniz her zaman mükemmel numaralandırılmış olsun!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}