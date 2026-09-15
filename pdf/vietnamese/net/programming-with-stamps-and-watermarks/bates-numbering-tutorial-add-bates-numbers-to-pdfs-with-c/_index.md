---
category: general
date: 2026-02-25
description: Hướng dẫn đánh số Bates – học cách thêm số trang vào PDF và áp dụng đánh
  số Bates tùy chỉnh bằng Aspose.Pdf trong C#. Hướng dẫn chi tiết từng bước kèm mã
  nguồn đầy đủ.
draft: false
keywords:
- bates numbering tutorial
- add page numbers pdf
- how to add bates
- add bates numbering
language: vi
og_description: Hướng dẫn đánh số Bates cho bạn biết cách thêm số trang PDF và đánh
  số Bates tùy chỉnh trong C#. Bao gồm mã đầy đủ, giải thích và mẹo.
og_title: Hướng dẫn đánh số Bates – Thêm số Bates vào PDF bằng C#
tags:
- PDF
- C#
- Aspose.Pdf
title: 'Hướng dẫn đánh số Bates: Thêm số Bates vào PDF bằng C#'
url: /vi/net/programming-with-stamps-and-watermarks/bates-numbering-tutorial-add-bates-numbers-to-pdfs-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# hướng dẫn đánh số Bates – Thêm số Bates vào PDF trong C#

Bạn đã bao giờ tự hỏi cách thêm số trang vào PDF đồng thời nhúng một số Bates kiểu pháp lý chưa? Bạn không phải là người duy nhất. Trong **bates numbering tutorial** này, chúng ta sẽ đi qua mọi thứ bạn cần biết để dán nhãn mỗi trang của PDF bằng một tiền tố tùy chỉnh, số 0 ở đầu và vị trí chính xác — sử dụng Aspose.Pdf cho .NET.

Tin tốt? Nó khá đơn giản một khi bạn nắm bắt được các khái niệm cốt lõi. Khi kết thúc hướng dẫn này, bạn sẽ có một chương trình có thể chạy được, nhận *input.pdf* và tạo ra *bates_out.pdf* với nhãn “ABC‑01000” gọn gàng trên mỗi trang. Hãy bắt đầu.

## Những gì bạn cần

- **Aspose.Pdf cho .NET** (phiên bản 23.10 trở lên). Thư viện này là thương mại, nhưng bản dùng thử miễn phí vẫn đủ cho việc học.
- .NET 6+ SDK (bất kỳ phiên bản mới nào cũng được).
- Môi trường phát triển C# cơ bản — Visual Studio, VS Code hoặc Rider.
- Một tệp PDF đầu vào để thử nghiệm (bất kỳ tài liệu đa trang nào cũng minh hoạ hiệu ứng).

Không cần bất kỳ gói NuGet nào ngoài Aspose.Pdf, và mã chạy trên Windows, Linux hoặc macOS mà không cần chỉnh sửa.

## Bước 1: Tải tài liệu PDF nguồn (bates numbering tutorial – initialization)

Đầu tiên chúng ta tạo một đối tượng `Document` đại diện cho PDF mà chúng ta muốn chỉnh sửa. Hãy tưởng tượng đó là một canvas trống mà bạn có thể vẽ lên.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Annotations;

// Load the source PDF – replace the path with your actual file location
Document pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");

