---
date: '2025-11-28'
description: Tìm hiểu cách sử dụng giấy phép tạm thời của Aspose PDF để tạo các tệp
  PDF có thẻ truy cập được bằng Java. Hướng dẫn từng bước, mẫu mã và các thực tiễn
  tốt nhất.
keywords:
- aspose pdf temporary license
- tagged PDFs
- accessibility with Aspose.PDF
- create structured PDFs
title: Giấy phép tạm thời Aspose PDF – PDF có thẻ trong Java
url: /vi/java/advanced-features/aspose-pdf-java-create-tagged-pdfs/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}
# Giấy phép tạm thời Aspose PDF – PDF có thẻ trong Java

## Introduction
Trong hướng dẫn này, bạn sẽ học **cách sử dụng giấy phép tạm thời Aspose PDF** để tạo các PDF có thẻ hỗ trợ truy cập với **Aspose.PDF for Java**. Việc làm cho PDF có khả năng truy cập là rất quan trọng đối với người dùng dựa vào trình đọc màn hình, và giấy phép tạm thời cho phép bạn đánh giá toàn bộ tính năng mà không tốn chi phí ban đầu. Chúng tôi sẽ hướng dẫn qua việc cài đặt, tạo cấu trúc logic, và lưu tài liệu cuối cùng, đồng thời giữ cho mã nguồn đơn giản và sẵn sàng cho môi trường sản xuất.

**What You'll Learn**
- Cách lấy và áp dụng giấy phép tạm thời Aspose PDF
- Cài đặt Aspose.PDF for Java trong Maven hoặc Gradle
- Xây dựng cấu trúc logic với tiêu đề, cài đặt ngôn ngữ, các phần và đoạn
- Lưu PDF đã được gắn thẻ đầy đủ, sẵn sàng cho các công nghệ hỗ trợ
- Các kịch bản thực tế nơi PDF có thẻ mang lại giá trị

---

## Quick Answers
- **What is an Aspose PDF temporary license?** Một giấy phép ngắn hạn, miễn phí mở khóa tất cả các tính năng của Aspose.PDF để đánh giá.  
- **Do I need a license to create tagged PDFs?** Có, cần có giấy phép tạm thời hoặc đầy đủ để kích hoạt tính năng gắn thẻ.  
- **Which Java build tools are supported?** Maven và Gradle đều được hỗ trợ đầy đủ.  
- **Can I set the document language and title?** Chắc chắn – API cung cấp các phương thức để định nghĩa cả hai cho khả năng truy cập.  
- **Is the generated PDF compliant with PDF/UA?** Cấu trúc có thẻ tuân theo các khuyến nghị của PDF/UA, cải thiện mức độ tuân thủ.

---

## What is an Aspose PDF Temporary License?
Một **giấy phép tạm thời Aspose PDF** là một khóa có thời hạn cho phép bạn truy cập vào toàn bộ chức năng của Aspose.PDF for Java, bao gồm các tính năng truy cập nâng cao như gắn thẻ, cài đặt ngôn ngữ và thao tác cấu trúc logic. Đây là lựa chọn hoàn hảo để thử nghiệm, thực hiện proof‑of‑concept, hoặc đánh giá thư viện trước khi mua giấy phép vĩnh viễn.

## Why Use a Temporary License for Tagged PDFs?
- **Zero cost evaluation:** Thử nghiệm tính năng gắn thẻ, cấu trúc và tuân thủ mà không phải trả phí.
- **Full feature set:** Không có hạn chế tính năng – bạn nhận được cùng một API như giấy phép trả phí.
- **Fast onboarding:** Tích hợp nhanh thư viện, tạo PDF hỗ trợ truy cập, và chứng minh giá trị cho các bên liên quan.
- **Compliance testing:** Xác minh PDF của bạn đáp ứng tiêu chuẩn PDF/UA hoặc WCAG trước khi quyết định mua giấy phép.

## Prerequisites
Trước khi bắt đầu, hãy chắc chắn bạn đã có:

- **Java Development Kit (JDK):** Phiên bản 8 trở lên đã được cài đặt.
- **Aspose.PDF for Java Library:** Sử dụng phiên bản 25.3 hoặc mới hơn (giấy phép tạm thời hoạt động với bất kỳ phiên bản gần đây nào).
- **Maven hoặc Gradle:** Để quản lý phụ thuộc.
- **A temporary license file:** Lấy từ trang giấy phép của Aspose (xem liên kết bên dưới).

### Required Libraries and Dependencies
Thêm Aspose.PDF vào dự án của bạn bằng một trong các công cụ xây dựng sau.

#### Maven
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-pdf</artifactId>
    <version>25.3</version>
</dependency>
```

#### Gradle
```gradle
implementation 'com.aspose:aspose-pdf:25.3'
```

### License Acquisition
Lấy **giấy phép tạm thời** để dùng thử miễn phí hoặc mua giấy phép đầy đủ để mở khóa tất cả các tính năng. Truy cập [trang giấy phép của Aspose](https://purchase.aspose.com/temporary-license/) để biết thêm chi tiết.

## Setting Up Aspose.PDF for Java
Thêm phụ thuộc vào công cụ quản lý dự án (Maven/Gradle). Sau đó, khởi tạo thư viện:

```java
import com.aspose.pdf.Document;

public class SetupAspose {
    public static void main(String[] args) {
        // Initialize the Document object
        Document document = new Document();
        System.out.println("Aspose.PDF Initialized Successfully!");
    }
}
```

## Implementation Guide

### Create and Configure a Tagged PDF Document
**Overview:** Bắt đầu bằng việc tạo một PDF có nội dung được gắn thẻ để đảm bảo khả năng truy cập.

#### Step 1: Import Necessary Packages
```java
import com.aspose.pdf.Document;
import com.aspose.pdf.tagged.ITaggedContent;
```

#### Step 2: Set Up the Document Directory
Xác định thư mục tài liệu nơi bạn sẽ lưu các tệp đầu ra.

```java
String dataDir = "YOUR_DOCUMENT_DIRECTORY";
Document document = new Document();
ITaggedContent taggedContent = document.getTaggedContent();

// Configure title and language for accessibility
taggedContent.setTitle("Tagged Pdf Document");
taggedContent.setLanguage("en-US");
```
- **Why:** Đặt tiêu đề và ngôn ngữ giúp trình đọc màn hình có thể diễn giải tài liệu của bạn một cách chính xác.

### Construct a Logical Structure of Sections and Divisions
**Overview:** Tổ chức nội dung một cách logic trong các phần và đoạn để cải thiện khả năng điều hướng.

#### Step 1: Import Logical Structure Elements
```java
import com.aspose.pdf.tagged.logicalstructure.elements.StructureElement;
import com.aspose.pdf.tagged.logicalstructure.elements.grouping.DivElement;
import com.aspose.pdf.tagged.logicalstructure.elements.grouping.SectElement;
```

#### Step 2: Build the Document Structure
Tạo các phần và đoạn trong PDF của bạn.

```java
String outputDir = "YOUR_OUTPUT_DIRECTORY";
StructureElement rootElement = taggedContent.getRootElement();

// Create sections
SectElement sect1 = taggedContent.createSectElement();
rootElement.appendChild(sect1);

SectElement sect2 = taggedContent.createSectElement();
rootElement.appendChild(sect2);

// Add divisions to sections
DivElement div11 = taggedContent.createDivElement();
sect1.appendChild(div11);
DivElement div12 = taggedContent.createDivElement();
sect1.appendChild(div12);

ArtElement art21 = taggedContent.createArtElement();
sect2.appendChild(art21);
ArtElement art22 = taggedContent.createArtElement();
sect2.appendChild(art22);

// Further divide sections
DivElement div211 = taggedContent.createDivElement();
art21.appendChild(div211);
DivElement div212 = taggedContent.createDivElement();
art21.appendChild(div212);

DivElement div221 = taggedContent.createDivElement();
art22.appendChild(div221);
DivElement div222 = taggedContent.createDivElement();
art22.appendChild(div222);

// Add another section
SectElement sect3 = taggedContent.createSectElement();
rootElement.appendChild(sect3);

