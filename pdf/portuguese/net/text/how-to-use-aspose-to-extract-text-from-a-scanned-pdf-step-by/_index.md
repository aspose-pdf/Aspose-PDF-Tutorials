---
category: general
date: 2026-08-04
description: Como usar o Aspose para extrair texto de PDF escaneado e converter PDF
  em texto com C#. Aprenda a ler arquivos PDF escaneados e obter resultados confiáveis
  de OCR.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use aspose
- extract scanned pdf text
- convert pdf to text
- read scanned pdf
- how to extract text
language: pt
lastmod: 2026-08-04
og_description: Como usar o Aspose para ler arquivos PDF digitalizados, extrair texto
  de PDF digitalizado e converter PDF em texto com um exemplo completo e executável.
og_image_alt: Screenshot showing how to use Aspose OCR copilot to extract text from
  a scanned PDF
og_title: Como usar o Aspose – extrair texto de PDFs digitalizados em C#
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: How to use Aspose to extract scanned PDF text and convert PDF to text
    with C#. Learn to read scanned PDF files and get reliable OCR results.
  headline: How to use Aspose to extract text from a scanned PDF – step‑by‑step guide
  type: TechArticle
- questions:
  - answer: Yes. Add `.WithPassword("yourPassword")` to the options builder before
      creating the copilot.
    question: Does this work with password‑protected PDFs?
  - answer: Use `GetTextStructureAsync()` instead of `GetTextAsync()`. The method
      returns a JSON payload that includes page indices, bounding boxes, and confidence
      scores.
    question: Can I extract text in a structured format (e.g., JSON with page numbers)?
  - answer: 'The plain‑text extraction flattens tables into line‑break‑separated rows.
      For richer data, request the PDF‑to‑HTML conversion (`GetHtmlAsync`) and parse
      the HTML table elements. ## Conclusion You now know **how to use Aspose** to
      read a scanned PDF, extract scanned PDF text, and **convert PDF to tex'
    question: What if the PDF contains tables?
  type: FAQPage
tags:
- Aspose.PDF.AI
- OCR
- C#
- PDF processing
title: Como usar o Aspose para extrair texto de um PDF escaneado – guia passo a passo
url: /pt/net/text/how-to-use-aspose-to-extract-text-from-a-scanned-pdf-step-by/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como usar Aspose para extrair texto de um PDF escaneado – guia passo a passo

Se você precisa **como usar Aspose** para OCR, este guia mostra como extrair texto de PDF escaneado em algumas linhas de C#. Seja você quem está construindo um serviço de arquivamento de documentos ou um índice de busca para papéis legados, a solução funciona com qualquer PDF escaneado que você enviar ao serviço Aspose.Pdf.AI.

Neste tutorial você irá:

* Criar um copilot OCR que lê um PDF escaneado.
* Extrair o texto reconhecido de forma assíncrona.
* Exibir ou processar ainda mais a string extraída.

O único pré‑requisito é uma assinatura ativa do Aspose.Pdf.AI e um ambiente de desenvolvimento .NET 6 (ou posterior).

## Pré‑requisitos

| Requisito | Por que é importante |
|-------------|----------------|
| .NET 6 SDK ou mais recente | Fornece `async Main` e recursos modernos da linguagem. |
| Pacote NuGet Aspose.Pdf.AI (`Aspose.Pdf.AI`) | Contém o `AICopilotFactory` e opções de OCR. |
| Uma instância válida de `client` Aspose.Pdf.AI (chave de API) | Autentica suas solicitações ao serviço em nuvem. |
| Um arquivo PDF escaneado (ex.: `Scanned.pdf`) | O documento fonte do qual o texto será extraído. |

Instale o pacote com a CLI do .NET:

```bash
dotnet add package Aspose.Pdf.AI
```

## Passo 1: Configurar o cliente Aspose.Pdf.AI

Antes de chamar qualquer endpoint de OCR, você deve criar um cliente que contenha suas credenciais de API. O cliente é thread‑safe e pode ser reutilizado para vários documentos.

