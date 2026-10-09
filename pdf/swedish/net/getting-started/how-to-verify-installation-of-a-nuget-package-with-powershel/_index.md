---
category: general
date: 2026-03-03
description: Hur man verifierar installationen av ett NuGet‑paket i PowerShell. Lär
  dig att köra PowerShell som administratör, installera en specifik version och hantera
  paket effektivt.
draft: false
keywords:
- how to verify installation
- install specific version
- run powershell as admin
- install nuget package powershell
- powershell package management
language: sv
og_description: Hur du verifierar installationen av ett NuGet‑paket i PowerShell.
  Denna steg‑för‑steg‑guide visar dig hur du kör PowerShell som administratör, installerar
  en specifik version och bekräftar att paketet finns.
og_title: Hur man verifierar installation av ett NuGet‑paket med PowerShell
tags:
- PowerShell
- NuGet
- Package Management
title: Hur man verifierar installationen av ett NuGet‑paket med PowerShell
url: /sv/net/getting-started/how-to-verify-installation-of-a-nuget-package-with-powershel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Så verifierar du installation av ett NuGet-paket med PowerShell

Att verifiera installation av ett NuGet-paket i PowerShell är en vanlig uppgift för Windows-administratörer. Om du någonsin har undrat om paketet verkligen har landat på ditt system, visar den här guiden exakt hur du verifierar installationen—utan gissningar.  

Under de kommande minuterna går vi igenom hur du kör PowerShell som administratör, hämtar en specifik version av ett paket och slutligen bekräftar att paketet finns på din maskin. Du får också med dig ett par tips för daglig **PowerShell package management** som håller din miljö prydlig.  

Innan vi dyker ner, se till att du har en Windows-dator med PowerShell 7 (eller Windows PowerShell 5.1) och en internetanslutning. Inga extra verktyg behövs; allt körs direkt från den inbyggda PackageManagement‑leverantören.

---

![Skärmdump av ett förhöjt PowerShell‑fönster med Get-Package‑kommandot](/images/verify-installation.png "Skärmdump som visar hur man verifierar installation i ett förhöjt PowerShell‑fönster")

## Steg 1: Kör PowerShell som administratör  

Att köra PowerShell med administrativa rättigheter är den första försvarslinjen mot behörighetsrelaterade problem. När du **kör PowerShell som administratör**, kan `Install-Package`‑cmdleten skriva till Program Files‑mappen och registrera paketet i det systemomfattande katalogen.

```powershell
# Open an elevated session (manual step)
# Right‑click the PowerShell icon → Run as administrator
```

> **Proffstips:** Fäst genvägen “Windows PowerShell (Admin)” på ditt aktivitetsfält. Ett klick så är du redo att köra.

### Varför förhöjning är viktigt  

Utan förhöjning kan `Install-Package` tyst falla tillbaka till en användarspecifik plats, vilket senare kan förvirra `Get-Package` eftersom den som standard söker i systemomfånget. Att köra med förhöjning garanterar att paketet visas där de flesta skript förväntar sig det.

---

## Steg 2: Installera en specifik version av NuGet‑paketet  

Ofta vill du inte ha den senaste versionen utan en beprövad version som ditt projekt har testats mot. Mönstret **install specific version** är enkelt med flaggan `-Version`.

```powershell
# Install Aspose.PDF version 25.3 from the PowerShell Gallery
Install-Package Aspose.PDF -Version 25.3 -ProviderName NuGet -Scope AllUsers -Force
```

### Genomgång av kommandot  

| Parameter | Vad den gör | Varför du behöver den |
|-----------|--------------|-----------------------|
| `-Version 25.3` | Anger exakt byggnummer | Säkerställer reproducerbara byggen |
| `-ProviderName NuGet` | Anger vilken leverantör PowerShell ska använda | Undviker tvetydighet om flera leverantörer är registrerade |
| `-Scope AllUsers` | Installerar för alla konton på maskinen | Fungerar med `Get-Package`‑frågor i systemomfång |
| `-Force` | Undertrycker frågor (användbart i skript) | Håller automatiseringen smidig |

> **Varning:** Om du utelämnar `-Version` hämtar PowerShell det senaste paketet, vilket kan introducera brytande förändringar.

---

## Steg 3: Verifiera installationen  

Nu kommer sanningsögonblicket: **hur man verifierar installation**. Det mest direkta sättet är att be PowerShell om paketet du just installerade.

```powershell
# Retrieve the package info
Get-Package -Name Aspose.PDF -ProviderName NuGet
```

Du bör se en output liknande:

```
Name           Version   Source   Summary
----           -------   ------   -------
Aspose.PDF    25.3      NuGet    .NET PDF library from Aspose
```

Om kommandot inte returnerar något, prova användarspecifik fråga:

```powershell
Get-Package -Name Aspose.PDF -ProviderName NuGet -Scope CurrentUser
```

### Alternativa verifieringsmetoder  

1. **Kontrollera modulmappen** – Paket lagras under `C:\Program Files\PackageManagement\Packages\`. Leta efter en mapp med namnet `Aspose.PDF.25.3`.  
2. **Använd `Find-Package`** – Detta söker i förrådet och kan bekräfta att versionen är tillgänglig:  

   ```powershell
   Find-Package -Name Aspose.PDF -ProviderName NuGet | Where-Object { $_.Version -eq '25.3' }
   ```

3. **Validera med .NET** – Ladda assemblyn i PowerShell för att säkerställa att DLL‑filen kan laddas:  

   ```powershell
   Add-Type -Path "C:\Program Files\PackageManagement\Packages\Aspose.PDF.25.3\lib\netstandard2.0\Aspose.Pdf.dll"
   [Aspose.Pdf.License] | Get-Member
   ```

Om någon av dessa kontroller lyckas, har du framgångsrikt **verifierat installationen**.

---

## Vanliga fallgropar och hur du undviker dem  

- **Saknad NuGet‑leverantör** – Kör `Install-PackageProvider -Name NuGet -Force` först.  
- **ExecutionPolicy‑blockeringar** – Ställ tillfälligt in `Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass` för sessionen.  
- **Nätverksproxy‑problem** – Använd parametrarna `-Proxy` och `-ProxyCredential` om din miljö sitter bakom en företagsproxy.  
- **Versionskonflikter** – När flera versioner finns, specificera `-RequiredVersion` i `Get-Package` för att tydliggöra.

---

## Sätt ihop allt – ett komplett skript  

Nedan är ett färdigt skript som kapslar in de tre stegen, inkluderar felhantering och skriver ut ett vänligt framgångsmeddelande.

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

När skriptet körs får du en tydlig rad “✅ Successfully verified installation…” som bekräftar att **hur man verifierar installation** fungerar från början till slut.

---

## Slutsats  

Du vet nu **hur man verifierar installation** av vilket NuGet‑paket som helst med PowerShell, från att starta en förhöjd session till att installera en specifik version och slutligen bekräfta paketets närvaro. Att behärska dessa steg ger dig förtroende för ditt **PowerShell package management**‑arbetsflöde och förhindrar de “det ser ut att vara installerat men är det inte”‑huvudvärken som ofta plågar Windows‑utvecklare.

Vad blir nästa steg? Prova att byta ut `Aspose.PDF` mot ett annat bibliotek, experimentera med `-Scope CurrentUser`, eller skript en massinstallation av flera paket för en ny arbetsstation. Och om du stöter på konstigheter, kom ihåg felsökningstipsen ovan—särskilt kontrollerna för leverantör och ExecutionPolicy.

Lycklig scripting, och må dina installationer alltid vara verifierbara!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}