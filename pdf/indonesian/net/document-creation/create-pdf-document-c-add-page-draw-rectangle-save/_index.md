---
category: general
date: 2026-02-14
description: 'Buat dokumen PDF C# dengan cepat: tambahkan halaman ke PDF, gambar bentuk
  persegi panjang, dan simpan PDF ke file menggunakan Aspose.Pdf dalam beberapa baris
  kode.'
draft: false
keywords:
- create pdf document c#
- add page to pdf
- how to draw rectangle
- add shape to pdf
- save pdf to file
language: id
og_description: Buat dokumen PDF dengan C# dalam hitungan menit. Pelajari cara menambahkan
  halaman ke PDF, menggambar persegi panjang, menambahkan bentuk ke PDF, dan menyimpan
  PDF ke file dengan contoh kode yang jelas.
og_title: Buat Dokumen PDF C# – Panduan Langkah demi Langkah
tags:
- Aspose.Pdf
- C#
- PDF generation
title: Buat Dokumen PDF C# – Tambah Halaman, Gambar Persegi Panjang & Simpan
url: /id/net/document-creation/create-pdf-document-c-add-page-draw-rectangle-save/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat Dokumen PDF C# – Tambahkan Halaman, Gambar Persegi Panjang & Simpan

Pernah perlu **membuat dokumen PDF C#** dari awal dan bertanya-tanya harus mulai dari mana? Anda tidak sendirian—banyak pengembang mengalami hal yang sama saat pertama kali menangani pembuatan PDF secara programatik. Kabar baik? Dengan beberapa baris kode Aspose.Pdf Anda dapat menambahkan halaman ke PDF, menggambar persegi panjang, dan **menyimpan PDF ke file** tanpa kesulitan.

Dalam tutorial ini kita akan membahas semua yang Anda perlukan: menginisialisasi PDF, menyisipkan halaman baru, menggambar bentuk persegi panjang, dan akhirnya menyimpan file ke disk. Pada akhir tutorial Anda akan memiliki aplikasi console yang dapat dijalankan dan menghasilkan persegi panjang berpinggir biru di dalam halaman PDF baru.

## Apa yang Anda Butuhkan

- **.NET 6 atau lebih baru** (contoh menggunakan pernyataan tingkat atas, tetapi versi .NET terbaru mana pun dapat dipakai)
- **Aspose.Pdf for .NET** paket NuGet  
  ```bash
  dotnet add package Aspose.Pdf
  ```
- Sebuah folder yang Anda miliki hak menulisnya – tutorial ini akan menyimpan file ke `YOUR_DIRECTORY/shapes.pdf`.

Tidak ada konfigurasi tambahan, tidak ada XML, hanya C# biasa.

## Buat Dokumen PDF C# – Gambaran Umum

Langkah pertama adalah membuat objek `Document`. Anggap ini sebagai kanvas kosong Anda; semua yang Anda tambahkan kemudian—halaman, teks, bentuk—akan terikat pada satu instance ini.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

// Step 1: Create a new PDF document (the canvas)
using var pdfDocument = new Document();
```

> **Mengapa `using var`?**  
> Kelas `Document` mengimplementasikan `IDisposable`. Membungkusnya dalam pernyataan `using` menjamin semua sumber daya tak terkelola (handle file, buffer native) dilepaskan segera setelah selesai, yang sangat penting pada layanan yang berjalan lama.

## Tambahkan Halaman ke PDF

PDF tanpa halaman ibarat buku tanpa halaman—tidak berguna. Menambahkan halaman cukup dengan satu pemanggilan metode, dan Anda juga akan mendapatkan objek `Page` yang dapat dimanipulasi kemudian.

```csharp
// Step 2: Add a fresh page to the document
var pdfPage = pdfDocument.Pages.Add();
```

> **Tip:** Halaman yang baru ditambahkan secara otomatis memakai ukuran default (A4). Jika Anda memerlukan ukuran khusus, Anda dapat mengatur `pdfPage.PageInfo.Width` dan `Height` sebelum menambahkan konten apa pun.

## Cara Menggambar Persegi Panjang

Sekarang bagian yang menyenangkan: menggambar persegi panjang. Aspose.Pdf menggunakan kelas `RectangleShape`, yang mengharapkan sebuah `Rectangle` (x, y, lebar, tinggi) yang mendefinisikan batasnya. Koordinat dimulai dari sudut kiri‑bawah halaman.

```csharp
// Step 3: Define the rectangle bounds (x, y, width, height)
// This will be validated – an exception is thrown if the rectangle is out of bounds
var rectangleBounds = new Rectangle(50, 50, 200, 150);
```

> **Kasus tepi:** Jika `x + width` melebihi lebar halaman atau `y + height` melebihi tinggi halaman, Aspose akan melempar `ArgumentException`. Selalu periksa kembali dimensi Anda, terutama saat menghasilkan PDF untuk ukuran halaman yang berbeda.

## Tambahkan Bentuk ke PDF

Setelah batas siap, kita buat bentuknya, beri warna garis biru, dan letakkan ke dalam koleksi paragraf halaman.

```csharp
// Step 4: Create a rectangle shape with a blue stroke and add it to the page
var rectangleShape = new RectangleShape(rectangleBounds)
{
    StrokeColor = Color.Blue,   // Outline color
    // FillColor = Color.LightGray, // Uncomment to add a fill
    // LineWidth = 2                // Adjust border thickness if needed
};
pdfPage.Paragraphs.Add(rectangleShape);
```

> **Mengapa menambahkannya ke `Paragraphs`?**  
> Di Aspose.Pdf, elemen visual seperti bentuk diperlakukan sebagai “paragraf” karena mereka menempati area persegi panjang pada halaman. Desain ini menjaga konsistensi mesin tata letak antara teks dan grafik.

## Simpan PDF ke File

Langkah akhir adalah menyimpan dokumen. Berikan path lengkap, dan Aspose akan menangani semua proses berat—kompresi, aliran objek, dan tabel referensi silang semuanya diurus secara otomatis.

```csharp
// Step 5: Save the PDF to a file
pdfDocument.Save("YOUR_DIRECTORY/shapes.pdf");
```

> **Pro tip:** Gunakan `Path.Combine(Environment.CurrentDirectory, "shapes.pdf")` jika Anda ingin file berada di samping executable Anda, atau panggil `Directory.CreateDirectory` terlebih dahulu untuk menghindari `DirectoryNotFoundException`.

### Hasil yang Diharapkan

Buka `shapes.pdf` dengan penampil PDF apa pun. Anda akan melihat satu halaman berukuran A4 dengan **persegi panjang berpinggir biru** yang ditempatkan 50 poin dari tepi kiri dan bawah, berukuran 200 × 150 poin. Tidak ada teks, hanya bentuk—sempurna untuk watermark, bidang formulir, atau placeholder visual.

![PDF document with a blue rectangle created using create pdf document c#](https://example.com/images/pdf-rectangle.png "PDF document with a blue rectangle created using create pdf document c#")

*Alt text:* *PDF document with a blue rectangle created using create pdf document c#.*

## Contoh Kerja Penuh

Berikut adalah program lengkap yang siap disalin‑tempel. Program ini dikompilasi sebagai aplikasi console (`dotnet new console`) dan berjalan tanpa konfigurasi tambahan selain paket NuGet.

```csharp
// Program.cs
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

