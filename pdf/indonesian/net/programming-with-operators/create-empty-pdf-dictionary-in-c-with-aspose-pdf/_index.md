---
category: general
date: 2026-08-14
description: Buat kamus PDF kosong di C# menggunakan Aspose.Pdf – pelajari cara menambahkan
  state grafis ke koleksi ExtGState dan memodifikasi PDF secara programatik.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create empty PDF dictionary
- Aspose.Pdf Document
- PDF graphics state
- ExtGState dictionary
- CosPdfDictionary usage
language: id
lastmod: 2026-08-14
og_description: Buat kamus PDF kosong dalam C# dengan Aspose.Pdf. Ikuti panduan lengkap
  ini untuk menambahkan state grafis khusus ke koleksi ExtGState PDF.
og_image_alt: Screenshot showing C# code that creates an empty PDF dictionary with
  Aspose.Pdf
og_title: Buat kamus PDF kosong di C# – Panduan langkah demi langkah Aspose.Pdf
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: Create empty PDF dictionary in C# using Aspose.Pdf – learn how to add
    a graphics state to the ExtGState collection and modify PDFs programmatically.
  headline: Create empty PDF dictionary in C# with Aspose.Pdf
  type: TechArticle
- description: Create empty PDF dictionary in C# using Aspose.Pdf – learn how to add
    a graphics state to the ExtGState collection and modify PDFs programmatically.
  name: Create empty PDF dictionary in C# with Aspose.Pdf
  steps:
  - name: Create a new **Console App** project in Visual Studio.
    text: Create a new **Console App** project in Visual Studio.
  - name: 'Open the **NuGet Package Manager** and install `Aspose.Pdf`:'
    text: 'Open the **NuGet Package Manager** and install `Aspose.Pdf`:'
  - name: 'Add the following `using` directives at the top of `Program.cs`:'
    text: 'Add the following `using` directives at the top of `Program.cs`:'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Buat kamus PDF kosong di C# dengan Aspose.Pdf
url: /id/net/programming-with-operators/create-empty-pdf-dictionary-in-c-with-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat kamus PDF kosong di C# dengan Aspose.Pdf

Jika Anda perlu **create empty PDF dictionary** objek saat bekerja dengan file PDF, panduan ini menunjukkan secara tepat cara melakukannya di C# menggunakan pustaka Aspose.Pdf. Baik Anda sedang membangun state grafis khusus, menambahkan sumber daya baru, atau menyiapkan templat untuk penggunaan nanti, langkah‑langkah di bawah ini memberi Anda solusi lengkap yang dapat dijalankan.

Anda akan belajar cara memuat PDF, mengakses kamus sumber daya halaman pertama, membangun `CosPdfDictionary` baru, dan menyisipkannya ke dalam koleksi `ExtGState`. Pada akhir tutorial Anda akan memiliki `output.pdf` yang berfungsi dan berisi kamus yang baru dibuat.

## Prasyarat

- .NET 6.0 atau yang lebih baru (kode juga berfungsi dengan .NET Framework 4.6+)
- Visual Studio 2022 atau IDE C# apa pun yang Anda sukai
- Lisensi Aspose.Pdf untuk .NET (atau kunci evaluasi sementara)
- Contoh PDF bernama **input.pdf** yang ditempatkan di folder yang Anda kontrol (jalur folder akan digunakan sebagai `dataDir`)

Tidak ada paket NuGet tambahan yang diperlukan selain `Aspose.Pdf`.

## Langkah 1: Siapkan proyek dan referensikan Aspose.Pdf

1. Buat proyek **Console App** baru di Visual Studio.  
2. Buka **NuGet Package Manager** dan instal `Aspose.Pdf`:

   ```bash
   dotnet add package Aspose.Pdf
   ```

3. Tambahkan direktif `using` berikut di bagian atas `Program.cs`:

   ```csharp
   using Aspose.Pdf;
   using Aspose.Pdf.Text;
   using Aspose.Pdf.Operators;
   using Aspose.Pdf.Facades;
   using Aspose.Pdf.InteractiveFeatures;
   using Aspose.Pdf.Xmp;
   using Aspose.Pdf.Operators.Filters;
   using Aspose.Pdf.Operators.Gfx;
   ```

   *Mengapa namespace ini?* `Aspose.Pdf` berisi kelas inti `Document`, sementara `Aspose.Pdf.Operators.Gfx` menyediakan `CosPdfDictionary`, `CosPdfNumber`, dan objek PDF tingkat‑rendah terkait yang diperlukan untuk **create empty PDF dictionary** struktur.

