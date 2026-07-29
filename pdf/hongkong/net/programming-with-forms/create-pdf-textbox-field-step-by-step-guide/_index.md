---
category: general
date: 2026-06-21
description: 使用 C# 建立 PDF 文字方塊欄位，並學習如何複製 PDF 表單欄位或在 PDF 表單中加入文字方塊，只需幾行程式碼。
draft: false
keywords:
- create pdf textbox field
- duplicate pdf form field
- add textbox to pdf form
- pdf form automation
- c# pdf library
language: zh-hant
og_description: 快速建立 PDF 文本框欄位。本指南說明如何複製 PDF 表單欄位，並使用現代 C# PDF 函式庫將文本框加入 PDF 表單。
og_title: 建立 PDF 文字方塊欄位 – 完整 C# 教學
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Create PDF textbox field with C# and learn how to duplicate PDF form
    field or add textbox to PDF form in just a few lines of code.
  headline: Create PDF Textbox Field – Step‑by‑Step Guide
  type: TechArticle
- description: Create PDF textbox field with C# and learn how to duplicate PDF form
    field or add textbox to PDF form in just a few lines of code.
  name: Create PDF Textbox Field – Step‑by‑Step Guide
  steps:
  - name: What if I need the field on *more* than two pages?
    text: Just repeat the clone‑and‑add steps for each additional page. The underlying
      data object stays the same, so all widgets stay in sync.
  - name: How do I change the appearance (font, border, background)?
    text: Each `Widget` has a `SetBorderColor`, `SetBorderWidth`, and `SetBackgroundColor`
      method. You can also assign a default appearance string (`DA`) to control the
      font and size.
  - name: Can I make the field read‑only after the user fills it?
    text: Yes. Set the `ReadOnly` flag on the field after you’ve collected the data,
      or toggle it based on your workflow.
  - name: What about PDFs that already contain a form?
    text: If the document already has an AcroForm, `doc.GetForm()` simply returns
      it. You can then add new fields without disturbing existing ones. Just be careful
      to use unique field names.
  type: HowTo
tags:
- PDF
- C#
- FormFields
title: 建立 PDF 文本框欄位 – 步驟指南
url: /zh-hant/net/programming-with-forms/create-pdf-textbox-field-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 建立 PDF 文字方塊欄位 – 完整 C# 教學

是否曾經需要 **create PDF textbox field**，卻不確定該使用哪個 API 呼叫？你並不孤單。無論你是在構建合約簽署平台，還是簡單的資料收集表格，向 PDF 添加互動式文字方塊都是任何表單自動化開發者的核心技能。  

在本指南中，我們將逐步示範一個實用範例，不僅 **adds textbox to PDF form**，還會展示如何 **duplicate PDF form field**，讓相同的輸入出現在多個頁面。完成後，你將擁有一個可直接放入任何 .NET 專案的可執行程式。

## 需要的環境

- .NET 6.0 或更新版本（此程式碼亦可在 .NET Core 上執行）  
- 現代的 C# PDF 函式庫 – 以下範例使用 **PDFTron SDK**，但概念同樣適用於 iText 7、PdfSharp 或其他函式庫。  
- Visual Studio 2022（或任何你喜歡的 IDE）  

就是這樣 – 無需額外服務，亦無奇怪的相依性。如果你已經有要增強的 PDF，只需將程式碼指向該檔案即可。

---

## 步驟 1：設定專案並匯入 SDK

首先，建立一個 console 應用程式：

```bash
dotnet new console -n PdfFormDemo
cd PdfFormDemo
```

加入 PDFTron NuGet 套件：

```bash
dotnet add package PDFTron.NET
```

現在開啟 `Program.cs`，並引入我們需要的命名空間：

```csharp
using System;
using pdftron;
using pdftron.Common;
using pdftron.PDF;
using pdftron.SDF;
```

> **專業提示：** 若你使用其他函式庫，請將 `using` 陳述式替換為等效的（例如 iText 7 使用 `iText.Kernel.Pdf`）。

## 步驟 2：初始化 PDF 文件與表單

我們將從一個包含兩頁的全新 PDF 開始 – 第一頁作為原始文字方塊的來源頁，第二頁作為複製目標頁。

