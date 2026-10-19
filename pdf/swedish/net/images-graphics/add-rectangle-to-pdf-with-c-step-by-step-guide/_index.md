---
category: general
date: 2026-08-04
description: Lägg till rektangel i PDF med C#. Lär dig hur du ritar en form i PDF
  med C# och Aspose.Pdf i ett tydligt, komplett exempel.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add rectangle to pdf
- how to draw shape in pdf c#
language: sv
lastmod: 2026-08-04
og_description: Lägg till rektangel i PDF med C#. Den här handledningen visar hur
  du snabbt och pålitligt ritar former i PDF med C#.
og_image_alt: Screenshot of a PDF page with a blue rectangle drawn by C# code
og_title: Lägg till rektangel i PDF med C# – komplett programmeringsguide
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Add rectangle to PDF using C#. Learn how to draw shape in PDF C# with
    Aspose.Pdf in a clear, complete example.
  headline: Add rectangle to PDF with C# – step‑by‑step guide
  type: TechArticle
- description: Add rectangle to PDF using C#. Learn how to draw shape in PDF C# with
    Aspose.Pdf in a clear, complete example.
  name: Add rectangle to PDF with C# – step‑by‑step guide
  steps:
  - name: '**Create a new console project**'
    text: '**Create a new console project**'
  - name: '**Add the Aspose.Pdf package**'
    text: '**Add the Aspose.Pdf package**'
  - name: '**Place `input.pdf`** in the project directory (or any folder you reference
      later).'
    text: '**Place `input.pdf`** in the project directory (or any folder you reference
      later).'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Lägg till rektangel i PDF med C# – steg‑för‑steg‑guide
url: /sv/net/images-graphics/add-rectangle-to-pdf-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Lägg till rektangel i PDF med C# – steg‑för‑steg guide

Om du behöver **lägga till rektangel i PDF**‑filer från en C#‑applikation visar den här guiden exakt hur du gör det. Du får se ett komplett, körbart exempel som ritar en form i PDF C# med hjälp av Aspose.Pdf‑biblioteket, och du kommer att förstå varför varje kodrad är viktig.

Att rita former i PDF‑filer är ett vanligt krav för rapportgeneratorer, fakturamallar och anpassad dokumentbranding. I slutet av den här handledningen kan du infoga vilken rektangulär annotation som helst, ändra dess storlek, färg eller position, och spara det modifierade dokumentet utan att förlora befintligt innehåll.

**Vad du kommer att lära dig**

* Hur du laddar en befintlig PDF med Aspose.Pdf.
* Hur du definierar rektangelns gränser och skapar en rektangel‑form.
* Hur du lägger till rektangeln i en sidas paragraf‑samling.
* Hur du sparar den uppdaterade PDF‑filen och verifierar resultatet.
* Variationer för flera sidor, transparens och anpassade linjestilar.

**Förutsättningar**

* .NET 6.0 eller senare (koden fungerar också med .NET Framework 4.7+).
* Visual Studio 2022 eller någon annan C#‑IDE.
* Ett NuGet‑referens till `Aspose.Pdf` (gratis provversion eller licensierad version).
* En inmatnings‑PDF‑fil med namnet `input.pdf` placerad i en mapp du kontrollerar.

---

## Så ritar du en form i PDF C# – sätt upp projektet

1. **Skapa ett nytt konsolprojekt**  

   ```bash
   dotnet new console -n PdfRectangleDemo
   cd PdfRectangleDemo
   ```

2. **Lägg till Aspose.Pdf‑paketet**  

   ```bash
   dotnet add package Aspose.Pdf
   ```

3. **Placera `input.pdf`** i projektkatalogen (eller i någon mapp du refererar till senare).

Projektet är nu redo att kompilera kod som **lägger till rektangel i PDF**‑filer.

---

## Steg 1: Ladda PDF‑dokumentet

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

