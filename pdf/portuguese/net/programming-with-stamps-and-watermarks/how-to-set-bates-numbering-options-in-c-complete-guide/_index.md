---
category: general
date: 2026-08-14
description: Como definir opções de numeração Bates em C# usando o GroupDocs. Siga
  este tutorial passo a passo para adicionar prefixos personalizados e números iniciais
  ao converter Word para PDF.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to set bates numbering options
- Bates numbering C#
- GroupDocs API
- document conversion C#
- AddBatesNumbering method
- C# PDF generation
language: pt
lastmod: 2026-08-14
og_description: Como definir opções de numeração Bates rapidamente em C#. Este guia
  mostra como adicionar prefixos personalizados e números iniciais ao converter Word
  para PDF.
og_image_alt: Screenshot of C# code applying Bates numbering to a PDF
og_title: Como definir opções de numeração Bates em C# – tutorial passo a passo
schemas:
- author: GroupDocs
  dateModified: '2026-08-14'
  description: How to set bates numbering options in C# using GroupDocs. Follow this
    step‑by‑step tutorial to add custom prefixes and start numbers when converting
    Word to PDF.
  headline: How to set bates numbering options in C# – complete guide
  type: TechArticle
- description: How to set bates numbering options in C# using GroupDocs. Follow this
    step‑by‑step tutorial to add custom prefixes and start numbers when converting
    Word to PDF.
  name: How to set bates numbering options in C# – complete guide
  steps:
  - name: '`Document` – loads the source file.'
    text: '`Document` – loads the source file.'
  - name: '`BatesNumberingOptions` – holds the start number, prefix, and other formatting
      details.'
    text: '`BatesNumberingOptions` – holds the start number, prefix, and other formatting
      details.'
  - name: '`AddBatesNumbering` – the method that injects the numbering into each page.'
    text: '`AddBatesNumbering` – the method that injects the numbering into each page.'
  type: HowTo
tags:
- Bates numbering
- C#
- .NET
- GroupDocs
- PDF conversion
title: Como definir opções de numeração Bates em C# – guia completo
url: /pt/net/programming-with-stamps-and-watermarks/how-to-set-bates-numbering-options-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como definir opções de numeração Bates em C# – guia completo

Se você precisa **como definir opções de numeração Bates** em C#, este guia o conduz pelos passos exatos. Você aprenderá a configurar o número inicial, adicionar um prefixo e aplicar a numeração ao converter um documento Word para PDF usando a API GroupDocs.

O processamento de documentos costuma exigir identificadores únicos em cada página para fins legais ou de arquivamento. Ao final deste tutorial você terá um trecho reutilizável que pode ser inserido em qualquer projeto .NET, seja para criar uma ferramenta de suporte a litígios ou um gerador de relatórios automatizado. Nenhuma ferramenta externa é necessária — apenas a biblioteca GroupDocs.Conversion e algumas linhas de C#.

## O que você precisará

Antes de começar, certifique‑se de que tem:

* .NET 6.0 SDK ou versão posterior instalada  
* Visual Studio 2022 (ou qualquer IDE que suporte .NET)  
* Uma licença válida do GroupDocs.Conversion (a avaliação gratuita funciona para testes)  
* Um documento Word de exemplo (`input.docx`) que você deseja numerar  

Esses pré‑requisitos garantem que o código seja executado sem configurações adicionais.

## Como definir opções de numeração Bates – visão geral

O núcleo de **como definir opções de numeração Bates** está em três objetos:

1. `Document` – carrega o arquivo de origem.  
2. `BatesNumberingOptions` – contém o número inicial, o prefixo e outros detalhes de formatação.  
3. `AddBatesNumbering` – o método que insere a numeração em cada página.

Entender por que cada componente existe ajuda a adaptar a solução a cenários mais complexos, como fontes personalizadas ou numeração multilíngue.

## Etapa 1: Instalar o pacote NuGet GroupDocs.Conversion

Abra um terminal na pasta da sua solução e execute:

```bash
dotnet add package GroupDocs.Conversion
```

A **GroupDocs API** fornece a classe `Document` e o método de extensão `AddBatesNumbering` usados mais adiante no tutorial.

## Etapa 2: Carregar o documento de origem

```csharp
using GroupDocs.Conversion;
using GroupDocs.Conversion.Options.Convert;

// Step 2: Load the source Word document
Document document = new Document(@"C:\Docs\input.docx");
```

*Por que esta etapa?*  
Carregar o arquivo cria uma representação em memória que o motor de conversão pode manipular. Sem uma instância de `Document` você não pode aplicar a numeração Bates nem qualquer outra transformação.

## Etapa 3: Criar as opções de numeração Bates

```csharp
// Step 3: Configure Bates numbering
BatesNumberingOptions batesOptions = new BatesNumberingOptions
{
    // The first page will be numbered 1000
    StartNumber = 1000,
    // Each page will be prefixed with "CASE-"
    Prefix = "CASE-",
    // Optional: set the number format (e.g., 4 digits)
    NumberFormat = "#0000",
    // Optional: choose where the number appears (header/footer)
    Position = BatesNumberingPosition.FooterRight
};
```

*Por que esta etapa?*  
`BatesNumberingOptions` encapsula todas as configurações necessárias ao **definir opções de numeração Bates**. Ajustar `StartNumber` e `Prefix` permite alinhar a saída ao seu sistema de gerenciamento de casos. A propriedade `Position` controla a colocação visual, que frequentemente é um requisito de conformidade.

## Etapa 4: Aplicar a numeração Bates ao documento

