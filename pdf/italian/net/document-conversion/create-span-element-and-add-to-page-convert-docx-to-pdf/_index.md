---
category: general
date: 2026-03-27
description: Creare un elemento span in C# e imparare come aggiungere lo span a una
  pagina durante la conversione da DOCX a PDF e il salvataggio come PDF. Guida passo‑passo
  per gli sviluppatori.
draft: false
keywords:
- create span element
- how to add span
- convert docx to pdf
- add element to page
- save as pdf
language: it
og_description: Crea un elemento span in C# e impara come aggiungere lo span a una
  pagina durante la conversione da DOCX a PDF, quindi salva come PDF. Esempio di codice
  completo incluso.
og_title: Crea elemento span e aggiungilo alla pagina – Converti DOCX in PDF
tags:
- C#
- DocumentProcessing
- PDFConversion
title: Crea elemento span e aggiungilo alla pagina – Converti DOCX in PDF
url: /it/net/document-conversion/create-span-element-and-add-to-page-convert-docx-to-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crea elemento span e aggiungilo alla pagina – Converti DOCX in PDF

Creare **span element** in un file DOCX è un'operazione comune quando hai bisogno di un controllo preciso del layout. In questo tutorial ti mostreremo **come aggiungere uno span** a una pagina, **convertire DOCX in PDF** e **salvare come PDF**—tutto in pochi passaggi ordinati.  

Se ti è mai capitato di fissare un documento Word e pensare, “Vorrei poter inserire una piccola casella di testo a una coordinata esatta”, sei nel posto giusto. Ti guideremo attraverso l'intero flusso di lavoro, dal caricamento del file sorgente fino all'ottenimento di un PDF rifinito.

## Cosa otterrai

* Carica un file `.docx` usando la classe `Document` della libreria di documenti.  
* **Create span element** con l'API `TaggedContent`.  
* Posiziona quello span a coordinate X/Y esatte su una pagina scelta.  
* **Add element to page** in modo affidabile, anche quando la pagina non è la prima.  
* **Convert DOCX to PDF** e **save as PDF** con una singola chiamata `Save`.

Nessuno strumento esterno, nessuna impostazione misteriosa—solo codice C# puro che puoi copiare‑incollare nel tuo progetto.

## Prerequisiti

* .NET 6+ (o qualsiasi runtime .NET recente supportato dalla tua libreria).  
* L'SDK di elaborazione documenti che fornisce `Document`, `TaggedContent`, `Position`, ecc.  
* Una conoscenza di base della sintassi C#—se sai scrivere un `Console.WriteLine`, sei a posto.

> **Suggerimento:** Mantieni la tua versione SDK aggiornata; l'ultima release (v3.2 a partire da marzo 2026) include ottimizzazioni delle prestazioni per le operazioni a livello di pagina.

---

