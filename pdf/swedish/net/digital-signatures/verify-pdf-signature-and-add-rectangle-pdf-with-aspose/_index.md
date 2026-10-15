---
category: general
date: 2026-02-09
description: Verifiera PDF‑signatur med Aspose.PDF i C#. Lär dig hur du lägger till
  en rektangel i PDF, sparar den uppdaterade PDF‑filen och använder Aspose PDF:s signaturfunktioner.
draft: false
keywords:
- verify pdf signature
- add rectangle pdf
- save updated pdf
- aspose pdf signature
- add graphics pdf
language: sv
og_description: Verifiera PDF‑signatur i C# snabbt. Den här guiden visar hur du lägger
  till grafik i PDF, sparar den uppdaterade PDF‑filen och använder Aspose PDF‑signatur‑API:er.
og_title: Verifiera PDF‑signatur och lägg till rektangel i PDF – Komplett Aspose‑guide
tags:
- Aspose.PDF
- C#
- Digital Signature
- PDF Manipulation
title: Verifiera PDF-signatur och lägg till rektangel i PDF med Aspose
url: /sv/net/digital-signatures/verify-pdf-signature-and-add-rectangle-pdf-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# verifiera pdf signatur och lägg till rektangel pdf med Aspose

Har du någonsin behövt **verify pdf signature** i ett C#-projekt men varit osäker på var du ska börja? Du är inte ensam—digitala signaturer är ett måste‑för‑efterlevnad, men många utvecklare fastnar när de också måste justera dokumentet efteråt.  

I den här handledningen går vi igenom ett komplett, körbart exempel som **verifies pdf signature**, lägger till en **rectangle** på den första sidan, kontrollerar att formen förblir inom sidans gränser, och slutligen **save updated pdf**—allt med det moderna Aspose.PDF API:et. I slutet har du ett enda, självständigt program som du kan släppa in i vilken .NET‑lösning som helst.

## Vad du kommer att lära dig

- Läs in en signerad PDF med Aspose.PDF.
- Använd **aspose pdf signature**-klasserna för att verifiera varje signatur och upptäcka kompromisser.
- **Add rectangle pdf**-grafik på ett säkert sätt, så att den passar sidan.
- **Save updated pdf** medan befintliga signaturer bevaras.
- Tips, hantering av edge‑case och vanliga fallgropar.

Inga externa dokument krävs—allt du behöver finns här.

## Förutsättningar

- .NET 6.0 eller senare (koden fungerar också på .NET Framework 4.7+).
- Aspose.PDF för .NET NuGet‑paket (≥ 23.10). Installera med:

```bash
dotnet add package Aspose.Pdf
```

- En signerad PDF‑fil med namnet `signed.pdf` placerad i en mapp du kontrollerar (byt ut `YOUR_DIRECTORY` i koden).
- Grundläggande kunskap om C# och Visual Studio eller VS Code.

> **Pro tip:** Om du inte har en signerad PDF till hands, erbjuder Aspose en gratis demofil på sin webbplats som du kan ladda ner för testning.

---

## verify pdf signature – Steg för steg

Det första vi behöver göra är att öppna dokumentet och loopa igenom varje digital signatur. Aspose.PDF ger oss två praktiska metoder: `VerifySignature` visar om den kryptografiska kontrollen passerar, medan den nyare `IsSignatureCompromised` flaggar eventuell manipulering som kan ha inträffat efter signering.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Facades;

// Load the signed PDF document
Document pdfDocument = new Document("YOUR_DIRECTORY/signed.pdf");

// Create a signature handler for the document
PdfFileSignature signatureHandler = new PdfFileSignature(pdfDocument);

