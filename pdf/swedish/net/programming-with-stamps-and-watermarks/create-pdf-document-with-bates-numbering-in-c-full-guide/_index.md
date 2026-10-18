---
category: general
date: 2026-03-06
description: Skapa PDF-dokument i C# och lägg enkelt till bates‑nummer. Lär dig hur
  du lägger till en tom PDF‑sida, placerar ett stämpel på sidan och implementerar
  bates‑nummerering.
draft: false
keywords:
- create pdf document
- add bates number
- add blank page pdf
- how to add bates numbering
- place stamp on page
language: sv
og_description: Skapa PDF-dokument i C# och lägg till bates‑nummer. Denna guide visar
  hur du lägger till en tom PDF‑sida, placerar en stämpel på sidan och tillämpar bates‑nummerering.
og_title: Skapa PDF-dokument med Bates-nummerering – C#-handledning
tags:
- Aspose.Pdf
- C#
- PDF automation
title: Skapa PDF-dokument med Bates-nummerering i C# – Fullständig guide
url: /sv/net/programming-with-stamps-and-watermarks/create-pdf-document-with-bates-numbering-in-c-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa PDF-dokument med Bates-nummerering i C#

Har du någonsin behövt **skapa PDF-dokument** i C# och undrat hur du lägger till ett Bates‑nummer utan att rycka upp håret? Du är inte ensam—juridiska firmor, domstolar och till och med vissa företags‑compliance‑team stöter på exakt detta problem varje dag. Den goda nyheten? Med några rader Aspose.Pdf‑kod kan du skapa ett helt nytt PDF, lägga till en tom sida och stämpla ett korrekt Bates‑nummer i ett smidigt flöde.

I den här handledningen går vi igenom hela processen: från att sätta upp projektet, till att lägga till en tom PDF‑sida, till att ta reda på **how to add bates numbering**, och slutligen **place stamp on page** och spara resultatet. I slutet har du ett färdigt kodsnutt som du kan klistra in i vilken .NET‑app som helst. Inga vaga referenser, bara ett komplett, körbart exempel.

## Vad du behöver

