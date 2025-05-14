---
"date": "2025-04-10"
"description": "了解如何使用 Aspose.PDF for .NET 將 PDF 檔案轉換為 HTML 格式，並有效地自訂影像路徑。非常適合網路整合。"
"title": "使用 Aspose.PDF 在 .NET 中使用自訂影像路徑將 PDF 轉換為 HTML"
"url": "/zh-hant/net/conversion-export/convert-pdf-html-custom-image-paths-dotnet/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# 在 .NET 中使用自訂圖像路徑將 PDF 轉換為 HTML

## 使用 Aspose.PDF for .NET 將 PDF 轉換為互動式 HTML

### 介紹
您是否希望將 PDF 文件轉換為 HTML，同時保持對影像路徑的完全控制？本教學將指導您使用 Aspose.PDF for .NET，重點介紹自訂圖像前綴。透過利用 Aspose.PDF，您可以有效地儲存和引用生成的 HTML 文件中的圖像。

**好處：**
- 控制影像儲存：指定影像的精確路徑。
- 增強的文檔演示：在 HTML 輸出中保持高品質的視覺效果。
- 簡化的工作流程：使用自訂設定自動將 PDF 轉換為 HTML。

**您將學到什麼：**
- 設定 Aspose.PDF for .NET
- 在 PDF 到 HTML 轉換期間實現自訂圖像前綴
- 實際應用和整合可能性

## 先決條件
在開始之前，請確保您已準備好以下內容：

### 所需的函式庫、版本和相依性
根據您的開發環境，使用以下方法之一將 Aspose.PDF for .NET 整合到您的專案中：

**.NET CLI**
```bash
dotnet add package Aspose.PDF
```

**套件管理器**
```powershell
Install-Package Aspose.PDF
```

**NuGet 套件管理器 UI**：搜尋「Aspose.PDF」並選擇最新版本進行安裝。

### 環境設定要求
確保您有一個相容的 .NET 環境（最好是 .NET Core 或 .NET Framework 4.6.1+）。還需要存取 Visual Studio 或其他支援 .NET 開發的 IDE。

### 知識前提
當我們瀏覽程式碼時，對 C# 的基本了解和對 .NET 中的文件處理的熟悉將會很有幫助。

