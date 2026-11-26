---
category: general
date: 2026-11-25
description: Pelajari cara menyimpan PDF yang dimodifikasi, menambahkan penomoran
  Bates pada PDF, dan menyisipkan bentuk khusus pada PDF menggunakan Aspose.PDF untuk
  C# dalam panduan langkah demi langkah yang lengkap.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save modified pdf
- add bates numbering pdf
- add bates numbers pdf
- add custom shape pdf
- load pdf document c#
language: id
lastmod: 2026-11-25
og_description: Simpan PDF yang dimodifikasi dengan Aspose.PDF untuk C#. Panduan ini
  menunjukkan cara menambahkan penomoran Bates pada PDF, menambahkan bentuk khusus
  pada PDF, dan memuat dokumen PDF C# secara efisien.
og_image_alt: Screenshot of a C# program that saves modified PDF after adding Bates
  numbering and a custom shape
og_title: Simpan PDF yang dimodifikasi dan tambahkan penomoran Bates di C# – tutorial
  lengkap
schemas:
- author: Aspose
  dateModified: '2026-11-25'
  description: Learn how to save modified PDF, add Bates numbering PDF, and insert
    a custom shape PDF using Aspose.PDF for C# in a complete step‑by‑step guide.
  headline: How to save modified PDF and add Bates numbering in C#
  type: TechArticle
tags:
- PDF
- C#
- Aspose.PDF
title: Cara menyimpan PDF yang dimodifikasi dan menambahkan penomoran Bates di C#
url: /id/net/document-manipulation/how-to-save-modified-pdf-and-add-bates-numbering-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara menyimpan PDF yang dimodifikasi dan menambahkan penomoran Bates di C#

Jika Anda perlu **menyimpan PDF yang dimodifikasi** setelah menerapkan penomoran Bates bergaya hukum, solusinya ada di sini. Tutorial ini memandu Anda melalui proses memuat dokumen PDF di C#, menambahkan nomor Bates, menyisipkan bentuk khusus, dan akhirnya **menyimpan PDF yang dimodifikasi** dengan Aspose.PDF. Baik Anda menyiapkan berkas kasus maupun mengotomatisasi alur kerja dokumen, Anda akan mendapatkan contoh lengkap yang dapat dijalankan.

Anda juga akan melihat cara **load PDF document C#** code, mendeteksi tanda tangan digital yang terkompromi, dan memverifikasi batas bentuk—semua yang Anda butuhkan untuk membangun pipeline pemrosesan PDF yang kuat. Pada akhir panduan ini Anda akan dapat menjalankan contoh dan menghasilkan PDF yang berisi nomor Bates berurutan, grafik khusus, dan modifikasi lain yang Anda perlukan.

## Prasyarat

