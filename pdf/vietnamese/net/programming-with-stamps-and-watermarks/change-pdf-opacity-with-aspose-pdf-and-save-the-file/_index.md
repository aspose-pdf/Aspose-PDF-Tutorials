---
category: general
date: 2026-11-12
description: Tìm hiểu cách thay đổi độ trong suốt của PDF bằng Aspose.Pdf, thêm hiệu
  ứng trong suốt, thiết lập chế độ hòa trộn và lưu PDF đã chỉnh sửa trong C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- change PDF opacity
- how to add transparency
- save modified PDF
- how to set blend mode
- set fill opacity
language: vi
lastmod: 2026-11-12
og_description: Thay đổi độ trong suốt của PDF với Aspose.Pdf, tìm hiểu cách thêm
  độ trong suốt, thiết lập chế độ hòa trộn và lưu các tệp PDF đã chỉnh sửa trong C#.
og_image_alt: Screenshot of a PDF page with altered opacity using Aspose.Pdf
og_title: Thay đổi độ trong suốt PDF với Aspose.Pdf – thêm độ trong suốt và lưu
schemas:
- author: Aspose
  dateModified: '2026-11-12'
  description: Learn how to change PDF opacity using Aspose.Pdf, add transparency,
    set blend mode, and save modified PDF in C#.
  headline: Change PDF opacity with Aspose.Pdf and save the file
  type: TechArticle
- description: Learn how to change PDF opacity using Aspose.Pdf, add transparency,
    set blend mode, and save modified PDF in C#.
  name: Change PDF opacity with Aspose.Pdf and save the file
  steps:
  - name: Load the PDF document
    text: Start by creating a `Document` instance that points to your source file.
      The constructor reads the entire PDF into memory, allowing you to manipulate
      its internal objects.
  - name: Access the first page’s resources
    text: Each PDF page stores a *resource dictionary* that holds objects such as
      fonts, images, and graphics states. You need to edit this dictionary to inject
      a new `ExtGState` entry.
  - name: Ensure an ExtGState dictionary exists
    text: The `ExtGState` dictionary holds custom graphics states. If it does not
      exist, the code creates one automatically.
  - name: Define a new graphics state (ExtGState)
    text: A graphics state defines how drawing operations behave. The following dictionary
      sets stroke opacity (`CA`), fill opacity (`ca`), and blend mode (`BM`).
  - name: Register the graphics state in the resource dictionary
    text: Give the new state a name (e.g., `GS0`) and add it to the `ExtGState` dictionary.
      This name will be referenced later in the page content stream.
  - name: Apply the graphics state to page content
    text: To actually see the opacity effect, insert the `/GS0 gs` operator before
      the drawing commands you want to affect. The example below draws a semi‑transparent
      rectangle.
  - name: Save the modified PDF
    text: Finally, write the updated document to disk. The `Save` method overwrites
      the target file or creates a new one if it does not exist.
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Thay đổi độ trong suốt của PDF bằng Aspose.Pdf và lưu tệp
url: /vi/net/programming-with-stamps-and-watermarks/change-pdf-opacity-with-aspose-pdf-and-save-the-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Thay đổi độ trong suốt PDF với Aspose.Pdf và lưu tệp

Nếu bạn cần **thay đổi độ trong suốt PDF** trong một tài liệu, Aspose.Pdf cung cấp một API đơn giản để điều chỉnh độ trong suốt của đường viền và phần tô. Hướng dẫn này cho thấy **cách thêm độ trong suốt**, **cách đặt chế độ hòa trộn**, và **lưu các tệp PDF đã chỉnh sửa** chỉ với vài dòng mã C#.

Bạn sẽ đi qua từng bước—từ việc tải một PDF hiện có đến việc định nghĩa một trạng thái đồ họa mới và lưu các thay đổi. Khi kết thúc hướng dẫn, bạn có thể:

* Giảm độ hiển thị của đồ họa vector hoặc hình ảnh.
* Áp dụng một chế độ hòa trộn tùy chỉnh như *Normal* hoặc *Multiply*.
* Xuất tệp đã cập nhật mà không mất bất kỳ nội dung nào khác.

