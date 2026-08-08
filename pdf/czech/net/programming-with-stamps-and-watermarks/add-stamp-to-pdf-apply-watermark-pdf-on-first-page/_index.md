---
category: general
date: 2026-03-19
description: Přidejte razítko do PDF na první stránku a aplikujte vodoznak PDF pomocí
  Aspose.Pdf v C#. Naučte se, jak přidat poznámku do PDF a podívejte se na kompletní
  funkční příklad.
draft: false
keywords:
- add stamp to pdf
- apply watermark pdf
- add note to pdf
- how to add stamp
- add stamp first page
language: cs
og_description: Přidejte razítko do PDF na první stránku a aplikujte vodoznak PDF
  pomocí Aspose.Pdf v C#. Kompletní návod krok za krokem.
og_title: Přidat razítko do PDF – Aplikovat vodoznak na první stránku PDF
tags:
- aspnet
- csharp
- pdf
- aspose
title: Přidat razítko do PDF – Aplikovat vodoznak PDF na první stránku
url: /cs/net/programming-with-stamps-and-watermarks/add-stamp-to-pdf-apply-watermark-pdf-on-first-page/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Přidat razítko do PDF – Použít vodoznak PDF na první stránce

Už jste někdy potřebovali **add stamp to PDF**, ale nebyli jste si jisti, kde začít? Možná také chcete **apply watermark PDF** na té stejné stránce, nebo jen rychle **add note to PDF** pro recenzenty. V tomto tutoriálu projdeme kompletní, připravený příklad v C#, který přesně to dělá, a vysvětlíme „proč“ za každým řádkem, abyste jej mohli přizpůsobit libovolnému scénáři.

Probereme vše od načtení zdrojového dokumentu po uložení verze s razítkem, plus několik tipů pro práci s více stránkovými PDF, problémy se škálováním a přizpůsobení vzhledu razítka. Na konci budete schopni s jistotou odpovědět na otázku „**how to add stamp**?“ a vědět, jak **add stamp first page** bez potíží.

---

## Co budete potřebovat

- **Aspose.Pdf for .NET** (any recent version, e.g., 23.10) – knihovna, která usnadňuje manipulaci s PDF.  
- Vývojové prostředí .NET (Visual Studio, VS Code, Rider – co vám vyhovuje).  
- Vstupní PDF soubor (nazveme jej `input.pdf`) umístěný ve složce, na kterou můžete odkazovat.  

Žádné další NuGet balíčky kromě Aspose.Pdf nejsou potřeba a kód funguje na .NET 6+ i na .NET Framework 4.7.2.

![Přidat razítko do PDF příklad](/images/add-stamp-to-pdf.png "Snímek obrazovky ukazující PDF s textovým razítkem – add stamp to pdf")

*Alt text: add stamp to pdf – vizuální příklad textového razítka aplikovaného na první stránku PDF.*

## Krok 1 – Načtení zdrojového PDF dokumentu

Pro **add stamp to PDF** nejprve potřebujeme v‑paměti reprezentaci souboru. Třída `Aspose.Pdf.Document` provádí těžkou práci.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;

