---
category: general
date: 2026-03-22
description: Thêm đánh số Bates vào PDF nhanh chóng với Aspose.Pdf. Tìm hiểu cách
  thêm Bates, thêm số trang tuần tự, thêm chân trang tùy chỉnh vào PDF và thêm artifact
  vào PDF trong vài phút.
draft: false
keywords:
- add bates numbering pdf
- how to add bates
- add sequential page numbers
- add custom footer pdf
- add artifact to pdf
language: vi
og_description: Thêm đánh số Bates vào PDF bằng Aspose.Pdf. Hướng dẫn này cho thấy
  cách thêm Bates, thêm số trang tuần tự, thêm chân trang tùy chỉnh vào PDF và thêm
  artifact vào PDF.
og_title: Thêm Đánh số Bates vào PDF – Hướng dẫn C# Từng bước
tags:
- Aspose.Pdf
- C#
- PDF automation
title: Thêm Số Bates vào PDF – Hướng Dẫn C# Đầy Đủ
url: /vi/net/programming-with-stamps-and-watermarks/add-bates-numbering-pdf-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Thêm Số Bates vào PDF – Hướng Dẫn Đầy Đủ C#

Bạn đã bao giờ cần **thêm số bates pdf** vào một loạt tài liệu pháp lý nhưng không biết bắt đầu từ đâu? Bạn không phải là người duy nhất—nhiều nhà phát triển gặp khó khăn này khi xây dựng công cụ quản lý vụ án. Tin tốt là gì? Với Aspose.Pdf, bạn có thể **thêm bates**, **thêm số trang tuần tự**, và thậm chí **thêm phần chân trang tùy chỉnh pdf** chỉ trong vài dòng mã.

Trong tutorial này, chúng ta sẽ đi qua toàn bộ quy trình, từ cài đặt thư viện đến lưu file cuối cùng, và sẽ chia sẻ một vài mẹo về cách **thêm artifact vào pdf** mà không làm hỏng nội dung hiện có. Khi hoàn thành, bạn sẽ có một đoạn mã sẵn sàng chạy mà có thể chèn vào bất kỳ dự án .NET nào.

## Những Gì Bạn Cần Chuẩn Bị

- .NET 6+ (mã chạy được trên .NET Core và .NET Framework)  
- Giấy phép Aspose.Pdf for .NET hợp lệ (bạn có thể bắt đầu với bản dùng thử miễn phí)  
- Một file PDF đầu vào (`input.pdf`) đặt trong thư mục bạn có thể tham chiếu  
- Visual Studio, Rider, hoặc bất kỳ trình soạn thảo C# nào bạn thích  

Chỉ vậy thôi—không cần thêm bất kỳ gói NuGet nào ngoài Aspose.Pdf.

## Bước 1: Cài Đặt Aspose.Pdf qua NuGet

Đầu tiên, hãy đưa thư viện vào máy của bạn. Mở terminal trong thư mục dự án và chạy:

```bash
dotnet add package Aspose.Pdf
```

Hoặc, nếu bạn đang dùng Package Manager Console của Visual Studio:

```powershell
Install-Package Aspose.Pdf
```

*Pro tip:* Sau khi cài đặt, kiểm tra lại rằng thư mục `Aspose.Pdf` xuất hiện dưới `Dependencies → Packages` trong Solution Explorer.

## Bước 2: Tải Tài Liệu PDF Nguồn

Bây giờ chúng ta tạo một đối tượng `Document` đại diện cho PDF cần dán dấu. Sử dụng câu lệnh `using` sẽ tự động giải phóng handle file.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using System.Drawing; // For Color

