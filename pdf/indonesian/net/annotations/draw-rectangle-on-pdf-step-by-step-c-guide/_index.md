---
category: general
date: 2026-08-14
description: Gambar persegi panjang pada PDF dengan cepat menggunakan C#. Pelajari
  cara menentukan dimensi persegi panjang dan menambahkan bentuk ke halaman PDF hanya
  dalam beberapa baris.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- draw rectangle on pdf
- how to define rectangle dimensions
language: id
lastmod: 2026-08-14
og_description: gambar persegi panjang pada PDF dengan C# dalam hitungan detik. Panduan
  ini menunjukkan cara menentukan dimensi persegi panjang, menambahkan bentuk, dan
  memverifikasi batas halaman untuk grafik PDF yang andal.
og_image_alt: Screenshot of a PDF page showing a black rectangle drawn with C# code
og_title: Menggambar persegi panjang pada PDF – tutorial lengkap C#
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: draw rectangle on pdf quickly using C#. Learn how to define rectangle
    dimensions and add shapes to a PDF page in just a few lines.
  headline: draw rectangle on pdf – step‑by‑step C# guide
  type: TechArticle
tags:
- PDF
- C#
- Aspose.PDF
- RectangleShape
- Graphics
title: menggambar persegi panjang pada PDF – panduan langkah demi langkah C#
url: /id/net/annotations/draw-rectangle-on-pdf-step-by-step-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# menggambar persegi panjang pada pdf – tutorial lengkap C#

Jika Anda perlu **draw rectangle on pdf** menggunakan C#, panduan ini menunjukkan solusi yang singkat dan siap produksi. Anda akan melihat secara tepat **how to define rectangle dimensions**, memverifikasi bahwa bentuknya cocok, dan menambahkannya ke halaman dengan satu panggilan metode.

Tutorial ini mencakup semua hal mulai dari membuat dokumen PDF hingga merender persegi panjang, sehingga Anda dapat menyalin‑tempel kode ke dalam proyek Anda sendiri dan melihat hasilnya secara langsung. Tidak diperlukan dokumentasi eksternal—hanya langkah‑langkah di bawah ini.

## Prasyarat

Sebelum Anda memulai, pastikan Anda memiliki:

* .NET 6.0 atau lebih baru (kode juga berfungsi dengan .NET Framework 4.7+)
* Paket NuGet **Aspose.PDF for .NET** (`Install-Package Aspose.PDF`)
* Pemahaman dasar tentang sintaks C#
* IDE seperti Visual Studio atau VS Code

> **Pro tip:** Gunakan lisensi evaluasi gratis Aspose.PDF untuk percobaan cepat; lisensi ini menambahkan watermark kecil tetapi memungkinkan Anda menguji semua fitur.

## Cara menggambar persegi panjang pada PDF dengan C#

Inti dari tugas ini adalah membuat `RectangleShape`, mengatur ukuran dan garis tepinya, serta melampirkannya ke `Page`. Header H2 berikut berisi kata kunci utama, memenuhi persyaratan SEO.

```csharp
using System;
using System.Drawing;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new PDF document
        Document pdfDoc = new Document();

        // 2️⃣ Add a blank page (default size: A4)
        Page page = pdfDoc.Pages.Add();

        // 3️⃣ Define the rectangle bounds (x, y, width, height)
        //    This demonstrates how to define rectangle dimensions.
        Rectangle rectBounds = new Rectangle(0, 0, 500, 700);

        // 4️⃣ Create the rectangle shape and set its stroke color
        RectangleShape rectangleShape = new RectangleShape(rectBounds)
        {
            StrokeColor = Color.Black   // black outline
        };

        // 5️⃣ Verify that the shape fits within the page boundaries
        page.CheckShapeBoundary(rectangleShape);

        // 6️⃣ Add the shape to the page
        page.Add(rectangleShape);

        // 7️⃣ Save the PDF to disk
        string outPath = "RectangleDemo.pdf";
        pdfDoc.Save(outPath);
        Console.WriteLine($"PDF saved to {outPath}");
    }
}
```

### Penjelasan setiap langkah

