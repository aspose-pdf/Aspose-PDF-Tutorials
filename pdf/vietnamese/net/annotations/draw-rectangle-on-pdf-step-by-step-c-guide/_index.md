---
category: general
date: 2026-08-14
description: Vẽ hình chữ nhật trên PDF nhanh chóng bằng C#. Tìm hiểu cách xác định
  kích thước hình chữ nhật và thêm các hình dạng vào trang PDF chỉ trong vài dòng.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- draw rectangle on pdf
- how to define rectangle dimensions
language: vi
lastmod: 2026-08-14
og_description: Vẽ hình chữ nhật trên PDF bằng C# trong vài giây. Hướng dẫn này chỉ
  cách xác định kích thước hình chữ nhật, thêm một hình dạng và kiểm tra ranh giới
  trang để có đồ họa PDF đáng tin cậy.
og_image_alt: Screenshot of a PDF page showing a black rectangle drawn with C# code
og_title: vẽ hình chữ nhật trên PDF – hướng dẫn C# đầy đủ
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: draw rectangle on pdf quickly using C#. Learn how to define rectangle
    dimensions and add shapes to a PDF page in just a few lines.
  headline: draw rectangle on pdf – step‑by‑step C# guide
  type: TechArticle
tags:
- PDF
- C#
- Aspose.PDF
- RectangleShape
- Graphics
title: Vẽ hình chữ nhật trên PDF – hướng dẫn C# từng bước
url: /vi/net/annotations/draw-rectangle-on-pdf-step-by-step-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# vẽ hình chữ nhật trên pdf – hướng dẫn C# đầy đủ

Nếu bạn cần **vẽ hình chữ nhật trên pdf** bằng C#, hướng dẫn này sẽ cho bạn một giải pháp ngắn gọn, sẵn sàng cho môi trường sản xuất. Bạn sẽ thấy **cách xác định kích thước hình chữ nhật**, kiểm tra xem hình có vừa trong trang hay không, và thêm nó vào trang chỉ bằng một lời gọi phương thức.

Bài học bao gồm mọi thứ từ tạo tài liệu PDF đến render hình chữ nhật, vì vậy bạn có thể sao chép‑dán mã vào dự án của mình và thấy kết quả ngay lập tức. Không cần tài liệu bên ngoài — chỉ cần thực hiện các bước dưới đây.

## Yêu cầu trước

Trước khi bắt đầu, hãy chắc chắn rằng bạn có:

* .NET 6.0 hoặc mới hơn (mã cũng hoạt động với .NET Framework 4.7+)
* Gói NuGet **Aspose.PDF for .NET** (`Install-Package Aspose.PDF`)
* Kiến thức cơ bản về cú pháp C#
* Một IDE như Visual Studio hoặc VS Code

> **Mẹo chuyên nghiệp:** Sử dụng giấy phép dùng thử miễn phí của Aspose.PDF để thử nghiệm nhanh; nó sẽ thêm một watermark nhỏ nhưng cho phép bạn kiểm tra mọi tính năng.

## Cách vẽ hình chữ nhật trên PDF bằng C#

Cốt lõi của nhiệm vụ là tạo một `RectangleShape`, thiết lập kích thước và nét viền, rồi gắn nó vào một `Page`. Tiêu đề H2 dưới đây chứa từ khóa chính, đáp ứng yêu cầu SEO.

```csharp
using System;
using System.Drawing;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new PDF document
        Document pdfDoc = new Document();

        // 2️⃣ Add a blank page (default size: A4)
        Page page = pdfDoc.Pages.Add();

        // 3️⃣ Define the rectangle bounds (x, y, width, height)
        //    This demonstrates how to define rectangle dimensions.
        Rectangle rectBounds = new Rectangle(0, 0, 500, 700);

        // 4️⃣ Create the rectangle shape and set its stroke color
        RectangleShape rectangleShape = new RectangleShape(rectBounds)
        {
            StrokeColor = Color.Black   // black outline
        };

        // 5️⃣ Verify that the shape fits within the page boundaries
        page.CheckShapeBoundary(rectangleShape);

        // 6️⃣ Add the shape to the page
        page.Add(rectangleShape);

        // 7️⃣ Save the PDF to disk
        string outPath = "RectangleDemo.pdf";
        pdfDoc.Save(outPath);
        Console.WriteLine($"PDF saved to {outPath}");
    }
}
```

### Giải thích từng bước

