---
category: general
date: 2026-09-27
description: Crie um documento PDF e adicione páginas ao PDF enquanto constrói um
  formulário PDF interativo. Aprenda como adicionar uma caixa de texto ao PDF e criar
  um PDF AcroForm com Aspose.Pdf.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create pdf document
- add pages to pdf
- create interactive pdf form
- how to add textbox to pdf
- how to create acroform pdf
language: pt
lastmod: 2026-09-27
og_description: Crie um documento PDF e adicione páginas ao PDF enquanto desenvolve
  um formulário PDF interativo. Siga este guia para aprender como adicionar uma caixa
  de texto ao PDF e criar um PDF AcroForm usando Aspose.Pdf.
og_image_alt: Screenshot showing a PDF document with a textbox field on two pages
og_title: Crie documento PDF com campos de formulário interativos – guia passo a passo
  em C#
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: create PDF document and add pages to PDF while building an interactive
    PDF form. Learn how to add TextBox to PDF and create AcroForm PDF with Aspose.Pdf.
  headline: How to create PDF document with interactive form fields in C#
  type: TechArticle
- description: create PDF document and add pages to PDF while building an interactive
    PDF form. Learn how to add TextBox to PDF and create AcroForm PDF with Aspose.Pdf.
  name: How to create PDF document with interactive form fields in C#
  steps:
  - name: '**Create PDF document** and add the needed pages.'
    text: '**Create PDF document** and add the needed pages.'
  - name: '**Initialize AcroForm** and define a `TextBoxField`.'
    text: '**Initialize AcroForm** and define a `TextBoxField`.'
  - name: '**Add widget annotations** on each page to place the textbox.'
    text: '**Add widget annotations** on each page to place the textbox.'
  - name: '**Save** the document and test the interactive behavior.'
    text: '**Save** the document and test the interactive behavior.'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF forms
title: Como criar documento PDF com campos de formulário interativos em C#
url: /pt/net/programming-with-forms/how-to-create-pdf-document-with-interactive-form-fields-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como criar documento PDF com campos de formulário interativos em C#

Se você precisa **criar documento PDF** que contenha várias páginas e um formulário interativo, este guia mostra exatamente como fazer. Vamos percorrer a adição de páginas ao PDF, a construção de um AcroForm e a colocação de um campo TextBox em cada página usando Aspose.Pdf para .NET.

Ao final, você terá um único arquivo PDF que permite que os usuários digitem comentários em ambas as páginas. Sem ferramentas externas, apenas algumas linhas de C# e a poderosa biblioteca Aspose.Pdf.

## Pré‑requisitos

Antes de começar, certifique‑se de que você tem:

* .NET 6.0 ou posterior (o código também funciona com .NET Framework 4.7+)
* Uma licença válida do Aspose.Pdf para .NET ou uma chave de avaliação temporária
* Visual Studio 2022 (ou qualquer IDE que suporte C#)
* Familiaridade básica com a sintaxe C# e conceitos de orientação a objetos

> **Dica profissional:** Se você estiver usando a avaliação gratuita, lembre‑se de definir o objeto `License` logo no início do seu programa para evitar marcas d'água de avaliação.

## Etapa 1: Configurar o projeto e importar namespaces

Crie um novo aplicativo de console e adicione o pacote NuGet Aspose.Pdf:

```bash
dotnet new console -n PdfFormDemo
cd PdfFormDemo
dotnet add package Aspose.Pdf
```

No `Program.cs` importe os namespaces necessários:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using Aspose.Pdf.Forms;
```

Esses namespaces dão acesso aos objetos principais do PDF, tipos de anotações e classes de campos de formulário necessárias para o tutorial.

## Etapa 2: Criar documento PDF e adicionar páginas ao PDF

O primeiro passo funcional é **criar documento PDF** e então **adicionar páginas ao PDF**. Cada página hospedará o mesmo campo TextBox.

```csharp
// Initialize a new PDF document
var pdfDocument = new Document();

// Add two blank pages
var firstPage = pdfDocument.Pages.Add();
var secondPage = pdfDocument.Pages.Add();
```

*Por que isso importa:*  
`Document` representa o arquivo PDF completo. Adicionar páginas explicitamente garante que você tenha uma tela para posicionar os widgets do formulário. Você pode adicionar quantas páginas precisar; o exemplo usa duas para clareza.

## Etapa 3: Criar um formulário PDF interativo (AcroForm)

Um **formulário PDF interativo** é construído sobre um objeto AcroForm que vive dentro do `Document`. Criaremos um único `TextBoxField` que será compartilhado entre ambas as páginas.

```csharp
// Initialize the AcroForm if it doesn't exist
if (!pdfDocument.AcroForm.IsPresent)
{
    pdfDocument.AcroForm = new AcroForm(pdfDocument);
}

// Create a TextBox field named "Comments"
var textBoxField = new TextBoxField(pdfDocument.AcroForm)
{
    Name = "Comments",
    // Optional: set default appearance (font size, color)
    DefaultAppearance = new DefaultAppearance("Helvetica", 12, Color.Black)
};
```

*Por que isso importa:*  
O contêiner AcroForm contém todos os elementos interativos. Ao criar um único `TextBoxField`, podemos reutilizar o mesmo campo lógico em várias páginas, mantendo os dados sincronizados quando o usuário o preenche.

## Etapa 4: Como adicionar TextBox ao PDF – posicionar anotações de widget

Uma **anotação de widget** vincula um retângulo visual em uma página ao campo de formulário lógico. Adicionaremos um widget em cada página.

```csharp
// Widget on the first page (coordinates: lower‑left X,Y – upper‑right X,Y)
var firstPageWidget = new WidgetAnnotation(
    firstPage,
    new Rectangle(50, 700, 200, 750))
{
    Parent = textBoxField,
    // Optional visual properties
    HighlightingMode = HighlightingMode.Invert,
    Border = new Border(BorderStyle.Solid, 1, Color.Black)
};

// Widget on the second page, positioned slightly lower
var secondPageWidget = new WidgetAnnotation(
    secondPage,
    new Rectangle(50, 600, 200, 650))
{
    Parent = textBoxField,
    HighlightingMode = HighlightingMode.Invert,
    Border = new Border(BorderStyle.Solid, 1, Color.Black)
};
```

*Por que isso importa:*  
O `WidgetAnnotation` define onde a caixa de texto aparece e como ela se parece. Ao atribuir o mesmo `Parent` (`textBoxField`), ambos os widgets referenciam o mesmo campo de dados subjacente. Usuários que digitarem em um widget verão o mesmo valor no outro página.

## Etapa 5: Salvar o PDF e verificar o resultado

Por fim, grave o documento no disco:

```csharp
// Save the PDF to the output folder
string outputPath = Path.Combine(Environment.CurrentDirectory, "output.pdf");
pdfDocument.Save(outputPath);

Console.WriteLine($"PDF saved to {outputPath}");
```

Ao abrir `output.pdf` no Adobe Acrobat Reader:

* O documento mostra duas páginas.
* Cada página contém uma caixa de texto rotulada “Comments”.
* Digitar na caixa de texto em qualquer página atualiza a outra instantaneamente (elas compartilham o mesmo nome de campo).

### Captura de tela do resultado esperado

![PDF with textbox on two pages](https://example.com/pdf-form-screenshot.png "create PDF document with interactive form fields")

*(O texto alternativo da imagem contém a palavra‑chave principal para acessibilidade e SEO.)*

## Variações comuns e casos de borda

| Situação | Como lidar |
|-----------|------------|
| **Mais de duas páginas** | Crie objetos `WidgetAnnotation` adicionais para cada nova página, reutilizando o mesmo `textBoxField`. |
| **Nomes de campo diferentes por página** | Crie instâncias separadas de `TextBoxField` (por exemplo, `CommentsPage1`, `CommentsPage2`) e atribua a cada widget seu próprio pai. |
| **Caixa de texto multilinha** | Defina `textBoxField.Multiline = true;` antes de adicionar os widgets. |
| **Campos somente‑leitura** | Defina `textBoxField.ReadOnly = true;` para impedir a edição pelo usuário. |
| **Fontes personalizadas** | Carregue um `TrueTypeFont` e atribua‑o via `textBoxField.DefaultAppearance = new DefaultAppearance(font, 12, Color.Black);` |

Essas variações ilustram quão flexível a API AcroForm é, mantendo o padrão central idêntico.

## Recapitulação passo a passo (referência rápida)

1. **Criar documento PDF** e adicionar as páginas necessárias.  
2. **Inicializar AcroForm** e definir um `TextBoxField`.  
3. **Adicionar anotações de widget** em cada página para posicionar a caixa de texto.  
4. **Salvar** o documento e testar o comportamento interativo.

## Próximos passos

Agora que você sabe **como adicionar textbox ao PDF** e **como criar formulário PDF interativo**, pode expandir o formulário:

* Adicionar caixas de seleção, botões de opção ou listas suspensas usando `CheckBoxField`, `RadioButtonField` e `ComboBoxField`.
* Exportar dados do formulário para FDF ou XFDF para processamento no servidor.
* Aplicar ações JavaScript aos campos para validação dinâmica.

Explore a documentação oficial do Aspose.Pdf para obter uma lista completa de tipos de campos de formulário e opções avançadas de estilo.

---

*Você aprendeu como **criar documento PDF**, **adicionar páginas ao PDF**, **criar formulário PDF interativo**, **como adicionar textbox ao PDF** e **como criar AcroForm PDF** usando um exemplo conciso e executável. Sinta‑se à vontade para experimentar tipos de campo adicionais e ajustes de layout que atendam às necessidades da sua aplicação.*

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui código completo e funcional com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas em seus próprios projetos.

- [How to Create PDF with Aspose – Add Form Field and Pages](/pdf/english/net/programming-with-forms/how-to-create-pdf-with-aspose-add-form-field-and-pages/)
- [How to Add Text Box PDF – Create PDF Form Field & Save Edited PDF Document](/pdf/english/net/programming-with-forms/how-to-add-text-box-pdf-create-pdf-form-field-save-edited-pd/)
- [Create PDF Document with Aspose – Add Page, Text Box, and Form](/pdf/english/net/forms-annotations/create-pdf-document-with-aspose-add-page-text-box-and-form/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}