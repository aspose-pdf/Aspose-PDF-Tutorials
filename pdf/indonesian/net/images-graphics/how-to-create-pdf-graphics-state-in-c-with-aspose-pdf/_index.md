---
category: general
date: 2026-11-16
description: Pelajari cara membuat keadaan grafik PDF di C# menggunakan Aspose.Pdf.
  Panduan ini mencakup opasitas, mode pencampuran, dan contoh kode lengkap.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create pdf graphics state
- Aspose.Pdf ExtGState
- PDF opacity
- C# PDF manipulation
- PDF blend mode
- Aspose.Pdf graphics state
language: id
lastmod: 2026-11-16
og_description: Buat keadaan grafik PDF di C# dengan Aspose.Pdf. Ikuti tutorial lengkap
  ini untuk mengatur opasitas dan mode campuran secara programatis.
og_image_alt: Illustration of how to create PDF graphics state with Aspose.Pdf in
  C#
og_title: Buat status grafis PDF di C# – panduan Aspose.Pdf langkah demi langkah
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Learn how to create PDF graphics state in C# using Aspose.Pdf. This
    guide covers opacity, blend mode, and full code example.
  headline: How to create PDF graphics state in C# with Aspose.Pdf
  type: TechArticle
tags:
- Aspose.Pdf
- C#
- PDF
title: Cara membuat state grafik PDF di C# dengan Aspose.Pdf
url: /id/net/images-graphics/how-to-create-pdf-graphics-state-in-c-with-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara membuat PDF graphics state di C# dengan Aspose.Pdf

Jika Anda perlu **membuat PDF graphics state** dalam proyek .NET, tutorial ini menunjukkan secara tepat cara melakukannya dengan Aspose.Pdf. Baik Anda ingin mengontrol opacity, mengubah blend mode, atau menggunakan kembali graphics state khusus di seluruh halaman, langkah‑langkah di bawah ini memberikan solusi lengkap yang siap dijalankan.

Dalam panduan ini Anda akan belajar cara mengakses resources halaman, menambahkan entri **ExtGState**, dan menyimpan perubahan ke file baru. Contoh ini bekerja dengan Aspose.Pdf 23.12 (atau yang lebih baru) dan menargetkan .NET 6+, namun konsepnya juga berlaku untuk versi sebelumnya.

## Prerequisites

Sebelum Anda memulai, pastikan Anda memiliki:

* Visual Studio 2022 (atau IDE C# apa pun) dengan .NET 6 SDK terpasang.  
* Lisensi Aspose.Pdf untuk .NET atau kunci evaluasi sementara.  
* File PDF bernama `input.pdf` ditempatkan di folder yang dapat Anda referensikan dari kode.  

Tidak ada paket NuGet tambahan yang diperlukan selain `Aspose.Pdf`.

## What the tutorial covers

* Memuat dokumen PDF yang ada.  
* Menavigasi ke kamus resources halaman pertama.  
* Membuat kamus graphics state baru yang mendefinisikan stroke opacity (`CA`), fill opacity (`ca`), dan blend mode (`BM`).  
* Menambahkan graphics state baru ke koleksi **ExtGState** dengan nama khusus (`GS0`).  
* Menyimpan PDF yang diperbarui sehingga perintah menggambar berikutnya dapat merujuk ke state baru.

Pada akhir tutorial Anda akan dapat **membuat PDF graphics state** secara programatis dan menggunakannya kembali dalam operasi menggambar apa pun.

## Step 1: Set up the project and import namespaces

Buat aplikasi console baru (atau integrasikan kode ke dalam proyek yang sudah ada). Tambahkan referensi Aspose.Pdf dan sertakan namespace yang diperlukan:

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Operators;
using Aspose.Pdf.Generator;
```

> **Pro tip:** Jika Anda menggunakan versi evaluasi gratis, tambahkan `Aspose.Pdf.License license = new Aspose.Pdf.License(); license.SetLicense("Aspose.Pdf.lic");` sebelum memuat dokumen untuk menghindari pesan watermark.

## Step 2: Load the PDF document

Membuka file sangat sederhana. Kelas `Document` mewakili seluruh PDF dan memberi Anda akses ke halaman serta resources‑nya.

```csharp
// Step 2: Load the PDF document
string inputPath = @"YOUR_DIRECTORY\input.pdf";

using (var document = new Document(inputPath))
{
    // All subsequent steps run inside this using block
```

Menempatkan kode di dalam blok `using` menjamin handle file dilepaskan setelah operasi selesai, yang penting untuk **C# PDF manipulation** dalam layanan produksi.

## Step 3: Retrieve the first page’s resources dictionary

Setiap halaman PDF memiliki kamus *Resources* yang menyimpan font, gambar, dan graphics state. Kita memerlukan `DictionaryEditor` untuk mengedit struktur tersebut.

```csharp
    // Step 3: Get the first page and its resources dictionary
    var page = document.Pages[1];
    var resourcesEditor = new DictionaryEditor(page.Resources);
```

Jika PDF sudah berisi entri `ExtGState`, `resourcesEditor["ExtGState"]` akan mengembalikannya; jika tidak, Aspose.Pdf membuat kamus kosong untuk kita saat menambahkan entri pertama.

## Step 4: Access or create the ExtGState dictionary

Kamus **ExtGState** menyimpan objek graphics state yang diberi nama. Kita dapat mengambil yang sudah ada atau membuat kontainer baru.

```csharp
    // Step 4: Access (or create) the ExtGState dictionary within the resources
    var extGState = resourcesEditor["ExtGState"].ToCosPdfDictionary();
```

Ketika `ExtGState` tidak ada, `resourcesEditor["ExtGState"]` secara otomatis mengembalikan kamus kosong baru, memastikan kode berfungsi untuk PDF apa pun.

## Step 5: Build the new graphics state dictionary

Graphics state adalah `CosPdfDictionary` dengan kunci khusus:

* `CA` – opacity garis (stroke) (0‑1)  
* `ca` – opacity isi (fill) (0‑1)  
* `BM` – blend mode (`Normal`, `Multiply`, dll.)

Kami membuat kamus kosong, mengisinya, lalu menambahkannya ke `ExtGState`.

```csharp
    // Step 5: Create a new graphics state dictionary with desired parameters
    var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(document);
    var parameters = new[]
    {
        new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),   // Stroke opacity (fully opaque)
        new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // Fill opacity (50% transparent)
        new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // Blend mode
    };

    foreach (var p in parameters)
        newGraphicsState.Add(p);
```

Anda dapat mengubah `0.5` ke nilai apa pun antara `0` dan `1` untuk menyesuaikan opacity isi, atau mengganti `"Normal"` dengan `"Multiply"` untuk **PDF blend mode** yang berbeda. Fleksibilitas ini menjadikan pembuatan graphics state khusus teknik yang kuat dalam penanganan **Aspose.Pdf graphics state**.

## Step 6: Register the graphics state with a name

Stream konten PDF merujuk ke graphics state berdasarkan nama. Di sini kami menggunakan `GS0`, tetapi nama unik apa pun dapat dipakai.

```csharp
    // Step 6: Add the new graphics state to the ExtGState dictionary with a name (e.g., GS0)
    extGState.Add("GS0", newGraphicsState);
```

Jika Anda memerlukan beberapa state, ulangi langkah pembuatan dengan parameter berbeda dan tambahkan sebagai `GS1`, `GS2`, dll. Pola ini skalabel untuk dokumen kompleks yang memerlukan opacity atau blend setting yang beragam pada lapisan berbeda.

## Step 7: Save the modified PDF

Akhirnya, tulis dokumen yang telah diperbarui ke file baru. Menjaga file asli tetap utuh memudahkan proses debugging.

```csharp
    // Step 7: Save the updated PDF document
    string outputPath = @"YOUR_DIRECTORY\output.pdf";
    document.Save(outputPath);
}
```

Setelah dijalankan, `output.pdf` berisi entri `ExtGState` bernama `GS0`. Setiap operator menggambar selanjutnya dapat merujuknya menggunakan operator `gs` (misalnya `GS0 gs` dalam stream konten).  

> **Why this matters:** Dengan membuat graphics state yang dapat digunakan kembali, Anda menghindari pengulangan pengaturan opacity dan blend untuk setiap perintah menggambar, yang meningkatkan kinerja dan kemudahan pemeliharaan.

## Using the new graphics state in a content stream (optional)

Jika Anda ingin melihat efeknya segera, Anda dapat menambahkan persegi sederhana yang menggunakan state yang baru saja dibuat:

```csharp
using (var document = new Document(outputPath))
{
    var page = document.Pages[1];
    var content = page.Contents[1]; // Get the first content stream

    // Insert graphics state selection and a semi‑transparent rectangle
    var operators = new List<Operator>
    {
        new Operator("GS0", "gs"),                     // Select our custom graphics state
        new Operator("0.5", "w"),                      // Set line width (optional)
        new Operator("100", "100", "200", "150", "re"), // Rectangle (x, y, width, height)
        new Operator("B")                              // Stroke the rectangle
    };

    foreach (var op in operators)
        content.Operators.Add(op);

    document.Save(@"YOUR_DIRECTORY\final_output.pdf");
}
```

Persegi akan digambar dengan 50 % opacity isi sementara garis tetap sepenuhnya opaque, persis seperti yang didefinisikan dalam kamus **create PDF graphics state**.

## Common pitfalls and how to avoid them

| Masalah | Mengapa terjadi | Solusi |
|-------|----------------|-----|
| `ExtGState` tidak ditemukan | Beberapa PDF tidak menyertakan kamus tersebut sama sekali. | `DictionaryEditor` secara otomatis membuatnya ketika Anda menambahkan entri pertama, jadi tidak perlu pemeriksaan tambahan. |
| Nilai opacity > 1 atau < 0 | Spesifikasi PDF membatasi opacity pada rentang `[0,1]`. | Batasi nilai sebelum membuat `CosPdfNumber`. |
| Kesalahan penulisan blend mode | Nama blend mode PDF bersifat case‑sensitive. | Gunakan nama yang tepat seperti `"Normal"`, `"Multiply"`, `"Screen"`. |
| Watermark lisensi | Versi evaluasi menambahkan watermark pada halaman pertama. | Terapkan file lisensi yang valid sebelum membuka dokumen. |

Menangani kasus tepi ini memastikan implementasi **create PDF graphics state** Anda bekerja secara andal di berbagai sumber PDF.

## Full, runnable example

Berikut adalah program mandiri yang dapat Anda salin, tempel, dan jalankan. Ganti `YOUR_DIRECTORY` dengan jalur folder yang sebenarnya di mesin Anda.

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Generator;

class Program
{
    static void Main()
    {
        // Optional: apply license to remove evaluation watermark
        // var license = new Aspose.Pdf.License();
        // license.SetLicense("Aspose.Pdf.lic");

        string inputPath = @"YOUR_DIRECTORY\input.pdf";
        string outputPath = @"YOUR_DIRECTORY\output.pdf";

        using (var document = new Document(inputPath))
        {
            // 1️⃣ Get first page and its resources
            var page = document.Pages[1];
            var resourcesEditor = new DictionaryEditor(page.Resources);

            // 2️⃣ Access (or create) ExtGState dictionary
            var extGState = resourcesEditor["ExtGState"].ToCosPdfDictionary();

            // 3️⃣ Build new graphics state
            var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(document);
            var parameters = new[]
            {
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),   // Stroke opacity
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // Fill opacity
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // Blend mode
            };
            foreach (var p in parameters) newGraphicsState.Add(p);

            // 4️⃣ Register the state with a name (GS0)
            extGState.Add("


## Apa yang Harus Anda Pelajari Selanjutnya?


- [Buat custom graphics state dalam PDF menggunakan Aspose.Pdf](/pdf/english/net/programming-with-operators/create-custom-graphics-state-in-pdf-using-aspose-pdf/)
- [Tambahkan graphics state ke PDF menggunakan Aspose.PDF untuk .NET (C#)](/pdf/english/net/programming-with-operators/how-to-add-graphics-state-pdf-using-aspose-pdf-in-c/)
- [Cara membuat graphics state kosong dalam PDF dengan C#](/pdf/english/net/programming-with-operators/how-to-create-empty-graphics-state-in-a-pdf-with-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}