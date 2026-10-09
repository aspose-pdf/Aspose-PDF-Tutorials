---
category: general
date: 2026-06-21
description: Aggiungi la numerazione Bates in Word rapidamente. Scopri come aggiungere
  Bates, applicare la numerazione Bates per documenti legali e automatizzare la numerazione
  con C#.
draft: false
keywords:
- add bates numbering
- how to add bates
- bates numbering in word
- bates numbering for legal
- apply bates numbering
language: it
og_description: Aggiungi la numerazione Bates in Word usando C#. Questa guida mostra
  come aggiungere Bates, applicare la numerazione Bates per documenti legali e automatizzare
  il processo.
og_title: Aggiungi la numerazione Bates in Word – Guida completa alla programmazione
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Add Bates numbering in Word quickly. Learn how to add Bates, apply
    Bates numbering for legal docs, and automate numbering with C#.
  headline: Add Bates Numbering in Word – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Add Bates numbering in Word quickly. Learn how to add Bates, apply
    Bates numbering for legal docs, and automate numbering with C#.
  name: Add Bates Numbering in Word – Complete Step‑by‑Step Guide
  steps:
  - name: Expected Output
    text: '| Page | Bates Number | |------|--------------| | 1 | ABC-1000 | | 2 |
      ABC-1001 | | … | … | | N | ABC‑(1000 + N‑1) |'
  - name: What if the document already contains page numbers?
    text: The `AddBatesNumbering` method will **not** overwrite existing page number
      fields; it simply adds a new field. If you want to replace the existing numbers,
      remove them first or set `batesOptions.Position` to the same location as the
      current page numbers.
  - name: Can I skip pages (e.g., exclude a cover page)?
    text: 'Yes. Use the overload that accepts a `PageRange`:'
  - name: How do I change the numbering format (Roman numerals, letters)?
    text: 'The `BatesNumberingOptions` class supports a `NumberFormat` property:'
  - name: What about performance on huge files?
    text: Loading a 2‑GB Word file can consume a lot of RAM. To mitigate, process
      the document in chunks using the `DocumentSplitter` utility, apply Bates numbering
      to each chunk, then merge the parts back together. This pattern keeps memory
      usage under control while still letting you **apply bates numbering*
  type: HowTo
tags:
- document‑automation
- csharp
- legal‑tech
title: Aggiungi la numerazione Bates in Word – Guida completa passo‑passo
url: /it/net/programming-with-document/add-bates-numbering-in-word-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aggiungere la numerazione Bates in Word – Guida completa passo‑passo

Ti sei mai chiesto come aggiungere la numerazione Bates a un file Word senza digitare manualmente ogni numero? Non sei solo. Molti avvocati, paralegali e specialisti di e‑discovery hanno bisogno di un modo affidabile per **add Bates numbering** a centinaia di pagine, e farlo a mano è un incubo.

In questo tutorial percorreremo una soluzione C# pulita che **applies Bates numbering** a un file `.docx`, spiega perché ogni riga è importante e ti mostra come modificare il codice per esigenze legali specifiche. Alla fine sarai in grado di generare un documento perfettamente numerato in pochi secondi—senza plugin aggiuntivi.

## Cosa imparerai

- Il codice esatto necessario per **add Bates numbering** a un documento Word.
- Come funziona la classe `BatesNumberingOptions` e perché potresti modificare il prefisso o il valore iniziale.
- Suggerimenti per utilizzare questo approccio su grandi fascicoli, incluse considerazioni sulla memoria.
- Una rapida panoramica dei prerequisiti così potrai copiare‑incollare la soluzione ed eseguirla oggi.

**Prerequisiti**  
- .NET 6+ (o .NET Framework 4.7.2+ se preferisci il runtime più vecchio).  
- Un riferimento alla libreria Aspose.Words per .NET (o qualsiasi API simile che espone `AddBatesNumbering`).  
- Familiarità di base con C# e Visual Studio (o il tuo IDE preferito).

Se ti trovi a tuo agio con questi, immergiamoci.

## Passo 1: Configura il progetto e importa la libreria

Per prima cosa, crea una nuova app console (o integrala in un servizio esistente). Quindi aggiungi il pacchetto NuGet Aspose.Words:

```bash
dotnet add package Aspose.Words
```

