---
category: general
date: 2026-08-14
description: Buat bidang formulir PDF dengan cepat menggunakan C#. Pelajari cara menambahkan
  kotak teks ke PDF dan memodifikasi PDF untuk menyertakan kotak teks menggunakan
  Aspose.PDF.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create pdf form field
- add text box to pdf
- modify pdf to include text box
- Aspose.PDF form field
- C# PDF manipulation
language: id
lastmod: 2026-08-14
og_description: Buat bidang formulir PDF dengan C#. Tutorial ini menunjukkan cara
  menambahkan kotak teks ke PDF dan memodifikasi PDF untuk menyertakan kotak teks
  menggunakan Aspose.PDF.
og_image_alt: Screenshot of a PDF page showing a newly added text box form field
og_title: Buat bidang formulir PDF di C# – panduan pemrograman lengkap
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: Create pdf form field quickly with C#. Learn how to add text box to
    pdf and modify pdf to include text box using Aspose.PDF.
  headline: Create pdf form field in C# – step‑by‑step guide
  type: TechArticle
- description: Create pdf form field quickly with C#. Learn how to add text box to
    pdf and modify pdf to include text box using Aspose.PDF.
  name: Create pdf form field in C# – step‑by‑step guide
  steps:
  - name: Load the existing PDF document.
    text: Load the existing PDF document.
  - name: Instantiate a `TextBoxField` and configure its name and appearance.
    text: Instantiate a `TextBoxField` and configure its name and appearance.
  - name: Add a widget annotation that defines the visual rectangle on the target
      page.
    text: Add a widget annotation that defines the visual rectangle on the target
      page.
  - name: Insert the field into the document’s form collection.
    text: Insert the field into the document’s form collection.
  - name: Save the modified PDF.
    text: Save the modified PDF.
  - name: Open `output.pdf` in Adobe Acrobat Reader.
    text: Open `output.pdf` in Adobe Acrobat Reader.
  - name: Click inside the “Comments” box; the cursor should appear.
    text: Click inside the “Comments” box; the cursor should appear.
  - name: Type any text and press **Tab** or click elsewhere.
    text: Type any text and press **Tab** or click elsewhere.
  - name: Choose **File → Save As** to persist the entered value.
    text: Choose **File → Save As** to persist the entered value.
  - name: '(Optional) Use Aspose.PDF’s `Form` API to extract the value programmatically:'
    text: '(Optional) Use Aspose.PDF’s `Form` API to extract the value programmatically:'
  type: HowTo
tags:
- pdf
- csharp
- form-fields
title: Buat bidang formulir PDF di C# – panduan langkah demi langkah
url: /id/net/programming-with-forms/create-pdf-form-field-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat bidang formulir pdf di C# – panduan langkah‑demi‑langkah

Jika Anda perlu **create pdf form field** dalam sebuah dokumen, panduan ini akan memandu Anda melalui seluruh proses. Anda akan melihat secara tepat cara **add text box to pdf** pada halaman, dan cara **modify pdf to include text box** menggunakan pustaka Aspose.PDF untuk .NET.

Bekerja dengan formulir PDF adalah kebutuhan umum untuk sistem penagihan, survei, atau alur kerja apa pun yang mengumpulkan masukan pengguna. Pada akhir tutorial ini Anda akan memiliki potongan kode yang dapat digunakan kembali yang membuat bidang kotak teks yang berfungsi penuh, menempatkannya di lokasi yang Anda inginkan, dan menyimpan PDF yang telah diperbarui—semua tanpa meninggalkan proyek C# Anda.

## Prasyarat

Sebelum Anda memulai, pastikan Anda memiliki:

* .NET 6.0 atau yang lebih baru (kode ini juga berfungsi dengan .NET Framework 4.7+)
* Visual Studio 2022 atau IDE apa pun yang mendukung C#
* Lisensi aktif Aspose.PDF untuk .NET (versi percobaan gratis dapat digunakan untuk pengembangan)
* File PDF bernama `input.pdf` yang ditempatkan di direktori yang diketahui (tutorial ini menggunakan `YOUR_DIRECTORY` sebagai placeholder)

> **Pro tip:** Jika Anda belum memiliki lisensi, Anda dapat meminta kunci sementara dari situs web Aspose; pustaka ini berfungsi dalam mode evaluasi tanpa perubahan kode.

## Cara membuat bidang formulir pdf di C# (ikhtisar)

1. Muat dokumen PDF yang sudah ada.  
2. Buat instance `TextBoxField` dan konfigurasikan nama serta tampilannya.  
3. Tambahkan anotasi widget yang menentukan persegi visual pada halaman target.  
4. Sisipkan bidang ke dalam koleksi formulir dokumen.  
5. Simpan PDF yang telah dimodifikasi.

Setiap langkah dijelaskan secara detail di bawah ini, dengan contoh kode lengkap dan penjelasan di balik pemanggilan API.

## Langkah 1: Muat dokumen PDF

