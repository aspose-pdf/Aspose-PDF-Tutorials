---
"description": "了解如何使用 Aspose.PDF for .NET 從 PDF 文件中提取數位簽章和憑證資訊。面向 C# 開發人員的完整逐步指南。"
"linktitle": "提取簽名資訊"
"second_title": "Aspose.PDF for .NET API參考"
"title": "提取簽名資訊"
"url": "/zh-hant/net/programming-with-security-and-signatures/extract-signature-info/"
"weight": 80
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 提取簽名資訊

## 介紹

在當今的數位世界中，確保文件的安全性和完整性至關重要。保護 PDF 安全的常用方法之一是新增數位簽章。然而，檢索和驗證簽名的詳細資訊有時會是一個挑戰，特別是當您處理各種證書時。在本指南中，我們將引導您完成使用 Aspose.PDF for .NET 從 PDF 文件中提取簽名資訊的過程，使任務變得輕而易舉。您將學習如何存取簽名字段、提取證書資訊並將其保存到文件中。

## 先決條件

在我們開始之前，讓我們確保您已經做好一切準備。

- Aspose.PDF for .NET Library：如果您還沒有，可以從 [Aspose.PDF for .NET下載頁面](https://releases。aspose.com/pdf/net/). 
- .NET 開發環境：您需要一個像 Visual Studio 這樣的 IDE。
- 基本 C# 知識：熟悉 C# 有助於理解本教學中的程式碼片段。
- 帶有數位簽名的 PDF 文件：出於測試目的，請確保您有一個包含至少一個數位簽名的 PDF 文件。

## 導入所需的命名空間

在進入程式碼之前，導入必要的命名空間非常重要。這些命名空間將允許您存取 Aspose.PDF 功能並處理 PDF 文件。

```csharp
using System.IO;
using Aspose.Pdf.Forms;
using Aspose.Pdf;
using System;
```

現在您已經設定好了基本內容，讓我們繼續從 PDF 中提取簽名資訊的實際流程。

## 步驟1：設定文檔目錄

在處理 PDF 文件之前，您需要指定要使用的文件的位置。您可以替換 `"YOUR DOCUMENT DIRECTORY"` 使用儲存 PDF 的目錄的實際路徑。

```csharp
// 文檔目錄的路徑。
string dataDir = "YOUR DOCUMENT DIRECTORY";
string input = dataDir + "ExtractSignatureInfo.pdf";
```

在這裡，我們指定包含 PDF 檔案的目錄和檔案名稱本身。確保該檔案存在於該目錄中！

## 步驟2：載入PDF文檔

現在您已經設定了目錄，下一步是使用 `Document` 來自 Aspose.PDF 的類別。

```csharp
using (Document pdfDocument = new Document(input))
{
    // 在此處理 PDF。
}
```

這行程式碼初始化一個 `Document` 代表 PDF 檔案的對象。這 `using` 語句確保在處理文件後清理資源。

## 步驟 3：存取表單字段

在此步驟中，我們將循環遍歷 PDF 文件中的所有表單欄位。由於簽名通常儲存為表單字段，因此此步驟將幫助我們識別簽名字段。

```csharp
foreach (Field field in pdfDocument.Form)
{
    // 在此處識別簽名字段。
}
```

透過迭代 `Form` 的財產 `Document` 對象，我們可以檢查每個表單欄位以檢查它是否是簽名欄位。

## 步驟 4：識別簽名字段

存取表單欄位後，下一步就是確定哪些是簽名欄位。我們可以透過將每個欄位轉換為 `SignatureField` 目的。

```csharp
SignatureField sf = field as SignatureField;
if (sf != null)
{
    // 提取簽名資訊。
}
```

在這裡，我們使用 `as` 關鍵字嘗試將每個表單欄位轉換為 `SignatureField`。如果轉換成功，我們就知道該欄位是一個簽名。

## 步驟5：提取證書

現在您已經識別了簽名字段，下一個任務是從簽名中提取證書。證書包含有關簽署者和簽名有效性的重要資訊。

```csharp
Stream cerStream = sf.ExtractCertificate();
```

這 `ExtractCertificate` 方法回傳一個 `Stream` 包含證書資料的物件。此流可用於保存證書以供進一步分析或儲存。

## 步驟 6：將證書儲存到文件

提取證書後，最後一步是將其儲存到文件中。在這種情況下，我們將證書儲存為 `.cer` 文件。

```csharp
if (cerStream != null)
{
    using (cerStream)
    {
        byte[] bytes = new byte[cerStream.Length];
        using (FileStream fs = new FileStream(dataDir + @"input.cer", FileMode.CreateNew))
        {
            cerStream.Read(bytes, 0, bytes.Length);
            fs.Write(bytes, 0, bytes.Length);
        }
    }
}
```

在此程式碼區塊中，我們：

1. 檢查證書流是否不為空。
2. 將證書資料讀入位元組數組。
3. 將位元組數組寫入 `.cer` 文檔目錄中的檔案。

## 結論

使用 Aspose.PDF for .NET 從 PDF 文件中提取數位簽章及其相關憑證資訊非常簡單，只需分解為簡單的步驟即可。無論您是審計文件、驗證簽名還是僅儲存憑證以保管，本教學都會為您提供高效完成這些工作所需的知識。請記住，在當今的數位世界中，保護和驗證文件至關重要，而使用 Aspose.PDF for .NET 等工具可以使其更容易處理。

## 常見問題解答

### 我可以使用 Aspose.PDF for .NET 從 PDF 中擷取多個簽章嗎？
是的，程式碼循環遍歷文件中的所有表單字段，允許您提取存在的多個簽名。

### 如果在 PDF 中找不到簽名會發生什麼？
如果沒有簽名字段，程式碼將直接跳過它們而不會引發錯誤。

### 我可以使用這種方法來驗證簽章的有效性嗎？
雖然您可以提取證書，但驗證簽名的有效性需要額外的步驟，例如檢查證書的信任鏈。

### 是否可以使用 Aspose.PDF for .NET 擷取其他表單欄位資料？
是的，Aspose.PDF 允許您存取和操作 PDF 中的各種類型的表單字段，而不僅僅是簽名字段。

### 如何查看提取的證書的詳細資訊？
一旦證書被保存為 `.cer` 文件，您可以使用任何憑證檢視器開啟它或將其匯入系統憑證儲存區以進行進一步檢查。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}