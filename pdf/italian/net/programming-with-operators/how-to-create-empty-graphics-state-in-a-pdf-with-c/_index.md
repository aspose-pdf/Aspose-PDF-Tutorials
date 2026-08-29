---
category: general
date: 2026-08-17
description: Crea uno stato grafico vuoto in un PDF usando C# e Aspose.Pdf. Segui
  questa guida passo‑passo per modificare in modo sicuro le risorse ExtGState.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create empty graphics state
- Aspose PDF graphics state
- C# modify PDF resources
- add ExtGState dictionary
- PDF page resources editing
language: it
lastmod: 2026-08-17
og_description: Crea uno stato grafico vuoto in un PDF usando C#. Questo tutorial
  mostra come modificare le risorse ExtGState con Aspose.Pdf per modifiche PDF affidabili.
og_image_alt: Screenshot of C# code that adds an empty graphics state to a PDF document
og_title: Crea uno stato grafico vuoto in PDF con C# – guida passo‑a‑passo
schemas:
- author: Aspose
  dateModified: '2026-08-17'
  description: Create empty graphics state in a PDF using C# and Aspose.Pdf. Follow
    this step‑by‑step guide to edit ExtGState resources safely.
  headline: How to create empty graphics state in a PDF with C#
  type: TechArticle
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Come creare uno stato grafico vuoto in un PDF con C#
url: /it/net/programming-with-operators/how-to-create-empty-graphics-state-in-a-pdf-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come creare uno stato grafico vuoto in un PDF con C#

Se devi **creare uno stato grafico vuoto** in un PDF, questa guida ti mostra esattamente come farlo con C# e Aspose.Pdf. Vedrai un esempio completo, eseguibile, che aggiunge una nuova voce al dizionario ExtGState della pagina senza influire sul contenuto esistente.

Lavorare con gli stati grafici PDF è una necessità comune quando vuoi controllare trasparenza, modalità di fusione o altri parametri di rendering su base per‑oggetto. Il codice qui sotto dimostra l'approccio consigliato, spiega perché ogni passaggio è importante e copre le variazioni tipiche che potresti incontrare.

## Prerequisiti

Prima di iniziare, assicurati di avere:

* .NET 6.0 o successivo (il campione compila anche con .NET Core).
* Una licenza Aspose.Pdf per .NET (o una chiave di valutazione temporanea).
* Una cartella che contiene un file `input.pdf` che desideri modificare.
* Familiarità di base con la sintassi C# e i concetti PDF come i dizionari delle risorse.

## Passo 1: Configura il progetto e importa i namespace

Crea una nuova applicazione console o integra il codice in un progetto esistente. Aggiungi il pacchetto NuGet Aspose.Pdf:

```bash
dotnet add package Aspose.Pdf
```

Quindi importa i namespace richiesti:

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Operators;
```

Queste importazioni ti danno accesso alle classi `Document`, `DictionaryEditor` e alle primitive PDF necessarie per **creare uno stato grafico vuoto**.

## Passo 2: Definisci la cartella che contiene i file PDF

```csharp
// Step 1: Define the folder that contains the PDF files
string dataDir = @"C:\PdfSamples\";
```

Sostituisci il percorso con la posizione dei tuoi file PDF. Tenere la directory in una variabile rende il codice riutilizzabile e più facile da testare.

## Passo 3: Carica il documento PDF di origine

```csharp
// Step 2: Load the source PDF document
using (var pdfDocument = new Document(dataDir + "input.pdf"))
{
    // All subsequent operations happen inside this using block
```

Aprire il documento all'interno di un'istruzione `using` garantisce che il handle del file venga rilasciato automaticamente dopo aver salvato le modifiche.

## Passo 4: Accedi alla prima pagina e al suo dizionario Resources

```csharp
    // Step 3: Get the first page and its Resources dictionary
    var firstPage = pdfDocument.Pages[1];
    var resourcesEditor = new DictionaryEditor(firstPage.Resources);
    var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
```

* `Pages[1]` recupera la prima pagina (i numeri di pagina PDF partono da 1).
* `DictionaryEditor` fornisce un modo comodo per leggere e modificare i dizionari PDF.
* La voce `ExtGState` contiene tutti gli oggetti di stato grafico per la pagina. Se la chiave non esiste, Aspose.Pdf crea automaticamente un dizionario vuoto.

## Passo 5: Costruisci un nuovo dizionario di stato grafico vuoto

Lo stato grafico che aggiungi può essere vuoto o pre‑popolato con parametri come opacità (`CA`, `ca`) o modalità di fusione (`BM`). In questo tutorial creiamo uno **stato grafico vuoto** e poi impostiamo alcuni valori tipici per illustrare come funziona il dizionario.

```csharp
    // Step 4: Create a new empty graphics‑state dictionary and set its parameters
    var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
    var parameters = new[]
    {
        new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),   // Stroke opacity
        new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // Fill opacity
        new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // Blend mode
    };
    foreach (var p in parameters)
        newGraphicsState.Add(p);
```

* `CosPdfDictionary.CreateEmptyDictionary` crea un contenitore pulito che puoi riempire con qualsiasi chiave di stato grafico.
* L'aggiunta di `CA`, `ca` e `BM` è opzionale; puoi ometterli se ti serve davvero uno stato vuoto. Il codice mostra come aggiungere voci quando decidi in seguito di controllare il rendering.

## Passo 6: Inserisci il nuovo stato grafico nel dizionario ExtGState

```csharp
    // Step 5: Add the new graphics state to the page's ExtGState dictionary (e.g., name it "GS0")
    extGStateDict.Add("GS0", newGraphicsState);
