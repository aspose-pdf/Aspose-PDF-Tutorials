---
category: general
date: 2026-09-27
description: Tambahkan penomoran Bates ke PDF menggunakan Aspose.PDF dalam C#. Pelajari
  cara memuat dokumen PDF, mengatur opsi penomoran Bates, dan menyimpan file yang
  diperbarui.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add bates numbering
- load pdf document
- how to add bates numbering
- Aspose.PDF C#
- PDF Bates numbering example
language: id
lastmod: 2026-09-27
og_description: Tambahkan penomoran Bates ke PDF menggunakan Aspose.PDF dalam C#.
  Tutorial ini menunjukkan cara memuat dokumen PDF, mengonfigurasi penomoran Bates,
  dan menyimpan hasilnya.
og_image_alt: Screenshot of a PDF page displaying Bates numbers in the footer
og_title: Tambahkan penomoran Bates ke PDF dengan Aspose.PDF – Panduan C#
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Add bates numbering to PDF using Aspose.PDF in C#. Learn how to load
    a PDF document, set Bates numbering options, and save the updated file.
  headline: Add bates numbering to PDF using Aspose.PDF in C#
  type: TechArticle
tags:
- Aspose.PDF
- C#
- PDF processing
title: Tambahkan penomoran Bates ke PDF menggunakan Aspose.PDF di C#
url: /id/net/programming-with-text/add-bates-numbering-to-pdf-using-aspose-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tambahkan penomoran bates ke PDF menggunakan Aspose.PDF di C#

Jika Anda perlu **menambahkan penomoran bates** ke file PDF, panduan ini menunjukkan solusi lengkap yang siap dijalankan. Anda akan melihat cara **memuat dokumen PDF**, mengonfigurasi opsi penomoran Bates, dan menulis file yang telah diberi nomor kembali ke disk—semua dengan Aspose.PDF untuk .NET.

Menerapkan nomor Bates umum dalam alur kerja hukum, penegakan hukum, dan arsip. Pada akhir tutorial ini Anda dapat menyematkan pengidentifikasi berurutan pada setiap halaman, menyesuaikan prefiks, dan memulai hitungan pada nomor berapa pun yang Anda pilih.

## Apa yang akan Anda pelajari

* Cara **memuat konten dokumen PDF** ke dalam objek `Aspose.Pdf.Document`.  
* Langkah tepat **cara menambahkan penomoran bates** dengan `BatesNumberingOptions`.  
* Cara menyimpan file yang telah dimodifikasi sambil mempertahankan tata letak dan kualitas asli.  

Tidak diperlukan alat eksternal—hanya paket Aspose.PDF NuGet dan lingkungan pengembangan .NET (Visual Studio, VS Code, atau Rider).  

---

## Langkah 1: Instal Aspose.PDF untuk .NET

Buka folder proyek Anda di terminal dan jalankan:

```bash
dotnet add package Aspose.PDF
```

Paket ini menyertakan namespace `Aspose.Pdf`, yang menyediakan semua kelas yang digunakan dalam tutorial ini. Setelah instalasi, muat ulang proyek agar IDE mengenali referensi baru.

## Langkah 2: Muat dokumen PDF

Memuat file sumber adalah operasi pertama karena mesin penomoran Bates bekerja pada instance `Document` yang sudah ada.

```csharp
using Aspose.Pdf;

// ...

// Replace with the path to your input PDF
string inputPath = @"YOUR_DIRECTORY\input.pdf";

// Load the PDF document into memory
Document doc = new Document(inputPath);
```

**Mengapa ini penting:** Kelas `Document` mengurai struktur PDF, memberi Anda akses ke halaman, anotasi, dan metadata. Tanpa memuat file terlebih dahulu, Anda tidak dapat menerapkan penomoran apa pun.

## Langkah 3: Konfigurasikan opsi penomoran Bates

Buat objek `BatesNumberingOptions` dan atur prefiks yang diinginkan, nomor mulai, serta parameter format opsional.

```csharp
using Aspose.Pdf;

// ...

BatesNumberingOptions batesOptions = new BatesNumberingOptions
{
    // Text that appears before the numeric part
    Prefix = "CASE01",

    // First number to use (1 means the first page gets CASE01-1)
    StartNumber = 1,

    // Optional: customize the appearance
    // The default places the number in the footer, centered.
    // You can change Font, FontSize, Color, and Position if needed.
    // Example:
    // Font = FontRepository.FindFont("Arial"),
    // FontSize = 10,
    // Color = Color.Black,
    // Margin = new Margin(0, 0, 0, 20)
};
```

**Mengapa ini penting:** `BatesNumberingOptions` memberi tahu Aspose.PDF cara menghasilkan label untuk setiap halaman. `Prefix` membantu Anda mengelompokkan kasus terkait, sementara `StartNumber` memungkinkan Anda melanjutkan urutan dari batch sebelumnya.

## Langkah 4: Simpan PDF dengan penomoran Bates yang diterapkan

