---
category: general
date: 2026-07-14
description: Lưu PDF dưới dạng HTML bằng Aspose.Pdf – tìm hiểu cách tạo tài liệu PDF,
  thêm hình chữ nhật vào PDF và xuất ra HTML sạch không có hình ảnh.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save pdf as html
- how to create pdf document
- add rectangle shape pdf
language: vi
lastmod: 2026-07-14
og_description: Lưu PDF dưới dạng HTML với Aspose.Pdf. Khám phá cách tạo tài liệu
  PDF, vẽ hình chữ nhật trong PDF và tạo HTML không có hình ảnh trong vài phút.
og_image_alt: Screenshot of a PDF saved as HTML showing a rectangle shape
og_title: Lưu PDF dưới dạng HTML – Hướng dẫn nhanh tạo PDF và Thêm hình chữ nhật
schemas:
- author: Aspose
  dateModified: '2026-07-14'
  description: Save PDF as HTML using Aspose.Pdf – learn how to create PDF document,
    add rectangle shape PDF, and export to clean HTML without images.
  headline: Save PDF as HTML – Create PDF, add rectangle shape
  type: TechArticle
tags:
- pdf
- aspnet
- csharp
- html-export
title: Lưu PDF dưới dạng HTML – Tạo PDF, thêm hình chữ nhật
url: /vi/net/conversion-export/save-pdf-as-html-create-pdf-add-rectangle-shape/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Lưu PDF dưới dạng HTML – Tạo PDF, thêm hình chữ nhật

Bạn có bao giờ tự hỏi làm thế nào để **lưu PDF dưới dạng HTML** trong khi vẫn có thể vẽ đồ họa trên PDF nguồn không? Bạn không phải là người duy nhất. Trong nhiều công cụ nội bộ, chúng tôi cần một bản xem trước HTML sạch sẽ của PDF có chứa các hình dạng tùy chỉnh, và các bộ chuyển đổi thông thường hoặc nhúng các hình ảnh raster nặng, hoặc loại bỏ hoàn toàn dữ liệu vector.

Trong hướng dẫn này, chúng ta sẽ đi qua **cách tạo tài liệu PDF** một cách lập trình với Aspose.Pdf, vẽ một **hình chữ nhật PDF**, cấu hình đánh số Bates, và cuối cùng **lưu PDF dưới dạng HTML** mà không bao gồm các hình ảnh raster. Khi kết thúc, bạn sẽ có một ứng dụng console C# chạy được đầy đủ, tạo ra một tệp HTML mà bạn có thể mở trong bất kỳ trình duyệt nào—không cần các tệp hình ảnh bổ sung.

> **Mẹo chuyên nghiệp:** Aspose.Pdf hoạt động với .NET 6+, .NET Framework 4.6+ và thậm chí .NET Core, vì vậy bạn có thể đưa nó vào một dịch vụ Windows cũ hoặc một microservice mới hoàn toàn.

---

## Prerequisites

- **Visual Studio 2022** (Community hoặc cao hơn) hoặc bất kỳ IDE nào tương thích với C#.  
- **Aspose.Pdf for .NET** gói NuGet (phiên bản 23.11 trở lên). Cài đặt nó qua Package Manager Console:

```powershell
Install-Package Aspose.Pdf
```

- Kiến thức cơ bản về cú pháp C#; không cần kinh nghiệm trước về PDF.

---

## Save PDF as HTML with Aspose.Pdf

Dưới đây là đoạn mã hoàn chỉnh, sẵn sàng sao chép‑dán. Nó tuân theo các bước chính xác từ đoạn mã gốc nhưng thêm các chú thích, xử lý lỗi, và một phương thức trợ giúp nhỏ để giữ luồng chính dễ đọc.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using Aspose.Pdf.Text;

