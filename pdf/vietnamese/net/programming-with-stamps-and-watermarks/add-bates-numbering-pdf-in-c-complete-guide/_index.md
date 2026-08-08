---
category: general
date: 2026-05-27
description: Thêm số Bates vào PDF bằng Aspose.Pdf trong C#. Tìm hiểu cách thêm số
  Bates nhanh chóng, tùy chỉnh định dạng và tự động gắn thẻ tài liệu pháp lý.
draft: false
keywords:
- add bates numbering pdf
- how to add bates numbering
language: vi
og_description: Thêm đánh số Bates vào PDF với Aspose.Pdf trong C#. Hướng dẫn này
  cho thấy cách thêm đánh số Bates, cấu hình tiền tố và lưu kết quả.
og_title: Thêm đánh số Bates vào PDF trong C# – Hướng dẫn từng bước
schemas:
- author: Aspose
  dateModified: '2026-05-27'
  description: Add Bates numbering PDF using Aspose.Pdf in C#. Learn how to add Bates
    numbering quickly, customize format, and automate legal document tagging.
  headline: Add Bates Numbering PDF in C# – Complete Guide
  type: TechArticle
- description: Add Bates numbering PDF using Aspose.Pdf in C#. Learn how to add Bates
    numbering quickly, customize format, and automate legal document tagging.
  name: Add Bates Numbering PDF in C# – Complete Guide
  steps:
  - name: Expected Output
    text: 'When you run the program, the console prints:'
  - name: Can I position the Bates number elsewhere?
    text: Yes. Use the `BatesNumberingArtifact`’s `Location` property (e.g., `Location
      = new Position(10, 10)`) to place the number at custom X/Y coordinates. You
      can also set `HorizontalAlignment` and `VerticalAlignment` for more control.
  - name: What if my PDF has thousands of pages?
    text: Aspose.Pdf streams pages efficiently, but it’s still a good idea to process
      in batches if you hit memory limits. The `Document` class also supports `PdfConverter`
      for incremental saving.
  - name: How do I change the font or color?
    text: 'Wrap the artifact in a `TextState` object:'
  - name: Do I need a license for production use?
    text: A licensed version removes evaluation watermarks and unlocks full performance.
      The free trial works fine for testing and proof‑of‑concepts.
  type: HowTo
tags:
- Aspose.Pdf
- C#
- Bates numbering
- PDF automation
title: Thêm số Bates vào PDF bằng C# – Hướng dẫn toàn diện
url: /vi/net/programming-with-stamps-and-watermarks/add-bates-numbering-pdf-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Thêm Số Bates vào PDF trong C# – Hướng Dẫn Toàn Diện

Bạn đã bao giờ tự hỏi **cách thêm số Bates** vào một tệp PDF mà không phải tốn hàng giờ chỉnh sửa bằng các công cụ thủ công chưa? Bạn không phải là người duy nhất—các đội ngũ pháp lý, kiểm toán viên và chuyên gia e‑discovery đều cần một cách đáng tin cậy để **thêm số Bates vào các tệp PDF** một cách lập trình.  

Trong hướng dẫn này, chúng tôi sẽ trình bày một giải pháp ngắn gọn, từ đầu đến cuối bằng cách sử dụng Aspose.Pdf cho .NET, để bạn có thể chèn số Bates vào bất kỳ tài liệu nào chỉ với vài dòng mã C#.

## Những gì bạn sẽ học

- Cách mở một tệp PDF hiện có bằng Aspose.Pdf  
- Cách tạo một BatesNumberingArtifact và tinh chỉnh định dạng của nó  
- Cách gắn artifact vào mỗi trang (hoặc chỉ trang đầu)  
- Cách lưu tệp đã cập nhật và xác minh kết quả  

Bạn không cần kinh nghiệm trước với Aspose—chỉ cần hiểu cơ bản về C# và .NET. Khi kết thúc, bạn sẽ có một đoạn mã có thể tái sử dụng và có thể sao chép‑dán vào bất kỳ dự án nào.

## Yêu cầu trước

- .NET 6.0 trở lên (mã cũng hoạt động trên .NET Framework 4.7+)  
- Gói NuGet Aspose.Pdf cho .NET (`Install-Package Aspose.Pdf`)  
- Một tệp PDF nguồn mà bạn muốn gắn thẻ (đặt nó trong một thư mục bạn có thể tham chiếu)

> **Mẹo chuyên nghiệp:** Nếu bạn chưa có giấy phép, Aspose cung cấp một khóa tạm thời miễn phí giúp loại bỏ watermark đánh giá.

## Bước 1 – Mở Tài liệu PDF Nguồn  

