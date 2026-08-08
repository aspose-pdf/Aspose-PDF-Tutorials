---
category: general
date: 2026-03-27
description: Tambahkan penomoran Bates di C# dengan cepat. Pelajari cara menambahkan
  nomor halaman khusus, menambahkan nomor halaman berurutan, dan menambahkan nomor
  khusus ke dokumen Word.
draft: false
keywords:
- add bates numbering
- how to add bates
- add custom page numbers
- add sequential page numbers
- add custom numbers
language: id
og_description: Tambahkan penomoran Bates dalam C# dengan contoh yang jelas. Panduan
  ini menunjukkan cara menambahkan nomor halaman kustom, menambahkan nomor halaman
  berurutan, dan lainnya.
og_title: Tambahkan Penomoran Bates di C# – Tutorial Lengkap
tags:
- C#
- Document Processing
- Bates Numbering
title: Tambahkan Penomoran Bates di C# – Panduan Langkah demi Langkah
url: /id/net/programming-with-pdf-pages/add-bates-numbering-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Menambahkan Penomoran Bates di C# – Panduan Langkah‑ demi‑ Langkah

Pernah bertanya‑tanya bagaimana cara **add bates numbering** ke dokumen Word tanpa membuat Anda stres? Anda bukan satu‑satunya. Dalam banyak proyek hukum atau kepatuhan, setiap halaman memerlukan identifier unik, dan melakukannya secara manual adalah mimpi buruk.  

Dalam tutorial ini kami akan menelusuri contoh lengkap yang dapat dijalankan yang **adds bates numbering**, menunjukkan **how to add bates** dalam beberapa baris, dan bahkan membahas cara **add custom page numbers** serta **add sequential page numbers** ketika Anda membutuhkannya. Pada akhir tutorial Anda akan memiliki file .docx yang sudah ditempeli nomor pilihan Anda—tanpa memerlukan alat pihak ketiga.

## Apa yang Akan Anda Pelajari

- Memuat file DOCX dengan API Aspose.Words untuk .NET (atau perpustakaan kompatibel lainnya).  
- Mengonfigurasi **add custom numbers** seperti prefix, nilai awal, dan ukuran font.  
- Menerapkan penomoran ke setiap halaman dalam satu panggilan.  
- Menyimpan hasil dan memverifikasi bahwa nomor muncul seperti yang diharapkan.  

Tidak diperlukan pengalaman sebelumnya dengan penomoran Bates; cukup dengan setup C# dasar dan salinan dokumen sumber. Mari kita mulai.

## Prasyarat

- .NET 6+ (kode ini bekerja pada .NET Core dan .NET Framework).  
- Aspose.Words untuk .NET terpasang via NuGet (`Install-Package Aspose.Words`).  
- Dokumen Word bernama `input.docx` ditempatkan di folder yang dapat Anda referensikan (`YOUR_DIRECTORY`).  
- Visual Studio, VS Code, atau IDE C# apa pun yang Anda suka.

> **Pro tip:** Jika Anda menggunakan perpustakaan lain (misalnya Open XML SDK), konsepnya tetap sama—hanya ganti pemanggilan API.

## Langkah 1: Muat Dokumen Sumber

Pertama kita perlu membawa file Word ke memori.

```csharp
using Aspose.Words;

// Step 1: Load the source document
Document document = new Document("YOUR_DIRECTORY/input.docx");
```

*Mengapa ini penting:* Memuat file membuat objek `Document` yang memberi Anda akses ke halaman, bagian, dan pohon node tingkat rendah. Tanpa itu Anda tidak dapat menempelkan penomoran apa pun.

## Langkah 2: Konfigurasikan Opsi Penomoran Bates

Sekarang kita mendefinisikan tepat bagaimana nomor harus terlihat. Di sinilah Anda **add custom page numbers** atau **add sequential page numbers**.

```csharp
// Step 2: Define Bates numbering options (prefix, start number, font size)
BatesNumberingOptions batesOptions = new BatesNumberingOptions
{
    // Prefix that appears before every number, e.g., "ABC"
    Prefix = "ABC",
    // The first number in the sequence; change to 1 if you prefer
    Start = 1000,
    // Font size in points; 9 works well for most legal docs
    FontSize = 9
};
```

*Mengapa ini penting:* `Prefix` memungkinkan Anda **add custom numbers** seperti ID kasus, sementara `Start` menentukan penghitung awal. Mengubah `FontSize` memastikan nomor tidak menutupi margin halaman.

## Langkah 3: Terapkan Penomoran Bates ke Setiap Halaman

Dengan opsi yang sudah siap, kami memberi tahu perpustakaan untuk menempelkan setiap halaman.

```csharp
// Step 3: Apply Bates numbering to all pages of the document
document.Pages.AddBatesNumbering(batesOptions);
```

