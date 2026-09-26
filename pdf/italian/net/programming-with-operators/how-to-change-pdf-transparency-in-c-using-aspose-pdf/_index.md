---
category: general
date: 2026-09-24
description: Scopri come modificare la trasparenza dei PDF in C# con Aspose.Pdf. Questa
  guida passo passo copre l'opacità dei PDF, la modalità di fusione e la modifica
  dello stato grafico.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- change PDF transparency
- Aspose.Pdf graphics state
- PDF opacity
- C# PDF manipulation
- blend mode PDF
- modify PDF resources
language: it
lastmod: 2026-09-24
og_description: Modifica la trasparenza dei PDF in C# usando Aspose.Pdf. Segui questa
  guida per modificare l'opacità del PDF, la modalità di fusione e lo stato grafico
  per una produzione professionale di documenti.
og_image_alt: Screenshot showing C# code that changes PDF transparency
og_title: Modifica la trasparenza dei PDF in C# – guida completa ad Aspose.Pdf
schemas:
- author: Aspose
  dateModified: '2026-09-24'
  description: Learn how to change PDF transparency in C# with Aspose.Pdf. This step‑by‑step
    guide covers PDF opacity, blend mode and graphics state editing.
  headline: How to change PDF transparency in C# using Aspose.Pdf
  type: TechArticle
tags:
- PDF
- C#
- Aspose.Pdf
- Transparency
title: Come modificare la trasparenza di un PDF in C# usando Aspose.Pdf
url: /it/net/programming-with-operators/how-to-change-pdf-transparency-in-c-using-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come modificare la trasparenza PDF in C# usando Aspose.Pdf

Se hai bisogno di **modificare la trasparenza PDF** in un progetto .NET, questa guida ti mostra esattamente come farlo con Aspose.Pdf. Vedrai un esempio completo e eseguibile che modifica l'opacità PDF, imposta una modalità di fusione e aggiorna il dizionario dello stato grafico della pagina.

Modificare la trasparenza PDF è una necessità comune quando si desiderano filigrane, grafiche sovrapposte o effetti visivi personalizzati. In questo tutorial imparerai a modificare lo **stato grafico Aspose.Pdf**, regolare l'**opacità PDF** e lavorare con le impostazioni **blend mode PDF**, tutto usando codice C# pulito.

## Prerequisiti

* .NET 6.0 o versioni successive installate  
* Una licenza Aspose.Pdf per .NET (o una chiave di valutazione temporanea)  
* Un file PDF chiamato `input.pdf` in una cartella che puoi riferire come `YOUR_DIRECTORY`  
* Familiarità di base con C# e Visual Studio (qualsiasi IDE va bene)

Non sono richiesti pacchetti NuGet aggiuntivi oltre a `Aspose.Pdf`. Il codice funziona su Windows, Linux o macOS perché Aspose.Pdf è cross‑platform.

## Modifica della trasparenza PDF – passo 1: aprire il documento PDF

La prima operazione è caricare il PDF di origine. L'uso di un blocco `using` garantisce che il handle del file venga rilasciato automaticamente.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;
using System.Collections.Generic;

string inputPath  = @"YOUR_DIRECTORY\input.pdf";
string outputPath = @"YOUR_DIRECTORY\output.pdf";

using (var document = new Document(inputPath))
{
    // The document is now ready for manipulation.
```

Aprire il documento è la base per qualsiasi attività di **manipolazione PDF in C#**. Se il file non viene trovato, Aspose.Pdf genera una `FileNotFoundException`, quindi verifica il percorso prima di eseguire il codice.

## Accedere alle risorse della pagina con lo stato grafico Aspose.Pdf

Successivamente, recupera la prima pagina e il suo dizionario delle risorse. Il dizionario delle risorse contiene oggetti come font, immagini e voci **ExtGState** che controllano i parametri grafici.

```csharp
    // Step 2: Get the first page of the document
    var page = document.Pages[1];

    // Step 3: Access the page's resource dictionary for editing
    var resourcesEditor = new DictionaryEditor(page.Resources);
```

La classe `DictionaryEditor` fornisce un wrapper comodo per leggere e scrivere i dizionari PDF. Qui ci concentriamo sul dizionario **ExtGState** perché memorizza le impostazioni di trasparenza.

## Creare e configurare un nuovo stato grafico per l'opacità PDF

Ora costruiamo un nuovo dizionario di stato grafico. Questo dizionario conterrà i parametri che definiscono l'opacità del tratto (`CA`), l'opacità di riempimento (`ca`) e la modalità di fusione (`BM`).

```csharp
    // Step 4: Retrieve the existing ExtGState dictionary (graphics states)
    var extGState = resourcesEditor["ExtGState"].ToCosPdfDictionary();

    // Step 5: Create a new empty graphics state dictionary
    var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(document);

    // Step 6: Define graphics state parameters (stroke opacity, fill opacity, blend mode)
    var parameters = new[]
    {
        new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),            // Stroke opacity (fully opaque)
        new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),          // Fill opacity (50 % transparent)
        new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))       // Blend mode PDF (standard normal blending)
    };

    // Step 7: Add each parameter to the new graphics state dictionary
    foreach (var param in parameters)
        newGraphicsState.Add(param);
