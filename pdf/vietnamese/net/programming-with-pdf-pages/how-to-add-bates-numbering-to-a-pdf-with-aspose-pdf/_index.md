---
category: general
date: 2026-10-07
description: Tìm hiểu cách thêm đánh số Bates vào PDF bằng C#. Hướng dẫn chi tiết
  này cũng bao gồm cách đánh số trang PDF và các thủ thuật đánh số khác.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add bates numbering
- pdf page numbering
- number pdf pages
- how to add bates
- bates numbering pdf
language: vi
lastmod: 2026-10-07
og_description: Thêm đánh số Bates vào PDF nhanh chóng. Theo dõi hướng dẫn này để
  thành thạo việc đánh số trang PDF, đánh số các trang PDF và tự động theo dõi tài
  liệu.
og_image_alt: Screenshot of a PDF with Bates numbers added using Aspose.Pdf
og_title: Thêm đánh số Bates vào PDF trong C# – hướng dẫn đầy đủ của Aspose
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Learn how to add bates numbering to a PDF using C#. This step‑by‑step
    guide also covers pdf page numbering and other numbering tricks.
  headline: How to add bates numbering to a PDF with Aspose.Pdf
  type: TechArticle
- description: Learn how to add bates numbering to a PDF using C#. This step‑by‑step
    guide also covers pdf page numbering and other numbering tricks.
  name: How to add bates numbering to a PDF with Aspose.Pdf
  steps:
  - name: 1. Can I change the location of the numbers?
    text: Yes. Set `batesOptions.Position = new Position(10, 10, 10, 10);` where the
      four values represent margins from the top, bottom, left, and right edges. Aspose
      also provides predefined enums such as `BatesNumberingPosition.BottomCenter`.
  - name: 2. What if my PDF already contains page numbers?
    text: Adding Bates numbers will **stack** on top of existing numbers. To avoid
      visual clutter, either hide the original numbers (if they are part of a text
      layer) or adjust the `batesOptions` font size and position.
  - name: 3. Does this work with encrypted PDFs?
    text: 'Aspose can open password‑protected PDFs if you supply the password:'
  - name: 4. How do I **number pdf pages** with a simple sequential counter (no prefix/suffix)?
    text: 'Just set `Prefix = string.Empty` and `Suffix = string.Empty`:'
  - name: 5. Can I use this approach in ASP.NET Core to serve PDFs on‑the‑fly?
    text: 'Absolutely. Load the document, apply the numbering, then write the stream
      to the HTTP response:'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Cách thêm đánh số Bates vào PDF bằng Aspose.Pdf
url: /vi/net/programming-with-pdf-pages/how-to-add-bates-numbering-to-a-pdf-with-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách thêm **bates numbering** vào PDF bằng Aspose.Pdf

Nếu bạn cần **thêm bates numbering** vào một PDF, hướng dẫn này sẽ cho bạn thấy cách thực hiện chính xác bằng C#. Dù bạn đang chuẩn bị các bộ tài liệu pháp lý, quản lý hồ sơ vụ án, hay chỉ muốn **đánh số trang pdf** đáng tin cậy, các bước dưới đây sẽ cung cấp cho bạn một giải pháp hoàn chỉnh, có thể chạy được.

Trong tutorial này bạn sẽ học cách:

* Tải một tệp PDF hiện có.
* Cấu hình các tùy chọn Bates numbering như tiền tố, số bắt đầu, độ dài chữ số, ký tự phân tách và hậu tố.
* Áp dụng việc đánh số cho mỗi trang.
* Lưu tài liệu đã cập nhật.

Không cần công cụ bên ngoài nào ngoài thư viện Aspose.Pdf for .NET, và mã hoạt động với .NET 6+ cũng như .NET Framework 4.7.2+.  

---

## Yêu cầu trước

Trước khi bắt đầu, hãy chắc chắn bạn có:

