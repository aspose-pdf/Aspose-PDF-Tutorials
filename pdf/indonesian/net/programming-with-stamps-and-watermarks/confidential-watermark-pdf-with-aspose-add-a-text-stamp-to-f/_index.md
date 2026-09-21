---
category: general
date: 2026-02-22
description: Tutorial watermark PDF rahasia menggunakan Aspose.Pdf – pelajari cara
  menambahkan label rahasia sebagai stempel teks pada halaman pertama dari PDF apa
  pun.
draft: false
keywords:
- confidential watermark pdf
- add confidential label
- aspose pdf watermark
- add stamp first page
- add text stamp pdf
language: id
og_description: 'Panduan PDF watermark rahasia: petunjuk langkah demi langkah untuk
  menambahkan label rahasia sebagai cap teks pada halaman pertama menggunakan Aspose.Pdf
  untuk .NET.'
og_title: PDF watermark rahasia dengan Aspose – Tambahkan Stempel Teks
tags:
- aspose
- pdf
- watermark
- csharp
title: 'Watermark PDF Rahasia dengan Aspose: Tambahkan Stempel Teks ke Halaman Pertama'
url: /id/net/programming-with-stamps-and-watermarks/confidential-watermark-pdf-with-aspose-add-a-text-stamp-to-f/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Confidential watermark PDF – Cara Menambahkan Stempel Teks pada Halaman Pertama

Pernah membutuhkan **confidential watermark PDF** tetapi tidak yakin cara menempelkan label hanya pada halaman pertama? Anda tidak sendirian—banyak pengembang bergumul dengan “Bagaimana cara menambahkan label rahasia tanpa mengacaukan tata letak?”  

Berita baik? Dengan Aspose.Pdf untuk .NET Anda dapat melakukannya dalam beberapa baris kode, dan saya akan memandu Anda melalui seluruh proses sekarang juga. Tidak ada referensi yang samar, hanya solusi lengkap yang dapat disalin‑tempel dan berfungsi hari ini.

## Apa yang Akan Anda Pelajari

Di tutorial ini kami akan membahas:

* Menginstal paket NuGet Aspose.Pdf (satu-satunya prasyarat).
* Memuat PDF yang sudah ada.
* Membuat **confidential watermark PDF** menggunakan `TextStamp`.
* Menambahkan stempel tersebut **hanya pada halaman pertama** (persyaratan “add stamp first page”).
* Menyimpan hasil dan memverifikasi output.

## Prasyarat

* .NET 6+ (kode ini bekerja pada .NET Core dan .NET Framework sekaligus).
* Visual Studio 2022 atau IDE apa pun yang Anda sukai.
* Aspose.Pdf for .NET – version 23.10 atau lebih baru disarankan untuk perbaikan bug terbaru.

Jika Anda belum menambahkan Aspose.Pdf ke proyek Anda, jalankan:

```bash
dotnet add package Aspose.Pdf
```

Itu saja—tidak ada DLL tambahan, tidak ada masalah lisensi untuk versi percobaan (hanya ingat untuk menerapkan kunci lisensi Anda sebelum merilis).

## Langkah 1: Memuat Dokumen PDF Sumber

Pertama kita perlu membuka file yang ingin dilindungi. Kelas `Document` mewakili seluruh PDF, dan memuatnya semudah memberikan path.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Path to the PDF you want to watermark
string inputPdfPath = @"C:\MyDocs\input.pdf";

// Load the PDF into memory
using var pdfDocument = new Document(inputPdfPath);
```

*Mengapa ini penting*: Memuat dokumen memberi Anda akses ke koleksi `Pages`, tempat kami akan menempelkan stempel. Menggunakan `using var` memastikan handle file segera dilepaskan—penting untuk batch besar.

## Langkah 2: Membuat Stempel Teks Rahasia

Sekarang kami membuat label visual. `TextStamp` memungkinkan kami mengontrol ukuran, pembungkus, dan skala. Pengaturan berikut memastikan kata *Confidential* pas tanpa meluber.

```csharp
// Build a text stamp that says "Confidential"
var confidentialStamp = new TextStamp("Confidential")
{
    // Auto‑adjust the font so it never exceeds the rectangle
    AutoAdjustFontSizeToFitStampRectangle = true,
    AutoAdjustFontSizePrecision = 0.01f,

    // Wrap by whole words—no broken words in the middle
    WordWrapMode = TextFormattingOptions.WordWrapMode.ByWords,

    // Define the stamp rectangle (you can tweak width/height)
    Width = 300,
    Height = 100,

    // Keep the stamp size constant even if the page is resized
    Scale = false
};
```

**Pro tip**: Jika Anda membutuhkan font atau warna yang berbeda, atur `confidentialStamp.TextState.Font` dan `confidentialStamp.TextState.ForegroundColor`. Misalnya, `confidentialStamp.TextState.Font = FontRepository.FindFont("Arial")` dan `confidentialStamp.TextState.ForegroundColor = Color.Red`.

## Langkah 3: Menambahkan Stempel Hanya pada Halaman Pertama

Aspose menggunakan indeks halaman berbasis 1, jadi `Pages[1]` adalah halaman pertama. Menambahkan stempel di sana memenuhi persyaratan **add stamp first page**.

```csharp
// Attach the stamp to the very first page
pdfDocument.Pages[1].AddStamp(confidentialStamp);
```

Jika Anda perlu menambahkan watermark ke setiap halaman, lakukan loop melalui `pdfDocument.Pages`. Namun untuk label satu halaman, satu baris kode ini sudah cukup.

## Langkah 4: Menyimpan PDF yang Diberi Watermark

Terakhir, tulis dokumen yang telah dimodifikasi kembali ke disk. Anda dapat menimpa file asli atau membuat file baru—sesuai keinginan.

```csharp
// Destination path for the watermarked PDF
string outputPdfPath = @"C:\MyDocs\Stamped.pdf";

