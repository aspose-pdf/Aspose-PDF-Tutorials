---
category: general
date: 2026-09-28
description: Scopri come aggiungere lo stato grafico PDF con Aspose.PDF in C#. Questa
  guida passo passo ti mostra come impostare l'opacità e la modalità di fusione per
  le pagine PDF.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add graphics state pdf
- Aspose PDF graphics state
- PDF opacity settings
- modify PDF resources
- Aspose.Pdf DictionaryEditor
language: it
lastmod: 2026-09-28
og_description: Aggiungi lo stato grafico PDF usando Aspose.PDF in C#. Segui questa
  guida per modificare l'opacità del tratto/riempimento e la modalità di fusione su
  qualsiasi pagina PDF.
og_image_alt: Screenshot of a PDF page after adding graphics state pdf with opacity
  settings
og_title: Aggiungi lo stato grafico PDF con Aspose.PDF – guida completa C#
schemas:
- author: Aspose
  dateModified: '2026-09-28'
  description: Learn how to add graphics state pdf with Aspose.PDF in C#. This step‑by‑step
    guide shows you how to set opacity and blend mode for PDF pages.
  headline: How to add graphics state pdf using Aspose.PDF in C#
  type: TechArticle
tags:
- Aspose.PDF
- C#
- PDF manipulation
title: Come aggiungere lo stato grafico PDF usando Aspose.PDF in C#
url: /it/net/programming-with-operators/how-to-add-graphics-state-pdf-using-aspose-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come aggiungere graphics state pdf usando Aspose.PDF in C#

Se hai bisogno di **add graphics state pdf** per controllare l'opacità o la modalità di fusione, questa guida ti mostra esattamente come fare. Con Aspose.PDF puoi modificare il dizionario delle risorse di una pagina e inserire uno stato grafico personalizzato in poche righe di codice.

Imparerai a caricare un PDF, creare un nuovo dizionario di graphics state, impostare l'opacità del tratto, l'opacità di riempimento e la modalità di fusione, quindi salvare il documento modificato. Non sono necessari strumenti esterni—solo la libreria Aspose.PDF per .NET.

## Prerequisiti

Prima di iniziare, assicurati di avere:

* .NET 6.0 o successivo (il codice funziona anche con .NET Core 3.1 e .NET Framework 4.7+)
* Una licenza valida per **Aspose.PDF for .NET** (la versione di prova gratuita è sufficiente per la valutazione)
* Un file PDF di input (`input.pdf`) collocato in una cartella nota
* Visual Studio 2022 o qualsiasi editor C# tu preferisca

> **Pro tip:** Tieni i file PDF al di fuori della cartella del progetto per evitare commit accidentali di binari di grandi dimensioni.

## Passo 1: Installa il pacchetto NuGet Aspose.PDF

Apri un terminale nella directory del tuo progetto ed esegui:

```bash
dotnet add package Aspose.Pdf
```

Il pacchetto contiene lo spazio dei nomi `Aspose.Pdf`, che fornisce le classi `Document`, `DictionaryEditor` e `CosPdfDictionary` utilizzate più avanti.

## Passo 2: Carica il documento PDF

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Path to the source PDF
string pdfPath = @"C:\MyPdfs\input.pdf";

// The `using` statement ensures the document is disposed automatically
using var pdfDocument = new Document(pdfPath);
```

*Perché questo passo è importante*: il caricamento del PDF crea una rappresentazione in memoria che puoi manipolare. L'oggetto `Document` ti dà accesso a pagine, risorse e oggetti COS a basso livello necessari per **add graphics state pdf**.

## Passo 3: Accedi alle risorse della prima pagina

```csharp
// Get the first page (pages are 1‑based in Aspose.PDF)
Page firstPage = pdfDocument.Pages[1];

// Create a DictionaryEditor to work with the page’s resource dictionary
var resourcesEditor = new DictionaryEditor(firstPage.Resources);
```

Il dizionario `Resources` contiene oggetti come font, immagini e voci **ExtGState**. Modificarlo è l'unico modo per **modify PDF resources** in modo sicuro.

## Passo 4: Recupera (o crea) il dizionario ExtGState

```csharp
// Try to get the existing ExtGState dictionary; if it does not exist, create one
CosPdfDictionary extGStateDict;
if (resourcesEditor.ContainsKey("ExtGState"))
{
    extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
}
else
{
    extGStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
    resourcesEditor["ExtGState"] = extGStateDict;
}
```

*Perché è importante*: la voce `ExtGState` memorizza gli oggetti di graphics state. Se il PDF ne contiene già uno, lo riutilizziamo; altrimenti creiamo un nuovo dizionario in modo che l'operazione **add graphics state pdf** non fallisca mai.

## Passo 5: Costruisci un nuovo dizionario di graphics state

```csharp
// Create an empty dictionary that will hold our graphics state parameters
CosPdfDictionary graphicsStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

// Stroke opacity (CA) – 1.0 means fully opaque strokes
graphicsStateDict.Add("CA", new CosPdfNumber(1));

// Fill opacity (ca) – 0.5 makes filled shapes 50 % transparent
graphicsStateDict.Add("ca", new CosPdfNumber(0.5));

