---
category: general
date: 2026-09-08
description: Como usar o Aspose para converter um PDF em PDF/X‑1A especificando um
  perfil ICC. Aprenda as opções de conversão de PDF, como adicionar ICC e carregar
  PDF com Aspose em C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use aspose
- how to add icc
- pdf conversion options
- specify icc profile
- load pdf aspose
language: pt
lastmod: 2026-09-08
og_description: Como usar o Aspose para converter um PDF para PDF/X‑1A especificando
  um perfil ICC. Siga o guia passo a passo que cobre as opções de conversão de PDF
  e como adicionar ICC.
og_image_alt: Diagram showing how to use Aspose to convert a PDF to PDF/X‑1A with
  an ICC profile
og_title: Como usar o Aspose para conversão PDF/X‑1A com um perfil ICC
schemas:
- author: Aspose
  dateModified: '2026-09-08'
  description: How to use Aspose to convert a PDF to PDF/X‑1A while specifying an
    ICC profile. Learn pdf conversion options, how to add icc, and load pdf aspose
    in C#.
  headline: How to use Aspose to convert PDF to PDF/X‑1A with ICC
  type: TechArticle
- description: How to use Aspose to convert a PDF to PDF/X‑1A while specifying an
    ICC profile. Learn pdf conversion options, how to add icc, and load pdf aspose
    in C#.
  name: How to use Aspose to convert PDF to PDF/X‑1A with ICC
  steps:
  - name: – Load the source PDF (load pdf aspose)
    text: '```csharp using System; using Aspose.Pdf; using Aspose.Pdf.Conversion;'
  - name: – Create conversion options and **how to add icc** (specify icc profile)
    text: '```csharp // Create an instance of PdfFormatConversionOptions. // This
      object lets you control the output format and color management. PdfFormatConversionOptions
      conversionOptions = new PdfFormatConversionOptions();'
  - name: – Save as PDF/X‑1A (the final PDF/X‑1A output)
    text: '```csharp // Save the document as PDF/X‑1A, passing the conversion options.
      pdfDocument.Save( dataFolder + "output_pdfx1.pdf", PdfSaveOptions.PdfX1A, conversionOptions);'
  - name: Full, runnable example
    text: Putting the three steps together yields a self‑contained program you can
      copy‑paste into Visual Studio, Rider, or any .NET editor.
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF/X‑1A
title: Como usar o Aspose para converter PDF em PDF/X‑1A com ICC
url: /pt/net/document-conversion/how-to-use-aspose-to-convert-pdf-to-pdf-x-1a-with-icc/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como usar Aspose para converter PDF para PDF/X‑1A com ICC

Se você precisa de **how to use Aspose** para conversão confiável de PDF, este guia mostra exatamente como converter um PDF comum em um arquivo PDF/X‑1A enquanto **especifica um perfil ICC**. A abordagem funciona com a versão mais recente do Aspose.Pdf para .NET e requer apenas algumas linhas de código.

Converter PDFs para o padrão PDF/X‑1A é comum quando você deve atender aos requisitos da indústria de impressão. Além disso, anexar um perfil ICC (International Color Consortium) como **FOGRA39** garante que as cores sejam renderizadas de forma consistente em diferentes dispositivos. Você também aprenderá as **pdf conversion options** que pode ajustar e como **load PDF Aspose** com segurança.

## O que você vai alcançar

* **Load PDF Aspose** usando a classe `Document`.  
* Crie **pdf conversion options** e **specify ICC profile** corretamente.  
* Salve o arquivo como PDF/X‑1A, o formato exigido para fluxos de trabalho de pré-impressão.  
* Entenda armadilhas comuns ao **how to add icc** em uma conversão.

> **Prerequisite** – Você deve ter uma licença Aspose.Pdf para .NET (ou uma chave de avaliação temporária) e .NET 6+ instalado. O código funciona no Windows, Linux ou macOS com os mesmos resultados.

## Como usar Aspose para conversão de PDF com um perfil ICC

Esta seção percorre cada passo. A palavra‑chave principal **how to use Aspose** aparece no cabeçalho, atendendo à regra de SEO de que a palavra‑chave principal esteja em pelo menos um H2.

### Etapa 1 – Carregar o PDF de origem (load pdf aspose)

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Conversion;

class PdfX1AConverter
{
    static void Main()
    {
        // Define the folder that contains the input PDF and the ICC file.
        // Adjust the path to match your environment.
        string dataFolder = @"C:\MyData\";

        // Load PDF aspose. The Document constructor reads the file into memory.
        using (Document pdfDocument = new Document(dataFolder + "input.pdf"))
        {
            // Subsequent steps go here.
```

**Por que isso importa:**  
`Document` é a classe central no Aspose.Pdf. Ela analisa a estrutura do PDF e fornece acesso total a páginas, fontes e recursos. Carregar o arquivo corretamente é a base para qualquer conversão, portanto **load pdf aspose** é a primeira operação que você deve executar.

### Etapa 2 – Criar opções de conversão e **how to add icc** (especificar perfil icc)

```csharp
            // Create an instance of PdfFormatConversionOptions.
            // This object lets you control the output format and color management.
            PdfFormatConversionOptions conversionOptions = new PdfFormatConversionOptions();

            // How to add ICC: set the path to the ICC profile file.
            // The profile must be a valid .icc/.icm file; here we use FOGRA39.
            conversionOptions.IccProfileFileName = dataFolder + "FOGRA39.icc";

            // You can also tweak additional pdf conversion options if needed.
            // For example, conversionOptions.PreserveFormFields = true;
```

**Por que isso importa:**  
O objeto **pdf conversion options** é onde você indica ao Aspose qual espaço de cor usar. Ao atribuir `IccProfileFileName`, você **specify ICC profile** para o arquivo PDF/X‑1A de saída. Esta etapa responde diretamente à pergunta **how to add icc** em uma conversão.

### Etapa 3 – Salvar como PDF/X‑1A (a saída final PDF/X‑1A)

```csharp
            // Save the document as PDF/X‑1A, passing the conversion options.
            pdfDocument.Save(
                dataFolder + "output_pdfx1.pdf",
                PdfSaveOptions.PdfX1A,
                conversionOptions);

            // Inform the user that the process succeeded.
            Console.WriteLine("PDF converted to PDF/X‑1A with ICC profile successfully.");
        }
    }
}
```

**Por que isso importa:**  
`PdfSaveOptions.PdfX1A` indica ao Aspose que produza um arquivo compatível com PDF/X‑1A, que é um subconjunto do PDF 1.3 com requisitos rigorosos de cor e fontes. As `conversionOptions` que você criou na etapa anterior são aplicadas automaticamente, garantindo que a flag **specify icc profile** seja respeitada.

### Exemplo completo e executável

Juntando as três etapas resulta em um programa autônomo que você pode copiar e colar no Visual Studio, Rider ou qualquer editor .NET.



## O que você deve aprender a seguir?

Os tutoriais a seguir cobrem tópicos intimamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Como definir ICC na conversão de PDF Aspose – Guia Completo](/pdf/english/net/document-conversion/how-to-set-icc-in-aspose-pdf-conversion-complete-guide/)
- [Como converter PDFs para PDF/A usando Aspose.PDF para Java : Guia passo a passo](/pdf/english/java/pdfa-compliance/convert-pdf-to-pdfa-aspose-java-guide/)
- [Como rastrear o progresso da conversão de PDF com Aspose.PDF para .NET : Guia passo a passo](/pdf/english/net/conversion-export/track-pdf-conversion-progress-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}