---
category: general
date: 2025-12-22
description: How to describe images using Aspose PDF AI – learn how to generate image
  captions, add alt text PDF, and retrieve image descriptions in C#.
draft: false
keywords:
- how to describe images
- how to use aspose
- generate image captions
- add alt text pdf
- retrieve image descriptions
language: en
og_description: How to describe images using Aspose PDF AI. This tutorial shows you
  how to generate image captions, add alt text PDF, and retrieve image descriptions
  in C#.
og_title: How to Describe Images with Aspose – Add Alt Text to PDFs
tags:
- Aspose
- PDF
- C#
- AI
title: How to Describe Images with Aspose – Complete Guide to Add Alt Text to PDFs
url: /net/programming-with-tagged-pdf/how-to-describe-images-with-aspose-complete-guide-to-add-alt/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Describe Images with Aspose – Complete Guide to Add Alt Text to PDFs

Ever wondered **how to describe images** so that screen‑readers can actually “see” what’s on the page? You’re not the only one. In many projects the lack of proper alt text makes PDFs inaccessible, and fixing that manually is a pain.  

The good news? With Aspose PDF AI you can automatically generate captions, retrieve image descriptions, and embed them right back into your PDF—all from C#. In this tutorial we’ll walk through the whole process, from setting up the client to saving the final, accessible document.

> **Quick win:** By the end you’ll have a runnable code sample that adds meaningful alt text to every image in a PDF, and you’ll understand how to **generate image captions** on the fly.

---

## What You’ll Learn

* **How to use Aspose** PDF AI together with OpenAI’s vision‑capable models.  
* The exact steps to **retrieve image descriptions** from a PDF and a standalone image file.  
* How to **add alt text PDF** automatically, so your documents pass accessibility audits.  
* Tips for handling edge cases—like PDFs with no images or with encrypted pages.  

No prior experience with Aspose is required; just a basic C# environment and an OpenAI API key.

---

## Prerequisites

| Requirement | Reason |
|-------------|--------|
| .NET 6 SDK (or later) | Modern language features and async support |
| Visual Studio 2022 (or VS Code) | IDE for easy debugging |
| Aspose.PDF AI NuGet package | The core library that talks to OpenAI |
| OpenAI API key | Needed for the vision model (GPT‑4 Turbo) |
| A folder with a PDF that contains images (`Pdf_with_images.pdf`) and an image file (`Mona_liza.jpg`) | Sample assets for the demo |

If you’re missing any of these, grab them now—getting stuck halfway through is the worst.

---

## Step 1: Set Up the Aspose PDF AI Client (**how to use aspose**)

First, we need an `OpenAIClient` that knows which API key to use. The `using var` pattern ensures the client is disposed correctly.

```csharp
// Step 1: Define the folder that holds your input files
string dataDir = @"C:\MyProjects\ImageAltDemo\";

// Step 2: Initialise the Aspose PDF AI client with your OpenAI key
using var openAiClient = Aspose.Pdf.AI.OpenAIClient
    .CreateWithApiKey("YOUR_API_KEY")   // ← replace with your real key
    .Build();
```

> **Why this matters:** The client handles authentication, request throttling, and retries for you. Skipping this step means you’ll have to reinvent a lot of plumbing.

---

## Step 2: Configure the Copilot – Choose a Vision Model and Attach Documents (**generate image captions**)

Aspose provides a “copilot” that wraps the OpenAI model. Here we select GPT‑4 Turbo (the vision‑enabled variant) and point it at both a PDF and a separate image.

```csharp
// Step 3: Build the copilot options
var options = Aspose.Pdf.AI.OpenAIImageDescriptionCopilotOptions
    .Create()
    .WithModel(Aspose.Pdf.AI.OpenAIModels.Gpt4Turbo) // Vision‑capable model
    .WithTemperature(0.5)      // Balanced creativity vs. determinism
    .WithTopP(1)               // Use full probability mass
    .WithDocument(new Aspose.Pdf.AI.PdfDocument
    {
        Name = "Pdf_with_images",
        Document = new Aspose.Pdf.Document(dataDir + "Pdf_with_images.pdf")
    })
    .WithDocument(dataDir + "Mona_liza.jpg"); // Stand‑alone image
```

* **Temperature** controls randomness; 0.5 is a safe middle ground.  
* **TopP** set to 1 means we consider the entire probability distribution—good for accurate captions.  

> **Tip:** If you have many PDFs, you can call `.WithDocument(...)` repeatedly; the copilot will batch them for you.

---

## Step 3: Create the Image‑Description Copilot (**retrieve image descriptions**)

Now we instantiate the copilot using the client and the options we just defined.

```csharp
// Step 4: Create the copilot instance
var copilot = Aspose.Pdf.AI.AICopilotFactory
    .CreateImageDescriptionCopilot(openAiClient, options);
```

At this point the copilot is ready to talk to OpenAI, fetch descriptions, and later embed them.

---

## Step 4: Ask the Model for Captions – Get Image Descriptions Asynchronously

We call `GetImageDescriptionsAsync()` which returns a list of `ImageDescriptionResult` objects. Each object contains the original image reference and the generated caption.