## Langkah 2: Muat PDF sumber

Operasi pertama adalah memuat file PDF yang ada ke dalam instance `Document`. Ini memberi Anda akses ke semua halaman, sumber daya, dan kamus tingkat‑rendah.

```csharp
// Step 2: Load the PDF document
string dataDir = @"C:\MyPdfFolder\";               // Change to your folder
using var pdfDocument = new Document(dataDir + "input.pdf");
```

*Penjelasan*: `Document` membaca file ke memori dan menyiapkan struktur internal. Pernyataan `using` memastikan handle file dilepaskan setelah selesai memproses.

## Langkah 3: Akses kamus sumber daya halaman pertama

Setiap halaman PDF memiliki kamus **Resources** yang mengelompokkan font, gambar, objek ExtGState, dan sumber daya bersama lainnya. Untuk menyisipkan state grafis baru, kita perlu mengedit kamus ini.

```csharp
// Step 3: Get the first page and its Resources dictionary
Page firstPage = pdfDocument.Pages[1];                     // PDF pages are 1‑based
DictionaryEditor resourcesEditor = new DictionaryEditor(firstPage.Resources);
```

`DictionaryEditor` adalah kelas pembantu yang memungkinkan Anda memperlakukan kamus PDF seperti `Dictionary<string, object>` di C#.

## Langkah 4: Dapatkan (atau buat) koleksi ExtGState

`ExtGState` menyimpan objek state grafis seperti opacity, blend mode, dan line width. Jika PDF sumber sudah berisi entri `ExtGState`, kami menggunakannya kembali; jika tidak, kami membuat kamus kosong baru.

```csharp
// Step 4: Ensure an ExtGState dictionary exists
CosPdfDictionary extGStateDict;
if (resourcesEditor.ContainsKey("ExtGState"))
{
    extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
}
else
{
    // Create a brand‑new ExtGState dictionary and add it to Resources
    extGStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
    resourcesEditor["ExtGState"] = extGStateDict;
}
```

*Mengapa pengecekan ini?* Beberapa PDF tidak menyertakan entri `ExtGState` sama sekali. Dengan menangani kedua kasus, tutorial tetap kuat untuk file masukan apa pun.

## Langkah 5: **Create empty PDF dictionary** untuk state grafis baru

Sekarang kami benar‑benarnya **create empty PDF dictionary** objek yang mendefinisikan parameter state grafis. Kamus dimulai kosong, dan kami menambahkan kunci yang diperlukan:

```csharp
// Step 5: Build a new graphics state dictionary (empty PDF dictionary + entries)
CosPdfDictionary newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

// Stroke opacity (CA) – 1 means fully opaque strokes
newGraphicsState.Add("CA", new CosPdfNumber(1));

// Fill opacity (ca) – 0.5 makes semi‑transparent fills
newGraphicsState.Add("ca", new CosPdfNumber(0.5));

// Blend mode (BM) – "Normal" is the default compositing mode
newGraphicsState.Add("BM", new CosPdfName("Normal"));
```

### Apa yang dilakukan setiap entri

| Kunci | Tipe | Makna |
|-----|------|---------|
| **CA** | `CosPdfNumber` | Opacity garis (rentang 0‑1). |
| **ca** | `CosPdfNumber` | Opacity isi (rentang 0‑1). |
| **BM** | `CosPdfName`   | Mode pencampuran; `"Normal"` adalah yang paling umum. |

Karena kami memulai dengan **empty PDF dictionary**, kami memiliki kontrol penuh atas entri yang ditambahkan. Anda dapat memperluas kamus ini dengan parameter state grafis tambahan seperti `LW` (lebar garis) atau `LC` (cap garis) kapan pun diperlukan.

## Langkah 6: Sisipkan state grafis baru ke dalam ExtGState

Kamus `ExtGState` berfungsi seperti peta di mana setiap entri diidentifikasi dengan nama (mis., `GS0`, `GS1`). Kami menambahkan kamus yang baru dibangun di bawah kunci unik.

```csharp
// Step 6: Add the graphics state to the ExtGState collection
extGStateDict.Add("GS0", newGraphicsState);
```

Jika Anda berencana menambahkan beberapa state, tingkatkan sufiks (`GS1`, `GS2`, …) untuk menghindari bentrok nama.

## Langkah 7: Simpan PDF yang dimodifikasi

Akhirnya, tulis perubahan kembali ke disk. Metode `Save` secara otomatis menyerialkan kamus yang diperbarui.

```csharp
// Step 7: Persist the changes
pdfDocument.Save(dataDir + "output.pdf");
```

