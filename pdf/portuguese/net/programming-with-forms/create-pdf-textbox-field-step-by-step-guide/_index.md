---
category: general
date: 2026-06-21
description: Crie um campo de caixa de texto PDF com C# e aprenda como duplicar um
  campo de formulário PDF ou adicionar uma caixa de texto a um formulário PDF em apenas
  algumas linhas de código.
draft: false
keywords:
- create pdf textbox field
- duplicate pdf form field
- add textbox to pdf form
- pdf form automation
- c# pdf library
language: pt
og_description: Crie rapidamente um campo de texto PDF. Este guia mostra como duplicar
  um campo de formulário PDF e adicionar um campo de texto ao formulário PDF usando
  uma biblioteca PDF moderna em C#.
og_title: Criar Campo de Texto PDF – Tutorial Completo de C#
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Create PDF textbox field with C# and learn how to duplicate PDF form
    field or add textbox to PDF form in just a few lines of code.
  headline: Create PDF Textbox Field – Step‑by‑Step Guide
  type: TechArticle
- description: Create PDF textbox field with C# and learn how to duplicate PDF form
    field or add textbox to PDF form in just a few lines of code.
  name: Create PDF Textbox Field – Step‑by‑Step Guide
  steps:
  - name: What if I need the field on *more* than two pages?
    text: Just repeat the clone‑and‑add steps for each additional page. The underlying
      data object stays the same, so all widgets stay in sync.
  - name: How do I change the appearance (font, border, background)?
    text: Each `Widget` has a `SetBorderColor`, `SetBorderWidth`, and `SetBackgroundColor`
      method. You can also assign a default appearance string (`DA`) to control the
      font and size.
  - name: Can I make the field read‑only after the user fills it?
    text: Yes. Set the `ReadOnly` flag on the field after you’ve collected the data,
      or toggle it based on your workflow.
  - name: What about PDFs that already contain a form?
    text: If the document already has an AcroForm, `doc.GetForm()` simply returns
      it. You can then add new fields without disturbing existing ones. Just be careful
      to use unique field names.
  type: HowTo
tags:
- PDF
- C#
- FormFields
title: Criar Campo de Texto PDF – Guia Passo a Passo
url: /pt/net/programming-with-forms/create-pdf-textbox-field-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar Campo de Texto PDF – Tutorial Completo em C#

Já precisou **criar campo de texto PDF** mas não sabia quais chamadas de API usar? Você não está sozinho. Seja construindo um portal de assinatura de contratos ou uma simples planilha de captura de dados, adicionar caixas de texto interativas a um PDF é uma habilidade essencial para qualquer desenvolvedor de automação de formulários.  

Neste guia vamos percorrer um exemplo prático que não só **adiciona caixa de texto ao formulário PDF**, mas também mostra como **duplicar campo de formulário PDF** para que a mesma entrada apareça em várias páginas. Ao final, você terá um programa executável que pode ser inserido em qualquer projeto .NET.

## O que você vai precisar

- .NET 6.0 ou superior (o código funciona também com .NET Core)  
- Uma biblioteca PDF moderna para C# – o trecho abaixo usa o **PDFTron SDK**, mas os conceitos se aplicam ao iText 7, PdfSharp ou outras bibliotecas.  
- Visual Studio 2022 (ou qualquer IDE de sua preferência)  

É só isso – sem serviços extras, sem dependências obscuras. Se já tem um PDF que deseja augmentar, basta apontar o código para ele.

---

## Etapa 1: Configurar o Projeto e Importar o SDK

Primeiro, crie um aplicativo console:

```bash
dotnet new console -n PdfFormDemo
cd PdfFormDemo
```

Adicione o pacote NuGet do PDFTron:

```bash
dotnet add package PDFTron.NET
```

Agora abra `Program.cs` e importe os namespaces que vamos precisar:

```csharp
using System;
using pdftron;
using pdftron.Common;
using pdftron.PDF;
using pdftron.SDF;
```

> **Dica profissional:** Se estiver usando outra biblioteca, substitua as instruções `using` pelos equivalentes (por exemplo, `iText.Kernel.Pdf` para iText 7).

## Etapa 2: Inicializar o Documento PDF e o Formulário

Começaremos com um PDF novo que contém duas páginas – a página de origem para a caixa de texto original e uma página de destino para a duplicata.

