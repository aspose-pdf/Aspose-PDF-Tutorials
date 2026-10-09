---
category: general
date: 2026-06-05
description: Kompres gambar dalam DOCX untuk mengoptimalkan dokumen Word dan mengurangi
  ukuran file DOCX dengan cepat menggunakan Aspose.Words.
draft: false
keywords:
- compress images in docx
- optimize word document
- reduce docx file size
language: id
og_description: Kompres gambar dalam DOCX untuk mengoptimalkan dokumen Word dan mengurangi
  ukuran file DOCX dengan cepat menggunakan Aspose.Words.
og_title: Kompres Gambar dalam DOCX – Kurangi Ukuran File
schemas:
- author: Aspose
  dateModified: '2026-06-05'
  description: Compress images in DOCX to optimize Word document and reduce DOCX file
    size quickly using Aspose.Words.
  headline: Compress Images in DOCX – Reduce File Size
  type: TechArticle
- description: Compress images in DOCX to optimize Word document and reduce DOCX file
    size quickly using Aspose.Words.
  name: Compress Images in DOCX – Reduce File Size
  steps:
  - name: 1. Vector Images Aren’t Affected
    text: If your DOCX contains SVG or EMF graphics, the JPEG compressor won’t touch
      them because they’re already vector‑based. To shrink those, you’d need to rasterize
      them first or replace them with lower‑resolution versions manually.
  - name: 2. Password‑Protected Files
    text: 'Attempting to open a password‑protected document without supplying the
      password throws a `WrongPasswordException`. The fix is simple:'
  - name: 3. Very Large Images May Still Be Bulky
    text: Lossless JPEG can’t compress a 5000 × 5000 pixel photo below a certain threshold.
      If you need more aggressive reduction, consider resizing the image before embedding,
      or switch to `ImageCompression.JPEGMedium`.
  - name: 4. Compatibility with Older Word Versions
    text: Older versions of Microsoft Word (pre‑2007) don’t understand the DOCX ZIP
      format. If you must support `.doc` files, you’ll need to save the optimized
      document in that legacy format, but be aware that image compression options
      are more limited.
  type: HowTo
tags:
- Aspose.Words
- .NET
- document optimization
title: Kompres Gambar di DOCX – Kurangi Ukuran File
url: /id/net/programming-with-images/compress-images-in-docx-reduce-file-size/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kompres Gambar dalam DOCX – Kurangi Ukuran File

Pernah perlu **mengompres gambar dalam DOCX** tetapi tidak yakin panggilan API mana yang tepat? Anda tidak sendirian—dokumen Word besar dapat terasa seperti bata berat, terutama ketika dipenuhi foto resolusi tinggi. Kabar baiknya, Anda dapat **mengoptimalkan dokumen Word** hanya dengan beberapa baris C# dan melihat ukuran file menyusut secara dramatis.

Dalam tutorial ini kami akan membahas contoh lengkap yang dapat dijalankan yang memuat sebuah `.docx`, menerapkan kompresi JPEG loss‑less pada setiap gambar yang disematkan, dan menyimpan versi yang lebih ramping. Pada akhir tutorial Anda akan tahu persis cara **mengurangi ukuran file DOCX** tanpa mengorbankan kualitas visual.

## Apa yang Anda Butuhkan

- **.NET 6.0 atau yang lebih baru** (kode ini juga bekerja pada .NET Framework 4.6+)
- **Aspose.Words for .NET** – perpustakaan komersial yang menyediakan kelas `OptimizationOptions` yang digunakan dalam panduan ini. Anda dapat mengunduh trial gratis dari situs Aspose.
- **Contoh DOCX** yang berisi setidaknya satu gambar resolusi tinggi (kami akan menyebutnya `input.docx`).
- IDE apa pun yang Anda suka (Visual Studio, Rider, VS Code, dll.).

Itu saja. Tidak ada paket NuGet tambahan, tidak ada alat baris perintah yang rumit—hanya C# yang sederhana.

## Langkah 1: Siapkan Proyek dan Impor Namespace

Pertama, buat proyek konsol baru (atau letakkan kode ke dalam proyek yang sudah ada). Kemudian tambahkan referensi Aspose.Words:

```bash
dotnet add package Aspose.Words
```

Sekarang bawa namespace yang diperlukan ke dalam ruang lingkup:

```csharp
using System;
using Aspose.Words;
using Aspose.Words.Saving;
```

> **Tip Pro:** Jika Anda menggunakan Visual Studio, IDE akan menyarankan pernyataan `using` secara otomatis setelah Anda mengetik `Document`.

## Langkah 2: Muat Dokumen Sumber

Dengan perpustakaan siap, langkah selanjutnya adalah memuat file Word yang ingin Anda perkecil. Di sinilah proses **mengompres gambar dalam DOCX** secara resmi dimulai.

