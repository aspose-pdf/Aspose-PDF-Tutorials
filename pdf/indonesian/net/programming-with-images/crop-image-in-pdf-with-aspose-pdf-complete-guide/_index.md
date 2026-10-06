---
category: general
date: 2026-06-08
description: Potong gambar dalam PDF menggunakan Aspose.PDF di C#. Pelajari cara membuat
  PDF dengan gambar, menyimpan PDF dengan gambar, dan menambahkan gambar ke PDF hanya
  dalam beberapa baris.
draft: false
keywords:
- crop image in pdf
- create pdf with image
- save pdf with image
- how to add image to pdf
- how to crop image pdf
language: id
og_description: Potong gambar dalam PDF menggunakan Aspose.PDF di C#. Tutorial ini
  menunjukkan cara membuat PDF dengan gambar, menyimpan PDF dengan gambar, dan menambahkan
  gambar ke PDF dengan cepat.
og_title: Memotong Gambar dalam PDF dengan Aspose.PDF – Panduan Lengkap
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Crop image in PDF using Aspose.PDF in C#. Learn how to create PDF with
    image, save PDF with image, and add image to PDF in just a few lines.
  headline: Crop Image in PDF with Aspose.PDF – Complete Guide
  type: TechArticle
- description: Crop image in PDF using Aspose.PDF in C#. Learn how to create PDF with
    image, save PDF with image, and add image to PDF in just a few lines.
  name: Crop Image in PDF with Aspose.PDF – Complete Guide
  steps:
  - name: '**Image stream** – the raw bytes of your picture.'
    text: '**Image stream** – the raw bytes of your picture.'
  - name: '**Placement rectangle** – where on the page the image lives.'
    text: '**Placement rectangle** – where on the page the image lives.'
  - name: '**Crop rectangle** – the portion of the image you actually want to render.'
    text: '**Crop rectangle** – the portion of the image you actually want to render.'
  type: HowTo
tags:
- Aspose.PDF
- C#
- PDF manipulation
- Image processing
title: Memotong Gambar dalam PDF dengan Aspose.PDF – Panduan Lengkap
url: /id/net/programming-with-images/crop-image-in-pdf-with-aspose-pdf-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Memotong Gambar dalam PDF dengan Aspose.PDF – Panduan Lengkap

Pernah bertanya-tanya bagaimana cara **crop image in PDF** tanpa harus membuka editor grafis? Anda tidak sendirian. Dalam banyak laporan, faktur, atau e‑book Anda hanya membutuhkan sebagian kecil gambar—mungkin sudut logo atau potongan grafik—dan Anda ingin menambahkannya langsung ke dalam PDF.  

Panduan ini menunjukkan hal tersebut: kami akan **create PDF with image**, **add image to PDF**, dan kemudian **crop image in PDF** menggunakan pustaka Aspose.PDF untuk C#. Pada akhir tutorial Anda juga akan mengetahui cara **save PDF with image** sehingga Anda dapat mengirimkan file tersebut ke siapa saja.

---

## Apa yang Anda Butuhkan

- .NET 6.0 atau lebih baru (kode ini juga bekerja dengan .NET Framework 4.6+)  
- Salinan berlisensi atau percobaan dari **Aspose.PDF for .NET** (pasang via NuGet `Install-Package Aspose.PDF`)  
- File gambar (JPEG/PNG) di disk – kami akan menyebutnya `image.jpg`  
- IDE apa saja yang Anda suka (Visual Studio, Rider, VS Code)

Itu saja. Tidak ada layanan tambahan, tidak ada alat eksternal.

---

## Langkah 1: Siapkan Proyek dan Impor

Pertama, buat aplikasi console dan impor namespace yang akan kita gunakan. Pernyataan `using` membuat kode rapi dan memudahkan langkah selanjutnya untuk dibaca.

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;   // for text fragments if you want captions later
```

> **Pro tip:** Jika Anda menggunakan Visual Studio, klik kanan proyek → *Manage NuGet Packages* → cari “Aspose.PDF” dan pasang. Pustaka ini menangani penempatan gambar dan pemotongan secara internal, sehingga Anda tidak memerlukan pustaka gambar pihak ketiga.

---

## Langkah 2: Buat PDF dengan Gambar

Sekarang kita benar‑benarnya **create pdf with image**. Potongan kode di bawah membuat `Document` baru, menambahkan halaman kosong, dan menyiapkan aliran gambar.

```csharp
// Initialize a new PDF document
Document pdf = new Document();

