---
category: general
date: 2026-04-10
description: Voeg Bates‑nummering toe aan PDF’s met C# in enkele minuten. Leer hoe
  je aangepaste paginanummers toevoegt, hoe je PDF‑bestanden nummert en Bates‑nummering
  efficiënt toepast.
draft: false
keywords:
- add bates numbering
- add custom page numbers
- how to number pdf
- how to add bates
- apply bates numbering
language: nl
og_description: Voeg Bates‑nummering toe aan PDF’s met C# in enkele minuten. Deze
  gids laat zien hoe je aangepaste paginanummers toevoegt, hoe je PDF‑bestanden nummert
  en Bates‑nummering stap‑voor‑stap toepast.
og_title: Voeg Bates-nummering toe aan PDF's met C# – Complete gids
tags:
- PDF
- C#
- Bates numbering
title: Bates‑nummering toevoegen aan PDF’s met C# – Complete gids
url: /nl/net/programming-with-stamps-and-watermarks/add-bates-numbering-to-pdfs-with-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Add Bates Numbering to PDFs met C# – Complete Guide

Heb je ooit **add bates numbering** aan een PDF nodig gehad maar wist je niet waar te beginnen? Je bent niet alleen—juridische teams, auditors en iedereen die grote documentenverzamelingen verwerkt, stuiten hier regelmatig op. Het goede nieuws? Met een paar regels C# kun je automatisch elke pagina voorzien van een aangepaste identifier, en je leert ook **how to add custom page numbers**.

In deze tutorial lopen we alles door wat je nodig hebt: het vereiste NuGet‑pakket, het configureren van de nummeringsopties, het toepassen van de nummers en het verifiëren van het resultaat. Aan het einde weet je **how to number PDF** bestanden programmatically, en kun je de prefix, suffix, lettergrootte of zelfs specifieke pagina's aanpassen.

## Prerequisites

- .NET 6.0 of later (de code werkt ook met .NET Framework 4.7+)
- Visual Studio 2022 (of elke IDE die je verkiest)
- De **Aspose.PDF for .NET** bibliotheek (gratis proefversie werkt voor leren)
- Een voorbeeld‑PDF genaamd `source.pdf` geplaatst in een map die je beheert

Als je die punten hebt afgevinkt, laten we beginnen.

## Step 1: Install and Reference Aspose.PDF

First, add the Aspose.PDF package to your project:

```bash
dotnet add package Aspose.PDF
```

Or use the NuGet Package Manager UI. Once installed, include the namespace at the top of your file:

```csharp
using Aspose.Pdf;
```

> **Pro tip:** Houd je pakketten up‑to‑date; de nieuwste versie (vanaf april 2026) voegt verschillende prestatie‑verbeteringen toe voor grote documenten.

## Step 2: Open the Source PDF Document

Opening the file is straightforward. We’ll use a `using` block so the file handle is released automatically.

```csharp
// Step 2: Open the source PDF document
using (var sourceDocument = new Document("YOUR_DIRECTORY/source.pdf"))
{
    // The rest of the workflow lives inside this block.
}
```

The `Document` class represents the entire PDF, giving us access to pages, annotations, and, of course, Bates numbering.

## Step 3: Define Bates Numbering Settings

Now comes the heart of the matter—configuring **add bates numbering** options. You can control the start number, prefix, suffix, font size, margin, and even specify which pages receive a stamp.

```csharp
// Step 3: Define Bates numbering settings
var batesOptions = new BatesNumberingOptions
{
    StartNumber = 1,                 // First number in the sequence
    Prefix = "ABC-",                 // Text before the number
    Suffix = "-2024",                // Text after the number
    FontSize = 12,                   // Size of the numbering font
    Margin = 10,                     // Distance from the page edge (points)
    PageNumbers = new[] { 1, 2, 3 }  // Pages to which numbering is applied
};
```

### Why These Settings Matter

- **StartNumber** laat je een reeks voortzetten van een vorige batch.
- **Prefix/Suffix** zijn handig voor zaak‑identifiers of jaartal‑stempels.
- **FontSize** en **Margin** beïnvloeden de leesbaarheid; een te klein lettertype kan gemist worden bij afdrukken.
- **PageNumbers** is waar je **apply bates numbering** selectief toepast. Laat deze array weg om elke pagina te nummeren.

If you need to **add custom page numbers** that aren’t sequential, you can build a list like `{5, 10, 15}` and pass it here.

## Step 4: Apply the Bates Numbering to the Selected Pages

With the options prepared, the library does the heavy lifting. The method `AddBatesNumbering` injects the stamp onto each target page.

