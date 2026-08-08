---
category: general
date: 2026-06-05
description: Tambahkan persegi panjang ke PDF menggunakan Aspose.Pdf dalam C#. Pelajari
  cara memuat PDF yang ada, mengedit halaman PDF, dan menyisipkan bentuk ke PDF dalam
  hitungan menit.
draft: false
keywords:
- add rectangle to pdf
- draw rectangle on pdf
- load existing pdf
- edit pdf page
- insert shape into pdf
language: id
og_description: Tambahkan persegi panjang ke PDF dengan cepat. Tutorial ini menunjukkan
  cara memuat PDF yang ada, mengedit halaman PDF, dan menggambar persegi panjang pada
  PDF menggunakan Aspose.Pdf.
og_title: Menambahkan Persegi Panjang ke PDF dengan C# – Panduan Langkah demi Langkah
schemas:
- author: Aspose
  dateModified: '2026-06-05'
  description: Add rectangle to PDF using Aspose.Pdf in C#. Learn how to load existing
    PDF, edit PDF page, and insert shape into PDF in minutes.
  headline: Add Rectangle to PDF with C# – Complete Programming Guide
  type: TechArticle
- description: Add rectangle to PDF using Aspose.Pdf in C#. Learn how to load existing
    PDF, edit PDF page, and insert shape into PDF in minutes.
  name: Add Rectangle to PDF with C# – Complete Programming Guide
  steps:
  - name: Prerequisites
    text: '- .NET 6.0 or later (the code also works on .NET Framework 4.6+). - Aspose.Pdf
      for .NET NuGet package (`Install-Package Aspose.Pdf`). - Basic familiarity with
      C# syntax (no deep PDF knowledge required).'
  - name: Why loading matters
    text: Before you can draw anything, the PDF must be in memory. The `Document`
      constructor reads the file, parses its internal structure, and gives you an
      object model to work with. If the file is locked or corrupted, Aspose will throw
      a descriptive exception—so you know exactly what went wrong.
  - name: Code
    text: '```csharp Document doc = new Document("YOUR_DIRECTORY/input.pdf"); ```'
  - name: Why page selection is crucial
    text: PDFs are page‑oriented; each page has its own coordinate system. Aspose
      uses a **1‑based** index, which trips up developers coming from 0‑based collections.
      Selecting the wrong page either throws an `ArgumentOutOfRangeException` or modifies
      an unintended page.
  - name: Code
    text: '```csharp Page page = doc.Pages[1]; // First page ```'
  - name: Understanding the rectangle coordinates
    text: A rectangle in Aspose.Pdf is defined by its lower‑left (`xLL`, `yLL`) and
      upper‑right (`xUR`, `yUR`) corners. The coordinate system starts at the **bottom‑left**
      of the page, with X increasing to the right and Y increasing upward. This is
      opposite of many UI frameworks, so keep an eye on the axes.
  - name: Code to add the shape
    text: '```csharp Aspose.Pdf.Rectangle rect = new Aspose.Pdf.Rectangle(0, 0, 500,
      700); page.AddRectangle(rect); ```'
  - name: Why saving is the final step
    text: All manipulations stay in memory until you persist them. `Document.Save`
      writes the new content to disk (or stream). Overwriting the original file is
      possible, but keeping a backup (`output.pdf`) is safer.
  - name: Code
    text: '```csharp doc.Save("YOUR_DIRECTORY/output.pdf"); ```'
  type: HowTo
- questions:
  - answer: Yes—loop through `doc.Pages` and repeat the `AddRectangle` call for each
      `Page` object.
    question: Can I add the rectangle to every page automatically?
  - answer: Aspose provides `AddCircle`, `AddPolygon`, and `AddPolyline` methods.
      The same rectangle logic applies for bounding boxes.
    question: What if I need to draw a circle or a polygon?
  - answer: 'Compute the center coordinates:'
    question: Is there a way to position the rectangle relative to the page center?
  - answer: Aspose loads pages lazily, but if you’re processing thousands of pages,
      consider using `PdfExtractor` to work on subsets or stream the file to reduce
      memory footprint.
    question: Performance concerns for large PDFs?
  type: FAQPage
tags:
- pdf
- csharp
- aspose
- shape-manipulation
title: Menambahkan Persegi Panjang ke PDF dengan C# – Panduan Pemrograman Lengkap
url: /id/net/document-manipulation/add-rectangle-to-pdf-with-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tambahkan Persegi Panjang ke PDF dengan C# – Panduan Pemrograman Lengkap

Pernah perlu **menambahkan persegi panjang ke pdf** tetapi tidak yakin panggilan API mana yang harus digunakan? Anda tidak sendirian—banyak pengembang mengalami kebingungan ini saat pertama kali mencoba mengedit PDF secara programatik. Kabar baik? Dengan beberapa baris C# dan pustaka kuat Aspose.Pdf, Anda dapat menggambar persegi panjang pada halaman mana pun dari dokumen yang ada dalam sekejap.

Dalam panduan ini kami akan menelusuri cara memuat PDF yang ada, memilih halaman yang tepat, mendefinisikan persegi panjang yang sesuai, dan akhirnya menyisipkan bentuk ke dalam PDF. Pada akhir tutorial Anda akan memiliki potongan kode yang dapat digunakan kembali dan dapat disisipkan ke proyek .NET mana pun. Oh, dan kami juga akan menyentuh nuansa **draw rectangle on pdf** yang mungkin belum Anda pertimbangkan.

## Apa yang Akan Anda Dapatkan

- Solusi langkah‑demi‑langkah yang jelas dan langsung dapat dipakai.
- Pemahaman tentang cara **load existing pdf** dengan aman.
- Tips untuk **edit pdf page** tanpa merusak dokumen.
- Strategi untuk **insert shape into pdf** selain hanya persegi panjang.
- Kode C# siap‑jalankan yang dapat Anda salin‑tempel segera.

### Prasyarat

- .NET 6.0 atau lebih baru (kode ini juga berfungsi pada .NET Framework 4.6+).
- Paket NuGet Aspose.Pdf untuk .NET (`Install-Package Aspose.Pdf`).
- Familiaritas dasar dengan sintaks C# (tidak memerlukan pengetahuan PDF yang mendalam).

Jika Anda sudah memiliki semua itu, mari kita mulai.

![Contoh menambahkan persegi panjang ke PDF](add-rectangle-to-pdf.png "Tangkapan layar yang menunjukkan persegi panjang ditambahkan ke halaman PDF – add rectangle to pdf")

## Tambahkan Persegi Panjang ke PDF – Ikhtisar Langkah‑demi‑Langkah

Berikut contoh lengkap yang dapat dijalankan dan mengikuti urutan persis yang akan kami bahas:

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the existing PDF file
        Document doc = new Document("YOUR_DIRECTORY/input.pdf");

        // 2️⃣ Select the first page (pages are 1‑based)
        Page page = doc.Pages[1];

        // 3️⃣ Define a rectangle that fits inside the page bounds
        //    (xLL, yLL, xUR, yUR) – lower‑left & upper‑right corners
        Aspose.Pdf.Rectangle rect = new Aspose.Pdf.Rectangle(0, 0, 500, 700);

        // 4️⃣ Add the rectangle to the page – this draws the shape
        page.AddRectangle(rect);

        // 5️⃣ Save the modified PDF to a new file
        doc.Save("YOUR_DIRECTORY/output.pdf");
    }
}
```

