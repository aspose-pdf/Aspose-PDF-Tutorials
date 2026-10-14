---
category: general
date: 2026-10-13
description: Scopri come impostare la trasparenza in un PDF con Aspose.Pdf per C#.
  Vedi anche come salvare il PDF modificato e cambiare l'alpha di riempimento.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to set transparency
- save modified pdf
- change fill alpha
- set fill opacity
- edit pdf resources
language: it
lastmod: 2026-10-13
og_description: Come impostare la trasparenza in un PDF con Aspose.Pdf per C#. Segui
  questa guida per modificare le risorse PDF, cambiare l'alpha di riempimento e salvare
  i file PDF modificati.
og_image_alt: Screenshot of a PDF page showing transparent graphics applied with Aspose.Pdf
  in C#
og_title: Come impostare la trasparenza in un PDF con Aspose.Pdf C# – guida passo
  passo
schemas:
- author: Aspose
  dateModified: '2026-10-13'
  description: Learn how to set transparency in a PDF with Aspose.Pdf for C#. Also
    see how to save modified PDF and change fill alpha.
  headline: How to set transparency in a PDF with Aspose.Pdf C#
  type: TechArticle
- description: Learn how to set transparency in a PDF with Aspose.Pdf for C#. Also
    see how to save modified PDF and change fill alpha.
  name: How to set transparency in a PDF with Aspose.Pdf C#
  steps:
  - name: Load the PDF document
    text: '```csharp using Aspose.Pdf; using System.Collections.Generic;'
  - name: Edit PDF resources to add a graphics state
    text: '```csharp // Get the first page (pages are 1‑based) Page firstPage = pdfDocument.Pages[1];'
  - name: Change fill alpha and set fill opacity
    text: '```csharp // Create an empty graphics state dictionary CosPdfDictionary
      newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);'
  - name: Add the new graphics state to the ExtGState dictionary
    text: '```csharp // Register the new state under the name "GS0" extGStateDict.Add("GS0",
      newGraphicsState); ```'
  - name: (Optional) Apply the graphics state in a content stream
    text: 'If you want to draw a rectangle using the new fill opacity, add the following
      after the previous steps:'
  - name: Save modified PDF
    text: '```csharp // Persist the changes to a new file pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
      ```'
  - name: Next steps
    text: '* Explore other blend modes (`Multiply`, `Screen`, etc.) by changing the
      `BM` entry. * Adjust stroke alpha (`CA`) to create semi‑transparent outlines.
      * Combine multiple graphics states to build a library of reusable visual effects.'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF manipulation
- Transparency
title: Come impostare la trasparenza in un PDF con Aspose.Pdf C#
url: /it/net/images-graphics/how-to-set-transparency-in-a-pdf-with-aspose-pdf-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come impostare la trasparenza in un PDF con Aspose.Pdf C#

Se devi impostare la trasparenza in un PDF usando C#, questo tutorial mostra i passaggi esatti. Imparerai anche come salvare i file PDF modificati e cambiare l'alpha di riempimento senza uscire dall'ambiente Aspose.Pdf.

La guida percorre il caricamento di un documento, la modifica delle risorse PDF, la creazione di uno stato grafico che definisce l'opacità di riempimento e il salvataggio delle modifiche. Non sono necessari strumenti esterni; tutto viene eseguito all'interno di un progetto .NET standard.

## Prerequisiti

Prima di iniziare, assicurati di avere:

* .NET 6.0 o versioni successive installate  
* Una licenza valida di Aspose.Pdf per .NET (o una chiave di valutazione gratuita)  
* Un file PDF di input situato in una directory nota  

Puoi aggiungere il pacchetto Aspose.Pdf tramite NuGet:

```bash
dotnet add package Aspose.Pdf
```

## Come impostare la trasparenza in un PDF

Questa sezione contiene l'implementazione principale. Ogni passaggio spiega **perché** il codice è necessario, non solo **cosa** fa.

### Passo 1: Caricare il documento PDF

```csharp
using Aspose.Pdf;
using System.Collections.Generic;

