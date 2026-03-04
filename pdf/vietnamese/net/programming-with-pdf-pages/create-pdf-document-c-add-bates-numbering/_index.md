---
category: general
date: 2026-03-03
description: Tạo tài liệu PDF C# với đánh số Bates – học cách thêm đánh số Bates,
  thêm số trang tuần tự và tạo đánh số Bates chỉ trong vài bước.
draft: false
keywords:
- create pdf document c#
- add bates numbering pdf
- how to add bates
- add sequential page numbers
- how to generate bates
language: vi
og_description: Tạo tài liệu PDF C# với đánh số Bates. Hướng dẫn này chỉ cách thêm
  số Bates, thêm số trang tuần tự và tạo số Bates nhanh chóng.
og_title: Tạo tài liệu PDF bằng C# – Thêm đánh số Bates
tags:
- C#
- PDF
- Bates numbering
title: Tạo tài liệu PDF C# – Thêm đánh số Bates
url: /vi/net/programming-with-pdf-pages/create-pdf-document-c-add-bates-numbering/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo Tài liệu PDF C# – Thêm Số Bates

Bạn đã bao giờ **create PDF document C#** và sau đó gắn mỗi trang với một định danh duy nhất cho mục đích pháp lý hoặc lưu trữ chưa? Bạn không phải là người duy nhất—các công ty luật, tòa án, và thậm chí các tập đoàn lớn thường hỏi: “Làm thế nào để tự động **add Bates numbers** vào PDF của tôi?” Tin tốt là chỉ với vài dòng mã, bạn có thể tạo một PDF, rải số Bates lên mọi trang, và lưu kết quả mà không cần mở bất kỳ trình chỉnh sửa nào.

Trong tutorial này, chúng ta sẽ đi qua một ví dụ thực tế, từ đầu đến cuối, cho thấy **cách thêm Bates**, **cách thêm số trang tuần tự**, và thậm chí **cách tạo Bates** với tiền tố tùy chỉnh. Khi kết thúc, bạn sẽ có một đoạn mã có thể tái sử dụng và chèn vào bất kỳ dự án .NET nào.

## Những gì bạn cần

- **.NET 6+** (mã cũng hoạt động trên .NET Framework 4.6+)
- **Aspose.Pdf for .NET** – một thư viện thương mại cung cấp API sạch cho việc thao tác PDF. Bản đánh giá miễn phí đủ cho việc thử nghiệm.
- Kiến thức cơ bản về C# (bạn có lẽ đã quen với các câu lệnh `using` và các đối tượng).

Không cần thêm bất kỳ gói NuGet nào ngoài `Aspose.Pdf`. Nếu bạn chưa cài đặt, chạy:

```bash
dotnet add package Aspose.Pdf
```

> **Pro tip:** Giữ phiên bản Aspose luôn cập nhật; bản phát hành 23.x mới nhất đã thêm các tối ưu hiệu năng cho tài liệu lớn.

## Bước 1: Mở (hoặc Tạo) Tài liệu PDF nguồn

Đầu tiên chúng ta cần một PDF để làm việc. Trong nhiều trường hợp thực tế, bạn đã có sẵn một file đầu vào—ví dụ một hợp đồng đã quét. Để minh họa, chúng ta sẽ mở một file hiện có có tên `input.pdf`.

```csharp
using Aspose.Pdf;

// Step 1 – Load the PDF you want to number
var pdfPath = @"C:\Docs\input.pdf";
using var pdfDocument = new Document(pdfPath);
```

> **Tại sao điều này quan trọng:** Mở tài liệu trong một khối `using` đảm bảo tay cầm file được giải phóng kịp thời, tránh các vấn đề khóa file khi bạn cố gắng ghi đè lại file cùng tên sau này.

## Bước 2: Định nghĩa Các tùy chọn Đánh số Bates