using var pdfDocument = new Document();               // Create PDF document
var pdfPage = pdfDocument.Pages.Add();                // Add a page

// Define rectangle bounds (x, y, width, height)
// Aspose validates the rectangle – out‑of‑bounds throws an exception
var rectangleBounds = new Rectangle(50, 50, 200, 150);

// Create the rectangle shape (blue stroke) and add it to the page
var rectangleShape = new RectangleShape(rectangleBounds)
{
    StrokeColor = Color.Blue
};
pdfPage.Paragraphs.Add(rectangleShape);

// Save the document to disk
pdfDocument.Save("YOUR_DIRECTORY/shapes.pdf");

// Inform the user
Console.WriteLine("PDF created successfully at YOUR_DIRECTORY/shapes.pdf");
```

Jalankan program, buka file yang dihasilkan, dan Anda akan melihat bentuk persis di tempat yang telah didefinisikan.

## Pertanyaan Umum & Hal-hal yang Perlu Diperhatikan

- **T:** *Bagaimana jika saya membutuhkan persegi panjang yang terisi?*  
  **J:** Hapus komentar pada baris `FillColor` di inisialisasi `RectangleShape`. Aspose mendukung warna solid, gradien, dan bahkan isian gambar.

- **T:** *Bisakah saya menggambar beberapa bentuk pada halaman yang sama?*  
  **J:** Tentu saja. Cukup buat objek `RectangleShape`, `Ellipse`, atau `Polygon` tambahan dan tambahkan masing‑masing ke `pdfPage.Paragraphs`.

- **T:** *Apakah sistem koordinat selalu kiri‑bawah?*  
  **J:** Ya, Aspose mengikuti spesifikasi PDF di mana asal (0,0) berada di sudut kiri‑bawah. Jika Anda lebih suka asal di kiri‑atas, Anda harus menghitung `y = pageHeight - desiredY`.

- **T:** *Apa yang terjadi jika folder target tidak ada?*  
  **J:** `pdfDocument.Save` akan melempar `DirectoryNotFoundException`. Buat folder terlebih dahulu dengan `Directory.CreateDirectory`.

## Langkah Selanjutnya

Setelah Anda tahu cara **menambahkan halaman ke PDF**, **menggambar persegi panjang**, **menambahkan bentuk ke PDF**, dan **menyimpan PDF ke file**, Anda dapat memperluas fondasi ini:

- Menyisipkan teks, gambar, atau tabel bersamaan dengan bentuk.  
- Menggunakan `Graphics` untuk menggambar bebas (garis, busur, jalur khusus).  
- Menjelajahi enkripsi PDF atau tanda tangan digital jika keamanan menjadi perhatian.  

Setiap topik tersebut dibangun langsung di atas kode yang baru saja kita bahas, jadi silakan bereksperimen dengan percaya diri.

---

**Intinya:** Anda baru saja mempelajari alur kerja lengkap untuk **membuat dokumen PDF C#** dengan Aspose.Pdf—menginisialisasi, menambahkan halaman, menggambar bentuk persegi panjang, dan menyimpan file. Ini merupakan blok bangunan yang kuat untuk faktur, laporan, sertifikat, atau dokumen otomatis apa pun yang perlu Anda hasilkan secara dinamis. Selamat coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}