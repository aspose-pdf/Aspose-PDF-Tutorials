---
category: general
date: 2026-10-26
description: Pelajari cara membuat klien OpenAI, mengonversi PDF menjadi ringkasan,
  dan menyimpan PDF ringkasan menggunakan Aspose.Pdf.AI dalam beberapa langkah mudah.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create openai client
- convert pdf to summary
- generate pdf summary
- create summary copilot
- save summary pdf
language: id
lastmod: 2026-10-26
og_description: Buat klien OpenAI dan ubah PDF apa pun menjadi ringkasan singkat.
  Panduan ini menunjukkan cara menghasilkan ringkasan PDF dan menyimpan PDF ringkasan
  menggunakan Aspose.Pdf.AI.
og_image_alt: C# code displaying creation of OpenAI client and PDF summary generation
og_title: Buat klien OpenAI dan hasilkan ringkasan PDF dengan C# – panduan langkah
  demi langkah
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to create OpenAI client, convert PDF to summary and save
    summary PDF using Aspose.Pdf.AI in a few easy steps.
  headline: How to create OpenAI client and generate a PDF summary in C#
  type: TechArticle
tags:
- openai
- pdf
- csharp
- summary
- ai
title: Cara membuat klien OpenAI dan menghasilkan ringkasan PDF dalam C#
url: /id/net/programming-with-text/how-to-create-openai-client-and-generate-a-pdf-summary-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara membuat klien OpenAI dan menghasilkan ringkasan PDF dalam C#

Jika Anda perlu **create OpenAI client** yang dapat membaca PDF dan mengembalikan ringkasan singkat, tutorial ini menunjukkan cara melakukannya secara tepat. Pada akhir panduan Anda akan dapat **convert PDF to summary**, menghasilkan dokumen **generate PDF summary**, dan **save summary PDF** ke disk—semua dengan Aspose.Pdf.AI.

Anda akan melihat contoh lengkap yang dapat dijalankan, penjelasan mengapa setiap baris penting, dan tips untuk menangani jebakan umum seperti file besar atau pengaturan suhu khusus. Tidak diperlukan dokumentasi eksternal; semua yang Anda butuhkan sudah disertakan di sini.

## Prasyarat

* .NET 6.0 atau yang lebih baru terpasang.
* Lisensi Aspose.Pdf untuk .NET (atau percobaan gratis) yang mencakup modul AI.
* Kunci API OpenAI dengan kredit yang cukup untuk permintaan ringkasan.
* Visual Studio 2022 (atau IDE apa pun yang mendukung .NET).

Kode di bawah menargetkan C# 10, tetapi konsep yang sama berlaku untuk versi sebelumnya dengan perubahan sintaks kecil.

## Langkah 1: Buat klien OpenAI

Membuat klien OpenAI adalah dasar dari setiap operasi PDF yang didukung AI. Klien mengenkapsulasi otentikasi, penanganan HTTP, dan pembatasan permintaan, sehingga Anda hanya perlu menyediakan kunci API sekali.

```csharp
using System;
using System.Threading.Tasks;
using Aspose.Pdf;
using Aspose.Pdf.AI;

// Replace with your real key – never hard‑code it in production code.
const string ApiKey = "YOUR_OPENAI_API_KEY";

await using var openAiClient = OpenAIClient
    .CreateWithApiKey(ApiKey)   // supply your OpenAI key
    .Build();                    // builds a reusable HttpClient internally
```

**Mengapa ini penting:**  
* `CreateWithApiKey` memvalidasi format kunci lebih awal, mencegah error runtime 401.  
* `Build()` mengembalikan `IAsyncDisposable` sehingga koneksi HTTP yang mendasari dilepaskan secara otomatis ketika blok `using` berakhir.  
* Menggunakan `await using` memastikan pembuangan asynchronous, yang penting untuk skenario throughput tinggi.

> **Pro tip:** Simpan kunci API dalam variabel lingkungan (`OPENAI_API_KEY`) dan baca dengan `Environment.GetEnvironmentVariable`. Ini menjaga rahasia tetap tidak masuk ke kontrol sumber.

## Langkah 2: Konfigurasikan opsi copilot ringkasan

Copilot ringkasan menentukan bagaimana AI memproses PDF. Anda dapat menyesuaikan kreativitas dengan parameter *temperature* dan menunjuk ke dokumen sumber.

```csharp
var summaryOptions = OpenAISummaryCopilotOptions
    .Create()
    .WithTemperature(0.5)                     // 0 = deterministic, 1 = very creative
    .WithDocument("YOUR_DIRECTORY/input.pdf"); // path to the PDF you want to summarise
```

