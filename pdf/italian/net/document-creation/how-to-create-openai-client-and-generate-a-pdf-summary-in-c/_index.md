---
category: general
date: 2026-10-10
description: Crea un client OpenAI in C# e impara a riassumere un PDF, convertire
  un PDF in un riassunto e salvare il riassunto PDF generato con Aspose.Pdf.AI.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create openai client
- convert pdf to summary
- how to summarize pdf
- how to save summary
- generate pdf summary
language: it
lastmod: 2026-10-10
og_description: Crea un client OpenAI in C# e impara subito come riassumere un PDF,
  convertire il PDF in un riassunto e salvare il riassunto PDF generato.
og_image_alt: Screenshot of C# code that creates an OpenAI client and generates a
  PDF summary
og_title: Crea un client OpenAI e genera un riepilogo PDF in C# – guida passo‑passo
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Create OpenAI client in C# and learn how to summarize a PDF, convert
    PDF to summary, and save the generated PDF summary with Aspose.Pdf.AI.
  headline: How to create OpenAI client and generate a PDF summary in C#
  type: TechArticle
- description: Create OpenAI client in C# and learn how to summarize a PDF, convert
    PDF to summary, and save the generated PDF summary with Aspose.Pdf.AI.
  name: How to create OpenAI client and generate a PDF summary in C#
  steps:
  - name: '**Console output** – the plain‑text summary displayed on the screen.'
    text: '**Console output** – the plain‑text summary displayed on the screen.'
  - name: '**`Summary_out.pdf`** – a downloadable PDF containing the same summary,
      ready for distribution.'
    text: '**`Summary_out.pdf`** – a downloadable PDF containing the same summary,
      ready for distribution.'
  - name: Lower the `WithTemperature` to 0.2 for more deterministic output.
    text: Lower the `WithTemperature` to 0.2 for more deterministic output.
  - name: Increase the
    text: Increase the
  type: HowTo
tags:
- OpenAI
- C#
- PDF processing
- Aspose.Pdf.AI
title: Come creare un client OpenAI e generare un riepilogo PDF in C#
url: /it/net/document-creation/how-to-create-openai-client-and-generate-a-pdf-summary-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come creare un client OpenAI e generare un riepilogo PDF in C#

Se hai bisogno di **creare un client OpenAI** in un'applicazione .NET, questo tutorial ti mostra esattamente come farlo e come trasformare qualsiasi PDF in un riepilogo conciso generato dall'IA. Vedrai come **convertire PDF in riepilogo**, recuperare il testo e **salvare il riepilogo** come nuovo file PDF—tutto con Aspose.Pdf.AI.

Riassumere i PDF è una necessità comune per flussi di lavoro ricchi di documenti, come revisione legale, aggregazione di ricerche o generazione automatica di report. Alla fine di questa guida sarai in grado di **generare un riepilogo PDF** programmaticamente, senza uscire dal tuo codice C#.

## Cosa ti serve

