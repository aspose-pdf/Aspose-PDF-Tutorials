---
category: general
date: 2026-08-04
description: Aggiungi lo stato grafico PDF usando Aspose.Pdf per controllare l'opacità
  e la modalità di fusione. Segui questo tutorial completo per modificare le risorse
  PDF in modo sicuro.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add graphics state pdf
- Aspose.Pdf
- PDF opacity
- PDF blend mode
- ExtGState dictionary
language: it
lastmod: 2026-08-04
og_description: Aggiungi lo stato grafico PDF con Aspose.Pdf per impostare l'opacità
  e la modalità di fusione. Questa guida mostra il codice completo, spiega ogni passaggio
  e copre le insidie più comuni.
og_image_alt: Screenshot of a PDF page showing modified graphics state after using
  add graphics state pdf
og_title: Aggiungi lo stato grafico PDF con Aspose.Pdf – guida completa di programmazione
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Add graphics state pdf using Aspose.Pdf to control opacity and blend
    mode. Follow this complete tutorial for modifying PDF resources safely.
  headline: Add graphics state pdf with Aspose.Pdf – step‑by‑step guide
  type: TechArticle
- description: Add graphics state pdf using Aspose.Pdf to control opacity and blend
    mode. Follow this complete tutorial for modifying PDF resources safely.
  name: Add graphics state pdf with Aspose.Pdf – step‑by‑step guide
  steps:
  - name: Locate (or create) the `ExtGState` dictionary.
    text: Locate (or create) the `ExtGState` dictionary.
  - name: Build a new graphics‑state dictionary with the desired entries.
    text: Build a new graphics‑state dictionary with the desired entries.
  - name: Reference the new state from drawing commands (outside the scope of this
      tutorial).
    text: Reference the new state from drawing commands (outside the scope of this
      tutorial).
  type: HowTo
tags:
- PDF
- Aspose
- C#
- Graphics state
title: Aggiungi lo stato grafico PDF con Aspose.Pdf – guida passo passo
url: /it/net/images-graphics/add-graphics-state-pdf-with-aspose-pdf-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aggiungere lo stato grafico pdf con Aspose.Pdf – guida passo‑passo

Se hai bisogno di **add graphics state pdf** per controllare l'opacità o la modalità di fusione, questo tutorial ti mostra una soluzione completa, pronta per la produzione. Imparerai come modificare il dizionario ExtGState di una pagina PDF usando Aspose.Pdf, e vedrai il codice esatto che puoi copiare nel tuo progetto.

La guida copre tutto, dalla configurazione del progetto alla gestione dei casi limite come voci ExtGState mancanti. Alla fine avrai un PDF la cui prima pagina viene renderizzata con lo stato grafico che hai definito.

## Prerequisiti

* .NET 6.0 SDK o versioni successive installate.  
* Una versione recente del pacchetto NuGet **Aspose.Pdf** (ad es., 23.12 o più recente).  
* Un file PDF di input situato in una cartella a cui puoi fare riferimento dal codice.  
* Un ambiente di sviluppo come Visual Studio 2022 o VS Code.

## Panoramica del flusso di lavoro dello stato grafico

Lo stato grafico PDF controlla come vengono renderizzate le operazioni di disegno. Due proprietà sono le più comuni per gli effetti visivi:

* **Opacity** – le voci `ca` (riempimento) e `CA` (tratto).  
* **Blend mode** – la voce `BM`.

Questi valori vivono in un **ExtGState dictionary** collegato al dizionario delle risorse di una pagina. Aggiungere un nuovo stato grafico consiste in tre azioni:

1. Individuare (o creare) il dizionario `ExtGState`.  
2. Costruire un nuovo dizionario di stato grafico con le voci desiderate.  
3. Riferire il nuovo stato dai comandi di disegno (fuori dal campo di questo tutorial).

## Passo 1: Crea un nuovo progetto console .NET

```bash
dotnet new console -n PdfGraphicsStateDemo
cd PdfGraphicsStateDemo
dotnet add package Aspose.Pdf
```

Il comando `dotnet add package` scarica la libreria **Aspose.Pdf**, che fornisce l'API usata in tutta la guida.

