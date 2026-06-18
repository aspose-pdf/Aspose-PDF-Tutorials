---
category: general
date: 2026-03-24
description: PFX sertifikasını C# ile hızlı ve güvenli bir şekilde dosyadan PKCS7
  ayrık imza oluşturmak için yükleyin. Tam kod ve olası hatalarla adım adım rehber.
draft: false
keywords:
- load pfx certificate c#
- create pkcs7 detached signature
- pkcs7 signature from file
- c# pkcs7 signing
- digital signature c#
language: tr
og_description: C# ile PFX sertifikasını yükleyin ve dosyadan PKCS7 ayrı imza oluşturun.
  Açıklamalar ve uç durum yönetimi içeren tam örnek.
og_title: PFX Sertifikasını Yükle C# – PKCS7 Ayrı İmza Oluştur
tags:
- C#
- PKCS7
- X509
- Cryptography
title: PFX Sertifikasını Yükle C# – PKCS7 Ayrı İmza Oluştur
url: /tr/net/programming-with-security-and-signatures/load-pfx-certificate-c-create-pkcs7-detached-signature/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PFX Sertifikasını C# ile Yükleme – PKCS7 Ayrı İmza Oluşturma

Hiç **C#'ta bir PFX sertifikasını yükleyip** bazı verileri imzalamanız gerektiğinde, nereden başlayacağınızı bilemediniz mi? Tek başınıza değilsiniz—birçok geliştirici X.509 sertifikaları ve PKCS#7 ile ilk kez karşılaştıklarında aynı duvara çarpar.

İyi haber? Bu öğreticide **C#'ta bir PFX sertifikasını yükleyen**, bir **PKCS7 ayrı imza** oluşturan ve hatta imzayı bir dosyadan nasıl çıkaracağınızı gösteren hazır‑çalıştır çözümünü elde edeceksiniz. Belirsiz referanslar yok, sadece somut kod ve her satırın ardındaki mantık.

> **Neler Öğreneceksiniz**  
> * Sertifika yükleme sürecinin net bir anlayışı.  
> * PKCS7 ayrı imza oluşturan tam, derlenebilir bir örnek.  
> * Yaygın tuzakları (yanlış şifre, eksik dosya, algoritma uyumsuzlukları) ele almanın ipuçları.  

### Önkoşullar

