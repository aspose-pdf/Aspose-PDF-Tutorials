---
category: general
date: 2026-03-24
description: Tambahkan penomoran Bates pada PDF menggunakan Aspose.Pdf di C#. Pelajari
  cara menambahkan halaman PDF baru, menerapkan nomor Bates, dan memperbarui penomoran
  Bates secara efisien.
draft: false
keywords:
- add bates numbering pdf
- add new page pdf
- apply bates number
- create pdf aspose
- update bates numbering
language: id
og_description: Tambahkan penomoran Bates pada PDF dengan cepat. Panduan ini menunjukkan
  cara menambahkan halaman PDF baru, menerapkan nomor Bates, dan memperbarui penomoran
  Bates menggunakan Aspose.Pdf.
og_title: Menambahkan penomoran Bates pada PDF dengan Aspose – Panduan Lengkap
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Menambahkan Penomoran Bates pada PDF dengan Aspose – Panduan Lengkap
url: /id/net/programming-with-pdf-pages/add-bates-numbering-pdf-with-aspose-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Menambahkan penomoran Bates pada PDF dengan Aspose – Panduan Lengkap

Pernah membutuhkan untuk **add bates numbering pdf** file tetapi tidak yakin harus mulai dari mana? Anda bukan satu-satunya—tim hukum, auditor, dan siapa pun yang menangani kumpulan dokumen besar sering menghadapi hal ini. Kabar baik? Dengan Aspose.Pdf untuk .NET Anda dapat melakukannya hanya dengan beberapa baris kode, dan Anda bahkan akan belajar cara **add new page pdf** objek, **apply bates number**, dan **update bates numbering** nanti.

Dalam tutorial ini kami akan membahas skenario dunia nyata: Anda memiliki PDF sumber, Anda ingin menyisipkan stempel Bates pada halaman baru, dan Anda mungkin perlu menomori ulang seluruh dokumen nanti. Pada akhir tutorial Anda akan dapat membuat solusi **create pdf aspose** yang siap produksi, dan Anda akan memahami mengapa setiap langkah penting.

## Apa yang Akan Anda Capai

- Memuat PDF yang sudah ada dengan Aspose.Pdf.
- **Add new page pdf** untuk menampung stempel Bates.
- **Apply bates number** menggunakan `TextStamp`.
- (Opsional) **Update bates numbering** di semua halaman.
- Contoh C# lengkap yang dapat dijalankan dan dapat Anda masukkan ke proyek .NET apa pun.

### Prasyarat

- .NET 6.0 atau lebih baru (kode juga berfungsi pada .NET Framework 4.7+).
- Paket NuGet Aspose.Pdf untuk .NET (`Install-Package Aspose.Pdf`).
- File PDF sumber (`source.pdf`) yang ditempatkan di folder yang diketahui.

Tidak diperlukan konfigurasi rumit—hanya pustaka dan PDF untuk dicoba.

