---
category: general
date: 2026-06-21
description: Skapa PDF‑textfält med C# och lär dig hur du duplicerar PDF‑formulärfält
  eller lägger till ett textfält i PDF‑formuläret på bara några rader kod.
draft: false
keywords:
- create pdf textbox field
- duplicate pdf form field
- add textbox to pdf form
- pdf form automation
- c# pdf library
language: sv
og_description: Skapa PDF-textfält snabbt. Den här guiden visar hur du duplicerar
  PDF-formulärfält och lägger till ett textfält i PDF-formuläret med ett modernt C#
  PDF‑bibliotek.
og_title: Skapa PDF-textruta – Komplett C#‑handledning
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Create PDF textbox field with C# and learn how to duplicate PDF form
    field or add textbox to PDF form in just a few lines of code.
  headline: Create PDF Textbox Field – Step‑by‑Step Guide
  type: TechArticle
- description: Create PDF textbox field with C# and learn how to duplicate PDF form
    field or add textbox to PDF form in just a few lines of code.
  name: Create PDF Textbox Field – Step‑by‑Step Guide
  steps:
  - name: What if I need the field on *more* than two pages?
    text: Just repeat the clone‑and‑add steps for each additional page. The underlying
      data object stays the same, so all widgets stay in sync.
  - name: How do I change the appearance (font, border, background)?
    text: Each `Widget` has a `SetBorderColor`, `SetBorderWidth`, and `SetBackgroundColor`
      method. You can also assign a default appearance string (`DA`) to control the
      font and size.
  - name: Can I make the field read‑only after the user fills it?
    text: Yes. Set the `ReadOnly` flag on the field after you’ve collected the data,
      or toggle it based on your workflow.
  - name: What about PDFs that already contain a form?
    text: If the document already has an AcroForm, `doc.GetForm()` simply returns
      it. You can then add new fields without disturbing existing ones. Just be careful
      to use unique field names.
  type: HowTo
tags:
- PDF
- C#
- FormFields
title: Skapa PDF‑textfält – Steg‑för‑steg‑guide
url: /sv/net/programming-with-forms/create-pdf-textbox-field-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa PDF-textfält – Komplett C#-handledning

Har du någonsin behövt **create PDF textbox field** men varit osäker på vilka API-anrop du ska använda? Du är inte ensam. Oavsett om du bygger en kontrakts‑signeringsportal eller ett enkelt datainsamlings‑blad, är det att lägga till interaktiva textfält i en PDF en grundläggande färdighet för alla formulär‑automatiseringsutvecklare.  

I den här guiden går vi igenom ett praktiskt exempel som inte bara **adds textbox to PDF form**, utan också visar hur man **duplicate PDF form field** så att samma inmatning visas på flera sidor. I slutet har du ett körbart program som du kan lägga in i vilket .NET‑projekt som helst.

## Vad du behöver

- .NET 6.0 eller senare (koden fungerar även med .NET Core)  
- Ett modernt C# PDF‑bibliotek – kodsnutten nedan använder **PDFTron SDK**, men koncepten kan överföras till iText 7, PdfSharp eller andra bibliotek.  
- Visual Studio 2022 (eller någon annan IDE du föredrar)  

Det är allt – inga extra tjänster, inga obskyra beroenden. Om du redan har en PDF du vill utöka, peka bara koden mot den.

---

## Steg 1: Ställ in projektet och importera SDK:n

Först, skapa en konsolapp:

```bash
dotnet new console -n PdfFormDemo
cd PdfFormDemo
```

Lägg till PDFTron NuGet‑paketet:

```bash
dotnet add package PDFTron.NET
```

Öppna nu `Program.cs` och importera de namnrymder vi behöver:

```csharp
using System;
using pdftron;
using pdftron.Common;
using pdftron.PDF;
using pdftron.SDF;
```

> **Pro tip:** Om du använder ett annat bibliotek, ersätt `using`‑satserna med motsvarande (t.ex. `iText.Kernel.Pdf` för iText 7).

## Steg 2: Initiera PDF‑dokumentet och formuläret

Vi börjar med en ny PDF som innehåller två sidor – källsidan för det ursprungliga textfältet och en målsida för dupliceringen.

