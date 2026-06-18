---
category: general
date: 2026-03-19
description: Thêm độ trong suốt vào PDF bằng Aspose.PDF cho C#. Tìm hiểu cách thiết
  lập độ trong suốt, chế độ hòa trộn và ExtGState chỉ trong vài dòng mã.
draft: false
keywords:
- add transparency to pdf
- Aspose PDF transparency
- C# PDF graphics state
- PDF blend mode
- set PDF opacity
language: vi
og_description: Thêm độ trong suốt vào PDF một cách nhanh chóng. Hướng dẫn này cho
  thấy cách kiểm soát độ trong suốt và chế độ hòa trộn bằng Aspose.PDF trong C#.
og_title: Thêm tính trong suốt vào PDF bằng Aspose PDF – Hướng dẫn C# hoàn chỉnh
tags:
- Aspose.PDF
- C#
title: Thêm Độ Trong Suốt vào PDF với Aspose PDF trong C# – Hướng Dẫn Từng Bước
url: /vi/net/images-graphics/add-transparency-to-pdf-with-aspose-pdf-in-c-step-by-step-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Thêm Độ Trong Suốt vào PDF với Aspose PDF trong C# – Hướng Dẫn Đầy Đủ

Bạn đã bao giờ tự hỏi **cách thêm độ trong suốt vào file PDF** mà không phải vật lộn với cú pháp PDF cấp thấp chưa? Bạn không đơn độc. Nhiều nhà phát triển cần một cách nhanh chóng để làm cho các hình dạng hoặc văn bản bán trong suốt — nghĩ đến các dấu bản quyền, đồ họa phủ lên, hoặc các gợi ý UI tinh tế bên trong tài liệu.  

Trong hướng dẫn này, chúng ta sẽ đi qua một **ví dụ hoàn chỉnh, có thể chạy ngay** cho thấy cách thiết lập độ mờ của nền, độ mờ của viền, và chế độ hòa trộn bằng Aspose.PDF cho .NET. Khi hoàn thành, bạn sẽ có một PDF trong đó một hình chữ nhật xuất hiện với độ trong suốt 50 %, và bạn sẽ hiểu tại sao từ điển ExtGState là chìa khóa để đạt được hiệu ứng này.

Chúng ta sẽ bao phủ mọi thứ bạn cần: gói NuGet cần thiết, mã nguồn, giải thích từng dòng, và một vài mẹo cho các trường hợp đặc biệt như các trình xem PDF cũ. Không có tham chiếu bên ngoài — chỉ một giải pháp tự chứa mà bạn có thể sao chép‑dán và chạy ngay hôm nay.

## Những Gì Bạn Cần Chuẩn Bị

- **Aspose.PDF cho .NET** (v23.12 trở lên). Cài đặt qua NuGet: `Install-Package Aspose.PDF`.
- Môi trường phát triển .NET (Visual Studio, Rider, hoặc `dotnet` CLI).
- Một file PDF mẫu có tên `input.pdf` đặt trong thư mục bạn kiểm soát (hướng dẫn này sử dụng `YOUR_DIRECTORY/` làm placeholder).

Đó là tất cả. Nếu bạn đã có những thứ trên, hãy bắt đầu.

## Thêm Độ Trong Suốt vào PDF – Tổng Quan

Cốt lõi của việc làm cho một đối tượng trong PDF trở nên trong suốt là **trạng thái đồ họa** (`ExtGState`). Bằng cách thêm một đối tượng trạng thái đồ họa tùy chỉnh vào từ điển tài nguyên của trang, bạn có thể định nghĩa:

| Thuộc tính | Ý nghĩa |
|------------|----------|
| `ca` | Độ trong suốt của nền (0 = hoàn toàn trong suốt, 1 = độ đục). |
| `CA` | Độ trong suốt của viền (cùng thang đo). |
| `BM` | Chế độ hòa trộn (ví dụ: `Normal`, `Multiply`). |

Chúng ta sẽ tạo một trạng thái đồ họa mới, chèn nó vào từ điển `ExtGState` của trang, và sau đó tham chiếu tới nó khi vẽ. Đoạn mã dưới đây thực hiện đúng như vậy.

![add transparency to pdf diagram](add_transparency_to_pdf.png){alt="thêm độ trong suốt vào pdf"}

