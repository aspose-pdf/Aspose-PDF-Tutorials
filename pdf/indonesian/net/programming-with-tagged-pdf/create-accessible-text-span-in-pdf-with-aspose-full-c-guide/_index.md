---
category: general
date: 2026-06-05
description: Buat rentang teks yang dapat diakses dalam PDF menggunakan Aspose.PDF
  dan pelajari cara mengonversi PDF ke PDF/X-4. Ikuti tutorial C# langkah demi langkah
  ini untuk penanganan dokumen yang kuat.
draft: false
keywords:
- create accessible text span
- convert pdf to pdf/x-4
- how to convert pdf to pdfx4
language: id
og_description: Buat rentang teks yang dapat diakses dalam PDF dan temukan cara mengonversi
  PDF ke PDF/X-4 menggunakan Aspose.PDF. Tutorial ini memandu Anda melalui setiap
  langkah.
og_title: Buat Rentang Teks yang Aksesibel di PDF – Panduan Lengkap C#
schemas:
- author: Aspose
  dateModified: '2026-06-05'
  description: Create accessible text span in a PDF using Aspose.PDF and learn how
    to convert PDF to PDF/X-4. Follow this step‑by‑step C# tutorial for robust document
    handling.
  headline: 'Create Accessible Text Span in PDF with Aspose: Full C# Guide'
  type: TechArticle
tags:
- Aspose.PDF
- C#
- PDF manipulation
title: 'Buat Span Teks Aksesibel dalam PDF dengan Aspose: Panduan Lengkap C#'
url: /id/net/programming-with-tagged-pdf/create-accessible-text-span-in-pdf-with-aspose-full-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat Span Teks yang Dapat Diakses dalam PDF dengan Aspose: Panduan Lengkap C#

Pernahkah Anda perlu **membuat span teks yang dapat diakses** dalam PDF tetapi tidak yakin harus mulai dari mana? Anda tidak sendirian—banyak pengembang mengalami kebuntuan ini saat pertama kali mencoba mengaksesibilitas PDF. Kabar baiknya, Aspose.PDF membuatnya sangat mudah, dan sekaligus Anda juga dapat belajar **cara mengonversi PDF ke PDF/X-4** dalam satu proses.

Dalam tutorial ini kami akan memuat PDF yang sudah ada, menampilkan daftar tanda tangan digitalnya, mengonversi file ke PDF/X‑4, menambahkan span teks yang dapat diakses pada posisi tertentu, menyisipkan field formulir multi‑halaman, mengekspor ke HTML tanpa gambar raster, dan akhirnya memvalidasi tanda tangan terhadap server CA. Pada akhir tutorial Anda akan memiliki satu program C# yang berdiri sendiri yang melakukan semua itu—tanpa potongan kode terpisah, tanpa shortcut “lihat dokumen”.

## Prasyarat

- .NET 6.0 atau lebih baru (kode ini juga dapat dikompilasi pada .NET Framework 4.7+).  
- Lisensi Aspose.PDF for .NET yang valid (versi percobaan gratis berfungsi, tetapi Anda akan mencapai batas setelah beberapa halaman).  
- Sebuah PDF masukan bernama `input.pdf` yang ditempatkan di folder yang Anda kontrol (ganti `YOUR_DIRECTORY` dengan path yang sebenarnya).  
- Pemahaman dasar tentang aplikasi konsol C#—tidak ada yang rumit, hanya metode `Main`.

Sudah semua? Bagus—mari kita mulai.

## Buat Span Teks yang Dapat Diakses dengan Aspose.PDF

Tujuan konkret pertama adalah **membuat span teks yang dapat diakses** di dalam konten bertag PDF. PDF bertag adalah tulang punggung aksesibilitas; mereka memungkinkan pembaca layar memahami urutan bacaan logis.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Facades;
using Aspose.Pdf.Forms;
using Aspose.Pdf.Devices;
using System.Drawing;

// Load the source PDF
var sourcePdf = new Document("YOUR_DIRECTORY/input.pdf");

// Create a positioned span element
var positionedSpan = sourcePdf.TaggedContent.CreateSpanElement();
positionedSpan.SetPosition(150, 500);          // X=150, Y=500 points from bottom‑left
positionedSpan.Text = "Accessible positioned text";

