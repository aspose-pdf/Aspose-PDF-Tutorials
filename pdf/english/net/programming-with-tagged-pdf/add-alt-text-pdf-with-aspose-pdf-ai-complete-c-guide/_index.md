---
category: general
date: 2025-12-23
description: Add alt text PDF using Aspose.Pdf.AI and OpenAI vision models. Learn
  how to add image descriptions PDF automatically, embed them back, and boost accessibility.
draft: false
keywords:
- add alt text pdf
- add image descriptions pdf
- PDF accessibility C#
- Aspose PDF AI
- OpenAI vision model
language: en
og_description: Add alt text PDF instantly with Aspose.Pdf.AI. This step‑by‑step tutorial
  shows how to add image descriptions PDF using OpenAI's vision‑capable models.
og_title: Add Alt Text PDF with Aspose.Pdf.AI – Complete C# Guide
tags:
- PDF
- C#
- Accessibility
- Aspose
title: Add Alt Text PDF with Aspose.Pdf.AI – Complete C# Guide
url: /net/programming-with-tagged-pdf/add-alt-text-pdf-with-aspose-pdf-ai-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Add Alt Text PDF with Aspose.Pdf.AI – Complete C# Guide

Ever wondered how to **add alt text PDF** files without manually typing each description? You're not alone. Many developers hit a wall when they need to make PDFs accessible, especially when the documents contain dozens of images. The good news? With Aspose.Pdf.AI and OpenAI’s vision‑capable models you can automate the whole process and even **add image descriptions PDF** in one smooth run.

In this tutorial we’ll walk through everything you need to know: the why behind PDF accessibility, the required prerequisites, and a full, runnable C# example that extracts image descriptions and embeds them back into your PDF. By the end you’ll have a self‑contained solution you can drop into any .NET project.

## Prerequisites – What You’ll Need Before You Start

Before diving into code, make sure you have the following:

* **.NET 6+** (or .NET Framework 4.7+ – the API works with both)
* An **Aspose.Pdf for .NET** license (the free trial works for testing)
* An **OpenAI API key** with access to GPT‑4‑Turbo or any vision‑enabled model
* A folder containing at least one PDF with images and optionally a standalone image file (e.g., `Mona_liza.jpg`)

If any of these sound unfamiliar, pause here and grab the missing piece. The rest of the guide assumes you’ve got them ready.

## Step 1 – Set Up the Project and Install Packages

First, create a new console app (or integrate into an existing solution). Then add the required NuGet packages:

```bash
dotnet new console -n PdfAltTextDemo
cd PdfAltTextDemo
dotnet add package Aspose.PDF
dotnet add package Aspose.PDF.AI
```

> **Pro tip:** Use the latest stable versions; as of December 2025 the packages are `23.12.0` for Aspose.PDF and `1.5.0` for Aspose.PDF.AI.

## Step 2 – Define Input Folder and Initialize the OpenAI Client

We need to tell the code where our source files live and spin up an OpenAI client that can talk to the vision model.

```csharp
// Step 2.1: Point to the folder that holds your PDFs and images
string inputFolder = @"C:\MyPdfAssets";

// Step 2.2: Create the OpenAI client – replace with your real key
string apiKey = "YOUR_OPENAI_API_KEY";
using var openAiClient = Aspose.Pdf.AI.OpenAIClient
    .CreateWithApiKey(apiKey)
    .Build(); // Build the client ready for calls
```

**Why this matters:** The `inputFolder` variable keeps everything tidy, and the `openAiClient` handles authentication and request throttling behind the scenes. If you skip the `Build()` call the client won’t be usable.

## Step 3 – Configure Copilot Options: Choose a Vision‑Capable Model & Attach Documents

Aspose.Pdf.AI ships with a “copilot” abstraction that knows how to talk to OpenAI, fetch image data, and return descriptions. Here’s where we set it up:

```csharp
var copilotOptions = Aspose.Pdf.AI.OpenAIImageDescriptionCopilotOptions
    .Create()
    .WithModel(Aspose.Pdf.AI.OpenAIModels.Gpt4Turbo) // Model that understands images
    .WithTemperature(0.5)   // Balanced creativity vs. factual output
    .WithTopP(1)            // Use the full probability mass
    .WithDocument(new Aspose.Pdf.AI.PdfDocument
    {
        Name = "SamplePdfWithImages",
        Document = new Aspose.Pdf.Document($"{inputFolder}/Pdf_with_images.pdf")
    })
    .WithDocument($"{inputFolder}/Mona_liza.jpg"); // Standalone image
```

**Key points to note:**

* `WithModel` selects a vision‑enabled model; GPT‑4‑Turbo is the current go‑to.
* `WithDocument` can accept either a full `PdfDocument` object (for PDFs) or a simple file path (for images). You can attach as many files as you like – just chain more `.WithDocument(...)` calls.
* Temperature 0.5 is a sweet spot: the descriptions stay accurate but still sound natural.

## Step 4 – Create the Image‑Description Copilot

Now we actually instantiate the copilot that will perform the heavy lifting.

```csharp
var imageDescriptionCopilot = Aspose.Pdf.AI.AICopilotFactory
    .CreateImageDescriptionCopilot(openAiClient, copilotOptions);
```

Under the hood this object prepares the request payloads, streams the images to OpenAI, and parses the JSON responses into strongly‑typed C# objects.

## Step 5 – Retrieve Image Descriptions Asynchronously

We call the copilot and collect the results. The method returns a list where each entry corresponds to one image (whether from a PDF page or a standalone file).

