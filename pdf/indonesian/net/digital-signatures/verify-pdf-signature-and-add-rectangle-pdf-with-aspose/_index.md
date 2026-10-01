---
category: general
date: 2026-02-09
description: Verifikasi tanda tangan PDF dengan Aspose.PDF di C#. Pelajari cara menambahkan
  persegi panjang pada PDF, menyimpan PDF yang diperbarui, dan menggunakan fitur tanda
  tangan Aspose PDF.
draft: false
keywords:
- verify pdf signature
- add rectangle pdf
- save updated pdf
- aspose pdf signature
- add graphics pdf
language: id
og_description: Verifikasi tanda tangan PDF dalam C# dengan cepat. Panduan ini menunjukkan
  cara menambahkan grafik PDF, menyimpan PDF yang diperbarui, dan menggunakan API
  tanda tangan Aspose PDF.
og_title: Verifikasi Tanda Tangan PDF dan Tambahkan Persegi Panjang PDF – Panduan
  Lengkap Aspose
tags:
- Aspose.PDF
- C#
- Digital Signature
- PDF Manipulation
title: Verifikasi tanda tangan PDF dan tambahkan persegi panjang pada PDF dengan Aspose
url: /id/net/digital-signatures/verify-pdf-signature-and-add-rectangle-pdf-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# verifikasi tanda tangan pdf dan tambahkan persegi panjang pdf dengan Aspose

Pernah perlu **verifikasi tanda tangan pdf** dalam proyek C# tetapi tidak yakin harus mulai dari mana? Anda tidak sendirian—tanda tangan digital adalah keharusan untuk kepatuhan, namun banyak pengembang mengalami kesulitan ketika mereka juga harus mengubah dokumen setelahnya.  

Dalam tutorial ini kita akan melewati contoh lengkap yang dapat dijalankan yang **memverifikasi tanda tangan pdf**, menambahkan **persegi panjang** ke halaman pertama, memeriksa bahwa bentuk tetap berada di dalam batas halaman, dan akhirnya **menyimpan pdf yang diperbarui**—semua menggunakan API modern Aspose.PDF. Pada akhir tutorial Anda akan memiliki satu program mandiri yang dapat dimasukkan ke dalam solusi .NET apa pun.

## Apa yang akan Anda pelajari

- Memuat PDF yang ditandatangani dengan Aspose.PDF.  
- Menggunakan kelas **aspose pdf signature** untuk memverifikasi setiap tanda tangan dan mendeteksi kompromi.  
- **Menambahkan persegi panjang pdf** secara aman, memastikan mereka sesuai dengan halaman.  
- **Menyimpan pdf yang diperbarui** sambil mempertahankan tanda tangan yang ada.  
- Tips, penanganan kasus tepi, dan jebakan umum.

Tidak ada dokumen eksternal yang diperlukan—semua yang Anda butuhkan ada di sini.

## Prasyarat

- .NET 6.0 atau lebih baru (kode ini juga berfungsi pada .NET Framework 4.7+).  
- Paket NuGet Aspose.PDF untuk .NET (≥ 23.10). Instal dengan:

```bash
dotnet add package Aspose.Pdf
```

- Sebuah file PDF yang ditandatangani bernama `signed.pdf` ditempatkan di folder yang Anda kontrol (ganti `YOUR_DIRECTORY` dalam kode).  
- Familiaritas dasar dengan C# serta Visual Studio atau VS Code.

> **Pro tip:** Jika Anda tidak memiliki PDF yang ditandatangani, Aspose menyediakan file demo gratis di situs mereka yang dapat Anda unduh untuk pengujian.

---

## verifikasi tanda tangan pdf – Langkah demi Langkah

Hal pertama yang perlu kita lakukan adalah membuka dokumen dan mengulang setiap tanda tangan digital. Aspose.PDF menyediakan dua metode yang berguna: `VerifySignature` memberi tahu Anda apakah pemeriksaan kriptografis berhasil, sementara `IsSignatureCompromised` yang lebih baru menandai setiap manipulasi yang mungkin terjadi setelah penandatanganan.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Facades;

// Load the signed PDF document
Document pdfDocument = new Document("YOUR_DIRECTORY/signed.pdf");

// Create a signature handler for the document
PdfFileSignature signatureHandler = new PdfFileSignature(pdfDocument);

