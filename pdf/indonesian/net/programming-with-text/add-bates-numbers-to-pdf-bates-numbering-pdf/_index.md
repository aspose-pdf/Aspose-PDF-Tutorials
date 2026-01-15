---
category: general
date: 2026-01-15
description: Tambahkan nomor Bates ke PDF Anda dengan cepat menggunakan Aspose.Pdf.
  Pelajari cara menambahkan footer ke PDF, menambahkan nomor halaman pada PDF, dan
  menambahkan penomoran halaman khusus.
draft: false
keywords:
- add bates numbers
- bates numbering pdf
- add footer to pdf
- add page numbers pdf
- add custom page numbering
language: id
og_description: Tambahkan nomor Bates ke PDF Anda dengan cepat menggunakan Aspose.Pdf.
  Pelajari cara menambahkan footer ke PDF, menambahkan nomor halaman PDF, dan menambahkan
  penomoran halaman khusus.
og_title: Tambahkan Nomor Bates ke PDF – penomoran Bates PDF
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Tambahkan Nomor Bates ke PDF – penomoran bates pdf
url: /id/net/programming-with-text/add-bates-numbers-to-pdf-bates-numbering-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tambahkan Bates Numbers ke PDF – Panduan Lengkap

Pernah perlu **menambahkan bates numbers** ke PDF tetapi tidak yakin harus mulai dari mana? Anda tidak sendirian—tim hukum, auditor, dan siapa saja yang menangani kumpulan dokumen besar menghadapi masalah ini setiap hari. Kabar baik? Dengan Aspose.Pdf untuk .NET Anda dapat menaburkan nomor‑nomor itu ke setiap halaman hanya dengan beberapa baris kode.

Pada tutorial ini kami akan membahas seluruh proses: mulai dari mengimpor library Aspose.Pdf, memuat file sumber Anda, mengonfigurasi *BatesNumberingArtifact*, melampirkannya sebagai footer, dan akhirnya menyimpan hasilnya. Pada akhir tutorial Anda juga akan mengetahui cara **menambahkan footer ke pdf**, **menambahkan nomor halaman pdf**, dan bahkan **menambahkan penomoran halaman khusus** untuk kasus‑kasus rumit.

## Apa yang Anda Butuhkan

- .NET 6+ (atau .NET Framework 4.8 jika Anda masih menggunakan stack klasik)  
- Referensi ke paket NuGet **Aspose.Pdf** (`Install-Package Aspose.Pdf`)  
- File PDF yang ingin Anda beri cap (kami akan menyebutnya `source.pdf`)  

Itu saja—tanpa alat tambahan, tanpa editor PDF yang berat. Mari kita mulai.

