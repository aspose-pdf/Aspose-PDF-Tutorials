---
category: general
date: 2026-08-04
description: Buat AI Copilot untuk menghasilkan deskripsi gambar untuk file PDF. Pelajari
  cara mengonfigurasi opsi gambar OpenAI dan mengekstrak deskripsi gambar secara efisien.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create AI copilot
- generate image description
- image description PDF
- OpenAI image options
- extract image description
language: id
lastmod: 2026-08-04
og_description: Buat AI Copilot untuk menghasilkan deskripsi gambar untuk file PDF.
  Tutorial ini menunjukkan cara mengonfigurasi opsi gambar OpenAI, menjalankan copilot,
  dan mengekstrak deskripsi gambar dalam C#.
og_image_alt: Screenshot of C# code that creates an AI copilot for PDF image description
og_title: Buat AI Copilot untuk Deskripsi Gambar PDF – Panduan Lengkap
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Create AI Copilot to generate image description for PDF files. Learn
    how to configure OpenAI image options and extract image description efficiently.
  headline: Create AI Copilot for PDF image description – step‑by‑step guide
  type: TechArticle
tags:
- Aspose.Pdf.AI
- C#
- PDF processing
title: Buat AI Copilot untuk deskripsi gambar PDF – panduan langkah demi langkah
url: /id/net/programming-with-images/create-ai-copilot-for-pdf-image-description-step-by-step-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat AI Copilot untuk Deskripsi Gambar PDF – panduan lengkap

Jika Anda perlu **membuat AI Copilot** yang secara otomatis menulis deskripsi untuk gambar yang disematkan dalam PDF, panduan ini menunjukkan secara tepat cara melakukannya. Anda akan belajar mengonfigurasi OpenAI image options, menjalankan copilot, dan **mengekstrak deskripsi gambar** tanpa meninggalkan proyek C# Anda.

Menghasilkan konten teks untuk gambar PDF merupakan kebutuhan umum untuk aksesibilitas, pengindeksan konten, dan pelaporan otomatis. Pada akhir tutorial ini Anda akan memiliki komponen yang dapat digunakan kembali yang **menghasilkan deskripsi gambar** untuk dokumen PDF apa pun yang Anda arahkan.

## Prasyarat

