---
category: general
date: 2026-08-20
description: Tạo trạng thái đồ họa tùy chỉnh trong PDF với Aspose.Pdf. Tìm hiểu cách
  chỉnh sửa tài nguyên PDF và thêm độ trong suốt vào PDF chỉ trong vài bước.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create custom graphics state
- edit pdf resources
- add transparency pdf
- Aspose.Pdf graphics state
- PDF resource dictionary
language: vi
lastmod: 2026-08-20
og_description: Tạo trạng thái đồ họa tùy chỉnh trong PDF với Aspose.Pdf. Hướng dẫn
  này cho thấy cách chỉnh sửa tài nguyên PDF và nhanh chóng thêm độ trong suốt vào
  PDF.
og_image_alt: Screenshot of C# code that creates a custom graphics state in a PDF
og_title: Tạo trạng thái đồ họa tùy chỉnh trong PDF – Hướng dẫn Aspose.Pdf
schemas:
- author: Aspose
  dateModified: '2026-08-20'
  description: Create custom graphics state in PDF with Aspose.Pdf. Learn how to edit
    PDF resources and add transparency PDF in just a few steps.
  headline: Create custom graphics state in PDF using Aspose.Pdf
  type: TechArticle
tags:
- PDF
- Aspose.Pdf
- C#
- Graphics state
title: Tạo trạng thái đồ họa tùy chỉnh trong PDF bằng Aspose.Pdf
url: /vi/net/programming-with-operators/create-custom-graphics-state-in-pdf-using-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo trạng thái đồ họa tùy chỉnh trong PDF bằng Aspose.Pdf

Nếu bạn cần **tạo trạng thái đồ họa tùy chỉnh** trong một PDF, hướng dẫn này sẽ cho bạn thấy chính xác cách thực hiện với Aspose.Pdf cho .NET. Khi kết thúc tutorial, bạn sẽ có thể **chỉnh sửa tài nguyên PDF**, chèn một dictionary trạng thái đồ họa mới, và **thêm nội dung PDF trong suốt** mà không rời khỏi dự án C# của mình.

Bạn sẽ thấy một ví dụ hoàn chỉnh, có thể chạy được, giải thích tại sao mỗi dòng lại quan trọng, và các mẹo để xử lý tài liệu đa trang hoặc các chế độ hòa trộn khác nhau. Không cần công cụ bên ngoài—chỉ cần thư viện Aspose.Pdf và môi trường phát triển .NET cơ bản.

## Yêu cầu trước

* .NET 6.0 hoặc mới hơn (mã cũng hoạt động với .NET Framework 4.7+)
* Một bản sao có giấy phép của **Aspose.Pdf for .NET** (bản dùng thử miễn phí hoạt động cho việc thử nghiệm)
* Một tệp PDF đầu vào có tên `input.pdf` đặt trong thư mục bạn có thể tham chiếu từ mã
* Visual Studio 2022 hoặc bất kỳ IDE nào hỗ trợ phát triển C#

Tutorial giả định rằng bạn đã quen với cú pháp C# cơ bản và khái niệm về các trang PDF.

## Bước 1: Tải PDF nguồn và truy cập trang đầu tiên

Hoạt động đầu tiên là mở tệp PDF và lấy trang mà bạn muốn chỉnh sửa tài nguyên. Aspose.Pdf đại diện cho mỗi trang dưới dạng đối tượng `Page`, và mỗi trang chứa một **dictionary tài nguyên** lưu trữ các trạng thái đồ họa, phông chữ, XObjects và hơn nữa.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Operators;
using Aspose.Pdf.InteractiveFeatures;
using Aspose.Pdf.Text;
using Aspose.Pdf.Facades;
using System.Collections.Generic;

