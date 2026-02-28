---
category: general
date: 2026-02-28
description: Buat dokumen PDF C# dengan penomoran Bates. Pelajari cara menambahkan
  penomoran Bates pada PDF, mengatur awalan, dan menghasilkan nomor PDF berurutan
  dalam satu panduan.
draft: false
keywords:
- create pdf document c#
- add bates numbering pdf
- how to add bates
- add document identification numbers
- add sequential pdf numbers
language: id
og_description: Buat dokumen PDF C# dengan penomoran Bates. Tutorial ini menunjukkan
  cara menambahkan penomoran Bates pada PDF, mengatur awalan khusus, dan menghasilkan
  nomor PDF berurutan.
og_title: Buat Dokumen PDF C# – Tambahkan Penomoran Bates
tags:
- Aspose.PDF
- C#
- PDF automation
title: Buat Dokumen PDF C# – Panduan Penomoran Bates
url: /id/net/document-creation/create-pdf-document-c-add-bates-numbering-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat Dokumen PDF C# – Panduan Penambahan Penomoran Bates

Pernah bertanya-tanya bagaimana cara **create PDF document C#** yang sudah memiliki identifier unik pada setiap halaman? Itu adalah masalah umum ketika Anda harus melacak berkas hukum, pengajuan ke pengadilan, atau kumpulan PDF yang harus dapat dicari berdasarkan nomor. Kabar baik? Dengan Aspose.PDF Anda dapat menambahkan nomor Bates hanya dengan beberapa baris kode—tanpa perlu penyuntingan manual.

Dalam panduan ini kami akan menjelaskan seluruh proses: memuat PDF yang sudah ada, mengonfigurasi **add bates numbering pdf**, menerapkan nomor, dan akhirnya menyimpan hasilnya. Pada akhir tutorial Anda akan dapat **add document identification numbers** dan bahkan **add sequential PDF numbers** secara otomatis, semuanya dari C#.

## Prasyarat

- .NET 6.0 atau lebih baru (API bekerja dengan .NET Framework 4.5+ juga)
- Salinan berlisensi **Aspose.PDF for .NET** (versi percobaan gratis dapat digunakan untuk pengujian)
- File PDF input yang ingin Anda beri nomor (kami akan menyebutnya `input.pdf`)
- Visual Studio 2022 (atau IDE apa pun yang Anda sukai)

Tidak diperlukan paket NuGet tambahan selain Aspose.PDF.

