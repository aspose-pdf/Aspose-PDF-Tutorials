---
category: general
date: 2026-08-04
description: Cara menggunakan Aspose untuk mengekstrak teks PDF yang dipindai dan
  mengonversi PDF ke teks dengan C#. Pelajari cara membaca file PDF yang dipindai
  dan mendapatkan hasil OCR yang dapat diandalkan.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use aspose
- extract scanned pdf text
- convert pdf to text
- read scanned pdf
- how to extract text
language: id
lastmod: 2026-08-04
og_description: Cara menggunakan Aspose untuk membaca file PDF yang dipindai, mengekstrak
  teks PDF yang dipindai, dan mengonversi PDF ke teks dengan contoh lengkap yang dapat
  dijalankan.
og_image_alt: Screenshot showing how to use Aspose OCR copilot to extract text from
  a scanned PDF
og_title: Cara menggunakan Aspose – mengekstrak teks dari PDF yang dipindai dengan
  C#
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: How to use Aspose to extract scanned PDF text and convert PDF to text
    with C#. Learn to read scanned PDF files and get reliable OCR results.
  headline: How to use Aspose to extract text from a scanned PDF – step‑by‑step guide
  type: TechArticle
- questions:
  - answer: Yes. Add `.WithPassword("yourPassword")` to the options builder before
      creating the copilot.
    question: Does this work with password‑protected PDFs?
  - answer: Use `GetTextStructureAsync()` instead of `GetTextAsync()`. The method
      returns a JSON payload that includes page indices, bounding boxes, and confidence
      scores.
    question: Can I extract text in a structured format (e.g., JSON with page numbers)?
  - answer: 'The plain‑text extraction flattens tables into line‑break‑separated rows.
      For richer data, request the PDF‑to‑HTML conversion (`GetHtmlAsync`) and parse
      the HTML table elements. ## Conclusion You now know **how to use Aspose** to
      read a scanned PDF, extract scanned PDF text, and **convert PDF to tex'
    question: What if the PDF contains tables?
  type: FAQPage
tags:
- Aspose.PDF.AI
- OCR
- C#
- PDF processing
title: Cara menggunakan Aspose untuk mengekstrak teks dari PDF yang dipindai – panduan
  langkah demi langkah
url: /id/net/text/how-to-use-aspose-to-extract-text-from-a-scanned-pdf-step-by/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara menggunakan Aspose untuk mengekstrak teks dari PDF yang dipindai – panduan langkah demi langkah

Jika Anda perlu **cara menggunakan Aspose** untuk OCR, panduan ini menunjukkan cara mengekstrak teks PDF yang dipindai dalam beberapa baris C#. Baik Anda sedang membangun layanan pengarsipan dokumen atau indeks pencarian untuk dokumen lama, solusi ini bekerja dengan PDF yang dipindai apa pun yang Anda kirim ke layanan Aspose.Pdf.AI.

Dalam tutorial ini Anda akan:

* Membuat OCR copilot yang membaca PDF yang dipindai.
* Mengekstrak teks yang dikenali secara asynchronous.
* Menampilkan atau memproses lebih lanjut string yang diekstrak.

Satu-satunya prasyarat adalah langganan aktif Aspose.Pdf.AI dan lingkungan pengembangan .NET 6 (atau lebih baru).

## Prerequisites

| Persyaratan | Mengapa penting |
|-------------|----------------|
| .NET 6 SDK atau lebih baru | Menyediakan `async Main` dan fitur bahasa modern. |
| Paket NuGet Aspose.Pdf.AI (`Aspose.Pdf.AI`) | Berisi `AICopilotFactory` dan opsi OCR. |
| Instance `client` Aspose.Pdf.AI yang valid (API key) | Mengautentikasi permintaan Anda ke layanan cloud. |
| File PDF yang dipindai (mis., `Scanned.pdf`) | Dokumen sumber dari mana teks akan diekstrak. |

Install paket dengan .NET CLI:

```bash
dotnet add package Aspose.Pdf.AI
```

## Langkah 1: Siapkan klien Aspose.Pdf.AI

Sebelum Anda dapat memanggil endpoint OCR apa pun, Anda harus membuat klien yang menyimpan kredensial API Anda. Klien ini thread‑safe dan dapat digunakan kembali untuk banyak dokumen.

