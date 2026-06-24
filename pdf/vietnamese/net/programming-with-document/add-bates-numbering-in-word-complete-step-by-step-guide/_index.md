---
category: general
date: 2026-06-21
description: Thêm đánh số Bates trong Word nhanh chóng. Tìm hiểu cách thêm Bates,
  áp dụng đánh số Bates cho tài liệu pháp lý và tự động hoá việc đánh số bằng C#.
draft: false
keywords:
- add bates numbering
- how to add bates
- bates numbering in word
- bates numbering for legal
- apply bates numbering
language: vi
og_description: Thêm đánh số Bates trong Word bằng C#. Hướng dẫn này chỉ cách thêm
  Bates, áp dụng đánh số Bates cho tài liệu pháp lý và tự động hoá quá trình.
og_title: Thêm số Bates trong Word – Hướng dẫn lập trình chi tiết
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Add Bates numbering in Word quickly. Learn how to add Bates, apply
    Bates numbering for legal docs, and automate numbering with C#.
  headline: Add Bates Numbering in Word – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Add Bates numbering in Word quickly. Learn how to add Bates, apply
    Bates numbering for legal docs, and automate numbering with C#.
  name: Add Bates Numbering in Word – Complete Step‑by‑Step Guide
  steps:
  - name: Expected Output
    text: '| Page | Bates Number | |------|--------------| | 1 | ABC-1000 | | 2 |
      ABC-1001 | | … | … | | N | ABC‑(1000 + N‑1) |'
  - name: What if the document already contains page numbers?
    text: The `AddBatesNumbering` method will **not** overwrite existing page number
      fields; it simply adds a new field. If you want to replace the existing numbers,
      remove them first or set `batesOptions.Position` to the same location as the
      current page numbers.
  - name: Can I skip pages (e.g., exclude a cover page)?
    text: 'Yes. Use the overload that accepts a `PageRange`:'
  - name: How do I change the numbering format (Roman numerals, letters)?
    text: 'The `BatesNumberingOptions` class supports a `NumberFormat` property:'
  - name: What about performance on huge files?
    text: Loading a 2‑GB Word file can consume a lot of RAM. To mitigate, process
      the document in chunks using the `DocumentSplitter` utility, apply Bates numbering
      to each chunk, then merge the parts back together. This pattern keeps memory
      usage under control while still letting you **apply bates numbering*
  type: HowTo
tags:
- document‑automation
- csharp
- legal‑tech
title: Thêm số Bates trong Word – Hướng dẫn chi tiết từng bước
url: /vi/net/programming-with-document/add-bates-numbering-in-word-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Thêm Số Bates vào Word – Hướng Dẫn Chi Tiết Từng Bước

Bạn đã bao giờ tự hỏi làm thế nào để thêm số Bates vào tệp Word mà không phải gõ từng số một không? Bạn không phải là người duy nhất. Nhiều luật sư, trợ lý pháp lý và chuyên gia e‑discovery cần một cách đáng tin cậy để **add Bates numbering** vào hàng trăm trang, và việc làm thủ công là một cơn ác mộng.

Trong hướng dẫn này, chúng tôi sẽ đi qua một giải pháp C# sạch sẽ giúp **applies Bates numbering** vào tệp `.docx`, giải thích lý do mỗi dòng quan trọng, và chỉ cho bạn cách tùy chỉnh mã cho các nhu cầu pháp lý đặc thù. Khi kết thúc, bạn sẽ có thể tạo ra một tài liệu được đánh số hoàn hảo trong vài giây—không cần plugin bổ sung.

## Những Điều Bạn Sẽ Học

- Mã chính xác cần thiết để **add Bates numbering** vào tài liệu Word.  
- Cách lớp `BatesNumberingOptions` hoạt động và lý do bạn có thể điều chỉnh tiền tố hoặc giá trị bắt đầu.  
- Mẹo sử dụng cách tiếp cận này cho các hồ sơ vụ án lớn, bao gồm các cân nhắc về bộ nhớ.  
- Tóm tắt nhanh các yêu cầu trước để bạn có thể sao chép‑dán giải pháp và chạy ngay hôm nay.  

**Prerequisites**  
- .NET 6+ (hoặc .NET Framework 4.7.2+ nếu bạn thích runtime cũ hơn).  
- Tham chiếu tới thư viện Aspose.Words cho .NET (hoặc bất kỳ API tương tự nào cung cấp `AddBatesNumbering`).  
- Kiến thức cơ bản về C# và Visual Studio (hoặc IDE yêu thích của bạn).  

Nếu bạn đã quen với những yêu cầu trên, hãy bắt đầu.

## Bước 1: Thiết Lập Dự Án và Nhập Thư Viện

Đầu tiên, tạo một ứng dụng console mới (hoặc tích hợp vào dịch vụ hiện có). Sau đó thêm gói NuGet Aspose.Words:

```bash
dotnet add package Aspose.Words
```