```csharp
PDFNet.Initialize();                     // Initialize the PDFTron runtime

// Create a new PDF document
using (PDFDoc doc = new PDFDoc())
{
    // Add two blank pages (letter size)
    Page sourcePage = doc.PageCreate(new Size(612, 792));
    doc.PagePushBack(sourcePage);
    Page targetPage = doc.PageCreate(new Size(612, 792));
    doc.PagePushBack(targetPage);

    // Get (or create) the AcroForm object
    Form form = doc.GetForm();
```

O objeto `Form` é onde todos os campos interativos vivem. Se o documento ainda não possuir um formulário, `GetForm()` cria um para nós.

## Etapa 3: **Criar Campo de Texto PDF** na Primeira Página

Agora vem o núcleo do nosso tutorial – criar um campo de texto. As coordenadas do retângulo são expressas em pontos (1 polegada = 72 pontos). O exemplo posiciona a caixa próximo ao topo‑central da primeira página.

```csharp
    // Step 1: Create a text box field on the first page and set its initial value
    TextBoxField textBoxField = new TextBoxField(sourcePage, new Rect(100, 500, 300, 520))
    {
        Value = "Sample"
    };
```

Por que definimos `Value` imediatamente? Pré‑popular o campo dá ao usuário uma pista sobre a entrada esperada e também demonstra que o campo está totalmente funcional.

## Etapa 4: Adicionar o Campo ao Formulário – **Adicionar Caixa de Texto ao Formulário PDF**

Em seguida, registramos o campo no formulário usando um nome lógico. Esse nome será usado posteriormente quando precisar ler ou modificar os dados do campo programaticamente.

```csharp
    // Step 2: Add the field to the form with a logical name
    form.Add(textBoxField, "multiBox");
```

Escolher um nome claro (como `"multiBox"`) facilita a compreensão do código futuro, especialmente quando você tem dezenas de campos.

## Etapa 5: **Duplicar Campo de Formulário PDF** em Outra Página

Um requisito comum é exibir o mesmo campo em várias páginas – pense em uma caixa “Nome do Cliente” que aparece em cada página de uma fatura. O PDFTron permite clonar a anotação widget, que é a representação visual do campo.

```csharp
    // Step 3: Clone the field's widget annotation so it can appear on another page
    Widget clonedWidget = textBoxField.CreateWidgetAnnotation();

    // Step 4: Place the cloned widget on the second page
    targetPage.Annotations.Add(clonedWidget);
```

O widget clonado compartilha os mesmos dados subjacentes da caixa de texto original. Quando o usuário digita em uma instância, a outra é atualizada automaticamente – essa é a mágica da **duplicação de campo de formulário PDF**.

## Etapa 6: Salvar o Documento e Limpar

Por fim, grave o PDF no disco e encerre o runtime do PDFNet.

```csharp
    // Save the resulting PDF
    doc.Save("output.pdf", SDFDoc.SaveOptions.e_linearized);
    Console.WriteLine("PDF created: output.pdf");
}

// Shut down PDFNet (optional but good practice)
PDFNet.Terminate();
```

Executar o programa gera um PDF de duas páginas (`output.pdf`). Abra-o no Adobe Acrobat Reader, clique na caixa de texto da página 1, digite algo e, em seguida, vá para a página 2 – o mesmo texto aparecerá instantaneamente. Esse é um exemplo totalmente funcional de **criar campo de texto PDF** com um campo duplicado.

---

## Exemplo Completo (Pronto para Copiar‑Colar)

```csharp
// Program.cs
using System;
using pdftron;
using pdftron.Common;
using pdftron.PDF;
using pdftron.SDF;

class Program
{
    static void Main()
    {
        PDFNet.Initialize();

        using (PDFDoc doc = new PDFDoc())
        {
            // Create two pages
            Page sourcePage = doc.PageCreate(new Size(612, 792));
            doc.PagePushBack(sourcePage);
            Page targetPage = doc.PageCreate(new Size(612, 792));
            doc.PagePushBack(targetPage);

            // Get the form (creates one if missing)
            Form form = doc.GetForm();

            // Step 1: Create a text box field on the first page
            TextBoxField textBoxField = new TextBoxField(sourcePage,
                new Rect(100, 500, 300, 520))
            {
                Value = "Sample"
            };

            // Step 2: Add the field to the form
            form.Add(textBoxField, "multiBox");

            // Step 3: Clone the widget so it appears on page 2
            Widget clonedWidget = textBoxField.CreateWidgetAnnotation();

            // Step 4: Attach the cloned widget to the second page
            targetPage.Annotations.Add(clonedWidget);

            // Save the file
            doc.Save("output.pdf", SDFDoc.SaveOptions.e_linearized);
            Console.WriteLine("PDF created: output.pdf");
        }

        PDFNet.Terminate();
    }
}
```

