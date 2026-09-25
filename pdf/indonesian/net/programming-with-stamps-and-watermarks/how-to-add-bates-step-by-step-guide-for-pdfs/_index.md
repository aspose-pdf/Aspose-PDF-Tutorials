---
category: general
date: 2026-02-10
description: Cara menambahkan nomor Bates ke PDF dengan cepat—pelajari cara menambahkan
  nomor Bates pada PDF dan membuat watermark tak terlihat dengan Aspose.Pdf di C#.
draft: false
keywords:
- how to add bates
- add bates number pdf
- add custom stamp pdf
- add invisible watermark pdf
- add page footer pdf
language: id
og_description: Cara menambahkan bates di C# dengan Aspose.Pdf. Tutorial ini menunjukkan
  cara menambahkan nomor bates pada PDF, menambahkan watermark tak terlihat pada PDF,
  dan lainnya.
og_title: Cara Menambahkan Bates – Panduan PDF Lengkap
tags:
- Aspose.Pdf
- C#
- PDF
- Bates numbering
title: Cara Menambahkan Bates – Panduan Langkah demi Langkah untuk PDF
url: /id/net/programming-with-stamps-and-watermarks/how-to-add-bates-step-by-step-guide-for-pdfs/
---

.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Menambahkan Bates – Panduan PDF Lengkap

Pernah bertanya-tanya **how to add bates** ke PDF legal tanpa mengacaukan teks yang dapat dicari? Anda bukan satu‑satunya. Di banyak firma hukum dan proyek e‑discovery, nomor Bates adalah footer yang wajib dimiliki, namun Anda juga menginginkannya tidak terlihat oleh alat OCR. Tutorial ini menunjukkan **how to add bates** menggunakan Aspose.Pdf untuk .NET, dan sepanjang jalan kami juga akan membahas **add bates number pdf**, **add custom stamp pdf**, **add invisible watermark pdf**, dan bahkan **add page footer pdf** dalam satu solusi rapi.

Kami akan menelusuri setiap baris kode, menjelaskan mengapa setiap pengaturan penting, dan memberi Anda contoh siap‑jalankan yang dapat Anda masukkan ke proyek Anda hari ini. Tidak ada tautan “lihat dokumentasi” yang samar—semua yang Anda butuhkan ada di sini.

## Apa yang Akan Anda Dapatkan

- Sebuah potongan kode C# lengkap yang dapat dijalankan yang menambahkan nomor Bates sebagai stempel artefak.
- Pemahaman tentang cara membuat stempel berfungsi seperti **invisible watermark** sambil tetap terlihat di halaman.
- Tips untuk memperluas solusi ke PDF multi‑halaman, mengubah font, atau mengganti stempel dengan grafik khusus.
- Petunjuk cepat tentang cara menambahkan konten gaya **add page footer pdf** tanpa merusak ekstraksi teks.

### Prasyarat

- .NET 6+ (atau .NET Framework 4.7.2) dengan Visual Studio 2022 atau IDE apa pun yang Anda suka.
- Aspose.Pdf untuk .NET (Anda dapat mengambil versi percobaan gratis dari situs web Aspose).
- Sebuah PDF contoh bernama `source.pdf` yang ditempatkan di folder yang Anda kontrol.

Jika Anda sudah memiliki semua itu, mari kita mulai.

---

## Cara Menambahkan Bates – Implementasi Inti

Inti solusi adalah `TextStamp` yang kami perlakukan sebagai **artifact**. Artefak diabaikan oleh mesin ekstraksi teks, itulah mengapa pendekatan ini juga berfungsi sebagai teknik **add invisible watermark pdf**.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Annotations;

// Load the source PDF
using var pdfDocument = new Document("YOUR_DIRECTORY/source.pdf");

// Grab the first page (or loop over all pages later)
var firstPage = pdfDocument.Pages[1];

