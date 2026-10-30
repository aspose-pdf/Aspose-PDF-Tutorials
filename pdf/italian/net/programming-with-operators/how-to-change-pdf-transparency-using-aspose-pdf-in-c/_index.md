---
category: general
date: 2026-10-04
description: Scopri come modificare la trasparenza dei PDF con Aspose.Pdf in C#. Questa
  guida passo‑passo aggiunge uno stato grafico personalizzato per regolare l'opacità
  e la modalità di fusione.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- change PDF transparency
- Aspose.Pdf graphics state
- PDF opacity C#
- ExtGState dictionary
- blend mode PDF
language: it
lastmod: 2026-10-04
og_description: Modifica la trasparenza dei PDF in C# usando Aspose.Pdf. Segui questo
  breve tutorial per modificare l'opacità, la modalità di fusione e lo stato grafico
  nei tuoi PDF.
og_image_alt: Screenshot of a PDF page before and after changing transparency with
  Aspose.Pdf
og_title: Modifica la trasparenza dei PDF con Aspose.Pdf – guida completa in C#
schemas:
- author: Aspose
  dateModified: '2026-10-04'
  description: Learn how to change PDF transparency with Aspose.Pdf in C#. This step‑by‑step
    guide adds a custom graphics state to adjust opacity and blend mode.
  headline: How to change PDF transparency using Aspose.Pdf in C#
  type: TechArticle
tags:
- Aspose.Pdf
- C#
- PDF manipulation
- graphics state
title: Come modificare la trasparenza di un PDF usando Aspose.Pdf in C#
url: /it/net/programming-with-operators/how-to-change-pdf-transparency-using-aspose-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come modificare la trasparenza di un PDF usando Aspose.Pdf in C#

Se devi **modificare la trasparenza di un PDF** in un progetto .NET, questa guida ti mostra esattamente come farlo con Aspose.Pdf. Alla fine del tutorial avrai un PDF in cui gli oggetti selezionati usano un’opacità e una modalità di fusione personalizzate, senza necessità di strumenti esterni.

Lavorare con l’opacità dei PDF è una esigenza comune per filigrane, grafiche sovrapposte o effetti visivi sottili. I passaggi seguenti coprono tutto ciò di cui hai bisogno—dal caricamento del documento alla modifica del **dizionario ExtGState**, alla creazione di un nuovo stato grafico e al salvataggio del risultato.

## Prerequisiti

Prima di iniziare, assicurati di avere:

* **Aspose.Pdf for .NET** (versione 23.12 o successiva). Puoi installarlo tramite NuGet:

```bash
dotnet add package Aspose.Pdf
```

* Un ambiente di sviluppo .NET (Visual Studio, VS Code o la CLI `dotnet`).
* Un file PDF di input situato in una directory nota (l’esempio utilizza `input.pdf`).

Non sono richieste librerie aggiuntive.

## Passo 1: Caricare il documento PDF

La prima operazione è aprire il PDF esistente. L’uso di un blocco `using` garantisce che il handle del file venga rilasciato automaticamente.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Cos;
using Aspose.Pdf.Tools;

// ...

using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
{
    // Subsequent steps go here
}
```

*Perché è importante*: Caricare il documento crea una rappresentazione in memoria che puoi modificare. La classe `Document` ti dà anche accesso agli oggetti COS a basso livello, essenziali per cambiare la trasparenza del PDF.

## Passo 2: Accedere alle risorse della prima pagina

Gli stati grafici sono memorizzati nel dizionario delle risorse di una pagina. Recuperiamo la prima pagina e avvolgiamo le sue risorse con `DictionaryEditor` così da poterle modificare comodamente.

```csharp
var firstPage = pdfDocument.Pages[1];
var resourcesEditor = new DictionaryEditor(firstPage.Resources);
```

*Spiegazione*: `DictionaryEditor` astrae la gestione del dizionario COS, permettendoti di leggere e scrivere voci come `ExtGState` senza dover trattare la sintassi PDF grezza.

## Passo 3: Ottenere (o creare) il dizionario ExtGState

Il **dizionario ExtGState** contiene gli oggetti di stato grafico nominati. Se esiste già lo riutilizziamo; altrimenti ne creiamo uno nuovo.

```csharp
CosPdfDictionary extGStateDict;

