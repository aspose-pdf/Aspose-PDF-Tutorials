---
category: general
date: 2026-03-03
description: PowerShell'de bir NuGet paketinin kurulumunu nasıl doğrularsınız. PowerShell'i
  yönetici olarak çalıştırmayı, belirli bir sürümü kurmayı ve paketleri verimli bir
  şekilde yönetmeyi öğrenin.
draft: false
keywords:
- how to verify installation
- install specific version
- run powershell as admin
- install nuget package powershell
- powershell package management
language: tr
og_description: PowerShell'de bir NuGet paketinin kurulumunu nasıl doğrularsınız.
  Bu adım adım rehber, PowerShell'i yönetici olarak nasıl çalıştıracağınızı, belirli
  bir sürümü nasıl kuracağınızı ve paketin mevcut olduğunu nasıl onaylayacağınızı
  gösterir.
og_title: PowerShell ile bir NuGet paketinin kurulumunu nasıl doğrularsınız
tags:
- PowerShell
- NuGet
- Package Management
title: PowerShell ile bir NuGet Paketi Kurulumunu Nasıl Doğrularsınız
url: /tr/net/getting-started/how-to-verify-installation-of-a-nuget-package-with-powershel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# NuGet Paketi Kurulumunu PowerShell ile Doğrulama

PowerShell'de bir NuGet paketinin kurulumunu doğrulamak, Windows yöneticileri için yaygın bir görevdir. Paketin gerçekten sisteminize gelip gelmediğini hiç merak ettiyseniz, bu rehber size kurulumun nasıl doğrulanacağını tam olarak gösterir—tahmine gerek kalmaz.  

Önümüzdeki birkaç dakikada PowerShell'i yönetici olarak çalıştırmayı, bir paketin belirli bir sürümünü indirmeyi ve sonunda paketin makinenizde mevcut olduğunu doğrulamayı adım adım göstereceğiz. Ayrıca ortamınızı düzenli tutan günlük **PowerShell package management** için birkaç ipucu da öğreneceksiniz.  

Başlamadan önce, PowerShell 7 (veya Windows PowerShell 5.1) yüklü bir Windows makineniz ve internet bağlantınız olduğundan emin olun. Ekstra bir araç gerekmez; her şey yerleşik PackageManagement sağlayıcısından çalışır.

---

![Yükseltilmiş bir PowerShell penceresinin Get-Package komutuyla ekran görüntüsü](/images/verify-installation.png "Yükseltilmiş bir PowerShell penceresinde kurulumun nasıl doğrulanacağını gösteren ekran görüntüsü")

## Adım 1: PowerShell'i Yönetici Olarak Çalıştırın  

PowerShell'i yönetici haklarıyla çalıştırmak, izinle ilgili aksaklıklara karşı ilk savunma hattıdır. **PowerShell'i yönetici olarak çalıştırdığınızda**, `Install-Package` cmdlet'i Program Files klasörüne yazabilir ve paketi sistem çapında katalogda kaydedebilir.

```powershell
# Open an elevated session (manual step)
# Right‑click the PowerShell icon → Run as administrator
```

> **Pro tip:** “Windows PowerShell (Admin)” kısayolunu görev çubuğunuza sabitleyin. Tek bir tıklama ile hazırsınız.

### Yükseltmenin önemi  

Yükseltme olmadan, `Install-Package` sessizce kullanıcı‑kapsamlı bir konuma geri dönebilir; bu da `Get-Package`'ı varsayılan olarak sistem kapsamına baktığı için yanıltabilir. Yükseltme, paketin çoğu betiğin beklediği yerde görünmesini garanti eder.

---

## Adım 2: NuGet Paketinin Belirli Bir Sürümünü Yükleyin  

Çoğu zaman en son sürümü değil, projenizin test edildiği bilinen bir sürümü istersiniz. **Belirli sürümü yükleme** deseni, `-Version` bayrağıyla oldukça basittir.  

```powershell
# Install Aspose.PDF version 25.3 from the PowerShell Gallery
Install-Package Aspose.PDF -Version 25.3 -ProviderName NuGet -Scope AllUsers -Force
```

### Komutu Parçalara Ayırma  

| Parametre | Ne işe yarar | Neden gerekir |
|-----------|--------------|-----------------|
| `-Version 25.3` | Tam derleme numarasını sabitler | Tekrarlanabilir derlemeleri garanti eder |
| `-ProviderName NuGet` | PowerShell'e hangi sağlayıcının kullanılacağını söyler | Birden fazla sağlayıcı kayıtlıysa belirsizliği önler |
| `-Scope AllUsers` | Makinedeki her hesap için kurar | `Get-Package` sistem çapındaki sorgularıyla çalışır |
| `-Force` | İstemleri bastırır (betiklerde faydalıdır) | Otomasyonu sorunsuz tutar |

