---
"description": "Aprenda a converter PDF para XPS usando o Aspose.PDF para .NET com este guia passo a passo. Perfeito para desenvolvedores e entusiastas do processamento de documentos."
"linktitle": "PDF para XPS"
"second_title": "Referência da API Aspose.PDF para .NET"
"title": "PDF para XPS"
"url": "/pt/net/document-conversion/pdf-to-xps/"
"weight": 220
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# PDF para XPS

## Introdução

No mundo digital de hoje, a necessidade de converter documentos de um formato para outro é mais comum do que nunca. Seja você um desenvolvedor que busca integrar o processamento de documentos ao seu aplicativo ou um profissional que precisa compartilhar arquivos em um formato universalmente aceito, entender como converter arquivos PDF para XPS (XML Paper Specification) pode ser extremamente útil. Neste tutorial, vamos nos aprofundar no processo de conversão de PDF para XPS usando a poderosa biblioteca Aspose.PDF para .NET.

## Pré-requisitos

Antes de começar, há alguns pré-requisitos que você precisa ter em mente:

1. Visual Studio: Certifique-se de ter o Visual Studio instalado na sua máquina. É aqui que você escreverá e executará seu código .NET.
2. .NET Framework: A familiaridade com o .NET Framework é essencial, pois usaremos C# para nossos exemplos.
3. Biblioteca Aspose.PDF: Você precisa ter a biblioteca Aspose.PDF instalada. Você pode baixá-la do site [Página de lançamentos do Aspose PDF para .NET](https://releases.aspose.com/pdf/net/).
4. Conhecimento básico de C#: uma compreensão fundamental da programação em C# ajudará você a acompanhar os exemplos.

## Pacotes de importação

Para começar a usar o Aspose.PDF, você precisa importar os pacotes necessários para o seu projeto. Veja como fazer isso:

1. Abra o Visual Studio: inicie o Visual Studio e crie um novo projeto.
2. Adicionar referência: clique com o botão direito do mouse no seu projeto no Solution Explorer, selecione "Gerenciar pacotes NuGet" e procure por "Aspose.PDF". Instale o pacote no seu projeto.
3. Usando diretivas: No início do seu arquivo C#, inclua a seguinte diretiva using:

```csharp
using System;
using System.IO;
using Aspose.Pdf;
```

Agora que configuramos tudo, vamos dividir o processo de conversão em etapas gerenciáveis.

## Etapa 1: configure seu diretório de documentos

Antes de converter um PDF para XPS, você precisa especificar o diretório onde o arquivo PDF está localizado. Isso é crucial porque o programa precisa saber onde encontrar o arquivo de entrada.

Nesta etapa, você definirá uma variável de string que contém o caminho para o diretório dos seus documentos. Esse caminho deve apontar para o local do seu arquivo PDF.

```csharp
// O caminho para o diretório de documentos.
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

Substituir `"YOUR DOCUMENT DIRECTORY"` com o caminho real na sua máquina onde o arquivo PDF está armazenado.

## Etapa 2: Carregue o documento PDF

Agora que você configurou seu diretório de documentos, o próximo passo é carregar o documento PDF que você deseja converter.

Você criará uma instância do `Document` da biblioteca Aspose.PDF e passe o caminho do seu arquivo PDF para o construtor. Isso carregará o documento PDF na memória.

```csharp
// Carregar documento PDF
Document pdfDocument = new Document(dataDir + "input.pdf");
```

Certifique-se de substituir `"input.pdf"` com o nome do seu arquivo PDF real.

## Etapa 3: Instanciar opções de salvamento do XPS

Antes de salvar o documento no formato XPS, você precisa criar uma instância do `XpsSaveOptions` classe. Esta classe permite especificar várias opções para salvar o documento.

Ao instanciar `XpsSaveOptions`, você pode personalizar a forma como o PDF é convertido para XPS. Para essa conversão básica, você pode usar as configurações padrão.

```csharp
// Instanciar opções de salvamento do XPS
Aspose.Pdf.XpsSaveOptions saveOptions = new Aspose.Pdf.XpsSaveOptions();
```

## Etapa 4: Salve o documento como XPS

Por fim, é hora de salvar o documento PDF carregado como um arquivo XPS. É aqui que a mágica acontece!

Você vai ligar para o `Save` método sobre o `pdfDocument` objeto, passando o nome do arquivo de saída desejado e o `saveOptions` que você criou anteriormente.

```csharp
// Salvar o documento XPS
pdfDocument.Save("PDFToXPS_out.xps", saveOptions);
```

Esta linha de código criará um arquivo XPS chamado `PDFToXPS_out.xps` no diretório do seu projeto.

## Conclusão

Parabéns! Você converteu com sucesso um documento PDF para o formato XPS usando o Aspose.PDF para .NET. Esta biblioteca simples, porém poderosa, permite que você execute diversas tarefas de processamento de documentos com facilidade. Seja convertendo arquivos para melhor compatibilidade ou simplesmente arquivando documentos em um formato diferente, o Aspose.PDF tem tudo o que você precisa.

## Perguntas frequentes

### O que é o formato XPS?
XPS (XML Paper Specification) é um formato de documento desenvolvido pela Microsoft que preserva o layout e a aparência dos documentos.

### Posso converter vários arquivos PDF para XPS de uma só vez?
Sim, você pode percorrer vários arquivos PDF em um diretório e converter cada um para XPS usando o mesmo método.

### O Aspose.PDF é gratuito para usar?
O Aspose.PDF oferece um teste gratuito, mas para a funcionalidade completa, você precisará adquirir uma licença. Você pode encontrar mais detalhes em [página de compra](https://purchase.aspose.com/buy).

### E se eu tiver problemas durante a conversão?
Você pode buscar ajuda na comunidade Aspose em seu [fórum de suporte](https://forum.aspose.com/c/pdf/10).

### Posso obter uma licença temporária para o Aspose.PDF?
Sim, você pode solicitar uma licença temporária para fins de avaliação no [página de licença temporária](https://purchase.aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}