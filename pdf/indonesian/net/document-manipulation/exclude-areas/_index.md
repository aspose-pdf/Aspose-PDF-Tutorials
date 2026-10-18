---
title: Bandingkan PDF sambil Mengabaikan Area Spesifik menggunakan Aspose.Pdf untuk .NET
weight: 201
limit:
description: Pelajari cara membandingkan PDF berdampingan dan mengabaikan wilayah yang dipilih menggunakan Aspose.Pdf untuk .NET.
keywords: [Aspose.Pdf for .NET, pdf comparison, exclude areas pdf, ignore regions pdf diff, side-by-side pdf comparison, pdf diff highlighting]
url: /net/document-manipulation/exclude-areas/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Pelajari cara membandingkan PDF berdampingan dan mengabaikan wilayah
    yang dipilih menggunakan Aspose.Pdf untuk .NET.
  headline: Bandingkan PDF sambil Mengabaikan Area Spesifik menggunakan Aspose.Pdf
    untuk .NET
  type: TechArticle
- description: Pelajari cara membandingkan PDF berdampingan dan mengabaikan wilayah
    yang dipilih menggunakan Aspose.Pdf untuk .NET.
  name: Bandingkan PDF sambil Mengabaikan Area Spesifik menggunakan Aspose.Pdf untuk
    .NET
  steps:
  - name: Tentukan jalur file untuk dua PDF sumber dan PDF diff output.
    text: Tentukan jalur file untuk dua PDF sumber dan PDF diff output.
  - name: Periksa bahwa kedua file PDF sumber ada dan batalkan dengan pesan error
      jika salah satunya tidak ada.
    text: Periksa bahwa kedua file PDF sumber ada dan batalkan dengan pesan error
      jika salah satunya tidak ada.
  - name: Buat sebuah array yang berisi area persegi panjang yang akan diabaikan pada
      PDF pertama.
    text: Buat sebuah array yang berisi area persegi panjang yang akan diabaikan pada
      PDF pertama.
  - name: Buat sebuah array yang berisi area persegi panjang yang akan diabaikan pada
      PDF kedua.
    text: Buat sebuah array yang berisi area persegi panjang yang akan diabaikan pada
      PDF kedua.
  - name: Konfigurasikan perbandingan berdampingan, dengan menetapkan array area yang
      diabaikan ke properti yang sesuai.
    text: Konfigurasikan perbandingan berdampingan, dengan menetapkan array area yang
      diabaikan ke properti yang sesuai.
  - name: Muat kedua PDF dan jalankan perbandingan berdampingan, menghasilkan file
      diff pada jalur yang ditentukan.
    text: Muat kedua PDF dan jalankan perbandingan berdampingan, menghasilkan file
      diff pada jalur yang ditentukan.
  - name: Cetak pesan konfirmasi yang menunjukkan bahwa perbandingan telah selesai
      dan di mana PDF diff disimpan.
    text: Cetak pesan konfirmasi yang menunjukkan bahwa perbandingan telah selesai
      dan di mana PDF diff disimpan.
  type: HowTo