## 設定 Aspose.PDF for .NET
若要使用 Aspose.PDF，請依照下列步驟操作：
1. **安裝庫**：使用上面提到的安裝方法之一將 Aspose.PDF 整合到您的專案中。
2. **許可證獲取**： 
   - 取得免費試用許可證 [Aspose](https://purchase.aspose.com/temporary-license/) 進行不受限制的完整功能評估。
   - 考慮購買許可證或為特定項目使用臨時許可證。
3. **基本初始化和設定**：

以下是如何在專案中初始化 Aspose.PDF：
```csharp
// 使用現有 PDF 檔案初始化新的 Document 實例
Document doc = new Document("input.pdf");
```

設定完成後，讓我們探索在轉換過程中自訂影像前綴。

## 實施指南
### 在 PDF 到 HTML 轉換中自訂圖像前綴
此功能可讓您為從 PDF 文件中提取的圖像指定自訂路徑。透過這樣做，您可以在 Web 應用程式中有效地組織和提供這些圖像。

#### 功能概述
主要目標是控制將 PDF 轉換為 HTML 時圖像的保存位置，允許自訂 URL 或檔案路徑。

#### 實施步驟
**步驟 1：準備您的環境**
確保您的專案已將 Aspose.PDF 新增為依賴項。此設定可讓您利用其強大的轉換功能。

```csharp
using System.IO;
using Aspose.Pdf;

namespace PdfToHtmlConversion
{
    public class ImagePrefixCustomization
    {
        public static void Run()
        {
            try
            {
                // 定義文檔的目錄路徑
                string dataDir = "YourDocumentsPath";

                // 指定輸出檔案路徑
                string outFile = Path.Combine(dataDir, "SpecifyImages_out.html");

                // 載入您的 PDF 文檔
                Document doc = new Document(Path.Combine(dataDir, "input.pdf"));

                // 設定 HtmlSaveOptions
                HtmlSaveOptions saveOptions = new HtmlSaveOptions();
                saveOptions.SplitIntoPages = false;

                // 分配自訂資源節約策略
                saveOptions.CustomResourceSavingStrategy = new HtmlSaveOptions.ResourceSavingStrategy(SavingTestStrategy_1);

                // 將文件儲存為帶有自訂圖像前綴的 HTML
                doc.Save(outFile, saveOptions);
            }
            catch (Exception ex)
            {
                Console.WriteLine("Error: " + ex.Message);
            }
        }

        // 自訂資源節約策略方法
        private static string SavingTestStrategy_1(SaveOptions.ResourceSavingInfo resourceSavingInfo)
        {
            // 確定資源是否為影像並需要自訂處理
            if (!(resourceSavingInfo is HtmlSaveOptions.HtmlImageSavingInfo))
            {
                resourceSavingInfo.CustomProcessingCancelled = true;
                return "";
            }

            HtmlSaveOptions.HtmlImageSavingInfo asHtmlImageSavingInfo = (HtmlSaveOptions.HtmlImageSavingInfo)resourceSavingInfo;

            // 指定處理 SVG 影像的條件
            if ((asHtmlImageSavingInfo.ImageType != HtmlSaveOptions.HtmlImageType.Svg)
                 && (asHtmlImageSavingInfo.ImageType != HtmlSaveOptions.HtmlImageType.ZippedSvg))
            {
                resourceSavingInfo.CustomProcessingCancelled = true;
                return "";
            }

            // 定義影像的輸出資料夾
            string dataDir = "YourDocumentsPath";
            string imageOutFolder = Path.Combine(Path.GetDirectoryName(dataDir), @"35956_svg_files");

            if (!Directory.Exists(imageOutFolder))
            {
                Directory.CreateDirectory(imageOutFolder);
            }

            // 建立保存映像的完整路徑
            string outPath = Path.Combine(imageOutFolder, Path.GetFileName(resourceSavingInfo.SupposedFileName));

            // 儲存影像檔案的二進位內容
            using (var reader = new BinaryReader(resourceSavingInfo.ContentStream))
            {
                System.IO.File.WriteAllBytes(outPath, reader.ReadBytes((int)resourceSavingInfo.ContentStream.Length));
            }

            // 返回 HTML 中引用圖像的自訂 URL
            return $"/document-viewer/GetImage?path=CRWU-NDWAC-Final-Report-12-09-10-2.pdf&name={resourceSavingInfo.SupposedFileName}";
        }
    }
}
```
**關鍵部件說明：**
- **Html保存選項**：配置 PDF 轉換為 HTML 的方式。
- **資源節約策略**：一種確定在轉換過程中如何保存和引用資源（如圖像）的方法。

#### 故障排除提示
- 確保輸出目錄存在或在儲存檔案之前建立它。
- 優雅地處理異常以有效地調試問題，尤其是在處理檔案路徑時。

## 實際應用
以下是一些自訂圖像前綴可能有益的實際場景：
1. **入口網站**：對於託管 PDF 報告的門戶，確保圖像具有一致的 URL 結構可縮短載入時間並改善使用者體驗。
2. **內容管理系統（CMS）**：將 PDF 內容整合到 CMS 時，控製影像路徑可以更好地組織和檢索媒體資產。
3. **電子商務平台**：自訂圖像路徑可確保從 PDF 轉換的產品目錄保持高品質的視覺效果和優化的 URL。

## 性能考慮
使用 Aspose.PDF 時：
- **優化記憶體使用**：明智地使用流來管理記憶體消耗，尤其是在處理大型文件時。
- **批次處理**：如果轉換多個文件，請考慮批次任務以提高效能和資源分配。
- **非同步操作**：對檔案 I/O 操作實現非同步方法以增強回應能力。

## 結論
在本教學中，您學習如何使用 Aspose.PDF 在 .NET 中將 PDF 轉換為 HTML，同時自訂影像路徑。此功能透過確保高效的資源管理和演示質量，增強了 PDF 內容與 Web 應用程式的整合。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}