## Passo 2: Carica il PDF e accedi alla prima pagina

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.IO;

// Load the source PDF
using var pdfDoc = new Document("YOUR_DIRECTORY/input.pdf");

// PDF pages are 1‑based; page 1 is the first page
Page firstPage = pdfDoc.Pages[1];
```

*Perché è importante*: Il modello a oggetti PDF utilizza l'indicizzazione a partire da 1, quindi richiedere `Pages[0]` genererebbe un'eccezione. Caricare il documento all'interno di un blocco `using` garantisce che il handle del file venga rilasciato automaticamente.

## Passo 3: Assicurati che il dizionario ExtGState esista

```csharp
// The page’s Resources dictionary holds many sub‑dictionaries (Font, XObject, etc.)
DictionaryEditor resourcesEditor = new DictionaryEditor(firstPage.Resources);

// Try to get the existing ExtGState dictionary; create one if it is missing
CosCosPdfDictionary extGStateDict;
if (resourcesEditor.ContainsKey("ExtGState"))
{
    extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
}
else
{
    // Create an empty ExtGState dictionary and attach it to the page resources
    extGStateDict = CosCosPdfDictionary.CreateEmptyDictionary(pdfDoc);
    resourcesEditor["ExtGState"] = extGStateDict;
}
```

**Suggerimento**: Verifica sempre la presenza di `ExtGState`. Alcuni PDF vengono generati senza di esso, e tentare di modificare una voce inesistente genererebbe una `KeyNotFoundException`.

## Passo 4: Costruisci il nuovo stato grafico

```csharp
// Create a fresh dictionary for the new graphics state
CosCosPdfDictionary newGraphicsState = CosCosPdfDictionary.CreateEmptyDictionary(pdfDoc);

// Stroke opacity (CA) – 1.0 means fully opaque
newGraphicsState.Add("CA", new CosPdfNumber(1));

// Fill opacity (ca) – 0.5 makes the fill 50 % transparent
newGraphicsState.Add("ca", new CosPdfNumber(0.5));

// Blend mode (BM) – "Normal" is the default compositing operation
newGraphicsState.Add("BM", new CosPdfName("Normal"));
```

*Perché queste voci*:  
- `CA` influisce su linee e bordi (tratto).  
- `ca` influisce su forme riempite e testo.  
- `BM` determina come il colore sorgente si fonde con quello di destinazione; `"Normal"` preserva l'aspetto originale rispettando l'opacità.

## Passo 5: Inserisci lo stato grafico nel dizionario ExtGState

```csharp
// Choose a unique name for the graphics state; "GS0" is common for the first entry
extGStateDict.Add("GS0", newGraphicsState);
```

Se ti servono più stati, incrementa il suffisso (`GS1`, `GS2`, …) e fai riferimento al nome corretto più tardi nei tuoi content stream.

## Passo 6: Salva il PDF modificato

```csharp
pdfDoc.Save("YOUR_DIRECTORY/output.pdf");
Console.WriteLine("PDF saved with new graphics state.");
```

Il file risultante (`output.pdf`) contiene lo stesso contenuto visivo dell'originale, ma qualsiasi comando di disegno che in seguito faccia riferimento a `/GS0` verrà renderizzato con **PDF opacity** 0.5 e la **PDF blend mode** `Normal`.

## Esempio completo eseguibile

Copia il programma seguente in `Program.cs` del progetto creato al Passo 1. Regola i segnaposto `YOUR_DIRECTORY` per adattarli al tuo ambiente.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.IO;

namespace PdfGraphicsStateDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the PDF document
            using var pdfDoc = new Document("YOUR_DIRECTORY/input.pdf");

            // 2️⃣ Access the first page's resources
            Page firstPage = pdfDoc.Pages[1];
            var resourcesEditor = new DictionaryEditor(firstPage.Resources);

            // 3️⃣ Retrieve or create ExtGState dictionary
            CosCosPdfDictionary extGStateDict;
            if (resourcesEditor.ContainsKey("ExtGState"))
            {
                extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
            }
            else
            {
                extGStateDict = CosCosPdfDictionary.CreateEmptyDictionary(pdfDoc);
                resourcesEditor["ExtGState"] = extGStateDict;
            }

            // 4️⃣ Define a new graphics state (opacity & blend mode)
            var newGraphicsState = CosCosPdfDictionary.CreateEmptyDictionary(pdfDoc);
            newGraphicsState.Add("CA", new CosPdfNumber(1));           // stroke opacity
            newGraphicsState.Add("ca", new CosPdfNumber(0.5));         // fill opacity
            newGraphicsState.Add("BM", new CosPdfName("Normal"));     // blend mode

            // 5️⃣ Add the graphics state to the ExtGState dictionary
            extGStateDict.Add("GS0", newGraphicsState);

            // 6️⃣ Save the modified PDF
            pdfDoc.Save("YOUR_DIRECTORY/output.pdf");
            Console.WriteLine("PDF saved with new graphics state.");
        }
    }
}
```

