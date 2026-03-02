---
category: general
date: 2026-01-02
description: Lägg till sidnummer i PDF snabbt med Aspose.Pdf i C#. Lär dig att lägga
  till Bates‑nummerering, sidfotstext, anpassat vattenstämpel och loopa igenom PDF‑sidor
  i ett enda skript.
draft: false
keywords:
- add page numbers pdf
- add bates numbering
- add footer text
- add custom watermark
- loop through pdf pages
language: sv
og_description: Lägg till sidnummer i PDF omedelbart med Aspose.Pdf. Denna guide täcker
  också hur du lägger till Bates‑nummerering, sidfotstext, anpassat vattenstämpel
  och loopar igenom PDF‑sidor.
og_title: Lägg till sidnummer i PDF med C# – Komplett programmeringshandledning
tags:
- C#
- Aspose.Pdf
- PDF manipulation
title: Lägg till sidnummer i PDF med C# – Fullständig steg‑för‑steg‑guide
url: /sv/net/programming-with-pdf-pages/add-page-numbers-pdf-with-c-full-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Lägg till sidnummer i PDF med C# – Komplett programmeringshandledning

Har du någonsin behövt **lägga till sidnummer i pdf**‑filer men inte vetat var du ska börja? Du är inte ensam—utvecklare frågar ständigt hur man stämplar nummer, sidfötter eller till och med en Bates‑liknande identifierare på varje sida i en PDF.  

I den här handledningen får du se ett färdigt C#‑exempel som **loopar igenom pdf‑sidor**, lägger till en sidnummer‑sidfot och (om du vill) lägger till en anpassad vattenstämpel. Vi visar också hur du byter stämpeln till ett Bates‑nummer, vilket i praktiken betyder “lägg till Bates‑numrering” för juridiska eller forensiska dokument. I slutet har du en enda, återanvändbar metod som hanterar alla dessa uppgifter utan att du blir svettig.

## Lägg till sidnummer i pdf – Översikt

Innan vi dyker ner i koden, låt oss klargöra vad “lägga till sidnummer i pdf” egentligen betyder i Aspose.Pdf‑världen. Biblioteket behandlar varje textstycke du placerar på en sida som en **TextStamp**. Genom att skapa en stämpel med en sidplatshållare (`{page}`) och applicera den på varje sida får du automatiskt sekventiell numrering. Samma stämpel kan även innehålla extra text, så du kan **lägga till sidfotstext** som “Confidential” eller en ärendespecifik identifierare.

> **Varför använda en stämpel istället för att redigera PDF‑innehållsströmmen?**  
> Stämplar är hög‑nivå‑objekt som respekterar sidmarginaler, rotation och befintlig grafik. De är också mycket enklare att underhålla—ändra bara några egenskaper och kör skriptet igen.

## Loopa igenom PDF‑sidor för att applicera stämplar

Det första praktiska steget är att öppna käll‑PDF‑filen och iterera över dess sidor. Detta är det klassiska **loopa igenom pdf‑sidor**‑mönstret som de flesta Aspose‑exempel använder.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Paths – change these to match your environment
string sourcePdfPath = @"C:\Docs\input.pdf";
string outputPdfPath = @"C:\Docs\PageNumbered.pdf";

using (var pdfDocument = new Document(sourcePdfPath))
{
    // The loop – every Page object lives in pdfDocument.Pages
    foreach (Page page in pdfDocument.Pages)
    {
        // We'll attach a stamp later (see next section)
    }

    // Save the modified document
    pdfDocument.Save(outputPdfPath);
}
```

> **Proffstips:** Om din PDF är enorm (hundratals sidor), överväg att bearbeta den i batcher för att hålla minnesanvändningen låg. Aspose.Pdf strömmar sidorna lat, så loopen i sig är redan ganska effektiv.

## Lägg till Bates‑numrering och sidfotstext

Nu när vi kan gå igenom varje sida, låt oss skapa en **återanvändbar TextStamp** som innehåller både sidnumret och valfri sidfotstext. Platshållaren `{page}` ersätts automatiskt av det aktuella sidnumret.

```csharp
// Create a stamp that will be reused for every page
var batesStamp = new TextStamp("Bates-{page} – Confidential")
{
    // Position the stamp 20 points from the left and bottom edges
    XIndent = 20,
    YIndent = 20,
    // Align left‑bottom so it behaves like a traditional footer
    HorizontalAlignment = HorizontalAlignment.Left,
    VerticalAlignment   = VerticalAlignment.Bottom,
    // Font styling – Times New Roman, 10pt, bold, gray
    Font = new Font(FontFamily.TimesRoman, 10, FontStyle.Bold),
    TextState = { ForegroundColor = Color.Gray }
};

// Attach the stamp to every page
foreach (Page page in pdfDocument.Pages)
    page.AddStamp(batesStamp);
