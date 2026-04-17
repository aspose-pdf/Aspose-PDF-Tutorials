---
category: general
date: 2026-03-27
description: Tambahkan tanda tangan digital PDF di C# menggunakan sertifikat PFX –
  pelajari cara menandatangani PDF dengan sertifikat, membuat tanda tangan PKCS7 terpisah,
  dan memuat dokumen PDF di C#.
draft: false
keywords:
- add digital signature pdf
- sign pdf with certificate
- create pkcs7 detached signature
- load pdf document c#
- sign pdf using pfx
language: id
og_description: Tambahkan tanda tangan digital PDF di C# dengan sertifikat PFX. Panduan
  ini menunjukkan cara menandatangani PDF dengan sertifikat, membuat tanda tangan
  terpisah PKCS7, dan lainnya.
og_title: Tambahkan Tanda Tangan Digital pada PDF di C# – Tutorial Langkah demi Langkah
tags:
- pdf
- csharp
- digital-signature
title: Menambahkan Tanda Tangan Digital pada PDF di C# – Panduan Lengkap
url: /id/net/digital-signatures/add-digital-signature-pdf-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Menambahkan Tanda Tangan Digital PDF di C# – Panduan Lengkap

Pernahkah Anda perlu **add digital signature PDF** dalam proyek .NET tetapi tidak yakin harus mulai dari mana? Anda bukan satu-satunya – banyak pengembang mengalami hal yang sama ketika pertama kali mencoba menandatangani PDF dengan sertifikat. Kabar baik? Ini cukup sederhana setelah Anda memiliki semua komponen yang tepat, dan Anda akan dapat **sign PDF with certificate** dalam hanya beberapa baris kode.

Dalam tutorial ini kami akan menelusuri cara memuat dokumen PDF di C#, membuat tanda tangan PKCS#7 terpisah dari file `.pfx`, dan akhirnya menerapkan tanda tangan tersebut sehingga file yang dihasilkan dapat diverifikasi di semua penampil PDF. Pada akhir tutorial Anda akan memiliki contoh yang dapat dijalankan yang dapat Anda masukkan ke dalam solusi Anda sendiri, serta beberapa tips untuk menangani kasus tepi yang umum.

## Apa yang Anda Butuhkan

- **Aspose.PDF for .NET** (versi 23.9 atau lebih baru). Perpustakaan ini bersifat komersial, tetapi ada versi percobaan gratis yang dapat Anda gunakan untuk pengujian.
- Sebuah **code‑signing certificate** dalam format `.pfx` beserta kata sandinya.
- .NET 6+ (atau .NET Framework 4.7+). API ini bekerja pada keduanya, tetapi contoh ditargetkan ke .NET 6 untuk sintaks modern.
- Sebuah IDE seperti Visual Studio 2022 – meskipun editor apa pun yang dapat mengompilasi C# juga dapat digunakan.

Itu saja. Tidak ada paket NuGet tambahan selain Aspose.PDF, tidak ada file konfigurasi yang rumit. Mari kita mulai.

![Contoh menambahkan tanda tangan digital PDF](image-placeholder.png "Add digital signature PDF example")

## Langkah 1 – Memuat Dokumen PDF C# (Dasar)

Sebelum Anda dapat menandatangani apa pun, Anda memerlukan objek PDF di memori. Kelas `Document` milik Aspose.PDF mewakili seluruh file, dan Anda dapat membungkusnya dalam blok `using` sehingga sumber daya dilepaskan secara otomatis.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Facades;
using Aspose.Pdf.Signatures;
using System;

// Step 1: Load the PDF you want to sign
string sourcePath = @"C:\Docs\toSign.pdf";

using var pdfDocument = new Document(sourcePath);
```

**Mengapa ini penting:**  
Memuat dokumen memberi Anda akses ke halaman‑halamannya, metadata, dan, yang paling penting, kemampuan untuk menyematkan tanda tangan digital. Pernyataan `using` memastikan handle file ditutup bahkan jika terjadi pengecualian – kebiasaan kecil namun penting untuk kode produksi.

## Langkah 2 – Menyiapkan Tanda Tangan PKCS#7 Terpisah (Buat Tanda Tangan PKCS7 Terpisah)

Tanda tangan PKCS#7 terpisah berisi hash kriptografis dari PDF tetapi tidak menyertakan PDF itu sendiri. Hal ini menjaga ukuran file asli tetap utuh dan persis seperti yang diharapkan kebanyakan penampil PDF.

```csharp
using System.Security.Cryptography;

