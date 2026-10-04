---
category: general
date: 2026-10-01
description: Thêm ExtGState tùy chỉnh vào PDF bằng Aspose.PDF để thiết lập độ trong
  suốt nhanh chóng. Hãy làm theo hướng dẫn này để tìm hiểu cách thiết lập độ trong
  suốt PDF với trạng thái đồ họa tùy chỉnh.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add custom extgstate pdf
- how to set transparency pdf
- Aspose.PDF graphics state
- PDF opacity settings
- PDF blend mode tutorial
language: vi
lastmod: 2026-10-01
og_description: Thêm ExtGState tùy chỉnh vào PDF và học cách thiết lập độ trong suốt
  cho PDF chỉ trong vài dòng C#. Hướng dẫn này bao gồm mọi bước từ việc tải tệp đến
  lưu kết quả.
og_image_alt: Screenshot of a PDF page showing transparent graphics after adding a
  custom ExtGState
og_title: Thêm ExtGState tùy chỉnh vào PDF – hướng dẫn đầy đủ Aspose.PDF
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Add custom ExtGState PDF using Aspose.PDF to set transparency PDF quickly.
    Follow this guide to learn how to set transparency PDF with a custom graphics
    state.
  headline: Add custom ExtGState PDF with Aspose.PDF – step‑by‑step guide
  type: TechArticle
tags:
- PDF
- Aspose.PDF
- C#
- GraphicsState
title: Thêm ExtGState tùy chỉnh vào PDF với Aspose.PDF – hướng dẫn từng bước
url: /vi/net/images-graphics/add-custom-extgstate-pdf-with-aspose-pdf-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Thêm ExtGState PDF tùy chỉnh với Aspose.PDF – hướng dẫn từng bước

Nếu bạn cần **thêm ExtGState PDF tùy chỉnh** để kiểm soát độ trong suốt và chế độ hòa trộn, hướng dẫn này sẽ chỉ cho bạn cách thực hiện. Bạn sẽ thấy một ví dụ hoàn chỉnh, có thể chạy được, minh họa **cách thiết lập độ trong suốt PDF** bằng Aspose.PDF cho .NET.

Trong các phần tiếp theo, chúng tôi sẽ giới thiệu gói NuGet cần thiết, phân tích mã từng bước, và các mẹo xử lý các trường hợp đặc biệt như nhiều trang hoặc chế độ hòa trộn tùy chỉnh. Khi kết thúc, bạn sẽ có thể chỉnh sửa bất kỳ PDF nào hiện có và áp dụng trạng thái đồ họa trong suốt mà không rời khỏi IDE.

## Yêu cầu trước

- .NET 6.0 trở lên (mã cũng hoạt động với .NET Framework 4.7+)
- Visual Studio 2022 (hoặc bất kỳ trình chỉnh sửa C# nào bạn thích)
- Gói NuGet **Aspose.PDF for .NET** (phiên bản 23.12 hoặc mới hơn)
- Một tệp PDF mẫu có tên `input.pdf` đặt trong thư mục bạn có thể tham chiếu từ dự án

> **Mẹo chuyên nghiệp:** Sử dụng thư mục “Resources” riêng trong giải pháp của bạn để giữ các PDF đầu vào và đầu ra cùng nhau. Điều này tránh các lỗi liên quan đến đường dẫn khi mã chạy.

## Cài đặt Aspose.PDF

Mở console NuGet Package Manager và chạy:

```bash
dotnet add package Aspose.PDF
```

Gói này cung cấp các lớp `Aspose.Pdf.Document`, `CosPdfDictionary`, và các lớp liên quan được sử dụng trong mẫu mã.

## Bước 1 – Tải tài liệu PDF

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Operators;
using Aspose.Pdf.Text;

// Load the source PDF
using var pdfDocument = new Document("Resources/input.pdf");
```

**Tại sao bước này quan trọng:**  
`Document` đại diện cho toàn bộ tệp PDF trong bộ nhớ. Mở nó bằng khối `using` đảm bảo rằng tất cả tài nguyên không quản lý được giải phóng sau khi chúng ta hoàn thành xử lý.

## Bước 2 – Truy cập từ điển tài nguyên của trang đầu tiên

```csharp
// Get the first page (pages are 1‑based in Aspose.PDF)
Page firstPage = pdfDocument.Pages[1];

// The resource dictionary holds objects like fonts, XObjects, and ExtGState entries
var resourcesEditor = new DictionaryEditor(firstPage.Resources);
```

**Giải thích:**  
Mỗi trang PDF có một từ điển *Resources* nhóm các đối tượng có thể tái sử dụng. Bằng cách chỉnh sửa từ điển này, chúng ta có thể chèn một trạng thái đồ họa mới mà trang có thể tham chiếu sau này.

## Bước 3 – Lấy (hoặc tạo) từ điển ExtGState

```csharp
// Try to get the existing ExtGState dictionary; create one if it does not exist
CosPdfDictionary extGStateDict;
if (resourcesEditor.ContainsKey("ExtGState"))
{
    extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
}
else
{
    extGStateDict = new CosPdfDictionary(pdfDocument);
    resourcesEditor.Add("ExtGState", extGStateDict);
}
```

**Tại sao chúng ta kiểm tra trước:**  
Một số PDF đã định nghĩa mục `ExtGState`. Thêm một mục trùng sẽ ghi đè các trạng thái hiện có và có thể làm hỏng nội dung khác. Đoạn mã phòng thủ này giữ nguyên các mục gốc.

## Bước 4 – Xây dựng trạng thái đồ họa tùy chỉnh

```csharp
// Create an empty dictionary that will become our custom graphics state
CosPdfDictionary newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

// Define the graphics state entries
var graphicsStateEntries = new[]
{
    // CA – stroke opacity (range 0‑1)
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),
    // ca – fill opacity (range 0‑1)
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
    // BM – blend mode (Normal, Multiply, Screen, etc.)
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
};

