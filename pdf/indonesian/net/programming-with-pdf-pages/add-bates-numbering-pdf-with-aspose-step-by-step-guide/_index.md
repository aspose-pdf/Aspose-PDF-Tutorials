---
category: general
date: 2026-08-08
description: Tambahkan penomoran Bates pada PDF menggunakan Aspose.Pdf di C#. Tutorial
  ini juga menunjukkan cara menambahkan halaman kosong pada PDF dan menghasilkan PDF
  secara programatis.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add bates numbering pdf
- add blank page pdf
- generate pdf programmatically
- create pdf aspose
language: id
lastmod: 2026-08-08
og_description: Tambahkan penomoran Bates pada PDF dengan Aspose.Pdf di C#. Pelajari
  cara menambahkan halaman kosong pada PDF, menghasilkan PDF secara programatik, dan
  menyimpan dokumen akhir dalam hitungan menit.
og_image_alt: Screenshot of C# code adding Bates numbering and a blank page to a PDF
  using Aspose.Pdf
og_title: Menambahkan Penomoran Bates pada PDF dengan Aspose – Panduan Lengkap C#
schemas:
- author: Aspose
  dateModified: '2026-08-08'
  description: Add bates numbering pdf using Aspose.Pdf in C#. This tutorial also
    shows how to add blank page pdf and generate pdf programmatically.
  headline: Add bates numbering pdf with Aspose – step‑by‑step guide
  type: TechArticle
- description: Add bates numbering pdf using Aspose.Pdf in C#. This tutorial also
    shows how to add blank page pdf and generate pdf programmatically.
  name: Add bates numbering pdf with Aspose – step‑by‑step guide
  steps:
  - name: What if I need a different font or position?
    text: 'The `BatesNumberingArtifact` exposes properties such as `FontSize`, `FontColor`,
      `HorizontalAlignment`, and `VerticalAlignment`. For example:'
  - name: How do I exclude a specific page from numbering?
    text: Create a separate `BatesNumberingArtifact` for the pages you want to number
      and add it only to those pages. Pages without an attached artifact will remain
      unnumbered.
  - name: Does this work with existing PDFs?
    text: 'Yes. Instead of `new Document()`, load an existing file:'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF generation
- Bates numbering
title: Menambahkan penomoran Bates pada PDF dengan Aspose – panduan langkah demi langkah
url: /id/net/programming-with-pdf-pages/add-bates-numbering-pdf-with-aspose-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Menambahkan bates numbering pdf dengan Aspose – panduan langkah demi langkah

Menambahkan bates numbering pdf dengan Aspose.Pdf sangat mudah setelah Anda memahami langkah‑langkah dasarnya. Jika Anda juga perlu menambahkan blank page pdf atau menghasilkan pdf secara programatis, panduan ini mencakup semua yang Anda butuhkan.

Dalam tutorial ini Anda akan:

* Membuat dokumen PDF baru dari awal.  
* Menambahkan blank page pdf yang akan menampung nomor Bates.  
* Mengonfigurasi artefak Bates numbering dengan awalan khusus.  
* Menyimpan PDF sehingga nomor muncul pada file yang dihasilkan.  

Pada akhir tutorial Anda akan memiliki aplikasi konsol C# yang berfungsi penuh yang menghasilkan PDF berisi nomor Bates seperti **CASE‑1000**, **CASE‑1001**, … – sebuah kebutuhan umum untuk alur kerja hukum dan e‑discovery.

## Prasyarat

* .NET 6.0 SDK atau yang lebih baru (kode juga berfungsi dengan .NET Framework 4.8).  
* Visual Studio 2022 atau IDE yang kompatibel dengan C#.  
* Lisensi Aspose.Pdf untuk .NET yang valid (atau kunci evaluasi gratis).  
* Familiaritas dasar dengan sintaks C#.

> **Pro tip:** Jika Anda menjalankan kode tanpa lisensi, Aspose akan menambahkan watermark kecil pada PDF output.

