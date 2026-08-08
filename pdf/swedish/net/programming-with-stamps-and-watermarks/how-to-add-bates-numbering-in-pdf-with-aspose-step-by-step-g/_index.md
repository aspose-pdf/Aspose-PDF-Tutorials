---
category: general
date: 2026-07-20
description: Hur du lägger till Bates‑nummerering i en PDF med Aspose.Pdf. Lär dig
  att lägga till Bates‑nummer i PDF och sätta en stämpel på varje sida snabbt och
  pålitligt.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to add bates numbering
- add bates numbers pdf
- add stamp to each page
language: sv
lastmod: 2026-07-20
og_description: Hur man lägger till Bates-nummerering i en PDF med Aspose.Pdf. Denna
  guide visar hur du lägger till Bates-nummer i PDF och stämplar varje sida med bara
  några rader C#.
og_image_alt: Screenshot of a PDF page displaying Bates numbering added by Aspose.Pdf
og_title: Hur man lägger till Bates-nummerering i PDF – Komplett Aspose.Pdf-handledning
schemas:
- author: Aspose
  dateModified: '2026-07-20'
  description: How to add bates numbering to a PDF using Aspose.Pdf. Learn to add
    bates numbers pdf and add stamp to each page quickly and reliably.
  headline: How to Add Bates Numbering in PDF with Aspose – Step‑by‑Step Guide
  type: TechArticle
- questions:
  - answer: Yes. Load the document with a `PdfLoadOptions` object that supplies the
      password, then proceed exactly as shown.
    question: Does this work with password‑protected PDFs?
  - answer: Create multiple `BatesNumberingStamp` instances, configure each with its
      own `Prefix`, and apply them only to the appropriate page ranges.
    question: What if I need different prefixes per case?
  - answer: 'Aspose.Pdf offers a 30‑day trial. For production use you’ll need a license,
      but the API surface remains identical. --- ## Conclusion We’ve just covered
      **how to add bates numbering** to any PDF using Aspose.Pdf, demonstrated how
      to **add bates numbers pdf** in a clean, repeatable fashion, and showed'
    question: Is the library free?
  type: FAQPage
tags:
- Aspose.Pdf
- Bates numbering
- PDF automation
title: Hur man lägger till Bates-nummerering i PDF med Aspose – Steg‑för‑steg‑guide
url: /sv/net/programming-with-stamps-and-watermarks/how-to-add-bates-numbering-in-pdf-with-aspose-step-by-step-g/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man lägger till Bates‑numrering i PDF med Aspose – Steg‑för‑steg‑guide

Har du någonsin undrat **hur man lägger till bates‑numrering** i ett juridiskt dokument utan att spendera timmar i ett GUI? Du är inte ensam. På många advokatbyråer, myndigheter och även stora företag är det en daglig uppgift att stämpla varje sida med en unik identifierare—men en enda rad C# kan göra det till en barnlek.

I den här handledningen går vi igenom ett komplett, körbart exempel som visar dig exakt **hur man lägger till bates‑numrering** med Aspose.Pdf‑biblioteket. I slutet kommer du också att veta hur man **lägger till bates‑nummer pdf**‑filer och **lägger till stämpel på varje sida** med bara några rader kod. Ingen magi, bara tydlig resonemang och praktiska tips.

## Vad du kommer att lära dig

- Ladda en befintlig PDF med Aspose.Pdf.
- Skapa en `BatesNumberingStamp` och anpassa dess utseende.
- Loopa igenom varje sida och **lägger till stämpel på varje sida** automatiskt.
- Spara resultatet som en ny PDF som har ett professionellt Bates‑nummer på varje blad.

### Förutsättningar

- .NET 6.0 eller senare (koden fungerar även på .NET Framework 4.7+).
- En giltig Aspose.Pdf för .NET‑licens (eller en tillfällig utvärderingsnyckel).
- En original‑PDF‑fil som du vill numrera (vi kallar den `Original.pdf`).

Om du uppfyller dessa tre punkter är du redo att dyka in.

---

## Steg 1: Ställ in ditt projekt och installera Aspose.Pdf

Först, skapa ett nytt konsolprojekt (eller lägg till koden i ett befintligt). Hämta sedan NuGet‑paketet:

