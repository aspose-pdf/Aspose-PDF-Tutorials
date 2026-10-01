---
category: general
date: 2026-04-10
description: C# ile dakikalar içinde PDF'lere Bates numaralandırması ekleyin. Özel
  sayfa numaraları eklemeyi, PDF dosyalarını numaralandırmayı ve Bates numaralandırmasını
  verimli bir şekilde uygulamayı öğrenin.
draft: false
keywords:
- add bates numbering
- add custom page numbers
- how to number pdf
- how to add bates
- apply bates numbering
language: tr
og_description: C# ile dakikalar içinde PDF'lere Bates numaralandırması ekleyin. Bu
  rehber, özel sayfa numaraları eklemeyi, PDF dosyalarını numaralandırmayı ve Bates
  numaralandırmasını adım adım uygulamayı gösterir.
og_title: C# ile PDF'lere Bates Numaralandırması Ekleyin – Tam Kılavuz
tags:
- PDF
- C#
- Bates numbering
title: C# ile PDF'lere Bates Numaralandırması Ekle – Tam Rehber
url: /tr/net/programming-with-stamps-and-watermarks/add-bates-numbering-to-pdfs-with-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# ile PDF'lere Bates Numaralandırması Ekle – Tam Kılavuz

Hiç **bates numaralandırması eklemek** istediğiniz bir PDF'ye nereden başlayacağınızı bilemediniz mi? Tek değilsiniz—hukuk ekipleri, denetçiler ve büyük belge setleriyle çalışan herkes bu engelle sık sık karşılaşıyor. İyi haber? Birkaç satır C# kodu ile her sayfayı özel bir tanımlayıcıyla otomatik olarak damgalayabilirsiniz ve bu süreçte **özel sayfa numaraları eklemeyi** de öğreneceksiniz.

Bu öğreticide ihtiyacınız olan her şeyi adım adım inceleyeceğiz: gerekli NuGet paketi, numaralandırma seçeneklerinin yapılandırılması, numaraların uygulanması ve sonucun doğrulanması. Sonuna geldiğinizde **PDF dosyalarını programlı bir şekilde numaralandırmayı** bilecek ve önek, sonek, yazı tipi boyutu ya da belirli sayfaları hedefleme gibi ayarları nasıl değiştireceğinizi öğreneceksiniz.

## Gereksinimler

- .NET 6.0 veya üzeri (kod .NET Framework 4.7+ ile de çalışır)
- Visual Studio 2022 (veya tercih ettiğiniz herhangi bir IDE)
- **Aspose.PDF for .NET** kütüphanesi (öğrenme amaçlı ücretsiz deneme sürümü yeterli)
- Kontrol ettiğiniz bir klasörde bulunan `source.pdf` adlı örnek PDF

Bu maddeleri işaretlediyseniz, başlayalım.

## Adım 1: Aspose.PDF'yi Yükleyin ve Referans Verin

İlk olarak, Aspose.PDF paketini projenize ekleyin:

```bash
dotnet add package Aspose.PDF
```

Ya da NuGet Package Manager UI'ı kullanın. Yüklendikten sonra dosyanızın en üst kısmına isim alanını ekleyin:

```csharp
using Aspose.Pdf;
```

> **Pro ipucu:** Paketlerinizi güncel tutun; en son sürüm (Nisan 2026 itibarıyla) büyük belgeler için çeşitli performans iyileştirmeleri içeriyor.

## Adım 2: Kaynak PDF Belgesini Açın

Dosyayı açmak oldukça basit. `using` bloğu kullanacağız, böylece dosya tutamağı otomatik olarak serbest bırakılır.

```csharp
// Step 2: Open the source PDF document
using (var sourceDocument = new Document("YOUR_DIRECTORY/source.pdf"))
{
    // The rest of the workflow lives inside this block.
}
```

`Document` sınıfı tüm PDF'i temsil eder, sayfalara, açıklamalara ve tabii ki Bates numaralandırmasına erişim sağlar.

