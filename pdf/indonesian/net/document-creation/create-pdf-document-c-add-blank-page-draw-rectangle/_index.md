---
category: general
date: 2026-02-12
description: Buat dokumen PDF C# dengan cepat dengan menambahkan halaman kosong, memeriksa
  ukuran halaman, menggambar persegi panjang, dan menyimpan file. Panduan langkah
  demi langkah dengan Aspose.Pdf.
draft: false
keywords:
- create pdf document c#
- add blank page pdf
- draw rectangle pdf
- save pdf file c#
- check pdf page size
language: id
og_description: Buat dokumen PDF C# dengan cepat dengan menambahkan halaman kosong,
  memeriksa ukuran halaman, menggambar persegi panjang, dan menyimpan file. Tutorial
  lengkap dengan kode.
og_title: Buat Dokumen PDF C# – Tambahkan Halaman Kosong & Gambar Persegi Panjang
tags:
- PDF
- C#
- Aspose.Pdf
- Document Generation
title: Buat Dokumen PDF C# – Tambahkan Halaman Kosong & Gambar Persegi Panjang
url: /id/net/document-creation/create-pdf-document-c-add-blank-page-draw-rectangle/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat Dokumen PDF C# – Tambahkan Halaman Kosong & Gambar Persegi Panjang

Pernah perlu **create PDF document C#** dari awal dan bertanya-tanya bagaimana menambahkan halaman kosong, memverifikasi dimensi halaman, menggambar sebuah bentuk, dan akhirnya menyimpannya? Anda tidak sendirian. Banyak pengembang mengalami kendala yang sama saat mengotomatiskan laporan, faktur, atau output yang dapat dicetak apa pun.

Dalam tutorial ini kami akan membahas contoh lengkap yang dapat dijalankan yang menunjukkan secara tepat cara **add blank page PDF**, **check PDF page size**, **draw rectangle PDF**, dan **save PDF file C#** menggunakan library Aspose.Pdf. Pada akhir tutorial Anda akan memiliki file PDF siap pakai dengan persegi panjang berbingkai biru yang terletak rapi pada halaman berukuran A4.

## Prasyarat

- **.NET 6.0** atau yang lebih baru (kode ini juga bekerja pada .NET Framework 4.6+).  
- **Aspose.Pdf for .NET** terpasang melalui NuGet (`Install-Package Aspose.Pdf`).  
- Pemahaman dasar tentang sintaks C#—tidak memerlukan hal yang rumit.  
- IDE pilihan Anda (Visual Studio, Rider, VS Code, dll.).

> **Pro tip:** Jika Anda menggunakan Visual Studio, UI NuGet Package Manager memudahkan penambahan Aspose.Pdf—cukup cari “Aspose.Pdf” dan klik Install.

## Langkah 1: Create PDF Document C# – Inisialisasi Dokumen

Hal pertama yang Anda butuhkan adalah objek `Document` baru. Anggaplah itu sebagai kanvas kosong di mana setiap operasi selanjutnya akan melukis kontennya.

```csharp
using Aspose.Pdf;
using System;

// Step 1: Create a new PDF document
var pdfDocument = new Document();
```

> **Mengapa ini penting:** Kelas `Document` adalah titik masuk untuk setiap operasi PDF. Menginstansiasinya mengalokasikan struktur internal yang diperlukan untuk mengelola halaman, sumber daya, dan metadata.

## Langkah 2: Add Blank Page PDF – Tambahkan Halaman Baru

PDF tanpa halaman ibarat buku tanpa halaman—tidak berguna. Menambahkan halaman kosong memberi kita sesuatu untuk digambar.

```csharp
// Step 2: Add a blank page to the document
Page page = pdfDocument.Pages.Add();
```

> **Apa yang terjadi di balik layar?** `Pages.Add()` membuat sebuah halaman yang mewarisi ukuran default (A4 untuk kebanyakan pengaturan). Anda dapat mengubah dimensinya nanti jika memerlukan ukuran khusus.

## Langkah 3: Definisikan Persegi Panjang dan Periksa Ukuran Halaman PDF

Sebelum menggambar, kita harus menentukan di mana persegi panjang akan ditempatkan dan memastikan bahwa ia muat di dalam halaman. Di sinilah kata kunci **check PDF page size** berperan.

```csharp
// Step 3: Define rectangle position and size (fits within a standard A4 page)
var rectangle = new Rectangle(50, 50, 550, 750);

// Step 3b: Verify that the rectangle fits inside the page boundaries
bool fitsWidth = page.PageInfo.Width >= rectangle.Width;
bool fitsHeight = page.PageInfo.Height >= rectangle.Height;

if (!fitsWidth || !fitsHeight)
{
    throw new InvalidOperationException(
        $"Rectangle (W:{rectangle.Width}, H:{rectangle.Height}) exceeds page size (W:{page.PageInfo.Width}, H:{page.PageInfo.Height}).");
}
```

> **Mengapa kami memeriksa:** Beberapa PDF mungkin menggunakan ukuran halaman khusus (Letter, Legal, dll.). Jika persegi panjang lebih besar dari halaman, operasi menggambar akan terpotong atau menghasilkan error. Pemeriksaan ini membuat kode lebih tahan terhadap perubahan ukuran halaman di masa depan.

## Langkah 4: Draw Rectangle PDF – Render Bentuk

Sekarang bagian yang menyenangkan: benar‑benarnya menggambar persegi panjang dengan bingkai biru dan isi transparan. Ini menunjukkan kemampuan **draw rectangle PDF**.

