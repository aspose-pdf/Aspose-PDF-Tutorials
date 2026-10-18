---
category: general
date: 2026-04-06
description: 快速将 JPG 创建为 PDF，并学习如何在 PDF 中裁剪图像、添加新 PDF 页面，以及使用 C# 将 JPG 转换为带裁剪的 PDF。
draft: false
keywords:
- create pdf from jpg
- crop image in pdf
- how to add new pdf page
- convert jpg to pdf with crop
- insert image into pdf c#
language: zh
og_description: 使用 C# 将 JPG 生成 PDF 并在 PDF 中裁剪图像。了解如何添加新 PDF 页面以及在裁剪的情况下将 JPG 转换为 PDF。
og_title: 使用 C# 将 JPG 转换为 PDF – 步骤指南
tags:
- Aspose.Pdf
- C#
- PDF generation
title: 使用 C# 将 JPG 创建为 PDF – 完整指南，包含裁剪和新页面
url: /zh/net/document-conversion/create-pdf-from-jpg-in-c-full-guide-with-cropping-and-new-pa/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中从 JPG 创建 PDF – 完整指南，包含裁剪和新页面

是否曾经需要**从 JPG 创建 PDF**，但不确定如何只保留实际想要的部分？你并不孤单。在许多应用中——比如发票、收据或相册——开发者必须将图片转换为 PDF，同时去除不需要的边缘。

在本教程中，我们将逐步演示一个完整、可直接运行的解决方案，**创建 PDF from JPG**，展示如何**在 PDF 中裁剪图像**，并演示在需要多张图片时**如何添加新 PDF 页面**。结束时，你还将了解如何使用 Aspose.Pdf 库**将 JPG 转换为带裁剪的 PDF**以及**在 C# 中将图像插入 PDF**。

## 你将学到

- 在 .NET 项目中设置 Aspose.Pdf（无需繁重配置）。  
- 加载 JPEG，定义想要保留的区域，并在插入 PDF 页面时进行裁剪。  
- 向同一文档添加额外页面，帮助你从多张图片构建多页 PDF。  
- 保存最终文件并验证输出。  

**先决条件：** .NET 6+（或 .NET Framework 4.6+），Visual Studio 2022 或任意你喜欢的编辑器，以及对 `Aspose.Pdf` 的 NuGet 引用。无需其他外部服务。

![Create PDF from JPG example](image.jpg){: .align-center alt="创建 PDF from JPG 示例，展示裁剪后的图像放置在 PDF 页面上"}

---

## 第 1 步：安装 Aspose.Pdf 并准备项目

首先——添加 Aspose.Pdf 包。在解决方案文件夹的终端中运行：

```bash
dotnet add package Aspose.Pdf
```

这行代码会拉取所有必需的内容：我们稍后会使用的 `Document`、`Rectangle` 和 `Page` 类。根据我的经验，使用 NuGet 是保持最新且无需手动管理 DLL 的最简方式。

> **专业提示：** 如果你针对的是 .NET Framework，请改用 `Aspose.Pdf.NET` 包；API 表面完全相同。

---

## 第 2 步：加载 JPEG 并定义页面尺寸

我们需要一个画布，其尺寸与最终 PDF 页面相匹配。下面的代码创建一个全新的 `Document` 并将源图像作为流打开。

```csharp
using Aspose.Pdf;
using System.IO;

// Create a new PDF document – this will hold our pages.
using var pdfDocument = new Document();

// Open the JPEG you want to convert.
using var imageStream = File.OpenRead(@"C:\Images\photo.jpg");

// Define the full‑size rectangle (the page) – 600 × 800 points works well for most photos.
var pageBounds = new Rectangle(0, 0, 600, 800);
```

为什么使用矩形？在 Aspose.Pdf 中，`Rectangle` 同时表示页面尺寸和你想要显示的图像区域。通过将*页面*与*裁剪区域*分离，你可以细粒度地控制最终在 PDF 中出现的内容。

---

## 第 3 步：选择裁剪区域（左上四分之一）

假设你只需要照片的左上四分之一。我们相对于页面尺寸计算该区域：

```csharp
// Crop the upper‑left quarter of the image.
var cropArea = new Rectangle(
    pageBounds.LLX,                                 // left X (0)
    pageBounds.LLY + pageBounds.Height / 2,         // bottom Y (halfway up)
    pageBounds.LLX + pageBounds.Width / 2,          // right X (halfway across)
    pageBounds.URY);                                // top Y (full height)
```

`Rectangle` 构造函数接受**左下 X/Y**和**右上 X/Y**值。通过在 `LLY` 上加上高度的一半，我们将裁剪底部向上移动，从而去除图像的下半部分。如果需要不同的部分，请相应调整这些计算。

> **为什么先裁剪再添加？**  
> 在 PDF 端裁剪可以避免在磁盘上创建临时位图，节省 I/O 与内存。Aspose 会为你处理数学运算，结果是一个干净、适合矢量的 PDF。

---

## 第 4 步：添加新页面并插入裁剪后的图像

现在我们真正把图像放到 PDF 页面上。这正是**如何添加新 PDF 页面**关键字发挥作用的地方。

```csharp
// Add a new page to the document.
var page = pdfDocument.Pages.Add();

// Insert the image using both the page bounds and the crop rectangle.
page.AddImage(imageStream, pageBounds, cropArea);
```

`AddImage` 接受三个参数：

1. **Stream** – 源 JPEG。  
2. **Page rectangle** – 定义页面大小（我们的 `pageBounds`）。  
3. **Crop rectangle** – 告诉 Aspose 渲染图像的哪一部分。

