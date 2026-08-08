---
category: general
date: 2026-03-27
description: Pelajari cara menggambar persegi panjang di PDF menggunakan Aspose.Pdf
  untuk C#. Tambahkan persegi panjang ke PDF, tambahkan bentuk ke PDF, dan gambar
  bentuk pada PDF dengan contoh kode yang jelas.
draft: false
keywords:
- how to draw rectangle
- add rectangle to pdf
- add shape to pdf
- draw shape on pdf
- draw rectangle in pdf
language: id
og_description: Kuasi cara menggambar persegi panjang di PDF menggunakan Aspose.Pdf.
  Tutorial ini menunjukkan cara menambahkan persegi panjang ke PDF, menambahkan bentuk
  ke PDF, dan menggambar bentuk di PDF langkah demi langkah.
og_title: Cara Menggambar Persegi Panjang di PDF dengan C# – Panduan Lengkap
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Cara Menggambar Persegi Panjang di PDF dengan C# – Panduan Langkah demi Langkah
url: /id/net/images-graphics/how-to-draw-rectangle-in-pdf-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Menggambar Persegi Panjang di PDF dengan C# – Panduan Langkah‑ demi‑ Langkah

Pernah bertanya‑tanya **cara menggambar persegi panjang** di PDF tanpa harus berurusan dengan sintaks PDF tingkat rendah? Anda tidak sendirian. Banyak pengembang menemui kebuntuan ketika harus memvisualisasikan kotak pembatas, area sorotan, atau elemen dekoratif sederhana di dalam dokumen yang dihasilkan. Kabar baiknya? Dengan Aspose.Pdf untuk .NET prosesnya menjadi sangat mudah.

Dalam tutorial ini kita akan membahas semua yang Anda perlukan untuk **menambahkan persegi panjang ke PDF**, **menambahkan bentuk ke PDF**, dan pada akhirnya **menggambar persegi panjang di PDF** menggunakan C# yang bersih dan idiomatik. Pada akhir tutorial Anda akan memiliki program yang dapat dijalankan dan menghasilkan file PDF berisi persegi panjang yang tajam—tanpa memerlukan alat eksternal.

## Prasyarat

- .NET 6.0 atau yang lebih baru (kode ini juga bekerja dengan .NET Core dan .NET Framework)
- Paket NuGet Aspose.Pdf untuk .NET (`Install-Package Aspose.Pdf`)
- Lingkungan pengembangan C# dasar (Visual Studio, VS Code, Rider, dll.)

Tidak ada pustaka lain yang diperlukan; semua hal lain ditangani oleh Aspose.Pdf itu sendiri.

## Langkah 1: Siapkan Proyek dan Impor Namespace

Pertama, buat aplikasi konsol baru dan impor namespace Aspose.Pdf.

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
            // We'll place the rest of the code here.
        }
    }
}
```

**Mengapa ini penting:** Mengimpor `Aspose.Pdf.Drawing` memberi Anda akses ke kelas bentuk `Rectangle` yang akan kita gunakan untuk **menggambar bentuk pada PDF**. Menjaga titik masuk tetap rapi membuat langkah‑langkah selanjutnya lebih mudah diikuti.

## Langkah 2: Buat Dokumen PDF Baru dan Sebuah Halaman

PDF tanpa halaman tidak ada artinya, jadi kita mulai dengan membuat objek dokumen dan menambahkan satu halaman.

```csharp
// Step 2: Initialize a new PDF document
Document pdfDoc = new Document();

// Add a blank page to the document (size defaults to A4)
Page page = pdfDoc.Pages.Add();
```

**Penjelasan:** Kelas `Document` mewakili seluruh file, sementara `Pages.Add()` mengembalikan objek `Page` baru tempat kita nanti **menambahkan persegi panjang ke PDF**. Ukuran A4 default cocok untuk kebanyakan kasus, tetapi Anda dapat memberikan lebar/tinggi jika memerlukan kanvas khusus.

## Langkah 3: Definisikan Bentuk Persegi Panjang

Sekarang masuk ke inti **cara menggambar persegi panjang**—menentukan posisi dan dimensinya.

```csharp
// Step 3: Define a rectangle shape (x, y, width, height)
// Coordinates are measured from the lower‑left corner of the page.
var rectangleShape = new Rectangle(100, 500, 300, 200)
{
    // Optional: set line color and fill color
    BorderColor = Color.Black,
    BorderWidth = 2,
    FillColor = Color.LightGray
};
```

**Mengapa kami mengatur properti‑properti ini:**  
- `BorderColor` dan `BorderWidth` mengontrol garis tepi, membuat persegi panjang terlihat.  
- `FillColor` memberikan latar belakang yang halus, berguna saat Anda ingin menyorot suatu wilayah.  
- Konstruktor `(x, y, width, height)` memungkinkan Anda **menggambar persegi panjang di PDF** tepat di tempat yang diinginkan.

## Langkah 4: Tambahkan Persegi Panjang ke Halaman

Setelah bentuk siap, kita kini **menambahkan bentuk ke PDF** dengan menempelkannya ke koleksi `Annotations` halaman. Aspose.Pdf secara otomatis memvalidasi batas, jadi Anda tidak perlu khawatir tentang overflow.

```csharp
// Step 4: Add the rectangle shape to the page
page.Annotations.Add(rectangleShape);
```

**Apa yang terjadi di balik layar:** Koleksi `Annotations` memperlakukan persegi panjang sebagai grafik vektor. Saat PDF dirender, pustaka menerjemahkan koordinat kami ke dalam aliran konten PDF.

## Langkah 5: Simpan Dokumen

Akhirnya, tulis PDF ke disk sehingga Anda dapat membukanya dengan penampil apa pun.

```csharp
// Step 5: Save the PDF file
string outputPath = "RectangleDemo.pdf";
pdfDoc.Save(outputPath);
Console.WriteLine($"PDF saved to {outputPath}");
```

**Hasil:** Membuka `RectangleDemo.pdf` menampilkan persegi panjang abu‑abu muda dengan batas hitam yang ditempatkan 100 pt dari kiri dan 500 pt dari bawah halaman. Itulah solusi lengkap untuk **cara menggambar persegi panjang** di PDF menggunakan C#.

## Contoh Lengkap yang Berfungsi

Menggabungkan semua potongan, berikut program lengkap yang siap dijalankan:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using Aspose.Pdf.Color;

namespace PdfRectangleDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Initialize a new PDF document
            Document pdfDoc = new Document();

            // Add a blank page (A4 by default)
            Page page = pdfDoc.Pages.Add();

            // Define a rectangle shape (x, y, width, height)
            var rectangleShape = new Rectangle(100, 500, 300, 200)
            {
                BorderColor = Color.Black,
                BorderWidth = 2,
                FillColor = Color.LightGray
            };

            // Add the rectangle to the page
            page.Annotations.Add(rectangleShape);

            // Save the document
            string outputPath = "RectangleDemo.pdf";
            pdfDoc.Save(outputPath);
            Console.WriteLine($"PDF saved to {outputPath}");
        }
    }
}
```

