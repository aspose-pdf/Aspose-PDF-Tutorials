---
category: general
date: 2026-05-27
description: Tambahkan penomoran Bates pada PDF menggunakan Aspose.Pdf di C#. Pelajari
  cara menambahkan penomoran Bates dengan cepat, menyesuaikan format, dan mengotomatiskan
  penandaan dokumen hukum.
draft: false
keywords:
- add bates numbering pdf
- how to add bates numbering
language: id
og_description: Tambahkan penomoran Bates pada PDF dengan Aspose.Pdf di C#. Panduan
  ini menunjukkan cara menambahkan penomoran Bates, mengonfigurasi awalan, dan menyimpan
  hasilnya.
og_title: Menambahkan Penomoran Bates pada PDF di C# – Tutorial Langkah demi Langkah
schemas:
- author: Aspose
  dateModified: '2026-05-27'
  description: Add Bates numbering PDF using Aspose.Pdf in C#. Learn how to add Bates
    numbering quickly, customize format, and automate legal document tagging.
  headline: Add Bates Numbering PDF in C# – Complete Guide
  type: TechArticle
- description: Add Bates numbering PDF using Aspose.Pdf in C#. Learn how to add Bates
    numbering quickly, customize format, and automate legal document tagging.
  name: Add Bates Numbering PDF in C# – Complete Guide
  steps:
  - name: Expected Output
    text: 'When you run the program, the console prints:'
  - name: Can I position the Bates number elsewhere?
    text: Yes. Use the `BatesNumberingArtifact`’s `Location` property (e.g., `Location
      = new Position(10, 10)`) to place the number at custom X/Y coordinates. You
      can also set `HorizontalAlignment` and `VerticalAlignment` for more control.
  - name: What if my PDF has thousands of pages?
    text: Aspose.Pdf streams pages efficiently, but it’s still a good idea to process
      in batches if you hit memory limits. The `Document` class also supports `PdfConverter`
      for incremental saving.
  - name: How do I change the font or color?
    text: 'Wrap the artifact in a `TextState` object:'
  - name: Do I need a license for production use?
    text: A licensed version removes evaluation watermarks and unlocks full performance.
      The free trial works fine for testing and proof‑of‑concepts.
  type: HowTo
tags:
- Aspose.Pdf
- C#
- Bates numbering
- PDF automation
title: Menambahkan Penomoran Bates pada PDF di C# – Panduan Lengkap
url: /id/net/programming-with-stamps-and-watermarks/add-bates-numbering-pdf-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Menambahkan Penomoran Bates pada PDF di C# – Panduan Lengkap

Pernah bertanya-tanya **bagaimana cara menambahkan penomoran Bates** ke PDF tanpa menghabiskan berjam-jam mengutak-atik alat manual? Anda tidak sendirian—tim hukum, auditor, dan spesialis e‑discovery semua membutuhkan cara yang dapat diandalkan untuk **menambahkan penomoran Bates pada file PDF** secara programatik.  

Dalam tutorial ini kami akan membahas solusi singkat, end‑to‑end menggunakan Aspose.Pdf untuk .NET, sehingga Anda dapat menambahkan nomor Bates ke dokumen apa pun hanya dengan beberapa baris kode C#.

## Apa yang Akan Anda Pelajari

- Cara membuka PDF yang ada dengan Aspose.Pdf  
- Cara membuat artefak penomoran Bates dan menyesuaikan formatnya  
- Cara melampirkan artefak ke setiap halaman (atau hanya halaman pertama)  
- Cara menyimpan file yang diperbarui dan memverifikasi hasilnya  

Tidak diperlukan pengalaman sebelumnya dengan Aspose—hanya pemahaman dasar tentang C# dan .NET. Pada akhir tutorial, Anda akan memiliki potongan kode yang dapat digunakan kembali dan dapat disalin‑tempel ke proyek mana pun.

## Prasyarat

- .NET 6.0 atau lebih baru (kode juga berfungsi pada .NET Framework 4.7+)
- Paket NuGet Aspose.Pdf untuk .NET (`Install-Package Aspose.Pdf`)
- File PDF sumber yang ingin Anda beri tag (letakkan di folder yang dapat Anda referensikan)

> **Tips Pro:** Jika Anda belum memiliki lisensi, Aspose menawarkan kunci sementara gratis yang menghapus watermark evaluasi.

## Langkah 1 – Membuka Dokumen PDF Sumber  

