---
category: general
date: 2026-06-08
description: Adicionar numeração Bates em PDF usando Aspose.Pdf em C#. Aprenda como
  adicionar Bates, adicionar números de página em PDF, adicionar números sequenciais
  em PDF e veja um exemplo de número Bates em PDF.
draft: false
keywords:
- add bates numbering pdf
- how to add bates
- add page numbers pdf
- add sequential numbers pdf
- bates number pdf example
language: pt
og_description: Adicionar numeração Bates em PDF no C#. Este tutorial mostra como
  adicionar Bates, inserir números de página em PDF e acrescentar números sequenciais
  em PDF, com um exemplo completo de numeração Bates em PDF.
og_title: Adicionar Numeração Bates em PDF – Guia Completo com Aspose
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Add bates numbering pdf using Aspose.Pdf in C#. Learn how to add bates,
    add page numbers pdf, add sequential numbers pdf, and see a bates number pdf example.
  headline: Add Bates Numbering PDF – Complete Guide with Aspose
  type: TechArticle
- description: Add bates numbering pdf using Aspose.Pdf in C#. Learn how to add bates,
    add page numbers pdf, add sequential numbers pdf, and see a bates number pdf example.
  name: Add Bates Numbering PDF – Complete Guide with Aspose
  steps:
  - name: Install the Aspose.Pdf NuGet Package
    text: 'First, add the library to your project. Open the Package Manager Console
      and run:'
  - name: Open the Source PDF Document
    text: Now we load the PDF we want to stamp. The `using` statement ensures the
      file is closed properly even if an exception occurs.
  - name: Create a Bates Numbering Facade
    text: 'The *facade* pattern hides the complexity of the underlying PDF structure.
      Here’s how we instantiate it:'
  - name: Configure the Starting Number and Prefix
    text: Bates numbers often include a case‑specific prefix. You can also control
      the number of digits, the separator, and the placement on the page.
  - name: Apply the Bates Numbering to the Document
    text: 'With the facade configured, we now stamp every page:'
  - name: Save the Modified PDF
    text: 'Finally, write the output to disk:'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF processing
title: Adicionar Numeração Bates ao PDF – Guia Completo com Aspose
url: /pt/net/programming-with-stamps-and-watermarks/add-bates-numbering-pdf-complete-guide-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Adicionar Numeração Bates em PDF – Guia Completo de Programação

Já precisou **adicionar numeração bates pdf** mas não sabia por onde começar? Se você já se perguntou *como adicionar bates* a um documento jurídico, está no lugar certo. Neste tutorial vamos percorrer um exemplo prático, de ponta a ponta, que não só adiciona números Bates, mas também mostra como **adicionar números de página pdf**, **adicionar números sequenciais pdf**, e ainda fornece um **exemplo de número bates pdf** pronto para execução.

Usaremos a biblioteca Aspose.Pdf para .NET, porque ela abstrai os detalhes internos de PDF de baixo nível enquanto lhe dá controle granular. Ao final deste guia você terá um trecho reutilizável que pode ser inserido em qualquer projeto C#, e entenderá por que cada linha é importante.

## O que você precisará

- **.NET 6.0** ou superior (o código também funciona no .NET Framework 4.6+).  
- Uma **licença** para Aspose.Pdf ou uma chave de avaliação temporária gratuita.  
- Um PDF de exemplo chamado `input.pdf` colocado em uma pasta que você possa referenciar.  
- Visual Studio, Rider ou qualquer editor C# de sua preferência.

É só isso — sem ferramentas extras, sem acrobacias de linha de comando. Pronto? Vamos mergulhar.

## Adicionar Numeração Bates PDF – Implementação Passo a Passo

A seguir dividimos o processo em seis etapas lógicas. Cada etapa inclui um pequeno trecho de código, uma explicação do *porquê* fazemos isso, e uma dica que pode ser útil.

### Etapa 1: Instalar o Pacote NuGet Aspose.Pdf

