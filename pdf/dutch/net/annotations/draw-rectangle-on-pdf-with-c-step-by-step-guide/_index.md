---
category: general
date: 2026-06-21
description: Teken een rechthoek op PDF met C#. Leer hoe je een PDF-document laadt,
  een zwarte rechthoekannotatie maakt en de aangepaste PDF efficiënt opslaat.
draft: false
keywords:
- draw rectangle on pdf
- load pdf document
- add black rectangle
- create black rectangle
- save modified pdf
language: nl
og_description: Teken een rechthoek op een PDF in C# door een PDF‑document te laden,
  een zwarte rechthoekannotatie te maken en de gewijzigde PDF op te slaan. Volledige
  code inbegrepen.
og_title: Rechthoek tekenen op PDF met C# – Complete programmeertutorial
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Draw rectangle on PDF using C#. Learn how to load PDF document, create
    black rectangle annotation, and save modified PDF efficiently.
  headline: Draw Rectangle on PDF with C# – Step‑by‑Step Guide
  type: TechArticle
- description: Draw rectangle on PDF using C#. Learn how to load PDF document, create
    black rectangle annotation, and save modified PDF efficiently.
  name: Draw Rectangle on PDF with C# – Step‑by‑Step Guide
  steps:
  - name: .NET 6.0 SDK (or any recent .NET version) installed
    text: .NET 6.0 SDK (or any recent .NET version) installed
  - name: 'A reference to **Aspose.PDF for .NET** (available via NuGet: `Install-Package
      Aspose.PDF`)'
    text: 'A reference to **Aspose.PDF for .NET** (available via NuGet: `Install-Package
      Aspose.PDF`)'
  - name: An existing PDF file (`input.pdf`) placed in a folder you can read/write
    text: An existing PDF file (`input.pdf`) placed in a folder you can read/write
  type: HowTo
tags:
- PDF
- C#
- Aspose.PDF
title: Rechthoek tekenen op PDF met C# – Stapsgewijze handleiding
url: /nl/net/annotations/draw-rectangle-on-pdf-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Rechthoek tekenen in PDF met C# – Complete programmeertutorial

Heb je ooit een **rechthoek op PDF**‑bestanden moeten tekenen vanuit een .NET‑app, maar wist je niet waar te beginnen? Je bent niet de enige. Of het nu gaat om het markeren van een sectie, het redigeren van gevoelige gegevens, of simpelweg een visuele aanwijzing toevoegen, leren hoe je *rechthoek op PDF* programmatically kunt tekenen, kan je uren handmatig bewerken besparen.

In deze gids lopen we een praktisch voorbeeld door dat **een PDF‑document laadt**, **een zwarte rechthoek maakt**, en vervolgens **de gewijzigde PDF opslaat**. Aan het einde heb je een herbruikbare snippet die je in elk C#‑project kunt plaatsen—geen mysterie, alleen duidelijke code en uitleg.

## Wat deze tutorial behandelt

- Hoe je een **pdf‑document laadt** met de Aspose.PDF for .NET‑bibliotheek  
- Het definiëren van de coördinaten van een rechthoek en ervoor zorgen dat deze binnen de paginagrenzen blijft  
- Het gebruik van de **add black rectangle**‑methode om de pagina te annoteren  
- **Save modified pdf** naar een nieuwe bestandslocatie  
- Afhandeling van randgevallen (meerdere pagina’s, out‑of‑bounds‑rechthoeken, aangepaste kleuren)  

Geen externe tools, geen vage verwijzingen—alleen een compleet, uitvoerbaar voorbeeld dat je kunt copy‑pasten.

---

## Voorwaarden

Voordat we beginnen, zorg dat je het volgende hebt:

1. .NET 6.0 SDK (of een recente .NET‑versie) geïnstalleerd  
2. Een referentie naar **Aspose.PDF for .NET** (beschikbaar via NuGet: `Install-Package Aspose.PDF`)  
3. Een bestaand PDF‑bestand (`input.pdf`) geplaatst in een map waar je lees‑/schrijftoegang hebt  

Dat is alles. Als je vertrouwd bent met basis‑C#‑syntaxis, ben je klaar om te starten.

---

## Stap 1: PDF‑document laden

Het eerste wat we nodig hebben is een **load pdf document**‑aanroep. De `Document`‑klasse van Aspose.PDF neemt het bestandspad en leest het volledige bestand in het geheugen.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using System.Drawing;

// Load the source PDF
Document pdfDocument = new Document(@"C:\MyFiles\input.pdf");
```

