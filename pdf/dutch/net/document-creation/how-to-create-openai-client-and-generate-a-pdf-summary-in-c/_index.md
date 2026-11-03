---
category: general
date: 2026-10-10
description: Maak een OpenAI‑client in C# en leer hoe je een PDF kunt samenvatten,
  een PDF naar samenvatting kunt converteren en de gegenereerde PDF‑samenvatting kunt
  opslaan met Aspose.Pdf.AI.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create openai client
- convert pdf to summary
- how to summarize pdf
- how to save summary
- generate pdf summary
language: nl
lastmod: 2026-10-10
og_description: Maak een OpenAI‑client in C# en leer direct hoe je een PDF kunt samenvatten,
  een PDF naar samenvatting kunt converteren en de gegenereerde PDF‑samenvatting kunt
  opslaan.
og_image_alt: Screenshot of C# code that creates an OpenAI client and generates a
  PDF summary
og_title: Maak een OpenAI-client en genereer een PDF‑samenvatting in C# – stapsgewijze
  handleiding
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
title: Hoe een OpenAI-client te maken en een PDF-samenvatting te genereren in C#
url: /nl/net/document-creation/how-to-create-openai-client-and-generate-a-pdf-summary-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe een OpenAI‑client te maken en een PDF‑samenvatting te genereren in C#

Als je een **OpenAI‑client wilt maken** in een .NET‑applicatie, laat deze tutorial je precies zien hoe je dat doet en hoe je elke PDF kunt omzetten in een beknopte, AI‑gegenereerde samenvatting. Je ziet hoe je **PDF naar samenvatting converteert**, de tekst ophaalt en **de samenvatting opslaat** als een nieuw PDF‑bestand — alles met Aspose.Pdf.AI.

Het samenvatten van PDF’s is een veelvoorkomende behoefte in document‑intensieve workflows, zoals juridische beoordelingen, onderzoeksaggregatie of geautomatiseerde rapportgeneratie. Aan het einde van deze gids kun je **PDF‑samenvatting genereren** programmatically, zonder je C#‑codebasis te verlaten.

## Wat je nodig hebt

- .NET 6.0 of later (het voorbeeld richt zich op .NET 6, maar elke recente .NET‑versie werkt)
- Een Aspose.Pdf.AI NuGet‑pakket (`Aspose.Pdf.AI`) — deze wrapper vereenvoudigt OpenAI‑aanroepen voor PDF‑inhoud
- Een geldige OpenAI‑API‑sleutel (verkrijg er één via het OpenAI‑portaal)
- Een voorbeeld‑PDF‑bestand dat je wilt samenvatten (bijv. `SampleDocument.pdf`)
- Visual Studio 2022, VS Code of een andere IDE die C#‑ontwikkeling ondersteunt

