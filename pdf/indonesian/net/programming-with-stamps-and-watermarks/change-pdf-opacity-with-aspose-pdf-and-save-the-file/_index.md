---
category: general
date: 2026-11-12
description: Pelajari cara mengubah opasitas PDF menggunakan Aspose.Pdf, menambahkan
  transparansi, mengatur mode pencampuran, dan menyimpan PDF yang dimodifikasi dalam
  C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- change PDF opacity
- how to add transparency
- save modified PDF
- how to set blend mode
- set fill opacity
language: id
lastmod: 2026-11-12
og_description: Ubah opasitas PDF dengan Aspose.Pdf, pelajari cara menambahkan transparansi,
  mengatur mode pencampuran, dan menyimpan file PDF yang dimodifikasi dalam C#.
og_image_alt: Screenshot of a PDF page with altered opacity using Aspose.Pdf
og_title: Ubah opasitas PDF dengan Aspose.Pdf – tambahkan transparansi dan simpan
schemas:
- author: Aspose
  dateModified: '2026-11-12'
  description: Learn how to change PDF opacity using Aspose.Pdf, add transparency,
    set blend mode, and save modified PDF in C#.
  headline: Change PDF opacity with Aspose.Pdf and save the file
  type: TechArticle
- description: Learn how to change PDF opacity using Aspose.Pdf, add transparency,
    set blend mode, and save modified PDF in C#.
  name: Change PDF opacity with Aspose.Pdf and save the file
  steps:
  - name: Load the PDF document
    text: Start by creating a `Document` instance that points to your source file.
      The constructor reads the entire PDF into memory, allowing you to manipulate
      its internal objects.
  - name: Access the first page’s resources
    text: Each PDF page stores a *resource dictionary* that holds objects such as
      fonts, images, and graphics states. You need to edit this dictionary to inject
      a new `ExtGState` entry.
  - name: Ensure an ExtGState dictionary exists
    text: The `ExtGState` dictionary holds custom graphics states. If it does not
      exist, the code creates one automatically.
  - name: Define a new graphics state (ExtGState)
    text: A graphics state defines how drawing operations behave. The following dictionary
      sets stroke opacity (`CA`), fill opacity (`ca`), and blend mode (`BM`).
  - name: Register the graphics state in the resource dictionary
    text: Give the new state a name (e.g., `GS0`) and add it to the `ExtGState` dictionary.
      This name will be referenced later in the page content stream.
  - name: Apply the graphics state to page content
    text: To actually see the opacity effect, insert the `/GS0 gs` operator before
      the drawing commands you want to affect. The example below draws a semi‑transparent
      rectangle.
  - name: Save the modified PDF
    text: Finally, write the updated document to disk. The `Save` method overwrites
      the target file or creates a new one if it does not exist.
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Ubah Opasitas PDF dengan Aspose.Pdf dan Simpan File
url: /id/net/programming-with-stamps-and-watermarks/change-pdf-opacity-with-aspose-pdf-and-save-the-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ubah Opasitas PDF dengan Aspose.Pdf dan Simpan File

Jika Anda perlu **mengubah opasitas PDF** dalam sebuah dokumen, Aspose.Pdf menyediakan API yang sederhana untuk menyesuaikan transparansi stroke dan fill. Tutorial ini menunjukkan secara tepat **cara menambahkan transparansi**, **cara mengatur mode campuran**, dan **menyimpan file PDF yang dimodifikasi** dengan hanya beberapa baris kode C#.

Anda akan melewati setiap langkah—dari memuat PDF yang ada hingga mendefinisikan state grafis baru dan menyimpan perubahan. Pada akhir panduan ini Anda dapat:

* Mengurangi visibilitas grafik vektor atau gambar.
* Menerapkan mode campuran khusus seperti *Normal* atau *Multiply*.
* Mengekspor file yang diperbarui tanpa kehilangan konten lainnya.

Satu-satunya prasyarat adalah lingkungan pengembangan .NET yang berfungsi dan referensi ke pustaka Aspose.Pdf (versi 23.9 atau lebih baru). Tidak diperlukan alat eksternal.