```csharp
// Step 4: Draw the rectangle with a blue border and a transparent fill
page.AddRectangle(
    rectangle,
    Color.Blue,          // Border color
    Color.Transparent    // Fill color (transparent)
);
```

> **Cara kerjanya:** `AddRectangle` menerima tiga argumen—geometri persegi panjang, warna garis (bingkai), dan warna isi. Menggunakan `Color.Transparent` memastikan bagian dalam tetap kosong, sehingga konten di bawahnya tetap terlihat.

## Langkah 5: Save PDF File C# – Simpan Dokumen ke Disk

Akhirnya, kita menulis dokumen ke sebuah file. Ini adalah langkah **save pdf file c#** yang menyelesaikan proses.

```csharp
// Step 5: Save the PDF to a file
string outputPath = @"C:\Temp\shape.pdf"; // Adjust the path as needed
pdfDocument.Save(outputPath);
Console.WriteLine($"PDF saved successfully to {outputPath}");
```

> **Tip:** Bungkus seluruh proses dalam blok `using` (atau panggil `pdfDocument.Dispose()`) untuk segera membebaskan sumber daya native, terutama saat menghasilkan banyak PDF dalam sebuah loop.

## Contoh Lengkap yang Dapat Dijalankan

Menggabungkan semua bagian, berikut program lengkap yang dapat Anda salin‑tempel ke aplikasi console:

```csharp
using Aspose.Pdf;
using System;

class Program
{
    static void Main()
    {
        // Create a new PDF document
        using (var pdfDocument = new Document())
        {
            // Add a blank page
            Page page = pdfDocument.Pages.Add();

            // Define rectangle (fits within a standard A4 page)
            var rectangle = new Rectangle(50, 50, 550, 750);

            // Ensure the rectangle fits inside the page boundaries
            if (page.PageInfo.Width >= rectangle.Width && page.PageInfo.Height >= rectangle.Height)
            {
                // Draw the rectangle with a blue border and a transparent fill
                page.AddRectangle(rectangle, Color.Blue, Color.Transparent);
            }
            else
            {
                Console.WriteLine("Rectangle does not fit on the page. Adjust dimensions.");
                return;
            }

            // Save the PDF to a file
            string outputPath = @"C:\Temp\shape.pdf"; // Change to your desired folder
            pdfDocument.Save(outputPath);
            Console.WriteLine($"PDF created at: {outputPath}");
        }
    }
}
```

### Hasil yang Diharapkan

Buka `shape.pdf` dan Anda akan melihat satu halaman berukuran A4 dengan persegi panjang berbingkai biru yang ditempatkan 50 pts dari tepi kiri dan bawah. Bagian dalam persegi panjang transparan, sehingga latar belakang halaman tetap terlihat.

![contoh create pdf document c# menampilkan persegi panjang](https://example.com/placeholder.png "contoh create pdf document c#")

*(Teks alt gambar: **create pdf document c# example showing rectangle**)  

Jika Anda mengubah `Color.Blue` menjadi `Color.Red` atau menyesuaikan koordinat, persegi panjang akan mencerminkan perubahan tersebut—silakan bereksperimen.

## Pertanyaan Umum & Kasus Tepi

### Bagaimana jika saya membutuhkan ukuran halaman yang berbeda?

Anda dapat mengatur dimensi halaman sebelum menambahkan konten:

```csharp
Page customPage = pdfDocument.Pages.Add();
customPage.SetPageSize(PageSize.Letter.Width, PageSize.Letter.Height);
```

Ingat untuk menjalankan kembali logika **check PDF page size** setelah mengubah dimensi.

### Bisakah saya menggambar bentuk lain?

Tentu saja. Aspose.Pdf menyediakan objek `AddCircle`, `AddEllipse`, `AddLine`, dan bahkan `Path` bentuk bebas. Pola yang sama—definisikan geometri, verifikasi batas, lalu panggil metode `Add*` yang sesuai—dapat diterapkan.

### Bagaimana cara mengisi persegi panjang dengan warna?

Ganti `Color.Transparent` dengan warna solid apa pun:

```csharp
page.AddRectangle(rectangle, Color.Blue, Color.LightGray);
```

### Apakah ada cara menambahkan teks di dalam persegi panjang?

Tentu saja. Setelah menggambar persegi panjang, tambahkan `TextFragment` yang diposisikan dalam koordinat persegi panjang:

```csharp
var tf = new TextFragment("Hello, world!");
tf.Rect = new Rectangle(60, 60, 540, 730); // Slightly inset
page.Paragraphs.Add(tf);
```

## Kesimpulan

Kami baru saja menunjukkan cara **create PDF document C#**, **add blank page PDF**, **check PDF page size**, **draw rectangle PDF**, dan akhirnya **save PDF file C#**—semua dalam contoh singkat yang menyeluruh. Kode siap dijalankan, penjelasan mencakup *mengapa* di balik setiap langkah, dan Anda kini memiliki fondasi kuat untuk tugas pembuatan PDF yang lebih canggih.

Siap untuk tantangan berikutnya? Cobalah menumpuk beberapa bentuk, menyisipkan gambar, atau menghasilkan tabel—semua mengikuti pola yang sama seperti yang kami gunakan di sini. Dan jika Anda perlu menyesuaikan dimensi halaman atau beralih ke library PDF lain, konsepnya tetap sama.

Selamat coding, semoga PDF Anda selalu ter‑render persis seperti yang Anda inginkan!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}