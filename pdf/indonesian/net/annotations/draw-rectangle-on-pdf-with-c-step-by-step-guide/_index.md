---
category: general
date: 2026-06-21
description: Gambar persegi panjang pada PDF menggunakan C#. Pelajari cara memuat
  dokumen PDF, membuat anotasi persegi panjang hitam, dan menyimpan PDF yang telah
  dimodifikasi secara efisien.
draft: false
keywords:
- draw rectangle on pdf
- load pdf document
- add black rectangle
- create black rectangle
- save modified pdf
language: id
og_description: Gambar persegi panjang pada PDF di C# dengan memuat dokumen PDF, membuat
  anotasi persegi panjang hitam, dan menyimpan PDF yang telah dimodifikasi. Kode lengkap
  disertakan.
og_title: Gambar Persegi Panjang pada PDF dengan C# – Tutorial Pemrograman Lengkap
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Draw rectangle on PDF using C#. Learn how to load PDF document, create
    black rectangle annotation, and save modified PDF efficiently.
  headline: Draw Rectangle on PDF with C# – Step‑by‑Step Guide
  type: TechArticle
- description: Draw rectangle on PDF using C#. Learn how to load PDF document, create
    black rectangle annotation, and save modified PDF efficiently.
  name: Draw Rectangle on PDF with C# – Step‑by‑Step Guide
  steps:
  - name: .NET 6.0 SDK (or any recent .NET version) installed
    text: .NET 6.0 SDK (or any recent .NET version) installed
  - name: 'A reference to **Aspose.PDF for .NET** (available via NuGet: `Install-Package
      Aspose.PDF`)'
    text: 'A reference to **Aspose.PDF for .NET** (available via NuGet: `Install-Package
      Aspose.PDF`)'
  - name: An existing PDF file (`input.pdf`) placed in a folder you can read/write
    text: An existing PDF file (`input.pdf`) placed in a folder you can read/write
  type: HowTo
tags:
- PDF
- C#
- Aspose.PDF
title: Menggambar Persegi Panjang pada PDF dengan C# – Panduan Langkah demi Langkah
url: /id/net/annotations/draw-rectangle-on-pdf-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Menggambar Persegi Panjang pada PDF dengan C# – Tutorial Pemrograman Lengkap

Pernah membutuhkan untuk **draw rectangle on PDF** file dari aplikasi .NET tetapi tidak yakin harus mulai dari mana? Anda bukan satu-satunya. Baik itu menyorot sebuah bagian, menyensor data sensitif, atau sekadar menambahkan petunjuk visual, mempelajari cara *draw rectangle on PDF* secara programatik dapat menghemat Anda berjam-jam pengeditan manual.

Dalam panduan ini kami akan membahas contoh praktis yang **loads a PDF document**, **creates a black rectangle**, dan kemudian **saves the modified PDF**. Pada akhir Anda akan memiliki potongan kode yang dapat digunakan kembali dan dapat dimasukkan ke proyek C# mana pun—tanpa misteri, hanya kode yang jelas dan penjelasan.

## Apa yang Dibahas dalam Tutorial Ini

- Cara **load pdf document** menggunakan pustaka Aspose.PDF untuk .NET  
- Mendefinisikan koordinat persegi panjang dan memastikan tetap berada di dalam batas halaman  
- Menggunakan metode **add black rectangle** untuk memberi anotasi pada halaman  
- **Save modified pdf** ke lokasi file baru  
- Penanganan edge‑case (banyak halaman, persegi panjang out‑of‑bounds, warna khusus)  

Tanpa alat eksternal, tanpa referensi yang samar—hanya contoh lengkap yang dapat dijalankan yang dapat Anda copy‑paste.

---

## Prasyarat

Sebelum kita mulai, pastikan Anda memiliki:

1. .NET 6.0 SDK (atau versi .NET terbaru lainnya) terpasang  
2. Referensi ke **Aspose.PDF for .NET** (tersedia via NuGet: `Install-Package Aspose.PDF`)  
3. File PDF yang sudah ada (`input.pdf`) ditempatkan di folder yang dapat Anda baca/tulis  

Itu saja. Jika Anda nyaman dengan sintaks dasar C#, Anda siap melanjutkan.

---

## Langkah 1: Load PDF Document

Hal pertama yang kita butuhkan adalah pemanggilan **load pdf document**. Kelas `Document` milik Aspose.PDF mengambil jalur file dan membaca seluruh file ke dalam memori.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using System.Drawing;

// Load the source PDF
Document pdfDocument = new Document(@"C:\MyFiles\input.pdf");
```

