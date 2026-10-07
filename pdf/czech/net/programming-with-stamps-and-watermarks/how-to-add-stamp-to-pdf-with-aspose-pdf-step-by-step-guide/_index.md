---
category: general
date: 2026-03-24
description: Jak přidat razítko do PDF pomocí Aspose.Pdf v C#. Naučte se umístit razítko
  do PDF a přidat textové razítko do PDF s automatickým přizpůsobením velikosti během
  několika snadných kroků.
draft: false
keywords:
- how to add stamp
- place stamp pdf
- add text stamp pdf
- Aspose.Pdf stamp example
- C# PDF annotation
language: cs
og_description: Jak přidat razítko do PDF v C#? Tento průvodce vám ukáže, jak umístit
  razítko do PDF a přidat textové razítko do PDF s automatickým nastavením velikosti
  písma pomocí Aspose.Pdf.
og_title: Jak přidat razítko do PDF pomocí Aspose.Pdf – rychlý průvodce
tags:
- pdf
- csharp
- aspose
- stamping
title: Jak přidat razítko do PDF pomocí Aspose.Pdf – krok za krokem
url: /cs/net/programming-with-stamps-and-watermarks/how-to-add-stamp-to-pdf-with-aspose-pdf-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak přidat razítko do PDF pomocí Aspose.Pdf – krok za krokem průvodce

**Jak přidat razítko** do PDF je běžná potřeba, když chcete dokument označit, certifikovat nebo jen poznamenat. Přemýšleli jste někdy, jaký je nejjednodušší způsob, jak umístit razítko PDF bez boje s nízkoúrovňovou grafikou? V tomto tutoriálu projdeme kompletní, připravené řešení, které nejen ukazuje **Jak přidat razítko**, ale také vysvětluje *proč* je každý řádek důležitý.

Naučíte se, jak **place stamp PDF** na libovolnou stránku, jak **add text stamp PDF**, které se automaticky zmenší, aby se vešlo do svého obdélníku, a jaké úskalí se vyhnout, když je text příliš dlouhý. Na konci budete mít jediný soubor C#, který můžete vložit do svého projektu a okamžitě začít razítkovat PDF soubory.

## Požadavky

* .NET 6.0 nebo novější (kód funguje také s .NET Core a .NET Framework).
* NuGet balíček Aspose.Pdf pro .NET (`Aspose.Pdf`) nainstalován.
* PDF soubor pojmenovaný `input.pdf` ve složce, na kterou můžete odkazovat (stačí jakýkoli jednoduchý jednosouborový PDF).

Žádná další konfigurace není vyžadována — Aspose.Pdf se postará o veškerou těžkou práci.

## Krok 1: Nastavení projektu a načtení zdrojového PDF

Prvním, co potřebujeme, je objekt `Document`, který představuje PDF, které chceme anotovat. Představte si to jako načtení prázdného plátna, na které později namalujeme razítko.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Load the source PDF document
// The using statement ensures the file is closed automatically.
using var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");
```

> **Proč je to důležité:** `Document` je vstupní bod pro jakoukoli manipulaci s PDF v Aspose.Pdf. Použitím vzoru `using` zajišťujeme uvolnění souborového handle, což zabraňuje problémům se zamčením souboru, když později ukládáte upravený PDF.

## Krok 2: Vytvoření textového razítka s automatickým přizpůsobením velikosti písma

Nyní vytvoříme `TextStamp`. Trik, který tento příklad odlišuje, je příznak `AutoAdjustFontSizeToFitStampRectangle` — říká Aspose, aby zmenšil text, dokud se nevejde do definovaného obdélníku.

```csharp
// Create a text stamp that will automatically resize to fit its rectangle
var textStamp = new TextStamp("Long text that must fit")
{
    // Let Aspose shrink the text if it overflows
    AutoAdjustFontSizeToFitStampRectangle = true,
    // Precision of the auto‑adjust algorithm (lower = more accurate)
    AutoAdjustFontSizePrecision = 0.01f,
    // Define the stamp's bounding box (in points)
    Width = 300,
    Height = 100,
    // Word‑wrap by whole words so we don’t split in the middle of a word
    WordWrapMode = TextFormattingOptions.WordWrapMode.ByWords,
    // Optional: set background color or opacity if you want a visible box
    Background = new Background()
    {
        Color = Color.LightGray,
        Opacity = 0.5
    }
};
```

> **Tip:** Pokud potřebujete místo textu logo nebo obrázek, použijte `ImageStamp` — stejná logika automatického přizpůsobení existuje i pro škálování obrázku.

## Krok 3: Vyberte, kam **Place Stamp PDF** – první stránka, poslední stránka nebo vlastní index

Aspose.Pdf ukládá stránky v kolekci číslované od 1 (`pdfDocument.Pages[1]` je první stránka). Můžete **place stamp PDF** na libovolnou stránku změnou indexu.

```csharp
// Place the stamp on the first page (index 1)
// To stamp the last page use pdfDocument.Pages[pdfDocument.Pages.Count]
pdfDocument.Pages[1].AddStamp(textStamp);
```

> **Proč je to flexibilní:** Protože kolekce `Pages` je měnitelná, můžete projít všechny stránky a přidat na každou stejné razítko, nebo můžete cílit na konkrétní stránku podle obchodní logiky (např. jen titulní stránku).

## Krok 4: Uložení upraveného dokumentu

Po přidání razítka musíte změny zapsat zpět na disk. Můžete přepsat původní soubor nebo vytvořit nový — na vás.

```csharp
// Save the stamped PDF – change the path if you don’t want to overwrite
pdfDocument.Save("YOUR_DIRECTORY/output-stamped.pdf");
```

Když otevřete `output-stamped.pdf`, uvidíte světle šedý obdélník na první stránce obsahující text „Long text that must fit“. Pokud by byl text delší, Aspose by jej automaticky zmenšil, dokud by se perfektně vešel do obdélníku 300 × 100 pt.

## Kompletní funkční příklad

Níže je kompletní program, který můžete zkopírovat a vložit do konzolové aplikace (`Program.cs`). Obsahuje všechny části, o kterých jsme mluvili, plus malý pomocník pro ověření, že se razítko zobrazí.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Drawing;   // Needed for Background and Color

namespace PdfStampDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the source PDF
            using var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");

            // 2️⃣ Create a text stamp with auto‑adjusting font size
            var textStamp = new TextStamp("Long text that must fit")
            {
                AutoAdjustFontSizeToFitStampRectangle = true,
                AutoAdjustFontSizePrecision = 0.01f,
                Width = 300,
                Height = 100,
                WordWrapMode = TextFormattingOptions.WordWrapMode.ByWords,
                Background = new Background()
                {
                    Color = Color.LightGray,
                    Opacity = 0.5
                }
            };

            // 3️⃣ Place the stamp on the first page (you can change the index)
            pdfDocument.Pages[1].AddStamp(textStamp);

            // 4️⃣ Save the result
            string outputPath = "YOUR_DIRECTORY/output-stamped.pdf";
            pdfDocument.Save(outputPath);

            Console.WriteLine($"Stamp added successfully! Check the file at: {outputPath}");
        }
    }
}
```

