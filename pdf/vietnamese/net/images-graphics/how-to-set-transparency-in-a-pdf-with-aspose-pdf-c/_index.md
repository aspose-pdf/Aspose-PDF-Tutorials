---
category: general
date: 2026-10-13
description: Tìm hiểu cách thiết lập độ trong suốt trong PDF bằng Aspose.Pdf cho C#.
  Ngoài ra, xem cách lưu PDF đã chỉnh sửa và thay đổi độ trong suốt của phần fill.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to set transparency
- save modified pdf
- change fill alpha
- set fill opacity
- edit pdf resources
language: vi
lastmod: 2026-10-13
og_description: Cách thiết lập độ trong suốt trong PDF bằng Aspose.Pdf cho C#. Hãy
  làm theo hướng dẫn này để chỉnh sửa tài nguyên PDF, thay đổi độ trong suốt của phần
  tô và lưu các tệp PDF đã chỉnh sửa.
og_image_alt: Screenshot of a PDF page showing transparent graphics applied with Aspose.Pdf
  in C#
og_title: Cách thiết lập độ trong suốt trong PDF bằng Aspose.Pdf C# – hướng dẫn từng
  bước
schemas:
- author: Aspose
  dateModified: '2026-10-13'
  description: Learn how to set transparency in a PDF with Aspose.Pdf for C#. Also
    see how to save modified PDF and change fill alpha.
  headline: How to set transparency in a PDF with Aspose.Pdf C#
  type: TechArticle
- description: Learn how to set transparency in a PDF with Aspose.Pdf for C#. Also
    see how to save modified PDF and change fill alpha.
  name: How to set transparency in a PDF with Aspose.Pdf C#
  steps:
  - name: Load the PDF document
    text: '```csharp using Aspose.Pdf; using System.Collections.Generic;'
  - name: Edit PDF resources to add a graphics state
    text: '```csharp // Get the first page (pages are 1‑based) Page firstPage = pdfDocument.Pages[1];'
  - name: Change fill alpha and set fill opacity
    text: '```csharp // Create an empty graphics state dictionary CosPdfDictionary
      newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);'
  - name: Add the new graphics state to the ExtGState dictionary
    text: '```csharp // Register the new state under the name "GS0" extGStateDict.Add("GS0",
      newGraphicsState); ```'
  - name: (Optional) Apply the graphics state in a content stream
    text: 'If you want to draw a rectangle using the new fill opacity, add the following
      after the previous steps:'
  - name: Save modified PDF
    text: '```csharp // Persist the changes to a new file pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
      ```'
  - name: Next steps
    text: '* Explore other blend modes (`Multiply`, `Screen`, etc.) by changing the
      `BM` entry. * Adjust stroke alpha (`CA`) to create semi‑transparent outlines.
      * Combine multiple graphics states to build a library of reusable visual effects.'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF manipulation
- Transparency
title: Cách đặt độ trong suốt trong PDF bằng Aspose.Pdf C#
url: /vi/net/images-graphics/how-to-set-transparency-in-a-pdf-with-aspose-pdf-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách đặt độ trong suốt trong PDF bằng Aspose.Pdf C#

Nếu bạn cần đặt độ trong suốt trong PDF bằng C#, hướng dẫn này sẽ chỉ cho bạn các bước chính xác. Bạn cũng sẽ học cách lưu các tệp PDF đã chỉnh sửa và thay đổi độ trong suốt của phần fill mà không rời khỏi môi trường Aspose.Pdf.

Hướng dẫn sẽ đi qua việc tải tài liệu, chỉnh sửa các tài nguyên PDF, tạo một graphics state xác định độ trong suốt của phần fill, và lưu các thay đổi. Không cần công cụ bên ngoài; mọi thứ chạy trong một dự án .NET tiêu chuẩn.

## Yêu cầu trước

Trước khi bắt đầu, hãy chắc chắn rằng bạn có:

* .NET 6.0 hoặc phiên bản mới hơn đã được cài đặt  
* Giấy phép Aspose.Pdf for .NET hợp lệ (hoặc khóa dùng thử miễn phí)  
* Một tệp PDF đầu vào nằm trong thư mục đã biết  

Bạn có thể thêm gói Aspose.Pdf thông qua NuGet:

```bash
dotnet add package Aspose.Pdf
```

## Cách đặt độ trong suốt trong PDF

Phần này chứa triển khai cốt lõi. Mỗi bước giải thích **tại sao** đoạn mã cần thiết, không chỉ **cái gì** nó làm.

### Bước 1: Tải tài liệu PDF

```csharp
using Aspose.Pdf;
using System.Collections.Generic;

