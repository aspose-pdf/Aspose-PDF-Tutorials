---
category: general
date: 2026-02-10
description: PowerShell kullanarak Aspose nasıl kurulur. PowerShell'i yönetici olarak
  çalıştırmayı, belirli bir sürümü kurmayı ve paketleri nasıl listeleyeceğinizi öğrenin.
draft: false
keywords:
- how to install aspose
- install specific version
- install nuget package powershell
- run powershell as administrator
- how to list packages
language: tr
og_description: PowerShell ile Aspose nasıl kurulur. Bu öğreticide PowerShell'i yönetici
  olarak çalıştırma, belirli bir sürümü kurma ve paketleri listeleme gösterilmektedir.
og_title: Aspose nasıl kurulur – PowerShell adım adım rehberi
tags:
- powershell
- nuget
- aspose
- devops
title: aspose nasıl kurulur – Belirli sürümler için PowerShell rehberi
url: /tr/net/getting-started/how-to-install-aspose-powershell-guide-for-specific-versions/
---

keep as is. In translation we wrote **run powershell as administrator** unchanged. Good.

Also "how to list packages" is a phrase; we kept unchanged.

Now produce final content with all markdown.

Let's assemble.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# aspose nasıl kurulur – PowerShell adım‑adım rehberi

Yeni bir Windows makinesinde **aspose nasıl kurulur** diye hiç merak ettiniz mi? Tek başınıza değilsiniz. Birçok .NET projesinde Aspose.PDF NuGet paketi PDF manipülasyonu için tercih edilen kütüphanedir, ancak kurulum adımı biraz belirsiz hissedebilir—özellikle belirli bir sürüme ihtiyacınız olduğunda veya kısıtlı bir sunucuda çalışıyorsanız.

İşte mesele: Aspose'yi saniyeler içinde PowerShell'den çalıştırabilirsiniz. Bu öğreticide doğru yetkilerle PowerShell'i başlatmayı, paketin belirli bir sürümünü çekmeyi ve kurulumu **how to list packages** ile doğrulamayı adım adım göstereceğiz. Sonunda CI betiklerine ekleyebileceğiniz tekrarlanabilir bir tek satır komuta sahip olacaksınız ve her bayrağın nedenini anlayacaksınız.

## Önkoşullar

- PowerShell 5.1+ yüklü Windows 10/11 (veya Windows Server).  
- NuGet beslemesine erişilebilmesi için internet bağlantısı.  
- Opsiyonel ama kullanışlı: **NuGet provider** (`Install-PackageProvider -Name NuGet -Force`) eğer hâlâ yüklü değilse.  
- Ortamınız paket kurulumunu sistem kapsamına sınırlıyorsa yönetici hakları.

Eğer bunlardan biri size yabancı geliyorsa endişelenmeyin—çoğu geliştirici makinesi zaten bu koşulları karşılar. Ayrıca **run powershell as administrator** adımını da ele alacağız, ihtiyacınız olursa.

## Adım 1: PowerShell'i uygun yetkilerle açın

> **Pro tip:** Kurumsal bir çalışma istasyonunda yürütme‑politika kısıtlamalarını aşmak için yükseltme yapmanız gerekebilir.

1. **Start**'a tıklayın, **PowerShell** yazın, sonucu sağ‑tıklayın ve **Run as administrator**'ı seçin.  
2. Kısayol yolunu tercih ediyorsanız `Win + X` tuşlarına basın → **Windows PowerShell (Admin)**.

```powershell
# Verify you’re running as admin (will output True if elevated)
([Security.Principal.WindowsPrincipal] [Security.Principal.WindowsIdentity]::GetCurrent()).IsInRole(`
    [Security.Principal.WindowsBuiltInRole]::Administrator)
