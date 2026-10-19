---
category: general
date: 2026-10-17
description: Přidejte průhlednost do PDF pomocí Aspose.PDF pro .NET, upravte zdroje
  PDF a uložte upravené PDF soubory v jediném spustitelném příkladu.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add transparency to pdf
- save modified pdf
- edit pdf resources
- Aspose.PDF transparency
- C# PDF manipulation
language: cs
lastmod: 2026-10-17
og_description: Přidejte průhlednost do PDF pomocí Aspose.PDF pro .NET, upravte zdroje
  PDF a uložte upravené PDF soubory s kompletním příkladem v C#.
og_image_alt: Screenshot showing a PDF with added transparency using Aspose.PDF in
  C#
og_title: Přidejte průhlednost do PDF pomocí Aspose.PDF – průvodce
schemas:
- author: Aspose
  dateModified: '2026-10-17'
  description: Add transparency to PDF with Aspose.PDF for .NET, edit PDF resources,
    and save modified PDF files in a single, runnable example.
  headline: How to add transparency to PDF using Aspose.PDF in C#
  type: TechArticle
tags:
- pdf
- aspnet
- csharp
title: Jak přidat průhlednost do PDF pomocí Aspose.PDF v C#
url: /cs/net/images-graphics/how-to-add-transparency-to-pdf-using-aspose-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak přidat průhlednost do PDF pomocí Aspose.PDF v C#

Pokud potřebujete **přidat průhlednost do PDF** souborů programově, tento návod vám ukáže jasné, kompletní řešení s Aspose.PDF pro .NET. Naučíte se, jak **editovat PDF zdroje**, vytvořit vlastní grafický stav a **uložit upravené PDF** výstup, aniž byste opustili svůj C# projekt.

Práce s průhledností v PDF se často zdá skrytá za nízkoúrovňovými PDF operátory. Na konci tohoto tutoriálu budete mít plně funkční příklad, který můžete zkopírovat, spustit a přizpůsobit pro více stránek nebo různé režimy míchání.

## Požadavky

- .NET 6.0 (nebo jakákoli aktuální verze .NET)  
- Aspose.PDF for .NET NuGet balíček (`Aspose.Pdf`)  
- Základní znalost C#  
- Vstupní PDF soubor (`input.pdf`) umístěný ve složce, na kterou můžete odkazovat

> **Tip:** Nainstalujte balíček pomocí `dotnet add package Aspose.Pdf` předtím, než začnete.

## Krok 1: Načtení PDF dokumentu

Prvním krokem je otevřít zdrojové PDF. Aspose.PDF představuje PDF jako objekt `Document`, který vám poskytuje přístup k stránkám, zdrojům a nízkoúrovňovým slovníkům.

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Collections;
using Aspose.Pdf.Text;
using Aspose.Pdf.Generator;   // for graphics‑state objects

// Path to the original PDF
string pdfPath = @"YOUR_DIRECTORY\input.pdf";

