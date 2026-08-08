---
category: general
date: 2026-04-12
description: 使用 C# 快速將圖形加入 Word。學習如何在 Word 中定位圖形、將圖形插入 docx，以及加入自訂 XML 以實現進階版面配置。
draft: false
keywords:
- add figure to word
- position figure in word
- insert figure into docx
- how to add custom xml
- how to position shape word
language: zh-hant
og_description: 使用 C# 快速將圖形加入 Word。學習如何在 Word 中定位圖形、將圖形插入 docx，並加入自訂 XML 以實現進階版面配置。
og_title: 在 Word 中插入圖形 – 完整 C# 程式設計指南
tags:
- C#
- Word Automation
- Document Generation
title: 在 Word 中加入圖形 – 完整 C# 程式設計指南
url: /zh-hant/net/programming-with-images/add-figure-to-word-complete-c-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Word 中加入圖形 – 完整 C# 程式設計指南

是否曾經需要 **add figure to Word**，卻不知從何下手？你並不孤單。在許多辦公自動化專案中，缺少的往往是一張恰當放置的圖片或圖表，且它位於自訂 XML 部分之中。本指南將完整說明如何 **position figure in Word**、將圖形插入 *.docx* 檔案，甚至微調底層的自訂 XML，讓圖形的行為如同原生 Word 物件。

我們將以 GemBox.Document 函式庫（小檔案免費，大檔案需商業授權）示範真實案例。完成後，你將擁有一個自包含、可執行的程式，能在標記內容容器內的座標 X = 50、Y = 200 處放置圖形。沒有模糊的「請參考文件」捷徑——只有清晰的程式碼、說明為何可行，以及可直接複製到自己專案的技巧。

## 前置條件

- .NET 6.0 或更新版本（程式碼亦可在 .NET Core 3.1 上編譯）
- **GemBox.Document** NuGet 套件（`Install-Package GemBox.Document`）
- 一個起始 Word 檔案（`input.docx`），其中已包含你想放置圖形的自訂 XML 標記
- 基本的 C# 知識（你將了解每一行程式碼的意義）

> **Pro tip:** 若沒有預先標記的文件，你可以在 Word 中插入 *Content Control* → *XML Mapping Pane* → 映射自訂 XML 部分，來建立。函式庫會將該控制項視為 `TaggedContent`。

## 第一步 – 載入來源文件

首先，我們打開既有的 *.docx* 檔案。`Document` 是所有 GemBox 操作的入口點。

```csharp
using GemBox.Document;
using System.Drawing;

// Set the license key (free version uses a limited license key)
ComponentInfo.SetLicense("FREE-LIMITED-KEY");

// Step 1: Load the source document
Document doc = new Document(@"YOUR_DIRECTORY\input.docx");
```

*Why?* 載入檔案後，我們才能存取其內部部件，包括任何自訂 XML 容器。若不這麼做，就找不到將要容納圖形的 `TaggedContent` 節點。

## 第二步 – 取得標記內容（自訂 XML 容器）

自訂 XML 以 *content control* 的形式儲存在 Word 中。GemBox 會將其呈現為 `TaggedContent`。

```csharp
// Step 2: Access the document's tagged content (the container for custom XML)
TaggedContent taggedContent = doc.TaggedContent;
```

如果文件中有多個標記區段，`TaggedContent` 會回傳 **第一個**。你也可以遍歷 `doc.TaggedContents`，依名稱挑選特定標記。

## 第三步 – 建立圖形元素

`FigureElement` 代表圖片、圖表或任何 Word 視為 *shape* 的視覺物件。我們會在標記容器內建立它。

```csharp
// Step 3: Create a new figure element that will be placed inside the tagged content
FigureElement figure = taggedContent.CreateFigureElement();
```

*Why create a figure here?* 把圖形附加到自訂 XML 節點上，Word 便會知道此圖形屬於該邏輯區段，這對日後編輯或以內容控制為基礎的工作流程相當重要。

## 第四步 – 精確定位圖形

Word 使用點 (1 pt ≈ 1/72 in) 作為定位單位。`PointF` 結構讓我們輕鬆設定 X/Y 座標。

```csharp
// Step 4: Position the figure at the desired coordinates (X = 50, Y = 200)
figure.Position = new PointF(50, 200);
```

> **How to position shape word:** `Position` 屬性接受一個 `PointF`，第一個值為水平偏移（左），第二個值為垂直偏移（上），相對於頁面邊界。依需求調整這些數值即可微調位置。

## 第五步 – 將圖形插入標記內容樹

