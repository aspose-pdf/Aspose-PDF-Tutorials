---
category: general
date: 2026-11-22
description: Thêm tính trong suốt vào PDF bằng Aspose.PDF cho C#. Tìm hiểu cách thay
  đổi độ trong suốt của PDF với ví dụ rõ ràng, từng bước.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add transparency to pdf
- how to change pdf opacity
- Aspose.PDF opacity
- PDF graphics state C#
- PDF blend mode example
language: vi
lastmod: 2026-11-22
og_description: Thêm độ trong suốt vào PDF với Aspose.PDF cho C#. Hướng dẫn này chỉ
  cách thay đổi độ trong suốt của PDF một cách nhanh chóng và đáng tin cậy.
og_image_alt: Screenshot of a PDF page showing translucent graphics after adding transparency
og_title: Thêm độ trong suốt vào PDF trong C# – hướng dẫn đầy đủ Aspose.PDF
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Add transparency to PDF using Aspose.PDF for C#. Learn how to change
    PDF opacity with a clear, step‑by‑step example.
  headline: How to add transparency to PDF in C# with Aspose.PDF
  type: TechArticle
tags:
- PDF
- C#
- Aspose.PDF
title: Cách thêm độ trong suốt vào PDF trong C# với Aspose.PDF
url: /vi/net/images-graphics/how-to-add-transparency-to-pdf-in-c-with-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách thêm độ trong suốt vào PDF trong C# với Aspose.PDF

Nếu bạn cần **thêm độ trong suốt vào file PDF**, hướng dẫn này sẽ cho bạn một giải pháp hoàn chỉnh bằng cách sử dụng Aspose.PDF cho .NET. Bạn sẽ thấy **cách thay đổi độ mờ của PDF** cho đồ họa vector, văn bản hoặc hình ảnh mà không rời khỏi môi trường C#.

Bài tutorial bao gồm mọi bước — từ tải tài liệu, chỉnh sửa trạng thái đồ họa của trang và lưu kết quả. Khi hoàn thành, bạn có thể tạo ra các PDF mà các phần tử được chọn hiển thị bán trong suốt, hữu ích cho watermark, hiệu ứng lớp phủ hoặc mô phỏng thiết kế.

## Yêu cầu trước

Trước khi bắt đầu, hãy chắc chắn rằng bạn có:

