---
category: general
date: 2026-09-18
description: Học cách tạo từ điển PDF trống trong C# bằng Aspose.PDF. Hướng dẫn từng
  bước này bao gồm ExtGState, trạng thái đồ họa và thao tác CosPdfDictionary.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create empty PDF dictionary
- Aspose.PDF
- ExtGState dictionary
- graphics state
- CosPdfDictionary
- PDF manipulation C#
language: vi
lastmod: 2026-09-18
og_description: Tạo từ điển PDF trống trong C# với Aspose.PDF. Theo dõi hướng dẫn
  toàn diện này để chỉnh sửa ExtGState và các từ điển trạng thái đồ họa.
og_image_alt: Screenshot showing creation of an empty PDF dictionary in C#
og_title: Tạo từ điển PDF trống trong C# – hướng dẫn đầy đủ Aspose.PDF
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: Learn to create empty PDF dictionary in C# using Aspose.PDF. This step‑by‑step
    guide covers ExtGState, graphics state, and CosPdfDictionary manipulation.
  headline: How to create empty PDF dictionary with Aspose.PDF in C#
  type: TechArticle
tags:
- PDF
- C#
- Aspose.PDF
title: Cách tạo từ điển PDF trống bằng Aspose.PDF trong C#
url: /vi/net/programming-with-document/how-to-create-empty-pdf-dictionary-with-aspose-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách tạo từ điển PDF trống với Aspose.PDF trong C#

Nếu bạn cần **tạo từ điển PDF trống** khi xử lý tệp PDF, hướng dẫn này sẽ chỉ cho bạn cách thực hiện chính xác bằng Aspose.PDF cho .NET. Dù bạn đang điều chỉnh độ trong suốt, chế độ hòa trộn, hay bất kỳ trạng thái đồ họa tùy chỉnh nào, các bước dưới đây sẽ giúp bạn chỉnh sửa từ điển `ExtGState` một cách an toàn và hiệu quả.

Trong tutorial này bạn sẽ học:

* Tải tài liệu PDF bằng Aspose.PDF.
* Truy cập tài nguyên của trang đầu tiên và từ điển `ExtGState` hiện có.
* Xây dựng một `CosPdfDictionary` trống mới và điền các mục trạng thái đồ họa.
* Lưu PDF đã chỉnh sửa mà không mất bất kỳ nội dung gốc nào.

Giải pháp này hoạt động với bất kỳ PDF nào có ít nhất một trang và chỉ yêu cầu thư viện Aspose.PDF (phiên bản 23.10 trở lên).

## Yêu cầu trước

* .NET 6.0 hoặc mới hơn (mã cũng chạy trên .NET Framework 4.8).
* Tham chiếu tới gói NuGet **Aspose.PDF**.
* Tệp PDF đầu vào nằm tại `YOUR_DIRECTORY/input.pdf`.
* Kiến thức cơ bản về C# và các khái niệm PDF như tài nguyên và trạng thái đồ họa.

> **Pro tip:** Khi làm việc với các PDF lớn, bao bọc đối tượng `Document` trong một khối `using` để đảm bảo tất cả các handle tệp được giải phóng kịp thời.

## Bước 1: Tải tài liệu PDF

