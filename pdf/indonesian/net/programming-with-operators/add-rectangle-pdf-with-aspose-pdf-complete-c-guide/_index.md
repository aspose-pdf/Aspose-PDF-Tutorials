---
category: general
date: 2026-07-20
description: Tambahkan persegi panjang ke PDF menggunakan Aspose.Pdf dalam C#. Pelajari
  cara memuat PDF yang ada, membuat persegi panjang berwarna, dan menyimpan PDF yang
  telah dimodifikasi dalam beberapa langkah mudah.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add rectangle PDF
- load existing pdf
- save modified pdf
- how to add shape pdf
- create colored rectangle
language: id
lastmod: 2026-07-20
og_description: Tambahkan persegi panjang ke PDF dengan cepat. Panduan ini menunjukkan
  cara memuat PDF yang ada, membuat bentuk persegi panjang berwarna, dan menyimpan
  PDF yang telah dimodifikasi menggunakan Aspose.Pdf.
og_image_alt: Screenshot showing a green rectangle added to a PDF page – add rectangle
  PDF example
og_title: Menambahkan Persegi Panjang ke PDF dengan Aspose.Pdf – Tutorial C# Cepat
schemas:
- author: Aspose
  dateModified: '2026-07-20'
  description: Add rectangle PDF using Aspose.Pdf in C#. Learn how to load existing
    PDF, create colored rectangle, and save modified PDF in a few easy steps.
  headline: Add rectangle PDF with Aspose.Pdf – Complete C# Guide
  type: TechArticle
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Menambahkan Persegi Panjang pada PDF dengan Aspose.Pdf – Panduan Lengkap C#
url: /id/net/programming-with-operators/add-rectangle-pdf-with-aspose-pdf-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tambahkan rectangle PDF – Panduan Lengkap C#

Pernah bertanya‑tanya **bagaimana cara menambahkan rectangle PDF** tanpa harus berurusan dengan aliran PDF tingkat‑rendah? Anda tidak sendirian. Banyak pengembang perlu **memuat file PDF yang ada**, menggambar sebuah bentuk, dan kemudian **menyimpan file PDF yang dimodifikasi**—semuanya dengan cara yang bersih dan dapat diulang. Dalam tutorial ini kami akan membahas langkah demi langkah, menggunakan pustaka Aspose.Pdf yang kuat untuk .NET.

Kami akan mencakup semua hal mulai dari mengambil dokumen kosong dari disk, memeriksa apakah bentuk kita muat, melukis rectangle berwarna hijau, dan akhirnya menyimpan perubahan. Pada akhir tutorial Anda akan memiliki contoh yang siap dijalankan dan dapat ditempatkan di proyek C# mana pun. Mari kita mulai.

## Prasyarat

Sebelum memulai, pastikan Anda memiliki:

- **.NET 6.0** (atau versi .NET terbaru) terpasang.
- Paket NuGet **Aspose.Pdf for .NET** (`Install-Package Aspose.Pdf`).
- Sebuah file PDF untuk dikerjakan – kami mengasumsikan `Blank.pdf` berada di `YOUR_DIRECTORY`.
- Pemahaman dasar tentang sintaks C# (tidak diperlukan hal yang rumit).

> **Pro tip:** Jika Anda menggunakan Visual Studio, klik kanan proyek → *Manage NuGet Packages* → cari *Aspose.Pdf* dan instal rilis stabil terbaru.

## Langkah 1: Muat PDF yang Ada

Hal pertama yang harus Anda lakukan adalah memuat PDF ke memori. Kelas `Document` milik Aspose.Pdf menangani ini dalam satu baris.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using System.Drawing;   // For Color

