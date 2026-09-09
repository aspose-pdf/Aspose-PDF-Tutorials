---
category: general
date: 2026-09-08
description: Aggiungi trasparenza ai PDF con Aspose.PDF per .NET – impara a impostare
  l'opacità del tratto e del riempimento, la modalità di fusione e a salvare il risultato
  in pochi minuti.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add transparency to pdf
- aspose.pdf transparency
- pdf graphics state
- extgstate dictionary
- pdf opacity settings
language: it
lastmod: 2026-09-08
og_description: Aggiungi trasparenza a PDF usando Aspose.PDF per .NET. Questo tutorial
  mostra come modificare il dizionario ExtGState, impostare l'opacità e la modalità
  di fusione e salvare il file aggiornato.
og_image_alt: Screenshot of a PDF page showing semi‑transparent shapes created with
  Aspose.PDF
og_title: Aggiungi trasparenza al PDF con Aspose.PDF – guida passo passo
schemas:
- author: Aspose
  dateModified: '2026-09-08'
  description: Add transparency to PDF with Aspose.PDF for .NET – learn to set stroke
    and fill opacity, blend mode, and save the result in minutes.
  headline: How to add transparency to PDF files using Aspose.PDF for .NET
  type: TechArticle
tags:
- PDF
- C#
- Aspose.PDF
title: Come aggiungere la trasparenza ai file PDF utilizzando Aspose.PDF per .NET
url: /it/net/images-graphics/how-to-add-transparency-to-pdf-files-using-aspose-pdf-for-ne/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come aggiungere trasparenza ai file PDF usando Aspose.PDF per .NET

Se hai bisogno di **aggiungere trasparenza ai PDF** documenti, questa guida ti mostra esattamente come modificare lo stato grafico con Aspose.PDF per .NET. Imparerai a impostare l'opacità del tratto, l'opacità di riempimento e la modalità di fusione su una singola pagina, quindi salvare il risultato come un nuovo file.

La trasparenza è una necessità comune per filigrane, grafiche sovrapposte o effetti visivi nei report. In questo tutorial vedrai il codice completo e eseguibile, comprenderai perché ogni chiamata API è importante e otterrai consigli per gestire casi limite come voci di risorse mancanti.

## Cosa ti serve

* .NET 6.0 o successivo (il codice funziona anche con .NET Framework 4.6+)
* Una licenza valida di Aspose.PDF per .NET (la versione di prova gratuita funziona per i test)
* Un PDF di input chiamato `input.pdf` posizionato in una cartella a cui puoi fare riferimento dal codice
* Un ambiente di sviluppo C# (Visual Studio, Rider o VS Code)

Nessun pacchetto NuGet aggiuntivo è necessario oltre a `Aspose.Pdf`.

## Panoramica dello stato grafico PDF

Lo stato grafico PDF è memorizzato in un **dizionario ExtGState** all'interno del dizionario delle risorse di una pagina. Ogni voce definisce parametri di rendering come larghezza della linea, opacità e modalità di fusione. Creando un nuovo oggetto di stato grafico e aggiungendolo al dizionario `ExtGState`, puoi riutilizzare le stesse impostazioni di trasparenza in più comandi di disegno.

Comprendere questa struttura ti aiuta a evitare errori comuni, come tentare di impostare l'opacità direttamente su un oggetto `Page` (cosa non supportata dall'API). Invece, lavori con oggetti COS a basso livello che corrispondono uno‑a‑uno alla specifica PDF.

## Passo 1: Caricare il documento PDF

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Operators;
using Aspose.Pdf.Cos;

// Load the source PDF
var pdfDoc = new Document("YOUR_DIRECTORY/input.pdf");
```

*Perché questo passo?*  
`Document` è il punto di ingresso per qualsiasi manipolazione PDF. Caricare il file crea una rappresentazione in memoria che puoi modificare senza toccare il file originale su disco.

## Passo 2: Ottenere la prima pagina e il suo editor del dizionario delle risorse

```csharp
// Retrieve the first page (pages are 1‑based)
var page = pdfDoc.Pages[1];

