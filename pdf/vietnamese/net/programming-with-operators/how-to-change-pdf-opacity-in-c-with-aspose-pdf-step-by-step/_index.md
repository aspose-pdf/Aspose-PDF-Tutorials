---
category: general
date: 2026-10-23
description: Cách thay đổi độ trong suốt của PDF bằng Aspose.Pdf trong C#. Học cách
  chỉnh sửa ExtGState, đặt độ trong suốt nét vẽ/lấp đầy và áp dụng các chế độ hòa
  trộn chỉ trong vài dòng mã.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to change PDF opacity
- Aspose.Pdf opacity
- PDF graphics state
- ExtGState dictionary
- C# PDF manipulation
- PDF blend mode
language: vi
lastmod: 2026-10-23
og_description: Cách thay đổi độ trong suốt của PDF bằng Aspose.Pdf trong C#. Hãy
  theo hướng dẫn ngắn gọn này để chỉnh sửa độ trong suốt đường viền và nền, thiết
  lập chế độ hòa trộn, và lưu tài liệu đã cập nhật.
og_image_alt: Screenshot of a PDF page with semi‑transparent graphics created by Aspose.Pdf
  in C#
og_title: Cách thay đổi độ trong suốt của PDF trong C# – hướng dẫn đầy đủ Aspose.Pdf
schemas:
- author: Aspose
  dateModified: '2026-10-23'
  description: How to change PDF opacity using Aspose.Pdf in C#. Learn to edit ExtGState,
    set stroke/fill opacity, and apply blend modes in just a few lines of code.
  headline: How to change PDF opacity in C# with Aspose.Pdf – step‑by‑step guide
  type: TechArticle