## Langkah 1: Siapkan proyek dan impor Aspose.Pdf

Buat proyek konsol baru dan tambahkan paket NuGet Aspose.Pdf:

```bash
dotnet new console -n BatesNumberingDemo
cd BatesNumberingDemo
dotnet add package Aspose.Pdf
```

Direktif `using` yang diperlukan untuk contoh ini adalah:

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Artifacts;
```

Namespace ini memberi Anda akses ke kelas `Document`, `Page`, dan `BatesNumberingArtifact` yang akan digunakan nanti.

## Langkah 2: Tambahkan blank page pdf

Nomor Bates harus ditempelkan pada sebuah halaman, jadi pertama-tama kami membuat halaman kosong yang akan menerima artefak penomoran.

```csharp
// Step 2: Add a blank page pdf
Document pdfDocument = new Document();          // creates an empty PDF
Page pdfPage = pdfDocument.Pages.Add();         // adds the first (blank) page
```

Kelas `Document` mewakili seluruh file PDF, sementara `Pages.Add()` menyisipkan halaman baru yang kosong di akhir koleksi halaman dokumen. Karena dokumen dimulai kosong, pemanggilan ini juga membuat halaman pertama.

## Langkah 3: Konfigurasikan artefak Bates numbering

Sekarang kami mendefinisikan bagaimana nomor Bates harus ditampilkan. `BatesNumberingArtifact` memungkinkan Anda mengatur nomor awal, awalan, akhiran, dan opsi format.

```csharp
// Step 3: Define Bates numbering settings
BatesNumberingArtifact batesArtifact = new BatesNumberingArtifact(pdfPage)
{
    StartNumber = 1000,          // first number in the sequence
    Prefix = "CASE-",            // custom prefix before each number
    // Optional: you can also set Suffix, FontSize, FontColor, etc.
};
```

**Mengapa ini penting:**  
Mengatur `StartNumber` ke **1000** sesuai dengan konvensi berkas kasus hukum yang umum. `Prefix` memastikan setiap nomor muncul sebagai **CASE‑1000**, **CASE‑1001**, … yang lebih mudah dicari dan diurutkan.

## Langkah 4: Lampirkan artefak ke halaman

Artefak harus ditambahkan ke koleksi `Artifacts` halaman sehingga Aspose merendernya pada setiap halaman saat disimpan.

```csharp
// Step 4: Attach the Bates numbering artifact to the PDF page
pdfPage.Artifacts.Add(batesArtifact);
```

Saat dokumen disimpan, Aspose secara otomatis mengulangi artefak pada semua halaman, menambah nomor untuk setiap halaman berikutnya.

## Langkah 5: (Opsional) Tambahkan halaman tambahan

Jika Anda membutuhkan lebih banyak halaman, cukup ulangi `pdfDocument.Pages.Add()`. Artefak Bates numbering yang Anda lampirkan pada langkah sebelumnya akan otomatis muncul pada setiap halaman baru.

```csharp
// Example: add two more pages
pdfDocument.Pages.Add();
pdfDocument.Pages.Add();
```

## Langkah 6: Simpan PDF – menghasilkan pdf secara programatis

Akhirnya, simpan dokumen ke disk. Inilah titik di mana nomor Bates dirender ke halaman.

```csharp
// Step 6: Save the PDF – generate pdf programmatically
string outputPath = Path.Combine(
    Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
    "BatesNumberedDocument.pdf");

// Ensure the directory exists
Directory.CreateDirectory(Path.GetDirectoryName(outputPath)!);