Berikan objek opsi ke metode `Save`. Aspose.PDF menulis nomor secara langsung pada setiap halaman.

```csharp
// Replace with the desired output path
string outputPath = @"YOUR_DIRECTORY\output.pdf";

// Save the document, applying the Bates numbering
doc.Save(outputPath, batesOptions);
```

**Mengapa ini penting:** Overload `Save(string, BatesNumberingOptions)` menggabungkan langkah rendering dengan proses penomoran, memastikan file output berisi identifier yang terlihat.

## Contoh lengkap – semua bersama

Berikut adalah program tunggal yang berdiri sendiri yang dapat Anda salin, tempel, dan jalankan. Program ini menunjukkan **cara menambahkan penomoran bates** dari awal hingga selesai.

```csharp
using System;
using Aspose.Pdf;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the PDF document
            string inputPath = @"YOUR_DIRECTORY\input.pdf";
            Document doc = new Document(inputPath);

            // 2️⃣ Set up Bates numbering options
            BatesNumberingOptions batesOptions = new BatesNumberingOptions
            {
                Prefix = "CASE01",
                StartNumber = 1,
                // Optional appearance tweaks:
                // Font = FontRepository.FindFont("Times New Roman"),
                // FontSize = 9,
                // Color = Color.DarkBlue,
                // Margin = new Margin(0, 0, 0, 15)
            };

            // 3️⃣ Save the document with Bates numbers
            string outputPath = @"YOUR_DIRECTORY\output.pdf";
            doc.Save(outputPath, batesOptions);

            Console.WriteLine($"Bates numbering added. Output saved to: {outputPath}");
        }
    }
}
```

### Output yang diharapkan

Menjalankan program menghasilkan `output.pdf` dimana setiap halaman menampilkan label serupa dengan:

```
CASE01-1
CASE01-2
CASE01-3
...
```

Nomor muncul di footer secara default, tetapi Anda dapat memindahkannya dengan menyesuaikan properti `Margin` dalam `BatesNumberingOptions`.

## Kasus tepi dan variasi umum

| Situasi | Apa yang harus disesuaikan |
|-----------|----------------|
| **Prefiks berbeda per batch** | Ubah `Prefix` sebelum memanggil `Save`. Anda dapat melakukan loop pada beberapa dokumen dengan prefiks yang berbeda. |
| **Lanjutkan penomoran dari file sebelumnya** | Setel `StartNumber` ke nomor terakhir yang digunakan + 1. |
| **Tempatkan nomor di header** | Gunakan `batesOptions.Margin = new Margin(20, 0, 0, 0);` (margin atas) atau sesuaikan `batesOptions.Position`. |
| **Font atau warna khusus** | Tetapkan properti `Font`, `FontSize`, dan `Color` seperti yang ditunjukkan pada bagian komentar. |
| **PDF besar (1000+ halaman)** | Operasi ini efisien memori; namun, Anda mungkin ingin mengaktifkan `doc.OptimizeResources()` sebelum menyimpan untuk mengurangi ukuran file. |

**Tips profesional:** Jika alur kerja Anda memerlukan skema penomoran berbeda per dokumen, enkapsulasi logika dalam metode pembantu:

```csharp
static void ApplyBatesNumbering(string src, string dst, string prefix, int start)
{
    var doc = new Document(src);
    var opts = new BatesNumberingOptions { Prefix = prefix, StartNumber = start };
    doc.Save(dst, opts);
}
```

## Kesimpulan

Anda sekarang tahu **cara menambahkan penomoran bates** ke PDF apa pun menggunakan Aspose.PDF di C#. Tutorial ini mencakup memuat dokumen PDF, mengonfigurasi opsi penomoran, dan menyimpan file akhir—semua dalam satu program yang dapat dijalankan.  

Dari sini Anda dapat menjelajahi topik yang sangat terkait seperti **menambahkan watermark**, **menggabungkan beberapa PDF**, atau **mengekstrak teks** dengan Aspose.PDF. Bereksperimenlah dengan berbagai font, warna, dan posisi untuk menyesuaikan standar format organisasi Anda.

Siap mengotomatisasi alur kerja dokumen hukum Anda? Tambahkan kode ke pipeline build Anda, jalankan pada kumpulan file, dan biarkan Aspose.PDF menangani pekerjaan berat. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan menjelajahi pendekatan implementasi alternatif dalam proyek Anda.

- [Buat Dokumen PDF C# – Tambahkan Penomoran Bates](/pdf/english/net/programming-with-pdf-pages/create-pdf-document-c-add-bates-numbering/)
- [Tambahkan Penomoran Bates PDF – Panduan Langkah‑per‑Langkah untuk Menomori Halaman PDF](/pdf/english/net/programming-with-pdf-pages/add-bates-numbering-pdf-step-by-step-guide-to-number-pdf-pag/)
- [Tutorial Aspose PDF – Sisipkan Halaman Kosong dan Perbarui Penomoran Bates](/pdf/english/net/programming-with-pdf-pages/aspose-pdf-tutorial-insert-a-blank-page-and-update-bates-num/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}