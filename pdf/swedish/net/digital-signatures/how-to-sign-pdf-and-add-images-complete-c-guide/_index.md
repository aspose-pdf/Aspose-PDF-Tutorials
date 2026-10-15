---
category: general
date: 2026-03-29
description: Hur man signerar en PDF med en digital signatur och lägger till en beskuren
  bild i C#. Lär dig att lägga till digital signatur i PDF, beskära bild för PDF och
  enkelt lägga till bild i PDF.
draft: false
keywords:
- how to sign pdf
- add digital signature pdf
- crop image for pdf
- add image to pdf
- digital signature pdf page
language: sv
og_description: Hur man signerar PDF med en digital signatur och bäddar in en beskuren
  bild med Aspose.Pdf i C#. Följ den här guiden för en komplett lösning.
og_title: Hur man signerar PDF och lägger till bilder – Steg‑för‑steg C#‑handledning
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Hur man signerar PDF och lägger till bilder – Komplett C#‑guide
url: /sv/net/digital-signatures/how-to-sign-pdf-and-add-images-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man signerar PDF och lägger till bilder – Komplett C#-guide

Har du någonsin undrat **how to sign PDF** filer programatiskt samtidigt som du infogar en anpassad bild? Kanske bygger du ett godkännandeflöde och behöver en juridiskt bindande signatur *och* en miniatyr av signatarens foto på samma sida. Kort sagt vill du **add digital signature pdf** innehåll, beskära den bilden och sedan **add image to pdf** utan att anstränga dig.  

Den här handledningen guidar dig genom varje steg—från att ladda ett ECDSA PKCS#7‑certifikat till att beskära en JPEG och stämpla den på den signerade sidan. I slutet har du en enda, körbar C#‑fil som signerar sida 1, beskär ett foto till 400 × 400 px och placerar det på en exakt plats. Inga externa skript, ingen magi, bara tydlig kod och förklaringar.

## Förutsättningar

- .NET 6.0 eller senare (koden fungerar också med .NET Framework 4.7+)
- **Aspose.Pdf for .NET** NuGet‑paket (version 23.9 eller nyare)
- Ett ECDSA P‑256‑certifikat i PKCS#7 (`.pfx`)‑format och dess lösenord
- En JPEG‑bild du vill bädda in (t.ex. `photo.jpg`)

> **Pro tip:** Håll din certifikatfil utanför versionskontrollen och skydda lösenordet med en hemlig hanterare.

---

## Steg 1: Ställ in projektet och importerna

Först, skapa en konsolapp (eller integrera detta i någon befintlig tjänst). Lägg till Aspose.Pdf‑referensen:

```bash
dotnet add package Aspose.Pdf
```

Inkludera sedan de nödvändiga namnutrymmena:

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Forms;
using Aspose.Pdf.Drawing;
```

Dessa `using`‑satser ger dig åtkomst till `Document`-, `Signature`- och `Rectangle`‑klasserna som vi kommer att behöva senare.

## Steg 2: Ladda PDF‑filen och förbered signaturen

Vi öppnar en befintlig PDF (`source.pdf`) och skapar ett **digital signature pdf**‑objekt som använder en PKCS#7‑detacherad signatur. Certifikatet är en ECDSA P‑256‑nyckel, som är allmänt accepterad för efterlevnad.

```csharp
// Load the PDF you want to sign
var doc = new Document("YOUR_DIRECTORY/source.pdf");

// Initialize the signature appearance (optional but recommended)
var signature = new Signature(doc);
signature.Contact = "John Doe";
signature.Location = "New York, USA";
signature.Reason = "Document approval";

// Load the PKCS#7 certificate (ECDSA P‑256) for signing
var pkcsSignature = new PKCS7Detached(
    "YOUR_DIRECTORY/ecdsa.pfx",   // certificate file
    "YOUR_PASSWORD");             // certificate password
