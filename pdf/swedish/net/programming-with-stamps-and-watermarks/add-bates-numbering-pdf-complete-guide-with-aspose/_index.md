---
category: general
date: 2026-06-08
description: Lägg till Bates‑nummerering i PDF med Aspose.Pdf i C#. Lär dig hur du
  lägger till Bates, lägger till sidnummer i PDF, lägger till sekventiella nummer
  i PDF, och se ett exempel på Bates‑nummer i PDF.
draft: false
keywords:
- add bates numbering pdf
- how to add bates
- add page numbers pdf
- add sequential numbers pdf
- bates number pdf example
language: sv
og_description: Lägg till Bates‑numrering i PDF med C#. Den här handledningen visar
  hur du lägger till Bates, lägger till sidnummer i PDF och lägger till sekventiella
  nummer i PDF med ett fullständigt exempel på Bates‑nummer i PDF.
og_title: Lägg till Bates‑nummerering i PDF – Komplett guide med Aspose
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Add bates numbering pdf using Aspose.Pdf in C#. Learn how to add bates,
    add page numbers pdf, add sequential numbers pdf, and see a bates number pdf example.
  headline: Add Bates Numbering PDF – Complete Guide with Aspose
  type: TechArticle
- description: Add bates numbering pdf using Aspose.Pdf in C#. Learn how to add bates,
    add page numbers pdf, add sequential numbers pdf, and see a bates number pdf example.
  name: Add Bates Numbering PDF – Complete Guide with Aspose
  steps:
  - name: Install the Aspose.Pdf NuGet Package
    text: 'First, add the library to your project. Open the Package Manager Console
      and run:'
  - name: Open the Source PDF Document
    text: Now we load the PDF we want to stamp. The `using` statement ensures the
      file is closed properly even if an exception occurs.
  - name: Create a Bates Numbering Facade
    text: 'The *facade* pattern hides the complexity of the underlying PDF structure.
      Here’s how we instantiate it:'
  - name: Configure the Starting Number and Prefix
    text: Bates numbers often include a case‑specific prefix. You can also control
      the number of digits, the separator, and the placement on the page.
  - name: Apply the Bates Numbering to the Document
    text: 'With the facade configured, we now stamp every page:'
  - name: Save the Modified PDF
    text: 'Finally, write the output to disk:'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF processing
title: Lägg till Bates‑nummerering i PDF – Komplett guide med Aspose
url: /sv/net/programming-with-stamps-and-watermarks/add-bates-numbering-pdf-complete-guide-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Lägg till Bates‑numrering i PDF – Komplett programmeringsguide

Har du någonsin behövt **add bates numbering pdf** men varit osäker på var du ska börja? Om du någonsin har funderat *hur man lägger till bates* i ett juridiskt dokument, är du på rätt plats. I den här handledningen går vi igenom ett praktiskt, end‑to‑end‑exempel som inte bara lägger till Bates‑nummer utan också visar dig hur du **add page numbers pdf**, **add sequential numbers pdf**, och till och med ger ett färdigt **bates number pdf example**.

Vi kommer att använda Aspose.Pdf‑biblioteket för .NET, eftersom det abstraherar bort de lågnivå PDF‑detaljerna samtidigt som det ger dig fin kontroll. I slutet av den här guiden har du ett återanvändbart kodsnutt som du kan lägga in i vilket C#‑projekt som helst, och du kommer att förstå varför varje rad är viktig.

## Vad du behöver

- **.NET 6.0** eller senare (koden fungerar också på .NET Framework 4.6+).  
- En **licens** för Aspose.Pdf eller en gratis tillfällig utvärderingsnyckel.  
- En exempel‑PDF kallad `input.pdf` placerad i en mapp du kan referera till.  
- Visual Studio, Rider eller någon C#‑redigerare du föredrar.

Det är allt—inga extra verktyg, ingen kommandorads‑gymnastik. Är du redo? Låt oss dyka in.

## Lägg till Bates‑numrering i PDF – Steg‑för‑steg‑implementering

Nedan delar vi upp processen i sex logiska steg. Varje steg innehåller ett kort kodexempel, en förklaring av *varför* vi gör det, och ett tips som kan vara praktiskt.