// Quick sanity check – make sure the document actually has pages
if (pdfDocument.Pages.Count == 0)
{
    throw new InvalidOperationException("The PDF you provided contains no pages.");
}
```

**Tại sao điều này quan trọng:** Nếu không tải tệp, sẽ không có gì để chú thích. Kiểm tra tính hợp lệ ngăn ngừa lỗi im lặng khi bạn cố gắng thêm các artifact vào một bộ sưu tập trang không tồn tại.

## Bước 2: Định nghĩa Bates Numbering Artifact (cách thêm bates)

Một *BatesNumberingArtifact* cho Aspose biết nơi và cách vẽ định danh. Bạn có thể điều chỉnh tiền tố, số bắt đầu, số 0 ở đầu, kích thước phông chữ và tọa độ X/Y chính xác.

```csharp
// Configure the Bates numbering artifact
BatesNumberingArtifact batesArtifact = new BatesNumberingArtifact
{
    Prefix = "ABC",          // Text that appears before the number
    Start = 1000,            // First number in the sequence
    LeadingZeros = 5,        // Pad the number with zeros (e.g., 01000)
    FontSize = 9,            // Small enough to sit in the margin
    Position = new Position   // Position measured from the lower‑left corner
    {
        X = 50,               // Horizontal offset (points)
        Y = 30                // Vertical offset (points)
    }
};
```

**Tại sao điều này quan trọng:** Thuộc tính `LeadingZeros` đảm bảo mỗi nhãn có cùng độ dài, điều này rất quan trọng đối với tài liệu pháp lý nơi việc căn chỉnh là yếu tố then chốt. Điều chỉnh `X` và `Y` để di chuyển dấu tới góc trên‑phải, góc dưới‑trái, hoặc bất kỳ vị trí nào quy trình của bạn yêu cầu.

## Bước 3: Gắn Artifact vào mọi trang (add page numbers pdf)

Bây giờ chúng ta lặp qua từng trang và gắn cùng một artifact. Đây là nơi yêu cầu *add page numbers pdf* được thực hiện — mỗi trang sẽ tự động nhận nhãn tuần tự riêng.

```csharp
// Iterate over each page and add the Bates artifact
foreach (Page page in pdfDocument.Pages)
{
    // The artifact is added to the page's Artifacts collection.
    // Aspose will handle the incrementing of the number for us.
    page.Artifacts.Add(batesArtifact);
}
```

**Tại sao điều này quan trọng:** Bằng cách thêm artifact vào bộ sưu tập `Artifacts` thay vì vẽ văn bản thủ công, chúng ta để Aspose quản lý logic đánh số, số 0 ở đầu và việc render. Điều này giảm lỗi và giữ cho mã ngắn gọn.

## Bước 4: Lưu PDF đã chỉnh sửa (add bates numbering)

Cuối cùng, chúng ta ghi các thay đổi vào một tệp mới. Thói quen tốt là ghi vào một tên tệp khác để giữ nguyên bản gốc.

```csharp
// Save the PDF with Bates numbers applied
pdfDocument.Save("YOUR_DIRECTORY/bates_out.pdf");

// Optional: let the user know we succeeded
Console.WriteLine("Bates numbering applied successfully! Output saved to bates_out.pdf");
```

**Tại sao điều này quan trọng:** Phương thức `Save` ghi toàn bộ PDF, nhúng các artifact như một phần của luồng nội dung trang. Tệp kết quả có thể mở bằng bất kỳ trình xem PDF nào và sẽ hiển thị số Bates chính xác như đã chỉ định.

## Ví dụ hoàn chỉnh (Tất cả các bước kết hợp)

Dưới đây là chương trình đầy đủ, sẵn sàng chạy. Sao chép‑dán vào dự án console, thay thế các đường dẫn placeholder, và nhấn **F5**.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the source PDF
            Document pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");
            if (pdfDocument.Pages.Count == 0)
                throw new InvalidOperationException("The PDF you provided contains no pages.");

            // 2️⃣ Configure the Bates numbering artifact
            BatesNumberingArtifact batesArtifact = new BatesNumberingArtifact
            {
                Prefix = "ABC",
                Start = 1000,
                LeadingZeros = 5,
                FontSize = 9,
                Position = new Position { X = 50, Y = 30 }
            };

            // 3️⃣ Attach the artifact to every page
            foreach (Page page in pdfDocument.Pages)
            {
                page.Artifacts.Add(batesArtifact);
            }

            // 4️⃣ Save the modified PDF
            pdfDocument.Save("YOUR_DIRECTORY/bates_out.pdf");
            Console.WriteLine("Bates numbering applied successfully! Output saved to bates_out.pdf");
        }
    }
}
```

