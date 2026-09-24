---
category: general
date: 2026-02-09
description: Lưu PDF dưới dạng PNG trong C# bằng Aspose PDF, sau đó xuất PDF sang
  HTML, thêm dấu watermark PDF, và tìm hiểu cách chuyển đổi PDFX‑1a cho việc chuyển
  đổi PDF trong ASP.NET.
draft: false
keywords:
- save pdf as png
- export pdf to html
- add watermark stamp pdf
- how to convert pdfx-1a
- asp.net pdf conversion
language: vi
og_description: Lưu PDF dưới dạng PNG trong C# với Aspose PDF, sau đó xuất PDF sang
  HTML, thêm dấu watermark vào PDF và khám phá cách chuyển đổi PDFX‑1a cho việc chuyển
  đổi PDF trong ASP.NET.
og_title: Lưu PDF dưới dạng PNG và Chuyển đổi sang PDF/X‑1a với Aspose PDF
tags:
- aspnet
- pdf
- csharp
title: Lưu PDF dưới dạng PNG và Chuyển đổi sang PDF/X‑1a với Aspose PDF
url: /vi/net/conversion-export/save-pdf-as-png-and-convert-to-pdf-x-1a-with-aspose-pdf/
---

we preserve the shortcodes exactly.

Let's produce the translated content.

We'll start with the shortcodes as is.

Then translate the heading "# Save PDF as PNG and Convert to PDF/X‑1a with Aspose PDF" to Vietnamese: "# Lưu PDF dưới dạng PNG và Chuyển đổi sang PDF/X‑1a với Aspose PDF". Keep the same.

Then paragraph.

Let's translate step by step.

I'll write Vietnamese translation, preserving technical terms.

Let's go.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Lưu PDF dưới dạng PNG và Chuyển đổi sang PDF/X‑1a với Aspose PDF

Bạn đã bao giờ tự hỏi cách **lưu PDF dưới dạng PNG** mà không phải đau đầu không? Bạn không phải là người duy nhất—các nhà phát triển luôn tìm kiếm một cách nhanh chóng để raster hoá một trang trong khi vẫn giữ nguyên PDF gốc. Trong hướng dẫn này, chúng ta sẽ thực hiện đúng như vậy, đồng thời sẽ chỉ cho bạn cách **xuất PDF sang HTML**, thêm một **đóng dấu watermark PDF**, và thậm chí **chuyển đổi PDFX‑1a** cho một pipeline **ASP.NET PDF conversion** mạnh mẽ.

Bạn sẽ nhận được từ tutorial này là một chương trình C# sẵn sàng copy‑paste, tải một PDF, chuyển đổi nó sang file tuân thủ PDF/X‑1a, render trang đầu tiên thành PNG, thêm một dấu văn bản động, và cuối cùng xuất ra phiên bản HTML giữ nguyên mã hoá phông chữ. Không có những tham chiếu mơ hồ, chỉ có code cụ thể và “lý do” đằng sau mỗi dòng.

## Yêu cầu trước

- .NET 6.0 hoặc mới hơn (code cũng hoạt động trên .NET Framework 4.7+)
- Gói NuGet Aspose.Pdf for .NET (`Install-Package Aspose.Pdf`)
- Một file hồ sơ ICC (`profile.icc`) nếu bạn cần tuân thủ PDF/X‑1a
- Một file PDF nguồn (`input.pdf`) mà bạn muốn chuyển đổi

Đó là tất cả—không cần thư viện phụ, không có bước ẩn. Nếu bạn đã có những thứ trên, bạn đã sẵn sàng.

## Bước 1: Tải tài liệu PDF nguồn

Trước khi làm bất cứ việc gì, chúng ta cần đưa PDF vào bộ nhớ.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Devices;

// Load the PDF you’ll be working with
Document pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");
```

**Tại sao lại quan trọng:** `Document` là đối tượng cốt lõi; nó cho bạn truy cập vào các trang, phông chữ và siêu dữ liệu. Tải một lần giúp phần còn lại của pipeline nhanh hơn.

## Bước 2: Chuyển đổi sang PDF/X‑1a (Cách chuyển đổi PDFX‑1a)

PDF/X‑1a là tiêu chuẩn được ưa chuộng cho các file sẵn sàng in. Việc chuyển đổi đảm bảo mọi phông chữ được nhúng và màu sắc được định nghĩa.

```csharp
// Set up conversion options for PDF/X‑1a
PdfFormatConversionOptions conversionOptions = new PdfFormatConversionOptions(
    PdfFormat.PDF_X_1A,               // Target format
    ConvertErrorAction.Delete)       // What to do on errors
{
    IccProfileFileName = "YOUR_DIRECTORY/profile.icc", // External ICC profile
    OutputIntent = new OutputIntent("FOGRA39")        // Output intent for printing
};

