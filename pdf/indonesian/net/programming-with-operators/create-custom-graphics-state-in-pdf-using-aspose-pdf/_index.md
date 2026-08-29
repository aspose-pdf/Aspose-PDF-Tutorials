---
category: general
date: 2026-08-20
description: Buat state grafik khusus dalam PDF dengan Aspose.Pdf. Pelajari cara mengedit
  sumber daya PDF dan menambahkan transparansi PDF dalam beberapa langkah saja.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create custom graphics state
- edit pdf resources
- add transparency pdf
- Aspose.Pdf graphics state
- PDF resource dictionary
language: id
lastmod: 2026-08-20
og_description: Buat state grafis khusus dalam PDF dengan Aspose.Pdf. Tutorial ini
  menunjukkan cara mengedit sumber daya PDF dan menambahkan transparansi PDF dengan
  cepat.
og_image_alt: Screenshot of C# code that creates a custom graphics state in a PDF
og_title: Buat keadaan grafik khusus di PDF – Panduan Aspose.Pdf
schemas:
- author: Aspose
  dateModified: '2026-08-20'
  description: Create custom graphics state in PDF with Aspose.Pdf. Learn how to edit
    PDF resources and add transparency PDF in just a few steps.
  headline: Create custom graphics state in PDF using Aspose.Pdf
  type: TechArticle
tags:
- PDF
- Aspose.Pdf
- C#
- Graphics state
title: Buat keadaan grafik khusus dalam PDF menggunakan Aspose.Pdf
url: /id/net/programming-with-operators/create-custom-graphics-state-in-pdf-using-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat custom graphics state dalam PDF menggunakan Aspose.Pdf

Jika Anda perlu **membuat custom graphics state** dalam PDF, panduan ini menunjukkan secara tepat cara melakukannya dengan Aspose.Pdf untuk .NET. Pada akhir tutorial Anda akan dapat **mengedit sumber daya PDF**, menyisipkan kamus graphics‑state baru, dan **menambahkan konten transparansi PDF** tanpa meninggalkan proyek C# Anda.

Anda akan melihat contoh lengkap yang dapat dijalankan, penjelasan mengapa setiap baris penting, serta tips untuk menangani dokumen multi‑halaman atau mode blend yang berbeda. Tidak diperlukan alat eksternal—hanya pustaka Aspose.Pdf dan lingkungan pengembangan .NET dasar.

## Prasyarat

Sebelum Anda mulai, pastikan Anda memiliki:

* .NET 6.0 atau lebih baru (kode juga berfungsi dengan .NET Framework 4.7+)
* Salinan berlisensi **Aspose.Pdf for .NET** (versi trial gratis dapat digunakan untuk pengujian)
* File PDF input bernama `input.pdf` yang ditempatkan di folder yang dapat Anda referensikan dari kode
* Visual Studio 2022 atau IDE apa pun yang mendukung pengembangan C#

Tutorial ini mengasumsikan Anda sudah familiar dengan sintaks dasar C# dan konsep halaman PDF.

## Langkah 1: Muat PDF sumber dan akses halaman pertama

Operasi pertama adalah membuka file PDF dan mengambil halaman yang sumber dayanya ingin Anda modifikasi. Aspose.Pdf merepresentasikan setiap halaman sebagai objek `Page`, dan setiap halaman berisi **kamus sumber daya** yang menyimpan graphics states, font, XObjects, dan lainnya.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Operators;
using Aspose.Pdf.InteractiveFeatures;
using Aspose.Pdf.Text;
using Aspose.Pdf.Facades;
using System.Collections.Generic;

