---
category: general
date: 2026-03-24
description: Hur man lägger till en stämpel i en PDF med Aspose.Pdf i C#. Lär dig
  att placera en stämpel i PDF och lägga till en textstämpel i PDF med automatisk
  storleksanpassning i några enkla steg.
draft: false
keywords:
- how to add stamp
- place stamp pdf
- add text stamp pdf
- Aspose.Pdf stamp example
- C# PDF annotation
language: sv
og_description: Hur lägger man till en stämpel i en PDF i C#? Denna guide visar hur
  du placerar en stämpel i PDF och lägger till en textstämpel i PDF med automatisk
  teckenstorlek med hjälp av Aspose.Pdf.
og_title: Hur man lägger till en stämpel i PDF med Aspose.Pdf – Snabbguide
tags:
- pdf
- csharp
- aspose
- stamping
title: Hur man lägger till en stämpel i PDF med Aspose.Pdf – Steg‑för‑steg‑guide
url: /sv/net/programming-with-stamps-and-watermarks/how-to-add-stamp-to-pdf-with-aspose-pdf-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man lägger till stämpel i PDF med Aspose.Pdf – Steg‑för‑steg‑guide

**How to add stamp** till en PDF är ett vanligt behov när du vill märka, certifiera eller helt enkelt kommentera ett dokument. Har du någonsin funderat på det enklaste sättet att placera en stamp PDF utan att kämpa med låg‑nivå grafik? I den här handledningen går vi igenom en komplett, färdig‑att‑köra lösning som inte bara visar **how to add stamp** utan också förklarar *varför* varje rad är viktig.

Du kommer att lära dig hur du **place stamp PDF** på vilken sida som helst, hur du **add text stamp PDF** som automatiskt krymper för att passa sin rektangel, och vilka fallgropar du bör undvika när texten är för lång. I slutet har du en enda C#‑fil som du kan lägga till i ditt projekt och börja stämpla PDF‑filer omedelbart.

## Förutsättningar

* .NET 6.0 eller senare (koden fungerar även med .NET Core och .NET Framework).
* Aspose.Pdf for .NET NuGet‑paketet (`Aspose.Pdf`) installerat.
* En PDF‑fil med namnet `input.pdf` i en mapp du kan referera till (valfri enkel en‑sidig PDF fungerar).

Ingen extra konfiguration krävs—Aspose.Pdf sköter allt tungt arbete.

## Steg 1: Ställ in projektet och läs in käll‑PDF‑filen