class Program
{
    static void Main()
    {
        // Load the existing PDF file.
        Document pdfDoc = new Document("input.pdf");
```

*Klassen `Document` analyserar filen och exponerar en `Pages`‑samling. Laddning är den första nödvändiga operationen innan någon ritning kan ske.*

---

## Steg 2: Välj målsidan

```csharp
        // Get the first page (pages are 1‑based).
        Page firstPage = pdfDoc.Pages[1];
```

*Om du behöver lägga till rektangeln på en annan sida, ersätt indexet med önskat sidnummer. Biblioteket kastar ett undantag när indexet ligger utanför intervallet, så se till att PDF‑filen innehåller tillräckligt många sidor.*

---

## Steg 3: Definiera rektangelns gränser

```csharp
        // Define the rectangle's position and size (points).
        // (left, bottom, right, top) – origin is bottom‑left.
        Rectangle bounds = new Rectangle(50, 700, 300, 800);
```

*Koordinatsystemet använder punkter (1 pt = 1/72 tum). Exemplet skapar en rektangel som är 250 pt bred och 100 pt hög nära sidans överkant. Justera siffrorna så att de passar ditt layout.*

---

## Steg 4: Skapa rektangel‑formen

```csharp
        // Create a rectangle shape with the defined bounds.
        Rectangle rectangleShape = new Rectangle(bounds)
        {
            // Optional styling – a semi‑transparent blue fill.
            FillColor = Color.FromRgb(0, 120, 215),
            FillOpacity = 0.4,

            // Optional border – 2 pt thick, dark gray.
            Border = new Border
            {
                Width = 2,
                Color = Color.FromRgb(50, 50, 50)
            }
        };
```

*Klassen `Rectangle` ärver från `GraphicalObject`. Att sätta `FillColor` och `Border` är valfritt, men det visar hur du styr utseendet när du **hur man ritar en form i PDF C#** bortom en enkel kontur.*

---

## Steg 5: Lägg till rektangeln på sidan

```csharp
        // Add the rectangle shape to the page's paragraph collection.
        firstPage.Paragraphs.Add(rectangleShape);
```

*Paragrafer är behållaren för alla ritbara objekt. Genom att infoga formen i `Paragraphs` renderar Aspose.Pdf den när dokumentet sparas.*

---

## Steg 6: Spara den modifierade PDF‑filen

```csharp
        // Save the updated PDF to a new file.
        pdfDoc.Save("output.pdf");

        // Inform the user.
        Console.WriteLine("Rectangle added and saved to output.pdf");
    }
}
```

*Sparandet skapar en ny fil så att den ursprungliga `input.pdf` förblir oförändrad. Du kan skriva över källfilen genom att ange samma sökväg, men att behålla en backup är en bästa praxis.*

---

## Fullständig källkod (körbar)

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using System.Drawing;   // For Color struct

class Program
{
    static void Main()
    {
        // Step 1: Load the PDF document
        Document pdfDoc = new Document("input.pdf");

        // Step 2: Get the first page (pages are 1‑based)
        Page firstPage = pdfDoc.Pages[1];

        // Step 3: Define rectangle bounds (left, bottom, right, top)
        Rectangle bounds = new Rectangle(50, 700, 300, 800);

        // Step 4: Create a rectangle shape with optional styling
        Rectangle rectangleShape = new Rectangle(bounds)
        {
            FillColor = Color.FromArgb(102, 0, 120, 215), // 40 % opacity blue
            FillOpacity = 0.4,
            Border = new Border
            {
                Width = 2,
                Color = Color.FromRgb(50, 50, 50)
            }
        };

        // Step 5: Add the rectangle shape to the page
        firstPage.Paragraphs.Add(rectangleShape);

        // Step 6: Save the modified PDF
        pdfDoc.Save("output.pdf");

        Console.WriteLine("Rectangle added to PDF successfully.");
    }
}
```

**Förväntat resultat** – Öppna `output.pdf` i någon PDF‑visare. Du bör se en blåfylld rektangel nära övre högra hörnet på den första sidan, med en mörkgrå kontur.

---

## Hur man ritar en form i PDF C# på flera sidor

