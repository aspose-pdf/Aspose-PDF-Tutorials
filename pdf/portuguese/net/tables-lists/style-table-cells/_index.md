---
title: Personalize o fundo, as bordas e o preenchimento de células de tabela em PDFs com Aspose.Pdf for .NET
weight: 101
limit:
description: Aprenda como criar um PDF com uma tabela de duas colunas e aplicar cores de fundo, bordas e preenchimento personalizados a cada célula usando Aspose.Pdf for .NET.
keywords: [Aspose.Pdf for .NET, style table cells pdf, pdf table cell background, pdf table cell border, pdf cell padding, Aspose PDF table styling]
url: /net/tables-lists/style-table-cells/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Aprenda como criar um PDF com uma tabela de duas colunas e aplicar
    cores de fundo, bordas e preenchimento personalizados a cada célula usando Aspose.Pdf
    for .NET.
  headline: Personalize o fundo, as bordas e o preenchimento de células de tabela
    em PDFs com Aspose.Pdf for .NET
  type: TechArticle
- description: Aprenda como criar um PDF com uma tabela de duas colunas e aplicar
    cores de fundo, bordas e preenchimento personalizados a cada célula usando Aspose.Pdf
    for .NET.
  name: Personalize o fundo, as bordas e o preenchimento de células de tabela em PDFs
    com Aspose.Pdf for .NET
  steps:
  - name: Crie um novo documento PDF vazio dentro de um bloco using.
    text: Crie um novo documento PDF vazio dentro de um bloco using.
  - name: Adicione uma página em branco ao documento PDF.
    text: Adicione uma página em branco ao documento PDF.
  - name: Instancie um objeto Table com duas colunas de 200 pontos, uma borda externa
      fina preta e um preenchimento padrão de célula de 5 pontos.
    text: Instancie um objeto Table com duas colunas de 200 pontos, uma borda externa
      fina preta e um preenchimento padrão de célula de 5 pontos.
  - name: Adicione a primeira linha à tabela.
    text: Adicione a primeira linha à tabela.
  - name: Crie a primeira célula, insira o texto "First cell", defina um fundo amarelo-claro,
      uma borda vermelha de 2 pontos e uma margem de 4 pontos.
    text: Crie a primeira célula, insira o texto "First cell", defina um fundo amarelo-claro,
      uma borda vermelha de 2 pontos e uma margem de 4 pontos.
  - name: Crie a segunda célula, adicione o texto "Second cell", dê a ela um fundo
      verde-claro, uma borda azul de 2 pontos e uma margem de 4 pontos.
    text: Crie a segunda célula, adicione o texto "Second cell", dê a ela um fundo
      verde-claro, uma borda azul de 2 pontos e uma margem de 4 pontos.
  - name: Adicione a segunda linha à tabela.
    text: Adicione a segunda linha à tabela.
  - name: Crie a terceira célula, insira "Third cell", defina um fundo ciano-claro,
      uma borda cinza-escura de 2 pontos e uma margem de 4 pontos.
    text: Crie a terceira célula, insira "Third cell", defina um fundo ciano-claro,
      uma borda cinza-escura de 2 pontos e uma margem de 4 pontos.
  - name: Crie a quarta célula, adicione "Fourth cell", dê a ela um fundo rosa-claro,
      uma borda roxa de 2 pontos e uma margem de 4 pontos.
    text: Crie a quarta célula, adicione "Fourth cell", dê a ela um fundo rosa-claro,
      uma borda roxa de 2 pontos e uma margem de 4 pontos.
  - name: Adicione a tabela totalmente estilizada à página para que ela fique visível
      no PDF.
    text: Adicione a tabela totalmente estilizada à página para que ela fique visível
      no PDF.
  - name: Salve o documento PDF em um arquivo e feche o bloco using.
    text: Salve o documento PDF em um arquivo e feche o bloco using.
  - name: Imprima uma mensagem de confirmação no console.
    text: Imprima uma mensagem de confirmação no console.
  type: HowTo
