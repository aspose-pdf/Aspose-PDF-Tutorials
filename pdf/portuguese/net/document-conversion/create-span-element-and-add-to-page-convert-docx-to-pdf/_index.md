---
category: general
date: 2026-03-27
description: Crie um elemento span em C# e aprenda como adicionar o span a uma página
  ao converter DOCX para PDF e salvar como PDF. Guia passo a passo para desenvolvedores.
draft: false
keywords:
- create span element
- how to add span
- convert docx to pdf
- add element to page
- save as pdf
language: pt
og_description: Crie um elemento span em C# e aprenda como adicionar span a uma página
  ao converter DOCX para PDF, depois salvar como PDF. Exemplo de código completo incluído.
og_title: Criar elemento span e adicionar à página – Converter DOCX para PDF
tags:
- C#
- DocumentProcessing
- PDFConversion
title: Criar elemento span e adicionar à página – Converter DOCX para PDF
url: /pt/net/document-conversion/create-span-element-and-add-to-page-convert-docx-to-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar elemento span e adicionar à página – Converter DOCX para PDF

Criar **elemento span** em um arquivo DOCX é uma tarefa comum quando você precisa de controle preciso de layout. Neste tutorial vamos mostrar **como adicionar um span** a uma página, **converter DOCX para PDF** e **salvar como PDF** — tudo em alguns passos simples.  

Se você já ficou olhando para um documento do Word e pensou: “Eu gostaria de colocar uma caixinha de texto em uma coordenada exata”, está no lugar certo. Vamos percorrer todo o fluxo de trabalho, desde o carregamento do arquivo fonte até a obtenção de um PDF finalizado.

## O que você vai conseguir

Ao final deste guia você será capaz de:

* Carregar um arquivo `.docx` usando a classe `Document` da biblioteca de documentos.  
* **Criar elemento span** com a API `TaggedContent`.  
* Posicionar esse span em coordenadas X/Y exatas em uma página escolhida.  
* **Adicionar elemento à página** de forma confiável, mesmo quando a página não for a primeira.  
* **Converter DOCX para PDF** e **salvar como PDF** com uma única chamada `Save`.

Sem ferramentas externas, sem configurações misteriosas — apenas código C# puro que você pode copiar‑colar no seu projeto.

## Pré‑requisitos

* .NET 6+ (ou qualquer runtime .NET recente que sua biblioteca suporte).  
* O SDK de processamento de documentos que fornece `Document`, `TaggedContent`, `Position`, etc.  
* Um entendimento básico da sintaxe C# — se você consegue escrever um `Console.WriteLine`, está pronto.

> **Dica profissional:** Mantenha sua versão do SDK atualizada; a versão mais recente (v3.2 a partir de março 2026) inclui ajustes de desempenho para operações ao nível de página.

---