Buka `output.pdf` di penampil PDF apa pun dan periksa entri **Resources → ExtGState** (sebagian besar penampil menyembunyikannya, tetapi alat seperti Adobe Acrobat Preflight atau PDF‑Tron dapat menampilkannya). Anda harus melihat entri `GS0` yang berisi nilai opacity dan blend mode yang Anda definisikan.

## Contoh kerja lengkap

Menggabungkan semua bagian, berikut program lengkap yang dapat Anda salin‑tempel ke `Program.cs` dan jalankan:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Operators.Gfx;

class Program
{
    static void Main()
    {
        // -----------------------------------------------------------------
        // 1️⃣ Load the PDF document
        // -----------------------------------------------------------------
        string dataDir = @"C:\MyPdfFolder\"; // <-- change to your folder
        using var pdfDocument = new Document(dataDir + "input.pdf");

        // -----------------------------------------------------------------
        // 2️⃣ Access the first page’s Resources dictionary
        // -----------------------------------------------------------------
        Page firstPage = pdfDocument.Pages[1];
        var resourcesEditor = new DictionaryEditor(firstPage.Resources);

        // -----------------------------------------------------------------
        // 3️⃣ Retrieve or create the ExtGState dictionary
        // -----------------------------------------------------------------
        CosPdfDictionary extGStateDict;
        if (resourcesEditor.ContainsKey("ExtGState"))
        {
            extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
        }
        else
        {
            extGStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            resourcesEditor["ExtGState"] = extGStateDict;
        }

        // -----------------------------------------------------------------
        // 4️⃣ **Create empty PDF dictionary** for a new graphics state
        // -----------------------------------------------------------------
        var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
        newGraphicsState.Add("CA", new CosPdfNumber(1));          // Stroke opacity
        newGraphicsState.Add("ca", new CosPdfNumber(0.5));        // Fill opacity
        newGraphicsState.Add("BM", new CosPdfName("Normal"));    // Blend mode

        // -----------------------------------------------------------------
        // 5️⃣ Add the graphics state to ExtGState
        // -----------------------------------------------------------------
        extGStateDict.Add("GS0", newGraphicsState);

        // -----------------------------------------------------------------
        // 6️⃣ Save the modified PDF
        // -----------------------------------------------------------------
        pdfDocument.Save(dataDir + "output.pdf");

        Console.WriteLine("PDF saved with new empty dictionary at: " + dataDir + "output.pdf");
    }
}
```

**Output yang diharapkan** – Konsol mencetak baris konfirmasi, dan `output.pdf` berisi entri `GS0` baru di bawah `ExtGState`. Saat Anda merender halaman yang merujuk ke `GS0` (mis., melalui operator aliran konten `gs`), garis akan sepenuhnya opaque sementara isi menjadi 50 % transparan.

## Pertanyaan umum dan penanganan kasus tepi

| Pertanyaan | Jawaban |
|----------|--------|
| *Bagaimana jika PDF memiliki banyak halaman?* | Contoh ini menargetkan halaman pertama (`Pages[1]`). Untuk memengaruhi semua halaman, lakukan loop melalui `pdfDocument.Pages` dan ulangi langkah 3‑5 untuk sumber daya setiap halaman. |
| *Bisakah saya menambahkan kamus ke halaman yang sudah memiliki entri ExtGState bernama “GS0”?* | Ya, tetapi Anda harus menggunakan kunci berbeda (`GS1`, `GS2`, …) untuk menghindari menimpa entri yang ada. |
| *Apakah aman memodifikasi kamus setelah menyimpan?* | Setelah Anda memanggil `Save`, representasi dalam memori terlepas dari file. Anda dapat terus mengedit objek `Document` dan memanggil `Save` lagi jika diperlukan. |
| *Apakah saya memerlukan lisensi untuk Aspose.Pdf untuk menggunakan `* |  |

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber daya menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan menjelajahi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Cara Membuat Garis Putus-Putus di PDF Menggunakan Aspose.PDF untuk .NET&#58; Panduan Langkah demi Langkah](/pdf/english/net/images-graphics/create-dashed-lines-aspose-pdf-net/)
- [Cara Menghapus Grafik dari PDF Menggunakan Aspose.PDF .NET&#58; Panduan Lengkap](/pdf/english/net/images-graphics/remove-graphics-aspose-pdf-net/)
- [Cara Membuat PDF Multi‑Lapisan Menggunakan Aspose.PDF untuk .NET&#58; Panduan Komprehensif](/pdf/english/net/advanced-features/create-multi-layer-pdfs-aspose-pdf-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}