---
category: general
date: 2026-06-21
description: Buat field kotak teks PDF dengan C# dan pelajari cara menduplikasi field
  formulir PDF atau menambahkan kotak teks ke formulir PDF hanya dalam beberapa baris
  kode.
draft: false
keywords:
- create pdf textbox field
- duplicate pdf form field
- add textbox to pdf form
- pdf form automation
- c# pdf library
language: id
og_description: Buat bidang kotak teks PDF dengan cepat. Panduan ini menunjukkan cara
  menduplikasi bidang formulir PDF dan menambahkan kotak teks ke formulir PDF menggunakan
  perpustakaan PDF C# modern.
og_title: Buat Kolom Teks PDF – Tutorial Lengkap C#
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Create PDF textbox field with C# and learn how to duplicate PDF form
    field or add textbox to PDF form in just a few lines of code.
  headline: Create PDF Textbox Field – Step‑by‑Step Guide
  type: TechArticle
- description: Create PDF textbox field with C# and learn how to duplicate PDF form
    field or add textbox to PDF form in just a few lines of code.
  name: Create PDF Textbox Field – Step‑by‑Step Guide
  steps:
  - name: What if I need the field on *more* than two pages?
    text: Just repeat the clone‑and‑add steps for each additional page. The underlying
      data object stays the same, so all widgets stay in sync.
  - name: How do I change the appearance (font, border, background)?
    text: Each `Widget` has a `SetBorderColor`, `SetBorderWidth`, and `SetBackgroundColor`
      method. You can also assign a default appearance string (`DA`) to control the
      font and size.
  - name: Can I make the field read‑only after the user fills it?
    text: Yes. Set the `ReadOnly` flag on the field after you’ve collected the data,
      or toggle it based on your workflow.
  - name: What about PDFs that already contain a form?
    text: If the document already has an AcroForm, `doc.GetForm()` simply returns
      it. You can then add new fields without disturbing existing ones. Just be careful
      to use unique field names.
  type: HowTo
tags:
- PDF
- C#
- FormFields
title: Buat Kolom Teks PDF – Panduan Langkah demi Langkah
url: /id/net/programming-with-forms/create-pdf-textbox-field-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat Bidang Kotak Teks PDF – Tutorial Lengkap C#

Pernah membutuhkan untuk **create PDF textbox field** tetapi tidak yakin panggilan API mana yang harus digunakan? Anda tidak sendirian. Baik Anda sedang membangun portal penandatanganan kontrak atau lembar penangkapan data sederhana, menambahkan kotak teks interaktif ke PDF adalah keterampilan inti bagi setiap pengembang otomatisasi formulir.  

Dalam panduan ini kami akan membahas contoh praktis yang tidak hanya **adds textbox to PDF form**, tetapi juga menunjukkan cara **duplicate PDF form field** sehingga input yang sama muncul di beberapa halaman. Pada akhir Anda akan memiliki program yang dapat dijalankan yang dapat Anda masukkan ke proyek .NET mana pun.

## Apa yang Anda Butuhkan

- .NET 6.0 atau lebih baru (kode ini juga bekerja dengan .NET Core)  
- Perpustakaan PDF C# modern – potongan kode di bawah menggunakan **PDFTron SDK**, tetapi konsepnya dapat diterapkan ke iText 7, PdfSharp, atau perpustakaan lain.  
- Visual Studio 2022 (atau IDE apa pun yang Anda suka)  

Itu saja – tidak ada layanan tambahan, tidak ada ketergantungan yang rumit. Jika Anda sudah memiliki PDF yang ingin ditambah, cukup arahkan kode ke sana.

---

## Langkah 1: Siapkan Proyek dan Impor SDK

Pertama, buat aplikasi console:

```bash
dotnet new console -n PdfFormDemo
cd PdfFormDemo
```

Add the PDFTron NuGet package:

```bash
dotnet add package PDFTron.NET
```

Now open `Program.cs` and pull in the namespaces we’ll need:

```csharp
using System;
using pdftron;
using pdftron.Common;
using pdftron.PDF;
using pdftron.SDF;
```

> **Pro tip:** Jika Anda menggunakan perpustakaan lain, ganti pernyataan `using` dengan yang setara (mis., `iText.Kernel.Pdf` untuk iText 7).

## Langkah 2: Inisialisasi Dokumen PDF dan Formulir

Kami akan memulai dengan PDF baru yang berisi dua halaman – halaman sumber untuk kotak teks asli dan halaman target untuk duplikat.

