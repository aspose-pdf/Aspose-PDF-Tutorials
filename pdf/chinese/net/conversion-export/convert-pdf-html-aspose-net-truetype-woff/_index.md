---
"date": "2025-04-10"
"description": "了解如何使用 Aspose.PDF for .NET 将 PDF 转换为 HTML，同时保留 TrueType (TTF) 和 Web 开放字体格式 (WOFF)。分步指南，包含代码示例。"
"title": "使用 Aspose.PDF for .NET 将 PDF 转换为 HTML&#58; 保留 TTF 和 WOFF 格式的字体"
"url": "/zh/net/conversion-export/convert-pdf-html-aspose-net-truetype-woff/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# 使用 Aspose.PDF for .NET 将 PDF 转换为 HTML：保留 TTF 和 WOFF 格式的字体

## 介绍
在将 PDF 文档转换为 HTML 时，难以保持其原始布局和字体的完整性？转换 PDF 文档并保留其字体可能颇具挑战性，但其实并非如此。有了 **Aspose.PDF for .NET**，您可以轻松将 PDF 文件转换为 HTML 格式，同时确保字体保留为 TrueType (TTF) 或 Web 开放字体格式 (WOFF)。本指南将逐步指导您完成整个过程。

在本教程中，我们将介绍：
- 将 PDF 转换为 HTML 时如何将字体保存为 TTF
- 配置转换以将字体保存为 WOFF
- 转换期间保存所有格式的字体

读完本文，您将全面了解如何使用 Aspose.PDF for .NET 有效地管理字体转换。让我们深入了解开始之前所需的先决条件。

## 先决条件
在使用 Aspose.PDF 将 PDF 转换为 HTML 之前，请确保满足以下要求：

### 所需的库和依赖项
- **Aspose.PDF for .NET**：该库对于在 .NET 应用程序中处理 PDF 文件至关重要。
- **.NET Framework 或 .NET Core/5+**：确保您的开发环境支持这些框架。

### 环境设置要求
确保您的开发环境（例如 Visual Studio）已设置好，可以使用 Aspose.PDF 库。您需要：
- 在 .NET Framework 或 .NET Core/5+ 中创建的项目
- 访问 NuGet 包管理器来安装库

### 知识前提
对 C# 的基本了解和熟悉 .NET 中的文件处理将会很有帮助。

## 设置 Aspose.PDF for .NET
首先，您需要安装 Aspose.PDF 库。您可以通过不同的包管理器来安装：

**.NET CLI：**
```bash
dotnet add package Aspose.PDF
```

**程序包管理器控制台：**
```powershell
Install-Package Aspose.PDF
```

**NuGet 包管理器 UI：**
搜索“Aspose.PDF”并安装最新版本。

