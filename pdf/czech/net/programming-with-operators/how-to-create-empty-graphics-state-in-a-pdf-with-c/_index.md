---
category: general
date: 2026-08-17
description: Vytvořte prázdný grafický stav v PDF pomocí C# a Aspose.Pdf. Postupujte
  podle tohoto krok‑za‑krokem návodu pro bezpečnou úpravu zdrojů ExtGState.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create empty graphics state
- Aspose PDF graphics state
- C# modify PDF resources
- add ExtGState dictionary
- PDF page resources editing
language: cs
lastmod: 2026-08-17
og_description: Vytvořte prázdný grafický stav v PDF pomocí C#. Tento tutoriál ukazuje,
  jak upravit zdroje ExtGState pomocí Aspose.Pdf pro spolehlivé úpravy PDF.
og_image_alt: Screenshot of C# code that adds an empty graphics state to a PDF document
og_title: Vytvořte prázdný grafický stav v PDF pomocí C# – krok za krokem průvodce
schemas:
- author: Aspose
  dateModified: '2026-08-17'
  description: Create empty graphics state in a PDF using C# and Aspose.Pdf. Follow
    this step‑by‑step guide to edit ExtGState resources safely.
  headline: How to create empty graphics state in a PDF with C#
  type: TechArticle
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Jak vytvořit prázdný grafický stav v PDF pomocí C#
url: /cs/net/programming-with-operators/how-to-create-empty-graphics-state-in-a-pdf-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak vytvořit prázdný grafický stav v PDF pomocí C#

Pokud potřebujete **vytvořit prázdný grafický stav** v PDF, tento návod vám přesně ukáže, jak to provést pomocí C# a Aspose.Pdf. Uvidíte kompletní, spustitelný příklad, který přidá nový záznam do slovníku ExtGState stránky, aniž by ovlivnil existující obsah.

Práce s grafickými stavy PDF je běžná požadavek, když chcete řídit průhlednost, režimy míchání nebo jiné parametry vykreslování na úrovni jednotlivých objektů. Níže uvedený kód demonstruje doporučený přístup, vysvětluje, proč je každý krok důležitý, a popisuje typické varianty, na které můžete narazit.

## Požadavky

* .NET 6.0 nebo novější (ukázka se také kompiluje s .NET Core).
* Licence Aspose.Pdf pro .NET (nebo dočasný evaluační klíč).
* Složka, která obsahuje soubor `input.pdf`, který chcete upravit.
* Základní znalost syntaxe C# a konceptů PDF, jako jsou slovníky zdrojů.

## Krok 1: Nastavení projektu a import jmenných prostorů

Vytvořte novou konzolovou aplikaci nebo integrujte kód do existujícího projektu. Přidejte NuGet balíček Aspose.Pdf:

```bash
dotnet add package Aspose.Pdf
```

Poté importujte požadované jmenné prostory:

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Operators;
```

Tyto importy vám poskytují přístup ke třídám `Document`, `DictionaryEditor` a PDF primitivům potřebným k **vytvoření prázdného grafického stavu**.

## Krok 2: Definování složky, která obsahuje PDF soubory

```csharp
// Step 1: Define the folder that contains the PDF files
string dataDir = @"C:\PdfSamples\";
```

Nahraďte cestu umístěním vašich vlastních PDF souborů. Uchování adresáře v proměnné činí kód znovupoužitelným a snadněji testovatelným.

## Krok 3: Načtení zdrojového PDF dokumentu

```csharp
// Step 2: Load the source PDF document
using (var pdfDocument = new Document(dataDir + "input.pdf"))
{
    // All subsequent operations happen inside this using block
```

Otevření dokumentu uvnitř `using` bloku zajišťuje, že souborový handle je automaticky uvolněn po uložení změn.

## Krok 4: Přístup k první stránce a jejímu slovníku Resources

```csharp
    // Step 3: Get the first page and its Resources dictionary
    var firstPage = pdfDocument.Pages[1];
    var resourcesEditor = new DictionaryEditor(firstPage.Resources);
    var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
```

* `Pages[1]` získá první stránku (čísla stránek PDF začínají na 1).
* `DictionaryEditor` poskytuje pohodlný způsob, jak číst a upravovat PDF slovníky.
* Záznam `ExtGState` obsahuje všechny objekty grafického stavu pro stránku. Pokud klíč neexistuje, Aspose.Pdf automaticky vytvoří prázdný slovník.

## Krok 5: Vytvoření nového prázdného slovníku grafického stavu

Grafický stav, který přidáte, může být prázdný nebo předem naplněný parametry, jako je průhlednost (`CA`, `ca`) nebo režim míchání (`BM`). V tomto tutoriálu vytvoříme **prázdný grafický stav** a poté nastavíme několik typických hodnot, abychom ilustrovali, jak slovník funguje.

```csharp
    // Step 4: Create a new empty graphics‑state dictionary and set its parameters
    var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
    var parameters = new[]
    {
        new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),   // Stroke opacity
        new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // Fill opacity
        new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // Blend mode
    };
    foreach (var p in parameters)
        newGraphicsState.Add(p);
```

* `CosPdfDictionary.CreateEmptyDictionary` vytvoří čistý kontejner, který můžete naplnit libovolnými klíči grafického stavu.
* Přidání `CA`, `ca` a `BM` je volitelné; můžete je vynechat, pokud opravdu potřebujete prázdný stav. Kód ukazuje, jak přidat záznamy, když se později rozhodnete řídit vykreslování.

## Krok 6: Vložení nového grafického stavu do slovníku ExtGState

```csharp
    // Step 5: Add the new graphics state to the page's ExtGState dictionary (e.g., name it "GS0")
    extGStateDict.Add("GS0", newGraphicsState);
