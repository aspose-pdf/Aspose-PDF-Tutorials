---
"description": "Aprenda a exportar dados de uma planilha do Excel para uma tabela em PDF usando o Aspose.PDF para .NET. Tutorial passo a passo com exemplos de código, pré-requisitos e dicas úteis."
"linktitle": "Exportar dados da planilha do Excel para uma tabela"
"second_title": "Referência da API Aspose.PDF para .NET"
"title": "Exportar dados da planilha do Excel para uma tabela"
"url": "/pt/net/programming-with-tables/export-excel-worksheet-data-to-table/"
"weight": 70
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Exportar dados da planilha do Excel para uma tabela

## Introdução

Você já precisou exportar dados de uma planilha do Excel para um arquivo PDF, organizados em formato de tabela? Imagine ter um monte de dados no Excel, mas precisar compartilhá-los como um PDF com aparência profissional. Pode parecer complicado, não é? Mas com o Aspose.PDF para .NET, você pode tornar essa tarefa muito mais fácil. Neste tutorial, mostraremos o processo de exportação de dados de uma planilha do Excel para uma tabela dentro de um documento PDF usando o Aspose.PDF para .NET. Vamos guiá-lo passo a passo, detalhando tudo para que, mesmo que você seja iniciante, se sinta um profissional ao final.

## Pré-requisitos

Antes de começarmos a codificação, vamos configurar algumas coisas:

1. Biblioteca Aspose.PDF para .NET – Certifique-se de ter a versão mais recente instalada. Você pode [baixe aqui](https://releases.aspose.com/pdf/net/).
2. Biblioteca Aspose.Cells para .NET – Você precisará dela para lidar com operações do Excel. Baixe-a em [aqui](https://releases.aspose.com/cells/net/).
3. Ambiente de desenvolvimento .NET – Uma ferramenta como o Visual Studio funcionará perfeitamente para codificação.
4. Arquivo Excel – Tenha um arquivo Excel com os dados que você deseja exportar pronto.

Se você não tem as bibliotecas Aspose.PDF e Aspose.Cells, você pode começar com uma [teste gratuito](https://releases.aspose.com/).

## Pacotes de importação

Para começar, certifique-se de ter instalado as bibliotecas Aspose.PDF e Aspose.Cells no seu projeto. Você pode instalá-las usando o Gerenciador de Pacotes NuGet no Visual Studio.

Veja como importar os pacotes necessários no seu código C#:

```csharp
using System.Data;
using System.IO;
using System.Linq;
```

Agora que os pré-requisitos estão definidos, vamos analisar o processo de exportação de dados de uma planilha do Excel para uma tabela em um documento PDF.

## Etapa 1: Carregar a pasta de trabalho do Excel

Para começar, você precisa carregar sua pasta de trabalho do Excel no programa. Nesta etapa, usaremos o Aspose.Cells para abrir o arquivo do Excel.

```csharp
// O caminho para o diretório de documentos.
string dataDir = "YOUR DOCUMENT DIRECTORY";

// Carregar a pasta de trabalho do Excel
Aspose.Cells.Workbook workbook = new Aspose.Cells.Workbook(new FileStream(dataDir + "newBook1.xlsx", FileMode.Open));
```

Explicação: Aqui, especificamos o caminho do diretório onde nosso arquivo Excel está localizado e carregamos a pasta de trabalho usando `Aspose.Cells.Workbook`. Certifique-se de ajustar `"YOUR DOCUMENT DIRECTORY"` para apontar para o local do seu arquivo.

## Etapa 2: Acesse a primeira planilha

Depois de carregar a pasta de trabalho, precisamos acessar a primeira planilha onde nossos dados estão armazenados.

```csharp
// Acessando a primeira planilha no arquivo Excel
Aspose.Cells.Worksheet worksheet = workbook.Worksheets[0];
```

Explicação: Esta etapa é simples: pegamos a primeira planilha da pasta de trabalho, que contém os dados a serem exportados.

## Etapa 3: Exportar dados para DataTable

Agora, vamos exportar os dados da planilha do Excel para um objeto DataTable, que atuará como intermediário para transferir os dados para o PDF.

```csharp
// Exportando o conteúdo de 7 linhas e 2 colunas começando da 1ª célula para DataTable
DataTable dataTable = worksheet.Cells.ExportDataTable(0, 0, worksheet.Cells.MaxRow + 1, worksheet.Cells.MaxColumn + 1, true);
```

Explicação: A `ExportDataTable` O método extrai os dados a partir da primeira célula da planilha e abrange todas as linhas e colunas. Esses dados são então armazenados em um `DataTable` para uso posterior.

## Etapa 4: Criar um novo documento PDF

Em seguida, precisamos criar um novo documento PDF usando Aspose.PDF.

```csharp
// Instanciar uma instância de Documento
Aspose.Pdf.Document pdfDocument = new Aspose.Pdf.Document();

// Crie uma página na instância do documento
Aspose.Pdf.Page page = pdfDocument.Pages.Add();
```

Explicação: Aqui, inicializamos um novo `Aspose.Pdf.Document` e adicione uma página a ela. Essa página posteriormente conterá a tabela que estamos criando a partir dos dados do Excel.

## Etapa 5: Criar um objeto de tabela em PDF

Vamos criar uma tabela dentro do documento PDF.

```csharp
// Criar um objeto Tabela
Aspose.Pdf.Table table = new Aspose.Pdf.Table();

// Adicione o objeto Table à coleção de parágrafos da página
page.Paragraphs.Add(table);
```

Explicação: Criamos um `Aspose.Pdf.Table` objeto e adicioná-lo à coleção de parágrafos da página, o que garante que a tabela seja exibida na página.

## Etapa 6: definir larguras e bordas das colunas

Tabelas em PDF precisam de larguras de coluna definidas. Também adicionaremos bordas para tornar a tabela mais legível.

```csharp
// Definir larguras de colunas da tabela
table.ColumnWidths = "40 100 100";

// Definir borda de célula padrão
table.DefaultCellBorder = new Aspose.Pdf.BorderInfo(Aspose.Pdf.BorderSide.All, 0.1F);
```

Explicação: Definimos as larguras das três colunas e damos a todas as células uma borda padrão com espessura de `0.1F`.

## Etapa 7: Importar dados do DataTable para a tabela PDF

Agora, é hora de importar os dados do DataTable para nossa tabela PDF.

```csharp
// Importar dados para o objeto Tabela a partir do DataTable
table.ImportDataTable(dataTable, true, 0, 0, dataTable.Rows.Count + 1, dataTable.Columns.Count);
```

Explicação: A `ImportDataTable` método transfere todos os dados do `DataTable` para a tabela PDF. Isso preenche a tabela com os dados da sua planilha do Excel.

## Etapa 8: estilize a linha de cabeçalho

Vamos estilizar a linha de cabeçalho da tabela alterando a cor de fundo, a fonte e o alinhamento.

```csharp
// Pegue a primeira linha da tabela
Aspose.Pdf.Row headerRow = table.Rows[0];

// Definir estilo para a linha de cabeçalho
foreach (Aspose.Pdf.Cell cell in headerRow.Cells)
{
    cell.BackgroundColor = Color.Blue;
    cell.DefaultCellTextState.Font = Aspose.Pdf.Text.FontRepository.FindFont("Helvetica-Oblique");
    cell.DefaultCellTextState.ForegroundColor = Color.Yellow;
    cell.DefaultCellTextState.HorizontalAlignment = Aspose.Pdf.HorizontalAlignment.Center;
}
```

Explicação: Fazemos um loop em todas as células da primeira linha (cabeçalho) e definimos a cor de fundo como azul, a cor do texto como amarelo e alinhamos o texto ao centro.

## Etapa 9: estilize as linhas restantes

Para diferenciar o cabeçalho do restante das linhas, vamos adicionar um estilo diferente para as linhas restantes.

```csharp
for (int i = 1; i <= dataTable.Rows.Count; i++)
{
    foreach (Aspose.Pdf.Cell cell in table.Rows[i].Cells)
    {
        cell.BackgroundColor = Color.Gray;
        cell.DefaultCellTextState.ForegroundColor = Color.White;
    }
}
```

Explicação: Para todas as linhas, exceto o cabeçalho, definimos um fundo cinza e uma cor de texto branca.

## Etapa 10: Salve o documento PDF

Por fim, salve o documento PDF com a tabela.

```csharp
// Salvar o PDF
pdfDocument.Save(dataDir + "Exceldata_toPdf_table.pdf");
```

Explicação: Salvamos o PDF no diretório especificado. Pronto! Seus dados do Excel agora estão dentro de uma tabela PDF com um formato elegante.

## Conclusão

E pronto! Em apenas alguns passos, você exportou dados de uma planilha do Excel para uma tabela dentro de um PDF usando o Aspose.PDF para .NET. Ao detalhar o processo e estilizá-lo ao longo do caminho, você pode personalizar sua saída e garantir que seus dados tenham uma aparência limpa e profissional. Assim, da próxima vez que alguém lhe entregar um arquivo do Excel e pedir um relatório em PDF, você saberá exatamente o que fazer.

## Perguntas frequentes

### Posso personalizar mais a tabela?
Com certeza! Você pode modificar cores, fontes, alinhamento e até adicionar bordas a células específicas.

### O Aspose.PDF para .NET é gratuito?
Oferece um teste gratuito, mas para uso prolongado, você precisará de uma licença. Você pode [compre aqui](https://purchase.aspose.com/buy).

### Posso exportar apenas linhas e colunas específicas?
Sim, você pode modificar os parâmetros no `ExportDataTable` método para exportar intervalos específicos.

### Isso funciona com arquivos grandes do Excel?
Sim, o Aspose.Cells foi projetado para lidar com arquivos grandes do Excel de forma eficiente.

### Como posso adicionar mais páginas ao PDF?
Você pode usar `pdfDocument.Pages.Add()` para adicionar quantas páginas você precisar.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}