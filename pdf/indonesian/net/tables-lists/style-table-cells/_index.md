---
title: Sesuaikan Latar Belakang, Border, dan Padding Sel Tabel dalam PDF dengan Aspose.Pdf untuk .NET
weight: 101
limit:
description: Pelajari cara membuat PDF dengan tabel dua kolom dan menerapkan warna latar belakang, border, serta padding khusus pada setiap sel menggunakan Aspose.Pdf untuk .NET.
keywords: [Aspose.Pdf for .NET, style table cells pdf, pdf table cell background, pdf table cell border, pdf cell padding, Aspose PDF table styling]
url: /net/tables-lists/style-table-cells/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Pelajari cara membuat PDF dengan tabel dua kolom dan menerapkan warna
    latar belakang, border, serta padding khusus pada setiap sel menggunakan Aspose.Pdf
    untuk .NET.
  headline: Sesuaikan Latar Belakang, Border, dan Padding Sel Tabel dalam PDF dengan
    Aspose.Pdf untuk .NET
  type: TechArticle
- description: Pelajari cara membuat PDF dengan tabel dua kolom dan menerapkan warna
    latar belakang, border, serta padding khusus pada setiap sel menggunakan Aspose.Pdf
    untuk .NET.
  name: Sesuaikan Latar Belakang, Border, dan Padding Sel Tabel dalam PDF dengan Aspose.Pdf
    untuk .NET
  steps:
  - name: Buat dokumen PDF kosong baru di dalam blok using.
    text: Buat dokumen PDF kosong baru di dalam blok using.
  - name: Tambahkan halaman kosong ke dokumen PDF.
    text: Tambahkan halaman kosong ke dokumen PDF.
  - name: Buat objek Table dengan dua kolom masing‑masing 200 poin, border luar tipis
      berwarna hitam, dan padding sel default sebesar 5 poin.
    text: Buat objek Table dengan dua kolom masing‑masing 200 poin, border luar tipis
      berwarna hitam, dan padding sel default sebesar 5 poin.
  - name: Tambahkan baris pertama ke tabel.
    text: Tambahkan baris pertama ke tabel.
  - name: Buat sel pertama, sisipkan teks "First cell", atur latar belakang kuning
      muda, border merah 2 poin, dan margin 4 poin.
    text: Buat sel pertama, sisipkan teks "First cell", atur latar belakang kuning
      muda, border merah 2 poin, dan margin 4 poin.
  - name: Buat sel kedua, tambahkan teks "Second cell", beri latar belakang hijau
      muda, border biru 2 poin, dan margin 4 poin.
    text: Buat sel kedua, tambahkan teks "Second cell", beri latar belakang hijau
      muda, border biru 2 poin, dan margin 4 poin.
  - name: Tambahkan baris kedua ke tabel.
    text: Tambahkan baris kedua ke tabel.
  - name: Buat sel ketiga, sisipkan "Third cell", atur latar belakang sian muda, border
      abu‑gelap 2 poin, dan margin 4 poin.
    text: Buat sel ketiga, sisipkan "Third cell", atur latar belakang sian muda, border
      abu‑gelap 2 poin, dan margin 4 poin.
  - name: Buat sel keempat, tambahkan "Fourth cell", beri latar belakang merah muda
      muda, border ungu 2 poin, dan margin 4 poin.
    text: Buat sel keempat, tambahkan "Fourth cell", beri latar belakang merah muda
      muda, border ungu 2 poin, dan margin 4 poin.
  - name: Tambahkan tabel yang sudah ditata sepenuhnya ke halaman agar terlihat dalam
      PDF.
    text: Tambahkan tabel yang sudah ditata sepenuhnya ke halaman agar terlihat dalam
      PDF.
  - name: Simpan dokumen PDF ke file dan tutup blok using.
    text: Simpan dokumen PDF ke file dan tutup blok using.
  - name: Cetak pesan konfirmasi ke konsol.
    text: Cetak pesan konfirmasi ke konsol.
  type: HowTo
