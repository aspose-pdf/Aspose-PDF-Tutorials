---
category: general
date: 2026-03-27
description: Skapa span‑element i C# och lär dig hur du lägger till ett span på en
  sida när du konverterar DOCX till PDF och sparar som PDF. Steg‑för‑steg‑guide för
  utvecklare.
draft: false
keywords:
- create span element
- how to add span
- convert docx to pdf
- add element to page
- save as pdf
language: sv
og_description: Skapa ett span‑element i C# och lär dig hur du lägger till ett span
  på en sida när du konverterar DOCX till PDF, och sedan sparar som PDF. Fullständigt
  kodexempel inkluderat.
og_title: Skapa spanelement och lägg till på sidan – Konvertera DOCX till PDF
tags:
- C#
- DocumentProcessing
- PDFConversion
title: Skapa span-element och lägg till på sidan – Konvertera DOCX till PDF
url: /sv/net/document-conversion/create-span-element-and-add-to-page-convert-docx-to-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa span-element och lägg till på sidan – Konvertera DOCX till PDF

Att skapa **span element** i en DOCX-fil är en vanlig uppgift när du behöver exakt layoutkontroll. I den här handledningen visar vi dig **hur du lägger till ett span** på en sida, **konverterar DOCX till PDF** och **sparar som PDF**—allt i några enkla steg.  

Om du någonsin har stirrat på ett Word-dokument och tänkt, “Jag önskar att jag kunde placera en liten textruta på en exakt koordinat,” så är du på rätt plats. Vi går igenom hela arbetsflödet, från att ladda källfilen till att få ett polerat PDF-resultat.

## Vad du kommer att uppnå

* Ladda en `.docx`-fil med dokumentbibliotekets `Document`-klass.  
* **Skapa span element** med `TaggedContent`-API:t.  
* Placera det spanet på exakta X/Y-koordinater på en vald sida.  
* **Lägg till element på sidan** på ett pålitligt sätt, även när sidan inte är den första.  
* **Konvertera DOCX till PDF** och **spara som PDF** med ett enda `Save`-anrop.

Inga externa verktyg, inga mystiska inställningar—bara ren C#-kod som du kan kopiera‑klistra in i ditt projekt.

## Förutsättningar

* .NET 6+ (eller någon recent .NET-runtime som ditt bibliotek stöder).  
* Det dokumentbehandlings‑SDK som tillhandahåller `Document`, `TaggedContent`, `Position` osv.  
* En grundläggande förståelse för C#-syntax—om du kan skriva en `Console.WriteLine` är du klar.

> **Proffstips:** Håll din SDK-version uppdaterad; den senaste releasen (v3.2 från mars 2026) innehåller prestandaförbättringar för sidnivåoperationer.

---

