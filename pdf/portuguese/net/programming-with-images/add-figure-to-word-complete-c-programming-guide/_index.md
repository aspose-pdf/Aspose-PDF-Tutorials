---
category: general
date: 2026-04-12
description: Adicione figura ao Word rapidamente com C#. Aprenda como posicionar a
  figura no Word, inserir a figura no docx e adicionar XML personalizado para layout
  avançado.
draft: false
keywords:
- add figure to word
- position figure in word
- insert figure into docx
- how to add custom xml
- how to position shape word
language: pt
og_description: Adicione figura ao Word rapidamente com C#. Aprenda como posicionar
  a figura no Word, inserir a figura no docx e adicionar XML personalizado para layout
  avançado.
og_title: Adicionar Figura ao Word – Guia Completo de Programação em C#
tags:
- C#
- Word Automation
- Document Generation
title: Adicionar Figura ao Word – Guia Completo de Programação C#
url: /pt/net/programming-with-images/add-figure-to-word-complete-c-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Adicionar Figura ao Word – Guia Completo de Programação C#

Já precisou **add figure to Word** mas não sabia por onde começar? Você não está sozinho. Em muitos projetos de automação de escritório, a peça que falta é uma imagem ou diagrama bem posicionado que vive dentro de uma parte de XML personalizada. Este guia mostra exatamente como **position figure in Word**, inserir a figura em um arquivo *.docx* e ainda ajustar o XML personalizado subjacente para que a forma se comporte como qualquer objeto nativo do Word.

Vamos percorrer um exemplo real usando a biblioteca GemBox.Document (gratuita para arquivos pequenos, comercial para cargas maiores). Ao final, você terá um programa autônomo e executável que coloca uma figura nas coordenadas X = 50, Y = 200 dentro de um contêiner de conteúdo marcado. Sem atalhos vagos de “veja a documentação” — apenas código claro, por que funciona e dicas que você pode copiar direto para seu próprio projeto.

## Pré‑requisitos

- .NET 6.0 ou superior (o código também compila com .NET Core 3.1)
- Pacote NuGet **GemBox.Document** (`Install-Package GemBox.Document`)
- Um arquivo Word inicial (`input.docx`) que já contenha uma tag de XML personalizada onde você deseja que a figura apareça
- Conhecimento básico de C# (você verá por que cada linha importa)

> **Dica de especialista:** Se você não tem um documento pré‑marcado, pode criar um no Word inserindo um *Content Control* → *XML Mapping Pane* → mapear uma parte de XML personalizada. A biblioteca tratará esse controle como `TaggedContent`.

## Etapa 1 – Carregar o Documento Fonte

A primeira coisa que fazemos é abrir o arquivo *.docx* existente. `Document` é o ponto de entrada para todas as operações do GemBox.

```csharp
using GemBox.Document;
using System.Drawing;

// Set the license key (free version uses a limited license key)
ComponentInfo.SetLicense("FREE-LIMITED-KEY");

// Step 1: Load the source document
Document doc = new Document(@"YOUR_DIRECTORY\input.docx");
```

*Por quê?* Carregar o arquivo nos dá acesso às suas partes internas, incluindo quaisquer contêineres de XML personalizados. Sem isso, não conseguiríamos localizar o nó `TaggedContent` que armazenará nossa figura.

## Etapa 2 – Acessar o Conteúdo Marcado (Contêiner de XML Personalizado)

XML personalizado é armazenado dentro de um *content control* no Word. O GemBox o expõe como `TaggedContent`.

```csharp
// Step 2: Access the document's tagged content (the container for custom XML)
TaggedContent taggedContent = doc.TaggedContent;
```

Se o documento possuir várias seções marcadas, `TaggedContent` retorna a **primeira**. Você também pode enumerar `doc.TaggedContents` para escolher uma tag específica pelo nome.

## Etapa 3 – Criar o Elemento de Figura

Um `FigureElement` representa uma imagem, gráfico ou qualquer objeto visual que o Word trata como uma *shape*. Criaremos ele dentro do contêiner marcado.

```csharp
// Step 3: Create a new figure element that will be placed inside the tagged content
FigureElement figure = taggedContent.CreateFigureElement();
```

*Por que criar a figura aqui?* Ao vinculá‑la ao nó de XML personalizado, o Word sabe que a figura pertence àquela seção lógica, o que é crucial para edições posteriores ou fluxos de trabalho baseados em controles de conteúdo.

## Etapa 4 – Posicionar a Figura Precisamente

O Word usa pontos (1 pt ≈ 1/72 in) para posicionamento. A estrutura `PointF` permite definir coordenadas X/Y facilmente.

```csharp
// Step 4: Position the figure at the desired coordinates (X = 50, Y = 200)
figure.Position = new PointF(50, 200);
```

> **Como posicionar shape word:** A propriedade `Position` aceita um `PointF` onde o primeiro valor é o deslocamento horizontal (esquerda) e o segundo é o deslocamento vertical (topo) relativo à margem da página. Ajuste esses números para refinar a colocação.