| Persyaratan | Alasan |
|-------------|--------|
| .NET 6.0 atau lebih baru | Menyediakan runtime untuk proyek C# |
| Visual Studio 2022 (atau IDE C# apa pun) | Memungkinkan pengeditan dan debugging yang mudah |
| Aspose.PDF untuk .NET (paket NuGet `Aspose.Pdf`) | Menyediakan API manipulasi PDF |
| File PDF input (`input.pdf`) | Berfungsi sebagai dokumen sumber |

Pastikan paket Aspose.PDF telah terinstal:

```bash
dotnet add package Aspose.Pdf
```

## Langkah 1: Load PDF document C# – menginisialisasi file sumber

Operasi pertama adalah membaca PDF yang ada ke dalam memori. Menggunakan kelas `Document` memberi Anda akses penuh ke halaman, tanda tangan, dan struktur tingkat rendah lainnya.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Facades;

// Load the PDF document from disk
var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");

// Optional: verify the document opened correctly
if (pdfDocument.Pages.Count == 0)
{
    throw new InvalidOperationException("The input PDF contains no pages.");
}
```

**Mengapa ini penting:** Memuat file adalah dasar bagi semua perubahan selanjutnya. Jika dokumen gagal dimuat, langkah-langkah berikutnya seperti **add bates numbering pdf** atau **add custom shape pdf** akan menghasilkan pengecualian.

## Langkah 2: Deteksi tanda tangan digital yang terkompromi (pemeriksaan keamanan)

Dokumen hukum sering kali memiliki tanda tangan digital. Sebelum Anda memodifikasi file, sebaiknya memeriksa apakah ada tanda tangan yang telah diubah.

```csharp
// Detect any compromised digital signatures
var compromisedSignatures = pdfDocument.DigitalSignatures.DetectCompromisedSignatures();

if (compromisedSignatures.Count > 0)
{
    Console.WriteLine("Warning: Compromised signatures detected.");
    // You may choose to abort or log details here
}
```

**Mengapa ini penting:** Memodifikasi PDF yang ditandatangani dapat membuat tanda tangan tidak valid. Mendeteksi tanda tangan yang terkompromi memungkinkan Anda memutuskan apakah akan mempertahankan, menghapus, atau menandatangani kembali dokumen setelah perubahan.

## Langkah 3: Tambahkan penomoran Bates PDF – mengonfigurasi awalan dan nomor mulai

Penomoran Bates penting untuk manajemen kasus hukum. Aspose.PDF menyediakan API sederhana untuk mengatur awalan dan nomor mulai.

```csharp
// Configure Bates numbering (starting number and prefix)
pdfDocument.BatesNumbering.Start = 1000;          // Start at 1000
pdfDocument.BatesNumbering.Prefix = "CASE-";     // Prefix for each number
pdfDocument.BatesNumbering.Suffix = "";          // Optional suffix
pdfDocument.BatesNumbering.FontSize = 12;        // Readable font size
pdfDocument.BatesNumbering.Color = Color.Black; // Standard black text
pdfDocument.BatesNumbering.Position = new Position(50, 20); // Bottom‑left corner
```

**Mengapa ini penting:** Objek `BatesNumbering` secara otomatis menempatkan nomor berurutan pada setiap halaman. Menyesuaikan `Position` memungkinkan Anda mengontrol di mana nomor muncul, memastikan tidak menutupi konten yang ada.

## Langkah 4: Tambahkan bentuk khusus PDF – membuat dan memposisikan elemen grafis

Tim hukum kadang perlu menempelkan logo atau menggambar kotak di sekitar paragraf. Aspose.PDF memungkinkan Anda mendefinisikan bentuk melalui objek `Path` dan menempelkannya ke halaman.

```csharp
// Create a custom shape (a simple rectangle in this example)
var shapePath = new Path();
shapePath.PathData = "M 100 200 L 300 200 L 300 400 L 100 400 Z"; // Rectangle path
shapePath.Stroke = new Stroke(Color.Blue, 2); // Blue border, 2pt thickness
shapePath.Fill = new Fill(Color.LightGray);   // Light gray fill

// Verify that the shape stays within page bounds
shapePath.VerifyBounds(); // Throws if the shape exceeds page size

// Add the shape to the first page
pdfDocument.Pages[1].Add(shapePath);
```

**Mengapa ini penting:** Mendefinisikan bentuk melalui sintaks `Path` memberi Anda kontrol tingkat vektor, yang dapat diskalakan dengan bersih untuk perangkat output apa pun. Pemanggilan `VerifyBounds` mencegah kesalahan runtime yang disebabkan oleh bentuk yang meluber keluar halaman.

## Langkah 5: Tambahkan elemen bertag – peningkatan aksesibilitas opsional

Jika Anda perlu meningkatkan aksesibilitas, Anda dapat menambahkan elemen bertag yang dapat diinterpretasikan oleh pembaca layar.

```csharp
var taggedElement = new TaggedElement();
taggedElement.Position = new Position(100, 200); // X=100, Y=200 points
taggedElement.Tag = "Figure"; // Semantic tag
pdfDocument.Pages[1].Add(taggedElement);
```

**Mengapa ini penting:** Elemen bertag membantu kepatuhan PDF/UA, menjadikan dokumen dapat digunakan oleh teknologi bantu.

## Langkah 6: Simpan PDF yang dimodifikasi – menyelesaikan file output

Setelah semua modifikasi diterapkan, Anda **menyimpan PDF yang dimodifikasi** ke lokasi baru. Langkah ini menuliskan perubahan dalam memori kembali ke disk.

```csharp
// Save the modified PDF document
pdfDocument.Save("YOUR_DIRECTORY/output.pdf");

// Confirmation message
Console.WriteLine("Modified PDF saved successfully as output.pdf");
```

**Mengapa ini penting:** Metode `Save` menyelesaikan file, menyematkan nomor Bates, bentuk khusus, dan edit lainnya. Tanpa pemanggilan ini, tidak ada perubahan yang akan tersimpan.

## Contoh lengkap yang dapat dijalankan

Berikut adalah program lengkap yang menggabungkan semua langkah yang dibahas. Salin kode ke dalam proyek konsol baru, sesuaikan jalur file, dan jalankan.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Facades;
using Aspose.Pdf.Drawing; // For Path, Stroke, Fill, etc.

namespace PdfProcessingDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Load the PDF document
            var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");

            // Step 2: Detect compromised digital signatures
            var compromisedSignatures = pdfDocument.DigitalSignatures.DetectCompromisedSignatures();
            if (compromisedSignatures.Count > 0)
            {
                Console.WriteLine("Warning: Compromised signatures detected.");
                // Handle according to business rules
            }

            // Step 3: Configure Bates numbering (add bates numbers pdf)
            pdfDocument.BatesNumbering.Start = 1000;
            pdfDocument.BatesNumbering.Prefix = "CASE-";
            pdfDocument.BatesNumbering.FontSize = 12;
            pdfDocument.BatesNumbering.Color = Color.Black;
            pdfDocument.BatesNumbering.Position = new Position(50, 20);

            // Step 4: Create a custom shape (add custom shape pdf)
            var shapePath = new Path();
            shapePath.PathData = "M 100 200 L 300 200 L 300 400 L 100 400 Z";
            shapePath.Stroke = new Stroke(Color.Blue, 2);
            shapePath.Fill = new Fill(Color.LightGray);
            shapePath.VerifyBounds(); // Ensure shape fits the page
            pdfDocument.Pages[1].Add(shapePath);

            // Step 5: Add a tagged element (optional accessibility aid)
            var taggedElement = new TaggedElement
            {
                Position = new Position(100, 200),
                Tag = "Figure"
            };
            pdfDocument.Pages[1].Add(taggedElement);

            // Step 6: Save the modified PDF (save modified pdf)
            pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
            Console.WriteLine("Modified PDF saved successfully as output.pdf");
        }
    }
}
```

### Output yang diharapkan

Menjalankan program menghasilkan `output.pdf` dengan:

* Nomor Bates seperti `CASE-1000`, `CASE-1001`, … pada setiap halaman.
* Sebuah persegi panjang abu‑abu muda dengan batas biru yang diposisikan pada (100, 200).
* Elemen bertag opsional untuk aksesibilitas.
* Semua konten asli dipertahankan kecuali tanda tangan yang terkompromi terdeteksi (Anda dapat memilih untuk menghentikan).

## Kesimpulan

Anda kini tahu cara **menyimpan PDF yang dimodifikasi** setelah menerapkan **add bates numbering PDF**, menyisipkan **add custom shape pdf**, dan melakukan pemeriksaan keamanan dengan **load PDF document C#**. Contoh lengkap menunjukkan praktik terbaik seperti memverifikasi batas bentuk, menangani tanda tangan digital, dan menggunakan API fluida Aspose.PDF.

Dari sini Anda dapat menjelajahi peningkatan lebih lanjut:

* **Add bates numbers pdf** dengan cap tanggal khusus atau ID kasus.
* Menyisipkan beberapa bentuk atau gambar untuk membuat watermark.
* Menandatangani kembali PDF setelah modifikasi menggunakan `DigitalSignatureFacade`.
* Mengekspor dokumen ke format lain (DOCX, TIFF) menggunakan API konversi Aspose.

Silakan bereksperimen dengan awalan, nomor mulai, atau geometri bentuk yang berbeda untuk menyesuaikan alur kerja organisasi Anda. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Cara Menambahkan Bentuk ke PDF dengan Aspose.PDF di C# – Panduan Langkah demi Langkah](/pdf/english/net/images-graphics/how-to-add-shape-to-pdf-with-aspose-pdf-in-c-step-by-step-gu/)
- [Cara menyimpan PDF yang dimodifikasi dengan Aspose.Pdf dan menambahkan transparansi](/pdf/english/net/document-manipulation/how-to-save-modified-pdf-with-aspose-pdf-and-add-transparenc/)
- [Buat Dokumen PDF dengan Aspose.PDF – Tambahkan Halaman, Bentuk & Simpan](/pdf/english/net/document-creation/create-pdf-document-with-aspose-pdf-add-page-shape-save/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}