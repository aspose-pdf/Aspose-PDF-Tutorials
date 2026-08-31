---
category: general
date: 2026-02-12
description: Rychle přidejte Batesova čísla do PDF souborů. Naučte se, jak přidat
  textové pole do PDF, přidat formulářové pole do PDF a přidat číslování stránek do
  PDF pomocí Aspose.PDF.
draft: false
keywords:
- add bates numbers
- add text field pdf
- add form field pdf
- add page numbers pdf
- how to add bates
language: cs
og_description: Přidejte Batesova čísla do PDF dokumentů v C#. Tento průvodce ukazuje,
  jak přidat textové pole do PDF, formulářové pole do PDF a číslování stránek do PDF
  pomocí Aspose.PDF.
og_title: Přidejte Batesova čísla do PDF souborů – Kompletní C# tutoriál
tags:
- PDF
- C#
- Aspose.PDF
title: Přidání Batesových čísel do PDF – krok za krokem průvodce v C#
url: /cs/net/programming-with-forms/add-bates-numbers-to-pdfs-step-by-step-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Přidání Batesových čísel do PDF – Kompletní průvodce v C#  

Už jste někdy potřebovali **add bates numbers** do hromady právních PDF, ale nebyli jste si jisti, kde začít? Nejste v tom sami. V mnoha advokátních kancelářích a e‑discovery projektech je označování každé stránky unikátním identifikátorem každodenní prací a provádět to ručně je noční můra.  

Dobrá zpráva? S několika řádky C# a Aspose.PDF můžete celý proces automatizovat. V tomto tutoriálu vás provedeme **how to add bates** numbers, nasypeme textové pole na každou stránku a uložíme čisté, prohledávatelné PDF — bez potu.

> **Co získáte:** plně spustitelný ukázkový kód, vysvětlení, proč je každý řádek důležitý, tipy pro okrajové případy a rychlý kontrolní seznam pro ověření výstupu.  

Také se dotkneme souvisejících úkolů, jako jsou **add text field pdf**, **add form field pdf** a **add page numbers pdf**, abyste měli připravenou sadu nástrojů pro jakoukoli výzvu v automatizaci dokumentů.

---

## Předpoklady

- .NET 6.0 nebo novější (kód funguje také s .NET Framework 4.6+)  
- Visual Studio 2022 (nebo jakékoli IDE, které preferujete)  
- Platná licence Aspose.PDF pro .NET (bezplatná zkušební verze funguje pro testování)  
- Zdrojové PDF pojmenované `source.pdf` umístěné ve složce, na kterou můžete odkazovat  

Pokud vám některý z těchto bodů není znám, pozastavte se a nainstalujte chybějící součást, než budete pokračovat. Níže uvedené kroky předpokládají, že jste již přidali NuGet balíček Aspose.PDF:

```bash
dotnet add package Aspose.Pdf
```

---

## Jak přidat bates numbers do PDF pomocí Aspose.PDF

Níže je kompletní program připravený ke zkopírování a vložení. Načte PDF, vytvoří **text box field** na každé stránce, zapíše formátované Bates číslo a nakonec uloží upravený soubor.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Forms;

