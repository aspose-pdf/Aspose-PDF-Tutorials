---
category: general
date: 2026-09-05
description: Crie um documento PDF em C# adicionando uma página em branco, desenhando
  um retângulo e salvando o arquivo PDF. Siga um exemplo passo a passo do Aspose.PDF.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create pdf document
- add blank page pdf
- draw rectangle pdf
- save pdf file
- how to add rectangle
language: pt
lastmod: 2026-09-05
og_description: Crie um documento PDF em C# adicionando uma página em branco, desenhando
  um retângulo e salvando o arquivo PDF. Siga este exemplo completo com Aspose.PDF.
og_image_alt: Screenshot showing a PDF document with a drawn rectangle on a blank
  page
og_title: Criar documento PDF com página em branco e retângulo – guia C#
schemas:
- author: Aspose
  dateModified: '2026-09-05'
  description: Create PDF document in C# by adding a blank page, drawing a rectangle,
    and saving the PDF file. Follow a step‑by‑step Aspose.PDF example.
  headline: How to create PDF document with a blank page and rectangle
  type: TechArticle
- description: Create PDF document in C# by adding a blank page, drawing a rectangle,
    and saving the PDF file. Follow a step‑by‑step Aspose.PDF example.
  name: How to create PDF document with a blank page and rectangle
  steps:
  - name: 'Edge case: custom page size'
    text: 'If your layout requires a 6 × 9 inch page, replace the default call with:'
  - name: 'Pro tip: styling the rectangle'
    text: 'You can change the stroke color and line width:'
  - name: 'Edge case: overwriting existing files'
    text: 'Aspose.PDF overwrites an existing file by default. To protect previous
      outputs, check for file existence first:'
  - name: Expected output
    text: Running the program creates a single‑page PDF. When you open `output.pdf`
      you will see a blank white page with a red rectangle positioned 100 points from
      the left and bottom edges, measuring 200 × 200 points.
  type: HowTo
tags:
- PDF
- C#
- Aspose.PDF
- PDF generation
title: Como criar um documento PDF com uma página em branco e um retângulo
url: /pt/net/document-creation/how-to-create-pdf-document-with-a-blank-page-and-rectangle/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como criar documento PDF com uma página em branco e retângulo

Se você precisar **criar documento PDF** programaticamente, este guia mostra uma solução completa em C#. Você aprenderá como adicionar uma página em branco, desenhar um retângulo nessa página e, finalmente, salvar o arquivo PDF. O exemplo usa a biblioteca Aspose.PDF, que funciona com .NET 6+ e .NET Framework 4.5+.

Adicionar uma página em branco e desenhar formas é uma necessidade comum para faturas, certificados ou relatórios personalizados. Ao final deste tutorial você terá um projeto executável que produz um PDF contendo um único retângulo posicionado em (100, 100) com tamanho de 200 × 200 pontos.

## Pré-requisitos

