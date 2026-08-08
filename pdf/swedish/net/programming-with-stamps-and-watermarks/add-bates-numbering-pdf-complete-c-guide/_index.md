---
category: general
date: 2026-03-22
description: Lägg till Bates‑numrering i PDF snabbt med Aspose.Pdf. Lär dig hur du
  lägger till Bates, sekventiella sidnummer, anpassad sidfot i PDF och artefakter
  i PDF på några minuter.
draft: false
keywords:
- add bates numbering pdf
- how to add bates
- add sequential page numbers
- add custom footer pdf
- add artifact to pdf
language: sv
og_description: Lägg till Bates-numrering i PDF med Aspose.Pdf. Denna guide visar
  hur du lägger till Bates, lägger till sekventiella sidnummer, lägger till anpassad
  sidfot i PDF och lägger till artefakt i PDF.
og_title: Lägg till Bates‑nummerering i PDF – Steg‑för‑steg C#‑handledning
tags:
- Aspose.Pdf
- C#
- PDF automation
title: Lägg till Bates-nummerering i PDF – Komplett C#-guide
url: /sv/net/programming-with-stamps-and-watermarks/add-bates-numbering-pdf-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Lägg till Bates-numrering PDF – Komplett C#-guide

Har du någonsin behövt **add bates numbering pdf** till en batch av juridiska dokument men varit osäker på var du ska börja? Du är inte den första—många utvecklare stöter på samma problem när de bygger ärendehanteringsverktyg. Den goda nyheten? Med Aspose.Pdf kan du **add bates**, **add sequential page numbers** och till och med **add custom footer pdf**‑element med bara några rader kod.  

I den här handledningen går vi igenom hela processen, från att installera biblioteket till att spara den slutliga filen, och vi kommer att strö över tips om hur man **add artifact to pdf**‑filer utan att förstöra befintligt innehåll. I slutet har du ett färdigt kodexempel som du kan klistra in i vilket .NET‑projekt som helst.

## Vad du behöver

- .NET 6+ (koden fungerar på .NET Core och .NET Framework lika bra)  
- En giltig Aspose.Pdf för .NET-licens (du kan börja med en gratis utvärdering)  
- En inmatnings‑PDF (`input.pdf`) placerad i en mapp du kan referera till  
- Visual Studio, Rider eller någon C#‑redigerare du föredrar  

Det är allt—inga extra NuGet‑paket förutom Aspose.Pdf.

## Steg 1: Installera Aspose.Pdf via NuGet

Först och främst—låt oss få biblioteket på din maskin. Öppna en terminal i din projektmapp och kör:

```bash
dotnet add package Aspose.Pdf
```

Eller, om du använder Visual Studios Package Manager Console:

```powershell
Install-Package Aspose.Pdf
```

*Proffstips:* Efter installationen, dubbelkolla att `Aspose.Pdf`‑mappen visas under `Dependencies → Packages` i din lösningsutforskare.

## Steg 2: Ladda källdokumentet PDF

Nu skapar vi ett `Document`‑objekt som representerar den PDF vi vill stämpla. Genom att använda `using`‑satsen säkerställs att filhandtaget släpps automatiskt.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using System.Drawing; // For Color

