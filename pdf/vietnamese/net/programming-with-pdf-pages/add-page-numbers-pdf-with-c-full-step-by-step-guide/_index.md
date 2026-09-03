---
category: general
date: 2026-01-02
description: Thêm số trang PDF nhanh chóng bằng Aspose.Pdf trong C#. Học cách thêm
  đánh số Bates, văn bản chân trang, dấu nước tùy chỉnh và lặp qua các trang PDF trong
  một script duy nhất.
draft: false
keywords:
- add page numbers pdf
- add bates numbering
- add footer text
- add custom watermark
- loop through pdf pages
language: vi
og_description: Thêm số trang PDF ngay lập tức với Aspose.Pdf. Hướng dẫn này cũng
  bao gồm cách thêm đánh số Bates, văn bản chân trang, watermark tùy chỉnh và duyệt
  qua các trang PDF.
og_title: Thêm số trang vào PDF bằng C# – Hướng dẫn lập trình đầy đủ
tags:
- C#
- Aspose.Pdf
- PDF manipulation
title: Thêm số trang vào PDF bằng C# – Hướng dẫn chi tiết từng bước
url: /vi/net/programming-with-pdf-pages/add-page-numbers-pdf-with-c-full-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Thêm số trang PDF bằng C# – Hướng dẫn lập trình đầy đủ

Bạn đã bao giờ cần **thêm số trang PDF** nhưng không biết bắt đầu từ đâu? Bạn không phải là người duy nhất—các nhà phát triển thường hỏi cách dán số, chân trang, hoặc thậm chí một định danh kiểu Bates lên mỗi trang của PDF.  

Trong hướng dẫn này, bạn sẽ thấy một ví dụ C# có thể chạy ngay, **lặp qua các trang PDF**, dán một chân trang số trang, và (nếu muốn) thêm một watermark tùy chỉnh. Chúng tôi cũng sẽ chỉ cho bạn cách chuyển dấu dán sang số Bates, tức là “thêm đánh số Bates” cho tài liệu pháp lý hoặc pháp y. Khi hoàn thành, bạn sẽ có một phương thức duy nhất, có thể tái sử dụng, xử lý tất cả các tác vụ này mà không gặp khó khăn.

## Thêm số trang PDF – Tổng quan

Trước khi đi vào mã, hãy làm rõ “thêm số trang PDF” thực sự có nghĩa gì trong thế giới Aspose.Pdf. Thư viện coi bất kỳ đoạn văn bản nào bạn đặt trên trang là một **TextStamp**. Bằng cách tạo một dấu dán với trình giữ chỗ trang (`{page}`) và áp dụng nó cho mỗi trang, bạn sẽ tự động nhận được đánh số tuần tự. Dấu dán cùng có thể mang thêm văn bản, vì vậy bạn có thể **thêm văn bản chân trang** như “Confidential” hoặc một định danh đặc thù cho vụ việc.

> **Tại sao sử dụng dấu dán (stamp) thay vì chỉnh sửa luồng nội dung PDF?**  
> Dấu dán là các đối tượng cấp cao, chúng tôn trọng lề trang, góc quay và đồ họa hiện có. Chúng cũng dễ bảo trì hơn rất nhiều—chỉ cần thay đổi một vài thuộc tính và chạy lại script.

## Lặp qua các trang PDF để áp dụng dấu dán

Bước thực tiễn đầu tiên là mở PDF nguồn và duyệt qua các trang của nó. Đây là mẫu **loop through pdf pages** cổ điển mà hầu hết các ví dụ Aspose sử dụng.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Paths – change these to match your environment
string sourcePdfPath = @"C:\Docs\input.pdf";
string outputPdfPath = @"C:\Docs\PageNumbered.pdf";

