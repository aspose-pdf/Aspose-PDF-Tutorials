---
category: general
date: 2026-01-15
description: Lägg till Bates-nummer i din PDF snabbt med Aspose.Pdf. Lär dig hur du
  lägger till sidfot i PDF, lägger till sidnummer i PDF och lägger till anpassad sidnumrering.
draft: false
keywords:
- add bates numbers
- bates numbering pdf
- add footer to pdf
- add page numbers pdf
- add custom page numbering
language: sv
og_description: Lägg till Bates-nummer i din PDF snabbt med Aspose.Pdf. Lär dig hur
  du lägger till sidfot i PDF, lägger till sidnummer i PDF och lägger till anpassad
  sidnumrering.
og_title: Lägg till Bates-nummer i PDF – Bates-numrering PDF
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Lägg till Bates-nummer i PDF – Bates-numrering PDF
url: /sv/net/programming-with-text/add-bates-numbers-to-pdf-bates-numbering-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Lägg till Bates-nummer i PDF – Komplett guide

Har du någonsin behövt **add bates numbers** till en PDF men varit osäker på var du ska börja? Du är inte ensam—juridiska team, revisorer och alla som hanterar massiva dokumentuppsättningar stöter på detta problem dagligen. Den goda nyheten? Med Aspose.Pdf för .NET kan du strö dessa nummer på varje sida med bara några få rader.

I den här handledningen går vi igenom hela processen: från att hämta Aspose.Pdf‑biblioteket, ladda din källfil, konfigurera ett *BatesNumberingArtifact*, fästa det som en sidfot och slutligen spara resultatet. I slutet kommer du också att veta hur man **add footer to pdf**, **add page numbers pdf**, och till och med **add custom page numbering** för de knepiga edge‑cases.

## Vad du behöver

- .NET 6+ (eller .NET Framework 4.8 om du fortfarande använder den klassiska stacken)  
- En referens till NuGet‑paketet **Aspose.Pdf** (`Install-Package Aspose.Pdf`)  
- En PDF‑fil du vill stämpla (vi kallar den `source.pdf`)  

Det är allt—inga extra verktyg, inga tunga PDF‑redigerare. Låt oss dyka in.

