---
category: general
date: 2026-06-21
description: Tambahkan penomoran Bates di Word dengan cepat. Pelajari cara menambahkan
  Bates, menerapkan penomoran Bates untuk dokumen hukum, dan mengotomatiskan penomoran
  dengan C#.
draft: false
keywords:
- add bates numbering
- how to add bates
- bates numbering in word
- bates numbering for legal
- apply bates numbering
language: id
og_description: Tambahkan penomoran Bates di Word menggunakan C#. Panduan ini menunjukkan
  cara menambahkan Bates, menerapkan penomoran Bates untuk dokumen hukum, dan mengotomatiskan
  prosesnya.
og_title: Tambahkan Penomoran Bates di Word – Panduan Pemrograman Lengkap
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Add Bates numbering in Word quickly. Learn how to add Bates, apply
    Bates numbering for legal docs, and automate numbering with C#.
  headline: Add Bates Numbering in Word – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Add Bates numbering in Word quickly. Learn how to add Bates, apply
    Bates numbering for legal docs, and automate numbering with C#.
  name: Add Bates Numbering in Word – Complete Step‑by‑Step Guide
  steps:
  - name: Expected Output
    text: '| Page | Bates Number | |------|--------------| | 1 | ABC-1000 | | 2 |
      ABC-1001 | | … | … | | N | ABC‑(1000 + N‑1) |'
  - name: What if the document already contains page numbers?
    text: The `AddBatesNumbering` method will **not** overwrite existing page number
      fields; it simply adds a new field. If you want to replace the existing numbers,
      remove them first or set `batesOptions.Position` to the same location as the
      current page numbers.
  - name: Can I skip pages (e.g., exclude a cover page)?
    text: 'Yes. Use the overload that accepts a `PageRange`:'
  - name: How do I change the numbering format (Roman numerals, letters)?
    text: 'The `BatesNumberingOptions` class supports a `NumberFormat` property:'
  - name: What about performance on huge files?
    text: Loading a 2‑GB Word file can consume a lot of RAM. To mitigate, process
      the document in chunks using the `DocumentSplitter` utility, apply Bates numbering
      to each chunk, then merge the parts back together. This pattern keeps memory
      usage under control while still letting you **apply bates numbering*
  type: HowTo
tags:
- document‑automation
- csharp
- legal‑tech
title: Tambahkan Penomoran Bates di Word – Panduan Lengkap Langkah demi Langkah
url: /id/net/programming-with-document/add-bates-numbering-in-word-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tambahkan Penomoran Bates di Word – Panduan Lengkap Langkah‑per‑Langkah

Pernah bertanya-tanya bagaimana cara menambahkan penomoran Bates ke file Word tanpa harus mengetik setiap nomor secara manual? Anda tidak sendirian. Banyak pengacara, paralegal, dan spesialis e‑discovery membutuhkan cara yang andal untuk **menambahkan penomoran Bates** ke ratusan halaman, dan melakukannya secara manual adalah mimpi buruk.

Dalam tutorial ini kami akan membahas solusi C# yang bersih yang **menerapkan penomoran Bates** ke file `.docx`, menjelaskan mengapa setiap baris penting, dan menunjukkan cara menyesuaikan kode untuk kebutuhan khusus hukum. Pada akhir tutorial Anda akan dapat menghasilkan dokumen bernomor sempurna dalam hitungan detik—tanpa plugin tambahan.

## Apa yang Akan Anda Pelajari

- Kode tepat yang diperlukan untuk **menambahkan penomoran Bates** ke dokumen Word.  
- Cara kerja kelas `BatesNumberingOptions` dan mengapa Anda mungkin menyesuaikan prefix atau nilai awal.  
- Tips menggunakan pendekatan ini pada file kasus besar, termasuk pertimbangan memori.  
- Ringkasan singkat prasyarat sehingga Anda dapat menyalin‑tempel solusi dan menjalankannya hari ini.

**Prasyarat**  
- .NET 6+ (atau .NET Framework 4.7.2+ jika Anda lebih suka runtime lama).  
- Referensi ke pustaka Aspose.Words for .NET (atau API serupa yang menyediakan `AddBatesNumbering`).  
- Familiaritas dasar dengan C# dan Visual Studio (atau IDE favorit Anda).

Jika Anda sudah nyaman dengan hal‑hal tersebut, mari kita mulai.

## Langkah 1: Siapkan Proyek dan Impor Pustaka

Pertama, buat aplikasi console baru (atau integrasikan ke layanan yang sudah ada). Kemudian tambahkan paket NuGet Aspose.Words:

```bash
dotnet add package Aspose.Words
```