| Langkah | Mengapa penting |
|---------|-----------------|
| **1️⃣ Buat dokumen PDF baru** | Inisialisasi kontainer yang akan menampung halaman dan grafik. |
| **2️⃣ Tambahkan halaman kosong** | Anda memerlukan objek `Page` karena bentuk dilampirkan ke halaman, bukan langsung ke dokumen. |
| **3️⃣ Tentukan batas persegi panjang** | Di sinilah Anda **how to define rectangle dimensions**. Konstruktor `Rectangle` menerima `x`, `y`, `width`, dan `height` dalam satuan point (1 pt = 1/72 in). |
| **4️⃣ Buat bentuk persegi panjang** | `RectangleShape` adalah kelas Aspose yang merender persegi panjang. Menetapkan `StrokeColor` menentukan garis tepi; Anda juga dapat mengatur `FillColor` untuk isi padat. |
| **5️⃣ Verifikasi batas halaman** | `CheckShapeBoundary` melempar pengecualian jika persegi panjang melebihi ukuran halaman, mencegah PDF yang rusak. |
| **6️⃣ Tambahkan bentuk ke halaman** | Bentuk menjadi bagian dari aliran konten halaman. |
| **7️⃣ Simpan PDF** | Menyimpan dokumen ke file yang dapat Anda buka dengan penampil PDF apa pun. |

File `RectangleDemo.pdf` yang dihasilkan berisi persegi panjang hitam yang ditempatkan di sudut kiri‑atas halaman, dengan lebar tepat 500 pt dan tinggi 700 pt.

