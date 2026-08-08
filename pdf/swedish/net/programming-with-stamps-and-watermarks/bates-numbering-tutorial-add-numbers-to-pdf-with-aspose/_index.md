---
category: general
date: 2026-07-03
description: Bates-nummereringstutorial som visar hur man lägger till Bates-nummerering
  i PDF-filer med Aspose.PDF. Inkluderar inställning av prefix för Bates-nummer och
  ett komplett exempel på Bates-nummerering.
draft: false
keywords:
- bates numbering tutorial
- add bates numbering pdf
- bates numbering example
- prefix bates number
language: sv
og_description: Bates-nummereringstutorial som visar hur du lägger till Bates-nummer
  i PDF-filer, ställer in ett prefix för Bates-nummer och levererar ett fullt fungerande
  exempel.
og_title: 'Bates‑numreringshandledning: Lägg till nummer i PDF med Aspose'
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Bates numbering tutorial showing how to add bates numbering pdf files
    using Aspose.PDF. Includes prefix bates number setup and a complete bates numbering
    example.
  headline: 'Bates Numbering Tutorial: Add Numbers to PDF with Aspose'
  type: TechArticle
- description: Bates numbering tutorial showing how to add bates numbering pdf files
    using Aspose.PDF. Includes prefix bates number setup and a complete bates numbering
    example.
  name: 'Bates Numbering Tutorial: Add Numbers to PDF with Aspose'
  steps:
  - name: What if I need to reset the counter for each section?
    text: You can call `pdfDocument.BatesNumbering.Reset()` before processing a new
      range of pages. Combine it with a loop over `pdfDocument.Pages` and set `Start`
      again for each section.
  - name: How do I apply different prefixes to different page ranges?
    text: 'Create multiple `BatesNumbering` objects—one per range—by cloning the document
      or by using the `Add` method (available in newer Aspose versions). Here’s a
      quick sketch:'
  - name: Does the library support Unicode prefixes?
    text: Absolutely. Pass any Unicode string (e.g., `"案件‑"`). Aspose.PDF handles
      right‑to‑left scripts and special symbols without extra configuration.
  - name: What about PDF security—will Bates numbering break encryption?
    text: If the source PDF is encrypted, you must provide the password before accessing
      `BatesNumbering`. The numbering process respects the original encryption settings—your
      output will stay encrypted unless you explicitly change it.
  type: HowTo
tags:
- Aspose.PDF
- PDF processing
- Bates numbering
title: 'Bates‑numreringshandledning: Lägg till nummer i PDF med Aspose'
url: /sv/net/programming-with-stamps-and-watermarks/bates-numbering-tutorial-add-numbers-to-pdf-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Bates‑nummereringstutorial – Lägg till Bates‑nummer i PDF‑filer med Aspose

Har du någonsin behövt ett **bates numbering tutorial** för att märka tusentals sidor i en rättegång? Du är inte ensam. I många juridiska och efterlevnadsarbetsflöden är ett pålitligt sätt att *add bates numbering pdf* filer ett icke‑förhandlingsbart krav. Lyckligtvis gör Aspose.PDF hela processen till en barnlek, och i den här guiden går vi igenom ett komplett **bates numbering example** som du kan klistra in direkt i ditt projekt.

> **Vad du får:** ett körbart kodexempel som sätter startnumret, applicerar ett **prefix bates number**, och sparar resultatet – allt på under 30 rader C#.

## Förutsättningar

Innan vi dyker ner, se till att du har:

- .NET 6.0 eller senare (API‑et fungerar likadant på .NET Framework 4.6+)
- En giltig Aspose.PDF for .NET‑licens (eller så kan du använda gratis utvärderingsläge)
- En inmatnings‑PDF med namnet `input.pdf` placerad i en mapp du kontrollerar
- Visual Studio 2022 eller någon editor som förstår C#‑projekt

Inga extra NuGet‑paket utöver `Aspose.Pdf` behövs.

## Steg 1: Installera Aspose.PDF för .NET

Öppna din terminal (eller Package Manager Console) och kör:

```bash
dotnet add package Aspose.Pdf
```

