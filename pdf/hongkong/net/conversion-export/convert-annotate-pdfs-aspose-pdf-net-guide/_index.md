---
"date": "2025-04-11"
"description": "了解如何使用 Aspose.PDF for .NET 將 PDF 轉換為圖像並反白顯示文字。本指南涵蓋安裝、程式碼範例和最佳實務。"
"title": "使用 Aspose.PDF for .NET&#58; 轉換與註解 PDF綜合指南"
"url": "/zh-hant/net/conversion-export/convert-annotate-pdfs-aspose-pdf-net-guide/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# 使用 Aspose.PDF for .NET 轉換與註解 PDF：綜合指南

如今，高效管理數位文件對於企業和個人來說至關重要。將 PDF 文件轉換為圖像或突出顯示文字可增強文件的可見性和可用性。本指南示範如何使用 **Aspose.PDF for .NET** 完成這些任務。

## 您將學到什麼：
- 載入 PDF 並將其轉換為圖像格式。
- 使用自訂註釋突出顯示 PDF 中的文字。
- 優化效能並將 Aspose.PDF 整合到您的專案中。

首先，請確保您具備必要的先決條件。

### 先決條件
在實現這些功能之前，請確保您已：

1. **所需庫：**
   - Aspose.PDF for .NET（最新版本）。
2. **環境設定：**
   - 安裝了 .NET Core 或 .NET Framework 的開發環境。
   - Visual Studio 或任何相容的 IDE。
3. **知識前提：**
   - 對 C# 程式設計和 .NET 專案設定有基本的了解。
   - 熟悉在 .NET 應用程式中處理文件。

## 設定 Aspose.PDF for .NET
若要使用 Aspose.PDF，請使用以下方法之一將其安裝到您的專案中：

**.NET CLI：**
```bash
dotnet add package Aspose.PDF
```

**套件管理器控制台：**
```powershell
Install-Package Aspose.PDF
```

**NuGet 套件管理器 UI：** 搜尋「Aspose.PDF」並直接從您的 IDE 安裝最新版本。

### 許可證獲取
您可以透過下載臨時許可證開始免費試用，以進行完整的功能測試。如需延長使用時間，請透過 Aspose 網站購買授權。

要在您的專案中初始化 Aspose.PDF：
```csharp
// Aspose.PDF for .NET 的基本初始化
Aspose.Pdf.License license = new Aspose.Pdf.License();
license.SetLicense("Path to your license file");
```

## 實施指南
我們將介紹如何將 PDF 轉換為圖像以及如何突出顯示 PDF 中的文字。

### 功能1：將PDF轉換為影像
此功能顯示如何載入 PDF 文件並將其轉換為 PNG 等圖片格式。

#### 概述
將 PDF 頁面轉換為圖像對於預覽文件或將其嵌入無法直接呈現 PDF 的應用程式中很有用。實現如下：

#### 步驟 1：設定您的項目
確保您的專案引用了 Aspose.PDF 庫並包含必要的使用指示：
```csharp
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Devices;
```

#### 第 2 步：載入 PDF 文檔
將目標 PDF 檔案載入到 `Aspose.Pdf.Document` 目的。
```csharp
string dataDir = "YOUR_DOCUMENT_DIRECTORY";
Aspose.Pdf.Document pdfDocument = new Aspose.Pdf.Document(dataDir + "/input.pdf");
```

#### 步驟3：轉換為影像
使用 `PdfConverter` 進行轉換的類別。根據品質和檔案大小需求調整解析度。
```csharp
int resolution = 150; // 數值越高，清晰度越高，但檔案大小也會越大
using (MemoryStream ms = new MemoryStream())
{
    PdfConverter conv = new PdfConverter(pdfDocument);
    conv.Resolution = new Resolution(resolution, resolution); 
    conv.GetNextImage(ms, System.Drawing.Imaging.ImageFormat.Png);

    string outputPath = "YOUR_OUTPUT_DIRECTORY/ConvertedImage.png";
    File.WriteAllBytes(outputPath, ms.ToArray());
}
```
**解釋：** 這 `GetNextImage` 方法將 PDF 的第一頁作為 PNG 影像提取到記憶體流中，然後將其儲存到磁碟。

### 功能 2：在 PDF 中突出顯示文字並繪製矩形
此功能使您能夠透過在 PDF 文件中繪製矩形來突出顯示特定文字片段。