## Prasyarat

| Persyaratan | Mengapa penting |
|-------------|-----------------|
| .NET 6.0 SDK atau lebih baru | Menjamin kompatibilitas dengan API Aspose.Pdf terbaru. |
| Paket NuGet Aspose.Pdf untuk .NET | Menyediakan kelas `Document`, `CosPdfDictionary`, dan kelas terkait yang digunakan dalam kode. |
| File PDF untuk diedit (mis., `input.pdf`) | Berfungsi sebagai sumber untuk perubahan opasitas. |

Instal paket NuGet dengan:

```bash
dotnet add package Aspose.Pdf
```

## Ubah Opasitas PDF dengan Aspose.Pdf

### Langkah 1: Muat dokumen PDF

Mulailah dengan membuat instance `Document` yang menunjuk ke file sumber Anda. Konstruktor membaca seluruh PDF ke dalam memori, memungkinkan Anda memanipulasi objek internalnya.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Operators;
using Aspose.Pdf.XObjects;
using Aspose.Pdf.Facades;

// Load the existing PDF
var pdfDoc = new Document(@"YOUR_DIRECTORY\input.pdf");
```

> **Mengapa langkah ini?** Memuat file membuat model objek yang dapat dimanipulasi. Semua perubahan berikutnya beroperasi pada representasi dalam‑memori ini, memastikan file asli tetap tidak tersentuh sampai Anda secara eksplisit menyimpannya.

### Langkah 2: Akses sumber daya halaman pertama

Setiap halaman PDF menyimpan *kamus sumber daya* yang berisi objek seperti font, gambar, dan state grafis. Anda perlu mengedit kamus ini untuk menyisipkan entri `ExtGState` baru.

```csharp
// Retrieve the first page (pages are 1‑based)
var page = pdfDoc.Pages[1];

// The DictionaryEditor simplifies access to the page's resource dictionary
var resourcesEditor = new DictionaryEditor(page.Resources);
```

> **Tip:** Jika PDF Anda berisi beberapa halaman yang memerlukan opasitas yang sama, ulangi langkah ini untuk setiap halaman atau bagikan satu `ExtGState` di seluruh halaman.

### Langkah 3: Pastikan kamus ExtGState ada

Kamus `ExtGState` menyimpan state grafis khusus. Jika tidak ada, kode akan membuatnya secara otomatis.

```csharp
// Get or create the ExtGState dictionary
var extGStateDict = resourcesEditor["ExtGState"]?.ToCosPdfDictionary()
                     ?? new CosPdfDictionary(pdfDoc);
resourcesEditor["ExtGState"] = extGStateDict;
```

> **Mengapa langkah ini?** Tanpa kontainer `ExtGState`, setiap upaya merujuk ke state grafis baru akan gagal, menghasilkan PDF yang mengabaikan pengaturan opasitas Anda.

### Langkah 4: Definisikan state grafis baru (ExtGState)

State grafis mendefinisikan bagaimana operasi menggambar berperilaku. Kamus berikut mengatur opasitas stroke (`CA`), opasitas fill (`ca`), dan mode campuran (`BM`).

```csharp
// Create an empty dictionary for the new graphics state
var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDoc);

// Set desired parameters
var parameters = new[]
{
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),   // Stroke opacity (1 = opaque)
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // Fill opacity (0.5 = 50% transparent)
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // Blend mode
};

foreach (var param in parameters)
    newGraphicsState.Add(param);
