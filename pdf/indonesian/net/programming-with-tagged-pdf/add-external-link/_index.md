---
title: Tambahkan Tagged External Link dengan Tooltip ke PDF Menggunakan Aspose.Pdf for .NET
weight: 440
limit:
description: Pelajari cara menambahkan hyperlink eksternal yang ditandai dengan teks tampilan dan tooltip ke PDF menggunakan Aspose.Pdf for .NET.
keywords: [Aspose.Pdf for .NET, add external link pdf, tagged pdf hyperlink, pdf tooltip title, pdf logical structure, c# pdf hyperlink]
url: /net/programming-with-tagged-pdf/add-external-link/
date: '2026-09-29'
lastmod: '2026-09-29'
schemas:
- author: Aspose
  dateModified: '2026-09-29'
  description: Pelajari cara menambahkan hyperlink eksternal yang ditandai dengan
    teks tampilan dan tooltip ke PDF menggunakan Aspose.Pdf for .NET.
  headline: Tambahkan Tagged External Link dengan Tooltip ke PDF Menggunakan Aspose.Pdf
    for .NET
  type: TechArticle
- description: Pelajari cara menambahkan hyperlink eksternal yang ditandai dengan
    teks tampilan dan tooltip ke PDF menggunakan Aspose.Pdf for .NET.
  name: Tambahkan Tagged External Link dengan Tooltip ke PDF Menggunakan Aspose.Pdf
    for .NET
  steps:
  - name: Definisikan jalur untuk PDF sumber dan file hasil.
    text: Definisikan jalur untuk PDF sumber dan file hasil.
  - name: Periksa apakah PDF sumber ada dan batalkan jika tidak dapat ditemukan.
    text: Periksa apakah PDF sumber ada dan batalkan jika tidak dapat ditemukan.
  - name: Buka dokumen PDF di dalam blok using untuk memastikan pembuangan yang tepat.
    text: Buka dokumen PDF di dalam blok using untuk memastikan pembuangan yang tepat.
  - name: Dapatkan manager konten bertag untuk dokumen yang dibuka.
    text: Dapatkan manager konten bertag untuk dokumen yang dibuka.
  - name: Setel bahasa dokumen ke English (US) dan beri PDF judul yang diambil dari
      nama file.
    text: Setel bahasa dokumen ke English (US) dan beri PDF judul yang diambil dari
      nama file.
  - name: Ambil elemen root dari pohon struktur logis tempat elemen baru akan ditambahkan.
    text: Ambil elemen root dari pohon struktur logis tempat elemen baru akan ditambahkan.
  - name: Buat elemen link, atur teks tampilan, URL target, dan judul tooltip, lalu
      sisipkan ke dalam struktur dokumen.
    text: Buat elemen link, atur teks tampilan, URL target, dan judul tooltip, lalu
      sisipkan ke dalam struktur dokumen.
  - name: Simpan PDF yang diperbarui ke file hasil yang ditentukan.
    text: Simpan PDF yang diperbarui ke file hasil yang ditentukan.
  - name: Tampilkan pesan konfirmasi yang menunjukkan di mana PDF yang dimodifikasi
      disimpan.
    text: Tampilkan pesan konfirmasi yang menunjukkan di mana PDF yang dimodifikasi
      disimpan.
  type: HowTo
- questions:
  - answer: '`pdfDoc.TaggedContent` mengembalikan konten bertag yang ada jika dokumen
      sudah ditandai; tidak membuat pohon duplikat.'
    question: Bagaimana jika PDF sumber sudah ditandai – apakah memanggil `pdfDoc.TaggedContent`
      akan membuat pohon tag baru atau menggunakan yang sudah ada?
  - answer: Ya – temukan `StructureElement` yang diinginkan (misalnya `Div` atau `Paragraph`
      pada halaman) melalui pohon struktur logis dan panggil `AppendChild(externalLink)`
      pada elemen tersebut.
    question: Bisakah saya menempatkan hyperlink pada halaman tertentu alih-alih menambahkannya
      ke elemen root?
  - answer: Tooltip hanya ditampilkan jika `externalLink.Title` diatur sebelum `pdfDoc.Save`;
      mengaturnya setelah penyimpanan tidak berpengaruh pada PDF yang sudah ditulis.
    question: Apakah properti `Title` dari `LinkElement` diperlukan agar tooltip muncul,
      dan dapatkah itu diatur setelah memanggil `Save`?
  - answer: Tetapkan `FileSpecification` (misalnya `new FileSpecification("file:///C:/Docs/manual.pdf")`)
      ke `externalLink.Hyperlink` alih-alih menggunakan `WebHyperlink`.
    question: Bagaimana cara membuat link ke file lokal alih-alih URL web?
  type: FAQPage
images:
- /net/programming-with-tagged-pdf/add-external-link/og-image.png
og_title: Sisipkan Tagged External Link dengan Tooltip dalam PDF
og_description: Sematkan hyperlink yang dapat diakses dengan teks yang terlihat dan tooltip ke dalam PDF Anda menggunakan Aspose.Pdf for .NET.
og_image_alt: Panduan yang menunjukkan cara menambahkan hyperlink eksternal yang ditandai dengan tooltip ke PDF menggunakan Aspose.Pdf for .NET
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Tambahkan Tagged External Link dengan Tooltip ke PDF Menggunakan Aspose.Pdf
Tutorial ini menunjukkan cara membuka PDF yang sudah ada dengan Aspose.Pdf for .NET, membuat hyperlink eksternal yang ditandai yang mencakup teks tampilan yang terlihat dan judul tooltip, menyisipkan link ke dalam struktur logis dokumen, dan menyimpan file yang diperbarui. Dengan mengikuti langkah‑langkah tersebut Anda akan menghasilkan PDF yang dapat diakses di mana link menjadi bagian dari hierarki tag dan memberikan konteks tambahan bagi pembaca.

---

{{< tutorial-widget sourcePath="pdf/net/programming-with-tagged-pdf/add-external-link" >}}


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

**Q: Bagaimana jika PDF sumber sudah ditandai – apakah memanggil `pdfDoc.TaggedContent` akan membuat pohon tag baru atau menggunakan yang sudah ada?**  
A: `pdfDoc.TaggedContent` mengembalikan konten bertag yang ada jika dokumen sudah ditandai; tidak membuat pohon duplikat.

**Q: Bisakah saya menempatkan hyperlink pada halaman tertentu alih-alih menambahkannya ke elemen root?**  
A: Ya – temukan `StructureElement` yang diinginkan (misalnya `Div` atau `Paragraph` pada halaman) melalui pohon struktur logis dan panggil `AppendChild(externalLink)` pada elemen tersebut.

**Q: Apakah properti `Title` dari `LinkElement` diperlukan agar tooltip muncul, dan dapatkah itu diatur setelah memanggil `Save`?**  
A: Tooltip hanya ditampilkan jika `externalLink.Title` diatur sebelum `pdfDoc.Save`; mengaturnya setelah penyimpanan tidak berpengaruh pada PDF yang sudah ditulis.

**Q: Bagaimana cara membuat link ke file lokal alih-alih URL web?**  
A: Tetapkan `FileSpecification` (misalnya `new FileSpecification("file:///C:/Docs/manual.pdf")`) ke `externalLink.Hyperlink` alih-alih menggunakan `WebHyperlink`.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}