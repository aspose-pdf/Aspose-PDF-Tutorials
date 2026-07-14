---
category: general
date: 2026-07-14
description: Salvar PDF como HTML usando Aspose.Pdf – aprenda como criar um documento
  PDF, adicionar uma forma retangular ao PDF e exportar para HTML limpo sem imagens.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save pdf as html
- how to create pdf document
- add rectangle shape pdf
language: pt
lastmod: 2026-07-14
og_description: Salve PDF como HTML com Aspose.Pdf. Descubra como criar um documento
  PDF, desenhar uma forma de retângulo em PDF e gerar HTML sem imagens em minutos.
og_image_alt: Screenshot of a PDF saved as HTML showing a rectangle shape
og_title: Salvar PDF como HTML – Guia rápido para criar PDF e adicionar forma retangular
schemas:
- author: Aspose
  dateModified: '2026-07-14'
  description: Save PDF as HTML using Aspose.Pdf – learn how to create PDF document,
    add rectangle shape PDF, and export to clean HTML without images.
  headline: Save PDF as HTML – Create PDF, add rectangle shape
  type: TechArticle
tags:
- pdf
- aspnet
- csharp
- html-export
title: Salvar PDF como HTML – Criar PDF, adicionar forma retangular
url: /pt/net/conversion-export/save-pdf-as-html-create-pdf-add-rectangle-shape/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Salvar PDF como HTML – Criar PDF, adicionar forma retangular

Já se perguntou como **salvar PDF como HTML** ainda podendo desenhar gráficos no PDF original? Você não está sozinho. Em muitas ferramentas internas precisamos de uma visualização HTML limpa de um PDF que contém formas personalizadas, e os conversores habituais ou incorporam imagens raster pesadas ou removem completamente os dados vetoriais.  

Neste tutorial vamos percorrer **como criar um documento PDF** programaticamente com Aspose.Pdf, desenhar um **retângulo PDF**, configurar a numeração Bates e, finalmente, **salvar PDF como HTML** omitindo as imagens raster. Ao final você terá um aplicativo console C# totalmente executável que produz um arquivo HTML que pode ser aberto em qualquer navegador—sem arquivos de imagem adicionais.

> **Dica profissional:** Aspose.Pdf funciona com .NET 6+, .NET Framework 4.6+ e até .NET Core, então você pode inseri‑lo em um serviço Windows legado ou em um microserviço totalmente novo.

---

## Pré‑requisitos

- **Visual Studio 2022** (Community ou superior) ou qualquer IDE compatível com C#.  
- **Aspose.Pdf for .NET** pacote NuGet (versão 23.11 ou posterior). Instale‑o via o Console do Gerenciador de Pacotes:

```powershell
Install-Package Aspose.Pdf
```

- Familiaridade básica com a sintaxe C#; não é necessário experiência prévia com PDF.

---

## Salvar PDF como HTML com Aspose.Pdf

Abaixo está o código completo, pronto para copiar e colar. Ele segue exatamente os passos do trecho original, mas adiciona comentários, tratamento de erros e um pequeno método auxiliar para manter o fluxo principal legível.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using Aspose.Pdf.Text;

