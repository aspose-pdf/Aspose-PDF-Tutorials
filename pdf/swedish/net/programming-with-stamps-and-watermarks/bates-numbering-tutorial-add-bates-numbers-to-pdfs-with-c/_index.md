---
category: general
date: 2026-02-25
description: Bates‑numreringshandledning – lär dig hur du lägger till sidnummer i
  PDF och tillämpar anpassad Bates‑numrering med Aspose.Pdf i C#. Steg‑för‑steg‑guide
  med fullständig kod.
draft: false
keywords:
- bates numbering tutorial
- add page numbers pdf
- how to add bates
- add bates numbering
language: sv
og_description: Bates‑numreringshandledning visar hur du lägger till sidnummer i PDF
  och anpassad Bates‑numrering i C#. Komplett kod, förklaringar och tips.
og_title: Bates-nummereringstutorial – Lägg till Bates-nummer i PDF-filer med C#
tags:
- PDF
- C#
- Aspose.Pdf
title: 'Bates‑numreringshandledning: Lägg till Bates‑nummer i PDF‑filer med C#'
url: /sv/net/programming-with-stamps-and-watermarks/bates-numbering-tutorial-add-bates-numbers-to-pdfs-with-c/
---

output.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# bates numbering handledning – Lägga till Bates‑nummer i PDF‑filer i C#

Har du någonsin undrat hur man lägger till sidnummer i en PDF samtidigt som man inbäddar ett juridiskt stilat Bates‑nummer? Du är inte ensam. I den här **bates numbering handledning** går vi igenom allt du behöver veta för att stämpla varje sida i en PDF med ett eget prefix, ledande nollor och exakt positionering—med Aspose.Pdf för .NET.

Den goda nyheten? Det är ganska enkelt när du väl förstår grunderna. I slutet av den här guiden har du ett körbart program som tar *input.pdf* och skapar *bates_out.pdf* med en snygg “ABC‑01000”-etikett på varje sida. Låt oss dyka ner.

## Vad du behöver

- **Aspose.Pdf for .NET** (version 23.10 eller senare). Biblioteket är kommersiellt, men en gratis provperiod fungerar utmärkt för lärande.
- .NET 6+ SDK (vilken recent version som helst räcker).
- En grundläggande C#‑utvecklingsmiljö—Visual Studio, VS Code eller Rider.
- En PDF att experimentera med (vilken flersidig dokument som helst visar effekten).

Inga extra NuGet‑paket utöver Aspose.Pdf behövs, och koden körs på Windows, Linux eller macOS utan modifieringar.

## Steg 1: Ladda källdokumentet PDF (bates numbering handledning – initiering)

Först skapar vi ett `Document`‑objekt som representerar den PDF vi vill modifiera. Tänk på det som att ladda en tom duk som du kan rita på.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Annotations;

// Load the source PDF – replace the path with your actual file location
Document pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");

// Quick sanity check – make sure the document actually has pages
if (pdfDocument.Pages.Count == 0)
{
    throw new InvalidOperationException("The PDF you provided contains no pages.");
}
```

**Varför detta är viktigt:** Utan att ladda filen finns det inget att annotera. Sanity‑checken förhindrar ett tyst fel senare när du försöker lägga till artefakter på en icke‑existerande sidkollektion.

## Steg 2: Definiera Bates‑nummereringsartefakten (hur man lägger till bates)

En *BatesNumberingArtifact* talar om för Aspose var och hur identifieraren ska ritas. Du kan styra prefix, startnummer, nollutfyllnad, teckenstorlek och exakta X/Y‑koordinater.

```csharp
// Configure the Bates numbering artifact
BatesNumberingArtifact batesArtifact = new BatesNumberingArtifact
{
    Prefix = "ABC",          // Text that appears before the number
    Start = 1000,            // First number in the sequence
    LeadingZeros = 5,        // Pad the number with zeros (e.g., 01000)
    FontSize = 9,            // Small enough to sit in the margin
    Position = new Position   // Position measured from the lower‑left corner
    {
        X = 50,               // Horizontal offset (points)
        Y = 30                // Vertical offset (points)
    }
};
```

**Varför detta är viktigt:** `LeadingZeros`‑egenskapen säkerställer att varje etikett har samma längd, vilket är avgörande för juridiska dokument där justering är viktigt. Justera `X` och `Y` för att flytta stämpeln till övre‑höger, nedre‑vänster eller var ditt arbetsflöde kräver.

## Steg 3: Fäst artefakten på varje sida (lägg till sidnummer pdf)

Nu loopar vi igenom varje sida och fäster samma artefakt. Det är här kravet *lägg till sidnummer pdf* uppfylls—varje sida får automatiskt sin egen sekventiella etikett.

```csharp
// Iterate over each page and add the Bates artifact
foreach (Page page in pdfDocument.Pages)
{
    // The artifact is added to the page's Artifacts collection.
    // Aspose will handle the incrementing of the number for us.
    page.Artifacts.Add(batesArtifact);
}
```

**Varför detta är viktigt:** Genom att lägga till artefakten i `Artifacts`‑samlingen istället för att rita text manuellt låter vi Aspose hantera numreringslogiken, ledande nollor och rendering. Detta minskar buggar och håller koden koncis.

## Steg 4: Spara den modifierade PDF‑filen (lägg till bates‑numrering)

Till sist sparar vi förändringarna till en ny fil. Det är en god vana att skriva till ett annat filnamn så att originalet förblir orört.

```csharp
// Save the PDF with Bates numbers applied
pdfDocument.Save("YOUR_DIRECTORY/bates_out.pdf");

