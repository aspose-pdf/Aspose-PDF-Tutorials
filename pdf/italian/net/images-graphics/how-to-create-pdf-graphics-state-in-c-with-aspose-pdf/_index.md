---
category: general
date: 2026-11-16
description: Scopri come creare lo stato grafico PDF in C# usando Aspose.Pdf. Questa
  guida copre l'opacità, la modalità di fusione e un esempio completo di codice.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create pdf graphics state
- Aspose.Pdf ExtGState
- PDF opacity
- C# PDF manipulation
- PDF blend mode
- Aspose.Pdf graphics state
language: it
lastmod: 2026-11-16
og_description: Crea lo stato grafico PDF in C# con Aspose.Pdf. Segui questo tutorial
  completo per impostare l'opacità e la modalità di fusione in modo programmatico.
og_image_alt: Illustration of how to create PDF graphics state with Aspose.Pdf in
  C#
og_title: Crea lo stato grafico PDF in C# – guida passo‑passo Aspose.Pdf
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Learn how to create PDF graphics state in C# using Aspose.Pdf. This
    guide covers opacity, blend mode, and full code example.
  headline: How to create PDF graphics state in C# with Aspose.Pdf
  type: TechArticle
tags:
- Aspose.Pdf
- C#
- PDF
title: Come creare lo stato grafico PDF in C# con Aspose.Pdf
url: /it/net/images-graphics/how-to-create-pdf-graphics-state-in-c-with-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come creare lo stato grafico PDF in C# con Aspose.Pdf

Se hai bisogno di **creare lo stato grafico PDF** in un progetto .NET, questo tutorial ti mostra esattamente come farlo con Aspose.Pdf. Che tu voglia controllare l'opacità, cambiare la modalità di fusione o riutilizzare uno stato grafico personalizzato tra le pagine, i passaggi seguenti ti offrono una soluzione completa, pronta all'uso.

In questa guida imparerai come accedere alle risorse della pagina, aggiungere una voce **ExtGState** e salvare le modifiche in un nuovo file. L'esempio funziona con Aspose.Pdf 23.12 (o versioni successive) e mira a .NET 6+, ma i concetti sono validi anche per versioni precedenti.

## Prerequisiti