![contoh menggambar persegi panjang pada pdf](https://example.com/rectangle-demo.png "contoh menggambar persegi panjang pada pdf")

*Teks alt gambar: contoh menggambar persegi panjang pada pdf menunjukkan persegi panjang hitam di sudut kiri atas halaman PDF.*

## Cara menentukan dimensi persegi panjang untuk ukuran halaman yang berbeda

Potongan kode di atas menggunakan nilai tetap (`500 x 700`). Dalam aplikasi nyata Anda sering perlu agar persegi panjang menyesuaikan lebar dan tinggi halaman.

```csharp
// Get page dimensions (in points)
float pageWidth = page.PageInfo.Width;
float pageHeight = page.PageInfo.Height;

// Define a rectangle that occupies 80% of the page width and 50% of the height
float rectWidth  = pageWidth * 0.8f;
float rectHeight = pageHeight * 0.5f;

// Center the rectangle on the page
float rectX = (pageWidth - rectWidth) / 2;
float rectY = (pageHeight - rectHeight) / 2;

Rectangle dynamicRect = new Rectangle(rectX, rectY, rectWidth, rectHeight);
RectangleShape dynamicShape = new RectangleShape(dynamicRect)
{
    StrokeColor = Color.DarkBlue,
    FillColor   = Color.LightGray   // optional fill
};

page.CheckShapeBoundary(dynamicShape);
page.Add(dynamicShape);
```

**Poin penting:**

* Gunakan `page.PageInfo.Width` dan `Height` untuk membaca ukuran halaman yang sebenarnya.
* Mengalikan dengan faktor (misalnya `0.8f`) memungkinkan Anda menyatakan dimensi sebagai persentase dari halaman.
* Pemusatan dicapai dengan mengurangi ukuran persegi panjang dari ukuran halaman dan membagi sisa menjadi dua.

## Kesalahan umum dan cara menghindarinya

| Kesalahan | Mengapa terjadi | Solusi |
|-----------|----------------|--------|
| Persegi panjang melampaui halaman | Dimensi yang dikodekan keras lebih besar dari ukuran halaman. | Panggil `page.CheckShapeBoundary` **sebelum** menambahkan bentuk; sesuaikan dimensi jika pengecualian dilempar. |
| Garis tepi tidak terlihat | `StrokeColor` dibiarkan pada nilai default (`Color.Empty`). | Tetapkan `StrokeColor` secara eksplisit (mis., `Color.Black`). |
| Persegi panjang muncul di luar layar | Koordinat dimulai dari kiri‑bawah dalam ruang PDF; menggunakan koordinat gaya layar kiri‑atas menyebabkan pembalikan. | Ingat bahwa asal `(0,0)` adalah sudut kiri‑bawah. Sesuaikan `y` sesuai atau gunakan `pageHeight - desiredY`. |
| Ketebalan garis tidak terduga | Lebar garis default mungkin terlalu tipis untuk pencetakan. | Setel `rectangleShape.LineWidth = 2;` untuk meningkatkan ketebalan. |

## Memperluas contoh

Setelah Anda dapat **draw rectangle on pdf**, Anda dapat dengan mudah menambahkan bentuk lain:

* **EllipseShape** – untuk lingkaran atau oval.
* **PolygonShape** – untuk poligon khusus.
* **TextFragment** – untuk memberi label pada persegi panjang Anda.

Semua bentuk berbagi alur kerja yang sama: tentukan batas, konfigurasikan tampilan, verifikasi batas, lalu tambahkan ke halaman.

## Program lengkap yang dapat dijalankan

Berikut adalah program lengkap yang menggabungkan contoh persegi panjang dasar dan contoh penyesuaian ukuran dinamis. Salin ke proyek konsol baru, pulihkan paket NuGet `Aspose.PDF`, dan jalankan.

```csharp
using System;
using System.Drawing;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

class RectangleDemo
{
    static void Main()
    {
        // Create document and page
        Document doc = new Document();
        Page page = doc.Pages.Add();

        // ==== Fixed‑size rectangle (basic example) ====
        Rectangle fixedRect = new Rectangle(0, 0, 500, 700);
        RectangleShape fixedShape = new RectangleShape(fixedRect)
        {
            StrokeColor = Color.Black,
            LineWidth   = 1
        };
        page.CheckShapeBoundary(fixedShape);
        page.Add(fixedShape);

        // ==== Dynamic rectangle that adapts to page size ====
        float pageW = page.PageInfo.Width;
        float pageH = page.PageInfo.Height;

        float dynWidth  = pageW * 0.6f;
        float dynHeight = pageH * 0.3f;
        float dynX      = (pageW - dynWidth) / 2;
        float dynY      = (pageH - dynHeight) / 2;

        Rectangle dynamicRect = new Rectangle(dynX, dynY, dynWidth, dynHeight);
        RectangleShape dynamicShape = new RectangleShape(dynamicRect)
        {
            StrokeColor = Color.DarkBlue,
            FillColor   = Color.LightYellow,
            LineWidth   = 2
        };
        page.CheckShapeBoundary(dynamicShape);
        page.Add(dynamicShape);

        // Save PDF
        string outFile = "CombinedRectangles.pdf";
        doc.Save(outFile);
        Console.WriteLine($"PDF created: {outFile}");
    }
}
```

**Output yang diharapkan:**  
Buka `CombinedRectangles.pdf`. Anda akan melihat persegi panjang hitam yang ditempatkan di sudut kiri‑bawah dan persegi panjang biru‑gelap terpusat dengan isi kuning‑terang. Kedua persegi panjang menghormati margin halaman.

## Kesimpulan

Anda kini tahu cara **draw rectangle on pdf** dengan C# dan secara tepat **how to define rectangle dimensions** untuk tata letak tetap maupun responsif. Pendekatan ini menggunakan `RectangleShape` Aspose.PDF, pemeriksaan batas, dan aritmetika sederhana untuk menyesuaikan dengan ukuran halaman apa pun.

Selanjutnya, Anda mungkin ingin menjelajahi:

* Menambahkan **warna isi** dan **gaya garis** (garis putus, titik‑titik) – kata kunci sekunder: how to define rectangle dimensions with style.
* Menggabungkan beberapa bentuk menjadi satu `Page` untuk membuat diagram atau formulir.
* Mengekspor PDF ke stream untuk API web alih‑alih menyimpan ke disk.

Bereksperimenlah dengan berbagai ukuran, warna, dan posisi untuk menguasai grafik PDF dalam aplikasi .NET Anda. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan menjelajahi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Cara Menyesuaikan PDF dengan Aspose.PDF untuk .NET&#58; Atur Margin Halaman dan Gambar Garis](/pdf/english/net/document-manipulation/customize-pdfs-aspose-pdf-set-margins-draw-lines/)
- [Cara Menambahkan Stempel Halaman pada PDF Menggunakan Aspose.PDF untuk .NET&#58; Panduan Lengkap](/pdf/english/net/watermarks-backgrounds/add-page-stamp-aspose-pdf-dotnet-guide/)
- [Cara Menambahkan Stempel Nomor Halaman pada PDF Menggunakan Aspose.PDF untuk .NET | Watermarks & Backgrounds](/pdf/english/net/watermarks-backgrounds/add-page-number-stamp-using-aspose-pdf-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}