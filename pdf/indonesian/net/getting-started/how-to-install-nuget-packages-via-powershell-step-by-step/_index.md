---
category: general
date: 2026-02-20
description: Pelajari cara menginstal paket NuGet menggunakan PowerShell, jalankan
  PowerShell sebagai admin, daftar paket yang terinstal, dan verifikasi paket yang
  terinstal dalam hitungan menit.
draft: false
keywords:
- how to install nuget
- run powershell as admin
- list installed packages
- how to verify package
- verify installed package
language: id
og_description: cara menginstal paket NuGet menggunakan PowerShell, menjalankan PowerShell
  sebagai admin, menampilkan daftar paket yang terinstal, dan memverifikasi paket
  yang terinstal—panduan lengkap.
og_title: Cara menginstal paket NuGet melalui PowerShell – panduan cepat
tags:
- PowerShell
- NuGet
- Package Management
title: cara menginstal paket NuGet melalui PowerShell – langkah demi langkah
url: /id/net/getting-started/how-to-install-nuget-packages-via-powershell-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# cara menginstal paket nuget via PowerShell – langkah demi langkah

Pernah bertanya-tanya **bagaimana cara menginstal nuget** paket tanpa membuka Visual Studio? Anda tidak sendirian. Dalam banyak pipeline CI atau pada mesin baru, cara tercepat adalah masuk ke PowerShell—sebaiknya *run powershell as admin*—dan biarkan package manager melakukan tugasnya.

Dalam tutorial ini kami akan membahas seluruh proses: membuka konsol yang tepat, mengunduh versi spesifik dari sebuah library, dan akhirnya mengonfirmasi bahwa paket benar‑benar terpasang di sistem Anda. Pada akhir tutorial Anda akan dapat **list installed packages**, mengetahui **how to verify package** integritas, dan merasa yakin bahwa langkah **verify installed package** berhasil setiap saat.

## Apa yang akan Anda pelajari

- Cara meluncurkan PowerShell dengan hak istimewa yang tepat.  
- Sintaks perintah `Install-Package` yang tepat untuk NuGet.  
- Cara **list installed packages** dan mengonfirmasi nomor versi.  
- Kesulitan umum (hak admin yang hilang, ketidaksesuaian versi) dan cara menghindarinya.  

Tidak diperlukan pengalaman sebelumnya dengan NuGet, hanya diperlukan mesin Windows yang berfungsi dan sedikit rasa ingin tahu.

---

## Cara Menginstal Paket NuGet Menggunakan PowerShell

> **Pro tip:** Jika Anda sering menambahkan paket yang sama, pertimbangkan untuk menambahkannya ke file skrip dan menjalankannya dengan `-File`. Ini menghemat Anda dari mengetik baris yang sama berulang‑ulang.

### Langkah 1: Buka PowerShell dengan izin yang diperlukan

Hal pertama yang harus Anda lakukan adalah **run powershell as admin**. Tanpa hak istimewa, cmdlet `Install-Package` dapat gagal secara diam‑diam atau meminta konfirmasi yang tidak ingin Anda tangani.

1. Klik tombol Start.  
2. Ketik **PowerShell**.  
3. Klik kanan *Windows PowerShell* dan pilih **Run as administrator**.  

Anda akan melihat prompt UAC; klik **Yes**. Sekarang Anda memiliki sesi dengan hak istimewa siap untuk instalasi paket.

> *Mengapa admin?*  
> NuGet menulis file ke folder paket global (`C:\Program Files\PackageManagement\NuGet\Packages` secara default). Lokasi itu dilindungi, sehingga hanya proses dengan hak istimewa yang dapat menulis di sana.

### Langkah 2: Instal paket NuGet yang diinginkan beserta versinya

With the console open, the core command is straightforward:

```powershell
# Install the Aspose.PDF library, version 25.3
Install-Package Aspose.PDF -Version 25.3
```

- `Install-Package` adalah pembungkus PowerShell di sekitar klien NuGet.  
- `-Version` mengunci build tepat yang Anda butuhkan, mencegah peningkatan tidak sengaja.  

Jika Anda menghilangkan `-Version`, PowerShell akan mengambil rilis stabil terbaru—kadang itu baik, kadang Anda menginginkan versi tepat yang Anda uji.

#### Apa yang terjadi di balik layar?

