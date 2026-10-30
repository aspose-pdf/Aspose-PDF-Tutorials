---
category: general
date: 2026-10-04
description: Tìm hiểu cách thay đổi độ trong suốt của PDF bằng Aspose.Pdf trong C#.
  Hướng dẫn từng bước này thêm một trạng thái đồ họa tùy chỉnh để điều chỉnh độ mờ
  và chế độ hòa trộn.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- change PDF transparency
- Aspose.Pdf graphics state
- PDF opacity C#
- ExtGState dictionary
- blend mode PDF
language: vi
lastmod: 2026-10-04
og_description: Thay đổi độ trong suốt PDF trong C# bằng Aspose.Pdf. Theo dõi hướng
  dẫn ngắn gọn này để chỉnh sửa độ mờ, chế độ hòa trộn và trạng thái đồ họa trong
  các tệp PDF của bạn.
og_image_alt: Screenshot of a PDF page before and after changing transparency with
  Aspose.Pdf
og_title: Thay đổi độ trong suốt PDF với Aspose.Pdf – hướng dẫn C# đầy đủ
schemas:
- author: Aspose
  dateModified: '2026-10-04'
  description: Learn how to change PDF transparency with Aspose.Pdf in C#. This step‑by‑step
    guide adds a custom graphics state to adjust opacity and blend mode.
  headline: How to change PDF transparency using Aspose.Pdf in C#
  type: TechArticle
tags:
- Aspose.Pdf
- C#
- PDF manipulation
- graphics state
title: Cách thay đổi độ trong suốt của PDF bằng Aspose.Pdf trong C#
url: /vi/net/programming-with-operators/how-to-change-pdf-transparency-using-aspose-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách thay đổi độ trong suốt PDF bằng Aspose.Pdf trong C#

Nếu bạn cần **thay đổi độ trong suốt PDF** trong một dự án .NET, hướng dẫn này sẽ chỉ cho bạn cách thực hiện chính xác với Aspose.Pdf. Khi kết thúc tutorial, bạn sẽ có một tệp PDF mà các đối tượng được chọn sử dụng độ mờ và chế độ hòa trộn tùy chỉnh, mà không cần bất kỳ công cụ bên ngoài nào.

Làm việc với độ trong suốt PDF là một yêu cầu phổ biến cho các dấu watermark, đồ họa phủ lên, hoặc hiệu ứng hình ảnh tinh tế. Các bước dưới đây bao gồm mọi thứ bạn cần—từ việc tải tài liệu đến chỉnh sửa **ExtGState dictionary**, tạo một trạng thái đồ họa mới, và lưu kết quả.

## Yêu cầu trước

Trước khi bắt đầu, hãy chắc chắn rằng bạn có:

* **Aspose.Pdf for .NET** (phiên bản 23.12 hoặc mới hơn). Bạn có thể cài đặt nó qua NuGet:

```bash
dotnet add package Aspose.Pdf
```

* Môi trường phát triển .NET (Visual Studio, VS Code, hoặc `dotnet` CLI).
* Một tệp PDF đầu vào nằm trong thư mục đã biết (ví dụ sử dụng `input.pdf`).

Không cần thư viện bổ sung nào khác.

## Bước 1: Tải tài liệu PDF

Hoạt động đầu tiên là mở PDF hiện có. Sử dụng khối `using` đảm bảo rằng tay cầm tệp được giải phóng tự động.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Cos;
using Aspose.Pdf.Tools;

// ...

