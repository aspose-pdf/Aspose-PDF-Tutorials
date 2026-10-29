---
category: general
date: 2026-10-07
description: Pelajari cara menambahkan penomoran Bates ke PDF menggunakan C#. Panduan
  langkah demi langkah ini juga mencakup penomoran halaman PDF dan trik penomoran
  lainnya.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add bates numbering
- pdf page numbering
- number pdf pages
- how to add bates
- bates numbering pdf
language: id
lastmod: 2026-10-07
og_description: Tambahkan penomoran Bates ke PDF dengan cepat. Ikuti tutorial ini
  untuk menguasai penomoran halaman PDF, memberi nomor pada halaman PDF, dan mengotomatiskan
  pelacakan dokumen.
og_image_alt: Screenshot of a PDF with Bates numbers added using Aspose.Pdf
og_title: Tambahkan penomoran Bates ke PDF dalam C# – panduan lengkap Aspose
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Learn how to add bates numbering to a PDF using C#. This step‑by‑step
    guide also covers pdf page numbering and other numbering tricks.
  headline: How to add bates numbering to a PDF with Aspose.Pdf
  type: TechArticle
- description: Learn how to add bates numbering to a PDF using C#. This step‑by‑step
    guide also covers pdf page numbering and other numbering tricks.
  name: How to add bates numbering to a PDF with Aspose.Pdf
  steps:
  - name: 1. Can I change the location of the numbers?
    text: Yes. Set `batesOptions.Position = new Position(10, 10, 10, 10);` where the
      four values represent margins from the top, bottom, left, and right edges. Aspose
      also provides predefined enums such as `BatesNumberingPosition.BottomCenter`.
  - name: 2. What if my PDF already contains page numbers?
    text: Adding Bates numbers will **stack** on top of existing numbers. To avoid
      visual clutter, either hide the original numbers (if they are part of a text
      layer) or adjust the `batesOptions` font size and position.
  - name: 3. Does this work with encrypted PDFs?
    text: 'Aspose can open password‑protected PDFs if you supply the password:'
  - name: 4. How do I **number pdf pages** with a simple sequential counter (no prefix/suffix)?
    text: 'Just set `Prefix = string.Empty` and `Suffix = string.Empty`:'
  - name: 5. Can I use this approach in ASP.NET Core to serve PDFs on‑the‑fly?
    text: 'Absolutely. Load the document, apply the numbering, then write the stream
      to the HTTP response:'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Cara menambahkan penomoran Bates ke PDF dengan Aspose.Pdf
url: /id/net/programming-with-pdf-pages/how-to-add-bates-numbering-to-a-pdf-with-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara menambahkan penomoran bates ke PDF dengan Aspose.Pdf

Jika Anda perlu **menambahkan penomoran bates** ke PDF, panduan ini menunjukkan secara tepat cara melakukannya dalam C#. Baik Anda sedang menyiapkan bundel hukum, mengelola berkas kasus, atau hanya menginginkan **penomoran halaman pdf** yang andal, langkah‑langkah di bawah ini memberikan solusi lengkap yang dapat dijalankan.

Dalam tutorial ini Anda akan belajar cara:

* Memuat file PDF yang sudah ada.
* Mengonfigurasi opsi penomoran Bates seperti prefix, nomor mulai, padding digit, pemisah, dan suffix.
* Menerapkan penomoran ke setiap halaman.
* Menyimpan dokumen yang telah diperbarui.

Tidak diperlukan alat eksternal selain pustaka Aspose.Pdf untuk .NET, dan kode ini bekerja dengan .NET 6+ serta .NET Framework 4.7.2+.

---

## Prasyarat

Sebelum Anda memulai, pastikan Anda memiliki:

| Persyaratan | Mengapa penting |
|-------------|-----------------|
| **Aspose.Pdf for .NET** (paket NuGet `Aspose.Pdf`) | Menyediakan kelas `Document` dan `BatesNumberingOptions` yang digunakan dalam kode. |
| **.NET SDK** (6.0 atau lebih baru disarankan) | Memungkinkan Anda untuk mengompilasi dan menjalankan aplikasi konsol C#. |
| **PDF sumber** yang ingin Anda beri nomor | Tutorial ini menggunakan `source.pdf` sebagai contoh; ganti path dengan file Anda sendiri. |
| **Izin menulis** ke folder output | Pemanggilan `Save` perlu menulis file baru. |

Anda dapat menginstal pustaka dengan perintah CLI berikut:

```bash
dotnet add package Aspose.Pdf
```

---

## Langkah 1: Buat proyek konsol baru

Buka terminal dan jalankan:

```bash
dotnet new console -n BatesNumberingDemo
cd BatesNumberingDemo
```

Ini membuat proyek C# minimal yang akan kita isi dengan kode yang diperlukan untuk **menambahkan penomoran bates**.

---

## Langkah 2: Tambahkan direktif `using` yang diperlukan