// Optional: let the user know we succeeded
Console.WriteLine("Bates numbering applied successfully! Output saved to bates_out.pdf");
```

**Varför detta är viktigt:** `Save`‑metoden skriver hela PDF‑filen och inbäddar artefakterna som en del av sidans innehållsström. Den resulterande filen kan öppnas i vilken PDF‑visare som helst och visar Bates‑numren exakt som specificerat.

## Fullt fungerande exempel (Alla steg kombinerade)

Nedan är det kompletta, körklara programmet. Kopiera‑klistra in det i ett konsol‑app‑projekt, ersätt platshållar‑sökvägarna och tryck **F5**.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the source PDF
            Document pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");
            if (pdfDocument.Pages.Count == 0)
                throw new InvalidOperationException("The PDF you provided contains no pages.");

            // 2️⃣ Configure the Bates numbering artifact
            BatesNumberingArtifact batesArtifact = new BatesNumberingArtifact
            {
                Prefix = "ABC",
                Start = 1000,
                LeadingZeros = 5,
                FontSize = 9,
                Position = new Position { X = 50, Y = 30 }
            };

            // 3️⃣ Attach the artifact to every page
            foreach (Page page in pdfDocument.Pages)
            {
                page.Artifacts.Add(batesArtifact);
            }

            // 4️⃣ Save the modified PDF
            pdfDocument.Save("YOUR_DIRECTORY/bates_out.pdf");
            Console.WriteLine("Bates numbering applied successfully! Output saved to bates_out.pdf");
        }
    }
}
```

### Förväntat resultat

Öppna *bates_out.pdf* i Adobe Reader, Foxit eller någon annan visare. Du bör se en etikett som **ABC‑01000** på första sidan, **ABC‑01001** på den andra och så vidare, placerad 50 pt från vänster kant och 30 pt från botten. Numren är högerjusterade på grund av de ledande nollorna, vilket ger dokumentet ett rent, professionellt utseende.

## Vanliga variationer & kantfall

| Scenario | Hur du justerar |
|----------|-----------------|
| **Annat prefix** | Ändra `Prefix = "XYZ"` i artefaktdefinitionen. |
| **Starta på ett eget nummer** | Sätt `Start = 5000` (eller vilket heltal som helst). |
| **Placera numret i övre‑höger hörnet** | Använd `Position = new Position { X = pdfDocument.PageInfo.Width - 50, Y = pdfDocument.PageInfo.Height - 30 }`. |
| **Ändra teckenstorlek för större dokument** | Modifiera `FontSize = 12` (eller valfri storlek). |
| **Lägg till en bakgrundsrektangel** | Skapa en `RectangleArtifact` och lägg till den före `BatesNumberingArtifact`. |
| **Hoppa över vissa sidor** | Inuti `foreach`‑loopen, lägg till `if (page.Number % 2 == 0) continue;` för att hoppa över jämna sidor. |

**Proffstips:** Testa alltid först med en kort PDF. Det går snabbare att verifiera positionering innan du kör skriptet på ett 200‑sidigt ärende.

## Vanliga frågor

- **Fungerar detta med krypterade PDF‑filer?**  
  Aspose.Pdf kan öppna lösenordsskyddade filer om du anger lösenordet via `Document(string, string)`. Bates‑artefakten appliceras fortfarande efter avkryptering.

- **Kan jag lägga till både Bates‑nummer och vanliga sidnummer?**  
  Ja. Lägg till en `PageNumberArtifact` tillsammans med `BatesNumberingArtifact`. Varje artefakt har sin egen räknare.

- **Vad händer om min PDF har olika sidstorlekar?**  
  `Position`‑värdena är absoluta punkter. För dokument med blandade storlekar, beräkna positionen per sida i loopen med `page.PageInfo.Width` och `page.PageInfo.Height`.

## Nästa steg & relaterade ämnen

Nu när du behärskar **bates numbering handledning** kanske du vill utforska:

- **Lägga till vattenstämplar** – liknande artefakt‑metod med `TextArtifact`.
- **Sammanfoga flera PDF‑filer** – använd `Document.AppendDocument`.
- **Extrahera text för sökindexering** – `TextAbsorber`‑klassen.
- **Automatisera batch‑behandling** – loopa över en mapp med PDF‑filer och applicera samma artefakt.

Alla dessa ämnen bygger på samma koncept du just lärt dig, så du är väl rustad att utöka ditt PDF‑automatiseringsverktyg.

---

*Lycka till med kodandet! Om du stöter på problem eller har idéer för vidare anpassning, lämna gärna en kommentar nedan. PDF‑manipulationens värld är stor, men med en solid **bates numbering handledning** i bagaget ligger du redan steget före.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}