---
category: general
date: 2026-04-25
description: 快速以清晰的 foreach 迴圈範例遍歷 C# 集合。學習如何取得物件名稱並在幾個步驟內顯示字串清單。
draft: false
keywords:
- iterate collection c#
- loop over items
- foreach loop example
- get object names
- display string list
language: zh-hant
og_description: 使用 foreach 迴圈示範在 C# 中遍歷集合。了解如何取得物件名稱並有效率地顯示字串清單。
og_title: 遍歷集合 C# – 逐步循環項目
tags:
- C#
- collections
- loops
title: 遍歷集合 C# – 簡易指南：循環遍歷項目
url: /zh-hant/net/programming-with-operators/iterate-collection-c-simple-guide-to-loop-over-items/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 遍歷集合 C# – 使用 foreach 迴圈範例來循環項目

是否曾經需要 **iterate collection C#**，卻不確定哪種結構能提供最簡潔的程式碼？你並不孤單。在許多專案中，我們常為了印出幾個字串而寫出冗長的 `for` 迴圈——浪費時間且降低可讀性。好消息是，只要一個 `foreach` 迴圈就能從物件中取出所有名稱，並在瞬間 **display string list**。

在本教學中，我們將逐步說明一個完整且可執行的範例，展示如何 **get object names**、循環項目，並將結果輸出至主控台。完成後，你將擁有一段可自行放入任何 .NET 6+ 主控台應用程式的獨立程式碼片段，並附上一些針對邊緣案例與效能的提示。

> **Pro tip:** 如果你正在處理大型集合，考慮使用 `Parallel.ForEach`——但這是另一個日後再談的主題。

## 你將學到什麼

- 如何從物件取得名稱集合（範例中的 `GetSignatureNames`）
- C# 中 **foreach loop example** 的語法與細節
- 在主控台中 **display string list** 的方法，包括格式化技巧
- 循環項目時的常見陷阱（null 集合、空結果）
- 一個完整、可直接複製貼上的程式，你可以立即執行

不需要任何外部函式庫；只要 .NET 隨附的基礎類別庫即可。如果已安裝 .NET SDK，就可以直接開始。

