---
date: '2026-05-28'
description: Tìm hiểu cách thiết lập PDF xem trang đơn, thay đổi tùy chọn trình xem,
  chỉnh sửa dấu trang và cấu hình cài đặt PDF bằng Aspose.PDF for Java.
keywords:
- single page view pdf
- aspose pdf maven dependency
- change pdf viewer preference
- configure pdf viewer settings
- set pdf bookmark destination
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: Learn how to set single page view PDF, change viewer preferences, edit
    bookmarks, and configure PDF settings using Aspose.PDF for Java.
  headline: Single Page View PDF in Java – Change Layout & Edit Bookmarks
  type: TechArticle
- description: Learn how to set single page view PDF, change viewer preferences, edit
    bookmarks, and configure PDF settings using Aspose.PDF for Java.
  name: Single Page View PDF in Java – Change Layout & Edit Bookmarks
  steps:
  - name: '**Digital Books** – Ensure each chapter bookmark lands at the top of the
      page for a seamless reading experience.'
    text: '**Digital Books** – Ensure each chapter bookmark lands at the top of the
      page for a seamless reading experience.'
  - name: '**Technical Manuals** – Precise navigation helps engineers find sections
      quickly, especially in large PDFs.'
    text: '**Technical Manuals** – Precise navigation helps engineers find sections
      quickly, especially in large PDFs.'
  - name: '**Product Catalogs** – Single‑page layout makes browsing catalogs on tablets
      more intuitive.'
    text: '**Product Catalogs** – Single‑page layout makes browsing catalogs on tablets
      more intuitive.'
  type: HowTo
- questions:
  - answer: Use `new Document("path/to/file.pdf")`; Aspose.PDF automatically detects
      the file format.
    question: What is the easiest way to load a PDF document in Java?
  - answer: Yes, you can set viewer preferences directly on the `Document` object
      via `pdfDocument.getViewerPreferences().setPageLayout(...)`.
    question: Can I change the page layout without using PdfContentEditor?
  - answer: Viewer layout only influences on‑screen display; it does not alter the
      printed output.
    question: Does changing the viewer layout affect printing?
  - answer: No explicit limit, but extremely large outline trees may impact performance;
      keep them organized.
    question: Are there limits on the number of bookmarks I can create?
  - answer: Re‑calculate destinations using the current page indices after any structural
      changes.
    question: How do I ensure bookmark destinations are accurate after adding or removing
      pages?
  type: FAQPage
title: Xem PDF Trang Đơn trong Java – Thay đổi Bố cục & Chỉnh sửa Dấu trang
url: /vi/java/bookmarks-navigation/edit-pdf-bookmarks-viewer-settings-aspose-pdf-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/products-backtop-button >}}
# Xem Trang Đơn PDF trong Java – Thay Đổi Bố Cục & Chỉnh Sửa Dấu Trang

## Giới thiệu
Khi người đọc mở một tệp PDF lớn, bố cục trình xem mặc định có thể cuộn liên tục, khiến khó tập trung vào một trang duy nhất. Bằng cách cấu hình cài đặt **single page view pdf**, bạn buộc trình xem hiển thị một trang mỗi lần, rất phù hợp cho báo cáo, e‑books và catalog. Trong hướng dẫn này, bạn cũng sẽ học cách chỉnh sửa dấu trang PDF hiện có, đặt đích cho dấu trang khi tạo tài liệu, và tinh chỉnh các tùy chọn trình xem khác bằng Aspose.PDF for Java. Khi hoàn thành, bạn sẽ có toàn quyền kiểm soát việc điều hướng, độ chính xác của dấu trang và bố cục trên màn hình.

**Bạn sẽ học**
- Cách chỉnh sửa dấu trang PDF hiện có để chúng trỏ tới đầu trang.  
- Cách đặt đích cho dấu trang khi tạo PDF.  
- Cách thay đổi tùy chọn trình xem như bố cục trang đơn.  
- Mẹo thực tế để tải tài liệu PDF trong Java và tối ưu hiệu suất.

### Câu trả lời nhanh
- **Cách chính để bật chế độ xem trang đơn PDF là gì?** Call `PdfContentEditor.changeViewerPreference()` with `ViewerPreference.PAGE_LAYOUT_SINGLE_PAGE`.  
- **Có thể chỉnh sửa đích của dấu trang sau khi PDF đã được tạo không?** Yes – load the document, retrieve the outline, and assign a new `ExplicitDestination`.  
- **Tôi có cần giấy phép cho các tính năng này không?** A free trial works for evaluation; a full license removes all limitations.  
- **Phụ thuộc Maven nào được yêu cầu?** `com.aspose:aspose-pdf:25.3` (or later).  
- **Điều này có tương thích với Java 11 trở lên không?** Absolutely – Aspose.PDF supports Java 8+.

