---
category: general
date: 2026-06-05
description: Crie um elemento span em um documento Word usando C#. Aprenda como adicionar
  span, definir posição absoluta e adicionar uma tag personalizada em apenas alguns
  passos.
draft: false
keywords:
- create span element
- how to add span
- set absolute position
- position text in word
- add custom tag
language: pt
og_description: Crie um elemento span em um arquivo Word usando C#. Este tutorial
  mostra como adicionar span, definir posição absoluta e adicionar tag personalizada
  de forma eficiente.
og_title: Criar elemento Span no Word com C# – Passo a passo
schemas:
- author: Aspose
  dateModified: '2026-06-05'
  description: Create span element in a Word document using C#. Learn how to add span,
    set absolute position, and add custom tag in just a few steps.
  headline: Create Span Element in Word with C# – Complete Guide
  type: TechArticle
- questions:
  - answer: Word will clip the content, or it may push the span onto a new page. Always
      validate against page size (`doc.FirstSection.PageSetup.PageWidth`) and margins.
    question: What if the coordinates are outside the printable area?
  - answer: Yes—use `span.AddPicture("path/to/image.png")` before saving. The same
      absolute positioning rules apply.
    question: Can I add images to a span?
  - answer: Not directly. It behaves like an inline object, so you’ll see its text
      or image, but the tag itself stays hidden.
    question: Is the span visible in the Word UI?
  - answer: '`Document` implements `IDisposable`, so wrapping it in a `using` block
      is a good practice, especially for large files.'
    question: Do I need to dispose of the `Document` object?
  type: FAQPage
tags:
- C#
- Aspose.Words
- Word Automation
title: Criar elemento Span no Word com C# – Guia completo
url: /pt/net/programming-with-text/create-span-element-in-word-with-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar Elemento Span no Word com C# – Guia Completo

Já precisou **criar um elemento span** dentro de um documento Word, mas não sabia por onde começar? Você não está sozinho — muitos desenvolvedores encontram esse obstáculo ao explorar a manipulação programática do Word pela primeira vez. Neste guia, vamos percorrer **como adicionar um span**, posicioná‑lo com precisão e até anexar uma tag personalizada, tudo com código C# limpo.

Usaremos a biblioteca Aspose.Words for .NET, que facilita o trabalho com arquivos Word. Ao final deste tutorial, você será capaz de **definir posição absoluta** para qualquer trecho de texto, controlar seu layout e persistir as alterações sem quebrar a estrutura do documento.

## O que você vai precisar

- .NET 6.0 ou superior (o código também compila com .NET Core)  
- Aspose.Words for .NET (pacote NuGet `Aspose.Words`)  
- Noções básicas de C# (loops, objetos, etc.)  
- Um arquivo DOCX de entrada para experimentar (vamos chamá‑lo de `input.docx`)

É só isso — sem ferramentas extras, sem dependências obscuras. Pronto? Vamos lá.

![Create span element positioned in Word document](image-placeholder.png)

*Alt text: criar elemento span posicionado em documento Word*

## Etapa 1: Inicializar o Documento e Criar um Elemento Span

A primeira coisa a fazer é carregar o DOCX de origem e pedir ao Aspose.Words que lhe forneça um novo objeto **span element**. Pense no span como um pequeno contêiner que pode conter texto, imagens ou até outros objetos inline.

```csharp
using Aspose.Words;
using Aspose.Words.Tagging;

class Program
{
    static void Main()
    {
        // Load the existing Word document
        Document doc = new Document("YOUR_DIRECTORY/input.docx");

        // Create a new span element – this is the core of our tutorial
        var span = doc.TaggedContent.CreateSpanElement();

        // We'll add the span to the document in the next step
    }
}
```

**Por que isso importa:** `CreateSpanElement` é a única forma de gerar um objeto inline marcado que o Aspose.Words reconhece como *span*. Sem ele, você ficaria preso inserindo texto bruto que não pode ser posicionado absolutamente.

## Etapa 2: Como Adicionar o Span à Hierarquia TaggedContent

Agora que temos um span, precisamos **add span** à árvore de conteúdo marcado do documento. O elemento raiz funciona como a pasta de nível superior em um sistema de arquivos — tudo o que você adicionar abaixo passa a fazer parte do fluxo.

```csharp
// Append the newly created span to the root of the TaggedContent hierarchy
doc.TaggedContent.RootElement.AppendChild(span);
```

Se você pular esta etapa, o span existirá na memória, mas nunca aparecerá no arquivo salvo. É o clássico bug de “criado, mas não anexado” que atrapalha iniciantes.

## Etapa 3: Definir Posição Absoluta – Posicionar Texto no Word com Precisão

O posicionamento absoluto no Word usa pontos (1 pt = 1/72 in). Ao chamar `SetPosition(x, y)` informamos ao Aspose.Words exatamente onde na página o span deve ficar, ignorando o fluxo normal de parágrafos.

```csharp
// Set the X and Y coordinates in points (100 pt ≈ 1.39 in, 200 pt ≈ 2.78 in)
span.SetPosition(100, 200);
```

**Dica rápida:** A origem das coordenadas (0,0) começa no canto superior esquerdo da área imprimível, não na borda física da página. Se precisar considerar as margens, adicione o tamanho da margem aos valores X/Y.