Om du behöver **lägga till rektangel i PDF** på varje sida, loopa igenom `Pages`‑samlingen:

```csharp
foreach (Page page in pdfDoc.Pages)
{
    Rectangle rect = new Rectangle(50, 700, 300, 800);
    Rectangle shape = new Rectangle(rect)
    {
        FillColor = Color.FromArgb(80, 255, 0, 0), // semi‑transparent red
        Border = new Border { Width = 1, Color = Color.Black }
    };
    page.Paragraphs.Add(shape);
}
```

*Detta mönster återanvänder samma gränser på varje sida. Justera koordinaterna per sida om du behöver olika positioner.*

---

## Vanliga fallgropar och bästa‑praxis‑tips

| Problem | Varför det händer | Lösning |
|---------|-------------------|---------|
| Rektangeln visas utanför sidan | Koordinaterna mäts från nedre vänstra hörnet; ett top‑orienterat koordinatsystem kan skapa förvirring. | Kom ihåg att Y‑axeln växer uppåt. Använd värden som ryms inom sidstorleken (`page.PageInfo.Width`, `page.PageInfo.Height`). |
| Formen är osynlig | Fyllnadsopaciteten är satt till `0` eller kantbredden är `0`. | Se till att `FillOpacity` är större än `0` och att `Border.Width` är minst `0.5`. |
| Sparandet kastar `AccessDeniedException` | Utdatafilen är öppen i ett annat program. | Stäng alla visare innan du kör koden, eller spara till en annan sökväg. |
| Rektangeln överlappar befintligt innehåll | Ingen lagerkontroll har satts. | Använd egenskapen `ZIndex` (högre värden renderas ovanpå) om du behöver styra lagren. |

---

## Utöka rektangeln – gradienter, rotation och transparens

Aspose.Pdf stödjer avancerad grafik. För att skapa en roterad rektangel med en linjär gradient:

```csharp
Rectangle gradientRect = new Rectangle(bounds)
{
    // Gradient fill from left (blue) to right (green)
    FillColor = Color.Blue,
    FillColor2 = Color.Green,
    FillMode = FillMode.LinearGradient,
    // Rotate 45 degrees around the rectangle's center
    Rotation = 45
};
firstPage.Paragraphs.Add(gradientRect);
```

*Detta kodmönster visar **hur man ritar en form i PDF C#** med rikare visuella effekter.*

---

## Verifiera resultatet programatiskt

Du kan bekräfta att rektangeln har lagts till genom att kontrollera sidans paragrafantal:

```csharp
int shapeCount = firstPage.Paragraphs.Count;
Console.WriteLine($"Page 1 now contains {shapeCount} paragraph objects.");
```

Om antalet har ökat med ett efter insättningen har operationen lyckats.

---

## Slutsats

Du vet nu hur du **lägger till rektangel i PDF**‑filer med C#. Handledningen täckte hur man laddar ett dokument, definierar gränser, skapar en rektangel‑form, infogar den i en sida och sparar resultatet. Du har också sett hur du hanterar flera sidor, undviker vanliga fel och tillämpar avancerad styling.

Nästa steg är att utforska relaterade ämnen som **hur man ritar en form i PDF C#** för cirklar, polygoner eller fria former, samt lära dig kombinera former med text och bilder för att bygga fullt utrustade PDF‑rapporter.

Lycka till med kodningen!

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger vidare på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Hur man lägger till sidstämplar i PDF‑filer med Aspose.PDF för .NET | Vattenstämplar & Bakgrunder Guide](/pdf/english/net/watermarks-backgrounds/implement-page-stamps-aspose-pdf-dotnet/)
- [Hur man lägger till en bildstämpel i en PDF med Aspose.PDF för .NET: En omfattande guide](/pdf/english/net/images-graphics/add-image-stamp-pdf-aspose-dotnet/)
- [Hur man lägger till ett roterande bildvattenstämpel i PDF‑filer med Aspose.PDF för .NET](/pdf/english/net/watermarks-backgrounds/add-rotating-image-watermark-aspose-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}