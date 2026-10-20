---
category: general
date: 2026-09-05
description: Crea un documento PDF in C# aggiungendo una pagina vuota, disegnando
  un rettangolo e salvando il file PDF. Segui un esempio passo‑passo di Aspose.PDF.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create pdf document
- add blank page pdf
- draw rectangle pdf
- save pdf file
- how to add rectangle
language: it
lastmod: 2026-09-05
og_description: Crea un documento PDF in C# aggiungendo una pagina vuota, disegnando
  un rettangolo e salvando il file PDF. Segui questo esempio completo con Aspose.PDF.
og_image_alt: Screenshot showing a PDF document with a drawn rectangle on a blank
  page
og_title: Crea un documento PDF con pagina vuota e rettangolo – Guida C#
schemas:
- author: Aspose
  dateModified: '2026-09-05'
  description: Create PDF document in C# by adding a blank page, drawing a rectangle,
    and saving the PDF file. Follow a step‑by‑step Aspose.PDF example.
  headline: How to create PDF document with a blank page and rectangle
  type: TechArticle
- description: Create PDF document in C# by adding a blank page, drawing a rectangle,
    and saving the PDF file. Follow a step‑by‑step Aspose.PDF example.
  name: How to create PDF document with a blank page and rectangle
  steps:
  - name: 'Edge case: custom page size'
    text: 'If your layout requires a 6 × 9 inch page, replace the default call with:'
  - name: 'Pro tip: styling the rectangle'
    text: 'You can change the stroke color and line width:'
  - name: 'Edge case: overwriting existing files'
    text: 'Aspose.PDF overwrites an existing file by default. To protect previous
      outputs, check for file existence first:'
  - name: Expected output
    text: Running the program creates a single‑page PDF. When you open `output.pdf`
      you will see a blank white page with a red rectangle positioned 100 points from
      the left and bottom edges, measuring 200 × 200 points.
  type: HowTo
tags:
- PDF
- C#
- Aspose.PDF
- PDF generation
title: Come creare un documento PDF con una pagina vuota e un rettangolo
url: /it/net/document-creation/how-to-create-pdf-document-with-a-blank-page-and-rectangle/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come creare un documento PDF con una pagina vuota e un rettangolo

Se hai bisogno di **creare un documento PDF** programmaticamente, questa guida mostra una soluzione completa in C#. Imparerai come aggiungere una pagina vuota, disegnare un rettangolo su quella pagina e infine salvare il file PDF. L'esempio utilizza la libreria Aspose.PDF, che funziona con .NET 6+ e .NET Framework 4.5+.

Aggiungere una pagina vuota e disegnare forme è una necessità comune per fatture, certificati o report personalizzati. Alla fine di questo tutorial avrai un progetto eseguibile che produce un PDF contenente un unico rettangolo posizionato a (100, 100) con una dimensione di 200 × 200 punti.

## Prerequisiti

