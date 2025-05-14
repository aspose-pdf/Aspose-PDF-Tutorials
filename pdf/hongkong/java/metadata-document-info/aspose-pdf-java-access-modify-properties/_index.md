---
"date": "2025-04-14"
"description": "了解如何使用 Aspose.PDF for Java 存取和修改 PDF 屬性。本指南涵蓋文件元資料、視窗設定、閱讀順序等。"
"title": "如何使用 Aspose.PDF for Java 存取和修改 PDF 屬性&#58;綜合指南"
"url": "/zh-hant/java/metadata-document-info/aspose-pdf-java-access-modify-properties/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}
# 如何使用 Aspose.PDF for Java 存取和修改 PDF 屬性

## 介紹

透過使用以下方式輕鬆存取和修改 PDF 文件的屬性，增強應用程式與 PDF 文件的交互 **Java 版 Aspose.PDF**。本綜合指南將指導您使用 Aspose.PDF 管理各種文件屬性，包括視窗位置、閱讀順序、顯示標題設定等。

**您將學到什麼：**
- 在您的專案中設定適用於 Java 的 Aspose.PDF。
- 使用 Aspose.PDF 方法存取各種文件屬性。
- 配置視窗顯示設定和閱讀順序。
- 解決處理 PDF 時常見的問題。

讓我們來探索一下您開始所需的先決條件！

## 先決條件

在開始之前，請確保您的設定包括：

### 所需庫
- **Java 版 Aspose.PDF**：建議使用 25.3 或更高版本。按照本教程中的詳細說明，透過 Maven 或 Gradle 添加它。

### 環境設定
- 您的機器上安裝了 Java 開發工具包 (JDK)。
- 整合開發環境 (IDE)，如 IntelliJ IDEA、Eclipse 或 NetBeans。

### 知識前提
- 對 Java 程式設計有基本的了解。
- 熟悉專案管理工具，例如 Maven 或 Gradle 進行依賴管理。

有了先決條件後，讓我們繼續設定 Aspose.PDF for Java。

## 為 Java 設定 Aspose.PDF

開始使用 **Java 版 Aspose.PDF**，您需要將其包含在您的項目中。方法如下：

### Maven
將以下相依性新增至您的 `pom.xml` 文件：
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-pdf</artifactId>
    <version>25.3</version>
</dependency>
```

### Gradle
將此行包含在您的 `build.gradle` 文件：
```gradle
implementation 'com.aspose:aspose-pdf:25.3'
```

### 許可證獲取

您可以獲得 **免費試用** Aspose.PDF 的下載位址如下： [發布頁面](https://releases.aspose.com/pdf/java/)。為了繼續使用，您可能需要購買許可證或透過以下方式申請臨時許可證 [購買頁面](https://purchase。aspose.com/buy).

### 基本初始化

使用 Aspose.PDF 設定項目後，請如下初始化它：
```java
import com.aspose.pdf.Document;

