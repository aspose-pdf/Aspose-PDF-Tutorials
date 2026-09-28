---
category: general
date: 2026-09-27
description: Adicione numeração Bates a PDF usando Aspose.PDF em C#. Aprenda como
  carregar um documento PDF, definir as opções de numeração Bates e salvar o arquivo
  atualizado.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add bates numbering
- load pdf document
- how to add bates numbering
- Aspose.PDF C#
- PDF Bates numbering example
language: pt
lastmod: 2026-09-27
og_description: Adicione numeração Bates a PDF usando Aspose.PDF em C#. Este tutorial
  mostra como carregar um documento PDF, configurar a numeração Bates e salvar o resultado.
og_image_alt: Screenshot of a PDF page displaying Bates numbers in the footer
og_title: Adicionar numeração Bates a PDF com Aspose.PDF – Guia C#
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Add bates numbering to PDF using Aspose.PDF in C#. Learn how to load
    a PDF document, set Bates numbering options, and save the updated file.
  headline: Add bates numbering to PDF using Aspose.PDF in C#
  type: TechArticle
tags:
- Aspose.PDF
- C#
- PDF processing
title: Adicionar numeração Bates ao PDF usando Aspose.PDF em C#
url: /pt/net/programming-with-text/add-bates-numbering-to-pdf-using-aspose-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Adicionar numeração Bates a PDF usando Aspose.PDF em C#

Se você precisa **adicionar numeração Bates** a um arquivo PDF, este guia mostra uma solução completa e pronta‑para‑executar. Você verá como **carregar um documento PDF**, configurar as opções de numeração Bates e gravar o arquivo numerado de volta ao disco — tudo com Aspose.PDF para .NET.

Aplicar números Bates é comum em fluxos de trabalho jurídicos, de aplicação da lei e de arquivamento. Ao final deste tutorial você poderá inserir um identificador sequencial em cada página, personalizar o prefixo e iniciar a contagem em qualquer número que escolher.

## O que você aprenderá

* Como **carregar o conteúdo de um documento PDF** em um objeto `Aspose.Pdf.Document`.  
* As etapas exatas **de como adicionar numeração Bates** com `BatesNumberingOptions`.  
* Como salvar o arquivo modificado preservando o layout e a qualidade originais.  

Nenhuma ferramenta externa é necessária — apenas o pacote NuGet Aspose.PDF e um ambiente de desenvolvimento .NET (Visual Studio, VS Code ou Rider).  

---

## Etapa 1: Instalar Aspose.PDF para .NET

Abra a pasta do seu projeto em um terminal e execute:

```bash
dotnet add package Aspose.PDF
```

O pacote inclui o namespace `Aspose.Pdf`, que fornece todas as classes usadas neste tutorial. Após a instalação, recarregue o projeto para que a IDE reconheça a nova referência.

## Etapa 2: Carregar documento PDF

Carregar o arquivo fonte é a primeira operação porque o mecanismo de numeração Bates funciona em uma instância `Document` já existente.

```csharp
using Aspose.Pdf;

// ...

// Replace with the path to your input PDF
string inputPath = @"YOUR_DIRECTORY\input.pdf";

// Load the PDF document into memory
Document doc = new Document(inputPath);
```

**Por que isso importa:** A classe `Document` analisa a estrutura do PDF, dando acesso a páginas, anotações e metadados. Sem carregar o arquivo primeiro, não é possível aplicar nenhuma numeração.

## Etapa 3: Configurar opções de numeração Bates

Crie um objeto `BatesNumberingOptions` e defina o prefixo desejado, o número inicial e os parâmetros de formatação opcionais.

```csharp
using Aspose.Pdf;

// ...

BatesNumberingOptions batesOptions = new BatesNumberingOptions
{
    // Text that appears before the numeric part
    Prefix = "CASE01",

    // First number to use (1 means the first page gets CASE01-1)
    StartNumber = 1,

    // Optional: customize the appearance
    // The default places the number in the footer, centered.
    // You can change Font, FontSize, Color, and Position if needed.
    // Example:
    // Font = FontRepository.FindFont("Arial"),
    // FontSize = 10,
    // Color = Color.Black,
    // Margin = new Margin(0, 0, 0, 20)
};
```

**Por que isso importa:** `BatesNumberingOptions` indica ao Aspose.PDF como gerar o rótulo para cada página. O `Prefix` ajuda a agrupar casos relacionados, enquanto `StartNumber` permite continuar uma sequência a partir de um lote anterior.

## Etapa 4: Salvar o PDF com numeração Bates aplicada

Passe o objeto de opções para o método `Save`. Aspose.PDF grava os números diretamente em cada página.

