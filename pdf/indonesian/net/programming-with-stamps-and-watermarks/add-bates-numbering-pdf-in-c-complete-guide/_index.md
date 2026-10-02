---
category: general
date: 2026-03-14
description: Tambahkan Penomoran Bates pada PDF menggunakan Aspose.Pdf di C#. Pelajari
  cara menambahkan Bates dan menambahkan nomor halaman berurutan secara otomatis untuk
  dokumen hukum atau arsip.
draft: false
keywords:
- add bates numbering pdf
- how to add bates
- add sequential page numbers
- Aspose PDF Bates artifact
- C# PDF automation
language: id
og_description: Tambahkan Penomoran Bates pada PDF langkah demi langkah. Tutorial
  ini menunjukkan cara menambahkan Bates dan menambahkan nomor halaman berurutan menggunakan
  Aspose.Pdf untuk .NET.
og_title: Menambahkan Penomoran Bates pada PDF di C# – Panduan Lengkap
tags:
- Aspose.Pdf
- C#
- PDF
- Bates numbering
title: Menambahkan Penomoran Bates pada PDF di C# – Panduan Lengkap
url: /id/net/programming-with-stamps-and-watermarks/add-bates-numbering-pdf-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Menambahkan Penomoran Bates pada PDF – Panduan Lengkap

Pernahkah Anda perlu **add bates numbering pdf** ke dalam satu paket hukum yang besar tetapi tidak yakin harus mulai dari mana? Menambahkan nomor Bates adalah prosedur rutin, namun secara mengejutkan rumit, dalam alur kerja peninjauan dokumen. Kabar baik? Dengan Aspose.Pdf untuk .NET Anda dapat mengotomatiskan semuanya dalam beberapa baris kode.

Dalam panduan ini kami akan menjelaskan **how to add bates** pada setiap halaman PDF, membahas opsi **add sequential page numbers**, dan menunjukkan contoh kode siap‑jalankan. Pada akhir Anda akan memiliki solusi mandiri yang dapat Anda sisipkan ke dalam proyek C# mana pun—tanpa skrip tambahan, tanpa stamping manual.

## Apa yang Anda Butuhkan

- **Aspose.Pdf for .NET** (versi 23.10 atau lebih baru). Perpustakaan ini bersifat komersial, tetapi evaluasi gratis sudah cukup untuk pengujian.
- Lingkungan pengembangan .NET (Visual Studio, Rider, atau `dotnet` CLI).
- PDF input (`input.pdf`) yang ingin Anda beri tag.
- Sedikit kesabaran untuk kasus tepi sesekali (kami akan membahasnya).

Jika Anda sudah memiliki semua itu, bagus—mari kita mulai.

![Add Bates Numbering PDF example](/images/bates-numbering-example.png "Screenshot showing a PDF with add bates numbering pdf applied")

## Langkah 1: Siapkan Proyek dan Instal Aspose.Pdf

Untuk menjaga kebersihan, mulai dengan aplikasi console baru:

```bash
dotnet new console -n BatesNumberingDemo
cd BatesNumberingDemo
dotnet add package Aspose.Pdf
```

Perintah `dotnet add package` mengambil assembly Aspose.Pdf terbaru dari NuGet, sehingga Anda siap untuk menulis kode.

### Mengapa aplikasi console?

Aplikasi console ringan, dapat dijalankan di mana saja, dan memungkinkan Anda fokus pada logika PDF tanpa gangguan UI. Tentu saja, Anda dapat nanti memigrasikan kode ke dalam web API atau layanan latar belakang—tidak ada yang dalam logika inti yang mengikat Anda pada console.

## Langkah 2: Muat PDF Sumber

Membuka dokumen sangat sederhana. Kami akan menggunakan blok `using` sehingga handle file dilepaskan secara otomatis.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using System.Drawing;   // Required for Color

