---
category: general
date: 2026-08-11
description: Thay đổi độ trong suốt của PDF bằng Aspose.Pdf trong C#. Tìm hiểu cách
  thêm độ trong suốt vào các trang PDF, thiết lập trạng thái đồ họa và lưu kết quả
  nhanh chóng.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- change opacity PDF
- how to add transparency
- add pdf transparency
language: vi
lastmod: 2026-08-11
og_description: Thay đổi độ trong suốt PDF với Aspose.Pdf trong C#. Hãy theo dõi hướng
  dẫn này để xem cách thêm tính trong suốt vào bất kỳ tài liệu PDF nào, tùy chỉnh
  trạng thái đồ họa và xuất kết quả.
og_image_alt: Screenshot illustrating change opacity PDF example in C# code
og_title: Thay đổi độ trong suốt PDF trong C# – hướng dẫn đầy đủ Aspose.Pdf
schemas:
- author: Aspose
  dateModified: '2026-08-11'
  description: Change opacity PDF using Aspose.Pdf in C#. Learn how to add transparency
    to PDF pages, set graphic state, and save the result quickly.
  headline: Change opacity PDF in C# with Aspose.Pdf – step‑by‑step guide
  type: TechArticle
- description: Change opacity PDF using Aspose.Pdf in C#. Learn how to add transparency
    to PDF pages, set graphic state, and save the result quickly.
  name: Change opacity PDF in C# with Aspose.Pdf – step‑by‑step guide
  steps:
  - name: '**Missing ExtGState dictionary** – Some PDFs do not contain an `ExtGState`
      entry by default. In that case, create one:'
    text: '**Missing ExtGState dictionary** – Some PDFs do not contain an `ExtGState`
      entry by default. In that case, create one:'
  - name: '**Incorrect resource name** – The name you use in `SetGraphicsState` must
      match exactly the key you added (`GS0`). A typo results in the default, fully
      opaque rendering.'
    text: '**Incorrect resource name** – The name you use in `SetGraphicsState` must
      match exactly the key you added (`GS0`). A typo results in the default, fully
      opaque rendering.'
  - name: '**Overriding existing graphics states** – Adding a new entry does not replace
      existing ones. If you reuse a name that already exists, you may unintentionally
      alter other page elements that reference it.'
    text: '**Overriding existing graphics states** – Adding a new entry does not replace
      existing ones. If you reuse a name that already exists, you may unintentionally
      alter other page elements that reference it.'
  - name: '**Viewer compatibility** – Older PDF viewers (pre‑1.4) may ignore transparency.
      Ensure your target audience uses a modern viewer such as Adobe Reader DC or
      Chrome’s built‑in PDF viewer.'
    text: '**Viewer compatibility** – Older PDF viewers (pre‑1.4) may ignore transparency.
      Ensure your target audience uses a modern viewer such as Adobe Reader DC or
      Chrome’s built‑in PDF viewer.'
  type: HowTo
tags:
- PDF
- C#
- Aspose.Pdf
- Transparency
title: Thay đổi độ trong suốt PDF trong C# với Aspose.Pdf – hướng dẫn từng bước
url: /vi/net/programming-with-pdf-pages/change-opacity-pdf-in-c-with-aspose-pdf-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Thay đổi độ trong suốt PDF trong C# với Aspose.Pdf – hướng dẫn từng bước

Nếu bạn cần **thay đổi độ trong suốt PDF** một cách lập trình, hướng dẫn này sẽ chỉ cho bạn cách thực hiện. Sử dụng Aspose.Pdf cho .NET, bạn có thể kiểm soát độ trong suốt của các đối tượng đồ họa, văn bản và hình ảnh mà không rời khỏi mã C# của mình.

Trong các phần sau, bạn sẽ học **cách thêm độ trong suốt** vào một trang PDF, ý nghĩa của các đối tượng trạng thái đồ họa nền tảng, và cách lưu tài liệu đã chỉnh sửa. Hướng dẫn cũng đề cập đến các lỗi thường gặp khi bạn **thêm độ trong suốt PDF** và cung cấp các mẹo cho các kịch bản thực tế.

## Những gì bạn sẽ đạt được

* Tải một tài liệu PDF hiện có.  
* Tạo một từ điển trạng thái đồ họa mới định nghĩa các giá trị độ trong suốt.  
* Chèn trạng thái đồ họa vào từ điển tài nguyên của trang.  
* Lưu tài liệu với hiệu ứng **thay đổi độ trong suốt PDF** đã được cập nhật.

Không cần công cụ bên ngoài—chỉ cần thư viện Aspose.Pdf cho .NET (phiên bản 23.10 hoặc mới hơn) và môi trường phát triển .NET.

