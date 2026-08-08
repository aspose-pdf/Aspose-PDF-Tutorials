---
category: general
date: 2026-03-24
description: 使用 C# 的 Aspose.PDF 建立 PDF 文件。快速學習如何新增文字方塊 PDF 表單欄位以及新增表單欄位。
draft: false
keywords:
- create pdf document
- add text box pdf
- add form field pdf
- how to create pdf
- how to add textbox
language: zh-hant
og_description: 使用 C# 與 Aspose.PDF 建立 PDF 文件。本指南示範如何在幾分鐘內新增文字方塊 PDF 表單欄位及其他表單欄位。
og_title: 使用 Aspose 建立 PDF 文件 – 新增文字方塊欄位
tags:
- Aspose.PDF
- C#
- PDF Forms
title: 使用 Aspose 建立 PDF 文件 – 新增文字方塊欄位
url: /zh-hant/net/programming-with-forms/create-pdf-document-with-aspose-add-text-box-field/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose 建立 PDF 文件 – 新增文字方塊欄位

曾經需要以程式方式 **create PDF document**，卻不知道從何開始嗎？你並不孤單——許多開發者在需要收集使用者輸入卻不想引入龐大 UI 函式庫時，都會卡在這裡。好消息是？使用 Aspose.PDF for .NET，你可以快速產生 PDF、在任意頁面放置文字方塊，甚至把同一個欄位附加到多個頁面——只需要幾行程式碼。

在本教學中，我們將一步步說明整個流程：從初始化 PDF、**add text box PDF** 表單欄位、**add form field PDF** 註冊，到最後驗證一切是否正常。完成後，你將會知道 **how to create PDF** 檔案的互動方式，並且看到 **how to add textbox** 控制項的行為與原生 Acrobat 欄位完全相同。

---

## 您需要的條件

- **ASP.NET Core** 或任何 .NET 6+ 專案（此程式碼同樣適用於 .NET Framework 4.6+）。  
- **Aspose.PDF for .NET** NuGet 套件（版本 23.9 或更新）。  
- 具備基本的 C# 經驗——不需要高階技巧，只要懂基礎即可。  

如果上述條件皆已符合，我們就可以開始了。無需額外工具、無需外部服務，只要純粹的 C# 程式碼，直接貼到 Console 應用程式中執行即可。

---

## 建立 PDF 文件並新增文字方塊表單欄位

第一步，自然是 **create PDF document**。把 `Document` 類別想像成一張空白畫布；取得它之後，就可以開始繪製頁面、圖形與互動元素。

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Forms;

// Step 1: Create a new PDF document (the blank canvas)
using var document = new Document();

// Step 2: Add a new page where the text box will live
var page1 = document.Pages.Add();
```

> **Why this matters:** 若在未加入任何頁面的情況下實例化 `Document`，在嘗試放置 widget 時會拋出例外。先加入頁面可確保後續使用的頁面索引 (`Pages[1]`) 為有效值。

---

## 在第 1 頁加入文字方塊 PDF 表單欄位

既然已經有頁面，接下來 **add text box PDF** 表單欄位。`TextBoxField` 類別代表單一邏輯欄位；你可以把它想成在多個位置出現的「名稱」。

```csharp
// Step 3: Define the rectangle where the textbox will appear (x, y, width, height)
var textBoxRect = new Rectangle(100, 500, 300, 520);

// Step 4: Create the text box field on page 1
var textBoxField = new TextBoxField(document.Pages[1], textBoxRect)
{
    // This logical name is used later when you retrieve the value
    PartialName = "MultiWidget"
};
```

> **Pro tip:** 矩形使用點 (1/72 英吋) 為單位。請依版面需求調整座標；原點 (0,0) 位於頁面的左下角。

---

## 在另一頁建立第二個 Widget

單一邏輯欄位可以擁有多個視覺 widget——非常適合多頁表單。以下示範 **how to add textbox** 到第二頁，並重複使用相同的欄位名稱。

```csharp
// Step 5: Add a second page for the extra widget
var page2 = document.Pages.Add();

// Step 6: Create a widget for the same field on page 2
var secondWidget = textBoxField.CreateWidget(new Rectangle(100, 400, 300, 420));
```

> **Why we do this:** 使用者常需要在不同區段填寫相同資訊（例如，頁首的「姓名」與摘要中的「姓名」）。透過共享相同的邏輯名稱，Aspose 會確保兩個 widget 同步更新。

---

## 在 PDF 中註冊表單欄位

僅建立欄位物件還不夠，必須將它加入文件的表單集合。這一步就是將 **add form field PDF** 加入內部結構。

```csharp
// Step 7: Register the field (with both widgets) in the document's form collection
document.Form.Add(textBoxField, "MultiWidget");

// Optional: Save the PDF to disk
document.Save("MultiWidgetExample.pdf");
```

> **What happens under the hood:** `Form.Add` 會把欄位定義寫入 AcroForm 字典，使 PDF 在 Acrobat Reader 或任何支援表單的 PDF 閱讀器中具備互動功能。

---

## 執行並驗證結果

編譯並執行 Console 應用程式。於 Adobe Acrobat（或任何支援表單的檢視器）開啟 `MultiWidgetExample.pdf`，你會看到第 1 與第 2 頁各有兩個相同的文字方塊。於其中一個方塊輸入文字——另一個會即時同步更新。這就是共享邏輯欄位的威力。

```text
Expected outcome:
- PDF with two pages.
- Each page shows a white rectangle (the text box).
- Editing one box updates the other automatically.
```

如果看不到方塊，請再次確認矩形座標位於頁面範圍內，且在加入欄位後已正確儲存文件。

---

## 常見問題與特殊情況

### 如果每頁需要不同的外觀該怎麼辦？

你可以在建立後自行客製化每個 widget：

```csharp
secondWidget.Rect = new Rectangle(150, 350, 350, 370); // reposition
secondWidget.Border = new Border(BorderStyle.Solid, 1, Color.Black);
secondWidget.BackgroundColor = Color.LightYellow;
```

### 可以設定預設值嗎？

當然可以——在儲存前給 `Value` 賦值即可：

```csharp
textBoxField.Value = "Enter your name here";
```

所有 widget 都會顯示該預設文字，直到使用者自行覆寫。

### 如何讓欄位成為必填？

```csharp
textBoxField.Required = true;
```

若使用者在未填寫該欄位的情況下嘗試送出表單，Acrobat 會顯示警告。

### 這樣做能符合 PDF/A 標準嗎？

Aspose.PDF 支援 PDF/A‑1b、‑2b、‑3b。完成表單建置後，你可以進行轉換：

```csharp
document.Convert(new PdfConversionOptions { Compliance = PdfCompliance.PdfA2b });
```

---

## 完整範例程式

以下是可直接複製貼上的完整程式。將它儲存為 `Program.cs`，放入 .NET Console 專案，加入 Aspose.PDF NuGet 套件後執行。

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Forms;
using Aspose.Pdf.Drawing;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new PDF document
        using var document = new Document();

        // 2️⃣ Add two pages (page 1 will host the first widget, page 2 the second)
        var page1 = document.Pages.Add();
        var page2 = document.Pages.Add();

        // 3️⃣ Define the rectangle for the first widget
        var rect1 = new Rectangle(100, 500, 300, 520);

        // 4️⃣ Create the text box field (logical name = "MultiWidget")
        var textBoxField = new TextBoxField(document.Pages[1], rect1)
        {
            PartialName = "MultiWidget",
            Value = "Sample text",        // optional default value
            Required = true               // makes the field mandatory
        };

        // 5️⃣ Add a second widget on page

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}