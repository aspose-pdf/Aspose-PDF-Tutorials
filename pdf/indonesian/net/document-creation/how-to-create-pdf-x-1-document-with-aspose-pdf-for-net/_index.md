---
category: general
date: 2026-10-13
description: Buat dokumen PDF/X‑1 di .NET menggunakan Aspose.PDF – panduan langkah
  demi langkah yang juga menunjukkan cara mengonversi PDF ke PDF/X‑1 dengan profil
  ICC.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create pdfx-1 document
- convert pdf to pdfx-1
- how to convert pdfx-1
language: id
lastmod: 2026-10-13
og_description: Buat dokumen PDF/X‑1 dengan Aspose.PDF untuk .NET. Pelajari cara mengonversi
  PDF ke PDF/X‑1, mengatur profil ICC, dan menyimpan hasilnya dalam hitungan menit.
og_image_alt: Screenshot of code that creates a PDF/X‑1 document using Aspose.PDF
og_title: Buat dokumen PDF/X‑1 di .NET – panduan lengkap Aspose.PDF
schemas:
- author: Aspose
  dateModified: '2026-10-13'
  description: Create PDF/X‑1 document in .NET using Aspose.PDF – a step‑by‑step guide
    that also shows how to convert PDF to PDF/X‑1 with ICC profiles.
  headline: How to create PDF/X‑1 document with Aspose.PDF for .NET
  type: TechArticle
- description: Create PDF/X‑1 document in .NET using Aspose.PDF – a step‑by‑step guide
    that also shows how to convert PDF to PDF/X‑1 with ICC profiles.
  name: How to create PDF/X‑1 document with Aspose.PDF for .NET
  steps:
  - name: Open the file in Adobe Acrobat Pro and check **File → Properties → Standards**.
      It should list **PDF/X‑1a:2001** (or PDF/X‑1a:2003) as the compliance level.
    text: Open the file in Adobe Acrobat Pro and check **File → Properties → Standards**.
      It should list **PDF/X‑1a:2001** (or PDF/X‑1a:2003) as the compliance level.
  - name: Use a free validator such as **VeraPDF** to run an automated compliance
      test. The tool will report any missing OutputIntent or disallowed features.
    text: Use a free validator such as **VeraPDF** to run an automated compliance
      test. The tool will report any missing OutputIntent or disallowed features.
  - name: If validation fails, double‑check that the ICC profile path is correct and
      that the source PDF does not contain prohibited elements (e.g., embedded multimedia).
    text: If validation fails, double‑check that the ICC profile path is correct and
      that the source PDF does not contain prohibited elements (e.g., embedded multimedia).
  type: HowTo
tags:
- Aspose.PDF
- .NET
- PDF/X‑1
title: Cara membuat dokumen PDF/X‑1 dengan Aspose.PDF untuk .NET
url: /id/net/document-creation/how-to-create-pdf-x-1-document-with-aspose-pdf-for-net/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara membuat dokumen PDF/X‑1 dengan Aspose.PDF untuk .NET

Jika Anda perlu **membuat dokumen PDF/X‑1** secara programatis, panduan ini menunjukkan secara tepat cara melakukannya. Dengan mengikuti langkah‑langkah di bawah, Anda akan dapat **mengonversi PDF ke PDF/X‑1** sambil mengontrol profil ICC, semuanya hanya dengan beberapa baris kode C#.

Anda juga akan mempelajari mengapa setiap langkah penting, cara menangani jebakan umum, dan seperti apa file akhir. Tidak diperlukan alat eksternal selain pustaka Aspose.PDF untuk .NET.

## Apa yang akan Anda capai

- Muat file PDF yang sudah ada.
- Tentukan profil ICC (FOGRA39) yang diperlukan untuk kepatuhan PDF/X‑1.
- Bangun opsi konversi yang menyematkan profil sebagai OutputIntent.
- Konversi PDF sumber menjadi dokumen **PDF/X‑1**.
- Simpan hasilnya ke disk.

> **Prasyarat** – Anda harus memiliki salinan berlisensi **Aspose.PDF untuk .NET** (versi 23.4 atau lebih baru) dan lingkungan pengembangan .NET seperti Visual Studio 2022.

## Langkah 1: Muat dokumen PDF sumber

