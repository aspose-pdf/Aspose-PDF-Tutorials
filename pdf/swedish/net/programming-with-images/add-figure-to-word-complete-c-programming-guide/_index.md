---
category: general
date: 2026-04-12
description: Lägg till figur i Word snabbt med C#. Lär dig hur du placerar en figur
  i Word, infogar en figur i docx och lägger till anpassad XML för avancerad layout.
draft: false
keywords:
- add figure to word
- position figure in word
- insert figure into docx
- how to add custom xml
- how to position shape word
language: sv
og_description: Lägg till figur i Word snabbt med C#. Lär dig hur du placerar en figur
  i Word, infogar en figur i docx och lägger till anpassad XML för avancerad layout.
og_title: Lägg till figur i Word – Komplett C#‑programmeringsguide
tags:
- C#
- Word Automation
- Document Generation
title: Lägg till figur i Word – Komplett C#‑programmeringsguide
url: /sv/net/programming-with-images/add-figure-to-word-complete-c-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Lägg till figur i Word – Komplett C# programmeringsguide

Har du någonsin behövt **add figure to Word** men varit osäker på var du ska börja? Du är inte ensam. I många kontors‑automatiseringsprojekt är den saknade delen en välplacerad bild eller diagram som finns i en anpassad XML-del. Den här guiden visar dig exakt hur du **position figure in Word**, infogar figuren i en *.docx*-fil och till och med justerar den underliggande anpassade XML‑en så att formen beter sig som vilket inbyggt Word‑objekt som helst.

Vi går igenom ett verkligt exempel med hjälp av GemBox.Document‑biblioteket (gratis för små filer, kommersiellt för större arbetsbelastningar). I slutet har du ett självständigt, körbart program som placerar en figur på koordinaterna X = 50, Y = 200 i en taggad‑innehållsbehållare. Inga vaga “see the docs”-genvägar—bara tydlig kod, varför den fungerar, och tips du kan kopiera direkt in i ditt eget projekt.

## Förutsättningar

- .NET 6.0 eller senare (koden kompileras även med .NET Core 3.1)
- **GemBox.Document** NuGet‑paket (`Install-Package GemBox.Document`)
- En start‑Word‑fil (`input.docx`) som redan innehåller en anpassad XML‑tagg där du vill att figuren ska visas
- Grundläggande C#‑kunskaper (du kommer att se varför varje rad är viktig)

> **Pro tip:** Om du inte har ett för‑taggat dokument kan du skapa ett i Word genom att infoga en *Content Control* → *XML Mapping Pane* → mappa en anpassad XML‑del. Biblioteket kommer att behandla den kontrollen som `TaggedContent`.

## Steg 1 – Läs in källdokumentet

Det första vi gör är att öppna den befintliga *.docx*-filen. `Document` är ingångspunkten för alla GemBox‑operationer.

```csharp
using GemBox.Document;
using System.Drawing;

// Set the license key (free version uses a limited license key)
ComponentInfo.SetLicense("FREE-LIMITED-KEY");

// Step 1: Load the source document
Document doc = new Document(@"YOUR_DIRECTORY\input.docx");
```

*Varför?* Att läsa in filen ger oss åtkomst till dess interna delar, inklusive eventuella anpassade XML‑behållare. Utan detta skulle vi inte kunna hitta `TaggedContent`‑noden som ska hålla vår figur.

## Steg 2 – Åtkomst till den taggade innehållet (anpassad XML‑behållare)

Anpassad XML lagras i en *content control* i Word. GemBox exponerar den som `TaggedContent`. 

```csharp
// Step 2: Access the document's tagged content (the container for custom XML)
TaggedContent taggedContent = doc.TaggedContent;
```

Om dokumentet har flera taggade sektioner returnerar `TaggedContent` den **första**. Du kan också enumerera `doc.TaggedContents` för att välja en specifik tagg efter namn.

## Steg 3 – Skapa Figure‑elementet

Ett `FigureElement` representerar en bild, diagram eller något visuellt objekt som Word behandlar som en *shape*. Vi kommer att skapa det i den taggade behållaren.

```csharp
// Step 3: Create a new figure element that will be placed inside the tagged content
FigureElement figure = taggedContent.CreateFigureElement();
```

*Varför skapa en figur här?* Genom att fästa den på den anpassade XML‑noden vet Word att figuren tillhör den logiska sektionen, vilket är avgörande för senare redigering eller arbetsflöden baserade på content‑control.

## Steg 4 – Positionera figuren exakt

Word använder punkter (1 pt ≈ 1/72 tum) för positionering. `PointF`‑strukturen låter oss enkelt sätta X/Y‑koordinater.

```csharp
// Step 4: Position the figure at the desired coordinates (X = 50, Y = 200)
figure.Position = new PointF(50, 200);
```

> **How to position shape word:** `Position`‑egenskapen accepterar en `PointF` där det första värdet är den horisontella förskjutningen (vänster) och det andra är den vertikala förskjutningen (top) relativt sidmarginalen. Justera dessa siffror för att finjustera placeringen.