**Mengapa ini penting:**  
- Suhu `0.5` memberikan output seimbang—cukup variasi untuk terdengar alami namun tetap setia pada sumber.  
- `WithDocument` memuat file ke parser PDF internal Aspose, yang mengekstrak teks, gambar, dan informasi tata letak sebelum mengirimnya ke OpenAI.  
- Jika PDF lebih besar dari 5 MB, pertimbangkan untuk membaginya menjadi bagian‑bagian dan merangkum setiap bagian secara terpisah agar tetap dalam batas token.

## Langkah 3: Buat copilot ringkasan

Sekarang Anda memiliki klien dan opsi, buat instance copilot. Copilot mengabstraksikan siklus permintaan‑respons dan menawarkan metode bantu untuk hasil teks biasa maupun PDF.

```csharp
ISummaryCopilot summaryCopilot = AICopilotFactory
    .CreateSummaryCopilot(openAiClient, summaryOptions);
```

**Mengapa ini penting:**  
- `AICopilotFactory` menjamin bahwa copilot menggunakan pipeline HTTP yang sama dengan klien, mempertahankan pooling koneksi.  
- Antarmuka `ISummaryCopilot` yang dikembalikan memungkinkan Anda mengganti implementasi nanti (misalnya, mock untuk pengujian unit) tanpa mengubah kode di sekitarnya.

## Langkah 4: Dapatkan ringkasan sebagai teks biasa

Jika Anda hanya membutuhkan ringkasan teks—untuk pencatatan, tampilan UI, atau pemrosesan lebih lanjut—panggil `GetSummaryAsync`.

```csharp
string summaryText = await summaryCopilot.GetSummaryAsync();
Console.WriteLine("=== Summary ===");
Console.WriteLine(summaryText);
```

**Apa yang akan Anda lihat:**  
Sebuah paragraf singkat (atau beberapa poin bullet) yang menangkap ide utama dari PDF sumber. Panjangnya tergantung pada dokumen asli dan anggaran token model.

### Menangani output besar

Jika ringkasan lebih panjang dari yang Anda harapkan, Anda dapat membatasi jumlah token dengan `WithMaxTokens` saat membangun `summaryOptions`. Misalnya:

```csharp
summaryOptions = summaryOptions.WithMaxTokens(300);
```

## Langkah 5: Hasilkan ringkasan PDF (convert PDF to summary)

Ketika Anda membutuhkan artefak visual—mungkin untuk dibagikan kepada pemangku kepentingan non‑teknis—gunakan metode pembuatan PDF. Langkah ini **convert pdf to summary** dan **generate pdf summary** dalam satu panggilan.

```csharp
Document summaryDoc = await summaryCopilot.GetSummaryDocumentAsync();
```

Objek `Document` yang dikembalikan adalah dokumen Aspose.Pdf yang lengkap yang berisi teks ringkasan, judul opsional, dan metadata PDF asli (jika Anda mempertahankannya).

**Mengapa ini penting:**  
- PDF mempertahankan kualitas vektor, membuatnya cocok untuk pencetakan atau penyematan dalam laporan lain.  
- Aspose secara otomatis menambahkan halaman judul dengan nama file sumber dan cap waktu, yang membantu jejak audit.

## Langkah 6: Simpan PDF ringkasan (save summary pdf)

Akhirnya, tulis PDF yang dihasilkan ke disk. Pembantu `SaveSummaryAsync` menggabungkan langkah 5 dan 6, tetapi kami akan menunjukkan penyimpanan eksplisit untuk menggambarkan pertimbangan sistem file.

```csharp
string outputPath = "YOUR_DIRECTORY/Summary_out.pdf";
await summaryCopilot.SaveSummaryAsync(outputPath);
Console.WriteLine($"Summary PDF saved to {outputPath}");
```

**Praktik terbaik untuk menyimpan file:**

| Situasi                               | Rekomendasi                                      |
|----------------------------------------|---------------------------------------------------|
| Menjalankan di Windows dan Linux       | Gunakan `Path.Combine` untuk membangun path yang bersifat OS‑agnostic. |
| Beberapa ringkasan bersamaan           | Tambahkan GUID atau cap waktu ke nama file. |
| Layanan yang berjalan lama (mis., web API) | Simpan PDF di penyimpanan blob khusus alih‑alih sistem file lokal. |

## Contoh lengkap yang dapat dijalankan

Berikut adalah program lengkap yang dapat Anda salin‑tempel ke proyek konsol baru (`dotnet new console`). Ini mencakup semua direktif `using` yang diperlukan dan mendemonstrasikan alur lengkap dari **create openai client** hingga **save summary pdf**.

