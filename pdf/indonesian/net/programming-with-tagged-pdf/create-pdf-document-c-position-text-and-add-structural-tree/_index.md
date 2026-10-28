---
category: general
date: 2026-07-20
description: 'Buat dokumen PDF C# dengan Aspose.Pdf: posisikan teks dalam PDF dan
  tambahkan pohon struktural untuk aksesibilitas. Ikuti panduan langkah demi langkah
  ini.'
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create pdf document c#
- position text in pdf
- add structural tree
- Aspose.Pdf tagging
- PDF/A‑2b generation
language: id
lastmod: 2026-07-20
og_description: Buat dokumen PDF dengan C# secara instan. Pelajari cara menempatkan
  teks dalam PDF dan menambahkan pohon struktural menggunakan Aspose.Pdf untuk kepatuhan
  PDF/A‑2b.
og_image_alt: Screenshot showing positioned text inside a PDF generated with Aspose.Pdf
  in C#
og_title: Membuat Dokumen PDF C# – Panduan Lengkap Menempatkan Teks & Struktur Tag
schemas:
- author: Aspose
  dateModified: '2026-07-20'
  description: 'Create PDF document C# with Aspose.Pdf: position text in PDF and add
    structural tree for accessibility. Follow this step‑by‑step guide.'
  headline: Create PDF Document C# – Position Text and Add Structural Tree
  type: TechArticle
- description: 'Create PDF document C# with Aspose.Pdf: position text in PDF and add
    structural tree for accessibility. Follow this step‑by‑step guide.'
  name: Create PDF Document C# – Position Text and Add Structural Tree
  steps:
  - name: Can I use other units (mm, cm) for positioning?
    text: Aspose.Pdf works natively with points. If you prefer millimeters, convert
      using `1 mm ≈ 2.83465 pt`. For example, `Position(25.4, 254)` places the paragraph
      1 cm from the left and 9 cm from the bottom.
  - name: What if I need to add multiple tags (headings, tables)?
    text: Simply create additional `StructureElement` objects with tags like `"H1"`
      for headings or `"Table"` for tables, and add the corresponding content as kids.
      Nesting works the same way—children inherit the parent’s logical order.
  - name: Does this approach work for PDF/A‑1b or PDF/A‑3b?
    text: Yes. Replace `SaveFormat.PdfA2b` with `SaveFormat.PdfA1b` or `SaveFormat.PdfA3b`.
      Keep in mind that each PDF/A version has its own set of required metadata; Aspose.Pdf
      will prompt you if something is missing.
  type: HowTo
tags:
- C#
- PDF
- Aspose.Pdf
title: Buat Dokumen PDF C# – Posisi Teks dan Tambahkan Pohon Struktural
url: /id/net/programming-with-tagged-pdf/create-pdf-document-c-position-text-and-add-structural-tree/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat Dokumen PDF C# – Menempatkan Teks dan Menambahkan Struktur Pohon

Pernahkah Anda perlu **create PDF document C#** yang tidak hanya menempatkan teks tepat di tempat yang Anda inginkan, tetapi juga menyematkan struktur pohon yang tepat untuk aksesibilitas? Anda bukan satu‑satunya—para pengembang yang membuat faktur, laporan, atau e‑book sering membutuhkan hal ini. Dalam tutorial ini kami akan membimbing Anda melalui contoh lengkap yang siap dijalankan yang melakukan hal tersebut, menggunakan library Aspose.Pdf yang kuat.

Kami akan membahas cara **position text in PDF**, menambahkan tag semantik melalui langkah **add structural tree**, dan akhirnya menyimpan file sebagai dokumen yang mematuhi PDF/A‑2b. Pada akhir tutorial Anda akan memiliki potongan kode yang dapat dipakai ulang dan dapat disisipkan ke proyek .NET mana pun.

---

## Apa yang Anda Butuhkan

- **.NET 6.0** atau yang lebih baru (kode ini juga berfungsi dengan .NET Framework 4.6+)
- Paket NuGet **Aspose.Pdf for .NET** (`Install-Package Aspose.Pdf`)
- Lingkungan pengembangan C# dasar (Visual Studio, Rider, atau VS Code)

Tidak ada alat pihak ketiga tambahan yang diperlukan; library ini menangani semuanya mulai dari tata letak halaman hingga kepatuhan PDF/A.

---

## Langkah 1: Inisialisasi Dokumen PDF (Create PDF Document C#)

Hal pertama yang kami lakukan adalah membuat objek `Document` baru. Anggap saja ini sebagai kanvas bersih—belum ada apa‑apa di dalamnya, tetapi siap menerima halaman, teks, dan metadata struktural.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Struct;