// Load the source PDF (replace the path with your actual location)
Document pdfDocument = new Document("YOUR_DIRECTORY/Blank.pdf");
```

**Mengapa ini penting:** Memuat file memberi Anda akses ke koleksi halaman, metadata, dan opsi rendering. Jika file tidak ada, Aspose akan melempar `FileNotFoundException`, jadi periksa kembali path-nya.

## Langkah 2: Ambil Halaman Target

Sebagian besar skenario penambahan bentuk berfokus pada satu halaman – biasanya halaman pertama. Anda dapat mengambilnya dengan indeks (Aspose menggunakan indeks berbasis 1).

```csharp
// Access the first page (pages are 1‑based)
Page firstPage = pdfDocument.Pages[1];
```

> **Catatan:** Mencoba mengakses nomor halaman yang tidak ada akan memicu `ArgumentOutOfRangeException`. Selalu pastikan dokumen memiliki cukup halaman sebelum mengindeks.

## Langkah 3: Definisikan Geometri Rectangle

Rectangle dalam istilah PDF hanyalah struktur `Rectangle` dengan empat koordinat: `llx, lly, urx, ury` (lower‑left X/Y, upper‑right X/Y). Mari buat rectangle yang lebih besar dari halaman A4 tipikal untuk mengilustrasikan pengecekan batas.

```csharp
// Rectangle larger than most pages (units are points; 72 points = 1 inch)
Rectangle shapeRect = new Rectangle(0, 0, 1200, 1200);
```

Jika Anda menginginkan rectangle yang pas, gunakan dimensi seperti `200, 200, 400, 400`. Koordinat diukur dari sudut kiri‑bawah halaman.

## Langkah 4: Validasi Bentuk terhadap Batas Halaman

Menambahkan bentuk yang melampaui halaman dapat merusak tata letak. Aspose menyediakan `IsShapeInsideBounds` untuk mempermudah proses ini.

```csharp
if (firstPage.IsShapeInsideBounds(shapeRect))
{
    // Shape fits – we can safely add it
}
else
{
    Console.WriteLine("Shape exceeds page boundaries – not added.");
}
```

**Mengapa dicek?** Beberapa penampil PDF memotong konten yang meluber secara diam‑diam, sementara yang lain mungkin menampilkannya secara aneh. Validasi membuat output Anda dapat diprediksi.

## Langkah 5: Tambahkan Rectangle Berwarna ke Halaman

Sekarang bagian yang menyenangkan: membuat **rectangle berwarna** dan menempelkannya ke koleksi paragraf halaman. Kami akan menggunakan isi berwarna hijau untuk visibilitas.

```csharp
if (firstPage.IsShapeInsideBounds(shapeRect))
{
    // Create the rectangle fragment with a green fill
    RectangleFragment rectFragment = new RectangleFragment(shapeRect)
    {
        FillColor = Color.Green,      // Fill the shape with green
        Border = new BorderInfo(BorderSide.All, 1) // Optional thin border
    };

    // Add the rectangle to the page
    firstPage.Paragraphs.Add(rectFragment);
}
```

**Penjelasan:**  
- `RectangleFragment` adalah objek ringan yang mewakili sebuah bentuk.  
- `FillColor` menentukan warna interior; Anda dapat menggunakan `System.Drawing.Color` apa saja.  
- Menambahkannya ke `Paragraphs` memastikan bentuk menghormati alur konten halaman.

### Kasus Pinggir & Variasi

- **Warna berbeda:** Ganti `Color.Green` dengan `Color.FromArgb(255, 0, 0)` untuk merah, atau nilai ARGB apa pun.  
- **Transparansi:** Gunakan `rectFragment.FillColor = Color.FromArgb(128, 0, 255, 0)` untuk opasitas 50 %.  
- **Sudut melengkung:** Aspose tidak mendukung rectangle dengan sudut melengkung secara langsung, tetapi Anda dapat menumpuk `EllipseFragment` untuk mensimulasikannya.  
- **Banyak bentuk:** Cukup ulangi blok pembuatan dengan koordinat baru dan tambahkan setiap fragmen ke `firstPage.Paragraphs`.

## Langkah 6: Simpan PDF yang Dimodifikasi

Akhirnya, tulis perubahan kembali ke disk. Anda dapat menimpa file asli atau membuat file baru – kami akan membuat file baru agar sumber tetap tidak berubah.

```csharp
// Save the updated document
pdfDocument.Save("YOUR_DIRECTORY/ShapeValidated.pdf");
Console.WriteLine("PDF saved successfully with the green rectangle.");
```

**Mengapa file terpisah?** Menjaga file asli memungkinkan Anda menjalankan skrip berulang kali tanpa perubahan kumulatif, yang sangat berguna saat pengujian.

## Contoh Lengkap yang Siap Dijalan

Menggabungkan semuanya, berikut program lengkap yang siap dijalankan:

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using System;
using System.Drawing;   // For Color

class Program
{
    static void Main()
    {
        // 1️⃣ Load the existing PDF
        Document pdfDocument = new Document("YOUR_DIRECTORY/Blank.pdf");

        // 2️⃣ Get the first page
        Page firstPage = pdfDocument.Pages[1];

        // 3️⃣ Define a rectangle (change dimensions as needed)
        Rectangle shapeRect = new Rectangle(0, 0, 1200, 1200);

        // 4️⃣ Verify bounds
        if (firstPage.IsShapeInsideBounds(shapeRect))
        {
            // 5️⃣ Create and add a green rectangle
            RectangleFragment rectFragment = new RectangleFragment(shapeRect)
            {
                FillColor = Color.Green,
                Border = new BorderInfo(BorderSide.All, 1)
            };
            firstPage.Paragraphs.Add(rectFragment);
        }
        else
        {
            Console.WriteLine("Shape exceeds page boundaries – not added.");
        }

        // 6️⃣ Save the modified PDF
        pdfDocument.Save("YOUR_DIRECTORY/ShapeValidated.pdf");
        Console.WriteLine("PDF saved successfully with the green rectangle.");
    }
}
```