Sekarang mari kita uraikan setiap baris agar Anda mengerti **mengapa** kami melakukan apa yang kami lakukan, bukan hanya **apa** yang dilakukan.

## Memuat Dokumen PDF yang Ada

### Mengapa pemuatan penting

Sebelum Anda dapat menggambar apa pun, PDF harus berada di memori. Konstruktor `Document` membaca file, mengurai struktur internalnya, dan memberi Anda model objek untuk bekerja. Jika file terkunci atau rusak, Aspose akan melemparkan pengecualian yang menjelaskan—sehingga Anda tahu persis apa yang salah.

### Kode

```csharp
Document doc = new Document("YOUR_DIRECTORY/input.pdf");
```

- Ganti `YOUR_DIRECTORY` dengan jalur absolut atau relatif ke file sumber Anda.
- Jalur dapat berupa URL jika Anda mengaktifkan pemuatan remote Aspose (skenario lanjutan).
- **Tip:** Bungkus ini dalam blok `try/catch` untuk menangani `FileNotFoundException` atau `PdfException` secara elegan.

```csharp
try
{
    Document doc = new Document("input.pdf");
}
catch (Exception ex)
{
    Console.WriteLine($"Failed to load PDF: {ex.Message}");
    return;
}
```

## Memilih dan Menyiapkan Halaman

