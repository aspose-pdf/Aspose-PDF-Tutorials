---
category: general
date: 2026-03-22
description: Aspose.Pdf ile PDF'ye Bates numaralandırmasını hızlıca ekleyin. Bates
  eklemeyi, sıralı sayfa numaraları eklemeyi, özel altbilgi PDF eklemeyi ve PDF'ye
  artefakt eklemeyi dakikalar içinde öğrenin.
draft: false
keywords:
- add bates numbering pdf
- how to add bates
- add sequential page numbers
- add custom footer pdf
- add artifact to pdf
language: tr
og_description: Aspose.Pdf kullanarak PDF'ye Bates numaralandırması ekleyin. Bu kılavuz,
  Bates ekleme, sıralı sayfa numaraları ekleme, özel altbilgi PDF ekleme ve PDF'ye
  artefakt ekleme yöntemlerini gösterir.
og_title: Bates Numaralandırma PDF Ekle – Adım Adım C# Öğreticisi
tags:
- Aspose.Pdf
- C#
- PDF automation
title: Bates Numaralandırması PDF Ekle – Tam C# Rehberi
url: /tr/net/programming-with-stamps-and-watermarks/add-bates-numbering-pdf-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Bates Numaralandırma PDF – Tam C# Rehberi

Hiç bir grup yasal belgeye **bates numbering pdf** eklemeniz gerekti ama nereden başlayacağınızı bilemediniz mi? Tek başınıza değilsiniz—birçok geliştirici, dava‑yönetim araçları oluştururken bu engelle karşılaşıyor. İyi haber? Aspose.Pdf ile sadece birkaç satır kodla **bates ekleyebilir**, **ardışık sayfa numaraları ekleyebilir** ve hatta **custom footer pdf** öğelerini ekleyebilirsiniz.  

Bu öğreticide, kütüphaneyi kurmaktan son dosyayı kaydetmeye kadar tüm süreci adım adım gösterecek ve mevcut içeriği bozmadan **add artifact to pdf** dosyalarına nasıl öğe ekleyeceğinize dair ipuçları paylaşacağız. Sonunda, herhangi bir .NET projesine ekleyebileceğiniz çalışır bir kod parçacığına sahip olacaksınız.

## Gereksinimler

- .NET 6+ (kod .NET Core ve .NET Framework’te de çalışır)  
- Geçerli bir Aspose.Pdf for .NET lisansı (ücretsiz deneme sürümüyle başlayabilirsiniz)  
- Bir klasörde bulunan giriş PDF’i (`input.pdf`)  
- Visual Studio, Rider veya tercih ettiğiniz herhangi bir C# editörü  

Hepsi bu—Aspose.Pdf dışındaki ekstra NuGet paketine gerek yok.

## Adım 1: Aspose.Pdf’i NuGet üzerinden kurun

İlk iş, kütüphaneyi makinenize getirmek. Proje klasörünüzde bir terminal açın ve şu komutu çalıştırın:

```bash
dotnet add package Aspose.Pdf
```

Ya da Visual Studio’nun Package Manager Console’unu kullanıyorsanız:

```powershell
Install-Package Aspose.Pdf
```

*İpucu:* Kurulumdan sonra, çözüm gezgininde `Dependencies → Packages` altında `Aspose.Pdf` klasörünün göründüğünden emin olun.

## Adım 2: Kaynak PDF Belgesini Yükleyin

Şimdi damga vurmak istediğimiz PDF’i temsil eden bir `Document` nesnesi oluşturacağız. `using` ifadesi, dosya tutamacının otomatik olarak serbest bırakılmasını sağlar.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using System.Drawing; // For Color

