---
"description": "学习如何使用 Aspose.PDF for .NET 将 Excel 工作表数据导出到 PDF 表格。本教程包含代码示例、先决条件和实用技巧。"
"linktitle": "将 Excel 工作表数据导出到表格"
"second_title": "Aspose.PDF for .NET API参考"
"title": "将 Excel 工作表数据导出到表格"
"url": "/zh/net/programming-with-tables/export-excel-worksheet-data-to-table/"
"weight": 70
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 将 Excel 工作表数据导出到表格

## 介绍

您是否曾经需要将 Excel 工作表中的数据导出到 PDF 文件，并以表格形式整齐地排列？想象一下，Excel 中有大量数据，但需要将其以专业的 PDF 格式共享。这听起来很复杂，对吧？但使用 Aspose.PDF for .NET，您可以轻松完成这项任务。在本教程中，我们将引导您使用 Aspose.PDF for .NET 将 Excel 工作表数据导出到 PDF 文档中的表格中。我们将逐步指导您，分解所有内容，以便即使您是新手，最终也能像专业人士一样熟练掌握。

## 先决条件

在深入编码之前，让我们先设置一些东西：

1. Aspose.PDF for .NET Library – 请确保已安装最新版本。您可以 [点击此处下载](https://releases。aspose.com/pdf/net/).
2. Aspose.Cells for .NET Library – 您需要用它来处理 Excel 操作。下载地址： [这里](https://releases。aspose.com/cells/net/).
3. .NET 开发环境 – 像 Visual Studio 这样的工具可以完美地用于编码。
4. Excel 文件 – 准备好包含要导出的数据的 Excel 文件。

如果您没有 Aspose.PDF 和 Aspose.Cells 库，您可以从 [免费试用](https://releases。aspose.com/).

## 导入包

首先，请确保您的项目中已安装 Aspose.PDF 和 Aspose.Cells 库。您可以使用 Visual Studio 中的 NuGet 包管理器安装它们。

以下是如何在 C# 代码中导入必要的包：

```csharp
using System.Data;
using System.IO;
using System.Linq;
```

现在已经设置了先决条件，让我们逐步了解将数据从 Excel 表导出到 PDF 文档中的表格的过程。

## 步骤 1：加载 Excel 工作簿

首先，您需要将 Excel 工作簿加载到程序中。在此步骤中，我们将使用 Aspose.Cells 打开 Excel 文件。

```csharp
// 文档目录的路径。
string dataDir = "YOUR DOCUMENT DIRECTORY";

// 加载 Excel 工作簿
Aspose.Cells.Workbook workbook = new Aspose.Cells.Workbook(new FileStream(dataDir + "newBook1.xlsx", FileMode.Open));
```

说明：在这里，我们指定 Excel 文件所在的目录路径，并使用 `Aspose.Cells.Workbook`确保调整 `"YOUR DOCUMENT DIRECTORY"` 指向您的文件位置。

## 第 2 步：访问第一个工作表

加载工作簿后，我们需要访问存储数据的第一个工作表。

```csharp
// 访问 Excel 文件中的第一个工作表
Aspose.Cells.Worksheet worksheet = workbook.Worksheets[0];
```

说明：这一步很简单——我们从工作簿中获取第一个工作表，其中包含要导出的数据。

## 步骤3：将数据导出到DataTable

现在，让我们将 Excel 表中的数据导出到 DataTable 对象中，该对象将充当将数据传输到 PDF 的中介。

```csharp
// 将从第一个单元格开始的7行2列的内容导出到DataTable
DataTable dataTable = worksheet.Cells.ExportDataTable(0, 0, worksheet.Cells.MaxRow + 1, worksheet.Cells.MaxColumn + 1, true);
```

解释： `ExportDataTable` 方法从工作表的第一个单元格开始提取数据，涵盖所有行和列。然后，这些数据将存储在 `DataTable` 以供进一步使用。

## 步骤 4：创建新的 PDF 文档

接下来，我们需要使用 Aspose.PDF 创建一个新的 PDF 文档。

```csharp
// 实例化 Document 实例
Aspose.Pdf.Document pdfDocument = new Aspose.Pdf.Document();

// 在文档实例中创建页面
Aspose.Pdf.Page page = pdfDocument.Pages.Add();
```

解释：在这里，我们初始化一个新的 `Aspose.Pdf.Document` 并添加一个页面。此页面稍后将包含我们根据 Excel 数据创建的表格。

## 步骤 5：在 PDF 中创建表格对象

让我们继续在 PDF 文档中创建表格。

```csharp
// 创建表对象
Aspose.Pdf.Table table = new Aspose.Pdf.Table();

// 将 Table 对象添加到页面的段落集合中
page.Paragraphs.Add(table);
```

解释：我们创建一个 `Aspose.Pdf.Table` 对象并将其添加到页面的段落集合中，以确保表格显示在页面上。

## 步骤 6：设置列宽和边框

PDF 中的表格需要定义列宽。我们还将添加边框，以提高表格的可读性。

```csharp
// 设置表格的列宽
table.ColumnWidths = "40 100 100";

// 设置默认单元格边框
table.DefaultCellBorder = new Aspose.Pdf.BorderInfo(Aspose.Pdf.BorderSide.All, 0.1F);
```

解释：我们设置三列的宽度，并为所有单元格设置一个厚度为的默认边框 `0。1F`.

## 步骤 7：将数据从 DataTable 导入 PDF 表

现在，是时候将 DataTable 中的数据导入到我们的 PDF 表中了。

```csharp
// 从 DataTable 导入数据到 Table 对象
table.ImportDataTable(dataTable, true, 0, 0, dataTable.Rows.Count + 1, dataTable.Columns.Count);
```

解释： `ImportDataTable` 方法将所有数据从 `DataTable` 到 PDF 表格。这会使用 Excel 工作表中的数据填充表格。

## 步骤 8：设置标题行的样式

让我们通过更改背景颜色、字体和对齐方式来设置表格标题行的样式。

```csharp
// 获取表中的第一行
Aspose.Pdf.Row headerRow = table.Rows[0];

// 设置标题行的样式
foreach (Aspose.Pdf.Cell cell in headerRow.Cells)
{
    cell.BackgroundColor = Color.Blue;
    cell.DefaultCellTextState.Font = Aspose.Pdf.Text.FontRepository.FindFont("Helvetica-Oblique");
    cell.DefaultCellTextState.ForegroundColor = Color.Yellow;
    cell.DefaultCellTextState.HorizontalAlignment = Aspose.Pdf.HorizontalAlignment.Center;
}
```

说明：我们循环遍历第一行（标题）中的所有单元格，并将它们的背景颜色设置为蓝色，文本颜色设置为黄色，并将文本对齐到中心。

## 步骤 9：设置剩余行的样式

为了区分标题和其余行，让我们为其余行添加不同的样式。

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

说明：对于除标题之外的所有行，我们设置灰色背景和白色文本颜色。

## 步骤 10：保存 PDF 文档

最后，将表格保存为PDF文档。

```csharp
// 保存 PDF
pdfDocument.Save(dataDir + "Exceldata_toPdf_table.pdf");
```

解释：我们将 PDF 保存到指定的目录。瞧！您的 Excel 数据现在位于一个格式精美的 PDF 表格中。

## 结论

就这样！只需几步，您就使用 Aspose.PDF for .NET 将 Excel 工作表中的数据导出到 PDF 文件中的表格中。通过分解流程并设置样式，您可以自定义输出，确保数据看起来干净利落、专业高效。这样，下次有人递给您 Excel 文件并要求您提供 PDF 报告时，您就知道该怎么做了。

## 常见问题解答

### 我可以进一步自定义表格吗？
当然！您可以修改颜色、字体、对齐方式，甚至可以为特定单元格添加边框。

### Aspose.PDF for .NET 免费吗？
它提供免费试用，但要长期使用，您需要许可证。您可以 [在这里购买](https://purchase。aspose.com/buy).

### 我可以只导出特定的行和列吗？
是的，您可以修改 `ExportDataTable` 方法导出特定范围。

### 这适用于大型 Excel 文件吗？
是的，Aspose.Cells 旨在高效处理大型 Excel 文件。

### 如何向 PDF 添加更多页面？
您可以使用 `pdfDocument.Pages.Add()` 添加所需数量的页面。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}