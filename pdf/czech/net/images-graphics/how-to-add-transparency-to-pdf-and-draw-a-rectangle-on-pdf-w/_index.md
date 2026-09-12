---
category: general
date: 2026-09-12
description: Naučte se, jak přidat průhlednost do PDF, nakreslit obdélník v PDF a
  uložit PDF s průhledností pomocí Aspose.PDF v C# – krok za krokem průvodce.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add transparency to pdf
- draw rectangle on pdf
- save pdf with transparency
language: cs
lastmod: 2026-09-12
og_description: Přidejte průhlednost do PDF, nakreslete obdélník do PDF a uložte PDF
  s průhledností pomocí Aspose.PDF v C#. Sledujte tento kompletní návod.
og_image_alt: Screenshot of a PDF page showing a semi‑transparent rectangle drawn
  with Aspose.PDF
og_title: Přidejte průhlednost do PDF a nakreslete obdélník v PDF – kompletní průvodce
  C#
schemas:
- author: Aspose
  dateModified: '2026-09-12'
  description: Learn how to add transparency to PDF, draw a rectangle on PDF, and
    save PDF with transparency using Aspose.PDF in C# – step‑by‑step guide.
  headline: How to add transparency to PDF and draw a rectangle on PDF with Aspose.PDF
  type: TechArticle
tags:
- Aspose.PDF
- C#
- PDF manipulation
title: Jak přidat průhlednost do PDF a nakreslit obdélník do PDF pomocí Aspose.PDF
url: /cs/net/images-graphics/how-to-add-transparency-to-pdf-and-draw-a-rectangle-on-pdf-w/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak přidat průhlednost do PDF a nakreslit obdélník v PDF pomocí Aspose.PDF

Pokud potřebujete **přidat průhlednost do PDF** souborů, tento návod vám přesně ukáže, jak to provést v C#. Také se naučíte, jak **nakreslit obdélník v PDF** a nakonec **uložit PDF s průhledností**, aby výsledek mohl být znovu použit v reportech, fakturách nebo jakémkoli workflow automatizace dokumentů.

V tomto tutoriálu se naučíte:

* Načíst existující PDF dokument.
* Vytvořit vlastní grafický stav, který určuje průhlednost obrysu a výplně.
* Použít tento grafický stav na plátno a nakreslit obdélník.
* Uložit upravený soubor při zachování nastavení průhlednosti.

Kromě knihovny Aspose.PDF pro .NET nejsou potřeba žádné externí nástroje a každý řádek kódu je vysvětlen, abyste pochopili *proč* je každý krok důležitý.

## Požadavky

* .NET 6.0 nebo novější (kód také funguje s .NET Framework 4.7+).
* Licencovaná nebo zkušební kopie **Aspose.PDF pro .NET**. Nainstalujte ji pomocí NuGet:

```bash
dotnet add package Aspose.Pdf
```

* Vstupní PDF (`input.pdf`) umístěné ve složce, na kterou můžete odkazovat z vašeho projektu.

## Krok 1: Načtení PDF dokumentu

První operací je otevřít zdrojový soubor. Použití příkazu `using` zajišťuje, že dokument bude řádně uvolněn, což později při pokusu o uložení zabraňuje problémům se zamčením souboru.

```csharp
// Step 1: Load the PDF document
string pdfPath = @"YOUR_DIRECTORY\input.pdf";
using var pdfDocument = new Aspose.Pdf.Document(pdfPath);
```

*Proč je to důležité*: Načtení dokumentu vám poskytuje přístup ke kolekci stránek, slovníkům zdrojů a objektům plátna potřebným pro kreslení.

## Krok 2: Přístup ke slovníku zdrojů první stránky

Každá stránka PDF má **slovník zdrojů**, který ukládá objekty jako písma, obrázky a grafické stavy. Pro zavedení nového nastavení průhlednosti musíme upravit položku `ExtGState`.

```csharp
// Step 2: Access the first page and its resource dictionary
var firstPage = pdfDocument.Pages[1];               // PDF pages are 1‑based
var resourcesEditor = new Aspose.Pdf.DictionaryEditor(firstPage.Resources);
```

*Proč je to důležité*: `DictionaryEditor` nám umožňuje číst a upravovat nízkoúrovňové PDF objekty, aniž by došlo k poškození struktury dokumentu.

