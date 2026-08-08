---
category: general
date: 2026-05-27
description: Adicionar numeração Bates a PDF usando Aspose.Pdf em C#. Aprenda como
  adicionar numeração Bates rapidamente, personalizar o formato e automatizar a marcação
  de documentos legais.
draft: false
keywords:
- add bates numbering pdf
- how to add bates numbering
language: pt
og_description: Adicionar numeração Bates a PDF com Aspose.Pdf em C#. Este guia mostra
  como adicionar numeração Bates, configurar prefixos e salvar o resultado.
og_title: Adicionar numeração Bates a PDF em C# – Tutorial passo a passo
schemas:
- author: Aspose
  dateModified: '2026-05-27'
  description: Add Bates numbering PDF using Aspose.Pdf in C#. Learn how to add Bates
    numbering quickly, customize format, and automate legal document tagging.
  headline: Add Bates Numbering PDF in C# – Complete Guide
  type: TechArticle
- description: Add Bates numbering PDF using Aspose.Pdf in C#. Learn how to add Bates
    numbering quickly, customize format, and automate legal document tagging.
  name: Add Bates Numbering PDF in C# – Complete Guide
  steps:
  - name: Expected Output
    text: 'When you run the program, the console prints:'
  - name: Can I position the Bates number elsewhere?
    text: Yes. Use the `BatesNumberingArtifact`’s `Location` property (e.g., `Location
      = new Position(10, 10)`) to place the number at custom X/Y coordinates. You
      can also set `HorizontalAlignment` and `VerticalAlignment` for more control.
  - name: What if my PDF has thousands of pages?
    text: Aspose.Pdf streams pages efficiently, but it’s still a good idea to process
      in batches if you hit memory limits. The `Document` class also supports `PdfConverter`
      for incremental saving.
  - name: How do I change the font or color?
    text: 'Wrap the artifact in a `TextState` object:'
  - name: Do I need a license for production use?
    text: A licensed version removes evaluation watermarks and unlocks full performance.
      The free trial works fine for testing and proof‑of‑concepts.
  type: HowTo
tags:
- Aspose.Pdf
- C#
- Bates numbering
- PDF automation
title: Adicionar numeração Bates em PDF com C# – Guia completo
url: /pt/net/programming-with-stamps-and-watermarks/add-bates-numbering-pdf-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Adicionar Numeração Bates a PDFs em C# – Guia Completo

Já se perguntou **como adicionar numeração Bates** a um PDF sem passar horas mexendo em ferramentas manuais? Você não está sozinho — equipes jurídicas, auditores e especialistas em e‑discovery precisam de uma forma confiável de **adicionar numeração Bates a arquivos PDF** programaticamente.  

Neste tutorial vamos percorrer uma solução concisa, de ponta a ponta, usando Aspose.Pdf para .NET, para que você possa inserir números Bates em qualquer documento com apenas algumas linhas de código C#.

## O que você vai aprender

- Como abrir um PDF existente com Aspose.Pdf  
- Como criar um artefato de numeração Bates e ajustar seu formato  
- Como anexar o artefato a cada página (ou apenas à primeira)  
- Como salvar o arquivo atualizado e verificar o resultado  

Não é necessário ter experiência prévia com Aspose — apenas um entendimento básico de C# e .NET. Ao final, você terá um snippet reutilizável que pode copiar‑colar em qualquer projeto.

## Pré‑requisitos

- .NET 6.0 ou superior (o código também funciona no .NET Framework 4.7+)  
- Pacote NuGet Aspose.Pdf for .NET (`Install-Package Aspose.Pdf`)  
- Um arquivo PDF de origem que você deseja marcar (coloque‑o em uma pasta que possa referenciar)

> **Dica de especialista:** Se ainda não tem uma licença, a Aspose oferece uma chave temporária gratuita que remove as marcas d'água de avaliação.

## Etapa 1 – Abrir o documento PDF de origem  

