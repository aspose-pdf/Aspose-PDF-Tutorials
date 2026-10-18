---
category: general
date: 2026-08-04
description: Tambahkan persegi panjang ke PDF menggunakan C#. Pelajari cara menggambar
  bentuk dalam PDF C# dengan Aspose.Pdf dalam contoh yang jelas dan lengkap.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add rectangle to pdf
- how to draw shape in pdf c#
language: id
lastmod: 2026-08-04
og_description: Tambahkan persegi panjang ke PDF menggunakan C#. Tutorial ini menunjukkan
  cara menggambar bentuk di PDF C# dengan cepat dan andal.
og_image_alt: Screenshot of a PDF page with a blue rectangle drawn by C# code
og_title: Tambahkan persegi panjang ke PDF dengan C# – panduan pemrograman lengkap
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Add rectangle to PDF using C#. Learn how to draw shape in PDF C# with
    Aspose.Pdf in a clear, complete example.
  headline: Add rectangle to PDF with C# – step‑by‑step guide
  type: TechArticle
- description: Add rectangle to PDF using C#. Learn how to draw shape in PDF C# with
    Aspose.Pdf in a clear, complete example.
  name: Add rectangle to PDF with C# – step‑by‑step guide
  steps:
  - name: '**Create a new console project**'
    text: '**Create a new console project**'
  - name: '**Add the Aspose.Pdf package**'
    text: '**Add the Aspose.Pdf package**'
  - name: '**Place `input.pdf`** in the project directory (or any folder you reference
      later).'
    text: '**Place `input.pdf`** in the project directory (or any folder you reference
      later).'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Menambahkan persegi panjang ke PDF dengan C# – panduan langkah demi langkah
url: /id/net/images-graphics/add-rectangle-to-pdf-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Menambahkan persegi panjang ke PDF dengan C# – panduan langkah demi langkah

Jika Anda perlu **menambahkan persegi panjang ke PDF** dari aplikasi C#, panduan ini menunjukkan secara tepat cara melakukannya. Anda akan melihat contoh lengkap yang dapat dijalankan yang menggambar bentuk dalam PDF C# menggunakan library Aspose.Pdf, dan Anda akan memahami mengapa setiap baris kode penting.

Menggambar bentuk dalam PDF adalah kebutuhan umum untuk pembuat laporan, templat faktur, dan branding dokumen khusus. Pada akhir tutorial ini Anda dapat menyisipkan anotasi persegi panjang apa pun, mengubah ukuran, warna, atau posisinya, dan menyimpan dokumen yang dimodifikasi tanpa kehilangan konten yang ada.

**Apa yang akan Anda pelajari**

* Cara memuat PDF yang sudah ada dengan Aspose.Pdf.  
* Cara mendefinisikan batas persegi panjang dan membuat bentuk persegi panjang.  
* Cara menambahkan persegi panjang ke koleksi paragraf sebuah halaman.  
* Cara menyimpan PDF yang telah diperbarui dan memverifikasi hasilnya.  
* Variasi untuk beberapa halaman, transparansi, dan gaya garis khusus.

**Prasyarat**

* .NET 6.0 atau lebih baru (kode juga berfungsi dengan .NET Framework 4.7+).  
* Visual Studio 2022 atau IDE C# apa pun.  
* Referensi NuGet ke `Aspose.Pdf` (versi trial gratis atau berlisensi).  
* File PDF input bernama `input.pdf` yang ditempatkan di folder yang Anda kontrol.

---

## Cara menggambar bentuk dalam PDF C# – menyiapkan proyek

1. **Buat proyek konsol baru**  

   ```bash
   dotnet new console -n PdfRectangleDemo
   cd PdfRectangleDemo
   ```

2. **Tambahkan paket Aspose.Pdf**  

   ```bash
   dotnet add package Aspose.Pdf
   ```

3. **Tempatkan `input.pdf`** di direktori proyek (atau folder apa pun yang akan Anda referensikan nanti).

Proyek kini siap untuk mengompilasi kode yang akan **menambahkan persegi panjang ke PDF**.

---

## Langkah 1: Muat dokumen PDF

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

