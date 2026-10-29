---
category: general
date: 2026-09-15
description: Cách thay đổi độ trong suốt trong PDF bằng Aspose.Pdf cho .NET và tìm
  hiểu cách thêm tính trong suốt khi lưu các tệp PDF đã chỉnh sửa.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to change opacity
- how to add transparency
- save modified pdf
language: vi
lastmod: 2026-09-15
og_description: Cách thay đổi độ trong suốt trong PDF bằng Aspose.Pdf cho .NET, bao
  gồm cách thêm hiệu ứng trong suốt và lưu các tệp PDF đã chỉnh sửa trong vài phút.
og_image_alt: Screenshot showing a PDF page before and after opacity changes
og_title: Cách thay đổi độ trong suốt trong PDF bằng Aspose.Pdf – hướng dẫn từng bước
schemas:
- author: Aspose
  dateModified: '2026-09-15'
  description: How to change opacity in a PDF using Aspose.Pdf for .NET and learn
    how to add transparency while you save modified PDF files.
  headline: How to change opacity in a PDF with Aspose.Pdf for .NET
  type: TechArticle
tags:
- Aspose.Pdf
- .NET
- PDF manipulation
title: Cách thay đổi độ trong suốt trong PDF bằng Aspose.Pdf cho .NET
url: /vi/net/images-graphics/how-to-change-opacity-in-a-pdf-with-aspose-pdf-for-net/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách thay đổi độ trong suốt trong PDF bằng Aspose.Pdf cho .NET

Nếu bạn cần **cách thay đổi độ trong suốt** của các đối tượng trong PDF, hướng dẫn này sẽ cho bạn các bước chính xác bằng cách sử dụng Aspose.Pdf cho .NET. Bạn cũng sẽ thấy **cách thêm độ trong suốt** vào trạng thái đồ họa và học cách **lưu PDF đã chỉnh sửa** mà không mất chất lượng.

Thay đổi độ trong suốt là một yêu cầu phổ biến khi bạn muốn chồng lên watermark, tạo nền mờ, hoặc xây dựng các hiệu ứng giống UI trong tài liệu. Mẫu mã dưới đây hoạt động với bất kỳ PDF nào mà Aspose.Pdf có thể mở, và hướng dẫn sẽ đưa bạn qua từng dòng để bạn hiểu *tại sao* nó quan trọng.

## Những gì bạn sẽ học

- Tải tài liệu PDF bằng Aspose.Pdf.
- Chỉnh sửa từ điển tài nguyên của trang để tạo một trạng thái đồ họa mới.
- Xác định độ trong suốt nét vẽ (`CA`), độ trong suốt tô (`ca`), và chế độ hòa trộn (`BM`).
- Chèn trạng thái đồ họa vào từ điển `ExtGState`.
- **Lưu PDF đã chỉnh sửa** mà giữ nguyên các thiết lập độ trong suốt mới.
- Xử lý các trường hợp đặc biệt như thiếu mục `ExtGState` hoặc tài liệu đa trang.

### Yêu cầu trước

| Yêu cầu | Lý do |
|-------------|--------|
| .NET 6.0 hoặc mới hơn | Cung cấp môi trường chạy cho mã C#. |
| Aspose.Pdf cho .NET (gói NuGet `Aspose.Pdf`) | Cung cấp API thao tác PDF được sử dụng trong ví dụ. |
| Kiến thức cơ bản về C# | Cần thiết để hiểu cú pháp và cấu trúc dự án. |
| Một PDF đầu vào (`input.pdf`) | Tệp mà bạn sẽ chỉnh sửa. |

> **Mẹo chuyên nghiệp:** Cài đặt gói bằng `dotnet add package Aspose.Pdf` trước khi bắt đầu.

## Bước 1: Tải tài liệu PDF

Hoạt động đầu tiên là mở tệp nguồn. Sử dụng khối `using` đảm bảo tài liệu được giải phóng đúng cách, tránh khóa tệp trên Windows.

```csharp
// Step 1: Load the PDF document
string pdfPath = @"YOUR_DIRECTORY\input.pdf";

using var pdfDocument = new Aspose.Pdf.Document(pdfPath);
```

> **Tại sao điều này quan trọng:** Mở tài liệu tạo ra một biểu diễn trong bộ nhớ mà bạn có thể chỉnh sửa. Lệnh `using` đảm bảo các tài nguyên được giải phóng, điều này rất cần thiết khi bạn sau này **lưu PDF đã chỉnh sửa** vào cùng một thư mục.

## Bước 2: Lấy trang đầu tiên và từ điển tài nguyên của nó

Các thiết lập độ trong suốt nằm trong từ điển tài nguyên của trang. Chúng tôi tập trung vào trang đầu tiên để đơn giản, nhưng logic này áp dụng cho bất kỳ chỉ số trang nào.