class Program
{
    static void Main()
    {
        // Adjust these paths to match your environment
        string sourcePdfPath = @"C:\Docs\input.pdf";
        string outputPdfPath = @"C:\Docs\output.pdf";

        // Load the PDF – this is where the “add bates numbering pdf” process begins
        using (var pdfDocument = new Document(sourcePdfPath))
        {
            // Next steps go here...
        }
    }
}
```

**Apa yang terjadi?** Kelas `Document` mewakili seluruh file PDF. Dengan membungkusnya dalam `using`, kami menjamin bahwa `Dispose` dijalankan, mengirimkan semua perubahan yang tertunda ke disk.

## Langkah 3: Definisikan Bates Number Artifact (Inti “how to add bates”)

Aspose.Pdf memperlakukan nomor Bates sebagai *artifacts*—metadata yang dapat ditampilkan di layar atau dicetak, tetapi tidak menjadi aliran konten permanen kecuali Anda meratakan (flatten) PDF. Berikut objek yang akan kami lampirkan pada setiap halaman:

```csharp
var batesArtifact = new BatesNumberArtifact
{
    Prefix = "CASE-",
    StartNumber = 1000,
    Increment = 1,
    X = 36,               // 0.5 inch from the left edge (points)
    Y = 36,               // 0.5 inch from the bottom edge (points)
    FontSize = 9,
    FontColor = Color.Black
};
```

### Mengapa menggunakan artifact?

- **Performance:** Nomor dirender secara langsung, sehingga Anda dapat mengubah prefix atau nomor awal tanpa menulis ulang seluruh PDF.
- **Flexibility:** Anda dapat kemudian meratakan PDF jika memerlukan stempel “hard‑coded” untuk pengajuan hukum.
- **Precision:** Penempatan menggunakan poin (1/72 inci), memberikan kontrol pixel‑perfect.

Jika Anda memerlukan prefix yang berbeda atau font yang lebih besar, cukup sesuaikan properti. Field `Increment` menentukan bagaimana nomor bertambah dari halaman ke halaman—sempurna untuk kebutuhan **add sequential page numbers**.

## Langkah 4: Lampirkan Artifact ke Setiap Halaman

Sekarang kita melakukan loop melalui koleksi `Pages` dan menambahkan artifact. Ini adalah aksi nyata “add bates numbering pdf”.

```csharp
foreach (Page page in pdfDocument.Pages)
{
    page.Artifacts.Add(batesArtifact);
}
```

### Catatan Edge‑Case

Jika PDF Anda sudah berisi Bates artifacts, Anda mungkin akan mendapatkan duplikat. Guard sederhana dapat mencegah hal itu:

```csharp
foreach (Page page in pdfDocument.Pages)
{
    bool alreadyHasBates = page.Artifacts.Any(a => a is BatesNumberArtifact);
    if (!alreadyHasBates)
        page.Artifacts.Add(batesArtifact);
}
```

Pengecekan kecil itu menyelamatkan Anda dari situasi double‑stamp yang berantakan, terutama saat memproses batch dokumen yang telah ditandai sebelumnya.

## Langkah 5: Simpan PDF yang Diperbarui

Akhirnya, tulis kembali file ke disk. Anda dapat menimpa file asli atau membuat file baru—di sini kami akan menghasilkan salinan baru:

```csharp
pdfDocument.Save(outputPdfPath);
Console.WriteLine($"Bates numbers added successfully. Output saved to {outputPdfPath}");
```

Saat Anda membuka `output.pdf` di viewer apa pun, Anda akan melihat “CASE‑1000”, “CASE‑1001”, dll., di pojok kiri bawah setiap halaman.

### Opsional: Meratakan (Flatten) PDF

Jika penerima memerlukan PDF yang tidak dapat diedit (umum dalam pengajuan ke pengadilan), ratakan halaman:

```csharp
pdfDocument.FlattenAllPages();   // Turns artifacts into permanent content
pdfDocument.Save(outputPdfPath);
```

Meratakan adalah operasi satu kali; setelah itu, nomor Bates menjadi bagian dari aliran konten halaman dan tidak dapat diubah tanpa pemrosesan ulang.

## Contoh Kerja Lengkap

Berikut adalah program lengkap yang dapat Anda salin‑tempel ke `Program.cs`. Ini mencakup langkah flatten opsional yang dikomentari untuk memudahkan pengaktifan.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using System;
using System.Drawing;
using System.Linq;

class Program
{
    static void Main()
    {
        string sourcePdfPath = @"C:\Docs\input.pdf";
        string outputPdfPath = @"C:\Docs\output.pdf";

        using (var pdfDocument = new Document(sourcePdfPath))
        {
            var batesArtifact = new BatesNumberArtifact
            {
                Prefix = "CASE-",
                StartNumber = 1000,
                Increment = 1,
                X = 36,
                Y = 36,
                FontSize = 9,
                FontColor = Color.Black
            };

            foreach (Page page in pdfDocument.Pages)
            {
                // Prevent duplicate artifacts if the PDF was processed before
                bool alreadyHasBates = page.Artifacts.Any(a => a is BatesNumberArtifact);
                if (!alreadyHasBates)
                    page.Artifacts.Add(batesArtifact);
            }

            // Uncomment the next line if you need a flattened PDF for legal submission
            // pdfDocument.FlattenAllPages();

            pdfDocument.Save(outputPdfPath);
        }

        Console.WriteLine($"Bates numbers added successfully. Output saved to {outputPdfPath}");
    }
}
```