Pertama kita memerlukan objek `Document` yang mewakili file di disk. Anggap ini sebagai memuat kanvas kosong yang nanti akan kita beri nomor Bates.

```csharp
using Aspose.Pdf;
using System;

class Program
{
    static void Main()
    {
        // Adjust the path to point at your source PDF
        string sourcePath = @"C:\Docs\source.pdf";

        // Load the PDF – this is where we start to add Bates numbering
        using (var pdfDocument = new Document(sourcePath))
        {
            // The rest of the logic lives inside this using block
        }
    }
}
```

**Mengapa ini penting:** Membuka dokumen di dalam blok `using` memastikan semua sumber daya tak terkelola dilepaskan dengan cepat, yang sangat penting untuk PDF berukuran besar.

## Langkah 2 – Membuat Artefak Penomoran Bates  

Sebuah *BatesNumberingArtifact* adalah cara Aspose untuk mendeskripsikan bagaimana nomor harus ditampilkan. Anda dapat mengatur awalan, nomor mulai, kenaikan, dan bahkan string format khusus.

```csharp
// Step 2: Define the Bates numbering artifact
var batesNumbering = new BatesNumberingArtifact
{
    Prefix = "ABC",            // Text that appears before each number
    StartNumber = 1000,        // First number in the sequence
    Increment = 1,             // Step between consecutive numbers
    Format = "{0:D5}"          // Zero‑padded 5‑digit number (e.g., 01000)
};
```

**Mengapa Anda mungkin mengubah nilai-nilai ini:**  
- **Prefix** berguna untuk ID kasus (“CASE‑”, “DOC‑”).  
- **StartNumber** memungkinkan Anda melanjutkan seri sebelumnya.  
- **Increment** dapat diatur menjadi 2 jika Anda memerlukan penomoran ganjil/genap.  
- **Format** mendukung format gabungan .NET apa pun; `{0:D5}` menjamin lima digit dengan nol di depan.

## Langkah 3 – Menempelkan Artefak ke Halaman yang Diinginkan  

Anda dapat menambahkan artefak ke satu halaman, rentang halaman, atau seluruh dokumen. Untuk sebagian besar alur kerja hukum, kami menempelkannya ke *setiap* halaman, tetapi contoh di bawah menunjukkan kasus minimal—menambahkannya ke halaman pertama.

```csharp
// Step 3: Attach the artifact to the first page (index is 1‑based)
pdfDocument.Pages[1].Artifacts.Add(batesNumbering);
```

Jika Anda perlu menutupi semua halaman, lakukan loop melalui mereka:

```csharp
foreach (Page page in pdfDocument.Pages)
{
    page.Artifacts.Add(batesNumbering);
}
```

**Mengapa langkah ini penting:** Artefak dirender *setelah* konten halaman, sehingga nomor muncul di atas teks yang ada tanpa mengubah tata letak asli.

## Langkah 4 – Menyimpan PDF yang Dimodifikasi  

Akhirnya, tulis perubahan kembali ke disk. Anda dapat menimpa file asli atau membuat file baru—di sini kami akan menghasilkan salinan baru bernama `bates.pdf`.

```csharp
// Step 4: Persist the changes
string outputPath = @"C:\Docs\bates.pdf";
pdfDocument.Save(outputPath);

Console.WriteLine($"Bates numbering added successfully. File saved to: {outputPath}");
```

Saat Anda membuka `bates.pdf`, Anda akan melihat “ABC01000” (atau format apa pun yang Anda pilih) tercetak di lokasi default—biasanya pojok kanan bawah.

## Contoh Kerja Lengkap  

Menggabungkan semuanya, berikut program lengkap yang dapat Anda kompilasi dan jalankan:

```csharp
using Aspose.Pdf;
using System;

class AddBatesNumbering
{
    static void Main()
    {
        // -----------------------------------------------------------------
        // 1️⃣ Open the source PDF
        // -----------------------------------------------------------------
        string sourcePath = @"C:\Docs\source.pdf";
        using (var pdfDocument = new Document(sourcePath))
        {
            // -----------------------------------------------------------------
            // 2️⃣ Create and configure the Bates numbering artifact
            // -----------------------------------------------------------------
            var batesNumbering = new BatesNumberingArtifact
            {
                Prefix = "ABC",
                StartNumber = 1000,
                Increment = 1,
                Format = "{0:D5}"
            };

            // -----------------------------------------------------------------
            // 3️⃣ Attach the artifact to each page (or a specific page)
            // -----------------------------------------------------------------
            foreach (Page page in pdfDocument.Pages)
            {
                page.Artifacts.Add(batesNumbering);
            }

            // -----------------------------------------------------------------
            // 4️⃣ Save the new PDF
            // -----------------------------------------------------------------
            string outputPath = @"C:\Docs\bates.pdf";
            pdfDocument.Save(outputPath);

            Console.WriteLine($"Bates numbers added. Output: {outputPath}");
        }
    }
}
```

