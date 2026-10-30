---
category: general
date: 2026-09-27
description: Pelajari cara menambahkan persegi panjang ke PDF dalam C# saat Anda memuat
  dokumen PDF C# dan mengakses halaman pertama PDF dengan Aspose.Pdf.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add rectangle to pdf
- access first page pdf
- load pdf document c#
- add graphics pdf c#
language: id
lastmod: 2026-09-27
og_description: Tambahkan persegi panjang ke PDF di C# dengan memuat dokumen PDF dan
  mengakses halaman pertama PDF. Ikuti tutorial langkah demi langkah ini untuk hasil
  yang dapat diandalkan.
og_image_alt: Code editor showing how to add rectangle to PDF using C#
og_title: Tambahkan persegi panjang ke PDF di C# – panduan lengkap Aspose.Pdf
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Learn how to add rectangle to PDF in C# while you load PDF document
    C# and access first page PDF with Aspose.Pdf.
  headline: How to add rectangle to PDF in C# with Aspose.Pdf
  type: TechArticle
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Cara menambahkan persegi panjang ke PDF dalam C# dengan Aspose.Pdf
url: /id/net/images-graphics/how-to-add-rectangle-to-pdf-in-c-with-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara menambahkan persegi panjang ke PDF dalam C# dengan Aspose.Pdf

Jika Anda perlu **add rectangle to PDF** dalam aplikasi C#, panduan ini menunjukkan langkah-langkah tepat. Anda akan memuat dokumen PDF, mengakses halaman pertama, membuat bentuk persegi panjang, dan menulis perubahan kembali ke disk. Solusi ini bekerja dengan Aspose.Pdf .NET 2024‑R2 dan tidak memerlukan alat eksternal.

Menambahkan persegi panjang ke file PDF adalah kebutuhan umum untuk menyorot bagian, membuat overlay seperti formulir, atau membuat grafik sederhana. Dengan mengikuti kode di bawah ini Anda akan mendapatkan pola yang dapat digunakan kembali yang dapat Anda perluas dengan bentuk lain, warna, atau pengaturan opacity.

## Apa yang akan Anda pelajari

* Cara **load PDF document C#** menggunakan Aspose.Pdf.
* Cara **access first page PDF** dengan aman.
* Cara membuat persegi panjang dan **add rectangle to PDF**.
* Cara memverifikasi bahwa persegi panjang berada di dalam batas halaman.
* Cara menyimpan file yang diperbarui tanpa kehilangan konten yang ada.

Tutorial ini mengasumsikan Anda memiliki lingkungan pengembangan C# dasar (Visual Studio 2022 atau lebih baru) dan lisensi Aspose.Pdf yang valid. Tidak ada paket NuGet tambahan yang diperlukan selain `Aspose.Pdf`.

## Langkah 1: Load PDF document C#  

Memuat file sumber adalah operasi pertama. Aspose.Pdf membaca seluruh PDF ke dalam memori, memungkinkan Anda memanipulasi halaman, anotasi, dan grafik.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using System.Drawing;   // for Color

// Load the PDF document
Document doc = new Document("YOUR_DIRECTORY/input.pdf");
```

*Mengapa langkah ini penting* – Objek `Document` mewakili seluruh PDF. Jika file tidak dapat dibuka, sebuah pengecualian akan dilempar, jadi Anda harus memverifikasi jalur sebelum memanggil konstruktor dalam kode produksi.

## Langkah 2: Access first page PDF  

Halaman di Aspose.Pdf menggunakan indeks berbasis 1, sehingga halaman pertama diambil dengan indeks 1. Langkah ini menunjukkan frasa tepat **access first page PDF**.

```csharp
// Access the first page (pages are 1‑based)
Page page = doc.Pages[1];
```

*Mengapa ini penting* – Memanipulasi halaman yang tepat mencegah pengeditan tidak sengaja pada halaman berikutnya. Jika PDF tidak berisi halaman, `doc.Pages[1]` akan menghasilkan `ArgumentOutOfRangeException`, yang dapat Anda tangkap untuk memberikan pesan kesalahan yang ramah.

## Langkah 3: Create the rectangle shape  

Sekarang Anda mendefinisikan geometri persegi panjang yang ingin ditambahkan. Parameter konstruktor adalah `(x, y, width, height)` dimana asal `(0,0)` berada di sudut kiri-bawah halaman.

```csharp
// Define a rectangle shape (x, y, width, height)
Rectangle rect = new Rectangle(10, 10, 200, 200);

