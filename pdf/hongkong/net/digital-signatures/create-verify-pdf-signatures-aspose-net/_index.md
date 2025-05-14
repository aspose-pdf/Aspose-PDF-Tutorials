---
"date": "2025-04-11"
"description": "了解如何使用 Aspose.PDF for .NET 安全地建立、簽署和驗證 PDF 簽章。透過本綜合指南增強您的文件工作流程。"
"title": "如何使用 Aspose.PDF for .NET 建立和驗證 PDF 簽名"
"url": "/zh-hant/net/digital-signatures/create-verify-pdf-signatures-aspose-net/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# 如何使用 Aspose.PDF for .NET 建立和驗證 PDF 簽名

在數位時代，確保文件的真實性至關重要。無論您是負責安全文件處理還是管理法律文件的開發人員，如果沒有合適的工具，建立和驗證 PDF 簽名可能會很困難。本教學將指導您使用 Aspose.PDF for .NET 無縫複製、簽署和驗證 PDF 文檔，從而提高工作流程的安全性和效率。

## 您將學到什麼

- **建立簽名字段：** 在您的 PDF 中新增簽名欄位。
- **簽署文件：** 使用數位憑證安全地簽署 PDF 檔案。
- **驗證簽名：** 檢查 PDF 文件上的簽名是否有效。

在開始實現這些功能之前，讓我們先深入了解如何設定您的環境！

## 先決條件

在開始之前，請確保您已：

- **.NET 框架** （版本 4.6.1 或更高版本）或安裝了 .NET Core。
- 像 Visual Studio 或 VS Code 這樣的程式碼編輯器。
- 對 C# 程式設計有基本的了解。

此外，熟悉數位憑證和 PDF 文件結構可能會有所幫助，但這並不是學習本教學的必要條件。

## 設定 Aspose.PDF for .NET

若要在您的專案中利用 Aspose.PDF 的功能，請依照下列安裝步驟操作：

### 安裝選項

**.NET CLI**
```shell
dotnet add package Aspose.PDF
```

**套件管理器控制台 (Visual Studio)**
```powershell
Install-Package Aspose.PDF
```

**NuGet 套件管理器 UI**
搜尋“Aspose.PDF”並點擊安裝以取得最新版本。

### 授權

