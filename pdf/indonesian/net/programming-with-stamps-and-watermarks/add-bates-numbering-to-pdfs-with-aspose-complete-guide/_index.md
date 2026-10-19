---
category: general
date: 2026-04-25
description: Tambahkan penomoran Bates ke PDF dengan cepat menggunakan Aspose.Pdf.
  Pelajari cara menambahkan nomor halaman PDF, menyesuaikan ukuran font secara otomatis,
  dan menambahkan watermark teks dalam C#.
draft: false
keywords:
- add bates numbering
- add page numbers pdf
- auto adjust font size
- how to add bates
- add text watermark
language: id
og_description: Tambahkan penomoran Bates ke PDF dengan Aspose.Pdf. Panduan ini menunjukkan
  cara menambahkan nomor halaman PDF, menyesuaikan ukuran font secara otomatis, dan
  menambahkan watermark teks dalam satu contoh yang dapat dijalankan.
og_title: Tambahkan Penomoran Bates ke PDF – Tutorial Lengkap Aspose.C#
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Tambahkan Penomoran Bates ke PDF dengan Aspose – Panduan Lengkap
url: /id/net/programming-with-stamps-and-watermarks/add-bates-numbering-to-pdfs-with-aspose-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Menambahkan Penomoran Bates ke PDF dengan Aspose – Panduan Lengkap

Pernah perlu **menambahkan penomoran bates** ke PDF tetapi tidak yakin harus mulai dari mana? Anda tidak sendirian—tim hukum, auditor, dan pengembang pun menghadapi hal ini setiap hari. Kabar baik? Dengan Aspose.Pdf untuk .NET Anda dapat menempelkan nomor Bates, secara otomatis menyesuaikan ukuran font, dan bahkan memperlakukan stempel tersebut sebagai watermark teks halus—semua dalam beberapa baris C#.

Dalam tutorial ini kami akan membahas langkah‑langkah tepat untuk **menambahkan nomor halaman pdf**, menyesuaikan font agar tidak pernah meluap, dan menjawab pertanyaan “cara menambahkan bates” sekali dan untuk selamanya. Pada akhir tutorial Anda akan memiliki aplikasi konsol siap‑jalankan yang menghasilkan PDF dengan penomoran profesional, dan Anda akan melihat cara memperluasnya menjadi solusi watermark lengkap.

## Prasyarat

