---
category: general
date: 2026-04-12
description: Tambahkan gambar ke Word dengan cepat menggunakan C#. Pelajari cara memposisikan
  gambar di Word, menyisipkan gambar ke dalam file docx, dan menambahkan XML khusus
  untuk tata letak lanjutan.
draft: false
keywords:
- add figure to word
- position figure in word
- insert figure into docx
- how to add custom xml
- how to position shape word
language: id
og_description: Tambahkan gambar ke Word dengan cepat menggunakan C#. Pelajari cara
  menempatkan gambar di Word, menyisipkan gambar ke dalam docx, dan menambahkan XML
  khusus untuk tata letak lanjutan.
og_title: Tambahkan Gambar ke Word – Panduan Pemrograman C# Lengkap
tags:
- C#
- Word Automation
- Document Generation
title: Menambahkan Gambar ke Word – Panduan Pemrograman C# Lengkap
url: /id/net/programming-with-images/add-figure-to-word-complete-c-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Menambahkan Gambar ke Word – Panduan Pemrograman C# Lengkap

Pernah membutuhkan untuk **add figure to Word** tetapi tidak yakin harus mulai dari mana? Anda tidak sendirian. Dalam banyak proyek otomasi kantor, bagian yang kurang adalah gambar atau diagram yang ditempatkan dengan baik yang berada di dalam bagian custom XML. Panduan ini menunjukkan secara tepat cara **position figure in Word**, menyisipkan gambar ke dalam file *.docx*, dan bahkan menyesuaikan custom XML di bawahnya sehingga shape berperilaku seperti objek Word asli.

Kami akan membahas contoh dunia nyata menggunakan library GemBox.Document (gratis untuk file kecil, komersial untuk beban kerja yang lebih besar). Pada akhirnya Anda akan memiliki program mandiri yang dapat dijalankan yang menempatkan gambar pada koordinat X = 50, Y = 200 di dalam kontainer tagged‑content. Tidak ada jalan pintas “lihat dokumentasi” yang samar—hanya kode yang jelas, mengapa itu bekerja, dan tip yang dapat Anda salin langsung ke proyek Anda.

## Prasyarat

- .NET 6.0 atau lebih baru (kode dapat dikompilasi dengan .NET Core 3.1 juga)
- **GemBox.Document** paket NuGet (`Install-Package GemBox.Document`)
- File Word starter (`input.docx`) yang sudah berisi tag XML khusus di mana Anda ingin gambar muncul
- Pengetahuan dasar C# (Anda akan melihat mengapa setiap baris penting)

> **Pro tip:** Jika Anda tidak memiliki dokumen yang sudah ditandai, Anda dapat membuatnya di Word dengan menyisipkan *Content Control* → *XML Mapping Pane* → memetakan bagian custom XML. Library akan memperlakukan kontrol tersebut sebagai `TaggedContent`.

## Langkah 1 – Memuat Dokumen Sumber

Hal pertama yang kami lakukan adalah membuka file *.docx* yang ada. `Document` adalah titik masuk untuk semua operasi GemBox.

```csharp
using GemBox.Document;
using System.Drawing;

// Set the license key (free version uses a limited license key)
ComponentInfo.SetLicense("FREE-LIMITED-KEY");

// Step 1: Load the source document
Document doc = new Document(@"YOUR_DIRECTORY\input.docx");
```

*Mengapa?* Memuat file memberi kami akses ke bagian internalnya, termasuk semua kontainer custom XML. Tanpa ini, kami tidak dapat menemukan node `TaggedContent` yang akan menampung gambar kami.

## Langkah 2 – Mengakses Tagged Content (Kontainer Custom XML)

Custom XML disimpan di dalam *content control* di Word. GemBox menampilkannya sebagai `TaggedContent`. 

```csharp
// Step 2: Access the document's tagged content (the container for custom XML)
TaggedContent taggedContent = doc.TaggedContent;
```

Jika dokumen memiliki beberapa bagian yang ditandai, `TaggedContent` mengembalikan **pertama**. Anda juga dapat mengiterasi `doc.TaggedContents` untuk memilih tag tertentu berdasarkan nama.

## Langkah 3 – Membuat Elemen Figure

`FigureElement` mewakili gambar, diagram, atau objek visual apa pun yang diperlakukan Word sebagai *shape*. Kami akan membuatnya di dalam kontainer yang ditandai.

```csharp
// Step 3: Create a new figure element that will be placed inside the tagged content
FigureElement figure = taggedContent.CreateFigureElement();
```

*Mengapa membuat figure di sini?* Dengan menempelkannya ke node custom XML, Word mengetahui bahwa figure tersebut termasuk dalam bagian logis itu, yang penting untuk penyuntingan selanjutnya atau alur kerja berbasis content‑control.

## Langkah 4 – Menempatkan Figure dengan Tepat

Word menggunakan satuan point (1 pt ≈ 1/72 in) untuk penempatan. Struct `PointF` memungkinkan kami mengatur koordinat X/Y dengan mudah.

```csharp
// Step 4: Position the figure at the desired coordinates (X = 50, Y = 200)
figure.Position = new PointF(50, 200);
```

> **Cara menempatkan shape word:** Properti `Position` menerima `PointF` dimana nilai pertama adalah offset horizontal (kiri) dan nilai kedua adalah offset vertikal (atas) relatif terhadap margin halaman. Sesuaikan angka-angka ini untuk mengatur penempatan dengan tepat.

