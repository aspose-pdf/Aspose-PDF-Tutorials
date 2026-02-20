---
category: general
date: 2026-02-20
description: Lär dig hur du installerar NuGet‑paket med PowerShell, kör PowerShell
  som administratör, lista installerade paket och verifiera installerat paket på några
  minuter.
draft: false
keywords:
- how to install nuget
- run powershell as admin
- list installed packages
- how to verify package
- verify installed package
language: sv
og_description: hur man installerar NuGet-paket med PowerShell, kör PowerShell som
  administratör, lista installerade paket och verifiera installerat paket – komplett
  genomgång.
og_title: hur man installerar NuGet-paket via PowerShell – snabb guide
tags:
- PowerShell
- NuGet
- Package Management
title: hur man installerar NuGet-paket via PowerShell – steg för steg
url: /sv/net/getting-started/how-to-install-nuget-packages-via-powershell-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# hur man installerar nuget‑paket via PowerShell – steg för steg

Har du någonsin funderat **hur man installerar nuget**‑paket utan att öppna Visual Studio? Du är inte ensam. I många CI‑pipelines eller på nya maskiner är det snabbaste sättet att gå in i PowerShell—helst *run powershell as admin*—och låta paket‑hanteraren göra sitt.

I den här handledningen går vi igenom hela processen: öppna rätt konsol, hämta en specifik version av ett bibliotek och slutligen bekräfta att paketet verkligen har landat på ditt system. I slutet kan du **lista installerade paket**, veta **hur man verifierar paket**‑integritet och känna dig säker på att **verify installed package**‑steget lyckades varje gång.

## Vad du kommer att lära dig

- Hur du startar PowerShell med rätt behörigheter.  
- Den exakta `Install-Package`‑kommandosyntaxen för NuGet.  
- Sätt att **lista installerade paket** och bekräfta versionsnummer.  
- Vanliga fallgropar (saknad admin‑rätt, versionskonflikter) och hur du undviker dem.  

Ingen förkunskap om NuGet krävs, bara en fungerande Windows‑maskin och lite nyfikenhet.

---

## Hur man installerar NuGet‑paket med PowerShell

> **Pro tip:** Om du ofta lägger till samma paket, överväg att lägga dem i en skriptfil och köra den med `-File`. Det sparar dig från att skriva samma rad om och om igen.

### Steg 1: Öppna PowerShell med nödvändiga rättigheter

Det allra första du måste göra är att **run powershell as admin**. Utan förhöjda rättigheter kan `Install-Package`‑cmdleten tyst misslyckas eller be om en bekräftelse du inte vill hantera.

1. Klicka på Start‑knappen.  
2. Skriv **PowerShell**.  
3. Högerklicka *Windows PowerShell* och välj **Run as administrator**.  

Du får en UAC‑prompt; klicka **Yes**. Nu har du en privilegierad session redo för paketinstallation.

> *Varför admin?*  
> NuGet skriver filer till den globala paketmappen (`C:\Program Files\PackageManagement\NuGet\Packages` som standard). Den platsen är skyddad, så bara en förhöjd process kan skriva där.

### Steg 2: Installera önskat NuGet‑paket och version

Med konsolen öppen är kärnkommandot enkelt:

```powershell
# Install the Aspose.PDF library, version 25.3
Install-Package Aspose.PDF -Version 25.3
```

- `Install-Package` är PowerShell‑omslaget runt NuGets klient.  
- `-Version` låser exakt den build du behöver, vilket förhindrar oavsiktliga uppgraderingar.  

Om du utelämnar `-Version` kommer PowerShell att hämta den senaste stabila releasen—ibland är det okej, ibland vill du ha exakt den version du testat mot.

#### Vad händer under huven?

