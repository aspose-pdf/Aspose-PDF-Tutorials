---
category: general
date: 2026-08-04
description: Crie um Copiloto de IA para gerar descrições de imagens para arquivos
  PDF. Aprenda como configurar as opções de imagem da OpenAI e extrair descrições
  de imagens de forma eficiente.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create AI copilot
- generate image description
- image description PDF
- OpenAI image options
- extract image description
language: pt
lastmod: 2026-08-04
og_description: Crie um Copiloto de IA para gerar descrições de imagens em arquivos
  PDF. Este tutorial mostra como configurar as opções de imagem da OpenAI, executar
  o copiloto e extrair a descrição da imagem em C#.
og_image_alt: Screenshot of C# code that creates an AI copilot for PDF image description
og_title: Crie um Copiloto de IA para descrição de imagens em PDF – guia completo
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Create AI Copilot to generate image description for PDF files. Learn
    how to configure OpenAI image options and extract image description efficiently.
  headline: Create AI Copilot for PDF image description – step‑by‑step guide
  type: TechArticle
tags:
- Aspose.Pdf.AI
- C#
- PDF processing
title: Crie um Copiloto de IA para descrição de imagens em PDF – guia passo a passo
url: /pt/net/programming-with-images/create-ai-copilot-for-pdf-image-description-step-by-step-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar AI Copilot para descrição de imagens em PDF – guia completo

Se você precisa **criar AI Copilot** que escreve automaticamente descrições para imagens incorporadas em um PDF, este guia mostra exatamente como fazer isso. Você aprenderá a configurar as opções de imagem da OpenAI, executar o copilot e **extrair descrição de imagem** sem sair do seu projeto C#.

Gerar conteúdo textual para imagens em PDF é uma necessidade comum para acessibilidade, indexação de conteúdo e relatórios automatizados. Ao final deste tutorial, você terá um componente reutilizável que **gera descrição de imagem** para qualquer documento PDF que você apontar.

## Pré-requisitos

