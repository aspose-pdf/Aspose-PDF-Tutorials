---
category: general
date: 2026-08-17
description: Buat keadaan grafik kosong dalam PDF menggunakan C# dan Aspose.Pdf. Ikuti
  panduan langkah demi langkah ini untuk mengedit sumber daya ExtGState dengan aman.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create empty graphics state
- Aspose PDF graphics state
- C# modify PDF resources
- add ExtGState dictionary
- PDF page resources editing
language: id
lastmod: 2026-08-17
og_description: Buat keadaan grafik kosong dalam PDF menggunakan C#. Tutorial ini
  menunjukkan cara mengedit sumber daya ExtGState dengan Aspose.Pdf untuk modifikasi
  PDF yang dapat diandalkan.
og_image_alt: Screenshot of C# code that adds an empty graphics state to a PDF document
og_title: Buat keadaan grafik kosong di PDF dengan C# – panduan langkah demi langkah
schemas:
- author: Aspose
  dateModified: '2026-08-17'
  description: Create empty graphics state in a PDF using C# and Aspose.Pdf. Follow
    this step‑by‑step guide to edit ExtGState resources safely.
  headline: How to create empty graphics state in a PDF with C#
  type: TechArticle
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Cara membuat status grafis kosong dalam PDF dengan C#
url: /id/net/programming-with-operators/how-to-create-empty-graphics-state-in-a-pdf-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara membuat graphics state kosong dalam PDF dengan C#

Jika Anda perlu **membuat graphics state kosong** dalam PDF, panduan ini menunjukkan secara tepat cara melakukannya dengan C# dan Aspose.Pdf. Anda akan melihat contoh lengkap yang dapat dijalankan yang menambahkan entri baru ke kamus ExtGState halaman tanpa memengaruhi konten yang ada.

Bekerja dengan graphics state PDF adalah kebutuhan umum ketika Anda ingin mengontrol transparansi, mode pencampuran, atau parameter rendering lainnya secara per‑objek. Kode di bawah ini mendemonstrasikan pendekatan yang direkomendasikan, menjelaskan mengapa setiap langkah penting, dan mencakup variasi tipikal yang mungkin Anda temui.

## Prasyarat

Sebelum memulai, pastikan Anda memiliki:

* .NET 6.0 atau yang lebih baru (contoh dapat dikompilasi dengan .NET Core juga).
* Lisensi Aspose.Pdf untuk .NET (atau kunci evaluasi sementara).
* Folder yang berisi file `input.pdf` yang ingin Anda modifikasi.
* Pengetahuan dasar tentang sintaks C# dan konsep PDF seperti kamus sumber daya.

## Langkah 1: Siapkan proyek dan impor namespace

Buat aplikasi konsol baru atau integrasikan kode ke dalam proyek yang sudah ada. Tambahkan paket NuGet Aspose.Pdf:

```bash
dotnet add package Aspose.Pdf
```