## Steg 5 – Infoga figuren i den taggade innehållsträdet

Nu fäster vi figuren till rot‑elementet i det anpassade XML‑trädet. Detta lägger fysiskt till formen i Word‑dokumentet.

```csharp
// Step 5: Insert the figure into the root element of the tagged content tree
taggedContent.RootElement.AppendChild(figure);
```

Vid detta tillfälle finns figuren i dokumentet, men den har ännu ingen bildkälla. Låt oss lägga till en enkel PNG från disk.

```csharp
// Optional: Load an image and assign it to the figure
using (var imageStream = System.IO.File.OpenRead(@"YOUR_DIRECTORY\sample.png"))
{
    figure.Image = new Image(imageStream);
}
```

## Steg 6 – Spara det modifierade dokumentet

Slutligen skriver vi tillbaka ändringarna till en ny *.docx*-fil.

```csharp
// Step 6: Save the updated document
doc.Save(@"YOUR_DIRECTORY\output.docx");
```

När du öppnar `output.docx` i Word kommer du att se bilden placerad exakt på (50, 200) i det anpassade XML‑blocket du riktade in på.

### Fullt fungerande exempel

```csharp
using GemBox.Document;
using System.Drawing;
using System.IO;

class Program
{
    static void Main()
    {
        // License (free version)
        ComponentInfo.SetLicense("FREE-LIMITED-KEY");

        // Load the source DOCX
        Document doc = new Document(@"YOUR_DIRECTORY\input.docx");

        // Access the first tagged content container
        TaggedContent taggedContent = doc.TaggedContent;

        // Create a new figure element
        FigureElement figure = taggedContent.CreateFigureElement();

        // Position the figure (X = 50 pt, Y = 200 pt)
        figure.Position = new PointF(50, 200);

        // Load an image file and assign it
        using (FileStream fs = File.OpenRead(@"YOUR_DIRECTORY\sample.png"))
        {
            figure.Image = new Image(fs);
        }

        // Append the figure to the custom XML root
        taggedContent.RootElement.AppendChild(figure);

        // Save the result
        doc.Save(@"YOUR_DIRECTORY\output.docx");
    }
}
```

**Expected result:** När du öppnar `output.docx` visas PNG‑filen placerad exakt där du angav, inbäddad i den anpassade XML‑delen. Om du granskar dokumentets XML (`.docx` → unzip → `word/document.xml`) ser du ett `<w:pict>`‑element med de korrekta `<v:shape>`‑koordinaterna.

## Vanliga frågor & kantfall

### Vad händer om dokumentet har flera taggade sektioner?

Använd `doc.TaggedContents` för att enumerera och välja efter taggnamn:

```csharp
TaggedContent myTag = doc.TaggedContents.First(tc => tc.TagName == "MyCustomTag");
```

### Hur lägger man till en bildtext till figuren?

```csharp
figure.Caption = new CaptionElement("Figure 1 – Sample Diagram");
```

### Fungerar detta med Word 2010 och senare?

Ja. GemBox.Document riktar sig mot Open XML‑standarden, som är kompatibel med Word 2007 + (inklusive 2010, 2013, 2016, 2019 och Microsoft 365).

### Vad händer om jag behöver rotera formen?

```csharp
figure.Rotation = 45; // degrees
```

### Hur lägger man till en vektorgrafik istället för en rasterbild?

```csharp
figure.Image = new Image(@"YOUR_DIRECTORY\vector.svg");
```

## Pro Tips & Fallgropar

- **File paths:** Använd `Path.Combine` för att undvika hårdkodade separatorer, särskilt på icke‑Windows‑plattformar.
- **License limits:** Den fria GemBox‑licensen begränsar dokumentstorleken till 20 KB. För större filer, köp en kommersiell nyckel.
- **Performance:** Återanvändning av en enda `Document`‑instans för batch‑behandling minskar minnesbelastningen dramatiskt.
- **Shape overflow:** Om figurens dimensioner överskrider sidmarginalerna kommer Word att klippa den. Justera `figure.Width` och `figure.Height` därefter.

## Slutsats

Du vet nu **how to add figure to Word**, exakt **position figure in Word**, och hur du manipulerar den underliggande anpassade XML‑en för att få formen att bete sig som vilket inbyggt element som helst. Det kompletta, körbara exemplet demonstrerar varje steg—från att läsa in dokumentet, skapa ett `FigureElement`, sätta dess koordinater, bifoga en bild och slutligen spara den uppdaterade *.docx*.

Nästa steg, prova att experimentera med **insert figure into docx** genom att lägga till flera figurer, använda loopar eller generera diagram i farten. Du kan också utforska **how to add custom xml** för rikare content‑controls eller lära dig **how to position shape word** i tabeller och sidhuvuden. Möjligheterna är oändliga, och med grunderna täckta här är du redo att automatisera Word‑dokument som ett proffs.

Lycka till med kodandet, och tveka inte att lämna en kommentar om du stöter på problem!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}