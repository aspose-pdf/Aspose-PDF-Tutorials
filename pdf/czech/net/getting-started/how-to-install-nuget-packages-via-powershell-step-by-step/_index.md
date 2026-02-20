---
category: general
date: 2026-02-20
description: Naučte se, jak instalovat balíčky NuGet pomocí PowerShellu, spustit PowerShell
  jako správce, vypsat nainstalované balíčky a ověřit nainstalovaný balíček během
  několika minut.
draft: false
keywords:
- how to install nuget
- run powershell as admin
- list installed packages
- how to verify package
- verify installed package
language: cs
og_description: jak nainstalovat balíčky NuGet pomocí PowerShellu, spustit PowerShell
  jako administrátor, vypsat nainstalované balíčky a ověřit nainstalovaný balíček –
  kompletní průvodce.
og_title: jak nainstalovat NuGet balíčky pomocí PowerShell – rychlý průvodce
tags:
- PowerShell
- NuGet
- Package Management
title: Jak nainstalovat NuGet balíčky pomocí PowerShellu – krok za krokem
url: /cs/net/getting-started/how-to-install-nuget-packages-via-powershell-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# jak nainstalovat nuget balíčky pomocí PowerShellu – krok za krokem

Už jste se někdy zamysleli **jak nainstalovat nuget** balíčky bez otevírání Visual Studio? Nejste sami. V mnoha CI pipelinech nebo na nových počítačích je nejrychlejší cesta vstoupit do PowerShellu—ideálně *run powershell as admin*—a nechat správce balíčků udělat svou práci.

V tomto tutoriálu projdeme celý proces: otevření správné konzole, stažení konkrétní verze knihovny a nakonec potvrzení, že balíček skutečně dorazil do vašeho systému. Na konci budete schopni **list installed packages**, vědět **how to verify package** integritu a mít jistotu, že krok **verify installed package** byl úspěšný pokaždé.

## Co se naučíte

- Jak spustit PowerShell s potřebnými oprávněními.  
- Přesná syntaxe příkazu `Install-Package` pro NuGet.  
- Způsoby, jak **list installed packages** a potvrdit čísla verzí.  
- Běžné úskalí (chybějící administrátorská práva, nesoulad verzí) a jak se jim vyhnout.  

Předchozí zkušenost s NuGet není vyžadována, stačí fungující Windows počítač a trochu zvědavosti.

---

## Jak nainstalovat NuGet balíčky pomocí PowerShellu

> **Pro tip:** Pokud často přidáváte stejné balíčky, zvažte jejich přidání do skriptového souboru a spuštění s `-File`. Ušetří vám to opakované psaní stejného řádku.

### Krok 1: Otevřete PowerShell s potřebnými oprávněními

První věc, kterou musíte udělat, je **run powershell as admin**. Bez zvýšených práv může cmdlet `Install-Package` tiše selhat nebo požádat o potvrzení, se kterým se nechcete zabývat.

1. Klikněte na tlačítko Start.  
2. Napište **PowerShell**.  
3. Klikněte pravým tlačítkem na *Windows PowerShell* a zvolte **Run as administrator**.  

Uvidíte výzvu UAC; klikněte na **Yes**. Nyní máte privilegovanou relaci připravenou k instalaci balíčků.

> *Proč admin?*  
> NuGet zapisuje soubory do globální složky balíčků (`C:\Program Files\PackageManagement\NuGet\Packages` ve výchozím nastavení). Toto umístění je chráněné, takže pouze zvýšený proces může zapisovat.

### Krok 2: Nainstalujte požadovaný NuGet balíček a verzi

With the console open, the core command is straightforward:

```powershell
# Install the Aspose.PDF library, version 25.3
Install-Package Aspose.PDF -Version 25.3
```

- `Install-Package` je PowerShell wrapper kolem klienta NuGet.  
- `-Version` připne přesnou verzi, kterou potřebujete, a zabraňuje nechtěným aktualizacím.  

Pokud vynecháte `-Version`, PowerShell stáhne nejnovější stabilní verzi—někdy je to v pořádku, jindy chcete přesně tu verzi, kterou jste testovali.

#### Co se děje pod kapotou?

