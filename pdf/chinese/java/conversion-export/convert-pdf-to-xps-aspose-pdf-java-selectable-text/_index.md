---
date: '2026-07-03'
description: 了解如何添加 Aspose PDF Maven 依赖，并使用 Aspose.PDF for Java 将 PDF 转换为可选择文本的 XPS。提供前置条件和常见问题的分步指南。
keywords:
- aspose pdf maven dependency
- how to convert pdf to xps
- java convert pdf xps
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Learn how to add the Aspose PDF Maven dependency and convert PDF to
    XPS with selectable text using Aspose.PDF for Java. Step‑by‑step guide with prerequisites
    and FAQs.
  headline: Aspose PDF Maven Dependency – Convert PDF to XPS (Java)
  type: TechArticle
- description: Learn how to add the Aspose PDF Maven dependency and convert PDF to
    XPS with selectable text using Aspose.PDF for Java. Step‑by‑step guide with prerequisites
    and FAQs.
  name: Aspose PDF Maven Dependency – Convert PDF to XPS (Java)
  steps:
  - name: Load the PDF Document
    text: 'First, load your PDF document from its directory:'
  - name: Configure Save Options
    text: 'Create an instance of `XpsSaveOptions` to set up the XPS conversion options:'
  - name: Save as XPS File
    text: 'Finally, save the document in XPS format to your desired output directory:'
  type: HowTo
- questions:
  - answer: Yes—pass the password to the `Document` constructor or use `Document.open(String
      path, String password)` before conversion.
    question: Can I convert password‑protected PDFs?
  - answer: Absolutely. All vector shapes, images, and text are preserved, and the
      text remains selectable.
    question: Does the XPS retain vector graphics?
  - answer: The trial works without a license but adds a watermark to the output;
      a permanent license removes all restrictions.
    question: Is a license mandatory for the trial version?
  - answer: It processes files in a streaming manner, allowing conversion of PDFs
      with hundreds of pages without loading the entire document into memory.
    question: How does Aspose.PDF handle large files?
  - answer: The library runs on any OS with a compatible JDK, including Windows, Linux,
      and macOS.
    question: Which platforms are supported?
  type: FAQPage
title: Aspose PDF Maven 依赖 – 将 PDF 转换为 XPS（Java）
url: /zh/java/conversion-export/convert-pdf-to-xps-aspose-pdf-java-selectable-text/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}
# Aspose PDF Maven 依赖 – 将 PDF 转换为 XPS（Java）

## 介绍

如果您需要**添加 Aspose PDF Maven 依赖**并将 PDF 文档转换为 XPS，同时保持文本可选择，您来对地方了。本教程将逐步指导您完成所有步骤——从配置 Maven 或 Gradle、加载 PDF、配置 XPS 选项，到最终保存可选择文本的 XPS 文件。完成后，您将拥有一个可在任何 Java 项目中使用的可复用代码片段。

## 快速答案
- **我需要什么依赖？** `com.aspose:aspose-pdf`（Maven）或等效的 Gradle 构件。  
- **XPS 能保留可选择的文本吗？** 是的——Aspose.PDF 会自动保留文本层。  
- **需要哪个 Java 版本？** JDK 8 或更高。  
- **生产环境需要许可证吗？** 需要有效的 Aspose.PDF 许可证才能无限制使用。  
- **转换需要多长时间？** 在标准硬件上，通常对少于 100 页的文件在一秒以内完成。

## 什么是 Aspose PDF Maven 依赖？

`aspose-pdf` Maven 构件提供完整的 Aspose.PDF for Java API，能够在无需外部软件的情况下创建、操作和转换 PDF。将此依赖添加到您的 `pom.xml` 或 `build.gradle` 中会自动拉取所有必需的二进制文件，您可以立即开始编码，无需手动管理 JAR。

## 为什么将 PDF 转换为可选择文本的 XPS？

Aspose.PDF 支持**50 多种输入和输出格式**，并且能够生成保留可搜索、可选择文本层的 XPS 文件。这对于需要档案级文档、精确布局保真或在支持 XPS 的工具中进行后续编辑的工作流至关重要。对典型的 20 页 PDF，在现代 CPU 上转换通常在一秒以内完成。

## 前提条件

- **Java Development Kit (JDK) 8+** 已安装并配置 `JAVA_HOME`。  
- **Maven 3.6+** 或 **Gradle 6+** 用于依赖管理。  
- 具备基本的 Java 文件 I/O 和异常处理的熟悉度。  

### 必需的库和依赖

您需要 Aspose.PDF for Java 库的 25.3 版或更高版本。使用以下任一构建工具将其包含进来：

**Maven:**  
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-pdf</artifactId>
    <version>25.3</version>
