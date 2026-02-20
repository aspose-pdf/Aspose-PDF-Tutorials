---
category: general
date: 2026-02-20
description: Tambahkan Penomoran Bates ke dokumen Anda dan konversi DOCX ke PDF dengan
  nomor halaman khusus dalam C#. Pelajari cara menambahkan nomor halaman berurutan
  dan menyimpan dokumen sebagai PDF.
draft: false
keywords:
- add bates numbering
- convert docx to pdf
- add custom page numbers
- save document as pdf
- add sequential page numbers
language: id
og_description: Tambahkan Penomoran Bates ke file DOCX Anda dan konversi menjadi PDF
  dengan nomor halaman khusus menggunakan C#. Panduan ini memandu Anda melalui setiap
  langkah.
og_title: Tambahkan Penomoran Bates ke DOCX dan Konversi ke PDF – Tutorial C#
tags:
- C#
- PDF
- Document Automation
title: Tambahkan Penomoran Bates ke DOCX dan Konversi ke PDF – Panduan Lengkap C#
url: /id/net/document-conversion/add-bates-numbering-to-docx-and-convert-to-pdf-complete-c-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Menambahkan Penomoran Bates ke DOCX dan Mengonversi ke PDF – Panduan Lengkap C#

Pernahkah Anda perlu **add bates numbering** ke sebuah brief hukum tetapi tidak yakin cara mengotomatiskannya? Anda bukan satu-satunya. Di banyak firma proses manual menempelkan nomor pada setiap halaman sangat memakan waktu, dan risiko kehilangan nomor dapat menjadi mahal.  

Berita baiknya? Dengan beberapa baris C# Anda dapat **add bates numbering**, **convert docx to pdf**, dan **save document as pdf** dalam satu alur yang mulus. Di bawah ini Anda akan menemukan solusi mandiri yang berfungsi hari ini, plus “mengapa” di balik setiap pilihan sehingga Anda dapat menyesuaikannya untuk alur kerja Anda.

---

## Apa yang Dibahas dalam Tutorial Ini

Dalam bagian berikut kami akan:

1. Memuat file DOCX dari disk.  
2. Mendefinisikan **custom page numbers** (prefix, nilai mulai, dan format opsional).  
3. Menerapkan **add bates numbering** ke setiap halaman sumber.  
4. **Convert docx to pdf** sambil mempertahankan penomoran.  
5. **Save document as pdf** ke lokasi pilihan Anda.  

Tanpa layanan eksternal, tanpa pengaturan tersembunyi—hanya C# biasa dan perpustakaan pemrosesan dokumen populer (mis., GroupDocs.Conversion). Pada akhir tutorial Anda akan memiliki aplikasi console siap‑jalankan yang menghasilkan PDF dengan nomor halaman berurutan tepat di tempat yang Anda butuhkan.

---

## Prasyarat

- **.NET 6.0** atau lebih baru (kode ini juga dapat dikompilasi pada .NET Framework 4.7+).  
- Paket NuGet **GroupDocs.Conversion** (atau perpustakaan apa pun yang menyediakan `Document`, `BatesNumberingOptions`, dan `Pages.AddBatesNumbering`). Instal dengan:  

```bash
dotnet add package GroupDocs.Conversion
```

- File DOCX yang ingin Anda proses (letakkan di `YOUR_DIRECTORY/input.docx`).  
- Familiaritas dasar dengan proyek console C#.

---

## Implementasi Langkah‑per‑Langkah

### ## Add Bates Numbering – Preparing the Project

Pertama, buat proyek console baru dan impor namespace yang diperlukan:

```csharp
using System;
using GroupDocs.Conversion;               // Core document handling
using GroupDocs.Conversion.Options;       // Options like BatesNumberingOptions
using GroupDocs.Conversion.Options.Pdf;   // PDF‑specific options (if needed)

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll fill the body in the next steps
        }
    }
}
```