```bash
dotnet add package Aspose.Pdf
```

> **Proffstips:** Om du är på ett företagsnätverk, se till att din NuGet‑källa är konfigurerad för att nå `https://www.nuget.org`.

## Steg 2: Ladda källdokumentet PDF

Att ladda en PDF är lika enkelt som att peka Aspose på filsökvägen. Klassen `Document` representerar hela filen.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Load the source PDF (replace the path with your own)
var document = new Document(@"C:\Temp\Original.pdf");

// Quick sanity check – how many pages are we dealing with?
Console.WriteLine($"Document contains {document.Pages.Count} pages.");
```

Varför loggar vi sidantalet? Eftersom Bates‑numrering måste vara sekventiell över *alla* sidor, och det är bra att verifiera att du inte av misstag laddar en annan fil.

## Steg 3: Skapa en Bates‑numreringsstämpel

Kärnan i operationen är `BatesNumberingStamp`. Den låter dig definiera prefix, separator, siffrutfyllnad och även om stämpeln ska behandlas som ett *artefakt* (dvs. osynligt för verktyg som extraherar text).

```csharp
var batesStamp = new BatesNumberingStamp
{
    // Starting number – change this to whatever your workflow requires
    StartingNumber = 1000,

    // A human‑readable prefix, often a case or project code
    Prefix = "ABC-",

    // Separator between the running number and the total page count
    Separator = "/",

    // Pad the number with leading zeros to a fixed width (5 digits here)
    NumberOfDigits = 5,

    // Mark the stamp as an artifact so it won’t be indexed by search
    Artifact = true
};
```

**Varför dessa inställningar?**  
- `StartingNumber = 1000` efterliknar ett typiskt juridiskt ärende som redan har en kö.  
- `NumberOfDigits = 5` garanterar att nummer som `01000`, `01001` osv. radas upp snyggt.  
- `Artifact = true` är avgörande när PDF‑filen ska matas in i OCR‑ eller e‑discovery‑pipelines; numren förblir synliga för människor men ignoreras av text‑sökmotorer.

## Steg 4: Lägg till stämpeln på varje sida

Nu loopar vi över `document.Pages` och applicerar samma stämpel på varje sida. Aspose ökar automatiskt numret åt dig.

```csharp
foreach (Page page in document.Pages)
{
    // The AddStamp method clones the stamp for the current page,
    // updates the running number, and positions it at the default location.
    page.AddStamp(batesStamp);
}
```

> **Vanlig fråga:** *Kan jag styra var stämpeln visas?*  
> Absolut. `BatesNumberingStamp` ärver från `Stamp`, så du kan sätta egenskaper som `HorizontalAlignment`, `VerticalAlignment`, `XIndent` och `YIndent` innan loopen. För korthetens skull håller vi oss till standardnedre‑högra hörnet.

## Steg 5: Spara den modifierade PDF‑filen

Till sist, spara ändringarna. Du kan skriva över originalfilen eller skriva till en ny plats—här behåller vi båda kopiorna.

```csharp
// Save the new PDF with Bates numbers
document.Save(@"C:\Temp\BatesNumbered.pdf");

// Inform the user
Console.WriteLine("Bates numbering added successfully!");
```

När du öppnar `BatesNumbered.pdf` kommer varje sida att visa en stämpel liknande:

```
ABC-01000/00123
ABC-01001/00123
…
ABC-01122/00123
```

där `00123` är det totala sidantalet, och prefixet `ABC-` förblir konstant.

---

## Fullt fungerande exempel

Kopiera hela blocket nedan till en ny `Program.cs`‑fil och kör den. Anpassa filsökvägarna så att de matchar din miljö.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the source PDF
            var srcPath = @"C:\Temp\Original.pdf";
            var document = new Document(srcPath);
            Console.WriteLine($"Loaded '{srcPath}' with {document.Pages.Count} pages.");

            // 2️⃣ Configure the Bates numbering stamp
            var batesStamp = new BatesNumberingStamp
            {
                StartingNumber = 1000,
                Prefix = "ABC-",
                Separator = "/",
                NumberOfDigits = 5,
                Artifact = true,
                // Optional: change alignment if you need a different location
                // HorizontalAlignment = HorizontalAlignment.Left,
                // VerticalAlignment = VerticalAlignment.Top,
                // XIndent = 20,
                // YIndent = 20
            };

            // 3️⃣ Apply the stamp to every page
            foreach (Page page in document.Pages)
            {
                page.AddStamp(batesStamp);
            }

            // 4️⃣ Save the new PDF
            var outPath = @"C:\Temp\BatesNumbered.pdf";
            document.Save(outPath);
            Console.WriteLine($"Saved Bates‑numbered PDF to '{outPath}'.");
        }
    }
}
```

