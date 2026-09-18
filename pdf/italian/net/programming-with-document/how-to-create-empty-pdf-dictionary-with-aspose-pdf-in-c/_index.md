---
category: general
date: 2026-09-18
description: Impara a creare un dizionario PDF vuoto in C# usando Aspose.PDF. Questa
  guida passo passo copre ExtGState, lo stato grafico e la manipolazione di CosPdfDictionary.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create empty PDF dictionary
- Aspose.PDF
- ExtGState dictionary
- graphics state
- CosPdfDictionary
- PDF manipulation C#
language: it
lastmod: 2026-09-18
og_description: Crea un dizionario PDF vuoto in C# con Aspose.PDF. Segui questo tutorial
  completo per modificare i dizionari ExtGState e lo stato grafico.
og_image_alt: Screenshot showing creation of an empty PDF dictionary in C#
og_title: Crea un dizionario PDF vuoto in C# – guida completa su Aspose.PDF
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: Learn to create empty PDF dictionary in C# using Aspose.PDF. This step‑by‑step
    guide covers ExtGState, graphics state, and CosPdfDictionary manipulation.
  headline: How to create empty PDF dictionary with Aspose.PDF in C#
  type: TechArticle
tags:
- PDF
- C#
- Aspose.PDF
title: Come creare un dizionario PDF vuoto con Aspose.PDF in C#
url: /it/net/programming-with-document/how-to-create-empty-pdf-dictionary-with-aspose-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come creare un dizionario PDF vuoto con Aspose.PDF in C#

Se hai bisogno di **creare un dizionario PDF vuoto** durante l'elaborazione di un file PDF, questa guida ti mostra esattamente come farlo usando Aspose.PDF per .NET. Che tu stia regolando la trasparenza, i blend mode o qualsiasi stato grafico personalizzato, i passaggi seguenti ti consentono di modificare il dizionario `ExtGState` in modo sicuro ed efficiente.

In questo tutorial imparerai a:

* Caricare un documento PDF con Aspose.PDF.
* Accedere alle risorse della prima pagina e al dizionario `ExtGState` esistente.
* Creare un nuovo `CosPdfDictionary` vuoto e popolarlo con voci di stato grafico.
* Salvare il PDF modificato senza perdere alcun contenuto originale.

La soluzione funziona con qualsiasi PDF che contenga almeno una pagina e richiede solo la libreria Aspose.PDF (versione 23.10 o successiva).

## Prerequisiti

* .NET 6.0 o successivo (il codice funziona anche su .NET Framework 4.8).
* Un riferimento al pacchetto NuGet **Aspose.PDF**.
* Un file PDF di input situato in `YOUR_DIRECTORY/input.pdf`.
* Familiarità di base con C# e concetti PDF come risorse e stato grafico.

> **Pro tip:** Quando lavori con PDF di grandi dimensioni, avvolgi l'oggetto `Document` in un blocco `using` per garantire che tutte le handle dei file vengano rilasciate tempestivamente.

## Passo 1: Caricare il documento PDF

La prima operazione apre il file sorgente. Aspose.PDF legge l'intero documento in memoria, consentendoti di modificare gli oggetti interni.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Step 1: Load the PDF document
using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
{
    // Subsequent steps go here
}
```

*Perché è importante*: Il caricamento del documento crea un modello di oggetti mutabile. Senza questo passaggio non è possibile accedere alle risorse della pagina necessarie per la manipolazione del dizionario.

## Passo 2: Recuperare le risorse della prima pagina

Ogni pagina memorizza un dizionario `Resources` che contiene font, immagini e stati grafici. Accedervi ti fornisce un `DictionaryEditor` che semplifica le operazioni di lettura/scrittura.

```csharp
// Step 2: Get the resources of the first page
Page firstPage = pdfDocument.Pages[1];
DictionaryEditor resourcesEditor = new DictionaryEditor(firstPage.Resources);
```

*Perché è importante*: Il dizionario `ExtGState` vive all'interno delle risorse della pagina. Modificare il dizionario sbagliato non avrebbe alcun effetto sul rendering.

## Passo 3: Individuare il dizionario ExtGState esistente

L'entry `ExtGState` potrebbe già contenere oggetti di stato grafico. Lo recuperiamo come `CosPdfDictionary` così da poter aggiungere nuove voci.

```csharp
// Step 3: Access the existing ExtGState dictionary
CosPdfDictionary extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
```

Se l'entry `ExtGState` non esiste, Aspose.PDF crea automaticamente un dizionario vuoto quando ne assegnerai uno nuovo in seguito.

## Passo 4: **Creare un dizionario PDF vuoto** per un nuovo stato grafico

Qui costruiamo un nuovo `CosPdfDictionary`—il nucleo dell'operazione **creare un dizionario PDF vuoto**. Lo popoliamo poi con le chiavi standard dello stato grafico:

* `CA` – opacità del tratto.
* `ca` – opacità del riempimento.
* `BM` – blend mode.

```csharp
// Step 4: Create a new graphics state dictionary and define its entries
CosPdfDictionary graphicsStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

KeyValuePair<string, ICosPdfPrimitive>[] graphicsStateEntries = new[]
{
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),          // Stroke opacity
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),       // Fill opacity
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))    // Blend mode
};

foreach (var entry in graphicsStateEntries)
    graphicsStateDict.Add(entry);
