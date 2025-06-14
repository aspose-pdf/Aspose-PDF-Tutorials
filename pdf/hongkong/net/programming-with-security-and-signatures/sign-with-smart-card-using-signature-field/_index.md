---
"description": "了解如何使用 Aspose.PDF for .NET 的智慧卡安全地簽署 PDF。按照我們的逐步指南即可輕鬆實施。"
"linktitle": "使用簽名字段透過智慧卡簽名"
"second_title": "Aspose.PDF for .NET API參考"
"title": "使用簽名字段透過智慧卡簽名"
"url": "/zh-hant/net/programming-with-security-and-signatures/sign-with-smart-card-using-signature-field/"
"weight": 120
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 使用簽名字段透過智慧卡簽名

## 介紹

在當今的數位世界中，保護文件安全比以往任何時候都更加重要。無論您是開發人員、企業主還是處理敏感資訊的人，了解如何以電子方式簽署 PDF 都可以節省您的時間並確保您的文件得到驗證。在本指南中，我們將引導您完成使用智慧卡和 Aspose.PDF for .NET 簽章欄位簽署 PDF 的過程。 

## 先決條件

在我們深入了解簽名過程的細節之前，讓我們確保您已準備好開始所需的一切。以下是先決條件清單：

1. Aspose.PDF for .NET：請確定您的 .NET 環境中安裝了 Aspose.PDF 庫。您可以從 [地點](https://releases。aspose.com/pdf/net/).

2. Visual Studio：您需要一個 IDE 來編寫和執行您的 .NET 程式碼。 Visual Studio 社群版是個很棒的免費選擇。

3. 智慧卡：這對於簽署 PDF 至關重要。確保您的機器上安裝了智慧卡讀卡機和必要的憑證。

4. 基本 C# 知識：熟悉 C# 程式設計將幫助您理解我們將使用的程式碼片段。

5. 範例 PDF 文件：準備一個範例 PDF 文件以供測試。您可以建立一個空白 PDF 或使用現有的 PDF。

## 導入包

在我們開始編碼之前，讓我們先導入必要的套件。您需要在 C# 檔案中包含以下命名空間：

```csharp
using Aspose.Pdf.Facades;
using Aspose.Pdf.Forms;
using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;
using System.Text;
```

這些命名空間將使您能夠存取處理 PDF 和數位簽章所需的類別和方法。

## 使用智慧卡簽署 PDF 的分步指南

現在我們已經解決了先決條件，讓我們將簽名過程分解為易於管理的步驟。我們將詳細介紹每個步驟，確保您了解幕後發生的情況。

### 步驟 1：設定文檔目錄

要做什麼：定義文檔目錄的路徑。

```csharp
string dataDir = "YOUR DOCUMENTS DIRECTORY";
```

解釋：替換 `"YOUR DOCUMENTS DIRECTORY"` 與您的 PDF 檔案所在的實際路徑。在這裡我們將閱讀空白 PDF 並保存簽署的文件。

### 第 2 步：複製空白 PDF

要做什麼：建立一份空白 PDF 副本以供使用。

```csharp
File.Copy(dataDir + "blank.pdf", dataDir + "externalSignature1.pdf", true);
```

說明：此行複製 `blank.pdf` 文件到名為 `externalSignature1.pdf`。這 `true` 如果檔案已經存在，參數允許覆蓋。

### 步驟3：開啟PDF文檔

操作方法：開啟複製的 PDF 進行閱讀和書寫。

```csharp
using (FileStream fs = new FileStream(dataDir + "externalSignature1.pdf", FileMode.Open, FileAccess.ReadWrite))
{
    using (Document doc = new Document(fs))
    {
        // 進一步的步驟將在此處進行
    }
}
```

解釋：我們使用 `FileStream` 打開我們的 PDF 檔案。這 `Document` Aspose.PDF 中的類別允許我們操作 PDF 內容。

### 步驟 4：建立簽名字段

操作方法：在 PDF 中定義一個放置簽章的簽章欄位。

```csharp
SignatureField field1 = new SignatureField(doc.Pages[1], new Rectangle(100, 400, 10, 10));
```

說明：在這裡，我們創建一個 `SignatureField` 在 PDF 的第二頁（頁面索引從 1 開始）。這 `Rectangle` 定義簽名欄位的位置和大小。

### 步驟 5：存取智慧卡憑證存儲

操作方法：開啟憑證儲存區以選擇您的智慧卡憑證。

```csharp
X509Store store = new X509Store(StoreLocation.CurrentUser);
store.Open(OpenFlags.ReadOnly);
```

解釋：我們存取目前使用者的憑證儲存。這是儲存您的智慧卡憑證的地方。

### 步驟6：選擇證書

要做什麼：提示使用者從商店中選擇一個憑證。

```csharp
X509Certificate2Collection sel = X509Certificate2UI.SelectFromCollection(store.Certificates, null, null, X509SelectionFlag.SingleSelection);
```

說明：此行開啟一個對話方塊供您選擇證書。您可以選擇與您的智慧卡關聯的憑證。

### 步驟 7：建立外部簽名

要做什麼：建立一個實例 `ExternalSignature` 使用選定的證書。

```csharp
Aspose.Pdf.Forms.ExternalSignature externalSignature = new Aspose.Pdf.Forms.ExternalSignature(sel[0])
{
    Authority = "Me",
    Reason = "Reason",
    ContactInfo = "Contact"
};
```

解釋：我們初始化 `ExternalSignature` 使用所選證書。您還可以設定權限、簽名原因和聯絡資訊。

### 步驟 8：將簽名欄位新增至文檔

操作方法：將簽名欄位新增至文件。

```csharp
field1.PartialName = "sig1";
doc.Form.Add(field1, 1);
```

說明：我們為簽名欄命名，並將其新增至文件的第一頁。這使得 PDF 做好簽名準備。

### 步驟9：簽署文件

操作方法：使用外部簽章對 PDF 進行簽章。

```csharp
field1.Sign(externalSignature);
doc.Save();
```

說明：此行使用外部簽名對文件進行簽名並將變更儲存到 PDF。您的文件現已簽署！

### 步驟10：驗證簽名

要做什麼：檢查簽名是否有效。

```csharp
using (PdfFileSignature pdfSign = new PdfFileSignature(new Document(dataDir + "externalSignature1.pdf")))
{
    IList<string> sigNames = pdfSign.GetSignNames();
    for (int index = 0; index <= sigNames.Count - 1; index++)
    {
        if (!pdfSign.VerifySigned(sigNames[index]) || !pdfSign.VerifySignature(sigNames[index]))
        {
            throw new ApplicationException("Not verified");
        }
    }
}
```

解釋：我們創建一個 `PdfFileSignature` 驗證文件中的簽名。如果簽章無效，則會引發異常。

## 結論

恭喜！您剛剛學習如何使用智慧卡和 Aspose.PDF for .NET 的簽名欄位對 PDF 文件進行簽署。此過程不僅可以保護您的文件，還可以確保真實性，使其成為當今數位環境中的必備技能。無論您簽署的是合約、發票或任何其他重要文件，了解如何實施數位簽章都可以節省您的時間並讓您安心。

## 常見問題解答

### 什麼是 Aspose.PDF for .NET？
Aspose.PDF for .NET 是一個強大的程式庫，可讓開發人員在 .NET 應用程式中建立、操作和轉換 PDF 文件。

### 我需要智慧卡來簽署 PDF 嗎？
是的，需要智慧卡才能使用數位憑證安全地簽署 PDF。

### 我可以免費使用 Aspose.PDF 嗎？
Aspose.PDF 提供免費試用版，您可以下載 [這裡](https://releases。aspose.com/).

### 我如何驗證已簽署的 PDF？
您可以使用 `PdfFileSignature` Aspose.PDF 中的類別來驗證 PDF 文件中的簽名。

### 在哪裡可以找到有關 Aspose.PDF 的更多文件？
您可以檢查 [Aspose.PDF文檔](https://reference.aspose.com/pdf/net/) 了解更多詳細資訊和範例。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}