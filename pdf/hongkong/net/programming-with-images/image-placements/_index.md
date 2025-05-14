---
"description": "了解如何使用 Aspose.PDF for .NET 擷取和操作 PDF 文件中的影像位置。帶有範例和程式碼片段的分步指南。"
"linktitle": "圖片展示位置"
"second_title": "Aspose.PDF for .NET API參考"
"title": "圖片展示位置"
"url": "/zh-hant/net/programming-with-images/image-placements/"
"weight": 170
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 圖片展示位置

## 介紹

處理 PDF 文件中的圖像可能很棘手，但使用 Aspose.PDF for .NET，您可以輕鬆操作和提取圖像屬性，而無需費力。無論您是想取得影像尺寸、擷取影像尺寸或檢索解析度等其他屬性，Aspose.PDF 都能提供您所需的工具。本教學將逐步指導您如何使用 Aspose.PDF for .NET 擷取 PDF 文件中的影像位置。我們將涵蓋從導入包到檢索影像屬性（如寬度、高度和解析度）的所有內容。

## 先決條件

在我們開始本教學之前，您需要準備好一些東西。以下是一份快速清單：

1. Aspose.PDF for .NET：請確定您已經安裝了 Aspose.PDF for .NET 程式庫。你可以下載 [這裡](https://releases。aspose.com/pdf/net/).
2. 開發環境：您需要在您的機器上安裝 Visual Studio 或任何其他支援 .NET 的 IDE。
3. PDF 文件：準備包含影像的範例 PDF 文件。對於此範例，我們將使用名為 `ImagePlacement。pdf`.
4. 基本 C# 知識：雖然本指南適合初學者，但 C# 的基本知識將幫助您更好地理解程式碼片段。

## 導入包

在我們深入了解程式碼細節之前，您需要做的第一件事就是匯入必要的命名空間。這些套件對於在 Aspose.PDF for .NET 中處理 PDF 文件和影像處理至關重要。

```csharp
using System.IO;
using Aspose.Pdf;
using System;
using System.Drawing;
```

這些軟體包可讓您處理 PDF（`Aspose.Pdf`）、操縱影像位置（`Aspose.Pdf.ImagePlacement`)，並處理影像流和圖形(`System.Drawing` 和 `System.IO`）。

現在我們已經準備好了先決條件和軟體包，讓我們以簡單易懂的指南來分解教程的每個部分。

## 步驟 1：載入 PDF 文檔

第一步是將 PDF 文件載入到您的專案中。這將是處理 PDF 文件內圖像的基礎。

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY"; 
Aspose.Pdf.Document doc = new Aspose.Pdf.Document(dataDir + "ImagePlacement.pdf");
```

在此步驟中，我們使用以下方式定義 PDF 文件的文件路徑 `dataDir` 然後建立一個新的實例 `Aspose.Pdf.Document` 班級。這使我們能夠將 PDF 文件載入到我們的程式中。很簡單，對吧？就像打開一本書開始閱讀一樣，我們現在準備探索裡面的內容。

## 步驟 2：初始化影像放置吸收器

為了提取影像，我們需要一種稱為「影像放置吸收器」的東西。可以想像成一種吸收特定頁面上所有圖像資訊的工具。

```csharp
ImagePlacementAbsorber abs = new ImagePlacementAbsorber();
```

這裡我們創建一個 `ImagePlacementAbsorber`。該物件將收集並儲存有關特定 PDF 頁面上所有影像位置的資訊。想像一下用放大鏡掃描頁面並識別其上的所有圖像！

## 步驟 3：在第一頁接受吸收器

接下來，我們要告訴吸收器要掃描 PDF 的哪一頁。對於這個例子，我們將重點放在第一頁。

```csharp
doc.Pages[1].Accept(abs);
```

這 `Accept` 方法掃描 PDF 文件的第一頁以查找任何圖像，並將結果儲存在 `ImagePlacementAbsorber`。這就像告訴放大鏡在哪裡尋找影像。

## 步驟 4：循環遍歷每個影像位置

現在我們已經掃描了頁面，我們需要循環遍歷頁面上找到的每個圖像並檢索其屬性。

```csharp
foreach (ImagePlacement imagePlacement in abs.ImagePlacements)
{
    Console.Out.WriteLine("image width:" + imagePlacement.Rectangle.Width);
    Console.Out.WriteLine("image height:" + imagePlacement.Rectangle.Height);
    Console.Out.WriteLine("image LLX:" + imagePlacement.Rectangle.LLX);
    Console.Out.WriteLine("image LLY:" + imagePlacement.Rectangle.LLY);
    Console.Out.WriteLine("image horizontal resolution:" + imagePlacement.Resolution.X);
    Console.Out.WriteLine("image vertical resolution:" + imagePlacement.Resolution.Y);
}
```

此循環遍歷頁面上找到的每個圖像。我們正在列印影像的寬度、高度、左下角 x (LLX)、左下角 y (LLY) 和解析度（水平和垂直）。這些詳細資訊可協助您了解 PDF 中每個影像的大小和位置。

## 步驟 5：擷取可見尺寸的影像

收集有關圖像的資訊後，您可能想要提取具有其尺寸的實際圖像。您可以按照以下方法操作。

```csharp
Bitmap scaledImage;
using (MemoryStream imageStream = new MemoryStream())
{
    imagePlacement.Image.Save(imageStream, System.Drawing.Imaging.ImageFormat.Png);
    Bitmap resourceImage = (Bitmap)Bitmap.FromStream(imageStream);
    scaledImage = new Bitmap(resourceImage, (int)imagePlacement.Rectangle.Width, (int)imagePlacement.Rectangle.Height);
}
```

此程式碼片段從 PDF 中檢索圖像並將其縮放到其實際尺寸，如 `ImagePlacement` 目的。透過將圖像保存在記憶體流中並對其進行縮放，您可以確保提取的圖像保持其在 PDF 中顯示的精確大小。

## 結論

一旦您逐步分解，使用 Aspose.PDF for .NET 從 PDF 文件中提取影像位置就非常簡單。我們涵蓋了從加載 PDF 到檢索圖像屬性以及提取具有實際尺寸的圖像的所有內容。 Aspose.PDF 讓處理 PDF 和操作內容變得非常簡單，讓您能夠有效率地處理影像、文字等。

## 常見問題解答

### 我可以從 PDF 的特定頁面提取圖像嗎？  
是的，透過指定頁碼 `Accept` 方法，您可以關注任何特定頁面。

### 支援提取哪些圖像格式？  
Aspose.PDF 支援各種格式，包括 PNG、JPEG、BMP 等。

### 是否可以處理提取的影像？  
絕對地！提取後，您可以使用 `System.Drawing` 命名空間來操作影像。

### 我可以從受密碼保護的 PDF 中提取圖像嗎？  
是的，可以，但在提取圖像之前，您需要使用適當的憑證解鎖 PDF。

### Aspose.PDF for .NET 是否適用於所有 .NET 框架？  
是的，它支援.NET Framework、.NET Core 和 .NET 5 及以上版本。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}