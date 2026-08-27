---
category: general
date: 2026-02-09
description: Simpan PDF sebagai PNG di C# menggunakan Aspose PDF, kemudian ekspor
  PDF ke HTML, tambahkan watermark stempel PDF, dan pelajari cara mengonversi PDFX‑1a
  untuk konversi PDF ASP.NET.
draft: false
keywords:
- save pdf as png
- export pdf to html
- add watermark stamp pdf
- how to convert pdfx-1a
- asp.net pdf conversion
language: id
og_description: Simpan PDF sebagai PNG di C# dengan Aspose PDF, lalu ekspor PDF ke
  HTML, tambahkan watermark stempel PDF, dan temukan cara mengonversi PDFX‑1a untuk
  konversi PDF ASP.NET.
og_title: Simpan PDF sebagai PNG dan Konversi ke PDF/X‑1a dengan Aspose PDF
tags:
- aspnet
- pdf
- csharp
title: Simpan PDF sebagai PNG dan Konversi ke PDF/X‑1a dengan Aspose PDF
url: /id/net/conversion-export/save-pdf-as-png-and-convert-to-pdf-x-1a-with-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Simpan PDF sebagai PNG dan Konversi ke PDF/X‑1a dengan Aspose PDF

Pernah bertanya-tanya bagaimana cara **menyimpan PDF sebagai PNG** tanpa membuat kepala Anda berhamburan? Anda bukan satu-satunya—para pengembang terus menanyakan cara cepat untuk meraster halaman sambil tetap menjaga PDF asli tetap utuh. Dalam panduan ini kami akan membahas hal tersebut, serta menunjukkan cara **mengekspor PDF ke HTML**, menambahkan **watermark stamp PDF**, dan bahkan **mengonversi PDFX‑1a** untuk pipeline **ASP.NET PDF conversion** yang kuat.

Apa yang akan Anda dapatkan dari tutorial ini adalah program C# siap‑salin‑tempel yang memuat PDF, mengonversinya ke file yang mematuhi PDF/X‑1a, merender halaman pertama sebagai PNG, menambahkan stempel teks dinamis, dan akhirnya menghasilkan versi HTML yang menghormati enkoding font. Tanpa referensi yang samar, hanya kode konkret dan “kenapa” di balik setiap baris.

## Prasyarat

- .NET 6.0 atau lebih baru (kode ini juga berfungsi pada .NET Framework 4.7+)
- Paket NuGet Aspose.Pdf untuk .NET (`Install-Package Aspose.Pdf`)
- File profil ICC (`profile.icc`) jika Anda memerlukan kepatuhan PDF/X‑1a
- PDF sumber (`input.pdf`) yang ingin Anda ubah

Itu saja—tidak ada pustaka tambahan, tidak ada langkah tersembunyi. Jika Anda sudah memiliki semua itu, Anda siap melanjutkan.

## Langkah 1: Muat Dokumen PDF Sumber

Sebelum kita dapat melakukan apa pun, kita harus membawa PDF ke memori.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Devices;

// Load the PDF you’ll be working with
Document pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");
```

**Mengapa ini penting:** `Document` adalah objek inti; ia memberi Anda akses ke halaman, font, dan metadata. Memuatnya sekali membuat sisa pipeline tetap cepat.

## Langkah 2: Konversi ke PDF/X‑1a (Cara Mengonversi PDFX‑1a)

PDF/X‑1a adalah standar utama untuk file siap cetak. Mengonversi memastikan semua font tertanam dan warna terdefinisi.

```csharp
// Set up conversion options for PDF/X‑1a
PdfFormatConversionOptions conversionOptions = new PdfFormatConversionOptions(
    PdfFormat.PDF_X_1A,               // Target format
    ConvertErrorAction.Delete)       // What to do on errors
{
    IccProfileFileName = "YOUR_DIRECTORY/profile.icc", // External ICC profile
    OutputIntent = new OutputIntent("FOGRA39")        // Output intent for printing
};

