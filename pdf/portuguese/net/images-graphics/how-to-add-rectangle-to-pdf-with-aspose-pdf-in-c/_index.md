---
category: general
date: 2026-10-10
description: Aprenda como adicionar um retângulo a um PDF, desenhar formas em um PDF
  e salvar o PDF modificado usando Aspose.PDF. Inclui um guia passo a passo para acessar
  uma página específica do PDF.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add rectangle to PDF
- draw shape on PDF
- save modified PDF
- add shape to PDF
- access specific PDF page
language: pt
lastmod: 2026-10-10
og_description: Adicionar retângulo ao PDF usando Aspose.PDF em C#. Este tutorial
  mostra como desenhar formas no PDF, acessar uma página específica do PDF e salvar
  o PDF modificado.
og_image_alt: Screenshot of a PDF page with a blue rectangle overlay created by Aspose.PDF
og_title: Adicionar retângulo ao PDF com Aspose.PDF – guia completo em C#
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Learn how to add rectangle to PDF, draw shape on PDF, and save modified
    PDF using Aspose.PDF. Includes step‑by‑step guide to access specific PDF page.
  headline: How to add rectangle to PDF with Aspose.PDF in C#
  type: TechArticle
- description: Learn how to add rectangle to PDF, draw shape on PDF, and save modified
    PDF using Aspose.PDF. Includes step‑by‑step guide to access specific PDF page.
  name: How to add rectangle to PDF with Aspose.PDF in C#
  steps:
  - name: Expected output
    text: 'Running the program prints:'
  - name: What if the PDF has only one page?
    text: Attempting to access `pdfDocument.Pages[1]` throws an `ArgumentOutOfRangeException`.
      Guard against this by checking `pdfDocument.Pages.Count` before indexing.
  - name: How to add multiple rectangles on different pages?
    text: Repeat Steps 2‑4 for each target page, adjusting the rectangle’s coordinates
      as needed. You can place the logic inside a loop that iterates over `pdfDocument.Pages`.
  - name: Can I use other shapes such as circles or polygons?
    text: Yes. Aspose.PDF provides `Ellipse`, `Polygon`, and `Polyline` classes that
      follow the same pattern as `Rectangle`. Replace the `new Aspose.Pdf.Drawing.Rectangle`
      call with the desired shape class.
  - name: Does the library support PDFs with rotated pages?
    text: Aspose.PDF automatically respects page rotation when rendering shapes. The
      rectangle’s coordinates are interpreted in the page’s native coordinate system,
      so no extra transformation is required.
  type: HowTo
tags:
- Aspose.PDF
- C#
- PDF manipulation
title: Como adicionar um retângulo ao PDF com Aspose.PDF em C#
url: /pt/net/images-graphics/how-to-add-rectangle-to-pdf-with-aspose-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como adicionar um retângulo a um PDF com Aspose.PDF em C#

Se você precisa **adicionar retângulo a PDF** programaticamente, este guia mostra exatamente como fazer. Você aprenderá a **desenhar forma em PDF**, direcionar uma página específica e **salvar PDF modificado** sem erros.

Trabalhar com documentos PDF é uma necessidade comum para relatórios, faturamento ou anotação de documentos. Ao final deste tutorial, você poderá **adicionar forma a PDF** com confiança, lidar com erros de fora dos limites e integrar a solução em qualquer projeto .NET.

## Pré-requisitos

Antes de começar, certifique‑se de que você tem:

* .NET 6.0 SDK ou posterior instalado  
* Visual Studio 2022 (ou qualquer IDE C#)  
* Uma licença Aspose.PDF for .NET ou uma chave de avaliação gratuita – a API funciona da mesma forma em ambos os modos  
* Um arquivo PDF chamado `input.pdf` colocado em uma pasta que você possa referenciar a partir do seu código  

Estes itens são as únicas dependências externas para o exemplo.

## Etapa 1: Instalar o pacote NuGet Aspose.PDF

A biblioteca Aspose.PDF fornece as classes `Document`, `Rectangle` e outras classes de desenho que você precisa.

```bash
dotnet add package Aspose.PDF
```

Executar este comando adiciona a versão estável mais recente do Aspose.PDF ao seu projeto, tornando as classes PDF disponíveis para compilação.

## Etapa 2: Carregar o documento PDF

A primeira operação é carregar o arquivo fonte. Isso cria uma representação em memória que você pode modificar.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using System;

class PdfRectangleExample
{
    static void Main()
    {
        // Load the PDF document from disk
        var pdfDocument = new Document(@"YOUR_DIRECTORY\input.pdf");
```

*Por que isso importa*: Carregar o documento lhe dá acesso à sua coleção de páginas, que é necessária para **acessar página PDF específica** mais tarde.

## Etapa 3: Acessar a segunda página (índice baseado em zero)

As páginas PDF são indexadas a partir de `0`. Para colocar um retângulo na segunda página, recupere a página no índice `1`.

```csharp
        // Access the second page (pages are zero‑based)
        var page = pdfDocument.Pages[1];
```

Se o documento tiver menos de duas páginas, será lançada uma `ArgumentOutOfRangeException`, alertando sobre a necessidade de uma cláusula de proteção no código de produção.

## Etapa 4: Criar a forma retângulo

Defina a posição e o tamanho do retângulo usando a estrutura `Rectangle`, depois envolva‑a em um objeto de desenho Aspose.

```csharp
        // Define rectangle bounds: (x, y, width, height)
        var rectangleBounds = new Rectangle(100, 100, 300, 200);
        var rectangleShape = new Aspose.Pdf.Drawing.Rectangle(rectangleBounds)
        {
            // Optional visual styling
            Border = new BorderInfo(BorderSide.All, 2f, Color.Blue),
            FillColor = Color.FromArgb(30, 0, 0, 255) // semi‑transparent blue
        };
```

*Por que isso importa*: As propriedades `BorderInfo` e `FillColor` permitem que você **desenhe forma em PDF** com um contorno visível e preenchimento opcional, fazendo o retângulo se destacar para os leitores.

## Etapa 5: Adicionar o retângulo à coleção de parágrafos da página

Aspose.PDF trata objetos de desenho como elementos de parágrafo. Adicionar o retângulo à coleção `Paragraphs` da página o renderiza na página.

```csharp
        // Add the rectangle shape to the page
        page.Paragraphs.Add(rectangleShape);
```

Neste ponto, o documento PDF em memória contém a nova forma, mas o arquivo no disco permanece inalterado até que você o salve.

## Etapa 6: Salvar o PDF modificado e tratar erros de fora dos limites

Chamar `Save` grava o documento atualizado em um novo arquivo. Se o retângulo exceder as dimensões da página, o Aspose lança uma `PdfException`. Capturar essa exceção permite que você reporte o problema de forma limpa.

```csharp
        try
        {
            // Save the altered PDF to a new file
            pdfDocument.Save(@"YOUR_DIRECTORY\output.pdf");
            Console.WriteLine("PDF saved successfully with rectangle added.");
        }
        catch (Aspose.Pdf.Exceptions.PdfException ex)
        {
            // Handle shape that does not fit on the page
            Console.WriteLine($"Shape out of bounds: {ex.Message}");
        }
    }
}
```

*Por que isso importa*: O bloco `try/catch` garante que sua aplicação **salve PDF modificado** com segurança, e a mensagem de erro ajuda a ajustar as coordenadas do retângulo, se necessário.

## Exemplo completo em funcionamento

Juntando todas as etapas, aqui está o programa completo, pronto para ser executado:

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using System;
using System.Drawing; // Required for Color

class PdfRectangleExample
{
    static void Main()
    {
        // Step 1: Load the PDF document
        var pdfDocument = new Document(@"YOUR_DIRECTORY\input.pdf");

        // Step 2: Access the second page (zero‑based)
        var page = pdfDocument.Pages[1];

        // Step 3: Create a rectangle shape positioned at (100,100) with width 300 and height 200
        var rectangleBounds = new Rectangle(100, 100, 300, 200);
        var rectangleShape = new Aspose.Pdf.Drawing.Rectangle(rectangleBounds)
        {
            Border = new BorderInfo(BorderSide.All, 2f, Color.Blue),
            FillColor = Color.FromArgb(30, 0, 0, 255) // semi‑transparent blue
        };

        // Step 4: Add the rectangle shape to the page's paragraph collection
        page.Paragraphs.Add(rectangleShape);

        // Step 5: Save the modified PDF, handling out‑of‑bounds cases
        try
        {
            pdfDocument.Save(@"YOUR_DIRECTORY\output.pdf");
            Console.WriteLine("PDF saved successfully with rectangle added.");
        }
        catch (Aspose.Pdf.Exceptions.PdfException ex)
        {
            Console.WriteLine($"Shape out of bounds: {ex.Message}");
        }
    }
}
```

### Saída esperada

Executar o programa exibe:

```
PDF saved successfully with rectangle added.
```

e cria `output.pdf` que mostra o conteúdo original mais um retângulo azul nas coordenadas especificadas na segunda página.

Se o retângulo fosse maior que a página, você veria:

```
Shape out of bounds: The shape exceeds page margins.
```

## Perguntas comuns e casos de borda

### E se o PDF tiver apenas uma página?

Tentar acessar `pdfDocument.Pages[1]` lança uma `ArgumentOutOfRangeException`. Proteja-se verificando `pdfDocument.Pages.Count` antes de indexar.

```csharp
if (pdfDocument.Pages.Count < 2)
{
    Console.WriteLine("Document does not contain a second page.");
    return;
}
```

### Como adicionar múltiplos retângulos em páginas diferentes?

Repita as Etapas 2‑4 para cada página alvo, ajustando as coordenadas do retângulo conforme necessário. Você pode colocar a lógica dentro de um loop que itere sobre `pdfDocument.Pages`.

### Posso usar outras formas, como círculos ou polígonos?

Sim. Aspose.PDF fornece as classes `Ellipse`, `Polygon` e `Polyline` que seguem o mesmo padrão de `Rectangle`. Substitua a chamada `new Aspose.Pdf.Drawing.Rectangle` pela classe de forma desejada.

### A biblioteca suporta PDFs com páginas rotacionadas?

Aspose.PDF respeita automaticamente a rotação da página ao renderizar formas. As coordenadas do retângulo são interpretadas no sistema de coordenadas nativo da página, portanto nenhuma transformação extra é necessária.

## Considerações de desempenho

* **Uso de memória** – Carregar um PDF grande (centenas de megabytes) consome memória proporcional. Se você precisar modificar apenas uma página, considere usar `PdfFileInfo` para extrair essa página, modificá‑la e depois mesclá‑la novamente.
* **Processamento em lote** – Ao adicionar formas a muitos documentos, reutilize uma única instância `License` para evitar a sobrecarga de validação de licença repetida.

## Próximos passos

Agora que você pode **adicionar retângulo a PDF**, explore os tópicos relacionados:

* **draw shape on PDF** – aprenda a sobrepor texto, imagens e marcas d’água  
* **add shape to PDF** – combine múltiplas formas em uma única camada de anotação  
* **save modified PDF** – use streams (`MemoryStream`) para retornar PDFs diretamente de APIs web  
* **access specific PDF page** – implemente extração de intervalo de páginas para relatórios personalizados  

Experimente diferentes cores, estilos de linha e níveis de transparência para adequar às diretrizes de sua marca.

---

*Feliz codificação! Se este tutorial ajudou você a **adicionar retângulo a PDF**, considere compartilhá‑lo com colegas ou contribuir com melhorias para a comunidade.*

## O que você deve aprender a seguir?

Os tutoriais a seguir cobrem tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas de implementação em seus próprios projetos.

- [How to Add Shape to PDF with Aspose.PDF in C# – Step‑by‑Step Guide](/pdf/english/net/images-graphics/how-to-add-shape-to-pdf-with-aspose-pdf-in-c-step-by-step-gu/)
- [How to Add a Line Object in PDF Using Aspose.PDF for .NET&#58; A Step-by-Step Guide](/pdf/english/net/document-manipulation/add-line-aspose-pdf-dotnet-tutorial/)
- [How to Create PDF in C# – Add Page, Draw Rectangle & Save](/pdf/english/net/document-creation/how-to-create-pdf-in-c-add-page-draw-rectangle-save/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}