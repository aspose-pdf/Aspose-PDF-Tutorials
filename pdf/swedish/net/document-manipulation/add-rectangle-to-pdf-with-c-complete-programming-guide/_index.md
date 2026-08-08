---
category: general
date: 2026-06-05
description: Lägg till rektangel i PDF med Aspose.Pdf i C#. Lär dig hur du laddar
  en befintlig PDF, redigerar PDF-sidan och infogar en form i PDF på några minuter.
draft: false
keywords:
- add rectangle to pdf
- draw rectangle on pdf
- load existing pdf
- edit pdf page
- insert shape into pdf
language: sv
og_description: Lägg till rektangel i PDF snabbt. Denna handledning visar hur du laddar
  en befintlig PDF, redigerar en PDF-sida och ritar en rektangel i PDF med Aspose.Pdf.
og_title: Lägg till rektangel i PDF med C# – Steg‑för‑steg‑guide
schemas:
- author: Aspose
  dateModified: '2026-06-05'
  description: Add rectangle to PDF using Aspose.Pdf in C#. Learn how to load existing
    PDF, edit PDF page, and insert shape into PDF in minutes.
  headline: Add Rectangle to PDF with C# – Complete Programming Guide
  type: TechArticle
- description: Add rectangle to PDF using Aspose.Pdf in C#. Learn how to load existing
    PDF, edit PDF page, and insert shape into PDF in minutes.
  name: Add Rectangle to PDF with C# – Complete Programming Guide
  steps:
  - name: Prerequisites
    text: '- .NET 6.0 or later (the code also works on .NET Framework 4.6+). - Aspose.Pdf
      for .NET NuGet package (`Install-Package Aspose.Pdf`). - Basic familiarity with
      C# syntax (no deep PDF knowledge required).'
  - name: Why loading matters
    text: Before you can draw anything, the PDF must be in memory. The `Document`
      constructor reads the file, parses its internal structure, and gives you an
      object model to work with. If the file is locked or corrupted, Aspose will throw
      a descriptive exception—so you know exactly what went wrong.
  - name: Code
    text: '```csharp Document doc = new Document("YOUR_DIRECTORY/input.pdf"); ```'
  - name: Why page selection is crucial
    text: PDFs are page‑oriented; each page has its own coordinate system. Aspose
      uses a **1‑based** index, which trips up developers coming from 0‑based collections.
      Selecting the wrong page either throws an `ArgumentOutOfRangeException` or modifies
      an unintended page.
  - name: Code
    text: '```csharp Page page = doc.Pages[1]; // First page ```'
  - name: Understanding the rectangle coordinates
    text: A rectangle in Aspose.Pdf is defined by its lower‑left (`xLL`, `yLL`) and
      upper‑right (`xUR`, `yUR`) corners. The coordinate system starts at the **bottom‑left**
      of the page, with X increasing to the right and Y increasing upward. This is
      opposite of many UI frameworks, so keep an eye on the axes.
  - name: Code to add the shape
    text: '```csharp Aspose.Pdf.Rectangle rect = new Aspose.Pdf.Rectangle(0, 0, 500,
      700); page.AddRectangle(rect); ```'
  - name: Why saving is the final step
    text: All manipulations stay in memory until you persist them. `Document.Save`
      writes the new content to disk (or stream). Overwriting the original file is
      possible, but keeping a backup (`output.pdf`) is safer.
  - name: Code
    text: '```csharp doc.Save("YOUR_DIRECTORY/output.pdf"); ```'
  type: HowTo
- questions:
  - answer: Yes—loop through `doc.Pages` and repeat the `AddRectangle` call for each
      `Page` object.
    question: Can I add the rectangle to every page automatically?
  - answer: Aspose provides `AddCircle`, `AddPolygon`, and `AddPolyline` methods.
      The same rectangle logic applies for bounding boxes.
    question: What if I need to draw a circle or a polygon?
  - answer: 'Compute the center coordinates:'
    question: Is there a way to position the rectangle relative to the page center?
  - answer: Aspose loads pages lazily, but if you’re processing thousands of pages,
      consider using `PdfExtractor` to work on subsets or stream the file to reduce
      memory footprint.
    question: Performance concerns for large PDFs?
  type: FAQPage
tags:
- pdf
- csharp
- aspose
- shape-manipulation
title: Lägg till en rektangel i PDF med C# – Komplett programmeringsguide
url: /sv/net/document-manipulation/add-rectangle-to-pdf-with-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Lägg till rektangel i PDF med C# – Komplett programmeringsguide

Har du någonsin behövt **lägga till rektangel i pdf** men varit osäker på vilken API‑anrop du ska använda? Du är inte ensam—många utvecklare stöter på den muren när de första gången försöker redigera en PDF programatiskt. Den goda nyheten? Med några rader C# och det kraftfulla Aspose.Pdf‑biblioteket kan du rita en rektangel på vilken sida som helst i ett befintligt dokument på ett ögonblick.

I den här guiden går vi igenom hur du laddar en befintlig PDF, väljer rätt sida, definierar en rektangel som passar, och slutligen infogar formen i PDF‑filen. I slutet har du ett återanvändbart kodsnutt som du kan klistra in i vilket .NET‑projekt som helst. Åh, och vi kommer också att beröra nyanser kring **draw rectangle on pdf** som du kanske inte har tänkt på.

## Vad du får

- En tydlig, steg‑för‑steg‑lösning som fungerar direkt.
- Förståelse för hur **load existing pdf**‑filer kan laddas säkert.
- Tips för **edit pdf page** utan att förstöra dokumentet.
- Strategier för att **insert shape into pdf** utöver bara rektanglar.
- Färdig‑att‑köra C#‑kod som du kan kopiera‑klistra in omedelbart.

### Förutsättningar

- .NET 6.0 eller senare (koden fungerar också på .NET Framework 4.6+).
- Aspose.Pdf för .NET NuGet‑paket (`Install-Package Aspose.Pdf`).
- Grundläggande kunskap om C#‑syntax (ingen djup PDF‑kunskap krävs).

Om du har detta, låt oss dyka in.

![Exempel på att lägga till rektangel i PDF](add-rectangle-to-pdf.png "Skärmbild som visar en rektangel tillagd på en PDF‑sida – add rectangle to pdf")

## Lägg till rektangel i PDF – Steg‑för‑steg‑översikt

Nedan är det fullständiga, körbara exemplet som följer exakt den ordning vi kommer att diskutera:

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the existing PDF file
        Document doc = new Document("YOUR_DIRECTORY/input.pdf");

        // 2️⃣ Select the first page (pages are 1‑based)
        Page page = doc.Pages[1];

        // 3️⃣ Define a rectangle that fits inside the page bounds
        //    (xLL, yLL, xUR, yUR) – lower‑left & upper‑right corners
        Aspose.Pdf.Rectangle rect = new Aspose.Pdf.Rectangle(0, 0, 500, 700);

        // 4️⃣ Add the rectangle to the page – this draws the shape
        page.AddRectangle(rect);

        // 5️⃣ Save the modified PDF to a new file
        doc.Save("YOUR_DIRECTORY/output.pdf");
    }
}
```

