---
category: general
date: 2026-04-06
description: Tambahkan persegi panjang ke PDF dengan cepat menggunakan C#. Pelajari
  cara menggambar persegi panjang pada PDF, memuat dokumen PDF menggunakan C#, dan
  menggunakan Aspose PDF untuk menggambar persegi panjang dalam tutorial langkah demi
  langkah ini.
draft: false
keywords:
- add rectangle to pdf
- draw rectangle on pdf
- draw shape in pdf
- load pdf document c#
- aspose pdf draw rectangle
language: id
og_description: Tambahkan persegi panjang ke PDF secara instan. Panduan ini menunjukkan
  cara menggambar persegi panjang pada PDF, memuat dokumen PDF dengan C#, dan menggunakan
  Aspose PDF untuk menggambar persegi panjang dengan contoh kode yang jelas.
og_title: Tambahkan Persegi Panjang ke PDF dengan C# – Tutorial Lengkap Aspose PDF
tags:
- Aspose.PDF
- C#
- PDF manipulation
title: Menambahkan Persegi Panjang ke PDF dengan C# – Panduan Lengkap Aspose PDF
url: /id/net/images-graphics/add-rectangle-to-pdf-with-c-full-aspose-pdf-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tambahkan Persegi Panjang ke PDF – Tutorial Lengkap Aspose PDF

Pernah perlu **menambahkan persegi panjang ke PDF** tetapi tidak yakin panggilan API mana yang tepat? Anda tidak sendirian; banyak pengembang mengalami hal ini saat mengotomatisasi laporan atau menyorot bagian dalam dokumen. Dalam panduan ini kami akan menjelaskan langkah‑langkah tepat untuk **menggambar persegi panjang pada PDF** menggunakan Aspose.PDF untuk .NET, dan Anda akan melihat contoh lengkap yang dapat dijalankan yang dapat Anda masukkan ke dalam proyek Anda.

Kami juga akan membahas cara **memuat dokumen PDF C#**, memverifikasi bahwa bentuk tersebut cocok dengan halaman, serta mendiskusikan beberapa jebakan umum ketika Anda mencoba **menggambar bentuk dalam PDF**. Pada akhir tutorial Anda akan memiliki program yang menambahkan persegi panjang kuning cerah ke halaman pertama dari PDF mana pun yang Anda pilih.

## Apa yang Anda Butuhkan

- .NET 6.0 atau lebih baru (kode ini juga bekerja dengan .NET Framework 4.6+)
- Paket NuGet Aspose.PDF untuk .NET (versi 23.11 atau lebih baru)
- File PDF contoh (`input.pdf`) yang ditempatkan di folder yang dapat Anda referensikan
- Visual Studio, VS Code, atau IDE C# apa pun yang Anda sukai

Tidak ada file konfigurasi tambahan, tidak ada COM interop, hanya beberapa pernyataan `using` dan beberapa baris logika.

## Langkah 1: Memuat Dokumen PDF C# – Menyiapkan File

Hal pertama yang harus Anda lakukan adalah membuka PDF yang sudah ada sehingga Anda memiliki sesuatu untuk digambar. Aspose.PDF membuat ini menjadi satu baris kode.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using System.Drawing;   // For Color

// Step 1: Load the PDF document
var inputPath = @"C:\MyPdfs\input.pdf";
using var pdfDocument = new Document(inputPath);
```

**Mengapa ini penting:**  
`Document` mewakili seluruh file PDF. Dengan membungkusnya dalam blok `using` kita memastikan handle file dilepaskan segera setelah selesai, mencegah masalah penguncian file di Windows. Jika Anda lupa menambahkan `using`, Anda mungkin akan melihat “cannot access the file because it is being used by another process” saat mencoba menyimpan.

## Langkah 2: Mengakses Halaman Target dan Memverifikasi Batas – Menggambar Bentuk dalam PDF dengan Aman

Sebelum Anda menempelkan persegi panjang ke halaman, Anda memerlukan objek halaman dan harus memastikan persegi panjang tersebut muat di dalam dimensi halaman. Ini mencegah pengecualian runtime dan menjaga PDF Anda tetap rapi.

```csharp
// Step 2: Get the first page (pages are 1‑based in Aspose)
Page firstPage = pdfDocument.Pages[1];