// Load the source PDF
using var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");
```

*Perché questo passaggio?*  
`Document` rappresenta l'intero file PDF in memoria. Aprire il file ti dà accesso a pagine, risorse e oggetti a basso livello che modificherai.

### Passo 2: Modificare le risorse PDF per aggiungere uno stato grafico

```csharp
// Get the first page (pages are 1‑based)
Page firstPage = pdfDocument.Pages[1];

// Create an editor for the page's resource dictionary
DictionaryEditor resourceEditor = new DictionaryEditor(firstPage.Resources);

// Retrieve the ExtGState dictionary; it holds graphics state objects
CosPdfDictionary extGStateDict = resourceEditor["ExtGState"].ToCosPdfDictionary();
```

*Perché questo passaggio?*  
Le pagine PDF memorizzano oggetti riutilizzabili — font, immagini e stati grafici — in un dizionario delle risorse. La voce `ExtGState` contiene le impostazioni di trasparenza. Modificando questo dizionario puoi introdurre un nuovo stato a cui la pagina può fare riferimento.

### Passo 3: Cambiare l'alpha di riempimento e impostare l'opacità di riempimento

```csharp
// Create an empty graphics state dictionary
CosPdfDictionary newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

// Define the graphics state entries
var graphicsStateEntries = new[]
{
    // Stroke alpha (CA) – fully opaque
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
    // Fill alpha (ca) – 50 % transparent
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
    // Blend mode (BM) – normal composition
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
};

// Populate the new graphics state
foreach (var entry in graphicsStateEntries)
    newGraphicsState.Add(entry);
```

*Perché questo passaggio?*  
`ca` controlla **l'opacità di riempimento**, mentre `CA` controlla **l'opacità del tratto**. Impostare `ca` a `0.5` rende le forme riempite al 50 % trasparenti. La voce `BM` seleziona la modalità di fusione; `"Normal"` è la scelta più comune per la trasparenza standard.

### Passo 4: Aggiungere il nuovo stato grafico al dizionario ExtGState

```csharp
// Register the new state under the name "GS0"
extGStateDict.Add("GS0", newGraphicsState);
```

*Perché questo passaggio?*  
Dare un nome allo stato grafico (`"GS0"`) consente ai flussi di contenuto sulla pagina di fare riferimento ad esso con l'operatore `gs`. Dopo questa registrazione la pagina può applicare la trasparenza appena definita.

### Passo 5: (Facoltativo) Applicare lo stato grafico in un flusso di contenuto

Se vuoi disegnare un rettangolo usando la nuova opacità di riempimento, aggiungi quanto segue dopo i passaggi precedenti:

```csharp
// Create a content stream that uses the new graphics state
string cs = @"
q               % Save graphics state
/GS0 gs         % Apply the graphics state defined earlier
0 0 200 100 re  % Define a rectangle (x, y, width, height)
0.2 0.6 0.8 rg  % Set fill color (RGB)
f               % Fill the rectangle using the current graphics state
Q               % Restore graphics state
";

