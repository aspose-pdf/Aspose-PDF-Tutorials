---
category: general
date: 2026-02-28
description: Criar documento PDF em C# com numeração Bates. Aprenda como adicionar
  numeração Bates ao PDF, definir prefixos e gerar números sequenciais de PDF em um
  único tutorial.
draft: false
keywords:
- create pdf document c#
- add bates numbering pdf
- how to add bates
- add document identification numbers
- add sequential pdf numbers
language: pt
og_description: Criar documento PDF em C# com numeração Bates. Este tutorial mostra
  como adicionar numeração Bates ao PDF, definir prefixos personalizados e gerar números
  sequenciais no PDF.
og_title: Criar documento PDF em C# – Adicionar numeração Bates
tags:
- Aspose.PDF
- C#
- PDF automation
title: Criar documento PDF C# – Guia de numeração Bates
url: /pt/net/document-creation/create-pdf-document-c-add-bates-numbering-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar Documento PDF C# – Guia de Numeração Bates

Já se perguntou como **criar PDF document C#** que já contenha um identificador único em cada página? Esse é um ponto crítico quando você precisa rastrear arquivos legais, petições judiciais ou qualquer lote de PDFs que deve ser pesquisável por número. A boa notícia? Com Aspose.PDF você pode adicionar números Bates em apenas algumas linhas de código — sem necessidade de edição manual.

Neste guia vamos percorrer todo o processo: carregar um PDF existente, configurar **add bates numbering pdf**, aplicar os números e, por fim, salvar o resultado. Ao final, você será capaz de **add document identification numbers** e até mesmo **add sequential PDF numbers** automaticamente, tudo em C#.

## Pré‑requisitos

- .NET 6.0 ou superior (a API também funciona com .NET Framework 4.5+)
- Uma cópia licenciada do **Aspose.PDF for .NET** (a versão de avaliação gratuita serve para testes)
- Um arquivo PDF de entrada que você deseja numerar (vamos chamá‑lo de `input.pdf`)
- Visual Studio 2022 (ou qualquer IDE de sua preferência)

Nenhum pacote NuGet extra além do Aspose.PDF é necessário.

