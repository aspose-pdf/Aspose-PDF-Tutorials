---
category: general
date: 2026-08-04
description: Crie um novo documento PDF em C# e adicione numeração Bates ao PDF rapidamente
  usando Aspose.Pdf – aprenda a inserir página em branco no PDF e números de página
  personalizados.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create new pdf document
- add bates numbering pdf
- how to add bates
- add blank page pdf
- add custom page numbers
language: pt
lastmod: 2026-08-04
og_description: Crie um novo documento PDF em C# e adicione automaticamente numeração
  Bates ao PDF para gerenciamento de casos jurídicos – exemplo de código completo
  incluído.
og_image_alt: Screenshot of a C# program creating a PDF document with Bates numbers
  applied
og_title: Criar novo documento PDF com numeração Bates em C#
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Create new PDF document in C# and add Bates numbering pdf quickly using
    Aspose.Pdf – learn to add blank page pdf and custom page numbers.
  headline: Create new PDF document with Bates numbering in C#
  type: TechArticle
tags:
- C#
- PDF
- Aspose.Pdf
- Bates numbering
title: Criar novo documento PDF com numeração Bates em C#
url: /pt/net/document-creation/create-new-pdf-document-with-bates-numbering-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar novo documento PDF com numeração Bates em C#

Se você precisa **criar um novo documento PDF** em C#, este guia mostra como **adicionar numeração Bates ao PDF** usando Aspose.Pdf. Você aprenderá a **adicionar página em branco ao PDF**, configurar **adicionar números de página personalizados**, e salvar o arquivo final.

O tutorial cobre cada passo, desde a instalação da biblioteca até a geração de um PDF que cumpre os padrões de arquivos de processos legais. Ao final, você poderá gerar um PDF, inserir uma página em branco, aplicar números Bates e personalizar o formato da numeração — tudo com um único programa executável.

## Pré-requisitos