```csharp
PDFNet.Initialize();                     // Initialize the PDFTron runtime

// Create a new PDF document
using (PDFDoc doc = new PDFDoc())
{
    // Add two blank pages (letter size)
    Page sourcePage = doc.PageCreate(new Size(612, 792));
    doc.PagePushBack(sourcePage);
    Page targetPage = doc.PageCreate(new Size(612, 792));
    doc.PagePushBack(targetPage);

    // Get (or create) the AcroForm object
    Form form = doc.GetForm();
```

`Form` 物件是所有互動欄位所在的地方。如果文件尚未有表單，`GetForm()` 會為我們建立一個。

## 步驟 3：在第一頁 **Create PDF Textbox Field**

現在進入本教學的核心 – 建立文字方塊欄位。矩形座標以點 (point) 為單位表示 (1 英吋 = 72 點)。此範例將方塊放置於第一頁的上方中央附近。

```csharp
    // Step 1: Create a text box field on the first page and set its initial value
    TextBoxField textBoxField = new TextBoxField(sourcePage, new Rect(100, 500, 300, 520))
    {
        Value = "Sample"
    };
```

為什麼要立即設定 `Value`？預先填入欄位可為使用者提供預期輸入的提示，同時也示範該欄位已完整運作。

## 步驟 4：將欄位加入表單 – **Add Textbox to PDF Form**

接下來，我們使用具意義的名稱將欄位註冊至表單。稍後若需以程式方式讀取或修改欄位資料時，即會使用此名稱。

```csharp
    // Step 2: Add the field to the form with a logical name
    form.Add(textBoxField, "multiBox");
```

選擇清晰的名稱（例如 `"multiBox"`）能讓後續程式碼更易讀，尤其當你有數十個欄位時。

## 步驟 5：在另一頁 **Duplicate PDF Form Field**

常見需求是將相同欄位顯示於多個頁面 – 例如每張發票頁面都出現的「客戶名稱」方塊。PDFTron 允許我們複製 widget 註解，即欄位的視覺呈現。

```csharp
    // Step 3: Clone the field's widget annotation so it can appear on another page
    Widget clonedWidget = textBoxField.CreateWidgetAnnotation();

    // Step 4: Place the cloned widget on the second page
    targetPage.Annotations.Add(clonedWidget);
```

被複製的 widget 與原始文字方塊共享相同的底層資料。使用者在其中一個實例輸入時，另一個會自動同步更新 – 這就是 **duplicate PDF form field** 的魔力。

## 步驟 6：儲存文件並清理資源

最後，將 PDF 寫入磁碟並關閉 PDFNet 執行環境。

```csharp
    // Save the resulting PDF
    doc.Save("output.pdf", SDFDoc.SaveOptions.e_linearized);
    Console.WriteLine("PDF created: output.pdf");
}

// Shut down PDFNet (optional but good practice)
PDFNet.Terminate();
```

執行程式會產生一個兩頁的 PDF（`output.pdf`）。在 Adobe Acrobat Reader 中開啟，點擊第 1 頁的文字方塊並輸入內容，然後切換至第 2 頁 – 相同的文字會即時顯示。這是一個完整可運作的 **create pdf textbox field** 範例，且包含複製的欄位。

---

## 完整可執行範例（直接複製貼上）

```csharp
// Program.cs
using System;
using pdftron;
using pdftron.Common;
using pdftron.PDF;
using pdftron.SDF;

class Program
{
    static void Main()
    {
        PDFNet.Initialize();

        using (PDFDoc doc = new PDFDoc())
        {
            // Create two pages
            Page sourcePage = doc.PageCreate(new Size(612, 792));
            doc.PagePushBack(sourcePage);
            Page targetPage = doc.PageCreate(new Size(612, 792));
            doc.PagePushBack(targetPage);

            // Get the form (creates one if missing)
            Form form = doc.GetForm();

            // Step 1: Create a text box field on the first page
            TextBoxField textBoxField = new TextBoxField(sourcePage,
                new Rect(100, 500, 300, 520))
            {
                Value = "Sample"
            };

            // Step 2: Add the field to the form
            form.Add(textBoxField, "multiBox");

            // Step 3: Clone the widget so it appears on page 2
            Widget clonedWidget = textBoxField.CreateWidgetAnnotation();

            // Step 4: Attach the cloned widget to the second page
            targetPage.Annotations.Add(clonedWidget);

            // Save the file
            doc.Save("output.pdf", SDFDoc.SaveOptions.e_linearized);
            Console.WriteLine("PDF created: output.pdf");
        }

        PDFNet.Terminate();
    }
}
```

