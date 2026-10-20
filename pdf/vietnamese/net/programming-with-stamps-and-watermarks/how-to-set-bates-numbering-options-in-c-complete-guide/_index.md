---
category: general
date: 2026-08-14
description: Cách thiết lập tùy chọn đánh số Bates trong C# bằng GroupDocs. Hãy làm
  theo hướng dẫn từng bước này để thêm tiền tố tùy chỉnh và số bắt đầu khi chuyển
  đổi Word sang PDF.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to set bates numbering options
- Bates numbering C#
- GroupDocs API
- document conversion C#
- AddBatesNumbering method
- C# PDF generation
language: vi
lastmod: 2026-08-14
og_description: Cách thiết lập tùy chọn đánh số Bates trong C# nhanh chóng. Hướng
  dẫn này chỉ cho bạn cách thêm tiền tố tùy chỉnh và số bắt đầu khi chuyển đổi Word
  sang PDF.
og_image_alt: Screenshot of C# code applying Bates numbering to a PDF
og_title: Cách thiết lập tùy chọn đánh số Bates trong C# – hướng dẫn từng bước
schemas:
- author: GroupDocs
  dateModified: '2026-08-14'
  description: How to set bates numbering options in C# using GroupDocs. Follow this
    step‑by‑step tutorial to add custom prefixes and start numbers when converting
    Word to PDF.
  headline: How to set bates numbering options in C# – complete guide
  type: TechArticle
- description: How to set bates numbering options in C# using GroupDocs. Follow this
    step‑by‑step tutorial to add custom prefixes and start numbers when converting
    Word to PDF.
  name: How to set bates numbering options in C# – complete guide
  steps:
  - name: '`Document` – loads the source file.'
    text: '`Document` – loads the source file.'
  - name: '`BatesNumberingOptions` – holds the start number, prefix, and other formatting
      details.'
    text: '`BatesNumberingOptions` – holds the start number, prefix, and other formatting
      details.'
  - name: '`AddBatesNumbering` – the method that injects the numbering into each page.'
    text: '`AddBatesNumbering` – the method that injects the numbering into each page.'
  type: HowTo
tags:
- Bates numbering
- C#
- .NET
- GroupDocs
- PDF conversion
title: Cách thiết lập tùy chọn đánh số Bates trong C# – hướng dẫn đầy đủ
url: /vi/net/programming-with-stamps-and-watermarks/how-to-set-bates-numbering-options-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách thiết lập tùy chọn đánh số Bates trong C# – hướng dẫn đầy đủ

Nếu bạn cần **cách thiết lập tùy chọn đánh số Bates** trong C#, hướng dẫn này sẽ đưa bạn qua các bước chính xác. Bạn sẽ học cách cấu hình số bắt đầu, thêm tiền tố và áp dụng việc đánh số khi chuyển đổi tài liệu Word sang PDF bằng GroupDocs API.

Quá trình xử lý tài liệu thường yêu cầu định danh duy nhất trên mỗi trang cho mục đích pháp lý hoặc lưu trữ. Khi kết thúc tutorial này, bạn sẽ có một đoạn mã có thể tái sử dụng, có thể chèn vào bất kỳ dự án .NET nào, dù bạn đang xây dựng công cụ hỗ trợ kiện tụng hay một trình tạo báo cáo tự động. Không cần công cụ bên ngoài—chỉ cần thư viện GroupDocs.Conversion và một vài dòng C#.

## Những gì bạn cần

* .NET 6.0 SDK hoặc phiên bản mới hơn đã được cài đặt  
* Visual Studio 2022 (hoặc bất kỳ IDE nào hỗ trợ .NET)  
* Giấy phép GroupDocs.Conversion hợp lệ (bản dùng thử miễn phí hoạt động cho việc thử nghiệm)  
* Một tài liệu Word mẫu (`input.docx`) mà bạn muốn đánh số  

Những yêu cầu này đảm bảo mã chạy mà không cần cấu hình bổ sung.

## Cách thiết lập tùy chọn đánh số Bates – tổng quan

Cốt lõi của **cách thiết lập tùy chọn đánh số Bates** nằm trong ba đối tượng:

1. `Document` – tải tệp nguồn.  
2. `BatesNumberingOptions` – chứa số bắt đầu, tiền tố và các chi tiết định dạng khác.  
3. `AddBatesNumbering` – phương thức chèn số vào mỗi trang.

