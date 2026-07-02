---
category: general
date: 2026-06-30
description: Tambahkan penomoran Bates ke PDF menggunakan Aspose.PDF dalam C#. Pelajari
  cara memberi nomor pada halaman PDF, mengatur awalan khusus, dan membuat dokumen
  penomoran Bates yang handal.
draft: false
keywords:
- add bates numbering
- how to add bates
- number pdf pages
- how to number pdf
- bates numbering document
language: id
og_description: Tambahkan penomoran Bates ke PDF dengan Aspose.PDF. Panduan ini menunjukkan
  cara memberi nomor halaman PDF dan membuat dokumen penomoran Bates dalam C#.
og_title: Tambahkan Penomoran Bates ke PDF – Panduan Aspose.PDF
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Add Bates numbering to PDF using Aspose.PDF in C#. Learn how to number
    PDF pages, set a custom prefix, and create a reliable Bates numbering document.
  headline: Add Bates Numbering to PDF with Aspose.PDF – Complete Guide
  type: TechArticle
- description: Add Bates numbering to PDF using Aspose.PDF in C#. Learn how to number
    PDF pages, set a custom prefix, and create a reliable Bates numbering document.
  name: Add Bates Numbering to PDF with Aspose.PDF – Complete Guide
  steps:
  - name: Customizing Appearance (Optional)
    text: 'If you need a different font, size, or placement, you can tweak the `BatesNumbering`
      properties:'
  - name: Expected Output
    text: Open `bates_numbered.pdf` in any PDF viewer. You’ll see a label like **CASE‑1000**
      on the first page, **CASE‑1001** on the second, and so on. The numbers appear
      in the bottom‑left corner by default (or wherever you set `XIndent`/`YIndent`).
  - name: 1. What if the PDF is huge (hundreds of MB)?
    text: 'Aspose.PDF streams pages to disk by default, so memory consumption stays
      low. However, you can explicitly enable **compression**:'
  - name: 2. Need a different numbering format (e.g., suffix instead of prefix)?
    text: 'Set the `Suffix` property:'
  - name: 3. How to restart numbering for a new section?
    text: Call `bates.StartNumber = 1;` before processing the next batch, or create
      a second `BatesNumbering` instance.
  - name: 4. The PDF already contains watermarks—will the numbers overlap?
    text: 'Adjust `XIndent` and `YIndent` to move the numbers away from existing elements.
      You can also change the `Position` enum (`BatesNumberingPosition.TopRight`,
      etc.):'
  - name: 5. Does this work with encrypted PDFs?
    text: 'If the source PDF is password‑protected, open it like this:'
  type: HowTo
tags:
- Aspose.PDF
- C#
- PDF processing
- Bates numbering
title: Tambahkan Penomoran Bates ke PDF dengan Aspose.PDF – Panduan Lengkap
url: /id/net/programming-with-pdf-pages/add-bates-numbering-to-pdf-with-aspose-pdf-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tambahkan Penomoran Bates ke PDF dengan Aspose.PDF – Panduan Lengkap

Pernah membutuhkan untuk **menambahkan penomoran bates** ke PDF tetapi tidak yakin harus mulai dari mana? Anda bukan satu-satunya—tim hukum, auditor, dan bahkan pengembang sering bertanya *bagaimana menambahkan bates* untuk melacak kumpulan dokumen besar. Dalam tutorial ini kami akan membahas solusi lengkap yang siap dijalankan yang memberi nomor pada halaman PDF, menerapkan awalan khusus, dan menyimpan **dokumen penomoran bates** yang baru. Tanpa basa‑basi, hanya kode yang dapat Anda salin‑tempel hari ini.

Kami akan membahas semuanya mulai dari menyiapkan Aspose.PDF, memilih nomor awal, menangani kasus tepi seperti file besar, dan bahkan menyesuaikan format jika Anda membutuhkan sesuatu di luar default. Pada akhir tutorial Anda akan dapat **menomori halaman pdf** secara otomatis, dan Anda akan memahami mengapa pendekatan ini kuat dan mudah dipelihara.

## Prasyarat