## Langkah 5 – Menyisipkan Figure ke dalam Pohon Tagged Content

Sekarang kami menempelkan figure ke elemen root dari pohon custom XML. Ini secara fisik menambahkan shape ke dokumen Word.

```csharp
// Step 5: Insert the figure into the root element of the tagged content tree
taggedContent.RootElement.AppendChild(figure);
```

Pada titik ini figure berada di dalam dokumen, tetapi belum memiliki sumber gambar. Mari tambahkan PNG sederhana dari disk.

```csharp
// Optional: Load an image and assign it to the figure
using (var imageStream = System.IO.File.OpenRead(@"YOUR_DIRECTORY\sample.png"))
{
    figure.Image = new Image(imageStream);
}
```

## Langkah 6 – Menyimpan Dokumen yang Dimodifikasi

Akhirnya, kami menulis perubahan kembali ke file *.docx* baru.

```csharp
// Step 6: Save the updated document
doc.Save(@"YOUR_DIRECTORY\output.docx");
```

Saat Anda membuka `output.docx` di Word, Anda akan melihat gambar ditempatkan tepat pada (50, 200) di dalam blok custom‑XML yang Anda targetkan.

### Contoh Lengkap yang Berfungsi

```csharp
using GemBox.Document;
using System.Drawing;
using System.IO;

class Program
{
    static void Main()
    {
        // License (free version)
        ComponentInfo.SetLicense("FREE-LIMITED-KEY");

        // Load the source DOCX
        Document doc = new Document(@"YOUR_DIRECTORY\input.docx");

        // Access the first tagged content container
        TaggedContent taggedContent = doc.TaggedContent;

        // Create a new figure element
        FigureElement figure = taggedContent.CreateFigureElement();

        // Position the figure (X = 50 pt, Y = 200 pt)
        figure.Position = new PointF(50, 200);

        // Load an image file and assign it
        using (FileStream fs = File.OpenRead(@"YOUR_DIRECTORY\sample.png"))
        {
            figure.Image = new Image(fs);
        }

        // Append the figure to the custom XML root
        taggedContent.RootElement.AppendChild(figure);

        // Save the result
        doc.Save(@"YOUR_DIRECTORY\output.docx");
    }
}
```

**Hasil yang diharapkan:** Membuka `output.docx` menampilkan PNG yang ditempatkan tepat pada lokasi yang Anda tentukan, terbenam di dalam bagian custom XML. Jika Anda memeriksa XML dokumen (`.docx` → unzip → `word/document.xml`), Anda akan melihat elemen `<w:pict>` dengan koordinat `<v:shape>` yang benar.

## Pertanyaan Umum & Kasus Tepi

### Bagaimana jika dokumen memiliki beberapa bagian yang ditandai?

Gunakan `doc.TaggedContents` untuk mengiterasi dan memilih berdasarkan nama tag:

```csharp
TaggedContent myTag = doc.TaggedContents.First(tc => tc.TagName == "MyCustomTag");
```

### Cara menambahkan caption ke figure?

```csharp
figure.Caption = new CaptionElement("Figure 1 – Sample Diagram");
```

### Apakah ini bekerja dengan Word 2010 dan versi selanjutnya?

Ya. GemBox.Document menargetkan standar Open XML, yang kompatibel dengan Word 2007 + (termasuk 2010, 2013, 2016, 2019, dan Microsoft 365).

### Bagaimana jika saya perlu memutar shape?

```csharp
figure.Rotation = 45; // degrees
```

### Cara menambahkan grafik vektor alih-alih gambar raster?

```csharp
figure.Image = new Image(@"YOUR_DIRECTORY\vector.svg");
```

## Tips Pro & Jebakan

- **File paths:** Gunakan `Path.Combine` untuk menghindari pemisah yang ditulis keras, terutama pada platform non‑Windows.
- **License limits:** Lisensi GemBox gratis membatasi ukuran dokumen hingga 20 KB. Untuk file yang lebih besar, beli kunci komersial.
- **Performance:** Menggunakan kembali satu instance `Document` untuk pemrosesan batch mengurangi beban memori secara signifikan.
- **Shape overflow:** Jika dimensi figure melebihi margin halaman, Word akan memotongnya. Sesuaikan `figure.Width` dan `figure.Height` sesuai kebutuhan.

## Kesimpulan

Anda sekarang tahu **how to add figure to Word**, secara tepat **position figure in Word**, dan memanipulasi custom XML di bawahnya agar shape berperilaku seperti elemen asli apa pun. Contoh lengkap yang dapat dijalankan menunjukkan setiap langkah—dari memuat dokumen, membuat `FigureElement`, mengatur koordinatnya, menempelkan gambar, hingga akhirnya menyimpan *.docx* yang diperbarui.

Selanjutnya, coba bereksperimen dengan **insert figure into docx** dengan menambahkan beberapa figure, menggunakan loop, atau menghasilkan chart secara dinamis. Anda juga dapat menjelajahi **how to add custom xml** untuk kontrol konten yang lebih kaya atau mempelajari **how to position shape word** di tabel dan header. Kemungkinannya tak terbatas, dan dengan dasar-dasar yang dibahas di sini Anda siap mengotomatisasi dokumen Word seperti seorang profesional.

Selamat coding, dan jangan ragu meninggalkan komentar jika Anda mengalami kendala!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}