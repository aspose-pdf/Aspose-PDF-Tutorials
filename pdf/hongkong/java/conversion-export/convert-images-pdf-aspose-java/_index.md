---
date: '2026-01-06'
description: 學習如何使用 Aspose.PDF for Java 高效將圖像轉換為 PDF，包括 Aspose PDF Maven 依賴設定。非常適合存檔相片或製作報告。
keywords:
- convert images to PDF
- Aspose.PDF for Java
- image-to-PDF conversion
title: 使用 Aspose.PDF for Java 將圖片轉換為 PDF 的完整指南
url: /zh-hant/java/conversion-export/convert-images-pdf-aspose-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}
# 如何使用 Aspose.PDF for Java 將圖像轉換為 PDF

在許多應用程式中，將圖像轉換為 PDF 文件是必不可少的，**本教學將向您完整示範如何使用 Aspose.PDF for Java 將圖像轉換為 PDF**。無論您是要歸檔家庭相片、產生報告，或是數位化收據，以下步驟都能提供快速且可靠的方式，將任何圖像檔案轉換為專業外觀的 PDF。

## 快速解答
- **需要哪個函式庫？** Aspose.PDF for Java（加入 aspose pdf Maven 依賴）。  
- **可以轉換 TIFF 檔案嗎？** 可以 — 相同程式碼適用於 TIFF、JPEG、PNG、GIF 等格式。  
- **需要授權嗎？** 免費試用版可用於評估；正式環境需購買永久授權。  
- **頁面邊距如何處理？** 您可以程式化設定（請參考 “java pdf page margins”）。  
- **建議使用緩衝串流嗎？** 建議 — 可減少大型圖像的記憶體使用量。

## 什麼是「將圖像轉換為 PDF」？
將圖像轉換為 PDF 指的是將一或多個點陣圖檔（例如 JPG、PNG 或 TIFF）嵌入 PDF 容器中，使其能在各平台上保持一致地檢視、分享與列印。

## 為何使用 Aspose.PDF for Java？
- **功能完整的 API** — 支援所有主要圖像格式，無需額外外掛。  
- **無外部相依性** — 僅使用 Aspose JAR 即可直接使用。  
- **細緻的控制** — 您可調整頁面尺寸、邊距、壓縮等設定。

## 前置條件

在開始之前，請確保您已具備以下條件：

### 新增 Aspose PDF Maven 依賴
若要使用 Aspose.PDF for Java，請在建置檔案中加入此函式庫。

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

### 環境設定
確保您已安裝 Java 8 或以上版本，並使用如 IntelliJ IDEA 或 Eclipse 等 IDE。

### 取得授權
若要使用 Aspose.PDF for Java：

- 考慮取得 **免費試用** 以探索函式庫的功能。  
- 若需求超過免費試用範圍，請取得 **臨時授權**。  
- 為長期專案購買 **完整授權**。

