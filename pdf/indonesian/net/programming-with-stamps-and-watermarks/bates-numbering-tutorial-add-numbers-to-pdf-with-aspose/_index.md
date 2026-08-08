---
category: general
date: 2026-07-03
description: Tutorial penomoran Bates yang menunjukkan cara menambahkan penomoran
  Bates pada file PDF menggunakan Aspose.PDF. Termasuk pengaturan awalan nomor Bates
  dan contoh lengkap penomoran Bates.
draft: false
keywords:
- bates numbering tutorial
- add bates numbering pdf
- bates numbering example
- prefix bates number
language: id
og_description: Tutorial penomoran Bates yang memandu Anda melalui penambahan penomoran
  Bates pada file PDF, mengatur awalan nomor Bates, dan memberikan contoh kerja lengkap.
og_title: 'Tutorial Penomoran Bates: Tambahkan Nomor ke PDF dengan Aspose'
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Bates numbering tutorial showing how to add bates numbering pdf files
    using Aspose.PDF. Includes prefix bates number setup and a complete bates numbering
    example.
  headline: 'Bates Numbering Tutorial: Add Numbers to PDF with Aspose'
  type: TechArticle
- description: Bates numbering tutorial showing how to add bates numbering pdf files
    using Aspose.PDF. Includes prefix bates number setup and a complete bates numbering
    example.
  name: 'Bates Numbering Tutorial: Add Numbers to PDF with Aspose'
  steps:
  - name: What if I need to reset the counter for each section?
    text: You can call `pdfDocument.BatesNumbering.Reset()` before processing a new
      range of pages. Combine it with a loop over `pdfDocument.Pages` and set `Start`
      again for each section.
  - name: How do I apply different prefixes to different page ranges?
    text: 'Create multiple `BatesNumbering` objects—one per range—by cloning the document
      or by using the `Add` method (available in newer Aspose versions). Here’s a
      quick sketch:'
  - name: Does the library support Unicode prefixes?
    text: Absolutely. Pass any Unicode string (e.g., `"案件‑"`). Aspose.PDF handles
      right‑to‑left scripts and special symbols without extra configuration.
  - name: What about PDF security—will Bates numbering break encryption?
    text: If the source PDF is encrypted, you must provide the password before accessing
      `BatesNumbering`. The numbering process respects the original encryption settings—your
      output will stay encrypted unless you explicitly change it.
  type: HowTo
tags:
- Aspose.PDF
- PDF processing
- Bates numbering
title: 'Tutorial Penomoran Bates: Tambahkan Nomor ke PDF dengan Aspose'
url: /id/net/programming-with-stamps-and-watermarks/bates-numbering-tutorial-add-numbers-to-pdf-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tutorial Penomoran Bates – Menambahkan Nomor Bates ke PDF dengan Aspose

Pernah membutuhkan **bates numbering tutorial** karena Anda harus menandai ribuan halaman untuk litigasi? Anda tidak sendirian. Dalam banyak alur kerja hukum dan kepatuhan, cara yang dapat diandalkan untuk *add bates numbering pdf* file adalah persyaratan yang tidak dapat dinegosiasikan. Untungnya, Aspose.PDF membuat seluruh proses menjadi sangat mudah, dan dalam panduan ini kami akan membahas contoh **bates numbering example** lengkap yang dapat Anda langsung gunakan dalam proyek Anda.

> **Apa yang akan Anda dapatkan:** potongan kode yang dapat dijalankan yang mengatur nomor mulai, menerapkan **prefix bates number**, dan menyimpan hasilnya—semua dalam kurang dari 30 baris C#.

## Prasyarat

Sebelum kita mulai, pastikan Anda memiliki:

- .NET 6.0 atau lebih baru (API berfungsi sama pada .NET Framework 4.6+)
- Lisensi Aspose.PDF for .NET yang valid (atau Anda dapat menggunakan mode evaluasi gratis)
- File PDF input bernama `input.pdf` ditempatkan di folder yang Anda kontrol
- Visual Studio 2022 atau editor apa pun yang memahami proyek C#

Tidak diperlukan paket NuGet tambahan selain `Aspose.Pdf`.

## Langkah 1: Instal Aspose.PDF untuk .NET

Buka terminal Anda (atau Package Manager Console) dan jalankan:

```bash
dotnet add package Aspose.Pdf
```

Atau, jika Anda lebih suka UI, klik kanan **Dependencies → Manage NuGet Packages**, cari *Aspose.Pdf*, dan klik **Install**. Ini akan mengunduh versi stabil terbaru (per Juli 2026, versi 23.12).

## Langkah 2: Buka Dokumen PDF Sumber

Baris pertama dari setiap alur kerja **add bates numbering pdf** adalah memuat file yang ingin Anda beri stempel. Kami akan membungkus operasi dalam blok `using` sehingga dokumen dibuang secara otomatis.

```csharp
using Aspose.Pdf;

// Step 2: Load the PDF you want to number
using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
{
    // Subsequent steps go here...
}
```

> **Tips pro:** Jika PDF Anda berada di bucket cloud, Anda dapat memberikan `Stream` alih-alih jalur file—Aspose.PDF menangani keduanya dengan mulus.

## Langkah 3: Atur Nomor Mulai dan Prefix

Sekarang masuk ke inti dari **bates numbering example**: memberi tahu Aspose di mana memulai dan teks apa yang harus mendahului setiap nomor. Properti `BatesNumbering` menampilkan baik `Start` maupun `Prefix`.

```csharp
    // Step 3a: Define where the numbering begins
    pdfDocument.BatesNumbering.Start = 1000;   // you can start anywhere

    // Step 3b: Add a custom prefix – this is the prefix bates number you asked for
    pdfDocument.BatesNumbering.Prefix = "ABC-";
```

Mengapa menggunakan prefix? Dalam banyak kasus hukum, prefix mengidentifikasi berkas kasus, departemen, atau batch produksi. Menggunakan `"ABC-"` sebagai placeholder, Anda dapat mengubahnya menjadi `"CASE42-"` atau string apa pun yang sesuai dengan konvensi penamaan Anda.

## Langkah 4: Pilih Lokasi Penampilan Nomor (Opsional)

Aspose secara default menempatkan nomor di sudut kanan bawah, tetapi Anda dapat memindahkannya ke mana saja dengan menyesuaikan properti `Location`. Langkah ini tidak wajib untuk operasi **add bates numbering pdf** dasar, namun berguna untuk diketahui.

```csharp
    // Optional: Move the number to the top‑left corner
    pdfDocument.BatesNumbering.Location = new Location(10, pdfDocument.Pages[1].PageInfo.Height - 30);
```

Properti `Location` menggunakan koordinat X dan Y yang diukur dalam poin (1 pt ≈ 1/72 in). Sesuaikan sesuai kebutuhan tata letak halaman Anda.

## Langkah 5: Simpan PDF yang Diperbarui

Akhirnya, simpan perubahan. Metode `Save` pada `BatesNumbering` menulis file baru sambil mempertahankan file asli tidak berubah.

```csharp
    // Step 5: Write the output file with numbering applied
    pdfDocument.BatesNumbering.Save("YOUR_DIRECTORY/output.pdf");
}
```

Saat Anda membuka `output.pdf`, setiap halaman akan menampilkan sesuatu seperti `ABC-1000`, `ABC-1001`, … hingga halaman terakhir.

## Contoh Kerja Lengkap

Menggabungkan semuanya, berikut adalah **bates numbering example** yang dapat Anda salin‑tempel ke metode `Main` aplikasi console:

```csharp
using System;
using Aspose.Pdf;

class Program
{
    static void Main()
    {
        // Path configuration – adjust to your environment
        string inputPath = @"YOUR_DIRECTORY\input.pdf";
        string outputPath = @"YOUR_DIRECTORY\output.pdf";

        // Load the PDF
        using (var pdfDocument = new Document(inputPath))
        {
            // Set start number and prefix
            pdfDocument.BatesNumbering.Start = 1000;
            pdfDocument.BatesNumbering.Prefix = "ABC-";

            // (Optional) Change location – comment out if default is fine
            // pdfDocument.BatesNumbering.Location = new Location(10, pdfDocument.Pages[1].PageInfo.Height - 30);

            // Save the numbered PDF
            pdfDocument.BatesNumbering.Save(outputPath);
        }

        Console.WriteLine($"Bates numbering applied! Check: {outputPath}");
    }
}
```

**Output yang diharapkan** (di konsol):