class Program
{
    static void Main()
    {
        // Load the existing PDF file.
        Document pdfDoc = new Document("input.pdf");
```

*Kelas `Document` mem-parsing file dan mengekspos koleksi `Pages`. Memuat adalah operasi pertama yang diperlukan sebelum gambar apa pun dapat dilakukan.*

---

## Langkah 2: Pilih halaman target

```csharp
        // Get the first page (pages are 1‑based).
        Page firstPage = pdfDoc.Pages[1];
```

*Jika Anda perlu menambahkan persegi panjang ke halaman yang berbeda, ganti indeks dengan nomor halaman yang diinginkan. Library akan melemparkan pengecualian ketika indeks berada di luar jangkauan, jadi pastikan PDF berisi cukup halaman.*

---

## Langkah 3: Definisikan batas persegi panjang

```csharp
        // Define the rectangle's position and size (points).
        // (left, bottom, right, top) – origin is bottom‑left.
        Rectangle bounds = new Rectangle(50, 700, 300, 800);
```

*Sistem koordinat menggunakan poin (1 pt = 1/72 inci). Contoh ini membuat persegi panjang selebar 250 pt dan setinggi 100 pt di dekat bagian atas halaman. Sesuaikan angka-angka tersebut agar cocok dengan tata letak Anda.*

---

## Langkah 4: Buat bentuk persegi panjang

```csharp
        // Create a rectangle shape with the defined bounds.
        Rectangle rectangleShape = new Rectangle(bounds)
        {
            // Optional styling – a semi‑transparent blue fill.
            FillColor = Color.FromRgb(0, 120, 215),
            FillOpacity = 0.4,

            // Optional border – 2 pt thick, dark gray.
            Border = new Border
            {
                Width = 2,
                Color = Color.FromRgb(50, 50, 50)
            }
        };
```

*Kelas `Rectangle` mewarisi dari `GraphicalObject`. Menetapkan `FillColor` dan `Border` bersifat opsional, tetapi ini menunjukkan cara mengontrol tampilan ketika Anda **menggambar bentuk dalam PDF C#** melampaui outline biasa.*

---

## Langkah 5: Tambahkan persegi panjang ke halaman

```csharp
        // Add the rectangle shape to the page's paragraph collection.
        firstPage.Paragraphs.Add(rectangleShape);
```

*Paragraf adalah wadah untuk objek yang dapat digambar apa pun. Dengan menyisipkan bentuk ke dalam `Paragraphs`, Aspose.Pdf merendernya saat dokumen disimpan.*

---

## Langkah 6: Simpan PDF yang telah dimodifikasi

```csharp
        // Save the updated PDF to a new file.
        pdfDoc.Save("output.pdf");

        // Inform the user.
        Console.WriteLine("Rectangle added and saved to output.pdf");
    }
}
```

*Menyimpan membuat file baru sehingga `input.pdf` asli tetap tidak berubah. Anda dapat menimpa file sumber dengan memberikan jalur yang sama, tetapi menyimpan cadangan adalah praktik terbaik.*

---

## Kode sumber lengkap (dapat dijalankan)

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using System.Drawing;   // For Color struct

class Program
{
    static void Main()
    {
        // Step 1: Load the PDF document
        Document pdfDoc = new Document("input.pdf");

        // Step 2: Get the first page (pages are 1‑based)
        Page firstPage = pdfDoc.Pages[1];

        // Step 3: Define rectangle bounds (left, bottom, right, top)
        Rectangle bounds = new Rectangle(50, 700, 300, 800);

        // Step 4: Create a rectangle shape with optional styling
        Rectangle rectangleShape = new Rectangle(bounds)
        {
            FillColor = Color.FromArgb(102, 0, 120, 215), // 40 % opacity blue
            FillOpacity = 0.4,
            Border = new Border
            {
                Width = 2,
                Color = Color.FromRgb(50, 50, 50)
            }
        };

        // Step 5: Add the rectangle shape to the page
        firstPage.Paragraphs.Add(rectangleShape);

        // Step 6: Save the modified PDF
        pdfDoc.Save("output.pdf");

        Console.WriteLine("Rectangle added to PDF successfully.");
    }
}
```

**Output yang diharapkan** – Buka `output.pdf` di penampil PDF apa pun. Anda akan melihat persegi panjang berisi warna biru di dekat sudut kanan‑atas halaman pertama, dengan garis tepi berwarna abu‑abu gelap.

---

## Cara menggambar bentuk dalam PDF C# pada beberapa halaman

Jika Anda perlu **menambahkan persegi panjang ke PDF** pada setiap halaman, lakukan loop melalui koleksi `Pages`:

```csharp
foreach (Page page in pdfDoc.Pages)
{
    Rectangle rect = new Rectangle(50, 700, 300, 800);
    Rectangle shape = new Rectangle(rect)
    {
        FillColor = Color.FromArgb(80, 255, 0, 0), // semi‑transparent red
        Border = new Border { Width = 1, Color = Color.Black }
    };
    page.Paragraphs.Add(shape);
}
```

*Pola ini menggunakan batas yang sama pada setiap halaman. Sesuaikan koordinat per halaman jika Anda memerlukan posisi yang berbeda.*

---

## Kesalahan umum dan tips praktik terbaik

| Masalah | Mengapa terjadi | Solusi |
|---------|-----------------|--------|
| Persegi panjang muncul di luar halaman | Koordinat diukur dari kiri‑bawah; menggunakan sistem koordinat yang berorientasi ke atas dapat menyebabkan kebingungan. | Ingat bahwa sumbu Y tumbuh ke atas. Gunakan nilai yang sesuai dengan ukuran halaman (`page.PageInfo.Width`, `page.PageInfo.Height`). |
| Bentuk tidak terlihat | Opasitas isi diatur ke `0` atau lebar batas diatur ke `0`. | Pastikan `FillOpacity` lebih besar dari `0` dan `Border.Width` setidaknya `0.5`. |
| Penyimpanan melempar `AccessDeniedException` | File output terbuka di program lain. | Tutup semua penampil sebelum menjalankan kode, atau simpan ke jalur yang berbeda. |
| Persegi panjang menutupi konten yang ada | Tidak ada kontrol lapisan yang diatur. | Gunakan properti `ZIndex` (nilai lebih tinggi dirender di atas) jika Anda perlu mengontrol lapisan. |

---

## Memperluas persegi panjang – gradien, rotasi, dan transparansi

Aspose.Pdf mendukung grafik tingkat lanjut. Untuk membuat persegi panjang berputar dengan gradien linear:

```csharp
Rectangle gradientRect = new Rectangle(bounds)
{
    // Gradient fill from left (blue) to right (green)
    FillColor = Color.Blue,
    FillColor2 = Color.Green,
    FillMode = FillMode.LinearGradient,
    // Rotate 45 degrees around the rectangle's center
    Rotation = 45
};
firstPage.Paragraphs.Add(gradientRect);
```

*Pola kode yang sama menunjukkan **cara menggambar bentuk dalam PDF C#** dengan efek visual yang lebih kaya.*

---

## Verifikasi hasil secara programatik

Anda dapat memastikan bahwa persegi panjang telah ditambahkan dengan memeriksa jumlah paragraf pada halaman:

```csharp
int shapeCount = firstPage.Paragraphs.Count;
Console.WriteLine($"Page 1 now contains {shapeCount} paragraph objects.");
```

Jika jumlahnya bertambah satu setelah penyisipan, operasi berhasil.

---

## Kesimpulan

Anda kini tahu cara **menambahkan persegi panjang ke PDF** menggunakan C#. Tutorial ini mencakup memuat dokumen, mendefinisikan batas, membuat bentuk persegi panjang, menyisipkannya ke dalam halaman, dan menyimpan hasilnya. Anda juga telah melihat cara menangani beberapa halaman, menghindari kesalahan umum, dan menerapkan gaya lanjutan.

Selanjutnya, jelajahi topik terkait seperti **cara menggambar bentuk dalam PDF C#** untuk lingkaran, poligon, atau jalur bebas, dan pelajari cara menggabungkan bentuk dengan teks serta gambar untuk membangun laporan PDF yang lengkap.

Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait dan membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber daya menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Cara Menambahkan Stempel Halaman pada PDF Menggunakan Aspose.PDF untuk .NET | Panduan Watermark & Latar Belakang](/pdf/english/net/watermarks-backgrounds/implement-page-stamps-aspose-pdf-dotnet/)
- [Cara Menambahkan Stempel Gambar ke PDF Menggunakan Aspose.PDF untuk .NET: Panduan Komprehensif](/pdf/english/net/images-graphics/add-image-stamp-pdf-aspose-dotnet/)
- [Cara Menambahkan Watermark Gambar Berputar ke PDF Menggunakan Aspose.PDF untuk .NET](/pdf/english/net/watermarks-backgrounds/add-rotating-image-watermark-aspose-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}