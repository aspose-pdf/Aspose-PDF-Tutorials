---
category: general
date: 2026-09-08
description: Thêm độ trong suốt vào PDF với Aspose.PDF cho .NET – học cách thiết lập
  độ trong suốt của nét và màu nền, chế độ hòa trộn, và lưu kết quả trong vài phút.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add transparency to pdf
- aspose.pdf transparency
- pdf graphics state
- extgstate dictionary
- pdf opacity settings
language: vi
lastmod: 2026-09-08
og_description: Thêm độ trong suốt vào PDF bằng Aspose.PDF cho .NET. Hướng dẫn này
  chỉ cách chỉnh sửa từ điển ExtGState, đặt độ mờ và chế độ hòa trộn, và lưu tệp đã
  cập nhật.
og_image_alt: Screenshot of a PDF page showing semi‑transparent shapes created with
  Aspose.PDF
og_title: Thêm độ trong suốt vào PDF với Aspose.PDF – hướng dẫn từng bước
schemas:
- author: Aspose
  dateModified: '2026-09-08'
  description: Add transparency to PDF with Aspose.PDF for .NET – learn to set stroke
    and fill opacity, blend mode, and save the result in minutes.
  headline: How to add transparency to PDF files using Aspose.PDF for .NET
  type: TechArticle
tags:
- PDF
- C#
- Aspose.PDF
title: Cách thêm độ trong suốt vào tệp PDF bằng Aspose.PDF cho .NET
url: /vi/net/images-graphics/how-to-add-transparency-to-pdf-files-using-aspose-pdf-for-ne/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách thêm độ trong suốt vào tệp PDF bằng Aspose.PDF cho .NET

Nếu bạn cần **thêm độ trong suốt vào tài liệu PDF**, hướng dẫn này sẽ chỉ cho bạn cách chỉnh sửa trạng thái đồ họa bằng Aspose.PDF cho .NET. Bạn sẽ học cách đặt độ mờ nét vẽ, độ mờ tô và chế độ hòa trộn trên một trang duy nhất, sau đó lưu kết quả thành tệp mới.

Độ trong suốt là yêu cầu phổ biến cho các dấu watermark, đồ họa phủ lên, hoặc hiệu ứng hình ảnh trong báo cáo. Trong tutorial này, bạn sẽ thấy toàn bộ mã có thể chạy được, hiểu vì sao mỗi lời gọi API quan trọng, và nhận các mẹo xử lý các trường hợp đặc biệt như thiếu mục tài nguyên.

## Những gì bạn cần

Trước khi bắt đầu, hãy chắc chắn rằng bạn có:

* .NET 6.0 hoặc mới hơn (mã cũng hoạt động với .NET Framework 4.6+)
* Giấy phép Aspose.PDF cho .NET hợp lệ (bản dùng thử miễn phí đủ để thử nghiệm)
* Một tệp PDF đầu vào có tên `input.pdf` đặt trong thư mục bạn có thể tham chiếu từ mã
* Môi trường phát triển C# (Visual Studio, Rider, hoặc VS Code)

Không cần thêm bất kỳ gói NuGet nào ngoài `Aspose.Pdf`.

## Tổng quan về trạng thái đồ họa PDF

Trạng thái đồ họa PDF được lưu trong một **dictionary ExtGState** bên trong dictionary tài nguyên của một trang. Mỗi mục định nghĩa các tham số render như độ rộng đường, độ trong suốt và chế độ hòa trộn. Bằng cách tạo một đối tượng trạng thái đồ họa mới và thêm nó vào dictionary `ExtGState`, bạn có thể tái sử dụng cùng một cài đặt độ trong suốt cho nhiều lệnh vẽ.

Hiểu cấu trúc này giúp bạn tránh các bẫy thường gặp, như cố gắng đặt độ trong suốt trực tiếp trên đối tượng `Page` (API không hỗ trợ). Thay vào đó, bạn làm việc với các đối tượng COS cấp thấp, tương ứng một‑một với đặc tả PDF.

## Bước 1: Tải tài liệu PDF

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Operators;
using Aspose.Pdf.Cos;

// Load the source PDF
var pdfDoc = new Document("YOUR_DIRECTORY/input.pdf");
```

*Tại sao lại cần bước này?*  
`Document` là điểm vào cho mọi thao tác với PDF. Việc tải tệp tạo ra một biểu diễn trong bộ nhớ mà bạn có thể chỉnh sửa mà không chạm tới tệp gốc trên đĩa.

## Bước 2: Lấy trang đầu tiên và trình chỉnh sửa dictionary tài nguyên của nó

```csharp
// Retrieve the first page (pages are 1‑based)
var page = pdfDoc.Pages[1];

