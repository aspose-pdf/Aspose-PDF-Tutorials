---
category: general
date: 2026-08-14
description: Crea un dizionario PDF vuoto in C# usando Aspose.Pdf – scopri come aggiungere
  uno stato grafico alla collezione ExtGState e modificare i PDF programmaticamente.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create empty PDF dictionary
- Aspose.Pdf Document
- PDF graphics state
- ExtGState dictionary
- CosPdfDictionary usage
language: it
lastmod: 2026-08-14
og_description: Crea un dizionario PDF vuoto in C# con Aspose.Pdf. Segui questa guida
  completa per aggiungere uno stato grafico personalizzato alla collezione ExtGState
  di un PDF.
og_image_alt: Screenshot showing C# code that creates an empty PDF dictionary with
  Aspose.Pdf
og_title: Crea un dizionario PDF vuoto in C# – Guida passo‑passo a Aspose.Pdf
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: Create empty PDF dictionary in C# using Aspose.Pdf – learn how to add
    a graphics state to the ExtGState collection and modify PDFs programmatically.
  headline: Create empty PDF dictionary in C# with Aspose.Pdf
  type: TechArticle
- description: Create empty PDF dictionary in C# using Aspose.Pdf – learn how to add
    a graphics state to the ExtGState collection and modify PDFs programmatically.
  name: Create empty PDF dictionary in C# with Aspose.Pdf
  steps:
  - name: Create a new **Console App** project in Visual Studio.
    text: Create a new **Console App** project in Visual Studio.
  - name: 'Open the **NuGet Package Manager** and install `Aspose.Pdf`:'
    text: 'Open the **NuGet Package Manager** and install `Aspose.Pdf`:'
  - name: 'Add the following `using` directives at the top of `Program.cs`:'
    text: 'Add the following `using` directives at the top of `Program.cs`:'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Crea un dizionario PDF vuoto in C# con Aspose.Pdf
url: /it/net/programming-with-operators/create-empty-pdf-dictionary-in-c-with-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Creare un dizionario PDF vuoto in C# con Aspose.Pdf

Se hai bisogno di **creare oggetti dizionario PDF vuoti** mentre lavori con file PDF, questa guida ti mostra esattamente come farlo in C# usando la libreria Aspose.Pdf. Che tu stia costruendo uno stato grafico personalizzato, aggiungendo una nuova risorsa o preparando un modello per uso futuro, i passaggi seguenti ti forniscono una soluzione completa e pronta all'uso.

Imparerai come caricare un PDF, accedere al dizionario delle risorse della prima pagina, costruire un nuovo `CosPdfDictionary` e inserirlo nella collezione `ExtGState`. Alla fine del tutorial avrai un `output.pdf` funzionante che contiene il dizionario appena creato.

## Prerequisiti

Prima di iniziare, assicurati di avere:

- .NET 6.0 o successivo (il codice funziona anche con .NET Framework 4.6+)
- Visual Studio 2022 o qualsiasi IDE C# tu preferisca
- Una licenza Aspose.Pdf per .NET (o una chiave di valutazione temporanea)
- Un PDF di esempio chiamato **input.pdf** posizionato in una cartella di tua scelta (il percorso della cartella sarà usato come `dataDir`)

Non sono richiesti pacchetti NuGet aggiuntivi oltre a `Aspose.Pdf`.

## Passo 1: Configurare il progetto e fare riferimento ad Aspose.Pdf

1. Crea un nuovo progetto **Console App** in Visual Studio.  
2. Apri il **NuGet Package Manager** e installa `Aspose.Pdf`:

   ```bash
   dotnet add package Aspose.Pdf
   ```

3. Aggiungi le seguenti direttive `using` all'inizio di `Program.cs`:

   ```csharp
   using Aspose.Pdf;
   using Aspose.Pdf.Text;
   using Aspose.Pdf.Operators;
   using Aspose.Pdf.Facades;
   using Aspose.Pdf.InteractiveFeatures;
   using Aspose.Pdf.Xmp;
   using Aspose.Pdf.Operators.Filters;
   using Aspose.Pdf.Operators.Gfx;
   ```

   *Perché questi namespace?* `Aspose.Pdf` contiene la classe core `Document`, mentre `Aspose.Pdf.Operators.Gfx` fornisce `CosPdfDictionary`, `CosPdfNumber` e altri oggetti PDF a basso livello necessari per **creare dizionari PDF vuoti**.