> **Pro tip:** Gunakan lisensi evaluasi gratis untuk pengujian; lisensi ini menambahkan watermark kecil tetapi berfungsi persis seperti versi penuh.

```csharp
using Aspose.Words;
using Aspose.Words.BatesNumbering;
```

Pernyataan `using` ini membawa kelas `Document` dan `BatesNumberingOptions` ke dalam ruang lingkup, yang penting untuk langkah **menerapkan penomoran Bates** nanti.

## Langkah 2: Muat Dokumen Sumber

Anda memerlukan file Word untuk diproses. Kode di bawah memuat `input.docx` dari folder yang Anda tentukan. Ganti `"YOUR_DIRECTORY"` dengan jalur sebenarnya di mesin Anda.

```csharp
// Step 1: Load the source document
var document = new Document("YOUR_DIRECTORY/input.docx");
```

Mengapa harus memuat file terlebih dahulu? Objek `Document` mem-parsing seluruh paket Word ke dalam memori, memungkinkan kita memanipulasi header, footer, dan tata letak halaman sebelum menyimpan. Jika file sangat besar (misalnya 10.000 halaman), pertimbangkan menggunakan `LoadOptions` dengan `LoadFormat.Docx` untuk men-stream bagian‑bagian alih‑alih memuat semuanya sekaligus.

## Langkah 3: Konfigurasikan Opsi Penomoran Bates

Di sinilah keajaiban terjadi. Anda memberi tahu pustaka prefix apa yang akan digunakan (`"ABC-"` dalam contoh) dan dari nomor berapa mulai menghitung (`1000`). Kedua nilai dapat disesuaikan sepenuhnya.

```csharp
// Step 2: Define Bates numbering options (prefix and starting number)
var batesOptions = new BatesNumberingOptions
{
    Prefix = "ABC-",
    Start = 1000,
    // Optional: set the position, alignment, and font if you need legal‑specific styling
    // Position = BatesNumberingPosition.Footer,
    // Alignment = BatesNumberingAlignment.Right,
    // Font = new Font("Times New Roman", 10, FontStyle.Bold)
};
```

**Mengapa menggunakan prefix?** Dalam praktik hukum, prefix sering mengidentifikasi kasus atau pihak yang memproduksi (`"ABC-"` dapat mewakili *Acme Bank Corp.*). Memulai dari `1000` umum karena banyak firma menyimpan 999 nomor pertama untuk draft internal.

Jika Anda menangani **penomoran Bates untuk dokumen hukum**, Anda mungkin juga ingin mengatur `batesOptions.Position` ke `Header` atau `Footer` dan menyesuaikan perataan agar sesuai dengan aturan pengadilan. Pustaka ini mendukung penyesuaian tersebut secara bawaan.

## Langkah 4: Terapkan Penomoran Bates ke Seluruh Dokumen

Sekarang kita benar‑benar menyisipkan nomor. Metode `AddBatesNumbering` berjalan melalui setiap halaman, menyisipkan string terformat, dan memperbarui hitungan halaman internal dokumen.

```csharp
// Step 3: Apply Bates numbering to the entire document
document.AddBatesNumbering(batesOptions);
```

Di balik layar, Aspose.Words membuat field tersembunyi pada setiap halaman yang ditampilkan sebagai `ABC-1000`, `ABC-1001`, dan seterusnya. Karena berupa field, Anda dapat mengedit prefix atau nomor awal nanti tanpa harus menghasilkan ulang seluruh file—praktis untuk **cara menambahkan bates** setelah permintaan discovery berubah.

## Langkah 5: Simpan Dokumen yang Telah Dimodifikasi

Akhirnya, tulis output ke file baru. Menjaga file asli tetap tidak tersentuh adalah praktik terbaik, terutama saat berurusan dengan bukti yang harus tetap pristine.

```csharp
// Step 4: Save the modified document
document.Save("YOUR_DIRECTORY/output.docx");
```

Sekarang Anda memiliki `output.docx` dengan nomor Bates berurutan yang ditambahkan ke setiap halaman. Buka di Word, dan Anda akan melihat nomor tepat di tempat yang Anda tentukan (biasanya di footer). Ukuran file mungkin sedikit bertambah karena field tambahan, tetapi peningkatannya tidak signifikan dibandingkan manfaatnya.

### Output yang Diharapkan

| Halaman | Nomor Bates |
|---------|-------------|
| 1       | ABC-1000    |
| 2       | ABC-1001    |
| …       | …           |
| N       | ABC‑(1000 + N‑1) |

Jika Anda membuka tampilan “Field Codes” dokumen (`Alt+F9` di Word), Anda akan melihat sesuatu seperti `{ BATES \* MERGEFORMAT ABC-1000 }` pada setiap halaman.

