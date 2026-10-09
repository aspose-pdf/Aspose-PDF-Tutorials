---
category: general
date: 2026-06-21
description: Tambahkan penomoran bates pada PDF dan pelajari cara menambahkan nomor
  bates, mengonversi PDF ke PDF/X-4, mengonversi PDF ke PDF/A-4, serta menandatangani
  PDF secara digital dengan C# dalam satu panduan.
draft: false
keywords:
- add bates numbering pdf
- how to add bates numbers
- digitally sign pdf c#
- convert pdf to pdf/x-4
- convert pdf to pdfa-4
language: id
og_description: Tambahkan penomoran Bates pada PDF, lihat cara menambahkan nomor Bates,
  konversi PDF ke PDF/X-4, konversi PDF ke PDFA-4, dan tanda tangan digital PDF dengan
  C# menggunakan Aspose.Pdf.
og_title: Menambahkan Penomoran Bates pada PDF – Tutorial C# Langkah demi Langkah
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Add bates numbering pdf and learn how to add bates numbers, convert
    pdf to pdf/x-4, convert pdf to pdfa-4, and digitally sign pdf c# in a single walkthrough.
  headline: Add Bates Numbering PDF – Complete C# Guide with Signing & Conversion
  type: TechArticle
- questions:
  - answer: Yes. Use `BatesNumberingOptions` properties such as `Location` and `FontSize`
      to fine‑tune placement.
    question: Can I change the position of the Bates numbers?
  - answer: Switch `PdfFormat.PDF_X_4` to `PdfFormat.PDFA_4` in the conversion options.
      That satisfies the **convert pdf to pdfa-4** requirement.
    question: What if I need PDF/A‑4 instead of PDF/X‑4?
  - answer: Absolutely. Replace `DigestHashAlgorithm.Sha384` with `DigestHashAlgorithm.Sha256`
      (or any supported algorithm).
    question: My certificate uses a different hash algorithm—can I use SHA‑256?
  - answer: 'Not strictly. In this flow we save after conversion and after Bates numbering
      to give you intermediate files. You could defer saving until the end if you
      prefer a single write operation. ## Wrap‑Up We’ve just demonstrated a practical,
      end‑to‑end solution that **add bates numbering pdf**, explains **'
    question: Do I need to call `document.Save` after each step?
  type: FAQPage
tags:
- Aspose.Pdf
- C#
- PDF processing
- Bates numbering
title: Menambahkan Penomoran Bates pada PDF – Panduan Lengkap C# dengan Penandatanganan
  & Konversi
url: /id/net/programming-with-security-and-signatures/add-bates-numbering-pdf-complete-c-guide-with-signing-conver/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tambahkan Penomoran Bates pada PDF – Panduan Lengkap C# dengan Penandatanganan & Konversi

Pernah bertanya-tanya **add bates numbering pdf** tanpa membuat rambut rontok? Anda tidak sendirian. Tim hukum, auditor, dan siapa saja yang membutuhkan dokumen yang dapat dilacak terus-menerus menanyakan *bagaimana cara menambahkan nomor bates* ke PDF, dan kemudian mereka juga membutuhkan file yang memenuhi standar PDF/X‑4 atau PDF/A‑4 serta ditandatangani secara digital.  

Dalam tutorial ini kami akan membahas semuanya—menggunakan Aspose.Pdf untuk .NET kami akan **add bates numbering pdf**, menunjukkan **how to add bates numbers**, **convert pdf to pdf/x-4**, **convert pdf to pdfa-4**, dan akhirnya **digitally sign pdf c#**. Pada akhir tutorial Anda akan memiliki program siap‑jalankan yang menghasilkan tiga PDF yang halus: versi PDF/X‑4, versi dengan penomoran Bates, dan versi yang ditandatangani secara digital.

![add bates numbering pdf example](image-placeholder.png "Screenshot showing add bates numbering pdf in action")

## Apa yang Anda Butuhkan

- **.NET 6+** (atau .NET Framework 4.6+). Aspose.Pdf mendukung keduanya.  
- **Lisensi Aspose.Pdf untuk .NET yang valid** (atau Anda dapat menggunakan versi evaluasi, tetapi watermark akan muncul).  
- **File sertifikat PKCS#7** (`.pfx`) beserta kata sandinya untuk penandatanganan.  
- **PDF contoh** yang ingin Anda ubah (letakkan di folder yang Anda kontrol).  
- Visual Studio, Rider, atau IDE C# apa pun yang Anda suka.

Itu saja—tidak ada paket NuGet tambahan selain `Aspose.Pdf`. Jika Anda belum menambahkan pustaka tersebut, jalankan:

```bash
dotnet add package Aspose.Pdf
```

Sekarang mari masuk ke kode.

