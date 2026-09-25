---
category: general
date: 2026-02-28
description: Aspose.Pdf ile C#'ta PDF imzasını kontrol edin – imzayı nasıl kontrol
  edeceğinizi, dijital PDF imzasını nasıl doğrulayacağınızı ve PDF imzasını hızlıca
  nasıl doğrulayacağınızı öğrenin.
draft: false
keywords:
- check pdf signature
- how to check signature
- validate digital signature pdf
- verify pdf signature
- read pdf digital signatures
language: tr
og_description: Aspose.Pdf ile C#’ta PDF imzasını kontrol edin. İmzayı nasıl kontrol
  edeceğinizi, dijital PDF imzasını nasıl doğrulayacağınızı ve PDF imzasını dakikalar
  içinde nasıl doğrulayacağınızı öğrenin.
og_title: C# ile PDF İmzasını Kontrol Et – PDF Dijital İmzasını Doğrula
tags:
- C#
- Aspose.Pdf
- Digital Signature
- PDF
title: C#'ta PDF İmzasını Kontrol Et – PDF Dijital İmzasını Doğrula
url: /tr/net/digital-signatures/check-pdf-signature-in-c-validate-digital-signature-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# ile PDF Signature Kontrolü – Dijital İmza PDF'yi Doğrulama

Hiç **PDF imzasını nasıl kontrol edeceğinizi** büyük bir GUI aracı kullanmadan merak ettiniz mi? Yalnız değilsiniz. Birçok kurumsal iş akışında **PDF imzasını** programlı olarak kontrol etmemiz gerekiyor, özellikle belge alım hatlarını otomatikleştirirken.  

Bu öğreticide, Aspose.Pdf for .NET kullanarak **PDF imzasını doğrulama** konusunda tam, çalıştırılabilir bir örnek üzerinden adım adım ilerleyeceğiz ve ayrıca **dijital imza PDF'yi doğrulama** en iyi uygulamalarına da değineceğiz. Belirsiz referanslar yok, sadece bugün kopyalayıp‑yapıştırabileceğiniz saf kod.

## Öğrenecekleriniz

- İmzalı bir PDF belgesini diskte yükleyin.
- Dosyaya gömülü tüm dijital imzaları alın.
- Her bir imzanın bozulup bozulmadığını belirleyin.
- Açık, insan tarafından okunabilir bir sonuç üretin.
- Birden fazla imza veya şifre korumalı PDF'ler gibi uç durumları ele almak için ekstra ipuçları.

**Prerequisites**  
.NET 6+ (veya .NET Framework 4.6+) ve geçerli bir Aspose.Pdf lisansı (veya geçici bir değerlendirme anahtarı) gerekir. NuGet paketini henüz kurmadıysanız, şu komutu çalıştırın:

```bash
dotnet add package Aspose.Pdf
```

Hepsi bu—ekstra bağımlılık yok.

![PDF imza doğrulama akışını gösteren diyagram](/images/check-pdf-signature-flow.png){: .align-center alt="pdf imza akış diyagramı"}

## Adım 1 – Projeyi Kurun ve Ad Alanlarını İçe Aktarın

İlk olarak, yeni bir konsol uygulaması oluşturun (veya kodu mevcut bir servise entegre edin). `using` yönergeleri gerekli sınıfları kapsam içine getirir.

```csharp
// Step 1: Project setup – import Aspose.Pdf namespaces
using Aspose.Pdf;
using Aspose.Pdf.Facades;
using System;
```

> **Neden önemli:** `Document` PDF yapısını yönetirken, `PdfFileSignature` imza‑ile ilgili işlemlere erişim sağlar. İçe aktarmaları en üstte tutmak, kodun geri kalanını daha temiz ve okunabilir hâle getirir.

## Adım 2 – İmzalı PDF Belgesini Yükleyin

Zaten bir veya daha fazla dijital imza içeren bir PDF'ye ihtiyacınız var. `YOUR_DIRECTORY/signed.pdf` ifadesini makinenizdeki gerçek yol ile değiştirin.

