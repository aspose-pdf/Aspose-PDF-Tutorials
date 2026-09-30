---
category: general
date: 2026-02-12
description: Thêm số Bates vào các tệp PDF một cách nhanh chóng. Tìm hiểu cách thêm
  trường văn bản PDF, thêm trường biểu mẫu PDF và thêm số trang PDF bằng Aspose.PDF.
draft: false
keywords:
- add bates numbers
- add text field pdf
- add form field pdf
- add page numbers pdf
- how to add bates
language: vi
og_description: Thêm số Bates vào tài liệu PDF bằng C#. Hướng dẫn này chỉ cách thêm
  trường văn bản PDF, thêm trường biểu mẫu PDF và thêm số trang PDF với Aspose.PDF.
og_title: Thêm số Bates vào PDF – Hướng dẫn C# đầy đủ
tags:
- PDF
- C#
- Aspose.PDF
title: Thêm số Bates vào PDF – Hướng dẫn C# chi tiết từng bước
url: /vi/net/programming-with-forms/add-bates-numbers-to-pdfs-step-by-step-c-guide/
---













{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Thêm Số Bates vào PDF – Hướng Dẫn Toàn Diện C#

Bạn đã bao giờ **add bates numbers** vào một đống PDF pháp lý mà không biết bắt đầu từ đâu chưa? Bạn không đơn độc. Ở nhiều công ty luật và dự án e‑discovery, việc dán nhãn mỗi trang bằng một định danh duy nhất là công việc hàng ngày, và làm thủ công là một cơn ác mộng.  

Tin tốt là gì? Chỉ với vài dòng C# và Aspose.PDF, bạn có thể tự động hoá toàn bộ quá trình. Trong tutorial này, chúng ta sẽ đi qua **cách add bates** numbers, rải một trường văn bản lên mỗi trang, và lưu lại một PDF sạch, có thể tìm kiếm — mà không phải lo lắng gì.

> **Bạn sẽ nhận được:** một mẫu code có thể chạy ngay, giải thích vì sao mỗi dòng lại quan trọng, mẹo cho các trường hợp đặc biệt, và một danh sách kiểm tra nhanh để xác nhận đầu ra của bạn.  

Chúng tôi cũng sẽ đề cập tới các nhiệm vụ liên quan như **add text field pdf**, **add form field pdf**, và **add page numbers pdf**, để bạn có một bộ công cụ sẵn sàng cho bất kỳ thách thức tự động hoá tài liệu nào.

---

## Các Điều Kiện Cần Thiết

- .NET 6.0 trở lên (code cũng hoạt động với .NET Framework 4.6+)
- Visual Studio 2022 (hoặc bất kỳ IDE nào bạn thích)
- Giấy phép Aspose.PDF for .NET hợp lệ (bản dùng thử miễn phí đủ cho việc thử nghiệm)
- Một file PDF nguồn có tên `source.pdf` đặt trong thư mục bạn có thể tham chiếu

Nếu có bất kỳ mục nào chưa quen, hãy tạm dừng và cài đặt phần còn thiếu trước khi tiếp tục. Các bước dưới đây giả định rằng bạn đã thêm gói NuGet Aspose.PDF:

```bash
dotnet add package Aspose.Pdf
```

---

## Cách add bates numbers vào PDF với Aspose.PDF

Dưới đây là chương trình hoàn chỉnh, sẵn sàng copy‑paste. Nó tải PDF, tạo một **text box field** trên mỗi trang, ghi số Bates đã định dạng, và cuối cùng lưu file đã chỉnh sửa.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Forms;

class Program
{
    static void Main()
    {
        // 👉 Step 1: Load the source PDF document
        using (var pdfDocument = new Document(@"YOUR_DIRECTORY\source.pdf"))
        {
            // 👉 Step 2: Add a Bates number text field to each page
            for (int pageNumber = 1; pageNumber <= pdfDocument.Pages.Count; pageNumber++)
            {
                // Define the rectangle where the field will appear (10,10) = lower‑left corner
                var fieldRect = new Rectangle(10, 10, 150, 30);

                // Create the TextBoxField – this is the “add text field pdf” part
                var batesField = new TextBoxField(pdfDocument.Pages[pageNumber], fieldRect)
                {
                    // Format the number: BATES-00001, BATES-00002, …
                    Value = $"BATES-{pageNumber:D5}"
                };

                // Register the field with the form collection – “add form field pdf”
                pdfDocument.Form.Add(batesField, $"Bates_{pageNumber}", pageNumber);
            }

            // 👉 Step 3: Save the modified PDF with Bates numbers
            pdfDocument.Save(@"YOUR_DIRECTORY\bates.pdf");
        }

        Console.WriteLine("✅ Bates numbers added successfully!");
    }
}
```

### Tại sao cách này hoạt động

- **`Document`** là điểm vào; nó đại diện cho toàn bộ file PDF.  
- **`Rectangle`** xác định vị trí của trường trên trang. Các số được tính bằng point (1 pt ≈ 1/72 in). Điều chỉnh tọa độ nếu bạn muốn số xuất hiện ở góc khác.  
- **`TextBoxField`** là một *form field* có thể chứa bất kỳ chuỗi nào. Bằng cách gán `Value` chúng ta thực chất **add page numbers pdf** với tiền tố tùy chỉnh.  
- **`pdfDocument.Form.Add`** đăng ký trường vào AcroForm của PDF, khiến nó hiển thị trong các trình xem như Adobe Acrobat.  

Nếu bạn muốn thay đổi giao diện (phông chữ, màu sắc, kích thước) bạn có thể tùy chỉnh các thuộc tính của `TextBoxField` — xem tài liệu Aspose về `DefaultAppearance` và `Border`.

---

## Thêm trường văn bản vào mỗi trang PDF (bước “add text field pdf”)

Đôi khi bạn chỉ muốn một nhãn hiển thị, không phải một trường form tương tác. Trong trường hợp đó, bạn có thể thay `TextBoxField` bằng một `TextFragment` và thêm trực tiếp vào bộ sưu tập `Paragraphs` của trang. Đây là một cách thay thế nhanh:

```csharp
var fragment = new TextFragment($"BATES-{pageNumber:D5}")
{
    // Position the text using a TextState (font, size, color)
    TextState = new TextState
    {
        Font = FontRepository.FindFont("Arial"),
        FontSize = 12,
        ForegroundColor = Color.Black
    }
};

// Set the fragment’s rectangle (same coordinates as before)
fragment.Position = new Position(10, 10);
pdfDocument.Pages[pageNumber].Paragraphs.Add(fragment);
```

Cách **add text field pdf** hữu ích khi tài liệu cuối cùng sẽ ở chế độ chỉ‑đọc, trong khi phương pháp **add form field pdf** giữ cho các số có thể chỉnh sửa sau này.

---

## Lưu PDF với số Bates (khoảnh khắc “add page numbers pdf”)

Sau khi vòng lặp kết thúc, gọi `pdfDocument.Save` sẽ ghi mọi thứ ra đĩa. Nếu bạn cần giữ nguyên file gốc, chỉ cần thay đổi đường dẫn đầu ra hoặc dùng các overload của `pdfDocument.Save` để stream kết quả trực tiếp tới response trong một web API.

```csharp
// Example: stream to HTTP response (ASP.NET Core)
Response.ContentType = "application/pdf";
pdfDocument.Save(Response.Body);
```

Đó là phần hay — không cần file tạm, không cần thư viện phụ, chỉ có Aspose lo phần nặng.

---

## Kết Quả Mong Đợi & Kiểm Tra Nhanh

Mở `bates.pdf` bằng bất kỳ trình xem PDF nào. Bạn sẽ thấy một hộp nhỏ ở góc dưới‑trái của mỗi trang, nội dung:

```
BATES-00001
BATES-00002
…
```

Nếu bạn kiểm tra thuộc tính tài liệu, sẽ thấy một AcroForm chứa các trường có tên `Bates_1`, `Bates_2`, … Điều này xác nhận bước **add form field pdf** đã thành công.

---

## Những Sai Lầm Thường Gặp & Mẹo Pro

| Vấn đề | Nguyên nhân | Cách khắc phục |
|-------|-------------|----------------|
| Số xuất hiện lệch trung tâm | Tọa độ Rectangle tính từ góc dưới‑trái của trang. | Đảo ngược giá trị Y (`pageHeight - marginTop`) hoặc dùng `page.PageInfo.Height` để tính vị trí lề trên. |
| Trường không hiển thị trong Adobe Reader | Viền mặc định được đặt là “No”. | Đặt `batesField.Border = new Border { Width = 0.5f, Color = Color.Black };` |
| PDF lớn gây áp lực bộ nhớ | `using` chỉ giải phóng tài liệu sau khi vòng lặp kết thúc. | Xử lý các trang theo lô hoặc dùng `pdfDocument.Save` với `SaveOptions` cho phép streaming. |
| Không áp dụng giấy phép | Aspose in watermark trên trang đầu. | Đăng ký giấy phép sớm: `License lic = new License(); lic.SetLicense("Aspose.Pdf.lic");` |

---

## Mở Rộng Giải Pháp

- **Tiền tố tùy chỉnh:** Thay `"BATES-"` bằng bất kỳ chuỗi nào (`"DOC-"`, `"CASE-"`, …).  
- **Độ dài zero‑padding:** Thay `{pageNumber:D5}` bằng `{pageNumber:D3}` cho ba chữ số.  
- **Vị trí động:** Dùng `pdfDocument.Pages[pageNumber].PageInfo.Width` để đặt trường ở phía bên phải.  
- **Đánh số có điều kiện:** Bỏ qua các trang trắng bằng cách kiểm tra `pdfDocument.Pages[pageNumber].IsBlank`.

Tất cả các biến thể này vẫn giữ nguyên mẫu cốt lõi của **add bates numbers**, **add text field pdf**, và **add form field pdf**.

---

## Ví Dụ Hoàn Chỉnh (Tất Cả Trong Một)

Dưới đây là chương trình cuối cùng, sẵn sàng chạy, đã tích hợp các mẹo ở trên. Sao chép vào một console app mới và nhấn F5.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Forms;
using Aspose.Pdf.Text;
using Aspose.Pdf.Drawing;

class AddBatesNumbers
{
    static void Main()
    {
        // Register your license here (optional for trial)
        // var license = new License();
        // license.SetLicense("Aspose.Pdf.lic");

        string inputPath = @"YOUR_DIRECTORY\source.pdf";
        string outputPath = @"YOUR_DIRECTORY\bates.pdf";

        using (var pdfDocument = new Document(inputPath))
        {
            int totalPages = pdfDocument.Pages.Count;

            for (int i = 1; i <= totalPages; i++)
            {
                // Position the field 10 pts from left and 10 pts from bottom
                var rect = new Rectangle(10, 10, 150, 30);

                var batesField = new TextBoxField(pdfDocument.Pages[i], rect)
                {
                    Value = $"BATES-{i:D5}"
                };

                // Optional: make the field look nicer
                batesField.Border = new Border
                {
                    Width = 0.5f,
                    Color = Color.Gray
                };
                batesField.DefaultAppearance = new DefaultAppearance
                {
                    Font = FontRepository.FindFont("Arial"),
                    FontSize = 10,
                    ForegroundColor = Color.DarkBlue
                };

                pdfDocument.Form.Add(batesField, $"Bates_{i}", i);
            }

            pdfDocument.Save(outputPath);
        }

        Console.WriteLine($"✅ Finished! Bates numbers saved to: {outputPath}");
    }
}
```

Chạy nó, mở kết quả, và bạn sẽ thấy một định danh chuyên nghiệp trên mỗi trang — chính xác những gì một chuyên gia hỗ trợ kiện tụng mong đợi.

---

## Kết Luận

Chúng ta vừa trình diễn **cách add bates numbers** vào bất kỳ PDF nào bằng C# và Aspose.PDF. Bằng việc tạo một **text box field** trên mỗi trang, chúng ta đồng thời **add text field pdf**, **add form field pdf**, và **add page numbers pdf** trong một lần xử lý. Cách tiếp cận này nhanh, mở rộng được, và dễ tùy chỉnh cho tiền tố riêng, bố cục khác, hoặc logic điều kiện.

Sẵn sàng cho thử thách tiếp theo? Hãy thử nhúng mã QR liên kết tới file vụ án gốc, hoặc tạo một trang chỉ mục liệt kê tất cả số Bates cùng tiêu đề trang tương ứng. Cùng API này, bạn còn có thể hợp nhất PDF, trích xuất trang, và thậm chí xóa nhạy cảm — không giới hạn gì cả.

Nếu gặp khó khăn, hãy để lại bình luận bên dưới hoặc tham khảo tài liệu chính thức của Aspose để tìm hiểu sâu hơn. Chúc lập trình vui vẻ, và mong PDF của bạn luôn được đánh số hoàn hảo!  

---  

![add bates numbers screenshot](https://example.com/images/add-bates-numbers.png "add bates numbers example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}