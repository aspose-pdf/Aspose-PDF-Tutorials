---
category: general
date: 2026-02-28
description: Tạo tài liệu PDF C# với đánh số Bates. Tìm hiểu cách thêm đánh số Bates
  vào PDF, đặt tiền tố và tạo các số PDF tuần tự trong một hướng dẫn duy nhất.
draft: false
keywords:
- create pdf document c#
- add bates numbering pdf
- how to add bates
- add document identification numbers
- add sequential pdf numbers
language: vi
og_description: Tạo tài liệu PDF bằng C# với số Bates. Hướng dẫn này chỉ cách thêm
  số Bates vào PDF, đặt tiền tố tùy chỉnh và tạo các số PDF tuần tự.
og_title: Tạo tài liệu PDF bằng C# – Thêm số Bates
tags:
- Aspose.PDF
- C#
- PDF automation
title: Tạo tài liệu PDF bằng C# – Hướng dẫn thêm số Bates
url: /vi/net/document-creation/create-pdf-document-c-add-bates-numbering-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo PDF Document C# – Hướng dẫn Thêm Số Bates

Bạn đã bao giờ tự hỏi làm thế nào để **create PDF document C#** mà đã có sẵn một định danh duy nhất trên mỗi trang chưa? Đó là một vấn đề phổ biến khi bạn cần theo dõi các hồ sơ pháp lý, hồ sơ tòa án, hoặc bất kỳ lô PDF nào cần có thể tìm kiếm bằng một số. Tin tốt là gì? Với Aspose.PDF bạn có thể thêm số Bates chỉ trong vài dòng mã—không cần chỉnh sửa thủ công.

Trong hướng dẫn này, chúng tôi sẽ đi qua toàn bộ quy trình: tải một PDF hiện có, cấu hình **add bates numbering pdf**, áp dụng các số, và cuối cùng lưu kết quả. Khi kết thúc, bạn sẽ có thể **add document identification numbers** và thậm chí **add sequential PDF numbers** một cách tự động, tất cả từ C#.

## Yêu cầu trước

- .NET 6.0 trở lên (API cũng hoạt động với .NET Framework 4.5+)
- Một bản sao có giấy phép của **Aspose.PDF for .NET** (bản dùng thử miễn phí đủ cho việc thử nghiệm)
- Một tệp PDF đầu vào mà bạn muốn đánh số (chúng tôi sẽ gọi nó là `input.pdf`)
- Visual Studio 2022 (hoặc bất kỳ IDE nào bạn thích)

Không cần bất kỳ gói NuGet bổ sung nào ngoài Aspose.PDF.