## Bước 1: Thiết Lập Dự Án và Tải PDF

Đầu tiên chúng ta tạo một ứng dụng console đơn giản (hoặc bất kỳ dự án C# nào) và tải PDF nguồn.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Operators;          // For low‑level PDF operators
using Aspose.Pdf.Text;               // Optional, if you want to add text later
using Aspose.Pdf.XObjects;          // For image handling, not needed here

// Define the folder that contains the PDF file
string inputDir = @"YOUR_DIRECTORY/";

// Load the PDF document
using (var pdfDocument = new Document(Path.Combine(inputDir, "input.pdf")))
{
    // All subsequent steps go inside this using block
```

**Tại sao điều này quan trọng:**  
`Document` là điểm vào cho mọi thao tác PDF với Aspose. Đặt nó trong khối `using` đảm bảo rằng tất cả tài nguyên được giải phóng đúng cách khi chúng ta lưu file sau này.

## Bước 2: Truy Cập Trang Đầu Tiên và Tài Nguyên Của Nó

Chúng ta cần từ điển tài nguyên của trang đầu tiên vì ở đó chứa bộ sưu tập `ExtGState`.

```csharp
    // Grab the first page (pages are 1‑based in Aspose)
    Page firstPage = pdfDocument.Pages[1];

    // Helper to edit dictionaries (resources, etc.)
    var resourcesEditor = new DictionaryEditor(firstPage.Resources);

    // Retrieve the existing ExtGState dictionary, or create a new one if missing
    CosPdfDictionary extGStateDict;
    if (resourcesEditor.ContainsKey("ExtGState"))
    {
        extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
    }
    else
    {
        extGStateDict = new CosPdfDictionary(pdfDocument);
        resourcesEditor.Add("ExtGState", extGStateDict);
    }
```

**Giải thích:**  
Nếu trang đã có mục `ExtGState` chúng ta sẽ tái sử dụng; nếu không, chúng ta tạo một từ điển mới. Cách tiếp cận phòng thủ này ngăn lỗi tham chiếu null khi làm việc với các PDF không có bất kỳ trạng thái đồ họa nào.

## Bước 3: Tạo Trạng Thái Đồ Họa Mới với Độ Trong Suốt Mong Muốn

Bây giờ chúng ta định nghĩa các giá trị trong suốt thực tế.

```csharp
    // Create an empty dictionary that will represent our new graphics state
    CosPdfDictionary newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

    // Stroke opacity – fully opaque (1.0)
    newGraphicsState.Add("CA", new CosPdfNumber(1));

    // Fill opacity – 50 % transparent (0.5)
    newGraphicsState.Add("ca", new CosPdfNumber(0.5));

    // Blend mode – Normal is the default, but you can experiment with Multiply, Screen, etc.
    newGraphicsState.Add("BM", new CosPdfName("Normal"));
```

**Tại sao lại dùng các khóa này?**  
- `CA` kiểm soát độ trong suốt của các đường viền (đường, khung).  
- `ca` kiểm soát độ trong suốt của nền (hình dạng rắn, văn bản).  
- `BM` chọn cách đối tượng trong suốt hòa trộn với nội dung phía dưới. Sử dụng `"Normal"` giữ cho kết quả hiển thị dự đoán được trên các trình xem.

## Bước 4: Đăng Ký Trạng Thái Đồ Họa vào Tài Nguyên Trang

Chúng ta đặt tên cho trạng thái đồ họa (`GS0`) và thêm nó vào từ điển `ExtGState`.

```csharp
    // Add the graphics state to the ExtGState dictionary with a unique name
    extGStateDict.Add("GS0", newGraphicsState);
```

**Mẹo:**  
Nếu bạn cần nhiều đối tượng trong suốt với các độ trong suốt khác nhau, tạo các mục bổ sung (`GS1`, `GS2`, …) và điều chỉnh giá trị `ca`/`CA` tương ứng.

## Bước 5: Vẽ Một Hình Chữ Nhật Trong Suốt Sử Dụng Trạng Thái Đồ Họa Mới

Với trạng thái đồ họa đã sẵn sàng, chúng ta có thể vẽ một đối tượng thực sự sử dụng nó. Dưới đây chúng ta thêm một hình chữ nhật màu xanh bán trong suốt vào trang.

```csharp
    // Prepare a content stream for the page (adds to existing content)
    var canvas = new Aspose.Pdf.Drawing.Graphic(firstPage);

    // Set the graphics state we just created
    canvas.SetGraphicsState("GS0");

    // Choose a fill color (blue) and draw the rectangle
    canvas.SetColor(new Aspose.Pdf.Drawing.Color(0, 0, 255)); // RGB blue
    canvas.Rectangle(100, 500, 200, 100); // x, y, width, height

    // Close the canvas to flush commands
    canvas.Close();
```

**Bạn sẽ thấy gì:**  
Khi mở PDF kết quả, một hình chữ nhật màu xanh sẽ xuất hiện ở vị trí đã chỉ định, nhưng nội dung trang nền vẫn hiển thị qua nó vì độ trong suốt của nền là 0.5. Nếu bạn kiểm tra PDF bằng công cụ như tính năng “Edit PDF” của Adobe Acrobat, bạn sẽ thấy đối tượng `ExtGState` (`GS0`) được gắn vào hình chữ nhật đó.

## Bước 6: Lưu PDF Đã Cập Nhật

Cuối cùng, ghi tài liệu đã chỉnh sửa trở lại đĩa.

```csharp
    // Save the document with a new name so the original stays untouched
    pdfDocument.Save(Path.Combine(inputDir, "ExtGStateAdded.pdf"));
}
```

Đó là toàn bộ quy trình. Chạy ứng dụng console, mở `ExtGStateAdded.pdf`, và xác nhận lớp phủ trong suốt.

---

## Ví Dụ Hoàn Chỉnh (Sẵn Sàng Sao Chép‑Dán)

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

class AddTransparencyDemo
{
    static void Main()
    {
        // Step 1: Define the folder that contains the PDF file
        string inputDir = @"YOUR_DIRECTORY/";

        // Step 2: Load the PDF document
        using (var pdfDocument = new Document(Path.Combine(inputDir, "input.pdf")))
        {
            // Step 3: Get the first page and its resource dictionary
            Page firstPage = pdfDocument.Pages[1];
            var resourcesEditor = new DictionaryEditor(firstPage.Resources);

            // Ensure ExtGState dictionary exists
            CosPdfDictionary extGStateDict;
            if (resourcesEditor.ContainsKey("ExtGState"))
                extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
            else
            {
                extGStateDict = new CosPdfDictionary(pdfDocument);
                resourcesEditor.Add("ExtGState", extGStateDict);
            }

            // Step 4: Create a new graphics state with opacity and blend mode settings
            CosPdfDictionary newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            newGraphicsState.Add("CA", new CosPdfNumber(1));          // stroke opacity (fully opaque)
            newGraphicsState.Add("ca", new CosPdfNumber(0.5));       // fill opacity (50% transparent)
            newGraphicsState.Add("BM", new CosPdfName("Normal"));   // blend mode

            // Step 5: Add the new graphics state to the page resources
            extGStateDict.Add("GS0", newGraphicsState);

            // Step 6: Draw a rectangle using the new graphics state
            var canvas = new Graphic(firstPage);
            canvas.SetGraphicsState("GS0");
            canvas.SetColor(new Color(0, 0, 255)); // blue fill
            canvas.Rectangle(100, 500, 200, 100);
            canvas.Close();

            // Step 7: Save the updated PDF document
            pdfDocument.Save(Path.Combine(inputDir, "ExtGStateAdded.pdf"));
        }

        Console.WriteLine("PDF with transparency created successfully.");
    }
}
```

**Kết quả mong đợi:**  
Mở `ExtGStateAdded.pdf` sẽ hiển thị một hình chữ nhật màu xanh tại (100, 500) với độ trong suốt nền 50 %. Phía dưới hình chữ nhật, bất kỳ văn bản hoặc hình ảnh nào đã tồn tại vẫn còn nhìn thấy được.

---

## Câu Hỏi Thường Gặp & Các Trường Hợp Đặc Biệt

### Điều này có hoạt động trên các trình xem PDF cũ không?
Hầu hết các trình xem hiện đại (Adobe Reader, Foxit, Chrome) hỗ trợ các khóa `ca`/`CA` cơ bản. Các trình xem rất cũ có thể bỏ qua chúng và hiển thị hình dạng hoàn toàn đục.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}