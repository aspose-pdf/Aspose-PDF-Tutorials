---
category: general
date: 2026-08-20
description: Vytvořte vlastní grafický stav v PDF pomocí Aspose.Pdf. Naučte se, jak
  upravit zdroje PDF a přidat průhlednost do PDF během několika kroků.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create custom graphics state
- edit pdf resources
- add transparency pdf
- Aspose.Pdf graphics state
- PDF resource dictionary
language: cs
lastmod: 2026-08-20
og_description: Vytvořte vlastní grafický stav v PDF pomocí Aspose.Pdf. Tento tutoriál
  ukazuje, jak rychle upravit zdroje PDF a přidat průhlednost do PDF.
og_image_alt: Screenshot of C# code that creates a custom graphics state in a PDF
og_title: Vytvořte vlastní grafický stav v PDF – průvodce Aspose.Pdf
schemas:
- author: Aspose
  dateModified: '2026-08-20'
  description: Create custom graphics state in PDF with Aspose.Pdf. Learn how to edit
    PDF resources and add transparency PDF in just a few steps.
  headline: Create custom graphics state in PDF using Aspose.Pdf
  type: TechArticle
tags:
- PDF
- Aspose.Pdf
- C#
- Graphics state
title: Vytvořte vlastní grafický stav v PDF pomocí Aspose.Pdf
url: /cs/net/programming-with-operators/create-custom-graphics-state-in-pdf-using-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření vlastního grafického stavu v PDF pomocí Aspose.Pdf

Pokud potřebujete **vytvořit vlastní grafický stav** v PDF, tento návod vám přesně ukáže, jak to provést pomocí Aspose.Pdf pro .NET. Na konci tutoriálu budete schopni **upravit PDF zdroje**, vložit nový slovník grafických stavů a **přidat transparentní PDF** obsah, aniž byste opustili svůj C# projekt.

Uvidíte kompletní, spustitelný příklad, vysvětlení, proč je každý řádek důležitý, a tipy pro práci s více‑stránkovými dokumenty nebo různými režimy míchání. Žádné externí nástroje nejsou potřeba — stačí knihovna Aspose.Pdf a základní vývojové prostředí .NET.

## Požadavky

* .NET 6.0 nebo novější (kód také funguje s .NET Framework 4.7+)
* Licencovaná kopie **Aspose.Pdf for .NET** (bezplatná zkušební verze funguje pro testování)
* Vstupní PDF soubor pojmenovaný `input.pdf` umístěný ve složce, na kterou můžete odkazovat z kódu
* Visual Studio 2022 nebo jakékoli IDE podporující vývoj v C#

Tutoriál předpokládá, že jste obeznámeni se základní syntaxí C# a pojmem PDF stránky.

## Krok 1: Načtení zdrojového PDF a přístup k první stránce

Prvním krokem je otevřít PDF soubor a získat stránku, jejíž zdroje chcete upravit. Aspose.Pdf představuje každou stránku jako objekt `Page` a každá stránka obsahuje **slovník zdrojů**, který ukládá grafické stavy, písma, XObjecty a další.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Operators;
using Aspose.Pdf.InteractiveFeatures;
using Aspose.Pdf.Text;
using Aspose.Pdf.Facades;
using System.Collections.Generic;

