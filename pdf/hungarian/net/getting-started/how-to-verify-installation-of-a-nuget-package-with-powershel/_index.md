---
category: general
date: 2026-03-03
description: Hogyan ellenőrizhetjük egy NuGet csomag telepítését a PowerShellben.
  Tanulja meg, hogyan futtassa a PowerShellt rendszergazdaként, telepítsen konkrét
  verziót, és kezelje hatékonyan a csomagokat.
draft: false
keywords:
- how to verify installation
- install specific version
- run powershell as admin
- install nuget package powershell
- powershell package management
language: hu
og_description: Hogyan ellenőrizhetjük egy NuGet csomag telepítését PowerShellben.
  Ez a lépésről‑lépésre útmutató megmutatja, hogyan futtassuk a PowerShellt rendszergazdaként,
  telepítsünk egy adott verziót, és erősítsük meg, hogy a csomag jelen van.
og_title: Hogyan ellenőrizhetjük egy NuGet csomag telepítését PowerShell segítségével
tags:
- PowerShell
- NuGet
- Package Management
title: Hogyan ellenőrizhetjük egy NuGet csomag telepítését PowerShell segítségével
url: /hu/net/getting-started/how-to-verify-installation-of-a-nuget-package-with-powershel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan ellenőrizhetjük egy NuGet csomag telepítését PowerShellben

A NuGet csomag telepítésének ellenőrzése PowerShellben gyakori feladat a Windows adminisztrátorok számára. Ha valaha is azon tűnődtél, hogy a csomag valóban megérkezett-e a rendszeredre, ez az útmutató pontosan megmutatja, hogyan ellenőrizheted a telepítést – találgatás nélkül.  

A következő néhány percben végigvezetünk a PowerShell adminisztrátorként történő indításán, egy adott verzió letöltésén, és végül a csomag meglétének megerősítésén a gépeden. Emellett néhány tippet is megismerhetsz a mindennapi **PowerShell csomagkezeléshez**, amelyek segítenek tisztán tartani a környezetet.  

Mielőtt belevágnánk, győződj meg róla, hogy rendelkezel egy Windows géppel, amelyen PowerShell 7 (vagy Windows PowerShell 5.1) és internetkapcsolat van. Nem szükséges extra eszköz; minden a beépített PackageManagement szolgáltatóból fut.

---

![Screenshot of an elevated PowerShell window with the Get-Package command](/images/verify-installation.png "Screenshot showing how to verify installation in an elevated PowerShell window")

## 1. lépés: PowerShell futtatása adminként  

A PowerShell adminisztrátori jogokkal való futtatása az első védelmi vonal a jogosultsági problémák ellen. Amikor **PowerShellt futtatsz adminként**, a `Install-Package` parancs képes írni a Program Files mappába és regisztrálni a csomagot a rendszer‑szintű katalógusban.

```powershell
# Open an elevated session (manual step)
# Right‑click the PowerShell icon → Run as administrator
```

> **Pro tip:** Rögzítsd a “Windows PowerShell (Admin)” parancsikont a tálcára. Egy kattintás, és már indulhatsz is.

### Miért fontos a jogosultság emelése  

Emelés nélkül a `Install-Package` csendben egy felhasználó‑szintű helyre telepíthet, ami később összezavarhatja a `Get-Package` parancsot, mivel az alapértelmezés szerint a rendszer‑szintű területet nézi. Az emelés garantálja, hogy a csomag ott jelenik meg, ahol a legtöbb script számít rá.

---

## 2. lépés: Egy adott verzió telepítése a NuGet csomagból  

Gyakran nem a legújabb kiadást szeretnéd, hanem egy ismert, stabil verziót, amelyet a projekted már tesztelt. A **konkrét verzió telepítése** minta egyszerű a `-Version` kapcsolóval.

```powershell
# Install Aspose.PDF version 25.3 from the PowerShell Gallery
Install-Package Aspose.PDF -Version 25.3 -ProviderName NuGet -Scope AllUsers -Force
```

### A parancs részletezése  

| Paraméter | Mit csinál | Miért van rá szükség |
|-----------|------------|----------------------|
| `-Version 25.3` | Pontosan a megadott build számot rögzíti | Biztosítja az ismételhető buildeket |
| `-ProviderName NuGet` | Megmondja a PowerShellnek, melyik szolgáltatót használja | Elkerüli a kétértelműséget, ha több szolgáltató is regisztrálva van |
| `-Scope AllUsers` | Minden felhasználó számára telepít | A `Get-Package` rendszer‑szintű lekérdezéseihez szükséges |
| `-Force` | Elnyomja a felugró kérdéseket (hasznos szkriptekben) | Zökkenőmentes automatizálást biztosít |