// Persist the changes
pdfDocument.Save(outputPdfPath);
```

Saat Anda membuka `Stamped.pdf`, Anda akan melihat *Confidential* ditampilkan di pojok kiri atas halaman 1 (atau di mana pun Anda menempatkan stempel). Sisanya dokumen tetap tidak berubah.

## Hasil yang Diharapkan

| Sebelum | Setelah (halaman pertama) |
|--------|---------------------------|
| ![Halaman PDF asli](/images/original.png "Halaman PDF asli") | ![Contoh watermark PDF rahasia](/images/confidential-watermark.png "Contoh watermark PDF rahasia") |

*Teks alt gambar*: **confidential watermark PDF example** (menyertakan kata kunci utama).

## Kasus Tepi & Pertanyaan Umum

### Bagaimana jika PDF tidak memiliki halaman?

Mencoba mengakses `Pages[1]` akan melempar `ArgumentOutOfRangeException`. Lindungi terhadap hal ini:

```csharp
if (pdfDocument.Pages.Count == 0)
    throw new InvalidOperationException("The PDF is empty.");
```

### Bagaimana cara menambahkan watermark ke beberapa halaman?

```csharp
foreach (Page page in pdfDocument.Pages)
{
    page.AddStamp(confidentialStamp);
}
```

Ingat untuk mengatur ulang posisi `confidentialStamp` jika Anda menginginkannya di sudut yang berbeda per halaman.

### Bisakah saya mengubah posisi stempel?

Ya—atur `confidentialStamp.HorizontalAlignment` dan `confidentialStamp.VerticalAlignment`, atau gunakan `confidentialStamp.XIndent` / `YIndent` untuk penempatan pixel‑perfect.

### Apakah ini bekerja dengan PDF yang dilindungi kata sandi?

Aspose dapat membuka file terenkripsi jika Anda menyediakan kata sandi:

```csharp
var pdfDocument = new Document(inputPdfPath, new LoadOptions { Password = "mySecret" });
```

### Bagaimana dengan kinerja pada batch besar?

Memuat dan menyimpan setiap dokumen secara terpisah dapat membebani I/O. Pertimbangkan untuk menggunakan kembali satu instance `Document` untuk operasi di memori dan hanya menyimpan sekali per batch.

## Contoh Lengkap yang Berfungsi

Berikut adalah program lengkap yang dapat Anda salin‑tempel ke aplikasi console. Program ini mencakup semua langkah, penanganan error, dan pesan verifikasi sederhana.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Load the source PDF
        // -------------------------------------------------
        string inputPdfPath = @"C:\MyDocs\input.pdf";
        if (!System.IO.File.Exists(inputPdfPath))
        {
            Console.WriteLine("Input file not found.");
            return;
        }

        using var pdfDocument = new Document(inputPdfPath);

        if (pdfDocument.Pages.Count == 0)
        {
            Console.WriteLine("The PDF contains no pages.");
            return;
        }

        // -------------------------------------------------
        // 2️⃣ Create the confidential text stamp
        // -------------------------------------------------
        var confidentialStamp = new TextStamp("Confidential")
        {
            AutoAdjustFontSizeToFitStampRectangle = true,
            AutoAdjustFontSizePrecision = 0.01f,
            WordWrapMode = TextFormattingOptions.WordWrapMode.ByWords,
            Width = 300,
            Height = 100,
            Scale = false,
            // Optional styling
            TextState = { FontSize = 24, Font = FontRepository.FindFont("Arial"), ForegroundColor = Color.Red }
        };

        // -------------------------------------------------
        // 3️⃣ Add the stamp to the first page only
        // -------------------------------------------------
        pdfDocument.Pages[1].AddStamp(confidentialStamp);

        // -------------------------------------------------
        // 4️⃣ Save the result
        // -------------------------------------------------
        string outputPdfPath = @"C:\MyDocs\Stamped.pdf";
        pdfDocument.Save(outputPdfPath);

        Console.WriteLine($"Successfully added a confidential watermark PDF. Saved to: {outputPdfPath}");
    }
}
```

Jalankan program, buka `Stamped.pdf`, dan Anda akan melihat **confidential watermark PDF** diterapkan tepat di tempat yang kami maksud.

## Kesimpulan

Anda kini memiliki cara yang solid dan siap produksi untuk **menambahkan label rahasia** sebagai **stempel teks** pada **halaman pertama** dari PDF apa pun menggunakan Aspose.Pdf. Solusi ini sepenuhnya mandiri, bekerja dengan versi .NET terbaru, dan dapat diperluas ke beberapa halaman, font khusus, atau warna berbeda.

**Langkah selanjutnya** yang dapat Anda jelajahi:

* Ganti stempel teks dengan stempel gambar (`ImageStamp`) untuk menyisipkan logo.
* Gabungkan pendekatan ini dengan loop untuk membuat **aspose pdf watermark** di seluruh dokumen.
* Integrasikan kode ke dalam API ASP.NET Core sehingga pengguna dapat mengunggah PDF dan menerima versi ber‑watermark secara langsung.

Cobalah, sesuaikan dimensinya, dan biarkan teknik **add text stamp pdf** menjadi andalan dalam kotak peralatan keamanan dokumen Anda. Selamat coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}