| Yêu cầu | Lý do quan trọng |
|-------------|----------------|
| **Aspose.Pdf for .NET** (gói NuGet `Aspose.Pdf`) | Cung cấp các lớp `Document` và `BatesNumberingOptions` được sử dụng trong mã. |
| **.NET SDK** (khuyến nghị 6.0 hoặc mới hơn) | Cho phép bạn biên dịch và chạy ứng dụng console C#. |
| **Một PDF nguồn** bạn muốn đánh số | Tutorial sử dụng `source.pdf` làm ví dụ; thay thế đường dẫn bằng tệp của bạn. |
| **Quyền ghi** vào thư mục đầu ra | Lệnh `Save` cần ghi tệp mới. |

Bạn có thể cài đặt thư viện bằng lệnh CLI sau:

```bash
dotnet add package Aspose.Pdf
```

---

## Bước 1: Tạo dự án console mới

Mở terminal và chạy:

```bash
dotnet new console -n BatesNumberingDemo
cd BatesNumberingDemo
```

Lệnh này tạo một dự án C# tối thiểu mà chúng ta sẽ điền mã cần thiết để **thêm bates numbering**.

---

## Bước 2: Thêm các chỉ thị `using` cần thiết

Mở `Program.cs` và thêm các không gian tên ở đầu file:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;
```

* `Aspose.Pdf` cho phép bạn truy cập lớp `Document` để tải và lưu PDF.  
* `Aspose.Pdf.Text` chứa `BatesNumberingOptions`, đối tượng xác định cách hiển thị các số.

---

## Bước 3: Tải PDF nguồn

Dòng lệnh đầu tiên tải PDF bạn muốn đánh số. Thay `"YOUR_DIRECTORY/source.pdf"` bằng đường dẫn thực tế tới tệp của bạn.

```csharp
// Load the source PDF
Document pdf = new Document("YOUR_DIRECTORY/source.pdf");
```

Nếu không tìm thấy tệp, Aspose sẽ ném ra `FileNotFoundException`. Để tránh lỗi này, bạn có thể kiểm tra đường dẫn trước:

```csharp
if (!System.IO.File.Exists("YOUR_DIRECTORY/source.pdf"))
{
    Console.WriteLine("Source PDF not found.");
    return;
}
```

---

## Bước 4: Định nghĩa các tùy chọn Bates numbering

`BatesNumberingOptions` cho phép bạn kiểm soát mọi yếu tố hiển thị của việc đánh số. Ví dụ dưới đây cho cấu hình điển hình cho các hồ sơ vụ án pháp lý:

```csharp
// Define Bates numbering options
BatesNumberingOptions batesOptions = new BatesNumberingOptions
{
    Prefix = "CASE-",          // Text before the numeric part
    StartNumber = 1000,       // First number to use
    Digits = 6,               // Pad with leading zeros (e.g., 001000)
    Separator = "-",          // Character between prefix, number, and suffix
    Suffix = "-2025"          // Text after the numeric part
};
```

**Tại sao mỗi thuộc tính lại quan trọng**

| Thuộc tính | Mục đích |
|----------|---------|
| `Prefix` | Giúp bạn nhóm tài liệu theo dự án, khách hàng hoặc vụ án. |
| `StartNumber` | Đặt số đếm ban đầu; hữu ích khi đã có các tệp đã được đánh số. |
| `Digits` | Đảm bảo độ rộng đồng nhất, giúp sắp xếp dễ dàng hơn. |
| `Separator` | Cải thiện khả năng đọc, đặc biệt khi kết hợp tiền tố và hậu tố. |
| `Suffix` | Cho phép bạn thêm năm, phiên bản hoặc bất kỳ định danh nào ở cuối. |

Bạn cũng có thể kiểm soát vị trí (trên, dưới, trái, phải) và kiểu phông chữ bằng cách truy cập `batesOptions.Position` và `batesOptions.Font`. Trong hầu hết các trường hợp, mặc định (góc dưới‑phải, 12‑pt Times New Roman) hoạt động tốt.

---

## Bước 5: Áp dụng việc đánh số cho mỗi trang

Gọi `pdf.BatesNumbering.Add` sẽ chèn các số vào mỗi trang theo thứ tự xuất hiện.

```csharp
// Apply Bates numbering to every page
pdf.BatesNumbering.Add(batesOptions);
```

Nếu bạn chỉ muốn **đánh số pdf pages** trên một phần (ví dụ: bỏ qua trang bìa), bạn có thể truyền một `PageCollection` thay thế:

```csharp
// Example: skip the first page
pdf.BatesNumbering.Add(batesOptions, pdf.Pages.Skip(1));
```

---

## Bước 6: Lưu PDF đã cập nhật

Cuối cùng, ghi tài liệu đã chỉnh sửa ra đĩa. Tên tệp thường phản ánh rằng PDF hiện đã chứa số Bates.

```csharp
// Save the PDF with Bates numbers applied
pdf.Save("YOUR_DIRECTORY/bates_numbered.pdf");
Console.WriteLine("Bates numbering added successfully.");
```

Nếu thư mục đầu ra không tồn tại, Aspose sẽ tự động tạo. Tuy nhiên, bạn nên chắc chắn có quyền ghi để tránh `UnauthorizedAccessException`.

---

## Ví dụ đầy đủ, có thể chạy

Kết hợp tất cả các phần lại, đây là chương trình hoàn chỉnh mà bạn có thể sao chép, dán và chạy:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Load the source PDF
        // -------------------------------------------------
        const string inputPath = "YOUR_DIRECTORY/source.pdf";
        if (!System.IO.File.Exists(inputPath))
        {
            Console.WriteLine($"Input file not found: {inputPath}");
            return;
        }

        Document pdf = new Document(inputPath);

        // -------------------------------------------------
        // 2️⃣ Configure Bates numbering
        // -------------------------------------------------
        BatesNumberingOptions batesOptions = new BatesNumberingOptions
        {
            Prefix = "CASE-",
            StartNumber = 1000,
            Digits = 6,
            Separator = "-",
            Suffix = "-2025"
        };

        // -------------------------------------------------
        // 3️⃣ Apply the numbering to every page
        // -------------------------------------------------
        pdf.BatesNumbering.Add(batesOptions);

        // -------------------------------------------------
        // 4️⃣ Save the result
        // -------------------------------------------------
        const string outputPath = "YOUR_DIRECTORY/bates_numbered.pdf";
        pdf.Save(outputPath);
        Console.WriteLine($"Bates numbering added. Saved to {outputPath}");
    }
}
```

