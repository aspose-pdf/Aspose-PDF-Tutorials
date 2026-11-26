---
category: general
date: 2026-11-25
description: Buat klien OpenAI dalam C# dan hasilkan ringkasan PDF dari dokumen sumber.
  Pelajari cara mengonversi PDF menjadi ringkasan, membuat copilot ringkasan, dan
  menyimpan ringkasan PDF.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create openai client
- generate pdf summary
- convert pdf to summary
- create summary copilot
- save pdf summary
language: id
lastmod: 2026-11-25
og_description: Buat klien OpenAI dalam C# dan hasilkan ringkasan PDF dari dokumen
  sumber. Ikuti panduan langkah demi langkah ini untuk mengonversi PDF menjadi ringkasan,
  membuat copilot ringkasan, dan menyimpan ringkasan PDF.
og_image_alt: Screenshot showing C# code that creates an OpenAI client and saves a
  PDF summary
og_title: Buat klien OpenAI dan hasilkan ringkasan PDF dalam C#
schemas:
- author: Aspose
  dateModified: '2026-11-25'
  description: Create OpenAI client in C# and generate a PDF summary from a source
    document. Learn how to convert PDF to summary, create summary copilot, and save
    PDF summary.
  headline: How to create OpenAI client and generate PDF summary in C#
  type: TechArticle
tags:
- OpenAI
- C#
- PDF summary
- Aspose.Pdf.AI
title: Cara membuat klien OpenAI dan menghasilkan ringkasan PDF dalam C#
url: /id/net/document-creation/how-to-create-openai-client-and-generate-pdf-summary-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara membuat klien OpenAI dan menghasilkan ringkasan PDF di C#

Jika Anda perlu **create OpenAI client** untuk tugas pemrosesan dokumen, panduan ini menunjukkan solusi lengkap end‑to‑end. Anda akan melihat cara mengonversi file PDF menjadi ringkasan singkat, mengambil ringkasan baik sebagai teks biasa maupun sebagai PDF baru, dan akhirnya menyimpan PDF ringkasan tersebut ke disk.

Membuat ringkasan PDF adalah kebutuhan umum ketika Anda ingin mengotomatisasi ekstraksi laporan, membuat briefing eksekutif, atau sekadar mereduksi dokumen besar menjadi poin‑poin utama. Contoh kode di bawah ini menggunakan Aspose.Pdf.AI, yang membungkus API OpenAI dan menyediakan *summary copilot* yang nyaman untuk file PDF.

## Prerequisites

Sebelum memulai, pastikan Anda memiliki:

- .NET 6.0 atau yang lebih baru terpasang  
- Paket NuGet Aspose.Pdf.AI (`Aspose.Pdf.AI`) yang sudah ditambahkan ke proyek Anda  
- Kunci API OpenAI yang aktif (Anda dapat memperolehnya dari portal OpenAI)  
- File PDF yang ingin Anda ringkas (misalnya `input.pdf` yang ditempatkan di folder yang diketahui)

Tutorial ini mengasumsikan Anda menggunakan Visual Studio, tetapi IDE C# apa pun dapat dipakai.

## Create OpenAI client in C#

Langkah pertama adalah **create OpenAI client** dengan kunci API Anda. Objek klien mengelola otentikasi dan routing permintaan untuk semua operasi AI selanjutnya.

```csharp
// Step 1: Initialize the OpenAI client with your API key
using var openAiClient = Aspose.Pdf.AI.OpenAIClient
    .CreateWithApiKey("YOUR_API_KEY")
    .Build();
```

*Mengapa ini penting*: `OpenAIClient` mengenkapsulasi lapisan HTTP, menangani perpanjangan token, dan memastikan semua panggilan ke layanan ringkasan terotorisasi dengan benar. Dengan menggunakan `using var`, klien secara otomatis dibuang ketika metode selesai, sehingga sumber daya dibebaskan dengan cepat.

## Configure summary options (convert PDF to summary)

Selanjutnya Anda mengonfigurasi bagaimana AI harus memperlakukan dokumen sumber. Opsi‑opsi ini memungkinkan Anda mengatur *temperature* (yang mengontrol tingkat keberacakan) dan menunjuk ke PDF yang ingin diringkas.

```csharp
// Step 2: Configure summary options (temperature and source document)
var summaryOptions = Aspose.Pdf.AI.OpenAISummaryCopilotOptions.Create()
    .WithTemperature(0.5)                     // Balanced creativity vs. factuality
    .WithDocument("YOUR_DIRECTORY/input.pdf"); // Path to the PDF you want to summarise
```

*Mengapa ini penting*: Menetapkan temperature sedang (0.5) memberi Anda ringkasan yang andal dan singkat tanpa halusinasi yang dapat muncul pada nilai yang lebih tinggi. Pemanggilan `WithDocument` memberi tahu copilot file mana yang harus dibaca, secara efektif **convert PDF to summary**.

## Build the summary copilot (create summary copilot)

Dengan klien dan opsi yang siap, Anda kini dapat **create summary copilot**. Objek copilot mengekspos metode async untuk mengambil ringkasan dalam berbagai format.

```csharp
// Step 3: Create the summary copilot using the client and options
var summaryCopilot = Aspose.Pdf.AI.AICopilotFactory
    .CreateSummaryCopilot(openAiClient, summaryOptions);
```

*Mengapa ini penting*: Pola factory memisahkan logika pembuatan, memungkinkan Anda mengganti implementasi di kemudian hari (misalnya, copilot mock untuk pengujian unit). `summaryCopilot` yang dihasilkan menjadi gerbang utama untuk semua operasi ringkasan.

## Retrieve the plain‑text summary