// Open the document in a using block so it disposes automatically
using (var document = new Document(pdfPath))
{
    // The rest of the steps are inside this block
```

*Proč je to důležité:* Otevření dokumentu tímto způsobem zajišťuje uvolnění souborového handle po dokončení úprav, čímž se předejde problémům se zamčením souboru, když později **uložíme upravené PDF**.

## Krok 2: Přístup k první stránce a jejímu slovníku zdrojů

PDF stránky ukládají grafické objekty (písma, obrázky, položky ExtGState) ve *slovníku zdrojů*. Pro změnu neprůhlednosti musíme pracovat s podslovníkem `ExtGState`.

```csharp
    // Get the first page (pages are 1‑based in Aspose.PDF)
    Page page = document.Pages[1];

    // Obtain a mutable editor for the page's resources
    var resourcesEditor = new DictionaryEditor(page.Resources);

    // Retrieve the ExtGState dictionary; create it if missing
    var extGStateDict = resourcesEditor["ExtGState"]?.ToCosPdfDictionary()
                         ?? new CosPdfDictionary(document);
```

*Proč je to důležité:* Pokud originální PDF již obsahuje slovník `ExtGState`, rozšíříme jej; jinak vytvoříme nový, abychom mohli bezpečně **editovat PDF zdroje**.

## Krok 3: Vytvoření nového grafického stavu s průhledností

Grafický stav (`ExtGState`) obsahuje parametry jako neprůhlednost obrysu (`CA`), neprůhlednost výplně (`ca`) a režim míchání (`BM`). Vytvoříme prázdný slovník a naplníme jej požadovanými hodnotami.

```csharp
    // Create an empty ExtGState dictionary for the new entry
    var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(document);

    // Define the transparency entries
    var entries = new[]
    {
        // CA – stroke opacity (1 = fully opaque)
        new KeyValuePair<string, ICosPdfPrimitive>("CA",
            new CosPdfNumber(1)),

        // ca – fill opacity (0.5 = 50 % transparent)
        new KeyValuePair<string, ICosPdfPrimitive>("ca",
            new CosPdfNumber(0.5)),

        // BM – blend mode (Normal is the default)
        new KeyValuePair<string, ICosPdfPrimitive>("BM",
            new CosPdfName("Normal"))
    };

    // Add each entry to the new ExtGState dictionary
    foreach (var entry in entries)
        newGraphicsState.Add(entry);
```

*Proč je to důležité:* Položka `ca` je klíčová pro **přidání průhlednosti do PDF** obsahu, který tento grafický stav používá. Můžete upravit číselnou hodnotu (0 – 1), abyste řídili, jak průhledný objekt bude.

## Krok 4: Vložení grafického stavu do zdrojů stránky

Musíme novému grafickému stavu přiřadit název (např. `"GS0"`). Tento název může být později odkazován v obsahových streamech pro aplikaci průhlednosti.

```csharp
    // Add the new ExtGState under the name "GS0"
    extGStateDict.Add("GS0", newGraphicsState);

    // Ensure the modified ExtGState dictionary is written back to the page
    resourcesEditor["ExtGState"] = extGStateDict;
```

*Proč je to důležité:* Přidáním `"GS0"` do slovníku `ExtGState` se jakákoli kreslicí operace, která tento stav vybere, vykreslí s definovanou neprůhledností. To je jádro **editování PDF zdrojů** pro průhlednost.

## Krok 5: Aplikace grafického stavu na obsah stránky (volitelné)

Pokud chcete, aby existující obsah stránky automaticky používal novou průhlednost, musíte předřadit operátor grafického stavu do obsahového streamu stránky. Následující úryvek ukazuje, jak obalit existující obsah pomocí `gs` (nastavit grafický stav) a `Q` (obnovit grafický stav).

```csharp
    // Get the current content stream
    var content = page.Contents[1]; // assume a single content stream

    // Build a new stream that sets the graphics state, draws the original content, then restores
    string gsOperator = "/GS0 gs\n"; // select the graphics state we created
    string restoreOperator = "Q\n";   // restore graphics state after drawing

    // Prepend the gs operator and append the restore operator
    string newStream = gsOperator + content.Stream.ToString() + restoreOperator;

    // Replace the original stream with the modified one
    content.Stream = new CosPdfStream(document);
    content.Stream.SetData(newStream);
```

*Proč je to důležité:* Bez tohoto kroku grafický stav existuje, ale není použit. Přidání operátoru `gs` říká PDF rendereru, aby aplikoval průhlednost na vše, co následuje.

## Krok 6: **Uložit upravené PDF** na disk

Nakonec zapíšete změněný dokument do nového souboru. Metoda `Save` automaticky zpracuje všechny nízkoúrovňové aktualizace.

```csharp
    // Path for the output PDF
    string outputPath = @"YOUR_DIRECTORY\output.pdf";

    // Persist the changes
    document.Save(outputPath);
}
```

*Proč je to důležité:* Volání `document.Save` zajišťuje, že aktualizované **uložené upravené pdf** obsahuje nový záznam `ExtGState` a obsahový stream, který na něj odkazuje. Výsledný soubor zobrazí poloprůhlednou výplň na první stránce.

## Očekávaný výsledek

Otevřete `output.pdf` v libovolném PDF prohlížeči (Adobe Reader, Chrome atd.) a měli byste vidět grafiku první stránky vykreslenou s 50 % neprůhledností výplně. Pokud PDF prozkoumáte nástrojem jako **PDF‑Tron** nebo **iText**, najdete položku slovníku `ExtGState` pojmenovanou `GS0` s hodnotou `ca` nastavenou na `0.5`.

## Okrajové případy a varianty

| Situace | Co změnit |
|-----------|----------------|
| **Více stránek** | Procházejte `document.Pages` a opakujte kroky 2‑5 pro každou stránku, používající jedinečný název jako `GS1`, `GS2`, … |
| **Stávající konflikt názvu ExtGState** | Před přidáním zkontrolujte `extGStateDict.ContainsKey("GS0")`; pokud existuje, vygenerujte nový klíč (`"GS" + Guid.NewGuid().ToString("N")`) |
| **Různé režimy míchání** | Nahraďte `"Normal"` za `"Multiply"`, `"Screen"` atd. změnou položky `BM` |
| **Potřebná jen neprůhlednost obrysu** | Vynechte položku `ca` nebo ji nastavte na `1` a upravte místo toho `CA` |

## Kompletní, spustitelný příklad



## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto návodu. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Přidat průhlednost do PDF s Aspose.PDF – Kompletní C# průvodce](/pdf/english/net/programming-with-stamps-and-watermarks/add-transparency-to-pdf-with-aspose-pdf-complete-c-guide/)
- [Jak přidat razítka na stránky v PDF pomocí Aspose.PDF pro .NET: Kompletní průvodce](/pdf/english/net/watermarks-backgrounds/add-page-stamp-aspose-pdf-dotnet-guide/)
- [Jak přidat obrázky do PDF pomocí Aspose.PDF pro .NET: Kompletní průvodce](/pdf/english/net/images-graphics/add-images-to-pdfs-using-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}