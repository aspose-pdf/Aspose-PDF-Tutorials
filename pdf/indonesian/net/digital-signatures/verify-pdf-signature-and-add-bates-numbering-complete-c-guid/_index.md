---
category: general
date: 2026-04-02
description: Verifikasi tanda tangan PDF dengan cepat dan pelajari cara menambahkan
  penomoran Bates menggunakan Aspose.Pdf. Termasuk kode langkah demi langkah dan tips.
draft: false
keywords:
- verify pdf signature
- add bates numbering
- how to verify signature
- how to add bates
- check pdf signature
language: id
og_description: Verifikasi tanda tangan PDF dengan cepat dan pelajari cara menambahkan
  penomoran Bates menggunakan Aspose.Pdf. Ikuti contoh lengkapnya dan hindari jebakan
  umum.
og_title: Verifikasi Tanda Tangan PDF dan Tambahkan Penomoran Bates – Panduan Lengkap
  C#
tags:
- Aspose.Pdf
- C#
- Digital Signature
- Document Automation
title: Verifikasi Tanda Tangan PDF dan Tambahkan Penomoran Bates – Panduan C# Lengkap
url: /id/net/digital-signatures/verify-pdf-signature-and-add-bates-numbering-complete-c-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Verifikasi Tanda Tangan PDF dan Tambahkan Penomoran Bates – Panduan Lengkap C#

Pernah perlu **verify PDF signature** sebelum Anda mengirimkan kontrak, tetapi tidak yakin panggilan API mana yang harus digunakan? Anda tidak sendirian—banyak pengembang mengalami hal yang sama saat menangani PDF yang memiliki ikatan hukum. Dalam tutorial ini kami akan menjelaskan secara tepat cara **verify PDF signature** dengan Aspose.Pdf dan kemudian menunjukkan **how to add bates numbering** sehingga file Anda siap audit.  

Kami juga akan membahas **how to verify signature** secara programatis, mencakup **how to add bates** dalam satu proses, dan menjelaskan hasil **check pdf signature** sehingga Anda dapat mempercayai outputnya. Pada akhir tutorial, Anda akan memiliki aplikasi konsol C# yang dapat dijalankan yang melakukan kedua tugas—tanpa misteri, hanya kode yang jelas.

---

## Apa yang Anda Butuhkan

- **.NET 6.0** atau yang lebih baru (contoh ini juga bekerja dengan .NET Framework 4.7+)
- **Aspose.Pdf for .NET** paket NuGet (versi 23.11 atau lebih baru)
- File PDF yang ditandatangani (`signed.pdf`) yang ingin Anda validasi
- File PDF biasa (`input.pdf`) yang akan menerima nomor Bates

Jika Anda sudah memiliki semua itu, Anda siap melanjutkan. Tidak perlu SDK tambahan, tidak ada file konfigurasi tersembunyi.

## Langkah 1: Siapkan Proyek

Mulailah dengan membuat proyek konsol:

```bash
dotnet new console -n PdfSignatureAndBatesDemo
cd PdfSignatureAndBatesDemo
dotnet add package Aspose.Pdf
```

Buka `Program.cs` dan hapus kode default. Kami akan membangun semuanya dari awal sehingga Anda dapat menyalin‑tempel versi final nanti.

## Langkah 2: Verifikasi Tanda Tangan PDF

### Mengapa verifikasi penting

Tanda tangan digital dapat **compromised** jika sertifikat yang mendasarinya dicabut atau dokumen telah diubah setelah penandatanganan. Aspose.Pdf menyediakan metode `IsSignatureCompromised` yang mengembalikan nilai boolean—sederhana, namun cukup kuat untuk sebagian besar alur audit.

### Potongan Kode

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Facades;

namespace PdfSignatureAndBatesDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // ---------- Verify PDF Signature ----------
            string signedPdfPath = @"YOUR_DIRECTORY\signed.pdf";

            // Load the signed document inside a using block to ensure disposal
            using (Document signedDoc = new Document(signedPdfPath))
            using (PdfFileSignature pdfSignature = new PdfFileSignature(signedDoc))
            {
                // The name "Signature1" is the default for the first signature.
                // Change it if your PDF uses a custom field name.
                bool isCompromised = pdfSignature.IsSignatureCompromised("Signature1");

                Console.WriteLine($"Signature compromised: {isCompromised}");
                // Expected output: "Signature compromised: False" if everything is fine.
            }

            // The rest of the program (Bates numbering) continues below...
```

**Explanation**

- `Document` memuat PDF ke memori.  
- `PdfFileSignature` membungkus dokumen dan menyediakan metode terkait tanda tangan.  
- `IsSignatureCompromised("Signature1")` memeriksa integritas tanda tangan yang bernama *Signature1*.  
- Hasil boolean memberi tahu Anda apakah tanda tangan masih dapat dipercaya.

> **Pro tip:** Jika Anda tidak yakin dengan nama bidang tanda tangan, panggil `pdfSignature.GetSignatureNames()` terlebih dahulu; itu mengembalikan daftar semua pengidentifikasi tanda tangan.

## Langkah 3: Siapkan Opsi Penomoran Bates

### Apa itu penomoran Bates?

Nomor Bates adalah pengidentifikasi berurutan yang dicetak pada setiap halaman dokumen hukum atau forensik. Mereka memudahkan referensi halaman selama proses penemuan atau audit. `BatesNumberingOptions` milik Aspose.Pdf memungkinkan Anda menyesuaikan awalan, nomor mulai, jumlah digit, perataan, dan margin—semua dalam satu objek.

### Lanjutan Kode

```csharp
            // ---------- Configure Bates Numbering ----------
            string sourcePdfPath = @"YOUR_DIRECTORY\input.pdf";
            using (Document pdfWithBates = new Document(sourcePdfPath))
            {
                // Set up the numbering style
                BatesNumberingOptions batesOptions = new BatesNumberingOptions
                {
                    Prefix = "INV-",          // Anything before the numeric part
                    StartNumber = 1000,      // First number to use
                    NumberOfDigits = 5,      // Pads numbers with leading zeros (e.g., 01000)
                    Alignment = HorizontalAlignment.Right,
                    BottomMargin = 20        // Distance from the bottom edge (points)
                };

                // Apply the numbering to every page in the document
                pdfWithBates.AddBatesNumbering(batesOptions);

                // Save the newly numbered PDF
                string outputPdfPath = @"YOUR_DIRECTORY\BatesNumbered.pdf";
                pdfWithBates.Save(outputPdfPath);

                Console.WriteLine($"Bates numbering added. File saved to: {outputPdfPath}");
                // Expected output: "Bates numbering added. File saved to: ...\BatesNumbered.pdf"
            }
        }
    }
}
```

**Explanation**

- `BatesNumberingOptions` memusatkan semua pilihan format.  
- `AddBatesNumbering` mengiterasi setiap halaman secara otomatis—tidak perlu loop manual.  
- `Prefix` (`INV-`) dan `StartNumber` (1000) menghasilkan label seperti `INV-01000`, `INV-01001`, dll.  
- Sesuaikan `BottomMargin` jika Anda membutuhkan nomor lebih tinggi atau lebih rendah pada halaman.

## Langkah 4: Jalankan Contoh Lengkap

Simpan file, lalu jalankan:

```bash
dotnet run
```

Anda akan melihat dua baris konsol:

```
Signature compromised: False
Bates numbering added. File saved to: YOUR_DIRECTORY\BatesNumbered.pdf
```

Jika baris pertama mencetak `True`, tanda tangan tersebut compromised—artinya dokumen mungkin telah diubah setelah penandatanganan atau sertifikat tidak lagi valid. Dalam kasus ini, hentikan semua proses lanjutan.

## Langkah 5: Kasus Tepi Umum & Cara Menanganinya

| Situasi | Hal yang Perlu Diperhatikan | Perbaikan yang Disarankan |
|-----------|-------------------|---------------|
| **Multiple signatures** | `IsSignatureCompromised` hanya memeriksa satu bidang pada satu waktu. | Lakukan loop melalui `pdfSignature.GetSignatureNames()` dan verifikasi masing‑masing. |
| **Custom signature field name** | Menggunakan `"Signature1"` dapat menghasilkan pengecualian jika namanya berbeda. | Ambil daftar nama terlebih dahulu, atau berikan nama tepat yang Anda lihat di Acrobat. |
| **Large PDFs (100+ pages)** | Menambahkan nomor Bates dapat memakan banyak memori. | Gunakan `Document.Save` dengan `SaveOptions` yang mengaktifkan streaming (`PdfSaveOptions { Compress = true }`). |
| **Non‑Latin characters in prefix** | Beberapa font tidak mendukung Unicode secara default. | Setel `pdfWithBates.Font` ke font yang kompatibel Unicode seperti `Arial Unicode MS`. |
| **Need to place numbers on the left** | Perataan dikodekan secara tetap ke `Right`. | Ubah `Alignment = HorizontalAlignment.Left` di `BatesNumberingOptions`. |

## Langkah 6: Verifikasi Hasil Secara Manual (Opsional)

Buka `BatesNumbered.pdf` di penampil PDF apa pun:

1. Lihat setiap halaman—setiap halaman harus menampilkan label seperti **INV‑01000** di pojok kanan‑bawah.  
2. Gunakan **Signature Panel** di Acrobat untuk mengklik ganda tanda tangan dan memastikan statusnya cocok dengan output konsol.

Jika semuanya cocok, Anda telah berhasil memeriksa status **check pdf signature** dan menerapkan **add bates numbering** sekaligus.

## Pertanyaan yang Sering Diajukan

**Q: Bisakah saya memverifikasi tanda tangan tanpa memuat seluruh dokumen?**  
A: Aspose.Pdf melakukan streaming file di balik layar, tetapi Anda tetap memerlukan instance `Document`. Untuk file yang sangat besar, pertimbangkan menggunakan `PdfFileSignature` secara langsung dengan aliran file untuk mengurangi jejak memori.

**Q: Apakah saya memerlukan lisensi untuk Aspose.Pdf?**  
A: Evaluasi gratis dapat digunakan, tetapi akan menambahkan watermark. Untuk produksi Anda memerlukan lisensi yang tepat; jika tidak, PDF output akan menampilkan banner Aspose.

**Q: Bagaimana jika saya hanya perlu menambahkan nomor Bates pada sebagian halaman?**  
A: Gunakan `pdfWithBates.AddBatesNumbering(batesOptions, new[] { 1, 3, 5 })` dimana array tersebut berisi nomor halaman yang ingin Anda beri nomor.

## Kesimpulan

Anda sekarang tahu **how to verify PDF signature** dengan Aspose.Pdf, memahami arti hasil boolean, dan dapat dengan yakin **add bates numbering** ke PDF apa pun yang Anda kontrol. Contoh lengkap yang dapat dijalankan menggabungkan kedua tugas, memberikan Anda satu alat konsol yang memeriksa keaslian dokumen dan menandainya dengan identifier siap audit.  

Selanjutnya, Anda dapat menjelajahi **how to verify signature** terhadap penyimpanan root yang tepercaya, atau bereksperimen dengan gaya **add bates numbering** khusus seperti stempel diagonal atau awalan per‑section. Kedua topik tersebut membangun di atas fondasi yang baru saja Anda kuasai, dan akan membuat pipeline pemrosesan dokumen Anda lebih kuat.  

Selamat coding, dan ingat—memeriksa tanda tangan dan menomori halaman sangat mudah setelah Anda memiliki kode yang tepat! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}