Số Bates gồm **tiền tố** (thường là mã vụ án) và **số bắt đầu**. Bạn cũng có thể kiểm soát số chữ số, vị trí trên trang, và kiểu phông chữ. Ở đây chúng ta sẽ sử dụng từ khóa phụ **add bates numbering pdf** bằng cách cấu hình một đối tượng `BatesNumberingOptions`.

```csharp
// Step 2 – Set up Bates numbering preferences
var batesOptions = new BatesNumberingOptions
{
    // Primary keyword in action: create pdf document c# with custom settings
    Prefix = "CASE-",
    Start = 1000,
    // Optional: set zero‑padding to 6 digits (e.g., CASE-001000)
    NumberOfDigits = 6,
    // Optional: define where the number appears (bottom‑right corner)
    HorizontalAlignment = HorizontalAlignment.Right,
    VerticalAlignment   = VerticalAlignment.Bottom,
    // Optional: choose a readable font
    Font = FontRepository.FindFont("Arial")
};
```

> **Cách thêm bates:** Bằng cách điều chỉnh `Prefix` và `Start` bạn kiểm soát chuỗi chính xác sẽ xuất hiện trên mỗi trang. Thuộc tính `NumberOfDigits` đảm bảo độ rộng đồng nhất, rất hữu ích cho các hồ sơ pháp lý.

## Bước 3: Áp dụng Đánh số Bates cho Mỗi Trang

Bây giờ là phần cốt lõi—thêm các số. Phương thức `AddBatesNumbering` sẽ duyệt qua từng trang, vẽ văn bản, và tuân theo các tùy chọn chúng ta đã định nghĩa.

```csharp
// Step 3 – Apply Bates numbering to all pages
pdfDocument.AddBatesNumbering(batesOptions);
```

Bên trong, Aspose render văn bản như một phần *content*, nghĩa là các số trở thành một phần của PDF và không thể tắt trong trình xem. Đây chính là điều bạn cần khi muốn **add sequential page numbers** không thể thay đổi.

### Trường hợp đặc biệt & Biến thể

- **Nhiều tiền tố:** Nếu bạn cần các tiền tố khác nhau cho từng phần, tạo các `BatesNumberingOptions` riêng và gọi `AddBatesNumbering` trên một phạm vi trang (`pdfDocument.Pages[1..5]`).
- **Kiểm soát zero‑padding:** Bỏ qua `NumberOfDigits` để có số có độ dài biến đổi, hoặc đặt giá trị cao hơn để có các số 0 ở đầu.
- **Vị trí tùy chỉnh:** Dùng `Margin` để dịch số ra khỏi mép, hoặc chuyển `HorizontalAlignment` thành `Center` để đặt ở dạng footer.

## Bước 4: Lưu PDF Đã chỉnh sửa

Cuối cùng, ghi tài liệu đã cập nhật ra đĩa. Bạn có thể ghi đè lên file gốc hoặc tạo một file mới hoàn toàn.

```csharp
// Step 4 – Save the PDF with Bates numbers applied
var outputPath = @"C:\Docs\output.pdf";
pdfDocument.Save(outputPath);
```

Sau khi dòng này chạy, `output.pdf` sẽ chứa nội dung gốc cộng với một thẻ Bates hiển thị trên mỗi trang—đúng như bạn mong đợi khi **how to generate bates** cho một hồ sơ vụ án.

## Ví dụ Hoàn chỉnh, Có thể Chạy

Kết hợp tất cả lại, đây là đoạn mã đầy đủ bạn có thể sao chép‑dán vào một ứng dụng console:

```csharp
using System;
using Aspose.Pdf;

class Program
{
    static void Main()
    {
        // 1️⃣ Open the source PDF
        var inputFile = @"C:\Docs\input.pdf";
        using var pdf = new Document(inputFile);

        // 2️⃣ Configure Bates numbering (add bates numbering pdf)
        var options = new BatesNumberingOptions
        {
            Prefix = "CASE-",
            Start = 1000,
            NumberOfDigits = 6,
            HorizontalAlignment = HorizontalAlignment.Right,
            VerticalAlignment = VerticalAlignment.Bottom,
            Font = FontRepository.FindFont("Arial")
        };

        // 3️⃣ Apply the numbering (how to add bates)
        pdf.AddBatesNumbering(options);

        // 4️⃣ Save the result (add sequential page numbers)
        var outputFile = @"C:\Docs\output.pdf";
        pdf.Save(outputFile);

        Console.WriteLine("Bates numbering applied successfully!");
    }
}
```

