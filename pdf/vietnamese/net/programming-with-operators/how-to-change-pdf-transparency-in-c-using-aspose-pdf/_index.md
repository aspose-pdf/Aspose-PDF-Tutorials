---
category: general
date: 2026-09-24
description: Tìm hiểu cách thay đổi độ trong suốt của PDF trong C# với Aspose.Pdf.
  Hướng dẫn từng bước này bao gồm độ mờ của PDF, chế độ hòa trộn và chỉnh sửa trạng
  thái đồ họa.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- change PDF transparency
- Aspose.Pdf graphics state
- PDF opacity
- C# PDF manipulation
- blend mode PDF
- modify PDF resources
language: vi
lastmod: 2026-09-24
og_description: Thay đổi độ trong suốt PDF trong C# bằng Aspose.Pdf. Hãy làm theo
  hướng dẫn này để chỉnh sửa độ trong suốt PDF, chế độ hòa trộn và trạng thái đồ họa
  cho đầu ra tài liệu chuyên nghiệp.
og_image_alt: Screenshot showing C# code that changes PDF transparency
og_title: Thay đổi độ trong suốt PDF trong C# – hướng dẫn đầy đủ Aspose.Pdf
schemas:
- author: Aspose
  dateModified: '2026-09-24'
  description: Learn how to change PDF transparency in C# with Aspose.Pdf. This step‑by‑step
    guide covers PDF opacity, blend mode and graphics state editing.
  headline: How to change PDF transparency in C# using Aspose.Pdf
  type: TechArticle
tags:
- PDF
- C#
- Aspose.Pdf
- Transparency
title: Cách thay đổi độ trong suốt của PDF trong C# bằng Aspose.Pdf
url: /vi/net/programming-with-operators/how-to-change-pdf-transparency-in-c-using-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách thay đổi độ trong suốt PDF trong C# bằng Aspose.Pdf

Nếu bạn cần **thay đổi độ trong suốt PDF** trong một dự án .NET, hướng dẫn này sẽ chỉ cho bạn cách thực hiện chính xác bằng Aspose.Pdf. Bạn sẽ thấy một ví dụ hoàn chỉnh, có thể chạy được, chỉnh sửa độ mờ của PDF, thiết lập chế độ hòa trộn và cập nhật từ điển trạng thái đồ họa của trang.

Thay đổi độ trong suốt PDF là một yêu cầu phổ biến khi bạn muốn thêm dấu watermark, lớp phủ đồ họa, hoặc các hiệu ứng hình ảnh tùy chỉnh. Trong tutorial này bạn sẽ học cách chỉnh sửa **trạng thái đồ họa Aspose.Pdf**, điều chỉnh **độ trong suốt PDF**, và làm việc với các cài đặt **blend mode PDF** — tất cả đều bằng mã C# sạch sẽ.

## Yêu cầu trước

Trước khi bắt đầu, hãy chắc chắn rằng bạn đã có:

* .NET 6.0 hoặc phiên bản mới hơn được cài đặt  
* Giấy phép Aspose.Pdf for .NET (hoặc khóa đánh giá tạm thời)  
* Một tệp PDF có tên `input.pdf` trong thư mục bạn có thể tham chiếu bằng `YOUR_DIRECTORY`  
* Kiến thức cơ bản về C# và Visual Studio (bất kỳ IDE nào cũng được)

Không cần thêm bất kỳ gói NuGet nào ngoài `Aspose.Pdf`. Mã chạy trên Windows, Linux hoặc macOS vì Aspose.Pdf hỗ trợ đa nền tảng.

## Thay đổi độ trong suốt PDF – bước 1: mở tài liệu PDF

Hoạt động đầu tiên là tải PDF nguồn. Sử dụng khối `using` sẽ đảm bảo rằng tay cầm tệp được giải phóng tự động.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;
using System.Collections.Generic;

string inputPath  = @"YOUR_DIRECTORY\input.pdf";
string outputPath = @"YOUR_DIRECTORY\output.pdf";

using (var document = new Document(inputPath))
{
    // The document is now ready for manipulation.
```

Mở tài liệu là nền tảng cho bất kỳ nhiệm vụ **C# PDF manipulation** nào. Nếu tệp không tìm thấy, Aspose.Pdf sẽ ném ra `FileNotFoundException`, vì vậy hãy kiểm tra lại đường dẫn trước khi chạy mã.

## Truy cập tài nguyên trang với trạng thái đồ họa Aspose.Pdf

Tiếp theo, lấy trang đầu tiên và từ điển tài nguyên của nó. Từ điển tài nguyên chứa các đối tượng như phông chữ, hình ảnh và các mục **ExtGState** điều khiển các tham số đồ họa.

```csharp
    // Step 2: Get the first page of the document
    var page = document.Pages[1];

    // Step 3: Access the page's resource dictionary for editing
    var resourcesEditor = new DictionaryEditor(page.Resources);
```

Lớp `DictionaryEditor` cung cấp một lớp bao tiện lợi để đọc và ghi các từ điển PDF. Ở đây chúng ta tập trung vào từ điển **ExtGState** vì nó lưu trữ các cài đặt độ trong suốt.

## Tạo và cấu hình trạng thái đồ họa mới cho độ trong suốt PDF

Bây giờ chúng ta xây dựng một từ điển trạng thái đồ họa mới. Từ điển này sẽ chứa các tham số xác định độ trong suốt nét vẽ (`CA`), độ trong suốt tô (`ca`) và chế độ hòa trộn (`BM`).

```csharp
    // Step 4: Retrieve the existing ExtGState dictionary (graphics states)
    var extGState = resourcesEditor["ExtGState"].ToCosPdfDictionary();

    // Step 5: Create a new empty graphics state dictionary
    var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(document);

    // Step 6: Define graphics state parameters (stroke opacity, fill opacity, blend mode)
    var parameters = new[]
    {
        new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),            // Stroke opacity (fully opaque)
        new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),          // Fill opacity (50 % transparent)
        new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))       // Blend mode PDF (standard normal blending)
    };

    // Step 7: Add each parameter to the new graphics state dictionary
    foreach (var param in parameters)
        newGraphicsState.Add(param);