Operasi pertama adalah membuka PDF yang ingin Anda ubah. Aspose.PDF menggunakan objek `Document` yang mewakili seluruh file di memori.

```csharp
// Step 1: Load the source PDF document
string dataDir = "YOUR_DIRECTORY/";                     // folder that contains input.pdf and the ICC profile
using (var doc = new Aspose.Pdf.Document(dataDir + "input.pdf"))
{
    // The Document object is now ready for conversion.
```

**Mengapa ini penting:** Membuka file di dalam blok `using` menjamin semua sumber daya yang tidak dikelola dilepaskan segera setelah konversi selesai, mencegah kebocoran handle file.

## Langkah 2: Buat opsi konversi untuk PDF/X‑1

Aspose.PDF memerlukan instance `PdfFormatConversionOptions` untuk menentukan format target dan data kepatuhan tambahan apa pun.

```csharp
    // Step 2: Create conversion options for PDF/X‑1
    var conversionOptions = new Aspose.Pdf.PdfFormatConversionOptions();
```

**Mengapa ini penting:** Objek opsi memberi tahu pustaka bahwa Anda tidak hanya menginginkan salinan PDF biasa—Anda memerlukan output yang **mematuhi PDF/X‑1**, yang memberlakukan aturan manajemen warna yang ketat.

## Langkah 3: Lampirkan profil ICC eksternal (FOGRA39)

PDF/X‑1 mewajibkan profil ICC yang disematkan yang mendefinisikan ruang warna. Di sini kami mengarahkan opsi konversi ke file `.icc` lokal.

```csharp
    // Step 3: Specify the external ICC profile (FOGRA39)
    conversionOptions.IccProfileFileName = dataDir + "FOGRA39.icc";
```

**Mengapa ini penting:** Tanpa profil ICC yang valid, file yang dihasilkan akan gagal pada alat validasi PDF/X‑1. FOGRA39 adalah profil CMYK umum untuk standar percetakan Eropa.

## Langkah 4: Bangun OutputIntent dan tambahkan ke opsi

`OutputIntent` membungkus profil ICC dan menjadikannya bagian dari metadata PDF.

```csharp
    // Step 4: Create an OutputIntent using the ICC profile and add it to the options
    var outputIntent = new Aspose.Pdf.OutputIntent(conversionOptions.IccProfileFileName);
    conversionOptions.OutputIntents.Add(outputIntent);
```

**Mengapa ini penting:** PDF/X‑1 memerlukan setidaknya satu OutputIntent. Menambahkannya secara eksplisit memastikan mesin konversi menyematkan profil dengan benar, menghindari kesalahan validasi.

## Langkah 5: Konversi dokumen ke format PDF/X‑1

Sekarang kami memicu konversi sebenarnya. Metode `Convert` menerima objek opsi dan nilai enumerasi target.

```csharp
    // Step 5: Convert the document to PDF/X‑1 format
    doc.Convert(conversionOptions, Aspose.Pdf.PdfFormat.PdfX_1);
```

**Mengapa ini penting:** Enum `PdfX_1` memberi tahu Aspose untuk menerapkan semua batasan PDF/X‑1 (mis., tidak ada objek transparan, font tersemat, ruang warna yang benar). Jika Anda memerlukan PDF/X‑4, Anda dapat menggunakan `PdfX_4` sebagai gantinya.

## Langkah 6: Simpan file PDF/X‑1 yang telah dikonversi

Akhirnya, tulis file yang mematuhi kembali ke disk.

```csharp
    // Step 6: Save the converted PDF/X‑1 file
    doc.Save(dataDir + "output_pdfx1.pdf");
}
```

**Mengapa ini penting:** Menyimpan di dalam blok `using` yang sama memastikan dokumen sepenuhnya ditulis sebelum handle file dilepaskan. File output sekarang dapat diverifikasi dengan validator PDF/X apa pun.

---

![Diagram yang menunjukkan pembuatan dokumen PDF/X‑1](/images/create-pdfx1-workflow.png){.align-center width=600 alt="Diagram yang menunjukkan cara membuat dokumen PDF/X‑1 dengan Aspose.PDF"}

## Cara memverifikasi bahwa dokumen PDF/X‑1 valid

