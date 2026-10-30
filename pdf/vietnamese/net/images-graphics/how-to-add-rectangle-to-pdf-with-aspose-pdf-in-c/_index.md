---
category: general
date: 2026-10-10
description: Học cách thêm hình chữ nhật vào PDF, vẽ hình dạng trên PDF và lưu PDF
  đã chỉnh sửa bằng Aspose.PDF. Bao gồm hướng dẫn từng bước để truy cập trang PDF
  cụ thể.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add rectangle to PDF
- draw shape on PDF
- save modified PDF
- add shape to PDF
- access specific PDF page
language: vi
lastmod: 2026-10-10
og_description: Thêm hình chữ nhật vào PDF bằng Aspose.PDF trong C#. Hướng dẫn này
  cho thấy cách vẽ hình trên PDF, truy cập một trang PDF cụ thể và lưu PDF đã chỉnh
  sửa.
og_image_alt: Screenshot of a PDF page with a blue rectangle overlay created by Aspose.PDF
og_title: Thêm hình chữ nhật vào PDF với Aspose.PDF – hướng dẫn C# đầy đủ
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Learn how to add rectangle to PDF, draw shape on PDF, and save modified
    PDF using Aspose.PDF. Includes step‑by‑step guide to access specific PDF page.
  headline: How to add rectangle to PDF with Aspose.PDF in C#
  type: TechArticle
- description: Learn how to add rectangle to PDF, draw shape on PDF, and save modified
    PDF using Aspose.PDF. Includes step‑by‑step guide to access specific PDF page.
  name: How to add rectangle to PDF with Aspose.PDF in C#
  steps:
  - name: Expected output
    text: 'Running the program prints:'
  - name: What if the PDF has only one page?
    text: Attempting to access `pdfDocument.Pages[1]` throws an `ArgumentOutOfRangeException`.
      Guard against this by checking `pdfDocument.Pages.Count` before indexing.
  - name: How to add multiple rectangles on different pages?
    text: Repeat Steps 2‑4 for each target page, adjusting the rectangle’s coordinates
      as needed. You can place the logic inside a loop that iterates over `pdfDocument.Pages`.
  - name: Can I use other shapes such as circles or polygons?
    text: Yes. Aspose.PDF provides `Ellipse`, `Polygon`, and `Polyline` classes that
      follow the same pattern as `Rectangle`. Replace the `new Aspose.Pdf.Drawing.Rectangle`
      call with the desired shape class.
  - name: Does the library support PDFs with rotated pages?
    text: Aspose.PDF automatically respects page rotation when rendering shapes. The
      rectangle’s coordinates are interpreted in the page’s native coordinate system,
      so no extra transformation is required.
  type: HowTo
tags:
- Aspose.PDF
- C#
- PDF manipulation
title: Cách thêm hình chữ nhật vào PDF bằng Aspose.PDF trong C#
url: /vi/net/images-graphics/how-to-add-rectangle-to-pdf-with-aspose-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách thêm hình chữ nhật vào PDF với Aspose.PDF trong C#

Nếu bạn cần **thêm hình chữ nhật vào PDF** một cách lập trình, hướng dẫn này sẽ chỉ cho bạn cách thực hiện. Bạn sẽ học cách **vẽ hình trên PDF**, chọn một trang cụ thể, và **lưu PDF đã chỉnh sửa** mà không gặp lỗi.

Làm việc với tài liệu PDF là một yêu cầu phổ biến cho báo cáo, lập hoá đơn hoặc chú thích tài liệu. Khi kết thúc tutorial này, bạn sẽ tự tin **thêm hình vào PDF**, xử lý các lỗi vượt giới hạn, và tích hợp giải pháp vào bất kỳ dự án .NET nào.

## Yêu cầu trước

