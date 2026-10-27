---
category: general
date: 2026-10-26
description: Naučte se vytvořit prázdný PDF slovník a upravovat PDF zdroje pomocí
  Aspose.PDF pro C#. Průvodce krok za krokem s kompletním ukázkovým kódem.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create empty PDF dictionary
- edit PDF resources
- Aspose.PDF C#
- PDF manipulation C#
- PDF graphics state
language: cs
lastmod: 2026-10-26
og_description: Vytvořte prázdný PDF slovník a upravte PDF zdroje pomocí Aspose.PDF
  pro C#. Sledujte tento kompletní návod k úpravě grafických stavů v PDF.
og_image_alt: Screenshot showing creation of empty PDF dictionary in Aspose.PDF
og_title: Vytvořte prázdný PDF slovník a upravte PDF zdroje v C# – průvodce Aspose.PDF
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn to create empty PDF dictionary and edit PDF resources using Aspose.PDF
    for C#. Step‑by‑step guide with full code example.
  headline: How to create empty PDF dictionary and edit PDF resources with Aspose.PDF
    in C#
  type: TechArticle
- description: Learn to create empty PDF dictionary and edit PDF resources using Aspose.PDF
    for C#. Step‑by‑step guide with full code example.
  name: How to create empty PDF dictionary and edit PDF resources with Aspose.PDF
    in C#
  steps:
  - name: Populate the graphics state entries
    text: 'Add the standard keys:'
  - name: Register the new graphics state in the resource dictionary
    text: Give the state a name (`GS0`) and add it to the `ExtGState` dictionary that
      lives inside the page resources.
  - name: Expected output
    text: 'Running the program prints:'
  type: HowTo
tags:
- Aspose.PDF
- C#
- PDF
title: Jak vytvořit prázdný PDF slovník a upravit PDF zdroje pomocí Aspose.PDF v C#
url: /cs/net/programming-with-document/how-to-create-empty-pdf-dictionary-and-edit-pdf-resources-wi/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak vytvořit prázdný PDF slovník a upravit PDF zdroje pomocí Aspose.PDF v C#

Pokud potřebujete **vytvořit prázdný PDF slovník** a následně **upravit PDF zdroje** v aplikaci C#, tento průvodce vám ukáže přesné kroky. Uvidíte kompletní, spustitelný příklad, který přidá vlastní grafický stav na první stránku existujícího PDF.

Práce s nízkoúrovňovými PDF objekty může působit zastrašujícím dojmem, ale Aspose.PDF poskytuje přehledné API pro manipulaci se slovníky. Na konci tohoto tutoriálu pochopíte, proč je každá operace důležitá a jak přizpůsobit kód pro jiné typy zdrojů.

## Požadavky

* .NET 6.0 (nebo novější) nainstalovaný.
* Licencovaná kopie **Aspose.PDF for .NET** – pro testování funguje i bezplatná zkušební verze.
* IDE, například Visual Studio 2022.
* PDF soubor pojmenovaný `input.pdf` umístěný ve složce, na kterou můžete odkazovat z kódu.

Žádné další NuGet balíčky nejsou potřeba kromě `Aspose.Pdf`.

## Krok 1: Nastavte projekt a importujte jmenné prostory

Vytvořte nový konzolový projekt a přidejte balíček Aspose.PDF:

```bash
dotnet new console -n PdfDictionaryDemo
cd PdfDictionaryDemo
dotnet add package Aspose.Pdf
```

