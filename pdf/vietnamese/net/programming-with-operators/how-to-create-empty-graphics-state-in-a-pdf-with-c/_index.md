---
category: general
date: 2026-08-17
description: Tạo trạng thái đồ họa trống trong PDF bằng C# và Aspose.Pdf. Thực hiện
  theo hướng dẫn từng bước này để chỉnh sửa tài nguyên ExtGState một cách an toàn.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create empty graphics state
- Aspose PDF graphics state
- C# modify PDF resources
- add ExtGState dictionary
- PDF page resources editing
language: vi
lastmod: 2026-08-17
og_description: Tạo trạng thái đồ họa trống trong PDF bằng C#. Hướng dẫn này chỉ cách
  chỉnh sửa tài nguyên ExtGState với Aspose.Pdf để thực hiện các sửa đổi PDF đáng
  tin cậy.
og_image_alt: Screenshot of C# code that adds an empty graphics state to a PDF document
og_title: Tạo trạng thái đồ họa trống trong PDF bằng C# – hướng dẫn từng bước
schemas:
- author: Aspose
  dateModified: '2026-08-17'
  description: Create empty graphics state in a PDF using C# and Aspose.Pdf. Follow
    this step‑by‑step guide to edit ExtGState resources safely.
  headline: How to create empty graphics state in a PDF with C#
  type: TechArticle
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Cách tạo trạng thái đồ họa rỗng trong PDF bằng C#
url: /vi/net/programming-with-operators/how-to-create-empty-graphics-state-in-a-pdf-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách tạo trạng thái đồ họa trống trong PDF bằng C#

Nếu bạn cần **tạo trạng thái đồ họa trống** trong một PDF, hướng dẫn này sẽ chỉ cho bạn cách thực hiện chính xác bằng C# và Aspose.Pdf. Bạn sẽ thấy một ví dụ hoàn chỉnh, có thể chạy được, thêm một mục mới vào từ điển ExtGState của trang mà không ảnh hưởng đến nội dung hiện có.

Làm việc với trạng thái đồ họa PDF là một yêu cầu phổ biến khi bạn muốn kiểm soát độ trong suốt, chế độ hòa trộn, hoặc các tham số render khác trên cơ sở từng đối tượng. Đoạn mã dưới đây minh họa cách tiếp cận được khuyến nghị, giải thích lý do mỗi bước quan trọng, và đề cập đến các biến thể thường gặp mà bạn có thể gặp phải.

## Yêu cầu trước

* .NET 6.0 hoặc phiên bản mới hơn (mẫu này cũng biên dịch được với .NET Core).
* Giấy phép Aspose.Pdf cho .NET (hoặc khóa đánh giá tạm thời).
* Một thư mục chứa tệp `input.pdf` mà bạn muốn sửa đổi.
* Kiến thức cơ bản về cú pháp C# và các khái niệm PDF như từ điển tài nguyên.

## Bước 1: Thiết lập dự án và nhập không gian tên

Tạo một ứng dụng console mới hoặc tích hợp mã vào dự án hiện có. Thêm gói NuGet Aspose.Pdf:

```bash
dotnet add package Aspose.Pdf
```

