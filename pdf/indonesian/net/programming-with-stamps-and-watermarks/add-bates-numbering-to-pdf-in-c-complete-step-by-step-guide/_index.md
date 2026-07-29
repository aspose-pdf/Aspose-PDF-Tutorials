---
category: general
date: 2026-06-18
description: Tambahkan penomoran Bates ke PDF dengan C# secara cepat. Pelajari cara
  memuat PDF, mengatur awalan penomoran Bates, dan menambahkan nomor halaman berurutan
  menggunakan pustaka C# sederhana.
draft: false
keywords:
- add bates numbering
- add sequential page numbers
- load pdf c#
- apply bates numbering
- bates numbering prefix
language: id
og_description: Tambahkan penomoran Bates ke PDF dengan C# pada kalimat pertama. Ikuti
  panduan ini untuk memuat PDF, mengatur awalan, dan secara otomatis menerapkan nomor
  halaman berurutan.
og_title: Tambahkan Penomoran Bates ke PDF dalam C# – Panduan Pemrograman Lengkap
schemas:
- author: Aspose
  dateModified: '2026-06-18'
  description: Add Bates numbering to PDF in C# quickly. Learn how to load PDF, set
    a bates numbering prefix, and add sequential page numbers using a simple C# library.
  headline: Add Bates Numbering to PDF in C# – Complete Step‑by‑Step Guide
  type: TechArticle
tags:
- PDF
- C#
- Document Processing
title: Tambahkan Penomoran Bates ke PDF dengan C# – Panduan Lengkap Langkah demi Langkah
url: /id/net/programming-with-stamps-and-watermarks/add-bates-numbering-to-pdf-in-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tambahkan Penomoran Bates ke PDF dalam C# – Panduan Lengkap Langkah‑per‑Langkah

Pernahkah Anda perlu **add bates numbering** ke PDF tetapi tidak yakin harus mulai dari mana di C#? Anda tidak sendirian. Dalam banyak alur kerja hukum, medis, atau arsip, menempelkan setiap halaman dengan pengenal unik adalah keharusan, dan melakukannya secara programatik menghemat upaya manual yang tak terhitung.

Dalam tutorial ini Anda akan melihat secara tepat cara **load pdf c#**, mengonfigurasi **bates numbering prefix**, dan **apply bates numbering** sehingga setiap halaman mendapatkan nomor berurutan. Pada akhir tutorial Anda akan memiliki potongan kode siap‑jalankan yang menambahkan nomor halaman berurutan dengan awalan khusus—tanpa misteri, hanya kode yang jelas.

## Apa yang Akan Anda Pelajari

- Cara membuka file PDF yang ada menggunakan perpustakaan PDF .NET yang populer.  
- Cara menyiapkan **bates numbering options** (awalan, nomor mulai, padding).  
- Cara memanggil metode `AddBatesNumbering` pada perpustakaan untuk **add bates numbering** secara otomatis.  
- Cara menyimpan dokumen yang telah dimodifikasi tanpa merusak konten yang ada.  

Tanpa alat eksternal, tanpa trik baris perintah—hanya kode C# langsung yang dapat Anda sisipkan ke proyek .NET mana pun.

![Diagram showing Bates numbering applied to PDF pages](/images/bates-numbering-flow.png){: .align-center alt="Diagram alur Penomoran Bates"}

## Prasyarat

- .NET 6.0 atau lebih baru (kode ini bekerja dengan .NET Core dan .NET Framework 4.6+).  
- Sebuah perpustakaan manipulasi PDF yang mendukung penomoran Bates (misalnya **Aspose.PDF**, **iText7**, atau **PdfSharp** dengan ekstensi). Contoh di bawah menggunakan API generik yang meniru sintaks Aspose.PDF, tetapi Anda dapat menyesuaikannya dengan perpustakaan favorit Anda.  
- Pengetahuan dasar C#—jika Anda dapat menulis `Console.WriteLine`, Anda siap.  

Sudah siap? Bagus—mari kita mulai.

## Penomoran Bates – Gambaran Umum

Sebelum kita mulai menulis kode, mari kita jelaskan mengapa **add bates numbering** penting. Nomor Bates adalah pengenal unik yang muncul pada setiap halaman, biasanya dalam format `PREFIX-####`. Pengadilan, firma hukum, dan lembaga pemerintah mengandalkannya untuk merujuk dokumen secara tepat. Mengotomatisasi langkah ini menghilangkan kesalahan manusia, memastikan format yang konsisten, dan mempercepat pemrosesan batch ratusan file.

