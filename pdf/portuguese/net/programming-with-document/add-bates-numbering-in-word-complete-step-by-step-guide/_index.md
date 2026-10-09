---
category: general
date: 2026-06-21
description: Adicione numeração Bates no Word rapidamente. Aprenda como adicionar
  Bates, aplicar numeração Bates em documentos jurídicos e automatizar a numeração
  com C#.
draft: false
keywords:
- add bates numbering
- how to add bates
- bates numbering in word
- bates numbering for legal
- apply bates numbering
language: pt
og_description: Adicione numeração Bates no Word usando C#. Este guia mostra como
  adicionar Bates, aplicar numeração Bates em documentos legais e automatizar o processo.
og_title: Adicionar numeração Bates no Word – Guia completo de programação
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Add Bates numbering in Word quickly. Learn how to add Bates, apply
    Bates numbering for legal docs, and automate numbering with C#.
  headline: Add Bates Numbering in Word – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Add Bates numbering in Word quickly. Learn how to add Bates, apply
    Bates numbering for legal docs, and automate numbering with C#.
  name: Add Bates Numbering in Word – Complete Step‑by‑Step Guide
  steps:
  - name: Expected Output
    text: '| Page | Bates Number | |------|--------------| | 1 | ABC-1000 | | 2 |
      ABC-1001 | | … | … | | N | ABC‑(1000 + N‑1) |'
  - name: What if the document already contains page numbers?
    text: The `AddBatesNumbering` method will **not** overwrite existing page number
      fields; it simply adds a new field. If you want to replace the existing numbers,
      remove them first or set `batesOptions.Position` to the same location as the
      current page numbers.
  - name: Can I skip pages (e.g., exclude a cover page)?
    text: 'Yes. Use the overload that accepts a `PageRange`:'
  - name: How do I change the numbering format (Roman numerals, letters)?
    text: 'The `BatesNumberingOptions` class supports a `NumberFormat` property:'
  - name: What about performance on huge files?
    text: Loading a 2‑GB Word file can consume a lot of RAM. To mitigate, process
      the document in chunks using the `DocumentSplitter` utility, apply Bates numbering
      to each chunk, then merge the parts back together. This pattern keeps memory
      usage under control while still letting you **apply bates numbering*
  type: HowTo
tags:
- document‑automation
- csharp
- legal‑tech
title: Adicionar numeração Bates no Word – Guia completo passo a passo
url: /pt/net/programming-with-document/add-bates-numbering-in-word-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Adicionar Numeração Bates no Word – Guia Completo Passo a Passo

Já se perguntou como adicionar numeração Bates a um arquivo Word sem digitar cada número manualmente? Você não está sozinho. Muitos advogados, paralegais e especialistas em e‑discovery precisam de uma forma confiável de **adicionar numeração Bates** a centenas de páginas, e fazer isso à mão é um pesadelo.

Neste tutorial vamos percorrer uma solução limpa em C# que **aplica numeração Bates** a um arquivo `.docx`, explica por que cada linha importa e mostra como ajustar o código para necessidades específicas do setor jurídico. Ao final, você será capaz de gerar um documento perfeitamente numerado em segundos — sem plugins extras.

## O que você aprenderá

- O código exato necessário para **adicionar numeração Bates** a um documento Word.  
- Como a classe `BatesNumberingOptions` funciona e por que você pode ajustar o prefixo ou o valor inicial.  
- Dicas para usar essa abordagem em arquivos de caso grandes, incluindo considerações de memória.  
- Um resumo rápido dos pré‑requisitos para que você possa copiar‑colar a solução e executá‑la hoje.

**Pré‑requisitos**  
- .NET 6+ (ou .NET Framework 4.7.2+ se preferir o runtime mais antigo).  
- Uma referência à biblioteca Aspose.Words for .NET (ou qualquer API similar que exponha `AddBatesNumbering`).  
- Familiaridade básica com C# e Visual Studio (ou seu IDE favorito).

Se você está confortável com isso, vamos começar.

## Etapa 1: Configurar o Projeto e Importar a Biblioteca

Primeiro, crie um novo aplicativo console (ou integre em um serviço existente). Em seguida, adicione o pacote NuGet Aspose.Words:

```bash
dotnet add package Aspose.Words
```

