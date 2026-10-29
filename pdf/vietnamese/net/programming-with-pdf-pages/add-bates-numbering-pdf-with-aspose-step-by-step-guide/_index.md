---
category: general
date: 2026-08-08
description: Thêm đánh số Bates vào PDF bằng Aspose.Pdf trong C#. Hướng dẫn này cũng
  chỉ cách thêm trang trắng vào PDF và tạo PDF một cách lập trình.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add bates numbering pdf
- add blank page pdf
- generate pdf programmatically
- create pdf aspose
language: vi
lastmod: 2026-08-08
og_description: Thêm đánh số Bates vào PDF với Aspose.Pdf trong C#. Tìm hiểu cách
  thêm trang trắng vào PDF, tạo PDF bằng lập trình và lưu tài liệu cuối cùng chỉ trong
  vài phút.
og_image_alt: Screenshot of C# code adding Bates numbering and a blank page to a PDF
  using Aspose.Pdf
og_title: Thêm đánh số Bates vào PDF với Aspose – hướng dẫn C# đầy đủ
schemas:
- author: Aspose
  dateModified: '2026-08-08'
  description: Add bates numbering pdf using Aspose.Pdf in C#. This tutorial also
    shows how to add blank page pdf and generate pdf programmatically.
  headline: Add bates numbering pdf with Aspose – step‑by‑step guide
  type: TechArticle
- description: Add bates numbering pdf using Aspose.Pdf in C#. This tutorial also
    shows how to add blank page pdf and generate pdf programmatically.
  name: Add bates numbering pdf with Aspose – step‑by‑step guide
  steps:
  - name: What if I need a different font or position?
    text: 'The `BatesNumberingArtifact` exposes properties such as `FontSize`, `FontColor`,
      `HorizontalAlignment`, and `VerticalAlignment`. For example:'
  - name: How do I exclude a specific page from numbering?
    text: Create a separate `BatesNumberingArtifact` for the pages you want to number
      and add it only to those pages. Pages without an attached artifact will remain
      unnumbered.
  - name: Does this work with existing PDFs?
    text: 'Yes. Instead of `new Document()`, load an existing file:'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF generation
- Bates numbering
title: Thêm đánh số Bates vào PDF với Aspose – hướng dẫn từng bước
url: /vi/net/programming-with-pdf-pages/add-bates-numbering-pdf-with-aspose-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Thêm đánh số Bates vào PDF với Aspose – hướng dẫn từng bước

Thêm đánh số Bates vào PDF với Aspose.Pdf rất đơn giản một khi bạn nắm rõ các bước cốt lõi. Nếu bạn cũng cần thêm trang trắng vào PDF hoặc tạo PDF một cách lập trình, hướng dẫn này sẽ bao gồm mọi thứ bạn cần.

Trong tutorial này bạn sẽ:

* Tạo một tài liệu PDF mới từ đầu.  
* Thêm một trang trắng PDF sẽ chứa các số Bates.  
* Cấu hình đối tượng Bates numbering với tiền tố tùy chỉnh.  
* Lưu PDF để các số xuất hiện trên tệp đã tạo.  

Khi hoàn thành, bạn sẽ có một ứng dụng console C# hoạt động đầy đủ, tạo ra một PDF chứa các số Bates như **CASE‑1000**, **CASE‑1001**, … – một yêu cầu phổ biến trong quy trình pháp lý và e‑discovery.

## Yêu cầu trước

* .NET 6.0 SDK hoặc mới hơn (mã cũng chạy được với .NET Framework 4.8).  
* Visual Studio 2022 hoặc bất kỳ IDE nào hỗ trợ C#.  
* Giấy phép Aspose.Pdf for .NET hợp lệ (hoặc khóa dùng thử miễn phí).  
* Kiến thức cơ bản về cú pháp C#.

> **Mẹo chuyên nghiệp:** Nếu chạy mã mà không có giấy phép, Aspose sẽ thêm một watermark nhỏ vào PDF đầu ra.

