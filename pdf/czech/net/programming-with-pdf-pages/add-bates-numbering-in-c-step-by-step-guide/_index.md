---
category: general
date: 2026-03-27
description: Rychle přidejte Batesovo číslování v C#. Naučte se, jak přidat vlastní
  čísla stránek, sekvenční čísla stránek a vlastní čísla do dokumentů Word.
draft: false
keywords:
- add bates numbering
- how to add bates
- add custom page numbers
- add sequential page numbers
- add custom numbers
language: cs
og_description: Přidejte Batesovo číslování v C# s jasným příkladem. Tento průvodce
  ukazuje, jak přidat vlastní čísla stránek, sekvenční čísla stránek a další.
og_title: Přidání Batesova číslování v C# – kompletní návod
tags:
- C#
- Document Processing
- Bates Numbering
title: Přidat Batesovo číslování v C# – Průvodce krok za krokem
url: /cs/net/programming-with-pdf-pages/add-bates-numbering-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Přidání Batesova číslování v C# – krok za krokem průvodce

Už jste se někdy zamysleli, jak **přidat Batesovo číslování** do dokumentu Word, aniž byste si trhali vlasy? Nejste v tom sami. V mnoha právních nebo compliance projektech potřebuje každá stránka jedinečný identifikátor a provádět to ručně je noční můra.  

V tomto tutoriálu projdeme kompletním, spustitelným příkladem, který **přidá Batesovo číslování**, ukáže vám **jak přidat bates** v několika řádcích a dokonce pokryje, jak **přidat vlastní čísla stránek** a **přidat sekvenční čísla stránek**, když je potřebujete. Na konci budete mít soubor .docx opatřený čísly, která si zvolíte — bez nutnosti třetích stran.

## Co se naučíte

- Načíst soubor DOCX pomocí Aspose.Words for .NET API (nebo jakékoli kompatibilní knihovny).  
- Nastavit **přidání vlastních čísel** jako předponu, počáteční hodnotu a velikost písma.  
- Aplikovat číslování na každou stránku jedním voláním.  
- Uložit výsledek a ověřit, že se čísla zobrazují podle očekávání.  

Předchozí zkušenost s Batesovým číslováním není vyžadována; stačí základní nastavení C# a kopie zdrojového dokumentu. Pojďme na to.

## Požadavky

- .NET 6+ (kód funguje jak na .NET Core, tak na .NET Framework).  
- Aspose.Words for .NET nainstalovaný přes NuGet (`Install-Package Aspose.Words`).  
- Dokument Word pojmenovaný `input.docx` umístěný ve složce, na kterou můžete odkazovat (`YOUR_DIRECTORY`).  
- Visual Studio, VS Code nebo jakékoli C# IDE, které máte rádi.

> **Tip:** Pokud používáte jinou knihovnu (např. Open XML SDK), principy zůstávají stejné — stačí vyměnit volání API.

## Krok 1: Načtení zdrojového dokumentu

Nejprve musíme načíst soubor Word do paměti.

```csharp
using Aspose.Words;

// Step 1: Load the source document
Document document = new Document("YOUR_DIRECTORY/input.docx");
```

*Proč je to důležité:* Načtení souboru vytvoří objekt `Document`, který vám poskytuje přístup ke stránkám, sekcím a nízkoúrovňovému stromu uzlů. Bez něj nemůžete přidat žádné číslování.

## Krok 2: Nastavení možností Batesova číslování

Nyní definujeme přesně, jak mají čísla vypadat. Zde **přidáte vlastní čísla stránek** nebo **přidáte sekvenční čísla stránek**.

```csharp
// Step 2: Define Bates numbering options (prefix, start number, font size)
BatesNumberingOptions batesOptions = new BatesNumberingOptions
{
    // Prefix that appears before every number, e.g., "ABC"
    Prefix = "ABC",
    // The first number in the sequence; change to 1 if you prefer
    Start = 1000,
    // Font size in points; 9 works well for most legal docs
    FontSize = 9
};
```

*Proč je to důležité:* `Prefix` vám umožní **přidat vlastní čísla**, například ID případu, zatímco `Start` určuje počáteční čítač. Změna `FontSize` zajistí, že čísla nebudou zasahovat do okrajů stránky.

## Krok 3: Aplikace Batesova číslování na každou stránku

S připravenými možnostmi řekneme knihovně, aby označila každou stránku.

```csharp
// Step 3: Apply Bates numbering to all pages of the document
document.Pages.AddBatesNumbering(batesOptions);
```