// Blend mode (BM) – "Normal" is the default PDF blend mode
graphicsStateDict.Add("BM", new CosPdfName("Normal"));
```

Le chiavi `CA`, `ca` e `BM` sono definite dalla specifica PDF. Impostarle ti permette di controllare le **PDF opacity settings** e il comportamento di fusione per tutti i comandi di disegno successivi.

## Passo 6: Registra il nuovo graphics state in ExtGState

```csharp
// Choose a unique name for the graphics state, e.g., GS0
extGStateDict.Add("GS0", graphicsStateDict);
```

Ora il dizionario delle risorse della pagina contiene una nuova voce chiamata `GS0`. Quando in seguito farai riferimento a `GS0` nei flussi di contenuto, il visualizzatore PDF applicherà l'opacità e la modalità di fusione che hai definito.

## Passo 7: (Opzionale) Applica lo stato grafico al contenuto esistente

Se desideri modificare i comandi di disegno già presenti, devi modificare il flusso di contenuto della pagina. Di seguito un esempio semplice che antepone un operatore `gs` per impostare lo stato grafico prima di qualsiasi disegno:

```csharp
// Retrieve the page’s content stream as a string
string originalContent = firstPage.Contents[1].ToString();

// Prepend the graphics state operator
string updatedContent = "GS0 gs\n" + originalContent;

// Replace the page content with the updated stream
firstPage.Contents[1].Replace(updatedContent);
```

> **Nota:** La manipolazione diretta dei flussi di contenuto può essere delicata. Testa sempre su una copia del PDF prima di procedere.

## Passo 8: Salva il PDF modificato

```csharp
string outputPath = @"C:\MyPdfs\output.pdf";
pdfDocument.Save(outputPath);
```

Dopo il salvataggio, apri `output.pdf` in un visualizzatore PDF. Qualsiasi forma riempita che disegnerai dopo l'operatore `GS0 gs` apparirà con un'opacità di riempimento del 50 % mentre i tratti rimarranno completamente opachi, dimostrando che hai eseguito con successo **add graphics state pdf**.

### Risultato atteso

| Prima | Dopo (con GS0) |
|--------|------------------|
| ![Before PDF page](placeholder-before.png){.img-fluid alt="Pagina PDF originale"} | ![After PDF page](placeholder-after.png){.img-fluid alt="Pagina PDF dopo l'aggiunta di graphics state pdf con impostazioni di opacità"} |

La colonna “Dopo” mostra riempimenti semitrasparenti mentre i tratti restano solidi, esattamente come definito nel dizionario di graphics state.

## Domande frequenti & casi particolari

| Domanda | Risposta |
|----------|--------|
| **Posso aggiungere più graphics states?** | Sì. Basta aggiungere voci aggiuntive (`GS1`, `GS2`, …) a `extGStateDict` e fare riferimento al nome desiderato nel flusso di contenuto. |
| **E se il PDF utilizza già un nome come `GS0`?** | Scegli un identificatore unico (ad esempio `GS_custom1`). Puoi controllare `extGStateDict.Keys` prima di aggiungere. |
| **Funziona con PDF criptati?** | Il PDF deve essere aperto con la password corretta. Usa `new Document(pdfPath, new LoadOptions { Password = "secret" })`. |
| **La modalità di fusione è limitata a “Normal”?** | No. La specifica PDF supporta molte modalità di fusione (`Multiply`, `Screen`, `Overlay`, ecc.). Sostituisci `"Normal"` con qualsiasi nome supportato. |
| **Questo influenzerà le altre pagine?** | Solo la pagina le cui risorse hai modificato. Se ti serve lo stesso stato su più pagine, ripeti i passi 3‑6 per ciascuna pagina o modifica le risorse globali del documento. |

## Conclusione

Ora sai come **add graphics state pdf** con Aspose.PDF per .NET, impostare l'opacità del tratto e del riempimento, scegliere una modalità di fusione e, opzionalmente, applicare lo stato al contenuto esistente. Questa tecnica ti offre un controllo fine sul rendering dei PDF senza dover convertire il file in un formato immagine.

Successivamente, potresti approfondire:

* **PDF opacity settings** per immagini e blocchi di testo
* L'uso di **Aspose.Pdf DictionaryEditor** per sostituire font o incorporare profili ICC personalizzati
* La combinazione di più graphics states per creare effetti visivi complessi

Sentiti libero di sperimentare con valori di opacità diversi, modalità di fusione e ambiti di risorse. Padroneggiare queste manipolazioni PDF a basso livello apre la porta a scenari avanzati di generazione e redazione di documenti.

---


## Cosa dovresti imparare dopo?


I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare ulteriori funzionalità dell'API e a esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Come aggiungere un timbro a PDF con Aspose.Pdf – Guida passo‑passo](/pdf/english/net/programming-with-stamps-and-watermarks/how-to-add-stamp-to-pdf-with-aspose-pdf-step-by-step-guide/)
- [Come aggiungere immagini a PDF usando Aspose.PDF per .NET: Guida passo‑passo](/pdf/english/net/images-graphics/add-images-to-pdfs-aspose-pdf-net/)
- [Come rimuovere grafiche da PDF usando Aspose.PDF .NET: Guida completa](/pdf/english/net/images-graphics/remove-graphics-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}