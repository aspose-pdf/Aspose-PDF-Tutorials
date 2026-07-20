---
category: general
date: 2026-07-20
description: Cara menambahkan penomoran Bates ke PDF menggunakan Aspose.Pdf. Pelajari
  cara menambahkan nomor Bates pada PDF dan menambahkan stempel ke setiap halaman
  dengan cepat dan andal.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to add bates numbering
- add bates numbers pdf
- add stamp to each page
language: id
lastmod: 2026-07-20
og_description: Cara menambahkan penomoran Bates ke PDF dengan Aspose.Pdf. Panduan
  ini menunjukkan cara menambahkan nomor Bates pada PDF dan menstempel setiap halaman
  hanya dengan beberapa baris kode C#.
og_image_alt: Screenshot of a PDF page displaying Bates numbering added by Aspose.Pdf
og_title: Cara Menambahkan Penomoran Bates pada PDF – Tutorial Lengkap Aspose.Pdf
schemas:
- author: Aspose
  dateModified: '2026-07-20'
  description: How to add bates numbering to a PDF using Aspose.Pdf. Learn to add
    bates numbers pdf and add stamp to each page quickly and reliably.
  headline: How to Add Bates Numbering in PDF with Aspose – Step‑by‑Step Guide
  type: TechArticle
- questions:
  - answer: Yes. Load the document with a `PdfLoadOptions` object that supplies the
      password, then proceed exactly as shown.
    question: Does this work with password‑protected PDFs?
  - answer: Create multiple `BatesNumberingStamp` instances, configure each with its
      own `Prefix`, and apply them only to the appropriate page ranges.
    question: What if I need different prefixes per case?
  - answer: 'Aspose.Pdf offers a 30‑day trial. For production use you’ll need a license,
      but the API surface remains identical. --- ## Conclusion We’ve just covered
      **how to add bates numbering** to any PDF using Aspose.Pdf, demonstrated how
      to **add bates numbers pdf** in a clean, repeatable fashion, and showed'
    question: Is the library free?
  type: FAQPage
tags:
- Aspose.Pdf
- Bates numbering
- PDF automation
title: Cara Menambahkan Penomoran Bates pada PDF dengan Aspose – Panduan Langkah demi
  Langkah
url: /id/net/programming-with-stamps-and-watermarks/how-to-add-bates-numbering-in-pdf-with-aspose-step-by-step-g/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Menambahkan Penomoran Bates dalam PDF dengan Aspose – Panduan Langkah‑per‑Langkah

Pernah bertanya-tanya **how to add bates numbering** ke dokumen hukum tanpa menghabiskan berjam‑jam di GUI? Anda tidak sendirian. Di banyak firma hukum, lembaga pemerintah, dan bahkan perusahaan besar, menempelkan setiap halaman dengan identifier unik adalah tugas harian—namun satu baris kode C# dapat membuatnya menjadi sangat mudah.

Dalam tutorial ini kami akan membahas contoh lengkap yang dapat dijalankan yang menunjukkan secara tepat **how to add bates numbering** menggunakan library Aspose.Pdf. Pada akhir Anda juga akan tahu cara **add bates numbers pdf** file dan **add stamp to each page** dengan hanya beberapa baris kode. Tidak ada sihir, hanya penalaran jelas dan tips praktis.

## Apa yang Akan Anda Pelajari

- Muat PDF yang sudah ada dengan Aspose.Pdf.
- Buat sebuah `BatesNumberingStamp` dan sesuaikan tampilannya.
- Loop melalui setiap halaman dan **add stamp to each page** secara otomatis.
- Simpan hasilnya sebagai PDF baru yang memiliki nomor Bates profesional pada setiap lembar.

### Prasyarat

- .NET 6.0 atau lebih baru (kode ini juga berfungsi pada .NET Framework 4.7+).
- Lisensi Aspose.Pdf untuk .NET yang valid (atau kunci evaluasi sementara).
- File PDF asli yang ingin Anda beri nomor (kami akan menyebutnya `Original.pdf`).

Jika Anda memenuhi ketiga hal tersebut, Anda siap untuk memulai.

---

## Langkah 1: Siapkan Proyek Anda dan Instal Aspose.Pdf

Pertama, buat proyek console baru (atau tambahkan kode ke proyek yang sudah ada). Kemudian unduh paket NuGet:

```bash
dotnet add package Aspose.Pdf
```

> **Pro tip:** Jika Anda berada di jaringan korporat, pastikan sumber NuGet Anda dikonfigurasi untuk mengakses `https://www.nuget.org`.

## Langkah 2: Muat Dokumen PDF Sumber

Memuat PDF semudah mengarahkan Aspose ke jalur file. Kelas `Document` mewakili seluruh file.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Load the source PDF (replace the path with your own)
var document = new Document(@"C:\Temp\Original.pdf");

// Quick sanity check – how many pages are we dealing with?
Console.WriteLine($"Document contains {document.Pages.Count} pages.");
```

Mengapa kami mencatat jumlah halaman? Karena penomoran Bates harus berurutan di seluruh *semua* halaman, dan bagus untuk memverifikasi bahwa Anda tidak secara tidak sengaja memuat file yang berbeda.

## Langkah 3: Buat Bates Numbering Stamp

Inti dari operasi ini adalah `BatesNumberingStamp`. Ini memungkinkan Anda menentukan prefix, separator, padding digit, dan bahkan apakah stempel harus diperlakukan sebagai *artifact* (misalnya, tidak terlihat oleh alat ekstraksi teks).

```csharp
var batesStamp = new BatesNumberingStamp
{
    // Starting number – change this to whatever your workflow requires
    StartingNumber = 1000,

    // A human‑readable prefix, often a case or project code
    Prefix = "ABC-",

    // Separator between the running number and the total page count
    Separator = "/",

    // Pad the number with leading zeros to a fixed width (5 digits here)
    NumberOfDigits = 5,

    // Mark the stamp as an artifact so it won’t be indexed by search
    Artifact = true
};
```

**Mengapa pengaturan ini?**  
- `StartingNumber = 1000` meniru docket hukum tipikal yang sudah memiliki backlog.  
- `NumberOfDigits = 5` menjamin angka seperti `01000`, `01001`, dll., terformat rapi.  
- `Artifact = true` penting ketika PDF akan diproses melalui OCR atau pipeline e‑discovery; angka tetap terlihat oleh manusia tetapi diabaikan oleh mesin pencari teks.

## Langkah 4: Tambahkan Stempel ke Setiap Halaman

Sekarang kami melakukan loop pada `document.Pages` dan menerapkan stempel yang sama ke setiap halaman. Aspose secara otomatis menambah nomor untuk Anda.

```csharp
foreach (Page page in document.Pages)
{
    // The AddStamp method clones the stamp for the current page,
    // updates the running number, and positions it at the default location.
    page.AddStamp(batesStamp);
}
```

> **Pertanyaan umum:** *Bisakah saya mengontrol di mana stempel muncul?*  
> Tentu saja. `BatesNumberingStamp` mewarisi dari `Stamp`, sehingga Anda dapat mengatur properti seperti `HorizontalAlignment`, `VerticalAlignment`, `XIndent`, dan `YIndent` sebelum loop. Untuk singkat, kami akan tetap menggunakan sudut kanan‑bawah default.

## Langkah 5: Simpan PDF yang Dimodifikasi

Akhirnya, simpan perubahan. Anda dapat menimpa file asli atau menulis ke lokasi baru—di sini kami akan menyimpan kedua salinan.

```csharp
// Save the new PDF with Bates numbers
document.Save(@"C:\Temp\BatesNumbered.pdf");

// Inform the user
Console.WriteLine("Bates numbering added successfully!");
```

Ketika Anda membuka `BatesNumbered.pdf`, setiap halaman akan menampilkan stempel serupa dengan:

```
ABC-01000/00123
ABC-01001/00123
…
ABC-01122/00123
```

di mana `00123` adalah total jumlah halaman, dan prefix `ABC-` tetap konstan.

---

## Contoh Kerja Lengkap

Salin seluruh blok di bawah ini ke file `Program.cs` baru dan jalankan. Sesuaikan jalur file agar cocok dengan lingkungan Anda.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the source PDF
            var srcPath = @"C:\Temp\Original.pdf";
            var document = new Document(srcPath);
            Console.WriteLine($"Loaded '{srcPath}' with {document.Pages.Count} pages.");

            // 2️⃣ Configure the Bates numbering stamp
            var batesStamp = new BatesNumberingStamp
            {
                StartingNumber = 1000,
                Prefix = "ABC-",
                Separator = "/",
                NumberOfDigits = 5,
                Artifact = true,
                // Optional: change alignment if you need a different location
                // HorizontalAlignment = HorizontalAlignment.Left,
                // VerticalAlignment = VerticalAlignment.Top,
                // XIndent = 20,
                // YIndent = 20
            };

            // 3️⃣ Apply the stamp to every page
            foreach (Page page in document.Pages)
            {
                page.AddStamp(batesStamp);
            }

            // 4️⃣ Save the new PDF
            var outPath = @"C:\Temp\BatesNumbered.pdf";
            document.Save(outPath);
            Console.WriteLine($"Saved Bates‑numbered PDF to '{outPath}'.");
        }
    }
}
```

