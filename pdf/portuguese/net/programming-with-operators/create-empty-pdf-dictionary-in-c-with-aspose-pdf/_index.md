---
category: general
date: 2026-08-14
description: Crie um dicionário PDF vazio em C# usando Aspose.Pdf – aprenda como adicionar
  um estado gráfico à coleção ExtGState e modificar PDFs programaticamente.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create empty PDF dictionary
- Aspose.Pdf Document
- PDF graphics state
- ExtGState dictionary
- CosPdfDictionary usage
language: pt
lastmod: 2026-08-14
og_description: Crie um dicionário PDF vazio em C# com Aspose.Pdf. Siga este guia
  completo para adicionar um estado gráfico personalizado à coleção ExtGState de um
  PDF.
og_image_alt: Screenshot showing C# code that creates an empty PDF dictionary with
  Aspose.Pdf
og_title: Criar dicionário PDF vazio em C# – Guia passo a passo do Aspose.Pdf
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: Create empty PDF dictionary in C# using Aspose.Pdf – learn how to add
    a graphics state to the ExtGState collection and modify PDFs programmatically.
  headline: Create empty PDF dictionary in C# with Aspose.Pdf
  type: TechArticle
- description: Create empty PDF dictionary in C# using Aspose.Pdf – learn how to add
    a graphics state to the ExtGState collection and modify PDFs programmatically.
  name: Create empty PDF dictionary in C# with Aspose.Pdf
  steps:
  - name: Create a new **Console App** project in Visual Studio.
    text: Create a new **Console App** project in Visual Studio.
  - name: 'Open the **NuGet Package Manager** and install `Aspose.Pdf`:'
    text: 'Open the **NuGet Package Manager** and install `Aspose.Pdf`:'
  - name: 'Add the following `using` directives at the top of `Program.cs`:'
    text: 'Add the following `using` directives at the top of `Program.cs`:'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Criar dicionário PDF vazio em C# com Aspose.Pdf
url: /pt/net/programming-with-operators/create-empty-pdf-dictionary-in-c-with-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar dicionário PDF vazio em C# com Aspose.Pdf

Se você precisa **criar dicionário PDF vazio** objetos enquanto trabalha com arquivos PDF, este guia mostra exatamente como fazer isso em C# usando a biblioteca Aspose.Pdf. Seja construindo um estado gráfico personalizado, adicionando um novo recurso ou preparando um modelo para uso futuro, os passos abaixo fornecem uma solução completa e executável.

Você aprenderá como carregar um PDF, acessar o dicionário de recursos da primeira página, construir um novo `CosPdfDictionary` e inseri-lo na coleção `ExtGState`. Ao final do tutorial você terá um `output.pdf` funcional que contém o dicionário recém‑criado.

## Pré-requisitos

Antes de começar, certifique‑se de que você tem:

- .NET 6.0 ou superior (o código também funciona com .NET Framework 4.6+)
- Visual Studio 2022 ou qualquer IDE C# de sua preferência
- Uma licença Aspose.Pdf para .NET (ou uma chave de avaliação temporária)
- Um PDF de exemplo chamado **input.pdf** colocado em uma pasta que você controla (o caminho da pasta será usado como `dataDir`)

Nenhum pacote NuGet adicional é necessário além de `Aspose.Pdf`.

## Etapa 1: Configurar o projeto e referenciar Aspose.Pdf

1. Crie um novo projeto **Console App** no Visual Studio.  
2. Abra o **NuGet Package Manager** e instale `Aspose.Pdf`:

   ```bash
   dotnet add package Aspose.Pdf
   ```

3. Adicione as seguintes diretivas `using` no topo de `Program.cs`:

   ```csharp
   using Aspose.Pdf;
   using Aspose.Pdf.Text;
   using Aspose.Pdf.Operators;
   using Aspose.Pdf.Facades;
   using Aspose.Pdf.InteractiveFeatures;
   using Aspose.Pdf.Xmp;
   using Aspose.Pdf.Operators.Filters;
   using Aspose.Pdf.Operators.Gfx;
   ```

   *Por que esses namespaces?* `Aspose.Pdf` contém a classe principal `Document`, enquanto `Aspose.Pdf.Operators.Gfx` fornece `CosPdfDictionary`, `CosPdfNumber` e objetos PDF de baixo nível relacionados necessários para **criar dicionário PDF vazio**.

