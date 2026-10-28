---
category: general
date: 2026-08-08
description: Aggiungi numerazione Bates a un PDF usando Aspose.Pdf in C#. Questo tutorial
  mostra anche come aggiungere una pagina vuota a un PDF e generare PDF programmaticamente.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add bates numbering pdf
- add blank page pdf
- generate pdf programmatically
- create pdf aspose
language: it
lastmod: 2026-08-08
og_description: Aggiungi la numerazione Bates a un PDF con Aspose.Pdf in C#. Impara
  ad aggiungere una pagina vuota al PDF, generare PDF programmaticamente e salvare
  il documento finale in pochi minuti.
og_image_alt: Screenshot of C# code adding Bates numbering and a blank page to a PDF
  using Aspose.Pdf
og_title: Aggiungi numerazione Bates a PDF con Aspose – guida completa C#
schemas:
- author: Aspose
  dateModified: '2026-08-08'
  description: Add bates numbering pdf using Aspose.Pdf in C#. This tutorial also
    shows how to add blank page pdf and generate pdf programmatically.
  headline: Add bates numbering pdf with Aspose – step‑by‑step guide
  type: TechArticle
- description: Add bates numbering pdf using Aspose.Pdf in C#. This tutorial also
    shows how to add blank page pdf and generate pdf programmatically.
  name: Add bates numbering pdf with Aspose – step‑by‑step guide
  steps:
  - name: What if I need a different font or position?
    text: 'The `BatesNumberingArtifact` exposes properties such as `FontSize`, `FontColor`,
      `HorizontalAlignment`, and `VerticalAlignment`. For example:'
  - name: How do I exclude a specific page from numbering?
    text: Create a separate `BatesNumberingArtifact` for the pages you want to number
      and add it only to those pages. Pages without an attached artifact will remain
      unnumbered.
  - name: Does this work with existing PDFs?
    text: 'Yes. Instead of `new Document()`, load an existing file:'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF generation
- Bates numbering
title: Aggiungi la numerazione Bates a PDF con Aspose – guida passo passo
url: /it/net/programming-with-pdf-pages/add-bates-numbering-pdf-with-aspose-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aggiungere numerazione Bates PDF con Aspose – guida passo‑passo

Aggiungere numerazione Bates PDF con Aspose.Pdf è semplice una volta compresi i passaggi fondamentali. Se hai anche bisogno di aggiungere una pagina vuota PDF o generare PDF programmaticamente, questa guida copre tutto ciò di cui hai bisogno.

In questo tutorial imparerai a:

* Creare un nuovo documento PDF da zero.  
* Aggiungere una pagina vuota PDF che ospiterà i numeri Bates.  
* Configurare l’artefatto di numerazione Bates con un prefisso personalizzato.  
* Salvare il PDF in modo che i numeri compaiano nel file generato.  

Al termine avrai un’applicazione console C# completamente funzionante che produce un PDF contenente numeri Bates come **CASE‑1000**, **CASE‑1001**, … – un requisito comune per i flussi di lavoro legali e di e‑discovery.

## Prerequisiti

* .NET 6.0 SDK o versioni successive (il codice funziona anche con .NET Framework 4.8).  
* Visual Studio 2022 o qualsiasi IDE compatibile con C#.  
* Una licenza valida di Aspose.Pdf per .NET (o una chiave di valutazione gratuita).  
* Familiarità di base con la sintassi C#.

> **Suggerimento:** Se esegui il codice senza licenza, Aspose aggiungerà una piccola filigrana al PDF di output.

## Passo 1: Configurare il progetto e importare Aspose.Pdf

Crea un nuovo progetto console e aggiungi il pacchetto NuGet Aspose.Pdf:

```bash
dotnet new console -n BatesNumberingDemo
cd BatesNumberingDemo
dotnet add package Aspose.Pdf
```

Le direttive `using` necessarie per l’esempio sono:

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Artifacts;
```

Questi namespace ti danno accesso alle classi `Document`, `Page` e `BatesNumberingArtifact` utilizzate più avanti.

## Passo 2: Aggiungere una pagina vuota PDF

Un numero Bates deve essere associato a una pagina, quindi creiamo prima una pagina vuota che riceverà l’artefatto di numerazione.

```csharp
// Step 2: Add a blank page pdf
Document pdfDocument = new Document();          // creates an empty PDF
Page pdfPage = pdfDocument.Pages.Add();         // adds the first (blank) page
```

La classe `Document` rappresenta l’intero file PDF, mentre `Pages.Add()` inserisce una nuova pagina vuota alla fine della collezione di pagine del documento. Poiché il documento parte vuoto, questa chiamata crea anche la prima pagina.

## Passo 3: Configurare l’artefatto di numerazione Bates

Ora definiamo come dovranno apparire i numeri Bates. Il `BatesNumberingArtifact` ti consente di impostare il numero iniziale, il prefisso, il suffisso e le opzioni di formattazione.

```csharp
// Step 3: Define Bates numbering settings
BatesNumberingArtifact batesArtifact = new BatesNumberingArtifact(pdfPage)
{
    StartNumber = 1000,          // first number in the sequence
    Prefix = "CASE-",            // custom prefix before each number
    // Optional: you can also set Suffix, FontSize, FontColor, etc.
};
```

**Perché è importante:**  
Impostare `StartNumber` a **1000** corrisponde alle convenzioni tipiche dei fascicoli legali. Il `Prefix` garantisce che ogni numero appaia come **CASE‑1000**, **CASE‑1001**, …, rendendo più semplice la ricerca e l’ordinamento.

## Passo 4: Allegare l’artefatto alla pagina

L’artefatto deve essere aggiunto alla collezione `Artifacts` della pagina affinché Aspose lo renderizzi su ogni pagina durante il salvataggio.

```csharp
// Step 4: Attach the Bates numbering artifact to the PDF page
pdfPage.Artifacts.Add(batesArtifact);
```

Quando il documento viene salvato, Aspose ripete automaticamente l’artefatto su tutte le pagine, incrementando il numero per ciascuna pagina successiva.

## Passo 5: (Facoltativo) Aggiungere pagine aggiuntive

Se ti servono più pagine, ripeti semplicemente `pdfDocument.Pages.Add()`. L’artefatto di numerazione Bates che hai allegato nel passaggio precedente apparirà automaticamente su ogni nuova pagina.

```csharp
// Example: add two more pages
pdfDocument.Pages.Add();
pdfDocument.Pages.Add();
```

## Passo 6: Salvare il PDF – generare PDF programmaticamente

Infine, persisti il documento su disco. È in questo momento che i numeri Bates vengono renderizzati sulle pagine.

```csharp
// Step 6: Save the PDF – generate pdf programmatically
string outputPath = Path.Combine(
    Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
    "BatesNumberedDocument.pdf");

