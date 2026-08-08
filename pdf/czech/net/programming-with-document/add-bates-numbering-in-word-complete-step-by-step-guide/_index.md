---
category: general
date: 2026-06-21
description: Rychle přidejte Batesovo číslování ve Wordu. Naučte se, jak přidat Bates,
  použít Batesovo číslování pro právní dokumenty a automatizovat číslování pomocí
  C#.
draft: false
keywords:
- add bates numbering
- how to add bates
- bates numbering in word
- bates numbering for legal
- apply bates numbering
language: cs
og_description: Přidejte Batesovo číslování ve Wordu pomocí C#. Tento průvodce ukazuje,
  jak přidat Bates, použít Batesovo číslování pro právní dokumenty a automatizovat
  proces.
og_title: Přidání Batesova číslování ve Wordu – Kompletní programovací průvodce
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Add Bates numbering in Word quickly. Learn how to add Bates, apply
    Bates numbering for legal docs, and automate numbering with C#.
  headline: Add Bates Numbering in Word – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Add Bates numbering in Word quickly. Learn how to add Bates, apply
    Bates numbering for legal docs, and automate numbering with C#.
  name: Add Bates Numbering in Word – Complete Step‑by‑Step Guide
  steps:
  - name: Expected Output
    text: '| Page | Bates Number | |------|--------------| | 1 | ABC-1000 | | 2 |
      ABC-1001 | | … | … | | N | ABC‑(1000 + N‑1) |'
  - name: What if the document already contains page numbers?
    text: The `AddBatesNumbering` method will **not** overwrite existing page number
      fields; it simply adds a new field. If you want to replace the existing numbers,
      remove them first or set `batesOptions.Position` to the same location as the
      current page numbers.
  - name: Can I skip pages (e.g., exclude a cover page)?
    text: 'Yes. Use the overload that accepts a `PageRange`:'
  - name: How do I change the numbering format (Roman numerals, letters)?
    text: 'The `BatesNumberingOptions` class supports a `NumberFormat` property:'
  - name: What about performance on huge files?
    text: Loading a 2‑GB Word file can consume a lot of RAM. To mitigate, process
      the document in chunks using the `DocumentSplitter` utility, apply Bates numbering
      to each chunk, then merge the parts back together. This pattern keeps memory
      usage under control while still letting you **apply bates numbering*
  type: HowTo
tags:
- document‑automation
- csharp
- legal‑tech
title: Přidejte Batesovo číslování ve Wordu – kompletní průvodce krok za krokem
url: /cs/net/programming-with-document/add-bates-numbering-in-word-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Přidání Batesova číslování ve Wordu – Kompletní krok‑za‑krokem průvodce

Už jste se někdy ptali, jak přidat Batesovo číslování do souboru Word, aniž byste museli ručně psát každé číslo? Nejste sami. Mnoho právníků, asistentů a specialistů na e‑discovery potřebuje spolehlivý způsob, jak **přidat Batesovo číslování** na stovky stránek, a ruční provádění je noční můra.

V tomto tutoriálu projdeme čistým řešením v C#, které **aplikuje Batesovo číslování** na soubor `.docx`, vysvětlí, proč je každý řádek důležitý, a ukáže vám, jak upravit kód pro právní specifické potřeby. Na konci budete schopni během několika sekund vygenerovat dokonale očíslovaný dokument – bez nutnosti dalších pluginů.

## Co se naučíte

- Přesný kód potřebný k **přidání Batesova číslování** do dokumentu Word.  
- Jak funguje třída `BatesNumberingOptions` a proč byste mohli upravit předponu nebo počáteční hodnotu.  
- Tipy pro použití tohoto přístupu u velkých případových souborů, včetně úvah o paměti.  
- Rychlý přehled předpokladů, abyste mohli dnes zkopírovat‑vložit řešení a spustit jej.

**Předpoklady**  
- .NET 6+ (nebo .NET Framework 4.7.2+, pokud dáváte přednost staršímu runtime).  
- Odkaz na knihovnu Aspose.Words pro .NET (nebo jakékoli podobné API, které poskytuje `AddBatesNumbering`).  
- Základní znalost C# a Visual Studio (nebo vašeho oblíbeného IDE).

Pokud jste s tímto spokojeni, pojďme na to.

## Krok 1: Nastavení projektu a import knihovny

Nejprve vytvořte novou konzolovou aplikaci (nebo ji integrujte do existující služby). Poté přidejte NuGet balíček Aspose.Words:

```bash
dotnet add package Aspose.Words
```

> **Tip:** Použijte bezplatnou evaluační licenci pro testování; přidá malý vodoznak, ale jinak funguje přesně jako plná verze.

```csharp
using Aspose.Words;
using Aspose.Words.BatesNumbering;
```

Tyto `using` direktivy přinášejí třídy `Document` a `BatesNumberingOptions` do rozsahu, což je nezbytné pro krok **aplikace Batesova číslování** později.

## Krok 2: Načtení zdrojového dokumentu

Budete potřebovat soubor Word, na kterém budete pracovat. Níže uvedený kód načte `input.docx` ze složky, kterou určíte. Nahraďte `"YOUR_DIRECTORY"` skutečnou cestou na vašem počítači.

```csharp
// Step 1: Load the source document
var document = new Document("YOUR_DIRECTORY/input.docx");
```

Proč nejprve načíst soubor? Objekt `Document` parsuje celý balíček Word do paměti, což nám umožňuje manipulovat s hlavičkami, patičkami a rozvržením stránek před uložením. Pokud je soubor obrovský (např. 10 000 stránek), zvažte použití `LoadOptions` s `LoadFormat.Docx` pro streamování sekcí místo načtení všeho najednou.

## Krok 3: Konfigurace možností Batesova číslování

Zde se děje kouzlo. Řeknete knihovně, jakou předponu použít (`"ABC-"` v příkladu) a kde začít počítat (`1000`). Obě hodnoty jsou plně přizpůsobitelné.

```csharp
// Step 2: Define Bates numbering options (prefix and starting number)
var batesOptions = new BatesNumberingOptions
{
    Prefix = "ABC-",
    Start = 1000,
    // Optional: set the position, alignment, and font if you need legal‑specific styling
    // Position = BatesNumberingPosition.Footer,
    // Alignment = BatesNumberingAlignment.Right,
    // Font = new Font("Times New Roman", 10, FontStyle.Bold)
};
```

**Proč předpona?** V právní praxi předpony často identifikují případ nebo produkující stranu (`"ABC-"` může představovat *Acme Bank Corp.*). Začátek na `1000` je běžný, protože mnoho firem si vyhrazuje prvních 999 čísel pro interní návrhy.

Při práci s **Batesovým číslováním pro právní** dokumenty můžete také nastavit `batesOptions.Position` na `Header` nebo `Footer` a upravit zarovnání podle pravidel soudu. Knihovna tyto úpravy podporuje přímo.

## Krok 4: Aplikace Batesova číslování na celý dokument

Nyní skutečně vložíme čísla. Metoda `AddBatesNumbering` prochází každou stránku, vloží formátovaný řetězec a aktualizuje interní čítač stránek dokumentu.

```csharp
// Step 3: Apply Bates numbering to the entire document
document.AddBatesNumbering(batesOptions);
```

Na pozadí Aspose.Words vytvoří na každé stránce skryté pole, které se vykreslí jako `ABC-1000`, `ABC-1001` a tak dále. Protože je to pole, můžete později upravit předponu nebo počáteční číslo bez nutnosti regenerovat celý soubor – užitečné pro **jak přidat bates** po změně požadavku na discovery.

## Krok 5: Uložení upraveného dokumentu

Na závěr zapište výstup do nového souboru. Zachování originálu nedotčeného je nejlepší praxe, zejména při práci s důkazy, které musí zůstat nedotčeny.

```csharp
// Step 4: Save the modified document
document.Save("YOUR_DIRECTORY/output.docx");
```

Nyní máte `output.docx` s postupnými Batesovými čísly připojenými ke každé stránce. Otevřete jej ve Wordu a uvidíte čísla přesně tam, kde jste je určili (ve výchozím nastavení v patičce). Velikost souboru může mírně vzrůst kvůli extra polím, ale je to zanedbatelné ve srovnání s výhodami.

### Očekávaný výstup

| Page | Bates Number |
|------|--------------|
| 1    | ABC-1000     |
| 2    | ABC-1001     |
| …    | …            |
| N    | ABC‑(1000 + N‑1) |

Při otevření zobrazení „Kódy polí“ dokumentu (`Alt+F9` ve Wordu) uvidíte na každé stránce něco jako `{ BATES \* MERGEFORMAT ABC-1000 }`.

## Okrajové případy a časté otázky