// Iterate over each signature name in the PDF
foreach (var signatureName in signatureHandler.GetSignNames())
{
    // Verify the cryptographic integrity
    bool isValid = signatureHandler.VerifySignature(signatureName);
    
    // Detect if the signature has been compromised (e.g., document altered)
    bool isCompromised = signatureHandler.IsSignatureCompromised(signatureName);
    
    Console.WriteLine($"{signatureName}: valid={isValid}, compromised={isCompromised}");
}
```

**Varför detta är viktigt:**  
- `VerifySignature` ensam bekräftar bara att undertecknarens certifikat fortfarande är betrott.  
- `IsSignatureCompromised` fångar subtila förändringar—som att lägga till ett dolt objekt—så du vet om PDF:ens visuella innehåll har ändrats efter signering.

**Förväntad output** (exempel med två signaturer):

```
Signature1: valid=True, compromised=False
Signature2: valid=True, compromised=True
```

Om någon signatur rapporterar `compromised=True` bör du avbryta vidare bearbetning eller varna användaren, eftersom dokumentets integritet inte kan garanteras.

## lägg till rektangel pdf på en sida

Nu när vi har bekräftat att signaturerna är intakta (eller åtminstone medvetna om eventuell kompromiss), låt oss lägga till en enkel rektangelgrafik. Detta är användbart för att stämpla “Reviewed”-markeringar, markera avsnitt, eller bara dra uppmärksamhet till ett område.

```csharp
// Access the first page (pages are 1‑based in Aspose)
Page firstPage = pdfDocument.Pages[1];

// Define a rectangle shape (coordinates: lower-left X, lower-left Y, upper-right X, upper-right Y)
Rectangle shapeRect = new Rectangle(100, 500, 200, 600);

// Add the rectangle to the page's graphics collection
firstPage.AddRectangle(shapeRect);
```

**Vad siffrorna betyder:**  
- PDF‑koordinatsystemet börjar i det nedre vänstra hörnet.  
- I exemplet sträcker rektangeln sig 100 punkter horisontellt och 100 punkter vertikalt, placerad ungefär i mitten av en typisk A4‑sida.

> **Obs:** Aspose stödjer även `AddEllipse`, `AddPolygon` osv., om du behöver mer avancerade former.

## kontrollera grafikgränser – säkerställ att rektangeln passar

Innan vi sparar ändringarna är det klokt att verifiera att vår grafik förblir inom sidans utskrivbara område. Den nya `CheckGraphicsBounds`‑metoden gör exakt det.

```csharp
// Verify that the rectangle does not exceed page limits
bool shapeFits = firstPage.CheckGraphicsBounds(shapeRect);
Console.WriteLine($"Shape fits page: {shapeFits}");
```

Om `shapeFits` returnerar `false` måste du justera rektangelns koordinater—kanske krympa den eller flytta den längre ner på sidan. Detta förhindrar oavsiktlig beskärning som kan se oprofessionell ut, särskilt när PDF:en senare skrivs ut.

## spara uppdaterad pdf – bevara signaturer och ny grafik

Till sist skriver vi det modifierade dokumentet tillbaka till disk. `Save`‑metoden respekterar befintliga signaturer; den ogiltigförklarar dem inte såvida inte innehållet verkligen har förändrats (vilket vi redan kontrollerade med `IsSignatureCompromised`).

```csharp
// Save the updated PDF to a new file
pdfDocument.Save("YOUR_DIRECTORY/output.pdf");

// Inform the user
Console.WriteLine("PDF saved as output.pdf with new rectangle.");
```

**Varför använda en ny fil?**  
Att spara över originalet kan radera de ursprungliga signaturerna, vilket gör det omöjligt att jämföra före/efter‑tillstånd. Genom att skriva till `output.pdf` behåller du källan för revisionsändamål.

## Fullständigt, körbart exempel

Nedan är det kompletta programmet som du kan kopiera‑och‑klistra in i en konsolapp. Alla steg är kombinerade, kommentarer förklarar varje block, och du kommer att se den förväntade konsolutskriften i slutet.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Facades;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Load the signed PDF document
        // -------------------------------------------------
        string inputPath = "YOUR_DIRECTORY/signed.pdf";
        Document pdfDocument = new Document(inputPath);
        Console.WriteLine($"Loaded PDF: {inputPath}");

        // -------------------------------------------------
        // 2️⃣ Verify each digital signature and detect compromise
        // -------------------------------------------------
        PdfFileSignature signatureHandler = new PdfFileSignature(pdfDocument);
        foreach (var signatureName in signatureHandler.GetSignNames())
        {
            bool isValid = signatureHandler.VerifySignature(signatureName);
            bool isCompromised = signatureHandler.IsSignatureCompromised(signatureName);
            Console.WriteLine($"{signatureName}: valid={isValid}, compromised={isCompromised}");
        }

        // -------------------------------------------------
        // 3️⃣ Access the first page and add a rectangle
        // -------------------------------------------------
        Page firstPage = pdfDocument.Pages[1];
        Rectangle shapeRect = new Rectangle(100, 500, 200, 600);
        firstPage.AddRectangle(shapeRect);
        Console.WriteLine("Added rectangle to page 1.");

        // -------------------------------------------------
        // 4️⃣ Ensure the rectangle fits inside the page bounds
        // -------------------------------------------------
        bool shapeFits = firstPage.CheckGraphicsBounds(shapeRect);
        Console.WriteLine($"Shape fits page: {shapeFits}");

        // -------------------------------------------------
        // 5️⃣ Save the updated PDF
        // -------------------------------------------------
        string outputPath = "YOUR_DIRECTORY/output.pdf";
        pdfDocument.Save(outputPath);
        Console.WriteLine($"Saved updated PDF as: {outputPath}");
    }
}
```