// Load the source PDF
using var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");
```

*Tại sao lại có bước này?*  
`Document` đại diện cho toàn bộ tệp PDF trong bộ nhớ. Mở tệp cho phép bạn truy cập các trang, tài nguyên và các đối tượng cấp thấp mà bạn sẽ chỉnh sửa.

### Bước 2: Chỉnh sửa tài nguyên PDF để thêm một graphics state

```csharp
// Get the first page (pages are 1‑based)
Page firstPage = pdfDocument.Pages[1];

// Create an editor for the page's resource dictionary
DictionaryEditor resourceEditor = new DictionaryEditor(firstPage.Resources);

// Retrieve the ExtGState dictionary; it holds graphics state objects
CosPdfDictionary extGStateDict = resourceEditor["ExtGState"].ToCosPdfDictionary();
```

*Tại sao lại có bước này?*  
Các trang PDF lưu trữ các đối tượng có thể tái sử dụng—phông chữ, hình ảnh và graphics state—trong một từ điển tài nguyên. Mục `ExtGState` chứa các cài đặt độ trong suốt. Bằng cách chỉnh sửa từ điển này, bạn có thể giới thiệu một trạng thái mới mà trang có thể tham chiếu.

### Bước 3: Thay đổi fill alpha và đặt độ trong suốt của fill

```csharp
// Create an empty graphics state dictionary
CosPdfDictionary newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

// Define the graphics state entries
var graphicsStateEntries = new[]
{
    // Stroke alpha (CA) – fully opaque
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
    // Fill alpha (ca) – 50 % transparent
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
    // Blend mode (BM) – normal composition
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
};

// Populate the new graphics state
foreach (var entry in graphicsStateEntries)
    newGraphicsState.Add(entry);
```

*Tại sao lại có bước này?*  
`ca` điều khiển **độ trong suốt của fill**, trong khi `CA` điều khiển **độ trong suốt của stroke**. Đặt `ca` thành `0.5` làm cho các hình đã tô 50 % trong suốt. Mục `BM` chọn chế độ hòa trộn; `"Normal"` là lựa chọn phổ biến nhất cho độ trong suốt tiêu chuẩn.

### Bước 4: Thêm graphics state mới vào từ điển ExtGState

```csharp
// Register the new state under the name "GS0"
extGStateDict.Add("GS0", newGraphicsState);
```

*Tại sao lại có bước này?*  
Đặt tên cho graphics state (`"GS0"`) cho phép các luồng nội dung trên trang tham chiếu nó bằng toán tử `gs`. Sau khi đăng ký, trang có thể áp dụng độ trong suốt mà bạn vừa định nghĩa.

### Bước 5: (Tùy chọn) Áp dụng graphics state trong một content stream

Nếu bạn muốn vẽ một hình chữ nhật sử dụng độ trong suốt fill mới, hãy thêm đoạn sau sau các bước trước:

```csharp
// Create a content stream that uses the new graphics state
string cs = @"
q               % Save graphics state
/GS0 gs         % Apply the graphics state defined earlier
0 0 200 100 re  % Define a rectangle (x, y, width, height)
0.2 0.6 0.8 rg  % Set fill color (RGB)
f               % Fill the rectangle using the current graphics state
Q               % Restore graphics state
";

