---
category: general
date: 2026-08-14
description: Cara mengatur opsi penomoran Bates di C# menggunakan GroupDocs. Ikuti
  tutorial langkah demi langkah ini untuk menambahkan awalan khusus dan nomor mulai
  saat mengonversi Word ke PDF.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to set bates numbering options
- Bates numbering C#
- GroupDocs API
- document conversion C#
- AddBatesNumbering method
- C# PDF generation
language: id
lastmod: 2026-08-14
og_description: Cara mengatur opsi penomoran Bates di C# dengan cepat. Panduan ini
  menunjukkan cara menambahkan awalan khusus dan nomor mulai saat mengonversi Word
  ke PDF.
og_image_alt: Screenshot of C# code applying Bates numbering to a PDF
og_title: Cara mengatur opsi penomoran Bates di C# – tutorial langkah demi langkah
schemas:
- author: GroupDocs
  dateModified: '2026-08-14'
  description: How to set bates numbering options in C# using GroupDocs. Follow this
    step‑by‑step tutorial to add custom prefixes and start numbers when converting
    Word to PDF.
  headline: How to set bates numbering options in C# – complete guide
  type: TechArticle
- description: How to set bates numbering options in C# using GroupDocs. Follow this
    step‑by‑step tutorial to add custom prefixes and start numbers when converting
    Word to PDF.
  name: How to set bates numbering options in C# – complete guide
  steps:
  - name: '`Document` – loads the source file.'
    text: '`Document` – loads the source file.'
  - name: '`BatesNumberingOptions` – holds the start number, prefix, and other formatting
      details.'
    text: '`BatesNumberingOptions` – holds the start number, prefix, and other formatting
      details.'
  - name: '`AddBatesNumbering` – the method that injects the numbering into each page.'
    text: '`AddBatesNumbering` – the method that injects the numbering into each page.'
  type: HowTo
tags:
- Bates numbering
- C#
- .NET
- GroupDocs
- PDF conversion
title: Cara mengatur opsi penomoran Bates di C# – panduan lengkap
url: /id/net/programming-with-stamps-and-watermarks/how-to-set-bates-numbering-options-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara mengatur opsi penomoran Bates di C# – panduan lengkap

Jika Anda membutuhkan **cara mengatur opsi penomoran bates** di C#, panduan ini akan memandu Anda melalui langkah‑langkah yang tepat. Anda akan belajar cara mengonfigurasi nomor mulai, menambahkan awalan, dan menerapkan penomoran saat mengonversi dokumen Word ke PDF menggunakan GroupDocs API.

Pemrosesan dokumen sering memerlukan pengidentifikasi unik pada setiap halaman untuk keperluan hukum atau arsip. Pada akhir tutorial ini Anda akan memiliki potongan kode yang dapat digunakan kembali dan dapat dimasukkan ke dalam proyek .NET apa pun, baik Anda sedang membangun alat dukungan litigasi atau generator laporan otomatis. Tidak diperlukan alat eksternal—hanya pustaka GroupDocs.Conversion dan beberapa baris kode C#.

## Apa yang Anda perlukan

* .NET 6.0 SDK atau yang lebih baru terpasang  
* Visual Studio 2022 (atau IDE apa pun yang mendukung .NET)  
* Lisensi GroupDocs.Conversion yang valid (versi percobaan gratis dapat digunakan untuk pengujian)  
* Dokumen Word contoh (`input.docx`) yang ingin Anda beri nomor  

Prasyarat ini memastikan kode berjalan tanpa konfigurasi tambahan.

## Cara mengatur opsi penomoran bates – ikhtisar

Inti dari **cara mengatur opsi penomoran bates** terletak pada tiga objek:

1. `Document` – memuat file sumber.  
2. `BatesNumberingOptions` – menyimpan nomor mulai, awalan, dan detail pemformatan lainnya.  
3. `AddBatesNumbering` – metode yang menyisipkan penomoran ke setiap halaman.  

Memahami mengapa setiap komponen ada membantu Anda menyesuaikan solusi untuk skenario yang lebih kompleks, seperti font khusus atau penomoran multi‑bahasa.