現在把圖形附加到自訂 XML 樹的根元素上，這會實際將形狀加入 Word 文件。

```csharp
// Step 5: Insert the figure into the root element of the tagged content tree
taggedContent.RootElement.AppendChild(figure);
```

此時圖形已存在於文件中，但尚未設定圖像來源。接下來加入一個簡單的 PNG 檔案。

```csharp
// Optional: Load an image and assign it to the figure
using (var imageStream = System.IO.File.OpenRead(@"YOUR_DIRECTORY\sample.png"))
{
    figure.Image = new Image(imageStream);
}
```

## 第六步 – 儲存修改後的文件

最後，我們將變更寫入新的 *.docx* 檔案。

```csharp
// Step 6: Save the updated document
doc.Save(@"YOUR_DIRECTORY\output.docx");
```

當你在 Word 中開啟 `output.docx`，會看到圖片正好位於 (50, 200) 的座標，且位於你先前標記的自訂 XML 區塊內。

### 完整可執行範例

```csharp
using GemBox.Document;
using System.Drawing;
using System.IO;

class Program
{
    static void Main()
    {
        // License (free version)
        ComponentInfo.SetLicense("FREE-LIMITED-KEY");

        // Load the source DOCX
        Document doc = new Document(@"YOUR_DIRECTORY\input.docx");

        // Access the first tagged content container
        TaggedContent taggedContent = doc.TaggedContent;

        // Create a new figure element
        FigureElement figure = taggedContent.CreateFigureElement();

        // Position the figure (X = 50 pt, Y = 200 pt)
        figure.Position = new PointF(50, 200);

        // Load an image file and assign it
        using (FileStream fs = File.OpenRead(@"YOUR_DIRECTORY\sample.png"))
        {
            figure.Image = new Image(fs);
        }

        // Append the figure to the custom XML root
        taggedContent.RootElement.AppendChild(figure);

        // Save the result
        doc.Save(@"YOUR_DIRECTORY\output.docx");
    }
}
```

**Expected result:** 開啟 `output.docx` 後，PNG 圖片會精確出現在你指定的位置，且嵌套於自訂 XML 部分。若檢視文件的 XML（`.docx` → 解壓 → `word/document.xml`），會看到帶有正確 `<v:shape>` 座標的 `<w:pict>` 元素。

## 常見問題與特殊情況

### 若文件有多個標記區段該怎麼辦？

使用 `doc.TaggedContents` 逐一列舉，並依標記名稱選取：

```csharp
TaggedContent myTag = doc.TaggedContents.First(tc => tc.TagName == "MyCustomTag");
```

### 如何為圖形加入說明文字（caption）？

```csharp
figure.Caption = new CaptionElement("Figure 1 – Sample Diagram");
```

### 此方法是否支援 Word 2010 及之後的版本？

是的。GemBox.Document 以 Open XML 標準為目標，兼容 Word 2007 +（包括 2010、2013、2016、2019 以及 Microsoft 365）。

### 若需要旋轉圖形該怎麼做？

```csharp
figure.Rotation = 45; // degrees
```

### 如何加入向量圖形而非點陣圖？

```csharp
figure.Image = new Image(@"YOUR_DIRECTORY\vector.svg");
```

## 專業技巧與常見陷阱

- **檔案路徑:** 使用 `Path.Combine` 以避免硬編碼分隔符，特別是在非 Windows 平台上。
- **授權限制:** 免費版 GemBox 會將文件大小上限設為 20 KB。若處理較大檔案，請購買商業授權金鑰。
- **效能:** 在批次處理時重複使用同一個 `Document` 實例，可大幅降低記憶體開銷。
- **形狀溢位:** 若圖形尺寸超出頁邊距，Word 會裁切它。請調整 `figure.Width` 與 `figure.Height` 以避免此問題。

## 結論

現在你已掌握 **how to add figure to Word**、精確 **position figure in Word**，以及如何操作底層自訂 XML，讓圖形的行為如同任何原生元素。完整、可執行的範例示範了從載入文件、建立 `FigureElement`、設定座標、附加圖像，到最終儲存 *.docx* 的每一步。

接下來，可嘗試透過 **insert figure into docx** 來加入多個圖形、使用迴圈或即時產生圖表。亦可探索 **how to add custom xml** 以建立更豐富的內容控制，或研究 **how to position shape word** 在表格與頁首/頁尾中的應用。可能性無窮，而本指南已為你奠定自動化 Word 文件的基礎。

祝程式開發順利，若遇到任何問題，歡迎留言討論！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}