* Visual Studio 2022 (ou qualquer IDE C#)
* .NET 6 SDK ou .NET Framework 4.5+
* Pacote NuGet Aspose.PDF para .NET  
  ```bash
  dotnet add package Aspose.PDF
  ```
* Permissão de gravação no diretório de saída

Nenhuma configuração adicional é necessária; o código funciona pronto para uso.

## Criar documento PDF – visão geral

Todo o processo consiste em quatro etapas lógicas:

1. **Instantiate** um objeto `Document` – isso representa o arquivo PDF.
2. **Add a blank page** – a página fornece uma tela para desenho.
3. **Draw a rectangle** – um objeto `Path` define a forma.
4. **Save the PDF file** – persiste o documento no disco.

Cada etapa está isolada em sua própria seção, permitindo reutilizar ou substituir partes conforme necessário.

![Diagram of a PDF with a rectangle on a blank page](https://example.com/placeholder-image.png){.img-fluid alt="Captura de tela mostrando um documento PDF com um retângulo desenhado em uma página em branco"}

## Adicionar página em branco pdf

Um PDF deve conter ao menos uma página antes que quaisquer gráficos possam ser inseridos. O método `Pages.Add()` cria uma página vazia com dimensões padrão (A4). Se você precisar de um tamanho diferente, passe um argumento `PageSize`.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

// Step 1: Create a new PDF document
using var pdfDocument = new Document();

// Step 2: Add a blank page to the document
Page pdfPage = pdfDocument.Pages.Add();   // adds an A4 page by default
```

*Por que esta etapa importa* – O objeto página contém coleções para texto, imagens e gráficos vetoriais. Sem uma página, qualquer tentativa de adicionar um retângulo geraria uma exceção.

### Caso de borda: tamanho de página personalizado

Se o seu layout requer uma página de 6 × 9 polegadas, substitua a chamada padrão por:

```csharp
var pageSize = new Size(432, 648); // 72 points per inch
Page pdfPage = pdfDocument.Pages.Add(pageSize);
```

## Desenhar retângulo pdf

Desenhar um retângulo consiste em criar uma geometria `Rectangle` e envolvê-la em um `Path`. A chamada `ValidateBounds()` garante que a forma caiba dentro das margens da página, evitando recorte.

```csharp
// Step 3: Define a rectangle shape (x, y, width, height)
Rectangle shapeRect = new Rectangle(100, 100, 200, 200);

// Step 4: Add the rectangle to the page contents
Path rectanglePath = new Path(shapeRect).ValidateBounds();
pdfPage.Contents.Add(rectanglePath);
```

*Por que esta etapa importa* – O objeto `Path` é a primitiva vetorial de baixo nível usada pelo Aspose.PDF. Ao validar os limites, você evita erros de tempo de execução quando o retângulo ultrapassa os limites da página.

### Dica profissional: estilizando o retângulo

Você pode alterar a cor do traço e a espessura da linha:

```csharp
rectanglePath.GraphInfo = new GraphInfo
{
    StrokeColor = Color.Red,
    LineWidth = 2
};
```

Isso produz um contorno vermelho com espessura de 2 pontos.

## Salvar arquivo pdf

Persistir o documento finaliza o arquivo no disco. O método `Save` aceita um caminho de arquivo ou um stream. Fornecer um caminho absoluto torna a localização explícita, o que é útil para scripts de automação.

```csharp
// Step 5: Save the PDF to a file
string outputPath = Path.Combine(Environment.CurrentDirectory, "output.pdf");
pdfDocument.Save(outputPath);
Console.WriteLine($"PDF saved to {outputPath}");
```

*Por que esta etapa importa* – Salvar é o único ponto em que a representação em memória se torna um arquivo físico. Se você precisar retornar o PDF de uma API web, substitua o caminho do arquivo por um `MemoryStream`.

### Caso de borda: sobrescrever arquivos existentes

O Aspose.PDF sobrescreve um arquivo existente por padrão. Para proteger saídas anteriores, verifique a existência do arquivo primeiro:

```csharp
if (File.Exists(outputPath))
{
    File.Delete(outputPath);
}
pdfDocument.Save(outputPath);
```

## Como adicionar retângulo – melhores práticas

* **Mantenha as coordenadas dentro das margens da página** – use `ValidateBounds()` ou calcule as margens manualmente.
* **Reutilize objetos `GraphInfo`** ao desenhar múltiplas formas; isso reduz a alocação de memória.
* **Descarte o objeto `Document`** (como mostrado com `using var`) para liberar recursos nativos prontamente.
* **Teste com diferentes configurações de DPI** se você later incorporar imagens raster; formas vetoriais como retângulos permanecem nítidas em qualquer resolução.

## Exemplo completo em funcionamento

Abaixo está o programa completo que você pode copiar para uma aplicação console. Ele compila sem modificações e produz `output.pdf` na pasta do projeto.

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using Aspose.Pdf.Color;

class Program
{
    static void Main()
    {
        // Create a new PDF document
        using var pdfDocument = new Document();

        // Add a blank page to the document
        Page pdfPage = pdfDocument.Pages.Add();

        // Define a rectangle shape (x, y, width, height)
        Rectangle shapeRect = new Rectangle(100, 100, 200, 200);

        // Create a path for the rectangle and validate its bounds
        Path rectanglePath = new Path(shapeRect).ValidateBounds();

        // Optional: style the rectangle (red outline, 2‑pt width)
        rectanglePath.GraphInfo = new GraphInfo
        {
            StrokeColor = Color.Red,
            LineWidth = 2
        };

        // Add the rectangle to the page contents
        pdfPage.Contents.Add(rectanglePath);

        // Determine output path
        string outputPath = Path.Combine(Environment.CurrentDirectory, "output.pdf");

        // Ensure no leftover file blocks the save operation
        if (File.Exists(outputPath))
        {
            File.Delete(outputPath);
        }

        // Save the PDF to a file
        pdfDocument.Save(outputPath);
        Console.WriteLine($"PDF saved to {outputPath}");
    }
}
```

### Saída esperada

Executar o programa cria um PDF de página única. Quando você abrir `output.pdf` verá uma página branca em branco com um retângulo vermelho posicionado a 100 pontos da borda esquerda e inferior, medindo 200 × 200 pontos.

## Conclusão

Agora você sabe como **criar documento PDF**, **adicionar página em branco pdf**, **desenhar retângulo pdf** e **salvar arquivo pdf** usando Aspose.PDF em C#. O exemplo cobre as chamadas de API essenciais, explica por que cada chamada é necessária e fornece dicas para variações comuns, como tamanhos de página personalizados ou estilização de retângulo.

Em seguida, explore tópicos relacionados como **adicionar texto**, **incorporar imagens** ou **criar relatórios multi‑página**. O mesmo padrão — instanciar um `Document`, manipular páginas, adicionar conteúdo vetorial ou raster, então `Save` — se aplica a todos esses cenários. Sinta-se à vontade para experimentar diferentes formas, cores e layouts de página para atender às necessidades do seu projeto.

## O que você deve aprender a seguir?

Os tutoriais a seguir cobrem tópicos intimamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá-lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Criar documento PDF C# – adicionar página, desenhar retângulo e salvar](/pdf/english/net/document-creation/create-pdf-document-c-add-page-draw-rectangle-save/)
- [Criar documento PDF com Aspose.PDF – Guia passo a passo](/pdf/english/net/document-creation/create-pdf-document-with-aspose-pdf-step-by-step-guide/)
- [Criar documento PDF com Aspose – adicionar página, caixa de texto e formulário](/pdf/english/net/forms-annotations/create-pdf-document-with-aspose-add-page-text-box-and-form/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}