* Visual Studio 2022 (o qualsiasi IDE C#) con .NET 6 SDK installato.  
* Una licenza Aspose.Pdf per .NET o una chiave di valutazione temporanea.  
* Un file PDF chiamato `input.pdf` posizionato in una cartella a cui puoi fare riferimento dal codice.  

Non sono necessari pacchetti NuGet aggiuntivi oltre a `Aspose.Pdf`.

## Cosa copre il tutorial

* Caricamento di un documento PDF esistente.  
* Navigazione al dizionario delle risorse della prima pagina.  
* Creazione di un nuovo dizionario di stato grafico che definisce l'opacità del tratto (`CA`), l'opacità di riempimento (`ca`) e la modalità di fusione (`BM`).  
* Aggiunta del nuovo stato grafico alla collezione **ExtGState** con un nome personalizzato (`GS0`).  
* Salvataggio del PDF aggiornato in modo che i successivi comandi di disegno possano fare riferimento al nuovo stato.

Al termine del tutorial sarai in grado di **creare oggetti di stato grafico PDF** programmaticamente e riutilizzarli in qualsiasi operazione di disegno.

## Passo 1: Configurare il progetto e importare i namespace

Creare una nuova applicazione console (o integrare il codice in un progetto esistente). Aggiungere il riferimento Aspose.Pdf e includere i namespace richiesti:

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Operators;
using Aspose.Pdf.Generator;
```

> **Consiglio professionale:** se stai usando la versione di valutazione gratuita, aggiungi `Aspose.Pdf.License license = new Aspose.Pdf.License(); license.SetLicense("Aspose.Pdf.lic");` prima di caricare il documento per evitare messaggi di filigrana.

## Passo 2: Caricare il documento PDF

Aprire il file è semplice. La classe `Document` rappresenta l'intero PDF e ti dà accesso alle sue pagine e risorse.

```csharp
// Step 2: Load the PDF document
string inputPath = @"YOUR_DIRECTORY\input.pdf";

using (var document = new Document(inputPath))
{
    // All subsequent steps run inside this using block
```

Inserire il codice all'interno di un blocco `using` garantisce che il handle del file venga rilasciato dopo l'operazione, il che è essenziale per la **manipolazione PDF in C#** nei servizi di produzione.

## Passo 3: Recuperare il dizionario delle risorse della prima pagina

Ogni pagina PDF ha un dizionario *Resources* che memorizza font, immagini e stati grafici. Abbiamo bisogno di un `DictionaryEditor` per modificare quella struttura.

```csharp
    // Step 3: Get the first page and its resources dictionary
    var page = document.Pages[1];
    var resourcesEditor = new DictionaryEditor(page.Resources);
```

Se il PDF contiene già una voce `ExtGState`, `resourcesEditor["ExtGState"]` la restituirà; altrimenti, Aspose.Pdf crea un dizionario vuoto per noi quando aggiungiamo la prima voce.

## Passo 4: Accedere o creare il dizionario ExtGState

Il dizionario **ExtGState** contiene oggetti di stato grafico nominati. Recuperiamo uno esistente o creiamo un nuovo contenitore.

```csharp
    // Step 4: Access (or create) the ExtGState dictionary within the resources
    var extGState = resourcesEditor["ExtGState"].ToCosPdfDictionary();
```

Quando `ExtGState` non esiste, `resourcesEditor["ExtGState"]` restituisce automaticamente un nuovo dizionario vuoto, garantendo che il codice funzioni per qualsiasi PDF.

## Passo 5: Costruire il nuovo dizionario di stato grafico

Uno stato grafico è un `CosPdfDictionary` con chiavi specifiche:

* `CA` – opacità del tratto (0‑1)  
* `ca` – opacità di riempimento (0‑1)  
* `BM` – modalità di fusione (`Normal`, `Multiply`, ecc.)

Creiamo un dizionario vuoto, lo popoliamo e poi lo aggiungiamo a `ExtGState`.

```csharp
    // Step 5: Create a new graphics state dictionary with desired parameters
    var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(document);
    var parameters = new[]
    {
        new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),   // Stroke opacity (fully opaque)
        new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // Fill opacity (50% transparent)
        new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // Blend mode
    };

    foreach (var p in parameters)
        newGraphicsState.Add(p);
```

Puoi cambiare `0.5` con qualsiasi valore compreso tra `0` e `1` per regolare l'opacità di riempimento, oppure sostituire `"Normal"` con `"Multiply"` per una diversa **modalità di fusione PDF**. Questa flessibilità è il motivo per cui creare uno stato grafico personalizzato è una tecnica potente nella gestione dello **stato grafico Aspose.Pdf**.

## Passo 6: Registrare lo stato grafico con un nome

I flussi di contenuto PDF fanno riferimento agli stati grafici per nome. Qui usiamo `GS0`, ma qualsiasi nome univoco funziona.

```csharp
    // Step 6: Add the new graphics state to the ExtGState dictionary with a name (e.g., GS0)
    extGState.Add("GS0", newGraphicsState);
```

Se ti servono più stati, ripeti il passaggio di creazione con parametri diversi e aggiungili come `GS1`, `GS2`, ecc. Questo schema scala bene per documenti complessi che richiedono opacità o impostazioni di fusione diverse su livelli differenti.

## Passo 7: Salvare il PDF modificato

Infine, scrivi il documento aggiornato in un nuovo file. Mantenere intatto l'originale semplifica il debug.

```csharp
    // Step 7: Save the updated PDF document
    string outputPath = @"YOUR_DIRECTORY\output.pdf";
    document.Save(outputPath);
}
```

Dopo l'esecuzione, `output.pdf` contiene una voce `ExtGState` denominata `GS0`. Qualsiasi operatore di disegno successivo può fare riferimento ad essa usando l'operatore `gs` (ad esempio, `GS0 gs` in un flusso di contenuto).  

> **Perché è importante:** Creando uno stato grafico riutilizzabile eviti di ripetere le impostazioni di opacità e fusione per ogni comando di disegno, migliorando sia le prestazioni sia la manutenibilità.

## Utilizzare il nuovo stato grafico in un flusso di contenuto (opzionale)

Se vuoi vedere l'effetto immediatamente, puoi aggiungere un semplice rettangolo che utilizza lo stato appena creato:

```csharp
using (var document = new Document(outputPath))
{
    var page = document.Pages[1];
    var content = page.Contents[1]; // Get the first content stream

    // Insert graphics state selection and a semi‑transparent rectangle
    var operators = new List<Operator>
    {
        new Operator("GS0", "gs"),                     // Select our custom graphics state
        new Operator("0.5", "w"),                      // Set line width (optional)
        new Operator("100", "100", "200", "150", "re"), // Rectangle (x, y, width, height)
        new Operator("B")                              // Stroke the rectangle
    };

    foreach (var op in operators)
        content.Operators.Add(op);

    document.Save(@"YOUR_DIRECTORY\final_output.pdf");
}
```

## Problemi comuni e come evitarli

| Problema | Perché accade | Soluzione |
|----------|---------------|-----------|
| `ExtGState` entry not found | Alcuni PDF omettono completamente il dizionario. | Il `DictionaryEditor` lo crea automaticamente quando aggiungi la prima voce, quindi non è necessario alcun controllo aggiuntivo. |
| Opacity values > 1 or < 0 | La specifica PDF limita l'opacità all'intervallo `[0,1]`. | Limita i valori prima di creare `CosPdfNumber`. |
| Blend mode typo | I nomi delle modalità di fusione PDF sono sensibili al maiuscolo/minuscolo. | Usa nomi esatti come `"Normal"`, `"Multiply"`, `"Screen"`. |
| License watermark | La versione di valutazione aggiunge una filigrana sulla prima pagina. | Applica un file di licenza valido prima di aprire il documento. |

Affrontare questi casi limite garantisce che la tua implementazione di **creazione dello stato grafico PDF** funzioni in modo affidabile su diverse fonti PDF.

## Esempio completo, eseguibile

Di seguito trovi un programma autonomo che puoi copiare, incollare ed eseguire. Sostituisci `YOUR_DIRECTORY` con un percorso di cartella reale sul tuo computer.

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Generator;

class Program
{
    static void Main()
    {
        // Optional: apply license to remove evaluation watermark
        // var license = new Aspose.Pdf.License();
        // license.SetLicense("Aspose.Pdf.lic");

        string inputPath = @"YOUR_DIRECTORY\input.pdf";
        string outputPath = @"YOUR_DIRECTORY\output.pdf";

        using (var document = new Document(inputPath))
        {
            // 1️⃣ Get first page and its resources
            var page = document.Pages[1];
            var resourcesEditor = new DictionaryEditor(page.Resources);

            // 2️⃣ Access (or create) ExtGState dictionary
            var extGState = resourcesEditor["ExtGState"].ToCosPdfDictionary();

            // 3️⃣ Build new graphics state
            var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(document);
            var parameters = new[]
            {
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),   // Stroke opacity
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // Fill opacity
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // Blend mode
            };
            foreach (var p in parameters) newGraphicsState.Add(p);

            // 4️⃣ Register the state with a name (GS0)
            extGState.Add("


## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Create custom graphics state in PDF using Aspose.Pdf](/pdf/english/net/programming-with-operators/create-custom-graphics-state-in-pdf-using-aspose-pdf/)
- [Add graphics state to PDF using Aspose.PDF for .NET (C#)](/pdf/english/net/programming-with-operators/how-to-add-graphics-state-pdf-using-aspose-pdf-in-c/)
- [How to create empty graphics state in a PDF with C#](/pdf/english/net/programming-with-operators/how-to-create-empty-graphics-state-in-a-pdf-with-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}