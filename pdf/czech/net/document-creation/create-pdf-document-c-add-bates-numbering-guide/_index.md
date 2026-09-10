---
category: general
date: 2026-02-28
description: Vytvořte PDF dokument v C# s Batesovým číslováním. Naučte se, jak přidat
  Batesovo číslování do PDF, nastavit předpony a generovat sekvenční čísla PDF v jednom
  průvodci.
draft: false
keywords:
- create pdf document c#
- add bates numbering pdf
- how to add bates
- add document identification numbers
- add sequential pdf numbers
language: cs
og_description: Vytvořte PDF dokument v C# s Batesovým číslováním. Tento tutoriál
  ukazuje, jak přidat Batesovo číslování do PDF, nastavit vlastní předpony a vytvořit
  sekvenční čísla PDF.
og_title: Vytvořit PDF dokument v C# – Přidat Batesovo číslování
tags:
- Aspose.PDF
- C#
- PDF automation
title: Vytvořte PDF dokument v C# – Průvodce přidáním Batesova číslování
url: /cs/net/document-creation/create-pdf-document-c-add-bates-numbering-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření PDF dokumentu v C# – Průvodce přidáním Bates číslování

Už jste se někdy zamýšleli, jak **vytvořit PDF dokument v C#**, který už má na každé stránce unikátní identifikátor? To je častý problém, když potřebujete sledovat právní soubory, soudní podání nebo jakýkoli svazek PDF, který musí být vyhledatelný podle čísla. Dobrá zpráva? S Aspose.PDF můžete přidat Bates čísla pomocí několika řádků kódu – bez ruční úpravy.

V tomto průvodci projdeme celý proces: načtení existujícího PDF, nastavení **add bates numbering pdf**, aplikaci čísel a nakonec uložení výsledku. Na konci budete schopni **add document identification numbers** a dokonce **add sequential PDF numbers** automaticky, vše z C#.

## Požadavky

- .NET 6.0 nebo novější (API funguje také s .NET Framework 4.5+)
- Licencovaná kopie **Aspose.PDF for .NET** (zkušební verze stačí pro testování)
- Vstupní PDF soubor, který chcete očíslovat (budeme ho nazývat `input.pdf`)
- Visual Studio 2022 (nebo jakékoli jiné IDE dle preference)

Žádné další NuGet balíčky kromě Aspose.PDF nejsou potřeba.

