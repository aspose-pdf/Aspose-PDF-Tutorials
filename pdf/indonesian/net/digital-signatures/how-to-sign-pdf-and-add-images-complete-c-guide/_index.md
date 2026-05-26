---
category: general
date: 2026-03-29
description: Cara menandatangani PDF dengan tanda tangan digital dan menambahkan gambar
  yang dipotong di C#. Pelajari cara menambahkan tanda tangan digital pada PDF, memotong
  gambar untuk PDF, dan menambahkan gambar ke PDF dengan mudah.
draft: false
keywords:
- how to sign pdf
- add digital signature pdf
- crop image for pdf
- add image to pdf
- digital signature pdf page
language: id
og_description: Cara menandatangani PDF dengan tanda tangan digital dan menyisipkan
  gambar yang dipotong menggunakan Aspose.Pdf di C#. Ikuti panduan ini untuk solusi
  lengkap.
og_title: Cara Menandatangani PDF dan Menambahkan Gambar – Tutorial C# Langkah demi
  Langkah
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Cara Menandatangani PDF dan Menambahkan Gambar – Panduan Lengkap C#
url: /id/net/digital-signatures/how-to-sign-pdf-and-add-images-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Menandatangani PDF dan Menambahkan Gambar – Panduan Lengkap C#

Pernah bertanya-tanya **cara menandatangani PDF** secara programatis sambil menyisipkan gambar khusus? Mungkin Anda sedang membangun alur kerja persetujuan dan memerlukan tanda tangan yang sah secara hukum *dan* thumbnail foto penandatangan pada halaman yang sama. Singkatnya, Anda ingin **menambahkan digital signature pdf** ke konten, memotong gambar tersebut, dan kemudian **menambahkan gambar ke pdf** tanpa kesulitan.  

Tutorial ini memandu Anda melalui setiap langkah—dari memuat sertifikat ECDSA PKCS#7 hingga memotong JPEG dan menempelkannya ke halaman yang ditandatangani. Pada akhir tutorial Anda akan memiliki satu file C# yang dapat dijalankan yang menandatangani halaman 1, memotong foto menjadi 400 × 400 px, dan menempatkannya pada lokasi yang tepat. Tanpa skrip eksternal, tanpa sulap, hanya kode yang jelas dan penjelasan.

## Prasyarat

- .NET 6.0 atau lebih baru (kode ini juga berfungsi dengan .NET Framework 4.7+)
- **Aspose.Pdf for .NET** paket NuGet (versi 23.9 atau lebih baru)
- Sertifikat ECDSA P‑256 dalam format PKCS#7 (`.pfx`) dan kata sandinya
- Gambar JPEG yang ingin Anda sematkan (misalnya `photo.jpg`)

> **Tips profesional:** Simpan file sertifikat Anda di luar kontrol sumber dan lindungi kata sandi dengan manajer rahasia.

---

## Langkah 1: Siapkan Proyek dan Impor

Pertama, buat aplikasi console (atau integrasikan ini ke dalam layanan yang sudah ada). Tambahkan referensi Aspose.Pdf:

```bash
dotnet add package Aspose.Pdf
```

Kemudian sertakan namespace yang diperlukan:

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Forms;
using Aspose.Pdf.Drawing;
```

Pernyataan `using` ini memberi Anda akses ke kelas `Document`, `Signature`, dan `Rectangle` yang akan kita perlukan nanti.

## Langkah 2: Muat PDF dan Siapkan Tanda Tangan

Kami akan membuka PDF yang sudah ada (`source.pdf`) dan membuat objek **digital signature pdf** yang menggunakan tanda tangan PKCS#7 terpisah. Sertifikat tersebut adalah kunci ECDSA P‑256, yang secara luas diterima untuk kepatuhan.

```csharp
// Load the PDF you want to sign
var doc = new Document("YOUR_DIRECTORY/source.pdf");

// Initialize the signature appearance (optional but recommended)
var signature = new Signature(doc);
signature.Contact = "John Doe";
signature.Location = "New York, USA";
signature.Reason = "Document approval";

// Load the PKCS#7 certificate (ECDSA P‑256) for signing
var pkcsSignature = new PKCS7Detached(
    "YOUR_DIRECTORY/ecdsa.pfx",   // certificate file
    "YOUR_PASSWORD");             // certificate password
