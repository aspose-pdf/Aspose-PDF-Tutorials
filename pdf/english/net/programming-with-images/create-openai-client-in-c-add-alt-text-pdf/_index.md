---
category: general
date: 2025-12-25
description: Create OpenAI client in C# to generate image descriptions and add alt
  text PDF. Learn how to set temperature OpenAI and describe images PDF in minutes.
draft: false
keywords:
- create openai client
- add alt text pdf
- generate image descriptions
- how to set temperature openai
- how to describe images pdf
language: en
og_description: Create OpenAI client in C# to generate image descriptions, set temperature
  OpenAI, and add alt text PDF. Complete step‑by‑step guide.
og_title: Create OpenAI client in C# – Add Alt Text PDF
tags:
- OpenAI
- C#
- PDF
- Aspose
title: Create OpenAI client in C# – Add Alt Text PDF
url: /net/programming-with-images/create-openai-client-in-c-add-alt-text-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create OpenAI client in C# – Add Alt Text PDF

Ever wondered how to **create OpenAI client** in C# and automatically embed alt‑text into PDFs? You're not the only one. Many developers hit a wall when they need to describe images inside a PDF without manually writing every caption. The good news? With Aspose.Pdf.AI you can spin up an OpenAI client, generate image descriptions, and sprinkle those alt texts right back into the document—all programmatically.

In this tutorial we’ll walk through the whole process: from setting up the client, tweaking the **temperature** of the model, to finally **add alt text PDF** files. By the end you’ll be able to **generate image descriptions** for any PDF or standalone image, and you’ll know **how to describe images PDF** in a way that’s both SEO‑friendly and accessibility‑ready.

## What You’ll Need

- **.NET 6+** (or any recent .NET runtime)
- **Aspose.Pdf.AI** NuGet package – the bridge between your C# code and OpenAI’s vision models.
- An **OpenAI API key** with access to GPT‑4 Turbo or any vision‑capable model.
- A folder with a sample PDF that contains images (e.g., `Pdf_with_images.pdf`) and optionally a separate image file (`Mona_liza.jpg`).

> **Pro tip:** Keep your API key in a secure environment variable or secret manager; never hard‑code it in production.

## Step 1: Create OpenAI client and set the temperature

The first thing we do is spin up an OpenAI client. The **temperature** controls the randomness of the model’s output – a value of `0.0` makes it deterministic, while `1.0` encourages creativity. For alt‑text we usually want a balanced tone, so `0.5` works well.

```csharp
// Step 1: Define the directory that contains the input files
string inputDirectory = "YOUR_DIRECTORY/";

// Step 2: Create an OpenAI client using your API key
using var openAiClient = Aspose.Pdf.AI.OpenAIClient
    .CreateWithApiKey(Environment.GetEnvironmentVariable("OPENAI_API_KEY") 
        ?? "YOUR_API_KEY")   // Replace with your actual key if not using env var
    .Build();
```

**Why this matters:**  
- `CreateWithApiKey` securely injects your credentials.  
- Using `Environment.GetEnvironmentVariable` avoids accidental leaks.  
- The client object is disposable (`using var`), ensuring proper cleanup.

## Step 2: Configure the image‑description copilot options

Now we tell the copilot which model to use, what temperature to apply, and which documents or images to analyze. This is where the **how to set temperature OpenAI** part comes into play.

```csharp
// Step 3: Configure the image‑description copilot options
var copilotOptions = Aspose.Pdf.AI.OpenAIImageDescriptionCopilotOptions
    .Create()
    .WithModel(Aspose.Pdf.AI.OpenAIModels.Gpt4Turbo) // Vision‑capable model
    .WithTemperature(0.5)                           // How to set temperature OpenAI
    .WithTopP(1)
    .WithDocument(new Aspose.Pdf.AI.PdfDocument   // Attach a PDF document
    {
        Name = "SamplePdfWithImages",
        Document = new Aspose.Pdf.Document(inputDirectory + "Pdf_with_images.pdf")
    })
    .WithDocument(inputDirectory + "Mona_liza.jpg"); // Attach an image file
```

**Key points:**  
- `WithModel` picks a vision‑enabled model (GPT‑4 Turbo).  
- `WithTemperature(0.5)` balances creativity and consistency.  
- You can attach **multiple** sources – both PDFs and individual images – to **generate image descriptions** in one go.

## Step 3: Create the image‑description copilot

With the options set, we instantiate the copilot. Think of it as a specialized assistant that knows how to talk to OpenAI about pictures.

```csharp
// Step 4: Create the image‑description copilot
var imageDescriptionCopilot = Aspose.Pdf.AI.AICopilotFactory
    .CreateImageDescriptionCopilot(openAiClient, copilotOptions);
```

> **Why use a copilot?** It abstracts the low‑level API calls, handles batching, and returns strongly‑typed results ready for further processing.

## Step 4: Retrieve descriptions for all attached images

Now we actually ask the model to describe everything we fed it. The method is asynchronous because it may involve network latency.

```csharp
// Step 5: Retrieve descriptions for all attached images
List<Aspose.Pdf.AI.ImageDescriptionResult> descriptions =
    await imageDescriptionCopilot.GetImageDescriptionsAsync();
```

Each `ImageDescriptionResult` contains the original image reference and a human‑readable description. This is the core of **how to describe images PDF** automatically.

