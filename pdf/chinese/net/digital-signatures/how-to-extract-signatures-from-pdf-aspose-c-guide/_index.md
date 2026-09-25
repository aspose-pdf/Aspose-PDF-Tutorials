---
category: general
date: 2026-04-02
description: 学习如何使用 Aspose.Pdf 在 C# 中提取签名、添加字段、添加空白页 PDF、添加小部件以及保留 PDF 的透明度。
draft: false
keywords:
- how to extract signatures
- how to add field
- add blank page pdf
- how to add widget
- preserve transparency pdf
language: zh
og_description: 如何使用 Aspose.Pdf 从 PDF 中提取签名，并执行添加字段、空白页、小部件以及保留透明度等相关任务。
og_title: 如何从 PDF 中提取签名 – Aspose C# 指南
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: 如何从 PDF 中提取签名 – Aspose C# 指南
url: /zh/net/digital-signatures/how-to-extract-signatures-from-pdf-aspose-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何从 PDF 中提取签名 – Aspose C# 指南

**How to extract signatures from a PDF** 是在自动化合同处理、发票审批或任何依赖数字签名的工作流时的常见需求。  
在本指南中，我们还将演示 **how to add field**、**add blank page PDF**、**how to add widget** 和 **preserve transparency PDF**，使用 Aspose.Pdf .NET 库。

想象一下，每晚你会收到数十个已签名的 PDF；手动打开每个文件来验证签名简直是噩梦。只需几行 C# 代码，你就可以以编程方式提取签名名称，保持原始图形完整，甚至在文档中添加新的表单字段——全部不破坏现有的透明度或色彩配置文件。

> **你将获得：** 一个完整、可运行的示例，能够将 PDF 转换为 PDF/X‑4（保留透明度），提取所有嵌入的签名名称，添加空白页，并创建一个在同一页面上出现两次的文本框表单字段。

## 前提条件

- .NET 6.0 或更高版本（代码同样适用于 .NET Framework）
- Aspose.Pdf for .NET **v25.2** 或更新版本（需要 `GetSignatureNames()`）
- 一个 Visual Studio 项目或任意 C# IDE
- 三个你自行管理的示例 PDF 文件：
  - `source.pdf` – 需要在保持透明度的情况下进行转换的任意 PDF
  - `signed.pdf` – 已经包含数字签名的 PDF
  - （可选）用于输出文件的空文件夹

> **专业提示：** 如果你还没有授权副本，可以从 Aspose 官网申请免费临时许可证。免费模式可用于测试，但会添加水印。

## Step 1 – Preserve Transparency PDF by Converting to PDF/X‑4

将 PDF 扁平化时，透明度和嵌入的色彩配置文件常常会丢失。转换为 **PDF/X‑4** 可以保持这些视觉元素完整，这对印前文档至关重要。

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Facades;

// 1️⃣ Convert source.pdf → PDF/X‑4 (preserves transparency & color profiles)
var conversionOptions = new PdfFormatConversionOptions(
    PdfFormat.PDF_X_4,          // Target format
    ConvertErrorAction.Delete  // Remove pages that cause conversion errors
);

using (var sourceDoc = new Document("YOUR_DIRECTORY/source.pdf"))
{
    sourceDoc.Convert(conversionOptions);
    sourceDoc.Save("YOUR_DIRECTORY/toPdfX4.pdf");
}
```

**为什么重要：**  
PDF/X‑4 是保留实时透明度的图形交换 PDF 的 ISO 标准。通过使用 `PdfFormatConversionOptions`，可以避免将透明对象光栅化的常见陷阱，从而防止文件体积急剧增大并降低质量。

## Step 2 – How to Extract Signatures from a PDF

Aspose 在 25.2 版中引入了 `GetSignatureNames()`，使签名提取只需一行代码。该方法返回分配给每个数字签名字段的逻辑名称数组。

```csharp
using Aspose.Pdf;

// 2️⃣ Pull out every signature name from signed.pdf
using (var signedDoc = new Document("YOUR_DIRECTORY/signed.pdf"))
{
    // Returns strings like "Signature1", "EmployeeSignature", etc.
    string[] signatureNames = signedDoc.GetSignatureNames();   // new method in 25.2

    // Show the names in the console – you could store them in a DB instead
    Console.WriteLine("Found signatures: " + string.Join(", ", signatureNames));
}
```

**预期结果：** 如果 `signed.pdf` 包含名为 *ManagerSig* 和 *ClientSig* 的两个签名，控制台将输出：

```
Found signatures: ManagerSig, ClientSig
```

**边缘情况处理：**  
- 如果 PDF 没有签名，`GetSignatureNames()` 返回空数组——不会抛出异常。  
- 对于签名字段损坏的 PDF，你可以将调用包装在 `try/catch` 中，记录错误而不中止整个流程。

## Step 3 – Add Blank Page PDF and Create a TextBox with Multiple Widgets

添加新页面相对简单，但 **how to add field** 与 **how to add widget** 同时使用时需要一些细微处理。*widget* 是表单字段的可视化表示；你可以将多个 widget 附加到同一个逻辑字段，从而让相同的数据出现在多个位置。

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Forms;

// 3️⃣ Build a fresh document, add a blank page, then a textbox with two widgets
using (var newDoc = new Document())
{
    // ---- Add a blank page -------------------------------------------------
    var page = newDoc.Pages.Add();   // This is the "add blank page pdf" step

    // ---- Define the primary widget (the actual appearance) ---------------
    var textBox = new TextBoxField(page, new Rectangle(100, 600, 300, 650))
    {
        PartialName = "Comments",               // logical name of the field
        Value = "Enter your comment here"       // default value
    };

    // ---- Add a second widget at a different location ----------------------
    var secondWidget = new WidgetAnnotation(page, new Rectangle(100, 500, 300, 550));
    textBox.Widgets.Add(secondWidget); // This is the "how to add widget" part

    // ---- Register the field with the document's form collection -----------
    newDoc.Form.Add(textBox, "Comments");

    // ---- Save the result --------------------------------------------------
    newDoc.Save("YOUR_DIRECTORY/TextBoxMultipleWidgets.pdf");
}
```

