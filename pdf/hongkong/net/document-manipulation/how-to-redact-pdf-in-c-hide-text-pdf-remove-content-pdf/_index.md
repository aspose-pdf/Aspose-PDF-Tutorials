---
category: general
date: 2026-03-01
description: 如何使用 Aspose.Pdf 在 C# 中快速對 PDF 進行遮蔽。學習隱藏 PDF 文字、移除 PDF 內容，以及在 PDF 中遮蔽區域，並提供完整可執行的範例。
draft: false
keywords:
- how to redact pdf
- hide text pdf
- remove content pdf
- create pdf document c#
- redact area in pdf
language: zh-hant
og_description: 如何在 C# 使用 Aspose.Pdf 進行 PDF 敏感資訊遮蔽。本指南示範如何隱藏 PDF 文字、刪除 PDF 內容，以及在
  PDF 中遮蔽區域，並提供完整程式碼。
og_title: 如何在 C# 中對 PDF 進行遮蔽 – 隱藏文字 PDF 與刪除內容 PDF
tags:
- Aspose.Pdf
- C#
- PDF Redaction
title: 如何在 C# 中對 PDF 進行遮蔽 – 隱藏文字 PDF 與移除內容 PDF
url: /zh-hant/net/document-manipulation/how-to-redact-pdf-in-c-hide-text-pdf-remove-content-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中遮蔽 PDF – 隱藏文字 PDF 與移除內容 PDF

有沒有想過 **how to redact pdf**，卻不想花上好幾個小時去玩第三方工具？你並不孤單。在許多合規性要求嚴格的專案中，你需要 **hide text pdf**、剔除機密資料，同時保持文件的其他部分完整。

好消息是？使用 Aspose.Pdf for .NET，只要幾行程式碼就能完成這一切。在本教學中，我們將示範如何在 C# 中建立 PDF 文件、定義遮蔽區域，最後儲存乾淨的副本。完成後，你將清楚知道如何 **remove content pdf**、**hide text pdf**，以及 **redact area in pdf**——全部透過可以直接放入任何 .NET 專案的程式碼。

## 前置條件與建置目標

- **.NET 6+**（或 .NET Framework 4.6+ – API 完全相同）
- **Aspose.Pdf for .NET** NuGet 套件（`Aspose.Pdf`）
- 基本的 C# 語法概念（不需要進階技巧）

我們將產生一個名為 `redacted.pdf` 的檔案，裡面會有一個紅色矩形覆蓋座標 (100, 100)‑(300, 200)。矩形下方的任何內容都會被永久移除，這正是當你被要求 **hide text pdf** 以符合 GDPR 或法律需求時所需要的。

> **專業小技巧：** 若需要遮蔽多個不相連的區域，只要在同一頁面上加入更多 `RedactionAnnotation` 物件即可 – 函式庫會一次處理全部。

---

## 如何遮蔽 PDF – 步驟說明

以下每個步驟都會提供簡潔的程式碼片段、說明「為什麼」這行程式碼重要，以及避免常見陷阱的小提醒。

### 1. 建立專案並加入 Aspose.Pdf

首先，建立一個新的 Console 應用程式（或整合到既有服務），然後安裝 NuGet 套件：

```bash
dotnet new console -n PdfRedactionDemo
cd PdfRedactionDemo
dotnet add package Aspose.Pdf
```

> **為什麼？** 安裝套件會把 `Aspose.Pdf` 組件拉進來，裡面包含 `Document`、`RedactionAnnotation` 以及所有低階 PDF 物件。沒有它，你就無法以程式方式 **remove content pdf**。

### 2. 在記憶體中建立 PDF 文件

我們從一個空白 PDF 開始——就像一張全新的紙張，可以隨意書寫。

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using Aspose.Pdf.Redactions;

