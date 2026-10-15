---
category: general
date: 2026-03-03
description: Tambahkan penomoran Bates pada PDF dengan cepat dan pelajari cara memberi
  nomor halaman PDF atau menambahkan nomor PDF berurutan menggunakan Aspose.Pdf di
  C#.
draft: false
keywords:
- add bates numbering pdf
- number pdf pages
- add sequential pdf numbers
- pdf bates numbering tutorial
- aspnet pdf automation
language: id
og_description: Tambahkan penomoran Bates PDF dalam C# untuk memberi nomor pada halaman
  PDF dan menambahkan nomor PDF berurutan. Kode lengkap, penjelasan, dan praktik terbaik.
og_title: Menambahkan Penomoran Bates pada PDF – Tutorial C# Lengkap
tags:
- PDF
- C#
- Aspose.Pdf
- Document Automation
title: Menambahkan Penomoran Bates pada PDF – Panduan Langkah demi Langkah untuk Menomori
  Halaman PDF
url: /id/net/programming-with-pdf-pages/add-bates-numbering-pdf-step-by-step-guide-to-number-pdf-pag/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tambahkan Penomoran Bates PDF – Tutorial Lengkap C#

Pernah membutuhkan untuk **add bates numbering pdf** file tetapi tidak yakin harus mulai dari mana? Anda bukan satu-satunya—tim hukum, auditor, dan arsiparis semua menghadapi masalah yang sama. Kabar baiknya? Dengan beberapa baris C# dan perpustakaan Aspose.Pdf Anda dapat **number pdf pages** secara otomatis, dan Anda bahkan akan mendapatkan fleksibilitas untuk **add sequential pdf numbers** dengan awalan, akhiran, dan penempatan khusus.

Dalam panduan ini kami akan membahas contoh dunia nyata, menjelaskan mengapa setiap pengaturan penting, dan menunjukkan cara menyesuaikan kode untuk kasus tepi seperti ukuran halaman yang berbeda atau jumlah digit khusus. Pada akhir tutorial Anda akan memiliki potongan kode siap‑jalankan yang menambahkan nomor Bates ke PDF apa pun yang Anda beri, dan Anda akan memahami “mengapa” di balik setiap opsi.

## Prasyarat