* .NET 6.0 SDK ou posterior instalado  
* Visual Studio 2022 (ou qualquer IDE C#)  
* Uma licença ativa do Aspose.Pdf para .NET ou uma chave de avaliação gratuita  

Você não precisa de nenhum pacote NuGet adicional; o tutorial instala tudo automaticamente.

## Etapa 1: Instalar Aspose.Pdf via NuGet

Abra um terminal na pasta do seu projeto e execute:

```bash
dotnet add package Aspose.Pdf
```

O comando adiciona a versão estável mais recente do Aspose.Pdf ao seu projeto, que fornece as classes `Document`, `BatesNumbering` e outras de manipulação de PDF que você usará.

## Etapa 2: Criar novo documento PDF – configuração inicial

Criar o arquivo PDF é a base para todas as operações subsequentes. A classe `Document` representa todo o contêiner PDF.

```csharp
using Aspose.Pdf;

// Step 2: Create a new PDF document
using var doc = new Document();
```

*Por que isso importa*: Instanciar `Document` aloca as estruturas internas necessárias para páginas, fontes e gráficos. Usar `using var` garante que o arquivo seja descartado corretamente após a gravação.

## Etapa 3: Adicionar página em branco ao PDF

Um PDF deve conter ao menos uma página antes que você possa colocar conteúdo nele. Adicionar uma página em branco fornece uma tela limpa para os números Bates.

```csharp
// Step 3: Add a blank page to the document
Page page = doc.Pages.Add();
```

O método `Pages.Add()` adiciona uma nova página vazia ao final da coleção de páginas do documento. Você pode repetir esta chamada para adicionar mais páginas se precisar **adicionar números de página personalizados** em várias páginas.

## Etapa 4: Configurar numeração Bates – como adicionar Bates

A numeração Bates é um identificador sequencial comumente usado em documentos legais. Você a configura através da classe `BatesNumbering`.

```csharp
// Step 4: Set up Bates numbering options
var bates = new BatesNumbering
{
    StartNumber = 1000,      // Starting number for the sequence
    Prefix = "CaseA-",       // Text to prepend to each number
    Increment = 1,           // Increment between consecutive numbers
    // Optional: Set the location, font size, etc.
};
```

*Por que isso importa*: `StartNumber` define o primeiro número, `Prefix` adiciona um rótulo legível, e `Increment` controla o tamanho do passo. Você também pode ajustar `HorizontalAlignment`, `VerticalAlignment`, `FontSize` e `Margins` para controlar a aparência do número em cada página.

## Etapa 5: Aplicar a numeração Bates ao PDF na página

Agora que as opções de numeração estão prontas, aplique-as à página (ou a todo o documento).

```csharp
// Step 5: Apply the Bates numbering to the page
bates.Apply(page);
```

Chamar `Apply` insere o número formatado no rodapé da página por padrão. Se precisar do número em outro local, defina `bates.Position` antes de chamar `Apply`.

## Etapa 6: Salvar o PDF com números Bates aplicados

Finalmente, grave o documento em memória no disco.

```csharp
// Step 6: Save the PDF with Bates numbers applied
string outputPath = Path.Combine(
    Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
    "BatesNumbered.pdf");

doc.Save(outputPath);
Console.WriteLine($"PDF saved to {outputPath}");
```

O arquivo salvo agora contém uma única página com o número Bates **CaseA-1000** exibido na parte inferior. Abra o PDF em qualquer visualizador para verificar a numeração.

## Saída esperada

Ao abrir `BatesNumbered.pdf`, você deverá ver:

* Uma página em branco (ou mais se você adicionou páginas adicionais)  
* O texto **CaseA-1000** posicionado na parte inferior da página (local padrão)  

Se você adicionar mais páginas e reutilizar a mesma instância `BatesNumbering`, os números serão incrementados automaticamente (CaseA-1001, CaseA-1002, …).

## Dica profissional: Adicionar números de página personalizados além dos números Bates

Às vezes você precisa tanto de números Bates quanto de números de página tradicionais. Você pode combiná-los adicionando um `TextFragment` após aplicar a numeração Bates:

```csharp
// Add a traditional page number in the header
var pageNumber = new TextFragment($"Page {page.Number}")
{
    HorizontalAlignment = HorizontalAlignment.Center,
    VerticalAlignment = VerticalAlignment.Top,
    FontSize = 12,
    Font = FontRepository.FindFont("Arial")
};
page.Paragraphs.Add(pageNumber);
```

Este trecho demonstra **adicionar números de página personalizados** enquanto preserva o rótulo Bates.

## Caso extremo: Aplicar numeração Bates a múltiplas páginas

Se o seu documento contém várias páginas, você pode aplicar a mesma instância `BatesNumbering` a cada página em um loop:

```csharp
for (int i = 1; i <= doc.Pages.Count; i++)
{
    bates.Apply(doc.Pages[i]);
}
```

O loop garante que cada página receba um número sequencial baseado no `StartNumber` e `Increment` que você definiu.

## Armadilhas comuns e como evitá‑las

| Problema | Por que acontece | Correção |
|----------|------------------|----------|
| Números aparecem fora do centro | O alinhamento padrão pode não corresponder ao seu layout | Defina `bates.HorizontalAlignment` e `bates.VerticalAlignment` explicitamente |
| Números se sobrepõem ao conteúdo existente | Nenhuma margem está definida | Ajuste `bates.Margin` ou use `bates.Position` para mover o número |
| Exceção de licença em tempo de execução | A versão de avaliação limita a saída | Aplique uma licença válida do Aspose.Pdf antes de criar o documento (`License license = new License(); license.SetLicense("Aspose.Pdf.lic");`) |

## Exemplo completo em funcionamento

Abaixo está um programa autônomo que você pode copiar, colar e executar.

```csharp
using System;
using System.IO;
using Aspose.Pdf;

class Program
{
    static void Main()
    {
        // 1. Create a new PDF document
        using var doc = new Document();

        // 2. Add a blank page pdf
        Page page = doc.Pages.Add();

        // 3. Configure Bates numbering – how to add bates
        var bates = new BatesNumbering
        {
            StartNumber = 1000,
            Prefix = "CaseA-",
            Increment = 1,
            HorizontalAlignment = HorizontalAlignment.Right,
            VerticalAlignment = VerticalAlignment.Bottom,
            Margin = new MarginInfo(20, 20, 20, 20),
            FontSize =


## O que você deve aprender a seguir?

Os tutoriais a seguir cobrem tópicos intimamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Como adicionar e personalizar números de página em PDFs usando Aspose.PDF para .NET | Guia de Manipulação de Documentos](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [Aspose.PDF .NET&#58; Adicionar números de página a PDFs usando FloatingBox](/pdf/english/net/text-operations/aspose-pdf-net-floatingbox-page-numbering/)
- [Criar documento PDF com Aspose.PDF – Adicionar página, forma e salvar](/pdf/english/net/document-creation/create-pdf-document-with-aspose-pdf-add-page-shape-save/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}