> **Mengapa ini penting:** Mengimpor namespace yang tepat memberi Anda akses ke kelas `Document` (titik masuk) dan objek **BatesNumberingOptions** yang mengontrol format penomoran. Melewatkan langkah ini akan menghasilkan error pada waktu kompilasi, itulah mengapa kami memulainya di sini.

### ## Load the Source DOCX File

Sekarang kami membaca file Word. Konstruktor `Document` menerima sebuah path, jadi pastikan path Anda absolut atau relatif terhadap executable.

```csharp
// Step 1: Load the source document
string inputPath = @"YOUR_DIRECTORY/input.docx";
Document document = new Document(inputPath);
```

> **Tips profesional:** Jika file mungkin tidak ada, bungkus dalam `try/catch` dan tampilkan pesan yang ramah. Ini mencegah seluruh aplikasi crash dan meningkatkan pengalaman pengguna.

### ## Define Custom Page Numbers (Bates Options)

Berikutnya kami menyiapkan **add custom page numbers**. Anda dapat mengubah `Prefix`, `Start`, dan bahkan format nomor (mis., leading zeros).

```csharp
// Step 2: Define Bates numbering options (prefix and starting number)
var batesOptions = new BatesNumberingOptions
{
    Prefix = "ABC",      // Anything you need – legal firms love prefixes
    Start = 1000,        // First number in the sequence
    // Optional: NumberFormat = "0000" // forces four‑digit padding
};
```

> **Mengapa Anda memerlukan prefix:** Di banyak yurisdiksi prefix mengidentifikasi berkas kasus atau klien. Perpustakaan akan menambahkan prefix tersebut ke setiap nomor halaman secara otomatis.

### ## Apply Bates Numbering to Every Page

Dengan opsi siap, kami memberi tahu dokumen untuk menstempel setiap halaman:

```csharp
// Step 3: Apply Bates numbering to every page in the document
document.Pages.AddBatesNumbering(batesOptions);
```

> **Kasus khusus:** Jika DOCX Anda sudah berisi footer, perpustakaan secara default akan menimpa nomor. Beberapa perpustakaan memungkinkan Anda menentukan penempatan (atas‑kanan, bawah‑tengah, dll.) melalui properti tambahan pada `BatesNumberingOptions`.

### ## Convert to PDF and Save

Akhirnya, kami menghasilkan PDF yang berisi nomor yang baru ditambahkan. Metode `Save` secara otomatis menebak format dari ekstensi file.

```csharp
// Step 4: Save the document with the new Bates numbers as PDF
string outputPath = @"YOUR_DIRECTORY/output.pdf";
document.Save(outputPath);
Console.WriteLine($"✅ PDF saved with Bates numbering at: {outputPath}");
```

> **Mengapa kami menyimpan sebagai PDF:** PDF mempertahankan tata letak, font, dan posisi tepat nomor, menjadikannya ideal untuk pengajuan hukum dan arsip.

---

## Contoh Lengkap yang Berfungsi

Menggabungkan semuanya, berikut program lengkap yang dapat Anda copy‑paste ke `Program.cs` dan jalankan:

```csharp
using System;
using GroupDocs.Conversion;
using GroupDocs.Conversion.Options;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the source DOCX
            string inputPath = @"YOUR_DIRECTORY/input.docx";
            Document document = new Document(inputPath);

            // 2️⃣ Set up Bates numbering (custom prefix & start)
            var batesOptions = new BatesNumberingOptions
            {
                Prefix = "ABC",
                Start = 1000
                // NumberFormat = "0000" // Uncomment for zero‑padded numbers
            };

            // 3️⃣ Apply the numbering to every page
            document.Pages.AddBatesNumbering(batesOptions);

            // 4️⃣ Convert and save as PDF
            string outputPath = @"YOUR_DIRECTORY/output.pdf";
            document.Save(outputPath);

            Console.WriteLine($"✅ Done! PDF with Bates numbers saved to {outputPath}");
        }
    }
}
```

### Expected Result