**預期輸出：** 產生名為 `output.pdf` 的檔案，內含兩頁。兩頁皆顯示標示為「Sample」的相同可編輯文字方塊。編輯其中一個會即時同步更新另一個。

---

## 常見問題與邊緣案例

### 如果需要在 *超過兩頁* 上放置欄位該怎麼辦？

只需對每個額外頁面重複「複製並加入」的步驟。底層資料物件保持不變，所有 widget 會同步。

```csharp
Widget anotherClone = textBoxField.CreateWidgetAnnotation();
thirdPage.Annotations.Add(anotherClone);
```

### 如何變更外觀（字型、邊框、背景）？

每個 `Widget` 都有 `SetBorderColor`、`SetBorderWidth` 與 `SetBackgroundColor` 方法。你也可以指定預設外觀字串（`DA`）來控制字型與大小。

```csharp
textBoxField.SetBorderColor(new ColorPt(0, 0, 1), 3); // blue border
textBoxField.SetBackgroundColor(new ColorPt(0.9, 0.9, 0.9), 3); // light gray fill
textBoxField.SetDefaultAppearance("Helvetica 12 Tf 0 g");
```

### 使用者填寫後，我可以將欄位設為唯讀嗎？

可以。於收集完資料後，將欄位的 `ReadOnly` 標誌設為 true，或依工作流程切換此屬性。

```csharp
textBoxField.SetFlag(Field.Flag.e_readonly, true);
```

### 已有表單的 PDF 該怎麼處理？

如果文件已經有 AcroForm，`doc.GetForm()` 只會回傳該表單。之後即可新增欄位而不影響既有欄位。只要注意使用唯一的欄位名稱即可。

---

## 真實專案的實用技巧

- **命名慣例：** 在欄位名稱前加上頁面或區段前綴（例如 `invoice_customer_name`），以避免衝突。  
- **驗證：** 若需要客戶端驗證，可使用 JavaScript 動作（`field.SetAction(Field.Action.e_keystroke, "event.rc = /^[A-Za-z]+$/.test(event.change);")`）。  
- **效能：** 處理大型 PDF 時，於批次操作前呼叫 `doc.Lock()` 以減少 I/O 開銷。  
- **無障礙：** 設定 `AlternateName` 屬性，讓螢幕閱讀器能描述此欄位。

---

## 結論

我們剛剛 **created a PDF textbox field**，示範了如何在多頁間 **duplicate PDF form field**，並展示了使用 C# 最簡單的 **add textbox to PDF form** 方法。完整、可執行的程式碼已於上方提供，你可以依需求加入樣式、驗證或更多頁面進行擴充。  

準備好進一步了嗎？試著嵌入下拉選單（`ChoiceField`）或簽名元件，或探索在資料輸入後將表單扁平化以便存檔的方式。PDFTron SDK（或任何類似函式庫）提供了構建基礎——最終形態由你的想像決定。  

如果遇到問題，歡迎在下方留言或查閱函式庫的官方文件；其中有許多範例與本教學相輔相成。祝開發愉快，願你的表單永遠保持同步！

## 接下來該學什麼？

以下教學涵蓋與本指南緊密相關的主題，建立於此處示範的技巧之上。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助你精通更多 API 功能，並在自己的專案中探索替代實作方式。

- [如何使用 Aspose 建立 PDF – 新增表單欄位與頁面](/pdf/english/net/programming-with-forms/how-to-create-pdf-with-aspose-add-form-field-and-pages/)
- [使用 Java 在 PDF 文件中新增表單欄位](/pdf/english/java/pdf-form-fields/add-form-field-in-pdf-document-using-java/)
- [使用 Java 在 PDF 文件中新增表單欄位（德語）](/pdf/german/java/pdf-form-fields/add-form-field-in-pdf-document-using-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}