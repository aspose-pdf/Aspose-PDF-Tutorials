---
category: general
date: 2026-06-08
description: Skapa ett flersidigt formulär i C# med Aspose.Pdf. Lär dig hur du lägger
  till en textruta i PDF, skapar PDF‑formulärfält och sparar den uppdaterade PDF‑filen
  med tydliga kodexempel.
draft: false
keywords:
- create multi page form
- add textbox to pdf
- create pdf form field
- how to save pdf
- save updated pdf
language: sv
og_description: Skapa flersidigt formulär i C# med Aspose.Pdf. Den här guiden visar
  hur du lägger till en textruta i PDF, skapar PDF-formulärfält och sparar den uppdaterade
  PDF-filen på några minuter.
og_title: Skapa flersidig formulär i C# – Komplett Aspose.Pdf-handledning
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Create multi page form in C# using Aspose.Pdf. Learn how to add textbox
    to pdf, create pdf form field, and save updated pdf with clear code examples.
  headline: Create Multi Page Form in C# with Aspose.Pdf – Step‑by‑Step Guide
  type: TechArticle
- description: Create multi page form in C# using Aspose.Pdf. Learn how to add textbox
    to pdf, create pdf form field, and save updated pdf with clear code examples.
  name: Create Multi Page Form in C# with Aspose.Pdf – Step‑by‑Step Guide
  steps:
  - name: '**Load** the existing PDF.'
    text: '**Load** the existing PDF.'
  - name: '**Create** a `TextBoxField` on the first page – this is our form field.'
    text: '**Create** a `TextBoxField` on the first page – this is our form field.'
  - name: '**Add** a widget annotation on the second page so the same field appears
      there too.'
    text: '**Add** a widget annotation on the second page so the same field appears
      there too.'
  - name: '**Save** the modified document as a new file.'
    text: '**Save** the modified document as a new file.'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF Forms
title: Skapa flersidigt formulär i C# med Aspose.Pdf – Steg‑för‑steg‑guide
url: /sv/net/programming-with-forms/create-multi-page-form-in-c-with-aspose-pdf-step-by-step-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa flersidig formulär i C# med Aspose.Pdf – Komplett guide

Har du någonsin funderat på hur man **skapar flersidigt formulär** i C# utan att kämpa med låg‑nivå PDF-specifikationer? Du är inte ensam. Oavsett om du bygger en jobbansökningsportal eller en skatteåterlämningsguide, kan ett flersidigt PDF‑formulär göra datainsamling smidig och professionell.

I den här handledningen går vi igenom ett verkligt exempel som **lägger till textruta i pdf**, **skapar pdf‑formulärfält**, och slutligen **sparar den uppdaterade pdf‑filen**. I slutet har du ett fullt fungerande tvåsidigt formulär som du kan använda i vilket .NET‑projekt som helst.

> **Proffstips:** Aspose.Pdf fungerar på .NET 6+, .NET Framework 4.6+ och även .NET Core, så du är täckt oavsett om du använder Windows eller Linux.

## Vad du behöver

- **Aspose.Pdf for .NET** (NuGet‑paket `Aspose.Pdf`).  
- En enkel PDF‑fil (`input.pdf`) som redan har minst två sidor.  
- Visual Studio 2022 eller någon editor som stödjer C#.  
- En mapp som du kan läsa/skriva till – vi refererar till den som `YOUR_DIRECTORY`.

Inga andra beroenden. Klar? Låt oss dyka ner.

