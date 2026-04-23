---
category: general
date: 2026-03-22
description: Tambahkan penomoran Bates pada PDF dengan cepat menggunakan Aspose.Pdf.
  Pelajari cara menambahkan Bates, menambahkan nomor halaman berurutan, menambahkan
  footer khusus pada PDF, dan menambahkan artefak ke PDF dalam hitungan menit.
draft: false
keywords:
- add bates numbering pdf
- how to add bates
- add sequential page numbers
- add custom footer pdf
- add artifact to pdf
language: id
og_description: Tambahkan penomoran Bates pada PDF menggunakan Aspose.Pdf. Panduan
  ini menunjukkan cara menambahkan bates, menambahkan nomor halaman berurutan, menambahkan
  footer kustom pada PDF, dan menambahkan artefak ke PDF.
og_title: Tambahkan Penomoran Bates pada PDF – Tutorial C# Langkah demi Langkah
tags:
- Aspose.Pdf
- C#
- PDF automation
title: Menambahkan Penomoran Bates pada PDF – Panduan Lengkap C#
url: /id/net/programming-with-stamps-and-watermarks/add-bates-numbering-pdf-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Menambahkan Penomoran Bates PDF – Panduan Lengkap C#

Pernahkah Anda perlu **add bates numbering pdf** ke sekumpulan dokumen hukum tetapi tidak yakin harus mulai dari mana? Anda bukan yang pertama—banyak pengembang mengalami hal yang sama saat membangun alat manajemen kasus. Kabar baiknya? Dengan Aspose.Pdf Anda dapat **add bates**, **add sequential page numbers**, dan bahkan **add custom footer pdf** hanya dengan beberapa baris kode.  

Dalam tutorial ini kami akan membahas seluruh proses, mulai dari menginstal pustaka hingga menyimpan file akhir, serta memberikan tips tentang cara **add artifact to pdf** tanpa merusak konten yang sudah ada. Pada akhir tutorial Anda akan memiliki potongan kode siap‑jalan yang dapat Anda sisipkan ke proyek .NET mana pun.

## Apa yang Anda Butuhkan

- .NET 6+ (kode ini bekerja pada .NET Core dan .NET Framework)  
- Lisensi Aspose.Pdf untuk .NET yang valid (Anda dapat memulai dengan evaluasi gratis)  
- File PDF input (`input.pdf`) yang ditempatkan di folder yang dapat Anda referensikan  
- Visual Studio, Rider, atau editor C# favorit Anda  

Itu saja—tidak ada paket NuGet tambahan selain Aspose.Pdf.

## Langkah 1: Instal Aspose.Pdf via NuGet

Langkah pertama—pasang pustaka ke mesin Anda. Buka terminal di folder proyek dan jalankan:

```bash
dotnet add package Aspose.Pdf
```

Atau, jika Anda menggunakan Package Manager Console di Visual Studio:

```powershell
Install-Package Aspose.Pdf
```

*Pro tip:* Setelah instalasi, pastikan folder `Aspose.Pdf` muncul di bawah `Dependencies → Packages` di Solution Explorer Anda.

## Langkah 2: Muat Dokumen PDF Sumber

Sekarang kita buat objek `Document` yang mewakili PDF yang ingin kita beri cap. Menggunakan pernyataan `using` memastikan handle file dilepaskan secara otomatis.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using System.Drawing; // For Color