## “Thay đổi bố cục trang PDF” là gì?
Thay đổi bố cục trang PDF kiểm soát cách các trang được hiển thị trong trình xem—trang đơn, liên tục, xem hai trang, v.v. Kích hoạt **single page view pdf** cải thiện khả năng đọc cho tài liệu dài và đảm bảo mỗi trang được trình bày riêng biệt, đặc biệt hữu ích trên thiết bị di động và máy tính bảng.

## Tại sao cần chỉnh sửa dấu trang PDF và đặt đích cho dấu trang?
Dấu trang hoạt động như mục lục động. Đích chính xác cho phép người đọc nhảy thẳng tới phần mong muốn, loại bỏ việc cuộn thêm và giảm sự bực bội. Điều này mang lại trải nghiệm điều hướng mượt mà hơn và sự hài lòng cao hơn cho các sổ tay kỹ thuật, catalog sản phẩm và sách điện tử.

## Yêu cầu trước
- **Thư viện & Phụ thuộc**: Aspose.PDF for Java v25.3 hoặc mới hơn.  
- **Môi trường**: JDK 8 hoặc mới hơn, công cụ xây dựng Maven hoặc Gradle.  
- **Kiến thức**: Lập trình Java cơ bản và hiểu biết về các khái niệm PDF.

## Cài đặt Aspose.PDF cho Java
### Cài đặt Maven
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-pdf</artifactId>
    <version>25.3</version>
</dependency>
```
### Cài đặt Gradle
```gradle
implementation 'com.aspose:aspose-pdf:25.3'
```
**Mua giấy phép**: Start with a free trial or request a temporary license for full‑feature access. Consider purchasing a permanent license for production use.

### Khởi tạo Cơ bản
The `Document` class is Aspose.PDF's core object that represents a PDF file in memory. After creating an instance, all read/write operations flow through this object.  
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

## Hướng dẫn triển khai
### Cách Thay đổi Bố cục Trang PDF trong Java
**Overview**: Adjust viewer preferences to display pages the way you want.

#### Khởi tạo PdfContentEditor
`PdfContentEditor` is a utility class that lets you modify viewer settings without rewriting the whole document.  
```java
import com.aspose.pdf.facades.PdfContentEditor;
import com.aspose.pdf.facades.ViewerPreference;

PdfContentEditor editor = new PdfContentEditor();
editor.bindPdf("YOUR_DOCUMENT_DIRECTORY/input.pdf");
```
#### Thay đổi Tùy chọn Trình xem
To enable **single page view pdf**, invoke `changeViewerPreference()` with the appropriate enum value. This call updates the PDF’s internal viewer preference dictionary.  
```java
editor.changeViewerPreference(ViewerPreference.PAGE_LAYOUT_SINGLE_PAGE);
```
#### Lưu Tài liệu Đã Cập nhật
After modifying preferences, call `save()` to write the changes back to disk.  
```java
String outputDir = "YOUR_OUTPUT_DIRECTORY/settingViewerPreferences.pdf";
editor.save(outputDir);
```

## Cách Chỉnh sửa Dấu trang PDF
**Answer**: To modify existing bookmarks, load the PDF with `Document`, retrieve its outline collection, locate the desired `OutlineItem`, and assign a new `ExplicitDestination` that points to the correct page and coordinates. After updating each bookmark, save the document to persist changes. This ensures users are directed precisely to the intended sections without extra scrolling.

#### Truy cập Dấu trang
The `OutlineItemCollection` represents the hierarchical bookmark tree. Retrieve it from the `Document` object to work with individual entries.  
```java
import com.aspose.pdf.Document;
import com.aspose.pdf.ExplicitDestination;
import com.aspose.pdf.OutlineItemCollection;

Document pdfDocument = new Document("YOUR_DOCUMENT_DIRECTORY/input.pdf");
OutlineItemCollection pdfOutline = pdfDocument.getOutlines().get_Item(1);
```
#### Đặt Đích Mới
An `ExplicitDestination` defines the exact page and location a bookmark should jump to. Assign it to the `Destination` property of the outline item.  
```java
pdfOutline.setDestination(
    ExplicitDestination.createDestination(pdfDocument.getPages().get_Item(1),
        ExplicitDestinationType.FitH,
        pdfDocument.getPages().get_Item(1).getMediaBox().getHeight())
);
```
#### Lưu Thay đổi
Persist the updated bookmark tree by calling `document.save()`.  
```java
String outputDir = "YOUR_OUTPUT_DIRECTORY/bookmarkShouldPointToStartOfPage.pdf";
pdfDocument.save(outputDir);
```

## Cách Đặt Đích Dấu trang Khi Tạo PDF
**Answer**: When generating a PDF, you can create bookmarks on the fly by instantiating `OutlineItem` objects, setting their titles, and defining an `ExplicitDestination` that targets a specific page and view mode. Add each bookmark to the document’s outline collection before saving, so the resulting file contains a ready‑to‑use navigation tree.

#### Tạo và Cấu hình Dấu trang
`OutlineItem` represents a single bookmark entry in the PDF outline. When building a PDF from scratch, instantiate a new `OutlineItem` and add it to the document’s outline collection.  
```java
import com.aspose.pdf.GoToAction;
import com.aspose.pdf.FitVExplicitDestination;

