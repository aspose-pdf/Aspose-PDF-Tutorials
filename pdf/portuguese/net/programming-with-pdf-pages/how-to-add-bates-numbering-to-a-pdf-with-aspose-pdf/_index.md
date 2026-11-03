---
category: general
date: 2026-10-07
description: Aprenda a adicionar numeração Bates a um PDF usando C#. Este guia passo
  a passo também aborda a numeração de páginas em PDF e outros truques de numeração.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add bates numbering
- pdf page numbering
- number pdf pages
- how to add bates
- bates numbering pdf
language: pt
lastmod: 2026-10-07
og_description: Adicione numeração Bates a um PDF rapidamente. Siga este tutorial
  para dominar a numeração de páginas de PDF, numerar páginas de PDF e automatizar
  o rastreamento de documentos.
og_image_alt: Screenshot of a PDF with Bates numbers added using Aspose.Pdf
og_title: Adicionar numeração Bates a PDFs em C# – guia completo da Aspose
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Learn how to add bates numbering to a PDF using C#. This step‑by‑step
    guide also covers pdf page numbering and other numbering tricks.
  headline: How to add bates numbering to a PDF with Aspose.Pdf
  type: TechArticle
- description: Learn how to add bates numbering to a PDF using C#. This step‑by‑step
    guide also covers pdf page numbering and other numbering tricks.
  name: How to add bates numbering to a PDF with Aspose.Pdf
  steps:
  - name: 1. Can I change the location of the numbers?
    text: Yes. Set `batesOptions.Position = new Position(10, 10, 10, 10);` where the
      four values represent margins from the top, bottom, left, and right edges. Aspose
      also provides predefined enums such as `BatesNumberingPosition.BottomCenter`.
  - name: 2. What if my PDF already contains page numbers?
    text: Adding Bates numbers will **stack** on top of existing numbers. To avoid
      visual clutter, either hide the original numbers (if they are part of a text
      layer) or adjust the `batesOptions` font size and position.
  - name: 3. Does this work with encrypted PDFs?
    text: 'Aspose can open password‑protected PDFs if you supply the password:'
  - name: 4. How do I **number pdf pages** with a simple sequential counter (no prefix/suffix)?
    text: 'Just set `Prefix = string.Empty` and `Suffix = string.Empty`:'
  - name: 5. Can I use this approach in ASP.NET Core to serve PDFs on‑the‑fly?
    text: 'Absolutely. Load the document, apply the numbering, then write the stream
      to the HTTP response:'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Como adicionar numeração Bates a um PDF com Aspose.Pdf
url: /pt/net/programming-with-pdf-pages/how-to-add-bates-numbering-to-a-pdf-with-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como adicionar numeração Bates a um PDF com Aspose.Pdf

Se você precisa **adicionar numeração bates** a um PDF, este guia mostra exatamente como fazer isso em C#. Seja preparando pacotes jurídicos, gerenciando arquivos de casos, ou apenas querendo uma **numeração de páginas pdf** confiável, os passos abaixo fornecem uma solução completa e executável.

Neste tutorial você aprenderá a:

* Carregar um arquivo PDF existente.
* Configurar opções de numeração Bates como prefixo, número inicial, preenchimento de dígitos, separador e sufixo.
* Aplicar a numeração a cada página.
* Salvar o documento atualizado.

Nenhuma ferramenta externa é necessária além da biblioteca Aspose.Pdf para .NET, e o código funciona com .NET 6+ assim como com .NET Framework 4.7.2+.  

---

## Pré-requisitos

Antes de começar, certifique‑se de que você tem:

| Requisito | Por que é importante |
|-------------|----------------|
| **Aspose.Pdf for .NET** (pacote NuGet `Aspose.Pdf`) | Fornece as classes `Document` e `BatesNumberingOptions` usadas no código. |
| **.NET SDK** (6.0 ou posterior recomendado) | Permite compilar e executar a aplicação console em C#. |
| **Um PDF de origem** que você deseja numerar | O tutorial usa `source.pdf` como exemplo; substitua o caminho pelo seu próprio arquivo. |
| **Permissão de gravação** na pasta de saída | A chamada `Save` precisa gravar o novo arquivo. |

Você pode instalar a biblioteca com o seguinte comando CLI:

```bash
dotnet add package Aspose.Pdf
```

---

## Etapa 1: Criar um novo projeto console

Abra um terminal e execute:

```bash
dotnet new console -n BatesNumberingDemo
cd BatesNumberingDemo
```

Isso cria um projeto C# mínimo que preencheremos com o código necessário para **adicionar numeração bates**.

---

## Etapa 2: Adicionar as diretivas `using` necessárias

