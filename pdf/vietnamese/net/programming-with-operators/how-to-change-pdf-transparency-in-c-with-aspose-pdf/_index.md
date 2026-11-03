---
category: general
date: 2026-10-10
description: Tìm hiểu cách thay đổi độ trong suốt của PDF trong C# bằng Aspose.PDF.
  Hướng dẫn từng bước này bao gồm độ mờ của PDF, chỉnh sửa trạng thái đồ họa và thao
  tác với từ điển ExtGState.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- change PDF transparency
- Aspose.PDF graphics state
- PDF opacity
- C# PDF manipulation
- ExtGState dictionary
language: vi
lastmod: 2026-10-10
og_description: Thay đổi độ trong suốt PDF trong C# với Aspose.PDF. Tham khảo hướng
  dẫn ngắn gọn này để chỉnh sửa độ mờ của PDF, các đối tượng trạng thái đồ họa và
  từ điển ExtGState.
og_image_alt: Screenshot showing C# code that changes PDF transparency using Aspose.PDF
og_title: Thay đổi độ trong suốt PDF trong C# – hướng dẫn đầy đủ Aspose.PDF
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Learn how to change PDF transparency in C# using Aspose.PDF. This step‑by‑step
    guide covers PDF opacity, graphics state editing, and ExtGState dictionary manipulation.
  headline: How to change PDF transparency in C# with Aspose.PDF
  type: TechArticle
tags:
- Aspose.PDF
- C#
- PDF transparency
- Graphics state
title: Cách thay đổi độ trong suốt của PDF trong C# với Aspose.PDF
url: /vi/net/programming-with-operators/how-to-change-pdf-transparency-in-c-with-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách thay đổi độ trong suốt PDF trong C# với Aspose.PDF

Nếu bạn cần **thay đổi độ trong suốt PDF** trong một dự án C#, hướng dẫn này sẽ cung cấp cho bạn một giải pháp hoàn chỉnh, sẵn sàng chạy. Bằng cách chỉnh sửa trạng thái đồ họa (graphics state) của PDF, bạn có thể kiểm soát độ mờ của nét (stroke opacity), độ mờ của phần tô (fill opacity) và chế độ hòa trộn (blend mode) mà không cần tạo lại tài liệu từ đầu.  

Bạn sẽ thấy cách tải PDF, sửa đổi **dictionary ExtGState**, đặt **độ trong suốt PDF** mong muốn và lưu kết quả — tất cả đều sử dụng thư viện Aspose.PDF. Không cần công cụ bên ngoài, và mã hoạt động với .NET 6+.

## Yêu cầu trước