```

*Perché è importante*: Definendo esplicitamente ogni voce, controlli come gli oggetti sulla pagina si fondono e vengono renderizzati. Il dizionario è **vuoto** finché non aggiungi queste chiavi, soddisfacendo così il requisito di **creare un dizionario PDF vuoto** prima di popolarlo.

## Passo 5: Aggiungere il nuovo stato grafico al dizionario ExtGState

Ogni stato grafico deve avere un nome univoco (ad es., `GS0`). Inseriamo il dizionario appena creato sotto quel nome.

```csharp
// Step 5: Add the new graphics state to the ExtGState dictionary with a unique name
extGStateDict.Add("GS0", graphicsStateDict);
```

Se ti servono più stati, continua ad aggiungere voci come `GS1`, `GS2`, ecc., assicurandoti che ogni nome sia unico all'interno del dizionario `ExtGState`.

## Passo 6: Salvare il documento PDF aggiornato

Infine, scrivi le modifiche su disco. Il file originale rimane intatto perché salviamo in un nuovo percorso.

```csharp
// Step 6: Save the updated PDF document
pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
}
```

Il risultato `output.pdf` ora contiene uno stato grafico aggiuntivo (`GS0`) che puoi riferire da qualsiasi stream di contenuto della pagina usando l'operatore `/GS0`.

## Esempio completo funzionante

Unire tutti i passaggi produce un programma autonomo che puoi eseguire immediatamente.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;

class Program
{
    static void Main()
    {
        // Load the source PDF
        using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
        {
            // Access first page resources
            Page firstPage = pdfDocument.Pages[1];
            DictionaryEditor resourcesEditor = new DictionaryEditor(firstPage.Resources);

            // Get (or create) ExtGState dictionary
            CosPdfDictionary extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();

            // Build a new empty PDF dictionary for graphics state
            CosPdfDictionary graphicsStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            var entries = new[]
            {
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
            };
            foreach (var entry in entries)
                graphicsStateDict.Add(entry);

            // Insert the new graphics state with a unique name
            extGStateDict.Add("GS0", graphicsStateDict);

            // Save the modified document
            pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
        }

        Console.WriteLine("PDF updated successfully.");
    }
}
```

**Output previsto**: Dopo aver eseguito il programma, `output.pdf` contiene lo stesso contenuto visivo di `input.pdf`. Analizzando il PDF con uno strumento come Adobe Acrobat o PDF‑Tron vedrai una nuova voce `GS0` sotto il dizionario `ExtGState` della prima pagina.

## Variazioni comuni e casi limite

| Situazione | Cosa modificare |
|-----------|----------------|
| **Nessuna voce ExtGState esistente** | Sostituisci `resourcesEditor["ExtGState"]` con `new CosPdfDictionary(pdfDocument)` e assegnalo nuovamente a `firstPage.Resources["ExtGState"]`. |
| **Più pagine necessitano dello stesso stato** | Aggiungi la stessa voce `GS0` al `ExtGState` di ogni pagina, oppure riferisci il dizionario da un oggetto risorsa condiviso. |
| **Blend mode diverso** | Cambia il valore `CosPdfName` da `"Normal"` a `"Multiply"`, `"Screen"` ecc., a seconda dell'effetto desiderato. |
| **Valori di opacità più alti** | Usa `new CosPdfNumber(0.8)` per `ca` o `CA` per aumentare l'opacità di riempimento o di tratto. |
| **Utilizzo di un operatore di stream** | Nel content stream, scrivi `"/GS0 gs"` prima delle operazioni di disegno per applicare il nuovo stato grafico. |

## Considerazioni sulle prestazioni

* **Utilizzo della memoria** – Caricare un PDF molto grande consuma memoria proporzionalmente al numero di pagine. Se devi modificare solo la prima pagina, considera l'uso di `pdfDocument.Pages.Delete(pageNumber)` dopo la lavorazione per liberare risorse.
* **Sicurezza dei thread** – Gli oggetti Aspose.PDF non sono thread‑safe. Esegui le modifiche al dizionario su un singolo thread o crea istanze separate di `Document` per ogni thread.

## Conclusione

Ora sai come **creare un dizionario PDF vuoto** con Aspose.PDF, popolarlo con voci di stato grafico e collegarlo al dizionario `ExtGState` di una pagina. Questa tecnica consente un controllo fine su opacità, blend mode e altri parametri di rendering direttamente da C#.

Successivamente, esplora argomenti correlati come **PDF manipulation C#**, aggiungere voci personalizzate al **dizionario ExtGState** per effetti avanzati di trasparenza, o usare **CosPdfDictionary** per modificare altri tipi di risorse come font o XObject. Sperimenta con più stati grafici per creare effetti visivi sofisticati nei tuoi PDF.

## Cosa dovresti imparare dopo?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Create & Fill Rectangles in PDFs Using Aspose.PDF for .NET&#58; A Step-by-Step Guide](/pdf/english/net/images-graphics/create-fill-rectangle-aspose-pdf-net/)
- [How to Create Dashed Lines in PDFs Using Aspose.PDF for .NET&#58; A Step-by-Step Guide](/pdf/english/net/images-graphics/create-dashed-lines-aspose-pdf-net/)
- [How to Add an Empty Page at the End of a PDF Using Aspose.PDF for .NET | Step-by-Step Guide](/pdf/english/net/document-manipulation/add-empty-page-end-pdf-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}