Buka `Program.cs` dan tambahkan namespace di bagian atas file:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;
```

* `Aspose.Pdf` memberi Anda akses ke kelas `Document` untuk memuat dan menyimpan PDF.  
* `Aspose.Pdf.Text` berisi `BatesNumberingOptions`, objek yang menentukan bagaimana angka muncul.

---

## Langkah 3: Muat PDF sumber

Baris pertama yang dapat dijalankan memuat PDF yang ingin Anda beri nomor. Ganti `"YOUR_DIRECTORY/source.pdf"` dengan path aktual ke file Anda.

```csharp
// Load the source PDF
Document pdf = new Document("YOUR_DIRECTORY/source.pdf");
```

Jika file tidak dapat ditemukan, Aspose melempar `FileNotFoundException`. Untuk menghindarinya, Anda mungkin ingin memvalidasi path terlebih dahulu:

```csharp
if (!System.IO.File.Exists("YOUR_DIRECTORY/source.pdf"))
{
    Console.WriteLine("Source PDF not found.");
    return;
}
```

---

## Langkah 4: Definisikan opsi penomoran Bates

`BatesNumberingOptions` memungkinkan Anda mengontrol setiap elemen visual dari penomoran. Contoh di bawah menunjukkan konfigurasi tipikal untuk berkas kasus hukum:

```csharp
// Define Bates numbering options
BatesNumberingOptions batesOptions = new BatesNumberingOptions
{
    Prefix = "CASE-",          // Text before the numeric part
    StartNumber = 1000,       // First number to use
    Digits = 6,               // Pad with leading zeros (e.g., 001000)
    Separator = "-",          // Character between prefix, number, and suffix
    Suffix = "-2025"          // Text after the numeric part
};
```

**Mengapa setiap properti penting**

| Properti | Tujuan |
|----------|--------|
| `Prefix` | Membantu Anda mengelompokkan dokumen berdasarkan proyek, klien, atau kasus. |
| `StartNumber` | Menetapkan penghitung awal; berguna ketika Anda sudah memiliki file yang sudah bernomor. |
| `Digits` | Menjamin lebar yang seragam, memudahkan penyortiran. |
| `Separator` | Meningkatkan keterbacaan, terutama saat menggabungkan prefix dan suffix. |
| `Suffix` | Memungkinkan Anda menambahkan tahun, versi, atau identifier lain di akhir. |

Anda juga dapat mengontrol penempatan (atas, bawah, kiri, kanan) dan gaya font dengan mengakses `batesOptions.Position` dan `batesOptions.Font`. Untuk kebanyakan skenario, nilai default (bawah‑kanan, 12‑pt Times New Roman) sudah cukup baik.

---

## Langkah 5: Terapkan penomoran ke setiap halaman

Memanggil `pdf.BatesNumbering.Add` menyisipkan angka pada setiap halaman sesuai urutan mereka muncul.

```csharp
// Apply Bates numbering to every page
pdf.BatesNumbering.Add(batesOptions);
```

Jika Anda perlu **menomori halaman pdf** hanya pada sebagian (mis., lewati halaman sampul), Anda dapat memberikan `PageCollection` sebagai gantinya:

```csharp
// Example: skip the first page
pdf.BatesNumbering.Add(batesOptions, pdf.Pages.Skip(1));
```

---

## Langkah 6: Simpan PDF yang telah diperbarui

Akhirnya, tulis dokumen yang telah dimodifikasi ke disk. Nama file biasanya mencerminkan bahwa PDF kini berisi nomor Bates.

```csharp
// Save the PDF with Bates numbers applied
pdf.Save("YOUR_DIRECTORY/bates_numbered.pdf");
Console.WriteLine("Bates numbering added successfully.");
```

Jika folder output tidak ada, Aspose akan membuatnya secara otomatis. Namun, pastikan Anda memiliki izin menulis untuk menghindari `UnauthorizedAccessException`.

---

## Contoh lengkap yang dapat dijalankan

Menggabungkan semua bagian, berikut program lengkap yang dapat Anda salin, tempel, dan jalankan:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Load the source PDF
        // -------------------------------------------------
        const string inputPath = "YOUR_DIRECTORY/source.pdf";
        if (!System.IO.File.Exists(inputPath))
        {
            Console.WriteLine($"Input file not found: {inputPath}");
            return;
        }

        Document pdf = new Document(inputPath);

        // -------------------------------------------------
        // 2️⃣ Configure Bates numbering
        // -------------------------------------------------
        BatesNumberingOptions batesOptions = new BatesNumberingOptions
        {
            Prefix = "CASE-",
            StartNumber = 1000,
            Digits = 6,
            Separator = "-",
            Suffix = "-2025"
        };

        // -------------------------------------------------
        // 3️⃣ Apply the numbering to every page
        // -------------------------------------------------
        pdf.BatesNumbering.Add(batesOptions);

        // -------------------------------------------------
        // 4️⃣ Save the result
        // -------------------------------------------------
        const string outputPath = "YOUR_DIRECTORY/bates_numbered.pdf";
        pdf.Save(outputPath);
        Console.WriteLine($"Bates numbering added. Saved to {outputPath}");
    }
}
```

**Output yang diharapkan** (console):

```
Bates numbering added. Saved to YOUR_DIRECTORY/bates_numbered.pdf
```