```

### Varför detta fungerar

* **`Bates-{page}`** – Aspose ersätter `{page}` med det faktiska sidnumret och ger dig automatiskt en klassisk Bates‑nummer.
* **`Confidential`** – Detta är delen för **lägga till sidfotstext**. Du kan ersätta den med vilken sträng som helst, till och med hämta data från en databas.
* **Stil** – Genom att använda `TextState` kan du justera färg, opacitet och även rotation utan att röra PDF‑ens interna innehållsströmmar.

Om du bara behöver rena siffror, ta bort “Bates‑”‑prefixet och den extra texten:

```csharp
var simpleStamp = new TextStamp("{page}")
{
    XIndent = 20,
    YIndent = 20,
    HorizontalAlignment = HorizontalAlignment.Center,
    VerticalAlignment   = VerticalAlignment.Bottom,
    Font = new Font(FontFamily.Helvetica, 12, FontStyle.Regular),
    TextState = { ForegroundColor = Color.Black }
};
```

## Lägg till en anpassad vattenstämpel (valfritt)

Ibland vill du ha mer än en sidfot—du behöver en halvtransparent logotyp eller ett “UTKAST”‑överlägg över hela sidan. Det är då **lägga till anpassad vattenstämpel** kommer in i bilden. Samma `TextStamp`‑klass kan återanvändas, bara ändra dess justering och opacitet.

```csharp
var watermark = new TextStamp("DRAFT")
{
    // Center it both horizontally and vertically
    HorizontalAlignment = HorizontalAlignment.Center,
    VerticalAlignment   = VerticalAlignment.Center,
    // Make it big and light
    Font = new Font(FontFamily.Helvetica, 72, FontStyle.Bold),
    TextState = { ForegroundColor = Color.Red, FontSize = 72, FontStyle = FontStyle.Bold, 
                  Transparency = 0.5f }   // 50% transparent
};

// Apply the watermark on top of the page‑number stamp
foreach (Page page in pdfDocument.Pages)
{
    page.AddStamp(watermark);   // watermark on top
    page.AddStamp(batesStamp);  // then the footer
}
```

> **Obs:** Ordningen är viktig. Att lägga till vattenstämpeln först säkerställer att sidnumren förblir läsbara ovanpå den halvtransparenta texten.

## Spara PDF‑filen och verifiera resultatet

Efter stämpling är sista steget att skriva tillbaka ändringarna till disk. `Save`‑anropet vi placerade tidigare gör det tunga arbetet, men låt oss lägga till ett snabbt verifieringssnutt som öppnar den nya filen och skriver ut hur många sidor som bearbetades.

```csharp
pdfDocument.Save(outputPdfPath);

// Quick verification
using (var resultDoc = new Document(outputPdfPath))
{
    Console.WriteLine($"✅ Successfully added page numbers to {resultDoc.Pages.Count} pages.");
}
```

När du kör hela programmet bör du se en PDF där varje sida avslutas med något i stil med **“Bates‑3 – Confidential”** (eller bara “3” om du använde den enkla stämpeln) och, om du aktiverade vattenstämpeln, ett svagt “UTKAST” över mitten.

### Förväntad utdata

| Sida | Sidfot (exempel) |
|------|------------------|
| 1    | Bates‑1 – Confidential |
| 2    | Bates‑2 – Confidential |
| …    | … |
| N    | Bates‑N – Confidential |

Om du öppnade filen i en visare kommer siffrorna att ligga 20 pt från vänster‑ och bottenmarginalerna, i enlighet med vanliga juridiska dokumentkonventioner.

## Fullt fungerande exempel (klar för kopiering)

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

string sourcePdfPath = @"C:\Docs\input.pdf";
string outputPdfPath = @"C:\Docs\PageNumbered.pdf";

using (var pdfDocument = new Document(sourcePdfPath))
{
    // ---------- Create the page‑number/footer stamp ----------
    var batesStamp = new TextStamp("Bates-{page} – Confidential")
    {
        XIndent = 20,
        YIndent = 20,
        HorizontalAlignment = HorizontalAlignment.Left,
        VerticalAlignment   = VerticalAlignment.Bottom,
        Font = new Font(FontFamily.TimesRoman, 10, FontStyle.Bold),
        TextState = { ForegroundColor = Color.Gray }
    };

    // ---------- Optional watermark ----------
    var watermark = new TextStamp("DRAFT")
    {
        HorizontalAlignment = HorizontalAlignment.Center,
        VerticalAlignment   = VerticalAlignment.Center,
        Font = new Font(FontFamily.Helvetica, 72, FontStyle.Bold),
        TextState = { ForegroundColor = Color.Red, Transparency = 0.5f }
    };

    // ---------- Apply stamps to every page ----------
    foreach (Page page in pdfDocument.Pages)
    {
        page.AddStamp(watermark);   // comment out if you don't need a watermark
        page.AddStamp(batesStamp);
    }

    // ---------- Save and verify ----------
    pdfDocument.Save(outputPdfPath);
    Console.WriteLine($"✅ Added page numbers and watermark to {pdfDocument.Pages.Count} pages.");
}
```

Spara detta som `AddPageNumbers.cs`, återställ Aspose.Pdf‑NuGet‑paketet (`Install-Package Aspose.Pdf`), och kör det. Du får en **lägga till sidnummer i pdf**‑fil som också demonstrerar **lägga till Bates‑numrering**, **lägga till sidfotstext**, **lägga till anpassad vattenstämpel**, och det klassiska **loopa igenom pdf‑sidor**‑mönstret—allt i ett prydligt skript.

![lägga till sidnummer i pdf‑exempel](https://example.com/images/add-page-numbers-pdf.png "Skärmbild som visar numrerade PDF‑sidor med sidfot och vattenstämpel")

## Slutsats

Vi har gått igenom allt du behöver för att **lägga till sidnummer i pdf**‑filer med Aspose.Pdf i C#. Från att loopa igenom varje sida, till att stämpla Bates‑nummer, lägga till anpassad sidfotstext och till och med lägga ett halvtransparent vattenstämpel‑lager, koden är kompakt nog att slänga in i vilket befintligt projekt som helst.  

Nästa steg kan vara att utforska mer avancerade scenarier—som att hämta sidfotstexten från en databas, använda olika typsnitt per avsnitt, eller generera en separat index‑PDF som listar alla Bates‑nummer. Alla dessa utökningar bygger på samma grundidéer som vi visat här, så du är väl förberedd att expandera lösningen i takt med att dina krav växer.  

Prova det, justera stilen, och låt mig veta i kommentarerna hur det fungerade för dig. Lycka till med kodandet!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}