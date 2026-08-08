---
category: general
date: 2026-03-24
description: Buat dokumen PDF dan pelajari cara mengatur posisi absolut untuk teks
  ber‑tag. Tutorial ini menunjukkan cara menambahkan elemen span, cara menambahkan
  konten ber‑tag, dan memposisikan teks pada halaman.
draft: false
keywords:
- create pdf document
- set absolute position
- add span element
- how to add tagged
- position text on page
language: id
og_description: Buat dokumen PDF dan langsung lihat cara mengatur posisi absolut,
  menambahkan elemen span, serta menempatkan teks pada halaman dengan konten PDF ber-tag.
og_title: Buat Dokumen PDF – Penempatan Absolut Teks yang Ditandai
tags:
- Aspose.Pdf
- C#
- PDF Tagging
title: Buat Dokumen PDF – Atur Posisi Absolut untuk Teks Berlabel
url: /id/net/programming-with-tagged-pdf/create-pdf-document-set-absolute-position-for-tagged-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat Dokumen PDF – Atur Posisi Absolut untuk Teks Ber‑tag

Pernahkah Anda perlu **membuat dokumen pdf** yang berisi teks ber‑tag yang dapat diakses dan ditempatkan tepat di mana Anda inginkan? Mungkin Anda sedang membuat PDF bergaya formulir di mana label harus berada pada koordinat yang tepat, atau Anda sedang menghasilkan sertifikat dan nama harus sejajar sempurna dengan gambar latar belakang.  

Dalam panduan ini kami akan menelusuri contoh lengkap yang dapat dijalankan yang menunjukkan **cara menambahkan konten ber‑tag**, **mengatur posisi absolut**, dan **menambahkan elemen span** sehingga Anda dapat **menempatkan teks pada halaman** tanpa menebak‑tebakan. Tanpa referensi eksternal—hanya kode yang dapat Anda salin‑tempel, plus penjelasan “mengapa” di balik setiap baris.

## Prasyarat

- .NET 6+ (atau .NET Framework 4.6+) dengan kompiler C#  
- Aspose.Pdf untuk .NET (versi terbaru pada saat penulisan, 23.12) terpasang via NuGet  
- Familiaritas dasar dengan sintaks C#  

Jika Anda sudah memiliki semua itu, mari kita mulai.

---

## Buat Dokumen PDF – Mengatur Posisi Absolut

Hal pertama yang kami lakukan adalah menginstansiasi `Document` kosong. Objek ini mewakili seluruh file PDF dan memberi kami akses ke pohon konten ber‑tag.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Tagged;