DivElement div31 = taggedContent.createDivElement();
sect3.appendChild(div31);
```
- **Why:** Cấu trúc logic là yếu tố then chốt cho khả năng truy cập, cho phép người dùng điều hướng nội dung một cách hiệu quả.

### Save the Tagged PDF Document
**Overview:** Hoàn thiện bằng cách lưu tài liệu đã cấu trúc vào thư mục đã chỉ định.

```java
document.save(outputDir + "/StructureElementsTree.pdf");
```

## Practical Applications
PDF có thẻ mang lại lợi ích trong nhiều kịch bản:

1. **Educational Materials:** Nâng cao khả năng truy cập cho sinh viên sử dụng công nghệ hỗ trợ.  
2. **Government Publications:** Đảm bảo tuân thủ các tiêu chuẩn truy cập như PDF/UA.  
3. **Corporate Reports:** Cải thiện khả năng điều hướng và trải nghiệm người dùng cho các bên liên quan.

Việc tích hợp Aspose.PDF vào quy trình làm việc giúp đơn giản hoá quản lý tài liệu trên các trường hợp sử dụng này.

## Performance Considerations
- **Optimize Memory Usage:** Sử dụng các cấu trúc dữ liệu hiệu quả khi xử lý tài liệu lớn.  
- **Resource Management:** Giải phóng các đối tượng không dùng để giải phóng bộ nhớ.  
- **Stay Updated:** Thường xuyên nâng cấp lên phiên bản Aspose.PDF mới nhất để cải thiện hiệu năng và sửa lỗi.

## Common Issues and Solutions
| Issue | Solution |
|-------|----------|
| **License not applied** | Xác minh rằng tệp giấy phép tạm thời đã được tải đúng trước khi tạo tài liệu. |
| **Missing tags in output** | Đảm bảo bạn gọi `document.getTaggedContent()` và đặt tiêu đề/ngôn ngữ trước khi thêm các phần tử cấu trúc. |
| **Large PDFs cause OutOfMemoryError** | Sử dụng `Document.optimizeResources()` và xử lý PDF theo từng phần nếu có thể. |
| **Incorrect language code** | Sử dụng mã ISO‑639‑1 (ví dụ: `en-US`, `fr-FR`) để phù hợp với yêu cầu của trình đọc màn hình. |

## Frequently Asked Questions

**Q: What is a tagged PDF?**  
A: Một PDF có thẻ bao gồm cấu trúc ngữ nghĩa giúp trình đọc màn hình diễn giải tài liệu một cách chính xác.

**Q: Can I use Aspose.PDF with other Java frameworks?**  
A: Có, Aspose.PDF tích hợp liền mạch với các framework Java phổ biến và công cụ xây dựng như Maven và Gradle.

**Q: How do I handle large documents efficiently?**  
A: Tối ưu hoá việc sử dụng bộ nhớ bằng cách quản lý tài nguyên cẩn thận và luôn cập nhật thư viện lên phiên bản mới nhất.

**Q: What are the benefits of using Aspose.PDF for tagged PDFs?**  
A: Nó đơn giản hoá việc tạo tài liệu truy cập, đảm bảo tuân thủ các tiêu chuẩn mà không cần quản lý thẻ thủ công.

**Q: Is support available if I encounter issues?**  
A: Có, truy cập [Diễn đàn Hỗ trợ của Aspose](https://forum.aspose.com/c/pdf/10) để nhận trợ giúp từ cộng đồng và các chuyên gia Aspose.

## Resources
- **Documentation:** Khám phá các hướng dẫn chi tiết tại [Aspose PDF Java Documentation](https://reference.aspose.com/pdf/java/).  
- **Download Library:** Truy cập các bản phát hành mới nhất tại [Aspose Downloads](https://releases.aspose.com/pdf/java/).  
- **Purchase:** Mua giấy phép qua [Aspose Purchase Page](https://purchase.aspose.com/buy).  
- **Free Trial:** Bắt đầu dùng thử tại [Aspose Free Trials](https://releases.aspose.com/pdf/java/).  
- **Temporary License:** Nhận quyền truy cập tạm thời để đánh giá tại [Aspose Temporary License](https://purchase.aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

---

**Last Updated:** 2025-11-28  
**Tested With:** Aspose.PDF for Java 25.3  
**Author:** Aspose  

---