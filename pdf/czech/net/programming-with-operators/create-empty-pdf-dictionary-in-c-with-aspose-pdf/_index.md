---
category: general
date: 2026-08-14
description: Vytvořte prázdný PDF slovník v C# pomocí Aspose.Pdf – naučte se, jak
  přidat grafický stav do kolekce ExtGState a programově upravovat PDF soubory.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create empty PDF dictionary
- Aspose.Pdf Document
- PDF graphics state
- ExtGState dictionary
- CosPdfDictionary usage
language: cs
lastmod: 2026-08-14
og_description: Vytvořte prázdný PDF slovník v C# pomocí Aspose.Pdf. Postupujte podle
  tohoto kompletního průvodce, jak přidat vlastní grafický stav do kolekce ExtGState
  PDF.
og_image_alt: Screenshot showing C# code that creates an empty PDF dictionary with
  Aspose.Pdf
og_title: Vytvořte prázdný PDF slovník v C# – průvodce krok za krokem Aspose.Pdf
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: Create empty PDF dictionary in C# using Aspose.Pdf – learn how to add
    a graphics state to the ExtGState collection and modify PDFs programmatically.
  headline: Create empty PDF dictionary in C# with Aspose.Pdf
  type: TechArticle
- description: Create empty PDF dictionary in C# using Aspose.Pdf – learn how to add
    a graphics state to the ExtGState collection and modify PDFs programmatically.
  name: Create empty PDF dictionary in C# with Aspose.Pdf
  steps:
  - name: Create a new **Console App** project in Visual Studio.
    text: Create a new **Console App** project in Visual Studio.
  - name: 'Open the **NuGet Package Manager** and install `Aspose.Pdf`:'
    text: 'Open the **NuGet Package Manager** and install `Aspose.Pdf`:'
  - name: 'Add the following `using` directives at the top of `Program.cs`:'
    text: 'Add the following `using` directives at the top of `Program.cs`:'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Vytvořte prázdný PDF slovník v C# pomocí Aspose.Pdf
url: /cs/net/programming-with-operators/create-empty-pdf-dictionary-in-c-with-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření prázdného PDF slovníku v C# pomocí Aspose.Pdf

Pokud potřebujete **vytvořit prázdný PDF slovník** objektů při práci s PDF soubory, tento průvodce vám přesně ukáže, jak to provést v C# pomocí knihovny Aspose.Pdf. Ať už vytváříte vlastní grafický stav, přidáváte nový zdroj nebo připravujete šablonu pro pozdější použití, níže uvedené kroky vám poskytnou kompletní, spustitelné řešení.

Dozvíte se, jak načíst PDF, získat slovník zdrojů první stránky, vytvořit zcela nový `CosPdfDictionary` a vložit jej do kolekce `ExtGState`. Na konci tutoriálu budete mít funkční `output.pdf`, který obsahuje nově vytvořený slovník.

## Požadavky

Než začnete, ujistěte se, že máte:

- .NET 6.0 nebo novější (kód také funguje s .NET Framework 4.6+)
- Visual Studio 2022 nebo jakékoli C# IDE, které preferujete
- Licenci Aspose.Pdf pro .NET (nebo dočasný evaluační klíč)
- Vzorek PDF pojmenovaný **input.pdf** umístěný ve složce, kterou ovládáte (cesta ke složce bude použita jako `dataDir`)

Žádné další NuGet balíčky nejsou potřeba nad rámec `Aspose.Pdf`.

## Krok 1: Nastavení projektu a odkaz na Aspose.Pdf

1. Vytvořte nový projekt **Console App** ve Visual Studiu.  
2. Otevřete **NuGet Package Manager** a nainstalujte `Aspose.Pdf`:

   ```bash
   dotnet add package Aspose.Pdf
   ```

3. Přidejte následující `using` direktivy na začátek souboru `Program.cs`:

   ```csharp
   using Aspose.Pdf;
   using Aspose.Pdf.Text;
   using Aspose.Pdf.Operators;
   using Aspose.Pdf.Facades;
   using Aspose.Pdf.InteractiveFeatures;
   using Aspose.Pdf.Xmp;
   using Aspose.Pdf.Operators.Filters;
   using Aspose.Pdf.Operators.Gfx;
   ```

   *Proč tyto jmenné prostory?* `Aspose.Pdf` obsahuje základní třídu `Document`, zatímco `Aspose.Pdf.Operators.Gfx` poskytuje `CosPdfDictionary`, `CosPdfNumber` a související nízkoúrovňové PDF objekty potřebné k **vytvoření prázdného PDF slovníku**.