Eller, om du föredrar UI, högerklicka **Dependencies → Manage NuGet Packages**, sök efter *Aspose.Pdf* och klicka **Install**. Detta hämtar den senaste stabila versionen (från och med juli 2026, version 23.12).

## Steg 2: Öppna källdokumentet PDF

Den första raden i varje **add bates numbering pdf**‑arbetsflöde är att ladda filen du vill stämpla. Vi omsluter operationen i ett `using`‑block så att dokumentet frigörs automatiskt.

```csharp
using Aspose.Pdf;

// Step 2: Load the PDF you want to number
using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
{
    // Subsequent steps go here...
}
```

> **Proffstips:** Om din PDF finns i en molnbucket kan du mata in ett `Stream` istället för en filsökväg – Aspose.PDF hanterar båda sömlöst.

## Steg 3: Ange startnummer och prefix

Nu kommer hjärtat i **bates numbering example**: att tala om för Aspose var den ska börja och vilken text som ska föregå varje nummer. `BatesNumbering`‑egenskapen exponerar både `Start` och `Prefix`.

```csharp
    // Step 3a: Define where the numbering begins
    pdfDocument.BatesNumbering.Start = 1000;   // you can start anywhere

    // Step 3b: Add a custom prefix – this is the prefix bates number you asked for
    pdfDocument.BatesNumbering.Prefix = "ABC-";
```

Varför bry sig om ett prefix? I många juridiska fall identifierar prefixet ärendefilen, avdelningen eller produktionsbatchen. Med `"ABC-"` som platshållare kan du byta till `"CASE42-"` eller någon annan sträng som passar din namngivningskonvention.

## Steg 4: Välj var numren ska visas (valfritt)

Aspose placerar som standard numret i det nedre högra hörnet, men du kan flytta det var som helst genom att justera `Location`‑egenskapen. Detta steg är inte obligatoriskt för en grundläggande **add bates numbering pdf**‑operation, men det är praktiskt att känna till.

```csharp
    // Optional: Move the number to the top‑left corner
    pdfDocument.BatesNumbering.Location = new Location(10, pdfDocument.Pages[1].PageInfo.Height - 30);
```

`Location` tar X‑ och Y‑koordinater mätta i punkter (1 pt ≈ 1/72 in). Justera efter behov för din sidlayout.

## Steg 5: Spara den uppdaterade PDF‑filen

Till sist, skriv förändringarna till disk. `Save`‑metoden på `BatesNumbering` skapar en ny fil samtidigt som originalet förblir orört.

```csharp
    // Step 5: Write the output file with numbering applied
    pdfDocument.BatesNumbering.Save("YOUR_DIRECTORY/output.pdf");
}
```

När du öppnar `output.pdf` kommer varje sida att visa något i stil med `ABC-1000`, `ABC-1001`, … upp till sista sidan.

## Fullt fungerande exempel

Sätter vi ihop allt får du **bates numbering example** som du kan kopiera‑klistra in i en konsolapps `Main`‑metod:

```csharp
using System;
using Aspose.Pdf;

class Program
{
    static void Main()
    {
        // Path configuration – adjust to your environment
        string inputPath = @"YOUR_DIRECTORY\input.pdf";
        string outputPath = @"YOUR_DIRECTORY\output.pdf";

        // Load the PDF
        using (var pdfDocument = new Document(inputPath))
        {
            // Set start number and prefix
            pdfDocument.BatesNumbering.Start = 1000;
            pdfDocument.BatesNumbering.Prefix = "ABC-";

            // (Optional) Change location – comment out if default is fine
            // pdfDocument.BatesNumbering.Location = new Location(10, pdfDocument.Pages[1].PageInfo.Height - 30);

            // Save the numbered PDF
            pdfDocument.BatesNumbering.Save(outputPath);
        }

        Console.WriteLine($"Bates numbering applied! Check: {outputPath}");
    }
}
```

**Förväntad utskrift** (i konsolen):

```
Bates numbering applied! Check: YOUR_DIRECTORY\output.pdf
```

