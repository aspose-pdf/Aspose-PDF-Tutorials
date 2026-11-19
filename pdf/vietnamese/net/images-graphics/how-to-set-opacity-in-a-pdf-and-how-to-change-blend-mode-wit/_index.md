---
category: general
date: 2026-11-19
description: Tìm hiểu cách thiết lập độ trong suốt và cách thay đổi chế độ hòa trộn
  trong PDF bằng Aspose.Pdf. Hướng dẫn C# chi tiết từng bước cho đồ họa trong suốt.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to set opacity
- how to change blend
- Aspose.Pdf graphics state
- PDF transparency C#
- modify PDF resources
language: vi
lastmod: 2026-11-19
og_description: Cách thiết lập độ trong suốt và cách thay đổi chế độ hòa trộn trong
  PDF bằng Aspose.Pdf. Theo dõi hướng dẫn C# đầy đủ này để làm cho đồ họa trở nên
  trong suốt.
og_image_alt: Code editor showing C# example that sets PDF opacity and blend mode
og_title: Cách đặt độ trong suốt và thay đổi chế độ hòa trộn trong PDF bằng Aspose.Pdf
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: Learn how to set opacity and how to change blend mode in a PDF using
    Aspose.Pdf. Step‑by‑step C# guide for transparent graphics.
  headline: How to set opacity in a PDF and how to change blend mode with Aspose.Pdf
  type: TechArticle
tags:
- Aspose.Pdf
- C#
- PDF manipulation
- Transparency
title: Cách đặt độ trong suốt trong PDF và cách thay đổi chế độ hòa trộn với Aspose.Pdf
url: /vi/net/images-graphics/how-to-set-opacity-in-a-pdf-and-how-to-change-blend-mode-wit/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách đặt độ trong suốt và cách thay đổi chế độ hòa trộn trong PDF với Aspose.Pdf

Nếu bạn cần **cách đặt độ trong suốt** cho các đối tượng trong PDF, hướng dẫn này sẽ chỉ ra các bước cụ thể. Nó cũng bao gồm **cách thay đổi chế độ hòa trộn** để trạng thái đồ họa mới hòa trộn đúng với nội dung trang.

Trong tutorial này bạn sẽ:

* Tải một PDF hiện có bằng Aspose.Pdf.
* Truy cập từ điển tài nguyên của trang.
* Tạo một từ điển trạng thái đồ họa mới định nghĩa độ trong suốt nét vẽ, độ trong suốt tô và chế độ hòa trộn.
* Thêm trạng thái đồ họa vào bộ sưu tập `ExtGState`.
* Lưu PDF đã cập nhật.

Không cần công cụ bên ngoài—chỉ cần thư viện Aspose.Pdf cho .NET và môi trường phát triển .NET.

## Yêu cầu trước

* .NET 6.0 trở lên (mã cũng hoạt động với .NET Framework 4.6+).
* Gói NuGet Aspose.Pdf cho .NET (`Install-Package Aspose.Pdf`).
* Tệp PDF có tên `input.pdf` nằm trong thư mục có quyền ghi (thay thế `YOUR_DIRECTORY` bằng đường dẫn thực tế của bạn).

## Bước 1: Cài đặt Aspose.Pdf và thiết lập dự án

Tạo một dự án console mới và thêm tham chiếu Aspose.Pdf:

```bash
dotnet new console -n PdfOpacityDemo
cd PdfOpacityDemo
dotnet add package Aspose.Pdf
```

Tệp dự án bây giờ đã bao gồm assembly Aspose.Pdf, cung cấp các lớp `Document`, `DictionaryEditor` và `CosPdfDictionary` được sử dụng sau này.

## Bước 2: Tải tài liệu PDF

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Engine;
using Aspose.Pdf.Engine.Data;

// Load the existing PDF
Document pdfDocument = new Document(@"YOUR_DIRECTORY\input.pdf");
```

**Tại sao điều này quan trọng:** Việc tải tài liệu tạo ra một biểu diễn trong bộ nhớ mà bạn có thể chỉnh sửa. Nếu bỏ qua bước này, các từ điển tài nguyên sẽ không thể truy cập được.

## Bước 3: Lấy trang đầu tiên và từ điển tài nguyên của nó

```csharp
// Retrieve the first page (pages are 1‑based)
Page firstPage = pdfDocument.Pages[1];

// Open the page’s resource dictionary for editing
DictionaryEditor resourceEditor = new DictionaryEditor(firstPage.Resources);
```

**Giải thích:** Từ điển `Resources` chứa các đối tượng như phông chữ, hình ảnh và bộ sưu tập `ExtGState`. Việc chỉnh sửa nó cho phép bạn chèn các trạng thái đồ họa mới kiểm soát độ trong suốt và hòa trộn.

## Bước 4: Truy cập (hoặc tạo) từ điển ExtGState

```csharp
// Try to get the existing ExtGState dictionary; create it if missing
CosPdfDictionary extGStateDict = null;
if (resourceEditor.ContainsKey("ExtGState"))
{
    extGStateDict = resourceEditor["ExtGState"].ToCosPdfDictionary();
}
else
{
    // Create an empty ExtGState dictionary and add it to resources
    extGStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
    resourceEditor["ExtGState"] = extGStateDict;
}
```

**Tại sao bước này cần thiết:** Mục `ExtGState` chứa các đối tượng trạng thái đồ họa. Nếu nó không tồn tại, bạn phải tạo nó trước khi thêm các mục mới.

## Bước 5: Tạo một trạng thái đồ họa mới với độ trong suốt và chế độ hòa trộn

```csharp
// Create a new empty graphics state dictionary
CosPdfDictionary newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