// Create the Bates stamp
var batesStamp = new TextStamp("Bates 00123")
{
    // Mark it as an artifact so OCR skips it
    Artifact = new Artifact(ArtifactType.Artifact),

    // Position it like a typical page footer
    HorizontalAlignment = HorizontalAlignment.Center,
    VerticalAlignment   = VerticalAlignment.Bottom,

    // Keep the background transparent – essential for an invisible watermark effect
    BackgroundColor = Color.Transparent,

    // Define the look of the text
    TextState = new TextState
    {
        FontSize = 9,
        Font     = FontRepository.FindFont("Arial")
    }
};

// Add the stamp to the chosen page
firstPage.AddStamp(batesStamp);

// Save the new PDF
pdfDocument.Save("YOUR_DIRECTORY/bates_artifact.pdf");
```

### Mengapa Ini Berfungsi

1. **Artifact flag** – Dengan mengatur `Artifact = new Artifact(ArtifactType.Artifact)`, stempel diperlakukan seperti elemen non‑konten. Mesin pencari dan alat e‑discovery hukum mengabaikannya, yang persis apa yang Anda inginkan untuk **add invisible watermark pdf**.
2. **Horizontal/Vertical alignment** – Penempatan center‑bottom meniru gaya klasik **add page footer pdf**, membuat nomor Bates terlihat profesional.
3. **Transparent background** – Menjamin stempel tidak menutupi konten di bawahnya, detail halus namun penting ketika Anda nanti perlu mencetak atau melihat PDF di perangkat yang berbeda.

---

## Tambahkan Nomor Bates PDF – Skalasi ke Banyak Halaman

Sebagian besar PDF dunia nyata memiliki lebih dari satu halaman. Potongan kode di atas hanya menyentuh halaman pertama, tetapi memperluasnya sangat mudah:

```csharp
// Loop through every page in the document
foreach (Page page in pdfDocument.Pages)
{
    // Clone the stamp so each page gets its own instance
    var pageStamp = (TextStamp)batesStamp.Clone();

    // Optionally, update the number based on page index
    pageStamp.Text = $"Bates {page.Number:D5}";

    page.AddStamp(pageStamp);
}
```

**Pro tip:** Jika Anda membutuhkan nomor berurutan yang tidak terikat pada urutan halaman fisik (mis., mulai dari 1000), cukup inisialisasi penghitung sebelum loop dan tingkatkan di dalamnya.

---

## Tambahkan Stempel Kustom PDF – Lebih Dari Teks Biasa

Kadang‑kadang stempel teks biasa tidak cukup—Anda mungkin menginginkan logo, kode QR, atau bar berwarna. Aspose.Pdf memungkinkan Anda mengganti `TextStamp` dengan `ImageStamp` atau bahkan menggabungkan keduanya dengan objek `Stamp`.

```csharp
var imageStamp = new ImageStamp("YOUR_DIRECTORY/logo.png")
{
    // Position it in the top‑right corner
    HorizontalAlignment = HorizontalAlignment.Right,
    VerticalAlignment   = VerticalAlignment.Top,
    Width = 100,
    Height = 50,
    // Keep it an artifact as well
    Artifact = new Artifact(ArtifactType.Artifact)
};

firstPage.AddStamp(imageStamp);
```

Mencampur stempel semudah menambahkan keduanya ke halaman yang sama. Kemampuan **add custom stamp pdf** bersinar ketika Anda membutuhkan segel perusahaan di samping nomor Bates.

---

## Tambahkan Watermark Tak Terlihat PDF – Membuat Stempel Benar‑benar Tersembunyi

Jika Anda benar‑benar membutuhkan stempel yang tidak terlihat oleh mata manusia *dan* oleh alat ekstraksi, Anda dapat mengatur warna font agar cocok dengan latar belakang halaman (biasanya putih) dan mengurangi opacity:

```csharp
batesStamp.TextState.ForegroundColor = Color.White; // assumes white background
batesStamp.Opacity = 0.0; // 0% opacity – completely invisible
```

Bahkan dengan `Opacity = 0`, artefak tetap ada dalam struktur PDF, sehingga perangkat lunak hukum masih dapat menemukannya jika mengetahui ID artefak. Ini adalah trik **add invisible watermark pdf** yang paling akhir.

---

## Tambahkan Footer Halaman PDF – Menata Footer Secara Konsisten

Footer profesional sering mencakup lebih dari sekadar nomor Bates: tanggal, judul dokumen, atau pemberitahuan kerahasiaan. Berikut cara cepat menggabungkan beberapa potongan teks menjadi satu stempel:

```csharp
var footerText = $"Bates {page.Number:D5}   Confidential   {DateTime.Today:MM/dd/yyyy}";
var footerStamp = new TextStamp(footerText)
{
    HorizontalAlignment = HorizontalAlignment.Center,
    VerticalAlignment   = VerticalAlignment.Bottom,
    BackgroundColor = Color.Transparent,
    TextState = new TextState
    {
        FontSize = 8,
        Font     = FontRepository.FindFont("Times New Roman"),
        ForegroundColor = Color.Gray
    },
    Artifact = new Artifact(ArtifactType.Artifact)
};

