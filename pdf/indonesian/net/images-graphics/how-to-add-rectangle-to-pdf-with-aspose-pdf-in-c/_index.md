---
category: general
date: 2026-10-10
description: Pelajari cara menambahkan persegi panjang ke PDF, menggambar bentuk pada
  PDF, dan menyimpan PDF yang telah dimodifikasi menggunakan Aspose.PDF. Termasuk
  panduan langkah demi langkah untuk mengakses halaman PDF tertentu.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add rectangle to PDF
- draw shape on PDF
- save modified PDF
- add shape to PDF
- access specific PDF page
language: id
lastmod: 2026-10-10
og_description: Tambahkan persegi panjang ke PDF menggunakan Aspose.PDF dalam C#.
  Tutorial ini menunjukkan cara menggambar bentuk pada PDF, mengakses halaman PDF
  tertentu, dan menyimpan PDF yang telah dimodifikasi.
og_image_alt: Screenshot of a PDF page with a blue rectangle overlay created by Aspose.PDF
og_title: Tambahkan persegi panjang ke PDF dengan Aspose.PDF – panduan lengkap C#
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Learn how to add rectangle to PDF, draw shape on PDF, and save modified
    PDF using Aspose.PDF. Includes step‑by‑step guide to access specific PDF page.
  headline: How to add rectangle to PDF with Aspose.PDF in C#
  type: TechArticle
- description: Learn how to add rectangle to PDF, draw shape on PDF, and save modified
    PDF using Aspose.PDF. Includes step‑by‑step guide to access specific PDF page.
  name: How to add rectangle to PDF with Aspose.PDF in C#
  steps:
  - name: Expected output
    text: 'Running the program prints:'
  - name: What if the PDF has only one page?
    text: Attempting to access `pdfDocument.Pages[1]` throws an `ArgumentOutOfRangeException`.
      Guard against this by checking `pdfDocument.Pages.Count` before indexing.
  - name: How to add multiple rectangles on different pages?
    text: Repeat Steps 2‑4 for each target page, adjusting the rectangle’s coordinates
      as needed. You can place the logic inside a loop that iterates over `pdfDocument.Pages`.
  - name: Can I use other shapes such as circles or polygons?
    text: Yes. Aspose.PDF provides `Ellipse`, `Polygon`, and `Polyline` classes that
      follow the same pattern as `Rectangle`. Replace the `new Aspose.Pdf.Drawing.Rectangle`
      call with the desired shape class.
  - name: Does the library support PDFs with rotated pages?
    text: Aspose.PDF automatically respects page rotation when rendering shapes. The
      rectangle’s coordinates are interpreted in the page’s native coordinate system,
      so no extra transformation is required.
  type: HowTo
tags:
- Aspose.PDF
- C#
- PDF manipulation
title: Cara menambahkan persegi panjang ke PDF dengan Aspose.PDF di C#
url: /id/net/images-graphics/how-to-add-rectangle-to-pdf-with-aspose-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara menambahkan persegi panjang ke PDF dengan Aspose.PDF di C#

Jika Anda perlu **menambahkan persegi panjang ke PDF** secara programatis, panduan ini menunjukkan secara tepat caranya. Anda akan belajar **menggambar bentuk pada PDF**, menargetkan halaman tertentu, dan **menyimpan PDF yang dimodifikasi** tanpa error.

Bekerja dengan dokumen PDF adalah kebutuhan umum untuk pelaporan, penagihan, atau anotasi dokumen. Pada akhir tutorial ini Anda dapat dengan percaya diri **menambahkan bentuk ke PDF**, menangani error out‑of‑bounds, dan mengintegrasikan solusi ke dalam proyek .NET apa pun.

## Prasyarat

