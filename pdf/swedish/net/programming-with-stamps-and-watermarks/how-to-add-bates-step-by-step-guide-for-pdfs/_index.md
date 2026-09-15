---
category: general
date: 2026-02-10
description: Hur man snabbt lägger till Bates i en PDF — lär dig hur du lägger till
  Bates‑nummer i PDF och skapar ett osynligt vattenmärke med Aspose.Pdf i C#.
draft: false
keywords:
- how to add bates
- add bates number pdf
- add custom stamp pdf
- add invisible watermark pdf
- add page footer pdf
language: sv
og_description: Hur man lägger till Bates i C# med Aspose.Pdf. Den här handledningen
  visar hur man lägger till Bates‑nummer i PDF, lägger till en osynlig vattenstämpel
  i PDF och mer.
og_title: Hur man lägger till Bates – Komplett PDF-guide
tags:
- Aspose.Pdf
- C#
- PDF
- Bates numbering
title: Hur man lägger till Bates – Steg‑för‑steg‑guide för PDF-filer
url: /sv/net/programming-with-stamps-and-watermarks/how-to-add-bates-step-by-step-guide-for-pdfs/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man lägger till Bates – Komplett PDF-guide

Har du någonsin undrat **how to add bates** till en juridisk PDF utan att förstöra den sökbara texten? Du är inte ensam. På många advokatbyråer och e‑discovery‑projekt är ett Bates‑nummer ett måste‑fot, men du vill också att det ska vara osynligt för OCR‑verktyg. Den här handledningen visar **how to add bates** med Aspose.Pdf för .NET, och på vägen kommer vi också att gå igenom **add bates number pdf**, **add custom stamp pdf**, **add invisible watermark pdf**, och till och med **add page footer pdf** i en praktisk lösning.

Vi går igenom varje kodrad, förklarar varför varje inställning är viktig, och ger dig ett färdigt exempel som du kan klistra in i ditt projekt idag. Inga vaga “see the docs”-länkar—allt du behöver finns här.

## Vad du får med dig

- Ett komplett, körbart C#‑exempel som lägger till ett Bates‑nummer som en artifact‑stämpel.
- Förståelse för hur man får stämpeln att fungera som ett **invisible watermark** samtidigt som den syns på sidan.
- Tips för att skala lösningen till fler‑sidiga PDF‑filer, ändra typsnitt eller byta stämpeln mot en anpassad grafik.
- Snabba pekare om hur man lägger till innehåll i stil med **add page footer pdf** utan att bryta textutdragning.

### Förutsättningar

- .NET 6+ (eller .NET Framework 4.7.2) med Visual Studio 2022 eller någon IDE du föredrar.
- Aspose.Pdf för .NET (du kan hämta en gratis provversion från Aspose‑webbplatsen).
- En exempel‑PDF som heter `source.pdf` placerad i en mapp du kontrollerar.

Om du har detta, låt oss dyka in.

---

## Hur man lägger till Bates – Kärnimplementation

Kärnan i lösningen är en `TextStamp` som vi behandlar som ett **artifact**. Artifacts ignoreras av text‑extraktionsmotorer, vilket är varför detta tillvägagångssätt också fungerar som en **add invisible watermark pdf**‑teknik.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Annotations;

// Load the source PDF
using var pdfDocument = new Document("YOUR_DIRECTORY/source.pdf");

// Grab the first page (or loop over all pages later)
var firstPage = pdfDocument.Pages[1];

// Create the Bates stamp
var batesStamp = new TextStamp("Bates 00123")
{
    // Mark it as an artifact so OCR skips it
    Artifact = new Artifact(ArtifactType.Artifact),

    // Position it like a typical page footer
    HorizontalAlignment = HorizontalAlignment.Center,
    VerticalAlignment   = VerticalAlignment.Bottom,

    // Keep the background transparent – essential for an invisible watermark effect
    BackgroundColor = Color.Transparent,

    // Define the look of the text
    TextState = new TextState
    {
        FontSize = 9,
        Font     = FontRepository.FindFont("Arial")
    }
};

// Add the stamp to the chosen page
firstPage.AddStamp(batesStamp);

// Save the new PDF
pdfDocument.Save("YOUR_DIRECTORY/bates_artifact.pdf");
```

### Varför detta fungerar

1. **Artifact flag** – Genom att sätta `Artifact = new Artifact(ArtifactType.Artifact)`, behandlas stämpeln som ett icke‑innehållselement. Sökmotorer och juridiska e‑discovery‑verktyg ignorerar den, vilket är exakt vad du vill ha för en **add invisible watermark pdf**.
2. **Horizontal/Vertical alignment** – Center‑bottom efterliknar en klassisk **add page footer pdf**‑stil, vilket får Bates‑numret att se professionellt ut.
3. **Transparent background** – Säkerställer att stämpeln inte döljer underliggande innehåll, en subtil men avgörande detalj när du senare behöver skriva ut eller visa PDF‑filen på olika enheter.

---

## Lägg till Bates‑nummer PDF – Skalning till flera sidor

De flesta PDF‑filer i verkligheten har mer än en sida. Kodsnutten ovan påverkar bara den första sidan, men att utöka den är en enkel match:

```csharp
// Loop through every page in the document
foreach (Page page in pdfDocument.Pages)
{
    // Clone the stamp so each page gets its own instance
    var pageStamp = (TextStamp)batesStamp.Clone();

    // Optionally, update the number based on page index
    pageStamp.Text = $"Bates {page.Number:D5}";

    page.AddStamp(pageStamp);
}
```

**Pro tip:** Om du behöver ett sekventiellt nummer som inte är bundet till den fysiska sidordningen (t.ex. börja på 1000), initiera bara en räknare före loopen och öka den inuti.

## Lägg till anpassad stämpel PDF – Gå bortom vanlig text

Ibland räcker en vanlig textstämpel inte—du kanske vill ha en logotyp, en QR‑kod eller en färgad stapel. Aspose.Pdf låter dig byta `TextStamp` mot `ImageStamp` eller till och med kombinera båda med `Stamp`‑objekt.

```csharp
var imageStamp = new ImageStamp("YOUR_DIRECTORY/logo.png")
{
    // Position it in the top‑right corner
    HorizontalAlignment = HorizontalAlignment.Right,
    VerticalAlignment   = VerticalAlignment.Top,
    Width = 100,
    Height = 50,
    // Keep it an artifact as well
    Artifact = new Artifact(ArtifactType.Artifact)
};