## Yêu cầu trước

* .NET 6.0 (hoặc .NET Framework 4.7.2+) đã được cài đặt.  
* Visual Studio 2022 hoặc bất kỳ IDE nào hỗ trợ C#.  
* Tham chiếu đến gói NuGet `Aspose.Pdf`.  
* Một tệp PDF đầu vào (`input.pdf`) nằm trong thư mục có quyền ghi.

> **Mẹo chuyên nghiệp:** Khi thử nghiệm thay đổi độ trong suốt, hãy làm việc với một PDF đã chứa đồ họa vector hoặc văn bản; hình ảnh raster sẽ bỏ qua các tham số `ca` và `CA` trừ khi chúng được đặt trong một nhóm trong suốt.

## Thay đổi độ trong suốt PDF với Aspose.Pdf

Cốt lõi của giải pháp là sửa đổi từ điển **ExtGState** (trạng thái đồ họa bên ngoài) của một trang. Từ điển này lưu trữ các tham số như **ca** (độ trong suốt nét) và **CA** (độ trong suốt tô). Bằng cách thêm một mục mới, bạn có thể tham chiếu nó sau này trong các luồng nội dung.

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;

class ChangeOpacityPdfExample
{
    static void Main()
    {
        // Step 1: Load the PDF document
        using (var document = new Document("YOUR_DIRECTORY/input.pdf"))
        {
            // Step 2: Access the first page and its resource dictionary
            var page = document.Pages[1];
            var dictEditor = new DictionaryEditor(page.Resources);
            var extGState = dictEditor["ExtGState"].ToCosPdfDictionary();

            // Step 3: Create a new graphics state dictionary with desired opacity values
            var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(document);
            var parameters = new[]
            {
                // Fill opacity (CA) – 1.0 means fully opaque
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
                // Stroke opacity (ca) – 0.5 makes lines semi‑transparent
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
                // Blend mode (BM) – Normal is the default blend mode
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
            };
            foreach (var p in parameters) newGraphicsState.Add(p);

            // Step 4: Add the new graphics state to the ExtGState dictionary
            // “GS0” is the identifier you will reference later in the content stream
            extGState.Add("GS0", newGraphicsState);

            // Optional: Demonstrate usage by drawing a semi‑transparent rectangle
            // This part shows how the new graphics state affects drawing commands.
            var canvas = new Aspose.Pdf.Drawing.Graphic(page);
            canvas.SetGraphicsState("GS0"); // Apply the opacity settings
            canvas.Rectangle(100, 500, 200, 600);
            canvas.FillColor = Color.FromRgb(255, 0, 0); // Red fill
            canvas.StrokeColor = Color.FromRgb(0, 0, 255); // Blue border
            canvas.Draw();

            // Step 5: Save the modified PDF
            document.Save("YOUR_DIRECTORY/output.pdf");
        }

        Console.WriteLine("PDF saved with changed opacity.");
    }
}
```

### Tại sao cách này hoạt động

* **ExtGState** là một tài nguyên PDF lưu trữ các tham số đồ họa có thể tái sử dụng. Bằng cách thêm một mục tùy chỉnh (`GS0`) bạn tạo ra một cấu hình độ trong suốt có thể tái sử dụng.  
* Khóa **ca** điều khiển độ trong suốt của các thao tác nét (đường, viền). Khóa **CA** điều khiển độ trong suốt của các thao tác tô (hình dạng màu, văn bản). Đặt `ca = 0.5` làm cho các nét trong suốt 50 %, trong khi `CA = 1` giữ các phần tô hoàn toàn không trong suốt.  
* Lệnh `SetGraphicsState("GS0")` thông báo cho Aspose.Pdf phát ra toán tử `/GS0 gs` trong luồng nội dung, kích hoạt các cài đặt trong suốt mới cho bất kỳ lệnh vẽ nào tiếp theo.

## Cách thêm độ trong suốt vào nội dung hiện có

Nếu bạn đã có văn bản hoặc hình ảnh trên trang và muốn làm chúng bán trong suốt mà không cần vẽ lại, bạn có thể chèn một toán tử **gs** trước nội dung hiện có. Đoạn mã dưới đây minh họa cách chèn toán tử vào đầu luồng nội dung của trang.

```csharp
// Retrieve the existing content stream
var content = page.Contents[1];
var originalBytes = content.ToByteArray();

// Build the new content with the graphics state applied
var gsOperator = System.Text.Encoding.ASCII.GetBytes("/GS0 gs\n");
var newBytes = new List<byte>(gsOperator);
newBytes.AddRange(originalBytes);