// Iterate over each signature name in the PDF
foreach (var signatureName in signatureHandler.GetSignNames())
{
    // Verify the cryptographic integrity
    bool isValid = signatureHandler.VerifySignature(signatureName);
    
    // Detect if the signature has been compromised (e.g., document altered)
    bool isCompromised = signatureHandler.IsSignatureCompromised(signatureName);
    
    Console.WriteLine($"{signatureName}: valid={isValid}, compromised={isCompromised}");
}
```

**Mengapa ini penting:**  
- `VerifySignature` saja hanya mengonfirmasi bahwa sertifikat penandatangan masih dipercaya.  
- `IsSignatureCompromised` menangkap perubahan halus—seperti penambahan objek tersembunyi—sehingga Anda tahu apakah konten visual PDF diubah setelah penandatanganan.

**Output yang diharapkan** (contoh dengan dua tanda tangan):

```
Signature1: valid=True, compromised=False
Signature2: valid=True, compromised=True
```

Jika ada tanda tangan yang melaporkan `compromised=True`, Anda harus menghentikan pemrosesan lebih lanjut atau memberi peringatan kepada pengguna, karena integritas dokumen tidak dapat dijamin.

---

## menambahkan persegi panjang pdf ke sebuah halaman

Setelah kita memastikan tanda tangan tetap utuh (atau setidaknya mengetahui adanya kompromi), mari tambahkan grafik persegi panjang sederhana. Ini berguna untuk menempelkan label “Reviewed”, menyorot bagian, atau sekadar menarik perhatian ke suatu area.

```csharp
// Access the first page (pages are 1‑based in Aspose)
Page firstPage = pdfDocument.Pages[1];

// Define a rectangle shape (coordinates: lower-left X, lower-left Y, upper-right X, upper-right Y)
Rectangle shapeRect = new Rectangle(100, 500, 200, 600);

// Add the rectangle to the page's graphics collection
firstPage.AddRectangle(shapeRect);
```

**Apa arti angka-angka tersebut:**  
- Sistem koordinat PDF dimulai dari sudut kiri‑bawah.  
- Pada contoh, persegi panjang memiliki lebar 100 poin secara horizontal dan tinggi 100 poin secara vertikal, ditempatkan kira‑kira di tengah halaman A4 standar.

> **Catatan:** Aspose juga mendukung `AddEllipse`, `AddPolygon`, dll., jika Anda memerlukan bentuk yang lebih kaya.

---

## memeriksa batas grafik – memastikan persegi panjang muat

Sebelum kita menyimpan perubahan, sebaiknya memverifikasi bahwa grafik kita tetap berada di dalam area cetak halaman. Metode baru `CheckGraphicsBounds` melakukan hal itu secara tepat.

```csharp
// Verify that the rectangle does not exceed page limits
bool shapeFits = firstPage.CheckGraphicsBounds(shapeRect);
Console.WriteLine($"Shape fits page: {shapeFits}");
```

Jika `shapeFits` mengembalikan `false`, Anda perlu menyesuaikan koordinat persegi panjang—mungkin memperkecilnya atau memindahkannya lebih rendah pada halaman. Ini mencegah pemotongan tidak sengaja yang dapat terlihat tidak profesional, terutama ketika PDF nanti dicetak.

---

## menyimpan pdf yang diperbarui – mempertahankan tanda tangan dan grafik baru

Akhirnya, kita menulis dokumen yang telah dimodifikasi kembali ke disk. Metode `Save` menghormati tanda tangan yang ada; ia tidak akan membuatnya tidak valid kecuali konten benar‑benar berubah (yang sudah kami periksa dengan `IsSignatureCompromised`).

```csharp
// Save the updated PDF to a new file
pdfDocument.Save("YOUR_DIRECTORY/output.pdf");

// Inform the user
Console.WriteLine("PDF saved as output.pdf with new rectangle.");
```

**Mengapa menggunakan file baru?**  
Menyimpan di atas file asli dapat menghapus tanda tangan asli, membuatnya tidak mungkin membandingkan keadaan sebelum/setelah. Dengan menulis ke `output.pdf` Anda tetap mempertahankan sumber untuk keperluan audit.

---

## Contoh lengkap yang dapat dijalankan

Berikut adalah program lengkap yang dapat Anda salin‑tempel ke aplikasi console. Semua langkah digabungkan, komentar menjelaskan setiap blok, dan Anda akan melihat output konsol yang diharapkan di akhir.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Facades;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Load the signed PDF document
        // -------------------------------------------------
        string inputPath = "YOUR_DIRECTORY/signed.pdf";
        Document pdfDocument = new Document(inputPath);
        Console.WriteLine($"Loaded PDF: {inputPath}");

        // -------------------------------------------------
        // 2️⃣ Verify each digital signature and detect compromise
        // -------------------------------------------------
        PdfFileSignature signatureHandler = new PdfFileSignature(pdfDocument);
        foreach (var signatureName in signatureHandler.GetSignNames())
        {
            bool isValid = signatureHandler.VerifySignature(signatureName);
            bool isCompromised = signatureHandler.IsSignatureCompromised(signatureName);
            Console.WriteLine($"{signatureName}: valid={isValid}, compromised={isCompromised}");
        }

        // -------------------------------------------------
        // 3️⃣ Access the first page and add a rectangle
        // -------------------------------------------------
        Page firstPage = pdfDocument.Pages[1];
        Rectangle shapeRect = new Rectangle(100, 500, 200, 600);
        firstPage.AddRectangle(shapeRect);
        Console.WriteLine("Added rectangle to page 1.");

        // -------------------------------------------------
        // 4️⃣ Ensure the rectangle fits inside the page bounds
        // -------------------------------------------------
        bool shapeFits = firstPage.CheckGraphicsBounds(shapeRect);
        Console.WriteLine($"Shape fits page: {shapeFits}");

        // -------------------------------------------------
        // 5️⃣ Save the updated PDF
        // -------------------------------------------------
        string outputPath = "YOUR_DIRECTORY/output.pdf";
        pdfDocument.Save(outputPath);
        Console.WriteLine($"Saved updated PDF as: {outputPath}");
    }
}
```