* Visual Studio 2022 (o qualsiasi IDE C#)
* .NET 6 SDK o .NET Framework 4.5+
* Aspose.PDF for .NET NuGet package  
  ```bash
  dotnet add package Aspose.PDF
  ```
* Permesso di scrittura sulla directory di output

Non è necessaria alcuna configurazione aggiuntiva; il codice funziona subito.

## Creare documento PDF – panoramica

L'intero processo consiste in quattro passaggi logici:

1. **Instantiate** un oggetto `Document` – rappresenta il file PDF.
2. **Add a blank page** – la pagina fornisce una tela per il disegno.
3. **Draw a rectangle** – un oggetto `Path` definisce la forma.
4. **Save the PDF file** – salva il documento su disco.

Ogni passaggio è isolato nella propria sezione così puoi riutilizzare o sostituire le parti secondo necessità.

![Diagram of a PDF with a rectangle on a blank page](https://example.com/placeholder-image.png){.img-fluid alt="Screenshot che mostra un documento PDF con un rettangolo disegnato su una pagina vuota"}

## Aggiungere pagina vuota pdf

Un PDF deve contenere almeno una pagina prima di poter inserire grafica. Il metodo `Pages.Add()` crea una pagina vuota con dimensioni predefinite (A4). Se ti serve una dimensione diversa, passa un argomento `PageSize`.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

// Step 1: Create a new PDF document
using var pdfDocument = new Document();

// Step 2: Add a blank page to the document
Page pdfPage = pdfDocument.Pages.Add();   // adds an A4 page by default
```

*Perché questo passaggio è importante* – L'oggetto pagina contiene collezioni per testo, immagini e grafica vettoriale. Senza una pagina, qualsiasi tentativo di aggiungere un rettangolo genererebbe un'eccezione.

### Caso limite: dimensione pagina personalizzata

Se il tuo layout richiede una pagina di 6 × 9 pollici, sostituisci la chiamata predefinita con:

```csharp
var pageSize = new Size(432, 648); // 72 points per inch
Page pdfPage = pdfDocument.Pages.Add(pageSize);
```

## Disegnare rettangolo pdf

Disegnare un rettangolo consiste nel creare una geometria `Rectangle` e avvolgerla in un `Path`. La chiamata `ValidateBounds()` garantisce che la forma rientri nei margini della pagina, evitando il ritaglio.

```csharp
// Step 3: Define a rectangle shape (x, y, width, height)
Rectangle shapeRect = new Rectangle(100, 100, 200, 200);

// Step 4: Add the rectangle to the page contents
Path rectanglePath = new Path(shapeRect).ValidateBounds();
pdfPage.Contents.Add(rectanglePath);
```

*Perché questo passaggio è importante* – L'oggetto `Path` è la primitiva vettoriale di basso livello usata da Aspose.PDF. Convalidando i limiti eviti errori di runtime quando il rettangolo supera i limiti della pagina.

### Consiglio professionale: stilizzare il rettangolo

Puoi modificare il colore del tratto e lo spessore della linea:

```csharp
rectanglePath.GraphInfo = new GraphInfo
{
    StrokeColor = Color.Red,
    LineWidth = 2
};
```

Questo produce un contorno rosso con uno spessore di 2 punti.

## Salvare file pdf

Persistere il documento finalizza il file su disco. Il metodo `Save` accetta un percorso file o uno stream. Fornire un percorso assoluto rende la posizione esplicita, utile per script di automazione.

```csharp
// Step 5: Save the PDF to a file
string outputPath = Path.Combine(Environment.CurrentDirectory, "output.pdf");
pdfDocument.Save(outputPath);
Console.WriteLine($"PDF saved to {outputPath}");
```

*Perché questo passaggio è importante* – Il salvataggio è l'unico momento in cui la rappresentazione in memoria diventa un file fisico. Se devi restituire il PDF da una web API, sostituisci il percorso file con un `MemoryStream`.

### Caso limite: sovrascrivere file esistenti

Aspose.PDF sovrascrive un file esistente per impostazione predefinita. Per proteggere le uscite precedenti, verifica prima l'esistenza del file:

```csharp
if (File.Exists(outputPath))
{
    File.Delete(outputPath);
}
pdfDocument.Save(outputPath);
```

## Come aggiungere un rettangolo – migliori pratiche

* **Keep coordinates within the page margins** – usa `ValidateBounds()` o calcola i margini manualmente.
* **Reuse `GraphInfo` objects** quando disegni più forme; questo riduce l'allocazione di memoria.
* **Dispose of the `Document` object** (come mostrato con `using var`) per liberare rapidamente le risorse native.
* **Test with different DPI settings** se in seguito incorpori immagini raster; le forme vettoriali come i rettangoli rimangono nitide a qualsiasi risoluzione.

## Esempio completo funzionante

Di seguito trovi il programma completo che puoi copiare in un'applicazione console. Compila senza modifiche e produce `output.pdf` nella cartella del progetto.

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using Aspose.Pdf.Color;

class Program
{
    static void Main()
    {
        // Create a new PDF document
        using var pdfDocument = new Document();

        // Add a blank page to the document
        Page pdfPage = pdfDocument.Pages.Add();

        // Define a rectangle shape (x, y, width, height)
        Rectangle shapeRect = new Rectangle(100, 100, 200, 200);

        // Create a path for the rectangle and validate its bounds
        Path rectanglePath = new Path(shapeRect).ValidateBounds();

        // Optional: style the rectangle (red outline, 2‑pt width)
        rectanglePath.GraphInfo = new GraphInfo
        {
            StrokeColor = Color.Red,
            LineWidth = 2
        };

        // Add the rectangle to the page contents
        pdfPage.Contents.Add(rectanglePath);

        // Determine output path
        string outputPath = Path.Combine(Environment.CurrentDirectory, "output.pdf");

        // Ensure no leftover file blocks the save operation
        if (File.Exists(outputPath))
        {
            File.Delete(outputPath);
        }

        // Save the PDF to a file
        pdfDocument.Save(outputPath);
        Console.WriteLine($"PDF saved to {outputPath}");
    }
}
```

### Output previsto

Eseguendo il programma si crea un PDF a pagina singola. Quando apri `output.pdf` vedrai una pagina bianca vuota con un rettangolo rosso posizionato a 100 punti dal bordo sinistro e inferiore, con dimensioni di 200 × 200 punti.

## Conclusione

Ora sai come **creare un documento PDF**, **aggiungere una pagina vuota pdf**, **disegnare un rettangolo pdf**, e **salvare il file pdf** usando Aspose.PDF in C#. L'esempio copre le chiamate API essenziali, spiega perché ogni chiamata è necessaria e fornisce consigli per variazioni comuni come dimensioni di pagina personalizzate o stilizzazione del rettangolo.

Successivamente, esplora argomenti correlati come **aggiungere testo**, **incorporare immagini**, o **creare report multi‑pagina**. Lo stesso schema—instanziare un `Document`, manipolare le pagine, aggiungere contenuto vettoriale o raster, poi `Save`—si applica a tutti questi scenari. Sentiti libero di sperimentare con forme, colori e layout di pagina diversi per adattarli alle esigenze del tuo progetto.

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Crea documento PDF C# – Aggiungi pagina, disegna rettangolo e salva](/pdf/english/net/document-creation/create-pdf-document-c-add-page-draw-rectangle-save/)
- [Crea documento PDF con Aspose.PDF – Guida passo‑passo](/pdf/english/net/document-creation/create-pdf-document-with-aspose-pdf-step-by-step-guide/)
- [Crea documento PDF con Aspose – Aggiungi pagina, casella di testo e modulo](/pdf/english/net/forms-annotations/create-pdf-document-with-aspose-add-page-text-box-and-form/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}