```csharp
using Aspose.Pdf.AI;
using Aspose.Pdf.AI.Models;

// Replace with your actual API key and base URL if you use a private cloud.
var client = new PdfAiClient(new PdfAiConfiguration
{
    ApiKey = "YOUR_API_KEY",
    // BaseUrl = "https://api.aspose.cloud" // default, change only if needed
});
```

**Mengapa langkah ini diperlukan** – Layanan Aspose memvalidasi setiap permintaan terhadap langganan Anda. Membuat klien sekali saja menghindari handshake jaringan berulang dan menjaga kode tetap bersih.

## Langkah 2: Buat OCR copilot untuk dokumen PDF yang dipindai

`AICopilotFactory` membangun OCR copilot khusus yang tahu cara memproses file yang Anda tentukan. Anda mengirimkan `client` dan objek `OpenAIOcrOptions` yang menunjuk ke path PDF.

```csharp
using Aspose.Pdf.AI;

// Step 2: Build the OCR copilot
var ocrCopilot = AICopilotFactory.CreateOcrCopilot(
    client,                                   // Your Aspose.Pdf.AI client instance
    OpenAIOcrOptions.Create()
        .WithDocument("YOUR_DIRECTORY/Scanned.pdf") // Path to the scanned PDF
);
```

**Penjelasan** – `CreateOcrCopilot` mengenkapsulasi semua panggilan HTTP tingkat rendah. Metode `WithDocument` memberi tahu layanan file mana yang akan dianalisis; Anda juga dapat menyediakan `Stream` jika PDF berada di memori.

## Langkah 3: Ekstrak teks yang dikenali secara asynchronous

Memanggil `GetTextAsync` menjalankan operasi OCR di cloud dan mengembalikan hasil plain‑text. Karena operasi ini dapat memakan beberapa detik, metode ini bersifat asynchronous.

```csharp
// Step 3: Perform OCR and get the text
string ocrText = await ocrCopilot.GetTextAsync();
```

**Mengapa asynchronous?** – Latensi jaringan dan waktu pemrosesan OCR tidak dapat diprediksi. Menggunakan `await` mencegah aplikasi Anda memblokir thread utama, yang terutama penting untuk skenario UI atau layanan web.

## Langkah 4: Gunakan teks yang diekstrak

Pada titik ini Anda memiliki `string` .NET biasa yang berisi transkripsi lengkap PDF yang dipindai. Anda dapat menuliskannya ke console, menyimpannya di basis data, atau mengirimkannya ke mesin pencari.

```csharp
// Step 4: Display the result
Console.WriteLine("=== OCR Result ===");
Console.WriteLine(ocrText);
```

### Output yang diharapkan

Jika `Scanned.pdf` berisi satu halaman dengan kalimat “Hello, world!”, console akan menampilkan:

```
=== OCR Result ===
Hello, world!
```

Untuk dokumen multi‑halaman output menggabungkan teks setiap halaman, mempertahankan jeda baris.

## Contoh lengkap yang dapat dijalankan

Berikut adalah program lengkap yang dapat Anda tempel ke proyek console baru (`dotnet new console`). Program ini mendemonstrasikan **cara menggunakan Aspose** dari awal hingga akhir, termasuk penanganan error untuk jebakan umum.

```csharp
using System;
using System.Threading.Tasks;
using Aspose.Pdf.AI;
using Aspose.Pdf.AI.Models;

namespace AsposeOcrDemo
{
    class Program
    {
        static async Task Main(string[] args)
        {
            // 1️⃣ Initialize the Aspose.Pdf.AI client
            var client = new PdfAiClient(new PdfAiConfiguration
            {
                ApiKey = "YOUR_API_KEY"
                // BaseUrl = "https://api.aspose.cloud" // optional
            });

            // 2️⃣ Build the OCR copilot for the target PDF
            var pdfPath = "YOUR_DIRECTORY/Scanned.pdf";
            var ocrCopilot = AICopilotFactory.CreateOcrCopilot(
                client,
                OpenAIOcrOptions.Create().WithDocument(pdfPath)
            );

            try
            {
                // 3️⃣ Extract text asynchronously
                string ocrText = await ocrCopilot.GetTextAsync();

                // 4️⃣ Use the extracted text (display in console)
                Console.WriteLine("=== OCR Result ===");
                Console.WriteLine(ocrText);
            }
            catch (Exception ex)
            {
                // Common errors: invalid API key, missing file, unsupported PDF version
                Console.Error.WriteLine($"Error during OCR: {ex.Message}");
            }
        }
    }
}
```

**Poin penting dalam contoh**