- .NET 6.0 atau lebih baru (kode ini juga berfungsi dengan .NET Framework 4.6+).
- Lisensi Aspose.Pdf untuk .NET yang valid (atau kunci evaluasi gratis).
- Visual Studio 2022 (atau editor C# apa pun yang Anda suka).
- Sebuah PDF sumber bernama `source.pdf` dalam folder yang dapat Anda referensikan.

Itu saja—tidak ada paket NuGet tambahan selain Aspose.Pdf.

## Langkah 1 – Buka Dokumen PDF Sumber

Hal pertama yang perlu Anda lakukan adalah memuat PDF yang ingin Anda beri stempel. Menggunakan blok `using` menjamin handle file dilepaskan dengan benar, yang mencegah masalah penguncian di kemudian hari.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Step 1: Load the original PDF
using (var pdfDocument = new Document(@"C:\MyDocs\source.pdf"))
{
    // The rest of the steps will go inside this block.
}
```

> **Mengapa ini penting:** Membuka dokumen di dalam pernyataan `using` memastikan pembuangan yang deterministik. Jika Anda melewatkannya, file dapat tetap terkunci, dan upaya selanjutnya untuk menyimpan atau menghapus PDF akan gagal—sesuatu yang pernah saya lihat menyebabkan masalah di jalur produksi.

## Langkah 2 – Konfigurasikan Opsi Penomoran Bates

Sekarang kami memberi tahu Aspose bagaimana tampilan nomor Bates yang diinginkan. Setiap properti langsung dipetakan ke elemen visual pada halaman.

```csharp
// Step 2: Set up Bates numbering preferences
var batesOptions = new BatesNumberingOptions
{
    Prefix = "2025-",               // Text before the number
    Suffix = "-A",                  // Text after the number
    Start = 5000,                   // First number in the sequence
    NumberOfDigits = 5,             // Pads with leading zeros (e.g., 05000)
    Placement = BatesNumberPlacement.BottomRight // Where the number appears
};
```

### Tips cepat untuk opsi

| Property | Apa fungsinya | Kapan mengubahnya |
|----------|---------------|-------------------|
| **Prefix / Suffix** | Menambahkan teks statis sebelum/setelah bagian numerik. | Gunakan ID kasus, kode proyek, atau “CONF‑” untuk dokumen rahasia. |
| **Start** | Angka pertama dalam rangkaian. | Jika Anda melanjutkan skema penomoran dari batch sebelumnya, atur sesuai. |
| **NumberOfDigits** | Mengontrol padding nol. | Untuk pengajuan hukum Anda sering memerlukan tepat 6 digit; atur ke `6`. |
| **Placement** | BottomRight, BottomLeft, TopRight, TopLeft, Center. | Pilih berdasarkan tata letak dokumen Anda; BottomRight paling umum untuk nomor Bates. |

> **Tip pro:** Jika Anda perlu **number pdf pages** dalam beberapa kolom, Anda dapat memanggil `pdfDocument.AddBatesNumbering` dua kali dengan nilai `Placement` yang berbeda dan string `Prefix` yang berbeda.

## Langkah 3 – Terapkan Penomoran Bates ke Dokumen

Dengan opsi siap, proses stamping sebenarnya hanya satu pemanggilan metode. Aspose menangani paginasi, rotasi, dan perhitungan margin secara internal.

```csharp
// Step 3: Apply the numbering to every page
pdfDocument.AddBatesNumbering(batesOptions);
```

> **Mengapa satu panggilan saja bekerja:** Di balik layar Aspose mengiterasi `pdfDocument.Pages`, membuat `TextFragment` untuk setiap halaman, dan menempatkannya berdasarkan `Placement` yang Anda pilih. Abstraksi ini menghemat Anda dari menulis loop manual dan menangani transformasi koordinat.

## Langkah 4 – Simpan PDF yang Diperbarui

Akhirnya, tulis file yang telah dimodifikasi ke disk. Anda dapat menimpa file asli atau membuat file baru; contoh di bawah ini membuat salinan baru.

```csharp
// Step 4: Persist the changes
pdfDocument.Save(@"C:\MyDocs\bates_numbered.pdf");
```

Jika Anda perlu **add sequential pdf numbers** ke sebuah stream (misalnya, saat mengirim file melalui API), ganti path file dengan `MemoryStream`:

```csharp
using var output = new MemoryStream();
pdfDocument.Save(output);
output.Position = 0; // Reset for downstream consumption
```

## Contoh Lengkap yang Berfungsi

Menggabungkan semuanya, berikut program lengkap yang siap dijalankan:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;

class Program
{
    static void Main()
    {
        // Open the source PDF
        using (var pdfDocument = new Document(@"C:\MyDocs\source.pdf"))
        {
            // Configure Bates numbering
            var batesOptions = new BatesNumberingOptions
            {
                Prefix = "2025-",
                Suffix = "-A",
                Start = 5000,
                NumberOfDigits = 5,
                Placement = BatesNumberPlacement.BottomRight
            };

            // Apply the numbering
            pdfDocument.AddBatesNumbering(batesOptions);

            // Save the result
            pdfDocument.Save(@"C:\MyDocs\bates_numbered.pdf");
        }

        Console.WriteLine("Bates numbering added successfully!");
    }
}
```

### Output yang Diharapkan

- File baru `bates_numbered.pdf` muncul di `C:\MyDocs`.
- Setiap halaman menampilkan sesuatu seperti `2025-05000-A`, `2025-05001-A`, … di pojok kanan bawah.
- Nomor-nomor tersebut dipadding nol hingga lima digit, sesuai dengan pengaturan `NumberOfDigits`.

## Menangani Variasi Umum

### 1. Ukuran Halaman Berbeda

Jika PDF Anda mencampur halaman potret dan lanskap, Anda mungkin melihat nomor terpotong di sisi yang lebih lebar. Untuk memperbaikinya, aktifkan properti `AutoFit`:

```csharp
batesOptions.AutoFit = true; // Adjusts font size to fit within page margins
```

### 2. Font atau Warna Kustom

Nomor Bates default berwarna hitam, 12‑pt Times New Roman. Ubah tampilannya dengan mengakses `TextState`:

```csharp
batesOptions.TextState = new TextState
{
    FontSize = 10,
    Font = FontRepository.FindFont("Courier New"),
    ForegroundColor = Color.GetBlue()
};
```

### 3. Melewatkan Halaman

Misalkan Anda ingin **number pdf pages** tetapi melewatkan halaman judul. Gunakan rentang halaman:

```csharp
pdfDocument.AddBatesNumbering(batesOptions, new PageNumbering { Start = 2 });
```

### 4. Menambahkan Skema Penomoran Ganda

Tim hukum kadang memerlukan baik nomor Bates maupun watermark rahasia. Jalankan dua panggilan `AddBatesNumbering` terpisah dengan nilai `Placement` yang berbeda:

```csharp
// First scheme – bottom right
pdfDocument.AddBatesNumbering(batesOptions);

// Second scheme – top left, different prefix
var confidentialOptions = new BatesNumberingOptions
{
    Prefix = "CONF-",
    Start = 1,
    NumberOfDigits = 4,
    Placement = BatesNumberPlacement.TopLeft,
    TextState = new TextState { FontSize = 8, ForegroundColor = Color.GetRed() }
};
pdfDocument.AddBatesNumbering(confidentialOptions);
```

## Pertanyaan yang Sering Diajukan

**Q: Apakah ini bekerja dengan PDF yang sudah memiliki teks yang ada?**  
A: Ya. Aspose menambahkan nomor Bates sebagai lapisan terpisah, sehingga konten yang ada tetap tidak tersentuh. Jika Anda membutuhkan nomor muncul *di belakang* teks yang ada (jarang), Anda harus memanipulasi aliran konten halaman secara manual.

**Q: Bagaimana jika PDF dilindungi kata sandi?**  
A: Muat terlebih dahulu dengan kata sandi: `new Document(path, new LoadOptions { Password = "secret" })`. Setelah stamping, Anda dapat menerapkan kembali enkripsi melalui `pdfDocument.Encrypt(...)`.

**Q: Bisakah saya menggunakan ini dalam aplikasi konsol .NET Core?**  
A: Tentu saja. Kode yang sama berfungsi di .NET Core, .NET 5+, dan .NET Framework. Cukup referensikan paket NuGet Aspose.Pdf yang sesuai.

## Kesimpulan

Kami baru saja membahas cara **add bates numbering pdf** file, cara **number pdf pages**, dan cara **add sequential pdf numbers** dengan kontrol penuh atas format, penempatan, dan penanganan kasus tepi. Potongan kode singkat di atas melakukan pekerjaan berat, sementara opsi tambahan memungkinkan Anda menyesuaikan solusi untuk alur kerja hukum, arsip, atau kepatuhan apa pun.

Siap untuk langkah selanjutnya? Coba menggabungkan pendekatan ini dengan:

- **Pemrosesan batch** – iterasi folder PDF dan terapkan skema penomoran yang sama.
- **Awalan dinamis** – ambil ID kasus dari basis data dan sisipkan per dokumen.
- **Kepatuhan PDF/A** – setelah penomoran, panggil `pdfDocument.Convert(..., PdfFormat.PdfA2b)` untuk memastikan preservasi jangka panjang.

Silakan bereksperimen, bagikan temuan Anda, atau ajukan pertanyaan di komentar. Selamat coding, dan semoga PDF Anda selalu terindeks dengan sempurna!

![Screenshot of a PDF page with Bates numbers in the bottom‑right corner](https://example.com/images/bates-numbered.png "add bates numbering pdf example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}