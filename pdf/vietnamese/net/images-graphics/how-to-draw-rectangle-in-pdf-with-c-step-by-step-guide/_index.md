---
category: general
date: 2026-03-27
description: Học cách vẽ hình chữ nhật trong PDF bằng Aspose.Pdf cho C#. Thêm hình
  chữ nhật vào PDF, thêm hình dạng vào PDF và vẽ hình dạng trên PDF với các ví dụ
  mã rõ ràng.
draft: false
keywords:
- how to draw rectangle
- add rectangle to pdf
- add shape to pdf
- draw shape on pdf
- draw rectangle in pdf
language: vi
og_description: Thành thạo cách vẽ hình chữ nhật trong PDF bằng Aspose.Pdf. Hướng
  dẫn này chỉ cho bạn cách thêm hình chữ nhật vào PDF, thêm hình dạng vào PDF và vẽ
  hình dạng trên PDF từng bước một.
og_title: Cách Vẽ Hình Chữ Nhật trong PDF bằng C# – Hướng Dẫn Toàn Diện
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Cách Vẽ Hình Chữ Nhật trong PDF bằng C# – Hướng Dẫn Từng Bước
url: /vi/net/images-graphics/how-to-draw-rectangle-in-pdf-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách Vẽ Hình Chữ Nhật trong PDF bằng C# – Hướng Dẫn Từng Bước

Bạn đã bao giờ tự hỏi **cách vẽ hình chữ nhật** trong PDF mà không phải vật lộn với cú pháp PDF cấp thấp chưa? Bạn không phải là người duy nhất. Nhiều lập trình viên gặp khó khăn khi cần hiển thị một bounding box, một vùng nổi bật, hoặc một yếu tố trang trí đơn giản trong tài liệu được tạo ra. Tin tốt là gì? Với Aspose.Pdf cho .NET, quá trình này trở nên cực kỳ đơn giản.

Trong tutorial này, chúng ta sẽ đi qua mọi thứ bạn cần để **thêm hình chữ nhật vào PDF**, **thêm hình dạng vào PDF**, và cuối cùng là **vẽ hình chữ nhật trong PDF** bằng C# sạch sẽ và idiomatic. Khi hoàn thành, bạn sẽ có một chương trình chạy được tạo ra file PDF chứa một hình chữ nhật sắc nét—không cần công cụ bên ngoài.

## Các Điều Kiện Cần Có

- .NET 6.0 trở lên (mã cũng hoạt động với .NET Core và .NET Framework)
- Gói NuGet Aspose.Pdf for .NET (`Install-Package Aspose.Pdf`)
- Môi trường phát triển C# cơ bản (Visual Studio, VS Code, Rider, v.v.)

Không cần thư viện nào khác; mọi thứ còn lại đều được Aspose.Pdf tự xử lý.

## Bước 1: Thiết Lập Dự Án và Nhập Namespace

Đầu tiên, tạo một ứng dụng console mới và nhập namespace Aspose.Pdf.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

namespace PdfRectangleDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll place the rest of the code here.
        }
    }
}
```

**Tại sao lại quan trọng:** Nhập `Aspose.Pdf.Drawing` cho phép bạn truy cập lớp hình dạng `Rectangle` mà chúng ta sẽ dùng để **vẽ hình dạng trên PDF**. Giữ cho điểm vào chương trình gọn gàng sẽ giúp các bước sau dễ theo dõi hơn.

## Bước 2: Tạo Tài Liệu PDF Mới và Thêm Trang

Một PDF không có trang là vô nghĩa, vì vậy chúng ta bắt đầu bằng việc tạo một đối tượng tài liệu và thêm một trang duy nhất.

```csharp
// Step 2: Initialize a new PDF document
Document pdfDoc = new Document();

