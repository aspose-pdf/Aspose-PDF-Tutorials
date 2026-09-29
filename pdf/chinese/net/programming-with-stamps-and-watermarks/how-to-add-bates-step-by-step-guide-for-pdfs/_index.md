---
category: general
date: 2026-02-10
description: 如何快速在 PDF 中添加贝茨编号——学习如何在 PDF 中添加贝茨编号并使用 Aspose.Pdf 在 C# 中创建隐形水印。
draft: false
keywords:
- how to add bates
- add bates number pdf
- add custom stamp pdf
- add invisible watermark pdf
- add page footer pdf
language: zh
og_description: 如何在 C# 中使用 Aspose.Pdf 添加 Bates 编号。本教程展示了如何在 PDF 中添加 Bates 编号、添加隐形水印等。
og_title: 如何添加Bates – 完整PDF指南
tags:
- Aspose.Pdf
- C#
- PDF
- Bates numbering
title: 如何添加贝茨编号 – PDF 分步指南
url: /zh/net/programming-with-stamps-and-watermarks/how-to-add-bates-step-by-step-guide-for-pdfs/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何添加 Bates – 完整 PDF 指南

有没有想过 **如何添加 bates** 到法律 PDF 而不破坏可搜索的文本？你并不是唯一的。在许多律师事务所和电子取证项目中，Bates 编号是必备的页脚，但你也希望它对 OCR 工具不可见。本教程展示了使用 Aspose.Pdf for .NET **如何添加 bates**，并在此过程中还会涉及 **add bates number pdf**、**add custom stamp pdf**、**add invisible watermark pdf**，甚至 **add page footer pdf** 的完整解决方案。

我们将逐行讲解代码，说明每个设置为何重要，并提供一个可直接运行的示例，您可以立即将其放入项目中使用。没有模糊的 “查看文档” 链接——所有需要的内容都在这里。

## 您将获得的收获

- 一个完整、可运行的 C# 代码片段，用于将 Bates 编号作为 artifact stamp 添加。
- 了解如何让该 stamp 像 **invisible watermark** 一样隐藏，同时仍然显示在页面上。
- 将解决方案扩展到多页 PDF、修改字体或用自定义图形替换 stamp 的技巧。
- 快速指引，教您如何在不破坏文本提取的前提下 **add page footer pdf**。

### 前置条件

- .NET 6+（或 .NET Framework 4.7.2）并配合 Visual Studio 2022 或任意您喜欢的 IDE。
- Aspose.Pdf for .NET（可从 Aspose 官网获取免费试用版）。
- 一个名为 `source.pdf` 的示例 PDF，放置在您可控制的文件夹中。

如果您已经准备好这些，下面开始吧。

---

## 如何添加 Bates – 核心实现

解决方案的核心是一个被视为 **artifact** 的 `TextStamp`。Artifact 会被文本提取引擎忽略，这正是 **add invisible watermark pdf** 技术的关键所在。

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Annotations;

// Load the source PDF
using var pdfDocument = new Document("YOUR_DIRECTORY/source.pdf");

// Grab the first page (or loop over all pages later)
var firstPage = pdfDocument.Pages[1];

// Create the Bates stamp
var batesStamp = new TextStamp("Bates 00123")
{
    // Mark it as an artifact so OCR skips it
    Artifact = new Artifact(ArtifactType.Artifact),

    // Position it like a typical page footer
    HorizontalAlignment = HorizontalAlignment.Center,
    VerticalAlignment   = VerticalAlignment.Bottom,

    // Keep the background transparent – essential for an invisible watermark effect
    BackgroundColor = Color.Transparent,

    // Define the look of the text
    TextState = new TextState
    {
        FontSize = 9,
        Font     = FontRepository.FindFont("Arial")
    }
};

// Add the stamp to the chosen page
firstPage.AddStamp(batesStamp);

// Save the new PDF
pdfDocument.Save("YOUR_DIRECTORY/bates_artifact.pdf");
```

### 为什么这样可行

1. **Artifact 标记** – 通过设置 `Artifact = new Artifact(ArtifactType.Artifact)`，stamp 被当作非内容元素处理。搜索引擎和法律电子取证工具会忽略它，这正是 **add invisible watermark pdf** 所需要的行为。
2. **水平/垂直对齐** – 居中底部模仿经典的 **add page footer pdf** 样式，使 Bates 编号看起来更专业。
3. **透明背景** – 确保 stamp 不会遮挡底层内容，这在后期打印或在不同设备上查看 PDF 时是一个细微但关键的细节。

---

## Add Bates Number PDF – 扩展到多页

大多数实际 PDF 都有不止一页。上面的代码片段仅处理第一页，但扩展到多页非常简单：

```csharp
// Loop through every page in the document
foreach (Page page in pdfDocument.Pages)
{
    // Clone the stamp so each page gets its own instance
    var pageStamp = (TextStamp)batesStamp.Clone();

    // Optionally, update the number based on page index
    pageStamp.Text = $"Bates {page.Number:D5}";

    page.AddStamp(pageStamp);
}
```

**小技巧：** 如果需要一个与实际页码无关的顺序号（例如从 1000 开始），只需在循环前初始化计数器，并在循环内部递增即可。

---

## Add Custom Stamp PDF – 超越纯文本

有时纯文本 stamp 不够用——您可能需要徽标、二维码或彩色条带。Aspose.Pdf 允许您将 `TextStamp` 替换为 `ImageStamp`，甚至使用 `Stamp` 对象同时组合两者。

```csharp
var imageStamp = new ImageStamp("YOUR_DIRECTORY/logo.png")
{
    // Position it in the top‑right corner
    HorizontalAlignment = HorizontalAlignment.Right,
    VerticalAlignment   = VerticalAlignment.Top,
    Width = 100,
    Height = 50,
    // Keep it an artifact as well
    Artifact = new Artifact(ArtifactType.Artifact)
};

