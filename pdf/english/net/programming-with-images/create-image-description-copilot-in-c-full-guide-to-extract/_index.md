---
category: general
date: 2025-12-23
description: Create image description copilot to extract image alt text from PDFs
  using a vision model – step‑by‑step tutorial that shows how to generate image descriptions
  and add alt text to PDF images.
draft: false
keywords:
- create image description copilot
- extract image alt text
- configure vision model
- how to generate image descriptions
- add alt text to pdf images
language: en
og_description: Create image description copilot quickly. Learn how to configure a
  vision model, generate image descriptions, and add alt text to PDF images in C#.
og_title: Create Image Description Copilot – Extract Alt Text from PDFs
tags:
- Aspose.Pdf.AI
- OpenAI
- C#
- PDF processing
title: Create Image Description Copilot in C# – Full Guide to Extract Image Alt Text
url: /net/programming-with-images/create-image-description-copilot-in-c-full-guide-to-extract/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create Image Description Copilot – Extract Alt Text from PDFs

Ever wondered how to **create image description copilot** that pulls alt text straight out of your PDFs? You're not alone; many developers hit a wall when they need to make images accessible but lack a reliable way to automate the process.  

In this guide we’ll walk through the entire workflow—*from configuring a vision‑capable model* to writing the generated captions back into the PDF files. By the end you’ll know **how to generate image descriptions**, extract image alt text, and **add alt text to pdf images** without leaving your IDE.

## What You’ll Need

Before we dive in, make sure you have:

- .NET 6+ (or .NET Core 3.1+) installed – the code targets modern runtimes.
- An Aspose.Pdf.AI NuGet package (version 23.9 or later) – it ships the copilot utilities.
- An OpenAI API key with vision model access (GPT‑4‑Turbo or newer).
- A folder containing a PDF that includes images and any standalone image files you want to describe.

That’s it. No extra SDKs, no heavy configuration files—just a few lines of C# and you’re good to go.

## Step 1 – Set Up the Project and Install Dependencies

First, spin up a console app (or integrate the code into any existing service). Then add the required NuGet packages:

```bash
dotnet new console -n ImageDescriptionCopilotDemo
cd ImageDescriptionCopilotDemo
dotnet add package Aspose.Pdf.AI
dotnet add package Aspose.Pdf
```

> **Pro tip:** If you’re using Visual Studio, the Package Manager UI makes this a couple of clicks.

## Step 2 – Create the OpenAI Client

The **create image description copilot** process starts by authenticating against OpenAI. We’ll use the fluent builder that Aspose provides:

```csharp
using Aspose.Pdf.AI;

// ...

// Step 2: Initialize the OpenAI client with your API key.
using var aiClient = OpenAIClient
    .CreateWithApiKey("YOUR_API_KEY")   // <-- replace with your real key
    .Build();
```

Why the `using var` pattern? It guarantees the underlying HTTP connections are disposed properly—something you’ll appreciate in long‑running services.

## Step 3 – Configure the Vision Model and Attach Documents

Now we tell the copilot which model to use and what files to analyze. This is where the **configure vision model** keyword comes into play.

```csharp
// Step 3: Build copilot options – pick a vision‑enabled model and point to your assets.
var copilotOptions = OpenAIImageDescriptionCopilotOptions
    .Create()
    .WithModel(OpenAIModels.Gpt4Turbo)   // Vision‑capable model
    .WithTemperature(0.5)                // Controls creativity
    .WithTopP(1)                         // Keeps sampling deterministic
    .WithDocument(new PdfDocument
    {
        Name = "SamplePdfWithImages",
        Document = new Aspose.Pdf.Document("YOUR_DIRECTORY/Pdf_with_images.pdf")
    })
    .WithDocument("YOUR_DIRECTORY/Mona_liza.jpg"); // Stand‑alone image
```

A couple of things to note:

- **Temperature** of `0.5` offers a balance between deterministic output and a bit of creativity.
- You can chain as many `.WithDocument()` calls as you like—perfect for batch processing.
- The `PdfDocument` wrapper lets the copilot treat PDF pages as image sources, which is essential for **extract image alt text**.

## Step 4 – Instantiate the Image‑Description Copilot

With the client and options ready, creating the copilot is a one‑liner:

```csharp
// Step 4: Create the image‑description copilot instance.
var imageCopilot = AICopilotFactory
    .CreateImageDescriptionCopilot(aiClient, copilotOptions);
```

Behind the scenes this object wires up request throttling, retries, and response parsing, so you don’t have to worry about the low‑level HTTP details.

## Step 5 – Retrieve and Inspect Image Descriptions

Here’s the heart of the tutorial: **how to generate image descriptions**. The async method returns a list of results—each result contains the generated caption and a confidence score.

```csharp
// Step 5: Pull the generated descriptions.
List<ImageDescriptionResult> descriptions = await imageCopilot.GetImageDescriptionsAsync();

foreach (var desc in descriptions)
{
    Console.WriteLine($"Image: {desc.ImageName}");
    Console.WriteLine($"Alt Text: {desc.Description}");
    Console.WriteLine($"Score: {desc.Confidence:P2}");
    Console.WriteLine(new string('-', 40));
}
```

