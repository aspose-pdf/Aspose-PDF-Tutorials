---
category: general
date: 2026-10-07
description: Aggiungi lo stato grafico PDF usando Aspose.Pdf in C# per modificare
  la trasparenza del PDF. Segui questa guida passo passo per incorporare stati grafici
  personalizzati e controllare l'opacità.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add graphics state pdf
- modify pdf transparency
language: it
lastmod: 2026-10-07
og_description: Aggiungi lo stato grafico PDF con Aspose.Pdf in C#. Scopri come modificare
  la trasparenza del PDF creando un dizionario di stato grafico personalizzato.
og_image_alt: Screenshot showing the add graphics state pdf code editor in Visual
  Studio
og_title: Aggiungi stato grafico PDF con Aspose.Pdf – controlla la trasparenza del
  PDF
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Add graphics state pdf using Aspose.Pdf in C# to modify PDF transparency.
    Follow this step‑by‑step guide to embed custom graphics states and control opacity.
  headline: Add graphics state pdf with Aspose.Pdf in C#
  type: TechArticle
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Aggiungi lo stato grafico PDF con Aspose.Pdf in C#
url: /it/net/images-graphics/add-graphics-state-pdf-with-aspose-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aggiungere lo stato grafico PDF con Aspose.Pdf in C#

Se hai bisogno di **add graphics state pdf** a un documento, questo tutorial ti mostra esattamente come farlo con Aspose.Pdf per .NET. Alla fine della guida saprai anche come **modify PDF transparency**, consentendoti di impostare valori di opacità personalizzati su qualsiasi operazione di disegno.

Lavorare con gli stati grafici PDF ti consente di controllare parametri come lo spessore della linea, la modalità di fusione e, soprattutto per questo articolo, la trasparenza del contenuto. I passaggi seguenti sono scritti per sviluppatori che hanno dimestichezza con C# e desiderano una soluzione pronta all'uso senza dover scavare nella documentazione ufficiale dell'SDK.

## Cosa imparerai

* Come creare un nuovo dizionario di stato grafico e popolarlo con le voci `CA`, `ca` e `BM`.  
* Come inserire quel dizionario nella risorsa `ExtGState` della pagina affinché il PDF lo riconosca.  
* Come i valori `ca` (tratto) e `CA` (riempimento) influenzano **modify PDF transparency** per i comandi di disegno successivi.  
* Problemi comuni come collisioni di nomi e compatibilità di versione, più consigli professionali per estendere lo stato grafico in seguito.

**Prerequisiti**

* .NET 6.0 o versioni successive (il codice funziona anche con .NET Framework 4.7+).  
* Una licenza valida di Aspose.Pdf per .NET (la valutazione gratuita funziona per i test).  
* Visual Studio 2022 o qualsiasi IDE C# tu preferisca.

---

## Passo 1: Installare Aspose.Pdf per .NET

Add the NuGet package to your project:

```bash
dotnet add package Aspose.Pdf
```

Il pacchetto include lo spazio dei nomi `Aspose.Pdf` che fornisce le classi `Document`, `DictionaryEditor` e `CosPdfDictionary` utilizzate più avanti.

> **Consiglio professionale:** Se prevedi di elaborare molti PDF in batch, abilita la **License** subito in `Program.cs` per evitare la filigrana di valutazione.

```csharp
// Apply your license (optional for evaluation)
Aspose.Pdf.License license = new Aspose.Pdf.License();
license.SetLicense("Aspose.Pdf.lic");
```

## Passo 2: Definire i percorsi di input e output

Devi indicare all'SDK un PDF esistente (`input.pdf`) e specificare dove salvare il file modificato (`output.pdf`).

```csharp
// Define input and output PDF file paths
string inputPath = @"C:\MyPdfs\input.pdf";
string outputPath = @"C:\MyPdfs\output.pdf";
```

> **Perché è importante:** L'uso di percorsi assoluti impedisce all'SDK di cercare nella directory di lavoro sbagliata, una causa comune di `FileNotFoundException`.

## Passo 3: Aprire il PDF e individuare le risorse della prima pagina

Il dizionario `ExtGState` si trova all'interno del dizionario delle risorse di ogni pagina. Modificheremo la prima pagina per semplicità, ma lo stesso approccio funziona per qualsiasi indice di pagina.

```csharp
using (var pdfDocument = new Aspose.Pdf.Document(inputPath))
{
    // Get the first page (pages are 1‑based)
    var firstPage = pdfDocument.Pages[1];

    // Access the page’s resource dictionary via DictionaryEditor
    var resourcesEditor = new Aspose.Pdf.DictionaryEditor(firstPage.Resources);

    // Retrieve (or create) the ExtGState entry
    var extGStateDict = resourcesEditor["ExtGState"]
        .ToCosPdfDictionary(); // Throws if ExtGState does not exist
```