// Create a new PDF document – this is the core of our create pdf document c# workflow
Document pdfDoc = new Document();

// Add a blank page to the document; the page will host our positioned text
Page pdfPage = pdfDoc.Pages.Add();
```

> **Mengapa ini penting:** Kelas `Document` adalah titik masuk untuk semua operasi Aspose.Pdf. Menambahkan halaman di awal memberi kami permukaan untuk menempelkan baik konten visual maupun struktur pohon nanti.

---

## Langkah 2: Definisikan Paragraph dan Posisi (Position Text in PDF)

Sekarang kami membuat objek `Paragraph` dan memberi tahu Aspose tepat di mana pada halaman paragraf tersebut harus muncul. Koordinat PDF diukur dalam poin (1 inci = 72 pt), jadi kami menggunakan `Position(72, 720)` untuk menempatkan paragraf 1 inci dari tepi kiri dan 10 inci dari bagian bawah.

```csharp
// Define a paragraph positioned 1 inch from the left and 10 inches from the bottom
Paragraph positionedParagraph = new Paragraph
{
    // Position(x, y) – X is horizontal, Y is vertical from the bottom-left corner
    Position = new Position(72, 720) // 72 pt = 1 inch, 720 pt = 10 inch
};

// Add the actual text we want to display
positionedParagraph.Segments.Add(
    new TextFragment("Tagged paragraph at a specific location.")
);
```

> **Tips pro:** Jika Anda perlu menempatkan beberapa baris, sesuaikan koordinat `Y` untuk setiap paragraf berikutnya, atau gunakan `TextBuilder` untuk kontrol yang lebih halus.

---

## Langkah 3: Buat Elemen Struktural (Add Structural Tree)

PDF yang ramah aksesibilitas mengandalkan *structure tree* yang menggambarkan urutan logis konten. Di sini kami membuat `StructureElement` dengan tag `"P"` (paragraph) dan melampirkan paragraf yang telah diposisikan sebagai anaknya.

```csharp
// Create a structural element (tag) for the paragraph – this is the add structural tree step
StructureElement structElement = new StructureElement("P");

// Attach the paragraph as a child of the structural element
structElement.AddKid(positionedParagraph);
```

> **Mengapa kami menambahkan struktur pohon:** Pembaca layar dan teknologi bantu lainnya menggunakan tag ini untuk menavigasi dokumen. Tanpa tag tersebut, PDF Anda mungkin tampak sempurna secara visual tetapi tidak dapat diakses.

---

## Langkah 4: Kaitkan Elemen Struktural ke Halaman

Setiap halaman memiliki koleksi elemen strukturalnya sendiri. Dengan menambahkan `structElement` ke `pdfPage.StructElements`, kami mengintegrasikan hierarki logis dengan tata letak visual.

```csharp
// Attach the structural element to the page's structure tree
pdfPage.StructElements.Add(structElement);
```

> **Kesalahan umum:** Lupa melakukan langkah ini berarti tag ada di memori tetapi tidak terhubung ke halaman mana pun, sehingga informasi aksesibilitas tidak terlihat oleh pembaca.

---

## Langkah 5: Simpan sebagai PDF/A‑2b (Menjamin Preservasi Jangka Panjang)

PDF/A‑2b adalah subset PDF yang dirancang untuk pengarsipan. Aspose.Pdf dapat menghasilkan format ini dengan satu panggilan. Ganti `"YOUR_DIRECTORY"` dengan jalur sebenarnya di mesin Anda.

```csharp
// Save the document as a PDF/A‑2b file – ideal for long‑term storage and compliance
pdfDoc.Save("YOUR_DIRECTORY/TaggedWithPosition.pdf", SaveFormat.PdfA2b);
```

> **Hasil:** Sekarang Anda memiliki PDF di mana teks berada tepat pada posisi yang Anda tentukan, dan dokumen menyertakan struktur pohon yang tepat untuk alat aksesibilitas.

---

## Contoh Lengkap yang Siap Pakai

Berikut adalah program lengkap yang dapat Anda salin‑tempel ke aplikasi konsol. Program ini dapat dikompilasi dan dijalankan apa adanya (setelah Anda menambahkan referensi NuGet Aspose.Pdf).

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Struct;

namespace PdfPositioningDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Initialize the document
            Document pdfDoc = new Document();
            Page pdfPage = pdfDoc.Pages.Add();

            // Step 2: Define and position the paragraph
            Paragraph positionedParagraph = new Paragraph
            {
                Position = new Position(72, 720) // 1 inch left, 10 inches up
            };
            positionedParagraph.Segments.Add(
                new TextFragment("Tagged paragraph at a specific location.")
            );

            // Step 3: Create the structural element (tag)
            StructureElement structElement = new StructureElement("P");
            structElement.AddKid(positionedParagraph);

            // Step 4: Attach the structural element to the page
            pdfPage.StructElements.Add(structElement);

            // Step 5: Save as PDF/A‑2b
            string outputPath = @"C:\Temp\TaggedWithPosition.pdf";
            pdfDoc.Save(outputPath, SaveFormat.PdfA2b);

            Console.WriteLine($"PDF created successfully at: {outputPath}");
        }
    }
}
```