Typical output looks like:

```
Image: Pdf_with_images.pdf/Page_1/Image_1
Alt Text: A portrait of Mona Lisa with a subtle smile.
Score: 96.73%
----------------------------------------
Image: Mona_liza.jpg
Alt Text: The famous Mona Lisa painting by Leonardo da Vinci.
Score: 98.41%
```

If you need to **extract image alt text** for downstream systems (e.g., a CMS), you now have a clean list ready to consume.

## Step 6 – Add Alt Text Back Into the PDF Files

The final, most valuable step is to write those captions back into the original PDFs. Aspose makes this painless:

```csharp
// Step 6: Write the alt text into the PDF(s) in the same folder.
await imageCopilot.AddPdfImageDescriptionsAsync("YOUR_DIRECTORY/");
Console.WriteLine("✅ Alt text added to all PDF images.");
```

What actually happens? The library creates an `/Alt` entry for each image XObject in the PDF, ensuring screen readers can announce the description. This satisfies accessibility guidelines like WCAG 2.1 Success Criterion 1.1.1.

### Edge Cases & Tips

| Situation | What to Do |
|-----------|-------------|
| **Large PDFs ( > 50 MB )** | Split the document into smaller chunks before feeding it to the copilot; the API has payload limits. |
| **Multiple images per page** | The copilot returns one description per image; iterate over `descriptions` and match `ImageName` to the PDF object ID. |
| **Rate‑limit errors** | Wrap the call in a retry policy (`Polly` works great) and respect the `Retry-After` header. |
| **Missing alt text after run** | Verify that each image has a unique name; duplicate names can cause the library to skip updates. |

## Complete Working Example

Below is the full program you can paste into `Program.cs`. Replace `YOUR_DIRECTORY` and `YOUR_API_KEY` with your actual paths and key.

```csharp
using System;
using System.Collections.Generic;
using System.Threading.Tasks;
using Aspose.Pdf;
using Aspose.Pdf.AI;

public class Program
{
    public static async Task Main()
    {
        await GenerateImageDescriptionsAsync();
    }

    private static async Task GenerateImageDescriptionsAsync()
    {
        // Step 1: Define the folder that holds the source PDF and images.
        string inputDirectory = "YOUR_DIRECTORY/";   // e.g., "C:/Docs/"

        // Step 2: Build the OpenAI client.
        using var aiClient = OpenAIClient
            .CreateWithApiKey("YOUR_API_KEY")   // <-- replace with your key
            .Build();

        // Step 3: Configure the copilot – pick a vision model and attach files.
        var copilotOptions = OpenAIImageDescriptionCopilotOptions
            .Create()
            .WithModel(OpenAIModels.Gpt4Turbo)   // vision‑capable model
            .WithTemperature(0.5)
            .WithTopP(1)
            .WithDocument(new PdfDocument
            {
                Name = "SamplePdfWithImages",
                Document = new Document(inputDirectory + "Pdf_with_images.pdf")
            })
            .WithDocument(inputDirectory + "Mona_liza.jpg");

        // Step 4: Instantiate the image‑description copilot.
        var imageCopilot = AICopilotFactory
            .CreateImageDescriptionCopilot(aiClient, copilotOptions);

        // Step 5: Get generated descriptions (optional, but handy for verification).
        List<ImageDescriptionResult> descriptions = await imageCopilot.GetImageDescriptionsAsync();

        Console.WriteLine("=== Generated Alt Text ===");
        foreach (var desc in descriptions)
        {
            Console.WriteLine($"• {desc.ImageName}: {desc.Description} (Score: {desc.Confidence:P2})");
        }
        Console.WriteLine();

        // Step 6: Write the alt text back into the PDFs in the directory.
        await imageCopilot.AddPdfImageDescriptionsAsync(inputDirectory);
        Console.WriteLine("✅ All PDF images now contain alt text.");
    }
}
```

Save, run `dotnet run`, and watch the console print the generated captions followed by a success message. Open one of the PDFs in Acrobat Reader → Right‑click an image → **Properties** → **Alternate Text** to verify the changes.

## Conclusion

We’ve just **created image description copilot** from scratch, learned how to **configure vision model**, demonstrated **how to generate image descriptions**, and finally **added alt text to pdf images** automatically. This end‑to‑end solution not only boosts accessibility but also saves countless manual hours.

### What’s Next?

- **Batch processing**: Loop over multiple directories and store results in a database.
- **Custom prompts**: Tweak the temperature or inject a system prompt to steer the tone of the captions.
- **Other formats**: Use the same copilot to describe images in Word documents or HTML pages.
- **Security**: Store your OpenAI key in Azure Key Vault or AWS Secrets Manager instead of hard‑coding.

Feel free to experiment—maybe you’ll discover a smarter way to **extract image alt text** for your own products. If you hit any snags, drop a comment below; happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}