* .NET 6.0 SDK atau yang lebih baru terinstal  
* Visual Studio 2022 (atau IDE C# apa pun)  
* Lisensi Aspose.PDF untuk .NET atau kunci evaluasi gratis – API berfungsi sama dalam kedua mode  
* File PDF bernama `input.pdf` ditempatkan dalam folder yang dapat Anda referensikan dari kode Anda  

Item-item ini adalah satu‑satunya dependensi eksternal untuk contoh.

## Langkah 1: Instal paket NuGet Aspose.PDF

Pustaka Aspose.PDF menyediakan kelas `Document`, `Rectangle`, dan kelas menggambar lainnya yang Anda perlukan.

```bash
dotnet add package Aspose.PDF
```

Menjalankan perintah ini menambahkan versi stabil terbaru Aspose.PDF ke proyek Anda, sehingga kelas PDF tersedia untuk kompilasi.

## Langkah 2: Muat dokumen PDF

Operasi pertama adalah memuat file sumber. Ini membuat representasi dalam memori yang dapat Anda modifikasi.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using System;

class PdfRectangleExample
{
    static void Main()
    {
        // Load the PDF document from disk
        var pdfDocument = new Document(@"YOUR_DIRECTORY\input.pdf");
```

*Mengapa ini penting*: Memuat dokumen memberi Anda akses ke koleksi halamannya, yang diperlukan untuk **mengakses halaman PDF tertentu** nanti.

## Langkah 3: Akses halaman kedua (indeks berbasis nol)

Halaman PDF diindeks mulai dari `0`. Untuk menempatkan persegi panjang pada halaman kedua, ambil halaman dengan indeks `1`.

```csharp
        // Access the second page (pages are zero‑based)
        var page = pdfDocument.Pages[1];
```

Jika dokumen memiliki kurang dari dua halaman, `ArgumentOutOfRangeException` akan dilempar, memberi peringatan bahwa Anda memerlukan guard clause dalam kode produksi.

## Langkah 4: Buat bentuk persegi panjang

Tentukan posisi dan ukuran persegi panjang menggunakan struktur `Rectangle`, lalu bungkus dalam objek gambar Aspose.

```csharp
        // Define rectangle bounds: (x, y, width, height)
        var rectangleBounds = new Rectangle(100, 100, 300, 200);
        var rectangleShape = new Aspose.Pdf.Drawing.Rectangle(rectangleBounds)
        {
            // Optional visual styling
            Border = new BorderInfo(BorderSide.All, 2f, Color.Blue),
            FillColor = Color.FromArgb(30, 0, 0, 255) // semi‑transparent blue
        };
```

*Mengapa ini penting*: Properti `BorderInfo` dan `FillColor` memungkinkan Anda **menggambar bentuk pada PDF** dengan outline yang terlihat dan isi opsional, sehingga persegi panjang menonjol bagi pembaca.

## Langkah 5: Tambahkan persegi panjang ke koleksi paragraf halaman

Aspose.PDF memperlakukan objek gambar sebagai elemen paragraf. Menambahkan persegi panjang ke koleksi `Paragraphs` halaman akan merendernya pada halaman.

```csharp
        // Add the rectangle shape to the page
        page.Paragraphs.Add(rectangleShape);
```

Pada titik ini dokumen PDF dalam memori berisi bentuk baru, tetapi file di disk belum berubah sampai Anda menyimpannya.

## Langkah 6: Simpan PDF yang dimodifikasi dan tangani error out‑of‑bounds

Memanggil `Save` menulis dokumen yang diperbarui ke file baru. Jika persegi panjang melebihi dimensi halaman, Aspose melempar `PdfException`. Menangkap exception ini memungkinkan Anda melaporkan masalah dengan bersih.

```csharp
        try
        {
            // Save the altered PDF to a new file
            pdfDocument.Save(@"YOUR_DIRECTORY\output.pdf");
            Console.WriteLine("PDF saved successfully with rectangle added.");
        }
        catch (Aspose.Pdf.Exceptions.PdfException ex)
        {
            // Handle shape that does not fit on the page
            Console.WriteLine($"Shape out of bounds: {ex.Message}");
        }
    }
}
```

*Mengapa ini penting*: Blok `try/catch` memastikan aplikasi Anda **menyimpan PDF yang dimodifikasi** dengan aman, dan pesan error membantu Anda menyesuaikan koordinat persegi panjang bila diperlukan.

## Contoh lengkap yang berfungsi

Menggabungkan semua langkah, berikut program lengkap yang siap dijalankan:

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using System;
using System.Drawing; // Required for Color

class PdfRectangleExample
{
    static void Main()
    {
        // Step 1: Load the PDF document
        var pdfDocument = new Document(@"YOUR_DIRECTORY\input.pdf");

        // Step 2: Access the second page (zero‑based)
        var page = pdfDocument.Pages[1];

        // Step 3: Create a rectangle shape positioned at (100,100) with width 300 and height 200
        var rectangleBounds = new Rectangle(100, 100, 300, 200);
        var rectangleShape = new Aspose.Pdf.Drawing.Rectangle(rectangleBounds)
        {
            Border = new BorderInfo(BorderSide.All, 2f, Color.Blue),
            FillColor = Color.FromArgb(30, 0, 0, 255) // semi‑transparent blue
        };

        // Step 4: Add the rectangle shape to the page's paragraph collection
        page.Paragraphs.Add(rectangleShape);

        // Step 5: Save the modified PDF, handling out‑of‑bounds cases
        try
        {
            pdfDocument.Save(@"YOUR_DIRECTORY\output.pdf");
            Console.WriteLine("PDF saved successfully with rectangle added.");
        }
        catch (Aspose.Pdf.Exceptions.PdfException ex)
        {
            Console.WriteLine($"Shape out of bounds: {ex.Message}");
        }
    }
}
```

### Output yang diharapkan

Menjalankan program mencetak:

```
PDF saved successfully with rectangle added.
```

dan membuat `output.pdf` yang menampilkan konten asli plus persegi panjang biru pada koordinat yang ditentukan di halaman kedua.

Jika persegi panjang lebih besar dari halaman, Anda akan melihat:

```
Shape out of bounds: The shape exceeds page margins.
```

## Pertanyaan umum dan kasus tepi

### Bagaimana jika PDF hanya memiliki satu halaman?

Mencoba mengakses `pdfDocument.Pages[1]` akan melempar `ArgumentOutOfRangeException`. Lindungi dengan memeriksa `pdfDocument.Pages.Count` sebelum mengindeks.

```csharp
if (pdfDocument.Pages.Count < 2)
{
    Console.WriteLine("Document does not contain a second page.");
    return;
}
```

### Bagaimana cara menambahkan beberapa persegi panjang pada halaman yang berbeda?

Ulangi Langkah 2‑4 untuk setiap halaman target, sesuaikan koordinat persegi panjang sesuai kebutuhan. Anda dapat menempatkan logika dalam loop yang mengiterasi `pdfDocument.Pages`.

### Bisakah saya menggunakan bentuk lain seperti lingkaran atau poligon?

Ya. Aspose.PDF menyediakan kelas `Ellipse`, `Polygon`, dan `Polyline` yang mengikuti pola yang sama seperti `Rectangle`. Ganti pemanggilan `new Aspose.Pdf.Drawing.Rectangle` dengan kelas bentuk yang diinginkan.

### Apakah pustaka mendukung PDF dengan halaman yang diputar?

Aspose.PDF secara otomatis menghormati rotasi halaman saat merender bentuk. Koordinat persegi panjang diinterpretasikan dalam sistem koordinat asli halaman, sehingga tidak diperlukan transformasi tambahan.

## Pertimbangan kinerja

* **Penggunaan memori** – Memuat PDF besar (ratusan megabyte) mengonsumsi memori secara proporsional. Jika Anda hanya perlu memodifikasi satu halaman, pertimbangkan menggunakan `PdfFileInfo` untuk mengekstrak halaman tersebut, memodifikasinya, dan kemudian menggabungkannya kembali.  
* **Pemrosesan batch** – Saat menambahkan bentuk ke banyak dokumen, gunakan kembali satu instance `License` untuk menghindari overhead validasi lisensi berulang.

## Langkah selanjutnya

Sekarang Anda dapat **menambahkan persegi panjang ke PDF**, jelajahi topik terkait berikut:

* **draw shape on PDF** – pelajari cara menambahkan teks, gambar, dan watermark  
* **add shape to PDF** – gabungkan beberapa bentuk menjadi satu lapisan anotasi  
* **save modified PDF** – gunakan stream (`MemoryStream`) untuk mengembalikan PDF langsung dari API web  
* **access specific PDF page** – implementasi ekstraksi rentang halaman untuk laporan khusus  

Bereksperimenlah dengan warna, gaya garis, dan tingkat transparansi yang berbeda untuk menyesuaikan pedoman merek Anda.

---

*Selamat coding! Jika tutorial ini membantu Anda **menambahkan persegi panjang ke PDF**, pertimbangkan untuk membagikannya dengan rekan tim atau berkontribusi perbaikan kembali ke komunitas.*

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Cara Menambahkan Bentuk ke PDF dengan Aspose.PDF di C# – Panduan Langkah demi Langkah](/pdf/english/net/images-graphics/how-to-add-shape-to-pdf-with-aspose-pdf-in-c-step-by-step-gu/)
- [Cara Menambahkan Objek Garis dalam PDF Menggunakan Aspose.PDF untuk .NET: Panduan Langkah demi Langkah](/pdf/english/net/document-manipulation/add-line-aspose-pdf-dotnet-tutorial/)
- [Cara Membuat PDF di C# – Tambah Halaman, Gambar Persegi Panjang & Simpan](/pdf/english/net/document-creation/how-to-create-pdf-in-c-add-page-draw-rectangle-save/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}