Hoạt động đầu tiên mở tệp nguồn. Aspose.PDF đọc toàn bộ tài liệu vào bộ nhớ, cho phép bạn chỉnh sửa các đối tượng nội bộ.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Step 1: Load the PDF document
using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
{
    // Subsequent steps go here
}
```

*Lý do quan trọng*: Việc tải tài liệu tạo ra một mô hình đối tượng có thể thay đổi. Nếu bỏ qua bước này, bạn sẽ không thể truy cập tài nguyên trang cần thiết để thao tác với từ điển.

## Bước 2: Lấy tài nguyên của trang đầu tiên

Mỗi trang lưu trữ một từ điển `Resources` chứa phông chữ, hình ảnh và trạng thái đồ họa. Truy cập nó sẽ cung cấp cho bạn một `DictionaryEditor` giúp đơn giản hoá các thao tác đọc/ghi.

```csharp
// Step 2: Get the resources of the first page
Page firstPage = pdfDocument.Pages[1];
DictionaryEditor resourcesEditor = new DictionaryEditor(firstPage.Resources);
```

*Lý do quan trọng*: Từ điển `ExtGState` nằm bên trong tài nguyên trang. Chỉnh sửa sai từ điển sẽ không ảnh hưởng tới việc hiển thị.

## Bước 3: Xác định từ điển ExtGState hiện có

Mục `ExtGState` có thể đã chứa các đối tượng trạng thái đồ họa. Chúng ta sẽ lấy nó dưới dạng `CosPdfDictionary` để có thể thêm các mục mới.

```csharp
// Step 3: Access the existing ExtGState dictionary
CosPdfDictionary extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
```

Nếu mục `ExtGState` không tồn tại, Aspose.PDF sẽ tự động tạo một từ điển trống khi bạn gán một đối tượng mới sau này.

## Bước 4: **Tạo từ điển PDF trống** cho một trạng thái đồ họa mới

Ở đây chúng ta xây dựng một `CosPdfDictionary` hoàn toàn mới — trung tâm của thao tác **tạo từ điển PDF trống**. Sau đó chúng ta điền các khóa trạng thái đồ họa tiêu chuẩn:

* `CA` – độ trong suốt nét vẽ.
* `ca` – độ trong suốt tô đầy.
* `BM` – chế độ hòa trộn.

```csharp
// Step 4: Create a new graphics state dictionary and define its entries
CosPdfDictionary graphicsStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

KeyValuePair<string, ICosPdfPrimitive>[] graphicsStateEntries = new[]
{
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),          // Stroke opacity
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),       // Fill opacity
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))    // Blend mode
};

foreach (var entry in graphicsStateEntries)
    graphicsStateDict.Add(entry);
```

*Lý do quan trọng*: Bằng cách định nghĩa rõ ràng từng mục, bạn kiểm soát cách các đối tượng trên trang hòa trộn và hiển thị. Từ điển **trống** cho đến khi bạn thêm các khóa này, đáp ứng yêu cầu **tạo từ điển PDF trống** trước khi điền nội dung.

## Bước 5: Thêm trạng thái đồ họa mới vào từ điển ExtGState

Mỗi trạng thái đồ họa phải có một tên duy nhất (ví dụ, `GS0`). Chúng ta chèn từ điển vừa tạo dưới tên đó.

```csharp
// Step 5: Add the new graphics state to the ExtGState dictionary with a unique name
extGStateDict.Add("GS0", graphicsStateDict);
```

Nếu bạn cần nhiều trạng thái, hãy tiếp tục thêm các mục như `GS1`, `GS2`, v.v., đảm bảo mỗi tên là duy nhất trong từ điển `ExtGState`.

## Bước 6: Lưu tài liệu PDF đã cập nhật

Cuối cùng, ghi các thay đổi trở lại đĩa. Tệp gốc vẫn không bị thay đổi vì chúng ta lưu vào một đường dẫn mới.

```csharp
// Step 6: Save the updated PDF document
pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
}
```

Tệp `output.pdf` hiện chứa một trạng thái đồ họa bổ sung (`GS0`) mà bạn có thể tham chiếu từ bất kỳ luồng nội dung trang nào bằng toán tử `/GS0`.

## Ví dụ hoàn chỉnh

Kết hợp tất cả các bước lại sẽ tạo ra một chương trình tự chứa mà bạn có thể chạy ngay lập tức.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;

class Program
{
    static void Main()
    {
        // Load the source PDF
        using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
        {
            // Access first page resources
            Page firstPage = pdfDocument.Pages[1];
            DictionaryEditor resourcesEditor = new DictionaryEditor(firstPage.Resources);

            // Get (or create) ExtGState dictionary
            CosPdfDictionary extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();

            // Build a new empty PDF dictionary for graphics state
            CosPdfDictionary graphicsStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            var entries = new[]
            {
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
            };
            foreach (var entry in entries)
                graphicsStateDict.Add(entry);

            // Insert the new graphics state with a unique name
            extGStateDict.Add("GS0", graphicsStateDict);

            // Save the modified document
            pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
        }

        Console.WriteLine("PDF updated successfully.");
    }
}
```