```

> **Cara mengatur opasitas fill:** Entri `ca` mengontrol opasitas bentuk yang diisi (teks, jalur). Sesuaikan nilai numerik antara `0` (sepenuhnya transparan) dan `1` (sepenuhnya opak) untuk memenuhi kebutuhan desain Anda.  
> **Cara mengatur mode campuran:** Entri `BM` memilih algoritma komposit. Nilai umum meliputi `Normal`, `Multiply`, `Screen`, dan `Overlay`. Pilih yang sesuai dengan maksud visual Anda.

### Langkah 5: Daftarkan state grafis dalam kamus sumber daya

Berikan state baru nama (mis., `GS0`) dan tambahkan ke kamus `ExtGState`. Nama ini akan direferensikan nanti dalam aliran konten halaman.

```csharp
// Add the graphics state with a symbolic name
extGStateDict.Add("GS0", newGraphicsState);
```

> **Pro tip:** Gunakan konvensi penamaan seperti `GS0`, `GS1`, … saat Anda membuat beberapa state. Ini mencegah bentrok nama dan memudahkan debugging.

### Langkah 6: Terapkan state grafis ke konten halaman

Untuk benar-benar melihat efek opasitas, sisipkan operator `/GS0 gs` sebelum perintah menggambar yang ingin Anda pengaruhi. Contoh di bawah menggambar persegi panjang semi‑transparan.

```csharp
// Build a content stream that uses the new graphics state
var content = new MemoryStream();
var writer = new StreamWriter(content);

// Activate the graphics state
writer.WriteLine("q");                 // Save graphics state
writer.WriteLine("/GS0 gs");           // Apply custom ExtGState
writer.WriteLine("0.2 0.5 0.8 rg");    // Set fill color (RGB)
writer.WriteLine("100 500 200 100 re"); // Rectangle (x y width height)
writer.WriteLine("f");                 // Fill rectangle
writer.WriteLine("Q");                 // Restore graphics state
writer.Flush();

content.Position = 0;
page.Contents.Add(new ContentStream(content));
```

> **Mengapa operator `q` dan `Q`?** Mereka menambah dan mengurangi stack state grafis, memastikan perubahan opasitas hanya memengaruhi persegi panjang dan bukan seluruh halaman.

### Langkah 7: Simpan PDF yang dimodifikasi

Akhirnya, tulis dokumen yang diperbarui ke disk. Metode `Save` menimpa file target atau membuat yang baru jika belum ada.

```csharp
// Persist the changes
pdfDoc.Save(@"YOUR_DIRECTORY\output.pdf");
```

> **Cara menyimpan PDF yang dimodifikasi:** Pemanggilan `Save` menulis semua modifikasi dalam memori, termasuk `ExtGState` baru, ke jalur yang ditentukan. Anda juga dapat mengalirkan hasilnya ke `MemoryStream` untuk respons web.

## Contoh lengkap yang berfungsi

Berikut adalah program tunggal yang berdiri sendiri yang menggabungkan setiap langkah yang dijelaskan di atas. Salin ke aplikasi konsol dan jalankan untuk memverifikasi perubahan opasitas.

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.XObjects;
using Aspose.Pdf.Facades;
using Aspose.Pdf.Operators;

class ChangePdfOpacityDemo
{
    static void Main()
    {
        // 1. Load the PDF
        var pdfDoc = new Document(@"YOUR_DIRECTORY\input.pdf");

        // 2. Get first page and its resources
        var page = pdfDoc.Pages[1];
        var resourcesEditor = new DictionaryEditor(page.Resources);

        // 3. Ensure ExtGState dictionary exists
        var extGStateDict = resourcesEditor["ExtGState"]?.ToCosPdfDictionary()
                             ?? new CosPdfDictionary(pdfDoc);
        resourcesEditor["Ext


## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang terkait erat yang membangun pada teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Cara menyimpan PDF yang dimodifikasi dengan Aspose.Pdf dan menambahkan transparansi](/pdf/english/net/document-manipulation/how-to-save-modified-pdf-with-aspose-pdf-and-add-transparenc/)
- [Cara menambahkan transparansi ke PDF menggunakan Aspose.PDF dalam C#](/pdf/english/net/images-graphics/how-to-add-transparency-to-pdf-using-aspose-pdf-in-c/)
- [Cara menambahkan state grafis PDF dan mengontrol transparansi dengan Aspose.PDF](/pdf/english/net/images-graphics/how-to-add-graphics-state-pdf-and-control-transparency-with/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}