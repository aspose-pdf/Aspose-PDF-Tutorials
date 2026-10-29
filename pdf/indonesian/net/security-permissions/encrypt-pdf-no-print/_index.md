---
title: Enkripsi PDF dengan Izin Tanpa Cetak Menggunakan Aspose.PDF untuk .NET
weight: 101
limit:
description: Pelajari cara mengenkripsi PDF dengan AES‑256 dan menonaktifkan pencetakan menggunakan Aspose.PDF untuk .NET.
keywords: [Aspose.PDF for .NET, pdf encryption aes-256, disable pdf printing, pdf password protection, no print permission pdf]
url: /net/security-permissions/encrypt-pdf-no-print/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Pelajari cara mengenkripsi PDF dengan AES‑256 dan menonaktifkan pencetakan
    menggunakan Aspose.PDF untuk .NET.
  headline: Enkripsi PDF dengan Izin Tanpa Cetak Menggunakan Aspose.PDF untuk .NET
  type: TechArticle
- description: Pelajari cara mengenkripsi PDF dengan AES‑256 dan menonaktifkan pencetakan
    menggunakan Aspose.PDF untuk .NET.
  name: Enkripsi PDF dengan Izin Tanpa Cetak Menggunakan Aspose.PDF untuk .NET
  steps:
  - name: Tentukan jalur PDF sumber, nama file output yang dilindungi, serta kata
      sandi viewer dan owner.
    text: Tentukan jalur PDF sumber, nama file output yang dilindungi, serta kata
      sandi viewer dan owner.
  - name: Periksa apakah file sumber ada dan batalkan dengan pesan error jika tidak
      ditemukan.
    text: Periksa apakah file sumber ada dan batalkan dengan pesan error jika tidak
      ditemukan.
  - name: Buka PDF asli, tidak mengatur izin apa pun, enkripsi dengan AES‑256 menggunakan
      kata sandi yang ditentukan, dan simpan file yang dilindungi.
    text: Buka PDF asli, tidak mengatur izin apa pun, enkripsi dengan AES‑256 menggunakan
      kata sandi yang ditentukan, dan simpan file yang dilindungi.
  - name: Buka kembali PDF yang dienkripsi dengan kata sandi viewer dan tulis flag
      IsEncrypted‑nya ke console untuk mengonfirmasi perlindungan.
    text: Buka kembali PDF yang dienkripsi dengan kata sandi viewer dan tulis flag
      IsEncrypted‑nya ke console untuk mengonfirmasi perlindungan.
  - name: Cetak pesan akhir yang menunjukkan bahwa enkripsi selesai dan nama file
      output.
    text: Cetak pesan akhir yang menunjukkan bahwa enkripsi selesai dan nama file
      output.
  type: HowTo
- questions:
  - answer: '`Permissions` adalah enum flag; menetapkan `0` berarti tidak ada bit
      izin yang diatur, sehingga Aspose.Pdf tidak memberikan hak PrintDocument dan
      viewer tidak dapat mencetak PDF.'
    question: Mengapa mengatur `Permissions rights = 0;` menonaktifkan pencetakan?
  - answer: Ya, ganti `CryptoAlgorithm.AESx256` dengan `CryptoAlgorithm.AESx128` (atau
      nilai enum lain yang didukung) dalam pemanggilan `pdfDoc.Encrypt`; sisanya tetap
      tidak berubah.
    question: Apakah saya dapat menggunakan algoritma enkripsi lain, seperti AES‑128,
      dengan kode yang sama?
  - answer: Aspose.Pdf akan menerima kata sandi yang identik, tetapi kata sandi owner
      tidak lagi memberikan hak istimewa tambahan; PDF tetap akan dienkripsi, dan
      izin yang Anda tentukan (tidak ada) akan diterapkan.
    question: Apa yang terjadi jika kata sandi viewer dan kata sandi master (owner)
      sama?
  - answer: Buka file yang dilindungi dengan kata sandi viewer (`new Document(securedFile,
      viewerPwd)`) dan coba cetak dari PDF viewer; karena tidak ada izin `PrintDocument`
      yang diatur, viewer akan menolak perintah cetak.
    question: Bagaimana saya dapat memastikan bahwa pencetakan benar-benar diblokir
      setelah enkripsi?
  - answer: Kode memeriksa `File.Exists(sourceFile)` dan menulis error ke `Console.Error`
      sebelum kembali, sehingga mencegah `FileNotFoundException` dilemparkan oleh
      konstruktor `Document`.
    question: Error apa yang dilemparkan jika `original.pdf` tidak ada, dan bagaimana
      cara menanganinya?
  type: FAQPage
