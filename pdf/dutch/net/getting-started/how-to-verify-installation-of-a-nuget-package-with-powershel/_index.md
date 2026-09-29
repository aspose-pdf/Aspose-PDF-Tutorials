---
category: general
date: 2026-03-03
description: Hoe de installatie van een NuGet‑pakket in PowerShell te verifiëren.
  Leer PowerShell als administrator uit te voeren, een specifieke versie te installeren
  en pakketten efficiënt te beheren.
draft: false
keywords:
- how to verify installation
- install specific version
- run powershell as admin
- install nuget package powershell
- powershell package management
language: nl
og_description: Hoe de installatie van een NuGet‑pakket in PowerShell te verifiëren.
  Deze stapsgewijze handleiding laat zien hoe je PowerShell als beheerder uitvoert,
  een specifieke versie installeert en bevestigt dat het pakket aanwezig is.
og_title: Hoe de installatie van een NuGet‑pakket te verifiëren met PowerShell
tags:
- PowerShell
- NuGet
- Package Management
title: Hoe de installatie van een NuGet‑pakket te verifiëren met PowerShell
url: /nl/net/getting-started/how-to-verify-installation-of-a-nuget-package-with-powershel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe de installatie van een NuGet‑pakket te verifiëren met PowerShell

Hoe de installatie van een NuGet‑pakket in PowerShell te verifiëren is een veelvoorkomende taak voor Windows‑beheerders. Als je je ooit hebt afgevraagd of het pakket echt op je systeem is terechtgekomen, laat deze gids je precies zien hoe je de installatie kunt verifiëren – geen giswerk meer.  

In de komende paar minuten lopen we door het uitvoeren van PowerShell als beheerder, het ophalen van een specifieke versie van een pakket, en uiteindelijk bevestigen dat het pakket op je machine bestaat. Je krijgt ook een paar tips voor alledaags **PowerShell package management** die je omgeving netjes houden.  

Voordat we beginnen, zorg dat je een Windows‑machine hebt met PowerShell 7 (of Windows PowerShell 5.1) en een internetverbinding. Er zijn geen extra tools nodig; alles draait rechtstreeks vanuit de ingebouwde PackageManagement‑provider.

---

![Screenshot of an elevated PowerShell window with the Get-Package command](/images/verify-installation.png "Screenshot showing how to verify installation in an elevated PowerShell window")

## Stap 1: PowerShell als beheerder uitvoeren  

PowerShell met administratieve rechten uitvoeren is de eerste verdedigingslinie tegen permissie‑gerelateerde haperingen. Wanneer je **PowerShell als admin uitvoert**, kan de `Install-Package`‑cmdlet schrijven naar de Program Files‑map en het pakket registreren in de systeem‑brede catalogus.

```powershell
# Open an elevated session (manual step)
# Right‑click the PowerShell icon → Run as administrator
```

> **Pro tip:** Pin de snelkoppeling “Windows PowerShell (Admin)” aan je taakbalk. Eén klik en je bent klaar om te gaan.

### Waarom verhoging belangrijk is  

Zonder verhoging kan `Install-Package` stilletjes terugvallen op een gebruikers‑gescope locatie, wat later `Get-Package` kan verwarren omdat die standaard in de systeem‑scope zoekt. Verhogen garandeert dat het pakket verschijnt waar de meeste scripts het verwachten.

---

## Stap 2: Een specifieke versie van het NuGet‑pakket installeren  

Vaak wil je niet de nieuwste release, maar een bekende, goede versie waar je project tegen getest is. Het **install specific version**‑patroon is eenvoudig met de `-Version`‑vlag.

```powershell
# Install Aspose.PDF version 25.3 from the PowerShell Gallery
Install-Package Aspose.PDF -Version 25.3 -ProviderName NuGet -Scope AllUsers -Force
```

### De opdracht ontleden  

| Parameter | Wat het doet | Waarom je het nodig hebt |
|-----------|--------------|--------------------------|
| `-Version 25.3` | Zet het exacte build‑nummer vast | Garandeert reproduceerbare builds |
| `-ProviderName NuGet` | Vertelt PowerShell welke provider te gebruiken | Voorkomt onduidelijkheid als meerdere providers zijn geregistreerd |
| `-Scope AllUsers` | Installeert voor elk account op de machine | Werkt met `Get-Package` systeem‑brede queries |
| `-Force` | Onderdrukt prompts (handig in scripts) | Houdt de automatisering soepel |