// Step 2: Load the source PDF
using var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");
```

Varför använda `using var`? Det garanterar att objektet tas bort även om ett undantag uppstår, vilket förhindrar fil‑låsningsproblem senare när du försöker skriva över samma fil.

## Steg 3: Skapa och konfigurera ett Bates‑numrerings‑artifact

Ett Bates‑nummer är i princip ett text‑artifact som finns i PDF:ens logiska struktur. Du kan behandla det som en **custom footer pdf** eftersom det visas på varje sida utan att vara en del av sidans innehållsström.

```csharp
// Step 3: Define the Bates numbering artifact
var batesArtifact = new BatesNumberingArtifact
{
    Prefix = "INV-",          // Optional prefix – change as needed
    Start = 1000,             // Starting number
    Format = "0000",          // Zero‑padded format (e.g., 1000 → 1000)
    X = 500,                  // Horizontal position (points from left)
    Y = 20,                   // Vertical position (points from bottom)
    FontSize = 10,
    FontColor = Color.Black
};
```

### Varför dessa inställningar är viktiga

- **Prefix**: Användbart för att särskilja dokumenttyper (t.ex. “INV‑” för fakturor).  
- **Start**: Anger det första numret; du kan hämta detta från en databas om du behöver kontinuitet mellan filer.  
- **Format**: `"0000"` tvingar en fyrsiffrig visning, vilket säkerställer justering när siffrorna växer.  
- **X/Y**: Koordinaterna mäts från det nedre vänstra hörnet, så `Y = 20` placerar texten precis ovanför sidmarginalen. Justera `X` om du vill ha numret vänsterjusterat eller centrerat.

Om du behöver **add sequential page numbers** istället för Bates‑nummer, utelämna helt enkelt `Prefix` och justera `Format` till `"###"` eller något annat mönster du föredrar.

## Steg 4: Applicera artifact på alla sidor

Aspose.Pdf låter dig bifoga ett artifact till hela dokumentet i ett enda anrop. Detta är det mest effektiva sättet att **add artifact to pdf** utan att loopa igenom varje sida manuellt.

```csharp
// Step 4: Apply the artifact to the whole document
pdfDocument.Pages.AddArtifact(batesArtifact);
```

Bakom kulisserna lägger Aspose till artifactet i sidordlistan för varje sida, vilket innebär att numreringen blir en del av PDF:ens logiska struktur—perfekt för senare extrahering eller sökning.

## Steg 5: Spara den uppdaterade PDF-filen

Till sist skriver du tillbaka ändringarna till disk. Du kan skriva över originalet eller spara till en ny fil; det senare är säkrare under utveckling.

```csharp
// Step 5: Save the PDF with Bates numbers
pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
```

När du öppnar `output.pdf` i en visare kommer du att se “INV‑1000”, “INV‑1001”, … längst ner till höger på varje sida.

### Verifiera resultatet

Öppna PDF-filen i Adobe Acrobat eller någon visare och leta efter siffrorna. Om du behöver bekräfta programatiskt kan du läsa tillbaka artifactet:

```csharp
foreach (var page in pdfDocument.Pages)
{
    foreach (var artifact in page.Artifacts)
    {
        Console.WriteLine($"Page {page.Number}: {artifact.Text}");
    }
}
```

Det kodsnutten skriver ut varje sidas Bates-etikett—praktiskt för automatiserade tester.

## Edge Cases & Vanliga frågor

### Vad händer om min PDF redan har en sidfot?

Att lägga till ett artifact kommer inte att skriva över befintliga sidfötter eftersom artifacts ligger i ett separat lager. Men om den visuella överlappningen är ett problem, justera `Y`‑koordinaten eller öka `X`‑offseten för att flytta Bates-numret åt sidan.

### Kan jag använda ett annat teckensnitt eller färg?

Absolut. `BatesNumberingArtifact` ärver från `Artifact`, så du kan sätta `Font`, `FontColor` och även `Opacity`. Exempel:

```csharp
batesArtifact.Font = FontRepository.FindFont("Arial");
batesArtifact.FontColor = Color.FromArgb(255, 0, 0); // Red
```

### Hur återställer jag räknaren för ett nytt dokument?

Ändra bara `Start` innan du anropar `AddArtifact`. Om du genererar många PDF-filer i en loop, håll en löpande räknare i din applikationslogik.

### Är detta tillvägagångssätt kompatibelt med krypterade PDF-filer?

Aspose.Pdf kan öppna krypterade PDF-filer om du anger lösenordet:

```csharp
var loadOptions = new LoadOptions { Password = "mySecret" };
using var pdfDocument = new Document("encrypted.pdf", loadOptions);
```

Efter dekryptering fungerar samma steg för att lägga till artifact utan problem.

## Fullt fungerande exempel

Nedan är det kompletta, färdiga programmet. Klistra in det i en konsolapp, justera sökvägarna och tryck **F5**.

```csharp
using System;
using System.Drawing;               // For Color
using Aspose.Pdf;
using Aspose.Pdf.Annotations;

class Program
{
    static void Main()
    {
        // Load the source PDF
        using var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");

        // Create the Bates numbering artifact
        var batesArtifact = new BatesNumberingArtifact
        {
            Prefix = "INV-",
            Start = 1000,
            Format = "0000",
            X = 500,
            Y = 20,
            FontSize = 10,
            FontColor = Color.Black
        };

        // Apply the artifact to every page
        pdfDocument.Pages.AddArtifact(batesArtifact);

        // Save the result
        pdfDocument.Save("YOUR_DIRECTORY/output.pdf");

        Console.WriteLine("Bates numbering added successfully!");
    }
}
```

**Förväntad utskrift:** Konsolen skriver “Bates numbering added successfully!” och `output.pdf` innehåller sekventiella etiketter som `INV‑1000`, `INV‑1001` osv., placerade längst ner till höger på varje sida.

## Snabb sammanfattning

- **Primärt mål:** **add bates numbering pdf** med Aspose.Pdf.  
- Vi gick igenom **how to add bates**, **add sequential page numbers** och **add custom footer pdf**‑element via ett enda artifact.  
- Handledningen visade hur man **add artifact to pdf**, hanterar edge cases och verifierar resultatet.  

## Vad blir nästa steg?

- **Dynamiska prefix:** Hämta värden från en databas för att generera “CASE‑2023‑001”, “CASE‑2023‑002”, …  
- **Villkorad placering:** Använd sidstorleksdetektering (`page.MediaBox`) för att centrera siffror på liggande sidor.  
- **Kombinera med vattenstämplar:** Lägg till en halvtransparent logotyp tillsammans med Bates-numret för varumärkesbyggande.  

Känn dig fri att experimentera—kanske upptäcker du ett smartare sätt att batch‑processa tusentals filer. Om du stöter på problem, lämna en kommentar eller kolla Asposes officiella dokumentation (den är förvånansvärt tydlig). Lycka till med kodandet!  

![exempel på add bates numbering pdf](https://example.com/bates-numbering-screenshot.png "Skärmbild som visar add bates numbering pdf i en PDF‑visare")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}