```csharp
// Step 4: Apply the numbering to every page
document.AddBatesNumbering(batesOptions);
```

O método `AddBatesNumbering` percorre cada página do `Document` carregado e insere a string configurada. Como o método atua sobre a representação em memória, você pode encadear etapas adicionais de processamento (por exemplo, marca d’água) antes de salvar.

## Etapa 5: Converter e salvar o resultado como PDF

```csharp
// Step 5: Define PDF conversion options (optional)
PdfConvertOptions pdfOptions = new PdfConvertOptions
{
    // Preserve original layout
    EmbedStandardFonts = true
};

// Save the numbered document as PDF
document.Save(@"C:\Docs\output.pdf", pdfOptions);
```

*Por que esta etapa?*  
Salvar como PDF é um formato final comum para documentos legais. O objeto `PdfConvertOptions` permite ajustar a saída, mas não é obrigatório para a numeração básica. A chamada `Save` grava o PDF totalmente numerado no disco.

## Exemplo completo e executável

Juntando tudo, segue um aplicativo de console autocontido que você pode compilar e executar:

```csharp
using System;
using GroupDocs.Conversion;
using GroupDocs.Conversion.Options.Convert;
using GroupDocs.Conversion.Options.Convert.Pdf;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Load the source Word document
            Document document = new Document(@"C:\Docs\input.docx");

            // Configure Bates numbering options
            BatesNumberingOptions batesOptions = new BatesNumberingOptions
            {
                StartNumber = 1000,
                Prefix = "CASE-",
                NumberFormat = "#0000",
                Position = BatesNumberingPosition.FooterRight
            };

            // Apply numbering to each page
            document.AddBatesNumbering(batesOptions);

            // Optional: set PDF conversion preferences
            PdfConvertOptions pdfOptions = new PdfConvertOptions
            {
                EmbedStandardFonts = true
            };

            // Save the numbered PDF
            document.Save(@"C:\Docs\output.pdf", pdfOptions);

            Console.WriteLine("Bates numbering applied successfully. Output saved to output.pdf");
        }
    }
}
```

**Saída esperada**

Ao executar o programa, ele cria `output.pdf` onde cada página exibe um rótulo como `CASE-1000`, `CASE-1001` etc., posicionado no rodapé direito. Abra o PDF em qualquer visualizador para confirmar que os números aparecem como esperado.

## Armadilhas comuns e boas práticas

| Problema | Por que acontece | Como evitar |
|----------|------------------|--------------|
| **Caminhos relativos causam `FileNotFoundException`** | O diretório de trabalho de um aplicativo console pode ser diferente do do Visual Studio. | Use caminhos absolutos ou `Path.Combine(AppContext.BaseDirectory, "input.docx")`. |
| **Numeração sobrepõe rodapés existentes** | Se o documento de origem já contém conteúdo na área de rodapé escolhida, o novo número pode ficar oculto. | Escolha um `Position` diferente (ex.: `HeaderLeft`) ou ajuste o modelo de origem. |
| **Documentos grandes são lentos** | A numeração Bates itera sobre cada página; o uso de memória cresce com o tamanho do arquivo. | Processar o documento em blocos usando `Document.Split` se ultrapassar 500 páginas. |
| **Expiração da licença** | A avaliação gratuita do GroupDocs expira após 30 dias, gerando exceção ao chamar `AddBatesNumbering`. | Aplique uma chave de licença válida antes de carregar o documento: `License license = new License(); license.SetLicense("license.lic");`. |

**Dica profissional:** Se precisar de um formato de número diferente por caso (ex.: `2023-CASE-001`), construa o prefixo dinamicamente antes de criar o `BatesNumberingOptions`.

## Expandindo a solução

A mesma abordagem **Bates numbering C#** funciona com outros formatos de origem, como `.txt`, `.html` ou até imagens. Basta alterar a extensão do arquivo ao instanciar o objeto `Document`, e o motor de conversão cuidará do resto.

Você também pode combinar **document conversion C#** com OCR para PDFs escaneados:

```csharp
// Example: add OCR before numbering (requires GroupDocs.Viewer)
using GroupDocs.Viewer;
using GroupDocs.Viewer.Options;

Document scannedPdf = new Document(@"C:\Docs\scanned.pdf");
var viewer = new Viewer(scannedPdf);
var viewOptions = new HtmlViewOptions();
viewer.View(viewOptions); // OCR step
// Then apply Bates numbering as shown earlier
```

## Conclusão

Agora você sabe **como definir opções de numeração Bates** em C# do início ao fim. Criando um objeto `BatesNumberingOptions`, aplicando‑o com `AddBatesNumbering` e salvando o resultado como PDF, você pode automatizar a produção de documentos legalmente compatíveis e identificados de forma única.  

A partir daqui, explore tópicos relacionados como **geração de PDF em C#**, **conversão de documentos C#** ou recursos avançados da **GroupDocs API**, como marca d’água e assinaturas digitais. Experimente diferentes prefixos, posições e formatos de número para adequar ao seu fluxo de trabalho.

Happy coding!

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas em seus próprios projetos.

- [Add Bates Numbering PDF in C# – Complete Guide](/pdf/english/net/programming-with-stamps-and-watermarks/add-bates-numbering-pdf-in-c-complete-guide/)
- [How to Add and Customize Page Numbers in PDFs Using Aspose.PDF for .NET | Document Manipulation Guide](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [How to Add a Text Stamp Footer in PDFs Using Aspose.PDF for .NET&#58; A Step‑By‑Step Guide](/pdf/english/net/document-manipulation/add-text-stamp-footer-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}