### Steg 1: Installera Aspose.Pdf NuGet‑paketet

Först, lägg till biblioteket i ditt projekt. Öppna Package Manager Console och kör:

```powershell
Install-Package Aspose.Pdf
```

> **Proffstips:** Om du använder .NET Core kan du också använda `dotnet add package Aspose.Pdf`.

Att installera paketet ger dig tillgång till klassen `Aspose.Pdf.Facades.BatesNumbering`, som är arbetshästen för **add bates numbering pdf**.

### Steg 2: Öppna källdokumentet PDF

Nu laddar vi PDF‑filen som vi vill stämpla. `using`‑satsen säkerställer att filen stängs korrekt även om ett undantag inträffar.

```csharp
using (var doc = new Aspose.Pdf.Document(@"C:\MyPdfs\input.pdf"))
{
    // All further steps happen inside this block.
}
```

Varför använda `Aspose.Pdf.Document`? Den representerar hela PDF‑filen i minnet, vilket låter oss manipulera sidor, teckensnitt och metadata utan att röra den ursprungliga filen på disken.

### Steg 3: Skapa en Bates‑numrerings‑facade

*Facade*-mönstret döljer komplexiteten i den underliggande PDF‑strukturen. Så här instansierar vi den:

```csharp
var bates = new Aspose.Pdf.Facades.BatesNumbering();
```

Detta objekt kommer senare att konfigureras med ett prefix, startnummer och formateringsalternativ. Tänk på det som “motorn” som kommer att **add page numbers pdf** på ett Bates‑kompatibelt sätt.

### Steg 4: Konfigurera startnummer och prefix

Bates‑nummer innehåller ofta ett ärendespecifikt prefix. Du kan också kontrollera antalet siffror, separatorn och placeringen på sidan.

```csharp
bates.StartNumber = 1000;          // First number in the sequence
bates.Prefix = "CASE-";            // Prefix that appears before each number
bates.NumberOfDigits = 5;          // Pads numbers with leading zeros (e.g., 01000)
bates.Separator = "-";             // Optional separator between prefix and number
bates.Location = new Aspose.Pdf.Rectangle(0, 0, 200, 20); // Bottom‑left corner
bates.FontSize = 12;
bates.FontColor = System.Drawing.Color.Blue;
```

**Varför dessa inställningar?**  
- `StartNumber` låter dig fortsätta en tidigare serie.  
- `NumberOfDigits` garanterar enhetlig längd, vilket är avgörande för juridisk indexering.  
- `Location` definierar var **add sequential numbers pdf** kommer att visas; du kan flytta den till övre‑höger om du föredrar.

### Steg 5: Tillämpa Bates‑numrering på dokumentet

Med facaden konfigurerad stämplar vi nu varje sida:

```csharp
bates.AddBatesNumbering(doc);
```

Under huven itererar Aspose genom varje sida, ritar texten på den angivna platsen och respekterar befintligt innehåll. Denna enda rad är det som faktiskt **add bates numbering pdf** till din fil.

### Steg 6: Spara den modifierade PDF‑filen

Till sist skriver vi utdata till disk:

```csharp
doc.Save(@"C:\MyPdfs\output.pdf");
```

Du har nu en PDF där varje sida har en unik Bates‑identifierare, redo för upptäckt eller domstolsinlämning.

#### Fullt fungerande exempel (Bates‑nummer PDF‑exempel)

