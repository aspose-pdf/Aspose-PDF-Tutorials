---
category: general
date: 2025-12-22
description: Extract summary from PDF using an OpenAI client C# example. Learn how
  to create summary PDF file, save PDF file C#, and summarize PDF with OpenAI in minutes.
draft: false
keywords:
- extract summary from pdf
- openai client c# example
- create summary pdf file
- how to save pdf file c#
- summarize pdf with openai
language: en
og_description: Extract summary from PDF instantly. This guide shows an OpenAI client
  C# example, how to create summary PDF file, and how to save PDF file C# safely.
og_title: Extract Summary from PDF with OpenAI C# – Full Tutorial
tags:
- pdf
- csharp
- openai
- summarization
title: Extract Summary from PDF with OpenAI C# – Complete Step‑by‑Step Guide
url: /net/programming-with-text/extract-summary-from-pdf-with-openai-c-complete-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extract Summary from PDF with OpenAI C# – Complete Step‑by‑Step Guide

Ever needed to **extract summary from PDF** but weren't sure which API to call or how to store the result? You're not alone. Many developers hit the same wall when they want a quick textual digest of a lengthy document and a nicely formatted PDF of that digest.  

In this tutorial we’ll walk through a practical **openai client c# example** that not only generates a concise summary but also writes it to a new PDF file. By the end you’ll know exactly how to **create summary pdf file**, master **how to save pdf file c#**, and feel comfortable with the whole **summarize pdf with openai** workflow.

## What You’ll Build

- Load an existing PDF (`input.pdf`) from disk.  
- Send the document to OpenAI via Aspose.Pdf.AI and receive a textual summary.  
- Convert that summary into a new PDF (`Summary_out.pdf`).  
- Save the file to a folder of your choice.

No external services beyond OpenAI and Aspose are required, and the code runs on .NET 6+.

> **Prerequisites**  
> - .NET 6 SDK (or later)  
> - An Aspose.Pdf for .NET license or a free evaluation key  
> - An OpenAI API key (you can get one from the OpenAI portal)  
> - Basic familiarity with async/await in C#  

If you have those, let’s dive in.

![extract summary from pdf example](/images/extract-summary-from-pdf.png "Diagram showing PDF input → OpenAI summarizer → PDF summary output")

## Step 1: Set Up the Project and Install Packages

Create a new console app and pull in the necessary NuGet packages.

```bash
dotnet new console -n PdfSummarizer
cd PdfSummarizer
dotnet add package Aspose.Pdf
dotnet add package Aspose.Pdf.AI
```

> **Pro tip:** Use the `--framework net6.0` flag if you want to lock the target framework right away.

## Step 2: Import Namespaces and Prepare Async Main

Open `Program.cs` and add the required `using` statements. We’ll also switch the default `Main` to an async method so we can await the summarizer calls.

```csharp
using System;
using System.IO;
using System.Threading.Tasks;
using Aspose.Pdf;
using Aspose.Pdf.AI;

class Program
{
    static async Task Main(string[] args)
    {
        // The rest of the tutorial code lives here.
    }
}
```

Having an async `Main` keeps the flow linear and avoids blocking the thread while the OpenAI service processes the document.

## Step 3: Define the Output Directory

It’s a good habit to keep input and output files separate. Change the placeholder to a real path on your machine.

```csharp
// Step 3: Define where the summary PDF will be saved
string outputDirectory = Path.Combine(Environment.CurrentDirectory, "output");
Directory.CreateDirectory(outputDirectory); // Ensure the folder exists
```

Creating the directory programmatically prevents “folder not found” errors when the code runs on a fresh machine.

## Step 4: Initialize the OpenAI Client (openai client c# example)

Now we build the **openai client c# example**. Replace `YOUR_OPENAI_API_KEY` with the actual key you obtained from OpenAI.

```csharp
// Step 4: Initialize the OpenAI client with your API key
using var openAiClient = OpenAIClient
    .CreateWithApiKey("YOUR_OPENAI_API_KEY") // Provide the API key
    .Build();                                 // Build the client
```

The `using var` pattern guarantees the client is disposed correctly, freeing any underlying HTTP connections.

## Step 5: Configure Summary Copilot Options

Here we tell Aspose which document to summarize and how creative the model should be. A temperature of `0.5` balances coherence with a hint of creativity.

```csharp
// Step 5: Configure summary copilot options
var summaryOptions = OpenAISummaryCopilotOptions
    .Create()
    .WithTemperature(0.5) // Adjust creativity of the summary
    .WithDocument(Path.Combine(Environment.CurrentDirectory, "input.pdf")); // Document to summarize
```

> **Why temperature matters:** Lower values (≈0.2) produce deterministic, factual text; higher values (≈0.8) may add flair but risk hallucinations. `0.5` is a safe middle ground for most business documents.

## Step 6: Create the Summary Copilot

The copilot is the high‑level wrapper that talks to OpenAI, extracts the summary, and can render it as a PDF.

```csharp
// Step 6: Create the summary copilot using the client and options
ISummaryCopilot summaryCopilot = AICopilotFactory.CreateSummaryCopilot(openAiClient, summaryOptions);
```

At this point we have everything wired: the client, the document, and the summarizer.

## Step 7: Retrieve the Summary Text (Optional)

