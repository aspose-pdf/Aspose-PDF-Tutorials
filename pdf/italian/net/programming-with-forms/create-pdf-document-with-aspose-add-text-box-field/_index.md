---
category: general
date: 2026-03-24
description: Crea un documento PDF usando Aspose.PDF in C#. Scopri come aggiungere
  un campo modulo PDF di tipo casella di testo e aggiungere rapidamente un campo modulo
  PDF.
draft: false
keywords:
- create pdf document
- add text box pdf
- add form field pdf
- how to create pdf
- how to add textbox
language: it
og_description: Crea un documento PDF con Aspose.PDF in C#. Questa guida mostra come
  aggiungere un campo modulo PDF di tipo casella di testo e inserire un campo modulo
  PDF in pochi minuti.
og_title: Crea documento PDF con Aspose – Aggiungi campo casella di testo
tags:
- Aspose.PDF
- C#
- PDF Forms
title: Crea documento PDF con Aspose – Aggiungi campo casella di testo
url: /it/net/programming-with-forms/create-pdf-document-with-aspose-add-text-box-field/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crea documento PDF con Aspose – Aggiungi campo casella di testo

Hai mai avuto bisogno di **creare un documento PDF** programmaticamente e ti sei chiesto da dove cominciare? Non sei l'unico—molti sviluppatori si trovano di fronte a questo ostacolo quando le loro app devono raccogliere input dell'utente senza introdurre una pesante libreria UI. La buona notizia? Con Aspose.PDF per .NET puoi generare un PDF, inserire una casella di testo su qualsiasi pagina e persino collegare lo stesso campo a più pagine—tutto in poche righe.

In questo tutorial percorreremo l'intero processo: dall'inizializzazione del PDF, all'**add text box PDF** dei campi modulo, alla **add form field PDF** registrazione, e infine come verificare che tutto funzioni. Alla fine saprai **come creare PDF** interattivi e vedrai anche **come aggiungere textbox** controlli che si comportano esattamente come i campi nativi di Acrobat.

---

## Cosa ti serve

- **ASP.NET Core** o qualsiasi progetto .NET 6+ (il codice funziona anche su .NET Framework 4.6+).  
- **Aspose.PDF for .NET** pacchetto NuGet (versione 23.9 o successiva).  
- Una discreta esperienza in C#—nulla di complicato, solo le basi.  

Se hai spuntato queste caselle, siamo pronti. Nessuno strumento aggiuntivo, nessun servizio esterno, solo puro codice C# che puoi incollare in un'app console e eseguire.

---

## Crea documento PDF e aggiungi un campo modulo casella di testo

Il primo passo, come ci si aspetta, è **create PDF document**. Pensa alla classe `Document` come a una tela vuota; una volta che la hai, puoi iniziare a dipingere pagine, forme ed elementi interattivi.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Forms;

// Step 1: Create a new PDF document (the blank canvas)
using var document = new Document();

// Step 2: Add a new page where the text box will live
var page1 = document.Pages.Add();
```

> **Why this matters:** L'istanziazione di `Document` senza pagine genera un'eccezione nel momento in cui provi a posizionare un widget. Aggiungere prima una pagina garantisce un indice di pagina valido (`Pages[1]`) per i passaggi successivi.

---

## Aggiungi un campo modulo casella di testo PDF alla pagina 1

Ora che abbiamo una pagina, aggiungiamo un campo modulo **add text box PDF**. La classe `TextBoxField` rappresenta un singolo campo logico; puoi considerarlo come il “nome” dell'input che può apparire in molti punti.

```csharp
// Step 3: Define the rectangle where the textbox will appear (x, y, width, height)
var textBoxRect = new Rectangle(100, 500, 300, 520);

// Step 4: Create the text box field on page 1
var textBoxField = new TextBoxField(document.Pages[1], textBoxRect)
{
    // This logical name is used later when you retrieve the value
    PartialName = "MultiWidget"
};
```

> **Pro tip:** Il rettangolo utilizza i punti (1/72 di pollice). Regola le coordinate per adattarle al tuo layout; l'origine (0,0) è nell'angolo in basso a sinistra della pagina.

---

## Crea un secondo widget su un'altra pagina

Un singolo campo logico può avere più widget visivi—perfetto per moduli multi‑pagina. Ecco **how to add textbox** su una seconda pagina, riutilizzando lo stesso nome del campo.

```csharp
// Step 5: Add a second page for the extra widget
var page2 = document.Pages.Add();