**Output yang diharapkan di konsol:**

```
Loaded 'C:\Temp\Original.pdf' with 12 pages.
Saved Bates-numbered PDF to 'C:\Temp\BatesNumbered.pdf'.
```

Buka file yang disimpan dan Anda akan melihat nomor berurutan pada setiap halaman—tepat seperti yang Anda harapkan ketika Anda **add bates numbers pdf**.

## Penyesuaian Lanjutan (Opsional)

| Tujuan | Cara mencapainya |
|------|-------------------|
| **Change stamp color** | Set `batesStamp.Color = Color.FromRgb(255, 0, 0);` before the loop. |
| **Place stamp in the header** | Adjust `HorizontalAlignment` and `VerticalAlignment` properties as shown in the commented code. |
| **Skip certain pages** | Add an `if (page.Number % 2 == 0) continue;` condition inside the `foreach`. |
| **Use a custom font** | Assign `batesStamp.Font = FontRepository.FindFont("Arial");`. |
| **Make the stamp visible to OCR** | Set `Artifact = false`. |

Variasi ini memungkinkan Anda **add stamp to each page** sambil tetap menjaga logika inti tetap rapi.

## Pertanyaan yang Sering Diajukan

**T: Apakah ini bekerja dengan PDF yang dilindungi kata sandi?**  
J: Ya. Muat dokumen dengan objek `PdfLoadOptions` yang menyediakan kata sandi, kemudian lanjutkan persis seperti yang ditunjukkan.

**T: Bagaimana jika saya membutuhkan prefix yang berbeda per kasus?**  
J: Buat beberapa instance `BatesNumberingStamp`, konfigurasikan masing‑masing dengan `Prefix` sendiri, dan terapkan hanya pada rentang halaman yang sesuai.

**T: Apakah perpustakaan ini gratis?**  
J: Aspose.Pdf menawarkan trial selama 30 hari. Untuk penggunaan produksi Anda memerlukan lisensi, tetapi antarmuka API tetap sama.

## Kesimpulan

Kami baru saja membahas **how to add bates numbering** ke PDF apa pun menggunakan Aspose.Pdf, mendemonstrasikan cara **add bates numbers pdf** secara bersih dan dapat diulang, serta menunjukkan cara paling sederhana untuk **add stamp to each page** dengan satu loop. Kode ini sepenuhnya mandiri, berjalan dalam hitungan detik, dan dapat dimasukkan ke dalam pipeline pemrosesan dokumen yang lebih besar tanpa modifikasi.

Siap untuk tantangan berikutnya? Coba buat halaman sampul yang mencantumkan rentang Bates, atau sematkan kode QR di samping setiap stempel. Kemungkinannya tak terbatas, dan pola yang Anda pelajari hari ini akan sangat berguna di mana pun Anda perlu mengotomatisasi metadata PDF.

Jika Anda menemukan panduan ini bermanfaat, bagikan, tinggalkan komentar, atau jelajahi tutorial lain kami tentang penggabungan PDF, watermarking, dan tanda tangan digital. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang dapat dijalankan dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [How to Add Page Stamps in PDFs Using Aspose.PDF for .NET&#58; A Complete Guide](/pdf/english/net/watermarks-backgrounds/add-page-stamp-aspose-pdf-dotnet-guide/)
- [How to Add Page Number Stamps in PDFs Using Aspose.PDF for .NET | Watermarks & Backgrounds](/pdf/english/net/watermarks-backgrounds/add-page-number-stamp-using-aspose-pdf-dotnet/)
- [How to Add and Customize Page Numbers in PDFs Using Aspose.PDF for .NET | Document Manipulation Guide](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}