```csharp
// Step 2: Retrieve the first page and its resources
var firstPage = pdfDocument.Pages[1];
var resourcesEditor = new Aspose.Pdf.DictionaryEditor(firstPage.Resources);
```

> **Tại sao điều này quan trọng:** `Resources` chứa các đối tượng như phông chữ, hình ảnh và từ điển `ExtGState` nơi lưu trữ các trạng thái đồ họa. Chỉnh sửa từ điển này là cách duy nhất để ảnh hưởng đến độ trong suốt cho các lệnh vẽ tham chiếu đến trạng thái.

## Bước 3: Đảm bảo tồn tại từ điển ExtGState

Nếu PDF đã chứa mục `ExtGState`, chúng ta có thể tái sử dụng. Nếu không, chúng ta phải tạo một từ điển mới để tránh `KeyNotFoundException`.

```csharp
// Step 3: Get or create the ExtGState dictionary
Aspose.Pdf.CosCosPdfDictionary extGStateDict;

if (resourcesEditor.ContainsKey("ExtGState"))
{
    extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
}
else
{
    // Create a fresh ExtGState dictionary and attach it
    extGStateDict = Aspose.Pdf.CosCosPdfDictionary.CreateEmptyDictionary(pdfDocument);
    resourcesEditor.Add("ExtGState", extGStateDict);
}
```

> **Tại sao điều này quan trọng:** PDF rất linh hoạt; một số tệp không bao giờ định nghĩa `ExtGState`. Tạo một từ điển mới đảm bảo các tham số độ trong suốt sau này có nơi lưu trữ.

## Bước 4: Xây dựng trạng thái đồ họa mới với các giá trị độ trong suốt

Một trạng thái đồ họa (`GS`) chứa các tham số render. Các khóa `CA` (độ trong suốt nét vẽ) và `ca` (độ trong suốt tô) chấp nhận giá trị từ `0` (hoàn toàn trong suốt) đến `1` (đầy đủ không trong suốt). Khóa `BM` chọn chế độ hòa trộn; `"Normal"` là lựa chọn phổ biến nhất.

```csharp
// Step 4: Create a graphics state dictionary and set opacity parameters
var graphicsState = Aspose.Pdf.CosCosPdfDictionary.CreateEmptyDictionary(pdfDocument);

var parameters = new[]
{
    new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>("CA", new Aspose.Pdf.CosPdfNumber(1.0)),   // stroke opacity (fully opaque)
    new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>("ca", new Aspose.Pdf.CosPdfNumber(0.5)), // fill opacity (50% transparent)
    new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>("BM", new Aspose.Pdf.CosPdfName("Normal")) // blend mode
};

foreach (var p in parameters)
{
    graphicsState.Add(p);
}
```

> **Tại sao điều này quan trọng:** Đặt `ca` thành `0.5` báo cho bộ render PDF vẽ các hình dạng được tô với độ trong suốt một nửa. Điều chỉnh các giá trị số để đáp ứng yêu cầu thiết kế của bạn. Mục `BM` là tùy chọn nhưng làm rõ cách nội dung trong suốt hòa trộn với các đối tượng bên dưới.

## Bước 5: Đăng ký trạng thái đồ họa mới vào từ điển ExtGState

Mỗi trạng thái đồ họa phải có một tên duy nhất (ví dụ, `"GS0"`). Bạn có thể tái sử dụng tên nếu muốn ghi đè lên trạng thái hiện có, nhưng sử dụng một định danh mới sẽ tránh các tác động phụ không mong muốn.

```csharp
// Step 5: Add the graphics state to ExtGState with a unique name
extGStateDict.Add("GS0", graphicsState);
```

> **Tại sao điều này quan trọng:** Khi trạng thái đã được lưu, bạn có thể tham chiếu tới nó từ các luồng nội dung trang bằng toán tử `/GS0`. Đây là cơ chế thực sự **cách thêm độ trong suốt** vào các lệnh vẽ.

## Bước 6: Lưu PDF đã chỉnh sửa

Sau khi cập nhật từ điển tài nguyên, ghi các thay đổi trở lại đĩa. Bạn có thể ghi đè lên tệp gốc hoặc tạo một tệp mới; ví dụ tạo `output.pdf` để giữ nguyên nguồn.

```csharp
// Step 6: Save the modified PDF
pdfDocument.Save(@"YOUR_DIRECTORY\output.pdf");
```

> **Tại sao điều này quan trọng:** Phương thức `Save` tuần tự hoá các đối tượng trong bộ nhớ, bao gồm trạng thái đồ họa mới, thành một tệp PDF hợp lệ. Đây là bước cuối cùng trong **cách thay đổi độ trong suốt** và **lưu PDF đã chỉnh sửa**.

## Ví dụ đầy đủ, có thể chạy

Kết hợp tất cả các phần lại với nhau sẽ cho bạn một chương trình tự chứa mà bạn có thể sao chép vào một ứng dụng console.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Collections;