*Waarom dit belangrijk is*: Het laden van de PDF geeft je toegang tot de pagina’s, metadata en het tekenoppervlak. Zonder deze stap kun je geen vormen plaatsen.

---

## Stap 2: De doelpagina kiezen

PDF‑pagina’s zijn 1‑gebaseerd in Aspose, dus de eerste pagina heeft index 1. Pak de pagina die je wilt annoteren—meestal de eerste voor een snelle demo.

```csharp
// Get the first page (pages are 1‑based)
Page targetPage = pdfDocument.Pages[1];
```

Als je op een andere pagina wilt werken, wijzig dan simpelweg de index. Vergeet niet te controleren of de index bestaat om een `ArgumentOutOfRangeException` te voorkomen.

---

## Stap 3: De rechthoekgeometrie definiëren

Een rechthoek wordt gedefinieerd door de linker‑onder‑(X,Y) en rechter‑boven‑(X,Y) coördinaten. De `Rectangle`‑struct slaat deze op als `LLX`, `LLY`, `URX`, `URY`.

```csharp
// Define the rectangle (lower‑left X,Y and upper‑right X,Y)
Rectangle boundingRect = new Rectangle(100, 100, 300, 300);
```

Voel je vrij om die getallen aan te passen—`100,100` plaatst de linker‑onderhoek 100 punten vanaf de linker‑ en onderrand, terwijl `300,300` de rechter‑bovenhoek 300 punten vanaf de randen zet.

---

## Stap 4: Verifiëren dat de rechthoek binnen de pagina past

Proberen te tekenen buiten de paginagrenzen wordt ofwel genegeerd of veroorzaakt een uitzondering, afhankelijk van de bibliotheekversie. Een snelle controle maakt je code robuuster.

```csharp
// Ensure the rectangle fits within the page dimensions
if (targetPage.PageInfo.Width >= boundingRect.URX &&
    targetPage.PageInfo.Height >= boundingRect.URY)
{
    // Rectangle is safe to add
}
else
{
    throw new InvalidOperationException("Rectangle exceeds page dimensions.");
}
```

*Pro tip*: Als je PDF’s van verschillende formaten wilt ondersteunen, kun je de rechthoek berekenen op basis van een percentage van de paginabreedte/hoogte in plaats van absolute punten.

---

## Stap 5: Zwarte rechthoek‑annotatie toevoegen

Nu het leuke deel—**add black rectangle** aan de pagina. Aspose biedt `AddRectangle` die de geometrie en een `Color` accepteert. We gebruiken `Color.Black` om **create black rectangle** te maken.

```csharp
// Add a black rectangle annotation to the page
targetPage.AddRectangle(boundingRect, Color.Black);
```

Die ene regel doet het zware werk: hij maakt een annotatie‑object, stelt de randkleur in op zwart, en voegt het toe aan de annotatie‑collectie van de pagina.

Als je ooit een andere vulling of randstijl nodig hebt, verken dan de overload die een `Annotation`‑object accepteert waarin je lijndikte, stippellijnpatroon of zelfs doorzichtigheid kunt aanpassen.

---

## Stap 6: Gewijzigde PDF opslaan

Tot slot, sla je wijzigingen op met **save modified pdf**. Je kunt het origineel overschrijven of naar een nieuw bestand schrijven—hier maken we een output‑bestand.

```csharp
// Save the updated PDF to a new location
pdfDocument.Save(@"C:\MyFiles\output.pdf");
```

Dat is de volledige workflow. Voer het programma uit en open `output.pdf`; je zou een solide zwarte rechthoek moeten zien op de door jou gedefinieerde positie.

---

## Volledig werkend voorbeeld

Hieronder vind je een zelfstandige console‑applicatie die alle stappen combineert. Kopieer het naar een nieuw `.csproj`‑bestand en druk op **Run**.