// Step 2: Load the source PDF
using var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");
```

Neden `using var` kullanıyoruz? Bir istisna oluşsa bile nesnenin disposal’ını garanti eder, böylece aynı dosyayı daha sonra üzerine yazmaya çalıştığınızda dosya kilitlenmesi sorunları yaşamazsınız.

## Adım 3: Bates Numaralandırma Artefaktını Oluşturup Yapılandırın

Bates numarası, PDF’in mantıksal yapısında yer alan bir metin artefaktıdır. **custom footer pdf** gibi davranabilir; çünkü her sayfada görünür ancak sayfanın içerik akışının bir parçası değildir.

```csharp
// Step 3: Define the Bates numbering artifact
var batesArtifact = new BatesNumberingArtifact
{
    Prefix = "INV-",          // Optional prefix – change as needed
    Start = 1000,             // Starting number
    Format = "0000",          // Zero‑padded format (e.g., 1000 → 1000)
    X = 500,                  // Horizontal position (points from left)
    Y = 20,                   // Vertical position (points from bottom)
    FontSize = 10,
    FontColor = Color.Black
};
```

### Bu Ayarların Önemi

- **Prefix**: Belge tiplerini ayırt etmek için faydalıdır (ör. faturalar için “INV‑”).  
- **Start**: İlk numarayı belirler; dosyalar arasında süreklilik gerekiyorsa bunu veritabanından alabilirsiniz.  
- **Format**: `"0000"` dört haneli bir gösterim zorlar, sayı büyüdükçe hizalamanın korunmasını sağlar.  
- **X/Y**: Koordinatlar alt‑sol köşeden ölçülür, bu yüzden `Y = 20` metni sayfa kenarının hemen üzerine yerleştirir. Sayıyı sola hizalamak veya ortalamak isterseniz `X` değerini ayarlayın.

Eğer Bates numarası yerine **ardışık sayfa numaraları** eklemek isterseniz, sadece `Prefix`’i kaldırın ve `Format`’ı `"###"` ya da tercih ettiğiniz başka bir desenle değiştirin.

## Adım 4: Artefaktı Tüm Sayfalara Uygulayın

Aspose.Pdf, tek bir çağrı ile artefaktı belgeye bütün sayfalara eklemenizi sağlar. Bu, **add artifact to pdf** işlemini manuel döngü kullanmadan yapmanın en verimli yoludur.

```csharp
// Step 4: Apply the artifact to the whole document
pdfDocument.Pages.AddArtifact(batesArtifact);
```

Arka planda, Aspose artefaktı her sayfanın sayfa sözlüğüne ekler; böylece numaralandırma PDF’in mantıksal yapısının bir parçası olur—daha sonraki çıkarma veya arama işlemleri için mükemmeldir.

## Adım 5: Güncellenmiş PDF’i Kaydedin

Son olarak değişiklikleri diske yazın. Orijinali üzerine yazabilir ya da yeni bir dosyaya kaydedebilirsiniz; ikincisi geliştirme sırasında daha güvenlidir.

```csharp
// Step 5: Save the PDF with Bates numbers
pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
```

`output.pdf` dosyasını bir görüntüleyicide açtığınızda, her sayfanın sağ‑alt köşesinde “INV‑1000”, “INV‑1001”, … gibi etiketleri göreceksiniz.

### Sonucu Doğrulama

PDF’i Adobe Acrobat ya da herhangi bir görüntüleyicide açıp numaraları kontrol edin. Programatik olarak doğrulamak isterseniz artefaktı şu şekilde okuyabilirsiniz:

```csharp
foreach (var page in pdfDocument.Pages)
{
    foreach (var artifact in page.Artifacts)
    {
        Console.WriteLine($"Page {page.Number}: {artifact.Text}");
    }
}
```

Bu kod parçacığı her sayfanın Bates etiketini yazdırır—otomatik testler için kullanışlıdır.

## Kenar Durumları ve Yaygın Sorular

### PDF’imde Zaten Bir Alt Bilgi (Footer) Varsa Ne Olur?

Bir artefakt eklemek mevcut alt bilgileri üzerine yazmaz çünkü artefaktlar ayrı bir katmanda bulunur. Görsel çakışma bir sorun ise `Y` koordinatını ayarlayın ya da `X` offsetini artırarak Bates numarasını kaydırın.

### Farklı Bir Yazı Tipi veya Renk Kullanabilir miyim?

Kesinlikle. `BatesNumberingArtifact`, `Artifact` sınıfından türediği için `Font`, `FontColor` ve hatta `Opacity` ayarlarını yapabilirsiniz. Örnek:

```csharp
batesArtifact.Font = FontRepository.FindFont("Arial");
batesArtifact.FontColor = Color.FromArgb(255, 0, 0); // Red
```

### Yeni Bir Belge İçin Sayacı Nasıl Sıfırlarım?

`AddArtifact` çağrısından önce `Start` değerini değiştirin. Bir döngü içinde birçok PDF oluşturuyorsanız, uygulama mantığınızda çalışan bir sayaç tutun.

### Şifreli PDF’lerle Çalışabilir mi?

Aspose.Pdf, şifreyi sağladığınızda şifreli PDF’leri açabilir:

```csharp
var loadOptions = new LoadOptions { Password = "mySecret" };
using var pdfDocument = new Document("encrypted.pdf", loadOptions);
```

Şifre çözüldükten sonra aynı artefakt‑ekleme adımları sorunsuz çalışır.

## Tam Çalışan Örnek

Aşağıda, tamamen çalışır durumda bir program bulunuyor. Konsol uygulamasına yapıştırın, yolları ayarlayın ve **F5** tuşuna basın.

```csharp
using System;
using System.Drawing;               // For Color
using Aspose.Pdf;
using Aspose.Pdf.Annotations;

