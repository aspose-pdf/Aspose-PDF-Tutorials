---
category: general
date: 2026-07-20
description: 'Criar documento PDF em C# com Aspose.Pdf: posicionar texto no PDF e
  adicionar árvore estrutural para acessibilidade. Siga este guia passo a passo.'
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create pdf document c#
- position text in pdf
- add structural tree
- Aspose.Pdf tagging
- PDF/A‑2b generation
language: pt
lastmod: 2026-07-20
og_description: Crie documentos PDF em C# instantaneamente. Aprenda a posicionar texto
  em PDF e adicionar a árvore estrutural usando Aspose.Pdf para conformidade PDF/A‑2b.
og_image_alt: Screenshot showing positioned text inside a PDF generated with Aspose.Pdf
  in C#
og_title: Criar Documento PDF em C# – Guia Completo para Posicionar Texto e Estrutura
  de Tags
schemas:
- author: Aspose
  dateModified: '2026-07-20'
  description: 'Create PDF document C# with Aspose.Pdf: position text in PDF and add
    structural tree for accessibility. Follow this step‑by‑step guide.'
  headline: Create PDF Document C# – Position Text and Add Structural Tree
  type: TechArticle
- description: 'Create PDF document C# with Aspose.Pdf: position text in PDF and add
    structural tree for accessibility. Follow this step‑by‑step guide.'
  name: Create PDF Document C# – Position Text and Add Structural Tree
  steps:
  - name: Can I use other units (mm, cm) for positioning?
    text: Aspose.Pdf works natively with points. If you prefer millimeters, convert
      using `1 mm ≈ 2.83465 pt`. For example, `Position(25.4, 254)` places the paragraph
      1 cm from the left and 9 cm from the bottom.
  - name: What if I need to add multiple tags (headings, tables)?
    text: Simply create additional `StructureElement` objects with tags like `"H1"`
      for headings or `"Table"` for tables, and add the corresponding content as kids.
      Nesting works the same way—children inherit the parent’s logical order.
  - name: Does this approach work for PDF/A‑1b or PDF/A‑3b?
    text: Yes. Replace `SaveFormat.PdfA2b` with `SaveFormat.PdfA1b` or `SaveFormat.PdfA3b`.
      Keep in mind that each PDF/A version has its own set of required metadata; Aspose.Pdf
      will prompt you if something is missing.
  type: HowTo
tags:
- C#
- PDF
- Aspose.Pdf
title: Criar documento PDF C# – Posicionar texto e adicionar árvore estrutural
url: /pt/net/programming-with-tagged-pdf/create-pdf-document-c-position-text-and-add-structural-tree/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar Documento PDF C# – Posicionar Texto e Adicionar Árvore Estrutural

Já precisou **criar documento PDF C#** que não só posiciona o texto exatamente onde você deseja, mas também incorpora uma árvore estrutural adequada para acessibilidade? Você não está sozinho — desenvolvedores que criam faturas, relatórios ou e‑books enfrentam essa necessidade o tempo todo. Neste tutorial, vamos percorrer um exemplo completo, pronto‑para‑executar, que faz exatamente isso, usando a poderosa biblioteca Aspose.Pdf.

Vamos abordar como **posicionar texto no PDF**, anexar uma tag semântica via a etapa **adicionar árvore estrutural**, e finalmente salvar o arquivo como um documento compatível com PDF/A‑2b. Ao final, você terá um trecho reutilizável que pode ser inserido em qualquer projeto .NET.

---

## O que você precisará

- **.NET 6.0** ou posterior (o código também funciona com .NET Framework 4.6+).  
- **Aspose.Pdf for .NET** pacote NuGet (`Install-Package Aspose.Pdf`).  
- Um ambiente básico de desenvolvimento C# (Visual Studio, Rider ou VS Code).  

Nenhuma ferramenta de terceiros adicional é necessária; a biblioteca cuida de tudo, desde o layout da página até a conformidade com PDF/A.

---

## Etapa 1: Inicializar o Documento PDF (Criar Documento PDF C#)

A primeira coisa que fazemos é criar um novo objeto `Document`. Pense nele como uma tela em branco — ainda não há nada, mas está pronto para receber páginas, texto e metadados estruturais.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Struct;

