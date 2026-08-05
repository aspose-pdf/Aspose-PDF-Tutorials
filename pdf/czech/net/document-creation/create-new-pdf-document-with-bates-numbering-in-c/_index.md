---
category: general
date: 2026-08-04
description: Vytvořte nový PDF dokument v C# a rychle přidejte Batesovo číslování
  PDF pomocí Aspose.Pdf – naučte se přidávat prázdnou stránku PDF a vlastní čísla
  stránek.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create new pdf document
- add bates numbering pdf
- how to add bates
- add blank page pdf
- add custom page numbers
language: cs
lastmod: 2026-08-04
og_description: Vytvořte nový PDF dokument v C# a automaticky přidejte Batesovo číslování
  PDF pro správu právních případů – kompletní příklad kódu zahrnut.
og_image_alt: Screenshot of a C# program creating a PDF document with Bates numbers
  applied
og_title: Vytvořte nový PDF dokument s Batesovým číslováním v C#
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Create new PDF document in C# and add Bates numbering pdf quickly using
    Aspose.Pdf – learn to add blank page pdf and custom page numbers.
  headline: Create new PDF document with Bates numbering in C#
  type: TechArticle
tags:
- C#
- PDF
- Aspose.Pdf
- Bates numbering
title: Vytvořit nový PDF dokument s Batesovým číslováním v C#
url: /cs/net/document-creation/create-new-pdf-document-with-bates-numbering-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření nového PDF dokumentu s Bates číslováním v C#

Pokud potřebujete **vytvořit nový PDF dokument** v C#, tento průvodce vám ukáže, jak **přidat Bates číslování pdf** pomocí Aspose.Pdf. Naučíte se **přidat prázdnou stránku pdf**, nakonfigurovat **přidat vlastní čísla stránek** a uložit finální soubor.

Tutoriál pokrývá každý krok od instalace knihovny až po generování PDF, které splňuje standardy právních spisů. Na konci budete schopni vygenerovat PDF, vložit prázdnou stránku, aplikovat Bates čísla a přizpůsobit formát číslování – vše pomocí jediného spustitelného programu.

## Požadavky