## Bước 1: Thiết lập dự án và nhập Aspose.Pdf

Tạo một dự án console mới và thêm gói NuGet Aspose.Pdf:

```bash
dotnet new console -n BatesNumberingDemo
cd BatesNumberingDemo
dotnet add package Aspose.Pdf
```

Các chỉ thị `using` cần thiết cho ví dụ là:

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Artifacts;
```

Các namespace này cung cấp cho bạn quyền truy cập vào các lớp `Document`, `Page` và `BatesNumberingArtifact` sẽ được dùng sau.

## Bước 2: Thêm một trang trắng PDF

Một số Bates phải được gắn vào một trang, vì vậy trước tiên chúng ta tạo một trang trắng sẽ nhận đối tượng đánh số.

```csharp
// Step 2: Add a blank page pdf
Document pdfDocument = new Document();          // creates an empty PDF
Page pdfPage = pdfDocument.Pages.Add();         // adds the first (blank) page
```

Lớp `Document` đại diện cho toàn bộ tệp PDF, trong khi `Pages.Add()` chèn một trang mới, trống vào cuối bộ sưu tập trang của tài liệu. Vì tài liệu bắt đầu rỗng, lời gọi này cũng tạo ra trang đầu tiên.

## Bước 3: Cấu hình đối tượng Bates numbering

Bây giờ chúng ta định nghĩa cách các số Bates sẽ hiển thị. `BatesNumberingArtifact` cho phép bạn đặt số bắt đầu, tiền tố, hậu tố và các tùy chọn định dạng.

```csharp
// Step 3: Define Bates numbering settings
BatesNumberingArtifact batesArtifact = new BatesNumberingArtifact(pdfPage)
{
    StartNumber = 1000,          // first number in the sequence
    Prefix = "CASE-",            // custom prefix before each number
    // Optional: you can also set Suffix, FontSize, FontColor, etc.
};
```

**Tại sao điều này quan trọng:**  
Đặt `StartNumber` thành **1000** phù hợp với các quy ước thường gặp trong hồ sơ vụ án pháp lý. `Prefix` đảm bảo mỗi số xuất hiện dưới dạng **CASE‑1000**, **CASE‑1001**, … giúp việc tìm kiếm và sắp xếp dễ dàng hơn.

## Bước 4: Gắn đối tượng vào trang

Đối tượng phải được thêm vào bộ sưu tập `Artifacts` của trang để Aspose render nó trên mọi trang khi lưu.

```csharp
// Step 4: Attach the Bates numbering artifact to the PDF page
pdfPage.Artifacts.Add(batesArtifact);
```

Khi tài liệu được lưu, Aspose tự động lặp lại đối tượng trên tất cả các trang, tăng số cho mỗi trang tiếp theo.

## Bước 5: (Tùy chọn) Thêm các trang bổ sung

Nếu cần thêm trang, chỉ cần lặp lại `pdfDocument.Pages.Add()`. Đối tượng Bates numbering bạn đã gắn ở bước trước sẽ tự động xuất hiện trên mỗi trang mới.

```csharp
// Example: add two more pages
pdfDocument.Pages.Add();
pdfDocument.Pages.Add();
```

## Bước 6: Lưu PDF – tạo PDF một cách lập trình

Cuối cùng, ghi tài liệu ra đĩa. Đây là thời điểm các số Bates được render lên các trang.

```csharp
// Step 6: Save the PDF – generate pdf programmatically
string outputPath = Path.Combine(
    Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
    "BatesNumberedDocument.pdf");

// Ensure the directory exists
Directory.CreateDirectory(Path.GetDirectoryName(outputPath)!);