## Passo 2: Caricare il PDF di origine

La prima operazione è caricare il file PDF esistente in un'istanza `Document`. Questo ti dà accesso a tutte le pagine, risorse e dizionari a basso livello.

```csharp
// Step 2: Load the PDF document
string dataDir = @"C:\MyPdfFolder\";               // Change to your folder
using var pdfDocument = new Document(dataDir + "input.pdf");
```

*Spiegazione*: `Document` legge il file in memoria e prepara le strutture interne. L'istruzione `using` garantisce che il handle del file venga rilasciato dopo aver terminato l'elaborazione.

## Passo 3: Accedere al dizionario delle risorse della prima pagina

Ogni pagina PDF ha un dizionario **Resources** che raggruppa font, immagini, oggetti ExtGState e altre risorse condivise. Per inserire un nuovo stato grafico dobbiamo modificare questo dizionario.

```csharp
// Step 3: Get the first page and its Resources dictionary
Page firstPage = pdfDocument.Pages[1];                     // PDF pages are 1‑based
DictionaryEditor resourcesEditor = new DictionaryEditor(firstPage.Resources);
```

`DictionaryEditor` è una classe di supporto che ti permette di trattare un dizionario PDF come un `Dictionary<string, object>` di C#.

## Passo 4: Recuperare (o creare) la collezione ExtGState

`ExtGState` contiene oggetti di stato grafico come opacità, modalità di fusione e larghezza della linea. Se il PDF di origine contiene già una voce `ExtGState`, la riutilizziamo; altrimenti creiamo un nuovo dizionario vuoto.

```csharp
// Step 4: Ensure an ExtGState dictionary exists
CosPdfDictionary extGStateDict;
if (resourcesEditor.ContainsKey("ExtGState"))
{
    extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
}
else
{
    // Create a brand‑new ExtGState dictionary and add it to Resources
    extGStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
    resourcesEditor["ExtGState"] = extGStateDict;
}
```

*Perché questo controllo?* Alcuni PDF omettono completamente la voce `ExtGState`. Gestendo entrambi i casi, il tutorial rimane robusto per qualsiasi file di input.

## Passo 5: **Creare un dizionario PDF vuoto** per un nuovo stato grafico

Ora creiamo effettivamente gli oggetti **dizionario PDF vuoto** che definiscono i parametri dello stato grafico. Il dizionario parte vuoto e aggiungiamo le chiavi richieste:

```csharp
// Step 5: Build a new graphics state dictionary (empty PDF dictionary + entries)
CosPdfDictionary newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

// Stroke opacity (CA) – 1 means fully opaque strokes
newGraphicsState.Add("CA", new CosPdfNumber(1));

// Fill opacity (ca) – 0.5 makes semi‑transparent fills
newGraphicsState.Add("ca", new CosPdfNumber(0.5));

// Blend mode (BM) – "Normal" is the default compositing mode
newGraphicsState.Add("BM", new CosPdfName("Normal"));
```

### Cosa fa ogni voce

| Chiave | Tipo | Significato |
|--------|------|-------------|
| **CA** | `CosPdfNumber` | Opacità del tratto (intervallo 0‑1). |
| **ca** | `CosPdfNumber` | Opacità del riempimento (intervallo 0‑1). |
| **BM** | `CosPdfName`   | Modalità di fusione; `"Normal"` è la più comune. |

Poiché abbiamo iniziato con un **dizionario PDF vuoto**, abbiamo il pieno controllo su quali voci vengono aggiunte. Puoi estendere questo dizionario con ulteriori parametri di stato grafico come `LW` (larghezza linea) o `LC` (cap line) quando necessario.

## Passo 6: Inserire il nuovo stato grafico in ExtGState

Il dizionario `ExtGState` funziona come una mappa dove ogni voce è identificata da un nome (es. `GS0`, `GS1`). Aggiungiamo il nostro dizionario appena creato sotto una chiave unica.

```csharp
// Step 6: Add the graphics state to the ExtGState collection
extGStateDict.Add("GS0", newGraphicsState);
```

Se prevedi di aggiungere più stati, incrementa il suffisso (`GS1`, `GS2`, …) per evitare collisioni di nomi.

## Passo 7: Salvare il PDF modificato

Infine, scrivi le modifiche su disco. Il metodo `Save` serializza automaticamente i dizionari aggiornati.