Sau đó nhập các không gian tên cần thiết:

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Operators;
```

Các import này cho phép bạn truy cập các lớp `Document`, `DictionaryEditor` và các primitive PDF cần thiết để **tạo trạng thái đồ họa trống**.

## Bước 2: Xác định thư mục chứa các tệp PDF

```csharp
// Step 1: Define the folder that contains the PDF files
string dataDir = @"C:\PdfSamples\";
```

Thay thế đường dẫn bằng vị trí các tệp PDF của bạn. Giữ thư mục trong một biến giúp mã có thể tái sử dụng và dễ kiểm thử hơn.

## Bước 3: Tải tài liệu PDF nguồn

```csharp
// Step 2: Load the source PDF document
using (var pdfDocument = new Document(dataDir + "input.pdf"))
{
    // All subsequent operations happen inside this using block
```

Mở tài liệu trong một câu lệnh `using` đảm bảo rằng tay cầm tệp được giải phóng tự động sau khi bạn lưu các thay đổi.

## Bước 4: Truy cập trang đầu tiên và từ điển Resources của nó

```csharp
    // Step 3: Get the first page and its Resources dictionary
    var firstPage = pdfDocument.Pages[1];
    var resourcesEditor = new DictionaryEditor(firstPage.Resources);
    var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
```

* `Pages[1]` lấy trang đầu tiên (số trang PDF bắt đầu từ 1).
* `DictionaryEditor` cung cấp cách tiện lợi để đọc và sửa đổi các từ điển PDF.
* Mục `ExtGState` chứa tất cả các đối tượng graphics‑state cho trang. Nếu khóa không tồn tại, Aspose.Pdf sẽ tự động tạo một từ điển trống.

## Bước 5: Xây dựng một từ điển graphics‑state trống mới

Trạng thái đồ họa bạn thêm có thể là trống hoặc đã được điền sẵn các tham số như độ trong suốt (`CA`, `ca`) hoặc chế độ hòa trộn (`BM`). Trong hướng dẫn này, chúng tôi tạo một **trạng thái đồ họa trống** và sau đó đặt một vài giá trị điển hình để minh họa cách hoạt động của từ điển.

```csharp
    // Step 4: Create a new empty graphics‑state dictionary and set its parameters
    var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
    var parameters = new[]
    {
        new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),   // Stroke opacity
        new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // Fill opacity
        new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // Blend mode
    };
    foreach (var p in parameters)
        newGraphicsState.Add(p);
```

* `CosPdfDictionary.CreateEmptyDictionary` tạo một container sạch mà bạn có thể điền bất kỳ khóa graphics‑state nào.
* Việc thêm `CA`, `ca` và `BM` là tùy chọn; bạn có thể bỏ qua chúng nếu thực sự cần một trạng thái trống. Đoạn mã cho thấy cách thêm các mục khi bạn sau này quyết định kiểm soát việc render.

## Bước 6: Chèn trạng thái đồ họa mới vào từ điển ExtGState

```csharp
    // Step 5: Add the new graphics state to the page's ExtGState dictionary (e.g., name it "GS0")
    extGStateDict.Add("GS0", newGraphicsState);
```

Đặt tên mục `"GS0"` tuân theo quy ước chung là đặt tiền tố “GS” cho tên graphics‑state. Bạn có thể chọn bất kỳ tên PDF hợp lệ nào mà không trùng với các khóa hiện có.

## Bước 7: Lưu tài liệu PDF đã sửa đổi

```csharp
    // Step 6: Save the modified PDF document
    pdfDocument.Save(dataDir + "output.pdf");
}
```

Lệnh `Save` ghi tệp đã cập nhật vào `output.pdf`. Mở tệp này trong trình xem PDF sẽ xác nhận rằng trạng thái đồ họa mới tồn tại; bạn có thể tham chiếu tới nó sau này bằng toán tử `gs` trong các luồng nội dung.

### Danh sách mã nguồn đầy đủ

Kết hợp mọi thứ lại, chương trình hoàn chỉnh trông như sau:

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Operators;

class Program
{
    static void Main()
    {
        // Define the folder that contains the PDF files
        string dataDir = @"C:\PdfSamples\";

        // Load the source PDF document
        using (var pdfDocument = new Document(dataDir + "input.pdf"))
        {
            // Get the first page and its Resources dictionary
            var firstPage = pdfDocument.Pages[1];
            var resourcesEditor = new DictionaryEditor(firstPage.Resources);
            var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();

            // Create a new empty graphics‑state dictionary and set its parameters
            var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            var parameters = new[]
            {
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
            };
            foreach (var p in parameters)
                newGraphicsState.Add(p);

            // Add the new graphics state to the page's ExtGState dictionary (name it "GS0")
            extGStateDict.Add("GS0", newGraphicsState);

            // Save the modified PDF document
            pdfDocument.Save(dataDir + "output.pdf");
        }

        Console.WriteLine("Empty graphics state created and saved to output.pdf");
    }
}
```

Chạy chương trình sẽ in ra một dòng xác nhận và tạo ra `output.pdf` với trạng thái đồ họa mới được thêm.

## Tại sao cách tiếp cận này là tốt nhất

