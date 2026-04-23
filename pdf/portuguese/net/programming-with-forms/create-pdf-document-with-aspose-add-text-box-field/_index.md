---
category: general
date: 2026-03-24
description: Criar documento PDF usando Aspose.PDF em C#. Aprenda como adicionar um
  campo de caixa de texto em um formulário PDF e inserir campos de formulário PDF
  rapidamente.
draft: false
keywords:
- create pdf document
- add text box pdf
- add form field pdf
- how to create pdf
- how to add textbox
language: pt
og_description: Crie um documento PDF com Aspose.PDF em C#. Este guia mostra como
  adicionar um campo de formulário PDF de caixa de texto e como adicionar um campo
  de formulário PDF em minutos.
og_title: Criar documento PDF com Aspose – Adicionar campo de caixa de texto
tags:
- Aspose.PDF
- C#
- PDF Forms
title: Criar documento PDF com Aspose – Adicionar campo de caixa de texto
url: /pt/net/programming-with-forms/create-pdf-document-with-aspose-add-text-box-field/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar Documento PDF com Aspose – Adicionar Campo de Caixa de Texto

Já precisou **criar documento PDF** programaticamente e se perguntou por onde começar? Você não é o único—muitos desenvolvedores encontram esse obstáculo quando seus aplicativos precisam coletar entrada do usuário sem usar uma biblioteca de UI pesada. A boa notícia? Com Aspose.PDF for .NET você pode gerar um PDF, colocar uma caixa de texto em qualquer página e até anexar o mesmo campo a várias páginas—tudo em poucas linhas.

Neste tutorial vamos percorrer todo o processo: desde a inicialização do PDF, até **adicionar caixa de texto PDF** nos campos de formulário, até **adicionar campo de formulário PDF** no registro, e finalmente como verificar se tudo funciona. Ao final, você saberá **como criar PDF** interativos e também verá **como adicionar caixa de texto** que se comportam exatamente como campos nativos do Acrobat.

---

## O que você precisará

- **ASP.NET Core** ou qualquer projeto .NET 6+ (o código também funciona no .NET Framework 4.6+).  
- **Aspose.PDF for .NET** pacote NuGet (versão 23.9 ou mais recente).  
- Um nível modesto de experiência em C#—nada sofisticado, apenas o básico.  

Se você já marcou essas caixas, estamos prontos para começar. Sem ferramentas extras, sem serviços externos, apenas código C# puro que você pode colar em um aplicativo console e executar.

---

## Criar Documento PDF e Adicionar um Campo de Caixa de Texto

O primeiro passo, como era de se esperar, é **criar documento PDF**. Pense na classe `Document` como uma tela em branco; depois de tê‑la, você pode começar a pintar páginas, formas e elementos interativos.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Forms;

// Step 1: Create a new PDF document (the blank canvas)
using var document = new Document();

// Step 2: Add a new page where the text box will live
var page1 = document.Pages.Add();
```

> **Por que isso importa:** Instanciar `Document` sem nenhuma página lança uma exceção no momento em que você tenta colocar um widget. Adicionar uma página primeiro garante um índice de página válido (`Pages[1]`) para os próximos passos.

---

## Adicionar Campo de Caixa de Texto PDF à Página 1

Agora que temos uma página, vamos **adicionar caixa de texto PDF** ao campo de formulário. A classe `TextBoxField` representa um único campo lógico; você pode pensar nele como o “nome” da entrada que pode aparecer em vários lugares.

```csharp
// Step 3: Define the rectangle where the textbox will appear (x, y, width, height)
var textBoxRect = new Rectangle(100, 500, 300, 520);

// Step 4: Create the text box field on page 1
var textBoxField = new TextBoxField(document.Pages[1], textBoxRect)
{
    // This logical name is used later when you retrieve the value
    PartialName = "MultiWidget"
};
```

> **Dica profissional:** O retângulo usa pontos (1/72 polegada). Ajuste as coordenadas para corresponder ao seu layout; a origem (0,0) está no canto inferior‑esquerdo da página.

---

## Criar um Segundo Widget em Outra Página

Um único campo lógico pode ter múltiplos widgets visuais—perfeito para formulários de várias páginas. Aqui está **como adicionar caixa de texto** em uma segunda página, reutilizando o mesmo nome de campo.

```csharp
// Step 5: Add a second page for the extra widget
var page2 = document.Pages.Add();

