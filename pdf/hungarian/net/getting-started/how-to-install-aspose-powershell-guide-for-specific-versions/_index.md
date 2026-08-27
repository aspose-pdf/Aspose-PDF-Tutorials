---
category: general
date: 2026-02-10
description: hogyan telepítsük az Aspose-t PowerShell használatával. Tanulja meg,
  hogyan futtassa a PowerShell-t rendszergazdaként, hogyan telepítsen konkrét verziót,
  és hogyan listázza a csomagokat.
draft: false
keywords:
- how to install aspose
- install specific version
- install nuget package powershell
- run powershell as administrator
- how to list packages
language: hu
og_description: Hogyan telepítsük az Aspose-t PowerShell-lel. Ez az útmutató bemutatja,
  hogyan futtassuk a PowerShell-t rendszergazdaként, hogyan telepítsünk egy adott
  verziót, és hogyan listázzuk a csomagokat.
og_title: Hogyan telepítsük az Aspose‑t – PowerShell lépésről‑lépésre útmutató
tags:
- powershell
- nuget
- aspose
- devops
title: Hogyan telepítsük az Aspose-t – PowerShell útmutató konkrét verziókhoz
url: /hu/net/getting-started/how-to-install-aspose-powershell-guide-for-specific-versions/
---

to translate "Pro tip:", "Edge case:", etc.

Also "## Prerequisites" etc.

Let's start.

We'll output the entire content with translation.

We must keep the shortcodes at top and bottom.

Let's produce.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# hogyan telepítsük az aspose‑t – PowerShell lépés‑ről‑lépésre útmutató

Gondolkodtál már azon, **hogyan telepítsük az aspose‑t** egy friss Windows gépre? Nem vagy egyedül. Sok .NET projektben az Aspose.PDF NuGet csomag a leggyakrabban használt könyvtár a PDF‑kezeléshez, mégis a telepítési lépés néha kissé homályos lehet – különösen, ha egy adott verzióra van szükséged, vagy egy szigorúan szabályozott szerveren dolgozol.

A lényeg: néhány másodperc alatt elindíthatod az Aspose‑t PowerShell‑ből. Ebben a tutorialban végigvezetünk a megfelelő jogosultságokkal indított PowerShell elindításán, egy konkrét verzió letöltésén, és a telepítés ellenőrzésén a **hogyan listázzuk a csomagokat** segítségével. A végére egy újrahasználható egy‑soros parancsot kapsz, amit CI‑szkriptekbe illeszthetsz, és megérted, miért kell minden kapcsolót megadni.

## Előfeltételek

- Windows 10/11 (vagy Windows Server) PowerShell 5.1+ verzióval.  
- Internetkapcsolat, hogy a NuGet tároló elérhető legyen.  
- Opcionális, de hasznos: a **NuGet provider** (`Install-PackageProvider -Name NuGet -Force`), ha még nincs telepítve.  
- Adminisztrátori jogok, ha a környezet csak a rendszer‑szintű telepítést engedélyezi.

Ha valamelyik pont ismeretlennek tűnik, ne aggódj – a legtöbb fejlesztői gép már eleve megfelel ezeknek. Kitérünk a **PowerShell futtatása rendszergazdaként** lépésre is, ha szükséges.

## 1. lépés: PowerShell megnyitása a megfelelő jogosultságokkal

> **Pro tip:** Egy vállalati munkaállomáson előfordulhat, hogy fel kell emelni a jogosultságot a végrehajtási szabályzat megkerüléséhez.

1. Kattints a **Start** menüre, írd be a **PowerShell**‑t, jobb‑kattintás az eredményre, majd válaszd a **Run as administrator**‑t.  
2. Ha a gyorsmenüt részesíted előnyben, nyomd meg a `Win + X` kombinációt → **Windows PowerShell (Admin)**.

```powershell
# Verify you’re running as admin (will output True if elevated)
([Security.Principal.WindowsPrincipal] [Security.Principal.WindowsIdentity]::GetCurrent()).IsInRole(`
    [Security.Principal.WindowsBuiltInRole]::Administrator)