// Append the span to the root of the tagged tree
sourcePdf.TaggedContent.RootElement.AppendChild(positionedSpan);
```

**Mengapa ini penting:** Dengan menempelkan span ke `TaggedContent.RootElement`, Anda menjamin bahwa teknologi bantu melihatnya sebagai bagian dari struktur logis, bukan sekadar overlay visual. Pemanggilan `SetPosition` memungkinkan Anda menempatkan teks tepat di lokasi yang dibutuhkan—sempurna untuk menambahkan keterangan di atas gambar atau diagram.

> **Pro tip:** Jika PDF Anda sudah berisi pohon `DocumentStructure`, Anda dapat menyisipkan span di bawah node `Paragraph` atau `Section` tertentu untuk mempertahankan hierarki.

## Konversi PDF ke PDF/X-4 Menggunakan Aspose

Sekarang setelah bagian aksesibilitas sudah siap, mari kita selesaikan kebutuhan **mengonversi pdf ke pdf/x-4**. PDF/X‑4 adalah subset yang dirancang untuk pencetakan yang dapat diandalkan; ia menyematkan semua font dan mendukung transparansi.

```csharp
// Define conversion options: target PDF/X‑4 and delete any conversion errors
var conversionOptions = new PdfFormatConversionOptions(
    PdfFormat.PDF_X_4,            // Target format
    ConvertErrorAction.Delete); // Remove problematic objects

// Perform the conversion in‑place
sourcePdf.Convert(conversionOptions);

// Save the converted file
sourcePdf.Save("YOUR_DIRECTORY/converted_pdfx4.pdf");
```

**Mengapa Anda melakukannya:** Mengonversi ke PDF/X‑4 menghapus elemen yang dapat menyebabkan gangguan pencetakan (seperti profil warna yang tidak didukung). Flag `ConvertErrorAction.Delete` memastikan konversi tidak pernah berhenti—setiap objek yang bermasalah hanya dihapus, sehingga file tetap dapat digunakan.

> **Edge case:** Jika Anda perlu menjaga file asli tetap tidak tersentuh, kloning dulu (`var clone = sourcePdf.Clone();`) dan jalankan konversi pada klon tersebut.

## Daftar Tanda Tangan Digital dan Periksa Status Kompromi

Sebelum kami mengutak‑atik dokumen lebih jauh, bijaksana untuk melihat tanda tangan apa saja yang sudah tertanam. Langkah ini tidak sepenuhnya tentang aksesibilitas, tetapi menunjukkan cara **cara mengonversi pdf ke pdfx4** dengan aman—tanpa merusak tanda tangan yang ada.

```csharp
// Retrieve signature information
var signatures = sourcePdf.DigitalSignatures.GetSignatureInfo();

foreach (var sig in signatures)
{
    Console.WriteLine($"{sig.Name} compromised? {sig.IsCompromised}");
}
```

Jika `IsCompromised` mengembalikan `true`, Anda mungkin ingin menandatangani ulang setelah konversi, karena PDF/X‑4 dapat membuat beberapa jenis tanda tangan menjadi tidak valid.

## Tambahkan Field Form TextBox Multi‑Halaman

Skenario dunia nyata yang umum adalah formulir yang melintasi beberapa halaman—misalnya kotak “Komentar” yang muncul di setiap halaman. Berikut cara membuat `TextBoxField` dan menempelkan widget ke dua halaman yang berbeda.

```csharp
// Create a TextBox on page 1 (pages are 1‑based)
var textBox = new TextBoxField(sourcePdf.Pages[1],
    new Rectangle(100, 700, 300, 730)); // left, bottom, right, top

// Add a second widget on page 2
textBox.AddWidget(sourcePdf.Pages[2],
    new Rectangle(50, 600, 250, 630));

// Register the field in the form collection
sourcePdf.Form.Add(textBox, "MultiWidgetField");
```

**Mengapa menggunakan banyak widget:** Setiap widget mewakili instance visual dari field logis yang sama. Pengguna mengisi salah satu instance, dan nilai tersebut menyebar ke seluruh halaman—sempurna untuk survei panjang.

## Simpan sebagai HTML Sambil Melewatkan Gambar Raster

Kadang Anda membutuhkan versi PDF yang siap untuk web, tetapi tidak ingin gambar raster yang berat membebani halaman. Cuplikan berikut menunjukkan cara **mengonversi pdf ke pdf/x-4**‑style output sambil mengekspor ke HTML dan menghilangkan gambar.

```csharp
var htmlOptions = new HtmlSaveOptions
{
    SkipImages = true          // Do not embed raster images
};

sourcePdf.Save("YOUR_DIRECTORY/output.html", htmlOptions);
```

`output.html` yang dihasilkan hanya berisi grafik vektor dan teks, sehingga sangat cepat dimuat di browser.

## Validasi Tanda Tangan Digital melalui Server CA

Akhirnya, mari verifikasi tanda tangan yang tertanam terhadap Certificate Authority (CA). Langkah ini memperlihatkan **cara mengonversi pdf ke pdfx4** dengan aman—dengan memastikan tanda tangan tetap dapat dipercaya setelah semua transformasi.

```csharp
var validator = new SignatureValidator(sourcePdf);
bool isCaValid = validator.ValidateWithCaServer("https://ca.mycompany.com/validate");