- questions:
  - answer: Koordinat berada dalam satuan point (1/72 inci) dengan asal di sudut kiri‑bawah
      halaman, sehingga dua angka pertama adalah X/Y kiri‑bawah dan dua angka terakhir
      adalah X/Y kanan‑atas.
    question: Sistem koordinat apa yang digunakan nilai `Rectangle` saat mendefinisikan
      zona yang diabaikan?
  - answer: Ya – berikan beberapa objek `Aspose.Pdf.Rectangle` dalam array `ExcludeAreas1`
      (atau `ExcludeAreas2`); setiap persegi panjang akan dikecualikan secara independen
      selama perbandingan.
    question: Bisakah saya mengabaikan lebih dari satu area persegi panjang dalam
      dokumen yang sama?
  - answer: Tidak. `ExcludeAreas1` berlaku untuk PDF pertama dan `ExcludeAreas2` untuk
      PDF kedua, sehingga Anda dapat menentukan koordinat yang berbeda untuk masing‑masing
      dokumen.
    question: Apakah persegi panjang yang diabaikan harus identik di kedua PDF?
  - answer: Aspose.Pdf secara diam-diam mengabaikan persegi panjang yang berada sepenuhnya
      di luar halaman; mereka tidak berpengaruh pada hasil perbandingan.
    question: Apa yang terjadi jika sebuah persegi panjang didefinisikan di luar batas
      halaman?
  - answer: Array `ExcludeAreas` berlaku per halaman, jadi Anda perlu menambahkan
      `Rectangle` yang sama ke koleksi setiap halaman (misalnya, loop melalui `pdf.Pages`
      dan tetapkan array) sebelum memanggil `SideBySidePdfComparer.Compare`.
    question: Bagaimana saya dapat mengecualikan wilayah yang sama pada setiap halaman
      PDF?
  type: FAQPage
images:
- /net/document-manipulation/exclude-areas/og-image.png
og_title: Abaikan Wilayah saat Membandingkan PDF
og_description: Lihat cara melewatkan area yang dipilih dalam perbandingan PDF berdampingan dan mendapatkan PDF diff yang bersih.
og_image_alt: Panduan yang menunjukkan perbandingan PDF berdampingan dengan wilayah persegi panjang yang dikecualikan menggunakan Aspose.Pdf untuk .NET
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Bandingkan PDF sambil Mengabaikan Area Spesifik menggunakan Aspose.Pdf untuk .NET
Tutorial ini menunjukkan cara membandingkan dua dokumen PDF berdampingan dengan Aspose.Pdf untuk .NET sambil mengecualikan wilayah persegi panjang yang ditentukan dari analisis. Dengan mendefinisikan area yang dikecualikan di setiap file, PDF diff yang dihasilkan menyoroti hanya perubahan yang penting, sehingga lebih mudah fokus pada perbedaan yang relevan.

---

{{< tutorial-widget sourcePath="pdf/net/document-manipulation/exclude-areas" >}}


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

**Q: Sistem koordinat apa yang digunakan nilai `Rectangle` saat mendefinisikan zona yang diabaikan?**  
A: Koordinat berada dalam satuan point (1/72 inci) dengan asal di sudut kiri‑bawah halaman, sehingga dua angka pertama adalah X/Y kiri‑bawah dan dua angka terakhir adalah X/Y kanan‑atas.

**Q: Bisakah saya mengabaikan lebih dari satu area persegi panjang dalam dokumen yang sama?**  
A: Ya – berikan beberapa objek `Aspose.Pdf.Rectangle` dalam array `ExcludeAreas1` (atau `ExcludeAreas2`); setiap persegi panjang akan dikecualikan secara independen selama perbandingan.

**Q: Apakah persegi panjang yang diabaikan harus identik di kedua PDF?**  
A: Tidak. `ExcludeAreas1` berlaku untuk PDF pertama dan `ExcludeAreas2` untuk PDF kedua, sehingga Anda dapat menentukan koordinat yang berbeda untuk masing‑masing dokumen.

**Q: Apa yang terjadi jika sebuah persegi panjang didefinisikan di luar batas halaman?**  
A: Aspose.Pdf secara diam-diam mengabaikan persegi panjang yang berada sepenuhnya di luar halaman; mereka tidak berpengaruh pada hasil perbandingan.

**Q: Bagaimana saya dapat mengecualikan wilayah yang sama pada setiap halaman PDF?**  
A: Array `ExcludeAreas` berlaku per halaman, jadi Anda perlu menambahkan `Rectangle` yang sama ke koleksi setiap halaman (misalnya, loop melalui `pdf.Pages` dan tetapkan array) sebelum memanggil `SideBySidePdfComparer.Compare`.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}