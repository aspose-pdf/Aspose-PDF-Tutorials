---
category: general
date: 2026-06-18
description: Tambahkan kotak teks ke formulir PDF dengan cepat. Pelajari cara membuat
  kotak teks PDF yang dapat diisi dan cara menambahkan bidang komentar PDF menggunakan
  Aspose.PDF untuk .NET.
draft: false
keywords:
- add text box to pdf form
- create fillable pdf textbox
- how to add comment field pdf
language: id
og_description: Tambahkan kotak teks ke formulir PDF dengan Aspose.PDF untuk .NET.
  Tutorial ini menunjukkan cara membuat kotak teks PDF yang dapat diisi dan cara menambahkan
  bidang komentar PDF hanya dalam beberapa baris.
og_title: Tambahkan Kotak Teks ke Form PDF – Panduan Lengkap C#
schemas:
- author: Aspose
  dateModified: '2026-06-18'
  description: Add text box to PDF form quickly. Learn how to create fillable PDF
    textbox and how to add comment field PDF using Aspose.PDF for .NET.
  headline: Add Text Box to PDF Form – Complete C# Guide
  type: TechArticle
- description: Add text box to PDF form quickly. Learn how to create fillable PDF
    textbox and how to add comment field PDF using Aspose.PDF for .NET.
  name: Add Text Box to PDF Form – Complete C# Guide
  steps:
  - name: – Load the PDF document
    text: We need a `Document` object that represents the existing file. Aspose.PDF
      makes this a one‑liner.
  - name: – Create a TextBox field on the target page
    text: We’ll place the textbox on page 1 (index 0) inside a rectangle that defines
      its size and position. The rectangle uses points (1 inch = 72 points).
  - name: – Assign a name to the field
    text: Every form field needs a unique identifier. This name is what you’ll reference
      later when extracting data.
  - name: – Enable multiple widget annotations (optional but handy)
    text: If you want the same textbox to appear on several pages, set `MultipleWidgetAnnotations`
      to `true`. For a single‑page comment field you can skip this, but it doesn’t
      hurt.
  - name: – Add the TextBox field to the document’s form collection
    text: Now the field becomes part of the PDF’s interactive form.
  - name: – Save the modified PDF
    text: Finally, write the changes back to disk.
  - name: Can I set a default value?
    text: Yes. Just assign `textBox.Value = "Enter your comment here";` before adding
      the field.
  - name: What if I need a multiline textbox?
    text: 'Set the `IsMultiline` property:'
  - name: How do I change the appearance (border, background)?
    text: '```csharp textBox.BorderColor = Color.Black; textBox.BorderWidth = 1; textBox.BackgroundColor
      = Color.LightYellow; ```'
  - name: Does this work with PDF/A or encrypted PDFs?
    text: 'Aspose.PDF can handle PDF/A‑1b, PDF/A‑2b, and encrypted files as long as
      you provide the password when loading:'
  type: HowTo
tags:
- pdf
- csharp
- pdf-form
- textbox
- aspnet
title: Tambahkan Kotak Teks ke Formulir PDF – Panduan Lengkap C#
url: /id/net/programming-with-forms/add-text-box-to-pdf-form-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Menambahkan Kotak Teks ke Form PDF – Panduan Lengkap C#

Pernahkah Anda perlu **menambahkan kotak teks ke form PDF** tetapi tidak yakin panggilan API mana yang harus digunakan? Anda bukan satu-satunya. Baik Anda sedang membangun pengumpul umpan balik, portal penandatanganan kontrak, atau bidang komentar sederhana, kotak teks yang dapat diisi adalah solusi utama. Dalam panduan ini kami akan menjelaskan langkah‑langkah tepat untuk **membuat kotak teks PDF yang dapat diisi** dan juga menjawab pertanyaan umum **cara menambahkan bidang komentar PDF** menggunakan Aspose.PDF untuk .NET.

Kami akan memulai dengan PDF bersih, menambahkan kotak teks ke halaman 1, memberi nama yang ramah, mengaktifkan beberapa widget, dan akhirnya menyimpan hasilnya. Pada akhir tutorial Anda akan memiliki PDF siap pakai yang dapat dibuka siapa saja di Adobe Reader, mengetik komentar, dan menekan Simpan. Tanpa alat eksternal, tanpa penyuntingan manual—hanya kode C# murni.

## Prasyarat

- .NET 6.0 atau yang lebih baru (kode ini juga bekerja dengan .NET Framework 4.7+)
- Visual Studio 2022 atau IDE apa pun yang Anda sukai
- Paket NuGet Aspose.PDF untuk .NET (`Install-Package Aspose.PDF`)
- PDF sumber (`input.pdf`) yang terletak di folder yang Anda kontrol  

Itu saja. Jika Anda sudah memiliki semua itu, Anda siap memulai.

## Menambahkan Kotak Teks ke Form PDF dengan C#

Berikut adalah inti dari tutorial. Setiap langkah dijelaskan, kemudian potongan kode C# yang bersesuaian mengikuti. Silakan menyalin‑tempel seluruh blok ke dalam aplikasi konsol; kode tersebut dapat dikompilasi dan dijalankan apa adanya.

### Langkah 1 – Memuat dokumen PDF

Kita memerlukan objek `Document` yang mewakili file yang ada. Aspose.PDF membuat ini menjadi satu baris kode.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Forms;
using System.Drawing;

// Load the source PDF
Document doc = new Document(@"C:\MyPdfs\input.pdf");
```

