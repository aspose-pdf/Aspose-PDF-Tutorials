---
category: general
date: 2026-09-12
description: Buat ringkasan PDF menggunakan Aspose.Pdf.AI dan OpenAI. Pelajari cara
  mendapatkan ringkasan, mengonversi PDF menjadi ringkasan, dan menginisialisasi klien
  OpenAI di C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- generate pdf summary
- how to get summary
- convert pdf to summary
- ai pdf summarization
- initialize openai client
language: id
lastmod: 2026-09-12
og_description: Hasilkan ringkasan PDF dengan Aspose.Pdf.AI dan OpenAI. Tutorial ini
  menunjukkan cara mendapatkan ringkasan, mengonversi PDF menjadi ringkasan, dan menginisialisasi
  klien OpenAI.
og_image_alt: Generate PDF summary example
og_title: Buat ringkasan PDF dengan Aspose.Pdf.AI – panduan langkah demi langkah
schemas:
- author: Aspose
  dateModified: '2026-09-12'
  description: Generate PDF summary using Aspose.Pdf.AI and OpenAI. Learn how to get
    summary, convert PDF to summary, and initialize OpenAI client in C#.
  headline: Generate PDF summary with Aspose.Pdf.AI and OpenAI
  type: TechArticle
- description: Generate PDF summary using Aspose.Pdf.AI and OpenAI. Learn how to get
    summary, convert PDF to summary, and initialize OpenAI client in C#.
  name: Generate PDF summary with Aspose.Pdf.AI and OpenAI
  steps:
  - name: '**Initialize OpenAI client** – authenticates your requests.'
    text: '**Initialize OpenAI client** – authenticates your requests.'
  - name: '**Configure options** – tells the service which PDF to read and how creative
      the output should be.'
    text: '**Configure options** – tells the service which PDF to read and how creative
      the output should be.'
  - name: '**Create copilot** – prepares the AI pipeline.'
    text: '**Create copilot** – prepares the AI pipeline.'
  - name: '**Fetch plain'
    text: '**Fetch plain'
  type: HowTo
tags:
- Aspose.Pdf.AI
- OpenAI
- C#
- PDF summarization
title: Buat ringkasan PDF dengan Aspose.Pdf.AI dan OpenAI
url: /id/net/programming-with-text/generate-pdf-summary-with-aspose-pdf-ai-and-openai/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hasilkan Ringkasan PDF dengan Aspose.Pdf.AI dan OpenAI

Jika Anda perlu **menghasilkan ringkasan PDF** dari dokumen yang sudah ada, Aspose.Pdf.AI menyediakan alur kerja singkat berbasis AI. Dalam panduan ini Anda akan melihat secara tepat **cara mendapatkan teks ringkasan**, **mengonversi PDF menjadi ringkasan**, dan **menginisialisasi klien OpenAI** menggunakan C#. Solusi lengkap dijalankan dalam beberapa baris kode dan menghasilkan PDF baru yang berisi ringkasan.

Tutorial ini membahas setiap langkah yang diperlukan, mulai dari menyiapkan klien OpenAI hingga menyimpan PDF ringkasan akhir. Anda akan mempelajari mengapa setiap konfigurasi penting, cara menangani kasus pinggiran umum, dan apa yang dapat disesuaikan untuk penyajian AI PDF tingkat produksi.

## Prasyarat

Sebelum memulai, pastikan Anda memiliki:

* .NET 6.0 atau yang lebih baru (kode berfungsi dengan .NET Core dan .NET Framework)
* Paket NuGet Aspose.Pdf.AI (`Aspose.Pdf.AI`) terpasang
* Kunci API OpenAI (Anda dapat memperolehnya dari portal OpenAI)
* File PDF contoh yang ingin Anda ringkas (misalnya `SampleDocument.pdf`)

Tidak ada SDK tambahan yang diperlukan; pustaka Aspose.Pdf.AI sudah menyertakan semua logika HTTP yang dibutuhkan untuk memanggil OpenAI di balik layar.

## Langkah 1: Inisialisasi klien OpenAI untuk Aspose.Pdf.AI

Tindakan pertama adalah **menginisialisasi klien OpenAI** dengan kunci rahasia Anda. Aspose.Pdf.AI menggunakan pola builder yang fluently, yang membuat kode tetap mudah dibaca dan tidak dapat diubah.