### Sample output (truncated)

```
Image: Pdf_with_images.pdf (page 2, image #1)
Description: "A close‑up of a vintage mechanical watch with a silver case and dark leather strap."

Image: Mona_liza.jpg
Description: "Leonardo da Vinci’s Mona Lisa, showing a woman with a subtle smile against a distant landscape."
```

## Step 5: Add the generated descriptions back into the PDF(s)

Finally, we embed the alt‑text directly into the PDF. Aspose.Pdf.AI writes the description into the image’s metadata, which screen readers can pick up.

```csharp
// Step 6: Embed the generated descriptions back into the PDF(s)
await imageDescriptionCopilot.AddPdfImageDescriptionsAsync(inputDirectory);
```

After this call, open `Pdf_with_images.pdf` in any PDF viewer and inspect the image properties – you’ll see the new alt‑text field populated.

## Full Working Example

Putting it all together, here’s a ready‑to‑run console app. Feel free to copy‑paste, adjust the file paths, and hit **F5**.

```csharp
using System;
using System.Collections.Generic;
using System.Threading.Tasks;
using Aspose.Pdf;
using Aspose.Pdf.AI;

class Program
{
    static async Task Main()
    {
        // Directory containing your PDF and image files
        string inputDirectory = "YOUR_DIRECTORY/";

        // 1️⃣ Create the OpenAI client (primary step)
        using var openAiClient = OpenAIClient
            .CreateWithApiKey(Environment.GetEnvironmentVariable("OPENAI_API_KEY") 
                ?? "YOUR_API_KEY")
            .Build();

        // 2️⃣ Set up copilot options – model, temperature, and sources
        var copilotOptions = OpenAIImageDescriptionCopilotOptions
            .Create()
            .WithModel(OpenAIModels.Gpt4Turbo)
            .WithTemperature(0.5)           // how to set temperature OpenAI
            .WithTopP(1)
            .WithDocument(new PdfDocument
            {
                Name = "SamplePdfWithImages",
                Document = new Document($"{inputDirectory}Pdf_with_images.pdf")
            })
            .WithDocument($"{inputDirectory}Mona_liza.jpg");

        // 3️⃣ Build the copilot
        var imageDescriptionCopilot = AICopilotFactory
            .CreateImageDescriptionCopilot(openAiClient, copilotOptions);

        // 4️⃣ Get descriptions – this is where we **generate image descriptions**
        List<ImageDescriptionResult> descriptions =
            await imageDescriptionCopilot.GetImageDescriptionsAsync();

        // Show the results in the console (helps you verify)
        Console.WriteLine("=== Generated Descriptions ===");
        foreach (var result in descriptions)
        {
            Console.WriteLine($"Source: {result.Source}");
            Console.WriteLine($"Alt‑text: {result.Description}");
            Console.WriteLine(new string('-', 40));
        }

        // 5️⃣ Write the alt‑text back into the PDF – **add alt text PDF**
        await imageDescriptionCopilot.AddPdfImageDescriptionsAsync(inputDirectory);

        Console.WriteLine("✅ Alt‑text successfully added to PDF(s).");
    }
}
```

### What to Expect

- The console prints each image’s description, so you can double‑check before the PDF is altered.
- After the final step, opening `Pdf_with_images.pdf` in Adobe Acrobat → Properties → Description will reveal the new alt‑text.
- If you run the app again, the copilot will skip images that already have descriptions, avoiding duplication.

## Common Questions & Edge Cases

### What if my PDF has hundreds of images?

The copilot processes images in batches internally, but you can also split the PDF into smaller chunks using `Aspose.Pdf.Document.Split()` and run the description pipeline on each part. This reduces memory pressure and makes progress tracking easier.

### How do I control the length of the description?

Adjust the **temperature** or add a `WithPrompt` customization (not shown here) to guide the model. For example, prepend “Provide a concise alt‑text (max 10 words): ” to the prompt.

### Can I use a different OpenAI model?

Absolutely. Replace `OpenAIModels.Gpt4Turbo` with `OpenAIModels.Gpt4Vision` or any model that supports image inputs. Just ensure your API plan includes vision capabilities.

### What about non‑English PDFs?

The model detects language automatically, but you can force a language by adding a prompt like “Describe the image in Spanish.” The same `GetImageDescriptionsAsync` call will return the description in the requested language.

## Tips for Production‑Ready Implementations

- **Cache results:** Store generated descriptions in a database to avoid re‑calling the API for unchanged images.
- **Rate‑limit:** Respect OpenAI’s rate limits; use exponential back‑off on `429 Too Many Requests`.
- **Secure the key:** Use Azure Key Vault, AWS Secrets Manager, or `.NET Secret Manager`.
- **Validate PDFs:** Before processing, run a quick integrity check (`Document.Validate()`) to catch corrupted files early.

## Conclusion

We’ve just **created OpenAI client** in C#, learned **how to set temperature OpenAI**, and used Aspose.Pdf.AI to **generate image descriptions** that are automatically **added as alt text PDF** entries. In short, you now know **how to describe images PDF** without lifting a finger—just a few lines of code.

Next steps? Try feeding a whole folder of marketing assets into the pipeline, or experiment with custom prompts to produce SEO‑optimized alt‑texts for web PDFs. You could also chain this with a PDF generation step to produce

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}