---
category: general
date: 2026-09-18
description: Aprenda a criar um dicionário PDF vazio em C# usando Aspose.PDF. Este
  guia passo a passo cobre ExtGState, estado gráfico e manipulação de CosPdfDictionary.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create empty PDF dictionary
- Aspose.PDF
- ExtGState dictionary
- graphics state
- CosPdfDictionary
- PDF manipulation C#
language: pt
lastmod: 2026-09-18
og_description: Crie um dicionário PDF vazio em C# com Aspose.PDF. Siga este tutorial
  abrangente para editar dicionários ExtGState e de estado gráfico.
og_image_alt: Screenshot showing creation of an empty PDF dictionary in C#
og_title: Criar dicionário PDF vazio em C# – guia completo do Aspose.PDF
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: Learn to create empty PDF dictionary in C# using Aspose.PDF. This step‑by‑step
    guide covers ExtGState, graphics state, and CosPdfDictionary manipulation.
  headline: How to create empty PDF dictionary with Aspose.PDF in C#
  type: TechArticle
tags:
- PDF
- C#
- Aspose.PDF
title: Como criar um dicionário PDF vazio com Aspose.PDF em C#
url: /pt/net/programming-with-document/how-to-create-empty-pdf-dictionary-with-aspose-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como criar dicionário PDF vazio com Aspose.PDF em C#

Se você precisa **criar dicionário PDF vazio** ao processar um arquivo PDF, este guia mostra exatamente como fazer isso usando Aspose.PDF para .NET. Seja ajustando transparência, modos de mesclagem ou qualquer estado gráfico personalizado, os passos abaixo permitem editar o dicionário `ExtGState` de forma segura e eficiente.

Neste tutorial você aprenderá a:

* Carregar um documento PDF com Aspose.PDF.
* Acessar os recursos da primeira página e o dicionário `ExtGState` existente.
* Construir um novo `CosPdfDictionary` vazio e preenchê‑lo com entradas de estado gráfico.
* Salvar o PDF modificado sem perder nenhum conteúdo original.

A solução funciona com qualquer PDF que contenha ao menos uma página e requer apenas a biblioteca Aspose.PDF (versão 23.10 ou posterior).

## Pré‑requisitos

* .NET 6.0 ou posterior (o código também funciona no .NET Framework 4.8).
* Uma referência ao pacote NuGet **Aspose.PDF**.
* Um arquivo PDF de entrada localizado em `YOUR_DIRECTORY/input.pdf`.
* Familiaridade básica com C# e conceitos de PDF, como recursos e estado gráfico.

> **Dica profissional:** Ao trabalhar com PDFs grandes, envolva o objeto `Document` em um bloco `using` para garantir que todos os manipuladores de arquivo sejam liberados rapidamente.

## Etapa 1: Carregar o documento PDF

A primeira operação abre o arquivo fonte. Aspose.PDF lê todo o documento na memória, permitindo que você edite objetos internos.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Step 1: Load the PDF document
using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
{
    // Subsequent steps go here
}
```

*Por que isso importa*: Carregar o documento cria um modelo de objeto mutável. Sem essa etapa você não consegue acessar os recursos da página necessários para manipular o dicionário.

## Etapa 2: Recuperar os recursos da primeira página

Cada página armazena um dicionário `Resources` que contém fontes, imagens e estados gráficos. Acessá‑lo fornece um `DictionaryEditor` que simplifica as operações de leitura/escrita.

```csharp
// Step 2: Get the resources of the first page
Page firstPage = pdfDocument.Pages[1];
DictionaryEditor resourcesEditor = new DictionaryEditor(firstPage.Resources);
```

*Por que isso importa*: O dicionário `ExtGState` está dentro dos recursos da página. Editar o dicionário errado não teria efeito na renderização.

## Etapa 3: Localizar o dicionário ExtGState existente

A entrada `ExtGState` pode já conter objetos de estado gráfico. Nós a recuperamos como um `CosPdfDictionary` para que possamos adicionar novas entradas.

```csharp
// Step 3: Access the existing ExtGState dictionary
CosPdfDictionary extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
```

Se a entrada `ExtGState` não existir, o Aspose.PDF cria automaticamente um dicionário vazio quando você atribuir um novo mais tarde.

## Etapa 4: **Criar dicionário PDF vazio** para um novo estado gráfico

Aqui construímos um `CosPdfDictionary` totalmente novo — o núcleo da operação **criar dicionário PDF vazio**. Em seguida, preenchemos com chaves padrão de estado gráfico:

* `CA` – opacidade do traço.
* `ca` – opacidade do preenchimento.
* `BM` – modo de mesclagem.

```csharp
// Step 4: Create a new graphics state dictionary and define its entries
CosPdfDictionary graphicsStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

KeyValuePair<string, ICosPdfPrimitive>[] graphicsStateEntries = new[]
{
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),          // Stroke opacity
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),       // Fill opacity
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))    // Blend mode
};

foreach (var entry in graphicsStateEntries)
    graphicsStateDict.Add(entry);