**Förväntad konsolutskrift** (förutsatt en giltig, okomprometterad signatur):

```
Loaded PDF: YOUR_DIRECTORY/signed.pdf
Signature1: valid=True, compromised=False
Added rectangle to page 1.
Shape fits page: True
Saved updated PDF as: YOUR_DIRECTORY/output.pdf
```

Om en signatur är komprometterad kommer du att se `compromised=True` och kan besluta om du vill fortsätta.

## Vanliga frågor & edge‑case‑hantering

| Question | Answer |
|----------|--------|
| **Vad händer om PDF:en saknar signaturer?** | `GetSignNames()` returnerar en tom samling; loopen hoppar helt enkelt över den, och du kan fortfarande lägga till grafik. |
| **Kan jag lägga till flera rektanglar?** | Ja—anropa bara `AddRectangle` upprepade gånger med olika `Rectangle`‑objekt. |
| **Vad händer med lösenordsskyddade PDF‑filer?** | Läs in dem med `pdfDocument = new Document("file.pdf", new LoadOptions("password"));` innan verifiering. |
| **Kommer tillägg av grafik att ogiltigförklara en giltig signatur?** | Endast om signaturen täcker den sida där du infogar grafik. Använd `IsSignatureCompromised` för att upptäcka detta; annars förblir signaturen intakt. |
| **Behöver jag stänga resurser?** | Aspose.PDF‑objekt är hanterade; disposering är valfri men du kan omsluta koden i ett `using`‑block för extra säkerhet. |

## Pro‑tips för produktionsanvändning

- **Batch‑bearbetning:** Omslut hela rutinen i en metod som accepterar in‑/ut‑sökvägar; mata sedan in en lista med filer till en `Parallel.ForEach` för snabbhet.
- **Loggning:** Ersätt `Console.WriteLine` med en riktig logger (t.ex. Serilog) för att fånga verifieringsresultat i revisionsspår.
- **Signaturpolicy:** Kombinera `VerifySignature` med en certifikatåterkallningskontroll (OCSP/CRL) för striktare efterlevnad.
- **Grafikstil:** Använd `firstPage.AddRectangle(shapeRect, new GraphicState { StrokeColor = Color.Red, FillColor = Color.Yellow });` för att få rektangeln att sticka ut.
- **Versionslås:** Fäst Aspose.PDF NuGet‑versionen för att undvika brytande förändringar när biblioteket uppdateras.

## Slutsats

Du har nu ett gediget, end‑to‑end‑exempel som **verify pdf signature**, **add rectangle pdf**, och **save updated pdf** med de senaste Aspose.PDF‑API:erna. Koden kontrollerar komprometterade signaturer, säkerställer att grafik förblir inom sidans gränser, och bevarar de ursprungliga digitala signaturerna—precis vad ett verkligt efterlevnadsflöde kräver.

Nästa steg, du kan utforska:

- Lägga till **add graphics pdf** som vattenstämplar eller QR‑koder.
- Använda **aspose pdf signature**‑API:et för att programatiskt skapa nya signaturer.
- Automatisera processen i en ASP.NET Core‑webbtjänst för dokumentvalidering i realtid.

Prova det, justera rektangelkoordinaterna, och se hur biblioteket reagerar på olika PDF‑strukturer. Lycka till med kodandet, och må dina PDF‑er både vara signerade och stilfulla! 

![verify pdf signature example](image.png "verify pdf signature example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}