> **Pro tip:** Bewaar je API‑sleutel op een veilige locatie, zoals [user‑secrets](https://learn.microsoft.com/en-us/aspnet/core/security/app-secrets) of Azure Key Vault. Hard‑code deze nooit in source control.

## Stap 1: Installeer het Aspose.Pdf.AI NuGet‑pakket

Open een terminal in je projectmap en voer uit:

```bash
dotnet add package Aspose.Pdf.AI
```

Het pakket haalt de benodigde HTTP‑client, PDF‑manipulatietools en een dunne wrapper rond de OpenAI‑API op. Na de installatie herstel je het project om er zeker van te zijn dat alle afhankelijkheden beschikbaar zijn:

```bash
dotnet restore
```

## Stap 2: **OpenAI‑client maken** met je API‑sleutel

Het maken van de client is de eerste stap naar elke AI‑gedreven PDF‑bewerking. De `OpenAIClient` verzorgt authenticatie, request‑throttling en connection pooling voor jou.

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

> **Waarom dit belangrijk is:** De `using`‑statement garandeert dat de client correct wordt vrijgegeven, waardoor netwerkbronnen worden vrijgemaakt en socket‑uitputting in langdurige services wordt voorkomen.

## Stap 3: Samenvattingsopties configureren – **PDF omzetten naar samenvatting**

Het `OpenAISummaryCopilotOptions`‑object vertelt de AI wat er moet gebeuren. Je kunt de temperatuur aanpassen, het token‑gebruik beperken en, het belangrijkste, wijzen naar de bron‑PDF.

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

### Waarom temperatuur 0,5?

Een temperatuur van 0,5 levert beknopte, accurate taal op terwijl het model nog steeds zinnen kan herformuleren. Hogere waarden (bijv. 0,9) maken de output creatiever, maar kunnen afwijken van de oorspronkelijke betekenis — ongewenst voor juridische of technische samenvattingen.

## Stap 4: **Hoe PDF samen te vatten** – instantieer de copilot en haal de tekst op

Nu de client en opties klaar zijn, maak je een summary‑copilot. Dit object coördineert de aanvraag naar OpenAI en retourneert het resultaat in meerdere formaten.

```csharp
    // ---- Step 4: instantiate the summary copilot (how to summarize PDF) ----
    var summaryCopilot = AICopilotFactory
        .CreateSummaryCopilot(client, summaryOptions);

    // Retrieve the generated summary as plain text
    string summaryText = await summaryCopilot.GetSummaryAsync();

    Console.WriteLine("=== Text Summary ===");
    Console.WriteLine(summaryText);
```

De `GetSummaryAsync`‑methode geeft een schone, platte‑tekst versie terug die je kunt embedden in een UI, per e‑mail kunt versturen of in een database kunt opslaan.

## Stap 5: Haal de samenvatting op als PDF‑document

Als je een draagbare, afdrukbare versie nodig hebt, vraag dan de copilot om een PDF‑document. Deze stap demonstreert **PDF‑samenvatting genereren** direct vanuit het AI‑model.

```csharp
    // ---- Step 5: retrieve the summary as a PDF document (generate PDF summary) ----
    Document summaryDocument = await summaryCopilot.GetSummaryDocumentAsync();

    // Optionally, you can add a cover page or watermark here before saving.
```

Het geretourneerde `Aspose.Pdf.Document` gedraagt zich als elk ander PDF‑object in het Aspose‑ecosysteem, wat betekent dat je pagina’s kunt bewerken, metadata kunt toevoegen of kunt samenvoegen met andere PDF’s.

## Stap 6: **Hoe samenvatting op te slaan** – bewaar de PDF op schijf

Tot slot sla je de gegenereerde samenvatting op het bestandssysteem op. De `SaveSummaryAsync`‑helper combineert ophalen en opslaan in één aanroep, maar we laten ook de expliciete opslaan‑stap zien voor de volledigheid.

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

> **Tip:** Als je een naamgevingsconventie moet afdwingen (bijv. tijdstempel‑bestanden), bouw dan het pad programmatisch op met `DateTime.UtcNow:yyyyMMdd_HHmmss`.

### Volledig uitvoerbaar voorbeeld

Alles bij elkaar, hier is een zelfstandige applicatie die je kunt kopiëren‑plakken in `Program.cs` en uitvoeren:

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

Het uitvoeren van het programma levert twee artefacten:

1. **Console‑output** — de platte‑tekst samenvatting die op het scherm wordt weergegeven.
2. **`Summary_out.pdf`** — een downloadbare PDF met dezelfde samenvatting, klaar voor distributie.

## Veelvoorkomende variaties en randgevallen

| Situatie | Aanbevolen aanpassing |
|-----------|-------------------|
| **Grote PDF’s (> 10 MB)** | Splits het document in kleinere delen (bijv. per hoofdstuk) en vat elk deel afzonderlijk samen. Combineer de resultaten met `Document.AppendDocument`. |
| **Aangepaste prompt nodig** | Gebruik `WithPrompt("Summarize the following legal contract in bullet points:")` vóór het aanroepen van `CreateSummaryCopilot`. |
| **Bron‑PDF in een andere taal** | Stel `WithLanguage("es")` (of de juiste ISO‑code) in om de taalverwerking van het model te sturen. |
| **Rate‑limit‑fouten** | Verhoog de `WithRetryCount` of voeg een `Task.Delay` toe tussen de calls. |
| **Opslaan naar cloudopslag** | Vervang het bestandssysteem‑pad door een stream (`MemoryStream`) en upload de stream naar Azure Blob Storage of AWS S3. |

## Het resultaat verifiëren

Na afloop van het programma open je `Summary_out.pdf` in een PDF‑viewer. Je zou een schone, één‑pagina (of meerdere pagina’s, afhankelijk van de lengte) moeten zien die de hoofdideeën van `SampleDocument.pdf` samenvat. Vergelijk de tekstsamenvatting die op de console wordt afgedrukt met de PDF‑versie — beide moeten letterlijk overeenkomen.

Als de samenvatting onvolledig lijkt:

1. Verlaag de `WithTemperature` naar 0,2 voor een meer deterministische output.
2. Verhoog de

## Wat kun je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap‑uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Hoe PDF maken in C# – Pagina toevoegen, rechthoek tekenen & opslaan](/pdf/english/net/document-creation/how-to-create-pdf-in-c-add-page-draw-rectangle-save/)
- [Leer hoe PDF‑documenten te genereren met Aspose.PDF voor .NET](/pdf/english/net/document-creation/)
- [Hoe getagde PDF’s te maken met Aspose.PDF voor .NET – Toegankelijkheid verbeteren](/pdf/english/net/bookmarks-navigation/tagged-pdf-creation-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}