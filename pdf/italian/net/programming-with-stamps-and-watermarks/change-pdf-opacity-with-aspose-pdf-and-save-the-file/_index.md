---
category: general
date: 2026-11-12
description: Impara come modificare l'opacità di un PDF usando Aspose.Pdf, aggiungere
  trasparenza, impostare la modalità di fusione e salvare il PDF modificato in C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- change PDF opacity
- how to add transparency
- save modified PDF
- how to set blend mode
- set fill opacity
language: it
lastmod: 2026-11-12
og_description: Modifica l'opacità dei PDF con Aspose.Pdf, scopri come aggiungere
  trasparenza, impostare la modalità di fusione e salvare i file PDF modificati in
  C#.
og_image_alt: Screenshot of a PDF page with altered opacity using Aspose.Pdf
og_title: Modifica l'opacità del PDF con Aspose.Pdf – aggiungi trasparenza e salva
schemas:
- author: Aspose
  dateModified: '2026-11-12'
  description: Learn how to change PDF opacity using Aspose.Pdf, add transparency,
    set blend mode, and save modified PDF in C#.
  headline: Change PDF opacity with Aspose.Pdf and save the file
  type: TechArticle
- description: Learn how to change PDF opacity using Aspose.Pdf, add transparency,
    set blend mode, and save modified PDF in C#.
  name: Change PDF opacity with Aspose.Pdf and save the file
  steps:
  - name: Load the PDF document
    text: Start by creating a `Document` instance that points to your source file.
      The constructor reads the entire PDF into memory, allowing you to manipulate
      its internal objects.
  - name: Access the first page’s resources
    text: Each PDF page stores a *resource dictionary* that holds objects such as
      fonts, images, and graphics states. You need to edit this dictionary to inject
      a new `ExtGState` entry.
  - name: Ensure an ExtGState dictionary exists
    text: The `ExtGState` dictionary holds custom graphics states. If it does not
      exist, the code creates one automatically.
  - name: Define a new graphics state (ExtGState)
    text: A graphics state defines how drawing operations behave. The following dictionary
      sets stroke opacity (`CA`), fill opacity (`ca`), and blend mode (`BM`).
  - name: Register the graphics state in the resource dictionary
    text: Give the new state a name (e.g., `GS0`) and add it to the `ExtGState` dictionary.
      This name will be referenced later in the page content stream.
  - name: Apply the graphics state to page content
    text: To actually see the opacity effect, insert the `/GS0 gs` operator before
      the drawing commands you want to affect. The example below draws a semi‑transparent
      rectangle.
  - name: Save the modified PDF
    text: Finally, write the updated document to disk. The `Save` method overwrites
      the target file or creates a new one if it does not exist.
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Modifica l'opacità del PDF con Aspose.Pdf e salva il file
url: /it/net/programming-with-stamps-and-watermarks/change-pdf-opacity-with-aspose-pdf-and-save-the-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Modifica l'opacità PDF con Aspose.Pdf e salva il file

Se hai bisogno di **cambiare l'opacità di un PDF** in un documento, Aspose.Pdf fornisce un'API semplice per regolare sia la trasparenza del tratto che del riempimento. Questo tutorial mostra esattamente **come aggiungere trasparenza**, **come impostare la modalità di fusione** e **salvare i PDF modificati** con poche righe di codice C#.

Seguirai ogni passaggio—dall'apertura di un PDF esistente alla definizione di un nuovo stato grafico e al salvataggio delle modifiche. Alla fine di questa guida potrai:

* Ridurre la visibilità di grafica vettoriale o immagini.
* Applicare una modalità di fusione personalizzata come *Normal* o *Multiply*.
* Esportare il file aggiornato senza perdere alcun altro contenuto.

L'unico prerequisito è un ambiente di sviluppo .NET funzionante e un riferimento alla libreria Aspose.Pdf (versione 23.9 o successiva). Non sono necessari strumenti esterni.

## Prerequisiti

| Requisito | Perché è importante |
|-------------|----------------|
| .NET 6.0 SDK or later | Garantisce la compatibilità con le API più recenti di Aspose.Pdf. |
| Aspose.Pdf for .NET NuGet package | Fornisce le classi `Document`, `CosPdfDictionary` e correlate utilizzate nel codice. |
| A PDF file to edit (e.g., `input.pdf`) | Serve come sorgente per le modifiche di opacità. |

Installa il pacchetto NuGet con:

```bash
dotnet add package Aspose.Pdf
```

## Modifica l'opacità PDF con Aspose.Pdf

### Passo 1: Carica il documento PDF

Inizia creando un'istanza di `Document` che punti al tuo file di origine. Il costruttore legge l'intero PDF in memoria, consentendoti di manipolare i suoi oggetti interni.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Operators;
using Aspose.Pdf.XObjects;
using Aspose.Pdf.Facades;

// Load the existing PDF
var pdfDoc = new Document(@"YOUR_DIRECTORY\input.pdf");
```

> **Perché questo passo?** Il caricamento del file crea un modello di oggetti manipolabile. Tutte le modifiche successive operano su questa rappresentazione in‑memoria, garantendo che il file originale rimanga intatto fino a quando non lo salvi esplicitamente.

### Passo 2: Accedi alle risorse della prima pagina

Ogni pagina PDF memorizza un *dizionario delle risorse* che contiene oggetti come font, immagini e stati grafici. È necessario modificare questo dizionario per inserire una nuova voce `ExtGState`.

```csharp
// Retrieve the first page (pages are 1‑based)
var page = pdfDoc.Pages[1];

