---
category: general
date: 2026-09-27
description: Aggiungi la numerazione Bates a un PDF usando Aspose.PDF in C#. Scopri
  come caricare un documento PDF, impostare le opzioni di numerazione Bates e salvare
  il file aggiornato.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add bates numbering
- load pdf document
- how to add bates numbering
- Aspose.PDF C#
- PDF Bates numbering example
language: it
lastmod: 2026-09-27
og_description: Aggiungi la numerazione Bates a un PDF usando Aspose.PDF in C#. Questo
  tutorial ti mostra come caricare un documento PDF, configurare la numerazione Bates
  e salvare il risultato.
og_image_alt: Screenshot of a PDF page displaying Bates numbers in the footer
og_title: Aggiungi la numerazione Bates al PDF con Aspose.PDF – Guida C#
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Add bates numbering to PDF using Aspose.PDF in C#. Learn how to load
    a PDF document, set Bates numbering options, and save the updated file.
  headline: Add bates numbering to PDF using Aspose.PDF in C#
  type: TechArticle
tags:
- Aspose.PDF
- C#
- PDF processing
title: Aggiungi la numerazione Bates a PDF usando Aspose.PDF in C#
url: /it/net/programming-with-text/add-bates-numbering-to-pdf-using-aspose-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aggiungere la numerazione Bates a PDF usando Aspose.PDF in C#

Se hai bisogno di **aggiungere la numerazione Bates** a un file PDF, questa guida ti mostra una soluzione completa, pronta all'uso. Vedrai come **caricare un documento PDF**, configurare le opzioni di numerazione Bates e scrivere il file numerato su disco, tutto con Aspose.PDF per .NET.

L'applicazione dei numeri Bates è comune nei flussi di lavoro legali, delle forze dell'ordine e di archiviazione. Alla fine di questo tutorial potrai inserire un identificatore sequenziale su ogni pagina, personalizzare il prefisso e avviare il conteggio a qualsiasi numero tu scelga.

## Cosa imparerai

* Come **caricare il contenuto di un documento PDF** in un oggetto `Aspose.Pdf.Document`.  
* I passaggi esatti **per aggiungere la numerazione Bates** con `BatesNumberingOptions`.  
* Come salvare il file modificato mantenendo il layout e la qualità originali.  

Non sono richiesti strumenti esterni—solo il pacchetto NuGet Aspose.PDF e un ambiente di sviluppo .NET (Visual Studio, VS Code o Rider).  

---

## Passo 1: Installare Aspose.PDF per .NET

Apri la cartella del tuo progetto in un terminale ed esegui:

```bash
dotnet add package Aspose.PDF
```

Il pacchetto include lo spazio dei nomi `Aspose.Pdf`, che fornisce tutte le classi usate in questo tutorial. Dopo l'installazione, ricarica il progetto affinché l'IDE rilevi il nuovo riferimento.

## Passo 2: Caricare il documento PDF

Caricare il file di origine è la prima operazione perché il motore di numerazione Bates funziona su un'istanza `Document` esistente.

```csharp
using Aspose.Pdf;

// ...

// Replace with the path to your input PDF
string inputPath = @"YOUR_DIRECTORY\input.pdf";

// Load the PDF document into memory
Document doc = new Document(inputPath);
```

**Perché è importante:** La classe `Document` analizza la struttura del PDF, fornendoti l'accesso a pagine, annotazioni e metadati. Senza caricare prima il file, non è possibile applicare alcuna numerazione.

## Passo 3: Configurare le opzioni di numerazione Bates

Crea un oggetto `BatesNumberingOptions` e imposta il prefisso desiderato, il numero di partenza e i parametri di formattazione opzionali.

```csharp
using Aspose.Pdf;

// ...

BatesNumberingOptions batesOptions = new BatesNumberingOptions
{
    // Text that appears before the numeric part
    Prefix = "CASE01",

    // First number to use (1 means the first page gets CASE01-1)
    StartNumber = 1,

    // Optional: customize the appearance
    // The default places the number in the footer, centered.
    // You can change Font, FontSize, Color, and Position if needed.
    // Example:
    // Font = FontRepository.FindFont("Arial"),
    // FontSize = 10,
    // Color = Color.Black,
    // Margin = new Margin(0, 0, 0, 20)
};
```

**Perché è importante:** `BatesNumberingOptions` indica ad Aspose.PDF come generare l'etichetta per ogni pagina. Il `Prefix` ti aiuta a raggruppare casi correlati, mentre `StartNumber` ti consente di continuare una sequenza da un batch precedente.

## Passo 4: Salvare il PDF con i numeri Bates applicati

Passa l'oggetto delle opzioni al metodo `Save`. Aspose.PDF scrive i numeri direttamente su ogni pagina.

