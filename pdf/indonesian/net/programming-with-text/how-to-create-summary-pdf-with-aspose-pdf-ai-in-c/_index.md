---
category: general
date: 2026-09-18
description: Pelajari cara membuat PDF ringkasan menggunakan Aspose.Pdf.AI. Panduan
  ini menunjukkan cara merangkum PDF, mengatur opsi, membuat klien, dan menghasilkan
  ringkasan.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create summary pdf
- how to summarize pdf
- how to create client
- how to set options
- how to generate summary
language: id
lastmod: 2026-09-18
og_description: Buat PDF ringkasan dalam C# dengan Aspose.Pdf.AI. Ikuti tutorial lengkap
  ini untuk merangkum PDF, mengatur opsi, membuat klien, dan menghasilkan ringkasan.
og_image_alt: Screenshot of a C# IDE showing code that creates a summary PDF using
  Aspose.Pdf.AI
og_title: Cara membuat PDF ringkasan dengan Aspose.Pdf.AI – panduan langkah demi langkah
  C#
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: Learn how to create summary PDF using Aspose.Pdf.AI. This guide shows
    how to summarize PDF, set options, create client, and generate the summary.
  headline: How to create summary PDF with Aspose.Pdf.AI in C#
  type: TechArticle
- description: Learn how to create summary PDF using Aspose.Pdf.AI. This guide shows
    how to summarize PDF, set options, create client, and generate the summary.
  name: How to create summary PDF with Aspose.Pdf.AI in C#
  steps:
  - name: How to create client
    text: The first action is to create an `OpenAIClient`. This client wraps the OpenAI
      HTTP calls and handles authentication for you.
  - name: How to set options
    text: Summarization behavior can be tuned with `OpenAISummaryCopilotOptions`.
      The most common parameters are **temperature** (creativity) and the **source
      document** path.
  - name: How to generate summary – instantiate the copilot
    text: With a client and options ready, you can create a **summary copilot**. The
      copilot orchestrates the interaction between the PDF and the OpenAI model.
  - name: Retrieve a plain‑text summary
    text: Often you only need the text version of the summary for logging or UI display.
  - name: Generate a PDF document that contains the summary
    text: If you prefer a portable, printable format, ask the copilot to build a PDF
      for you.
  - name: How to generate summary – save the PDF
    text: Finally, persist the generated summary PDF to disk.
  type: HowTo
tags:
- Aspose.Pdf.AI
- C#
- PDF summarization
title: Cara membuat PDF ringkasan dengan Aspose.Pdf.AI di C#
url: /id/net/programming-with-text/how-to-create-summary-pdf-with-aspose-pdf-ai-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara membuat PDF ringkasan dengan Aspose.Pdf.AI di C#

Jika Anda perlu **membuat file PDF ringkasan** secara otomatis, tutorial ini menunjukkan cara melakukannya secara tepat. Dengan menggunakan Aspose.Pdf.AI Anda dapat **menyimpulkan PDF** dokumen, mengambil ringkasan teks‑plain, dan menghasilkan PDF baru yang hanya berisi informasi terpenting.

Anda akan melewati setiap langkah—dari **cara membuat objek client**, ke **cara mengatur opsi**, hingga **cara menghasilkan file ringkasan** yang dapat Anda simpan atau bagikan. Tidak diperlukan alat eksternal, dan kode dapat dijalankan pada lingkungan .NET 6+ mana pun.

## Apa yang akan Anda pelajari

* Cara menginstansiasi klien OpenAI dengan kunci API Anda.  
* Cara mengonfigurasi opsi summarization seperti temperature dan dokumen sumber.  
* Cara membuat summary copilot dan mengambil ringkasan teks‑plain serta PDF.  
* Cara menyimpan PDF ringkasan yang dihasilkan ke disk.  

Pada akhir panduan ini Anda akan memiliki aplikasi konsol C# (atau aplikasi .NET apa pun) yang berfungsi penuh dan menghasilkan PDF ringkasan singkat dari dokumen input apa pun.

## Prasyarat

| Persyaratan | Alasan |
|-------------|--------|
| .NET 6 SDK atau lebih baru | Diperlukan untuk mengkompilasi dan menjalankan kode C#. |
| Paket NuGet Aspose.Pdf.AI (`Aspose.Pdf.AI`) | Menyediakan `OpenAIClient`, `OpenAISummaryCopilotOptions`, dan API terkait. |
| Kunci API OpenAI yang valid | Layanan bergantung pada model bahasa OpenAI untuk menghasilkan ringkasan. |
| Contoh PDF (`SampleDocument.pdf`) | Dokumen sumber yang ingin Anda ringkas. |

Pasang paket dengan:

```bash
dotnet add package Aspose.Pdf.AI
```

> **Pro tip:** Simpan kunci API Anda di luar kontrol sumber. Simpan dalam variabel lingkungan (`ASPOSE_PDF_AI_KEY`) dan baca pada saat runtime.