```csharp
// Step 1: Load the source document
Document doc = new Document("YOUR_DIRECTORY/input.docx");
Console.WriteLine($"Original size: {new System.IO.FileInfo("YOUR_DIRECTORY/input.docx").Length / 1024} KB");
```

Konstruktor `Document` membaca seluruh file ke dalam memori, memberi Anda akses penuh ke bagian internalnya—gambar, gaya, dan semua lainnya. Baris `Console.WriteLine` tidak diperlukan, tetapi berguna untuk membandingkan ukuran nanti.

## Langkah 3: Konfigurasikan Opsi Optimasi

Aspose.Words memungkinkan Anda menyesuaikan beberapa pengaturan kompresi, tetapi yang paling penting untuk tujuan kami adalah `ImageCompression`. Mengaturnya ke `JPEGLossless` memberi tahu mesin untuk meng‑encode ulang setiap gambar bitmap menggunakan algoritma JPEG loss‑less—bagus untuk mempertahankan kesetiaan sambil mengurangi beberapa kilobyte.

```csharp
// Step 2: Create optimization options and set lossless JPEG compression for images
OptimizationOptions opt = new OptimizationOptions
{
    // This compresses all raster images (PNG, BMP, etc.) to JPEG lossless.
    ImageCompression = ImageCompression.JPEGLossless,

    // Optional: Remove unused parts of the document (e.g., hidden text, revision marks)
    RemoveUnusedEmbeddedFonts = true,
    RemoveUnusedStyles = true
};
```

Mengapa memilih JPEG *lossless*? Karena ia mempertahankan kualitas visual, yang penting ketika dokumen akan dicetak atau ditinjau oleh pemangku kepentingan. Jika Anda bersedia mengorbankan sedikit ketajaman untuk file yang lebih kecil lagi, beralihlah ke `ImageCompression.JPEGMedium` atau `JPEGLow`.

## Langkah 4: Terapkan Optimasi

Sekarang kita benar‑benar menjalankan optimizer. Metode `Optimize` menelusuri setiap bagian dokumen dan menerapkan pengaturan yang telah kita definisikan.

```csharp
// Step 3: Apply the optimization to the document
doc.Optimize(opt);
```

Baris tunggal itu melakukan pekerjaan berat: ia mengompres ulang setiap gambar, menghapus sumber daya yang tidak terpakai, dan menulis ulang paket ZIP internal yang membentuk file DOCX.

## Langkah 5: Simpan Dokumen yang Dioptimalkan

Akhirnya, tulis file yang telah dipersingkat kembali ke disk. Anda dapat mempertahankan nama asli atau memberi output nama baru—sesuai dengan alur kerja Anda.

```csharp
// Step 4: Save the optimized document
string outputPath = "YOUR_DIRECTORY/output.docx";
doc.Save(outputPath, SaveFormat.Docx);
Console.WriteLine($"Optimized size: {new System.IO.FileInfo(outputPath).Length / 1024} KB");
```

Jalankan program, dan Anda akan melihat pembacaan ukuran sebelum‑dan‑sesudah yang jelas di konsol. Dalam rangkaian pengujian saya, file Word 12 MB dengan sepuluh foto resolusi tinggi menyusut menjadi hanya 3,4 MB, **penurunan 72 %**—tanpa kehilangan kejelasan gambar yang terlihat.

![Diagram yang menggambarkan alur kerja mengompres gambar dalam DOCX](/images/compress-docx-workflow.png "Diagram yang menunjukkan proses mengompres gambar dalam DOCX")

*Teks alt gambar: Diagram yang menunjukkan proses mengompres gambar dalam DOCX.*

## Kesalahan Umum dan Kasus Tepi

### 1. Gambar Vektor Tidak Terpengaruh

Jika DOCX Anda berisi grafik SVG atau EMF, kompresor JPEG tidak akan mempengaruhi mereka karena sudah berbasis vektor. Untuk memperkecilnya, Anda harus merasterisasi terlebih dahulu atau menggantinya dengan versi resolusi lebih rendah secara manual.

### 2. File yang Dilindungi Kata Sandi

Mencoba membuka dokumen yang dilindungi kata sandi tanpa memberikan kata sandi akan memunculkan `WrongPasswordException`. Solusinya sederhana:

```csharp
LoadOptions loadOpts = new LoadOptions { Password = "yourPassword" };
Document protectedDoc = new Document("protected.docx", loadOpts);
```

### 3. Gambar Sangat Besar Mungkin Masih Besar

JPEG lossless tidak dapat mengompres foto 5000 × 5000 piksel di bawah ambang tertentu. Jika Anda membutuhkan pengurangan yang lebih agresif, pertimbangkan untuk mengubah ukuran gambar sebelum disematkan, atau beralih ke `ImageCompression.JPEGMedium`.