**Förväntad utskrift i konsolen:**

```
Loaded 'C:\Temp\Original.pdf' with 12 pages.
Saved Bates-numbered PDF to 'C:\Temp\BatesNumbered.pdf'.
```

Öppna den sparade filen så ser du de sekventiella numren på varje sida—precis vad du kan förvänta dig när du **lägger till bates‑nummer pdf**.

---

## Avancerade justeringar (valfritt)

| Mål | Så här gör du |
|------|-------------------|
| **Ändra stämpelfärg** | Ställ in `batesStamp.Color = Color.FromRgb(255, 0, 0);` före loopen. |
| **Placera stämpel i rubriken** | Justera `HorizontalAlignment` och `VerticalAlignment`‑egenskaperna som visas i den kommenterade koden. |
| **Hoppa över vissa sidor** | Lägg till ett `if (page.Number % 2 == 0) continue;`‑villkor inuti `foreach`. |
| **Använd ett anpassat teckensnitt** | Tilldela `batesStamp.Font = FontRepository.FindFont("Arial");`. |
| **Gör stämpeln synlig för OCR** | Ställ in `Artifact = false`. |

Dessa variationer låter dig **lägga till stämpel på varje sida** samtidigt som du behåller kärnlogiken prydlig.

---

## Vanliga frågor

**Q: Fungerar detta med lösenordsskyddade PDF‑filer?**  
A: Ja. Ladda dokumentet med ett `PdfLoadOptions`‑objekt som anger lösenordet, fortsätt sedan exakt som visat.

**Q: Vad händer om jag behöver olika prefix per ärende?**  
A: Skapa flera `BatesNumberingStamp`‑instanser, konfigurera varje med sitt eget `Prefix`, och applicera dem endast på de relevanta sidintervallen.

**Q: Är biblioteket gratis?**  
A: Aspose.Pdf erbjuder en 30‑dagars provperiod. För produktionsbruk behöver du en licens, men API‑ytan är identisk.

---

## Slutsats

Vi har precis gått igenom **hur man lägger till bates‑numrering** i vilken PDF som helst med Aspose.Pdf, demonstrerat hur man **lägger till bates‑nummer pdf** på ett rent, repeterbart sätt, och visat dig det enklaste sättet att **lägga till stämpel på varje sida** med en enda loop. Koden är helt självständig, körs på sekunder och kan integreras i större dokument‑bearbetningspipelines utan ändring.

Klar för nästa utmaning? Försök skapa en framsida som listar Bates‑intervallet, eller bädda in en QR‑kod bredvid varje stämpel. Möjligheterna är oändliga, och samma mönster du lärde dig idag kommer att tjäna dig väl där du behöver automatisera PDF‑metadata.

Om du fann den här guiden hjälpsam, dela den, lämna en kommentar, eller utforska våra andra handledningar om PDF‑sammanfogning, vattenstämpling och digitala signaturer. Lycka till med kodandet!

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Hur man lägger till sidstämplar i PDF‑filer med Aspose.PDF för .NET: En komplett guide](/pdf/english/net/watermarks-backgrounds/add-page-stamp-aspose-pdf-dotnet-guide/)
- [Hur man lägger till sidnummerstämplar i PDF‑filer med Aspose.PDF för .NET | Vattenstämplar & bakgrunder](/pdf/english/net/watermarks-backgrounds/add-page-number-stamp-using-aspose-pdf-dotnet/)
- [Hur man lägger till och anpassar sidnummer i PDF‑filer med Aspose.PDF för .NET | Guide för dokumentmanipulation](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}