// Add each entry to the dictionary
foreach (var entry in graphicsStateEntries)
{
    newGraphicsState.Add(entry);
}
```

**Mỗi khóa có chức năng gì:**

| Khóa | Ý nghĩa | Giá trị điển hình |
|------|----------|-------------------|
| `CA` | Độ trong suốt nét vẽ | `0.0` (hoàn toàn trong suốt) → `1.0` (độ đục) |
| `ca` | Độ trong suốt tô | Cùng phạm vi như `CA` |
| `BM` | Chế độ hòa trộn | `Normal`, `Multiply`, `Screen`, `Overlay`, etc. |

Bằng cách đặt `ca` thành `0.5` chúng ta làm cho các hình dạng được tô 50 % trong suốt, trong khi `CA` vẫn hoàn toàn không trong suốt cho các nét vẽ. Thay đổi `BM` cho phép bạn thử nghiệm các hiệu ứng hòa trộn giống Photoshop.

## Bước 5 – Đăng ký trạng thái đồ họa tùy chỉnh dưới một tên duy nhất

```csharp
// Choose a unique name for the new state, e.g., "GS0"
extGStateDict.Add("GS0", newGraphicsState);
```

**Quy tắc đặt tên:**  
Các đặc tả PDF khuyến nghị các định danh ngắn, viết hoa. Sử dụng `GS0` (Graphics State 0) làm cho tên dễ tham chiếu từ các luồng nội dung.

## Bước 6 – Áp dụng trạng thái đồ họa tùy chỉnh trong luồng nội dung (tùy chọn)

Nếu bạn muốn vẽ một hình chữ nhật trong suốt trên trang đầu tiên, bạn có thể chèn trước các toán tử sau:

```csharp
// Build the content stream that uses the new graphics state
var content = new Operator[]
{
    new Operator("q"),                 // Save graphics state
    new Operator("GS0", "gs"),         // Set our custom ExtGState
    new Operator("0.5 0.5 1 rg"),      // Set fill color (light blue)
    new Operator("100 500 200 100 re"),// Rectangle (x, y, width, height)
    new Operator("f"),                 // Fill the rectangle using the fill opacity
    new Operator("Q")                  // Restore graphics state
};