// The DictionaryEditor provides convenient access to the page’s resources
var resourceEditor = new DictionaryEditor(page.Resources);
```

*Perché questo passo?*  
Tutte le voci dello stato grafico vivono all'interno delle risorse della pagina. `DictionaryEditor` astrae la gestione del dizionario COS a basso livello, consentendoti di leggere o creare voci come `ExtGState`.

## Passo 3: Recuperare il dizionario ExtGState dalle risorse della pagina

```csharp
// The ExtGState entry may already exist; if not, create it
CosPdfDictionary extGStateDict;
if (resourceEditor.ContainsKey("ExtGState"))
{
    extGStateDict = (CosPdfDictionary)resourceEditor["ExtGState"].ToCosPdfDictionary();
}
else
{
    // Create a new ExtGState dictionary and attach it to the page resources
    extGStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDoc);
    resourceEditor.Add("ExtGState", extGStateDict);
}
```

*Perché questo passo?*  
Un PDF può omettere completamente il dizionario `ExtGState`. Il codice sopra gestisce in modo sicuro sia i casi esistenti che quelli mancanti, garantendo che il tutorial funzioni con qualsiasi PDF di input.

## Passo 4: Creare un nuovo dizionario di stato grafico e definire le sue voci

```csharp
// Create an empty dictionary that will hold our transparency settings
var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDoc);

// Define the entries:
//   CA – stroke opacity (0 = fully transparent, 1 = opaque)
//   ca – fill opacity
//   BM – blend mode (Normal, Multiply, etc.)
var graphicsStateEntries = new[]
{
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),   // Stroke opacity = 100%
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),   // Fill opacity = 50%
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // Standard blend mode
};

foreach (var entry in graphicsStateEntries)
    newGraphicsState.Add(entry);
```

*Perché questo passo?*  
`CA` e `ca` sono gli operatori PDF che controllano l'opacità per le operazioni di tracciatura e non‑tracciatura (riempimento). Impostare `BM` su `Normal` mantiene il comportamento di composizione predefinito, ma puoi sperimentare con `Multiply` o `Screen` per effetti artistici.

## Passo 5: Aggiungere il nuovo stato grafico al dizionario ExtGState

```csharp
// Choose a unique name for the graphics state (e.g., GS0)
extGStateDict.Add("GS0", newGraphicsState);
```

*Perché questo passo?*  
Il nome `GS0` diventa un riferimento che puoi usare più tardi nei flussi di contenuto (`/GS0 gs`). Aggiungerlo a `ExtGState` rende il PDF consapevole dei nuovi parametri di trasparenza.

## Passo 6: Applicare lo stato grafico in un flusso di contenuto (opzionale)

Se vuoi vedere l'effetto immediatamente, puoi anteporre un semplice comando di disegno che utilizza il nuovo stato:

```csharp
// Build a content stream that draws a semi‑transparent rectangle
var content = new PageContent();
content.Operators.Add(new Operator("q"));                     // Save graphics state
content.Operators.Add(new Operator("GS0", "gs"));            // Set our custom graphics state
content.Operators.Add(new Operator("0.2", "0.2", "0.8", "rg")); // Set fill color (light blue)
content.Operators.Add(new Operator("100", "500", "200", "100", "re")); // Rectangle
content.Operators.Add(new Operator("f"));                    // Fill
content.Operators.Add(new Operator("Q"));                     // Restore graphics state

