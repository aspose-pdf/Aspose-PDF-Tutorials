---
"description": "透過本引人入勝的逐步指南，學習如何使用 Aspose.PDF for .NET 為 PDF 檔案添加墨跡註釋。"
"linktitle": "新增 lnk 註釋"
"second_title": "Aspose.PDF for .NET API參考"
"title": "新增 lnk 註釋"
"url": "/zh-hant/net/annotations/addlnkannotation/"
"weight": 20
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 新增 lnk 註釋

## 介紹

歡迎來到使用 Aspose.PDF for .NET 進行 PDF 操作的世界！如果您想增強 PDF 文件的功能，無論是用於專業用途、個人專案或其他用途，您都來對地方了。今天，我們將深入研究 Aspose.PDF 的一個具體而實用的功能：為您的 PDF 文件添加墨跡註釋。當您想要在文件中添加類似手寫的註釋或簽名時，此功能非常有用，可以使文件更具互動性和吸引力。

## 先決條件

在我們深入研究編碼魔法之前，讓我們確保您擁有開始所需的一切：

1. .NET Framework：確保您的機器上安裝了.NET。該程式庫可與包括 .NET Core 在內的各種版本的 .NET 無縫協作。
2. Aspose.PDF 庫：您需要下載 .NET 的 Aspose.PDF 庫並在專案中引用。如果你還沒有這樣做，你可以從 [下載連結](https://releases。aspose.com/pdf/net/).
3. 程式碼編輯器：您可以使用任何您選擇的程式碼編輯器，但強烈建議使用 Visual Studio，因為它易於與 .NET 應用程式一起使用。
4. 對 C# 的基本了解：對 C# 的工作知識將幫助您順利瀏覽編碼範例。
5. 設定您的開發環境：確保您的 IDE 已設定為處理 .NET 項目，並且您已在專案中正確引用 Aspose.PDF 庫。 

滿足這些先決條件後，您就可以開始為 PDF 添加墨跡註釋了！

## 導入包

在開始編碼之前，讓我們先導入必要的套件。在 C# 檔案的頂部，加入以下 using 語句：

```csharp
using System.IO;
using Aspose.Pdf.Annotations;
using Aspose.Pdf;
using System;
using System.Collections;
using System.Collections.Generic;
```

這將授予您存取處理 PDF 註釋所需的所有類別和方法的權限。

現在我們已經做好了準備，是時候捲起袖子，開始做細節工作了！我們將分解每個步驟，以確保您準確了解如何建立和添加墨跡註釋到您的 PDF 文件。

## 步驟1：設定文檔和目錄

您要做的第一件事是設定您的文件以及您想要儲存輸出文件的路徑。 

```csharp
string dataDir = "YOUR DATA DIRECTORY";
Document doc = new Document();
```
我們定義一個變數 `dataDir`，它指向將保存生成的 PDF 的目錄。這 `Document` 然後實例化對象，建立一個新的 PDF 文件以供編輯。

## 步驟 2：新增頁面

接下來，您需要為新建立的文件新增一個頁面。

```csharp
Page pdfPage = doc.Pages.Add();
```
在這裡，我們在文件中新增一個新頁面。每個 PDF 至少需要一頁，因此這一步至關重要。

## 步驟3：定義繪圖矩形

在繪製任何內容之前，您需要定義在頁面上放置墨跡註釋的位置。

```csharp
System.Drawing.Rectangle drect = new System.Drawing.Rectangle();
drect.Height = (int)pdfPage.Rect.Height;
drect.Width = (int)pdfPage.Rect.Width;
drect.X = 0;
drect.Y = 0;
Aspose.Pdf.Rectangle arect = Aspose.Pdf.Rectangle.FromRect(drect);
```
在這裡，我們創建一個 `Rectangle` 物件指定了頁面上我們將新增墨跡註解的區域。我們將其尺寸設定為適合整個頁面，從 (0,0) 開始。

## 步驟4：準備墨點

現在到了最有趣的部分——定義構成墨跡註釋的點。 

```csharp
IList<Point[]> inkList = new List<Point[]>();
Aspose.Pdf.Point[] arrpt = new Aspose.Pdf.Point[3];
inkList.Add(arrpt);
arrpt[0] = new Aspose.Pdf.Point(100, 800);
arrpt[1] = new Aspose.Pdf.Point(200, 800);
arrpt[2] = new Aspose.Pdf.Point(200, 700);
```
此程式碼區塊建立 Point 數組列表，其中每個數組代表一組墨跡筆畫的點。這裡，我們定義三個點形成一個三角形；您可以調整座標以適合您的設計。

## 步驟 5：建立墨跡註釋

定義好要點後，就可以建立實際的墨水註解了。

```csharp
InkAnnotation ia = new InkAnnotation(pdfPage, arect, inkList)
{
    Title = "XXX",
    Color = Aspose.Pdf.Color.LightBlue,
    CapStyle = CapStyle.Rounded
};
```
我們實例化 `InkAnnotation` 對象，傳入頁、矩形和墨點。此外，我們也設定了一些屬性，例如 `Title`， `Color`， 和 `CapStyle`。客製化這些以滿足您的需求！

## 步驟 6：設定邊框和不透明度

想要讓您的註解脫穎而出嗎？讓我們賦予它一些風格。

```csharp
Border border = new Border(ia);
border.Width = 25;
ia.Opacity = 0.5;
```
在這裡，我們為註釋添加具有特定寬度的邊框並設定其不透明度，使其半透明。

## 步驟 7：為頁面新增註釋

現在您的註釋已準備好，是時候將其新增至 PDF 頁面了。

```csharp
pdfPage.Annotations.Add(ia);
```
此行將我們先前建立的墨跡註解新增至頁面的註解集合中。 

## 步驟8：儲存文檔

最後，讓我們儲存修改後的文件。

```csharp
dataDir = dataDir + "AddInkAnnotation_out.pdf";
doc.Save(dataDir);
Console.WriteLine("\nInk annotation added successfully.\nFile saved at " + dataDir);
```
我們修改我們的 `dataDir` 包括輸出檔名並儲存文件。確認訊息會列印到控制台，讓您知道一切順利。

## 結論

就是這樣！您已成功使用 Aspose.PDF for .NET 為您的 PDF 文件新增墨跡註解。這個簡單而有效的功能可以增強您的文件並使其具有互動性。無論您添加簽名、註釋還是塗鴉，墨跡註釋都提供了豐富內容的獨特方式。

## 常見問題解答

### 什麼是 Aspose.PDF？
Aspose.PDF 是一個用於在 .NET 應用程式中建立、操作和轉換 PDF 文件的程式庫。

### 我可以免費使用 Aspose.PDF 嗎？
是的！ Aspose 提供免費試用版來評估其產品。你可以下載 [這裡](https://releases。aspose.com/).

### 可以新增多個墨跡註解嗎？
絕對地！您可以建立多個 `InkAnnotation` 物件並將它們新增至文件頁面。

### 在哪裡可以找到更多範例？
您可以查看 [文件](https://reference.aspose.com/pdf/net/) 以獲得詳細的教學和範例。

### 如果我需要支援該怎麼辦？
如果您遇到任何問題，可以向 [支援論壇](https://forum。aspose.com/c/pdf/10).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}