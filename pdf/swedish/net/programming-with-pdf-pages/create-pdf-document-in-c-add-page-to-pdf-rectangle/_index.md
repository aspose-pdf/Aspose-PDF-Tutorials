---
category: general
date: 2026-02-10
description: Skapa PDF-dokument i C# med Aspose.Pdf. Lär dig hur du lägger till en
  sida i PDF och hur du säkert lägger till en rektangel i PDF, med gränskontroll.
draft: false
keywords:
- create pdf document
- add page to pdf
- how to add rectangle pdf
language: sv
og_description: Skapa PDF-dokument i C# med Aspose.Pdf. Denna guide visar hur man
  lägger till en sida i PDF och hur man lägger till en rektangel i PDF samtidigt som
  man kontrollerar gränserna.
og_title: Skapa PDF-dokument i C# – Lägg till en sida i PDF & rektangel
tags:
- pdf
- csharp
- aspose
title: Skapa PDF-dokument i C# – Lägg till sida i PDF & rektangel
url: /sv/net/programming-with-pdf-pages/create-pdf-document-in-c-add-page-to-pdf-rectangle/
---

markdown.

Let's craft translation.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa PDF-dokument i C# – Lägg till sida i PDF & rektangel

Har du någonsin behövt **create pdf document** i C# och inte vetat var du ska börja? Du är inte ensam – de flesta utvecklare stöter på samma hinder när de första gången provar PDF‑genereringsbibliotek. Den goda nyheten är att med Aspose.Pdf kan du snabbt skapa en PDF, lägga till en sida i PDF och till och med rita former som en rektangel utan att svettas.

I den här handledningen går vi igenom ett komplett, körbart exempel som inte bara **creates a PDF document** utan också visar **how to add rectangle PDF**‑objekt på ett säkert sätt genom att slå på global gränskontroll. När du är klar har du en solid förståelse för API‑et, vet varför varje steg är viktigt och ser exakt vilket resultat du bör förvänta dig.

## Vad du behöver

- .NET 6+ (eller .NET Framework 4.6+). Koden fungerar likadant i båda.
- Aspose.Pdf for .NET NuGet‑paket (`Aspose.Pdf`) – installera det via `dotnet add package Aspose.Pdf`.
- Valfri C#‑editor (Visual Studio, VS Code, Rider… du bestämmer).

Ingen extra konfiguration krävs; biblioteket levereras med allt du behöver för att börja generera PDF‑filer direkt.

## Steg 1: Skapa PDF-dokument och aktivera gränskontroll

Det första vi gör är att instansiera ett `Document`‑objekt. Tänk på det som den tomma duken för ditt **create pdf document**‑äventyr. Direkt efter det aktiverar vi en global inställning som tvingar biblioteket att verifiera att varje grafikobjekt håller sig inom sidans område. Detta är avgörande när du senare försöker rita former som kan spilla över kanterna.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

// Step 1: Initialise a new PDF document
using var document = new Document();

