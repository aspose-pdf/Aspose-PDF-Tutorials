---
category: general
date: 2026-03-06
description: Buat dokumen PDF dalam C# dan tambahkan nomor bates dengan mudah. Pelajari
  cara menambahkan halaman kosong pada PDF, menempatkan stempel pada halaman, dan
  menerapkan penomoran bates.
draft: false
keywords:
- create pdf document
- add bates number
- add blank page pdf
- how to add bates numbering
- place stamp on page
language: id
og_description: Buat dokumen PDF dalam C# dan tambahkan nomor bates. Panduan ini menunjukkan
  cara menambahkan halaman kosong PDF, menempatkan stempel pada halaman, dan menerapkan
  penomoran bates.
og_title: Buat Dokumen PDF dengan Penomoran Bates – Tutorial C#
tags:
- Aspose.Pdf
- C#
- PDF automation
title: Buat Dokumen PDF dengan Penomoran Bates di C# – Panduan Lengkap
url: /id/net/programming-with-stamps-and-watermarks/create-pdf-document-with-bates-numbering-in-c-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Membuat Dokumen PDF dengan Penomoran Bates di C#

Pernah perlu **membuat dokumen PDF** di C# dan bertanya‑tanya bagaimana menambahkan nomor Bates tanpa membuat rambut rontok? Anda tidak sendirian—firma hukum, pengadilan, dan bahkan beberapa tim kepatuhan korporat menghadapi teka‑teki ini setiap hari. Kabar baik? Dengan beberapa baris kode Aspose.Pdf Anda dapat membuat PDF baru, menambahkan halaman kosong, dan menempelkan nomor Bates yang tepat dalam satu alur yang mulus.

Dalam tutorial ini kita akan melewati seluruh proses: mulai dari menyiapkan proyek, menambahkan PDF halaman kosong, mempelajari **cara menambahkan penomoran Bates**, dan akhirnya **menempatkan stempel pada halaman** serta menyimpan hasilnya. Pada akhir tutorial Anda akan memiliki potongan kode siap pakai yang dapat disisipkan ke aplikasi .NET mana pun. Tanpa referensi samar, hanya contoh lengkap yang dapat dijalankan.

## Apa yang Anda Butuhkan

