---
category: general
date: 2026-08-04
description: Come utilizzare Aspose per estrarre il testo da PDF scansionati e convertire
  PDF in testo con C#. Impara a leggere file PDF scansionati e ottenere risultati
  OCR affidabili.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use aspose
- extract scanned pdf text
- convert pdf to text
- read scanned pdf
- how to extract text
language: it
lastmod: 2026-08-04
og_description: Come utilizzare Aspose per leggere file PDF scansionati, estrarre
  il testo da PDF scansionati e convertire PDF in testo con un esempio completo e
  eseguibile.
og_image_alt: Screenshot showing how to use Aspose OCR copilot to extract text from
  a scanned PDF
og_title: Come usare Aspose – estrarre testo da PDF scansionati in C#
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: How to use Aspose to extract scanned PDF text and convert PDF to text
    with C#. Learn to read scanned PDF files and get reliable OCR results.
  headline: How to use Aspose to extract text from a scanned PDF – step‑by‑step guide
  type: TechArticle
- questions:
  - answer: Yes. Add `.WithPassword("yourPassword")` to the options builder before
      creating the copilot.
    question: Does this work with password‑protected PDFs?
  - answer: Use `GetTextStructureAsync()` instead of `GetTextAsync()`. The method
      returns a JSON payload that includes page indices, bounding boxes, and confidence
      scores.
    question: Can I extract text in a structured format (e.g., JSON with page numbers)?
  - answer: 'The plain‑text extraction flattens tables into line‑break‑separated rows.
      For richer data, request the PDF‑to‑HTML conversion (`GetHtmlAsync`) and parse
      the HTML table elements. ## Conclusion You now know **how to use Aspose** to
      read a scanned PDF, extract scanned PDF text, and **convert PDF to tex'
    question: What if the PDF contains tables?
  type: FAQPage
tags:
- Aspose.PDF.AI
- OCR
- C#
- PDF processing
title: Come utilizzare Aspose per estrarre testo da un PDF scansionato – guida passo
  passo
url: /it/net/text/how-to-use-aspose-to-extract-text-from-a-scanned-pdf-step-by/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come utilizzare Aspose per estrarre testo da un PDF scansionato – guida passo‑passo

Se hai bisogno di **come usare Aspose** per OCR, questa guida ti mostra come estrarre il testo da un PDF scansionato in poche righe di C#. Che tu stia costruendo un servizio di archiviazione documenti o un indice di ricerca per documenti cartacei legacy, la soluzione funziona con qualsiasi PDF scansionato che fornisci al servizio Aspose.Pdf.AI.

In questo tutorial imparerai a:

* Creare un copilot OCR che legge un PDF scansionato.
* Estrarre il testo riconosciuto in modo asincrono.
* Visualizzare o elaborare ulteriormente la stringa estratta.

L’unico prerequisito è un abbonamento attivo a Aspose.Pdf.AI e un ambiente di sviluppo .NET 6 (o successivo).

## Prerequisiti

| Requisito | Perché è importante |
|-----------|----------------------|
| .NET 6 SDK o più recente | Fornisce `async Main` e le moderne funzionalità del linguaggio. |
| Pacchetto NuGet Aspose.Pdf.AI (`Aspose.Pdf.AI`) | Contiene `AICopilotFactory` e le opzioni OCR. |
| Un’istanza valida di `client` Aspose.Pdf.AI (API key) | Autentica le tue richieste al servizio cloud. |
| Un file PDF scansionato (ad es., `Scanned.pdf`) | Il documento sorgente da cui verrà estratto il testo. |

Installa il pacchetto con la CLI .NET:

```bash
dotnet add package Aspose.Pdf.AI
```

## Passo 1: Configurare il client Aspose.Pdf.AI

Prima di poter chiamare qualsiasi endpoint OCR devi creare un client che contenga le tue credenziali API. Il client è thread‑safe e può essere riutilizzato per più documenti.

