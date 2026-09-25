---
category: general
date: 2026-09-24
description: Pelajari cara mengubah transparansi PDF di C# dengan Aspose.Pdf. Panduan
  langkah demi langkah ini mencakup opasitas PDF, mode perpaduan, dan penyuntingan
  keadaan grafis.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- change PDF transparency
- Aspose.Pdf graphics state
- PDF opacity
- C# PDF manipulation
- blend mode PDF
- modify PDF resources
language: id
lastmod: 2026-09-24
og_description: Ubah transparansi PDF di C# menggunakan Aspose.Pdf. Ikuti panduan
  ini untuk mengedit opasitas PDF, mode pencampuran, dan keadaan grafis demi output
  dokumen profesional.
og_image_alt: Screenshot showing C# code that changes PDF transparency
og_title: Ubah transparansi PDF di C# – panduan lengkap Aspose.Pdf
schemas:
- author: Aspose
  dateModified: '2026-09-24'
  description: Learn how to change PDF transparency in C# with Aspose.Pdf. This step‑by‑step
    guide covers PDF opacity, blend mode and graphics state editing.
  headline: How to change PDF transparency in C# using Aspose.Pdf
  type: TechArticle
tags:
- PDF
- C#
- Aspose.Pdf
- Transparency
title: Cara mengubah transparansi PDF di C# menggunakan Aspose.Pdf
url: /id/net/programming-with-operators/how-to-change-pdf-transparency-in-c-using-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara mengubah transparansi PDF di C# menggunakan Aspose.Pdf

Jika Anda perlu **mengubah transparansi PDF** dalam proyek .NET, panduan ini menunjukkan secara tepat cara melakukannya dengan Aspose.Pdf. Anda akan melihat contoh lengkap yang dapat dijalankan yang memodifikasi opacity PDF, mengatur blend mode, dan memperbarui kamus graphics state halaman.

Mengubah transparansi PDF adalah kebutuhan umum ketika Anda menginginkan watermark, grafik overlay, atau efek visual khusus. Dalam tutorial ini Anda akan belajar mengedit **graphics state Aspose.Pdf**, menyesuaikan **opacity PDF**, dan bekerja dengan pengaturan **blend mode PDF**—semua menggunakan kode C# yang bersih.

## Prasyarat

* .NET 6.0 atau yang lebih baru terinstal  
* Lisensi Aspose.Pdf untuk .NET (atau kunci evaluasi sementara)  
* File PDF bernama `input.pdf` dalam folder yang dapat Anda referensikan sebagai `YOUR_DIRECTORY`  
* Familiaritas dasar dengan C# dan Visual Studio (semua IDE dapat digunakan)

Tidak ada paket NuGet tambahan yang diperlukan selain `Aspose.Pdf`. Kode ini berjalan di Windows, Linux, atau macOS karena Aspose.Pdf bersifat lintas‑platform.

## Mengubah transparansi PDF – langkah 1: buka dokumen PDF

Operasi pertama adalah memuat PDF sumber. Menggunakan blok `using` menjamin bahwa handle file dilepaskan secara otomatis.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;
using System.Collections.Generic;

string inputPath  = @"YOUR_DIRECTORY\input.pdf";
string outputPath = @"YOUR_DIRECTORY\output.pdf";

using (var document = new Document(inputPath))
{
    // The document is now ready for manipulation.
```

Membuka dokumen adalah dasar untuk setiap tugas **manipulasi PDF C#**. Jika file tidak ditemukan, Aspose.Pdf akan melempar `FileNotFoundException`, jadi periksa kembali path sebelum menjalankan kode.

## Akses sumber daya halaman dengan graphics state Aspose.Pdf

Selanjutnya, ambil halaman pertama dan kamus sumber dayanya. Kamus sumber daya menyimpan objek seperti font, gambar, dan entri **ExtGState** yang mengontrol parameter grafik.

```csharp
    // Step 2: Get the first page of the document
    var page = document.Pages[1];

    // Step 3: Access the page's resource dictionary for editing
    var resourcesEditor = new DictionaryEditor(page.Resources);
```

Kelas `DictionaryEditor` menyediakan pembungkus yang nyaman untuk membaca dan menulis kamus PDF. Di sini kami fokus pada kamus **ExtGState** karena menyimpan pengaturan transparansi.

## Buat dan konfigurasikan graphics state baru untuk opacity PDF

Sekarang kami membuat kamus graphics state baru. Kamus ini akan menyimpan parameter yang menentukan opacity garis (`CA`), opacity isi (`ca`), dan blend mode (`BM`).

```csharp
    // Step 4: Retrieve the existing ExtGState dictionary (graphics states)
    var extGState = resourcesEditor["ExtGState"].ToCosPdfDictionary();

    // Step 5: Create a new empty graphics state dictionary
    var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(document);

    // Step 6: Define graphics state parameters (stroke opacity, fill opacity, blend mode)
    var parameters = new[]
    {
        new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),            // Stroke opacity (fully opaque)
        new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),          // Fill opacity (50 % transparent)
        new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))       // Blend mode PDF (standard normal blending)
    };

    // Step 7: Add each parameter to the new graphics state dictionary
    foreach (var param in parameters)
        newGraphicsState.Add(param);
