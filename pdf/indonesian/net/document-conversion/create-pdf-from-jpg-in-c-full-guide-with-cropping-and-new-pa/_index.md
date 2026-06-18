---
category: general
date: 2026-04-06
description: Buat PDF dari JPG dengan cepat dan pelajari cara memotong gambar dalam
  PDF, menambahkan halaman PDF baru, serta mengonversi JPG ke PDF dengan pemotongan
  menggunakan C#.
draft: false
keywords:
- create pdf from jpg
- crop image in pdf
- how to add new pdf page
- convert jpg to pdf with crop
- insert image into pdf c#
language: id
og_description: Buat PDF dari JPG dan pangkas gambar dalam PDF dengan C#. Pelajari
  cara menambahkan halaman PDF baru dan mengonversi JPG ke PDF dengan pemotongan.
og_title: Buat PDF dari JPG di C# – Panduan Langkah demi Langkah
tags:
- Aspose.Pdf
- C#
- PDF generation
title: Buat PDF dari JPG di C# – Panduan Lengkap dengan Pemotongan dan Halaman Baru
url: /id/net/document-conversion/create-pdf-from-jpg-in-c-full-guide-with-cropping-and-new-pa/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Membuat PDF dari JPG di C# – Panduan Lengkap dengan Pemotongan dan Halaman Baru

Pernah perlu **membuat PDF dari JPG** tetapi tidak yakin bagaimana cara menyimpan hanya bagian yang Anda inginkan? Anda tidak sendirian. Dalam banyak aplikasi—seperti faktur, kwitansi, atau buku foto—pengembang harus mengubah gambar menjadi PDF sambil membuang tepi yang tidak diinginkan.  

Dalam tutorial ini kami akan membahas solusi lengkap yang siap dijalankan untuk **membuat PDF dari JPG**, menunjukkan cara **memotong gambar dalam PDF**, dan mendemonstrasikan **cara menambahkan halaman PDF baru** ketika Anda memerlukan lebih dari satu gambar. Pada akhir tutorial Anda juga akan tahu cara **mengonversi JPG ke PDF dengan pemotongan** dan **menyisipkan gambar ke PDF C#** menggunakan pustaka Aspose.Pdf.

## Apa yang Akan Anda Pelajari

- Menyiapkan Aspose.Pdf dalam proyek .NET (tanpa konfigurasi berat).  
- Memuat JPEG, menentukan area yang ingin dipertahankan, dan memotongnya sambil menyisipkan ke halaman PDF.  
- Menambahkan halaman tambahan ke dokumen yang sama, memungkinkan Anda membangun PDF multi‑halaman dari banyak gambar.  
- Menyimpan file akhir dan memverifikasi output.  

**Prasyarat:** .NET 6+ (atau .NET Framework 4.6+), Visual Studio 2022 atau editor pilihan Anda, dan referensi NuGet ke `Aspose.Pdf`. Tidak diperlukan layanan eksternal lainnya.

![Create PDF from JPG example](image.jpg){: .align-center alt="Contoh membuat PDF dari JPG menampilkan gambar yang dipotong ditempatkan pada halaman PDF"}

---

## Langkah 1: Instal Aspose.Pdf dan Siapkan Proyek Anda

Hal pertama yang harus dilakukan—tambahkan paket Aspose.Pdf. Buka terminal di folder solusi Anda dan jalankan:

```bash
dotnet add package Aspose.Pdf
```

Baris tunggal itu mengunduh semua yang Anda perlukan: kelas `Document`, `Rectangle`, dan `Page` yang akan kita gunakan nanti. Menurut pengalaman saya, cara melalui NuGet adalah yang paling bersih untuk tetap up‑to‑date tanpa harus mengutak‑atik DLL.

> **Pro tip:** Jika Anda menargetkan .NET Framework, gunakan paket `Aspose.Pdf.NET` sebagai gantinya; permukaan API-nya identik.

---

## Langkah 2: Muat JPEG dan Tentukan Ukuran Halaman

Kita memerlukan kanvas yang cocok dengan dimensi yang diinginkan untuk halaman PDF akhir. Kode di bawah ini membuat `Document` baru dan membuka gambar sumber sebagai stream.

```csharp
using Aspose.Pdf;
using System.IO;

// Create a new PDF document – this will hold our pages.
using var pdfDocument = new Document();

// Open the JPEG you want to convert.
using var imageStream = File.OpenRead(@"C:\Images\photo.jpg");

// Define the full‑size rectangle (the page) – 600 × 800 points works well for most photos.
var pageBounds = new Rectangle(0, 0, 600, 800);
```