class Program
{
    static void Main()
    {
        // Step 2: Create a new PDF document in memory
        using var pdfDocument = new Document();

        // (Optional) Add a page with some sample text so you can see the redaction effect
        var page = pdfDocument.Pages.Add();
        page.Paragraphs.Add(new TextFragment("Sensitive data: 123‑45‑6789"));
```

**此步驟的重要性：**  
- `using var` 確保文件正確釋放，釋放原生資源。  
- 加入帶有可見文字的頁面，可讓你驗證遮蔽真的 *移除* 內容，而不是僅僅覆蓋。

### 3. 定義遮蔽註解（即「hide text pdf」區域）

在這裡指定將從頁面中剔除的矩形範圍。

```csharp
        // Step 3: Define a redaction annotation covering the desired area
        var redactionRect = new Rectangle(100, 100, 300, 200);
        var redactionAnnotation = new RedactionAnnotation(redactionRect)
        {
            // Optional: set the fill color to a solid black for visual feedback
            FillColor = Color.Black,
            // Optional: set overlay text that will appear after redaction
            OverlayText = "REDACTED"
        };

        // Attach the annotation to the first page (index 1)
        pdfDocument.Pages[1].Annotations.Add(redactionAnnotation);
```

**為什麼？** `RedactionAnnotation` 告訴 Aspose *在哪裡* 抹除資料。矩形使用 PDF 的座標系統（原點在左下角）。如果你習慣 Windows GDI 座標，記得 Y 軸是相反的。

> **常見錯誤：** 忘記將註解加入 `Pages[1].Annotations`。註解雖然已建立，但不會執行遮蔽。

### 4. 準備資源（例如 XObject） – 進階用法

若打算在遮蔽區域內嵌入圖片或自訂圖形，可先將它們預載到註解的資源字典中。

```csharp
        // Step 4: Access the annotation's resources dictionary (optional)
        var resources = redactionAnnotation.Resources;
        // Example: add an XObject later – omitted here for brevity
```

**為什麼要加這一步？** 即使只需要一個簡單的黑框，將資源字典暴露出來也會向引擎表示你 *可能* 之後會加入額外內容。這是一個無害的呼叫，讓程式碼未來更具彈性。

### 5. 執行遮蔽並儲存 PDF

呼叫 `Redact()` 才會真正抹除內容。之後再把檔案寫入磁碟。

```csharp
        // Step 5: Apply the redaction and save the PDF
        pdfDocument.Redact();   // This processes all redaction annotations
        pdfDocument.Save("redacted.pdf");

        Console.WriteLine("Redacted PDF saved as redacted.pdf");
    }
}
```

**為什麼要呼叫 `Redact()`？** 僅僅加入註解不會改變底層資料流。`Redact()` 會遍歷每個註解，移除被覆蓋的物件，並可選擇加入覆蓋文字。若省略此步，原始資料仍會保留——等於失敗了 **how to redact pdf** 的目的。

---

## 完整範例

將以下程式碼完整貼入 `Program.cs`，然後執行 `dotnet run`。你會在專案資料夾看到 `redacted.pdf`，其中敏感字串已被標示為「REDACTED」的黑框取代。

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using Aspose.Pdf.Redactions;
using Aspose.Pdf.Text;   // For TextFragment
using Aspose.Pdf.Drawing; // For Color

class Program
{
    static void Main()
    {
        // Create a new PDF document in memory
        using var pdfDocument = new Document();

        // Add a page with sample text (so we can see the effect)
        var page = pdfDocument.Pages.Add();
        page.Paragraphs.Add(new TextFragment("Sensitive data: 123‑45‑6789"));

        // Define a redaction annotation covering the desired area
        var redactionRect = new Rectangle(100, 100, 300, 200);
        var redactionAnnotation = new RedactionAnnotation(redactionRect)
        {
            FillColor = Color.Black,
            OverlayText = "REDACTED"
        };
        pdfDocument.Pages[1].Annotations.Add(redactionAnnotation);

        // (Optional) Access resources dictionary – useful for XObjects
        var resources = redactionAnnotation.Resources;

        // Apply redaction and save the PDF
        pdfDocument.Redact();
        pdfDocument.Save("redacted.pdf");

        Console.WriteLine("Redacted PDF saved as redacted.pdf");
    }
}
```

**預期結果：** 開啟 `redacted.pdf` 後，單一頁面上會看不到文字 “Sensitive data: 123‑45‑6789”，而是出現一個實心黑色矩形，中央寫著 “REDACTED”。不會留下任何隱藏的資料流，符合合規審計需求。

---

## 常見問題與特殊情境

| 問題 | 答案 |
|----------|--------|
| **可以一次遮蔽多個頁面嗎？** | 可以 – 只要在 `pdfDocument.Pages` 迴圈中，為每個頁面的 `Annotations` 集合加入 `RedactionAnnotation` 即可。 |
| **如果遮蔽區域與現有圖片重疊會怎樣？** | 遮蔽引擎會移除所有與矩形相交的物件，包括圖片、向量與文字。 |
| **每新增一個註解都要呼叫 `Redact()` 嗎？** | 不需要。等所有註解都加入完畢後，只要呼叫一次即可。 |
| **如何保持原始 PDF 不被改動？** | 將來源檔案載入 `Document`，使用 `var clone = (Document)source.Clone();` 複製一份，對副本執行遮蔽，最後儲存副本。 |
| **遮蔽可以復原嗎？** | 不行。`Redact()` 執行後，原始內容已從 PDF 資料流中剔除。若日後可能需要未遮蔽版本，請先備份。 |

---

## 相關主題推薦

- 使用 PDF 圖層（`OptionalContentGroup`）實作 **hide text pdf** 的可逆遮蔽。  
- 透過低階 PDF 物件模型 **remove content pdf**：刪除頁面或特定物件。  
- 使用 **Create PDF document C#** 建立含表格、圖片與數位簽章的文件。  
- 以自訂覆蓋圖形（例如公司商標）實作 **redact area in PDF**。  

以上主題皆以相同的 `Aspose.Pdf` 基礎為出發點，轉換起來相當順暢。

---

## 結語

現在，你已掌握在 C# 中 **how to redact pdf** 的完整、可投入生產環境的解法。只要建立 `Document`、加入 `RedactionAnnotation`、呼叫 `Redact()`，再儲存檔案，即可可靠地 **hide text pdf**、**remove content pdf**，以及 **redact area in pdf**，不再需要第三方編輯器。

試著在自己的檔案上操作，玩玩多個矩形，甚至自動化批次遮蔽流程。若遇到任何問題，歡迎在下方留言 – 祝開發順利！

--- 

![如何遮蔽 PDF 示例](redaction-example.png){: .align-center alt="如何遮蔽 PDF 示例"}

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}