* .NET 6.0 atau lebih baru terinstal  
* Lisensi Aspose.Pdf.AI (atau percobaan gratis)  
* Kunci API OpenAI yang dapat digunakan klien Aspose  
* Visual Studio 2022 (atau IDE apa pun yang mendukung C#)  

Tidak diperlukan paket NuGet tambahan selain `Aspose.Pdf.AI`.

## Langkah 1: Siapkan klien Aspose.Pdf.AI

Langkah pertama adalah membuat instance klien AI dengan detail autentikasi Anda. Klien menangani komunikasi dengan layanan OpenAI di belakang layar.

```csharp
using Aspose.Pdf.AI;
using Aspose.Pdf.AI.Models;

// Replace with your actual credentials
var client = new AiClient(new AiClientOptions
{
    ApiKey = Environment.GetEnvironmentVariable("OPENAI_API_KEY"),
    // Optional: set a custom endpoint if you use Azure OpenAI
    // Endpoint = "https://my-openai-instance.openai.azure.com/"
});
```

**Mengapa ini penting:** `AiClient` mengenkapsulasi semua pengaturan tingkat permintaan (API key, timeout, kebijakan retry). Membuatnya sekali dan menggunakan kembali di beberapa instance copilot mengurangi beban dan memastikan autentikasi yang konsisten.

## Langkah 2: Buat AI Copilot Deskripsi Gambar

Sekarang Anda membuat **AI copilot** yang akan membaca PDF dan menghasilkan deskripsi untuk setiap gambar. Metode pabrik `CreateImageDescriptionCopilot` menerima klien dan sekumpulan opsi yang menentukan bagaimana deskripsi dihasilkan.

```csharp
// Configure OpenAI image options – this is where you control model, temperature, etc.
var imageOptions = OpenAIImageDescriptionOptions.Create()
    .WithModel("gpt-4o-mini")           // Choose a model that balances cost and quality
    .WithTemperature(0.7)               // Controls creativity; 0 = deterministic
    .WithMaxTokens(150);                // Maximum length of each description

// Point the copilot at the PDF you want to process
var imgCopilot = AICopilotFactory.CreateImageDescriptionCopilot(
    client,
    imageOptions.WithDocument(@"C:\Reports\AnnualReport.pdf"));
```

**Mengapa ini penting:**  
* `OpenAIImageDescriptionOptions` (the **OpenAI image options**) memungkinkan Anda menyesuaikan model bahasa. Mengatur temperature atau model dapat meningkatkan relevansi untuk diagram teknis dibandingkan foto alami.  
* Menentukan path dokumen memberi tahu copilot PDF mana yang akan dipindai. Copilot mengekstrak setiap gambar raster, mengirimkannya ke model, dan mengembalikan deskripsi yang dapat dibaca manusia.

## Langkah 3: Ambil deskripsi yang dihasilkan secara asynchronous

Copilot bekerja secara asynchronous karena mungkin perlu mengunggah beberapa megabyte data gambar dan menunggu respons model. Gunakan `await` untuk memastikan panggilan selesai sebelum Anda mengakses hasilnya.

```csharp
try
{
    // Get a dictionary where the key is the page number and the value is the description
    var descriptionMap = await imgCopilot.GetDescriptionAsync();

    // Example: iterate over each image description
    foreach (var entry in descriptionMap)
    {
        Console.WriteLine($"Page {entry.Key}: {entry.Value}");
    }
}
catch (AiException ex)
{
    Console.Error.WriteLine($"AI service error: {ex.Message}");
}
```

**Mengapa ini penting:** Metode mengembalikan `Dictionary<int, string>` yang memetakan setiap halaman (atau indeks gambar) ke deskripsinya. Menangani `AiException` memungkinkan Anda menampilkan kesalahan jaringan atau kuota alih-alih membuat aplikasi crash.

## Langkah 4: Tampilkan atau simpan deskripsi

Anda dapat menulis deskripsi ke konsol, file log, atau menyematkannya kembali ke PDF sebagai alt‑text untuk aksesibilitas. Berikut contoh singkat yang menulis output ke file JSON untuk penggunaan selanjutnya.

```csharp
using System.Text.Json;

// Serialize the map to JSON
var json = JsonSerializer.Serialize(descriptionMap, new JsonSerializerOptions { WriteIndented = true });
File.WriteAllText(@"C:\Reports\ImageDescriptions.json", json);

Console.WriteLine("Image descriptions saved to ImageDescriptions.json");
```

**Mengapa ini penting:** Menyimpan output sebagai JSON mempertahankan asosiasi antara setiap halaman dan deskripsinya, memudahkan proses downstream (pengindeksan pencarian, rendering UI, dll.) untuk mengonsumsi data.

## Menangani beberapa gambar per halaman

Jika sebuah halaman berisi beberapa gambar, copilot mengembalikan deskripsi yang digabungkan dipisahkan oleh baris baru. Untuk memisahkannya, periksa hasil mentah dan split pada `\n\n` (newline ganda). Berikut metode pembantu:

```csharp
static IEnumerable<string> SplitDescriptions(string combined)
{
    return combined.Split(new[] { "\n\n" }, StringSplitOptions.RemoveEmptyEntries);
}
```

Anda kemudian dapat mengiterasi setiap deskripsi gambar individu dan menyimpannya secara terpisah jika diperlukan.

## Kasus tepi: PDF besar dan manajemen timeout

Memproses PDF yang lebih besar dari 100 MB dapat melampaui timeout HTTP default. Sesuaikan pengaturan timeout klien saat Anda membuat `AiClient`:

```csharp
var client = new AiClient(new AiClientOptions
{
    ApiKey = Environment.GetEnvironmentVariable("OPENAI_API_KEY"),
    Timeout = TimeSpan.FromMinutes(5)   // Increase timeout for heavy workloads
});
```

Meningkatkan timeout mencegah penghentian prematur saat layanan memproses banyak gambar beresolusi tinggi.

## Tips pro: Cache hasil untuk mengurangi biaya

OpenAI mengenakan biaya per token, dan deskripsi gambar dapat berulang di berbagai versi laporan yang sama. Cache output JSON dan gunakan kembali ketika hash PDF cocok dengan file yang sebelumnya diproses. Praktik ini menghemat uang dan mempercepat eksekusi berikutnya.

```csharp
static string ComputeFileHash(string path)
{
    using var sha256 = System.Security.Cryptography.SHA256.Create();
    using var stream = File.OpenRead(path);
    var hash = sha256.ComputeHash(stream);
    return Convert.ToHexString(hash);
}
```

Simpan hash bersama file JSON; jika hash cocok pada eksekusi berikutnya, lewati panggilan AI.

## Contoh lengkap yang dapat dijalankan

Menggabungkan semua, berikut aplikasi konsol mandiri yang dapat Anda tempel ke proyek .NET baru.

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using System.Text.Json;
using System.Threading.Tasks;
using Aspose.Pdf.AI;
using Aspose.Pdf.AI.Models;

class Program
{
    static async Task Main()
    {
        // 1️⃣ Initialize AI client
        var client = new AiClient(new AiClientOptions
        {
            ApiKey = Environment.GetEnvironmentVariable("OPENAI_API_KEY"),
            Timeout = TimeSpan.FromMinutes(5)
        });

        // 2️⃣ Configure OpenAI image options and create copilot
        var imageOptions = OpenAIImageDescriptionOptions.Create()
            .WithModel("gpt-4o-mini")
            .WithTemperature(0.7)
            .WithMaxTokens(150);

        string pdfPath = @"C:\Reports\AnnualReport.pdf";

        var imgCopilot = AICopilotFactory.CreateImageDescriptionCopilot(
            client,
            imageOptions.WithDocument(pdfPath));

        // 3️⃣ Retrieve descriptions
        Dictionary<int, string> descriptionMap;
        try
        {
            descriptionMap = await imgCopilot.GetDescriptionAsync();
        }
        catch (AiException ex)
        {
            Console.Error.WriteLine($"Error from AI service: {ex.Message}");
            return;
        }

        // 4️⃣ Output results
        foreach (var entry in descriptionMap)
        {
            Console.WriteLine($"Page {entry.Key}:");
            Console.WriteLine(entry.Value);
            Console.WriteLine(new string('-', 40));
        }

        // 5️⃣ Save to JSON for later use
        string json = JsonSerializer.Serialize(descriptionMap, new JsonSerializerOptions { WriteIndented = true });
        string jsonPath = Path.ChangeExtension(pdfPath, ".descriptions.json");
        await File.WriteAllTextAsync(jsonPath, json);
        Console.WriteLine($"Descriptions saved to {jsonPath}");
    }
}
```

**Output yang diharapkan (dipotong)**

```
Page 2:
A bar chart showing quarterly revenue growth, with blue bars representing Q1–Q4.
----------------------------------------
Page 5:
A high‑resolution photograph of the new manufacturing facility, showing the assembly line in operation.
...
Descriptions saved to C:\Reports\AnnualReport.descriptions.json
```

Program membaca `AnnualReport.pdf`, membuat **AI copilot**, dan menulis file JSON yang memetakan setiap halaman ke deskripsi yang dihasilkan.

## Pertanyaan umum

* **Apakah ini bekerja dengan PDF terenkripsi?**  
  Ya, tetapi Anda harus menyediakan kata sandi saat membuat copilot:  
  `imageOptions.WithPassword("mySecret")`.

* **Bisakah saya membatasi pemrosesan ke halaman tertentu?**  
  Gunakan `imageOptions.WithPageRange(1, 10)` untuk membatasi copilot ke halaman 1‑10.

* **Bagaimana jika sebuah gambar berisi teks?**  
  Model berusaha mendeskripsikan konten visual; untuk ekstraksi teks bergaya OCR Anda sebaiknya menggunakan `CreateTextExtractionCopilot`.

## Kesimpulan

Anda kini tahu cara **membuat AI Copilot** yang **menghasilkan deskripsi gambar** untuk file PDF, mengonfigurasi **OpenAI image options**, dan **mengekstrak deskripsi gambar** secara programatis di C#. Contoh lengkap menunjukkan praktik terbaik seperti penanganan async, manajemen error, dan caching hasil.

Selanjutnya, Anda mungkin ingin menjelajahi:

* Menambahkan deskripsi yang dihasilkan kembali ke PDF sebagai alt‑text untuk meningkatkan aksesibilitas (`PdfDocument` → `PdfImage.AlternativeText`).  
* Menggunakan pola copilot yang sama untuk **menghasilkan laporan PDF deskripsi gambar** untuk pemrosesan batch.  
* Mencoba berbagai model OpenAI atau pengaturan temperature untuk menyesuaikan gaya deskripsi.

Silakan sesuaikan kode, bereksperimen dengan dokumen yang lebih besar, dan integrasikan output ke pipeline pengindeksan Anda. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang terkait erat yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Buat PDF dengan Gambar Ber-tag di Java](/pdf/hindi/java/pdf-structure-elements/create-pdf-with-tagged-image-in-java/)
- [Buat PDF dengan Gambar Ber-tag](/pdf/hindi/net/programming-with-tagged-pdf/create-pdf-with-tagged-image/)
- [Buat Gambar PDF Ber-tag di .NET](/pdf/hindi/net/images-graphics/create-tagged-pdf-image-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}