Sekarang karena “mengapa” sudah jelas, mari kita lihat “bagaimana”.

## Langkah 1: Muat PDF dalam C#

Pertama, kita perlu memuat PDF sumber ke dalam memori. Sebagian besar perpustakaan menyediakan konstruktor `Document` yang menerima jalur file.

```csharp
// Step 1: Load the PDF document from disk
// Replace YOUR_DIRECTORY with the actual folder path.
Document doc = new Document("YOUR_DIRECTORY/input.pdf");

// Quick sanity check – ensure the file was loaded.
if (doc.Pages.Count == 0)
{
    throw new InvalidOperationException("The PDF appears to be empty or could not be read.");
}
```

*Mengapa langkah ini?* Memuat PDF memberi kita model objek yang dapat dimanipulasi. Tanpa itu, kita tidak dapat menambahkan **bates numbering prefix** atau metadata lainnya.

> **Pro tip:** Jika Anda memproses banyak file, pertimbangkan untuk menggunakan kembali satu instance `PdfLoadOptions` untuk meningkatkan kinerja.

## Langkah 2: Konfigurasikan Awalan Penomoran Bates

Selanjutnya, kita menentukan bagaimana penomoran harus terlihat. Kelas `BatesNumberingOptions` memungkinkan Anda menentukan awalan, nomor mulai, dan bahkan padding (berapa digit yang disediakan).

```csharp
// Step 2: Set up Bates numbering options
BatesNumberingOptions batesOptions = new BatesNumberingOptions
{
    // The prefix that will appear before every number.
    Prefix = "ABC",          // <-- this is the bates numbering prefix
    // The first number in the series.
    Start = 1000,
    // Optional: pad numbers to 5 digits (e.g., 01000, 01001)
    Padding = 5
};
```

*Mengapa ini penting:* **bates numbering prefix** membantu mengkategorikan dokumen (misalnya “ABC” untuk kasus tertentu). Sesuaikan `Start` dan `Padding` agar sesuai dengan konvensi organisasi Anda.

## Langkah 3: Terapkan Penomoran Bates ke Dokumen

Sekarang aksi inti: beri tahu perpustakaan untuk menyisipkan nomor pada setiap halaman. Nama metode dapat berbeda tergantung perpustakaan, tetapi konsepnya tetap sama.

```csharp
// Step 3: Apply the Bates numbering to every page
doc.AddBatesNumbering(batesOptions);
```

Di balik layar, perpustakaan mengiterasi `doc.Pages`, menggambar teks (biasanya di footer), dan menghormati margin halaman yang ada. Jika Anda memerlukan nomor di lokasi lain, sebagian besar API memungkinkan Anda menyesuaikan `BatesNumberingOptions.Position`.

> **Bagaimana jika PDF sudah memiliki nomor halaman?** Sebagian besar perpustakaan akan menimpa nomor Bates baru di atas konten yang ada. Jika Anda ingin menggantinya, mungkin perlu menghapus footer yang ada terlebih dahulu—periksa dokumentasi perpustakaan Anda untuk `RemovePageNumbers()` atau yang serupa.

## Langkah 4: Simpan PDF yang Diperbarui

Akhirnya, tulis dokumen yang telah dimodifikasi kembali ke disk. Anda dapat menimpa file asli atau menulis ke file baru; yang terakhir lebih aman untuk pekerjaan batch.

```csharp
// Step 4: Save the PDF with Bates numbers applied
doc.Save("YOUR_DIRECTORY/output.pdf");

// Confirmation message
Console.WriteLine("Bates numbering added successfully! Output saved to output.pdf");
```

Itu saja—empat langkah singkat dan Anda telah **add bates numbering** ke file PDF apa pun.

## Contoh Kerja Lengkap

Menggabungkan semuanya, berikut adalah aplikasi konsol mandiri yang dapat Anda salin‑tempel ke Visual Studio:

```csharp
using System;
using Aspose.Pdf;               // Replace with your PDF library namespace
using Aspose.Pdf.Facades;       // For Bates numbering support

class Program
{
    static void Main()
    {
        // 1️⃣ Load the PDF
        Document doc = new Document("YOUR_DIRECTORY/input.pdf");
        if (doc.Pages.Count == 0)
        {
            Console.WriteLine("Error: PDF is empty or unreadable.");
            return;
        }

        // 2️⃣ Configure Bates numbering
        BatesNumberingOptions batesOptions = new BatesNumberingOptions
        {
            Prefix = "ABC",
            Start = 1000,
            Padding = 5,
            // Optional: change position to top‑right
            // Position = new Position(0, 0, 0, 0) // customize as needed
        };

        // 3️⃣ Apply the numbering
        doc.AddBatesNumbering(batesOptions);

        // 4️⃣ Save the result
        doc.Save("YOUR_DIRECTORY/output.pdf");
        Console.WriteLine("Bates numbering added successfully!");
    }
}
```

**Output yang diharapkan:** Buka `output.pdf` dan Anda akan melihat setiap halaman diberi label seperti `ABC-01000`, `ABC-01001`, … hingga halaman terakhir. Nomor muncul di lokasi footer default kecuali Anda mengubah `Position`.

## Menangani Kasus Edge

| Situasi | Pendekatan yang Disarankan |
|-----------|----------------------|
| **Dokumen besar (1000+ halaman)** | Tingkatkan `Padding` untuk menampung nomor tertinggi, misalnya `Padding = 7`. |
| **Watermark yang ada** | Terapkan penomoran Bates *setelah* menambahkan watermark untuk menghindari tumpang tindih. |
| **Awalan berbeda per batch** | Lakukan loop pada file dan atur `batesOptions.Prefix` secara dinamis berdasarkan nama folder atau metadata. |
| **Karakter Unicode dalam awalan** | Pastikan perpustakaan PDF Anda mendukung UTF‑8; beberapa versi lama mungkin hanya mendukung ASCII. |

## Tips Pro & Kesalahan Umum

- **Pro tip:** Gunakan `doc.Optimize()` (jika tersedia) setelah penomoran untuk mengompres file dan menjaga ukuran tetap terkendali.  
- **Waspadai:** PDF dengan halaman terenkripsi—sebagian besar perpustakaan memerlukan kata sandi sebelum Anda dapat menambahkan nomor.  
- **Kesalahan umum:** Lupa mengatur `Padding`. Tanpanya, nomor seperti `1000` akan menjadi `1000` (tanpa nol di depan), yang dapat mengacaukan urutan di beberapa sistem.  
- **Tips performa:** Untuk pemrosesan batch, buat instance `BatesNumberingOptions` sekali dan gunakan kembali pada semua dokumen; hanya ubah `Start` jika Anda membutuhkan seri berkelanjutan.

## Kesimpulan

Anda kini memiliki cara yang jelas dan dapat direproduksi untuk **add bates numbering** ke PDF menggunakan C#. Dari memuat file hingga mengonfigurasi **bates numbering prefix**, menerapkan nomor, dan akhirnya menyimpan hasilnya, setiap langkah dibahas dengan penjelasan *bagaimana* dan *mengapa*. Solusi ini bekerja untuk proyek .NET apa pun dan dapat diperluas untuk menangani operasi massal, posisi khusus, atau integrasi dengan sistem manajemen dokumen.

Siap untuk tantangan berikutnya? Cobalah bereksperimen dengan **add sequential page numbers** dalam gaya yang berbeda, atau gabungkan nomor Bates dengan kode QR untuk metadata yang lebih kaya. Pola yang sama—load, configure, apply, save—berlaku untuk sebagian besar tugas otomatisasi PDF.

Jika Anda memiliki pertanyaan tentang menyesuaikan tata letak, menangani PDF terenkripsi, atau mengintegrasikan ini ke dalam API ASP.NET, tinggalkan komentar di bawah. Selamat coding, semoga PDF Anda selalu bernomor dengan sempurna!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait erat yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber daya menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Tambahkan nomor halaman pdf dengan C# – Panduan Langkah‑per‑Langkah Lengkap](/pdf/english/net/programming-with-pdf-pages/add-page-numbers-pdf-with-c-full-step-by-step-guide/)
- [Cara Menambahkan dan Menyesuaikan Nomor Halaman dalam PDF Menggunakan Aspose.PDF untuk .NET | Panduan Manipulasi Dokumen](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [Tambahkan Gambar & Nomor Halaman ke PDF Menggunakan Aspose.PDF untuk .NET: Panduan Lengkap](/pdf/english/net/document-manipulation/enhance-pdfs-images-page-numbers-aspose-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}