## Langkah 1: Muat Dokumen PDF Sumber

Pertama, kita perlu memuat file asli ke memori. Ini adalah dasar untuk setiap operasi selanjutnya.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Forms;
using Aspose.Pdf.Security;
using Aspose.Pdf.Saving;

// Load the source PDF – adjust the path to your environment
var document = new Document("YOUR_DIRECTORY/sample.pdf");
```

> **Mengapa ini penting:** Memuat PDF membuat objek `Document` yang mewakili seluruh file, memberi kita akses ke API konversi, bidang formulir, dan keamanan.

## Langkah 2: Konversi PDF ke PDF/X‑4 (Kepatuhan PDF/A‑4)

Jika alur kerja Anda menuntut kualitas arsip, PDF/X‑4 (sebuah subset dari PDF/A‑4) adalah pilihan yang tepat. Berikut cara **convert pdf to pdf/x-4** dengan Aspose.

```csharp
// Set conversion options – PDF/X‑4 is the target format
var conversionOptions = new PdfFormatConversionOptions(PdfFormat.PDF_X_4, ConvertErrorAction.Delete);

// Perform the conversion
document.Convert(conversionOptions);
```

> **Tip:** Flag `ConvertErrorAction.Delete` menghapus semua konten yang dapat melanggar kepatuhan, memastikan output PDF/X‑4 yang bersih.

## Langkah 3: Simpan Versi PDF/X‑4

Setelah dokumen mematuhi PDF/X‑4, kita simpan ke disk.

```csharp
document.Save("YOUR_DIRECTORY/sample_pdfx4.pdf");
```

Sekarang Anda memiliki file yang kompatibel dengan **convert pdf to pdfa-4** (PDF/X‑4 merupakan anggota keluarga PDF/A‑4). Silakan buka di Acrobat untuk memverifikasi lencana kepatuhan.

## Langkah 4: Tambahkan Penomoran Bates – Inti dari “Add Bates Numbering PDF”

Penomoran Bates adalah pengidentifikasi berurutan yang ditempatkan pada setiap halaman. Ini adalah jawaban tepat untuk *how to add bates numbers* secara programatik.

```csharp
// Configure Bates numbering options
var batesOptions = new BatesNumberingOptions
{
    Prefix = "CASE-",   // Optional prefix
    Start = 5000        // Starting number
};

// Apply Bates numbering to the document
document.AddBatesNumbering(batesOptions);
```

> **Mengapa ini berhasil:** `AddBatesNumbering` melintasi setiap halaman dan menempelkan nomor di lokasi default (kanan‑bawah). Anda dapat menyesuaikan posisi nanti melalui `BatesNumberingOptions` bila diperlukan.

## Langkah 5: Simpan PDF dengan Penomoran Bates

Setelah kami **add bates numbering pdf**, kami memerlukan file terpisah yang mempertahankan nomor‑nomor tersebut.

```csharp
document.Save("YOUR_DIRECTORY/sample_bates.pdf");
```

Buka file; Anda akan melihat “CASE‑5000”, “CASE‑5001”, dan seterusnya di bagian bawah setiap halaman.

## Langkah 6: Tanda Tangani PDF Secara Digital – “Digitally Sign PDF C#” dalam Aksi

Tanda tangan digital menjamin keaslian dan integritas. Di bawah ini kami akan **digitally sign pdf c#** menggunakan hash SHA‑384.

```csharp
// Prepare the signature handler
var signature = new PdfFileSignature(document);

// Load the PKCS#7 certificate (adjust password)
var pkcs7 = new PKCS7Detached(
    "YOUR_DIRECTORY/mycert.pfx", // Path to .pfx
    "pwd",                       // Certificate password
    DigestHashAlgorithm.Sha384   // Strong hashing algorithm
);

