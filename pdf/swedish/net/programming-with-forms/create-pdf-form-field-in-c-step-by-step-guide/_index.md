---
category: general
date: 2026-08-14
description: Skapa PDF-formulärfält snabbt med C#. Lär dig hur du lägger till en textruta
  i PDF och modifierar PDF för att inkludera en textruta med Aspose.PDF.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create pdf form field
- add text box to pdf
- modify pdf to include text box
- Aspose.PDF form field
- C# PDF manipulation
language: sv
lastmod: 2026-08-14
og_description: Skapa PDF-formulärfält med C#. Denna handledning visar hur man lägger
  till en textruta i en PDF och modifierar en PDF för att inkludera en textruta med
  hjälp av Aspose.PDF.
og_image_alt: Screenshot of a PDF page showing a newly added text box form field
og_title: Skapa PDF-formulärfält i C# – komplett programmeringsguide
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: Create pdf form field quickly with C#. Learn how to add text box to
    pdf and modify pdf to include text box using Aspose.PDF.
  headline: Create pdf form field in C# – step‑by‑step guide
  type: TechArticle
- description: Create pdf form field quickly with C#. Learn how to add text box to
    pdf and modify pdf to include text box using Aspose.PDF.
  name: Create pdf form field in C# – step‑by‑step guide
  steps:
  - name: Load the existing PDF document.
    text: Load the existing PDF document.
  - name: Instantiate a `TextBoxField` and configure its name and appearance.
    text: Instantiate a `TextBoxField` and configure its name and appearance.
  - name: Add a widget annotation that defines the visual rectangle on the target
      page.
    text: Add a widget annotation that defines the visual rectangle on the target
      page.
  - name: Insert the field into the document’s form collection.
    text: Insert the field into the document’s form collection.
  - name: Save the modified PDF.
    text: Save the modified PDF.
  - name: Open `output.pdf` in Adobe Acrobat Reader.
    text: Open `output.pdf` in Adobe Acrobat Reader.
  - name: Click inside the “Comments” box; the cursor should appear.
    text: Click inside the “Comments” box; the cursor should appear.
  - name: Type any text and press **Tab** or click elsewhere.
    text: Type any text and press **Tab** or click elsewhere.
  - name: Choose **File → Save As** to persist the entered value.
    text: Choose **File → Save As** to persist the entered value.
  - name: '(Optional) Use Aspose.PDF’s `Form` API to extract the value programmatically:'
    text: '(Optional) Use Aspose.PDF’s `Form` API to extract the value programmatically:'
  type: HowTo
tags:
- pdf
- csharp
- form-fields
title: Skapa PDF‑formulärfält i C# – steg‑för‑steg‑guide
url: /sv/net/programming-with-forms/create-pdf-form-field-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa PDF-formulärfält i C# – steg‑för‑steg‑guide

Om du behöver **skapa PDF-formulärfält** i ett dokument, guidar den här artikeln dig genom hela processen. Du får se exakt hur du **lägger till en textruta i PDF**‑sidor och hur du **modifierar PDF för att inkludera en textruta** med hjälp av Aspose.PDF‑biblioteket för .NET.

Att arbeta med PDF‑formulär är ett vanligt krav för faktureringssystem, enkäter eller någon arbetsflöde som samlar in användarinmatning. I slutet av den här handledningen har du ett återanvändbart kodexempel som skapar ett fullt funktionellt textrutefält, placerar det där du vill och sparar den uppdaterade PDF‑filen – allt utan att lämna ditt C#‑projekt.

## Förutsättningar

Innan du börjar, se till att du har:

* .NET 6.0 eller senare (koden fungerar även med .NET Framework 4.7+)
* Visual Studio 2022 eller någon IDE som stödjer C#
* En aktiv Aspose.PDF för .NET‑licens (gratis provversion fungerar för utveckling)
* En PDF‑fil med namnet `input.pdf` placerad i en känd katalog (handledningen använder `YOUR_DIRECTORY` som platshållare)

> **Proffstips:** Om du ännu inte har en licens kan du begära en temporär nyckel från Asposes webbplats; biblioteket fungerar i utvärderingsläge utan kodändringar.

## Hur du skapar PDF-formulärfält i C# (översikt)

1. Läs in den befintliga PDF‑dokumentet.  
2. Instansiera ett `TextBoxField` och konfigurera dess namn och utseende.  
3. Lägg till en widget‑annotation som definierar den visuella rektangeln på målsidan.  
4. Infoga fältet i dokumentets formulärsamling.  
5. Spara den modifierade PDF‑filen.

Varje steg förklaras i detalj nedan, med fullständiga kodexempel och resonemanget bakom API‑anropen.

## Steg 1: Läs in PDF‑dokumentet

