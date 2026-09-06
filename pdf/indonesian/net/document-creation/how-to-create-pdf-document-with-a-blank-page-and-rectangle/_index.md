---
category: general
date: 2026-09-05
description: Buat dokumen PDF dalam C# dengan menambahkan halaman kosong, menggambar
  persegi panjang, dan menyimpan file PDF. Ikuti contoh Aspose.PDF langkah demi langkah.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create pdf document
- add blank page pdf
- draw rectangle pdf
- save pdf file
- how to add rectangle
language: id
lastmod: 2026-09-05
og_description: Buat dokumen PDF di C# dengan menambahkan halaman kosong, menggambar
  persegi panjang, dan menyimpan file PDF. Ikuti contoh lengkap ini dengan Aspose.PDF.
og_image_alt: Screenshot showing a PDF document with a drawn rectangle on a blank
  page
og_title: Buat Dokumen PDF dengan Halaman Kosong dan Persegi Panjang – Panduan C#
schemas:
- author: Aspose
  dateModified: '2026-09-05'
  description: Create PDF document in C# by adding a blank page, drawing a rectangle,
    and saving the PDF file. Follow a step‑by‑step Aspose.PDF example.
  headline: How to create PDF document with a blank page and rectangle
  type: TechArticle
- description: Create PDF document in C# by adding a blank page, drawing a rectangle,
    and saving the PDF file. Follow a step‑by‑step Aspose.PDF example.
  name: How to create PDF document with a blank page and rectangle
  steps:
  - name: 'Edge case: custom page size'
    text: 'If your layout requires a 6 × 9 inch page, replace the default call with:'
  - name: 'Pro tip: styling the rectangle'
    text: 'You can change the stroke color and line width:'
  - name: 'Edge case: overwriting existing files'
    text: 'Aspose.PDF overwrites an existing file by default. To protect previous
      outputs, check for file existence first:'
  - name: Expected output
    text: Running the program creates a single‑page PDF. When you open `output.pdf`
      you will see a blank white page with a red rectangle positioned 100 points from
      the left and bottom edges, measuring 200 × 200 points.
  type: HowTo
tags:
- PDF
- C#
- Aspose.PDF
- PDF generation
title: Cara membuat dokumen PDF dengan halaman kosong dan persegi panjang
url: /id/net/document-creation/how-to-create-pdf-document-with-a-blank-page-and-rectangle/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara membuat PDF document dengan halaman kosong dan persegi panjang

Jika Anda perlu **create PDF document** secara programatis, panduan ini menunjukkan solusi lengkap dalam C#. Anda akan belajar cara menambahkan halaman kosong, menggambar persegi panjang pada halaman tersebut, dan akhirnya menyimpan file PDF. Contoh ini menggunakan pustaka Aspose.PDF, yang bekerja dengan .NET 6+ dan .NET Framework 4.5+.

Menambahkan halaman kosong dan menggambar bentuk adalah kebutuhan umum untuk faktur, sertifikat, atau laporan khusus. Pada akhir tutorial ini Anda akan memiliki proyek yang dapat dijalankan yang menghasilkan PDF berisi satu persegi panjang yang ditempatkan pada (100, 100) dengan ukuran 200 × 200 poin.

## Prasyarat