```csharp
// Step 5: Retrieve descriptions for all attached images
List<Aspose.Pdf.AI.ImageDescriptionResult> imageDescriptions =
    await copilot.GetImageDescriptionsAsync();
```

### What the result looks like

```csharp
foreach (var result in imageDescriptions)
{
    Console.WriteLine($"Image: {result.ImageName}");
    Console.WriteLine($"Caption: {result.Description}");
    Console.WriteLine(new string('-', 40));
}
```

**Sample output**

```
Image: Pdf_with_images.pdf – Page 2 – Image 1
Caption: A vintage car parked in front of a 1950s diner at sunset.
----------------------------------------
Image: Mona_liza.jpg
Caption: Leonardo da Vinci’s Mona Lisa, a portrait of a woman with an enigmatic smile.
----------------------------------------
```

> **Why this helps:** You now have machine‑generated, human‑readable captions that you can store, display, or embed as alt text.

---

## Step 5: Embed Captions Directly into the PDF (**add alt text pdf**)

Aspose makes it trivial to write the captions back into the PDF as alt text. The method walks each image, creates an `AlternativeText` entry, and saves the file.

```csharp
// Step 6: Write the generated descriptions back into the PDF(s)
await copilot.AddPdfImageDescriptionsAsync(dataDir);
```

The method produces new PDF files in the same folder, suffixed with `_described.pdf`. Open any of them in Adobe Acrobat and inspect the image properties—you’ll see the alt text you just generated.

---

## Step 6: Verify the Result – Quick Accessibility Check

You can programmatically confirm that alt text exists using Aspose’s API:

```csharp
var describedDoc = new Aspose.Pdf.Document(dataDir + "Pdf_with_images_described.pdf");
foreach (var page in describedDoc.Pages)
{
    foreach (var image in page.Images)
    {
        Console.WriteLine($"Alt text: {image.AlternativeText}");
    }
}
```

If you see the captions printed, the process succeeded. If any image shows an empty string, double‑check that the image actually contains visual content (blank placeholders sometimes slip through).

---

## Common Pitfalls & Pro Tips

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **No captions returned** | Model throttling or wrong model version | Increase `WithTemperature` to 0.7, or ensure you’re using a vision‑enabled model (GPT‑4 Turbo). |
| **Encrypted PDF throws exception** | Aspose can’t read protected files | Decrypt first with `Document.Load(..., new LoadOptions { Password = "pw" })`. |
| **Large PDFs cause timeouts** | API call exceeds default timeout | Use `openAiClient = ... .WithTimeout(TimeSpan.FromMinutes(5))`. |
| **Alt text appears in the wrong language** | Input PDF contains multilingual images | Pass `WithPrompt("Describe the image in English.")` to the options (custom prompt not shown above but supported). |
| **Duplicate captions for the same image** | Same image appears on multiple pages and is processed each time | Enable caching: `options.WithEnableCaching(true)`. |

---

## Full Working Example (Copy‑Paste Ready)

Below is the complete program you can drop into a console app. Replace the placeholders, run, and open the generated PDFs.

```csharp
// ------------------------------------------------------------
// Full example: Automatically generate and embed alt text
// ------------------------------------------------------------
using System;
using System.Collections.Generic;
using System.Threading.Tasks;
using Aspose.Pdf;
using Aspose.Pdf.AI;

class Program
{
    static async Task Main()
    {
        // 1️⃣ Define data folder
        string dataDir = @"C:\MyProjects\ImageAltDemo\";

        // 2️⃣ Initialise OpenAI client
        using var openAiClient = OpenAIClient
            .CreateWithApiKey("YOUR_API_KEY")   // <-- replace
            .Build();

        // 3️⃣ Configure copilot options
        var options = OpenAIImageDescriptionCopilotOptions
            .Create()
            .WithModel(OpenAIModels.Gpt4Turbo) // Vision‑capable
            .WithTemperature(0.5)
            .WithTopP(1)
            .WithDocument(new PdfDocument
            {
                Name = "Pdf_with_images",
                Document = new Document(dataDir + "Pdf_with_images.pdf")
            })
            .WithDocument(dataDir + "Mona_liza.jpg");

        // 4️⃣ Create copilot
        var copilot = AICopilotFactory
            .CreateImageDescriptionCopilot(openAiClient, options);

        // 5️⃣ Get descriptions
        List<ImageDescriptionResult> descriptions =
            await copilot.GetImageDescriptionsAsync();

        // 6️⃣ Show them in console (optional)
        foreach (var r in descriptions)
        {
            Console.WriteLine($"[{r.ImageName}] -> {r.Description}");
        }

        // 7️⃣ Embed alt text back into PDFs
        await copilot.AddPdfImageDescriptionsAsync(dataDir);

        Console.WriteLine("✅ All done! Check the *_described.pdf files.");
    }
}
```

**Expected outcome:** Two new files—`Pdf_with_images_described.pdf` and `Mona_liza_described.pdf`—appear in `dataDir`. Open them, inspect any image, and you’ll see the generated alt text.

---

## Recap: How We Solved the Problem

* We started by answering **how to describe images** using Aspose PDF AI.  
* We showed

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}