如果需要更多页面，只需对每个新的 `imageStream` 重复 `Add` + `AddImage` 模式。这既满足**如何添加新 PDF 页面**的需求，又保持代码整洁。

---

## 第 5 步：保存 PDF 并验证结果

最后一步是一行代码，但不要小看它——保存到正确的路径可确保文件能被任何 PDF 查看器打开。

```csharp
// Save the PDF to disk.
pdfDocument.Save(@"C:\Output\cropped_image.pdf");

// Optional: open the file automatically (Windows only).
System.Diagnostics.Process.Start(@"C:\Output\cropped_image.pdf");
```

打开 `cropped_image.pdf` 时，你应该看到一个单页，里面仅包含原始 JPEG 的左上四分之一，并且在 600 × 800 页面内居中显示。

---

## 完整工作示例（所有步骤合并）

下面是可以直接复制粘贴到控制台应用中的完整程序。只要已安装 Aspose.Pdf 并在指定位置放置 JPEG，即可直接编译运行。

```csharp
using Aspose.Pdf;
using System.IO;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new PDF document.
        using var pdfDocument = new Document();

        // 2️⃣ Open the source JPEG.
        using var imageStream = File.OpenRead(@"C:\Images\photo.jpg");

        // 3️⃣ Define the page size (600 × 800 points).
        var pageBounds = new Rectangle(0, 0, 600, 800);

        // 4️⃣ Calculate the crop area – upper‑left quarter.
        var cropArea = new Rectangle(
            pageBounds.LLX,
            pageBounds.LLY + pageBounds.Height / 2,
            pageBounds.LLX + pageBounds.Width / 2,
            pageBounds.URY);

        // 5️⃣ Add a new page and insert the cropped image.
        var page = pdfDocument.Pages.Add();
        page.AddImage(imageStream, pageBounds, cropArea);

        // 6️⃣ Save the resulting PDF.
        pdfDocument.Save(@"C:\Output\cropped_image.pdf");

        // 7️⃣ (Optional) Open the PDF automatically.
        System.Diagnostics.Process.Start(@"C:\Output\cropped_image.pdf");
    }
}
```

### 预期输出

- **文件：** `cropped_image.pdf`（约 30 KB）。  
- **内容：** 单页，600 × 800 点，显示 `photo.jpg` 的左上四分之一。  
- **行为：** 无失真；图像在裁剪范围内保持原始分辨率。

---

## 常见问题与边缘情况

### 如果我想保留整张图片，而不是四分之一怎么办？

只需将 `cropArea` 设置为等于 `pageBounds`：

```csharp
var cropArea = pageBounds; // No cropping – full image.
```

### 能使用其他页面尺寸吗（例如 A4）？

完全可以。将 `pageBounds` 的值替换为 A4 页面在点单位下的尺寸（595 × 842）：

```csharp
var pageBounds = new Rectangle(0, 0, 595, 842);
```

裁剪矩形可以保持不变，也可以重新计算以匹配新的宽高比。

### 如何为每张图片添加单独的页面？

遍历文件路径集合：

```csharp
foreach (var path in imagePaths)
{
    using var stream = File.OpenRead(path);
    var page = pdfDocument.Pages.Add();
    page.AddImage(stream, pageBounds, pageBounds); // No crop for each image.
}
```

### PNG 或透明度怎么办？

Aspose.Pdf 对 PNG 的处理方式与 JPEG 相同。如果源文件带有 alpha 通道，PDF 将保留它，只要 PDF 版本支持透明度（默认即可）。

### 这在 Linux 上的 .NET Core 能运行吗？

可以。Aspose.Pdf 是跨平台的，只需确保 `imageStream` 指向目标操作系统上的有效文件路径。未使用任何仅限 Windows 的 API。

---

## 提示与最佳实践

- **内存管理：** 始终使用 `using` 语句包装流（如示例所示），以避免文件锁定。  
- **性能：** 若处理数十张图片，考虑复用同一个 `Document` 实例，并对每张图片调用 `pdfDocument.Pages.Add()`。  
- **错误处理：** 将整个过程包裹在 `try/catch` 中，并记录 `PdfException` 以便排查。  
- **质量控制：** Aspose.Pdf 允许通过 `ImageFragment` 设置图像分辨率。对高 DPI 扫描，可设置 `ImageFragment.Resolution = 300;`。  
- **安全性：** 若 PDF 将外部共享，可使用 `pdfDocument.Encrypt("ownerPwd", "userPwd", Permission.All);` 添加加密。

---

## 结论

我们已经介绍了如何在 C# 中**创建 PDF from JPG**，**在 PDF 中裁剪图像**，以及**添加新 PDF 页面**以构建多页文档。相同的模式还能帮助你**将 JPG 转换为带裁剪的 PDF**以及**在 C# 中将图像插入 PDF**，无论是简单收据还是复杂相册，都能轻松应对。

动手试试吧：更改裁剪逻辑、尝试 A4 页面，或将多张图片串联。Aspose.Pdf 库让这些任务变得毫不费力，上述代码是一个可靠、可引用的示例，随时可以粘贴到任何项目中。

---

### 接下来可以做什么？

- **为 PDF 添加文本批注**（例如每张图片下方的说明）。  
- **自动生成目录**，适用于多页 PDF。  
- **合并多个 PDF**，使用 `pdfDocument.Pages.AddRange(otherDoc.Pages);`。  

这些主题都基于你刚刚掌握的基础，继续探索即可。

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}