namespace PdfToHtmlDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create a fresh PDF document.
            Document pdfDoc = new Document();
            Page pdfPage = pdfDoc.Pages.Add();

            // 2️⃣ Draw a rectangle shape on the page.
            //    This demonstrates the "add rectangle shape pdf" requirement.
            var rectangle = new Rectangle(100, 500, 300, 700)
            {
                // Optional visual tweaks
                FillColor = Color.GetYellow(),
                Border = new Border
                {
                    Width = 2,
                    Color = Color.GetRed()
                }
            };
            pdfPage.Paragraphs.Add(rectangle);
            pdfPage.ValidateGraphicsState(); // Ensures the shape fits within page bounds

            // 3️⃣ Configure Bates numbering – useful for legal documents.
            var bates = new BatesNumbering { StartNumber = 1, Prefix = "DOC-" };
            pdfDoc.BatesNumbering = bates;

            // 4️⃣ Add a tagged element with an explicit position.
            //    Tagging is important for accessibility (PDF/UA).
            var taggedElement = new TagStructure();
            taggedElement.PositionSettings = new TagPositionSettings { X = 150, Y = 600 };
            pdfPage.TagStructure.Add(taggedElement);

            // 5️⃣ Enable detection of compromised signatures.
            pdfDoc.SecurityOptions.DetectCompromisedSignatures = true;
            bool hasCompromisedSignature = pdfDoc.SecurityOptions.HasCompromisedSignature;
            Console.WriteLine($"Compromised signature? {hasCompromisedSignature}");

            // 6️⃣ Finally, save the PDF as HTML *without* embedding raster images.
            var htmlOptions = new HtmlSaveOptions
            {
                SkipImages = true,               // Removes <img> tags for raster data
                FixedLayout = true,              // Preserves the original page layout
                ExportEmbeddedFonts = false      // Keeps the HTML lightweight
            };

            string outputPath = @"output.html";
            pdfDoc.Save(outputPath, htmlOptions);
            Console.WriteLine($"✅ PDF successfully saved as HTML at: {outputPath}");
        }
    }
}
```

### O que o código faz, passo a passo

| Etapa | Por que é importante |
|------|----------------------|
| **Criar um documento PDF** | Esta é a base—sem um objeto `Document` você não pode adicionar nada. |
| **Adicionar forma retangular PDF** | Demonstra desenho vetorial; retângulos são a forma mais simples, mas a mesma API suporta círculos, polígonos, etc. |
| **Configurar numeração Bates** | Frequentemente necessária em cenários de litígio ou processamento em lote para identificar páginas de forma única. |
| **Estrutura de tags** | Melhora a acessibilidade; leitores de tela dependem de tags para transmitir a ordem de leitura. |
| **Detectar assinaturas comprometidas** | Aplicativos conscientes de segurança precisam saber se uma assinatura digital foi adulterada. |
| **Salvar PDF como HTML** | O objetivo final—gerar HTML limpo que reflita o layout do PDF sem arquivos de imagem volumosos. |

> **Por que `SkipImages = true`?**  
> Quando você converte um PDF que contém gráficos vetoriais (como nosso retângulo) normalmente não precisa da alternativa raster. Definir `SkipImages` remove os elementos `<img>` que, de outra forma, referenciariam blobs base‑64, mantendo o arquivo HTML com apenas alguns kilobytes.

---

## Como criar documento PDF com Aspose.Pdf

Se você é novo no Aspose, a biblioteca trata um PDF muito parecido com um documento Word: você adiciona **páginas**, depois **parágrafos**, **formas** ou **anotações** a essas páginas. A classe `Document` é o ponto de entrada, e cada `Page` hospeda uma coleção chamada `Paragraphs`. Qualquer coisa que herde de `TextFragmentAbsorber`, `Image`, `Rectangle`, etc., pode ser inserida nessa coleção.

Abaixo está um trecho mínimo que cria apenas um PDF em branco—útil quando você quer começar do zero:

```csharp
Document emptyPdf = new Document();
Page firstPage = emptyPdf.Pages.Add();   // Adds a default‑size A4 page
emptyPdf.Save("empty.pdf");
```

Você pode encadear páginas adicionais com um simples loop `for`, ou aplicar configurações de nível de página (margem, tamanho) via `PageInfo`. Essa flexibilidade é o que torna o Aspose.Pdf um favorito para geração de PDF no lado do servidor.

---

## Adicionar forma retangular PDF – desenhando gráficos

A classe `Rectangle` está em `Aspose.Pdf.Annotations`. Ela aceita quatro coordenadas: **X inferior‑esquerdo**, **Y inferior‑esquerdo**, **X superior‑direito**, **Y superior‑direito**. Pense no sistema de coordenadas do PDF como

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos estreitamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas de implementação em seus próprios projetos.

- [Create PDF Document with Aspose.PDF – Add Page, Shape & Save](/pdf/english/net/document-creation/create-pdf-document-with-aspose-pdf-add-page-shape-save/)
- [Convert PDF to HTML in .NET Using Aspose.PDF Without Saving Images](/pdf/english/net/conversion-export/convert-pdf-html-net-asposepdf-no-images/)
- [PDF to HTML Conversion Using Aspose.PDF .NET&#58; Save Images as External PNGs](/pdf/english/net/conversion-export/pdf-to-html-conversion-external-png-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}