// Try to fetch an existing ExtGState entry
if (resourcesEditor.ContainsKey("ExtGState"))
{
    extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
}
else
{
    // Create a fresh ExtGState dictionary and add it to the resources
    extGStateDict = new CosPdfDictionary(pdfDocument);
    resourcesEditor["ExtGState"] = extGStateDict;
}
```

*Perché questo passaggio*: Senza una voce `ExtGState` il motore PDF non ha dove cercare le impostazioni di opacità personalizzate. Aggiungere il dizionario rende la pagina consapevole di eventuali nuovi stati grafici che definisci.

## Passo 4: Definire un nuovo stato grafico con opacità e modalità di fusione

Uno stato grafico è una raccolta di parametri di rendering PDF. Qui impostiamo:

* **CA** – opacità del tratto (1 = completamente opaco)
* **ca** – opacità del riempimento (0.5 = 50 % trasparente)
* **BM** – modalità di fusione (`Normal` è il valore predefinito, ma puoi sperimentare con `Multiply`, `Screen`, ecc.)

```csharp
// Create an empty dictionary that will become the new graphics state
var graphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

// Prepare the entries
var graphicsStateEntries = new KeyValuePair<string, ICosPdfPrimitive>[]
{
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),   // stroke opacity
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // fill opacity
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // blend mode
};

// Populate the dictionary
foreach (var entry in graphicsStateEntries)
{
    graphicsState.Add(entry);
}
```

*Approfondimento*: I valori `CosPdfNumber` sono numeri a virgola mobile compresi tra 0 e 1. Modificarli ti permette di regolare finemente come appaiono i tratti e i riempimenti trasparenti. La modalità di fusione determina come il contenuto trasparente interagisce con la grafica sottostante.

## Passo 5: Registrare lo stato grafico in ExtGState

Assegniamo al nuovo stato un nome (`GS0`). Successivamente, quando disegnerai oggetti, farai riferimento a questo nome nello stream di contenuto.

```csharp
extGStateDict.Add("GS0", graphicsState); // "GS0" becomes the identifier you’ll use later
```

*Best practice*: Usa una convenzione di denominazione chiara (`GS0`, `GS_Watermark`, ecc.) così da gestire più stati senza confusione.

## Passo 6: Applicare lo stato grafico al contenuto della pagina (opzionale)

Se vuoi applicare la nuova opacità agli elementi esistenti della pagina, devi modificare lo stream di contenuto della pagina. Di seguito trovi un esempio semplice che aggiunge un rettangolo semitrasparente sopra la pagina.

```csharp
// Build a content stream that sets the graphics state and draws a rectangle
var contentBuilder = new Aspose.Pdf.Operators.ContentBuilder(pdfDocument);
contentBuilder.SetGraphicsState("GS0");
contentBuilder.SetFillColor(Color.FromRgb(255, 0, 0)); // red fill
contentBuilder.Rectangle(100, 500, 200, 100); // x, y, width, height
contentBuilder.FillPath();

firstPage.Contents.Add(contentBuilder);
```

*Perché funziona*: L’operatore `SetGraphicsState` indica all’interprete PDF di usare i parametri definiti in `GS0` per tutti i comandi di disegno successivi. Il rettangolo appare quindi con un’opacità di riempimento del 50 % mantenendo il tratto completamente opaco.

## Passo 7: Salvare il PDF modificato

Infine, scrivi le modifiche su disco.

```csharp
pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
```

Il `output.pdf` risultante contiene il nuovo stato grafico, e qualsiasi contenuto che faccia riferimento a `GS0` verrà renderizzato con la trasparenza definita.

---

![Diagram showing PDF transparency change](/images/pdf-transparency-before-after.png "PDF page before and after applying custom graphics state")
*Testo alternativo dell’immagine (per SEO e accessibilità):* **esempio di modifica della trasparenza PDF – pagina originale vs. pagina modificata**

## Esempio completo funzionante

Mettendo tutto insieme, ecco un singolo programma eseguibile che modifica la trasparenza di un PDF e aggiunge un rettangolo semitrasparente.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Cos;
using Aspose.Pdf.Tools;
using System.Collections.Generic;
using Aspose.Pdf.Operators;
using Aspose.Pdf.Drawing;

class ChangePdfTransparency
{
    static void Main()
    {
        // Load the source PDF
        using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
        {
            // Access first page resources
            var firstPage = pdfDocument.Pages[1];
            var resourcesEditor = new DictionaryEditor(firstPage.Resources);

            // Ensure ExtGState dictionary exists
            CosPdfDictionary extGStateDict;
            if (resourcesEditor.ContainsKey("ExtGState"))
                extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
            else
            {
                extGStateDict = new CosPdfDictionary(pdfDocument);
                resourcesEditor["ExtGState"] = extGStateDict;
            }

            // Create a new graphics state (opacity + blend mode)
            var graphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            var entries = new[]
            {
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
            };
            foreach (var e in entries) graphicsState.Add(e);

            // Register the graphics state as GS0
            extGStateDict.Add("GS0", graphicsState);

            // OPTIONAL: draw a semi‑transparent rectangle using GS0
            var builder = new ContentBuilder(pdfDocument);
            builder.SetGraphicsState("GS0");
            builder.SetFillColor(Color.FromRgb(255, 0, 0)); // red
            builder.Rectangle(100, 500, 200, 100);
            builder.FillPath();
            firstPage.Contents.Add(builder);

            // Save the result
            pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
        }

        Console.WriteLine("PDF transparency changed and saved to output.pdf");
    }
}
```