Yêu cầu duy nhất là môi trường phát triển .NET hoạt động và tham chiếu tới thư viện Aspose.Pdf (phiên bản 23.9 trở lên). Không cần công cụ bên ngoài.

## Yêu cầu trước

| Yêu cầu | Lý do quan trọng |
|-------------|----------------|
| .NET 6.0 SDK hoặc mới hơn | Đảm bảo tương thích với các API mới nhất của Aspose.Pdf. |
| Gói NuGet Aspose.Pdf for .NET | Cung cấp các lớp `Document`, `CosPdfDictionary`, và các lớp liên quan được sử dụng trong mã. |
| Một tệp PDF để chỉnh sửa (ví dụ, `input.pdf`) | Là nguồn để thực hiện các thay đổi độ trong suốt. |

Cài đặt gói NuGet bằng:

```bash
dotnet add package Aspose.Pdf
```

## Thay đổi độ trong suốt PDF với Aspose.Pdf

### Bước 1: Tải tài liệu PDF

Bắt đầu bằng cách tạo một thể hiện `Document` trỏ tới tệp nguồn của bạn. Hàm khởi tạo sẽ đọc toàn bộ PDF vào bộ nhớ, cho phép bạn thao tác với các đối tượng nội bộ.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Operators;
using Aspose.Pdf.XObjects;
using Aspose.Pdf.Facades;

// Load the existing PDF
var pdfDoc = new Document(@"YOUR_DIRECTORY\input.pdf");
```

> **Tại sao cần bước này?** Việc tải tệp tạo ra một mô hình đối tượng có thể thao tác. Tất cả các thay đổi sau này sẽ được thực hiện trên biểu diễn trong bộ nhớ này, đảm bảo tệp gốc không bị thay đổi cho đến khi bạn lưu một cách có chủ ý.

### Bước 2: Truy cập tài nguyên của trang đầu tiên

Mỗi trang PDF lưu trữ một *từ điển tài nguyên* chứa các đối tượng như phông chữ, hình ảnh và trạng thái đồ họa. Bạn cần chỉnh sửa từ điển này để chèn một mục `ExtGState` mới.

```csharp
// Retrieve the first page (pages are 1‑based)
var page = pdfDoc.Pages[1];

// The DictionaryEditor simplifies access to the page's resource dictionary
var resourcesEditor = new DictionaryEditor(page.Resources);
```

> **Mẹo:** Nếu PDF của bạn có nhiều trang cần cùng độ trong suốt, lặp lại bước này cho mỗi trang hoặc chia sẻ một `ExtGState` duy nhất giữa các trang.

### Bước 3: Đảm bảo tồn tại từ điển ExtGState

Từ điển `ExtGState` chứa các trạng thái đồ họa tùy chỉnh. Nếu nó không tồn tại, đoạn mã sẽ tự động tạo một từ điển mới.

```csharp
// Get or create the ExtGState dictionary
var extGStateDict = resourcesEditor["ExtGState"]?.ToCosPdfDictionary()
                     ?? new CosPdfDictionary(pdfDoc);
resourcesEditor["ExtGState"] = extGStateDict;
```

> **Tại sao cần bước này?** Nếu không có container `ExtGState`, bất kỳ cố gắng tham chiếu tới trạng thái đồ họa mới nào cũng sẽ thất bại, dẫn đến PDF bỏ qua các cài đặt độ trong suốt của bạn.

### Bước 4: Định nghĩa một trạng thái đồ họa mới (ExtGState)

Một trạng thái đồ họa xác định cách các thao tác vẽ hoạt động. Từ điển dưới đây đặt độ trong suốt đường viền (`CA`), độ trong suốt phần tô (`ca`) và chế độ hòa trộn (`BM`).

```csharp
// Create an empty dictionary for the new graphics state
var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDoc);

// Set desired parameters
var parameters = new[]
{
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),   // Stroke opacity (1 = opaque)
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // Fill opacity (0.5 = 50% transparent)
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // Blend mode
};

foreach (var param in parameters)
    newGraphicsState.Add(param);