Mengapa menggunakan rectangle? Di Aspose.Pdf, `Rectangle` mewakili baik dimensi halaman maupun wilayah gambar yang ingin Anda tampilkan. Dengan memisahkan *halaman* dari *area pemotongan* Anda mendapatkan kontrol yang lebih halus atas apa yang muncul di PDF.

---

## Langkah 3: Pilih Area Pemotongan (Kuarter Kiri‑Atas)

Misalkan Anda hanya membutuhkan kuarter kiri‑atas foto. Kami menghitung wilayah tersebut relatif terhadap ukuran halaman:

```csharp
// Crop the upper‑left quarter of the image.
var cropArea = new Rectangle(
    pageBounds.LLX,                                 // left X (0)
    pageBounds.LLY + pageBounds.Height / 2,         // bottom Y (halfway up)
    pageBounds.LLX + pageBounds.Width / 2,          // right X (halfway across)
    pageBounds.URY);                                // top Y (full height)
```

Konstruktor `Rectangle` menerima nilai **X/Y kiri‑bawah** dan **X/Y kanan‑atas**. Dengan menambahkan setengah tinggi ke `LLY` kami menggeser bagian bawah pemotongan ke atas, sehingga secara efektif membuang setengah bagian bawah gambar. Sesuaikan perhitungan ini jika Anda memerlukan bagian yang berbeda.

> **Mengapa memotong sebelum menambahkan?**  
> Memotong di sisi PDF menghindari pembuatan bitmap sementara di disk, menghemat I/O dan memori. Aspose menangani perhitungannya untuk Anda, dan hasilnya adalah PDF yang bersih serta ramah vektor.

---

## Langkah 4: Tambahkan Halaman Baru dan Sisipkan Gambar yang Dipotong

Sekarang kami menempatkan gambar pada halaman PDF. Inilah saat **cara menambahkan halaman pdf baru** menjadi penting.

```csharp
// Add a new page to the document.
var page = pdfDocument.Pages.Add();

// Insert the image using both the page bounds and the crop rectangle.
page.AddImage(imageStream, pageBounds, cropArea);
```

`AddImage` menerima tiga argumen:

1. **Stream** – JPEG sumber.  
2. **Page rectangle** – mendefinisikan ukuran halaman (yaitu `pageBounds` kami).  
3. **Crop rectangle** – memberi tahu Aspose bagian gambar mana yang harus dirender.

Jika Anda memerlukan lebih banyak halaman, cukup ulangi pola `Add` + `AddImage` dengan `imageStream` baru setiap kali. Ini memenuhi kebutuhan **cara menambahkan halaman pdf baru** sambil menjaga kode tetap rapi.

---

## Langkah 5: Simpan PDF dan Verifikasi Hasilnya

Langkah akhir hanya satu baris, tetapi jangan remehkan—menyimpan ke jalur yang tepat memastikan file dapat dibuka oleh semua penampil PDF.

```csharp
// Save the PDF to disk.
pdfDocument.Save(@"C:\Output\cropped_image.pdf");

// Optional: open the file automatically (Windows only).
System.Diagnostics.Process.Start(@"C:\Output\cropped_image.pdf");
```

Saat Anda membuka `cropped_image.pdf`, seharusnya terlihat satu halaman yang hanya berisi kuarter kiri‑atas JPEG asli, terpusat sempurna dalam halaman 600 × 800.

---

## Contoh Kerja Lengkap (Semua Langkah Digabung)

Berikut program lengkap yang dapat Anda salin‑tempel ke aplikasi console. Program ini dapat dikompilasi apa adanya, dengan asumsi Anda telah menginstal Aspose.Pdf dan menempatkan JPEG pada lokasi yang ditentukan.

```csharp
using Aspose.Pdf;
using System.IO;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new PDF document.
        using var pdfDocument = new Document();

        // 2️⃣ Open the source JPEG.
        using var imageStream = File.OpenRead(@"C:\Images\photo.jpg");

        // 3️⃣ Define the page size (600 × 800 points).
        var pageBounds = new Rectangle(0, 0, 600, 800);

        // 4️⃣ Calculate the crop area – upper‑left quarter.
        var cropArea = new Rectangle(
            pageBounds.LLX,
            pageBounds.LLY + pageBounds.Height / 2,
            pageBounds.LLX + pageBounds.Width / 2,
            pageBounds.URY);

        // 5️⃣ Add a new page and insert the cropped image.
        var page = pdfDocument.Pages.Add();
        page.AddImage(imageStream, pageBounds, cropArea);

        // 6️⃣ Save the resulting PDF.
        pdfDocument.Save(@"C:\Output\cropped_image.pdf");

        // 7️⃣ (Optional) Open the PDF automatically.
        System.Diagnostics.Process.Start(@"C:\Output\cropped_image.pdf");
    }
}
```