OutlineItemCollection pdfOutline_new = new OutlineItemCollection(pdfDocument.getOutlines());
pdfOutline_new.setTitle("Test Bookmark");
pdfOutline_new.setItalic(true);
pdfOutline_new.setBold(true);
```
#### Định nghĩa Đích Dấu trang
Use `ExplicitDestination.createFitH(page, top)` to position the view at the top of the target page.  
```java
pdfOutline_new.setAction(new GoToAction(
    new FitVExplicitDestination(pdfDocument.getPages().get_Item(2), 0)));
```
#### Thêm và Lưu PDF
Finally, add the bookmark to the outline and save the document.  
```java
pdfDocument.getOutlines().add(pdfOutline_new);

String outputDir = "YOUR_OUTPUT_DIRECTORY/setDestinationWhileCreatingPDF.pdf";
pdfDocument.save(outputDir);
```

## Ứng dụng Thực tiễn
1. **Sách điện tử** – Đảm bảo mỗi dấu trang chương đưa tới đầu trang để trải nghiệm đọc liền mạch.  
2. **Sổ tay kỹ thuật** – Điều hướng chính xác giúp kỹ sư tìm phần nhanh chóng, đặc biệt trong các PDF lớn.  
3. **Catalog sản phẩm** – Bố cục trang đơn giúp duyệt catalog trên máy tính bảng trở nên trực quan hơn.

## Các cân nhắc về Hiệu suất
- **Optimizing Resources**: Aspose.PDF can process PDFs up to 2 GB without loading the entire file into memory, thanks to its streaming architecture. Use `Document.optimizeResources()` to further reduce memory footprint.  
- **Java Memory Management**: Explicitly close streams and let the garbage collector reclaim objects after processing to avoid memory leaks.

## Các vấn đề thường gặp & Giải pháp
- **Bookmarks Not Updating**: Verify you’re modifying the correct outline index (`get_Item(1)` refers to the first top‑level bookmark).  
- **Viewer Preference Not Applied**: Ensure you call `editor.save()` after changing preferences; otherwise changes remain only in memory.  
- **License Exceptions**: A trial license may add watermarks; obtain a full license for production.

## Câu hỏi thường gặp
**Q: Cách dễ nhất để tải tài liệu PDF trong Java là gì?**  
A: Use `new Document("path/to/file.pdf")`; Aspose.PDF automatically detects the file format.

**Q: Có thể thay đổi bố cục trang mà không dùng PdfContentEditor không?**  
A: Yes, you can set viewer preferences directly on the `Document` object via `pdfDocument.getViewerPreferences().setPageLayout(...)`.

**Q: Thay đổi bố cục trình xem có ảnh hưởng đến việc in không?**  
A: Viewer layout only influences on‑screen display; it does not alter the printed output.

**Q: Có giới hạn số lượng dấu trang tôi có thể tạo không?**  
A: No explicit limit, but extremely large outline trees may impact performance; keep them organized.

**Q: Làm sao để đảm bảo đích dấu trang chính xác sau khi thêm hoặc xóa trang?**  
A: Re‑calculate destinations using the current page indices after any structural changes.

## Tài nguyên
- **Tài liệu**: [Aspose.PDF Java Reference](https://reference.aspose.com/pdf/java/)
- **Tải xuống**: [Latest Releases for Java](https://releases.aspose.com/pdf/java/)
- **Mua**: [Buy Aspose.PDF License](https://purchase.aspose.com/buy)
- **Dùng thử miễn phí**: [Try Aspose.PDF Free](https://releases.aspose.com/pdf/java/)
- **Giấy phép tạm thời**: [Request Temporary License](https://purchase.aspose.com/temporary-license)

---

**Cập nhật lần cuối:** 2026-05-28  
**Kiểm tra với:** Aspose.PDF for Java v25.3  
**Tác giả:** Aspose

## Hướng dẫn liên quan

- [Cách Thay đổi Tùy chọn Trình xem PDF bằng Aspose.PDF cho Java: Hướng dẫn Toàn diện](/pdf/java/printing-rendering/modify-pdf-viewer-preferences-aspose-pdf-java/)
- [Cách Tạo Dấu trang PDF và Quản lý Điều hướng bằng Aspose.PDF cho Java](/pdf/java/bookmarks-navigation/create-manage-pdf-bookmarks-aspose-java/)
- [Hướng dẫn Dấu trang PDF và Điều hướng cho Aspose.PDF Java](/pdf/java/bookmarks-navigation/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}