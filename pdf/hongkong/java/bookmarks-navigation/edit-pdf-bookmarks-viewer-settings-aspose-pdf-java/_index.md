---
date: '2025-12-19'
description: 學習如何使用 Aspose.PDF for Java 變更 PDF 頁面版面、編輯 PDF 書籤，並自訂檢視器設定。掌握導覽與版面偏好，提升使用者體驗的流暢度。
keywords:
- edit PDF bookmarks Java
- Aspose.PDF viewer settings
- configure PDF navigation Java
title: 在 Java 中更改 PDF 頁面佈局：編輯書籤與設定
url: /zh-hant/java/bookmarks-navigation/edit-pdf-bookmarks-viewer-settings-aspose-pdf-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}
# 在 Java 中變更 PDF 頁面佈局：編輯書籤與設定

## 介紹
在瀏覽複雜的 PDF 文件時可能會相當繁瑣，尤其是 **change PDF page layout** 設定未正確配置或書籤指向錯誤位置時。在本教學中，您將學習如何使用 Aspose.PDF for Java 來 **change PDF page layout**、**edit PDF bookmarks**，以及 **configure PDF viewer settings**。完成後，您將能完整掌控文件的導覽、書籤目的地，以及文件呈現給讀者的方式。

**您將學習**
- 如何編輯現有的 PDF 書籤，使其指向頁面的起始位置。  
- 如何在建立 PDF 時設定書籤目的地。  
- 如何變更檢視器偏好設定，例如頁面佈局。  
- 在 Java 中載入 PDF 文件的實用技巧與效能最佳化。

### 快速答覆
- **變更 PDF 頁面佈局的主要方式是什麼？** 使用 `PdfContentEditor.changeViewerPreference()` 搭配 `ViewerPreference.PAGE_LAYOUT_SINGLE_PAGE`。  
- **可以在 PDF 建立後編輯書籤目的地嗎？** 可以 – 載入文件、存取大綱，並設定新的 `ExplicitDestination`。  
- **使用這些功能需要授權嗎？** 免費試用版可供評估；完整授權會移除所有限制。  
- **需要哪個 Maven 相依性？** `com.aspose:aspose-pdf:25.3`（或更新版本）。  
- **此功能是否相容於 Java 11 以上？** 完全相容 – Aspose.PDF 支援 Java 8 以上。

## 什麼是「change PDF page layout」？
變更 PDF 頁面佈局可控制檢視器中頁面的顯示方式——單頁、連續、雙頁等。調整此設定可提升可讀性，特別是對於長篇報告或型錄而言。

## 為什麼要編輯 PDF 書籤並設定書籤目的地？
書籤就像目錄一樣。精確的目的地可讓讀者直接跳至目標章節，減少挫折感，提升整體使用體驗。

## 前置條件
- **函式庫與相依性**：Aspose.PDF for Java v25.3 或更新版本。  
- **環境**：JDK 8 或更新，Maven 或 Gradle 建置工具。  
- **知識**：基本的 Java 程式設計與 PDF 概念。

## 設定 Aspose.PDF for Java
### Maven 安裝
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-pdf</artifactId>
    <version>25.3</version>
</dependency>
```
### Gradle 安裝
```gradle
implementation 'com.aspose:aspose-pdf:25.3'
```
**授權取得**：先使用免費試用版或申請臨時授權以取得完整功能。若於正式環境使用，建議購買永久授權。

### 基本初始化
```java
import com.aspose.pdf.Document;

public class PDFSetup {
    public static void main(String[] args) {
        // Initialize document object
        Document pdfDocument = new Document("path/to/your/pdf");
        
        System.out.println("Aspose.PDF for Java initialized successfully.");
    }
}
```

## 實作指南
### 如何在 Java 中變更 PDF 頁面佈局
**概述**：調整檢視器偏好設定，以符合所需的頁面顯示方式。

#### 初始化 PdfContentEditor
```java
import com.aspose.pdf.facades.PdfContentEditor;
import com.aspose.pdf.facades.ViewerPreference;

PdfContentEditor editor = new PdfContentEditor();
editor.bindPdf("YOUR_DOCUMENT_DIRECTORY/input.pdf");
```
#### 變更檢視器偏好設定
```java
editor.changeViewerPreference(ViewerPreference.PAGE_LAYOUT_SINGLE_PAGE);
```
#### 儲存更新的文件
```java
String outputDir = "YOUR_OUTPUT_DIRECTORY/settingViewerPreferences.pdf";
editor.save(outputDir);
```

### 如何編輯 PDF 書籤
**概述**：調整現有書籤，使其正確指向特定頁面的起始位置。

#### 取得書籤
```java
import com.aspose.pdf.Document;
import com.aspose.pdf.ExplicitDestination;
import com.aspose.pdf.OutlineItemCollection;