Låt oss nu gå igenom varje rad så att du förstår **why** vi gör vad vi gör, inte bara **what**.

## Ladda befintligt PDF‑dokument

### Varför laddning är viktigt

Innan du kan rita något måste PDF‑filen vara i minnet. `Document`‑konstruktorn läser filen, parsar dess interna struktur och ger dig en objektmodell att arbeta med. Om filen är låst eller korrupt kommer Aspose att kasta ett beskrivande undantag—så att du exakt vet vad som gick fel.

### Kod

```csharp
Document doc = new Document("YOUR_DIRECTORY/input.pdf");
```

- Ersätt `YOUR_DIRECTORY` med den absoluta eller relativa sökvägen till din källfil.
- Sökvägen kan vara en URL om du aktiverar Asposes fjärrladdning (avancerat scenario).
- **Tip:** Packa in detta i ett `try/catch`‑block för att hantera `FileNotFoundException` eller `PdfException` på ett smidigt sätt.

```csharp
try
{
    Document doc = new Document("input.pdf");
}
catch (Exception ex)
{
    Console.WriteLine($"Failed to load PDF: {ex.Message}");
    return;
}
```

## Välj och förbered sidan

### Varför sidval är avgörande

PDF‑filer är sid‑orienterade; varje sida har sitt eget koordinatsystem. Aspose använder ett **1‑baserat** index, vilket kan förvirra utvecklare som är vana vid 0‑baserade samlingar. Att välja fel sida kastar antingen ett `ArgumentOutOfRangeException` eller ändrar en oavsiktlig sida.

