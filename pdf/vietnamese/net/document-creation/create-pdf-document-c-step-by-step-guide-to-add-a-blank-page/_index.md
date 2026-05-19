---
category: general
date: 2026-04-10
description: Tạo tài liệu PDF C# nhanh chóng. Học cách thêm trang trắng PDF, vẽ hình
  chữ nhật PDF, thêm hình dạng chữ nhật và chèn chữ nhật vào PDF với mã rõ ràng.
draft: false
keywords:
- create pdf document c#
- add blank page pdf
- draw rectangle pdf
- add rectangle shape
- add rectangle to pdf
language: vi
og_description: Tạo tài liệu PDF bằng C# trong vài phút. Hướng dẫn này chỉ cách thêm
  trang PDF trống, vẽ hình chữ nhật trong PDF và thêm hình chữ nhật bằng mã đơn giản.
og_title: Tạo tài liệu PDF C# – Hướng dẫn toàn diện
tags:
- C#
- PDF
- Aspose.PDF
- Document Generation
title: Tạo tài liệu PDF C# – Hướng dẫn từng bước để thêm trang trắng và vẽ hình chữ
  nhật
url: /vi/net/document-creation/create-pdf-document-c-step-by-step-guide-to-add-a-blank-page/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo tài liệu PDF C# – Hướng dẫn đầy đủ

Bạn đã bao giờ cần **tạo tài liệu PDF C#** cho một tính năng báo cáo nhưng không chắc bắt đầu từ đâu chưa? Bạn không phải là người duy nhất. Trong nhiều dự án, rào cản đầu tiên là có được một tệp PDF trang trống sạch sẽ và sau đó vẽ các đồ họa đơn giản như một hình chữ nhật.  

Trong hướng dẫn này, chúng ta sẽ giải quyết vấn đề ngay lập tức: bạn sẽ thấy cách thêm một trang PDF trống, vẽ hình chữ nhật PDF, và cuối cùng thêm hình chữ nhật vào tệp — tất cả chỉ với một vài dòng C#. Khi kết thúc, bạn sẽ có một tệp `shapes.pdf` sẵn sàng để sử dụng mà bạn có thể mở bằng bất kỳ trình xem nào.

## Những gì bạn sẽ học

- Cách khởi tạo một tài liệu PDF bằng cách sử dụng Aspose.PDF cho .NET.  
- Các bước chính xác để **thêm trang PDF trống** và đặt một hình chữ nhật bên trong nó.  
- Tại sao lớp `Rectangle` là lựa chọn đúng để vẽ các hình dạng.  
- Những lỗi thường gặp như không khớp kích thước trang và cách tránh chúng.  

Không có công cụ bên ngoài, không có phép màu — chỉ là mã C# thuần túy mà bạn có thể sao chép‑dán vào một ứng dụng console.

## Yêu cầu trước

- .NET 6.0 trở lên (mã này cũng hoạt động với .NET Framework 4.6+).  
- Gói NuGet **Aspose.PDF for .NET** (`Install-Package Aspose.PDF`).  
- Kiến thức cơ bản về cú pháp C# (biến, câu lệnh `using`, v.v.).  

> **Mẹo chuyên nghiệp:** Nếu bạn đang sử dụng Visual Studio, NuGet Package Manager cho phép cài đặt Aspose.PDF chỉ bằng một cú nhấp chuột.

## Bước 1: Khởi tạo tài liệu PDF

Việc tạo PDF bắt đầu bằng một đối tượng `Document`. Hãy nghĩ nó như một canvas sẽ chứa mọi trang, hình ảnh hoặc hình dạng bạn thêm sau này.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

