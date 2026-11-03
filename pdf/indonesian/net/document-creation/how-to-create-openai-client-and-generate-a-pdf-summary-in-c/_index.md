---
category: general
date: 2026-10-10
description: Buat klien OpenAI dalam C# dan pelajari cara merangkum PDF, mengonversi
  PDF menjadi ringkasan, serta menyimpan ringkasan PDF yang dihasilkan dengan Aspose.Pdf.AI.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create openai client
- convert pdf to summary
- how to summarize pdf
- how to save summary
- generate pdf summary
language: id
lastmod: 2026-10-10
og_description: Buat klien OpenAI di C# dan segera pelajari cara meringkas PDF, mengonversi
  PDF menjadi ringkasan, serta menyimpan ringkasan PDF yang dihasilkan.
og_image_alt: Screenshot of C# code that creates an OpenAI client and generates a
  PDF summary
og_title: Buat klien OpenAI dan hasilkan ringkasan PDF dalam C# – panduan langkah
  demi langkah
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Create OpenAI client in C# and learn how to summarize a PDF, convert
    PDF to summary, and save the generated PDF summary with Aspose.Pdf.AI.
  headline: How to create OpenAI client and generate a PDF summary in C#
  type: TechArticle
- description: Create OpenAI client in C# and learn how to summarize a PDF, convert
    PDF to summary, and save the generated PDF summary with Aspose.Pdf.AI.
  name: How to create OpenAI client and generate a PDF summary in C#
  steps:
  - name: '**Console output** – the plain‑text summary displayed on the screen.'
    text: '**Console output** – the plain‑text summary displayed on the screen.'
  - name: '**`Summary_out.pdf`** – a downloadable PDF containing the same summary,
      ready for distribution.'
    text: '**`Summary_out.pdf`** – a downloadable PDF containing the same summary,
      ready for distribution.'
  - name: Lower the `WithTemperature` to 0.2 for more deterministic output.
    text: Lower the `WithTemperature` to 0.2 for more deterministic output.
  - name: Increase the
    text: Increase the
  type: HowTo
tags:
- OpenAI
- C#
- PDF processing
- Aspose.Pdf.AI
title: Cara membuat klien OpenAI dan menghasilkan ringkasan PDF dalam C#
url: /id/net/document-creation/how-to-create-openai-client-and-generate-a-pdf-summary-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Membuat Klien OpenAI dan Menghasilkan Ringkasan PDF di C#

Jika Anda perlu **membuat klien OpenAI** dalam aplikasi .NET, tutorial ini menunjukkan secara tepat cara melakukannya dan bagaimana mengubah PDF apa pun menjadi ringkasan singkat yang dihasilkan AI. Anda akan melihat cara **mengonversi PDF ke ringkasan**, mengambil teksnya, dan **menyimpan ringkasan** sebagai file PDF baru—semua dengan Aspose.Pdf.AI.

Meringkas PDF adalah kebutuhan umum untuk alur kerja yang banyak berisi dokumen seperti peninjauan hukum, agregasi riset, atau pembuatan laporan otomatis. Pada akhir panduan ini Anda akan dapat **menghasilkan ringkasan PDF** secara programatis, tanpa meninggalkan basis kode C# Anda.

## Apa yang Anda Butuhkan

- .NET 6.0 atau yang lebih baru (contoh ini menargetkan .NET 6, tetapi versi .NET terbaru mana pun dapat digunakan)
- Paket NuGet Aspose.Pdf.AI (`Aspose.Pdf.AI`) – pembungkus ini menyederhanakan panggilan OpenAI untuk konten PDF
- Kunci API OpenAI yang valid (Anda dapat memperolehnya dari portal OpenAI)
- File PDF contoh yang ingin Anda ringkas (misalnya, `SampleDocument.pdf`)
- Visual Studio 2022, VS Code, atau IDE apa pun yang mendukung pengembangan C#