PowerShell kontaktar den konfigurerade paketkällan (standard är `https://www.nuget.org/api/v2`) och laddar ner `.nupkg`‑filen. Den extraherar sedan DLL‑arna till den globala paketmappen och registrerar paketet hos den lokala paketleverantören. Hela processen är vanligtvis klar på några sekunder såvida du inte har ett långsamt nätverk.

### Steg 3: Verifiera att paketet installerades korrekt

Nu när paketet ligger på disken kommer du förmodligen att fråga, **“Hur verifierar jag paketet?”** Svaret finns i en enkel fråga:

```powershell
# List all installed NuGet packages
Get-Package -Name Aspose.PDF
```

När du kör detta får du något i stil med:

```
Name        Version   Source
----        -------   ------
Aspose.PDF  25.3      nuget.org
```

Den utskriften bekräftar två saker:

1. Paketet **Aspose.PDF** finns.  
2. Dess version matchar den du begärde, vilket uppfyller kravet **verify installed package**.

Om du vill se *alla* paket på maskinen, ta bort `-Name`‑filtret:

```powershell
Get-Package | Where-Object {$_.ProviderName -eq 'NuGet'}
```

Denna **list installed packages**‑vy är praktisk för revisioner eller när du behöver rensa bort gamla bibliotek.

### Steg 4: Valfritt – hantera specialfall

#### a) Paketet hittas inte eller versionskonflikt

Om PowerShell svarar med *“Package not found”* eller *“Version not available”*, dubbelkolla stavning och versionsnummer. NuGet är inte skiftlägeskänsligt, men ett extra mellanslag bryter kommandot.

```powershell
# Search the NuGet feed for available versions
Find-Package Aspose.PDF -AllVersions
```

#### b) Kör utan admin‑rättigheter

Om du glömmer att **run powershell as admin**, kommer cmdleten att kasta ett behörighetsfel. Lösningen är helt enkelt att stänga fönstret och öppna det igen med förhöjda rättigheter—ingen om‑installation behövs.

#### c) Använd en anpassad källa

I företagsmiljöer kan du ha ett internt NuGet‑flöde:

```powershell
Install-Package MyCompany.Logging -Source https://nuget.mycompany.local/api/v2
```

Verifieringssteget är detsamma; kom bara ihåg att inkludera `-Source` när du installerar.

---

## Snabbreferenstabell

| Åtgärd                               | PowerShell‑kommando                                          | Varför det är viktigt |
|--------------------------------------|-------------------------------------------------------------|------------------------|
| Öppna förhöjd konsol                 | *Run PowerShell as Administrator*                           | Krävs för global installation |
| Installera en specifik version       | `Install-Package <pkg> -Version <x.y.z>`                    | Säkerställer reproducerbara byggen |
| Lista ett enskilt paket              | `Get-Package -Name <pkg>`                                    | Bekräftar **how to verify package** |
| Lista alla NuGet‑paket               | `Get-Package | Where-Object {$_.ProviderName -eq 'NuGet'}`| Användbart för **list installed packages** |
| Sök tillgängliga versioner           | `Find-Package <pkg> -AllVersions`                           | Hjälper när versionen är okänd |

---

## Slutsats

Vi har gått igenom **hur man installerar nuget**‑paket med PowerShell från början till slut—öppna konsolen **run powershell as admin**, hämta en specifik version och slutligen **list installed packages** för att **verify installed package**. Med dessa kommandon i verktygslådan kan du automatisera bibliotekshantering på vilken Windows‑maskin som helst, oavsett om du skriptar en CI‑pipeline eller bara fixar en saknad DLL på din utvecklingsdator.

Nästa steg? Prova att lägga till flera paket i ett enda skript, utforska parametern `-Scope` för att installera lokalt för ett projekt, eller kombinera dessa kommandon med `Invoke-Expression` för att bygga en lättviktig installerare åt ditt team. Och om du stöter på problem, kom ihåg **how to verify package**‑steget—att se versionen i `Get-Package` är ofta det snabbaste sättet att upptäcka ett fel.

Lycka till med PowerShell! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}