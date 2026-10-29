---
category: general
date: 2026-09-05
description: Tạo tài liệu PDF trong C# bằng cách thêm một trang trống, vẽ một hình
  chữ nhật và lưu tệp PDF. Thực hiện theo ví dụ từng bước của Aspose.PDF.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create pdf document
- add blank page pdf
- draw rectangle pdf
- save pdf file
- how to add rectangle
language: vi
lastmod: 2026-09-05
og_description: Tạo tài liệu PDF trong C# bằng cách thêm một trang trống, vẽ một hình
  chữ nhật và lưu tệp PDF. Tham khảo ví dụ đầy đủ này với Aspose.PDF.
og_image_alt: Screenshot showing a PDF document with a drawn rectangle on a blank
  page
og_title: Tạo tài liệu PDF với trang trống và hình chữ nhật – Hướng dẫn C#
schemas:
- author: Aspose
  dateModified: '2026-09-05'
  description: Create PDF document in C# by adding a blank page, drawing a rectangle,
    and saving the PDF file. Follow a step‑by‑step Aspose.PDF example.
  headline: How to create PDF document with a blank page and rectangle
  type: TechArticle
- description: Create PDF document in C# by adding a blank page, drawing a rectangle,
    and saving the PDF file. Follow a step‑by‑step Aspose.PDF example.
  name: How to create PDF document with a blank page and rectangle
  steps:
  - name: 'Edge case: custom page size'
    text: 'If your layout requires a 6 × 9 inch page, replace the default call with:'
  - name: 'Pro tip: styling the rectangle'
    text: 'You can change the stroke color and line width:'
  - name: 'Edge case: overwriting existing files'
    text: 'Aspose.PDF overwrites an existing file by default. To protect previous
      outputs, check for file existence first:'
  - name: Expected output
    text: Running the program creates a single‑page PDF. When you open `output.pdf`
      you will see a blank white page with a red rectangle positioned 100 points from
      the left and bottom edges, measuring 200 × 200 points.
  type: HowTo
tags:
- PDF
- C#
- Aspose.PDF
- PDF generation
title: Cách tạo tài liệu PDF với trang trắng và hình chữ nhật
url: /vi/net/document-creation/how-to-create-pdf-document-with-a-blank-page-and-rectangle/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách tạo tài liệu PDF với trang trắng và hình chữ nhật

Nếu bạn cần **tạo tài liệu PDF** một cách lập trình, hướng dẫn này cung cấp giải pháp hoàn chỉnh bằng C#. Bạn sẽ học cách thêm một trang trắng, vẽ một hình chữ nhật trên trang đó, và cuối cùng lưu tệp PDF. Ví dụ sử dụng thư viện Aspose.PDF, hỗ trợ .NET 6+ và .NET Framework 4.5+.

Thêm trang trắng và vẽ các hình dạng là yêu cầu phổ biến cho hoá đơn, chứng chỉ, hoặc báo cáo tùy chỉnh. Khi kết thúc tutorial này, bạn sẽ có một dự án có thể chạy được tạo ra một PDF chứa một hình chữ nhật duy nhất được đặt tại (100, 100) với kích thước 200 × 200 điểm.

## Yêu cầu trước

Trước khi bắt đầu, hãy chắc chắn bạn có:

* Visual Studio 2022 (hoặc bất kỳ IDE C# nào)
* .NET 6 SDK hoặc .NET Framework 4.5+
* Gói NuGet Aspose.PDF cho .NET  
  ```bash
  dotnet add package Aspose.PDF
  ```
* Quyền ghi vào thư mục đầu ra

Không cần cấu hình bổ sung; mã chạy ngay lập tức.

## Tạo tài liệu PDF – tổng quan

Quá trình toàn bộ bao gồm bốn bước logic:

1. **Khởi tạo** một đối tượng `Document` – đại diện cho tệp PDF.
2. **Thêm một trang trắng** – trang cung cấp nền vẽ.
3. **Vẽ một hình chữ nhật** – đối tượng `Path` xác định hình dạng.
4. **Lưu tệp PDF** – ghi tài liệu ra đĩa.

Mỗi bước được tách riêng trong phần của nó để bạn có thể tái sử dụng hoặc thay thế các phần khi cần.

![Sơ đồ một PDF với hình chữ nhật trên trang trắng](https://example.com/placeholder-image.png){.img-fluid alt="Ảnh chụp màn hình hiển thị tài liệu PDF với một hình chữ nhật được vẽ trên trang trắng"}

## Thêm trang trắng pdf

Một PDF phải có ít nhất một trang trước khi có thể đặt bất kỳ đồ họa nào. Phương thức `Pages.Add()` tạo một trang trống với kích thước mặc định (A4). Nếu bạn cần kích thước khác, hãy truyền một đối số `PageSize`.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

// Step 1: Create a new PDF document
using var pdfDocument = new Document();

// Step 2: Add a blank page to the document
Page pdfPage = pdfDocument.Pages.Add();   // adds an A4 page by default
```

*Tiêu đề* – Đối tượng trang chứa các bộ sưu tập cho văn bản, hình ảnh và đồ họa vector. Không có trang, bất kỳ cố gắng nào để thêm hình chữ nhật sẽ gây ra ngoại lệ.

### Trường hợp đặc biệt: kích thước trang tùy chỉnh

Nếu bố cục của bạn yêu cầu một trang 6 × 9 inch, thay thế lời gọi mặc định bằng:

```csharp
var pageSize = new Size(432, 648); // 72 points per inch
Page pdfPage = pdfDocument.Pages.Add(pageSize);
```

## Vẽ hình chữ nhật pdf

Vẽ một hình chữ nhật là việc tạo một hình học `Rectangle` và bọc nó trong một `Path`. Lệnh `ValidateBounds()` đảm bảo hình dạng vừa trong lề trang, ngăn ngừa việc cắt bớt.

```csharp
// Step 3: Define a rectangle shape (x, y, width, height)
Rectangle shapeRect = new Rectangle(100, 100, 200, 200);

// Step 4: Add the rectangle to the page contents
Path rectanglePath = new Path(shapeRect).ValidateBounds();
pdfPage.Contents.Add(rectanglePath);
```

*Tiêu đề* – Đối tượng `Path` là primitive vector cấp thấp được Aspose.PDF sử dụng. Bằng cách xác thực giới hạn, bạn tránh lỗi thời gian chạy khi hình chữ nhật vượt quá giới hạn trang.

### Mẹo chuyên nghiệp: tạo kiểu cho hình chữ nhật

Bạn có thể thay đổi màu viền và độ rộng đường:

```csharp
rectanglePath.GraphInfo = new GraphInfo
{
    StrokeColor = Color.Red,
    LineWidth = 2
};
```

Điều này tạo ra một đường viền màu đỏ với độ dày 2 điểm.

## Lưu tệp pdf

Lưu trữ tài liệu sẽ hoàn thiện tệp trên đĩa. Phương thức `Save` chấp nhận một đường dẫn tệp hoặc một luồng. Cung cấp đường dẫn tuyệt đối làm cho vị trí rõ ràng, hữu ích cho các script tự động.

```csharp
// Step 5: Save the PDF to a file
string outputPath = Path.Combine(Environment.CurrentDirectory, "output.pdf");
pdfDocument.Save(outputPath);
Console.WriteLine($"PDF saved to {outputPath}");
```

*Tiêu đề* – Lưu là thời điểm duy nhất mà biểu diễn trong bộ nhớ trở thành tệp vật lý. Nếu bạn cần trả về PDF từ một web API, thay thế đường dẫn tệp bằng một `MemoryStream`.

### Trường hợp đặc biệt: ghi đè các tệp hiện có

Aspose.PDF mặc định sẽ ghi đè lên tệp đã tồn tại. Để bảo vệ các kết quả trước, hãy kiểm tra sự tồn tại của tệp trước:

```csharp
if (File.Exists(outputPath))
{
    File.Delete(outputPath);
}
pdfDocument.Save(outputPath);
```

## Cách thêm hình chữ nhật – các thực tiễn tốt nhất

* **Giữ tọa độ trong giới hạn lề trang** – sử dụng `ValidateBounds()` hoặc tính toán lề thủ công.
* **Tái sử dụng các đối tượng `GraphInfo`** khi vẽ nhiều hình; điều này giảm việc cấp phát bộ nhớ.
* **Giải phóng đối tượng `Document`** (như trong ví dụ `using var`) để giải phóng nhanh các tài nguyên gốc.
* **Kiểm tra với các cài đặt DPI khác nhau** nếu bạn sau này nhúng hình ảnh raster; các hình vector như hình chữ nhật vẫn sắc nét ở bất kỳ độ phân giải nào.

## Ví dụ làm việc đầy đủ

Dưới đây là toàn bộ chương trình bạn có thể sao chép vào một ứng dụng console. Nó biên dịch mà không cần sửa đổi và tạo ra `output.pdf` trong thư mục dự án.

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using Aspose.Pdf.Color;

class Program
{
    static void Main()
    {
        // Create a new PDF document
        using var pdfDocument = new Document();

        // Add a blank page to the document
        Page pdfPage = pdfDocument.Pages.Add();

        // Define a rectangle shape (x, y, width, height)
        Rectangle shapeRect = new Rectangle(100, 100, 200, 200);

        // Create a path for the rectangle and validate its bounds
        Path rectanglePath = new Path(shapeRect).ValidateBounds();

        // Optional: style the rectangle (red outline, 2‑pt width)
        rectanglePath.GraphInfo = new GraphInfo
        {
            StrokeColor = Color.Red,
            LineWidth = 2
        };

        // Add the rectangle to the page contents
        pdfPage.Contents.Add(rectanglePath);

        // Determine output path
        string outputPath = Path.Combine(Environment.CurrentDirectory, "output.pdf");

        // Ensure no leftover file blocks the save operation
        if (File.Exists(outputPath))
        {
            File.Delete(outputPath);
        }

        // Save the PDF to a file
        pdfDocument.Save(outputPath);
        Console.WriteLine($"PDF saved to {outputPath}");
    }
}
```

### Kết quả mong đợi

Chạy chương trình sẽ tạo một PDF một trang. Khi bạn mở `output.pdf` bạn sẽ thấy một trang trắng trống với một hình chữ nhật màu đỏ được đặt cách mép trái và dưới 100 điểm, kích thước 200 × 200 điểm.

## Kết luận

Bây giờ bạn đã biết cách **tạo tài liệu PDF**, **thêm trang trắng pdf**, **vẽ hình chữ nhật pdf**, và **lưu tệp pdf** bằng Aspose.PDF trong C#. Ví dụ bao gồm các lời gọi API thiết yếu, giải thích lý do mỗi lời gọi cần thiết, và cung cấp các mẹo cho các biến thể phổ biến như kích thước trang tùy chỉnh hoặc tạo kiểu cho hình chữ nhật.

Tiếp theo, khám phá các chủ đề liên quan như **thêm văn bản**, **nhúng hình ảnh**, hoặc **tạo báo cáo đa trang**. Mẫu tương tự—khởi tạo một `Document`, thao tác các trang, thêm nội dung vector hoặc raster, rồi `Save`—áp dụng cho tất cả các trường hợp đó. Hãy thoải mái thử nghiệm các hình dạng, màu sắc và bố cục trang khác nhau để phù hợp với nhu cầu dự án của bạn.

## Bạn nên học gì tiếp theo?

Các tutorial sau đây bao phủ các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoạt động đầy đủ với giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Tạo tài liệu PDF C# – Thêm trang, Vẽ hình chữ nhật & Lưu](/pdf/english/net/document-creation/create-pdf-document-c-add-page-draw-rectangle-save/)
- [Tạo tài liệu PDF với Aspose.PDF – Hướng dẫn từng bước](/pdf/english/net/document-creation/create-pdf-document-with-aspose-pdf-step-by-step-guide/)
- [Tạo tài liệu PDF với Aspose – Thêm trang, Hộp văn bản và Form](/pdf/english/net/forms-annotations/create-pdf-document-with-aspose-add-page-text-box-and-form/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}