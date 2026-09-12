---
category: general
date: 2026-09-12
description: Pelajari cara menambahkan transparansi ke PDF, menggambar persegi panjang
  pada PDF, dan menyimpan PDF dengan transparansi menggunakan Aspose.PDF di C# – panduan
  langkah demi langkah.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add transparency to pdf
- draw rectangle on pdf
- save pdf with transparency
language: id
lastmod: 2026-09-12
og_description: Tambahkan transparansi ke PDF, gambar persegi panjang pada PDF, dan
  simpan PDF dengan transparansi menggunakan Aspose.PDF di C#. Ikuti tutorial lengkap
  ini.
og_image_alt: Screenshot of a PDF page showing a semi‑transparent rectangle drawn
  with Aspose.PDF
og_title: Tambahkan transparansi pada PDF dan gambar persegi panjang di PDF – panduan
  lengkap C#
schemas:
- author: Aspose
  dateModified: '2026-09-12'
  description: Learn how to add transparency to PDF, draw a rectangle on PDF, and
    save PDF with transparency using Aspose.PDF in C# – step‑by‑step guide.
  headline: How to add transparency to PDF and draw a rectangle on PDF with Aspose.PDF
  type: TechArticle
tags:
- Aspose.PDF
- C#
- PDF manipulation
title: Cara menambahkan transparansi pada PDF dan menggambar persegi panjang pada
  PDF dengan Aspose.PDF
url: /id/net/images-graphics/how-to-add-transparency-to-pdf-and-draw-a-rectangle-on-pdf-w/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara menambahkan transparansi ke PDF dan menggambar persegi panjang pada PDF dengan Aspose.PDF

Jika Anda perlu **menambahkan transparansi ke PDF** file, panduan ini menunjukkan secara tepat cara melakukannya di C#. Anda juga akan belajar cara **menggambar persegi panjang pada PDF** dan akhirnya **menyimpan PDF dengan transparansi** sehingga hasilnya dapat digunakan kembali dalam laporan, faktur, atau alur kerja otomatisasi dokumen apa pun.

Dalam tutorial ini Anda akan:

* Memuat dokumen PDF yang ada.
* Membuat keadaan grafik khusus yang mendefinisikan opacity garis tepi dan isi.
* Menerapkan keadaan grafik tersebut ke kanvas dan menggambar sebuah persegi panjang.
* Menyimpan file yang dimodifikasi sambil mempertahankan pengaturan transparansi.

Tidak ada alat eksternal yang diperlukan selain pustaka Aspose.PDF untuk .NET, dan setiap baris kode dijelaskan sehingga Anda memahami *mengapa* setiap langkah penting.

## Prasyarat

* .NET 6.0 atau lebih baru (kode juga berfungsi dengan .NET Framework 4.7+).
* Salinan berlisensi atau evaluasi dari **Aspose.PDF for .NET**. Instal melalui NuGet:

```bash
dotnet add package Aspose.Pdf
```

* Sebuah PDF input (`input.pdf`) yang ditempatkan dalam folder yang dapat Anda referensikan dari proyek Anda.

## Langkah 1: Memuat dokumen PDF

Operasi pertama adalah membuka file sumber. Menggunakan pernyataan `using` menjamin bahwa dokumen dibuang (disposed) dengan benar, yang mencegah masalah penguncian file nanti ketika Anda mencoba menyimpan.

```csharp
// Step 1: Load the PDF document
string pdfPath = @"YOUR_DIRECTORY\input.pdf";
using var pdfDocument = new Aspose.Pdf.Document(pdfPath);
```

*Mengapa ini penting*: Memuat dokumen memberi Anda akses ke koleksi halaman, kamus sumber daya, dan objek kanvas yang diperlukan untuk menggambar.

## Langkah 2: Mengakses kamus sumber daya halaman pertama

Setiap halaman PDF memiliki **kamus sumber daya** yang menyimpan objek seperti font, gambar, dan keadaan grafik. Untuk memperkenalkan pengaturan transparansi baru, kita perlu mengedit entri `ExtGState`.

```csharp
// Step 2: Access the first page and its resource dictionary
var firstPage = pdfDocument.Pages[1];               // PDF pages are 1‑based
var resourcesEditor = new Aspose.Pdf.DictionaryEditor(firstPage.Resources);
```