```csharp
PDFNet.Initialize();                     // Initialize the PDFTron runtime

// Create a new PDF document
using (PDFDoc doc = new PDFDoc())
{
    // Add two blank pages (letter size)
    Page sourcePage = doc.PageCreate(new Size(612, 792));
    doc.PagePushBack(sourcePage);
    Page targetPage = doc.PageCreate(new Size(612, 792));
    doc.PagePushBack(targetPage);

    // Get (or create) the AcroForm object
    Form form = doc.GetForm();
```

Objek `Form` adalah tempat semua bidang interaktif berada. Jika dokumen belum memiliki formulir, `GetForm()` akan membuatnya untuk kita.

## Langkah 3: **Create PDF Textbox Field** pada Halaman Pertama

Sekarang masuk ke inti tutorial kami – membuat bidang kotak teks. Koordinat persegi panjang dinyatakan dalam poin (1 inci = 72 poin). Contoh menempatkan kotak di dekat bagian atas‑tengah halaman pertama.

```csharp
    // Step 1: Create a text box field on the first page and set its initial value
    TextBoxField textBoxField = new TextBoxField(sourcePage, new Rect(100, 500, 300, 520))
    {
        Value = "Sample"
    };
```

Mengapa kami menetapkan `Value` langsung? Mengisi bidang sebelumnya memberikan petunjuk kepada pengguna tentang input yang diharapkan, dan juga menunjukkan bahwa bidang tersebut berfungsi sepenuhnya.

## Langkah 4: Tambahkan Bidang ke Formulir – **Add Textbox to PDF Form**

Selanjutnya, kami mendaftarkan bidang ke formulir menggunakan nama logis. Nama ini yang akan Anda referensikan nanti ketika perlu membaca atau memodifikasi data bidang secara programatis.

```csharp
    // Step 2: Add the field to the form with a logical name
    form.Add(textBoxField, "multiBox");
```

Memilih nama yang jelas (seperti `"multiBox"`) membuat kode selanjutnya lebih mudah dipahami, terutama ketika Anda memiliki puluhan bidang.

## Langkah 5: **Duplicate PDF Form Field** pada Halaman Lain

Kebutuhan umum adalah menampilkan bidang yang sama di beberapa halaman – misalnya kotak “Customer Name” yang muncul di setiap halaman faktur. PDFTron memungkinkan kami mengkloning anotasi widget, yang merupakan representasi visual dari bidang.

```csharp
    // Step 3: Clone the field's widget annotation so it can appear on another page
    Widget clonedWidget = textBoxField.CreateWidgetAnnotation();

    // Step 4: Place the cloned widget on the second page
    targetPage.Annotations.Add(clonedWidget);
```

Widget yang dikloning berbagi data dasar yang sama dengan kotak teks asli. Ketika pengguna mengetik pada satu instance, yang lain akan diperbarui secara otomatis – itulah keajaiban **duplicate PDF form field**.

## Langkah 6: Simpan Dokumen dan Bersihkan

Akhirnya, tulis PDF ke disk dan matikan runtime PDFNet.

```csharp
    // Save the resulting PDF
    doc.Save("output.pdf", SDFDoc.SaveOptions.e_linearized);
    Console.WriteLine("PDF created: output.pdf");
}

// Shut down PDFNet (optional but good practice)
PDFNet.Terminate();
```

Menjalankan program menghasilkan PDF dua‑halaman (`output.pdf`). Buka di Adobe Acrobat Reader, klik kotak teks pada halaman 1, ketik sesuatu, lalu beralih ke halaman 2 – teks yang sama muncul secara instan. Itu contoh **create pdf textbox field** yang berfungsi penuh dengan bidang yang diduplikasi.

---

## Contoh Kerja Penuh (Siap Salin‑Tempel)

```csharp
// Program.cs
using System;
using pdftron;
using pdftron.Common;
using pdftron.PDF;
using pdftron.SDF;

class Program
{
    static void Main()
    {
        PDFNet.Initialize();

        using (PDFDoc doc = new PDFDoc())
        {
            // Create two pages
            Page sourcePage = doc.PageCreate(new Size(612, 792));
            doc.PagePushBack(sourcePage);
            Page targetPage = doc.PageCreate(new Size(612, 792));
            doc.PagePushBack(targetPage);

            // Get the form (creates one if missing)
            Form form = doc.GetForm();

            // Step 1: Create a text box field on the first page
            TextBoxField textBoxField = new TextBoxField(sourcePage,
                new Rect(100, 500, 300, 520))
            {
                Value = "Sample"
            };

            // Step 2: Add the field to the form
            form.Add(textBoxField, "multiBox");

            // Step 3: Clone the widget so it appears on page 2
            Widget clonedWidget = textBoxField.CreateWidgetAnnotation();

            // Step 4: Attach the cloned widget to the second page
            targetPage.Annotations.Add(clonedWidget);

            // Save the file
            doc.Save("output.pdf", SDFDoc.SaveOptions.e_linearized);
            Console.WriteLine("PDF created: output.pdf");
        }

        PDFNet.Terminate();
    }
}
```

