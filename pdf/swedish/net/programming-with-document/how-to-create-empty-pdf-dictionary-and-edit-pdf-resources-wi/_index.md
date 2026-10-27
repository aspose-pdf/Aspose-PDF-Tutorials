---
category: general
date: 2026-10-26
description: Lär dig att skapa en tom PDF‑ordbok och redigera PDF‑resurser med Aspose.PDF
  för C#. Steg‑för‑steg‑guide med komplett kodexempel.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create empty PDF dictionary
- edit PDF resources
- Aspose.PDF C#
- PDF manipulation C#
- PDF graphics state
language: sv
lastmod: 2026-10-26
og_description: Skapa en tom PDF‑ordbok och redigera PDF‑resurser med Aspose.PDF för
  C#. Följ den här kompletta handledningen för att ändra grafiklägen i PDF‑filer.
og_image_alt: Screenshot showing creation of empty PDF dictionary in Aspose.PDF
og_title: Skapa tom PDF-ordbok och redigera PDF-resurser i C# – Aspose.PDF-guide
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn to create empty PDF dictionary and edit PDF resources using Aspose.PDF
    for C#. Step‑by‑step guide with full code example.
  headline: How to create empty PDF dictionary and edit PDF resources with Aspose.PDF
    in C#
  type: TechArticle
- description: Learn to create empty PDF dictionary and edit PDF resources using Aspose.PDF
    for C#. Step‑by‑step guide with full code example.
  name: How to create empty PDF dictionary and edit PDF resources with Aspose.PDF
    in C#
  steps:
  - name: Populate the graphics state entries
    text: 'Add the standard keys:'
  - name: Register the new graphics state in the resource dictionary
    text: Give the state a name (`GS0`) and add it to the `ExtGState` dictionary that
      lives inside the page resources.
  - name: Expected output
    text: 'Running the program prints:'
  type: HowTo
tags:
- Aspose.PDF
- C#
- PDF
title: Hur man skapar en tom PDF-ordbok och redigerar PDF-resurser med Aspose.PDF
  i C#
url: /sv/net/programming-with-document/how-to-create-empty-pdf-dictionary-and-edit-pdf-resources-wi/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man skapar en tom PDF-ordbok och redigerar PDF-resurser med Aspose.PDF i C#

Om du behöver **create empty PDF dictionary** och sedan **edit PDF resources** i en C#-applikation, visar den här guiden de exakta stegen. Du kommer att se ett komplett, körbart exempel som lägger till ett anpassat graphics state på den första sidan i en befintlig PDF.

Att arbeta med låg‑nivå PDF-objekt kan kännas skrämmande, men Aspose.PDF erbjuder ett tydligt API för ordboksmanipulation. I slutet av den här handledningen kommer du att förstå varför varje operation är viktig och hur du anpassar koden för andra resurstyp.

## Förutsättningar

* .NET 6.0 (eller senare) installerat.
* En licensierad kopia av **Aspose.PDF for .NET** – den kostnadsfria provversionen fungerar för testning.
* En IDE såsom Visual Studio 2022.
* En PDF‑fil med namnet `input.pdf` placerad i en mapp som du kan referera till från koden.

Inga ytterligare NuGet‑paket krävs utöver `Aspose.Pdf`.

## Steg 1: Ställ in projektet och importera namnrymder

Skapa ett nytt konsolprojekt och lägg till Aspose.PDF‑paketet:

```bash
dotnet new console -n PdfDictionaryDemo
cd PdfDictionaryDemo
dotnet add package Aspose.Pdf
```