- description: How to change PDF opacity using Aspose.Pdf in C#. Learn to edit ExtGState,
    set stroke/fill opacity, and apply blend modes in just a few lines of code.
  name: How to change PDF opacity in C# with Aspose.Pdf – step‑by‑step guide
  steps:
  - name: Load the PDF document
    text: '```csharp using Aspose.Pdf;'
  - name: Get the first page and its resource dictionary
    text: '```csharp // Step 2: Get the first page and its resource dictionary var
      firstPage = pdfDocument.Pages[1]; var resourcesEditor = new DictionaryEditor(firstPage.Resources);
      ```'
  - name: Retrieve (or create) the ExtGState dictionary
    text: '```csharp // Step 3: Retrieve the ExtGState dictionary from the page resources
      // If ExtGState does not exist, create an empty one. CosPdfDictionary extGStateDict;
      if (resourcesEditor.ContainsKey("ExtGState")) { extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
      } else { extGStateDic'
  - name: Create a new graphics state dictionary and define opacity entries
    text: '```csharp // Step 4: Create a new graphics state dictionary and define
      its entries var graphicsStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
      var graphicsStateEntries = new[] { new KeyValuePair<string, ICosPdfPrimitive>("CA",
      new CosPdfNumber(1.0)), // Stroke opacity (fully opaque)'
  - name: Add the new graphics state to the ExtGState dictionary
    text: '```csharp // Step 5: Add the new graphics state to the ExtGState dictionary
      (named "GS0") extGStateDict.Add("GS0", graphicsStateDict); ```'
  - name: Save the updated PDF document
    text: '```csharp // Step 6: Save the updated PDF document pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
      } ```'
  type: HowTo
tags:
- PDF
- C#
- Aspose.Pdf
- Opacity
- GraphicsState
title: Cách thay đổi độ trong suốt của PDF trong C# với Aspose.Pdf – hướng dẫn từng
  bước
url: /vi/net/programming-with-operators/how-to-change-pdf-opacity-in-c-with-aspose-pdf-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách thay đổi độ trong suốt PDF trong C# với Aspose.Pdf – hướng dẫn chi tiết

Nếu bạn cần **cách thay đổi độ trong suốt PDF** cho các thành phần cụ thể, hướng dẫn này cung cấp một giải pháp hoàn chỉnh, có thể chạy ngay. Bạn sẽ thấy cách chỉnh sửa từ điển ExtGState, đặt độ trong suốt cho đường viền và phần tô, và chọn chế độ hòa trộn — tất cả chỉ với vài dòng mã C# rõ ràng.

Thay đổi độ trong suốt PDF hữu ích khi bạn muốn thêm watermark, đồ họa chồng lên, hoặc hiệu ứng hình ảnh nhẹ nhàng mà không cần xây dựng lại toàn bộ tài liệu. Hướng dẫn giả định bạn đã có môi trường C# cơ bản và đã cài đặt thư viện Aspose.Pdf cho .NET.

![how to change PDF opacity using Aspose.Pdf in C#](https://example.com/og-image.png)

## Yêu cầu trước

Trước khi bắt đầu, hãy chắc chắn rằng bạn có:

* .NET 6.0 hoặc mới hơn (mã cũng hoạt động với .NET Framework 4.7+)
* Bản sao có giấy phép của **Aspose.Pdf for .NET** (bản dùng thử miễn phí đủ cho việc thử nghiệm)
* Một tệp PDF đầu vào nằm trong thư mục bạn có thể tham chiếu từ mã
* Visual Studio 2022 hoặc bất kỳ trình soạn thảo C# nào bạn thích

Không cần thêm gói NuGet nào — Aspose.Pdf đã chứa tất cả các kiểu được sử dụng trong hướng dẫn này.

## Hiểu trạng thái đồ họa PDF

Một trang PDF lưu trữ các tham số vẽ trong một đối tượng **graphics state**. Từ điển **ExtGState** chứa các mục như:

* **CA** – độ trong suốt đường viền (0 = trong suốt, 1 = đục)
* **ca** – độ trong suốt phần tô
* **BM** – chế độ hòa trộn (ví dụ: *Normal*, *Multiply*, *Screen*)

Bằng cách tạo một từ điển trạng thái đồ họa mới và thêm nó vào bộ sưu tập ExtGState của trang, bạn có thể tham chiếu trạng thái này sau này trong các luồng nội dung. Cách này tránh việc ghi lại toàn bộ nội dung trang và hoạt động với bất kỳ PDF nào hiện có.

## Cách thay đổi độ trong suốt PDF với Aspose.Pdf

Sáu bước sau đây bao phủ toàn bộ quy trình — từ tải tài liệu đến lưu tệp đã chỉnh sửa. Mỗi bước bao gồm đoạn mã chính xác bạn cần và giải thích lý do bước đó quan trọng.

### Bước 1: Tải tài liệu PDF

```csharp
using Aspose.Pdf;

// Step 1: Load the PDF document
using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
{
    // Subsequent steps go here
}
```

**Tại sao điều này quan trọng** – Mở tệp bằng `Aspose.Pdf.Document` cho phép bạn truy cập đầy đủ vào cấu trúc PDF nội bộ, bao gồm cả tài nguyên trang nơi từ điển **ExtGState** tồn tại.

### Bước 2: Lấy trang đầu tiên và từ điển tài nguyên của nó

```csharp
// Step 2: Get the first page and its resource dictionary
var firstPage = pdfDocument.Pages[1];
var resourcesEditor = new DictionaryEditor(firstPage.Resources);
```

**Tại sao điều này quan trọng** – Mỗi trang có một từ điển *Resources* nhóm các phông chữ, hình ảnh và trạng thái đồ họa. `DictionaryEditor` cung cấp khả năng đọc/ghi thuận tiện cho bộ sưu tập này.

### Bước 3: Lấy (hoặc tạo) từ điển ExtGState

```csharp
// Step 3: Retrieve the ExtGState dictionary from the page resources
// If ExtGState does not exist, create an empty one.
CosPdfDictionary extGStateDict;
if (resourcesEditor.ContainsKey("ExtGState"))
{
    extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
}
else
{
    extGStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
    resourcesEditor["ExtGState"] = extGStateDict;
}
```

**Tại sao điều này quan trọng** – Một số PDF đã có mục **ExtGState**; các PDF khác thì không. Logic điều kiện đảm bảo hướng dẫn hoạt động cho cả hai trường hợp, làm cho nó mạnh mẽ với các tệp thực tế.

### Bước 4: Tạo một từ điển trạng thái đồ họa mới và định nghĩa các mục độ trong suốt

```csharp
// Step 4: Create a new graphics state dictionary and define its entries
var graphicsStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
var graphicsStateEntries = new[]
{
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),   // Stroke opacity (fully opaque)
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),   // Fill opacity (50 % transparent)
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // Blend mode
};