PowerShell menghubungi sumber paket yang dikonfigurasi (secara default `https://www.nuget.org/api/v2`) dan mengunduh file `.nupkg`. Kemudian ia mengekstrak DLL ke dalam folder paket global dan mendaftarkan paket dengan penyedia paket lokal. Seluruh proses biasanya selesai dalam beberapa detik kecuali Anda berada pada jaringan yang lambat.

### Langkah 3: Verifikasi bahwa paket berhasil diinstal

Sekarang paket sudah berada di disk, Anda mungkin bertanya, **“Bagaimana cara memverifikasi paket?”** Jawabannya ada dalam kueri sederhana:

```powershell
# List all installed NuGet packages
Get-Package -Name Aspose.PDF
```

Menjalankan ini mengembalikan sesuatu seperti:

```
Name        Version   Source
----        -------   ------
Aspose.PDF  25.3      nuget.org
```

Output tersebut mengonfirmasi dua hal:

1. Paket **Aspose.PDF** ada.  
2. Versinya cocok dengan yang Anda minta, memenuhi persyaratan **verify installed package**.

Jika Anda ingin melihat *setiap* paket di mesin, hilangkan filter `-Name`:

```powershell
Get-Package | Where-Object {$_.ProviderName -eq 'NuGet'}
```

Tampilan **list installed packages** ini berguna untuk audit atau ketika Anda perlu membersihkan pustaka lama.

### Langkah 4: Opsional – menangani kasus tepi

#### a) Paket tidak ditemukan atau versi tidak cocok

Jika PowerShell membalas dengan *“Package not found”* atau *“Version not available”*, periksa kembali ejaan dan nomor versi. NuGet tidak sensitif huruf besar/kecil, tetapi spasi yang tidak diinginkan akan merusak perintah.

```powershell
# Search the NuGet feed for available versions
Find-Package Aspose.PDF -AllVersions
```

#### b) Menjalankan tanpa hak admin

Jika Anda lupa **run powershell as admin**, cmdlet akan melemparkan error izin. Solusinya cukup menutup jendela dan membukanya kembali dengan hak istimewa—tidak perlu menginstal ulang apa pun.

#### c) Menggunakan sumber khusus

Di lingkungan korporat Anda mungkin memiliki feed NuGet internal:

```powershell
Install-Package MyCompany.Logging -Source https://nuget.mycompany.local/api/v2
```

Langkah verifikasi tetap sama; cukup ingat untuk menyertakan `-Source` saat Anda menginstal.

---

## Tabel referensi cepat

| Action                              | PowerShell command                                          | Why it matters |
|-------------------------------------|-------------------------------------------------------------|----------------|
| Buka konsol dengan hak istimewa     | *Run PowerShell as Administrator*                           | Diperlukan untuk instalasi global |
| Instal versi spesifik               | `Install-Package <pkg> -Version <x.y.z>`                    | Menjamin build yang dapat direproduksi |
| Daftar satu paket                   | `Get-Package -Name <pkg>`                                    | Mengonfirmasi **how to verify package** |
| Daftar semua paket NuGet            | `Get-Package | Where-Object {$_.ProviderName -eq 'NuGet'}`| Berguna untuk **list installed packages** |
| Cari versi yang tersedia            | `Find-Package <pkg> -AllVersions`                           | Membantu ketika versi tidak diketahui |

---

## Kesimpulan

Kami telah membahas **how to install nuget** paket menggunakan PowerShell dari awal hingga akhir—membuka konsol **run powershell as admin**, mengunduh versi spesifik, dan akhirnya **list installed packages** untuk **verify installed package**. Dengan perintah ini di kotak peralatan Anda, Anda dapat mengotomatisasi manajemen pustaka pada mesin Windows mana pun, baik Anda menulis skrip pipeline CI atau sekadar memperbaiki DLL yang hilang di kotak pengembangan Anda.

Langkah selanjutnya? Coba tambahkan beberapa paket ke dalam satu skrip, jelajahi parameter `-Scope` untuk menginstal secara lokal untuk sebuah proyek, atau gabungkan perintah ini dengan `Invoke-Expression` untuk membuat installer ringan bagi tim Anda. Dan jika Anda menemui kendala, ingat langkah **how to verify package**—melihat versi di `Get-Package` seringkali menjadi cara tercepat untuk menemukan masalah.

Selamat bersenang‑senang dengan PowerShell! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}