// Add a blank page to the document (size defaults to A4)
Page page = pdfDoc.Pages.Add();
```

**Giải thích:** Lớp `Document` đại diện cho toàn bộ file, trong khi `Pages.Add()` trả về một đối tượng `Page` mới, nơi chúng ta sẽ **thêm hình chữ nhật vào PDF** sau này. Kích thước A4 mặc định phù hợp với hầu hết các trường hợp, nhưng bạn có thể truyền chiều rộng/chiều cao nếu cần canvas tùy chỉnh.

## Bước 3: Định Nghĩa Hình Chữ Nhật

Bây giờ là phần cốt lõi của **cách vẽ hình chữ nhật**—định vị và kích thước của nó.

```csharp
// Step 3: Define a rectangle shape (x, y, width, height)
// Coordinates are measured from the lower‑left corner of the page.
var rectangleShape = new Rectangle(100, 500, 300, 200)
{
    // Optional: set line color and fill color
    BorderColor = Color.Black,
    BorderWidth = 2,
    FillColor = Color.LightGray
};
```

**Lý do chúng ta đặt các thuộc tính này:**  
- `BorderColor` và `BorderWidth` điều khiển đường viền, giúp hình chữ nhật hiển thị.  
- `FillColor` cung cấp nền nhẹ, hữu ích khi bạn muốn làm nổi bật một vùng.  
- Constructor `(x, y, width, height)` cho phép bạn **vẽ hình chữ nhật trong PDF** chính xác ở vị trí mong muốn.

## Bước 4: Thêm Hình Chữ Nhật vào Trang

Khi hình đã sẵn sàng, chúng ta **thêm hình dạng vào PDF** bằng cách gắn nó vào bộ sưu tập `Annotations` của trang. Aspose.Pdf sẽ tự động xác thực giới hạn, vì vậy bạn không cần lo lắng về việc tràn ra ngoài.

```csharp
// Step 4: Add the rectangle shape to the page
page.Annotations.Add(rectangleShape);
```

**Điều gì xảy ra phía sau:** Bộ sưu tập `Annotations` xử lý hình chữ nhật như một đồ họa vector. Khi PDF được render, thư viện sẽ chuyển các tọa độ của chúng ta thành luồng nội dung PDF.

## Bước 5: Lưu Tài Liệu

Cuối cùng, ghi PDF ra đĩa để bạn có thể mở nó bằng bất kỳ trình xem nào.

```csharp
// Step 5: Save the PDF file
string outputPath = "RectangleDemo.pdf";
pdfDoc.Save(outputPath);
Console.WriteLine($"PDF saved to {outputPath}");
```

**Kết quả:** Mở `RectangleDemo.pdf` sẽ hiển thị một hình chữ nhật màu xám nhạt với viền đen, nằm cách lề trái 100 pts và cách đáy trang 500 pts. Đó là giải pháp hoàn chỉnh cho **cách vẽ hình chữ nhật** trong PDF bằng C#.

## Ví Dụ Hoàn Chỉnh Hoạt Động

Kết hợp tất cả các phần lại, đây là chương trình đầy đủ, sẵn sàng chạy:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using Aspose.Pdf.Color;

namespace PdfRectangleDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Initialize a new PDF document
            Document pdfDoc = new Document();

            // Add a blank page (A4 by default)
            Page page = pdfDoc.Pages.Add();

            // Define a rectangle shape (x, y, width, height)
            var rectangleShape = new Rectangle(100, 500, 300, 200)
            {
                BorderColor = Color.Black,
                BorderWidth = 2,
                FillColor = Color.LightGray
            };

            // Add the rectangle to the page
            page.Annotations.Add(rectangleShape);

            // Save the document
            string outputPath = "RectangleDemo.pdf";
            pdfDoc.Save(outputPath);
            Console.WriteLine($"PDF saved to {outputPath}");
        }
    }
}
```

**Kết quả mong đợi:** Một file tên `RectangleDemo.pdf` chứa một trang duy nhất với hình chữ nhật màu xám nhạt ở giữa, viền đen. Bạn có thể mở nó bằng Adobe Reader, Chrome, hoặc bất kỳ trình xem PDF nào.

## Các Biến Thể Thông Thường & Trường Hợp Cạnh

### 1. Vẽ Nhiều Hình Chữ Nhật