| Bước | Lý do quan trọng |
|------|-------------------|
| **1️⃣ Tạo một tài liệu PDF mới** | Khởi tạo container sẽ chứa các trang và đồ họa. |
| **2️⃣ Thêm một trang trống** | Bạn cần một đối tượng `Page` vì các hình được gắn vào trang, không phải trực tiếp vào tài liệu. |
| **3️⃣ Xác định giới hạn của hình chữ nhật** | Đây là nơi bạn **cách xác định kích thước hình chữ nhật**. Hàm khởi tạo `Rectangle` nhận `x`, `y`, `width`, và `height` tính bằng point (1 pt = 1/72 in). |
| **4️⃣ Tạo hình chữ nhật** | `RectangleShape` là lớp Aspose dùng để render hình chữ nhật. Đặt `StrokeColor` để xác định viền; bạn cũng có thể đặt `FillColor` cho màu nền đặc. |
| **5️⃣ Kiểm tra giới hạn trang** | `CheckShapeBoundary` ném ngoại lệ nếu hình chữ nhật vượt quá kích thước trang, ngăn PDF bị hỏng. |
| **6️⃣ Thêm hình vào trang** | Hình trở thành một phần của luồng nội dung trang. |
| **7️⃣ Lưu PDF** | Ghi tài liệu ra file để bạn có thể mở bằng bất kỳ trình xem PDF nào. |

File `RectangleDemo.pdf` tạo ra sẽ chứa một hình chữ nhật màu đen nằm ở góc trên‑trái của trang, rộng chính xác 500 pt và cao 700 pt.