class Program
{
    static void Main()
    {
        // Path to the source PDF
        string pdfPath = @"YOUR_DIRECTORY\input.pdf";

        // Load the document
        using var pdfDocument = new Document(pdfPath);

        // Work with the first page
        var firstPage = pdfDocument.Pages[1];
        var resourcesEditor = new DictionaryEditor(firstPage.Resources);

        // Ensure ExtGState exists
        CosCosPdfDictionary extGStateDict;
        if (resourcesEditor.ContainsKey("ExtGState"))
        {
            extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
        }
        else
        {
            extGStateDict = CosCosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            resourcesEditor.Add("ExtGState", extGStateDict);
        }

        // Create a new graphics state with opacity settings
        var graphicsState = CosCosPdfDictionary.CreateEmptyDictionary(pdfDocument);
        var parameters = new[]
        {
            new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),   // stroke opacity
            new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // fill opacity
            new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // blend mode
        };
        foreach (var p in parameters)
            graphicsState.Add(p);

        // Add the state to ExtGState under the name "GS0"
        extGStateDict.Add("GS0", graphicsState);

        // Save the result
        pdfDocument.Save(@"YOUR_DIRECTORY\output.pdf");

        Console.WriteLine("Opacity changed and PDF saved successfully.");
    }
}
```

### Kết quả mong đợi

Mở `output.pdf` trong bất kỳ trình xem PDF nào. Bất kỳ nội dung nào sau này tham chiếu đến trạng thái đồ họa `GS0` (ví dụ, một hình chữ nhật được vẽ bằng `/GS0 gs`) sẽ hiển thị với **độ trong suốt tô 50 %** trong khi nét vẽ vẫn hoàn toàn không trong suốt. Nếu bạn thêm các lệnh vẽ như vậy qua API `Page.Contents.Add` của Aspose.Pdf, bạn sẽ thấy hiệu ứng trong suốt ngay lập tức.

## Xử lý nhiều trang và nhiều trạng thái đồ họa

- **Nhiều trang:** Lặp qua `pdfDocument.Pages` và lặp lại các bước 2‑5 cho mỗi trang bạn muốn ảnh hưởng. Nhớ sử dụng các tên trạng thái riêng biệt (`GS1`, `GS2`, …) nếu các trang cần mức độ trong suốt khác nhau.
- **Tái sử dụng trạng thái hiện có:** Nếu PDF đã chứa một trạng thái có tên `"GS0"` và bạn chỉ muốn thay đổi độ trong suốt của nó, hãy lấy nó bằng `extGStateDict["GS0"]` thay vì tạo mục mới.
- **Mẹo hiệu năng:** Thêm nhiều trạng thái đồ họa có thể làm tăng kích thước tệp. Hợp nhất các thiết lập độ trong suốt giống nhau vào một trạng thái duy nhất và tham chiếu nó từ nhiều trang.

## Những lỗi thường gặp và cách tránh

| Vấn đề | Nguyên nhân | Cách khắc phục |
|-------|-------|-----|
| `KeyNotFoundException` trên `"ExtGState"` | PDF không có từ điển này. | Tạo một từ điển như đã trình bày ở Bước 3. |
| Độ trong suốt không hiển thị | Luồng nội dung không tham chiếu tới trạng thái mới. | Chèn `/GS0 gs` trước các lệnh vẽ hoặc sử dụng API `Graphics` của Aspose.Pdf với tham số `GraphicsState`. |
| PDF đầu ra bị hỏng | Cố gắng lưu vào thư mục chỉ đọc. | Đảm bảo đường dẫn đích có thể ghi và không phải cùng một tệp đang mở. |
| Giá trị độ trong suốt > 1 hoặc < 0 | Nhầm lẫn truyền phần trăm thay vì phân số. | Sử dụng số trong khoảng `0.0` đến `1.0`. |

## Các bước tiếp theo

Bây giờ bạn đã biết **cách thay đổi độ trong suốt** và **cách thêm độ trong suốt**, bạn có thể khám phá các chủ đề liên quan:

- [Cách Thêm Watermark Hình Ảnh Quay Tròn vào PDF bằng Aspose.PDF cho .NET](/pdf/english/net/watermarks-backgrounds/add-rotating-image-watermark-aspose-pdf/)
- [Cách Thêm Dấu Ấn Trang trong PDF bằng Aspose.PDF cho .NET: Hướng Dẫn Toàn Diện](/pdf/english/net/watermarks-backgrounds/add-page-stamp-aspose-pdf-dotnet-guide/)
- [Cách Thêm Dấu Ấn Số Trang trong PDF bằng Aspose.PDF cho .NET | Watermarks & Backgrounds](/pdf/english/net/watermarks-backgrounds/add-page-number-stamp-using-aspose-pdf-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}