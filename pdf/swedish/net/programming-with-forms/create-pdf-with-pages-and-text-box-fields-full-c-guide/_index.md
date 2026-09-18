---
category: general
date: 2026-03-03
description: Skapa PDF med sidor och lägg till textrutor som PDF‑formulärfält med
  Aspose.PDF i C#. Lär dig hur du lägger till en textruta, skapar PDF‑formulärfält
  och snabbt lägger till flera sidor i en PDF.
draft: false
keywords:
- create pdf with pages
- add text box pdf
- how to add textbox
- create pdf form field
- add multiple pages pdf
language: sv
og_description: Skapa PDF med sidor med Aspose.PDF. Den här guiden visar hur du lägger
  till textrutefält i PDF, skapar PDF‑formulärfält och lägger till flera sidor i PDF
  i C#.
og_title: Skapa PDF med Pages – Komplett C#-handledning
tags:
- pdf
- csharp
- aspose
title: Skapa PDF med sidor och textrutefält – Fullständig C#‑guide
url: /sv/net/programming-with-forms/create-pdf-with-pages-and-text-box-fields-full-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa PDF med sidor och textrutefält – Fullständig C#‑guide

Har du någonsin behövt **create pdf with pages** som också låter användare skriva anteckningar? Kanske bygger du en kontraktsportal, ett feedbackformulär eller ett enkelt frågeformulär. I så fall vill du ha en PDF som inte bara har flera sidor utan också innehåller en återanvändbar textruta. Bra nyheter: med Aspose.PDF för .NET kan du göra allt detta på några få rader.

I den här handledningen går vi igenom **how to add textbox**‑kontroller, registrerar ett **create pdf form field**, och slutligen **add multiple pages pdf** för att skapa ett polerat, interaktivt dokument. Inga onödiga detaljer—bara koden du kan kopiera‑klistra in, plus “varför” bakom varje beslut. I slutet har du en PDF med namnet `TextBoxTwoWidgets.pdf` som innehåller samma textruta på två separata sidor.

## Förutsättningar

- .NET 6.0 eller senare (koden fungerar även med .NET Framework 4.6+)  
- Aspose.PDF för .NET NuGet‑paket (`Install-Package Aspose.PDF`)  
- Grundläggande förståelse för C#‑klasser och objektstädning (vi kommer att använda ett `using`‑block)  

> **Pro tip:** Om du använder Visual Studio, aktivera *nullable reference types* för en renare upplevelse, men det krävs inte för detta exempel.

## Steg 1: Skapa PDF med sidor – Ställ in dokumentet

Det första du måste göra är att skapa ett tomt PDF‑dokument. Tänk på `Document`‑klassen som en ny anteckningsbok; du kommer att lägga till sidor i den senare.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Forms;