## Langkah 1: Instal paket NuGet GroupDocs.Conversion

Buka terminal di folder solusi Anda dan jalankan:

```bash
dotnet add package GroupDocs.Conversion
```

**GroupDocs API** menyediakan kelas `Document` dan metode ekstensi `AddBatesNumbering` yang digunakan nanti dalam tutorial.

## Langkah 2: Muat dokumen sumber

```csharp
using GroupDocs.Conversion;
using GroupDocs.Conversion.Options.Convert;

// Step 2: Load the source Word document
Document document = new Document(@"C:\Docs\input.docx");
```

*Mengapa langkah ini?*  
Memuat file membuat representasi dalam memori yang dapat dimanipulasi oleh mesin konversi. Tanpa instance `Document` Anda tidak dapat menerapkan penomoran Bates atau transformasi lainnya.

## Langkah 3: Buat opsi penomoran Bates

```csharp
// Step 3: Configure Bates numbering
BatesNumberingOptions batesOptions = new BatesNumberingOptions
{
    // The first page will be numbered 1000
    StartNumber = 1000,
    // Each page will be prefixed with "CASE-"
    Prefix = "CASE-",
    // Optional: set the number format (e.g., 4 digits)
    NumberFormat = "#0000",
    // Optional: choose where the number appears (header/footer)
    Position = BatesNumberingPosition.FooterRight
};
```

*Mengapa langkah ini?*  
`BatesNumberingOptions` mengenkapsulasi semua pengaturan yang mungkin Anda perlukan saat **mengatur opsi penomoran bates**. Menyesuaikan `StartNumber` dan `Prefix` memungkinkan Anda menyelaraskan output dengan sistem manajemen kasus Anda. Properti `Position` mengontrol penempatan visual, yang sering menjadi persyaratan kepatuhan.

## Langkah 4: Terapkan penomoran Bates ke dokumen

```csharp
// Step 4: Apply the numbering to every page
document.AddBatesNumbering(batesOptions);
```

Metode `AddBatesNumbering` melintasi setiap halaman dari `Document` yang dimuat dan menyisipkan string yang telah dikonfigurasi. Karena metode ini bekerja pada representasi dalam memori, Anda dapat menambahkan langkah pemrosesan tambahan (misalnya, watermark) sebelum menyimpan.

## Langkah 5: Konversi dan simpan hasil sebagai PDF

```csharp
// Step 5: Define PDF conversion options (optional)
PdfConvertOptions pdfOptions = new PdfConvertOptions
{
    // Preserve original layout
    EmbedStandardFonts = true
};

// Save the numbered document as PDF
document.Save(@"C:\Docs\output.pdf", pdfOptions);
```

*Mengapa langkah ini?*  
Menyimpan sebagai PDF adalah format akhir yang umum untuk dokumen hukum. Objek `PdfConvertOptions` memungkinkan Anda menyesuaikan output secara detail, tetapi tidak diperlukan untuk penomoran dasar. Pemanggilan `Save` menulis PDF yang telah diberi nomor sepenuhnya ke disk.

## Contoh lengkap yang dapat dijalankan

Menggabungkan semua, berikut adalah aplikasi konsol mandiri yang dapat Anda kompilasi dan jalankan:

```csharp
using System;
using GroupDocs.Conversion;
using GroupDocs.Conversion.Options.Convert;
using GroupDocs.Conversion.Options.Convert.Pdf;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Load the source Word document
            Document document = new Document(@"C:\Docs\input.docx");

            // Configure Bates numbering options
            BatesNumberingOptions batesOptions = new BatesNumberingOptions
            {
                StartNumber = 1000,
                Prefix = "CASE-",
                NumberFormat = "#0000",
                Position = BatesNumberingPosition.FooterRight
            };

            // Apply numbering to each page
            document.AddBatesNumbering(batesOptions);

            // Optional: set PDF conversion preferences
            PdfConvertOptions pdfOptions = new PdfConvertOptions
            {
                EmbedStandardFonts = true
            };

            // Save the numbered PDF
            document.Save(@"C:\Docs\output.pdf", pdfOptions);

            Console.WriteLine("Bates numbering applied successfully. Output saved to output.pdf");
        }
    }
}
```

