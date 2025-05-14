---
"date": "2025-04-14"
"description": "了解如何使用 Aspose.PDF for Java 建立互動式 PDF 表單。本指南涵蓋新增文字方塊、單選按鈕、組合方塊等。"
"title": "使用 Aspose.PDF Java&#58; 建立互動式 PDF 表單綜合指南"
"url": "/zh-hant/java/forms-annotations/interactive-pdf-forms-asposepdf-java/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}
# 使用 Aspose.PDF Java 輕鬆建立互動式 PDF 表單

## 介紹

對於尋求高效資料收集、簡化工作流程或增強使用者參與度的企業來說，建立互動式動態 PDF 表單至關重要。無論您是希望自動化表單產生的開發人員，還是旨在數位化其流程的組織，掌握在 PDF 中添加表單欄位的技巧都可以顯著提高您的工作效率。

在本教程中，我們將探討如何使用 Aspose.PDF for Java（一個簡化 PDF 文件處理的強大庫）來添加各種表單字段，例如文字方塊、單選按鈕、組合框和簽名字段。透過利用這些功能，您可以建立適合您特定需求的強大、互動式 PDF 文件。

**您將學到什麼：**
- 如何將 Aspose.PDF for Java 整合到您的專案中
- 在 PDF 中新增不同類型表單欄位的逐步說明
- 實際應用和整合可能性

在開始編碼之旅之前，讓我們先深入了解先決條件！

## 先決條件

在開始實現這些功能之前，請確保您的開發環境已正確設定。您需要準備以下物品：

### 所需庫
- **Java 版 Aspose.PDF**：該庫提供了一套全面的工具來處理 PDF 文件。
  
### 環境設定
- **Java 開發工具包 (JDK)**：請確保您的機器上安裝了 JDK。我們推薦版本 8 或更高版本。

### 知識前提
- 對 Java 程式設計和物件導向概念的基本了解將會有所幫助，但不是強制性的。

## 為 Java 設定 Aspose.PDF

要使用 Aspose.PDF for Java，您需要將其包含在專案依賴項中。以下是 Maven 和 Gradle 設定的說明。

### Maven 設定

將以下相依性新增至您的 `pom.xml` 文件：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-pdf</artifactId>
    <version>25.3</version>
</dependency>
```

### Gradle 設定

對於 Gradle，在您的 `build.gradle` 文件：

```gradle
implementation 'com.aspose:aspose-pdf:25.3'
```

#### 許可證取得步驟

您可以獲得臨時許可證來測試 Aspose.PDF，不受評估限制：
- **免費試用**：從下載庫 [Aspose的下載頁面](https://releases。aspose.com/pdf/java/).
- **臨時執照**：透過以下方式取得免費臨時許可證 [此連結](https://purchase.aspose.com/temporary-license/) 在試用期間可存取全部功能。
- **購買**：如果您發現 Aspose.PDF 有用，請考慮從 [Aspose購買頁面](https://purchase。aspose.com/buy).

#### 基本初始化

設定完成後，初始化 `Document` 開始處理 PDF 檔案的對象：

```java
import com.aspose.pdf.Document;

// 初始化新文檔或載入現有文檔
Document pdfDocument = new Document("path/to/your/document.pdf");
```

## 實施指南

讓我們分解一下使用 Aspose.PDF for Java 新增表單欄位的過程。

### 在 PDF 中新增文字方塊欄位 (H2)

文字方塊欄位允許使用者在 PDF 中輸入文本，使其成為資料輸入或回饋表單的理想選擇。

#### 概述
此功能示範如何為現有 PDF 文件新增簡單的文字方塊欄位。

##### 步驟 1：載入文檔

首先，在要新增文字方塊的位置載入PDF文件：

```java
import com.aspose.pdf.Document;
import com.aspose.pdf.TextBoxField;
import com.aspose.pdf.Rectangle;

String dataDir = "YOUR_DOCUMENT_DIRECTORY";
Document pdfDocument = new Document(dataDir + "/input.pdf");
```

##### 步驟2：建立並配置TextBoxField

創建一個 `TextBoxField` 物件使用指定其位置和大小 `Rectangle` 班級：

```java
// 在第 1 頁的指定座標處建立一個 TextBoxField
TextBoxField textBoxField = new TextBoxField(pdfDocument.getPages().get_Item(1), 
    new Rectangle(100, 200, 300, 300));
textBoxField.setPartialName("textbox1");
textBoxField.setValue("Text Box");

// 定義並設定邊界以提高清晰度
import com.aspose.pdf.Border;
import com.aspose.pdf.BorderStyle;
import com.aspose.pdf.Dash;

