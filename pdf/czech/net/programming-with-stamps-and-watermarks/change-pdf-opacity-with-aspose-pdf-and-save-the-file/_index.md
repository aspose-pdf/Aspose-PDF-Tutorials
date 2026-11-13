---
category: general
date: 2026-11-12
description: Naučte se, jak změnit neprůhlednost PDF pomocí Aspose.Pdf, přidat průhlednost,
  nastavit režim prolnutí a uložit upravené PDF v C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- change PDF opacity
- how to add transparency
- save modified PDF
- how to set blend mode
- set fill opacity
language: cs
lastmod: 2026-11-12
og_description: Změňte neprůhlednost PDF pomocí Aspose.Pdf, naučte se, jak přidat
  průhlednost, nastavit režim prolnutí a uložit upravené PDF soubory v C#.
og_image_alt: Screenshot of a PDF page with altered opacity using Aspose.Pdf
og_title: Změňte průhlednost PDF pomocí Aspose.Pdf – přidejte průhlednost a uložte
schemas:
- author: Aspose
  dateModified: '2026-11-12'
  description: Learn how to change PDF opacity using Aspose.Pdf, add transparency,
    set blend mode, and save modified PDF in C#.
  headline: Change PDF opacity with Aspose.Pdf and save the file
  type: TechArticle
- description: Learn how to change PDF opacity using Aspose.Pdf, add transparency,
    set blend mode, and save modified PDF in C#.
  name: Change PDF opacity with Aspose.Pdf and save the file
  steps:
  - name: Load the PDF document
    text: Start by creating a `Document` instance that points to your source file.
      The constructor reads the entire PDF into memory, allowing you to manipulate
      its internal objects.
  - name: Access the first page’s resources
    text: Each PDF page stores a *resource dictionary* that holds objects such as
      fonts, images, and graphics states. You need to edit this dictionary to inject
      a new `ExtGState` entry.
  - name: Ensure an ExtGState dictionary exists
    text: The `ExtGState` dictionary holds custom graphics states. If it does not
      exist, the code creates one automatically.
  - name: Define a new graphics state (ExtGState)
    text: A graphics state defines how drawing operations behave. The following dictionary
      sets stroke opacity (`CA`), fill opacity (`ca`), and blend mode (`BM`).
  - name: Register the graphics state in the resource dictionary
    text: Give the new state a name (e.g., `GS0`) and add it to the `ExtGState` dictionary.
      This name will be referenced later in the page content stream.
  - name: Apply the graphics state to page content
    text: To actually see the opacity effect, insert the `/GS0 gs` operator before
      the drawing commands you want to affect. The example below draws a semi‑transparent
      rectangle.
  - name: Save the modified PDF
    text: Finally, write the updated document to disk. The `Save` method overwrites
      the target file or creates a new one if it does not exist.
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Změňte průhlednost PDF pomocí Aspose.Pdf a uložte soubor
url: /cs/net/programming-with-stamps-and-watermarks/change-pdf-opacity-with-aspose-pdf-and-save-the-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Změna opacity PDF pomocí Aspose.Pdf a uložení souboru

Pokud potřebujete **změnit opacity PDF** v dokumentu, Aspose.Pdf poskytuje jednoduché API pro úpravu průhlednosti jak obrysu, tak výplně. Tento tutoriál ukazuje přesně **jak přidat průhlednost**, **jak nastavit režim míchání** a **uložit upravené PDF** soubory pomocí několika řádků C# kódu.

Provedeme vás každým krokem – od načtení existujícího PDF po definování nového grafického stavu a uložení změn. Na konci tohoto průvodce budete umět:

* Snížit viditelnost vektorové grafiky nebo obrázků.
* Použít vlastní režim míchání, například *Normal* nebo *Multiply*.
* Exportovat aktualizovaný soubor bez ztráty jakéhokoli dalšího obsahu.

Jedinou podmínkou je funkční vývojové prostředí .NET a odkaz na knihovnu Aspose.Pdf (verze 23.9 nebo novější). Žádné externí nástroje nejsou vyžadovány.

## Požadavky

| Požadavek | Proč je důležité |
|-------------|----------------|
| .NET 6.0 SDK or later | Zajišťuje kompatibilitu s nejnovějšími API Aspose.Pdf. |
| Aspose.Pdf for .NET NuGet package | Poskytuje třídy `Document`, `CosPdfDictionary` a související třídy používané v kódu. |
| A PDF file to edit (e.g., `input.pdf`) | Slouží jako zdroj pro změny opacity. |

Nainstalujte NuGet balíček pomocí:

```bash
dotnet add package Aspose.Pdf
```

## Změna opacity PDF pomocí Aspose.Pdf

### Krok 1: Načtení PDF dokumentu

Začněte vytvořením instance `Document`, která ukazuje na váš zdrojový soubor. Konstruktor načte celé PDF do paměti, což vám umožní manipulovat s jeho vnitřními objekty.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Operators;
using Aspose.Pdf.XObjects;
using Aspose.Pdf.Facades;

// Load the existing PDF
var pdfDoc = new Document(@"YOUR_DIRECTORY\input.pdf");
```

> **Proč tento krok?** Načtení souboru vytvoří manipulovatelný objektový model. Všechny následné změny operují na této reprezentaci v paměti, což zajišťuje, že původní soubor zůstane nedotčený, dokud jej výslovně neuložíte.

### Krok 2: Přístup k prostředkům první stránky

Každá stránka PDF uchovává *slovník zdrojů*, který obsahuje objekty jako písma, obrázky a grafické stavy. Musíte tento slovník upravit a vložit nový záznam `ExtGState`.

```csharp
// Retrieve the first page (pages are 1‑based)
var page = pdfDoc.Pages[1];