**Output yang diharapkan:** Sebuah file bernama `output.pdf` yang berisi dua halaman. Kedua halaman menampilkan kotak teks yang dapat diedit dengan label “Sample”. Mengedit satu akan memperbarui yang lain secara instan.

---

## Pertanyaan Umum & Kasus Tepi

### Bagaimana jika saya membutuhkan bidang pada *lebih* dari dua halaman?

Cukup ulangi langkah kloning‑dan‑penambahan untuk setiap halaman tambahan. Objek data dasar tetap sama, sehingga semua widget tetap sinkron.

```csharp
Widget anotherClone = textBoxField.CreateWidgetAnnotation();
thirdPage.Annotations.Add(anotherClone);
```

### Bagaimana cara mengubah tampilan (font, border, background)?

Setiap `Widget` memiliki metode `SetBorderColor`, `SetBorderWidth`, dan `SetBackgroundColor`. Anda juga dapat menetapkan string tampilan default (`DA`) untuk mengontrol font dan ukuran.

```csharp
textBoxField.SetBorderColor(new ColorPt(0, 0, 1), 3); // blue border
textBoxField.SetBackgroundColor(new ColorPt(0.9, 0.9, 0.9), 3); // light gray fill
textBoxField.SetDefaultAppearance("Helvetica 12 Tf 0 g");
```

### Bisakah saya membuat bidang hanya‑baca setelah pengguna mengisinya?

Ya. Tetapkan flag `ReadOnly` pada bidang setelah Anda mengumpulkan data, atau ubah statusnya berdasarkan alur kerja Anda.

```csharp
textBoxField.SetFlag(Field.Flag.e_readonly, true);
```

### Bagaimana dengan PDF yang sudah berisi formulir?

Jika dokumen sudah memiliki AcroForm, `doc.GetForm()` hanya mengembalikannya. Anda kemudian dapat menambahkan bidang baru tanpa mengganggu yang sudah ada. Hanya pastikan menggunakan nama bidang yang unik.

## Tips untuk Proyek Dunia Nyata

- **Naming convention:** Tambahkan awalan pada nama bidang dengan halaman atau bagian (mis., `invoice_customer_name`) untuk menghindari benturan.  
- **Validation:** Gunakan aksi JavaScript (`field.SetAction(Field.Action.e_keystroke, "event.rc = /^[A-Za-z]+$/.test(event.change);")`) jika Anda memerlukan validasi sisi klien.  
- **Performance:** Saat bekerja dengan PDF besar, panggil `doc.Lock()` sebelum operasi bulk untuk mengurangi beban I/O.  
- **Accessibility:** Tetapkan properti `AlternateName` agar pembaca layar dapat menjelaskan bidang tersebut.

## Kesimpulan

Kami baru saja **created a PDF textbox field**, menunjukkan cara **duplicate PDF form field** di seluruh halaman, dan mendemonstrasikan cara paling sederhana untuk **add textbox to PDF form** menggunakan C#. Kode lengkap yang dapat dijalankan ada di atas, dan Anda dapat memperluasnya dengan styling, validasi, atau halaman tambahan sesuai kebutuhan.

Siap untuk langkah berikutnya? Coba sematkan dropdown (`ChoiceField`) atau widget tanda tangan, atau jelajahi cara meratakan formulir setelah entri data untuk tujuan arsip. PDFTron SDK (atau perpustakaan serupa) memberi Anda blok bangunan—imajinasi Anda yang menentukan bentuk akhir.

Jika Anda mengalami kendala, tinggalkan komentar di bawah atau periksa dokumentasi resmi perpustakaan; mereka penuh dengan contoh yang melengkapi apa yang kami bahas di sini. Selamat coding, dan semoga formulir Anda selalu sinkron!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait erat yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode kerja lengkap dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Cara Membuat PDF dengan Aspose – Tambahkan Form Field dan Halaman](/pdf/english/net/programming-with-forms/how-to-create-pdf-with-aspose-add-form-field-and-pages/)
- [Tambahkan Form Field dalam Dokumen PDF menggunakan Java](/pdf/english/java/pdf-form-fields/add-form-field-in-pdf-document-using-java/)
- [Tambahkan Form Field dalam Dokumen Pdf menggunakan Java](/pdf/german/java/pdf-form-fields/add-form-field-in-pdf-document-using-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}