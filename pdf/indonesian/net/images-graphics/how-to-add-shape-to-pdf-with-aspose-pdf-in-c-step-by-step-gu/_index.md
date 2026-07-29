---
category: general
date: 2026-06-18
description: Cara menambahkan bentuk ke PDF menggunakan Aspose.PDF di C# – memuat
  PDF, menggambar persegi panjang, dan menyimpannya.
draft: false
keywords:
- how to add shape to pdf
- load pdf document in c#
- how to draw shapes in pdf
- aspose pdf add rectangle
language: id
og_description: Cara menambahkan bentuk ke PDF dengan Aspose.PDF di C#. Pelajari cara
  memuat dokumen PDF, menggambar persegi panjang, dan menyimpan file yang diperbarui.
og_title: Cara Menambahkan Bentuk ke PDF dengan Aspose.PDF di C#
schemas:
- author: Aspose
  dateModified: '2026-06-18'
  description: How to add shape to PDF using Aspose.PDF in C# – load a PDF, draw a
    rectangle, and save it.
  headline: How to Add Shape to PDF with Aspose.PDF in C# – Step‑by‑Step Guide
  type: TechArticle
- description: How to add shape to PDF using Aspose.PDF in C# – load a PDF, draw a
    rectangle, and save it.
  name: How to Add Shape to PDF with Aspose.PDF in C# – Step‑by‑Step Guide
  steps:
  - name: What if I need to draw on multiple pages?
    text: Simply loop over `pdfDoc.Pages` and call `AddRectangle` (or any other shape)
      for each page. Remember to adjust coordinates if pages have different sizes.
  - name: Can I fill the rectangle with a color?
    text: Absolutely. Change `FillColor` from `Transparent` to any `Color` you like,
      e.g., `Color.Yellow`. The shape will appear as a solid block.
  - name: Does this work with password‑protected PDFs?
    text: 'Aspose.PDF can open encrypted files if you supply the password:'
  - name: How to add a rectangle with rounded corners?
    text: Use the `RoundedRectangle` class instead of `Rectangle`. The rest of the
      steps stay identical.
  type: HowTo
tags:
- Aspose.PDF
- C#
- PDF manipulation
title: Cara Menambahkan Bentuk ke PDF dengan Aspose.PDF di C# – Panduan Langkah demi
  Langkah
url: /id/net/images-graphics/how-to-add-shape-to-pdf-with-aspose-pdf-in-c-step-by-step-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Menambahkan Bentuk ke PDF dengan Aspose.PDF di C# – Tutorial Lengkap

Pernah bertanya-tanya **cara menambahkan bentuk ke PDF** tanpa harus berurusan dengan aliran byte tingkat rendah? Dalam banyak aplikasi dunia nyata Anda perlu menyorot sebuah wilayah, menggarisbawahi sebuah klausul, atau sekadar menggambar kotak pembatas untuk bidang tanda tangan. Kabar baiknya, Aspose.PDF membuat hal ini sangat mudah. Dalam panduan ini kita akan memuat dokumen PDF di C#, menggambar sebuah persegi panjang, dan menyimpan hasilnya—tidak lebih, tidak kurang.

Kami akan menelusuri setiap baris kode, menjelaskan *mengapa* setiap bagian penting, dan bahkan menunjukkan cara cepat untuk memverifikasi bahwa bentuk benar‑benar berada di tempat yang Anda harapkan. Pada akhir tutorial Anda akan merasa nyaman dengan **cara menggambar bentuk di file PDF**, dan Anda akan memiliki potongan kode yang dapat digunakan kembali di proyek .NET mana pun.

## Prasyarat

Sebelum kita mulai, pastikan Anda memiliki:

- **.NET 6.0** (atau versi .NET terbaru) terpasang di mesin Anda.  
- **Lisensi Aspose.PDF untuk .NET** yang valid (atau kunci evaluasi gratis).  
- Visual Studio 2022, Rider, atau editor lain yang Anda sukai.  
- File PDF yang sudah ada (`input.pdf`) ditempatkan di folder yang dapat Anda referensikan.

> **Tip profesional:** Jika Anda hanya melakukan pengujian, versi evaluasi gratis sudah cukup—ia menambahkan watermark kecil tetapi berfungsi seperti produk penuh.

## Langkah 1: Siapkan Proyek dan Impor Namespace