## Krok 3: Vytvoření vlastního grafického stavu s hodnotami průhlednosti

Grafický stav (`ExtGState`) řídí, jak jsou vykreslovány kreslicí operace. Definujeme dva parametry průhlednosti:

* **CA** – průhlednost obrysu (kontury tvarů).
* **ca** – průhlednost výplně (vnitřek tvarů).

Také nastavíme režim prolnutí (`BM`) na „Normal“, což je nejčastější operace kompozice.

```csharp
// Step 3: Create a custom graphics state (ExtGState) with transparency settings
var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
var customGs = Aspose.Pdf.Cos.CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

var parameters = new[]
{
    new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
        "CA", new Aspose.Pdf.Cos.CosPdfNumber(1)),          // stroke opacity = 100 %
    new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
        "ca", new Aspose.Pdf.Cos.CosPdfNumber(0.5)),        // fill opacity = 50 %
    new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
        "BM", new Aspose.Pdf.Cos.CosPdfName("Normal"))      // normal blend mode
};

foreach (var p in parameters)
    customGs.Add(p);

// Register the new graphics state under the name "GS0"
extGStateDict.Add("GS0", customGs);
```

*Proč je to důležité*: Přidáním `GS0` do slovníku `ExtGState` vytvoříme znovupoužitelnou referenci, kterou může plátno aktivovat před kreslením. Průhlednost výplně `0.5` způsobí, že obdélník bude poloprůhledný, čímž dosáhneme cíle **přidat průhlednost do PDF**.

## Krok 4: Použití grafického stavu a nakreslení obdélníku

Nyní řekneme plátnu stránky, aby použilo grafický stav, který jsme právě vytvořili, a poté nakreslíme obdélník. Souřadnice odpovídají souřadnicovému systému PDF (počátek v levém dolním rohu).

```csharp
// Step 4: Apply the custom graphics state and draw a rectangle
var canvas = firstPage.Canvas;

// Activate the transparency graphics state
canvas.SetGraphicsState("GS0");

// Draw a rectangle from (100, 500) to (200, 600)
canvas.Rectangle(100, 500, 200, 600);

// Render the rectangle outline using the current graphics state
canvas.Stroke();
```

*Proč je to důležité*: `SetGraphicsState("GS0")` přepíná kreslicí kontext na dříve definovaná nastavení průhlednosti. Metoda `Rectangle` definuje tvar a `Stroke` vykresluje obrys s určenou průhledností. Pokud chcete také vyplněný obdélník, nahraďte `Stroke()` metodou `FillAndStroke()`.

## Krok 5: Uložení upraveného PDF při zachování průhlednosti

Nakonec zapíšeme dokument zpět na disk. Výstupní soubor obsahuje nový grafický stav, nakreslený obdélník a informace o průhlednosti.

```csharp
// Step 5: Save the modified PDF
string outputPath = @"YOUR_DIRECTORY\output_with_extgstate.pdf";
pdfDocument.Save(outputPath);
```

*Proč je to důležité*: Uložení dokumentu dokončí všechny změny. Výsledný soubor lze otevřít v libovolném PDF prohlížeči a obdélník se zobrazí s 50 % průhledností výplně.

### Očekávaný výsledek

Když otevřete `output_with_extgstate.pdf`, měli byste vidět obdélník, jehož okraj je plně neprůhledný a vnitřek je poloprůhledný, což umožňuje zobrazit jakýkoli podkladový obsah stránky.

## Okrajové případy a praktické tipy

| Situace | Doporučené úpravy |
|-----------|------------------------|
| **Více stránek** | Procházet `pdfDocument.Pages` a opakovat kroky 2‑4 pro každou cílovou stránku. |
| **Různé hodnoty průhlednosti** | Změňte hodnoty `CosPdfNumber` pro `CA` (obrys) a `ca` (výplň) na libovolné číslo mezi `0` (zcela průhledné) a `1` (zcela neprůhledné). |
| **Vlastní režimy prolnutí** | Nahraďte `"Normal"` hodnotou `"Multiply"`, `"Screen"` nebo jakýmkoli PDF‑standardním režimem prolnutí podporovaným vaším prohlížečem. |
| **Vyplněný obdélník** | Zavolejte `canvas.FillAndStroke()` místo `canvas.Stroke()`, aby se použila jak výplň, tak obrys. |
| **Opakované použití stejného grafického stavu** | Můžete zavolat `canvas.SetGraphicsState("GS0")` před kreslením libovolného počtu tvarů na stejné stránce. |