Jika Anda hanya membutuhkan konten teks, panggil `GetSummaryAsync`. Metode ini mengembalikan string yang dapat Anda tampilkan, log, atau proses lebih lanjut.

```csharp
// Step 4: Retrieve the plain‑text summary
string plainTextSummary = await summaryCopilot.GetSummaryAsync();
Console.WriteLine("=== Plain‑text summary ===");
Console.WriteLine(plainTextSummary);
```

*Output yang diharapkan*: Sebuah paragraf singkat (atau beberapa poin bullet) yang menangkap esensi `input.pdf`. Pilihan kata tepatnya bergantung pada dokumen sumber, tetapi panjangnya biasanya di bawah 200 kata untuk laporan 10 halaman standar.

## Retrieve the summary as a PDF document (generate pdf summary)

Ketika Anda memerlukan artefak yang dapat dibagikan, minta copilot versi PDF dari ringkasan. Langkah ini **generate pdf summary** langsung dari layanan AI.

```csharp
// Step 5: Retrieve the summary as a PDF document
var pdfSummary = await summaryCopilot.GetSummaryDocumentAsync();
```

`pdfSummary` adalah objek `Aspose.Pdf.Document`, siap untuk manipulasi lebih lanjut (misalnya menambahkan halaman sampul) atau penyimpanan langsung.

## Save the PDF summary to a file (save pdf summary)

Akhirnya, persisten PDF yang dihasilkan menggunakan metode bantuan copilot. Ini mendemonstrasikan operasi **save pdf summary** dalam satu baris kode.

```csharp
// Step 6: Save the PDF summary to a file
await summaryCopilot.SaveSummaryAsync("YOUR_DIRECTORY/Summary_out.pdf");
Console.WriteLine("PDF summary saved to YOUR_DIRECTORY/Summary_out.pdf");
```

*Mengapa ini penting*: Metode `SaveSummaryAsync` menulis dokumen menggunakan mesin PDF berperforma tinggi milik Aspose, mempertahankan font, tata letak, dan metadata. File yang disimpan dapat dibuka di penampil PDF apa pun.

## Full working example

Berikut adalah program lengkap yang menyatukan semua bagian. Salin kode ke proyek konsol baru dan ganti nilai placeholder (`YOUR_API_KEY`, `YOUR_DIRECTORY`) dengan data yang sebenarnya.

```csharp
using System;
using System.Threading.Tasks;
using Aspose.Pdf.AI;

class Program
{
    static async Task Main()
    {
        // Initialize the OpenAI client
        using var openAiClient = OpenAIClient
            .CreateWithApiKey("YOUR_API_KEY")
            .Build();

        // Configure options for summarizing a PDF
        var summaryOptions = OpenAISummaryCopilotOptions.Create()
            .WithTemperature(0.5)
            .WithDocument("YOUR_DIRECTORY/input.pdf");

        // Create the summary copilot
        var summaryCopilot = AICopilotFactory
            .CreateSummaryCopilot(openAiClient, summaryOptions);

        // Get plain‑text summary
        string plainText = await summaryCopilot.GetSummaryAsync();
        Console.WriteLine("=== Plain‑text summary ===");
        Console.WriteLine(plainText);

        // Get PDF version of the summary
        var pdfDoc = await summaryCopilot.GetSummaryDocumentAsync();

        // Save the PDF summary
        await summaryCopilot.SaveSummaryAsync("YOUR_DIRECTORY/Summary_out.pdf");
        Console.WriteLine("PDF summary saved to YOUR_DIRECTORY/Summary_out.pdf");
    }
}
```

### Expected result

Menjalankan program akan mencetak ringkasan teks biasa ke konsol dan membuat `Summary_out.pdf` di folder target. Membuka PDF menampilkan dokumen bersih dan terformat yang berisi teks ringkasan yang sama, siap untuk distribusi.

![Screenshot of the C# code that creates an OpenAI client and saves a PDF summary](openai-pdf-summary.png){.center width="600" alt="Tangkapan layar kode C# yang membuat klien OpenAI dan menyimpan ringkasan PDF"}

## Common questions and edge cases

| Question | Answer |
|----------|--------|
| **What if the source PDF is password‑protected?** | Use `WithDocument` overload that accepts a stream and supply the password via `PdfLoadOptions`. The copilot will decrypt the file before summarizing. |
| **Can I change the summary length?** | Adjust the temperature or add `WithMaxTokens` to `summaryOptions`. Lower token limits produce shorter outputs. |
| **Do I need an internet connection?** | Yes. The copilot calls the OpenAI service over HTTPS, so a stable connection is required. |
| **How to handle large PDFs ( > 100 pages )?** | Split the document into smaller chunks and summarise each chunk separately, then combine the results. This avoids hitting token limits. |
| **Is the generated PDF searchable?** | The PDF contains selectable text because the summary is rendered as text, not as an image. |

## Tips from the field

- **Pro tip:** Cache the `OpenAIClient` instance for the lifetime of your application if you are summarizing many documents. This reduces connection overhead.  
- **Watch out for:** Using a temperature above 0.7 can introduce hallucinated details, which is

## What Should You Learn Next?

The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step‑by‑step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to initialize OpenAI API client in C# with Aspose.Pdf.AI and summarize PDF with AI](/pdf/english/net/document-creation/how-to-initialize-openai-client-and-summarize-pdf-with-ai/)
- [How to convert PDF to summary with Aspose.Pdf.AI in C#](/pdf/english/net/text-operations/how-to-convert-pdf-to-summary-with-aspose-pdf-ai-in-c/)
- [Generate PDF summary with Aspose.Pdf.AI and OpenAI](/pdf/english/net/programming-with-text/generate-pdf-summary-with-aspose-pdf-ai-and-openai/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}