Primeiro precisamos de um objeto `Document` que represente o arquivo no disco. Pense nisso como carregar uma tela em branco na qual pintaremos os números Bates depois.

```csharp
using Aspose.Pdf;
using System;

class Program
{
    static void Main()
    {
        // Adjust the path to point at your source PDF
        string sourcePath = @"C:\Docs\source.pdf";

        // Load the PDF – this is where we start to add Bates numbering
        using (var pdfDocument = new Document(sourcePath))
        {
            // The rest of the logic lives inside this using block
        }
    }
}
```

**Por que isso importa:** Abrir o documento dentro de um bloco `using` garante que todos os recursos não gerenciados sejam liberados rapidamente, o que é especialmente importante para PDFs grandes.

## Etapa 2 – Criar um artefato de Numeração Bates  

Um *BatesNumberingArtifact* é a forma que a Aspose usa para descrever como os números devem aparecer. Você pode definir um prefixo, número inicial, incremento e até uma string de formato personalizada.

```csharp
// Step 2: Define the Bates numbering artifact
var batesNumbering = new BatesNumberingArtifact
{
    Prefix = "ABC",            // Text that appears before each number
    StartNumber = 1000,        // First number in the sequence
    Increment = 1,             // Step between consecutive numbers
    Format = "{0:D5}"          // Zero‑padded 5‑digit number (e.g., 01000)
};
```

**Por que você pode querer mudar esses valores:**  
- **Prefix** é útil para IDs de caso (“CASE‑”, “DOC‑”).  
- **StartNumber** permite continuar uma série anterior.  
- **Increment** pode ser definido como 2 se precisar de numeração ímpar/par.  
- **Format** aceita qualquer formato composto .NET; `{0:D5}` garante cinco dígitos com zeros à esquerda.

## Etapa 3 – Anexar o artefato às páginas desejadas  

Você pode adicionar o artefato a uma única página, a um intervalo ou a todo o documento. Na maioria dos fluxos de trabalho jurídicos o anexamos a *todas* as páginas, mas o exemplo abaixo mostra o caso mínimo — adicioná‑lo à primeira página.

```csharp
// Step 3: Attach the artifact to the first page (index is 1‑based)
pdfDocument.Pages[1].Artifacts.Add(batesNumbering);
```

Se precisar cobrir todas as páginas, faça um loop sobre elas:

```csharp
foreach (Page page in pdfDocument.Pages)
{
    page.Artifacts.Add(batesNumbering);
}
```

**Por que esta etapa é crucial:** Os artefatos são renderizados *depois* do conteúdo da página, então os números aparecem sobre o texto existente sem alterar o layout original.

## Etapa 4 – Salvar o PDF modificado  

Por fim, grave as alterações de volta ao disco. Você pode sobrescrever o original ou criar um novo arquivo — aqui vamos gerar uma cópia chamada `bates.pdf`.

```csharp
// Step 4: Persist the changes
string outputPath = @"C:\Docs\bates.pdf";
pdfDocument.Save(outputPath);

Console.WriteLine($"Bates numbering added successfully. File saved to: {outputPath}");
```

Ao abrir `bates.pdf` você verá “ABC01000” (ou o formato que escolheu) estampado na localização padrão — geralmente no canto inferior‑direito.

## Exemplo completo funcionando  

Juntando tudo, aqui está o programa completo que você pode compilar e executar:

```csharp
using Aspose.Pdf;
using System;

class AddBatesNumbering
{
    static void Main()
    {
        // -----------------------------------------------------------------
        // 1️⃣ Open the source PDF
        // -----------------------------------------------------------------
        string sourcePath = @"C:\Docs\source.pdf";
        using (var pdfDocument = new Document(sourcePath))
        {
            // -----------------------------------------------------------------
            // 2️⃣ Create and configure the Bates numbering artifact
            // -----------------------------------------------------------------
            var batesNumbering = new BatesNumberingArtifact
            {
                Prefix = "ABC",
                StartNumber = 1000,
                Increment = 1,
                Format = "{0:D5}"
            };

            // -----------------------------------------------------------------
            // 3️⃣ Attach the artifact to each page (or a specific page)
            // -----------------------------------------------------------------
            foreach (Page page in pdfDocument.Pages)
            {
                page.Artifacts.Add(batesNumbering);
            }

            // -----------------------------------------------------------------
            // 4️⃣ Save the new PDF
            // -----------------------------------------------------------------
            string outputPath = @"C:\Docs\bates.pdf";
            pdfDocument.Save(outputPath);

            Console.WriteLine($"Bates numbers added. Output: {outputPath}");
        }
    }
}
```

