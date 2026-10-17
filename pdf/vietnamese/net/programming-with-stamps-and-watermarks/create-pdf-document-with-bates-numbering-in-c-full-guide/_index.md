---
category: general
date: 2026-03-06
description: Tạo tài liệu PDF trong C# và dễ dàng thêm số bates. Tìm hiểu cách thêm
  trang trắng vào PDF, đặt dấu trên trang và triển khai việc đánh số bates.
draft: false
keywords:
- create pdf document
- add bates number
- add blank page pdf
- how to add bates numbering
- place stamp on page
language: vi
og_description: Tạo tài liệu PDF bằng C# và thêm số bates. Hướng dẫn này chỉ cách
  thêm trang trắng vào PDF, đặt dấu lên trang và áp dụng đánh số bates.
og_title: Tạo tài liệu PDF với số Bates – Hướng dẫn C#
tags:
- Aspose.Pdf
- C#
- PDF automation
title: Tạo tài liệu PDF với đánh số Bates trong C# – Hướng dẫn đầy đủ
url: /vi/net/programming-with-stamps-and-watermarks/create-pdf-document-with-bates-numbering-in-c-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo tài liệu PDF với đánh số Bates trong C#

Bạn đã bao giờ cần **create PDF document** trong C# và tự hỏi làm thế nào để thêm một số Bates mà không làm rối mình không? Bạn không phải là người duy nhất—các công ty luật, tòa án, và thậm chí một số nhóm tuân thủ doanh nghiệp đều gặp phải vấn đề này mỗi ngày. Tin tốt? Chỉ với vài dòng mã Aspose.Pdf, bạn có thể tạo một PDF mới, thêm một trang trống, và dán một số Bates hợp lệ trong một quy trình liền mạch.

Trong hướng dẫn này, chúng ta sẽ đi qua toàn bộ quy trình: từ thiết lập dự án, đến việc thêm một PDF trang trống, đến cách **how to add bates numbering**, và cuối cùng là **place stamp on page** và lưu kết quả. Khi kết thúc, bạn sẽ có một đoạn mã sẵn sàng sử dụng mà có thể chèn vào bất kỳ ứng dụng .NET nào. Không có tham chiếu mơ hồ, chỉ có một ví dụ hoàn chỉnh, có thể chạy được.

## Những gì bạn cần

