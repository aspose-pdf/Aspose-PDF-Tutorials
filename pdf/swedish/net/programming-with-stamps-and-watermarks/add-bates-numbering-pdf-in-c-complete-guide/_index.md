---
category: general
date: 2026-05-27
description: Lägg till Bates‑nummerering i PDF med Aspose.Pdf i C#. Lär dig hur du
  snabbt lägger till Bates‑nummerering, anpassar formatet och automatiserar märkning
  av juridiska dokument.
draft: false
keywords:
- add bates numbering pdf
- how to add bates numbering
language: sv
og_description: Lägg till Bates-numrering i PDF med Aspose.Pdf i C#. Denna guide visar
  hur du lägger till Bates-numrering, konfigurerar prefix och sparar resultatet.
og_title: Lägg till Bates‑nummerering i PDF med C# – Steg‑för‑steg‑handledning
schemas:
- author: Aspose
  dateModified: '2026-05-27'
  description: Add Bates numbering PDF using Aspose.Pdf in C#. Learn how to add Bates
    numbering quickly, customize format, and automate legal document tagging.
  headline: Add Bates Numbering PDF in C# – Complete Guide
  type: TechArticle
- description: Add Bates numbering PDF using Aspose.Pdf in C#. Learn how to add Bates
    numbering quickly, customize format, and automate legal document tagging.
  name: Add Bates Numbering PDF in C# – Complete Guide
  steps:
  - name: Expected Output
    text: 'When you run the program, the console prints:'
  - name: Can I position the Bates number elsewhere?
    text: Yes. Use the `BatesNumberingArtifact`’s `Location` property (e.g., `Location
      = new Position(10, 10)`) to place the number at custom X/Y coordinates. You
      can also set `HorizontalAlignment` and `VerticalAlignment` for more control.
  - name: What if my PDF has thousands of pages?
    text: Aspose.Pdf streams pages efficiently, but it’s still a good idea to process
      in batches if you hit memory limits. The `Document` class also supports `PdfConverter`
      for incremental saving.
  - name: How do I change the font or color?
    text: 'Wrap the artifact in a `TextState` object:'
  - name: Do I need a license for production use?
    text: A licensed version removes evaluation watermarks and unlocks full performance.
      The free trial works fine for testing and proof‑of‑concepts.
  type: HowTo
tags:
- Aspose.Pdf
- C#
- Bates numbering
- PDF automation
title: Lägg till Bates-nummerering i PDF med C# – Komplett guide
url: /sv/net/programming-with-stamps-and-watermarks/add-bates-numbering-pdf-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Lägg till Bates-nummerering i PDF med C# – Komplett guide

Har du någonsin undrat **hur man lägger till Bates-nummerering** i en PDF utan att spendera timmar på manuella verktyg? Du är inte ensam—juridiska team, revisorer och e‑discovery‑specialister behöver alla ett pålitligt sätt att **lägga till Bates-nummerering i PDF**‑filer programmässigt.  

I den här handledningen går vi igenom en kortfattad, end‑to‑end‑lösning med Aspose.Pdf för .NET, så att du kan lägga till Bates‑nummer på vilket dokument som helst med bara några rader C#‑kod.

## Vad du kommer att lära dig

- Hur man öppnar en befintlig PDF med Aspose.Pdf  
- Hur man skapar ett Bates‑nummererings‑artefakt och finjusterar dess format  
- Hur man bifogar artefakten till varje sida (eller bara den första)  
- Hur man sparar den uppdaterade filen och verifierar resultatet  

Ingen tidigare erfarenhet av Aspose krävs—bara en grundläggande förståelse för C# och .NET. I slutet har du ett återanvändbart kodsnutt som du kan kopiera‑klistra in i vilket projekt som helst.

## Förutsättningar

- .NET 6.0 eller senare (koden fungerar också på .NET Framework 4.7+)
- Aspose.Pdf for .NET NuGet‑paket (`Install-Package Aspose.Pdf`)
- En käll‑PDF‑fil som du vill märka (placera den i en mapp du kan referera till)

> **Proffstips:** Om du ännu inte har en licens erbjuder Aspose en gratis temporär nyckel som tar bort utvärderingsvattenstämplar.

