---
"date": "2025-04-10"
"description": "了解如何使用 Aspose.PDF for .NET 將 PDF 文件轉換為具有外部 PNG 圖像的 HTML。本指南確保佈局保存和網路效能優化。"
"title": "使用 Aspose.PDF .NET&#58; 將 PDF 轉換為 HTML將圖片儲存為外部 PNG"
"url": "/zh-hant/net/conversion-export/pdf-to-html-conversion-external-png-aspose-pdf-net/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# 使用 Aspose.PDF .NET 將 PDF 文件轉換為 HTML：將圖片儲存為外部 PNG

## 介紹

將 PDF 檔案轉換為適合網路的 HTML 格式對於增強數位可存取性和使用者體驗至關重要。本教學課程示範如何使用 Aspose.PDF for .NET 將 PDF 文件轉換為 HTML 文件，並將圖片儲存為透過 SVG 引用的外部 PNG 檔案。

**您將學到什麼：**
- 設定 Aspose.PDF for .NET
- 將 PDF 轉換為 HTML，同時保持原始佈局
- 將圖像以 PNG 格式儲存到外部並透過 SVG 引用
- 優化實施以提高效能

在開始之前，請確保您已滿足所有必要的先決條件。

## 先決條件

### 所需的函式庫、版本和相依性
- Aspose.PDF for .NET：相容於.NET Framework 或 .NET Core 版本。

### 環境設定要求
- 安裝了 .NET SDK 的 Visual Studio 2019 或更高版本。

### 知識前提
- 對 C# 程式設計有基本的了解。
- 熟悉 .NET 應用程式中的檔案目錄結構。

檢查這些先決條件後，繼續為您的專案設定 Aspose.PDF。

## 設定 Aspose.PDF for .NET

若要使用 Aspose.PDF for .NET，請透過以下方法之一將程式庫安裝到您的專案中：

**.NET CLI：**
```bash
dotnet add package Aspose.PDF
```

**套件管理器控制台：**
```powershell
Install-Package Aspose.PDF
```

**NuGet 套件管理器 UI：**
1. 在 Visual Studio 中開啟 NuGet 套件管理器。
2. 搜尋“Aspose.PDF”並安裝最新版本。

### 許可證取得步驟
- **免費試用：** 從 30 天免費試用開始探索 Aspose.PDF 的功能。
- **臨時執照：** 申請臨時許可證，以便不受限制地延長訪問時間。
- **購買：** 考慮購買完整許可證以供長期使用。

在 Visual Studio 中建立一個新的 .NET 專案並使用上述方法之一安裝 Aspose.PDF。此設定提供對 PDF 處理所需的所有類別和方法的存取。

## 實施指南

本節詳細介紹如何使用 Aspose.PDF for .NET 將 PDF 文件轉換為 HTML 文件，並將圖片儲存為透過 SVG 引用的外部 PNG 檔案。

### 步驟 1：載入 PDF 文檔
首先將 PDF 檔案載入到 `Document` 目的：
```csharp
// 在此設定您的目錄路徑
string YOUR_DOCUMENT_DIRECTORY = "YOUR_DOCUMENT_DIRECTORY";
string YOUR_OUTPUT_DIRECTORY = "YOUR_OUTPUT_DIRECTORY";

try
{
    // 建立 Document 物件來載入 PDF 文件
    Document doc = new Document(YOUR_DOCUMENT_DIRECTORY + "/input.pdf");
}
catch (Exception ex)
{
    Console.WriteLine(ex.Message);
}
```

### 步驟 2：初始化 HtmlSaveOptions
使用配置轉換選項 `HtmlSaveOptions`：
```csharp
// 使用特定配置初始化 HtmlSaveOptions
HtmlSaveOptions saveOptions = new HtmlSaveOptions();
saveOptions.FixedLayout = true;  // 保留 PDF 的原始佈局
saveOptions.SplitIntoPages = false;  // 不要將每個 PDF 頁面拆分成單獨的 HTML 頁面
```

