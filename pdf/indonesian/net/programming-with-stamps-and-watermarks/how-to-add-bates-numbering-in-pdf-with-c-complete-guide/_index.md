---
category: general
date: 2026-06-05
description: Cara menambahkan penomoran Bates pada PDF menggunakan C#. Pelajari cara
  memuat dokumen PDF, memperbarui penomoran halaman, dan menambahkan stempel Bates
  dengan cepat.
draft: false
keywords:
- how to add bates numbering
- add bates numbers pdf
- load pdf document c#
- add bates stamps to pdf
- update pagination pdf
language: id
og_description: Cara menambahkan penomoran Bates pada PDF menggunakan C#. Panduan
  ini menunjukkan cara memuat PDF, memperbarui penomoran halaman, dan menyimpan dokumen
  yang telah ditempeli stempel.
og_title: Cara Menambahkan Penomoran Bates pada PDF dengan C# – Langkah demi Langkah
schemas:
- author: Aspose
  dateModified: '2026-06-05'
  description: How to add bates numbering in PDF using C#. Learn to load a PDF document,
    update pagination, and add bates stamps quickly.
  headline: How to Add Bates Numbering in PDF with C# – Complete Guide
  type: TechArticle
- description: How to add bates numbering in PDF using C#. Learn to load a PDF document,
    update pagination, and add bates stamps quickly.
  name: How to Add Bates Numbering in PDF with C# – Complete Guide
  steps:
  - name: Load PDF Document in C#
    text: Before any numbering can happen, the PDF must be loaded into memory. Aspose.Pdf’s
      `Document` class does the heavy lifting, handling everything from encryption
      to page streams.
  - name: Add Bates Stamps to PDF
    text: The real hero of the library is `UpdatePagination()`. When you call it without
      parameters, Aspose automatically inserts Bates numbers on every page, using
      the default format `Page 1 of N`. If you need a custom prefix (e.g., “ABC‑2023‑”),
      you can supply a `PaginationInfo` object.
  - name: Save the Updated PDF
    text: After stamping, you simply persist the modified document. You can overwrite
      the original or write to a new file—both are safe as long as you respect file
      locks.
  - name: Full Working Example
    text: 'Putting the three pieces together yields a compact, production‑ready program:'
  type: HowTo
- questions:
  - answer: 'Pass the password to the `Document` constructor:'
    question: What if my PDF is password‑protected?
  - answer: 'Embed the font when you save: `pdf.FontEmbeddingMode = FontEmbeddingMode.Always;`.'
    question: Fonts missing on the target machine?
  - answer: The free evaluation works but adds a watermark. For production, acquire
      a license to remove it and unlock full pagination features.
    question: Do I need a license for Aspose.Pdf?
  type: FAQPage
tags:
- PDF
- C#
- Aspose.Pdf
title: Cara Menambahkan Penomoran Bates pada PDF dengan C# – Panduan Lengkap
url: /id/net/programming-with-stamps-and-watermarks/how-to-add-bates-numbering-in-pdf-with-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Menambahkan Penomoran Bates pada PDF dengan C# – Panduan Lengkap

Pernah bertanya-tanya **bagaimana cara menambahkan penomoran bates** ke PDF tanpa menghabiskan berjam‑jam bermain dengan alat manual? Anda tidak sendirian. Dalam banyak alur kerja hukum, forensik, atau kepatuhan, menstempel dokumen dengan nomor Bates berurutan adalah langkah yang tidak dapat dinegosiasikan, dan melakukannya secara programatis dalam C# dapat menghemat banyak waktu.

Dalam tutorial ini kami akan membahas solusi bersih, end‑to‑end yang menunjukkan secara tepat bagaimana **memuat dokumen PDF dalam C#**, memperbarui paginasi, dan **menambahkan stempel bates ke PDF** menggunakan pustaka Aspose.Pdf. Pada akhir tutorial Anda akan memiliki contoh kode siap‑jalankan, beberapa tips praktis, dan gambaran jelas tentang cara menyesuaikan proses ini untuk proyek Anda sendiri.

## Apa yang Akan Anda Pelajari

- Cara merujuk dan mengonfigurasi Aspose.Pdf untuk .NET.
- Pola tiga langkah: load → update pagination → save.
- Mengapa `UpdatePagination()` adalah keajaiban di balik **add bates numbers pdf** secara otomatis.
- Opsi kustomisasi untuk format nomor Bates, posisi, dan gaya.
- Kesalahan umum (mis., font yang hilang, file besar) dan cara menghindarinya.

> **Prasyarat** – Anda memerlukan .NET 6+ (atau .NET Framework 4.6+), salinan berlisensi Aspose.Pdf untuk .NET, dan pemahaman dasar tentang C#. Tidak ada alat eksternal lain yang diperlukan.

