---
category: general
date: 2026-02-22
description: Návod na důvěrný vodoznak PDF pomocí Aspose.Pdf – naučte se, jak přidat
  označení „důvěrné“ jako textové razítko na první stránku libovolného PDF.
draft: false
keywords:
- confidential watermark pdf
- add confidential label
- aspose pdf watermark
- add stamp first page
- add text stamp pdf
language: cs
og_description: 'Průvodce důvěrným vodotiskem PDF: krok za krokem návod, jak přidat
  označení „důvěrné“ jako textové razítko na první stránku pomocí Aspose.Pdf pro .NET.'
og_title: Důvěrný vodoznak PDF s Aspose – Přidat textové razítko
tags:
- aspose
- pdf
- watermark
- csharp
title: 'Důvěrná vodoznak PDF s Aspose: Přidat textové razítko na první stránku'
url: /cs/net/programming-with-stamps-and-watermarks/confidential-watermark-pdf-with-aspose-add-a-text-stamp-to-f/
---

Let's write.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Důvěrný vodoznak PDF – Jak přidat textový razítko na první stránku

Už jste někdy potřebovali **confidential watermark PDF**, ale nebyli jste si jisti, jak přidat štítek jen na první stránku? Nejste sami – mnoho vývojářů se potýká s otázkou „Jak přidat důvěrný štítek, aniž by se narušilo rozložení?“

Dobrá zpráva? S Aspose.Pdf pro .NET to můžete udělat během několika řádků a já vás provedu celým procesem právě teď. Žádné vágní odkazy, jen kompletní řešení připravené ke zkopírování a vložení, které funguje dnes.

## Co se naučíte

* Instalace NuGet balíčku Aspose.Pdf (jediná předpoklad).
* Načtení existujícího PDF.
* Vytvoření **confidential watermark PDF** pomocí `TextStamp`.
* Přidání tohoto razítka pouze na **první stránku** (požadavek „add stamp first page“).
* Uložení výsledku a ověření výstupu.

## Požadavky

* .NET 6+ (kód funguje jak na .NET Core, tak na .NET Framework).
* Visual Studio 2022 nebo jakékoli jiné IDE, které preferujete.
* Aspose.Pdf pro .NET – verze 23.10 nebo novější se doporučuje pro nejnovější opravy chyb.

Pokud jste ještě nepřidali Aspose.Pdf do svého projektu, spusťte:

```bash
dotnet add package Aspose.Pdf
```

A to je vše – žádné další DLL, žádné problémy s licencí pro trial (jen nezapomeňte před nasazením aplikace použít licenční klíč).

## Krok 1: Načtení zdrojového PDF dokumentu

Nejprve musíme otevřít soubor, který chceme chránit. Třída `Document` představuje celý PDF a načtení je tak jednoduché jako předání cesty.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Path to the PDF you want to watermark
string inputPdfPath = @"C:\MyDocs\input.pdf";

// Load the PDF into memory
using var pdfDocument = new Document(inputPdfPath);
```

*Proč je to důležité*: Načtení dokumentu vám poskytne přístup ke kolekci `Pages`, kam připojíme razítko. Použití `using var` zajistí, že souborový handle bude rychle uvolněn – důležité při práci s velkými dávkami.

## Krok 2: Vytvoření důvěrného textového razítka

Nyní vytvoříme vizuální štítek. `TextStamp` nám umožňuje řídit velikost, zalamování a škálování. Následující nastavení zajistí, že slovo *Confidential* bude hezky pasovat bez přetečení.

```csharp
// Build a text stamp that says "Confidential"
var confidentialStamp = new TextStamp("Confidential")
{
    // Auto‑adjust the font so it never exceeds the rectangle
    AutoAdjustFontSizeToFitStampRectangle = true,
    AutoAdjustFontSizePrecision = 0.01f,

    // Wrap by whole words—no broken words in the middle
    WordWrapMode = TextFormattingOptions.WordWrapMode.ByWords,

    // Define the stamp rectangle (you can tweak width/height)
    Width = 300,
    Height = 100,

    // Keep the stamp size constant even if the page is resized
    Scale = false
};
```

**Pro tip**: Pokud potřebujete jiný font nebo barvu, nastavte `confidentialStamp.TextState.Font` a `confidentialStamp.TextState.ForegroundColor`. Například `confidentialStamp.TextState.Font = FontRepository.FindFont("Arial")` a `confidentialStamp.TextState.ForegroundColor = Color.Red`.

## Krok 3: Přidání razítka pouze na první stránku

Aspose používá indexaci stránek od 1, takže `Pages[1]` je první stránka. Přidání razítka tam splňuje požadavek **add stamp first page**.

```csharp
// Attach the stamp to the very first page
pdfDocument.Pages[1].AddStamp(confidentialStamp);
```

Pokud byste někdy potřebovali vodoznakovat každou stránku, projděte `pdfDocument.Pages` ve smyčce. Pro jednostránkový štítek však tento jednorázový řádek stačí.

## Krok 4: Uložení vodoznakovaného PDF

Nakonec zapíšeme upravený dokument zpět na disk. Můžete přepsat originál nebo vytvořit nový soubor – na vás.

```csharp
// Destination path for the watermarked PDF
string outputPdfPath = @"C:\MyDocs\Stamped.pdf";