**Saída esperada:** Um arquivo chamado `output.pdf` contendo duas páginas. Ambas exibem a mesma caixa de texto editável rotulada “Sample”. Editar uma atualiza a outra instantaneamente.

---

## Perguntas Frequentes & Casos de Borda

### E se eu precisar do campo em *mais* de duas páginas?

Basta repetir as etapas de clonar‑e‑adicionar para cada página adicional. O objeto de dados subjacente permanece o mesmo, então todos os widgets permanecem sincronizados.

```csharp
Widget anotherClone = textBoxField.CreateWidgetAnnotation();
thirdPage.Annotations.Add(anotherClone);
```

### Como mudar a aparência (fonte, borda, fundo)?

Cada `Widget` possui os métodos `SetBorderColor`, `SetBorderWidth` e `SetBackgroundColor`. Você também pode atribuir uma string de aparência padrão (`DA`) para controlar a fonte e o tamanho.

```csharp
textBoxField.SetBorderColor(new ColorPt(0, 0, 1), 3); // blue border
textBoxField.SetBackgroundColor(new ColorPt(0.9, 0.9, 0.9), 3); // light gray fill
textBoxField.SetDefaultAppearance("Helvetica 12 Tf 0 g");
```

### Posso tornar o campo somente‑leitura após o usuário preenchê‑lo?

Sim. Defina a flag `ReadOnly` no campo depois de coletar os dados, ou alterne‑a conforme seu fluxo de trabalho.

```csharp
textBoxField.SetFlag(Field.Flag.e_readonly, true);
```

### E quanto a PDFs que já contêm um formulário?

Se o documento já possui um AcroForm, `doc.GetForm()` simplesmente o retorna. Você pode então adicionar novos campos sem perturbar os existentes. Apenas tenha cuidado para usar nomes de campo únicos.

---

## Dicas para Projetos Reais

- **Convenção de nomes:** Prefixe os nomes dos campos com a página ou seção (ex.: `invoice_customer_name`) para evitar colisões.  
- **Validação:** Use ações JavaScript (`field.SetAction(Field.Action.e_keystroke, "event.rc = /^[A-Za-z]+$/.test(event.change);")`) se precisar de validação no lado do cliente.  
- **Desempenho:** Ao trabalhar com PDFs grandes, chame `doc.Lock()` antes de operações em lote para reduzir a sobrecarga de I/O.  
- **Acessibilidade:** Defina a propriedade `AlternateName` para que leitores de tela descrevam o campo.

---

## Conclusão

Acabamos de **criar um campo de texto PDF**, mostrar como **duplicar campo de formulário PDF** entre páginas e demonstrar a maneira mais simples de **adicionar caixa de texto ao formulário PDF** usando C#. O código completo e executável está acima, e você pode estendê‑lo com estilos, validações ou páginas adicionais conforme necessário.

Pronto para o próximo passo? Experimente incorporar um menu suspenso (`ChoiceField`) ou um widget de assinatura, ou explore como achatar o formulário após a entrada de dados para fins de arquivamento. O PDFTron SDK (ou qualquer biblioteca comparável) fornece os blocos de construção — sua imaginação decide a forma final.

Se encontrar algum obstáculo, deixe um comentário abaixo ou consulte a documentação oficial da biblioteca; ela está repleta de exemplos que complementam o que abordamos aqui. Boa codificação, e que seus formulários estejam sempre sincronizados!

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Como Criar PDF com Aspose – Adicionar Campo de Formulário e Páginas](/pdf/english/net/programming-with-forms/how-to-create-pdf-with-aspose-add-form-field-and-pages/)
- [Adicionar Campo de Formulário em Documento PDF usando Java](/pdf/english/java/pdf-form-fields/add-form-field-in-pdf-document-using-java/)
- [Adicionar Campo de Formulário em Documento PDF usando Java](/pdf/german/java/pdf-form-fields/add-form-field-in-pdf-document-using-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}