### Mengapa pemilihan halaman krusial

PDF bersifat berorientasi halaman; setiap halaman memiliki sistem koordinatnya sendiri. Aspose menggunakan indeks **berbasis‑1**, yang sering membingungkan pengembang yang terbiasa dengan koleksi berbasis‑0. Memilih halaman yang salah dapat menyebabkan `ArgumentOutOfRangeException` atau memodifikasi halaman yang tidak diinginkan.

### Kode

```csharp
Page page = doc.Pages[1]; // First page
```

Jika Anda perlu bekerja pada halaman 3, cukup ubah indeks menjadi `3`. Untuk skenario dinamis, Anda dapat melakukan perulangan:

```csharp
foreach (Page pg in doc.Pages)
{
    // Apply rectangle to every page
}
```

## Mendefinisikan dan Menggambar Persegi Panjang pada PDF

### Memahami koordinat persegi panjang

Persegi panjang di Aspose.Pdf didefinisikan oleh sudut kiri‑bawah (`xLL`, `yLL`) dan sudut kanan‑atas (`xUR`, `yUR`). Sistem koordinat dimulai dari **kiri‑bawah** halaman, dengan X meningkat ke kanan dan Y meningkat ke atas. Ini berlawanan dengan banyak kerangka UI, jadi perhatikan sumbu‑sumbu tersebut.

- `0,0` adalah sudut kiri‑bawah halaman.
- Lebar = `xUR - xLL`; Tinggi = `yUR - yLL`.

Jika Anda secara tidak sengaja menetapkan persegi panjang yang lebih besar dari halaman, `AddRectangle` akan melempar pengecualian. Untuk menghindarinya, Anda dapat menanyakan ukuran halaman:

```csharp
double pageWidth  = page.PageInfo.Width;
double pageHeight = page.PageInfo.Height;
```

Lalu batasi persegi panjang Anda:

```csharp
double rectWidth  = Math.Min(500, pageWidth);
double rectHeight = Math.Min(700, pageHeight);
Aspose.Pdf.Rectangle rect = new Aspose.Pdf.Rectangle(0, 0, rectWidth, rectHeight);
```

### Kode untuk menambahkan bentuk

```csharp
Aspose.Pdf.Rectangle rect = new Aspose.Pdf.Rectangle(0, 0, 500, 700);
page.AddRectangle(rect);
```

- `AddRectangle` secara otomatis menggambar batas hitam tipis.
- Ingin persegi panjang berisi? Gunakan `page.AddAnnotation(new SquareAnnotation(page, rect) { FillColor = Color.Yellow });`.
- Perlu ketebalan garis berbeda? Setel `rect.LineWidth = 2;` sebelum menambahkan.

#### Kasus tepi: banyak persegi panjang

Jika Anda memanggil `AddRectangle` berulang kali, setiap pemanggilan menambahkan bentuk lain. Untuk menghindari tumpang tindih, geser persegi panjang berikutnya:

```csharp
for (int i = 0; i < 3; i++)
{
    var offset = i * 20;
    var r = new Aspose.Pdf.Rectangle(offset, offset, 500 + offset, 700 + offset);
    page.AddRectangle(r);
}
```

## Menyimpan PDF yang Telah Dimodifikasi

### Mengapa penyimpanan adalah langkah akhir

Semua manipulasi tetap berada di memori hingga Anda menyimpannya. `Document.Save` menulis konten baru ke disk (atau stream). Menimpa file asli memungkinkan, tetapi menyimpan cadangan (`output.pdf`) lebih aman.

### Kode

```csharp
doc.Save("YOUR_DIRECTORY/output.pdf");
```

