---
category: general
date: 2026-10-13
description: Pelajari cara mengatur transparansi pada PDF dengan Aspose.Pdf untuk
  C#. Juga lihat cara menyimpan PDF yang telah dimodifikasi dan mengubah nilai fill
  alpha.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to set transparency
- save modified pdf
- change fill alpha
- set fill opacity
- edit pdf resources
language: id
lastmod: 2026-10-13
og_description: Cara mengatur transparansi dalam PDF dengan Aspose.Pdf untuk C#. Ikuti
  panduan ini untuk mengedit sumber daya PDF, mengubah nilai alpha isi, dan menyimpan
  file PDF yang telah dimodifikasi.
og_image_alt: Screenshot of a PDF page showing transparent graphics applied with Aspose.Pdf
  in C#
og_title: Cara mengatur transparansi dalam PDF dengan Aspose.Pdf C# – panduan langkah
  demi langkah
schemas:
- author: Aspose
  dateModified: '2026-10-13'
  description: Learn how to set transparency in a PDF with Aspose.Pdf for C#. Also
    see how to save modified PDF and change fill alpha.
  headline: How to set transparency in a PDF with Aspose.Pdf C#
  type: TechArticle
- description: Learn how to set transparency in a PDF with Aspose.Pdf for C#. Also
    see how to save modified PDF and change fill alpha.
  name: How to set transparency in a PDF with Aspose.Pdf C#
  steps:
  - name: Load the PDF document
    text: '```csharp using Aspose.Pdf; using System.Collections.Generic;'
  - name: Edit PDF resources to add a graphics state
    text: '```csharp // Get the first page (pages are 1‑based) Page firstPage = pdfDocument.Pages[1];'
  - name: Change fill alpha and set fill opacity
    text: '```csharp // Create an empty graphics state dictionary CosPdfDictionary
      newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);'
  - name: Add the new graphics state to the ExtGState dictionary
    text: '```csharp // Register the new state under the name "GS0" extGStateDict.Add("GS0",
      newGraphicsState); ```'
  - name: (Optional) Apply the graphics state in a content stream
    text: 'If you want to draw a rectangle using the new fill opacity, add the following
      after the previous steps:'
  - name: Save modified PDF
    text: '```csharp // Persist the changes to a new file pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
      ```'
  - name: Next steps
    text: '* Explore other blend modes (`Multiply`, `Screen`, etc.) by changing the
      `BM` entry. * Adjust stroke alpha (`CA`) to create semi‑transparent outlines.
      * Combine multiple graphics states to build a library of reusable visual effects.'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF manipulation
- Transparency
title: Cara mengatur transparansi dalam PDF dengan Aspose.Pdf C#
url: /id/net/images-graphics/how-to-set-transparency-in-a-pdf-with-aspose-pdf-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara mengatur transparansi dalam PDF dengan Aspose.Pdf C#

Jika Anda perlu mengatur transparansi dalam PDF menggunakan C#, tutorial ini menunjukkan langkah‑langkah tepatnya. Anda juga akan belajar cara menyimpan file PDF yang telah dimodifikasi dan mengubah fill alpha tanpa meninggalkan lingkungan Aspose.Pdf.

Panduan ini menjelaskan cara memuat dokumen, mengedit sumber daya PDF, membuat graphics state yang mendefinisikan fill opacity, dan menyimpan perubahan. Tidak diperlukan alat eksternal; semuanya berjalan di dalam proyek .NET standar.

## Prasyarat

Sebelum memulai, pastikan Anda memiliki:

* .NET 6.0 atau yang lebih baru terpasang  
* Lisensi Aspose.Pdf untuk .NET yang valid (atau kunci evaluasi gratis)  
* File PDF input yang berada di direktori yang diketahui  

Anda dapat menambahkan paket Aspose.Pdf melalui NuGet:

```bash
dotnet add package Aspose.Pdf
```

## Cara mengatur transparansi dalam PDF

Bagian ini berisi implementasi inti. Setiap langkah menjelaskan **mengapa** kode tersebut diperlukan, bukan hanya **apa** yang dilakukannya.

### Langkah 1: Muat dokumen PDF

```csharp
using Aspose.Pdf;
using System.Collections.Generic;