```

* **`CA`** kiểm soát độ trong suốt của các thao tác nét vẽ (đường, viền).  
* **`ca`** kiểm soát độ trong suốt của các thao tác tô (hình dạng đã tô, văn bản).  
* **`BM`** chọn chế độ hòa trộn; `"Normal"` là mặc định, nhưng bạn có thể dùng `"Multiply"` hoặc `"Screen"` cho các hiệu ứng nghệ thuật.

Các cài đặt này là cốt lõi của việc **điều chỉnh độ trong suốt PDF**. Điều chỉnh các giá trị số để phù hợp với thiết kế hình ảnh của bạn — `0` nghĩa là hoàn toàn trong suốt, `1` nghĩa là hoàn toàn không trong suốt.

## Chèn trạng thái đồ họa và lưu tài liệu

Sau khi tạo trạng thái mới, chúng ta thêm nó vào từ điển **ExtGState** hiện có dưới một tên duy nhất (`GS0`). Cuối cùng, lưu PDF đã được chỉnh sửa.

```csharp
    // Step 8: Insert the new graphics state into the ExtGState dictionary with a name
    extGState.Add("GS0", newGraphicsState);

    // Step 9: Save the modified PDF document
    document.Save(outputPath);
}
```

Khi PDF được mở trong trình xem, bất kỳ nội dung nào tham chiếu tới `GS0` sẽ được hiển thị với độ trong suốt đã định nghĩa. Bạn có thể sau này áp dụng trạng thái đồ họa này cho các đối tượng cụ thể bằng thuộc tính `GraphicsState` của các lệnh vẽ (ví dụ, `page.Contents.Add(new TextFragment(...){ GraphicsState = "GS0" })`).

## Xác minh kết quả

Mở `output.pdf` trong Adobe Acrobat Reader, Foxit, hoặc bất kỳ trình xem PDF nào hỗ trợ độ trong suốt. Bạn sẽ thấy các phần tử tô của trang đầu tiên được hiển thị với độ trong suốt 50 % trong khi các nét vẽ vẫn hoàn toàn không trong suốt. Nếu bạn không nhận thấy thay đổi, hãy chắc chắn rằng trang thực sự sử dụng trạng thái đồ họa mới — nếu không, bạn có thể gán rõ ràng `GS0` cho các đối tượng muốn ảnh hưởng.

![Change PDF transparency in C# code example](path/to/image.png){: .img-responsive alt="Thay đổi độ trong suốt PDF trong ví dụ mã C#"}  

*Hình ảnh trên hiển thị toàn bộ mã nguồn C# thay đổi độ trong suốt PDF.*

## Các biến thể phổ biến và trường hợp đặc biệt

| Tình huống | Cách điều chỉnh mã |
|-----------|--------------------|
| **Nhiều trang** | Lặp qua `document.Pages` và lặp lại các bước 2‑8 cho mỗi trang. |
| **Chế độ hòa trộn khác** | Thay `"Normal"` bằng `"Multiply"`, `"Screen"` hoặc bất kỳ tên blend chuẩn PDF nào. |
| **Tăng độ trong suốt tô** | Thay `new CosPdfNumber(0.5)` bằng giá trị từ `0` đến `1`. |
| **Không có ExtGState hiện có** | Nếu `resourcesEditor["ExtGState"]` trả về `null`, tạo một từ điển mới: `var extGState = CosPdfDictionary.CreateEmptyDictionary(document); resourcesEditor["ExtGState"] = extGState;` |

Các biến thể này minh họa tính linh hoạt của **việc sửa đổi tài nguyên PDF** bằng Aspose.Pdf. Bằng cách điều chỉnh các tham số, bạn có thể tạo dấu watermark, lớp phủ bán trong suốt, hoặc các yếu tố UI tùy chỉnh bên trong PDF.

## Ví dụ đầy đủ, có thể chạy

Dưới đây là chương trình hoàn chỉnh mà bạn có thể sao chép‑dán vào một dự án Console App mới. Nó chứa tất cả các chỉ thị `using` cần thiết, xử lý lỗi, và chú thích.



## Bạn nên học gì tiếp theo?

Các tutorial sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật đã được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh với giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Change PDF Opacity with Aspose.PDF – Complete C# Guide](/pdf/english/net/programming-with-stamps-and-watermarks/change-pdf-opacity-with-aspose-pdf-complete-c-guide/)
- [Change PDF Opacity in C# – Complete Aspose Guide](/pdf/english/net/programming-with-stamps-and-watermarks/change-pdf-opacity-in-c-complete-aspose-guide/)
- [Add Transparency to PDF using Aspose – Complete C# Guide](/pdf/english/net/programming-with-operators/add-transparency-to-pdf-using-aspose-complete-c-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}