```

Denominare la voce `"GS0"` segue la convenzione comune di prefissare i nomi degli stati grafici con “GS”. Puoi scegliere qualsiasi nome PDF valido che non confligga con le chiavi esistenti.

## Passo 7: Salva il documento PDF modificato

```csharp
    // Step 6: Save the modified PDF document
    pdfDocument.Save(dataDir + "output.pdf");
}
```

La chiamata `Save` scrive il file aggiornato in `output.pdf`. Aprire questo file in un visualizzatore PDF conferma che il nuovo stato grafico esiste; potrai riferirti ad esso in seguito con l'operatore `gs` nei flussi di contenuto.

### Elenco completo del codice sorgente

Mettendo tutto insieme, il programma completo è così:

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Operators;

class Program
{
    static void Main()
    {
        // Define the folder that contains the PDF files
        string dataDir = @"C:\PdfSamples\";

        // Load the source PDF document
        using (var pdfDocument = new Document(dataDir + "input.pdf"))
        {
            // Get the first page and its Resources dictionary
            var firstPage = pdfDocument.Pages[1];
            var resourcesEditor = new DictionaryEditor(firstPage.Resources);
            var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();

            // Create a new empty graphics‑state dictionary and set its parameters
            var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            var parameters = new[]
            {
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
            };
            foreach (var p in parameters)
                newGraphicsState.Add(p);

            // Add the new graphics state to the page's ExtGState dictionary (name it "GS0")
            extGStateDict.Add("GS0", newGraphicsState);

            // Save the modified PDF document
            pdfDocument.Save(dataDir + "output.pdf");
        }

        Console.WriteLine("Empty graphics state created and saved to output.pdf");
    }
}
```

Eseguendo il programma verrà stampata una riga di conferma e verrà prodotto `output.pdf` con lo stato grafico appena aggiunto.

## Perché questo approccio funziona al meglio

* **Modifica diretta del dizionario** – L'uso di `DictionaryEditor` evita la necessità di analizzare l'intero flusso di contenuto. Modifichi solo le risorse di cui ti interessa.
* **Primitive PDF tipizzate** – `CosPdfNumber`, `CosPdfName` e `CosPdfDictionary` garantiscono che il PDF generato sia conforme alla specifica PDF 1.7.
* **Sicurezza** – Il blocco `using` elimina l'oggetto `Document`, prevenendo blocchi di file che potrebbero corrompere build successive.
* **Estensibilità** – Una volta che lo stato grafico vuoto esiste, puoi riferirti ad esso da qualsiasi operatore di contenuto (`gs`) per cambiare opacità, modalità di fusione o altri parametri per i comandi di disegno selezionati.

## Variazioni comuni e casi limite

| Situazione | Modifica consigliata |
|-----------|-------------------|
| **Pagine multiple** | Esegui un ciclo su `pdfDocument.Pages` e ripeti l'inserimento del dizionario per ogni pagina che devi modificare. |
| **Nessuna voce ExtGState esistente** | `resourcesEditor["ExtGState"]` crea automaticamente un dizionario vuoto se non esiste. Non è necessario alcun codice aggiuntivo. |
| **Nome dello stato grafico diverso** | Sostituisci `"GS0"` con un nome che rispetti la tua convenzione, ad esempio `"MyTransparentState"`. |
| **Aggiungere solo uno stato vuoto** | Ometti l'array `parameters` e il ciclo `foreach`; il dizionario rimarrà vuoto. |
| **Lavorare con PDF criptati** | Fornisci la password quando costruisci `new Document(path, password)` prima di modificare le risorse. |

## Verifica del risultato

Puoi verificare che lo stato grafico sia stato aggiunto ispezionando il PDF con un visualizzatore a basso livello come **PDF‑Tron** o **iText Sharp**. Cerca una voce simile a:

```
/ExtGState << /GS0 << /CA 1 /ca 0.5 /BM /Normal >> >>
```

Se la voce appare, l'operazione **create empty graphics state** è riuscita.

## Conclusione

Ora sai come **creare uno stato grafico vuoto** in un PDF usando C# e Aspose.Pdf. Il tutorial ha coperto ogni passaggio—dal caricamento del documento alla modifica del dizionario `ExtGState` e al salvataggio del risultato—spiegando la logica dietro ogni azione.  

Da qui puoi:

* Usare il nuovo stato grafico nei flussi di contenuto (`gs /GS0`).
* Sperimentare con chiavi aggiuntive come `/SM` (stroke adjustment) o `/OPM` (overprint mode).
* Applicare la stessa tecnica ad altri tipi di risorse come `/XObject` o `/ColorSpace`.

Buon hacking PDF, e sentiti libero di esplorare altri scenari **Aspose PDF graphics state** come cambiamenti dinamici di opacità o modalità di fusione personalizzate!

## Cosa dovresti imparare dopo?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive e a esplorare approcci di implementazione alternativi nei tuoi progetti.

- [How to Create Dashed Lines in PDFs Using Aspose.PDF for .NET&#58; A Step-by-Step Guide](/pdf/english/net/images-graphics/create-dashed-lines-aspose-pdf-net/)
- [How to Remove Graphics from PDFs Using Aspose.PDF .NET&#58; A Complete Guide](/pdf/english/net/images-graphics/remove-graphics-aspose-pdf-net/)
- [Create & Fill Rectangles in PDFs Using Aspose.PDF for .NET&#58; A Step-by-Step Guide](/pdf/english/net/images-graphics/create-fill-rectangle-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}