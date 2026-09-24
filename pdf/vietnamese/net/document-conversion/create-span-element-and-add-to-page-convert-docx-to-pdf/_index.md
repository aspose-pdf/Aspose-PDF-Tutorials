---
category: general
date: 2026-03-27
description: Create span element in C# and learn how to add span to a page while converting
  DOCX to PDF and saving as PDF. Step‑by‑step guide for developers.
draft: false
keywords:
- create span element
- how to add span
- convert docx to pdf
- add element to page
- save as pdf
language: vi
og_description: Tạo phần tử span trong C# và học cách thêm span vào trang khi chuyển
  DOCX sang PDF, sau đó lưu dưới dạng PDF. Bao gồm ví dụ mã đầy đủ.
og_title: Tạo phần tử span và thêm vào trang – Chuyển DOCX sang PDF
tags:
- C#
- DocumentProcessing
- PDFConversion
title: Tạo phần tử span và thêm vào trang – Chuyển DOCX sang PDF
url: /vi/net/document-conversion/create-span-element-and-add-to-page-convert-docx-to-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo phần tử span và thêm vào trang – Chuyển DOCX sang PDF

Tạo **phần tử span** trong một tệp DOCX là một nhiệm vụ phổ biến khi bạn cần kiểm soát bố cục chính xác. Trong hướng dẫn này, chúng tôi sẽ chỉ cho bạn **cách thêm span** vào một trang, **chuyển DOCX sang PDF**, và **lưu dưới dạng PDF**—tất cả trong vài bước gọn gàng.  

Nếu bạn từng nhìn chằm chằm vào một tài liệu Word và nghĩ, “Giá như tôi có thể thả một hộp văn bản nhỏ tại một tọa độ chính xác,” thì bạn đang ở đúng nơi. Chúng tôi sẽ hướng dẫn toàn bộ quy trình, từ việc tải tệp nguồn đến việc tạo ra một tệp PDF hoàn chỉnh.

## Những gì bạn sẽ đạt được

* Tải một tệp `.docx` bằng cách sử dụng lớp `Document` của thư viện tài liệu.  
* **Tạo phần tử span** với API `TaggedContent`.  
* Đặt vị trí cho span tại tọa độ X/Y chính xác trên một trang đã chọn.  
* **Thêm phần tử vào trang** một cách đáng tin cậy, ngay cả khi trang không phải là trang đầu tiên.  
* **Chuyển DOCX sang PDF** và **lưu dưới dạng PDF** bằng một lời gọi `Save` duy nhất.

Không cần công cụ bên ngoài, không có cài đặt bí ẩn—chỉ là mã C# thuần túy mà bạn có thể sao chép‑dán vào dự án của mình.

## Yêu cầu trước

* .NET 6+ (hoặc bất kỳ runtime .NET gần đây nào mà thư viện của bạn hỗ trợ).  
* SDK xử lý tài liệu cung cấp `Document`, `TaggedContent`, `Position`, v.v.  
* Hiểu biết cơ bản về cú pháp C#—nếu bạn có thể viết một `Console.WriteLine`, bạn đã sẵn sàng.

> **Mẹo chuyên nghiệp:** Giữ phiên bản SDK của bạn luôn cập nhật; bản phát hành mới nhất (v3.2 tính đến tháng 3 2026) bao gồm các cải tiến hiệu năng cho các thao tác ở mức trang.

---

