---
category: general
date: 2026-10-07
description: Thêm trạng thái đồ họa PDF bằng Aspose.Pdf trong C# để thay đổi độ trong
  suốt của PDF. Hãy làm theo hướng dẫn từng bước này để nhúng các trạng thái đồ họa
  tùy chỉnh và kiểm soát độ mờ.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add graphics state pdf
- modify pdf transparency
language: vi
lastmod: 2026-10-07
og_description: Thêm trạng thái đồ họa PDF với Aspose.Pdf trong C#. Tìm hiểu cách
  chỉnh sửa độ trong suốt của PDF bằng cách tạo một từ điển trạng thái đồ họa tùy
  chỉnh.
og_image_alt: Screenshot showing the add graphics state pdf code editor in Visual
  Studio
og_title: Thêm trạng thái đồ họa PDF với Aspose.Pdf – kiểm soát độ trong suốt của
  PDF
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Add graphics state pdf using Aspose.Pdf in C# to modify PDF transparency.
    Follow this step‑by‑step guide to embed custom graphics states and control opacity.
  headline: Add graphics state pdf with Aspose.Pdf in C#
  type: TechArticle
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Thêm trạng thái đồ họa PDF bằng Aspose.Pdf trong C#
url: /vi/net/images-graphics/add-graphics-state-pdf-with-aspose-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Thêm graphics state pdf với Aspose.Pdf trong C#

Nếu bạn cần **thêm graphics state pdf** vào một tài liệu, hướng dẫn này sẽ chỉ cho bạn cách thực hiện chính xác với Aspose.Pdf cho .NET. Khi kết thúc hướng dẫn, bạn cũng sẽ biết cách **sửa đổi độ trong suốt PDF**, cho phép bạn đặt các giá trị độ mờ tùy chỉnh cho bất kỳ thao tác vẽ nào.

Làm việc với graphics state của PDF cho phép bạn kiểm soát các tham số như độ rộng đường, chế độ hòa trộn, và quan trọng nhất trong bài viết này là độ trong suốt của nội dung. Các bước dưới đây được viết cho các nhà phát triển quen thuộc với C# và muốn có một giải pháp sẵn sàng chạy mà không phải đào sâu vào tài liệu SDK chính thức.

## Những gì bạn sẽ học

* Cách tạo một graphics state dictionary mới và điền các mục `CA`, `ca`, và `BM`.  
* Cách chèn dictionary đó vào tài nguyên `ExtGState` của trang để PDF nhận diện nó.  
* Cách các giá trị `ca` (stroke) và `CA` (fill) ảnh hưởng đến **sửa đổi độ trong suốt PDF** cho các lệnh vẽ tiếp theo.  
* Các lỗi thường gặp như xung đột tên và tính tương thích phiên bản, cùng với các mẹo chuyên nghiệp để mở rộng graphics state sau này.

**Yêu cầu trước**

* .NET 6.0 trở lên (mã cũng hoạt động với .NET Framework 4.7+).  
* Giấy phép Aspose.Pdf cho .NET hợp lệ (phiên bản dùng thử miễn phí hoạt động cho việc thử nghiệm).  
* Visual Studio 2022 hoặc bất kỳ IDE C# nào bạn thích.  

---

## Bước 1: Cài đặt Aspose.Pdf cho .NET

Thêm gói NuGet vào dự án của bạn:

```bash
dotnet add package Aspose.Pdf
```

Gói này bao gồm namespace `Aspose.Pdf` cung cấp các lớp `Document`, `DictionaryEditor` và `CosPdfDictionary` được sử dụng sau này.

> **Mẹo chuyên nghiệp:** Nếu bạn dự định xử lý nhiều PDF trong một lô, hãy bật **License** sớm trong `Program.cs` để tránh dấu bản quyền đánh giá.

```csharp
// Apply your license (optional for evaluation)
Aspose.Pdf.License license = new Aspose.Pdf.License();
license.SetLicense("Aspose.Pdf.lic");
```

## Bước 2: Xác định đường dẫn đầu vào và đầu ra

