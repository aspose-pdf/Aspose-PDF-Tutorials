---
category: general
date: 2026-02-20
description: Pelajari cara memvalidasi tanda tangan PDF dan menambahkan penomoran
  Bates ke PDF dalam C# dengan Aspose.Pdf – kode langkah demi langkah, penjelasan,
  dan tips praktik terbaik.
draft: false
keywords:
- how to validate pdf signature
- add bates numbering to pdf
- pdf signature validation c#
- bates numbering aspaspdf
- pdf conversion pdf/x‑4
language: id
og_description: Cara memvalidasi tanda tangan PDF dan menambahkan penomoran Bates
  ke PDF menggunakan Aspose.Pdf dalam C#. Tutorial lengkap dengan kode dan tips.
og_title: Cara Memvalidasi Tanda Tangan PDF dan Menambahkan Penomoran Bates ke PDF
tags:
- Aspose.Pdf
- C#
- PDF processing
title: Cara Memvalidasi Tanda Tangan PDF dan Menambahkan Penomoran Bates pada PDF
url: /id/net/digital-signatures/how-to-validate-pdf-signature-and-add-bates-numbering-to-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Memvalidasi Tanda Tangan PDF dan Menambahkan Penomoran Bates ke PDF

Pernah bertanya-tanya **bagaimana memvalidasi tanda tangan PDF** sebelum Anda mengirimkan kontrak ke klien? Mungkin Anda juga sedang mengelola berkas kasus dan membutuhkan cara yang andal untuk **menambahkan penomoran bates ke PDF** untuk pelacakan yang mudah. Bagaimanapun, Anda berada di tempat yang tepat. Dalam tutorial ini kami akan membahas contoh lengkap yang dapat dijalankan yang melakukan keduanya – memvalidasi tanda tangan digital yang ada, lalu menandai dokumen Anda dengan nomor Bates berurutan, semuanya menggunakan Aspose.Pdf untuk .NET.

Kami juga akan menambahkan beberapa trik tambahan: mengonversi ke PDF/X‑4, menyesuaikan sumber daya halaman, mengekspor ke HTML tanpa meraster gambar, dan akhirnya menerapkan tanda tangan digital berbasis SHA‑3. Pada akhir tutorial Anda akan memiliki satu program C# yang menangani seluruh alur kerja, siap untuk produksi atau bukti konsep cepat.

## Apa yang Anda Butuhkan

- **.NET 6+** (atau .NET Framework 4.7.2 – API berfungsi sama)
- **Aspose.Pdf for .NET** paket NuGet (versi terbaru pada saat penulisan, 23.12)
- Sebuah **file PDF** dengan tanda tangan yang ada (`input.pdf`)
- Sebuah **sertifikat PKCS#7** (`cert.pfx`) dan kata sandinya
- Sedikit pengalaman C# – kami akan menjaga kode tetap jelas dan banyak komentar.

Jika ada yang belum Anda kenal, berhentilah sejenak dan dapatkan bagian yang hilang; sisanya dalam panduan mengasumsikan semuanya sudah tersedia.

---

## Langkah 1: Muat Dokumen PDF  

Hal pertama yang Anda lakukan adalah membuat objek `Document` yang mewakili seluruh file PDF. Anggap saja seperti memuat workbook di Excel – Anda memerlukan objek tersebut sebelum dapat memeriksa atau mengubah apa pun.

```csharp
using System;
using Aspose.Pdf;

static void Main()
{
    // Load the source PDF that may already contain a digital signature
    Document pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");
```

> **Mengapa ini penting:** Tanpa memuat dokumen Anda tidak dapat mengakses bidang tanda tangan atau koleksi halaman. Aspose.Pdf mengabstraksi struktur PDF tingkat rendah, memungkinkan Anda bekerja dengan objek tingkat tinggi seperti `Pages` dan `Resources`.

---

## Langkah 2: Validasi Tanda Tangan PDF yang Ada  