> **Pro tip:** Simpan kunci API Anda di lokasi yang aman seperti [user‑secrets](https://learn.microsoft.com/en-us/aspnet/core/security/app-secrets) atau Azure Key Vault. Jangan pernah menuliskannya secara hard‑code dalam kontrol sumber.

## Langkah 1: Instal paket NuGet Aspose.Pdf.AI

Buka terminal di folder proyek Anda dan jalankan:

```bash
dotnet add package Aspose.Pdf.AI
```

Paket ini akan mengunduh klien HTTP yang diperlukan, alat manipulasi PDF, dan pembungkus tipis di sekitar API OpenAI. Setelah instalasi, pulihkan proyek untuk memastikan semua dependensi tersedia:

```bash
dotnet restore
```

## Langkah 2: **Buat klien OpenAI** dengan kunci API Anda

Membuat klien adalah langkah pertama untuk setiap operasi PDF berbasis AI. `OpenAIClient` menangani otentikasi, throttling permintaan, dan pooling koneksi untuk Anda.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.AI;
using System;
using System.Threading.Tasks;

class PdfSummarizer
{
    // Replace with your real key – never commit it to source control
    private const string ApiKey = "YOUR_OPENAI_API_KEY";

    public static async Task Main()
    {
        // ---- Step 2: create OpenAI client ----
        using var openAiClient = OpenAIClient
            .CreateWithApiKey(ApiKey)
            .Build();

        // The client is now ready for any Aspose.Pdf.AI operation.
        await SummarizePdfAsync(openAiClient);
    }
}
```

> **Mengapa ini penting:** Pernyataan `using` menjamin klien dibuang dengan benar, melepaskan sumber daya jaringan dan menghindari kehabisan soket pada layanan yang berjalan lama.

## Langkah 3: Konfigurasikan opsi ringkasan – **konversi PDF ke ringkasan**

Objek `OpenAISummaryCopilotOptions` memberi tahu AI apa yang harus dilakukan. Anda dapat menyesuaikan temperature, membatasi penggunaan token, dan yang paling penting, menunjuk ke PDF sumber.

```csharp
private static async Task SummarizePdfAsync(OpenAIClient client)
{
    // ---- Step 3: set up summary options (convert PDF to summary) ----
    var summaryOptions = OpenAISummaryCopilotOptions
        .Create()
        .WithTemperature(0.5)                     // Balanced creativity vs. factuality
        .WithDocument("YOUR_DIRECTORY/SampleDocument.pdf");

    // The options are immutable; each call returns a new instance.
```

### Mengapa temperature 0.5?

Temperature 0.5 menghasilkan bahasa yang singkat dan akurat sambil tetap memungkinkan model untuk merumuskan ulang kalimat. Nilai yang lebih tinggi (misalnya 0.9) membuat output lebih kreatif tetapi dapat menyimpang dari makna asli—tidak diinginkan untuk ringkasan hukum atau teknis.

## Langkah 4: **Cara merangkum PDF** – buat copilot dan dapatkan teksnya

Setelah klien dan opsi siap, buat summary copilot. Objek ini mengatur permintaan ke OpenAI dan mengembalikan hasil dalam beberapa format.

```csharp
    // ---- Step 4: instantiate the summary copilot (how to summarize PDF) ----
    var summaryCopilot = AICopilotFactory
        .CreateSummaryCopilot(client, summaryOptions);

    // Retrieve the generated summary as plain text
    string summaryText = await summaryCopilot.GetSummaryAsync();

    Console.WriteLine("=== Text Summary ===");
    Console.WriteLine(summaryText);
```

Metode `GetSummaryAsync` mengembalikan versi teks polos yang bersih yang dapat Anda sematkan di UI, kirim melalui email, atau simpan di basis data.

## Langkah 5: Ambil ringkasan sebagai dokumen PDF

Jika Anda memerlukan versi yang dapat dipindahkan dan dicetak, minta copilot untuk menghasilkan dokumen PDF. Langkah ini memperlihatkan **menghasilkan ringkasan PDF** langsung dari model AI.

```csharp
    // ---- Step 5: retrieve the summary as a PDF document (generate PDF summary) ----
    Document summaryDocument = await summaryCopilot.GetSummaryDocumentAsync();

    // Optionally, you can add a cover page or watermark here before saving.
```

`Aspose.Pdf.Document` yang dikembalikan berperilaku seperti objek PDF lainnya dalam ekosistem Aspose, artinya Anda dapat mengedit halaman lebih lanjut, menambahkan metadata, atau menggabungkannya dengan PDF lain.

## Langkah 6: **Cara menyimpan ringkasan** – persist PDF ke disk

Akhirnya, simpan ringkasan yang dihasilkan ke sistem file. Helper `SaveSummaryAsync` menggabungkan pengambilan dan penyimpanan dalam satu panggilan, tetapi kami juga akan menunjukkan cara menyimpan secara eksplisit untuk melengkapi contoh.

```csharp
    // ---- Step 6: save the summary PDF (how to save summary) ----
    const string outputPath = "YOUR_DIRECTORY/Summary_out.pdf";

    // Direct helper method
    await summaryCopilot.SaveSummaryAsync(outputPath);

    // Or, save the Document object manually
    // summaryDocument.Save(outputPath);
    Console.WriteLine($"Summary PDF saved to: {outputPath}");
}
```

> **Tip:** Jika Anda perlu menerapkan konvensi penamaan (misalnya, file dengan timestamp), bangun path secara programatik dengan `DateTime.UtcNow:yyyyMMdd_HHmmss`.

### Contoh lengkap yang dapat dijalankan

Menggabungkan semuanya, berikut program mandiri yang dapat Anda salin‑tempel ke `Program.cs` dan jalankan:

```csharp
using Aspose.Pdf;
using Aspose.Pdf.AI;
using System;
using System.Threading.Tasks;

class PdfSummarizer
{
    private const string ApiKey = "YOUR_OPENAI_API_KEY";

    public static async Task Main()
    {
        // Create OpenAI client
        using var openAiClient = OpenAIClient
            .CreateWithApiKey(ApiKey)
            .Build();

        // Configure summary options (convert PDF to summary)
        var summaryOptions = OpenAISummaryCopilotOptions
            .Create()
            .WithTemperature(0.5)
            .WithDocument("YOUR_DIRECTORY/SampleDocument.pdf");

        // Instantiate the copilot (how to summarize PDF)
        var summaryCopilot = AICopilotFactory
            .CreateSummaryCopilot(openAiClient, summaryOptions);

        // Get plain‑text summary
        string summaryText = await summaryCopilot.GetSummaryAsync();
        Console.WriteLine("=== Text Summary ===");
        Console.WriteLine(summaryText);

        // Get PDF version (generate PDF summary)
        Document summaryDoc = await summaryCopilot.GetSummaryDocumentAsync();

        // Save the PDF (how to save summary)
        const string outPath = "YOUR_DIRECTORY/Summary_out.pdf";
        await summaryCopilot.SaveSummaryAsync(outPath);
        Console.WriteLine($"Summary PDF saved to: {outPath}");
    }
}
```

Menjalankan program menghasilkan dua artefak:

1. **Output konsol** – ringkasan teks polos yang ditampilkan di layar.
2. **`Summary_out.pdf`** – PDF yang dapat diunduh berisi ringkasan yang sama, siap didistribusikan.

## Variasi umum dan kasus tepi

| Situasi | Penyesuaian yang Disarankan |
|-----------|-------------------|
| **PDF besar (> 10 MB)** | Bagi dokumen menjadi potongan lebih kecil (mis., per bab) dan ringkas tiap potongan secara terpisah. Gabungkan hasilnya dengan `Document.AppendDocument`. |
| **Perlu prompt khusus** | Gunakan `WithPrompt("Summarize the following legal contract in bullet points:")` sebelum memanggil `CreateSummaryCopilot`. |
| **PDF sumber bukan bahasa Inggris** | Setel `WithLanguage("es")` (atau kode ISO yang sesuai) untuk mengarahkan penanganan bahasa model. |
| **Kesalahan rate‑limit** | Tingkatkan `WithRetryCount` atau tambahkan `Task.Delay` di antara panggilan. |
| **Menyimpan ke penyimpanan cloud** | Ganti path sistem file dengan stream (`MemoryStream`) dan unggah stream ke Azure Blob Storage atau AWS S3. |

## Memverifikasi hasil

Setelah program selesai, buka `Summary_out.pdf` di penampil PDF apa pun. Anda akan melihat dokumen bersih satu halaman (atau multi‑halaman, tergantung panjang) yang menangkap ide utama dari `SampleDocument.pdf`. Bandingkan ringkasan teks yang dicetak di konsol dengan versi PDF—keduanya harus cocok secara verbatim.

Jika ringkasan terlihat tidak lengkap:

1. Turunkan `WithTemperature` menjadi 0.2 untuk output yang lebih deterministik.
2. Tingkatkan ...

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [How to Create PDF in C# – Add Page, Draw Rectangle & Save](/pdf/english/net/document-creation/how-to-create-pdf-in-c-add-page-draw-rectangle-save/)
- [Learn How to Generate PDF Documents with Aspose.PDF for .NET](/pdf/english/net/document-creation/)
- [How to Create Tagged PDFs with Aspose.PDF for .NET – Enhance Accessibility](/pdf/english/net/bookmarks-navigation/tagged-pdf-creation-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}