> **Dikkat:** `-Version`'ı atladığınızda, PowerShell en yeni paketi alır ve bu, kırıcı değişiklikler getirebilir.

---

## Adım 3: Kurulumu Doğrulama  

Şimdi gerçek an geliyor: **kurulumu nasıl doğrularsınız**. En doğrudan yol, PowerShell'den az önce yüklediğiniz paketi istemektir.

```powershell
# Retrieve the package info
Get-Package -Name Aspose.PDF -ProviderName NuGet
```

Aşağıdaki gibi bir çıktı görmelisiniz:

```
Name           Version   Source   Summary
----           -------   ------   -------
Aspose.PDF    25.3      NuGet    .NET PDF library from Aspose
```

Komut hiçbir şey döndürmezse, kullanıcı‑kapsamlı sorguyu deneyin:

```powershell
Get-Package -Name Aspose.PDF -ProviderName NuGet -Scope CurrentUser
```

### Alternatif doğrulama yöntemleri  

1. **Modül klasörünü kontrol edin** – Paketler `C:\Program Files\PackageManagement\Packages\` altında depolanır. `Aspose.PDF.25.3` adlı bir klasör arayın.  
2. **`Find-Package` kullanın** – Bu, depoyu arar ve sürümün mevcut olduğunu doğrulayabilir:  

   ```powershell
   Find-Package -Name Aspose.PDF -ProviderName NuGet | Where-Object { $_.Version -eq '25.3' }
   ```

3. **.NET ile doğrulayın** – DLL'nin yüklenebilir olduğunu teyit etmek için PowerShell'de assembly'i yükleyin:  

   ```powershell
   Add-Type -Path "C:\Program Files\PackageManagement\Packages\Aspose.PDF.25.3\lib\netstandard2.0\Aspose.Pdf.dll"
   [Aspose.Pdf.License] | Get-Member
   ```

Bu kontrollerden herhangi biri başarılı olursa, **kurulumu başarıyla doğrulamış** olursunuz.

---

## Yaygın Tuzaklar ve Nasıl Kaçınılır  

- **NuGet sağlayıcısı eksik** – Önce `Install-PackageProvider -Name NuGet -Force` komutunu çalıştırın.  
- **ExecutionPolicy engelleri** – Oturum için geçici olarak `Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass` ayarlayın.  
- **Ağ proxy sorunları** – Ortamınız kurumsal bir proxy arkasındaysa `-Proxy` ve `-ProxyCredential` parametrelerini kullanın.  
- **Sürüm çakışmaları** – Birden fazla sürüm mevcut olduğunda, `Get-Package` içinde `-RequiredVersion` belirterek ayrım yapın.

---

## Hepsini Bir Araya Getirme – Tam Bir Betik  

Aşağıda, üç adımı kapsayan, hata yönetimi içeren ve dostane bir başarı mesajı yazdıran hazır bir betik bulabilirsiniz.

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

Betik çalıştırıldığında, **kurulumu nasıl doğrularsınız** sürecinin baştan sona çalıştığını onaylayan “✅ Successfully verified installation…” satırı net bir şekilde görülür.

---

## Sonuç  

Artık PowerShell kullanarak herhangi bir NuGet paketinin **kurulumu nasıl doğrulanır** konusunda bilgi sahibisiniz; yükseltilmiş bir oturum başlatmaktan hedef bir sürümü yüklemeye ve sonunda paketin varlığını onaylamaya kadar. Bu adımları ustalıkla uygulamak, **PowerShell package management** iş akışınıza güven kazandırır ve Windows geliştiricilerini sık sık rahatsız eden “kurulu gibi görünüyor ama değil” sorunlarını önler.  

Sırada ne var? `Aspose.PDF` yerine başka bir kütüphane deneyin, `-Scope CurrentUser` ile oynayın veya yeni bir iş istasyonu için birden fazla paketi toplu olarak kuran bir betik yazın. Ve eğer tuhaflıklarla karşılaşırsanız, yukarıdaki sorun giderme ipuçlarını—özellikle sağlayıcı ve execution‑policy kontrollerini—hatırlayın.  

İyi betikler, ve kurulumlarınız her zaman doğrulanabilir olsun!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}