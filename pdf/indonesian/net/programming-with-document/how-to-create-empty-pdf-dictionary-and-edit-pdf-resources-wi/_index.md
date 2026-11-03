---
category: general
date: 2026-10-26
description: Pelajari cara membuat kamus PDF kosong dan mengedit sumber daya PDF menggunakan
  Aspose.PDF untuk C#. Panduan langkah demi langkah dengan contoh kode lengkap.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create empty PDF dictionary
- edit PDF resources
- Aspose.PDF C#
- PDF manipulation C#
- PDF graphics state
language: id
lastmod: 2026-10-26
og_description: Buat kamus PDF kosong dan edit sumber daya PDF dengan Aspose.PDF untuk
  C#. Ikuti tutorial lengkap ini untuk memodifikasi keadaan grafis dalam PDF.
og_image_alt: Screenshot showing creation of empty PDF dictionary in Aspose.PDF
og_title: Buat kamus PDF kosong & edit sumber daya PDF di C# – Panduan Aspose.PDF
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn to create empty PDF dictionary and edit PDF resources using Aspose.PDF
    for C#. Step‑by‑step guide with full code example.
  headline: How to create empty PDF dictionary and edit PDF resources with Aspose.PDF
    in C#
  type: TechArticle
- description: Learn to create empty PDF dictionary and edit PDF resources using Aspose.PDF
    for C#. Step‑by‑step guide with full code example.
  name: How to create empty PDF dictionary and edit PDF resources with Aspose.PDF
    in C#
  steps:
  - name: Populate the graphics state entries
    text: 'Add the standard keys:'
  - name: Register the new graphics state in the resource dictionary
    text: Give the state a name (`GS0`) and add it to the `ExtGState` dictionary that
      lives inside the page resources.
  - name: Expected output
    text: 'Running the program prints:'
  type: HowTo
tags:
- Aspose.PDF
- C#
- PDF
title: Cara membuat kamus PDF kosong dan mengedit sumber daya PDF dengan Aspose.PDF
  di C#
url: /id/net/programming-with-document/how-to-create-empty-pdf-dictionary-and-edit-pdf-resources-wi/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara membuat kamus PDF kosong dan mengedit sumber daya PDF dengan Aspose.PDF di C#

Jika Anda perlu **membuat kamus PDF kosong** dan kemudian **mengedit sumber daya PDF** dalam aplikasi C#, panduan ini menunjukkan langkah‑langkah tepatnya. Anda akan melihat contoh lengkap yang dapat dijalankan yang menambahkan keadaan grafis khusus ke halaman pertama dari PDF yang ada.

Bekerja dengan objek PDF tingkat‑rendah dapat terasa menakutkan, tetapi Aspose.PDF menyediakan API yang jelas untuk manipulasi kamus. Pada akhir tutorial ini Anda akan memahami mengapa setiap operasi penting dan bagaimana menyesuaikan kode untuk tipe sumber daya lainnya.

## Prasyarat

Sebelum memulai, pastikan Anda memiliki:

* .NET 6.0 (atau lebih baru) terpasang.
* Salinan berlisensi **Aspose.PDF for .NET** – versi percobaan gratis dapat digunakan untuk pengujian.
* IDE seperti Visual Studio 2022.
* File PDF bernama `input.pdf` yang ditempatkan dalam folder yang dapat Anda referensikan dari kode.

Tidak ada paket NuGet tambahan yang diperlukan selain `Aspose.Pdf`.

## Langkah 1: Siapkan proyek dan impor namespace

Buat proyek konsol baru dan tambahkan paket Aspose.PDF:

```bash
dotnet new console -n PdfDictionaryDemo
cd PdfDictionaryDemo
dotnet add package Aspose.Pdf
```

