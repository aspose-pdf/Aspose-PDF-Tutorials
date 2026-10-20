---
category: general
date: 2026-08-04
description: Buat dokumen PDF baru di C# dan tambahkan penomoran Bates pada PDF dengan
  cepat menggunakan Aspose.Pdf – pelajari cara menambahkan halaman kosong PDF dan
  nomor halaman kustom.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create new pdf document
- add bates numbering pdf
- how to add bates
- add blank page pdf
- add custom page numbers
language: id
lastmod: 2026-08-04
og_description: Buat dokumen PDF baru dengan C# dan secara otomatis tambahkan penomoran
  Bates pada PDF untuk manajemen kasus hukum – contoh kode lengkap disertakan.
og_image_alt: Screenshot of a C# program creating a PDF document with Bates numbers
  applied
og_title: Buat dokumen PDF baru dengan penomoran Bates di C#
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Create new PDF document in C# and add Bates numbering pdf quickly using
    Aspose.Pdf – learn to add blank page pdf and custom page numbers.
  headline: Create new PDF document with Bates numbering in C#
  type: TechArticle
tags:
- C#
- PDF
- Aspose.Pdf
- Bates numbering
title: Buat dokumen PDF baru dengan penomoran Bates di C#
url: /id/net/document-creation/create-new-pdf-document-with-bates-numbering-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat dokumen PDF baru dengan penomoran Bates di C#

Jika Anda perlu **membuat dokumen PDF baru** di C#, panduan ini menunjukkan cara **menambahkan penomoran Bates pdf** menggunakan Aspose.Pdf. Anda akan belajar cara **menambahkan halaman kosong pdf**, mengonfigurasi **menambahkan nomor halaman khusus**, dan menyimpan file akhir.

Tutorial ini mencakup setiap langkah mulai dari menginstal perpustakaan hingga menghasilkan PDF yang memenuhi standar berkas kasus hukum. Pada akhir tutorial Anda dapat menghasilkan PDF, menyisipkan halaman kosong, menerapkan nomor Bates, dan menyesuaikan format penomoran—semua dengan satu program yang dapat dijalankan.

## Prasyarat

Sebelum memulai, pastikan Anda memiliki:

* .NET 6.0 SDK atau yang lebih baru terpasang  
* Visual Studio 2022 (atau IDE C# apa pun)  
* Lisensi aktif Aspose.Pdf untuk .NET atau kunci evaluasi gratis  

Anda tidak memerlukan paket NuGet tambahan; tutorial ini menginstal semuanya secara otomatis.

## Langkah 1: Instal Aspose.Pdf via NuGet

Buka terminal di folder proyek Anda dan jalankan:

```bash
dotnet add package Aspose.Pdf
```

Perintah ini menambahkan versi stabil terbaru Aspose.Pdf ke proyek Anda, yang menyediakan kelas `Document`, `BatesNumbering`, dan kelas manipulasi PDF lainnya yang akan Anda gunakan.

## Langkah 2: Buat dokumen PDF baru – penyiapan awal

Membuat file PDF adalah fondasi untuk semua operasi selanjutnya. Kelas `Document` mewakili seluruh kontainer PDF.

```csharp
using Aspose.Pdf;

// Step 2: Create a new PDF document
using var doc = new Document();
```

*Mengapa ini penting*: Menginstansiasi `Document` mengalokasikan struktur internal yang diperlukan untuk halaman, font, dan grafik. Menggunakan `using var` memastikan file dibuang dengan benar setelah disimpan.

## Langkah 3: Tambahkan halaman kosong pdf

Sebuah PDF harus memiliki setidaknya satu halaman sebelum Anda dapat menempatkan konten di dalamnya. Menambahkan halaman kosong memberi Anda kanvas bersih untuk nomor Bates.

```csharp
// Step 3: Add a blank page to the document
Page page = doc.Pages.Add();
```

Metode `Pages.Add()` menambahkan halaman baru yang kosong di akhir koleksi halaman dokumen. Anda dapat mengulangi pemanggilan ini untuk menambah lebih banyak halaman jika nanti Anda perlu **menambahkan nomor halaman khusus** pada beberapa halaman.

## Langkah 4: Konfigurasikan penomoran Bates – cara menambahkan bates

Penomoran Bates adalah pengenal berurutan yang umum digunakan dalam dokumen hukum. Anda mengonfigurasikannya melalui kelas `BatesNumbering`.

```csharp
// Step 4: Set up Bates numbering options
var bates = new BatesNumbering
{
    StartNumber = 1000,      // Starting number for the sequence
    Prefix = "CaseA-",       // Text to prepend to each number
    Increment = 1,           // Increment between consecutive numbers
    // Optional: Set the location, font size, etc.
};
```

*Mengapa ini penting*: `StartNumber` menentukan nomor pertama, `Prefix` menambahkan label yang dapat dibaca, dan `Increment` mengontrol ukuran langkah. Anda juga dapat menyesuaikan `HorizontalAlignment`, `VerticalAlignment`, `FontSize`, dan `Margins` untuk mengontrol tampilan nomor pada setiap halaman.

## Langkah 5: Terapkan penomoran Bates pdf ke halaman

Setelah opsi penomoran siap, terapkan ke halaman (atau ke seluruh dokumen).

```csharp
// Step 5: Apply the Bates numbering to the page
bates.Apply(page);
```

Pemanggilan `Apply` menyisipkan nomor yang diformat ke footer halaman secara default. Jika Anda memerlukan nomor di tempat lain, atur `bates.Position` sebelum memanggil `Apply`.

## Langkah 6: Simpan PDF dengan nomor Bates yang diterapkan

Akhirnya, tulis dokumen dalam memori ke disk.

```csharp
// Step 6: Save the PDF with Bates numbers applied
string outputPath = Path.Combine(
    Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
    "BatesNumbered.pdf");

doc.Save(outputPath);
Console.WriteLine($"PDF saved to {outputPath}");
```

File yang disimpan kini berisi satu halaman dengan nomor Bates **CaseA-1000** ditampilkan di bagian bawah. Buka PDF di penampil apa pun untuk memverifikasi penomoran.

## Output yang diharapkan

Saat Anda membuka `BatesNumbered.pdf`, Anda akan melihat:

* Satu halaman kosong (atau lebih jika Anda menambahkan halaman tambahan)  
* Teks **CaseA-1000** berada di bagian bawah halaman (lokasi default)  

Jika Anda menambahkan lebih banyak halaman dan menggunakan kembali instance `BatesNumbering` yang sama, nomor akan bertambah secara otomatis (CaseA-1001, CaseA-1002, …).

## Tip pro: Menambahkan nomor halaman khusus selain nomor Bates

Kadang-kadang Anda memerlukan nomor Bates dan nomor halaman tradisional sekaligus. Anda dapat menggabungkannya dengan menambahkan `TextFragment` setelah menerapkan penomoran Bates:

```csharp
// Add a traditional page number in the header
var pageNumber = new TextFragment($"Page {page.Number}")
{
    HorizontalAlignment = HorizontalAlignment.Center,
    VerticalAlignment = VerticalAlignment.Top,
    FontSize = 12,
    Font = FontRepository.FindFont("Arial")
};
page.Paragraphs.Add(pageNumber);
```

Cuplikan ini menunjukkan **menambahkan nomor halaman khusus** sambil mempertahankan label Bates.

## Kasus tepi: Menerapkan penomoran Bates ke beberapa halaman

Jika dokumen Anda berisi beberapa halaman, Anda dapat menerapkan instance `BatesNumbering` yang sama ke setiap halaman dalam loop:

```csharp
for (int i = 1; i <= doc.Pages.Count; i++)
{
    bates.Apply(doc.Pages[i]);
}
```

Loop ini memastikan setiap halaman menerima nomor berurutan berdasarkan `StartNumber` dan `Increment` yang Anda definisikan.

## Kesalahan umum dan cara menghindarinya

| Masalah | Mengapa terjadi | Solusi |
|-------|----------------|-----|
| Nomor muncul tidak terpusat | Penyelarasan default mungkin tidak cocok dengan tata letak Anda | Atur `bates.HorizontalAlignment` dan `bates.VerticalAlignment` secara eksplisit |
| Nomor menimpa konten yang ada | Tidak ada margin yang didefinisikan | Sesuaikan `bates.Margin` atau gunakan `bates.Position` untuk memindahkan nomor |
| Pengecualian lisensi saat runtime | Versi evaluasi membatasi output | Terapkan lisensi Aspose.Pdf yang valid sebelum membuat dokumen (`License license = new License(); license.SetLicense("Aspose.Pdf.lic");`) |

## Contoh kerja lengkap

Berikut adalah program mandiri yang dapat Anda salin, tempel, dan jalankan.

```csharp
using System;
using System.IO;
using Aspose.Pdf;

class Program
{
    static void Main()
    {
        // 1. Create a new PDF document
        using var doc = new Document();

        // 2. Add a blank page pdf
        Page page = doc.Pages.Add();

        // 3. Configure Bates numbering – how to add bates
        var bates = new BatesNumbering
        {
            StartNumber = 1000,
            Prefix = "CaseA-",
            Increment = 1,
            HorizontalAlignment = HorizontalAlignment.Right,
            VerticalAlignment = VerticalAlignment.Bottom,
            Margin = new MarginInfo(20, 20, 20, 20),
            FontSize =


## Apa yang Harus Anda Pelajari Selanjutnya?


Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [How to Add and Customize Page Numbers in PDFs Using Aspose.PDF for .NET | Document Manipulation Guide](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [Aspose.PDF .NET&#58; Add Page Numbers to PDFs Using FloatingBox](/pdf/english/net/text-operations/aspose-pdf-net-floatingbox-page-numbering/)
- [Create PDF Document with Aspose.PDF – Add Page, Shape & Save](/pdf/english/net/document-creation/create-pdf-document-with-aspose-pdf-add-page-shape-save/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}