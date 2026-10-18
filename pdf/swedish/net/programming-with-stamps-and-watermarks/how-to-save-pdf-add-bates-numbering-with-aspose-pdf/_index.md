---
category: general
date: 2026-02-23
description: Hur man sparar PDF‑filer samtidigt som man lägger till Bates‑nummerering
  och artefakter med Aspose.Pdf i C#. Steg‑för‑steg‑guide för utvecklare.
draft: false
keywords:
- how to save pdf
- how to add bates
- how to add artifact
- create pdf document
- add bates numbering
language: sv
og_description: Hur man sparar PDF-filer samtidigt som man lägger till Bates‑nummerering
  och artefakter med Aspose.Pdf i C#. Lär dig den kompletta lösningen på några minuter.
og_title: Hur man sparar PDF — Lägg till Bates-nummerering med Aspose.Pdf
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Hur man sparar PDF — Lägg till Bates‑nummerering med Aspose.Pdf
url: /sv/net/programming-with-stamps-and-watermarks/how-to-save-pdf-add-bates-numbering-with-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man sparar PDF — Lägg till Bates‑numrering med Aspose.Pdf

Har du någonsin undrat **how to save PDF** filer efter att du har stämplat dem med ett Bates‑nummer? Du är inte ensam. På juridiska firmor, domstolar och även interna efterlevnadsteam är behovet av att bädda in en unik identifierare på varje sida ett dagligt problem. De goda nyheterna? Med Aspose.Pdf för .NET kan du göra det på några få rader, och du får en perfekt sparad PDF som bär den numrering du kräver.

I den här handledningen går vi igenom hela processen: läsa in en befintlig PDF, lägga till ett Bates‑nummer *artifact*, och slutligen **how to save PDF** till en ny plats. På vägen kommer vi också att beröra **how to add bates**, **how to add artifact**, och till och med diskutera det bredare ämnet **create PDF document** programatiskt. I slutet har du ett återanvändbart kodsnutt som du kan klistra in i vilket C#‑projekt som helst.

## Förutsättningar

- .NET 6.0 eller senare (koden fungerar även med .NET Framework 4.6+)
- Aspose.Pdf för .NET NuGet‑paket (`Install-Package Aspose.Pdf`)
- En exempel‑PDF (`input.pdf`) placerad i en mapp du kan läsa/skriva till
- Grundläggande kunskap om C#‑syntax — ingen djup PDF‑kunskap krävs

> **Pro tip:** Om du använder Visual Studio, aktivera *nullable reference types* för en renare kompileringstidupplevelse.

---

## Så sparar du PDF med Bates‑numrering

Kärnan i lösningen består av tre enkla steg. Varje steg är inramat i sin egen H2‑rubrik så att du kan hoppa direkt till den del du behöver.

### Steg 1 – Läs in källdokumentet PDF

Först måste vi läsa in filen i minnet. Aspose.Pdf:s `Document`‑class representerar hela PDF‑filen, och du kan instansiera den direkt från en filsökväg.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Artifacts;
using Aspose.Pdf.Text;