</dependency>
```  

**Gradle:**  
```gradle
implementation 'com.aspose:aspose-pdf:25.3'
```  

### 环境设置

确保您的 IDE 或构建环境指向正确的 JDK，并且网络能够访问 Maven Central 或您的私有仓库。

## 如何添加 Aspose PDF Maven 依赖？

`aspose-pdf` 是您需要添加到项目构建文件中的构件，然后刷新依赖以自动下载 JAR。对于 Maven，将 `<dependency>` 块插入到 `<dependencies>` 中；对于 Gradle，将 `implementation` 行放入 `dependencies` 块中。刷新后，Aspose 类将出现在类路径上，您可以开始编码，无需手动处理 JAR。

## 设置 Aspose.PDF for Java

### 安装步骤

1. **Maven/Gradle 设置：** 按上述方式添加依赖并运行 `mvn clean install` 或 `gradle build` 拉取库。  
2. **许可证获取：**  
   - 下载[免费试用](https://releases.aspose.com/pdf/java/)或获取[临时许可证](https://purchase.aspose.com/temporary-license/)。  
   - 将许可证文件（`Aspose.Pdf.lic`）放在应用程序可访问的文件夹中，并在启动时加载它。

### 基本初始化

`License` 用于应用 Aspose 许可证文件以解锁全部功能。  
加载许可证（如果有）并创建一个 `Document` 对象来处理 PDF。  
`Document` 代表一个 PDF 文件，并提供操作其内容的方法。

```java
import com.aspose.pdf.Document;
import com.aspose.pdf.License;

// Initialize a License object
License license = new License();

// Set the license file path
license.setLicense("path/to/Aspose.Total.Java.lic");
```  

## 如何将 PDF 转换为可选择文本的 XPS？

`XpsSaveOptions` 用于配置将 PDF 保存为 XPS 文档的设置，包括文本保留。  
加载源 PDF，配置 `XpsSaveOptions` 以保留文本，然后使用 `.xps` 扩展名调用 `save`。API 会自动嵌入文本层，因此生成的 XPS 可以像原始 PDF 一样进行搜索和复制。整个过程在库设置好后通常只需三行代码。

## 实现指南

### 将 PDF 转换为 XPS

此功能使您能够使用 Aspose.PDF for Java 将 PDF 文档转换为 XPS 文件。

#### 步骤 1：加载 PDF 文档

首先，从目录中加载您的 PDF 文档：

```java
import com.aspose.pdf.Document;

String dataDir = "YOUR_DOCUMENT_DIRECTORY";
Document pdfDocument = new Document(dataDir + "/input.pdf");
```  

#### 步骤 2：配置保存选项

创建 `XpsSaveOptions` 实例以设置 XPS 转换选项：

```java
import com.aspose.pdf.XpsSaveOptions;

XpsSaveOptions saveOptions = new XpsSaveOptions();
```  

#### 步骤 3：保存为 XPS 文件

最后，将文档以 XPS 格式保存到您希望的输出目录：

```java
String outputDir = "YOUR_OUTPUT_DIRECTORY";
pdfDocument.save(outputDir + "/ConvertPDFtoXPS_out.xps\
```  

## 常见问题及解决方案

- **XPS 输出出现空白页：** 确保 PDF 未使用加密流；如果使用，请在加载 `Document` 时提供密码。  
- **大 PDF 内存错误：** 在保存前使用 `Document.optimizeResources()` 以降低内存占用。  
- **缺少字体：** 在服务器上安装所需字体，或在转换前将其嵌入 PDF。

## 常见问答

**问：我可以转换受密码保护的 PDF 吗？**  
答：可以——在 `Document` 构造函数中传入密码，或在转换前使用 `Document.open(String path, String password)`。

**问：XPS 能保留矢量图形吗？**  
答：当然。所有矢量形状、图像和文本都会被保留，且文本仍可选择。

**问：试用版是否必须使用许可证？**  
答：试用版可以在没有许可证的情况下使用，但会在输出中添加水印；永久许可证会移除所有限制。

**问：Aspose.PDF 如何处理大文件？**  
答：它以流式方式处理文件，允许在不将整个文档加载到内存中的情况下转换数百页的 PDF。

**问：支持哪些平台？**  
答：该库可在任何兼容 JDK 的操作系统上运行，包括 Windows、Linux 和 macOS。

---

**最后更新：** 2026-07-03  
**测试环境：** Aspose.PDF for Java 25.3  
**作者：** Aspose  

{{< blocks/products/products-backtop-button >}}

## 相关教程

- [使用 Aspose.PDF for Java 将 PDF 转换为 JPEG：分步指南](/pdf/java/conversion-export/convert-pdf-to-jpeg-aspose-java-tutorial/)
- [如何使用 Aspose.PDF for Java 将 PDF 转换为 Excel | 分步指南](/pdf/java/conversion-export/convert-pdf-excel-aspose-java-tutorial/)
- [如何使用 Aspose.PDF 在 Java 中将 XPS 文件转换为 PDF：完整指南](/pdf/java/conversion-export/convert-xps-pdf-aspose-java-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}