// Define rectangle bounds: lower‑left X/Y and upper‑right X/Y
var rectangleBounds = new Rectangle(50, 700, 200, 800);

// Verify the rectangle is inside the page limits
bool fits = rectangleBounds.LLX >= 0 &&
            rectangleBounds.URX <= firstPage.PageInfo.Width &&
            rectangleBounds.LLY >= 0 &&
            rectangleBounds.URY <= firstPage.PageInfo.Height;

if (!fits)
{
    throw new InvalidOperationException("Rectangle exceeds page dimensions.");
}
```

**Penjelasan:**  
Konstruktor `Rectangle` mengharapkan empat angka: X kiri‑bawah, Y kiri‑bawah, X kanan‑atas, Y kanan‑atas. Nilai‑nilai tersebut diukur dalam poin (1 pt ≈ 1/72 in). Langkah verifikasi adalah jaring pengaman kecil—terutama berguna ketika Anda menghitung koordinat secara dinamis (misalnya, berdasarkan ukuran gambar atau panjang teks).

## Langkah 3: Menambahkan Persegi Panjang ke PDF – Inti dari “Add Rectangle to PDF”

Sekarang bagian yang menyenangkan: benar‑benarnya menyisipkan bentuk. Aspose.PDF menyediakan kelas `RectangleShape` yang dapat Anda letakkan ke dalam koleksi `Paragraphs` halaman.

```csharp
// Step 3: Add a yellow rectangle shape
var rectangleShape = new RectangleShape(rectangleBounds)
{
    FillColor = Color.Yellow,
    Border = new BorderInfo(BorderSide.All, 1.0f, Color.Black) // Optional: thin black border
};

firstPage.Paragraphs.Add(rectangleShape);
```

**Mengapa menggunakan `RectangleShape`?**  
Ini adalah grafik vektor, sehingga persegi panjang dapat diskalakan dengan bersih pada perangkat apa pun. Menambahkannya ke `Paragraphs` berarti ia berperilaku seperti elemen konten lainnya—diposisikan relatif terhadap halaman, bukan terhadap teks yang ada. Jika Anda memerlukan isi transparan, cukup atur `FillColor = Color.Transparent`.

> **Tips pro:** Ubah `FillColor` menjadi `Color.FromArgb(128, 255, 255, 0)` untuk kuning semi‑transparan yang memungkinkan teks di bawahnya tetap terlihat.

## Langkah 4: Menyimpan PDF yang Telah Diperbarui – Menyelesaikan Siklus “Add Rectangle to PDF”

Setelah bentuk berada di tempatnya, Anda cukup menyimpan dokumen ke file baru (atau menimpa yang asli, jika Anda mau).

```csharp
// Step 4: Save the updated PDF
var outputPath = @"C:\MyPdfs\output.pdf";
pdfDocument.Save(outputPath);
```

Itu saja! Buka `output.pdf` dan Anda akan melihat persegi panjang kuning cerah yang pas berada di antara koordinat yang Anda tentukan.

## Contoh Program Lengkap – Semua Langkah dalam Satu File

Berikut adalah program lengkap yang dapat Anda kompilasi dan jalankan apa adanya. Program ini mencakup penanganan error dan komentar yang menjelaskan setiap baris.

```csharp
// ---------------------------------------------------------------
// AddRectangleToPdf.cs
// Demonstrates how to add rectangle to PDF using Aspose.PDF for .NET
// ---------------------------------------------------------------
using System;
using System.Drawing;               // For Color
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