```

* **`CA`** mengontrol opacity operasi stroke (garis, batas).  
* **`ca`** mengontrol opacity operasi fill (bentuk terisi, teks).  
* **`BM`** memilih blend mode; `"Normal"` adalah default, tetapi Anda dapat menggunakan `"Multiply"` atau `"Screen"` untuk efek artistik.

Pengaturan ini merupakan inti dari manipulasi **opacity PDF**. Sesuaikan nilai numerik sesuai desain visual Anda—`0` berarti sepenuhnya transparan, `1` berarti sepenuhnya opaque.

## Sisipkan graphics state dan simpan dokumen

Setelah membangun state baru, kami menambahkannya ke kamus **ExtGState** yang ada dengan nama unik (`GS0`). Akhirnya, kami menyimpan PDF yang telah diubah.

```csharp
    // Step 8: Insert the new graphics state into the ExtGState dictionary with a name
    extGState.Add("GS0", newGraphicsState);

    // Step 9: Save the modified PDF document
    document.Save(outputPath);
}
```

Ketika PDF dibuka di penampil, konten apa pun yang merujuk ke `GS0` akan ditampilkan dengan transparansi yang ditentukan. Anda dapat kemudian menerapkan graphics state ini ke objek tertentu menggunakan properti `GraphicsState` dari perintah menggambar (misalnya, `page.Contents.Add(new TextFragment(...){ GraphicsState = "GS0" })`).

## Verifikasi hasil

Buka `output.pdf` di Adobe Acrobat Reader, Foxit, atau penampil PDF apa pun yang mendukung transparansi. Anda seharusnya melihat elemen isi halaman pertama ditampilkan dengan opacity 50 % sementara garis tetap sepenuhnya opaque. Jika Anda tidak melihat perubahan, pastikan halaman memang menggunakan graphics state baru—jika tidak, Anda dapat secara eksplisit menetapkan `GS0` ke objek yang ingin dipengaruhi.

![Contoh kode C# mengubah transparansi PDF](path/to/image.png){: .img-responsive alt="Contoh kode C# mengubah transparansi PDF"}

*Gambar di atas menunjukkan sumber C# lengkap yang mengubah transparansi PDF.*

## Variasi umum dan kasus tepi

| Situasi | Cara menyesuaikan kode |
|-----------|-----------------------|
| **Beberapa halaman** | Loop melalui `document.Pages` dan ulangi langkah 2‑8 untuk setiap halaman. |
| **Blend mode berbeda** | Ganti `"Normal"` dengan `"Multiply"`, `"Screen"`, atau nama blend standar PDF lainnya. |
| **Opacity isi lebih tinggi** | Ubah `new CosPdfNumber(0.5)` menjadi nilai antara `0` dan `1`. |
| **Tidak ada ExtGState yang ada** | Jika `resourcesEditor["ExtGState"]` mengembalikan `null`, buat kamus baru: `var extGState = CosPdfDictionary.CreateEmptyDictionary(document); resourcesEditor["ExtGState"] = extGState;` |

Variasi ini menunjukkan fleksibilitas **memodifikasi sumber daya PDF** menggunakan Aspose.Pdf. Dengan menyesuaikan parameter, Anda dapat menghasilkan watermark, overlay semi‑transparan, atau elemen UI khusus di dalam PDF.

## Contoh lengkap yang dapat dijalankan

Berikut adalah program lengkap yang dapat Anda salin‑tempel ke proyek Console App baru. Program ini berisi semua direktif `using` yang diperlukan, penanganan error, dan komentar.



## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Ubah Opacity PDF dengan Aspose.PDF – Panduan C# Lengkap](/pdf/english/net/programming-with-stamps-and-watermarks/change-pdf-opacity-with-aspose-pdf-complete-c-guide/)
- [Ubah Opacity PDF di C# – Panduan Aspose Lengkap](/pdf/english/net/programming-with-stamps-and-watermarks/change-pdf-opacity-in-c-complete-aspose-guide/)
- [Tambahkan Transparansi ke PDF menggunakan Aspose – Panduan C# Lengkap](/pdf/english/net/programming-with-operators/add-transparency-to-pdf-using-aspose-complete-c-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}