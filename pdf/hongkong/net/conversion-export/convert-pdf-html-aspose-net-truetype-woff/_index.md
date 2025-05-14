---
"date": "2025-04-10"
"description": "了解如何使用 Aspose.PDF for .NET 將 PDF 轉換為 HTML，同時保留 TrueType (TTF) 和 Web 開放字體格式 (WOFF)。帶有程式碼範例的分步指南。"
"title": "使用 Aspose.PDF for .NET&#58; 將 PDF 轉換為 HTML保留 TTF 和 WOFF 格式的字體"
"url": "/zh-hant/net/conversion-export/convert-pdf-html-aspose-net-truetype-woff/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# 使用 Aspose.PDF for .NET 將 PDF 轉換為 HTML：保留 TTF 和 WOFF 格式的字體

## 介紹
將 PDF 文件轉換為 HTML 時，是否難以保持其原始佈局和字體完整性？轉換 PDF 並保留其字體可能具有挑戰性，但其實並非如此。和 **Aspose.PDF for .NET**，您可以毫不費力地將 PDF 檔案轉換為 HTML 格式，同時確保字體以 TrueType (TTF) 或 Web 開放字體格式 (WOFF) 儲存。本指南將逐步指導您完成整個過程。

在本教程中，我們將介紹：
- 將 PDF 轉換為 HTML 時如何將字體儲存為 TTF
- 配置轉換以將字體儲存為 WOFF
- 轉換期間儲存所有格式的字體

閱讀本文後，您將全面了解如何使用 Aspose.PDF for .NET 有效管理字體轉換。讓我們深入了解開始之前所需的先決條件。

## 先決條件
在使用 Aspose.PDF 將 PDF 轉換為 HTML 之前，請確保符合以下要求：

### 所需的庫和依賴項
- **Aspose.PDF for .NET**：該程式庫對於在 .NET 應用程式中處理 PDF 檔案至關重要。
- **.NET Framework 或 .NET Core/5+**：確保您的開發環境支援這些框架。

### 環境設定要求
確保您的開發環境（例如，Visual Studio）已設定為可使用 Aspose.PDF 庫。你需要：
- 在 .NET Framework 或 .NET Core/5+ 中建立的項目
- 存取 NuGet 套件管理器來安裝庫

### 知識前提
對 C# 的基本了解和熟悉 .NET 中的文件處理將會很有幫助。

## 設定 Aspose.PDF for .NET
首先，您需要安裝 Aspose.PDF 庫。您可以透過不同的套件管理器來執行此操作：

**.NET CLI：**
```bash
dotnet add package Aspose.PDF
```

**套件管理器控制台：**
```powershell
Install-Package Aspose.PDF
```

**NuGet 套件管理器 UI：**
搜尋“Aspose.PDF”並安裝最新版本。

### 許可證獲取
您可以從 Aspose 取得臨時許可證或購買完整許可證。免費試用可讓您不受限制地探索所有功能，非常適合初步評估。以下是使用許可證設定環境的方法：
1. 請求 [臨時執照](https://purchase。aspose.com/temporary-license/).
2. 在執行任何操作之前，請使用以下程式碼片段在您的應用程式中套用許可證：

```csharp
Aspose.Pdf.License license = new Aspose.Pdf.License();
license.SetLicense("Path to your License File");
```

## 實施指南
讓我們將實作分解為三個關鍵功能：將字體儲存為 TTF、WOFF 和所有格式。

### 將字體儲存為 TTF
**概述**
此功能可讓您在將 PDF 文件轉換為 HTML 時以 TrueType 格式 (TTF) 儲存其中的字型。這可確保在轉換過程中保持字體的視覺完整性。

#### 逐步實施
1. **初始化文件和選項：**
   首先使用 Aspose.PDF 載入您的 PDF 文檔 `Document` 課程和設定 `HtmlSaveOptions`。

   ```csharp
   string dataDir = "YOUR_DOCUMENT_DIRECTORY";
   string outFile = Path.GetFullPath(dataDir + "/36192_out.html");
   Document doc = new Document(dataDir + "/input.pdf");

   HtmlSaveOptions saveOptions = new HtmlSaveOptions();
   ```

2. **配置儲存選項：**
   設定必要的選項以維護佈局並指定字體儲存模式。

   ```csharp
   saveOptions.FixedLayout = true; // 保留原始 PDF 佈局
   saveOptions.SplitIntoPages = false; // 不要拆分成多個 HTML 文件
   saveOptions.FontSavingMode = HtmlSaveOptions.FontSavingModes.AlwaysSaveAsTTF;
   ```

3. **準備輸出目錄：**
   確保輸出目錄已準備好儲存連結的字體檔案。

   ```csharp
   string linkedFilesFolder = Path.GetDirectoryName(outFile) + "/36192_files";
   if (Directory.Exists(linkedFilesFolder))
   {
       Directory.Delete(linkedFilesFolder, true); // 清除現有文件
   }
   ```

4. **儲存文件：**
   最後，使用指定的選項儲存您的文件。

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

2. **套用儲存選項：**
   儲存文件時使用這些選項，類似於 TTF 方法。

### 以所有格式儲存字體
**概述**
為了確保最大的相容性和靈活性，您可能想要在轉換過程中儲存所有可用格式的字體。

#### 逐步實施
1. **初始化文件和選項：**
   載入PDF文件並配置 `HtmlSaveOptions`。

   ```csharp
   string dataDir = "YOUR_DOCUMENT_DIRECTORY";
   Document doc = new Document(dataDir + "/input.pdf");
   HtmlSaveOptions htmlOptions = new HtmlSaveOptions();
   ```

2. **配置儲存選項：**
   設定選項以儲存所有字體格式並維護佈局。

   ```csharp
   htmlOptions.FixedLayout = true;
   htmlOptions.RasterImagesSavingMode = HtmlSaveOptions.RasterImagesSavingModes.AsExternalPngFilesReferencedViaSvg;
   htmlOptions.FontSavingMode = HtmlSaveOptions.FontSavingModes.SaveInAllFormats;
   ```

3. **儲存文件：**
   使用這些設定儲存您的文件。

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