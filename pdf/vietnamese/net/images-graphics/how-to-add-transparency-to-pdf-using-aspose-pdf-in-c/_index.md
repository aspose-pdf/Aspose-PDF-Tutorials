---
category: general
date: 2026-10-17
description: Thêm độ trong suốt vào PDF bằng Aspose.PDF cho .NET, chỉnh sửa tài nguyên
  PDF và lưu các tệp PDF đã chỉnh sửa trong một ví dụ duy nhất, có thể chạy được.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add transparency to pdf
- save modified pdf
- edit pdf resources
- Aspose.PDF transparency
- C# PDF manipulation
language: vi
lastmod: 2026-10-17
og_description: Thêm độ trong suốt vào PDF bằng Aspose.PDF cho .NET, chỉnh sửa tài
  nguyên PDF và lưu các tệp PDF đã chỉnh sửa với ví dụ C# đầy đủ.
og_image_alt: Screenshot showing a PDF with added transparency using Aspose.PDF in
  C#
og_title: Thêm độ trong suốt vào PDF với Aspose.PDF – hướng dẫn
schemas:
- author: Aspose
  dateModified: '2026-10-17'
  description: Add transparency to PDF with Aspose.PDF for .NET, edit PDF resources,
    and save modified PDF files in a single, runnable example.
  headline: How to add transparency to PDF using Aspose.PDF in C#
  type: TechArticle
tags:
- pdf
- aspnet
- csharp
title: Cách thêm độ trong suốt vào PDF bằng Aspose.PDF trong C#
url: /vi/net/images-graphics/how-to-add-transparency-to-pdf-using-aspose-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách thêm độ trong suốt vào PDF bằng Aspose.PDF trong C#

Nếu bạn cần **thêm độ trong suốt vào PDF** một cách lập trình, hướng dẫn này sẽ cho bạn một giải pháp rõ ràng, từ đầu đến cuối với Aspose.PDF cho .NET. Bạn sẽ học cách **chỉnh sửa tài nguyên PDF**, tạo một trạng thái đồ họa tùy chỉnh, và **lưu PDF đã chỉnh sửa** mà không rời khỏi dự án C# của mình.

Làm việc với độ trong suốt của PDF thường cảm thấy ẩn sau các toán tử PDF cấp thấp. Khi kết thúc tutorial này, bạn sẽ có một ví dụ hoạt động đầy đủ mà bạn có thể sao chép‑dán, chạy và điều chỉnh cho nhiều trang hoặc các chế độ hòa trộn khác nhau.

## Prerequisites

- .NET 6.0 (hoặc bất kỳ phiên bản .NET nào gần đây)  
- Gói NuGet Aspose.PDF for .NET (`Aspose.Pdf`)  
- Kiến thức cơ bản về C#  
- Một tệp PDF đầu vào (`input.pdf`) đặt trong thư mục bạn có thể tham chiếu

> **Pro tip:** Cài đặt gói bằng `dotnet add package Aspose.Pdf` trước khi bắt đầu.

## Step 1: Load the PDF document

Hoạt động đầu tiên là mở PDF nguồn. Aspose.PDF biểu diễn một PDF dưới dạng đối tượng `Document`, cho phép bạn truy cập các trang, tài nguyên và các từ điển cấp thấp.

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Collections;
using Aspose.Pdf.Text;
using Aspose.Pdf.Generator;   // for graphics‑state objects

// Path to the original PDF
string pdfPath = @"YOUR_DIRECTORY\input.pdf";

