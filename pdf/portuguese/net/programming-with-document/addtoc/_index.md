---
"description": "Aprenda a adicionar um Sumário a um PDF usando o Aspose.PDF para .NET. Este guia passo a passo simplifica o processo e garante uma navegação fácil nos seus documentos."
"linktitle": "Adicionar TOC ao arquivo PDF"
"second_title": "Referência da API Aspose.PDF para .NET"
"title": "Adicionar TOC ao arquivo PDF"
"url": "/pt/net/programming-with-document/addtoc/"
"weight": 40
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Adicionar TOC ao arquivo PDF

## Introdução

Você já rolou infinitamente por um PDF extenso, desejando que ele tivesse um Sumário bem organizado? Bem, hoje é seu dia de sorte! Neste tutorial, você aprenderá a adicionar um Sumário ao seu arquivo PDF usando o Aspose.PDF para .NET. Seja trabalhando em um relatório complexo, um e-book ou uma proposta comercial, um Sumário pode transformar seu documento em uma obra-prima profissional e navegável.

## Pré-requisitos

Antes de começarmos o código, vamos garantir que você tenha tudo o que precisa:

1. Aspose.PDF para .NET: Certifique-se de ter baixado e instalado a biblioteca Aspose.PDF. Você pode baixá-la em [aqui](https://releases.aspose.com/pdf/net/).
   
2. Ambiente de desenvolvimento: certifique-se de ter um ambiente de desenvolvimento .NET, como o Visual Studio, configurado em sua máquina.

3. Licença: Se você não tiver uma licença, poderá obter uma avaliação gratuita ou solicitar uma licença temporária [aqui](https://purchase.aspose.com/temporary-license/).

## Pacotes de importação

Para começar, certifique-se de importar os namespaces necessários no início do seu arquivo de código. Veja como:

```csharp
using System.IO;
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;
```

Esses namespaces permitem que você acesse funcionalidades específicas do PDF e manipule elementos de texto dentro do seu documento.

Vamos dividir essa tarefa em etapas menores. Cada etapa guiará você pelo processo de criação e inserção de um TOC no seu documento PDF.

## Etapa 1: Carregue o documento PDF

A primeira coisa que precisamos fazer é carregar o arquivo PDF existente onde queremos adicionar o TOC.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
Document doc = new Document(dataDir + "AddTOC.pdf");
```

Nesta etapa, especificamos o caminho para o diretório do documento e carregamos o PDF usando o `Document` objeto. Certifique-se de substituir `"YOUR DOCUMENT DIRECTORY"` com o caminho real para seu arquivo.

## Etapa 2: Insira uma nova página para o TOC

Em seguida, inserimos uma nova página no início do documento PDF. Esta página abrigará o Índice.

```csharp
Page tocPage = doc.Pages.Insert(1);
```

Ao inserir a página TOC no início, garantimos que ela apareça como a primeira coisa que os leitores veem no PDF.

## Etapa 3: Criar um Objeto de Informação TOC

Agora, vamos criar um objeto que representará as informações do sumário. Também adicionaremos um título ao sumário para destacá-lo.

```csharp
TocInfo tocInfo = new TocInfo();
TextFragment title = new TextFragment("Table Of Contents");
title.TextState.FontSize = 20;
title.TextState.FontStyle = FontStyles.Bold;
tocInfo.Title = title;
tocPage.TocInfo = tocInfo;
```

Aqui, definimos o título do TOC como "Índice", aumentamos o tamanho da fonte e o deixamos em negrito para dar ênfase.

## Etapa 4: Definir os elementos do TOC

Nesta etapa, definimos os elementos (ou títulos) que serão exibidos no TOC. Esses elementos ajudarão os leitores a navegar por seções específicas do documento.

```csharp
string[] titles = new string[4];
titles[0] = "First page";
titles[1] = "Second page";
titles[2] = "Third page";
titles[3] = "Fourth page";
```

Criamos uma série de strings que servirão como itens do TOC, correspondendo a diferentes páginas no PDF.

## Etapa 5: Criar títulos de sumário

Agora vem a parte crucial: adicionar títulos ao TOC e vinculá-los às suas respectivas páginas.

```csharp
for (int i = 0; i < 2; i++)
{
    Aspose.Pdf.Heading heading2 = new Aspose.Pdf.Heading(1);
    TextSegment segment2 = new TextSegment();
    heading2.TocPage = tocPage;
    heading2.Segments.Add(segment2);

    heading2.DestinationPage = doc.Pages[i + 2];
    heading2.Top = doc.Pages[i + 2].Rect.Height;
    segment2.Text = titles[i];

    tocPage.Paragraphs.Add(heading2);
}
```

Veja o que está acontecendo:
- Título: Criamos um `Heading` objeto e adicione um `TextSegment` para isso.
- Página de destino: definimos a página para a qual cada título será vinculado.
- Posição superior: especificamos a posição na página para onde o título apontará.
- Texto: Cada título recebe seu respectivo título da matriz que criamos anteriormente.

Este loop cria títulos para os dois primeiros elementos do TOC e os vincula às páginas correspondentes.

## Etapa 6: Salve o PDF com o TOC

Por fim, depois de adicionar todos os elementos do TOC, é hora de salvar o PDF atualizado.

```csharp
dataDir = dataDir + "TOC_out.pdf";
doc.Save(dataDir);
```

O arquivo agora está salvo com o TOC adicionado ao PDF. Parabéns — você adicionou um Índice com sucesso!

## Etapa 7: Mensagem de confirmação

Para informar ao usuário que o processo foi concluído, exibiremos uma mensagem simples no console.

```csharp
Console.WriteLine("\nTOC added successfully to an existing PDF.\nFile saved at " + dataDir);
```

## Conclusão

E pronto! Com o Aspose.PDF para .NET, adicionar um Sumário a um PDF não só é fácil como também personalizável. Seja para criar links de navegação simples ou estruturas complexas, esta ferramenta tem tudo o que você precisa. Então, da próxima vez que estiver trabalhando em um PDF extenso, não se esqueça de adicionar um Sumário para dar um toque profissional!

## Perguntas frequentes

### Posso personalizar a aparência do TOC no Aspose.PDF?  
Sim, você pode personalizar totalmente a aparência do TOC, incluindo estilo, tamanho e alinhamento da fonte.

### Como adiciono subtítulos ao TOC?  
Você pode adicionar subtítulos ajustando o `Heading` nível (por exemplo, `Heading(2)`) para criar um TOC hierárquico.

### É possível atualizar o TOC automaticamente se o documento for alterado?  
Não, o TOC não será atualizado automaticamente. Você precisará recriá-lo se a estrutura do documento mudar.

### Posso vincular entradas do TOC a documentos externos?  
Sim, você pode usar hiperlinks para vincular entradas do TOC a PDFs ou URLs externos.

### O Aspose.PDF suporta TOCs multinível?  
Sim, o Aspose.PDF suporta TOCs multinível para documentos complexos com subseções.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}