```csharp
using Aspose.Pdf.AI;
using Aspose.Pdf.AI.Models;

// Replace with your actual API key and base URL if you use a private cloud.
var client = new PdfAiClient(new PdfAiConfiguration
{
    ApiKey = "YOUR_API_KEY",
    // BaseUrl = "https://api.aspose.cloud" // default, change only if needed
});
```

**Perché questo passo è necessario** – Il servizio Aspose valida ogni richiesta rispetto al tuo abbonamento. Creare il client una sola volta evita handshake di rete ripetuti e mantiene il codice pulito.

## Passo 2: Creare un copilot OCR per il documento PDF scansionato

`AICopilotFactory` costruisce un copilot OCR specializzato che sa come elaborare il file che specifichi. Passi il `client` e un oggetto `OpenAIOcrOptions` che punta al percorso del PDF.

```csharp
using Aspose.Pdf.AI;

// Step 2: Build the OCR copilot
var ocrCopilot = AICopilotFactory.CreateOcrCopilot(
    client,                                   // Your Aspose.Pdf.AI client instance
    OpenAIOcrOptions.Create()
        .WithDocument("YOUR_DIRECTORY/Scanned.pdf") // Path to the scanned PDF
);
```

**Spiegazione** – `CreateOcrCopilot` incapsula tutte le chiamate HTTP di basso livello. Il metodo `WithDocument` indica al servizio quale file analizzare; puoi anche fornire uno `Stream` se il PDF è in memoria.

## Passo 3: Estrarre il testo riconosciuto in modo asincrono

Chiamare `GetTextAsync` esegue l’operazione OCR nel cloud e restituisce il risultato in plain‑text. Poiché l’operazione può richiedere alcuni secondi, il metodo è asincrono.

```csharp
// Step 3: Perform OCR and get the text
string ocrText = await ocrCopilot.GetTextAsync();
```

**Perché asincrono?** – La latenza di rete e il tempo di elaborazione OCR sono imprevedibili. Usare `await` impedisce alla tua applicazione di bloccare il thread principale, cosa particolarmente importante per scenari UI o web‑service.

## Passo 4: Utilizzare il testo estratto

A questo punto disponi di una normale `string` .NET contenente la trascrizione completa del PDF scansionato. Puoi scriverla sulla console, salvarla in un database o passarla a un motore di ricerca.

```csharp
// Step 4: Display the result
Console.WriteLine("=== OCR Result ===");
Console.WriteLine(ocrText);
```

### Output previsto

Se `Scanned.pdf` contiene una singola pagina con la frase “Hello, world!”, la console mostrerà:

```
=== OCR Result ===
Hello, world!
```

Per documenti multi‑pagina l’output concatena il testo di ogni pagina, preservando le interruzioni di riga.

## Esempio completo, eseguibile

Di seguito trovi un programma completo che puoi incollare in un nuovo progetto console (`dotnet new console`). Dimostra **come usare Aspose** dall’inizio alla fine, includendo la gestione degli errori per le problematiche più comuni.

```csharp
using System;
using System.Threading.Tasks;
using Aspose.Pdf.AI;
using Aspose.Pdf.AI.Models;

namespace AsposeOcrDemo
{
    class Program
    {
        static async Task Main(string[] args)
        {
            // 1️⃣ Initialize the Aspose.Pdf.AI client
            var client = new PdfAiClient(new PdfAiConfiguration
            {
                ApiKey = "YOUR_API_KEY"
                // BaseUrl = "https://api.aspose.cloud" // optional
            });

            // 2️⃣ Build the OCR copilot for the target PDF
            var pdfPath = "YOUR_DIRECTORY/Scanned.pdf";
            var ocrCopilot = AICopilotFactory.CreateOcrCopilot(
                client,
                OpenAIOcrOptions.Create().WithDocument(pdfPath)
            );

            try
            {
                // 3️⃣ Extract text asynchronously
                string ocrText = await ocrCopilot.GetTextAsync();

                // 4️⃣ Use the extracted text (display in console)
                Console.WriteLine("=== OCR Result ===");
                Console.WriteLine(ocrText);
            }
            catch (Exception ex)
            {
                // Common errors: invalid API key, missing file, unsupported PDF version
                Console.Error.WriteLine($"Error during OCR: {ex.Message}");
            }
        }
    }
}
```