> **Pro tip:** Sử dụng giấy phép đánh giá miễn phí để thử nghiệm; nó sẽ thêm một watermark nhỏ nhưng vẫn hoạt động giống như phiên bản đầy đủ.

```csharp
using Aspose.Words;
using Aspose.Words.BatesNumbering;
```

Các câu lệnh `using` này đưa các lớp `Document` và `BatesNumberingOptions` vào phạm vi, chúng là cần thiết cho bước **apply bates numbering** sau này.

## Bước 2: Tải Tài Liệu Nguồn

Bạn sẽ cần một tệp Word để làm việc. Đoạn mã dưới đây tải `input.docx` từ thư mục bạn chỉ định. Thay `"YOUR_DIRECTORY"` bằng đường dẫn thực tế trên máy của bạn.

```csharp
// Step 1: Load the source document
var document = new Document("YOUR_DIRECTORY/input.docx");
```

Tại sao phải tải tệp trước? Đối tượng `Document` phân tích toàn bộ gói Word vào bộ nhớ, cho phép chúng ta thao tác header, footer và bố cục trang trước khi lưu. Nếu tệp rất lớn (ví dụ 10.000 trang), hãy cân nhắc sử dụng `LoadOptions` với `LoadFormat.Docx` để stream các phần thay vì tải toàn bộ một lúc.

## Bước 3: Cấu Hình Tùy Chọn Đánh Số Bates

Đây là nơi phép thuật xảy ra. Bạn chỉ định cho thư viện tiền tố cần dùng (`"ABC-"` trong ví dụ) và vị trí bắt đầu đếm (`1000`). Cả hai giá trị đều có thể tùy chỉnh hoàn toàn.

```csharp
// Step 2: Define Bates numbering options (prefix and starting number)
var batesOptions = new BatesNumberingOptions
{
    Prefix = "ABC-",
    Start = 1000,
    // Optional: set the position, alignment, and font if you need legal‑specific styling
    // Position = BatesNumberingPosition.Footer,
    // Alignment = BatesNumberingAlignment.Right,
    // Font = new Font("Times New Roman", 10, FontStyle.Bold)
};
```

**Why a prefix?** Trong thực hành pháp lý, tiền tố thường xác định vụ án hoặc bên cung cấp (`"ABC-"` có thể đại diện cho *Acme Bank Corp.*). Bắt đầu từ `1000` là phổ biến vì nhiều công ty giữ 999 số đầu cho bản nháp nội bộ.

Nếu bạn đang làm việc với **Bates numbering for legal** tài liệu, bạn cũng có thể muốn đặt `batesOptions.Position` thành `Header` hoặc `Footer` và điều chỉnh căn chỉnh để phù hợp với quy tắc tòa án. Thư viện hỗ trợ các điều chỉnh này ngay từ đầu.

## Bước 4: Áp Dụng Đánh Số Bates cho Toàn Bộ Tài Liệu

Bây giờ chúng ta thực sự chèn các số. Phương thức `AddBatesNumbering` duyệt qua từng trang, chèn chuỗi đã định dạng và cập nhật số trang nội bộ của tài liệu.

```csharp
// Step 3: Apply Bates numbering to the entire document
document.AddBatesNumbering(batesOptions);
```

Trong nền, Aspose.Words tạo một trường ẩn trên mỗi trang hiển thị dưới dạng `ABC-1000`, `ABC-1001`, v.v. Vì đây là một trường, bạn có thể chỉnh sửa tiền tố hoặc số bắt đầu sau này mà không cần tạo lại toàn bộ tệp—rất tiện cho **how to add bates** sau khi yêu cầu khám phá thay đổi.

## Bước 5: Lưu Tài Liệu Đã Sửa Đổi

Cuối cùng, ghi kết quả ra một tệp mới. Giữ nguyên tệp gốc không thay đổi là thực hành tốt, đặc biệt khi làm việc với bằng chứng phải giữ nguyên vẹn.

```csharp
// Step 4: Save the modified document
document.Save("YOUR_DIRECTORY/output.docx");
```

Bây giờ bạn có `output.docx` với các số Bates tuần tự được thêm vào mỗi trang. Mở nó trong Word, bạn sẽ thấy các số đúng vị trí bạn chỉ định (footer mặc định). Kích thước tệp có thể tăng nhẹ do các trường bổ sung, nhưng điều này không đáng kể so với lợi ích.

### Kết Quả Dự Kiến

| Trang | Số Bates |
|------|----------|
| 1    | ABC-1000 |
| 2    | ABC-1001 |
| …    | …        |
| N    | ABC‑(1000 + N‑1) |

Nếu bạn mở chế độ xem “Field Codes” của tài liệu (`Alt+F9` trong Word), bạn sẽ thấy một thứ giống như `{ BATES \* MERGEFORMAT ABC-1000 }` trên mỗi trang.

## Các Trường Hợp Đặc Biệt & Câu Hỏi Thường Gặp

### Nếu tài liệu đã chứa số trang thì sao?