// The DictionaryEditor provides convenient access to the page’s resources
var resourceEditor = new DictionaryEditor(page.Resources);
```

*Tại sao lại cần bước này?*  
Tất cả các mục trạng thái đồ họa nằm trong tài nguyên của trang. `DictionaryEditor` trừu tượng hoá việc xử lý dictionary COS cấp thấp, cho phép bạn đọc hoặc tạo các mục như `ExtGState`.

## Bước 3: Lấy dictionary ExtGState từ tài nguyên của trang

```csharp
// The ExtGState entry may already exist; if not, create it
CosPdfDictionary extGStateDict;
if (resourceEditor.ContainsKey("ExtGState"))
{
    extGStateDict = (CosPdfDictionary)resourceEditor["ExtGState"].ToCosPdfDictionary();
}
else
{
    // Create a new ExtGState dictionary and attach it to the page resources
    extGStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDoc);
    resourceEditor.Add("ExtGState", extGStateDict);
}
```

*Tại sao lại cần bước này?*  
Một PDF có thể không có dictionary `ExtGState` nào cả. Đoạn mã trên xử lý an toàn cả trường hợp tồn tại và không tồn tại, đảm bảo tutorial hoạt động với bất kỳ PDF đầu vào nào.

## Bước 4: Tạo một dictionary trạng thái đồ họa mới và định nghĩa các mục của nó

```csharp
// Create an empty dictionary that will hold our transparency settings
var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDoc);

// Define the entries:
//   CA – stroke opacity (0 = fully transparent, 1 = opaque)
//   ca – fill opacity
//   BM – blend mode (Normal, Multiply, etc.)
var graphicsStateEntries = new[]
{
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),   // Stroke opacity = 100%
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),   // Fill opacity = 50%
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // Standard blend mode
};

foreach (var entry in graphicsStateEntries)
    newGraphicsState.Add(entry);
```

*Tại sao lại cần bước này?*  
`CA` và `ca` là các toán tử PDF kiểm soát độ trong suốt cho các thao tác vẽ nét (stroke) và không vẽ nét (fill). Đặt `BM` thành `Normal` giữ hành vi hợp thành mặc định, nhưng bạn có thể thử `Multiply` hoặc `Screen` để tạo hiệu ứng nghệ thuật.

## Bước 5: Thêm trạng thái đồ họa mới vào dictionary ExtGState

```csharp
// Choose a unique name for the graphics state (e.g., GS0)
extGStateDict.Add("GS0", newGraphicsState);
```

*Tại sao lại cần bước này?*  
Tên `GS0` trở thành một tham chiếu bạn có thể dùng sau này trong các luồng nội dung (`/GS0 gs`). Thêm nó vào `ExtGState` khiến PDF nhận biết các tham số độ trong suốt mới.

## Bước 6: Áp dụng trạng thái đồ họa trong một luồng nội dung (tùy chọn)

Nếu bạn muốn thấy hiệu ứng ngay lập tức, có thể chèn một lệnh vẽ đơn giản sử dụng trạng thái mới:

```csharp
// Build a content stream that draws a semi‑transparent rectangle
var content = new PageContent();
content.Operators.Add(new Operator("q"));                     // Save graphics state
content.Operators.Add(new Operator("GS0", "gs"));            // Set our custom graphics state
content.Operators.Add(new Operator("0.2", "0.2", "0.8", "rg")); // Set fill color (light blue)
content.Operators.Add(new Operator("100", "500", "200", "100", "re")); // Rectangle
content.Operators.Add(new Operator("f"));                    // Fill
content.Operators.Add(new Operator("Q"));                     // Restore graphics state

