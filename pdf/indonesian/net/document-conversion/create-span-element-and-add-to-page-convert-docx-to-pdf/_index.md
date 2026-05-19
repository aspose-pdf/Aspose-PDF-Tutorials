---
category: general
date: 2026-03-27
description: Buat elemen span dalam C# dan pelajari cara menambahkan span ke halaman
  saat mengonversi DOCX ke PDF serta menyimpannya sebagai PDF. Panduan langkah demi
  langkah untuk pengembang.
draft: false
keywords:
- create span element
- how to add span
- convert docx to pdf
- add element to page
- save as pdf
language: id
og_description: Buat elemen span dalam C# dan pelajari cara menambahkan span ke halaman
  saat mengonversi DOCX ke PDF, kemudian menyimpannya sebagai PDF. Contoh kode lengkap
  disertakan.
og_title: Buat elemen span dan tambahkan ke halaman – Konversi DOCX ke PDF
tags:
- C#
- DocumentProcessing
- PDFConversion
title: Buat elemen span dan tambahkan ke halaman – Konversi DOCX ke PDF
url: /id/net/document-conversion/create-span-element-and-add-to-page-convert-docx-to-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat elemen span dan tambahkan ke halaman – Konversi DOCX ke PDF

Membuat **elemen span** dalam file DOCX adalah tugas umum ketika Anda membutuhkan kontrol tata letak yang tepat. Dalam tutorial ini kami akan menunjukkan **cara menambahkan span** ke sebuah halaman, **mengonversi DOCX ke PDF**, dan **menyimpan sebagai PDF**—semua dalam beberapa langkah rapi.  

Jika Anda pernah menatap dokumen Word dan berpikir, “Andai saja saya bisa menaruh kotak teks kecil pada koordinat yang tepat,” Anda berada di tempat yang tepat. Kami akan memandu seluruh alur kerja, mulai dari memuat file sumber hingga menghasilkan output PDF yang rapi.

## Apa yang akan Anda capai

Dengan menyelesaikan panduan ini Anda akan dapat:

* Muat file `.docx` menggunakan kelas `Document` dari perpustakaan dokumen.  
* **Buat elemen span** dengan API `TaggedContent`.  
* Posisi span tersebut pada koordinat X/Y yang tepat pada halaman yang dipilih.  
* **Tambahkan elemen ke halaman** secara andal, bahkan ketika halaman bukan yang pertama.  
* **Konversi DOCX ke PDF** dan **simpan sebagai PDF** dengan satu panggilan `Save`.

Tidak ada alat eksternal, tidak ada pengaturan misterius—hanya kode C# biasa yang dapat Anda salin‑tempel ke proyek Anda.

## Prasyarat

* .NET 6+ (atau runtime .NET terbaru yang didukung perpustakaan Anda).  
* SDK pemrosesan dokumen yang menyediakan `Document`, `TaggedContent`, `Position`, dll.  
* Pemahaman dasar tentang sintaks C#—jika Anda dapat menulis `Console.WriteLine`, Anda sudah siap.

> **Tips pro:** Jaga versi SDK Anda tetap terbaru; rilis terbaru (v3.2 per Maret 2026) mencakup perbaikan kinerja untuk operasi tingkat halaman.

---

