---
category: general
date: 2026-09-18
description: Pelajari cara membuat kamus PDF kosong dalam C# menggunakan Aspose.PDF.
  Panduan langkah demi langkah ini mencakup ExtGState, status grafis, dan manipulasi
  CosPdfDictionary.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create empty PDF dictionary
- Aspose.PDF
- ExtGState dictionary
- graphics state
- CosPdfDictionary
- PDF manipulation C#
language: id
lastmod: 2026-09-18
og_description: Buat kamus PDF kosong di C# dengan Aspose.PDF. Ikuti tutorial komprehensif
  ini untuk mengedit ExtGState dan kamus keadaan grafik.
og_image_alt: Screenshot showing creation of an empty PDF dictionary in C#
og_title: Buat kamus PDF kosong di C# – panduan lengkap Aspose.PDF
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: Learn to create empty PDF dictionary in C# using Aspose.PDF. This step‑by‑step
    guide covers ExtGState, graphics state, and CosPdfDictionary manipulation.
  headline: How to create empty PDF dictionary with Aspose.PDF in C#
  type: TechArticle
tags:
- PDF
- C#
- Aspose.PDF
title: Cara membuat kamus PDF kosong dengan Aspose.PDF di C#
url: /id/net/programming-with-document/how-to-create-empty-pdf-dictionary-with-aspose-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara membuat kamus PDF kosong dengan Aspose.PDF di C#

Jika Anda perlu **membuat kamus PDF kosong** saat memproses file PDF, panduan ini menunjukkan secara tepat cara melakukannya menggunakan Aspose.PDF untuk .NET. Baik Anda menyesuaikan transparansi, mode pencampuran, atau keadaan grafik khusus apa pun, langkah‑langkah di bawah ini memungkinkan Anda mengedit kamus `ExtGState` dengan aman dan efisien.

Dalam tutorial ini Anda akan belajar:

* Memuat dokumen PDF dengan Aspose.PDF.
* Mengakses sumber daya halaman pertama dan kamus `ExtGState` yang ada.
* Membuat `CosPdfDictionary` kosong baru dan mengisinya dengan entri keadaan‑grafik.
* Menyimpan PDF yang telah dimodifikasi tanpa kehilangan konten asli.

Solusi ini bekerja dengan PDF apa pun yang memiliki setidaknya satu halaman dan hanya memerlukan pustaka Aspose.PDF (versi 23.10 atau lebih baru).

## Prasyarat

* .NET 6.0 atau lebih baru (kode juga dapat dijalankan pada .NET Framework 4.8).
* Referensi ke paket NuGet **Aspose.PDF**.
* File PDF masukan yang berada di `YOUR_DIRECTORY/input.pdf`.
* Pengetahuan dasar tentang C# dan konsep PDF seperti sumber daya dan keadaan grafik.

> **Pro tip:** Saat bekerja dengan PDF berukuran besar, bungkus objek `Document` dalam blok `using` untuk memastikan semua handle file segera dilepaskan.

## Langkah 1: Muat dokumen PDF

Operasi pertama membuka file sumber. Aspose.PDF membaca seluruh dokumen ke dalam memori, memungkinkan Anda mengedit objek internal.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Step 1: Load the PDF document
using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
{
    // Subsequent steps go here
}
```

*Mengapa ini penting*: Memuat dokumen menciptakan model objek yang dapat diubah. Tanpa langkah ini Anda tidak dapat mengakses sumber daya halaman yang diperlukan untuk manipulasi kamus.

## Langkah 2: Ambil sumber daya halaman pertama

Setiap halaman menyimpan kamus `Resources` yang berisi font, gambar, dan keadaan grafik. Mengaksesnya memberi Anda `DictionaryEditor` yang menyederhanakan operasi baca/tulis.

```csharp
// Step 2: Get the resources of the first page
Page firstPage = pdfDocument.Pages[1];
DictionaryEditor resourcesEditor = new DictionaryEditor(firstPage.Resources);
```

*Mengapa ini penting*: Kamus `ExtGState` berada di dalam sumber daya halaman. Mengedit kamus yang salah tidak akan berpengaruh pada proses rendering.

## Langkah 3: Temukan kamus ExtGState yang sudah ada

Entri `ExtGState` mungkin sudah berisi objek keadaan‑grafik. Kami mengambilnya sebagai `CosPdfDictionary` sehingga dapat menambahkan entri baru.

```csharp
// Step 3: Access the existing ExtGState dictionary
CosPdfDictionary extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
```

Jika entri `ExtGState` tidak ada, Aspose.PDF secara otomatis membuat kamus kosong ketika Anda menetapkan kamus baru nanti.

## Langkah 4: **Buat kamus PDF kosong** untuk keadaan grafik baru

Di sini kami membangun `CosPdfDictionary` baru—inti dari operasi **create empty PDF dictionary**. Kemudian kami mengisinya dengan kunci standar keadaan‑grafik:

* `CA` – opacity garis.
* `ca` – opacity isi.
* `BM` – mode pencampuran.

```csharp
// Step 4: Create a new graphics state dictionary and define its entries
CosPdfDictionary graphicsStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

KeyValuePair<string, ICosPdfPrimitive>[] graphicsStateEntries = new[]
{
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),          // Stroke opacity
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),       // Fill opacity
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))    // Blend mode
};

foreach (var entry in graphicsStateEntries)
    graphicsStateDict.Add(entry);
