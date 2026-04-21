---
date: '2026-04-21'
description: 學習如何使用 Aspose.PDF for Java 將 PDF 匯出為 TIFF、減少 TIFF 檔案大小，並以實作範例將 PDF 頁面轉換為
  TIFF。
keywords:
- export pdf as tiff
- reduce tiff file size
- convert pdf to tiff java
- convert pdf page tiff
- generate tiff from pdf
title: 在 Java 中將 PDF 匯出為 TIFF：使用 Aspose.PDF 的完整指南
url: /zh-hant/java/conversion-export/convert-pdf-to-tiff-aspose-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}
# 在 Java 中將 PDF 匯出為 TIFF

## 介紹
您是否正在尋找 **export PDF as TIFF**？無論您是為了歸檔、分享，或是從 PDF 中提取高品質影像，掌握此轉換都能為您節省時間與精力。使用 **Aspose.PDF for Java**，您可以將整個 PDF 或僅選取的頁面轉換為 TIFF 影像，並控制解析度、壓縮，甚至 **reduce TIFF file size**。在本教學中，我們將一步步帶您了解所有必備資訊——從環境設定到程式碼實作，讓您能自信地 **convert PDF to TIFF Java**。

**您將學習**
- 如何在專案中設定 Aspose.PDF for Java  
- 如何 **convert PDF page TIFF**（單頁或範圍）  
- 降低 **reduce TIFF file size** 並提升效能的技巧  

讓我們深入了解此轉換過程所需的前置條件。

## 快速答案
- **主要的函式庫是什麼？** Aspose.PDF for Java  
- **我能以單行程式碼匯出 PDF 為 TIFF 嗎？** 可以，使用 `TiffDevice.process()`  
- **哪個設定可減少檔案大小？** 使用較低 DPI 的 CCITT4 壓縮  
- **是否能只轉換特定頁面？** 當然可以——使用重載的 `process()` 方法  
- **正式環境是否需要授權？** 需要，付費授權可移除評估限制  

## 前置條件
在實作之前，請確保您已準備好以下項目：
- **Java Development Kit (JDK)** – 任意較新版本（建議 8 以上）  
- **IDE** – IntelliJ IDEA、Eclipse 或您喜愛的 Java 編輯器  
- **Aspose.PDF for Java** 函式庫 – 透過 Maven 或 Gradle 加入（請參閱下一節）  

## 設定 Aspose.PDF for Java
要開始，請使用 Maven 或 Gradle 將 Aspose.PDF for Java 函式庫加入您的專案：

**Maven:**
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-pdf</artifactId>
    <version>25.3</version>