If you just need the raw text—for logging, UI display, or further processing—grab it like this:

```csharp
// Step 7: Retrieve the generated summary text (optional)
string summaryText = await summaryCopilot.GetSummaryAsync();
Console.WriteLine("=== Summary Text ===");
Console.WriteLine(summaryText);
```

Seeing the text in the console helps you verify that the model understood the source material before you create a PDF.

## Step 8: Generate a PDF from the Summary

Aspose can turn the plain‑text summary into a nicely formatted PDF document. This step demonstrates the **create summary pdf file** capability.

```csharp
// Step 8: Retrieve the summary as a PDF document (optional)
Document summaryPdf = await summaryCopilot.GetSummaryDocumentAsync();
```

The `Document` object now contains a single page with the summary, using default fonts and margins.

## Step 9: Save the Summary PDF (how to save pdf file c#)

Finally, write the PDF to disk. The `SaveSummaryAsync` helper does the heavy lifting, but you can also call `summaryPdf.Save` directly if you prefer more control.

```csharp
// Step 9: Save the summary PDF to the output folder
string outputPath = Path.Combine(outputDirectory, "Summary_out.pdf");
await summaryCopilot.SaveSummaryAsync(outputPath);
Console.WriteLine($"Summary PDF saved to: {outputPath}");
```

> **Tip:** If you need custom page size or branding, modify `summaryPdf` before saving—add headers, footers, or a company logo.

## Full Working Example

Putting all the pieces together, here’s the complete, ready‑to‑run program:

```csharp
using System;
using System.IO;
using System.Threading.Tasks;
using Aspose.Pdf;
using Aspose.Pdf.AI;

class Program
{
    static async Task Main(string[] args)
    {
        // 1️⃣ Output folder
        string outputDirectory = Path.Combine(Environment.CurrentDirectory, "output");
        Directory.CreateDirectory(outputDirectory);

        // 2️⃣ OpenAI client (openai client c# example)
        using var openAiClient = OpenAIClient
            .CreateWithApiKey("YOUR_OPENAI_API_KEY")
            .Build();

        // 3️⃣ Summary options (summarize pdf with openai)
        var summaryOptions = OpenAISummaryCopilotOptions
            .Create()
            .WithTemperature(0.5)
            .WithDocument(Path.Combine(Environment.CurrentDirectory, "input.pdf"));

        // 4️⃣ Copilot creation
        ISummaryCopilot summaryCopilot = AICopilotFactory.CreateSummaryCopilot(openAiClient, summaryOptions);

        // 5️⃣ Get raw text (optional)
        string summaryText = await summaryCopilot.GetSummaryAsync();
        Console.WriteLine("=== Summary Text ===");
        Console.WriteLine(summaryText);

        // 6️⃣ Get PDF document (create summary pdf file)
        Document summaryPdf = await summaryCopilot.GetSummaryDocumentAsync();

        // 7️⃣ Save the PDF (how to save pdf file c#)
        string outputPath = Path.Combine(outputDirectory, "Summary_out.pdf");
        await summaryCopilot.SaveSummaryAsync(outputPath);
        Console.WriteLine($"Summary PDF saved to: {outputPath}");
    }
}
```

Run it with:

```bash
dotnet run
```

If everything is set up correctly, you’ll see the summary printed in the console and a `Summary_out.pdf` file appear under the `output` folder.

## Common Questions & Edge Cases

### What if the source PDF is password‑protected?

Aspose.Pdf can open encrypted files by supplying the password in the `Document` constructor:

```csharp
var doc = new Document("encrypted.pdf", new LoadOptions { Password = "mySecret" });
summaryOptions.WithDocument(doc);
```

### How do I control the length of the summary?

Adjust the `WithTemperature` or add a `WithMaxTokens` call (if supported) to limit output size. Lower temperatures usually produce shorter, more factual summaries.

### Can I summarize multiple PDFs in one run?

Yes. Loop over a collection of file paths, re‑using the same `openAiClient` but creating a fresh `summaryOptions` and copilot for each document. The client is thread‑safe, so you could even parallelize the operation with `Task.WhenAll`.

### What if I need a custom page header/footer?

After `await summaryCopilot.GetSummaryDocumentAsync();` you have a `Document` object you can manipulate:

```csharp
var header = new HeaderFooter();
header.Paragraphs.Add(new TextFragment("Company Confidential"));
summaryPdf.Pages[1].Header = header;
```

Then save the modified document as shown earlier.

## Performance Tips

- **Reuse the OpenAI client** across multiple summarizations to avoid repeated TLS handshake overhead.  
- **Batch small PDFs** together if you have a high‑volume scenario; the API allows sending multiple pages in a single request.  
- **Cache the summary** if the same document is processed repeatedly—store the text or PDF in a database and skip the API call.

## Recap

We’ve covered everything you need to **extract summary from PDF** using an **openai client c# example**, turned that summary into a **create summary pdf file**, and demonstrated the proper way to **how to save pdf file c#**. With these building blocks you can now integrate PDF summarization into reporting pipelines, document management systems, or even chat‑bot assistants that need quick digests of long manuals.

Ready for the next step? Try adding a UI front‑end with ASP.NET Core, or experiment with different OpenAI models (e.g., `gpt‑4o-mini`)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}