*Mengapa ini penting*: Memuat PDF memberi Anda akses ke halaman, metadata, dan permukaan gambar. Tanpa langkah ini Anda tidak dapat menempatkan bentuk apa pun.

---

## Langkah 2: Pilih Halaman Target

Halaman PDF di Aspose menggunakan indeks mulai dari 1, jadi halaman pertama memiliki indeks 1. Ambil halaman yang ingin Anda beri anotasi—biasanya yang pertama untuk demo cepat.

```csharp
// Get the first page (pages are 1‑based)
Page targetPage = pdfDocument.Pages[1];
```

Jika Anda perlu bekerja pada halaman lain, cukup ubah indeksnya. Ingat untuk memvalidasi bahwa indeks tersebut ada untuk menghindari `ArgumentOutOfRangeException`.

---

## Langkah 3: Definisikan Geometri Persegi Panjang

Persegi panjang didefinisikan oleh koordinat lower‑left (X,Y) dan upper‑right (X,Y). Struct `Rectangle` menyimpan nilai-nilai ini sebagai `LLX`, `LLY`, `URX`, `URY`.

```csharp
// Define the rectangle (lower‑left X,Y and upper‑right X,Y)
Rectangle boundingRect = new Rectangle(100, 100, 300, 300);
```

Silakan sesuaikan angka-angka tersebut—`100,100` menempatkan sudut lower‑left 100 poin dari tepi kiri dan bawah, sementara `300,300` menetapkan sudut upper‑right 300 poin dari tepi.

---

## Langkah 4: Verifikasi Persegi Panjang Masuk dalam Halaman

Mencoba menggambar di luar batas halaman akan diabaikan atau menyebabkan pengecualian, tergantung pada versi pustaka. Pemeriksaan cepat membuat kode Anda lebih kuat.

```csharp
// Ensure the rectangle fits within the page dimensions
if (targetPage.PageInfo.Width >= boundingRect.URX &&
    targetPage.PageInfo.Height >= boundingRect.URY)
{
    // Rectangle is safe to add
}
else
{
    throw new InvalidOperationException("Rectangle exceeds page dimensions.");
}
```

*Tips pro*: Jika Anda berencana mendukung PDF dengan ukuran beragam, Anda dapat menghitung persegi panjang berdasarkan persentase lebar/tinggi halaman alih-alih poin absolut.

---

## Langkah 5: Tambahkan Anotasi Persegi Panjang Hitam

Sekarang bagian yang menyenangkan—**add black rectangle** ke halaman. Aspose menyediakan `AddRectangle` yang menerima geometri dan `Color`. Kami akan menggunakan `Color.Black` untuk **create black rectangle**.

```csharp
// Add a black rectangle annotation to the page
targetPage.AddRectangle(boundingRect, Color.Black);
```

Baris tunggal itu melakukan pekerjaan berat: ia membuat objek anotasi, mengatur warna batas menjadi hitam, dan menyisipkannya ke dalam koleksi anotasi halaman.

Jika Anda pernah membutuhkan isi atau gaya batas yang berbeda, jelajahi overload yang menerima objek `Annotation` dimana Anda dapat menyesuaikan lebar garis, pola dash, atau bahkan opacity.

---

## Langkah 6: Simpan PDF yang Dimodifikasi

Akhirnya, simpan perubahan Anda dengan **save modified pdf**. Anda dapat menimpa file asli atau menulis ke file baru—di sini kami akan membuat file output.

```csharp
// Save the updated PDF to a new location
pdfDocument.Save(@"C:\MyFiles\output.pdf");
```

Itulah seluruh alur kerja. Jalankan program dan buka `output.pdf`; Anda akan melihat persegi panjang hitam solid di tempat yang Anda definisikan.

---

## Contoh Lengkap yang Berfungsi

Berikut adalah aplikasi konsol mandiri yang menggabungkan semua langkah. Salin ke `.csproj` baru dan tekan **Run**.