### Output previsto

* Il file `output.pdf` viene creato nella cartella specificata.
* Aprendo il PDF, vedrai un rettangolo rosso il cui riempimento è trasparente al 50 % mentre il bordo rimane completamente opaco.
* Qualsiasi altro oggetto che faccia riferimento a `GS0` (ad es. filigrane) erediterà la stessa opacità e modalità di fusione.

## Domande frequenti e gestione dei casi limite

| Domanda | Risposta |
|----------|----------|
| **Posso modificare solo l’opacità del tratto?** | Imposta `CA` al valore desiderato e lascia `ca` a `1`. |
| **Quali modalità di fusione sono supportate?** | Tutte le modalità di fusione PDF standard (`Normal`, `Multiply`, `Screen`, `Overlay`, ecc.) sono accettate tramite la voce `BM`. |
| **Devo pulire il dizionario dopo l’uso?** | No. Gli oggetti `CosPdfDictionary` sono gestiti da Aspose.Pdf e vengono scritti nel file quando chiami `Save`. |
| **Come funziona con PDF criptati?** | Carica il documento con la password corretta (`new Document(path, password)`). La manipolazione dello stato grafico funziona allo stesso modo una volta che il documento è decrittato in memoria. |
| **È possibile applicare lo stesso stato grafico a più pagine?** | Sì. Aggiungi la voce `GS0` al dizionario `ExtGState` di ciascuna pagina, oppure crea un unico dizionario condiviso nelle risorse globali del documento e riferiscilo da ogni pagina. |

## Consigli e best practice

* **Pro tip:** Mantieni i nomi degli stati grafici brevi ma descrittivi (`GS_Watermark`, `GS_Overlay`). Questo evita collisioni di nomi e semplifica il debug.
* **Attenzione a:** Sovrascrivere accidentalmente una voce `ExtGState` esistente. Controlla sempre `resourcesEditor.ContainsKey("ExtGState")` prima di creare un nuovo dizionario.
* **Nota sulle prestazioni:** Modificare oggetti COS a basso livello è veloce, ma se devi elaborare migliaia di pagine considera di batchare le modifiche per ridurre la pressione sulla memoria.

## Prossimi passi

Ora che sai **come modificare la trasparenza di un PDF**, puoi approfondire argomenti correlati come:

* Aggiungere **filigrane** con opacità personalizzata (`PDF opacity C#`).
* Usare **modalità di fusione diverse** per ottenere effetti artistici (`blend mode PDF`).
* Creare librerie riutilizzabili di **stati grafici** per la generazione di documenti su larga scala (`Aspose.Pdf graphics state`).

Sperimenta variando i valori `ca` e `CA`, oppure sostituisci il rettangolo rosso con un’immagine o un overlay di testo. Gli stessi principi si applicano—basta fare riferimento allo stato grafico `GS0` prima di disegnare il nuovo contenuto.

---

*Hai imparato come modificare la trasparenza di un PDF usando Aspose.Pdf in C#. Applica queste tecniche per migliorare report, fatture o qualsiasi output PDF dove i dettagli visivi contano.*

## Cosa dovresti imparare dopo?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità aggiuntive dell’API ed esplorare approcci alternativi nei tuoi progetti.

- [Change PDF Opacity with Aspose.PDF – Complete C# Guide](/pdf/english/net/programming-with-stamps-and-watermarks/change-pdf-opacity-with-aspose-pdf-complete-c-guide/)
- [Change PDF Opacity in C# – Complete Aspose Guide](/pdf/english/net/programming-with-stamps-and-watermarks/change-pdf-opacity-in-c-complete-aspose-guide/)
- [Add Transparency to PDF using Aspose – Complete C# Guide](/pdf/english/net/programming-with-operators/add-transparency-to-pdf-using-aspose-complete-c-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}