firstPage.Contents.Add(new Aspose.Pdf.Operator.GsContent(cs));
```

*Tại sao lại có bước này?*  
Các toán tử `q`/`Q` lưu và khôi phục graphics state, đảm bảo độ trong suốt chỉ ảnh hưởng đến các lệnh vẽ dự định. Toán tử `gs` chuyển sang graphics state có tên `"GS0"`.

### Bước 6: Lưu PDF đã chỉnh sửa

```csharp
// Persist the changes to a new file
pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
```

*Tại sao lại có bước này?*  
Lưu sẽ ghi lại từ điển tài nguyên đã cập nhật và bất kỳ luồng nội dung mới nào vào đĩa. Tệp kết quả (`output.pdf`) chứa hình chữ nhật trong suốt được định nghĩa ở bước trước.

## Ví dụ đầy đủ có thể chạy

Kết hợp các phần lại, đây là chương trình hoàn chỉnh mà bạn có thể biên dịch và chạy:

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Operators;
using System.Collections.Generic;

class SetTransparencyDemo
{
    static void Main()
    {
        // Load the source PDF
        using var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");

        // Access the first page and its resources
        Page firstPage = pdfDocument.Pages[1];
        var resourceEditor = new DictionaryEditor(firstPage.Resources);
        var extGStateDict = resourceEditor["ExtGState"].ToCosPdfDictionary();

        // Create a new graphics state with 50 % fill opacity
        var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
        var graphicsStateEntries = new[]
        {
            new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),   // stroke alpha
            new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // fill alpha
            new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
        };
        foreach (var entry in graphicsStateEntries)
            newGraphicsState.Add(entry);

        // Register the graphics state as "GS0"
        extGStateDict.Add("GS0", newGraphicsState);

        // Optional: draw a rectangle using the new transparency
        string cs = @"
q
/GS0 gs
0 0 200 100 re
0.2 0.6 0.8 rg
f
Q
";
        firstPage.Contents.Add(new GsContent(cs));

        // Save the modified PDF
        pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
    }
}
```

**Kết quả mong đợi** – `output.pdf` hiển thị một hình chữ nhật được tô màu tím nhạt với độ trong suốt 50 %, cho phép bất kỳ nội dung nền nào cũng hiển thị một phần.

## Các câu hỏi thường gặp và các trường hợp đặc biệt

* **Tôi có thể thay đổi độ trong suốt của stroke thay vì fill không?**  
  Đặt giá trị của `CA` (chữ hoa) thành một số trong khoảng `0` (hoàn toàn trong suốt) và `1` (hoàn toàn đục). Ví dụ đã đặt `CA` là `1`, nghĩa là các stroke vẫn đục.

* **Nếu trang chưa có từ điển ExtGState thì sao?**  
  `resourceEditor["ExtGState"]` sẽ tự động tạo một từ điển rỗng. Thêm `"GS0"` hoạt động tương tự.

* **Graphics state có thể tái sử dụng trên nhiều trang không?**  
  Có. Khi bạn thêm mục vào từ điển tài nguyên của tài liệu, bất kỳ trang nào tham chiếu `"GS0"` sẽ kế thừa cùng một cài đặt độ trong suốt.

* **Cách tiếp cận này khác gì so với việc sử dụng API `Graphics` cấp cao?**  
  Chỉnh sửa từ điển tài nguyên cấp thấp cho phép bạn kiểm soát chính xác các thành phần bên trong PDF và tạo ra các tệp nhỏ hơn vì tránh nhúng các đối tượng phụ thêm.

## Kết luận

Bây giờ bạn đã biết **cách đặt độ trong suốt trong PDF** bằng Aspose.Pdf cho C#. Hướng dẫn đã đề cập đến việc chỉnh sửa tài nguyên PDF, thay đổi fill alpha, đặt độ trong suốt của fill và lưu PDF đã chỉnh sửa. Với nền tảng này, bạn có thể thử nghiệm các chế độ blend khác nhau, áp dụng độ trong suốt cho văn bản, hoặc tạo graphics state tái sử dụng cho các tài liệu phức tạp.

### Các bước tiếp theo

* Khám phá các chế độ blend khác (`Multiply`, `Screen`, v.v.) bằng cách thay đổi mục `BM`.  
* Điều chỉnh stroke alpha (`CA`) để tạo các đường viền bán trong suốt.  
* Kết hợp nhiều graphics state để xây dựng thư viện các hiệu ứng hình ảnh tái sử dụng.  

Hãy thoải mái chia sẻ kết quả của bạn hoặc đặt câu hỏi trong phần bình luận. Chúc lập trình vui vẻ!

## Bạn nên học gì tiếp theo?

Các hướng dẫn sau đây bao gồm các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh với giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [How to Customize PDFs with Aspose.PDF for .NET&#58; Set Page Margins and Draw Lines](/pdf/english/net/document-manipulation/customize-pdfs-aspose-pdf-set-margins-draw-lines/)
- [How to Set Image Size in a PDF Using Aspose-PDF for .NET](/pdf/english/net/images-graphics/set-image-size-pdf-aspose-dotnet/)
- [How to Set PDF Permissions Using Aspose.PDF for .NET&#58; A Comprehensive Guide](/pdf/english/net/security-permissions/set-pdf-privileges-aspose-pdf-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}