class PdfStampDemo
{
    static void Main()
    {
        // Load the original PDF (replace YOUR_DIRECTORY with your actual path)
        var pdfPath = @"YOUR_DIRECTORY\input.pdf";
        using var pdfDocument = new Document(pdfPath);
```

**Proč je to důležité:**  
`Document` parsuje strukturu souboru, poskytuje přístup k stránkám, anotacím a zdrojům. Použití bloku `using` zajišťuje rychlé uvolnění souborového handle – což je důležité, když později chcete přepsat stejný soubor.

## Krok 2 – Vytvoření a konfigurace TextStamp

Nyní **add note to PDF** vytvořením `TextStamp`. Tento objekt se chová jako vodoznak, ale můžete ovládat velikost, písmo a zalamování textu.

```csharp
        // Step 2: Create a text stamp that will serve as a note/watermark
        var textStamp = new TextStamp("Important note")
        {
            // Auto‑adjust font size so the text fits inside the stamp rectangle
            AutoAdjustFontSizeToFitStampRectangle = true,
            AutoAdjustFontSizePrecision = 0.01f,

            // Wrap words rather than breaking them mid‑word
            WordWrapMode = TextFormattingOptions.WordWrapMode.ByWords,

            // Define the stamp rectangle (you can tweak these values)
            Width = 400,
            Height = 200,

            // Turn off scaling – we want the stamp to keep its exact size
            Scale = false
        };
```

**Klíčové body k zapamatování:**

- `AutoAdjustFontSizeToFitStampRectangle` umožňuje razítku zmenšovat nebo zvětšovat tak, aby text nikdy nepřetekl – užitečné při **applying watermark PDF** na různé velikosti stránek.  
- `WordWrapMode.ByWords` zajišťuje, že text se zalamuje na mezích slov, což činí poznámku čitelnou.  
- Nastavení `Scale = false` zabraňuje natažení razítka, pokud se změní DPI stránky.

## Krok 3 – Připojení razítka k první stránce

Pokud se ptáte **how to add stamp** konkrétně na první stránku, zde je to místo. Kolekce `Pages` je číslována od 1, takže `Pages[1]` je první stránka.

```csharp
        // Step 3: Add the configured stamp to the first page
        pdfDocument.Pages[1].AddStamp(textStamp);
```

**Proč první stránka?**  
Mnoho právních nebo brandových požadavků vyžaduje viditelný vodoznak pouze na titulní stránce. Cílením na `Pages[1]` splníme scénář **add stamp first page** bez procházení celého dokumentu.

## Krok 4 – Uložení upraveného PDF

Nakonec zapíšeme změny zpět na disk. Můžete přepsat originál nebo vytvořit nový soubor; zde vygenerujeme `Stamped.pdf`.

```csharp
        // Step 4: Save the stamped PDF
        var outputPath = @"YOUR_DIRECTORY\Stamped.pdf";
        pdfDocument.Save(outputPath);
        Console.WriteLine($"Stamp added successfully! Output saved to {outputPath}");
    }
}
```

Spuštěním programu vznikne PDF, kde první stránka zobrazuje razítko „Important note“, čímž se efektivně **adding a stamp to pdf** a také **applying watermark pdf** v jednom kroku.

## Volitelné: Ladění razítka pro různé scénáře

### Více stránek

Pokud později rozhodnete, že potřebujete stejnou poznámku na *každé* stránce, nahraďte řádek pro jedinou stránku smyčkou:

```csharp
foreach (var page in pdfDocument.Pages)
{
    page.AddStamp(textStamp);
}
```

### Obrázkové razítka

Aspose také podporuje `ImageStamp`, pokud dáváte přednost logu místo textu. Stejné vlastnosti (velikost, pozice, škálování) se použijí.

### Umístění razítka

Ve výchozím nastavení se razítko zobrazuje v levém horním rohu obdélníku. Pro jeho posunutí nastavte `HorizontalAlignment` a `VerticalAlignment`:

```csharp
textStamp.HorizontalAlignment = HorizontalAlignment.Center;
textStamp.VerticalAlignment = VerticalAlignment.Middle;
```

## Časté úskalí a profesionální tipy

- **File locks:** Pokud získáte `IOException` s hláškou, že soubor je používán, ujistěte se, že žádný jiný proces (včetně Průzkumníka) nemá PDF otevřené. Blok `using` pomáhá, ale zkontrolujte to dvakrát.  
- **Font issues:** Aspose používá výchozí systémová písma. Pro ne‑latinské skripty vložte požadované písmo nebo explicitně nastavte `textStamp.Font`.  
- **Large PDFs:** Pro PDF soubory větší než 100 MB zvažte použití `pdfDocument.Optimize()` před uložením, aby se snížila velikost souboru.  
- **Testing:** Otevřete výsledný `Stamped.pdf` v několika prohlížečích (Adobe Reader, Edge, Chrome), abyste ověřili, že razítko se vykresluje konzistentně.

## Kompletní funkční příklad (připravený ke kopírování a vložení)

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;

class PdfStampDemo
{
    static void Main()
    {
        // 1️⃣ Load the source PDF
        var pdfPath = @"YOUR_DIRECTORY\input.pdf";
        using var pdfDocument = new Document(pdfPath);

        // 2️⃣ Create a configurable text stamp (our note/watermark)
        var textStamp = new TextStamp("Important note")
        {
            AutoAdjustFontSizeToFitStampRectangle = true,
            AutoAdjustFontSizePrecision = 0.01f,
            WordWrapMode = TextFormattingOptions.WordWrapMode.ByWords,
            Width = 400,
            Height = 200,
            Scale = false,
            HorizontalAlignment = HorizontalAlignment.Center,
            VerticalAlignment = VerticalAlignment.Middle
        };

        // 3️⃣ Add the stamp to the first page (add stamp first page)
        pdfDocument.Pages[1].AddStamp(textStamp);

        // 4️⃣ Save the stamped PDF
        var outputPath = @"YOUR_DIRECTORY\Stamped.pdf";
        pdfDocument.Save(outputPath);

        Console.WriteLine($"Stamp added successfully! Output saved to {outputPath}");
    }
}
```

**Očekávaný výsledek:** Otevřete `Stamped.pdf`; první stránka zobrazuje centrovaný rámec „Important note“ o rozměrech 400 × 200 bodů, přičemž text je automaticky přizpůsoben tak, aby se vešel. Všechny ostatní stránky zůstávají nedotčeny.

## Závěr

Právě jsme ukázali, jak **add stamp to pdf** a **apply watermark pdf** čistým, znovupoužitelným způsobem. Načtením dokumentu, konfigurací `TextStamp`, připojením k **add stamp first page** a uložením získáte profesionálně vypadající poznámku bez manipulace s nízkoúrovňovými PDF proudy.

Odtud můžete zkoumat přidávání razítek na každou stránku, výměnu za obrázky nebo dokonce vrstvení několika razítek pro složité brandování. Stejný vzor – vytvořit, nakonfigurovat, připojit, uložit – platí pro většinu úkolů Aspose.Pdf, takže jej bude snadné rozšířit.

Máte jiný případ použití, například razítko „confidential“ na desítky PDF v dávkovém úkolu? Zkuste obalit výše uvedenou logiku do `foreach`, který prochází složku se soubory. Nebo pokud potřebujete **add note to pdf** podmíněně na základě obsahu stránky, podívejte se na Aspose `TextFragmentAbsorber` pro vyhledávání textu před razítkem.

Šťastné programování a ať jsou vaše PDF vždy razítkována přesně tak, jak potřebujete!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}