</dependency>
```

**Gradle:**
```gradle
implementation 'com.aspose:aspose-pdf:25.3'
```

### 授權取得
Aspose.PDF 提供免費試用、臨時授權供評估，以及完整功能的購買選項：
- **免費試用：** 從 [release page](https://releases.aspose.com/pdf/java/) 下載以試用其功能。  
- **臨時授權：** 前往此 [link](https://purchase.aspose.com/temporary-license/) 取得臨時授權。  
- **購買：** 若需完整功能，請於此處購買授權：[Aspose Purchase Page](https://purchase.aspose.com/buy)。  

一旦您正確設定函式庫並取得授權，我們即可繼續實作 PDF 轉 TIFF 的流程。

## 實作指南

### 將所有 PDF 頁面轉換為單一 TIFF 影像
#### 為何要轉換所有頁面？
建立單一多頁 TIFF 適合用於歸檔，或在需要單一檔案簡化後續處理時使用。

#### 步驟說明
**1. 開啟 PDF 文件**  
```java
Document pdfDocument = new Document("YOUR_DOCUMENT_DIRECTORY/input.pdf");
```

**2. 為 TIFF 影像建立輸出串流**  
```java
java.io.OutputStream imageStream = new java.io.FileOutputStream("YOUR_OUTPUT_DIRECTORY/Converted_Image.tiff");
```

**3. 設定解析度與 TiffSettings**  
```java
Resolution resolution = new Resolution(300);
TiffSettings tiffSettings = new TiffSettings();
tiffSettings.setCompression(CompressionType.CCITT4);
tiffSettings.setDepth(ColorDepth.Format8bpp);
tiffSettings.setSkipBlankPages(true);
```
- **解析度：** 300 DPI 可提供列印品質。降低 DPI（例如 150）可 **reduce TIFF file size**。  
- **壓縮：** CCITT4 適用於黑白文件，可協助縮小檔案大小。  
- **色彩深度：** 8 bpp 在細節與檔案大小之間取得平衡。

**4. 初始化 TiffDevice**  
```java
TiffDevice tiffDevice = new TiffDevice(resolution, tiffSettings);
```

**5. 轉換並儲存 TIFF 影像**  
```java
tiffDevice.process(pdfDocument, imageStream);
imageStream.close();
```
`process()` 方法會將每一頁渲染成單一多頁 TIFF。關閉串流可確保所有資料寫入磁碟。

### 將特定 PDF 頁面轉換為 TIFF
#### 何時需要這樣做？
有時您只需要縮圖或單一頁面作為預覽用途。

#### 步驟說明
**1. 開啟 PDF 文件**  
```java
Document pdfDocument = new Document("YOUR_DOCUMENT_DIRECTORY/input.pdf");
```

**2. 為特定頁面的 TIFF 影像建立輸出串流**  
```java
java.io.OutputStream imageStream = new java.io.FileOutputStream("YOUR_OUTPUT_DIRECTORY/Converted_Image_Page_1.tiff");
```

**3. 重複使用相同的解析度與 TiffSettings**（設定與全部頁面範例相同）。

**4. 初始化 TiffDevice**  
```java
TiffDevice tiffDevice = new TiffDevice(resolution, tiffSettings);
```

**5. 僅轉換指定頁面**  
```java
tiffDevice.process(pdfDocument, 1, 1, imageStream); // Converts only the first page.
imageStream.close();
```
重載的 `process()` 方法允許您指定起始與結束頁面，支援 **convert pdf page tiff** 情境。

## 實務應用
- **歸檔：** 將法律或歷史 PDF 以 TIFF 形式保存，以確保長期保存。  
- **影像處理：** 提取高解析度 TIFF 供 OCR 或電腦視覺流程使用。  
- **文件分享：** 提供單頁視覺快照，確保在各平台上呈現一致。  

## 效能考量
- **記憶體管理：** 大型 PDF 可能佔用大量堆積空間。可分批處理頁面，或在需要時提升 JVM 的 `-Xmx` 參數。  
- **解析度與大小：** 較高 DPI 產生更清晰影像，但檔案較大。調整 DPI 以符合您的 **reduce tiff file size** 目標。  
- **壓縮選擇：** 對於彩色 PDF，可考慮使用 JPEG2000 壓縮取代 CCITT4，以維持檔案大小在可接受範圍。  

## 常見問題與除錯
- **出現空白頁面：** 確認已設定 `tiffSettings.setSkipBlankPages(true)`，或檢查來源 PDF 是否真的在該頁面有內容。  
- **記憶體不足錯誤：** 將 PDF 拆分為較小區段，或在轉換前使用 `Document.optimizeResources()`。  
- **顏色異常：** 若需灰階 TIFF，請設定 `tiffSettings.setDepth(ColorDepth.Format8bpp)` 並選擇適當的 `CompressionType`。  

## 常見問答

**Q: CCITT4 與其他壓縮類型有何差異？**  
A: CCITT4 為黑白影像最佳化，可在不犧牲文字清晰度的情況下產生較小檔案——非常適合掃描文件。

**Q: 我能將含混合內容（文字 + 圖片）的 PDF 轉換為 TIFF 嗎？**  
A: 可以，Aspose.PDF 能處理文字與影像層，保持視覺忠實度。

**Q: 如何在不耗盡記憶體的情況下處理非常大的 PDF？**  
A: 可將文件分頁範圍處理、提升 JVM 堆積 (`-Xmx`) 或呼叫 `Document.optimizeResources()` 以減少記憶體佔用。

**Q: 能否轉換頁面範圍而非單一頁面？**  
A: 當然可以。使用 `tiffDevice.process(pdfDocument, startPage, endPage, imageStream);`，其中 `startPage` 與 `endPage` 定義範圍。

**Q: 輸出的 TIFF 太大—我該怎麼辦？**  
A: 降低 DPI、改用更高壓縮率的方式（例如彩色使用 JPEG2000），或降低色彩深度。

## 資源
- [Aspose.PDF 文件說明](https://reference.aspose.com/pdf/java/)
- [下載 Aspose.PDF for Java](https://releases.aspose.com/pdf/java/)
- [購買授權](https://purchase.aspose.com/buy)
- [免費試用版](https://releases.aspose.com/pdf/java/)
- [臨時授權申請](https://purchase.aspose.com/temporary-license/)
- [Aspose 支援論壇](https://forum.aspose.com/c/pdf/10)

依照本教學操作後，您應已具備使用 Aspose.PDF for Java 有效 **export PDF as TIFF** 的能力。祝開發順利！

---

**最後更新：** 2026-04-21  
**測試環境：** Aspose.PDF 25.3 for Java  
**作者：** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}