> **Dica profissional:** Use a licença de avaliação gratuita para testes; ela adiciona uma pequena marca d'água, mas funciona exatamente como a versão completa.

```csharp
using Aspose.Words;
using Aspose.Words.BatesNumbering;
```

Essas instruções `using` trazem as classes `Document` e `BatesNumberingOptions` para o escopo, que são essenciais para a etapa de **aplicar numeração Bates** mais adiante.

## Etapa 2: Carregar o Documento de Origem

Você precisará de um arquivo Word para trabalhar. O código abaixo carrega `input.docx` a partir de uma pasta que você especificar. Substitua `"YOUR_DIRECTORY"` pelo caminho real na sua máquina.

```csharp
// Step 1: Load the source document
var document = new Document("YOUR_DIRECTORY/input.docx");
```

Por que carregar o arquivo primeiro? O objeto `Document` analisa todo o pacote Word na memória, permitindo que manipulemos cabeçalhos, rodapés e layout de página antes de salvar. Se o arquivo for massivo (pense em 10.000 páginas), considere usar `LoadOptions` com `LoadFormat.Docx` para transmitir seções em vez de carregar tudo de uma vez.

## Etapa 3: Configurar as Opções de Numeração Bates

É aqui que a mágica acontece. Você informa à biblioteca qual prefixo usar (`"ABC-"` no exemplo) e onde começar a contagem (`1000`). Ambos os valores são totalmente personalizáveis.

```csharp
// Step 2: Define Bates numbering options (prefix and starting number)
var batesOptions = new BatesNumberingOptions
{
    Prefix = "ABC-",
    Start = 1000,
    // Optional: set the position, alignment, and font if you need legal‑specific styling
    // Position = BatesNumberingPosition.Footer,
    // Alignment = BatesNumberingAlignment.Right,
    // Font = new Font("Times New Roman", 10, FontStyle.Bold)
};
```

**Por que um prefixo?** Na prática jurídica, os prefixos costumam identificar o caso ou a parte produtora (`"ABC-"` poderia representar *Acme Bank Corp.*). Começar em `1000` é comum porque muitas firmas reservam os primeiros 999 números para rascunhos internos.

Se você estiver lidando com **numeração Bates para documentos legais**, talvez queira também definir `batesOptions.Position` como `Header` ou `Footer` e ajustar o alinhamento para atender às regras do tribunal. A biblioteca oferece esses ajustes prontamente.

## Etapa 4: Aplicar Numeração Bates ao Documento Inteiro

Agora realmente inserimos os números. O método `AddBatesNumbering` percorre cada página, insere a string formatada e atualiza a contagem interna de páginas do documento.

```csharp
// Step 3: Apply Bates numbering to the entire document
document.AddBatesNumbering(batesOptions);
```

Nos bastidores, Aspose.Words cria um campo oculto em cada página que é renderizado como `ABC-1000`, `ABC-1001` e assim por diante. Como é um campo, você pode editar posteriormente o prefixo ou o número inicial sem precisar regenerar todo o arquivo — útil para **como adicionar Bates** após uma mudança de solicitação de descoberta.

## Etapa 5: Salvar o Documento Modificado

Por fim, escreva a saída em um novo arquivo. Manter o original intacto é uma prática recomendada, especialmente ao lidar com evidências que precisam permanecer impecáveis.

```csharp
// Step 4: Save the modified document
document.Save("YOUR_DIRECTORY/output.docx");
```

Agora você tem `output.docx` com números Bates sequenciais anexados a cada página. Abra-o no Word e verá os números exatamente onde especificou (rodapé por padrão). O tamanho do arquivo pode aumentar levemente por causa dos campos extras, mas isso é insignificante comparado aos benefícios.

### Saída Esperada

| Página | Número Bates |
|--------|--------------|
| 1      | ABC-1000     |
| 2      | ABC-1001     |
| …      | …            |
| N      | ABC‑(1000 + N‑1) |

Se você abrir a visualização “Códigos de Campo” do documento (`Alt+F9` no Word), verá algo como `{ BATES \* MERGEFORMAT ABC-1000 }` em cada página.

## Casos Limite e Perguntas Frequentes

### E se o documento já contiver números de página?