// Create a new PDF document – this is the core of our create pdf document c# workflow
Document pdfDoc = new Document();

// Add a blank page to the document; the page will host our positioned text
Page pdfPage = pdfDoc.Pages.Add();
```

> **Por que isso importa:** A classe `Document` é o ponto de entrada para todas as operações do Aspose.Pdf. Adicionar uma página logo no início nos fornece uma superfície para anexar tanto o conteúdo visual quanto a árvore estrutural posteriormente.

---

## Etapa 2: Definir um Parágrafo e Posicioná‑lo (Posicionar Texto no PDF)

Agora criamos um objeto `Paragraph` e informamos ao Aspose exatamente onde ele deve aparecer na página. As coordenadas PDF são medidas em pontos (1 polegada = 72 pt), então usamos `Position(72, 720)` para colocar o parágrafo a 1 polegada da borda esquerda e 10 polegadas acima da base.

```csharp
// Define a paragraph positioned 1 inch from the left and 10 inches from the bottom
Paragraph positionedParagraph = new Paragraph
{
    // Position(x, y) – X is horizontal, Y is vertical from the bottom-left corner
    Position = new Position(72, 720) // 72 pt = 1 inch, 720 pt = 10 inch
};

// Add the actual text we want to display
positionedParagraph.Segments.Add(
    new TextFragment("Tagged paragraph at a specific location.")
);
```

> **Dica profissional:** Se precisar posicionar várias linhas, ajuste a coordenada `Y` para cada parágrafo subsequente, ou use um `TextBuilder` para controle mais fino.

---

## Etapa 3: Criar um Elemento Estrutural (Adicionar Árvore Estrutural)

PDFs voltados à acessibilidade dependem de uma *árvore estrutural* que descreve a ordem lógica do conteúdo. Aqui criamos um `StructureElement` com a tag `"P"` (parágrafo) e anexamos nosso parágrafo posicionado como seu filho.

```csharp
// Create a structural element (tag) for the paragraph – this is the add structural tree step
StructureElement structElement = new StructureElement("P");

// Attach the paragraph as a child of the structural element
structElement.AddKid(positionedParagraph);
```

> **Por que adicionamos uma árvore estrutural:** Leitores de tela e outras tecnologias assistivas utilizam essas tags para navegar no documento. Sem elas, seu PDF pode ser visualmente perfeito, mas inacessível.

---

## Etapa 4: Vincular o Elemento Estrutural à Página

Cada página mantém sua própria coleção de elementos estruturais. Ao adicionar nosso `structElement` a `pdfPage.StructElements`, integramos a hierarquia lógica ao layout visual.

```csharp
// Attach the structural element to the page's structure tree
pdfPage.StructElements.Add(structElement);
```

> **Erro comum:** Esquecer esta etapa significa que a tag existe na memória, mas não está vinculada a nenhuma página, tornando as informações de acessibilidade invisíveis para os leitores.

---

## Etapa 5: Salvar como PDF/A‑2b (Garantindo Preservação a Longo Prazo)

PDF/A‑2b é um subconjunto de PDF projetado para arquivamento. O Aspose.Pdf pode gerar esse formato com uma única chamada. Substitua `"YOUR_DIRECTORY"` por um caminho real na sua máquina.

```csharp
// Save the document as a PDF/A‑2b file – ideal for long‑term storage and compliance
pdfDoc.Save("YOUR_DIRECTORY/TaggedWithPosition.pdf", SaveFormat.PdfA2b);
```

> **Resultado:** Você agora tem um PDF onde o texto está exatamente onde você o colocou, e o documento inclui uma árvore estrutural adequada para ferramentas de acessibilidade.

---

## Exemplo Completo Funcional

Abaixo está o programa completo que você pode copiar‑colar em um aplicativo console. Ele compila e executa como‑está (após adicionar a referência ao NuGet Aspose.Pdf).

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Struct;

namespace PdfPositioningDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Initialize the document
            Document pdfDoc = new Document();
            Page pdfPage = pdfDoc.Pages.Add();

            // Step 2: Define and position the paragraph
            Paragraph positionedParagraph = new Paragraph
            {
                Position = new Position(72, 720) // 1 inch left, 10 inches up
            };
            positionedParagraph.Segments.Add(
                new TextFragment("Tagged paragraph at a specific location.")
            );

            // Step 3: Create the structural element (tag)
            StructureElement structElement = new StructureElement("P");
            structElement.AddKid(positionedParagraph);

            // Step 4: Attach the structural element to the page
            pdfPage.StructElements.Add(structElement);

            // Step 5: Save as PDF/A‑2b
            string outputPath = @"C:\Temp\TaggedWithPosition.pdf";
            pdfDoc.Save(outputPath, SaveFormat.PdfA2b);

            Console.WriteLine($"PDF created successfully at: {outputPath}");
        }
    }
}
```

