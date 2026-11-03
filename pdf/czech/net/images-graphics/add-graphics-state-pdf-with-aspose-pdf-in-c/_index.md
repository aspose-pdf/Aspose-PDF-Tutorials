---
category: general
date: 2026-10-07
description: Přidejte grafický stav PDF pomocí Aspose.Pdf v C# pro úpravu průhlednosti
  PDF. Postupujte podle tohoto krok‑za‑krokem průvodce, abyste vložili vlastní grafické
  stavy a ovládali neprůhlednost.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add graphics state pdf
- modify pdf transparency
language: cs
lastmod: 2026-10-07
og_description: Přidejte grafický stav do PDF pomocí Aspose.Pdf v C#. Naučte se, jak
  upravit průhlednost PDF vytvořením vlastního slovníku grafického stavu.
og_image_alt: Screenshot showing the add graphics state pdf code editor in Visual
  Studio
og_title: Přidání grafického stavu PDF s Aspose.Pdf – kontrola průhlednosti PDF
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Add graphics state pdf using Aspose.Pdf in C# to modify PDF transparency.
    Follow this step‑by‑step guide to embed custom graphics states and control opacity.
  headline: Add graphics state pdf with Aspose.Pdf in C#
  type: TechArticle
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Přidat grafický stav PDF pomocí Aspose.Pdf v C#
url: /cs/net/images-graphics/add-graphics-state-pdf-with-aspose-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Přidání grafického stavu PDF pomocí Aspose.Pdf v C#

Pokud potřebujete **přidat grafický stav PDF** do dokumentu, tento tutoriál vám přesně ukáže, jak to provést pomocí Aspose.Pdf pro .NET. Na konci průvodce také budete vědět, jak **upravit průhlednost PDF**, což vám umožní nastavit vlastní hodnoty opacity pro jakoukoli kreslicí operaci.

Práce s grafickými stavy PDF vám umožňuje řídit parametry jako šířka čáry, režim prolnutí a co je pro tento článek nejdůležitější, průhlednost obsahu. Níže uvedené kroky jsou psány pro vývojáře, kteří jsou zkušení v C# a chtějí připravené řešení bez nutnosti procházet oficiální dokumentaci SDK.

## Co se naučíte

* Jak vytvořit nový slovník grafického stavu a naplnit jej položkami `CA`, `ca` a `BM`.  
* Jak vložit tento slovník do zdroje `ExtGState` stránky, aby jej PDF rozpoznalo.  
* Jak hodnoty `ca` (čára) a `CA` (výplň) ovlivňují **úpravu průhlednosti PDF** pro následné kreslicí příkazy.  
* Běžné úskalí, jako kolize názvů a kompatibilita verzí, plus tipy pro rozšíření grafického stavu v budoucnu.

**Požadavky**

* .NET 6.0 nebo novější (kód také funguje s .NET Framework 4.7+).  
* Platná licence Aspose.Pdf pro .NET (bezplatná zkušební verze funguje pro testování).  
* Visual Studio 2022 nebo jakékoli C# IDE, které preferujete.

---

## Krok 1: Instalace Aspose.Pdf pro .NET

Add the NuGet package to your project:

```bash
dotnet add package Aspose.Pdf
```

Balíček obsahuje jmenný prostor `Aspose.Pdf`, který poskytuje třídy `Document`, `DictionaryEditor` a `CosPdfDictionary` použité později.

> **Tip pro profesionály:** Pokud plánujete zpracovávat mnoho PDF souborů najednou, povolte **licenci** brzy v souboru `Program.cs`, abyste se vyhnuli vodoznaku z hodnocení.

```csharp
// Apply your license (optional for evaluation)
Aspose.Pdf.License license = new Aspose.Pdf.License();
license.SetLicense("Aspose.Pdf.lic");
```

## Krok 2: Definujte vstupní a výstupní cesty

Musíte nasměrovat SDK na existující PDF (`input.pdf`) a určit, kam se má uložit upravený soubor (`output.pdf`).

```csharp
// Define input and output PDF file paths
string inputPath = @"C:\MyPdfs\input.pdf";
string outputPath = @"C:\MyPdfs\output.pdf";
```

> **Proč je to důležité:** Použití absolutních cest zabraňuje SDK hledat ve špatném pracovním adresáři, což je častý zdroj `FileNotFoundException`.

## Krok 3: Otevřete PDF a najděte zdroje první stránky

Slovník `ExtGState` se nachází uvnitř slovníku zdrojů každé stránky. Pro jednoduchost upravíme první stránku, ale stejný postup funguje pro libovolný index stránky.

