---
category: general
date: 2026-06-21
description: Maak een PDF-tekstvak met C# en leer hoe je een PDF-formulierveld dupliceert
  of een tekstvak toevoegt aan een PDF-formulier in slechts een paar regels code.
draft: false
keywords:
- create pdf textbox field
- duplicate pdf form field
- add textbox to pdf form
- pdf form automation
- c# pdf library
language: nl
og_description: Maak snel een PDF-tekstvakveld aan. Deze gids laat zien hoe je een
  PDF-formulierveld dupliceert en een tekstvak toevoegt aan een PDF-formulier met
  behulp van een moderne C# PDF‑bibliotheek.
og_title: Maak PDF-tekstvakveld – Complete C#-handleiding
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
title: PDF-tekstvakveld maken – Stapsgewijze handleiding
url: /nl/net/programming-with-forms/create-pdf-textbox-field-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PDF‑tekstvakveld maken – Complete C#‑tutorial

Heb je ooit een **PDF‑tekstvakveld moeten maken** maar wist je niet welke API‑aanroepen je moet gebruiken? Je bent niet de enige. Of je nu een contract‑ondertekeningsportaal bouwt of een eenvoudig gegevens‑verzamelingsblad, het toevoegen van interactieve tekstvakken aan een PDF is een kernvaardigheid voor elke formulier‑automatiseringsontwikkelaar.  

In deze gids lopen we een praktisch voorbeeld door dat niet alleen **tekstvak aan PDF‑formulier toevoegt**, maar ook laat zien hoe je een **PDF‑formulier‑veld dupliceert** zodat dezelfde invoer op meerdere pagina's verschijnt. Aan het einde heb je een uitvoerbaar programma dat je in elk .NET‑project kunt plaatsen.

## Wat je nodig hebt

- .NET 6.0 of later (de code werkt ook met .NET Core)  
- Een moderne C# PDF‑bibliotheek – de snippet hieronder gebruikt **PDFTron SDK**, maar de concepten zijn toepasbaar op iText 7, PdfSharp of andere bibliotheken.  
- Visual Studio 2022 (of een IDE naar keuze)  

Dat is alles – geen extra services, geen obscure afhankelijkheden. Als je al een PDF hebt die je wilt uitbreiden, verwijs de code er dan gewoon naar.

---

## Stap 1: Het project instellen en de SDK importeren

First, create a console app:

```bash
dotnet new console -n PdfFormDemo
cd PdfFormDemo
```

Add the PDFTron NuGet package:

```bash
dotnet add package PDFTron.NET
```

Now open `Program.cs` and pull in the namespaces we’ll need:

```csharp
using System;
using pdftron;
using pdftron.Common;
using pdftron.PDF;
using pdftron.SDF;
```

> **Pro tip:** Als je een andere bibliotheek gebruikt, vervang dan de `using`‑statements door de equivalente (bijv. `iText.Kernel.Pdf` voor iText 7).

## Stap 2: Initialiseer het PDF‑document en het formulier

We’ll start with a fresh PDF that contains two pages – the source page for the original textbox and a target page for the duplicate.

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

Het `Form`‑object is waar alle interactieve velden wonen. Als het document nog geen formulier had, maakt `GetForm()` er één voor ons.

## Stap 3: **PDF‑tekstvakveld maken** op de eerste pagina

Now comes the core of our tutorial – creating a textbox field. The rectangle coordinates are expressed in points (1 inch = 72 points). The example places the box near the top‑center of the first page.

```csharp
    // Step 1: Create a text box field on the first page and set its initial value
    TextBoxField textBoxField = new TextBoxField(sourcePage, new Rect(100, 500, 300, 520))
    {
        Value = "Sample"
    };
```

Waarom stellen we `Value` meteen in? Het vooraf invullen van het veld geeft gebruikers een hint over de verwachte invoer, en het toont ook dat het veld volledig functioneel is.

## Stap 4: Voeg het veld toe aan het formulier – **Tekstvak toevoegen aan PDF‑formulier**

Next, we register the field with the form using a logical name. This name is what you’ll reference later when you need to read or modify the field’s data programmatically.

```csharp
    // Step 2: Add the field to the form with a logical name
    form.Add(textBoxField, "multiBox");
```

Een duidelijke naam kiezen (bijv. `"multiBox"`) maakt latere code makkelijker te begrijpen, vooral als je tientallen velden hebt.

## Stap 5: **PDF‑formulier‑veld dupliceren** op een andere pagina

A common requirement is to show the same field on multiple pages – think of a “Customer Name” box that appears on every invoice page. PDFTron lets us clone the widget annotation, which is the visual representation of the field.

```csharp
    // Step 3: Clone the field's widget annotation so it can appear on another page
    Widget clonedWidget = textBoxField.CreateWidgetAnnotation();

    // Step 4: Place the cloned widget on the second page
    targetPage.Annotations.Add(clonedWidget);
```