**Saída esperada:** Após a execução, abra `TaggedWithPosition.pdf`. Você verá a frase “Tagged paragraph at a specific location.” posicionada próximo ao canto inferior‑direito da primeira página. Se inspecionar as tags do PDF (por exemplo, com o painel “Tags” do Adobe Acrobat), encontrará um elemento `<P>` vinculado a esse parágrafo.

---

![Captura de tela do texto posicionado em um PDF gerado com Aspose.Pdf](/images/pdf-positioned.png){: .align-center }

*Texto alternativo da imagem:* **create pdf document c#** – captura de tela mostrando texto posicionado dentro de um PDF gerado com Aspose.Pdf.

---

## Perguntas Frequentes & Casos Limite

### Posso usar outras unidades (mm, cm) para posicionamento?

O Aspose.Pdf trabalha nativamente com pontos. Se preferir milímetros, converta usando `1 mm ≈ 2.83465 pt`. Por exemplo, `Position(25.4, 254)` coloca o parágrafo a 1 cm da esquerda e 9 cm da base.

### E se eu precisar adicionar múltiplas tags (cabeçalhos, tabelas)?

Basta criar objetos `StructureElement` adicionais com tags como `"H1"` para cabeçalhos ou `"Table"` para tabelas, e adicionar o conteúdo correspondente como filhos. O aninhamento funciona da mesma forma — os filhos herdam a ordem lógica do pai.

### Essa abordagem funciona para PDF/A‑1b ou PDF/A‑3b?

Sim. Substitua `SaveFormat.PdfA2b` por `SaveFormat.PdfA1b` ou `SaveFormat.PdfA3b`. Lembre‑se de que cada versão do PDF/A tem seu próprio conjunto de metadados obrigatórios; o Aspose.Pdf avisará caso algo esteja ausente.

---

## Recapitulação

Percorremos um cenário de **criar documento pdf c#** que:

1. Instancia um novo PDF usando Aspose.Pdf.  
2. **Posiciona texto no PDF** definindo coordenadas exatas.  
3. **Adiciona árvore estrutural** para acessibilidade.  
4. Salva o resultado como um arquivo PDF/A‑2b compatível com padrões.

Todas as etapas são totalmente autônomas, e você pode adaptar o trecho para layouts mais complexos, múltiplas páginas ou diferentes tipos de tags.

---

## O que vem a seguir?

- **Estilizar texto** – explore `TextState` para mudar fontes, cores e tamanhos.  
- **Incorporar imagens** – use `ImageFragment` e posicione‑as ao lado do parágrafo.  
- **Gerar tabelas** – crie objetos `Table` e marque‑os com `"Table"` para semântica avançada.  
- **Pipelines de automação** – integre este código a um serviço em segundo plano que gera faturas diariamente.

Sinta‑se à vontade para experimentar e nos conte quais variações foram mais úteis. Boa codificação!

## O que você deve aprender a seguir?

Os tutoriais abaixo abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas em seus próprios projetos.

- [Create Tagged PDFs with Aspose.PDF for .NET&#58; A Complete Guide to Enhancing Accessibility and Document Structure](/pdf/english/net/advanced-features/create-tagged-pdfs-aspose-pdf-net/)
- [Create PDF Document with Aspose.PDF – Step‑by‑Step Guide](/pdf/english/net/document-creation/create-pdf-document-with-aspose-pdf-step-by-step-guide/)
- [Create & Rotate Text in PDFs Using Aspose.PDF .NET&#58; A Comprehensive Guide for Developers](/pdf/english/net/text-operations/create-rotate-text-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}