Di `Program.cs` impor namespace yang akan Anda gunakan:

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Cos;
```

Impor ini memperkenalkan kelas `Document`, `DictionaryEditor`, dan COS (Canonical Object Structure) yang memungkinkan Anda **membuat kamus PDF kosong** dan memodifikasi kamus sumber daya yang ada.

## Langkah 2: Tentukan folder yang berisi file PDF

Tentukan direktori yang menyimpan `input.pdf`. Menggunakan jalur absolut menghindari ambiguitas ketika program dijalankan dari direktori kerja yang berbeda.

```csharp
// Step 1: Define the folder that contains the PDF files
string dataDir = @"C:\PdfDemo\";
```

Ganti `C:\PdfDemo\` dengan jalur pada mesin Anda. Menyimpan jalur dalam variabel memudahkan penggunaan kembali untuk file input dan output.

## Langkah 3: Buka dokumen PDF sumber

Muat PDF yang ingin Anda ubah di dalam blok `using` sehingga handle file dilepaskan secara otomatis.

```csharp
// Step 2: Open the source PDF document
using (var pdfDocument = new Document(dataDir + "input.pdf"))
{
    // The rest of the workflow lives inside this block
}
```

Membuka dokumen memberi Anda akses ke koleksi halaman, kamus sumber daya, dan objek COS tingkat‑rendah.

## Langkah 4: Akses halaman pertama dan kamus sumber dayanya

Halaman pertama diindeks dengan `1` (halaman PDF bersifat 1‑based). Ambil kamus `Resources` halaman tersebut dan bungkus dalam `DictionaryEditor` untuk memungkinkan pengeditan yang aman.

```csharp
// Step 3: Access the first page and its resource dictionary
var firstPage = pdfDocument.Pages[1];
var resourcesEditor = new DictionaryEditor(firstPage.Resources);
```

`DictionaryEditor` mengabstraksi struktur COS yang mendasari, memungkinkan Anda membaca atau membuat entri tanpa merusak PDF.

## Langkah 5: **Membuat kamus PDF kosong** untuk keadaan grafis baru

Keadaan grafis mengontrol transparansi, mode pencampuran, dan parameter gambar lainnya. Untuk menambahkan keadaan khusus, pertama‑tama Anda memerlukan kamus kosong, lalu mengisi dengan entri yang diperlukan.

```csharp
// Step 4: Retrieve the ExtGState dictionary and add a new graphics state
var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();

// Create an empty dictionary that will hold the graphics state parameters
var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
```

Pemanggilan `CreateEmptyDictionary` adalah inti dari **pembuatan kamus PDF kosong**. Metode ini mengembalikan kamus COS yang berada dalam dokumen yang sama, memastikan integritas referensi silang.

### Isi entri keadaan grafis

Tambahkan kunci standar:

* `CA` – konstanta alfa untuk stroke (rentang 0 – 1).
* `ca` – konstanta alfa untuk non‑stroke.
* `BM` – nama mode pencampuran.

```csharp
var graphicsStateEntries = new[]
{
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
};

foreach (var entry in graphicsStateEntries)
    newGraphicsState.Add(entry);
```

Setiap entri ditambahkan ke kamus kosong yang baru saja Anda buat. Dengan memisahkan definisi dari loop penyisipan, kode tetap mudah dibaca dan mudah diperluas dengan kunci tambahan di kemudian hari.

### Daftarkan keadaan grafis baru ke dalam kamus sumber daya

Berikan keadaan tersebut nama (`GS0`) dan tambahkan ke kamus `ExtGState` yang berada di dalam sumber daya halaman.

```csharp
// Name the new graphics state "GS0"
extGStateDict.Add("GS0", newGraphicsState);
```

Sekarang kamus sumber daya halaman berisi referensi ke keadaan grafis khusus, yang dapat Anda terapkan ke aliran konten nanti.

## Langkah 6: Simpan PDF yang telah diperbarui

Akhirnya, tulis dokumen yang telah dimodifikasi ke file baru. Menjaga file asli tetap tidak tersentuh membantu Anda memverifikasi perubahan.

```csharp
// Step 5: Save the updated PDF
pdfDocument.Save(dataDir + "output.pdf");
```

Saat Anda membuka `output.pdf` di penampil yang mendukung inspeksi keadaan grafis (misalnya Adobe Acrobat Pro), Anda akan melihat kamus `ExtGState` berisi entri bernama `GS0` dengan nilai yang Anda definisikan.

## Kode sumber lengkap

Menggabungkan semua bagian menghasilkan program mandiri:

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Cos;

class Program
{
    static void Main()
    {
        // Step 1: Define the folder that contains the PDF files
        string dataDir = @"C:\PdfDemo\"; // adjust to your environment

        // Step 2: Open the source PDF document
        using (var pdfDocument = new Document(dataDir + "input.pdf"))
        {
            // Step 3: Access the first page and its resource dictionary
            var firstPage = pdfDocument.Pages[1];
            var resourcesEditor = new DictionaryEditor(firstPage.Resources);

            // Step 4: Retrieve the ExtGState dictionary and add a new graphics state
            var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();

            // **Create empty PDF dictionary** for the new graphics state
            var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            var graphicsStateEntries = new[]
            {
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
            };

            foreach (var entry in graphicsStateEntries)
                newGraphicsState.Add(entry);

            // Register the new graphics state as "GS0"
            extGStateDict.Add("GS0", newGraphicsState);

            // Step 5: Save the updated PDF
            pdfDocument.Save(dataDir + "output.pdf");
        }

        Console.WriteLine("PDF updated successfully.");
    }
}
```

