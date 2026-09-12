---
category: general
date: 2026-09-12
description: Tìm hiểu cách thêm độ trong suốt vào PDF, vẽ hình chữ nhật trên PDF và
  lưu PDF với độ trong suốt bằng Aspose.PDF trong C# – hướng dẫn chi tiết từng bước.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add transparency to pdf
- draw rectangle on pdf
- save pdf with transparency
language: vi
lastmod: 2026-09-12
og_description: Thêm độ trong suốt vào PDF, vẽ một hình chữ nhật trên PDF và lưu PDF
  với độ trong suốt bằng Aspose.PDF trong C#. Tham khảo hướng dẫn đầy đủ này.
og_image_alt: Screenshot of a PDF page showing a semi‑transparent rectangle drawn
  with Aspose.PDF
og_title: Thêm độ trong suốt vào PDF và vẽ hình chữ nhật trên PDF – hướng dẫn C# đầy
  đủ
schemas:
- author: Aspose
  dateModified: '2026-09-12'
  description: Learn how to add transparency to PDF, draw a rectangle on PDF, and
    save PDF with transparency using Aspose.PDF in C# – step‑by‑step guide.
  headline: How to add transparency to PDF and draw a rectangle on PDF with Aspose.PDF
  type: TechArticle
tags:
- Aspose.PDF
- C#
- PDF manipulation
title: Cách thêm độ trong suốt vào PDF và vẽ hình chữ nhật trên PDF bằng Aspose.PDF
url: /vi/net/images-graphics/how-to-add-transparency-to-pdf-and-draw-a-rectangle-on-pdf-w/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách thêm độ trong suốt vào PDF và vẽ hình chữ nhật trên PDF bằng Aspose.PDF

Nếu bạn cần **thêm độ trong suốt vào PDF**, hướng dẫn này sẽ chỉ cho bạn cách thực hiện trong C#. Bạn cũng sẽ học cách **vẽ hình chữ nhật trên PDF** và cuối cùng **lưu PDF với độ trong suốt** để kết quả có thể được tái sử dụng trong báo cáo, hoá đơn, hoặc bất kỳ quy trình tự động hoá tài liệu nào.

Trong tutorial này bạn sẽ:

* Tải một tài liệu PDF hiện có.
* Tạo một graphics state tùy chỉnh định nghĩa độ mờ của nét và màu nền.
* Áp dụng graphics state đó vào canvas và vẽ một hình chữ nhật.
* Lưu tệp đã chỉnh sửa trong khi giữ nguyên các thiết lập độ trong suốt.

Không cần công cụ bên ngoài nào ngoài thư viện Aspose.PDF for .NET, và mỗi dòng mã đều được giải thích để bạn hiểu *tại sao* mỗi bước quan trọng.

## Yêu cầu trước

* .NET 6.0 hoặc mới hơn (mã cũng hoạt động với .NET Framework 4.7+).
* Bản sao có giấy phép hoặc bản dùng thử của **Aspose.PDF for .NET**. Cài đặt qua NuGet:

```bash
dotnet add package Aspose.Pdf
```

* Một file PDF đầu vào (`input.pdf`) đặt trong thư mục bạn có thể tham chiếu từ dự án.

## Bước 1: Tải tài liệu PDF

Hoạt động đầu tiên là mở file nguồn. Sử dụng câu lệnh `using` đảm bảo tài liệu được giải phóng đúng cách, tránh các vấn đề khóa file khi bạn cố lưu lại.

```csharp
// Step 1: Load the PDF document
string pdfPath = @"YOUR_DIRECTORY\input.pdf";
using var pdfDocument = new Aspose.Pdf.Document(pdfPath);
```

*Lý do quan trọng*: Việc tải tài liệu cho phép bạn truy cập vào bộ sưu tập trang, từ điển tài nguyên và các đối tượng canvas cần thiết cho việc vẽ.

## Bước 2: Truy cập từ điển tài nguyên của trang đầu tiên

Mỗi trang PDF có một **resource dictionary** lưu trữ các đối tượng như phông chữ, hình ảnh và graphics state. Để thêm một thiết lập độ trong suốt mới, chúng ta cần chỉnh sửa mục `ExtGState`.

```csharp
// Step 2: Access the first page and its resource dictionary
var firstPage = pdfDocument.Pages[1];               // PDF pages are 1‑based
var resourcesEditor = new Aspose.Pdf.DictionaryEditor(firstPage.Resources);
```

*Lý do quan trọng*: `DictionaryEditor` cho phép chúng ta đọc và sửa các đối tượng PDF mức thấp mà không làm hỏng cấu trúc tài liệu.

