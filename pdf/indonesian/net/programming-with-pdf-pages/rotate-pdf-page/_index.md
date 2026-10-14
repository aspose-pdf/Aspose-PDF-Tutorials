---
title: Putar Satu Halaman PDF 180 Derajat dengan Aspose.PDF for .NET
weight: 260
limit:
description: Pelajari cara memutar halaman ketiga PDF 180° menggunakan Aspose.PDF for .NET.
keywords: [rotate pdf page, Aspose.PDF for .NET, PDF page rotation .NET, rotate third page pdf, PDF SDK rotate page]
url: /net/programming-with-pdf-pages/rotate-pdf-page/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Pelajari cara memutar halaman ketiga PDF 180° menggunakan Aspose.PDF
    for .NET.
  headline: Putar Satu Halaman PDF 180 Derajat dengan Aspose.PDF for .NET
  type: TechArticle
- description: Pelajari cara memutar halaman ketiga PDF 180° menggunakan Aspose.PDF
    for .NET.
  name: Putar Satu Halaman PDF 180 Derajat dengan Aspose.PDF for .NET
  steps:
  - name: File ini hanya berisi komentar penjelas dan tidak ada kode yang dapat dijalankan,
      berfungsi sebagai placeholder untuk contoh asli.
    text: File ini hanya berisi komentar penjelas dan tidak ada kode yang dapat dijalankan,
      berfungsi sebagai placeholder untuk contoh asli.
  type: HowTo
- questions:
  - answer: Gunakan koleksi halaman SDK dengan indeks berbasis nol, misalnya `pdfDocument.Pages[2]`,
      karena indeks 2 mengacu pada halaman ketiga.
    question: Bagaimana cara menargetkan halaman ketiga PDF untuk rotasi?
  - answer: Properti rotasi hanya menerima empat nilai standar 0, 90, 180, dan 270
      derajat; nilai lain akan dibulatkan ke sudut terdekat yang diizinkan.
    question: Apakah saya dapat memutar halaman dengan sudut selain 180 derajat?
  - answer: Rotasi hanya diterapkan pada `PdfDocument` dalam memori; Anda harus memanggil
      `pdfDocument.Save(\"output.pdf\")` (atau metode simpan serupa) untuk menulis
      perubahan ke file baru, sehingga sumber tetap tidak berubah.
    question: Apakah memutar halaman secara otomatis mengubah file asli?
  - answer: SDK secara otomatis menghitung ulang posisi anotasi dan bidang formulir
      sehingga tetap teralign dengan benar pada orientasi baru.
    question: Apa yang terjadi pada anotasi atau bidang formulir setelah halaman diputar?
  type: FAQPage
images:
- /net/programming-with-pdf-pages/rotate-pdf-page/og-image.png
og_title: Putar Halaman PDF 180° dengan Aspose.PDF
og_description: Dengan cepat balikkan halaman ketiga PDF Anda terbalik dengan beberapa baris kode Aspose.PDF for .NET.
og_image_alt: Panduan yang menampilkan kode yang memutar halaman ketiga PDF 180 derajat menggunakan Aspose.PDF for .NET.
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Putar Satu Halaman PDF 180 Derajat dengan Aspose.PDF
Dalam tutorial ini Anda akan belajar cara memutar halaman ketiga dari dokumen PDF sebesar 180 derajat menggunakan Aspose.PDF for .NET. Contoh ini menjelaskan cara memuat PDF, memilih halaman 3, menerapkan rotasi, dan menyimpan file yang telah diperbarui. Pendekatan ini memungkinkan Anda membalik satu halaman tertentu tanpa mengubah orientasi halaman lainnya.

---

{{< tutorial-widget sourcePath="pdf/net/programming-with-pdf-pages/rotate-pdf-page" >}}


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

**Q: Bagaimana cara menargetkan halaman ketiga PDF untuk rotasi?**  
A: Gunakan koleksi halaman SDK dengan indeks berbasis nol, misalnya `pdfDocument.Pages[2]`, karena indeks 2 mengacu pada halaman ketiga.

**Q: Apakah saya dapat memutar halaman dengan sudut selain 180 derajat?**  
A: Properti rotasi hanya menerima empat nilai standar 0, 90, 180, dan 270 derajat; nilai lain akan dibulatkan ke sudut terdekat yang diizinkan.

**Q: Apakah memutar halaman secara otomatis mengubah file asli?**  
A: Rotasi hanya diterapkan pada `PdfDocument` dalam memori; Anda harus memanggil `pdfDocument.Save(\"output.pdf\")` (atau metode simpan serupa) untuk menulis perubahan ke file baru, sehingga sumber tetap tidak berubah.

**Q: Apa yang terjadi pada anotasi atau bidang formulir setelah halaman diputar?**  
A: SDK secara otomatis menghitung ulang posisi anotasi dan bidang formulir sehingga tetap teralign dengan benar pada orientasi baru.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}