## Adım 3: Bates Numaralandırma Ayarlarını Tanımlayın

Şimdi işin özü—**bates numaralandırması ekle** seçeneklerini yapılandırma zamanı. Başlangıç numarası, önek, sonek, yazı tipi boyutu, kenar boşluğu ve damganın hangi sayfalara uygulanacağını kontrol edebilirsiniz.

```csharp
// Step 3: Define Bates numbering settings
var batesOptions = new BatesNumberingOptions
{
    StartNumber = 1,                 // First number in the sequence
    Prefix = "ABC-",                 // Text before the number
    Suffix = "-2024",                // Text after the number
    FontSize = 12,                   // Size of the numbering font
    Margin = 10,                     // Distance from the page edge (points)
    PageNumbers = new[] { 1, 2, 3 }  // Pages to which numbering is applied
};
```

### Bu Ayarların Önemi

- **StartNumber** bir önceki partiden devam eden bir dizi oluşturmanızı sağlar.
- **Prefix/Suffix** dava kimlikleri ya da yıl damgaları için kullanışlıdır.
- **FontSize** ve **Margin** okunabilirliği etkiler; çok küçük bir yazı tipi baskıda gözden kaçabilir.
- **PageNumbers**, **bates numaralandırması ekle**yi seçici olarak uyguladığınız yerdir. Bu diziyi atlayarak her sayfayı numaralandırabilirsiniz.

Eğer sıralı olmayan **özel sayfa numaraları eklemek** istiyorsanız, `{5, 10, 15}` gibi bir liste oluşturup buraya aktarabilirsiniz.

## Adım 4: Seçilen Sayfalara Bates Numaralandırmasını Uygulayın

Seçenekler hazır olduğunda, kütüphane ağır işi halleder. `AddBatesNumbering` metodu damgayı her hedef sayfaya ekler.

```csharp
// Step 4: Apply the Bates numbering to the selected pages
sourceDocument.AddBatesNumbering(batesOptions);
```

Arka planda, Aspose.PDF her sayfa için bir metin fragmenti oluşturur, kenar boşluğuna göre konumlandırır ve seçilen yazı tipi boyutunu uygular. Bu sayede sayılar, PDF'i ekranda görüntüleseniz de ya da yazdırsanız da tam istediğiniz yerde belirir.

## Adım 5: Değiştirilmiş Belgeyi Kaydedin

Son olarak, değişiklikleri yeni bir dosyaya kaydedin; böylece orijinal dosyanız dokunulmaz kalır.

```csharp
// Step 5: Save the modified document with Bates numbers
sourceDocument.Save("YOUR_DIRECTORY/bates.pdf");
```

Artık damgalı sayfaları içeren `bates.pdf` dosyanız var. Herhangi bir PDF görüntüleyicide açın ve aşağıdakine benzer bir şey göreceksiniz:

```
ABC-1-2024   (on page 1, top‑right)
ABC-2-2024   (on page 2, top‑right)
ABC-3-2024   (on page 3, top‑right)
```

### Sonucu Doğrulama

Hızlı bir kontrol olarak, ilk sayfanın metnini programlı bir şekilde geri okuyabilirsiniz:

```csharp
using (var doc = new Document("YOUR_DIRECTORY/bates.pdf"))
{
    var text = doc.Pages[1].ExtractText();
    Console.WriteLine(text.Contains("ABC-1-2024") ? "Bates number applied!" : "Oops, something went wrong.");
}
```

Konsol *Bates numarası uygulandı!* mesajını yazdırıyorsa, işiniz bitti.

## Kenar Durumları ve Yaygın Varyasyonlar