Hiểu vì sao mỗi thành phần tồn tại sẽ giúp bạn điều chỉnh giải pháp cho các kịch bản phức tạp hơn, chẳng hạn như phông chữ tùy chỉnh hoặc đánh số đa ngôn ngữ.

## Bước 1: Cài đặt gói NuGet GroupDocs.Conversion

Mở terminal trong thư mục solution của bạn và chạy:

```bash
dotnet add package GroupDocs.Conversion
```

**GroupDocs API** cung cấp lớp `Document` và phương thức mở rộng `AddBatesNumbering` được sử dụng sau này trong tutorial.

## Bước 2: Tải tài liệu nguồn

```csharp
using GroupDocs.Conversion;
using GroupDocs.Conversion.Options.Convert;

// Step 2: Load the source Word document
Document document = new Document(@"C:\Docs\input.docx");
```

*Why this step?* → *Tại sao bước này?*  

Tải tệp tạo ra một biểu diễn trong bộ nhớ mà engine chuyển đổi có thể thao tác. Nếu không có một thể hiện `Document` bạn sẽ không thể áp dụng đánh số Bates hay bất kỳ chuyển đổi nào khác.

## Bước 3: Tạo tùy chọn đánh số Bates

```csharp
// Step 3: Configure Bates numbering
BatesNumberingOptions batesOptions = new BatesNumberingOptions
{
    // The first page will be numbered 1000
    StartNumber = 1000,
    // Each page will be prefixed with "CASE-"
    Prefix = "CASE-",
    // Optional: set the number format (e.g., 4 digits)
    NumberFormat = "#0000",
    // Optional: choose where the number appears (header/footer)
    Position = BatesNumberingPosition.FooterRight
};
```

*Why this step?* → *Tại sao bước này?*  

`BatesNumberingOptions` bao hàm tất cả các cài đặt bạn có thể cần khi **cài đặt tùy chọn đánh số Bates**. Điều chỉnh `StartNumber` và `Prefix` cho phép bạn đồng bộ đầu ra với hệ thống quản lý vụ việc. Thuộc tính `Position` kiểm soát vị trí hiển thị, thường là yêu cầu tuân thủ.

## Bước 4: Áp dụng đánh số Bates vào tài liệu

```csharp
// Step 4: Apply the numbering to every page
document.AddBatesNumbering(batesOptions);
```

Phương thức `AddBatesNumbering` duyệt qua từng trang của `Document` đã tải và chèn chuỗi đã cấu hình. Vì phương thức hoạt động trên biểu diễn trong bộ nhớ, bạn có thể xâu chuỗi các bước xử lý bổ sung (ví dụ: thêm watermark) trước khi lưu.

## Bước 5: Chuyển đổi và lưu kết quả dưới dạng PDF

```csharp
// Step 5: Define PDF conversion options (optional)
PdfConvertOptions pdfOptions = new PdfConvertOptions
{
    // Preserve original layout
    EmbedStandardFonts = true
};

// Save the numbered document as PDF
document.Save(@"C:\Docs\output.pdf", pdfOptions);
```

*Why this step?* → *Tại sao bước này?*  

Lưu dưới dạng PDF là định dạng cuối cùng phổ biến cho tài liệu pháp lý. Đối tượng `PdfConvertOptions` cho phép tinh chỉnh đầu ra, nhưng không bắt buộc đối với việc đánh số cơ bản. Lệnh `Save` ghi PDF đã được đánh số đầy đủ ra đĩa.

## Ví dụ hoàn chỉnh, có thể chạy được

Kết hợp mọi thứ lại, đây là một ứng dụng console tự chứa mà bạn có thể biên dịch và chạy:

```csharp
using System;
using GroupDocs.Conversion;
using GroupDocs.Conversion.Options.Convert;
using GroupDocs.Conversion.Options.Convert.Pdf;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Load the source Word document
            Document document = new Document(@"C:\Docs\input.docx");

            // Configure Bates numbering options
            BatesNumberingOptions batesOptions = new BatesNumberingOptions
            {
                StartNumber = 1000,
                Prefix = "CASE-",
                NumberFormat = "#0000",
                Position = BatesNumberingPosition.FooterRight
            };

            // Apply numbering to each page
            document.AddBatesNumbering(batesOptions);

            // Optional: set PDF conversion preferences
            PdfConvertOptions pdfOptions = new PdfConvertOptions
            {
                EmbedStandardFonts = true
            };

            // Save the numbered PDF
            document.Save(@"C:\Docs\output.pdf", pdfOptions);

            Console.WriteLine("Bates numbering applied successfully. Output saved to output.pdf");
        }
    }
}
```

