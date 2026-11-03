---
category: general
date: 2026-10-07
description: Tambahkan state grafis PDF menggunakan Aspose.Pdf di C# untuk memodifikasi
  transparansi PDF. Ikuti panduan langkah demi langkah ini untuk menyematkan state
  grafis khusus dan mengontrol opasitas.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add graphics state pdf
- modify pdf transparency
language: id
lastmod: 2026-10-07
og_description: Tambahkan state grafis PDF dengan Aspose.Pdf di C#. Pelajari cara
  memodifikasi transparansi PDF dengan membuat kamus state grafis khusus.
og_image_alt: Screenshot showing the add graphics state pdf code editor in Visual
  Studio
og_title: Tambahkan state grafis PDF dengan Aspose.Pdf – kontrol transparansi PDF
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Add graphics state pdf using Aspose.Pdf in C# to modify PDF transparency.
    Follow this step‑by‑step guide to embed custom graphics states and control opacity.
  headline: Add graphics state pdf with Aspose.Pdf in C#
  type: TechArticle
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Menambahkan state grafis PDF dengan Aspose.Pdf di C#
url: /id/net/images-graphics/add-graphics-state-pdf-with-aspose-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tambahkan graphics state PDF dengan Aspose.Pdf di C#

Jika Anda perlu **menambahkan graphics state PDF** ke sebuah dokumen, tutorial ini menunjukkan secara tepat cara melakukannya dengan Aspose.Pdf untuk .NET. Pada akhir panduan, Anda juga akan mengetahui cara **memodifikasi transparansi PDF**, yang memungkinkan Anda mengatur nilai opacity khusus pada operasi menggambar apa pun.

Bekerja dengan graphics state PDF memungkinkan Anda mengontrol parameter seperti lebar garis, mode pencampuran, dan yang paling penting untuk artikel ini, transparansi konten. Langkah‑langkah di bawah ini ditulis untuk pengembang yang nyaman dengan C# dan menginginkan solusi siap‑jalankan tanpa harus menelusuri dokumentasi SDK resmi.

## Apa yang akan Anda pelajari

* Cara membuat kamus graphics state baru dan mengisinya dengan entri `CA`, `ca`, dan `BM`.  
* Cara menyisipkan kamus tersebut ke dalam sumber daya `ExtGState` halaman sehingga PDF mengenalinya.  
* Bagaimana nilai `ca` (stroke) dan `CA` (fill) memengaruhi **modifikasi transparansi PDF** untuk perintah menggambar berikutnya.  
* Kesulitan umum seperti bentrok penamaan dan kompatibilitas versi, serta tip profesional untuk memperluas graphics state di kemudian hari.

**Prasyarat**

* .NET 6.0 atau yang lebih baru (kode ini juga berfungsi dengan .NET Framework 4.7+).  
* Lisensi Aspose.Pdf untuk .NET yang valid (evaluasi gratis dapat digunakan untuk pengujian).  
* Visual Studio 2022 atau IDE C# apa pun yang Anda sukai.  

---

## Step 1: Install Aspose.Pdf for .NET

Tambahkan paket NuGet ke proyek Anda:

```bash
dotnet add package Aspose.Pdf
```

Paket ini mencakup namespace `Aspose.Pdf` yang menyediakan kelas `Document`, `DictionaryEditor`, dan `CosPdfDictionary` yang akan digunakan nanti.

> **Tip pro:** Jika Anda berencana memproses banyak PDF dalam batch, aktifkan **License** lebih awal di `Program.cs` untuk menghindari watermark evaluasi.

```csharp
// Apply your license (optional for evaluation)
Aspose.Pdf.License license = new Aspose.Pdf.License();
license.SetLicense("Aspose.Pdf.lic");
```

## Step 2: Define input and output paths

Anda harus mengarahkan SDK ke PDF yang sudah ada (`input.pdf`) dan menentukan di mana file yang dimodifikasi akan disimpan (`output.pdf`).

```csharp
// Define input and output PDF file paths
string inputPath = @"C:\MyPdfs\input.pdf";
string outputPath = @"C:\MyPdfs\output.pdf";
```

> **Mengapa ini penting:** Menggunakan path absolut mencegah SDK mencari di direktori kerja yang salah, yang merupakan sumber umum `FileNotFoundException`.

## Step 3: Open the PDF and locate the first page’s resources

Kamus `ExtGState` berada di dalam kamus sumber daya setiap halaman. Kami akan mengedit halaman pertama untuk kesederhanaan, tetapi pendekatan yang sama berlaku untuk indeks halaman mana pun.

```csharp
using (var pdfDocument = new Aspose.Pdf.Document(inputPath))
{
    // Get the first page (pages are 1‑based)
    var firstPage = pdfDocument.Pages[1];

    // Access the page’s resource dictionary via DictionaryEditor
    var resourcesEditor = new Aspose.Pdf.DictionaryEditor(firstPage.Resources);

    // Retrieve (or create) the ExtGState entry
    var extGStateDict = resourcesEditor["ExtGState"]
        .ToCosPdfDictionary(); // Throws if ExtGState does not exist
```

**Kasus khusus:** Jika halaman tidak memiliki entri `ExtGState`, Anda perlu membuatnya:

```csharp
if (!resourcesEditor.ContainsKey("ExtGState"))
{
    var emptyDict = Aspose.Pdf.CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
    resourcesEditor.Add("ExtGState", emptyDict);
    extGStateDict = emptyDict;
}
```

## Step 4: Build a new graphics state dictionary

Graphics state adalah kumpulan pasangan kunci/nilai yang menggambarkan bagaimana operasi menggambar berperilaku. Untuk transparansi kita memerlukan tiga kunci:

| Key | Arti | Nilai tipikal |
|-----|------|---------------|
| `CA` | Opacity isi (0 = transparan, 1 = opaque) | `1` (sepenuhnya opaque) |
| `ca` | Opacity garis (skala sama) | `0.5` (50 % transparan) |
| `BM` | Mode pencampuran (mis., `Normal`, `Multiply`) | `Normal` |

```csharp
    // Create an empty dictionary that will hold the graphics state
    var newGraphicsState = Aspose.Pdf.CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

    // Populate the dictionary with transparency and blend mode entries
    var graphicsStateEntries = new[]
    {
        new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
            "CA", new Aspose.Pdf.CosPdfNumber(1)),
        new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
            "ca", new Aspose.Pdf.CosPdfNumber(0.5)),
        new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
            "BM", new Aspose.Pdf.CosPdfName("Normal"))
    };

    foreach (var entry in graphicsStateEntries)
        newGraphicsState.Add(entry);
```

**Mengapa nilai‑nilai ini?**  
`ca = 0.5` membuat setiap jalur yang digambar (garis, border) muncul dengan opacity 50 %, sementara `CA = 1` membiarkan bentuk yang diisi tetap sepenuhnya opaque. Sesuaikan kedua angka untuk mencapai efek **modifikasi transparansi PDF** yang tepat.

## Step 5: Insert the graphics state into the ExtGState dictionary

Anda harus memberi state baru nama yang unik (mis., `GS0`). Jika nama tersebut sudah ada, Aspose.Pdf akan menimpa entri yang ada, yang dapat merusak konten lain yang bergantung padanya.

```csharp
    // Add the new graphics state under a custom name
    const string stateName = "GS0";

    // Ensure we don’t clash with an existing entry
    if (extGStateDict.ContainsKey(stateName))
        extGStateDict.Remove(stateName);

    extGStateDict.Add(stateName, newGraphicsState);
```

Sekarang sumber daya halaman mengetahui tentang `GS0`. Untuk benar‑benar menggunakannya, Anda akan merujuk graphics state dalam stream konten melalui operator `gs` (mis., `GS0 gs`). Aspose.Pdf memungkinkan Anda menyuntikkan operator PDF mentah jika perlu menggambar bentuk khusus.

## Step 6: Save the modified PDF

```csharp
    // Persist the changes to a new file
    pdfDocument.Save(outputPath);
}
```

PDF `output.pdf` yang dihasilkan berisi konten visual yang sama dengan yang asli, tetapi setiap perintah menggambar berikutnya yang memilih `GS0` akan menghormati pengaturan transparansi yang Anda definisikan.

### Expected result

Buka `output.pdf` di Adobe Acrobat atau penampil PDF apa pun. Jika Anda menambahkan garis baru yang di‑stroke menggunakan graphics state `GS0` (mis., melalui `pdfDocument.Pages[1].Contents.Add(...)`), garis tersebut akan muncul semi‑transparent sementara isian tetap opaque. Ini menunjukkan bahwa Anda telah berhasil **menambahkan graphics state PDF** dan **memodifikasi transparansi PDF**.

---

## Full runnable example

Berikut adalah program lengkap yang dapat Anda salin‑tempel ke aplikasi konsol. Program ini mencakup pemuatan lisensi, penanganan error, dan komentar yang menjelaskan setiap langkah yang tidak langsung.

```csharp
using System;
using Aspose.Pdf;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣  Apply license (optional for evaluation)
        // -------------------------------------------------
        try
        {
            var license = new License();
            license.SetLicense("Aspose.Pdf.lic");
        }
        catch (Exception) { /* License not found – continue in evaluation mode */ }

        // -------------------------------------------------
        // 2️⃣  Define file locations
        // -------------------------------------------------
        string inputPath = @"C:\MyPdfs\input.pdf";
        string outputPath = @"C:\MyPdfs\output.pdf";

        // -------------------------------------------------
        // 3️⃣  Open document and prepare resources
        // -------------------------------------------------
        using (var pdfDocument = new Document(inputPath))
        {
            var firstPage = pdfDocument.Pages[1];
            var resourcesEditor = new DictionaryEditor(firstPage.Resources);

            // Ensure ExtGState dictionary exists
            if (!resourcesEditor.ContainsKey("ExtGState"))
            {
                var emptyExtGState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
                resourcesEditor.Add("ExtGState", emptyExtGState);
            }

            var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();

            // -------------------------------------------------
            // 4️⃣  Create custom graphics state (transparency)
            // -------------------------------------------------
            var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            newGraphicsState.Add("CA", new CosPdfNumber(1));   // Fill opacity
            newGraphicsState.Add("ca", new CosPdfNumber(0.5)); // Stroke opacity
            newGraphicsState.Add("BM", new CosPdf


## What Should You Learn Next?

Tutorial berikut mencakup topik terkait yang membangun pada teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Tambahkan Transparansi ke PDF dengan Aspose PDF di C# – Panduan Langkah demi Langkah](/pdf/english/net/images-graphics/add-transparency-to-pdf-with-aspose-pdf-in-c-step-by-step-gu/)
- [Tambahkan Transparansi ke PDF menggunakan Aspose – Panduan Lengkap C#](/pdf/english/net/programming-with-operators/add-transparency-to-pdf-using-aspose-complete-c-guide/)
- [Cara Menambahkan Stempel Gambar ke PDF Menggunakan Aspose.PDF untuk .NET: Panduan Komprehensif](/pdf/english/net/images-graphics/add-image-stamp-pdf-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}