// Add a blank page – think of it as a clean canvas
Page page = pdf.Pages.Add();

// Open the source image file
using (FileStream imgStream = new FileStream("YOUR_DIRECTORY/image.jpg", FileMode.Open))
{
    // We'll place the whole image first; cropping comes next
    // Define where the image should sit on the page (in points; 1 point = 1/72 inch)
    Rectangle placement = new Rectangle(0, 0, 600, 800); // width=600pt, height=800pt

    // Add the image without cropping yet – just to see the full picture
    page.AddImage(imgStream, placement);
}
```

Menjalankan kode ini akan menghasilkan PDF dengan seluruh gambar yang diregangkan ke dimensi yang Anda tentukan. Ini merupakan pemeriksaan awal yang baik sebelum Anda mulai memotong.

---

## Langkah 3: Cara Menambahkan Gambar ke PDF (dan Menyiapkan Pemotongan)

Jika Anda sudah mengetahui wilayah tepat yang diinginkan, Anda dapat melewatkan langkah ukuran penuh dan langsung ke bagian **how to add image to pdf**. Metode `AddImage` menerima tiga parameter:

1. **Image stream** – byte mentah gambar Anda.  
2. **Placement rectangle** – lokasi gambar pada halaman.  
3. **Crop rectangle** – bagian gambar yang ingin Anda tampilkan.

Berikut adalah versi ringkas yang melakukan penempatan **dan** pemotongan dalam satu panggilan.

```csharp
using (FileStream imgStream = new FileStream("YOUR_DIRECTORY/image.jpg", FileMode.Open))
{
    // Full‑size placement rectangle (you can adjust X/Y if you need margins)
    Rectangle placement = new Rectangle(0, 0, 600, 800);

    // Crop area: upper‑left quarter of the original image
    Rectangle crop = new Rectangle(0, 0, placement.Width / 2, placement.Height / 2);

    // This single line both adds the image and crops it
    page.AddImage(imgStream, placement, crop);
}
```

> **Why this works:** Aspose.PDF secara internal memetakan crop rectangle ke dimensi piksel gambar, lalu merender hanya potongan tersebut di dalam area `placement`. Tidak diperlukan pemrosesan bitmap tambahan, yang berarti ukuran PDF tetap kecil.

---

## Langkah 4: Cara Memotong Gambar PDF – Opsi Lanjutan

Kadang‑kadang pemotongan seperempat tidak cukup. Mungkin Anda membutuhkan rectangle khusus atau ingin mempertahankan rasio aspek gambar. Berikut pendekatan yang lebih fleksibel:

```csharp
using (FileStream imgStream = new FileStream("YOUR_DIRECTORY/image.jpg", FileMode.Open))
{
    // Placement on the page (centered, 300pt wide, keep original height)
    Rectangle placement = new Rectangle(150, 400, 450, 1200);

    // Suppose you want a 200 × 150 pixel region starting at (50, 30) in the source image
    // First, convert pixel coordinates to points (assuming 72 DPI)
    float dpi = 72f;
    float left   = 50  / dpi * 72; // = 50 points
    float bottom = 30  / dpi * 72; // = 30 points
    float width  = 200 / dpi * 72; // = 200 points
    float height = 150 / dpi * 72; // = 150 points

    Rectangle crop = new Rectangle(left, bottom, left + width, bottom + height);

    page.AddImage(imgStream, placement, crop);
}
```

**Penanganan kasus tepi:**  
- **Null streams** – selalu bungkus `FileStream` dalam blok `using`, seperti yang ditunjukkan, untuk menghindari kebocoran.  
- **Large images** – jika gambar sumber sangat besar, pertimbangkan untuk memperkecil rectangle `placement`; Aspose akan menurunkan sampel secara otomatis.  
- **Transparent PNGs** – pustaka menghormati kanal alfa, sehingga area yang dipotong akan mempertahankan transparansi.

---

## Langkah 5: Simpan PDF dengan Gambar (dan Verifikasi)

Akhirnya, kita **save pdf with image**. Metode `Save` menulis dokumen ke disk. Anda juga dapat mengirimnya kembali ke klien web jika Anda membuat API.

```csharp
// Save the final PDF to the output folder
pdf.Save("YOUR_DIRECTORY/output.pdf");

