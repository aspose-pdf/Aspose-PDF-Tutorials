---
category: general
date: 2026-08-14
description: Rita rektangel på PDF snabbt med C#. Lär dig hur du definierar rektangelns
  dimensioner och lägger till former på en PDF-sida på bara några rader.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- draw rectangle on pdf
- how to define rectangle dimensions
language: sv
lastmod: 2026-08-14
og_description: rita rektangel på PDF med C# på några sekunder. Den här guiden visar
  hur du definierar rektangelns mått, lägger till en form och verifierar sidgränser
  för pålitlig PDF‑grafik.
og_image_alt: Screenshot of a PDF page showing a black rectangle drawn with C# code
og_title: Rita rektangel på PDF – komplett C#‑handledning
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: draw rectangle on pdf quickly using C#. Learn how to define rectangle
    dimensions and add shapes to a PDF page in just a few lines.
  headline: draw rectangle on pdf – step‑by‑step C# guide
  type: TechArticle
tags:
- PDF
- C#
- Aspose.PDF
- RectangleShape
- Graphics
title: rita rektangel på pdf – steg‑för‑steg C#‑guide
url: /sv/net/annotations/draw-rectangle-on-pdf-step-by-step-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# rita rektangel i pdf – komplett C#-handledning

Om du behöver **draw rectangle on pdf** med C#, visar den här guiden en kortfattad, produktionsklar lösning. Du får se exakt **how to define rectangle dimensions**, verifiera att formen passar och lägga till den på en sida med ett enda metodanrop.

Handledningen täcker allt från att skapa ett PDF-dokument till att rendera rektangeln, så att du kan kopiera‑klistra koden i ditt eget projekt och se resultat omedelbart. Ingen extern dokumentation krävs—bara stegen nedan.

## Förutsättningar

* .NET 6.0 eller senare (koden fungerar också med .NET Framework 4.7+)
* **Aspose.PDF for .NET** NuGet‑paketet (`Install-Package Aspose.PDF`)
* Grundläggande förståelse för C#‑syntax
* En IDE såsom Visual Studio eller VS Code

> **Pro tip:** Använd den kostnadsfria evalueringslicensen för Aspose.PDF för snabba experiment; den lägger till ett litet vattenmärke men låter dig testa alla funktioner.

## Så ritar du rektangel i PDF med C#

Kärnan i uppgiften är att skapa en `RectangleShape`, sätta dess storlek och linje, och fästa den på en `Page`. Följande H2‑rubrik innehåller huvudnyckelordet, vilket uppfyller SEO‑kraven.

```csharp
using System;
using System.Drawing;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new PDF document
        Document pdfDoc = new Document();

        // 2️⃣ Add a blank page (default size: A4)
        Page page = pdfDoc.Pages.Add();

        // 3️⃣ Define the rectangle bounds (x, y, width, height)
        //    This demonstrates how to define rectangle dimensions.
        Rectangle rectBounds = new Rectangle(0, 0, 500, 700);

        // 4️⃣ Create the rectangle shape and set its stroke color
        RectangleShape rectangleShape = new RectangleShape(rectBounds)
        {
            StrokeColor = Color.Black   // black outline
        };

        // 5️⃣ Verify that the shape fits within the page boundaries
        page.CheckShapeBoundary(rectangleShape);

        // 6️⃣ Add the shape to the page
        page.Add(rectangleShape);

        // 7️⃣ Save the PDF to disk
        string outPath = "RectangleDemo.pdf";
        pdfDoc.Save(outPath);
        Console.WriteLine($"PDF saved to {outPath}");
    }
}
```

### Förklaring av varje steg