* .NET 6.0 hoặc mới hơn (mã cũng hoạt động với .NET Framework 4.8)
* Giấy phép Aspose.PDF cho .NET hợp lệ hoặc khóa đánh giá tạm thời
* Visual Studio 2022 (hoặc bất kỳ IDE nào hỗ trợ C#)
* Một file PDF đầu vào có tên `input.pdf` được đặt trong một thư mục đã biết

Những mục này đảm bảo mã chạy mà không cần cấu hình thêm.

## Bước 1: Tải tài liệu PDF

Hoạt động đầu tiên là mở file PDF hiện có. Aspose.PDF đại diện cho toàn bộ file bằng lớp `Document`.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Cos;

// Load the source PDF
var inputPath = @"C:\MyFiles\input.pdf";
var doc = new Document(inputPath);
```

*Lý do bước này quan trọng*: Việc tải tài liệu tạo ra một mô hình trong bộ nhớ cho phép bạn kiểm tra các trang, tài nguyên và luồng nội dung. Nếu không có đối tượng này, bạn không thể chỉnh sửa trạng thái đồ họa.

## Bước 2: Truy cập từ điển tài nguyên của trang đầu tiên

Độ trong suốt được áp dụng thông qua một **trạng thái đồ họa** được lưu trong từ điển tài nguyên của trang. Bạn cần một `DictionaryEditor` để chỉnh sửa từ điển đó.

```csharp
// Get the first page (pages are 1‑based)
var page = doc.Pages[1];

// Open the resource dictionary for editing
var dictEditor = new DictionaryEditor(page.Resources);
var extGState = dictEditor["ExtGState"].ToCosPdfDictionary();
```

Nếu trang chưa chứa mục `ExtGState`, Aspose.PDF sẽ tự động tạo một từ điển rỗng khi bạn yêu cầu. Tính linh hoạt này có nghĩa là cùng một đoạn mã hoạt động cho các PDF đã sử dụng độ trong suốt hoặc chưa bao giờ có.

## Bước 3: Tạo một trạng thái đồ họa mới với các giá trị độ mờ

Một trạng thái đồ họa chứa các tham số như độ mờ nền (`ca`), độ mờ viền (`CA`) và chế độ hòa trộn (`BM`). Khối mã dưới đây xây dựng một từ điển định nghĩa độ mờ nền 50 % trong khi giữ viền hoàn toàn không trong suốt.

```csharp
// Build a new graphics state dictionary
var graphicsState = CosPdfDictionary.CreateEmptyDictionary(doc);

// Stroke opacity – fully opaque (value between 0 and 1)
graphicsState.Add("CA", new CosPdfNumber(1));

// Fill opacity – 50 % transparent
graphicsState.Add("ca", new CosPdfNumber(0.5));

// Blend mode – Normal (other modes: Multiply, Screen, etc.)
graphicsState.Add("BM", new CosPdfName("Normal"));
```

*Lý do các khóa này*:
* `CA` điều khiển độ mờ của các đường viền (đường, khung).
* `ca` điều khiển độ mờ của các đối tượng được tô đầy (văn bản, hình ảnh).
* `BM` chọn cách đối tượng trong suốt hòa trộn với nội dung nền; `Normal` là lựa chọn phổ biến nhất.

## Bước 4: Đăng ký trạng thái đồ họa vào tài nguyên của trang

Sau khi tạo trạng thái đồ họa, bạn phải thêm nó vào từ điển `ExtGState` của trang dưới một tên duy nhất (ví dụ, `GS0`). Các luồng nội dung sau đó có thể tham chiếu tới tên này để áp dụng các cài đặt độ mờ.

```csharp
// Add the new graphics state to the resource dictionary
extGState.Add("GS0", graphicsState);
```

Tại thời điểm này, file PDF chứa một trạng thái đồ họa có thể tái sử dụng có tên `GS0`. Bất kỳ lệnh vẽ nào tham chiếu `/GS0 gs` sẽ được hiển thị với độ mờ đã chỉ định.

## Bước 5: Áp dụng trạng thái đồ họa vào nội dung trang (tùy chọn)

Nếu bạn muốn ảnh hưởng tới nội dung hiện có, cần chèn một lệnh vào đầu luồng nội dung của trang. Đoạn mã dưới đây minh họa cách chèn trước (prepend) toán tử trạng thái đồ họa.

```csharp
// Retrieve the original content stream
var content = page.Contents[1];

// Insert the graphics state operator at the start of the stream
content.Contents.Insert(0, new CosPdfLiteral("GS0 gs"));
```

*Khi nào nên dùng bước này*: Nếu PDF đã chứa các lệnh vẽ và bạn muốn chúng trở nên bán trong suốt, hãy chèn toán tử vào đầu. Nếu bạn dự định thêm các đối tượng mới sau này, bạn có thể tham chiếu `GS0` trực tiếp khi tạo các đối tượng đó.

## Bước 6: Lưu PDF đã chỉnh sửa

Cuối cùng, ghi tài liệu đã cập nhật ra đĩa.

```csharp
var outputPath = @"C:\MyFiles\output.pdf";
doc.Save(outputPath);
```

File `output.pdf` kết quả sẽ hiển thị các phần tử nền của trang đầu tiên ở độ mờ 50 % trong khi các đường viền vẫn hiển thị đầy đủ. Mở file trong bất kỳ trình xem PDF nào để xác nhận hiệu ứng.

## Cách thay đổi độ mờ PDF cho nhiều trang

Cách tiếp cận tương tự hoạt động cho bất kỳ số trang nào. Lặp qua `doc.Pages` và lặp lại các bước 2‑5, gán một tên trạng thái đồ họa riêng cho mỗi trang (ví dụ, `GS1`, `GS2`). Dưới đây là một phiên bản ngắn gọn:

```csharp
for (int i = 1; i <= doc.Pages.Count; i++)
{
    var pg = doc.Pages[i];
    var editor = new DictionaryEditor(pg.Resources);
    var ext = editor["ExtGState"].ToCosPdfDictionary();

    var gs = CosPdfDictionary.CreateEmptyDictionary(doc);
    gs.Add("CA", new CosPdfNumber(1));
    gs.Add("ca", new CosPdfNumber(0.75)); // 75% fill opacity
    gs.Add("BM", new CosPdfName("Normal"));

    var gsName = $"GS{i - 1}";
    ext.Add(gsName, gs);

    var cnt = pg.Contents[1];
    cnt.Contents.Insert(0, new CosPdfLiteral($"{gsName} gs"));
}
```

Vòng lặp này giảm thiểu việc lặp lại mã và minh họa **cách thay đổi độ mờ PDF** trên toàn bộ tài liệu.

## Các lỗi thường gặp và mẹo thực hành

| Vấn đề | Nguyên nhân | Giải pháp đề xuất |
|-------|------------|-------------------|
| Thiếu mục `ExtGState` | Một số PDF chưa tạo từ điển trạng thái đồ họa | `DictionaryEditor` sẽ tự động tạo; không cần mã bổ sung |
| Độ mờ không hiển thị | Trình xem lưu bộ nhớ đệm của trang gốc | Xóa bộ nhớ đệm của trình xem hoặc mở lại file |
| Chế độ hòa trộn không phù hợp | Dùng `Multiply` trên nền tối có thể làm đối tượng biến mất | Thử các giá trị `BM` khác (`Normal`, `Screen`, `Overlay`) để đạt hiệu ứng mong muốn |
| Nhiều trạng thái đồ họa xung đột | Sử dụng cùng một tên (`GS0`) trên các trang khác nhau ghi đè định nghĩa trước | Dùng tên duy nhất cho mỗi trang (`GS0`, `GS1`, …) |

## Ví dụ hoàn chỉnh

Dưới đây là một chương trình tự chứa mà bạn có thể sao chép, dán và chạy. Nó bao gồm tất cả các câu lệnh `using`, xử lý lỗi và chú thích.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Cos;

class AddTransparencyDemo
{
    static void Main()
    {
        // Paths – adjust to your environment
        const string inputPath = @"C:\MyFiles\input.pdf";
        const string outputPath = @"C:\MyFiles\output.pdf";

        // Load the PDF
        var doc = new Document(inputPath);

        // Process each page
        for (int pageIndex = 1; pageIndex <= doc.Pages.Count; pageIndex++)
        {
            var page = doc.Pages[pageIndex];
            var dictEditor = new DictionaryEditor(page.Resources);
            var extGState = dictEditor["ExtGState"].ToCosPdfDictionary();

            // Create a graphics state with 60% fill opacity
            var graphicsState = CosPdfDictionary.CreateEmptyDictionary(doc);
            graphicsState.Add("CA", new CosPdfNumber(1));               // stroke opacity
            graphicsState.Add("ca", new CosPdfNumber(0.6));             // fill opacity
            graphicsState.Add("BM", new CosPdfName("Normal"));         // blend mode

            // Unique name for this page
            string gsName = $"GS{pageIndex - 1}";
            extGState.Add(gsName, graphicsState);

            // Prepend the graphics state operator to the page content
            var content = page.Contents[1];
            content.Contents.Insert(0, new CosPdfLiteral($"{gsName} gs"));
        }

        // Save the result
        doc.Save(outputPath);
        Console.WriteLine($"PDF saved with transparency at: {outputPath}");
    }
}
```

**Kết quả mong đợi**: Khi mở `output.pdf`, bất kỳ hình dạng, văn bản hoặc hình ảnh nào được tô đầy trên mỗi trang sẽ có độ mờ 60 %, trong khi viền vẫn hoàn toàn không trong suốt. Thay đổi trực quan này ngay lập tức và hoạt động trong Adobe Acrobat, Edge, Chrome hoặc bất kỳ trình xem PDF nào tôn trọng trạng thái đồ họa PDF.

## Kết luận

Bây giờ bạn đã biết cách **thêm độ trong suốt vào file PDF** bằng Aspose.PDF cho C#. Bài tutorial đã bao gồm việc tải tài liệu, chỉnh sửa từ điển tài nguyên của trang, tạo trạng thái đồ họa tùy chỉnh và lưu file đã chỉnh sửa. Bạn cũng đã học **cách thay đổi độ mờ PDF** cho một hoặc nhiều trang, cùng với các mẹo thực tế để tránh những lỗi thường gặp.

Tiếp theo, hãy khám phá các chủ đề liên quan như:

* Thêm watermark hình ảnh với độ trong suốt thay đổi
* Sử dụng các chế độ hòa trộn khác nhau (`Multiply`, `Screen`) để tạo hiệu ứng sáng tạo
* Kết hợp độ trong suốt với chú thích PDF

Thử nghiệm các biến thể này để tùy chỉnh đầu ra PDF cho yêu cầu thị giác của dự án. Chúc bạn lập trình vui vẻ!

## Bạn nên học gì tiếp theo?

Các tutorial sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật đã trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm mã mẫu đầy đủ với các giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [How to add graphics state pdf and control transparency with Aspose.PDF](/pdf/english/net/images-graphics/how-to-add-graphics-state-pdf-and-control-transparency-with/)
- [How to set opacity in a PDF and how to change blend mode with Aspose.Pdf](/pdf/hongkong/net/images-graphics/how-to-set-opacity-in-a-pdf-and-how-to-change-blend-mode-wit/)
- [How to add transparency to PDF and draw a rectangle on PDF with Aspose.PDF](/pdf/english/net/images-graphics/how-to-add-transparency-to-pdf-and-draw-a-rectangle-on-pdf-w/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}