```

Emelt jogosultságú felhasználóként futtatva a csomag a globális csomagtárba kerül, ami a legtöbb build‑ügynök elvárása.

## 2. lépés: Egy adott Aspose verzió telepítése

A fejlesztők leggyakrabban azért kérdezik, hogy **hogyan telepítsük az aspose‑t**, mert egy ismert, stabil verzióra van szükségük – például egy hibajavított kiadásra célzó kód miatt. Az `Install-Package` cmdlet a `-Version` kapcsolóval lehetővé teszi a verzió rögzítését.

```powershell
# Step 2: Install Aspose.PDF version 25.3
Install-Package Aspose.PDF -Version 25.3 -ProviderName NuGet -Force
```

### Miért fontosak a kapcsolók

| Kapcsoló | Indoklás |
|------|--------|
| `-Version 25.3` | Biztosítja, hogy pontosan a 25.3‑as verziót kapod, elkerülve a véletlen frissítéseket. |
| `-ProviderName NuGet` | Kifejezetten megmondja a PowerShell‑nek, melyik providert használja; elkerüli a félreértéseket, ha más csomagforrások is vannak. |
| `-Force` | Elnyomja azokat a promptokat, amelyek egy automatizált szkriptet megállíthatnak. |

> **Edge case:** Ha már van egy újabb verzió telepítve, a PowerShell nem engedi a visszaállítást, hacsak nem adod meg a `-AllowDowngrade` kapcsolót. Használd csak akkor, ha valóban szükséges:

```powershell
Install-Package Aspose.PDF -Version 25.3 -ProviderName NuGet -Force -AllowDowngrade
```

## 3. lépés: A telepítés ellenőrzése – hogyan listázzuk a csomagokat

A telepítés befejezése után szeretnéd megbizonyosodni, hogy a megfelelő verzió a várt helyen landolt. Itt jön képbe a **hogyan listázzuk a csomagokat**.

```powershell
# Step 3: List all installed packages named Aspose.PDF
Get-Package -Name Aspose.PDF
```

A tipikus kimenet például így néz ki:

```
Name                     Version          Source
----                     -------          ------
Aspose.PDF               25.3             nuget.org
```

Ha más verziót látsz, ellenőrizd a korábban használt `-Version` kapcsolót, vagy futtasd a `Get-PackageSource`‑t, hogy megbizonyosodj róla, a megfelelő NuGet tárolóból húzod a csomagot.

### Csomagok listázása egy adott hatókörben

Néha csak a jelenlegi felhasználó számára telepített csomagokat akarod látni:

```powershell
Get-Package -Name Aspose.PDF -Scope CurrentUser
```

Vagy a rendszer‑szintű tároló auditálásához:

```powershell
Get-Package -Name Aspose.PDF -Scope AllUsers
```

Ezek a variációk hasznosak a jogosultsági hibák nyomozásakor.

## 4. lépés: Opcionális – a csomag automatikus hozzáadása egy projekthez

Ha egy megoldás (solution) mappájában dolgozol, a PowerShell képes a `.csproj` fájlt is frissíteni:

```powershell
# Add Aspose.PDF 25.3 to the current directory’s .csproj
dotnet add package Aspose.PDF --version 25.3
```

Ez a parancs a .NET CLI‑t használja a PowerShell NuGet providere helyett, de az eredmény ugyanaz: egy referencia bejegyzés a projektfájlban. Gyors mód arra, hogy a forráskód‑kezelő szinkronban legyen a most telepített verzióval.

## Gyakori buktatók és megoldások

| Tünet | Valószínű ok | Javítás |
|---------|--------------|-----|
| `Install-Package : No match was found for the specified search criteria` | Hiányzó vagy elavult NuGet provider | `Install-PackageProvider -Name NuGet -Force` majd `Set-PSRepository -Name 'PSGallery' -InstallationPolicy Trusted` |
| `Access denied` a telepítés során | Nem rendszergazdaként futtatva | Nyisd meg újra a PowerShell‑t **Run as administrator**‑rel |
| Rossz verzió jelenik meg a `Get-Package`‑ben | Gyorsítótárazott metaadat | Futtasd a `Update-Module -Name PowerShellGet`‑t, majd próbáld újra |
| A csomag megjelenik, de a VS nem találja | A projekt régebbi .NET keretrendszert céloz | Frissítsd a célkeretrendszert, vagy telepíts egy kompatibilis Aspose verziót |

## Teljes szkript, amit egyszerűen másolhatsz‑beilleszthetsz

Az alábbi egyetlen fájlból álló PowerShell‑szkript mindent tartalmaz, amit eddig tárgyaltunk. Mentsd `Install-Aspose.ps1` néven, és futtasd admin jogokkal.

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

Futtatás módja:

```powershell
.\Install-Aspose.ps1
```

A kimenetben egy zöld pipa jelzi a verzió sikeres telepítését, majd opcionálisan a projekt frissítését.

## Összegzés

Áttekintettük, **hogyan telepítsük az aspose‑t** PowerShell‑lel a kezdettől a befejezésig: emelt jogosultságú munkamenet indítása, pontos verzió lekérése, és az eredmény ellenőrzése a **hogyan listázzuk a csomagokat** segítségével. A fenti szkript a folyamatot újrahasználhatóvá teszi – ideális CI‑pipeline‑okhoz vagy új csapattagok betanításához.

Ezután érdemes lehet megvizsgálni a **install nuget package powershell** témát más könyvtárakhoz, vagy mélyebben belemerülni az Aspose saját API‑jába PDF‑ek generálásához. Ha elakadsz, nézd meg újra a „Gyakori buktatók” táblázatot; a legtöbb probléma jogosultsági vagy elavult provider kérdés.

Jó kódolást, és legyenek a NuGet‑telepítéseid örökké hibamentesek! 

![hogyan telepítsük az aspose‑t PowerShell képernyőkép](https://example.com/images/install-aspose-powershell.png)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}