// Load the source PDF
using var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");
```

*Mengapa langkah ini?*  
`Document` mewakili seluruh file PDF dalam memori. Membuka file memberi Anda akses ke halaman, sumber daya, dan objek tingkat‑rendah yang akan Anda modifikasi.

### Langkah 2: Edit sumber daya PDF untuk menambahkan graphics state

```csharp
// Get the first page (pages are 1‑based)
Page firstPage = pdfDocument.Pages[1];

// Create an editor for the page's resource dictionary
DictionaryEditor resourceEditor = new DictionaryEditor(firstPage.Resources);

// Retrieve the ExtGState dictionary; it holds graphics state objects
CosPdfDictionary extGStateDict = resourceEditor["ExtGState"].ToCosPdfDictionary();
```

*Mengapa langkah ini?*  
Halaman PDF menyimpan objek yang dapat digunakan kembali—font, gambar, dan graphics state—di dalam kamus sumber daya. Entri `ExtGState` berisi pengaturan transparansi. Dengan mengedit kamus ini Anda dapat memperkenalkan state baru yang dapat dirujuk oleh halaman.

### Langkah 3: Ubah fill alpha dan atur fill opacity

```csharp
// Create an empty graphics state dictionary
CosPdfDictionary newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

// Define the graphics state entries
var graphicsStateEntries = new[]
{
    // Stroke alpha (CA) – fully opaque
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
    // Fill alpha (ca) – 50 % transparent
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
    // Blend mode (BM) – normal composition
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
};

// Populate the new graphics state
foreach (var entry in graphicsStateEntries)
    newGraphicsState.Add(entry);
```

*Mengapa langkah ini?*  
`ca` mengontrol **fill opacity**, sedangkan `CA` mengontrol **stroke opacity**. Menetapkan `ca` ke `0.5` membuat bentuk yang diisi menjadi 50 % transparan. Entri `BM` memilih blend mode; `"Normal"` adalah pilihan paling umum untuk transparansi standar.

### Langkah 4: Tambahkan graphics state baru ke kamus ExtGState

```csharp
// Register the new state under the name "GS0"
extGStateDict.Add("GS0", newGraphicsState);
```

*Mengapa langkah ini?*  
Memberi nama graphics state (`"GS0"`) memungkinkan aliran konten pada halaman merujuknya dengan operator `gs`. Setelah pendaftaran ini, halaman dapat menerapkan transparansi yang baru saja Anda definisikan.

### Langkah 5: (Opsional) Terapkan graphics state dalam aliran konten

Jika Anda ingin menggambar persegi panjang menggunakan fill opacity baru, tambahkan kode berikut setelah langkah‑langkah sebelumnya:

```csharp
// Create a content stream that uses the new graphics state
string cs = @"
q               % Save graphics state
/GS0 gs         % Apply the graphics state defined earlier
0 0 200 100 re  % Define a rectangle (x, y, width, height)
0.2 0.6 0.8 rg  % Set fill color (RGB)
f               % Fill the rectangle using the current graphics state
Q               % Restore graphics state
";