![Create PDF Document C# with Bates numbering](https://example.com/image.png "Create PDF Document C# example")

## Krok 1: Načtení zdrojového PDF dokumentu

Než budete moci **add bates numbering pdf**, potřebujete objekt `Document`, který představuje soubor na disku.

```csharp
using Aspose.Pdf;

// Load the source PDF document
var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");
```

*Proč je to důležité*: Třída `Document` je vstupním bodem pro každou operaci v Aspose.PDF. Abstrahuje souborový systém, takže můžete pracovat se stránkami, anotacemi a metadaty, aniž byste se museli zabývat surovými bajty.

> **Tip:** Pokud zpracováváte mnoho souborů ve smyčce, znovu použijte stejnou instanci `Document` jen tehdy, když je zdroj identický; jinak vytvořte nový objekt pro každý soubor, aby nedošlo k únikům paměti.

## Krok 2: Definování možností Bates číslování

Zde se část **how to add bates** stává konkrétní. Nakonfigurujete objekt `BatesNumberingOptions`, který řekne Aspose, jaký má být prefix, kde začít a jak velké má být písmo.

```csharp
// Define Bates numbering options (prefix, start number, font size)
var batesOptions = new BatesNumberingOptions
{
    Prefix = "ABC-",   // You can change this to any string you need
    Start = 1000,      // Starting number – useful for continuous numbering across batches
    FontSize = 9       // Small enough to fit in the margin but still readable
};
```

*Proč je to důležité*: `Prefix` vám umožní vložit identifikátor případu (např. “ABC-”). Vlastnost `Start` je nezbytná, když **adding sequential PDF numbers** napříč více dokumenty – stačí ji postupně zvyšovat. A `FontSize` zajistí, že čísla nebudou překrývat existující obsah.

## Krok 3: Aplikace Bates číslování na celý dokument

Nyní skutečně přidáme čísla na každou stránku. Třída `BatesNumbering` provede veškerou těžkou práci.

```csharp
// Apply Bates numbering to the entire document
var bates = new BatesNumbering();
bates.AddBatesNumbering(pdfDocument, batesOptions);
```

*Proč je to důležité*: V pozadí Aspose prochází každou stránku, vypočítá odpovídající číslo (Prefix + (Start + pageIndex)) a vykreslí jej ve výchozím nastavení v pravém dolním rohu. Pozici můžete později upravit, ale výchozí nastavení funguje pro většinu právních dokumentů.

> **Často kladená otázka:** *Co když potřebuji očíslovat jen podmnožinu stránek?*  
> Použijte přetížení `AddBatesNumbering(Document, BatesNumberingOptions, int startPage, int endPage)` a omezte rozsah.

## Krok 4: Uložení PDF s aplikovaným Bates číslováním

Poslední krok je zapsat upravený dokument zpět na disk.

```csharp
// Save the PDF with Bates numbers applied
pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
```

*Proč je to důležité*: Metoda `Save` respektuje původní formát souboru, takže získáte standardní PDF, které může otevřít jakýkoli prohlížeč – s **add document identification numbers** na každé stránce.

## Kompletní funkční příklad

Spojením všech částí získáte samostatný program, který můžete vložit do nové konzolové aplikace a okamžitě spustit.

```csharp
using System;
using Aspose.Pdf;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the source PDF document
            var inputPath = @"YOUR_DIRECTORY/input.pdf";
            var pdfDocument = new Document(inputPath);

            // 2️⃣ Define Bates numbering options (prefix, start number, font size)
            var batesOptions = new BatesNumberingOptions
            {
                Prefix = "ABC-",
                Start = 1000,
                FontSize = 9
            };

            // 3️⃣ Apply Bates numbering to the entire document
            var bates = new BatesNumbering();
            bates.AddBatesNumbering(pdfDocument, batesOptions);

            // 4️⃣ Save the PDF with Bates numbers applied
            var outputPath = @"YOUR_DIRECTORY/output.pdf";
            pdfDocument.Save(outputPath);

            Console.WriteLine($"Bates numbering added successfully. Output saved to {outputPath}");
        }
    }
}
```

**Očekávaný výsledek:** Otevřete `output.pdf` v libovolném prohlížeči; uvidíte “ABC‑1000”, “ABC‑1001”, … vytištěné v pravém dolním rohu každé stránky. Čísla jsou textové, takže jsou vyhledatelná a lze je kopírovat – přesně to, co očekáváte od správné implementace **add sequential PDF numbers**.

## Okrajové případy a varianty

### Vlastní umístění

Pokud výchozí roh koliduje s existujícími zápatími, můžete posunout umístění:

```csharp
batesOptions.Position = new Position(10, 10); // X, Y from the bottom‑left
```

### Různé formáty čísel

Chcete čísla s nulovým doplněním (např. 001000)? Použijte `NumberFormat`:

```csharp
batesOptions.NumberFormat = "D6"; // Pads to 6 digits
```

### Více souborů v dávce

Při zpracování mnoha PDF udržujte běžící čítač:

```csharp
int globalStart = 5000;
foreach (var file in Directory.GetFiles(@"YOUR_DIRECTORY\Batch", "*.pdf"))
{
    var doc = new Document(file);
    var opts = new BatesNumberingOptions
    {
        Prefix = "BATCH-",
        Start = globalStart,
        FontSize = 9
    };
    new BatesNumbering().AddBatesNumbering(doc, opts);
    doc.Save(Path.ChangeExtension(file, ".bated.pdf"));
    globalStart += doc.Pages.Count; // Increment for the next file
}
```

### Zpracování PDF chráněných heslem

Pokud je zdrojové PDF šifrované, předávejte heslo při vytváření objektu `Document`:

```csharp
var pdfDocument = new Document("protected.pdf", new LoadOptions { Password = "mySecret" });
```

## Často kladené otázky

| Question | Answer |
|----------|--------|
| **Can I use a different library?** | Yes, libraries like iTextSharp or PdfSharp also support page‑level text insertion, but Aspose.PDF offers the most straightforward API for Bates numbering. |
| **Does this affect file size?** | Adding a few bytes of text per page is negligible; the output size typically grows by less than 1 KB per page. |
| **Is the numbering searchable?** | Absolutely. Aspose writes the numbers as text objects, not as images, so they’re indexed by PDF readers. |
| **What if I need a different font?** | Set `batesOptions.Font` to a `Font` object (e.g., `FontRepository.FindFont("Arial")`). |

## Závěr

Ukázali jsme, jak **vytvořit PDF dokument v C#** a okamžitě **add bates numbering pdf** pomocí Aspose.PDF. Proces je jednoduchý, spolehlivý a plně programovatelný – ideální pro právnické firmy, vládní úřady nebo jakoukoli organizaci, která musí **add document identification numbers** a **add sequential PDF numbers** do velkých šarží souborů.

Využijte tento základ a experimentujte: zkuste různé prefixy pro různé oddělení, propojte číslování napříč více soubory, nebo přidejte QR kódy vedle Bates čísel pro extra sledovatelnost. Možnosti jsou neomezené, jakmile máte základní workflow pod kontrolou.

Pokud se vám tento tutoriál hodil, sdílejte ho, zanechte komentář nebo prozkoumejte naše další návody na manipulaci s PDF v C#. Šťastné kódování!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}