**Output konsol yang diharapkan** (asumsi satu tanda tangan yang valid dan tidak dikompromikan):

```
Loaded PDF: YOUR_DIRECTORY/signed.pdf
Signature1: valid=True, compromised=False
Added rectangle to page 1.
Shape fits page: True
Saved updated PDF as: YOUR_DIRECTORY/output.pdf
```

Jika sebuah tanda tangan dikompromikan, Anda akan melihat `compromised=True` dan dapat memutuskan apakah akan melanjutkan.

---

## Pertanyaan umum & penanganan kasus tepi

| Pertanyaan | Jawaban |
|----------|--------|
| **Bagaimana jika PDF tidak memiliki tanda tangan?** | `GetSignNames()` mengembalikan koleksi kosong; loop cukup dilewati, dan Anda tetap dapat menambahkan grafik. |
| **Apakah saya dapat menambahkan beberapa persegi panjang?** | Ya—cukup panggil `AddRectangle` berulang kali dengan objek `Rectangle` yang berbeda. |
| **Bagaimana dengan PDF yang dilindungi kata sandi?** | Muat dengan `pdfDocument = new Document("file.pdf", new LoadOptions("password"));` sebelum verifikasi. |
| **Apakah menambahkan grafik akan membuat tanda tangan yang valid menjadi tidak valid?** | Hanya jika tanda tangan mencakup halaman tempat Anda menyisipkan grafik. Gunakan `IsSignatureCompromised` untuk mendeteksinya; jika tidak, tanda tangan tetap utuh. |
| **Apakah saya perlu menutup resource?** | Objek Aspose.PDF dikelola; disposing bersifat opsional tetapi Anda dapat membungkus kode dalam blok `using` untuk keamanan ekstra. |

---

## Pro tip untuk penggunaan produksi

- **Pemrosesan batch:** Bungkus seluruh rutinitas dalam metode yang menerima jalur input/output; kemudian berikan daftar file ke `Parallel.ForEach` untuk meningkatkan kecepatan.  
- **Logging:** Ganti `Console.WriteLine` dengan logger yang tepat (misalnya Serilog) untuk merekam hasil verifikasi dalam jejak audit.  
- **Kebijakan tanda tangan:** Gabungkan `VerifySignature` dengan pemeriksaan pencabutan sertifikat (OCSP/CRL) untuk kepatuhan yang lebih ketat.  
- **Styling grafik:** Gunakan `firstPage.AddRectangle(shapeRect, new GraphicState { StrokeColor = Color.Red, FillColor = Color.Yellow });` agar persegi panjang menonjol.  
- **Kunci versi:** Pin versi NuGet Aspose.PDF untuk menghindari perubahan yang merusak ketika perpustakaan diperbarui.

---

## Kesimpulan

Anda kini memiliki contoh menyeluruh end‑to‑end yang **memverifikasi tanda tangan pdf**, **menambahkan persegi panjang pdf**, dan **menyimpan pdf yang diperbarui** menggunakan API terbaru Aspose.PDF. Kode ini memeriksa tanda tangan yang dikompromikan, memastikan grafik tetap dalam batas halaman, dan mempertahankan tanda tangan digital asli—tepat apa yang dibutuhkan dalam alur kerja kepatuhan dunia nyata.

Selanjutnya, Anda dapat menjelajahi:

- Menambahkan **grafik pdf** seperti watermark atau kode QR.  
- Menggunakan API **aspose pdf signature** untuk membuat tanda tangan baru secara programatis.  
- Mengotomatiskan proses dalam layanan web ASP.NET Core untuk validasi dokumen secara real‑time.

Cobalah, ubah koordinat persegi panjang, dan lihat bagaimana perpustakaan bereaksi terhadap struktur PDF yang berbeda. Selamat coding, semoga PDF Anda tetap tertandatangani dan bergaya! 

![verify pdf signature example](image.png "verify pdf signature example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}