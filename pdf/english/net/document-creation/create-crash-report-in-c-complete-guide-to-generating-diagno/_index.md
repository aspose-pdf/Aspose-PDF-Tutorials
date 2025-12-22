---
category: general
date: 2025-12-22
description: Create crash report in C# to capture detailed diagnostic PDF reports.
  Learn how to generate report, catch exception in C#, and handle inner exception
  with Aspose.Pdf.
draft: false
keywords:
- create crash report
- how to generate report
- catch exception in c#
- diagnostic pdf report
- handle inner exception
language: en
og_description: Create crash report in C# quickly. This tutorial shows how to generate
  report, catch exception in C#, and produce a diagnostic PDF report with Aspose.Pdf.
og_title: Create crash report in C# – Step‑by‑Step Diagnostic PDF Guide
tags:
- C#
- exception‑handling
- PDF‑diagnostics
title: Create crash report in C# – Complete Guide to Generating Diagnostic PDF Reports
url: /net/document-creation/create-crash-report-in-c-complete-guide-to-generating-diagno/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create crash report in C# – Complete Guide

Ever needed to **create crash report** for a failing .NET service but weren’t sure which API to call? You’re not alone; most developers hit that wall when an exception bubbles up and they need a concrete PDF for the support team.  

In this tutorial we’ll walk through a real‑world example that **creates a crash report**, shows **how to generate report** programmatically, demonstrates **catch exception in C#** while preserving the **inner exception**, and finally produces a **diagnostic PDF report** you can email straight away.  

## What You’ll Learn

- The exact code you need to generate a crash report with Aspose.Pdf.  
- Why you should wrap the original exception in `CrashReportOptions`.  
- How to **handle inner exception** details so no clue is lost.  
- Tips for customizing the PDF output and troubleshooting common pitfalls.  

### Prerequisites

- .NET 6.0 or later (the API works on .NET Framework too).  
- A reference to the **Aspose.Pdf** NuGet package (`Install-Package Aspose.Pdf`).  
- Basic familiarity with `try / catch` blocks in C#.  

If you’ve got those, you’re ready to dive in—no extra tooling required.

## Step 1 – Simulate an Error with an Inner Exception

First we need something to report on. In practice this would be any method that throws, but for clarity we’ll deliberately throw an exception that contains an inner exception.  

```csharp
using System;
using Aspose.Pdf;

namespace CrashReportDemo
{
    class Program
    {
        static void Main()
        {
            // Trigger the demo
            GenerateCrashReportExample();
        }

        /// <summary>
        /// Demonstrates how to create crash report.
        /// </summary>
        private static void GenerateCrashReportExample()
        {
            // Step 1: Simulate an operation that throws an exception with an inner exception
            try
            {
                // The outer exception gives a high‑level context,
                // the inner one contains the low‑level details.
                throw new Exception(
                    "Top‑level error while processing request",
                    new Exception("Database connection timeout"));
            }
            catch (Exception ex)
            {
                // We now have an exception object (ex) that we can feed
                // into the crash‑report generator.
                CreatePdfCrashReport(ex);
            }
        }
```

> **Why an inner exception?**  
> Most real‑world failures are layered—think of a service error that stems from a failed DB call. Preserving that chain ensures the PDF contains the full story, not just the headline.

## Step 2 – Build the CrashReportOptions Object

Aspose.Pdf expects a `CrashReportOptions` instance that wraps the caught exception. This object also lets you tweak the output folder, file name, and whether stack traces are included.

```csharp
        /// <summary>
        /// Generates a PDF crash report from the supplied exception.
        /// </summary>
        /// <param name="exception">The caught exception (may contain inner exceptions).</param>
        private static void CreatePdfCrashReport(Exception exception)
        {
            // Step 2: Create crash report options based on the caught exception
            var crashOptions = new CrashReportOptions(exception)
            {
                // Optional: customize where the PDF lands
                OutputFolder = Environment.CurrentDirectory,
                // Optional: give the report a meaningful name
                ReportFileName = $"CrashReport_{DateTime.Now:yyyyMMdd_HHmmss}.pdf",
                // Include full stack traces for deep diagnostics
                IncludeStackTrace = true
            };
```

> **Pro tip:** If you’re running inside a Windows Service, point `OutputFolder` to a write‑able path like `Path.GetTempPath()` to avoid permission issues.

## Step 3 – Generate the Diagnostic PDF Report

Now the magic happens. The static `PdfException.GenerateCrashReport` method does all the heavy lifting: it formats the exception hierarchy, adds timestamps, and writes a tidy PDF.

```csharp
            // Step 3: Generate the crash report for diagnostic analysis
            PdfException.GenerateCrashReport(crashOptions);

            Console.WriteLine($"✅ Crash report created at: {crashOptions.OutputFolder}\\{crashOptions.ReportFileName}");
        }
    }
}
```

When you run the program, you’ll see a console line confirming the file location, and a PDF will appear in the same folder as the executable.

### Expected PDF Content

| Section | What you’ll see |
|---------|-----------------|
| **Header** | “Crash Report – Generated on 2025‑12‑22 14:35:12” |
| **Exception Summary** | Top‑level message (“Top‑level error while processing request”) |
| **Inner Exception** | “Database connection timeout” |
| **Stack Trace** | Full .NET stack trace for both exceptions |
| **System Info** | OS version, .NET runtime, machine name (if available) |