// Perform the conversion
pdfDocument.Convert(conversionOptions);
```

**Tips profesional:** Jika Anda melewatkan profil ICC, Aspose akan menanamkan profil default, tetapi menggunakan profil yang tepat sesuai printer Anda menghindari pergeseran warna yang tidak diinginkan.

## Langkah 3: Simpan File yang Mematuhi PDF/X‑1a

Setelah dokumen memenuhi spesifikasi PDF/X‑1a, kita menuliskannya ke disk.

```csharp
pdfDocument.Save("YOUR_DIRECTORY/pdfx1a.pdf");
```

Anda akan melihat ukuran file mungkin bertambah—sumber daya tambahan sedang ditanamkan, yang memang diinginkan untuk output cetak yang dapat diandalkan.

## Langkah 4: Render Halaman Pertama ke PNG (Simpan PDF sebagai PNG)

Di sinilah kata kunci utama bersinar: kita akan **menyimpan PDF sebagai PNG** untuk pratinjau thumbnail atau tampilan web.

```csharp
// Configure PNG device with font analysis (helps with text extraction later)
PngDevice pngDevice = new PngDevice
{
    RenderingOptions = new RenderingOptions { AnalyzeFonts = true }
};

// Render only the first page
pngDevice.Process(pdfDocument.Pages[1], "YOUR_DIRECTORY/page1.png");
```

![Contoh menyimpan PDF sebagai PNG](https://example.com/images/save-pdf-as-png.png "Contoh halaman PDF yang disimpan sebagai PNG")

Flag `AnalyzeFonts` memberi tahu Aspose untuk menanamkan informasi font dalam metadata PNG, trik berguna jika Anda nanti perlu memetakan kembali ke teks asli.

## Langkah 5: Tambahkan Watermark Stamp PDF

Menambahkan **watermark stamp PDF** sangat mudah dengan `TextStamp` milik Aspose. Kita akan membuat stempel menyesuaikan ukuran secara otomatis agar sesuai dengan persegi panjang.

```csharp
// Create a text stamp that auto‑adjusts its font size
TextStamp textStamp = new TextStamp("Important notice")
{
    AutoAdjustFontSizeToFitStampRectangle = true,
    AutoAdjustFontSizePrecision = 0.01f,
    Width = 400,               // Width of the stamp rectangle
    Height = 200,              // Height of the stamp rectangle
    WordWrapMode = TextFormattingOptions.WordWrapMode.ByWords
};

// Place the stamp on the first page
pdfDocument.Pages[1].AddStamp(textStamp);
```

**Mengapa menyesuaikan otomatis?** Halaman yang berbeda memiliki kepadatan yang berbeda; membiarkan API menghitung ukuran font optimal menjamin teks tidak meluber keluar dari persegi panjang.

## Langkah 6: Simpan PDF yang Sudah Diberi Stempel

Setelah menambahkan stempel, kita menyimpan perubahan.

```csharp
pdfDocument.Save("YOUR_DIRECTORY/stamped.pdf");
```

Buka `stamped.pdf` di penampil apa pun dan Anda akan melihat kotak “Important notice” terpusat rapi—tanpa perlu penyesuaian manual.

## Langkah 7: Ekspor PDF ke HTML (Export PDF to HTML)

Akhirnya, mari **mengekspor PDF ke HTML** sambil mengutamakan CMap untuk enkoding font. Ini memastikan HTML yang dihasilkan menggunakan Unicode bila memungkinkan, menjaga teks tetap dapat dicari.

```csharp
HtmlSaveOptions htmlOptions = new HtmlSaveOptions
{
    FontEncodingStrategy = HtmlSaveOptions.FontEncodingRules.DecreaseToUnicodePriorityLevel
};