foreach (var entry in graphicsStateEntries)
    graphicsStateDict.Add(entry);
```

**Tại sao điều này quan trọng** – Ba mục chính kiểm soát cách các lệnh vẽ được hiển thị:

* `CA = 1.0` giữ cho các đường viền hoàn toàn hiển thị.
* `ca = 0.5` làm cho các hình dạng được tô bán trong suốt.
* `BM = Normal` sử dụng chế độ hòa trộn mặc định; bạn có thể thay `"Normal"` bằng `"Multiply"` hoặc `"Screen"` để tạo hiệu ứng sáng tạo.

### Bước 5: Thêm trạng thái đồ họa mới vào từ điển ExtGState

```csharp
// Step 5: Add the new graphics state to the ExtGState dictionary (named "GS0")
extGStateDict.Add("GS0", graphicsStateDict);
```

**Tại sao điều này quan trọng** – Đặt tên mục `"GS0"` tạo một tham chiếu mà bạn có thể dùng sau này trong luồng nội dung (`/GS0 gs`). Nếu cần nhiều mức độ trong suốt, thêm các mục bổ sung (`"GS1"`, `"GS2"`, …) với các giá trị `CA`/`ca` khác nhau.

### Bước 6: Lưu tài liệu PDF đã cập nhật

```csharp
// Step 6: Save the updated PDF document
pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
}
```

**Tại sao điều này quan trọng** – Ghi lại các thay đổi sẽ đưa từ điển **ExtGState** đã chỉnh sửa trở lại tệp. PDF kết quả bây giờ chứa một trạng thái đồ họa có thể tái sử dụng mà bất kỳ lệnh vẽ nào cũng có thể gọi.

## Áp dụng trạng thái đồ họa mới vào nội dung trang

Các bước trên chỉ tạo ra trạng thái đồ họa; bạn vẫn cần tham chiếu nó trong luồng nội dung của trang. Dưới đây là một ví dụ nhanh vẽ một hình chữ nhật bán trong suốt bằng trạng thái vừa thêm:

```csharp
using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
{
    var page = pdfDocument.Pages[1];
    var content = new PageContentEditor(page);
    // Begin the graphics state GS0
    content.InsertContent(0, "q /GS0 gs\n"); // Save graphics state and apply GS0
    // Draw a rectangle (100,100) to (300,300)
    content.InsertContent(0, "0.2 0.6 0.8 rg\n"); // Set fill color (light blue)
    content.InsertContent(0, "100 100 200 200 re\n");
    content.InsertContent(0, "f\n"); // Fill rectangle with current fill opacity
    // Restore graphics state
    content.InsertContent(0, "Q\n");
    pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
}
```

**Giải thích** – Toán tử `q` lưu trạng thái đồ họa hiện tại, `/GS0 gs` áp dụng các thiết lập độ trong suốt, hình chữ nhật được vẽ, và `Q` khôi phục trạng thái gốc. Bạn có thể đặt đoạn mã này ở bất kỳ vị trí nào trên trang, trước hoặc sau nội dung hiện có, tùy thuộc vào lớp hình ảnh bạn muốn.

## Những lỗi thường gặp và cách tránh

| Triệu chứng | Nguyên nhân | Cách khắc phục |
|------------|-------------|----------------|
| Độ trong suốt không thay đổi | Trang không có mục ExtGState hoặc nội dung không tham chiếu trạng thái mới. | Kiểm tra `ExtGState` tồn tại và luồng nội dung chứa `/GS0 gs` (hoặc tên bạn đã đặt). |
| Chế độ hòa trộn không có hiệu lực | Sử dụng không gian màu không tương thích hoặc phiên bản PDF không hỗ trợ. | Đảm bảo phiên bản PDF ít nhất là 1.4 (yêu cầu cho độ trong suốt) và không trộn màu spot với chế độ hòa trộn. |
| Tài liệu không mở được trong trình xem cũ | PDF không hỗ trợ độ trong suốt trong phiên bản 1.3 hoặc cũ hơn. | Đặt `pdfDocument.Version = 1.4;` trước khi lưu, hoặc nâng cấp phiên bản PDF một cách rõ ràng. |

## Kiểm tra kết quả

Mở `output.pdf` trong Adobe Acrobat Reader, Foxit, hoặc bất kỳ trình xem PDF hiện đại nào. Bạn sẽ thấy hình chữ nhật được vẽ với độ trong suốt phần tô 50 % trong khi viền vẫn hoàn toàn đục. Sử dụng tùy chọn *Edit → Preferences → Accessibility* để bật “Use high‑contrast colors” và xác nhận hiệu ứng bán trong suốt vẫn tồn tại.

Nếu muốn xác minh bằng mã, Aspose.Pdf cho phép bạn đọc lại trạng thái đồ họa:

```csharp
var gs = pdfDocument.Pages[1].Resources["ExtGState"]["GS0"].ToCosPdfDictionary();
var fillOpacity = ((CosPdfNumber)gs["ca"]).Value; // Should be 0.5
```

## Mở rộng kỹ thuật

* **Nhiều mức độ trong suốt** – Thêm các mục (`"GS1"`, `"GS2"`) với giá trị `ca` khác nhau và tham chiếu chúng khi cần.
* **Các chế độ hòa trộn khác** – Thay `"Normal"` bằng `"Multiply"` hoặc `"Screen"` để tạo lớp phủ nghệ thuật.
* **Áp dụng cho hình ảnh** – Sử dụng cùng một trạng thái đồ họa trước toán tử `Do` vẽ một XObject hình ảnh.

Những biến thể này cho phép bạn xây dựng watermark, làm nổi bật các phần, hoặc tạo thiết kế hình ảnh phức tạp mà không cần raster hoá PDF.

## Kết luận

Bây giờ bạn đã biết **cách thay đổi độ trong suốt PDF** trong C# bằng Aspose.Pdf. Bằng cách tạo một trạng thái đồ họa tùy chỉnh, thêm nó vào từ điển ExtGState của trang, và gọi trạng thái này trong luồng nội dung, bạn có được kiểm soát chi tiết đối với độ trong suốt đường viền và phần tô cũng như chế độ hòa trộn. Ví dụ hoàn chỉnh đã sẵn sàng để sao chép, chạy và điều chỉnh cho bất kỳ kịch bản thao tác PDF nào bạn gặp.

Sẵn sàng cho thử thách tiếp theo? Hãy thử kết hợp kỹ thuật này với **Aspose.Pdf opacity** trên hình ảnh, hoặc khám phá các hiệu ứng **PDF blend mode** để tạo các lớp phủ chuyên nghiệp. Chúc bạn lập trình vui vẻ!

## Bạn nên học gì tiếp theo?

Các hướng dẫn sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong bài viết này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh với giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Change PDF Opacity with Aspose.PDF – Complete C# Guide](/pdf/english/net/programming-with-stamps-and-watermarks/change-pdf-opacity-with-aspose-pdf-complete-c-guide/)
- [Change opacity PDF in C# with Aspose.Pdf – step‑by‑step guide](/pdf/english/net/programming-with-pdf-pages/change-opacity-pdf-in-c-with-aspose-pdf-step-by-step-guide/)
- [How to change PDF transparency in C# using Aspose.Pdf](/pdf/english/net/programming-with-operators/how-to-change-pdf-transparency-in-c-using-aspose-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}