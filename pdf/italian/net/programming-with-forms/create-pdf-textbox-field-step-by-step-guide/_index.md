---
category: general
date: 2026-06-21
description: Crea un campo di testo PDF con C# e scopri come duplicare un campo modulo
  PDF o aggiungere un campo di testo a un modulo PDF in poche righe di codice.
draft: false
keywords:
- create pdf textbox field
- duplicate pdf form field
- add textbox to pdf form
- pdf form automation
- c# pdf library
language: it
og_description: Crea rapidamente un campo di testo PDF. Questa guida mostra come duplicare
  un campo modulo PDF e aggiungere un campo di testo al modulo PDF utilizzando una
  moderna libreria PDF C#.
og_title: Crea campo di testo PDF – Tutorial completo C#
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
title: Crea campo di testo PDF – Guida passo passo
url: /it/net/programming-with-forms/create-pdf-textbox-field-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crea campo di testo PDF – Tutorial completo C#

Hai mai avuto bisogno di **creare un campo di testo PDF** ma non sapevi quali chiamate API utilizzare? Non sei solo. Che tu stia costruendo un portale per la firma di contratti o un semplice foglio di acquisizione dati, aggiungere caselle di testo interattive a un PDF è una competenza fondamentale per qualsiasi sviluppatore di automazione dei moduli.  

In questa guida percorreremo un esempio pratico che non solo **aggiunge una casella di testo a un modulo PDF**, ma mostra anche come **duplicare un campo di modulo PDF** in modo che lo stesso input appaia su più pagine. Alla fine avrai un programma eseguibile da inserire in qualsiasi progetto .NET.

## Di cosa avrai bisogno

- .NET 6.0 o successivo (il codice funziona anche con .NET Core)  
- Una libreria PDF moderna per C# – lo snippet qui sotto utilizza **PDFTron SDK**, ma i concetti si applicano anche a iText 7, PdfSharp o altre librerie.  
- Visual Studio 2022 (o qualsiasi IDE tu preferisca)  

Questo è tutto – nessun servizio aggiuntivo, nessuna dipendenza oscura. Se hai già un PDF da arricchire, punta semplicemente il codice a quel file.

---

## Step 1: Configura il progetto e importa l'SDK

Per prima cosa, crea un'app console:

```bash
dotnet new console -n PdfFormDemo
cd PdfFormDemo
```

Aggiungi il pacchetto NuGet di PDFTron:

```bash
dotnet add package PDFTron.NET
```

Ora apri `Program.cs` e importa gli spazi dei nomi di cui avremo bisogno:

```csharp
using System;
using pdftron;
using pdftron.Common;
using pdftron.PDF;
using pdftron.SDF;
```

> **Pro tip:** Se utilizzi una libreria diversa, sostituisci le istruzioni `using` con le equivalenti (ad es., `iText.Kernel.Pdf` per iText 7).

## Step 2: Inizializza il documento PDF e il modulo

Inizieremo con un PDF nuovo che contiene due pagine – la pagina di origine per la casella di testo originale e una pagina di destinazione per il duplicato.

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

L'oggetto `Form` è dove vivono tutti i campi interattivi. Se il documento non ha già un modulo, `GetForm()` ne crea uno per noi.

## Step 3: **Create PDF Textbox Field** sulla prima pagina

Ora arriva il cuore del tutorial – creare un campo di testo. Le coordinate del rettangolo sono espresse in punti (1 pollice = 72 punti). L'esempio posiziona la casella vicino al centro‑alto della prima pagina.

```csharp
    // Step 1: Create a text box field on the first page and set its initial value
    TextBoxField textBoxField = new TextBoxField(sourcePage, new Rect(100, 500, 300, 520))
    {
        Value = "Sample"
    };
```

Perché impostiamo `Value` subito? Pre‑popolare il campo fornisce agli utenti un indizio sull'input atteso e dimostra anche che il campo è pienamente funzionante.

## Step 4: Aggiungi il campo al modulo – **Add Textbox to PDF Form**

Successivamente, registriamo il campo nel modulo usando un nome logico. Questo nome è quello che utilizzerai in seguito per leggere o modificare i dati del campo programmaticamente.

```csharp
    // Step 2: Add the field to the form with a logical name
    form.Add(textBoxField, "multiBox");
```

Scegliere un nome chiaro (come `"multiBox"`) rende il codice successivo più comprensibile, soprattutto quando hai decine di campi.

## Step 5: **Duplicate PDF Form Field** su un'altra pagina

Una necessità comune è mostrare lo stesso campo su più pagine – pensa a una casella “Nome Cliente” che appare su ogni pagina di una fattura. PDFTron consente di clonare l'annotazione widget, che è la rappresentazione visiva del campo.

```csharp
    // Step 3: Clone the field's widget annotation so it can appear on another page
    Widget clonedWidget = textBoxField.CreateWidgetAnnotation();

    // Step 4: Place the cloned widget on the second page
    targetPage.Annotations.Add(clonedWidget);
```

