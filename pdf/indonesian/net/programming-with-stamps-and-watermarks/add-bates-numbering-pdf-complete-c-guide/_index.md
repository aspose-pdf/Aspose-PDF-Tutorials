---
category: general
date: 2026-02-14
description: Tambahkan penomoran Bates PDF ke dokumen Anda dengan mudah. Pelajari
  cara menambahkan nomor halaman di footer dan menambahkan nomor berurutan pada PDF
  dengan Aspose.Pdf dalam hitungan menit.
draft: false
keywords:
- add bates numbering pdf
- add footer page numbers
- how to add bates numbers
- add sequential numbers pdf
language: id
og_description: Tambahkan penomoran Bates pada PDF dengan cepat. Panduan ini menunjukkan
  cara menambahkan nomor halaman footer dan nomor berurutan pada PDF menggunakan Aspose.Pdf,
  lengkap dengan kode lengkap dan tips.
og_title: Menambahkan Penomoran Bates pada PDF – Tutorial C# Langkah demi Langkah
tags:
- Aspose.Pdf
- C#
- PDF automation
title: Menambahkan Penomoran Bates pada PDF – Panduan Lengkap C#
url: /id/net/programming-with-stamps-and-watermarks/add-bates-numbering-pdf-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tambahkan Penomoran Bates PDF – Panduan Lengkap C#

Pernahkah Anda perlu **menambahkan penomoran Bates PDF** tetapi tidak yakin harus mulai dari mana? Anda tidak sendirian. Tim hukum, auditor, dan siapa pun yang menangani kumpulan dokumen besar terus bertanya, “Bagaimana cara menambahkan nomor Bates tanpa merusak tata letak?” Kabar baiknya, dengan Aspose.Pdf untuk .NET Anda dapat menyisipkan nomor tersebut sebagai footer sederhana—tanpa perlu penyuntingan manual.

Dalam tutorial ini kami akan membahas solusi praktis end‑to‑end yang tidak hanya **menambahkan nomor halaman footer** tetapi juga memungkinkan Anda **menambahkan nomor berurutan PDF** dengan awalan khusus, ukuran font, dan perataan. Pada akhir tutorial Anda akan memiliki program C# siap‑jalankan, pemahaman yang jelas mengapa setiap pengaturan penting, serta beberapa tips profesional untuk menghindari jebakan paling umum.

## Apa yang Akan Anda Pelajari

- Cara memuat PDF yang ada dan menyiapkannya untuk penomoran Bates.  
- Properti **BatesNumberingOptions** mana yang mengontrol tampilan dan penempatan.  
- Cara menerapkan penomoran ke setiap halaman dalam satu panggilan.  
- Cara menyesuaikan awalan, nomor mulai, dan margin untuk berbagai format hukum.  
- Penanganan kasus tepi—apa yang harus dilakukan dengan PDF terenkripsi atau dokumen yang sudah berisi footer.

**Prasyarat**: .NET 6+ (atau .NET Framework 4.7+), versi terbaru Aspose.Pdf (contoh menggunakan 23.10), dan PDF input yang Anda memiliki hak untuk memodifikasinya. Tidak diperlukan pustaka pihak ketiga lainnya.

---

## Langkah 1 – Muat PDF yang Ingin Anda Nomori

Hal pertama yang kita lakukan adalah membuat instance `Document` yang menunjuk ke file sumber. Menggunakan pola `using var` memastikan handle file dilepaskan secara otomatis.

```csharp
using Aspose.Pdf;

// Replace with the path to your source PDF
using var doc = new Document("YOUR_DIRECTORY/input.pdf");
```

> **Mengapa ini penting:** Aspose.Pdf membaca seluruh struktur PDF ke dalam memori, memungkinkan kami memanipulasi halaman, anotasi, dan metadata tanpa menyentuh file asli di disk. Jika PDF dilindungi kata sandi, Anda dapat mengirimkan kata sandi ke konstruktor—lihat catatan “PDF terenkripsi” di akhir.