- Visual Studio 2022 (hoặc bất kỳ IDE C# nào)  
- .NET 6 hoặc phiên bản runtime mới hơn  
- Gói NuGet Aspose.PDF for .NET (`Install-Package Aspose.PDF`)  
- Một tệp PDF có tên `input.pdf` trong thư mục bạn kiểm soát  

Có đầy đủ các yếu tố trên sẽ giúp tutorial chạy mà không thiếu phụ thuộc.

## Bước 1: Tải tài liệu PDF

Hoạt động đầu tiên là mở tệp PDF hiện có. Aspose.PDF biểu diễn PDF dưới dạng đối tượng `Document`, cho phép truy cập đầy đủ vào các trang, tài nguyên và các dictionary cấp thấp.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Operators;
using Aspose.Pdf.Text;
using Aspose.Pdf.XObjects;
using Aspose.Pdf.Cosmos;

// Load the source PDF
var document = new Document("YOUR_DIRECTORY/input.pdf");
```

*Lý do quan trọng:* Việc tải tệp tạo ra một mô hình trong bộ nhớ mà bạn có thể chỉnh sửa. Lớp `Document` trừu tượng hoá cấu trúc PDF đồng thời vẫn phơi bày các đối tượng cấp thấp cần thiết để thay đổi độ trong suốt.

## Bước 2: Lấy trang đầu tiên và dictionary tài nguyên của nó

Cài đặt độ trong suốt nằm trong dictionary tài nguyên của trang dưới mục **ExtGState**. Bạn phải lấy dictionary này trước khi có thể thêm hoặc sửa đổi trạng thái đồ họa.

```csharp
// Get the first page (pages are 1‑based)
var page = document.Pages[1];

// The DictionaryEditor simplifies access to resource entries
var resourcesEditor = new DictionaryEditor(page.Resources);
```

*Lý do quan trọng:* Bộ sưu tập `Resources` chứa phông chữ, hình ảnh và trạng thái đồ họa được trang sử dụng. Khi chỉnh sửa nó, bạn chỉ ảnh hưởng đến trang mục tiêu, các trang còn lại không bị thay đổi.

## Bước 3: Truy cập (hoặc tạo) dictionary ExtGState

Nếu PDF đã có một dictionary `ExtGState`, bạn có thể tái sử dụng; nếu không, Aspose.PDF sẽ tạo một dictionary rỗng khi bạn thêm mục đầu tiên.

```csharp
// Retrieve the ExtGState dictionary; create if missing
var extGState = resourcesEditor["ExtGState"]?.ToCosPdfDictionary()
               ?? new CosPdfDictionary(document);
```

*Lý do quan trọng:* Dictionary `ExtGState` lưu trữ **đối tượng trạng thái đồ họa**. Mỗi đối tượng định nghĩa các tham số như độ mờ nét (`CA`), độ mờ phần tô (`ca`) và chế độ hòa trộn (`BM`). Thay đổi các giá trị này trực tiếp ảnh hưởng đến cách PDF hiển thị các phần trong suốt.

## Bước 4: Định nghĩa một trạng thái đồ họa mới với độ trong suốt mong muốn

Tạo một trạng thái đồ họa mới (`GS0`) và đặt các tham số của nó. Ví dụ dưới đây đặt độ mờ nét 100 %, độ mờ phần tô 50 % và chế độ hòa trộn tiêu chuẩn “Normal”.

```csharp
// Name for the new graphics state
string graphicsStateName = "GS0";

// Create an empty dictionary for the graphics state
var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(document);

// Populate the dictionary with transparency parameters
var graphicsStateEntries = new[]
{
    // Stroke opacity (CA) – 1 = fully opaque
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),
    // Fill opacity (ca) – 0.5 = 50 % transparent
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
    // Blend mode (BM) – "Normal" is the most common mode
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
};

foreach (var entry in graphicsStateEntries)
    newGraphicsState.Add(entry);
```

*Lý do quan trọng:* Mục `CA` kiểm soát cách các nét (đường, viền) hòa trộn, trong khi `ca` ảnh hưởng đến phần tô (hình, văn bản). Điều chỉnh các giá trị này là cốt lõi của **việc thay đổi độ trong suốt PDF**. Chế độ hòa trộn quyết định cách nội dung trong suốt tương tác với đồ họa phía dưới.

## Bước 5: Chèn trạng thái đồ họa mới vào dictionary ExtGState

Bây giờ thêm trạng thái đồ họa vào bộ sưu tập `ExtGState` của trang và đảm bảo trang tham chiếu tới nó.

```csharp
// Add the new graphics state to the ExtGState dictionary
extGState.Add(graphicsStateName, newGraphicsState);

// Update the Resources dictionary with the modified ExtGState
resourcesEditor["ExtGState"] = extGState;
```

*Lý do quan trọng:* Thêm mục đăng ký trạng thái đồ họa với PDF. Bất kỳ thao tác vẽ nào sau này chọn `GS0` sẽ sử dụng các giá trị độ trong suốt bạn đã định nghĩa.

## Bước 6: Áp dụng trạng thái đồ họa vào nội dung trang (tùy chọn nhưng thường dùng)

Nếu bạn muốn nội dung hiện có trên trang áp dụng độ trong suốt mới, bạn phải chèn trước một toán tử `gs` để chọn trạng thái đồ họa. Dưới đây là cách đơn giản để chèn toán tử vào đầu nội dung của trang.

```csharp
// Create a content stream that selects the new graphics state
var selectStateOperator = new GraphicsStateOperator(graphicsStateName);