- **.NET 6+** (eller .NET Framework 4.6+ – Aspose.Pdf fungerar med båda)
- **Aspose.Pdf for .NET** NuGet‑paket (`Install-Package Aspose.Pdf`)
- En bra IDE (Visual Studio, Rider eller VS Code med C#‑tillägg)

Det är allt. Inga extra DLL‑filer, inga externa tjänster. Låt oss dyka ner.

## Steg 1: Skapa PDF-dokument – Initial setup

Först och främst behöver vi ett nytt `Document`‑objekt. Tänk på det som en tom duk där allt annat kommer att finnas.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Initialize a new PDF document
Document pdfDocument = new Document();
```

> **Varför detta är viktigt:** `Document`‑klassen är startpunkten för varje Aspose‑operation. Att instansiera den ger dig åtkomst till `Pages`‑samlingen, metadata och säkerhetsinställningar—alla byggstenar för en professionell PDF.

## Steg 2: Lägg till tom PDF‑sida

En PDF utan sidor är som en bok utan sidor—ganska värdelös. Att lägga till en tom sida är enkelt, och det ger oss en yta att stämpla Bates‑numret på.

```csharp
// Add a single blank page to the document
Page page = pdfDocument.Pages.Add();
```

> **Pro tip:** Om du behöver flera sidor, anropa bara `pdfDocument.Pages.Add()` i en loop. Varje anrop returnerar ett nytt `Page`‑objekt som du kan anpassa oberoende.

## Steg 3: Hur man lägger till Bates‑nummerering – Skapa TextStamp

Nu kommer kärnan i saken: **Bates number**. I Aspose.Pdf är det bara en `TextStamp` med en speciell artifact‑flagga.

```csharp
// Create a text stamp that will serve as a Bates number
TextStamp batesStamp = new TextStamp("Bates-001")
{
    // Mark the stamp as a Bates‑numbering artifact (helps PDF viewers treat it specially)
    Artifact = ArtifactType.BatesNumbering,
    // Align the stamp to the bottom‑right corner of the page
    HorizontalAlignment = HorizontalAlignment.Right,
    VerticalAlignment = VerticalAlignment.Bottom,
    // Add a small margin so the number isn’t glued to the edge
    Margin = new Margin { Bottom = 10, Right = 10 }
};
```

> **Varför vi sätter `Artifact`**: Vissa PDF‑läsare visar Bates‑nummer som sökbar metadata. Genom att flagga stämpeln som ett `BatesNumbering`‑artifact säkerställer du att efterföljande verktyg automatiskt kan känna igen den.

## Steg 4: Placera stämpel på sida

Med stämpeln klar, **place stamp on page** nu. Detta är steget där det visuella numret faktiskt visas i PDF‑filen.

```csharp
// Add the Bates number stamp to the previously created page
page.AddStamp(batesStamp);
```

> **Edge case:** Om du behöver att numret ökar på varje sida, skulle du loopa igenom `pdfDocument.Pages` och uppdatera `batesStamp.Value` innan du anropar `AddStamp`. Exemplet här håller det enkelt med ett statiskt “Bates‑001”.

## Steg 5: Spara och verifiera resultatet

Till sist sparar vi PDF‑filen till disk. Välj en mapp som du har skrivrättigheter till; annars får du ett `UnauthorizedAccessException`.

```csharp
// Save the stamped PDF to a file
pdfDocument.Save("YOUR_DIRECTORY/BatesStamped.pdf");
```

När du öppnar `BatesStamped.pdf` i någon visare bör du se en liten “Bates‑001” prydligt placerad i det nedre högra hörnet på den tomma sidan.

> **Förväntat resultat:**  
> ![PDF with Bates number stamp](image-placeholder.png "PDF with Bates number stamp")  
> *Alt text:* PDF med Bates‑nummerstämpling i nedre högra hörnet.

Om numret inte visas, dubbelkolla marginalvärdena och se till att sidstorleken inte är för liten (standard A4 fungerar bra). Bekräfta också att `Artifact`‑flaggan inte tas bort av några efterbearbetningsverktyg.

## Fullständigt fungerande exempel

Nedan är det kompletta, kopiera‑och‑klistra‑klara programmet. Det inkluderar alla `using`‑direktiv och kommentarer för att hålla dig orienterad.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize a new PDF document
        Document pdfDocument = new Document();

        // 2️⃣ Add a blank page – this is where we’ll put the Bates number
        Page page = pdfDocument.Pages.Add();

        // 3️⃣ Create a TextStamp for the Bates number
        TextStamp batesStamp = new TextStamp("Bates-001")
        {
            Artifact = ArtifactType.BatesNumbering,          // Marks it as a Bates‑numbering artifact
            HorizontalAlignment = HorizontalAlignment.Right, // Align right
            VerticalAlignment = VerticalAlignment.Bottom,    // Align bottom
            Margin = new Margin { Bottom = 10, Right = 10 }  // Small margin from edges
        };

        // 4️⃣ Place the stamp on the page
        page.AddStamp(batesStamp);

        // 5️⃣ Save the PDF to disk
        string outputPath = @"C:\Temp\BatesStamped.pdf";
        pdfDocument.Save(outputPath);

        Console.WriteLine($"PDF created successfully: {outputPath}");
    }
}
```

Kör programmet, öppna PDF‑filen, och du kommer att se Bates‑numret exakt där vi instruerade det att placeras. 🎉

## Vanliga variationer & fallgropar

| Scenario | Vad som ska ändras | Varför |
|----------|--------------------|--------|
| **Multiple pages, incrementing numbers** | Loop through `pdfDocument.Pages`, set `batesStamp.Value = $"Bates-{i:D3}"` before `AddStamp` | Ger varje sida en unik identifierare, typiskt för juridiska paket |
| **Different placement (top‑left)** | Change `HorizontalAlignment = HorizontalAlignment.Left` and `VerticalAlignment = VerticalAlignment.Top` | Vissa organisationer föredrar numret i rubriken istället för i sidfoten |
| **Custom font or color** | Set `batesStamp.TextState.Font = FontRepository.FindFont("Arial"); batesStamp.TextState.FontSize = 12; batesStamp.TextState.ForegroundColor = Color.Red;` | Förbättrar läsbarheten eller uppfyller varumärkesriktlinjer |
| **Adding an existing PDF as a background** | Load the source PDF with `Document src = new Document("source.pdf"); pdfDocument.Pages.Add(src.Pages[1]);` | Användbart när du behöver stämpla över ett förgenererat formulär |

## Avslutning

Vi har just visat hur man **create PDF document**, **add blank page pdf**, och **add bates number** med Aspose.Pdf för .NET, sedan **place stamp on page** och sparar filen. Koden är avsiktligt kompakt så att du kan anpassa den till större arbetsflöden—oavsett om du batchar dussintals filer eller integrerar i en webbtjänst.

Om du är redo att gå vidare, överväg:

- Automatisera inkrementeringslogiken för stora ärendefiler.
- Inbädda PDF‑genereringen i ett ASP.NET Core‑API.
- Lägga till säkerhet (lösenordsskydd) med `pdfDocument.Encrypt(...)`.

Känn dig fri att experimentera, bryta saker och ställa frågor i kommentarerna. Lycka till med kodandet, och må dina PDF‑filer alltid vara perfekt stämplade!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}