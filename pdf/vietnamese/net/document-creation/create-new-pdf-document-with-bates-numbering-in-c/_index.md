---
category: general
date: 2026-08-04
description: Tạo tài liệu PDF mới bằng C# và nhanh chóng thêm số Bates vào PDF bằng
  Aspose.Pdf – học cách thêm trang trắng vào PDF và đánh số trang tùy chỉnh.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create new pdf document
- add bates numbering pdf
- how to add bates
- add blank page pdf
- add custom page numbers
language: vi
lastmod: 2026-08-04
og_description: Tạo tài liệu PDF mới bằng C# và tự động thêm số Bates vào PDF cho
  quản lý vụ án pháp lý – kèm ví dụ mã đầy đủ.
og_image_alt: Screenshot of a C# program creating a PDF document with Bates numbers
  applied
og_title: Tạo tài liệu PDF mới với đánh số Bates trong C#
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Create new PDF document in C# and add Bates numbering pdf quickly using
    Aspose.Pdf – learn to add blank page pdf and custom page numbers.
  headline: Create new PDF document with Bates numbering in C#
  type: TechArticle
tags:
- C#
- PDF
- Aspose.Pdf
- Bates numbering
title: Tạo tài liệu PDF mới với đánh số Bates trong C#
url: /vi/net/document-creation/create-new-pdf-document-with-bates-numbering-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo tài liệu PDF mới với đánh số Bates trong C#

Nếu bạn cần **tạo tài liệu PDF mới** trong C#, hướng dẫn này sẽ chỉ cho bạn cách **thêm đánh số Bates vào PDF** bằng Aspose.Pdf. Bạn sẽ học cách **thêm trang trống vào PDF**, cấu hình **thêm số trang tùy chỉnh**, và lưu tệp cuối cùng.

Bài hướng dẫn bao gồm mọi bước từ cài đặt thư viện đến tạo PDF đáp ứng các tiêu chuẩn hồ sơ vụ án pháp lý. Khi hoàn thành, bạn có thể tạo PDF, chèn trang trống, áp dụng số Bates, và tùy chỉnh định dạng đánh số — tất cả bằng một chương trình có thể chạy được.

## Yêu cầu trước

Trước khi bắt đầu, hãy chắc chắn rằng bạn có:

* .NET 6.0 SDK hoặc phiên bản mới hơn đã được cài đặt  
* Visual Studio 2022 (hoặc bất kỳ IDE C# nào)  
* Giấy phép Aspose.Pdf for .NET đang hoạt động hoặc khóa dùng thử miễn phí  

Bạn không cần bất kỳ gói NuGet bổ sung nào; bài hướng dẫn sẽ tự động cài đặt mọi thứ.

## Bước 1: Cài đặt Aspose.Pdf qua NuGet

Mở terminal trong thư mục dự án của bạn và chạy:

```bash
dotnet add package Aspose.Pdf
```

Lệnh này sẽ thêm phiên bản ổn định mới nhất của Aspose.Pdf vào dự án của bạn, cung cấp các lớp `Document`, `BatesNumbering` và các lớp thao tác PDF khác mà bạn sẽ sử dụng.

## Bước 2: Tạo tài liệu PDF mới – thiết lập ban đầu

Tạo tệp PDF là nền tảng cho mọi thao tác sau này. Lớp `Document` đại diện cho toàn bộ container PDF.

```csharp
using Aspose.Pdf;

// Step 2: Create a new PDF document
using var doc = new Document();
```

*​Tại sao điều này quan trọng*: Khởi tạo `Document` cấp phát các cấu trúc nội bộ cần thiết cho các trang, phông chữ và đồ họa. Sử dụng `using var` đảm bảo tệp được giải phóng đúng cách sau khi lưu.

## Bước 3: Thêm trang trống vào PDF

PDF phải có ít nhất một trang trước khi bạn có thể đặt nội dung lên đó. Thêm một trang trống cung cấp một canvas sạch cho số Bates.

```csharp
// Step 3: Add a blank page to the document
Page page = doc.Pages.Add();
```

Phương thức `Pages.Add()` thêm một trang mới, trống vào cuối bộ sưu tập trang của tài liệu. Bạn có thể lặp lại lệnh này để thêm nhiều trang hơn nếu sau này cần **thêm số trang tùy chỉnh** trên nhiều trang.

## Bước 4: Cấu hình đánh số Bates – cách thêm Bates

Đánh số Bates là một định danh tuần tự thường được sử dụng trong tài liệu pháp lý. Bạn cấu hình nó qua lớp `BatesNumbering`.

```csharp
// Step 4: Set up Bates numbering options
var bates = new BatesNumbering
{
    StartNumber = 1000,      // Starting number for the sequence
    Prefix = "CaseA-",       // Text to prepend to each number
    Increment = 1,           // Increment between consecutive numbers
    // Optional: Set the location, font size, etc.
};
```

*​Tại sao điều này quan trọng*: `StartNumber` xác định số đầu tiên, `Prefix` thêm nhãn dễ đọc, và `Increment` điều chỉnh kích thước bước. Bạn cũng có thể điều chỉnh `HorizontalAlignment`, `VerticalAlignment`, `FontSize`, và `Margins` để kiểm soát cách hiển thị số trên mỗi trang.

## Bước 5: Áp dụng đánh số Bates vào trang

Bây giờ các tùy chọn đánh số đã sẵn sàng, hãy áp dụng chúng vào trang (hoặc toàn bộ tài liệu).

```csharp
// Step 5: Apply the Bates numbering to the page
bates.Apply(page);
```

Gọi `Apply` sẽ chèn số đã định dạng vào chân trang của trang theo mặc định. Nếu bạn cần số ở vị trí khác, hãy đặt `bates.Position` trước khi gọi `Apply`.

## Bước 6: Lưu PDF với số Bates đã áp dụng

Cuối cùng, ghi tài liệu trong bộ nhớ ra đĩa.

```csharp
// Step 6: Save the PDF with Bates numbers applied
string outputPath = Path.Combine(
    Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
    "BatesNumbered.pdf");

doc.Save(outputPath);
Console.WriteLine($"PDF saved to {outputPath}");
```

Tệp đã lưu bây giờ chứa một trang duy nhất với số Bates **CaseA-1000** hiển thị ở dưới cùng. Mở PDF bằng bất kỳ trình xem nào để xác nhận việc đánh số.

## Kết quả mong đợi

Khi bạn mở `BatesNumbered.pdf`, bạn sẽ thấy:

* Một trang trống (hoặc nhiều hơn nếu bạn đã thêm các trang bổ sung)  
* Văn bản **CaseA-1000** được đặt ở dưới cùng của trang (vị trí mặc định)  

Nếu bạn thêm nhiều trang và tái sử dụng cùng một thể hiện `BatesNumbering`, các số sẽ tự động tăng (CaseA-1001, CaseA-1002, …).

## Mẹo chuyên nghiệp: Thêm số trang tùy chỉnh bên cạnh số Bates

Đôi khi bạn cần cả số Bates và số trang truyền thống. Bạn có thể kết hợp chúng bằng cách thêm một `TextFragment` sau khi áp dụng đánh số Bates:

```csharp
// Add a traditional page number in the header
var pageNumber = new TextFragment($"Page {page.Number}")
{
    HorizontalAlignment = HorizontalAlignment.Center,
    VerticalAlignment = VerticalAlignment.Top,
    FontSize = 12,
    Font = FontRepository.FindFont("Arial")
};
page.Paragraphs.Add(pageNumber);
```

Đoạn mã này minh họa **thêm số trang tùy chỉnh** đồng thời giữ lại nhãn Bates.

## Trường hợp đặc biệt: Áp dụng đánh số Bates cho nhiều trang

Nếu tài liệu của bạn có nhiều trang, bạn có thể áp dụng cùng một thể hiện `BatesNumbering` cho mỗi trang trong một vòng lặp:

```csharp
for (int i = 1; i <= doc.Pages.Count; i++)
{
    bates.Apply(doc.Pages[i]);
}
```

Vòng lặp đảm bảo mỗi trang nhận được một số tuần tự dựa trên `StartNumber` và `Increment` mà bạn đã định nghĩa.

## Những lỗi thường gặp và cách tránh

| Vấn đề | Nguyên nhân | Cách khắc phục |
|-------|-------------|----------------|
| Số xuất hiện lệch trung tâm | Căn chỉnh mặc định có thể không phù hợp với bố cục của bạn | Đặt `bates.HorizontalAlignment` và `bates.VerticalAlignment` một cách rõ ràng |
| Số chồng lên nội dung hiện có | Không có lề được định nghĩa | Điều chỉnh `bates.Margin` hoặc sử dụng `bates.Position` để di chuyển số |
| Lỗi giấy phép tại thời gian chạy | Phiên bản dùng thử giới hạn đầu ra | Áp dụng giấy phép Aspose.Pdf hợp lệ trước khi tạo tài liệu (`License license = new License(); license.SetLicense("Aspose.Pdf.lic");`) |

## Ví dụ hoàn chỉnh hoạt động

Dưới đây là một chương trình tự chứa mà bạn có thể sao chép, dán và chạy.

```csharp
using System;
using System.IO;
using Aspose.Pdf;

class Program
{
    static void Main()
    {
        // 1. Create a new PDF document
        using var doc = new Document();

        // 2. Add a blank page pdf
        Page page = doc.Pages.Add();

        // 3. Configure Bates numbering – how to add bates
        var bates = new BatesNumbering
        {
            StartNumber = 1000,
            Prefix = "CaseA-",
            Increment = 1,
            HorizontalAlignment = HorizontalAlignment.Right,
            VerticalAlignment = VerticalAlignment.Bottom,
            Margin = new MarginInfo(20, 20, 20, 20),
            FontSize =


## Bạn nên học gì tiếp theo?

Các hướng dẫn sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng dựa trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh với giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Cách Thêm và Tùy Chỉnh Số Trang trong PDF bằng Aspose.PDF cho .NET \| Hướng Dẫn Thao Tác Tài Liệu](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [Aspose.PDF .NET: Thêm Số Trang vào PDF bằng FloatingBox](/pdf/english/net/text-operations/aspose-pdf-net-floatingbox-page-numbering/)
- [Tạo Tài liệu PDF với Aspose.PDF – Thêm Trang, Hình Dạng & Lưu](/pdf/english/net/document-creation/create-pdf-document-with-aspose-pdf-add-page-shape-save/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}