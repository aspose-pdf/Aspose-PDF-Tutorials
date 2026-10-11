---
category: general
date: 2026-10-10
description: Create OpenAI client in C# and learn how to summarize a PDF, convert
  PDF to summary, and save the generated PDF summary with Aspose.Pdf.AI.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create openai client
- convert pdf to summary
- how to summarize pdf
- how to save summary
- generate pdf summary
language: en
lastmod: 2026-10-10
og_description: Create OpenAI client in C# and instantly learn how to summarize a
  PDF, convert PDF to summary, and save the generated PDF summary.
og_image_alt: Screenshot of C# code that creates an OpenAI client and generates a
  PDF summary
og_title: Create OpenAI client and generate a PDF summary in C# – step‑by‑step guide
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
title: How to create OpenAI client and generate a PDF summary in C#
url: /net/document-creation/how-to-create-openai-client-and-generate-a-pdf-summary-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to create OpenAI client and generate a PDF summary in C#

If you need to **create OpenAI client** in a .NET application, this tutorial shows you exactly how to do it and how to turn any PDF into a concise, AI‑generated summary. You’ll see how to **convert PDF to summary**, retrieve the text, and **save the summary** as a new PDF file—all with Aspose.Pdf.AI.

Summarizing PDFs is a common requirement for document‑heavy workflows such as legal review, research aggregation, or automated report generation. By the end of this guide you will be able to **generate PDF summary** programmatically, without leaving your C# codebase.

## What you’ll need

- .NET 6.0 or later (the example targets .NET 6, but any recent .NET version works)
- An Aspose.Pdf.AI NuGet package (`Aspose.Pdf.AI`) – this wrapper simplifies OpenAI calls for PDF content
- A valid OpenAI API key (you can obtain one from the OpenAI portal)
- A sample PDF file you want to summarize (e.g., `SampleDocument.pdf`)
- Visual Studio 2022, VS Code, or any IDE that supports C# development

> **Pro tip:** Keep your API key in a secure location such as [user‑secrets](https://learn.microsoft.com/en-us/aspnet/core/security/app-secrets) or Azure Key Vault. Never hard‑code it in source control.

## Step 1: Install the Aspose.Pdf.AI NuGet package

Open a terminal in your project folder and run:

```bash
dotnet add package Aspose.Pdf.AI
```

The package pulls in the necessary HTTP client, PDF manipulation tools, and a thin wrapper around the OpenAI API. After the installation, restore the project to ensure all dependencies are available:

```bash
dotnet restore
```

## Step 2: **Create OpenAI client** with your API key

Creating the client is the first step toward any AI‑driven PDF operation. The `OpenAIClient` handles authentication, request throttling, and connection pooling for you.

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

> **Why this matters:** The `using` statement guarantees the client is disposed properly, releasing network resources and avoiding socket exhaustion in long‑running services.

## Step 3: Configure summary options – **convert PDF to summary**

The `OpenAISummaryCopilotOptions` object tells the AI what to do. You can adjust the temperature, limit token usage, and, most importantly, point to the source PDF.

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

### Why temperature 0.5?

A temperature of 0.5 produces concise, accurate language while still allowing the model to re‑phrase sentences. Higher values (e.g., 0.9) make the output more creative but can drift from the original meaning—undesirable for legal or technical summaries.

## Step 4: **How to summarize PDF** – instantiate the copilot and get the text

Now that the client and options are ready, create a summary copilot. This object orchestrates the request to OpenAI and returns the result in multiple formats.

```csharp
    // ---- Step 4: instantiate the summary copilot (how to summarize PDF) ----
    var summaryCopilot = AICopilotFactory
        .CreateSummaryCopilot(client, summaryOptions);

    // Retrieve the generated summary as plain text
    string summaryText = await summaryCopilot.GetSummaryAsync();

    Console.WriteLine("=== Text Summary ===");
    Console.WriteLine(summaryText);
```

The `GetSummaryAsync` method returns a clean, plain‑text version you can embed in UI, send via email, or store in a database.

## Step 5: Retrieve the summary as a PDF document

If you need a portable, printable version, ask the copilot for a PDF document. This step demonstrates **generate PDF summary** directly from the AI model.

```csharp
    // ---- Step 5: retrieve the summary as a PDF document (generate PDF summary) ----
    Document summaryDocument = await summaryCopilot.GetSummaryDocumentAsync();

    // Optionally, you can add a cover page or watermark here before saving.
```

The returned `Aspose.Pdf.Document` behaves like any other PDF object in the Aspose ecosystem, meaning you can further edit pages, add metadata, or merge with other PDFs.

## Step 6: **How to save summary** – persist the PDF to disk

Finally, store the generated summary on the file system. The `SaveSummaryAsync` helper combines retrieval and saving in one call, but we’ll also show the explicit save for completeness.

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

> **Tip:** If you need to enforce a naming convention (e.g., timestamped files), build the path programmatically with `DateTime.UtcNow:yyyyMMdd_HHmmss`.

### Full runnable example

Putting everything together, here’s a self‑contained program you can copy‑paste into `Program.cs` and run:

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

Running the program produces two artifacts:

1. **Console output** – the plain‑text summary displayed on the screen.
2. **`Summary_out.pdf`** – a downloadable PDF containing the same summary, ready for distribution.

## Common variations and edge cases

| Situation | Recommended tweak |
|-----------|-------------------|
| **Large PDFs (> 10 MB)** | Split the document into smaller chunks (e.g., per chapter) and summarize each chunk separately. Combine the results with `Document.AppendDocument`. |
| **Need a custom prompt** | Use `WithPrompt("Summarize the following legal contract in bullet points:")` before calling `CreateSummaryCopilot`. |
| **Non‑English source PDF** | Set `WithLanguage("es")` (or the appropriate ISO code) to guide the model’s language handling. |
| **Rate‑limit errors** | Increase the `WithRetryCount` or add a `Task.Delay` between calls. |
| **Saving to a cloud storage** | Replace the file‑system path with a stream (`MemoryStream`) and upload the stream to Azure Blob Storage or AWS S3. |

## Verifying the result

After the program finishes, open `Summary_out.pdf` in any PDF viewer. You should see a clean, one‑page (or multi‑page, depending on length) document that captures the main ideas of `SampleDocument.pdf`. Compare the text summary printed to the console with the PDF version—both should match verbatim.

If the summary appears incomplete:

1. Lower the `WithTemperature` to 0.2 for more deterministic output.
2. Increase the


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Create PDF in C# – Add Page, Draw Rectangle & Save](/pdf/english/net/document-creation/how-to-create-pdf-in-c-add-page-draw-rectangle-save/)
- [Learn How to Generate PDF Documents with Aspose.PDF for .NET](/pdf/english/net/document-creation/)
- [How to Create Tagged PDFs with Aspose.PDF for .NET – Enhance Accessibility](/pdf/english/net/bookmarks-navigation/tagged-pdf-creation-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}