// Insert the new content at the beginning of the page
page.Contents.Insert(0, content);
```

*Perché questo passo?*  
Il frammento opzionale dimostra come lo stato grafico aggiunto (`GS0`) venga effettivamente utilizzato. Il rettangolo apparirà con un'opacità di riempimento del 50 % mentre il suo contorno rimarrà completamente opaco.

## Passo 7: Salvare il documento PDF modificato

```csharp
pdfDoc.Save("YOUR_DIRECTORY/output.pdf");
```

Il file risultante, `output.pdf`, contiene la nuova voce `ExtGState` e, se hai aggiunto il contenuto opzionale, una sovrapposizione di rettangolo semi‑trasparente.

### Output previsto

Quando apri `output.pdf` in Adobe Acrobat Reader o in qualsiasi visualizzatore PDF, dovresti vedere:

* Il contenuto originale della pagina invariato.
* Se hai eseguito il codice di disegno opzionale, un rettangolo azzurro chiaro il cui riempimento è trasparente al 50 %, permettendo alla pagina sottostante di mostrarsi.

## Elenco completo del codice sorgente

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Cos;
using Aspose.Pdf.Operators;
using System.Collections.Generic;

class AddTransparencyExample
{
    static void Main()
    {
        // 1. Load the PDF
        var pdfDoc = new Document("YOUR_DIRECTORY/input.pdf");

        // 2. Get the first page and its resources
        var page = pdfDoc.Pages[1];
        var resourceEditor = new DictionaryEditor(page.Resources);

        // 3. Retrieve or create ExtGState dictionary
        CosPdfDictionary extGStateDict;
        if (resourceEditor.ContainsKey("ExtGState"))
            extGStateDict = (CosPdfDictionary)resourceEditor["ExtGState"].ToCosPdfDictionary();
        else
        {
            extGStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDoc);
            resourceEditor.Add("ExtGState", extGStateDict);
        }

        // 4. Create new graphics state with transparency settings
        var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDoc);
        var graphicsStateEntries = new[]
        {
            new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),   // Stroke opacity
            new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),   // Fill opacity
            new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // Blend mode
        };
        foreach (var entry in graphicsStateEntries)
            newGraphicsState.Add(entry);

        // 5. Add the graphics state to ExtGState with a unique name
        extGStateDict.Add("GS0", newGraphicsState);

        // 6. (Optional) Draw a rectangle using the new state
        var content = new PageContent();
        content.Operators.Add(new Operator("q"));
        content.Operators.Add(new Operator("GS0", "gs"));
        content.Operators.Add(new Operator("0.2", "0.2", "0.8", "rg"));
        content.Operators.Add(new Operator("100", "500", "200", "100", "re"));
        content.Operators.Add(new Operator("f"));
        content.Operators.Add(new Operator("Q"));
        page.Contents.Insert(0, content);

        // 7. Save the updated PDF
        pdfDoc.Save("YOUR_DIRECTORY/output.pdf");
    }
}
```

Copia il codice in un'applicazione console, sostituisci `YOUR_DIRECTORY` con il percorso reale della cartella e avvialo. Il programma produrrà `output.pdf` con le impostazioni di trasparenza aggiunte.

## Problemi comuni e come evitarli

| Sintomo | Causa | Soluzione |
|---------|-------|-----|
| `KeyNotFoundException` on `"ExtGState"` | La pagina non ha una voce `ExtGState`. | Il tutorial crea già il dizionario quando manca; assicurati di usare il blocco condizionale fornito. |
| Trasparenza non visibile nel visualizzatore | I comandi di disegno non fanno mai riferimento a `GS0`. | Aggiungi l'operatore `gs` (`"GS0 gs"`) prima di qualsiasi operazione di tracciatura/riempimento, come mostrato nello snippet opzionale. |
| Il PDF diventa corrotto dopo il salvataggio | Mescolare API di alto livello `Page` con oggetti COS a basso livello in modo errato. | Attieniti al modello di recuperare `CosPdfDictionary` tramite `DictionaryEditor` ed evita di modificare lo stesso dizionario due volte. |
| La modalità di fusione non ha effetto | Il visualizzatore non supporta la modalità di fusione selezionata. | Usa `Normal` per una compatibilità ampia; sperimenta con `Multiply` solo in visualizzatori che segnalano supporto. |

## Prossimi passi

Ora che sai come **aggiungere trasparenza ai PDF**, puoi:

* Applicare lo stesso stato grafico a più pagine iterando su `pdfDoc.Pages`.
* Combinare la trasparenza con percorsi di ritaglio per filigrane sofisticate.
* Esplorare altre voci ExtGState come `SM` (regolazione del tratto) o `CA

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Come aggiungere e allineare timbri di testo nei PDF usando Aspose.PDF per .NET | Filigrane e sfondi](/pdf/english/net/watermarks-backgrounds/add-text-stamp-aspose-pdf-dotnet/)
- [Come aggiungere una filigrana immagine rotante ai PDF usando Aspose.PDF per .NET](/pdf/english/net/watermarks-backgrounds/add-rotating-image-watermark-aspose-pdf/)
- [Come aggiungere timbri di pagina nei PDF usando Aspose.PDF per .NET: Guida completa](/pdf/english/net/watermarks-backgrounds/add-page-stamp-aspose-pdf-dotnet-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}