> **Consiglio professionale:** Usa la licenza di valutazione gratuita per i test; aggiunge una piccola filigrana ma funziona esattamente come la versione completa.

```csharp
using Aspose.Words;
using Aspose.Words.BatesNumbering;
```

Queste istruzioni `using` importano le classi `Document` e `BatesNumberingOptions` nello scope, essenziali per il passaggio **apply bates numbering** più avanti.

## Passo 2: Carica il documento sorgente

Avrai bisogno di un file Word su cui lavorare. Il codice qui sotto carica `input.docx` da una cartella che specifichi. Sostituisci `"YOUR_DIRECTORY"` con il percorso reale sul tuo computer.

```csharp
// Step 1: Load the source document
var document = new Document("YOUR_DIRECTORY/input.docx");
```

Perché caricare prima il file? L'oggetto `Document` analizza l'intero pacchetto Word in memoria, permettendoci di manipolare intestazioni, piè di pagina e layout di pagina prima di salvare. Se il file è enorme (ad esempio 10.000 pagine), considera l'uso di `LoadOptions` con `LoadFormat.Docx` per trasmettere in streaming le sezioni invece di caricare tutto in una volta.

## Passo 3: Configura le opzioni di numerazione Bates

Qui avviene la magia. Indichi alla libreria quale prefisso usare (`"ABC-"` nell'esempio) e da dove iniziare a contare (`1000`). Entrambi i valori sono completamente personalizzabili.

```csharp
// Step 2: Define Bates numbering options (prefix and starting number)
var batesOptions = new BatesNumberingOptions
{
    Prefix = "ABC-",
    Start = 1000,
    // Optional: set the position, alignment, and font if you need legal‑specific styling
    // Position = BatesNumberingPosition.Footer,
    // Alignment = BatesNumberingAlignment.Right,
    // Font = new Font("Times New Roman", 10, FontStyle.Bold)
};
```

**Perché un prefisso?** Nella pratica legale, i prefissi spesso identificano il caso o la parte produttrice (`"ABC-"` potrebbe rappresentare *Acme Bank Corp.*). Iniziare da `1000` è comune perché molte firme riservano i primi 999 numeri per bozze interne.

Se stai gestendo documenti **Bates numbering for legal**, potresti anche voler impostare `batesOptions.Position` su `Header` o `Footer` e regolare l'allineamento per rispettare le norme del tribunale. La libreria supporta queste modifiche di default.

## Passo 4: Applica la numerazione Bates all'intero documento

Ora iniettiamo effettivamente i numeri. Il metodo `AddBatesNumbering` scorre ogni pagina, inserisce la stringa formattata e aggiorna il conteggio interno delle pagine del documento.

```csharp
// Step 3: Apply Bates numbering to the entire document
document.AddBatesNumbering(batesOptions);
```

Dietro le quinte, Aspose.Words crea un campo nascosto su ogni pagina che viene visualizzato come `ABC-1000`, `ABC-1001`, e così via. Poiché è un campo, puoi successivamente modificare il prefisso o il numero iniziale senza rigenerare l'intero file—utile per **how to add bates** dopo che una richiesta di discovery è cambiata.

## Passo 5: Salva il documento modificato

Infine, scrivi l'output in un nuovo file. Mantenere l'originale intatto è una buona pratica, soprattutto quando si gestiscono prove che devono rimanere immutate.

```csharp
// Step 4: Save the modified document
document.Save("YOUR_DIRECTORY/output.docx");
```

Ora hai `output.docx` con numeri Bates sequenziali aggiunti a ogni pagina. Aprilo in Word e vedrai i numeri esattamente dove li hai specificati (piè di pagina per impostazione predefinita). La dimensione del file può aumentare leggermente a causa dei campi aggiuntivi, ma è trascurabile rispetto ai vantaggi.

### Output previsto

| Pagina | Numero Bates |
|--------|--------------|
| 1      | ABC-1000     |
| 2      | ABC-1001     |
| …      | …            |
| N      | ABC‑(1000 + N‑1) |

Se apri la vista “Field Codes” del documento (`Alt+F9` in Word), vedrai qualcosa come `{ BATES \* MERGEFORMAT ABC-1000 }` su ogni pagina.

## Casi limite e domande comuni

### E se il documento contiene già i numeri di pagina?

Il metodo `AddBatesNumbering` **non** sovrascriverà i campi dei numeri di pagina esistenti; aggiunge semplicemente un nuovo campo. Se vuoi sostituire i numeri esistenti, rimuovili prima o imposta `batesOptions.Position` nella stessa posizione dei numeri di pagina attuali.

### Posso saltare pagine (ad esempio, escludere la copertina)?

Sì. Usa la sovraccarico che accetta un `PageRange`:

```csharp
var range = new PageRange(2, document.PageCount); // start at page 2
document.AddBatesNumbering(batesOptions, range);
```

### Come cambio il formato di numerazione (numeri romani, lettere)?

La classe `BatesNumberingOptions` supporta una proprietà `NumberFormat`:

```csharp
batesOptions.NumberFormat = BatesNumberFormat.RomanUpper;
```

Impostala prima di chiamare `AddBatesNumbering`. Questa flessibilità è utile quando un tribunale richiede uno stile specifico.

### E per le prestazioni su file enormi?

Caricare un file Word da 2 GB può consumare molta RAM. Per mitigare, elabora il documento in blocchi usando l'utilità `DocumentSplitter`, applica la numerazione Bates a ciascun blocco, poi unisci le parti. Questo schema mantiene l'uso della memoria sotto controllo consentendo comunque di **apply bates numbering** in modo efficiente.

## Esempio completo funzionante

Mettendo tutto insieme, ecco un programma console pronto da eseguire:

```csharp
using System;
using Aspose.Words;
using Aspose.Words.BatesNumbering;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the source document
            var inputPath = @"C:\Docs\input.docx";
            var document = new Document(inputPath);

            // 2️⃣ Define Bates numbering options
            var batesOptions = new BatesNumberingOptions
            {
                Prefix = "ABC-",
                Start = 1000,
                // Optional styling for legal compliance
                Position = BatesNumberingPosition.Footer,
                Alignment = BatesNumberingAlignment.Right,
                Font = new Font("Times New Roman", 9, FontStyle.Bold)
            };

            // 3️⃣ Apply Bates numbering across all pages
            document.AddBatesNumbering(batesOptions);

            // 4️⃣ Save the result
            var outputPath = @"C:\Docs\output.docx";
            document.Save(outputPath);

            Console.WriteLine($"✅ Bates numbering applied! Saved to {outputPath}");
        }
    }
}
```

Esegui il programma, apri `output.docx` e vedrai una serie pulita di numeri pronta per l'archiviazione, la discovery o la presentazione al tribunale.

## Conclusione

Ora sai esattamente **how to add Bates** a un documento Word usando C#. I passaggi—caricare, configurare, applicare e salvare—sono semplici, ma sufficientemente flessibili per soddisfare i flussi di lavoro **Bates numbering for legal**, prefissi personalizzati e anche l'elaborazione batch su larga scala.

Se sei pronto a portare il tutto oltre, considera:

- Integrare il codice in una web API così i colleghi possono caricare file e ricevere PDF numerati istantaneamente.  
- Aggiungere la gestione degli errori per file mancanti o problemi di permessi (un rapido `try/catch` attorno a `Document.Load`).  
- Esplorare altre funzionalità di Aspose.Words come filigrane o redazione per una suite completa di strumenti e‑discovery.

Sentiti libero di sperimentare con prefissi diversi, numeri iniziali, o anche combinare più schemi di numerazione nello stesso documento. Il mondo di **apply bates numbering** è sorprendentemente versatile una volta che hai la logica di base.

Hai domande o uno scenario complicato? Lascia un commento qui sotto e risolveremo insieme. Buon coding!

## Cosa dovresti imparare dopo?

I tutorial seguenti coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Apply Numbering Style in Heading of PDF using Java](/pdf/english/java/pdf-images/apply-numbering-style-in-heading-of-pdf-using-java/)
- [Apply Numbering Style In Heading Of Pdf Using Java](/pdf/german/java/pdf-images/apply-numbering-style-in-heading-of-pdf-using-java/)
- [Apply Numbering Style In Heading Of Pdf Using Java](/pdf/french/java/pdf-images/apply-numbering-style-in-heading-of-pdf-using-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}