```csharp
List<Aspose.Pdf.AI.ImageDescriptionResult> descriptions =
    await imageDescriptionCopilot.GetImageDescriptionsAsync();

// Quick sanity check – print the first description
if (descriptions.Count > 0)
{
    Console.WriteLine($"First description: {descriptions[0].Description}");
}
```

**What you’ll see:** A short, human‑readable sentence like “A portrait of a woman with a mysterious smile, painted by Leonardo da Vinci.” This is the exact text we’ll embed as alt text, effectively **adding image descriptions PDF** automatically.

## Step 6 – Embed the Generated Descriptions Back Into the PDFs

The final step writes the alt text into the PDF’s image objects, making the file accessible to screen readers and other assistive technologies.

```csharp
await imageDescriptionCopilot.AddPdfImageDescriptionsAsync(inputFolder);
Console.WriteLine("All image descriptions have been embedded successfully.");
```

The method scans every PDF in `inputFolder`, matches each image with its description, and updates the PDF’s metadata accordingly. The operation is atomic – if something fails, no partial changes are saved.

## Full Working Example – Paste This Into `Program.cs`

Below is the complete program you can compile and run. It includes all the snippets above in the correct order, plus using directives and a minimal `Main` method.

```csharp
using System;
using System.Collections.Generic;
using System.Threading.Tasks;
using Aspose.Pdf;
using Aspose.Pdf.AI;

class Program
{
    static async Task Main(string[] args)
    {
        // -----------------------------------------------------------------
        // 1️⃣ Define input folder and OpenAI credentials
        // -----------------------------------------------------------------
        string inputFolder = @"C:\MyPdfAssets";
        string apiKey = "YOUR_OPENAI_API_KEY";

        // -----------------------------------------------------------------
        // 2️⃣ Build the OpenAI client
        // -----------------------------------------------------------------
        using var openAiClient = OpenAIClient
            .CreateWithApiKey(apiKey)
            .Build();

        // -----------------------------------------------------------------
        // 3️⃣ Configure copilot options – model + documents
        // -----------------------------------------------------------------
        var copilotOptions = OpenAIImageDescriptionCopilotOptions
            .Create()
            .WithModel(OpenAIModels.Gpt4Turbo)
            .WithTemperature(0.5)
            .WithTopP(1)
            .WithDocument(new PdfDocument
            {
                Name = "SamplePdfWithImages",
                Document = new Document($"{inputFolder}/Pdf_with_images.pdf")
            })
            .WithDocument($"{inputFolder}/Mona_liza.jpg");

        // -----------------------------------------------------------------
        // 4️⃣ Create the copilot
        // -----------------------------------------------------------------
        var imageDescriptionCopilot = AICopilotFactory
            .CreateImageDescriptionCopilot(openAiClient, copilotOptions);

        // -----------------------------------------------------------------
        // 5️⃣ Get image descriptions
        // -----------------------------------------------------------------
        List<ImageDescriptionResult> descriptions =
            await imageDescriptionCopilot.GetImageDescriptionsAsync();

        if (descriptions.Count > 0)
        {
            Console.WriteLine($"Sample description: {descriptions[0].Description}");
        }

        // -----------------------------------------------------------------
        // 6️⃣ Embed descriptions back into PDFs
        // -----------------------------------------------------------------
        await imageDescriptionCopilot.AddPdfImageDescriptionsAsync(inputFolder);
        Console.WriteLine("✅ All image descriptions have been added to PDFs.");
    }
}
```

### Expected Output

```
Sample description: A portrait of a woman with a mysterious smile, painted by Leonardo da Vinci.
✅ All image descriptions have been added to PDFs.
```

Open any of the processed PDFs in Adobe Acrobat and inspect the image properties – you’ll see the alt text you just generated.

## Common Questions & Edge‑Case Handling

| Question | Answer |
|----------|--------|
| **What if my PDF has thousands of images?** | The copilot processes them in batches. You can control batch size via `WithTopP` or by splitting the folder and running the tool multiple times. |
| **Can I use a different OpenAI model?** | Absolutely. Replace `Gpt4Turbo` with `Gpt4Vision` or any future model that supports image inputs. Just ensure your API plan includes vision credits. |
| **What about non‑English PDFs?** | The model will return descriptions in the language of the prompt. You can add `.WithPrompt("Describe the image in Spanish.")` if you need localized alt text. |
| **Do I need a paid Aspose license for production?** | The trial works for development, but a commercial license removes the evaluation watermark and grants unlimited usage. |
| **How do I verify that alt text was correctly embedded?** | Open the PDF in a viewer that shows image properties (e.g., Adobe Acrobat → Tools → Accessibility → Reading Order). The “Alternate Text” field should contain the generated description. |

## Pro Tips for Perfect PDF Accessibility

* **Keep descriptions concise:** Aim for 1‑2 sentences; too long alt text can overwhelm screen readers.
* **Avoid redundant information:** If surrounding text already explains the image, a brief “see surrounding text” note is acceptable.
* **Test with real assistive tech:** NVDA (Windows) and VoiceOver (macOS) are free tools that let you hear how your PDF sounds to users.
* **Batch‑process nightly:** Automate the script as part of your CI pipeline so every new PDF gets alt text before release.

## Conclusion – You’ve Learned How to Add Alt Text PDF Automatically

We’ve covered the whole journey: from setting up Aspose.Pdf.AI and OpenAI, through configuring a vision‑capable model, to pulling image descriptions and embedding them back into your PDFs. In short, you now know **how to add image descriptions PDF** without manual effort, boosting accessibility and compliance with standards like WCAG 2.1.

Next steps? Try swapping the model for a cheaper alternative, experiment with multilingual prompts, or integrate the copilot into a web API that processes user‑uploaded PDFs on the fly. The sky

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}