Opening the PDF should give you a clean, printable document you can attach to a support ticket.

## How to Generate Report Without Aspose.Pdf (Alternative)

If you can’t use a commercial library, you can still **how to generate report** manually using `System.Drawing` and `PdfSharp`. The steps are identical—capture the exception, format the text, and write a PDF. The code is longer, but the principle stays the same: **catch exception in C#**, extract `Message` and `StackTrace`, then feed them to a PDF writer.

```csharp
// Pseudo‑code for a DIY approach (not production‑ready)
var sb = new StringBuilder();
sb.AppendLine("Crash Report");
sb.AppendLine($"Time: {DateTime.Now}");
sb.AppendLine($"Message: {ex.Message}");
if (ex.InnerException != null)
    sb.AppendLine($"Inner: {ex.InnerException.Message}");
sb.AppendLine("StackTrace:");
sb.AppendLine(ex.StackTrace);

// Use PdfSharp to write sb.ToString() into a PDF page.
```

You’ll rarely need this unless licensing is a blocker, but it’s good to know the **how to generate report** logic isn’t locked to a single library.

## Catch Exception in C# – Best Practices

While the demo above uses a simple `try / catch`, production code should consider:

1. **Specific exception types** – Catch `IOException` separately from `SqlException` to provide richer context.  
2. **Using `ExceptionDispatchInfo`** – If you need to rethrow while preserving the original stack trace.  
3. **Logging before reporting** – Write to a structured logger (Serilog, NLog) so you have both a log entry and a PDF.  

```csharp
catch (SqlException sqlEx)
{
    // Log to file
    logger.Error(sqlEx, "Database failure");
    // Then create PDF report
    CreatePdfCrashReport(sqlEx);
}
```

## Diagnostic PDF Report – Customizing the Look

Aspose.Pdf lets you style the PDF with fonts, colors, and even embed screenshots. Here’s a quick tweak to add a red warning banner at the top:

```csharp
crashOptions.CustomHeader = new HeaderFooter()
{
    // Add a red rectangle with warning text
    Paragraphs = { new TextFragment("⚠️  Crash Detected") { TextState = new TextState { FontSize = 14, FontStyle = FontStyles.Bold, ForegroundColor = Color.Red } } }
};
```

You can also inject your company logo:

```csharp
crashOptions.CustomHeader.Paragraphs.Add(
    new ImageFragment("logo.png") { Width = 100, Height = 50 });
```

These tweaks make the **diagnostic PDF report** look polished for clients.

## Edge Cases & Common Pitfalls

| Situation | What can go wrong | Fix |
|-----------|-------------------|-----|
| **Null exception** | Passing `null` to `CrashReportOptions` throws `ArgumentNullException`. | Guard with `if (ex == null) return;` |
| **Missing write permission** | PDF generation fails silently. | Ensure `OutputFolder` points to a writable directory; catch `UnauthorizedAccessException`. |
| **Large inner exception chain** | PDF becomes huge and unreadable. | Limit depth: `crashOptions.MaxInnerExceptionDepth = 5;` |
| **Unicode characters** | Some symbols appear as �. | Set `crashOptions.Font = FontRepository.FindFont("Arial Unicode MS");` |

Addressing these early saves you from having a crash report that itself crashes.

## Full Working Example (Copy‑Paste Ready)

```csharp
using System;
using Aspose.Pdf;

namespace CrashReportDemo
{
    class Program
    {
        static void Main()
        {
            GenerateCrashReportExample();
        }

        private static void GenerateCrashReportExample()
        {
            try
            {
                // Simulate a failure with an inner exception
                throw new Exception(
                    "Top‑level error while processing request",
                    new Exception("Database connection timeout"));
            }
            catch (Exception ex)
            {
                CreatePdfCrashReport(ex);
            }
        }

        private static void CreatePdfCrashReport(Exception exception)
        {
            var crashOptions = new CrashReportOptions(exception)
            {
                OutputFolder = Environment.CurrentDirectory,
                ReportFileName = $"CrashReport_{DateTime.Now:yyyyMMdd_HHmmss}.pdf",
                IncludeStackTrace = true,
                // Optional styling
                // CustomHeader = new HeaderFooter { /* add logo or banner here */ }
            };

            PdfException.GenerateCrashReport(crashOptions);
            Console.WriteLine($"✅ Crash report created at: {crashOptions.OutputFolder}\\{crashOptions.ReportFileName}");
        }
    }
}
```

Run the program (`dotnet run`) and open the generated PDF. You should see a nicely formatted document containing both the outer and inner exception details, complete stack traces, and a timestamp.

## Conclusion

You now know how to **create crash report** in C# using Aspose.Pdf, how to **how to generate report** automatically, how to **catch exception in C#** while preserving every **inner exception**, and how to turn that information into a polished **diagnostic PDF report**.  

Give it a spin in your own project, swap the simulated error for real business logic, and you’ll have a ready‑to‑send PDF every time something blows up.  

**Next steps:**  
- Explore Aspose.Pdf’s theming options to match your brand.  
- Combine the PDF generation with a background job queue (Hangfire, Azure Functions) for asynchronous reporting.  
- Add a “Send to Support” button that emails the PDF directly from your application.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}