// Step 6: Create a widget for the same field on page 2
var secondWidget = textBoxField.CreateWidget(new Rectangle(100, 400, 300, 420));
```

> **Por que fazemos isso:** Usuários frequentemente precisam preencher a mesma informação em diferentes seções (por exemplo, “Nome” no topo e novamente em um resumo). Ao compartilhar o nome lógico, o Aspose garante que ambos os widgets permaneçam sincronizados.

---

## Registrar o Campo de Formulário no PDF

Criar o objeto do campo não é suficiente; você deve adicioná‑lo à coleção de formulários do documento. Esta é a etapa onde você **adicionar campo de formulário PDF** à estrutura interna.

```csharp
// Step 7: Register the field (with both widgets) in the document's form collection
document.Form.Add(textBoxField, "MultiWidget");

// Optional: Save the PDF to disk
document.Save("MultiWidgetExample.pdf");
```

> **O que acontece nos bastidores:** `Form.Add` grava a definição do campo no dicionário AcroForm, tornando o PDF interativo quando aberto no Acrobat Reader ou em qualquer visualizador de PDF que suporte formulários.

---

## Executar e Verificar o Resultado

Compile e execute o aplicativo console. Abra `MultiWidgetExample.pdf` no Adobe Acrobat (ou em qualquer visualizador que suporte formulários) e você verá duas caixas de texto idênticas nas páginas 1 e 2. Digite algo em uma caixa—observe a outra atualizar instantaneamente. Esse é o poder de um campo lógico compartilhado.

```text
Expected outcome:
- PDF with two pages.
- Each page shows a white rectangle (the text box).
- Editing one box updates the other automatically.
```

Se você não vir as caixas, verifique novamente se os retângulos estão dentro dos limites da página e se você salvou o documento após adicionar o campo.

---

## Perguntas Frequentes & Casos Limítrofes

### E se eu precisar de uma aparência diferente em cada página?

Você pode personalizar cada widget após a criação:

```csharp
secondWidget.Rect = new Rectangle(150, 350, 350, 370); // reposition
secondWidget.Border = new Border(BorderStyle.Solid, 1, Color.Black);
secondWidget.BackgroundColor = Color.LightYellow;
```

### Posso definir um valor padrão?

Claro—basta atribuir `Value` antes de salvar:

```csharp
textBoxField.Value = "Enter your name here";
```

Todos os widgets exibirão esse placeholder até que o usuário o sobrescreva.

### Como tornar o campo obrigatório?

```csharp
textBoxField.Required = true;
```

O Acrobat avisará o usuário se ele tentar enviar o formulário sem preenchê‑lo.

### Isso funciona com conformidade PDF/A?

Aspose.PDF suporta PDF/A‑1b,‑2b,‑3b. Depois de terminar de construir o formulário, você pode converter:

```csharp
document.Convert(new PdfConversionOptions { Compliance = PdfCompliance.PdfA2b });
```

---

## Exemplo Completo Funcional

Abaixo está o programa completo, pronto para copiar e colar. Salve‑o como `Program.cs` em um projeto console .NET, adicione o pacote NuGet Aspose.PDF e execute.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Forms;
using Aspose.Pdf.Drawing;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new PDF document
        using var document = new Document();

        // 2️⃣ Add two pages (page 1 will host the first widget, page 2 the second)
        var page1 = document.Pages.Add();
        var page2 = document.Pages.Add();

        // 3️⃣ Define the rectangle for the first widget
        var rect1 = new Rectangle(100, 500, 300, 520);

        // 4️⃣ Create the text box field (logical name = "MultiWidget")
        var textBoxField = new TextBoxField(document.Pages[1], rect1)
        {
            PartialName = "MultiWidget",
            Value = "Sample text",        // optional default value
            Required = true               // makes the field mandatory
        };

        // 5️⃣ Add a second widget on page

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}