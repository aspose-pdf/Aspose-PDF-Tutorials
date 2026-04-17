---
category: general
date: 2026-03-27
description: Lär dig hur du ritar en rektangel i PDF med Aspose.Pdf för C#. Lägg till
  en rektangel i PDF, lägg till en form i PDF och rita formen i PDF med tydliga kodexempel.
draft: false
keywords:
- how to draw rectangle
- add rectangle to pdf
- add shape to pdf
- draw shape on pdf
- draw rectangle in pdf
language: sv
og_description: Lär dig att rita rektangel i PDF med Aspose.Pdf. Den här handledningen
  visar dig hur du lägger till en rektangel i PDF, lägger till en form i PDF och ritar
  en form i PDF steg för steg.
og_title: Hur man ritar en rektangel i PDF med C# – Komplett guide
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Hur man ritar en rektangel i PDF med C# – Steg‑för‑steg‑guide
url: /sv/net/images-graphics/how-to-draw-rectangle-in-pdf-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man ritar rektangel i PDF med C# – Steg‑för‑steg guide

Har du någonsin undrat **hur man ritar rektangel** i en PDF utan att kämpa med låg‑nivå PDF‑syntax? Du är inte ensam. Många utvecklare stöter på problem när de behöver visualisera en avgränsningsruta, ett markeringsområde eller ett enkelt dekorativt element i ett genererat dokument. Den goda nyheten? Med Aspose.Pdf för .NET är processen en barnlek.

I den här handledningen går vi igenom allt du behöver för att **lägga till rektangel i PDF**, **lägga till form i PDF**, och slutligen **rita rektangel i PDF** med ren, idiomatisk C#. I slutet har du ett körbart program som skapar en PDF‑fil som innehåller en skarp rektangel—utan externa verktyg.

## Förutsättningar

- .NET 6.0 eller senare (koden fungerar även med .NET Core och .NET Framework)
- Aspose.Pdf för .NET NuGet‑paket (`Install-Package Aspose.Pdf`)
- En grundläggande C#‑utvecklingsmiljö (Visual Studio, VS Code, Rider osv.)

Inga andra bibliotek behövs; allt annat hanteras av Aspose.Pdf själv.

## Steg 1: Ställ in projektet och importera namnrymder

Först, skapa en ny konsolapplikation och importera Aspose.Pdf‑namnrymden.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

namespace PdfRectangleDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll place the rest of the code here.
        }
    }
}
```

**Varför detta är viktigt:** Att importera `Aspose.Pdf.Drawing` ger dig tillgång till `Rectangle`‑formklassen som vi kommer att använda för att **rita form på PDF**. Att hålla startpunkten ren gör de senare stegen enklare att följa.

## Steg 2: Skapa ett nytt PDF‑dokument och en sida

En PDF utan sidor är meningslös, så vi börjar med att skapa ett dokumentobjekt och lägga till en enda sida.

```csharp
// Step 2: Initialize a new PDF document
Document pdfDoc = new Document();

// Add a blank page to the document (size defaults to A4)
Page page = pdfDoc.Pages.Add();
```

**Förklaring:** `Document`‑klassen representerar hela filen, medan `Pages.Add()` returnerar ett nytt `Page`‑objekt där vi senare kommer att **lägga till rektangel i PDF**. Standard A4‑storlek fungerar i de flesta fall, men du kan ange bredd/höjd om du behöver en anpassad canvas.

## Steg 3: Definiera rektangel‑formen

Nu kommer kärnan i **hur man ritar rektangel**—att definiera dess position och dimensioner.

```csharp
// Step 3: Define a rectangle shape (x, y, width, height)
// Coordinates are measured from the lower‑left corner of the page.
var rectangleShape = new Rectangle(100, 500, 300, 200)
{
    // Optional: set line color and fill color
    BorderColor = Color.Black,
    BorderWidth = 2,
    FillColor = Color.LightGray
};
```

**Varför vi sätter dessa egenskaper:**  
- `BorderColor` och `BorderWidth` styr konturen, vilket gör rektangeln synlig.  
- `FillColor` ger den en subtil bakgrund, användbart när du vill markera ett område.  
- Konstruktorn `(x, y, width, height)` låter dig **rita rektangel i PDF** exakt där du behöver den.

## Steg 4: Lägg till rektangeln på sidan

Med formen klar, **lägger vi nu till form i PDF** genom att fästa den i sidans `Annotations`‑samling. Aspose.Pdf validerar gränserna automatiskt, så du behöver inte oroa dig för överspill.

```csharp
// Step 4: Add the rectangle shape to the page
page.Annotations.Add(rectangleShape);
```

**Vad som händer under huven:** `Annotations`‑samlingen behandlar rektangeln som en vektorgrafik. När PDF:en renderas översätter biblioteket våra koordinater till PDF‑innehållsströmmen.

## Steg 5: Spara dokumentet

Till sist, skriv PDF‑filen till disk så att du kan öppna den i någon visare.

```csharp
// Step 5: Save the PDF file
string outputPath = "RectangleDemo.pdf";
pdfDoc.Save(outputPath);
Console.WriteLine($"PDF saved to {outputPath}");
```

**Resultat:** När du öppnar `RectangleDemo.pdf` visas en ljusgrå rektangel med en svart kant placerad 100 pt från vänster och 500 pt från botten av sidan. Det är den kompletta lösningen för **hur man ritar rektangel** i en PDF med C#.

## Fullt fungerande exempel

När alla bitar sätts ihop, här är det kompletta, körklara programmet:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using Aspose.Pdf.Color;

namespace PdfRectangleDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Initialize a new PDF document
            Document pdfDoc = new Document();

            // Add a blank page (A4 by default)
            Page page = pdfDoc.Pages.Add();

            // Define a rectangle shape (x, y, width, height)
            var rectangleShape = new Rectangle(100, 500, 300, 200)
            {
                BorderColor = Color.Black,
                BorderWidth = 2,
                FillColor = Color.LightGray
            };

            // Add the rectangle to the page
            page.Annotations.Add(rectangleShape);

            // Save the document
            string outputPath = "RectangleDemo.pdf";
            pdfDoc.Save(outputPath);
            Console.WriteLine($"PDF saved to {outputPath}");
        }
    }
}
```