![Iterate collection C# diagram showing a list flowing into a foreach loop and then to the console](/images/iterate-collection-csharp.png "iterate collection c# diagram")

## 步驟 1：設定範例物件

首先，我們需要一個能返回名稱集合的物件。想像一下你有一個 `Signature` 類別，裡面保存了多個簽名；每個簽名都有 `Name` 屬性。`GetSignatureNames` 方法僅僅是將這些名稱提取為 `IEnumerable<string>`。

```csharp
using System;
using System.Collections.Generic;
using System.Linq;

namespace IterateCollectionDemo
{
    // A minimal representation of the object you might be working with
    public class Signature
    {
        private readonly List<string> _names = new()
        {
            "Alice Johnson",
            "Bob Smith",
            "Charlie Davis"
        };

        // This method mimics the real‑world API that returns a collection of names
        public IEnumerable<string> GetSignatureNames()
        {
            // Using LINQ to return a read‑only IEnumerable<string>
            return _names.AsReadOnly();
        }
    }
}
```

**Why this matters:** 透過回傳 `IEnumerable<string>`，我們使方法保持彈性——呼叫端可以列舉、查詢或轉換結果，而不必複製底層清單。這也讓之後的 **loop over items** 變得簡單。

## 步驟 2：撰寫 Foreach 迴圈以顯示字串清單

既然我們已有名稱來源，現在就真正來 **iterate collection C#**。`foreach` 結構會自動從可列舉物件中取出每個元素，無需自行管理索引變數。

```csharp
using System;

namespace IterateCollectionDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Instantiate the object that holds our signatures
            var signature = new Signature();

            // Step 2: Retrieve the collection of signature names from the signature object
            var signatureNames = signature.GetSignatureNames();

            // Step 3: Loop over items and output each name to the console
            foreach (var name in signatureNames)
            {
                Console.WriteLine(name);
            }

            // Keep the console window open when debugging locally
            Console.WriteLine("\nPress any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**程式碼說明：**

1. **Instantiate** `Signature` – 你現在擁有一個知道自己名稱的物件。  
2. **Retrieve** the collection via `GetSignatureNames()` – 這就是 **get object names** 的步驟。  
3. **Foreach loop example** – `foreach (var name in signatureNames)` 會自動遍歷每個字串。  
4. **Display** each `name` with `Console.WriteLine` – 這是於主控台應用程式中 **display string list** 的經典方式。

因為 `signatureNames` 實作了 `IEnumerable<string>`，`foreach` 迴圈即可直接使用，背後自動處理列舉器。無需擔心索引錯誤或手動檢查界限。

## 步驟 3：執行程式並驗證輸出

編譯並執行程式（例如在專案資料夾執行 `dotnet run`）。你應該會看到：

```
Alice Johnson
Bob Smith
Charlie Davis

Press any key to exit...
```

如果沒有任何輸出，請再次確認 `GetSignatureNames` 沒有回傳 `null`。加入簡單的防護檢查可以避免頭痛：

```csharp
var signatureNames = signature.GetSignatureNames() ?? Enumerable.Empty<string>();
```

現在迴圈會優雅地處理缺少的集合，僅輸出空白而不會拋出 `NullReferenceException`。

## 步驟 4：常見變形與邊緣案例

### 4.1 迭代複雜物件清單

通常你不會只處理純字串，而是包含多個屬性的物件。在此情況下，你仍然可以 **loop over items**，並決定要顯示什麼：

```csharp
foreach (var sig in signature.GetAllSignatures())
{
    Console.WriteLine($"{sig.Id}: {sig.Name}");
}
```

此處我們使用字串插值來合併欄位——仍然是 `foreach` 迴圈，只是輸出更豐富。

### 4.2 使用 `break` 提前退出

如果只需要第一個符合的名稱，可在迴圈中使用 `break` 退出：

```csharp
foreach (var name in signatureNames)
{
    if (name.StartsWith("B"))
    {
        Console.WriteLine(name);
        break; // stops after the first B‑name
    }
}
```

### 4.3 平行列舉（進階）

當集合非常龐大且每次迭代都耗費 CPU 時，`Parallel.ForEach` 可以加速處理：

```csharp
System.Threading.Tasks.Parallel.ForEach(signatureNames, name =>
{
    // Simulate work
    Console.WriteLine(name);
});
```

請記得，`Console.WriteLine` 本身是執行緒安全的，但輸出順序會是非決定性的。

## 步驟 5：乾淨且易於維護的迴圈技巧

- **Prefer `foreach` over `for`** 當你不需要索引時；它可減少越界錯誤。  
- **Use `IEnumerable<T>`** 在方法簽名中保持 API 彈性。  
- **Guard against null** 集合可使用 null 合併運算子 (`??`) 進行防護。  
- **Keep the loop body small** — 若發現程式碼行數過多，請抽出成方法。  
- **Avoid modifying the collection** 於迭代過程中修改集合；會拋出 `InvalidOperationException`。

## 結論

我們剛剛示範了如何使用簡潔的 **foreach loop example** 來 **iterate collection C#**，取得 **object names**，並在主控台 **display string list**。完整程式——物件定義、取得與迭代——可直接執行，為任何需要循環項目的情境提供堅實基礎。

從這裡你可以進一步探索：

- 在迴圈前使用 LINQ 進行過濾 (`signatureNames.Where(n => n.Contains("a"))`)  
- 將輸出寫入檔案而非主控台  
- 使用 `IAsyncEnumerable<T>` 進行非同步串流  

試試看這些做法，你會發現 `foreach` 結構的多樣性。對於邊緣案例或效能有疑問嗎？在下方留言，我們祝你編程愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}