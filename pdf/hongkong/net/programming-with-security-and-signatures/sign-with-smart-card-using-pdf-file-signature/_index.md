---
"description": "了解如何使用 Aspose.PDF for .NET 的智慧卡簽署 PDF 檔案。請按照本逐步指南取得安全的數位簽章。"
"linktitle": "使用 PDF 檔案簽名透過智慧卡進行簽名"
"second_title": "Aspose.PDF for .NET API參考"
"title": "使用 PDF 檔案簽名透過智慧卡進行簽名"
"url": "/zh-hant/net/programming-with-security-and-signatures/sign-with-smart-card-using-pdf-file-signature/"
"weight": 110
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 使用 PDF 檔案簽名透過智慧卡進行簽名

## 介紹

在數位時代，保護文件安全比以往任何時候都更加重要。無論是合約、協議或任何敏感資訊，確保文件真實且未被篡改是至關重要的。輸入數位簽章！今天，我們將深入研究如何使用 Aspose.PDF for .NET 透過智慧卡簽署 PDF 檔案。這個強大的程式庫允許開發人員有效地操作和建立 PDF 文檔，包括添加安全的數位簽章。那麼，拿起您的智慧卡，讓我們開始吧！

## 先決條件

在我們深入了解簽署 PDF 文件的細節之前，讓我們確保您已準備好所需的一切。以下是一份可幫助您做好準備的清單：