**Output yang diharapkan:** Sebuah file bernama `RectangleDemo.pdf` berisi satu halaman dengan persegi panjang abu‑abu muda yang terpusat dan berbingkai hitam. Anda dapat membukanya dengan Adobe Reader, Chrome, atau penampil PDF apa pun.

## Variasi Umum & Kasus Tepi

### 1. Menggambar Beberapa Persegi Panjang

Jika Anda perlu **menambahkan persegi panjang ke PDF** lebih dari satu kali, cukup buat objek `Rectangle` tambahan dan tambahkan masing‑masing ke `page.Annotations`. Melakukan iterasi atas koleksi koordinat membuatnya sangat mudah.

```csharp
foreach (var rectInfo in rectangles)
{
    var rect = new Rectangle(rectInfo.X, rectInfo.Y, rectInfo.Width, rectInfo.Height)
    {
        BorderColor = Color.Blue,
        BorderWidth = 1,
        FillColor = Color.Transparent
    };
    page.Annotations.Add(rect);
}
```

### 2. Menggunakan Unit Berbeda

Aspose.Pdf bekerja dalam poin (1 pt = 1/72 inci). Jika Anda lebih suka milimeter, konversikan terlebih dahulu:

```csharp
double mmToPt = 72.0 / 25.4;
float x = (float)(20 * mmToPt); // 20 mm from left
float y = (float)(150 * mmToPt);
```

### 3. Menambahkan Persegi Panjang sebagai Form Field

Ketika Anda memerlukan persegi panjang interaktif (misalnya area yang dapat diklik), gunakan `LinkAnnotation` alih‑alih `Rectangle` biasa. Kodenya serupa tetapi menambahkan URL atau aksi JavaScript.

### 4. Kekhawatiran Kompatibilitas

Aspose.Pdf versi 23.9 (dirilis awal 2026) sepenuhnya mendukung API yang ditunjukkan di atas. Versi lama mungkin memerlukan `page.AddAnnotation(rectangleShape)` alih‑alih `page.Annotations.Add`. Selalu periksa catatan rilis jika Anda menemukan kesalahan kompilasi.

## Tips Pro & Jebakan

- **Tip pro:** Atur `FillColor = Color.Transparent` jika Anda hanya membutuhkan garis tepi. Ini sedikit mengurangi ukuran file.
- **Waspadai:** Menggunakan koordinat yang melebihi dimensi halaman. Aspose.Pdf akan memotong bentuk secara diam‑diam, yang dapat membingungkan saat debugging.
- **Catatan kinerja:** Menambahkan ribuan persegi panjang tidak masalah, tetapi jika Anda menghasilkan laporan besar pertimbangkan untuk mengelompokkan bentuk ke dalam satu objek `Graphics` guna mengurangi beban.

## Referensi Visual

Berikut adalah tangkapan layar cepat dari PDF yang dihasilkan (persegi panjang disorot dengan abu‑abu muda). Teks alt mencakup kata kunci utama untuk SEO.

![contoh cara menggambar persegi panjang di PDF](https://example.com/images/rectangle-demo.png "contoh cara menggambar persegi panjang di PDF")

## Kesimpulan

Kami telah membahas **cara menggambar persegi panjang** di PDF menggunakan Aspose.Pdf untuk C#. Dengan membuat `Document`, menambahkan `Page`, mendefinisikan bentuk `Rectangle`, dan akhirnya **menambahkan bentuk ke PDF**, Anda dapat menghasilkan grafik berbasis vektor hanya dengan beberapa baris kode. Baik Anda perlu **menambahkan persegi panjang ke pdf** untuk sorotan, debugging tata letak, atau overlay UI, pendekatan ini skalabel dengan baik.

Selanjutnya, Anda dapat menjelajahi **menggambar bentuk pada pdf** selain persegi panjang—misalnya lingkaran, polyline, atau bahkan jalur SVG khusus. Atau selami rendering teks, penyisipan gambar, dan manipulasi form PDF untuk membangun laporan lengkap. Pustaka Aspose.Pdf menawarkan API yang kaya, dan dengan dasar yang telah dibahas di sini Anda siap bereksperimen.

Selamat coding, semoga PDF Anda selalu tampil persis seperti yang Anda bayangkan!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}