### Kod

```csharp
Page page = doc.Pages[1]; // First page
```

Om du behöver arbeta på sida 3, ändra helt enkelt indexet till `3`. För dynamiska scenarier kan du loopa:

```csharp
foreach (Page pg in doc.Pages)
{
    // Apply rectangle to every page
}
```

## Definiera och rita rektangel i PDF

### Förstå rektangelkoordinaterna

En rektangel i Aspose.Pdf definieras av dess nedre‑vänstra (`xLL`, `yLL`) och övre‑högra (`xUR`, `yUR`) hörn. Koordinatsystemet startar i sidans **nedre‑vänstra** hörn, med X som ökar åt höger och Y som ökar uppåt. Detta är motsatt många UI‑ramverk, så håll koll på axlarna.

- `0,0` är sidans nedre‑vänstra hörn.
- Bredd = `xUR - xLL`; Höjd = `yUR - yLL`.

Om du av misstag sätter en rektangel som är större än sidan, kommer `AddRectangle` att kasta ett undantag. För att undvika det kan du fråga efter sidans storlek:

```csharp
double pageWidth  = page.PageInfo.Width;
double pageHeight = page.PageInfo.Height;
```

Kläm sedan din rektangel:

```csharp
double rectWidth  = Math.Min(500, pageWidth);
double rectHeight = Math.Min(700, pageHeight);
Aspose.Pdf.Rectangle rect = new Aspose.Pdf.Rectangle(0, 0, rectWidth, rectHeight);
```

### Kod för att lägga till formen

```csharp
Aspose.Pdf.Rectangle rect = new Aspose.Pdf.Rectangle(0, 0, 500, 700);
page.AddRectangle(rect);
```

- `AddRectangle` ritar automatiskt en tunn svart kant.
- Vill du ha en fylld rektangel? Använd `page.AddAnnotation(new SquareAnnotation(page, rect) { FillColor = Color.Yellow });`.
- Behöver du en annan linjetjocklek? Sätt `rect.LineWidth = 2;` innan du lägger till.

#### Kantfall: flera rektanglar

Om du anropar `AddRectangle` upprepade gånger lägger varje anrop till en ny form. För att undvika överlappning, förskjut efterföljande rektanglar:

```csharp
for (int i = 0; i < 3; i++)
{
    var offset = i * 20;
    var r = new Aspose.Pdf.Rectangle(offset, offset, 500 + offset, 700 + offset);
    page.AddRectangle(r);
}
```

## Spara den modifierade PDF‑filen

### Varför sparande är sista steget

Alla manipulationer finns i minnet tills du sparar dem. `Document.Save` skriver det nya innehållet till disk (eller ström). Att skriva över originalfilen är möjligt, men att behålla en backup (`output.pdf`) är säkrare.

### Kod

```csharp
doc.Save("YOUR_DIRECTORY/output.pdf");
```