![Contoh penomoran bates pdf](https://example.com/placeholder.png "Diagram yang menunjukkan penomoran Bates ditambahkan ke halaman PDF")

## Langkah 1 – Memuat PDF Sumber (Dasar)

Sebelum Anda dapat **add bates numbering pdf**, Anda memerlukan objek dokumen untuk bekerja. Anggap `Document` sebagai kanvas; tanpa itu, tidak ada yang dapat ditempeli stempel.

```csharp
using Aspose.Pdf;

// Load the existing PDF – replace the path with your actual file location
using var pdfDocument = new Document(@"C:\MyPdfs\source.pdf");

// Verify the document was loaded (optional but handy for debugging)
Console.WriteLine($"Document loaded: {pdfDocument.Pages.Count} pages found.");
```

*Mengapa ini penting:* Memuat file memberi Anda akses ke koleksi halaman, metadata, dan pengaturan keamanan. Jika file rusak, Aspose akan melemparkan pengecualian yang informatif, menyelamatkan Anda dari kegagalan diam-diam nanti.

## Langkah 2 – **Add new page pdf** untuk Stempel Bates

Mengapa menempatkan stempel pada halaman baru? Banyak alur kerja hukum mengharuskan nomor Bates muncul pada halaman judul terpisah, menjaga konten asli tetap tidak tersentuh. Menambahkan halaman adalah satu baris kode dengan Aspose.

```csharp
// Create a fresh page at the end of the document
var newPage = pdfDocument.Pages.Add();

// Quick sanity check – print the new total page count
Console.WriteLine($"New page added. Total pages: {pdfDocument.Pages.Count}");
```

*Tip profesional:* Jika Anda membutuhkan stempel pada setiap halaman, Anda dapat melewatkan penambahan halaman baru dan melakukan loop melalui `pdfDocument.Pages`. Di sini kami sengaja **add new page pdf** untuk mengilustrasikan pola “halaman sampul” yang paling umum.

## Langkah 3 – **Apply bates number** dengan TextStamp

Inti dari operasi ini adalah `TextStamp`. Ia memungkinkan Anda menempatkan teks secara tepat, mengatur margin, dan menata tampilan.

```csharp
// Create a TextStamp that holds the Bates number
var batesStamp = new TextStamp("Bates: 001")
{
    // Align the stamp to the bottom‑right corner
    HorizontalAlignment = HorizontalAlignment.Right,
    VerticalAlignment   = VerticalAlignment.Bottom,
    
    // Margin values are in points (1 point = 1/72 inch)
    Margin = new Margin(0, 0, 20, 20) // left, bottom, right, top
};

// Attach the stamp to the newly created page
newPage.AddStamp(batesStamp);
```

*Mengapa kami memilih pengaturan ini:* Penempatan kanan-bawah mencerminkan cara kebanyakan pengadilan mengharapkan nomor Bates. Margin 20 poin menjaga teks jauh dari tepi halaman, menghindari pemotongan printer. Anda dapat mengganti `"Bates: 001"` dengan variabel jika membutuhkan nomor berurutan.

## Langkah 4 – Simpan PDF yang Diperbarui

Menyimpan sangat sederhana, tetapi Anda mungkin ingin mempertahankan file asli. Mari menulis ke lokasi baru.

```csharp
string outputPath = @"C:\MyPdfs\output_with_bates.pdf";
pdfDocument.Save(outputPath);
Console.WriteLine($"PDF saved with Bates stamp at: {outputPath}");
```

Pada titik ini Anda telah berhasil **add bates numbering pdf** ke sebuah dokumen, dan Anda juga **add new page pdf** untuk menampungnya. Buka file di penampil apa pun—Anda harus melihat stempel terpasang rapi di sudut kanan-bawah halaman terakhir.

## Langkah 5 – (Opsional) **Update bates numbering** di Semua Halaman

Bagaimana jika nanti Anda memutuskan menambahkan lebih banyak stempel pada halaman lain? Aspose menyediakan metode pembantu yang secara otomatis meningkatkan nomor pada setiap halaman, menyelamatkan Anda dari manipulasi string manual.

```csharp
// This will renumber all pages using the same stamp format
pdfDocument.Pages.UpdateBatesNumbering();
pdfDocument.Save(@"C:\MyPdfs\output_renumbered.pdf");
Console.WriteLine("All pages have been renumbered.");
```

*Kapan menggunakan ini:* Ideal untuk batch besar di mana setiap halaman memerlukan identifier unik. Metode ini menghormati properti `TextStamp` asli, sehingga penyelarasan dan margin Anda tetap konsisten.

## Contoh Lengkap yang Berfungsi – Dari Awal hingga Selesai

Berikut adalah program lengkap yang dapat Anda salin‑tempel ke aplikasi konsol. Program ini mencakup semua langkah, penanganan error, dan komentar.

```csharp
using System;
using Aspose.Pdf;

class Program
{
    static void Main()
    {
        // Path to the source PDF – adjust as needed
        const string sourcePath = @"C:\MyPdfs\source.pdf";
        const string resultPath = @"C:\MyPdfs\output_with_bates.pdf";

        try
        {
            // 1️⃣ Load the existing PDF
            using var pdfDocument = new Document(sourcePath);
            Console.WriteLine($"Loaded PDF with {pdfDocument.Pages.Count} pages.");

            // 2️⃣ Add a new blank page for the Bates stamp
            var newPage = pdfDocument.Pages.Add();
            Console.WriteLine($"Added new page. Total pages now: {pdfDocument.Pages.Count}");

            // 3️⃣ Create and configure the Bates TextStamp
            var batesStamp = new TextStamp("Bates: 001")
            {
                HorizontalAlignment = HorizontalAlignment.Right,
                VerticalAlignment   = VerticalAlignment.Bottom,
                Margin = new Margin(0, 0, 20, 20) // left, bottom, right, top
            };

            // 4️⃣ Place the stamp on the newly added page
            newPage.AddStamp(batesStamp);
            Console.WriteLine("Bates stamp applied to the new page.");

            // 5️⃣ Save the modified PDF
            pdfDocument.Save(resultPath);
            Console.WriteLine($"PDF saved successfully at {resultPath}");

            // Optional: Renumber all pages if you add more stamps later
            // pdfDocument.Pages.UpdateBatesNumbering();
            // pdfDocument.Save(@"C:\MyPdfs\output_renumbered.pdf");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error: {ex.Message}");
        }
    }
}
```

**Hasil yang diharapkan:** Membuka `output_with_bates.pdf` menampilkan konten asli tidak berubah, halaman terakhir baru, dan teks “Bates: 001” terpasang rapi di sudut kanan-bawah. Jika Anda menghapus komentar pada baris `UpdateBatesNumbering`, setiap halaman akan mendapatkan nomor inkremental masing‑masing.

## Pertanyaan Umum & Kasus Tepi

- **Bisakah saya mengubah font atau warna?**  
  Tentu saja. `TextStamp` mewarisi dari `Stamp`, sehingga Anda dapat mengatur `Font`, `FontSize`, `Color`, dll. Contoh: `batesStamp.Font = FontRepository.FindFont("Arial"); batesStamp.FontSize = 12; batesStamp.TextColor = Color.Red;`.

- **Bagaimana jika PDF saya dilindungi kata sandi?**  
  Muat dengan kata sandi: `new Document(sourcePath, new LoadOptions { Password = "mySecret" })`.

- **Apakah saya perlu membuang (`dispose`) `Document`?**  
  Menggunakan pernyataan `using` (seperti yang ditunjukkan) secara otomatis membuangnya, melepaskan handle file.

- **Apakah margin diukur dalam poin atau piksel?**  
  Poin. Satu poin sama dengan 1/72 inci, yang merupakan satuan standar PDF.

- **Bisakah saya menempatkan stempel pada halaman pertama alih-alih halaman baru?**  
  Ya—cukup ganti `newPage` dengan `pdfDocument.Pages[1]` (halaman dimulai dari 1).

## Kesimpulan

Anda kini memiliki resep lengkap, ujung‑ke‑ujung untuk **add bates numbering pdf** menggunakan Aspose.Pdf, lengkap dengan cara **add new page pdf**, **apply bates number**, dan **update bates numbering** ketika dokumen berkembang. Kode siap disisipkan ke proyek C# apa pun, dan penjelasannya akan membantu Anda menyesuaikannya dengan tata letak khusus, font berbeda, atau pemrosesan batch.

### Selanjutnya?

- Selami lebih dalam **create pdf aspose** dengan menambahkan gambar, tabel, atau tanda tangan digital.  
- Otomatiskan pemrosesan batch: loop melalui folder PDF dan beri stempel pada masing‑masing.  
- Jelajahi fitur kepatuhan PDF/A Aspose jika Anda membutuhkan dokumen yang dapat diarsipkan.

Cobalah, sesuaikan penyelarasan, bereksperimen dengan teks stempel yang berbeda, dan biarkan pustaka melakukan pekerjaan berat. Jika Anda menemui kendala, forum komunitas Aspose adalah tempat yang tepat untuk bertanya—selamat coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}