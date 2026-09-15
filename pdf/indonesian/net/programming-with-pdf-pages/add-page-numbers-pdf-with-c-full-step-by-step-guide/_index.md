---
category: general
date: 2026-01-02
description: Tambahkan nomor halaman PDF dengan cepat menggunakan Aspose.Pdf di C#.
  Pelajari cara menambahkan penomoran Bates, teks footer, watermark khusus, dan mengulang
  halaman PDF dalam satu skrip.
draft: false
keywords:
- add page numbers pdf
- add bates numbering
- add footer text
- add custom watermark
- loop through pdf pages
language: id
og_description: Tambahkan nomor halaman PDF secara instan dengan Aspose.Pdf. Panduan
  ini juga mencakup penambahan penomoran Bates, teks footer, watermark khusus, dan
  iterasi halaman PDF.
og_title: Menambahkan nomor halaman pada PDF dengan C# – Tutorial Pemrograman Lengkap
tags:
- C#
- Aspose.Pdf
- PDF manipulation
title: Menambahkan nomor halaman PDF dengan C# – Panduan Lengkap Langkah demi Langkah
url: /id/net/programming-with-pdf-pages/add-page-numbers-pdf-with-c-full-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tambahkan nomor halaman pdf dengan C# – Tutorial Pemrograman Lengkap

Pernah perlu **menambahkan nomor halaman pdf** tetapi tidak yakin harus mulai dari mana? Anda bukan satu-satunya—para pengembang terus menanyakan cara menempelkan nomor, footer, atau bahkan pengidentifikasi gaya Bates pada setiap halaman PDF.

Dalam tutorial ini Anda akan melihat contoh C# yang siap dijalankan yang **mengulang halaman pdf**, menempelkan footer nomor halaman, dan (jika diinginkan) menambahkan watermark khusus. Kami juga akan menunjukkan cara mengubah stempel menjadi nomor Bates, yang pada dasarnya berarti “menambahkan penomoran bates” untuk dokumen hukum atau forensik. Pada akhir tutorial, Anda akan memiliki satu metode yang dapat digunakan kembali untuk menangani semua tugas ini tanpa kesulitan.

## Tambahkan nomor halaman pdf – Ikhtisar

Sebelum kita masuk ke kode, mari klarifikasi apa arti “tambahkan nomor halaman pdf” di dunia Aspose.Pdf. Library menata setiap potongan teks yang Anda tempatkan pada halaman sebagai **TextStamp**. Dengan membuat satu stempel dengan placeholder halaman (`{page}`) dan menerapkannya ke setiap halaman, Anda secara otomatis mendapatkan penomoran berurutan. Stempel yang sama dapat membawa teks tambahan, sehingga Anda dapat **menambahkan teks footer** seperti “Confidential” atau identifier khusus kasus.

> **Mengapa menggunakan stamp alih-alih mengedit aliran konten PDF?**
> Stempel adalah objek tingkat tinggi yang menghormati margin halaman, rotasi, dan grafis yang ada. Mereka juga jauh lebih mudah dipelihara—cukup mengubah beberapa properti dan menjalankan kembali skrip.

## Ulangi halaman PDF untuk menerapkan prangko

Langkah praktis pertama adalah membuka sumber PDF dan mengiterasi halamannya. Ini adalah pola **loop through pdf page** klasik yang digunakan kebanyakan contoh Aspose.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Paths – change these to match your environment
string sourcePdfPath = @"C:\Docs\input.pdf";
string outputPdfPath = @"C:\Docs\PageNumbered.pdf";