```csharp
// Replace with the desired output path
string outputPath = @"YOUR_DIRECTORY\output.pdf";

// Save the document, applying the Bates numbering
doc.Save(outputPath, batesOptions);
```

**Perché è importante:** La sovraccarico `Save(string, BatesNumberingOptions)` combina il passaggio di rendering con il processo di numerazione, garantendo che il file di output contenga gli identificatori visibili.

## Esempio completo – tutto insieme

Di seguito trovi un unico programma autonomo che puoi copiare, incollare ed eseguire. Dimostra **come aggiungere la numerazione Bates** dall'inizio alla fine.

```csharp
using System;
using Aspose.Pdf;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the PDF document
            string inputPath = @"YOUR_DIRECTORY\input.pdf";
            Document doc = new Document(inputPath);

            // 2️⃣ Set up Bates numbering options
            BatesNumberingOptions batesOptions = new BatesNumberingOptions
            {
                Prefix = "CASE01",
                StartNumber = 1,
                // Optional appearance tweaks:
                // Font = FontRepository.FindFont("Times New Roman"),
                // FontSize = 9,
                // Color = Color.DarkBlue,
                // Margin = new Margin(0, 0, 0, 15)
            };

            // 3️⃣ Save the document with Bates numbers
            string outputPath = @"YOUR_DIRECTORY\output.pdf";
            doc.Save(outputPath, batesOptions);

            Console.WriteLine($"Bates numbering added. Output saved to: {outputPath}");
        }
    }
}
```

### Output previsto

Eseguendo il programma si genera `output.pdf` dove ogni pagina mostra un'etichetta simile a:

```
CASE01-1
CASE01-2
CASE01-3
...
```

I numeri appaiono nel piè di pagina per impostazione predefinita, ma puoi spostarli regolando la proprietà `Margin` in `BatesNumberingOptions`.

## Casi limite e variazioni comuni

| Situazione | Cosa regolare |
|-----------|----------------|
| **Prefisso diverso per batch** | Modifica `Prefix` prima di chiamare `Save`. Puoi iterare su più documenti con prefissi distinti. |
| **Continuare la numerazione da un file precedente** | Imposta `StartNumber` all'ultimo numero usato + 1. |
| **Posizionare i numeri nell'intestazione** | Usa `batesOptions.Margin = new Margin(20, 0, 0, 0);` (margine superiore) o personalizza `batesOptions.Position`. |
| **Carattere o colore personalizzato** | Assegna le proprietà `Font`, `FontSize` e `Color` come mostrato nella sezione commentata. |
| **PDF di grandi dimensioni (1000+ pagine)** | L'operazione è efficiente in termini di memoria; tuttavia, potresti voler abilitare `doc.OptimizeResources()` prima di salvare per ridurre le dimensioni del file. |

**Suggerimento professionale:** Se il tuo flusso di lavoro richiede schemi di numerazione diversi per documento, incapsula la logica in un metodo di supporto:

```csharp
static void ApplyBatesNumbering(string src, string dst, string prefix, int start)
{
    var doc = new Document(src);
    var opts = new BatesNumberingOptions { Prefix = prefix, StartNumber = start };
    doc.Save(dst, opts);
}
```

## Conclusione

Ora sai **come aggiungere la numerazione Bates** a qualsiasi PDF usando Aspose.PDF in C#. Il tutorial ha coperto il caricamento del documento PDF, la configurazione delle opzioni di numerazione e il salvataggio del file finale—tutto in un unico programma eseguibile.

Da qui puoi esplorare argomenti correlati come **aggiungere filigrane**, **unire più PDF**, o **estrarre testo** con Aspose.PDF. Sperimenta con diversi caratteri, colori e posizioni per adeguare gli standard di formattazione della tua organizzazione.

Pronto a automatizzare il tuo flusso di lavoro dei documenti legali? Aggiungi il codice al tuo pipeline di build, eseguilo su batch di file e lascia che Aspose.PDF gestisca il lavoro pesante. Buona programmazione!

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Crea documento PDF C# – Aggiungi numerazione Bates](/pdf/english/net/programming-with-pdf-pages/create-pdf-document-c-add-bates-numbering/)
- [Aggiungi numerazione Bates PDF – Guida passo‑a‑passo per numerare le pagine PDF](/pdf/english/net/programming-with-pdf-pages/add-bates-numbering-pdf-step-by-step-guide-to-number-pdf-pag/)
- [Tutorial Aspose PDF – Inserire una pagina vuota e aggiornare la numerazione Bates](/pdf/english/net/programming-with-pdf-pages/aspose-pdf-tutorial-insert-a-blank-page-and-update-bates-num/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}