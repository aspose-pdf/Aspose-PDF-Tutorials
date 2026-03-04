---
category: general
date: 2026-03-03
description: Buat Dokumen PDF C# dengan penomoran Bates – pelajari cara menambahkan
  Bates, menambahkan nomor halaman berurutan, dan menghasilkan Bates dalam beberapa
  langkah saja.
draft: false
keywords:
- create pdf document c#
- add bates numbering pdf
- how to add bates
- add sequential page numbers
- how to generate bates
language: id
og_description: Buat Dokumen PDF C# dengan penomoran Bates. Panduan ini menunjukkan
  cara menambahkan Bates, menambahkan nomor halaman berurutan, dan menghasilkan Bates
  dengan cepat.
og_title: Buat Dokumen PDF C# – Tambahkan Penomoran Bates
tags:
- C#
- PDF
- Bates numbering
title: Buat Dokumen PDF C# – Tambahkan Penomoran Bates
url: /id/net/programming-with-pdf-pages/create-pdf-document-c-add-bates-numbering/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Membuat Dokumen PDF C# – Tambahkan Penomoran Bates

Pernah membutuhkan **create PDF document C#** dan kemudian menandai setiap halaman dengan pengenal unik untuk keperluan hukum atau arsip? Anda bukan satu-satunya—firma hukum, pengadilan, bahkan korporasi besar terus bertanya, “Bagaimana cara menambahkan nomor Bates ke PDF saya secara otomatis?” Kabar baiknya, dengan beberapa baris kode Anda dapat menghasilkan PDF, menaburkan nomor Bates di setiap halaman, dan menyimpan hasilnya tanpa pernah membuka editor.

Dalam tutorial ini kami akan membahas contoh praktis end‑to‑end yang menunjukkan **how to add Bates**, cara **add sequential page numbers**, dan bahkan cara **generate Bates** dengan awalan khusus. Pada akhir tutorial Anda akan memiliki potongan kode yang dapat digunakan kembali dan dapat dimasukkan ke proyek .NET mana pun.

## Apa yang Anda Butuhkan

- **.NET 6+** (kode ini juga berfungsi pada .NET Framework 4.6+)
- **Aspose.Pdf for .NET** – perpustakaan komersial yang menyediakan API bersih untuk manipulasi PDF. Evaluasi gratis sudah cukup untuk pengujian.
- Pemahaman dasar tentang C# (Anda mungkin sudah terbiasa dengan pernyataan `using` dan objek).

Tidak ada paket NuGet tambahan yang diperlukan selain `Aspose.Pdf`. Jika Anda belum menginstalnya, jalankan:

```bash
dotnet add package Aspose.Pdf
```

> **Pro tip:** Pastikan versi Aspose Anda selalu terbaru; rilis 23.x terbaru menambahkan penyesuaian kinerja untuk dokumen besar.

## Langkah 1: Buka (atau Buat) Dokumen PDF Sumber

Pertama, kita memerlukan PDF untuk diproses. Dalam banyak skenario dunia nyata Anda sudah memiliki file masukan—misalnya kontrak yang dipindai. Untuk contoh ini kita akan membuka file yang sudah ada bernama `input.pdf`.

```csharp
using Aspose.Pdf;

// Step 1 – Load the PDF you want to number
var pdfPath = @"C:\Docs\input.pdf";
using var pdfDocument = new Document(pdfPath);
```

> **Mengapa ini penting:** Membuka dokumen di dalam blok `using` menjamin handle file dilepaskan dengan cepat, menghindari masalah penguncian file ketika Anda kemudian mencoba menimpa file yang sama.

## Langkah 2: Tentukan Opsi Penomoran Bates Anda

Nomor Bates terdiri dari **prefix** (seringkali pengidentifikasi kasus) dan **starting number**. Anda juga dapat mengontrol jumlah digit, penempatan pada halaman, dan gaya font. Di sini kami akan menggunakan kata kunci sekunder **add bates numbering pdf** dengan mengonfigurasi objek `BatesNumberingOptions`.

```csharp
// Step 2 – Set up Bates numbering preferences
var batesOptions = new BatesNumberingOptions
{
    // Primary keyword in action: create pdf document c# with custom settings
    Prefix = "CASE-",
    Start = 1000,
    // Optional: set zero‑padding to 6 digits (e.g., CASE-001000)
    NumberOfDigits = 6,
    // Optional: define where the number appears (bottom‑right corner)
    HorizontalAlignment = HorizontalAlignment.Right,
    VerticalAlignment   = VerticalAlignment.Bottom,
    // Optional: choose a readable font
    Font = FontRepository.FindFont("Arial")
};
```

> **Cara menambahkan bates:** Dengan menyesuaikan `Prefix` dan `Start` Anda mengontrol string tepat yang akan muncul pada setiap halaman. Properti `NumberOfDigits` memastikan lebar konsisten, yang berguna untuk pengajuan hukum.

## Langkah 3: Terapkan Penomoran Bates ke Setiap Halaman

Sekarang datang operasi inti—menambahkan nomor. Metode `AddBatesNumbering` melintasi setiap halaman, menggambar teks, dan menghormati opsi yang telah kami definisikan.

```csharp
// Step 3 – Apply Bates numbering to all pages
pdfDocument.AddBatesNumbering(batesOptions);
```

Di balik layar Aspose merender teks sebagai elemen *content*, artinya nomor menjadi bagian dari PDF dan tidak dapat dimatikan di penampil. Ini persis yang Anda butuhkan ketika ingin **add sequential page numbers** yang tidak dapat diubah.

### Kasus Khusus & Variasi

