---
"date": "2025-04-11"
"description": "了解如何使用 Aspose.PDF for .NET 有效率地將日期和時間戳記或註解新增至 PDF 文件中。透過這些簡單易行的步驟來增強文件管理。"
"title": "使用 Aspose.PDF for .NET 為 PDF 新增日期和時間戳"
"url": "/zh-hant/net/document-manipulation/aspose-pdf-net-date-time-stamps-annotations/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# 使用 Aspose.PDF for .NET 為 PDF 新增日期和時間戳

## 介紹

在當今數位時代，有效的文件管理對於企業和個人來說至關重要。在 PDF 中新增日期和時間戳記或註釋可以增強資料完整性和組織性。本教學課程示範如何使用 Aspose.PDF for .NET 整合這些功能。

**關鍵要點：**
- 在指定的 PDF 頁面上新增目前日期和時間作為文字戳記。
- 在文件中的所需位置建立自由文字註解。
- 遵循最佳實務以獲得 Aspose.PDF for .NET 的最佳效能。

## 先決條件
在開始之前，請確保您已：

### 所需的庫和版本
- **Aspose.PDF for .NET**：無需 Adobe Acrobat 即可進行 PDF 操作的強大程式庫。使用 21.x 或更高版本。

### 環境設定要求
- 具有 .NET Framework 4.5+ 或 .NET Core 2.0+ 的開發環境
- Visual Studio 或其他支援 C# 程式設計的 IDE

### 知識前提
- 對 C# 和 .NET 專案架構有基本的了解
- 熟悉處理目錄結構中的文件

## 設定 Aspose.PDF for .NET
使用以下方法之一安裝 Aspose.PDF：

**使用 .NET CLI：**
```bash
dotnet add package Aspose.PDF
```

**使用套件管理器：**
```powershell
Install-Package Aspose.PDF
```

**透過 NuGet 套件管理器 UI：**
- 在您的 IDE 中開啟 NuGet 套件管理器。
- 搜尋“Aspose.PDF”並安裝最新版本。

### 許可證取得步驟
要充分利用 Aspose.PDF：
1. **免費試用：** 下載臨時許可證以探索所有功能。
2. **臨時執照：** 如有必要，請申請延長評估許可證。
3. **購買：** 從 Aspose 網站購買長期使用許可證。

在程式碼中初始化您的許可證：
```csharp
Aspose.Pdf.License license = new Aspose.Pdf.License();
license.SetLicense("Path to License File");
```

## 實施指南
讓我們為 PDF 新增日期和時間戳記。

### 功能 1：在 PDF 中新增日期時間戳
此功能將目前日期和時間作為文字戳記新增至指定的 PDF 文件的第一頁。

#### 逐步實施

##### 1. 開啟現有的 PDF 文檔
載入目標文檔：
```csharp
document pdfDocument = new Document("YOUR_DOCUMENT_DIRECTORY/AddTextStamp.pdf");
```

##### 2. 取得目前日期和時間的字串
格式化目前日期和時間：
```csharp
string annotationText = DateTime.Now.ToString("MM/dd/yy hh:mm:ss tt ");
```

##### 3. 使用目前日期和時間建立文字戳
創建一個 `TextStamp` 使用格式化字串的實例：
```csharp
TextStamp textStamp = new TextStamp(annotationText);
textStamp.BottomMargin = 10;
textStamp.RightMargin = 20;
textStamp.HorizontalAlignment = HorizontalAlignment.Right;
textStamp.VerticalAlignment = VerticalAlignment.Bottom;
```

##### 4. 在第一頁新增文字標記
將印章新增至文件的第一頁：
```csharp
document.Pages[1].AddStamp(textStamp);
```

##### 5.建立並新增FreeTextAnnotation（可選）
對於更複雜的註釋，請建立 `FreeTextAnnotation`：
```csharp
DefaultAppearance default_appearance = new DefaultAppearance("Arial", 6, System.Drawing.Color.Black);
FreeTextAnnotation textAnnotation = new FreeTextAnnotation(document.Pages[1], new Aspose.Pdf.Rectangle(0, 0, 0, 0), default_appearance)
{
    Name = "Stamp",
    Contents = textStamp.Value
};
textAnnotation.Border = new Border(textAnnotation) { Width = 0 };
document.Pages[1].Annotations.Add(textAnnotation);
```

##### 6.保存修改後的文檔
儲存變更：
```csharp
string outputDir = "YOUR_OUTPUT_DIRECTORY/AddDateTimeStamp_out.pdf";
document.Save(outputDir);
```

### 功能2：在PDF上新增自由文字註釋
在 PDF 文件中的任何所需位置新增自由文字註釋。

#### 逐步實施

##### 1. 開啟現有的 PDF 文檔
載入目標文檔：
```csharp
document pdfDocument = new Document("YOUR_DOCUMENT_DIRECTORY/Sample.pdf");
```

##### 2. 定義註解的矩形區域
指定在頁面上放置註解的位置：
```csharp
Aspose.Pdf.Rectangle rect = new Aspose.Pdf.Rectangle(100, 400, 200, 450);
```

##### 3. 建立指定外觀和位置的 FreeTextAnnotation
使用所需的文字和外觀設定初始化註解：
```csharp
DefaultAppearance default_appearance = new DefaultAppearance("Arial", 12, System.Drawing.Color.Blue);
FreeTextAnnotation freeTextAnnotation = new FreeTextAnnotation(pdfDocument.Pages[1], rect, default_appearance)
{
    Contents = "This is a sample annotation",
    Title = "Sample Annotation"
};
```

##### 4. 設定邊框樣式並新增註釋
確保邊框樣式符合您的需求（在這種情況下不可見）：
```csharp
freeTextAnnotation.Border = new Border(freeTextAnnotation) { Width = 0 };
pdfDocument.Pages[1].Annotations.Add(freeTextAnnotation);
```

##### 5.保存修改後的文檔
使用新新增的註解儲存您的文件：
```csharp
string outputDir = "YOUR_OUTPUT_DIRECTORY/FreeTextAnnotation_out.pdf";
document.Save(outputDir);
```

## 實際應用
在 PDF 中添加日期戳記和註釋對各個行業都很有用：
- **法律文件**：透過時間戳更改來確保合規性。
- **學術論文**：透過註釋促進協作編輯。
- **財務記錄**：透過帶有時間戳的報告維護準確的審計追蹤。
- **技術文件**：突出顯示手冊中的更新或重要說明。

## 性能考慮
為了在使用 Aspose.PDF for .NET 時獲得最佳效能：
- **批次處理**：批量處理多個 PDF 以減少開銷。
- **記憶體管理**： 使用 `Dispose` 處理每個文件後釋放記憶體資源的方法。
- **優化字體和圖像**：限製字體類型和圖像解析度以減小檔案大小。

## 結論
整合 Aspose.PDF for .NET 可讓您在 PDF 文件中新增日期戳記和註解功能，從而增強功能。這些工具提高了資料完整性並簡化了文件管理。

嘗試不同的配置並探索 Aspose.PDF 提供的附加功能以滿足您的特定需求。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}