**Output yang diharapkan**

Menjalankan program akan membuat `output.pdf` di mana setiap halaman menampilkan label seperti `CASE-1000`, `CASE-1001`, dll., yang ditempatkan di footer kanan. Buka PDF tersebut dengan penampil apa pun untuk memverifikasi bahwa nomor muncul sesuai yang diharapkan.

## Kesalahan umum dan praktik terbaik

| Masalah | Mengapa terjadi | Cara menghindarinya |
|---------|----------------|---------------------|
| **Path relatif menyebabkan `FileNotFoundException`** | Direktori kerja aplikasi konsol dapat berbeda dari Visual Studio. | Gunakan path absolut atau `Path.Combine(AppContext.BaseDirectory, "input.docx")`. |
| **Penomoran menutupi footer yang ada** | Jika dokumen sumber sudah memiliki konten di area footer yang dipilih, nomor baru dapat tersembunyi. | Pilih `Position` yang berbeda (misalnya, `HeaderLeft`) atau sesuaikan templat sumber. |
| **Dokumen besar menjadi lambat** | Penomoran Bates mengiterasi setiap halaman; penggunaan memori meningkat seiring ukuran file. | Proses dokumen dalam potongan menggunakan `Document.Split` jika melebihi 500 halaman. |
| **Kedaluwarsa lisensi** | Versi percobaan gratis GroupDocs berakhir setelah 30 hari, menyebabkan pengecualian pada `AddBatesNumbering`. | Terapkan kunci lisensi yang valid sebelum memuat dokumen: `License license = new License(); license.SetLicense("license.lic");`. |

**Tips profesional:** Jika Anda membutuhkan format nomor yang berbeda per kasus (mis., `2023-CASE-001`), bangun awalan secara dinamis sebelum membuat `BatesNumberingOptions`.

## Memperluas solusi

Pendekatan **Bates numbering C#** yang sama bekerja dengan format sumber lain seperti `.txt`, `.html`, atau bahkan gambar. Cukup ubah ekstensi file saat membuat objek `Document`, dan mesin konversi akan menangani sisanya.

Anda juga dapat menggabungkan **document conversion C#** dengan OCR untuk PDF yang dipindai:

```csharp
// Example: add OCR before numbering (requires GroupDocs.Viewer)
using GroupDocs.Viewer;
using GroupDocs.Viewer.Options;

Document scannedPdf = new Document(@"C:\Docs\scanned.pdf");
var viewer = new Viewer(scannedPdf);
var viewOptions = new HtmlViewOptions();
viewer.View(viewOptions); // OCR step
// Then apply Bates numbering as shown earlier
```

## Kesimpulan

Anda kini tahu **cara mengatur opsi penomoran bates** di C# dari awal hingga akhir. Dengan membuat objek `BatesNumberingOptions`, menerapkannya dengan `AddBatesNumbering`, dan menyimpan hasilnya sebagai PDF, Anda dapat mengotomatisasi produksi dokumen yang secara hukum mematuhi regulasi dan memiliki identifikasi unik.

Dari sini Anda dapat menjelajahi topik terkait seperti **C# PDF generation**, **document conversion C#**, atau fitur lanjutan **GroupDocs API** seperti watermarking dan tanda tangan digital. Bereksperimenlah dengan awalan, posisi, dan format nomor yang berbeda untuk menyesuaikan alur kerja Anda.

Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan menjelajahi pendekatan implementasi alternatif dalam proyek Anda.

- [Tambahkan Penomoran Bates PDF di C# – Panduan Lengkap](/pdf/english/net/programming-with-stamps-and-watermarks/add-bates-numbering-pdf-in-c-complete-guide/)
- [Cara Menambahkan dan Menyesuaikan Nomor Halaman di PDF Menggunakan Aspose.PDF untuk .NET | Panduan Manipulasi Dokumen](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [Cara Menambahkan Footer Stempel Teks di PDF Menggunakan Aspose.PDF untuk .NET&#58; Panduan Langkah‑per‑Langkah](/pdf/english/net/document-manipulation/add-text-stamp-footer-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}