// Ensure the directory exists
Directory.CreateDirectory(Path.GetDirectoryName(outputPath)!);

pdfDocument.Save(outputPath);
Console.WriteLine($"PDF saved to: {outputPath}");
```

**Risultato atteso:**  
Apri *BatesNumberedDocument.pdf* e vedrai un PDF di tre pagine. Ogni pagina mostra un numero Bates nell’angolo in basso a destra:

* Pagina 1 → **CASE‑1000**  
* Pagina 2 → **CASE‑1001**  
* Pagina 3 → **CASE‑1002**

I numeri vengono incrementati automaticamente perché l’artefatto è collegato alla collezione di pagine.

## Esempio completo, eseguibile

Mettendo tutto insieme, ecco un programma console completo che puoi copiare, incollare ed eseguire:

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Artifacts;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main()
        {
            // Create a new PDF document
            Document pdfDocument = new Document();

            // Add a blank page pdf
            Page pdfPage = pdfDocument.Pages.Add();

            // Define Bates numbering settings (add bates numbering pdf)
            BatesNumberingArtifact batesArtifact = new BatesNumberingArtifact(pdfPage)
            {
                StartNumber = 1000,
                Prefix = "CASE-"
            };

            // Attach the artifact to the page
            pdfPage.Artifacts.Add(batesArtifact);

            // (Optional) add more pages to see incremented numbers
            pdfDocument.Pages.Add(); // page 2
            pdfDocument.Pages.Add(); // page 3

            // Save the PDF – generate pdf programmatically
            string outputPath = Path.Combine(
                Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
                "BatesNumberedDocument.pdf");

            Directory.CreateDirectory(Path.GetDirectoryName(outputPath)!);
            pdfDocument.Save(outputPath);

            Console.WriteLine($"PDF saved to: {outputPath}");
        }
    }
}
```

Esegui il programma con `dotnet run`. Dopo l’esecuzione, individua il file sul desktop e verifica i numeri Bates.

![Esempio di aggiunta numerazione Bates PDF](/images/bates-numbering.png "Add bates numbering pdf example")

## Domande comuni e casi particolari

### E se avessi bisogno di un font o di una posizione diversi?

Il `BatesNumberingArtifact` espone proprietà come `FontSize`, `FontColor`, `HorizontalAlignment` e `VerticalAlignment`. Ad esempio:

```csharp
batesArtifact.FontSize = 12;
batesArtifact.FontColor = Color.Blue;
batesArtifact.HorizontalAlignment = HorizontalAlignment.Left;
batesArtifact.VerticalAlignment = VerticalAlignment.Top;
```

### Come escludere una pagina specifica dalla numerazione?

Crea un `BatesNumberingArtifact` separato per le pagine che desideri numerare e aggiungilo solo a quelle pagine. Le pagine senza artefatto allegato rimarranno non numerate.

### Funziona con PDF esistenti?

Sì. Invece di `new Document()`, carica un file esistente:

```csharp
Document pdfDocument = new Document("input.pdf");
```

Quindi allega l’artefatto alle pagine desiderate e salva.

## Conclusione

Ora sai come **aggiungere numerazione Bates PDF** usando Aspose.Pdf, come **aggiungere una pagina vuota PDF** e come **generare PDF programmaticamente** in una soluzione C# pulita e riutilizzabile. L’approccio funziona con qualsiasi numero di pagine, prefissi personalizzati e opzioni di stile, offrendoti il pieno controllo sul documento finale.

Prossimi passi che potresti esplorare:

* Usa **create pdf as

## Cosa dovresti imparare dopo?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità aggiuntive dell’API e a esplorare approcci di implementazione alternativi nei tuoi progetti.

- [How to Add and Customize Page Numbers in PDFs Using Aspose.PDF for .NET | Document Manipulation Guide](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [How to Add an Empty Page at the End of a PDF Using Aspose.PDF for .NET | Step-by-Step Guide](/pdf/english/net/document-manipulation/add-empty-page-end-pdf-aspose-pdf-net/)
- [Create PDF Document with Aspose.PDF – Add Page, Shape & Save](/pdf/english/net/document-creation/create-pdf-document-with-aspose-pdf-add-page-shape-save/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}