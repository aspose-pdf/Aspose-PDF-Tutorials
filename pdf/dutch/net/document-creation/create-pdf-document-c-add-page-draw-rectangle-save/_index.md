---
category: general
date: 2026-02-14
description: 'Maak snel een PDF‑document in C#: voeg een pagina toe aan de PDF, teken
  een rechthoek en sla de PDF op in een bestand met Aspose.Pdf in een paar regels
  code.'
draft: false
keywords:
- create pdf document c#
- add page to pdf
- how to draw rectangle
- add shape to pdf
- save pdf to file
language: nl
og_description: Maak PDF‑document C# in enkele minuten. Leer hoe je een pagina aan
  een PDF toevoegt, een rechthoek tekent, een vorm aan een PDF toevoegt en een PDF
  opslaat naar een bestand met duidelijke codevoorbeelden.
og_title: PDF-document maken met C# – Stapsgewijze handleiding
tags:
- Aspose.Pdf
- C#
- PDF generation
title: PDF-document maken C# – Pagina toevoegen, rechthoek tekenen & opslaan
url: /nl/net/document-creation/create-pdf-document-c-add-page-draw-rectangle-save/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PDF-document maken in C# – Pagina toevoegen, rechthoek tekenen & opslaan

Heb je ooit **een PDF-document in C#** moeten maken vanaf nul en je afgevraagd waar je moet beginnen? Je bent niet de enige—veel ontwikkelaars lopen tegen dezelfde muur aan wanneer ze voor het eerst programmatisch PDF‑generatie aanpakken. Het goede nieuws? Met een paar regels Aspose.Pdf‑code kun je een pagina aan een PDF toevoegen, een rechthoek tekenen en **de PDF opslaan naar een bestand** zonder al te veel moeite.

In deze tutorial lopen we alles door wat je nodig hebt: het initialiseren van de PDF, een nieuwe pagina invoegen, een rechthoekvorm tekenen en tenslotte het bestand op schijf opslaan. Aan het einde heb je een werkende console‑app die een scherp blauw omlijnde rechthoek produceert op een verse PDF‑pagina.

## Wat je nodig hebt

- **.NET 6 of later** (het voorbeeld gebruikt top‑level statements, maar elke recente .NET‑versie werkt)
- **Aspose.Pdf for .NET** NuGet‑package  
  ```bash
  dotnet add package Aspose.Pdf
  ```
- Een map waarin je schrijfrechten hebt – de tutorial slaat het bestand op in `YOUR_DIRECTORY/shapes.pdf`.

Geen extra configuratie, geen XML, alleen gewone C#.

## PDF-document maken in C# – Overzicht

De eerste stap is het aanmaken van een `Document`‑object. Beschouw dit als je lege canvas; alles wat je later toevoegt—pagina’s, tekst, vormen—wordt gekoppeld aan deze enkele instantie.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

// Step 1: Create a new PDF document (the canvas)
using var pdfDocument = new Document();
```

> **Waarom `using var`?**  
> De `Document`‑klasse implementeert `IDisposable`. Het omhullen met een `using`‑statement garandeert dat alle unmanaged resources (bestandshandvatten, native buffers) worden vrijgegeven zodra we klaar zijn, wat vooral belangrijk is in langdurige services.

## Pagina toevoegen aan PDF

Een PDF zonder pagina’s is als een boek zonder bladzijden—tamelijk nutteloos. Een pagina toevoegen is één methode‑aanroep, maar geeft je ook een `Page`‑object dat je later kunt manipuleren.

```csharp
// Step 2: Add a fresh page to the document
var pdfPage = pdfDocument.Pages.Add();
```

> **Tip:** De nieuw toegevoegde pagina neemt automatisch de standaardgrootte (A4) over. Als je een aangepaste grootte nodig hebt, kun je `pdfPage.PageInfo.Width` en `Height` instellen voordat je enige inhoud toevoegt.

## Hoe een rechthoek te tekenen

Nu het leuke deel: een rechthoek tekenen. Aspose.Pdf gebruikt de `RectangleShape`‑klasse, die een `Rectangle` (x, y, breedte, hoogte) verwacht die de grenzen definieert. De coördinaten beginnen bij de linksonderhoek van de pagina.

```csharp
// Step 3: Define the rectangle bounds (x, y, width, height)
// This will be validated – an exception is thrown if the rectangle is out of bounds
var rectangleBounds = new Rectangle(50, 50, 200, 150);
```

> **Randgeval:** Als `x + width` de paginabreedte overschrijdt of `y + height` de paginahhoogte, gooit Aspose een `ArgumentException`. Controleer altijd je afmetingen, vooral bij het genereren van PDF’s voor verschillende paginagroottes.

## Vorm toevoegen aan PDF

Met de grenzen klaar, maken we de vorm, geven we een blauwe lijn en plaatsen we deze in de alinea‑collectie van de pagina.

```csharp
// Step 4: Create a rectangle shape with a blue stroke and add it to the page
var rectangleShape = new RectangleShape(rectangleBounds)
{
    StrokeColor = Color.Blue,   // Outline color
    // FillColor = Color.LightGray, // Uncomment to add a fill
    // LineWidth = 2                // Adjust border thickness if needed
};
pdfPage.Paragraphs.Add(rectangleShape);
```

> **Waarom toevoegen aan `Paragraphs`?**  
> In Aspose.Pdf worden visuele elementen zoals vormen behandeld als “paragraphs” omdat ze een rechthoekig gebied op de pagina innemen. Dit ontwerp houdt de layout‑engine consistent tussen tekst en grafische elementen.

## PDF opslaan naar bestand

De laatste stap is het document permanent maken. Geef een volledig pad op, en Aspose regelt de zware klus—compressie, object‑streams en cross‑reference‑tabellen worden automatisch afgehandeld.

```csharp
// Step 5: Save the PDF to a file
pdfDocument.Save("YOUR_DIRECTORY/shapes.pdf");
```

> **Pro tip:** Gebruik `Path.Combine(Environment.CurrentDirectory, "shapes.pdf")` als je het bestand naast je executable wilt plaatsen, of roep vooraf `Directory.CreateDirectory` aan om een `DirectoryNotFoundException` te voorkomen.

### Verwacht resultaat

Open `shapes.pdf` met een PDF‑viewer. Je zou een enkele A4‑pagina moeten zien met een **blauw omlijnde rechthoek** die 50 punten van de linker‑ en onderkant is geplaatst, met een afmeting van 200 × 150 punten. Geen tekst, alleen de vorm—perfect voor watermerken, formulier‑velden of visuele placeholders.

![PDF document with a blue rectangle created using create pdf document c#](https://example.com/images/pdf-rectangle.png "PDF document with a blue rectangle created using create pdf document c#")

*Alt‑tekst:* *PDF‑document met een blauwe rechthoek gemaakt met create pdf document c#.*

## Volledig werkend voorbeeld

Hieronder staat het complete, kant‑klaar‑te‑kopiëren programma. Het compileert als een console‑app (`dotnet new console`) en draait zonder extra configuratie behalve het NuGet‑package.

```csharp
// Program.cs
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

