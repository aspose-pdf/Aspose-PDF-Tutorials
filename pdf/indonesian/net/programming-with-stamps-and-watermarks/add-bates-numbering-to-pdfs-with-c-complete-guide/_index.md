---
category: general
date: 2026-04-10
description: Tambahkan penomoran Bates ke PDF dengan C# dalam hitungan menit. Pelajari
  cara menambahkan nomor halaman khusus, cara memberi nomor pada file PDF, dan menerapkan
  penomoran Bates secara efisien.
draft: false
keywords:
- add bates numbering
- add custom page numbers
- how to number pdf
- how to add bates
- apply bates numbering
language: id
og_description: Tambahkan penomoran Bates ke PDF dengan C# dalam hitungan menit. Panduan
  ini menunjukkan cara menambahkan nomor halaman khusus, cara menomori file PDF, dan
  menerapkan penomoran Bates langkah demi langkah.
og_title: Tambahkan Penomoran Bates ke PDF dengan C# – Panduan Lengkap
tags:
- PDF
- C#
- Bates numbering
title: Tambahkan Penomoran Bates ke PDF dengan C# – Panduan Lengkap
url: /id/net/programming-with-stamps-and-watermarks/add-bates-numbering-to-pdfs-with-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tambahkan Penomoran Bates ke PDF dengan C# – Panduan Lengkap

Pernah membutuhkan untuk **add bates numbering** ke PDF tetapi tidak yakin harus mulai dari mana? Anda tidak sendirian—tim hukum, auditor, dan siapa pun yang menangani kumpulan dokumen besar sering mengalami hambatan ini. Kabar baiknya? Dengan beberapa baris C# Anda dapat secara otomatis menempelkan stempel pada setiap halaman dengan identifier khusus, dan Anda juga akan belajar **how to add custom page numbers** sepanjang proses.

Dalam tutorial ini kami akan membahas semua yang Anda perlukan: paket NuGet yang diperlukan, mengonfigurasi opsi penomoran, menerapkan nomor, dan memverifikasi hasilnya. Pada akhir tutorial Anda akan mengetahui **how to number PDF** secara programatis, dan Anda akan siap menyesuaikan prefix, suffix, ukuran font, atau bahkan menargetkan halaman tertentu.

## Prasyarat

- .NET 6.0 atau lebih baru (kode ini juga berfungsi dengan .NET Framework 4.7+)
- Visual Studio 2022 (atau IDE apa pun yang Anda sukai)
- Perpustakaan **Aspose.PDF for .NET** (versi percobaan gratis cukup untuk belajar)
- Sebuah PDF contoh bernama `source.pdf` yang ditempatkan di folder yang Anda kontrol

Jika Anda sudah mencentang semua kotak tersebut, mari kita mulai.

## Langkah 1: Instal dan Referensikan Aspose.PDF

Pertama, tambahkan paket Aspose.PDF ke proyek Anda:

```bash
dotnet add package Aspose.PDF
```

Atau gunakan UI NuGet Package Manager. Setelah terinstal, sertakan namespace di bagian atas file Anda:

```csharp
using Aspose.Pdf;
```

> **Pro tip:** Jaga paket Anda tetap terbaru; versi terbaru (per April 2026) menambahkan beberapa peningkatan kinerja untuk dokumen besar.

## Langkah 2: Buka Dokumen PDF Sumber

Membuka file sangat sederhana. Kami akan menggunakan blok `using` sehingga handle file dilepaskan secara otomatis.

```csharp
// Step 2: Open the source PDF document
using (var sourceDocument = new Document("YOUR_DIRECTORY/source.pdf"))
{
    // The rest of the workflow lives inside this block.
}
```

Kelas `Document` mewakili seluruh PDF, memberi kami akses ke halaman, anotasi, dan tentu saja, penomoran Bates.

## Langkah 3: Definisikan Pengaturan Penomoran Bates

Sekarang masuk ke inti masalah—mengonfigurasi opsi **add bates numbering**. Anda dapat mengontrol nomor mulai, prefix, suffix, ukuran font, margin, dan bahkan menentukan halaman mana yang menerima stempel.

```csharp
// Step 3: Define Bates numbering settings
var batesOptions = new BatesNumberingOptions
{
    StartNumber = 1,                 // First number in the sequence
    Prefix = "ABC-",                 // Text before the number
    Suffix = "-2024",                // Text after the number
    FontSize = 12,                   // Size of the numbering font
    Margin = 10,                     // Distance from the page edge (points)
    PageNumbers = new[] { 1, 2, 3 }  // Pages to which numbering is applied
};
```

### Mengapa Pengaturan Ini Penting

- **StartNumber** memungkinkan Anda melanjutkan urutan dari batch sebelumnya.
- **Prefix/Suffix** berguna untuk identifier kasus atau stempel tahun.
- **FontSize** dan **Margin** memengaruhi keterbacaan; font yang terlalu kecil dapat terlewat saat dicetak.
- **PageNumbers** adalah tempat Anda **apply bates numbering** secara selektif. Hapus array ini untuk menomori setiap halaman.

Jika Anda perlu **add custom page numbers** yang tidak berurutan, Anda dapat membuat daftar seperti `{5, 10, 15}` dan mengirimkannya di sini.

## Langkah 4: Terapkan Penomoran Bates ke Halaman yang Dipilih

Dengan opsi yang sudah dipersiapkan, pustaka melakukan pekerjaan berat. Metode `AddBatesNumbering` menyuntikkan stempel ke setiap halaman target.