Phương thức `AddBatesNumbering` sẽ **không** ghi đè lên các trường số trang hiện có; nó chỉ thêm một trường mới. Nếu bạn muốn thay thế các số hiện có, hãy xóa chúng trước hoặc đặt `batesOptions.Position` vào cùng vị trí với số trang hiện tại.

### Tôi có thể bỏ qua các trang (ví dụ, loại trừ trang bìa) không?

Có. Sử dụng overload chấp nhận `PageRange`:

```csharp
var range = new PageRange(2, document.PageCount); // start at page 2
document.AddBatesNumbering(batesOptions, range);
```

Điều này hữu ích khi bạn cần **bates numbering for legal** bản tóm tắt bắt đầu sau trang tiêu đề.

### Làm sao để thay đổi định dạng đánh số (số La Mã, chữ cái)?

Lớp `BatesNumberingOptions` hỗ trợ thuộc tính `NumberFormat`:

```csharp
batesOptions.NumberFormat = BatesNumberFormat.RomanUpper;
```

Đặt nó trước khi gọi `AddBatesNumbering`. Sự linh hoạt này giúp khi tòa án yêu cầu một kiểu cụ thể.

### Về hiệu năng trên các tệp lớn?

Tải một tệp Word 2 GB có thể tiêu tốn nhiều RAM. Để giảm thiểu, xử lý tài liệu thành các khối bằng công cụ `DocumentSplitter`, áp dụng Bates numbering cho mỗi khối, sau đó hợp nhất các phần lại với nhau. Mô hình này giữ mức sử dụng bộ nhớ dưới kiểm soát đồng thời vẫn cho phép bạn **apply bates numbering** hiệu quả.

## Ví Dụ Hoàn Chỉnh Hoạt Động

Kết hợp mọi thứ lại, đây là một chương trình console sẵn sàng chạy:

```csharp
using System;
using Aspose.Words;
using Aspose.Words.BatesNumbering;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the source document
            var inputPath = @"C:\Docs\input.docx";
            var document = new Document(inputPath);

            // 2️⃣ Define Bates numbering options
            var batesOptions = new BatesNumberingOptions
            {
                Prefix = "ABC-",
                Start = 1000,
                // Optional styling for legal compliance
                Position = BatesNumberingPosition.Footer,
                Alignment = BatesNumberingAlignment.Right,
                Font = new Font("Times New Roman", 9, FontStyle.Bold)
            };

            // 3️⃣ Apply Bates numbering across all pages
            document.AddBatesNumbering(batesOptions);

            // 4️⃣ Save the result
            var outputPath = @"C:\Docs\output.docx";
            document.Save(outputPath);

            Console.WriteLine($"✅ Bates numbering applied! Saved to {outputPath}");
        }
    }
}
```

Chạy chương trình, mở `output.docx`, và bạn sẽ thấy một dãy số sạch sẽ sẵn sàng cho việc nộp hồ sơ, khám phá hoặc nộp tòa án.

## Kết Luận

Bây giờ bạn đã biết chính xác **how to add Bates** vào tài liệu Word bằng C#. Các bước—tải, cấu hình, áp dụng và lưu—rất đơn giản, nhưng đủ linh hoạt để đáp ứng **Bates numbering for legal** quy trình làm việc, tiền tố tùy chỉnh và thậm chí xử lý hàng loạt quy mô lớn.

Nếu bạn muốn tiến xa hơn, hãy cân nhắc:

- Tích hợp mã vào một web API để đồng nghiệp có thể tải lên tệp và nhận PDF đã đánh số ngay lập tức.  
- Thêm xử lý lỗi cho các tệp bị thiếu hoặc vấn đề quyền (một `try/catch` nhanh quanh `Document.Load`).  
- Khám phá các tính năng khác của Aspose.Words như watermark hoặc redaction để có bộ công cụ e‑discovery đầy đủ.  

Bạn có thể thoải mái thử nghiệm với các tiền tố khác nhau, số bắt đầu khác, hoặc thậm chí kết hợp nhiều sơ đồ đánh số trong cùng một tài liệu. Thế giới của **apply bates numbering** thật bất ngờ đa dạng khi bạn đã nắm vững logic cốt lõi.

Có câu hỏi hoặc tình huống khó khăn? Để lại bình luận bên dưới, chúng tôi sẽ cùng bạn khắc phục. Chúc lập trình vui vẻ!

## Bạn Nên Học Gì Tiếp Theo?

Các hướng dẫn sau đây bao gồm các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh với giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Áp Dụng Kiểu Đánh Số trong Tiêu Đề PDF bằng Java](/pdf/english/java/pdf-images/apply-numbering-style-in-heading-of-pdf-using-java/)
- [Áp Dụng Kiểu Đánh Số trong Tiêu Đề PDF bằng Java](/pdf/german/java/pdf-images/apply-numbering-style-in-heading-of-pdf-using-java/)
- [Áp Dụng Kiểu Đánh Số trong Tiêu Đề PDF bằng Java](/pdf/french/java/pdf-images/apply-numbering-style-in-heading-of-pdf-using-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}