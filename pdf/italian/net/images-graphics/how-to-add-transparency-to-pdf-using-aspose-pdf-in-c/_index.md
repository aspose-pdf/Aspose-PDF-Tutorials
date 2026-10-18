---
category: general
date: 2026-10-17
description: Aggiungi trasparenza al PDF con Aspose.PDF per .NET, modifica le risorse
  PDF e salva i file PDF modificati in un unico esempio eseguibile.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add transparency to pdf
- save modified pdf
- edit pdf resources
- Aspose.PDF transparency
- C# PDF manipulation
language: it
lastmod: 2026-10-17
og_description: Aggiungi trasparenza ai PDF usando Aspose.PDF per .NET, modifica le
  risorse PDF e salva i file PDF modificati con un esempio completo in C#.
og_image_alt: Screenshot showing a PDF with added transparency using Aspose.PDF in
  C#
og_title: Aggiungi trasparenza al PDF con Aspose.PDF – guida
schemas:
- author: Aspose
  dateModified: '2026-10-17'
  description: Add transparency to PDF with Aspose.PDF for .NET, edit PDF resources,
    and save modified PDF files in a single, runnable example.
  headline: How to add transparency to PDF using Aspose.PDF in C#
  type: TechArticle
tags:
- pdf
- aspnet
- csharp
title: Come aggiungere trasparenza a un PDF usando Aspose.PDF in C#
url: /it/net/images-graphics/how-to-add-transparency-to-pdf-using-aspose-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come aggiungere trasparenza a PDF usando Aspose.PDF in C#

Se hai bisogno di **aggiungere trasparenza a PDF** programmaticamente, questa guida ti mostra una soluzione chiara, end‑to‑end con Aspose.PDF per .NET. Imparerai come **modificare le risorse PDF**, creare uno stato grafico personalizzato e **salvare il PDF modificato** senza uscire dal tuo progetto C#.

Lavorare con la trasparenza nei PDF spesso sembra nascosto dietro operatori PDF di basso livello. Alla fine di questo tutorial avrai un esempio completamente funzionante che potrai copiare‑incollare, eseguire e adattare a più pagine o a diversi blend mode.

## Prerequisiti

- .NET 6.0 (o qualsiasi versione recente di .NET)  
- Pacchetto NuGet Aspose.PDF per .NET (`Aspose.Pdf`)  
- Conoscenze di base di C#  
- Un file PDF di input (`input.pdf`) posizionato in una cartella a cui puoi fare riferimento

> **Consiglio professionale:** Installa il pacchetto con `dotnet add package Aspose.Pdf` prima di iniziare.

## Passo 1: Caricare il documento PDF

La prima operazione è aprire il PDF di origine. Aspose.PDF rappresenta un PDF come un oggetto `Document`, che ti consente di accedere a pagine, risorse e dizionari di basso livello.

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Collections;
using Aspose.Pdf.Text;
using Aspose.Pdf.Generator;   // for graphics‑state objects

// Path to the original PDF
string pdfPath = @"YOUR_DIRECTORY\input.pdf";

