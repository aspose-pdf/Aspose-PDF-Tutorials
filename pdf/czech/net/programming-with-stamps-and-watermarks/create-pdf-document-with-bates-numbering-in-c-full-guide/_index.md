---
category: general
date: 2026-03-06
description: Vytvořte PDF dokument v C# a snadno přidejte Batesovo číslování. Naučte
  se, jak přidat prázdnou stránku do PDF, umístit razítko na stránku a implementovat
  Batesovo číslování.
draft: false
keywords:
- create pdf document
- add bates number
- add blank page pdf
- how to add bates numbering
- place stamp on page
language: cs
og_description: Vytvořte PDF dokument v C# a přidejte Batesovo číslování. Tento průvodce
  ukazuje, jak přidat prázdnou stránku PDF, umístit razítko na stránku a aplikovat
  Batesovo číslování.
og_title: Vytvořte PDF dokument s Batesovým číslováním – C# tutoriál
tags:
- Aspose.Pdf
- C#
- PDF automation
title: Vytvořte PDF dokument s Batesovým číslováním v C# – Kompletní průvodce
url: /cs/net/programming-with-stamps-and-watermarks/create-pdf-document-with-bates-numbering-in-c-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření PDF dokumentu s Bates číslováním v C#

Už jste někdy potřebovali **create PDF document** v C# a přemýšleli, jak přidat Bates číslo, aniž byste si trhali vlasy? Nejste v tom sami — advokátní kanceláře, soudy i některé týmy pro firemní soulad čelí tomuto problému každý den. Dobrá zpráva? S několika řádky kódu Aspose.Pdf můžete vytvořit zcela nový PDF, přidat prázdnou stránku a otisknout správné Bates číslo v jednom plynulém postupu.

V tomto tutoriálu projdeme celý proces: od nastavení projektu, přes přidání prázdné stránky PDF, až po zjištění **how to add bates numbering**, a nakonec **place stamp on page** a uložení výsledku. Na konci budete mít připravený úryvek, který můžete vložit do jakékoli .NET aplikace. Žádné vágní odkazy, jen kompletní, spustitelný příklad.

## Co budete potřebovat