pdfDocument.Save(outputPath);
Console.WriteLine($"PDF saved to: {outputPath}");
```

**Hasil yang diharapkan:**  
Buka *BatesNumberedDocument.pdf* dan Anda akan melihat PDF tiga halaman. Setiap halaman menampilkan nomor Bates di pojok kanan bawah:

* Halaman 1 → **CASE‑1000**  
* Halaman 2 → **CASE‑1001**  
* Halaman 3 → **CASE‑1002**

Nomor-nomor tersebut secara otomatis bertambah karena artefak terlampir pada koleksi halaman.

## Contoh lengkap yang dapat dijalankan

Menggabungkan semuanya, berikut adalah program konsol lengkap yang dapat Anda salin, tempel, dan jalankan:

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Artifacts;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main()
        {
            // Create a new PDF document
            Document pdfDocument = new Document();

            // Add a blank page pdf
            Page pdfPage = pdfDocument.Pages.Add();

            // Define Bates numbering settings (add bates numbering pdf)
            BatesNumberingArtifact batesArtifact = new BatesNumberingArtifact(pdfPage)
            {
                StartNumber = 1000,
                Prefix = "CASE-"
            };

            // Attach the artifact to the page
            pdfPage.Artifacts.Add(batesArtifact);

            // (Optional) add more pages to see incremented numbers
            pdfDocument.Pages.Add(); // page 2
            pdfDocument.Pages.Add(); // page 3

            // Save the PDF – generate pdf programmatically
            string outputPath = Path.Combine(
                Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
                "BatesNumberedDocument.pdf");

            Directory.CreateDirectory(Path.GetDirectoryName(outputPath)!);
            pdfDocument.Save(outputPath);

            Console.WriteLine($"PDF saved to: {outputPath}");
        }
    }
}
```

Jalankan program dengan `dotnet run`. Setelah eksekusi, temukan file di desktop Anda dan verifikasi nomor Bates.

![Add bates numbering pdf example](/images/bates-numbering.png "Add bates numbering pdf example")

## Pertanyaan umum dan kasus tepi

### Bagaimana jika saya membutuhkan font atau posisi yang berbeda?

`BatesNumberingArtifact` menyediakan properti seperti `FontSize`, `FontColor`, `HorizontalAlignment`, dan `VerticalAlignment`. Misalnya:

```csharp
batesArtifact.FontSize = 12;
batesArtifact.FontColor = Color.Blue;
batesArtifact.HorizontalAlignment = HorizontalAlignment.Left;
batesArtifact.VerticalAlignment = VerticalAlignment.Top;
```

### Bagaimana cara mengecualikan halaman tertentu dari penomoran?

Buat `BatesNumberingArtifact` terpisah untuk halaman yang ingin Anda beri nomor dan tambahkan hanya ke halaman‑halaman tersebut. Halaman tanpa artefak yang terlampir akan tetap tidak bernomor.

### Apakah ini bekerja dengan PDF yang sudah ada?

Ya. Alih-alih `new Document()`, muat file yang sudah ada:

```csharp
Document pdfDocument = new Document("input.pdf");
```

Kemudian lampirkan artefak ke halaman yang diinginkan dan simpan.

## Kesimpulan

Anda kini tahu cara **add bates numbering pdf** menggunakan Aspose.Pdf, cara **add blank page pdf**, dan cara **generate pdf programmatically** dalam solusi C# yang bersih dan dapat digunakan kembali. Pendekatan ini bekerja dengan jumlah halaman berapa pun, awalan khusus, dan opsi styling, memberi Anda kontrol penuh atas dokumen akhir.

Langkah selanjutnya yang dapat Anda jelajahi:

* Use **create pdf as

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber daya menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [How to Add and Customize Page Numbers in PDFs Using Aspose.PDF for .NET | Document Manipulation Guide](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [How to Add an Empty Page at the End of a PDF Using Aspose.PDF for .NET | Step-by-Step Guide](/pdf/english/net/document-manipulation/add-empty-page-end-pdf-aspose-pdf-net/)
- [Create PDF Document with Aspose.PDF – Add Page, Shape & Save](/pdf/english/net/document-creation/create-pdf-document-with-aspose-pdf-add-page-shape-save/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}