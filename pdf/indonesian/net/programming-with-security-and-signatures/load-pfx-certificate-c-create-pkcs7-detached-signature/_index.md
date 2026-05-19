---
category: general
date: 2026-03-24
description: Muat sertifikat PFX di C# secara cepat dan aman untuk membuat tanda tangan
  PKCS7 terpisah dari file. Panduan langkah demi langkah dengan kode lengkap dan jebakan.
draft: false
keywords:
- load pfx certificate c#
- create pkcs7 detached signature
- pkcs7 signature from file
- c# pkcs7 signing
- digital signature c#
language: id
og_description: Muat sertifikat PFX dengan C# dan hasilkan tanda tangan PKCS7 terpisah
  dari file. Contoh lengkap dengan penjelasan dan penanganan kasus tepi.
og_title: Muat Sertifikat PFX C# – Buat Tanda Tangan PKCS7 Terpisah
tags:
- C#
- PKCS7
- X509
- Cryptography
title: Muat Sertifikat PFX C# – Buat Tanda Tangan PKCS7 Terpisah
url: /id/net/programming-with-security-and-signatures/load-pfx-certificate-c-create-pkcs7-detached-signature/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Muat Sertifikat PFX C# – Buat PKCS7 Detached Signature

Pernahkah Anda perlu **load a PFX certificate in C#** hanya untuk menandatangani beberapa data, tetapi tidak yakin harus mulai dari mana? Anda bukan satu-satunya—banyak pengembang mengalami hal yang sama ketika pertama kali menyentuh sertifikat X.509 dan PKCS#7.  

Berita baiknya? Dalam tutorial ini Anda akan mendapatkan solusi siap‑jalankan yang **loads a PFX certificate C#**, membuat **PKCS7 detached signature**, dan bahkan menunjukkan cara mengambil tanda tangan dari sebuah file. Tidak ada referensi yang samar, hanya kode konkret dan penjelasan di balik setiap baris.

> **Apa yang akan Anda dapatkan**  
> * Pemahaman yang jelas tentang proses memuat sertifikat.  
> * Contoh lengkap yang dapat dikompilasi yang membuat PKCS7 detached signature.  
> * Tips untuk menangani jebakan umum (kata sandi salah, file tidak ditemukan, ketidaksesuaian algoritma).  

### Prasyarat

- .NET 6.0 atau lebih baru (API yang digunakan merupakan bagian dari pustaka kelas dasar).  
- File `.pfx` yang valid dan kata sandinya.  
- Visual Studio 2022 atau editor apa pun yang Anda suka—tidak memerlukan paket NuGet khusus untuk contoh inti.  

Jika Anda sudah memiliki semuanya, mari kita mulai.

---

## Muat Sertifikat PFX C# – Langkah‑per‑Langkah

Berikut adalah set minimal dari direktif `using` yang Anda perlukan. Simpan di bagian atas file Anda agar kompiler tahu di mana menemukan tipe-tipe tersebut.

```csharp
using System;
using System.IO;
using System.Security.Cryptography;
using System.Security.Cryptography.X509Certificates;
```

### 1️⃣ Tentukan jalur sertifikat dan kata sandi

Pertama, beri tahu runtime di mana letak file `.pfx` dan apa kata sandinya. Menuliskan jalur secara hard‑coding boleh untuk demo, tetapi **never** menyematkan kata sandi dalam kode produksi.

```csharp
// Step 1: Path to your certificate and its password
string certificatePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "certificate.pfx");
string certificatePassword = "yourPassword"; // <-- replace with a secure source
```

> **Pro tip:** Simpan kata sandi di Azure Key Vault, AWS Secrets Manager, atau variabel lingkungan—**never** commit it to source control.

### 2️⃣ Muat sertifikat dengan aman

Kami membungkus proses pemuatan dalam blok `try / catch` untuk menampilkan kesalahan umum seperti file tidak ditemukan atau kata sandi yang salah.

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

### 3️⃣ Buat objek **PKCS7 detached signature**

Dengan asumsi Anda menggunakan pustaka pihak ketiga yang menyediakan kelas `PKCS7Detached` (banyak SDK komersial melakukannya), kami menginstansiasikannya dengan sertifikat yang baru saja dimuat.

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