```

Pojmenování záznamu `"GS0"` následuje běžnou konvenci, kdy se názvy grafických stavů předponují „GS“. Můžete zvolit libovolný platný PDF název, který nekoliduje s existujícími klíči.

## Krok 7: Uložení upraveného PDF dokumentu

```csharp
    // Step 6: Save the modified PDF document
    pdfDocument.Save(dataDir + "output.pdf");
}
```

Volání `Save` zapíše aktualizovaný soubor do `output.pdf`. Otevření tohoto souboru v PDF prohlížeči potvrdí, že nový grafický stav existuje; můžete na něj později odkazovat pomocí operátoru `gs` v obsahových streamech.

### Kompletní výpis zdrojového kódu

Spojením všeho dohromady vypadá kompletní program takto:

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Operators;

class Program
{
    static void Main()
    {
        // Define the folder that contains the PDF files
        string dataDir = @"C:\PdfSamples\";

        // Load the source PDF document
        using (var pdfDocument = new Document(dataDir + "input.pdf"))
        {
            // Get the first page and its Resources dictionary
            var firstPage = pdfDocument.Pages[1];
            var resourcesEditor = new DictionaryEditor(firstPage.Resources);
            var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();

            // Create a new empty graphics‑state dictionary and set its parameters
            var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            var parameters = new[]
            {
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
            };
            foreach (var p in parameters)
                newGraphicsState.Add(p);

            // Add the new graphics state to the page's ExtGState dictionary (name it "GS0")
            extGStateDict.Add("GS0", newGraphicsState);

            // Save the modified PDF document
            pdfDocument.Save(dataDir + "output.pdf");
        }

        Console.WriteLine("Empty graphics state created and saved to output.pdf");
    }
}
```

Spuštěním programu se vypíše potvrzovací řádek a vytvoří se `output.pdf` s nově přidaným grafickým stavem.

## Proč tento přístup funguje nejlépe

* **Přímá úprava slovníku** – Použití `DictionaryEditor` eliminuje potřebu parsovat celý obsahový stream. Měníte jen zdroje, které vás zajímají.
* **Typované PDF primitivy** – `CosPdfNumber`, `CosPdfName` a `CosPdfDictionary` zaručují, že generované PDF splňuje specifikaci PDF 1.7.
* **Bezpečnost** – `using` blok uvolní objekt `Document`, což zabraňuje zamykání souborů, které by mohly poškodit následné sestavení.
* **Rozšiřitelnost** – Jakmile existuje prázdný grafický stav, můžete na něj odkazovat z libovolného obsahového operátoru (`gs`) a měnit průhlednost, režim míchání nebo jiné parametry pro vybrané kreslicí příkazy.

## Běžné varianty a okrajové případy

| Situace | Doporučená úprava |
|-----------|-------------------|
| **Více stránek** | Procházet `pdfDocument.Pages` a opakovat vložení slovníku pro každou stránku, kterou potřebujete upravit. |
| **Žádný existující záznam ExtGState** | `resourcesEditor["ExtGState"]` automaticky vytvoří prázdný slovník, pokud neexistuje. Není potřeba žádný další kód. |
| **Jiný název grafického stavu** | Nahraďte `"GS0"` názvem, který odpovídá vaší konvenci, např. `"MyTransparentState"`. |
| **Přidání pouze prázdného stavu** | Vynechte pole `parameters` a smyčku `foreach`; slovník zůstane prázdný. |
| **Práce s šifrovanými PDF** | Zadejte heslo při vytváření `new Document(path, password)` před úpravou zdrojů. |

## Ověření výsledku

Můžete ověřit, že byl grafický stav přidán, inspekcí PDF pomocí nízkoúrovňového prohlížeče, jako je **PDF‑Tron** nebo **iText Sharp**. Hledejte záznam podobný:

```
/ExtGState << /GS0 << /CA 1 /ca 0.5 /BM /Normal >> >>
```

Pokud se záznam objeví, operace **vytvořit prázdný grafický stav** byla úspěšná.

## Závěr

Nyní víte, jak **vytvořit prázdný grafický stav** v PDF pomocí C# a Aspose.Pdf. Tutoriál pokryl každý krok – od načtení dokumentu po úpravu slovníku `ExtGState` a uložení výsledku – a vysvětlil důvody za každou akcí.

Odtud můžete:

* Použít nový grafický stav v obsahových streamech (`gs /GS0`).
* Experimentovat s dalšími klíči, jako je `/SM` (úprava tahu) nebo `/OPM` (režim přetisku).
* Použít stejnou techniku na jiné typy zdrojů, jako `/XObject` nebo `/ColorSpace`.

Šťastné hackování PDF a neváhejte prozkoumat další scénáře **Aspose PDF graphics state**, jako jsou dynamické změny průhlednosti nebo vlastní režimy míchání!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto návodu. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Jak vytvořit čárkované čáry v PDF pomocí Aspose.PDF pro .NET: krok za krokem](/pdf/english/net/images-graphics/create-dashed-lines-aspose-pdf-net/)
- [Jak odstranit grafiku z PDF pomocí Aspose.PDF .NET: kompletní průvodce](/pdf/english/net/images-graphics/remove-graphics-aspose-pdf-net/)
- [Vytvořit a vyplnit obdélníky v PDF pomocí Aspose.PDF pro .NET: krok za krokem](/pdf/english/net/images-graphics/create-fill-rectangle-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}