![Sơ đồ minh họa cách tạo phần tử span và đặt nó trên một trang PDF](https://example.com/images/create-span-element.png "Create span element placement diagram")

## Tạo phần tử span – Đặt vị trí và Thêm vào Trang

Dưới đây là đoạn mã đầy đủ, có thể chạy được, thực hiện mọi thứ từ việc tải DOCX nguồn đến việc ghi PDF cuối cùng. Bạn có thể sao chép nó vào một ứng dụng console, điều chỉnh các đường dẫn và chạy nó.

```csharp
using DocumentProcessing;   // Replace with the actual namespace of your SDK
using DocumentProcessing.Models;

class Program
{
    static void Main()
    {
        // Step 1: Load the DOCX you want to modify
        // -------------------------------------------------
        // The constructor takes a file path; make sure the file exists.
        Document doc = new Document(@"C:\Docs\input.docx");

        // Step 2: Create a new span element using the TaggedContent API
        // -------------------------------------------------
        // A span is a lightweight container for inline content.
        var span = doc.TaggedContent.CreateSpanElement();
        // Optional: add some text inside the span
        span.Text = "Hello, world!";

        // Step 3: Position the span at the desired coordinates (X = 50, Y = 750)
        // -------------------------------------------------
        // Position uses points (1/72 inch). Adjust as needed.
        span.Position = new Position(50, 750);

        // Step 4: Add the span to the target page (page index 1 = second page)
        // -------------------------------------------------
        // Pages are zero‑based; index 1 means the second page in the document.
        doc.Pages[1].Add(span);

        // Step 5: Convert the modified DOCX to PDF and save the result
        // -------------------------------------------------
        // The Save method automatically detects the output format from the extension.
        doc.Save(@"C:\Docs\output.pdf");

        // Confirmation output
        Console.WriteLine("Span added, document converted, and PDF saved successfully.");
    }
}
```

### Giải thích từng bước

#### Bước 1 – Tải tài liệu DOCX  
Chúng tôi tạo một đối tượng `Document` trỏ tới `input.docx`. Đối tượng này đại diện cho toàn bộ tệp Word trong bộ nhớ, cho phép chúng ta truy cập các trang, nội dung và siêu dữ liệu.  

#### Bước 2 – Tạo một phần tử span  
Lệnh `TaggedContent.CreateSpanElement()` trả về một container nội tuyến nhẹ. Hãy nghĩ nó như một hộp nhỏ, vô hình có thể chứa văn bản, hình ảnh hoặc các phần tử nội tuyến khác. Thêm văn bản (`span.Text`) là tùy chọn nhưng hữu ích cho việc gỡ lỗi.

#### Bước 3 – Đặt vị trí cho span  
`new Position(50, 750)` đặt góc trên‑trái của span cách lề trái 50 pt và cách trên trang 750 pt. Các giá trị này là tuyệt đối, vì vậy bạn có thể đặt span ở bất kỳ đâu—lý tưởng cho bố cục chính xác.

#### Bước 4 – Thêm span vào trang mục tiêu  
`doc.Pages[1].Add(span)` chèn span vào trang thứ hai. API sử dụng chỉ mục bắt đầu từ 0, vì vậy trang 0 là trang đầu tiên. Nếu bạn cần thêm vào trang đầu, chỉ cần dùng `doc.Pages[0]`.

#### Bước 5 – Chuyển DOCX sang PDF và lưu dưới dạng PDF  
Gọi `doc.Save("output.pdf")` thực hiện hai việc: ghi tài liệu đã chỉnh sửa lên đĩa **và** chuyển nội dung sang PDF nhờ phần mở rộng `.pdf`. Không cần bước chuyển đổi thêm—đây là cách dễ nhất để **lưu dưới dạng PDF**.

---

## Cách thêm span vào một trang khác (nâng cao)

Đôi khi bạn không biết chỉ mục trang trước. Bạn có thể xác định một trang bằng số của nó (dễ hiểu) hoặc bằng cách tìm kiếm một từ khóa cụ thể.

```csharp
// Find the page that contains the word "Summary"
int targetIndex = doc.Pages
    .Select((p, i) => new { Page = p, Index = i })
    .FirstOrDefault(x => x.Page.Text.Contains("Summary"))?.Index ?? 0;

// Fallback to first page if not found
targetIndex = Math.Max(targetIndex, 0);

// Add the span to the discovered page
doc.Pages[targetIndex].Add(span);
```

**Tại sao điều này quan trọng:** Trong các báo cáo mà số trang thay đổi, việc mã cứng `Pages[1]` có thể làm hỏng bố cục. Đoạn mã này cho thấy một mẫu mạnh mẽ cho **cách thêm span** một cách động.

---

## Những khó khăn thường gặp và cách tránh chúng

| Vấn đề | Điều gì xảy ra | Cách khắc phục |
|-------|----------------|----------------|
| **Span không hiển thị** | Tọa độ nằm ngoài trang hoặc span có chiều rộng/chiều cao bằng 0. | Kiểm tra lại các giá trị `Position`; sử dụng thước đo trong trình xem PDF của bạn. |
| **Chỉ mục trang sai** | Bạn thêm vào trang 0 nhưng mong đợi nó ở trang 2. | Nhớ rằng API bắt đầu từ 0; cộng 1 vào số trang dành cho người dùng. |
| **Lưu đè lên nguồn** | `doc.Save("input.docx")` thay thế tệp gốc. | Luôn lưu vào một đường dẫn mới (`output.pdf`) khi chuyển đổi. |
| **Thiếu tham chiếu SDK** | Lỗi biên dịch trên lớp `Document`. | Cài đặt gói NuGet: `dotnet add package DocumentProcessing.SDK`. |

## Xác minh kết quả

Sau khi chạy chương trình, mở `output.pdf` trong bất kỳ trình xem PDF nào. Bạn sẽ thấy văn bản “Hello, world!” được đặt chính xác tại (50, 750) trên trang thứ hai. Nếu văn bản xuất hiện ở vị trí khác, hãy điều chỉnh các giá trị `Position` và chạy lại.  

Đối với kiểm thử tự động, bạn có thể sử dụng một trình phân tích PDF (ví dụ, iTextSharp) để xác nhận tọa độ của văn bản một cách lập trình.

```csharp
// Example using iTextSharp to verify position (pseudo‑code)
var pdfReader = new PdfReader(@"C:\Docs\output.pdf");
var page = pdfReader.GetPageContent(2);
Debug.Assert(page.Contains("Hello, world!"));
```

---

## Các bước tiếp theo

* **Định dạng span** – khám phá các thuộc tính `span.Font`, `span.Color`, và các thuộc tính định dạng khác.  
* **Thêm hình ảnh** – sử dụng `CreateImageElement()` thay vì span cho đồ họa.  
* **Xử lý hàng loạt** – lặp qua một thư mục các tệp DOCX

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}