```

**Mengapa ini penting:** Menggunakan tanda tangan PKCS#7 terpisah menjaga konten PDF asli tetap utuh sambil menyematkan hash kriptografis. Ini adalah pendekatan standar industri untuk PDF yang sah secara hukum.

## Langkah 3: Terapkan Tanda Tangan Digital ke Halaman Tertentu

Sekarang kami akan menempatkan bidang tanda tangan yang terlihat pada **halaman 1**. Persegi panjang menentukan di mana kotak tanda tangan muncul (koordinat dalam poin, di mana 1 inci = 72 poin).

```csharp
// Apply the digital signature to page 1, covering a rectangular area
signature.Sign(
    pageNumber: 1,
    isVisible: true,
    signatureRect: new Rectangle(100, 100, 300, 300),
    pkcsSignature);
```

Jika Anda tidak memerlukan kotak yang terlihat, setel `isVisible` ke `false`. `signatureRect` dapat disesuaikan agar cocok dengan tata letak dokumen Anda.

## Langkah 4: Buka Stream Gambar dan Tentukan Area Pemotongan

Kami akan membaca file JPEG ke dalam stream dan menentukan **source rectangle** yang memilih 400 × 400 piksel bagian kiri‑atas. Ini adalah operasi **crop image for pdf**.

```csharp
// Open the image file that will be added to the PDF
using var imageStream = File.OpenRead("YOUR_DIRECTORY/photo.jpg");