```

*Por que isso importa*: Ao definir explicitamente cada entrada, você controla como os objetos na página se mesclam e são renderizados. O dicionário está **vazio** até que você adicione essas chaves, atendendo ao requisito de **criar dicionário PDF vazio** antes de preenchê‑lo.

## Etapa 5: Adicionar o novo estado gráfico ao dicionário ExtGState

Todo estado gráfico deve ter um nome único (por exemplo, `GS0`). Inserimos o dicionário recém‑criado sob esse nome.

```csharp
// Step 5: Add the new graphics state to the ExtGState dictionary with a unique name
extGStateDict.Add("GS0", graphicsStateDict);
```

Se precisar de múltiplos estados, continue adicionando entradas como `GS1`, `GS2`, etc., garantindo que cada nome seja único dentro do dicionário `ExtGState`.

## Etapa 6: Salvar o documento PDF atualizado

Por fim, gravamos as alterações de volta ao disco. O arquivo original permanece intacto porque salvamos em um novo caminho.

```csharp
// Step 6: Save the updated PDF document
pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
}
```

O `output.pdf` resultante agora contém um estado gráfico adicional (`GS0`) que pode ser referenciado a partir de qualquer fluxo de conteúdo de página usando o operador `/GS0`.

## Exemplo completo em funcionamento

Juntando todas as etapas, obtém‑se um programa autocontido que pode ser executado imediatamente.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;

class Program
{
    static void Main()
    {
        // Load the source PDF
        using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
        {
            // Access first page resources
            Page firstPage = pdfDocument.Pages[1];
            DictionaryEditor resourcesEditor = new DictionaryEditor(firstPage.Resources);

            // Get (or create) ExtGState dictionary
            CosPdfDictionary extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();

            // Build a new empty PDF dictionary for graphics state
            CosPdfDictionary graphicsStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            var entries = new[]
            {
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
            };
            foreach (var entry in entries)
                graphicsStateDict.Add(entry);

            // Insert the new graphics state with a unique name
            extGStateDict.Add("GS0", graphicsStateDict);

            // Save the modified document
            pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
        }

        Console.WriteLine("PDF updated successfully.");
    }
}
```

**Saída esperada**: Após executar o programa, `output.pdf` contém o mesmo conteúdo visual de `input.pdf`. Inspecionando o PDF com uma ferramenta como Adobe Acrobat ou PDF‑Tron, você verá uma nova entrada `GS0` dentro do dicionário `ExtGState` da primeira página.

## Variações comuns e casos de borda

| Situação | O que ajustar |
|-----------|----------------|
| **Nenhuma entrada ExtGState existente** | Substitua `resourcesEditor["ExtGState"]` por `new CosPdfDictionary(pdfDocument)` e atribua de volta a `firstPage.Resources["ExtGState"]`. |
| **Múltiplas páginas precisam do mesmo estado** | Adicione a mesma entrada `GS0` ao `ExtGState` de cada página, ou referencie o dicionário a partir de um objeto de recurso compartilhado. |
| **Modo de mesclagem diferente** | Altere o valor de `CosPdfName` de `"Normal"` para `"Multiply"`, `"Screen"`, etc., conforme o efeito desejado. |
| **Valores de opacidade mais altos** | Use `new CosPdfNumber(0.8)` para `ca` ou `CA` para aumentar a opacidade de preenchimento ou traço. |
| **Usando um operador de fluxo** | No fluxo de conteúdo, escreva `"/GS0 gs"` antes das operações de desenho para aplicar o novo estado gráfico. |

## Considerações de desempenho

* **Uso de memória** – Carregar um PDF muito grande consome memória proporcional ao número de páginas. Se você precisar editar apenas a primeira página, considere usar `pdfDocument.Pages.Delete(pageNumber)` após o processamento para liberar recursos.
* **Segurança de thread** – Objetos Aspose.PDF não são seguros para uso simultâneo em múltiplas threads. Execute edições de dicionário em uma única thread ou crie instâncias `Document` separadas por thread.

## Conclusão

Agora você sabe como **criar dicionário PDF vazio** com Aspose.PDF, preenchê‑lo com entradas de estado gráfico e anexá‑lo ao dicionário `ExtGState` de uma página. Essa técnica permite controle granular sobre opacidade, modo de mesclagem e outros parâmetros de renderização diretamente a partir de C#.

Em seguida, explore tópicos relacionados como **manipulação de PDF C#**, adicionando entradas personalizadas ao **dicionário ExtGState** para efeitos avançados de transparência, ou usando **CosPdfDictionary** para modificar outros tipos de recurso como fontes ou XObjects. Experimente múltiplos estados gráficos para criar efeitos visuais sofisticados em seus PDFs.

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas em seus próprios projetos.

- [Create & Fill Rectangles in PDFs Using Aspose.PDF for .NET&#58; A Step-by-Step Guide](/pdf/english/net/images-graphics/create-fill-rectangle-aspose-pdf-net/)
- [How to Create Dashed Lines in PDFs Using Aspose.PDF for .NET&#58; A Step-by-Step Guide](/pdf/english/net/images-graphics/create-dashed-lines-aspose-pdf-net/)
- [How to Add an Empty Page at the End of a PDF Using Aspose.PDF for .NET | Step-by-Step Guide](/pdf/english/net/document-manipulation/add-empty-page-end-pdf-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}