- Du kan också spara till en `MemoryStream` om du behöver skicka PDF‑filen via HTTP:

```csharp
using var ms = new MemoryStream();
doc.Save(ms);
byte[] pdfBytes = ms.ToArray();
// return File(pdfBytes, "application/pdf");
```

## Fullt fungerande exempel (Klar‑för‑kopiering)

När vi sätter ihop allt, här är det slutgiltiga programmet som du kan köra direkt:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using Aspose.Pdf.Text;

class AddRectangleDemo
{
    static void Main()
    {
        const string inputPath  = "input.pdf";
        const string outputPath = "output.pdf";

        // Load the existing PDF
        Document doc;
        try
        {
            doc = new Document(inputPath);
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Error loading PDF: {ex.Message}");
            return;
        }

        // Ensure the document has at least one page
        if (doc.Pages.Count == 0)
        {
            Console.WriteLine("PDF contains no pages.");
            return;
        }

        // Select the first page (1‑based index)
        Page page = doc.Pages[1];

        // Get page dimensions to avoid overflow
        double pageW = page.PageInfo.Width;
        double pageH = page.PageInfo.Height;

        // Define rectangle size (clamp to page bounds)
        double rectW = Math.Min(500, pageW);
        double rectH = Math.Min(700, pageH);
        Aspose.Pdf.Rectangle rect = new Aspose.Pdf.Rectangle(0, 0, rectW, rectH);

        // Optional: set line width and color
        rect.LineWidth = 2;
        rect.Color = Color.Blue;

        // Add rectangle to the page
        page.AddRectangle(rect);

        // Save the result
        doc.Save(outputPath);
        Console.WriteLine($"Rectangle added and saved to {outputPath}");
    }
}
```

**Förväntad output:** Öppna `output.pdf` så ser du en blå‑kantad rektangel förankrad i sidans nedre‑vänstra hörn på den första sidan, med storlek upp till 500 × 700 punkter (eller mindre om sidan är liten).

## Vanliga frågor & pro‑tips

- **Kan jag lägga till rektangeln på varje sida automatiskt?**  
  Ja—loopa igenom `doc.Pages` och upprepa `AddRectangle`‑anropet för varje `Page`‑objekt.

- **Vad händer om jag behöver rita en cirkel eller en polygon?**  
  Aspose tillhandahåller `AddCircle`, `AddPolygon` och `AddPolyline`‑metoder. Samma rektangel‑logik gäller för omgivningsrutor.

- **Finns det ett sätt att positionera rektangeln relativt sidans centrum?**  
  Beräkna mittkoordinaterna:  
  ```csharp
  double centerX = pageW / 2;
  double centerY = pageH / 2;
  double halfW = rectW / 2;
  double halfH = rectH / 2;
  var centeredRect = new Aspose.Pdf.Rectangle(centerX - halfW, centerY - halfH,
                                              centerX + halfW, centerY + halfH);
  page.AddRectangle(centeredRect);
  ```

- **Prestanda‑bekymmer för stora PDF‑filer?**  
  Aspose laddar sidor lat, men om du bearbetar tusentals sidor, överväg att använda `PdfExtractor` för att arbeta på delmängder eller strömma filen för att minska minnesavtrycket.

## Slutsats

Du vet nu **hur man lägger till rektangel

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Skapa PDF‑dokument med Aspose.PDF – Lägg till sida, form & spara](/pdf/english/net/document-creation/create-pdf-document-with-aspose-pdf-add-page-shape-save/)
- [Hur man lägger till sidstämplar i PDF‑filer med Aspose.PDF för .NET: En komplett guide](/pdf/english/net/watermarks-backgrounds/add-page-stamp-aspose-pdf-dotnet-guide/)
- [Lägg till bilder & sidnummer i PDF‑filer med Aspose.PDF för .NET: En komplett guide](/pdf/english/net/document-manipulation/enhance-pdfs-images-page-numbers-aspose-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}