- questions:
  - answer: '`DefaultCellPadding` menyediakan padding dasar untuk setiap sel, tetapi
      jika Anda menetapkan `Margin` (mis., `cellA1.Margin = new MarginInfo(...)`)
      nilai margin akan menggantikan padding default untuk sel tersebut.'
    question: Apakah `DefaultCellPadding` yang diatur pada `Table` memengaruhi sel
      yang juga memiliki `Margin` yang didefinisikan?
  - answer: Tanpa `Table.Border`, persegi panjang luar di sekitar seluruh tabel tidak
      ditampilkan; hanya border sel individual yang Anda atur (mis., `cellA2.Border`)
      yang akan terlihat.
    question: Apa yang akan terlihat pada PDF jika saya menghapus properti `Border`
      dari objek `Table`?
  - answer: Ya, buat `BorderInfo` dengan `BorderSide` tertentu (mis., `new BorderInfo(BorderSide.Left,
      3, Aspose.Pdf.Color.Black)`) dan tetapkan ke properti `Border` sel.
    question: Apakah saya dapat memberi sel lebar border yang berbeda pada setiap
      sisinya?
  - answer: Buat instance `Row` baru dengan `Row newRow = dataTable.Rows.Add();` lalu
      tambahkan sel ke `newRow.Cells` seperti pada baris sebelumnya.
    question: Bagaimana cara menambahkan baris ketiga ke tabel setelah kode yang ditampilkan?
  type: FAQPage
images:
- /net/tables-lists/style-table-cells/og-image.png
og_title: Penataan Sel Tabel PDF – Latar Belakang, Border, Padding
og_description: Format sel tabel dalam PDF dengan cepat menggunakan warna, border, dan spasi khusus dengan Aspose.Pdf untuk .NET.
og_image_alt: Panduan yang menunjukkan cara menata warna latar belakang, border, dan padding sel tabel dalam PDF menggunakan Aspose.Pdf untuk .NET
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Sesuaikan Latar Belakang, Border, dan Padding Sel Tabel dalam PDF dengan Aspose.Pdf untuk .NET
Pada tutorial ini Anda akan melihat cara menghasilkan dokumen PDF, menambahkan tabel dua kolom, dan mengontrol tampilan setiap sel secara tepat. Dengan mengatur warna latar belakang, mendefinisikan border, dan menyesuaikan padding, Anda dapat membuat data tabel menonjol dan tampak rapi. Contoh ini menggunakan kelas Aspose.Pdf Document dan Table untuk mendemonstrasikan setiap opsi penataan.

---

{{< tutorial-widget sourcePath="pdf/net/tables-lists/style-table-cells" >}}


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

**Q: Apakah `DefaultCellPadding` yang diatur pada `Table` memengaruhi sel yang juga memiliki `Margin` yang didefinisikan?**  
A: `DefaultCellPadding` menyediakan padding dasar untuk setiap sel, tetapi jika Anda menetapkan `Margin` (mis., `cellA1.Margin = new MarginInfo(...)`) nilai margin akan menggantikan padding default untuk sel tersebut.

**Q: Apa yang akan terlihat pada PDF jika saya menghapus properti `Border` dari objek `Table`?**  
A: Tanpa `Table.Border`, persegi panjang luar di sekitar seluruh tabel tidak ditampilkan; hanya border sel individual yang Anda atur (mis., `cellA2.Border`) yang akan terlihat.

**Q: Apakah saya dapat memberi sel lebar border yang berbeda pada setiap sisinya?**  
A: Ya, buat `BorderInfo` dengan `BorderSide` tertentu (mis., `new BorderInfo(BorderSide.Left, 3, Aspose.Pdf.Color.Black)`) dan tetapkan ke properti `Border` sel.

**Q: Bagaimana cara menambahkan baris ketiga ke tabel setelah kode yang ditampilkan?**  
A: Buat instance `Row` baru dengan `Row newRow = dataTable.Rows.Add();` lalu tambahkan sel ke `newRow.Cells` seperti pada baris sebelumnya.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}