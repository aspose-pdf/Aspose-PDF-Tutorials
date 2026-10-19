---
title: Enkripsi PDF untuk Hanya Mengizinkan Pengisian Formulir Menggunakan Aspose.Pdf for .NET
weight: 101
limit:
description: Pelajari cara mengenkripsi PDF dengan AES‑256, mengatur kata sandi, dan membatasi izin hanya untuk pengisian formulir menggunakan Aspose.Pdf for .NET.
keywords: [Aspose.Pdf for .NET, encrypt PDF, PDF form filling permissions, AES-256 PDF encryption, viewer password PDF, owner password PDF]
url: /net/security-permissions/encrypt-pdf-form-filling/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Pelajari cara mengenkripsi PDF dengan AES‑256, mengatur kata sandi,
    dan membatasi izin hanya untuk pengisian formulir menggunakan Aspose.Pdf for .NET.
  headline: Enkripsi PDF untuk Hanya Mengizinkan Pengisian Formulir Menggunakan Aspose.Pdf
    for .NET
  type: TechArticle
- description: Pelajari cara mengenkripsi PDF dengan AES‑256, mengatur kata sandi,
    dan membatasi izin hanya untuk pengisian formulir menggunakan Aspose.Pdf for .NET.
  name: Enkripsi PDF untuk Hanya Mengizinkan Pengisian Formulir Menggunakan Aspose.Pdf
    for .NET
  steps:
  - name: Definisikan jalur file sumber dan tujuan serta kata sandi viewer dan owner.
    text: Definisikan jalur file sumber dan tujuan serta kata sandi viewer dan owner.
  - name: Periksa apakah PDF sumber ada dan batalkan dengan pesan error jika tidak.
    text: Periksa apakah PDF sumber ada dan batalkan dengan pesan error jika tidak.
  - name: Mulai blok try untuk menangani setiap error yang mungkin terjadi selama
      pemrosesan.
    text: Mulai blok try untuk menangani setiap error yang mungkin terjadi selama
      pemrosesan.
  - name: Buka file PDF yang ada dengan membuat objek Document bernama pdfDoc.
    text: Buka file PDF yang ada dengan membuat objek Document bernama pdfDoc.
  - name: Atur izin untuk hanya mengizinkan pengisian formulir, enkripsi dokumen dengan
      kata sandi viewer dan owner menggunakan AES‑256, dan simpan PDF yang dilindungi.
    text: Atur izin untuk hanya mengizinkan pengisian formulir, enkripsi dokumen dengan
      kata sandi viewer dan owner menggunakan AES‑256, dan simpan PDF yang dilindungi.
  - name: Tuliskan pesan konfirmasi ke konsol dan tutup blok try.
    text: Tuliskan pesan konfirmasi ke konsol dan tutup blok try.
  - name: Tangkap semua exception dan tampilkan pesan error ke konsol.
    text: Tangkap semua exception dan tampilkan pesan error ke konsol.
  type: HowTo
- questions:
  - answer: Saat dibuka dengan kata sandi viewer (pengguna), dokumen dapat dilihat
      dan bidang formulir dapat diisi, tetapi semua tindakan lain seperti mengedit
      teks, menambahkan anotasi, atau mengekstrak konten diblokir.
    question: Apa yang dapat dilakukan pengguna dengan PDF setelah dienkripsi dengan
      `Permissions.FillForm`?
  - answer: Gabungkan izin menggunakan operator OR bitwise, misalnya `Permissions
      allowed = Permissions.FillForm | Permissions.Printing;` dan berikan nilai gabungan
      tersebut ke `pdfDoc.Encrypt`.
    question: Bagaimana saya dapat mengizinkan hak tambahan, seperti mencetak, sambil
      tetap membatasi semua hal lainnya?
  - answer: Ya. Argumen pertama adalah kata sandi pengguna (viewer) yang memberikan
      hak terbatas, dan argumen kedua adalah kata sandi pemilik (admin) yang memberikan
      kontrol penuh atas dokumen.
    question: Apakah urutan kata sandi dalam `pdfDoc.Encrypt(viewerPass, adminPass,
      …)` penting?
  - answer: Aspose.Pdf akan melempar exception saat mencoba membuka file yang sudah
      dienkripsi; Anda harus terlebih dahulu membukanya dengan kata sandi yang ada,
      menghapus atau memodifikasi perlindungan, dan kemudian menerapkan pengaturan
      enkripsi baru.
    question: Apa yang terjadi jika PDF sumber sudah dilindungi kata sandi?
  type: FAQPage
images:
- /net/security-permissions/encrypt-pdf-form-filling/og-image.png
og_title: Enkripsi PDF dan Hanya Izinkan Pengisian Formulir
og_description: Amankan PDF Anda dengan AES‑256 dan biarkan pengguna mengisi formulir tetapi tidak melakukan hal lain.
og_image_alt: Tangkapan layar yang menampilkan kode Aspose.Pdf for .NET yang mengenkripsi PDF dan membatasinya hanya untuk pengisian formulir
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Enkripsi PDF untuk Hanya Mengizinkan Pengisian Formulir Menggunakan Aspose.Pdf
Pada tutorial ini Anda akan belajar cara membuka PDF yang sudah ada dengan Aspose.Pdf for .NET, menerapkan enkripsi AES‑256, mengatur kata sandi viewer dan owner, serta membatasi izin dokumen sehingga penerima hanya dapat mengisi bidang formulir. Pendekatan ini berguna ketika Anda perlu melindungi konten namun tetap memperbolehkan pengguna mengisi formulir interaktif. Kode tersebut menjelaskan setiap langkah dan menyimpan PDF yang aman siap untuk didistribusikan.

---

{{< tutorial-widget sourcePath="pdf/net/security-permissions/encrypt-pdf-form-filling" >}}


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

**Q: Apa yang dapat dilakukan pengguna dengan PDF setelah dienkripsi dengan `Permissions.FillForm`?**  
A: Saat dibuka dengan kata sandi viewer (pengguna), dokumen dapat dilihat dan bidang formulir dapat diisi, tetapi semua tindakan lain seperti mengedit teks, menambahkan anotasi, atau mengekstrak konten diblokir.

**Q: Bagaimana saya dapat mengizinkan hak tambahan, seperti mencetak, sambil tetap membatasi semua hal lainnya?**  
A: Gabungkan izin menggunakan operator OR bitwise, misalnya `Permissions allowed = Permissions.FillForm | Permissions.Printing;` dan berikan nilai gabungan tersebut ke `pdfDoc.Encrypt`.

**Q: Apakah urutan kata sandi dalam `pdfDoc.Encrypt(viewerPass, adminPass, …)` penting?**  
A: Ya. Argumen pertama adalah kata sandi pengguna (viewer) yang memberikan hak terbatas, dan argumen kedua adalah kata sandi pemilik (admin) yang memberikan kontrol penuh atas dokumen.

**Q: Apa yang terjadi jika PDF sumber sudah dilindungi kata sandi?**  
A: Aspose.Pdf akan melempar exception saat mencoba membuka file yang sudah dienkripsi; Anda harus terlebih dahulu membukanya dengan kata sandi yang ada, menghapus atau memodifikasi perlindungan, dan kemudian menerapkan pengaturan enkripsi baru.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}