![Diagramma che illustra come creare un elemento span e posizionarlo su una pagina PDF](https://example.com/images/create-span-element.png "Diagramma di posizionamento dell'elemento span")

## Crea elemento span – Posizionamento e aggiunta alla pagina

Di seguito trovi il codice completo e eseguibile che fa tutto, dal caricamento del DOCX sorgente alla scrittura del PDF finale. Sentiti libero di inserirlo in un'app console, modificare i percorsi e eseguirlo.

```csharp
using DocumentProcessing;   // Replace with the actual namespace of your SDK
using DocumentProcessing.Models;

class Program
{
    static void Main()
    {
        // Step 1: Load the DOCX you want to modify
        // -------------------------------------------------
        // The constructor takes a file path; make sure the file exists.
        Document doc = new Document(@"C:\Docs\input.docx");

        // Step 2: Create a new span element using the TaggedContent API
        // -------------------------------------------------
        // A span is a lightweight container for inline content.
        var span = doc.TaggedContent.CreateSpanElement();
        // Optional: add some text inside the span
        span.Text = "Hello, world!";

        // Step 3: Position the span at the desired coordinates (X = 50, Y = 750)
        // -------------------------------------------------
        // Position uses points (1/72 inch). Adjust as needed.
        span.Position = new Position(50, 750);

        // Step 4: Add the span to the target page (page index 1 = second page)
        // -------------------------------------------------
        // Pages are zero‑based; index 1 means the second page in the document.
        doc.Pages[1].Add(span);

        // Step 5: Convert the modified DOCX to PDF and save the result
        // -------------------------------------------------
        // The Save method automatically detects the output format from the extension.
        doc.Save(@"C:\Docs\output.pdf");

        // Confirmation output
        Console.WriteLine("Span added, document converted, and PDF saved successfully.");
    }
}
```

### Spiegazione passo‑passo

#### Passo 1 – Carica il documento DOCX  
Instanziamo un oggetto `Document` che punta a `input.docx`. Questo oggetto rappresenta l'intero file Word in memoria, fornendoci l'accesso a pagine, contenuti e metadati.  

#### Passo 2 – Crea un elemento span  
La chiamata `TaggedContent.CreateSpanElement()` restituisce un contenitore inline leggero. Pensalo come una piccola scatola invisibile che può contenere testo, immagini o altri elementi inline. Aggiungere testo (`span.Text`) è opzionale ma utile per il debug.  

#### Passo 3 – Posiziona lo span  
`new Position(50, 750)` imposta l'angolo in alto‑a‑sinistra dello span a 50 pt dal margine sinistro e 750 pt dalla parte superiore della pagina. Questi valori sono assoluti, quindi puoi posizionare lo span ovunque—perfetto per layout precisi.  

#### Passo 4 – Aggiungi lo span alla pagina di destinazione  
`doc.Pages[1].Add(span)` inserisce lo span nella seconda pagina. L'API utilizza un indice basato su zero, quindi la pagina 0 è la prima pagina. Se devi aggiungerlo alla prima pagina, usa semplicemente `doc.Pages[0]`.  

#### Passo 5 – Converti DOCX in PDF e salva come PDF  
Chiamare `doc.Save("output.pdf")` fa due cose: scrive il documento modificato su disco **e** converte il contenuto in PDF grazie all'estensione `.pdf`. Non è necessario alcun passaggio di conversione aggiuntivo—questo è il modo più semplice per **salvare come PDF**.

---

## Come aggiungere uno span su una pagina diversa (avanzato)

A volte non conosci l'indice della pagina in anticipo. Puoi individuare una pagina per il suo numero (amichevole per l'utente) o cercando una parola chiave specifica.

```csharp
// Find the page that contains the word "Summary"
int targetIndex = doc.Pages
    .Select((p, i) => new { Page = p, Index = i })
    .FirstOrDefault(x => x.Page.Text.Contains("Summary"))?.Index ?? 0;

// Fallback to first page if not found
targetIndex = Math.Max(targetIndex, 0);

// Add the span to the discovered page
doc.Pages[targetIndex].Add(span);
```

**Perché è importante:** Nei report in cui il numero di pagine varia, codificare rigidamente `Pages[1]` può rompere il layout. Questo snippet mostra un modello robusto per **come aggiungere uno span** in modo dinamico.

---

## Problemi comuni e come evitarli

| Problema | Cosa succede | Soluzione |
|----------|--------------|-----------|
| **Span non visibile** | Le coordinate sono fuori dalla pagina o lo span ha larghezza/altezza zero. | Verifica nuovamente i valori di `Position`; usa un righello nel visualizzatore PDF. |
| **Indice pagina errato** | Aggiungi alla pagina 0 ma ti aspetti che sia sulla pagina 2. | Ricorda che l'API è basata su zero; aggiungi 1 al numero di pagina umano. |
| **Salvataggio sovrascrive la sorgente** | `doc.Save("input.docx")` sostituisce il file originale. | Salva sempre in un nuovo percorso (`output.pdf`) durante la conversione. |
| **Riferimento SDK mancante** | Errore di compilazione sulla classe `Document`. | Installa il pacchetto NuGet: `dotnet add package DocumentProcessing.SDK`. |

## Verifica del risultato

Dopo aver eseguito il programma, apri `output.pdf` in qualsiasi visualizzatore PDF. Dovresti vedere il testo “Hello, world!” posizionato esattamente a (50, 750) sulla seconda pagina. Se il testo appare altrove, regola i valori di `Position` e riesegui.  

Per i test automatizzati, puoi usare un parser PDF (ad esempio iTextSharp) per verificare programmaticamente le coordinate del testo.

```csharp
// Example using iTextSharp to verify position (pseudo‑code)
var pdfReader = new PdfReader(@"C:\Docs\output.pdf");
var page = pdfReader.GetPageContent(2);
Debug.Assert(page.Contains("Hello, world!"));
```

---

## Prossimi passi

* **Style the span** – esplora le proprietà `span.Font`, `span.Color` e altre proprietà di stile.  
* **Add images** – usa `CreateImageElement()` al posto di uno span per le grafiche.  
* **Batch processing** – itera su una cartella di file DOCX

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}