firstPage.Contents.Add(new Aspose.Pdf.Operator.GsContent(cs));
```

*Mengapa langkah ini?*  
Operator `q`/`Q` menyimpan dan mengembalikan graphics state, memastikan transparansi hanya memengaruhi perintah gambar yang dimaksud. Operator `gs` beralih ke graphics state bernama `"GS0"`.

### Langkah 6: Simpan PDF yang telah dimodifikasi

```csharp
// Persist the changes to a new file
pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
```

*Mengapa langkah ini?*  
Menyimpan menuliskan kamus sumber daya yang telah diperbarui dan aliran konten baru ke disk. File yang dihasilkan (`output.pdf`) berisi persegi panjang transparan yang didefinisikan pada langkah sebelumnya.

## Contoh lengkap yang dapat dijalankan

Menggabungkan semua bagian, berikut adalah program lengkap yang dapat Anda kompilasi dan jalankan:

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Operators;
using System.Collections.Generic;

class SetTransparencyDemo
{
    static void Main()
    {
        // Load the source PDF
        using var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");

        // Access the first page and its resources
        Page firstPage = pdfDocument.Pages[1];
        var resourceEditor = new DictionaryEditor(firstPage.Resources);
        var extGStateDict = resourceEditor["ExtGState"].ToCosPdfDictionary();

        // Create a new graphics state with 50 % fill opacity
        var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
        var graphicsStateEntries = new[]
        {
            new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),   // stroke alpha
            new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // fill alpha
            new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
        };
        foreach (var entry in graphicsStateEntries)
            newGraphicsState.Add(entry);

        // Register the graphics state as "GS0"
        extGStateDict.Add("GS0", newGraphicsState);

        // Optional: draw a rectangle using the new transparency
        string cs = @"
q
/GS0 gs
0 0 200 100 re
0.2 0.6 0.8 rg
f
Q
";
        firstPage.Contents.Add(new GsContent(cs));

        // Save the modified PDF
        pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
    }
}
```

**Hasil yang diharapkan** – `output.pdf` menampilkan persegi panjang berwarna ungu muda dengan transparansi 50 %, sehingga konten latar belakang terlihat sebagian.

## Pertanyaan umum dan kasus tepi

* **Apakah saya dapat mengubah stroke opacity alih-alih fill opacity?**  
  Atur nilai `CA` (huruf kapital) ke angka antara `0` (sepenuhnya transparan) dan `1` (sepenuhnya opak). Contoh di atas sudah menetapkan `CA` ke `1`, yang berarti garis tetap opak.

* **Bagaimana jika halaman belum memiliki kamus ExtGState?**  
  `resourceEditor["ExtGState"]` akan secara otomatis membuat kamus kosong. Menambahkan `"GS0"` akan berfungsi dengan cara yang sama.

* **Apakah graphics state dapat digunakan kembali di beberapa halaman?**  
  Ya. Setelah Anda menambahkan entri ke kamus sumber daya dokumen, halaman mana pun yang merujuk `"GS0"` akan mewarisi pengaturan transparansi yang sama.

* **Bagaimana pendekatan ini berbeda dari menggunakan API `Graphics` tingkat tinggi?**  
  Mengedit kamus sumber daya tingkat rendah memberi Anda kontrol presisi atas internal PDF dan menghasilkan file yang lebih kecil karena menghindari penyisipan objek tambahan.

## Kesimpulan

Anda kini tahu **cara mengatur transparansi dalam PDF** dengan Aspose.Pdf untuk C#. Tutorial ini mencakup pengeditan sumber daya PDF, mengubah fill alpha, mengatur fill opacity, dan menyimpan PDF yang telah dimodifikasi. Dengan dasar ini Anda dapat bereksperimen dengan berbagai blend mode, menerapkan transparansi pada teks, atau membuat graphics state yang dapat digunakan kembali untuk dokumen kompleks.

### Langkah selanjutnya

* Jelajahi blend mode lain (`Multiply`, `Screen`, dll.) dengan mengubah entri `BM`.  
* Sesuaikan stroke alpha (`CA`) untuk membuat outline semi‑transparan.  
* Gabungkan beberapa graphics state untuk membangun pustaka efek visual yang dapat dipakai ulang.  

Silakan bagikan hasil Anda atau ajukan pertanyaan di kolom komentar. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?


Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber daya menyertakan contoh kode lengkap dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Cara Menyesuaikan PDF dengan Aspose.PDF untuk .NET: Mengatur Margin Halaman dan Menggambar Garis](/pdf/english/net/document-manipulation/customize-pdfs-aspose-pdf-set-margins-draw-lines/)
- [Cara Mengatur Ukuran Gambar dalam PDF Menggunakan Aspose-PDF untuk .NET](/pdf/english/net/images-graphics/set-image-size-pdf-aspose-dotnet/)
- [Cara Mengatur Izin PDF Menggunakan Aspose.PDF untuk .NET: Panduan Komprehensif](/pdf/english/net/security-permissions/set-pdf-privileges-aspose-pdf-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}