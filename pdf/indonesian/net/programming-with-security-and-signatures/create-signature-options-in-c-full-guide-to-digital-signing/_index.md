---
category: general
date: 2026-08-14
description: Buat opsi tanda tangan di C# untuk menerapkan tanda tangan digital. Pelajari
  cara mengkonfigurasi tanda tangan, mengimplementasikan fungsi hash khusus, dan menandatangani
  dokumen secara programatis.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create signature options
- custom hash function
- apply digital signature
- how to sign document
- how to configure signature
language: id
lastmod: 2026-08-14
og_description: Buat opsi tanda tangan di C# dan terapkan tanda tangan digital. Tutorial
  ini memandu Anda melalui konfigurasi tanda tangan, menambahkan fungsi hash khusus,
  dan menandatangani dokumen.
og_image_alt: Code editor view showing C# creation of signature options and document
  signing
og_title: Buat opsi tanda tangan di C# – panduan penandatanganan digital langkah demi
  langkah
schemas:
- author: GroupDocs
  dateModified: '2026-08-14'
  description: Create signature options in C# to apply digital signature. Learn how
    to configure signature, implement a custom hash function, and sign documents programmatically.
  headline: Create signature options in C# – full guide to digital signing
  type: TechArticle
- description: Create signature options in C# to apply digital signature. Learn how
    to configure signature, implement a custom hash function, and sign documents programmatically.
  name: Create signature options in C# – full guide to digital signing
  steps:
  - name: '**Hash calculation** – now delegated to your custom hash function.'
    text: '**Hash calculation** – now delegated to your custom hash function.'
  - name: '**Signature generation** – using the private key supplied to the library’s
      configuration.'
    text: '**Signature generation** – using the private key supplied to the library’s
      configuration.'
  - name: '**Embedding** – the generated signature is attached to the output file.'
    text: '**Embedding** – the generated signature is attached to the output file.'
  type: HowTo
tags:
- digital signature
- C#
- security
title: Buat opsi tanda tangan di C# – panduan lengkap untuk penandatanganan digital
url: /id/net/programming-with-security-and-signatures/create-signature-options-in-c-full-guide-to-digital-signing/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat opsi tanda tangan di C# – panduan lengkap untuk penandatanganan digital

Buat opsi tanda tangan di C# untuk mengonfigurasi alur kerja tanda tangan digital. Tutorial ini menunjukkan cara menerapkan tanda tangan digital, mengimplementasikan fungsi hash khusus, dan menandatangani dokumen menggunakan kelas `SignatureOptions`. Jika Anda pernah perlu menandatangani PDF, XML, atau payload biner apa pun dari aplikasi .NET, langkah‑langkah di bawah ini memberikan solusi siap‑jalankan.

Anda akan belajar cara:

* mengonfigurasi `SignatureOptions` dengan algoritma hash khusus,
* memanggil metode penandatanganan dengan benar,
* memverifikasi bahwa tanda tangan telah diterapkan,
* menghindari jebakan umum saat mengonfigurasi tanda tangan.

Prasyarat satu-satunya adalah .NET SDK terbaru (≥ .NET 6) dan perpustakaan penandatanganan yang menyediakan `SignatureOptions` (misalnya, **GroupDocs.Signature**, **Aspose.Signature**, atau API serupa). Tidak diperlukan alat eksternal.

---

## Prasyarat

| Persyaratan | Mengapa penting |
|-------------|-----------------|
| .NET 6 SDK atau lebih baru | Menyediakan fitur bahasa modern yang digunakan dalam contoh. |
| Paket NuGet perpustakaan penandatanganan (misalnya, `GroupDocs.Signature`) | Menyediakan tipe `SignatureOptions` dan metode ekstensi `Sign`. |
| Akses ke kunci pribadi atau sertifikat | Diperlukan untuk menghasilkan tanda tangan digital yang dapat diverifikasi. |

Instal perpustakaan dengan CLI standar:

```bash
dotnet add package GroupDocs.Signature
```

---

## Langkah 1: Buat opsi tanda tangan

Langkah pertama adalah menginstansiasi `SignatureOptions` dan mengatur properti yang mengontrol proses penandatanganan. Objek ini memberi tahu perpustakaan *apa* yang harus ditandatangani dan *bagaimana* menandatanganinya.

```csharp
using GroupDocs.Signature;
using GroupDocs.Signature.Options;

// Create a new SignatureOptions instance
var signatureOptions = new SignatureOptions
{
    // The signing algorithm (e.g., RSA‑SHA256) is defined by the library.
    // You can also set visual appearance, page number, etc., here.
    // For this tutorial we focus on the custom hash function.
};
```