// Step 2: Build the PKCS#7 signature object
string certPath = @"C:\Certs\myCertificate.pfx";
string certPassword = "SuperSecret123";

var pkcs7 = new PKCS7Detached(certPath, certPassword, DigestHashAlgorithm.Sha512);
```

**Mengapa SHA‑512?**  
SHA‑512 menawarkan ketahanan tabrakan yang lebih kuat dibandingkan SHA‑256 sekaligus tetap didukung secara luas. Jika Anda memerlukan kompatibilitas dengan pembaca lama, Anda dapat beralih ke `DigestHashAlgorithm.Sha256` – cukup ubah nilai enum‑nya.

## Langkah 3 – Menentukan Lokasi Tanda Tangan (Tandatangani PDF Menggunakan PFX)

Sebagian besar perusahaan menginginkan bidang tanda tangan yang terlihat pada halaman pertama. Aspose.PDF memungkinkan Anda menentukan sebuah persegi panjang dalam satuan point (1 pt ≈ 1/72 in). Koordinat dimulai dari sudut kiri‑bawah halaman.

```csharp
// Step 3: Create a visible signature rectangle
var signatureRect = new Rectangle(100, 100, 200, 150); // left, bottom, right, top
```

**Tip:**  
Jika Anda lebih suka tanda tangan yang tidak terlihat, berikan `isVisible: false` ke metode `Sign` nanti. Tanda tangan tak terlihat berguna untuk pemrosesan batch di mana petunjuk visual tidak diperlukan.

## Langkah 4 – Menerapkan Tanda Tangan (Tandatangani PDF dengan Sertifikat)

Sekarang kita menggabungkan semuanya. Fasade `PdfFileSignature` menangani mekanisme penandatanganan PDF tingkat rendah, sementara kami memberi tahu nomor halaman, flag visibilitas, persegi panjang, dan objek PKCS#7 kami.

```csharp
// Step 4: Sign the PDF
using var pdfSigner = new PdfFileSignature(pdfDocument);

pdfSigner.Sign(
    pageNumber: 1,
    isVisible: true,
    signatureRect,
    pkcs7);
```

**Apa yang terjadi di balik layar?**  
Aspose.PDF membuat `SigField` pada halaman yang ditentukan, menulis hash dari seluruh dokumen, mengenkripsi hash tersebut dengan kunci pribadi dari file `.pfx` Anda, dan akhirnya menyematkan struktur PKCS#7 yang dihasilkan ke dalam kamus `/AcroForm` PDF. Hasilnya adalah tanda tangan digital yang sesuai standar dan dapat dikenali oleh Adobe Acrobat, Foxit, serta penampil PDF di browser.

## Langkah 5 – Menyimpan PDF yang Ditandatangani (Tandatangani PDF Menggunakan PFX – Langkah Akhir)

Dokumen yang ditandatangani tidak berguna jika Anda tidak menyimpannya. Pilih nama file baru untuk menghindari menimpa file asli – terutama saat pengujian.

```csharp
// Step 5: Persist the signed PDF
string signedPath = @"C:\Docs\Signed.pdf";
pdfSigner.Save(signedPath);

Console.WriteLine($"PDF signed successfully! Saved to: {signedPath}");
```

Saat Anda membuka `Signed.pdf` di penampil, Anda seharusnya melihat panel tanda tangan yang menunjukkan tanda tangan valid (asalkan rantai sertifikat dipercaya di mesin).

## Contoh Kerja Penuh (Semua Langkah dalam Satu File)

Menggabungkan semua langkah memudahkan penyalinan‑tempel ke dalam aplikasi konsol.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Facades;
using Aspose.Pdf.Signatures;

class Program
{
    static void Main()
    {
        // Paths – adjust to your environment
        string sourcePdf = @"C:\Docs\toSign.pdf";
        string certFile = @"C:\Certs\myCertificate.pfx";
        string certPass = "SuperSecret123";
        string outputPdf = @"C:\Docs\Signed.pdf";

        // Load the PDF
        using var pdfDoc = new Document(sourcePdf);

        // Prepare the PKCS#7 detached signature (create pkcs7 detached signature)
        var pkcs7 = new PKCS7Detached(certFile, certPass, DigestHashAlgorithm.Sha512);

        // Define a visible signature rectangle
        var rect = new Rectangle(100, 100, 200, 150);

        // Sign the document (sign pdf with certificate)
        using var signer = new PdfFileSignature(pdfDoc);
        signer.Sign(pageNumber: 1, isVisible: true, rect, pkcs7);

        // Save the signed PDF (sign pdf using pfx)
        signer.Save(outputPdf);

        Console.WriteLine($"Signed PDF saved to: {outputPdf}");
    }
}
```