pdfDocument.Save(outputPath);
Console.WriteLine($"PDF saved to: {outputPath}");
```

**Kết quả mong đợi:**  
Mở *BatesNumberedDocument.pdf* và bạn sẽ thấy một PDF ba trang. Mỗi trang hiển thị một số Bates ở góc dưới‑phải:

* Trang 1 → **CASE‑1000**  
* Trang 2 → **CASE‑1001**  
* Trang 3 → **CASE‑1002**

Các số được tự động tăng vì đối tượng đã được gắn vào bộ sưu tập trang.

## Ví dụ đầy đủ, có thể chạy được

Kết hợp tất cả lại, đây là một chương trình console hoàn chỉnh mà bạn có thể sao chép, dán và chạy:

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Artifacts;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main()
        {
            // Create a new PDF document
            Document pdfDocument = new Document();

            // Add a blank page pdf
            Page pdfPage = pdfDocument.Pages.Add();

            // Define Bates numbering settings (add bates numbering pdf)
            BatesNumberingArtifact batesArtifact = new BatesNumberingArtifact(pdfPage)
            {
                StartNumber = 1000,
                Prefix = "CASE-"
            };

            // Attach the artifact to the page
            pdfPage.Artifacts.Add(batesArtifact);

            // (Optional) add more pages to see incremented numbers
            pdfDocument.Pages.Add(); // page 2
            pdfDocument.Pages.Add(); // page 3

            // Save the PDF – generate pdf programmatically
            string outputPath = Path.Combine(
                Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
                "BatesNumberedDocument.pdf");

            Directory.CreateDirectory(Path.GetDirectoryName(outputPath)!);
            pdfDocument.Save(outputPath);

            Console.WriteLine($"PDF saved to: {outputPath}");
        }
    }
}
```

Chạy chương trình bằng `dotnet run`. Sau khi thực thi, tìm tệp trên desktop và kiểm tra các số Bates.

![Add bates numbering pdf example](/images/bates-numbering.png "Add bates numbering pdf example")

## Các câu hỏi thường gặp và trường hợp đặc biệt

### Nếu tôi cần phông chữ hoặc vị trí khác thì sao?

`BatesNumberingArtifact` cung cấp các thuộc tính như `FontSize`, `FontColor`, `HorizontalAlignment` và `VerticalAlignment`. Ví dụ:

```csharp
batesArtifact.FontSize = 12;
batesArtifact.FontColor = Color.Blue;
batesArtifact.HorizontalAlignment = HorizontalAlignment.Left;
batesArtifact.VerticalAlignment = VerticalAlignment.Top;
```

### Làm thế nào để loại trừ một trang cụ thể khỏi việc đánh số?

Tạo một `BatesNumberingArtifact` riêng cho các trang bạn muốn đánh số và chỉ thêm nó vào những trang đó. Các trang không có đối tượng gắn sẽ không được đánh số.

### Điều này có hoạt động với các PDF đã tồn tại không?

Có. Thay vì `new Document()`, tải một tệp hiện có:

```csharp
Document pdfDocument = new Document("input.pdf");
```

Sau đó gắn đối tượng vào các trang mong muốn và lưu lại.

## Kết luận

Bây giờ bạn đã biết cách **add bates numbering pdf** bằng Aspose.Pdf, cách **add blank page pdf**, và cách **generate pdf programmatically** trong một giải pháp C# sạch sẽ, có thể tái sử dụng. Phương pháp này hoạt động với bất kỳ số lượng trang nào, tiền tố tùy chỉnh và tùy chọn định dạng, cho phép bạn kiểm soát hoàn toàn tài liệu cuối cùng.

Các bước tiếp theo bạn có thể khám phá:

* Use **create pdf as

## Bạn nên học gì tiếp theo?

Các tutorial sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm mã mẫu đầy đủ với các giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [How to Add and Customize Page Numbers in PDFs Using Aspose.PDF for .NET | Document Manipulation Guide](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [How to Add an Empty Page at the End of a PDF Using Aspose.PDF for .NET | Step-by-Step Guide](/pdf/english/net/document-manipulation/add-empty-page-end-pdf-aspose-pdf-net/)
- [Create PDF Document with Aspose.PDF – Add Page, Shape & Save](/pdf/english/net/document-creation/create-pdf-document-with-aspose-pdf-add-page-shape-save/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}