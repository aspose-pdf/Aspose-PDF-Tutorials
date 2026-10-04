---
category: general
date: 2026-10-04
description: Pelajari cara mengubah transparansi PDF dengan Aspose.Pdf di C#. Panduan
  langkah demi langkah ini menambahkan keadaan grafis khusus untuk menyesuaikan opasitas
  dan mode pencampuran.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- change PDF transparency
- Aspose.Pdf graphics state
- PDF opacity C#
- ExtGState dictionary
- blend mode PDF
language: id
lastmod: 2026-10-04
og_description: Ubah transparansi PDF di C# menggunakan Aspose.Pdf. Ikuti tutorial
  singkat ini untuk memodifikasi opasitas, mode pencampuran, dan status grafis pada
  PDF Anda.
og_image_alt: Screenshot of a PDF page before and after changing transparency with
  Aspose.Pdf
og_title: Ubah transparansi PDF dengan Aspose.Pdf – panduan lengkap C#
schemas:
- author: Aspose
  dateModified: '2026-10-04'
  description: Learn how to change PDF transparency with Aspose.Pdf in C#. This step‑by‑step
    guide adds a custom graphics state to adjust opacity and blend mode.
  headline: How to change PDF transparency using Aspose.Pdf in C#
  type: TechArticle
tags:
- Aspose.Pdf
- C#
- PDF manipulation
- graphics state
title: Cara mengubah transparansi PDF menggunakan Aspose.Pdf di C#
url: /id/net/programming-with-operators/how-to-change-pdf-transparency-using-aspose-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara mengubah transparansi PDF menggunakan Aspose.Pdf di C#

Jika Anda perlu **mengubah transparansi PDF** dalam proyek .NET, panduan ini menunjukkan secara tepat cara melakukannya dengan Aspose.Pdf. Pada akhir tutorial Anda akan memiliki PDF di mana objek yang dipilih menggunakan opasitas dan mode campuran khusus, tanpa memerlukan alat eksternal apa pun.

Bekerja dengan opasitas PDF adalah kebutuhan umum untuk watermark, grafik overlay, atau efek visual halus. Langkah‑langkah di bawah ini mencakup semua yang Anda perlukan—mulai dari memuat dokumen hingga mengedit **dictionary ExtGState**, membuat keadaan grafik baru, dan menyimpan hasilnya.

## Prerequisites

Sebelum Anda memulai, pastikan Anda memiliki:

* **Aspose.Pdf for .NET** (versi 23.12 atau lebih baru). Anda dapat menginstalnya melalui NuGet:

```bash
dotnet add package Aspose.Pdf
```

* Lingkungan pengembangan .NET (Visual Studio, VS Code, atau `dotnet` CLI).
* File PDF input yang berada di direktori yang diketahui (contoh menggunakan `input.pdf`).

Tidak ada pustaka tambahan yang diperlukan.

## Step 1: Load the PDF document

Operasi pertama adalah membuka PDF yang sudah ada. Menggunakan blok `using` menjamin bahwa handle file akan dilepaskan secara otomatis.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Cos;
using Aspose.Pdf.Tools;

// ...

using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
{
    // Subsequent steps go here
}
```

*Why this matters*: Memuat dokumen membuat representasi dalam memori yang dapat Anda modifikasi. Kelas `Document` juga memberi Anda akses ke objek COS tingkat rendah, yang penting untuk mengubah transparansi PDF.

## Step 2: Access the first page’s resources

Keadaan grafik disimpan dalam dictionary sumber daya halaman. Kami mengambil halaman pertama dan membungkus sumber dayanya dengan `DictionaryEditor` sehingga dapat diedit dengan mudah.

```csharp
var firstPage = pdfDocument.Pages[1];
var resourcesEditor = new DictionaryEditor(firstPage.Resources);
```

*Explanation*: `DictionaryEditor` mengabstraksi penanganan dictionary COS, memungkinkan Anda membaca dan menulis entri seperti `ExtGState` tanpa berurusan dengan sintaks PDF mentah.

## Step 3: Get (or create) the ExtGState dictionary

**Dictionary ExtGState** menyimpan objek keadaan grafik yang bernama. Jika sudah ada, kami menggunakannya kembali; jika tidak, kami membuat yang baru.

```csharp
CosPdfDictionary extGStateDict;