```csharp
PDFNet.Initialize();                     // Initialize the PDFTron runtime

// Create a new PDF document
using (PDFDoc doc = new PDFDoc())
{
    // Add two blank pages (letter size)
    Page sourcePage = doc.PageCreate(new Size(612, 792));
    doc.PagePushBack(sourcePage);
    Page targetPage = doc.PageCreate(new Size(612, 792));
    doc.PagePushBack(targetPage);

    // Get (or create) the AcroForm object
    Form form = doc.GetForm();
```

`Form`‑objektet är där alla interaktiva fält finns. Om dokumentet inte redan hade ett formulär, skapar `GetForm()` ett åt oss.

## Steg 3: **Create PDF Textbox Field** på första sidan

Nu kommer kärnan i vår handledning – att skapa ett textfält. Rektangelkoordinaterna anges i punkter (1 tum = 72 punkter). Exemplet placerar rutan nära toppen‑centrum på första sidan.

```csharp
    // Step 1: Create a text box field on the first page and set its initial value
    TextBoxField textBoxField = new TextBoxField(sourcePage, new Rect(100, 500, 300, 520))
    {
        Value = "Sample"
    };
```

Varför sätter vi `Value` direkt? Att förifylla fältet ger användarna en ledtråd om den förväntade inmatningen, och det visar också att fältet är fullt funktionellt.

## Steg 4: Lägg till fältet i formuläret – **Add Textbox to PDF Form**

Nästa steg är att registrera fältet i formuläret med ett logiskt namn. Detta namn är det du senare refererar till när du behöver läsa eller ändra fältets data programatiskt.

```csharp
    // Step 2: Add the field to the form with a logical name
    form.Add(textBoxField, "multiBox");
```

Att välja ett tydligt namn (t.ex. `"multiBox"`) gör senare kod enklare att förstå, särskilt när du har dussintals fält.

## Steg 5: **Duplicate PDF Form Field** på en annan sida

Ett vanligt krav är att visa samma fält på flera sidor – tänk på en “Customer Name”-ruta som visas på varje fakturasida. PDFTron låter oss klona widget‑annoteringen, som är den visuella representationen av fältet.

```csharp
    // Step 3: Clone the field's widget annotation so it can appear on another page
    Widget clonedWidget = textBoxField.CreateWidgetAnnotation();

    // Step 4: Place the cloned widget on the second page
    targetPage.Annotations.Add(clonedWidget);
```

Den klonade widgeten delar samma underliggande data som det ursprungliga textfältet. När en användare skriver i en instans uppdateras den andra automatiskt – det är magin med **duplicate PDF form field**.

## Steg 6: Spara dokumentet och rensa upp

Till sist, skriv PDF‑filen till disk och stäng ner PDFNet‑runtime.

```csharp
    // Save the resulting PDF
    doc.Save("output.pdf", SDFDoc.SaveOptions.e_linearized);
    Console.WriteLine("PDF created: output.pdf");
}

// Shut down PDFNet (optional but good practice)
PDFNet.Terminate();
```

När programmet körs skapas en två‑sidig PDF (`output.pdf`). Öppna den i Adobe Acrobat Reader, klicka på textfältet på sida 1, skriv något, och byt sedan till sida 2 – samma text visas omedelbart. Det är ett fullt funktionellt **create pdf textbox field**‑exempel med ett duplicerat fält.

---

## Fullt fungerande exempel (Klar att kopiera‑klistra in)

```csharp
// Program.cs
using System;
using pdftron;
using pdftron.Common;
using pdftron.PDF;
using pdftron.SDF;

class Program
{
    static void Main()
    {
        PDFNet.Initialize();

        using (PDFDoc doc = new PDFDoc())
        {
            // Create two pages
            Page sourcePage = doc.PageCreate(new Size(612, 792));
            doc.PagePushBack(sourcePage);
            Page targetPage = doc.PageCreate(new Size(612, 792));
            doc.PagePushBack(targetPage);

            // Get the form (creates one if missing)
            Form form = doc.GetForm();

            // Step 1: Create a text box field on the first page
            TextBoxField textBoxField = new TextBoxField(sourcePage,
                new Rect(100, 500, 300, 520))
            {
                Value = "Sample"
            };

            // Step 2: Add the field to the form
            form.Add(textBoxField, "multiBox");

            // Step 3: Clone the widget so it appears on page 2
            Widget clonedWidget = textBoxField.CreateWidgetAnnotation();

            // Step 4: Attach the cloned widget to the second page
            targetPage.Annotations.Add(clonedWidget);

            // Save the file
            doc.Save("output.pdf", SDFDoc.SaveOptions.e_linearized);
            Console.WriteLine("PDF created: output.pdf");
        }

        PDFNet.Terminate();
    }
}
```