Sekarang kami menjawab pertanyaan utama: **bagaimana memvalidasi tanda tangan pdf**? Kelas `PdfFileSignature` menyediakan metode `ValidateSignature` yang mengembalikan `SignatureValidationResult`. Metode ini memberi tahu Anda apakah tanda tangan masih utuh, dicabut, atau telah terkompromi.

```csharp
    // Detect if the existing signature is compromised
    PdfFileSignature signatureValidator = new PdfFileSignature(pdfDocument);
    var validationResult = signatureValidator.ValidateSignature();

    Console.WriteLine($"Compromised? {validationResult.IsCompromised}");
```

> **Tip profesional:** `IsCompromised` mengembalikan `true` jika dokumen diubah setelah penandatanganan, atau jika rantai sertifikat tidak dapat diverifikasi. Untuk keperluan forensik, periksa juga `validationResult.ValidationErrors` untuk pesan detail.

---

## Langkah 3: Konversi ke PDF/X‑4 (Opsional tapi Berguna)  

Alur kerja hukum dan arsip sering memerlukan kepatuhan PDF/X. Mengonversi ke PDF/X‑4 juga menghapus kesalahan konversi yang tersisa yang dapat mengganggu sistem hilir.

```csharp
    // Convert the PDF to PDF/X‑4, deleting any conversion errors automatically
    PdfFormatConversionOptions conversionOptions =
        new PdfFormatConversionOptions(PdfFormat.PDF_X_4, ConvertErrorAction.Delete);
    pdfDocument.Convert(conversionOptions);
```

> **Mengapa mengonversi?** PDF/X‑4 menjamin semua profil warna dan font tersemat, mengurangi risiko masalah rendering ketika file dibuka di platform yang berbeda.

---

## Langkah 4: Tambahkan Penomoran Bates ke PDF  

Di sinilah kami **menambahkan penomoran bates ke pdf** – hal yang wajib untuk litigasi, audit, atau kumpulan dokumen besar apa pun. `BatesNumberingOptions` memungkinkan Anda mengatur awalan, nomor mulai, dan bahkan format.

```csharp
    // Add Bates numbering for case management
    BatesNumberingOptions batesOptions = new BatesNumberingOptions
    {
        Prefix = "CASE",   // You can change this to any identifier you need
        Start = 5000       // Starting number – adjust as required
    };
    pdfDocument.Pages.AddBatesNumbering(batesOptions);
```

> **Tip dunia nyata:** Jaga agar awalan singkat (3‑5 karakter) untuk menghindari pemotongan baris pada halaman sempit. Jika Anda memerlukan penomoran per‑bagian, jalankan `AddBatesNumbering` pada subset halaman alih-alih seluruh dokumen.

---

## Langkah 5: Sisipkan Kamus ExtGState (Contoh Opasitas Redaksi)  

Kadang-kadang Anda perlu mengontrol keadaan grafik – misalnya, mengatur lapisan redaksi semi‑transparan. Langkah ini menunjukkan cara menyuntikkan kamus ExtGState khusus ke dalam sumber daya halaman pertama.

```csharp
    // Insert an ExtGState dictionary on the first page (example: redaction opacity)
    Page firstPage = pdfDocument.Pages[1];
    DictionaryEditor resourcesEditor = new DictionaryEditor(firstPage.Resources);
    CosPdfDictionary extGStateDictionary = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
    extGStateDictionary.Add("CA", new CosPdfNumber(1));   // stroke opacity
    extGStateDictionary.Add("ca", new CosPdfNumber(0.5)); // fill opacity
    resourcesEditor["ExtGState"] = extGStateDictionary;
```

> **Kapan digunakan:** Jika Anda membuat alat redaksi, Anda nanti akan merujuk ke ExtGState ini saat menggambar bentuk yang menutupi teks sensitif.

---

## Langkah 6: Simpan sebagai HTML Tanpa Meraster Gambar  

Mengekspor ke HTML dapat berguna untuk pratinjau web. Secara default Aspose.Pdf meraster gambar, yang memperbesar ukuran file. Menetapkan `SkipRasterImages` mempertahankan vektor asli.

