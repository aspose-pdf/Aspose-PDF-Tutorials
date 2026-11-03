---
category: general
date: 2026-09-27
description: Thêm đánh số Bates vào PDF bằng Aspose.PDF trong C#. Tìm hiểu cách tải
  tài liệu PDF, thiết lập các tùy chọn đánh số Bates và lưu tệp đã cập nhật.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add bates numbering
- load pdf document
- how to add bates numbering
- Aspose.PDF C#
- PDF Bates numbering example
language: vi
lastmod: 2026-09-27
og_description: Thêm đánh số Bates vào PDF bằng Aspose.PDF trong C#. Hướng dẫn này
  cho bạn biết cách tải tài liệu PDF, cấu hình đánh số Bates và lưu kết quả.
og_image_alt: Screenshot of a PDF page displaying Bates numbers in the footer
og_title: Thêm đánh số Bates vào PDF với Aspose.PDF – Hướng dẫn C#
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Add bates numbering to PDF using Aspose.PDF in C#. Learn how to load
    a PDF document, set Bates numbering options, and save the updated file.
  headline: Add bates numbering to PDF using Aspose.PDF in C#
  type: TechArticle
tags:
- Aspose.PDF
- C#
- PDF processing
title: Thêm đánh số Bates vào PDF bằng Aspose.PDF trong C#
url: /vi/net/programming-with-text/add-bates-numbering-to-pdf-using-aspose-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Thêm đánh số Bates vào PDF bằng Aspose.PDF trong C#

Nếu bạn cần **thêm đánh số Bates** vào một tệp PDF, hướng dẫn này sẽ cho bạn một giải pháp hoàn chỉnh, sẵn sàng chạy. Bạn sẽ thấy cách **tải tài liệu PDF**, cấu hình các tùy chọn đánh số Bates, và ghi tệp đã đánh số trở lại đĩa — tất cả đều sử dụng Aspose.PDF cho .NET.

Việc áp dụng số Bates thường gặp trong các quy trình pháp lý, thực thi pháp luật và lưu trữ. Khi kết thúc tutorial này, bạn có thể nhúng một định danh tuần tự trên mỗi trang, tùy chỉnh tiền tố, và bắt đầu đếm từ bất kỳ số nào bạn muốn.

## Những gì bạn sẽ học

* Cách **tải nội dung tài liệu PDF** vào đối tượng `Aspose.Pdf.Document`.  
* Các bước chi tiết **cách thêm đánh số Bates** bằng `BatesNumberingOptions`.  
* Cách lưu tệp đã chỉnh sửa mà vẫn giữ nguyên bố cục và chất lượng gốc.  

Không cần công cụ bên ngoài — chỉ cần gói NuGet Aspose.PDF và môi trường phát triển .NET (Visual Studio, VS Code, hoặc Rider).  

---

## Bước 1: Cài đặt Aspose.PDF cho .NET

Mở thư mục dự án của bạn trong terminal và chạy:

```bash
dotnet add package Aspose.PDF
```

Gói này bao gồm namespace `Aspose.Pdf`, cung cấp tất cả các lớp được sử dụng trong tutorial này. Sau khi cài đặt, tải lại dự án để IDE nhận diện tham chiếu mới.

## Bước 2: Tải tài liệu PDF

Việc tải tệp nguồn là thao tác đầu tiên vì engine đánh số Bates hoạt động trên một đối tượng `Document` đã tồn tại.

```csharp
using Aspose.Pdf;

// ...

// Replace with the path to your input PDF
string inputPath = @"YOUR_DIRECTORY\input.pdf";

// Load the PDF document into memory
Document doc = new Document(inputPath);
```

**Tại sao điều này quan trọng:** Lớp `Document` phân tích cấu trúc PDF, cho phép bạn truy cập các trang, chú thích và siêu dữ liệu. Nếu không tải tệp trước, bạn không thể áp dụng bất kỳ số thứ tự nào.

## Bước 3: Cấu hình tùy chọn đánh số Bates

Tạo một đối tượng `BatesNumberingOptions` và đặt tiền tố, số bắt đầu, và các tham số định dạng tùy chọn.

```csharp
using Aspose.Pdf;

// ...

BatesNumberingOptions batesOptions = new BatesNumberingOptions
{
    // Text that appears before the numeric part
    Prefix = "CASE01",

    // First number to use (1 means the first page gets CASE01-1)
    StartNumber = 1,

    // Optional: customize the appearance
    // The default places the number in the footer, centered.
    // You can change Font, FontSize, Color, and Position if needed.
    // Example:
    // Font = FontRepository.FindFont("Arial"),
    // FontSize = 10,
    // Color = Color.Black,
    // Margin = new Margin(0, 0, 0, 20)
};
```

**Tại sao điều này quan trọng:** `BatesNumberingOptions` chỉ cho Aspose.PDF cách tạo nhãn cho mỗi trang. Thuộc tính `Prefix` giúp bạn nhóm các vụ việc liên quan, trong khi `StartNumber` cho phép tiếp tục một chuỗi từ lô trước.

## Bước 4: Lưu PDF với số Bates đã áp dụng

Truyền đối tượng tùy chọn vào phương thức `Save`. Aspose.PDF sẽ ghi số trực tiếp lên mỗi trang.