Border border = new Border(textBoxField);
border.setWidth(5);
border.setDash(new Dash(1, 1));
textBoxField.setBorder(border);

pdfDocument.getForm().add(textBoxField, 1);
```

##### 步驟3：儲存文檔

最後，將更新後的文檔儲存到輸出目錄：

```java
String outputDir = "YOUR_OUTPUT_DIRECTORY";
pdfDocument.save(outputDir + "/output.pdf");
```

#### 故障排除提示
- 確保載入和儲存文件的文件路徑正確。
- 驗證您在輸出目錄中具有寫入權限。

### 在 PDF (H2) 中新增單選按鈕字段

單選按鈕使用戶能夠從多個選項中選擇一個選項，通常用於調查或測驗。

#### 概述
此功能顯示如何為新的 PDF 文件新增單選按鈕欄位。

##### 步驟 1：初始化新文檔

首先創建一個新的 `Document` 目的：

```java
import com.aspose.pdf.Document;
import com.aspose.pdf.RadioButtonField;
import com.aspose.pdf.Rectangle;

String outputDir = "YOUR_OUTPUT_DIRECTORY";
Document pdfDocument = new Document();
pdfDocument.getPages().add(); // 新增空白頁
```

##### 步驟2：建立並設定RadioButtonField

創建一個 `RadioButtonField` 對象，新增具有指定座標的選項：

```java
// 在第一頁上建立一個 RadioButtonField
RadioButtonField radio = new RadioButtonField(pdfDocument.getPages().get_Item(1));
radio.addOption("Test", new Rectangle(20, 720, 40, 740));
radio.addOption("Test1", new Rectangle(120, 720, 140, 740));

pdfDocument.getForm().add(radio);
```

##### 步驟3：儲存文檔

儲存包含新新增的單選按鈕欄位的文件：

```java
pdfDocument.save(outputDir + "/RadioButtonSample.pdf");
```

#### 故障排除提示
- 如果選項重疊或未出現，請仔細檢查它們的座標。

### 在 PDF (H2) 中新增包含三個選項的單選按鈕字段

為了清楚呈現多個選擇，您可以在表格佈局中排列單選按鈕。

#### 概述
此功能示範如何使用表格結構新增具有三個選項的單選按鈕欄位。

##### 步驟1：初始化文件並新增頁面

建立文件並新增頁面：

```java
import com.aspose.pdf.Document;
import com.aspose.pdf.Page;
import com.aspose.pdf.Table;
import com.aspose.pdf.Row;
import com.aspose.pdf.Cell;
import com.aspose.pdf.RadioButtonField;
import com.aspose.pdf.RadioButtonOptionField;
import com.aspose.pdf.TextFragment;
import java.awt.Color;

String outputDir = "YOUR_OUTPUT_DIRECTORY";
Document doc = new Document();
Page page = doc.getPages().add();

// 建立一個表格來儲存單選按鈕
Table table = new Table();
table.setColumnWidths("120 120 120");
page.getParagraphs().add(table);

Row r1 = table.getRows().add();
Cell c1 = r1.getCells().add();
Cell c2 = r1.getCells().add();
Cell c3 = r1.getCells().add();
```

##### 步驟 2：建立 RadioButtonField 和選項

設定單選按鈕字段，在 `RadioButtonField`：

```java
// 使用部分名稱初始化 RadioButtonField 以便識別
RadioButtonField rf = new RadioButtonField(page);
rf.setPartialName("radio");
doc.getForm().add(rf, 1);

// 定義選項
RadioButtonOptionField opt1 = new RadioButtonOptionField();
RadioButtonOptionField opt2 = new RadioButtonOptionField();
RadioButtonOptionField opt3 = new RadioButtonOptionField();

opt1.setOptionName("Option 1");
opt2.setOptionName("Option 2");
opt3.setOptionName("Option 3");

// 向字段添加選項
rf.add(opt1);
rf.add(opt2);
rf.add(opt3);

// 將每個選項放在單獨的儲存格中
c1.getParagraphs().add(opt1);
c2.getParagraphs().add(opt2);
c3.getParagraphs().add(opt3);
```

##### 步驟3：儲存文檔

使用表格佈局儲存您的文件：

```java
doc.save(outputDir + "/RadioButtonTableSample.pdf");
```

#### 故障排除提示
- 確保每個單選按鈕都新增到單獨的儲存格。
- 如果選項顯示不正確，請仔細檢查表格和儲存格座標。

本指南為您提供使用 Aspose.PDF for Java 建立互動式 PDF 表單所需的工具。嘗試不同的欄位類型和配置，以根據特定要求自訂您的文件。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}