---
category: general
date: 2026-04-25
description: Iterasi koleksi C# dengan cepat menggunakan contoh loop foreach yang
  jelas. Pelajari cara mendapatkan nama objek dan menampilkan daftar string dalam
  beberapa langkah saja.
draft: false
keywords:
- iterate collection c#
- loop over items
- foreach loop example
- get object names
- display string list
language: id
og_description: Iterasi koleksi C# menggunakan contoh loop foreach. Temukan cara mendapatkan
  nama objek dan menampilkan daftar string secara efisien.
og_title: Iterasi Koleksi C# – Langkah demi Langkah Mengulang Item
tags:
- C#
- collections
- loops
title: Iterasi Koleksi C# – Panduan Sederhana untuk Mengulang Item
url: /id/net/programming-with-operators/iterate-collection-c-simple-guide-to-loop-over-items/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Iterate Collection C# – Cara Mengulang Item dengan Contoh Loop Foreach

Pernah perlu **iterate collection C#** tetapi tidak yakin konstruk apa yang memberi kode paling bersih? Anda tidak sendirian. Dalam banyak proyek kami berakhir menulis loop `for` yang bertele‑tele hanya untuk mencetak beberapa string—membuang waktu dan mengurangi keterbacaan. Kabar baik? Satu loop `foreach` saja dapat mengambil setiap nama dari sebuah objek dan **display string list** dalam hitungan detik.

Dalam tutorial ini kami akan membahas contoh lengkap yang dapat dijalankan yang menunjukkan cara **get object names**, mengulang item, dan menampilkannya ke konsol. Pada akhir tutorial Anda akan memiliki potongan kode mandiri yang dapat disisipkan ke aplikasi konsol .NET 6+ mana pun, plus beberapa tips untuk kasus tepi dan kinerja.

> **Tip pro:** Jika Anda bekerja dengan koleksi besar, pertimbangkan menggunakan `Parallel.ForEach`—tetapi itu topik untuk lain waktu.

---

## Apa yang Akan Anda Pelajari

- Cara mengambil koleksi nama dari sebuah objek (`GetSignatureNames` dalam contoh kami)
- Sintaks dan nuansa **foreach loop example** dalam C#
- Cara **display string list** di konsol, termasuk trik pemformatan
- Jebakan umum saat mengulang item (koleksi null, hasil kosong)
- Program lengkap siap salin‑tempel yang dapat langsung dijalankan

Tidak diperlukan pustaka eksternal; hanya pustaka kelas dasar yang disertakan dengan .NET. Jika Anda sudah menginstal .NET SDK, Anda siap mulai.

---