// Save the HTML representation
pdfDocument.Save("YOUR_DIRECTORY/cmap.html", htmlOptions);
```

`cmap.html` yang dihasilkan berisi elemen `<canvas>` untuk grafik kompleks dan tag `<span>` yang tepat untuk teks, menjadikannya siap untuk halaman web yang SEO‑friendly.

## Contoh Program Lengkap

Berikut adalah program lengkap yang dapat Anda masukkan ke aplikasi console. Cukup ganti jalur placeholder dan Anda siap.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Devices;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source PDF
        Document pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");

        // 2️⃣ Convert to PDF/X‑1a (how to convert pdfx‑1a)
        PdfFormatConversionOptions conversionOptions = new PdfFormatConversionOptions(
            PdfFormat.PDF_X_1A,
            ConvertErrorAction.Delete)
        {
            IccProfileFileName = "YOUR_DIRECTORY/profile.icc",
            OutputIntent = new OutputIntent("FOGRA39")
        };
        pdfDocument.Convert(conversionOptions);

        // 3️⃣ Save the PDF/X‑1a file
        pdfDocument.Save("YOUR_DIRECTORY/pdfx1a.pdf");

        // 4️⃣ Render first page as PNG (save pdf as png)
        PngDevice pngDevice = new PngDevice
        {
            RenderingOptions = new RenderingOptions { AnalyzeFonts = true }
        };
        pngDevice.Process(pdfDocument.Pages[1], "YOUR_DIRECTORY/page1.png");

        // 5️⃣ Add a dynamic watermark stamp (add watermark stamp pdf)
        TextStamp textStamp = new TextStamp("Important notice")
        {
            AutoAdjustFontSizeToFitStampRectangle = true,
            AutoAdjustFontSizePrecision = 0.01f,
            Width = 400,
            Height = 200,
            WordWrapMode = TextFormattingOptions.WordWrapMode.ByWords
        };
        pdfDocument.Pages[1].AddStamp(textStamp);

        // 6️⃣ Save the stamped PDF
        pdfDocument.Save("YOUR_DIRECTORY/stamped.pdf");

        // 7️⃣ Export to HTML (export pdf to html)
        HtmlSaveOptions htmlOptions = new HtmlSaveOptions
        {
            FontEncodingStrategy = HtmlSaveOptions.FontEncodingRules.DecreaseToUnicodePriorityLevel
        };
        pdfDocument.Save("YOUR_DIRECTORY/cmap.html", htmlOptions);

        Console.WriteLine("All operations completed successfully.");
    }
}
```

**Output yang diharapkan**

- `pdfx1a.pdf` – file PDF/X‑1a siap cetak
- `page1.png` – gambar raster halaman pertama (sempurna untuk thumbnail)
- `stamped.pdf` – PDF asli dengan watermark “Important notice” yang dapat diskalakan
- `cmap.html` – versi HTML ramah web dengan font Unicode

## Pertanyaan Umum & Kasus Tepi

- **Bagaimana jika PDF sumber memiliki halaman terenkripsi?**  
  Muat dengan kata sandi: `new Document("input.pdf", new LoadOptions { Password = "secret" })`.

- **Apakah saya perlu profil ICC untuk setiap konversi?**  
  Tidak mutlak—Aspose akan kembali ke profil generik, tetapi untuk kepatuhan PDF/X‑1a yang ketat sebaiknya gunakan profil yang sama persis dengan yang dipakai percetakan Anda.

- **Bisakah saya merender lebih dari satu halaman ke PNG?**  
  Tentu saja. Lakukan loop pada `pdfDocument.Pages` dan panggil `pngDevice.Process(page, $"page{page.Number}.png")`.

- **Apakah output HTML mobile‑friendly?**  
  HTML yang dihasilkan menggunakan elemen `<canvas>` responsif. Jika Anda memerlukan teks berbasis CSS murni, atur `htmlOptions.SplitIntoPages = false` dan sesuaikan `htmlOptions.PartsEmbeddingMode`.

## Tips untuk ASP.NET PDF Conversion

Saat Anda mengintegrasikan kode ini ke dalam controller ASP.NET Core, ingat untuk:

1. **Stream hasilnya** alih-alih menulis ke disk—gunakan `MemoryStream` dan kembalikan `FileResult`.
2. **Dispose** objek `Document` dan perangkat dengan `using

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}