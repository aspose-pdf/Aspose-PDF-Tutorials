---
category: general
date: 2026-08-04
description: Create AI Copilot to generate image description for PDF files. Learn
  how to configure OpenAI image options and extract image description efficiently.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create AI copilot
- generate image description
- image description PDF
- OpenAI image options
- extract image description
language: en
lastmod: 2026-08-04
og_description: Create AI Copilot to generate image description for PDF files. This
  tutorial shows you how to configure OpenAI image options, run the copilot, and extract
  image description in C#.
og_image_alt: Screenshot of C# code that creates an AI copilot for PDF image description
og_title: Create AI Copilot for PDF image description – complete guide
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
title: Create AI Copilot for PDF image description – step‑by‑step guide
url: /net/programming-with-images/create-ai-copilot-for-pdf-image-description-step-by-step-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create AI Copilot for PDF image description – complete guide

If you need to **create AI Copilot** that automatically writes descriptions for images embedded in a PDF, this guide shows you exactly how to do it. You’ll learn to configure the OpenAI image options, run the copilot, and **extract image description** without leaving your C# project.

Generating textual content for PDF images is a common requirement for accessibility, content indexing, and automated reporting. By the end of this tutorial you will have a reusable component that **generates image description** for any PDF document you point it at.

## Prerequisites

Before you start, make sure you have:

* .NET 6.0 or later installed  
* An Aspose.Pdf.AI license (or a free trial)  
* An OpenAI API key that the Aspose client can use  
* Visual Studio 2022 (or any IDE that supports C#)  

No additional NuGet packages are required beyond `Aspose.Pdf.AI`.

## Step 1: Set up the Aspose.Pdf.AI client

The first step is to instantiate the AI client with your authentication details. The client handles communication with the OpenAI service behind the scenes.

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

**Why this matters:** The `AiClient` encapsulates all request‑level settings (API key, timeout, retry policy). Creating it once and reusing it across multiple copilot instances reduces overhead and ensures consistent authentication.

## Step 2: Create an Image Description Copilot

Now you create the **AI copilot** that will read the PDF and produce a description for each image. The `CreateImageDescriptionCopilot` factory method accepts the client and a set of options that define how the description is generated.

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

**Why this matters:**  
* `OpenAIImageDescriptionOptions` (the **OpenAI image options**) let you fine‑tune the language model. Adjusting temperature or model can improve relevance for technical diagrams versus natural photos.  
* Specifying the document path tells the copilot which PDF to scan. The copilot extracts every raster image, sends it to the model, and returns a human‑readable description.

## Step 3: Retrieve the generated description asynchronously

The copilot works asynchronously because it may need to upload several megabytes of image data and wait for the model’s response. Use `await` to ensure the call completes before you access the result.

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

**Why this matters:** The method returns a `Dictionary<int, string>` that maps each page (or image index) to its description. Handling `AiException` lets you surface network or quota errors instead of crashing the application.

## Step 4: Display or store the description

You can write the descriptions to the console, a log file, or embed them back into the PDF as alt‑text for accessibility. Below is a quick example that writes the output to a JSON file for later consumption.

```csharp
using System.Text.Json;

// Serialize the map to JSON
var json = JsonSerializer.Serialize(descriptionMap, new JsonSerializerOptions { WriteIndented = true });
File.WriteAllText(@"C:\Reports\ImageDescriptions.json", json);

Console.WriteLine("Image descriptions saved to ImageDescriptions.json");
```

**Why this matters:** Storing the output as JSON preserves the association between each page and its description, making it easy for downstream processes (search indexing, UI rendering, etc.) to consume the data.

## Handling multiple images per page

If a page contains several images, the copilot returns a concatenated description separated by line breaks. To split them, inspect the raw result and split on `\n\n` (double newline). Here’s a helper method:

```csharp
static IEnumerable<string> SplitDescriptions(string combined)
{
    return combined.Split(new[] { "\n\n" }, StringSplitOptions.RemoveEmptyEntries);
}
```

You can then iterate over each individual image description and store them separately if needed.

## Edge case: Large PDFs and timeout management

Processing a PDF larger than 100 MB may exceed default HTTP timeouts. Adjust the client’s timeout setting when you create the `AiClient`:

```csharp
var client = new AiClient(new AiClientOptions
{
    ApiKey = Environment.GetEnvironmentVariable("OPENAI_API_KEY"),
    Timeout = TimeSpan.FromMinutes(5)   // Increase timeout for heavy workloads
});
```

Increasing the timeout prevents premature termination while the service processes many high‑resolution images.

## Pro tip: Cache results to reduce cost

OpenAI charges per token, and image description can be repetitive across versions of the same report. Cache the JSON output and reuse it when the PDF hash matches a previously processed file. This practice saves money and speeds up subsequent runs.

```csharp
static string ComputeFileHash(string path)
{
    using var sha256 = System.Security.Cryptography.SHA256.Create();
    using var stream = File.OpenRead(path);
    var hash = sha256.ComputeHash(stream);
    return Convert.ToHexString(hash);
}
```

Store the hash alongside the JSON file; if the hash matches on a later run, skip the AI call.

## Full runnable example

Putting everything together, here is a self‑contained console application you can paste into a new .NET project.

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

**Expected output (truncated)**

```
Page 2:
A bar chart showing quarterly revenue growth, with blue bars representing Q1–Q4.
----------------------------------------
Page 5:
A high‑resolution photograph of the new manufacturing facility, showing the assembly line in operation.
...
Descriptions saved to C:\Reports\AnnualReport.descriptions.json
```

The program reads `AnnualReport.pdf`, creates an **AI copilot**, and writes a JSON file that maps each page to its generated description.

## Common questions

* **Does this work with encrypted PDFs?**  
  Yes, but you must provide the password when creating the copilot:  
  `imageOptions.WithPassword("mySecret")`.

* **Can I limit processing to specific pages?**  
  Use `imageOptions.WithPageRange(1, 10)` to restrict the copilot to pages 1‑10.

* **What if an image contains text?**  
  The model attempts to describe visual content; for OCR‑style text extraction you should use `CreateTextExtractionCopilot` instead.

## Conclusion

You now know how to **create AI Copilot** that **generates image description** for PDF files, configure **OpenAI image options**, and **extract image description** programmatically in C#. The complete example demonstrates best practices such as async handling, error management, and result caching.

Next, you might explore:

* Adding the generated descriptions back into the PDF as alt‑text for improved accessibility (`PdfDocument` → `PdfImage.AlternativeText`).  
* Using the same copilot pattern to **generate image description PDF** reports for batch processing.  
* Experimenting with different OpenAI models or temperature settings to fine‑tune description style.

Feel free to adapt the code, experiment with larger documents, and integrate the output into your indexing pipeline. Happy coding!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Create Pdf With Tagged Image In Java](/pdf/hindi/java/pdf-structure-elements/create-pdf-with-tagged-image-in-java/)
- [Create Pdf With Tagged Image](/pdf/hindi/net/programming-with-tagged-pdf/create-pdf-with-tagged-image/)
- [Create Tagged Pdf Image Dotnet](/pdf/hindi/net/images-graphics/create-tagged-pdf-image-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}