*Proč je to důležité:* Metoda `AddBatesNumbering` prochází interní kolekci stránek a vloží textové pole do pravého dolního rohu (výchozí umístění). Je to jádro **jak přidat bates** bez nutnosti psát smyčku sami.

## Krok 4: Uložení aktualizovaného dokumentu

Nakonec zapíšeme upravený soubor zpět na disk.

```csharp
// Step 4: Save the updated document
document.Save("YOUR_DIRECTORY/output.docx");
```

*Proč je to důležité:* Uložením vznikne nový `output.docx`, který můžete otevřít ve Wordu, LibreOffice nebo jakémkoli prohlížeči a ověřit, že se čísla zobrazují.

## Očekávaný výsledek

Otevřete `output.docx`. Každá stránka by měla zobrazovat něco jako:

```
ABC‑1000   (on page 1)
ABC‑1001   (on page 2)
ABC‑1002   (on page 3)
...
```

Pokud otevřete náhled tisku dokumentu, uvidíte čísla v pravém dolním rohu, odpovídající nastavené velikosti písma.

## Okrajové případy a varianty

| Situace | Co změnit | Proč |
|-----------|----------------|-----|
| **Žádná předpona není potřeba** | `Prefix = string.Empty` | Odstraní část “ABC‑”, zůstane jen číselná sekvence. |
| **Začít od 1** | `Start = 1` | Užitečné pro jednoduché **přidání sekvenčních čísel stránek** bez vlastní předpony. |
| **Velké dokumenty (>10 000 stránek)** | Zvyšte `FontSize` nebo upravte `Location` (použijte přetížení `AddBatesNumbering`) | Zabrání překrývání s patičkami nebo záhlavími. |
| **Zdrojový soubor jen pro čtení** | Otevřete s `LoadOptions`, které umožňují zápis, nebo nejprve soubor zkopírujte | Jinak `document.Save` vyvolá výjimku. |
| **Jiné umístění** | Použijte `batesOptions.Position = BatesNumberingPosition.TopLeft` (nebo jiný enum) | Některé firmy vyžadují čísla v horní části stránky. |

> **Poznámka:** Ne všechny knihovny poskytují třídu `BatesNumberingOptions`. S Open XML SDK byste vložili `TextBox` ručně — stejný princip, více kódu.

## Kompletní funkční příklad

Zde je celý program na jednom místě. Zkopírujte a vložte jej do konzolové aplikace a spusťte.

```csharp
using System;
using Aspose.Words;

class Program
{
    static void Main()
    {
        // Load the source document
        Document document = new Document("YOUR_DIRECTORY/input.docx");

        // Define Bates numbering options
        BatesNumberingOptions batesOptions = new BatesNumberingOptions
        {
            Prefix = "ABC",      // custom prefix
            Start = 1000,        // starting number
            FontSize = 9         // font size in points
        };

        // Apply numbering to every page
        document.Pages.AddBatesNumbering(batesOptions);

        // Save the result
        document.Save("YOUR_DIRECTORY/output.docx");

        Console.WriteLine("Bates numbering added successfully!");
    }
}
```

Spusťte program, otevřete `output.docx` a uvidíte číslování přesně tam, kde jste očekávali. 🎉

## Často kladené otázky

**Q: Můžu změnit barvu čísel?**  
A: Ano. Po zavolání `AddBatesNumbering` můžete získat vygenerované objekty `Shape` a nastavit jejich vlastnost `FillColor`.

**Q: Co když potřebuji čísla na levé straně místo pravé?**  
A: Použijte `batesOptions.Position = BatesNumberingPosition.BottomLeft` (nebo `TopLeft`, `TopRight`). API podporuje všechny čtyři rohy.

**Q: Funguje to i s výstupem do PDF?**  
A: Rozhodně. Po přidání číslování zavolejte `document.Save("output.pdf")`. Čísla jsou vykreslena do PDF stejně jako ve Wordu.

## Závěr

Nyní víte **jak přidat Batesovo číslování** do souboru Word pomocí C#. Tutoriál pokryl načtení dokumentu, nastavení **přidání vlastních čísel**, aplikaci **přidání sekvenčních čísel stránek** a uložení finálního výsledku. S kompletním ukázkovým kódem jej můžete vložit do libovolného projektu a okamžitě začít označovat dokumenty.

Jste připraveni na další výzvu? Zkuste to zkombinovat s dávkovým procesorem, který prochází složku souborů, nebo prozkoumejte **přidání vlastních čísel stránek** v záhlaví/patičce pro elegantnější vzhled. V každém případě máte pevný základ pro jakýkoli právní‑technologický nebo compliance automatizační úkol.

Máte otázky nebo zajímavý případ použití? Zanechte komentář níže a šťastné programování!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}