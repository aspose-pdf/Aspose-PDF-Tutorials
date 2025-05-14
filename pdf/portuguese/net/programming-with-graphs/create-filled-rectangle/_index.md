---
"description": "Aprenda a criar um retângulo preenchido em um PDF usando o Aspose.PDF para .NET com este tutorial passo a passo. Perfeito para desenvolvedores de todos os níveis."
"linktitle": "Criar retângulo preenchido"
"second_title": "Referência da API Aspose.PDF para .NET"
"title": "Criar retângulo preenchido"
"url": "/pt/net/programming-with-graphs/create-filled-rectangle/"
"weight": 50
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Criar retângulo preenchido

## Introdução

Você já quis criar PDFs visualmente atraentes programaticamente? Se sim, você está no lugar certo! Neste tutorial, vamos mergulhar no mundo do Aspose.PDF para .NET, uma biblioteca poderosa que permite manipular documentos PDF com facilidade. Hoje, vamos nos concentrar na criação de um retângulo preenchido dentro de um arquivo PDF. Seja você um desenvolvedor experiente ou iniciante, este guia o guiará por cada etapa de forma amigável e envolvente. Então, pegue seu chapéu de programador e vamos começar!

## Pré-requisitos

Antes de começarmos a trabalhar no código, há algumas coisas que você precisa ter em mãos:

1. Visual Studio: Certifique-se de ter o Visual Studio instalado na sua máquina. É um IDE fantástico para desenvolvimento .NET.
2. Aspose.PDF para .NET: Você precisará baixar e instalar a biblioteca Aspose.PDF. Você pode encontrá-la [aqui](https://releases.aspose.com/pdf/net/).
3. Conhecimento básico de C#: Um pouco de familiaridade com programação em C# ajudará você a entender melhor os trechos de código.

## Pacotes de importação

Para começar, você precisa importar os pacotes necessários para o seu projeto C#. Veja como fazer isso:

### Criar um novo projeto

Abra o Visual Studio e crie um novo projeto em C#. Você pode escolher um Aplicativo de Console para simplificar.

### Adicionar referência Aspose.PDF

1. Clique com o botão direito do mouse no seu projeto no Solution Explorer.
2. Selecione "Gerenciar pacotes NuGet".
3. Procure por "Aspose.PDF" e instale a versão mais recente.

```csharp
using System.IO;
using System;
using Aspose.Pdf;
```

Agora que configuramos tudo, vamos mergulhar no código!

## Etapa 1: configure seu diretório de documentos

Antes de mais nada, você precisa especificar o caminho onde o PDF será salvo. Isso é crucial porque informa ao programa onde criar o arquivo.

```csharp
// O caminho para o diretório de documentos.
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

Substituir `"YOUR DOCUMENT DIRECTORY"` com o caminho real na sua máquina onde você deseja salvar o PDF.

## Etapa 2: Criar uma instância de documento

seguir, criaremos uma instância do `Document` classe. Esta classe representa o documento PDF com o qual você trabalhará.

```csharp
// Criar instância de documento
Document doc = new Document();
```

Esta linha inicializa um novo documento PDF que podemos manipular.

## Etapa 3: Adicionar uma página ao documento

Agora, vamos adicionar uma página ao nosso documento. Todo PDF precisa de pelo menos uma página, certo?

```csharp
// Adicionar página à coleção de páginas do arquivo PDF
Page page = doc.Pages.Add();
```

Este código adiciona uma nova página ao documento, permitindo-nos desenhar formas nela.

## Etapa 4: Criar uma instância de gráfico

Para desenhar formas, precisamos criar uma `Graph` Por exemplo. Pense em um gráfico como uma tela onde você pode desenhar várias formas.

```csharp
// Criar instância do Graph
Aspose.Pdf.Drawing.Graph graph = new Aspose.Pdf.Drawing.Graph(100.0, 400.0);
```

Aqui, estamos criando um gráfico com largura de 100 e altura de 400.

## Etapa 5: adicione o gráfico à página

Agora que temos nosso gráfico, vamos adicioná-lo à página que criamos anteriormente.

```csharp
// Adicionar objeto gráfico à coleção de parágrafos da instância de página
page.Paragraphs.Add(graph);
```

Esta linha anexa o gráfico à página, deixando-o pronto para desenho.

## Etapa 6: Criar uma instância de retângulo

Em seguida, criaremos um retângulo que queremos preencher com cor.

```csharp
// Criar instância de retângulo
Aspose.Pdf.Drawing.Rectangle rect = new Aspose.Pdf.Drawing.Rectangle(100, 100, 200, 120);
```

Neste código, definimos a posição e o tamanho do retângulo. Os parâmetros representam as coordenadas x e y, largura e altura.

## Etapa 7: especifique a cor de preenchimento

Agora, vamos escolher uma cor para o nosso retângulo. Vamos preenchê-lo com vermelho neste exemplo.

```csharp
// Especificar cor de preenchimento para objeto Graph
rect.GraphInfo.FillColor = Aspose.Pdf.Color.Red;
```

Esta linha define a cor de preenchimento do retângulo como vermelho. Você pode escolher a cor que quiser!

## Etapa 8: adicione o retângulo ao gráfico

Com nosso retângulo pronto, é hora de adicioná-lo ao gráfico.

```csharp
// Adicionar objeto retângulo à coleção de formas do objeto Graph
graph.Shapes.Add(rect);
```

Este código adiciona o retângulo ao gráfico, tornando-o parte do nosso desenho.

## Etapa 9: Salve o documento PDF

Por fim, precisamos salvar nosso documento no diretório especificado.

```csharp
dataDir = dataDir + "CreateFilledRectangle_out.pdf";
// Salvar arquivo PDF
doc.Save(dataDir);
```

Este código salva o arquivo PDF com o nome `CreateFilledRectangle_out.pdf` no diretório que você especificou anteriormente.

## Etapa 10: Mensagem de confirmação

Para nos informar que tudo ocorreu bem, podemos imprimir uma mensagem de confirmação.

```csharp
Console.WriteLine("\nFilled rectangle object created successfully.\nFile saved at " + dataDir);
```

Esta linha exibirá uma mensagem no console, confirmando que o retângulo preenchido foi criado com sucesso.

## Conclusão

E pronto! Você criou com sucesso um retângulo preenchido em um documento PDF usando o Aspose.PDF para .NET. Esta poderosa biblioteca abre um mundo de possibilidades para a manipulação de PDFs, permitindo que você crie documentos incríveis programaticamente. Seja para gerar relatórios, faturas ou qualquer outro tipo de PDF, o Aspose.PDF tem tudo o que você precisa.

## Perguntas frequentes

### O que é Aspose.PDF para .NET?
Aspose.PDF para .NET é uma biblioteca que permite aos desenvolvedores criar, manipular e converter documentos PDF programaticamente.

### Posso usar o Aspose.PDF gratuitamente?
Sim, o Aspose oferece uma versão de teste gratuita que você pode usar para explorar os recursos da biblioteca. Você pode baixá-la [aqui](https://releases.aspose.com/).

### Existe uma maneira de obter suporte para o Aspose.PDF?
Com certeza! Você pode obter suporte através do fórum Aspose [aqui](https://forum.aspose.com/c/pdf/10).

### Como posso comprar o Aspose.PDF?
Você pode comprar Aspose.PDF visitando a página de compra [aqui](https://purchase.aspose.com/buy).

### Que tipos de formas posso criar com o Aspose.PDF?
Você pode criar várias formas, incluindo retângulos, círculos, linhas e muito mais, usando a biblioteca Aspose.PDF.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}