Console.WriteLine($"CA validation result: {isCaValid}");
```

Jika server CA mengembalikan `false`, Anda perlu menandatangani ulang PDF setelah langkah konversi. `SignatureValidator` milik Aspose menyederhanakan proses validasi rantai sertifikat.

## Contoh Lengkap yang Berfungsi

Menggabungkan semua bagian, berikut program lengkap yang dapat Anda salin‑tempel ke proyek konsol:

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Facades;
using Aspose.Pdf.Forms;
using Aspose.Pdf.Devices;
using System.Drawing;

class Demo
{
    static void Main()
    {
        // 1️⃣ Load the source PDF
        var sourcePdf = new Document("YOUR_DIRECTORY/input.pdf");

        // 2️⃣ List existing digital signatures
        var signatures = sourcePdf.DigitalSignatures.GetSignatureInfo();
        foreach (var sig in signatures)
            Console.WriteLine($"{sig.Name} compromised? {sig.IsCompromised}");

        // 3️⃣ Convert to PDF/X‑4 (how to convert pdf to pdfx4)
        var conversionOptions = new PdfFormatConversionOptions(
            PdfFormat.PDF_X_4,
            ConvertErrorAction.Delete);
        sourcePdf.Convert(conversionOptions);
        sourcePdf.Save("YOUR_DIRECTORY/converted_pdfx4.pdf");

        // 4️⃣ Create an accessible positioned text span
        var positionedSpan = sourcePdf.TaggedContent.CreateSpanElement();
        positionedSpan.SetPosition(150, 500);
        positionedSpan.Text = "Accessible positioned text";
        sourcePdf.TaggedContent.RootElement.AppendChild(positionedSpan);

        // 5️⃣ Add a TextBox form field with widgets on two pages
        var textBox = new TextBoxField(sourcePdf.Pages[1],
            new Rectangle(100, 700, 300, 730));
        textBox.AddWidget(sourcePdf.Pages[2],
            new Rectangle(50, 600, 250, 630));
        sourcePdf.Form.Add(textBox, "MultiWidgetField");

        // 6️⃣ Export to HTML, skipping raster images
        var htmlOptions = new HtmlSaveOptions { SkipImages = true };
        sourcePdf.Save("YOUR_DIRECTORY/output.html", htmlOptions);

        // 7️⃣ Validate the signature against a CA server
        var validator = new SignatureValidator(sourcePdf);
        bool isCaValid = validator.ValidateWithCaServer("https://ca.mycompany.com/validate");
        Console.WriteLine($"CA validation result: {isCaValid}");
    }
}
```

**Output yang diharapkan** (konsol):

```
John Doe compromised? False
CA validation result: True
```

Anda juga akan melihat tiga file baru di `YOUR_DIRECTORY`:

- `converted_pdfx4.pdf` – versi PDF/X‑4.  
- `output.html` – HTML tanpa gambar raster.  
- File asli `input.pdf` kini berisi span teks yang dapat diakses dan field formulir.

## Kesalahan Umum & Cara Menghindarinya

| Masalah | Mengapa terjadi | Solusi |
|-------|----------------|-----|
| **Tanda tangan menjadi tidak valid setelah konversi** | PDF/X‑4 menghapus objek tertentu yang dibutuhkan tanda tangan. | Tanda tangan ulang setelah langkah `Convert`, atau gunakan `ConvertErrorAction.Keep` jika Anda harus mempertahankan objek asli. |
| **Konten bertag tidak dikenali** | Anda menempelkan span ke node yang salah. | Selalu tempelkan ke `TaggedContent.RootElement` *atau* elemen struktural spesifik (mis., `Paragraph`). |
| **Ekspor HTML masih berisi gambar** | `SkipImages` hanya melewatkan gambar raster, bukan grafik vektor. | Untuk output yang hanya teks, juga atur `RasterImagesCompression = RasterImagesCompression.None`. |
| **Validasi CA gagal karena masalah jaringan** | Validator dapat |

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Buat PDF Tagged yang Dapat Diakses Menggunakan Aspose.PDF untuk .NET: Tingkatkan Judul, Teks Alt, dan Tata Letak](/pdf/english/net/advanced-features/enhanced-tagged-pdfs-aspose-pdf-dot-net/)
- [Cara Memutar Teks dalam PDF Menggunakan Aspose.PDF untuk .NET: Panduan Langkah demi Langkah](/pdf/english/net/text-operations/rotate-text-aspose-pdf-net-guide/)
- [Cara Membuat Halaman Bookmark dalam PDF Menggunakan Aspose.PDF untuk .NET: Panduan Langkah demi Langkah](/pdf/english/net/bookmarks-navigation/create-pdf-bookmarks-aspose-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}