class Program
{
    static void Main()
    {
        // 👉 Step 1: Load the source PDF document
        using (var pdfDocument = new Document(@"YOUR_DIRECTORY\source.pdf"))
        {
            // 👉 Step 2: Add a Bates number text field to each page
            for (int pageNumber = 1; pageNumber <= pdfDocument.Pages.Count; pageNumber++)
            {
                // Define the rectangle where the field will appear (10,10) = lower‑left corner
                var fieldRect = new Rectangle(10, 10, 150, 30);

                // Create the TextBoxField – this is the “add text field pdf” part
                var batesField = new TextBoxField(pdfDocument.Pages[pageNumber], fieldRect)
                {
                    // Format the number: BATES-00001, BATES-00002, …
                    Value = $"BATES-{pageNumber:D5}"
                };

                // Register the field with the form collection – “add form field pdf”
                pdfDocument.Form.Add(batesField, $"Bates_{pageNumber}", pageNumber);
            }

            // 👉 Step 3: Save the modified PDF with Bates numbers
            pdfDocument.Save(@"YOUR_DIRECTORY\bates.pdf");
        }

        Console.WriteLine("✅ Bates numbers added successfully!");
    }
}
```

### Proč to funguje

- **`Document`** je vstupní bod; představuje celý PDF soubor.  
- **`Rectangle`** určuje, kde pole na stránce leží. Čísla jsou v bodech (1 pt ≈ 1/72 in). Pokud potřebujete číslo v jiném rohu, upravte souřadnice.  
- **`TextBoxField`** je *form field*, který může obsahovat libovolný řetězec. Přiřazením `Value` efektivně **add page numbers pdf** s vlastním prefixem.  
- **`pdfDocument.Form.Add`** zaregistruje pole do AcroForm PDF, což ho činí viditelným v prohlížečích jako Adobe Acrobat.  

Pokud budete někdy potřebovat změnit vzhled (písmo, barvu, velikost), můžete upravit vlastnosti `TextBoxField` — podívejte se do dokumentace Aspose na `DefaultAppearance` a `Border`.

## Přidání textového pole na každou stránku PDF (krok „add text field pdf“)

Někdy chcete jen viditelný popisek, ne interaktivní formulářové pole. V takovém případě můžete nahradit `TextBoxField` za `TextFragment` a přidat jej přímo do kolekce `Paragraphs` stránky. Zde je rychlá alternativa:

```csharp
var fragment = new TextFragment($"BATES-{pageNumber:D5}")
{
    // Position the text using a TextState (font, size, color)
    TextState = new TextState
    {
        Font = FontRepository.FindFont("Arial"),
        FontSize = 12,
        ForegroundColor = Color.Black
    }
};

