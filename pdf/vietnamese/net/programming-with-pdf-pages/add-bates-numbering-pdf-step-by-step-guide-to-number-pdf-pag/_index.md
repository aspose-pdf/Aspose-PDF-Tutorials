---
category: general
date: 2026-03-03
description: Thêm đánh số Bates cho PDF một cách nhanh chóng và học cách đánh số các
  trang PDF hoặc thêm các số PDF tuần tự bằng Aspose.Pdf trong C#.
draft: false
keywords:
- add bates numbering pdf
- number pdf pages
- add sequential pdf numbers
- pdf bates numbering tutorial
- aspnet pdf automation
language: vi
og_description: Thêm đánh số Bates vào PDF bằng C# để đánh số các trang PDF và thêm
  các số PDF tuần tự. Mã đầy đủ, giải thích và các thực tiễn tốt nhất.
og_title: Thêm số Bates vào PDF – Hướng dẫn C# đầy đủ
tags:
- PDF
- C#
- Aspose.Pdf
- Document Automation
title: Thêm Số Bates vào PDF – Hướng Dẫn Từng Bước Đánh Số Các Trang PDF
url: /vi/net/programming-with-pdf-pages/add-bates-numbering-pdf-step-by-step-guide-to-number-pdf-pag/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Thêm Số Bates vào PDF – Hướng Dẫn C# Đầy Đủ

Bạn đã bao giờ cần **add bates numbering pdf** nhưng không biết bắt đầu từ đâu? Bạn không phải là người duy nhất—các nhóm pháp lý, kiểm toán và lưu trữ đều gặp vấn đề tương tự. Tin tốt là gì? Chỉ với vài dòng C# và thư viện Aspose.Pdf, bạn có thể **number pdf pages** một cách tự động, và thậm chí còn có khả năng **add sequential pdf numbers** với tiền tố, hậu tố và vị trí tùy chỉnh.

Trong hướng dẫn này, chúng tôi sẽ đi qua một ví dụ thực tế, giải thích tại sao mỗi thiết lập lại quan trọng, và chỉ cho bạn cách tinh chỉnh mã cho các trường hợp đặc biệt như kích thước trang khác nhau hoặc số chữ số tùy chỉnh. Khi hoàn thành, bạn sẽ có một đoạn mã sẵn sàng chạy để thêm số Bates vào bất kỳ PDF nào, và bạn sẽ hiểu “tại sao” đằng sau mỗi tùy chọn.

## Prerequisites

Trước khi bắt đầu, hãy chắc chắn rằng bạn có:

- .NET 6.0 trở lên (mã cũng hoạt động với .NET Framework 4.6+)
- Giấy phép Aspose.Pdf for .NET hợp lệ (hoặc khóa dùng thử miễn phí)
- Visual Studio 2022 (hoặc bất kỳ trình chỉnh sửa C# nào bạn thích)
- Một tệp PDF nguồn có tên `source.pdf` trong thư mục bạn có thể tham chiếu

Chỉ vậy—không cần gói NuGet nào khác ngoài Aspose.Pdf.

## Bước 1 – Mở Tài Liệu PDF Nguồn

Điều đầu tiên bạn cần làm là tải PDF bạn muốn dán dấu. Sử dụng một khối `using` đảm bảo tay cầm tệp được giải phóng đúng cách, ngăn ngừa các vấn đề khóa tệp sau này.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Step 1: Load the original PDF
using (var pdfDocument = new Document(@"C:\MyDocs\source.pdf"))
{
    // The rest of the steps will go inside this block.
}
```

> **Why this matters:** Mở tài liệu bên trong một câu lệnh `using` đảm bảo việc hủy tài nguyên một cách quyết đoán. Nếu bỏ qua, tệp có thể bị khóa, và các lần cố gắng lưu hoặc xóa PDF sẽ thất bại—điều tôi đã thấy gây rắc rối trong các pipeline sản xuất.

## Bước 2 – Cấu Hình Các Tùy Chọn Đánh Số Bates

Bây giờ chúng ta cho Aspose biết chúng ta muốn số Bates trông như thế nào. Mỗi thuộc tính tương ứng trực tiếp với một yếu tố hiển thị trên trang.

```csharp
// Step 2: Set up Bates numbering preferences
var batesOptions = new BatesNumberingOptions
{
    Prefix = "2025-",               // Text before the number
    Suffix = "-A",                  // Text after the number
    Start = 5000,                   // First number in the sequence
    NumberOfDigits = 5,             // Pads with leading zeros (e.g., 05000)
    Placement = BatesNumberPlacement.BottomRight // Where the number appears
};
```

### Mẹo nhanh cho các tùy chọn

| Property | Chức năng | Khi nào cần thay đổi |
|----------|-----------|----------------------|
| **Prefix / Suffix** | Thêm văn bản tĩnh trước/sau phần số. | Sử dụng ID vụ án, mã dự án, hoặc “CONF‑” cho tài liệu mật. |
| **Start** | Số đầu tiên trong chuỗi. | Nếu bạn đang tiếp tục một kế hoạch đánh số từ lô trước, hãy đặt giá trị này cho phù hợp. |
| **NumberOfDigits** | Kiểm soát việc thêm số 0 phía trước. | Đối với hồ sơ pháp lý thường cần đúng 6 chữ số; đặt thành `6`. |
| **Placement** | BottomRight, BottomLeft, TopRight, TopLeft, Center. | Chọn dựa trên bố cục tài liệu; BottomRight là vị trí phổ biến nhất cho số Bates. |

> **Pro tip:** Nếu bạn cần **number pdf pages** trong nhiều cột, bạn có thể gọi `pdfDocument.AddBatesNumbering` hai lần với các giá trị `Placement` khác nhau và các chuỗi `Prefix` riêng biệt.

## Bước 3 – Áp Dụng Đánh Số Bates vào Tài Liệu

Với các tùy chọn đã sẵn sàng, việc dán dấu thực tế chỉ là một lời gọi phương thức duy nhất. Aspose xử lý việc phân trang, xoay và tính toán lề nội bộ.

```csharp
// Step 3: Apply the numbering to every page
pdfDocument.AddBatesNumbering(batesOptions);
```

> **Why a single call works:** Bên trong, Aspose lặp qua `pdfDocument.Pages`, tạo một `TextFragment` cho mỗi trang, và định vị nó dựa trên `Placement` bạn đã chọn. Trừu tượng này giúp bạn không phải viết vòng lặp thủ công và xử lý các phép biến đổi tọa độ.

## Bước 4 – Lưu PDF Đã Cập Nhật

Cuối cùng, ghi tệp đã chỉnh sửa ra đĩa. Bạn có thể ghi đè lên tệp gốc hoặc tạo một tệp mới; ví dụ dưới đây tạo một bản sao mới.

```csharp
// Step 4: Persist the changes
pdfDocument.Save(@"C:\MyDocs\bates_numbered.pdf");
```

Nếu bạn cần **add sequential pdf numbers** vào một luồng (ví dụ, khi gửi tệp qua API), thay thế đường dẫn tệp bằng một `MemoryStream`:

```csharp
using var output = new MemoryStream();
pdfDocument.Save(output);
output.Position = 0; // Reset for downstream consumption
```

## Ví Dụ Hoạt Động Đầy Đủ

Kết hợp tất cả lại, đây là chương trình hoàn chỉnh, sẵn sàng chạy:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;

class Program
{
    static void Main()
    {
        // Open the source PDF
        using (var pdfDocument = new Document(@"C:\MyDocs\source.pdf"))
        {
            // Configure Bates numbering
            var batesOptions = new BatesNumberingOptions
            {
                Prefix = "2025-",
                Suffix = "-A",
                Start = 5000,
                NumberOfDigits = 5,
                Placement = BatesNumberPlacement.BottomRight
            };

            // Apply the numbering
            pdfDocument.AddBatesNumbering(batesOptions);

            // Save the result
            pdfDocument.Save(@"C:\MyDocs\bates_numbered.pdf");
        }

        Console.WriteLine("Bates numbering added successfully!");
    }
}
```

### Kết Quả Dự Kiến

- Một tệp mới `bates_numbered.pdf` xuất hiện trong `C:\MyDocs`.
- Mỗi trang hiển thị dạng như `2025-05000-A`, `2025-05001-A`, … ở góc dưới‑phải.
- Các số được bổ sung số 0 phía trước để có năm chữ số, phù hợp với thiết lập `NumberOfDigits`.

## Xử Lý Các Biến Thể Thông Thường

### 1. Kích Thước Trang Khác Nhau

Nếu PDF của bạn pha trộn các trang dọc và ngang, bạn có thể thấy số bị cắt ở phía rộng hơn. Để khắc phục, bật thuộc tính `AutoFit`:

```csharp
batesOptions.AutoFit = true; // Adjusts font size to fit within page margins
```

### 2. Phông Chữ Hoặc Màu Tùy Chỉnh

Số Bates mặc định là màu đen, kích thước 12‑pt Times New Roman. Thay đổi giao diện bằng cách truy cập `TextState`:

```csharp
batesOptions.TextState = new TextState
{
    FontSize = 10,
    Font = FontRepository.FindFont("Courier New"),
    ForegroundColor = Color.GetBlue()
};
```

### 3. Bỏ Qua Các Trang

Giả sử bạn muốn **number pdf pages** nhưng bỏ qua trang tiêu đề. Sử dụng một phạm vi trang:

```csharp
pdfDocument.AddBatesNumbering(batesOptions, new PageNumbering { Start = 2 });
```

### 4. Thêm Nhiều Định Dạng Đánh Số

Các nhóm pháp lý đôi khi yêu cầu cả số Bates và một dấu watermark bí mật. Chạy hai lời gọi `AddBatesNumbering` riêng biệt với các giá trị `Placement` khác nhau:

```csharp
// First scheme – bottom right
pdfDocument.AddBatesNumbering(batesOptions);

// Second scheme – top left, different prefix
var confidentialOptions = new BatesNumberingOptions
{
    Prefix = "CONF-",
    Start = 1,
    NumberOfDigits = 4,
    Placement = BatesNumberPlacement.TopLeft,
    TextState = new TextState { FontSize = 8, ForegroundColor = Color.GetRed() }
};
pdfDocument.AddBatesNumbering(confidentialOptions);
```

## Câu Hỏi Thường Gặp

**Q: Điều này có hoạt động với các PDF đã có văn bản sẵn không?**  
A: Có. Aspose thêm số Bates như một lớp riêng, vì vậy nội dung hiện có không bị thay đổi. Nếu bạn cần các số xuất hiện *phía sau* văn bản hiện có (hiếm), bạn sẽ phải thao tác trực tiếp với các luồng nội dung của trang.

**Q: Nếu PDF được bảo vệ bằng mật khẩu thì sao?**  
A: Đầu tiên tải nó với mật khẩu: `new Document(path, new LoadOptions { Password = "secret" })`. Sau khi dán dấu, bạn có thể áp dụng lại mã hóa bằng `pdfDocument.Encrypt(...)`.

**Q: Tôi có thể dùng điều này trong một ứng dụng console .NET Core không?**  
A: Chắc chắn. Mã giống nhau hoạt động trong .NET Core, .NET 5+, và .NET Framework. Chỉ cần tham chiếu gói NuGet Aspose.Pdf phù hợp.

## Kết Luận

Chúng ta vừa tìm hiểu cách **add bates numbering pdf**, cách **number pdf pages**, và cách **add sequential pdf numbers** với kiểm soát đầy đủ về định dạng, vị trí và xử lý các trường hợp đặc biệt. Đoạn mã ngắn ở trên thực hiện phần lớn công việc, trong khi các tùy chọn bổ sung cho phép bạn điều chỉnh giải pháp cho bất kỳ quy trình pháp lý, lưu trữ hoặc tuân thủ nào.

Sẵn sàng cho bước tiếp theo? Hãy thử kết hợp cách tiếp cận này với:

- **Batch processing** – lặp qua một thư mục các PDF và áp dụng cùng một kế hoạch đánh số.
- **Dynamic prefixes** – lấy ID vụ án từ cơ sở dữ liệu và chèn chúng vào từng tài liệu.
- **PDF/A compliance** – sau khi đánh số, gọi `pdfDocument.Convert(..., PdfFormat.PdfA2b)` để đảm bảo lưu trữ lâu dài.

Hãy thoải mái thử nghiệm, chia sẻ kết quả, hoặc đặt câu hỏi trong phần bình luận. Chúc lập trình vui vẻ, và mong các PDF của bạn luôn được lập chỉ mục một cách hoàn hảo! 

![Ảnh chụp màn hình một trang PDF với số Bates ở góc dưới‑phải](https://example.com/images/bates-numbered.png "ví dụ thêm số bates vào pdf")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}