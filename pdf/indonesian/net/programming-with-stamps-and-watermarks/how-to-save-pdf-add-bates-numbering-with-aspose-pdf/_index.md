---
category: general
date: 2026-02-23
description: Cara menyimpan file PDF sambil menambahkan penomoran Bates dan artefak
  menggunakan Aspose.Pdf dalam C#. Panduan langkah demi langkah untuk pengembang.
draft: false
keywords:
- how to save pdf
- how to add bates
- how to add artifact
- create pdf document
- add bates numbering
language: id
og_description: Cara menyimpan file PDF sambil menambahkan penomoran Bates dan artefak
  menggunakan Aspose.Pdf di C#. Pelajari solusi lengkap dalam hitungan menit.
og_title: Cara Menyimpan PDF — Tambahkan Penomoran Bates dengan Aspose.Pdf
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Cara Menyimpan PDF — Tambahkan Penomoran Bates dengan Aspose.Pdf
url: /id/net/programming-with-stamps-and-watermarks/how-to-save-pdf-add-bates-numbering-with-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Menyimpan PDF — Menambahkan Penomoran Bates dengan Aspose.Pdf

Pernah bertanya-tanya **how to save PDF** file setelah Anda menandainya dengan nomor Bates? Anda bukan satu-satunya. Di firma hukum, pengadilan, dan bahkan tim kepatuhan internal, kebutuhan untuk menyematkan pengidentifikasi unik pada setiap halaman menjadi masalah harian. Kabar baik? Dengan Aspose.Pdf untuk .NET Anda dapat melakukannya dalam beberapa baris kode, dan Anda akan mendapatkan PDF yang tersimpan dengan sempurna yang membawa penomoran yang Anda butuhkan.

Dalam tutorial ini kami akan membahas seluruh proses: memuat PDF yang ada, menambahkan *artifact* nomor Bates, dan akhirnya **how to save PDF** ke lokasi baru. Sepanjang jalan kami juga akan menyentuh **how to add bates**, **how to add artifact**, dan bahkan membahas topik lebih luas tentang **create PDF document** secara programatis. Pada akhir Anda akan memiliki potongan kode yang dapat digunakan kembali dan dapat dimasukkan ke proyek C# mana pun.

## Prasyarat

- .NET 6.0 atau lebih baru (kode juga berfungsi dengan .NET Framework 4.6+)
- Paket NuGet Aspose.Pdf untuk .NET (`Install-Package Aspose.Pdf`)
- Contoh PDF (`input.pdf`) yang ditempatkan di folder yang dapat Anda baca/tulis
- Familiaritas dasar dengan sintaks C#—tidak memerlukan pengetahuan mendalam tentang PDF

> **Pro tip:** Jika Anda menggunakan Visual Studio, aktifkan *nullable reference types* untuk pengalaman kompilasi yang lebih bersih.

---

## Cara Menyimpan PDF dengan Penomoran Bates

Inti solusi terdiri dari tiga langkah sederhana. Setiap langkah dibungkus dalam heading H2 masing‑masing sehingga Anda dapat langsung melompat ke bagian yang Anda butuhkan.

### Langkah 1 – Memuat Dokumen PDF Sumber

Pertama, kita perlu memuat file ke memori. Kelas `Document` milik Aspose.Pdf mewakili seluruh PDF, dan Anda dapat menginstansiasinya langsung dari jalur file.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Artifacts;
using Aspose.Pdf.Text;