```

> **Cách đặt độ trong suốt phần tô:** Mục `ca` kiểm soát độ trong suốt của các hình dạng được tô (văn bản, đường dẫn). Điều chỉnh giá trị số giữa `0` (hoàn toàn trong suốt) và `1` (hoàn toàn mờ) để đáp ứng yêu cầu thiết kế của bạn.  
> **Cách đặt chế độ hòa trộn:** Mục `BM` chọn thuật toán hợp thành. Các giá trị phổ biến bao gồm `Normal`, `Multiply`, `Screen`, và `Overlay`. Chọn giá trị phù hợp với ý định hình ảnh của bạn.

### Bước 5: Đăng ký trạng thái đồ họa vào từ điển tài nguyên

Gán cho trạng thái mới một tên (ví dụ, `GS0`) và thêm nó vào từ điển `ExtGState`. Tên này sẽ được tham chiếu sau này trong luồng nội dung của trang.

```csharp
// Add the graphics state with a symbolic name
extGStateDict.Add("GS0", newGraphicsState);
```

> **Mẹo chuyên nghiệp:** Sử dụng quy ước đặt tên như `GS0`, `GS1`, … khi tạo nhiều trạng thái. Điều này ngăn xung đột tên và giúp việc gỡ lỗi dễ dàng hơn.

### Bước 6: Áp dụng trạng thái đồ họa vào nội dung trang

Để thực sự thấy hiệu ứng độ trong suốt, chèn toán tử `/GS0 gs` trước các lệnh vẽ mà bạn muốn ảnh hưởng. Ví dụ dưới đây vẽ một hình chữ nhật bán trong suốt.

```csharp
// Build a content stream that uses the new graphics state
var content = new MemoryStream();
var writer = new StreamWriter(content);

// Activate the graphics state
writer.WriteLine("q");                 // Save graphics state
writer.WriteLine("/GS0 gs");           // Apply custom ExtGState
writer.WriteLine("0.2 0.5 0.8 rg");    // Set fill color (RGB)
writer.WriteLine("100 500 200 100 re"); // Rectangle (x y width height)
writer.WriteLine("f");                 // Fill rectangle
writer.WriteLine("Q");                 // Restore graphics state
writer.Flush();

content.Position = 0;
page.Contents.Add(new ContentStream(content));
```

> **Tại sao cần các toán tử `q` và `Q`?** Chúng đẩy và bật ngăn xếp trạng thái đồ họa, đảm bảo thay đổi độ trong suốt chỉ ảnh hưởng tới hình chữ nhật và không ảnh hưởng tới phần còn lại của trang.

### Bước 7: Lưu PDF đã chỉnh sửa

Cuối cùng, ghi tài liệu đã cập nhật ra đĩa. Phương thức `Save` sẽ ghi đè tệp đích hoặc tạo tệp mới nếu chưa tồn tại.

```csharp
// Persist the changes
pdfDoc.Save(@"YOUR_DIRECTORY\output.pdf");
```

> **Cách lưu PDF đã chỉnh sửa:** Lệnh `Save` ghi tất cả các thay đổi trong bộ nhớ, bao gồm `ExtGState` mới, tới đường dẫn đã chỉ định. Bạn cũng có thể truyền kết quả tới một `MemoryStream` để trả về trong các phản hồi web.

## Ví dụ hoàn chỉnh hoạt động

Dưới đây là một chương trình độc lập duy nhất tích hợp mọi bước đã mô tả ở trên. Sao chép nó vào một ứng dụng console và chạy để xác nhận việc thay đổi độ trong suốt.



## Bạn nên học gì tiếp theo?

Các hướng dẫn sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng dựa trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh với giải thích chi tiết từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Cách lưu PDF đã chỉnh sửa với Aspose.Pdf và thêm độ trong suốt](/pdf/english/net/document-manipulation/how-to-save-modified-pdf-with-aspose-pdf-and-add-transparenc/)
- [Cách thêm độ trong suốt vào PDF bằng Aspose.PDF trong C#](/pdf/english/net/images-graphics/how-to-add-transparency-to-pdf-using-aspose-pdf-in-c/)
- [Cách thêm trạng thái đồ họa pdf và kiểm soát độ trong suốt với Aspose.PDF](/pdf/english/net/images-graphics/how-to-add-graphics-state-pdf-and-control-transparency-with/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}