// Add the operators to the page's content
firstPage.Contents.Add(content);
```

**Tại sao bước này là tùy chọn:**  
Các bước trước chỉ *định nghĩa* trạng thái đồ họa. Để thấy hiệu ứng, bạn phải tham chiếu nó từ luồng nội dung của một trang. Đoạn mã trên minh họa một trường hợp sử dụng thực tế, nhưng bạn cũng có thể áp dụng trạng thái này cho các lệnh vẽ hiện có trong PDF của mình.

## Bước 7 – Lưu PDF đã chỉnh sửa

```csharp
// Persist the changes to a new file
pdfDocument.Save("Resources/output.pdf");
```

Khi bạn mở `output.pdf` bạn sẽ thấy hình chữ nhật được vẽ với độ trong suốt tô 50 % trong khi viền của nó vẫn hoàn toàn không trong suốt — chính là kết quả của **cách thiết lập độ trong suốt PDF** bằng cách sử dụng ExtGState tùy chỉnh.

## Xử lý nhiều trang

Nếu bạn cần cùng hiệu ứng trong suốt trên mọi trang, hãy lặp qua `pdfDocument.Pages` và lặp lại **Bước 2**‑**Bước 5** cho tài nguyên của mỗi trang. Hãy cẩn thận chỉ thêm trạng thái đồ họa một lần cho mỗi trang; việc tái sử dụng cùng một từ điển trên nhiều trang không được cho phép theo đặc tả PDF.

```csharp
foreach (Page page in pdfDocument.Pages)
{
    var editor = new DictionaryEditor(page.Resources);
    // Ensure ExtGState exists, then add GS0 as shown earlier
    // (code omitted for brevity)
}
```

## Những lỗi thường gặp và cách tránh

| Triệu chứng | Nguyên nhân | Cách khắc phục |
|------------|-------------|----------------|
| Không có thay đổi độ trong suốt | Giá trị `ca` hoặc `CA` nằm ngoài phạm vi 0‑1 | Sử dụng giá trị thập phân trong khoảng `0.0` đến `1.0`. |
| Nội dung biến mất | Trạng thái đồ họa không được áp dụng (thiếu toán tử `gs`) | Chèn `GS0 gs` trước các lệnh vẽ. |
| PDF không mở được | Khóa trùng trong từ điển `ExtGState` | Kiểm tra `extGStateDict.ContainsKey("GS0")` trước khi thêm. |
| Chế độ hòa trộn bị bỏ qua | Trình xem không hỗ trợ chế độ đã chỉ định | Sử dụng các chế độ tiêu chuẩn như `Normal`, `Multiply`. |

## Ví dụ đầy đủ có thể chạy

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Operators;
using Aspose.Pdf.Text;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        // Load the PDF
        using var pdfDocument = new Document("Resources/input.pdf");

        // Work with the first page
        Page firstPage = pdfDocument.Pages[1];
        var resourcesEditor = new DictionaryEditor(firstPage.Resources);

        // Ensure ExtGState dictionary exists
        CosPdfDictionary extGStateDict;
        if (resourcesEditor.ContainsKey("ExtGState"))
            extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
        else
        {
            extGStateDict = new CosPdfDictionary(pdfDocument);
            resourcesEditor.Add("ExtGState", extGStateDict);
        }

        // Create custom graphics state
        CosPdfDictionary newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
        var entries = new[]
        {
            new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),
            new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
            new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
        };
        foreach (var e in entries) newGraphicsState.Add(e);

        // Register under a unique name
        extGStateDict.Add("GS0", newGraphicsState);

        // Optional: draw a transparent rectangle
        var ops = new Operator[]
        {
            new Operator("q"),
            new Operator("GS0", "gs"),
            new Operator("0.5 0.5 1 rg"),
            new Operator("100 500 200 100 re"),
            new Operator("f"),
            new Operator("Q")
        };
        firstPage.Contents.Add(ops);

        // Save result
        pdfDocument.Save("Resources/output.pdf");
    }
}
```

**Kết quả mong đợi:**  
Mở `output.pdf` hiển thị một hình chữ nhật màu xanh nhạt tại tọa độ (100, 500) với độ trong suốt tô 50 %. Viền của hình chữ nhật vẫn hoàn toàn không trong suốt vì `CA` được đặt là `1.0`.

## Kết luận

Bây giờ bạn đã biết cách **thêm các đối tượng ExtGState PDF tùy chỉnh** với Aspose.PDF và kiểm soát chính xác độ trong suốt và chế độ hòa trộn — trả lời câu hỏi phổ biến **cách thiết lập độ trong suốt PDF**. Hướng dẫn đã bao gồm việc tải tài liệu, chỉnh sửa từ điển tài nguyên, định nghĩa trạng thái đồ họa, áp dụng nó và lưu kết quả.

Tiếp theo, bạn có thể khám phá:

- Sử dụng các chế độ hòa trộn khác nhau (`Multiply`, `Screen`) để tạo hiệu ứng sáng tạo.
- Áp dụng ExtGState giống nhau cho các XObject hình ảnh để có logo bán trong suốt.
- Tự động hoá quá trình cho việc chỉnh sửa hàng loạt PDF trong một dịch vụ nền.

Bạn có thể tự do thử nghiệm các giá trị, đổi tên trạng thái đồ họa, hoặc

## Bạn Nên Học Gì Tiếp Theo?

Các hướng dẫn sau đây bao gồm các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh, hoạt động với giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Thêm Độ Trong Suốt vào PDF bằng Aspose – Hướng Dẫn C# Đầy Đủ](/pdf/english/net/programming-with-operators/add-transparency-to-pdf-using-aspose-complete-c-guide/)
- [Cách Thêm Dấu Trang vào PDF bằng Aspose.PDF cho Java (Hướng Dẫn 2023)](/pdf/english/java/watermarks-backgrounds/add-page-stamp-aspose-pdf-java/)
- [Cách Thêm Dấu Văn Bản vào PDF bằng Aspose.PDF cho Java: Hướng Dẫn Toàn Diện](/pdf/english/java/document-manipulation/aspose-pdf-java-add-text-stamp/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}