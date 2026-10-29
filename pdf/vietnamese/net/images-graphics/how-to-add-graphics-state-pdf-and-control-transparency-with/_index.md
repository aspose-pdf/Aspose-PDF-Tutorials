---
category: general
date: 2026-09-05
description: Tìm hiểu cách thêm trạng thái đồ họa PDF bằng Aspose.PDF để thiết lập
  độ trong suốt. Hướng dẫn từng bước này cũng chỉ cách thêm độ trong suốt vào PDF
  và chỉnh sửa độ trong suốt của PDF một cách hiệu quả.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add graphics state pdf
- how to add transparency pdf
- modify pdf transparency
language: vi
lastmod: 2026-09-05
og_description: Thêm trạng thái đồ họa PDF bằng Aspose.PDF. Theo dõi hướng dẫn này
  để học cách thêm độ trong suốt cho PDF và chỉnh sửa độ trong suốt của PDF chỉ trong
  vài dòng mã C#.
og_image_alt: Screenshot of C# code that adds graphics state pdf to a PDF document
og_title: Thêm trạng thái đồ họa PDF với Aspose.PDF – kiểm soát độ trong suốt trong
  C#
schemas:
- author: Aspose
  dateModified: '2026-09-05'
  description: Learn how to add graphics state pdf using Aspose.PDF to set transparency.
    This step‑by‑step guide also shows how to add transparency pdf and modify pdf
    transparency efficiently.
  headline: How to add graphics state pdf and control transparency with Aspose.PDF
  type: TechArticle
tags:
- Aspose.PDF
- PDF graphics state
- PDF transparency
- C# PDF manipulation
title: Cách thêm trạng thái đồ họa PDF và kiểm soát độ trong suốt với Aspose.PDF
url: /vi/net/images-graphics/how-to-add-graphics-state-pdf-and-control-transparency-with/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách thêm graphics state pdf và kiểm soát độ trong suốt với Aspose.PDF

Nếu bạn cần **add graphics state pdf** vào một tài liệu hiện có, hướng dẫn này sẽ chỉ cho bạn các bước chính xác. Bạn sẽ thấy cách **add transparency pdf** bằng Aspose.PDF cho .NET, và cách chỉnh sửa **pdf transparency** mà không làm hỏng bố cục gốc.

Trong các phần sau, chúng ta sẽ đi qua một ví dụ hoàn chỉnh, có thể chạy được, giải thích lý do mỗi dòng quan trọng, và thảo luận các lỗi thường gặp. Khi kết thúc, bạn sẽ có thể nhúng các graphics state tùy chỉnh—như giá trị alpha cho stroke và fill—vào bất kỳ trang PDF nào.

## Prerequisites

Trước khi bắt đầu, hãy chắc chắn rằng bạn có:

* .NET 6.0 hoặc mới hơn (mã cũng hoạt động với .NET Framework 4.7+)
* Giấy phép Aspose.PDF for .NET hợp lệ hoặc khóa đánh giá tạm thời
* Visual Studio 2022 (hoặc bất kỳ trình soạn thảo C# nào bạn thích)
* Một tệp PDF đầu vào (`input.pdf`) mà bạn có quyền sửa đổi

Không cần bất kỳ gói NuGet bổ sung nào ngoài `Aspose.Pdf`.

## Step 1: Load the PDF document

Hoạt động đầu tiên là mở PDF nguồn. Aspose.PDF bọc tệp trong một đối tượng `Document`, cho phép bạn truy cập các trang, tài nguyên và cấu trúc PDF mức thấp.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Generator;
using Aspose.Pdf.Operators;
using Aspose.Pdf.Text;
using Aspose.Pdf.Xmp;

string inputPath = @"YOUR_DIRECTORY\input.pdf";

// Open the document inside a using block so resources are released automatically.
using (var doc = new Document(inputPath))
{
    // The rest of the code lives inside this block.
}
```

**Tại sao điều này quan trọng:** Mở tệp bằng câu lệnh `using` đảm bảo rằng handle của tệp được đóng ngay cả khi có ngoại lệ xảy ra. Đối tượng `Document` cũng tải bảng tham chiếu chéo, cho phép chúng ta chỉnh sửa các dictionary mức thấp sau này.

## Step 2: Access the first page’s resource dictionary

Mỗi trang PDF có một dictionary *Resources* lưu trữ fonts, XObjects và graphics states (`ExtGState`). Để chèn một graphics state mới, trước tiên chúng ta lấy dictionary này.

```csharp
// Inside the using block
Page page = doc.Pages[1];                     // Get the first page (pages are 1‑based)
var dictEditor = new DictionaryEditor(page.Resources);
var extGState = dictEditor["ExtGState"].ToCosPdfDictionary();
```

**Tại sao điều này quan trọng:** `ExtGState` là khóa mà dưới đó các đối tượng graphics state được lưu. Nếu trang chưa chứa mục `ExtGState`, Aspose.PDF sẽ tự động tạo một dictionary rỗng, vì vậy mã sẽ hoạt động trong cả hai trường hợp.

## Step 3: Create a new graphics state dictionary

Một graphics state dictionary định nghĩa cách các thao tác vẽ hoạt động. Đối với độ trong suốt, chúng ta cần `CA` (stroke alpha), `ca` (fill alpha), và tùy chọn chế độ hòa trộn (`BM`). Đoạn mã dưới đây xây dựng dictionary đó.

```csharp
// Create an empty COS dictionary that will become our new graphics state.
CosPdfDictionary newGs = CosPdfDictionary.CreateEmptyDictionary(doc);

// Define the entries we want: 1.0 stroke opacity, 0.5 fill opacity, Normal blend mode.
var entries = new[]
{
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),   // stroke alpha (fully opaque)
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),   // fill alpha (50 % transparent)
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // blend mode
};