// Define the source rectangle that selects the portion to crop (0‑400 pixels)
var sourceRect = new Rectangle(0, 0, 400, 400);
```

> **Kasus tepi:** Jika gambar Anda lebih kecil dari 400 × 400, pemotongan akan otomatis menyesuaikan dengan dimensi sebenarnya—tidak ada pengecualian yang dilempar.

## Langkah 5: Tentukan Lokasi Gambar yang Dipotong

Selanjutnya, atur **destination rectangle** pada halaman PDF. Pada contoh ini kami menempatkan gambar pada (50, 50) dengan ukuran 200 × 200 poin (≈2,78 inci persegi).

```csharp
// Define the destination rectangle where the cropped image will be placed on the page
var destinationRect = new Rectangle(50, 50, 200, 200);
```

Silakan bereksperimen: ubah koordinat X/Y untuk memindahkan gambar, atau sesuaikan lebar/tinggi untuk skala.

## Langkah 6: Sisipkan Gambar yang Dipotong ke Halaman yang Ditandatangani

Akhirnya, kami menambahkan gambar ke **halaman 1** (halaman yang sama yang kini membawa tanda tangan). Overload `AddImage` yang kami gunakan menerima source dan destination rectangle, secara efektif melakukan pemotongan dan penempatan dalam satu panggilan.

```csharp
// Insert the cropped image onto page 1 at the specified location
doc.Pages[1].AddImage(imageStream, sourceRect, destinationRect);
```

Di balik layar, Aspose.Pdf mengekstrak wilayah 400 × 400 piksel, mengubah skalanya menjadi 200 × 200 poin, dan menuliskannya ke dalam stream konten PDF.

## Langkah 7: Simpan PDF yang Ditandatangani dan Ditingkatkan dengan Gambar

Setelah semua modifikasi, simpan dokumen. Anda dapat menimpa file asli atau menulis ke file baru.

```csharp
// Save the final document
doc.Save("YOUR_DIRECTORY/output_signed.pdf");
Console.WriteLine("PDF signed and image added successfully!");
```

Saat Anda membuka `output_signed.pdf` di Adobe Acrobat atau penampil PDF apa pun, Anda akan melihat:

- Bidang tanda tangan yang terlihat pada koordinat yang Anda tentukan.
- Foto yang dipotong ditempatkan pada (50, 50) di halaman 1.
- Tanda tangan digital tervalidasi (asalkan penampil mempercayai sertifikat Anda).

---

## Pertanyaan yang Sering Diajukan (FAQ)

| Question | Answer |
|----------|--------|
| **Bisakah saya menandatangani halaman yang berbeda?** | Ubah argumen `pageNumber` pada `signature.Sign` ke indeks halaman yang valid (berbasis 1). |
| **Bagaimana jika saya memerlukan beberapa tanda tangan?** | Buat instance `Signature` baru untuk setiap halaman atau lokasi, gunakan kembali `pkcsSignature` yang sama jika sertifikat yang sama berlaku. |
| **Apakah pemotongan gambar terbatas pada persegi panjang?** | Ya, `AddImage` milik Aspose.Pdf bekerja dengan wilayah persegi panjang. Untuk bentuk yang kompleks, Anda perlu memproses gambar terlebih dahulu (misalnya, menggunakan System.Drawing) sebelum disematkan. |
| **Bagaimana cara membuat tanda tangan tidak terlihat?** | Setel `isVisible` ke `false` dan hilangkan `signatureRect`. Tanda tangan tetap valid secara kriptografis. |
| **Format apa saja yang dapat saya sematkan selain JPEG?** | PNG, BMP, GIF, dan TIFF semuanya didukung. Cukup ubah jalur file dan pastikan stream membaca byte yang tepat. |

## Contoh Lengkap yang Berfungsi

Berikut adalah program lengkap yang berdiri sendiri. Salin‑tempel ke dalam `Program.cs`, sesuaikan jalur, dan jalankan.

```csharp
// Program.cs
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Forms;
using Aspose.Pdf.Drawing;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source PDF
        var doc = new Document("YOUR_DIRECTORY/source.pdf");

        // 2️⃣ Prepare the digital signature appearance
        var signature = new Signature(doc)
        {
            Contact = "John Doe",
            Location = "New York, USA",
            Reason = "Document approval"
        };

        // 3️⃣ Load the PKCS#7 ECDSA P‑256 certificate
        var pkcsSignature = new PKCS7Detached(
            "YOUR_DIRECTORY/ecdsa.pfx",
            "YOUR_PASSWORD");

        // 4️⃣ Apply a visible signature on page 1
        signature.Sign(
            pageNumber: 1,
            isVisible: true,
            signatureRect: new Rectangle(100, 100, 300, 300),
            pkcsSignature);

        // 5️⃣ Open the image to be added
        using var imageStream = File.OpenRead("YOUR_DIRECTORY/photo.jpg");

        // 6️⃣ Define crop (source) and placement (destination) rectangles
        var sourceRect = new Rectangle(0, 0, 400, 400);      // crop 400×400 px from top‑left
        var destinationRect = new Rectangle(50, 50, 200, 200); // place at (50,50) with 200×200 pt size

        // 7️⃣ Insert the cropped image onto the same page
        doc.Pages[1].AddImage(imageStream, sourceRect, destinationRect);

        // 8️⃣ Save the final PDF
        doc.Save("YOUR_DIRECTORY/output_signed.pdf");
        Console.WriteLine("PDF signed and image added successfully!");
    }
}
```

**Hasil yang diharapkan:** Membuka `output_signed.pdf` menampilkan bidang tanda tangan (100 × 100 → 300 × 300 poin) dan gambar 200 × 200 poin yang diambil dari sudut kiri‑atas `photo.jpg`. Tanda tangan tervalidasi terhadap sertifikat ECDSA yang disediakan.

## Kesimpulan

Kami telah membahas **cara menandatangani PDF** file, cara **menambahkan digital signature pdf** ke halaman tertentu, cara **memotong gambar untuk pdf**, dan akhirnya cara **menambahkan gambar ke pdf** menggunakan Aspose.Pdf di C#. Seluruh alur—dari memuat sertifikat hingga menyimpan dokumen akhir—termasuk dalam satu file sumber yang mudah dibaca.

Jika Anda siap untuk tantangan berikutnya, pertimbangkan:

- Menambahkan **banyak tanda tangan** pada halaman yang berbeda (gunakan konsep “digital signature pdf page”).
- Menyematkan **kode QR** yang menautkan ke layanan verifikasi.
- Mengotomatiskan proses dalam API ASP.NET Core untuk pembuatan PDF secara langsung.

Ingat, kunci otomatisasi PDF yang kuat adalah pemisahan tugas yang jelas: penanganan tanda tangan, pemrosesan gambar, dan perakitan dokumen akhir. Bereksperimenlah dengan koordinat, ganti format gambar, atau coba timestamp—alur kerja Anda kini sepenuhnya dapat diperluas.

Ada pertanyaan, skenario kasus tepi, atau contoh penggunaan menarik untuk dibagikan? Tinggalkan komentar di bawah, dan selamat coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}