// Insert the operator at the beginning of the page's content
page.Contents.Insert(0, selectStateOperator);
```

*Lý do quan trọng:* Nếu bỏ qua bước này, trạng thái đồ họa tồn tại nhưng không bao giờ được sử dụng. Toán tử `gs` (`GraphicsStateOperator`) báo cho bộ render PDF áp dụng các cài đặt độ trong suốt đã định nghĩa cho mọi thứ phía sau.

## Bước 7: Lưu PDF đã chỉnh sửa

Cuối cùng, ghi tài liệu đã cập nhật ra đĩa.

```csharp
document.Save("YOUR_DIRECTORY/output.pdf");
```

Tệp `output.pdf` sẽ hiển thị với độ trong suốt phần tô bạn chỉ định (50 % trong suốt) trong khi các nét vẫn giữ độ mờ đầy đủ. Thay đổi trực quan này xác nhận rằng bạn đã **thay đổi độ trong suốt PDF** thành công.

---

## Mã nguồn đầy đủ (có thể chạy)

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Cosmos;
using System.Collections.Generic;

class ChangePdfTransparency
{
    static void Main()
    {
        // 1️⃣ Load the PDF
        var document = new Document("YOUR_DIRECTORY/input.pdf");

        // 2️⃣ Get first page and its resource dictionary
        var page = document.Pages[1];
        var resourcesEditor = new DictionaryEditor(page.Resources);

        // 3️⃣ Access (or create) the ExtGState dictionary
        var extGState = resourcesEditor["ExtGState"]?.ToCosPdfDictionary()
                       ?? new CosPdfDictionary(document);

        // 4️⃣ Define a new graphics state (GS0) with desired opacity
        string gsName = "GS0";
        var newGs = CosPdfDictionary.CreateEmptyDictionary(document);
        var entries = new[]
        {
            new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),
            new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
            new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
        };
        foreach (var e in entries) newGs.Add(e);

        // 5️⃣ Add the graphics state to ExtGState and update resources
        extGState.Add(gsName, newGs);
        resourcesEditor["ExtGState"] = extGState;

        // 6️⃣ Apply the graphics state to existing content (optional)
        var gsOperator = new GraphicsStateOperator(gsName);
        page.Contents.Insert(0, gsOperator);

        // 7️⃣ Save the modified PDF
        document.Save("YOUR_DIRECTORY/output.pdf");
    }
}
```

**Kết quả mong đợi:** Mở `output.pdf` trong Adobe Acrobat hoặc bất kỳ trình xem PDF nào sẽ thấy các hình dạng được tô trên trang đầu hiển thị với độ trong suốt 50 %, trong khi các nét vẫn hoàn toàn không trong suốt. Sự thay đổi này chứng minh bạn đã **thay đổi độ trong suốt PDF**.

---

## Các câu hỏi thường gặp và trường hợp đặc biệt

| Câu hỏi | Trả lời |
|----------|--------|
| *Tôi có thể thay đổi độ trong suốt cho một đối tượng cụ thể thay vì toàn bộ trang không?* | Có. Thay vì chèn toán tử `gs` ở đầu trang, hãy đặt nó ngay trước các lệnh vẽ mục tiêu. Dùng `page.Contents.Insert(index, gsOperator)` trong đó `index` chỉ vị trí mong muốn. |
| *Nếu PDF đã có một mục ExtGState có tên “GS0” thì sao?* | Chọn một tên duy nhất (ví dụ `GS1`) hoặc ghi đè mục hiện có nếu bạn muốn thay thế. Khóa trong dictionary phải là duy nhất trong tài nguyên của trang. |
| *Giá trị `ca` có giới hạn từ 0‑1 không?* | Đúng. `ca` (độ trong suốt phần tô) và `CA` (độ trong suốt nét) chấp nhận giá trị từ 0 (hoàn toàn trong suốt) đến 1 (hoàn toàn không trong suốt). Các giá trị ngoài phạm vi này sẽ bị cắt. |
| *Liệu cách này có hoạt động với PDF tuân thủ PDF/A hoặc PDF/X không?* | Việc sửa đổi trạng thái đồ họa có thể phá vỡ tuân thủ nghiêm ngặt. Nếu cần giữ tuân thủ, hãy xác thực đầu ra bằng công cụ kiểm tra PDF/A và điều chỉnh dictionary cho phù hợp (ví dụ, thêm mục `/PDFXConformance`). |
| *Tôi có thể đặt chế độ hòa trộn khác, như “Multiply”?* | Chắc chắn. Thay `new CosPdfName("Normal")` bằng `new CosPdfName("Multiply")` hoặc bất kỳ chế độ hòa trộn nào được định nghĩa trong chuẩn PDF. |