Đầu tiên chúng ta cần một đối tượng `Document` đại diện cho tệp trên đĩa. Hãy nghĩ đây như việc tải một canvas trống mà sau này chúng ta sẽ vẽ các số Bates lên.

```csharp
using Aspose.Pdf;
using System;

class Program
{
    static void Main()
    {
        // Adjust the path to point at your source PDF
        string sourcePath = @"C:\Docs\source.pdf";

        // Load the PDF – this is where we start to add Bates numbering
        using (var pdfDocument = new Document(sourcePath))
        {
            // The rest of the logic lives inside this using block
        }
    }
}
```

**Tại sao điều này quan trọng:** Mở tài liệu trong một khối `using` đảm bảo tất cả tài nguyên không quản lý được giải phóng kịp thời, điều này đặc biệt quan trọng đối với các PDF lớn.

## Bước 2 – Tạo một BatesNumberingArtifact  

*BatesNumberingArtifact* là cách của Aspose để mô tả cách các số sẽ hiển thị. Bạn có thể đặt tiền tố, số bắt đầu, bước tăng, và thậm chí một chuỗi định dạng tùy chỉnh.

```csharp
// Step 2: Define the Bates numbering artifact
var batesNumbering = new BatesNumberingArtifact
{
    Prefix = "ABC",            // Text that appears before each number
    StartNumber = 1000,        // First number in the sequence
    Increment = 1,             // Step between consecutive numbers
    Format = "{0:D5}"          // Zero‑padded 5‑digit number (e.g., 01000)
};
```

**Tại sao bạn có thể muốn thay đổi các giá trị này:**  
- **Prefix** hữu ích cho các ID vụ việc (“CASE‑”, “DOC‑”).  
- **StartNumber** cho phép bạn tiếp tục một chuỗi trước đó.  
- **Increment** có thể đặt là 2 nếu bạn cần đánh số lẻ/chẵn.  
- **Format** hỗ trợ bất kỳ định dạng hợp thành .NET nào; `{0:D5}` đảm bảo năm chữ số với số 0 phía trước.

## Bước 3 – Gắn Artifact vào các Trang Mong Muốn  

Bạn có thể thêm artifact vào một trang duy nhất, một phạm vi, hoặc toàn bộ tài liệu. Đối với hầu hết quy trình pháp lý, chúng tôi gắn nó vào *mọi* trang, nhưng ví dụ dưới đây minh họa trường hợp tối thiểu—thêm vào trang đầu tiên.

```csharp
// Step 3: Attach the artifact to the first page (index is 1‑based)
pdfDocument.Pages[1].Artifacts.Add(batesNumbering);
```

Nếu bạn cần bao phủ tất cả các trang, hãy lặp qua chúng:

```csharp
foreach (Page page in pdfDocument.Pages)
{
    page.Artifacts.Add(batesNumbering);
}
```

**Tại sao bước này quan trọng:** Artifacts được vẽ *sau* nội dung trang, vì vậy các số xuất hiện trên đầu văn bản hiện có mà không làm thay đổi bố cục gốc.

## Bước 4 – Lưu PDF Đã Sửa Đổi  

Cuối cùng, ghi các thay đổi trở lại đĩa. Bạn có thể ghi đè lên tệp gốc hoặc tạo một tệp mới—ở đây chúng tôi sẽ tạo một bản sao mới có tên `bates.pdf`.

```csharp
// Step 4: Persist the changes
string outputPath = @"C:\Docs\bates.pdf";
pdfDocument.Save(outputPath);

Console.WriteLine($"Bates numbering added successfully. File saved to: {outputPath}");
```

Khi bạn mở `bates.pdf` bạn sẽ thấy “ABC01000” (hoặc bất kỳ định dạng nào bạn đã chọn) được dán ở vị trí mặc định—thường là góc dưới‑phải.

## Ví dụ Hoạt Động Đầy Đủ  

Kết hợp tất cả lại, đây là chương trình hoàn chỉnh mà bạn có thể biên dịch và chạy:

```csharp
using Aspose.Pdf;
using System;

class AddBatesNumbering
{
    static void Main()
    {
        // -----------------------------------------------------------------
        // 1️⃣ Open the source PDF
        // -----------------------------------------------------------------
        string sourcePath = @"C:\Docs\source.pdf";
        using (var pdfDocument = new Document(sourcePath))
        {
            // -----------------------------------------------------------------
            // 2️⃣ Create and configure the Bates numbering artifact
            // -----------------------------------------------------------------
            var batesNumbering = new BatesNumberingArtifact
            {
                Prefix = "ABC",
                StartNumber = 1000,
                Increment = 1,
                Format = "{0:D5}"
            };

            // -----------------------------------------------------------------
            // 3️⃣ Attach the artifact to each page (or a specific page)
            // -----------------------------------------------------------------
            foreach (Page page in pdfDocument.Pages)
            {
                page.Artifacts.Add(batesNumbering);
            }

            // -----------------------------------------------------------------
            // 4️⃣ Save the new PDF
            // -----------------------------------------------------------------
            string outputPath = @"C:\Docs\bates.pdf";
            pdfDocument.Save(outputPath);

            Console.WriteLine($"Bates numbers added. Output: {outputPath}");
        }
    }
}
```

