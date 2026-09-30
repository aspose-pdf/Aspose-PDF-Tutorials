---
category: general
date: 2026-02-20
description: Leer hoe je NuGet‑pakketten installeert met PowerShell, PowerShell als
  admin uitvoert, geïnstalleerde pakketten weergeeft en een geïnstalleerd pakket verifieert
  in enkele minuten.
draft: false
keywords:
- how to install nuget
- run powershell as admin
- list installed packages
- how to verify package
- verify installed package
language: nl
og_description: hoe nuget‑pakketten te installeren met PowerShell, PowerShell als
  administrator uit te voeren, geïnstalleerde pakketten te tonen en het geïnstalleerde
  pakket te verifiëren — volledige walkthrough.
og_title: Hoe nuget‑pakketten via PowerShell te installeren – snelle gids
tags:
- PowerShell
- NuGet
- Package Management
title: Hoe NuGet-pakketten te installeren via PowerShell – stap voor stap
url: /nl/net/getting-started/how-to-install-nuget-packages-via-powershell-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# hoe nuget-pakketten te installeren via PowerShell – stap voor stap

Heb je je ooit afgevraagd **hoe nuget** pakketten kunt installeren zonder Visual Studio te openen? Je bent niet de enige. In veel CI‑pipelines of op verse machines is de snelste route om PowerShell te openen—bij voorkeur *run powershell as admin*—en de package manager zijn werk te laten doen.

In deze tutorial lopen we het volledige proces door: de juiste console openen, een specifieke versie van een bibliotheek ophalen, en uiteindelijk bevestigen dat het pakket daadwerkelijk op je systeem is geïnstalleerd. Aan het einde kun je **list installed packages** uitvoeren, weet je **how to verify package** integriteit, en ben je ervan overtuigd dat de stap **verify installed package** elke keer geslaagd is.

## Wat je zult leren

- Hoe PowerShell te starten met de juiste rechten.  
- De exacte `Install-Package` opdrachtsyntaxis voor NuGet.  
- Manieren om **list installed packages** te bekijken en versienummers te bevestigen.  
- Veelvoorkomende valkuilen (ontbrekende adminrechten, versiemismatches) en hoe deze te vermijden.  

Ervaring met NuGet is niet vereist, alleen een werkende Windows‑machine en een beetje nieuwsgierigheid.

---

## Hoe NuGet-pakketten te installeren met PowerShell

> **Pro tip:** Als je vaak dezelfde pakketten toevoegt, overweeg ze toe te voegen aan een scriptbestand en uit te voeren met `-File`. Het bespaart je het steeds opnieuw typen van dezelfde regel.

### Stap 1: Open PowerShell met de benodigde rechten

Het eerste wat je moet doen is **run powershell as admin**. Zonder verhoogde rechten kan de `Install-Package` cmdlet stilzwijgend falen of om bevestiging vragen die je niet wilt behandelen.

1. Klik op de Start‑knop.  
2. Typ **PowerShell**.  
3. Klik met de rechtermuisknop op *Windows PowerShell* en kies **Run as administrator**.  

Je ziet een UAC‑prompt; klik op **Yes**. Nu heb je een bevoorrechte sessie klaar voor het installeren van pakketten.

> *Waarom admin?*  
> NuGet schrijft bestanden naar de globale pakkettenmap (`C:\Program Files\PackageManagement\NuGet\Packages` standaard). Die locatie is beschermd, dus alleen een verhoogd proces kan daar schrijven.

### Stap 2: Installeer het gewenste NuGet‑pakket en versie

With the console open, the core command is straightforward:

```powershell
# Install the Aspose.PDF library, version 25.3
Install-Package Aspose.PDF -Version 25.3
```

- `Install-Package` is de PowerShell‑wrapper rond de client van NuGet.  
- `-Version` vergrendelt de exacte build die je nodig hebt, waardoor per ongeluk upgraden wordt voorkomen.

Als je `-Version` weglaten, haalt PowerShell de nieuwste stabiele release—soms is dat prima, soms wil je de exacte versie die je getest hebt.

#### Wat gebeurt er onder de motorkap?