![Create PDF Document C# with Bates numbering](https://example.com/image.png "Create PDF Document C# example")

## Bước 1: Tải tài liệu PDF nguồn

Trước khi bạn có thể **add bates numbering pdf**, bạn cần một đối tượng `Document` đại diện cho tệp trên đĩa.

```csharp
using Aspose.Pdf;

// Load the source PDF document
var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");
```

*Tại sao điều này quan trọng*: Lớp `Document` là điểm vào cho mọi thao tác trong Aspose.PDF. Nó trừu tượng hoá hệ thống tệp, cho phép bạn làm việc với các trang, chú thích và siêu dữ liệu mà không cần chạm vào các byte thô.

> **Mẹo:** Nếu bạn đang xử lý nhiều tệp trong một vòng lặp, hãy tái sử dụng cùng một thể hiện `Document` chỉ khi nguồn giống hệt; nếu không, hãy tạo một đối tượng mới cho mỗi tệp để tránh rò rỉ bộ nhớ.

## Bước 2: Định nghĩa tùy chọn Bates Numbering

Đây là nơi phần **how to add bates** trở nên cụ thể. Bạn cấu hình một đối tượng `BatesNumberingOptions` để cho Aspose biết tiền tố nên là gì, bắt đầu từ đâu, và kích thước phông chữ cần hiển thị.

```csharp
// Define Bates numbering options (prefix, start number, font size)
var batesOptions = new BatesNumberingOptions
{
    Prefix = "ABC-",   // You can change this to any string you need
    Start = 1000,      // Starting number – useful for continuous numbering across batches
    FontSize = 9       // Small enough to fit in the margin but still readable
};
```

*Tại sao điều này quan trọng*: Thuộc tính `Prefix` cho phép bạn nhúng một định danh vụ việc (ví dụ, “ABC-”). Thuộc tính `Start` là cần thiết khi bạn **adding sequential PDF numbers** trên nhiều tài liệu—chỉ cần tăng giá trị lên. Và `FontSize` đảm bảo các số không che khuất nội dung hiện có.

## Bước 3: Áp dụng Bates Numbering cho toàn bộ tài liệu

Bây giờ chúng ta thực sự dán các số lên mỗi trang. Lớp `BatesNumbering` thực hiện toàn bộ công việc nặng nhọc.

```csharp
// Apply Bates numbering to the entire document
var bates = new BatesNumbering();
bates.AddBatesNumbering(pdfDocument, batesOptions);
```

*Tại sao điều này quan trọng*: Bên trong, Aspose duyệt qua mỗi trang, tính toán số thích hợp (Prefix + (Start + pageIndex)), và vẽ nó ở góc dưới‑phải theo mặc định. Bạn có thể tùy chỉnh vị trí sau này, nhưng mặc định phù hợp với hầu hết các tài liệu kiểu pháp lý.

> **Câu hỏi thường gặp:** *Nếu tôi chỉ cần đánh số một phần các trang thì sao?*  
> Sử dụng overload `AddBatesNumbering(Document, BatesNumberingOptions, int startPage, int endPage)` để giới hạn phạm vi.

## Bước 4: Lưu PDF với Bates Numbers đã áp dụng

Bước cuối cùng là ghi tài liệu đã sửa đổi trở lại đĩa.

```csharp
// Save the PDF with Bates numbers applied
pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
```

*Tại sao điều này quan trọng*: Phương thức `Save` giữ nguyên định dạng tệp gốc, vì vậy bạn sẽ có một PDF tiêu chuẩn mà bất kỳ trình xem nào cũng mở được—đầy đủ **add document identification numbers** trên mỗi trang.

## Ví dụ hoạt động đầy đủ

Kết hợp tất cả lại, đây là một chương trình tự chứa mà bạn có thể dán vào một ứng dụng console mới và chạy ngay lập tức.

```csharp
using System;
using Aspose.Pdf;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the source PDF document
            var inputPath = @"YOUR_DIRECTORY/input.pdf";
            var pdfDocument = new Document(inputPath);

            // 2️⃣ Define Bates numbering options (prefix, start number, font size)
            var batesOptions = new BatesNumberingOptions
            {
                Prefix = "ABC-",
                Start = 1000,
                FontSize = 9
            };

            // 3️⃣ Apply Bates numbering to the entire document
            var bates = new BatesNumbering();
            bates.AddBatesNumbering(pdfDocument, batesOptions);

            // 4️⃣ Save the PDF with Bates numbers applied
            var outputPath = @"YOUR_DIRECTORY/output.pdf";
            pdfDocument.Save(outputPath);

            Console.WriteLine($"Bates numbering added successfully. Output saved to {outputPath}");
        }
    }
}
```

**Kết quả mong đợi:** Mở `output.pdf` trong bất kỳ trình xem nào; bạn sẽ thấy “ABC‑1000”, “ABC‑1001”, … được in trên góc dưới‑phải của mỗi trang. Các số là văn bản có thể chọn, vì vậy chúng có thể tìm kiếm và sao chép—đúng như bạn mong đợi từ một triển khai **add sequential PDF numbers** đúng chuẩn.

## Các trường hợp đặc biệt & biến thể

### Định vị tùy chỉnh

Nếu góc mặc định trùng với chân trang hiện có, bạn có thể dịch vị trí:

```csharp
batesOptions.Position = new Position(10, 10); // X, Y from the bottom‑left
```

### Định dạng số khác nhau

Muốn số có đệm số 0 (ví dụ, 001000)? Sử dụng `NumberFormat`:

```csharp
batesOptions.NumberFormat = "D6"; // Pads to 6 digits
```

### Nhiều tệp trong một lô

Khi xử lý nhiều PDF, duy trì một bộ đếm chạy:

```csharp
int globalStart = 5000;
foreach (var file in Directory.GetFiles(@"YOUR_DIRECTORY\Batch", "*.pdf"))
{
    var doc = new Document(file);
    var opts = new BatesNumberingOptions
    {
        Prefix = "BATCH-",
        Start = globalStart,
        FontSize = 9
    };
    new BatesNumbering().AddBatesNumbering(doc, opts);
    doc.Save(Path.ChangeExtension(file, ".bated.pdf"));
    globalStart += doc.Pages.Count; // Increment for the next file
}
```

### Xử lý PDF có mật khẩu

Nếu PDF nguồn được mã hoá, truyền mật khẩu khi tạo `Document`:

```csharp
var pdfDocument = new Document("protected.pdf", new LoadOptions { Password = "mySecret" });
```

## Câu hỏi thường gặp

| Câu hỏi | Trả lời |
|----------|--------|
| **Tôi có thể sử dụng thư viện khác không?** | Có, các thư viện như iTextSharp hoặc PdfSharp cũng hỗ trợ chèn văn bản ở mức trang, nhưng Aspose.PDF cung cấp API đơn giản nhất cho Bates numbering. |
| **Điều này có ảnh hưởng đến kích thước tệp không?** | Thêm vài byte văn bản mỗi trang là không đáng kể; kích thước đầu ra thường tăng ít hơn 1 KB mỗi trang. |
| **Số thứ tự có thể tìm kiếm được không?** | Chắc chắn. Aspose ghi các số dưới dạng đối tượng văn bản, không phải hình ảnh, vì vậy chúng được các trình đọc PDF lập chỉ mục. |
| **Nếu tôi cần một phông chữ khác thì sao?** | Đặt `batesOptions.Font` thành một đối tượng `Font` (ví dụ, `FontRepository.FindFont("Arial")`). |

## Kết luận

Chúng tôi vừa trình diễn cách **create PDF document C#** và ngay lập tức **add bates numbering pdf** bằng Aspose.PDF. Quy trình đơn giản, đáng tin cậy và hoàn toàn có thể lập trình—hoàn hảo cho các công ty luật, cơ quan chính phủ, hoặc bất kỳ tổ chức nào cần **add document identification numbers** và **add sequential PDF numbers** cho các lô tệp lớn.

Hãy lấy nền tảng này và thử nghiệm: thử các tiền tố khác nhau cho các phòng ban, chuỗi đánh số qua nhiều tệp, hoặc nhúng mã QR bên cạnh số Bates để tăng khả năng truy xuất. Không gì là không thể khi bạn đã nắm vững quy trình cốt lõi.

Nếu bạn thấy hướng dẫn này hữu ích, hãy chia sẻ, để lại bình luận, hoặc khám phá các hướng dẫn khác của chúng tôi về thao tác PDF với C#. Chúc lập trình vui vẻ!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}