using (var pdfDocument = new Document(sourcePdfPath))
{
    // The loop – every Page object lives in pdfDocument.Pages
    foreach (Page page in pdfDocument.Pages)
    {
        // We'll attach a stamp later (see next section)
    }

    // Save the modified document
    pdfDocument.Save(outputPdfPath);
}
```

> **Mẹo chuyên nghiệp:** Nếu PDF của bạn rất lớn (hàng trăm trang), hãy cân nhắc xử lý theo lô để giảm mức sử dụng bộ nhớ. Aspose.Pdf stream các trang một cách lười biếng, vì vậy vòng lặp đã khá hiệu quả.

## Thêm đánh số Bates và văn bản chân trang

Bây giờ chúng ta có thể duyệt qua từng trang, hãy tạo một **TextStamp** có thể tái sử dụng, mang cả số trang và văn bản chân trang tùy chọn. Trình giữ chỗ `{page}` sẽ tự động được thay bằng chỉ số trang hiện tại.

```csharp
// Create a stamp that will be reused for every page
var batesStamp = new TextStamp("Bates-{page} – Confidential")
{
    // Position the stamp 20 points from the left and bottom edges
    XIndent = 20,
    YIndent = 20,
    // Align left‑bottom so it behaves like a traditional footer
    HorizontalAlignment = HorizontalAlignment.Left,
    VerticalAlignment   = VerticalAlignment.Bottom,
    // Font styling – Times New Roman, 10pt, bold, gray
    Font = new Font(FontFamily.TimesRoman, 10, FontStyle.Bold),
    TextState = { ForegroundColor = Color.Gray }
};

// Attach the stamp to every page
foreach (Page page in pdfDocument.Pages)
    page.AddStamp(batesStamp);
```

### Tại sao cách này hoạt động

* **`Bates-{page}`** – Aspose thay thế `{page}` bằng số trang thực tế, cho bạn một số Bates cổ điển một cách tự động.  
* **`Confidential`** – Đây là phần **add footer text**. Bạn có thể thay bằng bất kỳ chuỗi nào, thậm chí lấy dữ liệu từ cơ sở dữ liệu.  
* **Styling** – Sử dụng `TextState` cho phép bạn điều chỉnh màu, độ trong suốt và thậm chí góc quay mà không cần chạm vào luồng nội dung bên trong PDF.

Nếu bạn chỉ cần số thuần, hãy bỏ tiền tố “Bates‑” và phần văn bản phụ:

```csharp
var simpleStamp = new TextStamp("{page}")
{
    XIndent = 20,
    YIndent = 20,
    HorizontalAlignment = HorizontalAlignment.Center,
    VerticalAlignment   = VerticalAlignment.Bottom,
    Font = new Font(FontFamily.Helvetica, 12, FontStyle.Regular),
    TextState = { ForegroundColor = Color.Black }
};
```

## Thêm watermark tùy chỉnh (tùy chọn)

Đôi khi bạn muốn hơn một chân trang—cần một logo bán trong suốt hoặc một lớp phủ “DRAFT” trên toàn bộ trang. Đó là lúc **add custom watermark** xuất hiện. Lớp `TextStamp` giống nhau có thể được tái sử dụng, chỉ cần thay đổi căn chỉnh và độ trong suốt.

```csharp
var watermark = new TextStamp("DRAFT")
{
    // Center it both horizontally and vertically
    HorizontalAlignment = HorizontalAlignment.Center,
    VerticalAlignment   = VerticalAlignment.Center,
    // Make it big and light
    Font = new Font(FontFamily.Helvetica, 72, FontStyle.Bold),
    TextState = { ForegroundColor = Color.Red, FontSize = 72, FontStyle = FontStyle.Bold, 
                  Transparency = 0.5f }   // 50% transparent
};

// Apply the watermark on top of the page‑number stamp
foreach (Page page in pdfDocument.Pages)
{
    page.AddStamp(watermark);   // watermark on top
    page.AddStamp(batesStamp);  // then the footer
}
```

> **Lưu ý:** Thứ tự quan trọng. Thêm watermark trước sẽ đảm bảo các số trang vẫn dễ đọc phía trên văn bản bán trong suốt.

## Lưu PDF và xác minh kết quả

Sau khi dán dấu, bước cuối cùng là ghi các thay đổi trở lại đĩa. Lệnh `Save` chúng ta đã đặt ở trên thực hiện phần lớn công việc, nhưng hãy thêm một đoạn mã kiểm tra nhanh mở file mới và in ra số trang đã được xử lý.

```csharp
pdfDocument.Save(outputPdfPath);