### Output yang diharapkan

Menjalankan program akan mencetak:

```
PDF updated successfully.
```

dan membuat `output.pdf` di folder yang sama. Membuka file tersebut memperlihatkan entri baru di **Resources → ExtGState → GS0** dengan parameter yang Anda setel.

## Variasi umum dan kasus tepi

| Situasi | Cara menyesuaikan kode |
|-----------|-----------------------|
| **Beberapa halaman** memerlukan keadaan grafis yang sama | Buat kamus sekali, lalu tambahkan referensi `GS0` yang sama ke kamus `ExtGState` setiap halaman. |
| **Mode pencampuran berbeda** (mis., `Multiply`) | Ubah nilai `CosPdfName("Normal")` menjadi `CosPdfName("Multiply")`. |
| **Tidak ada kamus ExtGState yang ada** | Sebelum mengakses `resourcesEditor["ExtGState"]`, periksa `resourcesEditor.ContainsKey("ExtGState")`. Jika tidak ada, buat kamus kosong baru dan tambahkan ke `firstPage.Resources`. |
| **PDF besar** menyebabkan tekanan memori | Gunakan overload `PdfDocument.Load` yang melakukan streaming halaman, atau proses halaman satu per satu di dalam blok `using`. |
| **Perlu mengedit sumber daya lain** (font, XObject) | Ganti `"ExtGState"` dengan `"Font"` atau `"XObject"` pada pencarian `resourcesEditor`, lalu ikuti pola yang sama: buat kamus kosong dan isi. |

Variasi ini menunjukkan bagaimana pola **membuat kamus PDF kosong** yang sama dapat diterapkan pada tipe sumber daya apa pun yang ingin Anda **edit sumber daya PDF**.

## Tips profesional

* **Validasi hasil** – setelah menyimpan, buka PDF dengan alat yang dapat menampilkan kamus sumber daya mentah (mis., `PDFDebugger` dari PDF‑Box) untuk memastikan entri ada.
* **Gunakan kembali kamus** – jika Anda menambahkan keadaan grafis yang sama ke banyak halaman, simpan kamus dalam variabel dan referensikan daripada membuatnya berulang‑ulang.
* **Kompatibilitas versi** – kode ini bekerja dengan Aspose.PDF 23.12 dan yang lebih baru. Versi sebelumnya mungkin memerlukan `CosDictionary` alih‑alih `CosPdfDictionary`.

## Kesimpulan

Anda kini mengetahui cara **membuat kamus PDF kosong** dan **mengedit sumber daya PDF** menggunakan Aspose.PDF untuk C#. Tutorial ini mencakup membuka dokumen, mengakses kamus sumber daya halaman, membangun keadaan grafis khusus, mendaftarkannya, dan menyimpan hasilnya. Dari sini Anda dapat bereksperimen dengan tipe sumber daya lain, menggabungkan beberapa keadaan grafis, atau mengintegrasikan teknik ini ke dalam pipeline pemrosesan PDF yang lebih besar.

---

*Siap menjelajah lebih jauh? Coba tambahkan **ExtGState** khusus ke aliran konten, atau manipulasi kamus **Font** untuk menyematkan font baru. Kedua langkah tersebut mengikuti pola yang sama: membuat kamus kosong dan mengedit sumber daya PDF.*


## Apa yang Harus Anda Pelajari Selanjutnya?


Tutorial berikut membahas topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber daya menyertakan contoh kode lengkap dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Edit Kamus Sumber Daya PDF dengan Aspose.PDF – Panduan C#](/pdf/english/net/programming-with-operators/edit-pdf-resource-dictionary-with-aspose-pdf-c-guide/)
- [Buat keadaan grafis khusus dalam PDF menggunakan Aspose.Pdf](/pdf/english/net/programming-with-operators/create-custom-graphics-state-in-pdf-using-aspose-pdf/)
- [Cara membuat keadaan grafis kosong dalam PDF dengan C#](/pdf/english/net/programming-with-operators/how-to-create-empty-graphics-state-in-a-pdf-with-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}