// Set stroke opacity (CA) – 1 = fully opaque, 0 = fully transparent
newGraphicsState.Add("CA", new CosPdfNumber(1));

// Set fill opacity (ca) – 0.5 = 50 % transparent fill
newGraphicsState.Add("ca", new CosPdfNumber(0.5));

// Set blend mode (BM) – "Normal" is the default; other options: Multiply, Screen, Overlay, etc.
newGraphicsState.Add("BM", new CosPdfName("Normal"));
```

**Cách giải quyết vấn đề:**  
* `CA` kiểm soát độ trong suốt của các đường viền (ví dụ: các đường thẳng).  
* `ca` kiểm soát độ trong suốt của các hình dạng được tô (ví dụ: hình chữ nhật).  
* `BM` xác định cách các đồ họa mới được hợp thành với nội dung trang hiện có. Thay đổi chế độ hòa trộn chính là **cách thay đổi hòa trộn** cho PDF.

## Bước 6: Đăng ký trạng thái đồ họa vào bộ sưu tập ExtGState

```csharp
// Use a unique key for the new graphics state (e.g., GS0)
extGStateDict.Add("GS0", newGraphicsState);
```

Bây giờ trang có thể tham chiếu trạng thái đồ họa này bằng tên `/GS0`. Bất kỳ nội dung nào đặt `/GS0 gs` sẽ sử dụng độ trong suốt và chế độ hòa trộn đã định nghĩa.

## Bước 7: Áp dụng trạng thái đồ họa vào nội dung hiện có (tùy chọn)

Nếu bạn muốn sửa đổi các lệnh vẽ hiện có, bạn có thể chèn trước toán tử trạng thái đồ họa vào luồng nội dung của trang:

```csharp
// Retrieve the content stream as a string
string pageContent = firstPage.Contents[1].ToString();

// Prepend the graphics state operator
string modifiedContent = "GS0 gs\n" + pageContent;

// Replace the original content
firstPage.Contents[1].Replace(modifiedContent);
```

**Lưu ý:** Bước này là tùy chọn. Nếu bạn thêm các lệnh vẽ mới sau này, chỉ cần bắt đầu luồng bằng `GS0 gs`.

## Bước 8: Lưu PDF đã chỉnh sửa

```csharp
pdfDocument.Save(@"YOUR_DIRECTORY\out.pdf");
```

Tệp `out.pdf` kết quả chứa một trạng thái đồ họa trong đó độ trong suốt tô là 50 % và chế độ hòa trộn là `Normal`. Bất kỳ nội dung nào sử dụng `/GS0 gs` sẽ hiển thị với độ trong suốt đã chỉ định.

## Ví dụ hoàn chỉnh hoạt động

Dưới đây là chương trình đầy đủ mà bạn có thể sao chép‑dán vào `Program.cs` và chạy:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Engine;
using Aspose.Pdf.Engine.Data;

class Program
{
    static void Main()
    {
        // 1. Load the PDF document
        Document pdfDocument = new Document(@"YOUR_DIRECTORY\input.pdf");

        // 2. Get the first page and its resource dictionary
        Page firstPage = pdfDocument.Pages[1];
        DictionaryEditor resourceEditor = new DictionaryEditor(firstPage.Resources);

        // 3. Access or create the ExtGState dictionary
        CosPdfDictionary extGStateDict;
        if (resourceEditor.ContainsKey("ExtGState"))
        {
            extGStateDict = resourceEditor["ExtGState"].ToCosPdfDictionary();
        }
        else
        {
            extGStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            resourceEditor["ExtGState"] = extGStateDict;
        }

        // 4. Define a new graphics state with opacity and blend mode
        CosPdfDictionary newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
        newGraphicsState.Add("CA", new CosPdfNumber(1));          // Stroke opacity (fully opaque)
        newGraphicsState.Add("ca", new CosPdfNumber(0.5));        // Fill opacity (50 % transparent)
        newGraphicsState.Add("BM", new CosPdfName("Normal"));    // Blend mode (Normal)

        // 5. Add the graphics state to ExtGState collection
        extGStateDict.Add("GS0", newGraphicsState);

        // 6. (Optional) Apply the graphics state to existing page content
        if (firstPage.Contents.Count > 0)
        {
            string original = firstPage.Contents[1].ToString();
            string withGs = "GS0 gs\n" + original;
            firstPage.Contents[1].Replace(withGs);
        }

        // 7. Save the updated PDF
        pdfDocument.Save(@"YOUR_DIRECTORY\out.pdf");

        Console.WriteLine("PDF updated successfully – opacity set and blend mode changed.");
    }
}
```