Jalankan dengan `dotnet run` dan lihat console mengonfirmasi operasi.

## Pertanyaan Umum & Tips Pro

| Question | Answer |
|----------|--------|
| **Bisakah saya mengubah posisi per halaman?** | Ya. Alih-alih satu `batesArtifact`, buat yang baru di dalam loop dan atur `X`/`Y` berdasarkan ukuran halaman. |
| **Bagaimana jika PDF dilindungi kata sandi?** | Muat dengan `new Document(sourcePdfPath, new LoadOptions { Password = "mySecret" })`. Sisa alur kerja tetap tidak berubah. |
| **Apakah saya perlu khawatir tentang performa pada file besar?** | Menambahkan artifacts memiliki kompleksitas O(N) dimana N = jumlah halaman, dan penggunaan memori tetap rendah karena Aspose memproses halaman secara streaming. Untuk PDF >10 000 halaman, pertimbangkan memproses dalam batch untuk menghindari jeda GC yang lama. |
| **Apakah penomoran dapat direset per bagian?** | Tentu saja. Set `StartNumber` ke nilai baru sebelum Anda mencapai halaman pertama bagian berikutnya, atau buat `BatesNumberArtifact` kedua dengan `Prefix` yang berbeda. |
| **Apakah ini akan bekerja di .NET Core?** | Ya. Aspose.Pdf mendukung .NET Framework, .NET Core, dan .NET 5/6+. Cukup target runtime yang sesuai di csproj Anda. |

### Tips Pro

Ketika Anda menangani **add sequential page numbers** untuk satu set multi‑volume, simpan nomor terakhir yang digunakan dalam file JSON kecil. Baca sebelum memulai, tingkatkan sesuai, lalu tulis kembali. Lapisan persistensi kecil ini mencegah penggunaan kembali nomor secara tidak sengaja antar run.

## Memverifikasi Hasil

Buka `output.pdf` di Adobe Reader, Foxit, atau bahkan Chrome. Anda harus melihat sesuatu seperti:

```
CASE-1000   (Page 1)
CASE-1001   (Page 2)
…
CASE-1015   (Page 16)
```

Jika Anda meratakan PDF, nomor menjadi bagian dari grafik halaman—klik kanan → “Inspect” akan menampilkannya sebagai objek teks biasa.

## Kesimpulan

Kami baru saja membahas cara **add bates numbering pdf** menggunakan Aspose.Pdf, mengeksplor mekanik **how to add bates**, dan mendemonstrasikan cara bersih untuk **add sequential page numbers** di seluruh dokumen. Potongan kode ini siap produksi, menangani artifact duplikat, dan bahkan menawarkan langkah flatten opsional untuk kepatuhan hukum.

Selanjutnya, Anda mungkin ingin mengeksplor:

- Menggabungkan beberapa PDF sambil mempertahankan kontinuitas Bates (gunakan `Document.AppendDocument` dan sesuaikan `StartNumber` secara dinamis).
- Menambahkan kode QR di samping nomor Bates untuk pelacakan otomatis.
- Mengintegrasikan logika ini ke dalam API ASP.NET Core sehingga layanan web Anda dapat menandai PDF sesuai permintaan.

Cobalah, ubah prefix, bereksperimen dengan font, dan biarkan otomatisasi mengurangi pekerjaan berat dalam alur peninjauan dokumen Anda. Selamat coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}