// Initialise a new PDF document – this is the core of create pdf document c#
var pdfDocument = new Document();
```

Lớp `Document` cung cấp cho bạn quyền truy cập vào bộ sưu tập `Pages`, nơi chúng ta sẽ **thêm trang PDF trống** sau này.

## Bước 2: Thêm một trang trống vào tài liệu

Một tệp PDF không có trang thực chất là rỗng. Thêm một trang đơn giản chỉ cần gọi `pdfDocument.Pages.Add()`. Trang mới sẽ kế thừa kích thước mặc định (A4) trừ khi bạn chỉ định khác.

```csharp
// Add a fresh, blank page – this satisfies the add blank page pdf requirement
Page page = pdfDocument.Pages.Add();
```

> **Tại sao điều này quan trọng:** Thêm trang trước đảm bảo rằng bất kỳ lệnh vẽ nào sau đó đều có bề mặt để hiển thị. Bỏ qua bước này sẽ gây lỗi thời gian chạy khi bạn cố vẽ một hình chữ nhật.

## Bước 3: Xác định giới hạn hình chữ nhật

Bây giờ chúng ta sẽ **vẽ hình chữ nhật PDF** bằng cách tạo một đối tượng `Rectangle`. Hàm khởi tạo nhận tọa độ X/Y góc dưới‑trái, sau đó là chiều rộng và chiều cao. Trong ví dụ của chúng ta, chúng ta muốn một hình chữ nhật vừa vặn bên trong trang, để lại một khoảng lề nhỏ.

```csharp
// Rectangle coordinates: (0,0) is the lower‑left corner of the page
// Width = 500, Height = 700 – fits comfortably on an A4 page
var rectangle = new Rectangle(0, 0, 500, 700);
```

Nếu bạn cần kích thước khác, chỉ cần điều chỉnh các giá trị chiều rộng/chiều cao. Gốc của hình chữ nhật (0,0) nằm ở góc dưới‑trái của trang, đây là nguồn gây nhầm lẫn phổ biến cho người mới.

## Bước 4: Thêm hình chữ nhật vào trang

Khi đối tượng hình chữ nhật đã sẵn sàng, chúng ta có thể **thêm hình chữ nhật** vào trang. Phương thức `AddRectangle` vẽ đường viền sử dụng trạng thái đồ họa hiện tại (mặc định là một đường đen mỏng).

```csharp
// Add the rectangle shape – this completes the add rectangle to pdf step
page.AddRectangle(rectangle);
```

Bạn có thể tùy chỉnh giao diện bằng cách sửa đổi đối tượng `Graphics` trước khi gọi `AddRectangle`, ví dụ, đặt `LineWidth` hoặc `Color`. Đối với việc tô đầy, bạn có thể dùng `page.AddAnnotation(new SquareAnnotation(...))`, nhưng điều này nằm ngoài phạm vi của hướng dẫn đơn giản này.

## Bước 5: Lưu tệp PDF

Cuối cùng, lưu tài liệu vào đĩa. Chọn một thư mục mà bạn có quyền ghi, và đặt tên tệp có ý nghĩa như `shapes.pdf`.

```csharp
// Save the PDF – you’ll find shapes.pdf in the specified directory
pdfDocument.Save(@"C:\Temp\shapes.pdf");
```

> **Lưu ý:** Câu lệnh `using` từ đoạn mã gốc không bắt buộc ở đây vì `Document` triển khai `IDisposable`. Tuy nhiên, bao nó trong `using` là thói quen tốt để dọn dẹp tài nguyên, đặc biệt trong các ứng dụng lớn hơn.

## Ví dụ hoàn chỉnh hoạt động

Kết hợp tất cả lại, đây là một chương trình console tự chứa mà bạn có thể chạy ngay lập tức:

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
            // Step 1: Create a new PDF document
            using (var pdfDocument = new Document())
            {
                // Step 2: Add a blank page to the document
                Page page = pdfDocument.Pages.Add();

                // Step 3: Define a rectangle that fits inside the page bounds (0,0 to 500,700)
                var rectangle = new Rectangle(0, 0, 500, 700);

                // Step 4: Add the rectangle shape to the page
                page.AddRectangle(rectangle);

                // Step 5: Save the PDF file
                string outputPath = @"C:\Temp\shapes.pdf";
                pdfDocument.Save(outputPath);

                Console.WriteLine($"PDF created successfully at {outputPath}");
            }
        }
    }
}
```

**Kết quả mong đợi:** Sau khi chạy chương trình, mở `C:\Temp\shapes.pdf`. Bạn sẽ thấy một trang duy nhất với một hình chữ nhật viền đen nằm ở góc dưới‑trái, có kích thước chính xác 500 × 700 điểm.

## Câu hỏi thường gặp & Các trường hợp đặc biệt

| Câu hỏi | Trả lời |
|----------|--------|
| *Tôi có thể thay đổi kích thước trang trước khi thêm hình chữ nhật không?* | Có. Tạo một `Page` với kích thước tùy chỉnh: `var page = pdfDocument.Pages.Add(); page.PageInfo.Width = 600; page.PageInfo.Height = 800;` |
| *Nếu tôi cần một hình chữ nhật được tô đầy thì sao?* | Sử dụng đối tượng `Graphics`: `page.Canvas.Rectangle(rectangle, Color.Blue, Color.LightBlue);` |
| *Aspose.PDF có miễn phí không?* | Nó cung cấp **bản dùng thử miễn phí** với đầy đủ chức năng; cần giấy phép thương mại cho việc sử dụng trong môi trường sản xuất. |
| *Làm sao để thêm nhiều hình chữ nhật?* | Chỉ cần lặp lại các bước 3‑4 với các đối tượng `Rectangle` khác nhau hoặc điều chỉnh tọa độ. |

## Các bước tiếp theo

Bây giờ bạn đã biết cách **tạo tài liệu PDF C#**, **thêm trang PDF trống**, và **vẽ hình chữ nhật PDF**, bạn có thể muốn khám phá:

- Thêm văn bản vào bên trong hình chữ nhật (`TextFragment`, `page.Paragraphs.Add`).  
- Chèn hình ảnh (`page.Resources.Images.Add`) để tạo báo cáo phong phú hơn.  
- Xuất PDF sang các định dạng khác như PNG hoặc DOCX bằng các API chuyển đổi của Aspose.  

Tất cả các chủ đề này tự nhiên mở rộng từ nền tảng **thêm hình chữ nhật vào PDF** mà chúng ta đã xây dựng ở đây.

---

*Chúc lập trình vui vẻ!* Nếu bạn gặp bất kỳ khó khăn nào, hãy thoải mái để lại bình luận bên dưới. Và hãy nhớ — một khi bạn nắm vững các kiến thức cơ bản, việc tạo PDF phức tạp sẽ trở nên dễ dàng.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}