**Kết quả mong đợi** (console):

```
Bates numbering added. Saved to YOUR_DIRECTORY/bates_numbered.pdf
```

Mở `bates_numbered.pdf` và bạn sẽ thấy mỗi trang được gắn nhãn như `CASE-001000-2025`, `CASE-001001-2025`, v.v., nằm ở góc dưới‑phải mặc định.

---

## Câu hỏi thường gặp (FAQ)

### 1. Tôi có thể thay đổi vị trí của các số không?
Có. Đặt `batesOptions.Position = new Position(10, 10, 10, 10);` trong đó bốn giá trị đại diện cho lề từ trên, dưới, trái và phải. Aspose cũng cung cấp các enum đã định sẵn như `BatesNumberingPosition.BottomCenter`.

### 2. Nếu PDF của tôi đã có sẵn số trang thì sao?
Việc thêm số Bates sẽ **chép** lên trên các số hiện có. Để tránh lộn xộn, bạn có thể ẩn các số gốc (nếu chúng là lớp văn bản) hoặc điều chỉnh kích thước phông và vị trí trong `batesOptions`.

### 3. Điều này có hoạt động với PDF được mã hóa không?
Aspose có thể mở các PDF được bảo vệ bằng mật khẩu nếu bạn cung cấp mật khẩu:

```csharp
Document pdf = new Document("source.pdf", new LoadOptions { Password = "mySecret" });
```

Sau đó Bates numbering sẽ được áp dụng theo cách tương tự.

