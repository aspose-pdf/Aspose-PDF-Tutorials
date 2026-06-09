---
category: general
date: 2026-06-08
description: Tambahkan penomoran bates pada PDF menggunakan Aspose.Pdf di C#. Pelajari
  cara menambahkan bates, menambahkan nomor halaman PDF, menambahkan nomor berurutan
  PDF, dan lihat contoh penomoran bates PDF.
draft: false
keywords:
- add bates numbering pdf
- how to add bates
- add page numbers pdf
- add sequential numbers pdf
- bates number pdf example
language: id
og_description: Tambahkan penomoran bates pada PDF di C#. Tutorial ini menunjukkan
  cara menambahkan bates, menambahkan nomor halaman pada PDF, dan menambahkan nomor
  berurutan pada PDF dengan contoh lengkap penomoran bates pada PDF.
og_title: Menambahkan Penomoran Bates pada PDF – Panduan Lengkap dengan Aspose
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Add bates numbering pdf using Aspose.Pdf in C#. Learn how to add bates,
    add page numbers pdf, add sequential numbers pdf, and see a bates number pdf example.
  headline: Add Bates Numbering PDF – Complete Guide with Aspose
  type: TechArticle
- description: Add bates numbering pdf using Aspose.Pdf in C#. Learn how to add bates,
    add page numbers pdf, add sequential numbers pdf, and see a bates number pdf example.
  name: Add Bates Numbering PDF – Complete Guide with Aspose
  steps:
  - name: Install the Aspose.Pdf NuGet Package
    text: 'First, add the library to your project. Open the Package Manager Console
      and run:'
  - name: Open the Source PDF Document
    text: Now we load the PDF we want to stamp. The `using` statement ensures the
      file is closed properly even if an exception occurs.
  - name: Create a Bates Numbering Facade
    text: 'The *facade* pattern hides the complexity of the underlying PDF structure.
      Here’s how we instantiate it:'
  - name: Configure the Starting Number and Prefix
    text: Bates numbers often include a case‑specific prefix. You can also control
      the number of digits, the separator, and the placement on the page.
  - name: Apply the Bates Numbering to the Document
    text: 'With the facade configured, we now stamp every page:'
  - name: Save the Modified PDF
    text: 'Finally, write the output to disk:'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF processing
title: Tambahkan Penomoran Bates pada PDF – Panduan Lengkap dengan Aspose
url: /id/net/programming-with-stamps-and-watermarks/add-bates-numbering-pdf-complete-guide-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Menambahkan Penomoran Bates PDF – Panduan Pemrograman Lengkap

Pernah perlu **menambahkan bates numbering pdf** tetapi tidak yakin harus mulai dari mana? Jika Anda pernah bertanya-tanya *bagaimana menambahkan bates* ke dokumen hukum, Anda berada di tempat yang tepat. Dalam tutorial ini kami akan membimbing Anda melalui contoh praktis end‑to‑end yang tidak hanya menambahkan nomor Bates tetapi juga menunjukkan cara **menambahkan nomor halaman pdf**, **menambahkan nomor berurutan pdf**, dan bahkan menyediakan **bates number pdf example** yang siap dijalankan.

Kami akan menggunakan pustaka Aspose.Pdf untuk .NET, karena ia menyembunyikan detail internal PDF tingkat rendah sekaligus memberi Anda kontrol yang detail. Pada akhir panduan ini Anda akan memiliki potongan kode yang dapat dipakai ulang di proyek C# mana pun, dan Anda akan memahami mengapa setiap baris penting.

## Apa yang Anda Butuhkan

- **.NET 6.0** atau lebih baru (kode ini juga berfungsi pada .NET Framework 4.6+).  
- **Lisensi** untuk Aspose.Pdf atau kunci evaluasi sementara gratis.  
- Sebuah PDF contoh bernama `input.pdf` yang ditempatkan di folder yang dapat Anda referensikan.  
- Visual Studio, Rider, atau editor C# pilihan Anda.

Itu saja—tanpa alat tambahan, tanpa akrobatik baris perintah. Siap? Mari kita mulai.

## Menambahkan Penomoran Bates PDF – Implementasi Langkah‑per‑Langkah

Berikut kami membagi proses menjadi enam langkah logis. Setiap langkah mencakup potongan kode singkat, penjelasan *mengapa* kami melakukannya, dan tip yang mungkin berguna.

### Langkah 1: Instal Paket NuGet Aspose.Pdf

Pertama, tambahkan pustaka ke proyek Anda. Buka Package Manager Console dan jalankan:

```powershell
Install-Package Aspose.Pdf
```

> **Pro tip:** Jika Anda menggunakan .NET Core, Anda juga dapat memakai `dotnet add package Aspose.Pdf`.

Menginstal paket memberi Anda akses ke kelas `Aspose.Pdf.Facades.BatesNumbering`, yang merupakan mesin utama untuk **add bates numbering pdf**.

### Langkah 2: Buka Dokumen PDF Sumber

Sekarang kita memuat PDF yang ingin kita beri stempel. Pernyataan `using` memastikan file ditutup dengan benar bahkan jika terjadi pengecualian.

```csharp
using (var doc = new Aspose.Pdf.Document(@"C:\MyPdfs\input.pdf"))
{
    // All further steps happen inside this block.
}
```

Mengapa memakai `Aspose.Pdf.Document`? Kelas ini mewakili seluruh PDF dalam memori, memungkinkan kita memanipulasi halaman, font, dan metadata tanpa menyentuh file asli di disk.

### Langkah 3: Buat Bates Numbering Facade

Polanya *facade* menyembunyikan kompleksitas struktur PDF di bawahnya. Berikut cara menginstansiasinya:

```csharp
var bates = new Aspose.Pdf.Facades.BatesNumbering();
```

Objek ini nantinya akan dikonfigurasi dengan prefiks, nomor mulai, dan opsi format. Anggaplah ini sebagai “mesin” yang akan **add page numbers pdf** secara sesuai standar Bates.

### Langkah 4: Konfigurasikan Nomor Mulai dan Prefiks

Nomor Bates sering menyertakan prefiks khusus kasus. Anda juga dapat mengontrol jumlah digit, pemisah, dan penempatan pada halaman.

```csharp
bates.StartNumber = 1000;          // First number in the sequence
bates.Prefix = "CASE-";            // Prefix that appears before each number
bates.NumberOfDigits = 5;          // Pads numbers with leading zeros (e.g., 01000)
bates.Separator = "-";             // Optional separator between prefix and number
bates.Location = new Aspose.Pdf.Rectangle(0, 0, 200, 20); // Bottom‑left corner
bates.FontSize = 12;
bates.FontColor = System.Drawing.Color.Blue;
```

**Mengapa pengaturan ini?**  
- `StartNumber` memungkinkan Anda melanjutkan seri sebelumnya.  
- `NumberOfDigits` menjamin panjang seragam, yang penting untuk pengindeksan hukum.  
- `Location` menentukan di mana **add sequential numbers pdf** akan muncul; Anda dapat memindahkannya ke kanan‑atas jika lebih suka.

### Langkah 5: Terapkan Penomoran Bates ke Dokumen

Dengan facade yang sudah dikonfigurasi, kini kita beri stempel pada setiap halaman:

```csharp
bates.AddBatesNumbering(doc);
```

Di balik layar, Aspose mengiterasi setiap halaman, menggambar teks pada lokasi yang ditentukan, dan menghormati konten yang sudah ada. Baris tunggal inilah yang sebenarnya **add bates numbering pdf** ke file Anda.

### Langkah 6: Simpan PDF yang Telah Dimodifikasi

Akhirnya, tulis hasilnya ke disk:

```csharp
doc.Save(@"C:\MyPdfs\output.pdf");
```

Sekarang Anda memiliki PDF di mana setiap halaman membawa identifikasi Bates unik, siap untuk penemuan atau pengajuan di ruang sidang.

#### Contoh Kerja Penuh (Bates Number PDF Example)