## Steg 1 – Öppna käll‑PDF‑dokumentet  

Först behöver vi ett `Document`‑objekt som representerar filen på disken. Tänk på detta som att ladda en tom duk som vi senare ska måla Bates‑nummer på.

```csharp
using Aspose.Pdf;
using System;

class Program
{
    static void Main()
    {
        // Adjust the path to point at your source PDF
        string sourcePath = @"C:\Docs\source.pdf";

        // Load the PDF – this is where we start to add Bates numbering
        using (var pdfDocument = new Document(sourcePath))
        {
            // The rest of the logic lives inside this using block
        }
    }
}
```

**Varför detta är viktigt:** Att öppna dokumentet inom ett `using`‑block säkerställer att alla ohanterade resurser frigörs omedelbart, vilket är särskilt viktigt för stora PDF‑filer.

## Steg 2 – Skapa ett Bates‑nummererings‑artefakt  

Ett *BatesNumberingArtifact* är Asposes sätt att beskriva hur siffrorna ska se ut. Du kan ange ett prefix, startnummer, inkrement och till och med en anpassad formatsträng.

```csharp
// Step 2: Define the Bates numbering artifact
var batesNumbering = new BatesNumberingArtifact
{
    Prefix = "ABC",            // Text that appears before each number
    StartNumber = 1000,        // First number in the sequence
    Increment = 1,             // Step between consecutive numbers
    Format = "{0:D5}"          // Zero‑padded 5‑digit number (e.g., 01000)
};
```

**Varför du kanske vill ändra dessa värden:**  
- **Prefix** är användbart för ärende‑ID:n (“CASE‑”, “DOC‑”).  
- **StartNumber** låter dig fortsätta en tidigare serie.  
- **Increment** kan sättas till 2 om du behöver udda/jämna nummer.  
- **Format** stöder vilket .NET‑kompositformat som helst; `{0:D5}` garanterar fem siffror med inledande nollor.

## Steg 3 – Bifoga artefakten till önskade sidor  

Du kan lägga till artefakten på en enskild sida, ett intervall eller hela dokumentet. För de flesta juridiska arbetsflöden bifogar vi den till *varje* sida, men exemplet nedan visar det minimala fallet—att lägga till den på den första sidan.

```csharp
// Step 3: Attach the artifact to the first page (index is 1‑based)
pdfDocument.Pages[1].Artifacts.Add(batesNumbering);
```

Om du behöver täcka alla sidor, loopa igenom dem:

```csharp
foreach (Page page in pdfDocument.Pages)
{
    page.Artifacts.Add(batesNumbering);
}
```

**Varför detta steg är avgörande:** Artefakter renderas *efter* sidans innehåll, så siffrorna visas ovanpå befintlig text utan att ändra den ursprungliga layouten.

## Steg 4 – Spara den modifierade PDF‑filen  

Till sist skriver vi tillbaka ändringarna till disken. Du kan skriva över originalet eller skapa en ny fil—här genererar vi en färsk kopia som heter `bates.pdf`.

```csharp
// Step 4: Persist the changes
string outputPath = @"C:\Docs\bates.pdf";
pdfDocument.Save(outputPath);

Console.WriteLine($"Bates numbering added successfully. File saved to: {outputPath}");
```

När du öppnar `bates.pdf` ser du “ABC01000” (eller vilket format du valt) stämplat på standardplatsen—vanligtvis längst ner till höger.

## Fullt fungerande exempel  

Sätter vi ihop allt får du det kompletta programmet som du kan kompilera och köra:

```csharp
using Aspose.Pdf;
using System;

class AddBatesNumbering
{
    static void Main()
    {
        // -----------------------------------------------------------------
        // 1️⃣ Open the source PDF
        // -----------------------------------------------------------------
        string sourcePath = @"C:\Docs\source.pdf";
        using (var pdfDocument = new Document(sourcePath))
        {
            // -----------------------------------------------------------------
            // 2️⃣ Create and configure the Bates numbering artifact
            // -----------------------------------------------------------------
            var batesNumbering = new BatesNumberingArtifact
            {
                Prefix = "ABC",
                StartNumber = 1000,
                Increment = 1,
                Format = "{0:D5}"
            };

            // -----------------------------------------------------------------
            // 3️⃣ Attach the artifact to each page (or a specific page)
            // -----------------------------------------------------------------
            foreach (Page page in pdfDocument.Pages)
            {
                page.Artifacts.Add(batesNumbering);
            }

            // -----------------------------------------------------------------
            // 4️⃣ Save the new PDF
            // -----------------------------------------------------------------
            string outputPath = @"C:\Docs\bates.pdf";
            pdfDocument.Save(outputPath);

            Console.WriteLine($"Bates numbers added. Output: {outputPath}");
        }
    }
}
```

### Förväntad utskrift

När du kör programmet skriver konsolen ut:

```
Bates numbers added. Output: C:\Docs\bates.pdf
```

Att öppna `bates.pdf` visar prefixet “ABC” följt av en nollutfylld femsiffrig sekvens på varje sida—precis vad du bad koden göra.

## Vanliga frågor & kantfall

### Kan jag placera Bates‑numret någon annanstans?

Ja. Använd `BatesNumberingArtifact`‑s `Location`‑egenskap (t.ex. `Location = new Position(10, 10)`) för att placera numret på anpassade X/Y‑koordinater. Du kan också sätta `HorizontalAlignment` och `VerticalAlignment` för mer kontroll.

### Vad händer om min PDF har tusentals sidor?

Aspose.Pdf strömmar sidor effektivt, men det är fortfarande en bra idé att bearbeta i batcher om du når minnesgränser. `Document`‑klassen stödjer också `PdfConverter` för inkrementell sparning.

### Hur ändrar jag teckensnitt eller färg?

Bunta in artefakten i ett `TextState`‑objekt:

```csharp
batesNumbering.TextState = new TextState
{
    FontSize = 12,
    Font = FontRepository.FindFont("Arial"),
    ForegroundColor = Color.FromRgb(255, 0, 0) // red
};
```

### Behöver jag en licens för produktionsbruk?

En licensierad version tar bort utvärderingsvattenstämplar och låser upp full prestanda. Gratisprovversionen fungerar bra för testning och proof‑of‑concepts.

## Verifiering – Snabb visuell kontroll  

Om du föredrar en automatiserad verifiering kan Aspose extrahera texten från en sida och bekräfta att prefixet finns:

```csharp
string pageText = pdfDocument.Pages[1].ExtractText();
bool hasBates = pageText.Contains("ABC01000");
Console.WriteLine(hasBates ? "Bates number verified." : "Number missing!");
```

Att köra detta efter sparsteget skriver ut `Bates number verified.` om allt gick smidigt.

## Slutsats  

Du vet nu **hur man lägger till Bates‑nummerering i PDF**‑filer med Aspose.Pdf i C#. Från att öppna dokumentet till att konfigurera artefakten, bifoga den till sidor och spara resultatet är processen enkel och helt skriptbar.  

Nästa steg? Prova att experimentera med:

- Olika `Prefix`‑värden för flera ärende‑batchar  
- Anpassad `Location` och `TextState` för varumärkesprofilering  
- Lägga till sid‑specifika prefix (t.ex. “VOL‑1‑”, “VOL‑2‑”) genom att justera `StartNumber` per loop‑iteration  

Dessa justeringar låter dig anpassa lösningen till nästan alla juridiska eller arkiveringsarbetsflöden.  

Har du fler frågor om **hur man lägger till Bates‑nummerering** för flerspråkiga PDF‑filer eller krypterade filer? Lägg en kommentar nedan, och lycka till med kodningen!

## Relaterade handledningar

- [Hur man lägger till och anpassar sidnummer i PDF‑filer med Aspose.PDF för .NET | Dokumentmanipuleringsguide](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [Hur man lägger till olika rubriker i PDF med Aspose.PDF för .NET: En steg‑för‑steg‑guide](/pdf/english/net/document-manipulation/add-different-headers-aspose-pdf-net/)
- [Hur man lägger till en textstämpelfot i PDF med Aspose.PDF för .NET: En steg‑för‑steg‑guide](/pdf/english/net/document-manipulation/add-text-stamp-footer-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}