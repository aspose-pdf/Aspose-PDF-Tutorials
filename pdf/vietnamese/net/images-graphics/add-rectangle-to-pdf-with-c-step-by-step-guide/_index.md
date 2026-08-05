---
category: general
date: 2026-08-04
description: Thêm hình chữ nhật vào PDF bằng C#. Tìm hiểu cách vẽ hình dạng trong
  PDF C# với Aspose.Pdf trong một ví dụ rõ ràng, đầy đủ.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add rectangle to pdf
- how to draw shape in pdf c#
language: vi
lastmod: 2026-08-04
og_description: Thêm hình chữ nhật vào PDF bằng C#. Hướng dẫn này cho thấy cách vẽ
  hình trong PDF bằng C# một cách nhanh chóng và đáng tin cậy.
og_image_alt: Screenshot of a PDF page with a blue rectangle drawn by C# code
og_title: Thêm hình chữ nhật vào PDF bằng C# – hướng dẫn lập trình đầy đủ
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Add rectangle to PDF using C#. Learn how to draw shape in PDF C# with
    Aspose.Pdf in a clear, complete example.
  headline: Add rectangle to PDF with C# – step‑by‑step guide
  type: TechArticle
- description: Add rectangle to PDF using C#. Learn how to draw shape in PDF C# with
    Aspose.Pdf in a clear, complete example.
  name: Add rectangle to PDF with C# – step‑by‑step guide
  steps:
  - name: '**Create a new console project**'
    text: '**Create a new console project**'
  - name: '**Add the Aspose.Pdf package**'
    text: '**Add the Aspose.Pdf package**'
  - name: '**Place `input.pdf`** in the project directory (or any folder you reference
      later).'
    text: '**Place `input.pdf`** in the project directory (or any folder you reference
      later).'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Thêm hình chữ nhật vào PDF bằng C# – hướng dẫn từng bước
url: /vi/net/images-graphics/add-rectangle-to-pdf-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Thêm hình chữ nhật vào PDF bằng C# – hướng dẫn từng bước

Nếu bạn cần **thêm hình chữ nhật vào PDF** từ một ứng dụng C#, hướng dẫn này sẽ chỉ cho bạn cách thực hiện chính xác. Bạn sẽ thấy một ví dụ đầy đủ, có thể chạy được, vẽ một hình dạng trong PDF C# bằng thư viện Aspose.Pdf, và bạn sẽ hiểu tại sao mỗi dòng mã đều quan trọng.

Việc vẽ các hình dạng trong PDF là một yêu cầu phổ biến cho các công cụ tạo báo cáo, mẫu hoá đơn và thương hiệu tài liệu tùy chỉnh. Khi kết thúc bài hướng dẫn này, bạn có thể chèn bất kỳ chú thích hình chữ nhật nào, thay đổi kích thước, màu sắc hoặc vị trí của nó, và lưu tài liệu đã chỉnh sửa mà không mất nội dung hiện có.

**Bạn sẽ học được**

* Cách tải một PDF hiện có bằng Aspose.Pdf.
* Cách định nghĩa giới hạn hình chữ nhật và tạo một hình chữ nhật.
* Cách thêm hình chữ nhật vào bộ sưu tập đoạn văn của một trang.
* Cách lưu PDF đã cập nhật và xác minh kết quả.
* Các biến thể cho nhiều trang, độ trong suốt và kiểu đường viền tùy chỉnh.

**Yêu cầu trước**

* .NET 6.0 trở lên (mã cũng hoạt động với .NET Framework 4.7+).
* Visual Studio 2022 hoặc bất kỳ IDE C# nào.
* Tham chiếu NuGet tới `Aspose.Pdf` (bản dùng thử miễn phí hoặc phiên bản có giấy phép).
* Tệp PDF đầu vào có tên `input.pdf` được đặt trong thư mục bạn kiểm soát.

---

## Cách vẽ hình dạng trong PDF C# – thiết lập dự án

1. **Tạo một dự án console mới**  

   ```bash
   dotnet new console -n PdfRectangleDemo
   cd PdfRectangleDemo
   ```

2. **Thêm gói Aspose.Pdf**  

   ```bash
   dotnet add package Aspose.Pdf
   ```

3. **Đặt `input.pdf`** vào thư mục dự án (hoặc bất kỳ thư mục nào bạn sẽ tham chiếu sau này).

Dự án hiện đã sẵn sàng để biên dịch mã sẽ **thêm hình chữ nhật vào PDF**.

---

## Step 1: Load the PDF document

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