PowerShell kontaktuje nakonfigurovaný zdroj balíčků (ve výchozím nastavení `https://www.nuget.org/api/v2`) a stáhne soubor `.nupkg`. Poté rozbalí DLL soubory do globální složky balíčků a zaregistruje balíček u lokálního poskytovatele balíčků. Celý proces obvykle skončí během několika sekund, pokud nejste na pomalé síti.

### Krok 3: Ověřte, že byl balíček úspěšně nainstalován

Nyní, když je balíček na disku, pravděpodobně se zeptáte, **„Jak ověřím balíček?“** Odpověď spočívá v jednoduchém dotazu:

```powershell
# List all installed NuGet packages
Get-Package -Name Aspose.PDF
```

Spuštěním tohoto získáte něco jako:

```
Name        Version   Source
----        -------   ------
Aspose.PDF  25.3      nuget.org
```

Tento výstup potvrzuje dvě věci:

1. Balíček **Aspose.PDF** je přítomen.  
2. Jeho verze odpovídá té, kterou jste požadovali, což splňuje požadavek **verify installed package**.

Pokud chcete zobrazit *každý* balíček na stroji, vynechte filtr `-Name`:

```powershell
Get-Package | Where-Object {$_.ProviderName -eq 'NuGet'}
```

Tento pohled **list installed packages** je užitečný pro audity nebo když potřebujete vyčistit staré knihovny.

### Krok 4: Volitelné – řešení okrajových případů

#### a) Balíček nenalezen nebo nesoulad verzí

Pokud PowerShell odpoví *„Package not found“* nebo *„Version not available“*, zkontrolujte pravopis a číslo verze. NuGet nerozlišuje velikost písmen, ale nadbytečná mezera příkaz zlomí.

```powershell
# Search the NuGet feed for available versions
Find-Package Aspose.PDF -AllVersions
```

#### b) Spuštění bez administrátorských práv

Pokud zapomenete **run powershell as admin**, cmdlet vyhodí chybu oprávnění. Oprava je jednoduše zavřít okno a znovu ho otevřít se zvýšenými právy—není třeba nic reinstalovat.

#### c) Použití vlastního zdroje

V korporátním prostředí můžete mít interní NuGet feed:

```powershell
Install-Package MyCompany.Logging -Source https://nuget.mycompany.local/api/v2
```

Krok ověření zůstává stejný; jen nezapomeňte při instalaci zahrnout `-Source`.

## Rychlá referenční tabulka

| Action                              | PowerShell command                                          | Why it matters |
|-------------------------------------|-------------------------------------------------------------|----------------|
| Otevřít zvýšenou konzoli            | *Run PowerShell as Administrator*                           | Potřeba pro globální instalaci |
| Instalovat konkrétní verzi          | `Install-Package <pkg> -Version <x.y.z>`                    | Zajišťuje reprodukovatelné sestavení |
| Vypsat jeden balíček                | `Get-Package -Name <pkg>`                                    | Potvrzuje **how to verify package** |
| Vypsat všechny NuGet balíčky        | `Get-Package | Where-Object {$_.ProviderName -eq 'NuGet'}`| Užitečné pro **list installed packages** |
| Vyhledat dostupné verze             | `Find-Package <pkg> -AllVersions`                           | Pomáhá, když není verze známa |

## Závěr

Probrali jsme **how to install nuget** balíčky pomocí PowerShellu od začátku do konce—otevření konzole **run powershell as admin**, stažení konkrétní verze a nakonec **list installed packages** pro **verify installed package**. S těmito příkazy ve vašem nářadí můžete automatizovat správu knihoven na jakémkoli Windows počítači, ať už skriptujete CI pipeline nebo jen opravujete chybějící DLL na svém vývojovém počítači.

Další kroky? Zkuste přidat více balíčků do jednoho skriptu, prozkoumejte parametr `-Scope` pro lokální instalaci pro projekt, nebo zkombinujte tyto příkazy s `Invoke-Expression` a vytvořte lehký instalátor pro svůj tým. A pokud narazíte na problém, pamatujte na krok **how to verify package**—zobrazení verze v `Get-Package` je často nejrychlejší způsob, jak odhalit problém.

Šťastné PowerShellování! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}