Pertama, buat proyek konsol baru (atau tambahkan ke proyek yang sudah ada) dan masukkan namespace yang diperlukan ke dalam ruang lingkup.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;   // Required for shape classes
```

Mengapa ini penting: `Aspose.Pdf` memberikan model dokumen inti, sementara `Aspose.Pdf.Drawing` berisi kelas bentuk `Rectangle` yang akan kita gunakan nanti. Tanpa yang terakhir, kompiler akan mengeluh bahwa `Rectangle` tidak didefinisikan.

## Langkah 2: Muat Dokumen PDF di C#

Sekarang kita benar‑benar **memuat dokumen pdf di c#**. Ini adalah operasi pertama yang selalu Anda lakukan ketika ingin memodifikasi file yang sudah ada.

```csharp
// Step 2: Load the PDF document
string inputPath = @"YOUR_DIRECTORY\input.pdf";
Document pdfDoc = new Document(inputPath);
Console.WriteLine($"Loaded PDF with {pdfDoc.Pages.Count} page(s).");
```

*Penjelasan*:  
- `Document` adalah representasi Aspose untuk seluruh file.  
- Menyertakan jalur lengkap ke konstruktor membaca file ke memori.  
- Baris `Console.WriteLine` bersifat opsional tetapi berguna untuk debugging—jika jumlah halaman nol, Anda tahu ada yang salah sejak awal.

## Langkah 3: Definisikan Bentuk Persegi Panjang

Inilah inti dari **cara menambahkan bentuk ke PDF**. Kita membuat objek `Rectangle` yang menentukan posisi dan ukuran menggunakan sistem koordinat di mana (0,0) berada di sudut kiri‑bawah halaman.

```csharp
// Step 3: Define a rectangle (left, bottom, right, top)
Rectangle rect = new Rectangle(0, 0, 200, 100)
{
    // Optional styling – you can tweak these as needed
    FillColor = Color.Transparent,          // No fill, just the border
    Border = new Border(BorderStyle.Solid, 2, Color.Red)
};
```

Mengapa kita mengatur `FillColor` menjadi transparan: kebanyakan kasus penggunaan hanya menginginkan outline (bayangkan kotak sorotan). Properti `Border` memungkinkan Anda mengontrol ketebalan dan warna; merah membuat persegi panjang menonjol pada halaman putih standar.

## Langkah 4: Verifikasi Bentuk Masuk dalam Batas Halaman

Sebelum kita **menambahkan persegi panjang**, ada baiknya memastikan bentuk tidak melampaui tepi halaman. Aspose menyediakan `ValidateShapeBounds` khusus untuk tujuan ini.

```csharp
// Step 4: Validate that the rectangle fits on the first page
bool fits = pdfDoc.Pages[1].ValidateShapeBounds(rect);
if (!fits)
{
    Console.WriteLine("Rectangle exceeds page dimensions – adjusting...");
    // Simple fallback: shrink to fit the page width
    rect.Right = pdfDoc.Pages[1].PageInfo.Width - 10;
    rect.Top  = pdfDoc.Pages[1].PageInfo.Height - 10;
}
```

*Mengapa*: Menggambar di luar halaman dapat menyebabkan gangguan render atau bahkan melempar pengecualian. Pemeriksaan ini membuat tutorial menjadi lebih kuat untuk PDF dengan ukuran apa pun.

## Langkah 5: Tambahkan Persegi Panjang ke Halaman yang Diinginkan

Sekarang kita akhirnya **menambahkan bentuk ke pdf**. Metode `AddRectangle` menempelkan bentuk ke koleksi anotasi halaman, yang berarti penampil PDF akan merendernya seperti gambar lainnya.

```csharp
// Step 5: Add the rectangle to the first page
pdfDoc.Pages[1].AddRectangle(rect);
Console.WriteLine("Rectangle added to page 1.");
```

Jika Anda perlu menargetkan halaman lain, cukup ganti indeks `1` dengan nomor halaman yang sesuai (Aspose menggunakan indeks berbasis 1).

## Langkah 6: Simpan PDF yang Telah Dimodifikasi

Langkah terakhir adalah menuliskan perubahan kembali ke disk. Anda dapat menimpa file asli atau membuat yang baru—di sini kami akan menghasilkan `output.pdf`.

```csharp
// Step 6: Save the updated PDF
string outputPath = @"YOUR_DIRECTORY\output.pdf";
pdfDoc.Save(outputPath);
Console.WriteLine($"PDF saved as {outputPath}");
```

*Apa yang diharapkan*: Buka `output.pdf` di Adobe Reader atau penampil apa pun dan Anda akan melihat persegi panjang merah tajam yang terpasang di sudut kiri‑bawah halaman pertama.

![Diagram showing rectangle added to PDF](https://example.com/rectangle-diagram.png "how to add shape to pdf example")

*Alt text*: "how to add shape to pdf – rectangle drawn on first page of a PDF file"

## Langkah 7: Contoh Lengkap yang Siap Salin‑Tempel

Berikut adalah program lengkap yang dapat Anda kompilasi dan jalankan segera. Ingat untuk mengganti `YOUR_DIRECTORY` dengan jalur folder yang sebenarnya di mesin Anda.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using Aspose.Pdf.Color;   // For color definitions

namespace PdfShapeDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Load the PDF document in C#
            string inputPath = @"YOUR_DIRECTORY\input.pdf";
            Document pdfDoc = new Document(inputPath);
            Console.WriteLine($"Loaded PDF with {pdfDoc.Pages.Count} page(s).");

            // Define the rectangle shape
            Rectangle rect = new Rectangle(0, 0, 200, 100)
            {
                FillColor = Color.Transparent,
                Border = new Border(BorderStyle.Solid, 2, Color.Red)
            };

            // Validate bounds on the first page
            if (!pdfDoc.Pages[1].ValidateShapeBounds(rect))
            {
                Console.WriteLine("Rectangle exceeds page dimensions – adjusting...");
                rect.Right = pdfDoc.Pages[1].PageInfo.Width - 10;
                rect.Top  = pdfDoc.Pages[1].PageInfo.Height - 10;
            }

            // Add the rectangle (how to add shape to pdf)
            pdfDoc.Pages[1].AddRectangle(rect);
            Console.WriteLine("Rectangle added to page 1.");

            // Save the modified PDF
            string outputPath = @"YOUR_DIRECTORY\output.pdf";
            pdfDoc.Save(outputPath);
            Console.WriteLine($"PDF saved as {outputPath}");
        }
    }
}
```

