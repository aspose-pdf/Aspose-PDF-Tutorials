---
category: general
date: 2026-09-28
description: Inisialisasi klien OpenAI di C# dan rangkum PDF dengan AI, mengekstrak
  ringkasan singkat serta mengonversinya menjadi file PDF.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- initialize openai client
- summarize pdf with ai
- extract summary from pdf
- convert summary to pdf
- create summary copilot
language: id
lastmod: 2026-09-28
og_description: Inisialisasi klien OpenAI di C# untuk meringkas PDF dengan AI, mengekstrak
  ringkasan, dan mengonversinya menjadi PDF menggunakan Aspose.Pdf.AI.
og_image_alt: Code editor view showing how to initialize OpenAI client in C#
og_title: Inisialisasi klien OpenAI & rangkum PDF dengan AI – panduan langkah demi
  langkah
schemas:
- author: Aspose
  dateModified: '2026-09-28'
  description: Initialize OpenAI client in C# and summarize PDF with AI, extracting
    a concise summary and converting it to a PDF file.
  headline: How to initialize OpenAI client and summarize PDF with AI
  type: TechArticle
tags:
- OpenAI
- C#
- PDF processing
title: Cara menginisialisasi klien OpenAI dan merangkum PDF dengan AI
url: /id/net/document-creation/how-to-initialize-openai-client-and-summarize-pdf-with-ai/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara menginisialisasi OpenAI client dan merangkum PDF dengan AI

Jika Anda perlu **initialize OpenAI client** dalam proyek .NET dan **summarize PDF with AI**, panduan ini memberikan solusi lengkap yang dapat dijalankan. Anda akan belajar cara menyiapkan klien, membuat summary copilot, mengekstrak ringkasan singkat dari PDF, dan akhirnya **convert summary to PDF**—semua dengan kode yang jelas dan penjelasan.

Tutorial ini mencakup semua hal mulai dari paket NuGet yang diperlukan hingga penanganan panggilan async, sehingga Anda dapat menyalin‑tempel program akhir ke dalam solusi Anda sendiri dan melihat hasilnya segera.

## Prasyarat

* .NET 6.0 atau yang lebih baru terinstal  
* Kunci API OpenAI (Anda dapat memperoleh satu dari portal OpenAI)  
* Paket NuGet **Aspose.Pdf.AI** – instal dengan  

```bash
dotnet add package Aspose.Pdf.AI
```

Tidak ada layanan eksternal tambahan yang diperlukan; kode berjalan sepenuhnya secara lokal setelah kunci API diberikan.

## Langkah 1: Initialize OpenAI client

Operasi pertama adalah **initialize OpenAI client**. Ini membuat HTTP client yang dapat digunakan kembali yang menangani otentikasi dan pembatasan permintaan untuk Anda.

```csharp
using var openAiClient = Aspose.Pdf.AI.OpenAIClient
    .CreateWithApiKey(Environment.GetEnvironmentVariable("OPENAI_API_KEY"))
    .Build();
```

*Mengapa ini penting*: Menginisialisasi klien sekali dan menggunakannya kembali menghindari handshake berulang, mengurangi latensi, dan memastikan kunci API Anda tidak pernah ditulis keras dalam kontrol sumber.

> **Pro tip**: Simpan kunci API dalam variabel lingkungan atau secret manager. Jangan pernah meng-commit-nya ke kontrol sumber.

## Langkah 2: Configure summary copilot options

Selanjutnya, Anda perlu memberi tahu AI apa yang harus dirangkum dan bagaimana. Objek opsi memungkinkan Anda mengatur temperature (mengontrol keberacakan) dan menunjuk ke PDF sumber.

```csharp
var summaryOptions = Aspose.Pdf.AI.OpenAISummaryCopilotOptions.Create()
    .WithTemperature(0.5)                     // Balanced creativity vs. factuality
    .WithDocument("YOUR_DIRECTORY/SampleDocument.pdf"); // Path to the PDF you want to summarize
```

*Mengapa ini penting*: Menyesuaikan temperature membantu Anda mendapatkan ringkasan deterministik saat Anda **extract summary from PDF**. Nilai 0.5 adalah default yang baik untuk kebanyakan dokumen bisnis.

## Langkah 3: Create summary copilot

Sekarang Anda **create summary copilot** dengan menggabungkan klien yang diinisialisasi dengan opsi yang baru saja Anda atur. Copilot mengabstraksi penanganan permintaan tingkat rendah.

```csharp
var summaryCopilot = Aspose.Pdf.AI.AICopilotFactory
    .CreateSummaryCopilot(openAiClient, summaryOptions);
```

*Mengapa ini penting*: Pola copilot mengikuti prinsip single‑responsibility—kode Anda hanya menangani aksi tingkat tinggi seperti “GetSummaryAsync” alih-alih membangun payload HTTP mentah.

## Langkah 4: Generate the summary text asynchronously

Memanggil `GetSummaryAsync` mengirim PDF ke OpenAI, menjalankan model summarization, dan mengembalikan ringkasan teks biasa.

```csharp
string summaryText = await summaryCopilot.GetSummaryAsync();
Console.WriteLine("=== Extracted Summary ===");
Console.WriteLine(summaryText);
```

Pada titik ini Anda telah **extracted summary from PDF** dalam variabel string. Output tipikal terlihat seperti:

```
=== Extracted Summary ===
This report outlines the quarterly revenue growth of 12% across all regions, highlights key product launches, and recommends strategic investments in cloud infrastructure.
```

## Langkah 5: Convert summary to PDF

