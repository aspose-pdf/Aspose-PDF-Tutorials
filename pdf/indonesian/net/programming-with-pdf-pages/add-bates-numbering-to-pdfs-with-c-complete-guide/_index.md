---
category: general
date: 2026-06-24
description: Tambahkan penomoran Bates ke file PDF menggunakan C# dan Aspose.PDF.
  Pelajari penomoran halaman khusus, penomoran halaman berurutan, dan penomoran header
  dan footer dalam hitungan menit.
draft: false
keywords:
- add bates numbering
- custom page numbers
- sequential page numbers
- bates numbering pdf
- header footer numbering
language: id
og_description: Tambahkan penomoran Bates ke file PDF menggunakan C# dan Aspose.PDF.
  Kuasai penomoran halaman khusus serta penomoran header dan footer dalam beberapa
  langkah mudah.
og_title: Tambahkan Penomoran Bates ke PDF dengan C# – Panduan Lengkap
schemas:
- author: Aspose
  dateModified: '2026-06-24'
  description: Add bates numbering to PDF files using C# and Aspose.PDF. Learn custom
    page numbers, sequential page numbers, and header footer numbering in minutes.
  headline: Add Bates Numbering to PDFs with C# – Complete Guide
  type: TechArticle
- description: Add bates numbering to PDF files using C# and Aspose.PDF. Learn custom
    page numbers, sequential page numbers, and header footer numbering in minutes.
  name: Add Bates Numbering to PDFs with C# – Complete Guide
  steps:
  - name: Load the Source PDF Document
    text: First we need a `Document` object that represents the file we want to modify.
  - name: Configure Bates Numbering Options (custom page numbers)
    text: Now we set up a `BatesNumberingOptions` object. This is where you define
      **custom page numbers**, the font, colors, and margins.
  - name: Apply the Bates Numbering to the Entire Document
    text: With the options prepared, the actual insertion is a single method call.
  - name: Save the PDF with Bates Numbers Applied
    text: Finally, write the modified document back to disk.
  - name: Limiting the Page Range
    text: 'Sometimes you only want to number a subset, such as pages 3‑10 of a 25‑page
      contract. Adjust `StartingPage` and `EndingPage` accordingly:'
  - name: Changing the Placement to Footer
    text: 'If your workflow requires **header footer numbering** at the bottom left,
      tweak the `Margin`:'
  - name: Using a Different Format
    text: 'Legal teams sometimes use “2024‑A‑001”. Just change the format string:'
  - name: Handling Transparent Backgrounds
    text: The `BackgroundColor = Color.Transparent` ensures the number doesn’t obscure
      existing content. If you need a light gray box behind the text for readability,
      replace it with `Color.LightGray`.
  type: HowTo
- questions:
  - answer: Yes—load the document with the password first (`pdfDocument = new Document("file.pdf",
      new LoadOptions { Password = "pwd" })`) then apply the same steps.
    question: Will this work with password‑protected PDFs?
  - answer: You can run `AddBatesNumbering` twice with two separate `BatesNumberingOptions`,
      each targeting either odd (`StartingPage = 1; EndingPage = pdfDocument.Pages.Count;
      PageSequence = PageSequence.Odd`) or even pages.
    question: Can I add different numbers to odd and even pages?
  - answer: A trial works for evaluation, but the trial adds a watermark. For production
      use you’ll need a valid license to get a clean **bates numbering pdf**.
    question: Do I need a license for Aspose.PDF?
  type: FAQPage
tags:
- Aspose.PDF
- C#
- PDF manipulation
title: Tambahkan Penomoran Bates ke PDF dengan C# – Panduan Lengkap
url: /id/net/programming-with-pdf-pages/add-bates-numbering-to-pdfs-with-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tambahkan Penomoran Bates ke PDF dengan C# – Panduan Lengkap

Tambahkan penomoran bates ke file PDF Anda dengan C# hanya dengan beberapa baris kode. Jika Anda pernah membutuhkan nomor halaman khusus untuk brief hukum atau menginginkan nomor halaman berurutan di seluruh bundel kontrak, tutorial ini akan membantu Anda.

Dalam beberapa menit ke depan kami akan membahas semua yang perlu Anda ketahui: memuat PDF, mengonfigurasi gaya penomoran, menerapkan nomor, dan akhirnya menyimpan file yang diperbarui. Pada akhir tutorial Anda akan dapat menghasilkan **bates numbering pdf** yang tampak profesional, baik Anda memproses satu file maupun seluruh folder dokumen.

## Apa yang Anda Butuhkan

- **.NET 6.0 atau lebih baru** – kode menargetkan .NET 6, tetapi versi sebelumnya dari .NET Framework juga dapat digunakan.
- **Aspose.PDF for .NET** – perpustakaan komersial (tersedia trial gratis) yang menyediakan kelas `Document` dan `BatesNumberingOptions` yang digunakan dalam panduan ini.
- **IDE C#** (Visual Studio, Rider, atau VS Code) – editor apa pun yang dapat mengompilasi proyek .NET sudah cukup.
- File PDF input bernama `input.pdf` yang ditempatkan di folder yang dapat Anda referensikan dari kode Anda.