*Mengapa ini penting:* Memuat PDF memberi kita akses ke halaman‑halamannya, anotasi, dan koleksi form tempat bidang‑bidang berada. Tanpa instance `Document` kita tidak dapat menambahkan apa pun.

### Langkah 2 – Membuat bidang TextBox pada halaman target

Kami akan menempatkan kotak teks pada halaman 1 (indeks 0) di dalam sebuah persegi panjang yang menentukan ukuran dan posisinya. Persegi panjang menggunakan satuan poin (1 inci = 72 poin).

```csharp
// Define the rectangle: left, bottom, right, top
Rectangle rect = new Rectangle(100, 600, 300, 630);

// Create the TextBox field on page 1
TextBoxField textBox = new TextBoxField(doc.Pages[1], rect);
```

*Mengapa ini penting:* Persegi panjang menentukan di mana pengguna akan melihat bidang tersebut. Sesuaikan koordinat untuk menyesuaikan tata letak Anda. Kelas `TextBoxField` secara otomatis mewarisi properti visual seperti batas dan latar belakang.

### Langkah 3 – Menetapkan nama pada bidang

Setiap bidang form memerlukan pengidentifikasi unik. Nama ini yang akan Anda gunakan nanti saat mengekstrak data.

```csharp
textBox.FieldName = "Comments";
```

*Mengapa ini penting:* Menamai bidang `"Comments"` memungkinkan Anda mengambil input pengguna dengan `doc.Form["Comments"]` setelah PDF diisi. Nama tersebut juga muncul dalam daftar bidang pembaca PDF.

### Langkah 4 – Mengaktifkan anotasi widget ganda (opsional namun berguna)

Jika Anda ingin kotak teks yang sama muncul di beberapa halaman, setel `MultipleWidgetAnnotations` ke `true`. Untuk bidang komentar satu halaman Anda dapat melewatkan ini, namun tidak ada salahnya.

```csharp
textBox.MultipleWidgetAnnotations = true;
```

*Mengapa ini penting:* Beberapa widget berbagi data yang sama, sehingga pengguna dapat mengetik sekali dan melihat komentar yang sama di setiap halaman yang berisi widget tersebut. Ini trik yang berguna untuk kontrak multi‑halaman.

### Langkah 5 – Menambahkan bidang TextBox ke koleksi form dokumen

Sekarang bidang tersebut menjadi bagian dari form interaktif PDF.

```csharp
doc.Form.Add(textBox);
```

*Mengapa ini penting:* Menambahkan bidang mendaftarkannya ke dalam kamus AcroForm PDF. Tanpa langkah ini kotak teks hanya ada di memori dan tidak pernah muncul di file yang disimpan.

### Langkah 6 – Menyimpan PDF yang telah dimodifikasi

Akhirnya, tulis perubahan kembali ke disk.

```csharp
doc.Save(@"C:\MyPdfs\output.pdf");
```

*Mengapa ini penting:* Menyimpan membuat bidang form baru menjadi permanen. Buka `output.pdf` di Adobe Reader dan Anda akan melihat kotak teks kosong berlabel “Comments” siap untuk diketik.

## Contoh Lengkap yang Berfungsi

Menggabungkan semuanya, berikut adalah aplikasi konsol mandiri yang dapat Anda jalankan langsung:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Forms;
using System.Drawing; // for Rectangle