// Step 2: Load the source PDF
using var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");
```

Tại sao lại dùng `using var`? Nó đảm bảo việc giải phóng tài nguyên ngay cả khi có ngoại lệ, tránh các vấn đề khóa file khi bạn cố gắng ghi đè lại file cùng tên.

## Bước 3: Tạo và Cấu Hình Artifact Số Bates

Số Bates thực chất là một artifact dạng văn bản tồn tại trong cấu trúc logic của PDF. Bạn có thể xem nó như một **custom footer pdf** vì nó xuất hiện trên mọi trang mà không nằm trong luồng nội dung của trang.

```csharp
// Step 3: Define the Bates numbering artifact
var batesArtifact = new BatesNumberingArtifact
{
    Prefix = "INV-",          // Optional prefix – change as needed
    Start = 1000,             // Starting number
    Format = "0000",          // Zero‑padded format (e.g., 1000 → 1000)
    X = 500,                  // Horizontal position (points from left)
    Y = 20,                   // Vertical position (points from bottom)
    FontSize = 10,
    FontColor = Color.Black
};
```

### Tại Sao Các Cài Đặt Này Quan Trọng

- **Prefix**: Hữu ích để phân biệt loại tài liệu (ví dụ, “INV‑” cho hoá đơn).  
- **Start**: Đặt số đầu tiên; bạn có thể lấy giá trị này từ cơ sở dữ liệu nếu cần duy trì liên tục giữa các file.  
- **Format**: `"0000"` buộc hiển thị bốn chữ số, giúp căn chỉnh khi số tăng lên.  
- **X/Y**: Tọa độ đo từ góc dưới‑trái, vì vậy `Y = 20` đặt văn bản ngay trên lề trang. Điều chỉnh `X` nếu muốn căn trái hoặc căn giữa.

Nếu bạn muốn **thêm số trang tuần tự** thay vì số Bates, chỉ cần bỏ `Prefix` và thay đổi `Format` thành `"###"` hoặc bất kỳ mẫu nào bạn muốn.

## Bước 4: Áp Dụng Artifact cho Tất Cả Các Trang

Aspose.Pdf cho phép bạn gắn một artifact vào toàn bộ tài liệu chỉ bằng một lệnh. Đây là cách hiệu quả nhất để **thêm artifact vào pdf** mà không cần lặp qua từng trang một.

```csharp
// Step 4: Apply the artifact to the whole document
pdfDocument.Pages.AddArtifact(batesArtifact);
```

Ở phía sau, Aspose sẽ thêm artifact vào dictionary của mỗi trang, nghĩa là việc đánh số trở thành một phần của cấu trúc logic PDF—rất thích hợp cho việc trích xuất hoặc tìm kiếm sau này.

## Bước 5: Lưu PDF Đã Cập Nhật

Cuối cùng, ghi các thay đổi trở lại đĩa. Bạn có thể ghi đè lên file gốc hoặc lưu vào một file mới; cách sau an toàn hơn trong quá trình phát triển.

```csharp
// Step 5: Save the PDF with Bates numbers
pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
```

Khi mở `output.pdf` bằng một trình xem, bạn sẽ thấy “INV‑1000”, “INV‑1001”, … ở góc dưới‑phải của mỗi trang.

### Kiểm Tra Kết Quả

Mở PDF trong Adobe Acrobat hoặc bất kỳ trình xem nào và tìm các số. Nếu muốn xác nhận bằng mã, bạn có thể đọc lại artifact:

```csharp
foreach (var page in pdfDocument.Pages)
{
    foreach (var artifact in page.Artifacts)
    {
        Console.WriteLine($"Page {page.Number}: {artifact.Text}");
    }
}
```

Đoạn mã này in ra nhãn Bates của mỗi trang—rất tiện cho các bài kiểm tra tự động.

## Các Trường Hợp Cạnh & Câu Hỏi Thường Gặp

### PDF Của Tôi Đã Có Footer Rồi?

Thêm artifact sẽ không ghi đè lên footer hiện có vì artifact nằm ở lớp riêng. Tuy nhiên, nếu lo ngại về việc chồng chéo hình ảnh, hãy điều chỉnh tọa độ `Y` hoặc tăng offset `X` để di chuyển số Bates ra khỏi vị trí gây cản trở.

### Có Thể Dùng Font Hoặc Màu Khác Không?

Chắc chắn rồi. `BatesNumberingArtifact` kế thừa từ `Artifact`, vì vậy bạn có thể đặt `Font`, `FontColor`, và thậm chí `Opacity`. Ví dụ:

```csharp
batesArtifact.Font = FontRepository.FindFont("Arial");
batesArtifact.FontColor = Color.FromArgb(255, 0, 0); // Red
```

### Làm Sao Để Đặt Lại Bộ Đếm Khi Tạo Tài Liệu Mới?

Chỉ cần thay đổi `Start` trước khi gọi `AddArtifact`. Nếu bạn tạo nhiều PDF trong một vòng lặp, hãy giữ một bộ đếm trong logic ứng dụng của bạn.

### Phương Pháp Này Có Tương Thích Với PDF Được Mã Hoá Không?

Aspose.Pdf có thể mở PDF được mã hoá nếu bạn cung cấp mật khẩu:

```csharp
var loadOptions = new LoadOptions { Password = "mySecret" };
using var pdfDocument = new Document("encrypted.pdf", loadOptions);
```

Sau khi giải mã, các bước thêm artifact vẫn hoạt động bình thường.

## Ví Dụ Hoàn Chỉnh

Dưới đây là chương trình đầy đủ, sẵn sàng chạy. Dán vào một ứng dụng console, chỉnh đường dẫn, và nhấn **F5**.

```csharp
using System;
using System.Drawing;               // For Color
using Aspose.Pdf;
using Aspose.Pdf.Annotations;