## Kasus Khusus & Pertanyaan Umum

### Bagaimana jika dokumen sudah berisi nomor halaman?

Metode `AddBatesNumbering` **tidak** akan menimpa field nomor halaman yang sudah ada; ia hanya menambahkan field baru. Jika Anda ingin mengganti nomor yang ada, hapus dulu atau atur `batesOptions.Position` ke lokasi yang sama dengan nomor halaman saat ini.

### Bisakah saya melewatkan halaman (misalnya mengecualikan halaman sampul)?

Ya. Gunakan overload yang menerima `PageRange`:

```csharp
var range = new PageRange(2, document.PageCount); // start at page 2
document.AddBatesNumbering(batesOptions, range);
```

Ini berguna ketika Anda membutuhkan **penomoran Bates untuk dokumen hukum** yang dimulai setelah halaman judul.

### Bagaimana cara mengubah format penomoran (angka Romawi, huruf)?

Kelas `BatesNumberingOptions` mendukung properti `NumberFormat`:

```csharp
batesOptions.NumberFormat = BatesNumberFormat.RomanUpper;
```

Setel sebelum memanggil `AddBatesNumbering`. Fleksibilitas ini membantu ketika pengadilan mewajibkan gaya tertentu.

### Bagaimana dengan kinerja pada file yang sangat besar?

Memuat file Word berukuran 2 GB dapat mengonsumsi banyak RAM. Untuk mengurangi beban, proses dokumen dalam potongan menggunakan utilitas `DocumentSplitter`, terapkan penomoran Bates pada tiap potongan, lalu gabungkan kembali. Pola ini menjaga penggunaan memori tetap terkendali sambil tetap memungkinkan **menerapkan penomoran Bates** secara efisien.

## Contoh Lengkap yang Siap Jalan

Menggabungkan semua langkah, berikut program console yang siap dijalankan:

```csharp
using System;
using Aspose.Words;
using Aspose.Words.BatesNumbering;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the source document
            var inputPath = @"C:\Docs\input.docx";
            var document = new Document(inputPath);

            // 2️⃣ Define Bates numbering options
            var batesOptions = new BatesNumberingOptions
            {
                Prefix = "ABC-",
                Start = 1000,
                // Optional styling for legal compliance
                Position = BatesNumberingPosition.Footer,
                Alignment = BatesNumberingAlignment.Right,
                Font = new Font("Times New Roman", 9, FontStyle.Bold)
            };

            // 3️⃣ Apply Bates numbering across all pages
            document.AddBatesNumbering(batesOptions);

            // 4️⃣ Save the result
            var outputPath = @"C:\Docs\output.docx";
            document.Save(outputPath);

            Console.WriteLine($"✅ Bates numbering applied! Saved to {outputPath}");
        }
    }
}
```

Jalankan program, buka `output.docx`, dan Anda akan melihat rangkaian nomor bersih yang siap untuk filing, discovery, atau pengajuan ke pengadilan.

## Kesimpulan

Anda kini tahu persis **cara menambahkan Bates** ke dokumen Word menggunakan C#. Langkah‑langkah—muat, konfigurasikan, terapkan, dan simpan—sederhana, namun cukup fleksibel untuk memenuhi **penomoran Bates untuk alur kerja hukum**, prefix khusus, bahkan pemrosesan batch berskala besar.

Jika Anda ingin melangkah lebih jauh, pertimbangkan:

- Mengintegrasikan kode ke dalam web API sehingga rekan dapat mengunggah file dan menerima PDF bernomor secara instan.  
- Menambahkan penanganan error untuk file yang hilang atau masalah izin (misalnya `try/catch` di sekitar `Document.Load`).  
- Menjelajahi fitur Aspose.Words lain seperti watermark atau redaction untuk toolkit e‑discovery lengkap.

Jangan ragu bereksperimen dengan prefix berbeda, nomor awal yang lain, atau bahkan menggabungkan beberapa skema penomoran dalam satu dokumen. Dunia **menerapkan penomoran Bates** ternyata sangat fleksibel setelah Anda menguasai logika dasarnya.

Punya pertanyaan atau skenario rumit? Tinggalkan komentar di bawah, dan kami akan membantu memecahkannya bersama. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah‑per‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Apply Numbering Style in Heading of PDF using Java](/pdf/english/java/pdf-images/apply-numbering-style-in-heading-of-pdf-using-java/)
- [Apply Numbering Style In Heading Of Pdf Using Java](/pdf/german/java/pdf-images/apply-numbering-style-in-heading-of-pdf-using-java/)
- [Apply Numbering Style In Heading Of Pdf Using Java](/pdf/french/java/pdf-images/apply-numbering-style-in-heading-of-pdf-using-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}