// Try to fetch an existing ExtGState entry
if (resourcesEditor.ContainsKey("ExtGState"))
{
    extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
}
else
{
    // Create a fresh ExtGState dictionary and add it to the resources
    extGStateDict = new CosPdfDictionary(pdfDocument);
    resourcesEditor["ExtGState"] = extGStateDict;
}
```

*Why this step*: Tanpa entri `ExtGState` mesin PDF tidak memiliki tempat untuk mencari pengaturan opasitas khusus. Menambahkan dictionary membuat halaman menyadari setiap keadaan grafik baru yang Anda definisikan.

## Step 4: Define a new graphics state with opacity and blend mode

Keadaan grafik adalah kumpulan parameter rendering PDF. Di sini kami menetapkan:

* **CA** – opasitas garis (1 = sepenuhnya opak)
* **ca** – opasitas isi (0.5 = 50 % transparan)
* **BM** – mode campuran (`Normal` adalah default, tetapi Anda dapat bereksperimen dengan `Multiply`, `Screen`, dll.)

```csharp
// Create an empty dictionary that will become the new graphics state
var graphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

// Prepare the entries
var graphicsStateEntries = new KeyValuePair<string, ICosPdfPrimitive>[]
{
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),   // stroke opacity
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // fill opacity
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // blend mode
};

// Populate the dictionary
foreach (var entry in graphicsStateEntries)
{
    graphicsState.Add(entry);
}
```

*Insight*: Nilai `CosPdfNumber` adalah angka floating‑point antara 0 dan 1. Mengubahnya memungkinkan Anda menyesuaikan seberapa transparan garis dan isi muncul. Mode campuran menentukan bagaimana konten transparan berinteraksi dengan grafik di bawahnya.

## Step 5: Register the graphics state in ExtGState

Kami memberi nama pada keadaan baru (`GS0`). Nanti, ketika Anda menggambar objek, Anda akan merujuk nama ini dalam aliran konten.

```csharp
extGStateDict.Add("GS0", graphicsState); // "GS0" becomes the identifier you’ll use later
```

*Best practice*: Gunakan konvensi penamaan yang jelas (`GS0`, `GS_Watermark`, dll.) sehingga Anda dapat mengelola banyak keadaan tanpa kebingungan.

## Step 6: Apply the graphics state to page content (optional)

Jika Anda ingin menerapkan opasitas baru pada elemen halaman yang sudah ada, Anda perlu memodifikasi aliran konten halaman. Berikut contoh sederhana yang menambahkan persegi panjang semi‑transparan di atas halaman.

```csharp
// Build a content stream that sets the graphics state and draws a rectangle
var contentBuilder = new Aspose.Pdf.Operators.ContentBuilder(pdfDocument);
contentBuilder.SetGraphicsState("GS0");
contentBuilder.SetFillColor(Color.FromRgb(255, 0, 0)); // red fill
contentBuilder.Rectangle(100, 500, 200, 100); // x, y, width, height
contentBuilder.FillPath();

firstPage.Contents.Add(contentBuilder);
```

*Why it works*: Operator `SetGraphicsState` memberi tahu interpreter PDF untuk menggunakan parameter yang didefinisikan dalam `GS0` untuk semua perintah menggambar berikutnya. Persegi panjang tersebut muncul dengan opasitas isi 50 % sementara garisnya tetap sepenuhnya opak.

## Step 7: Save the modified PDF

Akhirnya, tulis perubahan kembali ke disk.

```csharp
pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
```

PDF `output.pdf` yang dihasilkan berisi keadaan grafik baru, dan setiap konten yang merujuk `GS0` akan dirender dengan transparansi yang telah ditentukan.

---

![Diagram showing PDF transparency change](/images/pdf-transparency-before-after.png "PDF page before and after applying custom graphics state")
*Image alt text (for SEO and accessibility):* **contoh mengubah transparansi PDF – halaman asli vs. halaman yang dimodifikasi**

## Full working example

Menggabungkan semua langkah, berikut adalah program tunggal yang dapat dijalankan untuk mengubah transparansi PDF dan menambahkan persegi panjang semi‑transparan.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Cos;
using Aspose.Pdf.Tools;
using System.Collections.Generic;
using Aspose.Pdf.Operators;
using Aspose.Pdf.Drawing;

class ChangePdfTransparency
{
    static void Main()
    {
        // Load the source PDF
        using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
        {
            // Access first page resources
            var firstPage = pdfDocument.Pages[1];
            var resourcesEditor = new DictionaryEditor(firstPage.Resources);

            // Ensure ExtGState dictionary exists
            CosPdfDictionary extGStateDict;
            if (resourcesEditor.ContainsKey("ExtGState"))
                extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
            else
            {
                extGStateDict = new CosPdfDictionary(pdfDocument);
                resourcesEditor["ExtGState"] = extGStateDict;
            }

            // Create a new graphics state (opacity + blend mode)
            var graphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            var entries = new[]
            {
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
            };
            foreach (var e in entries) graphicsState.Add(e);

            // Register the graphics state as GS0
            extGStateDict.Add("GS0", graphicsState);

            // OPTIONAL: draw a semi‑transparent rectangle using GS0
            var builder = new ContentBuilder(pdfDocument);
            builder.SetGraphicsState("GS0");
            builder.SetFillColor(Color.FromRgb(255, 0, 0)); // red
            builder.Rectangle(100, 500, 200, 100);
            builder.FillPath();
            firstPage.Contents.Add(builder);

            // Save the result
            pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
        }

        Console.WriteLine("PDF transparency changed and saved to output.pdf");
    }
}
```