Sudah siap? Bagus—mari kita mulai.

## Penambahan Penomoran Bates – Ikhtisar

Ide utama di balik **add bates numbering** adalah memperlakukan PDF sebagai kanvas dan kemudian menggambar sebuah string (seperti “DOC‑001”) pada header atau footer setiap halaman. Aspose.PDF melakukan pekerjaan berat: Anda cukup mendeskripsikan format, rentang halaman, dan gaya visual, dan perpustakaan akan menuliskan nomor-nomornya untuk Anda.

Berikut adalah contoh lengkap yang dapat dijalankan yang dapat Anda salin‑tempel ke aplikasi konsol. Setiap baris dijelaskan, sehingga Anda akan memahami tidak hanya *apa* yang harus ditulis, tetapi *mengapa* setiap bagian penting.

### Langkah 1: Muat Dokumen PDF Sumber

Pertama kita membutuhkan objek `Document` yang mewakili file yang ingin kita modifikasi.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Facades;
using System.Drawing;

// Load the source PDF (replace the path with your actual folder)
Document pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");
```

> **Mengapa ini penting:** Kelas `Document` adalah titik masuk untuk semua operasi PDF. Ia memuat file ke dalam memori, memberi Anda akses ke koleksi `Pages`, yang nanti akan kami iterasi saat menambahkan nomor.

### Langkah 2: Konfigurasikan Opsi Penomoran Bates (nomor halaman khusus)

Sekarang kami menyiapkan objek `BatesNumberingOptions`. Di sinilah Anda mendefinisikan **nomor halaman khusus**, font, warna, dan margin.

```csharp
BatesNumberingOptions batesOptions = new BatesNumberingOptions
{
    NumberingFormat = "DOC-{0:D3}",          // e.g., DOC-001, DOC-002 …
    StartNumber = 1,
    StartingPage = 1,
    EndingPage = pdfDocument.Pages.Count,
    Font = new Font(FontFamily.Helvetica, 12, FontStyle.Bold),
    ForegroundColor = Color.Black,
    BackgroundColor = Color.Transparent,
    Margin = new Margin(0, 20, 20, 0)        // top, right, bottom, left (points)
};
```

- **NumberingFormat** – placeholder `{0:D3}` memberi tahu Aspose untuk menambahkan angka nol di depan sehingga menjadi tiga digit.
- **StartNumber** – tempat urutan dimulai; ubah jika Anda menambahkan ke bundel yang sudah ada.
- **StartingPage / EndingPage** – menentukan rentang halaman; Anda dapat membatasinya ke 2‑5 untuk subset, memberikan **nomor halaman berurutan** hanya di mana Anda membutuhkannya.
- **Font & Colors** – gaya visual untuk **penomoran header footer**; Helvetica bekerja baik untuk dokumen hukum karena bersih dan mudah dibaca.
- **Margin** – menempatkan teks 20 pts dari tepi atas dan kanan; sesuaikan nilai ini untuk memindahkan nomor ke bawah atau kiri jika diinginkan.

> **Tip pro:** Jika Anda membutuhkan nomor di footer bukan di header, tukar nilai `Margin` menjadi sesuatu seperti `new Margin(0, 0, 20, 20)` (bawah, kiri).

### Langkah 3: Terapkan Penomoran Bates ke Seluruh Dokumen

Dengan opsi yang sudah disiapkan, penyisipan sebenarnya cukup dengan satu pemanggilan metode.

```csharp
// Apply the numbering to every page in the defined range
pdfDocument.AddBatesNumbering(batesOptions);
```

Di balik layar, Aspose mengiterasi halaman yang dipilih, memformat setiap nomor sesuai `NumberingFormat`, dan menggambar string pada kanvas halaman. Ini adalah inti dari **add bates numbering**—tanpa perlu loop manual.

### Langkah 4: Simpan PDF dengan Penomoran Bates yang Diterapkan

Akhirnya, tulis dokumen yang telah dimodifikasi kembali ke disk.

```csharp
// Save the output file (choose a different name to avoid overwriting the source)
pdfDocument.Save("YOUR_DIRECTORY/BatesNumbered.pdf");
```

Saat Anda membuka `BatesNumbered.pdf` Anda akan melihat “DOC‑001”, “DOC‑002”, … tercetak di pojok kanan atas setiap halaman. Itu adalah **bates numbering pdf** yang berfungsi penuh siap untuk pengarsipan atau e‑discovery.

## Hasil yang Diharapkan

| Page | Header (example) |
|------|------------------|
| 1    | DOC‑001 |
| 2    | DOC‑002 |
| …    | … |
| N    | DOC‑00N |

Nomor muncul tepat di tempat yang ditentukan oleh `Margin`, menggunakan font Helvetica Bold 12‑pt. Jika Anda membuka file di Adobe Acrobat, Anda akan memperhatikan bahwa nomor tersebut merupakan bagian dari konten halaman—bukan anotasi terpisah—sehingga mereka tetap ada saat mencetak dan meratakan.

## Kasus Tepi & Variasi

### Membatasi Rentang Halaman

Kadang-kadang Anda hanya ingin menomori subset, seperti halaman 3‑10 dari kontrak 25 halaman. Sesuaikan `StartingPage` dan `EndingPage` sesuai kebutuhan:

```csharp
batesOptions.StartingPage = 3;
batesOptions.EndingPage = 10;
batesOptions.StartNumber = 1; // reset numbering for the subset
```

### Mengubah Penempatan ke Footer

Jika alur kerja Anda memerlukan **header footer numbering** di kiri bawah, sesuaikan `Margin`:

```csharp
batesOptions.Margin = new Margin(20, 0, 0, 20); // top, right, bottom, left
```

### Menggunakan Format yang Berbeda

Tim hukum kadang-kadang menggunakan “2024‑A‑001”. Cukup ubah string formatnya:

```csharp
batesOptions.NumberingFormat = "2024-A-{0:D3}";
```

### Menangani Latar Belakang Transparan

`BackgroundColor = Color.Transparent` memastikan nomor tidak menutupi konten yang ada. Jika Anda membutuhkan kotak abu-abu muda di belakang teks untuk keterbacaan, ganti dengan `Color.LightGray`.

## Pertanyaan Umum (Terjawab)

- **Apakah ini akan bekerja dengan PDF yang dilindungi password?**  
  Ya—muat dokumen dengan password terlebih dahulu (`pdfDocument = new Document("file.pdf", new LoadOptions { Password = "pwd" })`) kemudian terapkan langkah yang sama.

- **Bisakah saya menambahkan nomor yang berbeda pada halaman ganjil dan genap?**  
  Anda dapat menjalankan `AddBatesNumbering` dua kali dengan dua `BatesNumberingOptions` terpisah, masing‑masing menargetkan halaman ganjil (`StartingPage = 1; EndingPage = pdfDocument.Pages.Count; PageSequence = PageSequence.Odd`) atau genap.

- **Apakah saya memerlukan lisensi untuk Aspose.PDF?**  
  Versi trial dapat digunakan untuk evaluasi, tetapi trial menambahkan watermark. Untuk penggunaan produksi Anda memerlukan lisensi yang valid agar mendapatkan **bates numbering pdf** yang bersih.

## Contoh Lengkap yang Berfungsi (Siap Salin‑Tempel)

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Facades;
using System.Drawing;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source PDF
        Document pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");

        // 2️⃣ Set up numbering options (custom page numbers, sequential page numbers)
        BatesNumberingOptions batesOptions = new BatesNumberingOptions
        {
            NumberingFormat = "DOC-{0:D3}",
            StartNumber = 1,
            StartingPage = 1,
            EndingPage = pdfDocument.Pages.Count,
            Font = new Font(FontFamily.Helvetica, 12, FontStyle.Bold),
            ForegroundColor = Color.Black,
            BackgroundColor = Color.Transparent,
            Margin = new Margin(0, 20, 20, 0) // top, right, bottom, left
        };

        // 3️⃣ Apply the numbering (header footer numbering)
        pdfDocument.AddBatesNumbering(batesOptions);

        // 4️⃣ Save the result
        pdfDocument.Save("YOUR_DIRECTORY/BatesNumbered.pdf");

        System.Console.WriteLine("Bates numbering added successfully!");
    }
}
```