## Etapa 2: Carregar o PDF de origem

A primeira operação é carregar o arquivo PDF existente em uma instância `Document`. Isso lhe dá acesso a todas as páginas, recursos e dicionários de baixo nível.

```csharp
// Step 2: Load the PDF document
string dataDir = @"C:\MyPdfFolder\";               // Change to your folder
using var pdfDocument = new Document(dataDir + "input.pdf");
```

*Explicação*: `Document` lê o arquivo para a memória e prepara estruturas internas. A instrução `using` garante que o manipulador de arquivo seja liberado após concluirmos o processamento.

## Etapa 3: Acessar o dicionário de recursos da primeira página

Cada página PDF possui um dicionário **Resources** que agrupa fontes, imagens, objetos ExtGState e outros recursos compartilhados. Para inserir um novo estado gráfico, precisamos editar esse dicionário.

```csharp
// Step 3: Get the first page and its Resources dictionary
Page firstPage = pdfDocument.Pages[1];                     // PDF pages are 1‑based
DictionaryEditor resourcesEditor = new DictionaryEditor(firstPage.Resources);
```

`DictionaryEditor` é uma classe auxiliar que permite tratar um dicionário PDF como um `Dictionary<string, object>` do C#.

## Etapa 4: Recuperar (ou criar) a coleção ExtGState

`ExtGState` contém objetos de estado gráfico como opacidade, modo de mesclagem e espessura de linha. Se o PDF de origem já contém uma entrada `ExtGState`, reutilizamos; caso contrário, criamos um novo dicionário vazio.

```csharp
// Step 4: Ensure an ExtGState dictionary exists
CosPdfDictionary extGStateDict;
if (resourcesEditor.ContainsKey("ExtGState"))
{
    extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
}
else
{
    // Create a brand‑new ExtGState dictionary and add it to Resources
    extGStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
    resourcesEditor["ExtGState"] = extGStateDict;
}
```

*Por que essa verificação?* Alguns PDFs omitem completamente a entrada `ExtGState`. Ao tratar ambos os casos, o tutorial permanece robusto para qualquer arquivo de entrada.

## Etapa 5: **Criar dicionário PDF vazio** para um novo estado gráfico

Agora realmente **criamos objetos dicionário PDF vazio** que definem os parâmetros do estado gráfico. O dicionário começa vazio, e adicionamos as chaves necessárias:

```csharp
// Step 5: Build a new graphics state dictionary (empty PDF dictionary + entries)
CosPdfDictionary newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

// Stroke opacity (CA) – 1 means fully opaque strokes
newGraphicsState.Add("CA", new CosPdfNumber(1));

// Fill opacity (ca) – 0.5 makes semi‑transparent fills
newGraphicsState.Add("ca", new CosPdfNumber(0.5));

// Blend mode (BM) – "Normal" is the default compositing mode
newGraphicsState.Add("BM", new CosPdfName("Normal"));
```

### O que cada entrada faz

| Chave | Tipo | Significado |
|-----|------|------------|
| **CA** | `CosPdfNumber` | Opacidade do traço (intervalo 0‑1). |
| **ca** | `CosPdfNumber` | Opacidade do preenchimento (intervalo 0‑1). |
| **BM** | `CosPdfName`   | Modo de mesclagem; `"Normal"` é o mais comum. |

Como começamos com um **dicionário PDF vazio**, temos controle total sobre quais entradas são adicionadas. Você pode estender esse dicionário com parâmetros adicionais de estado gráfico, como `LW` (espessura da linha) ou `LC` (extremidade da linha), sempre que necessário.

## Etapa 6: Inserir o novo estado gráfico em ExtGState

O dicionário `ExtGState` funciona como um mapa onde cada entrada é identificada por um nome (ex.: `GS0`, `GS1`). Nós adicionamos nosso dicionário recém‑construído sob uma chave única.

```csharp
// Step 6: Add the graphics state to the ExtGState collection
extGStateDict.Add("GS0", newGraphicsState);
```

Se você planeja adicionar múltiplos estados, incremente o sufixo (`GS1`, `GS2`, …) para evitar colisões de nomes.

## Etapa 7: Salvar o PDF modificado

Finalmente, grave as alterações de volta ao disco. O método `Save` serializa automaticamente os dicionários atualizados.