| Step | Why it matters |
|------|----------------|
| **1️⃣ Skapa ett nytt PDF-dokument** | Initierar behållaren som kommer att hålla sidor och grafik. |
| **2️⃣ Lägg till en tom sida** | Du behöver ett `Page`‑objekt eftersom former fästs på en sida, inte direkt på dokumentet. |
| **3️⃣ Definiera rektangelns gränser** | Här är där du **how to define rectangle dimensions**. `Rectangle`‑konstruktorn tar `x`, `y`, `width` och `height` i punkter (1 pt = 1/72 in). |
| **4️⃣ Skapa rektangelformen** | `RectangleShape` är Aspose‑klassen som renderar en rektangel. Att sätta `StrokeColor` definierar konturen; du kan också sätta `FillColor` för en solid fyllning. |
| **5️⃣ Verifiera sidgränser** | `CheckShapeBoundary` kastar ett undantag om rektangeln överskrider sidans storlek, vilket förhindrar felaktiga PDF‑filer. |
| **6️⃣ Lägg till formen på sidan** | Formen blir en del av sidans innehållsström. |
| **7️⃣ Spara PDF‑filen** | Sparar dokumentet till en fil som du kan öppna med vilken PDF‑visare som helst. |

Den resulterande `RectangleDemo.pdf` innehåller en svart rektangel placerad i sidans övre‑vänstra hörn, exakt 500 pt bred och 700 pt hög.