```csharp
// Program.cs
using System;
using System.IO;
using System.Threading.Tasks;
using Aspose.Pdf;
using Aspose.Pdf.AI;

class Program
{
    // Replace with your actual OpenAI key or read from env variables.
    private const string ApiKey = "YOUR_OPENAI_API_KEY";

    static async Task Main()
    {
        // 1️⃣ Create OpenAI client
        await using var openAiClient = OpenAIClient
            .CreateWithApiKey(ApiKey)
            .Build();

        // 2️⃣ Configure summary copilot options
        var summaryOptions = OpenAISummaryCopilotOptions
            .Create()
            .WithTemperature(0.5)
            .WithDocument("YOUR_DIRECTORY/input.pdf"); // path to source PDF

        // 3️⃣ Create the summary copilot
        ISummaryCopilot summaryCopilot = AICopilotFactory
            .CreateSummaryCopilot(openAiClient, summaryOptions);

        // 4️⃣ Get plain‑text summary (optional)
        string summaryText = await summaryCopilot.GetSummaryAsync();
        Console.WriteLine("=== Plain‑text summary ===");
        Console.WriteLine(summaryText);
        Console.WriteLine();

        // 5️⃣ Generate PDF summary (convert pdf to summary)
        Document summaryDoc = await summaryCopilot.GetSummaryDocumentAsync();

        // 6️⃣ Save the generated PDF (save summary pdf)
        string outputPath = Path.Combine("YOUR_DIRECTORY", "Summary_out.pdf");
        await summaryCopilot.SaveSummaryAsync(outputPath);
        Console.WriteLine($"✅ PDF summary saved at: {outputPath}");
    }
}
```

**Output yang diharapkan**

```
=== Plain‑text summary ===
This document outlines the quarterly performance metrics, highlighting a 12% increase in revenue and a 5% reduction in operational costs...

✅ PDF summary saved at: YOUR_DIRECTORY\Summary_out.pdf
```

Buka `Summary_out.pdf` yang dihasilkan dan Anda akan melihat halaman yang diformat rapi berisi teks yang sama, plus header dengan nama file asli dan cap waktu.

## Pertanyaan umum dan kasus tepi

| Question | Answer |
|----------|--------|
| *Bagaimana jika PDF berisi gambar yang dipindai?* | Aspose.Pdf.AI secara otomatis menjalankan OCR ketika `WithDocument` dipanggil, tetapi Anda dapat meningkatkan akurasi dengan mengatur `WithOcrLanguage("eng")`. |
| *Bisakah saya merangkum beberapa PDF dalam satu panggilan?* | Tidak secara langsung. Buat `summaryCopilot` terpisah untuk setiap file atau gabungkan PDF sebelum diringkas. |
| *Bagaimana cara mengubah bahasa output?* | Gunakan `summaryOptions.WithLanguage("fr")` untuk meminta model mengembalikan teks dalam bahasa Prancis. |
| *Bagaimana jika permintaan melebihi batas token?* | Kurangi `WithMaxTokens` atau bagi PDF menjadi beberapa bagian dan rangkum setiap bagian secara terpisah. |
| *Apakah PDF yang dihasilkan dapat dicari?* | Ya. Teks ringkasan disematkan sebagai teks yang dapat dipilih, bukan hanya gambar. |

## Kesimpulan

Anda sekarang tahu cara **create OpenAI client**, mengonfigurasi **create summary copilot**, **convert PDF to summary**, **generate PDF summary**, dan akhirnya **save summary pdf** menggunakan Aspose.Pdf.AI dalam C#. Alur end‑to‑end ini memungkinkan Anda menambahkan ringkasan berbasis AI ke aplikasi .NET apa pun dengan hanya beberapa baris kode.

Langkah selanjutnya yang mungkin Anda jelajahi:

* **Sesuaikan rekayasa prompt** dengan `WithPrompt("Summarise in three bullet points.")`.
* **Integrasikan dengan ASP.NET Core** untuk mengekspos endpoint REST yang mengembalikan PDF ringkasan sesuai permintaan.
* **Gabungkan dengan layanan AI lain** (mis., terjemahan) untuk menghasilkan ringkasan multibahasa.

Silakan bereksperimen dengan pengaturan temperature, max‑token, dan opsi OCR untuk menyesuaikan kebutuhan spesifik proyek Anda. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait erat yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Generate PDF summary with Aspose.Pdf.AI and OpenAI](/pdf/english/net/programming-with-text/generate-pdf-summary-with-aspose-pdf-ai-and-openai/)
- [How to convert PDF to summary with Aspose.Pdf.AI in C#](/pdf/english/net/text-operations/how-to-convert-pdf-to-summary-with-aspose-pdf-ai-in-c/)
- [How to Create a PDF Booklet Using Aspose.PDF .NET: A Comprehensive Guide](/pdf/english/net/printing-rendering/create-pdf-booklet-using-asposepdf-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}