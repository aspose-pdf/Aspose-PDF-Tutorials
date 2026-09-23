---
category: general
date: 2026-03-03
description: Cara memverifikasi instalasi paket NuGet di PowerShell. Pelajari cara
  menjalankan PowerShell sebagai admin, menginstal versi tertentu, dan mengelola paket
  secara efisien.
draft: false
keywords:
- how to verify installation
- install specific version
- run powershell as admin
- install nuget package powershell
- powershell package management
language: id
og_description: Cara memverifikasi instalasi paket NuGet di PowerShell. Panduan langkah
  demi langkah ini menunjukkan cara menjalankan PowerShell sebagai admin, menginstal
  versi tertentu, dan memastikan paket tersebut ada.
og_title: Cara Memverifikasi Instalasi Paket NuGet dengan PowerShell
tags:
- PowerShell
- NuGet
- Package Management
title: Cara Memverifikasi Instalasi Paket NuGet dengan PowerShell
url: /id/net/getting-started/how-to-verify-installation-of-a-nuget-package-with-powershel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Memverifikasi Instalasi Paket NuGet dengan PowerShell

Memverifikasi instalasi paket NuGet di PowerShell adalah tugas umum bagi admin Windows. Jika Anda pernah bertanya-tanya apakah paket tersebut benar‑benar terpasang di sistem Anda, panduan ini menunjukkan secara tepat cara memverifikasi instalasi—tanpa tebakan.  

Dalam beberapa menit ke depan kami akan membahas cara menjalankan PowerShell sebagai admin, mengambil versi tertentu dari sebuah paket, dan akhirnya memastikan bahwa paket tersebut ada di mesin Anda. Anda juga akan mendapatkan beberapa tips untuk **PowerShell package management** sehari‑hari yang membuat lingkungan Anda tetap rapi.  

Sebelum kita mulai, pastikan Anda memiliki mesin Windows dengan PowerShell 7 (atau Windows PowerShell 5.1) dan koneksi internet. Tidak diperlukan alat tambahan; semuanya berjalan langsung dari provider PackageManagement bawaan.

---

![Screenshot of an elevated PowerShell window with the Get-Package command](/images/verify-installation.png "Screenshot showing how to verify installation in an elevated PowerShell window")

## Langkah 1: Jalankan PowerShell sebagai Admin  

Menjalankan PowerShell dengan hak administratif adalah garis pertahanan pertama terhadap masalah terkait izin. Ketika Anda **menjalankan PowerShell sebagai admin**, cmdlet `Install-Package` dapat menulis ke folder Program Files dan mendaftarkan paket di katalog sistem‑luas.

```powershell
# Open an elevated session (manual step)
# Right‑click the PowerShell icon → Run as administrator
```

> **Pro tip:** Sematkan pintasan “Windows PowerShell (Admin)” ke taskbar Anda. Satu klik dan Anda siap.

### Mengapa elevasi penting  

Tanpa elevasi, `Install-Package` mungkin diam‑diam beralih ke lokasi berskala pengguna, yang kemudian dapat membingungkan `Get-Package` karena secara default ia mencari di ruang lingkup sistem. Dengan elevasi, paket akan muncul di tempat yang diharapkan kebanyakan skrip.

---

## Langkah 2: Instal Versi Spesifik dari Paket NuGet  

Seringkali Anda tidak menginginkan rilis terbaru melainkan versi yang sudah terbukti baik dan telah diuji pada proyek Anda. Pola **install specific version** menjadi sederhana dengan flag `-Version`.

```powershell
# Install Aspose.PDF version 25.3 from the PowerShell Gallery
Install-Package Aspose.PDF -Version 25.3 -ProviderName NuGet -Scope AllUsers -Force
```

### Memecah perintah  

| Parameter | Apa yang dilakukan | Mengapa Anda membutuhkannya |
|-----------|--------------------|----------------------------|
| `-Version 25.3` | Menetapkan nomor build yang tepat | Menjamin build yang dapat direproduksi |
| `-ProviderName NuGet` | Memberitahu PowerShell provider mana yang akan digunakan | Menghindari ambiguitas jika beberapa provider terdaftar |
| `-Scope AllUsers` | Menginstal untuk setiap akun di mesin | Berfungsi dengan kueri `Get-Package` berskala sistem |
| `-Force` | Menekan prompt (berguna dalam skrip) | Menjaga otomatisasi tetap lancar |

> **Watch out:** Jika Anda menghilangkan `-Version`, PowerShell akan mengambil paket terbaru, yang mungkin memperkenalkan perubahan yang merusak.

---

## Langkah 3: Verifikasi Instalasi  

Sekarang tiba saatnya menguji: **cara memverifikasi instalasi**. Cara paling langsung adalah meminta PowerShell menampilkan paket yang baru saja Anda instal.