![cara menambahkan penomoran bates pada PDF menggunakan C#](image.png "cara menambahkan penomoran bates pada PDF menggunakan C#")

## Cara Menambahkan Penomoran Bates – Langkah‑per‑Langkah

Di bawah ini kami membagi proses menjadi tiga langkah logis. Setiap langkah dibungkus dalam header **H2** masing‑masing sehingga Anda dapat langsung melompat ke bagian yang Anda butuhkan.

### Memuat Dokumen PDF dalam C#

Sebelum penomoran dapat dilakukan, PDF harus dimuat ke memori. Kelas `Document` dari Aspose.Pdf melakukan pekerjaan berat, menangani segala hal mulai dari enkripsi hingga aliran halaman.

```csharp
using System;
using Aspose.Pdf;          // Make sure the Aspose.Pdf namespace is referenced

class BatesNumberingDemo
{
    static void Main()
    {
        // 👉 Step 1: Load the source PDF
        // Replace YOUR_DIRECTORY with the actual folder path on your machine.
        var inputPath = @"YOUR_DIRECTORY\input.pdf";

        // The `using` block ensures the document is properly disposed.
        using (var pdf = new Document(inputPath))
        {
            // The rest of the workflow continues inside this block.
            // ...
        }
    }
}
```

**Mengapa ini penting:**  
- Pernyataan `using` menjamin bahwa handle file dilepaskan, mencegah error “file in use” nanti saat Anda mencoba menyimpan.  
- Memuat file sekali menjaga penggunaan memori tetap rendah, bahkan untuk PDF dengan ratusan halaman.

### Menambahkan Stempel Bates ke PDF

Pahlawan sejati pustaka ini adalah `UpdatePagination()`. Ketika Anda memanggilnya tanpa parameter, Aspose secara otomatis menyisipkan nomor Bates pada setiap halaman, menggunakan format default `Page 1 of N`. Jika Anda memerlukan prefiks khusus (mis., “ABC‑2023‑”), Anda dapat menyediakan objek `PaginationInfo`.

```csharp
using Aspose.Pdf.Text;

// Inside the using block from the previous step:
{
    // 👉 Step 2: Configure and apply Bates numbering
    var pagination = new PaginationInfo
    {
        // Example: "ABC-2023-" will be prepended to each page number.
        Prefix = "ABC-2023-",
        // Suffix can be left empty or used for things like "-END".
        Suffix = string.Empty,
        // Choose where the stamp appears. Bottom‑right is common.
        HorizontalAlignment = HorizontalAlignment.Right,
        VerticalAlignment = VerticalAlignment.Bottom,
        // Font settings ensure the numbers are legible.
        Font = new FontRepository().FindFont("Arial"),
        FontSize = 10,
        // Optional: Add a border or background if you need a stamp look.
        // Border = new BorderInfo(BorderSide.All, 0.5f, Color.Black)
    };

    // This call adds the stamps to every page.
    pdf.Pages.UpdatePagination(pagination);
}
```

**Mengapa ini berhasil:**  
- `PaginationInfo` memberi Anda kontrol detail atas **add bates stamps to pdf** tanpa menulis loop sendiri.  
- Pustaka secara otomatis menangani jumlah halaman, padding nol, dan bahkan bahasa right‑to‑left bila diperlukan.

### Menyimpan PDF yang Diperbarui

Setelah menstempel, Anda cukup menyimpan dokumen yang telah dimodifikasi. Anda dapat menimpa file asli atau menulis ke file baru—keduanya aman selama Anda menghormati kunci file.

```csharp
// 👉 Step 3: Save the output PDF
var outputPath = @"YOUR_DIRECTORY\output.pdf";
pdf.Save(outputPath);
Console.WriteLine($"Bates‑numbered PDF saved to: {outputPath}");
```

**Tip:** Jika Anda memproses banyak file secara batch, pertimbangkan menggunakan `pdf.Save(outputPath, SaveFormat.PdfA_1b)` untuk menghasilkan arsip yang mematuhi PDF/A, yang sering diperlukan untuk bukti hukum.

### Contoh Kerja Lengkap

Menggabungkan ketiga bagian menghasilkan program yang ringkas dan siap produksi:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;

class BatesNumberingDemo
{
    static void Main()
    {
        var inputPath = @"YOUR_DIRECTORY\input.pdf";
        var outputPath = @"YOUR_DIRECTORY\output.pdf";

        using (var pdf = new Document(inputPath))
        {
            var pagination = new PaginationInfo
            {
                Prefix = "ABC-2023-",
                HorizontalAlignment = HorizontalAlignment.Right,
                VerticalAlignment = VerticalAlignment.Bottom,
                Font = new FontRepository().FindFont("Arial"),
                FontSize = 10
            };

            // Add or refresh Bates numbers
            pdf.Pages.UpdatePagination(pagination);

            // Persist the changes
            pdf.Save(outputPath);
        }

        Console.WriteLine($"Bates‑numbered PDF saved to: {outputPath}");
    }
}
```

**Output yang diharapkan:**  
Buka `output.pdf` di penampil apa pun dan Anda akan melihat urutan seperti `ABC-2023-001`, `ABC-2023-002`, … di kanan‑bawah setiap halaman. Nomor secara otomatis bertambah, bahkan jika Anda kemudian menyisipkan atau menghapus halaman dan menjalankan kembali `UpdatePagination()`.

## Menyesuaikan Penampilan Nomor Bates (Opsional)

Jika pengaturan default tidak cocok dengan alur kerja Anda, Anda dapat menyesuaikan beberapa properti lagi:

| Property | Apa yang dikontrol | Contoh |
|----------|--------------------|--------|
| `StartNumber` | Nomor pertama dalam seri | `StartNumber = 1000` |
| `NumberStyle` | Numerik, Romawi, atau alfanumerik | `NumberStyle = NumberStyle.AlphaNumeric` |
| `Margin` | Jarak dari tepi halaman (dalam poin) | `Margin = new MarginInfo(10, 10, 10, 10)` |
| `Color` | Warna teks untuk stempel | `Color = Color.Red` |

```csharp
pagination.StartNumber = 1000;
pagination.NumberStyle = NumberStyle.AlphaNumeric;
pagination.Margin = new MarginInfo(5, 5, 5, 5);
pagination.Color = Color.Red;
```

Penyesuaian ini sangat berguna ketika Anda perlu **add bates numbers pdf** untuk pengajuan pengadilan yang memerlukan format khusus.

## Pertanyaan Umum & Kasus Tepi

- **Bagaimana jika PDF saya dilindungi kata sandi?**  
  Berikan kata sandi ke konstruktor `Document`:  
  `new Document(inputPath, new LoadOptions { Password = "secret" })`.

- **PDF besar (>500 MB) menyebabkan OutOfMemoryException.**  
  Aktifkan streaming: `var pdf = new Document(inputPath) { EnableMemoryOptimization = true };`.

- **Font tidak ada di mesin target?**  
  Sematkan font saat menyimpan: `pdf.FontEmbeddingMode = FontEmbeddingMode.Always;`.

- **Apakah saya memerlukan lisensi untuk Aspose.Pdf?**  
  Evaluasi gratis berfungsi tetapi menambahkan watermark. Untuk produksi, dapatkan lisensi untuk menghapusnya dan membuka semua fitur paginasi.

## Ringkasan

Kami telah membahas **cara menambahkan penomoran bates** ke PDF menggunakan C# dari awal hingga akhir. Langkah‑langkah inti—**load pdf document c#**, panggil `UpdatePagination()` (inti dari **add bates stamps to pdf**), dan **save**—sederhana namun kuat. Dengan menyesuaikan `PaginationInfo`, Anda dapat memenuhi hampir semua kebutuhan hukum atau forensik, dan mekanisme perlindungan bawaan menjaga kode Anda tetap tangguh untuk file besar atau yang dilindungi.

## Apa Selanjutnya?

- Selami lebih dalam **add bates numbers pdf** dengan menghasilkan halaman indeks terpisah yang mencantumkan setiap stempel.  
- Gabungkan pendekatan ini dengan OCR untuk menyematkan teks yang dapat dicari bersama nomor Bates.  
- Jelajahi fitur Aspose.Pdf lainnya seperti watermarking, tanda tangan digital, atau konversi PDF/A.

Silakan bereksperimen, memecahkan hal‑hal, dan kemudian memperbaikinya—itulah cara Anda benar‑benar menguasai otomasi PDF. Jika Anda mengalami kendala atau memiliki kasus penggunaan yang cerdas, tinggalkan komentar di bawah. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang terkait erat yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap dengan penjelasan langkah‑per‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Cara Menambahkan dan Menyesuaikan Nomor Halaman dalam PDF Menggunakan Aspose.PDF untuk .NET | Panduan Manipulasi Dokumen](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [Cara Menambahkan Stempel Nomor Halaman dalam PDF Menggunakan Aspose.PDF untuk .NET | Watermark & Latar Belakang](/pdf/english/net/watermarks-backgrounds/add-page-number-stamp-using-aspose-pdf-dotnet/)
- [Cara Menambahkan Stempel Halaman dalam PDF Menggunakan Aspose.PDF untuk .NET&#58; Panduan Lengkap](/pdf/english/net/watermarks-backgrounds/add-page-stamp-aspose-pdf-dotnet-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}