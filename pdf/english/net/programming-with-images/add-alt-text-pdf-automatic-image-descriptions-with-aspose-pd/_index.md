---
category: general
date: 2025-12-22
description: Learn how to add alt text pdf automatically and even extract images from
  pdf using Aspose.Pdf AI. Step‑by‑step C# guide with full code.
draft: false
keywords:
- add alt text pdf
- extract images from pdf
language: en
og_description: Add alt text pdf automatically with Aspose PDF AI. This guide shows
  how to extract images from pdf, generate descriptions, and embed them back.
og_title: Add Alt Text PDF – Complete C# Tutorial
tags:
- Aspose.PDF
- C#
- AI
- Accessibility
title: Add Alt Text PDF – Automatic Image Descriptions with Aspose PDF AI
url: /net/programming-with-images/add-alt-text-pdf-automatic-image-descriptions-with-aspose-pd/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Add Alt Text PDF – Automatic Image Descriptions with Aspose PDF AI

Ever wondered how to **add alt text pdf** files without manually typing a caption for every picture? You're not alone. Accessibility regulations are tightening, and developers need a reliable way to embed meaningful alt text into PDFs.  

In this tutorial we’ll show you exactly how to do that—and, as a bonus, we’ll also cover how to **extract images from pdf** so you can see what’s being described. By the end you’ll have a ready‑to‑run C# program that pulls images out of a PDF, asks an AI model for descriptions, and writes those descriptions back as alt text. No vague pointers, just concrete code and explanations.

## What You’ll Need

- **.NET 6+** (the example uses a console app, but any .NET project works)
- An **Aspose.Pdf for .NET** license or a free trial (download from the Aspose site)
- An **OpenAI API key** (or any compatible endpoint that supports GPT‑4‑Turbo)
- A folder with a PDF that contains images (e.g., `Pdf_with_images.pdf`) and any standalone images you want to describe
- Visual Studio, VS Code, or your favorite IDE

That’s it—no extra NuGet packages beyond `Aspose.Pdf` and the Aspose AI client.  

Now, let’s dive in.

## Step 1 – Set Up the Project and Install Packages

Create a new console project and add the necessary packages:

```bash
dotnet new console -n PdfAltTextDemo
cd PdfAltTextDemo
dotnet add package Aspose.PDF
dotnet add package Aspose.PDF.AI
```

> **Pro tip:** If you’re using a trial license, place the `License.xml` file in the project root and load it at startup:

```csharp
// Load Aspose license (optional but removes evaluation watermark)
var license = new Aspose.Pdf.License();
license.SetLicense("License.xml");
```

## Step 2 – Define the Core Async Method

The heart of the solution lives in a single async method called `GenerateImageDescriptionsAsync`. It does everything from locating the source folder to writing the alt text back into the PDF.

```csharp
using System;
using System.Collections.Generic;
using System.Threading.Tasks;
using Aspose.Pdf;
using Aspose.Pdf.AI;

class Program
{
    // Replace with your actual OpenAI key
    private const string ApiKey = "YOUR_OPENAI_API_KEY";

    static async Task Main(string[] args)
    {
        await GenerateImageDescriptionsAsync();
        Console.WriteLine("✅ Alt text added successfully!");
    }

    private static async Task GenerateImageDescriptionsAsync()
    {
        // Step 1: Set the folder that contains your PDF and image files
        string inputFolder = "YOUR_DIRECTORY/"; // e.g., "C:/Docs/"

        // Step 2: Initialize the OpenAI client with your API key
        using var openAiClient = Aspose.Pdf.AI.OpenAIClient
            .CreateWithApiKey(ApiKey)
            .Build();

        // Step 3: Build copilot options – choose a vision‑capable model and attach source files
        var copilotOptions = Aspose.Pdf.AI.OpenAIImageDescriptionCopilotOptions
            .Create()
            .WithModel(Aspose.Pdf.AI.OpenAIModels.Gpt4Turbo)   // Vision‑enabled model
            .WithTemperature(0.5)
            .WithTopP(1)
            .WithDocument(new Aspose.Pdf.AI.PdfDocument
            {
                Name = "SamplePdfWithImages",
                Document = new Aspose.Pdf.Document(inputFolder + "Pdf_with_images.pdf")
            })
            .WithDocument(inputFolder + "Mona_liza.jpg"); // Example standalone image

        // Step 4: Create the image‑description copilot
        var imageCopilot = Aspose.Pdf.AI.AICopilotFactory
            .CreateImageDescriptionCopilot(openAiClient, copilotOptions);

        // Step 5: Asynchronously obtain descriptions for each attached image
        List<ImageDescriptionResult> imageDescriptions = await imageCopilot.GetImageDescriptionsAsync();

        // Step 6: Embed the generated descriptions back into the PDF files
        await imageCopilot.AddPdfImageDescriptionsAsync(inputFolder);
    }
}
```

### Why This Works

- **Vision‑capable model:** `Gpt4Turbo` can see images, so it can actually generate meaningful captions.
- **`WithDocument` overloads:** One overload loads a full PDF (`PdfDocument`), the other loads a raw image file. This is how we **extract images from pdf** (the PDF is parsed internally) and also feed external pictures.
- **Async flow:** The AI call may take a few seconds per image; using `await` keeps the UI responsive if you later move this code into a desktop or web app.

## Step 3 – Run the Code and Verify Output

Compile and run:

```bash
dotnet run
```

If everything is wired correctly, you’ll see:

```
✅ Alt text added successfully!
```