* **Aspose.Pdf for .NET** (paket NuGet terbaru per April 2026).  
* .NET 6.0 SDK atau yang lebih baru – API berfungsi sama pada .NET Framework, tetapi .NET 6 memberikan kinerja terbaik.  
* Sebuah PDF contoh bernama `input.pdf` yang ditempatkan di folder yang dapat Anda referensikan (misalnya `C:\Docs\`).  

Tidak ada konfigurasi tambahan yang diperlukan; perpustakaan ini berdiri sendiri.

---

## Langkah 1 – Memuat Dokumen PDF Sumber

Hal pertama yang kami lakukan adalah membuka file yang ingin diberi nomor. Kelas `Document` milik Aspose mewakili seluruh PDF, dan memuatnya semudah memberikan path ke konstruktor.

```csharp
using Aspose.Pdf;

string inputPath = @"C:\Docs\input.pdf";
Document pdfDocument = new Document(inputPath);
```

*Mengapa ini penting*: Memuat dokumen memberi Anda akses ke koleksi `Pages`, tempat kami akan menempelkan stempel Bates nanti. Jika file tidak ditemukan, Aspose akan melempar `FileNotFoundException` yang jelas, sehingga Anda tahu persis apa yang salah.

---

## Langkah 2 – Membuat Text Stamp untuk Nomor Bates

Sekarang kami membuat elemen visual yang akan muncul di setiap halaman. Kelas `TextStamp` memungkinkan Anda menyisipkan string apa pun, dan kami akan menggunakan placeholder `{page}-{total}` agar Aspose mengganti token tersebut secara otomatis.

```csharp
// Create a stamp that will display "Bates: 1-10", "Bates: 2-10", etc.
TextStamp batesStamp = new TextStamp("Bates: {page}-{total}")
{
    // Let the stamp automatically adjust its font size to fit the stamp rectangle
    AutoAdjustFontSizeToFitStampRectangle = true,
    // Optional: make the stamp look like a subtle watermark
    Opacity = 0.4,
    // Position the stamp at the bottom‑right corner
    XIndent = 20,
    YIndent = 20,
    HorizontalAlignment = HorizontalAlignment.Right,
    VerticalAlignment = VerticalAlignment.Bottom,
    // Choose a readable font
    Font = new Font(FontFamilyEnum.Helvetica, 12, FontStyle.Regular, Color.Black)
};
```

*Poin penting*:

* **auto adjust font size** – Menetapkan `AutoAdjustFontSizeToFitStampRectangle` ke `true` menjamin teks tidak pernah meluber keluar dari persegi panjang, yang sempurna untuk nomor halaman dengan panjang variabel.
* **add text watermark** – Dengan menurunkan `Opacity` kami mengubah nomor Bates menjadi watermark yang samar, memenuhi kebutuhan “add text watermark” tanpa langkah terpisah.
* **how to add bates** – Token `{page}` dan `{total}` adalah rahasia utama; Aspose menggantinya saat runtime, sehingga Anda tidak perlu menghitung apa pun secara manual.

---

## Langkah 3 – Menerapkan Stempel ke Setiap Halaman

Kesalahan umum adalah menempelkan hanya pada halaman pertama. Untuk benar‑benar **menambahkan nomor halaman pdf**, kita perlu melakukan loop melalui seluruh koleksi `Pages`.

```csharp
foreach (Page page in pdfDocument.Pages)
{
    // Clone the stamp for each page to avoid shared state issues
    page.AddStamp(batesStamp);
}
```

Mengapa clone? Metode `AddStamp` secara internal membuat salinan, tetapi secara eksplisit menggunakan instance baru setiap iterasi menghindari efek samping tidak sengaja jika Anda kemudian mengubah properti stempel (seperti mengubah warna untuk halaman tertentu).

---

## Langkah 4 – Menyimpan PDF yang Diperbarui

Dengan stempel yang sudah ditempatkan, menyimpan perubahan menjadi sederhana. Anda dapat menimpa file asli atau menulis ke lokasi baru—di sini kami akan menyimpan file baru bernama `output.pdf`.

```csharp
string outputPath = @"C:\Docs\output.pdf";
pdfDocument.Save(outputPath);
Console.WriteLine($"Bates‑numbered PDF saved to: {outputPath}");
```

Jika Anda membuka `output.pdf` Anda akan melihat setiap halaman berlabel “Bates: 1‑10”, “Bates: 2‑10”, … tepat di kanan‑bawah, dengan opacity yang samar yang berfungsi juga sebagai **add text watermark**.

---

## Contoh Lengkap yang Berfungsi

Menggabungkan semuanya, berikut adalah program konsol tunggal yang berdiri sendiri yang dapat Anda salin‑tempel ke Visual Studio.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Drawing;
using Aspose.Pdf.Annotations;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source PDF
        string inputPath = @"C:\Docs\input.pdf";
        Document pdfDocument = new Document(inputPath);

        // 2️⃣ Create a Bates number stamp with auto‑adjusted font size
        TextStamp batesStamp = new TextStamp("Bates: {page}-{total}")
        {
            AutoAdjustFontSizeToFitStampRectangle = true,
            Opacity = 0.4, // acts as a subtle watermark
            XIndent = 20,
            YIndent = 20,
            HorizontalAlignment = HorizontalAlignment.Right,
            VerticalAlignment = VerticalAlignment.Bottom,
            Font = new Font(FontFamilyEnum.Helvetica, 12, FontStyle.Regular, Color.Black)
        };

        // 3️⃣ Add the stamp to every page (adds page numbers pdf)
        foreach (Page page in pdfDocument.Pages)
        {
            page.AddStamp(batesStamp);
        }

        // 4️⃣ Save the result
        string outputPath = @"C:\Docs\output.pdf";
        pdfDocument.Save(outputPath);
        Console.WriteLine($"Bates‑numbered PDF saved to: {outputPath}");
    }
}
```

**Hasil yang diharapkan**: Buka `output.pdf` di penampil apa pun; setiap halaman menampilkan baris seperti “Bates: 3‑12” di sudut kanan‑bawah, berukuran tepat untuk persegi panjang dan ditampilkan dengan opacity 40 %. Ini memenuhi baik persyaratan pelacakan hukum maupun kebutuhan watermark visual.

---

## Variasi Umum & Kasus Tepi

| Situation | What to change | Why |
|-----------|----------------|-----|
| **Penempatan berbeda** | Sesuaikan `HorizontalAlignment` / `VerticalAlignment` atau atur `XIndent`/`YIndent` | Beberapa perusahaan lebih menyukai penempatan kiri‑atas atau tengah. |
| **Awalan khusus** | Ganti `"Bates: "` dengan `"Doc‑ID: "` atau string apa pun | Anda mungkin menggunakan konvensi penamaan yang berbeda. |
| **Beberapa stempel** | Buat `TextStamp` kedua (misalnya untuk pemberitahuan kerahasiaan) dan tambahkan setelah yang pertama | Menggabungkan **add bates numbering** dengan persyaratan **add text watermark** lainnya sangat mudah. |
| **Jumlah halaman besar** | Tingkatkan ukuran font awal (misalnya `14`) – auto‑adjust akan memperkecilnya bila diperlukan | Ketika Anda memiliki > 999 halaman, string menjadi lebih panjang; auto‑adjust mencegah pemotongan. |
| **PDF terenkripsi** | Panggil `pdfDocument.Decrypt("password")` sebelum menempelkan | Anda tidak dapat memodifikasi file yang diamankan tanpa kata sandi. |

---

## Tips Pro & Jebakan

* **Pro tip:** Atur `batesStamp.Margin = new MarginInfo(5, 5, 5, 5)` jika Anda melihat teks menempel pada tepi halaman.  
* **Waspadai:** Persegi panjang yang sangat kecil (ukuran default 100 × 30 pt). Jika Anda membutuhkan area yang lebih besar, atur `batesStamp.Width` dan `batesStamp.Height` secara manual.  
* **Catatan performa:** Menempelkan ribuan halaman dapat memakan beberapa detik, tetapi Aspose men‑stream halaman secara efisien—tidak perlu memuat seluruh dokumen ke memori.  

---

## Kesimpulan

Kami baru saja menunjukkan cara **menambahkan penomoran bates** ke PDF menggunakan Aspose.Pdf, sekaligus **menambahkan nomor halaman pdf**, mengaktifkan **auto adjust font size**, dan membuat **add text watermark** dalam satu alur yang terpadu. Contoh lengkap yang dapat dijalankan di atas memberi Anda fondasi kuat yang dapat disesuaikan dengan alur kerja dokumen hukum apa pun atau sistem pelaporan internal.

Siap untuk langkah selanjutnya? Coba gabungkan pendekatan ini dengan API penggabungan PDF Aspose untuk memproses banyak file secara batch, atau jelajahi kelas `TextFragment` untuk watermark yang lebih kaya (berwarna, diputar, atau multi‑baris). Kemungkinannya tak terbatas, dan kode yang Anda miliki sekarang adalah dasar yang dapat diandalkan.

Jika Anda menemukan panduan ini membantu, silakan tinggalkan komentar, beri bintang pada repositori, atau bagikan variasi Anda sendiri. Selamat coding, dan semoga PDF Anda selalu bernomor dengan sempurna!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}