#### 概述
突出顯示文字可增強可讀性或引起對重要部分的注意。此功能的實作方法如下：

#### 步驟 1：載入並轉換 PDF 文檔
與第一個功能一樣，加載您的 PDF：
```csharp
string dataDir = "YOUR_DOCUMENT_DIRECTORY";
Aspose.Pdf.Document pdfDocument = new Aspose.Pdf.Document(dataDir + "/input.pdf");
```

#### 第 2 步：處理並突出顯示文本
使用 `TextFragmentAbsorber` 根據正規表示式模式尋找文字片段，然後在每個片段或字元周圍繪製矩形。
```csharp
using (MemoryStream ms = new MemoryStream())
{
    PdfConverter conv = new PdfConverter(pdfDocument);
    conv.Resolution = new Resolution(150, 150); 
    conv.GetNextImage(ms, System.Drawing.Imaging.ImageFormat.Png);

    Bitmap bmp = (Bitmap)Bitmap.FromStream(ms);
    using (System.Drawing.Graphics gr = System.Drawing.Graphics.FromImage(bmp))
    {
        float scale = 150 / 72f;
        gr.Transform = new System.Drawing.Drawing2D.Matrix(scale, 0, 0, -scale, 0, bmp.Height);

        Page page = pdfDocument.Pages[1];
        TextFragmentAbsorber textFragmentAbsorber = new TextFragmentAbsorber(@"[\S]+");
        textFragmentAbsorber.TextSearchOptions.IsRegularExpressionUsed = true;
        page.Accept(textFragmentAbsorber);
        
        foreach (TextFragment textFragment in textFragmentAbsorber.TextFragments)
        {
            gr.DrawRectangle(Pens.Yellow, 
                (float)textFragment.Position.XIndent,
                (float)textFragment.Position.YIndent,
                (float)textFragment.Rectangle.Width,
                (float)textFragment.Rectangle.Height);

            foreach (TextSegment segment in textFragment.Segments)
            {
                gr.DrawRectangle(Pens.Green, 
                    (float)segment.Rectangle.LLX,
                    (float)segment.Rectangle.LLY,
                    (float)segment.Rectangle.Width,
                    (float)segment.Rectangle.Height);
                
                foreach (TextSegment.TextSegmentCharacterInfo characterInfo in segment.Characters)
                {
                    gr.DrawRectangle(Pens.Black, 
                        (float)characterInfo.Rectangle.LLX,
                        (float)characterInfo.Rectangle.LLY,
                        (float)characterInfo.Rectangle.Width,
                        (float)characterInfo.Rectangle.Height);
                }
            }
        }
    }

    string outputPath = "YOUR_OUTPUT_DIRECTORY/HighlightedPDF.png";
    bmp.Save(outputPath, System.Drawing.Imaging.ImageFormat.Png);
}
```
**解釋：** 程式碼使用正規表示式在 PDF 中尋找單詞，並使用不同的顏色在每個文字片段周圍繪製矩形以提高可見性。

## 實際應用
1. **文件預覽系統：** 將 PDF 轉換為圖像，以便在網路平台上更輕鬆地預覽。
2. **內容突出顯示工具：** 開發應用程序，允許使用者突出顯示文件中的重要部分，以便進行協作或審查。
3. **教育平台：** 透過自動突出顯示 PDF 教科書中的關鍵術語和概念來增強學習材料。

## 性能考慮
使用 Aspose.PDF 時，請考慮以下技巧來優化效能：
- 根據您的需求使用適當的解析度設定來平衡品質和檔案大小。
- 透過及時處理物件和串流來有效地管理記憶體。
- 在適用於非阻塞操作的地方利用非同步程式設計模式。

## 結論
您已經了解如何使用 .NET 中的 Aspose.PDF 將 PDF 轉換為圖像並突出顯示文字。這些功能可以整合到各種應用程式中，從文件管理系統到教育工具。嘗試不同的配置來根據您的特定需求自訂功能。

下一步可能涉及探索 Aspose.PDF 提供的其他功能，例如編輯 PDF 內容或合併多個文件。

## 常見問題部分
1. **我可以將 PDF 的所有頁面轉換為圖像嗎？**
   是的，循環遍歷每個頁面並應用轉換過程從每個頁面中提取圖像。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}