```csharp
// Step 2: Load the signed PDF document
using var signedPdf = new Document("YOUR_DIRECTORY/signed.pdf");

// Quick sanity check – does the file even exist?
if (signedPdf == null)
{
    Console.WriteLine("Unable to load the PDF. Verify the path and try again.");
    return;
}
```

> **Pro ipucu:** PDF'niz şifre korumalıysa, güvenli bir şekilde açmak için `new Document(path, password)` aşırı yüklemesini kullanın.

## Adım 3 – PdfFileSignature Örneği Oluşturun

`PdfFileSignature`, tüm imza‑ile ilgili sorgular için temel araçtır. Az önce yüklediğimiz `Document` nesnesini sarar.

```csharp
// Step 3: Initialise the signature handler
using var signatureHandler = new PdfFileSignature(signedPdf);
```

> **Neden `using` kullanıyoruz** – Hem `Document` hem de `PdfFileSignature` `IDisposable` uygular. `using` ifadesi, yönetilmeyen kaynakların (dosya tutamaçları, yerel tamponlar) hızlıca serbest bırakılmasını garanti eder ve uzun süren servislerde bellek sızıntılarını önler.

## Adım 4 – Tüm İmza Adlarını Alın

Bir PDF birden fazla imza içerebilir ve her biri benzersiz bir adla tanımlanır. `GetSignNames` yöntemi bu tanımlayıcıları içeren bir string dizisi döndürür.

```csharp
// Step 4: Grab every signature name present in the PDF
string[] signatureNames = signatureHandler.GetSignNames();

if (signatureNames.Length == 0)
{
    Console.WriteLine("No signatures were found in this document.");
    return;
}
```

> **Sık sorulan soru:** *PDF'de görünmez imzalar olursa ne olur?*  
> Aspose.Pdf, görünmez ve görünür imzaları aynı şekilde ele alır; ikisi de `GetSignNames` koleksiyonunda görünecektir.

## Adım 5 – Her İmzanın Bütünlüğünü Doğrulayın

Şimdi dizi üzerinde döngü kurarak Aspose'a herhangi bir imzanın değiştirilip değiştirilmediğini soruyoruz. `IsSignatureCompromised` yöntemi, imzanın kriptografik hash'i belge içeriğiyle artık eşleşmiyorsa `true` döndürür.

```csharp
// Step 5: Check each signature for compromise
foreach (var name in signatureNames)
{
    bool isCompromised = signatureHandler.IsSignatureCompromised(name);

    // Step 6: Output the result
    Console.WriteLine($"{name}: compromised = {isCompromised}");
}
```

**Beklenen çıktı** (örnek):

```
Signature1: compromised = False
Signature2: compromised = True
```

Bir imza *bozulmamış* ise, belgenin bütünlüğüne güvenle güvenebilirsiniz. `True` değeri görünürse, imza uygulandıktan sonra belge değiştirilmiş demektir—denetim günlükleri için mükemmeldir.

## Adım 6 – Uç Durumları ve İleri Senaryoları Ele Alma

### Farklı Algoritmalara Sahip Birden Çok İmza

Bazen bir PDF, RSA, ECDSA veya zaman damgası tokenlarıyla oluşturulmuş imzalar içerir. `IsSignatureCompromised` algoritma detaylarını soyutlar, ancak yine de **PDF dijital imzalarını** okuyarak algoritma adını, imzalama zamanını veya sertifika detaylarını kaydetmek isteyebilirsiniz.

```csharp
// Optional: Retrieve detailed info for each signature
foreach (var name in signatureNames)
{
    var info = signatureHandler.GetSignatureInfo(name);
    Console.WriteLine($"--- {name} Details ---");
    Console.WriteLine($"Signer: {info.SignerName}");
    Console.WriteLine($"Reason: {info.Reason}");
    Console.WriteLine($"Signing Time: {info.SigningTime}");
    Console.WriteLine($"Algorithm: {info.SignatureAlgorithm}");
}
```