## Krok 2: Načtení zdrojového PDF

Prvním krokem je načíst existující PDF soubor do instance `Document`. Tím získáte přístup ke všem stránkám, zdrojům a nízkoúrovňovým slovníkům.

```csharp
// Step 2: Load the PDF document
string dataDir = @"C:\MyPdfFolder\";               // Change to your folder
using var pdfDocument = new Document(dataDir + "input.pdf");
```

*Vysvětlení*: `Document` načte soubor do paměti a připraví interní struktury. Příkaz `using` zajistí uvolnění souborového handle po dokončení zpracování.

## Krok 3: Přístup ke slovníku zdrojů první stránky

Každá PDF stránka má slovník **Resources**, který seskupuje fonty, obrázky, objekty ExtGState a další sdílené zdroje. Pro vložení nového grafického stavu musíme tento slovník upravit.

```csharp
// Step 3: Get the first page and its Resources dictionary
Page firstPage = pdfDocument.Pages[1];                     // PDF pages are 1‑based
DictionaryEditor resourcesEditor = new DictionaryEditor(firstPage.Resources);
```

`DictionaryEditor` je pomocná třída, která vám umožní zacházet se slovníkem PDF jako s C# `Dictionary<string, object>`.

## Krok 4: Získání (nebo vytvoření) kolekce ExtGState

`ExtGState` obsahuje objekty grafického stavu, jako je neprůhlednost, režim míchání a šířka čáry. Pokud zdrojové PDF již obsahuje položku `ExtGState`, použijeme ji; jinak vytvoříme nový prázdný slovník.

```csharp
// Step 4: Ensure an ExtGState dictionary exists
CosPdfDictionary extGStateDict;
if (resourcesEditor.ContainsKey("ExtGState"))
{
    extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
}
else
{
    // Create a brand‑new ExtGState dictionary and add it to Resources
    extGStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
    resourcesEditor["ExtGState"] = extGStateDict;
}
```

*Proč tato kontrola?* Některá PDF úplně neobsahují položku `ExtGState`. Ošetřením obou případů je tutoriál odolný vůči libovolnému vstupnímu souboru.

## Krok 5: **Vytvoření prázdného PDF slovníku** pro nový grafický stav

Nyní skutečně **vytvoříme prázdný PDF slovník** objektů, který definuje parametry grafického stavu. Slovník začíná prázdný a přidáme požadované klíče:

```csharp
// Step 5: Build a new graphics state dictionary (empty PDF dictionary + entries)
CosPdfDictionary newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

// Stroke opacity (CA) – 1 means fully opaque strokes
newGraphicsState.Add("CA", new CosPdfNumber(1));

// Fill opacity (ca) – 0.5 makes semi‑transparent fills
newGraphicsState.Add("ca", new CosPdfNumber(0.5));

// Blend mode (BM) – "Normal" is the default compositing mode
newGraphicsState.Add("BM", new CosPdfName("Normal"));
```

### Co jednotlivé položky dělají

| Klíč | Typ | Význam |
|------|-----|--------|
| **CA** | `CosPdfNumber` | Neprůhlednost tahů (rozsah 0‑1). |
| **ca** | `CosPdfNumber` | Neprůhlednost výplní (rozsah 0‑1). |
| **BM** | `CosPdfName`   | Režim míchání; `"Normal"` je nejčastější. |

Protože jsme začali s **prázdným PDF slovníkem**, máte plnou kontrolu nad tím, které položky jsou přidány. Slovník můžete rozšířit o další parametry grafického stavu, jako jsou `LW` (šířka čáry) nebo `LC` (ukončení čáry), kdykoliv budete potřebovat.

## Krok 6: Vložení nového grafického stavu do ExtGState

Slovník `ExtGState` funguje jako mapa, kde je každá položka identifikována názvem (např. `GS0`, `GS1`). Přidáme náš čerstvě vytvořený slovník pod jedinečný klíč.

```csharp
// Step 6: Add the graphics state to the ExtGState collection
extGStateDict.Add("GS0", newGraphicsState);
```

Pokud plánujete přidat více stavů, zvyšte příponu (`GS1`, `GS2`, …), aby nedošlo ke kolizi názvů.

## Krok 7: Uložení upraveného PDF

Nakonec zapíšeme změny zpět na disk. Metoda `Save` automaticky serializuje aktualizované slovníky.