namespace PdfToHtmlDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create a fresh PDF document.
            Document pdfDoc = new Document();
            Page pdfPage = pdfDoc.Pages.Add();

            // 2️⃣ Draw a rectangle shape on the page.
            //    This demonstrates the "add rectangle shape pdf" requirement.
            var rectangle = new Rectangle(100, 500, 300, 700)
            {
                // Optional visual tweaks
                FillColor = Color.GetYellow(),
                Border = new Border
                {
                    Width = 2,
                    Color = Color.GetRed()
                }
            };
            pdfPage.Paragraphs.Add(rectangle);
            pdfPage.ValidateGraphicsState(); // Ensures the shape fits within page bounds

            // 3️⃣ Configure Bates numbering – useful for legal documents.
            var bates = new BatesNumbering { StartNumber = 1, Prefix = "DOC-" };
            pdfDoc.BatesNumbering = bates;

            // 4️⃣ Add a tagged element with an explicit position.
            //    Tagging is important for accessibility (PDF/UA).
            var taggedElement = new TagStructure();
            taggedElement.PositionSettings = new TagPositionSettings { X = 150, Y = 600 };
            pdfPage.TagStructure.Add(taggedElement);

            // 5️⃣ Enable detection of compromised signatures.
            pdfDoc.SecurityOptions.DetectCompromisedSignatures = true;
            bool hasCompromisedSignature = pdfDoc.SecurityOptions.HasCompromisedSignature;
            Console.WriteLine($"Compromised signature? {hasCompromisedSignature}");

            // 6️⃣ Finally, save the PDF as HTML *without* embedding raster images.
            var htmlOptions = new HtmlSaveOptions
            {
                SkipImages = true,               // Removes <img> tags for raster data
                FixedLayout = true,              // Preserves the original page layout
                ExportEmbeddedFonts = false      // Keeps the HTML lightweight
            };

            string outputPath = @"output.html";
            pdfDoc.Save(outputPath, htmlOptions);
            Console.WriteLine($"✅ PDF successfully saved as HTML at: {outputPath}");
        }
    }
}
```

### What the code does, step by step

| Bước | Tại sao quan trọng |
|------|--------------------|
| **Create a PDF document** | Đây là nền tảng—không có đối tượng `Document` bạn không thể thêm bất kỳ gì. |
| **Add rectangle shape PDF** | Minh họa việc vẽ vector; hình chữ nhật là hình dạng đơn giản nhất nhưng cùng API cũng hỗ trợ vòng tròn, đa giác, v.v. |
| **Configure Bates numbering** | Thường được yêu cầu trong các trường hợp kiện tụng hoặc xử lý hàng loạt để xác định duy nhất các trang. |
| **Tag structure** | Cải thiện khả năng truy cập; trình đọc màn hình dựa vào thẻ để truyền tải thứ tự đọc. |
| **Detect compromised signatures** | Các ứng dụng chú ý bảo mật cần biết nếu chữ ký số bị giả mạo. |
| **Save PDF as HTML** | Mục tiêu cuối cùng—tạo HTML sạch sẽ phản ánh bố cục PDF mà không có các tệp hình ảnh nặng. |

> **Tại sao `SkipImages = true`?**  
> Khi bạn chuyển đổi một PDF chứa đồ họa vector (như hình chữ nhật của chúng ta) bạn thường không cần bản sao raster. Thiết lập `SkipImages` sẽ loại bỏ các phần tử `<img>` mà nếu không sẽ tham chiếu tới các blob base‑64, giữ cho tệp HTML dưới vài kilobyte.

---

## How to create PDF document with Aspose.Pdf

Nếu bạn mới với Aspose, thư viện này xử lý PDF giống như một tài liệu Word: bạn thêm **trang**, sau đó **đoạn văn**, **hình dạng**, hoặc **chú thích** vào các trang đó. Lớp `Document` là điểm vào, và mỗi `Page` chứa một bộ sưu tập gọi là `Paragraphs`. Bất kỳ đối tượng nào kế thừa từ `TextFragmentAbsorber`, `Image`, `Rectangle`, v.v., đều có thể được chèn vào bộ sưu tập đó.

Dưới đây là một đoạn mã tối thiểu chỉ tạo một PDF trống—hữu ích khi bạn muốn bắt đầu từ đầu:

```csharp
Document emptyPdf = new Document();
Page firstPage = emptyPdf.Pages.Add();   // Adds a default‑size A4 page
emptyPdf.Save("empty.pdf");
```

Bạn có thể nối thêm các trang bằng một vòng lặp `for` đơn giản, hoặc áp dụng các cài đặt cấp trang (lề, kích thước) qua `PageInfo`. Sự linh hoạt này là lý do Aspose.Pdf được ưa chuộng cho việc tạo PDF phía máy chủ.

---

## Add rectangle shape PDF – drawing graphics

Lớp `Rectangle` nằm trong `Aspose.Pdf.Annotations`. Nó nhận bốn tọa độ: **lower‑left X**, **lower‑left Y**, **upper‑right X**, **upper‑right Y**. Hãy nghĩ hệ tọa độ PDF như

## What Should You Learn Next?

Các hướng dẫn sau đây bao phủ các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoạt động đầy đủ với các giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Tạo tài liệu PDF với Aspose.PDF – Thêm trang, hình dạng & Lưu](/pdf/english/net/document-creation/create-pdf-document-with-aspose-pdf-add-page-shape-save/)
- [Chuyển PDF sang HTML trong .NET bằng Aspose.PDF mà không lưu hình ảnh](/pdf/english/net/conversion-export/convert-pdf-html-net-asposepdf-no-images/)
- [Chuyển PDF sang HTML bằng Aspose.PDF .NET: Lưu hình ảnh dưới dạng PNG bên ngoài](/pdf/english/net/conversion-export/pdf-to-html-conversion-external-png-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}