// Step 6: Create a widget for the same field on page 2
var secondWidget = textBoxField.CreateWidget(new Rectangle(100, 400, 300, 420));
```

> **Why we do this:** Gli utenti spesso devono inserire le stesse informazioni in sezioni diverse (ad esempio, “Nome” in alto e di nuovo in un riepilogo). Condividendo lo stesso nome logico, Aspose garantisce che entrambi i widget rimangano sincronizzati.

---

## Registra il campo modulo nel PDF

Creare l'oggetto campo non è sufficiente; devi aggiungerlo alla collezione di moduli del documento. Questo è il passaggio in cui **add form field PDF** viene inserito nella struttura interna.

```csharp
// Step 7: Register the field (with both widgets) in the document's form collection
document.Form.Add(textBoxField, "MultiWidget");

// Optional: Save the PDF to disk
document.Save("MultiWidgetExample.pdf");
```

> **What happens under the hood:** `Form.Add` scrive la definizione del campo nel dizionario AcroForm, rendendo il PDF interattivo quando viene aperto in Acrobat Reader o in qualsiasi visualizzatore PDF che supporta i moduli.

---

## Esegui e verifica il risultato

Compila ed esegui l'app console. Apri `MultiWidgetExample.pdf` in Adobe Acrobat (o in qualsiasi visualizzatore che supporta i moduli) e vedrai due caselle di testo identiche nelle pagine 1 e 2. Digita qualcosa in una casella—guarda l'altra aggiornarsi istantaneamente. Questa è la potenza di un campo logico condiviso.

```text
Expected outcome:
- PDF with two pages.
- Each page shows a white rectangle (the text box).
- Editing one box updates the other automatically.
```

Se non vedi le caselle, controlla che i rettangoli siano all'interno dei bordi della pagina e che tu abbia salvato il documento dopo aver aggiunto il campo.

---

## Domande comuni e casi particolari

### E se ho bisogno di un aspetto diverso su ogni pagina?

Puoi personalizzare ogni widget dopo la creazione:

```csharp
secondWidget.Rect = new Rectangle(150, 350, 350, 370); // reposition
secondWidget.Border = new Border(BorderStyle.Solid, 1, Color.Black);
secondWidget.BackgroundColor = Color.LightYellow;
```

### Posso impostare un valore predefinito?

Certo—basta assegnare `Value` prima di salvare:

```csharp
textBoxField.Value = "Enter your name here";
```

Tutti i widget mostreranno quel segnaposto finché l'utente non lo sovrascrive.

### Come rendere il campo obbligatorio?

```csharp
textBoxField.Required = true;
```

Acrobat avviserà l'utente se tenta di inviare il modulo senza compilarlo.

### Funziona con la conformità PDF/A?

Aspose.PDF supporta PDF/A‑1b,‑2b,‑3b. Dopo aver terminato la costruzione del modulo, puoi convertire:

```csharp
document.Convert(new PdfConversionOptions { Compliance = PdfCompliance.PdfA2b });
```

---

## Esempio completo funzionante

Di seguito trovi il programma completo, pronto per il copia‑incolla. Salvalo come `Program.cs` in un progetto console .NET, aggiungi il pacchetto NuGet Aspose.PDF e esegui.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Forms;
using Aspose.Pdf.Drawing;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new PDF document
        using var document = new Document();

        // 2️⃣ Add two pages (page 1 will host the first widget, page 2 the second)
        var page1 = document.Pages.Add();
        var page2 = document.Pages.Add();

        // 3️⃣ Define the rectangle for the first widget
        var rect1 = new Rectangle(100, 500, 300, 520);

        // 4️⃣ Create the text box field (logical name = "MultiWidget")
        var textBoxField = new TextBoxField(document.Pages[1], rect1)
        {
            PartialName = "MultiWidget",
            Value = "Sample text",        // optional default value
            Required = true               // makes the field mandatory
        };

        // 5️⃣ Add a second widget on page

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}