1. Aspose.PDF for .NET：請確定您已安裝 Aspose.PDF 庫。您可以從 [地點](https://releases。aspose.com/pdf/net/).
2. Visual Studio：您可以在其中編寫和執行 .NET 程式碼的開發環境。
3. 智慧卡：您需要一張安裝了有效數位憑證的智慧卡。
4. 對 C# 的基本了解：熟悉 C# 程式設計將會很有幫助，因為我們將用這種語言編寫程式碼片段。
5. PDF 文件：範例 PDF 文件（如 `blank.pdf`）來測試我們的簽名流程。

滿足這些先決條件後，您就可以開始研究程式碼了！

## 導入包

首先，讓我們導入必要的套件。您需要在專案中新增對 Aspose.PDF 庫的引用。您可以按照以下步驟操作：

1. 開啟 Visual Studio。
2. 建立新項目或開啟現有項目。
3. 在解決方案資源管理器中右鍵單擊您的專案並選擇 `Manage NuGet Packages`。
4. 搜尋 `Aspose.PDF` 並安裝最新版本。

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

現在我們已經導入了必要的套件，讓我們逐步分解程式碼。

## 步驟 1：設定文檔

我們流程的第一步是設定我們要簽署的 PDF 文件。您可以按照以下步驟操作：

```csharp
string dataDir = "YOUR DOCUMENTS DIRECTORY";
Document doc = new Document(dataDir + "blank.pdf");
```
在此程式碼片段中，我們定義了文件目錄的路徑，並建立了 `Document` 使用名為 `blank.pdf`。確保更換 `"YOUR DOCUMENTS DIRECTORY"` 與您的 PDF 所在的實際路徑。

## 步驟2：初始化PdfFileSignature

接下來，我們將初始化 `PdfFileSignature` 類，負責處理簽名過程。

```csharp
using (Facades.PdfFileSignature pdfSign = new Facades.PdfFileSignature())
{
    pdfSign.BindPdf(doc);
```
在這裡，我們建立一個實例 `PdfFileSignature` 並將其綁定到我們的PDF文件。這使得文件做好了簽署的準備。

## 步驟3：存取智慧卡證書

現在到了關鍵的部分——存取儲存在智慧卡上的數位憑證。我們可以這樣做：

### 開啟證書存儲

```csharp
System.Security.Cryptography.X509Certificates.X509Store store = new System.Security.Cryptography.X509Certificates.X509Store(System.Security.Cryptography.X509Certificates.StoreLocation.CurrentUser);
store.Open(System.Security.Cryptography.X509Certificates.OpenFlags.ReadOnly);
```
我們開啟位於目前使用者設定檔中的憑證儲存區。這使我們能夠存取您機器上安裝的證書，包括智慧卡上的證書。

### 選擇證書

```csharp
System.Security.Cryptography.X509Certificates.X509Certificate2Collection sel =
    System.Security.Cryptography.X509Certificates.X509Certificate2UI.SelectFromCollection(
        store.Certificates, null, null, System.Security.Cryptography.X509Certificates.X509SelectionFlag.SingleSelection);
```
此程式碼提示使用者從集合中選擇一個憑證。使用者介面將顯示所有可用的證書，讓您可以選擇與您的智慧卡相關聯的證書。

## 步驟 4：建立外部簽名

選擇憑證後，下一步是使用所選憑證建立外部簽章。

```csharp
Aspose.Pdf.Forms.ExternalSignature externalSignature = new Aspose.Pdf.Forms.ExternalSignature(sel[0]);
```
在這裡，我們建立一個實例 `ExternalSignature` 使用選定的證書。該物件將用於簽署 PDF 文件。

## 步驟 5：設定簽名外觀

現在，讓我們來設定簽名的外觀。您可以在此處自訂簽名在文件上的顯示方式。

```csharp
pdfSign.SignatureAppearance = dataDir + "demo.png";
```
在此程式碼片段中，我們透過提供圖像檔案（如徽標或簽名圖形）的路徑來指定簽名的外觀。確保更換 `"demo.png"` 與您想要使用的實際影像。

## 步驟 6：簽署 PDF

一切設定完畢後，就可以簽署 PDF 文件了！

```csharp
pdfSign.Sign(1, "Reason", "Contact", "Location", true, new System.Drawing.Rectangle(100, 100, 200, 200), externalSignature);
pdfSign.Save(dataDir + "externalSignature2.pdf");
```
在此步驟中，我們稱 `Sign` 我們的方法 `pdfSign` 目的。每個參數的意義如下：
- `1`：簽名出現的頁碼。
- `"Reason"`：簽署該文件的原因。
- `"Contact"`：簽名者的聯絡資訊。
- `"Location"`：簽名者所在地。
- `true`：表示是否建立可見簽名。
- `new System.Drawing.Rectangle(100, 100, 200, 200)`：簽名在PDF上的位置和大小。
- `externalSignature`：我們之前建立的簽名對象。

最後，我們將簽署的文檔儲存為 `externalSignature2。pdf`.

## 步驟 7：驗證簽名

簽署文件後，必須驗證簽名是否有效。具體操作如下：

### 初始化驗證流程

```csharp
using (Facades.PdfFileSignature pdfSign = new Facades.PdfFileSignature(new Document(dataDir + "externalSignature2.pdf")))
{
    IList<string> sigNames = pdfSign.GetSignNames();
```
我們建立一個新的實例 `PdfFileSignature` 簽署文件。然後我們檢索文檔中所有簽名的名稱。

### 檢查簽名有效性

```csharp
for (int index = 0; index <= sigNames.Count - 1; index++)
{
    if (!pdfSign.VerifySigned(sigNames[index]) || !pdfSign.VerifySignature(sigNames[index]))
    {
        throw new ApplicationException("Not verified");
    }
}
```
我們循環遍歷每個簽名名稱並驗證其有效性。如果任何簽名驗證失敗，則會拋出異常，表示該簽名無效。

## 結論

就是這樣！您已成功使用帶有 Aspose.PDF for .NET 的智慧卡簽署 PDF 文件。此過程不僅可以保護您的文檔，還可以增加在當今數位世界中至關重要的真實性。無論您處理的是合約、法律文件還是任何敏感訊息，了解如何實施數位簽名都是一項寶貴的技能。 

## 常見問題解答

### 什麼是 Aspose.PDF for .NET？
Aspose.PDF for .NET 是一個功能強大的程式庫，可讓開發人員在 .NET 應用程式內建立、操作和轉換 PDF 文件。

### 我需要智慧卡來簽署 PDF 嗎？
雖然智慧卡不是強制性的，但強烈建議使用智慧卡進行安全數位簽名，因為它提供了額外的安全保障。

### 我可以使用任何 PDF 檔案進行簽名嗎？
是的，您可以使用任何 PDF 文件，但請確保它沒有受密碼保護。如果是，您需要先將其解鎖。

### 如果我沒有數位憑證怎麼辦？
您可以從受信任的證書頒發機構 (CA) 取得數位證書，或使用自簽名證書進行測試。

### 有 Aspose.PDF 的試用版嗎？
是的，您可以從 [Aspose 網站](https://releases。aspose.com/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}