* .NET 6.0 ou posterior instalado  
* Uma licença Aspose.Pdf.AI (ou um teste gratuito)  
* Uma chave de API OpenAI que o cliente Aspose pode usar  
* Visual Studio 2022 (ou qualquer IDE que suporte C#)  

Nenhum pacote NuGet adicional é necessário além de `Aspose.Pdf.AI`.

## Etapa 1: Configurar o cliente Aspose.Pdf.AI

O primeiro passo é instanciar o cliente AI com seus detalhes de autenticação. O cliente gerencia a comunicação com o serviço OpenAI nos bastidores.

```csharp
using Aspose.Pdf.AI;
using Aspose.Pdf.AI.Models;

// Replace with your actual credentials
var client = new AiClient(new AiClientOptions
{
    ApiKey = Environment.GetEnvironmentVariable("OPENAI_API_KEY"),
    // Optional: set a custom endpoint if you use Azure OpenAI
    // Endpoint = "https://my-openai-instance.openai.azure.com/"
});
```

**Por que isso importa:** O `AiClient` encapsula todas as configurações de nível de requisição (chave de API, timeout, política de retry). Criá‑lo uma vez e reutilizá‑lo em várias instâncias de copilot reduz a sobrecarga e garante autenticação consistente.

## Etapa 2: Criar um Copilot de Descrição de Imagem

Agora você cria o **AI copilot** que lerá o PDF e produzirá uma descrição para cada imagem. O método de fábrica `CreateImageDescriptionCopilot` aceita o cliente e um conjunto de opções que definem como a descrição é gerada.

```csharp
// Configure OpenAI image options – this is where you control model, temperature, etc.
var imageOptions = OpenAIImageDescriptionOptions.Create()
    .WithModel("gpt-4o-mini")           // Choose a model that balances cost and quality
    .WithTemperature(0.7)               // Controls creativity; 0 = deterministic
    .WithMaxTokens(150);                // Maximum length of each description

// Point the copilot at the PDF you want to process
var imgCopilot = AICopilotFactory.CreateImageDescriptionCopilot(
    client,
    imageOptions.WithDocument(@"C:\Reports\AnnualReport.pdf"));
```

**Por que isso importa:**  
* `OpenAIImageDescriptionOptions` (as **opções de imagem da OpenAI**) permitem ajustar finamente o modelo de linguagem. Ajustar a temperatura ou o modelo pode melhorar a relevância para diagramas técnicos versus fotos naturais.  
* Especificar o caminho do documento informa ao copilot qual PDF escanear. O copilot extrai cada imagem raster, envia‑a ao modelo e retorna uma descrição legível por humanos.

## Etapa 3: Recuperar a descrição gerada de forma assíncrona

O copilot funciona de forma assíncrona porque pode precisar enviar vários megabytes de dados de imagem e aguardar a resposta do modelo. Use `await` para garantir que a chamada seja concluída antes de acessar o resultado.

```csharp
try
{
    // Get a dictionary where the key is the page number and the value is the description
    var descriptionMap = await imgCopilot.GetDescriptionAsync();

    // Example: iterate over each image description
    foreach (var entry in descriptionMap)
    {
        Console.WriteLine($"Page {entry.Key}: {entry.Value}");
    }
}
catch (AiException ex)
{
    Console.Error.WriteLine($"AI service error: {ex.Message}");
}
```

**Por que isso importa:** O método retorna um `Dictionary<int, string>` que mapeia cada página (ou índice de imagem) para sua descrição. Tratar `AiException` permite expor erros de rede ou de cota em vez de fazer a aplicação travar.

## Etapa 4: Exibir ou armazenar a descrição

Você pode gravar as descrições no console, em um arquivo de log ou incorporá‑las de volta ao PDF como alt‑text para acessibilidade. Abaixo está um exemplo rápido que grava a saída em um arquivo JSON para consumo posterior.

```csharp
using System.Text.Json;

// Serialize the map to JSON
var json = JsonSerializer.Serialize(descriptionMap, new JsonSerializerOptions { WriteIndented = true });
File.WriteAllText(@"C:\Reports\ImageDescriptions.json", json);

Console.WriteLine("Image descriptions saved to ImageDescriptions.json");
```

**Por que isso importa:** Armazenar a saída como JSON preserva a associação entre cada página e sua descrição, facilitando o consumo dos dados por processos posteriores (indexação de busca, renderização de UI, etc.).

## Manipulando múltiplas imagens por página

Se uma página contém várias imagens, o copilot retorna uma descrição concatenada separada por quebras de linha. Para dividi‑las, inspecione o resultado bruto e divida em `\n\n` (dupla quebra de linha). Aqui está um método auxiliar:

```csharp
static IEnumerable<string> SplitDescriptions(string combined)
{
    return combined.Split(new[] { "\n\n" }, StringSplitOptions.RemoveEmptyEntries);
}
```

Você pode então iterar sobre cada descrição de imagem individual e armazená‑las separadamente, se necessário.

## Caso de borda: PDFs grandes e gerenciamento de timeout

Processar um PDF maior que 100 MB pode exceder os timeouts HTTP padrão. Ajuste a configuração de timeout do cliente ao criar o `AiClient`:

```csharp
var client = new AiClient(new AiClientOptions
{
    ApiKey = Environment.GetEnvironmentVariable("OPENAI_API_KEY"),
    Timeout = TimeSpan.FromMinutes(5)   // Increase timeout for heavy workloads
});
```

Aumentar o timeout impede a terminação prematura enquanto o serviço processa muitas imagens de alta resolução.

## Dica profissional: Cachear resultados para reduzir custos

OpenAI cobra por token, e a descrição de imagem pode ser repetitiva em versões do mesmo relatório. Cacheie a saída JSON e reutilize‑a quando o hash do PDF corresponder a um arquivo já processado. Essa prática economiza dinheiro e acelera execuções subsequentes.

```csharp
static string ComputeFileHash(string path)
{
    using var sha256 = System.Security.Cryptography.SHA256.Create();
    using var stream = File.OpenRead(path);
    var hash = sha256.ComputeHash(stream);
    return Convert.ToHexString(hash);
}
```

Armazene o hash junto ao arquivo JSON; se o hash coincidir em uma execução posterior, pule a chamada AI.

## Exemplo completo executável

Juntando tudo, aqui está um aplicativo console autônomo que você pode colar em um novo projeto .NET.

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using System.Text.Json;
using System.Threading.Tasks;
using Aspose.Pdf.AI;
using Aspose.Pdf.AI.Models;

class Program
{
    static async Task Main()
    {
        // 1️⃣ Initialize AI client
        var client = new AiClient(new AiClientOptions
        {
            ApiKey = Environment.GetEnvironmentVariable("OPENAI_API_KEY"),
            Timeout = TimeSpan.FromMinutes(5)
        });

        // 2️⃣ Configure OpenAI image options and create copilot
        var imageOptions = OpenAIImageDescriptionOptions.Create()
            .WithModel("gpt-4o-mini")
            .WithTemperature(0.7)
            .WithMaxTokens(150);

        string pdfPath = @"C:\Reports\AnnualReport.pdf";

        var imgCopilot = AICopilotFactory.CreateImageDescriptionCopilot(
            client,
            imageOptions.WithDocument(pdfPath));

        // 3️⃣ Retrieve descriptions
        Dictionary<int, string> descriptionMap;
        try
        {
            descriptionMap = await imgCopilot.GetDescriptionAsync();
        }
        catch (AiException ex)
        {
            Console.Error.WriteLine($"Error from AI service: {ex.Message}");
            return;
        }

        // 4️⃣ Output results
        foreach (var entry in descriptionMap)
        {
            Console.WriteLine($"Page {entry.Key}:");
            Console.WriteLine(entry.Value);
            Console.WriteLine(new string('-', 40));
        }

        // 5️⃣ Save to JSON for later use
        string json = JsonSerializer.Serialize(descriptionMap, new JsonSerializerOptions { WriteIndented = true });
        string jsonPath = Path.ChangeExtension(pdfPath, ".descriptions.json");
        await File.WriteAllTextAsync(jsonPath, json);
        Console.WriteLine($"Descriptions saved to {jsonPath}");
    }
}
```

**Saída esperada (truncada)**

```
Page 2:
A bar chart showing quarterly revenue growth, with blue bars representing Q1–Q4.
----------------------------------------
Page 5:
A high‑resolution photograph of the new manufacturing facility, showing the assembly line in operation.
...
Descriptions saved to C:\Reports\AnnualReport.descriptions.json
```

O programa lê `AnnualReport.pdf`, cria um **AI copilot** e grava um arquivo JSON que mapeia cada página para sua descrição gerada.

## Perguntas comuns

* **Isso funciona com PDFs criptografados?**  
  Sim, mas você deve fornecer a senha ao criar o copilot:  
  `imageOptions.WithPassword("mySecret")`.

* **Posso limitar o processamento a páginas específicas?**  
  Use `imageOptions.WithPageRange(1, 10)` para restringir o copilot às páginas 1‑10.

* **E se uma imagem contiver texto?**  
  O modelo tenta descrever o conteúdo visual; para extração de texto no estilo OCR você deve usar `CreateTextExtractionCopilot` em vez disso.

## Conclusão

Agora você sabe como **criar AI Copilot** que **gera descrição de imagem** para arquivos PDF, configurar **opções de imagem da OpenAI** e **extrair descrição de imagem** programaticamente em C#. O exemplo completo demonstra boas práticas como tratamento assíncrono, gerenciamento de erros e cache de resultados.

Em seguida, você pode explorar:

* Adicionar as descrições geradas de volta ao PDF como alt‑text para melhorar a acessibilidade (`PdfDocument` → `PdfImage.AlternativeText`).  
* Usar o mesmo padrão de copilot para **gerar relatórios PDF de descrição de imagem** em processamento em lote.  
* Experimentar diferentes modelos OpenAI ou configurações de temperatura para ajustar o estilo da descrição.

Sinta‑se à vontade para adaptar o código, experimentar documentos maiores e integrar a saída ao seu pipeline de indexação. Feliz codificação!

## O que você deve aprender a seguir?

Os tutoriais a seguir cobrem tópicos estreitamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Criar PDF com Imagem Marcada em Java](/pdf/hindi/java/pdf-structure-elements/create-pdf-with-tagged-image-in-java/)
- [Criar PDF com Imagem Marcada](/pdf/hindi/net/programming-with-tagged-pdf/create-pdf-with-tagged-image/)
- [Criar Imagem PDF Marcada .NET](/pdf/hindi/net/images-graphics/create-tagged-pdf-image-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}