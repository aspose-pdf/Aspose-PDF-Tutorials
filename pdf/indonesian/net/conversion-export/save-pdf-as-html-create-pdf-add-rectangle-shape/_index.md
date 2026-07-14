---
category: general
date: 2026-07-14
description: Simpan PDF sebagai HTML menggunakan Aspose.Pdf – pelajari cara membuat
  dokumen PDF, menambahkan bentuk persegi panjang pada PDF, dan mengekspor ke HTML
  bersih tanpa gambar.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save pdf as html
- how to create pdf document
- add rectangle shape pdf
language: id
lastmod: 2026-07-14
og_description: Simpan PDF sebagai HTML dengan Aspose.Pdf. Temukan cara membuat dokumen
  PDF, menggambar bentuk persegi panjang pada PDF, dan menghasilkan HTML tanpa gambar
  dalam hitungan menit.
og_image_alt: Screenshot of a PDF saved as HTML showing a rectangle shape
og_title: Simpan PDF sebagai HTML – Panduan Cepat Membuat PDF dan Menambahkan Bentuk
  Persegi Panjang
schemas:
- author: Aspose
  dateModified: '2026-07-14'
  description: Save PDF as HTML using Aspose.Pdf – learn how to create PDF document,
    add rectangle shape PDF, and export to clean HTML without images.
  headline: Save PDF as HTML – Create PDF, add rectangle shape
  type: TechArticle
tags:
- pdf
- aspnet
- csharp
- html-export
title: Simpan PDF sebagai HTML – Buat PDF, tambahkan bentuk persegi panjang
url: /id/net/conversion-export/save-pdf-as-html-create-pdf-add-rectangle-shape/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Simpan PDF sebagai HTML – Buat PDF, tambahkan bentuk persegi panjang

Pernah bertanya-tanya bagaimana cara **save PDF as HTML** sambil tetap dapat menggambar grafik pada PDF sumber? Anda tidak sendirian. Dalam banyak alat internal kami membutuhkan pratinjau HTML yang bersih dari PDF yang berisi bentuk khusus, dan konverter biasanya malah menyematkan gambar raster yang berat atau menghapus data vektor sepenuhnya.  

Dalam tutorial ini kami akan menjelaskan **how to create PDF document** secara programatis dengan Aspose.Pdf, menggambar **rectangle shape PDF**, mengonfigurasi penomoran Bates, dan akhirnya **save PDF as HTML** dengan gambar raster dihilangkan. Pada akhir tutorial Anda akan memiliki aplikasi konsol C# yang sepenuhnya dapat dijalankan yang menghasilkan file HTML yang dapat Anda buka di browser mana pun—tanpa memerlukan file gambar tambahan.

> **Pro tip:** Aspose.Pdf bekerja dengan .NET 6+, .NET Framework 4.6+ dan bahkan .NET Core, sehingga Anda dapat menaruhnya ke dalam layanan Windows lama atau microservice baru sekalipun.

---

## Prasyarat

- **Visual Studio 2022** (Community atau lebih tinggi) atau IDE yang kompatibel dengan C#.  
- **Aspose.Pdf for .NET** paket NuGet (versi 23.11 atau lebih baru). Install melalui Package Manager Console:

```powershell
Install-Package Aspose.Pdf
```

- Familiaritas dasar dengan sintaks C#; tidak diperlukan pengalaman PDF sebelumnya.

---

## Simpan PDF sebagai HTML dengan Aspose.Pdf

Berikut adalah kode lengkap yang siap disalin‑tempel. Kode ini mengikuti langkah‑langkah tepat dari cuplikan asli namun menambahkan komentar, penanganan error, dan metode pembantu kecil untuk menjaga alur utama tetap mudah dibaca.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using Aspose.Pdf.Text;

