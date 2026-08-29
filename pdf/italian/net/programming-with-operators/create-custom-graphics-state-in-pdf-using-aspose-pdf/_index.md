---
category: general
date: 2026-08-20
description: Crea uno stato grafico personalizzato in PDF con Aspose.Pdf. Scopri come
  modificare le risorse PDF e aggiungere la trasparenza al PDF in pochi passaggi.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create custom graphics state
- edit pdf resources
- add transparency pdf
- Aspose.Pdf graphics state
- PDF resource dictionary
language: it
lastmod: 2026-08-20
og_description: Crea uno stato grafico personalizzato in PDF con Aspose.Pdf. Questo
  tutorial mostra come modificare le risorse PDF e aggiungere rapidamente la trasparenza
  al PDF.
og_image_alt: Screenshot of C# code that creates a custom graphics state in a PDF
og_title: Crea stato grafico personalizzato in PDF – Guida Aspose.Pdf
schemas:
- author: Aspose
  dateModified: '2026-08-20'
  description: Create custom graphics state in PDF with Aspose.Pdf. Learn how to edit
    PDF resources and add transparency PDF in just a few steps.
  headline: Create custom graphics state in PDF using Aspose.Pdf
  type: TechArticle
tags:
- PDF
- Aspose.Pdf
- C#
- Graphics state
title: Crea uno stato grafico personalizzato in PDF usando Aspose.Pdf
url: /it/net/programming-with-operators/create-custom-graphics-state-in-pdf-using-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crea uno stato grafico personalizzato in PDF usando Aspose.Pdf

Se hai bisogno di **creare uno stato grafico personalizzato** in un PDF, questa guida ti mostra esattamente come farlo con Aspose.Pdf per .NET. Alla fine del tutorial sarai in grado di **modificare le risorse PDF**, inserire un nuovo dizionario di stato grafico e **aggiungere contenuto PDF con trasparenza** senza uscire dal tuo progetto C#.

Vedrai un esempio completo e eseguibile, una spiegazione del perché ogni riga è importante e consigli per gestire documenti multi‑pagina o diversi blend mode. Non sono richiesti strumenti esterni—solo la libreria Aspose.Pdf e un ambiente di sviluppo .NET di base.

## Prerequisiti

* .NET 6.0 o versioni successive (il codice funziona anche con .NET Framework 4.7+)
* Una copia con licenza di **Aspose.Pdf for .NET** (la versione di prova gratuita è valida per i test)
* Un file PDF di input chiamato `input.pdf` posizionato in una cartella a cui puoi fare riferimento dal codice
* Visual Studio 2022 o qualsiasi IDE che supporti lo sviluppo C#

Il tutorial presuppone che tu abbia familiarità con la sintassi di base di C# e il concetto di pagine PDF.

## Passo 1: Carica il PDF di origine e accedi alla prima pagina

La prima operazione è aprire il file PDF e recuperare la pagina le cui risorse desideri modificare. Aspose.Pdf rappresenta ogni pagina come un oggetto `Page`, e ogni pagina contiene un **dizionario delle risorse** che memorizza gli stati grafici, i font, gli XObject e altro.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Operators;
using Aspose.Pdf.InteractiveFeatures;
using Aspose.Pdf.Text;
using Aspose.Pdf.Facades;
using System.Collections.Generic;

