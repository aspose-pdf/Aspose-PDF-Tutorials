---
"description": "Aprenda a adicionar um carimbo de data e hora aos seus arquivos PDF usando o Aspose.PDF para .NET com este guia passo a passo. Perfeito para aprimorar a autenticidade dos documentos."
"linktitle": "Adicionar carimbo de data e hora em arquivo PDF"
"second_title": "Referência da API Aspose.PDF para .NET"
"title": "Adicionar carimbo de data e hora em arquivo PDF"
"url": "/pt/net/programming-with-stamps-and-watermarks/add-date-time-stamp/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Adicionar carimbo de data e hora em arquivo PDF

## Introdução

Quando se trata de gerenciar documentos, especialmente PDFs, adicionar um carimbo de data e hora pode ser um divisor de águas. Seja trabalhando em documentos jurídicos, relatórios de projetos ou faturas, um carimbo de data e hora não só adiciona autenticidade, como também fornece um registro claro de quando o documento foi criado ou modificado. Neste guia, mostraremos o processo de adicionar um carimbo de data e hora a um arquivo PDF usando a biblioteca Aspose.PDF para .NET. 

Este artigo foi elaborado para ser direto e fácil de seguir, então, mesmo que você seja iniciante em programação ou na biblioteca Aspose.PDF, conseguirá implementar este recurso com confiança. Vamos lá!

## Pré-requisitos

Antes de começar, há alguns pré-requisitos que você precisa ter em mente:

1. Visual Studio: Certifique-se de ter o Visual Studio instalado na sua máquina. É aqui que você escreverá e executará seu código.
2. Aspose.PDF para .NET: Você precisa baixar e instalar a biblioteca Aspose.PDF. Você pode encontrar a versão mais recente [aqui](https://releases.aspose.com/pdf/net/).
3. Conhecimento básico de C#: A familiaridade com a programação em C# ajudará você a entender melhor os exemplos, mas não se preocupe se estiver apenas começando; explicaremos tudo passo a passo.
4. Um arquivo PDF: Tenha um arquivo PDF de exemplo pronto. Para o nosso exemplo, usaremos um arquivo chamado `AddTextStamp.pdf`.

Depois de atender a esses pré-requisitos, você estará pronto para começar a adicionar carimbos de data e hora aos seus arquivos PDF!

## Pacotes de importação

Para começar, você precisa importar os namespaces necessários para o seu projeto C#. Veja como fazer:

### Criar um novo projeto

1. Abra o Visual Studio: inicie seu aplicativo Visual Studio.
2. Criar um novo projeto: Selecione “Criar um novo projeto” na tela inicial.
3. Escolha o aplicativo de console: selecione “Aplicativo de console (.NET Framework)” na lista de modelos de projeto.
4. Dê um nome ao seu projeto: Dê um nome ao seu projeto, por exemplo, `PDFDateTimeStamp`.

### Adicionar referência Aspose.PDF

1. Clique com o botão direito do mouse em Referências: No Solution Explorer, clique com o botão direito do mouse na pasta “Referências” do seu projeto.
2. Selecione “Adicionar referência”: Escolha “Adicionar referência” no menu de contexto.
3. Procure por Aspose.PDF: Navegue até o local onde você baixou o Aspose.PDF e selecione-o. Clique em "OK" para adicioná-lo ao seu projeto.

### Importar namespaces necessários

No topo do seu `Program.cs` arquivo, você precisa importar os seguintes namespaces:

```csharp
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using System;
using Aspose.Pdf.Annotations;
```

Agora que tudo está configurado, vamos dividir o processo de adição de um carimbo de data e hora a um arquivo PDF em etapas claras e gerenciáveis.

## Etapa 1: definir o diretório de documentos

Primeiro, você precisa especificar o diretório onde o arquivo PDF está localizado. Isso é crucial porque o código procurará o PDF nesse diretório.

```csharp
// O caminho para o diretório de documentos.
string dataDir = "YOUR DOCUMENT DIRECTORY"; // Substitua pelo seu caminho atual
```

Certifique-se de substituir `YOUR DOCUMENT DIRECTORY` com o caminho real para seu arquivo PDF.

## Etapa 2: Abra o documento PDF

Em seguida, você abrirá o documento PDF onde deseja adicionar o carimbo de data/hora. 

```csharp
// Abrir documento
Document pdfDocument = new Document(dataDir + "AddTextStamp.pdf");
```

Esta linha de código inicializa o `Document` classe e carrega seu arquivo PDF no `pdfDocument` objeto.

## Etapa 3: Crie o Carimbo de Data e Hora

Agora é hora de gerar o registro de data e hora. Você o formatará para ser exibido de uma maneira específica. 

```csharp
string annotationText = DateTime.Now.ToString("MM/dd/yy hh:mm:ss tt ");
```

Aqui, `DateTime.Now` obtém a data e hora atuais e `ToString` formata-o no formato desejado.

## Etapa 4: Crie um carimbo de texto

Com a data e a hora prontas, agora você pode criar um carimbo de texto que será adicionado ao seu PDF.

```csharp
// Criar carimbo de texto
TextStamp textStamp = new TextStamp(annotationText);
```

Esta linha cria uma nova instância de `TextStamp` usando a sequência de data e hora formatada.

## Etapa 5: Definir propriedades do carimbo

Você pode personalizar a aparência e a posição do carimbo. Veja como definir suas propriedades:

```csharp
// Definir propriedades do carimbo
textStamp.BottomMargin = 10;
textStamp.RightMargin = 20;
textStamp.HorizontalAlignment = Aspose.Pdf.HorizontalAlignment.Right;
textStamp.VerticalAlignment = VerticalAlignment.Bottom;
```

Nesta etapa, definimos as margens e alinhamos o carimbo ao canto inferior direito da página do PDF.

## Etapa 6: adicione o carimbo ao PDF

Agora é hora de adicionar o carimbo de texto ao seu documento PDF. 

```csharp
// Adicionar selo à coleção de selos
pdfDocument.Pages[1].AddStamp(textStamp);
```

Esta linha adiciona o carimbo à primeira página do PDF. Você pode alterar o número da página se quiser colocá-lo em uma página diferente.

## Etapa 7: Crie uma anotação de texto livre (opcional)

Se você quiser adicionar uma anotação ao carimbo, você pode criar uma `FreeTextAnnotation` do seguinte modo:

```csharp
DefaultAppearance default_appearance = new DefaultAppearance("Arial", 6, System.Drawing.Color.Black);
FreeTextAnnotation textAnnotation = new FreeTextAnnotation(pdfDocument.Pages[1], new Aspose.Pdf.Rectangle(0, 0, 0, 0), default_appearance);
textAnnotation.Name = "Stamp";
textAnnotation.Accept(new AnnotationSelector(textAnnotation));
textAnnotation.Contents = textStamp.Value;
```

Esta etapa opcional cria uma anotação de texto livre que pode fornecer contexto ou informações adicionais sobre o selo.

## Etapa 8: Configurar a Borda de Anotação

Se você quiser personalizar a borda da sua anotação, você também pode fazer isso:

```csharp
Border border = new Border(textAnnotation);
border.Width = 0;
border.Dash = new Dash(1, 1);
textAnnotation.Border = border;
textAnnotation.Rect = new Aspose.Pdf.Rectangle(0, 0, 0, 0);
pdfDocument.Pages[1].Annotations.Add(textAnnotation);
```

Este trecho de código define a largura da borda como 0, tornando-a invisível, e adiciona a anotação ao PDF.

## Etapa 9: Salve o documento PDF

Por fim, você precisa salvar o documento PDF modificado. 

```csharp
dataDir = dataDir + "AddDateTimeStamp_out.pdf"; // Especifique o nome do arquivo de saída
pdfDocument.Save(dataDir);
Console.WriteLine("\nDate time stamp added successfully.\nFile saved at " + dataDir);
```

Esta linha salva o PDF com o carimbo de data/hora adicionado em um novo arquivo. Você pode verificar o diretório especificado para ver a saída.

## Conclusão

Parabéns! Você adicionou com sucesso um carimbo de data e hora a um arquivo PDF usando o Aspose.PDF para .NET. Este recurso simples, porém eficaz, pode aprimorar seus documentos, tornando-os mais profissionais e fornecendo um registro claro de quando foram criados ou modificados. 

## Perguntas frequentes

### Posso personalizar o formato da data no registro de data e hora?
Sim, você pode modificar o `ToString` método para alterar o formato da data de acordo com sua preferência.

### O Aspose.PDF é gratuito para usar?
O Aspose.PDF oferece um teste gratuito, mas para obter todos os recursos, você precisa adquirir uma licença. Você pode obter uma licença temporária [aqui](https://purchase.aspose.com/temporary-license/).

### Posso adicionar vários carimbos de data/hora a um PDF?
Com certeza! Você pode criar vários `TextStamp` instâncias e adicioná-las a diferentes páginas ou posições no PDF.

### E se eu não tiver o Visual Studio?
Você pode usar qualquer IDE ou editor de texto C#, mas para executar e depurar seu projeto, o Visual Studio é recomendado.

### Onde posso encontrar mais exemplos de uso do Aspose.PDF?
Você pode explorar mais exemplos e tutoriais no [Documentação Aspose.PDF](https://reference.aspose.com/pdf/net/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}