// Persist the changes
pdfDocument.Save(outputPdfPath);
```

Když otevřete `Stamped.pdf`, uvidíte *Confidential* vykreslené v levém horním rohu stránky 1 (nebo tam, kde jste razítko umístili). Zbytek dokumentu zůstane nedotčený.

## Očekávaný výsledek

| Před | Po (první stránka) |
|--------|-------------------|
| ![Původní stránka PDF](/images/original.png "Původní stránka PDF") | ![Příklad důvěrného vodoznaku PDF](/images/confidential-watermark.png "Příklad důvěrného vodoznaku PDF") |

*Text alt obrázku*: **confidential watermark PDF example** (obsahuje hlavní klíčové slovo).

## Okrajové případy a časté otázky

### Co když PDF nemá žádné stránky?

Pokus o přístup k `Pages[1]` vyvolá `ArgumentOutOfRangeException`. Ošetřete to:

```csharp
if (pdfDocument.Pages.Count == 0)
    throw new InvalidOperationException("The PDF is empty.");
```

### Jak vodoznakovat více stránek?

```csharp
foreach (Page page in pdfDocument.Pages)
{
    page.AddStamp(confidentialStamp);
}
```

Nezapomeňte resetovat pozici `confidentialStamp`, pokud ji chcete mít na různých rozích podle stránky.

### Můžu změnit pozici razítka?

Ano – nastavte `confidentialStamp.HorizontalAlignment` a `confidentialStamp.VerticalAlignment`, nebo použijte `confidentialStamp.XIndent` / `YIndent` pro pixel‑přesné umístění.

### Funguje to s PDF chráněnými heslem?

Aspose může otevřít šifrované soubory, pokud zadáte heslo:

```csharp
var pdfDocument = new Document(inputPdfPath, new LoadOptions { Password = "mySecret" });
```

### Jaká je výkonnost při velkých dávkách?

Načítání a ukládání každého dokumentu zvlášť může být I/O‑náročné. Zvažte opětovné použití jedné instance `Document` pro operace v paměti a ukládejte jen jednou na dávku.

## Kompletní funkční příklad

Níže je kompletní program, který můžete zkopírovat a vložit do konzolové aplikace. Obsahuje všechny kroky, ošetření chyb a jednoduchou ověřovací zprávu.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Load the source PDF
        // -------------------------------------------------
        string inputPdfPath = @"C:\MyDocs\input.pdf";
        if (!System.IO.File.Exists(inputPdfPath))
        {
            Console.WriteLine("Input file not found.");
            return;
        }

        using var pdfDocument = new Document(inputPdfPath);

        if (pdfDocument.Pages.Count == 0)
        {
            Console.WriteLine("The PDF contains no pages.");
            return;
        }

        // -------------------------------------------------
        // 2️⃣ Create the confidential text stamp
        // -------------------------------------------------
        var confidentialStamp = new TextStamp("Confidential")
        {
            AutoAdjustFontSizeToFitStampRectangle = true,
            AutoAdjustFontSizePrecision = 0.01f,
            WordWrapMode = TextFormattingOptions.WordWrapMode.ByWords,
            Width = 300,
            Height = 100,
            Scale = false,
            // Optional styling
            TextState = { FontSize = 24, Font = FontRepository.FindFont("Arial"), ForegroundColor = Color.Red }
        };

        // -------------------------------------------------
        // 3️⃣ Add the stamp to the first page only
        // -------------------------------------------------
        pdfDocument.Pages[1].AddStamp(confidentialStamp);

        // -------------------------------------------------
        // 4️⃣ Save the result
        // -------------------------------------------------
        string outputPdfPath = @"C:\MyDocs\Stamped.pdf";
        pdfDocument.Save(outputPdfPath);

        Console.WriteLine($"Successfully added a confidential watermark PDF. Saved to: {outputPdfPath}");
    }
}
```

Spusťte program, otevřete `Stamped.pdf` a uvidíte **confidential watermark PDF** aplikovaný přesně tam, kde jsme zamýšleli.

## Závěr

Nyní máte solidní, připravené pro produkci řešení, jak **add a confidential label** jako **text stamp** na **first page** libovolného PDF pomocí Aspose.Pdf. Řešení je zcela samostatné, funguje s nejnovějšími verzemi .NET a lze jej rozšířit na více stránek, vlastní fonty nebo různé barvy.

**Další kroky**, které můžete prozkoumat:

* Vyměňte textové razítko za obrazové razítko (`ImageStamp`) a vložte logo.
* Kombinujte tento přístup se smyčkou a vytvořte **aspose pdf watermark** napříč celým dokumentem.
* Integrovat kód do ASP.NET Core API, aby uživatelé mohli nahrávat PDF a okamžitě získat vodoznakované verze.

Vyzkoušejte to, upravte rozměry a nechte techniku **add text stamp pdf** stát se základním nástrojem ve vaší sadě pro zabezpečení dokumentů. Šťastné programování!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}