1. **免費試用：** 從免費試用許可證開始 [Aspose的網站](https://releases.aspose.com/pdf/net/) 進行初步測試。
2. **臨時執照：** 如需延長評估時間，請透過以下方式申請臨時許可證 [Aspose的購買頁面](https://purchase。aspose.com/temporary-license/).
3. **購買：** 要在生產中使用 Aspose.PDF，請從 [購買門戶](https://purchase。aspose.com/buy).

### 基本初始化

一旦安裝並獲得許可，您可以像這樣初始化 Aspose.PDF：

```csharp
using Aspose.Pdf;

Document pdfDocument = new Document();
```

## 實施指南

讓我們逐步分解每個功能。

### 功能 1：文件複製和簽名創建

#### 概述

此功能可以複製 PDF 文件以建立新的簽名文檔，然後新增簽名欄位。

#### 步驟

##### **步驟 1：複製 PDF**

首先複製現有的 PDF 作為基礎文件：

```csharp
string dataDir = "YOUR_DOCUMENT_DIRECTORY";
File.Copy(dataDir + "/blank.pdf", dataDir + "/externalSignature1.pdf", true);
```

**為什麼：** 這可確保您擁有一個新的起點，而無需修改原始文件。

##### **步驟 2：建立並新增簽名字段**

載入您複製的 PDF 並新增簽名欄位：

```csharp
using (FileStream fs = new FileStream(dataDir + "/externalSignature1.pdf", FileMode.Open, FileAccess.ReadWrite))
{
    Document doc = new Document(fs);
    Rectangle rect = new Rectangle(100, 400, 200, 450); // 定義簽名欄位的位置和大小。
    SignatureField field1 = new SignatureField(doc.Pages[1], rect);
    doc.Form.Add(field1, 1);
}
```

**為什麼：** 簽章欄位定義使用者放置其數位簽章的位置。

### 功能 2：簽署 PDF 文檔

#### 概述

本節介紹如何使用 Windows 憑證儲存區的憑證對先前建立的 PDF 進行簽署。

#### 步驟

##### **步驟 3：存取憑證**

開啟憑證儲存區並選擇一個憑證：

```csharp
X509Store store = new X509Store(StoreLocation.CurrentUser);
store.Open(OpenFlags.ReadOnly);
X509Certificate2Collection sel = X509Certificate2UI.SelectFromCollection(store.Certificates, null, "Select a Certificate:", SelectionFlag.SingleSelection);
```

**為什麼：** 證書提供簽署文件所需的必要憑證。

##### **步驟 4：簽署 PDF**

建立外部簽名並將其套用到您的文件：

```csharp
using (FileStream fs = new FileStream(dataDir + "/externalSignature1.pdf", FileMode.Open, FileAccess.ReadWrite))
{
    Document doc = new Document(fs);
    SignatureField field1 = (SignatureField)doc.Form["sig1"];
    
    Aspose.Pdf.Forms.ExternalSignature externalSignature = new Aspose.Pdf.Forms.ExternalSignature(sel[0])
    {
        Authority = "Me",
        Reason = "Reason",
        ContactInfo = "Contact"
    };

    field1.Sign(externalSignature);
    doc.Save();
}
```

**為什麼：** 此步驟套用您的數位簽章來驗證文件。

### 功能3：驗證已簽署的PDF文檔

#### 概述

透過驗證簽名來確保簽名文件的完整性。

#### 步驟

##### **步驟5：驗證簽名**

檢查 PDF 中的所有簽名以確認其有效性：

```csharp
using (PdfFileSignature pdfSign = new PdfFileSignature(new Document(dataDir + "/externalSignature1.pdf")))
{
    IList<string> sigNames = pdfSign.GetSignNames();
    foreach (string sigName in sigNames)
    {
        bool isVerified = pdfSign.VerifySigned(sigName) && pdfSign.VerifySignature(sigName);
        if (!isVerified)
        {
            throw new ApplicationException("Not verified");
        }
    }
}
```

**為什麼：** 驗證可確保文件自簽署以來未被更改。

## 實際應用

Aspose.PDF for .NET 提供了廣泛的功能，包括：

1. **法律文件管理：** 確保合約和協議以數位方式簽署。
2. **發票處理：** 在將發票發送給客戶之前，請先進行安全簽署。
3. **認證和憑證：** 對證書和學術文件進行數位簽署。
4. **電子郵件附件：** 在 PDF 附件中新增數位簽章以進行真實性驗證。
5. **協作工作流程：** 將簽章整合到協作平台，確保文件的完整性。

## 性能考慮

若要在使用 Aspose.PDF 時最佳化應用程式的效能：

- **管理資源：** 關閉檔案流並適當處置物件以釋放記憶體。
- **使用串流 API：** 對於大型文檔，使用串流 API 來有效地處理資料。
- **優化處理：** 盡可能批量執行簽名操作以減少開銷。

## 結論

現在您已經了解如何使用 Aspose.PDF for .NET 建立、簽署和驗證 PDF 簽章。透過實現這些功能，您可以增強文件工作流程的安全性和可靠性。為了進一步探索，請考慮將 Aspose.PDF 與其他系統整合或探索加密和元資料管理等附加功能。

## 常見問題部分

1. **什麼是數位簽章？**
   - 數位簽名是一種電子形式的簽名，用於驗證數位文件的真實性和完整性。

2. **如何取得用於簽署 PDF 的數位憑證？**
   - 您可以從受信任的證書頒發機構購買證書，或建立自簽名證書以用於測試目的。

3. **Aspose.PDF 可以處理大量文件嗎？**
   - 是的，Aspose.PDF 旨在利用其串流和批次功能同時有效地處理多個文件。

4. **如果簽名驗證失敗會發生什麼事？**
   - 如果驗證失敗，則表示該文件可能在簽署後被更改。透過記錄錯誤或通知用戶採取進一步措施來處理此類情況。

5. **Aspose.PDF 可以免費使用嗎？**
   - Aspose.PDF 提供具有完整功能的免費試用版以供測試，但生產使用需要許可證。

## 資源

- [Aspose.PDF文檔](https://reference.aspose.com/pdf/net/)
- [下載最新版本](https://releases.aspose.com/pdf/net/)
- [購買許可證](https://purchase.aspose.com/buy)
- [免費試用和臨時許可證](https://releases.aspose.com/pdf/net/)
- [Aspose 支援論壇](https://forum.aspose.com/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}