foreach (var entry in entries)
{
    newGs.Add(entry);
}
```

**Tại sao điều này quan trọng:**  
* `CA` điều khiển độ mờ của các đường viền (stroke).  
* `ca` điều khiển độ mờ của các đối tượng được tô (fill).  
* `BM` chọn chế độ hòa trộn; “Normal” là phổ biến nhất và hoạt động với mọi trình xem PDF.

### Edge case: missing `ExtGState` entry

Nếu `page.Resources` không chứa dictionary `ExtGState`, `dictEditor["ExtGState"]` sẽ trả về `null`. Trong trường hợp đó, bạn có thể tạo nó thủ công:

```csharp
if (extGState == null)
{
    extGState = CosPdfDictionary.CreateEmptyDictionary(doc);
    dictEditor["ExtGState"] = extGState;
}
```

Thêm kiểm tra này làm cho tutorial trở nên vững chắc hơn đối với các PDF chưa từng sử dụng graphics state tùy chỉnh.

## Step 4: Add the new graphics state to the resource dictionary

Bây giờ chúng ta gắn dictionary vừa tạo vào một tên (ví dụ, `GS0`). Các luồng nội dung có thể tham chiếu tên này để áp dụng độ trong suốt đã định nghĩa.

```csharp
// Register the new graphics state under the name "GS0"
extGState.Add("GS0", newGs);
```

**Tại sao điều này quan trọng:** Các toán tử nội dung PDF như `gs` chuyển sang một graphics state có tên. Bằng cách thêm `GS0`, bạn cho phép các luồng nội dung sau này sử dụng ` /GS0 gs ` để kích hoạt các cài đặt trong suốt.

## Step 5: (Optional) Apply the graphics state to existing content

Nếu bạn muốn các phần tử hiện có trên trang hiện tại trở nên trong suốt, có thể chèn một toán tử `gs` vào đầu luồng nội dung của trang. Bước này là tùy chọn vì nhiều trường hợp chỉ cần graphics state cho các đối tượng mới được thêm vào.

```csharp
// Prepend "GS0" graphics state to the page’s content
page.Contents.Insert(0, new OperatorGraphicsState("GS0"));
```

**Tại sao điều này quan trọng:** Nếu không có dòng này, trang sẽ giữ nguyên giao diện gốc. Thêm toán tử đảm bảo mọi thứ được vẽ sau toán tử sẽ kế thừa các giá trị opacity mới.

## Step 6: Save the modified PDF

Cuối cùng, ghi tài liệu đã cập nhật ra đĩa. Bạn có thể ghi đè lên tệp gốc hoặc lưu vào vị trí mới.

```csharp
string outputPath = @"YOUR_DIRECTORY\output.pdf";
doc.Save(outputPath);
```

**Tại sao điều này quan trọng:** `doc.Save` tuần tự hoá bảng tham chiếu chéo đã chỉnh sửa, các dictionary tài nguyên, và bất kỳ luồng nội dung mới nào, tạo ra một PDF hợp lệ mà bất kỳ trình xem nào cũng có thể mở.

## Full working example

Kết hợp tất cả các phần lại, dưới đây là một chương trình tự chứa mà bạn có thể sao chép, dán và chạy.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Operators;
using Aspose.Pdf.Xmp;
using Aspose.Pdf.Text;
using Aspose.Pdf.Generator;
using Aspose.Pdf.Cos;

class AddGraphicsStateExample
{
    static void Main()
    {
        // -----------------------------------------------------------------
        // 1️⃣ Load the PDF document
        // -----------------------------------------------------------------
        string inputPath = @"YOUR_DIRECTORY\input.pdf";
        using (var doc = new Document(inputPath))
        {
            // -----------------------------------------------------------------
            // 2️⃣ Access the first page's resource dictionary
            // -----------------------------------------------------------------
            Page page = doc.Pages[1];
            var dictEditor = new DictionaryEditor(page.Resources);
            var extGState = dictEditor["ExtGState"]?.ToCosPdfDictionary();

            // Ensure ExtGState exists
            if (extGState == null)
            {
                extGState = CosPdfDictionary.CreateEmptyDictionary(doc);
                dictEditor["ExtGState"] = extGState;
            }

            // -----------------------------------------------------------------
            // 3️⃣ Create a new graphics state (transparency settings)
            // -----------------------------------------------------------------
            CosPdfDictionary newGs = CosPdfDictionary.CreateEmptyDictionary(doc);
            var entries = new[]
            {
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),   // stroke opacity
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),   // fill opacity
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
            };
            foreach (var entry in entries) newGs.Add(entry);

            // -----------------------------------------------------------------
            // 4️⃣ Register the graphics state as "GS0"
            // -----------------------------------------------------------------
            extGState.Add("GS0", newGs);

            // -----------------------------------------------------------------
            // 5️⃣ (Optional) Apply the graphics state to existing content
            // -----------------------------------------------------------------
            page.Contents.Insert(0, new OperatorGraphicsState("GS0"));

            // -----------------------------------------------------------------
            // 6️⃣ Save the modified PDF
            // -----------------------------------------------------------------
            string outputPath = @"YOUR_DIRECTORY\output.pdf";
            doc.Save(outputPath);
            Console.WriteLine($"PDF saved with new graphics state at: {outputPath}");
        }
    }
}
```