using (var pdfDocument = new Document(sourcePdfPath))
{
    // The loop – every Page object lives in pdfDocument.Pages
    foreach (Page page in pdfDocument.Pages)
    {
        // We'll attach a stamp later (see next section)
    }

    // Save the modified document
    pdfDocument.Save(outputPdfPath);
}
```

> **Tips pro:** Jika PDF Anda sangat besar (ratusan halaman), memprosesnya dalam batch untuk menjaga penggunaan memori tetap rendah. Aspose.Pdf memuat halaman dengan malas, sehingga loop itu sendiri sudah cukup efisien.

## Tambahkan penomoran bates dan teks footer

Sekarang kita dapat melintasi setiap halaman, mari buat **TextStamp** yang dapat digunakan kembali yang memuat nomor halaman dan teks footer opsional. Placeholder `{page}` secara otomatis diganti dengan indeks halaman saat ini.

```csharp
// Create a stamp that will be reused for every page
var batesStamp = new TextStamp("Bates-{page} – Confidential")
{
    // Position the stamp 20 points from the left and bottom edges
    XIndent = 20,
    YIndent = 20,
    // Align left‑bottom so it behaves like a traditional footer
    HorizontalAlignment = HorizontalAlignment.Left,
    VerticalAlignment   = VerticalAlignment.Bottom,
    // Font styling – Times New Roman, 10pt, bold, gray
    Font = new Font(FontFamily.TimesRoman, 10, FontStyle.Bold),
    TextState = { ForegroundColor = Color.Gray }
};

// Attach the stamp to every page
foreach (Page page in pdfDocument.Pages)
    page.AddStamp(batesStamp);
```

### Mengapa ini berhasil

* **`Bates-{page}`** – Asumsikan mengganti `{page}` dengan nomor halaman sebenarnya, memberi Anda nomor Bates klasik secara otomatis.
* **`Confidential`** – Ini adalah bagian **tambahkan teks footer**. Anda dapat menggantinya dengan string apa pun, bahkan menarik data dari basis data.
* **Styling** – Menggunakan `TextState` memungkinkan Anda menyesuaikan warna, opacity, dan bahkan rotasi tanpa menyentuh aliran konten internal PDF.

Jika Anda hanya membutuhkan angka biasa, hapus awalan “Bates‑” dan teks tambahan:

```csharp
var simpleStamp = new TextStamp("{page}")
{
    XIndent = 20,
    YIndent = 20,
    HorizontalAlignment = HorizontalAlignment.Center,
    VerticalAlignment   = VerticalAlignment.Bottom,
    Font = new Font(FontFamily.Helvetica, 12, FontStyle.Regular),
    TextState = { ForegroundColor = Color.Black }
};
```

## Tambahkan tanda air khusus (opsional)

Kadang-kadang Anda menginginkan lebih dari footer—Anda membutuhkan logo semi-transparan atau overlay “DRAFT” di seluruh halaman. Di sini **tambahkan tanda air khusus** ikut serta. Kelas `TextStamp` yang sama dapat dipakai kembali, cukup ubah penyelarasan dan opacity-nya.

```csharp
var watermark = new TextStamp("DRAFT")
{
    // Center it both horizontally and vertically
    HorizontalAlignment = HorizontalAlignment.Center,
    VerticalAlignment   = VerticalAlignment.Center,
    // Make it big and light
    Font = new Font(FontFamily.Helvetica, 72, FontStyle.Bold),
    TextState = { ForegroundColor = Color.Red, FontSize = 72, FontStyle = FontStyle.Bold, 
                  Transparency = 0.5f }   // 50% transparent
};

// Apply the watermark on top of the page‑number stamp
foreach (Page page in pdfDocument.Pages)
{
    page.AddStamp(watermark);   // watermark on top
    page.AddStamp(batesStamp);  // then the footer
}
```

> **Catatan:** Urutan penting. Menambahkan watermark terlebih dahulu memastikan nomor halaman tetap terbaca di atas teks semi‑transparan.

## Simpan PDF dan verifikasi hasilnya

Setelah stamping, langkah terakhir adalah menulis perubahan kembali ke disk. Panggilan `Save` yang kami tempatkan sebelumnya melakukan pekerjaan berat, tetapi mari tambahkan cuplikan verifikasi cepat yang membuka file baru dan mencetak berapa banyak halaman yang diproses.

```csharp
pdfDocument.Save(outputPdfPath);