class Program
{
    static void Main()
    {
        // Load the source PDF
        using var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");

        // Create the Bates numbering artifact
        var batesArtifact = new BatesNumberingArtifact
        {
            Prefix = "INV-",
            Start = 1000,
            Format = "0000",
            X = 500,
            Y = 20,
            FontSize = 10,
            FontColor = Color.Black
        };

        // Apply the artifact to every page
        pdfDocument.Pages.AddArtifact(batesArtifact);

        // Save the result
        pdfDocument.Save("YOUR_DIRECTORY/output.pdf");

        Console.WriteLine("Bates numbering added successfully!");
    }
}
```

**Kết quả mong đợi:** Console in ra “Bates numbering added successfully!” và `output.pdf` chứa các nhãn tuần tự như `INV‑1000`, `INV‑1001`, …, được đặt ở góc dưới‑phải của mỗi trang.

## Tóm Tắt Nhanh

- **Mục tiêu chính:** **thêm số bates pdf** bằng Aspose.Pdf.  
- Chúng ta đã đề cập tới **cách thêm bates**, **cách thêm số trang tuần tự**, và **cách thêm custom footer pdf** thông qua một artifact duy nhất.  
- Tutorial cho thấy cách **thêm artifact vào pdf**, xử lý các trường hợp đặc biệt, và kiểm tra kết quả.  

## Tiếp Theo?

- **Tiền tố động:** Lấy giá trị từ cơ sở dữ liệu để tạo “CASE‑2023‑001”, “CASE‑2023‑002”, …  
- **Đặt vị trí có điều kiện:** Dùng phát hiện kích thước trang (`page.MediaBox`) để căn giữa số trên các trang ngang.  
- **Kết hợp với watermark:** Thêm logo bán trong suốt bên cạnh số Bates để tăng nhận diện thương hiệu.  

Hãy thử nghiệm—có thể bạn sẽ khám phá ra cách thông minh hơn để xử lý hàng ngàn file cùng lúc. Nếu gặp khó khăn, hãy để lại bình luận hoặc tham khảo tài liệu chính thức của Aspose (rất dễ hiểu). Chúc bạn lập trình vui vẻ!  

![ví dụ thêm số Bates vào PDF](https://example.com/bates-numbering-screenshot.png "Ảnh chụp màn hình cho việc thêm số Bates vào PDF trong trình xem PDF")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}