I `Program.cs` importerar du de namnrymder du kommer att använda:

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Cos;
```

Dessa importeringar exponerar klasserna `Document`, `DictionaryEditor` och COS (Canonical Object Structure) som låter dig **create empty PDF dictionary**‑objekt och modifiera befintliga resurs‑ordböcker.

## Steg 2: Definiera mappen som innehåller PDF‑filerna

Ange katalogen som innehåller `input.pdf`. Att använda en absolut sökväg undviker tvetydighet när programmet körs från en annan arbetskatalog.

```csharp
// Step 1: Define the folder that contains the PDF files
string dataDir = @"C:\PdfDemo\";
```

Byt ut `C:\PdfDemo\` mot sökvägen på din maskin. Att hålla sökvägen i en variabel gör det enkelt att återanvända den för både in- och utdatafiler.

## Steg 3: Öppna källdokumentet PDF

Läs in PDF‑filen du vill modifiera inom ett `using`‑block så att filhandtaget frigörs automatiskt.

```csharp
// Step 2: Open the source PDF document
using (var pdfDocument = new Document(dataDir + "input.pdf"))
{
    // The rest of the workflow lives inside this block
}
```

När du öppnar dokumentet får du åtkomst till dess sidcollection, resurs‑ordböcker och låg‑nivå COS‑objekt.

## Steg 4: Åtkomst till den första sidan och dess resurs‑ordbok

Den första sidan indexeras med `1` (PDF‑sidor är 1‑baserade). Hämta sidans `Resources`‑ordbok och omslut den i en `DictionaryEditor` för att möjliggöra säker redigering.

```csharp
// Step 3: Access the first page and its resource dictionary
var firstPage = pdfDocument.Pages[1];
var resourcesEditor = new DictionaryEditor(firstPage.Resources);
```

`DictionaryEditor` abstraherar den underliggande COS‑strukturen, vilket låter dig läsa eller skapa poster utan att förstöra PDF‑filen.

## Steg 5: **Create empty PDF dictionary** för ett nytt graphics state

Ett graphics state styr transparens, blandningsläge och andra ritparametrar. För att lägga till ett anpassat state behöver du först en tom ordbok, sedan fylla den med de nödvändiga posterna.

```csharp
// Step 4: Retrieve the ExtGState dictionary and add a new graphics state
var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();

// Create an empty dictionary that will hold the graphics state parameters
var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
```

Anropet till `CreateEmptyDictionary` är kärnan i **creating empty PDF dictionary**‑objekt. Det returnerar en COS‑ordbok som tillhör samma dokument, vilket säkerställer korsreferensintegritet.

### Fyll i graphics state‑posterna

Lägg till standardnycklarna:

* `CA` – stroking‑alfa‑konstant (intervall 0 – 1).
* `ca` – non‑stroking‑alfa‑konstant.
* `BM` – namn på blend‑läge.

```csharp
var graphicsStateEntries = new[]
{
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
};

foreach (var entry in graphicsStateEntries)
    newGraphicsState.Add(entry);
```

Varje post läggs till i den tomma ordbok du just skapade. Genom att separera definitionen från insättningsloopen håller du koden läsbar och gör det enkelt att utöka med ytterligare nycklar senare.

### Registrera det nya graphics state i resurs‑ordboken

Ge state ett namn (`GS0`) och lägg till det i `ExtGState`‑ordboken som finns i sidans resurser.

```csharp
// Name the new graphics state "GS0"
extGStateDict.Add("GS0", newGraphicsState);
```

Nu innehåller sidans resurs‑ordbok en referens till det anpassade graphics state, som du senare kan applicera på innehållsströmmar.

## Steg 6: Spara den uppdaterade PDF‑filen

Slutligen skriver du det modifierade dokumentet till en ny fil. Att behålla originalet intakt hjälper dig att verifiera ändringarna.

```csharp
// Step 5: Save the updated PDF
pdfDocument.Save(dataDir + "output.pdf");
```

När du öppnar `output.pdf` i en visare som stöder inspektion av graphics state (t.ex. Adobe Acrobat Pro) kommer du att se att `ExtGState`‑ordboken innehåller en post med namnet `GS0` med de värden du definierade.

## Fullständig källkod

När alla bitar sätts ihop får du ett självständigt program:

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Cos;

class Program
{
    static void Main()
    {
        // Step 1: Define the folder that contains the PDF files
        string dataDir = @"C:\PdfDemo\"; // adjust to your environment

        // Step 2: Open the source PDF document
        using (var pdfDocument = new Document(dataDir + "input.pdf"))
        {
            // Step 3: Access the first page and its resource dictionary
            var firstPage = pdfDocument.Pages[1];
            var resourcesEditor = new DictionaryEditor(firstPage.Resources);

            // Step 4: Retrieve the ExtGState dictionary and add a new graphics state
            var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();

            // **Create empty PDF dictionary** for the new graphics state
            var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            var graphicsStateEntries = new[]
            {
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
            };

            foreach (var entry in graphicsStateEntries)
                newGraphicsState.Add(entry);

            // Register the new graphics state as "GS0"
            extGStateDict.Add("GS0", newGraphicsState);

            // Step 5: Save the updated PDF
            pdfDocument.Save(dataDir + "output.pdf");
        }

        Console.WriteLine("PDF updated successfully.");
    }
}
```