**Punti chiave nell'esempio**

* `await` garantisce un’esecuzione non bloccante.
* Il blocco `try/catch` espone errori di rete o di servizio, essenziali quando **si leggono PDF scansionati** su larga scala.
* Sostituisci `YOUR_API_KEY` e `YOUR_DIRECTORY/Scanned.pdf` con valori reali prima di eseguire.

## Gestione dei casi limite e consigli di best‑practice

| Situazione | Approccio consigliato |
|------------|-----------------------|
| **PDF di grandi dimensioni ( > 50 MB )** | Suddividi il documento in blocchi più piccoli lato client e processa ciascun blocco con un copilot separato. Questo riduce la pressione sulla memoria e migliora l’affidabilità. |
| **Scansioni di bassa qualità** | Regola la qualità OCR aggiungendo `.WithLanguage("eng")` o `.WithEnhanceImage(true)` a `OpenAIOcrOptions`. Il servizio supporta suggerimenti di lingua che migliorano l’accuratezza. |
| **Più lingue** | Fornisci una lista separata da virgole, ad es., `.WithLanguage("eng,spa")`. Il motore OCR rileverà e trascriverà entrambe le lingue. |
| **File immagine non PDF** | Converti l’immagine in PDF prima (`Aspose.Pdf` library) o usa `OpenAIOcrOptions.WithImage` per inviare direttamente l’immagine. |
| **Limite di velocità superato** | Implementa un back‑off esponenziale e una logica di retry; l’API Aspose restituisce HTTP 429 quando superi la quota. |

### Consiglio professionale

Cachea il risultato `ocrText` se prevedi di riutilizzarlo in seguito. L’operazione OCR è la parte più costosa del flusso di lavoro, e riutilizzare la stringa evita chiamate API duplicate e salva crediti.

## Domande frequenti

**D: Funziona con PDF protetti da password?**  
R: Sì. Aggiungi `.WithPassword("yourPassword")` al builder delle opzioni prima di creare il copilot.

**D: Posso estrarre il testo in un formato strutturato (ad es., JSON con numeri di pagina)?**  
R: Usa `GetTextStructureAsync()` invece di `GetTextAsync()`. Il metodo restituisce un payload JSON che include indici di pagina, bounding box e punteggi di confidenza.

**D: E se il PDF contiene tabelle?**  
R: L’estrazione in plain‑text appiattisce le tabelle in righe separate da interruzioni di riga. Per dati più ricchi, richiedi la conversione PDF‑to‑HTML (`GetHtmlAsync`) e analizza gli elementi HTML delle tabelle.

## Conclusione

Ora sai **come usare Aspose** per leggere un PDF scansionato, estrarre il testo da PDF scansionati e **convertire PDF in testo** con un programma C# minimale. Il processo consiste nel creare un copilot OCR, chiamare `GetTextAsync` e gestire la stringa risultante. Seguendo i consigli per i casi limite potrai scalare la soluzione a grandi batch di documenti, contenuti multilingue e PDF sicuri.

Prossimamente potresti approfondire:

* **Come estrarre testo** con preservazione del layout (`GetHtmlAsync`).
* Usare Aspose.Pdf.AI per **estrarre tabelle** ed esportarle in CSV.
* Integrare l’output OCR con Azure Cognitive Search per archivi documentali ricercabili.

Buon coding e goditi l’accuratezza che l’OCR potenziato dall’AI di Aspose porta ai tuoi flussi di lavoro con PDF scansionati!

## Cosa dovresti imparare dopo?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Extract Text from PDF Files Using Aspose.PDF for .NET](/pdf/english/net/text-operations/extract-text-pdf-aspose-dotnet/)
- [How to Extract Text from Specific Regions in PDFs Using Aspose.PDF for .NET](/pdf/english/net/text-operations/extract-text-specific-region-aspose-pdf-net/)
- [How to Extract Highlighted Text from PDFs Using Aspose.PDF for .NET](/pdf/english/net/text-operations/extract-highlighted-text-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}