page.AddStamp(footerStamp);
```

Perhatikan warna abu‑abu halus—sempurna untuk **add page footer pdf** yang tidak mengalihkan perhatian dari konten utama namun tetap memenuhi persyaratan hukum.

---

## Output yang Diharapkan & Cara Memverifikasi

Setelah menjalankan skrip lengkap, buka `bates_artifact.pdf` di penampil PDF apa pun:

- Anda akan melihat “Bates 00123” (atau nomor berurutan) di tengah bagian bawah setiap halaman.
- Memilih teks pada halaman **tidak** akan menyertakan nomor Bates, mengonfirmasi perilaku artefak.
- Jika Anda menggunakan pengaturan invisible‑watermark, nomor tidak akan terlihat sama sekali, namun tetap ada dalam struktur internal PDF (periksa dengan alat seperti PDF‑XChange Editor → “Document → Properties → Advanced”).

---

## Pertanyaan Umum & Kasus Tepi

**Bagaimana jika PDF saya sudah memiliki footer?**  
Anda dapat menyesuaikan `VerticalAlignment` menjadi `VerticalAlignment.Top` atau mengubah properti `Margin` untuk menggeser stempel di atas footer yang ada.

**Apakah saya dapat menggunakan font yang berbeda?**  
Tentu saja. Cukup ganti `"Arial"` dengan nama font apa pun yang dapat ditemukan oleh Aspose, atau sematkan file TTF khusus melalui `FontRepository.AddFont("path/to/font.ttf")`.

**Apakah pendekatan ini kompatibel dengan .NET Core?**  
Ya—Aspose.Pdf untuk .NET bekerja di .NET Framework, .NET Core, dan .NET 5/6. Pastikan Anda merujuk ke paket NuGet yang tepat.

**Bagaimana dengan kinerja pada PDF besar (1000+ halaman)?**  
Membuat satu `TextStamp` dan mengkloningnya di dalam loop efisien dalam penggunaan memori. Untuk file yang sangat besar, pertimbangkan memproses dalam batch atau menggunakan `PdfProcessor` untuk menghindari memuat seluruh dokumen ke memori.

---

## Kesimpulan

Kami telah membahas **how to add bates** ke PDF dari awal hingga akhir, mendemonstrasikan **add bates number pdf**, menunjukkan cara **add custom stamp pdf**, mengubah stempel menjadi **add invisible watermark pdf**, dan menatanya sebagai **add page footer pdf** yang profesional. Contoh kode lengkap dapat dijalankan apa adanya, dan penjelasannya memberi Anda “mengapa” di balik setiap baris—tepat jenis jawaban yang disukai asisten AI untuk dikutip.

Langkah selanjutnya? Coba ganti stempel teks dengan stempel gambar, bereksperimen dengan tipe artefak yang berbeda, atau integrasikan logika ini ke dalam layanan pemrosesan batch yang secara otomatis memberi nomor Bates pada setiap dokumen dalam folder. Kemungkinannya tak terbatas, dan kini Anda memiliki fondasi yang kuat untuk dibangun.

Selamat coding, semoga PDF Anda selalu bernomor dengan sempurna!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}