// Perform the conversion
pdfDocument.Convert(conversionOptions);
```

**Mẹo chuyên nghiệp:** Nếu bạn bỏ qua hồ sơ ICC, Aspose sẽ tự động nhúng một hồ sơ mặc định, nhưng sử dụng đúng hồ sơ mà máy in của bạn yêu cầu sẽ tránh được những sai lệch màu không mong muốn.

## Bước 3: Lưu file tuân thủ PDF/X‑1a

Bây giờ tài liệu đã đáp ứng tiêu chuẩn PDF/X‑1a, chúng ta ghi ra file.

```csharp
pdfDocument.Save("YOUR_DIRECTORY/pdfx1a.pdf");
```

Bạn sẽ nhận thấy kích thước file có thể tăng—các tài nguyên bổ sung đang được nhúng, và đó chính là điều bạn muốn cho đầu ra in đáng tin cậy.

## Bước 4: Render trang đầu tiên thành PNG (Lưu PDF dưới dạng PNG)

Đây là nơi từ khóa chính tỏa sáng: chúng ta sẽ **lưu PDF dưới dạng PNG** để tạo ảnh thu nhỏ hoặc hiển thị trên web.

```csharp
// Configure PNG device with font analysis (helps with text extraction later)
PngDevice pngDevice = new PngDevice
{
    RenderingOptions = new RenderingOptions { AnalyzeFonts = true }
};

// Render only the first page
pngDevice.Process(pdfDocument.Pages[1], "YOUR_DIRECTORY/page1.png");
```

![Lưu PDF dưới dạng PNG ví dụ](https://example.com/images/save-pdf-as-png.png "Ví dụ một trang PDF được lưu dưới dạng PNG")

Cờ `AnalyzeFonts` báo cho Aspose nhúng thông tin phông chữ vào siêu dữ liệu PNG, một thủ thuật hữu ích nếu bạn sau này cần ánh xạ lại tới văn bản gốc.

## Bước 5: Thêm Watermark Stamp PDF

Thêm một **watermark stamp PDF** là việc đơn giản với `TextStamp` của Aspose. Chúng ta sẽ làm cho dấu tự động điều chỉnh kích thước để vừa với một hình chữ nhật.

```csharp
// Create a text stamp that auto‑adjusts its font size
TextStamp textStamp = new TextStamp("Important notice")
{
    AutoAdjustFontSizeToFitStampRectangle = true,
    AutoAdjustFontSizePrecision = 0.01f,
    Width = 400,               // Width of the stamp rectangle
    Height = 200,              // Height of the stamp rectangle
    WordWrapMode = TextFormattingOptions.WordWrapMode.ByWords
};

// Place the stamp on the first page
pdfDocument.Pages[1].AddStamp(textStamp);
```

**Tại sao cần tự động điều chỉnh?** Các trang có mật độ khác nhau; để API tính toán kích thước phông chữ tối ưu đảm bảo văn bản không bị tràn ra khỏi hình chữ nhật.

## Bước 6: Lưu PDF đã dán dấu

Sau khi dán dấu, chúng ta ghi lại các thay đổi.

```csharp
pdfDocument.Save("YOUR_DIRECTORY/stamped.pdf");
```

Mở `stamped.pdf` bằng bất kỳ trình xem nào và bạn sẽ thấy hộp “Important notice” được căn giữa một cách gọn gàng—không cần tinh chỉnh thủ công.

## Bước 7: Xuất PDF sang HTML (Export PDF to HTML)

Cuối cùng, hãy **xuất PDF sang HTML** đồng thời ưu tiên CMap cho mã hoá phông chữ. Điều này đảm bảo HTML tạo ra sử dụng Unicode ở mọi nơi có thể, giữ cho văn bản có thể tìm kiếm được.

```csharp
HtmlSaveOptions htmlOptions = new HtmlSaveOptions
{
    FontEncodingStrategy = HtmlSaveOptions.FontEncodingRules.DecreaseToUnicodePriorityLevel
};