Abra `Program.cs` e adicione os namespaces no topo do arquivo:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;
```

* `Aspose.Pdf` fornece acesso à classe `Document` para carregar e salvar PDFs.  
* `Aspose.Pdf.Text` contém `BatesNumberingOptions`, o objeto que define como os números aparecem.

---

## Etapa 3: Carregar o PDF de origem

A primeira linha executável carrega o PDF que você deseja numerar. Substitua `"YOUR_DIRECTORY/source.pdf"` pelo caminho real do seu arquivo.

```csharp
// Load the source PDF
Document pdf = new Document("YOUR_DIRECTORY/source.pdf");
```

Se o arquivo não for encontrado, Aspose lança uma `FileNotFoundException`. Para evitar isso, você pode validar o caminho antes:

```csharp
if (!System.IO.File.Exists("YOUR_DIRECTORY/source.pdf"))
{
    Console.WriteLine("Source PDF not found.");
    return;
}
```

---

## Etapa 4: Definir as opções de numeração Bates

`BatesNumberingOptions` permite controlar cada elemento visual da numeração. O exemplo abaixo mostra uma configuração típica para arquivos de casos jurídicos:

```csharp
// Define Bates numbering options
BatesNumberingOptions batesOptions = new BatesNumberingOptions
{
    Prefix = "CASE-",          // Text before the numeric part
    StartNumber = 1000,       // First number to use
    Digits = 6,               // Pad with leading zeros (e.g., 001000)
    Separator = "-",          // Character between prefix, number, and suffix
    Suffix = "-2025"          // Text after the numeric part
};
```

**Por que cada propriedade importa**

| Propriedade | Propósito |
|----------|---------|
| `Prefix` | Ajuda a agrupar documentos por projeto, cliente ou caso. |
| `StartNumber` | Define o contador inicial; útil quando já existem arquivos numerados. |
| `Digits` | Garante largura uniforme, facilitando a ordenação. |
| `Separator` | Melhora a legibilidade, especialmente ao combinar prefixo e sufixo. |
| `Suffix` | Permite adicionar um ano, versão ou qualquer identificador final. |

Você também pode controlar a posição (topo, fundo, esquerda, direita) e o estilo da fonte acessando `batesOptions.Position` e `batesOptions.Font`. Para a maioria dos cenários, os padrões (canto inferior‑direito, Times New Roman 12 pt) funcionam bem.

---

## Etapa 5: Aplicar a numeração a cada página

Chamar `pdf.BatesNumbering.Add` insere os números em cada página na ordem em que aparecem.

```csharp
// Apply Bates numbering to every page
pdf.BatesNumbering.Add(batesOptions);
```

Se precisar **numerar páginas pdf** apenas em um subconjunto (por exemplo, pular a capa), pode passar um `PageCollection` em vez disso:

```csharp
// Example: skip the first page
pdf.BatesNumbering.Add(batesOptions, pdf.Pages.Skip(1));
```

---

## Etapa 6: Salvar o PDF atualizado

Finalmente, grave o documento modificado no disco. O nome do arquivo geralmente reflete que o PDF agora contém números Bates.

```csharp
// Save the PDF with Bates numbers applied
pdf.Save("YOUR_DIRECTORY/bates_numbered.pdf");
Console.WriteLine("Bates numbering added successfully.");
```

Se a pasta de saída não existir, Aspose a cria automaticamente. Contudo, certifique‑se de que você tem permissão de gravação para evitar uma `UnauthorizedAccessException`.

---

## Exemplo completo e executável

Juntando todas as peças, aqui está um programa completo que você pode copiar, colar e executar:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Load the source PDF
        // -------------------------------------------------
        const string inputPath = "YOUR_DIRECTORY/source.pdf";
        if (!System.IO.File.Exists(inputPath))
        {
            Console.WriteLine($"Input file not found: {inputPath}");
            return;
        }

        Document pdf = new Document(inputPath);

        // -------------------------------------------------
        // 2️⃣ Configure Bates numbering
        // -------------------------------------------------
        BatesNumberingOptions batesOptions = new BatesNumberingOptions
        {
            Prefix = "CASE-",
            StartNumber = 1000,
            Digits = 6,
            Separator = "-",
            Suffix = "-2025"
        };

        // -------------------------------------------------
        // 3️⃣ Apply the numbering to every page
        // -------------------------------------------------
        pdf.BatesNumbering.Add(batesOptions);

        // -------------------------------------------------
        // 4️⃣ Save the result
        // -------------------------------------------------
        const string outputPath = "YOUR_DIRECTORY/bates_numbered.pdf";
        pdf.Save(outputPath);
        Console.WriteLine($"Bates numbering added. Saved to {outputPath}");
    }
}
```

**Saída esperada** (console):

```
Bates numbering added. Saved to YOUR_DIRECTORY/bates_numbered.pdf
```

