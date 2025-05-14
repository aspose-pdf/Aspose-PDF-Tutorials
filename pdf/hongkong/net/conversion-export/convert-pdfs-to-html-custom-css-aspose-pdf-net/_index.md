---
"date": "2025-04-10"
"description": "了解如何使用 Aspose.PDF .NET 將 PDF 文件轉換為互動式、適合網路的 HTML 格式，並附有自訂 CSS 樣式。"
"title": "使用 Aspose.PDF .NET 將 PDF 轉換為具有自訂 CSS 的互動式 HTML"
"url": "/zh-hant/net/conversion-export/convert-pdfs-to-html-custom-css-aspose-pdf-net/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# 使用 Aspose.PDF .NET 將 PDF 轉換為具有自訂 CSS 的互動式 HTML

## 介紹

您是否正在努力將 PDF 文件轉換為互動式、適合網路的格式，同時保持其美觀和專業的外觀？將 PDF 文件轉換為 HTML 可能具有挑戰性，尤其是在追求自訂樣式和高保真度時。本綜合指南將引導您使用 Aspose.PDF .NET（一個以強大的轉換功能而聞名的強大庫）將 PDF 轉換為 HTML。

在本教學中，我們將探討如何利用 Aspose.PDF .NET 轉換您的 PDF 文檔，同時使用自訂 CSS 樣式將它們分割為單獨的頁面。這確保每個頁面在網路上查看時都保持獨特的外觀和感覺。

**您將學到什麼：**
- 在您的專案中設定 Aspose.PDF for .NET。
- 轉換前清理目標目錄。
- 建立並初始化用於轉換的 PDF 文件。
- 使用自訂 CSS 策略配置轉換選項。
- 實現這些功能的實際應用。

準備好深入了解 PDF 到 HTML 轉換的世界了嗎？讓我們先了解您需要的先決條件。

## 先決條件

在深入實施之前，請確保您已具備以下條件：

### 所需的庫和版本
- **Aspose.PDF for .NET**：用於處理 PDF 操作的強大庫。
  
### 環境設定要求
- **.NET Framework 或 .NET Core/5+** 安裝在您的機器上。
- 造訪 Visual Studio 等開發環境。

### 知識前提
- 對 C# 程式設計有基本的了解。
- 熟悉.NET中的檔案系統操作。

## 設定 Aspose.PDF for .NET

首先，您需要安裝 Aspose.PDF 庫。這裡有幾種方法可以實現這一點：

**.NET CLI**
```bash
dotnet add package Aspose.PDF
```

**套件管理器控制台**
```powershell
Install-Package Aspose.PDF
```

**NuGet 套件管理器 UI**
- 搜尋「Aspose.PDF」並直接從您的 IDE 安裝最新版本。

### 許可證獲取

若要無限制地使用 Aspose.PDF，請考慮取得許可證。你可以：
- **免費試用**：存取臨時功能。
- **購買訂閱**：可完全存取所有功能。
- **臨時執照**：如果您需要的不僅僅是試用版，請申請此項。

安裝並獲得許可後（如有必要），透過包含 Aspose.PDF 命名空間來初始化您的專案：

```csharp
using Aspose.Pdf;
```

## 實施指南

讓我們將轉換過程分解為可管理的步驟，並專注於我們實施的不同特點。

### 清理目標資料夾

**概述**：在將 PDF 轉換為 HTML 之前，請務必清除目標目錄中的所有現有文件，以避免衝突並確保重新開始。

1. **刪除指定目錄**
   
   ```csharp
   using System.IO;

   string htmlFile = Path.GetFullPath("YOUR_DOCUMENT_DIRECTORY\\resultant.html");
   string imagesDir = Path.GetDirectoryName(htmlFile) + "\\35942_files";
   string cssDir = Path.GetDirectoryName(htmlFile) + "\\35942_css_files";

   if (Directory.Exists(imagesDir)) { Directory.Delete(imagesDir, true); }
   if (Directory.Exists(cssDir)) { Directory.Delete(cssDir, true); }
   ```

   **解釋**： 
   - `Path.GetFullPath`：解析結果 HTML 檔案的完整路徑。
   - `Directory.Delete`：遞歸刪除目錄以防止剩餘檔案幹擾。

### 建立轉換文檔

**概述**：初始化您想要轉換為 HTML 格式的 PDF 文件。

1. **載入 PDF**

   ```csharp
   string dataDir = "YOUR_DOCUMENT_DIRECTORY";
   Document pdfDocument = new Document(dataDir + "input.pdf");
   ```

   **解釋**：
   - `Document`：代表您的 PDF 文件，Aspose.PDF 將對其進行操作。
   - 確保 `"input.pdf"` 存在於指定目錄中。