*Mengapa ini penting:* Metode `AddBatesNumbering` menelusuri koleksi halaman internal dan menyisipkan kotak teks di pojok kanan‑bawah (lokasi default). Inilah inti **how to add bates** tanpa menulis loop secara manual.

## Langkah 4: Simpan Dokumen yang Telah Diperbarui

Akhirnya, kami menulis file yang telah dimodifikasi kembali ke disk.

```csharp
// Step 4: Save the updated document
document.Save("YOUR_DIRECTORY/output.docx");
```

*Mengapa ini penting:* Menyimpan menghasilkan `output.docx` baru yang dapat Anda buka di Word, LibreOffice, atau penampil apa pun untuk memastikan nomor muncul.

## Hasil yang Diharapkan

Buka `output.docx`. Setiap halaman harus menampilkan sesuatu seperti:

```
ABC‑1000   (on page 1)
ABC‑1001   (on page 2)
ABC‑1002   (on page 3)
...
```

Jika Anda membuka pratinjau cetak dokumen, Anda akan melihat nomor di pojok kanan‑bawah, dengan ukuran font yang telah Anda tentukan.

## Kasus Khusus & Variasi

| Situasi | Apa yang Diubah | Mengapa |
|-----------|----------------|-----|
| **Tidak perlu prefix** | `Prefix = string.Empty` | Menghapus bagian “ABC‑”, menyisakan hanya urutan numerik. |
| **Mulai dari 1** | `Start = 1` | Berguna untuk **add sequential page numbers** sederhana tanpa prefix khusus. |
| **Dokumen besar (>10.000 halaman)** | Tingkatkan `FontSize` atau sesuaikan `Location` (gunakan overload `AddBatesNumbering`) | Mencegah tumpang tindih dengan footer atau header. |
| **File sumber read‑only** | Buka dengan `LoadOptions` yang memungkinkan akses tulis, atau salin file terlebih dahulu | Jika tidak, `document.Save` akan melempar pengecualian. |
| **Penempatan berbeda** | Gunakan `batesOptions.Position = BatesNumberingPosition.TopLeft` (atau enum lain) | Beberapa firma mengharuskan nomor di bagian atas halaman. |

> **Catatan:** Tidak semua perpustakaan menyediakan kelas `BatesNumberingOptions`. Dengan Open XML SDK Anda harus menyisipkan `TextBox` secara manual—prinsipnya sama, hanya kodenya lebih banyak.

## Contoh Lengkap yang Berfungsi

Berikut seluruh program dalam satu tempat. Salin‑tempel ke aplikasi console dan jalankan.

```csharp
using System;
using Aspose.Words;

class Program
{
    static void Main()
    {
        // Load the source document
        Document document = new Document("YOUR_DIRECTORY/input.docx");

        // Define Bates numbering options
        BatesNumberingOptions batesOptions = new BatesNumberingOptions
        {
            Prefix = "ABC",      // custom prefix
            Start = 1000,        // starting number
            FontSize = 9         // font size in points
        };

        // Apply numbering to every page
        document.Pages.AddBatesNumbering(batesOptions);

        // Save the result
        document.Save("YOUR_DIRECTORY/output.docx");

        Console.WriteLine("Bates numbering added successfully!");
    }
}
```

Jalankan program, buka `output.docx`, dan Anda akan melihat penomoran tepat di tempat yang Anda harapkan. 🎉

## Pertanyaan yang Sering Diajukan

**T: Bisakah saya mengubah warna nomor?**  
J: Ya. Setelah memanggil `AddBatesNumbering`, Anda dapat mengambil objek `Shape` yang dihasilkan dan mengatur properti `FillColor`‑nya.

**T: Bagaimana jika saya ingin nomor di sisi kiri bukan kanan?**  
J: Gunakan `batesOptions.Position = BatesNumberingPosition.BottomLeft` (atau `TopLeft`, `TopRight`). API mendukung keempat sudut.

**T: Apakah ini bekerja dengan output PDF?**  
J: Tentu saja. Setelah menambahkan penomoran, panggil `document.Save("output.pdf")`. Nomor akan dirender ke PDF persis seperti di Word.

## Kesimpulan

Anda kini tahu **how to add bates numbering** ke file Word menggunakan C#. Tutorial ini mencakup memuat dokumen, mengonfigurasi **add custom numbers**, menerapkan **add sequential page numbers**, dan menyimpan hasil akhir. Dengan contoh kode lengkap, Anda dapat menambahkan ini ke proyek apa pun dan langsung menstempel dokumen.

Siap untuk tantangan berikutnya? Coba gabungkan dengan proses batch yang mengulang folder berkas, atau jelajahi **add custom page numbers** di header/footer untuk tampilan yang lebih profesional. Bagaimanapun, Anda kini memiliki fondasi kuat untuk tugas otomasi legal‑tech atau kepatuhan apa pun.

Punya pertanyaan atau contoh penggunaan menarik? Tinggalkan komentar di bawah, dan selamat coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}