### Kết quả Mong đợi

Mở `output.pdf` trong bất kỳ trình xem nào (Adobe Reader, Edge, v.v.). Bạn sẽ thấy mỗi trang được dán nhãn như **CASE-001000**, **CASE-001001**, … cho tới trang cuối cùng. Các số nằm gọn ở góc dưới‑phải, phù hợp với các tùy chọn chúng ta đã đặt.

## Câu hỏi Thường gặp & Khắc phục sự cố

- **“Nếu PDF của tôi được bảo vệ bằng mật khẩu thì sao?”**  
  Tải nó bằng mật khẩu: `new Document(inputFile, new LoadOptions { Password = "secret" })`.

- **“Tôi có thể thêm số Bates vào một PDF mới tạo không?”**  
  Chắc chắn. Chỉ cần tạo tài liệu trước (`var doc = new Document();`) rồi thực hiện các Bước 2‑4 trước khi lưu.

- **“Phông chữ có luôn được nhúng không?”**  
  Aspose tự động nhúng phông chữ nếu nó chưa có trong PDF. Nếu bạn cần một họ phông chữ cụ thể, đặt `options.Font` cho phù hợp.

- **“Hiệu năng thế nào với file 10.000 trang?”**  
  Thư viện stream các trang, vì vậy việc sử dụng bộ nhớ vẫn ở mức vừa phải. Tuy nhiên, bạn có thể tăng `PdfSaveOptions.CompressionMode` để cải thiện tốc độ I/O.

## Mẹo Pro cho Sản xuất

1. **Xử lý hàng loạt:** Đặt logic trên vào một vòng lặp duyệt qua thư mục chứa các PDF. Dùng `Directory.GetFiles("*.pdf")` và xử lý từng file riêng.
2. **Ghi log:** Ghi số Bates đầu tiên và cuối cùng vào file log—giúp kiểm toán viên xác nhận việc đánh số liên tục.
3. **Xử lý lỗi:** Bao toàn bộ khối trong một `try/catch` và đưa ra thông báo rõ ràng nếu PDF nguồn thiếu hoặc bị hỏng.
4. **Linh hoạt zero‑padding:** Nếu bạn cần độ dài chữ số động dựa trên tổng số trang, tính `NumberOfDigits = (pdf.Pages.Count + options.Start).ToString().Length`.

## Kết luận

Chúng ta vừa trình bày cách **create PDF document C#** và một cách liền mạch để **add Bates numbering**—từ việc tải tài liệu ban đầu tới lưu cuối cùng. Ví dụ ngắn gọn này minh họa **how to add bates**, **add sequential page numbers**, và **how to generate bates** với tiền tố tùy chỉnh và zero‑padding. Với một vài chỉnh sửa, bạn có thể áp dụng mẫu này cho các công việc batch, bố cục khác nhau, hoặc thậm chí tích hợp vào một API web trả về PDF đã được đánh số ngay khi yêu cầu.

Sẵn sàng cho bước tiếp theo? Hãy thử kết hợp với tính năng **watermark** của Aspose, hoặc tạo một chỉ mục tóm tắt liệt kê mỗi số Bates cùng mô tả ngắn gọn nội dung trang. Khả năng là vô hạn, và đoạn mã bạn vừa có là nền tảng vững chắc cho bất kỳ quy trình tự động hoá tài liệu nào.

Happy coding, và chúc các PDF của bạn luôn được đánh số hoàn hảo! 

![Ảnh chụp màn hình của trình xem PDF hiển thị tạo tài liệu pdf c# với số Bates đã áp dụng](image-placeholder.png "tạo tài liệu pdf c# với số Bates")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}