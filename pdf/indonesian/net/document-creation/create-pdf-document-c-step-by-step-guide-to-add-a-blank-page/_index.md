---
category: general
date: 2026-04-10
description: Buat dokumen PDF C# dengan cepat. Pelajari cara menambahkan halaman kosong
  PDF, menggambar persegi panjang PDF, menambahkan bentuk persegi panjang, dan menambahkan
  persegi panjang ke PDF dengan kode yang jelas.
draft: false
keywords:
- create pdf document c#
- add blank page pdf
- draw rectangle pdf
- add rectangle shape
- add rectangle to pdf
language: id
og_description: Buat dokumen PDF C# dalam hitungan menit. Panduan ini menunjukkan
  cara menambahkan halaman PDF kosong, menggambar persegi panjang pada PDF, dan menambahkan
  bentuk persegi panjang dengan kode yang mudah.
og_title: Buat Dokumen PDF C# – Tutorial Lengkap
tags:
- C#
- PDF
- Aspose.PDF
- Document Generation
title: Membuat Dokumen PDF C# – Panduan Langkah-demi-Langkah untuk Menambahkan Halaman
  Kosong dan Menggambar Persegi Panjang
url: /id/net/document-creation/create-pdf-document-c-step-by-step-guide-to-add-a-blank-page/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Membuat Dokumen PDF C# – Panduan Lengkap

Pernah perlu **membuat dokumen PDF C#** untuk fitur pelaporan tetapi tidak tahu harus mulai dari mana? Anda tidak sendirian. Dalam banyak proyek, hambatan pertama adalah mendapatkan PDF halaman kosong yang bersih lalu menggambar grafik sederhana seperti persegi panjang.  

Dalam tutorial ini kita akan menyelesaikan masalah itu langsung: Anda akan melihat cara menambahkan PDF halaman kosong, menggambar persegi panjang PDF, dan akhirnya menambahkan bentuk persegi panjang ke file—semua dengan beberapa baris C#. Pada akhir tutorial Anda akan memiliki `shapes.pdf` yang siap pakai dan dapat dibuka di viewer mana pun.

## Apa yang Akan Anda Pelajari

- Cara menginisialisasi dokumen PDF menggunakan Aspose.PDF untuk .NET.  
- Langkah‑langkah tepat untuk **menambahkan halaman kosong pdf** dan menempatkan persegi panjang di dalamnya.  
- Mengapa kelas `Rectangle` adalah pilihan yang tepat untuk menggambar bentuk.  
- Kesalahan umum seperti ketidaksesuaian ukuran halaman dan cara menghindarinya.  

Tanpa alat eksternal, tanpa sulap—hanya kode C# murni yang dapat Anda salin‑tempel ke aplikasi console.

## Prasyarat

- .NET 6.0 atau lebih baru (kode ini juga bekerja dengan .NET Framework 4.6+).  
- Paket NuGet **Aspose.PDF untuk .NET** (`Install-Package Aspose.PDF`).  
- Pemahaman dasar tentang sintaks C# (variabel, pernyataan `using`, dll.).  

> **Pro tip:** Jika Anda menggunakan Visual Studio, NuGet Package Manager memudahkan instalasi Aspose.PDF hanya dengan satu klik.

## Langkah 1: Inisialisasi Dokumen PDF

Membuat PDF dimulai dengan objek `Document`. Anggaplah ini sebagai kanvas yang akan menampung setiap halaman, gambar, atau bentuk yang Anda tambahkan nanti.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