Kemudian impor namespace yang diperlukan:

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Operators;
```

Impor ini memberi Anda akses ke kelas `Document`, `DictionaryEditor`, dan primitif PDF yang dibutuhkan untuk **membuat graphics state kosong**.

## Langkah 2: Tentukan folder yang berisi file PDF

```csharp
// Step 1: Define the folder that contains the PDF files
string dataDir = @"C:\PdfSamples\";
```

Ganti path dengan lokasi file PDF Anda sendiri. Menyimpan direktori dalam variabel membuat kode dapat digunakan kembali dan lebih mudah diuji.

## Langkah 3: Muat dokumen PDF sumber

```csharp
// Step 2: Load the source PDF document
using (var pdfDocument = new Document(dataDir + "input.pdf"))
{
    // All subsequent operations happen inside this using block
```

Membuka dokumen di dalam pernyataan `using` memastikan handle file dilepaskan secara otomatis setelah Anda menyimpan perubahan.

## Langkah 4: Akses halaman pertama dan kamus Resources‑nya

```csharp
    // Step 3: Get the first page and its Resources dictionary
    var firstPage = pdfDocument.Pages[1];
    var resourcesEditor = new DictionaryEditor(firstPage.Resources);
    var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
```

* `Pages[1]` mengambil halaman pertama (nomor halaman PDF dimulai dari 1).
* `DictionaryEditor` menyediakan cara yang nyaman untuk membaca dan memodifikasi kamus PDF.
* Entri `ExtGState` menyimpan semua objek graphics‑state untuk halaman tersebut. Jika kunci tidak ada, Aspose.Pdf secara otomatis membuat kamus kosong.

## Langkah 5: Bangun kamus graphics‑state kosong baru

Graphics state yang Anda tambahkan dapat kosong atau sudah berisi parameter seperti opacity (`CA`, `ca`) atau blend mode (`BM`). Dalam tutorial ini kami membuat **graphics state kosong** dan kemudian menetapkan beberapa nilai tipikal untuk mengilustrasikan cara kerja kamus.

```csharp
    // Step 4: Create a new empty graphics‑state dictionary and set its parameters
    var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
    var parameters = new[]
    {
        new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),   // Stroke opacity
        new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // Fill opacity
        new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // Blend mode
    };
    foreach (var p in parameters)
        newGraphicsState.Add(p);
```

* `CosPdfDictionary.CreateEmptyDictionary` membuat wadah bersih yang dapat Anda isi dengan kunci graphics‑state apa pun.
* Menambahkan `CA`, `ca`, dan `BM` bersifat opsional; Anda dapat menghilangkannya jika benar‑benar membutuhkan state kosong. Kode ini menunjukkan cara menambahkan entri ketika Anda kemudian memutuskan untuk mengontrol rendering.

## Langkah 6: Sisipkan graphics state baru ke dalam kamus ExtGState

```csharp
    // Step 5: Add the new graphics state to the page's ExtGState dictionary (e.g., name it "GS0")
    extGStateDict.Add("GS0", newGraphicsState);
```

Menamai entri `"GS0"` mengikuti konvensi umum memberi awalan “GS” pada nama graphics‑state. Anda dapat memilih nama PDF yang valid asalkan tidak bentrok dengan kunci yang sudah ada.

## Langkah 7: Simpan dokumen PDF yang telah dimodifikasi

```csharp
    // Step 6: Save the modified PDF document
    pdfDocument.Save(dataDir + "output.pdf");
}
```

Pemanggilan `Save` menulis file yang telah diperbarui ke `output.pdf`. Membuka file ini di penampil PDF mengonfirmasi bahwa graphics state baru ada; Anda dapat merujuknya nanti dengan operator `gs` dalam aliran konten.

### Daftar sumber lengkap

Menggabungkan semua bagian, program lengkapnya terlihat seperti ini:

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Operators;

class Program
{
    static void Main()
    {
        // Define the folder that contains the PDF files
        string dataDir = @"C:\PdfSamples\";

        // Load the source PDF document
        using (var pdfDocument = new Document(dataDir + "input.pdf"))
        {
            // Get the first page and its Resources dictionary
            var firstPage = pdfDocument.Pages[1];
            var resourcesEditor = new DictionaryEditor(firstPage.Resources);
            var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();

            // Create a new empty graphics‑state dictionary and set its parameters
            var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            var parameters = new[]
            {
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
            };
            foreach (var p in parameters)
                newGraphicsState.Add(p);

            // Add the new graphics state to the page's ExtGState dictionary (name it "GS0")
            extGStateDict.Add("GS0", newGraphicsState);

            // Save the modified PDF document
            pdfDocument.Save(dataDir + "output.pdf");
        }

        Console.WriteLine("Empty graphics state created and saved to output.pdf");
    }
}
```

Menjalankan program mencetak baris konfirmasi dan menghasilkan `output.pdf` dengan graphics state yang baru ditambahkan.

