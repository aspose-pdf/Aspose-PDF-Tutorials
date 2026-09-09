---
category: general
date: 2026-02-12
description: Tambahkan nomor Bates ke file PDF dengan cepat. Pelajari cara menambahkan
  bidang teks PDF, menambahkan bidang formulir PDF, dan menambahkan nomor halaman
  PDF menggunakan Aspose.PDF.
draft: false
keywords:
- add bates numbers
- add text field pdf
- add form field pdf
- add page numbers pdf
- how to add bates
language: id
og_description: Tambahkan nomor Bates ke dokumen PDF dalam C#. Panduan ini menunjukkan
  cara menambahkan bidang teks PDF, menambahkan bidang formulir PDF, dan menambahkan
  nomor halaman PDF dengan Aspose.PDF.
og_title: Tambahkan Nomor Bates ke PDF – Tutorial C# Lengkap
tags:
- PDF
- C#
- Aspose.PDF
title: Tambahkan Nomor Bates ke PDF – Panduan C# Langkah demi Langkah
url: /id/net/programming-with-forms/add-bates-numbers-to-pdfs-step-by-step-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Menambahkan Bates Numbers ke PDF – Panduan Lengkap C#

Pernahkah Anda perlu **add bates numbers** ke tumpukan PDF legal tetapi tidak yakin harus mulai dari mana? Anda tidak sendirian. Di banyak firma hukum dan proyek e‑discovery, menstempel setiap halaman dengan identifier unik adalah tugas harian, dan melakukannya secara manual adalah mimpi buruk.  

Berita baiknya? Dengan beberapa baris C# dan Aspose.PDF Anda dapat mengotomatiskan semuanya. Dalam tutorial ini kami akan menjelaskan **how to add bates** numbers, menambahkan field teks pada setiap halaman, dan menyimpan PDF yang bersih serta dapat dicari—tanpa susah payah.

> **What you’ll get:** contoh kode yang dapat dijalankan sepenuhnya, penjelasan mengapa setiap baris penting, tips untuk kasus tepi, dan daftar periksa cepat untuk memverifikasi output Anda.  

Kami juga akan membahas tugas terkait seperti **add text field pdf**, **add form field pdf**, dan **add page numbers pdf**, sehingga Anda memiliki kotak peralatan siap untuk tantangan otomatisasi dokumen apa pun.

---

## Prasyarat

- .NET 6.0 atau lebih baru (kode ini juga bekerja dengan .NET Framework 4.6+).  
- Visual Studio 2022 (atau IDE apa pun yang Anda sukai).  
- Lisensi Aspose.PDF untuk .NET yang valid (versi percobaan gratis cukup untuk pengujian).  
- PDF sumber bernama `source.pdf` yang ditempatkan di folder yang dapat Anda referensikan.  

Jika ada yang belum familiar, cukup jeda dan instal komponen yang belum ada sebelum melanjutkan. Langkah‑langkah di bawah mengasumsikan Anda sudah menambahkan paket NuGet Aspose.PDF:

```bash
dotnet add package Aspose.Pdf
```

---

## Cara menambahkan bates numbers ke PDF dengan Aspose.PDF

Berikut adalah program lengkap yang siap disalin‑tempel. Program ini memuat PDF, membuat **text box field** pada setiap halaman, menulis Bates number yang diformat, dan akhirnya menulis file yang telah dimodifikasi.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Forms;