* .NET 6.0 SDK hoặc phiên bản mới hơn đã được cài đặt  
* Visual Studio 2022 (hoặc bất kỳ IDE C# nào)  
* Giấy phép Aspose.PDF cho .NET hoặc khóa đánh giá miễn phí – API hoạt động tương tự trong cả hai chế độ  
* Một tệp PDF có tên `input.pdf` đặt trong thư mục mà bạn có thể tham chiếu từ mã của mình  

Các mục này là các phụ thuộc bên ngoài duy nhất cho ví dụ.

## Bước 1: Cài đặt gói NuGet Aspose.PDF

Thư viện Aspose.PDF cung cấp các lớp `Document`, `Rectangle` và các lớp vẽ khác mà bạn cần.

```bash
dotnet add package Aspose.PDF
```

Chạy lệnh này sẽ thêm phiên bản ổn định mới nhất của Aspose.PDF vào dự án của bạn, cho phép các lớp PDF được sử dụng trong quá trình biên dịch.

## Bước 2: Tải tài liệu PDF

Hoạt động đầu tiên là tải tệp nguồn. Điều này tạo ra một biểu diễn trong bộ nhớ mà bạn có thể chỉnh sửa.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using System;

class PdfRectangleExample
{
    static void Main()
    {
        // Load the PDF document from disk
        var pdfDocument = new Document(@"YOUR_DIRECTORY\input.pdf");
```

*Tại sao điều này quan trọng*: Việc tải tài liệu cho phép bạn truy cập vào bộ sưu tập các trang, điều này cần thiết để **truy cập trang PDF cụ thể** sau này.

## Bước 3: Truy cập trang thứ hai (chỉ mục bắt đầu từ 0)

Các trang PDF được đánh chỉ mục bắt đầu từ `0`. Để đặt một hình chữ nhật trên trang thứ hai, lấy trang có chỉ mục `1`.

```csharp
        // Access the second page (pages are zero‑based)
        var page = pdfDocument.Pages[1];
```

Nếu tài liệu có ít hơn hai trang, một `ArgumentOutOfRangeException` sẽ được ném ra, cảnh báo bạn cần một câu lệnh bảo vệ trong mã sản xuất.

## Bước 4: Tạo hình chữ nhật

Xác định vị trí và kích thước của hình chữ nhật bằng cấu trúc `Rectangle`, sau đó bọc nó trong một đối tượng vẽ của Aspose.

```csharp
        // Define rectangle bounds: (x, y, width, height)
        var rectangleBounds = new Rectangle(100, 100, 300, 200);
        var rectangleShape = new Aspose.Pdf.Drawing.Rectangle(rectangleBounds)
        {
            // Optional visual styling
            Border = new BorderInfo(BorderSide.All, 2f, Color.Blue),
            FillColor = Color.FromArgb(30, 0, 0, 255) // semi‑transparent blue
        };
```

*Tại sao điều này quan trọng*: Các thuộc tính `BorderInfo` và `FillColor` cho phép bạn **vẽ hình trên PDF** với viền rõ ràng và tùy chọn màu nền, làm cho hình chữ nhật nổi bật với người đọc.

## Bước 5: Thêm hình chữ nhật vào bộ sưu tập đoạn văn của trang

Aspose.PDF coi các đối tượng vẽ như các phần tử đoạn văn. Thêm hình chữ nhật vào bộ sưu tập `Paragraphs` của trang sẽ hiển thị nó trên trang.

```csharp
        // Add the rectangle shape to the page
        page.Paragraphs.Add(rectangleShape);
```

Tại thời điểm này, tài liệu PDF trong bộ nhớ đã chứa hình mới, nhưng tệp trên đĩa vẫn chưa thay đổi cho đến khi bạn lưu nó.

## Bước 6: Lưu PDF đã chỉnh sửa và xử lý lỗi vượt giới hạn

Gọi `Save` sẽ ghi tài liệu đã cập nhật vào một tệp mới. Nếu hình chữ nhật vượt quá kích thước trang, Aspose sẽ ném ra một `PdfException`. Bắt ngoại lệ này cho phép bạn báo cáo vấn đề một cách sạch sẽ.

```csharp
        try
        {
            // Save the altered PDF to a new file
            pdfDocument.Save(@"YOUR_DIRECTORY\output.pdf");
            Console.WriteLine("PDF saved successfully with rectangle added.");
        }
        catch (Aspose.Pdf.Exceptions.PdfException ex)
        {
            // Handle shape that does not fit on the page
            Console.WriteLine($"Shape out of bounds: {ex.Message}");
        }
    }
}
```

*Tại sao điều này quan trọng*: Khối `try/catch` đảm bảo ứng dụng của bạn **lưu PDF đã chỉnh sửa** một cách an toàn, và thông báo lỗi giúp bạn điều chỉnh tọa độ của hình chữ nhật nếu cần.

## Ví dụ hoàn chỉnh hoạt động

Kết hợp tất cả các bước lại, dưới đây là chương trình hoàn chỉnh, sẵn sàng để chạy:

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using System;
using System.Drawing; // Required for Color

class PdfRectangleExample
{
    static void Main()
    {
        // Step 1: Load the PDF document
        var pdfDocument = new Document(@"YOUR_DIRECTORY\input.pdf");

        // Step 2: Access the second page (zero‑based)
        var page = pdfDocument.Pages[1];

        // Step 3: Create a rectangle shape positioned at (100,100) with width 300 and height 200
        var rectangleBounds = new Rectangle(100, 100, 300, 200);
        var rectangleShape = new Aspose.Pdf.Drawing.Rectangle(rectangleBounds)
        {
            Border = new BorderInfo(BorderSide.All, 2f, Color.Blue),
            FillColor = Color.FromArgb(30, 0, 0, 255) // semi‑transparent blue
        };

        // Step 4: Add the rectangle shape to the page's paragraph collection
        page.Paragraphs.Add(rectangleShape);

        // Step 5: Save the modified PDF, handling out‑of‑bounds cases
        try
        {
            pdfDocument.Save(@"YOUR_DIRECTORY\output.pdf");
            Console.WriteLine("PDF saved successfully with rectangle added.");
        }
        catch (Aspose.Pdf.Exceptions.PdfException ex)
        {
            Console.WriteLine($"Shape out of bounds: {ex.Message}");
        }
    }
}
```

### Kết quả mong đợi

Chạy chương trình sẽ in ra:

```
PDF saved successfully with rectangle added.
```

và tạo ra `output.pdf` hiển thị nội dung gốc cộng với một hình chữ nhật màu xanh ở tọa độ đã chỉ định trên trang thứ hai.

Nếu hình chữ nhật lớn hơn trang, bạn sẽ thấy:

```
Shape out of bounds: The shape exceeds page margins.
```

## Các câu hỏi thường gặp và trường hợp đặc biệt

### Nếu PDF chỉ có một trang thì sao?

Cố gắng truy cập `pdfDocument.Pages[1]` sẽ ném ra một `ArgumentOutOfRangeException`. Để tránh điều này, hãy kiểm tra `pdfDocument.Pages.Count` trước khi sử dụng chỉ mục.

```csharp
if (pdfDocument.Pages.Count < 2)
{
    Console.WriteLine("Document does not contain a second page.");
    return;
}
```

### Cách thêm nhiều hình chữ nhật trên các trang khác nhau?

Lặp lại Các bước 2‑4 cho mỗi trang mục tiêu, điều chỉnh tọa độ của hình chữ nhật theo nhu cầu. Bạn có thể đặt logic này trong một vòng lặp lặp qua `pdfDocument.Pages`.

### Tôi có thể sử dụng các hình dạng khác như vòng tròn hoặc đa giác không?

Có. Aspose.PDF cung cấp các lớp `Ellipse`, `Polygon` và `Polyline` theo cùng mẫu như `Rectangle`. Thay thế lời gọi `new Aspose.Pdf.Drawing.Rectangle` bằng lớp hình dạng mong muốn.

### Thư viện có hỗ trợ PDF với các trang đã xoay không?

Aspose.PDF tự động tôn trọng việc xoay trang khi vẽ các hình. Tọa độ của hình chữ nhật được hiểu trong hệ tọa độ gốc của trang, vì vậy không cần chuyển đổi thêm.

## Các cân nhắc về hiệu năng

* **Sử dụng bộ nhớ** – Tải một PDF lớn (hàng trăm megabyte) sẽ tiêu tốn bộ nhớ tương ứng. Nếu bạn chỉ cần chỉnh sửa một trang duy nhất, hãy cân nhắc sử dụng `PdfFileInfo` để trích xuất trang đó, chỉnh sửa và sau đó hợp nhất lại.  
* **Xử lý hàng loạt** – Khi thêm hình vào nhiều tài liệu, hãy tái sử dụng một thể hiện `License` duy nhất để tránh việc xác thực giấy phép lặp lại gây tốn kém.

## Bước tiếp theo

Bây giờ bạn đã có thể **thêm hình chữ nhật vào PDF**, hãy khám phá các chủ đề liên quan sau:

* **draw shape on PDF** – học cách chồng lên văn bản, hình ảnh và watermark  
* **add shape to PDF** – kết hợp nhiều hình thành một lớp chú thích duy nhất  
* **save modified PDF** – sử dụng stream (`MemoryStream`) để trả về PDF trực tiếp từ API web  
* **access specific PDF page** – triển khai trích xuất phạm vi trang cho báo cáo tùy chỉnh  

Thử nghiệm với các màu sắc, kiểu đường và mức độ trong suốt khác nhau để phù hợp với hướng dẫn thương hiệu của bạn.

---

*Chúc lập trình vui vẻ! Nếu tutorial này đã giúp bạn **thêm hình chữ nhật vào PDF**, hãy cân nhắc chia sẻ nó với đồng nghiệp hoặc đóng góp cải tiến trở lại cộng đồng.*

## Bạn nên học gì tiếp theo?

Các tutorial sau đây bao gồm các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên đều có các ví dụ mã hoàn chỉnh với giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [How to Add Shape to PDF with Aspose.PDF in C# – Step‑by‑Step Guide](/pdf/english/net/images-graphics/how-to-add-shape-to-pdf-with-aspose-pdf-in-c-step-by-step-gu/)
- [How to Add a Line Object in PDF Using Aspose.PDF for .NET&#58; A Step-by-Step Guide](/pdf/english/net/document-manipulation/add-line-aspose-pdf-dotnet-tutorial/)
- [How to Create PDF in C# – Add Page, Draw Rectangle & Save](/pdf/english/net/document-creation/how-to-create-pdf-in-c-add-page-draw-rectangle-save/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}