### 4. Làm sao để **đánh số pdf pages** chỉ với bộ đếm tuần tự đơn giản (không có prefix/suffix)?
Chỉ cần đặt `Prefix = string.Empty` và `Suffix = string.Empty`:

```csharp
BatesNumberingOptions simple = new BatesNumberingOptions
{
    StartNumber = 1,
    Digits = 4   // 0001, 0002, …
};
pdf.BatesNumbering.Add(simple);
```

### 5. Tôi có thể dùng cách này trong ASP.NET Core để phục vụ PDF ngay lập tức không?
Chắc chắn rồi. Tải tài liệu, áp dụng đánh số, rồi ghi luồng vào phản hồi HTTP:

```csharp
using (var ms = new MemoryStream())
{
    pdf.Save(ms);
    ms.Position = 0;
    return File(ms, "application/pdf", "bates_numbered.pdf");
}
```

---

## Các trường hợp đặc biệt và mẹo thực hành tốt

| Tình huống | Cách tiếp cận đề xuất |
|-----------|----------------------|
| **PDF lớn (hàng trăm trang)** | Gọi `pdf.BatesNumbering.Add` **sau** khi bạn đã thực hiện mọi biến đổi ở mức trang để tránh xử lý lại cùng một trang nhiều lần. |
| **Phông chữ tùy chỉnh** | Đặt `batesOptions.Font = FontRepository.FindFont("Arial")` và điều chỉnh `batesOptions.FontSize` để đọc tốt hơn trên tài liệu quét. |
| **Công việc batch yêu cầu hiệu năng cao** | Tái sử dụng một thể hiện `Document` duy nhất khi xử lý nhiều tệp trong vòng lặp; giải phóng nó sau mỗi lần lặp để giải bộ nhớ. |
| **Ký tự quốc tế** | Sử dụng phông chữ hỗ trợ Unicode (ví dụ: `Times New Roman Unicode`) để đảm bảo tiền tố hoặc hậu tố hiển thị đúng. |
| **Tương thích phiên bản** | Mã hoạt động với Aspose.Pdf 23.10 trở lên. Nếu bạn nhắm tới phiên bản cũ hơn, hãy kiểm tra tài liệu API để biết thay đổi tên thuộc tính. |

---

## Kết luận

Bạn đã biết cách **thêm bates numbering** vào PDF bằng Aspose.Pdf for .NET. Tutorial đã bao gồm việc tải PDF, cấu hình `BatesNumberingOptions`, áp dụng số lên mỗi trang và lưu kết quả. Với các khối xây dựng này, bạn cũng có thể triển khai **đánh số trang pdf** chung, **đánh số pdf pages** với định dạng tùy chỉnh, và tích hợp quy trình vào các pipeline tự động lớn hơn.

**Bước tiếp theo**

* Khám phá thêm API **bates numbering pdf** để tùy chỉnh phông, màu và vị trí.  
* Kết hợp kỹ thuật này với **chữ ký số** để tạo các bộ tài liệu pháp lý không thể bị giả mạo.  
* Tìm hiểu khả năng **gộp PDF** của Aspose nếu bạn cần nối nhiều hồ sơ vụ án trước khi đánh số.

Hãy thoải mái thử nghiệm các tiền tố, hậu tố và độ dài chữ số khác nhau để phù hợp với tiêu chuẩn lưu trữ của tổ chức bạn. Chúc lập trình vui vẻ!

## Bạn nên học gì tiếp theo?

Các tutorial sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật đã trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm mã mẫu đầy đủ và giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Create PDF Document C# – Add Bates Numbering Guide](/pdf/english/net/document-creation/create-pdf-document-c-add-bates-numbering-guide/)
- [How to Add Bates Numbering in PDF with C# – Complete Guide](/pdf/english/net/programming-with-stamps-and-watermarks/how-to-add-bates-numbering-in-pdf-with-c-complete-guide/)
- [Aspose PDF Tutorial – Insert a Blank Page and Update Bates Numbering](/pdf/english/net/programming-with-pdf-pages/aspose-pdf-tutorial-insert-a-blank-page-and-update-bates-num/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}