---
"description": "Aprenda a usar o recurso GetDocumentWindow do Aspose.PDF para .NET para recuperar informações sobre as propriedades da janela de um documento PDF."
"linktitle": "Obter janela de documento"
"second_title": "Referência da API Aspose.PDF para .NET"
"title": "Obter janela de documento"
"url": "/pt/net/programming-with-document/getdocumentwindow/"
"weight": 170
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Obter janela de documento

# Introdução

Você trabalha com PDFs e quer ter mais controle sobre como eles aparecem quando abertos? Seja ocultando a barra de menus ou redimensionando a janela para caber na primeira página, o Aspose.PDF para .NET oferece todas as ferramentas necessárias para personalizar o comportamento de um PDF quando aberto em um visualizador. Neste tutorial, vamos explicar como recuperar e manipular as configurações da janela do documento no Aspose.PDF para .NET.


# Pré-requisitos

Antes de começar o tutorial, certifique-se de ter os seguintes pré-requisitos:

- Aspose.PDF para .NET instalado no seu ambiente de desenvolvimento.
  - [Baixe Aspose.PDF para .NET](https://releases.aspose.com/pdf/net/)
- Uma licença válida para Aspose.PDF, ou você pode obter uma [teste gratuito](https://releases.aspose.com/) ou [licença temporária](https://purchase.aspose.com/temporary-license/).
- Noções básicas de .NET e C#.
- Visual Studio ou outro IDE adequado.

# Pacotes de importação

Antes de começar a escrever qualquer código, você precisará importar os pacotes necessários. Abra seu projeto e, no topo do seu arquivo C#, adicione o seguinte namespace:

```csharp
using System.IO;
using System;
using Aspose.Pdf;
```

Isso lhe dará acesso a todas as classes e métodos necessários para manipular documentos PDF usando o Aspose.PDF para .NET.

Agora, vamos analisar o processo de recuperação de diferentes configurações da janela do documento. Para este exemplo, usaremos um arquivo PDF de exemplo chamado `GetDocumentWindow.pdf`.

## Etapa 1: definir o caminho do diretório de documentos

Antes de mais nada, precisamos definir o caminho para o nosso arquivo PDF. É crucial que você tenha o caminho correto para evitar erros durante a execução.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

Aqui, substitua `"YOUR DOCUMENT DIRECTORY"` com o diretório real onde o arquivo PDF está localizado. Este é o seu diretório de trabalho de onde você carregará o documento PDF.

## Etapa 2: Abra o documento PDF

Agora que o caminho do arquivo está definido, o próximo passo é abrir o documento PDF usando o Aspose.PDF. Isso carregará o documento na memória, permitindo que você recupere suas propriedades.

```csharp
Document pdfDocument = new Document(dataDir + "GetDocumentWindow.pdf");
```

Com esta simples linha de código, você carregou com sucesso seu arquivo PDF no `pdfDocument` objeto, que agora permitirá que você acesse todas as suas propriedades.

## Etapa 3: recuperar o status de centralização da janela

A seguir, vamos verificar se a janela do documento deve ser centralizada ao ser aberta. O valor padrão para isso é `false`.

```csharp
Console.WriteLine("CenterWindow : {0}", pdfDocument.CenterWindow);
```

Se a saída for `true`, a janela do documento será aberta no centro da tela. Caso contrário, ela será aberta em sua posição padrão.

## Etapa 4: Verifique a direção do texto

Outro aspecto crucial da aparência de um PDF é a direção do texto, que determina se o texto será lido da esquerda para a direita (L2R) ou da direita para a esquerda (R2L). Você pode obter essa informação usando o seguinte código:

```csharp
Console.WriteLine("Direction : {0}", pdfDocument.Direction);
```

A saída será `L2R` para texto da esquerda para a direita e `R2L` para texto da direita para a esquerda. Esta configuração é especialmente útil para documentos em idiomas como árabe ou hebraico.

## Etapa 5: Exibir o título do documento na janela

A próxima propriedade permite controlar se o título do documento ou o nome do arquivo deve ser exibido na barra de título da janela. Por padrão, esta propriedade é definida como `false`, o que significa que o nome do arquivo será exibido.

```csharp
Console.WriteLine("DisplayDocTitle : {0}", pdfDocument.DisplayDocTitle);
```

Se você quiser que o título do documento seja exibido em vez do nome do arquivo, esta configuração deve ser habilitada.

## Etapa 6: redimensione a janela para caber na primeira página

Às vezes, você pode querer que a janela do documento seja redimensionada automaticamente para caber na primeira página do PDF quando aberta. Veja como verificar se esse recurso está habilitado:

```csharp
Console.WriteLine("FitWindow : {0}", pdfDocument.FitWindow);
```

Por padrão, isso é definido como `false`, o que significa que o tamanho da janela permanecerá o mesmo, independentemente do tamanho da primeira página.

## Etapa 7: Ocultar a barra de menu

Para uma experiência de leitura mais focada, você pode ocultar a barra de menus do aplicativo visualizador. Você pode recuperar essa configuração usando a seguinte linha:

```csharp
Console.WriteLine("HideMenuBar : {0}", pdfDocument.HideMenubar);
```

Isso retornará `true` se a barra de menu estiver oculta e `false` de outra forma.

## Etapa 8: Ocultar a barra de ferramentas

Da mesma forma, você também pode querer ocultar a barra de ferramentas no visualizador de PDF para uma interface de usuário mais limpa. Essa configuração pode ser recuperada da seguinte forma:

```csharp
Console.WriteLine("HideToolBar : {0}", pdfDocument.HideToolBar);
```

Se esta configuração estiver ativada, a barra de ferramentas ficará oculta quando o PDF for aberto.

## Etapa 9: ocultar as barras de rolagem e os elementos da interface do usuário

Se você quiser exibir apenas o conteúdo da página, sem nenhum elemento adicional da interface do usuário, como barras de rolagem, esta configuração controla esse comportamento:

```csharp
Console.WriteLine("HideWindowUI : {0}", pdfDocument.HideWindowUI);
```

Quando definido para `true`, o visualizador de PDF ocultará as barras de rolagem e outros elementos da interface do usuário, deixando apenas o conteúdo do documento.

## Etapa 10: definir o modo de página sem tela cheia

Você pode controlar como o documento aparece ao sair do modo de tela cheia usando o `NonFullScreenPageMode` propriedade. Esta configuração é útil para definir como o usuário deve interagir com o documento em modo de tela não cheia.

```csharp
Console.WriteLine("NonFullScreenPageMode : {0}", pdfDocument.NonFullScreenPageMode);
```

A saída pode ser definida para diferentes modos, como miniaturas, contornos ou painel de anexos.

## Etapa 11: Definir o layout da página

Esta configuração permite controlar a disposição das páginas do documento. Por exemplo, você pode optar por uma visualização de página única ou uma visualização em colunas contínuas:

```csharp
Console.WriteLine("PageLayout : {0}", pdfDocument.PageLayout);
```

Isso dá aos usuários flexibilidade na forma como leem ou visualizam o conteúdo do documento.

## Etapa 12: especificar o modo de página

Finalmente, o `PageMode` A propriedade define como o documento deve ser exibido quando aberto. As opções incluem mostrar miniaturas, entrar no modo de tela cheia ou exibir o painel de anexos.

```csharp
Console.WriteLine("PageMode : {0}", pdfDocument.PageMode);
```

Dependendo das suas necessidades, você pode definir isso para qualquer modo que seja adequado à finalidade do seu PDF.

## Conclusão

Como você pode ver, o Aspose.PDF para .NET oferece ferramentas abrangentes para manipular a exibição dos seus documentos PDF em diversos visualizadores de PDF. Seja para ocultar a barra de ferramentas, centralizar a janela ou controlar a direção do texto, o Aspose.PDF oferece a flexibilidade necessária para aprimorar a experiência de visualização do usuário.

# Perguntas frequentes

### Posso personalizar o nível de zoom inicial do PDF?
Sim, o Aspose.PDF permite que você defina o nível de zoom quando o documento é aberto.

### Como posso bloquear o tamanho da janela de um PDF?
Você pode definir o `FitWindow` propriedade para impedir que a janela seja redimensionada.

### O Aspose.PDF suporta diferentes modos de leitura?
Sim, ele suporta diferentes modos, como tela cheia, miniaturas e anexos.

### É possível ocultar barras de rolagem no visualizador de PDF?
Com certeza, você pode ocultar as barras de rolagem configurando o `HideWindowUI` propriedade para `true`.

### Posso centralizar a janela do documento quando aberta?
Sim, você pode controlar isso configurando o `CenterWindow` propriedade.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}