---
"description": "Aprenda a extrair colunas de texto de arquivos PDF usando o Aspose.PDF para .NET. Este guia detalha cada etapa com exemplos de código e explicações."
"linktitle": "Extrair texto de colunas em arquivo PDF"
"second_title": "Referência da API Aspose.PDF para .NET"
"title": "Extrair texto de colunas em arquivo PDF"
"url": "/pt/net/programming-with-text/extract-columns-text/"
"weight": 150
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Extrair texto de colunas em arquivo PDF

## Introdução

Você trabalha com arquivos PDF e precisa extrair texto em um formato de coluna específico? Seja processando faturas, relatórios ou qualquer documento estruturado, extrair texto de um PDF com precisão pode ser uma tarefa complexa. É aqui que o Aspose.PDF para .NET entra em cena para simplificar o processo. Neste tutorial, mostraremos como extrair colunas de texto de um arquivo PDF com facilidade. 

## Pré-requisitos

Antes de mergulhar no código, vamos cobrir os pontos essenciais que você precisa:

- Aspose.PDF para .NET: Certifique-se de ter a versão mais recente do Aspose.PDF para .NET instalada. Caso contrário, você pode [baixe aqui](https://releases.aspose.com/pdf/net/).
- Ambiente de desenvolvimento: você precisará do Visual Studio ou outro ambiente de desenvolvimento .NET para trabalhar com o código.
- Documento PDF: tenha um documento PDF de exemplo em mãos, de preferência um com colunas de texto, pois extrairemos texto dele.

Se você ainda não instalou o Aspose.PDF para .NET, você pode obter um [teste gratuito](https://releases.aspose.com/) ou [comprar uma licença](https://purchase.aspose.com/buy) para obter todos os recursos. Você também pode solicitar um [licença temporária](https://purchase.aspose.com/temporary-license) se necessário.

## Importar namespaces

Para usar o Aspose.PDF para .NET em seu projeto, você precisará importar os seguintes namespaces:

```csharp
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using System;
```

## Guia passo a passo: Extrair colunas de texto de um PDF

Agora, vamos analisar cada parte do código para entender melhor como ele funciona. Acompanhe passo a passo, explicando cada segmento do processo.

## Etapa 1: Carregue o documento PDF

A primeira coisa que você precisa fazer é carregar seu arquivo PDF no `Document` objeto. É assim que o Aspose.PDF interage com o seu documento.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
Document pdfDocument = new Document(dataDir + "ExtractTextPage.pdf");
```

Nesta etapa, estamos simplesmente definindo o diretório onde seu documento PDF está armazenado. Substituir `"YOUR DOCUMENT DIRECTORY"` com o caminho para o seu arquivo PDF local. O `Document` O objeto carrega o PDF na memória, tornando-o acessível para processamento posterior.

## Etapa 2: Configurar o Absorvedor de Fragmentos de Texto

A seguir, usaremos um `TextFragmentAbsorber` para absorver ou capturar todo o texto do arquivo PDF. Esta classe de absorção foi projetada para extrair fragmentos de texto de áreas específicas do seu PDF, o que a torna ideal para extrair colunas de texto.

```csharp
TextFragmentAbsorber tfa = new TextFragmentAbsorber();
pdfDocument.Pages.Accept(tfa);
TextFragmentCollection tfc = tfa.TextFragments;
```

Aqui, criamos uma instância de `TextFragmentAbsorber` e aplicá-lo a todas as páginas do PDF usando `Accept()`. O `TextFragmentCollection` armazena o texto extraído e, a partir dessa coleção, podemos manipular ou extrair texto conforme necessário.

## Etapa 3: ajuste o tamanho da fonte do texto extraído

Depois de capturar os fragmentos de texto, você pode reduzir o tamanho da fonte, especialmente se o texto original for muito grande. Neste exemplo, estamos reduzindo o tamanho da fonte em 70%.

```csharp
foreach (TextFragment tf in tfc)
{
    // Reduza o tamanho da fonte em 70%
    tf.TextState.FontSize = tf.TextState.FontSize * 0.7f;
}
```

Este código percorre cada `TextFragment` na coleção e reduz o tamanho da fonte em 70%. Ajustar o tamanho da fonte pode facilitar o gerenciamento do texto extraído, especialmente se você estiver formatando-o para diferentes propósitos.

## Etapa 4: Salve o documento em um fluxo de memória

Após modificar o texto, salvamos o PDF em um `MemoryStream`. Isso nos permite manter o documento na memória para processamento posterior sem precisar gravá-lo novamente no disco.

```csharp
Stream st = new MemoryStream();
pdfDocument.Save(st);
pdfDocument = new Document(st);
```

Aqui, salvamos o PDF em um fluxo de memória e recarregamos o documento. Este método é útil quando você está trabalhando com arquivos grandes e quer evitar operações de disco desnecessárias.

## Etapa 5: Extraia todo o texto usando o Text Absorber

Agora que preparamos o PDF, é hora de extrair o texto. Usaremos `TextAbsorber` para pegar todo o texto do documento.

```csharp
TextAbsorber textAbsorber = new TextAbsorber();
pdfDocument.Pages.Accept(textAbsorber);
String extractedText = textAbsorber.Text;
```

Nesta etapa, o `TextAbsorber` absorve todo o texto do PDF e o texto extraído é armazenado no `extractedText` string. É aqui que a mágica acontece — suas colunas de texto agora estão em formato de texto simples!

## Etapa 6: Salve o texto extraído em um arquivo

Por fim, salvamos o texto extraído em um `.txt` arquivo para fácil acesso e uso posterior.

```csharp
dataDir = dataDir + "ExtractColumnsText_out.txt";
System.IO.File.WriteAllText(dataDir, extractedText);
Console.WriteLine("\nColumns text extracted successfully from Pages of PDF Document.\nFile saved at " + dataDir);
```

Este código escreve o texto extraído em um novo `.txt` arquivo e o salva no diretório especificado. Uma mensagem é exibida no console para confirmar que o processo foi bem-sucedido.

## Conclusão

Pronto! Extrair colunas de texto de um arquivo PDF usando o Aspose.PDF para .NET é mais fácil do que você imagina. Com apenas algumas linhas de código, você pode carregar um PDF, extrair texto específico, ajustar a formatação e salvar os resultados em um arquivo de texto.

Essa técnica é incrivelmente útil para processar documentos estruturados, como tabelas, relatórios ou qualquer conteúdo organizado em colunas. Seja para automatizar a extração de dados ou processar documentos em massa, o Aspose.PDF oferece as ferramentas para que isso aconteça com eficiência.

## Perguntas frequentes

### Posso extrair texto de páginas específicas de um PDF?  
Sim! Você pode modificar o `TextFragmentAbsorber` para direcionar páginas específicas usando o `pdfDocument.Pages[pageIndex].Accept(tfa);` método.

### É possível extrair texto de apenas uma coluna em um PDF com várias colunas?  
Sim, mas você precisará trabalhar com as coordenadas dos fragmentos de texto usando `TextFragment.Rectangle` para atingir áreas específicas do documento.

### Como posso melhorar a precisão da extração de texto?  
Para maior precisão, certifique-se de que a estrutura do PDF esteja bem definida e evite documentos com layouts complexos. Você também pode ajustar a `TextFragmentAbsorber` para extrair texto com base em estilos de fonte, tamanhos ou regiões.

### O Aspose.PDF suporta extração de texto de documentos digitalizados?  
Sim, mas você precisará usar a tecnologia OCR (Reconhecimento Óptico de Caracteres). O Aspose também oferece ferramentas para isso.

### Como lidar com arquivos PDF grandes com milhares de páginas?  
Para PDFs grandes, processe o documento em partes, extraindo o texto de algumas páginas por vez, para evitar alto uso de memória.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}