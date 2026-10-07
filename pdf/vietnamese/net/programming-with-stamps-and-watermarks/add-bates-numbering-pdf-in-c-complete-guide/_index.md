---
category: general
date: 2026-03-14
description: Thêm số Bates vào PDF bằng Aspose.Pdf trong C#. Tìm hiểu cách thêm số
  Bates và tự động đánh số trang liên tiếp cho các tài liệu pháp lý hoặc lưu trữ.
draft: false
keywords:
- add bates numbering pdf
- how to add bates
- add sequential page numbers
- Aspose PDF Bates artifact
- C# PDF automation
language: vi
og_description: Thêm đánh số Bates vào PDF từng bước. Hướng dẫn này cho thấy cách
  thêm Bates và đánh số trang tuần tự bằng Aspose.Pdf cho .NET.
og_title: Thêm Đánh số Bates vào PDF bằng C# – Hướng dẫn đầy đủ
tags:
- Aspose.Pdf
- C#
- PDF
- Bates numbering
title: Thêm số Bates vào PDF trong C# – Hướng dẫn toàn diện
url: /vi/net/programming-with-stamps-and-watermarks/add-bates-numbering-pdf-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Thêm Số Bates vào PDF – Hướng Dẫn Toàn Diện

Bạn đã bao giờ cần **add bates numbering pdf** vào một bộ tài liệu pháp lý khổng lồ nhưng không chắc bắt đầu từ đâu chưa? Thêm số Bates là một công việc thường xuyên, nhưng lại bất ngờ phức tạp, trong quy trình xem xét tài liệu. Tin tốt là gì? Với Aspose.Pdf cho .NET, bạn có thể tự động hoá toàn bộ quá trình chỉ trong vài dòng mã.

Trong hướng dẫn này, chúng tôi sẽ hướng dẫn **how to add bates** cho mỗi trang của một PDF, thảo luận các tùy chọn **add sequential page numbers**, và cho bạn xem một mẫu mã đã sẵn sàng chạy. Khi kết thúc, bạn sẽ có một giải pháp tự chứa có thể đưa vào bất kỳ dự án C# nào — không cần script bổ sung, không cần dán nhãn thủ công.

## Những Gì Bạn Cần

- **Aspose.Pdf for .NET** (phiên bản 23.10 hoặc mới hơn). Thư viện là thương mại, nhưng bản đánh giá miễn phí vẫn hoạt động tốt cho việc thử nghiệm.
- Môi trường phát triển .NET (Visual Studio, Rider, hoặc `dotnet` CLI).
- Một tệp PDF đầu vào (`input.pdf`) mà bạn muốn gắn nhãn.
- Một chút kiên nhẫn cho những trường hợp đặc biệt thỉnh thoảng (chúng tôi sẽ đề cập tới).

Nếu bạn đã có những thứ này, tuyệt vời — hãy bắt đầu.

![Add Bates Numbering PDF example](/images/bates-numbering-example.png "Screenshot showing a PDF with add bates numbering pdf applied")

## Bước 1: Thiết Lập Dự Án và Cài Đặt Aspose.Pdf

Để giữ mọi thứ gọn gàng, hãy bắt đầu một ứng dụng console mới:

```bash
dotnet new console -n BatesNumberingDemo
cd BatesNumberingDemo
dotnet add package Aspose.Pdf
```

Lệnh `dotnet add package` sẽ tải bộ lắp ráp Aspose.Pdf mới nhất từ NuGet, vì vậy bạn đã sẵn sàng để viết mã.

### Tại sao lại là ứng dụng console?

Một ứng dụng console nhẹ, chạy ở bất kỳ đâu, và cho phép bạn tập trung vào logic PDF mà không bị phân tâm bởi giao diện người dùng. Tất nhiên, bạn có thể sau này di chuyển mã vào một web API hoặc dịch vụ nền — không có gì trong logic cốt lõi buộc bạn phải dùng console.

## Bước 2: Tải PDF Nguồn

Mở tài liệu rất đơn giản. Chúng ta sẽ sử dụng khối `using` để tự động giải phóng handle của tệp.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using System.Drawing;   // Required for Color