**Förväntad output:** En fil med namnet `output.pdf` som innehåller två sidor. Båda sidorna visar samma redigerbara textfält med etiketten “Sample”. Att redigera en uppdaterar den andra omedelbart.

---

## Vanliga frågor & kantfall

### Vad händer om jag behöver fältet på *mer* än två sidor?

Upprepa bara klona‑och‑lägg‑till‑stegen för varje extra sida. Det underliggande dataobjektet förblir detsamma, så alla widgetar hålls synkroniserade.

```csharp
Widget anotherClone = textBoxField.CreateWidgetAnnotation();
thirdPage.Annotations.Add(anotherClone);
```

### Hur ändrar jag utseendet (font, ram, bakgrund)?

Varje `Widget` har metoderna `SetBorderColor`, `SetBorderWidth` och `SetBackgroundColor`. Du kan också tilldela en standardutseende‑sträng (`DA`) för att styra font och storlek.

```csharp
textBoxField.SetBorderColor(new ColorPt(0, 0, 1), 3); // blue border
textBoxField.SetBackgroundColor(new ColorPt(0.9, 0.9, 0.9), 3); // light gray fill
textBoxField.SetDefaultAppearance("Helvetica 12 Tf 0 g");
```

### Kan jag göra fältet skrivskyddat efter att användaren har fyllt i det?

Ja. Sätt `ReadOnly`‑flaggan på fältet efter att du har samlat in data, eller växla den baserat på ditt arbetsflöde.

```csharp
textBoxField.SetFlag(Field.Flag.e_readonly, true);
```

### Vad händer med PDF‑filer som redan innehåller ett formulär?

Om dokumentet redan har ett AcroForm, returnerar `doc.GetForm()` helt enkelt det. Du kan då lägga till nya fält utan att störa befintliga. Var bara noga med att använda unika fältnamn.

---

## Tips för verkliga projekt

- **Naming convention:** Prefixa fältnamn med sidan eller sektionen (t.ex. `invoice_customer_name`) för att undvika kollisioner.  
- **Validation:** Använd JavaScript‑åtgärder (`field.SetAction(Field.Action.e_keystroke, "event.rc = /^[A-Za-z]+$/.test(event.change);")`) om du behöver klient‑sidovalidering.  
- **Performance:** När du arbetar med stora PDF‑filer, anropa `doc.Lock()` före massoperationer för att minska I/O‑belastning.  
- **Accessibility:** Sätt egenskapen `AlternateName` så skärmläsare kan beskriva fältet.

## Slutsats

Vi har just **created a PDF textbox field**, visat hur man **duplicate PDF form field** över sidor, och demonstrerat det enklaste sättet att **add textbox to PDF form** med C#. Den fullständiga, körbara koden finns ovan, och du kan utöka den med styling, validering eller extra sidor efter behov.

Redo för nästa steg? Prova att bädda in en dropdown (`ChoiceField`) eller en signaturwidget, eller utforska hur du kan platta till formuläret efter datainmatning för arkiveringsändamål. PDFTron SDK (eller något liknande bibliotek) ger dig byggstenarna – din fantasi bestämmer den slutgiltiga formen.

Om du stöter på problem, lämna en kommentar nedan eller kolla bibliotekets officiella dokumentation; de är fulla av exempel som kompletterar det vi gått igenom här. Lycka till med kodandet, och må dina formulär alltid hålla sig i synk!

## Vad du bör lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [How to Create PDF with Aspose – Add Form Field and Pages](/pdf/english/net/programming-with-forms/how-to-create-pdf-with-aspose-add-form-field-and-pages/)
- [Add Form Field in PDF Document using Java](/pdf/english/java/pdf-form-fields/add-form-field-in-pdf-document-using-java/)
- [Add Form Field In Pdf Document Using Java](/pdf/german/java/pdf-form-fields/add-form-field-in-pdf-document-using-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}