Langkah terakhir adalah **convert summary to PDF** sehingga Anda dapat membagikan atau mengarsipkannya seperti dokumen lainnya. Copilot menyediakan metode `SaveSummaryAsync` yang nyaman.

```csharp
await summaryCopilot.SaveSummaryAsync("YOUR_DIRECTORY/Summary_out.pdf");
Console.WriteLine("Summary saved to Summary_out.pdf");
```

*Mengapa ini penting*: Menyimpan ringkasan sebagai PDF mempertahankan format, memudahkan melampirkannya ke email, dan menjaga semuanya dalam ekosistem dokumen yang sama yang sudah Anda gunakan.

## Contoh lengkap yang berfungsi

Berikut adalah aplikasi console lengkap yang menyatukan semua komponen. Ganti `YOUR_DIRECTORY` dan atur variabel lingkungan `OPENAI_API_KEY` sebelum menjalankan.

```csharp
// Program.cs
using System;
using System.Threading.Tasks;
using Aspose.Pdf.AI;

class Program
{
    static async Task Main()
    {
        // 1️⃣ Initialize the OpenAI client
        using var openAiClient = OpenAIClient
            .CreateWithApiKey(Environment.GetEnvironmentVariable("OPENAI_API_KEY"))
            .Build();

        // 2️⃣ Set up summary copilot options (temperature and source document)
        var summaryOptions = OpenAISummaryCopilotOptions.Create()
            .WithTemperature(0.5)
            .WithDocument("YOUR_DIRECTORY/SampleDocument.pdf");

        // 3️⃣ Create the summary copilot
        var summaryCopilot = AICopilotFactory
            .CreateSummaryCopilot(openAiClient, summaryOptions);

        // 4️⃣ Generate the summary text asynchronously
        string summaryText = await summaryCopilot.GetSummaryAsync();
        Console.WriteLine("=== Extracted Summary ===");
        Console.WriteLine(summaryText);

        // 5️⃣ Save the generated summary as a PDF file
        await summaryCopilot.SaveSummaryAsync("YOUR_DIRECTORY/Summary_out.pdf");
        Console.WriteLine("Summary saved to Summary_out.pdf");
    }
}
```

### Output yang diharapkan

```
=== Extracted Summary ===
[Your concise summary here]

Summary saved to Summary_out.pdf
```

Buka `Summary_out.pdf` di penampil PDF apa pun—Anda akan melihat teks yang sama, kini diformat sebagai dokumen PDF yang tepat.

## Variasi umum dan kasus tepi

| Situasi | Cara menyesuaikan kode |
|-----------|----------------------|
| **PDF besar (> 10 MB)** | Tingkatkan timeout dengan menambahkan `.WithTimeout(TimeSpan.FromMinutes(5))` ke `summaryOptions`. |
| **Prompt khusus** | Gunakan `.WithPrompt("Provide a bullet‑point summary focusing on financial metrics.")`. |
| **Beberapa PDF** | Lakukan loop pada daftar jalur file, membuat `summaryCopilot` baru untuk masing‑masing atau menggunakan kembali klien yang sama dengan opsi yang berbeda. |
| **Dokumen non‑Inggris** | Setel `.WithLanguage("es")` untuk meminta model merangkum dalam bahasa Spanyol. |
| **Menyimpan dalam format lain** | Setelah `GetSummaryAsync`, Anda dapat menggunakan perpustakaan PDF apa pun (mis., iTextSharp) untuk membuat PDF, tetapi `SaveSummaryAsync` sudah menangani kasus paling umum. |

## Tips untuk penggunaan produksi

* **Rate limiting** – OpenAI menegakkan kuota permintaan. Gunakan kembali instance `openAiClient` yang sama di beberapa rangkuman untuk tetap dalam batas.  
* **Error handling** – Bungkus panggilan async dalam blok `try/catch` dan periksa `OpenAIException` untuk kesalahan throttling atau otentikasi.  
* **Security** – Jangan pernah mencatat (log) kunci API mentah. Gunakan penyimpanan rahasia yang aman (Azure Key Vault, AWS Secrets Manager, dll.).  
* **Testing** – Mock `OpenAIClient` dengan implementasi palsu jika Anda membutuhkan unit test yang tidak mengakses API live.  

## Kesimpulan

Anda sekarang tahu cara **initialize OpenAI client**, **create summary copilot**, **extract summary from PDF**, dan **convert summary to PDF** menggunakan Aspose.Pdf.AI dalam C#. Contoh lengkap berjalan end‑to‑end, memberikan Anda solusi siap pakai untuk alur kerja rangkuman dokumen apa pun.

Selanjutnya, Anda mungkin ingin menjelajahi:

* **Summarize PDF with AI** untuk pemrosesan batch arsip  
* Menambahkan **metadata** (penulis, tanggal) ke PDF yang dihasilkan  
* Mengintegrasikan langkah rangkuman ke dalam **pipeline manajemen dokumen** yang lebih besar  

Silakan bereksperimen dengan nilai temperature, prompt khusus, atau rangkuman multibahasa untuk menyesuaikan output dengan domain spesifik Anda. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Ekstrak & Konversi Region PDF ke Gambar dengan Aspose.PDF](/pdf/english/net/images-graphics/extract-convert-pdf-regions-aspose-net/)
- [Ekstrak Konversi Region PDF Aspose Net](/pdf/german/net/images-graphics/extract-convert-pdf-regions-aspose-net/)
- [Ekstrak Konversi Region PDF Aspose Net](/pdf/french/net/images-graphics/extract-convert-pdf-regions-aspose-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}