- **.NET 6+** (atau .NET Framework 4.6+ – Aspose.Pdf bekerja dengan keduanya)
- Paket NuGet **Aspose.Pdf for .NET** (`Install-Package Aspose.Pdf`)
- IDE yang memadai (Visual Studio, Rider, atau VS Code dengan ekstensi C#)

Itu saja. Tanpa DLL tambahan, tanpa layanan eksternal. Mari kita mulai.

## Langkah 1: Membuat Dokumen PDF – Penyiapan Awal

Hal pertama yang harus dilakukan, kita membutuhkan objek `Document` yang baru. Anggap saja ini sebagai kanvas kosong tempat semua hal lainnya akan berada.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Initialize a new PDF document
Document pdfDocument = new Document();
```

> **Mengapa ini penting:** Kelas `Document` adalah titik masuk untuk setiap operasi Aspose. Menginstansiasinya memberi Anda akses ke koleksi `Pages`, metadata, dan pengaturan keamanan—semua blok bangunan untuk PDF profesional.

## Langkah 2: Menambahkan PDF Halaman Kosong

PDF tanpa halaman ibarat buku tanpa halaman—tidak berguna. Menambahkan halaman kosong sangat mudah, dan memberi kita permukaan untuk menempelkan nomor Bates.

```csharp
// Add a single blank page to the document
Page page = pdfDocument.Pages.Add();
```

> **Tip pro:** Jika Anda memerlukan beberapa halaman, cukup panggil `pdfDocument.Pages.Add()` dalam sebuah loop. Setiap pemanggilan mengembalikan objek `Page` baru yang dapat Anda sesuaikan secara independen.

## Langkah 3: Cara Menambahkan Penomoran Bates – Membuat TextStamp

Sekarang masuk ke inti masalah: **nomor Bates**. Di Aspose.Pdf ini hanyalah sebuah `TextStamp` dengan flag artefak khusus.

```csharp
// Create a text stamp that will serve as a Bates number
TextStamp batesStamp = new TextStamp("Bates-001")
{
    // Mark the stamp as a Bates‑numbering artifact (helps PDF viewers treat it specially)
    Artifact = ArtifactType.BatesNumbering,
    // Align the stamp to the bottom‑right corner of the page
    HorizontalAlignment = HorizontalAlignment.Right,
    VerticalAlignment = VerticalAlignment.Bottom,
    // Add a small margin so the number isn’t glued to the edge
    Margin = new Margin { Bottom = 10, Right = 10 }
};
```

> **Mengapa kami mengatur `Artifact`:** Beberapa pembaca PDF menampilkan nomor Bates sebagai metadata yang dapat dicari. Menandai stempel sebagai artefak `BatesNumbering` memastikan bahwa alat downstream dapat mengenalinya secara otomatis.

## Langkah 4: Menempatkan Stempel pada Halaman

Dengan stempel yang siap, kini kita **menempatkan stempel pada halaman**. Ini adalah langkah di mana nomor visual sebenarnya muncul di PDF.

```csharp
// Add the Bates number stamp to the previously created page
page.AddStamp(batesStamp);
```

> **Kasus tepi:** Jika Anda memerlukan nomor yang bertambah pada setiap halaman, Anda dapat melakukan loop melalui `pdfDocument.Pages` dan memperbarui `batesStamp.Value` sebelum memanggil `AddStamp`. Contoh di sini tetap sederhana dengan “Bates‑001” statis.

## Langkah 5: Menyimpan dan Memverifikasi Hasil

Akhirnya, kita menyimpan PDF ke disk. Pilih folder yang Anda miliki hak tulisnya; jika tidak, Anda akan mendapatkan `UnauthorizedAccessException`.

```csharp
// Save the stamped PDF to a file
pdfDocument.Save("YOUR_DIRECTORY/BatesStamped.pdf");
```

Saat Anda membuka `BatesStamped.pdf` di penampil apa pun, Anda harus melihat “Bates‑001” kecil yang tertata rapi di sudut kanan‑bawah halaman kosong.

> **Output yang diharapkan:**  
> ![PDF with Bates number stamp](image-placeholder.png "PDF with Bates number stamp")  
> *Alt text: PDF with Bates number stamp on the bottom‑right corner.*

Jika nomor tidak muncul, periksa kembali nilai margin dan pastikan ukuran halaman tidak terlalu kecil (A4 default berfungsi baik). Juga pastikan flag `Artifact` tidak dihapus oleh alat pemrosesan pasca‑produksi apa pun.

## Contoh Lengkap yang Berfungsi

Berikut adalah program lengkap yang siap disalin‑tempel. Ia mencakup semua direktif `using` dan komentar untuk membantu Anda tetap terarah.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize a new PDF document
        Document pdfDocument = new Document();

        // 2️⃣ Add a blank page – this is where we’ll put the Bates number
        Page page = pdfDocument.Pages.Add();

        // 3️⃣ Create a TextStamp for the Bates number
        TextStamp batesStamp = new TextStamp("Bates-001")
        {
            Artifact = ArtifactType.BatesNumbering,          // Marks it as a Bates‑numbering artifact
            HorizontalAlignment = HorizontalAlignment.Right, // Align right
            VerticalAlignment = VerticalAlignment.Bottom,    // Align bottom
            Margin = new Margin { Bottom = 10, Right = 10 }  // Small margin from edges
        };

        // 4️⃣ Place the stamp on the page
        page.AddStamp(batesStamp);

        // 5️⃣ Save the PDF to disk
        string outputPath = @"C:\Temp\BatesStamped.pdf";
        pdfDocument.Save(outputPath);

        Console.WriteLine($"PDF created successfully: {outputPath}");
    }
}
```

Jalankan program, buka PDF, dan Anda akan melihat nomor Bates tepat di tempat yang kami tentukan. 🎉

## Variasi Umum & Hal-hal yang Perlu Diwaspadai

| Skenario | Apa yang Diubah | Mengapa |
|----------|----------------|-----|
| **Beberapa halaman, nomor bertambah** | Loop melalui `pdfDocument.Pages`, set `batesStamp.Value = $"Bates-{i:D3}"` sebelum `AddStamp` | Memberikan setiap halaman identifier unik, umum untuk bundel hukum |
| **Penempatan berbeda (atas‑kiri)** | Ubah `HorizontalAlignment = HorizontalAlignment.Left` dan `VerticalAlignment = VerticalAlignment.Top` | Beberapa organisasi lebih suka nomor di header daripada footer |
| **Font atau warna khusus** | Set `batesStamp.TextState.Font = FontRepository.FindFont("Arial"); batesStamp.TextState.FontSize = 12; batesStamp.TextState.ForegroundColor = Color.Red;` | Meningkatkan keterbacaan atau memenuhi pedoman merek |
| **Menambahkan PDF yang ada sebagai latar belakang** | Muat PDF sumber dengan `Document src = new Document("source.pdf"); pdfDocument.Pages.Add(src.Pages[1]);` | Berguna saat Anda perlu menempelkan stempel di atas formulir yang sudah dibuat |

## Penutup

Kami baru saja menunjukkan cara **membuat dokumen PDF**, **menambahkan PDF halaman kosong**, dan **menambahkan nomor Bates** menggunakan Aspose.Pdf untuk .NET, kemudian **menempatkan stempel pada halaman** dan menyimpan file. Kode dibuat sengaja ringkas agar Anda dapat menyesuaikannya dengan alur kerja yang lebih besar—baik saat memproses puluhan file sekaligus atau mengintegrasikannya ke layanan web.

Jika Anda siap melangkah lebih jauh, pertimbangkan:

- Mengotomatiskan logika peningkatan nomor untuk berkas kasus besar.
- Menyematkan pembuatan PDF ke dalam API ASP.NET Core.
- Menambahkan keamanan (proteksi password) dengan `pdfDocument.Encrypt(...)`.

Silakan bereksperimen, pecahkan masalah, dan ajukan pertanyaan di komentar. Selamat coding, semoga PDF Anda selalu tercapainya stempel yang sempurna!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}