namespace PdfFormDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the existing PDF
            string inputPath = @"C:\MyPdfs\input.pdf";
            Document doc = new Document(inputPath);

            // 2️⃣ Define the rectangle where the textbox will live
            Rectangle rect = new Rectangle(100, 600, 300, 630);

            // 3️⃣ Create the TextBox field on page 1 (index 1)
            TextBoxField textBox = new TextBoxField(doc.Pages[1], rect)
            {
                // 4️⃣ Give it a meaningful name
                FieldName = "Comments",

                // 5️⃣ Allow the same widget on multiple pages (optional)
                MultipleWidgetAnnotations = true
            };

            // 6️⃣ Add the field to the form collection
            doc.Form.Add(textBox);

            // 7️⃣ Save the updated PDF
            string outputPath = @"C:\MyPdfs\output.pdf";
            doc.Save(outputPath);

            Console.WriteLine("✅ Text box added successfully! Check " + outputPath);
        }
    }
}
```

**Output yang diharapkan:** Saat Anda membuka `output.pdf` Anda akan melihat area input berbentuk persegi panjang di halaman 1. Mengklik di dalamnya memungkinkan Anda mengetik komentar apa pun. Bidang tersebut tetap ada setelah disimpan, yang berarti Anda telah berhasil menjawab **cara menambahkan bidang komentar PDF**.

## Pertanyaan Umum & Kasus Tepi

### Bisakah saya menetapkan nilai default?

Ya. Cukup tetapkan `textBox.Value = "Enter your comment here";` sebelum menambahkan bidang.

### Bagaimana jika saya membutuhkan kotak teks multiline?

Setel properti `IsMultiline`:

```csharp
textBox.IsMultiline = true;
textBox.MaxLength = 500; // optional limit
```

### Bagaimana cara mengubah tampilan (batas, latar belakang)?

```csharp
textBox.BorderColor = Color.Black;
textBox.BorderWidth = 1;
textBox.BackgroundColor = Color.LightYellow;
```

### Apakah ini bekerja dengan PDF/A atau PDF terenkripsi?

Aspose.PDF dapat menangani PDF/A‑1b, PDF/A‑2b, dan file terenkripsi selama Anda menyediakan kata sandi saat memuat:

```csharp
Document doc = new Document(inputPath, new LoadOptions { Password = "secret" });
```

### Bagaimana jika saya membutuhkan kotak teks di halaman lain?

Ganti `doc.Pages[1]` dengan indeks halaman yang diinginkan (`doc.Pages[2]` untuk halaman 3, dll.). Ingat bahwa koleksi halaman **berbasis 1** di Aspose.PDF.

## Tips Pro

- **Tips pro:** Gunakan `doc.Form.RefreshAppearance();` setelah menambahkan beberapa bidang untuk memastikan semua widget ditampilkan dengan benar di penampil PDF lama.
- **Waspada:** Persegi panjang yang tumpang tindih. Jika dua bidang berbagi area yang sama, Acrobat dapat menyembunyikan salah satunya.
- **Catatan kinerja:** Saat memproses ribuan PDF, gunakan kembali satu instance `Document` untuk membaca dan hanya mengkloning bidang form untuk menghindari alokasi berulang.

## Langkah Selanjutnya

Sekarang Anda sudah tahu cara **menambahkan kotak teks ke form PDF**, Anda mungkin ingin menjelajahi topik terkait:

- **Buat kotak teks PDF yang dapat diisi** dengan aturan validasi (`textBox.Validate = new RegExValidator("[A-Za-z0-9]+");`)
- **Tambahkan tombol radio atau kotak centang** untuk membangun kuesioner lengkap
- **Flatten form** setelah pengiriman untuk mencegah pengeditan lebih lanjut (`doc.Form.Flatten();`)
- **Ekstrak data yang dimasukkan** menggunakan `doc.Form["Comments"].Value` dan simpan ke basis data

Semua ini dibangun di atas konsep inti yang telah kami bahas, sehingga Anda berada pada posisi yang tepat untuk memperluas toolkit otomatisasi PDF Anda.

---

*Selamat coding! Jika Anda mengalami kendala, tinggalkan komentar di bawah dan kami akan membantu memecahkan bersama.*

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang dibangun di atas teknik yang ditunjukkan dalam panduan ini. Setiap sumber daya menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Cara Menambahkan Bidang TextBox dalam PDF Menggunakan Aspose.PDF untuk .NET: Panduan Langkah demi Langkah](/pdf/english/net/forms-annotations/add-textbox-field-aspose-pdf-net/)
- [Cara Menambahkan dan Mengekstrak Bidang Form PDF Menggunakan Aspose.PDF untuk .NET: Panduan Komprehensif](/pdf/english/net/forms-annotations/manage-pdf-form-fields-aspose-dotnet/)
- [Cara Menambahkan Tooltip ke Teks PDF Menggunakan Aspose.PDF untuk .NET (Form & Anotasi)](/pdf/english/net/forms-annotations/aspose-pdf-net-add-tooltips-pdfs/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}