Bạn phải chỉ định SDK tới một tệp PDF hiện có (`input.pdf`) và chỉ ra nơi tệp đã chỉnh sửa sẽ được lưu (`output.pdf`).

```csharp
// Define input and output PDF file paths
string inputPath = @"C:\MyPdfs\input.pdf";
string outputPath = @"C:\MyPdfs\output.pdf";
```

> **Tại sao điều này quan trọng:** Sử dụng đường dẫn tuyệt đối ngăn SDK tìm kiếm trong thư mục làm việc sai, đây là nguyên nhân phổ biến gây ra `FileNotFoundException`.

## Bước 3: Mở PDF và xác định tài nguyên của trang đầu tiên

Dictionary `ExtGState` nằm trong dictionary tài nguyên của mỗi trang. Chúng ta sẽ chỉnh sửa trang đầu tiên để đơn giản, nhưng cách tiếp cận này cũng hoạt động cho bất kỳ chỉ số trang nào.

```csharp
using (var pdfDocument = new Aspose.Pdf.Document(inputPath))
{
    // Get the first page (pages are 1‑based)
    var firstPage = pdfDocument.Pages[1];

    // Access the page’s resource dictionary via DictionaryEditor
    var resourcesEditor = new Aspose.Pdf.DictionaryEditor(firstPage.Resources);

    // Retrieve (or create) the ExtGState entry
    var extGStateDict = resourcesEditor["ExtGState"]
        .ToCosPdfDictionary(); // Throws if ExtGState does not exist
```

**Trường hợp đặc biệt:** Nếu trang không có mục `ExtGState`, bạn cần tạo nó:

```csharp
if (!resourcesEditor.ContainsKey("ExtGState"))
{
    var emptyDict = Aspose.Pdf.CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
    resourcesEditor.Add("ExtGState", emptyDict);
    extGStateDict = emptyDict;
}
```

## Bước 4: Xây dựng một graphics state dictionary mới

Graphics state là một tập hợp các cặp khóa/giá trị mô tả cách các thao tác vẽ hoạt động. Đối với độ trong suốt, chúng ta cần ba khóa:

| Key | Ý nghĩa | Giá trị điển hình |
|-----|---------|-------------------|
| `CA` | Độ trong suốt tô (0 = transparent, 1 = opaque) | `1` (hoàn toàn không trong suốt) |
| `ca` | Độ trong suốt viền (cùng thang) | `0.5` (50 % trong suốt) |
| `BM` | Chế độ hòa trộn (ví dụ, `Normal`, `Multiply`) | `Normal` |

```csharp
    // Create an empty dictionary that will hold the graphics state
    var newGraphicsState = Aspose.Pdf.CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

    // Populate the dictionary with transparency and blend mode entries
    var graphicsStateEntries = new[]
    {
        new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
            "CA", new Aspose.Pdf.CosPdfNumber(1)),
        new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
            "ca", new Aspose.Pdf.CosPdfNumber(0.5)),
        new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
            "BM", new Aspose.Pdf.CosPdfName("Normal"))
    };

    foreach (var entry in graphicsStateEntries)
        newGraphicsState.Add(entry);
```

**Tại sao lại chọn các giá trị này?**  
`ca = 0.5` làm bất kỳ đường viền nào (đường, viền) hiển thị ở độ trong suốt 50 %, trong khi `CA = 1` giữ các hình đã tô đầy hoàn toàn không trong suốt. Điều chỉnh cả hai số để đạt được hiệu ứng **sửa đổi độ trong suốt PDF** chính xác mà bạn cần.

## Bước 5: Chèn graphics state vào dictionary ExtGState

Bạn phải đặt cho trạng thái mới một tên duy nhất (ví dụ, `GS0`). Nếu tên đã tồn tại, Aspose.Pdf sẽ ghi đè mục hiện có, có thể làm hỏng nội dung khác phụ thuộc vào nó.