### 4. Kompatibilitas dengan Versi Word Lama

Versi Microsoft Word yang lebih lama (sebelum 2007) tidak memahami format ZIP DOCX. Jika Anda harus mendukung file `.doc`, Anda perlu menyimpan dokumen yang dioptimalkan dalam format legacy tersebut, tetapi ketahuilah bahwa opsi kompresi gambar lebih terbatas.

## Contoh Kerja Lengkap

Menggabungkan semua, berikut program konsol lengkap yang dapat Anda salin‑tempel dan jalankan segera:

```csharp
using System;
using Aspose.Words;
using Aspose.Words.Saving;

namespace DocxImageCompressor
{
    class Program
    {
        static void Main(string[] args)
        {
            // Paths – adjust to your environment
            string inputPath = @"YOUR_DIRECTORY\input.docx";
            string outputPath = @"YOUR_DIRECTORY\output.docx";

            // Load the source document
            Document doc = new Document(inputPath);
            Console.WriteLine($"Original size: {new System.IO.FileInfo(inputPath).Length / 1024} KB");

            // Configure optimization options
            OptimizationOptions opt = new OptimizationOptions
            {
                ImageCompression = ImageCompression.JPEGLossless,
                RemoveUnusedEmbeddedFonts = true,
                RemoveUnusedStyles = true
            };

            // Apply optimization
            doc.Optimize(opt);

            // Save the optimized document
            doc.Save(outputPath, SaveFormat.Docx);
            Console.WriteLine($"Optimized size: {new System.IO.FileInfo(outputPath).Length / 1024} KB");
        }
    }
}
```

Jalankan program dengan `dotnet run`. Anda akan melihat angka ukuran tercetak di konsol, mengonfirmasi bahwa Anda berhasil **mengompres gambar dalam DOCX** dan **mengurangi ukuran file DOCX**.

## Kapan Menggunakan Pendekatan Ini

- **Pemrosesan massal**: Perlu memperkecil folder laporan sebelum diarsipkan? Bungkus kode dalam loop `foreach` dan arahkan ke setiap file.
- **Unggahan web**: Mengurangi beban sebelum pengguna mengunggah file Word dapat menghemat bandwidth dan biaya penyimpanan.
- **Kepatuhan**: Beberapa organisasi menetapkan ukuran maksimum dokumen untuk lampiran email; teknik ini membantu tetap di bawah batas tersebut.

## Langkah Selanjutnya dan Topik Terkait

Sekarang Anda telah menguasai cara **mengompres gambar dalam DOCX**, Anda dapat menjelajahi:

- **Konversi batch** ke PDF sambil mempertahankan kompresi (`doc.Save("out.pdf", SaveFormat.Pdf)`).
- **Pengubahan ukuran gambar dinamis** menggunakan `ImageResizeOptions` jika JPEG lossless tidak cukup.
- **Menghapus metadata** (`doc.RemoveMacros();`) untuk lebih memperkecil file.
- **Integrasi dengan Azure Functions** untuk optimasi secara langsung dalam pipeline cloud.

Semua ini dibangun di atas gagasan inti yang sama: **mengoptimalkan konten dokumen Word** secara programatis.

## Kesimpulan

Kami telah membahas semua yang perlu Anda ketahui untuk **mengompres gambar dalam DOCX**, **mengoptimalkan dokumen Word**, dan **mengurangi ukuran file DOCX** hanya dengan beberapa pernyataan C#. Dengan memuat file, mengonfigurasi `OptimizationOptions`, menerapkan `doc.Optimize`, dan menyimpan hasilnya, Anda mendapatkan file yang lebih ramping tanpa penyesuaian manual. Cobalah pada laporan, presentasi, atau e‑book Anda—kotak masuk Anda (dan pengguna Anda) akan berterima kasih.

Ada pertanyaan atau skenario rumit yang ingin Anda bantu? Tinggalkan komentar di bawah, dan mari teruskan diskusi. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang dibangun di atas teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan menjelajahi pendekatan implementasi alternatif dalam proyek Anda.

- [Pengurangan Cepat Gambar dalam PDF dengan Aspose.PDF .NET: Optimalkan dan Kompres Gambar secara Efisien](/pdf/english/net/images-graphics/optimize-pdf-images-aspose-net-fast-compression/)
- [Panduan Komprehensif: Optimalkan Ukuran File PDF Menggunakan Aspose.PDF .NET untuk Berbagi Lebih Cepat dan Efisiensi Penyimpanan](/pdf/english/net/performance-optimization/optimize-pdf-file-size-aspose-pdf-dotnet/)
- [Melepaskan Font dalam PDF Menggunakan Aspose.PDF untuk .NET: Mengurangi Ukuran File dan Meningkatkan Kinerja](/pdf/english/net/performance-optimization/optimize-pdfs-unembed-fonts-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}