- **.NET 6+** (nebo .NET Framework 4.6+ — Aspose.Pdf funguje s oběma)
- **Aspose.Pdf for .NET** NuGet balíček (`Install-Package Aspose.Pdf`)
- Slušné IDE (Visual Studio, Rider nebo VS Code s rozšířením C#)

To je vše. Žádné extra DLL, žádné externí služby. Ponořme se.

## Krok 1: Vytvoření PDF dokumentu — Počáteční nastavení

Nejprve potřebujeme čerstvý objekt `Document`. Představte si ho jako prázdné plátno, na kterém bude vše ostatní.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Initialize a new PDF document
Document pdfDocument = new Document();
```

> **Proč je to důležité:** Třída `Document` je vstupním bodem pro každou operaci Aspose. Její vytvoření vám poskytne přístup ke kolekci `Pages`, metadatům a bezpečnostním nastavením — všechny stavební bloky pro profesionální PDF.

## Krok 2: Přidání prázdné stránky PDF

PDF bez stránek je jako kniha bez listů — docela k ničemu. Přidání prázdné stránky je jednoduché a poskytne nám plochu, na kterou můžeme otisknout Bates číslo.

```csharp
// Add a single blank page to the document
Page page = pdfDocument.Pages.Add();
```

> **Tip:** Pokud potřebujete více stránek, stačí v cyklu volat `pdfDocument.Pages.Add()`. Každé volání vrátí nový objekt `Page`, který můžete nezávisle přizpůsobit.

## Krok 3: Jak přidat Bates číslování — Vytvoření TextStamp

Nyní přichází jádro záležitosti: **Bates number**. V Aspose.Pdf je to jen `TextStamp` se speciálním příznakem artifact.

```csharp
// Create a text stamp that will serve as a Bates number
TextStamp batesStamp = new TextStamp("Bates-001")
{
    // Mark the stamp as a Bates‑numbering artifact (helps PDF viewers treat it specially)
    Artifact = ArtifactType.BatesNumbering,
    // Align the stamp to the bottom‑right corner of the page
    HorizontalAlignment = HorizontalAlignment.Right,
    VerticalAlignment = VerticalAlignment.Bottom,
    // Add a small margin so the number isn’t glued to the edge
    Margin = new Margin { Bottom = 10, Right = 10 }
};
```

> **Proč nastavujeme `Artifact`**: Některé PDF čtečky zobrazují Bates čísla jako prohledávatelná metadata. Označením razítka jako `BatesNumbering` artifact zajistíme, že následné nástroje jej automaticky rozpoznají.

## Krok 4: Umístění razítka na stránku

S připraveným razítkem nyní **place stamp on page**. Toto je krok, kde se vizuální číslo skutečně objeví v PDF.

```csharp
// Add the Bates number stamp to the previously created page
page.AddStamp(batesStamp);
```

> **Hraniční případ:** Pokud potřebujete, aby se číslo zvyšovalo na každé stránce, projdete `pdfDocument.Pages` v cyklu a před voláním `AddStamp` aktualizujete `batesStamp.Value`. V tomto příkladu je to zjednodušené statickým „Bates‑001“.

## Krok 5: Uložení a ověření výsledku

Nakonec PDF uložíme na disk. Vyberte složku, do které máte právo zápisu; jinak narazíte na `UnauthorizedAccessException`.

```csharp
// Save the stamped PDF to a file
pdfDocument.Save("YOUR_DIRECTORY/BatesStamped.pdf");
```

Když otevřete `BatesStamped.pdf` v libovolném prohlížeči, měli byste vidět drobné „Bates‑001“ umístěné úhledně v pravém dolním rohu prázdné stránky.

> **Očekávaný výstup:**  
> ![PDF s Bates číslem](image-placeholder.png "PDF s Bates číslem")  
> *Alternativní text: PDF s Bates číslem v pravém dolním rohu.*

Pokud se číslo nezobrazuje, zkontrolujte hodnoty okrajů a ujistěte se, že velikost stránky není příliš malá (výchozí A4 funguje dobře). Také ověřte, že příznak `Artifact` není odstraňován žádnými nástroji pro následné zpracování.

## Kompletní funkční příklad

Níže je kompletní program připravený ke zkopírování a vložení. Obsahuje všechny `using` direktivy a komentáře, aby vás udržel v orientaci.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize a new PDF document
        Document pdfDocument = new Document();

        // 2️⃣ Add a blank page – this is where we’ll put the Bates number
        Page page = pdfDocument.Pages.Add();

        // 3️⃣ Create a TextStamp for the Bates number
        TextStamp batesStamp = new TextStamp("Bates-001")
        {
            Artifact = ArtifactType.BatesNumbering,          // Marks it as a Bates‑numbering artifact
            HorizontalAlignment = HorizontalAlignment.Right, // Align right
            VerticalAlignment = VerticalAlignment.Bottom,    // Align bottom
            Margin = new Margin { Bottom = 10, Right = 10 }  // Small margin from edges
        };

        // 4️⃣ Place the stamp on the page
        page.AddStamp(batesStamp);

        // 5️⃣ Save the PDF to disk
        string outputPath = @"C:\Temp\BatesStamped.pdf";
        pdfDocument.Save(outputPath);

        Console.WriteLine($"PDF created successfully: {outputPath}");
    }
}
```

Spusťte program, otevřete PDF a uvidíte Bates číslo přesně tam, kam jsme ho umístili. 🎉

## Běžné varianty a úskalí

| Scénář | Co změnit | Proč |
|----------|----------------|-----|
| **Více stránek, inkrementální čísla** | Projít `pdfDocument.Pages` v cyklu, nastavit `batesStamp.Value = $"Bates-{i:D3}"` před `AddStamp` | Dává každé stránce jedinečný identifikátor, typické pro právní svazky |
| **Jiné umístění (nahoře vlevo)** | Změnit `HorizontalAlignment = HorizontalAlignment.Left` a `VerticalAlignment = VerticalAlignment.Top` | Některé organizace upřednostňují číslo v hlavičce místo v patičce |
| **Vlastní font nebo barva** | Nastavit `batesStamp.TextState.Font = FontRepository.FindFont("Arial"); batesStamp.TextState.FontSize = 12; batesStamp.TextState.ForegroundColor = Color.Red;` | Zlepšuje čitelnost nebo splňuje brandingové směrnice |
| **Přidání existujícího PDF jako pozadí** | Načíst zdrojové PDF pomocí `Document src = new Document("source.pdf"); pdfDocument.Pages.Add(src.Pages[1]);` | Užitečné, když potřebujete razítko na předem vygenerovaném formuláři |

## Závěr

Právě jsme ukázali, jak **create PDF document**, **add blank page pdf** a **add bates number** pomocí Aspose.Pdf pro .NET, poté **place stamp on page** a uložit soubor. Kód je úmyslně stručný, aby ho šlo přizpůsobit větším pracovním postupům — ať už zpracováváte desítky souborů najednou nebo jej integrujete do webové služby.

- Automatizace logiky inkrementace pro velké spisy.
- Vložení generování PDF do ASP.NET Core API.
- Přidání zabezpečení (ochrana heslem) pomocí `pdfDocument.Encrypt(...)`.

Neváhejte experimentovat, zkoušet nové věci a klást otázky v komentářích. Šťastné programování a ať jsou vaše PDF vždy perfektně razítkovaná!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}