前往 [Aspose's Purchase Page](https://purchase.aspose.com/buy) 了解取得授權的詳細資訊。您亦可從 [here](https://purchase.aspose.com/temporary-license/) 取得臨時授權。

## 設定 Aspose.PDF for Java

在加入相依性後，於專案中初始化 Aspose.PDF。

1. **將 Maven 或 Gradle 依賴** 加入您的 `pom.xml` 或 `build.gradle`。  
2. **在 Java 檔案中匯入 Aspose.PDF 類別**。  
3. 如需授權，請使用以下程式碼套用：```java
com.aspose.pdf.License license = new com.aspose.pdf.License();
license.setLicense("path/to/your/license/file");
```

## 實作指南

本指南分為兩個主要功能：使用直接檔案串流將圖像轉換為 PDF，以及從 `BufferedImage` 新增圖像至 PDF。

### 使用直接檔案串流將圖像轉換為 PDF

#### 步驟 1：建立 Document 物件
```java
doc = new Document();
```
建立一個 `Document` 物件，作為 PDF 檔案的容器。

#### 步驟 2：向 Document 新增頁面
```java
page = doc.getPages().add();
```
向文件新增一個頁面，圖像將放置於此。

#### 步驟 3：載入圖像檔案
```java
FileInputStream fs = new FileInputStream("YOUR_DOCUMENT_DIRECTORY/source.tif");
```
將來源圖像檔載入 `FileInputStream`。將 "YOUR_DOCUMENT_DIRECTORY/source.tif" 替換為實際的圖像路徑。

#### 步驟 4：設定頁面邊距與裁切框
```java
page.getPageInfo().getMargin().setBottom(0);
page.getPageInfo().getMargin().setTop(0);
page.getPageInfo().getMargin().setLeft(0);
page.getPageInfo().getMargin().setRight(0);
page.setCropBox(new Rectangle(0, 0, 400, 400));
```
調整邊距與裁切框，以確保圖像在頁面內適當顯示。

#### 步驟 5：建立並新增 Image 物件
```java
Image image1 = new Image();
page.getParagraphs().add(image1);
image1.setImageStream(fs);
```
建立 `Image` 物件，將其加入頁面的段落集合，並以檔案輸入串流設定其來源。

#### 步驟 6：儲存 PDF 文件
```java
doc.save("YOUR_OUTPUT_DIRECTORY/Image2PDF_DOM.pdf");
```
將文件儲存至指定位置。將 "YOUR_OUTPUT_DIRECTORY/Image2PDF_DOM.pdf" 替換為您的輸出路徑。

### 從 BufferedImage 新增圖像至 PDF

#### 步驟 1：建立 Document 並新增頁面
```java
doc = new Document();
page = doc.getPages().add();
```
首先建立文件並新增頁面，與前述功能相同。

#### 步驟 2：從圖像檔建立 BufferedImage
```java
Image image1 = new Image();
java.awt.image.BufferedImage bufferedImage = ImageIO.read(new File("YOUR_DOCUMENT_DIRECTORY/source.gif"));
ByteArrayOutputStream baos = new ByteArrayOutputStream();

// Write the BufferedImage as GIF
ImageIO.write(bufferedImage, "gif", baos);
baos.flush();
ByteArrayInputStream bais = new ByteArrayInputStream(baos.toByteArray());
```
將圖像檔轉換為 `BufferedImage`，再寫入 `ByteArrayOutputStream`。此串流將用於將圖像加入 PDF。

#### 步驟 3：將圖像加入頁面並設定串流
```java
page.getParagraphs().add(image1);
image1.setImageStream(bais);
```
將圖像物件加入頁面的段落集合，並使用 `ByteArrayInputStream` 設定其串流。

#### 步驟 4：儲存 PDF 文件
```java
doc.save("YOUR_OUTPUT_DIRECTORY/BufferedImage.pdf");
```
儲存文件，請確認指定正確的輸出目錄。

## 實務應用

- **照片歸檔：** 將數位相片合併為 PDF，便於分享與儲存。  
- **文件製作：** 以嵌入圖像的方式製作報告或簡報。  
- **收據管理：** 將紙本收據轉換為 PDF，以進行電子歸檔。

這些方法可整合至文件管理平台或雲端儲存服務，以提升工作流程自動化。

## 效能考量

在使用 Aspose.PDF for Java 時：

- 在轉換前最佳化圖像解析度與大小，以控制記憶體使用量。  
- 使用緩衝串流有效處理大型檔案，減少 I/O 操作。  
- 遵循 Java 記憶體管理最佳實踐，例如使用後關閉串流，以防止記憶體洩漏。

## 常見問題與解決方案

| 問題 | 原因 | 解決方案 |
|------|------|----------|
| **OutOfMemoryError** | 未使用緩衝直接載入極大圖像 | 使用 `FileInputStream` 或搭配串流的 `BufferedImage`，並及時關閉。 |
| **圖像未顯示** | 圖像路徑不正確或格式不支援 | 確認檔案路徑，並確保格式（JPEG、PNG、GIF、TIFF）受支援。 |
| **邊距顯示不正確** | 未覆寫預設邊距 | 如程式碼所示，明確將四個邊距設定為 `0`（或其他所需值）。 |

## 常見問答

**Q: 可以在同一個 PDF 中轉換不同格式的圖像嗎？**  
A: 可以 — 只需在連續的頁面上加入多個 `Image` 物件，分別指向不同格式的圖像。

**Q: 如何在不耗盡記憶體的情況下處理大型 TIFF 檔案？**  
A: 使用直接檔案串流方式（第一個功能的第 3 步），並在儲存後關閉 `FileInputStream`。

**Q: 正式環境是否需要授權？**  
A: 正式環境必須使用有效的 Aspose.PDF 授權；免費試用僅適用於評估。

**Q: 能否設定自訂頁面尺寸（A4、Letter 等）？**  
A: 可以 — 在加入圖像前，先以自訂 `Rectangle` 大小建立 `Page`。

**Q: Aspose.PDF 是否支援受密碼保護的 PDF？**  
A: 此函式庫可開啟與儲存加密的 PDF，但圖像插入僅在未加密的頁面上可用。

## 資源
- [Aspose.PDF 文件](https://reference.aspose.com/pdf/java/)
- [下載 Aspose.PDF for Java](https://releases.aspose.com/pdf/java/)
- [購買授權](https://purchase.aspose.com/buy)
- [免費試用](https://releases.aspose.com/pdf/java/)
- [臨時授權](https://purchase.aspose.com/temporary-license/)
- [Aspose 支援論壇](https://forum.aspose.com/c/pdf/10)

準備好試試看了嗎？立即在您的專案中實作此解決方案，簡化圖像轉 PDF 的工作流程！

---

**最後更新：** 2026-01-06  
**測試環境：** Aspose.PDF for Java 25.3  
**作者：** Aspose

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
