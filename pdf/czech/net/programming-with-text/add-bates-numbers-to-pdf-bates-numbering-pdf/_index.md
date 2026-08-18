---
category: general
date: 2026-01-15
description: Rychle přidejte Batesova čísla do svého PDF pomocí Aspose.Pdf. Naučte
  se, jak přidat zápatí do PDF, přidat číslování stránek do PDF a vytvořit vlastní
  číslování stránek.
draft: false
keywords:
- add bates numbers
- bates numbering pdf
- add footer to pdf
- add page numbers pdf
- add custom page numbering
language: cs
og_description: Rychle přidejte Batesova čísla do svého PDF pomocí Aspose.Pdf. Naučte
  se, jak přidat zápatí do PDF, přidat číslování stránek do PDF a přidat vlastní číslování
  stránek.
og_title: Přidejte Batesova čísla do PDF – Bates číslování PDF
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Přidat Batesova čísla do PDF – Bates číslování PDF
url: /cs/net/programming-with-text/add-bates-numbers-to-pdf-bates-numbering-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Přidání Batesových čísel do PDF – Kompletní průvodce

Už jste někdy potřebovali **přidat Batesova čísla** do PDF, ale nevedeli ste, kde začít? Nejste sami – právní týmy, auditoři a všich pracují s obrovskými sadami dokumentů, se s tímto problémem setkávají denně. Dobrá zpráva? S Aspose.Pdf pro .NET můžete tato čísla nasypat na každou stránku během několika řádků kódu.

V tomto tutoriálu projdeme celý proces: od načtení knihovny Aspose.Pdf, načtení zdrojového souboru, nastavení *BatesNumberingArtifact*, připojení jako zápatí a nakonec uložení výsledku. Na konci budete také vědět, jak **přidat zápatí do pdf**, **přidat čísla stránek pdf** a dokonce **přidat vlastní číslování stránek** pro ty neobvyklé případy.

## Co budete potřebovat

- .NET 6+ (nebo .NET Framework 4.8, pokud stále používáte klasický stack)  
- Odkaz na NuGet balíček **Aspose.Pdf** (`Install-Package Aspose.Pdf`)  
- PDF soubor, který chcete otisknout (budeme ho nazývat `source.pdf`)  

To je vše – žádné další nástroje, žádné těžké PDF editory. Pojďme na to.