![Diagram yang menggambarkan cara membuat elemen span dan menempatkannya pada halaman PDF](https://example.com/images/create-span-element.png "Diagram penempatan elemen span")

## Buat elemen span – Posisi dan Tambahkan ke Halaman

Berikut adalah kode lengkap yang dapat dijalankan yang melakukan semua hal mulai dari memuat DOCX sumber hingga menulis PDF akhir. Silakan masukkan ke aplikasi console, sesuaikan jalur, dan jalankan.

```csharp
using DocumentProcessing;   // Replace with the actual namespace of your SDK
using DocumentProcessing.Models;

class Program
{
    static void Main()
    {
        // Step 1: Load the DOCX you want to modify
        // -------------------------------------------------
        // The constructor takes a file path; make sure the file exists.
        Document doc = new Document(@"C:\Docs\input.docx");

        // Step 2: Create a new span element using the TaggedContent API
        // -------------------------------------------------
        // A span is a lightweight container for inline content.
        var span = doc.TaggedContent.CreateSpanElement();
        // Optional: add some text inside the span
        span.Text = "Hello, world!";

        // Step 3: Position the span at the desired coordinates (X = 50, Y = 750)
        // -------------------------------------------------
        // Position uses points (1/72 inch). Adjust as needed.
        span.Position = new Position(50, 750);

        // Step 4: Add the span to the target page (page index 1 = second page)
        // -------------------------------------------------
        // Pages are zero‑based; index 1 means the second page in the document.
        doc.Pages[1].Add(span);

        // Step 5: Convert the modified DOCX to PDF and save the result
        // -------------------------------------------------
        // The Save method automatically detects the output format from the extension.
        doc.Save(@"C:\Docs\output.pdf");

        // Confirmation output
        Console.WriteLine("Span added, document converted, and PDF saved successfully.");
    }
}
```

### Penjelasan langkah‑demi‑langkah

#### Langkah 1 – Muat dokumen DOCX  
Kami menginstansiasi objek `Document` yang menunjuk ke `input.docx`. Objek ini mewakili seluruh file Word dalam memori, memberi kami akses ke halaman, konten, dan metadata.  

#### Langkah 2 – Buat elemen span  
Pemanggilan `TaggedContent.CreateSpanElement()` mengembalikan kontainer inline ringan. Anggaplah sebagai kotak kecil tak terlihat yang dapat menampung teks, gambar, atau elemen inline lainnya. Menambahkan teks (`span.Text`) bersifat opsional tetapi berguna untuk debugging.

#### Langkah 3 – Posisi span  
`new Position(50, 750)` menetapkan sudut kiri‑atas span 50 pts dari margin kiri dan 750 pts dari atas halaman. Nilai‑nilai ini bersifat absolut, sehingga Anda dapat menempatkan span di mana saja—sempurna untuk tata letak yang presisi.

#### Langkah 4 – Tambahkan span ke halaman target  
`doc.Pages[1].Add(span)` menyuntikkan span ke halaman kedua. API menggunakan indeks berbasis nol, jadi halaman 0 adalah halaman pertama. Jika Anda perlu menambahkannya ke halaman pertama, gunakan saja `doc.Pages[0]`.

#### Langkah 5 – Konversi DOCX ke PDF dan simpan sebagai PDF  
Pemanggilan `doc.Save("output.pdf")` melakukan dua hal: menulis dokumen yang telah dimodifikasi ke disk **dan** mengonversi kontennya ke PDF karena ekstensi `.pdf`. Tidak diperlukan langkah konversi tambahan—ini cara termudah untuk **menyimpan sebagai PDF**.

---

## Cara menambahkan span pada halaman yang berbeda (lanjutan)

Kadang‑kadang Anda tidak mengetahui indeks halaman sebelumnya. Anda dapat menemukan halaman berdasarkan nomor (yang mudah dipahami) atau dengan mencari kata kunci tertentu.

```csharp
// Find the page that contains the word "Summary"
int targetIndex = doc.Pages
    .Select((p, i) => new { Page = p, Index = i })
    .FirstOrDefault(x => x.Page.Text.Contains("Summary"))?.Index ?? 0;

// Fallback to first page if not found
targetIndex = Math.Max(targetIndex, 0);

// Add the span to the discovered page
doc.Pages[targetIndex].Add(span);
```

**Mengapa ini penting:** Pada laporan yang jumlah halamannya bervariasi, menuliskan secara keras `Pages[1]` dapat merusak tata letak. Potongan kode ini menunjukkan pola yang kuat untuk **cara menambahkan span** secara dinamis.

---

## Kesalahan umum dan cara menghindarinya

| Masalah | Apa yang terjadi | Perbaikan |
|-------|--------------|-----|
| **Span tidak terlihat** | Koordinat berada di luar halaman atau span memiliki lebar/tinggi nol. | Periksa kembali nilai `Position`; gunakan penggaris di penampil PDF Anda. |
| **Indeks halaman salah** | Anda menambahkan ke halaman 0 tetapi mengharapkannya di halaman 2. | Ingat API menggunakan indeks nol; tambahkan 1 ke nomor halaman manusia. |
| **Menyimpan menimpa sumber** | `doc.Save("input.docx")` menggantikan file asli. | Selalu simpan ke jalur baru (`output.pdf`) saat mengonversi. |
| **Referensi SDK hilang** | Kesalahan kompilasi pada kelas `Document`. | Instal paket NuGet: `dotnet add package DocumentProcessing.SDK`. |

---

## Memverifikasi hasil

Setelah menjalankan program, buka `output.pdf` di penampil PDF apa pun. Anda harus melihat teks “Hello, world!” tepat pada posisi (50, 750) di halaman kedua. Jika teks muncul di tempat lain, sesuaikan nilai `Position` dan jalankan kembali.  

Untuk pengujian otomatis, Anda dapat menggunakan parser PDF (misalnya iTextSharp) untuk memverifikasi koordinat teks secara programatik.

```csharp
// Example using iTextSharp to verify position (pseudo‑code)
var pdfReader = new PdfReader(@"C:\Docs\output.pdf");
var page = pdfReader.GetPageContent(2);
Debug.Assert(page.Contains("Hello, world!"));
```

---

## Langkah selanjutnya

* **Gaya span** – jelajahi properti `span.Font`, `span.Color`, dan properti styling lainnya.  
* **Tambahkan gambar** – gunakan `CreateImageElement()` alih‑alih span untuk grafik.  
* **Pemrosesan batch** – iterasi pada folder berisi file DOCX

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}