- **Multiple prefixes:** Jika Anda memerlukan awalan berbeda per bagian, buat `BatesNumberingOptions` terpisah dan panggil `AddBatesNumbering` pada rentang halaman (`pdfDocument.Pages[1..5]`).
- **Zero‑padding control:** Hilangkan `NumberOfDigits` untuk nomor dengan panjang variabel, atau setel ke nilai lebih tinggi untuk menambahkan nol di depan.
- **Custom positioning:** Gunakan `Margin` untuk menggeser nomor dari tepi, atau ubah `HorizontalAlignment` menjadi `Center` untuk gaya footer.

## Langkah 4: Simpan PDF yang Telah Dimodifikasi

Akhirnya, tulis dokumen yang telah diperbarui ke disk. Anda dapat menimpa file asli atau membuat file baru.

```csharp
// Step 4 – Save the PDF with Bates numbers applied
var outputPath = @"C:\Docs\output.pdf";
pdfDocument.Save(outputPath);
```

Setelah baris ini dijalankan, `output.pdf` berisi konten asli ditambah tag Bates yang terlihat pada setiap halaman—tepat seperti yang Anda harapkan ketika **how to generate bates** untuk berkas kasus.

## Contoh Lengkap yang Dapat Dijalankan

Menggabungkan semuanya, berikut potongan kode lengkap yang dapat Anda salin‑tempel ke aplikasi console:

```csharp
using System;
using Aspose.Pdf;

class Program
{
    static void Main()
    {
        // 1️⃣ Open the source PDF
        var inputFile = @"C:\Docs\input.pdf";
        using var pdf = new Document(inputFile);

        // 2️⃣ Configure Bates numbering (add bates numbering pdf)
        var options = new BatesNumberingOptions
        {
            Prefix = "CASE-",
            Start = 1000,
            NumberOfDigits = 6,
            HorizontalAlignment = HorizontalAlignment.Right,
            VerticalAlignment = VerticalAlignment.Bottom,
            Font = FontRepository.FindFont("Arial")
        };

        // 3️⃣ Apply the numbering (how to add bates)
        pdf.AddBatesNumbering(options);

        // 4️⃣ Save the result (add sequential page numbers)
        var outputFile = @"C:\Docs\output.pdf";
        pdf.Save(outputFile);

        Console.WriteLine("Bates numbering applied successfully!");
    }
}
```

### Hasil yang Diharapkan

Buka `output.pdf` di penampil apa pun (Adobe Reader, Edge, dll.). Anda akan melihat setiap halaman dicap dengan sesuatu seperti **CASE-001000**, **CASE-001001**, … hingga halaman terakhir. Nomor tersebut terletak rapi di kanan‑bawah, sesuai dengan opsi yang kami atur.

## Pertanyaan Umum & Pemecahan Masalah

- **“Bagaimana jika PDF saya dilindungi kata sandi?”**  
  Muat dengan kata sandi: `new Document(inputFile, new LoadOptions { Password = "secret" })`.

- **“Bisakah saya menambahkan nomor Bates ke PDF yang baru dibuat?”**  
  Tentu saja. Buat dokumen terlebih dahulu (`var doc = new Document();`) lalu ikuti Langkah 2‑4 sebelum menyimpan.

- **“Apakah font selalu disematkan?”**  
  Aspose secara otomatis menyematkan font jika belum ada di PDF. Jika Anda memerlukan keluarga font tertentu, setel `options.Font` sesuai.

- **“Bagaimana dengan kinerja pada file 10.000 halaman?”**  
  Perpustakaan ini men‑stream halaman, sehingga penggunaan memori tetap rendah. Namun, Anda mungkin ingin meningkatkan `PdfSaveOptions.CompressionMode` untuk I/O yang lebih cepat.

## Tips Pro untuk Penggunaan Produksi

1. **Batch processing:** Bungkus logika di atas dalam loop yang mengiterasi folder berisi PDF. Gunakan `Directory.GetFiles("*.pdf")` dan proses setiap file secara terpisah.
2. **Logging:** Catat nomor Bates pertama dan terakhir ke file log—membantu auditor memverifikasi bahwa penomoran berkelanjutan.
3. **Error handling:** Bungkus seluruh blok dalam `try/catch` dan tampilkan pesan jelas jika PDF sumber tidak ada atau rusak.
4. **Zero‑padding flexibility:** Jika Anda memerlukan jumlah digit dinamis berdasarkan total halaman, hitung `NumberOfDigits = (pdf.Pages.Count + options.Start).ToString().Length`.

## Kesimpulan

Kami baru saja menunjukkan cara **create PDF document C#** dan secara mulus **add Bates numbering**—mencakup semua mulai dari pemuatan awal hingga penyimpanan akhir. Contoh singkat ini memperlihatkan **how to add bates**, **add sequential page numbers**, dan **how to generate bates** dengan awalan khusus dan zero‑padding. Dengan beberapa penyesuaian Anda dapat mengadaptasi pola ini ke pekerjaan batch, tata letak berbeda, atau bahkan mengintegrasikannya ke dalam API web yang mengembalikan PDF yang baru saja diberi nomor sesuai permintaan.

Siap untuk langkah selanjutnya? Cobalah menggabungkan ini dengan fitur **watermark** Aspose, atau buat indeks ringkasan yang mencantumkan setiap nomor Bates beserta deskripsi singkat isi halaman. Kemungkinannya tak terbatas, dan kode yang Anda miliki kini menjadi fondasi yang kuat untuk alur kerja otomatisasi dokumen apa pun.

Selamat coding, dan semoga PDF Anda selalu bernomor dengan sempurna! 

![Tangkapan layar penampil PDF yang menampilkan create pdf document c# dengan nomor Bates yang diterapkan](image-placeholder.png "create pdf document c# dengan nomor Bates")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}