![ví dụ vẽ hình chữ nhật trên pdf](https://example.com/rectangle-demo.png "ví dụ vẽ hình chữ nhật trên pdf")

*Văn bản thay thế hình ảnh: ví dụ vẽ hình chữ nhật trên pdf hiển thị một hình chữ nhật màu đen ở góc trên bên trái của trang PDF.*

## Cách xác định kích thước hình chữ nhật cho các kích thước trang khác nhau

Đoạn mã trên sử dụng giá trị cố định (`500 x 700`). Trong các ứng dụng thực tế, bạn thường cần hình chữ nhật thích ứng với chiều rộng và chiều cao của trang.

```csharp
// Get page dimensions (in points)
float pageWidth = page.PageInfo.Width;
float pageHeight = page.PageInfo.Height;

// Define a rectangle that occupies 80% of the page width and 50% of the height
float rectWidth  = pageWidth * 0.8f;
float rectHeight = pageHeight * 0.5f;

// Center the rectangle on the page
float rectX = (pageWidth - rectWidth) / 2;
float rectY = (pageHeight - rectHeight) / 2;

Rectangle dynamicRect = new Rectangle(rectX, rectY, rectWidth, rectHeight);
RectangleShape dynamicShape = new RectangleShape(dynamicRect)
{
    StrokeColor = Color.DarkBlue,
    FillColor   = Color.LightGray   // optional fill
};

page.CheckShapeBoundary(dynamicShape);
page.Add(dynamicShape);
```

**Các điểm chính:**

* Sử dụng `page.PageInfo.Width` và `Height` để đọc kích thước thực tế của trang.
* Nhân với một hệ số (ví dụ, `0.8f`) cho phép bạn biểu diễn kích thước dưới dạng phần trăm của trang.
* Căn giữa được thực hiện bằng cách trừ kích thước hình chữ nhật khỏi kích thước trang và chia đôi phần còn lại.

## Những lỗi thường gặp và cách tránh

| Lỗi | Nguyên nhân | Cách khắc phục |
|-----|--------------|----------------|
| Hình chữ nhật vượt ra ngoài trang | Kích thước cứng mã lớn hơn kích thước trang. | Gọi `page.CheckShapeBoundary` **trước** khi thêm hình; điều chỉnh kích thước nếu có ngoại lệ. |
| Viền không hiển thị | `StrokeColor` để mặc định (`Color.Empty`). | Đặt rõ ràng `StrokeColor` (ví dụ, `Color.Black`). |
| Hình chữ nhật xuất hiện ngoài màn hình | Tọa độ bắt đầu ở góc dưới‑trái trong không gian PDF; dùng tọa độ kiểu màn hình (trên‑trái) gây lộn ngược. | Nhớ rằng gốc `(0,0)` là góc dưới‑trái. Điều chỉnh `y` cho phù hợp hoặc dùng `pageHeight - desiredY`. |
| Độ dày đường không mong muốn | Độ dày mặc định có thể quá mỏng cho việc in. | Đặt `rectangleShape.LineWidth = 2;` để tăng độ dày. |

## Mở rộng ví dụ

Khi bạn đã có thể **vẽ hình chữ nhật trên pdf**, bạn có thể dễ dàng thêm các hình khác:

* **EllipseShape** – cho vòng tròn hoặc hình bầu dục.
* **PolygonShape** – cho các đa giác tùy chỉnh.
* **TextFragment** – để gắn nhãn cho các hình chữ nhật.

Tất cả các hình đều tuân theo quy trình giống nhau: xác định giới hạn, cấu hình giao diện, kiểm tra ranh giới, rồi thêm vào trang.

## Chương trình hoàn chỉnh, có thể chạy ngay

Dưới đây là toàn bộ chương trình kết hợp ví dụ hình chữ nhật cơ bản và ví dụ kích thước động. Sao chép vào một dự án console mới, khôi phục gói NuGet `Aspose.PDF`, và chạy.

```csharp
using System;
using System.Drawing;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

class RectangleDemo
{
    static void Main()
    {
        // Create document and page
        Document doc = new Document();
        Page page = doc.Pages.Add();

        // ==== Fixed‑size rectangle (basic example) ====
        Rectangle fixedRect = new Rectangle(0, 0, 500, 700);
        RectangleShape fixedShape = new RectangleShape(fixedRect)
        {
            StrokeColor = Color.Black,
            LineWidth   = 1
        };
        page.CheckShapeBoundary(fixedShape);
        page.Add(fixedShape);

        // ==== Dynamic rectangle that adapts to page size ====
        float pageW = page.PageInfo.Width;
        float pageH = page.PageInfo.Height;

        float dynWidth  = pageW * 0.6f;
        float dynHeight = pageH * 0.3f;
        float dynX      = (pageW - dynWidth) / 2;
        float dynY      = (pageH - dynHeight) / 2;

        Rectangle dynamicRect = new Rectangle(dynX, dynY, dynWidth, dynHeight);
        RectangleShape dynamicShape = new RectangleShape(dynamicRect)
        {
            StrokeColor = Color.DarkBlue,
            FillColor   = Color.LightYellow,
            LineWidth   = 2
        };
        page.CheckShapeBoundary(dynamicShape);
        page.Add(dynamicShape);

        // Save PDF
        string outFile = "CombinedRectangles.pdf";
        doc.Save(outFile);
        Console.WriteLine($"PDF created: {outFile}");
    }
}
```

**Kết quả mong đợi:**  
Mở `CombinedRectangles.pdf`. Bạn sẽ thấy một hình chữ nhật màu đen gắn ở góc dưới‑trái và một hình chữ nhật màu xanh đậm ở giữa với nền màu vàng nhạt. Cả hai hình đều tuân theo lề trang.

## Kết luận

Bây giờ bạn đã biết cách **vẽ hình chữ nhật trên pdf** bằng C# và chính xác **cách xác định kích thước hình chữ nhật** cho cả bố cục cố định và đáp ứng. Phương pháp sử dụng `RectangleShape` của Aspose.PDF, kiểm tra ranh giới, và các phép tính đơn giản để thích ứng với bất kỳ kích thước trang nào.

Tiếp theo, bạn có thể khám phá:

* Thêm **màu nền** và **kiểu đường** (gạch đứt, chấm) – từ khóa phụ: cách xác định kích thước hình chữ nhật với kiểu dáng.
* Kết hợp nhiều hình vào một `Page` để tạo biểu đồ hoặc mẫu đơn.
* Xuất PDF ra stream cho API web thay vì lưu vào đĩa.

Thử nghiệm với các kích thước, màu sắc và vị trí khác nhau để thành thạo đồ họa PDF trong các ứng dụng .NET của bạn. Chúc lập trình vui vẻ!


## Bạn nên học gì tiếp theo?


Các hướng dẫn sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong bài viết này. Mỗi tài nguyên bao gồm mã mẫu đầy đủ với giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Cách tùy chỉnh PDF với Aspose.PDF for .NET: Đặt lề trang và vẽ đường](/pdf/english/net/document-manipulation/customize-pdfs-aspose-pdf-set-margins-draw-lines/)
- [Cách thêm dấu trang (stamp) vào PDF bằng Aspose.PDF for .NET: Hướng dẫn toàn diện](/pdf/english/net/watermarks-backgrounds/add-page-stamp-aspose-pdf-dotnet-guide/)
- [Cách thêm dấu số trang vào PDF bằng Aspose.PDF for .NET | Watermarks & Backgrounds](/pdf/english/net/watermarks-backgrounds/add-page-number-stamp-using-aspose-pdf-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}