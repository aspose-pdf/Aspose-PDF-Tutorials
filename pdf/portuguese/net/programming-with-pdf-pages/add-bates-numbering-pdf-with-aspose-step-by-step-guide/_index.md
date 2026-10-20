---
category: general
date: 2026-08-08
description: Adicionar numeração Bates em PDF usando Aspose.Pdf em C#. Este tutorial
  também mostra como adicionar uma página em branco ao PDF e gerar PDF programaticamente.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add bates numbering pdf
- add blank page pdf
- generate pdf programmatically
- create pdf aspose
language: pt
lastmod: 2026-08-08
og_description: Adicione numeração Bates a PDFs com Aspose.Pdf em C#. Aprenda a adicionar
  página em branco ao PDF, gerar PDFs programaticamente e salvar o documento final
  em minutos.
og_image_alt: Screenshot of C# code adding Bates numbering and a blank page to a PDF
  using Aspose.Pdf
og_title: Adicionar numeração Bates a PDF com Aspose – guia completo em C#
schemas:
- author: Aspose
  dateModified: '2026-08-08'
  description: Add bates numbering pdf using Aspose.Pdf in C#. This tutorial also
    shows how to add blank page pdf and generate pdf programmatically.
  headline: Add bates numbering pdf with Aspose – step‑by‑step guide
  type: TechArticle
- description: Add bates numbering pdf using Aspose.Pdf in C#. This tutorial also
    shows how to add blank page pdf and generate pdf programmatically.
  name: Add bates numbering pdf with Aspose – step‑by‑step guide
  steps:
  - name: What if I need a different font or position?
    text: 'The `BatesNumberingArtifact` exposes properties such as `FontSize`, `FontColor`,
      `HorizontalAlignment`, and `VerticalAlignment`. For example:'
  - name: How do I exclude a specific page from numbering?
    text: Create a separate `BatesNumberingArtifact` for the pages you want to number
      and add it only to those pages. Pages without an attached artifact will remain
      unnumbered.
  - name: Does this work with existing PDFs?
    text: 'Yes. Instead of `new Document()`, load an existing file:'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF generation
- Bates numbering
title: Adicionar numeração Bates ao PDF com Aspose – guia passo a passo
url: /pt/net/programming-with-pdf-pages/add-bates-numbering-pdf-with-aspose-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Add bates numbering pdf with Aspose – guia passo a passo

Adicionar bates numbering pdf com Aspose.Pdf é simples uma vez que você entende as etapas principais. Se você também precisar adicionar blank page pdf ou gerar pdf programmatically, este guia cobre tudo o que você precisa.

In this tutorial you will:

* Create a new PDF document from scratch.  
* Add a blank page pdf that will host the Bates numbers.  
* Configure the Bates numbering artifact with a custom prefix.  
* Save the PDF so the numbers appear on the generated file.  

By the end you will have a fully functional C# console application that produces a PDF containing Bates numbers like **CASE‑1000**, **CASE‑1001**, … – a common requirement for legal and e‑discovery workflows.

## Pré-requisitos

* .NET 6.0 SDK ou posterior (o código também funciona com .NET Framework 4.8).  
* Visual Studio 2022 ou qualquer IDE compatível com C#.  
* Uma licença válida do Aspose.Pdf for .NET (ou uma chave de avaliação gratuita).  
* Familiaridade básica com a sintaxe C#.

> **Dica:** Se você executar o código sem uma licença, a Aspose adicionará uma pequena marca d'água ao PDF de saída.

## Etapa 1: Configurar o projeto e importar Aspose.Pdf

Create a new console project and add the Aspose.Pdf NuGet package:

```bash
dotnet new console -n BatesNumberingDemo
cd BatesNumberingDemo
dotnet add package Aspose.Pdf
```

