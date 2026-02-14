---
category: general
date: 2026-02-14
description: 輕鬆為文件加入 Bates 編號 PDF。了解如何在數分鐘內使用 Aspose.Pdf 為 PDF 添加頁腳頁碼與順序編號。
draft: false
keywords:
- add bates numbering pdf
- add footer page numbers
- how to add bates numbers
- add sequential numbers pdf
language: zh-hant
og_description: 快速為 PDF 添加 Bates 編號。本指南展示如何使用 Aspose.Pdf 為 PDF 添加頁腳頁碼和順序編號，並提供完整程式碼與技巧。
og_title: 為 PDF 添加 Bates 編號 – 逐步 C# 教學
tags:
- Aspose.Pdf
- C#
- PDF automation
title: 添加 Bates 編號 PDF – 完整 C# 指南
url: /zh-hant/net/programming-with-stamps-and-watermarks/add-bates-numbering-pdf-complete-c-guide/
---

any other markdown like images none.

Make sure to keep code block placeholders unchanged.

Now produce final content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 新增 Bates 編號 PDF – 完整 C# 指南

是否曾經需要 **新增 Bates 編號 PDF** 檔案卻不知從何下手？你並不孤單。法律團隊、審計師以及所有處理大量文件的人士常常會問：「如何在不破壞版面配置的情況下加入 Bates 編號？」好消息是，使用 Aspose.Pdf for .NET，你可以將這些編號直接注入為簡單的頁腳——無需手動編輯。

在本教學中，我們將逐步說明一個實用的端對端解決方案，不僅 **adds footer page numbers**，還能讓你 **add sequential numbers PDF** 檔案，並自訂前綴、字型大小與對齊方式。完成後，你將擁有一個可直接執行的 C# 程式、清楚了解每個設定的意義，以及避免常見陷阱的幾個專業技巧。

## 你將學到什麼

- 如何載入現有的 PDF 並為 Bates 編號做準備。  
- 哪些 **BatesNumberingOptions** 屬性控制外觀與位置。  
- 如何一次呼叫為每一頁套用編號。  
- 自訂前綴、起始編號與邊距以符合不同法律格式的方法。  
- 邊緣案例處理——如何應對加密的 PDF 或已包含頁腳的文件。  

**Prerequisites**: .NET 6+（或 .NET Framework 4.7+）、最新版本的 Aspose.Pdf（範例使用 23.10）以及你擁有修改權限的輸入 PDF。無需其他第三方函式庫。

---

## 第一步 – 載入要編號的 PDF

我們首先建立一個指向來源檔案的 `Document` 實例。使用 `using var` 模式可確保檔案句柄自動釋放。

```csharp
using Aspose.Pdf;

// Replace with the path to your source PDF
using var doc = new Document("YOUR_DIRECTORY/input.pdf");
```

> **Why this matters:** Aspose.Pdf 會將整個 PDF 結構讀入記憶體，讓我們能在不觸碰磁碟上原始檔案的情況下操作頁面、註解與中繼資料。如果 PDF 受密碼保護，你可以在建構子中傳入密碼——請參閱結尾的「Encrypted PDFs」說明。

---

## 第二步 – 定義你的 Bates 編號選項

Bates 編號本質上是帶有可設定前綴與連續計數器的頁腳。`BatesNumberingOptions` 類別讓你微調每個視覺細節。

```csharp
var batesOptions = new BatesNumberingOptions
{
    // The text that will appear before the numeric part
    Prefix = "ABC-",

    // Starting number; the library will increment this automatically
    StartNumber = 1000,

    // Font size of the footer text (points)
    FontSize = 12,

    // Align the number to the right side of the page
    HorizontalAlignment = HorizontalAlignment.Right,

    // Place the number at the bottom of the page
    VerticalAlignment = VerticalAlignment.Bottom,

    // Margins: left, top, right, bottom (in points)
    Margin = new MarginInfo(0, 20, 0, 0)
};
```

### 快速提示

- **Prefix**：使用簡短且唯一的識別碼（例如案件編號）以保持頁腳易讀。  
- **StartNumber**：法律事務所通常從 `1` 或自訂的起始值開始；選擇符合你檔案編號系統的數字即可。  
- **Margins**：`20` 點的底部邊距可確保文字不會與腳註或已位於頁面邊緣的簽名重疊。  

---

## 第三步 – 為所有頁面套用編號

設定好選項後，實際的注入只需一行程式碼。Aspose.Pdf 會自動處理分頁、更新現有內容流，並遵守頁面旋轉。

```csharp
doc.Pages.AddBatesNumbering(batesOptions);
```