firstPage.Contents.Add(new Aspose.Pdf.Operator.GsContent(cs));
```

*Perché questo passaggio?*  
Gli operatori `q`/`Q` salvano e ripristinano lo stato grafico, garantendo che la trasparenza influisca solo sui comandi di disegno desiderati. L'operatore `gs` passa allo stato grafico denominato `"GS0"`.

### Passo 6: Salvare il PDF modificato

```csharp
// Persist the changes to a new file
pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
```

*Perché questo passaggio?*  
Il salvataggio scrive il dizionario delle risorse aggiornato e eventuali nuovi flussi di contenuto su disco. Il file risultante (`output.pdf`) contiene il rettangolo trasparente definito nel passaggio precedente.

## Esempio completo eseguibile

Mettendo insieme tutti i pezzi, ecco un programma completo che puoi compilare ed eseguire:

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Operators;
using System.Collections.Generic;

class SetTransparencyDemo
{
    static void Main()
    {
        // Load the source PDF
        using var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");

        // Access the first page and its resources
        Page firstPage = pdfDocument.Pages[1];
        var resourceEditor = new DictionaryEditor(firstPage.Resources);
        var extGStateDict = resourceEditor["ExtGState"].ToCosPdfDictionary();

        // Create a new graphics state with 50 % fill opacity
        var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
        var graphicsStateEntries = new[]
        {
            new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),   // stroke alpha
            new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // fill alpha
            new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
        };
        foreach (var entry in graphicsStateEntries)
            newGraphicsState.Add(entry);

        // Register the graphics state as "GS0"
        extGStateDict.Add("GS0", newGraphicsState);

        // Optional: draw a rectangle using the new transparency
        string cs = @"
q
/GS0 gs
0 0 200 100 re
0.2 0.6 0.8 rg
f
Q
";
        firstPage.Contents.Add(new GsContent(cs));

        // Save the modified PDF
        pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
    }
}
```

**Risultato atteso** – `output.pdf` mostra un rettangolo riempito con un colore viola chiaro al 50 % trasparente, consentendo al contenuto di sfondo di essere parzialmente visibile.

## Domande frequenti e casi particolari

* **Posso cambiare l'opacità del tratto invece di quella di riempimento?**  
  Imposta il valore di `CA` (lettere maiuscole) a un numero compreso tra `0` (completamente trasparente) e `1` (completamente opaco). L'esempio imposta già `CA` a `1`, il che significa che i tratti rimangono opachi.

* **Cosa succede se la pagina non ha già un dizionario ExtGState?**  
  `resourceEditor["ExtGState"]` creerà automaticamente un dizionario vuoto. Aggiungere `"GS0"` funziona allo stesso modo.

* **Lo stato grafico è riutilizzabile su più pagine?**  
  Sì. Una volta aggiunta la voce al dizionario delle risorse del documento, qualsiasi pagina che faccia riferimento a `"GS0"` erediterà le stesse impostazioni di trasparenza.

* **In che modo questo approccio differisce dall'uso dell'API di alto livello `Graphics`?**  
  Modificare il dizionario delle risorse a basso livello ti dà un controllo preciso sugli internali del PDF e produce file più piccoli perché evita l'inserimento di oggetti aggiuntivi.

## Conclusione

Ora sai **come impostare la trasparenza in un PDF** con Aspose.Pdf per C#. Il tutorial ha coperto la modifica delle risorse PDF, il cambiamento dell'alpha di riempimento, l'impostazione dell'opacità di riempimento e il salvataggio del PDF modificato. Con questa base puoi sperimentare diverse modalità di fusione, applicare la trasparenza al testo o creare stati grafici riutilizzabili per documenti complessi.

### Prossimi passi

* Esplora altre modalità di fusione (`Multiply`, `Screen`, ecc.) modificando la voce `BM`.  
* Regola l'alpha del tratto (`CA`) per creare contorni semi‑trasparenti.  
* Combina più stati grafici per costruire una libreria di effetti visivi riutilizzabili.  

Sentiti libero di condividere i tuoi risultati o porre domande nei commenti. Buon coding!

## Cosa dovresti imparare dopo?


I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità aggiuntive dell'API ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [How to Customize PDFs with Aspose.PDF for .NET&#58; Set Page Margins and Draw Lines](/pdf/english/net/document-manipulation/customize-pdfs-aspose-pdf-set-margins-draw-lines/)
- [How to Set Image Size in a PDF Using Aspose-PDF for .NET](/pdf/english/net/images-graphics/set-image-size-pdf-aspose-dotnet/)
- [How to Set PDF Permissions Using Aspose.PDF for .NET&#58; A Comprehensive Guide](/pdf/english/net/security-permissions/set-pdf-privileges-aspose-pdf-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}