class Program
{
    static void Main()
    {
        // 👉 Step 1: Load the source PDF document
        using (var pdfDocument = new Document(@"YOUR_DIRECTORY\source.pdf"))
        {
            // 👉 Step 2: Add a Bates number text field to each page
            for (int pageNumber = 1; pageNumber <= pdfDocument.Pages.Count; pageNumber++)
            {
                // Define the rectangle where the field will appear (10,10) = lower‑left corner
                var fieldRect = new Rectangle(10, 10, 150, 30);

                // Create the TextBoxField – this is the “add text field pdf” part
                var batesField = new TextBoxField(pdfDocument.Pages[pageNumber], fieldRect)
                {
                    // Format the number: BATES-00001, BATES-00002, …
                    Value = $"BATES-{pageNumber:D5}"
                };

                // Register the field with the form collection – “add form field pdf”
                pdfDocument.Form.Add(batesField, $"Bates_{pageNumber}", pageNumber);
            }

            // 👉 Step 3: Save the modified PDF with Bates numbers
            pdfDocument.Save(@"YOUR_DIRECTORY\bates.pdf");
        }

        Console.WriteLine("✅ Bates numbers added successfully!");
    }
}
```

### Mengapa ini berhasil

- **`Document`** adalah titik masuk; ia mewakili seluruh file PDF.  
- **`Rectangle`** menentukan di mana field berada pada halaman. Angka‑angka tersebut dalam satuan point (1 pt ≈ 1/72 in). Sesuaikan koordinat jika Anda memerlukan nomor di sudut yang berbeda.  
- **`TextBoxField`** adalah *form field* yang dapat menampung string apa pun. Dengan menetapkan `Value` kita secara efektif **add page numbers pdf** dengan prefiks khusus.  
- **`pdfDocument.Form.Add`** mendaftarkan field ke AcroForm PDF, sehingga terlihat di penampil seperti Adobe Acrobat.  

Jika Anda perlu mengubah tampilan (font, warna, ukuran) Anda dapat menyesuaikan properti `TextBoxField`—lihat dokumentasi Aspose untuk `DefaultAppearance` dan `Border`.

---

## Menambahkan field teks ke setiap halaman PDF (langkah “add text field pdf”)

Kadang‑kadang Anda hanya menginginkan label yang terlihat, bukan form field interaktif. Dalam kasus itu Anda dapat mengganti `TextBoxField` dengan `TextFragment` dan menambahkannya langsung ke koleksi `Paragraphs` halaman. Berikut alternatif singkatnya:

```csharp
var fragment = new TextFragment($"BATES-{pageNumber:D5}")
{
    // Position the text using a TextState (font, size, color)
    TextState = new TextState
    {
        Font = FontRepository.FindFont("Arial"),
        FontSize = 12,
        ForegroundColor = Color.Black
    }
};