using (var pdfDocument = new Document())
{
    // The document is now ready for pages and form fields.
```

*Varför ett `using`‑block?* Det garanterar att alla ohanterade resurser (filhandtag, minnesbuffertar) frigörs så snart vi är klara, vilket förhindrar läckor—särskilt viktigt när du genererar många PDF‑filer i en webbtjänst.

## Steg 2: Lägg till textrutefält i PDF på första sidan

Nu när dokumentet finns, behöver vi minst en sida för att hysa ett formulärfält. Vi kommer att lägga till **två sidor** eftersom vi vill att samma textruta ska visas på båda.

```csharp
    // Add the first page
    var firstPage = pdfDocument.Pages.Add();

    // Add the second page (will host the widget copy)
    var secondPage = pdfDocument.Pages.Add();

    // Create a TextBoxField on the first page
    var notesField = new TextBoxField(
        firstPage,
        new Rectangle(50, 700, 300, 750))   // left, bottom, right, top
    {
        Name = "Notes",
        Value = "Type here..."
    };
```

Rektangelkoordinaterna följer PDF‑koordinatsystemet (ursprung i nedre vänstra hörnet). `Name`‑egenskapen är den interna identifieraren; du kommer att använda den senare när du hämtar värdet efter att användaren fyllt i formuläret.

## Steg 3: Hur man lägger till textrutewidget på en andra sida

En *widget* är den visuella representationen av ett formulärfält. Som standard får ett fält en enda widget på den sida där det skapades. Om du behöver samma textruta på en annan sida, lägger du till en annan widget‑annotation.

```csharp
    // Place a second widget of the same field on the second page
    notesField.AddWidgetAnnotation(
        secondPage,
        new Rectangle(50, 500, 300, 550));
```

Observera de olika Y‑koordinaterna—detta placerar den andra textrutan lägre på sidan. Du kan naturligtvis använda samma rektangel om du vill ha identisk placering.

## Steg 4: Skapa PDF‑formulärfält och registrera det

Även om vi redan har instansierat `notesField` måste vi fortfarande registrera det i dokumentets `Form`‑samling. Detta steg gör fältet till en del av den interaktiva formulärstrukturen.

```csharp
    // Register the field with the PDF form
    pdfDocument.Form.Add(notesField, notesField.Name);
```

Om du hoppar över den här raden kommer textrutan att visas visuellt men sparas inte som ett formulärfält, vilket betyder att dess innehåll inte kommer att skickas när PDF‑filen bearbetas.

## Steg 5: Spara PDF‑filen och verifiera flera sidor PDF

Till sist skriver vi dokumentet till disk. Filnamnet är godtyckligt; se bara till att mappen finns och att din app har skrivbehörighet.

```csharp
    // Save the resulting PDF
    pdfDocument.Save(@"C:\Temp\TextBoxTwoWidgets.pdf");
}
```

När du öppnar `TextBoxTwoWidgets.pdf` i Adobe Acrobat Reader kommer du att se två sidor, var och en innehåller samma “Notes”‑textruta. Skriv något på den första sidan, hoppa till den andra—båda fälten förblir oberoende eftersom de delar samma underliggande dataobjekt.

### Förväntat resultat

- **Sida 1:** Textruta på koordinaterna (50, 700) med platshållare “Type here…”.  
- **Sida 2:** Identisk textruta placerad lägre (50, 500).  
- Båda sidorna tillhör ett **enkelt PDF‑formulär** med namnet “Notes”.  

Du kan testa formuläret genom att exportera data (Acrobat → Tools → Prepare Form → Export Data) och du kommer att se en enda post för `Notes`.

## Vanliga variationer och kantfall

| Scenario | Vad som ska ändras | Varför |
|----------|--------------------|--------|
| **Olika standardtext per sida** | Skapa två separata `TextBoxField`‑objekt med olika `Name`‑värden. | Varje widget måste tillhöra sitt eget fält för att hålla oberoende värden. |
| **Skrivskyddad textruta** | Sätt `notesField.ReadOnly = true;` innan widgeten läggs till. | Förhindrar att användare redigerar fältet samtidigt som informationen visas. |
| **Flerradig textruta** | Sätt `notesField.Multiline = true;` och öka rektangelns höjd. | Tillåter längre anteckningar utan att behöva scrolla. |
| **Lösenordsskyddad PDF** | Efter sparande, anropa `pdfDocument.Encrypt("ownerPwd", "userPwd", EncryptionAlgorithms.AESx128);`. | Säkerställer dokumentet samtidigt som formulärfälten bevaras. |

## Pro‑tips för att arbeta med Aspose.PDF‑formulär

- **Batch creation:** Om du behöver dussintals identiska widgets, loopa över `pdfDocument.Pages` och anropa `AddWidgetAnnotation` inuti loopen.  
- **Field naming conventions:** Använd ett prefix som `txt_` eller `fld_` för att undvika kollisioner när du slår ihop PDF‑filer senare.  
- **Performance:** Återanvänd en enda `Rectangle`‑instans när det är möjligt; biblioteket kopierar värdena internt, så du undviker en minnesflaskhals.  

## Fullt fungerande exempel (Klar att kopiera‑klistra in)

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Forms;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new PDF document
        using (var pdfDocument = new Document())
        {
            // 2️⃣ Add two pages – we’ll place a widget on each
            var firstPage = pdfDocument.Pages.Add();
            var secondPage = pdfDocument.Pages.Add();

            // 3️⃣ Define the textbox field (add text box pdf)
            var notesField = new TextBoxField(
                firstPage,
                new Rectangle(50, 700, 300, 750))
            {
                Name = "Notes",
                Value = "Type here..."
            };

            // 4️⃣ Add a second widget on the second page (how to add textbox)
            notesField.AddWidgetAnnotation(
                secondPage,
                new Rectangle(50, 500, 300, 550));

            // 5️⃣ Register the field (create pdf form field)
            pdfDocument.Form.Add(notesField, notesField.Name);

            // 6️⃣ Save the file (add multiple pages pdf)
            pdfDocument.Save(@"C:\Temp\TextBoxTwoWidgets.pdf");
        }

        System.Console.WriteLine("PDF created successfully!");
    }
}
```

Kör programmet, öppna den resulterande filen, och du kommer att se exakt det som handledningen beskriver.

## Slutsats

Vi har just **created pdf with pages** som innehåller ett återanvändbart **add text box pdf**‑formelement, demonstrerat **how to add textbox**‑widgets på flera sidor, och registrerat ett korrekt **create pdf form field**. Det slutgiltiga dokumentet visar att du kan **add multiple pages pdf** samtidigt som formuläret förblir interaktivt och lättviktigt.

Vad blir nästa steg? Prova att lägga till kryssrutor, radioknappar eller till och med JavaScript‑åtgärder för att göra PDF‑filen riktigt dynamisk. Du kan också utforska att slå ihop flera sådana PDF‑filer till en enda rapport—Aspose.PDF gör det enkelt.

Har du frågor eller ett coolt användningsfall du vill dela? Lämna en kommentar nedan, och lycka till med kodandet!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}