// Quick verification
using (var resultDoc = new Document(outputPdfPath))
{
    Console.WriteLine($"✅ Successfully added page numbers to {resultDoc.Pages.Count} pages.");
}
```

Saat Anda menjalankan program lengkap, Anda akan melihat PDF di mana setiap halaman diakhiri dengan sesuatu seperti **“Bates‑3 – Confidential”** (atau hanya “3” jika Anda menggunakan stempel sederhana) dan, jika Anda mengaktifkan watermark, “DRAFT” samar di tengah.

### Hasil yang diharapkan

| Halaman | Catatan Kaki (contoh) |
|---------|-----------------|
| 1 | Bates‑1 – Rahasia |
| 2 | Bates‑2 – Rahasia |
| … | … |
| tidak | Bates‑N – Rahasia |

Jika Anda membuka file di penampil, angka-angka akan berada 20pts dari margin kiri dan bawah, sesuai konvensi dokumen hukum umum.

## Contoh kerja lengkap (siap salin‑tempel)

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

string sourcePdfPath = @"C:\Docs\input.pdf";
string outputPdfPath = @"C:\Docs\PageNumbered.pdf";

using (var pdfDocument = new Document(sourcePdfPath))
{
    // ---------- Create the page‑number/footer stamp ----------
    var batesStamp = new TextStamp("Bates-{page} – Confidential")
    {
        XIndent = 20,
        YIndent = 20,
        HorizontalAlignment = HorizontalAlignment.Left,
        VerticalAlignment   = VerticalAlignment.Bottom,
        Font = new Font(FontFamily.TimesRoman, 10, FontStyle.Bold),
        TextState = { ForegroundColor = Color.Gray }
    };

    // ---------- Optional watermark ----------
    var watermark = new TextStamp("DRAFT")
    {
        HorizontalAlignment = HorizontalAlignment.Center,
        VerticalAlignment   = VerticalAlignment.Center,
        Font = new Font(FontFamily.Helvetica, 72, FontStyle.Bold),
        TextState = { ForegroundColor = Color.Red, Transparency = 0.5f }
    };

    // ---------- Apply stamps to every page ----------
    foreach (Page page in pdfDocument.Pages)
    {
        page.AddStamp(watermark);   // comment out if you don't need a watermark
        page.AddStamp(batesStamp);
    }

    // ---------- Save and verify ----------
    pdfDocument.Save(outputPdfPath);
    Console.WriteLine($"✅ Added page numbers and watermark to {pdfDocument.Pages.Count} pages.");
}
```

Simpan ini sebagai `AddPageNumbers.cs`, pulihkan paket NuGet Aspose.Pdf (`Install-Package Aspose.Pdf`), dan jalankan. Anda akan mendapatkan file **tambahkan nomor halaman pdf** yang juga mendemonstrasikan **tambahkan penomoran bates**, **tambahkan teks footer**, **tambahkan tanda air khusus**, dan pola **loop through pdf halaman** klasik—semua dalam satu skrip rapi.

![contoh menambahkan nomor halaman pdf](https://example.com/images/add-page-numbers-pdf.png "Tangkapan layar menampilkan halaman PDF berangka dengan footer dan watermark")

## Kesimpulan

Kami telah membahas semua yang Anda perlukan untuk **menambahkan nomor halaman pdf** menggunakan Aspose.Pdf di C#. Dari looping melalui setiap halaman, menempelkan nomor Bates, menambahkan teks footer khusus, hingga melapisi watermark semi-transparan, kode ini cukup ringkas untuk dimasukkan ke proyek apa pun.

Selanjutnya, Anda mungkin ingin menjelajahi skenario lebih lanjut—seperti menarik teks footer dari data dasar, menerapkan font yang berbeda per bagian, atau menghasilkan indeks PDF secara terpisah yang mencantumkan semua nomor Bates. Semua ekstensi tersebut dibangun di atas ide inti yang telah kami tunjukkan, sehingga Anda berada pada posisi yang tepat untuk memperluas solusi seiring berkembangnya kebutuhan Anda.

Saya, sesuaikan stylingnya, dan beri tahu kami di komentar bagaimana hasilnya. Selamat coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}