using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
{
    // Subsequent steps go here
}
```

*Why this matters*: Tải tài liệu tạo ra một biểu diễn trong bộ nhớ mà bạn có thể sửa đổi. Lớp `Document` cũng cung cấp quyền truy cập vào các đối tượng COS cấp thấp, điều này rất cần thiết để thay đổi độ trong suốt PDF.

## Bước 2: Truy cập tài nguyên của trang đầu tiên

Trạng thái đồ họa được lưu trong từ điển tài nguyên của một trang. Chúng ta lấy trang đầu tiên và bao bọc tài nguyên của nó bằng `DictionaryEditor` để có thể chỉnh sửa một cách thuận tiện.

```csharp
var firstPage = pdfDocument.Pages[1];
var resourcesEditor = new DictionaryEditor(firstPage.Resources);
```

*Explanation*: `DictionaryEditor` trừu tượng việc xử lý từ điển COS, cho phép bạn đọc và ghi các mục như `ExtGState` mà không phải làm việc trực tiếp với cú pháp PDF thô.

## Bước 3: Lấy (hoặc tạo) từ điển ExtGState

**ExtGState dictionary** chứa các đối tượng trạng thái đồ họa có tên. Nếu nó đã tồn tại, chúng ta sẽ tái sử dụng; nếu không, chúng ta tạo một cái mới.

```csharp
CosPdfDictionary extGStateDict;

// Try to fetch an existing ExtGState entry
if (resourcesEditor.ContainsKey("ExtGState"))
{
    extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
}
else
{
    // Create a fresh ExtGState dictionary and add it to the resources
    extGStateDict = new CosPdfDictionary(pdfDocument);
    resourcesEditor["ExtGState"] = extGStateDict;
}
```

*Why this step*: Nếu không có mục `ExtGState` thì engine PDF sẽ không có nơi nào để tra cứu các cài đặt độ trong suốt tùy chỉnh. Thêm từ điển này giúp trang nhận biết bất kỳ trạng thái đồ họa mới nào bạn định nghĩa.

## Bước 4: Định nghĩa trạng thái đồ họa mới với độ trong suốt và chế độ hòa trộn

Một trạng thái đồ họa là tập hợp các tham số render PDF. Ở đây chúng ta đặt:

* **CA** – độ trong suốt nét vẽ (1 = hoàn toàn không trong suốt)
* **ca** – độ trong suốt tô màu (0.5 = 50 % trong suốt)
* **BM** – chế độ hòa trộn (`Normal` là mặc định, nhưng bạn có thể thử `Multiply`, `Screen`, v.v.)

```csharp
// Create an empty dictionary that will become the new graphics state
var graphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

// Prepare the entries
var graphicsStateEntries = new KeyValuePair<string, ICosPdfPrimitive>[]
{
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),   // stroke opacity
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // fill opacity
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // blend mode
};

// Populate the dictionary
foreach (var entry in graphicsStateEntries)
{
    graphicsState.Add(entry);
}
```

*Insight*: Các giá trị `CosPdfNumber` là số thực dấu phẩy động trong khoảng từ 0 đến 1. Thay đổi chúng cho phép bạn tinh chỉnh mức độ trong suốt của nét vẽ và tô màu. Chế độ hòa trộn quyết định cách nội dung trong suốt tương tác với đồ họa nền.

## Bước 5: Đăng ký trạng thái đồ họa trong ExtGState

Chúng ta đặt tên cho trạng thái mới (`GS0`). Sau này, khi vẽ các đối tượng, bạn sẽ tham chiếu tên này trong luồng nội dung.

```csharp
extGStateDict.Add("GS0", graphicsState); // "GS0" becomes the identifier you’ll use later
```

*Best practice*: Sử dụng quy ước đặt tên rõ ràng (`GS0`, `GS_Watermark`, v.v.) để bạn có thể quản lý nhiều trạng thái mà không gây nhầm lẫn.

## Bước 6: Áp dụng trạng thái đồ họa vào nội dung trang (tùy chọn)

Nếu bạn muốn áp dụng độ trong suốt mới cho các phần tử hiện có trên trang, cần chỉnh sửa luồng nội dung của trang. Dưới đây là một ví dụ đơn giản thêm một hình chữ nhật bán trong suốt lên trên trang.

```csharp
// Build a content stream that sets the graphics state and draws a rectangle
var contentBuilder = new Aspose.Pdf.Operators.ContentBuilder(pdfDocument);
contentBuilder.SetGraphicsState("GS0");
contentBuilder.SetFillColor(Color.FromRgb(255, 0, 0)); // red fill
contentBuilder.Rectangle(100, 500, 200, 100); // x, y, width, height
contentBuilder.FillPath();

