---
category: general
date: 2025-12-25
description: How to use Aspose to extract text from PDF and image files. Learn step‑by‑step
  how to run OCR on images with Aspose OCR copilot.
draft: false
keywords:
- how to use aspose
- extract text from pdf
- extract text from image
- how to extract text
- run ocr on images
language: en
og_description: How to use Aspose to extract text from PDF and image files. This guide
  shows you how to run OCR on images with a simple C# example.
og_title: How to Use Aspose for OCR – Extract Text from PDFs & Images
tags:
- Aspose
- OCR
- C#
- PDF processing
title: 'How to Use Aspose for OCR: Extract Text from PDFs and Images'
url: /net/text-operations/how-to-use-aspose-for-ocr-extract-text-from-pdfs-and-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Use Aspose for OCR: Extract Text from PDFs and Images

Ever wondered **how to use Aspose** to pull text out of a scanned PDF or a picture of a sign? You're not the only one. In many real‑world projects—think invoice automation or content indexing—developers need a reliable way to **extract text from PDF** files and **extract text from image** sources without hunting for third‑party services.

The good news? Aspose’s AI‑powered OCR copilot does the heavy lifting for you. In this tutorial we’ll walk through a complete, ready‑to‑run C# example that shows exactly **how to use Aspose** to **run OCR on images**, and then we’ll discuss why this approach beats the ad‑hoc alternatives.

By the end of this guide you’ll be able to:

* Initialize the Aspose PDF AI client with your own API key.  
* Configure the OCR copilot to work with both PDF and image inputs.  
* Retrieve the recognized text and handle common edge cases.  

No external scripts, no missing imports—just a single .cs file you can drop into any .NET 6+ project.

## Prerequisites (What You Need Before Starting)

| Requirement | Why It Matters |
|-------------|----------------|
| .NET 6 SDK or later | Aspose PDF AI ships as a modern NuGet package that targets .NET Standard 2.1+. |
| Aspose.Pdf.AI NuGet package (`Aspose.Pdf.AI`) | Provides the `OpenAIClient`, `AICopilotFactory`, and OCR types used in the code. |
| An active Aspose Cloud API key | Required to authenticate calls to the underlying OpenAI model. |
| A folder containing at least one scanned PDF and one image with text | Demonstrates both **extract text from pdf** and **extract text from image** scenarios. |

If any of these sound unfamiliar, just install the SDK, add the NuGet package, and sign up for a free trial key on the Aspose website. It’s that simple.

## Overview of the Solution

The solution revolves around three core concepts:

1. **OpenAIClient** – a thin wrapper that handles authentication and request routing.  
2. **OcrCopilotOptions** – a builder object where you tell Aspose which model to use (`Gpt4OMini` is a good balance of speed and accuracy) and which documents to process.  
3. **IOcrCopilot** – the orchestrator that sends the files to the service, waits for the response, and returns a list of `TextRecognitionResult` objects.

Understanding each piece helps you **how to extract text** from any supported format, and it also makes it easy to swap in a different model later if you need higher fidelity.

---

## Step 1: Set Up the Project and Import Namespaces

First, create a new console app (or add the code to an existing project). Then add the required `using` statements so the compiler knows where to find the Aspose types.

```csharp
// Program.cs – entry point for the OCR demo
using System;
using System.Collections.Generic;
using System.Threading.Tasks;
using Aspose.Pdf.AI;                 // Core Aspose PDF AI namespace
using Aspose.Pdf.AI.OpenAI;          // OpenAI client and model enums
using Aspose.Pdf.AI.IOcr;            // OCR copilot interfaces
```

> **Pro tip:** If you’re using Visual Studio, the IDE will suggest installing the missing NuGet package automatically when you type `Aspose.Pdf.AI`. Just click “Restore”.

---

## Step 2: Define the Input Directory and Initialize the Aspose Client

Here’s where we answer the “**how to use aspose**” question in practice: you tell Aspose where your files live and give it your API credentials.

```csharp
// Step 2.1: Point to the folder that holds your source files
const string inputDir = @"C:\MyDocuments\OCRSamples\";   // <-- change to your own path

// Step 2.2: Create the OpenAI client using your Aspose API key
using var openAiClient = OpenAIClient
    .CreateWithApiKey("YOUR_API_KEY")   // Replace with your actual key
    .Build();
```

**Why this matters:**  
*The `inputDir` variable keeps the code portable—just swap the path and you’re good to go.*  
*The `using` statement ensures the client is disposed properly, releasing any underlying HTTP connections.*

---

## Step 3: Configure OCR Copilot Options – Choose a Vision‑Capable Model

Now we tell the copilot **which model** to use and **which documents** to feed it. The example below runs OCR on both a scanned PDF and a JPEG image, covering the two most common extraction scenarios.

```csharp
// Step 3: Build OCR options with a vision‑capable model
var ocrOptions = OcrCopilotOptions
    .Create()
    .WithModel(OpenAIModels.Gpt4OMini)                     // Fast, accurate, supports images
    .WithDocument($"{inputDir}ScannedDocument.pdf")       // PDF to demonstrate extract text from pdf
    .WithDocument($"{inputDir}ImageWithText.jpg");        // Image to demonstrate extract text from image
```

> **Why `Gpt4OMini`?** It’s a lightweight variant that still understands visual layouts, making it perfect for most business documents. If you need higher precision (e.g., handwriting), switch to `Gpt4Vision`.

---

## Step 4: Create the OCR Copilot Instance