class AddRectangleToPdf
{
    static void Main()
    {
        // ----- 1. Load the PDF document -----
        string inputPath = @"C:\MyPdfs\input.pdf";
        if (!System.IO.File.Exists(inputPath))
        {
            Console.WriteLine($"Input file not found: {inputPath}");
            return;
        }

        using var pdfDoc = new Document(inputPath);

        // ----- 2. Access first page and define rectangle bounds -----
        Page page = pdfDoc.Pages[1];
        var rect = new Rectangle(50, 700, 200, 800);

        // Verify rectangle fits the page
        bool fits = rect.LLX >= 0 && rect.URX <= page.PageInfo.Width &&
                    rect.LLY >= 0 && rect.URY <= page.PageInfo.Height;
        if (!fits)
        {
            Console.WriteLine("Rectangle exceeds page dimensions. Adjust coordinates.");
            return;
        }

        // ----- 3. Create and add rectangle shape -----
        var shape = new RectangleShape(rect)
        {
            FillColor = Color.Yellow,
            Border = new BorderInfo(BorderSide.All, 1.0f, Color.Black)
        };
        page.Paragraphs.Add(shape);

        // ----- 4. Save the modified PDF -----
        string outputPath = @"C:\MyPdfs\output.pdf";
        pdfDoc.Save(outputPath);
        Console.WriteLine($"Rectangle added successfully. Saved to {outputPath}");
    }
}
```

**Hasil yang diharapkan:**  
Saat Anda membuka `output.pdf`, halaman pertama akan menampilkan persegi panjang kuning yang sudut kiri‑bawahnya berada di (50 pt, 700 pt) dan sudut kanan‑atasnya di (200 pt, 800 pt). Persegi panjang tersebut akan memiliki batas hitam tipis, sehingga jelas terlihat di atas kebanyakan latar belakang.

## Pertanyaan Umum & Kasus Tepi

### Bagaimana jika saya perlu menggambar persegi panjang pada halaman yang berbeda?

Cukup ubah `pdfDoc.Pages[1]` ke nomor halaman yang diinginkan (`pdfDoc.Pages[3]` untuk halaman ketiga). Ingat bahwa Aspose menggunakan indeks berbasis 1, bukan berbasis 0.

### Bisakah saya menggambar beberapa persegi panjang dalam sebuah loop?

Tentu saja. Bungkus logika pembuatan persegi panjang dalam `foreach` yang iterasi atas koleksi koordinat. Hanya perhatikan performa; menambahkan ribuan bentuk dapat meningkatkan ukuran file secara signifikan.

### Bagaimana perbedaan dengan menggunakan `Graphics` atau `System.Drawing`?

`System.Drawing` bekerja dengan gambar raster; hasilnya tertanam dalam bitmap, yang dapat menjadi buram saat diperbesar. `RectangleShape` berbasis vektor, artinya tetap tajam pada tingkat zoom berapa pun—ideal untuk PDF profesional.

### Bagaimana jika PDF dilindungi kata sandi?

Muat dokumen dengan objek `PdfLoadOptions` yang menyertakan kata sandi:

```csharp
var loadOpts = new PdfLoadOptions { Password = "mySecret" };
using var pdfDoc = new Document(inputPath, loadOpts);
```

Kemudian lanjutkan seperti biasa. Persegi panjang akan ditambahkan setelah dokumen didekripsi di memori.

## Referensi Visual

![Contoh menambahkan persegi panjang ke PDF yang menampilkan bentuk kuning pada halaman pertama](/images/add-rectangle-to-pdf-example.png)

*Alt text: “contoh menambahkan persegi panjang ke pdf dengan persegi panjang kuning pada halaman pertama”*

Tangkapan layar memperlihatkan tepat apa yang dihasilkan oleh kode di atas—petunjuk visual yang jelas bahwa persegi panjang telah ditempatkan dengan benar.

## Ringkasan & Langkah Selanjutnya

Kami baru saja membahas cara **menambahkan persegi panjang ke PDF** menggunakan Aspose.PDF untuk .NET, mulai dari memuat dokumen hingga menyimpan file yang telah dimodifikasi. Poin penting yang harus diingat:

1. Muat PDF (`load pdf document c#`) dengan pembuangan yang tepat.
2. Tentukan batas persegi panjang dan verifikasi bahwa ia muat di halaman.
3. Gunakan `RectangleShape` untuk **menggambar persegi panjang pada pdf** (atau **menggambar bentuk dalam pdf** lainnya yang mungkin Anda perlukan).
4. Simpan hasilnya dan nikmati persegi panjang vektor yang tajam.

Siap untuk lebih lanjut? Coba ganti `RectangleShape` dengan `EllipseShape` atau `PolygonShape` untuk membuat sorotan khusus. Atau jelajahi kemampuan ekstraksi teks Aspose untuk menempatkan bentuk secara dinamis berdasarkan lokasi kata kunci. Library ini cukup kaya untuk memungkinkan Anda membangun alat anotasi lengkap tanpa pernah meninggalkan C#.

Jika Anda mengalami kendala, tinggalkan komentar di bawah—senang membantu. Dan jangan lupa memberi bintang pada paket NuGet Aspose.PDF jika Anda merasa itu berguna. Selamat coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}