### Output yang Diharapkan

Saat Anda menjalankan program, konsol akan mencetak:

```
Bates numbers added. Output: C:\Docs\bates.pdf
```

Membuka `bates.pdf` menampilkan awalan “ABC” diikuti oleh urutan lima digit dengan nol di depan pada setiap halaman—tepat seperti yang diminta kode.

## Pertanyaan Umum & Kasus Tepi

### Bisakah saya menempatkan nomor Bates di tempat lain?

Ya. Gunakan properti `Location` dari `BatesNumberingArtifact` (misalnya, `Location = new Position(10, 10)`) untuk menempatkan nomor pada koordinat X/Y khusus. Anda juga dapat mengatur `HorizontalAlignment` dan `VerticalAlignment` untuk kontrol lebih.

### Bagaimana jika PDF saya memiliki ribuan halaman?

Aspose.Pdf men-stream halaman secara efisien, tetapi tetap disarankan memproses dalam batch jika Anda mencapai batas memori. Kelas `Document` juga mendukung `PdfConverter` untuk penyimpanan inkremental.

### Bagaimana cara mengubah font atau warna?

Wrap the artifact in a `TextState` object:

```csharp
batesNumbering.TextState = new TextState
{
    FontSize = 12,
    Font = FontRepository.FindFont("Arial"),
    ForegroundColor = Color.FromRgb(255, 0, 0) // red
};
```

### Apakah saya memerlukan lisensi untuk penggunaan produksi?

Versi berlisensi menghapus watermark evaluasi dan membuka kinerja penuh. Versi percobaan gratis berfungsi baik untuk pengujian dan proof‑of‑concept.

## Verifikasi – Pemeriksaan Visual Cepat  

Jika Anda lebih suka verifikasi otomatis, Aspose dapat mengekstrak teks sebuah halaman dan mengonfirmasi keberadaan awalan:

```csharp
string pageText = pdfDocument.Pages[1].ExtractText();
bool hasBates = pageText.Contains("ABC01000");
Console.WriteLine(hasBates ? "Bates number verified." : "Number missing!");
```

Menjalankan ini setelah langkah penyimpanan akan mencetak `Bates number verified.` jika semuanya berjalan lancar.

## Kesimpulan  

Anda sekarang tahu **cara menambahkan penomoran Bates pada file PDF** menggunakan Aspose.Pdf di C#. Dari membuka dokumen hingga mengonfigurasi artefak, menempelkannya ke halaman, dan menyimpan hasilnya, prosesnya sederhana dan sepenuhnya dapat diprogram.  

Langkah selanjutnya? Cobalah bereksperimen dengan:

- Nilai `Prefix` yang berbeda untuk beberapa batch kasus  
- `Location` dan `TextState` khusus untuk branding  
- Menambahkan awalan khusus per halaman (mis., “VOL‑1‑”, “VOL‑2‑”) dengan menyesuaikan `StartNumber` per iterasi loop  

Penyesuaian ini memungkinkan Anda menyesuaikan solusi untuk hampir semua alur kerja hukum atau arsip.  

Ada pertanyaan lebih lanjut tentang **cara menambahkan penomoran Bates** untuk PDF multi‑bahasa atau file terenkripsi? Tinggalkan komentar di bawah, dan selamat coding!

## Tutorial Terkait

- [Cara Menambahkan dan Menyesuaikan Nomor Halaman dalam PDF Menggunakan Aspose.PDF untuk .NET | Panduan Manipulasi Dokumen](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [Cara Menambahkan Header Berbeda dalam PDF Menggunakan Aspose.PDF untuk .NET&#58; Panduan Langkah demi Langkah](/pdf/english/net/document-manipulation/add-different-headers-aspose-pdf-net/)
- [Cara Menambahkan Footer Cap Teks dalam PDF Menggunakan Aspose.PDF untuk .NET&#58; Panduan Langkah demi Langkah](/pdf/english/net/document-manipulation/add-text-stamp-footer-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}