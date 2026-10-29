---
title: Perbandingan PDF Berdampingan dengan Mengecualikan Anotasi menggunakan Aspose.Pdf untuk .NET
weight: 101
limit:
description: Panduan langkah demi langkah untuk membandingkan PDF dan mengecualikan area anotasi menggunakan Aspose.Pdf untuk .NET.
keywords: [pdf comparison, exclude annotations, Aspose.Pdf for .NET, side by side comparison, annotation bounding boxes, diff pdf]
url: /net/forms-annotations/exclude-annotations/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Panduan langkah demi langkah untuk membandingkan PDF dan mengecualikan
    area anotasi menggunakan Aspose.Pdf untuk .NET.
  headline: Perbandingan PDF Berdampingan dengan Mengecualikan Anotasi menggunakan
    Aspose.Pdf untuk .NET
  type: TechArticle
- description: Panduan langkah demi langkah untuk membandingkan PDF dan mengecualikan
    area anotasi menggunakan Aspose.Pdf untuk .NET.
  name: Perbandingan PDF Berdampingan dengan Mengecualikan Anotasi menggunakan Aspose.Pdf
    untuk .NET
  steps:
  - name: Tentukan jalur file untuk PDF utama, PDF sekunder, dan PDF diff output.
    text: Tentukan jalur file untuk PDF utama, PDF sekunder, dan PDF diff output.
  - name: Periksa bahwa kedua file PDF input ada dan batalkan dengan pesan error jika
      salah satu tidak ada.
    text: Periksa bahwa kedua file PDF input ada dan batalkan dengan pesan error jika
      salah satu tidak ada.
  - name: Buka kedua file PDF sebagai objek Document (pdfA dan pdfB) dalam blok using
      sehingga mereka dibuang secara otomatis.
    text: Buka kedua file PDF sebagai objek Document (pdfA dan pdfB) dalam blok using
      sehingga mereka dibuang secara otomatis.
  - name: Kumpulkan persegi panjang pembatas setiap anotasi di pdfA dan simpan dalam
      ignoredRectsA.
    text: Kumpulkan persegi panjang pembatas setiap anotasi di pdfA dan simpan dalam
      ignoredRectsA.
  - name: Kumpulkan persegi panjang pembatas setiap anotasi di pdfB dan simpan dalam
      ignoredRectsB.
    text: Kumpulkan persegi panjang pembatas setiap anotasi di pdfB dan simpan dalam
      ignoredRectsB.
  - name: Buat objek SideBySideComparisonOptions dan tetapkan persegi panjang anotasi
      yang telah dikumpulkan sebelumnya ke ExcludeAreas1 dan ExcludeAreas2 sehingga
      wilayah tersebut diabaikan selama perbandingan.
    text: Buat objek SideBySideComparisonOptions dan tetapkan persegi panjang anotasi
      yang telah dikumpulkan sebelumnya ke ExcludeAreas1 dan ExcludeAreas2 sehingga
      wilayah tersebut diabaikan selama perbandingan.
  - name: Jalankan perbandingan PDF berdampingan menggunakan dua objek Document dan
      opsi yang dikonfigurasi, menulis hasilnya ke outputPdf.
    text: Jalankan perbandingan PDF berdampingan menggunakan dua objek Document dan
      opsi yang dikonfigurasi, menulis hasilnya ke outputPdf.
  - name: Buang objek Document dan keluar dari blok using.
    text: Buang objek Document dan keluar dari blok using.
  - name: Cetak pesan konfirmasi yang menunjukkan bahwa perbandingan selesai dan di
      mana PDF diff disimpan.
    text: Cetak pesan konfirmasi yang menunjukkan bahwa perbandingan selesai dan di
      mana PDF diff disimpan.
  type: HowTo