![add bates numbers example](https://example.com/images/add-bates-numbers.png "add bates numbers example")

## Steg 1: Lägg till Bates-nummer – Ladda PDF‑dokumentet

Först behöver vi ett `Document`‑objekt som representerar PDF‑filen vi ska modifiera. Tänk på det som att öppna ett Word‑dokument innan du börjar skriva.

```csharp
using Aspose.Pdf;
using System;

class Program
{
    static void Main()
    {
        // Load the PDF you want to add bates numbers to
        var pdfDocument = new Document(@"YOUR_DIRECTORY\source.pdf");

        // The rest of the steps go here...
    }
}
```

> **Varför detta är viktigt:** Att ladda filen ger dig åtkomst till dess `Pages`‑samling, vilket är där vi senare kommer att fästa Bates‑numreringsartefakten. Om filen inte kan hittas kommer Aspose att kasta ett tydligt `FileNotFoundException`, så dubbelkolla sökvägen.

## Steg 2: Konfigurera bates numbering pdf-inställningar

Nu definierar vi *hur* siffrorna ska se ut. `BatesNumberingArtifact` låter dig ange ett prefix, startnummer, siffrupadding, suffix och placering. Detta är kärnan i **bates numbering pdf**.

```csharp
// Step 2: Create and configure the Bates numbering artifact
var batesArtifact = new BatesNumberingArtifact
{
    Prefix = "CASE-",
    StartNumber = 1000,
    NumberDigits = 5,          // forces 5 digits, e.g., 01000
    Suffix = "-A",
    Placement = BatesNumberingArtifact.PlacementLocation.BottomCenter
};
```

> **Proffstips:** Om du vill att siffrorna ska visas i sidhuvudet istället, byt `BottomCenter` mot `TopCenter`. Placering‑enumet stödjer även `BottomLeft`, `BottomRight` osv., vilket ger dig flexibilitet för olika **add footer to pdf**‑stilar.

## Steg 3: Lägg till page numbers pdf – Fäst artefakten på varje sida

När artefakten är klar loopar vi igenom varje sida och lägger till den i `Artifacts`‑samlingen. Detta är steget som faktiskt **adds page numbers pdf**.

```csharp
// Step 3: Attach the artifact to each page
foreach (Page page in pdfDocument.Pages)
{
    page.Artifacts.Add(batesArtifact);
}
```

> **Vad händer under huven?** `Artifacts`‑samlingen renderas efter sidans huvudinnehåll, vilket säkerställer att Bates‑numret ligger ovanpå eventuell befintlig text men under annotationer. Om du vill att numret ska ligga bakom innehållet (sällsynt) använder du `page.Artifacts.Insert(0, batesArtifact)`.

## Steg 4: Lägg till custom page numbering – Spara den uppdaterade PDF‑filen

Slutligen skriver vi det modifierade dokumentet till disk. Utdatafilen kommer att innehålla Bates‑numren som en permanent del av varje sida.

```csharp
// Step 4: Save the PDF with the new numbering
pdfDocument.Save(@"YOUR_DIRECTORY\bates_out.pdf");

Console.WriteLine("Bates numbers added successfully! Check bates_out.pdf.");
```

> **Verifieringstips:** Öppna `bates_out.pdf` i någon visare. Du bör se något i stil med `CASE-01000-A` centrerat längst ner på varje sida. Om siffrorna saknas, dubbelkolla att `Placement`‑egenskapen matchar den avsedda platsen.

## Fullt fungerande exempel

När vi sätter ihop allt, här är det kompletta, färdiga programmet:

```csharp
using Aspose.Pdf;
using System;

class Program
{
    static void Main()
    {
        // Load the source PDF
        var pdfDocument = new Document(@"YOUR_DIRECTORY\source.pdf");

        // Configure Bates numbering artifact
        var batesArtifact = new BatesNumberingArtifact
        {
            Prefix = "CASE-",
            StartNumber = 1000,
            NumberDigits = 5,
            Suffix = "-A",
            Placement = BatesNumberingArtifact.PlacementLocation.BottomCenter
        };

        // Attach artifact to each page (adds page numbers pdf)
        foreach (Page page in pdfDocument.Pages)
        {
            page.Artifacts.Add(batesArtifact);
        }

        // Save the new PDF (adds footer to pdf)
        pdfDocument.Save(@"YOUR_DIRECTORY\bates_out.pdf");

        Console.WriteLine("Bates numbers added successfully! Check bates_out.pdf.");
    }
}
```

### Förväntat resultat

- **Fil:** `bates_out.pdf` i samma mapp som `source.pdf`  
- **Visuell:** Text i botten‑center `CASE-01000-A`, `CASE-01001-A`, … för varje efterföljande sida  
- **Beteende:** Siffrorna är permanent inbäddade; de överlever utskrift, plattning och vidare redigering.

## Vanliga variationer & edge‑cases

| Situation | Hur man justerar |
|-----------|-------------------|
| **Olika startnummer** | Ändra `StartNumber` till valfritt heltal (t.ex. `StartNumber = 500`). |
| **Bokstavssuffix per volym** | Använd en loop för att ändra `Suffix` per sida, eller skapa flera artefakter med olika suffix. |
| **Högerjusterad numrering** | Sätt `Placement = BatesNumberingArtifact.PlacementLocation.BottomRight`. |
| **Stora dokument (10 000+ sidor)** | Överväg att batcha sidor eller öka `NumberDigits` för att undvika overflow. |
| **Behöver dölja nummer på vissa sidor** | Hoppa över dessa sidor i `foreach`‑loopen (t.ex. `if (page.Number != 1) page.Artifacts.Add(batesArtifact);`). |

> **Var försiktig med:** Att använda ett `Prefix` eller `Suffix` som innehåller otillåtna filnamnstecken (t.ex. `*` eller `?`). Aspose kommer fortfarande att bädda in dem, men de kan orsaka problem när du senare extraherar texten.

## Proffstips för produktionsanvändning

- **Cachea artefakten** om du bearbetar många PDF‑filer i rad; att skapa den en gång sparar några millisekunder per fil.  
- **Trådsäkerhet:** `BatesNumberingArtifact`‑instansen är inte trådsäker, så ge varje tråd sin egen kopia.  
- **Prestanda:** För massiva batcher, inaktivera PDF‑komprimering (`pdfDocument.Compress = false`) innan du sparar, återaktivera vid behov.  
- **Testning:** Kör alltid en snabb visuell kontroll på den första genererade PDF‑filen för att säkerställa att placeringen matchar ditt juridiska teams standarder.

## Slutsats

Du har nu ett gediget, end‑to‑end‑recept för hur man **add bates numbers** till vilken PDF som helst med Aspose.Pdf, komplett med alternativ för **add footer to pdf**, **add page numbers pdf**, och **add custom page numbering**. Koden är helt självständig, fungerar med .NET 6 och senare, och kan släppas in i vilken befintlig automatiseringspipeline som helst.

Vad blir nästa steg? Prova att byta `BottomCenter`‑placeringen till en header‑stil, experimentera med dynamiska prefix (t.ex. ärendenummer från en databas), eller kombinera detta med Asposes text‑extraktionsfunktioner för att skapa ett sökbart index över dina ny‑numrerade dokument. Himlen är gränsen, och du har just fått ett kraftfullt verktyg för dokumentkontroll.

Lycka till med kodandet, och må dina PDF‑filer alltid vara perfekt numrerade!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}