// Initialise a new PDF document – this is the core of create pdf document c#
var pdfDocument = new Document();
```

Kelas `Document` memberi Anda akses ke koleksi `Pages`, yang merupakan tempat kita nanti akan **menambahkan halaman kosong pdf**.

## Langkah 2: Tambahkan Halaman Kosong ke Dokumen

PDF tanpa halaman pada dasarnya kosong. Menambahkan halaman semudah memanggil `pdfDocument.Pages.Add()`. Halaman baru mewarisi ukuran default (A4) kecuali Anda menentukan lain.

```csharp
// Add a fresh, blank page – this satisfies the add blank page pdf requirement
Page page = pdfDocument.Pages.Add();
```

> **Mengapa ini penting:** Menambahkan halaman terlebih dahulu memastikan bahwa perintah menggambar berikutnya memiliki permukaan untuk dirender. Melewatkan langkah ini akan menyebabkan error runtime saat Anda mencoba menggambar persegi panjang.

## Langkah 3: Tentukan Batas Persegi Panjang

Sekarang kita akan **menggambar persegi panjang pdf** dengan membuat objek `Rectangle`. Konstruktornya menerima koordinat X/Y kiri‑bawah diikuti oleh lebar dan tinggi. Pada contoh kami, kami menginginkan persegi panjang yang pas di dalam halaman dengan margin kecil.

```csharp
// Rectangle coordinates: (0,0) is the lower‑left corner of the page
// Width = 500, Height = 700 – fits comfortably on an A4 page
var rectangle = new Rectangle(0, 0, 500, 700);
```

Jika Anda memerlukan ukuran berbeda, cukup sesuaikan nilai lebar/tinggi. Asal‑mula persegi panjang (0,0) berkorespondensi dengan sudut kiri‑bawah halaman, yang sering menjadi sumber kebingungan bagi pemula.

## Langkah 4: Tambahkan Bentuk Persegi Panjang ke Halaman

Dengan objek persegi panjang siap, kita dapat **menambahkan bentuk persegi panjang** ke halaman. Metode `AddRectangle` menggambar outline menggunakan status grafis saat ini (default adalah garis hitam tipis).

```csharp
// Add the rectangle shape – this completes the add rectangle to pdf step
page.AddRectangle(rectangle);
```

Anda dapat menyesuaikan tampilan dengan memodifikasi objek `Graphics` sebelum memanggil `AddRectangle`, misalnya mengatur `LineWidth` atau `Color`. Untuk mengisi penuh Anda dapat menggunakan `page.AddAnnotation(new SquareAnnotation(...))`, tetapi itu di luar cakupan panduan sederhana ini.

## Langkah 5: Simpan File PDF

Akhirnya, persistenkan dokumen ke disk. Pilih folder yang Anda miliki hak tulis, dan beri file nama yang bermakna seperti `shapes.pdf`.

```csharp
// Save the PDF – you’ll find shapes.pdf in the specified directory
pdfDocument.Save(@"C:\Temp\shapes.pdf");
```

> **Catatan:** Pernyataan `using` dari cuplikan asli tidak diperlukan di sini karena `Document` mengimplementasikan `IDisposable`. Namun, membungkusnya dalam `using` merupakan kebiasaan baik untuk pembersihan sumber daya, terutama pada aplikasi yang lebih besar.

## Contoh Lengkap yang Berfungsi

Menggabungkan semuanya, berikut program console mandiri yang dapat Anda jalankan langsung:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

namespace PdfRectangleDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Create a new PDF document
            using (var pdfDocument = new Document())
            {
                // Step 2: Add a blank page to the document
                Page page = pdfDocument.Pages.Add();

                // Step 3: Define a rectangle that fits inside the page bounds (0,0 to 500,700)
                var rectangle = new Rectangle(0, 0, 500, 700);

                // Step 4: Add the rectangle shape to the page
                page.AddRectangle(rectangle);

                // Step 5: Save the PDF file
                string outputPath = @"C:\Temp\shapes.pdf";
                pdfDocument.Save(outputPath);

                Console.WriteLine($"PDF created successfully at {outputPath}");
            }
        }
    }
}
```

**Output yang diharapkan:** Setelah menjalankan program, buka `C:\Temp\shapes.pdf`. Anda akan melihat satu halaman dengan persegi panjang beroutline hitam yang ditempatkan di sudut kiri‑bawah, berukuran tepat 500 × 700 poin.

## Pertanyaan Umum & Kasus Tepi

| Pertanyaan | Jawaban |
|------------|---------|
| *Apakah saya dapat mengubah ukuran halaman sebelum menambahkan persegi panjang?* | Ya. Buat `Page` dengan dimensi khusus: `var page = pdfDocument.Pages.Add(); page.PageInfo.Width = 600; page.PageInfo.Height = 800;` |
| *Bagaimana jika saya membutuhkan persegi panjang yang terisi?* | Gunakan objek `Graphics`: `page.Canvas.Rectangle(rectangle, Color.Blue, Color.LightBlue);` |
| *Apakah Aspose.PDF gratis?* | Ia menawarkan **free trial** dengan fungsionalitas penuh; lisensi komersial diperlukan untuk penggunaan produksi. |
| *Bagaimana cara menambahkan beberapa persegi panjang?* | Cukup ulangi langkah 3‑4 dengan instance `Rectangle` yang berbeda atau sesuaikan koordinatnya. |

## Langkah Selanjutnya

Sekarang Anda sudah tahu cara **membuat dokumen pdf c#**, **menambahkan halaman kosong pdf**, dan **menggambar persegi panjang pdf**, Anda mungkin ingin menjelajahi:

- Menambahkan teks di dalam persegi panjang (`TextFragment`, `page.Paragraphs.Add`).  
- Menyisipkan gambar (`page.Resources.Images.Add`) untuk membangun laporan yang lebih kaya.  
- Mengekspor PDF ke format lain seperti PNG atau DOCX menggunakan API konversi Aspose.  

Semua topik ini secara alami memperluas fondasi **menambahkan persegi panjang ke pdf** yang telah kita bangun di sini.

---

*Selamat coding!* Jika Anda mengalami kendala, silakan tinggalkan komentar di bawah. Dan ingat—setelah menguasai dasar‑dasarnya, menghasilkan PDF yang kompleks menjadi sangat mudah.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}