### Kết quả mong đợi

Chạy chương trình sẽ in:

```
PDF updated successfully – opacity set and blend mode changed.
```

Khi bạn mở `out.pdf` trong trình xem PDF, bất kỳ hình dạng nào sử dụng trạng thái đồ họa mới định nghĩa sẽ hiển thị với độ trong suốt tô 50 % trong khi các nét vẽ vẫn hoàn toàn không trong suốt. Chế độ hòa trộn `Normal` đảm bảo các đồ họa được hợp thành mà không có hiệu ứng đặc biệt. Bạn có thể thay đổi `"Normal"` thành `"Multiply"` hoặc `"Screen"` để xem **cách thay đổi hòa trộn** cho các kết quả hình ảnh khác nhau.

## Các câu hỏi thường gặp và trường hợp đặc biệt

| Question | Answer |
|----------|--------|
| **Tôi có thể đặt các giá trị độ trong suốt khác nhau cho nhiều đối tượng không?** | Có. Tạo các trạng thái đồ họa bổ sung (ví dụ: `GS1`, `GS2`) với các giá trị `ca`/`CA` khác nhau và tham chiếu tên phù hợp trước khi vẽ mỗi đối tượng. |
| **Nếu PDF đã chứa mục `ExtGState` có tên `GS0` thì sao?** | Chọn một khóa duy nhất (`GS1`, `MyOpacityState`, v.v.) hoặc ghi đè mục hiện có nếu định nghĩa cũ không còn cần thiết. |
| **Chế độ hòa trộn có bị giới hạn ở `Normal` không?** | Không. Các tên hợp lệ bao gồm `Multiply`, `Screen`, `Overlay`, `Darken`, `Lighten`, `ColorDodge`, `ColorBurn`, `HardLight`, `SoftLight`, `Difference`, `Exclusion`, và `Hue`, `Saturation`, `Color`, `Luminosity`. |
| **Điều này có hoạt động với PDF được mã hóa không?** | Aspose.Pdf có thể mở các PDF được mã hóa nếu bạn cung cấp mật khẩu qua `Document(string, LoadOptions)`. Việc thao tác trạng thái đồ họa hoạt động tương tự sau khi giải mã. |
| **Các thay đổi sẽ ảnh hưởng tới tất cả các trang không?** | Ví dụ chỉ sửa đổi trang đầu tiên. Để ảnh hưởng tới mọi trang, hãy lặp qua `pdfDocument.Pages` và lặp lại các bước 2‑6 cho mỗi trang. |

## Mẹo chuyên nghiệp

* **Tái sử dụng trạng thái đồ họa:** Thêm một trạng thái đồ họa một lần và tham chiếu nó trên nhiều trang sẽ giảm kích thước tệp.
* **Hiệu năng:** Việc chỉnh sửa các PDF lớn trong bộ nhớ có thể tốn nhiều bộ nhớ. Sử dụng `pdfDocument.Save(..., SaveOptions)` với cập nhật tăng dần nếu bạn chỉ cần thay đổi nhỏ.
* **Kiểm tra chế độ hòa trộn:** Không phải tất cả các trình xem PDF đều hiển thị mỗi chế độ hòa trộn một cách giống nhau. Kiểm tra kết quả trong Adobe Acrobat Reader và một trình xem thay thế (ví dụ: Foxit) để xác nhận tính nhất quán về hình ảnh.

## Kết luận

Bạn giờ đã biết **cách đặt độ trong suốt** và **cách thay đổi chế độ hòa trộn** trong PDF bằng Aspose.Pdf cho .NET. Bằng cách chỉnh sửa từ điển `ExtGState`, bạn có được kiểm soát chi tiết về độ trong suốt và hợp thành, cho phép tạo đồ họa PDF chất lượng chuyên nghiệp mà không cần công cụ bên ngoài.

Tiếp theo, bạn có thể khám phá:

* Thêm hình ảnh với nền trong suốt (`cách đặt độ trong suốt` cho hình ảnh).
* Tạo các luồng nội dung có thể tái sử dụng tham chiếu tới trạng thái đồ họa mới.
* Sử dụng các chế độ hòa trộn khác (`cách thay đổi hòa trộn` thành `Multiply` hoặc `Screen`) để tạo hiệu ứng sáng tạo.

Chúc lập trình vui vẻ, và tận hưởng việc làm cho PDF của bạn trở nên sinh động hơn!

## Bạn Nên Học Gì Tiếp Theo?

Các hướng dẫn sau đây bao gồm các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên đều có các ví dụ mã hoàn chỉnh với giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [How to Change Opacity in PDF with Aspose.PDF – Complete Guide](/pdf/english/net/programming-with-stamps-and-watermarks/how-to-change-opacity-in-pdf-with-aspose-pdf-complete-guide/)
- [How to change opacity in a PDF with Aspose.Pdf for .NET](/pdf/english/net/images-graphics/how-to-change-opacity-in-a-pdf-with-aspose-pdf-for-net/)
- [How to change PDF transparency using Aspose.Pdf in C#](/pdf/english/net/programming-with-operators/how-to-change-pdf-transparency-using-aspose-pdf-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}