firstPage.Contents.Add(contentBuilder);
```

*Why it works*: Toán tử `SetGraphicsState` thông báo cho trình thông dịch PDF sử dụng các tham số được định nghĩa trong `GS0` cho tất cả các lệnh vẽ tiếp theo. Vì vậy hình chữ nhật sẽ xuất hiện với độ trong suốt tô màu 50 % trong khi nét viền vẫn hoàn toàn không trong suốt.

## Bước 7: Lưu PDF đã chỉnh sửa

Cuối cùng, ghi các thay đổi trở lại đĩa.

```csharp
pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
```

Tệp `output.pdf` kết quả chứa trạng thái đồ họa mới, và bất kỳ nội dung nào tham chiếu `GS0` sẽ được render với độ trong suốt đã định nghĩa.

---

![Diagram showing PDF transparency change](/images/pdf-transparency-before-after.png "PDF page before and after applying custom graphics state")
*Image alt text (for SEO and accessibility):* **ví dụ thay đổi độ trong suốt PDF – trang gốc so với trang đã chỉnh sửa**

## Ví dụ hoạt động đầy đủ

Kết hợp mọi thứ lại, đây là một chương trình duy nhất, có thể chạy được, thay đổi độ trong suốt PDF và thêm một hình chữ nhật bán trong suốt.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Cos;
using Aspose.Pdf.Tools;
using System.Collections.Generic;
using Aspose.Pdf.Operators;
using Aspose.Pdf.Drawing;

class ChangePdfTransparency
{
    static void Main()
    {
        // Load the source PDF
        using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
        {
            // Access first page resources
            var firstPage = pdfDocument.Pages[1];
            var resourcesEditor = new DictionaryEditor(firstPage.Resources);

            // Ensure ExtGState dictionary exists
            CosPdfDictionary extGStateDict;
            if (resourcesEditor.ContainsKey("ExtGState"))
                extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
            else
            {
                extGStateDict = new CosPdfDictionary(pdfDocument);
                resourcesEditor["ExtGState"] = extGStateDict;
            }

            // Create a new graphics state (opacity + blend mode)
            var graphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            var entries = new[]
            {
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
            };
            foreach (var e in entries) graphicsState.Add(e);

            // Register the graphics state as GS0
            extGStateDict.Add("GS0", graphicsState);

            // OPTIONAL: draw a semi‑transparent rectangle using GS0
            var builder = new ContentBuilder(pdfDocument);
            builder.SetGraphicsState("GS0");
            builder.SetFillColor(Color.FromRgb(255, 0, 0)); // red
            builder.Rectangle(100, 500, 200, 100);
            builder.FillPath();
            firstPage.Contents.Add(builder);

            // Save the result
            pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
        }

        Console.WriteLine("PDF transparency changed and saved to output.pdf");
    }
}
```

### Kết quả mong đợi

* Tệp `output.pdf` được tạo trong thư mục đã chỉ định.
* Nếu bạn mở PDF, sẽ thấy một hình chữ nhật màu đỏ có phần tô màu 50 % trong suốt trong khi viền vẫn hoàn toàn không trong suốt.
* Bất kỳ đối tượng nào khác tham chiếu `GS0` (ví dụ: watermark) sẽ kế thừa cùng độ trong suốt và chế độ hòa trộn.

## Câu hỏi thường gặp & xử lý các trường hợp đặc biệt