The factory method abstracts away the plumbing. Think of it as the “engine start” button for your OCR workflow.

```csharp
// Step 4: Instantiate the OCR copilot
IOcrCopilot copilot = AICopilotFactory
    .CreateOcrCopilot(openAiClient, ocrOptions);
```

**What’s happening under the hood?**  
The factory injects the `openAiClient` (which holds your authentication) and the `ocrOptions` (which contain the model and file list) into a concrete `OcrCopilot` implementation. From here on, you only interact with the high‑level `IOcrCopilot` interface.

---

## Step 5: Run OCR Asynchronously and Gather Results

Running OCR can take a few seconds, especially for large PDFs. That’s why we use `await` – it keeps the UI responsive if you embed this code in a desktop or web app.

```csharp
// Step 5: Execute OCR and collect the results
List<TextRecognitionResult> recognitions = await copilot.GetTextRecognitionResultAsync();
```

The `recognitions` list will contain one entry per input document, preserving the order you added them in `ocrOptions`. Each `TextRecognitionResult` holds an `OcrDetails` collection with the extracted text, confidence scores, and bounding boxes.

---

## Step 6: Extract and Display the Recognized Text

Finally, we pull the plain text out of the first document (the PDF) and print it to the console. You can loop through `recognitions` if you need to handle multiple files.

```csharp
// Step 6: Pull the extracted text from the first document (PDF)
if (recognitions.Count > 0 && recognitions[0].OcrDetails.Count > 0)
{
    string extractedPdfText = recognitions[0].OcrDetails[0].ExtractedText;
    Console.WriteLine("=== Text extracted from PDF ===");
    Console.WriteLine(extractedPdfText);
}
else
{
    Console.WriteLine("No OCR results were returned for the PDF.");
}

// Bonus: Show text from the image as well
if (recognitions.Count > 1 && recognitions[1].OcrDetails.Count > 0)
{
    string extractedImgText = recognitions[1].OcrDetails[0].ExtractedText;
    Console.WriteLine("\n=== Text extracted from Image ===");
    Console.WriteLine(extractedImgText);
}
```

**Typical output** might look like:

```
=== Text extracted from PDF ===
Invoice #12345
Date: 2025‑11‑30
Total: $1,250.00
...

=== Text extracted from Image ===
Welcome to the OpenAI Demo
```

That’s it—**you now know how to use Aspose** to **extract text from pdf** and **extract text from image** files, and you’ve seen a concrete example of **how to extract text** using the OCR copilot.

---

## Common Questions & Edge Cases

### What if my PDF is password‑protected?

Add the password to the document path:

```csharp
.WithDocument($"{inputDir}SecureDoc.pdf", password: "mySecret")
```

The API will decrypt it before running OCR.

### Can I process more than two files at once?

Absolutely. Call `.WithDocument()` repeatedly or pass a list:

```csharp
var files = new[] { "doc1.pdf", "doc2.pdf", "photo.png" };
foreach (var f in files)
    ocrOptions.WithDocument($"{inputDir}{f}");
```

Just remember that each extra file adds to the latency.

### How do I handle low‑confidence results?

Each `OcrDetail` includes a `Confidence` property (0‑1). You can filter:

```csharp
foreach (var detail in recognitions[i].OcrDetails)
{
    if (detail.Confidence < 0.75)
        Console.WriteLine("⚠️ Low confidence line: " + detail.ExtractedText);
}
```

### What if I need to process handwritten notes?

Swap the model:

```csharp
.WithModel(OpenAIModels.Gpt4Vision)   // Better at handwriting
```

The rest of the code stays identical.

---

## Full Working Example (Copy‑Paste Ready)

Below is the entire program you can drop into `Program.cs`. It compiles as‑is (just replace the placeholders).

```csharp
using System;
using System.Collections.Generic;
using System.Threading.Tasks;
using Aspose.Pdf.AI;
using Aspose.Pdf.AI.OpenAI;
using Aspose.Pdf.AI.IOcr;

namespace AsposeOcrDemo
{
    class Program
    {
        static async Task Main(string[] args)
        {
            // 👉 Step 1: Define where your files live
            const string inputDir = @"C:\MyDocuments\OCRSamples\"; // <-- update this path

            // 👉 Step 2: Create the OpenAI client (replace with your real key)
            using var openAiClient = OpenAIClient
                .CreateWithApiKey("YOUR_API_KEY")
                .Build();

            // 👉 Step 3: Build OCR options – choose model & add files
            var ocrOptions = OcrCopilotOptions
                .Create()
                .WithModel(OpenAIModels.Gpt4OMini)
                .WithDocument($"{inputDir}ScannedDocument.pdf")
                .WithDocument($"{inputDir}ImageWithText.jpg");

            // 👉 Step 4: Instantiate the OCR copilot
            IOcrCopilot copilot = AICopilotFactory
                .CreateOcrCopilot(openAiClient, ocrOptions);

            // 👉 Step 5: Run OCR asynchronously
            List<TextRecognitionResult> recognitions = await copilot.GetTextRecognitionResultAsync();

            // 👉 Step 6: Display results
            if (recognitions.Count > 0 && recognitions[0].OcrDetails.Count > 0)
            {
                string pdfText = recognitions[0].OcrDetails[0].ExtractedText;
                Console.WriteLine("=== Text extracted from PDF ===");
                Console.WriteLine(pdfText);
            }

            if (recognitions.Count > 1 && recognitions[1].OcrDetails.Count > 0)
            {
                string imgText = recognitions[1].OcrDetails[0].ExtractedText

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}