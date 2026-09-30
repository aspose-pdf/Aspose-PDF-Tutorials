---
category: general
date: 2026-01-15
description: Thêm số Bates vào PDF của bạn nhanh chóng với Aspose.Pdf. Tìm hiểu cách
  thêm chân trang vào PDF, thêm số trang vào PDF và thêm đánh số trang tùy chỉnh.
draft: false
keywords:
- add bates numbers
- bates numbering pdf
- add footer to pdf
- add page numbers pdf
- add custom page numbering
language: vi
og_description: Thêm số Bates vào PDF của bạn nhanh chóng với Aspose.Pdf. Tìm hiểu
  cách thêm chân trang vào PDF, thêm số trang vào PDF và thêm đánh số trang tùy chỉnh.
og_title: Thêm số Bates vào PDF – đánh số Bates cho PDF
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Thêm số Bates vào PDF – đánh số Bates PDF
url: /vi/net/programming-with-text/add-bates-numbers-to-pdf-bates-numbering-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Thêm Số Bates vào PDF – Hướng Dẫn Toàn Diện

Bạn đã bao giờ cần **add bates numbers** vào một PDF nhưng không chắc bắt đầu từ đâu? Bạn không đơn độc—các đội ngũ pháp lý, kiểm toán viên và bất kỳ ai làm việc với khối lượng tài liệu lớn đều gặp khó khăn này hàng ngày. Tin tốt là gì? Với Aspose.Pdf cho .NET, bạn có thể thêm những số đó vào mỗi trang chỉ với vài dòng mã.

Trong hướng dẫn này, chúng ta sẽ đi qua toàn bộ quy trình: từ việc nhập thư viện Aspose.Pdf, tải tệp nguồn của bạn, cấu hình một *BatesNumberingArtifact*, gắn nó như một footer, và cuối cùng lưu kết quả. Khi kết thúc, bạn cũng sẽ biết cách **add footer to pdf**, **add page numbers pdf**, và thậm chí **add custom page numbering** cho những trường hợp khó xử.

## Những Gì Bạn Cần

- .NET 6+ (hoặc .NET Framework 4.8 nếu bạn vẫn đang dùng stack cổ điển)  
- Tham chiếu tới gói NuGet **Aspose.Pdf** (`Install-Package Aspose.Pdf`)  
- Tệp PDF bạn muốn dán dấu (chúng tôi sẽ gọi nó là `source.pdf`)  

Đó là tất cả—không cần công cụ bổ sung, không cần trình chỉnh sửa PDF nặng. Hãy bắt đầu.