Document pdfDocument = new Document("YOUR_DOCUMENT_DIRECTORY/input.pdf");
OutlineItemCollection pdfOutline = pdfDocument.getOutlines().get_Item(1);
```
#### 設定新目的地
```java
pdfOutline.setDestination(
    ExplicitDestination.createDestination(pdfDocument.getPages().get_Item(1),
        ExplicitDestinationType.FitH,
        pdfDocument.getPages().get_Item(1).getMediaBox().getHeight())
);
```
#### 儲存變更
```java
String outputDir = "YOUR_OUTPUT_DIRECTORY/bookmarkShouldPointToStartOfPage.pdf";
pdfDocument.save(outputDir);
```

### 如何在建立 PDF 時設定書籤目的地
**概述**：在新產生的 PDF 中建立書籤，直接導向使用者想要的頁面位置。

#### 建立與設定書籤
```java
import com.aspose.pdf.GoToAction;
import com.aspose.pdf.FitVExplicitDestination;

OutlineItemCollection pdfOutline_new = new OutlineItemCollection(pdfDocument.getOutlines());
pdfOutline_new.setTitle("Test Bookmark");
pdfOutline_new.setItalic(true);
pdfOutline_new.setBold(true);
```
#### 定義書籤目的地
```java
pdfOutline_new.setAction(new GoToAction(
    new FitVExplicitDestination(pdfDocument.getPages().get_Item(2), 0)));
```
#### 新增並儲存 PDF
```java
pdfDocument.getOutlines().add(pdfOutline_new);

String outputDir = "YOUR_OUTPUT_DIRECTORY/setDestinationWhileCreatingPDF.pdf";
pdfDocument.save(outputDir);
```

## 實務應用
1. **數位書籍** – 確保每章節書籤位於頁首，提供流暢的閱讀體驗。  
2. **技術手冊** – 精準的導覽協助工程師快速找到所需章節，特別是大型 PDF。  
3. **產品型錄** – 單頁佈局讓在平板上瀏覽型錄更加直觀。

## 效能考量
- **最佳化資源**：處理大型 PDF 時，可使用 `Document.optimizeResources()` 以降低記憶體佔用。  
- **Java 記憶體管理**：明確關閉串流，並在處理完畢後讓垃圾回收器回收物件。

## 常見問題與解決方案
- **書籤未更新**：確認您修改的是正確的大綱索引（`get_Item(1)` 代表第一個頂層書籤）。  
- **檢視器偏好未套用**：確保在變更偏好後呼叫 `editor.save()`，否則變更僅停留在記憶體中。  
- **授權例外**：試用授權可能會加上浮水印，正式環境請取得完整授權。

## 常見問答
**Q: 在 Java 中載入 PDF 文件最簡單的方式是什麼？**  
A: 使用 `new Document("path/to/file.pdf")`；Aspose.PDF 會自動偵測檔案格式。

**Q: 可以不使用 PdfContentEditor 變更頁面佈局嗎？**  
A: 可以，直接在 `Document` 物件上設定檢視器偏好，例如 `pdfDocument.getViewerPreferences().setPageLayout(...)`。

**Q: 變更檢視器佈局會影響列印結果嗎？**  
A: 檢視器佈局僅影響螢幕顯示，不會改變列印輸出。

**Q: 建立書籤的數量有限制嗎？**  
A: 沒有明確上限，但極大的大綱樹可能會影響效能，建議保持結構清晰。

**Q: 在新增或移除頁面後，如何確保書籤目的地仍然正確？**  
A: 在任何結構變更後，重新計算目的地，使用當前的頁面索引。

## 資源
- **文件說明**： [Aspose.PDF Java Reference](https://reference.aspose.com/pdf/java/)  
- **下載**： [Latest Releases for Java](https://releases.aspose.com/pdf/java/)  
- **購買**： [Buy Aspose.PDF License](https://purchase.aspose.com/buy)  
- **免費試用**： [Try Aspose.PDF Free](https://releases.aspose.com/pdf/java/)  
- **臨時授權**： [Request Temporary License](https://purchase.aspose.com/temporary-license)

---

**最後更新：** 2025-12-19  
**測試版本：** Aspose.PDF for Java v25.3  
**作者：** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}