> **Why a callback?** Beberapa SDK memungkinkan Anda menghubungkan hardware security modules (HSM) atau layanan penandatanganan jarak jauh. Dengan mengekspos `CustomSignHash`, Anda menjaga logika penandatanganan tetap fleksibel.

### 4️⃣ Implementasikan delegasi penandatanganan

Berikut implementasi sederhana yang menggunakan kunci privat dari sertifikat yang dimuat. Ganti `MySigner.Sign` dengan panggilan HSM Anda sendiri jika diperlukan.

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

### 5️⃣ Tanda tangani data arbitrer dan ambil blob PKCS7 terpisah

Sekarang kita benar‑benar menandatangani sesuatu. Data tersebut bisa berupa file, payload JSON, atau apa pun yang perlu Anda lindungi.

```csharp
// Step 5: Data you want to protect
byte[] dataToSign = File.ReadAllBytes("sample.txt");

// The PKCS7Detached class usually offers a Sign method that returns the raw signature.
byte[] detachedSignature = pkcs7Signer.Sign(dataToSign);

// Save the signature to disk for later verification
File.WriteAllBytes("sample.txt.sig", detachedSignature);

Console.WriteLine("Detached PKCS7 signature created successfully.");
```

**Output yang Diharapkan**

```
Detached PKCS7 signature created successfully.
```

Anda kini memiliki **PKCS7 signature from file** (`sample.txt.sig`) yang dapat diverifikasi secara independen dari data asli.

## Buat PKCS7 Detached Signature – Opsi Lanjutan

Meskipun alur dasar berfungsi untuk kebanyakan skenario, sistem produksi sering memerlukan pengaturan tambahan:

| Fitur | Cara mengaktifkan | Kapan digunakan |
|-------|-------------------|-----------------|
| **Pemilihan algoritma** | Pass `HashAlgorithmName.SHA256` (or SHA384/SHA512) to `SignHash` | Jika regulasi kepatuhan Anda mewajibkan hash tertentu |
| **Timestamping** | Append a RFC‑3161 timestamp after the signature | Untuk validasi jangka panjang |
| **Multiple signers** | Create additional `PKCS7Detached` instances and merge | Ketika dokumen memerlukan co‑signing |
| **Custom CMS attributes** | Use the library’s `AddAttribute` method before `Sign` | Untuk menyematkan waktu penandatanganan, ID penandatangan, dll. |

Berikut cuplikan cepat yang menunjukkan pemilihan SHA‑256:

```csharp
CustomSignHash = (hash, _) => MySigner.Sign(hash, HashAlgorithmName.SHA256)
```

## Verifikasi PKCS7 Detached Signature (Opsional)

Verifikasi adalah setengah cerita yang lain. Sebagian besar pustaka menyediakan metode `Verify` yang menerima data asli dan tanda tangan terpisah.

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

Jika Anda menggunakan SDK yang berbeda, cari kelas `CmsSignedData` atau `SignedCms` di namespace .NET `System.Security.Cryptography.Pkcs`—kelas tersebut juga dapat menangani tanda tangan terpisah.

## Kesalahan Umum & Cara Menghindarinya

1. **Wrong password** – `CryptographicException` akan menampilkan *“The specified network password is not correct.”* Simpan kata sandi dengan aman dan uji secara terpisah sebelum memuat sertifikat.  
2. **Certificate without a private key** – Beberapa file `.pfx` diekspor tanpa kunci privat. Periksa kembali pengaturan ekspor di CA atau Key Vault Anda.  
3. **Algorithm mismatch** – Jika penandatangan mengharapkan SHA‑256 tetapi Anda memberikan SHA-1, verifikasi akan gagal. Selaraskan algoritma di antara langkah penandatanganan dan verifikasi.  
4. **File path issues** – Jalur relatif berfungsi dalam pengembangan tetapi gagal saat dideploy. Lebih baik gunakan `Path.Combine(AppDomain.CurrentDomain.BaseDirectory, ...)` atau jalur absolut yang dikonfigurasi.  
5. **Platform differences** – Windows dan Linux menangani penyimpanan kunci privat secara berbeda. Menggunakan `X509KeyStorageFlags.Exportable` mengurangi sebagian besar masalah lintas‑platform.  

## Contoh Lengkap yang Berfungsi (Siap Salin‑Tempel)

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