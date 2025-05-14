---
"description": "Aprenda a extrair texto de um documento PDF usando o Dispositivo de Texto no Aspose.PDF para .NET."
"linktitle": "Extrair texto usando dispositivo de texto"
"second_title": "Referência da API Aspose.PDF para .NET"
"title": "Extrair texto usando dispositivo de texto"
"url": "/pt/net/programming-with-text/extract-text-using-text-device/"
"weight": 210
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Extrair texto usando dispositivo de texto

## Introdução

Extrair texto de um PDF pode ser complicado, especialmente quando se trata de documentos com vários formatos, fontes incorporadas ou layouts complexos. Mas com o Aspose.PDF para .NET, esse processo se torna muito fácil! Seja para converter páginas de um PDF em texto simples para análise posterior ou simplesmente extrair seções específicas, o Aspose.PDF tem tudo o que você precisa. Neste tutorial, explicaremos passo a passo como extrair texto de um PDF usando a classe TextDevice no Aspose.PDF. Também forneceremos explicações claras para que você possa aplicar os mesmos métodos aos seus próprios projetos com facilidade.

## Pré-requisitos

Antes de começarmos a programar, certifique-se de ter tudo pronto para acompanhar. Aqui está o que você precisa:

1. Aspose.PDF para .NET: Baixe a versão mais recente do [Página de download do Aspose.PDF para .NET](https://releases.aspose.com/pdf/net/).
2. Ambiente de desenvolvimento: Visual Studio ou qualquer outro ambiente de desenvolvimento C#.
3. .NET Framework: certifique-se de que seu projeto tenha como alvo o .NET Framework 4.x ou superior.
4. Arquivo PDF de entrada: um arquivo PDF que você usará para extração de texto. Coloque-o em um diretório em sua máquina (vamos nos referir a ele como `YOUR DOCUMENT DIRECTORY`).

## Pacotes de importação

No início do seu código, você precisará importar os namespaces necessários para trabalhar com o Aspose.PDF:

```csharp
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Devices;
using System;
using System.Text;
```

## Etapa 1: carregue seu documento PDF

Antes de extrair o texto, precisamos carregar o documento PDF na memória. Nesta etapa, você abrirá seu PDF usando o Aspose.PDF. `Document` classe. Isso permitirá que você acesse todas as páginas e o conteúdo do arquivo.

```csharp
// Defina o caminho para o seu documento PDF
string dataDir = "YOUR DOCUMENT DIRECTORY";

// Carregar o documento PDF
Document pdfDocument = new Document(dataDir + "input.pdf");
```

Aqui, estamos usando `Document pdfDocument = new Document(dataDir + "input.pdf");` para carregar o PDF. O `dataDir` A variável contém o caminho do diretório do seu arquivo PDF. Isso nos dará acesso a todo o documento, permitindo-nos percorrer as páginas e extrair conteúdo.

## Etapa 2: Configurar um construtor de strings para armazenamento de texto

Agora que o documento foi carregado, precisamos de uma maneira de armazenar o texto extraído. Para isso, usaremos um `StringBuilder` que permite concatenação eficiente de strings.

```csharp
// StringBuilder para armazenar o texto extraído
StringBuilder builder = new StringBuilder();
```

Inicializamos um `StringBuilder` instância, que coletará o texto extraído de cada página. É uma maneira mais eficiente de lidar com strings grandes em comparação à concatenação de strings comum em um loop.

## Etapa 3: Percorrer as páginas do PDF

Em seguida, percorremos cada página do documento PDF para extrair o texto. Processaremos cada página individualmente usando o `TextDevice` classe, que é responsável por converter o conteúdo PDF para o formato de texto.

```csharp
// Percorrer todas as páginas do PDF
foreach (Page pdfPage in pdfDocument.Pages)
{
    // Processe cada página para extração de texto
}
```

Este loop percorre todas as páginas do PDF (`pdfDocument.Pages`). Para cada página, extrairemos o texto e o adicionaremos ao nosso `StringBuilder`.

## Etapa 4: Extraia o texto de cada página

Agora, configuramos o processo de extração de texto para cada página. Aqui, criaremos um `TextDevice` objeto e usá-lo para processar as páginas do PDF. O `TextDevice` extrai texto bruto ou formatado com base nas opções de extração que definimos.

```csharp
using (MemoryStream textStream = new MemoryStream())
{
    // Crie um dispositivo de texto para extração de texto
    TextDevice textDevice = new TextDevice();
    
    // Defina as opções de extração de texto para o modo 'Puro'
    TextExtractionOptions textExtOptions = new TextExtractionOptions(TextExtractionOptions.TextFormattingMode.Pure);
    textDevice.ExtractionOptions = textExtOptions;

    // Extraia o texto da página atual e salve-o no fluxo de memória
    textDevice.Process(pdfPage, textStream);

    // Converter fluxo de memória em texto
    string extractedText = Encoding.Unicode.GetString(textStream.ToArray());

    // Anexar o texto extraído ao StringBuilder
    builder.Append(extractedText);
}
```

- `TextDevice textDevice = new TextDevice();`: O `TextDevice` A classe é usada para extrair texto do PDF.
- `TextExtractionOptions textExtOptions = new TextExtractionOptions(TextExtractionOptions.TextFormattingMode.Pure);`: Esta opção extrai o texto original sem reter nenhuma formatação, como fontes ou posições. Você também pode usar `TextFormattingMode.Raw` se precisar de mais controle sobre a formatação.
- `textDevice.Process(pdfPage, textStream);`: Isso processa cada página do PDF e armazena o texto extraído em um `MemoryStream`.
- Por fim, convertemos o texto do `MemoryStream` para uma string e anexá-la ao `StringBuilder`.

## Etapa 5: salvar o texto extraído em um arquivo

Após o processamento de todas as páginas, o texto é armazenado no `StringBuilder`O último passo é salvar o texto extraído em um arquivo.

```csharp
// Defina o caminho de saída para o arquivo de texto
dataDir = dataDir + "input_Text_Extracted_out.txt";

// Salve o texto extraído em um arquivo
File.WriteAllText(dataDir, builder.ToString());

Console.WriteLine("\nText extracted successfully from PDF document.\nFile saved at " + dataDir);
```

- `File.WriteAllText(dataDir, builder.ToString());`:Isso escreve todo o conteúdo do `StringBuilder` em um arquivo de texto.
- O caminho para o arquivo de saída é definido anexando um nome de arquivo (`"input_Text_Extracted_out.txt"`) para o `dataDir` caminho.

## Conclusão

Extrair texto de um PDF usando o Aspose.PDF para .NET é um processo simples e eficiente. Seguindo os passos descritos neste guia, você pode facilmente abrir documentos PDF, navegar pelas páginas e extrair texto para um arquivo de texto. Isso é especialmente útil para processar grandes volumes de dados em PDF, realizar análises de texto ou converter documentos para manipulação posterior.

Com o Aspose.PDF, você não se limita à extração de texto — você pode fazer anotações, manipular imagens ou até mesmo converter PDFs para outros formatos, como HTML ou Word. A flexibilidade e o poder desta biblioteca a tornam uma ferramenta inestimável para o gerenciamento de PDFs em aplicativos .NET.

## Perguntas frequentes

### Aspose.PDF pode extrair texto de PDFs baseados em imagens?
Não, o Aspose.PDF foi projetado para extrair texto de PDFs baseados em conteúdo. Para PDFs baseados em imagens, é necessária a tecnologia OCR.

### O Aspose.PDF mantém a formatação ao extrair texto?
Por padrão, o texto é extraído sem formatação, mas você pode ajustar as opções de extração se quiser manter alguma formatação.

### Posso extrair texto de um intervalo de páginas específico?
Sim, você pode modificar o código para executar um loop em um intervalo específico de páginas em vez de todas as páginas.

### Quais são os modos de extração de texto no Aspose.PDF?
O Aspose.PDF oferece dois modos: Raw e Pure. O modo Raw tenta manter o layout original, enquanto o modo Pure extrai apenas o texto sem formatação.

### O Aspose.PDF para .NET é compatível com o .NET Core?
Sim, o Aspose.PDF para .NET é totalmente compatível com .NET Core e .NET Framework.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}