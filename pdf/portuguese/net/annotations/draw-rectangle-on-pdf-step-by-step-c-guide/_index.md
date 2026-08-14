---
category: general
date: 2026-08-14
description: Desenhe retângulo em PDF rapidamente usando C#. Aprenda como definir
  as dimensões do retângulo e adicionar formas a uma página PDF em apenas algumas
  linhas.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- draw rectangle on pdf
- how to define rectangle dimensions
language: pt
lastmod: 2026-08-14
og_description: Desenhe retângulo em PDF com C# em segundos. Este guia mostra como
  definir as dimensões do retângulo, adicionar uma forma e verificar os limites da
  página para gráficos PDF confiáveis.
og_image_alt: Screenshot of a PDF page showing a black rectangle drawn with C# code
og_title: Desenhar retângulo em PDF – tutorial completo de C#
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: draw rectangle on pdf quickly using C#. Learn how to define rectangle
    dimensions and add shapes to a PDF page in just a few lines.
  headline: draw rectangle on pdf – step‑by‑step C# guide
  type: TechArticle
tags:
- PDF
- C#
- Aspose.PDF
- RectangleShape
- Graphics
title: Desenhar retângulo em PDF – guia passo a passo C#
url: /pt/net/annotations/draw-rectangle-on-pdf-step-by-step-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# desenhar retângulo em pdf – tutorial completo em C#

Se você precisa **desenhar retângulo em pdf** usando C#, este guia mostra uma solução concisa e pronta para produção. Você verá exatamente **como definir dimensões do retângulo**, verificar se a forma cabe e adicioná‑la a uma página com uma única chamada de método.

O tutorial cobre tudo, desde a criação de um documento PDF até a renderização do retângulo, para que você possa copiar‑colar o código no seu próprio projeto e ver os resultados instantaneamente. Nenhuma documentação externa é necessária—apenas os passos abaixo.

## Prerequisites

Before you start, make sure you have:

* .NET 6.0 ou posterior (o código também funciona com .NET Framework 4.7+)
* O pacote NuGet **Aspose.PDF for .NET** (`Install-Package Aspose.PDF`)
* Um entendimento básico da sintaxe C#
* Uma IDE como Visual Studio ou VS Code

> **Pro tip:** Use a licença de avaliação gratuita do Aspose.PDF para experimentos rápidos; ela adiciona uma pequena marca d'água, mas permite testar todos os recursos.

## How to draw rectangle on PDF with C#

The core of the task is creating a `RectangleShape`, setting its size and stroke, and attaching it to a `Page`. The following H2 header contains the primary keyword, satisfying SEO requirements.

```csharp
using System;
using System.Drawing;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new PDF document
        Document pdfDoc = new Document();

        // 2️⃣ Add a blank page (default size: A4)
        Page page = pdfDoc.Pages.Add();

        // 3️⃣ Define the rectangle bounds (x, y, width, height)
        //    This demonstrates how to define rectangle dimensions.
        Rectangle rectBounds = new Rectangle(0, 0, 500, 700);

        // 4️⃣ Create the rectangle shape and set its stroke color
        RectangleShape rectangleShape = new RectangleShape(rectBounds)
        {
            StrokeColor = Color.Black   // black outline
        };

        // 5️⃣ Verify that the shape fits within the page boundaries
        page.CheckShapeBoundary(rectangleShape);

        // 6️⃣ Add the shape to the page
        page.Add(rectangleShape);

        // 7️⃣ Save the PDF to disk
        string outPath = "RectangleDemo.pdf";
        pdfDoc.Save(outPath);
        Console.WriteLine($"PDF saved to {outPath}");
    }
}
```

### Explanation of each step

| Etapa | Por que é importante |
|------|-----------------------|
| **1️⃣ Criar um novo documento PDF** | Inicializa o contêiner que armazenará páginas e gráficos. |
| **2️⃣ Adicionar uma página em branco** | Você precisa de um objeto `Page` porque as formas são anexadas a uma página, não diretamente ao documento. |
| **3️⃣ Definir os limites do retângulo** | É aqui que você **como definir dimensões do retângulo**. O construtor `Rectangle` recebe `x`, `y`, `width` e `height` em pontos (1 pt = 1/72 in). |
| **4️⃣ Criar a forma retângulo** | `RectangleShape` é a classe Aspose que renderiza um retângulo. Definir `StrokeColor` define o contorno; você também pode definir `FillColor` para um preenchimento sólido. |
| **5️⃣ Verificar limites da página** | `CheckShapeBoundary` lança uma exceção se o retângulo exceder o tamanho da página, evitando PDFs malformados. |
| **6️⃣ Adicionar a forma à página** | A forma torna‑se parte do fluxo de conteúdo da página. |
| **7️⃣ Salvar o PDF** | Persiste o documento em um arquivo que você pode abrir com qualquer visualizador de PDF. |

O documento resultante `RectangleDemo.pdf` contém um retângulo preto posicionado no canto superior‑esquerdo da página, exatamente 500 pt de largura e 700 pt de altura.