### Risultato atteso

Apri `output.pdf` in qualsiasi visualizzatore. Se in seguito aggiungi comandi di disegno che fanno riferimento a `/GS0` (ad esempio, tramite un content stream o un'altra chiamata API di Aspose.Pdf), il riempimento apparirà al 50 % di opacità mentre i tratti rimarranno completamente opachi. La modalità di fusione rimane `"Normal"`, adatta alla maggior parte degli scenari di composizione.

## Gestione delle variazioni comuni

| Situazione | Cosa cambiare | Motivo |
|-----------|----------------|--------|
| **Multiple pages need the same state** | Loop over `pdfDoc.Pages` and repeat Steps 3‑5 for each page, or create a single ExtGState dictionary in the document’s global resources and reference it from every page. | Avoids duplicate dictionaries and keeps the file size small. |
| **Different opacity values per page** | Use distinct names (`GS0`, `GS1`, …) and adjust `ca`/`CA` accordingly before adding to each page’s ExtGState. | Gives fine‑grained control over rendering. |
| **ExtGState already contains a key named “GS0”** | Choose a different key name (`GS1`, `MyState`, …) and update any content streams that reference it. | Prevents accidental overwriting of existing graphics states. |
| **PDF generated without an ExtGState dictionary** | The code in Step 3 already creates one, so no extra work is required. | Guarantees the operation succeeds for any input PDF. |

## Suggerimenti e migliori pratiche

* **Validate the PDF after modification** – use `pdfDoc.Validate()` (available in newer Aspose.Pdf releases) to catch structural issues early.  
* **Keep the graphics‑state dictionary small** – only include entries you need; extra keys increase file size without benefit.  
* **When adding content streams that use the new state**, prepend `/GS0 gs` before drawing operators. For example: `contentStream.Append("/GS0 gs 100 100 m 200 200 l S");`  
* **Dispose of large PDFs promptly** – the `using` statement in the example ensures the file handle is released, which is essential in web‑service scenarios.

## Conclusione

Ora sai come **add graphics state pdf** usando Aspose.Pdf, manipolare **PDF opacity**, impostare una **PDF blend mode** e lavorare in sicurezza con il **ExtGState dictionary**. Il codice completo è pronto per essere inserito in qualsiasi progetto .NET, e i suggerimenti allegati ti aiutano a evitare le insidie più comuni.

Successivamente, esplora come applicare lo stato grafico appena creato a testo, immagini o forme vettoriali. Potresti anche investigare altre voci ExtGState come `SM` (stroke‑adjustment) o valori `CA` superiori a 1 per effetti specializzati. Buon hacking PDF!

## Cosa dovresti imparare dopo?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità aggiuntive dell'API e a esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Come aggiungere filigrane di pagina nei PDF usando Aspose.PDF per .NET: Guida completa](/pdf/english/net/watermarks-backgrounds/add-page-stamp-aspose-pdf-dotnet-guide/)
- [Aggiungere filigrane immagine ai PDF usando Aspose.PDF per .NET: Guida passo‑passo](/pdf/english/net/images-graphics/add-image-stamp-to-pdf-aspose-dotnet/)
- [Come rimuovere grafiche dai PDF usando Aspose.PDF .NET: Guida completa](/pdf/english/net/images-graphics/remove-graphics-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}