* `await` memastikan eksekusi non‑blocking.
* Blok `try/catch` menampilkan error jaringan atau layanan, yang penting saat **membaca PDF yang dipindai** dalam skala besar.
* Ganti `YOUR_API_KEY` dan `YOUR_DIRECTORY/Scanned.pdf` dengan nilai sebenarnya sebelum menjalankan.

## Menangani kasus tepi dan tips praktik terbaik

| Situasi | Pendekatan yang disarankan |
|-----------|----------------------|
| **PDF besar ( > 50 MB )** | Bagi dokumen menjadi potongan lebih kecil di sisi klien dan proses setiap potongan dengan copilot terpisah. Ini mengurangi tekanan memori dan meningkatkan keandalan. |
| **Pemindaian kualitas rendah** | Sesuaikan kualitas OCR dengan menambahkan `.WithLanguage("eng")` atau `.WithEnhanceImage(true)` ke `OpenAIOcrOptions`. Layanan mendukung petunjuk bahasa yang meningkatkan akurasi. |
| **Beberapa bahasa** | Berikan daftar dipisahkan koma, misalnya `.WithLanguage("eng,spa")`. Mesin OCR akan mendeteksi dan menuliskan kedua bahasa. |
| **File gambar bukan PDF** | Konversi gambar ke PDF terlebih dahulu (`Aspose.Pdf` library) atau gunakan `OpenAIOcrOptions.WithImage` untuk mengirim gambar secara langsung. |
| **Batas laju terlampaui** | Implementasikan back‑off eksponensial dan logika retry; API Aspose mengembalikan HTTP 429 ketika Anda melampaui kuota. |

### Tips pro

Cache hasil `ocrText` jika Anda berencana menggunakannya kembali nanti. Operasi OCR adalah bagian paling mahal dalam alur kerja, dan menggunakan kembali string menghindari panggilan API duplikat serta menghemat kredit.

## Pertanyaan yang sering diajukan

**Q: Apakah ini bekerja dengan PDF yang dilindungi kata sandi?**  
A: Ya. Tambahkan `.WithPassword("yourPassword")` ke builder opsi sebelum membuat copilot.

**Q: Bisakah saya mengekstrak teks dalam format terstruktur (mis., JSON dengan nomor halaman)?**  
A: Gunakan `GetTextStructureAsync()` alih‑alih `GetTextAsync()`. Metode ini mengembalikan payload JSON yang mencakup indeks halaman, kotak pembatas, dan skor kepercayaan.

**Q: Bagaimana jika PDF berisi tabel?**  
A: Ekstraksi plain‑text akan meratakan tabel menjadi baris‑baris yang dipisahkan jeda baris. Untuk data yang lebih kaya, minta konversi PDF‑ke‑HTML (`GetHtmlAsync`) dan parse elemen tabel HTML.

## Kesimpulan

Anda kini tahu **cara menggunakan Aspose** untuk membaca PDF yang dipindai, mengekstrak teks PDF yang dipindai, dan **mengonversi PDF ke teks** dengan program C# minimal. Prosesnya meliputi pembuatan OCR copilot, pemanggilan `GetTextAsync`, dan penanganan string yang dihasilkan. Dengan mengikuti rekomendasi kasus tepi, Anda dapat menskalakan solusi ke batch dokumen besar, konten multibahasa, dan PDF yang aman.

Selanjutnya, Anda mungkin ingin menjelajahi:

* **Cara mengekstrak teks** dengan preservasi tata letak (`GetHtmlAsync`).
* Menggunakan Aspose.Pdf.AI untuk **mengekstrak tabel** dan mengekspornya ke CSV.
* Mengintegrasikan output OCR dengan Azure Cognitive Search untuk arsip dokumen yang dapat dicari.

Selamat coding, dan nikmati akurasi yang dibawa OCR berbasis AI Aspose ke alur kerja PDF yang dipindai Anda!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Ekstrak Teks dari File PDF Menggunakan Aspose.PDF untuk .NET](/pdf/english/net/text-operations/extract-text-pdf-aspose-dotnet/)
- [Cara Mengekstrak Teks dari Region Spesifik dalam PDF Menggunakan Aspose.PDF untuk .NET](/pdf/english/net/text-operations/extract-text-specific-region-aspose-pdf-net/)
- [Cara Mengekstrak Teks yang Disorot dari PDF Menggunakan Aspose.PDF untuk .NET](/pdf/english/net/text-operations/extract-highlighted-text-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}