// Insert the new content at the beginning of the page
page.Contents.Insert(0, content);
```

*Tại sao lại cần bước này?*  
Đoạn mã tùy chọn minh họa cách trạng thái đồ họa bạn đã thêm (`GS0`) thực sự được sử dụng. Hình chữ nhật sẽ xuất hiện với độ trong suốt tô 50 % trong khi nét vẽ vẫn hoàn toàn không trong suốt.

## Bước 7: Lưu tài liệu PDF đã chỉnh sửa

```csharp
pdfDoc.Save("YOUR_DIRECTORY/output.pdf");
```

Tệp kết quả, `output.pdf`, chứa mục `ExtGState` mới và, nếu bạn đã thêm nội dung tùy chọn, một lớp phủ hình chữ nhật bán trong suốt.

### Kết quả mong đợi

Khi mở `output.pdf` bằng Adobe Acrobat Reader hoặc bất kỳ trình xem PDF nào, bạn sẽ thấy:

* Nội dung trang gốc không thay đổi.
* Nếu bạn chạy đoạn mã vẽ tùy chọn, một hình chữ nhật màu xanh nhạt có độ trong suốt 50 %, cho phép nội dung phía dưới hiển thị.

## Danh sách mã nguồn đầy đủ

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Cos;
using Aspose.Pdf.Operators;
using System.Collections.Generic;

class AddTransparencyExample
{
    static void Main()
    {
        // 1. Load the PDF
        var pdfDoc = new Document("YOUR_DIRECTORY/input.pdf");

        // 2. Get the first page and its resources
        var page = pdfDoc.Pages[1];
        var resourceEditor = new DictionaryEditor(page.Resources);

        // 3. Retrieve or create ExtGState dictionary
        CosPdfDictionary extGStateDict;
        if (resourceEditor.ContainsKey("ExtGState"))
            extGStateDict = (CosPdfDictionary)resourceEditor["ExtGState"].ToCosPdfDictionary();
        else
        {
            extGStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDoc);
            resourceEditor.Add("ExtGState", extGStateDict);
        }

        // 4. Create new graphics state with transparency settings
        var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDoc);
        var graphicsStateEntries = new[]
        {
            new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),   // Stroke opacity
            new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),   // Fill opacity
            new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // Blend mode
        };
        foreach (var entry in graphicsStateEntries)
            newGraphicsState.Add(entry);

        // 5. Add the graphics state to ExtGState with a unique name
        extGStateDict.Add("GS0", newGraphicsState);

        // 6. (Optional) Draw a rectangle using the new state
        var content = new PageContent();
        content.Operators.Add(new Operator("q"));
        content.Operators.Add(new Operator("GS0", "gs"));
        content.Operators.Add(new Operator("0.2", "0.2", "0.8", "rg"));
        content.Operators.Add(new Operator("100", "500", "200", "100", "re"));
        content.Operators.Add(new Operator("f"));
        content.Operators.Add(new Operator("Q"));
        page.Contents.Insert(0, content);

        // 7. Save the updated PDF
        pdfDoc.Save("YOUR_DIRECTORY/output.pdf");
    }
}
```

Sao chép mã vào một ứng dụng console, thay `YOUR_DIRECTORY` bằng đường dẫn thư mục thực tế, và chạy. Chương trình sẽ tạo `output.pdf` với các cài đặt độ trong suốt đã được thêm.

## Những lỗi thường gặp và cách tránh

| Triệu chứng | Nguyên nhân | Cách khắc phục |
|------------|-------------|----------------|
| `KeyNotFoundException` trên `"ExtGState"` | Trang không có mục `ExtGState`. | Tutorial đã tạo dictionary khi thiếu; hãy chắc chắn bạn dùng khối điều kiện được cung cấp. |
| Độ trong suốt không hiển thị trong trình xem | Các lệnh vẽ không tham chiếu tới `GS0`. | Thêm toán tử `gs` (`"GS0 gs"`) trước bất kỳ thao tác vẽ nào, như trong đoạn mã tùy chọn. |
| PDF bị hỏng sau khi lưu | Kết hợp API cấp cao `Page` với các đối tượng COS cấp thấp không đúng cách. | Tuân thủ mẫu lấy `CosPdfDictionary` qua `DictionaryEditor` và tránh sửa cùng một dictionary hai lần. |
| Chế độ hòa trộn không có hiệu lực | Trình xem không hỗ trợ chế độ hòa trộn đã chọn. | Dùng `Normal` để tương thích rộng; thử `Multiply` chỉ trong các trình xem báo cáo hỗ trợ. |

## Các bước tiếp theo

Bây giờ bạn đã biết cách **thêm độ trong suốt vào tệp PDF**, bạn có thể:

* Áp dụng cùng một trạng thái đồ họa cho nhiều trang bằng cách lặp qua `pdfDoc.Pages`.
* Kết hợp độ trong suốt với các đường cắt (clipping paths) để tạo watermark tinh vi.
* Khám phá các mục ExtGState khác như `SM` (điều chỉnh nét) hoặc `CA`.

## Bạn nên học gì tiếp theo?

Các tutorial sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh với giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [How to Add and Align Text Stamps in PDFs Using Aspose.PDF for .NET | Watermarks & Backgrounds](/pdf/english/net/watermarks-backgrounds/add-text-stamp-aspose-pdf-dotnet/)
- [How to Add a Rotating Image Watermark to PDFs Using Aspose.PDF for .NET](/pdf/english/net/watermarks-backgrounds/add-rotating-image-watermark-aspose-pdf/)
- [How to Add Page Stamps in PDFs Using Aspose.PDF for .NET: A Complete Guide](/pdf/english/net/watermarks-backgrounds/add-page-stamp-aspose-pdf-dotnet-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}