// Step 1b: Turn on boundary checking for all graphics objects
document.FileStructureSettings.CheckGraphicsObjectBoundaries = true;
```

*Varför aktivera gränskontroll?*  
Om du av misstag placerar en rektangel utanför sidan kommer Aspose att kasta ett `PdfException`. Att fånga detta tidigt sparar dig från korrupta PDF‑filer som vissa visare helt enkelt vägrar öppna.

## Steg 2: Lägg till sida i PDF

En PDF utan sidor är som en bok utan blad – ganska värdelös. Att lägga till en sida är så enkelt som att anropa `Pages.Add()`. Metoden returnerar ett `Page`‑objekt som du använder för att placera innehåll på.

```csharp
// Step 2: Add a new page (this is the “add page to pdf” part)
Page page = document.Pages.Add();
```

> **Proffstips:** Standard sidstorlek i Aspose är 595 × 842 punkter (A4). Om du behöver en annan storlek kan du sätta `page.PageInfo.Width` och `page.PageInfo.Height` innan du lägger till innehåll.

## Steg 3: Definiera rektangeln som kommer att ligga utanför gränsen

Nu kommer vi till kärnan i **how to add rectangle pdf**‑objekt. Vi skapar medvetet en rektangel som överskrider sidans dimensioner för att se undantaget i aktion. `Rectangle`‑konstruktorn tar fyra argument: *lower‑left X, lower‑left Y, upper‑right X, upper‑right Y*.

```csharp
// Step 3: Create a rectangle that goes beyond the page edges
// Page size: 595x842, so X=800 and Y=900 are out of bounds
var outOfBoundsRect = new Rectangle(400, 750, 800, 900);
```

Om du kör koden med gränskontrollen avstängd skulle rektangeln helt enkelt klippas. Med kontroll på kommer Aspose att ge ett fel, vilket är precis vad vi vill ha för robusta PDF‑genereringspipelines.

## Steg 4: Bygg formen och ge den en synlig kant

En rektangel i sig är osynlig om du inte lägger till en kant eller fyllning. Här omsluter vi `Rectangle` i ett `Rectangle`‑formobjekt (ja, klassnamnet är lite förvirrande) och tilldelar en tunn svart kant.

```csharp
// Step 4: Turn the rectangle into a shape and add a border
var rectangleShape = new Rectangle(outOfBoundsRect)
{
    Border = new BorderInfo(BorderSide.All, 1f)   // 1‑point black border
};
```

*Varför en kant?*  
Utan en kant ser du ingenting på sidan, vilket gör felsökning svårare. En tunn kant gör också tydligt när formen ligger utanför gränsen.

## Steg 5: Lägg till formen på sidan – förvänta ett undantag

Nu placerar vi faktiskt formen på sidan. Eftersom rektangeln överskrider sidans gränser och vi har slagit på gränskontrollen kommer Aspose att kasta ett `PdfException`. Vi omsluter anropet i ett `try/catch`‑block för att demonstrera elegant felhantering.

```csharp
// Step 5: Attempt to add the shape – this will raise an exception
try
{
    page.Paragraphs.Add(rectangleShape);
}
catch (PdfException ex)
{
    Console.WriteLine("Caught PdfException: " + ex.Message);
    // Handle the error – maybe adjust the rectangle or log the issue
}
```

Om du kommenterar bort raden `CheckGraphicsObjectBoundaries` i Steg 1 kommer koden att lyckas och rektangeln kommer att klippas till sidans kanter. Detta beteende är användbart för snabba prototyper, men i produktion vill du vanligtvis ha säkerhetsnätet på.

## Steg 6: Spara PDF‑filen

Till sist sparar vi dokumentet till disk. Filen skapas i den mapp du anger; se till att sökvägen finns eller använd `Path.Combine` med `Environment.CurrentDirectory`.

```csharp
// Step 6: Save the resulting PDF
string outputPath = Path.Combine(Environment.CurrentDirectory, "checked_shapes.pdf");
document.Save(outputPath);
Console.WriteLine($"PDF saved to {outputPath}");
```

När du öppnar `checked_shapes.pdf` ser du en tom sida (eftersom rektangeln avvisades). Om du tog bort gränskontrollen skulle du se en delvis ritad rektangel som klipps vid högra och övre kanten.

---

![Exempel på att skapa PDF-dokument som visar rektangelgränskontroll](https://example.com/images/checked_shapes.png "Exempel på att skapa PDF-dokument med rektangelgränskontroll")

*Skärmdumpen ovan illustrerar PDF‑filen efter att ha kört handledningen med gränskontrollen avstängd (rektangeln är klippt). Med kontroll på utelämnas formen och ett undantag loggas.*

## Sammanfattning: Fullt fungerande exempel

Sätter vi ihop allt får vi det kompletta, körklara programmet:

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialise document and enable boundary checking
        using var document = new Document();
        document.FileStructureSettings.CheckGraphicsObjectBoundaries = true;

        // 2️⃣ Add a page (add page to pdf)
        Page page = document.Pages.Add();

        // 3️⃣ Define an out‑of‑bounds rectangle (how to add rectangle pdf)
        var outOfBoundsRect = new Rectangle(400, 750, 800, 900);

        // 4️⃣ Create shape with a visible border
        var rectangleShape = new Rectangle(outOfBoundsRect)
        {
            Border = new BorderInfo(BorderSide.All, 1f)
        };

        // 5️⃣ Try to add the shape – expect an exception
        try
        {
            page.Paragraphs.Add(rectangleShape);
        }
        catch (PdfException ex)
        {
            Console.WriteLine("Caught PdfException: " + ex.Message);
        }

        // 6️⃣ Save the PDF
        string outputPath = Path.Combine(Environment.CurrentDirectory, "checked_shapes.pdf");
        document.Save(outputPath);
        Console.WriteLine($"PDF saved to {outputPath}");
    }
}
```

Kör programmet så ser du konsolutdata som bekräftar om undantaget fångades. Öppna den genererade PDF‑filen för att verifiera resultatet.

## Vanliga frågor & kantfall

- **Vad gör jag om jag behöver en annan sidstorlek?**  
  Sätt `page.PageInfo.Width` och `page.PageInfo.Height` innan du lägger till former. Gränskontrollen använder automatiskt de nya dimensionerna.

- **Kan jag inaktivera gränskontrollen för en enskild form?**  
  Inte direkt. Inställningen är global, men du kan tillfälligt stänga av den, lägga till formen och sedan slå på den igen – var medveten om att du då förlorar säkerhetsnätet för just den operationen.

- **Är undantagsmeddelandet hjälpsamt?**  
  Ja, Aspose inkluderar de felande koordinaterna, så du kan programatiskt justera rektangeln eller logga detaljerad diagnostik.

- **Fungerar detta på .NET Core på Linux?**  
  Absolut. Aspose.Pdf är plattformsoberoende; se bara till att de teckensnitt du refererar till finns på mål‑OS‑et.

## Nästa steg

Nu när du vet **how to add rectangle pdf**‑objekt och hur du **add page to pdf**, kanske du vill utforska:

- Att lägga till andra grafiska typer (ellipser, linjer) med samma gränskontroller.
- Att infoga text, bilder eller tabeller – Aspose erbjuder rika API:er för varje.
- Att använda `Document.Save`‑överladdningar för att skriva direkt till en `MemoryStream` för webb‑API:er.

Känn dig fri att experimentera med olika rektangelkoordinater, kanter och fyllningsfärger. Ju mer du leker, desto bättre förstår du hur Aspose.P

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}