![Create PDF Document C# with Bates numbering](https://example.com/image.png "Create PDF Document C# example")

## Langkah 1: Muat Dokumen PDF Sumber

Sebelum Anda dapat **add bates numbering pdf**, Anda memerlukan objek `Document` yang mewakili file di disk.

```csharp
using Aspose.Pdf;

// Load the source PDF document
var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");
```

*Mengapa ini penting*: Kelas `Document` adalah titik masuk untuk setiap operasi di Aspose.PDF. Ia mengabstraksi sistem file, sehingga Anda dapat bekerja dengan halaman, anotasi, dan metadata tanpa menyentuh byte mentah.

> **Tips profesional:** Jika Anda memproses banyak file dalam sebuah loop, gunakan kembali instance `Document` yang sama hanya ketika sumbernya identik; jika tidak, buat objek baru untuk setiap file guna menghindari kebocoran memori.

## Langkah 2: Tentukan Opsi Penomoran Bates

Di sinilah bagian **how to add bates** menjadi konkret. Anda mengonfigurasi objek `BatesNumberingOptions` untuk memberi tahu Aspose apa prefix yang harus digunakan, dari mana memulai, dan seberapa besar ukuran font yang harus muncul.

```csharp
// Define Bates numbering options (prefix, start number, font size)
var batesOptions = new BatesNumberingOptions
{
    Prefix = "ABC-",   // You can change this to any string you need
    Start = 1000,      // Starting number – useful for continuous numbering across batches
    FontSize = 9       // Small enough to fit in the margin but still readable
};
```

*Mengapa ini penting*: `Prefix` memungkinkan Anda menyematkan identifier kasus (misalnya “ABC-”). Properti `Start` penting ketika Anda **adding sequential PDF numbers** di beberapa dokumen—cukup tingkatkan nilainya. Dan `FontSize` memastikan nomor tidak menghalangi konten yang ada.

## Langkah 3: Terapkan Penomoran Bates ke Seluruh Dokumen

Sekarang kita benar‑benar menempelkan nomor pada setiap halaman. Kelas `BatesNumbering` melakukan semua pekerjaan berat.

```csharp
// Apply Bates numbering to the entire document
var bates = new BatesNumbering();
bates.AddBatesNumbering(pdfDocument, batesOptions);
```

*Mengapa ini penting*: Di balik layar, Aspose berjalan melalui setiap halaman, menghitung nomor yang tepat (Prefix + (Start + pageIndex)), dan menggambarnya di pojok kanan‑bawah secara default. Anda dapat menyesuaikan posisi nanti, tetapi defaultnya sudah cukup untuk kebanyakan dokumen bergaya hukum.

> **Pertanyaan umum:** *Bagaimana jika saya hanya perlu menomori sebagian halaman?*  
> Gunakan overload `AddBatesNumbering(Document, BatesNumberingOptions, int startPage, int endPage)` untuk membatasi rentang.

## Langkah 4: Simpan PDF dengan Penomoran Bates yang Diterapkan

Langkah terakhir adalah menulis dokumen yang telah dimodifikasi kembali ke disk.

```csharp
// Save the PDF with Bates numbers applied
pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
```

*Mengapa ini penting*: Metode `Save` menghormati format file asli, sehingga Anda mendapatkan PDF standar yang dapat dibuka oleh viewer apa pun—lengkap dengan **add document identification numbers** pada setiap halaman.

## Contoh Kerja Penuh

Menggabungkan semuanya, berikut program mandiri yang dapat Anda tempel ke aplikasi console baru dan jalankan langsung.

```csharp
using System;
using Aspose.Pdf;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the source PDF document
            var inputPath = @"YOUR_DIRECTORY/input.pdf";
            var pdfDocument = new Document(inputPath);

            // 2️⃣ Define Bates numbering options (prefix, start number, font size)
            var batesOptions = new BatesNumberingOptions
            {
                Prefix = "ABC-",
                Start = 1000,
                FontSize = 9
            };

            // 3️⃣ Apply Bates numbering to the entire document
            var bates = new BatesNumbering();
            bates.AddBatesNumbering(pdfDocument, batesOptions);

            // 4️⃣ Save the PDF with Bates numbers applied
            var outputPath = @"YOUR_DIRECTORY/output.pdf";
            pdfDocument.Save(outputPath);

            Console.WriteLine($"Bates numbering added successfully. Output saved to {outputPath}");
        }
    }
}
```

**Hasil yang diharapkan:** Buka `output.pdf` di viewer apa pun; Anda akan melihat “ABC‑1000”, “ABC‑1001”, … tercetak di pojok kanan‑bawah setiap halaman. Nomor‑nomor tersebut berupa teks yang dapat dipilih, sehingga dapat dicari dan disalin—tepat seperti yang Anda harapkan dari implementasi **add sequential PDF numbers** yang tepat.

## Kasus Tepi & Variasi

### Penempatan Kustom

Jika sudut default bertabrakan dengan footer yang ada, Anda dapat menggeser penempatan:

```csharp
batesOptions.Position = new Position(10, 10); // X, Y from the bottom‑left
```

### Format Nomor Berbeda

Ingin nomor berformat nol‑padded (misalnya 001000)? Gunakan `NumberFormat`:

```csharp
batesOptions.NumberFormat = "D6"; // Pads to 6 digits
```

### Banyak File dalam Batch

Saat memproses banyak PDF, pertahankan counter yang berjalan:

```csharp
int globalStart = 5000;
foreach (var file in Directory.GetFiles(@"YOUR_DIRECTORY\Batch", "*.pdf"))
{
    var doc = new Document(file);
    var opts = new BatesNumberingOptions
    {
        Prefix = "BATCH-",
        Start = globalStart,
        FontSize = 9
    };
    new BatesNumbering().AddBatesNumbering(doc, opts);
    doc.Save(Path.ChangeExtension(file, ".bated.pdf"));
    globalStart += doc.Pages.Count; // Increment for the next file
}
```

### Menangani PDF yang Dilindungi Kata Sandi

Jika PDF sumber dienkripsi, berikan kata sandi saat membuat `Document`:

```csharp
var pdfDocument = new Document("protected.pdf", new LoadOptions { Password = "mySecret" });
```

## Pertanyaan yang Sering Diajukan

| Pertanyaan | Jawaban |
|------------|---------|
| **Bisakah saya menggunakan library lain?** | Ya, library seperti iTextSharp atau PdfSharp juga mendukung penyisipan teks tingkat halaman, tetapi Aspose.PDF menawarkan API paling sederhana untuk penomoran Bates. |
| **Apakah ini memengaruhi ukuran file?** | Menambahkan beberapa byte teks per halaman hampir tidak terasa; ukuran output biasanya bertambah kurang dari 1 KB per halaman. |
| **Apakah penomoran dapat dicari?** | Tentu saja. Aspose menulis nomor sebagai objek teks, bukan sebagai gambar, sehingga dapat diindeks oleh pembaca PDF. |
| **Bagaimana jika saya membutuhkan font yang berbeda?** | Atur `batesOptions.Font` ke objek `Font` (misalnya `FontRepository.FindFont("Arial")`). |

## Kesimpulan

Kami baru saja mendemonstrasikan cara **create PDF document C#** dan langsung **add bates numbering pdf** menggunakan Aspose.PDF. Prosesnya sederhana, dapat diandalkan, dan sepenuhnya dapat diprogram—sempurna untuk firma hukum, lembaga pemerintah, atau organisasi mana pun yang harus **add document identification numbers** dan **add sequential PDF numbers** ke batch besar berkas.

Gunakan fondasi ini dan bereksperimenlah: coba prefix berbeda untuk departemen yang berbeda, rangkaikan penomoran lintas beberapa file, atau sematkan kode QR di samping nomor Bates untuk jejak tambahan. Langit adalah batasnya setelah Anda menguasai alur kerja inti.

Jika Anda menemukan tutorial ini berguna, bagikan, tinggalkan komentar, atau jelajahi panduan lain kami tentang manipulasi PDF dengan C#. Selamat coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}