// Quick verification
using (var resultDoc = new Document(outputPdfPath))
{
    Console.WriteLine($"✅ Successfully added page numbers to {resultDoc.Pages.Count} pages.");
}
```

Khi chạy toàn bộ chương trình, bạn sẽ thấy một PDF mà mỗi trang kết thúc bằng một chuỗi như **“Bates‑3 – Confidential”** (hoặc chỉ “3” nếu bạn dùng dấu dán đơn giản) và, nếu bạn bật watermark, một “DRAFT” mờ nhạt ở giữa trang.

### Kết quả mong đợi

| Trang | Chân trang (ví dụ) |
|------|--------------------|
| 1    | Bates‑1 – Confidential |
| 2    | Bates‑2 – Confidential |
| …    | … |
| N    | Bates‑N – Confidential |

Nếu bạn mở file trong trình xem, các số sẽ nằm cách lề trái và dưới 20 pts, phù hợp với quy ước tài liệu pháp lý thông thường.

## Ví dụ hoàn chỉnh (sẵn sàng sao chép)

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

string sourcePdfPath = @"C:\Docs\input.pdf";
string outputPdfPath = @"C:\Docs\PageNumbered.pdf";

using (var pdfDocument = new Document(sourcePdfPath))
{
    // ---------- Create the page‑number/footer stamp ----------
    var batesStamp = new TextStamp("Bates-{page} – Confidential")
    {
        XIndent = 20,
        YIndent = 20,
        HorizontalAlignment = HorizontalAlignment.Left,
        VerticalAlignment   = VerticalAlignment.Bottom,
        Font = new Font(FontFamily.TimesRoman, 10, FontStyle.Bold),
        TextState = { ForegroundColor = Color.Gray }
    };

    // ---------- Optional watermark ----------
    var watermark = new TextStamp("DRAFT")
    {
        HorizontalAlignment = HorizontalAlignment.Center,
        VerticalAlignment   = VerticalAlignment.Center,
        Font = new Font(FontFamily.Helvetica, 72, FontStyle.Bold),
        TextState = { ForegroundColor = Color.Red, Transparency = 0.5f }
    };

    // ---------- Apply stamps to every page ----------
    foreach (Page page in pdfDocument.Pages)
    {
        page.AddStamp(watermark);   // comment out if you don't need a watermark
        page.AddStamp(batesStamp);
    }

    // ---------- Save and verify ----------
    pdfDocument.Save(outputPdfPath);
    Console.WriteLine($"✅ Added page numbers and watermark to {pdfDocument.Pages.Count} pages.");
}
```

Lưu lại dưới tên `AddPageNumbers.cs`, khôi phục gói NuGet Aspose.Pdf (`Install-Package Aspose.Pdf`), và chạy nó. Bạn sẽ có một file **add page numbers pdf** đồng thời thể hiện **add bates numbering**, **add footer text**, **add custom watermark**, và mẫu **loop through pdf pages** cổ điển—tất cả trong một script gọn gàng.

![add page numbers pdf example](https://example.com/images/add-page-numbers-pdf.png "Screenshot showing numbered PDF pages with footer and watermark")

## Kết luận

Chúng ta đã bao quát mọi thứ bạn cần để **add page numbers pdf** bằng Aspose.Pdf trong C#. Từ việc lặp qua từng trang, dán số Bates, thêm văn bản chân trang tùy chỉnh, cho tới việc lớp watermark bán trong suốt, mã nguồn đủ ngắn gọn để chèn vào bất kỳ dự án nào hiện có.  

Tiếp theo, bạn có thể khám phá các kịch bản nâng cao hơn—như lấy văn bản chân trang từ cơ sở dữ liệu, áp dụng phông chữ khác nhau cho từng phần, hoặc tạo một PDF chỉ mục riêng liệt kê tất cả các số Bates. Tất cả các mở rộng này dựa trên cùng những ý tưởng cốt lõi mà chúng tôi đã trình bày, vì vậy bạn đã sẵn sàng mở rộng giải pháp khi yêu cầu tăng lên.  

Hãy thử nghiệm, tinh chỉnh kiểu dáng, và cho chúng tôi biết trong phần bình luận cách nó hoạt động với bạn. Chúc lập trình vui vẻ!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}