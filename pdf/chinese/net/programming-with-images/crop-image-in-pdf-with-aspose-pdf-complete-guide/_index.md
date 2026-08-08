---
category: general
date: 2026-06-08
description: 使用 Aspose.PDF 在 C# 中裁剪 PDF 中的图像。学习如何创建带图像的 PDF、保存带图像的 PDF，以及仅用几行代码将图像添加到
  PDF 中。
draft: false
keywords:
- crop image in pdf
- create pdf with image
- save pdf with image
- how to add image to pdf
- how to crop image pdf
language: zh
og_description: 使用 Aspose.PDF 在 C# 中裁剪 PDF 中的图像。本教程展示了如何创建带图像的 PDF、保存带图像的 PDF，以及快速向
  PDF 添加图像。
og_title: 使用 Aspose.PDF 在 PDF 中裁剪图像 – 完整指南
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Crop image in PDF using Aspose.PDF in C#. Learn how to create PDF with
    image, save PDF with image, and add image to PDF in just a few lines.
  headline: Crop Image in PDF with Aspose.PDF – Complete Guide
  type: TechArticle
- description: Crop image in PDF using Aspose.PDF in C#. Learn how to create PDF with
    image, save PDF with image, and add image to PDF in just a few lines.
  name: Crop Image in PDF with Aspose.PDF – Complete Guide
  steps:
  - name: '**Image stream** – the raw bytes of your picture.'
    text: '**Image stream** – the raw bytes of your picture.'
  - name: '**Placement rectangle** – where on the page the image lives.'
    text: '**Placement rectangle** – where on the page the image lives.'
  - name: '**Crop rectangle** – the portion of the image you actually want to render.'
    text: '**Crop rectangle** – the portion of the image you actually want to render.'
  type: HowTo
tags:
- Aspose.PDF
- C#
- PDF manipulation
- Image processing
title: 使用 Aspose.PDF 在 PDF 中裁剪图像 – 完整指南
url: /zh/net/programming-with-images/crop-image-in-pdf-with-aspose-pdf-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 PDF 中裁剪图像（使用 Aspose.PDF） – 完整指南

是否曾想过在不打开图形编辑器的情况下 **在 PDF 中裁剪图像**？你并不是唯一有此需求的人。在许多报告、发票或电子书中，你只需要图片的一小块——比如徽标的角落或图表的片段，并且希望它直接嵌入 PDF 中。  

本指南将完整演示这一过程：我们将 **创建带图像的 PDF**、**向 PDF 添加图像**，随后使用 Aspose.PDF for C# **在 PDF 中裁剪图像**。最后，你还会了解如何 **保存带图像的 PDF**，以便将文件发送给任何人。

---

## 您需要的环境

- .NET 6.0 或更高版本（代码同样适用于 .NET Framework 4.6+）  
- 已授权或试用版的 **Aspose.PDF for .NET**（通过 NuGet `Install-Package Aspose.PDF` 安装）  
- 磁盘上的图像文件（JPEG/PNG），我们将其命名为 `image.jpg`  
- 任意你喜欢的 IDE（Visual Studio、Rider、VS Code）

就这些。无需额外服务，也不需要外部工具。

---

## 第一步：创建项目并导入命名空间

首先，新建一个控制台应用并引入我们将使用的命名空间。`using` 语句可以让代码更整洁，也便于后续阅读。

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;   // for text fragments if you want captions later
```

> **小贴士：** 如果使用 Visual Studio，右键项目 → *Manage NuGet Packages* → 搜索 “Aspose.PDF” 并安装。该库内部已经实现了图像定位和裁剪功能，无需任何第三方图像库。

---

## 第二步：创建带图像的 PDF

现在我们真正 **创建带图像的 PDF**。下面的代码片段会生成一个全新的 `Document`，添加一个空白页，并准备图像流。

```csharp
// Initialize a new PDF document
Document pdf = new Document();