Nếu bạn cần **thêm hình chữ nhật vào PDF** nhiều lần, chỉ cần tạo thêm các đối tượng `Rectangle` và thêm từng cái vào `page.Annotations`. Việc lặp qua một tập hợp các tọa độ là rất đơn giản.

```csharp
foreach (var rectInfo in rectangles)
{
    var rect = new Rectangle(rectInfo.X, rectInfo.Y, rectInfo.Width, rectInfo.Height)
    {
        BorderColor = Color.Blue,
        BorderWidth = 1,
        FillColor = Color.Transparent
    };
    page.Annotations.Add(rect);
}
```

### 2. Sử Dụng Đơn Vị Khác

Aspose.Pdf làm việc bằng điểm (1 pt = 1/72 inch). Nếu bạn muốn dùng milimet, hãy chuyển đổi trước:

```csharp
double mmToPt = 72.0 / 25.4;
float x = (float)(20 * mmToPt); // 20 mm from left
float y = (float)(150 * mmToPt);
```

### 3. Thêm Hình Chữ Nhật như Trường Form

Khi bạn cần một hình chữ nhật tương tác (ví dụ: vùng nhấp), hãy dùng `LinkAnnotation` thay vì `Rectangle` thông thường. Mã nguồn tương tự nhưng thêm URL hoặc hành động JavaScript.

### 4. Các Vấn Đề Tương Thích

Aspose.Pdf phiên bản 23.9 (phát hành đầu năm 2026) hoàn toàn hỗ trợ các API được trình bày ở trên. Các phiên bản cũ hơn có thể yêu cầu `page.AddAnnotation(rectangleShape)` thay vì `page.Annotations.Add`. Luôn kiểm tra ghi chú phát hành nếu gặp lỗi biên dịch.

## Mẹo Chuyên Gia & Những Cạm Bẫy

- **Mẹo chuyên gia:** Đặt `FillColor = Color.Transparent` nếu bạn chỉ cần viền. Điều này sẽ giảm kích thước file hơi.
- **Cẩn thận với:** Các tọa độ vượt quá kích thước trang. Aspose.Pdf sẽ cắt hình một cách im lặng, điều này có thể gây nhầm lẫn khi debug.
- **Lưu ý hiệu năng:** Thêm hàng ngàn hình chữ nhật là ổn, nhưng nếu bạn tạo báo cáo lớn, hãy cân nhắc gom nhiều hình vào một đối tượng `Graphics` duy nhất để giảm overhead.

## Tham Chiếu Hình Ảnh

Dưới đây là một ảnh chụp nhanh của PDF đã tạo (hình chữ nhật được tô sáng màu xám nhạt). Văn bản alt bao gồm từ khóa chính cho SEO.

![cách vẽ hình chữ nhật trong PDF ví dụ](https://example.com/images/rectangle-demo.png "cách vẽ hình chữ nhật trong PDF ví dụ")

## Kết Luận

Chúng ta đã tìm hiểu **cách vẽ hình chữ nhật** trong PDF bằng Aspose.Pdf cho C#. Bằng cách tạo một `Document`, thêm một `Page`, định nghĩa một hình dạng `Rectangle`, và cuối cùng **thêm hình dạng vào PDF**, bạn có thể tạo đồ họa vector chỉ với vài dòng mã. Dù bạn cần **thêm hình chữ nhật vào pdf** để làm nổi bật, gỡ lỗi bố cục, hay tạo lớp phủ UI, cách tiếp cận này mở rộng tốt.

Tiếp theo, bạn có thể khám phá **vẽ hình dạng trên pdf** ngoài hình chữ nhật—như vòng tròn, polyline, hoặc thậm chí các đường SVG tùy chỉnh. Hoặc đi sâu vào render văn bản, chèn ảnh, và thao tác form PDF để xây dựng các báo cáo đầy đủ tính năng. Thư viện Aspose.Pdf cung cấp API phong phú, và với những kiến thức cơ bản ở đây, bạn đã sẵn sàng thử nghiệm.

Chúc lập trình vui vẻ, và hy vọng các PDF của bạn luôn trông đúng như bạn mong muốn!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}