// Replace the page content
page.Contents[1].Replace(newBytes.ToArray());
```

### Các trường hợp đặc biệt và lưu ý

| Tình huống | Cách xử lý đề xuất |
|-----------|----------------------|
| **Nhiều trang** | Lặp qua `document.Pages` và lặp lại các bước 2‑4 cho mỗi trang bạn muốn áp dụng. |
| **Độ trong suốt khác nhau cho từng phần tử** | Tạo các trạng thái đồ họa bổ sung (`GS1`, `GS2`, …) với các giá trị `ca`/`CA` khác nhau và áp dụng chúng một cách chọn lọc. |
| **PDF có mục ExtGState hiện có** | Sử dụng `dictEditor["ExtGState"]` một cách an toàn; nếu khóa không tồn tại, tạo một `CosPdfDictionary` mới và gán nó cho `page.Resources`. |
| **Nhóm trong suốt** | Đối với việc hợp thành phức tạp (ví dụ: hình ảnh chồng lên nhau), thiết lập từ điển `/Group` với `S /Transparency` và `CS /DeviceRGB`. Điều này vượt ra ngoài **thay đổi độ trong suốt PDF** cơ bản nhưng có thể cần cho các bố cục nâng cao. |

## Thêm độ trong suốt PDF vào đồ họa vector

Ngoài các hình chữ nhật, bạn có thể áp dụng cùng một trạng thái đồ họa cho bất kỳ bản vẽ vector nào—đường, đường cong, hoặc thậm chí văn bản. Dưới đây là một ví dụ nhanh ghi văn bản bán trong suốt:

```csharp
var textFragment = new TextFragment("Transparent text")
{
    Position = new Position(100, 400),
    TextState = { FontSize = 36, ForegroundColor = Color.Black }
};
page.Paragraphs.Add(textFragment);

// Apply the graphics state to the text fragment
textFragment.TextState.GraphicsState = "GS0";
```

Thuộc tính `GraphicsState` của `TextState` cho phép engine PDF render văn bản bằng độ trong suốt được định nghĩa trong `GS0`. Đây là cách đơn giản nhất để **thêm độ trong suốt pdf** vào nội dung văn bản.

## Những lỗi thường gặp khi bạn thay đổi độ trong suốt PDF

1. **Missing ExtGState dictionary** – Một số PDF không có mục `ExtGState` theo mặc định. Trong trường hợp này, hãy tạo một mục mới:  
   ```csharp
   if (!dictEditor.ContainsKey("ExtGState"))
       dictEditor.Add("ExtGState", new CosPdfDictionary(document));
   ```
2. **Incorrect resource name** – Tên bạn dùng trong `SetGraphicsState` phải khớp chính xác với khóa bạn đã thêm (`GS0`). Lỗi đánh máy sẽ dẫn đến việc render mặc định, hoàn toàn không trong suốt.  
3. **Overriding existing graphics states** – Thêm một mục mới không thay thế các mục hiện có. Nếu bạn tái sử dụng một tên đã tồn tại, có thể vô tình thay đổi các phần tử khác trên trang tham chiếu tới nó.  
4. **Viewer compatibility** – Các trình xem PDF cũ (trước phiên bản 1.4) có thể bỏ qua độ trong suốt. Đảm bảo người dùng mục tiêu của bạn sử dụng trình xem hiện đại như Adobe Reader DC hoặc trình xem PDF tích hợp của Chrome.

## Ví dụ đầy đủ hoạt động

Dưới đây là chương trình hoàn chỉnh, tự chứa, mà bạn có thể sao chép, dán và chạy. Nó bao gồm tất cả các chỉ thị `using` cần thiết, xử lý lỗi và chú thích.



## Bạn nên học gì tiếp theo?

Các hướng dẫn sau đây bao gồm các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên đều có các ví dụ mã hoạt động đầy đủ với giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Cách Thêm Đóng Dấu Văn Bản vào PDF bằng Aspose.PDF .NET: Hướng Dẫn Toàn Diện](/pdf/english/net/watermarks-backgrounds/add-text-stamp-pdf-aspose-pdf-dotnet/)
- [Cách Thêm Đóng Dấu Trang trong PDF bằng Aspose.PDF cho .NET: Hướng Dẫn Hoàn Chỉnh](/pdf/english/net/watermarks-backgrounds/add-page-stamp-aspose-pdf-dotnet-guide/)
- [Cách Thêm Đóng Dấu Trang trong PDF bằng Aspose.PDF cho .NET | Hướng Dẫn Đánh Dấu & Nền](/pdf/english/net/watermarks-backgrounds/implement-page-stamps-aspose-pdf-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}