// Step 1: Create a new PDF document
using var pdfDocument = new Document();
```

**Mengapa ini penting:**  
`Document` adalah akar dari struktur PDF. Dengan membuatnya terlebih dahulu kami memastikan ada kanvas untuk elemen visual (halaman, grafik) dan struktur logis (tag). Pernyataan `using` menjamin file dibuang dengan benar, yang mencegah kebocoran handle file di Windows.

---

## Aktifkan Konten Ber‑tag (Cara Menambahkan Tag)

Sebelum kami dapat menyisipkan elemen ber‑tag apa pun, dokumen harus ditandai sebagai *tagged*. Aspose.Pdf secara otomatis membuat objek `TaggedContent`, tetapi Anda tetap harus mengaktifkan benderanya.

```csharp
// Step 2: Mark the document as tagged (required for accessibility)
pdfDocument.TaggedContent = true;
```

**Apa yang terjadi di balik layar?**  
Menetapkan `TaggedContent` ke `true` memberi tahu pembaca PDF bahwa file berisi pohon struktur logis. Ini krusial bagi pembaca layar dan agar metode `SetPosition` berfungsi dengan benar pada elemen span.

---

## Dapatkan Elemen Root dari Pohon Konten Ber‑tag

Elemen root adalah titik masuk untuk semua tag struktural (seperti `<Document>`, `<Section>`, `<Span>`). Anggaplah ini sebagai “body” tak terlihat dari PDF.

```csharp
// Step 3: Retrieve the root element of the tag tree
var rootElement = pdfDocument.TaggedContent.RootElement;
```

**Mengapa kami membutuhkan root:**  
Semua tag selanjutnya harus terlampir di suatu tempat dalam pohon; jika tidak, mereka tidak akan muncul dalam hierarki aksesibilitas.

---

## Tambahkan Elemen Span – Blok Bangunan untuk Teks Inline

Sebuah *span* adalah padanan PDF dari `<span>` HTML—sempurna untuk potongan teks pendek yang ingin Anda posisikan secara tepat.

```csharp
// Step 4: Create a span element that will hold the text
var spanElement = rootElement.CreateSpanElement();
```

**Catatan desain:**  
Jika Anda memerlukan pemformatan lebih kaya (tebal, miring, hyperlink), Anda dapat membungkus span dalam `<Paragraph>` atau menggunakan objek `TextFragment` nanti. Untuk penempatan absolut, span biasa adalah yang paling ringan.

---

## Atur Posisi Absolut – X=100, Y=200

Sekarang bagian yang menyenangkan: menempatkan span pada lokasi tepat di halaman. Sistem koordinat dimulai dari sudut kiri‑bawah (0,0) dan menggunakan poin (1 pt ≈ 1/72 in).

```csharp
// Step 5: Position the span at an absolute location (X=100, Y=200)
spanElement.SetPosition(100, 200);
```

**Mengapa posisi absolut?**  
Ketika Anda memerlukan tata letak pixel‑perfect—pikirkan sertifikat, faktur, atau formulir—aliran relatif (seperti teks kiri‑ke‑kanan) tidak cukup. `SetPosition` melewati aliran teks normal dan menancapkan elemen di tempat yang Anda tentukan.

---

## Tambahkan Teks ke Span

Setelah span diposisikan, kami kini menyuntikkan string sebenarnya.

```csharp
// Step 6: Add the desired text to the span
spanElement.AddText("Positioned tagged text");
```

**Tip:**  
Jika Anda memerlukan karakter Unicode atau skrip kanan‑ke‑kiri, cukup berikan string; Aspose.Pdf menangani enkoding secara otomatis.

---

## Lampirkan Span ke Elemen Root

Akhirnya, kami menempelkan span ke pohon logis dokumen sehingga menjadi bagian dari PDF akhir.

```csharp
// Step 7: Append the span to the root so it becomes part of the PDF structure
rootElement.AppendChild(spanElement);
```

**Bagaimana jika Anda lupa langkah ini?**  
Span akan tetap ada di memori tetapi tidak pernah diserialisasi ke dalam file, sehingga Anda tidak akan melihat teks apa pun dan pohon aksesibilitas akan tidak lengkap.

---

## Contoh Lengkap yang Dapat Dijalankan

Berikut adalah program lengkap yang dapat Anda letakkan ke dalam aplikasi console. Program ini membuat PDF satu‑halaman, menambahkan span ber‑tag pada (100, 200), dan menyimpan file sebagai `TaggedPositioned.pdf`.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Tagged;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new PDF document
        using var pdfDocument = new Document();

        // 2️⃣ Enable tagging for accessibility
        pdfDocument.TaggedContent = true;

        // 3️⃣ Add a blank page (required for visual placement)
        var page = pdfDocument.Pages.Add();

        // 4️⃣ Get the root element of the tagged‑content tree
        var rootElement = pdfDocument.TaggedContent.RootElement;

        // 5️⃣ Create a span element that will hold the text
        var spanElement = rootElement.CreateSpanElement();

        // 6️⃣ Position the span at an absolute location on the page (X=100, Y=200)
        spanElement.SetPosition(100, 200);

        // 7️⃣ Add the desired text to the span
        spanElement.AddText("Positioned tagged text");

        // 8️⃣ Append the span to the root so it becomes part of the PDF structure
        rootElement.AppendChild(spanElement);

        // 9️⃣ Save the document
        pdfDocument.Save("TaggedPositioned.pdf");

        Console.WriteLine("PDF created successfully – check TaggedPositioned.pdf");
    }
}
```