class Program
{
    static void Main()
    {
        // Adjust these paths to match your environment
        string sourcePdfPath = @"C:\Docs\input.pdf";
        string outputPdfPath = @"C:\Docs\output.pdf";

        // Load the PDF – this is where the “add bates numbering pdf” process begins
        using (var pdfDocument = new Document(sourcePdfPath))
        {
            // Next steps go here...
        }
    }
}
```

**Điều gì đang xảy ra?** Lớp `Document` đại diện cho toàn bộ tệp PDF. Bằng cách bao bọc nó trong `using`, chúng ta đảm bảo `Dispose` được gọi, ghi bất kỳ thay đổi nào còn lại ra đĩa.

## Bước 3: Định Nghĩa Bates Number Artifact (Lõi “how to add bates”)

Aspose.Pdf coi số Bates là *artifact* — siêu dữ liệu có thể được hiển thị trên màn hình hoặc in ra, nhưng không trở thành luồng nội dung cố định trừ khi bạn flatten PDF. Đây là đối tượng chúng ta sẽ gắn vào mỗi trang:

```csharp
var batesArtifact = new BatesNumberArtifact
{
    Prefix = "CASE-",
    StartNumber = 1000,
    Increment = 1,
    X = 36,               // 0.5 inch from the left edge (points)
    Y = 36,               // 0.5 inch from the bottom edge (points)
    FontSize = 9,
    FontColor = Color.Black
};
```

### Tại sao lại dùng artifact?

- **Performance:** Số được render ngay lập tức, vì vậy bạn có thể thay đổi tiền tố hoặc số bắt đầu mà không cần ghi lại toàn bộ PDF.
- **Flexibility:** Bạn có thể flatten PDF sau này nếu cần một dấu “hard‑coded” cho việc nộp hồ sơ pháp lý.
- **Precision:** Vị trí sử dụng đơn vị point (1/72 inch), cho phép bạn kiểm soát chính xác từng pixel.

Nếu bạn cần tiền tố khác hoặc phông chữ lớn hơn, chỉ cần điều chỉnh các thuộc tính. Trường `Increment` xác định cách số tăng từ trang này sang trang khác — hoàn hảo cho yêu cầu **add sequential page numbers**.

## Bước 4: Gắn Artifact vào Mỗi Trang

Bây giờ chúng ta lặp qua bộ sưu tập `Pages` và thêm artifact. Đây là hành động thực tế “add bates numbering pdf”.

```csharp
foreach (Page page in pdfDocument.Pages)
{
    page.Artifacts.Add(batesArtifact);
}
```

### Lưu Ý Trường Hợp Đặc Biệt

Nếu PDF của bạn đã chứa các Bates artifact, bạn có thể gặp trùng lặp. Một kiểm tra nhanh có thể ngăn chặn điều này:

```csharp
foreach (Page page in pdfDocument.Pages)
{
    bool alreadyHasBates = page.Artifacts.Any(a => a is BatesNumberArtifact);
    if (!alreadyHasBates)
        page.Artifacts.Add(batesArtifact);
}
```

Kiểm tra nhỏ này giúp bạn tránh tình huống dán nhãn đôi lộn xộn, đặc biệt khi xử lý hàng loạt tài liệu đã được gắn nhãn trước.

## Bước 5: Lưu PDF Đã Cập Nhật

Cuối cùng, ghi tệp trở lại đĩa. Bạn có thể ghi đè lên tệp gốc hoặc tạo tệp mới — ở đây chúng tôi sẽ tạo một bản sao mới:

```csharp
pdfDocument.Save(outputPdfPath);
Console.WriteLine($"Bates numbers added successfully. Output saved to {outputPdfPath}");
```

Khi bạn mở `output.pdf` bằng bất kỳ trình xem nào, bạn sẽ thấy “CASE‑1000”, “CASE‑1001”, v.v., ở góc dưới‑trái của mỗi trang.

### Tùy Chọn: Flatten PDF

Nếu người nhận yêu cầu PDF không thể chỉnh sửa (thường trong hồ sơ tòa án), hãy flatten các trang:

```csharp
pdfDocument.FlattenAllPages();   // Turns artifacts into permanent content
pdfDocument.Save(outputPdfPath);
```

Flatten là một thao tác một lần; sau khi thực hiện, các số Bates trở thành một phần của luồng nội dung trang và không thể thay đổi mà không phải xử lý lại.

## Ví Dụ Hoạt Động Đầy Đủ

Dưới đây là chương trình hoàn chỉnh bạn có thể sao chép‑dán vào `Program.cs`. Nó bao gồm bước flatten tùy chọn được chú thích để dễ bật/tắt.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using System;
using System.Drawing;
using System.Linq;

class Program
{
    static void Main()
    {
        string sourcePdfPath = @"C:\Docs\input.pdf";
        string outputPdfPath = @"C:\Docs\output.pdf";

        using (var pdfDocument = new Document(sourcePdfPath))
        {
            var batesArtifact = new BatesNumberArtifact
            {
                Prefix = "CASE-",
                StartNumber = 1000,
                Increment = 1,
                X = 36,
                Y = 36,
                FontSize = 9,
                FontColor = Color.Black
            };

            foreach (Page page in pdfDocument.Pages)
            {
                // Prevent duplicate artifacts if the PDF was processed before
                bool alreadyHasBates = page.Artifacts.Any(a => a is BatesNumberArtifact);
                if (!alreadyHasBates)
                    page.Artifacts.Add(batesArtifact);
            }

            // Uncomment the next line if you need a flattened PDF for legal submission
            // pdfDocument.FlattenAllPages();

            pdfDocument.Save(outputPdfPath);
        }

        Console.WriteLine($"Bates numbers added successfully. Output saved to {outputPdfPath}");
    }
}
```