V souboru `Program.cs` importujte jmenné prostory, které budete používat:

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Cos;
```

Tyto importy zpřístupňují třídy `Document`, `DictionaryEditor` a COS (Canonical Object Structure), které vám umožní **vytvořit prázdný PDF slovník** objekty a upravovat existující slovníky zdrojů.

## Krok 2: Definujte složku, která obsahuje PDF soubory

Zadejte adresář, který obsahuje `input.pdf`. Použití absolutní cesty zabraňuje nejasnostem, když se program spouští z jiného pracovního adresáře.

```csharp
// Step 1: Define the folder that contains the PDF files
string dataDir = @"C:\PdfDemo\";
```

Nahraďte `C:\PdfDemo\` cestou na vašem počítači. Uložení cesty do proměnné usnadňuje opakované použití pro vstupní i výstupní soubory.

## Krok 3: Otevřete zdrojový PDF dokument

Načtěte PDF, které chcete upravit, uvnitř bloku `using`, aby se souborový handle automaticky uvolnil.

```csharp
// Step 2: Open the source PDF document
using (var pdfDocument = new Document(dataDir + "input.pdf"))
{
    // The rest of the workflow lives inside this block
}
```

Otevřením dokumentu získáte přístup k jeho kolekci stránek, slovníkům zdrojů a nízkoúrovňovým COS objektům.

## Krok 4: Získejte první stránku a její slovník zdrojů

První stránka je indexována číslem `1` (PDF stránky jsou číslovány od 1). Získejte slovník `Resources` stránky a zabalte jej do `DictionaryEditor`, aby bylo možné bezpečně upravovat.

```csharp
// Step 3: Access the first page and its resource dictionary
var firstPage = pdfDocument.Pages[1];
var resourcesEditor = new DictionaryEditor(firstPage.Resources);
```

`DictionaryEditor` abstrahuje podkladovou strukturu COS, což vám umožní číst nebo vytvářet položky, aniž byste PDF poškodili.

## Krok 5: **Vytvořit prázdný PDF slovník** pro nový grafický stav

Grafický stav řídí průhlednost, režim prolnutí a další parametry kreslení. Pro přidání vlastního stavu nejprve potřebujete prázdný slovník, který následně naplníte požadovanými položkami.

```csharp
// Step 4: Retrieve the ExtGState dictionary and add a new graphics state
var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();

// Create an empty dictionary that will hold the graphics state parameters
var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
```

Volání `CreateEmptyDictionary` je jádrem **vytváření prázdného PDF slovníku** objektů. Vrací COS slovník, který patří stejnému dokumentu, což zajišťuje integritu křížových odkazů.

### Naplňte položky grafického stavu

Přidejte standardní klíče:

* `CA` – konstantní alfa hodnota pro kreslení (rozsah 0 – 1).
* `ca` – konstantní alfa hodnota pro ne‑kreslení.
* `BM` – název režimu prolnutí.

```csharp
var graphicsStateEntries = new[]
{
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
};

foreach (var entry in graphicsStateEntries)
    newGraphicsState.Add(entry);
```

Každá položka je přidána do prázdného slovníku, který jste právě vytvořili. Oddělením definice od smyčky vkládání zůstane kód čitelný a snadno rozšířitelný o další klíče později.

### Zaregistrujte nový grafický stav ve slovníku zdrojů

Dejte stavu název (`GS0`) a přidejte jej do slovníku `ExtGState`, který se nachází uvnitř zdrojů stránky.

```csharp
// Name the new graphics state "GS0"
extGStateDict.Add("GS0", newGraphicsState);
```

Nyní slovník zdrojů stránky obsahuje odkaz na vlastní grafický stav, který můžete později použít v obsahových tocích.

## Krok 6: Uložte aktualizovaný PDF

Nakonec zapište upravený dokument do nového souboru. Zachování originálu nedotčeného vám pomůže ověřit změny.

```csharp
// Step 5: Save the updated PDF
pdfDocument.Save(dataDir + "output.pdf");
```

Když otevřete `output.pdf` v prohlížeči, který podporuje inspekci grafických stavů (např. Adobe Acrobat Pro), uvidíte, že slovník `ExtGState` obsahuje položku pojmenovanou `GS0` s hodnotami, které jste definovali.

## Kompletní zdrojový kód

Spojením všech částí dohromady získáte samostatný program:

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Cos;

class Program
{
    static void Main()
    {
        // Step 1: Define the folder that contains the PDF files
        string dataDir = @"C:\PdfDemo\"; // adjust to your environment

        // Step 2: Open the source PDF document
        using (var pdfDocument = new Document(dataDir + "input.pdf"))
        {
            // Step 3: Access the first page and its resource dictionary
            var firstPage = pdfDocument.Pages[1];
            var resourcesEditor = new DictionaryEditor(firstPage.Resources);

            // Step 4: Retrieve the ExtGState dictionary and add a new graphics state
            var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();

            // **Create empty PDF dictionary** for the new graphics state
            var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            var graphicsStateEntries = new[]
            {
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
            };

            foreach (var entry in graphicsStateEntries)
                newGraphicsState.Add(entry);

            // Register the new graphics state as "GS0"
            extGStateDict.Add("GS0", newGraphicsState);

            // Step 5: Save the updated PDF
            pdfDocument.Save(dataDir + "output.pdf");
        }

        Console.WriteLine("PDF updated successfully.");
    }
}
```

