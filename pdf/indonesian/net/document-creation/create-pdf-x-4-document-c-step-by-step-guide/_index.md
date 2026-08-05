---
category: general
date: 2026-08-05
description: Buat dokumen PDF/X‑4 dengan C# dan pelajari cara mengonversi PDF ke PDFX4
  menggunakan Aspose.Pdf. Kode lengkap, penjelasan, dan pembuatan ringkasan AI.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create pdf/x‑4 document c#
- convert pdf to pdfx4
- aspose.pdf c# tutorial
- pdf graphics state c#
- ai summary pdf c#
- pdfx4 conversion example
language: id
lastmod: 2026-08-05
og_description: Buat dokumen PDF/X‑4 C# dengan Aspose.Pdf. Panduan ini menunjukkan
  cara mengonversi PDF ke PDFX4, menambahkan ExtGState khusus, dan menghasilkan ringkasan
  AI.
og_image_alt: Screenshot of a C# IDE displaying code that creates a PDF/X‑4 file and
  adds graphics state
og_title: Membuat dokumen PDF/X‑4 dengan C# – tutorial lengkap konversi dan ringkasan
  AI
schemas:
- author: Aspose
  dateModified: '2026-08-05'
  description: Create PDF/X‑4 document C# and learn how to convert PDF to PDFX4 using
    Aspose.Pdf. Full code, explanations, and AI summary generation.
  headline: Create PDF/X‑4 document C# – step‑by‑step guide
  type: TechArticle
tags:
- C#
- PDF
- Aspose.Pdf
- AI
- Document processing
title: Membuat Dokumen PDF/X‑4 dengan C# – Panduan Langkah demi Langkah
url: /id/net/document-creation/create-pdf-x-4-document-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat Dokumen PDF/X‑4 C# – panduan langkah demi langkah

Jika Anda perlu **membuat dokumen PDF/X‑4 C#**, tutorial ini menunjukkan secara tepat cara melakukannya. Anda akan melihat cara mengonversi PDF biasa menjadi PDFX4, menambahkan custom graphics state, dan menghasilkan ringkasan berbasis AI—semua dengan Aspose.Pdf untuk .NET.

Panduan ini mencakup semua hal mulai dari memuat file sumber hingga menyimpan output PDF/X‑4 akhir dan menghasilkan PDF ringkasan. Tidak diperlukan dokumentasi eksternal; cukup ikuti langkah‑langkahnya, salin kode, dan jalankan di IDE .NET pilihan Anda.

## Prasyarat

Sebelum memulai, pastikan Anda memiliki:

- .NET 6.0 atau yang lebih baru terpasang  
- Lisensi aktif Aspose.Pdf untuk .NET (atau kunci evaluasi sementara)  
- Kunci API OpenAI untuk langkah ringkasan AI  
- File PDF bernama `source.pdf` yang ditempatkan di folder yang dapat Anda referensikan dari kode  

Item‑item ini adalah satu‑satunya ketergantungan untuk contoh lengkap.

## Langkah 1: Muat PDF sumber

Operasi pertama adalah membaca file PDF yang sudah ada. Aspose.Pdf merepresentasikan PDF sebagai objek `Document`, yang memberi Anda akses penuh ke halaman, sumber daya, dan metadata.

```csharp
using Aspose.Pdf;

// Load the source PDF from disk
Document sourceDoc = new Document("YOUR_DIRECTORY/source.pdf");
```

> **Mengapa ini penting** – Memuat file membuat representasi dalam memori yang dapat Anda modifikasi tanpa menyentuh file asli di disk.

## Langkah 2: Konversi dokumen ke format PDF/X‑4

PDF/X‑4 adalah subset PDF yang dirancang untuk pencetakan yang dapat diandalkan. Aspose.Pdf menyediakan kelas `PdfFormatConversionOptions` yang memungkinkan Anda menentukan versi target.

```csharp
using Aspose.Pdf;

// Define conversion options for PDF/X‑4
var conversionOptions = new PdfFormatConversionOptions
{
    PdfXVersion = PdfXVersion.PDFX4
};

// Perform the conversion in place
sourceDoc.Convert(conversionOptions);
```

> **Catatan** – Langkah ini **mengonversi pdf ke pdfx4** secara otomatis; `sourceDoc` yang asli kini mengikuti spesifikasi PDF/X‑4.

## Langkah 3: Simpan file PDF/X‑4 yang telah dikonversi

Setelah konversi, tulis file kembali ke disk. Anda dapat mempertahankan nama yang sama atau menggunakan nama baru untuk menghindari menimpa file asli.

```csharp
// Save the PDF/X‑4 document
sourceDoc.Save("YOUR_DIRECTORY/converted-pdfx4.pdf");
```

File yang disimpan mematuhi standar PDF/X‑4 dan dapat dibuka di penampil PDF mana pun yang mendukungnya.

## Langkah 4: Tambahkan ExtGState khusus ke halaman pertama

