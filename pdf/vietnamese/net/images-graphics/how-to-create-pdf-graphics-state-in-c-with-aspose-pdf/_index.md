---
category: general
date: 2026-11-16
description: Tìm hiểu cách tạo trạng thái đồ họa PDF trong C# bằng Aspose.Pdf. Hướng
  dẫn này bao gồm độ trong suốt, chế độ hòa trộn và ví dụ mã đầy đủ.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create pdf graphics state
- Aspose.Pdf ExtGState
- PDF opacity
- C# PDF manipulation
- PDF blend mode
- Aspose.Pdf graphics state
language: vi
lastmod: 2026-11-16
og_description: Tạo trạng thái đồ họa PDF trong C# bằng Aspose.Pdf. Tham khảo hướng
  dẫn toàn diện này để thiết lập độ trong suốt và chế độ hòa trộn một cách lập trình.
og_image_alt: Illustration of how to create PDF graphics state with Aspose.Pdf in
  C#
og_title: Tạo trạng thái đồ họa PDF trong C# – hướng dẫn chi tiết Aspose.Pdf
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Learn how to create PDF graphics state in C# using Aspose.Pdf. This
    guide covers opacity, blend mode, and full code example.
  headline: How to create PDF graphics state in C# with Aspose.Pdf
  type: TechArticle
tags:
- Aspose.Pdf
- C#
- PDF
title: Cách tạo trạng thái đồ họa PDF trong C# với Aspose.Pdf
url: /vi/net/images-graphics/how-to-create-pdf-graphics-state-in-c-with-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách tạo trạng thái đồ họa PDF trong C# với Aspose.Pdf

Nếu bạn cần **tạo trạng thái đồ họa PDF** trong một dự án .NET, hướng dẫn này sẽ chỉ cho bạn cách thực hiện chính xác với Aspose.Pdf. Cho dù bạn muốn kiểm soát độ trong suốt, thay đổi chế độ hòa trộn, hoặc tái sử dụng một trạng thái đồ họa tùy chỉnh trên nhiều trang, các bước dưới đây sẽ cung cấp cho bạn một giải pháp hoàn chỉnh, sẵn sàng chạy.

Trong hướng dẫn này bạn sẽ học cách truy cập tài nguyên của trang, thêm một mục **ExtGState**, và lưu các thay đổi vào một tệp mới. Ví dụ hoạt động với Aspose.Pdf 23.12 (hoặc mới hơn) và nhắm tới .NET 6+, nhưng các khái niệm cũng áp dụng cho các phiên bản trước.

## Prerequisites

Trước khi bắt đầu, hãy chắc chắn rằng bạn có:

* Visual Studio 2022 (hoặc bất kỳ IDE C# nào) với .NET 6 SDK đã được cài đặt.  
* Giấy phép Aspose.Pdf cho .NET hoặc khóa đánh giá tạm thời.  
* Một tệp PDF có tên `input.pdf` được đặt trong thư mục mà bạn có thể tham chiếu từ mã.  

Không cần thêm bất kỳ gói NuGet nào ngoài `Aspose.Pdf`.

## What the tutorial covers

* Tải tài liệu PDF hiện có.  
* Điều hướng tới từ điển tài nguyên của trang đầu tiên.  
* Tạo một từ điển trạng thái đồ họa mới định nghĩa độ trong suốt nét vẽ (`CA`), độ trong suốt tô (`ca`), và chế độ hòa trộn (`BM`).  
* Thêm trạng thái đồ họa mới vào bộ sưu tập **ExtGState** với tên tùy chỉnh (`GS0`).  
* Lưu PDF đã cập nhật để các lệnh vẽ tiếp theo có thể tham chiếu đến trạng thái mới.

Khi kết thúc hướng dẫn, bạn sẽ có khả năng **tạo trạng thái đồ họa PDF** một cách lập trình và tái sử dụng chúng trong bất kỳ thao tác vẽ nào.

## Step 1: Set up the project and import namespaces

Tạo một ứng dụng console mới (hoặc tích hợp mã vào dự án hiện có). Thêm tham chiếu Aspose.Pdf và bao gồm các namespace cần thiết:

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Operators;
using Aspose.Pdf.Generator;
```

> **Pro tip:** Nếu bạn đang sử dụng phiên bản đánh giá miễn phí, thêm `Aspose.Pdf.License license = new Aspose.Pdf.License(); license.SetLicense("Aspose.Pdf.lic");` trước khi tải tài liệu để tránh thông báo watermark.

## Step 2: Load the PDF document

Mở tệp rất đơn giản. Lớp `Document` đại diện cho toàn bộ PDF và cung cấp cho bạn quyền truy cập vào các trang và tài nguyên của nó.

```csharp
// Step 2: Load the PDF document
string inputPath = @"YOUR_DIRECTORY\input.pdf";

using (var document = new Document(inputPath))
{
    // All subsequent steps run inside this using block
```

Việc đặt mã trong một khối `using` đảm bảo rằng handle của tệp được giải phóng sau khi thực hiện, điều này rất quan trọng cho **C# PDF manipulation** trong các dịch vụ sản xuất.

## Step 3: Retrieve the first page’s resources dictionary

Mỗi trang PDF có một từ điển *Resources* lưu trữ phông chữ, hình ảnh và trạng thái đồ họa. Chúng ta cần một `DictionaryEditor` để chỉnh sửa cấu trúc này.

```csharp
    // Step 3: Get the first page and its resources dictionary
    var page = document.Pages[1];
    var resourcesEditor = new DictionaryEditor(page.Resources);
```

Nếu PDF đã chứa mục `ExtGState`, `resourcesEditor["ExtGState"]` sẽ trả về nó; nếu không, Aspose.Pdf sẽ tạo một từ điển rỗng cho chúng ta khi chúng ta thêm mục đầu tiên.

## Step 4: Access or create the ExtGState dictionary

**ExtGState** là từ điển chứa các đối tượng trạng thái đồ họa có tên. Chúng ta hoặc lấy một mục đã tồn tại hoặc tạo một container mới.

```csharp
    // Step 4: Access (or create) the ExtGState dictionary within the resources
    var extGState = resourcesEditor["ExtGState"].ToCosPdfDictionary();
```

Khi `ExtGState` không tồn tại, `resourcesEditor["ExtGState"]` sẽ tự động trả về một từ điển rỗng mới, đảm bảo mã hoạt động với bất kỳ PDF nào.

## Step 5: Build the new graphics state dictionary

Một trạng thái đồ họa là một `CosPdfDictionary` với các khóa cụ thể:

* `CA` – độ trong suốt nét vẽ (0‑1)  
* `ca` – độ trong suốt tô (0‑1)  
* `BM` – chế độ hòa trộn (`Normal`, `Multiply`, v.v.)

Chúng ta tạo một từ điển rỗng, điền dữ liệu và sau đó thêm nó vào `ExtGState`.

```csharp
    // Step 5: Create a new graphics state dictionary with desired parameters
    var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(document);
    var parameters = new[]
    {
        new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),   // Stroke opacity (fully opaque)
        new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // Fill opacity (50% transparent)
        new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // Blend mode
    };

    foreach (var p in parameters)
        newGraphicsState.Add(p);
```

Bạn có thể thay đổi `0.5` thành bất kỳ giá trị nào trong khoảng `0` đến `1` để điều chỉnh độ trong suốt tô, hoặc thay `"Normal"` bằng `"Multiply"` để có một **PDF blend mode** khác. Sự linh hoạt này là lý do tạo một trạng thái đồ họa tùy chỉnh là kỹ thuật mạnh mẽ trong việc xử lý **Aspose.Pdf graphics state**.

## Step 6: Register the graphics state with a name

Các luồng nội dung PDF tham chiếu đến trạng thái đồ họa bằng tên. Ở đây chúng ta dùng `GS0`, nhưng bất kỳ tên duy nhất nào cũng được.

```csharp
    // Step 6: Add the new graphics state to the ExtGState dictionary with a name (e.g., GS0)
    extGState.Add("GS0", newGraphicsState);
```

Nếu bạn cần nhiều trạng thái, lặp lại bước tạo với các tham số khác nhau và thêm chúng dưới dạng `GS1`, `GS2`, v.v. Mô hình này mở rộng tốt cho các tài liệu phức tạp cần độ trong suốt hoặc cài đặt hòa trộn khác nhau trên các lớp khác nhau.

## Step 7: Save the modified PDF

Cuối cùng, ghi tài liệu đã cập nhật vào một tệp mới. Giữ nguyên tệp gốc giúp việc gỡ lỗi dễ dàng hơn.

```csharp
    // Step 7: Save the updated PDF document
    string outputPath = @"YOUR_DIRECTORY\output.pdf";
    document.Save(outputPath);
}
```

Sau khi thực thi, `output.pdf` sẽ chứa một mục `ExtGState` có tên `GS0`. Bất kỳ toán tử vẽ nào sau đó đều có thể tham chiếu tới nó bằng toán tử `gs` (ví dụ, `GS0 gs` trong một luồng nội dung).

> **Why this matters:** Bằng cách tạo một trạng thái đồ họa có thể tái sử dụng, bạn tránh việc lặp lại cài đặt độ trong suốt và hòa trộn cho mỗi lệnh vẽ, điều này cải thiện cả hiệu năng và khả năng bảo trì.

## Using the new graphics state in a content stream (optional)

Nếu bạn muốn thấy hiệu ứng ngay lập tức, có thể thêm một hình chữ nhật đơn giản sử dụng trạng thái chúng ta vừa tạo:

```csharp
using (var document = new Document(outputPath))
{
    var page = document.Pages[1];
    var content = page.Contents[1]; // Get the first content stream

    // Insert graphics state selection and a semi‑transparent rectangle
    var operators = new List<Operator>
    {
        new Operator("GS0", "gs"),                     // Select our custom graphics state
        new Operator("0.5", "w"),                      // Set line width (optional)
        new Operator("100", "100", "200", "150", "re"), // Rectangle (x, y, width, height)
        new Operator("B")                              // Stroke the rectangle
    };

    foreach (var op in operators)
        content.Operators.Add(op);

    document.Save(@"YOUR_DIRECTORY\final_output.pdf");
}
```

Hình chữ nhật sẽ được vẽ với độ trong suốt tô 50 % trong khi nét vẽ vẫn hoàn toàn không trong suốt, chính xác như đã định nghĩa trong từ điển **create PDF graphics state**.

## Common pitfalls and how to avoid them

| Vấn đề | Nguyên nhân | Cách khắc phục |
|-------|------------|----------------|
| `ExtGState` entry not found | Một số tệp PDF không có từ điển này. | `DictionaryEditor` sẽ tự động tạo nó khi bạn thêm mục đầu tiên, vì vậy không cần kiểm tra thêm. |
| Opacity values > 1 or < 0 | Spec PDF giới hạn độ trong suốt trong khoảng `[0,1]`. | Giới hạn giá trị trước khi tạo `CosPdfNumber`. |
| Blend mode typo | Tên chế độ hòa trộn PDF phân biệt chữ hoa và chữ thường. | Sử dụng đúng tên như `"Normal"`, `"Multiply"`, `"Screen"`. |
| License watermark | Phiên bản đánh giá sẽ thêm watermark trên trang đầu tiên. | Áp dụng tệp giấy phép hợp lệ trước khi mở tài liệu. |

Việc xử lý các trường hợp này sẽ đảm bảo việc **tạo trạng thái đồ họa PDF** của bạn hoạt động ổn định trên các nguồn PDF khác nhau.

## Full, runnable example

Dưới đây là một chương trình tự chứa mà bạn có thể sao chép, dán và chạy. Thay `YOUR_DIRECTORY` bằng đường dẫn thư mục thực tế trên máy của bạn.

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Generator;

class Program
{
    static void Main()
    {
        // Optional: apply license to remove evaluation watermark
        // var license = new Aspose.Pdf.License();
        // license.SetLicense("Aspose.Pdf.lic");

        string inputPath = @"YOUR_DIRECTORY\input.pdf";
        string outputPath = @"YOUR_DIRECTORY\output.pdf";

        using (var document = new Document(inputPath))
        {
            // 1️⃣ Get first page and its resources
            var page = document.Pages[1];
            var resourcesEditor = new DictionaryEditor(page.Resources);

            // 2️⃣ Access (or create) ExtGState dictionary
            var extGState = resourcesEditor["ExtGState"].ToCosPdfDictionary();

            // 3️⃣ Build new graphics state
            var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(document);
            var parameters = new[]
            {
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),   // Stroke opacity
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // Fill opacity
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // Blend mode
            };
            foreach (var p in parameters) newGraphicsState.Add(p);

            // 4️⃣ Register the state with a name (GS0)
            extGState.Add("


## What Should You Learn Next?


Các hướng dẫn sau đây bao gồm các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên đều có các ví dụ mã hoàn chỉnh kèm giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Create custom graphics state in PDF using Aspose.Pdf](/pdf/english/net/programming-with-operators/create-custom-graphics-state-in-pdf-using-aspose-pdf/)
- [Add graphics state to PDF using Aspose.PDF for .NET (C#)](/pdf/english/net/programming-with-operators/how-to-add-graphics-state-pdf-using-aspose-pdf-in-c/)
- [How to create empty graphics state in a PDF with C#](/pdf/english/net/programming-with-operators/how-to-create-empty-graphics-state-in-a-pdf-with-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}