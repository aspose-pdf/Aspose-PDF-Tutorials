---
category: general
date: 2026-02-25
description: tutorial penomoran Bates – pelajari cara menambahkan nomor halaman PDF
  dan menerapkan penomoran Bates kustom menggunakan Aspose.Pdf dalam C#. Panduan langkah
  demi langkah dengan kode lengkap.
draft: false
keywords:
- bates numbering tutorial
- add page numbers pdf
- how to add bates
- add bates numbering
language: id
og_description: Tutorial penomoran Bates menunjukkan cara menambahkan nomor halaman
  PDF dan penomoran Bates khusus dalam C#. Kode lengkap, penjelasan, dan tips.
og_title: Tutorial Penomoran Bates – Tambahkan Nomor Bates ke PDF dengan C#
tags:
- PDF
- C#
- Aspose.Pdf
title: 'Tutorial Penomoran Bates: Tambahkan Nomor Bates ke PDF dengan C#'
url: /id/net/programming-with-stamps-and-watermarks/bates-numbering-tutorial-add-bates-numbers-to-pdfs-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# tutorial penomoran bates – Menambahkan Nomor Bates ke PDF dengan C#

Pernah bertanya-tanya bagaimana cara menambahkan nomor halaman pada PDF sekaligus menyisipkan nomor Bates bergaya legal? Anda tidak sendirian. Dalam **tutorial penomoran bates** ini kami akan membahas semua yang perlu Anda ketahui untuk menstempel setiap halaman PDF dengan prefiks khusus, nol di depan, dan posisi yang tepat—menggunakan Aspose.Pdf untuk .NET.

Kabar baiknya? Ini cukup sederhana setelah Anda memahami konsep dasarnya. Pada akhir panduan ini Anda akan memiliki program yang dapat dijalankan yang mengambil *input.pdf* dan menghasilkan *bates_out.pdf* dengan label “ABC‑01000” yang rapi pada setiap halaman. Mari kita mulai.

## Apa yang Anda Butuhkan

- **Aspose.Pdf untuk .NET** (versi 23.10 atau lebih baru). Perpustakaan ini bersifat komersial, tetapi percobaan gratis sudah cukup untuk belajar.
- .NET 6+ SDK (versi terbaru apa pun sudah cukup).
- Lingkungan pengembangan C# dasar—Visual Studio, VS Code, atau Rider.
- Sebuah PDF masukan untuk percobaan (dokumen multi‑halaman apa pun akan memperlihatkan efeknya).

Tidak ada paket NuGet tambahan selain Aspose.Pdf yang diperlukan, dan kode dapat dijalankan di Windows, Linux, atau macOS tanpa modifikasi.

## Langkah 1: Muat Dokumen PDF Sumber (tutorial penomoran bates – inisialisasi)

Pertama kita membuat objek `Document` yang mewakili PDF yang ingin kita ubah. Anggap saja ini sebagai kanvas kosong yang dapat Anda gambar.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Annotations;

// Load the source PDF – replace the path with your actual file location
Document pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");

// Quick sanity check – make sure the document actually has pages
if (pdfDocument.Pages.Count == 0)
{
    throw new InvalidOperationException("The PDF you provided contains no pages.");
}
```

**Mengapa ini penting:** Tanpa memuat file, tidak ada yang dapat diberi anotasi. Pemeriksaan keabsahan mencegah kegagalan diam-diam nanti ketika Anda mencoba menambahkan artefak ke koleksi halaman yang tidak ada.

## Langkah 2: Definisikan Artefak Penomoran Bates (cara menambahkan bates)

Sebuah *BatesNumberingArtifact* memberi tahu Aspose di mana dan bagaimana menggambar identifier. Anda dapat mengontrol prefiks, nomor mulai, padding nol, ukuran font, dan koordinat X/Y yang tepat.

```csharp
// Configure the Bates numbering artifact
BatesNumberingArtifact batesArtifact = new BatesNumberingArtifact
{
    Prefix = "ABC",          // Text that appears before the number
    Start = 1000,            // First number in the sequence
    LeadingZeros = 5,        // Pad the number with zeros (e.g., 01000)
    FontSize = 9,            // Small enough to sit in the margin
    Position = new Position   // Position measured from the lower‑left corner
    {
        X = 50,               // Horizontal offset (points)
        Y = 30                // Vertical offset (points)
    }
};
```

**Mengapa ini penting:** Properti `LeadingZeros` memastikan setiap label memiliki panjang yang sama, yang sangat penting untuk dokumen legal di mana perataan penting. Sesuaikan `X` dan `Y` untuk memindahkan stempel ke kanan‑atas, kiri‑bawah, atau ke posisi mana pun yang dibutuhkan alur kerja Anda.

## Langkah 3: Lampirkan Artefak ke Setiap Halaman (menambahkan nomor halaman pdf)

Sekarang kita melakukan iterasi pada setiap halaman dan melampirkan artefak yang sama. Di sinilah kebutuhan *menambahkan nomor halaman pdf* terpenuhi—setiap halaman mendapatkan label berurutan secara otomatis.

```csharp
// Iterate over each page and add the Bates artifact
foreach (Page page in pdfDocument.Pages)
{
    // The artifact is added to the page's Artifacts collection.
    // Aspose will handle the incrementing of the number for us.
    page.Artifacts.Add(batesArtifact);
}
```

**Mengapa ini penting:** Dengan menambahkan artefak ke koleksi `Artifacts` alih‑alih menggambar teks secara manual, kita membiarkan Aspose mengelola logika penomoran, nol di depan, dan rendering. Ini mengurangi bug dan membuat kode tetap ringkas.

## Langkah 4: Simpan PDF yang Telah Dimodifikasi (menambahkan penomoran bates)

Akhirnya, kita menyimpan perubahan ke file baru. Kebiasaan menulis ke nama file yang berbeda membantu menjaga file asli tetap tidak tersentuh.

```csharp
// Save the PDF with Bates numbers applied
pdfDocument.Save("YOUR_DIRECTORY/bates_out.pdf");

