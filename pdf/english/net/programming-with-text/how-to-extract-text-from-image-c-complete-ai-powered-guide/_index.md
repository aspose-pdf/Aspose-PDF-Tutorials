---
category: general
date: 2025-12-22
description: Learn how to extract text from image C# using Aspose.Pdf.AI and OpenAI.
  This tutorial also covers extract text from pdf using AI and extract text from scanned
  pdf in a single workflow.
draft: false
keywords:
- how to extract text from image c#
- extract text from pdf using ai
- extract text from scanned pdf
- ocr c# tutorial
- aspnet pdf ai
language: en
og_description: How to extract text from image C# using Aspose.Pdf.AI. Follow this
  step‑by‑step guide to also extract text from pdf using AI and from scanned pdf files.
og_title: How to Extract Text from Image C# – AI‑Powered OCR Tutorial
tags:
- C#
- OCR
- AI
- Aspose.Pdf.AI
title: How to Extract Text from Image C# – Complete AI‑Powered Guide
url: /net/programming-with-text/how-to-extract-text-from-image-c-complete-ai-powered-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Extract Text from Image C# – Complete AI‑Powered Guide

Ever wondered **how to extract text from image C#** without wrestling with low‑level pixel analysis? You're not alone. Many developers hit a wall when a PDF or JPEG comes in scanned, and the usual string‑search tricks fall flat. The good news? With Aspose.Pdf.AI and OpenAI’s vision models, the whole process becomes a few lines of code.

In this tutorial we’ll walk through a real‑world solution that not only shows **how to extract text from image C#**, but also demonstrates **extract text from pdf using AI** and **extract text from scanned pdf** in one seamless flow. By the end you’ll have a ready‑to‑run console app, a handful of practical tips, and a clear picture of where to go next.

## What You’ll Learn

- Set up the Aspose.Pdf.AI NuGet package and OpenAI credentials.  
- Configure the OCR copilot to handle both PDF and image inputs.  
- Retrieve and parse the OCR results, extracting clean text strings.  
- Handle common edge cases such as multi‑page PDFs, language selection, and error handling.  

### Prerequisites

| Requirement | Why it matters |
|-------------|----------------|
| .NET 6.0+ (or .NET Core 3.1) | Modern APIs and async/await support. |
| An Aspose.Pdf.AI license (free trial works) | Needed for the SDK components. |
| OpenAI API key | Powers the vision‑capable model (GPT‑4‑o‑mini). |
| Visual Studio 2022 or VS Code | Any IDE will do, but these make debugging easier. |

If you have those pieces in place, let’s dive in.

## Step 1 – Install the Aspose.Pdf.AI NuGet Package

First, add the SDK to your project. Open a terminal in the solution folder and run:

```bash
dotnet add package Aspose.Pdf.AI
```

> **Pro tip:** The package pulls in `System.Text.Json` and `Microsoft.Extensions.Http` automatically, so you don’t need extra references.

## Step 2 – Create a Simple Console Skeleton

Below is a minimal program that holds the async entry point. Notice the `using` statements at the top – they keep the code tidy and avoid fully‑qualified names later.

```csharp
using System;
using System.Collections.Generic;
using System.Threading.Tasks;
using Aspose.Pdf.AI;
using Aspose.Pdf.AI.OpenAI;
using Aspose.Pdf.AI.IOcr;

namespace OcrDemo
{
    class Program
    {
        static async Task Main(string[] args)
        {
            await ExtractTextAsync();
        }

        // The method that implements the full OCR workflow – see next steps.
        private static async Task ExtractTextAsync()
        {
            // implementation will be inserted here
        }
    }
}
```

Save this as `Program.cs`. The `ExtractTextAsync` method will host the core logic we’ll flesh out moment‑by‑moment.

## Step 3 – Initialise the OpenAI Client

Inside `ExtractTextAsync`, the first thing we do is spin up an OpenAI client that knows your API key. The client is disposable, so we wrap it in a `using` block.

```csharp
// Step 3: Initialise the OpenAI client
string openAiKey = "YOUR_API_KEY"; // <-- replace with your real key
using var openAiClient = OpenAIClient
    .CreateWithApiKey(openAiKey)
    .Build();
```

> **Why this matters:** The client handles authentication, retries, and throttling for you, so you don’t have to reinvent HTTP plumbing.

## Step 4 – Configure OCR Copilot Options

Now we tell the SDK which documents we want to process and which model should do the heavy lifting. The example below covers **how to extract text from image C#** as well as **extract text from scanned pdf**.

```csharp
// Step 4: Configure OCR options – add both image and PDF inputs
string inputFolder = @"YOUR_DIRECTORY\"; // <-- adjust to your folder
var ocrOptions = OpenAIOcrCopilotOptions
    .Create()
    .WithModel(OpenAIModels.Gpt4OMini) // vision‑capable, cost‑effective
    .WithDocument($"{inputFolder}ScannedDocument.pdf")
    .WithDocument($"{inputFolder}ImageWithText.jpg");
```

If you have more files, simply chain additional `.WithDocument(...)` calls. The SDK will treat each file as a separate “task” and return results in the same order.

## Step 5 – Build the OCR Copilot

The copilot is the orchestrator that talks to OpenAI, streams the image data, and parses the response into a strongly‑typed object.

```csharp
// Step 5: Create the OCR copilot using the client and the options
IOcrCopilot ocrCopilot = AICopilotFactory
    .CreateOcrCopilot(openAiClient, ocrOptions);
```

> **Note:** `IOcrCopilot` implements `IAsyncDisposable`, but because we’re using it only inside this method, we don’t need an extra `using`. The underlying HTTP connections are closed when the method finishes.