// The DictionaryEditor simplifies access to the page's resource dictionary
var resourcesEditor = new DictionaryEditor(page.Resources);
```

> **Suggerimento:** Se il tuo PDF contiene più pagine che necessitano della stessa opacità, ripeti questo passo per ogni pagina o condividi un unico `ExtGState` tra le pagine.

### Passo 3: Assicurati che esista un dizionario ExtGState

Il dizionario `ExtGState` contiene stati grafici personalizzati. Se non esiste, il codice ne crea uno automaticamente.

```csharp
// Get or create the ExtGState dictionary
var extGStateDict = resourcesEditor["ExtGState"]?.ToCosPdfDictionary()
                     ?? new CosPdfDictionary(pdfDoc);
resourcesEditor["ExtGState"] = extGStateDict;
```

> **Perché questo passo?** Senza un contenitore `ExtGState`, qualsiasi tentativo di fare riferimento a un nuovo stato grafico fallirebbe, risultando in un PDF che ignora le impostazioni di opacità.

### Passo 4: Definisci un nuovo stato grafico (ExtGState)

Uno stato grafico definisce come si comportano le operazioni di disegno. Il dizionario seguente imposta l'opacità del tratto (`CA`), l'opacità del riempimento (`ca`) e la modalità di fusione (`BM`).

```csharp
// Create an empty dictionary for the new graphics state
var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDoc);

// Set desired parameters
var parameters = new[]
{
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),   // Stroke opacity (1 = opaque)
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // Fill opacity (0.5 = 50% transparent)
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // Blend mode
};

foreach (var param in parameters)
    newGraphicsState.Add(param);
```

> **Come impostare l'opacità di riempimento:** L'entry `ca` controlla l'opacità delle forme riempite (testo, percorsi). Regola il valore numerico tra `0` (completamente trasparente) e `1` (completamente opaco) per soddisfare i requisiti del tuo design.

> **Come impostare la modalità di fusione:** L'entry `BM` seleziona l'algoritmo di composizione. I valori comuni includono `Normal`, `Multiply`, `Screen` e `Overlay`. Scegli quello che corrisponde alla tua intenzione visiva.

### Passo 5: Registra lo stato grafico nel dizionario delle risorse

Assegna al nuovo stato un nome (ad es., `GS0`) e aggiungilo al dizionario `ExtGState`. Questo nome verrà referenziato più tardi nel flusso di contenuto della pagina.

```csharp
// Add the graphics state with a symbolic name
extGStateDict.Add("GS0", newGraphicsState);
```

> **Consiglio professionale:** Usa una convenzione di denominazione come `GS0`, `GS1`, … quando crei più stati. Previene collisioni di nomi e rende il debug più semplice.

### Passo 6: Applica lo stato grafico al contenuto della pagina

Per vedere effettivamente l'effetto di opacità, inserisci l'operatore `/GS0 gs` prima dei comandi di disegno che desideri influenzare. L'esempio sotto disegna un rettangolo semi‑trasparente.

```csharp
// Build a content stream that uses the new graphics state
var content = new MemoryStream();
var writer = new StreamWriter(content);

// Activate the graphics state
writer.WriteLine("q");                 // Save graphics state
writer.WriteLine("/GS0 gs");           // Apply custom ExtGState
writer.WriteLine("0.2 0.5 0.8 rg");    // Set fill color (RGB)
writer.WriteLine("100 500 200 100 re"); // Rectangle (x y width height)
writer.WriteLine("f");                 // Fill rectangle
writer.WriteLine("Q");                 // Restore graphics state
writer.Flush();

content.Position = 0;
page.Contents.Add(new ContentStream(content));
```

> **Perché gli operatori `q` e `Q`?** Spingono e rimuovono dallo stack lo stato grafico, garantendo che la modifica di opacità influisca solo sul rettangolo e non sul resto della pagina.

### Passo 7: Salva il PDF modificato

Infine, scrivi il documento aggiornato su disco. Il metodo `Save` sovrascrive il file di destinazione o ne crea uno nuovo se non esiste.

```csharp
// Persist the changes
pdfDoc.Save(@"YOUR_DIRECTORY\output.pdf");
```

> **Come salvare il PDF modificato:** La chiamata `Save` scrive tutte le modifiche in‑memoria, incluso il nuovo `ExtGState`, nel percorso specificato. Puoi anche inviare il risultato a un `MemoryStream` per risposte web.

## Esempio completo funzionante

Di seguito trovi un programma unico e autonomo che incorpora tutti i passaggi descritti sopra. Copialo in un'applicazione console ed eseguilo per verificare la modifica dell'opacità.

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.XObjects;
using Aspose.Pdf.Facades;
using Aspose.Pdf.Operators;

class ChangePdfOpacityDemo
{
    static void Main()
    {
        // 1. Load the PDF
        var pdfDoc = new Document(@"YOUR_DIRECTORY\input.pdf");

        // 2. Get first page and its resources
        var page = pdfDoc.Pages[1];
        var resourcesEditor = new DictionaryEditor(page.Resources);

        // 3. Ensure ExtGState dictionary exists
        var extGStateDict = resourcesEditor["ExtGState"]?.ToCosPdfDictionary()
                             ?? new CosPdfDictionary(pdfDoc);
        resourcesEditor["Ext


## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare ulteriori funzionalità dell'API ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Come salvare un PDF modificato con Aspose.Pdf e aggiungere trasparenza](/pdf/english/net/document-manipulation/how-to-save-modified-pdf-with-aspose-pdf-and-add-transparenc/)
- [Come aggiungere trasparenza a un PDF usando Aspose.PDF in C#](/pdf/english/net/images-graphics/how-to-add-transparency-to-pdf-using-aspose-pdf-in-c/)
- [Come aggiungere lo stato grafico a un PDF e controllare la trasparenza con Aspose.PDF](/pdf/english/net/images-graphics/how-to-add-graphics-state-pdf-and-control-transparency-with/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}