Den första operationen är att läsa in käll‑PDF‑filen. Aspose.PDF representerar en PDF‑fil med klassen `Document`. När du laddar dokumentet får du åtkomst till dess sidor, formulärsamling och andra strukturer.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using Aspose.Pdf.Text;

// Adjust the path to match your environment
string inputPath = Path.Combine("YOUR_DIRECTORY", "input.pdf");

// Load the PDF you want to modify
Document pdfDocument = new Document(inputPath);
```

**Varför detta är viktigt:**  
Att ladda filen skapar en modell av PDF‑filen i minnet, vilket gör att du kan lägga till, ta bort eller redigera objekt utan att förstöra originalfilen. `Document`‑objektet exponerar också egenskapen `Form`, där du senare **lägger till en textruta i PDF**.

## Steg 2: Skapa ett textrutefält

Ett textrutefält är en typ av formulärfält som låter användare skriva fri text. I Aspose.PDF skapar du det genom att instansiera `TextBoxField`, ange målsidan och en rektangel som definierar widgetens initiala storlek.

```csharp
// Choose the page index (0‑based). Here we use page 2 (index 1).
Page targetPage = pdfDocument.Pages[1];

// Define the rectangle for the field’s *initial* size.
// Rectangle(left, bottom, right, top) – values are in points (1/72 inch).
Rectangle fieldRect = new Rectangle(100, 500, 200, 530);

// Create the TextBoxField with a partial name that will be used in form data.
TextBoxField textBox = new TextBoxField(targetPage, fieldRect)
{
    PartialName = "Comments", // This identifier appears in the PDF form data.
    // Optional: set default appearance (font, size, color)
    DefaultAppearance = new DefaultAppearance(FontRepository.FindFont("Helvetica"), 12, Color.Black)
};
```

**Varför detta är viktigt:**  
* `PartialName` är nyckeln som formulärhanteringsverktyg (t.ex. Adobe Acrobat, server‑sidiga parsers) använder för att hämta det angivna värdet.  
* Rektangeln du anger här definierar endast den *initiala* widget‑storleken; du kan senare justera dess visuella placering med en widget‑annotation (nästa steg).  
* Att sätta `DefaultAppearance` säkerställer att texten i rutan renderas konsekvent i olika visare.

## Steg 3: Definiera den visuella widget‑annoteringen

Ett formulärfält kan ha en eller flera **widget‑annotationer** som styr var fältet visas på varje sida. Genom att lägga till en widget kan du placera samma logiska fält på en annan plats eller till och med på flera sidor.

```csharp
// Define where the field will actually be displayed on the page.
// This rectangle can differ from the one used in the constructor.
Rectangle widgetRect = new Rectangle(100, 300, 200, 330);
textBox.AddWidgetAnnotation(widgetRect);
```

**Varför detta är viktigt:**  
Widget‑rektangeln bestämmer de skärmkoordinater som användarna ser. Om du hoppar över detta steg kan fältet finnas i PDF‑filens datastruktur men blir osynligt för slutanvändaren. Att lägga till en widget är steget som verkligen **lägger till en textruta i PDF**.

## Steg 4: Lägg till det konfigurerade fältet i dokumentets formulär

Nu när `TextBoxField` är fullt konfigurerat måste du registrera det i PDF‑filens formulärsamling. Detta gör fältet till en del av det interaktiva formuläret och säkerställer att det sparas.

```csharp
pdfDocument.Form.Add(textBox);
```

**Varför detta är viktigt:**  
Utan att lägga till fältet i `pdfDocument.Form` skulle PDF‑visaren ignorera widget‑annoteringen, och fältdata skulle aldrig skickas. Den här raden slutför **modifiera PDF för att inkludera en textruta**‑operationen.

## Steg 5: Spara den uppdaterade PDF‑filen

Till sist skriver du tillbaka ändringarna till disk. Du kan skriva över originalfilen eller skapa en ny; exemplet sparar till `output.pdf`.

```csharp
string outputPath = Path.Combine("YOUR_DIRECTORY", "output.pdf");