### Expected output

* File `output.pdf` dibuat di folder yang ditentukan.
* Jika Anda membuka PDF, Anda akan melihat persegi panjang merah dengan isi 50 % transparan sementara batasnya tetap sepenuhnya opak.
* Objek lain yang merujuk `GS0` (misalnya watermark) akan mewarisi opasitas dan mode campuran yang sama.

## Common questions & edge‑case handling

| Question | Answer |
|----------|--------|
| **Can I change only the stroke opacity?** | Set `CA` ke nilai yang diinginkan dan biarkan `ca` tetap `1`. |
| **What blend modes are supported?** | Semua mode campuran PDF standar (`Normal`, `Multiply`, `Screen`, `Overlay`, dll.) diterima melalui entri `BM`. |
| **Do I need to clean up the dictionary after use?** | Tidak. Objek `CosPdfDictionary` dikelola oleh Aspose.Pdf dan ditulis ke file saat Anda memanggil `Save`. |
| **How does this work with encrypted PDFs?** | Muat dokumen dengan kata sandi yang tepat (`new Document(path, password)`). Manipulasi keadaan‑grafik bekerja sama setelah dokumen didekripsi di memori. |
| **Is it possible to apply the same graphics state to multiple pages?** | Ya. Tambahkan entri `GS0` ke setiap `ExtGState` dictionary halaman, atau buat satu dictionary bersama di sumber daya global dokumen dan referensikan dari setiap halaman. |

## Tips and best practices

* **Pro tip:** Simpan nama keadaan‑grafik pendek namun deskriptif (`GS_Watermark`, `GS_Overlay`). Ini menghindari bentrok nama dan memudahkan debugging.
* **Watch out for:** Menimpa entri `ExtGState` yang sudah ada secara tidak sengaja. Selalu periksa `resourcesEditor.ContainsKey("ExtGState")` sebelum membuat dictionary baru.
* **Performance note:** Memodifikasi objek COS tingkat rendah cepat, tetapi jika Anda harus memproses ribuan halaman pertimbangkan melakukan batch perubahan untuk mengurangi tekanan memori.

## Next steps

Sekarang Anda tahu cara **mengubah transparansi PDF**, Anda dapat menjelajahi topik terkait seperti:

* Menambahkan **watermark** dengan opasitas khusus (`PDF opacity C#`).
* Menggunakan **mode campuran** berbeda untuk mencapai efek artistik (`blend mode PDF`).
* Membuat **perpustakaan keadaan grafik** yang dapat digunakan kembali untuk pembuatan dokumen skala besar (`Aspose.Pdf graphics state`).

Bereksperimenlah dengan mengubah nilai `ca` dan `CA`, atau ganti persegi panjang merah dengan gambar atau overlay teks. Prinsip yang sama berlaku—cukup referensikan keadaan grafik `GS0` sebelum menggambar konten baru.

---

*Anda telah mempelajari cara mengubah transparansi PDF menggunakan Aspose.Pdf di C#. Terapkan teknik ini untuk meningkatkan laporan, faktur, atau output berbasis PDF apa pun di mana nuansa visual penting.*

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber daya menyertakan contoh kode lengkap dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Ubah Opasitas PDF dengan Aspose.PDF – Panduan Lengkap C#](/pdf/english/net/programming-with-stamps-and-watermarks/change-pdf-opacity-with-aspose-pdf-complete-c-guide/)
- [Ubah Opasitas PDF di C# – Panduan Lengkap Aspose](/pdf/english/net/programming-with-stamps-and-watermarks/change-pdf-opacity-in-c-complete-aspose-guide/)
- [Tambahkan Transparansi ke PDF menggunakan Aspose – Panduan Lengkap C#](/pdf/english/net/programming-with-operators/add-transparency-to-pdf-using-aspose-complete-c-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}