```csharp
using (var pdfDocument = new Aspose.Pdf.Document(inputPath))
{
    // Get the first page (pages are 1‑based)
    var firstPage = pdfDocument.Pages[1];

    // Access the page’s resource dictionary via DictionaryEditor
    var resourcesEditor = new Aspose.Pdf.DictionaryEditor(firstPage.Resources);

    // Retrieve (or create) the ExtGState entry
    var extGStateDict = resourcesEditor["ExtGState"]
        .ToCosPdfDictionary(); // Throws if ExtGState does not exist
```

**Hraniční případ:** Pokud stránka nemá položku `ExtGState`, musíte ji vytvořit:

```csharp
if (!resourcesEditor.ContainsKey("ExtGState"))
{
    var emptyDict = Aspose.Pdf.CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
    resourcesEditor.Add("ExtGState", emptyDict);
    extGStateDict = emptyDict;
}
```

## Krok 4: Vytvořte nový slovník grafického stavu

Grafický stav je kolekce párů klíč/hodnota, která popisuje, jak se chovají kreslicí operace. Pro průhlednost potřebujeme tři klíče:

| Klíč | Význam | Typická hodnota |
|------|--------|-----------------|
| `CA` | Opacity výplně (0 = průhledná, 1 = neprůhledná) | `1` (zcela neprůhledná) |
| `ca` | Opacity čáry (stejná škála) | `0.5` (50 % průhledná) |
| `BM` | Režim prolnutí (např. `Normal`, `Multiply`) | `Normal` |

```csharp
    // Create an empty dictionary that will hold the graphics state
    var newGraphicsState = Aspose.Pdf.CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

    // Populate the dictionary with transparency and blend mode entries
    var graphicsStateEntries = new[]
    {
        new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
            "CA", new Aspose.Pdf.CosPdfNumber(1)),
        new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
            "ca", new Aspose.Pdf.CosPdfNumber(0.5)),
        new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
            "BM", new Aspose.Pdf.CosPdfName("Normal"))
    };

    foreach (var entry in graphicsStateEntries)
        newGraphicsState.Add(entry);
```

**Proč tyto hodnoty?**  
`ca = 0.5` způsobí, že jakákoli čárová cesta (čáry, okraje) bude mít 50 % opacity, zatímco `CA = 1` ponechá vyplněné tvary zcela neprůhledné. Upravením obou čísel dosáhnete požadovaného efektu **úpravy průhlednosti PDF**.

## Krok 5: Vložte grafický stav do slovníku ExtGState

Musíte novému stavu přiřadit jedinečný název (např. `GS0`). Pokud název již existuje, Aspose.Pdf přepíše existující položku, což může narušit další obsah, který na ní závisí.

```csharp
    // Add the new graphics state under a custom name
    const string stateName = "GS0";

    // Ensure we don’t clash with an existing entry
    if (extGStateDict.ContainsKey(stateName))
        extGStateDict.Remove(stateName);

    extGStateDict.Add(stateName, newGraphicsState);
```

Nyní zdroje stránky znají `GS0`. Pro skutečné použití byste odkazovali na grafický stav v content streamu pomocí operátoru `gs` (např. `GS0 gs`). Aspose.Pdf vám umožní vložit surové PDF operátory, pokud potřebujete kreslit vlastní tvary.

## Krok 6: Uložte upravený PDF

```csharp
    // Persist the changes to a new file
    pdfDocument.Save(outputPath);
}
```

Výsledný `output.pdf` obsahuje stejný vizuální obsah jako originál, ale všechny následné kreslicí příkazy, které vyberou `GS0`, budou respektovat nastavené hodnoty průhlednosti.

### Očekávaný výsledek

Otevřete `output.pdf` v Adobe Acrobat nebo jakémkoli PDF prohlížeči. Pokud přidáte novou čáru pomocí grafického stavu `GS0` (např. pomocí `pdfDocument.Pages[1].Contents.Add(...)`), čára se zobrazí poloprůhledně, zatímco výplně zůstanou neprůhledné. To dokazuje, že jste úspěšně **přidali grafický stav PDF** a **upravili průhlednost PDF**.

---

## Kompletní spustitelný příklad

Níže je kompletní program, který můžete zkopírovat a vložit do konzolové aplikace. Obsahuje načítání licence, ošetření chyb a komentáře, které vysvětlují každý ne zcela zřejmý krok.



## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Přidání průhlednosti do PDF pomocí Aspose PDF v C# – krok za krokem](/pdf/english/net/images-graphics/add-transparency-to-pdf-with-aspose-pdf-in-c-step-by-step-gu/)
- [Přidání průhlednosti do PDF pomocí Aspose – kompletní průvodce C#](/pdf/english/net/programming-with-operators/add-transparency-to-pdf-using-aspose-complete-c-guide/)
- [Jak přidat obrázkový razítko do PDF pomocí Aspose.PDF pro .NET: komplexní průvodce](/pdf/english/net/images-graphics/add-image-stamp-pdf-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}