```

* **`CA`** controlla l'opacità delle operazioni di tratto (linee, bordi).  
* **`ca`** controlla l'opacità delle operazioni di riempimento (forme riempite, testo).  
* **`BM`** seleziona la modalità di fusione; `"Normal"` è il valore predefinito, ma puoi usare `"Multiply"` o `"Screen"` per effetti artistici.

Queste impostazioni sono il nucleo della manipolazione dell'**opacità PDF**. Regola i valori numerici in base al tuo design visivo—`0` significa completamente trasparente, `1` completamente opaco.

## Inserire lo stato grafico e salvare il documento

Dopo aver costruito il nuovo stato, lo aggiungiamo al dizionario **ExtGState** esistente sotto un nome unico (`GS0`). Infine, salviamo il PDF modificato.

```csharp
    // Step 8: Insert the new graphics state into the ExtGState dictionary with a name
    extGState.Add("GS0", newGraphicsState);

    // Step 9: Save the modified PDF document
    document.Save(outputPath);
}
```

Quando il PDF viene aperto in un visualizzatore, qualsiasi contenuto che fa riferimento a `GS0` verrà renderizzato con la trasparenza definita. Puoi successivamente applicare questo stato grafico a oggetti specifici usando la proprietà `GraphicsState` dei comandi di disegno (ad esempio, `page.Contents.Add(new TextFragment(...){ GraphicsState = "GS0" })`).

## Verificare il risultato

Apri `output.pdf` in Adobe Acrobat Reader, Foxit o qualsiasi visualizzatore PDF che supporti la trasparenza. Dovresti vedere gli elementi di riempimento della prima pagina renderizzati al 50 % di opacità mentre i tratti rimangono completamente opachi. Se non noti alcuna modifica, assicurati che la pagina utilizzi effettivamente il nuovo stato grafico—altrimenti, puoi assegnare esplicitamente `GS0` agli oggetti che desideri modificare.

![Change PDF transparency in C# code example](path/to/image.png){: .img-responsive alt="Esempio di codice C# per cambiare la trasparenza PDF"}

*L'immagine sopra mostra il codice C# completo che cambia la trasparenza PDF.*

## Variazioni comuni e casi limite

| Situazione | Come adattare il codice |
|------------|--------------------------|
| **Pagine multiple** | Itera su `document.Pages` e ripeti i passi 2‑8 per ogni pagina. |
| **Modalità di fusione diversa** | Sostituisci `"Normal"` con `"Multiply"`, `"Screen"` o qualsiasi nome di fusione standard PDF. |
| **Opacità di riempimento più alta** | Modifica `new CosPdfNumber(0.5)` con un valore compreso tra `0` e `1`. |
| **Nessun ExtGState esistente** | Se `resourcesEditor["ExtGState"]` restituisce `null`, crea un nuovo dizionario: `var extGState = CosPdfDictionary.CreateEmptyDictionary(document); resourcesEditor["ExtGState"] = extGState;` |

Queste variazioni dimostrano la flessibilità di **modificare le risorse PDF** usando Aspose.Pdf. Regolando i parametri, puoi creare filigrane, sovrapposizioni semitrasparenti o elementi UI personalizzati all'interno di un PDF.

## Esempio completo e eseguibile

Di seguito trovi il programma completo che puoi copiare‑incollare in un nuovo progetto Console App. Contiene tutte le direttive `using` necessarie, la gestione degli errori e i commenti.



## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare ulteriori funzionalità dell'API ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Modifica l'opacità PDF con Aspose.PDF – Guida completa C#](/pdf/english/net/programming-with-stamps-and-watermarks/change-pdf-opacity-with-aspose-pdf-complete-c-guide/)
- [Modifica l'opacità PDF in C# – Guida completa Aspose](/pdf/english/net/programming-with-stamps-and-watermarks/change-pdf-opacity-in-c-complete-aspose-guide/)
- [Aggiungi trasparenza al PDF usando Aspose – Guida completa C#](/pdf/english/net/programming-with-operators/add-transparency-to-pdf-using-aspose-complete-c-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}