- **.NET 6+** (hoặc .NET Framework 4.6+ – Aspose.Pdf hoạt động với cả hai)
- **Aspose.Pdf for .NET** gói NuGet (`Install-Package Aspose.Pdf`)
- Một IDE tốt (Visual Studio, Rider, hoặc VS Code với phần mở rộng C#)

Chỉ vậy thôi. Không có DLL bổ sung, không có dịch vụ bên ngoài. Hãy bắt đầu.

## Bước 1: Tạo tài liệu PDF – Thiết lập ban đầu

Đầu tiên, chúng ta cần một đối tượng `Document` mới. Hãy tưởng tượng nó như một nền trắng trống nơi mọi thứ sẽ được đặt.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Initialize a new PDF document
Document pdfDocument = new Document();
```

> **Tại sao điều này quan trọng:** Lớp `Document` là điểm vào cho mọi thao tác Aspose. Khi khởi tạo nó, bạn sẽ có quyền truy cập vào bộ sưu tập `Pages`, siêu dữ liệu và cài đặt bảo mật — tất cả các khối xây dựng cho một PDF chuyên nghiệp.

## Bước 2: Thêm trang PDF trống

Một PDF không có trang giống như một cuốn sách không có trang—không có ích gì. Thêm một trang trống là rất đơn giản, và nó cung cấp bề mặt để dán số Bates lên.

```csharp
// Add a single blank page to the document
Page page = pdfDocument.Pages.Add();
```

> **Mẹo chuyên nghiệp:** Nếu bạn cần nhiều trang, chỉ cần gọi `pdfDocument.Pages.Add()` trong một vòng lặp. Mỗi lần gọi trả về một đối tượng `Page` mới mà bạn có thể tùy chỉnh độc lập.

## Bước 3: Cách thêm đánh số Bates – Tạo TextStamp

Bây giờ là phần cốt lõi: **Bates number**. Trong Aspose.Pdf, nó chỉ là một `TextStamp` với cờ artifact đặc biệt.

```csharp
// Create a text stamp that will serve as a Bates number
TextStamp batesStamp = new TextStamp("Bates-001")
{
    // Mark the stamp as a Bates‑numbering artifact (helps PDF viewers treat it specially)
    Artifact = ArtifactType.BatesNumbering,
    // Align the stamp to the bottom‑right corner of the page
    HorizontalAlignment = HorizontalAlignment.Right,
    VerticalAlignment = VerticalAlignment.Bottom,
    // Add a small margin so the number isn’t glued to the edge
    Margin = new Margin { Bottom = 10, Right = 10 }
};
```

> **Tại sao chúng ta đặt `Artifact`**: Một số trình đọc PDF hiển thị số Bates dưới dạng siêu dữ liệu có thể tìm kiếm. Đánh dấu stamp là một artifact `BatesNumbering` đảm bảo các công cụ hạ nguồn có thể nhận diện nó tự động.

## Bước 4: Đặt stamp lên trang

Với stamp đã sẵn sàng, chúng ta bây giờ **place stamp on page**. Đây là bước mà số hiển thị thực sự xuất hiện trong PDF.

```csharp
// Add the Bates number stamp to the previously created page
page.AddStamp(batesStamp);
```

> **Trường hợp đặc biệt:** Nếu bạn cần số tăng lên trên mỗi trang, bạn sẽ lặp qua `pdfDocument.Pages` và cập nhật `batesStamp.Value` trước khi gọi `AddStamp`. Ví dụ ở đây giữ đơn giản với “Bates‑001” tĩnh.

## Bước 5: Lưu và xác minh kết quả

Cuối cùng, chúng ta lưu PDF vào đĩa. Chọn một thư mục mà bạn có quyền ghi; nếu không, bạn sẽ gặp `UnauthorizedAccessException`.

```csharp
// Save the stamped PDF to a file
pdfDocument.Save("YOUR_DIRECTORY/BatesStamped.pdf");
```

Khi bạn mở `BatesStamped.pdf` bằng bất kỳ trình xem nào, bạn sẽ thấy một “Bates‑001” nhỏ gọn nằm gọn ở góc dưới‑phải của trang trống.

> **Kết quả mong đợi:**  
> ![PDF có dấu số Bates](image-placeholder.png "PDF có dấu số Bates")  
> *Alt text: PDF có dấu số Bates ở góc dưới‑phải.*

Nếu số không hiển thị, hãy kiểm tra lại giá trị lề và đảm bảo kích thước trang không quá nhỏ (mặc định A4 hoạt động tốt). Cũng xác nhận rằng cờ `Artifact` không bị các công cụ xử lý hậu kỳ loại bỏ.

## Ví dụ làm việc đầy đủ

Dưới đây là chương trình hoàn chỉnh, sẵn sàng sao chép‑dán. Nó bao gồm tất cả các chỉ thị `using` và chú thích để bạn dễ theo dõi.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize a new PDF document
        Document pdfDocument = new Document();

        // 2️⃣ Add a blank page – this is where we’ll put the Bates number
        Page page = pdfDocument.Pages.Add();

        // 3️⃣ Create a TextStamp for the Bates number
        TextStamp batesStamp = new TextStamp("Bates-001")
        {
            Artifact = ArtifactType.BatesNumbering,          // Marks it as a Bates‑numbering artifact
            HorizontalAlignment = HorizontalAlignment.Right, // Align right
            VerticalAlignment = VerticalAlignment.Bottom,    // Align bottom
            Margin = new Margin { Bottom = 10, Right = 10 }  // Small margin from edges
        };

        // 4️⃣ Place the stamp on the page
        page.AddStamp(batesStamp);

        // 5️⃣ Save the PDF to disk
        string outputPath = @"C:\Temp\BatesStamped.pdf";
        pdfDocument.Save(outputPath);

        Console.WriteLine($"PDF created successfully: {outputPath}");
    }
}
```

Chạy chương trình, mở PDF, và bạn sẽ thấy số Bates chính xác ở vị trí chúng ta đã chỉ định. 🎉

## Các biến thể phổ biến & lưu ý

| Scenario | What to Change | Why |
|----------|----------------|-----|
| **Nhiều trang, tăng dần số** | Loop through `pdfDocument.Pages`, set `batesStamp.Value = $"Bates-{i:D3}"` before `AddStamp` | Cung cấp cho mỗi trang một định danh duy nhất, thường dùng cho các bộ tài liệu pháp lý |
| **Vị trí khác (trên‑trái)** | Change `HorizontalAlignment = HorizontalAlignment.Left` and `VerticalAlignment = VerticalAlignment.Top` | Một số tổ chức thích số ở phần đầu trang thay vì chân trang |
| **Phông chữ hoặc màu tùy chỉnh** | Set `batesStamp.TextState.Font = FontRepository.FindFont("Arial"); batesStamp.TextState.FontSize = 12; batesStamp.TextState.ForegroundColor = Color.Red;` | Cải thiện khả năng đọc hoặc đáp ứng các hướng dẫn thương hiệu |
| **Thêm PDF hiện có làm nền** | Load the source PDF with `Document src = new Document("source.pdf"); pdfDocument.Pages.Add(src.Pages[1]);` | Hữu ích khi bạn cần dán lên một mẫu đã được tạo trước |

## Kết luận

Chúng tôi vừa trình bày cách **create PDF document**, **add blank page pdf**, và **add bates number** bằng Aspose.Pdf cho .NET, sau đó **place stamp on page** và lưu tệp. Mã được viết ngắn gọn để bạn có thể áp dụng vào các quy trình lớn hơn—cho dù bạn đang xử lý hàng chục tệp hoặc tích hợp vào một dịch vụ web.

Nếu bạn sẵn sàng tiến xa hơn, hãy cân nhắc:

- Tự động hoá logic tăng dần cho các tệp vụ án lớn.
- Nhúng việc tạo PDF vào một API ASP.NET Core.
- Thêm bảo mật (bảo vệ bằng mật khẩu) với `pdfDocument.Encrypt(...)`.

Hãy thoải mái thử nghiệm, phá vỡ và đặt câu hỏi trong phần bình luận. Chúc lập trình vui vẻ, và chúc các PDF của bạn luôn được dán dấu hoàn hảo!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}