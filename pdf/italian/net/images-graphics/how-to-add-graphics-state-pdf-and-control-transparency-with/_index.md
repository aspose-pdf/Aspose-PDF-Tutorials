---
category: general
date: 2026-09-05
description: Scopri come aggiungere lo stato grafico PDF usando Aspose.PDF per impostare
  la trasparenza. Questa guida passo passo mostra anche come aggiungere la trasparenza
  al PDF e modificare la trasparenza del PDF in modo efficiente.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add graphics state pdf
- how to add transparency pdf
- modify pdf transparency
language: it
lastmod: 2026-09-05
og_description: Aggiungi lo stato grafico PDF usando Aspose.PDF. Segui questa guida
  per imparare come aggiungere la trasparenza al PDF e modificare la trasparenza del
  PDF in poche righe di codice C#.
og_image_alt: Screenshot of C# code that adds graphics state pdf to a PDF document
og_title: Aggiungi lo stato grafico al PDF con Aspose.PDF – controlla la trasparenza
  in C#
schemas:
- author: Aspose
  dateModified: '2026-09-05'
  description: Learn how to add graphics state pdf using Aspose.PDF to set transparency.
    This step‑by‑step guide also shows how to add transparency pdf and modify pdf
    transparency efficiently.
  headline: How to add graphics state pdf and control transparency with Aspose.PDF
  type: TechArticle
tags:
- Aspose.PDF
- PDF graphics state
- PDF transparency
- C# PDF manipulation
title: Come aggiungere lo stato grafico PDF e controllare la trasparenza con Aspose.PDF
url: /it/net/images-graphics/how-to-add-graphics-state-pdf-and-control-transparency-with/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come aggiungere lo stato grafico PDF e controllare la trasparenza con Aspose.PDF

Se hai bisogno di **aggiungere lo stato grafico PDF** a un documento esistente, questa guida ti mostra i passaggi esatti. Vedrai come aggiungere la trasparenza PDF usando Aspose.PDF per .NET e come modificare la trasparenza PDF senza rompere il layout originale.

Nelle sezioni seguenti percorreremo un esempio completo e eseguibile, spiegheremo perché ogni riga è importante e discuteremo le difficoltà più comuni. Alla fine sarai in grado di incorporare stati grafici personalizzati — come i valori alfa per tratti e riempimenti — in qualsiasi pagina PDF.

## Prerequisiti

Prima di iniziare, assicurati di avere:

* .NET 6.0 o successivo (il codice funziona anche con .NET Framework 4.7+)
* Una licenza valida di Aspose.PDF per .NET o una chiave di valutazione temporanea
* Visual Studio 2022 (o qualsiasi editor C# tu preferisca)
* Un file PDF di input (`input.pdf`) di cui possiedi i diritti di modifica

Non sono necessari pacchetti NuGet aggiuntivi oltre a `Aspose.Pdf`.

## Passo 1: Caricare il documento PDF

La prima operazione è aprire il PDF di origine. Aspose.PDF avvolge il file in un oggetto `Document`, che ti dà accesso a pagine, risorse e strutture PDF a basso livello.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Generator;
using Aspose.Pdf.Operators;
using Aspose.Pdf.Text;
using Aspose.Pdf.Xmp;

string inputPath = @"YOUR_DIRECTORY\input.pdf";

// Open the document inside a using block so resources are released automatically.
using (var doc = new Document(inputPath))
{
    // The rest of the code lives inside this block.
}
```

**Perché è importante:** Aprire il file con un'istruzione `using` garantisce che il handle del file venga chiuso anche in caso di eccezione. L'oggetto `Document` carica anche la tabella di cross‑reference, consentendoci di modificare i dizionari a basso livello in seguito.

## Passo 2: Accedere al dizionario delle risorse della prima pagina

Ogni pagina PDF ha un dizionario *Resources* che memorizza font, XObject e stati grafici (`ExtGState`). Per inserire un nuovo stato grafico, recuperiamo prima questo dizionario.

```csharp
// Inside the using block
Page page = doc.Pages[1];                     // Get the first page (pages are 1‑based)
var dictEditor = new DictionaryEditor(page.Resources);
var extGState = dictEditor["ExtGState"].ToCosPdfDictionary();
```

**Perché è importante:** `ExtGState` è la chiave sotto la quale sono memorizzati gli oggetti di stato grafico. Se la pagina non contiene ancora una voce `ExtGState`, Aspose.PDF crea automaticamente un dizionario vuoto, quindi il codice funziona in entrambi i casi.

## Passo 3: Creare un nuovo dizionario di stato grafico

Un dizionario di stato grafico definisce come si comportano le operazioni di disegno. Per la trasparenza abbiamo bisogno di `CA` (alpha del tratto), `ca` (alpha del riempimento) e, facoltativamente, della modalità di fusione (`BM`). Il codice qui sotto costruisce quel dizionario.

```csharp
// Create an empty COS dictionary that will become our new graphics state.
CosPdfDictionary newGs = CosPdfDictionary.CreateEmptyDictionary(doc);

// Define the entries we want: 1.0 stroke opacity, 0.5 fill opacity, Normal blend mode.
var entries = new[]
{
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),   // stroke alpha (fully opaque)
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),   // fill alpha (50 % transparent)
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // blend mode
};