### Förväntad utdata

När programmet körs skrivs följande ut:

```
PDF updated successfully.
```

och skapar `output.pdf` i samma mapp. När du öppnar filen visas en ny post under **Resources → ExtGState → GS0** med de parametrar du angav.

## Vanliga variationer och specialfall

| Situation | Hur man anpassar koden |
|-----------|-----------------------|
| **Multiple pages** behöver samma graphics state | Skapa ordboken en gång, och lägg sedan till samma `GS0`‑referens i varje sidas `ExtGState`‑ordbok. |
| **Different blend mode** (t.ex. `Multiply`) | Ändra värdet `CosPdfName("Normal")` till `CosPdfName("Multiply")`. |
| **No existing ExtGState dictionary** | Innan du får åtkomst till `resourcesEditor["ExtGState"]`, kontrollera `resourcesEditor.ContainsKey("ExtGState")`. Om den saknas, skapa en ny tom ordbok och lägg till den i `firstPage.Resources`. |
| **Large PDFs** orsakar minnespress | Använd `PdfDocument.Load`‑överladdning som strömmar sidor, eller bearbeta sidor en åt gången inom `using`‑blocket. |
| **Need to edit other resources** (fonter, XObjects) | Byt ut `"ExtGState"` mot `"Font"` eller `"XObject"` i `resourcesEditor`‑uppslagningen, och följ sedan samma mönster för att skapa en tom ordbok och fylla den. |

Dessa variationer visar hur samma **create empty PDF dictionary**‑mönster gäller för vilken resurstyp du än vill **edit PDF resources**.

## Pro‑tips

* **Validate the result** – efter att du har sparat, öppna PDF‑filen i ett verktyg som kan visa den råa resurs‑ordboken (t.ex. PDF‑Box’s `PDFDebugger`) för att säkerställa att posten finns.
* **Reuse dictionaries** – om du lägger till samma graphics state på många sidor, lagra ordboken i en variabel och referera till den istället för att återskapa den varje gång.
* **Version compatibility** – koden fungerar med Aspose.PDF 23.12 och senare. Tidigare versioner kan kräva `CosDictionary` istället för `CosPdfDictionary`.

## Slutsats

Du vet nu hur man **create empty PDF dictionary**‑objekt och **edit PDF resources** med Aspose.PDF för C#. Handledningen täckte att öppna ett dokument, komma åt sidans resurs‑ordbok, bygga ett anpassat graphics state, registrera det och spara resultatet. Härifrån kan du experimentera med andra resurs‑typer, kombinera flera graphics states eller integrera tekniken i en större PDF‑bearbetningspipeline.

---

*Redo att utforska mer? Prova att lägga till en anpassad **ExtGState** i ett innehållsflöde, eller manipulera **Font**‑ordboken för att bädda in nya fonter. Båda följer samma mönster för att skapa en tom ordbok och redigera PDF‑resurser.*

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig behärska ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Redigera PDF‑resurs‑ordbok med Aspose.PDF – C#‑guide](/pdf/english/net/programming-with-operators/edit-pdf-resource-dictionary-with-aspose-pdf-c-guide/)
- [Skapa anpassat graphics state i PDF med Aspose.Pdf](/pdf/english/net/programming-with-operators/create-custom-graphics-state-in-pdf-using-aspose-pdf/)
- [Hur man skapar ett tomt graphics state i en PDF med C#](/pdf/english/net/programming-with-operators/how-to-create-empty-graphics-state-in-a-pdf-with-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}