När vi sätter ihop allt, här är ett komplett, fristående program som du kan kompilera och köra:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Facades;
using System.Drawing; // For Color

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source PDF
        using (var doc = new Document(@"C:\MyPdfs\input.pdf"))
        {
            // 2️⃣ Create the Bates numbering facade
            var bates = new BatesNumbering();

            // 3️⃣ Configure prefix, start number, and formatting
            bates.StartNumber = 1000;
            bates.Prefix = "CASE-";
            bates.NumberOfDigits = 5;
            bates.Separator = "-";
            bates.Location = new Rectangle(0, 0, 200, 20); // Bottom‑left
            bates.FontSize = 12;
            bates.FontColor = Color.Blue;

            // 4️⃣ Apply the numbering to every page
            bates.AddBatesNumbering(doc);

            // 5️⃣ Save the result
            doc.Save(@"C:\MyPdfs\output.pdf");
        }

        Console.WriteLine("Bates numbering added successfully!");
    }
}
```

> **Förväntad output:** Öppna `output.pdf` och du kommer att se “CASE‑01000”, “CASE‑01001”, … längst ner till vänster på varje sida.

![Skärmbild av en PDF‑sida med Bates‑nummer i nedre vänstra hörnet – add bates numbering pdf example](https://example.com/bates-numbering-screenshot.png "add bates numbering pdf example")

*(Bildens alt‑text: *add bates numbering pdf example* – visar Bates‑numren som tillämpats på en exempel‑PDF.)*

## Hur man lägger till Bates – Förstå facaden

Du kanske undrar **how to add bates** utan Aspose‑facaden. Alternativet är att manuellt rita text på varje sida med lågnivå PDF‑operatorer, men den metoden är felbenägen och kräver djup kunskap om PDF‑specifikationen. Facaden abstraherar dessa detaljer, så att du kan fokusera på *vad* du vill (ett prefix, ett startnummer) snarare än *hur* du renderar det.

Om du någonsin behöver **add page numbers pdf** i en icke‑Bates‑stil (t.ex. “Sida 3 av 12”), kan du återanvända samma `BatesNumbering`‑klass—byt bara `Prefix` till en tom sträng och justera `Location`. Den underliggande motorn är densamma, vilket betyder att du får konsekvent rendering i båda fallen.

## Lägg till sidnummer i PDF – Anpassa placering och stil

Juridiska team begär ofta sidnumret i rubriken, medan stödpersonal för rättstvister föredrar det i sidfoten. Här är en snabb justering:

```csharp
bates.Location = new Rectangle(0, doc.Pages[1].PageInfo.Height - 20, 200, 20); // Top‑right
bates.Prefix = "";               // No prefix for plain page numbers
bates.StartNumber = 1;           // Start from 1
bates.NumberOfDigits = 0;        // No padding
bates.FontColor = Color.Black;
```

Samma `AddBatesNumbering`‑anrop kommer nu att **add page numbers pdf** högst upp på varje sida. Eftersom facaden arbetar på dokumentobjektet kan du växla mellan Bates och enkla sidnummer med några egenskapsändringar—ingen behov av att skriva om loopen.

## Lägg till sekventiella nummer i PDF – Avancerad formatering

Anta att du behöver ett format som `2023-CASE-00123`. Du kan kombinera ett datum‑prefix med de befintliga inställningarna:

```csharp
bates.Prefix = $"{DateTime.Now:yyyy}-CASE-";
bates.NumberOfDigits = 5;
bates.Separator = "-";
```

Nu kommer varje sida att visa `2023-CASE-00123`, `2023-CASE-00124`, osv. Detta visar hur enkelt du kan **add sequential numbers pdf** som uppfyller komplexa namngivningskonventioner.

## Edge Cases och vanliga fallgropar

| Situation | Vad du bör vara uppmärksam på | Föreslagen lösning |
|-----------|------------------------------|--------------------|
| **Very large PDFs ( > 500 MB )** | Minnesanvändningen kan öka kraftigt eftersom hela dokumentet laddas in i RAM. | Använd `Document` med `MemoryManagement`‑inställningar eller bearbeta filen i delar med `PdfFileEditor`. |
| **Existing page numbers** |  |  |

## Vad bör du lära dig härnäst?

Följande handledningar täcker närliggande ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Hur man lägger till och anpassar sidnummer i PDF‑filer med Aspose.PDF för .NET \| Dokumentmanipuleringsguide](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [Hur man lägger till sidnummerstämplar i PDF‑filer med Aspose.PDF för .NET \| Vattenstämplar & bakgrunder](/pdf/english/net/watermarks-backgrounds/add-page-number-stamp-using-aspose-pdf-dotnet/)
- [Aspose.PDF .NET: Lägg till sidnummer i PDF‑filer med FloatingBox](/pdf/english/net/text-operations/aspose-pdf-net-floatingbox-page-numbering/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}