### 調整轉換選項

**概述**：配置如何將 PDF 轉換為 HTML，包括圖像格式和 CSS 拆分策略。

1. **設定 HTML 儲存選項**

   ```csharp
   HtmlSaveOptions options = new HtmlSaveOptions();
   options.RasterImagesSavingMode = HtmlSaveOptions.RasterImagesSavingModes.AsPngImagesEmbeddedIntoSvg;
   options.SplitIntoPages = true;
   options.SplitCssIntoPages = true;

   options.CustomCssSavingStrategy = new HtmlSaveOptions.CssSavingStrategy(Strategy_4_CSS_MULTIPAGE_SAVING_RIGHT_WAY);
   options.CustomStrategyOfCssUrlCreation = new HtmlSaveOptions.CssUrlMakingStrategy(Strategy_5_CSS_MAKING_CUSTOM_URL_FOR_MULTIPAGING);
   ```

   **關鍵配置選項**：
   - `RasterImagesSavingMode`：確定如何保存影像，確保相容性。
   - `SplitIntoPages` 和 `SplitCssIntoPages`：支援將 HTML 和 CSS 拆分為每頁單獨的檔案。

### 進行轉換

**概述**：使用您配置的選項執行從 PDF 到 HTML 的轉換。

1. **儲存為 HTML**

   ```csharp
   pdfDocument.Save("YOUR_DOCUMENT_DIRECTORY\\resultant.html", options);
   ```

   **解釋**：
   - `pdfDocument.Save`：使用指定的設定轉換文件並將其儲存為所需的格式。

### CSS 多頁保存策略助手

**概述**：此功能負責在轉換過程中單獨保存每個 HTML 頁面的 CSS。

```csharp
private static void Strategy_4_CSS_MULTIPAGE_SAVING_RIGHT_WAY(HtmlSaveOptions.CssSavingInfo partSavingInfo)
{
    string dataDir = "YOUR_DOCUMENT_DIRECTORY";
    string outPath = dataDir + $"style_xyz_page{partSavingInfo.CssNumber}.css";

    using (System.IO.BinaryReader reader = new System.IO.BinaryReader(partSavingInfo.ContentStream))
    {
        System.IO.File.WriteAllBytes(outPath, reader.ReadBytes((int)partSavingInfo.ContentStream.Length));
    }
}
```

**解釋**： 
- 此策略將每個頁面的 CSS 儲存到單獨的檔案中，有助於保持跨頁面樣式的一致性。

### 自訂 CSS URL 建立策略助手

**概述**：為多頁 HTML 輸出中的 CSS 檔案產生自訂 URL。

```csharp
private static string Strategy_5_CSS_MAKING_CUSTOM_URL_FOR_MULTIPAGING(HtmlSaveOptions.CssUrlRequestInfo requestInfo)
{
    return $"/document-viewer/GetCss?cssId=4544554445_page{
{{requestInfo.PageNumber}
}}";
}
```

**解釋**： 
- 此功能為每個 CSS 檔案建立一個唯一的 URL，以方便動態載入和模組化樣式。

## 實際應用

### 實際用例：
1. **數位出版**：將書籍或報告轉換為網頁格式以供線上分發。
2. **電子商務產品描述**：將產品規格從 PDF 轉換為互動式網頁。
3. **法律文件**：使合約以 HTML 格式呈現，以便於審查和簽署。
4. **教育材料**：以易於瀏覽的 HTML 文件形式分發課程材料。
5. **行銷資料**：創建引人入勝的小冊子或目錄的網路版本。

這些範例說明如何使用 Aspose.PDF 將 PDF 轉換為 HTML 來增強可訪問性、使用者參與度和跨平台的內容分發。

## 性能考慮

處理大型 PDF 檔案時，請考慮以下事項：
- **記憶體管理**： 使用 `using` 語句來正確處置資源。
- **優化影像處理**：將影像轉換為嵌入在 SVG 中的 PNG 等高效格式，以獲得更好的效能。
- **批次處理**：如果轉換許多文檔，請分批處理以有效管理系統資源使用情況。

## 結論

本教學將引導您完成使用 Aspose.PDF .NET 將 PDF 轉換為互動式 HTML 的步驟。您學習如何清理目標目錄、初始化和配置文件轉換設定以及如何應用自訂 CSS 策略來實現精美的網頁演示。

準備好進一步了解嗎？探索 Aspose.PDF 的其他功能，並考慮將這些解決方案整合到更廣泛的系統（如 CMS 平台或電子商務網站）中。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}