### Expected output

Sau khi chạy chương trình, mở `output.pdf` bằng Adobe Acrobat Reader hoặc bất kỳ trình xem PDF nào. Bất kỳ hình dạng nào được tô (ví dụ, hình chữ nhật màu) trên trang đầu tiên sẽ xuất hiện với **độ trong suốt 50 %**, trong khi các đường viền vẫn giữ độ mờ đầy đủ. Nếu bạn đã thêm toán tử `gs` tùy chọn, *tất cả* nội dung hiện có trên trang sẽ kế thừa cùng độ trong suốt.

## Common questions and troubleshooting

| Question | Answer |
|----------|--------|
| **Can I add more than one graphics state?** | Có. Tạo các dictionary bổ sung (ví dụ, `GS1`, `GS2`) và tham chiếu chúng bằng các toán tử `gs` khác nhau. |
| **What if the PDF already uses a name like `GS0`?** | Chọn một tên duy nhất (ví dụ, `MyGS`) hoặc kiểm tra các khóa hiện có bằng `extGState.Keys`. |
| **Does this work with encrypted PDFs?** | Tài liệu phải được mở bằng mật khẩu đúng. Sử dụng `new Document(inputPath, new LoadOptions { Password = "pwd" })`. |
| **Will the changes affect other pages?** | Không. Graphics state được thêm vào tài nguyên của trang bạn chỉnh sửa. Để ảnh hưởng tới mọi trang, lặp lại quy trình cho mỗi trang hoặc thêm dictionary vào tài nguyên *cấp tài liệu* (`doc.Resources`). |
| **Is there a performance impact?** | Thêm một graphics state duy nhất là không đáng kể. Các PDF lớn với nhiều trang có thể cần vòng lặp, nhưng thao tác vẫn có độ phức tạp O(số trang). |

## Pro tips

* **Reuse graphics states:** Nếu bạn cần cùng một độ trong suốt trên nhiều trang, hãy thêm dictionary vào tài nguyên *cấp tài liệu* (`doc.Resources`) và tham chiếu nó từ mỗi trang. Điều này giảm kích thước tệp.
* **Blend modes:** Thử nghiệm các giá trị `BM` khác như `Multiply`, `Screen`, hoặc `Overlay` để tạo hiệu ứng sáng tạo. Không phải tất cả trình xem đều hỗ trợ mọi chế độ hòa trộn, vì vậy hãy kiểm tra với đối tượng người dùng mục tiêu.
* **Testing:** Luôn so sánh PDF gốc và PDF đã chỉnh sửa cạnh nhau. Sử dụng công cụ diff có khả năng render PDF (ví dụ, `DiffPDF`) để xác nhận chỉ có những thay đổi mong muốn.

## Next steps

Bây giờ bạn đã biết **cách add transparency pdf** và **cách modify pdf transparency**, bạn có thể khám phá các chủ đề liên quan:

* **Add graphics state pdf** để tạo hiệu ứng overprint và halftone
* **Embedding images with custom opacity** bằng `ImageFragment` và một graphics state
* **Batch processing** nhiều PDF trong một thư mục với parallelism để tăng tốc độ xử lý
* **Using Aspose.PDF’s high‑level API** (`PdfSaveOptions`, `PdfPageEditor`) cho các quy trình làm việc phức tạp hơn

Hãy thoải mái thử nghiệm với các giá trị alpha khác nhau.

## What Should You Learn Next?

Các tutorial sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh với giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Thêm Độ Trong Suốt vào PDF bằng Aspose – Hướng Dẫn C# Đầy Đủ](/pdf/english/net/programming-with-operators/add-transparency-to-pdf-using-aspose-complete-c-guide/)
- [Cách Thêm Dấu Văn Bản (Text Stamp) vào PDF Sử Dụng Aspose.PDF .NET: Hướng Dẫn Toàn Diện](/pdf/english/net/watermarks-backgrounds/add-text-stamp-pdf-aspose-pdf-dotnet/)
- [Cách Thêm Hình Ảnh vào PDF Sử Dụng Aspose.PDF cho .NET: Hướng Dẫn Từng Bước](/pdf/english/net/images-graphics/add-images-to-pdfs-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}