> **What’s happening under the hood?** 這個函式庫會遍歷每個 `Page` 物件，建立包含前綴與目前計數的 `TextFragment`，再使用頁面的座標系統將其繪製。由於我們設定了 `HorizontalAlignment.Right` 與 `VerticalAlignment.Bottom`，文字會自動貼齊右下角，與頁面大小無關。  

---

## 第四步 – 儲存已修改的 PDF

最後，將結果寫入新檔案。雖然可以覆寫原始檔案，但保留副本有助於版本控制。

```csharp
doc.Save("YOUR_DIRECTORY/output.pdf");
```

如果需要保留原始中繼資料（作者、建立日期），Aspose.Pdf 會預設複製。你也可以指定 `SaveOptions` 物件以符合 PDF/A 標準或進行壓縮。

---

## 完整範例程式

以下是完整、可直接執行的程式。將其貼到 Console 應用程式專案中，調整檔案路徑，然後按 **F5**。

```csharp
using Aspose.Pdf;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source PDF
        using var doc = new Document("YOUR_DIRECTORY/input.pdf");

        // 2️⃣ Configure Bates numbering options
        var batesOptions = new BatesNumberingOptions
        {
            Prefix = "ABC-",
            StartNumber = 1000,
            FontSize = 12,
            HorizontalAlignment = HorizontalAlignment.Right,
            VerticalAlignment = VerticalAlignment.Bottom,
            Margin = new MarginInfo(0, 20, 0, 0)
        };

        // 3️⃣ Apply numbering to every page
        doc.Pages.AddBatesNumbering(batesOptions);

        // 4️⃣ Save the output PDF
        doc.Save("YOUR_DIRECTORY/output.pdf");

        System.Console.WriteLine("Bates numbering added successfully!");
    }
}
```

**Expected result:** `output.pdf` 的每一頁現在都會顯示類似 `ABC-1000`、`ABC-1001` … 的頁腳，固定在右下角。使用任何 PDF 閱讀器開啟檔案即可驗證。

---

## 處理常見變化

### 僅加入頁腳頁碼

如果只需要沒有前綴的簡單頁碼，將 `Prefix = ""`，並視需要調整邊距以避免與現有頁腳衝突。

```csharp
batesOptions.Prefix = "";
batesOptions.StartNumber = 1; // classic page numbering
```

### 使用不同的對齊方式

法律文件有時需要將編號置於底部置中。切換對齊方式如下：

```csharp
batesOptions.HorizontalAlignment = HorizontalAlignment.Center;
```

### 處理加密的 PDF

當來源 PDF 受密碼保護時，請這樣提供密碼：

```csharp
using var doc = new Document("secure.pdf", new LoadOptions { Password = "mySecret" });
```

其餘工作流程保持相同。

### 跳過已存在的頁腳

如果文件已包含不想覆寫的頁腳，你可以在前面加上自訂字串以使新編號與之區別，或手動遍歷頁面，只在沒有頁腳的地方加入 `TextFragment`。函式庫的 `Page` 類別提供 `Annotations` 與 `Contents` 集合，以便進行細緻的控制。

---

## 專業提示與常見陷阱

- **Avoid clipping**：過小的底部邊距可能導致列印時文字被裁切。若要發放紙本，請先實體列印測試。  
- **Performance**：在現代筆記型電腦上為 500 頁的 PDF 加入 Bates 編號耗時不到一秒，但大量批次可透過平行處理提升效能——請記得 `Document` 並非執行緒安全，每個執行緒需自行建立實例。  
- **Version compatibility**：此程式碼相容於 Aspose.Pdf 23.10 及更新版本。若使用較舊版本，屬性名稱相同，但 `MarginInfo` 建構子可能需要 `float` 參數。  
- **Legal compliance**：某些司法管轄區要求將 Bates 編號放置於特定位置（例如左下角）。請相應調整 `HorizontalAlignment`。  

---

## 結論

我們剛剛示範了如何使用 Aspose.Pdf for .NET **add Bates numbering PDF** 檔案，涵蓋從載入文件到以乾淨頁腳儲存最終版本的全部步驟。只要微調少數屬性，你亦可 **add footer page numbers**、**add sequential numbers PDF**，或自訂外觀以符合任何法律標準。

準備好進一步了嗎？試著將此技巧與 OCR 文字擷取結合，將可搜尋關鍵字與 Bates 編號一起嵌入，或使用 `Directory.GetFiles` 為整個資料夾自動化處理。可能性無窮，而你現在掌握的基礎將使這些擴充變得輕鬆。

祝開發順利，願你的 PDF 永遠編號完整！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}