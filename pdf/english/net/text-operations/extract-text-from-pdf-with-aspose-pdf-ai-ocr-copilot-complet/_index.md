---
category: general
date: 2025-12-22
description: Learn how to extract text from PDF and recognize text from JPG using
  Aspose.Pdf.AI. This tutorial shows you how to run OCR on document files in C#.
draft: false
keywords:
- extract text from pdf
- recognize text from jpg
- run OCR on document
- extract scanned text
- process image with OCR
language: en
og_description: Extract text from PDF instantly. This guide walks you through recognizing
  text from JPG and running OCR on any document using Aspose.Pdf.AI in C#.
og_title: Extract Text from PDF with Aspose.Pdf.AI – Full Guide
tags:
- OCR
- C#
- Aspose
title: Extract Text from PDF with Aspose.Pdf.AI OCR Copilot – Complete Step‑by‑Step
  Guide
url: /net/text-operations/extract-text-from-pdf-with-aspose-pdf-ai-ocr-copilot-complet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extract Text from PDF with Aspose.Pdf.AI OCR Copilot – Complete Step‑by‑Step Guide

Ever needed to **extract text from PDF** files but the content is locked inside a scanned image? You’re not the only one hitting that wall. In many real‑world apps—think invoice processing, legal document archiving, or a simple search feature—you must **run OCR on document** assets before you can index or analyze them.  

In this tutorial we’ll walk through exactly how to extract text from PDF, recognize text from JPG, and generally **process image with OCR** using the Aspose.Pdf.AI library. By the end you’ll have a ready‑to‑run C# console app that pulls every line of readable text out of your scanned PDFs and image files.

## What You’ll Learn

- How to set up the Aspose.Pdf.AI OpenAI client with your API key.  
- Configuring the OCR copilot to handle both PDF and JPG inputs.  
- Running the OCR operation asynchronously and retrieving **extract scanned text** results.  
- Common pitfalls (large files, multi‑page PDFs, missing OCR details) and how to avoid them.  
- Quick ways to swap the model if you need higher accuracy or a lower cost.  

### Prerequisites

- .NET 6.0 or later (the example uses the modern `async Main` pattern).  
- An Aspose.Pdf.AI account with a valid API key.  
- Basic familiarity with C# async/await.  

If you already have those pieces in place, great—let’s dive in.

![Screenshot of extracted text from PDF using Aspose.Pdf.AI OCR Copilot – shows the primary keyword extract text from PDF in the result pane](extract-text-from-pdf-screenshot.png "extract text from PDF result screenshot")

## Step 1 – Initialize the OpenAI Client to **Extract Text from PDF**

Before any OCR can happen, you need a client that knows how to talk to Aspose’s cloud services. The client holds your API key and handles authentication for every request.

```csharp
using System;
using System.Collections.Generic;
using System.Threading.Tasks;
using Aspose.Pdf.AI;
using Aspose.Pdf.AI.OpenAI;

class Program
{
    // Async Main entry point (C# 9+)
    static async Task Main(string[] args)
    {
        // Replace with your real key – keep it secret!
        var apiKey = "YOUR_API_KEY";

        // The `using var` pattern ensures the client is disposed properly.
        await using var aiClient = OpenAIClient
            .CreateWithApiKey(apiKey)
            .Build();

        // The rest of the steps follow here...
```

**Why this matters:** The `OpenAIClient` abstracts token handling, retries, and request throttling. Skipping this step would force you to manually craft HTTP calls, which is error‑prone and defeats the purpose of a high‑level SDK.

## Step 2 – Configure OCR Copilot Options (including **recognize text from JPG**)

Now we tell the copilot what files to scan. The same options object can hold multiple documents, so you can **process image with OCR** in a single request.

```csharp
        // Build OCR options – we’ll feed both a PDF and a JPG.
        var ocrOptions = OpenAIOcrCopilotOptions
            .Create()
            .WithModel(OpenAIModels.Gpt4OMini) // Vision‑capable, cost‑effective model
            .WithDocument("YOUR_DIRECTORY/ScannedDocument.pdf")
            .WithDocument("YOUR_DIRECTORY/ImageWithText.jpg");
```

**Why this matters:** Selecting `Gpt4OMini` gives you a vision‑enabled model that can read raster images inside PDFs as well as standalone JPGs. If your workload demands higher accuracy (e.g., legal contracts), you could swap to `Gpt4TurboVision`. The `WithDocument` calls are additive, meaning you can keep adding files until you hit the service‑specific size limit.

## Step 3 – Create the OCR Copilot Instance

With the client and options ready, we instantiate the copilot. Think of the copilot as a specialized service worker that knows exactly how to run OCR for you.

```csharp
        // Create the OCR copilot using the client and the options we just built.
        IOcrCopilot ocrCopilot = AICopilotFactory
            .CreateOcrCopilot(aiClient, ocrOptions);
```

**Why this matters:** The factory pattern isolates the creation logic, allowing Aspose to inject future enhancements (like batch processing) without breaking your code. It also guarantees that the copilot is bound to the same `aiClient` instance, preserving authentication context.

