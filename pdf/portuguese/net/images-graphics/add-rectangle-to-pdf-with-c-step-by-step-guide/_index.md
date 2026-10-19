---
category: general
date: 2026-08-04
description: Adicionar retângulo ao PDF usando C#. Aprenda a desenhar formas em PDF
  C# com Aspose.Pdf em um exemplo claro e completo.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add rectangle to pdf
- how to draw shape in pdf c#
language: pt
lastmod: 2026-08-04
og_description: Adicionar retângulo ao PDF usando C#. Este tutorial mostra como desenhar
  formas no PDF C# de forma rápida e confiável.
og_image_alt: Screenshot of a PDF page with a blue rectangle drawn by C# code
og_title: Adicionar retângulo ao PDF com C# – guia completo de programação
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Add rectangle to PDF using C#. Learn how to draw shape in PDF C# with
    Aspose.Pdf in a clear, complete example.
  headline: Add rectangle to PDF with C# – step‑by‑step guide
  type: TechArticle
- description: Add rectangle to PDF using C#. Learn how to draw shape in PDF C# with
    Aspose.Pdf in a clear, complete example.
  name: Add rectangle to PDF with C# – step‑by‑step guide
  steps:
  - name: '**Create a new console project**'
    text: '**Create a new console project**'
  - name: '**Add the Aspose.Pdf package**'
    text: '**Add the Aspose.Pdf package**'
  - name: '**Place `input.pdf`** in the project directory (or any folder you reference
      later).'
    text: '**Place `input.pdf`** in the project directory (or any folder you reference
      later).'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Adicionar retângulo ao PDF com C# – guia passo a passo
url: /pt/net/images-graphics/add-rectangle-to-pdf-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Adicionar retângulo a PDF com C# – guia passo a passo

Se você precisa **adicionar retângulo a PDF** a partir de uma aplicação C#, este guia mostra exatamente como fazer isso. Você verá um exemplo completo e executável que desenha uma forma em PDF C# usando a biblioteca Aspose.Pdf, e entenderá por que cada linha de código é importante.

Desenhar formas em PDFs é uma necessidade comum para geradores de relatórios, modelos de faturas e personalização de documentos. Ao final deste tutorial você poderá inserir qualquer anotação retangular, alterar seu tamanho, cor ou posição e salvar o documento modificado sem perder o conteúdo existente.

**O que você aprenderá**

* Como carregar um PDF existente com Aspose.Pdf.
* Como definir os limites do retângulo e criar uma forma retangular.
* Como adicionar o retângulo à coleção de parágrafos de uma página.
* Como salvar o PDF atualizado e verificar o resultado.
* Variações para múltiplas páginas, transparência e estilos de linha personalizados.

**Pré‑requisitos**

* .NET 6.0 ou superior (o código também funciona com .NET Framework 4.7+).
* Visual Studio 2022 ou qualquer IDE C#.
* Uma referência NuGet ao `Aspose.Pdf` (versão de avaliação ou licenciada).
* Um arquivo PDF de entrada chamado `input.pdf` colocado em uma pasta que você controla.

---

## Como desenhar forma em PDF C# – configure o projeto

1. **Crie um novo projeto de console**  

   ```bash
   dotnet new console -n PdfRectangleDemo
   cd PdfRectangleDemo
   ```

2. **Adicione o pacote Aspose.Pdf**  

   ```bash
   dotnet add package Aspose.Pdf
   ```

3. **Coloque `input.pdf`** no diretório do projeto (ou em qualquer pasta que você referencie mais tarde).

O projeto está pronto para compilar o código que **adicionará retângulo a PDF**.

---

## Etapa 1: Carregar o documento PDF

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