// Optional: customize the appearance
rect.GraphInfo = new GraphInfo
{
    Color = Color.Black,   // stroke color
    LineWidth = 2          // thickness in points
};
```

*Mengapa ini penting* – Menetapkan `GraphInfo` mengontrol bagaimana persegi panjang dirender. Tanpa itu, bentuk akan tidak terlihat karena garis default transparan.

## Langkah 4: Verify the rectangle fits within the page boundaries  

Sebelum menambahkan bentuk, Anda harus memastikan bahwa bentuk tidak melebihi ukuran halaman. Ini mencegah artefak rendering dan menjaga kepatuhan pada spesifikasi PDF.

```csharp
// Verify the rectangle fits within the page boundaries
if (page.Rect.Contains(rect))
{
    // Step 5 will run here
}
else
{
    // Adjust rectangle or log a warning
    throw new InvalidOperationException("Rectangle exceeds page dimensions.");
}
```

*Mengapa ini penting* – Pemeriksaan `Contains` menjamin bahwa persegi panjang sepenuhnya berada di dalam area yang dapat dicetak. Jika Anda melewatkan langkah ini dan persegi panjang meluber, beberapa penampil mungkin memotong bentuk atau melaporkan kesalahan.

## Langkah 5: Add rectangle to PDF  

Ketika pemeriksaan batas berhasil, Anda menambahkan persegi panjang ke halaman. Ini adalah tindakan inti yang memenuhi persyaratan **add rectangle to PDF**.

```csharp
// Add the rectangle to the page
page.Add(rect);
```

*Mengapa ini penting* – `page.Add` menyisipkan bentuk ke dalam aliran konten halaman. Persegi panjang menjadi bagian dari lapisan visual dan akan muncul di semua penampil PDF.

## Langkah 6: Save the updated PDF  

Akhirnya, tulis dokumen yang dimodifikasi kembali ke disk. Anda dapat menimpa file asli atau membuat yang baru.

```csharp
// Save the updated PDF
doc.Save("YOUR_DIRECTORY/output.pdf");
```

*Mengapa ini penting* – Menyimpan menyelesaikan semua perubahan. Jika Anda perlu mempertahankan file asli, pilih jalur output yang berbeda seperti yang ditunjukkan.

## Contoh lengkap yang dapat dijalankan

Berikut adalah program konsol mandiri yang menggabungkan setiap langkah. Salin kode ke dalam proyek C# baru, sesuaikan jalur file, dan jalankan.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using System.Drawing;

class AddRectangleExample
{
    static void Main()
    {
        // Load the PDF document (load pdf document c#)
        Document doc = new Document("YOUR_DIRECTORY/input.pdf");

        // Access first page PDF
        Page page = doc.Pages[1];

        // Create a rectangle shape
        Rectangle rect = new Rectangle(10, 10, 200, 200);
        rect.GraphInfo = new GraphInfo
        {
            Color = Color.Black,
            LineWidth = 2
        };

        // Verify bounds before adding
        if (page.Rect.Contains(rect))
        {
            // Add rectangle to PDF
            page.Add(rect);
        }
        else
        {
            System.Console.WriteLine("Rectangle does not fit on the page.");
            return;
        }

        // Save the result
        doc.Save("YOUR_DIRECTORY/output.pdf");

        System.Console.WriteLine("Rectangle added successfully.");
    }
}
```

**Output yang diharapkan** – Setelah eksekusi, `output.pdf` berisi konten asli plus persegi panjang berpinggir hitam yang ditempatkan 10 pt dari sudut kiri‑bawah. Membuka file di Adobe Acrobat atau penampil PDF apa pun menampilkan overlay persegi panjang pada halaman pertama.

## Menangani variasi umum

| Situasi | Perubahan yang disarankan |
|-----------|--------------------|
| Ukuran halaman berbeda (mis., A4 vs. Letter) | Gunakan `page.Rect.Width` dan `page.Rect.Height` untuk menghitung persegi panjang yang secara dinamis sesuai. |
| Anda membutuhkan persegi panjang terisi | Set `rect.GraphInfo.FillColor = Color.LightGray;` dan opsional `rect.GraphInfo.IsFilled = true;`. |
| Beberapa halaman memerlukan persegi panjang yang sama | Lakukan loop pada `doc.Pages` dan ulangi operasi penambahan untuk setiap halaman. |
| Transparansi diperlukan | Set `rect.GraphInfo.Transparency = 0.5;` (rentang 0–1). |

Variasi ini menggambarkan bagaimana pendekatan **add graphics pdf c#** dapat diskalakan melampaui satu bentuk.

## Tips profesional

* **Tips kinerja** – Saat memproses PDF besar, gunakan kembali satu instance `Document` dan hindari memanggil `Save` di dalam loop. Simpan sekali setelah semua halaman diproses.
* **Penanganan error** – Bungkus seluruh alur dalam blok `try/catch` untuk menangkap `FileNotFoundException`, `InvalidOperationException`, dan `PdfException` khusus Aspose.
* **Lisensi** – Daftarkan lisensi Aspose.Pdf Anda sebelum membuat `Document` untuk menghindari watermark evaluasi.

## Kesimpulan

Anda sekarang tahu cara **add rectangle to PDF** dalam C# dengan memuat sebuah

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang membangun pada teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Create PDF Document in C# – Add Page to PDF & Rectangle](/pdf/english/net/programming-with-pdf-pages/create-pdf-document-in-c-add-page-to-pdf-rectangle/)
- [Create PDF Document C# – Add Blank Page & Draw Rectangle](/pdf/english/net/document-creation/create-pdf-document-c-add-blank-page-draw-rectangle/)
- [Create PDF Document C# – Add Page, Draw Rectangle & Save](/pdf/english/net/document-creation/create-pdf-document-c-add-page-draw-rectangle-save/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}