Primeiro, adicione a biblioteca ao seu projeto. Abra o Console do Gerenciador de Pacotes e execute:

```powershell
Install-Package Aspose.Pdf
```

> **Dica profissional:** Se você estiver usando .NET Core, também pode usar `dotnet add package Aspose.Pdf`.

Instalar o pacote lhe dá acesso à classe `Aspose.Pdf.Facades.BatesNumbering`, que é a responsável por **add bates numbering pdf**.

### Etapa 2: Abrir o Documento PDF Fonte

Agora carregamos o PDF que queremos carimbar. A instrução `using` garante que o arquivo seja fechado corretamente mesmo se ocorrer uma exceção.

```csharp
using (var doc = new Aspose.Pdf.Document(@"C:\MyPdfs\input.pdf"))
{
    // All further steps happen inside this block.
}
```

Por que usar `Aspose.Pdf.Document`? Ela representa todo o PDF na memória, permitindo manipular páginas, fontes e metadados sem tocar no arquivo original no disco.

### Etapa 3: Criar um Facade de Numeração Bates

O padrão *facade* oculta a complexidade da estrutura subjacente do PDF. Veja como instanciamos:

```csharp
var bates = new Aspose.Pdf.Facades.BatesNumbering();
```

Este objeto será configurado posteriormente com um prefixo, número inicial e opções de formatação. Pense nele como o “motor” que **add page numbers pdf** de forma compatível com Bates.

### Etapa 4: Configurar o Número Inicial e o Prefixo

Números Bates costumam incluir um prefixo específico do caso. Você também pode controlar a quantidade de dígitos, o separador e a posição na página.

```csharp
bates.StartNumber = 1000;          // First number in the sequence
bates.Prefix = "CASE-";            // Prefix that appears before each number
bates.NumberOfDigits = 5;          // Pads numbers with leading zeros (e.g., 01000)
bates.Separator = "-";             // Optional separator between prefix and number
bates.Location = new Aspose.Pdf.Rectangle(0, 0, 200, 20); // Bottom‑left corner
bates.FontSize = 12;
bates.FontColor = System.Drawing.Color.Blue;
```

**Por que essas configurações?**  
- `StartNumber` permite continuar uma série anterior.  
- `NumberOfDigits` garante comprimento uniforme, o que é crucial para indexação jurídica.  
- `Location` define onde o **add sequential numbers pdf** aparecerá; você pode movê‑lo para o canto superior‑direito se preferir.

### Etapa 5: Aplicar a Numeração Bates ao Documento

Com o facade configurado, agora carimbamos cada página:

```csharp
bates.AddBatesNumbering(doc);
```

Nos bastidores, o Aspose itera por cada página, desenha o texto na localização especificada e respeita qualquer conteúdo existente. Esta única linha é o que realmente **add bates numbering pdf** ao seu arquivo.

### Etapa 6: Salvar o PDF Modificado

Por fim, escreva a saída no disco:

```csharp
doc.Save(@"C:\MyPdfs\output.pdf");
```

Agora você tem um PDF onde cada página contém um identificador Bates único, pronto para descoberta ou submissão em tribunal.

#### Exemplo Completo em Funcionamento (Exemplo de Número Bates PDF)