---

## Langkah 2 – Tentukan Opsi Penomoran Bates Anda

Nomor Bates pada dasarnya adalah footer halaman dengan awalan yang dapat dikonfigurasi dan penghitung berurutan. Kelas `BatesNumberingOptions` memungkinkan Anda menyesuaikan setiap aspek visual.

```csharp
var batesOptions = new BatesNumberingOptions
{
    // The text that will appear before the numeric part
    Prefix = "ABC-",

    // Starting number; the library will increment this automatically
    StartNumber = 1000,

    // Font size of the footer text (points)
    FontSize = 12,

    // Align the number to the right side of the page
    HorizontalAlignment = HorizontalAlignment.Right,

    // Place the number at the bottom of the page
    VerticalAlignment = VerticalAlignment.Bottom,

    // Margins: left, top, right, bottom (in points)
    Margin = new MarginInfo(0, 20, 0, 0)
};
```

### Tips Cepat

- **Prefix**: Gunakan identifier pendek dan unik (misalnya nomor kasus) agar footer tetap dapat dibaca.  
- **StartNumber**: Firma hukum sering memulai dari `1` atau offset khusus; pilih yang sesuai dengan sistem pengarsipan Anda.  
- **Margins**: Margin bawah `20` poin menjaga teks tetap jelas dari catatan kaki atau tanda tangan yang mungkin sudah berada di dekat tepi halaman.

---

## Langkah 3 – Terapkan Penomoran ke Semua Halaman

Dengan opsi yang dikonfigurasi, penyisipan sebenarnya hanya satu baris kode. Aspose.Pdf menangani paginasi, memperbarui aliran konten yang ada, dan menghormati rotasi halaman secara otomatis.

```csharp
doc.Pages.AddBatesNumbering(batesOptions);
```

> **Apa yang terjadi di balik layar?** Perpustakaan mengiterasi setiap objek `Page`, membuat `TextFragment` yang menggabungkan awalan dan penghitung saat ini, kemudian menggambarnya menggunakan sistem koordinat halaman. Karena kami mengatur `HorizontalAlignment.Right` dan `VerticalAlignment.Bottom`, teks akan menempel di sudut kanan‑bawah terlepas dari ukuran halaman.

---

## Langkah 4 – Simpan PDF yang Dimodifikasi

Akhirnya, tulis hasilnya ke file baru. Menimpa file asli memungkinkan, tetapi menyimpan salinan membantu dalam kontrol versi.

```csharp
doc.Save("YOUR_DIRECTORY/output.pdf");
```

Jika Anda perlu mempertahankan metadata asli (penulis, tanggal pembuatan), Aspose.Pdf menyalinnya secara default. Anda juga dapat menentukan objek `SaveOptions` untuk kepatuhan PDF/A atau kompresi.

---

## Contoh Lengkap yang Berfungsi

Berikut adalah program lengkap yang siap dijalankan. Tempelkan ke dalam proyek aplikasi konsol, sesuaikan jalur file, dan tekan **F5**.

```csharp
using Aspose.Pdf;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source PDF
        using var doc = new Document("YOUR_DIRECTORY/input.pdf");

        // 2️⃣ Configure Bates numbering options
        var batesOptions = new BatesNumberingOptions
        {
            Prefix = "ABC-",
            StartNumber = 1000,
            FontSize = 12,
            HorizontalAlignment = HorizontalAlignment.Right,
            VerticalAlignment = VerticalAlignment.Bottom,
            Margin = new MarginInfo(0, 20, 0, 0)
        };

        // 3️⃣ Apply numbering to every page
        doc.Pages.AddBatesNumbering(batesOptions);

        // 4️⃣ Save the output PDF
        doc.Save("YOUR_DIRECTORY/output.pdf");

        System.Console.WriteLine("Bates numbering added successfully!");
    }
}
```