## Bước 3: Tạo graphics state tùy chỉnh với các giá trị độ trong suốt

Một graphics state (`ExtGState`) kiểm soát cách các thao tác vẽ được hiển thị. Chúng ta định nghĩa hai tham số độ mờ:

* **CA** – độ mờ của nét (đường viền của hình).
* **ca** – độ mờ của màu nền (bên trong hình).

Chúng ta cũng đặt chế độ hòa trộn (`BM`) thành “Normal”, là thao tác kết hợp phổ biến nhất.

```csharp
// Step 3: Create a custom graphics state (ExtGState) with transparency settings
var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
var customGs = Aspose.Pdf.Cos.CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

var parameters = new[]
{
    new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
        "CA", new Aspose.Pdf.Cos.CosPdfNumber(1)),          // stroke opacity = 100 %
    new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
        "ca", new Aspose.Pdf.Cos.CosPdfNumber(0.5)),        // fill opacity = 50 %
    new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
        "BM", new Aspose.Pdf.Cos.CosPdfName("Normal"))      // normal blend mode
};

foreach (var p in parameters)
    customGs.Add(p);

// Register the new graphics state under the name "GS0"
extGStateDict.Add("GS0", customGs);
```

*Lý do quan trọng*: Bằng cách thêm `GS0` vào từ điển `ExtGState`, chúng ta tạo một tham chiếu có thể tái sử dụng mà canvas có thể kích hoạt trước khi vẽ. Độ mờ nền `0.5` làm cho hình chữ nhật bán trong suốt, đạt được mục tiêu **thêm độ trong suốt vào PDF**.

## Bước 4: Áp dụng graphics state và vẽ hình chữ nhật

Bây giờ chúng ta yêu cầu canvas của trang sử dụng graphics state vừa tạo, sau đó vẽ một hình chữ nhật. Các tọa độ tuân theo hệ tọa độ PDF (gốc ở góc dưới‑trái).

```csharp
// Step 4: Apply the custom graphics state and draw a rectangle
var canvas = firstPage.Canvas;

// Activate the transparency graphics state
canvas.SetGraphicsState("GS0");

// Draw a rectangle from (100, 500) to (200, 600)
canvas.Rectangle(100, 500, 200, 600);

// Render the rectangle outline using the current graphics state
canvas.Stroke();
```

*Lý do quan trọng*: `SetGraphicsState("GS0")` chuyển ngữ cảnh vẽ sang các thiết lập độ trong suốt đã định nghĩa trước. Phương thức `Rectangle` xác định hình dạng, và `Stroke` vẽ đường viền với độ mờ đã chỉ định. Nếu bạn muốn hình chữ nhật có màu nền, thay `Stroke()` bằng `FillAndStroke()`.

## Bước 5: Lưu PDF đã chỉnh sửa trong khi giữ độ trong suốt

Cuối cùng, ghi tài liệu trở lại đĩa. File đầu ra chứa graphics state mới, hình chữ nhật đã vẽ, và thông tin độ trong suốt.

```csharp
// Step 5: Save the modified PDF
string outputPath = @"YOUR_DIRECTORY\output_with_extgstate.pdf";
pdfDocument.Save(outputPath);
```

*Lý do quan trọng*: Việc lưu tài liệu hoàn thiện mọi thay đổi. File kết quả có thể mở bằng bất kỳ trình xem PDF nào, và hình chữ nhật sẽ hiển thị với độ mờ nền 50 %.

### Kết quả mong đợi

Khi bạn mở `output_with_extgstate.pdf` bạn sẽ thấy một hình chữ nhật có viền hoàn toàn không trong suốt và phần bên trong bán trong suốt, cho phép nội dung trang nền hiện ra phía sau.

## Các trường hợp đặc biệt và mẹo thực tế

| Tình huống | Điều chỉnh đề xuất |
|-----------|--------------------|
| **Nhiều trang** | Lặp qua `pdfDocument.Pages` và lặp lại các bước 2‑4 cho mỗi trang mục tiêu. |
| **Giá trị độ trong suốt khác nhau** | Thay đổi giá trị `CosPdfNumber` cho `CA` (nét) và `ca` (nền) thành bất kỳ số nào từ `0` (hoàn toàn trong suốt) tới `1` (hoàn toàn không trong suốt). |
| **Chế độ hòa trộn tùy chỉnh** | Thay `"Normal"` bằng `"Multiply"`, `"Screen"` hoặc bất kỳ chế độ hòa trộn chuẩn PDF nào được trình xem hỗ trợ. |
| **Hình chữ nhật có màu nền** | Gọi `canvas.FillAndStroke()` thay vì `canvas.Stroke()` để áp dụng cả màu nền và viền. |
| **Tái sử dụng cùng một graphics state** | Bạn có thể gọi `canvas.SetGraphicsState("GS0")` trước khi vẽ bất kỳ số lượng hình nào trên cùng một trang. |