- questions:
  - answer: '`DefaultCellPadding` fornece um preenchimento base para cada célula,
      mas se você atribuir um `Margin` (por exemplo, `cellA1.Margin = new MarginInfo(...)`)
      os valores da margem substituem o preenchimento padrão para essa célula específica.'
    question: O `DefaultCellPadding` definido na `Table` afeta as células que também
      têm um `Margin` definido?
  - answer: Sem `Table.Border`, o retângulo externo ao redor de toda a tabela é omitido;
      apenas as bordas individuais das células que você definir (por exemplo, `cellA2.Border`)
      serão visíveis.
    question: Como ficará o PDF se eu remover a propriedade `Border` do objeto `Table`?
  - answer: Sim, crie um `BorderInfo` com um `BorderSide` específico (por exemplo,
      `new BorderInfo(BorderSide.Left, 3, Aspose.Pdf.Color.Black)`) e atribua-o à
      propriedade `Border` da célula.
    question: Posso dar a uma célula uma largura de borda diferente em cada lado?
  - answer: Instancie um novo `Row` com `Row newRow = dataTable.Rows.Add();` e então
      adicione células a `newRow.Cells` da mesma forma que nas linhas anteriores.
    question: Como adiciono uma terceira linha à tabela após o código mostrado?
  type: FAQPage
images:
- /net/tables-lists/style-table-cells/og-image.png
og_title: Estilizar Células de Tabela PDF – Fundo, Borda, Preenchimento
og_description: Formate rapidamente células de tabela em um PDF com cores, bordas e espaçamento personalizados usando Aspose.Pdf for .NET.
og_image_alt: Guia que mostra como estilizar a cor de fundo, a borda e o preenchimento de células de tabela em um PDF usando Aspose.Pdf for .NET
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Personalize o fundo, as bordas e o preenchimento de células de tabela em PDFs com Aspose.Pdf
Neste tutorial você verá como gerar um documento PDF, adicionar uma tabela de duas colunas e controlar precisamente a aparência de cada célula. Definindo cores de fundo, especificando bordas e ajustando o preenchimento, você pode fazer os dados da tabela se destacarem e parecerem refinados. O exemplo usa as classes Aspose.Pdf Document e Table para demonstrar cada opção de estilo.

---

{{< tutorial-widget sourcePath="pdf/net/tables-lists/style-table-cells" >}}


{{< /blocks/products/pf/tutorial-page-section >}}

{{< blocks/products/pf/tutorial-page-section >}}
## Installation Instructions
1. Download Aspose.Pdf for .NET:
   Get the latest version from the [Aspose Downloads page](https://releases.aspose.com/pdf/net/).

2. Install via NuGet:
   - Open your Visual Studio project.
   - Navigate to the NuGet Package Manager (Tools > NuGet Package Manager > Manage NuGet Packages for Solution).
   - Search for "Aspose.Pdf" and click Install.

3. Add Namespace References:
   Add the following namespace at the top of your code file:
   ```csharp
   using Aspose.Pdf;
   using Aspose.Pdf.Devices;
   using Aspose.Pdf.Operators;
   ```

4. Apply License (Optional):
   To use the full version, [apply a license](https://purchase.aspose.com/temporary-license/) or use a [free trial](https://releases.aspose.com/).

## Also See
[Aspose.Pdf for .NET Documentation](https://docs.aspose.com/pdf/net/)
[Aspose.Pdf for .NET References](https://reference.aspose.com/pdf/net/)

## Frequently asked questions

**Q: O `DefaultCellPadding` definido na `Table` afeta as células que também têm um `Margin` definido?**  
A: `DefaultCellPadding` fornece um preenchimento base para cada célula, mas se você atribuir um `Margin` (por exemplo, `cellA1.Margin = new MarginInfo(...)`) os valores da margem substituem o preenchimento padrão para essa célula específica.

**Q: Como ficará o PDF se eu remover a propriedade `Border` do objeto `Table`?**  
A: Sem `Table.Border`, o retângulo externo ao redor de toda a tabela é omitido; apenas as bordas individuais das células que você definir (por exemplo, `cellA2.Border`) serão visíveis.

**Q: Posso dar a uma célula uma largura de borda diferente em cada lado?**  
A: Sim, crie um `BorderInfo` com um `BorderSide` específico (por exemplo, `new BorderInfo(BorderSide.Left, 3, Aspose.Pdf.Color.Black)`) e atribua-o à propriedade `Border` da célula.

**Q: Como adiciono uma terceira linha à tabela após o código mostrado?**  
A: Instancie um novo `Row` com `Row newRow = dataTable.Rows.Add();` e então adicione células a `newRow.Cells` da mesma forma que nas linhas anteriores.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}