| Câu hỏi | Trả lời |
|----------|--------|
| **Tôi có thể chỉ thay đổi độ trong suốt nét vẽ không?** | Đặt `CA` thành giá trị mong muốn và để `ca` ở `1`. |
| **Các chế độ hòa trộn nào được hỗ trợ?** | Tất cả các chế độ hòa trộn PDF tiêu chuẩn (`Normal`, `Multiply`, `Screen`, `Overlay`, v.v.) được chấp nhận qua mục `BM`. |
| **Tôi có cần dọn dẹp từ điển sau khi sử dụng không?** | Không. Các đối tượng `CosPdfDictionary` được Aspose.Pdf quản lý và sẽ được ghi vào tệp khi bạn gọi `Save`. |
| **Điều này hoạt động như thế nào với PDF được mã hóa?** | Tải tài liệu với mật khẩu phù hợp (`new Document(path, password)`). Việc thao tác trạng thái đồ họa hoạt động tương tự một khi tài liệu đã được giải mã trong bộ nhớ. |
| **Có thể áp dụng cùng một trạng thái đồ họa cho nhiều trang không?** | Có. Thêm mục `GS0` vào từ điển `ExtGState` của mỗi trang, hoặc tạo một từ điển chia sẻ duy nhất trong tài nguyên toàn cục của tài liệu và tham chiếu nó từ mỗi trang. |

## Mẹo và thực hành tốt nhất

* **Pro tip:** Giữ tên trạng thái đồ họa ngắn gọn nhưng mô tả (`GS_Watermark`, `GS_Overlay`). Điều này tránh xung đột tên và giúp việc gỡ lỗi dễ dàng hơn.
* **Watch out for:** Ghi đè một mục `ExtGState` hiện có một cách vô tình. Luôn kiểm tra `resourcesEditor.ContainsKey("ExtGState")` trước khi tạo từ điển mới.
* **Performance note:** Thay đổi các đối tượng COS cấp thấp rất nhanh, nhưng nếu bạn cần xử lý hàng nghìn trang, hãy cân nhắc thực hiện thay đổi theo lô để giảm áp lực bộ nhớ.

## Các bước tiếp theo

Bây giờ bạn đã biết cách **thay đổi độ trong suốt PDF**, bạn có thể khám phá các chủ đề liên quan như:

* Thêm **watermarks** với độ trong suốt tùy chỉnh (`PDF opacity C#`).
* Sử dụng **các chế độ hòa trộn khác nhau** để đạt hiệu ứng nghệ thuật (`blend mode PDF`).
* Tạo thư viện **trạng thái đồ họa** có thể tái sử dụng cho việc tạo tài liệu quy mô lớn (`Aspose.Pdf graphics state`).

Thử nghiệm với việc thay đổi các giá trị `ca` và `CA`, hoặc thay hình chữ nhật đỏ bằng hình ảnh hoặc lớp chữ. Nguyên tắc vẫn giống nhau—chỉ cần tham chiếu trạng thái đồ họa `GS0` trước khi vẽ nội dung mới.

---

*Bạn đã học cách thay đổi độ trong suốt PDF bằng Aspose.Pdf trong C#. Áp dụng các kỹ thuật này để nâng cao báo cáo, hoá đơn, hoặc bất kỳ đầu ra dựa trên PDF nào nơi mà sự tinh tế về hình ảnh quan trọng.*

## Bạn nên học gì tiếp theo?

Các tutorial sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật đã trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh với giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Thay đổi độ trong suốt PDF với Aspose.PDF – Hướng dẫn C# đầy đủ](/pdf/english/net/programming-with-stamps-and-watermarks/change-pdf-opacity-with-aspose-pdf-complete-c-guide/)
- [Thay đổi độ trong suốt PDF trong C# – Hướng dẫn Aspose đầy đủ](/pdf/english/net/programming-with-stamps-and-watermarks/change-pdf-opacity-in-c-complete-aspose-guide/)
- [Thêm độ trong suốt vào PDF bằng Aspose – Hướng dẫn C# đầy đủ](/pdf/english/net/programming-with-operators/add-transparency-to-pdf-using-aspose-complete-c-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}