Jalankan program, buka `output.pdf`, dan Anda akan melihat persegi panjang merah tepat di tempat yang kami tentukan. Jika Anda membutuhkan bentuk lain—elips, garis, atau poligon—cukup ganti `Rectangle` dengan `Ellipse`, `Line`, atau `Polygon` sambil mempertahankan alur kerja yang sama. Itulah pada dasarnya **cara menggambar bentuk di pdf** menggunakan Aspose.

## Pertanyaan Umum & Kasus Tepi

### Bagaimana jika saya perlu menggambar di beberapa halaman?
Cukup lakukan loop pada `pdfDoc.Pages` dan panggil `AddRectangle` (atau bentuk lain) untuk setiap halaman. Ingat untuk menyesuaikan koordinat jika halaman memiliki ukuran yang berbeda.

```csharp
foreach (Page page in pdfDoc.Pages)
{
    page.AddRectangle(rect);
}
```

### Bisakah saya mengisi persegi panjang dengan warna?
Tentu saja. Ubah `FillColor` dari `Transparent` ke warna `Color` apa pun yang Anda suka, misalnya `Color.Yellow`. Bentuk akan muncul sebagai blok padat.

### Apakah ini bekerja dengan PDF yang dilindungi kata sandi?
Aspose.PDF dapat membuka file terenkripsi jika Anda menyediakan kata sandinya:

```csharp
Document pdfDoc = new Document(inputPath, new LoadOptions { Password = "mySecret" });
```

### Bagaimana cara menambahkan persegi panjang dengan sudut melengkung?
Gunakan kelas `RoundedRectangle` alih‑alih `Rectangle`. Langkah‑langkah lainnya tetap sama.

## Ringkasan

Kami telah membahas **cara menambahkan bentuk ke PDF** menggunakan Aspose.PDF di C#. Prosesnya dapat diringkas menjadi:

1. **Muat dokumen pdf di c#** – buat objek `Document`.  
2. **Definisikan persegi panjang** (atau bentuk lain).  
3. **Validasi batas** untuk menghindari overflow.  
4. **Tambahkan persegi panjang** ke halaman target.  
5. **Simpan** file yang telah dimodifikasi.

Itulah seluruh alur kerja untuk **aspose pdf add rectangle**, dan kini Anda memiliki templat yang dapat disesuaikan untuk lingkaran, garis, atau poligon khusus.

## Apa Selanjutnya?

- **Jelajahi primitif gambar lainnya**: `Ellipse`, `Line`, `Polygon`.  
- **Tambahkan anotasi teks** di samping bentuk Anda untuk interaktivitas yang lebih kaya.  
- **Gabungkan dengan bidang formulir PDF** jika Anda membangun kontrak yang dapat diisi.  
- **Lihat fitur konversi PDF Aspose** untuk mengubah PDF beranotasi menjadi gambar untuk thumbnail pratinjau.

Silakan bereksperimen—mungkin menggambar watermark, menyorot sel tabel, atau menggarisbawahi bidang tanda tangan. API-nya fleksibel, dan kini Anda sudah menguasai dasarnya.

Selamat coding, semoga PDF Anda selalu tampil persis seperti yang Anda inginkan!


## Apa yang Harus Anda Pelajari Selanjutnya?


Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Create PDF Document with Aspose.PDF – Add Page, Shape & Save](/pdf/english/net/document-creation/create-pdf-document-with-aspose-pdf-add-page-shape-save/)
- [How to Add and Customize Page Numbers in PDFs Using Aspose.PDF for .NET | Document Manipulation Guide](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [How to Add Hyperlinks in PDFs Using Aspose.PDF for .NET&#58; A Comprehensive Guide](/pdf/english/net/bookmarks-navigation/add-hyperlinks-pdf-aspose-net-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}