*Mengapa ini penting*: `DictionaryEditor` memungkinkan kami membaca dan memodifikasi objek PDF tingkat rendah tanpa merusak struktur dokumen.

## Langkah 3: Membuat keadaan grafik khusus dengan nilai transparansi

Keadaan grafik (`ExtGState`) mengontrol bagaimana operasi menggambar dirender. Kami mendefinisikan dua parameter opacity:

* **CA** – opacity garis tepi (garis luar bentuk).
* **ca** – opacity isi (bagian dalam bentuk).

Kami juga mengatur mode pencampuran (`BM`) ke “Normal”, yang merupakan operasi komposit paling umum.

```csharp
// Step 3: Create a custom graphics state (ExtGState) with transparency settings
var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
var customGs = Aspose.Pdf.Cos.CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

var parameters = new[]
{
    new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
        "CA", new Aspose.Pdf.Cos.CosPdfNumber(1)),          // stroke opacity = 100 %
    new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
        "ca", new Aspose.Pdf.Cos.CosPdfNumber(0.5)),        // fill opacity = 50 %
    new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
        "BM", new Aspose.Pdf.Cos.CosPdfName("Normal"))      // normal blend mode
};

foreach (var p in parameters)
    customGs.Add(p);

// Register the new graphics state under the name "GS0"
extGStateDict.Add("GS0", customGs);
```

*Mengapa ini penting*: Dengan menambahkan `GS0` ke kamus `ExtGState` kami membuat referensi yang dapat digunakan kembali yang dapat diaktifkan kanvas sebelum menggambar. Opacity isi `0.5` membuat persegi panjang menjadi semi‑transparan, mencapai tujuan **menambahkan transparansi ke PDF**.

## Langkah 4: Menerapkan keadaan grafik dan menggambar persegi panjang

Sekarang kami memberi tahu kanvas halaman untuk menggunakan keadaan grafik yang baru saja kami buat, kemudian kami menggambar sebuah persegi panjang. Koordinat mengikuti sistem koordinat PDF (asal di sudut kiri bawah).

```csharp
// Step 4: Apply the custom graphics state and draw a rectangle
var canvas = firstPage.Canvas;

// Activate the transparency graphics state
canvas.SetGraphicsState("GS0");

// Draw a rectangle from (100, 500) to (200, 600)
canvas.Rectangle(100, 500, 200, 600);

// Render the rectangle outline using the current graphics state
canvas.Stroke();
```

*Mengapa ini penting*: `SetGraphicsState("GS0")` mengubah konteks menggambar ke pengaturan transparansi yang didefinisikan sebelumnya. Metode `Rectangle` mendefinisikan bentuk, dan `Stroke` merender garis luar dengan opacity yang ditentukan. Jika Anda juga menginginkan persegi panjang terisi, ganti `Stroke()` dengan `FillAndStroke()`.

## Langkah 5: Menyimpan PDF yang dimodifikasi sambil mempertahankan transparansi

Akhirnya, tulis kembali dokumen ke disk. File output berisi keadaan grafik baru, persegi panjang yang digambar, dan informasi transparansi.

```csharp
// Step 5: Save the modified PDF
string outputPath = @"YOUR_DIRECTORY\output_with_extgstate.pdf";
pdfDocument.Save(outputPath);
```

*Mengapa ini penting*: Menyimpan dokumen menyelesaikan semua perubahan. File yang dihasilkan dapat dibuka di viewer PDF apa pun, dan persegi panjang akan muncul dengan opacity isi 50 %.

### Hasil yang diharapkan

Saat Anda membuka `output_with_extgstate.pdf` Anda akan melihat sebuah persegi panjang yang batasnya sepenuhnya opak dan interiornya semi‑transparan, memungkinkan konten halaman di bawahnya terlihat.

## Kasus tepi dan tip praktis

| Situasi | Penyesuaian yang disarankan |
|-----------|------------------------|
| **Beberapa halaman** | Loop over `pdfDocument.Pages` and repeat steps 2‑4 for each target page. |
| **Nilai opacity berbeda** | Change the `CosPdfNumber` values for `CA` (stroke) and `ca` (fill) to any number between `0` (fully transparent) and `1` (fully opaque). |
| **Mode pencampuran khusus** | Replace `"Normal"` with `"Multiply"`, `"Screen"`, or any PDF‑standard blend mode supported by your viewer. |
| **Persegi panjang terisi** | Call `canvas.FillAndStroke()` instead of `canvas.Stroke()` to apply both fill and outline. |
| **Menggunakan kembali keadaan grafik yang sama** | You can call `canvas.SetGraphicsState("GS0")` before drawing any number of shapes on the same page. |