### Očekávaný výsledek

* PDF se otevře se semi‑transparentním šedým boxem na první stránce.
* Uvnitř boxu se dodaný text perfektně vejde, i když jej nahradíte delší větou.
* Není potřeba ručně počítat velikost písma — Aspose se postará o těžkou práci.

## Časté úskalí při **Place Stamp PDF**

| Symptom | Likely Cause | Fix |
|---------|--------------|-----|
| Text je oříznut | `AutoAdjustFontSizeToFitStampRectangle` je **false** nebo je obdélník příliš malý. | Povolte příznak a zvětšete `Width`/`Height` nebo zkraťte text. |
| Razítko se zobrazuje mimo střed | Výchozí `HorizontalAlignment`/`VerticalAlignment` jsou `Left`/`Top`. | Nastavte `HorizontalAlignment = HorizontalAlignment.Center` a `VerticalAlignment = VerticalAlignment.Center`. |
| Razítko není viditelné v některých prohlížečích | Průhlednost pozadí je nastavena na 0 nebo barva razítka odpovídá pozadí stránky. | Použijte kontrastní `Background.Color` nebo nastavte `Opacity` > 0.3. |
| Více razítek se překrývá | Přidávání razítek ve smyčce bez úpravy souřadnic. | Použijte `textStamp.XIndent` a `textStamp.YIndent` k posunutí každého razítka. |

## Rozšíření příkladu: Přidání obrázkového razítka

Pokud potřebujete **add text stamp PDF** *a* obrázek (např. firemní logo), můžete je kombinovat:

```csharp
var imageStamp = new ImageStamp("YOUR_DIRECTORY/logo.png")
{
    Width = 100,
    Height = 50,
    XIndent = 400,          // Position to the right of the text stamp
    YIndent = 20,
    Background = new Background()
    {
        Color = Color.Transparent
    }
};

pdfDocument.Pages[1].AddStamp(imageStamp);
```

Nyní stránka zobrazuje jak dynamické textové razítko, tak statické obrázkové razítko vedle sebe.

## Testování vaší implementace

1. Spusťte konzolovou aplikaci.  
2. Otevřete `output-stamped.pdf` v Adobe Reader, Edge nebo jakémkoli PDF prohlížeči.  
3. Ověřte, že obdélník razítka je přítomen a text je plně viditelný.  
4. Změňte text na delší frázi, spusťte znovu a potvrďte, že písmo se automaticky zmenšuje.

Pokud něco vypadá špatně, zkontrolujte rozměry obdélníku a nastavení `AutoAdjustFontSizePrecision`.

## Závěr

Nyní víte, **how to add stamp** do PDF pomocí Aspose.Pdf, jak **place stamp PDF** na konkrétní stránku a jak **add text stamp PDF**, který automaticky upravuje velikost písma. Kompletní, spustitelný příklad výše eliminuje hádání a poskytuje pevný základ pro pokročilejší scénáře razítkování — jako hromadné zpracování desítek souborů nebo podmíněné přidávání vodoznaků.

Připraveni na další krok? Zkuste razítkovat každou stránku ve smyčce, experimentujte s různými fonty nebo kombinujte obrázek a textové razítko pro vytvoření profesionální pečeti. Možnosti jsou neomezené a s Aspose.Pdf máte spolehlivý motor pod kapotou.

Pokud narazíte na problémy, zanechte komentář nebo si prohlédněte dokumentaci Aspose.Pdf pro podrobnější možnosti přizpůsobení. Šťastné razítkování!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}