**Mẹo chuyên nghiệp:** Luôn kiểm tra resource dictionary sau khi thêm một `ExtGState` mới. Nếu dictionary chưa tồn tại, hãy tạo nó trước:

```csharp
if (!resourcesEditor.ContainsKey("ExtGState"))
    resourcesEditor.Add("ExtGState", new Aspose.Pdf.Cos.CosPdfDictionary(pdfDocument));
```

## Ví dụ đầy đủ, có thể chạy

Dưới đây là một chương trình tự chứa mà bạn có thể sao chép vào ứng dụng console và chạy ngay (thay `YOUR_DIRECTORY` bằng đường dẫn thực tế).

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Cos;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the PDF document
        string pdfPath = @"YOUR_DIRECTORY\input.pdf";
        using var pdfDocument = new Document(pdfPath);

        // 2️⃣ Access the first page’s resources
        var firstPage = pdfDocument.Pages[1];
        var resourcesEditor = new DictionaryEditor(firstPage.Resources);

        // Ensure ExtGState dictionary exists
        if (!resourcesEditor.ContainsKey("ExtGState"))
            resourcesEditor.Add("ExtGState", new CosPdfDictionary(pdfDocument));

        // 3️⃣ Create a custom graphics state with transparency
        var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
        var customGs = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

        var parameters = new[]
        {
            new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),   // stroke opacity
            new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // fill opacity
            new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
        };

        foreach (var p in parameters)
            customGs.Add(p);

        extGStateDict.Add("GS0", customGs);

        // 4️⃣ Apply the graphics state and draw a rectangle
        var canvas = firstPage.Canvas;
        canvas.SetGraphicsState("GS0");
        canvas.Rectangle(100, 500, 200, 600);
        canvas.Stroke(); // use FillAndStroke() for a filled shape

        // 5️⃣ Save the PDF with transparency
        string outputPath = @"YOUR_DIRECTORY\output_with_extgstate.pdf";
        pdfDocument.Save(outputPath);

        Console.WriteLine("PDF saved with a transparent rectangle at: " + outputPath);
    }
}
```

Chạy chương trình sẽ tạo ra `output_with_extgstate.pdf`, minh họa **thêm độ trong suốt vào PDF**, **vẽ hình chữ nhật trên PDF**, và **lưu PDF với độ trong suốt** trong một luồng duy nhất.

## Kết luận

Bạn đã biết cách **thêm độ trong suốt vào PDF**, **vẽ hình chữ nhật trên PDF**, và **lưu PDF với độ trong suốt** bằng Aspose.PDF for .NET. Quy trình xoay quanh việc tạo một `ExtGState` tùy chỉnh, áp dụng nó vào canvas, và lưu các thay đổi. Với những khối xây dựng này, bạn có thể mở rộng kỹ thuật sang các hình dạng khác, nhiều trang, hoặc giá trị độ trong suốt động.

**Các bước tiếp theo**

* Khám phá các primitive vẽ khác như `canvas.Ellipse`, `canvas.Path`, hoặc `canvas.TextFragment` trong khi tái sử dụng cùng một graphics state.
* Kết hợp độ trong suốt với lớp phủ hình ảnh để tạo watermark (`canvas.Image` + `ExtGState` tùy chỉnh).
* Xem tài liệu Aspose.PDF về **graphics state parameters** để biết các hiệu ứng kết hợp nâng cao.

Chúc bạn lập trình vui vẻ, và tận hưởng sự linh hoạt về hình ảnh mà độ trong suốt mang lại cho quy trình làm việc với PDF của bạn!

## Bạn nên học gì tiếp theo?

Các tutorial sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên đều bao gồm mã mẫu đầy đủ với các giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [How to Create PDF in C# – Add Page, Draw Rectangle & Save](/pdf/english/net/document-creation/how-to-create-pdf-in-c-add-page-draw-rectangle-save/)
- [How to Add a Line Object in PDF Using Aspose.PDF for .NET: A Step-by-Step Guide](/pdf/english/net/document-manipulation/add-line-aspose-pdf-dotnet-tutorial/)
- [Add Image Stamps to PDFs Using Aspose.PDF for .NET: A Step-by-Step Guide](/pdf/english/net/images-graphics/add-image-stamp-to-pdf-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}