// Open the document in a using block so it disposes automatically
using (var document = new Document(pdfPath))
{
    // The rest of the steps are inside this block
```

*Perché è importante:* Aprire il documento in questo modo garantisce che il handle del file venga rilasciato dopo aver terminato le modifiche, evitando problemi di blocco del file quando successivamente **salvi il PDF modificato**.

## Passo 2: Accedere alla prima pagina e al suo dizionario delle risorse

Le pagine PDF memorizzano gli oggetti grafici (font, immagini, voci ExtGState) in un *dizionario delle risorse*. Per modificare l'opacità dobbiamo lavorare con il sotto‑dizionario `ExtGState`.

```csharp
    // Get the first page (pages are 1‑based in Aspose.PDF)
    Page page = document.Pages[1];

    // Obtain a mutable editor for the page's resources
    var resourcesEditor = new DictionaryEditor(page.Resources);

    // Retrieve the ExtGState dictionary; create it if missing
    var extGStateDict = resourcesEditor["ExtGState"]?.ToCosPdfDictionary()
                         ?? new CosPdfDictionary(document);
```

*Perché è importante:* Se il PDF originale contiene già un dizionario `ExtGState`, lo estendiamo; altrimenti ne creiamo uno nuovo così possiamo **modificare le risorse PDF** in modo sicuro.

## Passo 3: Creare un nuovo stato grafico con trasparenza

Uno stato grafico (`ExtGState`) contiene parametri come l'opacità del tratto (`CA`), l'opacità del riempimento (`ca`) e il blend mode (`BM`). Creiamo un dizionario vuoto e lo popoliamo con i valori desiderati.

```csharp
    // Create an empty ExtGState dictionary for the new entry
    var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(document);

    // Define the transparency entries
    var entries = new[]
    {
        // CA – stroke opacity (1 = fully opaque)
        new KeyValuePair<string, ICosPdfPrimitive>("CA",
            new CosPdfNumber(1)),

        // ca – fill opacity (0.5 = 50 % transparent)
        new KeyValuePair<string, ICosPdfPrimitive>("ca",
            new CosPdfNumber(0.5)),

        // BM – blend mode (Normal is the default)
        new KeyValuePair<string, ICosPdfPrimitive>("BM",
            new CosPdfName("Normal"))
    };

    // Add each entry to the new ExtGState dictionary
    foreach (var entry in entries)
        newGraphicsState.Add(entry);
```

*Perché è importante:* L'entrata `ca` è la chiave per **aggiungere trasparenza a PDF** nei contenuti che usano questo stato grafico. Puoi regolare il valore numerico (0 – 1) per controllare quanto l'oggetto diventa trasparente.

## Passo 4: Inserire lo stato grafico nelle risorse della pagina

Dobbiamo assegnare al nuovo stato grafico un nome (ad esempio, `"GS0"`). Questo nome potrà in seguito essere referenziato dai flussi di contenuto per applicare la trasparenza.

```csharp
    // Add the new ExtGState under the name "GS0"
    extGStateDict.Add("GS0", newGraphicsState);

    // Ensure the modified ExtGState dictionary is written back to the page
    resourcesEditor["ExtGState"] = extGStateDict;
```

*Perché è importante:* Aggiungendo `"GS0"` al dizionario `ExtGState`, qualsiasi operazione di disegno che seleziona questo stato verrà renderizzata con l'opacità definita. Questo è il fulcro di **modificare le risorse PDF** per la trasparenza.

## Passo 5: Applicare lo stato grafico al contenuto della pagina (opzionale)

Se desideri che il contenuto della pagina esistente utilizzi automaticamente la nuova trasparenza, devi anteporre un operatore di stato grafico al flusso di contenuto della pagina. Il frammento seguente dimostra come avvolgere il contenuto esistente con `gs` (imposta lo stato grafico) e `Q` (ripristina lo stato grafico).

```csharp
    // Get the current content stream
    var content = page.Contents[1]; // assume a single content stream

    // Build a new stream that sets the graphics state, draws the original content, then restores
    string gsOperator = "/GS0 gs\n"; // select the graphics state we created
    string restoreOperator = "Q\n";   // restore graphics state after drawing

    // Prepend the gs operator and append the restore operator
    string newStream = gsOperator + content.Stream.ToString() + restoreOperator;

    // Replace the original stream with the modified one
    content.Stream = new CosPdfStream(document);
    content.Stream.SetData(newStream);
```

*Perché è importante:* Senza questo passaggio, lo stato grafico esiste ma non viene utilizzato. Aggiungere l'operatore `gs` indica al renderer PDF di applicare la trasparenza a tutto ciò che segue.

## Passo 6: **Salvare il PDF modificato** su disco

Infine, scrivi il documento modificato in un nuovo file. Il metodo `Save` gestisce automaticamente tutti gli aggiornamenti di basso livello.

```csharp
    // Path for the output PDF
    string outputPath = @"YOUR_DIRECTORY\output.pdf";

    // Persist the changes
    document.Save(outputPath);
}
```

*Perché è importante:* La chiamata `document.Save` garantisce che il **PDF modificato** contenga la nuova voce `ExtGState` e il flusso di contenuto che la riferisce. Il file risultante mostrerà il riempimento semitrasparente nella prima pagina.

## Risultato atteso

Apri `output.pdf` in qualsiasi visualizzatore PDF (Adobe Reader, Chrome, ecc.) e dovresti vedere la grafica della prima pagina renderizzata con un'opacità di riempimento del 50 %. Se ispezioni il PDF con uno strumento come **PDF‑Tron** o **iText**, troverai una voce del dizionario `ExtGState` chiamata `GS0` con il valore `ca` impostato a `0.5`.

## Casi limite e variazioni

| Situazione | Cosa modificare |
|-----------|----------------|
| **Multiple pages** | Itera su `document.Pages` e ripeti i passi 2‑5 per ogni pagina, usando un nome unico come `GS1`, `GS2`, … |
| **Existing ExtGState name conflict** | Verifica `extGStateDict.ContainsKey("GS0")` prima di aggiungere; se esiste, genera una nuova chiave (`"GS" + Guid.NewGuid().ToString("N")`) |
| **Different blend modes** | Sostituisci `"Normal"` con `"Multiply"`, `"Screen"`, ecc., modificando la voce `BM` |
| **Only stroke opacity needed** | Ometti la voce `ca` o impostala a `1` e regola `CA` invece |

## Esempio completo, eseguibile



## Cosa dovresti imparare dopo?

I tutorial seguenti coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità aggiuntive dell'API e a esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Aggiungere trasparenza a PDF con Aspose.PDF – Guida completa C#](/pdf/english/net/programming-with-stamps-and-watermarks/add-transparency-to-pdf-with-aspose-pdf-complete-c-guide/)
- [Come aggiungere timbri di pagina nei PDF usando Aspose.PDF per .NET: Guida completa](/pdf/english/net/watermarks-backgrounds/add-page-stamp-aspose-pdf-dotnet-guide/)
- [Come aggiungere immagini ai PDF usando Aspose.PDF per .NET: Guida completa](/pdf/english/net/images-graphics/add-images-to-pdfs-using-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}