// Save the document with the new form field
pdfDocument.Save(outputPath);
```

När du öppnar `output.pdf` i Adobe Acrobat Reader ser du en rektangulär textruta med etiketten “Comments” på sida 2. Användare kan klicka i rutan, skriva, och den angivna texten blir en del av PDF‑formulärets data.

## Fullständigt fungerande exempel

När alla bitar sätts ihop får du ett komplett, körklart program. Kopiera det till ett nytt konsolprojekt, ersätt `YOUR_DIRECTORY` med en riktig sökväg och kör.

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using Aspose.Pdf.Text;
using System.Drawing; // For Color

namespace PdfFormFieldDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the existing PDF
            string inputPath = Path.Combine("YOUR_DIRECTORY", "input.pdf");
            Document pdfDocument = new Document(inputPath);

            // 2️⃣ Create a TextBoxField on page 2 (index 1)
            Page targetPage = pdfDocument.Pages[1];
            Rectangle fieldRect = new Rectangle(100, 500, 200, 530);
            TextBoxField textBox = new TextBoxField(targetPage, fieldRect)
            {
                PartialName = "Comments",
                DefaultAppearance = new DefaultAppearance(
                    FontRepository.FindFont("Helvetica"), 12, Color.Black)
            };

            // 3️⃣ Add a widget annotation to control visual placement
            Rectangle widgetRect = new Rectangle(100, 300, 200, 330);
            textBox.AddWidgetAnnotation(widgetRect);

            // 4️⃣ Register the field with the document's form collection
            pdfDocument.Form.Add(textBox);

            // 5️⃣ Save the modified PDF
            string outputPath = Path.Combine("YOUR_DIRECTORY", "output.pdf");
            pdfDocument.Save(outputPath);

            Console.WriteLine("PDF form field created successfully.");
            Console.WriteLine($"Output saved to: {outputPath}");
        }
    }
}
```

**Förväntad output:**  
När programmet körs skrivs två bekräftelsesatser till konsolen. När du öppnar `output.pdf` visas en textruta på sida 2 där användaren kan skriva kommentarer. När formuläret skickas (t.ex. via Adobe Acrobats “Submit”-knapp) visas fältnamnet `Comments` i den exporterade FDF‑ eller XFDF‑datan.

## Vanliga variationer och kantfall

| Situation | Hur du anpassar koden |
|-----------|-----------------------|
| **Lägg till fältet på en annan sida** | Ändra `pdfDocument.Pages[1]` till önskat sidindex (0‑baserat). |
| **Skapa en flerradig textruta** | Sätt `textBox.Multiline = true;` innan du lägger till widgeten. |
| **Ange ett standardvärde** | Tilldela `textBox.Value = "Enter your comments here";`. |
| **Gör fältet obligatoriskt** | Sätt `textBox.Required = true;`. |
| **Placera fältet på flera sidor** | Anropa `textBox.AddWidgetAnnotation` för varje extra rektangel på målsidorna. |
| **Använd ett eget typsnitt** | Ladda typsnittet med `FontRepository.AddFont("path/to/font.ttf")` och referera till det i `DefaultAppearance`. |

**Proffstips:** Validera alltid rektangelkoordinaterna mot sidstorleken (`pdfDocument.Pages[1].Rect`). Om widgeten ligger utanför sidans gränser kan visare klippa eller dölja fältet.

## Testa formulärfältet

1. Öppna `output.pdf` i Adobe Acrobat Reader.  
2. Klicka i “Comments”-rutan; markören ska visas.  
3. Skriv någon text och tryck **Tab** eller klicka någon annanstans.  
4. Välj **File → Save As** för att spara det angivna värdet.  
5. (Valfritt) Använd Aspose.PDF:s `Form`‑API för att extrahera värdet programatiskt:

```csharp
string commentValue = pdfDocument.Form["Comments"].Value;
Console.WriteLine($"Submitted comment: {commentValue}");
```

Detta kodexempel visar att fältet inte bara är synligt utan också kan hämtas via kod – viktigt för server‑sidig bearbetning.

## Slutsats

Du vet nu hur du **skapar PDF-formulärfält** i C# från början till slut. Handledningen gick igenom att läsa in en PDF, konfigurera ett `TextBoxField`, lägga till en widget‑annotation, registrera fältet och spara resultatet. Med dessa byggstenar kan du **lägga till en textruta i PDF**‑dokument, **modifiera PDF för att inkludera en textruta**, och utöka metoden till andra fälttyper som kryssrutor, radioknappar eller rullgardinsmenyer.

Nästa steg är att utforska relaterade ämnen som **extrahera formulärdata**, **platta till PDF‑formulär** eller **styla fält med ramar och färger**. Alla dessa koncept bygger på samma kärn‑API som du just har bemästrat, vilket låter dig skapa sofistikerade interaktiva PDF‑filer helt i C#.

Lycka till med kodandet, och experimentera gärna med olika rektanglar, typsnitt och valideringsregler för att passa just ditt program!

## Vad bör du lära dig härnäst?

Följande handledningar täcker nära besläktade ämnen som bygger vidare på teknikerna i den här guiden. Varje resurs innehåller kompletta kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationssätt i dina egna projekt.

- [Create PDF Document with Aspose – Add Page, Text Box, and Form](/pdf/english/net/forms-annotations/create-pdf-document-with-aspose-add-page-text-box-and-form/)
- [How to Create PDF with Aspose – Add Form Field and Pages](/pdf/english/net/programming-with-forms/how-to-create-pdf-with-aspose-add-form-field-and-pages/)
- [How to Add a Text Stamp to PDF Using Aspose.PDF .NET: Comprehensive Guide](/pdf/english/net/watermarks-backgrounds/add-text-stamp-pdf-aspose-pdf-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}