namespace BatesNumberDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 👉 Step 1: Load the source PDF document
            string inputPdfPath = @"C:\MyDocs\input.pdf";

            // The Document constructor throws if the file is missing, so wrap it in a try/catch if you need resilience.
            using (var pdfDocument = new Document(inputPdfPath))
            {
                // The rest of the workflow continues inside this using block.
```

**Varför detta är viktigt:** Att läsa in filen är den enda punkt där I/O kan misslyckas. Genom att behålla `using`‑satsen säkerställer vi att filhandtaget frigörs omedelbart — avgörande när du senare **how to save pdf** tillbaka till disk.

### Steg 2 – Hur man lägger till Bates‑numrerings‑artifact

Bates‑nummer placeras vanligtvis i sidhuvudet eller sidfoten på varje sida. Aspose.Pdf tillhandahåller klassen `BatesNumberArtifact`, som automatiskt ökar numret för varje sida du lägger till den på.

```csharp
                // 👉 Step 2: Add a Bates number artifact to the first page (you could loop for all pages)
                var batesArtifact = new BatesNumberArtifact
                {
                    // The Text property can contain a format string. "{0}" will be replaced by the page number.
                    Text = "Case-2026-{0}",
                    Position = new Position(50, 50), // X=50pt, Y=50pt from the bottom‑left corner
                    Font = FontRepository.FindFont("Helvetica"),
                    FontSize = 12,
                    // Optional: set color, opacity, etc.
                };

                // Attach the artifact to the first page; Aspose will replicate it on subsequent pages automatically.
                pdfDocument.Pages[1].Artifacts.Add(batesArtifact);
```

**How to add bates** över hela dokumentet? Om du vill ha artifact på *varje* sida, lägg helt enkelt till den på den första sidan som visas — Aspose hanterar spridningen. För mer fin kontroll kan du iterera `pdfDocument.Pages` och lägga till ett anpassat `TextFragment` istället, men den inbyggda artifact är den mest koncisa.

### Steg 3 – Hur man sparar PDF till en ny plats

Nu när PDF‑filen har Bates‑numret är det dags att skriva ut den. Det är här huvudnyckelordet återigen kommer till sin rätt: **how to save pdf** efter modifieringar.

```csharp
                // 👉 Step 3: Save the updated PDF to the desired location
                string outputPdfPath = @"C:\MyDocs\output.pdf";

                // Overwrite if the file already exists; you can also check File.Exists first.
                pdfDocument.Save(outputPdfPath);
                Console.WriteLine($"PDF saved successfully to {outputPdfPath}");
            } // using block disposes the Document
        }
    }
}
```

När `Save`‑metoden är klar innehåller filen på disken Bates‑numret på varje sida, och du har precis lärt dig **how to save pdf** med en artifact bifogad.

---

## Hur man lägger till artifact i en PDF (utöver Bates)

Ibland behöver du ett generiskt vattenstämpel, en logotyp eller en anpassad notering istället för ett Bates‑nummer. Samma `Artifacts`‑samling fungerar för vilket visuellt element som helst.

```csharp
// Example: Adding a simple text watermark artifact
var watermark = new TextArtifact
{
    Text = "CONFIDENTIAL",
    Position = new Position(200, 400),
    Font = FontRepository.FindFont("Arial"),
    FontSize = 36,
    Color = Color.FromRgb(255, 0, 0),
    Opacity = 0.3
};
pdfDocument.Pages[1].Artifacts.Add(watermark);
```

**Why use an artifact?** Artifacts är *non‑content*‑objekt, vilket betyder att de inte stör textutdragning eller PDF‑tillgänglighetsfunktioner. Det är därför de är det föredragna sättet att bädda in Bates‑nummer, vattenstämplar eller någon överlagring som ska förbli osynlig för sökmotorer.

## Skapa PDF‑dokument från grunden (om du inte har någon indata)

De föregående stegen förutsatte en befintlig fil, men ibland behöver du **create PDF document** från grunden innan du kan **add bates numbering**. Här är en minimalistisk start:

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Create a fresh PDF document
var newDoc = new Document();
Page page = newDoc.Pages.Add();

// Add a simple paragraph
var paragraph = new TextFragment("Hello, this is a newly created PDF.");
page.Paragraphs.Add(paragraph);

// Save it
newDoc.Save(@"C:\MyDocs\newfile.pdf");
```

Härifrån kan du återanvända *how to add bates*-snutten och *how to save pdf*-rutinen för att förvandla en tom duk till ett fullt märkt juridiskt dokument.

## Vanliga kantfall & tips