### Hasil yang Diharapkan

- **Visual cue:** Sebuah kotak persegi panjang biru muncul di halaman 1 tempat tanda tangan berada.
- **Signature panel:** Membuka file di Adobe Reader menampilkan “Signed and all signatures are valid.”
- **File size:** PDF yang ditandatangani hanya beberapa kilobyte lebih besar daripada yang asli – berkat sifat terpisah dari payload PKCS#7.

## Pertanyaan Umum & Kasus Tepi

### Bagaimana jika sertifikat tidak dipercaya?

Jika penampil melaporkan “Signature is unknown” Anda mungkin perlu menginstal sertifikat CA penerbit di mesin atau mengonfigurasi trust store di lingkungan penyebaran Anda. Untuk lingkungan pengujian, Anda dapat menandatangani sendiri sertifikat, tetapi ingat bahwa pengguna produksi akan memerlukan sertifikat dari otoritas yang terpercaya.

### Bisakah saya menandatangani beberapa halaman?

Tentu saja. Panggil `pdfSigner.Sign` untuk setiap halaman yang ingin Anda beri bidang terlihat, atau gunakan instance `PKCS7Detached` yang sama untuk menerapkan tanda tangan tak terlihat yang mencakup seluruh dokumen. Pastikan Anda tidak menimpa bidang tanda tangan yang sudah ada dengan nama yang sama.

### Bagaimana cara menangani PDF besar secara efisien?

Aspose.PDF melakukan streaming dokumen, sehingga penggunaan memori tetap rendah. Namun, jika Anda memproses ribuan file dalam batch, pertimbangkan untuk menggunakan kembali objek `PKCS7Detached` (objek ini thread‑safe) dan memparalelkan loop penandatanganan dengan `Parallel.ForEach`.

### Bagaimana dengan kepatuhan PDF/A?

Ketika Anda memerlukan kepatuhan PDF/A‑1b atau PDF/A‑2b, atur properti `PdfAConformanceLevel` pada `PdfFileSignature` sebelum menandatangani. Ini memberi tahu perpustakaan untuk menyematkan profil ICC dan metadata yang diperlukan, memastikan file yang ditandatangani tetap kompatibel dengan PDF/A.

## Tips Pro (Dari Pengalaman Saya)

- **Pro tip:** Selalu simpan salinan PDF asli. Meskipun penandatanganan bersifat non‑destructive, persegi panjang yang salah konfigurasi dapat membuat tanda tangan tidak terlihat atau ditempatkan secara aneh.
- **Watch out for:** Menggunakan algoritma hash lemah (MD5) akan menyebabkan penampil modern menandai tanda tangan sebagai tidak aman. Gunakan SHA‑256 atau SHA‑512.
- **Performance tip:** Jika Anda hanya memerlukan tanda tangan tak terlihat, set `isVisible: false`. Ini melewatkan proses rendering bidang formulir dan dapat menghemat beberapa milidetik pada pekerjaan batch besar.
- **Debugging:** Aspose.PDF menulis log detail jika Anda mengaktifkan `Aspose.Pdf.Logging`. Aktifkan saat Anda memecahkan masalah rantai sertifikat.

## Kesimpulan

Anda baru saja belajar cara **add digital signature PDF** di C# menggunakan sertifikat PFX, mulai dari memuat dokumen hingga membuat tanda tangan PKCS#7 terpisah dan akhirnya menyimpan file yang ditandatangani. Contoh lengkap yang dapat dijalankan di atas seharusnya berfungsi langsung, dan tips tambahan akan membantu Anda menghindari jebakan paling umum.

Siap untuk langkah selanjutnya? Cobalah menandatangani PDF dalam sebuah web API sehingga pengguna dapat mengunggah dokumen dan menerima salinan yang ditandatangani secara instan, atau jelajahi layanan timestamping untuk menyematkan sumber waktu terpercaya ke dalam tanda tangan Anda. Kedua topik tersebut secara alami memperluas konsep **sign PDF with certificate** dan **create PKCS7 detached signature** yang dibahas di sini.

Ada pertanyaan atau menemukan kendala? Tinggalkan komentar, dan selamat coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}