## Mengapa pendekatan ini paling efektif

* **Pengeditan kamus langsung** – Menggunakan `DictionaryEditor` menghindari kebutuhan untuk mengurai seluruh aliran konten. Anda hanya memodifikasi sumber daya yang Anda perlukan.
* **Primtif PDF bertipe** – `CosPdfNumber`, `CosPdfName`, dan `CosPdfDictionary` menjamin PDF yang dihasilkan mematuhi spesifikasi PDF 1.7.
* **Keamanan** – Blok `using` membuang objek `Document`, mencegah penguncian file yang dapat merusak build selanjutnya.
* **Ekstensibilitas** – Setelah graphics state kosong ada, Anda dapat merujuknya dari operator konten mana pun (`gs`) untuk mengubah opacity, blend mode, atau parameter lain pada perintah gambar yang dipilih.

## Variasi umum dan kasus tepi

| Situasi | Penyesuaian yang disarankan |
|-----------|-------------------|
| **Beberapa halaman** | Lakukan loop pada `pdfDocument.Pages` dan ulangi penyisipan kamus untuk setiap halaman yang perlu Anda modifikasi. |
| **Tidak ada entri ExtGState yang ada** | `resourcesEditor["ExtGState"]` secara otomatis membuat kamus kosong jika belum ada. Tidak diperlukan kode tambahan. |
| **Nama graphics‑state yang berbeda** | Ganti `"GS0"` dengan nama yang sesuai konvensi penamaan Anda, misalnya `"MyTransparentState"`. |
| **Menambahkan hanya state kosong** | Hapus array `parameters` dan loop `foreach`; kamus akan tetap kosong. |
| **Bekerja dengan PDF terenkripsi** | Berikan password saat membuat `new Document(path, password)` sebelum mengedit sumber daya. |

## Memverifikasi hasil

Anda dapat memverifikasi bahwa graphics state telah ditambahkan dengan memeriksa PDF menggunakan penampil tingkat‑rendah seperti **PDF‑Tron** atau **iText Sharp**. Cari entri serupa dengan:

```
/ExtGState << /GS0 << /CA 1 /ca 0.5 /BM /Normal >> >>
```

Jika entri muncul, operasi **create empty graphics state** berhasil.

## Kesimpulan

Anda kini tahu cara **membuat graphics state kosong** dalam PDF menggunakan C# dan Aspose.Pdf. Tutorial ini mencakup setiap langkah—dari memuat dokumen hingga mengedit kamus `ExtGState` dan menyimpan hasilnya—serta menjelaskan alasan di balik setiap tindakan.

Dari sini Anda dapat:

* Menggunakan graphics state baru dalam aliran konten (`gs /GS0`).
* Bereksperimen dengan kunci tambahan seperti `/SM` (penyesuaian goresan) atau `/OPM` (mode overprint).
* Menerapkan teknik yang sama pada tipe sumber daya lain seperti `/XObject` atau `/ColorSpace`.

Selamat bereksperimen dengan PDF, dan jangan ragu menjelajahi skenario **Aspose PDF graphics state** lainnya seperti perubahan opacity dinamis atau blend mode khusus!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber daya menyertakan contoh kode lengkap yang dapat dijalankan dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Cara Membuat Garis Putus-putus dalam PDF Menggunakan Aspose.PDF untuk .NET: Panduan Langkah demi Langkah](/pdf/english/net/images-graphics/create-dashed-lines-aspose-pdf-net/)
- [Cara Menghapus Grafik dari PDF Menggunakan Aspose.PDF .NET: Panduan Lengkap](/pdf/english/net/images-graphics/remove-graphics-aspose-pdf-net/)
- [Membuat & Mengisi Persegi Panjang dalam PDF Menggunakan Aspose.PDF untuk .NET: Panduan Langkah demi Langkah](/pdf/english/net/images-graphics/create-fill-rectangle-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}