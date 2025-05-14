---
"description": "Guia passo a passo para criar um elemento de array com Aspose.PDF para .NET. Gere PDFs dinâmicos com tabelas facilmente."
"linktitle": "Criar elemento de tabela"
"second_title": "Referência da API Aspose.PDF para .NET"
"title": "Criar elemento de tabela"
"url": "/pt/net/programming-with-tagged-pdf/create-table-element/"
"weight": 80
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Criar elemento de tabela

## Introdução

Você já se perguntou como criar e personalizar elementos de tabela em um PDF sem esforço usando .NET? Bem, o Aspose.PDF para .NET é a solução ideal! Seja para automatizar a geração de relatórios ou criar tabelas dinamicamente para vários documentos, o Aspose.PDF oferece uma API avançada para trabalhar com elementos de tabela. Este guia explicará passo a passo como criar uma tabela, estilizá-la e até mesmo garantir que ela atenda aos padrões de conformidade com PDF/UA. Parece empolgante, não é? Vamos direto ao assunto!

## Pré-requisitos

Antes de começar, você precisará de algumas coisas:
1. Aspose.PDF para .NET: Baixe a versão mais recente em [Baixar Aspose.PDF para .NET](https://releases.aspose.com/pdf/net/).
2. Ambiente de desenvolvimento: qualquer IDE compatível com .NET (por exemplo, Visual Studio).
3. Conhecimento básico de C#: recomenda-se familiaridade com programação em C#.

Por fim, não se esqueça da sua licença Aspose.PDF. Se você não tiver uma, pode usar a [teste gratuito](https://releases.aspose.com/) ou solicitar um [licença temporária](https://purchase.aspose.com/temporary-license/) para testar tudo.

## Pacotes de importação

Antes de mais nada, vamos importar os pacotes necessários. Isso nos permitirá trabalhar com todas as classes relevantes para a criação de tabelas em documentos PDF.

```csharp
using Aspose.Pdf.LogicalStructure;
using Aspose.Pdf.Tagged;
using Aspose.Pdf.Text;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

Nesta seção, dividiremos o processo de criação de uma tabela em várias etapas. Cada etapa se concentra em diferentes partes do processo de criação e personalização da tabela.

## Etapa 1: Criar um novo documento PDF

A primeira coisa que precisamos fazer é criar um novo documento PDF. Ele servirá como contêiner para nossa tabela.

```csharp
// O caminho para o diretório de documentos.
string dataDir = "YOUR DOCUMENT DIRECTORY";

// Criar um novo documento PDF
Document document = new Document();
```

Aqui, estamos inicializando uma nova instância do `Document` class, que será nosso arquivo PDF em branco. Não se esqueça de definir o caminho do arquivo!

## Etapa 2: Configurar conteúdo marcado

Em seguida, precisamos habilitar o conteúdo marcado, o que garante a acessibilidade da tabela. PDFs marcados são necessários para a conformidade com o PDF/UA (Acessibilidade Universal).

```csharp
// Habilitar conteúdo marcado
ITaggedContent taggedContent = document.TaggedContent;
taggedContent.SetTitle("Example Table");
taggedContent.SetLanguage("en-US");
```

Esta etapa define o título e o idioma do documento, garantindo que a tabela esteja em conformidade com os padrões de acessibilidade. Ter documentos acessíveis é crucial para a experiência do usuário e para os requisitos legais em alguns setores.

## Etapa 3: Crie o elemento de tabela

Agora vem a parte divertida: criar a mesa em si!

```csharp
// Obter o elemento de estrutura raiz
StructureElement rootElement = taggedContent.RootElement;
TableElement tableElement = taggedContent.CreateTableElement();
rootElement.AppendChild(tableElement);
```

Aqui, estamos usando o `RootElement` do conteúdo marcado para anexar nossa tabela. Isso significa essencialmente adicionar uma tabela como um nó filho à estrutura do documento.

## Etapa 4: personalizar bordas e cabeçalhos de tabela

Você não quer que sua mesa fique sem graça, certo? Vamos dar um toque de estilo!

```csharp
tableElement.Border = new BorderInfo(BorderSide.All, 1.2F, Color.DarkBlue);
TableTHeadElement tableTHeadElement = tableElement.CreateTHead();
TableTBodyElement tableTBodyElement = tableElement.CreateTBody();
TableTFootElement tableTFootElement = tableElement.CreateTFoot();
```

Estamos definindo bordas e adicionando cabeçalhos, corpo e rodapés à tabela. Observe o uso de `BorderInfo` para estilizar as bordas da mesa com uma cor azul escura.

## Etapa 5: adicionar linhas e células à tabela

Agora, vamos preencher nossa tabela com linhas e células. Esta parte do processo é onde definimos o layout da nossa tabela.

### Etapa 5.1: Criar linha de cabeçalho

```csharp
TableTRElement headTrElement = tableTHeadElement.CreateTR();
headTrElement.AlternativeText = "Head Row";
headTrElement.BackgroundColor = Color.LightGray;

for (int colIndex = 0; colIndex < 4; colIndex++)
{
    TableTHElement thElement = headTrElement.CreateTH();
    thElement.SetText($"Head {colIndex}");
    thElement.BackgroundColor = Color.GreenYellow;
    thElement.Border = new BorderInfo(BorderSide.All, 4.0F, Color.Gray);
    thElement.Alignment = HorizontalAlignment.Right;
}
```

Estamos criando uma linha de cabeçalho com 4 colunas e cada célula de cabeçalho é estilizada com uma cor de fundo de `GreenYellow`. Também definimos uma borda e alinhamento para os cabeçalhos.

### Etapa 5.2: Adicionar linhas do corpo

```csharp
for (int rowIndex = 0; rowIndex < 50; rowIndex++)
{
    TableTRElement trElement = tableTBodyElement.CreateTR();
    trElement.AlternativeText = $"Row {rowIndex}";

    for (int colIndex = 0; colIndex < 4; colIndex++)
    {
        TableTDElement tdElement = trElement.CreateTD();
        tdElement.SetText($"Cell [{rowIndex}, {colIndex}]");
        tdElement.BackgroundColor = Color.Yellow;
        tdElement.Alignment = HorizontalAlignment.Center;
    }
}
```

Aqui, estamos criando dinamicamente 50 linhas e 4 colunas, preenchendo-as com texto e estilizando as células. A cor de fundo é amarela, com o texto centralizado.

### Etapa 5.3: Adicionar linha de rodapé

```csharp
TableTRElement footTrElement = tableTFootElement.CreateTR();
footTrElement.AlternativeText = "Foot Row";
footTrElement.BackgroundColor = Color.LightSeaGreen;

for (int colIndex = 0; colIndex < 4; colIndex++)
{
    TableTDElement tdElement = footTrElement.CreateTD();
    tdElement.SetText($"Foot {colIndex}");
    tdElement.Alignment = HorizontalAlignment.Center;
}
```

Para completar a tabela, adicionamos um rodapé com texto centralizado e uma `LightSeaGreen` fundo.

## Etapa 6: Validar a conformidade com PDF/UA

Depois que a tabela for criada, é crucial garantir que o PDF seja compatível com PDF/UA.

```csharp
document.Save(dataDir + "CreateTableElement.pdf");

// Validar a conformidade com PDF/UA
document = new Document(dataDir + "CreateTableElement.pdf");
bool isPdfUaCompliance = document.Validate(dataDir + "table.xml", PdfFormat.PDF_UA_1);
Console.WriteLine($"PDF/UA compliance: {isPdfUaCompliance}");
```

Este snippet salva o arquivo PDF e verifica se ele atende aos padrões de conformidade do PDF/UA. Se o documento estiver em conformidade, ele poderá ser acessado por usuários com deficiência.

## Conclusão

Parabéns! Você criou com sucesso uma tabela totalmente personalizada em PDF usando o Aspose.PDF para .NET. Da estilização da tabela à garantia da compatibilidade com PDF/UA, você agora tem uma base sólida para gerar tabelas dinâmicas em seus documentos PDF. Não se esqueça de explorar os amplos recursos do Aspose.PDF para aprimorar ainda mais seus documentos!

## Perguntas frequentes

### Posso personalizar a fonte e o estilo do texto da tabela?
Sim, o Aspose.PDF permite que você personalize totalmente fontes, estilos de texto e alinhamento usando o `TextState` aula.

### Como adiciono mais colunas ou linhas dinamicamente?
Você pode ajustar o número de colunas ou linhas modificando o `rowIndex` e `colIndex` nos laços.

### É possível mesclar células na tabela?
Sim, você pode usar o `ColSpan` e `RowSpan` propriedades para mesclar células em colunas ou linhas.

### O que é conformidade com PDF/UA?
A conformidade com o PDF/UA garante que o documento seja acessível a usuários com deficiências, aderindo aos padrões internacionais de acessibilidade.

### Como posso testar a conformidade com PDF/UA no Aspose.PDF?
Você pode usar o `Validate` método para verificar se o documento está em conformidade com os padrões PDF/UA.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}