Abra `bates_numbered.pdf` e você verá cada página rotulada algo como `CASE-001000-2025`, `CASE-001001-2025`, etc., posicionada no canto inferior‑direito padrão.

---

## Perguntas frequentes (FAQ)

### 1. Posso mudar a localização dos números?

Sim. Defina `batesOptions.Position = new Position(10, 10, 10, 10);` onde os quatro valores representam as margens superior, inferior, esquerda e direita. Aspose também fornece enums predefinidos como `BatesNumberingPosition.BottomCenter`.

### 2. E se meu PDF já contém numeração de páginas?

Adicionar números Bates **sobreporá** os números existentes. Para evitar confusão visual, oculte os números originais (se fizerem parte de uma camada de texto) ou ajuste o tamanho da fonte e a posição em `batesOptions`.

### 3. Isso funciona com PDFs criptografados?

Aspose pode abrir PDFs protegidos por senha se você fornecer a senha:

```csharp
Document pdf = new Document("source.pdf", new LoadOptions { Password = "mySecret" });
```

A numeração Bates é então aplicada da mesma forma.

### 4. Como faço para **numerar páginas pdf** com um contador sequencial simples (sem prefixo/sufixo)?

Basta definir `Prefix = string.Empty` e `Suffix = string.Empty`:

```csharp
BatesNumberingOptions simple = new BatesNumberingOptions
{
    StartNumber = 1,
    Digits = 4   // 0001, 0002, …
};
pdf.BatesNumbering.Add(simple);
```

### 5. Posso usar esta abordagem no ASP.NET Core para servir PDFs sob demanda?

Absolutamente. Carregue o documento, aplique a numeração e, em seguida, escreva o stream na resposta HTTP:

```csharp
using (var ms = new MemoryStream())
{
    pdf.Save(ms);
    ms.Position = 0;
    return File(ms, "application/pdf", "bates_numbered.pdf");
}
```

---

## Casos extremos e dicas de boas práticas

| Situação | Abordagem recomendada |
|-----------|----------------------|
| **PDFs grandes (centenas de páginas)** | Chame `pdf.BatesNumbering.Add` **depois** de realizar quaisquer transformações nível página para evitar reprocessar as mesmas páginas várias vezes. |
| **Fontes personalizadas** | Defina `batesOptions.Font = FontRepository.FindFont("Arial")` e ajuste `batesOptions.FontSize` para melhor legibilidade em documentos escaneados. |
| **Jobs em lote críticos de desempenho** | Reutilize uma única instância `Document` ao processar muitos arquivos em um loop; descarte‑a após cada iteração para liberar memória. |
| **Caracteres internacionais** | Use fontes compatíveis com Unicode (ex.: `Times New Roman Unicode`) para garantir que o prefixo ou sufixo seja exibido corretamente. |
| **Compatibilidade de versão** | O código funciona com Aspose.Pdf 23.10 ou superior. Se você usar uma versão mais antiga, verifique a referência da API para possíveis mudanças nos nomes das propriedades. |

---

## Conclusão

Agora você sabe como **adicionar numeração bates** a um PDF usando Aspose.Pdf para .NET. O tutorial abordou o carregamento de um PDF, a configuração de `BatesNumberingOptions`, a aplicação dos números a cada página e a gravação do resultado. Com esses blocos de construção, você também pode implementar **numeração de páginas pdf** genérica, **numerar páginas pdf** com formatos personalizados e integrar o processo em pipelines de automação maiores.

**Próximos passos**

* Explore a API **bates numbering pdf** para personalizar fonte, cor e posicionamento.  
* Combine esta técnica com **assinaturas digitais** para criar pacotes jurídicos à prova de adulteração.  
* Veja as capacidades de **mesclagem de PDF** da Aspose se precisar concatenar vários arquivos de caso antes da numeração.

Sinta‑se à vontade para experimentar diferentes prefixos, sufixos e comprimentos de dígitos para atender aos padrões de arquivamento da sua organização. Boa codificação!

## O que você deve aprender a seguir?

Os tutoriais a seguir cobrem tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas em seus próprios projetos.

- [Criar Documento PDF C# – Guia de Adição de Numeração Bates](/pdf/english/net/document-creation/create-pdf-document-c-add-bates-numbering-guide/)
- [Como Adicionar Numeração Bates em PDF com C# – Guia Completo](/pdf/english/net/programming-with-stamps-and-watermarks/how-to-add-bates-numbering-in-pdf-with-c-complete-guide/)
- [Tutorial Aspose PDF – Inserir Página em Branco e Atualizar Numeração Bates](/pdf/english/net/programming-with-pdf-pages/aspose-pdf-tutorial-insert-a-blank-page-and-update-bates-num/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}