// Load the PDF you want to edit
using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
{
    // Get the first page (pages are 1‑based in Aspose.Pdf)
    Page firstPage = pdfDocument.Pages[1];
```

*Perché è importante:* La classe `Document` carica il file in memoria, e `Pages[1]` ti dà accesso diretto al dizionario delle risorse della prima pagina, dove risiede uno stato grafico.

## Passo 2: Apri il dizionario delle risorse per la modifica

Aspose.Pdf fornisce un helper `DictionaryEditor` che ti permette di trattare un dizionario delle risorse come un normale `Dictionary` .NET. Questo rende semplice leggere, aggiungere o sostituire voci come `ExtGState`.

```csharp
    // Create an editor for the page’s resources
    var resourcesEditor = new DictionaryEditor(firstPage.Resources);
```

*Perché è importante:* `DictionaryEditor` astrae gli oggetti COS di basso livello, consentendoti di lavorare con coppie chiave/valore familiari mantenendo la conformità PDF.

## Passo 3: Recupera (o crea) il dizionario ExtGState

La voce **ExtGState** contiene tutti gli oggetti di stato grafico esterno per la pagina. Se il dizionario non esiste, Aspose.Pdf ne creerà uno vuoto per te.

```csharp
    // Ensure the ExtGState dictionary exists
    var extGStateDict = resourcesEditor.ContainsKey("ExtGState")
        ? resourcesEditor["ExtGState"].ToCosPdfDictionary()
        : new CosPdfDictionary(pdfDocument);
```

*Perché è importante:* Un'entrata `ExtGState` mancante causerebbe una `KeyNotFoundException` in seguito. Questa verifica consente al codice di funzionare su PDF che non hanno mai definito uno stato grafico personalizzato—una parte essenziale della robustezza di **edit PDF resources**.

## Passo 4: Costruisci il dizionario dello stato grafico personalizzato

Uno stato grafico descrive come vengono renderizzate le operazioni di disegno. Per **add transparency PDF**, è necessario impostare le voci `ca` (opacità di riempimento) e `CA` (opacità del tratto), e facoltativamente un blend mode (`BM`). Il codice seguente costruisce un nuovo dizionario con questi parametri.

```csharp
    // Create an empty dictionary that will become the new graphics state
    var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

    // Define the parameters you want for the custom state
    var graphicsStateParams = new KeyValuePair<string, ICosPdfPrimitive>[]
    {
        // Stroke opacity (1 = fully opaque)
        new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
        // Fill opacity (0.5 = 50 % transparent)
        new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
        // Blend mode – "Normal" is the default, but you can use "Multiply", "Screen", etc.
        new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
    };

    // Populate the dictionary with the parameters
    foreach (var param in graphicsStateParams)
        newGraphicsState.Add(param);
```

*Perché è importante:* Le voci `ca` e `CA` controllano la trasparenza per le operazioni di riempimento e di tratto, rispettivamente. Impostare `BM` ti permette di sperimentare diversi effetti di composizione, utile quando successivamente **add transparency PDF** contenuti come forme o immagini semi‑trasparenti.

## Passo 5: Registra il nuovo stato grafico con un nome univoco

Ogni stato grafico nel dizionario `ExtGState` deve avere un nome univoco (ad esempio `GS0`, `GS1`). Puoi scegliere qualsiasi nome che non confligga con le voci esistenti.

```csharp
    // Choose a name that is unlikely to collide with existing states
    const string graphicsStateName = "GS0";

    // Add the new graphics state to the ExtGState dictionary
    extGStateDict.Add(graphicsStateName, newGraphicsState);

    // If the ExtGState entry was missing, attach it back to the page resources
    if (!resourcesEditor.ContainsKey("ExtGState"))
        resourcesEditor["ExtGState"] = extGStateDict;
```

*Perché è importante:* Inserendo il nuovo dizionario sotto `GS0`, rendi lo stato indirizzabile dai flussi di contenuto della pagina. Il blocco condizionale garantisce che la voce `ExtGState` sia presente anche per i PDF che ne erano privi—un'ulteriore salvaguardia di **edit PDF resources**.

## Passo 6: Usa lo stato grafico personalizzato nel contenuto della pagina (opzionale)

I passaggi precedenti *definiscono* solo lo stato grafico. Per vedere effettivamente l'effetto, devi fare riferimento ad esso nel flusso di contenuto della pagina. Di seguito un rapido esempio che disegna un rettangolo semi‑trasparente usando lo stato appena creato.

```csharp
    // Get the page’s content stream (or create a new one if empty)
    var content = firstPage.Contents[1];
    var graphics = new ContentWriter(content);

    // Save current graphics state
    graphics.WriteOperator(OperatorName.SaveState);
    // Set the custom graphics state we just defined
    graphics.WriteOperand($"/{graphicsStateName}");
    graphics.WriteOperator(OperatorName.SetExtGState);
    // Draw a rectangle (coordinates are in points)
    graphics.WriteOperand(100);   // lower‑left x
    graphics.WriteOperand(500);   // lower‑left y
    graphics.WriteOperand(200);   // width
    graphics.WriteOperand(100);   // height
    graphics.WriteOperator(OperatorName.Rectangle);
    // Fill the rectangle using the current fill opacity (ca = 0.5)
    graphics.WriteOperator(OperatorName.Fill);
    // Restore the previous graphics state
    graphics.WriteOperator(OperatorName.RestoreState);
```

*Perché è importante:* L'operatore `SetExtGState` (`gs`) indica al renderer PDF di applicare i parametri definiti in `GS0`. Il rettangolo apparirà con un'opacità di riempimento del 50 % mentre il suo tratto rimarrà completamente opaco.

## Passo 7: Salva il PDF modificato

Infine, scrivi le modifiche su disco. Puoi sovrascrivere il file originale o crearne uno nuovo.

```csharp
    // Save the updated PDF
    pdfDocument.Save("YOUR_DIRECTORY/output_with_custom_gs.pdf");
}
```

Quando apri `output_with_custom_gs.pdf` in un visualizzatore PDF, dovresti vedere un rettangolo semi‑trasparente nella prima pagina. Questo conferma che hai creato con successo **create custom graphics state**, **edit PDF resources**, e **add transparency PDF** contenuti.

## Variazioni comuni e casi limite

| Situazione | Cosa regolare |
|-----------|----------------|
| **Più pagine necessitano dello stesso stato** | Registra lo stato grafico una volta (passi 1‑5) e fai riferimento a `GS0` nel flusso di contenuto di qualsiasi pagina. |
| **Opacità diversa per elemento** | Definisci stati aggiuntivi (`GS1`, `GS2`, …) con valori `ca`/`CA` differenti e passa da uno all'altro usando `SetExtGState`. |
| **Blend mode diverso da Normal** | Sostituisci `"Normal"` con `"Multiply"`, `"Screen"` o qualsiasi blend mode standard PDF nella voce `BM`. |
| **Collisione di nome** | Prima di aggiungere, verifica `extGStateDict.ContainsKey(yourName)` e scegli un suffisso univoco se necessario. |
| **Il PDF contiene già un dizionario ExtGState** | Il codice nel Passo 3 riutilizza già il dizionario esistente, quindi non è necessario alcun ulteriore trattamento. |

**Consiglio professionale:** Quando lavori con PDF di grandi dimensioni, avvolgi l'uso di `Document` in un blocco `using` (come mostrato) per rilasciare rapidamente le risorse native. Inoltre, considera di abilitare la proprietà `PdfCompliance` di Aspose.Pdf se devi garantire la conformità PDF/A o PDF/X dopo la modifica delle risorse.

## Esempio completo funzionante

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Operators;
using Aspose.Pdf.InteractiveFeatures;
using Aspose.Pdf.Text;
using Aspose.Pdf.Facades;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        // Load the PDF you want to edit
        using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
        {
            // Step 1: Get the first page
            Page firstPage = pdfDocument.Pages[1];

            // Step 2: Open the page resources for editing
            var resourcesEditor = new DictionaryEditor(firstPage.Resources);

            // Step 3: Retrieve or create the ExtGState dictionary
            var extGStateDict = resourcesEditor.ContainsKey("ExtGState")
                ? resourcesEditor["ExtGState"].ToCosPdfDictionary()
                : new CosPdfDictionary(pdfDocument);

            // Step 4: Build a custom graphics state (50 % fill opacity, 100 % stroke opacity)
            var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            var graphicsStateParams = new KeyValuePair<string, ICosPdfPrimitive>[]
            {
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
            };
            foreach (var param in graphicsStateParams)
                newGraphicsState.Add(param);

            // Step 5: Register the graphics state under the name GS0
            const string graphicsStateName = "GS0";
            extGStateDict.Add(graphicsStateName, newGraphics


## Cosa dovresti imparare dopo?

I tutorial seguenti coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Come creare PDF con Aspose – Aggiungere campo modulo e pagine](/pdf/english/net/programming-with-forms/how-to-create-pdf-with-aspose-add-form-field-and-pages/)
- [Come creare tabelle personalizzate nei PDF usando Aspose.PDF .NET](/pdf/english/net/tables-lists/create-custom-tables-in-pdfs-aspose-pdf-dot-net/)
- [Crea timbri PDF personalizzati Aspose Pdf Net](/pdf/hongkong/net/images-graphics/create-custom-pdf-stamps-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}