> **Let op:** Als je `-Version` weglaten, haalt PowerShell het nieuwste pakket op, wat mogelijk brekende wijzigingen introduceert.

---

## Stap 3: De installatie verifiëren  

Nu volgt het moment van de waarheid: **hoe de installatie te verifiëren**. De meest directe manier is PowerShell vragen naar het pakket dat je zojuist hebt geïnstalleerd.

```powershell
# Retrieve the package info
Get-Package -Name Aspose.PDF -ProviderName NuGet
```

Je zou output moeten zien die lijkt op:

```
Name           Version   Source   Summary
----           -------   ------   -------
Aspose.PDF    25.3      NuGet    .NET PDF library from Aspose
```

Als de opdracht niets teruggeeft, probeer dan de gebruikers‑gescope query:

```powershell
Get-Package -Name Aspose.PDF -ProviderName NuGet -Scope CurrentUser
```

### Alternatieve verificatiemethoden  

1. **Controleer de modulemap** – Pakketten worden opgeslagen onder `C:\Program Files\PackageManagement\Packages\`. Zoek naar een map genaamd `Aspose.PDF.25.3`.  
2. **Gebruik `Find-Package`** – Dit doorzoekt de repository en kan bevestigen dat de versie beschikbaar is:  

   ```powershell
   Find-Package -Name Aspose.PDF -ProviderName NuGet | Where-Object { $_.Version -eq '25.3' }
   ```

3. **Valideer met .NET** – Laad de assembly in PowerShell om te zorgen dat de DLL laadbaar is:

   ```powershell
   Add-Type -Path "C:\Program Files\PackageManagement\Packages\Aspose.PDF.25.3\lib\netstandard2.0\Aspose.Pdf.dll"
   [Aspose.Pdf.License] | Get-Member
   ```

Als een van die controles slaagt, heb je de **installatie geverifieerd**.

---

## Veelvoorkomende valkuilen en hoe ze te vermijden  

- **Ontbrekende NuGet‑provider** – Voer eerst `Install-PackageProvider -Name NuGet -Force` uit.  
- **ExecutionPolicy‑blokken** – Stel tijdelijk `Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass` in voor de sessie.  
- **Netwerkproxy‑problemen** – Gebruik de parameters `-Proxy` en `-ProxyCredential` als je omgeving zich achter een bedrijfsproxy bevindt.  
- **Versieconflicten** – Wanneer meerdere versies bestaan, specificeer `-RequiredVersion` in `Get-Package` om te onderscheiden.

---

## Alles samenvoegen – Een compleet script  

Hieronder staat een kant‑klaar script dat de drie stappen omvat, foutafhandeling bevat, en een vriendelijke succesmelding afdrukt.

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

Het uitvoeren van het script levert een duidelijke “✅ Successfully verified installation…”‑regel op, waarmee wordt bevestigd dat **hoe de installatie te verifiëren** van begin tot eind werkt.

---

## Conclusie  

Je weet nu **hoe de installatie te verifiëren** van elk NuGet‑pakket met PowerShell, van het starten van een verhoogde sessie tot het installeren van een gerichte versie en uiteindelijk het bevestigen van de aanwezigheid van het pakket. Het beheersen van deze stappen geeft je vertrouwen in je **PowerShell package management**‑workflow en voorkomt de “het lijkt geïnstalleerd maar is dat niet”‑hoofdpijn die Windows‑ontwikkelaars vaak treft.

Wat nu? Probeer `Aspose.PDF` te vervangen door een andere bibliotheek, experimenteer met `-Scope CurrentUser`, of script een bulk‑installatie van meerdere pakketten voor een nieuwe werkstation. En als je tegen eigenaardigheden aanloopt, onthoud dan de bovenstaande probleemoplossingstips – vooral de provider‑ en execution‑policy‑controles.

Happy scripting, and may your installations always be verifiable!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}