// Step 2: Load the source PDF
using var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");
```

Mengapa menggunakan `using var`? Ini menjamin disposisi bahkan jika terjadi pengecualian, mencegah masalah penguncian file saat Anda mencoba menimpa file yang sama.

## Langkah 3: Buat dan Konfigurasikan Bates Numbering Artifact

Nomor Bates pada dasarnya adalah artefak teks yang berada dalam struktur logis PDF. Anda dapat memperlakukannya seperti **custom footer pdf** karena muncul di setiap halaman tanpa menjadi bagian dari aliran konten halaman.

```csharp
// Step 3: Define the Bates numbering artifact
var batesArtifact = new BatesNumberingArtifact
{
    Prefix = "INV-",          // Optional prefix – change as needed
    Start = 1000,             // Starting number
    Format = "0000",          // Zero‑padded format (e.g., 1000 → 1000)
    X = 500,                  // Horizontal position (points from left)
    Y = 20,                   // Vertical position (points from bottom)
    FontSize = 10,
    FontColor = Color.Black
};
```

### Mengapa Pengaturan Ini Penting

- **Prefix**: Berguna untuk membedakan tipe dokumen (misalnya “INV‑” untuk faktur).  
- **Start**: Menentukan nomor pertama; Anda dapat mengisinya dari basis data jika memerlukan kesinambungan antar file.  
- **Format**: `"0000"` memaksa tampilan empat digit, memastikan perataan ketika nomor bertambah.  
- **X/Y**: Koordinat diukur dari sudut kiri‑bawah, sehingga `Y = 20` menempatkan teks tepat di atas margin halaman. Sesuaikan `X` jika Anda ingin nomor rata kiri atau terpusat.

Jika Anda ingin **add sequential page numbers** alih‑alih nomor Bates, cukup hilangkan `Prefix` dan ubah `Format` menjadi `"###"` atau pola lain yang Anda inginkan.

## Langkah 4: Terapkan Artefak ke Semua Halaman

Aspose.Pdf memungkinkan Anda melampirkan artefak ke seluruh dokumen dalam satu panggilan. Ini adalah cara paling efisien untuk **add artifact to pdf** tanpa harus mengulangi setiap halaman secara manual.

```csharp
// Step 4: Apply the artifact to the whole document
pdfDocument.Pages.AddArtifact(batesArtifact);
```

Di balik layar, Aspose menambahkan artefak ke kamus halaman setiap halaman, yang berarti penomoran menjadi bagian dari struktur logis PDF—sempurna untuk ekstraksi atau pencarian di kemudian hari.

## Langkah 5: Simpan PDF yang Telah Diperbarui

Akhirnya, tulis perubahan kembali ke disk. Anda dapat menimpa file asli atau menyimpan ke file baru; yang terakhir lebih aman selama pengembangan.

```csharp
// Step 5: Save the PDF with Bates numbers
pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
```

Saat Anda membuka `output.pdf` di penampil, Anda akan melihat “INV‑1000”, “INV‑1001”, … di kanan‑bawah setiap halaman.

### Memverifikasi Hasil

Buka PDF di Adobe Acrobat atau penampil apa pun dan perhatikan nomor‑nomornya. Jika Anda perlu mengonfirmasi secara programatis, Anda dapat membaca kembali artefak:

```csharp
foreach (var page in pdfDocument.Pages)
{
    foreach (var artifact in page.Artifacts)
    {
        Console.WriteLine($"Page {page.Number}: {artifact.Text}");
    }
}
```

Potongan kode tersebut mencetak label Bates tiap halaman—berguna untuk pengujian otomatis.

## Kasus Khusus & Pertanyaan Umum

### Bagaimana Jika PDF Saya Sudah Memiliki Footer?

Menambahkan artefak tidak akan menimpa footer yang ada karena artefak berada di lapisan terpisah. Namun, jika tumpang‑tindih visual menjadi masalah, sesuaikan koordinat `Y` atau tingkatkan offset `X` untuk memindahkan nomor Bates ke tempat yang lebih aman.

### Bisakah Saya Menggunakan Font atau Warna yang Berbeda?

Tentu saja. `BatesNumberingArtifact` mewarisi dari `Artifact`, sehingga Anda dapat mengatur `Font`, `FontColor`, dan bahkan `Opacity`. Contoh:

```csharp
batesArtifact.Font = FontRepository.FindFont("Arial");
batesArtifact.FontColor = Color.FromArgb(255, 0, 0); // Red
```

### Bagaimana Cara Mengatur Ulang Counter untuk Dokumen Baru?

Cukup ubah `Start` sebelum memanggil `AddArtifact`. Jika Anda menghasilkan banyak PDF dalam sebuah loop, simpan counter yang berjalan di logika aplikasi Anda.

### Apakah Pendekatan Ini Kompatibel dengan PDF yang Enkripsi?

Aspose.Pdf dapat membuka PDF terenkripsi jika Anda menyediakan kata sandi:

```csharp
var loadOptions = new LoadOptions { Password = "mySecret" };
using var pdfDocument = new Document("encrypted.pdf", loadOptions);
```

Setelah dekripsi, langkah‑langkah penambahan artefak yang sama bekerja dengan sempurna.

## Contoh Lengkap yang Siap Jalan

Berikut adalah program lengkap yang siap dijalankan. Tempelkan ke aplikasi console, sesuaikan jalur file, dan tekan **F5**.

```csharp
using System;
using System.Drawing;               // For Color
using Aspose.Pdf;
using Aspose.Pdf.Annotations;

class Program
{
    static void Main()
    {
        // Load the source PDF
        using var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");

        // Create the Bates numbering artifact
        var batesArtifact = new BatesNumberingArtifact
        {
            Prefix = "INV-",
            Start = 1000,
            Format = "0000",
            X = 500,
            Y = 20,
            FontSize = 10,
            FontColor = Color.Black
        };

        // Apply the artifact to every page
        pdfDocument.Pages.AddArtifact(batesArtifact);

        // Save the result
        pdfDocument.Save("YOUR_DIRECTORY/output.pdf");

        Console.WriteLine("Bates numbering added successfully!");
    }
}
```

**Output yang diharapkan:** Konsol mencetak “Bates numbering added successfully!” dan `output.pdf` berisi label berurutan seperti `INV‑1000`, `INV‑1001`, dll., yang ditempatkan di kanan‑bawah setiap halaman.

## Ringkasan Cepat

- **Tujuan utama:** **add bates numbering pdf** menggunakan Aspose.Pdf.  
- Kami membahas **how to add bates**, **add sequential page numbers**, dan **add custom footer pdf** melalui satu artefak.  
- Tutorial menunjukkan cara **add artifact to pdf**, menangani kasus khusus, dan memverifikasi hasil.  

## Apa Selanjutnya?

- **Prefix dinamis:** Ambil nilai dari basis data untuk menghasilkan “CASE‑2023‑001”, “CASE‑2023‑002”, …  
- **Penempatan bersyarat:** Gunakan deteksi ukuran halaman (`page.MediaBox`) untuk menengahkan nomor pada halaman lanskap.  
- **Kombinasikan dengan watermark:** Tambahkan logo semi‑transparan bersamaan dengan nomor Bates untuk branding.  

Silakan bereksperimen—mungkin Anda akan menemukan cara yang lebih cerdas untuk memproses ribuan file sekaligus. Jika mengalami masalah, tinggalkan komentar atau periksa dokumentasi resmi Aspose (sangat jelas). Selamat coding!  

![add bates numbering pdf example](https://example.com/bates-numbering-screenshot.png "Screenshot showing add bates numbering pdf in a PDF viewer")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}