**Kết quả mong đợi**: Sau khi chạy chương trình, `output.pdf` chứa cùng nội dung hình ảnh như `input.pdf`. Kiểm tra PDF bằng công cụ như Adobe Acrobat hoặc PDF‑Tron sẽ hiển thị một mục mới `GS0` trong từ điển `ExtGState` của trang đầu tiên.

## Các biến thể phổ biến và trường hợp đặc biệt

| Tình huống | Cần điều chỉnh |
|-----------|----------------|
| **Không có mục ExtGState hiện có** | Thay `resourcesEditor["ExtGState"]` bằng `new CosPdfDictionary(pdfDocument)` và gán lại cho `firstPage.Resources["ExtGState"]`. |
| **Nhiều trang cần cùng một trạng thái** | Thêm mục `GS0` vào mỗi từ điển `ExtGState` của các trang, hoặc tham chiếu từ điển từ một đối tượng tài nguyên chung. |
| **Chế độ hòa trộn khác** | Thay giá trị `CosPdfName` từ `"Normal"` thành `"Multiply"`, `"Screen"`,... tùy theo hiệu ứng mong muốn. |
| **Giá trị độ trong suốt cao hơn** | Dùng `new CosPdfNumber(0.8)` cho `ca` hoặc `CA` để tăng độ trong suốt tô đầy hoặc nét vẽ. |
| **Sử dụng toán tử stream** | Trong luồng nội dung, viết `"/GS0 gs"` trước các thao tác vẽ để áp dụng trạng thái đồ họa mới. |

## Các lưu ý về hiệu năng

* **Tiêu thụ bộ nhớ** – Tải một PDF rất lớn sẽ tiêu tốn bộ nhớ tỷ lệ với số trang. Nếu bạn chỉ cần chỉnh sửa trang đầu, cân nhắc sử dụng `pdfDocument.Pages.Delete(pageNumber)` sau khi xử lý để giải phóng tài nguyên.
* **An toàn đa luồng** – Các đối tượng Aspose.PDF không hỗ trợ đa luồng. Thực hiện các chỉnh sửa từ điển trên một luồng duy nhất hoặc tạo các thể hiện `Document` riêng cho mỗi luồng.

## Kết luận

Bây giờ bạn đã biết cách **tạo từ điển PDF trống** với Aspose.PDF, điền chúng bằng các mục trạng thái đồ họa, và gắn chúng vào từ điển `ExtGState` của một trang. Kỹ thuật này cho phép bạn kiểm soát chi tiết độ trong suốt, chế độ hòa trộn và các tham số hiển thị khác trực tiếp từ C#.

Tiếp theo, khám phá các chủ đề liên quan như **PDF manipulation C#**, thêm các mục **ExtGState dictionary** tùy chỉnh cho các hiệu ứng trong suốt nâng cao, hoặc sử dụng **CosPdfDictionary** để chỉnh sửa các loại tài nguyên khác như phông chữ hoặc XObject. Thử nghiệm với nhiều trạng thái đồ họa để xây dựng các hiệu ứng hình ảnh tinh vi trong PDF của bạn.


## Bạn Nên Học Gì Tiếp Theo?


Các tutorial sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật đã trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh với giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Create & Fill Rectangles in PDFs Using Aspose.PDF for .NET&#58; A Step-by-Step Guide](/pdf/english/net/images-graphics/create-fill-rectangle-aspose-pdf-net/)
- [How to Create Dashed Lines in PDFs Using Aspose.PDF for .NET&#58; A Step-by-Step Guide](/pdf/english/net/images-graphics/create-dashed-lines-aspose-pdf-net/)
- [How to Add an Empty Page at the End of a PDF Using Aspose.PDF for .NET | Step-by-Step Guide](/pdf/english/net/document-manipulation/add-empty-page-end-pdf-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}