## Etapa 4: Adicionar Tag Personalizada – Enriquecer o Span com Metadados

Tags personalizadas permitem armazenar informações extras que podem ser consultadas ou substituídas posteriormente. Por exemplo, você pode marcar um span como “AuthorSignature” para que um processo posterior o localize automaticamente.

```csharp
// Attach a custom tag named "MyCustomTag" with a simple value
span.CustomTags.Add("MyCustomTag", "SampleValue");
```

**Quando usar:** Se você estiver construindo um mecanismo de templating, tags personalizadas são o seu molho secreto. Elas sobrevivem a salvamentos e podem ser lidas novamente sem precisar analisar o conteúdo visual.

## Etapa 5: Salvar o Documento para Persistir as Alterações

Por fim, grave o documento modificado de volta ao disco. O método `Save` cuida de todo o trabalho pesado, garantindo que a posição e as tags do span sejam armazenadas corretamente.

```csharp
// Save the modified document; this writes the span with its absolute position
doc.Save("YOUR_DIRECTORY/output.docx");
```

Abra `output.docx` no Word e você verá o texto (ou qualquer conteúdo inline que você adicionar ao span depois) exatamente nas coordenadas especificadas. A tag personalizada é invisível na interface, mas pode ser inspecionada via APIs do Aspose.Words.

## Exemplo Completo em Funcionamento

Juntando tudo, segue o programa completo que você pode copiar‑colar e executar:

```csharp
using System;
using Aspose.Words;
using Aspose.Words.Tagging;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source document
        Document doc = new Document("YOUR_DIRECTORY/input.docx");

        // 2️⃣ Create a new span element
        var span = doc.TaggedContent.CreateSpanElement();

        // 3️⃣ Append the span to the root hierarchy
        doc.TaggedContent.RootElement.AppendChild(span);

        // 4️⃣ Set absolute position (X = 100 pt, Y = 200 pt)
        span.SetPosition(100, 200);

        // 5️⃣ Add a custom tag for later identification
        span.CustomTags.Add("MyCustomTag", "SampleValue");

        // 6️⃣ Optionally, insert some text into the span
        span.Text = "Hello, positioned world!";

        // 7️⃣ Save the document
        doc.Save("YOUR_DIRECTORY/output.docx");

        Console.WriteLine("Span element created, positioned, and saved successfully.");
    }
}
```

**Resultado esperado:** Ao abrir `output.docx` aparecerá a frase *“Hello, positioned world!”* flutuando exatamente no ponto que você definiu, independente dos parágrafos ao redor. A tag personalizada `MyCustomTag` está anexada e pode ser consultada depois com `doc.TaggedContent.GetElementsByTag("MyCustomTag")`.

## Perguntas Frequentes & Casos de Borda

- **E se as coordenadas estiverem fora da área imprimível?**  
  O Word recortará o conteúdo ou pode mover o span para uma nova página. Sempre valide contra o tamanho da página (`doc.FirstSection.PageSetup.PageWidth`) e as margens.

- **Posso adicionar imagens a um span?**  
  Sim — use `span.AddPicture("path/to/image.png")` antes de salvar. As mesmas regras de posicionamento absoluto se aplicam.

- **O span é visível na UI do Word?**  
  Não diretamente. Ele se comporta como um objeto inline, então você verá seu texto ou imagem, mas a tag permanece oculta.

- **Preciso descartar o objeto `Document`?**  
  `Document` implementa `IDisposable`, portanto envolver seu uso em um bloco `using` é uma boa prática, especialmente para arquivos grandes.

## Dicas de Profissional

- **Posicionamento em lote:** Se precisar colocar muitos spans, faça um loop sobre a fonte de dados e calcule X/Y dinamicamente.  
- **Conversão de coordenadas:** Para designers que pensam em centímetros, multiplique os centímetros por 28,35 para obter pontos.  
- **Segurança de versão:** O código funciona com Aspose.Words 23.3 ou superior; versões mais antigas podem usar `CreateSpan` em vez de `CreateSpanElement`.

## Conclusão

Agora você sabe exatamente como **criar elemento span**, **como add span** em um documento Word, **definir posição absoluta** e **adicionar tag personalizada** usando C#. Essa abordagem oferece controle pixel‑perfect sobre a colocação de texto e abre caminho para cenários avançados de templating.

Qual o próximo passo? Experimente substituir o texto simples por uma imagem de logotipo, teste diferentes coordenadas ou construa um pequeno motor que substitua todos os spans com uma tag específica em tempo de execução. O céu é o limite quando você domina o fluxo de trabalho com spans.

Feliz codificação, e sinta‑se à vontade para deixar um comentário se algo não estiver claro!

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas de implementação em seus próprios projetos.

- [Add Structure Element into Element in PDF using Java](/pdf/english/java/pdf-structure-elements/add-structure-element-into-element-in-pdf-using-java/)
- [How to Add Text to PDFs Using Aspose.PDF for Java: A Comprehensive Guide](/pdf/english/java/text-operations/aspose-pdf-java-add-text-to-pdf/)
- [How to Add Text Stamps to PDFs Using Aspose.PDF for Java](/pdf/english/java/watermarks-backgrounds/aspose-pdf-java-add-text-stamp/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}