```csharp
// Replace with the desired output path
string outputPath = @"YOUR_DIRECTORY\output.pdf";

// Save the document, applying the Bates numbering
doc.Save(outputPath, batesOptions);
```

**Por que isso importa:** A sobrecarga `Save(string, BatesNumberingOptions)` combina a etapa de renderização com o processo de numeração, garantindo que o arquivo de saída contenha os identificadores visíveis.

## Exemplo completo – tudo junto

Abaixo está um programa único e autocontido que você pode copiar, colar e executar. Ele demonstra **como adicionar numeração Bates** do início ao fim.

```csharp
using System;
using Aspose.Pdf;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the PDF document
            string inputPath = @"YOUR_DIRECTORY\input.pdf";
            Document doc = new Document(inputPath);

            // 2️⃣ Set up Bates numbering options
            BatesNumberingOptions batesOptions = new BatesNumberingOptions
            {
                Prefix = "CASE01",
                StartNumber = 1,
                // Optional appearance tweaks:
                // Font = FontRepository.FindFont("Times New Roman"),
                // FontSize = 9,
                // Color = Color.DarkBlue,
                // Margin = new Margin(0, 0, 0, 15)
            };

            // 3️⃣ Save the document with Bates numbers
            string outputPath = @"YOUR_DIRECTORY\output.pdf";
            doc.Save(outputPath, batesOptions);

            Console.WriteLine($"Bates numbering added. Output saved to: {outputPath}");
        }
    }
}
```

### Saída esperada

Executar o programa produz `output.pdf` onde cada página exibe um rótulo semelhante a:

```
CASE01-1
CASE01-2
CASE01-3
...
```

Os números aparecem no rodapé por padrão, mas você pode movê‑los ajustando a propriedade `Margin` em `BatesNumberingOptions`.

## Casos limites e variações comuns

| Situação | O que ajustar |
|-----------|----------------|
| **Prefixo diferente por lote** | Altere `Prefix` antes de chamar `Save`. Você pode percorrer vários documentos com prefixos distintos. |
| **Continuar numeração a partir de um arquivo anterior** | Defina `StartNumber` para o último número usado + 1. |
| **Colocar números no cabeçalho** | Use `batesOptions.Margin = new Margin(20, 0, 0, 0);` (margem superior) ou personalize `batesOptions.Position`. |
| **Fonte ou cor personalizada** | Atribua as propriedades `Font`, `FontSize` e `Color` conforme mostrado na seção comentada. |
| **PDFs grandes (1000+ páginas)** | A operação é eficiente em memória; porém, pode ser útil habilitar `doc.OptimizeResources()` antes de salvar para reduzir o tamanho do arquivo. |

**Dica:** Se seu fluxo de trabalho exigir esquemas de numeração diferentes por documento, encapsule a lógica em um método auxiliar:

```csharp
static void ApplyBatesNumbering(string src, string dst, string prefix, int start)
{
    var doc = new Document(src);
    var opts = new BatesNumberingOptions { Prefix = prefix, StartNumber = start };
    doc.Save(dst, opts);
}
```

## Conclusão

Agora você sabe **como adicionar numeração Bates** a qualquer PDF usando Aspose.PDF em C#. O tutorial abordou o carregamento do documento PDF, a configuração das opções de numeração e a gravação do arquivo final — tudo em um único programa executável.  

A partir daqui, você pode explorar tópicos relacionados, como **adicionar marcas d'água**, **mesclar vários PDFs** ou **extrair texto** com Aspose.PDF. Experimente diferentes fontes, cores e posições para adequar aos padrões de formatação da sua organização.

Pronto para automatizar seu fluxo de trabalho de documentos legais? Adicione o código ao seu pipeline de build, execute‑o em lotes de arquivos e deixe o Aspose.PDF fazer o trabalho pesado. Boa codificação!


## O que você deve aprender a seguir?


Os tutoriais a seguir cobrem tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas de implementação em seus próprios projetos.

- [Create PDF Document C# – Add Bates Numbering](/pdf/english/net/programming-with-pdf-pages/create-pdf-document-c-add-bates-numbering/)
- [Add Bates Numbering PDF – Step‑by‑Step Guide to Number PDF Pages](/pdf/english/net/programming-with-pdf-pages/add-bates-numbering-pdf-step-by-step-guide-to-number-pdf-pag/)
- [Aspose PDF Tutorial – Insert a Blank Page and Update Bates Numbering](/pdf/english/net/programming-with-pdf-pages/aspose-pdf-tutorial-insert-a-blank-page-and-update-bates-num/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}