**Tip pro:** Selalu periksa kamus sumber daya setelah menambahkan `ExtGState` baru. Jika kamus tidak ada, buat terlebih dahulu:

```csharp
if (!resourcesEditor.ContainsKey("ExtGState"))
    resourcesEditor.Add("ExtGState", new Aspose.Pdf.Cos.CosPdfDictionary(pdfDocument));
```

## Contoh lengkap yang dapat dijalankan

Berikut adalah program mandiri yang dapat Anda salin ke aplikasi konsol dan jalankan segera (ganti `YOUR_DIRECTORY` dengan jalur yang sebenarnya).

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Cos;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the PDF document
        string pdfPath = @"YOUR_DIRECTORY\input.pdf";
        using var pdfDocument = new Document(pdfPath);

        // 2️⃣ Access the first page’s resources
        var firstPage = pdfDocument.Pages[1];
        var resourcesEditor = new DictionaryEditor(firstPage.Resources);

        // Ensure ExtGState dictionary exists
        if (!resourcesEditor.ContainsKey("ExtGState"))
            resourcesEditor.Add("ExtGState", new CosPdfDictionary(pdfDocument));

        // 3️⃣ Create a custom graphics state with transparency
        var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
        var customGs = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

        var parameters = new[]
        {
            new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),   // stroke opacity
            new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // fill opacity
            new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
        };

        foreach (var p in parameters)
            customGs.Add(p);

        extGStateDict.Add("GS0", customGs);

        // 4️⃣ Apply the graphics state and draw a rectangle
        var canvas = firstPage.Canvas;
        canvas.SetGraphicsState("GS0");
        canvas.Rectangle(100, 500, 200, 600);
        canvas.Stroke(); // use FillAndStroke() for a filled shape

        // 5️⃣ Save the PDF with transparency
        string outputPath = @"YOUR_DIRECTORY\output_with_extgstate.pdf";
        pdfDocument.Save(outputPath);

        Console.WriteLine("PDF saved with a transparent rectangle at: " + outputPath);
    }
}
```

Menjalankan program menghasilkan `output_with_extgstate.pdf`, yang mendemonstrasikan **menambahkan transparansi ke PDF**, **menggambar persegi panjang pada PDF**, dan **menyimpan PDF dengan transparansi** semuanya dalam satu alur.

## Kesimpulan

Anda sekarang tahu cara **menambahkan transparansi ke PDF** file, **menggambar persegi panjang pada PDF**, dan **menyimpan PDF dengan transparansi** menggunakan Aspose.PDF untuk .NET. Proses ini berpusat pada pembuatan `ExtGState` khusus, menerapkannya ke kanvas, dan menyimpan perubahan. Dengan blok bangunan ini Anda dapat memperluas teknik ke bentuk lain, beberapa halaman, atau nilai opacity dinamis.

**Langkah selanjutnya**

* Jelajahi primitif menggambar lain seperti `canvas.Ellipse`, `canvas.Path`, atau `canvas.TextFragment` sambil menggunakan kembali keadaan grafik yang sama.
* Gabungkan transparansi dengan overlay gambar untuk membuat watermark (`canvas.Image` + `ExtGState` khusus).
* Tinjau dokumentasi Aspose.PDF tentang **parameter keadaan grafik** untuk efek komposit lanjutan.

Selamat coding, dan nikmati fleksibilitas visual yang dibawa transparansi ke alur kerja PDF Anda!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang terkait erat yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [How to Create PDF in C# – Add Page, Draw Rectangle & Save](/pdf/english/net/document-creation/how-to-create-pdf-in-c-add-page-draw-rectangle-save/)
- [How to Add a Line Object in PDF Using Aspose.PDF for .NET: A Step-by-Step Guide](/pdf/english/net/document-manipulation/add-line-aspose-pdf-dotnet-tutorial/)
- [Add Image Stamps to PDFs Using Aspose.PDF for .NET: A Step-by-Step Guide](/pdf/english/net/images-graphics/add-image-stamp-to-pdf-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}