// Set the fragment’s rectangle (same coordinates as before)
fragment.Position = new Position(10, 10);
pdfDocument.Pages[pageNumber].Paragraphs.Add(fragment);
```

Přístup **add text field pdf** je užitečný, když bude finální dokument pouze ke čtení, zatímco metoda **add form field pdf** ponechává čísla později editovatelná.

## Uložení PDF s Bates numbers (moment „add page numbers pdf“)

Po dokončení smyčky volání `pdfDocument.Save` zapíše vše na disk. Pokud potřebujete zachovat původní soubor, stačí změnit výstupní cestu nebo použít přetížení `pdfDocument.Save` k přímému streamování výsledku do odpovědi ve webovém API.

```csharp
// Example: stream to HTTP response (ASP.NET Core)
Response.ContentType = "application/pdf";
pdfDocument.Save(Response.Body);
```

To je ta šikovná část — žádné dočasné soubory, žádné další knihovny, jen Aspose, který se postará o těžkou práci.

## Očekávaný výsledek a rychlé ověření

Otevřete `bates.pdf` v libovolném PDF prohlížeči. Měli byste vidět malé pole v levém dolním rohu každé stránky s textem:

```
BATES-00001
BATES-00002
…
```

Pokud prozkoumáte vlastnosti dokumentu, všimnete si AcroForm obsahující pole pojmenovaná `Bates_1`, `Bates_2` atd. To potvrzuje úspěšnost kroku **add form field pdf**.

## Časté problémy a profesionální tipy

| Problém | Proč se to děje | Oprava |
|-------|----------------|-----|
| Čísla jsou mimo střed | Souřadnice Rectangle jsou relativní k levému dolnímu rohu stránky. | Otočte Y‑hodnotu (`pageHeight - marginTop`) nebo použijte `page.PageInfo.Height` k výpočtu umístění s horním okrajem. |
| Pole jsou neviditelná v Adobe Reader | Výchozí okraj je nastaven na „No“. | Nastavte `batesField.Border = new Border { Width = 0.5f, Color = Color.Black };` |
| Velká PDF způsobují tlak na paměť | `using` uvolní dokument až po dokončení smyčky. | Zpracovávejte stránky po částech nebo použijte `pdfDocument.Save` s `SaveOptions`, které umožňují streamování. |
| Licence není použita | Aspose na první stránce vytiskne vodoznak. | Zaregistrujte licenci brzy: `License lic = new License(); lic.SetLicense("Aspose.Pdf.lic");` |

## Rozšíření řešení

- **Vlastní prefixy:** Nahraďte `"BATES-"` libovolným řetězcem (`"DOC-"`, `"CASE-"`, …).  
- **Délka nulového doplnění:** Změňte `{pageNumber:D5}` na `{pageNumber:D3}` pro tři číslice.  
- **Dynamické umístění:** Použijte `pdfDocument.Pages[pageNumber].PageInfo.Width` k umístění pole na pravé straně.  
- **Podmíněné číslování:** Přeskočte prázdné stránky kontrolou `pdfDocument.Pages[pageNumber].IsBlank`.  

Všechny tyto varianty zachovávají základní vzor **add bates numbers**, **add text field pdf** a **add form field pdf** beze změny.

## Kompletní funkční příklad (vše v jednom)

Níže je finální program připravený ke spuštění, který zahrnuje výše uvedené tipy. Zkopírujte jej do nové konzolové aplikace a stiskněte F5.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Forms;
using Aspose.Pdf.Text;
using Aspose.Pdf.Drawing;

class AddBatesNumbers
{
    static void Main()
    {
        // Register your license here (optional for trial)
        // var license = new License();
        // license.SetLicense("Aspose.Pdf.lic");

        string inputPath = @"YOUR_DIRECTORY\source.pdf";
        string outputPath = @"YOUR_DIRECTORY\bates.pdf";

        using (var pdfDocument = new Document(inputPath))
        {
            int totalPages = pdfDocument.Pages.Count;

            for (int i = 1; i <= totalPages; i++)
            {
                // Position the field 10 pts from left and 10 pts from bottom
                var rect = new Rectangle(10, 10, 150, 30);

                var batesField = new TextBoxField(pdfDocument.Pages[i], rect)
                {
                    Value = $"BATES-{i:D5}"
                };

                // Optional: make the field look nicer
                batesField.Border = new Border
                {
                    Width = 0.5f,
                    Color = Color.Gray
                };
                batesField.DefaultAppearance = new DefaultAppearance
                {
                    Font = FontRepository.FindFont("Arial"),
                    FontSize = 10,
                    ForegroundColor = Color.DarkBlue
                };

                pdfDocument.Form.Add(batesField, $"Bates_{i}", i);
            }

            pdfDocument.Save(outputPath);
        }

        Console.WriteLine($"✅ Finished! Bates numbers saved to: {outputPath}");
    }
}
```

Spusťte jej, otevřete výsledek a uvidíte profesionálně vypadající identifikátor na každé stránce — přesně to, co by očekával specialista na podporu soudních řízení.

## Závěr

Právě jsme ukázali **how to add bates numbers** do libovolného PDF pomocí C# a Aspose.PDF. Vytvořením **text box field** na každé stránce současně **add text field pdf**, **add form field pdf** a **add page numbers pdf** v jednom průchodu. Přístup je rychlý, škálovatelný a snadno upravitelný pro vlastní prefixy, různé rozvržení nebo podmíněnou logiku.

Jste připraveni na další výzvu? Zkuste vložit QR kód, který odkazuje na originální spis, nebo vygenerujte samostatnou indexovou stránku, která vypíše všechna Bates čísla s odpovídajícími názvy stránek. Stejná API vám umožní sloučit PDF, extrahovat stránky a dokonce zakrýt citlivá data — možnosti jsou neomezené.

Pokud narazíte na problém, zanechte komentář níže nebo si prostudujte oficiální dokumentaci Aspose pro podrobnější informace. Šťastné programování a ať jsou vaše PDF vždy perfektně očíslovaná!  

---  

![add bates numbers screenshot](https://example.com/images/add-bates-numbers.png "add bates numbers example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}