```csharp
// Step 1: Initialize the OpenAI client with your API key
using var openAiClient = Aspose.Pdf.AI.OpenAIClient
    .CreateWithApiKey("YOUR_OPENAI_API_KEY")
    .Build();
```

**Mengapa ini penting** – Klien menyimpan header otentikasi, pengaturan timeout, dan kebijakan retry. Dengan membuatnya sekali dan menggunakannya kembali, Anda menghindari handshake jaringan berulang dan menjaga proses peringkasan tetap cepat.

> **Pro tip:** Simpan kunci API dalam variabel lingkungan (`OPENAI_API_KEY`) dan baca pada saat runtime untuk menghindari menuliskan rahasia secara langsung dalam kode.

## Langkah 2: Konfigurasikan opsi copilot ringkasan (temperature dan PDF sumber)

Selanjutnya, beri tahu copilot dokumen mana yang akan diringkas dan seberapa kreatif AI harus bersikap. Parameter `temperature` mengontrol tingkat keacakan; nilai `0.5` menghasilkan ringkasan yang dapat diandalkan dan faktual.

```csharp
// Step 2: Set up summary copilot options (temperature and source PDF)
var summaryOptions = Aspose.Pdf.AI.OpenAISummaryCopilotOptions
    .Create()
    .WithTemperature(0.5)                     // lower = more deterministic
    .WithDocument("YOUR_DIRECTORY/SampleDocument.pdf");
```

**Mengapa ini penting** – Panggilan `WithDocument` mengarahkan AI ke file yang ingin Anda **konversi PDF menjadi ringkasan**. Jika Anda perlu merangkum beberapa PDF secara batch, Anda dapat melakukan loop pada langkah ini dengan jalur file yang berbeda.

## Langkah 3: Buat instance copilot ringkasan

Copilot adalah objek tingkat tinggi yang mengatur permintaan ke OpenAI, mengurai respons, dan secara opsional membangun PDF baru.

```csharp
// Step 3: Create the summary copilot instance
Aspose.Pdf.AI.ISummaryCopilot summaryCopilot =
    Aspose.Pdf.AI.AICopilotFactory.CreateSummaryCopilot(openAiClient, summaryOptions);
```

**Mengapa ini penting** – Pola pabrik menyembunyikan panggilan HTTP yang mendasarinya. Ini juga memastikan copilot menghormati opsi yang Anda tetapkan, seperti temperature dan dokumen sumber.

## Langkah 4: Ambil ringkasan teks biasa dari PDF

Sekarang Anda dapat meminta copilot untuk memberikan ringkasan mentah. Panggilan ini bersifat asynchronous karena menghubungi layanan OpenAI.

```csharp
// Step 4: Retrieve the plain‑text summary of the PDF
string summaryText = await summaryCopilot.GetSummaryAsync();
Console.WriteLine("Summary:\n" + summaryText);
```

**Mengapa ini penting** – Mendapatkan teks biasa memungkinkan Anda menampilkan hasil di konsol, menyimpannya di basis data, atau menggunakannya untuk pemrosesan bahasa alami lebih lanjut. Ini menjawab pertanyaan “**cara mendapatkan ringkasan**” secara langsung.

### Output yang diharapkan

```
Summary:
The document outlines the benefits of AI‑driven PDF summarization, explains the role of temperature in controlling output creativity, and provides a step‑by‑step guide for developers using Aspose.Pdf.AI...
```

## Langkah 5: Hasilkan dokumen PDF yang berisi ringkasan dan simpan

Jika Anda memerlukan artefak yang dapat dipindahkan, minta copilot untuk membuat PDF baru yang menyematkan teks ringkasan. Ini adalah bagian akhir dari alur kerja **menghasilkan ringkasan PDF**.

```csharp
// Step 5: Generate a PDF document that contains the summary and save it
Aspose.Pdf.Document summaryPdf = await summaryCopilot.GetSummaryDocumentAsync();
summaryPdf.Save("YOUR_DIRECTORY/Summary_out.pdf");
```

**Mengapa ini penting** – Objek `Document` yang dikembalikan sudah mencakup pagination yang tepat, font default, dan metadata. Anda dapat menyesuaikan tata letak lebih lanjut (menambahkan header, footer, atau gambar) sebelum menyimpannya.

### Verifikasi hasil

Buka `Summary_out.pdf` di penampil PDF apa pun. Anda seharusnya melihat dokumen satu halaman yang bersih dengan ringkasan yang dihasilkan AI, siap untuk distribusi atau arsip.