![add bates numbers example](https://example.com/images/add-bates-numbers.png "add bates numbers example")

## Langkah 1: Tambahkan Bates Numbers – Muat Dokumen PDF

Pertama, kita memerlukan objek `Document` yang mewakili PDF yang akan dimodifikasi. Anggap ini seperti membuka dokumen Word sebelum mulai mengetik.

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

> **Mengapa ini penting:** Memuat file memberi Anda akses ke koleksi `Pages`‑nya, yang merupakan tempat kami akan melampirkan artefak penomoran Bates nanti. Jika file tidak ditemukan, Aspose akan melempar `FileNotFoundException` yang jelas, jadi periksa kembali jalurnya.

## Langkah 2: Konfigurasikan Pengaturan bates numbering pdf

Sekarang kita menentukan *bagaimana* nomor‑nomor tersebut harus terlihat. `BatesNumberingArtifact` memungkinkan Anda mengatur prefix, nomor awal, padding digit, suffix, dan penempatan. Ini adalah inti dari **bates numbering pdf**.

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

> **Tips pro:** Jika Anda ingin nomor muncul di header, ganti `BottomCenter` dengan `TopCenter`. Enum penempatan juga mendukung `BottomLeft`, `BottomRight`, dll., memberi Anda fleksibilitas untuk gaya **add footer to pdf** yang berbeda.

## Langkah 3: Tambahkan page numbers pdf – Lampirkan Artefak ke Setiap Halaman

Dengan artefak siap, kami melakukan loop melalui setiap halaman dan menambahkannya ke koleksi `Artifacts`. Ini adalah langkah yang sebenarnya **menambahkan page numbers pdf**.

```csharp
// Step 3: Attach the artifact to each page
foreach (Page page in pdfDocument.Pages)
{
    page.Artifacts.Add(batesArtifact);
}
```

> **Apa yang terjadi di balik layar?** Koleksi `Artifacts` dirender setelah konten utama halaman, memastikan nomor Bates berada di atas teks yang ada tetapi di bawah anotasi. Jika Anda ingin nomor berada di belakang konten (jarang), Anda dapat menggunakan `page.Artifacts.Insert(0, batesArtifact)`.

## Langkah 4: Tambahkan custom page numbering – Simpan PDF yang Diperbarui

Akhirnya, kami menulis dokumen yang telah dimodifikasi ke disk. File output akan berisi nomor Bates sebagai bagian permanen setiap halaman.

```csharp
// Step 4: Save the PDF with the new numbering
pdfDocument.Save(@"YOUR_DIRECTORY\bates_out.pdf");

Console.WriteLine("Bates numbers added successfully! Check bates_out.pdf.");
```

> **Tips verifikasi:** Buka `bates_out.pdf` di viewer apa pun. Anda harus melihat sesuatu seperti `CASE-01000-A` terpusat di bagian bawah setiap halaman. Jika nomor tidak muncul, periksa kembali properti `Placement` apakah sesuai dengan lokasi yang diinginkan.

## Contoh Lengkap yang Berfungsi

Menggabungkan semuanya, berikut program lengkap yang siap dijalankan:

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

### Hasil yang Diharapkan

- **File:** `bates_out.pdf` di folder yang sama dengan `source.pdf`
- **Visual:** Teks bottom‑center `CASE-01000-A`, `CASE-01001-A`, … untuk setiap halaman berikutnya
- **Behaviour:** Nomor‑nomor tersebut tertanam secara permanen; mereka tetap ada setelah pencetakan, flattening, dan pengeditan lebih lanjut.

## Variasi Umum & Kasus Edge

| Situation | How to Adjust |
|-----------|---------------|
| **Nomor awal yang berbeda** | Ubah `StartNumber` ke integer apa pun (misalnya, `StartNumber = 500`). |
| **Suffix huruf per volume** | Gunakan loop untuk mengubah `Suffix` per halaman, atau buat beberapa artefak dengan suffix yang berbeda. |
| **Penomoran rata kanan** | Set `Placement = BatesNumberingArtifact.PlacementLocation.BottomRight`. |
| **Dokumen besar (10rb+ halaman)** | Pertimbangkan memproses halaman secara batch atau meningkatkan `NumberDigits` untuk menghindari overflow. |
| **Perlu menyembunyikan nomor pada halaman tertentu** | Lewati halaman‑halaman tersebut dalam loop `foreach` (misalnya, `if (page.Number != 1) page.Artifacts.Add(batesArtifact);`). |

> **Waspada:** Menggunakan `Prefix` atau `Suffix` yang berisi karakter ilegal untuk nama file (misalnya, `*` atau `?`). Aspose tetap akan menyematkannya, tetapi dapat menyebabkan masalah saat Anda mengekstrak teks nanti.

## Tips Pro untuk Penggunaan Produksi

- **Cache artefak** jika Anda memproses banyak PDF secara berurutan; membuatnya sekali menghemat beberapa milidetik per file.  
- **Keamanan thread:** Instansi `BatesNumberingArtifact` tidak thread‑safe, jadi berikan setiap thread salinan tersendiri.  
- **Kinerja:** Untuk batch besar, nonaktifkan kompresi PDF (`pdfDocument.Compress = false`) sebelum menyimpan, lalu aktifkan kembali jika diperlukan.  
- **Pengujian:** Selalu lakukan pemeriksaan visual cepat pada PDF pertama yang dihasilkan untuk memastikan penempatan sesuai standar tim hukum Anda.

## Kesimpulan

Anda kini memiliki resep lengkap,‑end, tentang cara **menambahkan bates numbers** ke PDF apa pun menggunakan Aspose.Pdf, lengkap dengan opsi untuk **menambahkan footer ke pdf**, **menambahkan nomor halaman pdf**, dan **menambahkan penomoran halaman khusus**. Kode ini sepenuhnya mandiri, bekerja dengan .NET 6 ke atas, dan dapat dimasukkan ke dalam pipeline otomatisasi apa pun.

Apa selanjutnya? Coba ganti penempatan `BottomCenter` dengan gaya header, bereksperimen dengan prefix dinamis (misalnya, ID kasus dari basis data), atau gabungkan ini dengan fitur ekstraksi teks Aspose untuk menghasilkan indeks yang dapat dicari dari dokumen yang baru saja Anda beri nomor. Tidak ada batasan, dan Anda kini memiliki alat yang kuat untuk kontrol dokumen.

Selamat coding, semoga PDF Anda selalu ternomori dengan sempurna!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}