> **Figyelem:** Ha kihagyod a `-Version` kapcsolót, a PowerShell a legújabb csomagot tölti le, ami esetleg törődésszerű változásokat hozhat.

---

## 3. lépés: A telepítés ellenőrzése  

Most jön a döntő pillanat: **hogyan ellenőrizhetjük a telepítést**. A legegyszerűbb mód, ha a PowerShellt megkérdezzük a frissen telepített csomagról.

```powershell
# Retrieve the package info
Get-Package -Name Aspose.PDF -ProviderName NuGet
```

Az eredménynek a következőhöz hasonlónak kell lennie:

```
Name           Version   Source   Summary
----           -------   ------   -------
Aspose.PDF    25.3      NuGet    .NET PDF library from Aspose
```

Ha a parancs semmit sem ad vissza, próbáld meg a felhasználó‑szintű lekérdezést:

```powershell
Get-Package -Name Aspose.PDF -ProviderName NuGet -Scope CurrentUser
```

### Alternatív ellenőrzési módszerek  

1. **Ellenőrizd a modul mappát** – A csomagok a `C:\Program Files\PackageManagement\Packages\` alatt tárolódnak. Keresd meg a `Aspose.PDF.25.3` nevű mappát.  
2. **Használd a `Find-Package` parancsot** – Ez a tárolót keresve megerősíti, hogy a verzió elérhető:  

   ```powershell
   Find-Package -Name Aspose.PDF -ProviderName NuGet | Where-Object { $_.Version -eq '25.3' }
   ```

3. **Érvényesítsd .NET‑tel** – Töltsd be az assembly‑t PowerShellben, hogy biztosan betölthető legyen a DLL:

   ```powershell
   Add-Type -Path "C:\Program Files\PackageManagement\Packages\Aspose.PDF.25.3\lib\netstandard2.0\Aspose.Pdf.dll"
   [Aspose.Pdf.License] | Get-Member
   ```

Ha bármelyik ellenőrzés sikeres, akkor **sikeresen ellenőrizted a telepítést**.

---

## Gyakori hibák és elkerülésük módjai  

- **Hiányzó NuGet szolgáltató** – Először futtasd a `Install-PackageProvider -Name NuGet -Force` parancsot.  
- **ExecutionPolicy blokkok** – Ideiglenesen állítsd be a `Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass` értéket a munkamenethez.  
- **Hálózati proxy problémák** – Használd a `-Proxy` és `-ProxyCredential` paramétereket, ha a környezet egy vállalati proxy mögött van.  
- **Verzióütközések** – Ha több verzió is létezik, add meg a `-RequiredVersion` kapcsolót a `Get-Package` parancsban a tisztázáshoz.

---

## Összeállítás – egy komplett szkript  

Az alábbiakban egy azonnal futtatható szkriptet találsz, amely magába foglalja a három lépést, hibakezelést, és egy barátságos sikerüzenetet ír ki.

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

A szkript futtatása egy egyértelmű „✅ Successfully verified installation…” sorral zárul, ami megerősíti, hogy a **hogyan ellenőrizhetjük a telepítést** folyamat vég‑től‑végig működik.

---

## Összegzés  

Most már tudod, **hogyan ellenőrizheted egy NuGet csomag telepítését** PowerShell segítségével, az emelt jogosultságú munkamenet indításától, egy célzott verzió telepítéséig, és végül a csomag jelenlétének megerősítéséig. Ezeknek a lépéseknek a elsajátítása magabiztosságot ad a **PowerShell csomagkezelési** munkafolyamatodban, és megakadályozza a „telepítve van, de nem működik” jellegű fejfájásokat, amelyek gyakran megnehezítik a Windows fejlesztőket.

Mi a következő? Próbáld ki a `Aspose.PDF` helyett egy másik könyvtárat, kísérletezz a `-Scope CurrentUser` kapcsolóval, vagy írd meg a szkriptedet több csomag tömeges telepítésére egy új munkaállomáson. Ha bármilyen furcsaságba ütközöl, ne feledd a fentebb leírt hibaelhárítási tippeket – különösen a szolgáltató és az execution‑policy ellenőrzéseket.

Boldog szkriptelést, és legyenek a telepítéseid mindig ellenőrizhetők!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}