O método `AddBatesNumbering` **não** sobrescreve campos de número de página existentes; ele simplesmente adiciona um novo campo. Se quiser substituir os números atuais, remova-os primeiro ou defina `batesOptions.Position` para o mesmo local dos números de página atuais.

### Posso pular páginas (por exemplo, excluir a capa)?

Sim. Use a sobrecarga que aceita um `PageRange`:

```csharp
var range = new PageRange(2, document.PageCount); // start at page 2
document.AddBatesNumbering(batesOptions, range);
```

Isso é útil quando você precisa de **numeração Bates para documentos legais** que começam após uma página de título.

### Como mudar o formato da numeração (números romanos, letras)?

A classe `BatesNumberingOptions` suporta a propriedade `NumberFormat`:

```csharp
batesOptions.NumberFormat = BatesNumberFormat.RomanUpper;
```

Defina-a antes de chamar `AddBatesNumbering`. Essa flexibilidade ajuda quando um tribunal exige um estilo específico.

### E quanto ao desempenho em arquivos enormes?

Carregar um arquivo Word de 2 GB pode consumir muita RAM. Para mitigar, processe o documento em blocos usando a utilidade `DocumentSplitter`, aplique a numeração Bates a cada bloco e, em seguida, mescle as partes novamente. Esse padrão mantém o uso de memória sob controle enquanto ainda permite **aplicar numeração Bates** de forma eficiente.

## Exemplo Completo Funcional

Juntando tudo, aqui está um programa console pronto‑para‑executar:

```csharp
using System;
using Aspose.Words;
using Aspose.Words.BatesNumbering;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the source document
            var inputPath = @"C:\Docs\input.docx";
            var document = new Document(inputPath);

            // 2️⃣ Define Bates numbering options
            var batesOptions = new BatesNumberingOptions
            {
                Prefix = "ABC-",
                Start = 1000,
                // Optional styling for legal compliance
                Position = BatesNumberingPosition.Footer,
                Alignment = BatesNumberingAlignment.Right,
                Font = new Font("Times New Roman", 9, FontStyle.Bold)
            };

            // 3️⃣ Apply Bates numbering across all pages
            document.AddBatesNumbering(batesOptions);

            // 4️⃣ Save the result
            var outputPath = @"C:\Docs\output.docx";
            document.Save(outputPath);

            Console.WriteLine($"✅ Bates numbering applied! Saved to {outputPath}");
        }
    }
}
```

Execute o programa, abra `output.docx` e verá uma série limpa de números pronta para arquivamento, descoberta ou submissão ao tribunal.

## Conclusão

Agora você sabe exatamente **como adicionar Bates** a um documento Word usando C#. As etapas — carregar, configurar, aplicar e salvar — são diretas, porém flexíveis o suficiente para atender a **fluxos de trabalho de numeração Bates para o setor jurídico**, prefixos personalizados e até processamento em lote de grande escala.

Se quiser avançar, considere:

- Integrar o código a uma API web para que colegas possam fazer upload de arquivos e receber PDFs numerados instantaneamente.  
- Adicionar tratamento de erros para arquivos ausentes ou problemas de permissão (um rápido `try/catch` ao redor de `Document.Load`).  
- Explorar outros recursos do Aspose.Words, como marcas d'água ou redação, para um conjunto completo de ferramentas de e‑discovery.

Sinta‑se à vontade para experimentar diferentes prefixos, números iniciais ou até combinar múltiplos esquemas de numeração no mesmo documento. O mundo de **aplicar numeração Bates** é surpreendentemente versátil quando você tem a lógica central em mãos.

Tem perguntas ou um cenário complicado? Deixe um comentário abaixo e vamos solucionar juntos. Boa codificação!

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas de implementação em seus próprios projetos.

- [Apply Numbering Style in Heading of PDF using Java](/pdf/english/java/pdf-images/apply-numbering-style-in-heading-of-pdf-using-java/)
- [Apply Numbering Style In Heading Of Pdf Using Java](/pdf/german/java/pdf-images/apply-numbering-style-in-heading-of-pdf-using-java/)
- [Apply Numbering Style In Heading Of Pdf Using Java](/pdf/french/java/pdf-images/apply-numbering-style-in-heading-of-pdf-using-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}