Graphics state (`ExtGState`) memungkinkan Anda mengontrol properti seperti opacity. Menambahkan state khusus menunjukkan cara bekerja dengan objek PDF tingkat rendah.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Collections;
using Aspose.Pdf.Text;

// Access the first page
var firstPage = sourceDoc.Pages[1];

// Edit the page resources dictionary
var resourcesEditor = new DictionaryEditor(firstPage.Resources);
var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();

// Create an empty dictionary for the new graphics state
var customGs = CosPdfDictionary.CreateEmptyDictionary(sourceDoc);
customGs.Add("CA", new CosPdfNumber(0.7)); // stroke opacity (70%)
customGs.Add("ca", new CosPdfNumber(0.5)); // fill opacity (50%)

// Register the new state under the name "MyGs"
extGStateDict.Add("MyGs", customGs);
```

> **Mengapa Anda mungkin menggunakan ini** – Objek ExtGState khusus berguna ketika Anda memerlukan overlay semi‑transparent, watermark, atau mode blend khusus pada materi cetak.

## Langkah 5: Simpan PDF dengan graphics state baru

Setelah graphics state khusus terpasang, persistenkan perubahan tersebut.

```csharp
// Save the PDF that includes the custom graphics state
sourceDoc.Save("YOUR_DIRECTORY/with-gs.pdf");
```

Buka `with-gs.pdf` di penampil yang mendukung transparansi untuk melihat efeknya (Anda perlu menerapkan state pada perintah menggambar, yang akan ditunjukkan nanti jika Anda memperluas contoh).

## Langkah 6: Siapkan klien AI dan opsi ringkasan

Aspose.Pdf.AI memungkinkan Anda memanggil layanan OpenAI langsung dari kode C# Anda. Pertama, buat `OpenAIClient` dengan kunci API Anda, lalu konfigurasikan opsi ringkasan.

```csharp
using Aspose.Pdf.AI;

// Build the OpenAI client
var aiClient = OpenAIClient.CreateWithApiKey("YOUR_API_KEY").Build();

// Configure summary generation (temperature controls creativity)
var summaryOptions = OpenAISummaryCopilotOptions.Create()
                      .WithTemperature(0.4)
                      .WithDocument("YOUR_DIRECTORY/converted-pdfx4.pdf");
```

> **Penjelasan** – Metode `WithDocument` memberi tahu AI PDF mana yang akan dianalisis. Temperatur yang lebih rendah (0.4) menghasilkan ringkasan singkat dan faktual.

## Langkah 7: Hasilkan ringkasan dan simpan sebagai PDF

Akhirnya, buat copilot ringkasan, minta teksnya, dan tulis hasilnya ke file PDF baru.

```csharp
using Aspose.Pdf.AI;

// Create the summary copilot
var summaryCopilot = AICopilotFactory.CreateSummaryCopilot(aiClient, summaryOptions);

// Asynchronously get the summary text
string summaryText = await summaryCopilot.GetSummaryAsync();

// Output the summary to console (optional)
Console.WriteLine("=== PDF Summary ===\n" + summaryText);

// Save the summary as a PDF file
await summaryCopilot.SaveSummaryAsync("YOUR_DIRECTORY/summary.pdf");
```

### Output yang diharapkan

Saat Anda menjalankan program, konsol akan menampilkan sesuatu yang mirip dengan:

```
=== PDF Summary ===
This document is a PDF/X‑4 file generated from source.pdf. It includes a custom graphics state named MyGs with stroke opacity 0.7 and fill opacity 0.5. The file complies with PDF/X‑4 standards and is ready for high‑quality printing.
```

File `summary.pdf` berisi teks yang sama yang dirender sebagai halaman PDF, memudahkan berbagi dengan pemangku kepentingan yang lebih menyukai format visual.

## Kode sumber lengkap (siap salin‑tempel)

```csharp
using System;
using System.Collections.Generic;
using System.Threading.Tasks;
using Aspose.Pdf;
using Aspose.Pdf.AI;