Operasi pertama adalah membaca PDF sumber. Aspose.PDF merepresentasikan file PDF dengan kelas `Document`. Memuat dokumen memberi Anda akses ke halaman‑halamannya, koleksi formulir, dan struktur lainnya.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using Aspose.Pdf.Text;

// Adjust the path to match your environment
string inputPath = Path.Combine("YOUR_DIRECTORY", "input.pdf");

// Load the PDF you want to modify
Document pdfDocument = new Document(inputPath);
```

**Mengapa ini penting:**  
Memuat file membuat model PDF dalam memori, memungkinkan Anda menambah, menghapus, atau mengedit objek tanpa merusak file asli. Objek `Document` juga menyediakan properti `Form`, yang nantinya akan Anda gunakan untuk **add text box to pdf**.

## Langkah 2: Buat bidang kotak teks

Bidang kotak teks adalah jenis bidang formulir yang memungkinkan pengguna mengetik teks bebas. Di Aspose.PDF Anda membuatnya dengan menginstansiasi `TextBoxField`, memberikan halaman target dan persegi yang mendefinisikan ukuran awal widget.

```csharp
// Choose the page index (0‑based). Here we use page 2 (index 1).
Page targetPage = pdfDocument.Pages[1];

// Define the rectangle for the field’s *initial* size.
// Rectangle(left, bottom, right, top) – values are in points (1/72 inch).
Rectangle fieldRect = new Rectangle(100, 500, 200, 530);

// Create the TextBoxField with a partial name that will be used in form data.
TextBoxField textBox = new TextBoxField(targetPage, fieldRect)
{
    PartialName = "Comments", // This identifier appears in the PDF form data.
    // Optional: set default appearance (font, size, color)
    DefaultAppearance = new DefaultAppearance(FontRepository.FindFont("Helvetica"), 12, Color.Black)
};
```

**Mengapa ini penting:**  
* `PartialName` adalah kunci yang digunakan alat pemrosesan formulir (misalnya Adobe Acrobat, parser sisi‑server) untuk mengambil nilai yang dimasukkan.  
* Persegi yang Anda berikan di sini hanya menentukan ukuran *awal* widget; Anda dapat menyesuaikan lokasinya secara visual dengan anotasi widget (langkah berikutnya).  
* Menetapkan `DefaultAppearance` memastikan teks di dalam kotak ditampilkan secara konsisten di semua penampil.

## Langkah 3: Definisikan anotasi widget visual

Sebuah bidang formulir dapat memiliki satu atau lebih **widget annotations** yang mengontrol di mana bidang muncul pada setiap halaman. Dengan menambahkan widget Anda dapat menempatkan bidang logis yang sama di lokasi berbeda atau bahkan pada beberapa halaman.

```csharp
// Define where the field will actually be displayed on the page.
// This rectangle can differ from the one used in the constructor.
Rectangle widgetRect = new Rectangle(100, 300, 200, 330);
textBox.AddWidgetAnnotation(widgetRect);
```

**Mengapa ini penting:**  
Persegi widget menentukan koordinat layar yang dilihat pengguna. Jika Anda melewatkan langkah ini, bidang mungkin ada dalam struktur data PDF tetapi tidak akan terlihat oleh pengguna akhir. Menambahkan widget adalah langkah yang benar‑benar **adds text box to pdf**.

## Langkah 4: Tambahkan bidang yang telah dikonfigurasi ke formulir dokumen

Setelah `TextBoxField` sepenuhnya dikonfigurasi, Anda perlu mendaftarkannya ke koleksi formulir PDF. Ini menjadikan bidang bagian dari formulir interaktif dan memastikan bidang tersebut disimpan.

```csharp
pdfDocument.Form.Add(textBox);
```

**Mengapa ini penting:**  
Tanpa menambahkan bidang ke `pdfDocument.Form`, penampil PDF akan mengabaikan anotasi widget, dan data bidang tidak akan pernah dikirim. Baris ini menyelesaikan operasi **modify pdf to include text box**.

## Langkah 5: Simpan PDF yang telah diperbarui

Akhirnya, tulis perubahan kembali ke disk. Anda dapat menimpa file asli atau membuat file baru; contoh ini menyimpan ke `output.pdf`.

```csharp
string outputPath = Path.Combine("YOUR_DIRECTORY", "output.pdf");