The `using` directives required for the example are:

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Artifacts;
```

These namespaces give you access to the `Document`, `Page`, and `BatesNumberingArtifact` classes used later.

## Etapa 2: Add a blank page pdf

A Bates number must be attached to a page, so we first create a blank page that will receive the numbering artifact.

```csharp
// Step 2: Add a blank page pdf
Document pdfDocument = new Document();          // creates an empty PDF
Page pdfPage = pdfDocument.Pages.Add();         // adds the first (blank) page
```

The `Document` class represents the whole PDF file, while `Pages.Add()` inserts a new, empty page at the end of the document’s page collection. Because the document starts empty, this call also creates the first page.

## Etapa 3: Configurar o BatesNumberingArtifact

Now we define how the Bates numbers should look. The `BatesNumberingArtifact` lets you set the start number, prefix, suffix, and formatting options.

```csharp
// Step 3: Define Bates numbering settings
BatesNumberingArtifact batesArtifact = new BatesNumberingArtifact(pdfPage)
{
    StartNumber = 1000,          // first number in the sequence
    Prefix = "CASE-",            // custom prefix before each number
    // Optional: you can also set Suffix, FontSize, FontColor, etc.
};
```

**Por que isso importa:**  
Setting `StartNumber` to **1000** matches typical legal case file conventions. The `Prefix` ensures each number appears as **CASE‑1000**, **CASE‑1001**, … which is easier to search and sort.

## Etapa 4: Anexar o artifact à página

The artifact must be added to the page’s `Artifacts` collection so that Aspose renders it on every page during saving.

```csharp
// Step 4: Attach the Bates numbering artifact to the PDF page
pdfPage.Artifacts.Add(batesArtifact);
```

When the document is saved, Aspose automatically repeats the artifact on all pages, incrementing the number for each subsequent page.

## Etapa 5: (Opcional) Adicionar páginas adicionais

If you need more pages, simply repeat `pdfDocument.Pages.Add()`. The Bates numbering artifact you attached in the previous step will automatically appear on each new page.

```csharp
// Example: add two more pages
pdfDocument.Pages.Add();
pdfDocument.Pages.Add();
```

## Etapa 6: Salvar o PDF – gerar pdf programmatically

Finally, persist the document to disk. This is the point where the Bates numbers are rendered onto the pages.

```csharp
// Step 6: Save the PDF – generate pdf programmatically
string outputPath = Path.Combine(
    Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
    "BatesNumberedDocument.pdf");

// Ensure the directory exists
Directory.CreateDirectory(Path.GetDirectoryName(outputPath)!);

pdfDocument.Save(outputPath);
Console.WriteLine($"PDF saved to: {outputPath}");
```

**Resultado esperado:**  
Open *BatesNumberedDocument.pdf* and you will see a three‑page PDF. Each page displays a Bates number in the bottom‑right corner:

* Página 1 → **CASE‑1000**  
* Página 2 → **CASE‑1001**  
* Página 3 → **CASE‑1002**

The numbers are automatically incremented because the artifact is attached to the page collection.

## Exemplo completo e executável

Putting everything together, here is a complete console program you can copy, paste, and run:

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Artifacts;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main()
        {
            // Create a new PDF document
            Document pdfDocument = new Document();

            // Add a blank page pdf
            Page pdfPage = pdfDocument.Pages.Add();

            // Define Bates numbering settings (add bates numbering pdf)
            BatesNumberingArtifact batesArtifact = new BatesNumberingArtifact(pdfPage)
            {
                StartNumber = 1000,
                Prefix = "CASE-"
            };

            // Attach the artifact to the page
            pdfPage.Artifacts.Add(batesArtifact);

            // (Optional) add more pages to see incremented numbers
            pdfDocument.Pages.Add(); // page 2
            pdfDocument.Pages.Add(); // page 3

            // Save the PDF – generate pdf programmatically
            string outputPath = Path.Combine(
                Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
                "BatesNumberedDocument.pdf");

            Directory.CreateDirectory(Path.GetDirectoryName(outputPath)!);
            pdfDocument.Save(outputPath);

            Console.WriteLine($"PDF saved to: {outputPath}");
        }
    }
}
```

Run the program with `dotnet run`. After execution, locate the file on your desktop and verify the Bates numbers.

![Exemplo de adição de numeração bates pdf](/images/bates-numbering.png "Exemplo de adição de numeração bates pdf")

## Perguntas comuns e casos extremos

### E se eu precisar de uma fonte ou posição diferente?

The `BatesNumberingArtifact` exposes properties such as `FontSize`, `FontColor`, `HorizontalAlignment`, and `VerticalAlignment`. For example:

```csharp
batesArtifact.FontSize = 12;
batesArtifact.FontColor = Color.Blue;
batesArtifact.HorizontalAlignment = HorizontalAlignment.Left;
batesArtifact.VerticalAlignment = VerticalAlignment.Top;
```

### Como excluir uma página específica da numeração?

Create a separate `BatesNumberingArtifact` for the pages you want to number and add it only to those pages. Pages without an attached artifact will remain unnumbered.

### Isso funciona com PDFs existentes?

Yes. Instead of `new Document()`, load an existing file:

```csharp
Document pdfDocument = new Document("input.pdf");
```

Then attach the artifact to the desired pages and save.

## Conclusão

You now know how to **add bates numbering pdf** using Aspose.Pdf, how to **add blank page pdf**, and how to **generate pdf programmatically** in a clean, reusable C# solution. The approach works with any number of pages, custom prefixes, and styling options, giving you full control over the final document.

Next steps you might explore:

* Use **create pdf as

## O que você deve aprender a seguir?

The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Como adicionar e personalizar números de página em PDFs usando Aspose.PDF para .NET | Guia de Manipulação de Documentos](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [Como adicionar uma página vazia ao final de um PDF usando Aspose.PDF para .NET | Guia passo a passo](/pdf/english/net/document-manipulation/add-empty-page-end-pdf-aspose-pdf-net/)
- [Criar documento PDF com Aspose.PDF – adicionar página, forma e salvar](/pdf/english/net/document-creation/create-pdf-document-with-aspose-pdf-add-page-shape-save/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}