Juntando tudo, aqui está um programa completo, autocontido, que você pode compilar e executar:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Facades;
using System.Drawing; // For Color

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source PDF
        using (var doc = new Document(@"C:\MyPdfs\input.pdf"))
        {
            // 2️⃣ Create the Bates numbering facade
            var bates = new BatesNumbering();

            // 3️⃣ Configure prefix, start number, and formatting
            bates.StartNumber = 1000;
            bates.Prefix = "CASE-";
            bates.NumberOfDigits = 5;
            bates.Separator = "-";
            bates.Location = new Rectangle(0, 0, 200, 20); // Bottom‑left
            bates.FontSize = 12;
            bates.FontColor = Color.Blue;

            // 4️⃣ Apply the numbering to every page
            bates.AddBatesNumbering(doc);

            // 5️⃣ Save the result
            doc.Save(@"C:\MyPdfs\output.pdf");
        }

        Console.WriteLine("Bates numbering added successfully!");
    }
}
```

> **Saída esperada:** Abra `output.pdf` e você verá “CASE‑01000”, “CASE‑01001”, … no canto inferior‑esquerdo de cada página.

![Captura de tela de uma página PDF com números Bates no canto inferior‑esquerdo – exemplo de add bates numbering pdf](https://example.com/bates-numbering-screenshot.png "exemplo de add bates numbering pdf")

*(Texto alternativo da imagem: *exemplo de add bates numbering pdf* – mostra os números Bates aplicados a um PDF de exemplo.)*

## Como Adicionar Bates – Entendendo o Facade

Você pode se perguntar **como adicionar bates** sem o facade da Aspose. A alternativa seria desenhar texto manualmente em cada página usando operadores PDF de baixo nível, mas essa abordagem é propensa a erros e requer profundo conhecimento da especificação PDF. O facade abstrai esses detalhes, permitindo que você se concentre no *o que* deseja (um prefixo, um número inicial) ao invés do *como* renderizá‑lo.

Se precisar **add page numbers pdf** em um estilo não‑Bates (por exemplo, “Página 3 de 12”), pode reutilizar a mesma classe `BatesNumbering` — basta definir `Prefix` como uma string vazia e ajustar `Location`. O motor subjacente é o mesmo, o que significa renderização consistente em ambos os casos de uso.

## Adicionar Números de Página PDF – Personalizando Posicionamento e Estilo

Equipes jurídicas frequentemente solicitam o número da página no cabeçalho, enquanto o suporte de litígio prefere no rodapé. Aqui está um ajuste rápido:

```csharp
bates.Location = new Rectangle(0, doc.Pages[1].PageInfo.Height - 20, 200, 20); // Top‑right
bates.Prefix = "";               // No prefix for plain page numbers
bates.StartNumber = 1;           // Start from 1
bates.NumberOfDigits = 0;        // No padding
bates.FontColor = Color.Black;
```

A mesma chamada `AddBatesNumbering` agora **add page numbers pdf** no topo de cada página. Como o facade opera sobre o objeto documento, você pode alternar entre Bates e numeração simples de página com algumas mudanças de propriedade — sem precisar reescrever o loop.

## Adicionar Números Sequenciais PDF – Formatação Avançada

Suponha que você precise de um formato como `2023-CASE-00123`. Você pode combinar um prefixo de data com as configurações existentes:

```csharp
bates.Prefix = $"{DateTime.Now:yyyy}-CASE-";
bates.NumberOfDigits = 5;
bates.Separator = "-";
```

Agora cada página exibirá `2023-CASE-00123`, `2023-CASE-00124`, etc. Isso demonstra como é fácil **add sequential numbers pdf** que atendam a convenções de nomenclatura complexas.

## Casos Limite e Armadilhas Comuns

| Situação | O que observar | Correção sugerida |
|-----------|----------------------|---------------|
| **PDFs muito grandes ( > 500 MB )** | O consumo de memória pode disparar porque todo o documento é carregado na RAM. | Use `Document` com configurações de `MemoryManagement` ou processe o arquivo em blocos com `PdfFileEditor`. |
| **Números de página já existentes** | | |

## O que Você Deve Aprender a Seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [How to Add and Customize Page Numbers in PDFs Using Aspose.PDF for .NET | Document Manipulation Guide](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [How to Add Page Number Stamps in PDFs Using Aspose.PDF for .NET | Watermarks & Backgrounds](/pdf/english/net/watermarks-backgrounds/add-page-number-stamp-using-aspose-pdf-dotnet/)
- [Aspose.PDF .NET: Add Page Numbers to PDFs Using FloatingBox](/pdf/english/net/text-operations/aspose-pdf-net-floatingbox-page-numbering/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}