Open `Pdf_with_images.pdf` in any PDF reader that shows accessibility tags (Adobe Acrobat, for example). Right‑click an image → **Properties** → **Tag** → **Alternative Text**. You should see a sentence like:

> *“A portrait of a woman wearing a Renaissance dress, known as the Mona Lisa, painted by Leonardo da Vinci.”*

That sentence is the AI‑generated description, automatically **added as alt text pdf**.  

> **Note:** The AI may occasionally produce overly verbose captions. Feel free to post‑process the strings (trim length, remove filler words) before embedding them.

## Step 4 – Extract Images from PDF (Optional)

Sometimes you need the raw image files—for a gallery, a machine‑learning pipeline, or just to verify what the AI saw. Aspose makes this a breeze:

```csharp
// Extract all images from a PDF and save them to disk
static void ExtractImages(string pdfPath, string outputFolder)
{
    var pdfDoc = new Document(pdfPath);
    int imageIndex = 1;

    foreach (var page in pdfDoc.Pages)
    {
        foreach (var image in page.Resources.Images)
        {
            var img = image.Value;
            string fileExt = img.FileFormat.ToString().ToLower(); // e.g., png, jpeg
            string outPath = Path.Combine(outputFolder, $"image_{imageIndex}.{fileExt}");
            img.Save(outPath);
            Console.WriteLine($"Saved {outPath}");
            imageIndex++;
        }
    }
}
```

Call it before the AI step if you want to **extract images from pdf** manually:

```csharp
ExtractImages(inputFolder + "Pdf_with_images.pdf", inputFolder + "extracted/");
```

The extracted files can be inspected, edited, or fed into other services. This dual capability—both extracting and automatically captioning—covers most accessibility workflows.

## Step 5 – Fine‑Tune the Process (Edge Cases & Tips)

| Situation | What to Do |
|-----------|------------|
| **Large PDFs (100+ pages)** | Process pages in batches; call `GetImageDescriptionsAsync` with a subset of `WithDocument` objects to avoid hitting token limits. |
| **Low‑resolution images** | Increase `WithTemperature` to 0.7 for more creative guesses, or pre‑upscale images with a library like **ImageSharp** before sending them to the model. |
| **Non‑English PDFs** | Set the model’s `WithPrompt` to include language hints, e.g., “Provide the description in Spanish.” |
| **Duplicate images** | After extraction, hash each image and skip duplicates to save API calls. |
| **Accessibility compliance** | Verify the generated alt text meets WCAG 2.1 AA by checking length (< 125 characters) and relevance. |

> **Watch out:** Some AI providers charge per token, so unnecessary calls can add up. The table above helps you keep costs predictable.

## Full Working Example (All Pieces Together)

Below is the complete, copy‑paste‑ready program that includes extraction, description, and embedding. Replace `YOUR_DIRECTORY` and `YOUR_OPENAI_API_KEY` before running.

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using System.Threading.Tasks;
using Aspose.Pdf;
using Aspose.Pdf.AI;

class Program
{
    private const string ApiKey = "YOUR_OPENAI_API_KEY";

    static async Task Main(string[] args)
    {
        string folder = "YOUR_DIRECTORY/"; // e.g., "C:/Docs/"

        // Optional: extract images first
        ExtractImages(folder + "Pdf_with_images.pdf", folder + "extracted/");

        await GenerateImageDescriptionsAsync(folder);
    }

    private static void ExtractImages(string pdfPath, string outputFolder)
    {
        var pdfDoc = new Document(pdfPath);
        Directory.CreateDirectory(outputFolder);
        int idx = 1;

        foreach (Page page in pdfDoc.Pages)
        {
            foreach (var imgEntry in page.Resources.Images)
            {
                var img = imgEntry.Value;
                string ext = img.FileFormat.ToString().ToLower();
                string outPath = Path.Combine(outputFolder, $"img_{idx}.{ext}");
                img.Save(outPath);
                Console.WriteLine($"Saved {outPath}");
                idx++;
            }
        }
    }

    private static async Task GenerateImageDescriptionsAsync(string inputFolder)
    {
        using var client = Aspose.Pdf.AI.OpenAIClient
            .CreateWithApiKey(ApiKey)
            .Build();

        var options = Aspose.Pdf.AI.OpenAIImageDescriptionCopilotOptions
            .Create()
            .WithModel(Aspose.Pdf.AI.OpenAIModels.Gpt4Turbo)
            .WithTemperature(0.5)
            .WithTopP(1)
            .WithDocument(new Aspose.Pdf.AI.PdfDocument
            {
                Name = "SamplePdfWithImages",
                Document = new Aspose.Pdf.Document(inputFolder + "Pdf_with_images.pdf")
            })
            .WithDocument(inputFolder + "Mona_liza.jpg");

        var copilot = Aspose.Pdf.AI.AICopilotFactory
            .CreateImageDescriptionCopilot(client, options);

        List<ImageDescriptionResult> results = await copilot.GetImageDescriptionsAsync();

        // Optional: log each description
        foreach (var r in results)
        {
            Console.WriteLine($"Image: {r.SourceFileName}");
            Console.WriteLine($"Description: {r.Description}");
            Console.WriteLine(new string('-', 40));
        }

        await copilot.AddPdfImageDescriptionsAsync(inputFolder);
    }
}
```

### Expected Result

- All images inside `Pdf_with_images.pdf` now carry an **alt text** entry.
- The console prints each AI‑generated caption, letting you verify quality.
- Extracted images appear in `YOUR_DIRECTORY/extracted/` for any downstream processing.

## Wrap‑Up: What We Achieved

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}