// Load the PDF you want to edit
using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
{
    // Get the first page (pages are 1‑based in Aspose.Pdf)
    Page firstPage = pdfDocument.Pages[1];
```

*Tiêu sao điều này quan trọng:* Lớp `Document` tải tệp vào bộ nhớ, và `Pages[1]` cung cấp cho bạn quyền truy cập trực tiếp vào dictionary tài nguyên của trang đầu tiên, nơi mà một trạng thái đồ họa được lưu.

## Bước 2: Mở dictionary tài nguyên để chỉnh sửa

Aspose.Pdf cung cấp một trợ giúp `DictionaryEditor` cho phép bạn xử lý một dictionary tài nguyên như một `Dictionary` .NET thông thường. Điều này giúp dễ dàng đọc, thêm hoặc thay thế các mục như `ExtGState`.

```csharp
    // Create an editor for the page’s resources
    var resourcesEditor = new DictionaryEditor(firstPage.Resources);
```

*Tiêu sao điều này quan trọng:* `DictionaryEditor` trừu tượng hoá các đối tượng COS cấp thấp, cho phép bạn làm việc với các cặp khóa/giá trị quen thuộc trong khi vẫn duy trì tuân thủ PDF.

## Bước 3: Lấy (hoặc tạo) dictionary ExtGState

Mục **ExtGState** chứa tất cả các đối tượng trạng thái đồ họa bên ngoài cho trang. Nếu dictionary không tồn tại, Aspose.Pdf sẽ tạo một dictionary rỗng cho bạn.

```csharp
    // Ensure the ExtGState dictionary exists
    var extGStateDict = resourcesEditor.ContainsKey("ExtGState")
        ? resourcesEditor["ExtGState"].ToCosPdfDictionary()
        : new CosPdfDictionary(pdfDocument);
```

*Tiêu sao điều này quan trọng:* Một mục `ExtGState` thiếu sẽ gây ra `KeyNotFoundException` sau này. Điều này bảo vệ cho mã hoạt động trên các PDF chưa bao giờ định nghĩa trạng thái đồ họa tùy chỉnh—một phần thiết yếu của độ bền **chỉnh sửa tài nguyên PDF**.

## Bước 4: Xây dựng dictionary trạng thái đồ họa tùy chỉnh

Một trạng thái đồ họa mô tả cách các thao tác vẽ được hiển thị. Để **thêm PDF trong suốt**, bạn cần đặt các mục `ca` (độ trong suốt tô) và `CA` (độ trong suốt nét) và tùy chọn một chế độ hòa trộn (`BM`). Đoạn mã dưới đây xây dựng một dictionary mới với các tham số đó.

```csharp
    // Create an empty dictionary that will become the new graphics state
    var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

    // Define the parameters you want for the custom state
    var graphicsStateParams = new KeyValuePair<string, ICosPdfPrimitive>[]
    {
        // Stroke opacity (1 = fully opaque)
        new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
        // Fill opacity (0.5 = 50 % transparent)
        new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
        // Blend mode – "Normal" is the default, but you can use "Multiply", "Screen", etc.
        new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
    };

    // Populate the dictionary with the parameters
    foreach (var param in graphicsStateParams)
        newGraphicsState.Add(param);
```

*Tiêu sao điều này quan trọng:* Các mục `ca` và `CA` kiểm soát độ trong suốt cho các thao tác tô và nét, tương ứng. Đặt `BM` cho phép bạn thử nghiệm các hiệu ứng hợp thành khác nhau, hữu ích khi bạn sau này **thêm nội dung PDF trong suốt** như các hình dạng hoặc hình ảnh bán trong suốt.

## Bước 5: Đăng ký trạng thái đồ họa mới dưới một tên duy nhất

Mỗi trạng thái đồ họa trong dictionary `ExtGState` phải có một tên duy nhất (ví dụ, `GS0`, `GS1`). Bạn có thể chọn bất kỳ tên nào không trùng với các mục hiện có.

```csharp
    // Choose a name that is unlikely to collide with existing states
    const string graphicsStateName = "GS0";

    // Add the new graphics state to the ExtGState dictionary
    extGStateDict.Add(graphicsStateName, newGraphicsState);

    // If the ExtGState entry was missing, attach it back to the page resources
    if (!resourcesEditor.ContainsKey("ExtGState"))
        resourcesEditor["ExtGState"] = extGStateDict;
```

*Tiêu sao điều này quan trọng:* Bằng cách chèn dictionary mới dưới `GS0`, bạn làm cho trạng thái có thể được truy cập từ các luồng nội dung của trang. Khối điều kiện đảm bảo mục `ExtGState` tồn tại ngay cả với các PDF bắt đầu mà không có—một biện pháp bảo vệ **chỉnh sửa tài nguyên PDF** khác.

## Bước 6: Sử dụng trạng thái đồ họa tùy chỉnh trong nội dung trang (tùy chọn)

Các bước trước chỉ *định nghĩa* trạng thái đồ họa. Để thực sự thấy hiệu ứng, bạn phải tham chiếu nó trong luồng nội dung của trang. Dưới đây là một ví dụ nhanh vẽ một hình chữ nhật bán trong suốt bằng trạng thái chúng ta vừa tạo.

```csharp
    // Get the page’s content stream (or create a new one if empty)
    var content = firstPage.Contents[1];
    var graphics = new ContentWriter(content);

    // Save current graphics state
    graphics.WriteOperator(OperatorName.SaveState);
    // Set the custom graphics state we just defined
    graphics.WriteOperand($"/{graphicsStateName}");
    graphics.WriteOperator(OperatorName.SetExtGState);
    // Draw a rectangle (coordinates are in points)
    graphics.WriteOperand(100);   // lower‑left x
    graphics.WriteOperand(500);   // lower‑left y
    graphics.WriteOperand(200);   // width
    graphics.WriteOperand(100);   // height
    graphics.WriteOperator(OperatorName.Rectangle);
    // Fill the rectangle using the current fill opacity (ca = 0.5)
    graphics.WriteOperator(OperatorName.Fill);
    // Restore the previous graphics state
    graphics.WriteOperator(OperatorName.RestoreState);
```

*Tiêu sao điều này quan trọng:* Toán tử `SetExtGState` (`gs`) cho trình render PDF biết áp dụng các tham số được định nghĩa trong `GS0`. Hình chữ nhật sẽ hiển thị với độ trong suốt tô 50 % trong khi nét vẫn hoàn toàn không trong suốt.

## Bước 7: Lưu PDF đã chỉnh sửa

Cuối cùng, ghi các thay đổi trở lại đĩa. Bạn có thể ghi đè lên tệp gốc hoặc tạo một tệp mới.

```csharp
    // Save the updated PDF
    pdfDocument.Save("YOUR_DIRECTORY/output_with_custom_gs.pdf");
}
```

Khi bạn mở `output_with_custom_gs.pdf` trong một trình xem PDF, bạn sẽ thấy một hình chữ nhật bán trong suốt trên trang đầu tiên. Điều này xác nhận rằng bạn đã thành công **tạo trạng thái đồ họa tùy chỉnh**, **chỉnh sửa tài nguyên PDF**, và **thêm nội dung PDF trong suốt**.

## Các biến thể phổ biến và trường hợp đặc biệt

| Situation | What to adjust |
|-----------|----------------|
| **Nhiều trang cần cùng một trạng thái** | Đăng ký trạng thái đồ họa một lần (các bước 1‑5) và tham chiếu `GS0` trong luồng nội dung của bất kỳ trang nào. |
| **Độ trong suốt khác nhau cho mỗi phần tử** | Định nghĩa các trạng thái bổ sung (`GS1`, `GS2`, …) với các giá trị `ca`/`CA` khác nhau và chuyển đổi giữa chúng bằng `SetExtGState`. |
| **Chế độ hòa trộn khác Normal** | Thay thế `"Normal"` bằng `"Multiply"`, `"Screen"`, hoặc bất kỳ chế độ hòa trộn tiêu chuẩn PDF nào trong mục `BM`. |
| **Xung đột tên** | Trước khi thêm, kiểm tra `extGStateDict.ContainsKey(yourName)` và chọn hậu tố duy nhất nếu cần. |
| **PDF đã chứa dictionary ExtGState** | Mã trong Bước 3 đã tái sử dụng dictionary hiện có, vì vậy không cần xử lý bổ sung. |

**Mẹo chuyên nghiệp:** Khi làm việc với các PDF lớn, bao bọc việc sử dụng `Document` trong một khối `using` (như đã minh họa) để giải phóng tài nguyên gốc kịp thời. Ngoài ra, hãy cân nhắc bật thuộc tính `PdfCompliance` của Aspose.Pdf nếu bạn cần đảm bảo tuân thủ PDF/A hoặc PDF/X sau khi chỉnh sửa tài nguyên.

## Ví dụ làm việc đầy đủ

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Operators;
using Aspose.Pdf.InteractiveFeatures;
using Aspose.Pdf.Text;
using Aspose.Pdf.Facades;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        // Load the PDF you want to edit
        using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
        {
            // Step 1: Get the first page
            Page firstPage = pdfDocument.Pages[1];

            // Step 2: Open the page resources for editing
            var resourcesEditor = new DictionaryEditor(firstPage.Resources);

            // Step 3: Retrieve or create the ExtGState dictionary
            var extGStateDict = resourcesEditor.ContainsKey("ExtGState")
                ? resourcesEditor["ExtGState"].ToCosPdfDictionary()
                : new CosPdfDictionary(pdfDocument);

            // Step 4: Build a custom graphics state (50 % fill opacity, 100 % stroke opacity)
            var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            var graphicsStateParams = new KeyValuePair<string, ICosPdfPrimitive>[]
            {
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
            };
            foreach (var param in graphicsStateParams)
                newGraphicsState.Add(param);

            // Step 5: Register the graphics state under the name GS0
            const string graphicsStateName = "GS0";
            extGStateDict.Add(graphicsStateName, newGraphics


## Bạn Nên Học Gì Tiếp Theo?

Các tutorial sau đây bao phủ các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã đầy đủ với giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Cách Tạo PDF với Aspose – Thêm Trường Form và Trang](/pdf/english/net/programming-with-forms/how-to-create-pdf-with-aspose-add-form-field-and-pages/)
- [Cách Tạo Bảng Tùy Chỉnh trong PDF bằng Aspose.PDF .NET](/pdf/english/net/tables-lists/create-custom-tables-in-pdfs-aspose-pdf-dot-net/)
- [Tạo Dấu PDF Tùy Chỉnh Aspose Pdf Net](/pdf/hongkong/net/images-graphics/create-custom-pdf-stamps-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}