- .NET 6.0 o successivo (l'esempio è mirato a .NET 6, ma funziona con qualsiasi versione recente di .NET)
- Un pacchetto NuGet Aspose.Pdf.AI (`Aspose.Pdf.AI`) – questo wrapper semplifica le chiamate OpenAI per contenuti PDF
- Una chiave API OpenAI valida (puoi ottenerla dal portale OpenAI)
- Un file PDF di esempio che desideri riassumere (ad es., `SampleDocument.pdf`)
- Visual Studio 2022, VS Code o qualsiasi IDE che supporti lo sviluppo C#

> **Pro tip:** Conserva la tua chiave API in una posizione sicura come [user‑secrets](https://learn.microsoft.com/en-us/aspnet/core/security/app-secrets) o Azure Key Vault. Non inserirla mai direttamente nel codice sorgente.

## Passo 1: Installa il pacchetto NuGet Aspose.Pdf.AI

Apri un terminale nella cartella del tuo progetto ed esegui:

```bash
dotnet add package Aspose.Pdf.AI
```

Il pacchetto scarica il client HTTP necessario, gli strumenti di manipolazione PDF e un leggero wrapper attorno all'API OpenAI. Dopo l'installazione, ripristina il progetto per assicurarti che tutte le dipendenze siano disponibili:

```bash
dotnet restore
```

## Passo 2: **Crea il client OpenAI** con la tua chiave API

Creare il client è il primo passo verso qualsiasi operazione PDF guidata dall'IA. L'`OpenAIClient` gestisce l'autenticazione, il throttling delle richieste e il pooling delle connessioni per te.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.AI;
using System;
using System.Threading.Tasks;

class PdfSummarizer
{
    // Replace with your real key – never commit it to source control
    private const string ApiKey = "YOUR_OPENAI_API_KEY";

    public static async Task Main()
    {
        // ---- Step 2: create OpenAI client ----
        using var openAiClient = OpenAIClient
            .CreateWithApiKey(ApiKey)
            .Build();

        // The client is now ready for any Aspose.Pdf.AI operation.
        await SummarizePdfAsync(openAiClient);
    }
}
```

> **Perché è importante:** L'istruzione `using` garantisce che il client venga smaltito correttamente, rilasciando le risorse di rete ed evitando l'esaurimento dei socket in servizi a lunga esecuzione.

## Passo 3: Configura le opzioni di riepilogo – **converti PDF in riepilogo**

L'oggetto `OpenAISummaryCopilotOptions` indica all'IA cosa fare. Puoi regolare la temperatura, limitare l'uso dei token e, soprattutto, indicare il PDF di origine.

```csharp
private static async Task SummarizePdfAsync(OpenAIClient client)
{
    // ---- Step 3: set up summary options (convert PDF to summary) ----
    var summaryOptions = OpenAISummaryCopilotOptions
        .Create()
        .WithTemperature(0.5)                     // Balanced creativity vs. factuality
        .WithDocument("YOUR_DIRECTORY/SampleDocument.pdf");

    // The options are immutable; each call returns a new instance.
```

### Perché una temperatura 0.5?

Una temperatura di 0.5 produce un linguaggio conciso e accurato, consentendo comunque al modello di riformulare le frasi. Valori più alti (ad es., 0.9) rendono l'output più creativo ma possono allontanarsi dal significato originale—cosa indesiderabile per riepiloghi legali o tecnici.

## Passo 4: **Come riassumere un PDF** – istanzia il copilot e ottieni il testo

Ora che client e opzioni sono pronti, crea un summary copilot. Questo oggetto orchestra la richiesta a OpenAI e restituisce il risultato in più formati.

```csharp
    // ---- Step 4: instantiate the summary copilot (how to summarize PDF) ----
    var summaryCopilot = AICopilotFactory
        .CreateSummaryCopilot(client, summaryOptions);

    // Retrieve the generated summary as plain text
    string summaryText = await summaryCopilot.GetSummaryAsync();

    Console.WriteLine("=== Text Summary ===");
    Console.WriteLine(summaryText);
```

Il metodo `GetSummaryAsync` restituisce una versione pulita in plain‑text che puoi incorporare nell'interfaccia, inviare via email o memorizzare in un database.

## Passo 5: Recupera il riepilogo come documento PDF

Se ti serve una versione portatile e stampabile, chiedi al copilot un documento PDF. Questo passaggio dimostra **generare un riepilogo PDF** direttamente dal modello IA.

```csharp
    // ---- Step 5: retrieve the summary as a PDF document (generate PDF summary) ----
    Document summaryDocument = await summaryCopilot.GetSummaryDocumentAsync();

    // Optionally, you can add a cover page or watermark here before saving.
```

Il `Aspose.Pdf.Document` restituito si comporta come qualsiasi altro oggetto PDF nell'ecosistema Aspose, il che significa che puoi modificare ulteriormente le pagine, aggiungere metadati o unire altri PDF.

## Passo 6: **Come salvare il riepilogo** – persisti il PDF su disco

Infine, salva il riepilogo generato sul file system. L'helper `SaveSummaryAsync` combina recupero e salvataggio in una sola chiamata, ma mostreremo anche il salvataggio esplicito per completezza.

```csharp
    // ---- Step 6: save the summary PDF (how to save summary) ----
    const string outputPath = "YOUR_DIRECTORY/Summary_out.pdf";

    // Direct helper method
    await summaryCopilot.SaveSummaryAsync(outputPath);

    // Or, save the Document object manually
    // summaryDocument.Save(outputPath);
    Console.WriteLine($"Summary PDF saved to: {outputPath}");
}
```

> **Suggerimento:** Se devi imporre una convenzione di denominazione (ad es., file con timestamp), costruisci il percorso programmaticamente con `DateTime.UtcNow:yyyyMMdd_HHmmss`.

### Esempio completo eseguibile

Mettendo tutto insieme, ecco un programma autonomo che puoi copiare‑incollare in `Program.cs` ed eseguire:

```csharp
using Aspose.Pdf;
using Aspose.Pdf.AI;
using System;
using System.Threading.Tasks;

class PdfSummarizer
{
    private const string ApiKey = "YOUR_OPENAI_API_KEY";

    public static async Task Main()
    {
        // Create OpenAI client
        using var openAiClient = OpenAIClient
            .CreateWithApiKey(ApiKey)
            .Build();

        // Configure summary options (convert PDF to summary)
        var summaryOptions = OpenAISummaryCopilotOptions
            .Create()
            .WithTemperature(0.5)
            .WithDocument("YOUR_DIRECTORY/SampleDocument.pdf");

        // Instantiate the copilot (how to summarize PDF)
        var summaryCopilot = AICopilotFactory
            .CreateSummaryCopilot(openAiClient, summaryOptions);

        // Get plain‑text summary
        string summaryText = await summaryCopilot.GetSummaryAsync();
        Console.WriteLine("=== Text Summary ===");
        Console.WriteLine(summaryText);

        // Get PDF version (generate PDF summary)
        Document summaryDoc = await summaryCopilot.GetSummaryDocumentAsync();

        // Save the PDF (how to save summary)
        const string outPath = "YOUR_DIRECTORY/Summary_out.pdf";
        await summaryCopilot.SaveSummaryAsync(outPath);
        Console.WriteLine($"Summary PDF saved to: {outPath}");
    }
}
```

L'esecuzione del programma produce due artefatti:

1. **Output della console** – il riepilogo in plain‑text visualizzato sullo schermo.
2. **`Summary_out.pdf`** – un PDF scaricabile contenente lo stesso riepilogo, pronto per la distribuzione.

## Variazioni comuni e casi limite

| Situazione | Modifica consigliata |
|------------|----------------------|
| **PDF di grandi dimensioni (> 10 MB)** | Dividi il documento in blocchi più piccoli (ad es., per capitolo) e riassumi ogni blocco separatamente. Combina i risultati con `Document.AppendDocument`. |
| **Necessità di un prompt personalizzato** | Usa `WithPrompt("Summarize the following legal contract in bullet points:")` prima di chiamare `CreateSummaryCopilot`. |
| **PDF di origine non inglese** | Imposta `WithLanguage("es")` (o il codice ISO appropriato) per guidare la gestione della lingua da parte del modello. |
| **Errori di rate‑limit** | Aumenta `WithRetryCount` o aggiungi un `Task.Delay` tra le chiamate. |
| **Salvataggio su storage cloud** | Sostituisci il percorso del file system con uno stream (`MemoryStream`) e carica lo stream su Azure Blob Storage o AWS S3. |

## Verifica del risultato

Al termine del programma, apri `Summary_out.pdf` in qualsiasi visualizzatore PDF. Dovresti vedere un documento pulito, di una pagina (o più pagine, a seconda della lunghezza) che cattura le idee principali di `SampleDocument.pdf`. Confronta il riepilogo testuale stampato sulla console con la versione PDF—entrambi dovrebbero corrispondere parola per parola.

Se il riepilogo risulta incompleto:

1. Abbassa `WithTemperature` a 0.2 per un output più deterministico.
2. Aumenta il


## Cosa dovresti imparare dopo?


I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [How to Create PDF in C# – Add Page, Draw Rectangle & Save](/pdf/english/net/document-creation/how-to-create-pdf-in-c-add-page-draw-rectangle-save/)
- [Learn How to Generate PDF Documents with Aspose.PDF for .NET](/pdf/english/net/document-creation/)
- [How to Create Tagged PDFs with Aspose.PDF for .NET – Enhance Accessibility](/pdf/english/net/bookmarks-navigation/tagged-pdf-creation-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}