![Criar Documento PDF C# com numeração Bates](https://example.com/image.png "Criar Documento PDF C# exemplo")

## Etapa 1: Carregar o Documento PDF de Origem

Antes de poder **add bates numbering pdf**, você precisa de um objeto `Document` que represente o arquivo no disco.

```csharp
using Aspose.Pdf;

// Load the source PDF document
var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");
```

*Por que isso importa*: A classe `Document` é o ponto de entrada para toda operação no Aspose.PDF. Ela abstrai o sistema de arquivos, permitindo que você trabalhe com páginas, anotações e metadados sem tocar nos bytes brutos.

> **Dica profissional:** Se você estiver processando muitos arquivos em um loop, reutilize a mesma instância de `Document` apenas quando a origem for idêntica; caso contrário, crie um novo objeto para cada arquivo para evitar vazamentos de memória.

## Etapa 2: Definir as Opções de Numeração Bates

É aqui que a parte **how to add bates** se torna concreta. Você configura um objeto `BatesNumberingOptions` para dizer ao Aspose qual deve ser o prefixo, onde iniciar e qual o tamanho da fonte.

```csharp
// Define Bates numbering options (prefix, start number, font size)
var batesOptions = new BatesNumberingOptions
{
    Prefix = "ABC-",   // You can change this to any string you need
    Start = 1000,      // Starting number – useful for continuous numbering across batches
    FontSize = 9       // Small enough to fit in the margin but still readable
};
```

*Por que isso importa*: O `Prefix` permite incorporar um identificador de caso (ex.: “ABC-”). A propriedade `Start` é essencial quando você está **adding sequential PDF numbers** em vários documentos — basta incrementá‑la. E `FontSize` garante que os números não obstruam o conteúdo existente.

## Etapa 3: Aplicar a Numeração Bates ao Documento Inteiro

Agora realmente estampamos os números em cada página. A classe `BatesNumbering` faz todo o trabalho pesado.

```csharp
// Apply Bates numbering to the entire document
var bates = new BatesNumbering();
bates.AddBatesNumbering(pdfDocument, batesOptions);
```

*Por que isso importa*: Nos bastidores, o Aspose percorre cada página, calcula o número apropriado (Prefix + (Start + pageIndex)) e o desenha no canto inferior‑direito por padrão. Você pode personalizar a posição depois, mas o padrão funciona para a maioria dos documentos de estilo jurídico.

> **Pergunta comum:** *E se eu precisar numerar apenas um subconjunto de páginas?*  
> Use a sobrecarga `AddBatesNumbering(Document, BatesNumberingOptions, int startPage, int endPage)` para limitar o intervalo.

## Etapa 4: Salvar o PDF com a Numeração Bates Aplicada

O passo final é gravar o documento modificado de volta ao disco.

```csharp
// Save the PDF with Bates numbers applied
pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
```

*Por que isso importa*: O método `Save` respeita o formato original do arquivo, de modo que você obtém um PDF padrão que qualquer visualizador pode abrir — completo com **add document identification numbers** em cada página.

## Exemplo Completo Funcional

Juntando tudo, aqui está um programa autônomo que você pode colar em um novo aplicativo console e executar imediatamente.

```csharp
using System;
using Aspose.Pdf;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the source PDF document
            var inputPath = @"YOUR_DIRECTORY/input.pdf";
            var pdfDocument = new Document(inputPath);

            // 2️⃣ Define Bates numbering options (prefix, start number, font size)
            var batesOptions = new BatesNumberingOptions
            {
                Prefix = "ABC-",
                Start = 1000,
                FontSize = 9
            };

            // 3️⃣ Apply Bates numbering to the entire document
            var bates = new BatesNumbering();
            bates.AddBatesNumbering(pdfDocument, batesOptions);

            // 4️⃣ Save the PDF with Bates numbers applied
            var outputPath = @"YOUR_DIRECTORY/output.pdf";
            pdfDocument.Save(outputPath);

            Console.WriteLine($"Bates numbering added successfully. Output saved to {outputPath}");
        }
    }
}
```

**Resultado esperado:** Abra `output.pdf` em qualquer visualizador; você verá “ABC‑1000”, “ABC‑1001”, … impressos no canto inferior‑direito de cada página. Os números são texto selecionável, portanto são pesquisáveis e podem ser copiados — exatamente o que se espera de uma implementação correta de **add sequential PDF numbers**.

## Casos Limite & Variações

### Posicionamento Personalizado

Se o canto padrão colidir com rodapés existentes, você pode deslocar a colocação:

```csharp
batesOptions.Position = new Position(10, 10); // X, Y from the bottom‑left
```

### Formatos de Número Diferentes

Quer números com preenchimento de zeros (ex.: 001000)? Use `NumberFormat`:

```csharp
batesOptions.NumberFormat = "D6"; // Pads to 6 digits
```

### Vários Arquivos em Lote

Ao processar muitos PDFs, mantenha um contador em execução:

```csharp
int globalStart = 5000;
foreach (var file in Directory.GetFiles(@"YOUR_DIRECTORY\Batch", "*.pdf"))
{
    var doc = new Document(file);
    var opts = new BatesNumberingOptions
    {
        Prefix = "BATCH-",
        Start = globalStart,
        FontSize = 9
    };
    new BatesNumbering().AddBatesNumbering(doc, opts);
    doc.Save(Path.ChangeExtension(file, ".bated.pdf"));
    globalStart += doc.Pages.Count; // Increment for the next file
}
```

### Manipulando PDFs Protegidos por Senha

Se o PDF de origem estiver criptografado, passe a senha ao criar o `Document`:

```csharp
var pdfDocument = new Document("protected.pdf", new LoadOptions { Password = "mySecret" });
```

## Perguntas Frequentes

| Pergunta | Resposta |
|----------|----------|
| **Posso usar outra biblioteca?** | Sim, bibliotecas como iTextSharp ou PdfSharp também suportam inserção de texto em nível de página, mas o Aspose.PDF oferece a API mais direta para numeração Bates. |
| **Isso afeta o tamanho do arquivo?** | Adicionar alguns bytes de texto por página é insignificante; o tamanho de saída normalmente cresce menos de 1 KB por página. |
| **A numeração é pesquisável?** | Absolutamente. O Aspose grava os números como objetos de texto, não como imagens, portanto são indexados pelos leitores de PDF. |
| **E se eu precisar de uma fonte diferente?** | Defina `batesOptions.Font` para um objeto `Font` (ex.: `FontRepository.FindFont("Arial")`). |

## Conclusão

Acabamos de demonstrar como **create PDF document C#** e instantaneamente **add bates numbering pdf** usando Aspose.PDF. O processo é simples, confiável e totalmente programável — perfeito para escritórios de advocacia, agências governamentais ou qualquer organização que precise **add document identification numbers** e **add sequential PDF numbers** a grandes lotes de arquivos.

Pegue essa base e experimente: teste diferentes prefixos para departamentos distintos, encadeie a numeração entre vários arquivos ou incorpore códigos QR ao lado dos números Bates para rastreabilidade extra. O céu é o limite quando você tem o fluxo de trabalho principal bem definido.

Se este tutorial foi útil, compartilhe, deixe um comentário ou explore nossos outros guias sobre manipulação de PDF com C#. Boa codificação!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}