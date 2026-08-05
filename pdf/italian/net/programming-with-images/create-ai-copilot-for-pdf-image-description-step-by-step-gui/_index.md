---
category: general
date: 2026-08-04
description: Crea AI Copilot per generare descrizioni delle immagini per file PDF.
  Scopri come configurare le opzioni immagine di OpenAI ed estrarre le descrizioni
  delle immagini in modo efficiente.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create AI copilot
- generate image description
- image description PDF
- OpenAI image options
- extract image description
language: it
lastmod: 2026-08-04
og_description: Crea un AI Copilot per generare descrizioni delle immagini per file
  PDF. Questo tutorial ti mostra come configurare le opzioni immagine di OpenAI, eseguire
  il copilot ed estrarre la descrizione dell'immagine in C#.
og_image_alt: Screenshot of C# code that creates an AI copilot for PDF image description
og_title: Crea un copilota AI per la descrizione di immagini PDF – guida completa
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Create AI Copilot to generate image description for PDF files. Learn
    how to configure OpenAI image options and extract image description efficiently.
  headline: Create AI Copilot for PDF image description – step‑by‑step guide
  type: TechArticle
tags:
- Aspose.Pdf.AI
- C#
- PDF processing
title: Crea un copilota AI per la descrizione delle immagini PDF – guida passo passo
url: /it/net/programming-with-images/create-ai-copilot-for-pdf-image-description-step-by-step-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crea AI Copilot per la descrizione delle immagini PDF – guida completa

Se hai bisogno di **create AI Copilot** che scriva automaticamente descrizioni per le immagini incorporate in un PDF, questa guida ti mostra esattamente come farlo. Imparerai a configurare le OpenAI image options, eseguire il copilot e **extract image description** senza uscire dal tuo progetto C#.

Generare contenuti testuali per le immagini PDF è una necessità comune per l'accessibilità, l'indicizzazione dei contenuti e la generazione automatica di report. Alla fine di questo tutorial avrai un componente riutilizzabile che **generates image description** per qualsiasi documento PDF a cui lo indirizzi.

## Prerequisiti