class Program
{
    static void Main()
    {
        // Load the source PDF
        using var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");

        // Create the Bates numbering artifact
        var batesArtifact = new BatesNumberingArtifact
        {
            Prefix = "INV-",
            Start = 1000,
            Format = "0000",
            X = 500,
            Y = 20,
            FontSize = 10,
            FontColor = Color.Black
        };

        // Apply the artifact to every page
        pdfDocument.Pages.AddArtifact(batesArtifact);

        // Save the result
        pdfDocument.Save("YOUR_DIRECTORY/output.pdf");

        Console.WriteLine("Bates numbering added successfully!");
    }
}
```

**Beklenen çıktı:** Konsol “Bates numbering added successfully!” mesajını verir ve `output.pdf` her sayfada sağ‑alt köşede `INV‑1000`, `INV‑1001` gibi ardışık etiketler içerir.

## Hızlı Özet

- **Ana hedef:** Aspose.Pdf ile **add bates numbering pdf**.  
- **Ne yaptık:** **add bates**, **add sequential page numbers** ve **add custom footer pdf** öğelerini tek bir artefaktla eklemeyi gösterdik.  
- **Ne öğrendik:** **add artifact to pdf**, kenar durumlarını ele alma ve sonucu doğrulama.

## Sıradaki Adımlar

- **Dinamik önekler:** Veritabanından değer çekerek “CASE‑2023‑001”, “CASE‑2023‑002” gibi etiketler oluşturun.  
- **Koşullu yerleştirme:** Sayfa boyutu algılamasını (`page.MediaBox`) kullanarak yatay sayfalarda numaraları ortalayın.  
- **Su işaretiyle birleştirme:** Bates numarasının yanına yarı saydam bir logo ekleyerek marka oluşturun.  

Deney yapmaktan çekinmeyin—belki binlerce dosyayı toplu işlemek için daha akıllı bir yol keşfedersiniz. Sorun yaşarsanız yorum bırakın ya da Aspose’un resmi dokümantasyonuna göz atın (gerçekten çok açıklayıcı). Mutlu kodlamalar!  

![bates numaralandırma pdf örneği](https://example.com/bates-numbering-screenshot.png "Screenshot showing add bates numbering pdf in a PDF viewer")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}