1. Buka file di Adobe Acrobat Pro dan periksa **File → Properties → Standards**. Itu harus menampilkan **PDF/X‑1a:2001** (atau PDF/X‑1a:2003) sebagai tingkat kepatuhan.  
2. Gunakan validator gratis seperti **VeraPDF** untuk menjalankan tes kepatuhan otomatis. Alat tersebut akan melaporkan OutputIntent yang hilang atau fitur yang tidak diizinkan.  
3. Jika validasi gagal, periksa kembali bahwa jalur profil ICC sudah benar dan bahwa PDF sumber tidak mengandung elemen terlarang (mis., multimedia yang disematkan).

## Kasus tepi umum dan cara menanganinya

| Situation | Solution |
|-----------|----------|
| **PDF sumber berisi objek transparan** | Objek transparan tidak diizinkan dalam PDF/X‑1. Sebelum konversi, ratakan PDF dengan meraster halaman atau menghapus transparansi melalui `doc.FlattenPages();`. |
| **Font tidak disematkan** | Pastikan `doc.FontEmbeddingMode = Aspose.Pdf.FontEmbeddingMode.Always;` sebelum konversi. |
| **File profil ICC besar** | Gunakan profil terkompresi (mis., `.icc` < 1 MB) untuk menjaga ukuran PDF akhir tetap wajar. |
| **Konversi melempar `ArgumentException`** | Verifikasi bahwa jalur file ICC bersifat absolut dan bahwa file dapat diakses oleh proses yang sedang berjalan. |

## Tips pro: Menggunakan kembali opsi konversi untuk pemrosesan batch

Jika Anda perlu mengonversi banyak PDF ke PDF/X‑1, buat instance `PdfFormatConversionOptions` sekali, konfigurasikan profil ICC, dan gunakan kembali di dalam loop. Ini mengurangi overhead pembuatan objek dan menjamin manajemen warna yang konsisten di semua file.

```csharp
var options = new Aspose.Pdf.PdfFormatConversionOptions
{
    IccProfileFileName = dataDir + "FOGRA39.icc"
};
options.OutputIntents.Add(new Aspose.Pdf.OutputIntent(options.IccProfileFileName));

foreach (string file in Directory.GetFiles(dataDir, "*.pdf"))
{
    using (var doc = new Aspose.Pdf.Document(file))
    {
        doc.Convert(options, Aspose.Pdf.PdfFormat.PdfX_1);
        string outPath = Path.Combine(dataDir, Path.GetFileNameWithoutExtension(file) + "_pdfx1.pdf");
        doc.Save(outPath);
    }
}
```

## Kesimpulan

Anda sekarang tahu cara **membuat dokumen PDF/X‑1** secara programatis dengan Aspose.PDF untuk .NET, dan Anda juga memahami alur kerja lengkap **mengonversi PDF ke PDF/X‑1**, termasuk penanganan profil ICC, pembuatan OutputIntent, dan tips validasi. Terapkan langkah‑langkah ini untuk mengotomatiskan pembuatan PDF siap cetak dalam aplikasi .NET apa pun.

**Langkah selanjutnya**

- Jelajahi properti **`PdfFormatConversionOptions`** untuk menyempurnakan konversi PDF/X‑4 atau PDF/A.  
- Gabungkan alur kerja ini dengan **ekstraksi gambar Aspose.PDF** untuk menyematkan grafik resolusi tinggi sebelum konversi.  
- Baca dokumentasi resmi Aspose.PDF tentang **manajemen warna** untuk wawasan lebih dalam mengenai pemilihan profil ICC.

Selamat coding, dan nikmati keyakinan bahwa PDF Anda kini memenuhi standar ketat PDF/X‑1!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang terkait erat yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber daya menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan menjelajahi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Cara Mengonversi PDF ke PDF/X-4 Menggunakan Aspose.PDF untuk .NET&#58; Panduan Langkah demi Langkah](/pdf/english/net/pdfa-compliance/convert-pdfs-to-pdf-x4-aspose-dotnet-guide/)
- [Cara Mengonversi PDF ke XML Menggunakan Aspose.PDF untuk .NET&#58; Panduan Langkah demi Langkah](/pdf/english/net/conversion-export/pdf-to-xml-conversion-aspose-pdf-net/)
- [Cara Mengonversi Halaman PDF ke Gambar Menggunakan Aspose.PDF untuk .NET (Panduan Langkah demi Langkah)](/pdf/english/net/conversion-export/convert-pdf-pages-to-images-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}