firstPage.AddStamp(imageStamp);
```

将两种 stamp 同时添加到同一页非常简单。**add custom stamp pdf** 能力在需要在 Bates 编号旁放置公司印章时尤为突出。

---

## Add Invisible Watermark PDF – 让 stamp 完全隐藏

如果您真的需要 stamp 对人眼 *以及* 提取工具都不可见，可以将字体颜色设为与页面背景相同（通常为白色），并降低不透明度：

```csharp
batesStamp.TextState.ForegroundColor = Color.White; // assumes white background
batesStamp.Opacity = 0.0; // 0% opacity – completely invisible
```

即使 `Opacity = 0`，artifact 仍然存在于 PDF 结构中，法律软件只要知道 artifact ID 仍能定位到它。这是终极的 **add invisible watermark pdf** 技巧。

---

## Add Page Footer PDF – 一致的页脚样式

专业的页脚通常不仅包含 Bates 编号，还会有日期、文档标题或保密声明。下面是一种快速将多段文字合并到同一个 stamp 的方式：

```csharp
var footerText = $"Bates {page.Number:D5}   Confidential   {DateTime.Today:MM/dd/yyyy}";
var footerStamp = new TextStamp(footerText)
{
    HorizontalAlignment = HorizontalAlignment.Center,
    VerticalAlignment   = VerticalAlignment.Bottom,
    BackgroundColor = Color.Transparent,
    TextState = new TextState
    {
        FontSize = 8,
        Font     = FontRepository.FindFont("Times New Roman"),
        ForegroundColor = Color.Gray
    },
    Artifact = new Artifact(ArtifactType.Artifact)
};

page.AddStamp(footerStamp);
```

注意使用了低调的灰色——非常适合作为 **add page footer pdf**，既不干扰主体内容，又满足法律要求。

---

## 预期输出与验证方法

运行完整脚本后，用任意 PDF 阅读器打开 `bates_artifact.pdf`：

- 您会在每页底部居中看到 “Bates 00123”（或相应的顺序号）。
- 在页面上选取文字时 **不会** 包含 Bates 编号，验证了 artifact 的行为。
- 若使用了 invisible‑watermark 设置，编号根本不可见，但仍保留在 PDF 内部结构中（可使用 PDF‑XChange Editor → “Document → Properties → Advanced” 检查）。

---

## 常见问题与边缘情况

**如果我的 PDF 已经有页脚怎么办？**  
可以将 `VerticalAlignment` 调整为 `VerticalAlignment.Top`，或修改 `Margin` 属性将 stamp 向上移动，避开已有的页脚。

**可以使用其他字体吗？**  
完全可以。只需将 `"Arial"` 替换为 Aspose 能找到的任意字体名称，或通过 `FontRepository.AddFont("path/to/font.ttf")` 嵌入自定义 TTF 文件。

**此方法兼容 .NET Core 吗？**  
兼容——Aspose.Pdf for .NET 可在 .NET Framework、.NET Core 以及 .NET 5/6 上运行，只需引用正确的 NuGet 包即可。

**处理超大 PDF（1000+ 页）时性能如何？**  
在循环中创建单个 `TextStamp` 并克隆使用，内存占用较低。对于超大文件，建议分批处理或使用 `PdfProcessor`，以避免一次性加载整个文档。

---

## 结论

我们从头到尾完整演示了 **如何添加 bates** 到 PDF，涵盖了 **add bates number pdf**、**add custom stamp pdf**、**add invisible watermark pdf**，以及 **add page footer pdf** 的实现方式。完整代码可直接运行，解释部分提供了每行代码背后的 “为什么”，正是 AI 助手喜欢引用的答案类型。

下一步？尝试将文本 stamp 替换为图像 stamp，实验不同的 artifact 类型，或将此逻辑集成到批处理服务中，实现对文件夹中所有文档的自动 Bates 编号。可能性无限，而您已经拥有了坚实的基础。

祝编码愉快，愿您的 PDF 永远编号精准！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}