### Kết Quả Dự Kiến

Khi bạn chạy chương trình, console sẽ in ra:

```
Bates numbers added. Output: C:\Docs\bates.pdf
```

Mở `bates.pdf` sẽ hiển thị tiền tố “ABC” tiếp theo là chuỗi năm chữ số có số 0 phía trước trên mỗi trang—đúng như bạn yêu cầu trong mã.

## Câu Hỏi Thường Gặp & Trường Hợp Đặc Biệt

### Tôi có thể đặt số Bates ở vị trí khác không?

Có. Sử dụng thuộc tính `Location` của `BatesNumberingArtifact` (ví dụ, `Location = new Position(10, 10)`) để đặt số tại tọa độ X/Y tùy chỉnh. Bạn cũng có thể đặt `HorizontalAlignment` và `VerticalAlignment` để kiểm soát chi tiết hơn.

### Nếu PDF của tôi có hàng ngàn trang thì sao?

Aspose.Pdf xử lý các trang một cách hiệu quả, nhưng vẫn nên xử lý theo lô nếu bạn gặp giới hạn bộ nhớ. Lớp `Document` cũng hỗ trợ `PdfConverter` để lưu incremental.

### Làm sao để thay đổi phông chữ hoặc màu sắc?

Wrap the artifact in a `TextState` object:

```csharp
batesNumbering.TextState = new TextState
{
    FontSize = 12,
    Font = FontRepository.FindFont("Arial"),
    ForegroundColor = Color.FromRgb(255, 0, 0) // red
};
```

### Tôi có cần giấy phép cho việc sử dụng trong môi trường sản xuất không?

Phiên bản có giấy phép sẽ loại bỏ watermark đánh giá và mở khóa hiệu năng đầy đủ. Bản dùng thử miễn phí hoạt động tốt cho việc thử nghiệm và chứng minh ý tưởng.

## Xác Minh – Kiểm Tra Nhanh Bằng Hình Ảnh  

Nếu bạn muốn kiểm tra tự động, Aspose có thể trích xuất văn bản của một trang và xác nhận sự hiện diện của tiền tố:

```csharp
string pageText = pdfDocument.Pages[1].ExtractText();
bool hasBates = pageText.Contains("ABC01000");
Console.WriteLine(hasBates ? "Bates number verified." : "Number missing!");
```

Chạy đoạn này sau bước lưu sẽ in ra `Bates number verified.` nếu mọi thứ diễn ra suôn sẻ.

## Kết Luận  

Bây giờ bạn đã biết **cách thêm số Bates vào các tệp PDF** bằng Aspose.Pdf trong C#. Từ việc mở tài liệu, cấu hình artifact, gắn nó vào các trang và lưu kết quả, quy trình này đơn giản và có thể tự động hoá hoàn toàn.  

Các bước tiếp theo? Hãy thử nghiệm với:

- Các giá trị `Prefix` khác nhau cho nhiều lô vụ việc  
- `Location` và `TextState` tùy chỉnh để thương hiệu  
- Thêm tiền tố riêng cho từng trang (ví dụ, “VOL‑1‑”, “VOL‑2‑”) bằng cách điều chỉnh `StartNumber` cho mỗi vòng lặp  

Những điều chỉnh này cho phép bạn tùy biến giải pháp cho hầu hết mọi quy trình pháp lý hoặc lưu trữ.  

Có thêm câu hỏi về **cách thêm số Bates** cho các PDF đa ngôn ngữ hoặc tệp được mã hoá? Hãy để lại bình luận bên dưới, và chúc bạn lập trình vui vẻ!

## Hướng Dẫn Liên Quan

- [How to Add and Customize Page Numbers in PDFs Using Aspose.PDF for .NET | Document Manipulation Guide](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [How to Add Different Headers in PDF Using Aspose.PDF for .NET&#58; A Step-by-Step Guide](/pdf/english/net/document-manipulation/add-different-headers-aspose-pdf-net/)
- [How to Add a Text Stamp Footer in PDFs Using Aspose.PDF for .NET&#58; A Step-by-Step Guide](/pdf/english/net/document-manipulation/add-text-stamp-footer-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}