### 步驟3：設定影像儲存模式
設定圖像的儲存和引用方式：
```csharp
// 將圖像儲存為透過 SVG 引用的外部 PNG 文件
saveOptions.RasterImagesSavingMode = HtmlSaveOptions.RasterImagesSavingModes.AsExternalPngFilesReferencedViaSvg;
```

### 步驟4：儲存轉換後的文檔
最後，使用指定選項將文件儲存為 HTML 文件：
```csharp
// 使用指定選項將轉換後的文件儲存為 HTML 文件
doc.Save(YOUR_OUTPUT_DIRECTORY + "/SaveImages_out.html", saveOptions);
```

**關鍵配置選項：**
- `FixedLayout`：在 HTML 輸出中保留 PDF 的原始佈局。
- `RasterImagesSavingMode`：將圖像儲存為透過 SVG 引用的外部 PNG 文件，以獲得更好的網路效能。

### 故障排除提示
- 確保目錄路徑設定正確，以避免檔案未找到錯誤。
- 驗證 Aspose.PDF 是否已正確安裝並獲得許可，以防止執行期間異常。

## 實際應用

這種轉換方法有幾種實際應用：
1. **數位檔案：** 轉換歷史文檔以供線上訪問，同時保留佈局完整性。
2. **電子商務平台：** 以網路友善格式顯示產品手冊或小冊子，而不會遺失設計元素。
3. **教育資源：** 在學習管理系統上以互動方式分享課程材料。

透過使用 API 來自動化轉換過程或將其合併到現有工作流程中，可以與其他系統整合。

## 性能考慮

為確保在轉換大型文件時獲得最佳效能：
- **優化記憶體使用：** Aspose.PDF 可以有效率地處理資源，但如果擔心記憶體使用問題，則應考慮分塊處理文件。
- **使用最新版本：** 保持您的庫更新，以受益於最新的優化和錯誤修復。
- **批次：** 處理多個文件時實施批次以便更好地管理資源。

## 結論

我們已經介紹瞭如何為 .NET 設定 Aspose.PDF 以及將 PDF 轉換為 HTML，同時將圖像作為透過 SVG 引用的外部 PNG 檔案進行管理。此方法既保持了原有的佈局，又優化了網頁效能。

下一步包括嘗試不同的配置或將該解決方案整合到更大的應用程式中以充分發揮其潛力。

**號召性用語：** 嘗試在您的專案中實現此轉換流程並分享您遇到的任何改進或挑戰！

## 常見問題部分

1. **我可以一次轉換多個 PDF 嗎？**
   - 是的，透過遍歷文件列表並對每個文件應用相同的轉換邏輯。
   
2. **如果我的圖片無法在 HTML 中正確載入怎麼辦？**
   - 驗證檔案路徑並確保可以從 HTML 輸出目錄存取外部 PNG 檔案。

3. **如何在轉換過程中保持文字格式？**
   - 使用 `FixedLayout` 使文字格式與原始 PDF 保持一致。

4. **這種方法適合所有類型的 PDF 嗎？**
   - 雖然它適用於大多數文檔，但高度複雜的佈局可能需要額外的調整。

5. **我可以在沒有許可證的情況下使用 Aspose.PDF 嗎？**
   - 是的，但您會遇到浮水印和試用限制等限制。

## 資源

- **文件:** [Aspose.PDF .NET文檔](https://reference.aspose.com/pdf/net/)
- **下載：** [最新發布](https://releases.aspose.com/pdf/net/)
- **購買：** [購買許可證](https://purchase.aspose.com/buy)
- **免費試用：** [開始免費試用](https://releases.aspose.com/pdf/net/)
- **臨時執照：** [申請臨時許可證](https://purchase.aspose.com/temporary-license/)
- **支持：** [Aspose 論壇](https://forum.aspose.com/c/pdf/10)

透過遵循本指南，您可以有效地使用 Aspose.PDF for .NET 將 PDF 轉換為具有外部圖像的 HTML。編碼愉快！


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}