using var pdfDocument = new Document();               // Create PDF document
var pdfPage = pdfDocument.Pages.Add();                // Add a page

// Define rectangle bounds (x, y, width, height)
// Aspose validates the rectangle – out‑of‑bounds throws an exception
var rectangleBounds = new Rectangle(50, 50, 200, 150);

// Create the rectangle shape (blue stroke) and add it to the page
var rectangleShape = new RectangleShape(rectangleBounds)
{
    StrokeColor = Color.Blue
};
pdfPage.Paragraphs.Add(rectangleShape);

// Save the document to disk
pdfDocument.Save("YOUR_DIRECTORY/shapes.pdf");

// Inform the user
Console.WriteLine("PDF created successfully at YOUR_DIRECTORY/shapes.pdf");
```

Voer het programma uit, open het gegenereerde bestand, en je ziet de vorm precies op de plek die we hebben gedefinieerd.

## Veelgestelde vragen & valkuilen

- **V:** *Wat als ik een gevulde rechthoek wil?*  
  **A:** Haal de commentaartekens weg bij de `FillColor`‑regel in de `RectangleShape`‑initializer. Aspose ondersteunt effen kleuren, verlopen en zelfs afbeeldingsvullingen.

- **V:** *Kan ik meerdere vormen op dezelfde pagina tekenen?*  
  **A:** Zeker. Maak gewoon extra `RectangleShape`, `Ellipse` of `Polygon`‑objecten aan en voeg elk toe aan `pdfPage.Paragraphs`.

- **V:** *Is het coördinatensysteem altijd linksonder?*  
  **A:** Ja, Aspose volgt de PDF‑specificatie waarbij de oorsprong (0,0) zich in de linkeronderhoek bevindt. Als je liever een linkerboven‑oorsprong hebt, moet je `y = pageHeight - gewensteY` berekenen.

- **V:** *Wat gebeurt er als de doelmap niet bestaat?*  
  **A:** `pdfDocument.Save` zal een `DirectoryNotFoundException` gooien. Maak de map vooraf aan met `Directory.CreateDirectory`.

## Volgende stappen

Nu je weet hoe je **een pagina aan een PDF toevoegt**, **een rechthoek tekent**, **een vorm aan een PDF toevoegt**, en **een PDF opslaat naar een bestand**, kun je dit fundament uitbreiden:

- Tekst, afbeeldingen of tabellen naast vormen invoegen.  
- `Graphics` gebruiken voor vrije vormtekeningen (lijnen, bogen, aangepaste paden).  
- PDF‑versleuteling of digitale handtekeningen verkennen als beveiliging een rol speelt.  

Al deze onderwerpen bouwen direct voort op de code die we net hebben behandeld, dus voel je vrij om te experimenteren.

---

**Kort samengevat:** Je hebt zojuist de volledige workflow geleerd om **een PDF-document in C#** te maken met Aspose.Pdf—initialiseren, een pagina toevoegen, een rechthoek tekenen en het bestand opslaan. Het is een solide bouwsteen voor facturen, rapporten, certificaten of elk geautomatiseerd document dat je on‑the‑fly moet genereren. Veel programmeerplezier!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}