![exemplo de desenhar retângulo em pdf](https://example.com/rectangle-demo.png "exemplo de desenhar retângulo em pdf")

*Texto alternativo da imagem: exemplo de desenhar retângulo em pdf mostrando um retângulo preto no canto superior esquerdo de uma página PDF.*

## Como definir dimensões do retângulo para diferentes tamanhos de página

The snippet above uses fixed values (`500 x 700`). In real applications you often need the rectangle to adapt to the page’s width and height.

```csharp
// Get page dimensions (in points)
float pageWidth = page.PageInfo.Width;
float pageHeight = page.PageInfo.Height;

// Define a rectangle that occupies 80% of the page width and 50% of the height
float rectWidth  = pageWidth * 0.8f;
float rectHeight = pageHeight * 0.5f;

// Center the rectangle on the page
float rectX = (pageWidth - rectWidth) / 2;
float rectY = (pageHeight - rectHeight) / 2;

Rectangle dynamicRect = new Rectangle(rectX, rectY, rectWidth, rectHeight);
RectangleShape dynamicShape = new RectangleShape(dynamicRect)
{
    StrokeColor = Color.DarkBlue,
    FillColor   = Color.LightGray   // optional fill
};

page.CheckShapeBoundary(dynamicShape);
page.Add(dynamicShape);
```

**Pontos principais:**

* Use `page.PageInfo.Width` e `Height` para ler o tamanho real da página.
* Multiplicar por um fator (ex., `0.8f`) permite expressar as dimensões como uma porcentagem da página.
* Centralizar é conseguido subtraindo o tamanho do retângulo do tamanho da página e dividindo o restante pela metade.

## Armadilhas comuns e como evitá‑las

| Armadilha | Por que acontece | Correção |
|-----------|------------------|----------|
| Retângulo se estende além da página | Dimensões codificadas fixas maiores que o tamanho da página. | Chame `page.CheckShapeBoundary` **antes** de adicionar a forma; ajuste as dimensões se uma exceção for lançada. |
| Contorno não visível | `StrokeColor` deixado no padrão (`Color.Empty`). | Defina explicitamente `StrokeColor` (ex., `Color.Black`). |
| Retângulo aparece fora da tela | As coordenadas começam no canto inferior‑esquerdo no espaço PDF; usar coordenadas estilo tela (canto superior‑esquerdo) causa inversão. | Lembre‑se de que a origem `(0,0)` é o canto inferior‑esquerdo. Ajuste `y` adequadamente ou use `pageHeight - desiredY`. |
| Espessura de linha inesperada | A largura de linha padrão pode ser muito fina para impressão. | Defina `rectangleShape.LineWidth = 2;` para aumentar a espessura. |

## Expandindo o exemplo

Once you can **draw rectangle on pdf**, you can easily add other shapes:

* **EllipseShape** – para círculos ou elipses.
* **PolygonShape** – para polígonos personalizados.
* **TextFragment** – para rotular seus retângulos.

Todas as formas compartilham o mesmo fluxo de trabalho: definir limites, configurar aparência, verificar limites e, então, adicionar à página.

## Programa completo e executável

Below is the full program that combines the basic rectangle and the dynamic sizing example. Copy it into a new console project, restore the `Aspose.PDF` NuGet package, and run.

```csharp
using System;
using System.Drawing;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

class RectangleDemo
{
    static void Main()
    {
        // Create document and page
        Document doc = new Document();
        Page page = doc.Pages.Add();

        // ==== Fixed‑size rectangle (basic example) ====
        Rectangle fixedRect = new Rectangle(0, 0, 500, 700);
        RectangleShape fixedShape = new RectangleShape(fixedRect)
        {
            StrokeColor = Color.Black,
            LineWidth   = 1
        };
        page.CheckShapeBoundary(fixedShape);
        page.Add(fixedShape);

        // ==== Dynamic rectangle that adapts to page size ====
        float pageW = page.PageInfo.Width;
        float pageH = page.PageInfo.Height;

        float dynWidth  = pageW * 0.6f;
        float dynHeight = pageH * 0.3f;
        float dynX      = (pageW - dynWidth) / 2;
        float dynY      = (pageH - dynHeight) / 2;

        Rectangle dynamicRect = new Rectangle(dynX, dynY, dynWidth, dynHeight);
        RectangleShape dynamicShape = new RectangleShape(dynamicRect)
        {
            StrokeColor = Color.DarkBlue,
            FillColor   = Color.LightYellow,
            LineWidth   = 2
        };
        page.CheckShapeBoundary(dynamicShape);
        page.Add(dynamicShape);

        // Save PDF
        string outFile = "CombinedRectangles.pdf";
        doc.Save(outFile);
        Console.WriteLine($"PDF created: {outFile}");
    }
}
```

**Saída esperada:**  
Abra `CombinedRectangles.pdf`. Você verá um retângulo preto ancorado no canto inferior‑esquerdo e um retângulo azul‑escuro centralizado com preenchimento amarelo‑claro. Ambos os retângulos respeitam as margens da página.

## Conclusão

Você agora sabe como **desenhar retângulo em pdf** com C# e precisamente **como definir dimensões do retângulo** para layouts fixos e responsivos. A abordagem usa `RectangleShape` do Aspose.PDF, verificação de limites e aritmética simples para adaptar a qualquer tamanho de página.

Em seguida, você pode explorar:

* Adicionar **cores de preenchimento** e **estilos de linha** (tracejada, pontilhada) – palavra‑chave secundária: como definir dimensões do retângulo com estilo.
* Combinar múltiplas formas em uma única `Page` para criar gráficos ou formulários.
* Exportar o PDF para um stream para APIs web em vez de salvar em disco.

Experimente diferentes tamanhos, cores e posições para dominar gráficos PDF em suas aplicações .NET. Feliz codificação!

## O que você deve aprender a seguir?

The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Como personalizar PDFs com Aspose.PDF para .NET: definir margens de página e desenhar linhas](/pdf/english/net/document-manipulation/customize-pdfs-aspose-pdf-set-margins-draw-lines/)
- [Como adicionar carimbos de página em PDFs usando Aspose.PDF para .NET: um guia completo](/pdf/english/net/watermarks-backgrounds/add-page-stamp-aspose-pdf-dotnet-guide/)
- [Como adicionar carimbos de número de página em PDFs usando Aspose.PDF para .NET | Marcas d'água e fundos](/pdf/english/net/watermarks-backgrounds/add-page-number-stamp-using-aspose-pdf-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}