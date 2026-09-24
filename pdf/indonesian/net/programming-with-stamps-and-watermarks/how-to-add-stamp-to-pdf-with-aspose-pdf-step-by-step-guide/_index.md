---
category: general
date: 2026-03-24
description: Cara menambahkan stempel ke PDF menggunakan Aspose.Pdf di C#. Pelajari
  cara menempatkan stempel PDF dan menambahkan stempel teks PDF dengan penyesuaian
  ukuran otomatis dalam beberapa langkah mudah.
draft: false
keywords:
- how to add stamp
- place stamp pdf
- add text stamp pdf
- Aspose.Pdf stamp example
- C# PDF annotation
language: id
og_description: Bagaimana menambahkan stempel ke PDF dalam C#? Panduan ini menunjukkan
  cara menempatkan stempel PDF dan menambahkan stempel teks PDF dengan penyesuaian
  ukuran font otomatis menggunakan Aspose.Pdf.
og_title: Cara Menambahkan Stempel ke PDF dengan Aspose.Pdf – Panduan Cepat
tags:
- pdf
- csharp
- aspose
- stamping
title: Cara Menambahkan Stempel ke PDF dengan Aspose.Pdf – Panduan Langkah demi Langkah
url: /id/net/programming-with-stamps-and-watermarks/how-to-add-stamp-to-pdf-with-aspose-pdf-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Menambahkan Stempel ke PDF dengan Aspose.Pdf – Panduan Langkah‑per‑Langkah

**Cara menambahkan stempel** ke PDF adalah kebutuhan umum ketika Anda ingin memberi merek, mengesahkan, atau sekadar memberi anotasi pada dokumen. Pernah bertanya‑tanya cara termudah menempatkan stempel PDF tanpa berurusan dengan grafis tingkat‑rendah? Dalam tutorial ini kami akan membahas solusi lengkap yang siap dijalankan yang tidak hanya menunjukkan **cara menambahkan stempel** tetapi juga menjelaskan *mengapa* setiap baris penting.

Anda akan belajar cara **menempatkan stempel PDF** pada halaman mana pun, cara **menambahkan teks stempel PDF** yang secara otomatis menyusut agar sesuai dengan persegi panjangnya, dan jebakan apa yang harus dihindari ketika teks terlalu panjang. Pada akhir tutorial Anda akan memiliki satu file C# yang dapat Anda masukkan ke dalam proyek dan langsung mulai menstempel PDF.

## Prasyarat

* .NET 6.0 atau lebih baru (kode ini bekerja dengan .NET Core dan .NET Framework juga).
* Paket NuGet Aspose.Pdf untuk .NET (`Aspose.Pdf`) terpasang.
* File PDF bernama `input.pdf` di folder yang dapat Anda referensikan (PDF satu‑halaman sederhana apa pun dapat digunakan).

Tidak ada konfigurasi tambahan yang diperlukan—Aspose.Pdf menangani semua pekerjaan berat.

## Langkah 1: Siapkan Proyek dan Muat PDF Sumber