```
Bates numbering applied! Check: YOUR_DIRECTORY\output.pdf
```

Buka PDF yang dihasilkan dan Anda akan melihat nomor berurutan dengan prefix `ABC-` mulai dari `1000`.

## Pertanyaan Umum & Kasus Tepi

### Bagaimana jika saya perlu mengatur ulang penghitung untuk setiap bagian?

Anda dapat memanggil `pdfDocument.BatesNumbering.Reset()` sebelum memproses rentang halaman baru. Gabungkan dengan loop pada `pdfDocument.Pages` dan atur kembali `Start` untuk setiap bagian.

### Bagaimana cara menerapkan prefix berbeda untuk rentang halaman yang berbeda?

Buat beberapa objek `BatesNumbering`—satu per rentang—dengan mengkloning dokumen atau menggunakan metode `Add` (tersedia di versi Aspose yang lebih baru). Berikut contoh singkatnya:

```csharp
// Number first 10 pages with "PRE‑"
pdfDocument.BatesNumbering.Start = 1;
pdfDocument.BatesNumbering.Prefix = "PRE-";
pdfDocument.BatesNumbering.Save(outputPath, new PageRange(1, 10));

// Number the rest with "POST‑"
pdfDocument.BatesNumbering.Start = 1;
pdfDocument.BatesNumbering.Prefix = "POST-";
pdfDocument.BatesNumbering.Save(outputPath, new PageRange(11, pdfDocument.Pages.Count));
```

### Apakah perpustakaan mendukung prefix Unicode?

Tentu saja. Berikan string Unicode apa pun (mis., `"案件‑"`). Aspose.PDF menangani skrip kanan‑ke‑kiri dan simbol khusus tanpa konfigurasi tambahan.

### Bagaimana dengan keamanan PDF—apakah penomoran Bates akan merusak enkripsi?

Jika PDF sumber dienkripsi, Anda harus memberikan kata sandi sebelum mengakses `BatesNumbering`. Proses penomoran menghormati pengaturan enkripsi asli—output Anda akan tetap terenkripsi kecuali Anda secara eksplisit mengubahnya.

```csharp
pdfDocument.Encrypt(new DocumentEncryption("ownerPwd", "userPwd"));
```

## Tips & Praktik Terbaik

- **Pemrosesan batch:** Bungkus seluruh rutinitas dalam loop `foreach` untuk menangani puluhan file secara otomatis.
- **Logging:** Catat nomor mulai, prefix, dan jalur output ke file log; ini mempermudah jejak audit untuk tim hukum.
- **Kinerja:** Untuk PDF besar (500 + halaman), pertimbangkan mengaktifkan **optimisasi memori** melalui `pdfDocument.OptimizeMemory = true;`.
- **Pengujian:** Selalu simpan salinan PDF asli; penomoran Bates tidak dapat dibatalkan setelah disimpan.

## Kesimpulan

Dalam **bates numbering tutorial** ini kami telah membahas semua yang Anda perlukan untuk **add bates numbering pdf** file dengan Aspose.PDF:

1. Instal perpustakaan.
2. Muat dokumen sumber Anda.
3. Atur nomor mulai dan **prefix bates number**.
4. (Opsional) sesuaikan penempatan.
5. Simpan hasilnya.

Anda kini memiliki contoh **bates numbering example** yang solid yang dapat Anda sesuaikan untuk alur kerja hukum, arsip, atau kepatuhan apa pun. Ingin melangkah lebih jauh? Coba gabungkan nomor Bates dengan watermark, atau hasilkan manifest CSV yang memetakan setiap halaman ke identifier-nya. Langit adalah batasnya, dan Aspose memberi Anda alat untuk mencapainya.

*Siap menerapkannya ke produksi? Tinggalkan komentar jika Anda mengalami kendala, dan selamat coding!*

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait erat yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Terapkan Gaya Penomoran di Heading PDF menggunakan Java](/pdf/english/java/pdf-images/apply-numbering-style-in-heading-of-pdf-using-java/)
- [Aspose Pdf Net Floatingbox Penomoran Halaman](/pdf/german/net/text-operations/aspose-pdf-net-floatingbox-page-numbering/)
- [Terapkan Gaya Penomoran di Heading PDF Menggunakan Java](/pdf/german/java/pdf-images/apply-numbering-style-in-heading-of-pdf-using-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}