Buka `output.pdf` di viewer apa pun. Anda akan melihat setiap halaman bernomor seperti **ABC‑1000**, **ABC‑1001**, … hingga halaman terakhir. Nomor muncul di lokasi default (bawah‑kanan) kecuali Anda mengubah opsi.

---

## Common Questions & Edge Cases

| Pertanyaan | Jawaban |
|----------|--------|
| **Bisakah saya mengubah penempatan nomor?** | Ya. Sebagian besar perpustakaan menyediakan properti `Position` atau `Margin` pada `BatesNumberingOptions`. Set `batesOptions.Position = BatesNumberingPosition.BottomLeft;` untuk sudut yang berbeda. |
| **Bagaimana jika DOCX memiliki footer yang sudah ada?** | Perpustakaan biasanya menimpa area tempat nomor digambar. Jika Anda perlu mempertahankan footer yang ada, cari flag `OverwriteExisting` atau tambahkan nomor secara manual melalui templat footer khusus. |
| **Apakah saya perlu khawatir tentang karakter Unicode?** | Prefix dapat berisi teks Unicode apa pun, tetapi pastikan font yang digunakan dalam PDF mendukung karakter tersebut; jika tidak, mereka akan muncul sebagai kotak. |
| **Bagaimana cara menambahkan nol di depan?** | Set `NumberFormat = "0000"` (atau pola apa pun) di `BatesNumberingOptions`. Ini memaksa nomor menjadi seperti 0010, 0011, dll. |
| **Bisakah saya memproses banyak file DOCX secara batch?** | Tentu saja. Bungkus logika dalam loop `foreach (var file in Directory.GetFiles(..., "*.docx"))` dan gunakan kembali objek `batesOptions` yang sama atau ubah per file. |

---

## Pro Tips & Best Practices

- **Performance:** Jika Anda memproses ratusan file, gunakan kembali satu instance `Document` bila memungkinkan dan panggil `document.Dispose()` setelah setiap penyimpanan untuk membebaskan sumber daya tak terkelola.  
- **Version control:** Simpan nilai `Prefix` dan `Start` dalam file konfigurasi (`appsettings.json`). Dengan begitu Anda dapat mengubahnya tanpa harus mengkompilasi ulang.  
- **Testing:** Jalankan program pada DOCX satu halaman terlebih dahulu. Verifikasi nomor muncul di tempat yang diharapkan sebelum memperluas ke kontrak besar.  
- **Compliance:** Beberapa yurisdiksi mengharuskan nomor Bates setidaknya 8 karakter. Sesuaikan `Prefix` dan `NumberFormat` sesuai kebutuhan.  

---

## Next Steps – Expand Your Automation

Setelah Anda menguasai **add bates numbering**, pertimbangkan peningkatan terkait berikut:

- **Convert docx to pdf** sambil mempertahankan hyperlink dan bookmark.  
- **Add custom page numbers** ke PDF yang sudah ada menggunakan perpustakaan khusus PDF (mis., iTextSharp).  
- **Save document as pdf** dengan pengaturan kualitas berbeda untuk web vs. cetak.  
- **Add sequential page numbers** ke gambar yang dipindai dengan memproses OCR setiap halaman terlebih dahulu.  

Setiap topik ini dibangun di atas konsep inti yang sama—memuat dokumen, mengonfigurasi opsi, dan menyimpan hasil—sehingga Anda akan merasa nyaman.

---

## Conclusion

Kami telah membahas solusi lengkap end‑to‑end untuk **add bates numbering** pada file DOCX, **convert docx to pdf**, dan **save document as pdf** dengan nomor halaman berurutan yang dapat disesuaikan. Kode singkat, dependensi minimal, dan pendekatan cukup fleksibel untuk proyek firma hukum kecil maupun pipeline perusahaan berskala besar.

Cobalah, ubah prefix, bereksperimen dengan format nomor, dan Anda akan memiliki alat yang kuat dalam kotak peralatan pengembang Anda. Jika Anda menemukan keanehan atau memiliki ide untuk otomasi lebih lanjut, tinggalkan komentar di bawah—selamat coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}