Il widget clonato condivide gli stessi dati sottostanti della casella di testo originale. Quando un utente digita in un'istanza, l'altra si aggiorna automaticamente – è la magia del **duplicate PDF form field**.

## Step 6: Salva il documento e pulisci

Infine, scrivi il PDF su disco e chiudi il runtime di PDFNet.

```csharp
    // Save the resulting PDF
    doc.Save("output.pdf", SDFDoc.SaveOptions.e_linearized);
    Console.WriteLine("PDF created: output.pdf");
}

// Shut down PDFNet (optional but good practice)
PDFNet.Terminate();
```

Eseguendo il programma otterrai un PDF a due pagine (`output.pdf`). Aprilo in Adobe Acrobat Reader, clicca sulla casella di testo nella pagina 1, digita qualcosa, poi passa alla pagina 2 – lo stesso testo appare immediatamente. Questo è un esempio completo di **create pdf textbox field** con un campo duplicato.

---

## Esempio completo funzionante (pronto per il copia‑incolla)

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

**Output previsto:** Un file chiamato `output.pdf` contenente due pagine. Entrambe le pagine mostrano la stessa casella di testo modificabile etichettata “Sample”. Modificando una, l'altra si aggiorna istantaneamente.

---

## Domande frequenti e casi particolari

### E se avessi bisogno del campo su *più* di due pagine?

Basta ripetere i passaggi di clonazione‑e‑aggiunta per ogni pagina aggiuntiva. L'oggetto dati sottostante rimane lo stesso, quindi tutti i widget rimangono sincronizzati.

```csharp
Widget anotherClone = textBoxField.CreateWidgetAnnotation();
thirdPage.Annotations.Add(anotherClone);
```

### Come modifico l'aspetto (font, bordo, sfondo)?

Ogni `Widget` dispone dei metodi `SetBorderColor`, `SetBorderWidth` e `SetBackgroundColor`. Puoi anche assegnare una stringa di aspetto predefinito (`DA`) per controllare font e dimensione.

```csharp
textBoxField.SetBorderColor(new ColorPt(0, 0, 1), 3); // blue border
textBoxField.SetBackgroundColor(new ColorPt(0.9, 0.9, 0.9), 3); // light gray fill
textBoxField.SetDefaultAppearance("Helvetica 12 Tf 0 g");
```

### Posso rendere il campo di sola lettura dopo che l'utente lo ha compilato?

Sì. Imposta il flag `ReadOnly` sul campo dopo aver raccolto i dati, o attivalo in base al tuo flusso di lavoro.

```csharp
textBoxField.SetFlag(Field.Flag.e_readonly, true);
```

### E i PDF che contengono già un modulo?

Se il documento ha già un AcroForm, `doc.GetForm()` lo restituisce semplicemente. Puoi quindi aggiungere nuovi campi senza disturbare quelli esistenti. Fai solo attenzione a usare nomi di campo univoci.

---

## Consigli per progetti reali

- **Convenzione di denominazione:** Prefissa i nomi dei campi con la pagina o la sezione (ad es., `invoice_customer_name`) per evitare collisioni.  
- **Validazione:** Usa azioni JavaScript (`field.SetAction(Field.Action.e_keystroke, "event.rc = /^[A-Za-z]+$/.test(event.change);")`) se ti serve una validazione lato client.  
- **Performance:** Quando lavori con PDF di grandi dimensioni, chiama `doc.Lock()` prima di operazioni bulk per ridurre l'overhead I/O.  
- **Accessibilità:** Imposta la proprietà `AlternateName` così i lettori di schermo possono descrivere il campo.

---

## Conclusione

Abbiamo appena **creato un campo di testo PDF**, mostrato come **duplicare un campo di modulo PDF** su più pagine, e dimostrato il modo più semplice per **add textbox to PDF form** usando C#. Il codice completo e eseguibile è sopra, e puoi estenderlo con stile, validazione o pagine aggiuntive secondo le necessità.

Pronto per il passo successivo? Prova a inserire un menu a discesa (`ChoiceField`) o un widget di firma, oppure esplora come appiattire il modulo dopo l'inserimento dei dati per scopi di archiviazione. Il PDFTron SDK (o qualsiasi libreria comparabile) ti fornisce i mattoni di base—la tua immaginazione decide la forma finale.

Se incontri difficoltà, lascia un commento qui sotto o consulta la documentazione ufficiale della libreria; è ricca di esempi che completano quanto trattato qui. Buon coding, e che i tuoi moduli rimangano sempre sincronizzati!

## Cosa dovresti imparare dopo?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive e a esplorare approcci di implementazione alternativi nei tuoi progetti.

- [How to Create PDF with Aspose – Add Form Field and Pages](/pdf/english/net/programming-with-forms/how-to-create-pdf-with-aspose-add-form-field-and-pages/)
- [Add Form Field in PDF Document using Java](/pdf/english/java/pdf-form-fields/add-form-field-in-pdf-document-using-java/)
- [Add Form Field In Pdf Document Using Java](/pdf/german/java/pdf-form-fields/add-form-field-in-pdf-document-using-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}