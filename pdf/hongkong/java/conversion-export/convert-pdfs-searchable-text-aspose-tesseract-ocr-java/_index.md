---
"date": "2025-04-14"
"description": "了解如何使用 Java 的 Aspose.PDF 和 Tesseract OCR 將基於圖像的 PDF 文件轉換為可搜尋的文字。本指南涵蓋設定、實施和實際應用。"
"title": "如何在 Java 中使用 Aspose.PDF 和 Tesseract OCR 將 PDF 轉換為可搜尋文本"
"url": "/zh-hant/java/conversion-export/convert-pdfs-searchable-text-aspose-tesseract-ocr-java/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}
# 如何在 Java 中使用 Aspose.PDF 和 Tesseract OCR 將 PDF 轉換為可搜尋文本

## 介紹

您是否面臨從掃描或基於圖像的 PDF 文件中提取文字的挑戰？將這些不可搜尋的檔案轉換為可搜尋的格式可以徹底改變資料擷取、存檔和可存取性。本教學將指導您使用 Aspose.PDF for Java 和 Tesseract OCR 來有效地實現這種轉換。

**您將學到什麼：**
- 使用 Java 中的 Tesseract OCR 將 PDF 圖像轉換為文字
- 實現 Aspose.PDF 強大的文件處理功能
- 將處理後的文件儲存為可搜尋的 PDF

有了這些技能，您可以充分發揮文件的潛力。在深入實施之前，請確保一切準備就緒。

## 先決條件

為了有效地遵循本教程，請確保您已：
- 對 Java 程式設計有基本的了解。
- 熟悉 Maven 或 Gradle 的依賴管理。
- Tesseract OCR 軟體的安裝版本（可從 Google 免費取得）。

此外，設定您的開發環境來處理 Java 專案並確保可以存取 Aspose.PDF 庫。

## 為 Java 設定 Aspose.PDF

若要開始在 Java 專案中使用 Aspose.PDF，請透過 Maven 或 Gradle 將其新增為依賴項：

**Maven：**

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-pdf</artifactId>
    <version>25.3</version>
</dependency>
```

**Gradle：**

```gradle
implementation 'com.aspose:aspose-pdf:25.3'
```

### 許可證獲取

您可以獲得免費試用許可證來測試 Aspose.PDF 的功能，或購買臨時許可證進行擴展測試。訪問 [Aspose 的許可頁面](https://purchase.aspose.com/temporary-license/) 了解更多詳情。

要初始化和設定 Aspose.PDF，請確保您已準備好許可證文件並按如下所示應用它：

```java
com.aspose.pdf.License license = new com.aspose.pdf.License();
license.setLicense("path/to/your/license/file.lic");
```

## 實施指南

### 功能 1：使用 Tesseract 進行 OCR 轉換

此功能示範如何使用 Tesseract OCR 將 PDF 中的圖像轉換為文字。

#### 步驟 1：建立 OCR 處理的回調

回呼函數 `CallBackGetHocr` 處理 PDF 中的每個圖像：

```java
import com.aspose.pdf.Document;
import com.aspose.pdf.Document.CallBackGetHocr;
import javax.imageio.ImageIO;
import java.awt.image.BufferedImage;
import java.io.File;
import java.io.FileNotFoundException;
import java.io.IOException;
import java.util.Scanner;

CallBackGetHocr cbgh = new CallBackGetHocr() {
    @Override
    public String invoke(BufferedImage img) {
        String dataDir = "YOUR_DOCUMENT_DIRECTORY";
        String outputDir = "YOUR_OUTPUT_DIRECTORY";

        File outputfile = new File(dataDir + "/test.jpg");
        try {
            // 將緩衝影像寫入 JPEG 文件
            ImageIO.write(img, "jpg", outputfile);
        } catch (IOException e1) {
            e1.printStackTrace();
        }
        
        try {
            // 執行 Tesseract OCR 將圖像轉換為文字並以 HOCR 格式存儲
            java.lang.Process process = Runtime.getRuntime().exec(
                "tesseract " + dataDir + "/test.jpg " + outputDir + "/out hocr"
            );
            process.waitFor();
        } catch (IOException | InterruptedException e) {
            e.printStackTrace();
        }

        // 將產生的 HOCR HTML 檔案讀入字串
        File file = new File(outputDir + "/out.html");
        StringBuilder fileContents = new StringBuilder((int) file.length());
        Scanner scanner = null;
        try {
            scanner = new Scanner(file);
            String lineSeparator = System.getProperty("line.separator");
            while (scanner.hasNextLine()) {
                fileContents.append(scanner.nextLine() + lineSeparator);
            }
        } catch (FileNotFoundException e) {
            e.printStackTrace();
        } finally {
            if (scanner != null)
                scanner.close();
        }

        // 刪除臨時文件
        File fileOut = new File(outputDir + "/out.html");
        if (fileOut.exists()) {
            fileOut.delete();
        }
        File fileTest = new File(dataDir + "/test.jpg");
        if (fileTest.exists()) {
            fileTest.delete();
        }
        return fileContents.toString();
    }
};
```

#### 步驟 2：將 PDF 轉換為可搜尋文本

載入現有的不可搜尋的 PDF 並使用回調進行轉換：

```java
// 定義佔位符目錄路徑
String dataDir = "YOUR_DOCUMENT_DIRECTORY";
String outputDir = "YOUR_OUTPUT_DIRECTORY";