```

*Mengapa ini penting*: Dengan secara eksplisit mendefinisikan setiap entri, Anda mengontrol cara objek pada halaman bercampur dan dirender. Kamus tersebut **kosong** sampai Anda menambahkan kunci‑kunci ini, yang memenuhi persyaratan **create empty PDF dictionary** sebelum diisi.

## Langkah 5: Tambahkan keadaan grafik baru ke kamus ExtGState

Setiap keadaan grafik harus memiliki nama unik (misalnya `GS0`). Kami menyisipkan kamus yang baru dibangun di bawah nama tersebut.

```csharp
// Step 5: Add the new graphics state to the ExtGState dictionary with a unique name
extGStateDict.Add("GS0", graphicsStateDict);
```

Jika Anda memerlukan beberapa keadaan, terus tambahkan entri seperti `GS1`, `GS2`, dll., pastikan setiap nama unik dalam kamus `ExtGState`.

## Langkah 6: Simpan dokumen PDF yang telah diperbarui

Akhirnya, tulis perubahan kembali ke disk. File asli tetap tidak tersentuh karena kami menyimpan ke jalur baru.

```csharp
// Step 6: Save the updated PDF document
pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
}
```

`output.pdf` yang dihasilkan kini berisi keadaan grafik tambahan (`GS0`) yang dapat Anda referensikan dari aliran konten halaman mana pun menggunakan operator `/GS0`.

## Contoh lengkap yang berfungsi

Menggabungkan semua langkah menghasilkan program mandiri yang dapat langsung dijalankan.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;

class Program
{
    static void Main()
    {
        // Load the source PDF
        using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
        {
            // Access first page resources
            Page firstPage = pdfDocument.Pages[1];
            DictionaryEditor resourcesEditor = new DictionaryEditor(firstPage.Resources);

            // Get (or create) ExtGState dictionary
            CosPdfDictionary extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();

            // Build a new empty PDF dictionary for graphics state
            CosPdfDictionary graphicsStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            var entries = new[]
            {
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
            };
            foreach (var entry in entries)
                graphicsStateDict.Add(entry);

            // Insert the new graphics state with a unique name
            extGStateDict.Add("GS0", graphicsStateDict);

            // Save the modified document
            pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
        }

        Console.WriteLine("PDF updated successfully.");
    }
}
```

**Output yang diharapkan**: Setelah menjalankan program, `output.pdf` berisi konten visual yang sama dengan `input.pdf`. Memeriksa PDF dengan alat seperti Adobe Acrobat atau PDF‑Tron akan menampilkan entri baru `GS0` di bawah kamus `ExtGState` halaman pertama.

## Variasi umum dan kasus tepi

| Situasi | Apa yang harus disesuaikan |
|-----------|----------------|
| **Tidak ada entri ExtGState yang ada** | Ganti `resourcesEditor["ExtGState"]` dengan `new CosPdfDictionary(pdfDocument)` dan tetapkan kembali ke `firstPage.Resources["ExtGState"]`. |
| **Beberapa halaman memerlukan keadaan yang sama** | Tambahkan entri `GS0` yang sama ke kamus `ExtGState` tiap halaman, atau referensikan kamus dari objek sumber daya bersama. |
| **Mode pencampuran berbeda** | Ubah nilai `CosPdfName` dari `"Normal"` ke `"Multiply"`, `"Screen"`, dll., tergantung efek yang diinginkan. |
| **Nilai opacity lebih tinggi** | Gunakan `new CosPdfNumber(0.8)` untuk `ca` atau `CA` guna meningkatkan opacity isi atau garis. |
| **Menggunakan operator aliran** | Di aliran konten, tulis `"/GS0 gs"` sebelum operasi menggambar untuk menerapkan keadaan grafik baru. |

## Pertimbangan kinerja

* **Penggunaan memori** – Memuat PDF yang sangat besar mengonsumsi memori secara proporsional dengan jumlah halaman. Jika Anda hanya perlu mengedit halaman pertama, pertimbangkan menggunakan `pdfDocument.Pages.Delete(pageNumber)` setelah proses selesai untuk membebaskan sumber daya.
* **Keamanan thread** – Objek Aspose.PDF tidak thread‑safe. Lakukan edit kamus pada satu thread atau buat instance `Document` terpisah per thread.

## Kesimpulan

Anda kini tahu cara **create empty PDF dictionary** dengan Aspose.PDF, mengisinya dengan entri keadaan‑grafik, dan menempelkannya ke kamus `ExtGState` sebuah halaman. Teknik ini memungkinkan kontrol halus atas opacity, mode pencampuran, dan parameter rendering lainnya langsung dari C#.

Selanjutnya, jelajahi topik terkait seperti **PDF manipulation C#**, menambahkan entri **ExtGState dictionary** khusus untuk efek transparansi lanjutan, atau menggunakan **CosPdfDictionary** untuk memodifikasi tipe sumber daya lain seperti font atau XObject. Bereksperimenlah dengan beberapa keadaan grafik untuk membangun efek visual yang canggih dalam PDF Anda.

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait dan membangun di atas teknik yang ditunjukkan dalam panduan ini. Setiap sumber daya menyertakan contoh kode lengkap dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Create & Fill Rectangles in PDFs Using Aspose.PDF for .NET&#58; A Step-by-Step Guide](/pdf/english/net/images-graphics/create-fill-rectangle-aspose-pdf-net/)
- [How to Create Dashed Lines in PDFs Using Aspose.PDF for .NET&#58; A Step-by-Step Guide](/pdf/english/net/images-graphics/create-dashed-lines-aspose-pdf-net/)
- [How to Add an Empty Page at the End of a PDF Using Aspose.PDF for .NET | Step-by-Step Guide](/pdf/english/net/document-manipulation/add-empty-page-end-pdf-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}