PowerShell benadert de geconfigureerde pakketbron (standaard `https://www.nuget.org/api/v2`) en downloadt het `.nupkg`‑bestand. Vervolgens extraheert het de DLL‑s naar de globale pakkettenmap en registreert het pakket bij de lokale pakketprovider. Het hele proces duurt meestal een paar seconden, tenzij je een trage verbinding hebt.

### Stap 3: Verifieer dat het pakket succesvol is geïnstalleerd

Nu het pakket op schijf staat, vraag je je waarschijnlijk af, **“Hoe verifieer ik het pakket?”** Het antwoord zit in een eenvoudige query:

```powershell
# List all installed NuGet packages
Get-Package -Name Aspose.PDF
```

Het uitvoeren hiervan geeft iets als:

```
Name        Version   Source
----        -------   ------
Aspose.PDF  25.3      nuget.org
```

Die output bevestigt twee zaken:

1. Het pakket **Aspose.PDF** is aanwezig.  
2. De versie komt overeen met de versie die je hebt opgegeven, waardoor aan de **verify installed package**‑vereiste wordt voldaan.

Als je *elk* pakket op de machine wilt zien, laat dan de `-Name`‑filter weg:

```powershell
Get-Package | Where-Object {$_.ProviderName -eq 'NuGet'}
```

Deze **list installed packages**‑weergave is handig voor audits of wanneer je oude bibliotheken moet opruimen.

### Stap 4: Optioneel – omgaan met randgevallen

#### a) Pakket niet gevonden of versie‑mismatch

Als PowerShell antwoordt met *“Package not found”* of *“Version not available”*, controleer dan de spelling en het versienummer. NuGet is niet hoofdlettergevoelig, maar een extra spatie zal de opdracht breken.

```powershell
# Search the NuGet feed for available versions
Find-Package Aspose.PDF -AllVersions
```

#### b) Uitvoeren zonder adminrechten

Als je vergeet **run powershell as admin** uit te voeren, zal de cmdlet een permissiefout geven. De oplossing is simpelweg het venster te sluiten en opnieuw te openen met verhoogde rechten—er is niets opnieuw te installeren.

#### c) Een aangepaste bron gebruiken

In bedrijfsomgevingen kun je een interne NuGet‑feed hebben:

```powershell
Install-Package MyCompany.Logging -Source https://nuget.mycompany.local/api/v2
```

De verificatiestap blijft hetzelfde; vergeet alleen niet `-Source` toe te voegen bij het installeren.

## Snelreferentietabel

| Action                              | PowerShell command                                          | Why it matters |
|-------------------------------------|-------------------------------------------------------------|----------------|
| Open verhoogde console               | *Run PowerShell as Administrator*                           | Nodig voor globale installatie |
| Installeer een specifieke versie          | `Install-Package <pkg> -Version <x.y.z>`                    | Garandeert reproduceerbare builds |
| Lijst een enkel pakket               | `Get-Package -Name <pkg>`                                    | Bevestigt **how to verify package** |
| Lijst alle NuGet-pakketten             | `Get-Package | Where-Object {$_.ProviderName -eq 'NuGet'}`| Handig voor **list installed packages** |
| Zoek beschikbare versies           | `Find-Package <pkg> -AllVersions`                           | Helpt wanneer de versie onbekend is |

## Conclusie

We hebben **how to install nuget** pakketten behandeld met PowerShell van begin tot eind—het openen van de console **run powershell as admin**, het ophalen van een specifieke versie, en uiteindelijk **list installed packages** om **verify installed package** te **verifiëren**. Met deze opdrachten in je gereedschapskist kun je bibliotheekbeheer automatiseren op elke Windows‑machine, of je nu een CI‑pipeline script, of gewoon een ontbrekende DLL op je ontwikkelbox repareert.

Volgende stappen? Probeer meerdere pakketten toe te voegen aan één script, verken de `-Scope`‑parameter om lokaal voor een project te installeren, of combineer deze opdrachten met `Invoke-Expression` om een lichtgewicht installer voor je team te bouwen. En als je een probleem tegenkomt, onthoud dan de **how to verify package** stap—het zien van de versie in `Get-Package` is vaak de snelste manier om een probleem te ontdekken.

Veel plezier met PowerShellen! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}