- questions:
  - answer: Ya. Kode tersebut hanya tidak menambahkan persegi panjang apa pun ke daftar
      `ignoredRects` yang bersangkutan, sehingga `ExcludeAreas1`/`ExcludeAreas2` menerima
      array kosong dan pembanding memproses seluruh halaman.
    question: Apa yang terjadi jika halaman PDF tidak memiliki anotasi – apakah perbandingan
      tetap berfungsi?
  - answer: Setel `ExcludeAreas1` (atau `ExcludeAreas2`) ke persegi panjang yang dikumpulkan
      dan biarkan properti lainnya sebagai array kosong; pembanding akan mengabaikan
      wilayah hanya pada dokumen yang ditentukan.
    question: Bisakah saya mengecualikan hanya anotasi dari satu dokumen sementara
      mempertahankan anotasi dokumen lain dalam diff?
  - answer: Persegi panjang yang tumpang tindih digabungkan secara internal oleh pembanding,
      sehingga batas anotasi yang tumpang tindih dikecualikan dengan aman tanpa menghitung
      ganda.
    question: Apakah persegi panjang anotasi yang tumpang tindih menyebabkan masalah
      dengan `ExcludeAreas`?
  - answer: Ya, setel `compareOpts.ExcludeTables = true;` – flag ini bekerja bersama
      `ExcludeAreas1`/`ExcludeAreas2` untuk mengabaikan wilayah tabel juga.
    question: Apakah ada cara untuk mengecualikan tabel selain anotasi menggunakan
      objek opsi yang sama?
  - answer: Kode memeriksa `if (a != null && a.Rect != null)` sebelum menambahkan
      ke daftar, sehingga persegi panjang null hanya dilewati dan tidak ada pengecualian
      yang dilempar.
    question: Bagaimana jika properti `Rect` dari anotasi bernilai null – apakah kode
      akan melempar pengecualian?
  type: FAQPage
images:
- /net/forms-annotations/exclude-annotations/og-image.png
og_title: Bandingkan PDF Tanpa Anotasi
og_description: Jalankan diff PDF berdampingan yang melewatkan semua tanda anotasi.
og_image_alt: Panduan yang menunjukkan perbandingan PDF berdampingan yang mengecualikan wilayah anotasi menggunakan Aspose.Pdf untuk .NET
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Perbandingan PDF Berdampingan dengan Mengecualikan Anotasi menggunakan Aspose.Pdf untuk .NET
Tutorial ini menunjukkan cara membandingkan dua file PDF menggunakan Aspose.Pdf untuk .NET sambil mengabaikan konten anotasi apa pun. Ia mengekstrak kotak pembatas semua anotasi dari setiap dokumen, memasukkan wilayah tersebut ke SideBySideComparisonOptions, dan kemudian menjalankan perbandingan berdampingan. Hasilnya adalah PDF diff yang menyoroti hanya perubahan non-anotasi.

---

{{< tutorial-widget sourcePath="pdf/net/forms-annotations/exclude-annotations" >}}


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

**Q: Apa yang terjadi jika halaman PDF tidak memiliki anotasi – apakah perbandingan tetap berfungsi?**  
A: Ya. Kode tersebut hanya tidak menambahkan persegi panjang apa pun ke daftar `ignoredRects` yang bersangkutan, sehingga `ExcludeAreas1`/`ExcludeAreas2` menerima array kosong dan pembanding memproses seluruh halaman.

**Q: Bisakah saya mengecualikan hanya anotasi dari satu dokumen sementara mempertahankan anotasi dokumen lain dalam diff?**  
A: Setel `ExcludeAreas1` (atau `ExcludeAreas2`) ke persegi panjang yang dikumpulkan dan biarkan properti lainnya sebagai array kosong; pembanding akan mengabaikan wilayah hanya pada dokumen yang ditentukan.

**Q: Apakah persegi panjang anotasi yang tumpang tindih menyebabkan masalah dengan `ExcludeAreas`?**  
A: Persegi panjang yang tumpang tindih digabungkan secara internal oleh pembanding, sehingga batas anotasi yang tumpang tindih dikecualikan dengan aman tanpa menghitung ganda.

**Q: Apakah ada cara untuk mengecualikan tabel selain anotasi menggunakan objek opsi yang sama?**  
A: Ya, setel `compareOpts.ExcludeTables = true;` – flag ini bekerja bersama `ExcludeAreas1`/`ExcludeAreas2` untuk mengabaikan wilayah tabel juga.

**Q: Bagaimana jika properti `Rect` dari anotasi bernilai null – apakah kode akan melempar pengecualian?**  
A: Kode memeriksa `if (a != null && a.Rect != null)` sebelum menambahkan ke daftar, sehingga persegi panjang null hanya dilewati dan tidak ada pengecualian yang dilempar.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}