* Visual Studio 2022 (atau IDE C# apa pun)
* .NET 6 SDK atau .NET Framework 4.5+
* Aspose.PDF for .NET NuGet package  
  ```bash
  dotnet add package Aspose.PDF
  ```
* Izin menulis ke direktori output

Tidak ada konfigurasi tambahan yang diperlukan; kode dapat dijalankan langsung.

## Membuat PDF document – ikhtisar

Seluruh proses terdiri dari empat langkah logis:

1. **Instantiate** sebuah objek `Document` – ini mewakili file PDF.
2. **Add a blank page** – halaman menyediakan kanvas untuk menggambar.
3. **Draw a rectangle** – sebuah objek `Path` mendefinisikan bentuk.
4. **Save the PDF file** – menyimpan dokumen ke disk.

Setiap langkah diisolasi dalam bagiannya masing‑masing sehingga Anda dapat menggunakan kembali atau mengganti bagian sesuai kebutuhan.

![Diagram of a PDF with a rectangle on a blank page](https://example.com/placeholder-image.png){.img-fluid alt="Tangkapan layar yang menunjukkan dokumen PDF dengan persegi panjang yang digambar pada halaman kosong"}

## Tambahkan halaman kosong pdf

Sebuah PDF harus berisi setidaknya satu halaman sebelum grafik apa pun dapat ditempatkan. Metode `Pages.Add()` membuat halaman kosong dengan dimensi default (A4). Jika Anda memerlukan ukuran berbeda, berikan argumen `PageSize`.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

// Step 1: Create a new PDF document
using var pdfDocument = new Document();

// Step 2: Add a blank page to the document
Page pdfPage = pdfDocument.Pages.Add();   // adds an A4 page by default
```

*Why this step matters* – Objek halaman menyimpan koleksi untuk teks, gambar, dan grafik vektor. Tanpa halaman, setiap upaya menambahkan persegi panjang akan memunculkan pengecualian.

### Kasus tepi: ukuran halaman khusus

Jika tata letak Anda memerlukan halaman 6 × 9 inci, ganti pemanggilan default dengan:

```csharp
var pageSize = new Size(432, 648); // 72 points per inch
Page pdfPage = pdfDocument.Pages.Add(pageSize);
```

## Gambar persegi panjang pdf

Menggambar persegi panjang melibatkan pembuatan geometri `Rectangle` dan membungkusnya dalam `Path`. Pemanggilan `ValidateBounds()` memastikan bentuk tersebut berada di dalam margin halaman, mencegah pemotongan.

```csharp
// Step 3: Define a rectangle shape (x, y, width, height)
Rectangle shapeRect = new Rectangle(100, 100, 200, 200);

// Step 4: Add the rectangle to the page contents
Path rectanglePath = new Path(shapeRect).ValidateBounds();
pdfPage.Contents.Add(rectanglePath);
```

*Why this step matters* – Objek `Path` adalah primitif vektor tingkat rendah yang digunakan oleh Aspose.PDF. Dengan memvalidasi batas, Anda menghindari kesalahan runtime ketika persegi panjang melebihi batas halaman.

### Tips pro: menata persegi panjang

Anda dapat mengubah warna garis tepi dan lebar garis:

```csharp
rectanglePath.GraphInfo = new GraphInfo
{
    StrokeColor = Color.Red,
    LineWidth = 2
};
```

Ini menghasilkan outline berwarna merah dengan ketebalan 2‑poin.

## Simpan file pdf

Menyimpan dokumen menyelesaikan file di disk. Metode `Save` menerima jalur file atau stream. Menyediakan jalur absolut membuat lokasi menjadi jelas, yang berguna untuk skrip otomatisasi.

```csharp
// Step 5: Save the PDF to a file
string outputPath = Path.Combine(Environment.CurrentDirectory, "output.pdf");
pdfDocument.Save(outputPath);
Console.WriteLine($"PDF saved to {outputPath}");
```

*Why this step matters* – Penyimpanan adalah satu‑satunya titik di mana representasi dalam memori menjadi file fisik. Jika Anda perlu mengembalikan PDF dari web API, ganti jalur file dengan `MemoryStream`.

### Kasus tepi: menimpa file yang ada

Aspose.PDF secara default menimpa file yang ada. Untuk melindungi output sebelumnya, periksa keberadaan file terlebih dahulu:

```csharp
if (File.Exists(outputPath))
{
    File.Delete(outputPath);
}
pdfDocument.Save(outputPath);
```

## Cara menambahkan persegi panjang – praktik terbaik

* **Keep coordinates within the page margins** – gunakan `ValidateBounds()` atau hitung margin secara manual.
* **Reuse `GraphInfo` objects** saat menggambar beberapa bentuk; ini mengurangi alokasi memori.
* **Dispose of the `Document` object** (seperti yang ditunjukkan dengan `using var`) untuk membebaskan sumber daya native dengan cepat.
* **Test with different DPI settings** jika Anda kemudian menyisipkan gambar raster; bentuk vektor seperti persegi panjang tetap tajam pada resolusi apa pun.

## Contoh kerja lengkap

Berikut adalah program lengkap yang dapat Anda salin ke aplikasi konsol. Program ini dapat dikompilasi tanpa modifikasi dan menghasilkan `output.pdf` di folder proyek.

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using Aspose.Pdf.Color;

class Program
{
    static void Main()
    {
        // Create a new PDF document
        using var pdfDocument = new Document();

        // Add a blank page to the document
        Page pdfPage = pdfDocument.Pages.Add();

        // Define a rectangle shape (x, y, width, height)
        Rectangle shapeRect = new Rectangle(100, 100, 200, 200);

        // Create a path for the rectangle and validate its bounds
        Path rectanglePath = new Path(shapeRect).ValidateBounds();

        // Optional: style the rectangle (red outline, 2‑pt width)
        rectanglePath.GraphInfo = new GraphInfo
        {
            StrokeColor = Color.Red,
            LineWidth = 2
        };

        // Add the rectangle to the page contents
        pdfPage.Contents.Add(rectanglePath);

        // Determine output path
        string outputPath = Path.Combine(Environment.CurrentDirectory, "output.pdf");

        // Ensure no leftover file blocks the save operation
        if (File.Exists(outputPath))
        {
            File.Delete(outputPath);
        }

        // Save the PDF to a file
        pdfDocument.Save(outputPath);
        Console.WriteLine($"PDF saved to {outputPath}");
    }
}
```

### Output yang diharapkan

Menjalankan program membuat PDF satu‑halaman. Saat Anda membuka `output.pdf`, Anda akan melihat halaman putih kosong dengan persegi panjang merah yang ditempatkan 100 poin dari tepi kiri dan bawah, berukuran 200 × 200 poin.

## Kesimpulan

Anda kini tahu cara **create PDF document**, **add blank page pdf**, **draw rectangle pdf**, dan **save pdf file** menggunakan Aspose.PDF dalam C#. Contoh ini mencakup panggilan API penting, menjelaskan mengapa setiap panggilan diperlukan, dan memberikan tips untuk variasi umum seperti ukuran halaman khusus atau penataan persegi panjang.

Selanjutnya, jelajahi topik terkait seperti **adding text**, **embedding images**, atau **creating multi‑page reports**. Pola yang sama—menginstansiasi `Document`, memanipulasi halaman, menambahkan konten vektor atau raster, lalu `Save`—berlaku untuk semua skenario tersebut. Silakan bereksperimen dengan bentuk, warna, dan tata letak halaman yang berbeda untuk menyesuaikan kebutuhan proyek Anda.

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan menjelajahi pendekatan implementasi alternatif dalam proyek Anda.

- [Buat Dokumen PDF C# – Tambah Halaman, Gambar Persegi Panjang & Simpan](/pdf/english/net/document-creation/create-pdf-document-c-add-page-draw-rectangle-save/)
- [Buat Dokumen PDF dengan Aspose.PDF – Panduan Langkah‑per‑Langkah](/pdf/english/net/document-creation/create-pdf-document-with-aspose-pdf-step-by-step-guide/)
- [Buat Dokumen PDF dengan Aspose – Tambah Halaman, Kotak Teks, dan Formulir](/pdf/english/net/forms-annotations/create-pdf-document-with-aspose-add-page-text-box-and-form/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}