// 載入現有的 PDF 文檔
Document doc = new Document(dataDir + "/outFile.pdf");

// 使用回調函數轉換文件以進行 OCR 處理
doc.convert(cbgh);

// 將轉換後的文件儲存為可搜尋的 PDF
doc.save(outputDir + "/output971.pdf");
```

### 功能2：PDF文件轉換與儲存

套用 OCR 後，以可搜尋的格式儲存您的 PDF。

## 實際應用

1. **歸檔：** 將舊的掃描文件轉換為可搜尋的格式，以便於檢索。
2. **可訪問性：** 透過使文字可供螢幕閱讀器使用來提高可訪問性。
3. **資料探勘：** 從基於圖像的報告或書籍中提取文字資料進行分析。
4. **法律文件：** 轉換法庭記錄和法律文件，以提高可搜尋性。
5. **一體化：** 在 Web 應用程式或文件管理系統中使用轉換過程。

## 性能考慮

- **優化影像品質：** 更高解析度的影像提供更準確的 OCR 結果，但需要更強的處理能力。
- **批次：** 批次處理多個文件以提高效率。
- **記憶體管理：** 監視 Java 記憶體使用情況並為較大的文件適當配置堆大小。

## 結論

使用 Aspose.PDF 和 Tesseract OCR 將 PDF 轉換為可搜尋文字是從基於圖像的文件中解鎖有價值資訊的有效方法。透過遵循本指南，您可以輕鬆地將此功能整合到您的應用程式中。透過定製程式碼來適應特定用例或與其他系統集成，進一步探索。

準備好嘗試了嗎？今天就開始在您的專案中實施這些技術！

## 常見問題部分

**問題1：我可以在沒有許可證的情況下使用 Aspose.PDF for Java 嗎？**
- A1：是的，您可以嘗試 Aspose.PDF 的免費試用版，但它有一定的限制。為了獲得完整的功能，請考慮取得臨時或永久許可證。

**Q2：Tesseract OCR 支援哪些影像格式？**
- A2：Tesseract 支援各種影像格式，包括 JPEG、PNG、TIFF 和 BMP。確保您的影像採用這些格式以獲得最佳效果。

**Q3：如何處理OCR過程中的錯誤？**
- A3：在 OCR 執行程式碼周圍使用 try-catch 區塊實現強大的錯誤處理，以有效管理異常。

**Q4：是否可以將此解決方案整合到 Web 應用程式中？**
- A4：當然！您可以在伺服器環境中部署 Aspose.PDF 和 Tesseract，讓您可以透過 API 或直接與後端系統整合來處理文件。

**Q5：運行 Tesseract OCR 的系統需求是什麼？**
- A5：Tesseract 需要基本的作業系統支援。確保您的機器上安裝了 Java，並具備執行 Tesseract 等外部進程所需的任何權限。

## 資源

- **文件:** 探索詳細指南和 API 參考 [Aspose.PDF文檔](https://reference。aspose.com/pdf/java/).
- **下載：** 透過以下方式存取 Aspose.PDF 的最新版本 [下載頁面](https://releases。aspose.com/pdf/java/).
- **購買：** 直接從 [Aspose 購買頁面](https://purchase。aspose.com/buy).
- **免費試用：** 免費試用以下功能 [Aspose 免費試用](https://releases。aspose.com/pdf/java/#downloads).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}