![příklad přidání Batesových čísel](https://example.com/images/add-bates-numbers.png "příklad přidání Batesových čísel")

## Krok 1: Přidání Batesových čísel – Načtení PDF dokumentu

Nejprve potřebujeme objekt `Document`, který představuje PDF, které budeme upravovat. Představte si to jako otevření Word dokumentu před začátkem psaní.

```csharp
using Aspose.Pdf;
using System;

class Program
{
    static void Main()
    {
        // Load the PDF you want to add bates numbers to
        var pdfDocument = new Document(@"YOUR_DIRECTORY\source.pdf");

        // The rest of the steps go here...
    }
}
```

> **Proč je to důležité:** Načtení souboru vám poskytne přístup k jeho kolekci `Pages`, kam později připojíme artefakt Batesova číslování. Pokud soubor nelze najít, Aspose vyhodí jasnou výjimku `FileNotFoundException`, takže zkontrolujte cestu.

## Krok 2: Nastavení bates numbering pdf

Nyní definujeme *jak* mají čísla vypadat. `BatesNumberingArtifact` vám umožní nastavit předponu, počáteční číslo, počet číslic, příponu a umístění. Toto je jádro **bates numbering pdf**.

```csharp
// Step 2: Create and configure the Bates numbering artifact
var batesArtifact = new BatesNumberingArtifact
{
    Prefix = "CASE-",
    StartNumber = 1000,
    NumberDigits = 5,          // forces 5 digits, e.g., 01000
    Suffix = "-A",
    Placement = BatesNumberingArtifact.PlacementLocation.BottomCenter
};
```

> **Tip:** Pokud chcete, aby se čísla objevila v záhlaví místo zápatí, zaměňte `BottomCenter` za `TopCenter`. Výčtový typ `Placement` také podporuje `BottomLeft`, `BottomRight` a další, což vám dává flexibilitu pro různé styly **add footer to pdf**.

## Krok 3: Přidání page numbers pdf – Připojení artefaktu ke každé stránce

S připraveným artefaktem projdeme každou stránku a přidáme ho do kolekce `Artifacts`. Toto je krok, který skutečně **adds page numbers pdf**.

```csharp
// Step 3: Attach the artifact to each page
foreach (Page page in pdfDocument.Pages)
{
    page.Artifacts.Add(batesArtifact);
}
```

> **Co se děje pod kapotou?** Kolekce `Artifacts` se vykresluje po hlavním obsahu stránky, takže Batesovo číslo leží nad existujícím textem, ale pod anotacemi. Pokud potřebujete číslo umístit za obsah (vzácně), použijte `page.Artifacts.Insert(0, batesArtifact)`.

## Krok 4: Přidání custom page numbering – Uložení aktualizovaného PDF

Nakonec zapíšeme upravený dokument na disk. Výstupní soubor bude obsahovat Batesova čísla jako trvalou součást každé stránky.

```csharp
// Step 4: Save the PDF with the new numbering
pdfDocument.Save(@"YOUR_DIRECTORY\bates_out.pdf");

Console.WriteLine("Bates numbers added successfully! Check bates_out.pdf.");
```

> **Tip na ověření:** Otevřete `bates_out.pdf` v libovolném prohlížeči. Měli byste vidět něco jako `CASE-01000-A` uprostřed dole na každé stránce. Pokud čísla chybí, zkontrolujte, že vlastnost `Placement` odpovídá zamýšlenému umístění.

## Kompletní funkční příklad

Sestavením všech částí získáte kompletní, připravený program:

```csharp
using Aspose.Pdf;
using System;

class Program
{
    static void Main()
    {
        // Load the source PDF
        var pdfDocument = new Document(@"YOUR_DIRECTORY\source.pdf");

        // Configure Bates numbering artifact
        var batesArtifact = new BatesNumberingArtifact
        {
            Prefix = "CASE-",
            StartNumber = 1000,
            NumberDigits = 5,
            Suffix = "-A",
            Placement = BatesNumberingArtifact.PlacementLocation.BottomCenter
        };

        // Attach artifact to each page (adds page numbers pdf)
        foreach (Page page in pdfDocument.Pages)
        {
            page.Artifacts.Add(batesArtifact);
        }

        // Save the new PDF (adds footer to pdf)
        pdfDocument.Save(@"YOUR_DIRECTORY\bates_out.pdf");

        Console.WriteLine("Bates numbers added successfully! Check bates_out.pdf.");
    }
}
```

### Očekávaný výsledek

- **Soubor:** `bates_out.pdf` ve stejné složce jako `source.pdf`  
- **Vzhled:** Text `CASE-01000-A`, `CASE-01001-A`, … uprostřed dole na každé následující stránce  
- **Chování:** Čísla jsou trvale vložena; přežijí tisk, zploštění a další úpravy.

## Běžné varianty a okrajové případy

| Situace | Jak upravit |
|-----------|---------------|
| **Jiné počáteční číslo** | Změňte `StartNumber` na libovolné celé číslo (např. `StartNumber = 500`). |
| **Přípony písmen podle svazku** | Použijte smyčku pro úpravu `Suffix` podle stránky, nebo vytvořte více artefaktů s různými příponami. |
| **Číslování zarovnané vpravo** | Nastavte `Placement = BatesNumberingArtifact.PlacementLocation.BottomRight`. |
| **Velké dokumenty (10 000+ stránek)** | Zvažte zpracování po dávkách nebo zvýšení `NumberDigits`, aby nedošlo k přetečení. |
| **Potřeba skrýt čísla na určitých stránkách** | Přeskočte tyto stránky ve smyčce `foreach` (např. `if (page.Number != 1) page.Artifacts.Add(batesArtifact);`). |

> **Pozor:** Použití `Prefix` nebo `Suffix`, který obsahuje nelegální znaky pro názvy souborů (např. `*` nebo `?`). Aspose je i tak vloží, ale mohou způsobit problémy při pozdějším extrahování textu.

## Profesionální tipy pro produkční nasazení

- **Ukládejte artefakt do cache**, pokud zpracováváte mnoho PDF po sobě; vytvoření jednou ušetří několik milisekund na soubor.  
- **Vlákna:** Instance `BatesNumberingArtifact` není thread‑safe, takže každému vláknu dejte vlastní kopii.  
- **Výkon:** Pro masové dávky vypněte kompresi PDF (`pdfDocument.Compress = false`) před uložením a případně ji po uložení znovu zapněte.  
- **Testování:** Vždy proveďte rychlou vizuální kontrolu prvního vygenerovaného PDF, aby umístění odpovídalo standardům vašeho právního týmu.

## Závěr

Nyní máte kompletní recept, jak **add bates numbers** do libovolného PDF pomocí Aspose.Pdf, včetně možností **add footer to pdf**, **add page numbers pdf** a **add custom page numbering**. Kód je zcela samostatný, funguje s .NET 6 a novějšími verzemi a lze jej vložit do jakéhokoli existujícího automatizačního pipeline.

Co dál? Vyzkoušejte výměnu umístění `BottomCenter` za styl záhlaví, experimentujte s dynamickými předponami (např. ID případů z databáze) nebo kombinujte s funkcemi Aspose pro extrakci textu a vytvořte prohledávatelný index vašich nově očíslovaných dokumentů. Možnosti jsou neomezené a právě jste získali výkonný nástroj pro kontrolu dokumentů.

Šťastné programování a ať jsou vaše PDF vždy perfektně očíslovaná!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}