**Mengapa ini penting:** `SignatureOptions` berfungsi sebagai kontrak antara kode Anda dan mesin penandatanganan. Dengan mengonfigurasinya di awal, Anda menghindari boilerplate berulang saat menandatangani banyak dokumen.

---

## Langkah 2: Implementasikan fungsi hash khusus

Fungsi *hash khusus* memberi Anda kontrol penuh atas digest yang ditandatangani oleh algoritma tanda tangan. Ini berguna ketika hash default (SHA‑256) tidak memenuhi persyaratan kepatuhan atau ketika Anda perlu melakukan hash pada subset dokumen.

```csharp
using System.Security.Cryptography;
using System.Text;

// Define a delegate that matches the library’s expected signature
Func<byte[], byte[]> MyHash = data =>
{
    // Example: compute SHA‑512 and then truncate to 256 bits
    using var sha512 = SHA512.Create();
    var fullHash = sha512.ComputeHash(data);

    // Truncate to the first 32 bytes (256 bits)
    var truncated = new byte[32];
    Buffer.BlockCopy(fullHash, 0, truncated, 0, truncated.Length);
    return truncated;
};

// Attach the custom hash to the options
signatureOptions.CustomSignHash = hash => MyHash(hash);
```

**Mengapa ini penting:** Dengan menetapkan `CustomSignHash`, Anda menggantikan langkah hashing internal perpustakaan dengan `MyHash`. Mesin penandatanganan kini akan menandatangani byte yang dikembalikan oleh fungsi Anda, memastikan kepatuhan dengan kebijakan khusus apa pun.

---

## Langkah 3: Muat dokumen dan terapkan tanda tangan digital

Dengan opsi yang telah disiapkan, Anda kini dapat membuka file target dan memanggil metode penandatanganan. Metode `Sign` disediakan oleh perpustakaan dan menggunakan `SignatureOptions` yang telah dikonfigurasi.

```csharp
using System.IO;

// Path to the file you want to sign
string inputPath = @"C:\Docs\contract.pdf";
string outputPath = @"C:\Docs\contract.signed.pdf";

// Load the document into the Signature object
using var signature = new Signature(inputPath);

// Sign the document using the previously created options
bool result = signature.Sign(outputPath, signatureOptions);

if (!result)
{
    throw new InvalidOperationException("The document could not be signed.");
}
```

**Mengapa ini penting:** Pemanggilan `Sign` melakukan tiga aksi secara internal:

1. **Perhitungan hash** – kini didelegasikan ke fungsi hash khusus Anda.
2. **Pembuatan tanda tangan** – menggunakan kunci pribadi yang disediakan dalam konfigurasi perpustakaan.
3. **Penyisipan** – tanda tangan yang dihasilkan dilampirkan ke file output.

Jika ada langkah yang gagal, metode akan mengembalikan `false`, memungkinkan Anda menangani kesalahan dengan elegan.

---

## Langkah 4: Verifikasi bahwa dokumen telah ditandatangani

Verifikasi cepat memastikan bahwa tanda tangan telah diterapkan dengan benar. Sebagian besar perpustakaan menyediakan metode `Verify` yang memeriksa integritas file yang ditandatangani.

```csharp
using var verifier = new Signature(outputPath);
var verificationResult = verifier.Verify();

Console.WriteLine(verificationResult
    ? "Signature verified successfully."
    : "Signature verification failed.");
```

**Mengapa ini penting:** Verifikasi memastikan bahwa dokumen yang ditandatangani tidak diubah setelah penandatanganan dan bahwa hash khusus menghasilkan digest yang kompatibel.

---

## Cara mengonfigurasi tanda tangan untuk berbagai jenis file

Objek `SignatureOptions` yang sama dapat digunakan kembali untuk PDF, dokumen Word, gambar, atau file biner biasa. Satu‑satunya perubahan yang diperlukan adalah kelas opsi spesifik (misalnya, `PdfSignatureOptions`, `WordSignatureOptions`). Berikut contoh cepat untuk gambar JPEG:

```csharp
using GroupDocs.Signature.Options;

var imageOptions = new ImageSignatureOptions
{
    // Position the signature on the image
    Left = 100,
    Top = 50,
    Width = 150,
    Height = 50,
    CustomSignHash = hash => MyHash(hash)   // reuse the same custom hash
};

using var imgSignature = new Signature(@"C:\Images\photo.jpg");
imgSignature.Sign(@"C:\Images\photo.signed.jpg", imageOptions);
```