// Load the PDF you want to edit
using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
{
    // Get the first page (pages are 1‑based in Aspose.Pdf)
    Page firstPage = pdfDocument.Pages[1];
```

*Mengapa ini penting:* Kelas `Document` memuat file ke memori, dan `Pages[1]` memberi Anda akses langsung ke kamus sumber daya halaman pertama, tempat graphics state berada.

## Langkah 2: Buka kamus sumber daya untuk diedit

Aspose.Pdf menyediakan pembantu `DictionaryEditor` yang memungkinkan Anda memperlakukan kamus sumber daya seperti `Dictionary` .NET biasa. Ini memudahkan untuk membaca, menambah, atau mengganti entri seperti `ExtGState`.

```csharp
    // Create an editor for the page’s resources
    var resourcesEditor = new DictionaryEditor(firstPage.Resources);
```

*Mengapa ini penting:* `DictionaryEditor` mengabstraksi objek COS level rendah, memungkinkan Anda bekerja dengan pasangan kunci/nilai yang familiar sambil tetap menjaga kepatuhan PDF.

## Langkah 3: Ambil (atau buat) kamus ExtGState

Entri **ExtGState** menyimpan semua objek graphics‑state eksternal untuk halaman. Jika kamus tidak ada, Aspose.Pdf akan membuat kamus kosong untuk Anda.

```csharp
    // Ensure the ExtGState dictionary exists
    var extGStateDict = resourcesEditor.ContainsKey("ExtGState")
        ? resourcesEditor["ExtGState"].ToCosPdfDictionary()
        : new CosPdfDictionary(pdfDocument);
```

*Mengapa ini penting:* Entri `ExtGState` yang hilang akan menyebabkan `KeyNotFoundException` nanti. Penjagaan ini memungkinkan kode bekerja pada PDF yang belum pernah mendefinisikan custom graphics state sebelumnya—bagian penting dari ketahanan **edit PDF resources**.

## Langkah 4: Bangun kamus custom graphics state

Graphics state mendeskripsikan bagaimana operasi menggambar dirender. Untuk **menambahkan transparansi PDF**, Anda perlu mengatur entri `ca` (opacity isi) dan `CA` (opacity garis), serta opsional mode blend (`BM`). Kode berikut membangun kamus baru dengan parameter tersebut.

```csharp
    // Create an empty dictionary that will become the new graphics state
    var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

    // Define the parameters you want for the custom state
    var graphicsStateParams = new KeyValuePair<string, ICosPdfPrimitive>[]
    {
        // Stroke opacity (1 = fully opaque)
        new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
        // Fill opacity (0.5 = 50 % transparent)
        new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
        // Blend mode – "Normal" is the default, but you can use "Multiply", "Screen", etc.
        new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
    };

    // Populate the dictionary with the parameters
    foreach (var param in graphicsStateParams)
        newGraphicsState.Add(param);
```

*Mengapa ini penting:* Entri `ca` dan `CA` mengontrol transparansi untuk operasi isi dan garis, masing‑masing. Menetapkan `BM` memungkinkan Anda bereksperimen dengan efek komposit yang berbeda, yang berguna ketika Anda kemudian **menambahkan konten transparansi PDF** seperti bentuk atau gambar semi‑transparan.

## Langkah 5: Daftarkan graphics state baru dengan nama unik

Setiap graphics state dalam kamus `ExtGState` harus memiliki nama unik (misalnya, `GS0`, `GS1`). Anda dapat memilih nama apa saja yang tidak bentrok dengan entri yang ada.

```csharp
    // Choose a name that is unlikely to collide with existing states
    const string graphicsStateName = "GS0";

    // Add the new graphics state to the ExtGState dictionary
    extGStateDict.Add(graphicsStateName, newGraphicsState);

    // If the ExtGState entry was missing, attach it back to the page resources
    if (!resourcesEditor.ContainsKey("ExtGState"))
        resourcesEditor["ExtGState"] = extGStateDict;
```

*Mengapa ini penting:* Dengan menyisipkan kamus baru di bawah `GS0`, Anda membuat state dapat diakses dari aliran konten halaman. Blok kondisional memastikan entri `ExtGState` ada bahkan untuk PDF yang awalnya tidak memilikinya—perlindungan tambahan **edit PDF resources**.

## Langkah 6: Gunakan custom graphics state dalam konten halaman (opsional)

Langkah‑langkah sebelumnya hanya *mendefinisikan* graphics state. Untuk benar‑benar melihat efeknya, Anda harus merujuknya dalam aliran konten halaman. Berikut contoh singkat yang menggambar persegi panjang semi‑transparan menggunakan state yang baru saja dibuat.

```csharp
    // Get the page’s content stream (or create a new one if empty)
    var content = firstPage.Contents[1];
    var graphics = new ContentWriter(content);

    // Save current graphics state
    graphics.WriteOperator(OperatorName.SaveState);
    // Set the custom graphics state we just defined
    graphics.WriteOperand($"/{graphicsStateName}");
    graphics.WriteOperator(OperatorName.SetExtGState);
    // Draw a rectangle (coordinates are in points)
    graphics.WriteOperand(100);   // lower‑left x
    graphics.WriteOperand(500);   // lower‑left y
    graphics.WriteOperand(200);   // width
    graphics.WriteOperand(100);   // height
    graphics.WriteOperator(OperatorName.Rectangle);
    // Fill the rectangle using the current fill opacity (ca = 0.5)
    graphics.WriteOperator(OperatorName.Fill);
    // Restore the previous graphics state
    graphics.WriteOperator(OperatorName.RestoreState);
```

*Mengapa ini penting:* Operator `SetExtGState` (`gs`) memberi tahu renderer PDF untuk menerapkan parameter yang didefinisikan dalam `GS0`. Persegi panjang akan muncul dengan opacity isi 50 % sementara garisnya tetap sepenuhnya opaque.

## Langkah 7: Simpan PDF yang telah dimodifikasi

Akhirnya, tulis perubahan kembali ke disk. Anda dapat menimpa file asli atau membuat file baru.

```csharp
    // Save the updated PDF
    pdfDocument.Save("YOUR_DIRECTORY/output_with_custom_gs.pdf");
}
```

Saat Anda membuka `output_with_custom_gs.pdf` di penampil PDF, Anda akan melihat persegi panjang semi‑transparan pada halaman pertama. Ini mengonfirmasi bahwa Anda berhasil **membuat custom graphics state**, **mengedit sumber daya PDF**, dan **menambahkan konten transparansi PDF**.

## Variasi umum dan kasus tepi

| Situasi | Apa yang harus disesuaikan |
|-----------|----------------|
| **Beberapa halaman membutuhkan state yang sama** | Daftarkan graphics state sekali (langkah 1‑5) dan referensikan `GS0` pada aliran konten halaman mana pun. |
| **Opacity berbeda per elemen** | Definisikan state tambahan (`GS1`, `GS2`, …) dengan nilai `ca`/`CA` yang berbeda dan beralih di antara mereka menggunakan `SetExtGState`. |
| **Mode blend selain Normal** | Ganti `"Normal"` dengan `"Multiply"`, `"Screen"`, atau mode blend standar PDF apa pun pada entri `BM`. |
| **Tabrakan nama** | Sebelum menambahkan, periksa `extGStateDict.ContainsKey(yourName)` dan pilih sufiks unik bila diperlukan. |
| **PDF sudah berisi kamus ExtGState** | Kode pada Langkah 3 sudah menggunakan kembali kamus yang ada, jadi tidak diperlukan penanganan tambahan. |

**Tips profesional:** Saat bekerja dengan PDF besar, bungkus penggunaan `Document` dalam blok `using` (seperti yang ditunjukkan) untuk segera melepaskan sumber daya native. Juga, pertimbangkan mengaktifkan properti `PdfCompliance` Aspose.Pdf jika Anda perlu menjamin kepatuhan PDF/A atau PDF/X setelah mengedit sumber daya.

## Contoh lengkap yang dapat dijalankan

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Operators;
using Aspose.Pdf.InteractiveFeatures;
using Aspose.Pdf.Text;
using Aspose.Pdf.Facades;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        // Load the PDF you want to edit
        using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
        {
            // Step 1: Get the first page
            Page firstPage = pdfDocument.Pages[1];

            // Step 2: Open the page resources for editing
            var resourcesEditor = new DictionaryEditor(firstPage.Resources);

            // Step 3: Retrieve or create the ExtGState dictionary
            var extGStateDict = resourcesEditor.ContainsKey("ExtGState")
                ? resourcesEditor["ExtGState"].ToCosPdfDictionary()
                : new CosPdfDictionary(pdfDocument);

            // Step 4: Build a custom graphics state (50 % fill opacity, 100 % stroke opacity)
            var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            var graphicsStateParams = new KeyValuePair<string, ICosPdfPrimitive>[]
            {
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
            };
            foreach (var param in graphicsStateParams)
                newGraphicsState.Add(param);

            // Step 5: Register the graphics state under the name GS0
            const string graphicsStateName = "GS0";
            extGStateDict.Add(graphicsStateName, newGraphics


## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang dapat dijalankan dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Cara Membuat PDF dengan Aspose – Tambahkan Form Field dan Halaman](/pdf/english/net/programming-with-forms/how-to-create-pdf-with-aspose-add-form-field-and-pages/)
- [Cara Membuat Tabel Kustom dalam PDF Menggunakan Aspose.PDF .NET](/pdf/english/net/tables-lists/create-custom-tables-in-pdfs-aspose-pdf-dot-net/)
- [Buat Stempel PDF Kustom Aspose Pdf Net](/pdf/hongkong/net/images-graphics/create-custom-pdf-stamps-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}