## Opsional: Penyempurnaan AI PDF summarization

Meskipun pengaturan default bekerja untuk kebanyakan kasus, Anda mungkin ingin menyesuaikan:

| Pengaturan | Dampak | Nilai yang Direkomendasikan |
|------------|--------|-----------------------------|
| `temperature` | Mengontrol kreativitas vs. determinisme | 0.3 – 0.7 untuk laporan faktual |
| `maxTokens` (jika tersedia) | Membatasi panjang output | 500–800 untuk ringkasan eksekutif yang singkat |
| `model` (mis., `gpt-4o-mini`) | Menentukan biaya & kualitas | Gunakan `gpt-4o` terbaru untuk hasil terbaik |

Anda dapat menambahkan opsi tambahan dengan API fluently:

```csharp
var summaryOptions = Aspose.Pdf.AI.OpenAISummaryCopilotOptions
    .Create()
    .WithTemperature(0.4)
    .WithMaxTokens(600)
    .WithModel("gpt-4o")
    .WithDocument("YOUR_DIRECTORY/LongReport.pdf");
```

## Kesalahan umum dan cara menghindarinya

* **Kunci API tidak valid** – Klien akan melempar `AuthenticationException`. Pastikan kunci benar dan memiliki izin yang diperlukan.
* **PDF besar (> 30 MB)** – Batas ukuran permintaan OpenAI mungkin terlampaui. Bagi PDF menjadi bagian‑bagian yang lebih kecil dan ringkas masing‑masing, lalu gabungkan hasilnya.
* **PDF non‑tekstual** – Gambar tanpa OCR akan diabaikan. Gunakan kemampuan OCR Aspose.Pdf.AI (`WithOcrEnabled(true)`) sebelum melakukan peringkasan.
* **Timeout jaringan** – Untuk koneksi lambat, tingkatkan timeout klien lewat `.WithTimeout(TimeSpan.FromSeconds(120))`.

## Contoh lengkap end‑to‑end

Berikut adalah program lengkap yang siap dijalankan. Ganti jalur placeholder dan kunci API dengan nilai Anda sendiri.

```csharp
using System;
using System.Threading.Tasks;
using Aspose.Pdf;
using Aspose.Pdf.AI;

class Program
{
    static async Task Main()
    {
        // 1️⃣ Initialize OpenAI client
        using var openAiClient = OpenAIClient
            .CreateWithApiKey(Environment.GetEnvironmentVariable("OPENAI_API_KEY"))
            .Build();

        // 2️⃣ Define summarization options
        var summaryOptions = OpenAISummaryCopilotOptions
            .Create()
            .WithTemperature(0.5)
            .WithDocument(@"C:\Docs\SampleDocument.pdf");

        // 3️⃣ Build the summary copilot
        ISummaryCopilot summaryCopilot =
            AICopilotFactory.CreateSummaryCopilot(openAiClient, summaryOptions);

        // 4️⃣ Get plain‑text summary
        string summaryText = await summaryCopilot.GetSummaryAsync();
        Console.WriteLine("Summary:\n" + summaryText);

        // 5️⃣ Create PDF that contains the summary
        Document summaryPdf = await summaryCopilot.GetSummaryDocumentAsync();
        summaryPdf.Save(@"C:\Docs\Summary_out.pdf");

        Console.WriteLine("Summary PDF saved successfully.");
    }
}
```

**Penjelasan alur**

1. **Inisialisasi klien OpenAI** – mengotentikasi permintaan Anda.
2. **Konfigurasikan opsi** – memberi tahu layanan PDF mana yang dibaca dan seberapa kreatif outputnya.
3. **Buat copilot** – menyiapkan pipeline AI.
4. **Ambil teks biasa**

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Pelajari Cara Menghasilkan Dokumen PDF dengan Aspose.PDF untuk .NET](/pdf/english/net/document-creation/)
- [Cara Mengonversi Halaman PDF menjadi Gambar Menggunakan Aspose.PDF untuk .NET (Panduan Langkah demi Langkah)](/pdf/english/net/conversion-export/convert-pdf-pages-to-images-aspose-pdf-net/)
- [Cara Mengonversi PDF menjadi TIFF Multi‑Halaman Menggunakan Aspose.PDF .NET - Panduan Langkah demi Langkah](/pdf/english/net/conversion-export/convert-pdf-to-multi-page-tiff-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}