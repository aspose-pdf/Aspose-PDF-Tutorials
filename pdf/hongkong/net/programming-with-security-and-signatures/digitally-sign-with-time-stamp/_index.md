---
"description": "了解如何使用 Aspose.PDF for .NET 對帶有時間戳記的 PDF 進行數位簽章。本逐步指南涵蓋先決條件、證書設定、時間戳記等。"
"linktitle": "在 PDF 檔案中使用時間戳進行數位簽名"
"second_title": "Aspose.PDF for .NET API參考"
"title": "在 PDF 檔案中使用時間戳進行數位簽名"
"url": "/zh-hant/net/programming-with-security-and-signatures/digitally-sign-with-time-stamp/"
"weight": 50
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 在 PDF 檔案中使用時間戳進行數位簽名

## 介紹

您是否需要對 PDF 進行數位簽章並添加時間戳以增強安全性？無論您處理的是法律文件、合約或任何需要安全認證的文件，帶有時間戳記的數位簽章都會增加額外的可信度。在本教學中，我們將詳細介紹如何使用 Aspose.PDF for .NET 在您的 PDF 文件中新增數位簽章和時間戳記。別擔心，我們會一步一步來！

## 先決條件

在我們深入研究程式碼之前，您需要進行一些設定才能繼續操作。以下是幫助您入門的先決條件的快速清單：

- Aspose.PDF for .NET 函式庫：您需要在專案中安裝 Aspose.PDF for .NET 函式庫。你可以 [點此下載最新版本](https://releases.aspose.com/pdf/net/) 或透過 NuGet 將其新增至您的專案。
- PDF 文件：您需要一個範例 PDF 文件來使用。確保專案目錄中有一個您想要簽署的檔案。
- 數位憑證（PFX 檔案）：確保您擁有數位憑證（ `.pfx` 文件）對文件進行數位簽章。
- 時間戳 URL：這是一個線上時間戳服務，將用於將時間戳附加到數位簽章。 
- 基本的 C# 知識：您不需要成為專家，但了解 C# 的基礎知識將有助於您理解和自訂程式碼。

一旦勾選了所有這些框，您就可以開始編碼了！

## 導入包

首先，您需要將以下命名空間匯入到您的 C# 專案中。這可確保您可以存取相關的 Aspose.PDF 類別和函數。

```csharp
using System.IO;
using System;
using Aspose.Pdf;
using Aspose.Pdf.Facades;
using Aspose.Pdf.Forms;
using System.Collections;
```

## 步驟 1：載入 PDF 文檔

我們需要做的第一件事是載入我們想要簽署的 PDF 文件。以下是具體操作方法：

```csharp
// 定義文檔目錄的路徑
string dataDir = "YOUR DOCUMENTS DIRECTORY";

// 載入 PDF 文件
Document document = new Document(dataDir + @"DigitallySign.pdf");
```

這一步非常簡單。我們只是定義我們想要簽署的文檔的路徑。這 `Document` Aspose.PDF 中的類別負責載入文件。

## 第 2 步：設定數位簽名

接下來，我們將使用 PKCS7 類別建立數位簽章並載入 PFX 檔案。此 PFX 檔案包含您的憑證和私鑰，它們是簽署文件所必需的。

```csharp
// .pfx 檔案的路徑
string pfxFile = "YOUR DOCUMENTS DIRECTORY\\certificate.pfx";

// 初始化簽名對象
PdfFileSignature signature = new PdfFileSignature(document);

// 使用密碼載入 PFX 文件
PKCS7 pkcs = new PKCS7(pfxFile, "pfx_password");
```

此時，您正在告訴 Aspose 使用您的數位憑證來簽署文件。這 `PKCS7` 物件為您處理所有加密工作，因此您不必擔心細節。

## 步驟3：新增時間戳設置

強大的數位簽章的關鍵組成部分之一是時間戳。這確保了即使證書過期後仍然可以驗證文件的簽名。讓我們使用線上時間戳機構來設定時間戳。

```csharp
// 定義時間戳設置
TimestampSettings timestampSettings = new TimestampSettings("https://您的時間戳網址”，“用戶名：密碼”）；

// 向 PKCS7 物件新增時間戳設置
pkcs.TimestampSettings = timestampSettings;
```

在這裡，您指定時間戳服務的 URL，它將自動為您的簽名提供時間和日期。無論是否經過身份驗證都可以完成此操作。

## 步驟 4：定義簽名位置和外觀

現在，我們將定義簽名在 PDF 中出現的位置及其尺寸。您可以自訂頁面上簽名框的位置以及大小。

```csharp
// 定義簽名的外觀和位置（第 1 頁，指定矩形）
System.Drawing.Rectangle rect = new System.Drawing.Rectangle(100, 100, 200, 100);
```

在這裡，我們定義一個矩形，將簽名定位在 PDF 第一頁的座標 (100, 100) 處，寬度為 200，高度為 100。您可以更改這些值以適合您的設計。

## 步驟5：簽署PDF文檔

一切設定完畢後，就可以將數位簽章實際套用到 PDF 了。此步驟將證書、時間戳記和定位組合成一個簡單的命令。

```csharp
// 在文件第一頁簽名
signature.Sign(1, "Signature Reason", "Contact", "Location", true, rect, pkcs);
```

以下是正在發生的事情：
- 1：這表示簽名應套用於第一頁。
- 「簽名原因」：您可以在此指定簽署文件的原因。
- 「聯絡方式」：輸入簽名人的聯絡方式。
- 「地點」：指定簽名者的位置。
- true：此佈林值表示簽名是否在文件中可見。
- rect：我們先前定義的矩形，指定了簽名的大小和位置。
- pkcs：PKCS7 物件包含數位憑證和時間戳記設定。

## 步驟 6：儲存簽署的 PDF

一旦文件簽署完畢，剩下要做的就是保存它。您可以選擇一個新檔案名稱來保留原始版本和簽名版本。

```csharp
// 儲存已簽署的 PDF 文檔
signature.Save(dataDir + "DigitallySignWithTimeStamp_out.pdf");
```

您新簽名並帶有時間戳記的 PDF 現已儲存到指定目錄！

## 結論

就是這樣！您已成功使用 Aspose.PDF for .NET 對帶有時間戳記的 PDF 進行數位簽署。此流程可確保您的文件的真實性和完整性，讓您和收件人都安心。數位簽章在當今的數位世界中變得越來越重要，因此掌握這個過程絕對是一項值得擁有的技能。

## 常見問題解答

### 我可以使用不同的憑證檔案格式嗎？  
是的，但本教學重點在於如何使用 PFX 文件，這是最常見的數位憑證格式。

### 我需要網路連線來應用時間戳記嗎？  
是的，由於時間戳是從線上時間戳機構獲取的，因此您需要網路存取。

### 我可以在 PDF 中的多個頁面進行簽名嗎？  
絕對地！您可以修改 `signature.Sign()` 方法定位多個頁面或循環遍歷所有頁面。

### 如果 PFX 檔案密碼不正確會發生什麼事？  
如果密碼錯誤，您將收到異常，因此請確保密碼輸入正確。

### 我可以讓簽名不可見嗎？  
是的，您可以透過 `false` 到 `Sign` 方法的可見性參數使簽名不可見。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}