```csharp
// Step 4: Apply the Bates numbering to the selected pages
sourceDocument.AddBatesNumbering(batesOptions);
```

Behind the scenes, Aspose.PDF creates a text fragment for each page, positions it according to the margin, and respects the chosen font size. This ensures the numbers appear exactly where you expect, whether you view the PDF on screen or print it out.

## Step 5: Save the Modified Document

Finally, persist the changes to a new file so your original stays untouched.

```csharp
// Step 5: Save the modified document with Bates numbers
sourceDocument.Save("YOUR_DIRECTORY/bates.pdf");
```

You now have `bates.pdf` containing the stamped pages. Open it in any PDF viewer and you’ll see something like:

```
ABC-1-2024   (on page 1, top‑right)
ABC-2-2024   (on page 2, top‑right)
ABC-3-2024   (on page 3, top‑right)
```

### Verifying the Result

A quick sanity check is to programmatically read back the first page’s text:

```csharp
using (var doc = new Document("YOUR_DIRECTORY/bates.pdf"))
{
    var text = doc.Pages[1].ExtractText();
    Console.WriteLine(text.Contains("ABC-1-2024") ? "Bates number applied!" : "Oops, something went wrong.");
}
```

If the console prints *Bates number applied!*, you’re golden.

## Edge Cases & Common Variations

| Situation | What to Change | Reason |
|-----------|----------------|--------|
| **Number every page** | Omit `PageNumbers` or set it to `null` | The API defaults to all pages when the array isn’t supplied. |
| **Different margin per side** | Use `Margin = new MarginInfo { Top = 15, Right = 10 }` (requires Aspose > 23.3) | Gives you fine‑grained control over placement. |
| **Large documents (> 500 pages)** | Enable `batesOptions.StartNumber` at a higher value and consider `batesOptions.FontSize = 10` to avoid overlap | Keeps the stamp readable without crowding the page. |
| **Need a different font** | Set `batesOptions.Font = FontRepository.FindFont("Arial")` | Some legal firms require a specific typeface. |

> **Watch out:** Als je een paginanummer opgeeft dat niet bestaat (bijv. `PageNumbers = new[] { 999 }`), slaat Aspose.PDF dit stilletjes over. Valideer altijd het bereik als je de lijst dynamisch bouwt.

## Full Working Example

Below is the complete, ready‑to‑run program. Paste it into a console app, adjust the paths, and hit **F5**.

```csharp
using System;
using Aspose.Pdf;

class Program
{
    static void Main()
    {
        // Adjust these paths to match your environment
        string sourcePath = @"YOUR_DIRECTORY\source.pdf";
        string outputPath = @"YOUR_DIRECTORY\bates.pdf";

        // Open the source PDF
        using (var sourceDocument = new Document(sourcePath))
        {
            // Configure Bates numbering options
            var batesOptions = new BatesNumberingOptions
            {
                StartNumber = 1,
                Prefix = "ABC-",
                Suffix = "-2024",
                FontSize = 12,
                Margin = 10,
                PageNumbers = new[] { 1, 2, 3 } // Change or remove to number all pages
            };

            // Apply the numbering
            sourceDocument.AddBatesNumbering(batesOptions);

            // Save the new PDF
            sourceDocument.Save(outputPath);
        }

        // Verify the first page contains the expected stamp
        using (var doc = new Document(outputPath))
        {
            string extracted = doc.Pages[1].ExtractText();
            bool success = extracted.Contains("ABC-1-2024");
            Console.WriteLine(success
                ? "Bates numbering added successfully!"
                : "Numbering failed – check your options.");
        }
    }
}
```

Running this code will generate `bates.pdf` with the three stamped pages shown earlier. Open the file, and you’ll see the numbers right‑aligned, 10 points from the edge, in 12‑point font.

## Visual Preview

![add bates numbering preview](/images/bates-numbering-sample.png)

*De screenshot hierboven illustreert hoe de **add bates numbering** output eruitziet nadat het script is uitgevoerd.*

## Conclusion

We’ve just covered how to **add bates numbering** to a PDF using C#. By configuring `BatesNumberingOptions`, applying the stamp, and saving the document, you now have a repeatable solution that can also **add custom page numbers**, **how to number pdf** files, and **apply bates numbering** across any project. 

Next steps? Probeer dit te combineren met een batch‑processor die door een map met PDF’s loopt, of experimenteer met verschillende prefixes voor elk zaaktype. Je kunt ook onderzoeken hoe je meerdere PDF’s kunt samenvoegen na het nummeren—handig voor het bouwen van uitgebreide zaakbundels.

Got questions about edge cases, or want to see how to embed the numbers in the footer instead of the header? Drop a comment, and happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}