foreach (var entry in entries)
{
    newGs.Add(entry);
}
```

**Perché è importante:**  
* `CA` controlla l'opacità dei percorsi tracciati (linee, bordi).  
* `ca` controlla l'opacità degli oggetti riempiti (forme, testo).  
* `BM` seleziona la modalità di fusione; “Normal” è la più comune e funziona con tutti i visualizzatori PDF.

### Caso limite: voce `ExtGState` mancante

Se `page.Resources` non contiene un dizionario `ExtGState`, `dictEditor["ExtGState"]` restituisce `null`. In quella situazione puoi crearlo manualmente:

```csharp
if (extGState == null)
{
    extGState = CosPdfDictionary.CreateEmptyDictionary(doc);
    dictEditor["ExtGState"] = extGState;
}
```

L'inclusione di questa verifica rende il tutorial robusto per PDF che non hanno mai usato uno stato grafico personalizzato.

## Passo 4: Aggiungere il nuovo stato grafico al dizionario delle risorse

Ora associamo il dizionario appena creato a un nome (ad es., `GS0`). I flussi di contenuto possono fare riferimento a questo nome per applicare la trasparenza definita.

```csharp
// Register the new graphics state under the name "GS0"
extGState.Add("GS0", newGs);
```

**Perché è importante:** Gli operatori di contenuto PDF come `gs` passano a uno stato grafico nominato. Aggiungendo `GS0`, abiliti i flussi di contenuto successivi a usare ` /GS0 gs ` per attivare le impostazioni di trasparenza.

## Passo 5: (Opzionale) Applicare lo stato grafico al contenuto esistente

Se desideri che gli elementi già presenti nella pagina diventino trasparenti, puoi anteporre un operatore `gs` al flusso di contenuto della pagina. Questo passaggio è opzionale perché molti casi d'uso richiedono lo stato grafico solo per gli oggetti aggiunti successivamente.

```csharp
// Prepend "GS0" graphics state to the page’s content
page.Contents.Insert(0, new OperatorGraphicsState("GS0"));
```

**Perché è importante:** Senza questa riga la pagina manterrà il suo aspetto originale. Aggiungere l'operatore assicura che tutto ciò che viene disegnato dopo erediti i nuovi valori di opacità.

## Passo 6: Salvare il PDF modificato

Infine, scrivi il documento aggiornato su disco. Puoi sovrascrivere il file originale o scrivere in una nuova posizione.

```csharp
string outputPath = @"YOUR_DIRECTORY\output.pdf";
doc.Save(outputPath);
```

**Perché è importante:** `doc.Save` serializza la tabella di cross‑reference modificata, i dizionari delle risorse e i nuovi flussi di contenuto, producendo un PDF valido che qualsiasi visualizzatore può aprire.

## Esempio completo funzionante

Unendo tutti i pezzi, ecco un programma autonomo che puoi copiare, incollare ed eseguire.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Operators;
using Aspose.Pdf.Xmp;
using Aspose.Pdf.Text;
using Aspose.Pdf.Generator;
using Aspose.Pdf.Cos;

class AddGraphicsStateExample
{
    static void Main()
    {
        // -----------------------------------------------------------------
        // 1️⃣ Load the PDF document
        // -----------------------------------------------------------------
        string inputPath = @"YOUR_DIRECTORY\input.pdf";
        using (var doc = new Document(inputPath))
        {
            // -----------------------------------------------------------------
            // 2️⃣ Access the first page's resource dictionary
            // -----------------------------------------------------------------
            Page page = doc.Pages[1];
            var dictEditor = new DictionaryEditor(page.Resources);
            var extGState = dictEditor["ExtGState"]?.ToCosPdfDictionary();

            // Ensure ExtGState exists
            if (extGState == null)
            {
                extGState = CosPdfDictionary.CreateEmptyDictionary(doc);
                dictEditor["ExtGState"] = extGState;
            }

            // -----------------------------------------------------------------
            // 3️⃣ Create a new graphics state (transparency settings)
            // -----------------------------------------------------------------
            CosPdfDictionary newGs = CosPdfDictionary.CreateEmptyDictionary(doc);
            var entries = new[]
            {
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),   // stroke opacity
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),   // fill opacity
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
            };
            foreach (var entry in entries) newGs.Add(entry);

            // -----------------------------------------------------------------
            // 4️⃣ Register the graphics state as "GS0"
            // -----------------------------------------------------------------
            extGState.Add("GS0", newGs);

            // -----------------------------------------------------------------
            // 5️⃣ (Optional) Apply the graphics state to existing content
            // -----------------------------------------------------------------
            page.Contents.Insert(0, new OperatorGraphicsState("GS0"));

            // -----------------------------------------------------------------
            // 6️⃣ Save the modified PDF
            // -----------------------------------------------------------------
            string outputPath = @"YOUR_DIRECTORY\output.pdf";
            doc.Save(outputPath);
            Console.WriteLine($"PDF saved with new graphics state at: {outputPath}");
        }
    }
}
```