## Cara membuat PDF ringkasan – implementasi langkah‑demi‑langkah

Berikut adalah program lengkap yang dapat dijalankan. Setiap bagian menjelaskan **mengapa** kode tersebut diperlukan, bukan hanya **apa** yang dilakukannya.

### Langkah 1: Cara membuat client

Tindakan pertama adalah membuat `OpenAIClient`. Klien ini membungkus panggilan HTTP OpenAI dan menangani otentikasi untuk Anda.

```csharp
using System;
using System.Threading.Tasks;
using Aspose.Pdf;
using Aspose.Pdf.AI;

class Program
{
    // Retrieve the API key from an environment variable for security.
    private static readonly string ApiKey = Environment.GetEnvironmentVariable("ASPOSE_PDF_AI_KEY")
                                            ?? throw new InvalidOperationException("API key not set.");

    static async Task Main()
    {
        // Create the OpenAI client using the provided key.
        await using var openAiClient = OpenAIClient
            .CreateWithApiKey(ApiKey)   // how to create client
            .Build();

        // The client is now ready to be passed to copilot factories.
```

**Mengapa ini penting:**  
`OpenAIClient` mengelola pooling koneksi dan retry. Dengan menggunakan `await using`, Anda memastikan klien dibuang dengan benar, mencegah kebocoran socket.

### Langkah 2: Cara mengatur opsi

Perilaku summarization dapat disesuaikan dengan `OpenAISummaryCopilotOptions`. Parameter yang paling umum adalah **temperature** (kreativitas) dan jalur **dokumen sumber**.

```csharp
        // Configure summarization options.
        var summaryOptions = OpenAISummaryCopilotOptions
            .Create()
            .WithTemperature(0.5)                     // low temperature = more factual output
            .WithDocument("YOUR_DIRECTORY/SampleDocument.pdf"); // how to summarize pdf
```

**Mengapa ini penting:**  
Temperature mengontrol tingkat kebetulan model bahasa. Nilai `0.5` memberikan output seimbang—ringkas namun akurat. Metode `WithDocument` memberi tahu layanan PDF mana yang akan diproses, menghilangkan kebutuhan ekstraksi teks manual.

### Langkah 3: Cara menghasilkan ringkasan – menginstansiasi copilot

Setelah klien dan opsi siap, Anda dapat membuat **summary copilot**. Copilot mengatur interaksi antara PDF dan model OpenAI.

```csharp
        // Instantiate the summary copilot using the client and options.
        ISummaryCopilot copilot = AICopilotFactory.CreateSummaryCopilot(openAiClient, summaryOptions);
```

**Mengapa ini penting:**  
`ISummaryCopilot` menyederhanakan kompleksitas pengiriman PDF ke OpenAI, menerima respons, dan mengonversinya kembali menjadi PDF bila diperlukan. Satu baris ini menggantikan puluhan panggilan HTTP.

### Langkah 4: Mengambil ringkasan teks‑plain

Seringkali Anda hanya membutuhkan versi teks dari ringkasan untuk pencatatan atau tampilan UI.

```csharp
        // Get the plain‑text summary.
        string summaryText = await copilot.GetSummaryAsync(); // how to generate summary
        Console.WriteLine("=== Plain‑text summary ===");
        Console.WriteLine(summaryText);
```

**Output yang diharapkan** (dipotong untuk singkat):

```
=== Plain‑text summary ===
This document outlines the key findings of the 2024 market analysis...
```

**Mengapa ini penting:**  
Metode ini mengembalikan `string` yang dapat Anda simpan di basis data, kirim lewat API, atau tampilkan di halaman web tanpa harus membuat PDF baru.

### Langkah 5: Menghasilkan dokumen PDF yang berisi ringkasan

Jika Anda menginginkan format yang dapat dibawa, dicetak, minta copilot membangun PDF untuk Anda.

```csharp
        // Generate a PDF that contains the summary.
        Document summaryDoc = await copilot.GetSummaryDocumentAsync(); // how to generate summary
```

**Mengapa ini penting:**  
`GetSummaryDocumentAsync` membuat PDF yang sepenuhnya diformat menggunakan mesin rendering Aspose.Pdf, secara otomatis mempertahankan font dan tata letak.

### Langkah 6: Cara menghasilkan ringkasan – menyimpan PDF

Akhirnya, simpan PDF ringkasan yang dihasilkan ke disk.

```csharp
        // Save the summary PDF to a file.
        await copilot.SaveSummaryAsync("YOUR_DIRECTORY/Summary_out.pdf"); // how to generate summary

        Console.WriteLine("Summary PDF saved to YOUR_DIRECTORY/Summary_out.pdf");
    }
}
```

**Mengapa ini penting:**  
`SaveSummaryAsync` menulis file dalam satu panggilan asynchronous, yang optimal untuk aplikasi I/O‑bound seperti layanan web.

## Kode sumber lengkap (siap salin‑tempel)