De gekloonde widget deelt dezelfde onderliggende data als het originele tekstvak. Wanneer een gebruiker in één instantie typt, wordt de andere automatisch bijgewerkt – dat is de magie van **duplicate PDF form field**.

## Stap 6: Sla het document op en maak opruimen

Finally, write the PDF to disk and shut down the PDFNet runtime.

```csharp
    // Save the resulting PDF
    doc.Save("output.pdf", SDFDoc.SaveOptions.e_linearized);
    Console.WriteLine("PDF created: output.pdf");
}

// Shut down PDFNet (optional but good practice)
PDFNet.Terminate();
```

Het uitvoeren van het programma levert een twee‑pagina PDF (`output.pdf`). Open deze in Adobe Acrobat Reader, klik op het tekstvak op pagina 1, typ iets, en ga vervolgens naar pagina 2 – dezelfde tekst verschijnt direct. Dat is een volledig functioneel **create pdf textbox field**‑voorbeeld met een gedupliceerd veld.

---

## Volledig werkend voorbeeld (Klaar om te kopiëren‑plakken)

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

**Verwachte output:** Een bestand genaamd `output.pdf` met twee pagina's. Beide pagina's tonen hetzelfde bewerkbare tekstvak met het label “Sample”. Het bewerken van één veld werkt het andere onmiddellijk bij.

---

## Veelgestelde vragen & randgevallen

### Wat als ik het veld op *meer* dan twee pagina's nodig heb?

Just repeat the clone‑and‑add steps for each additional page. The underlying data object stays the same, so all widgets stay in sync.

```csharp
Widget anotherClone = textBoxField.CreateWidgetAnnotation();
thirdPage.Annotations.Add(anotherClone);
```

### Hoe wijzig ik het uiterlijk (lettertype, rand, achtergrond)?

Each `Widget` has a `SetBorderColor`, `SetBorderWidth`, and `SetBackgroundColor` method. You can also assign a default appearance string (`DA`) to control the font and size.

```csharp
textBoxField.SetBorderColor(new ColorPt(0, 0, 1), 3); // blue border
textBoxField.SetBackgroundColor(new ColorPt(0.9, 0.9, 0.9), 3); // light gray fill
textBoxField.SetDefaultAppearance("Helvetica 12 Tf 0 g");
```

### Kan ik het veld alleen‑lezen maken nadat de gebruiker het heeft ingevuld?

Yes. Set the `ReadOnly` flag on the field after you’ve collected the data, or toggle it based on your workflow.

```csharp
textBoxField.SetFlag(Field.Flag.e_readonly, true);
```

### Hoe zit het met PDF's die al een formulier bevatten?

If the document already has an AcroForm, `doc.GetForm()` simply returns it. You can then add new fields without disturbing existing ones. Just be careful to use unique field names.

## Tips voor projecten in de echte wereld

- **Naming convention:** Prefix field names with the page or section (e.g., `invoice_customer_name`) to avoid collisions.  
- **Validation:** Use JavaScript actions (`field.SetAction(Field.Action.e_keystroke, "event.rc = /^[A-Za-z]+$/.test(event.change);")`) if you need client‑side validation.  
- **Performance:** When working with large PDFs, call `doc.Lock()` before bulk operations to reduce I/O overhead.  
- **Accessibility:** Set the `AlternateName` property so screen readers can describe the field.

## Conclusie

We hebben zojuist **een PDF‑tekstvakveld gemaakt**, laten zien hoe je een **PDF‑formulier‑veld dupliceert** over pagina's, en de eenvoudigste manier gedemonstreerd om **tekstvak toe te voegen aan PDF‑formulier** met C#. De volledige, uitvoerbare code staat hierboven, en je kunt deze uitbreiden met styling, validatie of extra pagina's naar behoefte.

Klaar voor de volgende stap? Probeer een dropdown (`ChoiceField`) of een handtekeningwidget in te voegen, of onderzoek hoe je het formulier kunt flattenen na gegevensinvoer voor archiveringsdoeleinden. De PDFTron SDK (of een vergelijkbare bibliotheek) geeft je de bouwblokken—jouw verbeelding bepaalt de uiteindelijke vorm.

Als je tegen een probleem aanloopt, laat dan een reactie achter of raadpleeg de officiële documentatie van de bibliotheek; die zit vol met voorbeelden die aansluiten bij wat we hier hebben behandeld. Veel programmeerplezier, en moge je formulieren altijd gesynchroniseerd blijven!

## Wat je hierna moet leren

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [How to Create PDF with Aspose – Add Form Field and Pages](/pdf/english/net/programming-with-forms/how-to-create-pdf-with-aspose-add-form-field-and-pages/)
- [Add Form Field in PDF Document using Java](/pdf/english/java/pdf-form-fields/add-form-field-in-pdf-document-using-java/)
- [Add Form Field In Pdf Document Using Java](/pdf/german/java/pdf-form-fields/add-form-field-in-pdf-document-using-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}