| Situation | Vad att hålla utkik efter | Föreslagen lösning |
|-----------|---------------------------|--------------------|
| **Inmatnings‑PDF har inga sidor** | `pdfDocument.Pages[1]` kastar ett out‑of‑range‑undantag. | Verifiera `pdfDocument.Pages.Count > 0` innan du lägger till artifacts, eller skapa en ny sida först. |
| **Flera sidor behöver olika positioner** | En artifact tillämpar samma koordinater på varje sida. | Loopa igenom `pdfDocument.Pages` och sätt `Artifacts.Add` per sida med en anpassad `Position`. |
| **Stora PDF‑filer (hundratals MB)** | Minnetryck när dokumentet ligger i RAM. | Använd `PdfFileEditor` för modifieringar på plats, eller bearbeta sidor i batcher. |
| **Anpassat Bates‑format** | Vill ha ett prefix, suffix eller nollutfyllda nummer. | Sätt `Text = "DOC-{0:0000}"` – `{0}`‑platshållaren respekterar .NET‑formatsträngar. |
| **Spara till en skrivskyddad mapp** | `Save` kastar ett `UnauthorizedAccessException`. | Säkerställ att mål katalogen har skrivrättigheter, eller be användaren om en alternativ sökväg. |

## Förväntat resultat

Efter att ha kört hela programmet:

1. `output.pdf` visas i `C:\MyDocs\`.
2. När du öppnar den i någon PDF‑visare visas texten **“Case-2026-1”**, **“Case-2026-2”** osv., placerad 50 pt från vänster- och bottenkanten på varje sida.
3. Om du lade till den valfria vattenstämpel‑artifacten, visas ordet **“CONFIDENTIAL”** halvtransparent över innehållet.

Du kan verifiera Bates‑numren genom att markera texten (de är markerbara eftersom de är artifacts) eller genom att använda ett PDF‑inspektionsverktyg.

## Sammanfattning – Så sparar du PDF med Bates‑numrering på ett svep

- **Load** källfilen med `new Document(path)`.
- **Add** en `BatesNumberArtifact` (eller någon annan artifact) till den första sidan.
- **Save** det modifierade dokumentet med `pdfDocument.Save(destinationPath)`.

Det är hela svaret på **how to save pdf** samtidigt som du bäddar in en unik identifierare. Inga externa skript, ingen manuell sidredigering — bara en ren, återanvändbar C#‑metod.

## Nästa steg & relaterade ämnen

- **Add Bates numbering to every page manually** – iterera över `pdfDocument.Pages` för anpassningar per sida.
- **How to add artifact** för bilder: ersätt `TextArtifact` med `ImageArtifact`.
- **Create PDF document** med tabeller, diagram eller formulärfält med Aspose.Pdf:s rika API.
- **Automate batch processing** – läs en mapp med PDF‑filer, applicera samma Bates‑nummer, och spara dem i bulk.

Känn dig fri att experimentera med olika typsnitt, färger och positioner. Aspose.Pdf‑biblioteket är förvånansvärt flexibelt, och när du har bemästrat **how to add bates** och **how to add artifact**, är himlen gränsen.

### Snabbreferenskod (Alla steg i ett block)

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Artifacts;
using Aspose.Pdf.Text;

class BatesDemo
{
    static void Main()
    {
        string inputPath = @"C:\MyDocs\input.pdf";
        string outputPath = @"C:\MyDocs\output.pdf";

        using (var pdf = new Document(inputPath))
        {
            var bates = new BatesNumberArtifact
            {
                Text = "Case-2026-{0}",
                Position = new Position(50, 50),
                Font = FontRepository.FindFont("Helvetica"),
                FontSize = 12
            };
            pdf.Pages[1].Artifacts.Add(bates);
            pdf.Save(outputPath);
        }

        Console.WriteLine($"Saved PDF with Bates number to {outputPath}");
    }
}
```

Kör detta kodsnutt, så har du en solid grund för alla framtida PDF‑automatiseringsprojekt.

---

*Happy coding! If

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}