```csharp
using System;
using System.Threading.Tasks;
using Aspose.Pdf;
using Aspose.Pdf.AI;

class Program
{
    private static readonly string ApiKey = Environment.GetEnvironmentVariable("ASPOSE_PDF_AI_KEY")
                                            ?? throw new InvalidOperationException("API key not set.");

    static async Task Main()
    {
        // Step 1: create client
        await using var openAiClient = OpenAIClient
            .CreateWithApiKey(ApiKey)
            .Build();

        // Step 2: set options (temperature + source PDF)
        var summaryOptions = OpenAISummaryCopilotOptions
            .Create()
            .WithTemperature(0.5)
            .WithDocument("YOUR_DIRECTORY/SampleDocument.pdf");

        // Step 3: instantiate the copilot
        ISummaryCopilot copilot = AICopilotFactory.CreateSummaryCopilot(openAiClient, summaryOptions);

        // Step 4: get plain‑text summary
        string summaryText = await copilot.GetSummaryAsync();
        Console.WriteLine("=== Plain‑text summary ===");
        Console.WriteLine(summaryText);

        // Step 5: generate summary PDF document
        Document summaryDoc = await copilot.GetSummaryDocumentAsync();

        // Step 6: save the summary PDF
        await copilot.SaveSummaryAsync("YOUR_DIRECTORY/Summary_out.pdf");
        Console.WriteLine("Summary PDF saved to YOUR_DIRECTORY/Summary_out.pdf");
    }
}
```

Menjalankan program akan mencetak ringkasan teks ke konsol dan membuat `Summary_out.pdf` yang berisi informasi yang sama dalam PDF yang diformat dengan baik.

## Pertanyaan umum & penanganan kasus tepi

| Pertanyaan | Jawaban |
|------------|---------|
| **Bagaimana jika PDF sumber dilindungi kata sandi?** | Gunakan overload `WithDocument` yang menerima `FileStream` dan tetapkan kata sandi pada `PdfDocument` sebelum mengirimkannya ke copilot. |
| **Bisakah saya mengubah bahasa output?** | Ya. Panggil `.WithLanguage("fr")` (atau kode ISO yang didukung) pada `OpenAISummaryCopilotOptions`. |
| **Bagaimana jika dokumen sangat besar (>100 halaman)?** | Tingkatkan presisi `WithTemperature` atau bagi PDF menjadi potongan lebih kecil dan ringkas tiap potongan secara terpisah, lalu gabungkan hasilnya. |
| **Apakah saya memerlukan koneksi internet?** | Summarization dijalankan di cloud OpenAI, jadi koneksi internet yang stabil diperlukan. |
| **Bagaimana menangani batasan laju API?** | Bungkus panggilan dalam kebijakan retry (misalnya Polly) dengan exponential back‑off. `OpenAIClient` sendiri menghormati header `Retry-After`. |

## Praktik terbaik dan tip

* **Gunakan kembali client** – buat satu `OpenAIClient` untuk seluruh masa hidup aplikasi, bukan per permintaan.  
* **Amankan kunci API** – jangan pernah menuliskannya secara keras; gunakan Azure Key Vault, AWS Secrets Manager, atau variabel lingkungan.  
* **Sesuaikan temperature** – nilai lebih rendah (`0.2‑0.4`) untuk laporan faktual; nilai lebih tinggi (`0.7‑0.9`) untuk abstrak kreatif.  
* **Validasi jalur PDF** – periksa `File.Exists` sebelum memanggil `WithDocument` untuk menghindari error runtime.  
* **Catat ringkasan** – simpan `summaryText` dalam basis data yang dapat dicari untuk analitik di masa mendatang.

## Kesimpulan

Anda kini tahu **cara membuat PDF ringkasan** dengan Aspose.Pdf.AI di C#. Tutorial ini mencakup **cara merangkum PDF**, **cara membuat client**, **cara mengatur opsi**, dan **cara menghasilkan dokumen ringkasan**, memberikan solusi lengkap yang siap produksi.  

Selanjutnya Anda dapat mengeksplorasi fitur lanjutan seperti summarization multibahasa, rekayasa prompt khusus, atau mengintegrasikan pembuatan ringkasan ke dalam API ASP.NET Core. Bereksperimenlah dengan pengaturan temperature dan ukuran dokumen yang berbeda untuk menemukan titik optimal bagi kasus penggunaan Anda.

Selamat coding, dan nikmati mengubah PDF tebal menjadi ringkasan yang singkat dan dapat dibagikan!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [How to Create Tagged PDFs with Aspose.PDF for .NET&#58; An Advanced Guide](/pdf/english/net/advanced-features/creating-tagged-pdfs-aspose-pdf-dotnet/)
- [How to Create a PDF Portfolio Using Aspose.PDF for .NET&#58; A Comprehensive Guide](/pdf/english/net/pdf-portfolios/create-pdf-portfolio-aspose-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}