### Co když dokument již obsahuje čísla stránek?

Metoda `AddBatesNumbering` **nepřepíše** existující pole s čísly stránek; jednoduše přidá nové pole. Pokud chcete nahradit existující čísla, odstraňte je nejprve nebo nastavte `batesOptions.Position` na stejné místo jako aktuální čísla stránek.

### Mohu přeskočit stránky (např. vyloučit titulní stránku)?

Ano. Použijte přetížení, které přijímá `PageRange`:

```csharp
var range = new PageRange(2, document.PageCount); // start at page 2
document.AddBatesNumbering(batesOptions, range);
```

Toto je užitečné, když potřebujete **Batesovo číslování pro právní** podání, která začínají po titulní stránce.

### Jak změním formát číslování (římské číslice, písmena)?

Třída `BatesNumberingOptions` podporuje vlastnost `NumberFormat`:

```csharp
batesOptions.NumberFormat = BatesNumberFormat.RomanUpper;
```

Nastavte ji před voláním `AddBatesNumbering`. Tato flexibilita pomáhá, když soud vyžaduje konkrétní styl.

### Co výkon s obrovskými soubory?

Nahrání 2‑GB souboru Word může spotřebovat hodně RAM. Pro zmírnění zpracovávejte dokument po částech pomocí nástroje `DocumentSplitter`, aplikujte Batesovo číslování na každou část a poté je spojte zpět. Tento vzor udržuje využití paměti pod kontrolou a přitom vám umožní **aplikovat Batesovo číslování** efektivně.

## Kompletní funkční příklad

Spojením všeho dohromady, zde je připravený ke spuštění konzolový program:

```csharp
using System;
using Aspose.Words;
using Aspose.Words.BatesNumbering;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the source document
            var inputPath = @"C:\Docs\input.docx";
            var document = new Document(inputPath);

            // 2️⃣ Define Bates numbering options
            var batesOptions = new BatesNumberingOptions
            {
                Prefix = "ABC-",
                Start = 1000,
                // Optional styling for legal compliance
                Position = BatesNumberingPosition.Footer,
                Alignment = BatesNumberingAlignment.Right,
                Font = new Font("Times New Roman", 9, FontStyle.Bold)
            };

            // 3️⃣ Apply Bates numbering across all pages
            document.AddBatesNumbering(batesOptions);

            // 4️⃣ Save the result
            var outputPath = @"C:\Docs\output.docx";
            document.Save(outputPath);

            Console.WriteLine($"✅ Bates numbering applied! Saved to {outputPath}");
        }
    }
}
```

Spusťte program, otevřete `output.docx` a uvidíte čistou řadu čísel připravených k podání, discovery nebo soudnímu předložení.

## Závěr

Nyní přesně víte **jak přidat Bates** do dokumentu Word pomocí C#. Kroky – načtení, konfigurace, aplikace a uložení – jsou jednoduché, ale dostatečně flexibilní pro **Batesovo číslování pro právní** pracovní postupy, vlastní předpony a dokonce i zpracování ve velkém měřítku.

Pokud jste připraveni jít dál, zvažte:

- Integraci kódu do webového API, aby kolegové mohli nahrávat soubory a okamžitě získat očíslované PDF.  
- Přidání ošetření chyb pro chybějící soubory nebo problémy s oprávněním (rychlý `try/catch` kolem `Document.Load`).  
- Prozkoumání dalších funkcí Aspose.Words, jako jsou vodoznaky nebo redakce, pro kompletní sadu e‑discovery nástrojů.

Klidně experimentujte s různými předponami, počátečními čísly nebo dokonce kombinujte více číslovacích schémat v jednom dokumentu. Svět **aplikace Batesova číslování** je překvapivě všestranný, jakmile máte základní logiku pod kontrolou.

Máte otázky nebo složitý scénář? Zanechte komentář níže a společně to vyřešíme. Šťastné kódování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční příklady kódu s krok‑za‑krokem vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Apply Numbering Style in Heading of PDF using Java](/pdf/english/java/pdf-images/apply-numbering-style-in-heading-of-pdf-using-java/)
- [Apply Numbering Style In Heading Of Pdf Using Java](/pdf/german/java/pdf-images/apply-numbering-style-in-heading-of-pdf-using-java/)
- [Apply Numbering Style In Heading Of Pdf Using Java](/pdf/french/java/pdf-images/apply-numbering-style-in-heading-of-pdf-using-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}