// Add a blank page – think of it as a clean canvas
Page page = pdf.Pages.Add();

// Open the source image file
using (FileStream imgStream = new FileStream("YOUR_DIRECTORY/image.jpg", FileMode.Open))
{
    // We'll place the whole image first; cropping comes next
    // Define where the image should sit on the page (in points; 1 point = 1/72 inch)
    Rectangle placement = new Rectangle(0, 0, 600, 800); // width=600pt, height=800pt

    // Add the image without cropping yet – just to see the full picture
    page.AddImage(imgStream, placement);
}
```

运行此代码后，你会得到一个 PDF，图片会按照你指定的尺寸拉伸填满页面。这是开始裁剪前的一个良好检查。

---

## 第三步：向 PDF 添加图像（并为裁剪做准备）

如果已经知道确切的裁剪区域，可以跳过全尺寸步骤，直接进入 **向 PDF 添加图像** 的部分。`AddImage` 方法接受三个参数：

1. **Image stream** – 图片的原始字节流。  
2. **Placement rectangle** – 图像在页面上的放置位置。  
3. **Crop rectangle** – 实际想要渲染的图像区域。

下面的紧凑代码一次性完成放置 **和** 裁剪。

```csharp
using (FileStream imgStream = new FileStream("YOUR_DIRECTORY/image.jpg", FileMode.Open))
{
    // Full‑size placement rectangle (you can adjust X/Y if you need margins)
    Rectangle placement = new Rectangle(0, 0, 600, 800);

    // Crop area: upper‑left quarter of the original image
    Rectangle crop = new Rectangle(0, 0, placement.Width / 2, placement.Height / 2);

    // This single line both adds the image and crops it
    page.AddImage(imgStream, placement, crop);
}
```

> **为什么这样可行：** Aspose.PDF 在内部将裁剪矩形映射到图像的像素尺寸，然后只在 `placement` 区域渲染该切片。无需额外的位图处理，从而保持 PDF 文件体积小巧。

---

## 第四步：裁剪 PDF 中的图像 – 高级选项

有时四分之一裁剪并不足够。也许你需要自定义矩形，或希望保持图像的宽高比。下面提供一种更灵活的实现方式：

```csharp
using (FileStream imgStream = new FileStream("YOUR_DIRECTORY/image.jpg", FileMode.Open))
{
    // Placement on the page (centered, 300pt wide, keep original height)
    Rectangle placement = new Rectangle(150, 400, 450, 1200);

    // Suppose you want a 200 × 150 pixel region starting at (50, 30) in the source image
    // First, convert pixel coordinates to points (assuming 72 DPI)
    float dpi = 72f;
    float left   = 50  / dpi * 72; // = 50 points
    float bottom = 30  / dpi * 72; // = 30 points
    float width  = 200 / dpi * 72; // = 200 points
    float height = 150 / dpi * 72; // = 150 points

    Rectangle crop = new Rectangle(left, bottom, left + width, bottom + height);

    page.AddImage(imgStream, placement, crop);
}
```

**边缘情况处理：**  
- **空流（Null streams）** – 如示例所示，始终在 `using` 块中包装 `FileStream`，以防泄漏。  
- **大图像** – 若源图像尺寸过大，考虑将 `placement` 矩形缩小；Aspose 会自动下采样。  
- **透明 PNG** – 库会保留 Alpha 通道，裁剪后的区域仍保持透明。

---

## 第五步：保存带图像的 PDF（并进行验证）

最后，我们 **保存带图像的 PDF**。`Save` 方法会将文档写入磁盘。若你在构建 API，也可以将其流式返回给 Web 客户端。

```csharp
// Save the final PDF to the output folder
pdf.Save("YOUR_DIRECTORY/output.pdf");