```csharp
using Aspose.Pdf.AI;
using Aspose.Pdf.AI.Models;

// Replace with your actual API key and base URL if you use a private cloud.
var client = new PdfAiClient(new PdfAiConfiguration
{
    ApiKey = "YOUR_API_KEY",
    // BaseUrl = "https://api.aspose.cloud" // default, change only if needed
});
```

**Por que este passo é necessário** – O serviço Aspose valida cada solicitação contra sua assinatura. Criar o cliente uma única vez evita handshakes de rede repetidos e mantém o código limpo.

## Passo 2: Criar um copilot OCR para o documento PDF escaneado

O `AICopilotFactory` cria um copilot OCR especializado que sabe como processar o arquivo que você especificar. Você passa o `client` e um objeto `OpenAIOcrOptions` que aponta para o caminho do PDF.

```csharp
using Aspose.Pdf.AI;

// Step 2: Build the OCR copilot
var ocrCopilot = AICopilotFactory.CreateOcrCopilot(
    client,                                   // Your Aspose.Pdf.AI client instance
    OpenAIOcrOptions.Create()
        .WithDocument("YOUR_DIRECTORY/Scanned.pdf") // Path to the scanned PDF
);
```

**Explicação** – `CreateOcrCopilot` encapsula todas as chamadas HTTP de baixo nível. O método `WithDocument` informa ao serviço qual arquivo analisar; você também pode fornecer um `Stream` se o PDF estiver em memória.

## Passo 3: Extrair o texto reconhecido de forma assíncrona

Chamar `GetTextAsync` executa a operação de OCR na nuvem e devolve o resultado em texto simples. Como a operação pode levar alguns segundos, o método é assíncrono.

```csharp
// Step 3: Perform OCR and get the text
string ocrText = await ocrCopilot.GetTextAsync();
```

**Por que assíncrono?** – Latência de rede e tempo de processamento de OCR são imprevisíveis. Usar `await` impede que sua aplicação bloqueie a thread principal, o que é especialmente importante em cenários de UI ou serviços web.

## Passo 4: Usar o texto extraído

Neste ponto você tem uma `string` .NET regular contendo a transcrição completa do PDF escaneado. Você pode escrevê‑la no console, armazená‑la em um banco de dados ou enviá‑la para um motor de busca.

```csharp
// Step 4: Display the result
Console.WriteLine("=== OCR Result ===");
Console.WriteLine(ocrText);
```

### Saída esperada

Se `Scanned.pdf` contiver uma única página com a frase “Hello, world!”, o console mostrará:

```
=== OCR Result ===
Hello, world!
```

Para documentos com várias páginas, a saída concatena o texto de cada página, preservando quebras de linha.

## Exemplo completo, executável

Abaixo está um programa completo que você pode colar em um novo projeto de console (`dotnet new console`). Ele demonstra **como usar Aspose** do início ao fim, incluindo tratamento de erros para armadilhas comuns.

```csharp
using System;
using System.Threading.Tasks;
using Aspose.Pdf.AI;
using Aspose.Pdf.AI.Models;

namespace AsposeOcrDemo
{
    class Program
    {
        static async Task Main(string[] args)
        {
            // 1️⃣ Initialize the Aspose.Pdf.AI client
            var client = new PdfAiClient(new PdfAiConfiguration
            {
                ApiKey = "YOUR_API_KEY"
                // BaseUrl = "https://api.aspose.cloud" // optional
            });

            // 2️⃣ Build the OCR copilot for the target PDF
            var pdfPath = "YOUR_DIRECTORY/Scanned.pdf";
            var ocrCopilot = AICopilotFactory.CreateOcrCopilot(
                client,
                OpenAIOcrOptions.Create().WithDocument(pdfPath)
            );

            try
            {
                // 3️⃣ Extract text asynchronously
                string ocrText = await ocrCopilot.GetTextAsync();

                // 4️⃣ Use the extracted text (display in console)
                Console.WriteLine("=== OCR Result ===");
                Console.WriteLine(ocrText);
            }
            catch (Exception ex)
            {
                // Common errors: invalid API key, missing file, unsupported PDF version
                Console.Error.WriteLine($"Error during OCR: {ex.Message}");
            }
        }
    }
}
```