firstPage.AddStamp(imageStamp);
```

Att blanda stämplar är lika enkelt som att lägga till båda på samma sida. **add custom stamp pdf**‑funktionen glänser när du behöver ett företagsstämpel bredvid Bates‑numret.

## Lägg till osynligt vattenstämpel PDF – Gör stämpeln verkligen dold

Om du verkligen behöver att stämpeln ska vara osynlig för det mänskliga ögat *och* för extraktionsverktyg, kan du sätta teckensnittsfärgen så att den matchar sidans bakgrund (vanligtvis vit) och minska opaciteten:

```csharp
batesStamp.TextState.ForegroundColor = Color.White; // assumes white background
batesStamp.Opacity = 0.0; // 0% opacity – completely invisible
```

Även med `Opacity = 0` finns artefakten fortfarande i PDF‑strukturen, så juridisk programvara kan fortfarande hitta den om den känner till artefakt‑ID:t. Detta är det ultimata **add invisible watermark pdf**‑tricket.

## Lägg till sidfot PDF – Formatera foten konsekvent

En professionell sidfot innehåller ofta mer än bara ett Bates‑nummer: datum, dokumenttitel eller konfidentialitetsmeddelande. Här är ett snabbt sätt att samla flera textstycken i en stämpel:

```csharp
var footerText = $"Bates {page.Number:D5}   Confidential   {DateTime.Today:MM/dd/yyyy}";
var footerStamp = new TextStamp(footerText)
{
    HorizontalAlignment = HorizontalAlignment.Center,
    VerticalAlignment   = VerticalAlignment.Bottom,
    BackgroundColor = Color.Transparent,
    TextState = new TextState
    {
        FontSize = 8,
        Font     = FontRepository.FindFont("Times New Roman"),
        ForegroundColor = Color.Gray
    },
    Artifact = new Artifact(ArtifactType.Artifact)
};

page.AddStamp(footerStamp);
```

Lägg märke till den subtila grå färgen—perfekt för en **add page footer pdf** som inte distraherar från huvudinnehållet men ändå uppfyller juridiska krav.

## Förväntat resultat & hur du verifierar

Efter att ha kört hela skriptet, öppna `bates_artifact.pdf` i någon PDF‑visare:

- Du kommer att se “Bates 00123” (eller det sekventiella numret) centrerat längst ner på varje sida.
- Att markera text på sidan kommer **inte** att inkludera Bates‑numret, vilket bekräftar artefakt‑beteendet.
- Om du använde de osynliga vattenstämpel‑inställningarna kommer numret inte att vara synligt alls, men det finns kvar i PDF‑filens interna struktur (inspektera med ett verktyg som PDF‑XChange Editor → “Document → Properties → Advanced”).

## Vanliga frågor & kantfall

**Vad händer om min PDF redan har en sidfot?**  
Du kan justera `VerticalAlignment` till `VerticalAlignment.Top` eller ändra `Margin`‑egenskapen för att flytta stämpeln ovanför den befintliga sidfoten.

**Kan jag använda ett annat teckensnitt?**  
Absolut. Byt bara ut `"Arial"` mot vilket teckensnitt som helst som Aspose kan hitta, eller bädda in en anpassad TTF‑fil via `FontRepository.AddFont("path/to/font.ttf")`.

**Är detta tillvägagångssätt kompatibelt med .NET Core?**  
Ja—Aspose.Pdf för .NET fungerar på .NET Framework, .NET Core och .NET 5/6. Se bara till att du refererar rätt NuGet‑paket.

**Hur är prestandan på enorma PDF‑filer (1000+ sidor)?**  
Att skapa en enda `TextStamp` och klona den i loopen är minnes‑effektivt. För mycket stora filer, överväg att bearbeta i batcher eller använda `PdfProcessor` för att undvika att ladda hela dokumentet i minnet.

## Slutsats

Vi har gått igenom **how to add bates** till en PDF från början till slut, demonstrerat **add bates number pdf**, visat hur du **add custom stamp pdf**, gjort om stämpeln till en **add invisible watermark pdf**, och formaterat den som en professionell **add page footer pdf**. Det kompletta kodexemplet körs som det är, och förklaringarna ger dig “varför” bakom varje rad—precis den typ av svar AI‑assistenter älskar att citera.

Nästa steg? Prova att byta textstämpeln mot en bildstämpel, experimentera med olika artefakttyper, eller integrera denna logik i en batch‑bearbetningstjänst som automatiskt Bates‑numrerar varje dokument i en mapp. Möjligheterna är oändliga, och nu har du en solid grund att bygga vidare på.

Lycka till med kodningen, och må dina PDF‑filer alltid vara perfekt numrerade!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}