![Diagram iterate collection C# yang menunjukkan daftar mengalir ke loop foreach dan kemudian ke konsol](/images/iterate-collection-csharp.png "diagram iterate collection c#")

---

## Langkah 1: Siapkan Objek Contoh

Hal pertama yang perlu dilakukan—kita butuh objek yang dapat mengembalikan koleksi nama. Bayangkan Anda memiliki kelas `Signature` yang menyimpan beberapa tanda tangan; setiap tanda tangan memiliki properti `Name`. Metode `GetSignatureNames` cukup mengekstrak nama‑nama tersebut ke dalam `IEnumerable<string>`.

```csharp
using System;
using System.Collections.Generic;
using System.Linq;

namespace IterateCollectionDemo
{
    // A minimal representation of the object you might be working with
    public class Signature
    {
        private readonly List<string> _names = new()
        {
            "Alice Johnson",
            "Bob Smith",
            "Charlie Davis"
        };

        // This method mimics the real‑world API that returns a collection of names
        public IEnumerable<string> GetSignatureNames()
        {
            // Using LINQ to return a read‑only IEnumerable<string>
            return _names.AsReadOnly();
        }
    }
}
```

**Mengapa ini penting:** Dengan mengembalikan `IEnumerable<string>` kami menjaga metode tetap fleksibel—pemanggil dapat menelusuri, melakukan query, atau mengonversi hasil tanpa menyalin daftar yang mendasarinya. Ini juga memudahkan **loop over items** nanti.

---

## Langkah 2: Tulis Loop Foreach untuk Menampilkan String List

Sekarang kita memiliki sumber nama, mari **iterate collection C#**. Konstruk `foreach` secara otomatis mengambil setiap elemen dari enumerable, sehingga kita tidak perlu mengelola variabel indeks.

```csharp
using System;

namespace IterateCollectionDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Instantiate the object that holds our signatures
            var signature = new Signature();

            // Step 2: Retrieve the collection of signature names from the signature object
            var signatureNames = signature.GetSignatureNames();

            // Step 3: Loop over items and output each name to the console
            foreach (var name in signatureNames)
            {
                Console.WriteLine(name);
            }

            // Keep the console window open when debugging locally
            Console.WriteLine("\nPress any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**Penjelasan kode:**

1. **Instantiate** `Signature` – Anda kini memiliki objek yang mengetahui nama‑namanya sendiri.
2. **Retrieve** koleksi melalui `GetSignatureNames()` – ini adalah langkah **get object names**.
3. **Foreach loop example** – `foreach (var name in signatureNames)` otomatis mengiterasi setiap string.
4. **Display** setiap `name` dengan `Console.WriteLine` – cara klasik untuk **display string list** dalam aplikasi konsol.

Karena `signatureNames` mengimplementasikan `IEnumerable<string>`, loop `foreach` bekerja langsung, menangani enumerator di balik layar. Tidak perlu khawatir tentang kesalahan off‑by‑one atau pengecekan batas manual.

---

## Langkah 3: Jalankan Program dan Verifikasi Output

Kompilasi dan jalankan program (misalnya `dotnet run` dari folder proyek). Anda akan melihat:

```
Alice Johnson
Bob Smith
Charlie Davis

Press any key to exit...
```

Jika tidak ada yang tercetak, periksa kembali bahwa `GetSignatureNames` tidak mengembalikan `null`. Penjagaan defensif singkat dapat menyelamatkan Anda dari sakit kepala:

```csharp
var signatureNames = signature.GetSignatureNames() ?? Enumerable.Empty<string>();
```

Sekarang loop akan menangani koleksi yang hilang dengan anggun dan hanya tidak menghasilkan apa‑apa alih‑alih melempar `NullReferenceException`.

---

## Langkah 4: Variasi Umum & Kasus Tepi

### 4.1 Mengulang Daftar Objek Kompleks

Seringkali Anda tidak berurusan dengan string biasa melainkan objek yang berisi beberapa properti. Dalam kasus itu Anda tetap dapat **loop over items** dan memutuskan apa yang akan ditampilkan:

```csharp
foreach (var sig in signature.GetAllSignatures())
{
    Console.WriteLine($"{sig.Id}: {sig.Name}");
}
```

Di sini kami menggunakan interpolasi string untuk menggabungkan bidang—masih `foreach` loop, hanya output yang lebih kaya.

### 4.2 Keluar Lebih Awal dengan `break`

Jika Anda hanya membutuhkan nama yang pertama cocok, keluar dari loop dengan `break`:

```csharp
foreach (var name in signatureNames)
{
    if (name.StartsWith("B"))
    {
        Console.WriteLine(name);
        break; // stops after the first B‑name
    }
}
```

### 4.3 Enumerasi Paralel (Lanjutan)

Ketika koleksi sangat besar dan setiap iterasi memakan CPU secara intensif, `Parallel.ForEach` dapat mempercepat proses:

```csharp
System.Threading.Tasks.Parallel.ForEach(signatureNames, name =>
{
    // Simulate work
    Console.WriteLine(name);
});
```

Ingat, `Console.WriteLine` sendiri thread‑safe tetapi urutan output akan nondeterministik.

---

## Langkah 5: Tips untuk Loop yang Bersih dan Mudah Dipelihara

- **Prefer `foreach` over `for`** ketika Anda tidak memerlukan indeks; ini mengurangi bug off‑by‑one.
- **Gunakan `IEnumerable<T>`** dalam tanda tangan metode untuk menjaga API tetap fleksibel.
- **Guard against null** koleksi dengan operator null‑coalescing (`??`).
- **Keep the loop body small**—jika Anda menemukan diri menulis banyak baris, ekstrak menjadi metode terpisah.
- **Avoid modifying the collection** saat iterasi; hal itu akan melempar `InvalidOperationException`.

---

## Kesimpulan

Kami baru saja mendemonstrasikan cara **iterate collection C#** menggunakan contoh **foreach loop example** yang bersih, mengambil **object names**, dan **display string list** di konsol. Program lengkap—definisi objek, pengambilan, dan iterasi—bisa dijalankan apa adanya, memberi Anda fondasi kuat untuk skenario apa pun yang memerlukan pengulangan item.

Dari sini Anda dapat mengeksplorasi:

- Penyaringan dengan LINQ sebelum looping (`signatureNames.Where(n => n.Contains("a"))`)
- Menulis output ke file alih‑alih konsol
- Menggunakan `IAsyncEnumerable<T>` untuk aliran asynchronous

Cobalah, dan Anda akan melihat betapa fleksibelnya konstruk `foreach`. Ada pertanyaan tentang kasus tepi atau kinerja? Tinggalkan komentar di bawah, dan selamat coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}