**Pontos principais no exemplo**

* `await` garante execução não bloqueante.
* O bloco `try/catch` expõe erros de rede ou do serviço, o que é essencial ao **ler PDFs escaneados** em escala.
* Substitua `YOUR_API_KEY` e `YOUR_DIRECTORY/Scanned.pdf` por valores reais antes de executar.

## Tratamento de casos extremos e dicas de boas práticas

| Situação | Abordagem recomendada |
|-----------|----------------------|
| **Large PDFs ( > 50 MB )** | Divida o documento em partes menores no lado do cliente e processe cada parte com um copilot separado. Isso reduz a pressão de memória e melhora a confiabilidade. |
| **Low‑quality scans** | Ajuste a qualidade do OCR adicionando `.WithLanguage("eng")` ou `.WithEnhanceImage(true)` ao `OpenAIOcrOptions`. O serviço oferece dicas de idioma que aumentam a precisão. |
| **Multiple languages** | Forneça uma lista separada por vírgulas, ex.: `.WithLanguage("eng,spa")`. O motor de OCR detectará e transcreverá ambos os idiomas. |
| **Non‑PDF image files** | Converta a imagem para PDF primeiro (biblioteca `Aspose.Pdf`) ou use `OpenAIOcrOptions.WithImage` para enviar a imagem diretamente. |
| **Rate‑limit exceeded** | Implemente back‑off exponencial e lógica de retry; a API Aspose retorna HTTP 429 quando você ultrapassa a cota. |

### Dica profissional

Cache o resultado `ocrText` se você planeja reutilizá‑lo mais tarde. A operação de OCR é a parte mais cara do fluxo de trabalho, e reutilizar a string evita chamadas duplicadas à API e economiza créditos.

## Perguntas frequentes

**Q: Isso funciona com PDFs protegidos por senha?**  
A: Sim. Adicione `.WithPassword("yourPassword")` ao construtor de opções antes de criar o copilot.

**Q: Posso extrair texto em um formato estruturado (ex.: JSON com números de página)?**  
A: Use `GetTextStructureAsync()` em vez de `GetTextAsync()`. O método devolve um payload JSON que inclui índices de página, caixas delimitadoras e pontuações de confiança.

**Q: E se o PDF contiver tabelas?**  
A: A extração em texto simples achata as tabelas em linhas separadas por quebras. Para dados mais ricos, solicite a conversão PDF‑para‑HTML (`GetHtmlAsync`) e analise os elementos de tabela HTML.

## Conclusão

Agora você sabe **como usar Aspose** para ler um PDF escaneado, extrair texto de PDF escaneado e **converter PDF em texto** com um programa C# mínimo. O processo consiste em criar um copilot OCR, chamar `GetTextAsync` e tratar a string resultante. Seguindo as recomendações para casos extremos, você pode escalar a solução para grandes lotes de documentos, conteúdo multilíngue e PDFs seguros.

Em seguida, você pode explorar:

* **Como extrair texto** com preservação de layout (`GetHtmlAsync`).
* Usar Aspose.Pdf.AI para **extrair tabelas** e exportá‑las para CSV.
* Integrar a saída OCR ao Azure Cognitive Search para arquivos de documentos pesquisáveis.

Bom codificação, e aproveite a precisão que o OCR alimentado por IA da Aspose traz aos seus fluxos de trabalho com PDFs escaneados!

## O que você deve aprender a seguir?

Os tutoriais a seguir cobrem tópicos intimamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Extrair texto de arquivos PDF usando Aspose.PDF para .NET](/pdf/english/net/text-operations/extract-text-pdf-aspose-dotnet/)
- [Como extrair texto de regiões específicas em PDFs usando Aspose.PDF para .NET](/pdf/english/net/text-operations/extract-text-specific-region-aspose-pdf-net/)
- [Como extrair texto destacado de PDFs usando Aspose.PDF para .NET](/pdf/english/net/text-operations/extract-highlighted-text-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}