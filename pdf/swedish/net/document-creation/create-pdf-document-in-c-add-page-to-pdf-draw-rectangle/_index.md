---
category: general
date: 2026-03-24
description: Skapa PDF-dokument i C# med Aspose.Pdf – lär dig hur du lägger till en
  sida i PDF, ritar en rektangel och sparar PDF till fil.
draft: false
keywords:
- create pdf document
- add page to pdf
- save pdf to file
- how to create pdf
- how to add rectangle
language: sv
og_description: Skapa PDF-dokument i C# med Aspose.Pdf. Lär dig hur du lägger till
  en sida i PDF, ritar en rektangel och sparar PDF till fil i några enkla steg.
og_title: Skapa PDF-dokument i C# – Lägg till sida i PDF & rita rektangel
tags:
- pdf
- csharp
- aspose
title: Skapa PDF-dokument i C# – Lägg till sida i PDF och rita rektangel
url: /sv/net/document-creation/create-pdf-document-in-c-add-page-to-pdf-draw-rectangle/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa PDF-dokument i C# – Lägg till sida i PDF & rita rektangel

Har du någonsin behövt **skapa pdf-dokument** i C# men inte vetat var du ska börja? Du är inte ensam – de flesta utvecklare stöter på den muren när de första gången tar sig an programmatisk PDF‑generering. Den goda nyheten är att med Aspose.Pdf kan du snabbt skapa en PDF, **lägga till sida i pdf**, placera en rektangel på den och sedan **spara pdf till fil** med bara några få rader kod.

I den här handledningen går vi igenom hela processen, från att initiera dokumentet till att lagra det på disk. När du är klar vet du **hur man skapar pdf**‑filer i farten, **hur man lägger till rektangel**‑former och exakt var filen hamnar på ditt system.

## Vad du kommer att lära dig

- Hur du **skapar pdf-dokument** med Aspose.Pdf:s `Document`‑klass.  
- Det korrekta sättet att **lägga till sida i pdf** utan att trigga layoutfel.  
- Steg‑för‑steg‑instruktioner för **hur man lägger till rektangel** på en sida.  
- Den säkraste metoden för att **spara pdf till fil** och hantera vanliga fallgropar.  

Inga avancerade förutsättningar – bara en .NET‑utvecklingsmiljö och Aspose.Pdf för .NET‑paketet från NuGet.

## Förutsättningar

- .NET 6.0 eller senare (koden fungerar även på .NET Framework 4.7+).  
- Visual Studio 2022 eller någon C#‑kompatibel IDE.  
- Aspose.Pdf för .NET installerat (`dotnet add package Aspose.Pdf`).  

Om du har detta, låt oss dyka ner.

## Skapa PDF-dokument – Översikt

Det första du måste göra är att instansiera `Document`‑objektet. Tänk på det som en tom duk som väntar på sidor, text, bilder eller former.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

// Step 1: Create a new PDF document in memory
using var pdfDocument = new Document();
```

Varför använda `using var`? Det garanterar att de underliggande filströmmarna tas bort automatiskt, vilket förhindrar fil‑låsningsbuggar senare när du försöker **spara pdf till fil**.

## Lägg till sida i PDF

En PDF utan sidor är i princip ett tomt skal. Att lägga till en sida är så enkelt som att anropa `Pages.Add()`. Metoden returnerar ett `Page`‑objekt som du omedelbart kan börja arbeta med.

```csharp
// Step 2: Add a blank page to the document
var pdfPage = pdfDocument.Pages.Add();
```

**Proffstips:** Standard sidstorlek är A4 (595 × 842 punkter). Om du behöver en annan storlek, skicka en `PageSize`‑enum eller egna dimensioner till `Add()`.

```csharp
// Example: Add a Letter‑sized page
var letterPage = pdfDocument.Pages.Add(PageSize.Letter);
```

## Hur man lägger till rektangel i en PDF‑sida

Nu till den roliga delen – att rita en rektangel. Aspose.Pdf:s `Rectangle`‑klass förväntar sig koordinaterna för det nedre vänstra hörnet följt av bredd och höjd. Dessa värden mäts i punkter (1 pt ≈ 1/72 tum).

```csharp
// Step 3: Insert a rectangle shape onto the page
// Lower‑left corner at (0,0), width 600 pt, height 800 pt
pdfPage.Paragraphs.Add(new Rectangle(0, 0, 600, 800));
```

### Varför de siffrorna spelar roll

- **(0,0)** placerar rektangeln längst ner till vänster på sidan.  
- **600 × 800** får plats bekvämt på en A4‑sida (som är 595 × 842).  
- Om rektangeln överskrider sidans gränser kastar Aspose ett undantag – så verifiera alltid dimensionerna, särskilt när du byter sidstorlek.

### Anpassa rektangeln

Du kan ändra linjestil, färg och fyllning:

```csharp
var rect = new Rectangle(50, 700, 200, 100)
{
    Border = new BorderInfo(BorderSide.All, .5f, Color.Black),
    FillColor = Color.LightGray
};
pdfPage.Paragraphs.Add(rect);
```

Det här kodsnutten ritar en rektangel på 200 × 100 pt, förskjuten 50 pt från vänster och 700 pt från botten, med en tunn svart kantlinje och en ljusgrå fyllning.

## Spara PDF till fil

När din sida ser ut som du vill är det sista steget att lagra filen. `Save`‑metoden accepterar en filsökväg, en `Stream` eller till och med en `MemoryStream` om du föredrar att skicka PDF‑filen över ett nätverk.

```csharp
// Step 4: Save the PDF to a file on disk
pdfDocument.Save("C:\\Temp\\output.pdf");
```

**Kom ihåg:** När du kör detta på Linux, använd framåtsnedstreck (`/`) eller `Path.Combine` för att undvika problem med sökvägsseparatorer.

### Hantera undantag

Sparandet kan misslyckas av orsaker som otillräckliga skrivbehörigheter eller en befintlig skrivskyddad fil. Omslut anropet med en try/catch‑block för att få fram hjälpsam diagnostik:

```csharp
try
{
    pdfDocument.Save("C:\\Temp\\output.pdf");
}
catch (IOException ex)
{
    Console.WriteLine($"Unable to write file: {ex.Message}");
}
```

## Fullt fungerande exempel

Nedan är ett självständigt program som du kan kopiera‑klistra in i en konsolapp. Det demonstrerar **hur man skapar pdf**, **lägger till sida i pdf**, **hur man lägger till rektangel** och **sparar pdf till fil** – allt i ett svep.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using System.Drawing; // For Color struct

class Program
{
    static void Main()
    {
        // 1️⃣ Create the PDF document
        using var pdfDocument = new Document();

        // 2️⃣ Add a new page (default A4)
        var page = pdfDocument.Pages.Add();

        // 3️⃣ Draw a rectangle – fits inside the page
        var rect = new Rectangle(0, 0, 600, 800)
        {
            Border = new BorderInfo(BorderSide.All, 1.0f, Color.Blue),
            FillColor = Color.AliceBlue
        };
        page.Paragraphs.Add(rect);

        // 4️⃣ Persist the PDF to disk
        const string outputPath = "output.pdf";
        try
        {
            pdfDocument.Save(outputPath);
            Console.WriteLine($"PDF successfully saved to {outputPath}");
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Error saving PDF: {ex.Message}");
        }
    }
}
```