// Sign page 1, place signature rectangle at (100,100)-(200,150)
signature.Sign(
    pageNumber: 1,
    signatureAppearance: true,
    rectangle: new Rectangle(100, 100, 200, 150),
    pkcs7: pkcs7
);
```

> **Pro tip:** `Rectangle` menentukan di mana tanda tangan visual muncul. Jika Anda tidak memerlukan petunjuk visual, setel `signatureAppearance` ke `false`.

## Langkah 7: Simpan PDF yang Ditandatangani Secara Digital

Akhirnya, tulis dokumen yang ditandatangani ke disk.

```csharp
signature.Save("YOUR_DIRECTORY/sample_signed.pdf");
```

Sekarang Anda memiliki file **digitally sign pdf c#** yang dapat divalidasi di pembaca PDF apa pun yang mendukung tanda tangan digital.

## Kode Sumber Lengkap – Solusi Satu‑Pintu

Berikut adalah program lengkap yang siap‑jalankan dan menggabungkan semua langkah. Salin‑tempel, sesuaikan jalur, dan tekan **F5**.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Forms;
using Aspose.Pdf.Security;
using Aspose.Pdf.Saving;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Load the source PDF document
        // -------------------------------------------------
        var document = new Document("YOUR_DIRECTORY/sample.pdf");

        // -------------------------------------------------
        // Step 2: Convert the document to PDF/X‑4 format
        // (PDF/A‑4 compliance)
        // -------------------------------------------------
        var conversionOptions = new PdfFormatConversionOptions(
            PdfFormat.PDF_X_4,
            ConvertErrorAction.Delete);
        document.Convert(conversionOptions);

        // -------------------------------------------------
        // Step 3: Save the PDF/X‑4 version
        // -------------------------------------------------
        document.Save("YOUR_DIRECTORY/sample_pdfx4.pdf");

        // -------------------------------------------------
        // Step 4: Add Bates numbering – how to add bates numbers
        // -------------------------------------------------
        var batesOptions = new BatesNumberingOptions
        {
            Prefix = "CASE-",
            Start = 5000
        };
        document.AddBatesNumbering(batesOptions);

        // -------------------------------------------------
        // Step 5: Save the Bates‑numbered PDF
        // -------------------------------------------------
        document.Save("YOUR_DIRECTORY/sample_bates.pdf");

        // -------------------------------------------------
        // Step 6: Sign the document using SHA‑384 hashing
        // -------------------------------------------------
        var signature = new PdfFileSignature(document);
        var pkcs7 = new PKCS7Detached(
            "YOUR_DIRECTORY/mycert.pfx",
            "pwd",
            DigestHashAlgorithm.Sha384);
        signature.Sign(
            pageNumber: 1,
            signatureAppearance: true,
            rectangle: new Rectangle(100, 100, 200, 150),
            pkcs7: pkcs7);

        // -------------------------------------------------
        // Step 7: Save the digitally signed PDF
        // -------------------------------------------------
        signature.Save("YOUR_DIRECTORY/sample_signed.pdf");
    }
}
```

### Output yang Diharapkan

| Berkas | Tujuan | Fitur Utama |
|--------|--------|-------------|
| `sample_pdfx4.pdf` | Versi PDF/X‑4 | Memenuhi kepatuhan PDF/A‑4 |
| `sample_bates.pdf` | PDF dengan nomor Bates | **add bates numbering pdf** diterapkan |
| `sample_signed.pdf` | PDF yang ditandatangani secara digital | **digitally sign pdf c#** dengan SHA‑384 |

Buka salah satu dari tiga file tersebut di Adobe Acrobat Reader; Anda akan melihat nomor Bates pada file kedua dan bidang tanda tangan pada file ketiga.

## Pertanyaan yang Sering Diajukan (FAQ)

**T: Bisakah saya mengubah posisi nomor Bates?**  
J: Ya. Gunakan properti `BatesNumberingOptions` seperti `Location` dan `FontSize` untuk menyesuaikan penempatan.

**T: Bagaimana jika saya membutuhkan PDF/A‑4 bukan PDF/X‑4?**  
J: Ganti `PdfFormat.PDF_X_4` dengan `PdfFormat.PDFA_4` pada opsi konversi. Itu akan memenuhi kebutuhan **convert pdf to pdfa-4**.

**T: Sertifikat saya menggunakan algoritma hash yang berbeda—apakah saya bisa memakai SHA‑256?**  
J: Tentu. Ganti `DigestHashAlgorithm.Sha384` dengan `DigestHashAlgorithm.Sha256` (atau algoritma lain yang didukung).

**T: Apakah saya harus memanggil `document.Save` setelah setiap langkah?**  
J: Tidak mutlak. Pada alur ini kami menyimpan setelah konversi dan setelah penomoran Bates untuk memberi Anda file perantara. Anda dapat menunda penyimpanan hingga akhir jika menginginkan satu operasi penulisan saja.

## Penutup

Kami baru saja mendemonstrasikan solusi praktis end‑to‑end yang **add bates numbering pdf**, menjelaskan **how to add bates numbers**, menampilkan **convert pdf to pdf/x-4**, dan mencakup

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut membahas topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Aspose Pdf Net Add Attachments Convert Pdfa](/pdf/german/net/pdfa-compliance/aspose-pdf-net-add-attachments-convert-pdfa/)
- [Aspose Pdf Net Add Attachments Convert Pdfa](/pdf/french/net/pdfa-compliance/aspose-pdf-net-add-attachments-convert-pdfa/)
- [Aspose Pdf Net Add Attachments Convert Pdfa](/pdf/japanese/net/pdfa-compliance/aspose-pdf-net-add-attachments-convert-pdfa/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}