### Saída esperada

Ao executar o programa, o console exibe:

```
Bates numbers added. Output: C:\Docs\bates.pdf
```

Abrir `bates.pdf` mostra o prefixo “ABC” seguido de uma sequência de cinco dígitos preenchidos com zero em cada página — exatamente o que o código foi escrito para fazer.

## Perguntas frequentes & casos especiais

### Posso posicionar o número Bates em outro lugar?

Sim. Use a propriedade `Location` do `BatesNumberingArtifact` (por exemplo, `Location = new Position(10, 10)`) para colocar o número em coordenadas X/Y personalizadas. Também é possível definir `HorizontalAlignment` e `VerticalAlignment` para maior controle.

### E se meu PDF tiver milhares de páginas?

Aspose.Pdf faz streaming das páginas de forma eficiente, mas ainda é recomendável processar em lotes caso atinja limites de memória. A classe `Document` também oferece suporte ao `PdfConverter` para salvamento incremental.

### Como mudar a fonte ou a cor?

Envolva o artefato em um objeto `TextState`:

```csharp
batesNumbering.TextState = new TextState
{
    FontSize = 12,
    Font = FontRepository.FindFont("Arial"),
    ForegroundColor = Color.FromRgb(255, 0, 0) // red
};
```

### Preciso de licença para uso em produção?

Uma versão licenciada remove as marcas d'água de avaliação e desbloqueia desempenho total. O trial gratuito funciona bem para testes e provas de conceito.

## Verificação – Checagem visual rápida  

Se preferir uma verificação automatizada, a Aspose pode extrair o texto de uma página e confirmar a presença do prefixo:

```csharp
string pageText = pdfDocument.Pages[1].ExtractText();
bool hasBates = pageText.Contains("ABC01000");
Console.WriteLine(hasBates ? "Bates number verified." : "Number missing!");
```

Executar isso após a etapa de salvamento imprimirá `Bates number verified.` se tudo correr bem.

## Conclusão  

Agora você sabe **como adicionar numeração Bates a arquivos PDF** usando Aspose.Pdf em C#. Desde a abertura do documento até a configuração do artefato, sua anexação às páginas e o salvamento do resultado, o processo é simples e totalmente scriptável.  

Próximos passos? Experimente:

- Valores diferentes de `Prefix` para múltiplos lotes de casos  
- `Location` e `TextState` personalizados para branding  
- Prefixos específicos por página (por exemplo, “VOL‑1‑”, “VOL‑2‑”) ajustando `StartNumber` a cada iteração do loop  

Essas adaptações permitem que você ajuste a solução a praticamente qualquer fluxo de trabalho jurídico ou de arquivamento.  

Tem mais perguntas sobre **como adicionar numeração Bates** para PDFs multilíngues ou arquivos criptografados? Deixe um comentário abaixo e feliz codificação!

## Tutoriais relacionados

- [How to Add and Customize Page Numbers in PDFs Using Aspose.PDF for .NET | Document Manipulation Guide](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [How to Add Different Headers in PDF Using Aspose.PDF for .NET&#58; A Step-by-Step Guide](/pdf/english/net/document-manipulation/add-different-headers-aspose-pdf-net/)
- [How to Add a Text Stamp Footer in PDFs Using Aspose.PDF for .NET&#58; A Step-by-Step Guide](/pdf/english/net/document-manipulation/add-text-stamp-footer-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}