Chạy nó bằng `dotnet run` và xem console xác nhận thao tác.

## Câu Hỏi Thường Gặp & Mẹo Chuyên Gia

| Câu hỏi | Trả lời |
|----------|--------|
| **Tôi có thể thay đổi vị trí trên mỗi trang không?** | Có. Thay vì sử dụng một `batesArtifact` duy nhất, hãy tạo một đối tượng mới trong vòng lặp và đặt `X`/`Y` dựa trên kích thước trang. |
| **Nếu PDF được bảo vệ bằng mật khẩu thì sao?** | Tải nó bằng `new Document(sourcePdfPath, new LoadOptions { Password = \"mySecret\" })`. Phần còn lại của quy trình vẫn không thay đổi. |
| **Tôi có cần lo lắng về hiệu năng khi xử lý các tệp lớn không?** | Thêm artifact có độ phức tạp O(N) trong đó N = số trang, và việc sử dụng bộ nhớ vẫn thấp vì Aspose stream các trang. Đối với PDF >10 000 trang, hãy cân nhắc xử lý theo lô để tránh các khoảng dừng GC kéo dài. |
| **Số thứ tự có thể được đặt lại cho mỗi phần không?** | Chắc chắn. Đặt `StartNumber` thành giá trị mới trước khi xử lý trang đầu tiên của phần tiếp theo, hoặc tạo một `BatesNumberArtifact` thứ hai với `Prefix` khác. |
| **Điều này có hoạt động trên .NET Core không?** | Có. Aspose.Pdf hỗ trợ .NET Framework, .NET Core và .NET 5/6+. Chỉ cần chỉ định runtime phù hợp trong tệp csproj của bạn. |

### Mẹo chuyên gia

Khi bạn làm việc với **add sequential page numbers** cho một bộ tài liệu đa tập, hãy lưu số cuối cùng đã dùng vào một tệp JSON nhỏ. Đọc nó trước khi bắt đầu, tăng số tương ứng, rồi ghi lại. Lớp lưu trữ nhỏ này ngăn ngừa việc sử dụng lại số một cách vô tình giữa các lần chạy.

## Xác Minh Kết Quả

Mở `output.pdf` trong Adobe Reader, Foxit, hoặc thậm chí Chrome. Bạn sẽ thấy một thứ gì đó như sau:

```
CASE-1000   (Page 1)
CASE-1001   (Page 2)
…
CASE-1015   (Page 16)
```

Nếu bạn đã flatten PDF, các số sẽ trở thành một phần của đồ họa trang — nhấp chuột phải → “Inspect” sẽ hiển thị chúng như các đối tượng văn bản thông thường.

## Kết Luận

Chúng tôi vừa trình bày cách **add bates numbering pdf** bằng Aspose.Pdf, khám phá cơ chế **how to add bates**, và minh họa cách sạch sẽ để **add sequential page numbers** trên toàn bộ tài liệu. Đoạn mã đã sẵn sàng cho môi trường sản xuất, xử lý các artifact trùng lặp, và thậm chí cung cấp bước flatten tùy chọn để đáp ứng yêu cầu pháp lý.

Tiếp theo, bạn có thể muốn khám phá:

- Kết hợp nhiều PDF đồng thời giữ liên tục số Bates (sử dụng `Document.AppendDocument` và điều chỉnh `StartNumber` ngay lập tức).
- Thêm mã QR bên cạnh số Bates để theo dõi tự động.
- Tích hợp logic này vào một API ASP.NET Core để dịch vụ web của bạn có thể gắn thẻ PDF theo yêu cầu.

Hãy thử nghiệm, điều chỉnh tiền tố, chơi với phông chữ, và để tự động hoá gánh bỏ công việc nặng nhọc trong quy trình xem xét tài liệu của bạn. Chúc lập trình vui vẻ!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}