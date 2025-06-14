---
"description": "Aprenda a criar botões de opção alinhados horizontal e verticalmente em PDF usando o Aspose.PDF para .NET com este tutorial passo a passo."
"linktitle": "Botões de opção horizontais e verticais"
"second_title": "Referência da API Aspose.PDF para .NET"
"title": "Botões de opção horizontais e verticais"
"url": "/pt/net/programming-with-forms/horizontally-and-vertically-radio-buttons/"
"weight": 180
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Botões de opção horizontais e verticais

## Introdução

A criação de formulários PDF interativos pode aprimorar significativamente a experiência do usuário, especialmente quando se trata de coletar informações. Um dos elementos de formulário mais comuns é o botão de opção, que permite aos usuários selecionar uma opção de um conjunto. Neste tutorial, exploraremos como criar botões de opção alinhados horizontal e verticalmente usando o Aspose.PDF para .NET. Seja você um desenvolvedor experiente ou iniciante, este guia o guiará pelo processo passo a passo, garantindo que você tenha uma compreensão clara de cada parte.

## Pré-requisitos

Antes de mergulhar no código, há alguns pré-requisitos que você deve ter em mente:

1. Aspose.PDF para .NET: Certifique-se de ter a biblioteca Aspose.PDF instalada. Você pode baixá-la do site [site](https://releases.aspose.com/pdf/net/).
2. Visual Studio: um ambiente de desenvolvimento onde você pode escrever e testar seu código.
3. Conhecimento básico de C#: a familiaridade com a programação em C# ajudará você a entender melhor os trechos de código.

## Pacotes de importação

Para começar, você precisa importar os pacotes necessários para o seu projeto C#. Veja como fazer isso:

### Criar um novo projeto

Abra o Visual Studio e crie um novo projeto em C#. Você pode escolher um Aplicativo de Console para simplificar.

### Adicionar referência Aspose.PDF

1. Clique com o botão direito do mouse no seu projeto no Solution Explorer.
2. Selecione "Gerenciar pacotes NuGet".
3. Procure por "Aspose.PDF" e instale a versão mais recente.

```csharp
using System;
using System.IO;
using Aspose.Pdf.Facades;
using Aspose.Pdf;
using Aspose.Pdf.Forms;
```

Agora que você configurou tudo, vamos dividir o código para criar botões de opção alinhados horizontal e verticalmente.

## Etapa 1: Configurar o diretório de documentos

Nesta etapa, definiremos o caminho para o diretório onde seus documentos PDF serão armazenados.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

Substituir `"YOUR DOCUMENT DIRECTORY"` com o caminho real onde você deseja salvar o arquivo PDF. Isso é crucial, pois indica ao programa onde procurar os arquivos de entrada e onde salvar a saída.

## Etapa 2: Carregue o documento PDF existente

Em seguida, precisamos carregar o documento PDF com o qual trabalharemos. Isso é feito usando o `FormEditor` aula.

```csharp
FormEditor formEditor = new FormEditor();
formEditor.BindPdf(dataDir + "input.pdf");
```

Aqui, criamos uma instância de `FormEditor` e vinculá-lo a um arquivo PDF existente chamado `input.pdf`. Certifique-se de que este arquivo exista no diretório especificado.

## Etapa 3: Configurar propriedades do botão de opção

Agora, vamos definir algumas propriedades para nossos botões de opção. Isso inclui o espaço entre os botões, sua orientação e seu tamanho.

```csharp
formEditor.RadioGap = 4; // Distância entre as opções dos botões de opção
formEditor.RadioHoriz = true; // Definir como verdadeiro para alinhamento horizontal
formEditor.RadioButtonItemSize = 20; // Tamanho do botão de opção
formEditor.Facade.BorderWidth = 1; // Largura da borda
formEditor.Facade.BorderColor = System.Drawing.Color.Black; // Cor da borda
```

Essas propriedades ajudarão a definir como os botões de opção aparecerão no PDF. `RadioGap` propriedade controla o espaço entre os botões, enquanto `RadioHoriz` determina seu layout.

## Etapa 4: adicionar botões de opção horizontais

Agora, vamos adicionar os botões de opção horizontais ao PDF.

```csharp
formEditor.Items = new string[] { "First", "Second", "Third" };
formEditor.AddField(FieldType.Radio, "NewField1", 1, 40, 600, 120, 620);
```

Neste código, definimos os itens para os botões de opção e os adicionamos ao PDF. `AddField` O método usa vários parâmetros, incluindo o tipo de campo, o nome do campo e as coordenadas para posicionamento.

## Etapa 5: adicionar botões de opção verticais

Em seguida, adicionaremos os botões de opção verticais. Para isso, precisamos alterar a orientação de volta para vertical.

```csharp
formEditor.RadioHoriz = false; // Definir como falso para alinhamento vertical
formEditor.Items = new string[] { "First", "Second", "Third" };
formEditor.AddField(FieldType.Radio, "NewField2", 1, 40, 500, 60, 550);
```

Assim como antes, definimos os itens e os adicionamos ao PDF, mas desta vez eles serão alinhados verticalmente.

## Etapa 6: Salve o documento PDF

Por fim, precisamos salvar o documento PDF modificado.

```csharp
dataDir = dataDir + "HorizontallyAndVerticallyRadioButtons_out.pdf";
formEditor.Save(dataDir);
Console.WriteLine("\nHorizontally and vertically laid out radio buttons successfully.\nFile saved at " + dataDir);
```

Este código salva o PDF com os botões de opção recém-adicionados. Certifique-se de verificar o diretório especificado para o arquivo de saída.

## Conclusão

Criar botões de opção em um PDF usando o Aspose.PDF para .NET é um processo simples. Seguindo os passos descritos neste tutorial, você pode adicionar facilmente botões de opção alinhados horizontal e verticalmente aos seus formulários PDF. Isso não só melhora a interatividade dos seus documentos, como também a experiência geral do usuário. Então, vá em frente e experimente!

## Perguntas frequentes

### O que é Aspose.PDF para .NET?
Aspose.PDF para .NET é uma biblioteca poderosa que permite aos desenvolvedores criar, manipular e converter documentos PDF programaticamente.

### Posso usar o Aspose.PDF gratuitamente?
Sim, o Aspose oferece uma versão de teste gratuita que você pode usar para avaliar a biblioteca. Você pode baixá-la [aqui](https://releases.aspose.com/).

### Como obtenho suporte para o Aspose.PDF?
Você pode obter suporte visitando o [Fórum Aspose](https://forum.aspose.com/c/pdf/10).

### É possível criar outros elementos de formulário com Aspose.PDF?
Com certeza! O Aspose.PDF suporta vários elementos de formulário, incluindo campos de texto, caixas de seleção e menus suspensos.

### Onde posso comprar o Aspose.PDF para .NET?
Você pode comprar Aspose.PDF para .NET no [página de compra](https://purchase.aspose.com/buy).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}