```csharp
using System;
using System.Drawing;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;

namespace PdfRectangleDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load PDF document
            Document pdfDocument = new Document(@"C:\MyFiles\input.pdf");

            // 2️⃣ Get the first page (pages are 1‑based)
            Page firstPage = pdfDocument.Pages[1];

            // 3️⃣ Define the rectangle geometry
            Rectangle rect = new Rectangle(100, 100, 300, 300);

            // 4️⃣ Verify bounds
            if (firstPage.PageInfo.Width < rect.URX || firstPage.PageInfo.Height < rect.URY)
            {
                Console.WriteLine("Rectangle does not fit on the page.");
                return;
            }

            // 5️⃣ Add a black rectangle annotation
            firstPage.AddRectangle(rect, Color.Black);

            // 6️⃣ Save modified PDF
            pdfDocument.Save(@"C:\MyFiles\output.pdf");

            Console.WriteLine("Successfully drew rectangle on PDF and saved the file.");
        }
    }
}
```

**Verwachte output** in de console:

```
Successfully drew rectangle on PDF and saved the file.
```

Open `output.pdf` en je ziet een zwarte rechthoek gepositioneerd op de coördinaten die je hebt opgegeven.

---

## Veelvoorkomende variaties behandelen

| Situatie | Wat te wijzigen | Waarom |
|-----------|----------------|--------|
| **Meerdere pagina’s** | Loop door `pdfDocument.Pages` en pas dezelfde logica toe op elk `Page`‑object. | Maakt batch‑annotatie over een heel document mogelijk. |
| **Andere kleuren** | Vervang `Color.Black` door `Color.Red` of een andere `System.Drawing.Color`. | Handig voor markeren in plaats van redigeren. |
| **Transparante vulling** | Gebruik `new Annotation(rect) { Color = Color.Black, Opacity = 0.5 }`. | Geeft een halfdoorzichtige overlay in plaats van een solide blok. |
| **Dynamische rechthoekgrootte** | Bereken `URX` en `URY` op basis van `PageInfo.Width * 0.5` etc. | Laat de rechthoek zich aanpassen aan verschillende paginagroottes. |
| **Foutafhandeling** | Plaats het hele blok in een `try…catch` en log `Aspose.Pdf.IOException`. | Voorkomt crashes wanneer het bronbestand ontbreekt of vergrendeld is. |

Deze aanpassingen laten zien hoe je **create black rectangle**‑annotaties in diverse contexten kunt maken zonder de kernlogica te herschrijven.

---

## Pro Tips & Valkuilen

- **Document vrijgeven**: Hoewel Aspose.PDF `IDisposable` implementeert, is het `using`‑patroon niet strikt vereist voor kortlevende console‑apps. In langdurige services, wikkel `Document` in een `using`‑blok om native resources tijdig vrij te geven.  
- **Coördinatensysteem**: PDF‑coördinaten beginnen in de linker‑onderhoek. Als je gewend bent aan een oorsprong links‑boven (zoals in WinForms), moet je de Y‑as inverteren: `pageHeight - y`.  
- **Prestaties**: Het toevoegen van annotaties aan zeer grote PDF‑bestanden kan veel geheugen verbruiken. Overweeg pagina’s in delen te verwerken of `PdfFileEditor` te gebruiken voor lichtere bewerkingen.  
- **Juridisch**: Zorg dat je rechten hebt om de bron‑PDF te wijzigen—sommige documenten zijn beschermd tegen bewerking.

---

## Conclusie

We hebben zojuist laten zien hoe je **draw rectangle on PDF** kunt uitvoeren met C#—beginnend met **load pdf document**, geometrie definiëren, **add black rectangle**, en tenslotte **save modified pdf**. Het voorbeeld is compleet, uitvoerbaar en aanpasbaar voor real‑world scenario’s zoals batch‑verwerking of aangepaste styling.

Vervolgens kun je andere annotatietypen (tekst, markeringen) toevoegen of meerdere PDF‑bestanden samenvoegen na annotatie. Zowel **load pdf document** als **save modified pdf** blijven ongewijzigd, zodat je dit patroon met vertrouwen kunt uitbreiden.

Heb je een eigen twist geprobeerd? Deel het in de reacties, en happy coding!


## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids zijn gedemonstreerd. Elke bron bevat complete werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Maak een gevulde rechthoekobject in PDF met Java](/pdf/english/java/pdf-images/create-filled-rectangle-object-in-pdf-using-java/)
- [Create Filled Rectangle Object In Pdf Using Java](/pdf/german/java/pdf-images/create-filled-rectangle-object-in-pdf-using-java/)
- [Create Filled Rectangle Object In Pdf Using Java](/pdf/french/java/pdf-images/create-filled-rectangle-object-in-pdf-using-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}