**Förväntat resultat:** Öppna `output.pdf` så ser du en enda A4‑sida med en blåkantad, ljusblå rektangel förankrad i det nedre vänstra hörnet. Ingen text behövs; rektangeln i sig bevisar att formen lades till korrekt.

## Vanliga fallgropar & tips

| Problem | Varför det händer | Så fixar du det |
|-------|----------------|---------------|
| **Rektangeln överskrider sidstorlek** | Koordinater eller dimensioner som är större än sidans mått ger ett `ArgumentException`. | Dubbelkolla sidstorleken (`page.PageInfo.Width`, `.Height`) innan du ritar. |
| **Sökvägen är inte skrivbar** | Körs under ett begränsat användarkonto eller försöker skriva till en skyddad mapp. | Använd en skrivbar katalog som `%TEMP%` eller `Environment.GetFolderPath(Environment.SpecialFolder.Desktop)`. |
| **Glömt att disponera** | Att inte disponera `Document` kan låsa filen tills processen avslutas. | Använd `using var` eller anropa explicit `pdfDocument.Dispose()`. |
| **Saknar Aspose.Pdf‑referens** | NuGet‑paketet är inte installerat eller projektet riktar mot ett inkompatibelt ramverk. | Kör `dotnet add package Aspose.Pdf` och säkerställ att ditt mål‑ramverk stöds. |

### Edge Cases

- **Flera sidor:** Anropa `pdfDocument.Pages.Add()` för varje extra sida och lägg sedan till former på respektive `Page`‑objekt.  
- **Dynamiska dimensioner:** Om du vill att rektangeln ska fylla hela sidan, använd `page.PageInfo.Width` och `page.PageInfo.Height` för bredd/höjd.  
- **Strömning till en webbklient:** Ersätt `pdfDocument.Save(filePath)` med `pdfDocument.Save(stream, SaveFormat.Pdf)` och skriv strömmen till HTTP‑svaret.

## Nästa steg

Nu när du vet **hur man skapar pdf**, fundera på att utöka dokumentet:

- Lägg till text med `TextFragment`.  
- Infoga bilder via `Image`‑klassen.  
- Generera tabeller för fakturor eller rapporter.  

Alla dessa följer samma mönster: skapa ett objekt, konfigurera dess egenskaper och lägg till det i `page.Paragraphs`.

Om du är nyfiken på mer avancerad formatering – som gradienter, rotationer eller PDF‑kryptering – kolla in Asposes officiella dokumentation eller “Advanced PDF Manipulation”-handledningsserien.

## Slutsats

Vi har gått igenom allt du behöver för att **skapa pdf-dokument** i C# med Aspose.Pdf: initiera dokumentet, **lägga till sida i pdf**, rita en rektangel med **hur man lägger till rektangel**, och slutligen **spara pdf till fil**. Det kompletta exemplet körs direkt, och tipsen ovan bör hålla dig borta från de vanligaste huvudvärken.

Ge det

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}