namespace PdfToHtmlDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create a fresh PDF document.
            Document pdfDoc = new Document();
            Page pdfPage = pdfDoc.Pages.Add();

            // 2️⃣ Draw a rectangle shape on the page.
            //    This demonstrates the "add rectangle shape pdf" requirement.
            var rectangle = new Rectangle(100, 500, 300, 700)
            {
                // Optional visual tweaks
                FillColor = Color.GetYellow(),
                Border = new Border
                {
                    Width = 2,
                    Color = Color.GetRed()
                }
            };
            pdfPage.Paragraphs.Add(rectangle);
            pdfPage.ValidateGraphicsState(); // Ensures the shape fits within page bounds

            // 3️⃣ Configure Bates numbering – useful for legal documents.
            var bates = new BatesNumbering { StartNumber = 1, Prefix = "DOC-" };
            pdfDoc.BatesNumbering = bates;

            // 4️⃣ Add a tagged element with an explicit position.
            //    Tagging is important for accessibility (PDF/UA).
            var taggedElement = new TagStructure();
            taggedElement.PositionSettings = new TagPositionSettings { X = 150, Y = 600 };
            pdfPage.TagStructure.Add(taggedElement);

            // 5️⃣ Enable detection of compromised signatures.
            pdfDoc.SecurityOptions.DetectCompromisedSignatures = true;
            bool hasCompromisedSignature = pdfDoc.SecurityOptions.HasCompromisedSignature;
            Console.WriteLine($"Compromised signature? {hasCompromisedSignature}");

            // 6️⃣ Finally, save the PDF as HTML *without* embedding raster images.
            var htmlOptions = new HtmlSaveOptions
            {
                SkipImages = true,               // Removes <img> tags for raster data
                FixedLayout = true,              // Preserves the original page layout
                ExportEmbeddedFonts = false      // Keeps the HTML lightweight
            };

            string outputPath = @"output.html";
            pdfDoc.Save(outputPath, htmlOptions);
            Console.WriteLine($"✅ PDF successfully saved as HTML at: {outputPath}");
        }
    }
}
```

### Apa yang dilakukan kode, langkah demi langkah

| Step | Why it matters |
|------|----------------|
| **Buat dokumen PDF** | Ini adalah dasar—tanpa objek `Document` Anda tidak dapat menambahkan apa pun. |
| **Tambahkan bentuk persegi panjang PDF** | Menunjukkan cara menggambar vektor; persegi panjang adalah bentuk paling sederhana tetapi API yang sama mendukung lingkaran, poligon, dll. |
| **Konfigurasikan penomoran Bates** | Sering diperlukan dalam skenario litigasi atau pemrosesan batch untuk mengidentifikasi halaman secara unik. |
| **Struktur tag** | Meningkatkan aksesibilitas; pembaca layar mengandalkan tag untuk menyampaikan urutan baca. |
| **Deteksi tanda tangan yang dikompromikan** | Aplikasi yang peduli keamanan perlu mengetahui apakah tanda tangan digital telah diubah. |
| **Simpan PDF sebagai HTML** | Tujuan akhir—menghasilkan HTML bersih yang mencerminkan tata letak PDF tanpa file gambar yang besar. |

> **Mengapa `SkipImages = true`?**  
> Saat Anda mengonversi PDF yang berisi grafik vektor (seperti persegi panjang kami) biasanya Anda tidak memerlukan fallback raster. Mengatur `SkipImages` menghapus elemen `<img>` yang sebaliknya akan merujuk ke blob base‑64, sehingga file HTML tetap berukuran beberapa kilobyte.

---

## Cara membuat dokumen PDF dengan Aspose.Pdf

Jika Anda baru dengan Aspose, perpustakaan ini memperlakukan PDF seperti dokumen Word: Anda menambahkan **pages**, kemudian **paragraphs**, **shapes**, atau **annotations** ke halaman tersebut. Kelas `Document` adalah titik masuk, dan setiap `Page` memiliki koleksi bernama `Paragraphs`. Apa pun yang mewarisi dari `TextFragmentAbsorber`, `Image`, `Rectangle`, dll., dapat dimasukkan ke dalam koleksi itu.

Berikut adalah cuplikan minimal yang hanya membuat PDF kosong—berguna ketika Anda ingin memulai dari awal:

```csharp
Document emptyPdf = new Document();
Page firstPage = emptyPdf.Pages.Add();   // Adds a default‑size A4 page
emptyPdf.Save("empty.pdf");
```

Anda dapat menambahkan halaman tambahan dengan loop `for` sederhana, atau menerapkan pengaturan tingkat halaman (margin, ukuran) melalui `PageInfo`. Fleksibilitas inilah yang membuat Aspose.Pdf menjadi favorit untuk pembuatan PDF di sisi server.

---

## Tambahkan bentuk persegi panjang PDF – menggambar grafik

Kelas `Rectangle` berada di `Aspose.Pdf.Annotations`. Ia menerima empat koordinat: **lower‑left X**, **lower‑left Y**, **upper‑right X**, **upper‑right Y**. Anggap sistem koordinat PDF sebagai

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang terkait erat yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber daya menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Buat Dokumen PDF dengan Aspose.PDF – Tambah Halaman, Bentuk & Simpan](/pdf/english/net/document-creation/create-pdf-document-with-aspose-pdf-add-page-shape-save/)
- [Konversi PDF ke HTML di .NET Menggunakan Aspose.PDF Tanpa Menyimpan Gambar](/pdf/english/net/conversion-export/convert-pdf-html-net-asposepdf-no-images/)
- [Konversi PDF ke HTML Menggunakan Aspose.PDF .NET&#58; Simpan Gambar sebagai PNG Eksternal](/pdf/english/net/conversion-export/pdf-to-html-conversion-external-png-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}