namespace BatesNumberDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 👉 Step 1: Load the source PDF document
            string inputPdfPath = @"C:\MyDocs\input.pdf";

            // The Document constructor throws if the file is missing, so wrap it in a try/catch if you need resilience.
            using (var pdfDocument = new Document(inputPdfPath))
            {
                // The rest of the workflow continues inside this using block.
```

**Why this matters:** Memuat file adalah satu‑satunya titik di mana I/O dapat gagal. Dengan mempertahankan pernyataan `using` kita memastikan handle file dilepaskan segera—penting ketika Anda kemudian **how to save pdf** kembali ke disk.

### Langkah 2 – Cara Menambahkan Artifact Penomoran Bates

Nomor Bates biasanya ditempatkan di header atau footer setiap halaman. Aspose.Pdf menyediakan kelas `BatesNumberArtifact`, yang secara otomatis meningkatkan nomor untuk setiap halaman yang Anda tambahkan.

```csharp
                // 👉 Step 2: Add a Bates number artifact to the first page (you could loop for all pages)
                var batesArtifact = new BatesNumberArtifact
                {
                    // The Text property can contain a format string. "{0}" will be replaced by the page number.
                    Text = "Case-2026-{0}",
                    Position = new Position(50, 50), // X=50pt, Y=50pt from the bottom‑left corner
                    Font = FontRepository.FindFont("Helvetica"),
                    FontSize = 12,
                    // Optional: set color, opacity, etc.
                };

                // Attach the artifact to the first page; Aspose will replicate it on subsequent pages automatically.
                pdfDocument.Pages[1].Artifacts.Add(batesArtifact);
```

**How to add bates** di seluruh dokumen? Jika Anda menginginkan artifact pada *setiap* halaman, cukup tambahkan ke halaman pertama seperti yang ditunjukkan—Aspose menangani propagasinya. Untuk kontrol yang lebih detail Anda dapat mengiterasi `pdfDocument.Pages` dan menambahkan `TextFragment` khusus, tetapi artifact bawaan adalah yang paling ringkas.

### Langkah 3 – Cara Menyimpan PDF ke Lokasi Baru

Sekarang PDF sudah membawa nomor Bates, saatnya menuliskannya. Di sinilah kata kunci utama bersinar lagi: **how to save pdf** setelah modifikasi.

```csharp
                // 👉 Step 3: Save the updated PDF to the desired location
                string outputPdfPath = @"C:\MyDocs\output.pdf";

                // Overwrite if the file already exists; you can also check File.Exists first.
                pdfDocument.Save(outputPdfPath);
                Console.WriteLine($"PDF saved successfully to {outputPdfPath}");
            } // using block disposes the Document
        }
    }
}
```

Ketika metode `Save` selesai, file di disk berisi nomor Bates pada setiap halaman, dan Anda baru saja mempelajari **how to save pdf** dengan artifact yang terlampir.

---

## Cara Menambahkan Artifact ke PDF (Selain Bates)

Terkadang Anda membutuhkan watermark umum, logo, atau catatan khusus alih-alih nomor Bates. Koleksi `Artifacts` yang sama bekerja untuk elemen visual apa pun.

```csharp
// Example: Adding a simple text watermark artifact
var watermark = new TextArtifact
{
    Text = "CONFIDENTIAL",
    Position = new Position(200, 400),
    Font = FontRepository.FindFont("Arial"),
    FontSize = 36,
    Color = Color.FromRgb(255, 0, 0),
    Opacity = 0.3
};
pdfDocument.Pages[1].Artifacts.Add(watermark);
```

**Why use an artifact?** Artifacts adalah objek *non‑content*, yang berarti mereka tidak mengganggu ekstraksi teks atau fitur aksesibilitas PDF. Itulah mengapa mereka menjadi cara yang disukai untuk menyematkan nomor Bates, watermark, atau overlay apa pun yang harus tetap tidak terlihat oleh mesin pencari.

---

## Membuat Dokumen PDF dari Awal (Jika Anda Tidak Memiliki Input)

Langkah‑langkah sebelumnya mengasumsikan adanya file yang ada, tetapi terkadang Anda perlu **create PDF document** dari awal sebelum dapat **add bates numbering**. Berikut contoh minimalis:

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Create a fresh PDF document
var newDoc = new Document();
Page page = newDoc.Pages.Add();

// Add a simple paragraph
var paragraph = new TextFragment("Hello, this is a newly created PDF.");
page.Paragraphs.Add(paragraph);

// Save it
newDoc.Save(@"C:\MyDocs\newfile.pdf");
```

Dari sini Anda dapat menggunakan kembali potongan *how to add bates* dan rutinitas *how to save pdf* untuk mengubah kanvas kosong menjadi dokumen hukum yang sepenuhnya berpenomoran.

---

## Kasus Pinggir Umum & Tips