### 许可证获取
您可以从 Aspose 获取临时许可证或购买完整许可证。免费试用版允许您无限制地探索所有功能，非常适合进行初步评估。以下是使用许可证设置环境的方法：
1. 请求 [临时执照](https://purchase。aspose.com/temporary-license/).
2. 在执行任何操作之前，使用以下代码片段在您的应用程序中应用许可证：

```csharp
Aspose.Pdf.License license = new Aspose.Pdf.License();
license.SetLicense("Path to your License File");
```

## 实施指南
让我们将实现分解为三个关键功能：将字体保存为 TTF、WOFF 和所有格式。

### 将字体保存为 TTF
**概述**
此功能允许您在将 PDF 文档转换为 HTML 时，将字体保存为 TrueType 格式 (TTF)。这可确保在转换过程中保持字体的视觉完整性。

#### 逐步实施
1. **初始化文档和选项：**
   首先使用 Aspose.PDF 加载您的 PDF 文档 `Document` 课程和设置 `HtmlSaveOptions`。

   ```csharp
   string dataDir = "YOUR_DOCUMENT_DIRECTORY";
   string outFile = Path.GetFullPath(dataDir + "/36192_out.html");
   Document doc = new Document(dataDir + "/input.pdf");

   HtmlSaveOptions saveOptions = new HtmlSaveOptions();
   ```

2. **配置保存选项：**
   设置必要的选项以维护布局并指定字体保存模式。

   ```csharp
   saveOptions.FixedLayout = true; // 保留原始 PDF 布局
   saveOptions.SplitIntoPages = false; // 不要拆分成多个 HTML 文件
   saveOptions.FontSavingMode = HtmlSaveOptions.FontSavingModes.AlwaysSaveAsTTF;
   ```

3. **准备输出目录：**
   确保输出目录已准备好存储链接的字体文件。

   ```csharp
   string linkedFilesFolder = Path.GetDirectoryName(outFile) + "/36192_files";
   if (Directory.Exists(linkedFilesFolder))
   {
       Directory.Delete(linkedFilesFolder, true); // 清除现有文件
   }
   ```

4. **保存文档：**
   最后，使用指定的选项保存您的文档。

   ```csharp
doc.保存（outFile，saveOptions）；
```

### Save Fonts as WOFF
**Overview**
Configuring Aspose.PDF to save fonts in Web Open Font Format (WOFF) is beneficial for web optimization, reducing font file sizes while maintaining quality.

#### Step-by-Step Implementation
1. **Configure Save Options:**
   Initialize `HtmlSaveOptions` and set the font saving mode to WOFF.

   ```csharp
   HtmlSaveOptions woffSaveOptions = new HtmlSaveOptions();
   woffSaveOptions.FontSavingMode = HtmlSaveOptions.FontSavingModes.AlwaysSaveAsWOFF;
   ```

2. **应用保存选项：**
   保存文档时使用这些选项，类似于 TTF 方法。

### 以所有格式保存字体
**概述**
为了确保最大的兼容性和灵活性，您可能希望在转换过程中保存所有可用格式的字体。

#### 逐步实施
1. **初始化文档和选项：**
   加载PDF文档并配置 `HtmlSaveOptions`。

   ```csharp
   string dataDir = "YOUR_DOCUMENT_DIRECTORY";
   Document doc = new Document(dataDir + "/input.pdf");
   HtmlSaveOptions htmlOptions = new HtmlSaveOptions();
   ```

2. **配置保存选项：**
   设置选项以保存所有字体格式并维护布局。

   ```csharp
   htmlOptions.FixedLayout = true;
   htmlOptions.RasterImagesSavingMode = HtmlSaveOptions.RasterImagesSavingModes.AsExternalPngFilesReferencedViaSvg;
   htmlOptions.FontSavingMode = HtmlSaveOptions.FontSavingModes.SaveInAllFormats;
   ```

3. **保存文档：**
   使用这些设置保存您的文档。

   ```csharp
doc.保存（dataDir +“/ThreeSetFonts_out.html”，htmlOptions）；
```

## Practical Applications
Converting PDFs to HTML with font preservation has numerous real-world applications:
1. **Web Publishing**: Ensure that documents retain their original styling when published online.
2. **Content Portability**: Easily move content between desktop and web environments without loss of formatting.
3. **Document Archiving**: Maintain document integrity during long-term storage or migration.

Integration possibilities include embedding these conversions into CMS systems, automated reporting tools, or digital libraries for seamless font management across platforms.

## Performance Considerations
When using Aspose.PDF for .NET, consider the following tips to optimize performance:
- **Memory Management**: Dispose of objects properly and utilize `using` statements where applicable.
- **Batch Processing**: Process documents in batches if dealing with large volumes to prevent memory overflow.
- **Resource Optimization**: Configure options like image compression and font subsetting to reduce file sizes.

## Conclusion
We've explored how to convert PDFs to HTML while preserving fonts using Aspose.PDF for .NET. Whether saving fonts as TTF, WOFF, or all formats, these techniques ensure your documents maintain their original design and readability in web environments. 

For further exploration, consider diving into Aspose's extensive documentation or experimenting with additional conversion features offered by the library.

## FAQ Section
1. **What are the benefits of converting PDFs to HTML using Aspose.PDF?**
   - Maintains document layout and font integrity.
   - Facilitates web publishing and content portability.
2. **Can I convert large PDF files efficiently with Aspose.PDF?**
   - Yes, by optimizing memory usage and processing in batches.
3. **How do I handle licensing for Aspose.PDF?**
   - Obtain a temporary or full license from the [Aspose website](https://purchase.aspose.com/buy).
4. **Is it possible to customize font settings during conversion?**
   - Yes, through various `HtmlSaveOptions`.
5. **What are some common issues when converting PDFs and how can I address them?**
   - Common issues include missing fonts or layout discrepancies. Adjusting save options and ensuring proper licensing can help mitigate these problems.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}