- .NET 6.0 atau lebih baru (contoh menggunakan .NET 6 tetapi bekerja dengan .NET Core 3.1+)
- Lisensi Aspose.PDF untuk .NET (evaluasi gratis dapat digunakan untuk pengujian)
- File PDF yang ingin Anda proses (dengan nama `source.pdf` dalam contoh)
- Visual Studio 2022 atau editor C# apa pun yang Anda sukai

Itu saja—tidak ada paket NuGet tambahan selain Aspose.PDF.

## Langkah 1: Instal Aspose.PDF untuk .NET

Buka terminal atau Package Manager Console Anda dan jalankan:

```bash
dotnet add package Aspose.PDF
```

atau, di dalam Visual Studio:

```
Tools → NuGet Package Manager → Manage NuGet Packages for Solution…
Search “Aspose.PDF” and click Install.
```

> **Pro tip:** Jika Anda berencana memproses ribuan halaman, aktifkan **mode penghematan memori Aspose.PDF** dengan mengatur `PdfConversion.SaveOptions.UseObjectPooling = true;` nanti.

## Langkah 2: Buat Kerangka Aplikasi Konsol Sederhana

Mari buat aplikasi konsol minimal sehingga Anda dapat menjalankan kode secara langsung:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Facades;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll fill this in the next steps.
        }
    }
}
```

Simpan file sebagai `Program.cs`. Kerangka ini memberi kami tempat bersih untuk menempatkan logika **penomoran bates**.

## Langkah 3: Buka Dokumen PDF Sumber

Operasi nyata pertama adalah membuka PDF yang ingin Anda cap. Kami akan menggunakan blok `using` sehingga pegangan file dilepaskan secara otomatis:

```csharp
// Step 3: Open the source PDF document
using (var doc = new Document("YOUR_DIRECTORY/source.pdf"))
{
    // Subsequent steps go here.
}
```

> **Mengapa blok `using`?** Itu menjamin aliran file yang mendasari ditutup, mencegah masalah penguncian file ketika Anda kemudian mencoba menimpa file yang sama.

## Langkah 4: Siapkan Fasade BatesNumbering

Aspose.PDF menyediakan fasade yang nyaman bernama `BatesNumbering`. Ini menyembunyikan penanganan halaman demi halaman tingkat rendah dan memungkinkan Anda fokus pada penomoran itu sendiri.

```csharp
// Step 4: Create a Bates numbering facade
var bates = new BatesNumbering
{
    // Step 4a: Choose the starting number
    StartNumber = 1000,

    // Step 4b: Add an optional prefix (e.g., CASE-)
    Prefix = "CASE-"
    
    // You can also set a suffix, font size, or position if needed.
};
```

### Menyesuaikan Penampilan (Opsional)

Jika Anda memerlukan font, ukuran, atau penempatan yang berbeda, Anda dapat menyesuaikan properti `BatesNumbering`:

```csharp
bates.FontSize = 10;               // Smaller than the default 12
bates.TextColor = Color.Black;    // Ensure high contrast
bates.XIndent = 20;               // Move number 20 points from the left edge
bates.YIndent = 30;               // Move number 30 points from the bottom edge
```

Pengaturan ini berguna ketika penempatan default mengganggu konten yang ada.

## Langkah 5: Terapkan Penomoran Bates ke Dokumen

Sekarang kami benar‑benar menempelkan nomor pada setiap halaman:

```csharp
// Step 5: Apply the Bates numbering to the document
bates.AddBatesNumbering(doc);
```

Di balik layar Aspose.PDF mengiterasi setiap halaman, menyisipkan string terformat (misalnya `CASE-1000`, `CASE-1001`, …), dan menghormati semua opsi tata letak yang Anda atur sebelumnya.

## Langkah 6: Simpan PDF yang Baru Dinomori

Akhirnya, tulis hasilnya ke disk. Anda dapat menimpa file asli atau membuat yang baru—di sini kami akan menyimpan keduanya untuk keamanan:

```csharp
// Step 6: Save the newly numbered PDF
doc.Save("YOUR_DIRECTORY/bates_numbered.pdf");
Console.WriteLine("Bates numbering applied successfully!");
```

Menjalankan program seharusnya menghasilkan file bernama `bates_numbered.pdf` dengan setiap halaman jelas berlabel.

### Output yang Diharapkan

Buka `bates_numbered.pdf` di penampil PDF apa pun. Anda akan melihat label seperti **CASE‑1000** pada halaman pertama, **CASE‑1001** pada halaman kedua, dan seterusnya. Angka muncul di sudut kiri bawah secara default (atau di mana pun Anda mengatur `XIndent`/`YIndent`).

## Contoh Kerja Lengkap

Menggabungkan semua bagian, berikut kode lengkap yang dapat Anda salin‑tempel:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Facades;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Adjust these paths to match your environment
            const string sourcePath = "YOUR_DIRECTORY/source.pdf";
            const string outputPath = "YOUR_DIRECTORY/bates_numbered.pdf";

            // Open the source PDF
            using (var doc = new Document(sourcePath))
            {
                // Configure Bates numbering
                var bates = new BatesNumbering
                {
                    StartNumber = 1000,
                    Prefix = "CASE-",
                    // Optional customizations:
                    // FontSize = 10,
                    // TextColor = Color.Black,
                    // XIndent = 20,
                    // YIndent = 30
                };

                // Apply numbering
                bates.AddBatesNumbering(doc);

                // Save the result
                doc.Save(outputPath);
                Console.WriteLine($"Bates numbering added. Saved to: {outputPath}");
            }
        }
    }
}
```