### Output yang Diharapkan

- **File:** `cropped_image.pdf` (≈ 30 KB).  
- **Konten:** Satu halaman, 600 × 800 poin, menampilkan kuarter kiri‑atas `photo.jpg`.  
- **Perilaku:** Tanpa distorsi; gambar mempertahankan resolusi aslinya dalam batas pemotongan.

---

## Pertanyaan yang Sering Diajukan & Kasus Khusus

### Bagaimana jika saya ingin menyimpan seluruh gambar, bukan hanya kuarter?

Cukup setel `cropArea` sama dengan `pageBounds`:

```csharp
var cropArea = pageBounds; // No cropping – full image.
```

### Bisakah saya menggunakan ukuran halaman lain (misalnya A4)?

Tentu saja. Ganti nilai `pageBounds` dengan dimensi halaman A4 dalam poin (595 × 842):

```csharp
var pageBounds = new Rectangle(0, 0, 595, 842);
```

Rectangle pemotongan dapat tetap sama atau dihitung ulang agar cocok dengan rasio aspek baru.

### Bagaimana cara menambahkan beberapa gambar, masing‑masing pada halaman terpisah?

Lakukan iterasi pada koleksi jalur file:

```csharp
foreach (var path in imagePaths)
{
    using var stream = File.OpenRead(path);
    var page = pdfDocument.Pages.Add();
    page.AddImage(stream, pageBounds, pageBounds); // No crop for each image.
}
```

### Bagaimana dengan transparansi atau gambar PNG?

Aspose.Pdf memperlakukan PNG sama seperti JPEG. Jika sumber memiliki kanal alfa, PDF akan mempertahankannya, asalkan versi PDF mendukung transparansi (default sudah cukup).

### Apakah ini bekerja di .NET Core pada Linux?

Ya. Aspose.Pdf bersifat lintas‑platform; pastikan `imageStream` mengarah ke jalur file yang valid di OS target. Tidak ada API khusus Windows yang digunakan.

---

## Tips & Praktik Terbaik

- **Manajemen Memori:** Selalu bungkus stream dengan pernyataan `using` (seperti contoh) untuk menghindari penguncian file.  
- **Kinerja:** Jika Anda memproses puluhan gambar, pertimbangkan untuk menggunakan satu instance `Document` dan memanggil `pdfDocument.Pages.Add()` untuk setiap gambar.  
- **Penanganan Kesalahan:** Bungkus seluruh prosedur dalam blok `try/catch` dan log `PdfException` untuk pemecahan masalah.  
- **Kontrol Kualitas:** Aspose.Pdf memungkinkan Anda mengatur resolusi gambar melalui `ImageFragment`. Untuk pemindaian DPI tinggi, setel `ImageFragment.Resolution = 300;`.  
- **Keamanan:** Jika PDF akan dibagikan secara eksternal, Anda dapat menambahkan enkripsi dengan `pdfDocument.Encrypt("ownerPwd", "userPwd", Permission.All);`.

---

## Kesimpulan

Kami baru saja membahas cara **membuat PDF dari JPG** di C#, **memotong gambar dalam PDF**, dan **menambahkan halaman PDF baru** untuk membangun dokumen multi‑halaman. Pola yang sama memungkinkan Anda **mengonversi JPG ke PDF dengan pemotongan** dan **menyisipkan gambar ke PDF C#** untuk skenario apa pun—dari kwitansi sederhana hingga buku foto yang kompleks.  

Cobalah: ubah logika pemotongan, bereksperimen dengan halaman A4, atau rangkaikan beberapa gambar bersama. Pustaka Aspose.Pdf membuat tugas‑tugas ini mudah, dan kode di atas merupakan referensi yang solid dan dapat dikutip untuk dimasukkan ke proyek apa pun.

---

### Apa Selanjutnya?

- **Menambahkan anotasi teks** ke PDF (misalnya, keterangan di bawah setiap gambar).  
- **Membuat daftar isi** secara otomatis untuk PDF multi‑halaman.  
- **Menggabungkan beberapa PDF** menggunakan `pdfDocument.Pages.AddRange(otherDoc.Pages);`.  

Setiap topik tersebut dibangun di atas dasar yang baru saja Anda kuasai, sehingga Anda berada pada posisi yang tepat untuk mengeksplorasinya.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}