```csharp
// Step 7: Persist the changes
pdfDocument.Save(dataDir + "output.pdf");
```

Abra `output.pdf` em qualquer visualizador de PDF e inspecione a entrada **Resources → ExtGState** (a maioria dos visualizadores oculta isso, mas ferramentas como Adobe Acrobat Preflight ou PDF‑Tron podem revelá‑lo). Você deve ver uma entrada `GS0` contendo os valores de opacidade e modo de mesclagem que definiu.

## Exemplo completo em funcionamento

Juntando todas as peças, aqui está o programa completo que você pode copiar‑colar em `Program.cs` e executar:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Operators.Gfx;

class Program
{
    static void Main()
    {
        // -----------------------------------------------------------------
        // 1️⃣ Load the PDF document
        // -----------------------------------------------------------------
        string dataDir = @"C:\MyPdfFolder\"; // <-- change to your folder
        using var pdfDocument = new Document(dataDir + "input.pdf");

        // -----------------------------------------------------------------
        // 2️⃣ Access the first page’s Resources dictionary
        // -----------------------------------------------------------------
        Page firstPage = pdfDocument.Pages[1];
        var resourcesEditor = new DictionaryEditor(firstPage.Resources);

        // -----------------------------------------------------------------
        // 3️⃣ Retrieve or create the ExtGState dictionary
        // -----------------------------------------------------------------
        CosPdfDictionary extGStateDict;
        if (resourcesEditor.ContainsKey("ExtGState"))
        {
            extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
        }
        else
        {
            extGStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            resourcesEditor["ExtGState"] = extGStateDict;
        }

        // -----------------------------------------------------------------
        // 4️⃣ **Create empty PDF dictionary** for a new graphics state
        // -----------------------------------------------------------------
        var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
        newGraphicsState.Add("CA", new CosPdfNumber(1));          // Stroke opacity
        newGraphicsState.Add("ca", new CosPdfNumber(0.5));        // Fill opacity
        newGraphicsState.Add("BM", new CosPdfName("Normal"));    // Blend mode

        // -----------------------------------------------------------------
        // 5️⃣ Add the graphics state to ExtGState
        // -----------------------------------------------------------------
        extGStateDict.Add("GS0", newGraphicsState);

        // -----------------------------------------------------------------
        // 6️⃣ Save the modified PDF
        // -----------------------------------------------------------------
        pdfDocument.Save(dataDir + "output.pdf");

        Console.WriteLine("PDF saved with new empty dictionary at: " + dataDir + "output.pdf");
    }
}
```

**Saída esperada** – O console imprime uma linha de confirmação, e `output.pdf` contém a nova entrada `GS0` sob `ExtGState`. Quando você renderiza uma página que referencia `GS0` (ex.: via operador de fluxo de conteúdo `gs`), os traços serão totalmente opacos enquanto os preenchimentos terão 50 % de transparência.

## Perguntas comuns e tratamento de casos extremos

| Pergunta | Resposta |
|----------|----------|
| *E se o PDF tiver várias páginas?* | O exemplo foca na primeira página (`Pages[1]`). Para afetar todas as páginas, faça um loop em `pdfDocument.Pages` e repita as etapas 3‑5 para os recursos de cada página. |
| *Posso adicionar o dicionário a uma página que já tem uma entrada ExtGState chamada “GS0”?* | Sim, mas você deve usar uma chave diferente (`GS1`, `GS2`, …) para evitar sobrescrever a entrada existente. |
| *É seguro modificar o dicionário após salvar?* | Depois de chamar `Save`, a representação em memória é desvinculada do arquivo. Você pode continuar editando o objeto `Document` e chamar `Save` novamente, se necessário. |
| *Preciso de uma licença para Aspose.Pdf para usar ` |  |

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Como criar linhas tracejadas em PDFs usando Aspose.PDF para .NET: Um guia passo a passo](/pdf/english/net/images-graphics/create-dashed-lines-aspose-pdf-net/)
- [Como remover gráficos de PDFs usando Aspose.PDF .NET: Um guia completo](/pdf/english/net/images-graphics/remove-graphics-aspose-pdf-net/)
- [Como criar PDFs multilayer usando Aspose.PDF para .NET: Um guia abrangente](/pdf/english/net/advanced-features/create-multi-layer-pdfs-aspose-pdf-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}