```

Yükseltilmiş bir kullanıcı olarak çalışmak, paketin global paket deposuna yerleşmesini sağlar; bu, çoğu derleme ajanının beklediği şeydir.

## Adım 2: Aspose'un belirli bir sürümünü kurun

Geliştiricilerin “**aspose nasıl kurulur**” sorusunun temel nedeni, bilinen, kararlı bir sürüme ihtiyaç duymalarıdır—belki kodları hata‑düzeltmeli bir sürüme hedeflenmiştir. `Install-Package` cmdlet'i, sürümü `-Version` bayrağıyla sabitlemenizi sağlar.

```powershell
# Step 2: Install Aspose.PDF version 25.3
Install-Package Aspose.PDF -Version 25.3 -ProviderName NuGet -Force
```

### Bayrakların önemi

| Flag | Reason |
|------|--------|
| `-Version 25.3` | Tam olarak 25.3 almanızı garanti eder, istem dışı yükseltmeleri önler. |
| `-ProviderName NuGet` | PowerShell'e hangi sağlayıcının kullanılacağını açıkça söyler; başka paket kaynaklarınız varsa belirsizliği önler. |
| `-Force` | Otomatik bir betiği durdurabilecek istemleri bastırır. |

> **Köşe durum:** Daha yeni bir sürüm zaten yüklüyse, `-AllowDowngrade` eklemediğiniz sürece PowerShell sürüm düşürmeyi reddeder. Az kullanın:

```powershell
Install-Package Aspose.PDF -Version 25.3 -ProviderName NuGet -Force -AllowDowngrade
```

## Adım 3: Kurulumu doğrulayın – how to list packages

Kurulum tamamlandıktan sonra, doğru sürümün beklediğiniz yere yerleştiğinden emin olmak isteyeceksiniz. İşte **how to list packages** burada devreye girer.

```powershell
# Step 3: List all installed packages named Aspose.PDF
Get-Package -Name Aspose.PDF
```

Tipik çıktı şu şekildedir:

```
Name                     Version          Source
----                     -------          ------
Aspose.PDF               25.3             nuget.org
```

Farklı bir sürüm görürseniz, daha önce kullandığınız `-Version` bayrağını tekrar kontrol edin veya doğru NuGet beslemesinden çektiğinizi doğrulamak için `Get-PackageSource` komutunu çalıştırın.

### Belirli bir kapsamda paketleri listeleme

Bazen yalnızca geçerli kullanıcı için yüklü paketleri görmek isteyebilirsiniz:

```powershell
Get-Package -Name Aspose.PDF -Scope CurrentUser
```

Ya da sistem‑geneli depoyu denetlemek için:

```powershell
Get-Package -Name Aspose.PDF -Scope AllUsers
```

Bu varyasyonlar, izinle ilgili hataları giderirken kullanışlıdır.

## Adım 4: Opsiyonel – Paketi otomatik olarak bir projeye ekleyin

Bir çözüm klasörü içinde çalışıyorsanız, PowerShell `.csproj` dosyasını sizin için güncelleyebilir:

```powershell
# Add Aspose.PDF 25.3 to the current directory’s .csproj
dotnet add package Aspose.PDF --version 25.3
```

Bu komut, PowerShell'in NuGet sağlayıcısı yerine .NET CLI'yi kullanır, ancak sonuç aynı: proje dosyanızda bir referans girişi. Az önce kurduğunuz tam sürümle kaynak kontrolünü senkronize tutmanın hızlı bir yoludur.

## Yaygın tuzaklar ve nasıl önlenir

| Belirti | Muhtemel neden | Çözüm |
|---------|----------------|-------|
| `Install-Package : No match was found for the specified search criteria` | NuGet provider missing or outdated | `Install-PackageProvider -Name NuGet -Force` then `Set-PSRepository -Name 'PSGallery' -InstallationPolicy Trusted` |
| `Access denied` when installing | Not running as admin | Re‑open PowerShell with **Run as administrator** |
| Wrong version appears in `Get-Package` | Cached metadata | Run `Update-Module -Name PowerShellGet` and retry |
| Package appears but VS can’t find it | Project still targets older .NET framework | Upgrade the target framework or install a compatible Aspose version |

## Kopyalayıp‑yapıştırabileceğiniz tam betik

Aşağıda, konuştuğumuz her şeyi bir araya getiren tek dosyalı bir PowerShell betiği var. `Install-Aspose.ps1` olarak kaydedin ve yönetici haklarıyla çalıştırın.

```powershell
<# 
.SYNOPSIS
Installs a specific version of Aspose.PDF via PowerShell and verifies the installation.

.DESCRIPTION
This script demonstrates how to run PowerShell as administrator, install a
specific version of the Aspose.PDF NuGet package, and list the installed
packages to confirm success. It also shows optional steps for adding the
package to a .NET project.

.AUTHOR
Your Name – 2026
#>

# 1️⃣ Ensure we are running elevated
if (-not ([Security.Principal.WindowsPrincipal] `
        [Security.Principal.WindowsIdentity]::GetCurrent()).IsInRole(`
        [Security.Principal.WindowsBuiltInRole]::Administrator)) {
    Write-Error "Please run this script from an elevated PowerShell session."
    exit 1
}

# 2️⃣ Install NuGet provider if missing
if (-not (Get-PackageProvider -Name NuGet -ErrorAction SilentlyContinue)) {
    Write-Host "NuGet provider not found – installing..."
    Install-PackageProvider -Name NuGet -Force | Out-Null
}

# 3️⃣ Install Aspose.PDF version 25.3
$desiredVersion = "25.3"
Write-Host "Installing Aspose.PDF version $desiredVersion ..."
Install-Package Aspose.PDF -Version $desiredVersion -ProviderName NuGet -Force

# 4️⃣ Verify installation
Write-Host "`nVerifying installation..."
$pkg = Get-Package -Name Aspose.PDF -ErrorAction SilentlyContinue
if ($pkg) {
    Write-Host "✅ Aspose.PDF $($pkg.Version) installed successfully."
} else {
    Write-Error "❌ Installation failed – package not found."
}

# 5️⃣ (Optional) Add to .csproj if present
$csproj = Get-ChildItem -Path . -Filter *.csproj -ErrorAction SilentlyContinue | Select-Object -First 1
if ($csproj) {
    Write-Host "`nAdding package reference to $($csproj.Name)..."
    dotnet add $csproj.FullName package Aspose.PDF --version $desiredVersion
}
```

Şöyle çalıştırın:

```powershell
.\Install-Aspose.ps1
```

Sürümü onaylayan yeşil bir işaret görmeli, ardından isteğe bağlı bir proje güncellemesi alacaksınız.

## Sonuç

**aspose nasıl kurulur** konusunu PowerShell kullanarak baştan sona ele aldık: yükseltilmiş bir oturum başlatma, kesin bir sürüm çekme ve sonucu **how to list packages** ile doğrulama. Yukarıdaki betik, tüm süreci tekrarlanabilir hâle getirir—CI boru hatları veya yeni ekip üyelerinin işe alımı için idealdir.

Sonraki adımda, diğer kütüphaneler için **install nuget package powershell**'ı keşfedebilir veya PDF üretmeye başlamak için Aspose'un kendi API'sine dalabilirsiniz. Bir sorunla karşılaşırsanız, “Yaygın tuzaklar” tablosuna tekrar bakın; çoğu sorun izinler veya güncel olmayan bir sağlayıcıdan kaynaklanır.

Kodlamaktan keyif alın, ve NuGet kurulumlarınızın daima hatasız olmasını dileriz!

![how to install aspose PowerShell screenshot](https://example.com/images/install-aspose-powershell.png)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}