**Output yang diharapkan:**  
Buka `TaggedPositioned.pdf` di penampil apa pun (Adobe Acrobat, Foxit, dll.). Anda akan melihat frasa **“Positioned tagged text”** tepat 100 pt dari tepi kiri dan 200 pt dari tepi bawah halaman. Jika Anda memeriksa panel *Tags*, elemen `<Span>` akan terdaftar di bawah root dokumen, mengonfirmasi bahwa konten telah ditandai dengan benar.

---

## Pertanyaan Umum & Kasus Edge

### Bagaimana jika saya perlu menempatkan teks pada halaman tertentu selain halaman pertama?

Tambahkan halaman yang Anda inginkan (`var page = pdfDocument.Pages[3];`) sebelum memanggil `SetPosition`. Span akan otomatis terikat pada konteks halaman yang aktif.

### Bisakah saya mengatur posisi dalam inci atau sentimeter?

`SetPosition` menerima poin. Konversi menggunakan rumus:  
- **Inci → poin:** `points = inches * 72`  
- **Sentimeter → poin:** `points = cm * 28.3465`

### Bagaimana cara mengubah font atau warna span?

Setelah membuat span, Anda dapat mengambil `TextState`‑nya dan memodifikasinya:

```csharp
var textState = spanElement.TextState;
textState.Font = FontRepository.FindFont("Arial");
textState.FontSize = 12;
textState.ForegroundColor = Color.GetBlack();
```

### Bagaimana jika dokumen sudah memiliki tag yang ada?

Anda masih dapat membuat span baru dan menambahkannya ke elemen yang ada (`rootElement`, sebuah `<Section>` tertentu, dll.). Pastikan Anda mempertahankan hierarki logis—pembaca layar mengharapkan pohon yang terstruktur dengan baik.

### Apakah ini bekerja dengan kepatuhan PDF/A atau PDF/UA?

Ya. PDF ber‑tag merupakan persyaratan inti untuk PDF/UA. Jika Anda memerlukan PDF/A, panggil `pdfDocument.Convert(new PdfAConversionOptions(PdfAStandard.PdfA_1b));` setelah membangun konten.

---

## Pro Tips & Pitfalls

- **Pro tip:** Selalu tambahkan halaman sebelum memposisikan konten. Tanpa halaman, `SetPosition` gagal secara diam‑diam karena tidak ada tempat untuk merender.
- **Perhatikan satuan:** Mencampur pixel dari desain UI dengan poin PDF akan memindahkan teks Anda. Periksa konversi Anda dua kali.
- **Petunjuk kinerja:** Jika Anda menghasilkan ribuan PDF, gunakan kembali satu instance `Document` dan panggil `pdfDocument.Pages.Clear()` di antara proses untuk menghindari alokasi memori berlebih.
- **Pengingat aksesibilitas:** Tagging bukan sekadar tambahan; banyak regulasi (Section 508, EN 301 549) mewajibkannya. Menggunakan `CreateSpanElement` memastikan teks dapat ditemukan oleh teknologi bantu.

---

## Kesimpulan

Kami baru saja **membuat dokumen pdf** dari awal, **mengatur posisi absolut**, **menambahkan elemen span**, dan mendemonstrasikan **cara menambahkan konten ber‑tag** sehingga Anda dapat **menempatkan teks pada halaman** dengan akurasi pixel‑perfect. Contoh lengkap siap dijalankan, dan penjelasan mencakup baik *bagaimana* maupun *mengapa*—tepat apa yang dicari pengembang (dan asisten AI) ketika mereka membutuhkan solusi yang dapat diandalkan.

Selanjutnya, Anda dapat mengeksplor:

- Menambahkan gambar di belakang teks yang diposisikan untuk sertifikat ber‑watermark.  
- Menggunakan `CreateParagraphElement` untuk blok multi‑baris yang tetap memerlukan penempatan absolut.  
- Mengekspor ke PDF/UA untuk memenuhi audit aksesibilitas yang ketat.  

Jangan ragu mengubah koordinat, font, atau warna—eksperimen adalah cara tercepat menguasai pembuatan PDF ber‑tag. Jika Anda menemui kendala, tinggalkan komentar di bawah; selamat coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}