class Program
{
    static void Main()
    {
        // Load the existing PDF file.
        Document pdfDoc = new Document("input.pdf");
```

*Lớp `Document` phân tích tệp và cung cấp một bộ sưu tập `Pages`. Việc tải là thao tác đầu tiên cần thiết trước khi thực hiện bất kỳ việc vẽ nào.*

---

## Step 2: Choose the target page

```csharp
        // Get the first page (pages are 1‑based).
        Page firstPage = pdfDoc.Pages[1];
```

*Nếu bạn cần thêm hình chữ nhật vào một trang khác, hãy thay thế chỉ mục bằng số trang mong muốn. Thư viện sẽ ném ngoại lệ khi chỉ mục vượt quá phạm vi, vì vậy hãy đảm bảo PDF có đủ số trang.*

---

## Step 3: Define rectangle bounds

```csharp
        // Define the rectangle's position and size (points).
        // (left, bottom, right, top) – origin is bottom‑left.
        Rectangle bounds = new Rectangle(50, 700, 300, 800);
```

*Hệ thống tọa độ sử dụng đơn vị điểm (1 pt = 1/72 inch). Ví dụ tạo một hình chữ nhật rộng 250 pt và cao 100 pt gần phần trên của trang. Điều chỉnh các số để phù hợp với bố cục của bạn.*

---

## Step 4: Create the rectangle shape

```csharp
        // Create a rectangle shape with the defined bounds.
        Rectangle rectangleShape = new Rectangle(bounds)
        {
            // Optional styling – a semi‑transparent blue fill.
            FillColor = Color.FromRgb(0, 120, 215),
            FillOpacity = 0.4,

            // Optional border – 2 pt thick, dark gray.
            Border = new Border
            {
                Width = 2,
                Color = Color.FromRgb(50, 50, 50)
            }
        };
```

*Lớp `Rectangle` kế thừa từ `GraphicalObject`. Việc đặt `FillColor` và `Border` là tùy chọn, nhưng nó minh họa cách kiểm soát giao diện khi bạn **vẽ hình dạng trong PDF C#** vượt ra ngoài một đường viền đơn giản.*

---

## Step 5: Add the rectangle to the page

```csharp
        // Add the rectangle shape to the page's paragraph collection.
        firstPage.Paragraphs.Add(rectangleShape);
```

*Các đoạn văn (`Paragraphs`) là container cho bất kỳ đối tượng có thể vẽ nào. Bằng cách chèn hình dạng vào `Paragraphs`, Aspose.Pdf sẽ render nó khi tài liệu được lưu.*

---

## Step 6: Save the modified PDF

```csharp
        // Save the updated PDF to a new file.
        pdfDoc.Save("output.pdf");

        // Inform the user.
        Console.WriteLine("Rectangle added and saved to output.pdf");
    }
}
```

*Việc lưu tạo ra một tệp mới để tệp `input.pdf` gốc không bị thay đổi. Bạn có thể ghi đè lên tệp nguồn bằng cách truyền cùng một đường dẫn, nhưng việc giữ bản sao lưu là thực hành tốt nhất.*

---

## Full source code (runnable)

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using System.Drawing;   // For Color struct

class Program
{
    static void Main()
    {
        // Step 1: Load the PDF document
        Document pdfDoc = new Document("input.pdf");

        // Step 2: Get the first page (pages are 1‑based)
        Page firstPage = pdfDoc.Pages[1];

        // Step 3: Define rectangle bounds (left, bottom, right, top)
        Rectangle bounds = new Rectangle(50, 700, 300, 800);

        // Step 4: Create a rectangle shape with optional styling
        Rectangle rectangleShape = new Rectangle(bounds)
        {
            FillColor = Color.FromArgb(102, 0, 120, 215), // 40 % opacity blue
            FillOpacity = 0.4,
            Border = new Border
            {
                Width = 2,
                Color = Color.FromRgb(50, 50, 50)
            }
        };

        // Step 5: Add the rectangle shape to the page
        firstPage.Paragraphs.Add(rectangleShape);

        // Step 6: Save the modified PDF
        pdfDoc.Save("output.pdf");

        Console.WriteLine("Rectangle added to PDF successfully.");
    }
}
```

**Kết quả mong đợi** – Mở `output.pdf` trong bất kỳ trình xem PDF nào. Bạn sẽ thấy một hình chữ nhật được tô màu xanh dương gần góc trên‑phải của trang đầu tiên, được viền bằng màu xám đậm.

---

## Cách vẽ hình dạng trong PDF C# trên nhiều trang

Nếu bạn cần **thêm hình chữ nhật vào PDF** trên mỗi trang, hãy lặp qua bộ sưu tập `Pages`:

```csharp
foreach (Page page in pdfDoc.Pages)
{
    Rectangle rect = new Rectangle(50, 700, 300, 800);
    Rectangle shape = new Rectangle(rect)
    {
        FillColor = Color.FromArgb(80, 255, 0, 0), // semi‑transparent red
        Border = new Border { Width = 1, Color = Color.Black }
    };
    page.Paragraphs.Add(shape);
}
```

*Mẫu này tái sử dụng cùng một giới hạn trên mỗi trang. Điều chỉnh tọa độ cho mỗi trang nếu bạn cần vị trí khác nhau.*

---

## Những lỗi thường gặp và mẹo thực hành tốt

| Vấn đề | Nguyên nhân | Cách khắc phục |
|-------|-------------|----------------|
| Hình chữ nhật xuất hiện ngoài trang | Tọa độ được đo từ góc dưới‑trái; việc sử dụng hệ thống tọa độ hướng từ trên có thể gây nhầm lẫn. | Nhớ rằng trục Y tăng lên phía trên. Sử dụng các giá trị phù hợp với kích thước trang (`page.PageInfo.Width`, `page.PageInfo.Height`). |
| Hình dạng không hiển thị | Độ trong suốt của Fill được đặt thành `0` hoặc độ rộng viền được đặt thành `0`. | Đảm bảo `FillOpacity` lớn hơn `0` và `Border.Width` ít nhất là `0.5`. |
| Lưu gây ra `AccessDeniedException` | Tệp đầu ra đang mở trong chương trình khác. | Đóng mọi trình xem trước khi chạy mã, hoặc lưu vào đường dẫn khác. |
| Hình chữ nhật chồng lên nội dung hiện có | Không có kiểm soát lớp (layering) được thiết lập. | Sử dụng thuộc tính `ZIndex` (giá trị cao hơn sẽ được vẽ lên trên) nếu bạn cần kiểm soát lớp. |

---

## Mở rộng hình chữ nhật – gradient, xoay và độ trong suốt

Aspose.Pdf hỗ trợ đồ họa nâng cao. Để tạo một hình chữ nhật xoay với gradient tuyến tính:

```csharp
Rectangle gradientRect = new Rectangle(bounds)
{
    // Gradient fill from left (blue) to right (green)
    FillColor = Color.Blue,
    FillColor2 = Color.Green,
    FillMode = FillMode.LinearGradient,
    // Rotate 45 degrees around the rectangle's center
    Rotation = 45
};
firstPage.Paragraphs.Add(gradientRect);
```

*Mẫu mã tương tự minh họa **cách vẽ hình dạng trong PDF C#** với các hiệu ứng hình ảnh phong phú hơn.*

---

## Xác minh kết quả bằng chương trình

Bạn có thể xác nhận rằng hình chữ nhật đã được thêm bằng cách kiểm tra số lượng đoạn văn của trang:

```csharp
int shapeCount = firstPage.Paragraphs.Count;
Console.WriteLine($"Page 1 now contains {shapeCount} paragraph objects.");
```

Nếu số lượng đoạn văn tăng lên một sau khi chèn, thao tác đã thành công.

---

## Kết luận

Bây giờ bạn đã biết cách **thêm hình chữ nhật vào PDF** bằng C#. Bài hướng dẫn đã bao gồm việc tải tài liệu, định nghĩa giới hạn, tạo hình chữ nhật, chèn nó vào một trang và lưu kết quả. Bạn cũng đã thấy cách xử lý nhiều trang, tránh các lỗi thường gặp và áp dụng kiểu dáng nâng cao.

Tiếp theo, hãy khám phá các chủ đề liên quan như **cách vẽ hình dạng trong PDF C#** cho vòng tròn, đa giác hoặc đường tự do, và học cách kết hợp các hình dạng với văn bản và hình ảnh để tạo ra các báo cáo PDF đầy đủ tính năng.

Chúc lập trình vui vẻ!

## Bạn nên học gì tiếp theo?

Các hướng dẫn sau đây bao gồm các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh có thể chạy được cùng với các giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [How to Add Page Stamps in PDFs Using Aspose.PDF for .NET | Watermarks & Backgrounds Guide](/pdf/english/net/watermarks-backgrounds/implement-page-stamps-aspose-pdf-dotnet/)
- [How to Add an Image Stamp to a PDF Using Aspose.PDF for .NET: A Comprehensive Guide](/pdf/english/net/images-graphics/add-image-stamp-pdf-aspose-dotnet/)
- [How to Add a Rotating Image Watermark to PDFs Using Aspose.PDF for .NET](/pdf/english/net/watermarks-backgrounds/add-rotating-image-watermark-aspose-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}