---
category: general
date: 2026-11-16
description: Aprenda como criar o estado gráfico de PDF em C# usando Aspose.Pdf. Este
  guia aborda opacidade, modo de mesclagem e um exemplo completo de código.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create pdf graphics state
- Aspose.Pdf ExtGState
- PDF opacity
- C# PDF manipulation
- PDF blend mode
- Aspose.Pdf graphics state
language: pt
lastmod: 2026-11-16
og_description: Crie o estado gráfico de PDF em C# com Aspose.Pdf. Siga este tutorial
  completo para definir opacidade e modo de mesclagem programaticamente.
og_image_alt: Illustration of how to create PDF graphics state with Aspose.Pdf in
  C#
og_title: Criar estado gráfico de PDF em C# – guia passo a passo do Aspose.Pdf
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Learn how to create PDF graphics state in C# using Aspose.Pdf. This
    guide covers opacity, blend mode, and full code example.
  headline: How to create PDF graphics state in C# with Aspose.Pdf
  type: TechArticle
tags:
- Aspose.Pdf
- C#
- PDF
title: Como criar o estado gráfico de PDF em C# com Aspose.Pdf
url: /pt/net/images-graphics/how-to-create-pdf-graphics-state-in-c-with-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como criar estado gráfico PDF em C# com Aspose.Pdf

Se você precisa **criar estado gráfico PDF** em um projeto .NET, este tutorial mostra exatamente como fazer isso com Aspose.Pdf. Seja para controlar opacidade, mudar o modo de mesclagem ou reutilizar um estado gráfico personalizado em várias páginas, os passos abaixo fornecem uma solução completa e pronta‑para‑executar.

Neste guia você aprenderá como acessar os recursos da página, adicionar uma entrada **ExtGState** e persistir as alterações em um novo arquivo. O exemplo funciona com Aspose.Pdf 23.12 (ou posterior) e tem como alvo .NET 6+, mas os conceitos se aplicam a versões anteriores também.

## Pré‑requisitos

Antes de começar, certifique‑se de que você tem:

* Visual Studio 2022 (ou qualquer IDE C#) com o .NET 6 SDK instalado.  
* Uma licença Aspose.Pdf for .NET ou uma chave de avaliação temporária.  
* Um arquivo PDF chamado `input.pdf` colocado em uma pasta que você possa referenciar a partir do código.  

Nenhum pacote NuGet adicional é necessário além do `Aspose.Pdf`.

## O que o tutorial cobre

* Carregar um documento PDF existente.  
* Navegar até o dicionário de recursos da primeira página.  
* Criar um novo dicionário de estado gráfico que define opacidade de traço (`CA`), opacidade de preenchimento (`ca`) e modo de mesclagem (`BM`).  
* Adicionar o novo estado gráfico à coleção **ExtGState** com um nome personalizado (`GS0`).  
* Salvar o PDF atualizado para que comandos de desenho subsequentes possam referenciar o novo estado.

Ao final do tutorial você será capaz de **criar objetos de estado gráfico PDF** programaticamente e reutilizá‑los em qualquer operação de desenho.

## Etapa 1: Configurar o projeto e importar namespaces

Crie um novo aplicativo de console (ou integre o código em um projeto existente). Adicione a referência Aspose.Pdf e inclua os namespaces necessários:

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Operators;
using Aspose.Pdf.Generator;
```

> **Dica profissional:** Se você estiver usando a versão de avaliação gratuita, adicione `Aspose.Pdf.License license = new Aspose.Pdf.License(); license.SetLicense("Aspose.Pdf.lic");` antes de carregar o documento para evitar mensagens de marca d'água.

## Etapa 2: Carregar o documento PDF

Abrir o arquivo é simples. A classe `Document` representa todo o PDF e fornece acesso às suas páginas e recursos.

```csharp
// Step 2: Load the PDF document
string inputPath = @"YOUR_DIRECTORY\input.pdf";

using (var document = new Document(inputPath))
{
    // All subsequent steps run inside this using block
```

Colocar o código dentro de um bloco `using` garante que o manipulador de arquivo seja liberado após a operação, o que é essencial para **manipulação de PDF em C#** em serviços de produção.

## Etapa 3: Recuperar o dicionário de recursos da primeira página

Cada página PDF possui um dicionário *Resources* que armazena fontes, imagens e estados gráficos. Precisamos de um `DictionaryEditor` para editar essa estrutura.

```csharp
    // Step 3: Get the first page and its resources dictionary
    var page = document.Pages[1];
    var resourcesEditor = new DictionaryEditor(page.Resources);
```

Se o PDF já contiver uma entrada `ExtGState`, `resourcesEditor["ExtGState"]` a retornará; caso contrário, Aspose.Pdf cria um dicionário vazio para nós quando adicionamos a primeira entrada.

## Etapa 4: Acessar ou criar o dicionário ExtGState

O dicionário **ExtGState** contém objetos de estado gráfico nomeados. Buscamos um existente ou criamos um novo contêiner.

```csharp
    // Step 4: Access (or create) the ExtGState dictionary within the resources
    var extGState = resourcesEditor["ExtGState"].ToCosPdfDictionary();
```

Quando `ExtGState` não existir, `resourcesEditor["ExtGState"]` retorna automaticamente um novo dicionário vazio, garantindo que o código funcione para qualquer PDF.

## Etapa 5: Construir o novo dicionário de estado gráfico

Um estado gráfico é um `CosPdfDictionary` com chaves específicas:

* `CA` – opacidade do traço (0‑1)  
* `ca` – opacidade do preenchimento (0‑1)  
* `BM` – modo de mesclagem (`Normal`, `Multiply`, etc.)

Criamos um dicionário vazio, o preenchemos e então o adicionamos ao `ExtGState`.

```csharp
    // Step 5: Create a new graphics state dictionary with desired parameters
    var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(document);
    var parameters = new[]
    {
        new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),   // Stroke opacity (fully opaque)
        new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // Fill opacity (50% transparent)
        new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // Blend mode
    };

    foreach (var p in parameters)
        newGraphicsState.Add(p);
```

Você pode mudar `0.5` para qualquer valor entre `0` e `1` para ajustar a opacidade de preenchimento, ou substituir `"Normal"` por `"Multiply"` para um **modo de mesclagem PDF** diferente. Essa flexibilidade é o que torna a criação de um estado gráfico personalizado uma técnica poderosa no gerenciamento de **estado gráfico Aspose.Pdf**.

## Etapa 6: Registrar o estado gráfico com um nome

Os fluxos de conteúdo PDF referenciam estados gráficos por nome. Aqui usamos `GS0`, mas qualquer nome único funciona.

```csharp
    // Step 6: Add the new graphics state to the ExtGState dictionary with a name (e.g., GS0)
    extGState.Add("GS0", newGraphicsState);
```

Se precisar de múltiplos estados, repita a etapa de criação com parâmetros diferentes e adicione‑os como `GS1`, `GS2`, etc. Esse padrão escala bem para documentos complexos que exigem opacidades ou configurações de mesclagem variadas em diferentes camadas.

## Etapa 7: Salvar o PDF modificado

Por fim, escreva o documento atualizado em um novo arquivo. Manter o original intacto facilita a depuração.

```csharp
    // Step 7: Save the updated PDF document
    string outputPath = @"YOUR_DIRECTORY\output.pdf";
    document.Save(outputPath);
}
```

Após a execução, `output.pdf` contém uma entrada `ExtGState` chamada `GS0`. Qualquer operador de desenho subsequente pode referenciá‑la usando o operador `gs` (por exemplo, `GS0 gs` em um fluxo de conteúdo).  

> **Por que isso importa:** Ao criar um estado gráfico reutilizável você evita repetir configurações de opacidade e mesclagem para cada comando de desenho, o que melhora tanto o desempenho quanto a manutenibilidade.

## Usando o novo estado gráfico em um fluxo de conteúdo (opcional)

Se quiser ver o efeito imediatamente, pode adicionar um retângulo simples que usa o estado que acabamos de criar:

```csharp
using (var document = new Document(outputPath))
{
    var page = document.Pages[1];
    var content = page.Contents[1]; // Get the first content stream

    // Insert graphics state selection and a semi‑transparent rectangle
    var operators = new List<Operator>
    {
        new Operator("GS0", "gs"),                     // Select our custom graphics state
        new Operator("0.5", "w"),                      // Set line width (optional)
        new Operator("100", "100", "200", "150", "re"), // Rectangle (x, y, width, height)
        new Operator("B")                              // Stroke the rectangle
    };

    foreach (var op in operators)
        content.Operators.Add(op);

    document.Save(@"YOUR_DIRECTORY\final_output.pdf");
}
```

O retângulo será desenhado com 50 % de opacidade de preenchimento enquanto o traço permanece totalmente opaco, exatamente como definido no dicionário **create PDF graphics state**.

## Armadilhas comuns e como evitá‑las

| Problema | Por que acontece | Solução |
|----------|------------------|---------|
| Entrada `ExtGState` não encontrada | Alguns PDFs omitem o dicionário completamente. | O `DictionaryEditor` cria‑o automaticamente ao adicionar a primeira entrada, portanto nenhuma verificação extra é necessária. |
| Valores de opacidade > 1 ou < 0 | A especificação PDF limita a opacidade ao intervalo `[0,1]`. | Limite os valores antes de criar `CosPdfNumber`. |
| Erro de digitação no modo de mesclagem | Os nomes de modo de mesclagem PDF diferenciam maiúsculas de minúsculas. | Use nomes exatos como `"Normal"`, `"Multiply"`, `"Screen"`. |
| Marca d'água de licença | A versão de avaliação adiciona marca d'água na primeira página. | Aplique um arquivo de licença válido antes de abrir o documento. |

Tratar esses casos de borda garante que sua implementação de **create PDF graphics state** funcione de forma confiável em diferentes fontes de PDF.

## Exemplo completo, executável

Abaixo está um programa autocontido que você pode copiar, colar e executar. Substitua `YOUR_DIRECTORY` por um caminho de pasta real na sua máquina.

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Generator;

class Program
{
    static void Main()
    {
        // Optional: apply license to remove evaluation watermark
        // var license = new Aspose.Pdf.License();
        // license.SetLicense("Aspose.Pdf.lic");

        string inputPath = @"YOUR_DIRECTORY\input.pdf";
        string outputPath = @"YOUR_DIRECTORY\output.pdf";

        using (var document = new Document(inputPath))
        {
            // 1️⃣ Get first page and its resources
            var page = document.Pages[1];
            var resourcesEditor = new DictionaryEditor(page.Resources);

            // 2️⃣ Access (or create) ExtGState dictionary
            var extGState = resourcesEditor["ExtGState"].ToCosPdfDictionary();

            // 3️⃣ Build new graphics state
            var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(document);
            var parameters = new[]
            {
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),   // Stroke opacity
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // Fill opacity
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // Blend mode
            };
            foreach (var p in parameters) newGraphicsState.Add(p);

            // 4️⃣ Register the state with a name (GS0)
            extGState.Add("


## O que você deve aprender a seguir?


Os tutoriais a seguir abordam tópicos intimamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Create custom graphics state in PDF using Aspose.Pdf](/pdf/english/net/programming-with-operators/create-custom-graphics-state-in-pdf-using-aspose-pdf/)
- [Add graphics state to PDF using Aspose.PDF for .NET (C#)](/pdf/english/net/programming-with-operators/how-to-add-graphics-state-pdf-using-aspose-pdf-in-c/)
- [How to create empty graphics state in a PDF with C#](/pdf/english/net/programming-with-operators/how-to-create-empty-graphics-state-in-a-pdf-with-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}