**Mengapa ini penting:** Memahami cara *mengonfigurasi tanda tangan* untuk setiap format memungkinkan Anda memperluas basis kode yang sama ke berbagai jenis dokumen tanpa menulis ulang logika hashing.

---

## Jebakan umum dan praktik terbaik

| Jebakan | Perbaikan yang disarankan |
|---------|---------------------------|
| Lupa mengatur `CustomSignHash` setelah membuat `SignatureOptions` | Tetapkan delegate segera setelah membangun objek opsi. |
| Menggunakan algoritma hash yang tidak didukung oleh sertifikat penandatangan | Verifikasi bahwa penggunaan kunci sertifikat cocok dengan panjang hash (misalnya, RSA‑2048 dengan SHA‑512). |
| Mengabaikan kebutuhan untuk membuang objek `Signature` | Bungkus instance `Signature` dalam blok `using` untuk melepaskan handle file. |
| Menyimpan file yang ditandatangani di atas sumber asli | Selalu tulis ke jalur file baru (`outputPath`) untuk mempertahankan dokumen asli. |

---

## Contoh lengkap yang berfungsi

Berikut adalah program mandiri yang menyatukan semua bagian. Salin ke proyek konsol baru dan jalankan; konsol akan melaporkan keberhasilan atau kegagalan.

```csharp
using System;
using System.IO;
using System.Security.Cryptography;
using GroupDocs.Signature;
using GroupDocs.Signature.Options;

class Program
{
    // Custom hash implementation (SHA‑512 truncated to 256 bits)
    private static byte[] MyHash(byte[] data)
    {
        using var sha512 = SHA512.Create();
        var full = sha512.ComputeHash(data);
        var truncated = new byte[32];
        Buffer.BlockCopy(full, 0, truncated, 0, truncated.Length);
        return truncated;
    }

    static void Main()
    {
        // Paths
        string input = @"C:\Docs\contract.pdf";
        string output = @"C:\Docs\contract.signed.pdf";

        // Step 1: create signature options
        var signatureOptions = new SignatureOptions
        {
            CustomSignHash = hash => MyHash(hash)
        };

        // Step 2: sign the document
        using var signer = new Signature(input);
        bool signed = signer.Sign(output, signatureOptions);
        if (!signed)
        {
            Console.WriteLine("Signing failed.");
            return;
        }

        // Step 3: verify the signature
        using var verifier = new Signature(output);
        bool verified = verifier.Verify();
        Console.WriteLine(verified
            ? "Signature verified successfully."
            : "Signature verification failed.");
    }
}
```

**Output yang diharapkan**

```
Signature verified successfully.
```

Jika konsol mencetak “Signing failed.” atau “Signature verification failed.”, periksa kembali konfigurasi sertifikat dan pastikan hash khusus mengembalikan array byte dengan ukuran yang diharapkan.

---

## Kesimpulan

Anda sekarang tahu cara **membuat opsi tanda tangan** di C#, melampirkan **fungsi hash khusus**, dan **menerapkan tanda tangan digital** ke dokumen apa pun yang didukung. Tutorial ini mencakup siklus hidup lengkap: mengonfigurasi opsi, menandatangani file, dan memverifikasi hasil. Dengan menggunakan kembali instance `SignatureOptions` yang sama, Anda juga dapat **mengonfigurasi tanda tangan** untuk gambar, file Word, atau biner mentah.

---

## Selanjutnya?

* Jelajahi properti tambahan `SignatureOptions` seperti stempel visual, server timestamp, dan rantai sertifikat – ini selaras dengan kata kunci **apply digital signature**.
* Bereksperimen dengan algoritma hash lain (mis., Blake2b) dengan mengganti implementasi di dalam `MyHash`.
* Integrasikan alur penandatanganan ke dalam API web untuk memungkinkan penandatanganan dokumen secara langsung – ekstensi alami dari **how to sign document** dalam arsitektur berbasis layanan.

Silakan sesuaikan kode untuk kebijakan keamanan Anda sendiri, dan bagikan pengalaman Anda di kolom komentar. Selamat menandatangani!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait erat yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Cara Mengubah Bahasa Tanda Tangan PDF dengan Aspose.PDF untuk .NET](/pdf/english/net/digital-signatures/change-pdf-signature-language-aspose-net/)
- [Tutorial Tanda Tangan Digital Aspose Pdf Net](/pdf/german/net/digital-signatures/digital-signature-aspose-pdf-net-tutorial/)
- [Tutorial Tanda Tangan Digital Aspose Pdf Net](/pdf/french/net/digital-signatures/digital-signature-aspose-pdf-net-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}