// Optional: Open the file automatically (only works on Windows)
System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo
{
    FileName = "YOUR_DIRECTORY/output.pdf",
    UseShellExecute = true
});
```

打开 `output.pdf` 后，你应该只能看到 `image.jpg` 的裁剪部分，且位置正好是你定义的坐标。如果图像出现拉伸，请调整 `placement` 矩形的宽高，使其与裁剪矩形的宽高比保持一致。

---

## 常见问题与注意事项

| 问题 | 解答 |
|----------|--------|
| **可以在同一页上裁剪多张图片吗？** | 完全可以。对每张图片分别调用 `page.AddImage`，并提供各自的放置和裁剪矩形。 |
| **如果我的图片是其他格式（例如 BMP）怎么办？** | Aspose.PDF 原生支持 JPEG、PNG、BMP、GIF 和 TIFF。只需更改文件扩展名即可。 |
| **生产环境是否需要许可证？** | 试用版最多支持 5 页。正式部署请购买许可证以去除水印。 |
| **如何旋转已裁剪的图片？** | 添加图片后，获取 `Image` 对象并设置其 `Rotate` 属性（`Rotate = RotationAngle.Rotate90`）。 |
| **能否使用百分比而非绝对点数进行裁剪？** | 可以——先根据 `image.Width * 0.25` 等计算矩形尺寸，再按步骤 4 的示例转换为点数。 |

---

## 完整示例（可直接复制粘贴）

```csharp
using System;
using System.IO;
using Aspose.Pdf;

namespace CropImageInPdfDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create a new PDF document and add a blank page
            Document pdf = new Document();
            Page page = pdf.Pages.Add();

            // 2️⃣ Open the image that will be placed on the page
            using (FileStream imgStream = new FileStream("YOUR_DIRECTORY/image.jpg", FileMode.Open))
            {
                // 3️⃣ Define where the image will sit on the page (points)
                Rectangle placement = new Rectangle(0, 0, 600, 800);

                // 4️⃣ Define the crop area – upper‑left quarter of the image
                Rectangle crop = new Rectangle(0, 0, placement.Width / 2, placement.Height / 2);

                // 5️⃣ Add the image using both placement and crop rectangles
                page.AddImage(imgStream, placement, crop);
            }

            // (Optional) Save the PDF to verify the result
            pdf.Save("YOUR_DIRECTORY/output.pdf");

            Console.WriteLine("PDF created and image cropped successfully!");
        }
    }
}
```

运行程序，打开 `output.pdf`，你将看到 `image.jpg` 的左上四分之一被渲染在页面左上角。修改 `crop` 矩形的数值即可尝试不同的裁剪效果。

---

## 结论

我们已经完整演示了如何使用 Aspose.PDF for C# **在 PDF 中裁剪图像**。从创建空白文档、**创建带图像的 PDF**、展示 **向 PDF 添加图像**、应用自定义 **裁剪图像的矩形**，到最后 **保存带图像的 PDF**，整个流程一目了然。  

现在，你可以在生成的任何 PDF 中嵌入精确裁剪后的图片——这对发票、营销手册或自动化报表都非常实用。下一步，可以考虑添加文字说明 (`TextFragment`) 或在裁剪图像周围绘制形状以突出显示。  

还有其他场景想了解？欢迎留言，祝编码愉快！

## 接下来你可以学习什么？

以下教程与本指南所示技术紧密相关，帮助你进一步掌握 API 的其他功能，并探索在项目中实现的不同方案。每篇资源都提供完整可运行的代码示例和逐步说明。

- [如何使用 Aspose.PDF for .NET 设置 PDF 中的图像大小](/pdf/english/net/images-graphics/set-image-size-pdf-aspose-dotnet/)
- [如何使用 Aspose.PDF for .NET 为 PDF 添加图像水印：全面指南](/pdf/english/net/images-graphics/add-image-stamp-pdf-aspose-dotnet/)
- [如何使用 Aspose.PDF for .NET 从 PDF 中提取图像信息](/pdf/english/net/images-graphics/extract-image-info-pdf-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}