---
category: general
date: 2026-04-12
description: 如何使用 C# 读取 Word 文档并提取特定页面。逐步代码展示加载 .docx、获取第 2 页以及读取 Bates 标记。
draft: false
keywords:
- how to read word document
- extract specific page from word
- C# Word processing
- read .docx page
- document artifact extraction
language: zh
og_description: 如何读取 Word 文档并提取特定页面，完整 C# 示例。学习加载 .docx、定位第 2 页并提取 Bates 编号。
og_title: 如何读取 Word 文档 – 在 C# 中从 Word 提取特定页面
tags:
- C#
- Word
- Document Automation
title: 如何读取 Word 文档并提取特定页面 – C# 指南
url: /zh/net/programming-with-document/how-to-read-word-document-and-extract-specific-page-from-wor/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何读取 Word 文档并提取特定页面 – 完整 C# 教程  

是否曾想过 **如何以编程方式读取 Word 文档** 并只提取所需的部分？也许你正在构建一个案件管理系统，需要从法律简报的第 2 页获取 Bates 编号。在这种情况下，你需要 **提取特定页面**，而不是每次都将整个文件加载到内存中。  

在本指南中，我们将演示一个真实场景的解决方案：加载 `.docx`，选择第二页，定位第一个 “Bates” 工件，并打印其文本。完成后，你将拥有一个可直接放入任何 .NET 项目的自包含、可运行代码片段。没有模糊的 “参考文档” 快捷方式——只有具体代码以及每行代码为何重要的解释。

> **你将学到**  
> * 如何使用流行的 SDK 在 C# 中读取 Word 文档。  
> * 如何使用零基索引 **提取特定页面**。  
> * 如何搜索工件（例如 Bates 编号）并优雅地处理缺失数据。  
> * 边缘情况、性能优化以及进一步扩展的技巧。

## 前置条件  

在开始之前，请确保你具备以下条件：

| 要求 | 为什么重要 |
|------|------------|
| .NET 6.0 或更高（或 .NET Framework 4.7+） | 我们使用的 SDK 目标是 .NET Standard 2.0+。 |
| Visual Studio 2022（或任意你喜欢的 IDE） | 便于调试和 IntelliSense。 |
| **GroupDocs.Annotation for .NET**（如果你更喜欢也可以使用 Aspose.Words）通过 NuGet 安装 | 提供示例中使用的 `Document`、`Page` 和 `Artifact` 类。 |
| 一个示例 Word 文件（`input.docx`），放在名为 `YOUR_DIRECTORY` 的文件夹中 | 本教程假设该文件已存在；你可以替换为自己的路径。 |

你可以使用以下方式添加包：

```bash
dotnet add package GroupDocs.Annotation --version 23.10
```

如果选择 Aspose.Words，API 会有细微差别——但加载文档、访问页面集合以及遍历工件的核心思路保持不变。

![图示如何读取 Word 文档并提取单页](/images/read-word-document.png){: .center alt="展示如何读取 Word 文档的示意图"}

## 步骤实现  

下面我们将解决方案拆分为若干逻辑块。每个块都有明确的标题（便于 AI 索引）以及基于前一步的简短代码片段。

### 1. 如何读取 Word 文档 – 加载文件  

任何文档处理代码的第一步都是打开文件。使用 GroupDocs.Annotation 时，你需要实例化一个 `Document` 对象，并传入 `.docx` 的完整路径。  

```csharp
using GroupDocs.Annotation;
using GroupDocs.Annotation.Models;

// Load the source document (replace YOUR_DIRECTORY with your actual path)
string docPath = Path.Combine("YOUR_DIRECTORY", "input.docx");
Document doc = new Document(docPath);
```

**为什么重要：**  
* 构造函数会解析 Word 文件并在内存中构建页面、注释和工件的表示。  
* 如果文件缺失或损坏，SDK 会抛出描述性的 `FileNotFoundException` 或 `AnnotationException`，你可以在后续捕获。

### 2. 提取特定页面 – 访问目标页面  

Word 文档本身并不提供原生的 “页面” 对象，因为分页取决于布局。SDK 在加载后会将文档渲染为 `Page` 对象集合。页面采用零基索引，所以第 2 页的索引是 1。  

```csharp
// Retrieve the second page (zero‑based index)
int pageIndex = 1; // page 2 in human terms
Page secondPage = doc.Pages[pageIndex];
```

**为何需要这一步：**  
* 直接访问 `doc.Pages[1]` 可以避免在只关心单页时遍历整个文档。  
* 如果文档页数不足，会抛出 `IndexOutOfRangeException`——请在后文的 “错误处理” 中捕获以保持应用稳健。

### 3. 定位 Bates 工件 – 在页面内搜索  