### Output previsto

Dopo aver eseguito il programma, apri `output.pdf` in Adobe Acrobat Reader o in qualsiasi visualizzatore PDF. Qualsiasi forma riempita (ad es., rettangoli colorati) nella prima pagina dovrebbe apparire al **50 % di opacità**, mentre i tratti rimangono completamente opachi. Se hai aggiunto l'operatore `gs` opzionale, *tutto* il contenuto esistente su quella pagina erediterà la stessa trasparenza.

## Domande comuni e risoluzione dei problemi

| Domanda | Risposta |
|----------|----------|
| **Posso aggiungere più di uno stato grafico?** | Sì. Crea dizionari aggiuntivi (ad es., `GS1`, `GS2`) e riferiscili con operatori `gs` diversi. |
| **E se il PDF utilizza già un nome come `GS0`?** | Scegli un nome univoco (ad es., `MyGS`) o controlla le chiavi esistenti con `extGState.Keys`. |
| **Funziona con PDF criptati?** | Il documento deve essere aperto con la password corretta. Usa `new Document(inputPath, new LoadOptions { Password = "pwd" })`. |
| **Le modifiche influenzeranno altre pagine?** | No. Lo stato grafico viene aggiunto alle risorse della pagina che modifichi. Per influenzare tutte le pagine, ripeti il processo per ciascuna pagina o aggiungi il dizionario alle risorse a livello *documento*. |
| **C'è un impatto sulle prestazioni?** | Aggiungere un singolo stato grafico è trascurabile. PDF di grandi dimensioni con molte pagine potrebbero richiedere un ciclo, ma l'operazione resta O(numero di pagine). |

## Consigli professionali

* **Riutilizzare gli stati grafici:** Se hai bisogno della stessa trasparenza su più pagine, aggiungi il dizionario alle risorse del *documento* (`doc.Resources`) e riferiscilo da ciascuna pagina. Questo riduce le dimensioni del file.  
* **Modalità di fusione:** Sperimenta con altri valori `BM` come `Multiply`, `Screen` o `Overlay` per effetti creativi. Non tutti i visualizzatori supportano ogni modalità di fusione, quindi testa con il tuo pubblico di destinazione.  
* **Test:** Confronta sempre i PDF originali e modificati fianco a fianco. Usa uno strumento di diff che possa renderizzare PDF (ad es., `DiffPDF`) per verificare che siano state apportate solo le modifiche previste.

## Prossimi passi

Ora che sai **come aggiungere la trasparenza PDF** e **modificare la trasparenza PDF**, puoi approfondire argomenti correlati:

* **Aggiungere lo stato grafico PDF** per effetti di sovrastampa e mezzitoni  
* **Incorporare immagini con opacità personalizzata** usando `ImageFragment` e uno stato grafico  
* **Elaborazione batch** di più PDF in una cartella con parallelismo per migliorare il throughput  
* **Usare l'API di alto livello di Aspose.PDF** (`PdfSaveOptions`, `PdfPageEditor`) per flussi di lavoro più complessi  

Sentiti libero di sperimentare con valori alfa diversi.


## Cosa dovresti imparare dopo?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi con spiegazioni passo‑passo per aiutarti a padroneggiare ulteriori funzionalità dell'API e a esplorare approcci alternativi nei tuoi progetti.

- [Aggiungere trasparenza a PDF usando Aspose – Guida completa C#](/pdf/english/net/programming-with-operators/add-transparency-to-pdf-using-aspose-complete-c-guide/)
- [Come aggiungere un timbro di testo a PDF usando Aspose.PDF .NET&#58; Guida completa](/pdf/english/net/watermarks-backgrounds/add-text-stamp-pdf-aspose-pdf-dotnet/)
- [Come aggiungere immagini a PDF usando Aspose.PDF per .NET&#58; Guida passo passo](/pdf/english/net/images-graphics/add-images-to-pdfs-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}