![Diagram illustrating how to create span element and place it on a PDF page](https://example.com/images/create-span-element.png "Create span element placement diagram")

## Criar elemento span – Posicionar e Adicionar à Página

Abaixo está o código completo e executável que faz tudo, desde carregar o DOCX fonte até gerar o PDF final. Sinta‑se à vontade para inseri‑lo em um aplicativo console, ajustar os caminhos e executá‑lo.

```csharp
using DocumentProcessing;   // Replace with the actual namespace of your SDK
using DocumentProcessing.Models;

class Program
{
    static void Main()
    {
        // Step 1: Load the DOCX you want to modify
        // -------------------------------------------------
        // The constructor takes a file path; make sure the file exists.
        Document doc = new Document(@"C:\Docs\input.docx");

        // Step 2: Create a new span element using the TaggedContent API
        // -------------------------------------------------
        // A span is a lightweight container for inline content.
        var span = doc.TaggedContent.CreateSpanElement();
        // Optional: add some text inside the span
        span.Text = "Hello, world!";

        // Step 3: Position the span at the desired coordinates (X = 50, Y = 750)
        // -------------------------------------------------
        // Position uses points (1/72 inch). Adjust as needed.
        span.Position = new Position(50, 750);

        // Step 4: Add the span to the target page (page index 1 = second page)
        // -------------------------------------------------
        // Pages are zero‑based; index 1 means the second page in the document.
        doc.Pages[1].Add(span);

        // Step 5: Convert the modified DOCX to PDF and save the result
        // -------------------------------------------------
        // The Save method automatically detects the output format from the extension.
        doc.Save(@"C:\Docs\output.pdf");

        // Confirmation output
        Console.WriteLine("Span added, document converted, and PDF saved successfully.");
    }
}
```

### Explicação passo a passo

#### Etapa 1 – Carregar o documento DOCX  
Instanciamos um objeto `Document` apontando para `input.docx`. Esse objeto representa todo o arquivo Word na memória, dando acesso a páginas, conteúdo e metadados.  

#### Etapa 2 – Criar um elemento span  
A chamada `TaggedContent.CreateSpanElement()` devolve um contêiner inline leve. Pense nele como uma caixinha invisível que pode conter texto, imagens ou outros elementos inline. Definir o texto (`span.Text`) é opcional, mas útil para depuração.

#### Etapa 3 – Posicionar o span  
`new Position(50, 750)` define o canto superior esquerdo do span a 50 pts da margem esquerda e 750 pts do topo da página. Esses valores são absolutos, então você pode colocar o span onde quiser — perfeito para layouts precisos.

#### Etapa 4 – Adicionar o span à página alvo  
`doc.Pages[1].Add(span)` injeta o span na segunda página. A API usa indexação baseada em zero, então a página 0 é a primeira página. Se precisar adicioná‑lo à primeira página, basta usar `doc.Pages[0]`.

#### Etapa 5 – Converter DOCX para PDF e salvar como PDF  
Chamar `doc.Save("output.pdf")` faz duas coisas: grava o documento modificado no disco **e** converte o conteúdo para PDF por causa da extensão `.pdf`. Nenhum passo extra de conversão é necessário — esta é a maneira mais fácil de **salvar como PDF**.

---

## Como adicionar span em outra página (avançado)

Às vezes você não conhece o índice da página com antecedência. Você pode localizar uma página pelo seu número (amigável ao usuário) ou pesquisando por uma palavra‑chave específica.

```csharp
// Find the page that contains the word "Summary"
int targetIndex = doc.Pages
    .Select((p, i) => new { Page = p, Index = i })
    .FirstOrDefault(x => x.Page.Text.Contains("Summary"))?.Index ?? 0;

// Fallback to first page if not found
targetIndex = Math.Max(targetIndex, 0);

// Add the span to the discovered page
doc.Pages[targetIndex].Add(span);
```

**Por que isso importa:** Em relatórios onde o número de páginas varia, codificar `Pages[1]` pode quebrar o layout. Este trecho demonstra um padrão robusto para **como adicionar span** dinamicamente.

---

## Armadilhas comuns e como evitá‑las

| Problema | O que acontece | Solução |
|----------|----------------|---------|
| **Span não visível** | As coordenadas ficam fora da página ou o span tem largura/altura zero. | Verifique novamente os valores de `Position`; use uma régua no visualizador de PDF. |
| **Índice de página errado** | Você adiciona na página 0 mas espera que apareça na página 2. | Lembre‑se que a API usa indexação zero; adicione 1 ao número da página humana. |
| **Salvar sobrescreve a fonte** | `doc.Save("input.docx")` substitui o arquivo original. | Sempre salve em um caminho novo (`output.pdf`) ao converter. |
| **Referência ao SDK ausente** | Erro de compilação na classe `Document`. | Instale o pacote NuGet: `dotnet add package DocumentProcessing.SDK`. |

---

## Verificando o resultado

Depois de executar o programa, abra `output.pdf` em qualquer visualizador de PDF. Você deverá ver o texto “Hello, world!” posicionado exatamente em (50, 750) na segunda página. Se o texto aparecer em outro lugar, ajuste os valores de `Position` e execute novamente.  

Para testes automatizados, você pode usar um parser de PDF (por exemplo, iTextSharp) para validar programaticamente as coordenadas do texto.

```csharp
// Example using iTextSharp to verify position (pseudo‑code)
var pdfReader = new PdfReader(@"C:\Docs\output.pdf");
var page = pdfReader.GetPageContent(2);
Debug.Assert(page.Contains("Hello, world!"));
```

---

## Próximos passos

* **Estilizar o span** – explore `span.Font`, `span.Color` e outras propriedades de estilo.  
* **Adicionar imagens** – use `CreateImageElement()` em vez de um span para gráficos.  
* **Processamento em lote** – percorra uma pasta de arquivos DOCX

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}