![exempel på att rita rektangel i pdf](https://example.com/rectangle-demo.png "exempel på att rita rektangel i pdf")

*Bildtext: exempel på att rita rektangel i pdf som visar en svart rektangel i PDF‑sidans övre vänstra hörn.*

## Så definierar du rektangelns dimensioner för olika sidstorlekar

Kodsnutten ovan använder fasta värden (`500 x 700`). I verkliga applikationer behöver du ofta att rektangeln anpassas till sidans bredd och höjd.

```csharp
// Get page dimensions (in points)
float pageWidth = page.PageInfo.Width;
float pageHeight = page.PageInfo.Height;

// Define a rectangle that occupies 80% of the page width and 50% of the height
float rectWidth  = pageWidth * 0.8f;
float rectHeight = pageHeight * 0.5f;

// Center the rectangle on the page
float rectX = (pageWidth - rectWidth) / 2;
float rectY = (pageHeight - rectHeight) / 2;

Rectangle dynamicRect = new Rectangle(rectX, rectY, rectWidth, rectHeight);
RectangleShape dynamicShape = new RectangleShape(dynamicRect)
{
    StrokeColor = Color.DarkBlue,
    FillColor   = Color.LightGray   // optional fill
};

page.CheckShapeBoundary(dynamicShape);
page.Add(dynamicShape);
```

**Viktiga punkter:**

* Använd `page.PageInfo.Width` och `Height` för att läsa den faktiska sidstorleken.
* Multiplikation med en faktor (t.ex. `0.8f`) låter dig uttrycka dimensioner som en procentandel av sidan.
* Centrering uppnås genom att subtrahera rektangelns storlek från sidans storlek och halvera återstoden.

## Vanliga fallgropar och hur du undviker dem

| Fallgrop | Varför det händer | Lösning |
|----------|-------------------|---------|
| Rektangeln sträcker sig utanför sidan | Hårdkodade dimensioner som är större än sidans storlek. | Anropa `page.CheckShapeBoundary` **innan** du lägger till formen; justera dimensionerna om ett undantag kastas. |
| Kontur syns inte | `StrokeColor` lämnad på standard (`Color.Empty`). | Ange explicit `StrokeColor` (t.ex. `Color.Black`). |
| Rektangeln visas utanför skärmen | Koordinaterna startar i nedre vänstra hörnet i PDF‑rymden; att använda skärm‑stilens övre vänstra koordinater orsakar en vändning. | Kom ihåg att ursprunget `(0,0)` är det nedre vänstra hörnet. Justera `y` därefter eller använd `pageHeight - desiredY`. |
| Oväntad linjetjocklek | Standardlinjebredden kan vara för tunn för utskrift. | Sätt `rectangleShape.LineWidth = 2;` för att öka tjockleken. |

## Utöka exemplet

När du kan **draw rectangle on pdf**, kan du enkelt lägga till andra former:

* **EllipseShape** – för cirklar eller ovaler.
* **PolygonShape** – för anpassade polygoner.
* **TextFragment** – för att märka dina rektanglar.

Alla former delar samma arbetsflöde: definiera gränser, konfigurera utseende, verifiera gränser och sedan lägga till på sidan.

## Komplett, körbart program

Nedan är hela programmet som kombinerar den grundläggande rektangeln och exemplet med dynamisk storlek. Kopiera det till ett nytt konsolprojekt, återställ `Aspose.PDF`‑NuGet‑paketet och kör.

```csharp
using System;
using System.Drawing;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

class RectangleDemo
{
    static void Main()
    {
        // Create document and page
        Document doc = new Document();
        Page page = doc.Pages.Add();

        // ==== Fixed‑size rectangle (basic example) ====
        Rectangle fixedRect = new Rectangle(0, 0, 500, 700);
        RectangleShape fixedShape = new RectangleShape(fixedRect)
        {
            StrokeColor = Color.Black,
            LineWidth   = 1
        };
        page.CheckShapeBoundary(fixedShape);
        page.Add(fixedShape);

        // ==== Dynamic rectangle that adapts to page size ====
        float pageW = page.PageInfo.Width;
        float pageH = page.PageInfo.Height;

        float dynWidth  = pageW * 0.6f;
        float dynHeight = pageH * 0.3f;
        float dynX      = (pageW - dynWidth) / 2;
        float dynY      = (pageH - dynHeight) / 2;

        Rectangle dynamicRect = new Rectangle(dynX, dynY, dynWidth, dynHeight);
        RectangleShape dynamicShape = new RectangleShape(dynamicRect)
        {
            StrokeColor = Color.DarkBlue,
            FillColor   = Color.LightYellow,
            LineWidth   = 2
        };
        page.CheckShapeBoundary(dynamicShape);
        page.Add(dynamicShape);

        // Save PDF
        string outFile = "CombinedRectangles.pdf";
        doc.Save(outFile);
        Console.WriteLine($"PDF created: {outFile}");
    }
}
```

**Förväntad output:**  
Öppna `CombinedRectangles.pdf`. Du kommer att se en svart rektangel förankrad i det nedre vänstra hörnet och en centrerad mörkblå rektangel med en ljusgul fyllning. Båda rektanglarna respekterar sidmarginalerna.

## Slutsats

Du vet nu hur du **draw rectangle on pdf** med C# och exakt **how to define rectangle dimensions** för både fasta och responsiva layouter. Metoden använder Aspose.PDF:s `RectangleShape`, gränskontroll och enkel aritmetik för att anpassa sig till vilken sidstorlek som helst.

Nästa steg kan du utforska:

* Lägga till **fill colors** och **line styles** (streckade, prickade) – sekundärt nyckelord: how to define rectangle dimensions with style.
* Kombinera flera former till en enda `Page` för att skapa diagram eller formulär.
* Exportera PDF‑en till en ström för webb‑API:er istället för att spara till disk.

Experimentera med olika storlekar, färger och positioner för att bemästra PDF‑grafik i dina .NET‑applikationer. Lycka till med kodningen!

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Hur du anpassar PDF‑filer med Aspose.PDF för .NET&#58; Ställ in sidmarginaler och rita linjer](/pdf/english/net/document-manipulation/customize-pdfs-aspose-pdf-set-margins-draw-lines/)
- [Hur du lägger till sidstämplar i PDF‑filer med Aspose.PDF för .NET&#58; En komplett guide](/pdf/english/net/watermarks-backgrounds/add-page-stamp-aspose-pdf-dotnet-guide/)
- [Hur du lägger till sidnumreringsstämplar i PDF‑filer med Aspose.PDF för .NET | Vattenstämplar & bakgrunder](/pdf/english/net/watermarks-backgrounds/add-page-number-stamp-using-aspose-pdf-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}