Buka `bates_numbered.pdf` dan Anda akan melihat setiap halaman berlabel seperti `CASE-001000-2025`, `CASE-001001-2025`, dll., ditempatkan di sudut kanan‑bawah default.

---

## Pertanyaan yang sering diajukan (FAQ)

### 1. Bisakah saya mengubah lokasi angka?
Ya. Atur `batesOptions.Position = new Position(10, 10, 10, 10);` dimana keempat nilai tersebut mewakili margin dari atas, bawah, kiri, dan kanan. Aspose juga menyediakan enum bawaan seperti `BatesNumberingPosition.BottomCenter`.

### 2. Bagaimana jika PDF saya sudah berisi nomor halaman?
Menambahkan nomor Bates akan **menumpuk** di atas nomor yang sudah ada. Untuk menghindari kekacauan visual, sembunyikan nomor asli (jika mereka berada pada lapisan teks) atau sesuaikan ukuran font dan posisi `batesOptions`.

### 3. Apakah ini bekerja dengan PDF yang terenkripsi?
Aspose dapat membuka PDF yang dilindungi password jika Anda menyediakan password:

```csharp
Document pdf = new Document("source.pdf", new LoadOptions { Password = "mySecret" });
```

Penomoran Bates kemudian diterapkan dengan cara yang sama.

### 4. Bagaimana cara **menomori halaman pdf** dengan penghitung berurutan sederhana (tanpa prefix/suffix)?
Cukup atur `Prefix = string.Empty` dan `Suffix = string.Empty`:

```csharp
BatesNumberingOptions simple = new BatesNumberingOptions
{
    StartNumber = 1,
    Digits = 4   // 0001, 0002, …
};
pdf.BatesNumbering.Add(simple);
```

### 5. Bisakah saya menggunakan pendekatan ini di ASP.NET Core untuk menyajikan PDF secara langsung?
Tentu saja. Muat dokumen, terapkan penomoran, lalu tulis stream ke respons HTTP:

```csharp
using (var ms = new MemoryStream())
{
    pdf.Save(ms);
    ms.Position = 0;
    return File(ms, "application/pdf", "bates_numbered.pdf");
}
```

---

## Kasus tepi dan tips praktik terbaik

| Situasi | Pendekatan yang direkomendasikan |
|---------|----------------------------------|
| **PDF besar** (ratusan halaman) | Panggil `pdf.BatesNumbering.Add` **setelah** Anda melakukan transformasi tingkat halaman apa pun untuk menghindari pemrosesan ulang halaman yang sama berkali‑kali. |
| **Font khusus** | Atur `batesOptions.Font = FontRepository.FindFont("Arial")` dan sesuaikan `batesOptions.FontSize` untuk keterbacaan yang lebih baik pada dokumen yang dipindai. |
| **Pekerjaan batch dengan performa kritis** | Gunakan kembali satu instance `Document` saat memproses banyak file dalam loop; buang (dispose) setelah setiap iterasi untuk membebaskan memori. |
| **Karakter internasional** | Gunakan font yang kompatibel Unicode (mis., `Times New Roman Unicode`) untuk memastikan prefix atau suffix ditampilkan dengan benar. |
| **Kompatibilitas versi** | Kode ini bekerja dengan Aspose.Pdf 23.10 dan yang lebih baru. Jika Anda menargetkan versi lebih lama, periksa referensi API untuk perubahan nama properti. |

---

## Kesimpulan

Anda kini tahu cara **menambahkan penomoran bates** ke PDF menggunakan Aspose.Pdf untuk .NET. Tutorial ini mencakup memuat PDF, mengonfigurasi `BatesNumberingOptions`, menerapkan angka ke setiap halaman, dan menyimpan hasilnya. Dengan blok‑blok bangunan ini Anda juga dapat mengimplementasikan **penomoran halaman pdf** umum, **menomori halaman pdf** dengan format khusus, dan mengintegrasikan proses ke dalam pipeline otomatisasi yang lebih besar.

**Langkah selanjutnya**

* Jelajahi API **bates numbering pdf** lebih lanjut untuk menyesuaikan font, warna, dan penempatan.  
* Gabungkan teknik ini dengan **tanda tangan digital** untuk membuat bundel hukum yang tahan manipulasi.  
* Lihat kemampuan **penggabungan PDF** Aspose jika Anda perlu menggabungkan beberapa berkas kasus sebelum penomoran.

Silakan bereksperimen dengan berbagai prefix, suffix, dan panjang digit untuk menyesuaikan standar pengarsipan organisasi Anda. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Create PDF Document C# – Add Bates Numbering Guide](/pdf/english/net/document-creation/create-pdf-document-c-add-bates-numbering-guide/)
- [How to Add Bates Numbering in PDF with C# – Complete Guide](/pdf/english/net/programming-with-stamps-and-watermarks/how-to-add-bates-numbering-in-pdf-with-c-complete-guide/)
- [Aspose PDF Tutorial – Insert a Blank Page and Update Bates Numbering](/pdf/english/net/programming-with-pdf-pages/aspose-pdf-tutorial-insert-a-blank-page-and-update-bates-num/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}