| Situasi | Hal yang Perlu Diperhatikan | Perbaikan yang Disarankan |
|-----------|-------------------|---------------|
| **Input PDF has no pages** | `pdfDocument.Pages[1]` melempar pengecualian out‑of‑range. | Verifikasi `pdfDocument.Pages.Count > 0` sebelum menambahkan artifacts, atau buat halaman baru terlebih dahulu. |
| **Multiple pages need different positions** | Satu artifact menerapkan koordinat yang sama ke setiap halaman. | Loop melalui `pdfDocument.Pages` dan set `Artifacts.Add` per halaman dengan `Position` khusus. |
| **Large PDFs (hundreds of MB)** | Tekanan memori saat dokumen tetap berada di RAM. | Gunakan `PdfFileEditor` untuk modifikasi in‑place, atau proses halaman secara batch. |
| **Custom Bates format** | Menginginkan prefix, suffix, atau nomor berisi nol di depan. | Set `Text = "DOC-{0:0000}"` – placeholder `{0}` menghormati string format .NET. |
| **Saving to a read‑only folder** | `Save` melempar `UnauthorizedAccessException`. | Pastikan direktori target memiliki izin menulis, atau minta pengguna memilih path alternatif. |

---

## Hasil yang Diharapkan

Setelah menjalankan program lengkap:

1. `output.pdf` muncul di `C:\MyDocs\`.
2. Membukanya di penampil PDF apa pun menampilkan teks **“Case-2026-1”**, **“Case-2026-2”**, dll., yang diposisikan 50 pt dari tepi kiri dan bawah pada setiap halaman.
3. Jika Anda menambahkan artifact watermark opsional, kata **“CONFIDENTIAL”** muncul semi‑transparent di atas konten.

Anda dapat memverifikasi nomor Bates dengan memilih teks (mereka dapat dipilih karena merupakan artifacts) atau dengan menggunakan alat inspeksi PDF.

---

## Ringkasan – Cara Menyimpan PDF dengan Penomoran Bates Sekaligus

- **Load** file sumber dengan `new Document(path)`.
- **Add** `BatesNumberArtifact` (atau artifact lain) ke halaman pertama.
- **Save** dokumen yang dimodifikasi menggunakan `pdfDocument.Save(destinationPath)`.

Itulah seluruh jawaban untuk **how to save pdf** sambil menyematkan pengidentifikasi unik. Tanpa skrip eksternal, tanpa penyuntingan halaman manual—hanya metode C# yang bersih dan dapat digunakan kembali.

---

## Langkah Selanjutnya & Topik Terkait

- **Add Bates numbering to every page manually** – iterasi `pdfDocument.Pages` untuk kustomisasi per‑halaman.
- **How to add artifact** untuk gambar: ganti `TextArtifact` dengan `ImageArtifact`.
- **Create PDF document** dengan tabel, diagram, atau bidang formulir menggunakan API kaya Aspose.Pdf.
- **Automate batch processing** – baca folder PDF, terapkan nomor Bates yang sama, dan simpan secara massal.

Silakan bereksperimen dengan berbagai font, warna, dan posisi. Library Aspose.Pdf sangat fleksibel, dan setelah Anda menguasai **how to add bates** dan **how to add artifact**, tidak ada batasnya.

### Kode Referensi Cepat (Semua Langkah dalam Satu Blok)

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Artifacts;
using Aspose.Pdf.Text;

class BatesDemo
{
    static void Main()
    {
        string inputPath = @"C:\MyDocs\input.pdf";
        string outputPath = @"C:\MyDocs\output.pdf";

        using (var pdf = new Document(inputPath))
        {
            var bates = new BatesNumberArtifact
            {
                Text = "Case-2026-{0}",
                Position = new Position(50, 50),
                Font = FontRepository.FindFont("Helvetica"),
                FontSize = 12
            };
            pdf.Pages[1].Artifacts.Add(bates);
            pdf.Save(outputPath);
        }

        Console.WriteLine($"Saved PDF with Bates number to {outputPath}");
    }
}
```

Jalankan potongan ini, dan Anda akan memiliki fondasi yang kuat untuk proyek otomatisasi PDF di masa depan.

---

*Happy coding! If

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}