// Optional: Open the file automatically (only works on Windows)
System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo
{
    FileName = "YOUR_DIRECTORY/output.pdf",
    UseShellExecute = true
});
```

Saat Anda membuka `output.pdf`, Anda akan melihat hanya bagian yang dipotong dari `image.jpg` yang ditempatkan tepat di lokasi yang Anda tentukan. Jika gambar tampak terdistorsi, sesuaikan lebar/tinggi rectangle `placement` agar cocok dengan rasio aspek rectangle crop.

---

## Pertanyaan Umum & Hal-hal yang Perlu Diwaspadai

| Pertanyaan | Jawaban |
|------------|---------|
| **Apakah saya dapat memotong beberapa gambar pada halaman yang sama?** | Tentu saja. Panggil `page.AddImage` untuk setiap gambar dengan rectangle penempatan dan pemotongan masing‑masing. |
| **Bagaimana jika gambar saya dalam format berbeda (misalnya BMP)?** | Aspose.PDF mendukung JPEG, PNG, BMP, GIF, dan TIFF secara bawaan. Cukup ubah ekstensi file. |
| **Apakah saya memerlukan lisensi untuk penggunaan produksi?** | Versi percobaan berfungsi hingga 5 halaman. Untuk penggunaan sebenarnya, beli lisensi untuk menghilangkan watermark. |
| **Bagaimana cara memutar gambar yang dipotong?** | Setelah menambahkan gambar, dapatkan objek `Image` dan atur properti `Rotate`‑nya (`Rotate = RotationAngle.Rotate90`). |
| **Apakah ada cara memotong menggunakan persentase alih‑alih poin absolut?** | Ya—hitung dimensi rectangle berdasarkan `image.Width * 0.25` dll., kemudian konversikan ke poin seperti yang ditunjukkan pada Langkah 4. |

---

## Contoh Lengkap yang Siap Pakai (Copy‑Paste Ready)

```csharp
using System;
using System.IO;
using Aspose.Pdf;

namespace CropImageInPdfDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create a new PDF document and add a blank page
            Document pdf = new Document();
            Page page = pdf.Pages.Add();

            // 2️⃣ Open the image that will be placed on the page
            using (FileStream imgStream = new FileStream("YOUR_DIRECTORY/image.jpg", FileMode.Open))
            {
                // 3️⃣ Define where the image will sit on the page (points)
                Rectangle placement = new Rectangle(0, 0, 600, 800);

                // 4️⃣ Define the crop area – upper‑left quarter of the image
                Rectangle crop = new Rectangle(0, 0, placement.Width / 2, placement.Height / 2);

                // 5️⃣ Add the image using both placement and crop rectangles
                page.AddImage(imgStream, placement, crop);
            }

            // (Optional) Save the PDF to verify the result
            pdf.Save("YOUR_DIRECTORY/output.pdf");

            Console.WriteLine("PDF created and image cropped successfully!");
        }
    }
}
```

Jalankan program, buka `output.pdf`, dan Anda akan melihat hanya seperempat kiri‑atas dari `image.jpg` yang ditampilkan di sudut kiri‑atas halaman. Ubah nilai rectangle `crop` untuk bereksperimen dengan potongan yang berbeda.

---

## Kesimpulan

Kami telah menelusuri seluruh proses **crop image in pdf** menggunakan Aspose.PDF untuk C#. Mulai dari dokumen baru, kami **create pdf with image**, mendemonstrasikan **how to add image to pdf**, menerapkan rectangle **how to crop image pdf** yang dapat disesuaikan, dan akhirnya **save pdf with image**.  

Sekarang Anda dapat menyisipkan gambar yang dipotong secara presisi ke dalam PDF apa pun yang Anda hasilkan—sangat cocok untuk faktur, brosur pemasaran, atau laporan otomatis. Selanjutnya, pertimbangkan menambahkan keterangan teks (`TextFragment`) atau menggambar bentuk di sekitar gambar yang dipotong untuk menyorotnya lebih lanjut.  

Ada skenario lain yang ingin Anda ketahui? Tinggalkan komentar, dan selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

- [Cara Mengatur Ukuran Gambar dalam PDF Menggunakan Aspose.PDF untuk .NET](/pdf/english/net/images-graphics/set-image-size-pdf-aspose-dotnet/)
- [Cara Menambahkan Stempel Gambar ke PDF Menggunakan Aspose.PDF untuk .NET&#58; Panduan Komprehensif](/pdf/english/net/images-graphics/add-image-stamp-pdf-aspose-dotnet/)
- [Cara Mengekstrak Informasi Gambar dari PDF Menggunakan Aspose.PDF untuk .NET](/pdf/english/net/images-graphics/extract-image-info-pdf-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}