## Step 6 – Run the OCR and Collect Results

Now we actually call the service. The method returns a list where each element corresponds to one input file.

```csharp
// Step 6: Run OCR asynchronously
List<TextRecognitionResult> results = await ocrCopilot.GetTextRecognitionResultAsync();
```

Each `TextRecognitionResult` contains a collection of `OcrDetails`. The first detail usually holds the extracted plain text, but you can explore confidence scores, bounding boxes, and language hints if you need them.

## Step 7 – Extract Clean Text from the Results

Finally, we pull out the strings and display them. The snippet below prints the text for each file, labeling it appropriately.

```csharp
// Step 7: Loop through results and output extracted text
for (int i = 0; i < results.Count; i++)
{
    var fileResult = results[i];
    string sourceFile = ocrOptions.Documents[i]; // the path we passed earlier

    // Most OCR services return a single OcrDetail per page; we concatenate them.
    string combinedText = string.Empty;
    foreach (var detail in fileResult.OcrDetails)
    {
        combinedText += detail.ExtractedText + Environment.NewLine;
    }

    Console.WriteLine($"--- Extracted text from: {sourceFile} ---");
    Console.WriteLine(combinedText);
}
```

Running the program should produce console output similar to:

```
--- Extracted text from: C:\MyFiles\ScannedDocument.pdf ---
Lorem ipsum dolor sit amet, consectetur ...

--- Extracted text from: C:\MyFiles\ImageWithText.jpg ---
Invoice #12345
Date: 2025‑12‑01
Total: $1,250.00
```

That’s the core workflow for **how to extract text from image C#**, and you’ve simultaneously learned **extract text from pdf using AI** and **extract text from scanned pdf**.

## Edge Cases & Practical Tips

### Multi‑Page PDFs

If your PDF has more than one page, Aspose will return an `OcrDetail` for each page. The loop above already concatenates them, but you may want to insert page separators:

```csharp
combinedText += $"[Page {detail.PageNumber}]{Environment.NewLine}";
combinedText += detail.ExtractedText + Environment.NewLine;
```

### Language Support

OpenAI’s vision models auto‑detect language, yet you can improve accuracy by adding a prompt hint:

```csharp
.WithPrompt("Please OCR the document and return the text in English.")
```

### Handling Large Files

The SDK streams data, but extremely large PDFs (>50 MB) can hit request‑size limits. In such cases, split the document into smaller chunks (e.g., per 10 pages) before sending.

### Error Handling

Wrap the OCR call in a `try/catch` block to surface network or quota errors:

```csharp
try
{
    var results = await ocrCopilot.GetTextRecognitionResultAsync();
    // process results...
}
catch (OpenAIException ex)
{
    Console.Error.WriteLine($"OpenAI error: {ex.Message}");
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Unexpected error: {ex}");
}
```

### Saving Results to a File

If you need the extracted text for downstream processing, write it to a `.txt` file:

```csharp
File.WriteAllText($"{Path.GetFileNameWithoutExtension(sourceFile)}_extracted.txt", combinedText);
```

## Full Working Example

Below is the *entire* program you can copy‑paste into a new console project. Replace the placeholders (`YOUR_API_KEY`, `YOUR_DIRECTORY`) and you’re good to go.

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using System.Threading.Tasks;
using Aspose.Pdf.AI;
using Aspose.Pdf.AI.OpenAI;
using Aspose.Pdf.AI.IOcr;

namespace OcrDemo
{
    class Program
    {
        static async Task Main(string[] args)
        {
            await ExtractTextAsync();
        }

        private static async Task ExtractTextAsync()
        {
            // 1️⃣ Define the folder that contains the input files
            string inputFolder = @"YOUR_DIRECTORY\"; // e.g., C:\Docs\

            // 2️⃣ Initialise OpenAI client
            string openAiKey = "YOUR_API_KEY";
            using var openAiClient = OpenAIClient
                .CreateWithApiKey(openAiKey)
                .Build();

            // 3️⃣ Configure OCR options – image + scanned PDF
            var ocrOptions = OpenAIOcrCopilotOptions
                .Create()
                .WithModel(OpenAIModels.Gpt4OMini)
                .WithDocument($"{inputFolder}ScannedDocument.pdf")
                .WithDocument($"{inputFolder}ImageWithText.jpg");

            // 4️⃣ Build the OCR copilot
            IOcrCopilot ocrCopilot = AICopilotFactory
                .CreateOcrCopilot(openAiClient, ocrOptions);

            // 5️⃣ Run OCR and get results
            List<TextRecognitionResult> results;
            try
            {
                results = await ocrCopilot.GetTextRecognitionResultAsync();
            }
            catch (OpenAIException ex)
            {
                Console.Error.WriteLine($"OpenAI error: {ex.Message}");
                return;
            }

            // 6️⃣ Extract and display text
            for (int i = 0; i < results.Count; i++)
            {
                var fileResult = results[i];
                string sourceFile = ocrOptions.Documents[i];

                string combinedText = string.Empty;
                foreach (var detail in fileResult.OcrDetails)
                {
                    combinedText += $"[Page {detail.PageNumber}]{Environment.NewLine}";
                    combinedText += detail.ExtractedText + Environment.NewLine;
                }

                Console.WriteLine($"--- Extracted text from: {sourceFile} ---");
                Console.WriteLine(combinedText);

                // Optional: save to .txt
                string outPath = Path.Combine(
                    Path.GetDirectoryName(sourceFile)!,
                    $"{Path.GetFileNameWithoutExtension(sourceFile)}_extracted.txt");
                File.WriteAllText(outPath

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}