// The DictionaryEditor simplifies access to the page's resource dictionary
var resourcesEditor = new DictionaryEditor(page.Resources);
```

> **Tip:** Pokud vaše PDF obsahuje více stránek, které potřebují stejnou opacity, opakujte tento krok pro každou stránku nebo sdílejte jeden `ExtGState` napříč stránkami.

### Krok 3: Zajistěte existenci slovníku ExtGState

`ExtGState` slovník obsahuje vlastní grafické stavy. Pokud neexistuje, kód jej vytvoří automaticky.

```csharp
// Get or create the ExtGState dictionary
var extGStateDict = resourcesEditor["ExtGState"]?.ToCosPdfDictionary()
                     ?? new CosPdfDictionary(pdfDoc);
resourcesEditor["ExtGState"] = extGStateDict;
```

> **Proč tento krok?** Bez kontejneru `ExtGState` by jakýkoli pokus o odkaz na nový grafický stav selhal, což by vedlo k PDF, které ignoruje vaše nastavení opacity.

### Krok 4: Definujte nový grafický stav (ExtGState)

Grafický stav určuje, jak se chovají kreslicí operace. Následující slovník nastavuje opacity obrysu (`CA`), opacity výplně (`ca`) a režim míchání (`BM`).

```csharp
// Create an empty dictionary for the new graphics state
var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDoc);

// Set desired parameters
var parameters = new[]
{
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),   // Stroke opacity (1 = opaque)
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // Fill opacity (0.5 = 50% transparent)
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // Blend mode
};

foreach (var param in parameters)
    newGraphicsState.Add(param);
```

> **Jak nastavit opacity výplně:** Položka `ca` řídí průhlednost vyplněných tvarů (text, cesty). Nastavte číselnou hodnotu mezi `0` (zcela průhledné) a `1` (zcela neprůhledné) podle požadavků vašeho designu.  
> **Jak nastavit režim míchání:** Položka `BM` vybírá algoritmus kompozice. Běžné hodnoty zahrnují `Normal`, `Multiply`, `Screen` a `Overlay`. Vyberte tu, která odpovídá vašemu vizuálnímu záměru.

### Krok 5: Zaregistrujte grafický stav ve slovníku zdrojů

Dejte novému stavu jméno (např. `GS0`) a přidejte jej do slovníku `ExtGState`. Toto jméno bude později odkazováno v proudu obsahu stránky.

```csharp
// Add the graphics state with a symbolic name
extGStateDict.Add("GS0", newGraphicsState);
```

> **Pro tip:** Používejte pojmenovací konvenci jako `GS0`, `GS1`, … při vytváření více stavů. Zabrání kolizím názvů a usnadní ladění.

### Krok 6: Použijte grafický stav na obsah stránky

Aby se efekt opacity skutečně projevil, vložte operátor `/GS0 gs` před kreslicí příkazy, které chcete ovlivnit. Níže uvedený příklad vykresluje poloprůhledný obdélník.

```csharp
// Build a content stream that uses the new graphics state
var content = new MemoryStream();
var writer = new StreamWriter(content);

// Activate the graphics state
writer.WriteLine("q");                 // Save graphics state
writer.WriteLine("/GS0 gs");           // Apply custom ExtGState
writer.WriteLine("0.2 0.5 0.8 rg");    // Set fill color (RGB)
writer.WriteLine("100 500 200 100 re"); // Rectangle (x y width height)
writer.WriteLine("f");                 // Fill rectangle
writer.WriteLine("Q");                 // Restore graphics state
writer.Flush();

content.Position = 0;
page.Contents.Add(new ContentStream(content));
```

> **Proč operátory `q` a `Q`?** Přidávají a odebírají stav grafiky ze zásobníku, čímž zajišťují, že změna opacity ovlivní jen obdélník a ne zbytek stránky.

### Krok 7: Uložte upravené PDF

Nakonec zapište aktualizovaný dokument na disk. Metoda `Save` přepíše cílový soubor nebo vytvoří nový, pokud neexistuje.

```csharp
// Persist the changes
pdfDoc.Save(@"YOUR_DIRECTORY\output.pdf");
```

> **Jak uložit upravené PDF:** Volání `Save` zapíše všechny úpravy v paměti, včetně nového `ExtGState`, na zadanou cestu. Výsledek můžete také streamovat do `MemoryStream` pro webové odpovědi.

## Kompletní funkční příklad

Níže je jeden samostatný program, který zahrnuje všechny výše popsané kroky. Zkopírujte jej do konzolové aplikace a spusťte, abyste ověřili změnu opacity.



## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy ve vašich projektech.

- [Jak uložit upravené PDF s Aspose.Pdf a přidat průhlednost](/pdf/english/net/document-manipulation/how-to-save-modified-pdf-with-aspose-pdf-and-add-transparenc/)
- [Jak přidat průhlednost do PDF pomocí Aspose.PDF v C#](/pdf/english/net/images-graphics/how-to-add-transparency-to-pdf-using-aspose-pdf-in-c/)
- [Jak přidat grafický stav do PDF a řídit průhlednost pomocí Aspose.PDF](/pdf/english/net/images-graphics/how-to-add-graphics-state-pdf-and-control-transparency-with/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}