- .NET 6.0 veya üzeri (kullanılan API'ler temel sınıf kitaplığının bir parçasıdır).  
- Geçerli bir `.pfx` dosyası ve şifresi.  
- Visual Studio 2022 veya tercih ettiğiniz herhangi bir editör—temel örnek için özel bir NuGet paketi gerekmez.  

Eğer bunlara sahipseniz, başlayalım.

---

## PFX Sertifikasını C# ile Yükleme – Adım‑Adım

Aşağıda ihtiyacınız olacak minimal `using` yönergeleri seti bulunmaktadır. Derleyicinin tipleri bulabilmesi için dosyanızın en üstünde tutun.

```csharp
using System;
using System.IO;
using System.Security.Cryptography;
using System.Security.Cryptography.X509Certificates;
```

### 1️⃣ Sertifika yolunu ve şifresini belirtin

İlk olarak, çalışma zamanına `.pfx` dosyasının nerede olduğunu ve şifresinin ne olduğunu söyleyin. Demo için yolları sabit kodlamak sorun değil, ancak **asla** şifreleri üretim koduna gömmeyin.

```csharp
// Step 1: Path to your certificate and its password
string certificatePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "certificate.pfx");
string certificatePassword = "yourPassword"; // <-- replace with a secure source
```

> **Pro ipucu:** Şifreyi Azure Key Vault, AWS Secrets Manager veya bir ortam değişkeninde saklayın—asla kaynak kontrolüne commit etmeyin.

### 2️⃣ Sertifikayı güvenli bir şekilde yükleyin

Yüklemeyi bir `try / catch` bloğuna sararız, böylece eksik dosya veya hatalı şifre gibi yaygın hataları ortaya çıkarırız.

```csharp
X509Certificate2 LoadCertificate(string path, string password)
{
    try
    {
        // The X509KeyStorageFlags ensure the private key is exportable for signing
        var cert = new X509Certificate2(path, password,
            X509KeyStorageFlags.MachineKeySet |
            X509KeyStorageFlags.PersistKeySet |
            X509KeyStorageFlags.Exportable);

        if (!cert.HasPrivateKey)
            throw new InvalidOperationException("The certificate does not contain a private key.");

        return cert;
    }
    catch (Exception ex) when (ex is CryptographicException || ex is IOException)
    {
        Console.Error.WriteLine($"Failed to load certificate: {ex.Message}");
        throw;
    }
}
```

### 3️⃣ Bir **PKCS7 ayrı imza** nesnesi oluşturun

Bir `PKCS7Detached` sınıfını (birçok ticari SDK bunu sağlar) ortaya çıkaran üçüncü‑taraf bir kütüphane kullandığınızı varsayarsak, az önce yüklediğimiz sertifika ile bir örnek oluştururuz.

```csharp
// Step 3: Build the signer
var certificate = LoadCertificate(certificatePath, certificatePassword);

var pkcs7Signer = new PKCS7Detached(certificate)
{
    // Provide a custom hash‑signing callback.
    // The library will invoke this delegate for each hash it needs to sign.
    CustomSignHash = (hash, algorithm) => MySigner.Sign(hash, algorithm)
};
```

> **Neden bir geri çağırma?** Bazı SDK'lar donanım güvenlik modüllerini (HSM) veya uzaktan imzalama hizmetlerini bağlamanıza izin verir. `CustomSignHash`'i ortaya çıkararak imzalama mantığını esnek tutarsınız.

### 4️⃣ İmzalama temsilcisini uygulayın

İşte yüklenen sertifikadan özel anahtarı kullanan basit bir uygulama. Gerekirse `MySigner.Sign` ifadesini kendi HSM çağrınızla değiştirin.

```csharp
static class MySigner
{
    public static byte[] Sign(byte[] hash, HashAlgorithmName algorithm)
    {
        // The certificate's private key is an RSA key in most cases.
        using RSA rsa = certificate.GetRSAPrivateKey()
            ?? throw new InvalidOperationException("RSA private key not available.");

        // RSA-PKCS#1 v1.5 signing – adjust if your policy requires PSS.
        return rsa.SignHash(hash, algorithm, RSASignaturePadding.Pkcs1);
    }
}
```

### 5️⃣ Rastgele veriyi imzalayın ve ayrı PKCS7 ikili verisini alın

Şimdi gerçekten bir şeyi imzalıyoruz. Veri bir dosya, bir JSON yükü ya da korumanız gereken herhangi bir şey olabilir.

```csharp
// Step 5: Data you want to protect
byte[] dataToSign = File.ReadAllBytes("sample.txt");

// The PKCS7Detached class usually offers a Sign method that returns the raw signature.
byte[] detachedSignature = pkcs7Signer.Sign(dataToSign);

// Save the signature to disk for later verification
File.WriteAllBytes("sample.txt.sig", detachedSignature);

Console.WriteLine("Detached PKCS7 signature created successfully.");
```

**Beklenen çıktı**

```
Detached PKCS7 signature created successfully.
```

Artık **dosyadan bir PKCS7 imzasına** (`sample.txt.sig`) sahipsiniz; bu imza, orijinal veriden bağımsız olarak doğrulanabilir.

---

## PKCS7 Ayrı İmza Oluşturma – Gelişmiş Seçenekler

Temel akış çoğu senaryo için çalışsa da, üretim sistemleri genellikle ekstra ayarlara ihtiyaç duyar:

| Özellik | Nasıl etkinleştirilir | Ne zaman kullanılır |
|---------|----------------------|---------------------|
| **Algoritma seçimi** | `SignHash` metoduna `HashAlgorithmName.SHA256` (veya SHA384/SHA512) gönderin | Uyumluluk düzeniniz belirli bir hash gerektiriyorsa |
| **Zaman damgası** | İmzadan sonra bir RFC‑3161 zaman damgası ekleyin | Uzun vadeli doğrulama için |
| **Birden fazla imzalayan** | Ek `PKCS7Detached` örnekleri oluşturup birleştirin | Belgelerin birlikte imzalanması gerektiğinde |
| **Özel CMS öznitelikleri** | `Sign` öncesinde kütüphanenin `AddAttribute` metodunu kullanın | İmza zamanı, imzalayan kimliği vb. eklemek için |

Aşağıda SHA‑256 seçimini gösteren hızlı bir kod parçacığı bulunuyor:

```csharp
CustomSignHash = (hash, _) => MySigner.Sign(hash, HashAlgorithmName.SHA256)
```

---

## PKCS7 Ayrı İmzayı Doğrulama (Opsiyonel)

Doğrulama, hikayenin diğer yarısıdır. Çoğu kütüphane, orijinal veri ve ayrı imzayı alan bir `Verify` metodu sunar.

```csharp
bool VerifySignature(byte[] originalData, byte[] signature, X509Certificate2 cert)
{
    var verifier = new PKCS7Detached(cert);
    return verifier.Verify(originalData, signature);
}

// Usage
bool isValid = VerifySignature(dataToSign, detachedSignature, certificate);
Console.WriteLine(isValid ? "Signature valid!" : "Signature invalid!");
```

Farklı bir SDK kullanıyorsanız, .NET'in `System.Security.Cryptography.Pkcs` ad alanında `CmsSignedData` veya `SignedCms` sınıflarını arayın—bunlar da ayrı imzaları işleyebilir.

---

## Yaygın Tuzaklar ve Nasıl Önlenir

1. **Yanlış şifre** – `CryptographicException` *“The specified network password is not correct.”* mesajını verir. Şifreleri güvenli bir şekilde saklayın ve sertifikayı yüklemeden önce bağımsız olarak test edin.  
2. **Özel anahtarı olmayan sertifika** – Bazı `.pfx` dosyaları özel anahtar olmadan dışa aktarılır. CA veya Key Vault'taki dışa aktarma ayarlarını iki kez kontrol edin.  
3. **Algoritma uyumsuzluğu** – İmzalayan SHA‑256 beklerken siz SHA-1 gönderirseniz, doğrulama başarısız olur. İmzalama ve doğrulama adımları arasında algoritmayı aynı tutun.  
4. **Dosya yolu sorunları** – Göreli yollar geliştirme ortamında çalışır ama dağıtımda kırılır. `Path.Combine(AppDomain.CurrentDomain.BaseDirectory, ...)` ya da yapılandırma‑tabanlı mutlak yolları tercih edin.  
5. **Platform farkları** – Windows ve Linux özel anahtar deposunu farklı şekilde yönetir. `X509KeyStorageFlags.Exportable` kullanmak çoğu çapraz‑platform sorununu hafifletir.

---

## Tam Çalışan Örnek (Kopyala‑Yapıştır Hazır)

```csharp
using System;
using System.IO;
using System.Security.Cryptography;
using System.Security.Cryptography.X509Certificates;

// ------------------------------------------------------------
// Helper class that encapsulates signing logic
// ------------------------------------------------------------
static class MySigner
{
    private static X509Certificate2 _cert;

    public static void Init(X509Certificate2 cert) => _cert = cert;

    public static byte[] Sign(byte[] hash, HashAlgorithmName algorithm)
    {
        using RSA rsa = _cert.GetRSAPrivateKey()
            ?? throw new InvalidOperationException("RSA private key not available.");

        return rsa.SignHash(hash, algorithm, RSASignaturePadding.Pkcs1);
    }
}

// ------------------------------------------------------------
// Main program
// ------------------------------------------------------------
class Program
{
    static X509Certificate2 LoadCertificate(string path, string password)
    {
        try
        {
            var cert = new X509Certificate2(path, password,
                X509KeyStorageFlags.MachineKeySet |
                X509KeyStorageFlags.PersistKeySet |
                X509KeyStorageFlags.Exportable);

            if (!cert.HasPrivateKey)
                throw new InvalidOperationException("Certificate lacks a private key.");

            return cert;
        }
        catch (Exception ex) when (ex is CryptographicException || ex is IOException)
        {
            Console.Error.WriteLine($"Failed to load certificate: {ex.Message}");
            throw;
        }
    }

    static void Main()
    {
        // 1️⃣ Path & password
        string certPath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "certificate.pfx");
        string certPassword = "yourPassword";

        // 2️⃣ Load the cert
        X509Certificate2 cert = LoadCertificate(certPath, certPassword);
        MySigner.Init(cert);

        // 3️⃣ Create PKCS7 signer (replace with your library's class)
        var pkcs7Signer = new PKCS7Detached(cert)
        {
            CustomSignHash = (hash, _) => MySigner.Sign(hash, HashAlgorithmName.SHA256)
        };

        // 4️⃣ Data to sign
        string dataFile = "sample.txt";
        byte[] data = File.ReadAllBytes(dataFile);

        // 5️⃣ Generate detached signature
        byte[] signature = pkcs7Signer.Sign(data);
        File.WriteAllBytes

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}