```

**Varför detta är viktigt:** Att använda en detacherad PKCS#7‑signatur behåller det ursprungliga PDF‑innehållet intakt samtidigt som en kryptografisk hash bäddas in. Detta är branschstandardmetoden för juridiskt bindande PDF‑filer.

## Steg 3: Applicera den digitala signaturen på en specifik sida

Nu placerar vi det synliga signaturfältet på **page 1**. Rektangeln definierar var signaturrutan visas (koordinaterna är i punkter, där 1 tum = 72 punkter).

```csharp
// Apply the digital signature to page 1, covering a rectangular area
signature.Sign(
    pageNumber: 1,
    isVisible: true,
    signatureRect: new Rectangle(100, 100, 300, 300),
    pkcsSignature);
```

Om du inte behöver en synlig ruta, sätt `isVisible` till `false`. `signatureRect` kan justeras för att passa ditt dokumentlayout.

## Steg 4: Öppna bildströmmen och definiera beskärningsområden

Vi läser JPEG‑filen till en ström och specificerar en **source rectangle** som väljer de övre‑vänstra 400 × 400 pixlarna. Detta är **crop image for pdf**‑operationen.

```csharp
// Open the image file that will be added to the PDF
using var imageStream = File.OpenRead("YOUR_DIRECTORY/photo.jpg");