## Step 4 – Run OCR Asynchronously and Gather Results

The heavy lifting happens here. The call streams the document to the cloud, runs vision models, and returns a list of `TextRecognitionResult` objects.

```csharp
        // Execute OCR and wait for the results.
        List<TextRecognitionResult> recognitionResults =
            await ocrCopilot.GetTextRecognitionResultAsync();

        // Simple guard in case nothing was returned.
        if (recognitionResults == null || recognitionResults.Count == 0)
        {
            Console.WriteLine("No OCR results were returned. Check your files and model selection.");
            return;
        }
```

**Why this matters:** Using `await` ensures your UI (if you later migrate this to a desktop app) stays responsive. The guard clause prevents a null‑reference crash—a common edge case when the service times out or the input file is corrupted.

## Step 5 – Extract the Recognized Text (the **extract scanned text** part)

Each `TextRecognitionResult` contains one or more `OcrDetails` objects. The first detail usually holds the raw string output, but you can iterate over all pages if you need per‑page granularity.

```csharp
        // Pull the extracted text from the first result (you can loop for multi‑page PDFs).
        string extractedText = recognitionResults[0].OcrDetails[0].ExtractedText;

        // Output to console – in a real app you’d write to a DB or file.
        Console.WriteLine("=== Extracted Text Start ===");
        Console.WriteLine(extractedText);
        Console.WriteLine("=== Extracted Text End ===");
    }
}
```

**Why this matters:** The `ExtractedText` property is the final, human‑readable string you were after. If you need to **extract text from PDF** across many pages, simply loop through `recognitionResults` and concatenate each `ExtractedText`. That way you turn a multi‑page scan into a single searchable blob.

### Full Working Example (Copy‑Paste Ready)

Putting all the snippets together, here's a self‑contained program you can drop into a new console project:

```csharp
using System;
using System.Collections.Generic;
using System.Threading.Tasks;
using Aspose.Pdf.AI;
using Aspose.Pdf.AI.OpenAI;

class Program
{
    static async Task Main(string[] args)
    {
        // 1️⃣ Initialize the client
        var apiKey = "YOUR_API_KEY";
        await using var aiClient = OpenAIClient
            .CreateWithApiKey(apiKey)
            .Build();

        // 2️⃣ Configure OCR options (PDF + JPG)
        var ocrOptions = OpenAIOcrCopilotOptions
            .Create()
            .WithModel(OpenAIModels.Gpt4OMini)
            .WithDocument("YOUR_DIRECTORY/ScannedDocument.pdf")
            .WithDocument("YOUR_DIRECTORY/ImageWithText.jpg");

        // 3️⃣ Create the OCR copilot
        IOcrCopilot ocrCopilot = AICopilotFactory
            .CreateOcrCopilot(aiClient, ocrOptions);

        // 4️⃣ Run OCR
        List<TextRecognitionResult> results =
            await ocrCopilot.GetTextRecognitionResultAsync();

        if (results == null || results.Count == 0)
        {
            Console.WriteLine("No results – double‑check your files and API key.");
            return;
        }

        // 5️⃣ Extract and display the text
        string extracted = results[0].OcrDetails[0].ExtractedText;
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(extracted);
    }
}
```

Run the program (`dotnet run`) and watch the console print every line the model could read from your scanned PDF and JPG. Easy, right?

## Frequently Asked Questions & Edge Cases

| Question | Answer |
|----------|--------|
| **What if my PDF has 100+ pages?** | The API returns one `TextRecognitionResult` per input file, not per page. Each result’s `OcrDetails` array contains a separate entry for every page, so you can loop through `result.OcrDetails` to handle large documents. |
| **Can I change the model after the copilot is created?** | Not directly. You must rebuild the `OpenAIOcrCopilotOptions` with a different `WithModel` call and recreate the copilot. This is cheap because the heavy work only happens on the `GetTextRecognitionResultAsync` call. |
| **My images are low‑resolution – will OCR still work?** | Vision models need at least 300 dpi for reliable character recognition. If you’re stuck with lower resolution, consider pre‑processing the images (sharpen, upscale) before feeding them to the copilot. |
| **How do I handle non‑Latin scripts?** | Aspose.Pdf.AI supports multilingual OCR out of the box, but you may need to set the `WithLanguage` option (e.g., `.WithLanguage("ja")`) to improve accuracy for Japanese, Cyrillic, etc. |
| **Is there a way to get confidence scores?** | Each `OcrDetail` contains a `Confidence` property (0‑1 range). You can log it to decide whether to flag low‑confidence lines for manual review. |

## Pro Tips & Best Practices

- **Batch files wisely:** The service imposes a maximum payload size (usually ~50 MB). Group smaller PDFs together to reduce round‑trips, but keep each request under the limit.
- **Cache API keys securely:** Use environment variables or Azure Key Vault instead of hard‑coding the key.
- **Parallelize when safe:**

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}