* .NET 6.0 SDK nebo novější nainstalováno  
* Visual Studio 2022 (nebo jakékoli C# IDE)  
* Aktivní licence Aspose.Pdf pro .NET nebo bezplatný evaluační klíč  

Nemusíte instalovat žádné další NuGet balíčky; tutoriál vše nainstaluje automaticky.

## Krok 1: Instalace Aspose.Pdf přes NuGet

Otevřete terminál ve složce projektu a spusťte:

```bash
dotnet add package Aspose.Pdf
```

Příkaz přidá nejnovější stabilní verzi Aspose.Pdf do vašeho projektu, která poskytuje třídy `Document`, `BatesNumbering` a další třídy pro manipulaci s PDF, které budete používat.

## Krok 2: Vytvoření nového PDF dokumentu – počáteční nastavení

Vytvoření PDF souboru je základem pro všechny následné operace. Třída `Document` představuje celý PDF kontejner.

```csharp
using Aspose.Pdf;

// Step 2: Create a new PDF document
using var doc = new Document();
```

*Proč je to důležité*: Instancování `Document` alokuje vnitřní struktury potřebné pro stránky, písma a grafiku. Použití `using var` zajišťuje, že soubor bude po uložení řádně uvolněn.

## Krok 3: Přidání prázdné stránky pdf

PDF musí obsahovat alespoň jednu stránku, než na ni můžete umístit obsah. Přidání prázdné stránky vám poskytne čisté plátno pro Bates čísla.

```csharp
// Step 3: Add a blank page to the document
Page page = doc.Pages.Add();
```

Metoda `Pages.Add()` přidá novou, prázdnou stránku na konec kolekce stránek dokumentu. Tento volání můžete opakovat, pokud později potřebujete **přidat vlastní čísla stránek** napříč více stránkami.

## Krok 4: Konfigurace Bates číslování – jak přidat bates

Bates číslování je sekvenční identifikátor běžně používaný v právních dokumentech. Konfigurujete jej pomocí třídy `BatesNumbering`.

```csharp
// Step 4: Set up Bates numbering options
var bates = new BatesNumbering
{
    StartNumber = 1000,      // Starting number for the sequence
    Prefix = "CaseA-",       // Text to prepend to each number
    Increment = 1,           // Increment between consecutive numbers
    // Optional: Set the location, font size, etc.
};
```

*Proč je to důležité*: `StartNumber` určuje první číslo, `Prefix` přidává čitelný štítek a `Increment` řídí velikost kroku. Můžete také upravit `HorizontalAlignment`, `VerticalAlignment`, `FontSize` a `Margins`, abyste ovládali vzhled čísla na každé stránce.

## Krok 5: Aplikace Bates číslování pdf na stránku

Nyní, když jsou možnosti číslování připraveny, aplikujte je na stránku (nebo na celý dokument).

```csharp
// Step 5: Apply the Bates numbering to the page
bates.Apply(page);
```

Volání `Apply` vloží formátované číslo do patičky stránky jako výchozí. Pokud potřebujete číslo jinde, nastavte `bates.Position` před voláním `Apply`.

## Krok 6: Uložení PDF s aplikovaným Bates číslováním

Nakonec zapište dokument v paměti na disk.

```csharp
// Step 6: Save the PDF with Bates numbers applied
string outputPath = Path.Combine(
    Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
    "BatesNumbered.pdf");

doc.Save(outputPath);
Console.WriteLine($"PDF saved to {outputPath}");
```

Uložený soubor nyní obsahuje jedinou stránku s Bates číslem **CaseA-1000** zobrazeným ve spodní části. Otevřete PDF v libovolném prohlížeči a ověřte číslování.

## Očekávaný výstup

Když otevřete `BatesNumbered.pdf`, měli byste vidět:

* Jednu prázdnou stránku (nebo více, pokud jste přidali další stránky)  
* Text **CaseA-1000** umístěný ve spodní části stránky (výchozí umístění)  

Pokud přidáte více stránek a znovu použijete stejnou instanci `BatesNumbering`, čísla se budou automaticky zvyšovat (CaseA-1001, CaseA-1002, …).

## Profesionální tip: Přidání vlastních čísel stránek vedle Bates číslování

Někdy potřebujete jak Bates čísla, tak tradiční čísla stránek. Můžete je kombinovat přidáním `TextFragment` po aplikaci Bates číslování:

```csharp
// Add a traditional page number in the header
var pageNumber = new TextFragment($"Page {page.Number}")
{
    HorizontalAlignment = HorizontalAlignment.Center,
    VerticalAlignment = VerticalAlignment.Top,
    FontSize = 12,
    Font = FontRepository.FindFont("Arial")
};
page.Paragraphs.Add(pageNumber);
```

Tento úryvek ukazuje **přidání vlastních čísel stránek** při zachování Bates štítku.

## Okrajový případ: Aplikace Bates číslování na více stránek

Pokud váš dokument obsahuje několik stránek, můžete stejnou instanci `BatesNumbering` aplikovat na každou stránku v cyklu:

```csharp
for (int i = 1; i <= doc.Pages.Count; i++)
{
    bates.Apply(doc.Pages[i]);
}
```

Cyklus zajistí, že každá stránka dostane sekvenční číslo na základě `StartNumber` a `Increment`, které jste definovali.

## Časté úskalí a jak se jim vyhnout

| Problém | Proč se to stane | Řešení |
|-------|----------------|-----|
| Čísla jsou mimo střed | Výchozí zarovnání nemusí odpovídat vašemu rozvržení | Explicitně nastavte `bates.HorizontalAlignment` a `bates.VerticalAlignment` |
| Čísla překrývají existující obsah | Není definován okraj | Upravte `bates.Margin` nebo použijte `bates.Position` k posunutí čísla |
| Výjimka licence za běhu | Evaluační verze omezuje výstup | Použijte platnou licenci Aspose.Pdf před vytvořením dokumentu (`License license = new License(); license.SetLicense("Aspose.Pdf.lic");`) |

## Kompletní funkční příklad

Níže je samostatný program, který můžete zkopírovat, vložit a spustit.

```csharp
using System;
using System.IO;
using Aspose.Pdf;

class Program
{
    static void Main()
    {
        // 1. Create a new PDF document
        using var doc = new Document();

        // 2. Add a blank page pdf
        Page page = doc.Pages.Add();

        // 3. Configure Bates numbering – how to add bates
        var bates = new BatesNumbering
        {
            StartNumber = 1000,
            Prefix = "CaseA-",
            Increment = 1,
            HorizontalAlignment = HorizontalAlignment.Right,
            VerticalAlignment = VerticalAlignment.Bottom,
            Margin = new MarginInfo(20, 20, 20, 20),
            FontSize =


## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [How to Add and Customize Page Numbers in PDFs Using Aspose.PDF for .NET | Document Manipulation Guide](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [Aspose.PDF .NET&#58; Add Page Numbers to PDFs Using FloatingBox](/pdf/english/net/text-operations/aspose-pdf-net-floatingbox-page-numbering/)
- [Create PDF Document with Aspose.PDF – Add Page, Shape & Save](/pdf/english/net/document-creation/create-pdf-document-with-aspose-pdf-add-page-shape-save/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}