// Set the fragment’s rectangle (same coordinates as before)
fragment.Position = new Position(10, 10);
pdfDocument.Pages[pageNumber].Paragraphs.Add(fragment);
```

Pendekatan **add text field pdf** berguna ketika dokumen akhir akan bersifat read‑only, sementara metode **add form field pdf** menjaga nomor tetap dapat diedit nanti.

---

## Menyimpan PDF dengan Bates numbers (momen “add page numbers pdf”)

Setelah loop selesai, pemanggilan `pdfDocument.Save` menulis semuanya ke disk. Jika Anda perlu mempertahankan file asli, cukup ubah jalur output atau gunakan overload `pdfDocument.Save` untuk mengalirkan hasil langsung ke respons dalam API web.

```csharp
// Example: stream to HTTP response (ASP.NET Core)
Response.ContentType = "application/pdf";
pdfDocument.Save(Response.Body);
```

Itulah bagian yang rapi—tanpa file sementara, tanpa pustaka tambahan, hanya Aspose yang menangani beban kerja berat.

---

## Hasil yang Diharapkan & Verifikasi Cepat

Buka `bates.pdf` di penampil PDF apa pun. Anda harus melihat kotak kecil di sudut kiri‑bawah setiap halaman yang berisi:

```
BATES-00001
BATES-00002
…
```

Jika Anda memeriksa properti dokumen, Anda akan melihat AcroForm yang berisi field bernama `Bates_1`, `Bates_2`, dll. Itu mengonfirmasi langkah **add form field pdf** berhasil.

---

## Kesalahan Umum & Tips Pro

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| Numbers appear off‑center | Rectangle coordinates are relative to the page’s lower‑left corner. | Flip the Y‑value (`pageHeight - marginTop`) or use `page.PageInfo.Height` to calculate a top‑margin placement. |
| Fields are invisible in Adobe Reader | The default border is set to “No”. | Set `batesField.Border = new Border { Width = 0.5f, Color = Color.Black };` |
| Large PDFs cause memory pressure | `using` disposes the document only after the loop finishes. | Process pages in chunks or use `pdfDocument.Save` with `SaveOptions` that enable streaming. |
| License not applied | Aspose prints a watermark on the first page. | Register your license early: `License lic = new License(); lic.SetLicense("Aspose.Pdf.lic");` |

---

## Memperluas Solusi

- **Custom prefixes:** Ganti `"BATES-"` dengan string apa pun (`"DOC-"`, `"CASE-"`, …).  
- **Zero‑padding length:** Ubah `{pageNumber:D5}` menjadi `{pageNumber:D3}` untuk tiga digit.  
- **Dynamic placement:** Gunakan `pdfDocument.Pages[pageNumber].PageInfo.Width` untuk menempatkan field di sisi kanan.  
- **Conditional numbering:** Lewati halaman kosong dengan memeriksa `pdfDocument.Pages[pageNumber].IsBlank`.

Semua variasi ini tetap mempertahankan pola inti **add bates numbers**, **add text field pdf**, dan **add form field pdf**.

---

## Contoh Lengkap yang Berfungsi (Semua dalam Satu)

Berikut adalah program akhir yang siap dijalankan dan menggabungkan semua tips di atas. Salin ke aplikasi konsol baru dan tekan F5.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Forms;
using Aspose.Pdf.Text;
using Aspose.Pdf.Drawing;

class AddBatesNumbers
{
    static void Main()
    {
        // Register your license here (optional for trial)
        // var license = new License();
        // license.SetLicense("Aspose.Pdf.lic");

        string inputPath = @"YOUR_DIRECTORY\source.pdf";
        string outputPath = @"YOUR_DIRECTORY\bates.pdf";

        using (var pdfDocument = new Document(inputPath))
        {
            int totalPages = pdfDocument.Pages.Count;

            for (int i = 1; i <= totalPages; i++)
            {
                // Position the field 10 pts from left and 10 pts from bottom
                var rect = new Rectangle(10, 10, 150, 30);

                var batesField = new TextBoxField(pdfDocument.Pages[i], rect)
                {
                    Value = $"BATES-{i:D5}"
                };

                // Optional: make the field look nicer
                batesField.Border = new Border
                {
                    Width = 0.5f,
                    Color = Color.Gray
                };
                batesField.DefaultAppearance = new DefaultAppearance
                {
                    Font = FontRepository.FindFont("Arial"),
                    FontSize = 10,
                    ForegroundColor = Color.DarkBlue
                };

                pdfDocument.Form.Add(batesField, $"Bates_{i}", i);
            }

            pdfDocument.Save(outputPath);
        }

        Console.WriteLine($"✅ Finished! Bates numbers saved to: {outputPath}");
    }
}
```

Jalankan, buka hasilnya, dan Anda akan melihat identifier berpenampilan profesional pada setiap halaman—tepat seperti yang diharapkan oleh spesialis dukungan litigasi.

---

## Kesimpulan

Kami baru saja mendemonstrasikan **how to add bates numbers** ke PDF apa pun menggunakan C# dan Aspose.PDF. Dengan membuat **text box field** pada setiap halaman kami sekaligus **add text field pdf**, **add form field pdf**, dan **add page numbers pdf** dalam satu proses. Pendekatan ini cepat, skalabel, dan mudah disesuaikan untuk prefiks khusus, tata letak berbeda, atau logika bersyarat.

Siap untuk tantangan berikutnya? Coba sematkan QR code yang menautkan ke berkas kasus asli, atau hasilkan halaman indeks terpisah yang mencantumkan semua Bates numbers beserta judul halaman yang bersangkutan. API yang sama memungkinkan Anda menggabungkan PDF, mengekstrak halaman, bahkan menyensor data sensitif—jadi batasnya hanya imajinasi Anda.

Jika Anda mengalami kendala, tinggalkan komentar di bawah atau periksa dokumentasi resmi Aspose untuk penjelasan lebih mendalam. Selamat coding, semoga PDF Anda selalu ternomori dengan sempurna!  

---  

![add bates numbers screenshot](https://example.com/images/add-bates-numbers.png "add bates numbers example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}