**Kết quả mong đợi**

Chạy chương trình sẽ tạo `output.pdf` trong đó mỗi trang hiển thị một nhãn như `CASE-1000`, `CASE-1001`, v.v., được đặt ở chân trang phải. Mở PDF bằng bất kỳ trình xem nào để xác nhận các số xuất hiện như mong muốn.

## Các lỗi thường gặp và thực hành tốt nhất

| Vấn đề | Nguyên nhân | Cách tránh |
|--------|-------------|------------|
| **Relative paths cause `FileNotFoundException`** | Thư mục làm việc của ứng dụng console có thể khác với của Visual Studio. | Sử dụng đường dẫn tuyệt đối hoặc `Path.Combine(AppContext.BaseDirectory, "input.docx")`. |
| **Numbering overlaps existing footers** | Nếu tài liệu nguồn đã có nội dung trong khu vực chân trang được chọn, số mới có thể bị ẩn. | Chọn một `Position` khác (ví dụ: `HeaderLeft`) hoặc điều chỉnh mẫu nguồn. |
| **Large documents are slow** | Đánh số Bates lặp lại qua mỗi trang; việc sử dụng bộ nhớ tăng theo kích thước tệp. | Xử lý tài liệu theo từng khối bằng `Document.Split` nếu vượt quá 500 trang. |
| **License expiration** | Bản dùng thử của GroupDocs hết hạn sau 30 ngày, gây ra ngoại lệ khi gọi `AddBatesNumbering`. | Áp dụng khóa giấy phép hợp lệ trước khi tải tài liệu: `License license = new License(); license.SetLicense("license.lic");`. |

**Pro tip:** Nếu bạn cần định dạng số khác cho mỗi vụ việc (ví dụ: `2023-CASE-001`), hãy xây dựng tiền tố một cách động trước khi tạo `BatesNumberingOptions`.

## Mở rộng giải pháp

Cùng một cách tiếp cận **Bates numbering C#** cũng hoạt động với các định dạng nguồn khác như `.txt`, `.html` hoặc thậm chí hình ảnh. Chỉ cần thay đổi phần mở rộng tệp khi khởi tạo đối tượng `Document`, engine chuyển đổi sẽ tự xử lý phần còn lại.

Bạn cũng có thể kết hợp **document conversion C#** với OCR cho PDF đã quét:

```csharp
// Example: add OCR before numbering (requires GroupDocs.Viewer)
using GroupDocs.Viewer;
using GroupDocs.Viewer.Options;

Document scannedPdf = new Document(@"C:\Docs\scanned.pdf");
var viewer = new Viewer(scannedPdf);
var viewOptions = new HtmlViewOptions();
viewer.View(viewOptions); // OCR step
// Then apply Bates numbering as shown earlier
```

## Kết luận

Bây giờ bạn đã biết **cách thiết lập tùy chọn đánh số Bates** trong C# từ đầu đến cuối. Bằng cách tạo một đối tượng `BatesNumberingOptions`, áp dụng nó với `AddBatesNumbering`, và lưu kết quả dưới dạng PDF, bạn có thể tự động hoá việc tạo ra các tài liệu tuân thủ pháp lý, được định danh duy nhất.  

Từ đây bạn có thể khám phá các chủ đề liên quan như **C# PDF generation**, **document conversion C#**, hoặc các tính năng nâng cao của **GroupDocs API** như watermarking và chữ ký số. Thử nghiệm với các tiền tố, vị trí và định dạng số khác nhau để phù hợp với quy trình làm việc của bạn.

Happy coding!

## Bạn nên học gì tiếp theo?

Các tutorial sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật đã được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh với giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Thêm đánh số Bates PDF trong C# – Hướng dẫn đầy đủ](/pdf/english/net/programming-with-stamps-and-watermarks/add-bates-numbering-pdf-in-c-complete-guide/)
- [Cách thêm và tùy chỉnh số trang trong PDF bằng Aspose.PDF cho .NET | Hướng dẫn thao tác tài liệu](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [Cách thêm chú thích văn bản vào chân trang trong PDF bằng Aspose.PDF cho .NET&#58; Hướng dẫn từng bước](/pdf/english/net/document-manipulation/add-text-stamp-footer-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}