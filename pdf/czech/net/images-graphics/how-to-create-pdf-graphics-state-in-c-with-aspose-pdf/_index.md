---
category: general
date: 2026-11-16
description: Naučte se, jak vytvořit grafický stav PDF v C# pomocí Aspose.Pdf. Tento
  průvodce zahrnuje průhlednost, režim prolnutí a kompletní příklad kódu.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create pdf graphics state
- Aspose.Pdf ExtGState
- PDF opacity
- C# PDF manipulation
- PDF blend mode
- Aspose.Pdf graphics state
language: cs
lastmod: 2026-11-16
og_description: Vytvořte grafický stav PDF v C# s Aspose.Pdf. Sledujte tento kompletní
  tutoriál, jak programově nastavit průhlednost a režim prolnutí.
og_image_alt: Illustration of how to create PDF graphics state with Aspose.Pdf in
  C#
og_title: Vytvoření grafického stavu PDF v C# – krok za krokem průvodce Aspose.Pdf
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Learn how to create PDF graphics state in C# using Aspose.Pdf. This
    guide covers opacity, blend mode, and full code example.
  headline: How to create PDF graphics state in C# with Aspose.Pdf
  type: TechArticle
tags:
- Aspose.Pdf
- C#
- PDF
title: Jak vytvořit grafický stav PDF v C# pomocí Aspose.Pdf
url: /cs/net/images-graphics/how-to-create-pdf-graphics-state-in-c-with-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak vytvořit PDF graphics state v C# s Aspose.Pdf

Pokud potřebujete **vytvořit PDF graphics state** v .NET projektu, tento tutoriál vám přesně ukáže, jak to provést pomocí Aspose.Pdf. Ať už chcete řídit průhlednost, změnit režim míchání nebo znovu použít vlastní grafický stav napříč stránkami, níže uvedené kroky vám poskytnou kompletní, připravené řešení.

V tomto průvodci se naučíte, jak získat přístup k prostředkům stránky, přidat položku **ExtGState** a uložit změny do nového souboru. Příklad funguje s Aspose.Pdf 23.12 (nebo novějším) a cílí na .NET 6+, ale koncepty platí i pro starší verze.

## Požadavky

Než začnete, ujistěte se, že máte:

* Visual Studio 2022 (nebo jakékoli C# IDE) s nainstalovaným .NET 6 SDK.  
* Licence Aspose.Pdf pro .NET nebo dočasný evaluační klíč.  
* Soubor PDF pojmenovaný `input.pdf` umístěný ve složce, na kterou můžete odkazovat z kódu.  

Kromě `Aspose.Pdf` nejsou vyžadovány žádné další NuGet balíčky.

## Co tutoriál pokrývá

* Načtení existujícího PDF dokumentu.  
* Navigace do slovníku prostředků první stránky.  
* Vytvoření nového slovníku grafického stavu, který definuje průhlednost tahu (`CA`), průhlednost výplně (`ca`) a režim míchání (`BM`).  
* Přidání nového grafického stavu do kolekce **ExtGState** s vlastním názvem (`GS0`).  
* Uložení aktualizovaného PDF, aby následné kreslicí příkazy mohly odkazovat na nový stav.

Na konci tutoriálu budete schopni programově **vytvořit PDF graphics state** objekty a znovu je použít v libovolné kreslicí operaci.

## Krok 1: Nastavení projektu a import jmenných prostorů

Vytvořte novou konzolovou aplikaci (nebo integrujte kód do existujícího projektu). Přidejte odkaz na Aspose.Pdf a zahrňte požadované jmenné prostory:

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Operators;
using Aspose.Pdf.Generator;
```

> **Pro tip:** Pokud používáte bezplatnou evaluační verzi, přidejte `Aspose.Pdf.License license = new Aspose.Pdf.License(); license.SetLicense("Aspose.Pdf.lic");` před načtením dokumentu, abyste se vyhnuli zprávám o vodoznaku.

## Krok 2: Načtení PDF dokumentu

Otevření souboru je jednoduché. Třída `Document` představuje celý PDF a poskytuje přístup k jeho stránkám a prostředkům.

```csharp
// Step 2: Load the PDF document
string inputPath = @"YOUR_DIRECTORY\input.pdf";

using (var document = new Document(inputPath))
{
    // All subsequent steps run inside this using block
```

Umístění kódu do bloku `using` zaručuje uvolnění souborového handle po operaci, což je nezbytné pro **C# PDF manipulaci** v produkčních službách.

## Krok 3: Získání slovníku prostředků první stránky

Každá stránka PDF má slovník *Resources*, který ukládá písma, obrázky a grafické stavy. K úpravě této struktury potřebujeme `DictionaryEditor`.

```csharp
    // Step 3: Get the first page and its resources dictionary
    var page = document.Pages[1];
    var resourcesEditor = new DictionaryEditor(page.Resources);
```

Pokud PDF již obsahuje položku `ExtGState`, `resourcesEditor["ExtGState"]` ji vrátí; jinak Aspose.Pdf vytvoří prázdný slovník, když přidáme první položku.

## Krok 4: Přístup nebo vytvoření slovníku ExtGState

**ExtGState** slovník obsahuje pojmenované objekty grafického stavu. Buď získáme existující, nebo vytvoříme nový kontejner.

```csharp
    // Step 4: Access (or create) the ExtGState dictionary within the resources
    var extGState = resourcesEditor["ExtGState"].ToCosPdfDictionary();
```

Když `ExtGState` neexistuje, `resourcesEditor["ExtGState"]` automaticky vrátí nový prázdný slovník, což zajišťuje, že kód funguje pro jakýkoli PDF.

## Krok 5: Vytvoření nového slovníku grafického stavu

Grafický stav je `CosPdfDictionary` s konkrétními klíči:

* `CA` – průhlednost tahu (0‑1)  
* `ca` – průhlednost výplně (0‑1)  
* `BM` – režim míchání (`Normal`, `Multiply`, atd.)

Vytvoříme prázdný slovník, naplníme jej a poté jej přidáme do `ExtGState`.

```csharp
    // Step 5: Create a new graphics state dictionary with desired parameters
    var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(document);
    var parameters = new[]
    {
        new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),   // Stroke opacity (fully opaque)
        new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // Fill opacity (50% transparent)
        new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // Blend mode
    };

    foreach (var p in parameters)
        newGraphicsState.Add(p);
```

Můžete změnit `0.5` na libovolnou hodnotu mezi `0` a `1` pro úpravu průhlednosti výplně, nebo nahradit `"Normal"` za `"Multiply"` pro jiný **PDF blend mode**. Tato flexibilita je důvod, proč je vytváření vlastního grafického stavu výkonnou technikou při práci s **Aspose.Pdf graphics state**.

## Krok 6: Registrace grafického stavu pod jménem

PDF obsahové proudy odkazují na grafické stavy podle jména. Zde používáme `GS0`, ale jakékoli jedinečné jméno funguje.

```csharp
    // Step 6: Add the new graphics state to the ExtGState dictionary with a name (e.g., GS0)
    extGState.Add("GS0", newGraphicsState);
```

Pokud potřebujete více stavů, opakujte krok vytvoření s různými parametry a přidejte je jako `GS1`, `GS2` atd. Tento vzor se dobře škáluje pro složité dokumenty, které vyžadují různé nastavení průhlednosti nebo režimu míchání na různých vrstvách.

## Krok 7: Uložení upraveného PDF

Nakonec zapište aktualizovaný dokument do nového souboru. Zachování originálu usnadňuje ladění.

```csharp
    // Step 7: Save the updated PDF document
    string outputPath = @"YOUR_DIRECTORY\output.pdf";
    document.Save(outputPath);
}
```

Po spuštění `output.pdf` obsahuje položku `ExtGState` pojmenovanou `GS0`. Jakýkoli následný kreslicí operátor ji může odkazovat pomocí operátoru `gs` (např. `GS0 gs` v obsahovém proudu).  

> **Proč je to důležité:** Protože vytvořením znovupoužitelného grafického stavu se vyhnete opakování nastavení průhlednosti a režimu míchání pro každý kreslicí příkaz, což zlepšuje jak výkon, tak udržovatelnost.

## Použití nového grafického stavu v obsahovém proudu (volitelné)

Pokud chcete efekt vidět okamžitě, můžete přidat jednoduchý obdélník, který používá právě vytvořený stav:

```csharp
using (var document = new Document(outputPath))
{
    var page = document.Pages[1];
    var content = page.Contents[1]; // Get the first content stream

    // Insert graphics state selection and a semi‑transparent rectangle
    var operators = new List<Operator>
    {
        new Operator("GS0", "gs"),                     // Select our custom graphics state
        new Operator("0.5", "w"),                      // Set line width (optional)
        new Operator("100", "100", "200", "150", "re"), // Rectangle (x, y, width, height)
        new Operator("B")                              // Stroke the rectangle
    };

    foreach (var op in operators)
        content.Operators.Add(op);

    document.Save(@"YOUR_DIRECTORY\final_output.pdf");
}
```

Obdélník bude vykreslen s 50 % průhledností výplně, zatímco tah zůstane plně neprůhledný, přesně tak, jak je definováno ve slovníku **create PDF graphics state**.

## Časté problémy a jak se jim vyhnout

| Problém | Proč se to děje | Řešení |
|-------|----------------|-----|
| `ExtGState` položka nenalezena | Některé PDF soubory slovník úplně vynechávají. | `DictionaryEditor` jej automaticky vytvoří, když přidáte první položku, takže není potřeba žádná další kontrola. |
| Hodnoty průhlednosti > 1 nebo < 0 | Specifikace PDF omezuje průhlednost na rozsah `[0,1]`. | Ořízněte hodnoty před vytvořením `CosPdfNumber`. |
| Chybný název blend mode | Názvy blend mode v PDF jsou citlivé na velikost písmen. | Používejte přesné názvy jako `"Normal"`, `"Multiply"`, `"Screen"`. |
| Vodoznak licence | Evaluační verze přidává vodoznak na první stránku. | Aplikujte platný licenční soubor před otevřením dokumentu. |

Řešením těchto okrajových případů zajistíte, že vaše implementace **create PDF graphics state** bude spolehlivě fungovat napříč různými PDF zdroji.

## Kompletní, spustitelný příklad

Níže je samostatný program, který můžete zkopírovat, vložit a spustit. Nahraďte `YOUR_DIRECTORY` skutečnou cestou ke složce na vašem počítači.

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Generator;

class Program
{
    static void Main()
    {
        // Optional: apply license to remove evaluation watermark
        // var license = new Aspose.Pdf.License();
        // license.SetLicense("Aspose.Pdf.lic");

        string inputPath = @"YOUR_DIRECTORY\input.pdf";
        string outputPath = @"YOUR_DIRECTORY\output.pdf";

        using (var document = new Document(inputPath))
        {
            // 1️⃣ Get first page and its resources
            var page = document.Pages[1];
            var resourcesEditor = new DictionaryEditor(page.Resources);

            // 2️⃣ Access (or create) ExtGState dictionary
            var extGState = resourcesEditor["ExtGState"].ToCosPdfDictionary();

            // 3️⃣ Build new graphics state
            var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(document);
            var parameters = new[]
            {
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),   // Stroke opacity
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // Fill opacity
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // Blend mode
            };
            foreach (var p in parameters) newGraphicsState.Add(p);

            // 4️⃣ Register the state with a name (GS0)
            extGState.Add("


## Co byste se měli naučit dál?


Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Vytvořit vlastní grafický stav v PDF pomocí Aspose.Pdf](/pdf/english/net/programming-with-operators/create-custom-graphics-state-in-pdf-using-aspose-pdf/)
- [Přidat grafický stav do PDF pomocí Aspose.PDF pro .NET (C#)](/pdf/english/net/programming-with-operators/how-to-add-graphics-state-pdf-using-aspose-pdf-in-c/)
- [Jak vytvořit prázdný grafický stav v PDF pomocí C#](/pdf/english/net/programming-with-operators/how-to-create-empty-graphics-state-in-a-pdf-with-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}