```csharp
// Replace with the desired output path
string outputPath = @"YOUR_DIRECTORY\output.pdf";

// Save the document, applying the Bates numbering
doc.Save(outputPath, batesOptions);
```

**Tại sao điều này quan trọng:** Phương thức overload `Save(string, BatesNumberingOptions)` kết hợp bước render với quá trình đánh số, đảm bảo tệp đầu ra chứa các định danh hiển thị.

## Ví dụ đầy đủ – tất cả trong một

Dưới đây là một chương trình tự chứa bạn có thể sao chép, dán và chạy. Nó minh họa **cách thêm đánh số Bates** từ đầu đến cuối.

```csharp
using System;
using Aspose.Pdf;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the PDF document
            string inputPath = @"YOUR_DIRECTORY\input.pdf";
            Document doc = new Document(inputPath);

            // 2️⃣ Set up Bates numbering options
            BatesNumberingOptions batesOptions = new BatesNumberingOptions
            {
                Prefix = "CASE01",
                StartNumber = 1,
                // Optional appearance tweaks:
                // Font = FontRepository.FindFont("Times New Roman"),
                // FontSize = 9,
                // Color = Color.DarkBlue,
                // Margin = new Margin(0, 0, 0, 15)
            };

            // 3️⃣ Save the document with Bates numbers
            string outputPath = @"YOUR_DIRECTORY\output.pdf";
            doc.Save(outputPath, batesOptions);

            Console.WriteLine($"Bates numbering added. Output saved to: {outputPath}");
        }
    }
}
```

### Kết quả mong đợi

Chạy chương trình sẽ tạo ra `output.pdf` trong đó mỗi trang hiển thị một nhãn tương tự:

```
CASE01-1
CASE01-2
CASE01-3
...
```

Các số xuất hiện ở chân trang theo mặc định, nhưng bạn có thể di chuyển chúng bằng cách điều chỉnh thuộc tính `Margin` trong `BatesNumberingOptions`.

## Các trường hợp đặc biệt và biến thể phổ biến

| Tình huống | Cần điều chỉnh |
|-----------|----------------|
| **Tiền tố khác nhau cho mỗi lô** | Thay đổi `Prefix` trước khi gọi `Save`. Bạn có thể lặp qua nhiều tài liệu với các tiền tố riêng biệt. |
| **Tiếp tục đánh số từ tệp trước** | Đặt `StartNumber` thành số cuối cùng đã dùng + 1. |
| **Đặt số ở đầu trang** | Sử dụng `batesOptions.Margin = new Margin(20, 0, 0, 0);` (lề trên) hoặc tùy chỉnh `batesOptions.Position`. |
| **Phông chữ hoặc màu sắc tùy chỉnh** | Gán các thuộc tính `Font`, `FontSize`, và `Color` như trong phần chú thích. |
| **PDF lớn (hơn 1000 trang)** | Thao tác này tiết kiệm bộ nhớ; tuy nhiên, bạn có thể gọi `doc.OptimizeResources()` trước khi lưu để giảm kích thước tệp. |

**Mẹo chuyên nghiệp:** Nếu quy trình của bạn yêu cầu các sơ đồ đánh số khác nhau cho mỗi tài liệu, hãy đóng gói logic vào một phương thức trợ giúp:

```csharp
static void ApplyBatesNumbering(string src, string dst, string prefix, int start)
{
    var doc = new Document(src);
    var opts = new BatesNumberingOptions { Prefix = prefix, StartNumber = start };
    doc.Save(dst, opts);
}
```

## Kết luận

Bây giờ bạn đã biết **cách thêm đánh số Bates** vào bất kỳ PDF nào bằng Aspose.PDF trong C#. Tutorial đã bao phủ việc tải tài liệu PDF, cấu hình các tùy chọn đánh số, và lưu tệp cuối cùng — tất cả trong một chương trình có thể thực thi.

Từ đây, bạn có thể khám phá các chủ đề liên quan như **thêm watermark**, **gộp nhiều PDF**, hoặc **trích xuất văn bản** với Aspose.PDF. Thử nghiệm với các phông chữ, màu sắc và vị trí khác nhau để phù hợp với tiêu chuẩn định dạng của tổ chức bạn.

Sẵn sàng tự động hoá quy trình tài liệu pháp lý? Thêm mã vào pipeline xây dựng, chạy nó trên các lô tệp, và để Aspose.PDF lo phần còn lại. Chúc bạn lập trình vui vẻ!


## Bạn nên học gì tiếp theo?


Các tutorial sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật đã được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm mã mẫu đầy đủ với các giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Create PDF Document C# – Add Bates Numbering](/pdf/english/net/programming-with-pdf-pages/create-pdf-document-c-add-bates-numbering/)
- [Add Bates Numbering PDF – Step‑by‑Step Guide to Number PDF Pages](/pdf/english/net/programming-with-pdf-pages/add-bates-numbering-pdf-step-by-step-guide-to-number-pdf-pag/)
- [Aspose PDF Tutorial – Insert a Blank Page and Update Bates Numbering](/pdf/english/net/programming-with-pdf-pages/aspose-pdf-tutorial-insert-a-blank-page-and-update-bates-num/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}