// Open the document in a using block so it disposes automatically
using (var document = new Document(pdfPath))
{
    // The rest of the steps are inside this block
```

*Why this matters:* Mở tài liệu theo cách này đảm bảo tay cầm tệp được giải phóng sau khi chúng ta hoàn thành việc chỉnh sửa, ngăn ngừa các vấn đề khóa tệp khi chúng ta **lưu PDF đã chỉnh sửa** sau này.

## Step 2: Access the first page and its resource dictionary

Các trang PDF lưu trữ các đối tượng đồ họa (phông chữ, hình ảnh, mục ExtGState) trong một *từ điển tài nguyên*. Để thay đổi độ mờ chúng ta cần làm việc với từ điển con `ExtGState`.

```csharp
    // Get the first page (pages are 1‑based in Aspose.PDF)
    Page page = document.Pages[1];

    // Obtain a mutable editor for the page's resources
    var resourcesEditor = new DictionaryEditor(page.Resources);

    // Retrieve the ExtGState dictionary; create it if missing
    var extGStateDict = resourcesEditor["ExtGState"]?.ToCosPdfDictionary()
                         ?? new CosPdfDictionary(document);
```

*Why this matters:* Nếu PDF gốc đã chứa một từ điển `ExtGState`, chúng ta sẽ mở rộng nó; nếu không, chúng ta tạo một từ điển mới để có thể an toàn **chỉnh sửa tài nguyên PDF**.

## Step 3: Build a new graphics state with transparency

Một trạng thái đồ họa (`ExtGState`) chứa các tham số như độ mờ nét (`CA`), độ mờ tô (`ca`) và chế độ hòa trộn (`BM`). Chúng ta tạo một từ điển rỗng và điền các giá trị mong muốn.

```csharp
    // Create an empty ExtGState dictionary for the new entry
    var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(document);

    // Define the transparency entries
    var entries = new[]
    {
        // CA – stroke opacity (1 = fully opaque)
        new KeyValuePair<string, ICosPdfPrimitive>("CA",
            new CosPdfNumber(1)),

        // ca – fill opacity (0.5 = 50 % transparent)
        new KeyValuePair<string, ICosPdfPrimitive>("ca",
            new CosPdfNumber(0.5)),

        // BM – blend mode (Normal is the default)
        new KeyValuePair<string, ICosPdfPrimitive>("BM",
            new CosPdfName("Normal"))
    };

    // Add each entry to the new ExtGState dictionary
    foreach (var entry in entries)
        newGraphicsState.Add(entry);
```

*Why this matters:* Mục `ca` là chìa khóa để **thêm độ trong suốt vào PDF** cho nội dung sử dụng trạng thái đồ họa này. Bạn có thể điều chỉnh giá trị số (0 – 1) để kiểm soát mức độ trong suốt của đối tượng.

## Step 4: Insert the graphics state into the page resources

Chúng ta phải đặt cho trạng thái đồ họa mới một tên (ví dụ, `"GS0"`). Tên này sau này có thể được tham chiếu bởi các luồng nội dung để áp dụng độ trong suốt.

```csharp
    // Add the new ExtGState under the name "GS0"
    extGStateDict.Add("GS0", newGraphicsState);

    // Ensure the modified ExtGState dictionary is written back to the page
    resourcesEditor["ExtGState"] = extGStateDict;
```

*Why this matters:* Bằng cách thêm `"GS0"` vào từ điển `ExtGState`, bất kỳ thao tác vẽ nào chọn trạng thái này sẽ được hiển thị với độ mờ đã định nghĩa. Đây là cốt lõi của **chỉnh sửa tài nguyên PDF** để đạt độ trong suốt.

## Step 5: Apply the graphics state to page content (optional)

Nếu bạn muốn nội dung trang hiện có tự động sử dụng độ trong suốt mới, bạn phải chèn một toán tử trạng thái đồ họa vào đầu luồng nội dung của trang. Đoạn mã dưới đây minh họa cách bao bọc nội dung hiện có bằng `gs` (đặt trạng thái đồ họa) và `Q` (khôi phục trạng thái đồ họa).

```csharp
    // Get the current content stream
    var content = page.Contents[1]; // assume a single content stream

    // Build a new stream that sets the graphics state, draws the original content, then restores
    string gsOperator = "/GS0 gs\n"; // select the graphics state we created
    string restoreOperator = "Q\n";   // restore graphics state after drawing

    // Prepend the gs operator and append the restore operator
    string newStream = gsOperator + content.Stream.ToString() + restoreOperator;

    // Replace the original stream with the modified one
    content.Stream = new CosPdfStream(document);
    content.Stream.SetData(newStream);
```

*Why this matters:* Nếu không thực hiện bước này, trạng thái đồ họa sẽ tồn tại nhưng không được sử dụng. Thêm toán tử `gs` báo cho trình render PDF áp dụng độ trong suốt cho mọi thứ tiếp theo.

## Step 6: **Save modified PDF** to disk

Cuối cùng, ghi tài liệu đã thay đổi vào một tệp mới. Phương thức `Save` tự động xử lý tất cả các cập nhật cấp thấp.

```csharp
    // Path for the output PDF
    string outputPath = @"YOUR_DIRECTORY\output.pdf";

    // Persist the changes
    document.Save(outputPath);
}
```

*Why this matters:* Lệnh `document.Save` đảm bảo **lưu PDF đã chỉnh sửa** chứa mục `ExtGState` mới và luồng nội dung tham chiếu tới nó. Tệp kết quả sẽ hiển thị màu tô bán trong suốt trên trang đầu tiên.

## Expected result

Mở `output.pdf` trong bất kỳ trình xem PDF nào (Adobe Reader, Chrome, v.v.) và bạn sẽ thấy đồ họa của trang đầu được vẽ với độ mờ tô 50 %. Nếu bạn kiểm tra PDF bằng công cụ như **PDF‑Tron** hoặc **iText**, bạn sẽ thấy một mục từ điển `ExtGState` có tên `GS0` với giá trị `ca` bằng `0.5`.

## Edge cases and variations

| Situation | What to change |
|-----------|----------------|
| **Multiple pages** | Lặp qua `document.Pages` và lặp lại các bước 2‑5 cho mỗi trang, sử dụng tên duy nhất như `GS1`, `GS2`, … |
| **Existing ExtGState name conflict** | Kiểm tra `extGStateDict.ContainsKey("GS0")` trước khi thêm; nếu đã tồn tại, tạo khóa mới (`"GS" + Guid.NewGuid().ToString("N")`) |
| **Different blend modes** | Thay `"Normal"` bằng `"Multiply"`, `"Screen"`, v.v., bằng cách thay đổi mục `BM` |
| **Only stroke opacity needed** | Bỏ mục `ca` hoặc đặt nó thành `1` và điều chỉnh `CA` thay thế |

## Complete, runnable example



## What Should You Learn Next?

Các tutorial sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh với giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Add transparency to PDF with Aspose.PDF – Complete C# Guide](/pdf/english/net/programming-with-stamps-and-watermarks/add-transparency-to-pdf-with-aspose-pdf-complete-c-guide/)
- [How to Add Page Stamps in PDFs Using Aspose.PDF for .NET: A Complete Guide](/pdf/english/net/watermarks-backgrounds/add-page-stamp-aspose-pdf-dotnet-guide/)
- [How to Add Images to PDFs Using Aspose.PDF for .NET: A Complete Guide](/pdf/english/net/images-graphics/add-images-to-pdfs-using-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}