### Tüm Belgeyi Yüklemeden Bir İmzayı Doğrulama

Eğer büyük bir dosya için sadece **pdf imzasını doğrulamanız** gerekiyorsa, doğrudan dosya yolunu kabul eden `PdfFileSignature` yapıcıyı kullanarak tam `Document` nesnesini yükleme yükünden kaçınabilirsiniz.

```csharp
using var signatureHandler = new PdfFileSignature("large_signed.pdf");
bool compromised = signatureHandler.IsSignatureCompromised("Signature1");
```

### Şifre Koruması Olan PDF'ler

PDF şifreli olduğunda, `Document` oluştururken sahibi ya da kullanıcı şifresini sağlamalısınız. İmza doğrulama süreci daha sonra aynı kalır.

```csharp
using var signedPdf = new Document("protected.pdf", "myPassword");
using var signatureHandler = new PdfFileSignature(signedPdf);
```

## Tam Çalışan Örnek

Aşağıda, olduğu gibi derleyip çalıştırabileceğiniz tam program yer alıyor. Yukarıdaki tüm adımları ve nazik hata yönetimini içerir.

```csharp
// Full example – Check PDF Signature with Aspose.Pdf
using Aspose.Pdf;
using Aspose.Pdf.Facades;
using System;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the signed PDF (adjust the path as needed)
        using var signedPdf = new Document("YOUR_DIRECTORY/signed.pdf");
        if (signedPdf == null)
        {
            Console.WriteLine("Failed to load PDF. Check the file path.");
            return;
        }

        // 2️⃣ Initialise the signature handler
        using var signatureHandler = new PdfFileSignature(signedPdf);

        // 3️⃣ Get all signature names
        string[] signatureNames = signatureHandler.GetSignNames();

        if (signatureNames.Length == 0)
        {
            Console.WriteLine("No signatures detected in the document.");
            return;
        }

        // 4️⃣ Iterate and check each signature
        foreach (var name in signatureNames)
        {
            bool isCompromised = signatureHandler.IsSignatureCompromised(name);
            Console.WriteLine($"{name}: compromised = {isCompromised}");

            // Optional: Dump extra info (demonstrates read pdf digital signatures)
            var info = signatureHandler.GetSignatureInfo(name);
            Console.WriteLine($"   Signer: {info.SignerName}");
            Console.WriteLine($"   Time  : {info.SigningTime}");
            Console.WriteLine($"   Algo  : {info.SignatureAlgorithm}");
        }
    }
}
```

`dotnet run` ile programı çalıştırın. Her şey doğru ayarlandıysa, imzaların bir listesini ve her birinin bozulup bozulmadığını gösteren bir boolean bayrağını göreceksiniz.

## Sonuç

Artık C# içinde programlı olarak **PDF imzasını nasıl kontrol edeceğinizi**, **dijital imza PDF'yi nasıl doğrulayacağınızı** ve Aspose.Pdf kullanarak **PDF imzasının** bütünlüğünü nasıl **doğrulayacağınızı** biliyorsunuz. Temel mantık, belgeyi yüklemek, imza adlarını almak ve `IsSignatureCompromised` metodunu çağırmaktan ibarettir. Buradan sertifika detaylarını kaydetmeye, şifre korumalı dosyaları ele almaya veya kontrolü daha büyük bir belge‑işleme hattına entegre etmeye genişletebilirsiniz.

**Sonraki adımlar**  
- Uyumluluk raporlaması için imzalayan sertifikalarını çıkarmak amacıyla **pdf dijital imzalarını oku** özelliğini keşfedin.  
- Bu kontrolü bir dosya‑izleyici servisiyle birleştirerek bozulmuş yüklemeleri otomatik olarak reddedin.  
- Farklı imza algoritmaları (RSA, ECDSA) ile test ederek doğrulama mantığınızın sağlam kalmasını sağlayın.

Uygulamaya çalıştığınız bir değişiklik mi var? Yorum bırakın, birlikte sorun giderelim. Kodlamanın tadını çıkarın!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}