### Očekávaný výstup

Spuštěním programu se vytiskne:

```
PDF updated successfully.
```

a vytvoří `output.pdf` ve stejné složce. Otevřením souboru se zobrazí nová položka pod **Resources → ExtGState → GS0** s parametry, které jste nastavili.

## Běžné varianty a okrajové případy

| Situace | Jak upravit kód |
|-----------|-----------------------|
| **Více stránek** potřebuje stejný grafický stav | Vytvořte slovník jednou a poté přidejte stejný odkaz `GS0` do slovníku `ExtGState` každé stránky. |
| **Jiný režim prolnutí** (např. `Multiply`) | Změňte hodnotu `CosPdfName("Normal")` na `CosPdfName("Multiply")`. |
| **Chybí existující slovník ExtGState** | Před přístupem k `resourcesEditor["ExtGState"]` zkontrolujte `resourcesEditor.ContainsKey("ExtGState")`. Pokud chybí, vytvořte nový prázdný slovník a přidejte jej do `firstPage.Resources`. |
| **Velké PDF** způsobují tlak na paměť | Použijte přetížení `PdfDocument.Load`, které streamuje stránky, nebo zpracovávejte stránky po jedné uvnitř bloku `using`. |
| **Potřeba upravit jiné zdroje** (fonty, XObjects) | Nahraďte `"ExtGState"` za `"Font"` nebo `"XObject"` ve vyhledávání `resourcesEditor` a poté postupujte podle stejného vzoru – vytvořte prázdný slovník a naplňte jej. |

Tyto varianty ukazují, jak stejný vzor **vytvořit prázdný PDF slovník** platí pro jakýkoli typ zdroje, který chcete **upravit PDF zdroje**.

## Profesionální tipy

* **Ověřte výsledek** – po uložení otevřete PDF v nástroji, který dokáže zobrazit surový slovník zdrojů (např. `PDFDebugger` z PDF‑Box), aby bylo jisté, že položka existuje.
* **Znovu používejte slovníky** – pokud přidáváte stejný grafický stav na mnoho stránek, uložte slovník do proměnné a odkazujte na něj místo opakovaného vytváření.
* **Kompatibilita verzí** – kód funguje s Aspose.PDF 23.12 a novějšími. Starší verze mohou vyžadovat `CosDictionary` místo `CosPdfDictionary`.

## Závěr

Nyní víte, jak **vytvořit prázdný PDF slovník** objekty a **upravit PDF zdroje** pomocí Aspose.PDF pro C#. Tutoriál pokrýval otevření dokumentu, přístup ke slovníku zdrojů stránky, vytvoření vlastního grafického stavu, jeho registraci a uložení výsledku. Odtud můžete experimentovat s dalšími typy zdrojů, kombinovat více grafických stavů nebo integrovat tuto techniku do většího pipeline pro zpracování PDF.

---

*Připraveni na další průzkum? Zkuste přidat vlastní **ExtGState** do obsahového proudu, nebo manipulovat se slovníkem **Font** pro vložení nových fontů. Obě možnosti následují stejný vzor – vytvořit prázdný slovník a upravit PDF zdroje.*

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Upravit slovník PDF zdrojů pomocí Aspose.PDF – C# průvodce](/pdf/english/net/programming-with-operators/edit-pdf-resource-dictionary-with-aspose-pdf-c-guide/)
- [Vytvořit vlastní grafický stav v PDF pomocí Aspose.Pdf](/pdf/english/net/programming-with-operators/create-custom-graphics-state-in-pdf-using-aspose-pdf/)
- [Jak vytvořit prázdný grafický stav v PDF s C#](/pdf/english/net/programming-with-operators/how-to-create-empty-graphics-state-in-a-pdf-with-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}