// Save the document with the new form field
pdfDocument.Save(outputPath);
```

Saat Anda membuka `output.pdf` di Adobe Acrobat Reader, Anda akan melihat kotak teks berbentuk persegi berlabel “Comments” pada halaman 2. Pengguna dapat mengklik di dalamnya, mengetik, dan teks yang dimasukkan akan menjadi bagian dari data formulir PDF.

## Contoh kerja lengkap

Menggabungkan semua potongan, berikut program lengkap yang siap dijalankan. Salin ke proyek konsol baru, ganti `YOUR_DIRECTORY` dengan jalur folder yang sebenarnya, dan jalankan.

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using Aspose.Pdf.Text;
using System.Drawing; // For Color

namespace PdfFormFieldDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the existing PDF
            string inputPath = Path.Combine("YOUR_DIRECTORY", "input.pdf");
            Document pdfDocument = new Document(inputPath);

            // 2️⃣ Create a TextBoxField on page 2 (index 1)
            Page targetPage = pdfDocument.Pages[1];
            Rectangle fieldRect = new Rectangle(100, 500, 200, 530);
            TextBoxField textBox = new TextBoxField(targetPage, fieldRect)
            {
                PartialName = "Comments",
                DefaultAppearance = new DefaultAppearance(
                    FontRepository.FindFont("Helvetica"), 12, Color.Black)
            };

            // 3️⃣ Add a widget annotation to control visual placement
            Rectangle widgetRect = new Rectangle(100, 300, 200, 330);
            textBox.AddWidgetAnnotation(widgetRect);

            // 4️⃣ Register the field with the document's form collection
            pdfDocument.Form.Add(textBox);

            // 5️⃣ Save the modified PDF
            string outputPath = Path.Combine("YOUR_DIRECTORY", "output.pdf");
            pdfDocument.Save(outputPath);

            Console.WriteLine("PDF form field created successfully.");
            Console.WriteLine($"Output saved to: {outputPath}");
        }
    }
}
```

**Output yang diharapkan:**  
Menjalankan program mencetak dua baris konfirmasi ke konsol. Membuka `output.pdf` menampilkan kotak teks pada halaman 2 tempat pengguna dapat mengetik komentar. Ketika formulir dikirim (misalnya melalui tombol “Submit” di Adobe Acrobat), nama bidang `Comments` muncul dalam data FDF atau XFDF yang diekspor.

## Variasi umum dan kasus tepi

| Situasi | Cara menyesuaikan kode |
|-----------|-----------------------|
| **Tambahkan bidang ke halaman yang berbeda** | Ubah `pdfDocument.Pages[1]` ke indeks halaman yang diinginkan (`0`‑based). |
| **Buat kotak teks multi‑baris** | Set `textBox.Multiline = true;` sebelum menambahkan widget. |
| **Tetapkan nilai default** | Assign `textBox.Value = "Enter your comments here";`. |
| **Jadikan bidang wajib** | Set `textBox.Required = true;`. |
| **Tempatkan bidang pada beberapa halaman** | Call `textBox.AddWidgetAnnotation` untuk setiap persegi tambahan pada halaman target. |
| **Gunakan font khusus** | Load the font with `FontRepository.AddFont("path/to/font.ttf")` and reference it in `DefaultAppearance`. |

**Pro tip:** Selalu validasi koordinat persegi terhadap ukuran halaman (`pdfDocument.Pages[1].Rect`). Jika widget berada di luar batas halaman, penampil mungkin memotong atau menyembunyikan bidang tersebut.

## Menguji bidang formulir

1. Buka `output.pdf` di Adobe Acrobat Reader.  
2. Klik di dalam kotak “Comments”; kursor harus muncul.  
3. Ketik teks apa saja dan tekan **Tab** atau klik di tempat lain.  
4. Pilih **File → Save As** untuk menyimpan nilai yang dimasukkan.  
5. (Opsional) Gunakan API `Form` Aspose.PDF untuk mengekstrak nilai secara programatis:

```csharp
string commentValue = pdfDocument.Form["Comments"].Value;
Console.WriteLine($"Submitted comment: {commentValue}");
```

Potongan kode ini menunjukkan bahwa bidang tidak hanya terlihat tetapi juga dapat diambil melalui kode—penting untuk pemrosesan sisi‑server.

## Kesimpulan

Anda kini tahu cara **create pdf form field** di C# dari awal hingga akhir. Tutorial ini mencakup memuat PDF, mengonfigurasi `TextBoxField`, menambahkan anotasi widget, mendaftarkan bidang, dan menyimpan hasilnya. Dengan blok‑blok bangunan ini Anda dapat **add text box to pdf** dokumen, **modify pdf to include text box**, dan memperluas pendekatan ke tipe bidang lain seperti kotak centang, tombol radio, atau dropdown.

Selanjutnya, jelajahi topik terkait seperti **extracting form data**, **flattening PDF forms**, atau **styling fields with borders and colors**. Masing‑masing konsep ini dibangun di atas API inti yang baru saja Anda kuasai, memungkinkan Anda membuat PDF interaktif yang canggih sepenuhnya dalam C#.

Selamat coding, dan jangan ragu bereksperimen dengan persegi yang berbeda, font, serta aturan validasi untuk menyesuaikan kebutuhan aplikasi Anda!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Buat Dokumen PDF dengan Aspose – Tambah Halaman, Kotak Teks, dan Formulir](/pdf/english/net/forms-annotations/create-pdf-document-with-aspose-add-page-text-box-and-form/)
- [Cara Membuat PDF dengan Aspose – Tambah Bidang Formulir dan Halaman](/pdf/english/net/programming-with-forms/how-to-create-pdf-with-aspose-add-form-field-and-pages/)
- [Cara Menambahkan Stempel Teks ke PDF Menggunakan Aspose.PDF .NET: Panduan Komprehensif](/pdf/english/net/watermarks-backgrounds/add-text-stamp-pdf-aspose-pdf-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}