// Optional: let the user know we succeeded
Console.WriteLine("Bates numbering applied successfully! Output saved to bates_out.pdf");
```

**Mengapa ini penting:** Metode `Save` menulis seluruh PDF, menyisipkan artefak sebagai bagian dari aliran konten halaman. File yang dihasilkan dapat dibuka di penampil PDF apa pun dan akan menampilkan nomor Bates persis seperti yang ditentukan.

## Contoh Lengkap yang Berfungsi (Semua Langkah Digabung)

Berikut adalah program lengkap yang siap dijalankan. Salin‑tempel ke proyek aplikasi konsol, ganti jalur placeholder, dan tekan **F5**.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the source PDF
            Document pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");
            if (pdfDocument.Pages.Count == 0)
                throw new InvalidOperationException("The PDF you provided contains no pages.");

            // 2️⃣ Configure the Bates numbering artifact
            BatesNumberingArtifact batesArtifact = new BatesNumberingArtifact
            {
                Prefix = "ABC",
                Start = 1000,
                LeadingZeros = 5,
                FontSize = 9,
                Position = new Position { X = 50, Y = 30 }
            };

            // 3️⃣ Attach the artifact to every page
            foreach (Page page in pdfDocument.Pages)
            {
                page.Artifacts.Add(batesArtifact);
            }

            // 4️⃣ Save the modified PDF
            pdfDocument.Save("YOUR_DIRECTORY/bates_out.pdf");
            Console.WriteLine("Bates numbering applied successfully! Output saved to bates_out.pdf");
        }
    }
}
```

### Hasil yang Diharapkan

Buka *bates_out.pdf* di Adobe Reader, Foxit, atau penampil apa pun. Anda akan melihat label seperti **ABC‑01000** pada halaman pertama, **ABC‑01001** pada halaman kedua, dan seterusnya, diposisikan 50 pt dari tepi kiri dan 30 pt dari tepi bawah. Angka-angka tersebut diratakan kanan karena adanya nol di depan, memberikan dokumen tampilan yang bersih dan profesional.

## Variasi Umum & Kasus Tepi

| Skenario | Cara Menyesuaikan |
|----------|-------------------|
| **Prefiks berbeda** | Ubah `Prefix = "XYZ"` pada definisi artefak. |
| **Mulai dari nomor khusus** | Setel `Start = 5000` (atau angka berapa pun). |
| **Tempatkan nomor di pojok kanan‑atas** | Gunakan `Position = new Position { X = pdfDocument.PageInfo.Width - 50, Y = pdfDocument.PageInfo.Height - 30 }`. |
| **Ubah ukuran font untuk dokumen besar** | Modifikasi `FontSize = 12` (atau ukuran berapa pun). |
| **Tambahkan persegi panjang latar belakang** | Buat `RectangleArtifact` dan tambahkan sebelum `BatesNumberingArtifact`. |
| **Lewati halaman tertentu** | Di dalam loop `foreach`, tambahkan `if (page.Number % 2 == 0) continue;` untuk melewatkan halaman genap. |

**Tips pro:** Selalu uji dulu dengan PDF yang pendek. Lebih cepat memverifikasi posisi sebelum menjalankan skrip pada file kasus 200‑halaman.

## Pertanyaan yang Sering Diajukan

- **Apakah ini bekerja dengan PDF yang terenkripsi?**  
  Aspose.Pdf dapat membuka file yang dilindungi kata sandi jika Anda menyediakan kata sandi melalui `Document(string, string)`. Artefak Bates tetap akan diterapkan setelah dekripsi.

- **Bisakah saya menambahkan nomor Bates sekaligus nomor halaman biasa?**  
  Ya. Tambahkan `PageNumberArtifact` bersamaan dengan `BatesNumberingArtifact`. Setiap artefak mempertahankan penghitungnya masing‑masing.

- **Bagaimana jika PDF saya memiliki ukuran halaman yang berbeda?**  
  Nilai `Position` bersifat absolut dalam poin. Untuk dokumen dengan ukuran campuran, hitung posisi per halaman di dalam loop menggunakan `page.PageInfo.Width` dan `page.PageInfo.Height`.

## Langkah Selanjutnya & Topik Terkait

Setelah Anda menguasai **tutorial penomoran bates**, Anda mungkin ingin menjelajahi:

- **Menambahkan watermark** – pendekatan artefak serupa dengan `TextArtifact`.
- **Menggabungkan beberapa PDF** – gunakan `Document.AppendDocument`.
- **Mengekstrak teks untuk pengindeksan pencarian** – kelas `TextAbsorber`.
- **Mengotomatiskan pemrosesan batch** – iterasi folder PDF dan terapkan artefak yang sama.

Semua topik ini dibangun di atas konsep yang baru saja Anda pelajari, sehingga Anda berada pada posisi yang tepat untuk memperluas toolkit otomasi PDF Anda.

---

*Selamat coding! Jika Anda menemukan kendala atau memiliki ide untuk kustomisasi lebih lanjut, jangan ragu meninggalkan komentar di bawah. Dunia manipulasi PDF sangat luas, tetapi dengan **tutorial penomoran bates** yang solid di bawah sabuk Anda, Anda sudah selangkah lebih maju.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}