Jalankan program, buka file output, dan Anda akan melihat nomor tepat di tempat yang ditentukan kode kepada Aspose. Tanpa loop tambahan, tanpa menggambar manual—hanya **add bates numbering** dalam empat langkah singkat.

## Kesimpulan

Anda kini memiliki cara yang solid dan siap produksi untuk **add bates numbering** ke PDF apa pun menggunakan C# dan Aspose.PDF. Dari memuat dokumen hingga mengonfigurasi **nomor halaman khusus**, menerapkan **nomor halaman berurutan**, dan menyimpan **bates numbering pdf** yang bersih, seluruh alur kerja dapat dilakukan dalam satu pemanggilan metode.

Apa selanjutnya? Cobalah menggabungkan teknik ini dengan fitur Aspose lainnya—seperti menempelkan logo, menggabungkan beberapa PDF, atau mengekstrak halaman berdasarkan nomor yang baru saja Anda tambahkan. Menjelajahi **header footer numbering** bersama watermark dapat memberikan

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Aspose.PDF .NET&#58; Tambahkan Nomor Halaman ke PDF Menggunakan FloatingBox](/pdf/english/net/text-operations/aspose-pdf-net-floatingbox-page-numbering/)
- [Cara Menambahkan dan Menyesuaikan Nomor Halaman di PDF Menggunakan Aspose.PDF untuk .NET | Panduan Manipulasi Dokumen](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [Tambahkan Gambar & Nomor Halaman ke PDF Menggunakan Aspose.PDF untuk .NET&#58; Panduan Lengkap](/pdf/english/net/document-manipulation/enhance-pdfs-images-page-numbers-aspose-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}