Öppna den genererade PDF‑filen så ser du sekventiella nummer med prefixet `ABC-` som börjar på `1000`.

## Vanliga frågor & kantfall

### Vad händer om jag måste återställa räknaren för varje avsnitt?

Du kan anropa `pdfDocument.BatesNumbering.Reset()` innan du bearbetar ett nytt sidintervall. Kombinera detta med en loop över `pdfDocument.Pages` och sätt `Start` igen för varje avsnitt.

### Hur applicerar jag olika prefix på olika sidintervall?

Skapa flera `BatesNumbering`‑objekt – ett per intervall – genom att klona dokumentet eller genom att använda `Add`‑metoden (tillgänglig i nyare Aspose‑versioner). Här är ett snabbt exempel:

```csharp
// Number first 10 pages with "PRE‑"
pdfDocument.BatesNumbering.Start = 1;
pdfDocument.BatesNumbering.Prefix = "PRE-";
pdfDocument.BatesNumbering.Save(outputPath, new PageRange(1, 10));

// Number the rest with "POST‑"
pdfDocument.BatesNumbering.Start = 1;
pdfDocument.BatesNumbering.Prefix = "POST-";
pdfDocument.BatesNumbering.Save(outputPath, new PageRange(11, pdfDocument.Pages.Count));
```

### Stöder biblioteket Unicode‑prefix?

Absolut. Skicka vilken Unicode‑sträng som helst (t.ex. `"案件‑"`). Aspose.PDF hanterar höger‑till‑vänster‑skript och specialtecken utan extra konfiguration.

### Vad händer med PDF‑säkerhet – bryter Bates‑numrering kryptering?

Om käll‑PDF‑filen är krypterad måste du ange lösenordet innan du får åtkomst till `BatesNumbering`. Numreringsprocessen respekterar de ursprungliga krypteringsinställningarna – ditt resultat förblir krypterat såvida du inte explicit ändrar det.

```csharp
pdfDocument.Encrypt(new DocumentEncryption("ownerPwd", "userPwd"));
```

## Tips & bästa praxis

- **Batch‑bearbetning:** Omslut hela rutinen i en `foreach`‑loop för att automatiskt hantera dussintals filer.
- **Loggning:** Skriv ut startnummer, prefix och utsökväg till en loggfil; detta underlättar revisionsspår för juridiska team.
- **Prestanda:** För enorma PDF‑filer (500 + sidor) kan du aktivera **memory optimization** via `pdfDocument.OptimizeMemory = true;`.
- **Testning:** Behåll alltid en kopia av original‑PDF‑filen; Bates‑numrering är oåterkallelig när den har sparats.

## Slutsats

I denna **bates numbering tutorial** har vi gått igenom allt du behöver för att **add bates numbering pdf** filer med Aspose.PDF:

1. Installera biblioteket.  
2. Ladda ditt källdokument.  
3. Ange startnummer och ett **prefix bates number**.  
4. (Valfritt) justera placeringen.  
5. Spara resultatet.

Du har nu ett robust **bates numbering example** som du kan anpassa till vilket juridiskt, arkiv‑ eller efterlevnadsarbetsflöde som helst. Vill du gå längre? Prova att kombinera Bates‑nummer med vattenstämplar, eller generera ett CSV‑manifest som mappar varje sida till dess identifierare. Himlen är gränsen, och Aspose ger dig verktygen för att nå dit.

---

*Redo att sätta detta i produktion? Lämna en kommentar om du stöter på problem, och lycka till med kodandet!*

## Vad bör du lära dig härnäst?

De följande tutorialerna täcker närbesläktade ämnen som bygger vidare på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementeringssätt i dina egna projekt.

- [Apply Numbering Style in Heading of PDF using Java](/pdf/english/java/pdf-images/apply-numbering-style-in-heading-of-pdf-using-java/)
- [Aspose Pdf Net Floatingbox Page Numbering](/pdf/german/net/text-operations/aspose-pdf-net-floatingbox-page-numbering/)
- [Apply Numbering Style In Heading Of Pdf Using Java](/pdf/german/java/pdf-images/apply-numbering-style-in-heading-of-pdf-using-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}