工件是附加在页面上的元数据对象——类似于隐藏的备注，如 Bates 编号、评论或自定义标签。我们将查找第一个 `Subtype` 等于 `"Bates"` 的工件。  

```csharp
// Find the first artifact with subtype "Bates"
Artifact batesArtifact = secondPage.Artifacts
    .FirstOrDefault(a => a.Subtype.Equals("Bates", StringComparison.OrdinalIgnoreCase));
```

**此步骤关键原因：**  
* 使用 `FirstOrDefault` 能在不存在 Bates 工件时返回 `null`，让你决定后续处理方式（记录日志、使用默认值等）。  
* `StringComparison.OrdinalIgnoreCase` 可防止源文档中大小写不一致导致的匹配失败。

### 4. 输出工件文本 – 安全的控制台写入  

现在我们已经拥有（或没有）Bates 工件，只需将其文本显示出来。这相当于真实场景中将结果写入数据库或发送给其他服务的操作。  

```csharp
if (batesArtifact != null)
{
    Console.WriteLine($"Current Bates: {batesArtifact.Text}");
}
else
{
    Console.WriteLine("No Bates artifact found on page 2.");
}
```

**预期结果：**  
在包含第 2 页 Bates 编号的文档上运行程序时，会打印类似以下内容：

```
Current Bates: 2023-00123
```

如果工件缺失，你会看到回退信息，从而避免 `NullReferenceException`。

### 5. 完整可运行示例 – 综合全部代码  

下面是完整的、可直接运行的控制台应用程序。复制粘贴到新的 C# 项目中，恢复 NuGet 包，然后按 **F5** 运行。  

```csharp
using System;
using System.IO;
using System.Linq;
using GroupDocs.Annotation;
using GroupDocs.Annotation.Models;

namespace WordPageExtractor
{
    class Program
    {
        static void Main(string[] args)
        {
            try
            {
                // 1️⃣ Load the source document
                string docPath = Path.Combine("YOUR_DIRECTORY", "input.docx");
                Document doc = new Document(docPath);

                // 2️⃣ Extract specific page from word (page 2 = index 1)
                int pageIndex = 1;
                if (pageIndex >= doc.Pages.Count)
                {
                    Console.WriteLine($"Document only has {doc.Pages.Count} page(s). Cannot access page {pageIndex + 1}.");
                    return;
                }
                Page secondPage = doc.Pages[pageIndex];

                // 3️⃣ Locate the first Bates artifact on that page
                Artifact batesArtifact = secondPage.Artifacts
                    .FirstOrDefault(a => a.Subtype.Equals("Bates", StringComparison.OrdinalIgnoreCase));

                // 4️⃣ Output the result
                if (batesArtifact != null)
                {
                    Console.WriteLine($"Current Bates: {batesArtifact.Text}");
                }
                else
                {
                    Console.WriteLine("No Bates artifact found on page 2.");
                }
            }
            catch (Exception ex)
            {
                // Pro tip: Log the exception details for troubleshooting
                Console.Error.WriteLine($"Error: {ex.Message}");
            }
        }
    }
}
```

**额外代码说明：**  

* **边界检查** – 我们在使用 `pageIndex` 前会与 `doc.Pages.Count` 对比，防止在页数不足的文档上崩溃。  
* **try‑catch 块** – 捕获文件访问错误、权限问题或 SDK 特定异常，提供友好的错误信息，而不是未处理的崩溃。  
* **注释** – 行内注释（`// 1️⃣`）充当视觉锚点，帮助新手快速浏览代码。

### 6. 常见变体与边缘情况  

| 情形 | 代码适配方式 |
|------|--------------|
| **同一页上有多个 Bates 编号** | 使用 `Where(...).Select(a => a.Text)` 获取所有匹配项，然后遍历或拼接。 |
| **需要第 5 页而不是第 2 页** | 将 `int pageIndex = 4;`（记住零基）进行相应修改。 |
| **文档使用不同的工件子类型（例如 “Comment”）** | 将 `FirstOrDefault` 谓词中的 `"Bates"` 替换为 `"Comment"`。 |
| **处理超大文档的性能** | 若 SDK 支持惰性加载，可使用 `Document.LoadPage(pageIndex)` 只加载所需页面。 |
| **在 Linux 上运行 .NET Core** | 确保已安装 GroupDocs.Annotation 的本机依赖（如 `libgdiplus` 用于图像渲染）。 |

### 7. 小技巧与注意事项  

* **专业技巧：** 若批量处理大量文档，复用同一个 `Annotation` 许可证实例，以避免重复的许可证检查。  
* **需留意：** 包含隐藏节（如脚注）的 Word 文件…

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}