images:
- /net/security-permissions/encrypt-pdf-no-print/og-image.png
og_title: Enkripsi PDF dan Blokir Pencetakan
og_description: Amankan PDF Anda dengan enkripsi AES‑256 dan pastikan tidak dapat dicetak—panduan langkah demi langkah.
og_image_alt: Tangkapan layar yang menampilkan kode Aspose.PDF untuk .NET yang mengenkripsi PDF dan menonaktifkan pencetakan.
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Enkripsi PDF dengan Izin Tanpa Cetak Menggunakan Aspose.PDF untuk .NET
Tutorial ini menunjukkan cara membuka PDF yang sudah ada dengan Aspose.PDF untuk .NET, menerapkan enkripsi AES‑256 sambil tidak memberikan izin apa pun—yang secara efektif menonaktifkan pencetakan—menyimpan dokumen yang diamankan, dan mengonfirmasi perlindungan dengan membukanya menggunakan kata sandi viewer. Ikuti kode langkah demi langkah untuk memastikan PDF Anda tidak dapat dicetak setelah enkripsi.

---

{{< tutorial-widget sourcePath="pdf/net/security-permissions/encrypt-pdf-no-print" >}}


{{< /blocks/products/pf/tutorial-page-section >}}

{{< blocks/products/pf/tutorial-page-section >}}
## Installation Instructions
1. Download Aspose.Pdf for .NET:
   Get the latest version from the [Aspose Downloads page](https://releases.aspose.com/pdf/net/).

2. Install via NuGet:
   - Open your Visual Studio project.
   - Navigate to the NuGet Package Manager (Tools > NuGet Package Manager > Manage NuGet Packages for Solution).
   - Search for "Aspose.Pdf" and click Install.

3. Add Namespace References:
   Add the following namespace at the top of your code file:
   ```csharp
   using Aspose.Pdf;
   using Aspose.Pdf.Devices;
   using Aspose.Pdf.Operators;
   ```

4. Apply License (Optional):
   To use the full version, [apply a license](https://purchase.aspose.com/temporary-license/) or use a [free trial](https://releases.aspose.com/).

## Also See
[Aspose.Pdf for .NET Documentation](https://docs.aspose.com/pdf/net/)
[Aspose.Pdf for .NET References](https://reference.aspose.com/pdf/net/)

## Frequently asked questions

**Q: Mengapa mengatur `Permissions rights = 0;` menonaktifkan pencetakan?**  
A: `Permissions` adalah enum flag; menetapkan `0` berarti tidak ada bit izin yang diatur, sehingga Aspose.Pdf tidak memberikan hak PrintDocument dan viewer tidak dapat mencetak PDF.

**Q: Apakah saya dapat menggunakan algoritma enkripsi lain, seperti AES‑128, dengan kode yang sama?**  
A: Ya, ganti `CryptoAlgorithm.AESx256` dengan `CryptoAlgorithm.AESx128` (atau nilai enum lain yang didukung) dalam pemanggilan `pdfDoc.Encrypt`; sisanya tetap tidak berubah.

**Q: Apa yang terjadi jika kata sandi viewer dan kata sandi master (owner) sama?**  
A: Aspose.Pdf akan menerima kata sandi yang identik, tetapi kata sandi owner tidak lagi memberikan hak istimewa tambahan; PDF tetap akan dienkripsi, dan izin yang Anda tentukan (tidak ada) akan diterapkan.

**Q: Bagaimana saya dapat memastikan bahwa pencetakan benar-benar diblokir setelah enkripsi?**  
A: Buka file yang dilindungi dengan kata sandi viewer (`new Document(securedFile, viewerPwd)`) dan coba cetak dari PDF viewer; karena tidak ada izin `PrintDocument` yang diatur, viewer akan menolak perintah cetak.

**Q: Error apa yang dilemparkan jika `original.pdf` tidak ada, dan bagaimana cara menanganinya?**  
A: Kode memeriksa `File.Exists(sourceFile)` dan menulis error ke `Console.Error` sebelum kembali, sehingga mencegah `FileNotFoundException` dilemparkan oleh konstruktor `Document`.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}