```csharp
    // Add the new graphics state under a custom name
    const string stateName = "GS0";

    // Ensure we don’t clash with an existing entry
    if (extGStateDict.ContainsKey(stateName))
        extGStateDict.Remove(stateName);

    extGStateDict.Add(stateName, newGraphicsState);
```

Bây giờ tài nguyên của trang đã biết về `GS0`. Để thực sự sử dụng, bạn sẽ tham chiếu graphics state trong một luồng nội dung qua toán tử `gs` (ví dụ, `GS0 gs`). Aspose.Pdf cho phép bạn chèn các toán tử PDF thô nếu cần vẽ các hình dạng tùy chỉnh.

## Bước 6: Lưu PDF đã chỉnh sửa

```csharp
    // Persist the changes to a new file
    pdfDocument.Save(outputPath);
}
```

`output.pdf` kết quả chứa cùng nội dung hình ảnh như bản gốc, nhưng bất kỳ lệnh vẽ nào sau đó chọn `GS0` sẽ tuân theo các cài đặt độ trong suốt mà bạn đã định nghĩa.

### Kết quả mong đợi

Mở `output.pdf` trong Adobe Acrobat hoặc bất kỳ trình xem PDF nào. Nếu bạn thêm một đường viền mới sử dụng graphics state `GS0` (ví dụ, qua `pdfDocument.Pages[1].Contents.Add(...)`), đường sẽ xuất hiện bán trong suốt trong khi các phần tô vẫn không trong suốt. Điều này chứng tỏ bạn đã thành công **thêm graphics state pdf** và **sửa đổi độ trong suốt PDF**.

---

## Ví dụ đầy đủ có thể chạy

Dưới đây là chương trình hoàn chỉnh bạn có thể sao chép‑dán vào một ứng dụng console. Nó bao gồm việc tải giấy phép, xử lý lỗi và các chú thích giải thích mỗi bước không hiển nhiên.

```csharp
using System;
using Aspose.Pdf;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣  Apply license (optional for evaluation)
        // -------------------------------------------------
        try
        {
            var license = new License();
            license.SetLicense("Aspose.Pdf.lic");
        }
        catch (Exception) { /* License not found – continue in evaluation mode */ }

        // -------------------------------------------------
        // 2️⃣  Define file locations
        // -------------------------------------------------
        string inputPath = @"C:\MyPdfs\input.pdf";
        string outputPath = @"C:\MyPdfs\output.pdf";

        // -------------------------------------------------
        // 3️⃣  Open document and prepare resources
        // -------------------------------------------------
        using (var pdfDocument = new Document(inputPath))
        {
            var firstPage = pdfDocument.Pages[1];
            var resourcesEditor = new DictionaryEditor(firstPage.Resources);

            // Ensure ExtGState dictionary exists
            if (!resourcesEditor.ContainsKey("ExtGState"))
            {
                var emptyExtGState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
                resourcesEditor.Add("ExtGState", emptyExtGState);
            }

            var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();

            // -------------------------------------------------
            // 4️⃣  Create custom graphics state (transparency)
            // -------------------------------------------------
            var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            newGraphicsState.Add("CA", new CosPdfNumber(1));   // Fill opacity
            newGraphicsState.Add("ca", new CosPdfNumber(0.5)); // Stroke opacity
            newGraphicsState.Add("BM", new CosPdf


## Bạn nên học gì tiếp theo?

Các hướng dẫn sau đây bao gồm các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoạt động đầy đủ với giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Thêm Độ trong suốt vào PDF với Aspose PDF trong C# – Hướng dẫn từng bước](/pdf/english/net/images-graphics/add-transparency-to-pdf-with-aspose-pdf-in-c-step-by-step-gu/)
- [Thêm Độ trong suốt vào PDF bằng Aspose – Hướng dẫn C# đầy đủ](/pdf/english/net/programming-with-operators/add-transparency-to-pdf-using-aspose-complete-c-guide/)
- [Cách Thêm Ấn Hình ảnh vào PDF Sử dụng Aspose.PDF cho .NET: Hướng dẫn Toàn diện](/pdf/english/net/images-graphics/add-image-stamp-pdf-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}