**Caso limite:** Se la pagina non ha una voce `ExtGState`, è necessario crearla:

```csharp
if (!resourcesEditor.ContainsKey("ExtGState"))
{
    var emptyDict = Aspose.Pdf.CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
    resourcesEditor.Add("ExtGState", emptyDict);
    extGStateDict = emptyDict;
}
```

## Passo 4: Creare un nuovo dizionario di stato grafico

Uno stato grafico è una collezione di coppie chiave/valore che descrivono il comportamento delle operazioni di disegno. Per la trasparenza abbiamo bisogno di tre chiavi:

| Chiave | Significato | Valore tipico |
|-----|---------|---------------|
| `CA` | Opacità di riempimento (0 = trasparente, 1 = opaco) | `1` (completamente opaco) |
| `ca` | Opacità del tratto (stessa scala) | `0.5` (50 % trasparente) |
| `BM` | Modalità di fusione (es., `Normal`, `Multiply`) | `Normal` |

```csharp
    // Create an empty dictionary that will hold the graphics state
    var newGraphicsState = Aspose.Pdf.CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

    // Populate the dictionary with transparency and blend mode entries
    var graphicsStateEntries = new[]
    {
        new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
            "CA", new Aspose.Pdf.CosPdfNumber(1)),
        new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
            "ca", new Aspose.Pdf.CosPdfNumber(0.5)),
        new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
            "BM", new Aspose.Pdf.CosPdfName("Normal"))
    };

    foreach (var entry in graphicsStateEntries)
        newGraphicsState.Add(entry);
```

**Perché questi valori?**  
`ca = 0.5` fa sì che qualsiasi percorso tracciato (linee, bordi) appaia al 50 % di opacità, mentre `CA = 1` mantiene le forme riempite completamente opache. Regola entrambi i numeri per ottenere l'effetto di **modify PDF transparency** desiderato.

## Passo 5: Inserire lo stato grafico nel dizionario ExtGState

Devi assegnare al nuovo stato un nome univoco (es., `GS0`). Se il nome esiste già, Aspose.Pdf sovrascriverà la voce esistente, il che potrebbe rompere altri contenuti che vi fanno affidamento.

```csharp
    // Add the new graphics state under a custom name
    const string stateName = "GS0";

    // Ensure we don’t clash with an existing entry
    if (extGStateDict.ContainsKey(stateName))
        extGStateDict.Remove(stateName);

    extGStateDict.Add(stateName, newGraphicsState);
```

Ora le risorse della pagina conoscono `GS0`. Per usarlo effettivamente, dovresti fare riferimento allo stato grafico in un flusso di contenuti tramite l'operatore `gs` (es., `GS0 gs`). Aspose.Pdf ti permette di iniettare operatori PDF grezzi se hai bisogno di disegnare forme personalizzate.

## Passo 6: Salvare il PDF modificato

```csharp
    // Persist the changes to a new file
    pdfDocument.Save(outputPath);
}
```

Il `output.pdf` risultante contiene lo stesso contenuto visivo dell'originale, ma qualsiasi comando di disegno successivo che selezioni `GS0` rispetterà le impostazioni di trasparenza che hai definito.

### Risultato atteso

Apri `output.pdf` in Adobe Acrobat o in qualsiasi visualizzatore PDF. Se aggiungi una nuova linea tracciata usando lo stato grafico `GS0` (es., tramite `pdfDocument.Pages[1].Contents.Add(...)`), la linea apparirà semi‑trasparente mentre i riempimenti rimarranno opachi. Questo dimostra che hai aggiunto correttamente **add graphics state pdf** e **modify PDF transparency**.

---

## Esempio completo eseguibile

Di seguito trovi il programma completo che puoi copiare‑incollare in un'applicazione console. Include il caricamento della licenza, la gestione degli errori e commenti che spiegano ogni passaggio non ovvio.



## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità aggiuntive dell'API ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Aggiungere trasparenza a PDF con Aspose PDF in C# – Guida passo‑passo](/pdf/english/net/images-graphics/add-transparency-to-pdf-with-aspose-pdf-in-c-step-by-step-gu/)
- [Aggiungere trasparenza a PDF usando Aspose – Guida completa C#](/pdf/english/net/programming-with-operators/add-transparency-to-pdf-using-aspose-complete-c-guide/)
- [Come aggiungere un timbro immagine a un PDF usando Aspose.PDF per .NET: Guida completa](/pdf/english/net/images-graphics/add-image-stamp-pdf-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}