```csharp
    // Save the document as HTML without rasterizing images
    HtmlSaveOptions htmlSaveOptions = new HtmlSaveOptions { SkipRasterImages = true };
    pdfDocument.Save("YOUR_DIRECTORY/output.html", htmlSaveOptions);
```

> **Hasil:** `output.html` yang dihasilkan berisi tag `<img>` ringan yang mengarah ke aliran gambar asli, menjaga halaman tetap tajam dan cepat dimuat.

---

## Langkah 7: Tanda Tangani PDF dengan Hash SHA‑3  

Akhirnya, kami menandatangani PDF (yang kini telah bernomor) menggunakan hash SHA‑3‑512. SHA‑3 lebih baru daripada SHA‑256 tradisional dan menawarkan konstruksi kriptografi yang berbeda, yang kini diperlukan oleh beberapa standar kepatuhan.

```csharp
    // Sign the PDF using a SHA‑3 hash and save the signed version
    PKCS7Detached pkcs7Signature = new PKCS7Detached(
        "YOUR_DIRECTORY/cert.pfx",
        "YOUR_PASSWORD",
        DigestHashAlgorithm.Sha3_512);

    PdfFileSignature pdfSigner = new PdfFileSignature(pdfDocument);
    // Sign on page 1, visible rectangle (x, y, width, height)
    pdfSigner.Sign(1, true, new Rectangle(100, 100, 200, 150), pkcs7Signature);
    pdfSigner.Save("YOUR_DIRECTORY/signed.pdf");
}
```

> **Penting:** Persegi panjang menentukan di mana tampilan tanda tangan yang terlihat akan ditempatkan. Sesuaikan koordinat agar cocok dengan tata letak dokumen Anda.

---

## Contoh Lengkap yang Berfungsi  

Berikut adalah program lengkap, siap untuk disalin‑tempel ke aplikasi konsol. Ganti jalur placeholder dan kata sandi dengan nilai Anda sendiri.

```csharp
using System;
using Aspose.Pdf;

static void Main()
{
    // 1️⃣ Load the PDF
    Document pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");

    // 2️⃣ Validate existing signature
    PdfFileSignature signatureValidator = new PdfFileSignature(pdfDocument);
    var validationResult = signatureValidator.ValidateSignature();
    Console.WriteLine($"Compromised? {validationResult.IsCompromised}");

    // 3️⃣ Convert to PDF/X‑4
    PdfFormatConversionOptions conversionOptions =
        new PdfFormatConversionOptions(PdfFormat.PDF_X_4, ConvertErrorAction.Delete);
    pdfDocument.Convert(conversionOptions);

    // 4️⃣ Add Bates numbering (add bates numbering to pdf)
    BatesNumberingOptions batesOptions = new BatesNumberingOptions
    {
        Prefix = "CASE",
        Start = 5000
    };
    pdfDocument.Pages.AddBatesNumbering(batesOptions);

    // 5️⃣ Insert ExtGState (redaction opacity)
    Page firstPage = pdfDocument.Pages[1];
    DictionaryEditor resourcesEditor = new DictionaryEditor(firstPage.Resources);
    CosPdfDictionary extGStateDictionary = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
    extGStateDictionary.Add("CA", new CosPdfNumber(1));
    extGStateDictionary.Add("ca", new CosPdfNumber(0.5));
    resourcesEditor["ExtGState"] = extGStateDictionary;

    // 6️⃣ Save as HTML (no raster images)
    HtmlSaveOptions htmlSaveOptions = new HtmlSaveOptions { SkipRasterImages = true };
    pdfDocument.Save("YOUR_DIRECTORY/output.html", htmlSaveOptions);

    // 7️⃣ Sign with SHA‑3
    PKCS7Detached pkcs7Signature = new PKCS7Detached(
        "YOUR_DIRECTORY/cert.pfx",
        "YOUR_PASSWORD",
        Digest
{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}