// Define the source rectangle that selects the portion to crop (0‑400 pixels)
var sourceRect = new Rectangle(0, 0, 400, 400);
```

> **Edge case:** Om din bild är mindre än 400 × 400, kommer beskärningen automatiskt att begränsas till bildens faktiska dimensioner—inget undantag kastas.

## Steg 5: Definiera var den beskurna bilden ska visas

Därefter ställer vi in **destination rectangle** på PDF‑sidan. I detta exempel placerar vi bilden vid (50, 50) med en storlek på 200 × 200 punkter (≈2,78 tum kvadrat).

```csharp
// Define the destination rectangle where the cropped image will be placed on the page
var destinationRect = new Rectangle(50, 50, 200, 200);
```

Känn dig fri att experimentera: ändra X/Y‑koordinaterna för att flytta bilden, eller justera bredd/höjd för skalning.

## Steg 6: Infoga den beskurna bilden på den signerade sidan

Slutligen lägger vi till bilden på **page 1** (samma sida som nu bär signaturen). Den `AddImage`‑överladdning vi använder accepterar käll‑ och destinationsrektanglar, vilket effektivt utför beskärning och placering i ett anrop.

```csharp
// Insert the cropped image onto page 1 at the specified location
doc.Pages[1].AddImage(imageStream, sourceRect, destinationRect);
```

Bakom kulisserna extraherar Aspose.Pdf 400 × 400‑pixelregionen, skalar om den till 200 × 200 punkter och skriver in den i PDF‑innehållsströmmen.

## Steg 7: Spara den signerade och bild‑förstärkta PDF‑filen

Efter alla ändringar, spara dokumentet. Du kan skriva över originalet eller skriva till en ny fil.

```csharp
// Save the final document
doc.Save("YOUR_DIRECTORY/output_signed.pdf");
Console.WriteLine("PDF signed and image added successfully!");
```

När du öppnar `output_signed.pdf` i Adobe Acrobat eller någon PDF‑visare, kommer du att se:

- Ett synligt signaturfält på de koordinater du angav.
- Den beskurna foton placerad vid (50, 50) på sida 1.
- Den digitala signaturen validerad (förutsatt att visaren litar på ditt certifikat).

## Vanliga frågor (FAQ)

| Question | Answer |
|----------|--------|
| **Kan jag signera en annan sida?** | Ändra argumentet `pageNumber` i `signature.Sign` till ett giltigt sidindex (1‑baserat). |
| **Vad händer om jag behöver flera signaturer?** | Skapa en ny `Signature`‑instans för varje sida eller plats, återanvänd samma `pkcsSignature` om samma certifikat gäller. |
| **Är bildbeskärning begränsad till rektanglar?** | Ja, Aspose.Pdf:s `AddImage` fungerar med rektangulära områden. För komplexa former måste du förbehandla bilden (t.ex. med System.Drawing) innan inbäddning. |
| **Hur gör jag signaturen osynlig?** | Sätt `isVisible` till `false` och utelämna `signatureRect`. Signaturen kommer fortfarande att vara kryptografiskt giltig. |
| **Vilka format kan jag bädda in förutom JPEG?** | PNG, BMP, GIF och TIFF stöds alla. Ändra bara filvägen och se till att strömmen läser rätt bytes. |

## Fullt fungerande exempel

Nedan är det kompletta, fristående programmet. Kopiera‑klistra in det i `Program.cs`, justera sökvägarna och kör.

```csharp
// Program.cs
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Forms;
using Aspose.Pdf.Drawing;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source PDF
        var doc = new Document("YOUR_DIRECTORY/source.pdf");

        // 2️⃣ Prepare the digital signature appearance
        var signature = new Signature(doc)
        {
            Contact = "John Doe",
            Location = "New York, USA",
            Reason = "Document approval"
        };

        // 3️⃣ Load the PKCS#7 ECDSA P‑256 certificate
        var pkcsSignature = new PKCS7Detached(
            "YOUR_DIRECTORY/ecdsa.pfx",
            "YOUR_PASSWORD");

        // 4️⃣ Apply a visible signature on page 1
        signature.Sign(
            pageNumber: 1,
            isVisible: true,
            signatureRect: new Rectangle(100, 100, 300, 300),
            pkcsSignature);

        // 5️⃣ Open the image to be added
        using var imageStream = File.OpenRead("YOUR_DIRECTORY/photo.jpg");

        // 6️⃣ Define crop (source) and placement (destination) rectangles
        var sourceRect = new Rectangle(0, 0, 400, 400);      // crop 400×400 px from top‑left
        var destinationRect = new Rectangle(50, 50, 200, 200); // place at (50,50) with 200×200 pt size

        // 7️⃣ Insert the cropped image onto the same page
        doc.Pages[1].AddImage(imageStream, sourceRect, destinationRect);

        // 8️⃣ Save the final PDF
        doc.Save("YOUR_DIRECTORY/output_signed.pdf");
        Console.WriteLine("PDF signed and image added successfully!");
    }
}
```

**Förväntat resultat:** När du öppnar `output_signed.pdf` visas ett signaturfält (100 × 100 → 300 × 300 punkter) och en 200 × 200‑punkts bild härledd från det övre‑vänstra hörnet av `photo.jpg`. Signaturen valideras mot det medföljande ECDSA‑certifikatet.

## Avslutning

Vi har gått igenom **how to sign PDF** filer, hur man **add digital signature pdf** på en specifik sida, hur man **crop image for pdf**, och slutligen hur man **add image to pdf** med Aspose.Pdf i C#. Hela flödet—från att ladda certifikatet till att spara det slutgiltiga dokumentet—passar in i en enda, lättläst källfil.

Om du är redo för nästa utmaning, överväg:

- Att lägga till **multiple signatures** på olika sidor (använd konceptet “digital signature pdf page”).
- Att bädda in **QR codes** som länkar till verifieringstjänster.
- Att automatisera processen i ett ASP.NET Core‑API för dynamisk PDF‑generering.

Kom ihåg att nyckeln till robust PDF‑automation är tydlig ansvarsfördelning: signaturhantering, bildbehandling och slutlig dokumentmontering. Lek med koordinaterna, byt bildformat eller experimentera med tidsstämpling—din arbetsflöde är nu fullt utbyggbart.

Har du frågor, edge‑case‑scenarier eller ett coolt användningsfall att dela? Lämna en kommentar nedan, och lycka till med kodningen!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}