```csharp
// Step 7: Persist the changes
pdfDocument.Save(dataDir + "output.pdf");
```

Apri `output.pdf` in qualsiasi visualizzatore PDF e ispeziona la voce **Resources → ExtGState** (la maggior parte dei visualizzatori nasconde questa sezione, ma strumenti come Adobe Acrobat Preflight o PDF‑Tron possono rivelarla). Dovresti vedere una voce `GS0` contenente i valori di opacità e modalità di fusione che hai definito.

## Esempio completo funzionante

Riunendo tutti i pezzi, ecco il programma completo che puoi copiare‑incollare in `Program.cs` e eseguire:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Operators.Gfx;

class Program
{
    static void Main()
    {
        // -----------------------------------------------------------------
        // 1️⃣ Load the PDF document
        // -----------------------------------------------------------------
        string dataDir = @"C:\MyPdfFolder\"; // <-- change to your folder
        using var pdfDocument = new Document(dataDir + "input.pdf");

        // -----------------------------------------------------------------
        // 2️⃣ Access the first page’s Resources dictionary
        // -----------------------------------------------------------------
        Page firstPage = pdfDocument.Pages[1];
        var resourcesEditor = new DictionaryEditor(firstPage.Resources);

        // -----------------------------------------------------------------
        // 3️⃣ Retrieve or create the ExtGState dictionary
        // -----------------------------------------------------------------
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

        // -----------------------------------------------------------------
        // 4️⃣ **Create empty PDF dictionary** for a new graphics state
        // -----------------------------------------------------------------
        var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
        newGraphicsState.Add("CA", new CosPdfNumber(1));          // Stroke opacity
        newGraphicsState.Add("ca", new CosPdfNumber(0.5));        // Fill opacity
        newGraphicsState.Add("BM", new CosPdfName("Normal"));    // Blend mode

        // -----------------------------------------------------------------
        // 5️⃣ Add the graphics state to ExtGState
        // -----------------------------------------------------------------
        extGStateDict.Add("GS0", newGraphicsState);

        // -----------------------------------------------------------------
        // 6️⃣ Save the modified PDF
        // -----------------------------------------------------------------
        pdfDocument.Save(dataDir + "output.pdf");

        Console.WriteLine("PDF saved with new empty dictionary at: " + dataDir + "output.pdf");
    }
}
```

**Output previsto** – La console stampa una riga di conferma, e `output.pdf` contiene la nuova voce `GS0` sotto `ExtGState`. Quando renderizzi una pagina che fa riferimento a `GS0` (ad esempio tramite l'operatore di flusso di contenuto `gs`), i tratti saranno completamente opachi mentre i riempimenti saranno trasparenti al 50 %.

## Domande comuni e gestione dei casi limite

| Domanda | Risposta |
|----------|----------|
| *E se il PDF ha più pagine?* | L'esempio si rivolge alla prima pagina (`Pages[1]`). Per influenzare tutte le pagine, itera su `pdfDocument.Pages` e ripeti i passi 3‑5 per le risorse di ciascuna pagina. |
| *Posso aggiungere il dizionario a una pagina che ha già una voce ExtGState chiamata “GS0”?* | Sì, ma devi usare una chiave diversa (`GS1`, `GS2`, …) per non sovrascrivere la voce esistente. |
| *È sicuro modificare il dizionario dopo il salvataggio?* | Dopo aver chiamato `Save`, la rappresentazione in memoria è separata dal file. Puoi continuare a modificare l'oggetto `Document` e chiamare nuovamente `Save` se necessario. |
| *Ho bisogno di una licenza per Aspose.Pdf per usare ` | *(il contenuto originale è troncato; mantenere così)* |

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità aggiuntive dell'API e a esplorare approcci alternativi nei tuoi progetti.

- [How to Create Dashed Lines in PDFs Using Aspose.PDF for .NET&#58; A Step-by-Step Guide](/pdf/english/net/images-graphics/create-dashed-lines-aspose-pdf-net/)
- [How to Remove Graphics from PDFs Using Aspose.PDF .NET&#58; A Complete Guide](/pdf/english/net/images-graphics/remove-graphics-aspose-pdf-net/)
- [How to Create Multi-Layer PDFs Using Aspose.PDF for .NET&#58; A Comprehensive Guide](/pdf/english/net/advanced-features/create-multi-layer-pdfs-aspose-pdf-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}