![Diagram som visar hur man skapar span-element och placerar det på en PDF-sida](https://example.com/images/create-span-element.png "Diagram för placering av span-element")

## Skapa span-element – Positionera och lägg till på sidan

Nedan är den kompletta, körbara koden som gör allt från att ladda källdokumentet DOCX till att skriva den slutgiltiga PDF-filen. Känn dig fri att klistra in den i en konsolapp, justera sökvägarna och köra den.

```csharp
using DocumentProcessing;   // Replace with the actual namespace of your SDK
using DocumentProcessing.Models;

class Program
{
    static void Main()
    {
        // Step 1: Load the DOCX you want to modify
        // -------------------------------------------------
        // The constructor takes a file path; make sure the file exists.
        Document doc = new Document(@"C:\Docs\input.docx");

        // Step 2: Create a new span element using the TaggedContent API
        // -------------------------------------------------
        // A span is a lightweight container for inline content.
        var span = doc.TaggedContent.CreateSpanElement();
        // Optional: add some text inside the span
        span.Text = "Hello, world!";

        // Step 3: Position the span at the desired coordinates (X = 50, Y = 750)
        // -------------------------------------------------
        // Position uses points (1/72 inch). Adjust as needed.
        span.Position = new Position(50, 750);

        // Step 4: Add the span to the target page (page index 1 = second page)
        // -------------------------------------------------
        // Pages are zero‑based; index 1 means the second page in the document.
        doc.Pages[1].Add(span);

        // Step 5: Convert the modified DOCX to PDF and save the result
        // -------------------------------------------------
        // The Save method automatically detects the output format from the extension.
        doc.Save(@"C:\Docs\output.pdf");

        // Confirmation output
        Console.WriteLine("Span added, document converted, and PDF saved successfully.");
    }
}
```

### Steg‑för‑steg-förklaring

#### Steg 1 – Ladda DOCX-dokumentet  
Vi instansierar ett `Document`-objekt som pekar på `input.docx`. Detta objekt representerar hela Word-filen i minnet och ger oss åtkomst till sidor, innehåll och metadata.  

#### Steg 2 – Skapa ett span-element  
`TaggedContent.CreateSpanElement()`‑anropet returnerar en lättvikts‑inline‑behållare. Tänk på den som en liten, osynlig låda som kan hålla text, bilder eller andra inline‑element. Att lägga till text (`span.Text`) är valfritt men användbart för felsökning.

#### Steg 3 – Positionera spanet  
`new Position(50, 750)` sätter det övre vänstra hörnet på spanet 50 pt från vänstermarginalen och 750 pt från sidans topp. Dessa värden är absoluta, så du kan placera spanet var som helst—perfekt för exakta layouter.

#### Steg 4 – Lägg till spanet på målsidan  
`doc.Pages[1].Add(span)` injicerar spanet på den andra sidan. API:t använder noll‑baserad indexering, så sida 0 är den första sidan. Om du behöver lägga till det på den första sidan, använd helt enkelt `doc.Pages[0]`.

#### Steg 5 – Konvertera DOCX till PDF och spara som PDF  
Att anropa `doc.Save("output.pdf")` gör två saker: den skriver det modifierade dokumentet till disk **och** konverterar innehållet till PDF på grund av `.pdf`‑ändelsen. Inget extra konverteringssteg behövs—detta är det enklaste sättet att **spara som PDF**.

---

## Hur man lägger till span på en annan sida (avancerat)

Ibland känner du inte till sidindexet i förväg. Du kan hitta en sida efter dess nummer (mänskligt vänligt) eller genom att söka efter ett specifikt nyckelord.

```csharp
// Find the page that contains the word "Summary"
int targetIndex = doc.Pages
    .Select((p, i) => new { Page = p, Index = i })
    .FirstOrDefault(x => x.Page.Text.Contains("Summary"))?.Index ?? 0;

// Fallback to first page if not found
targetIndex = Math.Max(targetIndex, 0);

// Add the span to the discovered page
doc.Pages[targetIndex].Add(span);
```

**Varför detta är viktigt:** I rapporter där antalet sidor varierar kan hårdkodning av `Pages[1]` bryta layouten. Detta kodsnutt visar ett robust mönster för **hur man lägger till span** dynamiskt.

---

## Vanliga fallgropar och hur man undviker dem

| Problem | Vad händer | Lösning |
|---------|------------|---------|
| **Span inte synligt** | Koordinaterna är utanför sidan eller spanet har noll bredd/höjd. | Dubbelkolla `Position`‑värdena; använd en linjal i din PDF‑visare. |
| **Fel sidindex** | Du lägger till på sida 0 men förväntar dig den på sida 2. | Kom ihåg att API:t är noll‑baserat; lägg till 1 till det mänskliga sidnumret. |
| **Sparar och skriver över källan** | `doc.Save("input.docx")` ersätter den ursprungliga filen. | Spara alltid till en ny sökväg (`output.pdf`) vid konvertering. |
| **Saknad SDK-referens** | Kompileringsfel på `Document`-klassen. | Installera NuGet‑paketet: `dotnet add package DocumentProcessing.SDK`. |

---

## Verifiera resultatet

Efter att programmet har körts, öppna `output.pdf` i någon PDF‑visare. Du bör se texten “Hello, world!” placerad exakt vid (50, 750) på den andra sidan. Om texten visas någon annanstans, justera `Position`‑värdena och kör igen.  

För automatiserade tester kan du använda en PDF‑parser (t.ex. iTextSharp) för att programatiskt verifiera textens koordinater.

```csharp
// Example using iTextSharp to verify position (pseudo‑code)
var pdfReader = new PdfReader(@"C:\Docs\output.pdf");
var page = pdfReader.GetPageContent(2);
Debug.Assert(page.Contains("Hello, world!"));
```

---

## Nästa steg

* **Styla spanet** – utforska `span.Font`, `span.Color` och andra stil‑egenskaper.  
* **Lägg till bilder** – använd `CreateImageElement()` istället för ett span för grafik.  
* **Batch‑behandling** – loopa över en mapp med DOCX-filer

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}