| Durum | Değiştirilecek | Sebep |
|-----------|----------------|--------|
| **Her sayfayı numarala** | `PageNumbers` öğesini atlayın veya `null` olarak ayarlayın | Dizi sağlanmadığında API varsayılan olarak tüm sayfalara uygular. |
| **Taraf başına farklı kenar boşluğu** | `Margin = new MarginInfo { Top = 15, Right = 10 }` (Aspose > 23.3 gerekir) | Yerleşim üzerinde ince ayar yapmanızı sağlar. |
| **Büyük belgeler (> 500 sayfa)** | `batesOptions.StartNumber` değerini yükseltin ve `batesOptions.FontSize = 10` ayarlayın; çakışmayı önler | Damganın okunabilirliğini korur, sayfayı kalabalıklaştırmaz. |
| **Farklı bir yazı tipi gerek** | `batesOptions.Font = FontRepository.FindFont("Arial")` | Bazı hukuk firmaları belirli bir tipografi talep eder. |

> **Dikkat:** Var olmayan bir sayfa numarası (ör. `PageNumbers = new[] { 999 }`) sağlarsanız, Aspose.PDF sessizce atlar. Listeyi dinamik oluşturuyorsanız her zaman aralığı doğrulayın.

## Tam Çalışan Örnek

Aşağıda, tamamen çalışır durumda olan program yer alıyor. Bir konsol uygulamasına yapıştırın, yolları ayarlayın ve **F5** tuşuna basın.

```csharp
using System;
using Aspose.Pdf;

class Program
{
    static void Main()
    {
        // Adjust these paths to match your environment
        string sourcePath = @"YOUR_DIRECTORY\source.pdf";
        string outputPath = @"YOUR_DIRECTORY\bates.pdf";

        // Open the source PDF
        using (var sourceDocument = new Document(sourcePath))
        {
            // Configure Bates numbering options
            var batesOptions = new BatesNumberingOptions
            {
                StartNumber = 1,
                Prefix = "ABC-",
                Suffix = "-2024",
                FontSize = 12,
                Margin = 10,
                PageNumbers = new[] { 1, 2, 3 } // Change or remove to number all pages
            };

            // Apply the numbering
            sourceDocument.AddBatesNumbering(batesOptions);

            // Save the new PDF
            sourceDocument.Save(outputPath);
        }

        // Verify the first page contains the expected stamp
        using (var doc = new Document(outputPath))
        {
            string extracted = doc.Pages[1].ExtractText();
            bool success = extracted.Contains("ABC-1-2024");
            Console.WriteLine(success
                ? "Bates numbering added successfully!"
                : "Numbering failed – check your options.");
        }
    }
}
```

Bu kod çalıştırıldığında, daha önce gösterilen üç damgalı sayfayı içeren `bates.pdf` oluşturulur. Dosyayı açtığınızda, sayıları kenardan 10 puan uzakta, 12 puanlık bir yazı tipiyle, sağa hizalanmış olarak göreceksiniz.

## Görsel Önizleme

![bates numaralandırma önizlemesi](/images/bates-numbering-sample.png)

*Yukarıdaki ekran görüntüsü, betik çalıştırıldıktan sonra **bates numaralandırması ekle** çıktısının nasıl göründüğünü göstermektedir.*

## Sonuç

C# kullanarak bir PDF'ye **bates numaralandırması eklemeyi** yeni öğrendik. `BatesNumberingOptions` yapılandırması, damganın uygulanması ve belgenin kaydedilmesi adımlarıyla, artık **özel sayfa numaraları ekleyebilen**, **pdf dosyalarını nasıl numaralandırır** ve **bates numaralandırması uygular** tekrar kullanılabilir bir çözümünüz var.

Sıradaki adım? Bu kodu bir klasördeki PDF'ler üzerinde toplu işleyiciyle birleştirin ya da her dava tipi için farklı önekler deneyin. Numaralandırdıktan sonra birden çok PDF'yi birleştirerek kapsamlı dava paketleri oluşturabilirsiniz.

Kenar durumlarıyla ilgili sorularınız mı var, yoksa sayıları başlık yerine alt bilgiye yerleştirmeyi mi merak ediyorsunuz? Yorum bırakın, iyi kodlamalar!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}