```csharp
// Step 4: Apply the Bates numbering to the selected pages
sourceDocument.AddBatesNumbering(batesOptions);
```

Di balik layar, Aspose.PDF membuat fragmen teks untuk setiap halaman, menempatkannya sesuai margin, dan menghormati ukuran font yang dipilih. Ini memastikan nomor muncul tepat di tempat yang Anda harapkan, baik saat melihat PDF di layar maupun mencetaknya.

## Langkah 5: Simpan Dokumen yang Dimodifikasi

Akhirnya, simpan perubahan ke file baru sehingga file asli tetap tidak tersentuh.

```csharp
// Step 5: Save the modified document with Bates numbers
sourceDocument.Save("YOUR_DIRECTORY/bates.pdf");
```

Sekarang Anda memiliki `bates.pdf` yang berisi halaman yang telah ditempeli stempel. Buka di penampil PDF apa pun dan Anda akan melihat sesuatu seperti:

```
ABC-1-2024   (on page 1, top‑right)
ABC-2-2024   (on page 2, top‑right)
ABC-3-2024   (on page 3, top‑right)
```

### Memverifikasi Hasil

Pemeriksaan cepat adalah dengan secara programatis membaca kembali teks halaman pertama:

```csharp
using (var doc = new Document("YOUR_DIRECTORY/bates.pdf"))
{
    var text = doc.Pages[1].ExtractText();
    Console.WriteLine(text.Contains("ABC-1-2024") ? "Bates number applied!" : "Oops, something went wrong.");
}
```

Jika konsol mencetak *Bates number applied!*, Anda berhasil.

## Kasus Pinggir & Variasi Umum

| Situation | What to Change | Reason |
|-----------|----------------|--------|
| **Number every page** | Omit `PageNumbers` or set it to `null` | API default ke semua halaman ketika array tidak diberikan. |
| **Different margin per side** | Use `Margin = new MarginInfo { Top = 15, Right = 10 }` (requires Aspose > 23.3) | Memberikan kontrol detail atas penempatan. |
| **Large documents (> 500 pages)** | Enable `batesOptions.StartNumber` at a higher value and consider `batesOptions.FontSize = 10` to avoid overlap | Menjaga stempel tetap terbaca tanpa menumpuk halaman. |
| **Need a different font** | Set `batesOptions.Font = FontRepository.FindFont("Arial")` | Beberapa firma hukum memerlukan jenis huruf tertentu. |

> **Watch out:** Jika Anda memberikan nomor halaman yang tidak ada (mis., `PageNumbers = new[] { 999 }`), Aspose.PDF akan melewatkannya secara diam-diam. Selalu validasi rentang jika Anda membangun daftar secara dinamis.

## Contoh Kerja Lengkap

Berikut adalah program lengkap yang siap dijalankan. Tempelkan ke aplikasi konsol, sesuaikan jalur, dan tekan **F5**.

```csharp
using System;
using Aspose.Pdf;

class Program
{
    static void Main()
    {
        // Adjust these paths to match your environment
        string sourcePath = @"YOUR_DIRECTORY\source.pdf";
        string outputPath = @"YOUR_DIRECTORY\bates.pdf";

        // Open the source PDF
        using (var sourceDocument = new Document(sourcePath))
        {
            // Configure Bates numbering options
            var batesOptions = new BatesNumberingOptions
            {
                StartNumber = 1,
                Prefix = "ABC-",
                Suffix = "-2024",
                FontSize = 12,
                Margin = 10,
                PageNumbers = new[] { 1, 2, 3 } // Change or remove to number all pages
            };

            // Apply the numbering
            sourceDocument.AddBatesNumbering(batesOptions);

            // Save the new PDF
            sourceDocument.Save(outputPath);
        }

        // Verify the first page contains the expected stamp
        using (var doc = new Document(outputPath))
        {
            string extracted = doc.Pages[1].ExtractText();
            bool success = extracted.Contains("ABC-1-2024");
            Console.WriteLine(success
                ? "Bates numbering added successfully!"
                : "Numbering failed – check your options.");
        }
    }
}
```

Menjalankan kode ini akan menghasilkan `bates.pdf` dengan tiga halaman yang telah ditempeli stempel seperti yang ditunjukkan sebelumnya. Buka file tersebut, dan Anda akan melihat nomor rata kanan, 10 point dari tepi, dengan font 12 point.

## Pratinjau Visual

![add bates numbering preview](/images/bates-numbering-sample.png)

*Tangkap layar di atas menggambarkan bagaimana output **add bates numbering** terlihat setelah skrip dijalankan.*

## Kesimpulan

Kami baru saja membahas cara **add bates numbering** ke PDF menggunakan C#. Dengan mengonfigurasi `BatesNumberingOptions`, menerapkan stempel, dan menyimpan dokumen, Anda kini memiliki solusi yang dapat diulang yang juga dapat **add custom page numbers**, **how to number pdf** file, dan **apply bates numbering** di seluruh proyek apa pun. 

Langkah selanjutnya? Coba gabungkan ini dengan pemroses batch yang menelusuri folder PDF, atau bereksperimen dengan prefix berbeda untuk setiap tipe kasus. Anda juga dapat mengeksplorasi penggabungan beberapa PDF setelah penomoran—berguna untuk membangun bundel kasus yang komprehensif.

Ada pertanyaan tentang kasus pinggir, atau ingin melihat cara menanamkan nomor di footer alih-alih header? Tinggalkan komentar, dan selamat coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}