**Förväntad output:** En fil med namnet `RectangleDemo.pdf` som innehåller en enda sida med en centrerad ljusgrå rektangel inramad i svart. Du kan öppna den med Adobe Reader, Chrome eller någon PDF‑visare.

## Vanliga variationer & kantfall

### 1. Rita flera rektanglar

Om du behöver **lägga till rektangel i PDF** mer än en gång, skapa helt enkelt ytterligare `Rectangle`‑objekt och lägg till varje i `page.Annotations`. Att loopa över en samling koordinater gör detta enkelt.

```csharp
foreach (var rectInfo in rectangles)
{
    var rect = new Rectangle(rectInfo.X, rectInfo.Y, rectInfo.Width, rectInfo.Height)
    {
        BorderColor = Color.Blue,
        BorderWidth = 1,
        FillColor = Color.Transparent
    };
    page.Annotations.Add(rect);
}
```

### 2. Använda olika enheter

Aspose.Pdf arbetar i punkter (1 pt = 1/72 tum). Om du föredrar millimeter, konvertera dem först:

```csharp
double mmToPt = 72.0 / 25.4;
float x = (float)(20 * mmToPt); // 20 mm from left
float y = (float)(150 * mmToPt);
```

### 3. Lägga till en rektangel som ett formulärfält

När du behöver en interaktiv rektangel (t.ex. ett klickbart område), använd en `LinkAnnotation` istället för en vanlig `Rectangle`. Koden är liknande men lägger till en URL‑ eller JavaScript‑åtgärd.

### 4. Kompatibilitetsfrågor

Aspose.Pdf version 23.9 (släppt tidigt 2026) stödjer fullt ut de API:er som visas ovan. Äldre versioner kan kräva `page.AddAnnotation(rectangleShape)` istället för `page.Annotations.Add`. Kontrollera alltid versionsnoterna om du stöter på kompileringsfel.

## Pro‑tips & fallgropar

- **Pro‑tips:** Sätt `FillColor = Color.Transparent` om du bara behöver en kontur. Detta minskar filstorleken något.
- **Se upp för:** Att använda koordinater som överskrider sidans dimensioner. Aspose.Pdf kommer tyst att klippa formen, vilket kan vara förvirrande vid felsökning.
- **Prestanda‑anmärkning:** Att lägga till tusentals rektanglar är okej, men om du genererar stora rapporter bör du överväga att batcha former i ett enda `Graphics`‑objekt för att minska overhead.

## Visuell referens

Nedan är en snabb skärmdump av den genererade PDF‑en (rektangeln är markerad i ljusgrått). Alt‑texten innehåller huvudnyckelordet för SEO.

![how to draw rectangle in PDF example](https://example.com/images/rectangle-demo.png "how to draw rectangle in PDF example")

## Slutsats

Vi har gått igenom **hur man ritar rektangel** i en PDF med Aspose.Pdf för C#. Genom att skapa ett `Document`, lägga till en `Page`, definiera en `Rectangle`‑form och slutligen **lägga till form i PDF**, kan du generera vektorbaserad grafik med bara några få rader. Oavsett om du behöver **lägga till rektangel i pdf** för markering, layout‑debugging eller UI‑överlägg, skalar metoden bra.

Därefter kan du utforska **draw shape on pdf** bortom rektanglar—tänk cirklar, polylinjer eller till och med anpassade SVG‑vägar. Eller fördjupa dig i textrendering, bildinfogning och PDF‑formulärshantering för att bygga fullständiga rapporter. Aspose.Pdf‑biblioteket erbjuder ett rikt API, och med grunderna täckta här är du redo att experimentera.

Lycka till med kodandet, och må dina PDF‑filer alltid se exakt ut som du föreställer dig!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}