Jalankan `dotnet run` dari folder proyek, dan Anda akan melihat pesan konsol yang mengonfirmasi keberhasilan.

## Kasus Tepi & Pertanyaan Umum

### 1. Bagaimana jika PDF sangat besar (ratusan MB)?

Aspose.PDF mengalirkan halaman ke disk secara default, sehingga konsumsi memori tetap rendah. Namun, Anda dapat secara eksplisit mengaktifkan **kompresi**:

```csharp
doc.Compress();
```

### 2. Membutuhkan format penomoran yang berbeda (mis., akhiran alih-alih awalan)?

Atur properti `Suffix`:

```csharp
bates.Suffix = "-2026";
```

Anda dapat menggabungkan keduanya:

```csharp
bates.Prefix = "CASE-";
bates.Suffix = "-2026";
```

Hasil: `CASE-1000-2026`.

### 3. Bagaimana cara memulai ulang penomoran untuk bagian baru?

Panggil `bates.StartNumber = 1;` sebelum memproses batch berikutnya, atau buat instance `BatesNumbering` kedua.

### 4. PDF sudah berisi watermark—apakah nomor akan tumpang tindih?

Sesuaikan `XIndent` dan `YIndent` untuk memindahkan nomor menjauh dari elemen yang ada. Anda juga dapat mengubah enum `Position` (`BatesNumberingPosition.TopRight`, dll.):

```csharp
bates.Position = BatesNumberingPosition.TopRight;
```

### 5. Apakah ini bekerja dengan PDF terenkripsi?

Jika PDF sumber dilindungi kata sandi, buka seperti ini:

```csharp
var doc = new Document(sourcePath, new LoadOptions { Password = "yourPassword" });
```

Sisa alur kerja tetap tidak berubah.

## Tips untuk Implementasi Siap Produksi

- **Lisensi lebih awal**: Sisipkan `Aspose.Pdf.License license = new Aspose.Pdf.License(); license.SetLicense("Aspose.Pdf.lic");` di awal `Main` untuk menghindari watermark evaluasi.
- **Pemrosesan paralel**: Untuk operasi batch pada banyak file, bungkus logika per‑file dalam loop `Parallel.ForEach`—hanya perhatikan batas I/O.
- **Logging**: Use `Ser

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang terkait erat yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode kerja lengkap dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Cara Menambahkan Cap Nomor Halaman di PDF Menggunakan Aspose.PDF untuk .NET | Watermarks & Backgrounds](/pdf/english/net/watermarks-backgrounds/add-page-number-stamp-using-aspose-pdf-dotnet/)
- [Cara Menambahkan dan Menyesuaikan Nomor Halaman di PDF Menggunakan Aspose.PDF untuk .NET | Panduan Manipulasi Dokumen](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [Cara Menambahkan Cap Teks ke PDF Menggunakan Aspose.PDF .NET: Panduan Komprehensif](/pdf/english/net/watermarks-backgrounds/add-text-stamp-pdf-aspose-pdf-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}