```csharp
// Step 7: Persist the changes
pdfDocument.Save(dataDir + "output.pdf");
```

Otevřete `output.pdf` v libovolném PDF prohlížeči a prohlédněte položku **Resources → ExtGState** (většina prohlížečů ji skryje, ale nástroje jako Adobe Acrobat Preflight nebo PDF‑Tron ji dokážou zobrazit). Měli byste vidět položku `GS0` obsahující hodnoty neprůhlednosti a režimu míchání, které jste definovali.

## Kompletní funkční příklad

Sestavením všech částí dohromady získáte celý program, který můžete zkopírovat a vložit do `Program.cs` a spustit:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Operators.Gfx;

class Program
{
    static void Main()
    {
        // -----------------------------------------------------------------
        // 1️⃣ Load the PDF document
        // -----------------------------------------------------------------
        string dataDir = @"C:\MyPdfFolder\"; // <-- change to your folder
        using var pdfDocument = new Document(dataDir + "input.pdf");

        // -----------------------------------------------------------------
        // 2️⃣ Access the first page’s Resources dictionary
        // -----------------------------------------------------------------
        Page firstPage = pdfDocument.Pages[1];
        var resourcesEditor = new DictionaryEditor(firstPage.Resources);

        // -----------------------------------------------------------------
        // 3️⃣ Retrieve or create the ExtGState dictionary
        // -----------------------------------------------------------------
        CosPdfDictionary extGStateDict;
        if (resourcesEditor.ContainsKey("ExtGState"))
        {
            extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
        }
        else
        {
            extGStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            resourcesEditor["ExtGState"] = extGStateDict;
        }

        // -----------------------------------------------------------------
        // 4️⃣ **Create empty PDF dictionary** for a new graphics state
        // -----------------------------------------------------------------
        var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
        newGraphicsState.Add("CA", new CosPdfNumber(1));          // Stroke opacity
        newGraphicsState.Add("ca", new CosPdfNumber(0.5));        // Fill opacity
        newGraphicsState.Add("BM", new CosPdfName("Normal"));    // Blend mode

        // -----------------------------------------------------------------
        // 5️⃣ Add the graphics state to ExtGState
        // -----------------------------------------------------------------
        extGStateDict.Add("GS0", newGraphicsState);

        // -----------------------------------------------------------------
        // 6️⃣ Save the modified PDF
        // -----------------------------------------------------------------
        pdfDocument.Save(dataDir + "output.pdf");

        Console.WriteLine("PDF saved with new empty dictionary at: " + dataDir + "output.pdf");
    }
}
```

**Očekávaný výstup** – Konzole vypíše potvrzovací řádek a `output.pdf` obsahuje novou položku `GS0` pod `ExtGState`. Když vykreslíte stránku, která odkazuje na `GS0` (např. pomocí operátoru obsahu `gs`), tahy budou zcela neprůhledné, zatímco výplně budou 50 % průhledné.

## Často kladené otázky a řešení okrajových případů

| Otázka | Odpověď |
|--------|---------|
| *Co když PDF obsahuje více stránek?* | Příklad cílí na první stránku (`Pages[1]`). Pro úpravu všech stránek projděte `pdfDocument.Pages` a opakujte kroky 3‑5 pro zdroje každé stránky. |
| *Mohu přidat slovník na stránku, která již má položku ExtGState pojmenovanou „GS0“?* | Ano, ale musíte použít jiný klíč (`GS1`, `GS2`, …), aby nedošlo k přepsání existující položky. |
| *Je bezpečné měnit slovník po uložení?* | Po zavolání `Save` je v‑paměti reprezentace oddělena od souboru. Můžete nadále upravovat objekt `Document` a volat `Save` znovu, pokud bude potřeba. |
| *Potřebuji licenci pro Aspose.Pdf k použití ` |  |

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, která vám pomohou zvládnout další funkce API a prozkoumat alternativní implementační přístupy ve vašich projektech.

- [Jak vytvořit čárkované čáry v PDF pomocí Aspose.PDF pro .NET: krok za krokem](/pdf/english/net/images-graphics/create-dashed-lines-aspose-pdf-net/)
- [Jak odstranit grafiku z PDF pomocí Aspose.PDF .NET: kompletní průvodce](/pdf/english/net/images-graphics/remove-graphics-aspose-pdf-net/)
- [Jak vytvořit vícevrstvé PDF pomocí Aspose.PDF pro .NET: komplexní průvodce](/pdf/english/net/advanced-features/create-multi-layer-pdfs-aspose-pdf-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}