* .NET 6.0 o versioni successive installate  
* Una licenza Aspose.Pdf.AI (o una prova gratuita)  
* Una chiave OpenAI API che il client Aspose può utilizzare  
* Visual Studio 2022 (o qualsiasi IDE che supporti C#)  

Non sono richiesti pacchetti NuGet aggiuntivi oltre a `Aspose.Pdf.AI`.

## Passo 1: Configura il client Aspose.Pdf.AI

Il primo passo è istanziare il client AI con i tuoi dettagli di autenticazione. Il client gestisce la comunicazione con il servizio OpenAI in background.

```csharp
using Aspose.Pdf.AI;
using Aspose.Pdf.AI.Models;

// Replace with your actual credentials
var client = new AiClient(new AiClientOptions
{
    ApiKey = Environment.GetEnvironmentVariable("OPENAI_API_KEY"),
    // Optional: set a custom endpoint if you use Azure OpenAI
    // Endpoint = "https://my-openai-instance.openai.azure.com/"
});
```

**Perché è importante:** Il `AiClient` incapsula tutte le impostazioni a livello di richiesta (API key, timeout, retry policy). Crearlo una sola volta e riutilizzarlo in più istanze di copilot riduce l'overhead e garantisce un'autenticazione coerente.

## Passo 2: Crea un Image Description Copilot

Ora crei l'**AI copilot** che leggerà il PDF e produrrà una descrizione per ogni immagine. Il metodo factory `CreateImageDescriptionCopilot` accetta il client e un insieme di opzioni che definiscono come viene generata la descrizione.

```csharp
// Configure OpenAI image options – this is where you control model, temperature, etc.
var imageOptions = OpenAIImageDescriptionOptions.Create()
    .WithModel("gpt-4o-mini")           // Choose a model that balances cost and quality
    .WithTemperature(0.7)               // Controls creativity; 0 = deterministic
    .WithMaxTokens(150);                // Maximum length of each description

// Point the copilot at the PDF you want to process
var imgCopilot = AICopilotFactory.CreateImageDescriptionCopilot(
    client,
    imageOptions.WithDocument(@"C:\Reports\AnnualReport.pdf"));
```

**Perché è importante:**  
* `OpenAIImageDescriptionOptions` (le **OpenAI image options**) ti permettono di regolare finemente il modello linguistico. Modificare la temperatura o il modello può migliorare la pertinenza per diagrammi tecnici rispetto a foto naturali.  
* Specificare il percorso del documento indica al copilot quale PDF scansionare. Il copilot estrae ogni immagine raster, la invia al modello e restituisce una descrizione leggibile dall'uomo.

## Passo 3: Recupera la descrizione generata in modo asincrono

Il copilot funziona in modo asincrono perché potrebbe dover caricare diversi megabyte di dati immagine e attendere la risposta del modello. Usa `await` per assicurarti che la chiamata sia completata prima di accedere al risultato.

```csharp
try
{
    // Get a dictionary where the key is the page number and the value is the description
    var descriptionMap = await imgCopilot.GetDescriptionAsync();

    // Example: iterate over each image description
    foreach (var entry in descriptionMap)
    {
        Console.WriteLine($"Page {entry.Key}: {entry.Value}");
    }
}
catch (AiException ex)
{
    Console.Error.WriteLine($"AI service error: {ex.Message}");
}
```

**Perché è importante:** Il metodo restituisce un `Dictionary<int, string>` che mappa ogni pagina (o indice immagine) alla sua descrizione. Gestire `AiException` ti permette di segnalare errori di rete o di quota invece di far crashare l'applicazione.

## Passo 4: Visualizza o salva la descrizione

Puoi scrivere le descrizioni sulla console, su un file di log, o incorporarle nuovamente nel PDF come alt‑text per l'accessibilità. Di seguito trovi un esempio rapido che scrive l'output in un file JSON per un utilizzo successivo.

```csharp
using System.Text.Json;

// Serialize the map to JSON
var json = JsonSerializer.Serialize(descriptionMap, new JsonSerializerOptions { WriteIndented = true });
File.WriteAllText(@"C:\Reports\ImageDescriptions.json", json);

Console.WriteLine("Image descriptions saved to ImageDescriptions.json");
```

**Perché è importante:** Salvare l'output in JSON preserva l'associazione tra ogni pagina e la sua descrizione, facilitando il consumo dei dati da parte dei processi a valle (indicizzazione di ricerca, rendering UI, ecc.).

## Gestione di più immagini per pagina

Se una pagina contiene diverse immagini, il copilot restituisce una descrizione concatenata separata da interruzioni di riga. Per dividerle, ispeziona il risultato grezzo e suddividi su `\n\n` (doppio newline). Ecco un metodo di supporto:

```csharp
static IEnumerable<string> SplitDescriptions(string combined)
{
    return combined.Split(new[] { "\n\n" }, StringSplitOptions.RemoveEmptyEntries);
}
```

Puoi quindi iterare su ciascuna descrizione di immagine individuale e salvarla separatamente se necessario.

## Caso limite: PDF di grandi dimensioni e gestione del timeout

Elaborare un PDF più grande di 100 MB può superare i timeout HTTP predefiniti. Regola l'impostazione del timeout del client quando crei il `AiClient`:

```csharp
var client = new AiClient(new AiClientOptions
{
    ApiKey = Environment.GetEnvironmentVariable("OPENAI_API_KEY"),
    Timeout = TimeSpan.FromMinutes(5)   // Increase timeout for heavy workloads
});
```

Aumentare il timeout previene la terminazione prematura mentre il servizio elabora molte immagini ad alta risoluzione.

## Suggerimento professionale: Cache dei risultati per ridurre i costi

OpenAI addebita per token, e le descrizioni delle immagini possono essere ripetitive tra versioni dello stesso report. Metti in cache l'output JSON e riutilizzalo quando l'hash del PDF corrisponde a un file già elaborato. Questa pratica fa risparmiare denaro e velocizza le esecuzioni successive.

```csharp
static string ComputeFileHash(string path)
{
    using var sha256 = System.Security.Cryptography.SHA256.Create();
    using var stream = File.OpenRead(path);
    var hash = sha256.ComputeHash(stream);
    return Convert.ToHexString(hash);
}
```

Salva l'hash insieme al file JSON; se l'hash corrisponde in un'esecuzione successiva, salta la chiamata AI.

## Esempio completo eseguibile

Mettendo tutto insieme, ecco un'applicazione console autonoma che puoi incollare in un nuovo progetto .NET.

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using System.Text.Json;
using System.Threading.Tasks;
using Aspose.Pdf.AI;
using Aspose.Pdf.AI.Models;

class Program
{
    static async Task Main()
    {
        // 1️⃣ Initialize AI client
        var client = new AiClient(new AiClientOptions
        {
            ApiKey = Environment.GetEnvironmentVariable("OPENAI_API_KEY"),
            Timeout = TimeSpan.FromMinutes(5)
        });

        // 2️⃣ Configure OpenAI image options and create copilot
        var imageOptions = OpenAIImageDescriptionOptions.Create()
            .WithModel("gpt-4o-mini")
            .WithTemperature(0.7)
            .WithMaxTokens(150);

        string pdfPath = @"C:\Reports\AnnualReport.pdf";

        var imgCopilot = AICopilotFactory.CreateImageDescriptionCopilot(
            client,
            imageOptions.WithDocument(pdfPath));

        // 3️⃣ Retrieve descriptions
        Dictionary<int, string> descriptionMap;
        try
        {
            descriptionMap = await imgCopilot.GetDescriptionAsync();
        }
        catch (AiException ex)
        {
            Console.Error.WriteLine($"Error from AI service: {ex.Message}");
            return;
        }

        // 4️⃣ Output results
        foreach (var entry in descriptionMap)
        {
            Console.WriteLine($"Page {entry.Key}:");
            Console.WriteLine(entry.Value);
            Console.WriteLine(new string('-', 40));
        }

        // 5️⃣ Save to JSON for later use
        string json = JsonSerializer.Serialize(descriptionMap, new JsonSerializerOptions { WriteIndented = true });
        string jsonPath = Path.ChangeExtension(pdfPath, ".descriptions.json");
        await File.WriteAllTextAsync(jsonPath, json);
        Console.WriteLine($"Descriptions saved to {jsonPath}");
    }
}
```

**Output previsto (troncato)**

```
Page 2:
A bar chart showing quarterly revenue growth, with blue bars representing Q1–Q4.
----------------------------------------
Page 5:
A high‑resolution photograph of the new manufacturing facility, showing the assembly line in operation.
...
Descriptions saved to C:\Reports\AnnualReport.descriptions.json
```

Il programma legge `AnnualReport.pdf`, crea un **AI copilot** e scrive un file JSON che mappa ogni pagina alla sua descrizione generata.

## Domande frequenti

* **Questo funziona con PDF criptati?**  
  Sì, ma devi fornire la password quando crei il copilot:  
  `imageOptions.WithPassword("mySecret")`.

* **Posso limitare l'elaborazione a pagine specifiche?**  
  Usa `imageOptions.WithPageRange(1, 10)` per limitare il copilot alle pagine 1‑10.

* **Cosa succede se un'immagine contiene testo?**  
  Il modello tenta di descrivere il contenuto visivo; per l'estrazione di testo in stile OCR dovresti usare `CreateTextExtractionCopilot`.

## Conclusione

Ora sai come **create AI Copilot** che **generates image description** per file PDF, configurare le **OpenAI image options** e **extract image description** programmaticamente in C#. L'esempio completo dimostra le migliori pratiche come la gestione asincrona, la gestione degli errori e la cache dei risultati.

Next, you might explore:

* Aggiungere le descrizioni generate nuovamente nel PDF come alt‑text per migliorare l'accessibilità (`PdfDocument` → `PdfImage.AlternativeText`).  
* Utilizzare lo stesso modello di copilot per **generate image description PDF** report per l'elaborazione batch.  
* Sperimentare con diversi modelli OpenAI o impostazioni di temperatura per affinare lo stile della descrizione.

Sentiti libero di adattare il codice, sperimentare con documenti più grandi e integrare l'output nella tua pipeline di indicizzazione. Buon coding!

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Create Pdf With Tagged Image In Java](/pdf/hindi/java/pdf-structure-elements/create-pdf-with-tagged-image-in-java/)
- [Create Pdf With Tagged Image](/pdf/hindi/net/programming-with-tagged-pdf/create-pdf-with-tagged-image/)
- [Create Tagged Pdf Image Dotnet](/pdf/hindi/net/images-graphics/create-tagged-pdf-image-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}