**Output yang diharapkan:** Setelah dijalankan, buka `TaggedWithPosition.pdf`. Anda akan melihat kalimat “Tagged paragraph at a specific location.” berada di sudut kanan‑bawah halaman pertama. Jika Anda memeriksa tag PDF (misalnya dengan panel “Tags” di Adobe Acrobat), Anda akan menemukan elemen `<P>` yang terhubung ke paragraf tersebut.

---

![Tangkapan layar teks yang diposisikan dalam PDF yang dihasilkan dengan Aspose.Pdf](/images/pdf-positioned.png){: .align-center }

*Teks alt gambar:* **create pdf document c#** – tangkapan layar yang menunjukkan teks yang diposisikan di dalam PDF yang dihasilkan dengan Aspose.Pdf.

---

## Pertanyaan Umum & Kasus Khusus

### Apakah saya dapat menggunakan satuan lain (mm, cm) untuk penempatan?

Aspose.Pdf bekerja secara native dengan poin. Jika Anda lebih suka milimeter, konversikan menggunakan `1 mm ≈ 2.83465 pt`. Misalnya, `Position(25.4, 254)` menempatkan paragraf 1 cm dari kiri dan 9 cm dari bawah.

### Bagaimana jika saya perlu menambahkan banyak tag (heading, tabel)?

Cukup buat objek `StructureElement` tambahan dengan tag seperti `"H1"` untuk heading atau `"Table"` untuk tabel, lalu tambahkan konten yang bersesuaian sebagai anaknya. Penumpukan (nesting) bekerja dengan cara yang sama—anak akan mewarisi urutan logis dari induknya.

### Apakah pendekatan ini bekerja untuk PDF/A‑1b atau PDF/A‑3b?

Ya. Ganti `SaveFormat.PdfA2b` dengan `SaveFormat.PdfA1b` atau `SaveFormat.PdfA3b`. Perlu diingat bahwa setiap versi PDF/A memiliki seperangkat metadata yang wajib; Aspose.Pdf akan memberi peringatan jika ada yang kurang.

---

## Ringkasan

Kami telah membahas skenario **create pdf document c#** yang:

1. Menginisialisasi PDF baru menggunakan Aspose.Pdf.  
2. **Position text in PDF** dengan menetapkan koordinat yang tepat.  
3. **Add structural tree** untuk meningkatkan aksesibilitas.  
4. Menyimpan hasil sebagai file PDF/A‑2b yang mematuhi standar.

Semua langkah bersifat mandiri, dan Anda dapat menyesuaikan potongan kode ini untuk tata letak yang lebih kompleks, banyak halaman, atau tipe tag yang berbeda.

---

## Apa Selanjutnya?

- **Styling text** – jelajahi `TextState` untuk mengubah font, warna, dan ukuran.  
- **Embedding images** – gunakan `ImageFragment` dan posisikan bersama paragraf.  
- **Generating tables** – buat objek `Table` dan beri tag `"Table"` untuk semantik yang lebih kaya.  
- **Automation pipelines** – integrasikan kode ini ke layanan latar belakang yang menghasilkan faktur setiap malam.

Silakan bereksperimen, dan beri tahu kami variasi mana yang paling berguna bagi Anda. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Buat PDF Ber‑tag dengan Aspose.PDF untuk .NET: Panduan Lengkap untuk Meningkatkan Aksesibilitas dan Struktur Dokumen](/pdf/english/net/advanced-features/create-tagged-pdfs-aspose-pdf-net/)
- [Buat Dokumen PDF dengan Aspose.PDF – Panduan Langkah demi Langkah](/pdf/english/net/document-creation/create-pdf-document-with-aspose-pdf-step-by-step-guide/)
- [Buat & Putar Teks dalam PDF Menggunakan Aspose.PDF .NET: Panduan Komprehensif untuk Pengembang](/pdf/english/net/text-operations/create-rotate-text-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}