### Kết quả mong đợi

Mở *bates_out.pdf* trong Adobe Reader, Foxit hoặc bất kỳ trình xem nào. Bạn sẽ thấy một nhãn như **ABC‑01000** trên trang đầu, **ABC‑01001** trên trang thứ hai, và cứ tiếp tục như vậy, đặt cách mép trái 50 pts và cách mép dưới 30 pts. Các số được căn phải nhờ số 0 ở đầu, tạo cho tài liệu một vẻ ngoài sạch sẽ, chuyên nghiệp.

## Các biến thể phổ biến & Trường hợp đặc biệt

| Kịch bản | Cách điều chỉnh |
|----------|-----------------|
| **Tiền tố khác** | Thay `Prefix = "XYZ"` trong định nghĩa artifact. |
| **Bắt đầu ở số tùy chỉnh** | Đặt `Start = 5000` (hoặc bất kỳ số nguyên nào). |
| **Đặt số ở góc trên‑phải** | Sử dụng `Position = new Position { X = pdfDocument.PageInfo.Width - 50, Y = pdfDocument.PageInfo.Height - 30 }`. |
| **Thay đổi kích thước phông chữ cho tài liệu lớn** | Sửa `FontSize = 12` (hoặc bất kỳ kích thước nào). |
| **Thêm hình chữ nhật nền** | Tạo một `RectangleArtifact` và thêm nó trước `BatesNumberingArtifact`. |
| **Bỏ qua một số trang** | Trong vòng `foreach`, thêm `if (page.Number % 2 == 0) continue;` để bỏ qua các trang chẵn. |

**Mẹo chuyên nghiệp:** Luôn thử nghiệm với một PDF ngắn trước. Việc này giúp bạn nhanh chóng xác nhận vị trí trước khi chạy script trên tệp 200 trang.

## Câu hỏi thường gặp

- **Điều này có hoạt động với PDF được mã hoá không?**  
  Aspose.Pdf có thể mở các tệp được bảo vệ bằng mật khẩu nếu bạn cung cấp mật khẩu qua `Document(string, string)`. Artifact Bates vẫn sẽ được áp dụng sau khi giải mã.

- **Tôi có thể thêm cả số Bates và số trang thông thường không?**  
  Có. Thêm một `PageNumberArtifact` cùng với `BatesNumberingArtifact`. Mỗi artifact duy trì bộ đếm riêng của mình.

- **Nếu PDF của tôi có các kích thước trang khác nhau thì sao?**  
  Các giá trị `Position` là điểm tuyệt đối. Đối với tài liệu kích thước hỗn hợp, tính vị trí cho mỗi trang bên trong vòng lặp bằng cách sử dụng `page.PageInfo.Width` và `page.PageInfo.Height`.

## Bước tiếp theo & Các chủ đề liên quan

Bây giờ bạn đã nắm vững **bates numbering tutorial**, bạn có thể muốn khám phá:

- **Thêm watermark** – cách tiếp cận artifact tương tự với `TextArtifact`.
- **Ghép nhiều PDF** – sử dụng `Document.AppendDocument`.
- **Trích xuất văn bản để lập chỉ mục tìm kiếm** – lớp `TextAbsorber`.
- **Tự động xử lý hàng loạt** – lặp qua một thư mục các PDF và áp dụng cùng một artifact.

Tất cả các chủ đề này dựa trên cùng các khái niệm bạn vừa học, vì vậy bạn đã sẵn sàng mở rộng bộ công cụ tự động hoá PDF của mình.

---

*Chúc lập trình vui vẻ! Nếu gặp khó khăn hoặc có ý tưởng tùy chỉnh thêm, hãy để lại bình luận bên dưới. Thế giới thao tác PDF rộng lớn, nhưng với một **bates numbering tutorial** vững chắc trong tay, bạn đã đi trước một bước dài.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}