---

## Mẹo và thực hành tốt (E‑E‑A‑T)

- **Mẹo chuyên nghiệp:** Lưu cache dictionary `ExtGState` sau lần sửa đổi đầu tiên nếu bạn dự định chỉnh sửa nhiều trang; điều này giảm tải tạo đối tượng.  
- **Cảnh báo:** Không nên dùng cùng một tên trạng thái đồ họa trên các trang khác nhau mà không cập nhật tài nguyên, vì có thể gây ra việc pha trộn độ trong suốt không mong muốn. Luôn giới hạn tên trong phạm vi trang hoặc dùng định danh toàn cục duy nhất.  
- **Hiệu năng:** Đối với PDF lớn, cân nhắc xử lý các trang song song (`Parallel.ForEach`) nhưng đồng bộ truy cập vào đối tượng `Document` để tránh lỗi thread‑safety.  
- **Kiểm thử:** Xác minh thay đổi độ trong suốt bằng ít nhất hai trình xem (Adobe Acrobat Reader và một plugin PDF trên trình duyệt) vì một số trình xem có cách xử lý chế độ hòa trộn khác nhau.

---

## Kết luận

Bạn đã biết cách **thay đổi độ trong suốt PDF** trong C# bằng cách chỉnh sửa **dictionary ExtGState** với Aspose.PDF. Tutorial đã bao gồm việc tải PDF, tạo trạng thái đồ họa tùy chỉnh, áp dụng nó vào nội dung trang và lưu tệp đã cập nhật.  

Từ đây, bạn có thể khám phá các chủ đề **xử lý PDF bằng C#** nâng cao hơn như xếp lớp nhiều trạng thái đồ họa, áp dụng các giá trị **độ trong suốt PDF** khác nhau cho từng đối tượng, hoặc tích hợp với API cấp cao của Aspose.PDF để chèn văn bản và hình ảnh.

Hãy thử nghiệm các chế độ hòa trộn, mức độ trong suốt khác nhau, hoặc áp dụng trạng thái đồ họa chỉ cho một số trang được chọn. Nếu gặp khó khăn, tài liệu Aspose.PDF cung cấp thông tin chi tiết hơn về mô hình đối tượng PDF và cách xử lý trạng thái đồ họa.

Chúc lập trình vui vẻ!

## Bạn nên học gì tiếp theo?

Các tutorial sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật đã trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm mã mẫu đầy đủ và giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Thay đổi độ trong suốt PDF với Aspose.PDF – Hướng dẫn C# đầy đủ](/pdf/english/net/programming-with-stamps-and-watermarks/change-pdf-opacity-with-aspose-pdf-complete-c-guide/)
- [Thêm độ trong suốt vào PDF với Aspose PDF trong C# – Hướng dẫn từng bước](/pdf/english/net/images-graphics/add-transparency-to-pdf-with-aspose-pdf-in-c-step-by-step-gu/)
- [Thêm độ trong suốt vào PDF bằng Aspose – Hướng dẫn C# đầy đủ](/pdf/english/net/programming-with-operators/add-transparency-to-pdf-using-aspose-complete-c-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}