Hal pertama yang kita butuhkan adalah objek `Document` yang mewakili PDF yang ingin kita beri anotasi. Anggap saja sebagai memuat kanvas kosong yang nanti akan kita beri stempel.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Load the source PDF document
// The using statement ensures the file is closed automatically.
using var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");
```

> **Mengapa ini penting:** `Document` adalah titik masuk untuk setiap manipulasi PDF di Aspose.Pdf. Dengan menggunakan pola `using` kami menjamin bahwa handle file dilepaskan, yang mencegah masalah penguncian file ketika Anda kemudian mencoba menyimpan PDF yang telah dimodifikasi.

## Langkah 2: Buat Text Stamp dengan Ukuran Font yang Menyesuaikan Otomatis

Sekarang kita membuat `TextStamp`. Trik yang membuat contoh ini menonjol adalah flag `AutoAdjustFontSizeToFitStampRectangle`—ini memberi tahu Aspose untuk mengecilkan teks hingga muat di dalam persegi panjang yang kita definisikan.

```csharp
// Create a text stamp that will automatically resize to fit its rectangle
var textStamp = new TextStamp("Long text that must fit")
{
    // Let Aspose shrink the text if it overflows
    AutoAdjustFontSizeToFitStampRectangle = true,
    // Precision of the auto‑adjust algorithm (lower = more accurate)
    AutoAdjustFontSizePrecision = 0.01f,
    // Define the stamp's bounding box (in points)
    Width = 300,
    Height = 100,
    // Word‑wrap by whole words so we don’t split in the middle of a word
    WordWrapMode = TextFormattingOptions.WordWrapMode.ByWords,
    // Optional: set background color or opacity if you want a visible box
    Background = new Background()
    {
        Color = Color.LightGray,
        Opacity = 0.5
    }
};
```

> **Tips pro:** Jika Anda membutuhkan logo atau gambar alih‑alih teks, gunakan `ImageStamp`—logika penyesuaian otomatis yang sama berlaku untuk skala gambar.

## Langkah 3: Pilih Di Mana **Menempatkan Stempel PDF** – Halaman Pertama, Halaman Terakhir, atau Indeks Kustom

Aspose.Pdf menyimpan halaman dalam koleksi berbasis 1 (`pdfDocument.Pages[1]` adalah halaman pertama). Anda dapat **menempatkan stempel PDF** pada halaman mana pun dengan mengubah indeks.

```csharp
// Place the stamp on the first page (index 1)
// To stamp the last page use pdfDocument.Pages[pdfDocument.Pages.Count]
pdfDocument.Pages[1].AddStamp(textStamp);
```

> **Mengapa ini fleksibel:** Karena koleksi `Pages` dapat diubah, Anda dapat melakukan loop melalui semua halaman dan menambahkan stempel yang sama ke masing‑masing, atau menargetkan halaman tertentu berdasarkan logika bisnis (misalnya, hanya halaman sampul).

## Langkah 4: Simpan Dokumen yang Dimodifikasi

Setelah menstempel, Anda perlu menulis perubahan kembali ke disk. Anda dapat menimpa file asli atau membuat file baru—sesuai pilihan Anda.

```csharp
// Save the stamped PDF – change the path if you don’t want to overwrite
pdfDocument.Save("YOUR_DIRECTORY/output-stamped.pdf");
```

Saat Anda membuka `output-stamped.pdf` Anda akan melihat persegi panjang abu‑abu terang pada halaman pertama yang berisi teks “Long text that must fit”. Jika teks lebih panjang, Aspose secara otomatis akan mengecilkannya hingga pas sempurna di dalam persegi panjang 300 × 100 pt.

## Contoh Lengkap yang Berfungsi

Berikut adalah program lengkap yang dapat Anda salin‑tempel ke dalam aplikasi konsol (`Program.cs`). Program ini mencakup semua bagian yang kami bahas, plus sebuah helper kecil untuk memverifikasi bahwa stempel muncul.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Drawing;   // Needed for Background and Color

namespace PdfStampDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the source PDF
            using var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");

            // 2️⃣ Create a text stamp with auto‑adjusting font size
            var textStamp = new TextStamp("Long text that must fit")
            {
                AutoAdjustFontSizeToFitStampRectangle = true,
                AutoAdjustFontSizePrecision = 0.01f,
                Width = 300,
                Height = 100,
                WordWrapMode = TextFormattingOptions.WordWrapMode.ByWords,
                Background = new Background()
                {
                    Color = Color.LightGray,
                    Opacity = 0.5
                }
            };

            // 3️⃣ Place the stamp on the first page (you can change the index)
            pdfDocument.Pages[1].AddStamp(textStamp);

            // 4️⃣ Save the result
            string outputPath = "YOUR_DIRECTORY/output-stamped.pdf";
            pdfDocument.Save(outputPath);

            Console.WriteLine($"Stamp added successfully! Check the file at: {outputPath}");
        }
    }
}
```