class Program
{
    static void Main()
    {
        // Load the existing PDF file.
        Document pdfDoc = new Document("input.pdf");
```

*A classe `Document` analisa o arquivo e expõe uma coleção `Pages`. Carregar é a primeira operação necessária antes que qualquer desenho possa ocorrer.*

---

## Etapa 2: Escolher a página de destino

```csharp
        // Get the first page (pages are 1‑based).
        Page firstPage = pdfDoc.Pages[1];
```

*Se precisar adicionar o retângulo a uma página diferente, substitua o índice pelo número da página desejada. A biblioteca lança uma exceção quando o índice está fora do intervalo, portanto, garanta que o PDF contenha páginas suficientes.*

---

## Etapa 3: Definir os limites do retângulo

```csharp
        // Define the rectangle's position and size (points).
        // (left, bottom, right, top) – origin is bottom‑left.
        Rectangle bounds = new Rectangle(50, 700, 300, 800);
```

*O sistema de coordenadas usa pontos (1 pt = 1/72 polegada). O exemplo cria um retângulo de 250 pt de largura por 100 pt de altura próximo ao topo da página. Ajuste os números para se adequar ao seu layout.*

---

## Etapa 4: Criar a forma retangular

```csharp
        // Create a rectangle shape with the defined bounds.
        Rectangle rectangleShape = new Rectangle(bounds)
        {
            // Optional styling – a semi‑transparent blue fill.
            FillColor = Color.FromRgb(0, 120, 215),
            FillOpacity = 0.4,

            // Optional border – 2 pt thick, dark gray.
            Border = new Border
            {
                Width = 2,
                Color = Color.FromRgb(50, 50, 50)
            }
        };
```

*A classe `Rectangle` herda de `GraphicalObject`. Definir `FillColor` e `Border` é opcional, mas demonstra como controlar a aparência ao **desenhar forma em PDF C#** além de um contorno simples.*

---

## Etapa 5: Adicionar o retângulo à página

```csharp
        // Add the rectangle shape to the page's paragraph collection.
        firstPage.Paragraphs.Add(rectangleShape);
```

*Parágrafos são o contêiner para qualquer objeto desenhável. Ao inserir a forma em `Paragraphs`, o Aspose.Pdf a renderiza quando o documento é salvo.*

---

## Etapa 6: Salvar o PDF modificado

```csharp
        // Save the updated PDF to a new file.
        pdfDoc.Save("output.pdf");

        // Inform the user.
        Console.WriteLine("Rectangle added and saved to output.pdf");
    }
}
```

*Salvar cria um novo arquivo para que o `input.pdf` original permaneça inalterado. Você pode sobrescrever o arquivo de origem passando o mesmo caminho, mas manter um backup é uma prática recomendada.*

---

## Código-fonte completo (executável)

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using System.Drawing;   // For Color struct

class Program
{
    static void Main()
    {
        // Step 1: Load the PDF document
        Document pdfDoc = new Document("input.pdf");

        // Step 2: Get the first page (pages are 1‑based)
        Page firstPage = pdfDoc.Pages[1];

        // Step 3: Define rectangle bounds (left, bottom, right, top)
        Rectangle bounds = new Rectangle(50, 700, 300, 800);

        // Step 4: Create a rectangle shape with optional styling
        Rectangle rectangleShape = new Rectangle(bounds)
        {
            FillColor = Color.FromArgb(102, 0, 120, 215), // 40 % opacity blue
            FillOpacity = 0.4,
            Border = new Border
            {
                Width = 2,
                Color = Color.FromRgb(50, 50, 50)
            }
        };

        // Step 5: Add the rectangle shape to the page
        firstPage.Paragraphs.Add(rectangleShape);

        // Step 6: Save the modified PDF
        pdfDoc.Save("output.pdf");

        Console.WriteLine("Rectangle added to PDF successfully.");
    }
}
```

**Saída esperada** – Abra `output.pdf` em qualquer visualizador de PDF. Você deverá ver um retângulo preenchido de azul próximo ao canto superior direito da primeira página, contornado por uma borda cinza escura.

---

## Como desenhar forma em PDF C# em múltiplas páginas

Se precisar **adicionar retângulo a PDF** em todas as páginas, percorra a coleção `Pages`:

```csharp
foreach (Page page in pdfDoc.Pages)
{
    Rectangle rect = new Rectangle(50, 700, 300, 800);
    Rectangle shape = new Rectangle(rect)
    {
        FillColor = Color.FromArgb(80, 255, 0, 0), // semi‑transparent red
        Border = new Border { Width = 1, Color = Color.Black }
    };
    page.Paragraphs.Add(shape);
}
```

*Esse padrão reutiliza os mesmos limites em cada página. Ajuste as coordenadas por página se precisar de posições diferentes.*

---

## Armadilhas comuns e dicas de boas práticas

| Problema | Por que acontece | Solução |
|----------|------------------|---------|
| Retângulo aparece fora da página | As coordenadas são medidas a partir do canto inferior esquerdo; usar um sistema de coordenadas orientado ao topo pode causar confusão. | Lembre que o eixo Y cresce para cima. Use valores que caibam dentro do tamanho da página (`page.PageInfo.Width`, `page.PageInfo.Height`). |
| Forma está invisível | Opacidade de preenchimento definida como `0` ou largura da borda definida como `0`. | Garanta que `FillOpacity` seja maior que `0` e que `Border.Width` seja pelo menos `0.5`. |
| Salvar lança `AccessDeniedException` | O arquivo de saída está aberto em outro programa. | Feche quaisquer visualizadores antes de executar o código, ou salve em um caminho diferente. |
| Retângulo sobrepõe conteúdo existente | Nenhum controle de camada foi definido. | Use a propriedade `ZIndex` (valores maiores são renderizados acima) se precisar controlar a ordem das camadas. |

---

## Estendendo o retângulo – gradientes, rotação e transparência

O Aspose.Pdf oferece suporte a gráficos avançados. Para criar um retângulo rotacionado com gradiente linear:

```csharp
Rectangle gradientRect = new Rectangle(bounds)
{
    // Gradient fill from left (blue) to right (green)
    FillColor = Color.Blue,
    FillColor2 = Color.Green,
    FillMode = FillMode.LinearGradient,
    // Rotate 45 degrees around the rectangle's center
    Rotation = 45
};
firstPage.Paragraphs.Add(gradientRect);
```

*O mesmo padrão de código demonstra **como desenhar forma em PDF C#** com efeitos visuais mais ricos.*

---

## Verificar o resultado programaticamente

Você pode confirmar que o retângulo foi adicionado verificando a contagem de parágrafos da página:

```csharp
int shapeCount = firstPage.Paragraphs.Count;
Console.WriteLine($"Page 1 now contains {shapeCount} paragraph objects.");
```

Se a contagem aumentou em um após a inserção, a operação foi bem‑sucedida.

---

## Conclusão

Agora você sabe como **adicionar retângulo a PDF** usando C#. O tutorial abordou carregamento de documento, definição de limites, criação da forma retangular, inserção na página e salvamento do resultado. Você também viu como lidar com múltiplas páginas, evitar erros comuns e aplicar estilos avançados.

Em seguida, explore tópicos relacionados como **como desenhar forma em PDF C#** para círculos, polígonos ou caminhos livres, e aprenda a combinar formas com texto e imagens para criar relatórios PDF totalmente funcionais.

Feliz codificação!

## O que você deve aprender a seguir?

Os tutoriais a seguir cobrem tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Como adicionar carimbos de página em PDFs usando Aspose.PDF para .NET | Guia de marcas d'água e fundos](/pdf/english/net/watermarks-backgrounds/implement-page-stamps-aspose-pdf-dotnet/)
- [Como adicionar um carimbo de imagem a um PDF usando Aspose.PDF para .NET: Guia abrangente](/pdf/english/net/images-graphics/add-image-stamp-pdf-aspose-dotnet/)
- [Como adicionar uma marca d'água de imagem rotativa a PDFs usando Aspose.PDF para .NET](/pdf/english/net/watermarks-backgrounds/add-rotating-image-watermark-aspose-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}