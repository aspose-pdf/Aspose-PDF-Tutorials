---
"description": "了解如何使用 Java 和 Aspose.PDF for Java 為您的 PDF 文件新增互動式表單欄位。輕鬆建立使用者友善的 PDF 表單。"
"linktitle": "使用 Java 在 PDF 文件中新增表單字段"
"second_title": "Aspose.PDF Java PDF處理API"
"title": "使用 Java 在 PDF 文件中新增表單字段"
"url": "/zh-hant/java/pdf-form-fields/add-form-field-in-pdf-document-using-java/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Java 在 PDF 文件中新增表單字段


## 介紹

在 PDF 文件中新增表單欄位可允許使用者直接在文件中輸入數據，從而增強其功能。這對於各種目的都非常有用，例如建立可填寫的表格、調查或包含使用者生成內容的報告。

我們將使用 Aspose.PDF for Java，這是一個功能強大的程式庫，可簡化 Java 應用程式中的 PDF 操作。使用 Aspose.PDF，您可以輕鬆建立、修改和操作 PDF 文檔，包括動態新增表單欄位。

## 設定環境

在我們深入研究程式碼之前，您需要設定您的開發環境。請依照以下步驟操作：

1. 下載 Java 的 Aspose.PDF：造訪 Aspose 網站並下載 Java 的 Aspose.PDF 的最新版本。你可以找到它 [這裡](https://releases。aspose.com/pdf/java/).

2. 安裝 Aspose.PDF：下載後，請依照網站上提供的安裝說明安裝 Aspose.PDF。

3. 建立 Java 專案：在您首選的整合開發環境 (IDE) 中建立一個新的 Java 項目，並在您的專案中包含 Aspose.PDF 庫。

## 建立新的 PDF 文檔

讓我們從建立一個新的 PDF 文件開始。在此範例中，我們將建立一個帶有標題和一些說明的簡單 PDF 檔案。

```java
// 導入 Aspose.PDF 庫
import com.aspose.pdf.*;

public class AddFormFieldPDF {
    public static void main(String[] args) {
        // 建立新的 PDF 文檔
        Document doc = new Document();

        // 新增頁面
        Page page = doc.getPages().add();

        // 新增標題
        TextFragment title = new TextFragment("Feedback Form");
        title.getTextState().setFontSize(18);
        title.getTextState().setFont(FontRepository.findFont("Arial"));
        page.getParagraphs().add(title);

        // 新增說明
        TextFragment instructions = new TextFragment("Please provide your feedback below:");
        instructions.getTextState().setFontSize(12);
        page.getParagraphs().add(instructions);

        // 將文件儲存到文件
        doc.save("FeedbackForm.pdf");
    }
}
```

在此程式碼片段中，我們建立一個新的 PDF 文檔，新增一個頁面，並插入一個標題和一些說明。

## 新增表單字段

現在，讓我們繼續將表單欄位新增至我們的 PDF 文件中。我們將包括文字欄位、複選框和單選按鈕來建立互動式回饋表。

### 文字欄位

文字欄位允許使用者輸入文字。新增文字欄位的方法如下：

```java
// 建立文字字段
TextField textField = new TextField(page, new Rectangle(100, 300, 200, 20));
textField.getPdfObject().setBorderStyle(new BorderStyle(1)); // 設定邊框樣式
textField.setPartialName("txtName"); // 設定欄位名稱
textField.setMultiline(false); // 停用多行
page.getAnnotations().add(textField);
```

### 複選框

複選框用於二元選項（例如，是/否問題）。新增複選框的方法如下：

```java
// 建立複選框
CheckboxField checkboxField = new CheckboxField(page, new Rectangle(100, 250, 20, 20));
checkboxField.setPartialName("chkAgree"); // 設定欄位名稱
checkboxField.setChecked(false); // 最初未檢查
page.getAnnotations().add(checkboxField);
```

### 單選按鈕

當使用者需要從一組選項中選擇一個選項時，請使用單選按鈕。每個選項都是一個單獨的單選按鈕，但它們屬於同一組。新增單選按鈕的方法如下：

```java
// 建立單選按鈕
RadioButtonOptionField option1 = new RadioButtonOptionField(page, new Rectangle(100, 200, 20, 20));
RadioButtonOptionField option2 = new RadioButtonOptionField(page, new Rectangle(100, 180, 20, 20));
option1.setPartialName("optYes"); // 設定選項 1 的欄位名稱
option2.setPartialName("optNo"); // 設定選項 2 的欄位名稱

// 為單選按鈕組新增選項
RadioButtonOptionField[] options = {option1, option2};
RadioButtonField radioButtonField = new RadioButtonField(page, options);
page.getAnnotations().add(radioButtonField);
```

透過這些程式碼範例，您可以為 PDF 文件新增文字欄位、複選框和單選按鈕。確保根據需要自訂其屬性，例如欄位名稱和預設值。

## 自訂表單字段

自訂表單欄位可讓您控制其外觀和行為。您可以變更字體大小、文字顏色、邊框樣式等屬性。

### 更改字段屬性

假設您想要更改文字欄位的字體大小和文字顏色：

```java
textField.getTextState().setFontSize(14);
textField.getTextState().setForegroundColor(Color.getGreen());
```

### 字段驗證

您也可以為表單欄位設定驗證規則。例如，您可以要求使用者在文字欄位中輸入有效的電子郵件地址：

```java
textField.getValidation().add(ValidationType.EMAIL);
```

## 設定字段值

若要用資料預先填入表單字段，您可以透過程式設定它們的預設值。這對於建立模板或預填已知資訊很有用。

```java
textField.setValue("John Doe"); // 設定文字欄位的預設值
checkboxField.setChecked(true); // 預設勾選複選框
```

## 表單提交和驗證

新增表單欄位只是故事的一半；你還會想要

 啟用表單提交和驗證。

### 表單提交

為了允許使用者提交表單數據，您需要指定一個操作，例如發送電子郵件或提交到 Web 伺服器。以下是如何設定提交按鈕的範例：

```java
ButtonField submitButton = new ButtonField(page, new Rectangle(100, 50, 80, 30));
submitButton.getPdfObject().setBorderStyle(new BorderStyle(1));
submitButton.getActions().getOnPushButton().add(new SubmitFormAction("https://yourserver.com/submit", SubmitFormActionType.URL, "FeedbackForm.pdf"));
page.getAnnotations().add(submitButton);
```

### 表單驗證

驗證確保使用者輸入符合特定標準。例如，您可以驗證電話號碼欄位僅接受數字：

```java
textField.getValidation().add(ValidationType.NUMBER);
```

## 儲存和匯出

一旦您建立並使用表單欄位自訂了 PDF 文檔，就可以儲存或匯出它了。 Aspose.PDF 為此提供了各種選項。

### 儲存到本機文件

若要將 PDF 文件儲存到本機文件，請使用下列程式碼：

```java
doc.save("FeedbackForm.pdf");
```

### 儲存到流

若要將 PDF 文件儲存到流中，您可以使用 `OutputStream` 班級：

```java
OutputStream outputStream = new FileOutputStream("FeedbackForm.pdf");
doc.save(outputStream);
outputStream.close();
```

## 結論

在本綜合指南中，我們探討如何使用 Java 和 Aspose.PDF for Java 為 PDF 文件新增表單欄位。您已經學習如何建立文字欄位、複選框和單選按鈕、自訂它們的屬性、設定預設值、啟用表單提交和驗證以及儲存/匯出 PDF 文件。

## 常見問題解答

### 如何在 PDF 表單中設定下拉清單？

要在 PDF 表單中建立下拉清單（組合方塊），您可以使用 `ComboBoxField` Aspose.PDF for Java 提供的類別。依照其他表單欄位所示的類似方法，並使用 `AddItem` 方法。您可以在 Aspose 網站上找到有關此內容的詳細文件。

### Aspose.PDF for Java 是否與其他 Java 函式庫和框架相容？

是的，Aspose.PDF for Java 與各種 Java 函式庫和框架相容。您可以將其整合到您的 Java 應用程式中，無論您使用的是 Spring、JavaFX 還是其他流行框架。請務必檢查文件和資源以獲取具體的整合指南。

### 我可以使用密碼保護使用 Aspose.PDF for Java 建立的 PDF 表單嗎？

絕對地！ Aspose.PDF for Java 可讓您為 PDF 文件（包括表單）新增密碼保護。您可以設定使用者級和所有者級密碼來限制存取和權限。有關如何實現此安全功能的詳細說明，請參閱文件。

### 如何提取透過 PDF 表單提交的資料？

要提取透過 PDF 表單提交的數據，您需要在伺服器或應用程式後端處理表單提交。當使用者提交表單時，您可以接收資料並根據需要進行處理。 Aspose.PDF 提供了從伺服器端的 PDF 文件以程式方式提取表單資料的工具。

### 我可以根據使用者輸入動態產生 PDF 表單嗎？

是的，您可以使用 Aspose.PDF for Java 根據使用者輸入動態產生 PDF 表單。根據使用者輸入或應用程式邏輯，您可以建立具有不同表單欄位和佈局的 PDF 文件。這種靈活性使得可以產生適合特定使用者需求或場景的定製表格。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}