```powershell
# Retrieve the package info
Get-Package -Name Aspose.PDF -ProviderName NuGet
```

Anda seharusnya melihat output serupa dengan:

```
Name           Version   Source   Summary
----           -------   ------   -------
Aspose.PDF    25.3      NuGet    .NET PDF library from Aspose
```

Jika perintah tidak menghasilkan apa‑apa, coba kueri berskala pengguna:

```powershell
Get-Package -Name Aspose.PDF -ProviderName NuGet -Scope CurrentUser
```

### Metode verifikasi alternatif  

1. **Periksa folder modul** – Paket disimpan di `C:\Program Files\PackageManagement\Packages\`. Cari folder bernama `Aspose.PDF.25.3`.  
2. **Gunakan `Find-Package`** – Ini mencari di repositori dan dapat mengonfirmasi versi tersedia:  

   ```powershell
   Find-Package -Name Aspose.PDF -ProviderName NuGet | Where-Object { $_.Version -eq '25.3' }
   ```

3. **Validasi dengan .NET** – Muat assembly di PowerShell untuk memastikan DLL dapat dimuat:  

   ```powershell
   Add-Type -Path "C:\Program Files\PackageManagement\Packages\Aspose.PDF.25.3\lib\netstandard2.0\Aspose.Pdf.dll"
   [Aspose.Pdf.License] | Get-Member
   ```

Jika salah satu pemeriksaan tersebut berhasil, Anda telah berhasil **memverifikasi instalasi**.

---

## Kesalahan Umum dan Cara Menghindarinya  

- **Missing NuGet provider** – Jalankan `Install-PackageProvider -Name NuGet -Force` terlebih dahulu.  
- **ExecutionPolicy blocks** – Secara sementara atur `Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass` untuk sesi tersebut.  
- **Network proxy issues** – Gunakan parameter `-Proxy` dan `-ProxyCredential` jika lingkungan Anda berada di belakang proxy perusahaan.  
- **Version conflicts** – Ketika ada beberapa versi, tentukan `-RequiredVersion` dalam `Get-Package` untuk menghilangkan ambiguitas.

---

## Menggabungkan Semua – Skrip Lengkap  

Berikut adalah skrip siap‑jalankan yang menggabungkan tiga langkah, menyertakan penanganan error, dan mencetak pesan keberhasilan yang ramah.

```powershell
<# 
.SYNOPSIS
    Installs a specific version of a NuGet package and verifies the installation.
.DESCRIPTION
    Demonstrates how to run PowerShell as admin, install a specific version, 
    and confirm that the package is present using Get-Package.
#>

# Ensure we are running elevated
if (-not ([Security.Principal.WindowsPrincipal] `
        [Security.Principal.WindowsIdentity]::GetCurrent()).IsInRole(`
        [Security.Principal.WindowsBuiltInRole]::Administrator)) {
    Write-Warning "Please run this script in an elevated PowerShell session."
    exit 1
}

$packageName = 'Aspose.PDF'
$packageVersion = '25.3'

try {
    Write-Host "Installing $packageName version $packageVersion..."
    Install-Package $packageName -Version $packageVersion `
        -ProviderName NuGet -Scope AllUsers -Force -ErrorAction Stop

    Write-Host "Installation completed. Verifying..."
    $pkg = Get-Package -Name $packageName -ProviderName NuGet -ErrorAction Stop

    if ($pkg.Version -eq $packageVersion) {
        Write-Host "`n✅ Successfully verified installation of $packageName $packageVersion."
    } else {
        Write-Error "Version mismatch: Expected $packageVersion but got $($pkg.Version)."
    }
}
catch {
    Write-Error "An error occurred: $_"
}
```

Menjalankan skrip menghasilkan baris jelas “✅ Successfully verified installation…” yang mengonfirmasi bahwa **cara memverifikasi instalasi** berfungsi dari awal hingga akhir.

---

## Kesimpulan  

Anda kini tahu **cara memverifikasi instalasi** paket NuGet apa pun menggunakan PowerShell, mulai dari meluncurkan sesi yang ditingkatkan, menginstal versi yang ditargetkan, hingga akhirnya memastikan keberadaan paket tersebut. Menguasai langkah‑langkah ini memberi Anda kepercayaan pada alur kerja **PowerShell package management** Anda dan mencegah sakit kepala “terlihat terinstal tetapi tidak” yang sering mengganggu pengembang Windows.

Apa selanjutnya? Cobalah mengganti `Aspose.PDF` dengan pustaka lain, bereksperimen dengan `-Scope CurrentUser`, atau menulis skrip instalasi massal beberapa paket untuk workstation baru. Dan jika Anda menemui keanehan, ingatlah tips pemecahan masalah di atas—terutama pemeriksaan provider dan execution‑policy.

Selamat menulis skrip, semoga instalasi Anda selalu dapat diverifikasi!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}