![add bates numbers example](https://example.com/images/add-bates-numbers.png "add bates numbers example")

## Bước 1: Thêm Số Bates – Tải Tài Liệu PDF

Đầu tiên, chúng ta cần một đối tượng `Document` đại diện cho PDF mà chúng ta sắp sửa chỉnh sửa. Hãy nghĩ về nó như mở một tài liệu Word trước khi bắt đầu gõ.

```csharp
using Aspose.Pdf;
using System;

class Program
{
    static void Main()
    {
        // Load the PDF you want to add bates numbers to
        var pdfDocument = new Document(@"YOUR_DIRECTORY\source.pdf");

        // The rest of the steps go here...
    }
}
```

> **Tại sao điều này quan trọng:** Việc tải tệp cho phép bạn truy cập vào bộ sưu tập `Pages` của nó, nơi chúng ta sẽ gắn artifact đánh số Bates sau này. Nếu tệp không tìm thấy, Aspose sẽ ném ra một `FileNotFoundException` rõ ràng, vì vậy hãy kiểm tra lại đường dẫn.

## Bước 2: Cấu Hình Cài Đặt bates numbering pdf

Bây giờ chúng ta định nghĩa *cách* các số sẽ hiển thị. `BatesNumberingArtifact` cho phép bạn đặt tiền tố, số bắt đầu, độ dài chữ số, hậu tố và vị trí. Đây là cốt lõi của **bates numbering pdf**.

```csharp
// Step 2: Create and configure the Bates numbering artifact
var batesArtifact = new BatesNumberingArtifact
{
    Prefix = "CASE-",
    StartNumber = 1000,
    NumberDigits = 5,          // forces 5 digits, e.g., 01000
    Suffix = "-A",
    Placement = BatesNumberingArtifact.PlacementLocation.BottomCenter
};
```

> **Mẹo chuyên nghiệp:** Nếu bạn cần các số xuất hiện ở header thay vì, hãy thay `BottomCenter` bằng `TopCenter`. Enum vị trí cũng hỗ trợ `BottomLeft`, `BottomRight`, v.v., cung cấp cho bạn tính linh hoạt cho các kiểu **add footer to pdf** khác nhau.

## Bước 3: Thêm page numbers pdf – Gắn Artifact vào Mỗi Trang

Với artifact đã sẵn sàng, chúng ta lặp qua từng trang và thêm nó vào bộ sưu tập `Artifacts`. Đây là bước thực sự **adds page numbers pdf**.

```csharp
// Step 3: Attach the artifact to each page
foreach (Page page in pdfDocument.Pages)
{
    page.Artifacts.Add(batesArtifact);
}
```

> **Điều gì đang diễn ra phía sau?** Bộ sưu tập `Artifacts` được render sau nội dung chính của trang, đảm bảo số Bates nằm trên bất kỳ văn bản hiện có nào nhưng dưới các chú thích. Nếu bạn cần số nằm phía sau nội dung (hiếm), bạn có thể dùng `page.Artifacts.Insert(0, batesArtifact)`.

## Bước 4: Thêm custom page numbering – Lưu PDF Đã Cập Nhật

Cuối cùng, chúng ta ghi tài liệu đã chỉnh sửa ra đĩa. Tệp đầu ra sẽ chứa các số Bates như một phần cố định của mỗi trang.

```csharp
// Step 4: Save the PDF with the new numbering
pdfDocument.Save(@"YOUR_DIRECTORY\bates_out.pdf");

Console.WriteLine("Bates numbers added successfully! Check bates_out.pdf.");
```

> **Mẹo kiểm tra:** Mở `bates_out.pdf` bằng bất kỳ trình xem nào. Bạn sẽ thấy một thứ gì đó giống như `CASE-01000-A` ở giữa dưới của mỗi trang. Nếu các số thiếu, hãy kiểm tra lại thuộc tính `Placement` có khớp với vị trí bạn mong muốn không.

## Ví Dụ Hoàn Chỉnh

Putting it all together, here’s the complete, ready‑to‑run program:

```csharp
using Aspose.Pdf;
using System;

class Program
{
    static void Main()
    {
        // Load the source PDF
        var pdfDocument = new Document(@"YOUR_DIRECTORY\source.pdf");

        // Configure Bates numbering artifact
        var batesArtifact = new BatesNumberingArtifact
        {
            Prefix = "CASE-",
            StartNumber = 1000,
            NumberDigits = 5,
            Suffix = "-A",
            Placement = BatesNumberingArtifact.PlacementLocation.BottomCenter
        };

        // Attach artifact to each page (adds page numbers pdf)
        foreach (Page page in pdfDocument.Pages)
        {
            page.Artifacts.Add(batesArtifact);
        }

        // Save the new PDF (adds footer to pdf)
        pdfDocument.Save(@"YOUR_DIRECTORY\bates_out.pdf");

        Console.WriteLine("Bates numbers added successfully! Check bates_out.pdf.");
    }
}
```

### Kết Quả Mong Đợi

- **File:** `bates_out.pdf` trong cùng thư mục với `source.pdf`
- **Visual:** Văn bản ở dưới‑giữa `CASE-01000-A`, `CASE-01001-A`, … cho mỗi trang tiếp theo
- **Behaviour:** Các số được nhúng vĩnh viễn; chúng tồn tại khi in, flatten, và chỉnh sửa tiếp theo.

## Các Biến Thể Thông Thường & Trường Hợp Đặc Biệt

| Tình Huống | Cách Điều Chỉnh |
|-----------|---------------|
| **Different starting number** | Thay `StartNumber` thành bất kỳ số nguyên nào (ví dụ, `StartNumber = 500`). |
| **Letter suffixes per volume** | Sử dụng vòng lặp để thay đổi `Suffix` cho mỗi trang, hoặc tạo nhiều artifact với các hậu tố khác nhau. |
| **Right‑aligned numbering** | Đặt `Placement = BatesNumberingArtifact.PlacementLocation.BottomRight`. |
| **Large documents (10k+ pages)** | Xem xét xử lý theo lô các trang hoặc tăng `NumberDigits` để tránh tràn. |
| **Need to hide numbers on certain pages** | Bỏ qua các trang đó trong vòng lặp `foreach` (ví dụ, `if (page.Number != 1) page.Artifacts.Add(batesArtifact);`). |

> **Cẩn thận:** Sử dụng `Prefix` hoặc `Suffix` chứa các ký tự không hợp lệ trong tên tệp (ví dụ, `*` hoặc `?`). Aspose vẫn sẽ nhúng chúng, nhưng có thể gây vấn đề khi bạn sau này trích xuất văn bản.

## Mẹo Chuyên Nghiệp cho Sản Xuất

- **Cache artifact** nếu bạn đang xử lý nhiều PDF liên tiếp; tạo một lần sẽ tiết kiệm vài mili giây cho mỗi tệp.  
- **Thread‑safety:** Đối tượng `BatesNumberingArtifact` không an toàn với đa luồng, vì vậy mỗi luồng nên có một bản sao riêng.  
- **Performance:** Đối với các lô lớn, tắt nén PDF (`pdfDocument.Compress = false`) trước khi lưu, sau đó bật lại nếu cần.  
- **Testing:** Luôn thực hiện kiểm tra nhanh bằng mắt trên PDF đầu tiên được tạo để đảm bảo vị trí phù hợp với tiêu chuẩn của đội pháp lý.

## Kết Luận

Bây giờ bạn đã có một công thức toàn diện, từ đầu đến cuối, để **add bates numbers** vào bất kỳ PDF nào bằng Aspose.Pdf, kèm theo các tùy chọn **add footer to pdf**, **add page numbers pdf**, và **add custom page numbering**. Mã hoàn toàn tự chứa, hoạt động với .NET 6 trở lên, và có thể được tích hợp vào bất kỳ pipeline tự động nào hiện có.

Tiếp theo là gì? Hãy thử thay đổi vị trí `BottomCenter` thành kiểu header, thử nghiệm với các tiền tố động (ví dụ, ID vụ án từ cơ sở dữ liệu), hoặc kết hợp với tính năng trích xuất văn bản của Aspose để tạo chỉ mục có thể tìm kiếm cho các tài liệu vừa được đánh số của bạn. Không có giới hạn, và bạn vừa có được một công cụ mạnh mẽ cho việc kiểm soát tài liệu.

Chúc lập trình vui vẻ, và mong các PDF của bạn luôn được đánh số hoàn hảo!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}