![Exempel på flersidigt formulär i C# med Aspose.Pdf](image.png "Exempel på flersidigt formulär")

## Skapa flersidigt formulär – Översikt

Innan vi börjar skriva kod, låt oss skissera den övergripande flödet:

1. **Läs in** den befintliga PDF‑filen.  
2. **Skapa** ett `TextBoxField` på den första sidan – detta är vårt formulärfält.  
3. **Lägg till** en widget‑annotation på den andra sidan så att samma fält visas där också.  
4. **Spara** det modifierade dokumentet som en ny fil.

Varje steg är avsiktligt isolerat så att du kan byta ut delar (t.ex. ändra rektangelns storlek eller lägga till fler sidor) utan att förstöra hela processen.

## Steg 1 – Läs in PDF‑dokumentet

Det första du gör när du arbetar med ett PDF‑bibliotek är att öppna källfilen. Aspose.Pdf gör detta till en enradare.

```csharp
// Step 1: Load the PDF document from disk
Aspose.Pdf.Document pdfDocument = new Aspose.Pdf.Document(@"YOUR_DIRECTORY\input.pdf");
```

*Varför detta är viktigt:* Att läsa in dokumentet ger dig åtkomst till `Pages`‑samlingen, där vi senare kommer att fästa vårt formulärfält och widget. Om filen inte hittas kastas ett undantag, så se till att sökvägen är korrekt.

## Steg 2 – Skapa ett TextBox‑formulärfält (lägg till textruta i pdf)

Nu **skapar vi pdf‑formulärfält** – ett `TextBoxField`. Tänk på det som en databehållare som kommer att hålla vad användaren skriver.

```csharp
// Step 2: Instantiate a TextBoxField on page 1
Aspose.Pdf.Forms.TextBoxField commentsField = new Aspose.Pdf.Forms.TextBoxField(
    pdfDocument.Pages[1],                                   // target page (1‑based index)
    new Aspose.Pdf.Rectangle(100, 100, 300, 120));         // position & size (LLX, LLY, URX, URY)
```

- Rektangelkoordinaterna uttrycks i punkter (1 pt = 1/72 tum). Justera dem för att passa din layout.  
- `pdfDocument.Pages[1]` refererar till den **första** sidan eftersom Aspose använder en 1‑baserad samling.  
- Genom att skapa fältet på sida 1 ger vi det också ett standardutseende, som vi återanvänder på sida 2.

## Steg 3 – Ange fältets namn och startvärde

Varje formulärfält behöver en identifierare. Detta är den sträng du senare kommer att referera till när du extraherar användarinmatning.

```csharp
// Step 3: Assign a name and an empty default value
commentsField.Name = "Comments";   // unique field name
commentsField.Value = "";          // start with a blank textbox
```

*Varför namnge det “Comments”?* Det är beskrivande, men du kan kalla det vad du vill (`"Address"`, `"PhoneNumber"`). Se bara till att det är unikt i hela PDF‑filen; duplicerade namn orsakar datakonflikter när formuläret skickas.

## Steg 4 – Lägg till en widget‑annotation på den andra sidan

En *widget* är den visuella representationen av ett formulärfält på en specifik sida. Som standard finns fältet vi skapade bara på sida 1. För att få samma textruta att visas på sida 2 lägger vi till en widget‑annotation.

```csharp
// Step 4: Place the same TextBoxField on page 2 via a widget
commentsField.Widgets.Add(
    new Aspose.Pdf.Forms.WidgetAnnotation(
        pdfDocument.Pages[2],                               // second page
        new Aspose.Pdf.Rectangle(50, 50, 250, 70)));       // widget rectangle
```

Varför en widget? Eftersom PDF‑formulär separerar **fältdefinition** (datat) från **widget‑utseende** (vad användaren ser). Att lägga till en widget låter användaren fylla i samma fält på flera sidor – ett klassiskt krav för flersidiga formulär.

### Tips för kantfall

Om din käll‑PDF har mer än två sidor och du vill ha textrutan på varje sida, loopa över `pdfDocument.Pages` och lägg till en widget för varje. Kom bara ihåg att hålla rektangelns storlek lämplig för varje sidas layout.

## Steg 5 – Spara den uppdaterade PDF‑filen (hur man sparar pdf)

Till sist sparar vi våra ändringar. Aspose.Pdf erbjuder en enkel `Save`‑metod som skriver över eller skapar en ny fil.

```csharp
// Step 5: Save the updated PDF to a new file
pdfDocument.Save(@"YOUR_DIRECTORY\output.pdf");
```

*Varför inte skriva över `input.pdf`?* Att behålla originalet intakt gör felsökning enklare och låter dig jämföra resultat före/efter. Om du verkligen behöver ersätta källan, anropa bara `Save` med samma sökväg.

## Fullt fungerande exempel

När allt sätts ihop, här är det kompletta, körklara programmet.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Forms;

class Program
{
    static void Main()
    {
        // Load the existing PDF (make sure the file exists)
        Document pdfDocument = new Document(@"YOUR_DIRECTORY\input.pdf");

        // Create a TextBoxField on the first page
        TextBoxField commentsField = new TextBoxField(
            pdfDocument.Pages[1],
            new Rectangle(100, 100, 300, 120));

        // Configure the field
        commentsField.Name = "Comments";
        commentsField.Value = ""; // blank by default

        // Add a widget on the second page so the same field appears there
        commentsField.Widgets.Add(
            new WidgetAnnotation(
                pdfDocument.Pages[2],
                new Rectangle(50, 50, 250, 70)));

        // Save the modified PDF
        pdfDocument.Save(@"YOUR_DIRECTORY\output.pdf");

        // Optional: inform the user
        System.Console.WriteLine("Multi‑page form created successfully!");
    }
}
```

### Förväntat resultat

När du öppnar `output.pdf` i Adobe Acrobat Reader:

- Sida 1 visar en tom textruta vid koordinaterna (100, 100)‑(300, 120).  
- Sida 2 visar samma textruta vid (50, 50)‑(250, 70).  
- Båda rutorna delar **fältnamnet** `Comments`, vilket betyder att data som skrivs in på någon av sidorna synkroniseras automatiskt.

## Vanliga frågor & fallgropar

| Fråga | Svar |
|----------|--------|
| *Kan jag lägga till mer än en textruta?* | Absolut. Upprepa bara steg 2‑4 med en ny `TextBoxField`‑instans och ett unikt `Name`. |
| *Vad händer om PDF‑filen inte har en andra sida?* | Koden kommer att kasta ett `ArgumentOutOfRangeException`. Skydda den med `if (pdfDocument.Pages.Count >= 2) { … }`. |
| *Behöver jag ange teckensnitt?* | Aspose använder standard Helvetica. För anpassade teckensnitt, sätt `commentsField.DefaultAppearance.Font` innan du sparar. |
| *Är fältet utskrivbart?* | Ja – Aspose markerar widgets som utskrivbara som standard. Du kan växla `WidgetAnnotation.Flags` om det behövs. |
| *Hur extraherar man det inmatade värdet senare?* | Efter att användare har fyllt i formuläret och du mottagit PDF‑filen, anropa `pdfDocument.Form["Comments"].Value` för att läsa datan. |

## Nästa steg

Nu när du vet **hur man sparar pdf** efter att ha lagt till en textruta, kanske du vill utforska:

- Lägga till **kryssrutor** eller **radioknappar** (`CheckBoxField`, `RadioButtonField`).  
- Använda **JavaScript**‑åtgärder för klient‑sidans validering (`commentsField.Actions.OnMouseUp = "…"`).  
- **Platta till** formuläret för att förhindra ytterligare redigering (`pdfDocument.Form.Flatten()`).

Alla dessa bygger på samma koncept som vi täckte när vi **skapade flersidigt formulär**.

---

**Slutsats:** Du har precis lärt dig hur man **skapar flersidigt formulär** i C# med Aspose.Pdf, hur man **lägger till textruta i pdf**, hur man **skapar pdf‑formulärfält**, och de exakta stegen för att **spara den uppdaterade pdf‑filen**. Känn dig fri att justera rektanglarna, lägga till fler fält, eller loopa över alla sidor för en riktigt dynamisk lösning.

Har du ett eget knep du vill dela? Lägg en kommentar nedan, och lycka till med kodandet!

## Vad bör du lära dig härnäst?

Följande handledningar täcker närliggande ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Hur man skapar PDF med Aspose – Lägg till formulärfält och sidor](/pdf/english/net/programming-with-forms/how-to-create-pdf-with-aspose-add-form-field-and-pages/)
- [Skapa PDF‑dokument med Aspose – Lägg till sida, textruta och formulär](/pdf/english/net/forms-annotations/create-pdf-document-with-aspose-add-page-text-box-and-form/)
- [Hur man lägger till och extraherar PDF‑formulärfält med Aspose.PDF för .NET: En omfattande guide](/pdf/english/net/forms-annotations/manage-pdf-form-fields-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}