Det första vi behöver är ett `Document`‑objekt som representerar den PDF vi vill kommentera. Tänk på det som att ladda en tom duk som vi senare kommer att måla en stämpel på.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Load the source PDF document
// The using statement ensures the file is closed automatically.
using var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");
```

> **Varför detta är viktigt:** `Document` är ingångspunkten för all PDF‑manipulation i Aspose.Pdf. Genom att använda `using`‑mönstret garanterar vi att filhandtaget släpps, vilket förhindrar lås‑problem när du senare försöker spara den modifierade PDF‑filen.

## Steg 2: Skapa en TextStamp med automatiskt anpassande teckenstorlek

Nu bygger vi en `TextStamp`. Tricket som får detta exempel att sticka ut är flaggan `AutoAdjustFontSizeToFitStampRectangle`—den säger åt Aspose att krympa texten tills den får plats i den rektangel vi definierar.

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

> **Proffstips:** Om du behöver en logotyp eller en bild istället för text, använd `ImageStamp`—samma auto‑justeringslogik finns för bildskalning.

## Steg 3: Välj var du **Place Stamp PDF** – Första sidan, sista sidan eller anpassat index

Aspose.Pdf lagrar sidor i en 1‑baserad samling (`pdfDocument.Pages[1]` är den första sidan). Du kan **place stamp PDF** på vilken sida som helst genom att ändra indexet.

```csharp
// Place the stamp on the first page (index 1)
// To stamp the last page use pdfDocument.Pages[pdfDocument.Pages.Count]
pdfDocument.Pages[1].AddStamp(textStamp);
```

> **Varför detta är flexibelt:** Eftersom `Pages`‑samlingen är muterbar kan du loopa igenom alla sidor och lägga till samma stämpel på varenda, eller så kan du rikta in dig på en specifik sida baserat på affärslogik (t.ex. endast framsidan).

## Steg 4: Spara det modifierade dokumentet

Efter stämpling måste du skriva tillbaka ändringarna till disk. Du kan skriva över originalfilen eller skapa en ny—det är upp till dig.

```csharp
// Save the stamped PDF – change the path if you don’t want to overwrite
pdfDocument.Save("YOUR_DIRECTORY/output-stamped.pdf");
```

När du öppnar `output-stamped.pdf` ser du en ljusgrå rektangel på den första sidan som innehåller texten “Long text that must fit”. Om texten var längre skulle Aspose automatiskt krympa den tills den passar perfekt i rektangeln 300 × 100 pt.

## Fullt fungerande exempel

Nedan är det kompletta programmet som du kan kopiera‑och‑klistra in i en konsolapp (`Program.cs`). Det inkluderar alla delar vi diskuterade, plus en liten hjälpfunktion för att verifiera att stämpeln visas.

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

### Förväntat resultat

* PDF‑filen öppnas med en halvtransparent grå ruta på den första sidan.
* Inuti rutan passar den medföljande texten perfekt, även om du ersätter den med en längre mening.
* Inga manuella beräkningar av teckenstorlek krävs—Aspose sköter det tunga arbetet.

## Vanliga fallgropar när du **Place Stamp PDF**

| Symptom | Trolig orsak | Åtgärd |
|---------|--------------|-----|
| Texten kapas av | `AutoAdjustFontSizeToFitStampRectangle` är **false** eller rektangeln är för liten. | Aktivera flaggan och öka `Width`/`Height` eller minska textlängden. |
| Stämpeln visas off‑center | Standardvärdena för `HorizontalAlignment`/`VerticalAlignment` är `Left`/`Top`. | Sätt `HorizontalAlignment = HorizontalAlignment.Center` och `VerticalAlignment = VerticalAlignment.Center`. |
| Stämpeln syns inte i vissa visare | Bakgrundens opacitet är satt till 0 eller stämpelfärgen matchar sidans bakgrund. | Använd en kontrasterande `Background.Color` eller sätt `Opacity` > 0.3. |
| Flera stämplar överlappar | Lägger till stämplar i en loop utan att justera koordinater. | Använd `textStamp.XIndent` och `textStamp.YIndent` för att förskjuta varje stämpel. |

Att åtgärda dessa problem tidigt sparar dig från mycket felsökning senare.

## Utöka exemplet: Lägga till en bildstämpel

Om du behöver **add text stamp PDF** *och* en bild (t.ex. en företagslogotyp), kan du kombinera båda:

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

Nu visar sidan både en dynamisk textstämpel och en statisk bildstämpel sida vid sida.

## Testa din implementation

1. Kör konsolappen.
2. Öppna `output-stamped.pdf` i Adobe Reader, Edge eller någon PDF‑visare.
3. Verifiera att stämpelrektangeln finns och att texten är helt synlig.
4. Ändra texten till en längre fras, kör igen, och bekräfta att teckensnittet krymper automatiskt.

Om något ser fel ut, dubbelkolla rektangelns dimensioner och inställningen `AutoAdjustFontSizePrecision`.

## Slutsats

Du vet nu **how to add stamp** till en PDF med Aspose.Pdf, hur du **place stamp PDF** på en specifik sida, och hur du **add text stamp PDF** som automatiskt justerar sin teckenstorlek. Det kompletta, körbara exemplet ovan eliminerar gissningar och ger dig en solid grund för mer avancerade stämplingsscenarier—som batch‑bearbetning av dussintals filer eller att lägga till vattenstämplar villkorligt.

Redo för nästa steg? Prova att stämpla varje sida i en loop, experimentera med olika typsnitt, eller kombinera bild‑ och textstämplar för att skapa en professionell seal. Himlen är gränsen, och med Aspose.Pdf har du en pålitlig motor under huven.

Om du stöter på problem, lämna en kommentar eller kolla Aspose.Pdf‑dokumentationen för djupare anpassningsalternativ. Lycka till med stämplingen!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}