- Anda juga dapat menyimpan ke `MemoryStream` jika perlu mengirim PDF melalui HTTP:

```csharp
using var ms = new MemoryStream();
doc.Save(ms);
byte[] pdfBytes = ms.ToArray();
// return File(pdfBytes, "application/pdf");
```

## Contoh Lengkap yang Siap Dijalan (Copy‑Paste)

Menggabungkan semuanya, berikut program akhir yang dapat Anda jalankan sekarang:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using Aspose.Pdf.Text;

class AddRectangleDemo
{
    static void Main()
    {
        const string inputPath  = "input.pdf";
        const string outputPath = "output.pdf";

        // Load the existing PDF
        Document doc;
        try
        {
            doc = new Document(inputPath);
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Error loading PDF: {ex.Message}");
            return;
        }

        // Ensure the document has at least one page
        if (doc.Pages.Count == 0)
        {
            Console.WriteLine("PDF contains no pages.");
            return;
        }

        // Select the first page (1‑based index)
        Page page = doc.Pages[1];

        // Get page dimensions to avoid overflow
        double pageW = page.PageInfo.Width;
        double pageH = page.PageInfo.Height;

        // Define rectangle size (clamp to page bounds)
        double rectW = Math.Min(500, pageW);
        double rectH = Math.Min(700, pageH);
        Aspose.Pdf.Rectangle rect = new Aspose.Pdf.Rectangle(0, 0, rectW, rectH);

        // Optional: set line width and color
        rect.LineWidth = 2;
        rect.Color = Color.Blue;

        // Add rectangle to the page
        page.AddRectangle(rect);

        // Save the result
        doc.Save(outputPath);
        Console.WriteLine($"Rectangle added and saved to {outputPath}");
    }
}
```

**Output yang diharapkan:** Buka `output.pdf` dan Anda akan melihat persegi panjang berpinggir biru yang ditempatkan di sudut kiri‑bawah halaman pertama, berukuran hingga 500 × 700 poin (atau lebih kecil jika halaman sangat kecil).

## Pertanyaan Umum & Tips Profesional

- **Bisakah saya menambahkan persegi panjang ke setiap halaman secara otomatis?**  
  Ya—lakukan perulangan pada `doc.Pages` dan ulangi pemanggilan `AddRectangle` untuk setiap objek `Page`.

- **Bagaimana jika saya perlu menggambar lingkaran atau poligon?**  
  Aspose menyediakan metode `AddCircle`, `AddPolygon`, dan `AddPolyline`. Logika persegi panjang yang sama berlaku untuk kotak pembatas.

- **Apakah ada cara menempatkan persegi panjang relatif ke tengah halaman?**  
  Hitung koordinat pusat:  
  ```csharp
  double centerX = pageW / 2;
  double centerY = pageH / 2;
  double halfW = rectW / 2;
  double halfH = rectH / 2;
  var centeredRect = new Aspose.Pdf.Rectangle(centerX - halfW, centerY - halfH,
                                              centerX + halfW, centerY + halfH);
  page.AddRectangle(centeredRect);
  ```

- **Kekhawatiran kinerja untuk PDF besar?**  
  Aspose memuat halaman secara lazy, tetapi jika Anda memproses ribuan halaman, pertimbangkan menggunakan `PdfExtractor` untuk bekerja pada subset atau streaming file guna mengurangi jejak memori.

## Kesimpulan

Anda kini tahu **cara menambahkan persegi panjang** ke PDF menggunakan C# dan Aspose.Pdf.

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Buat Dokumen PDF dengan Aspose.PDF – Tambah Halaman, Bentuk & Simpan](/pdf/english/net/document-creation/create-pdf-document-with-aspose-pdf-add-page-shape-save/)
- [Cara Menambahkan Stempel Halaman pada PDF Menggunakan Aspose.PDF untuk .NET: Panduan Lengkap](/pdf/english/net/watermarks-backgrounds/add-page-stamp-aspose-pdf-dotnet-guide/)
- [Tambahkan Gambar & Nomor Halaman ke PDF Menggunakan Aspose.PDF untuk .NET: Panduan Lengkap](/pdf/english/net/document-manipulation/enhance-pdfs-images-page-numbers-aspose-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}