```csharp
using System;
using System.Drawing;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;

namespace PdfRectangleDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load PDF document
            Document pdfDocument = new Document(@"C:\MyFiles\input.pdf");

            // 2️⃣ Get the first page (pages are 1‑based)
            Page firstPage = pdfDocument.Pages[1];

            // 3️⃣ Define the rectangle geometry
            Rectangle rect = new Rectangle(100, 100, 300, 300);

            // 4️⃣ Verify bounds
            if (firstPage.PageInfo.Width < rect.URX || firstPage.PageInfo.Height < rect.URY)
            {
                Console.WriteLine("Rectangle does not fit on the page.");
                return;
            }

            // 5️⃣ Add a black rectangle annotation
            firstPage.AddRectangle(rect, Color.Black);

            // 6️⃣ Save modified PDF
            pdfDocument.Save(@"C:\MyFiles\output.pdf");

            Console.WriteLine("Successfully drew rectangle on PDF and saved the file.");
        }
    }
}
```

**Output yang diharapkan** di konsol:

```
Successfully drew rectangle on PDF and saved the file.
```

Buka `output.pdf` dan Anda akan melihat persegi panjang hitam yang diposisikan pada koordinat yang Anda tentukan.

---

## Menangani Variasi Umum

| Situasi | Apa yang Diubah | Mengapa |
|-----------|----------------|-----|
| **Multiple pages** | Loop melalui `pdfDocument.Pages` dan terapkan logika yang sama pada setiap objek `Page`. | Memungkinkan anotasi batch di seluruh dokumen. |
| **Different colors** | Ganti `Color.Black` dengan `Color.Red` atau `System.Drawing.Color` apa pun. | Berguna untuk menyorot daripada menyensor. |
| **Transparent fill** | Gunakan `new Annotation(rect) { Color = Color.Black, Opacity = 0.5 }`. | Memberikan lapisan semi‑transparent alih-alih blok solid. |
| **Dynamic rectangle size** | Hitung `URX` dan `URY` berdasarkan `PageInfo.Width * 0.5` dll. | Membuat persegi panjang menyesuaikan dengan berbagai dimensi halaman. |
| **Error handling** | Bungkus seluruh blok dalam `try…catch` dan log `Aspose.Pdf.IOException`. | Mencegah crash ketika file sumber hilang atau terkunci. |

Penyesuaian ini menggambarkan bagaimana Anda dapat **create black rectangle** anotasi dalam banyak konteks tanpa menulis ulang logika inti.

---

## Tips Pro & Jebakan

- **Dispose the Document**: Meskipun Aspose.PDF mengimplementasikan `IDisposable`, pola `using` tidak wajib untuk aplikasi konsol yang berumur pendek. Pada layanan yang berjalan lama, bungkus `Document` dalam blok `using` untuk membebaskan sumber daya native dengan cepat.  
- **Coordinate System**: Koordinat PDF dimulai dari sudut lower‑left. Jika Anda terbiasa dengan asal top‑left (seperti WinForms), Anda perlu membalik sumbu Y: `pageHeight - y`.  
- **Performance**: Menambahkan anotasi ke PDF yang sangat besar dapat memakan banyak memori. Pertimbangkan memproses halaman secara bertahap atau menggunakan `PdfFileEditor` untuk edit yang lebih ringan.  
- **Legal**: Pastikan Anda memiliki hak untuk memodifikasi PDF sumber—beberapa dokumen dilindungi dari pengeditan.

---

## Kesimpulan

Kami baru saja mendemonstrasikan cara **draw rectangle on PDF** menggunakan C#—dimulai dari **load pdf document**, mendefinisikan geometri, **add black rectangle**, dan akhirnya **save modified pdf**. Contoh ini lengkap, dapat dijalankan, dan dapat disesuaikan untuk skenario dunia nyata seperti pemrosesan batch atau styling khusus.

Selanjutnya, Anda dapat menjelajahi penambahan tipe anotasi lain (teks, highlight) atau menggabungkan beberapa PDF setelah anotasi. Kedua langkah **load pdf document** dan **save modified pdf** tetap sama, sehingga Anda dapat memperluas pola ini dengan percaya diri.

Punya variasi yang Anda coba? Bagikan di komentar, dan selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang terkait erat yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan menjelajahi pendekatan implementasi alternatif dalam proyek Anda.

- [Buat Objek Persegi Panjang Terisi dalam PDF menggunakan Java](/pdf/english/java/pdf-images/create-filled-rectangle-object-in-pdf-using-java/)
- [Buat Objek Persegi Panjang Terisi dalam PDF Menggunakan Java](/pdf/german/java/pdf-images/create-filled-rectangle-object-in-pdf-using-java/)
- [Buat Objek Persegi Panjang Terisi dalam PDF Menggunakan Java](/pdf/french/java/pdf-images/create-filled-rectangle-object-in-pdf-using-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}