Menggabungkan semuanya, berikut program lengkap yang dapat Anda kompilasi dan jalankan:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Facades;
using System.Drawing; // For Color

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source PDF
        using (var doc = new Document(@"C:\MyPdfs\input.pdf"))
        {
            // 2️⃣ Create the Bates numbering facade
            var bates = new BatesNumbering();

            // 3️⃣ Configure prefix, start number, and formatting
            bates.StartNumber = 1000;
            bates.Prefix = "CASE-";
            bates.NumberOfDigits = 5;
            bates.Separator = "-";
            bates.Location = new Rectangle(0, 0, 200, 20); // Bottom‑left
            bates.FontSize = 12;
            bates.FontColor = Color.Blue;

            // 4️⃣ Apply the numbering to every page
            bates.AddBatesNumbering(doc);

            // 5️⃣ Save the result
            doc.Save(@"C:\MyPdfs\output.pdf");
        }

        Console.WriteLine("Bates numbering added successfully!");
    }
}
```

> **Output yang diharapkan:** Buka `output.pdf` dan Anda akan melihat “CASE‑01000”, “CASE‑01001”, … di pojok kiri‑bawah setiap halaman.

![Screenshot halaman PDF dengan nomor Bates di pojok kiri‑bawah – contoh add bates numbering pdf](https://example.com/bates-numbering-screenshot.png "contoh add bates numbering pdf")

*(Teks alt gambar: *contoh add bates numbering pdf* – menampilkan nomor Bates yang diterapkan pada PDF contoh.)*

## Cara Menambahkan Bates – Memahami Facade

Anda mungkin bertanya **bagaimana menambahkan bates** tanpa facade Aspose. Alternatifnya adalah menggambar teks secara manual pada setiap halaman menggunakan operator PDF tingkat rendah, tetapi pendekatan itu rawan kesalahan dan memerlukan pengetahuan mendalam tentang spesifikasi PDF. Facade menyederhanakan detail tersebut, memungkinkan Anda fokus pada *apa* yang Anda inginkan (prefiks, nomor mulai) bukan *bagaimana* cara merendernya.

Jika Anda pernah perlu **menambahkan nomor halaman pdf** dengan gaya non‑Bates (misalnya “Halaman 3 dari 12”), Anda dapat menggunakan kembali kelas `BatesNumbering`—cukup ubah `Prefix` menjadi string kosong dan sesuaikan `Location`. Mesin dasarnya tetap sama, yang berarti Anda mendapatkan rendering konsisten di kedua kasus penggunaan.

## Menambahkan Nomor Halaman PDF – Menyesuaikan Penempatan dan Gaya

Tim hukum sering meminta nomor halaman di header, sementara staf dukungan litigasi lebih suka di footer. Berikut penyesuaian cepat:

```csharp
bates.Location = new Rectangle(0, doc.Pages[1].PageInfo.Height - 20, 200, 20); // Top‑right
bates.Prefix = "";               // No prefix for plain page numbers
bates.StartNumber = 1;           // Start from 1
bates.NumberOfDigits = 0;        // No padding
bates.FontColor = Color.Black;
```

Pemanggilan `AddBatesNumbering` yang sama kini akan **add page numbers pdf** ke bagian atas setiap halaman. Karena facade bekerja pada objek dokumen, Anda dapat beralih antara penomoran Bates dan penomoran halaman biasa dengan beberapa perubahan properti—tanpa harus menulis ulang loop.

## Menambahkan Nomor Berurutan PDF – Format Lanjutan

Misalkan Anda memerlukan format seperti `2023-CASE-00123`. Anda dapat menggabungkan prefiks tanggal dengan pengaturan yang ada:

```csharp
bates.Prefix = $"{DateTime.Now:yyyy}-CASE-";
bates.NumberOfDigits = 5;
bates.Separator = "-";
```

Sekarang setiap halaman akan menampilkan `2023-CASE-00123`, `2023-CASE-00124`, dll. Ini menunjukkan betapa mudahnya **add sequential numbers pdf** yang memenuhi konvensi penamaan kompleks.

## Kasus Khusus dan Kesalahan Umum

| Situasi | Hal yang Perlu Diwaspadai | Solusi yang Disarankan |
|-----------|----------------------|---------------|
| **PDF sangat besar ( > 500 MB )** | Konsumsi memori dapat melonjak karena seluruh dokumen dimuat ke RAM. | Gunakan `Document` dengan pengaturan `MemoryManagement` atau proses file secara bertahap menggunakan `PdfFileEditor`. |
| **Nomor halaman yang sudah ada** | Penambahan nomor Bates dapat menimpa atau menumpuk dengan nomor yang sudah ada. | Sesuaikan `Location` atau hapus nomor lama terlebih dahulu dengan `PdfFileEditor`. |

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah‑per‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Cara Menambahkan dan Menyesuaikan Nomor Halaman dalam PDF Menggunakan Aspose.PDF untuk .NET | Panduan Manipulasi Dokumen](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [Cara Menambahkan Stempel Nomor Halaman dalam PDF Menggunakan Aspose.PDF untuk .NET | Watermarks & Backgrounds](/pdf/english/net/watermarks-backgrounds/add-page-number-stamp-using-aspose-pdf-dotnet/)
- [Aspose.PDF .NET: Menambahkan Nomor Halaman ke PDF Menggunakan FloatingBox](/pdf/english/net/text-operations/aspose-pdf-net-floatingbox-page-numbering/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}