* **Chỉnh sửa từ điển trực tiếp** – Sử dụng `DictionaryEditor` tránh việc phải phân tích toàn bộ luồng nội dung. Bạn chỉ sửa đổi các tài nguyên mà bạn quan tâm.
* **Primitive PDF có kiểu** – `CosPdfNumber`, `CosPdfName` và `CosPdfDictionary` đảm bảo PDF được tạo tuân thủ chuẩn PDF 1.7.
* **An toàn** – Khối `using` giải phóng đối tượng `Document`, ngăn chặn khóa tệp có thể làm hỏng các bản build tiếp theo.
* **Mở rộng** – Khi trạng thái đồ họa trống đã tồn tại, bạn có thể tham chiếu tới nó từ bất kỳ toán tử nội dung nào (`gs`) để thay đổi độ trong suốt, chế độ hòa trộn, hoặc các tham số khác cho các lệnh vẽ đã chọn.

## Các biến thể phổ biến và trường hợp đặc biệt

| Tình huống | Điều chỉnh đề xuất |
|-----------|-------------------|
| **Nhiều trang** | Lặp qua `pdfDocument.Pages` và lặp lại việc chèn từ điển cho mỗi trang bạn cần sửa đổi. |
| **Không có mục ExtGState hiện có** | `resourcesEditor["ExtGState"]` tự động tạo một từ điển trống nếu nó không tồn tại. Không cần mã bổ sung. |
| **Tên graphics‑state khác** | Thay `"GS0"` bằng một tên phù hợp với quy ước đặt tên của bạn, ví dụ `"MyTransparentState"`. |
| **Chỉ thêm một trạng thái trống** | Bỏ qua mảng `parameters` và vòng lặp `foreach`; từ điển sẽ vẫn trống. |
| **Làm việc với PDF được mã hoá** | Cung cấp mật khẩu khi khởi tạo `new Document(path, password)` trước khi chỉnh sửa tài nguyên. |

## Xác minh kết quả

Bạn có thể xác minh rằng trạng thái đồ họa đã được thêm bằng cách kiểm tra PDF bằng một trình xem cấp thấp như **PDF‑Tron** hoặc **iText Sharp**. Tìm một mục tương tự như:

```
/ExtGState << /GS0 << /CA 1 /ca 0.5 /BM /Normal >> >>
```

Nếu mục này xuất hiện, thao tác **tạo trạng thái đồ họa trống** đã thành công.

## Kết luận

Bây giờ bạn đã biết cách **tạo trạng thái đồ họa trống** trong PDF bằng C# và Aspose.Pdf. Hướng dẫn đã bao phủ mọi bước — từ tải tài liệu, chỉnh sửa từ điển `ExtGState` cho tới lưu kết quả — đồng thời giải thích lý do đằng sau mỗi hành động.

Từ đây bạn có thể:

* Sử dụng trạng thái đồ họa mới trong các luồng nội dung (`gs /GS0`).
* Thử nghiệm các khóa bổ sung như `/SM` (điều chỉnh nét) hoặc `/OPM` (chế độ in chồng).
* Áp dụng kỹ thuật tương tự cho các loại tài nguyên khác như `/XObject` hoặc `/ColorSpace`.

Chúc bạn vui vẻ khi làm việc với PDF, và hãy tự do khám phá các kịch bản **trạng thái đồ họa Aspose PDF** khác như thay đổi độ trong suốt động hoặc chế độ hòa trộn tùy chỉnh!

## Bạn nên học gì tiếp theo?

Các hướng dẫn sau đây bao gồm các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoạt động đầy đủ với các giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Cách tạo đường nét đứt trong PDF bằng Aspose.PDF cho .NET: Hướng dẫn từng bước](/pdf/english/net/images-graphics/create-dashed-lines-aspose-pdf-net/)
- [Cách xóa đồ họa khỏi PDF bằng Aspose.PDF .NET: Hướng dẫn đầy đủ](/pdf/english/net/images-graphics/remove-graphics-aspose-pdf-net/)
- [Tạo và tô hình chữ nhật trong PDF bằng Aspose.PDF cho .NET: Hướng dẫn từng bước](/pdf/english/net/images-graphics/create-fill-rectangle-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}