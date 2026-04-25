---
category: general
date: 2026-04-25
description: Thêm đánh số Bates vào PDF nhanh chóng bằng Aspose.Pdf. Tìm hiểu cách
  thêm số trang vào PDF, tự động điều chỉnh kích thước phông chữ và thêm watermark
  văn bản trong C#.
draft: false
keywords:
- add bates numbering
- add page numbers pdf
- auto adjust font size
- how to add bates
- add text watermark
language: vi
og_description: Thêm đánh số Bates vào PDF bằng Aspose.Pdf. Hướng dẫn này chỉ cách
  thêm số trang vào PDF, tự động điều chỉnh kích thước phông chữ và thêm watermark
  văn bản trong một ví dụ duy nhất, có thể chạy được.
og_title: Thêm đánh số Bates vào PDF – Hướng dẫn đầy đủ Aspose.C#
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Thêm Số Bates vào PDF với Aspose – Hướng Dẫn Toàn Diện
url: /vi/net/programming-with-stamps-and-watermarks/add-bates-numbering-to-pdfs-with-aspose-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Thêm Số Bates vào PDF với Aspose – Hướng Dẫn Toàn Diện

Bạn đã bao giờ cần **thêm số bates** vào một PDF nhưng không biết bắt đầu từ đâu? Bạn không đơn độc—các nhóm pháp lý, kiểm toán viên và nhà phát triển đều gặp khó khăn này hàng ngày. Tin tốt? Với Aspose.Pdf cho .NET, bạn có thể dán số Bates, tự động điều chỉnh kích thước phông chữ, và thậm chí xử lý dấu dán như một watermark văn bản nhẹ—tất cả chỉ trong vài dòng C#.

Trong hướng dẫn này, chúng ta sẽ đi qua các bước **thêm số trang pdf**, tinh chỉnh phông chữ để không bao giờ tràn, và trả lời câu hỏi “cách thêm bates” một lần và mãi mãi. Khi hoàn thành, bạn sẽ có một ứng dụng console sẵn sàng chạy, tạo ra PDF được đánh số chuyên nghiệp, và bạn sẽ thấy cách mở rộng nó thành một giải pháp watermark đầy đủ.

## Các Điều Kiện Cần Thiết

Trước khi bắt đầu, hãy chắc chắn rằng bạn có:

* **Aspose.Pdf cho .NET** (gói NuGet mới nhất tính đến tháng 4 2026).  
* .NET 6.0 SDK hoặc mới hơn – API hoạt động tương tự trên .NET Framework, nhưng .NET 6 mang lại hiệu năng tốt nhất.  
* Một file PDF mẫu có tên `input.pdf` đặt trong thư mục bạn có thể tham chiếu (ví dụ, `C:\Docs\`).  

Không cần cấu hình bổ sung; thư viện đã tự chứa mọi thứ.

---

## Bước 1 – Tải Tài Liệu PDF Nguồn

Điều đầu tiên chúng ta làm là mở file cần đánh số. Lớp `Document` của Aspose đại diện cho toàn bộ PDF, và việc tải nó chỉ đơn giản là truyền đường dẫn vào hàm khởi tạo.

```csharp
using Aspose.Pdf;

string inputPath = @"C:\Docs\input.pdf";
Document pdfDocument = new Document(inputPath);
```

*Lý do quan trọng*: Khi tải tài liệu, bạn sẽ có quyền truy cập vào bộ sưu tập `Pages`, nơi chúng ta sẽ gắn dấu Bates sau này. Nếu file không tồn tại, Aspose sẽ ném ra một `FileNotFoundException` rõ ràng, giúp bạn biết chính xác lỗi gì đã xảy ra.

---

## Bước 2 – Tạo Text Stamp cho Số Bates

Bây giờ chúng ta tạo phần tử trực quan sẽ xuất hiện trên mỗi trang. Lớp `TextStamp` cho phép bạn nhúng bất kỳ chuỗi nào, và chúng ta sẽ dùng placeholder `{page}-{total}` để Aspose tự động thay thế các token này.

```csharp
// Create a stamp that will display "Bates: 1-10", "Bates: 2-10", etc.
TextStamp batesStamp = new TextStamp("Bates: {page}-{total}")
{
    // Let the stamp automatically adjust its font size to fit the stamp rectangle
    AutoAdjustFontSizeToFitStampRectangle = true,
    // Optional: make the stamp look like a subtle watermark
    Opacity = 0.4,
    // Position the stamp at the bottom‑right corner
    XIndent = 20,
    YIndent = 20,
    HorizontalAlignment = HorizontalAlignment.Right,
    VerticalAlignment = VerticalAlignment.Bottom,
    // Choose a readable font
    Font = new Font(FontFamilyEnum.Helvetica, 12, FontStyle.Regular, Color.Black)
};
```

*Các điểm chính*:

* **auto adjust font size** – Đặt `AutoAdjustFontSizeToFitStampRectangle` thành `true` đảm bảo văn bản không bao giờ tràn ra ngoài hình chữ nhật, rất phù hợp cho các số trang có độ dài thay đổi.  
* **add text watermark** – Bằng cách giảm `Opacity` chúng ta biến số Bates thành một watermark nhẹ, đáp ứng yêu cầu “add text watermark” mà không cần bước riêng.  
* **how to add bates** – Các token `{page}` và `{total}` là bí quyết; Aspose thay thế chúng tại thời gian chạy, vì vậy bạn không cần tự tính toán gì.

---

## Bước 3 – Áp Dụng Stamp cho Mọi Trang

Một lỗi thường gặp là chỉ dán stamp lên trang đầu. Để thực sự **add page numbers pdf**, chúng ta cần lặp qua toàn bộ bộ sưu tập `Pages`.

```csharp
foreach (Page page in pdfDocument.Pages)
{
    // Clone the stamp for each page to avoid shared state issues
    page.AddStamp(batesStamp);
}
```

Tại sao phải clone? Phương thức `AddStamp` bên trong tạo một bản sao, nhưng việc tạo một instance mới cho mỗi vòng lặp giúp tránh các hiệu ứng phụ nếu bạn thay đổi thuộc tính stamp (ví dụ, đổi màu cho các trang cụ thể) sau này.

---

## Bước 4 – Lưu PDF Đã Cập Nhật

Sau khi đã dán stamp, việc lưu các thay đổi trở nên đơn giản. Bạn có thể ghi đè lên file gốc hoặc lưu vào vị trí mới—ở đây chúng ta sẽ lưu file mới có tên `output.pdf`.

```csharp
string outputPath = @"C:\Docs\output.pdf";
pdfDocument.Save(outputPath);
Console.WriteLine($"Bates‑numbered PDF saved to: {outputPath}");
```

Nếu bạn mở `output.pdf`, sẽ thấy mỗi trang được gắn nhãn “Bates: 1‑10”, “Bates: 2‑10”, … ngay ở góc dưới‑phải, với độ trong suốt nhẹ vừa đủ để **add text watermark**.

---

## Ví Dụ Hoàn Chỉnh

Kết hợp tất cả lại, đây là một chương trình console tự chứa mà bạn có thể sao chép‑dán vào Visual Studio.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Drawing;
using Aspose.Pdf.Annotations;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source PDF
        string inputPath = @"C:\Docs\input.pdf";
        Document pdfDocument = new Document(inputPath);

        // 2️⃣ Create a Bates number stamp with auto‑adjusted font size
        TextStamp batesStamp = new TextStamp("Bates: {page}-{total}")
        {
            AutoAdjustFontSizeToFitStampRectangle = true,
            Opacity = 0.4, // acts as a subtle watermark
            XIndent = 20,
            YIndent = 20,
            HorizontalAlignment = HorizontalAlignment.Right,
            VerticalAlignment = VerticalAlignment.Bottom,
            Font = new Font(FontFamilyEnum.Helvetica, 12, FontStyle.Regular, Color.Black)
        };

        // 3️⃣ Add the stamp to every page (adds page numbers pdf)
        foreach (Page page in pdfDocument.Pages)
        {
            page.AddStamp(batesStamp);
        }

        // 4️⃣ Save the result
        string outputPath = @"C:\Docs\output.pdf";
        pdfDocument.Save(outputPath);
        Console.WriteLine($"Bates‑numbered PDF saved to: {outputPath}");
    }
}
```

**Kết quả mong đợi**: Mở `output.pdf` bằng bất kỳ trình xem nào; mỗi trang sẽ hiển thị một dòng như “Bates: 3‑12” ở góc dưới‑phải, kích thước vừa khít với hình chữ nhật và được render với độ trong suốt 40 %. Điều này đáp ứng cả yêu cầu theo dõi pháp lý và nhu cầu watermark trực quan.

---

## Các Biến Thể Thông Thường & Trường Hợp Cạnh

| Tình huống | Cần thay đổi | Lý do |
|-----------|----------------|-----|
| **Vị trí khác** | Điều chỉnh `HorizontalAlignment` / `VerticalAlignment` hoặc đặt `XIndent`/`YIndent` | Một số công ty thích đặt ở góc trên‑trái hoặc trung tâm. |
| **Tiền tố tùy chỉnh** | Thay `"Bates: "` bằng `"Doc‑ID: "` hoặc bất kỳ chuỗi nào | Bạn có thể đang dùng quy ước đặt tên khác. |
| **Nhiều stamp** | Tạo một `TextStamp` thứ hai (ví dụ, cho thông báo bảo mật) và thêm nó sau stamp đầu tiên | Kết hợp **add bates numbering** với các yêu cầu **add text watermark** khác là rất dễ dàng. |
| **Số trang lớn** | Tăng kích thước phông chữ ban đầu (ví dụ, `14`) – tính năng auto‑adjust sẽ giảm kích thước khi cần | Khi có > 999 trang, chuỗi sẽ dài hơn; auto‑adjust ngăn cắt bỏ. |
| **PDF được mã hoá** | Gọi `pdfDocument.Decrypt("password")` trước khi dán stamp | Không thể chỉnh sửa file bảo mật nếu không có mật khẩu. |

---

## Mẹo Chuyên Gia & Những Cạm Bẫy

* **Mẹo chuyên gia:** Đặt `batesStamp.Margin = new MarginInfo(5, 5, 5, 5)` nếu bạn nhận thấy văn bản quá sát mép trang.  
* **Cẩn thận với:** Các hình chữ nhật quá nhỏ (kích thước mặc định là 100 × 30 pt). Nếu cần khu vực lớn hơn, hãy đặt thủ công `batesStamp.Width` và `batesStamp.Height`.  
* **Lưu ý hiệu năng:** Dán stamp cho hàng ngàn trang có thể mất vài giây, nhưng Aspose stream các trang một cách hiệu quả—không cần tải toàn bộ tài liệu vào bộ nhớ.  

---

## Kết Luận

Chúng ta vừa minh họa cách **add bates numbering** vào PDF bằng Aspose.Pdf, đồng thời **add page numbers pdf**, kích hoạt **auto adjust font size**, và tạo **add text watermark** trong một quy trình liền mạch. Ví dụ đầy đủ, có thể chạy ngay ở trên cung cấp nền tảng vững chắc để bạn tùy chỉnh cho bất kỳ quy trình tài liệu pháp lý hoặc hệ thống báo cáo nội bộ nào.

Sẵn sàng cho bước tiếp theo? Hãy thử kết hợp cách này với API hợp nhất PDF của Aspose để xử lý hàng loạt file, hoặc khám phá lớp `TextFragment` để tạo watermark phong phú hơn (màu, xoay, đa dòng). Khả năng là vô hạn, và đoạn code bạn vừa có là nền tảng đáng tin cậy.

Nếu bạn thấy hướng dẫn này hữu ích, đừng ngại để lại bình luận, star repository, hoặc chia sẻ các biến thể của bạn. Chúc lập trình vui vẻ, và chúc PDF của bạn luôn được đánh số hoàn hảo!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}