## Etapa 5 – Inserir a Figura na Árvore de Conteúdo Marcado

Agora anexamos a figura ao elemento raiz da árvore de XML personalizada. Isso adiciona fisicamente a forma ao documento Word.

```csharp
// Step 5: Insert the figure into the root element of the tagged content tree
taggedContent.RootElement.AppendChild(figure);
```

Neste ponto a figura está dentro do documento, mas ainda não tem uma fonte de imagem. Vamos adicionar um PNG simples do disco.

```csharp
// Optional: Load an image and assign it to the figure
using (var imageStream = System.IO.File.OpenRead(@"YOUR_DIRECTORY\sample.png"))
{
    figure.Image = new Image(imageStream);
}
```

## Etapa 6 – Salvar o Documento Modificado

Por fim, gravamos as alterações em um novo arquivo *.docx*.

```csharp
// Step 6: Save the updated document
doc.Save(@"YOUR_DIRECTORY\output.docx");
```

Ao abrir `output.docx` no Word, você verá a imagem posicionada exatamente em (50, 200) dentro do bloco de XML personalizado que você direcionou.

### Exemplo Completo Funcional

```csharp
using GemBox.Document;
using System.Drawing;
using System.IO;

class Program
{
    static void Main()
    {
        // License (free version)
        ComponentInfo.SetLicense("FREE-LIMITED-KEY");

        // Load the source DOCX
        Document doc = new Document(@"YOUR_DIRECTORY\input.docx");

        // Access the first tagged content container
        TaggedContent taggedContent = doc.TaggedContent;

        // Create a new figure element
        FigureElement figure = taggedContent.CreateFigureElement();

        // Position the figure (X = 50 pt, Y = 200 pt)
        figure.Position = new PointF(50, 200);

        // Load an image file and assign it
        using (FileStream fs = File.OpenRead(@"YOUR_DIRECTORY\sample.png"))
        {
            figure.Image = new Image(fs);
        }

        // Append the figure to the custom XML root
        taggedContent.RootElement.AppendChild(figure);

        // Save the result
        doc.Save(@"YOUR_DIRECTORY\output.docx");
    }
}
```

**Resultado esperado:** Abrir `output.docx` mostra o PNG colocado exatamente onde você especificou, aninhado dentro da parte de XML personalizada. Se você inspecionar o XML do documento (`.docx` → unzip → `word/document.xml`), verá um elemento `<w:pict>` com as coordenadas corretas do `<v:shape>`.

## Perguntas Frequentes & Casos de Borda

### E se o documento tiver várias seções marcadas?

Use `doc.TaggedContents` para enumerar e selecionar pelo nome da tag:

```csharp
TaggedContent myTag = doc.TaggedContents.First(tc => tc.TagName == "MyCustomTag");
```

### Como adicionar uma legenda à figura?

```csharp
figure.Caption = new CaptionElement("Figure 1 – Sample Diagram");
```

### Isso funciona com Word 2010 e versões posteriores?

Sim. O GemBox.Document tem como alvo o padrão Open XML, que é compatível com Word 2007 + (incluindo 2010, 2013, 2016, 2019 e Microsoft 365).

### E se eu precisar girar a forma?

```csharp
figure.Rotation = 45; // degrees
```

### Como adicionar um gráfico vetorial em vez de uma imagem raster?

```csharp
figure.Image = new Image(@"YOUR_DIRECTORY\vector.svg");
```

## Dicas de Especialista & Armadilhas

- **Caminhos de arquivo:** Use `Path.Combine` para evitar separadores codificados, especialmente em plataformas não‑Windows.
- **Limites de licença:** A licença gratuita do GemBox limita o tamanho do documento a 20 KB. Para arquivos maiores, adquira uma chave comercial.
- **Desempenho:** Reutilizar uma única instância de `Document` para processamento em lote reduz drasticamente o uso de memória.
- **Transbordamento de forma:** Se as dimensões da figura excederem as margens da página, o Word a recortará. Ajuste `figure.Width` e `figure.Height` conforme necessário.

## Conclusão

Agora você sabe **how to add figure to Word**, **position figure in Word** com precisão e manipular o XML personalizado subjacente para que a forma se comporte como qualquer elemento nativo. O exemplo completo e executável demonstra cada passo — desde carregar o documento, criar um `FigureElement`, definir suas coordenadas, anexar uma imagem e, finalmente, salvar o *.docx* atualizado.

Em seguida, experimente **insert figure into docx** adicionando múltiplas figuras, usando loops ou gerando gráficos dinamicamente. Você também pode explorar **how to add custom xml** para controles de conteúdo mais ricos ou aprender **how to position shape word** em tabelas e cabeçalhos. As possibilidades são infinitas, e com os fundamentos cobertos aqui você está pronto para automatizar documentos Word como um profissional.

Boa codificação, e sinta‑se à vontade para deixar um comentário se encontrar algum obstáculo!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}