### Hasil yang Diharapkan

* PDF terbuka dengan kotak abu‑abu semi‑transparan pada halaman pertama.
* Di dalam kotak, teks yang diberikan pas sempurna, bahkan jika Anda menggantinya dengan kalimat yang lebih panjang.
* Tidak diperlukan perhitungan ukuran font secara manual—Aspose menangani pekerjaan berat.

## Kesalahan Umum Saat Anda **Menempatkan Stempel PDF**

| Gejala | Penyebab Kemungkinan | Solusi |
|---------|----------------------|--------|
| Teks terpotong | `AutoAdjustFontSizeToFitStampRectangle` **false** atau persegi panjang terlalu kecil. | Aktifkan flag dan tingkatkan `Width`/`Height` atau kurangi panjang teks. |
| Stempel muncul tidak terpusat | `HorizontalAlignment`/`VerticalAlignment` default adalah `Left`/`Top`. | Set `HorizontalAlignment = HorizontalAlignment.Center` dan `VerticalAlignment = VerticalAlignment.Center`. |
| Stempel tidak terlihat pada beberapa viewer | Opacity latar belakang diatur ke 0 atau warna stempel sama dengan latar halaman. | Gunakan `Background.Color` yang kontras atau set `Opacity` > 0.3. |
| Beberapa stempel saling tumpang tindih | Menambahkan stempel dalam loop tanpa menyesuaikan koordinat. | Gunakan `textStamp.XIndent` dan `textStamp.YIndent` untuk menggeser setiap stempel. |

Menangani masalah ini sejak awal menghemat banyak waktu debugging di kemudian hari.

## Memperluas Contoh: Menambahkan Stempel Gambar

Jika Anda perlu **menambahkan teks stempel PDF** *dan* gambar (misalnya, logo perusahaan), Anda dapat menggabungkan keduanya:

```csharp
var imageStamp = new ImageStamp("YOUR_DIRECTORY/logo.png")
{
    Width = 100,
    Height = 50,
    XIndent = 400,          // Position to the right of the text stamp
    YIndent = 20,
    Background = new Background()
    {
        Color = Color.Transparent
    }
};

pdfDocument.Pages[1].AddStamp(imageStamp);
```

Sekarang halaman menampilkan baik stempel teks dinamis maupun stempel gambar statis berdampingan.

## Menguji Implementasi Anda

1. Jalankan aplikasi konsol.  
2. Buka `output-stamped.pdf` di Adobe Reader, Edge, atau penampil PDF apa pun.  
3. Verifikasi bahwa persegi panjang stempel ada dan teks terlihat sepenuhnya.  
4. Ubah teks menjadi frasa yang lebih panjang, jalankan kembali, dan pastikan font menyusut secara otomatis.

Jika ada yang terlihat tidak tepat, periksa kembali dimensi persegi panjang dan pengaturan `AutoAdjustFontSizePrecision`.

## Kesimpulan

Anda kini tahu **cara menambahkan stempel** ke PDF menggunakan Aspose.Pdf, cara **menempatkan stempel PDF** pada halaman tertentu, dan cara **menambahkan teks stempel PDF** yang secara otomatis menyesuaikan ukuran fontnya. Contoh lengkap yang dapat dijalankan di atas menghilangkan tebak‑tebakan dan memberi Anda dasar yang kuat untuk skenario stempel lanjutan—seperti memproses puluhan file secara batch atau menambahkan watermark secara kondisional.

Siap untuk langkah selanjutnya? Coba menstempel setiap halaman dalam loop, bereksperimen dengan font berbeda, atau menggabungkan stempel gambar dan teks untuk membuat segel yang tampak profesional. Tidak ada batasnya, dan dengan Aspose.Pdf Anda memiliki mesin yang dapat diandalkan di balik layar.

Jika Anda mengalami kendala, tinggalkan komentar atau periksa dokumentasi Aspose.Pdf untuk opsi kustomisasi yang lebih mendalam. Selamat menstempel!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}