**为什么使用多个 widget？**  
假设你需要同一条评论同时出现在合同的正面和背面。将两个 widget 附加到同一字段后，用户在任意位置的修改都会自动同步到另一处。

**常见陷阱：**  
- 忘记将字段添加到 `newDoc.Form` 会导致 widget 在 PDF 查看器中不可见。  
- 为两个 widget 使用相同的矩形坐标会导致它们堆叠在一起——请确保 `Rectangle` 的值不同。

## Step 4 – Putting It All Together: A Full, Runnable Example

下面是一段完整程序，按顺序执行上述所有步骤。将其复制粘贴到新的控制台项目中，调整路径后运行即可。

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Facades;
using Aspose.Pdf.Forms;

namespace AsposePdfDemo
{
    class Program
    {
        static void Main()
        {
            // -----------------------------------------------------------------
            // 1️⃣ Preserve transparency by converting to PDF/X‑4
            // -----------------------------------------------------------------
            var conversionOptions = new PdfFormatConversionOptions(
                PdfFormat.PDF_X_4,
                ConvertErrorAction.Delete);

            using (var sourceDoc = new Document("YOUR_DIRECTORY/source.pdf"))
            {
                sourceDoc.Convert(conversionOptions);
                sourceDoc.Save("YOUR_DIRECTORY/toPdfX4.pdf");
                Console.WriteLine("✅ PDF/X‑4 conversion complete (transparency preserved).");
            }

            // -----------------------------------------------------------------
            // 2️⃣ Extract signature names
            // -----------------------------------------------------------------
            using (var signedDoc = new Document("YOUR_DIRECTORY/signed.pdf"))
            {
                string[] signatureNames = signedDoc.GetSignatureNames(); // new in 25.2
                if (signatureNames.Length == 0)
                    Console.WriteLine("⚠️ No signatures found.");
                else
                    Console.WriteLine("🔍 Found signatures: " + string.Join(", ", signatureNames));
            }

            // -----------------------------------------------------------------
            // 3️⃣ Add a blank page and a textbox with two widgets
            // -----------------------------------------------------------------
            using (var newDoc = new Document())
            {
                // Add a blank page – “add blank page pdf”
                var page = newDoc.Pages.Add();

                // Primary widget for the textbox
                var textBox = new TextBoxField(page, new Rectangle(100, 600, 300, 650))
                {
                    PartialName = "Comments",
                    Value = "Enter your comment here"
                };

                // Second widget – “how to add widget”
                textBox.Widgets.Add(new WidgetAnnotation(page, new Rectangle(100, 500, 300, 550)));

                // Register the field – “how to add field”
                newDoc.Form.Add(textBox, "Comments");

                // Save the final document
                newDoc.Save("YOUR_DIRECTORY/TextBoxMultipleWidgets.pdf");
                Console.WriteLine("✅ Blank page added and textbox with two widgets created.");
            }

            Console.WriteLine("\nAll tasks completed successfully!");
        }
    }
}
```

### 预期输出

运行程序后，你应该会看到类似以下的输出：

```
✅ PDF/X‑4 conversion complete (transparency preserved).
🔍 Found signatures: ManagerSig, ClientSig
✅ Blank page added and textbox with two widgets created.

All tasks completed successfully!
```

打开 `TextBoxMultipleWidgets.pdf`（使用 Adobe Acrobat Reader），你会发现两个标记为 **Comments** 的相同文本框——一个在顶部附近，另一个稍低一些。对其中一个进行输入时，另一个会即时同步更新。

## Frequently Asked Questions (FAQ)

| Question | Answer |
|----------|--------|
| **Can I extract the actual signature bytes?** | `GetSignatureNames()` only returns logical names. To pull the certificate or signature value you need `SignatureField` objects (`document.Form["fieldName"] as SignatureField`). |
| **Does PDF/X‑4 conversion work on encrypted PDFs?** | Yes, as long as you supply the password via `Document.Open(file, password)`. |
| **What if I need more than two widgets?** | Just call `textBox.Widgets.Add()` for each additional `WidgetAnnotation`. |
| **Will the blank page inherit page size from the original PDF?** | The new page uses the default size (A4). You can pass a `Page` object with custom dimensions if needed. |
| **Is the code compatible with .NET Core?** | Absolutely—Aspose.Pdf is cross‑platform. Just reference the NuGet package in your .NET Core project. |

## 结论

在本教程中，我们演示了 **how to extract signatures from PDF** 的实现，同时覆盖了 **how to add field**、**add blank page PDF**、**how to add widget** 与 **preserve transparency PDF** 的使用方法，基于 Aspose.Pdf for C#。现在，你拥有了一套完整的端到端解决方案，可直接嵌入任何文档处理流水线。

准备好迎接下一个挑战了吗？尝试将这些技术与 Aspose 的 OCR 模块结合，以读取扫描的

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}