class Program
{
    static async Task Main()
    {
        // Step 1: Load the source PDF
        Document sourceDoc = new Document("YOUR_DIRECTORY/source.pdf");

        // Step 2: Convert the document to PDF/X‑4 format
        var conversionOptions = new PdfFormatConversionOptions
        {
            PdfXVersion = PdfXVersion.PDFX4
        };
        sourceDoc.Convert(conversionOptions);

        // Step 3: Save the converted PDF/X‑4 file
        sourceDoc.Save("YOUR_DIRECTORY/converted-pdfx4.pdf");

        // Step 4: Add a custom ExtGState to the first page
        var firstPage = sourceDoc.Pages[1];
        var resourcesEditor = new DictionaryEditor(firstPage.Resources);
        var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();

        var customGs = CosPdfDictionary.CreateEmptyDictionary(sourceDoc);
        customGs.Add("CA", new CosPdfNumber(0.7)); // stroke opacity
        customGs.Add("ca", new CosPdfNumber(0.5)); // fill opacity

        extGStateDict.Add("MyGs", customGs);

        // Step 5: Save the PDF with the new graphics state
        sourceDoc.Save("YOUR_DIRECTORY/with-gs.pdf");

        // Step 6: Set up the AI client and summary options
        var aiClient = OpenAIClient.CreateWithApiKey("YOUR_API_KEY").Build();
        var summaryOptions = OpenAISummaryCopilotOptions.Create()
                              .WithTemperature(0.4)
                              .WithDocument("YOUR_DIRECTORY/converted-pdfx4.pdf");

        // Step 7: Generate a summary and save it as a PDF
        var summaryCopilot = AICopilotFactory.CreateSummaryCopilot(aiClient, summaryOptions);
        string summaryText = await summaryCopilot.GetSummaryAsync();
        Console.WriteLine("=== PDF Summary ===\n" + summaryText);
        await summaryCopilot.SaveSummaryAsync("YOUR_DIRECTORY/summary.pdf");
    }
}
```

Kode ini berdiri sendiri; ganti `YOUR_DIRECTORY` dan `YOUR_API_KEY` dengan jalur serta kunci Anda yang sebenarnya, lalu jalankan proyek.

## Variasi umum dan kasus tepi

| Situasi | Penyesuaian |
|-----------|------------|
| **PDF sumber dilindungi password** | Berikan password ke konstruktor `Document`: `new Document(path, new LoadOptions { Password = "pwd" })`. |
| **Anda membutuhkan PDF/A‑2b alih‑alih PDF/X‑4** | Ubah `PdfXVersion.PDFX4` menjadi `PdfAStandard.PdfA2b` dan gunakan `PdfAConversionOptions`. |
| **Beberapa halaman membutuhkan objek ExtGState yang berbeda** | Loop melalui `sourceDoc.Pages` dan buat kamus terpisah untuk sumber daya masing‑masing halaman. |
| **Temperatur lebih tinggi untuk ringkasan yang lebih kreatif** | Set `.WithTemperature(0.8)`; AI akan menyertakan bahasa yang lebih interpretatif. |
| **Menjalankan dalam konteks non‑async** | Ganti pemanggilan `await` dengan `.Result` atau gunakan `GetSummaryAsync().GetAwaiter().GetResult()`, namun waspadai potensi deadlock. |

## Tips dan praktik terbaik (E‑E‑A‑T)

- **Pro tip:** Jaga objek `sourceDoc` tetap hidup hingga Anda menyimpan setiap file turunan. Membuangnya terlalu cepat akan membuang perubahan yang belum disimpan.
- **Waspadai:** Menimpa PDF asli secara tidak sengaja. Selalu tulis ke nama file baru kecuali Anda memang ingin mengganti sumber.
- **Catatan kinerja:** Mengonversi PDF besar ke PDF/X‑4 dapat memakan banyak memori. Jika Anda memproses file > 100 MB, pertimbangkan meningkatkan ukuran heap proses atau memproses halaman secara batch.
- **Pengingat keamanan:** Jangan pernah menuliskan kunci API OpenAI secara hard‑code dalam kode produksi; gunakan variabel lingkungan atau manajer rahasia yang aman.

## Kesimpulan

Anda kini tahu cara **membuat dokumen PDF/X‑4 C#**, mengonversi PDF ke PDFX4, menambahkan custom graphics state, dan menghasilkan ringkasan berbasis AI—semua dengan Aspose.Pdf untuk .NET. Contoh lengkap yang dapat dijalankan memperlihatkan alur kerja penuh dari file sumber hingga PDF ringkasan akhir.

Selanjutnya, Anda dapat mengeksplorasi:

- Menambahkan gambar atau watermark menggunakan `ExtGState` yang sama untuk efek transparansi.  
- Mengonversi ke standar PDF lain seperti PDF/A‑2b (alur kerja bergaya **convert pdf to pdfx4**).  
- Mengintegrasikan fitur AI Aspose.Pdf lainnya seperti ekstraksi konten atau terjemahan.

Silakan bereksperimen dengan kode, sesuaikan nilai graphics state, atau ubah temperatur AI agar cocok dengan kebutuhan proyek Anda. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan menjelajahi pendekatan implementasi alternatif dalam proyek Anda.

- [Create PDF Document with Aspose.PDF – Step‑by‑Step Guide](/pdf/english/net/document-creation/create-pdf-document-with-aspose-pdf-step-by-step-guide/)
- [Create Tagged PDFs with Aspose.PDF for .NET: A Complete Guide to Enhancing Accessibility and Document Structure](/pdf/english/net/advanced-features/create-tagged-pdfs-aspose-pdf-net/)
- [How to Convert PDF Page Size to A4 Using Aspose.PDF .NET | Document Manipulation Guide](/pdf/english/net/document-manipulation/update-pdf-page-dimensions-aspose-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}