**Output yang diharapkan:** Setelah dijalankan, buka `ShapeValidated.pdf`. Anda akan melihat rectangle hijau solid yang ditempatkan di sudut kiri‑bawah, menutupi area yang didefinisikan oleh koordinat. Jika rectangle terlalu besar, konsol akan mencetak pesan peringatan sebagai gantinya.

## Pertanyaan Umum & Pemecahan Masalah

- **“Mengapa rectangle saya muncul tidak terpusat?”**  
  Koordinat PDF dimulai dari kiri‑bawah, bukan kiri‑atas. Sesuaikan `llx` dan `lly` untuk menggerakkan bentuk ke atas atau ke kanan.

- **“Bisakah saya menambahkan rectangle ke lapisan tertentu?”**  
  Ya. Gunakan `pdfDocument.Pages[1].Resources.Layers.Add` untuk membuat lapisan, lalu tetapkan `rectFragment.Layer = yourLayer`.

- **“PDF saya dilindungi password—apakah saya masih bisa menambahkan bentuk?”**  
  Muat dengan `new Document(path, password)` lalu ikuti langkah yang sama. Ingat untuk menerapkan kembali pengaturan keamanan sebelum menyimpan jika diperlukan.

- **“Bagaimana jika saya perlu menambahkan rectangle ke setiap halaman?”**  
  Loop melalui `pdfDocument.Pages` dan ulangi langkah 3‑5 untuk setiap objek `Page`.

## Kesimpulan

Anda kini memiliki pemahaman kuat tentang **cara menambahkan rectangle PDF** menggunakan Aspose.Pdf di C#. Dari **memuat PDF yang ada**, **memvalidasi batas bentuk**, **membuat rectangle berwarna**, hingga **menyimpan PDF yang dimodifikasi**, setiap langkah dibahas lengkap dengan penjelasan dan kode yang dapat langsung disalin ke proyek Anda.

Selanjutnya, Anda dapat menjelajahi penambahan bentuk lain (`EllipseFragment`, `PolygonFragment`), menyisipkan gambar, atau bahkan menghasilkan PDF dari awal. Semua topik tersebut terkait dengan kata kunci sekunder **load existing pdf**, **save modified pdf**, **how to add shape pdf**, dan **create colored rectangle**, sehingga Anda siap memperluas toolkit manipulasi PDF Anda.

Ada trik yang Anda coba? Bagikan pengalaman Anda di kolom komentar, atau ajukan pertanyaan yang masih tersisa. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Create PDF Document with Aspose.PDF – Add Page, Shape & Save](/pdf/english/net/document-creation/create-pdf-document-with-aspose-pdf-add-page-shape-save/)
- [Create Fill Rectangle Aspose Pdf Net](/pdf/english/net/images-graphics/create-fill-rectangle-aspose-pdf-net/)
- [How to Create PDF with Aspose – Add Form Field and Pages](/pdf/english/net/programming-with-forms/how-to-create-pdf-with-aspose-add-form-field-and-pages/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}