**Hasil yang diharapkan:** Setiap halaman `output.pdf` kini menampilkan footer seperti `ABC-1000`, `ABC-1001`, … yang ditempatkan di sudut kanan‑bawah. Buka file tersebut di pembaca PDF apa pun untuk memverifikasi.

---

## Menangani Variasi Umum

### Menambahkan Hanya Nomor Halaman Footer

Jika Anda hanya membutuhkan nomor halaman sederhana tanpa awalan, atur `Prefix = ""` dan mungkin sesuaikan margin untuk menghindari benturan dengan footer yang sudah ada.

```csharp
batesOptions.Prefix = "";
batesOptions.StartNumber = 1; // classic page numbering
```

### Menggunakan Perataan yang Berbeda

Dokumen hukum kadang‑kadang memerlukan nomor yang ditempatkan di tengah bagian bawah. Ganti perataannya:

```csharp
batesOptions.HorizontalAlignment = HorizontalAlignment.Center;
```

### Menangani PDF yang Terenkripsi

Ketika PDF sumber dilindungi kata sandi, berikan kata sandi seperti ini:

```csharp
using var doc = new Document("secure.pdf", new LoadOptions { Password = "mySecret" });
```

Sisa alur kerja tetap sama.

### Melewati Footer yang Sudah Ada

Jika sebuah dokumen sudah berisi footer yang tidak ingin Anda timpa, Anda dapat menambahkan string khusus di depan yang membuat nomor baru menjadi berbeda, atau Anda dapat mengiterasi halaman secara manual dan menambahkan `TextFragment` hanya pada tempat yang tidak memiliki footer. Kelas `Page` pada perpustakaan menyediakan koleksi `Annotations` dan `Contents` untuk kontrol yang lebih detail.

---

## Tips Profesional & Jebakan

- **Hindari pemotongan**: Margin bawah yang sangat kecil dapat menyebabkan teks terpotong pada printer. Uji dengan cetakan fisik jika Anda akan mendistribusikan salinan cetak.  
- **Kinerja**: Menambahkan nomor Bates ke PDF 500‑halaman memakan kurang dari satu detik pada laptop modern, tetapi batch besar mendapat manfaat dari pemrosesan paralel—ingat bahwa `Document` tidak thread‑safe, sehingga setiap thread memerlukan instance‑nya sendiri.  
- **Kompatibilitas versi**: Kode ini bekerja dengan Aspose.Pdf 23.10 dan yang lebih baru. Jika Anda menggunakan versi lebih lama, nama properti tetap sama tetapi konstruktor `MarginInfo` mungkin memerlukan argumen `float`.  
- **Kepatuhan hukum**: Beberapa yurisdiksi mengharuskan nomor Bates ditempatkan di lokasi tertentu (mis., kiri‑bawah). Sesuaikan `HorizontalAlignment` sesuai kebutuhan.  

---

## Kesimpulan

Kami baru saja mendemonstrasikan cara **menambahkan penomoran Bates PDF** menggunakan Aspose.Pdf untuk .NET, mencakup semua mulai dari memuat dokumen hingga menyimpan versi akhir dengan footer yang bersih. Dengan menyesuaikan beberapa properti, Anda juga dapat **menambahkan nomor halaman footer**, **menambahkan nomor berurutan PDF**, atau menyesuaikan tampilan untuk memenuhi standar hukum apa pun.

Siap untuk langkah selanjutnya? Cobalah menggabungkan teknik ini dengan ekstraksi teks OCR untuk menyematkan kata kunci yang dapat dicari bersama nomor Bates Anda, atau otomatisasi proses untuk seluruh folder menggunakan `Directory.GetFiles`. Kemungkinannya tak terbatas, dan fondasi yang kini Anda miliki akan membuat ekstensi tersebut menjadi mudah.

Selamat coding, semoga PDF Anda selalu bernomor dengan sempurna!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}