public class PdfPropertiesExample {
    public static void main(String[] args) {
        String dataDir = "YOUR_DOCUMENT_DIRECTORY";
        
        // 初始化 Document 對象
        Document pdfDocument = new Document(dataDir + "/Original.pdf");
        
        // 繼續存取文件屬性
    }
}
```

配置 Aspose.PDF 後，我們現在可以探索如何存取和配置 PDF 文件屬性。

## 實施指南

本節將指導您使用 Aspose.PDF 存取 PDF 文件的各種屬性。

### 中心視窗屬性

**概述**：此屬性決定 PDF 視窗在開啟時是否應居中。預設情況下，它設定為 `false`。

#### 步驟
1. **訪問屬性**
   ```java
   boolean centerWindow = pdfDocument.isCenterWindow();
   System.out.println("Is center window enabled? " + centerWindow);
   ```

2. **設定屬性**
   要啟用居中：
   ```java
   pdfDocument.setCenterWindow(true);
   ```

### 閱讀順序

**概述**： 這 `Direction` 屬性指定閱讀順序，例如從左到右（L2R）或從右到左（R2L）。

#### 步驟
1. **訪問屬性**
   ```java
   String direction = pdfDocument.getDirection();
   System.out.println("Reading direction: " + direction);
   ```

2. **設定閱讀順序**
   將其更改為從右到左：
   ```java
   pdfDocument.setDirection(com.aspose.pdf.Document.DirectionType.R2L);
   ```

### 顯示文件標題

**概述**：控制視窗的標題列是否顯示文件標題或文件名稱。

#### 步驟
1. **訪問屬性**
   ```java
   boolean displayDocTitle = pdfDocument.isDisplayDocTitle();
   System.out.println("Is document title displayed? " + displayDocTitle);
   ```

2. **修改設定**
   若要顯示文件標題：
   ```java
   pdfDocument.setDisplayDocTitle(true);
   ```

### 適合視窗

**概述**：此屬性可在開啟時調整視窗大小以適合第一頁。

#### 步驟
1. **訪問屬性**
   ```java
   boolean fitWindow = pdfDocument.isFitWindow();
   System.out.println("Is fit window enabled? " + fitWindow);
   ```

2. **調整設定**
   啟用調整大小：
   ```java
   pdfDocument.setFitWindow(true);
   ```

### 隱藏功能表列和工具列

**概述**：這些屬性控制功能表列和工具列等 UI 元素的可見性。

#### 步驟
1. **訪問屬性**
   ```java
   boolean hideMenuBar = pdfDocument.isHideMenubar();
   System.out.println("Is menu bar hidden? " + hideMenuBar);

   boolean hideToolBar = pdfDocument.isHideToolBar();
   System.out.println("Is tool bar hidden? " + hideToolBar);
   ```

2. **配置可見性**
   要隱藏兩者：
   ```java
   pdfDocument.setHideMenubar(true);
   pdfDocument.setHideToolBar(true);
   ```

### 隱藏視窗 UI

**概述**：當設定為 true 時，此屬性將隱藏除頁面內容之外的所有 UI 元素。

#### 步驟
1. **訪問屬性**
   ```java
   boolean hideWindowUI = pdfDocument.isHideWindowUI();
   System.out.println("Is window UI hidden? " + hideWindowUI);
   ```

2. **啟用設定**
   ```java
   pdfDocument.setHideWindowUI(true);
   ```

### 非全螢幕頁面模式

**概述**：確定退出全螢幕顯示時的頁面模式。

#### 步驟
1. **訪問屬性**
   ```java
   String nonFullScreenPageMode = pdfDocument.getNonFullScreenPageMode();
   System.out.println("Non-full screen page mode: " + nonFullScreenPageMode);
   ```

2. **設定頁面模式**
   更改為縮圖：
   ```java
   pdfDocument.setNonFullScreenPageMode(com.aspose.pdf.Document.PageModeType.Thumbnails);
   ```

### 頁面佈局

**概述**：定義頁面的版面方式，例如單頁或兩列。

#### 步驟
1. **訪問屬性**
   ```java
   String pageLayout = pdfDocument.getPageLayout();
   System.out.println("Page layout: " + pageLayout);
   ```

2. **配置佈局**
   設定為兩列：
   ```java
   pdfDocument.setPageLayout(com.aspose.pdf.Document.PageLayoutType.TwoColumnLeft);
   ```

### 頁面模式

**概述**：控製文件開啟時的顯示方式，包括縮圖和輪廓等選項。

#### 步驟
1. **訪問屬性**
   ```java
   String pageMode = pdfDocument.getPageMode();
   System.out.println("Page mode: " + pageMode);
   ```

2. **設定頁面模式**
   顯示為書籤：
   ```java
   pdfDocument.setPageMode(com.aspose.pdf.Document.PageModeType.Outlines);
   ```

## 實際應用

理解和操作 PDF 屬性在各種情況下都非常有用：

1. **自動產生報告**：自訂客戶端演示的視窗設定。
2. **數位出版**：控制多語言文件的閱讀順序。
3. **使用者介面定制**：透過調整工具列等 UI 元素來增強使用者體驗。
4. **演示模式**：使用非全螢幕頁面模式和佈局調整，以獲得更好的觀看體驗。

## 結論

本指南引導您完成使用 Aspose.PDF for Java 存取和修改 PDF 屬性的過程。透過利用這些功能，您可以增強應用程式與 PDF 文件的交互，為用戶提供更量身定制的體驗。

為了進一步探索，請考慮深入研究 Aspose.PDF 的大量文件並探索可能對您的專案有益的其他功能。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}