// Save the HTML representation
pdfDocument.Save("YOUR_DIRECTORY/cmap.html", htmlOptions);
```

File `cmap.html` tạo ra chứa các phần tử `<canvas>` cho đồ họa phức tạp và các thẻ `<span>` thích hợp cho văn bản, sẵn sàng cho các trang web thân thiện SEO.

## Ví dụ đầy đủ hoạt động

Dưới đây là chương trình hoàn chỉnh mà bạn có thể đưa vào một ứng dụng console. Chỉ cần thay thế các đường dẫn placeholder và bạn đã sẵn sàng.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Devices;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source PDF
        Document pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");

        // 2️⃣ Convert to PDF/X‑1a (how to convert pdfx‑1a)
        PdfFormatConversionOptions conversionOptions = new PdfFormatConversionOptions(
            PdfFormat.PDF_X_1A,
            ConvertErrorAction.Delete)
        {
            IccProfileFileName = "YOUR_DIRECTORY/profile.icc",
            OutputIntent = new OutputIntent("FOGRA39")
        };
        pdfDocument.Convert(conversionOptions);

        // 3️⃣ Save the PDF/X‑1a file
        pdfDocument.Save("YOUR_DIRECTORY/pdfx1a.pdf");

        // 4️⃣ Render first page as PNG (save pdf as png)
        PngDevice pngDevice = new PngDevice
        {
            RenderingOptions = new RenderingOptions { AnalyzeFonts = true }
        };
        pngDevice.Process(pdfDocument.Pages[1], "YOUR_DIRECTORY/page1.png");

        // 5️⃣ Add a dynamic watermark stamp (add watermark stamp pdf)
        TextStamp textStamp = new TextStamp("Important notice")
        {
            AutoAdjustFontSizeToFitStampRectangle = true,
            AutoAdjustFontSizePrecision = 0.01f,
            Width = 400,
            Height = 200,
            WordWrapMode = TextFormattingOptions.WordWrapMode.ByWords
        };
        pdfDocument.Pages[1].AddStamp(textStamp);

        // 6️⃣ Save the stamped PDF
        pdfDocument.Save("YOUR_DIRECTORY/stamped.pdf");

        // 7️⃣ Export to HTML (export pdf to html)
        HtmlSaveOptions htmlOptions = new HtmlSaveOptions
        {
            FontEncodingStrategy = HtmlSaveOptions.FontEncodingRules.DecreaseToUnicodePriorityLevel
        };
        pdfDocument.Save("YOUR_DIRECTORY/cmap.html", htmlOptions);

        Console.WriteLine("All operations completed successfully.");
    }
}
```

**Kết quả mong đợi**

- `pdfx1a.pdf` – file PDF/X‑1a sẵn sàng in
- `page1.png` – ảnh raster của trang đầu tiên (hoàn hảo cho ảnh thu nhỏ)
- `stamped.pdf` – PDF gốc với watermark “Important notice” có thể mở rộng
- `cmap.html` – phiên bản HTML thân thiện web với phông chữ Unicode

## Câu hỏi thường gặp & Trường hợp đặc biệt

- **Nếu PDF nguồn có các trang được mã hoá thì sao?**  
  Tải nó bằng mật khẩu: `new Document("input.pdf", new LoadOptions { Password = "secret" })`.

- **Có cần hồ sơ ICC cho mọi lần chuyển đổi không?**  
  Không bắt buộc—Aspose sẽ sử dụng một hồ sơ chung, nhưng để đạt chuẩn PDF/X‑1a nghiêm ngặt bạn nên cung cấp đúng hồ sơ mà nhà in của bạn sử dụng.

- **Có thể render nhiều hơn một trang thành PNG không?**  
  Chắc chắn. Lặp qua `pdfDocument.Pages` và gọi `pngDevice.Process(page, $"page{page.Number}.png")`.

- **Kết quả HTML có thân thiện với thiết bị di động không?**  
  HTML tạo ra sử dụng các phần tử `<canvas>` đáp ứng. Nếu bạn cần văn bản thuần CSS, đặt `htmlOptions.SplitIntoPages = false` và điều chỉnh `htmlOptions.PartsEmbeddingMode`.

## Mẹo cho việc chuyển đổi PDF trong ASP.NET

Khi tích hợp đoạn code này vào một controller ASP.NET Core, hãy nhớ:

1. **Stream kết quả** thay vì ghi ra đĩa—sử dụng `MemoryStream` và trả về `FileResult`.
2. **Dispose** các đối tượng `Document` và các thiết bị bằng `using

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}