// Load the PDF you want to edit
using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
{
    // Get the first page (pages are 1‑based in Aspose.Pdf)
    Page firstPage = pdfDocument.Pages[1];
```

*Proč je to důležité:* Třída `Document` načte soubor do paměti a `Pages[1]` vám poskytne přímý přístup ke slovníku zdrojů první stránky, kde se nachází grafický stav.

## Krok 2: Otevření slovníku zdrojů pro úpravy

Aspose.Pdf poskytuje pomocníka `DictionaryEditor`, který vám umožní zacházet se slovníkem zdrojů jako s běžným .NET `Dictionary`. To usnadňuje čtení, přidávání nebo nahrazování položek, jako je `ExtGState`.

```csharp
    // Create an editor for the page’s resources
    var resourcesEditor = new DictionaryEditor(firstPage.Resources);
```

*Proč je to důležité:* `DictionaryEditor` abstrahuje nízkoúrovňové COS objekty, což vám umožní pracovat se známými páry klíč/hodnota a zároveň zachovat soulad s PDF.

## Krok 3: Získání (nebo vytvoření) slovníku ExtGState

**ExtGState** položka obsahuje všechny externí objekty grafického stavu pro stránku. Pokud slovník neexistuje, Aspose.Pdf pro vás vytvoří prázdný.

```csharp
    // Ensure the ExtGState dictionary exists
    var extGStateDict = resourcesEditor.ContainsKey("ExtGState")
        ? resourcesEditor["ExtGState"].ToCosPdfDictionary()
        : new CosPdfDictionary(pdfDocument);
```

*Proč je to důležité:* Chybějící položka `ExtGState` by později způsobila `KeyNotFoundException`. Tato ochrana umožňuje kódu fungovat i na PDF, která dosud neobsahovala vlastní grafický stav — zásadní část robustnosti **edit PDF resources**.

## Krok 4: Vytvoření vlastního slovníku grafického stavu

Grafický stav popisuje, jak jsou vykreslovány kreslicí operace. Pro **přidání transparentního PDF** musíte nastavit položky `ca` (průhlednost výplně) a `CA` (průhlednost tahu) a volitelně režim míchání (`BM`). Následující kód vytvoří nový slovník s těmito parametry.

```csharp
    // Create an empty dictionary that will become the new graphics state
    var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

    // Define the parameters you want for the custom state
    var graphicsStateParams = new KeyValuePair<string, ICosPdfPrimitive>[]
    {
        // Stroke opacity (1 = fully opaque)
        new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
        // Fill opacity (0.5 = 50 % transparent)
        new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
        // Blend mode – "Normal" is the default, but you can use "Multiply", "Screen", etc.
        new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
    };

    // Populate the dictionary with the parameters
    foreach (var param in graphicsStateParams)
        newGraphicsState.Add(param);
```

*Proč je to důležité:* Položky `ca` a `CA` řídí průhlednost výplně a tahu. Nastavení `BM` vám umožní experimentovat s různými efekty kompozice, což je užitečné, když později **přidáváte transparentní PDF** obsah, jako jsou poloprůhledné tvary nebo obrázky.

## Krok 5: Registrace nového grafického stavu pod jedinečným názvem

Každý grafický stav ve slovníku `ExtGState` musí mít jedinečný název (např. `GS0`, `GS1`). Můžete zvolit libovolný název, který nekoliduje s existujícími položkami.

```csharp
    // Choose a name that is unlikely to collide with existing states
    const string graphicsStateName = "GS0";

    // Add the new graphics state to the ExtGState dictionary
    extGStateDict.Add(graphicsStateName, newGraphicsState);

    // If the ExtGState entry was missing, attach it back to the page resources
    if (!resourcesEditor.ContainsKey("ExtGState"))
        resourcesEditor["ExtGState"] = extGStateDict;
```

*Proč je to důležité:* Vložením nového slovníku pod `GS0` umožníte, aby byl stav přístupný ze streamů obsahu stránky. Podmíněný blok zajišťuje, že položka `ExtGState` je přítomna i u PDF, které ji neměly od začátku — další ochrana **edit PDF resources**.

## Krok 6: Použití vlastního grafického stavu v obsahu stránky (volitelné)

Předchozí kroky pouze *definují* grafický stav. Aby se efekt projevil, musíte na něj odkazovat v proudu obsahu stránky. Níže je rychlý příklad, který vykreslí poloprůhledný obdélník pomocí právě vytvořeného stavu.

```csharp
    // Get the page’s content stream (or create a new one if empty)
    var content = firstPage.Contents[1];
    var graphics = new ContentWriter(content);

    // Save current graphics state
    graphics.WriteOperator(OperatorName.SaveState);
    // Set the custom graphics state we just defined
    graphics.WriteOperand($"/{graphicsStateName}");
    graphics.WriteOperator(OperatorName.SetExtGState);
    // Draw a rectangle (coordinates are in points)
    graphics.WriteOperand(100);   // lower‑left x
    graphics.WriteOperand(500);   // lower‑left y
    graphics.WriteOperand(200);   // width
    graphics.WriteOperand(100);   // height
    graphics.WriteOperator(OperatorName.Rectangle);
    // Fill the rectangle using the current fill opacity (ca = 0.5)
    graphics.WriteOperator(OperatorName.Fill);
    // Restore the previous graphics state
    graphics.WriteOperator(OperatorName.RestoreState);
```

*Proč je to důležité:* Operátor `SetExtGState` (`gs`) říká rendereru PDF, aby použil parametry definované v `GS0`. Obdélník se zobrazí s 50 % průhledností výplně, zatímco jeho tah zůstane plně neprůhledný.

## Krok 7: Uložení upraveného PDF

Nakonec změny zapíšete zpět na disk. Můžete přepsat původní soubor nebo vytvořit nový.

```csharp
    // Save the updated PDF
    pdfDocument.Save("YOUR_DIRECTORY/output_with_custom_gs.pdf");
}
```

Když otevřete `output_with_custom_gs.pdf` v prohlížeči PDF, měli byste na první stránce vidět poloprůhledný obdélník. To potvrzuje, že jste úspěšně **vytvořili vlastní grafický stav**, **upravili PDF zdroje** a **přidali transparentní PDF** obsah.

## Běžné varianty a okrajové případy

| Situace | Co upravit |
|-----------|----------------|
| **Více stránek potřebuje stejný stav** | Zaregistrujte grafický stav jednou (kroky 1‑5) a odkažte na `GS0` v proudu obsahu libovolné stránky. |
| **Různá průhlednost pro jednotlivé prvky** | Definujte další stavy (`GS1`, `GS2`, …) s různými hodnotami `ca`/`CA` a přepínejte mezi nimi pomocí `SetExtGState`. |
| **Režim míchání jiný než Normal** | Nahraďte `"Normal"` hodnotou `"Multiply"`, `"Screen"` nebo jakýmkoli standardním PDF režimem míchání v položce `BM`. |
| **Kolize názvů** | Před přidáním zkontrolujte `extGStateDict.ContainsKey(yourName)` a v případě potřeby zvolte jedinečnou příponu. |
| **PDF již obsahuje slovník ExtGState** | Kód v kroku 3 již znovu používá existující slovník, takže není potřeba žádná další manipulace. |

**Tip:** Při práci s velkými PDF obalte používání `Document` do bloku `using` (jak je ukázáno), aby se rychle uvolnily nativní zdroje. Také zvažte povolení vlastnosti `PdfCompliance` v Aspose.Pdf, pokud potřebujete zajistit soulad s PDF/A nebo PDF/X po úpravě zdrojů.

## Kompletní funkční příklad

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Operators;
using Aspose.Pdf.InteractiveFeatures;
using Aspose.Pdf.Text;
using Aspose.Pdf.Facades;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        // Load the PDF you want to edit
        using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
        {
            // Step 1: Get the first page
            Page firstPage = pdfDocument.Pages[1];

            // Step 2: Open the page resources for editing
            var resourcesEditor = new DictionaryEditor(firstPage.Resources);

            // Step 3: Retrieve or create the ExtGState dictionary
            var extGStateDict = resourcesEditor.ContainsKey("ExtGState")
                ? resourcesEditor["ExtGState"].ToCosPdfDictionary()
                : new CosPdfDictionary(pdfDocument);

            // Step 4: Build a custom graphics state (50 % fill opacity, 100 % stroke opacity)
            var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            var graphicsStateParams = new KeyValuePair<string, ICosPdfPrimitive>[]
            {
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
            };
            foreach (var param in graphicsStateParams)
                newGraphicsState.Add(param);

            // Step 5: Register the graphics state under the name GS0
            const string graphicsStateName = "GS0";
            extGStateDict.Add(graphicsStateName, newGraphics


## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která navazují na techniky předvedené v tomto návodu. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, aby vám pomohly zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Jak vytvořit PDF s Aspose – Přidat formulářové pole a stránky](/pdf/english/net/programming-with-forms/how-to-create-pdf-with-aspose-add-form-field-and-pages/)
- [Jak vytvořit vlastní tabulky v PDF pomocí Aspose.PDF .NET](/pdf/english/net/tables-lists/create-custom-tables-in-pdfs-aspose-pdf-dot-net/)
- [Vytvořit vlastní PDF razítka Aspose Pdf Net](/pdf/hongkong/net/images-graphics/create-custom-pdf-stamps-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}