**Tip:** Vždy zkontrolujte slovník zdrojů po přidání nového `ExtGState`. Pokud slovník neexistuje, vytvořte jej nejprve:

```csharp
if (!resourcesEditor.ContainsKey("ExtGState"))
    resourcesEditor.Add("ExtGState", new Aspose.Pdf.Cos.CosPdfDictionary(pdfDocument));
```

## Kompletní, spustitelný příklad

Níže je samostatný program, který můžete zkopírovat do konzolové aplikace a okamžitě spustit (nahraďte `YOUR_DIRECTORY` skutečnou cestou).

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Cos;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the PDF document
        string pdfPath = @"YOUR_DIRECTORY\input.pdf";
        using var pdfDocument = new Document(pdfPath);

        // 2️⃣ Access the first page’s resources
        var firstPage = pdfDocument.Pages[1];
        var resourcesEditor = new DictionaryEditor(firstPage.Resources);

        // Ensure ExtGState dictionary exists
        if (!resourcesEditor.ContainsKey("ExtGState"))
            resourcesEditor.Add("ExtGState", new CosPdfDictionary(pdfDocument));

        // 3️⃣ Create a custom graphics state with transparency
        var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
        var customGs = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

        var parameters = new[]
        {
            new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),   // stroke opacity
            new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // fill opacity
            new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
        };

        foreach (var p in parameters)
            customGs.Add(p);

        extGStateDict.Add("GS0", customGs);

        // 4️⃣ Apply the graphics state and draw a rectangle
        var canvas = firstPage.Canvas;
        canvas.SetGraphicsState("GS0");
        canvas.Rectangle(100, 500, 200, 600);
        canvas.Stroke(); // use FillAndStroke() for a filled shape

        // 5️⃣ Save the PDF with transparency
        string outputPath = @"YOUR_DIRECTORY\output_with_extgstate.pdf";
        pdfDocument.Save(outputPath);

        Console.WriteLine("PDF saved with a transparent rectangle at: " + outputPath);
    }
}
```

Spuštěním programu vznikne `output_with_extgstate.pdf`, který demonstruje **přidání průhlednosti do PDF**, **nakreslení obdélníku v PDF** a **uložení PDF s průhledností** v jednom postupu.

## Závěr

Nyní víte, jak **přidat průhlednost do PDF** souborů, **nakreslit obdélník v PDF** a **uložit PDF s průhledností** pomocí Aspose.PDF pro .NET. Proces spočívá ve vytvoření vlastního `ExtGState`, jeho aplikaci na plátno a uložení změn. S těmito stavebními kameny můžete techniku rozšířit na další tvary, více stránek nebo dynamické hodnoty průhlednosti.

**Další kroky**

* Prozkoumejte další kreslicí primitiva, jako jsou `canvas.Ellipse`, `canvas.Path` nebo `canvas.TextFragment`, při opakovaném použití stejného grafického stavu.
* Kombinujte průhlednost s překryvy obrázků pro vytvoření vodoznaků (`canvas.Image` + vlastní `ExtGState`).
* Prostudujte dokumentaci Aspose.PDF o **parametrech grafického stavu** pro pokročilé efekty kompozice.

Šťastné programování a užívejte si vizuální flexibilitu, kterou průhlednost přináší do vašich PDF workflow!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto návodu. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Jak vytvořit PDF v C# – Přidat stránku, nakreslit obdélník a uložit](/pdf/english/net/document-creation/how-to-create-pdf-in-c-add-page-draw-rectangle-save/)
- [Jak přidat čáru do PDF pomocí Aspose.PDF pro .NET: Průvodce krok za krokem](/pdf/english/net/document-manipulation/add-line-aspose-pdf-dotnet-tutorial/)
- [Přidat obrázkové razítka do PDF pomocí Aspose.PDF pro .NET: Průvodce krok za krokem](/pdf/english/net/images-graphics/add-image-stamp-to-pdf-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}