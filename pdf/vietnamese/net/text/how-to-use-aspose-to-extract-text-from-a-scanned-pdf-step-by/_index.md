---
category: general
date: 2026-08-04
description: Cách sử dụng Aspose để trích xuất văn bản từ PDF đã quét và chuyển PDF
  sang văn bản bằng C#. Học cách đọc các tệp PDF đã quét và nhận kết quả OCR đáng
  tin cậy.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use aspose
- extract scanned pdf text
- convert pdf to text
- read scanned pdf
- how to extract text
language: vi
lastmod: 2026-08-04
og_description: Cách sử dụng Aspose để đọc các tệp PDF đã quét, trích xuất văn bản
  từ PDF đã quét và chuyển PDF sang văn bản với một ví dụ đầy đủ, có thể chạy được.
og_image_alt: Screenshot showing how to use Aspose OCR copilot to extract text from
  a scanned PDF
og_title: Cách sử dụng Aspose – trích xuất văn bản từ PDF đã quét bằng C#
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: How to use Aspose to extract scanned PDF text and convert PDF to text
    with C#. Learn to read scanned PDF files and get reliable OCR results.
  headline: How to use Aspose to extract text from a scanned PDF – step‑by‑step guide
  type: TechArticle
- questions:
  - answer: Yes. Add `.WithPassword("yourPassword")` to the options builder before
      creating the copilot.
    question: Does this work with password‑protected PDFs?
  - answer: Use `GetTextStructureAsync()` instead of `GetTextAsync()`. The method
      returns a JSON payload that includes page indices, bounding boxes, and confidence
      scores.
    question: Can I extract text in a structured format (e.g., JSON with page numbers)?
  - answer: 'The plain‑text extraction flattens tables into line‑break‑separated rows.
      For richer data, request the PDF‑to‑HTML conversion (`GetHtmlAsync`) and parse
      the HTML table elements. ## Conclusion You now know **how to use Aspose** to
      read a scanned PDF, extract scanned PDF text, and **convert PDF to tex'
    question: What if the PDF contains tables?
  type: FAQPage
tags:
- Aspose.PDF.AI
- OCR
- C#
- PDF processing
title: Cách sử dụng Aspose để trích xuất văn bản từ PDF đã quét – hướng dẫn từng bước
url: /vi/net/text/how-to-use-aspose-to-extract-text-from-a-scanned-pdf-step-by/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách sử dụng Aspose để trích xuất văn bản từ PDF đã quét – hướng dẫn từng bước

Nếu bạn cần **cách sử dụng Aspose** cho OCR, hướng dẫn này sẽ chỉ cho bạn cách trích xuất văn bản PDF đã quét chỉ trong vài dòng C#. Dù bạn đang xây dựng dịch vụ lưu trữ tài liệu hay chỉ mục tìm kiếm cho các tài liệu giấy cũ, giải pháp này hoạt động với bất kỳ PDF đã quét nào bạn đưa vào dịch vụ Aspose.Pdf.AI.

Trong tutorial này bạn sẽ:

* Tạo một OCR copilot để đọc PDF đã quét.
* Trích xuất văn bản đã nhận dạng một cách bất đồng bộ.
* Hiển thị hoặc xử lý tiếp chuỗi văn bản đã trích xuất.

Điều kiện duy nhất là bạn có một thuê bao Aspose.Pdf.AI đang hoạt động và môi trường phát triển .NET 6 (hoặc mới hơn).

## Các yêu cầu trước

| Yêu cầu | Lý do quan trọng |
|-------------|----------------|
| .NET 6 SDK hoặc mới hơn | Cung cấp `async Main` và các tính năng ngôn ngữ hiện đại. |
| Gói NuGet Aspose.Pdf.AI (`Aspose.Pdf.AI`) | Chứa `AICopilotFactory` và các tùy chọn OCR. |
| Một thể hiện `client` Aspose.Pdf.AI hợp lệ (API key) | Xác thực các yêu cầu của bạn tới dịch vụ đám mây. |
| Tệp PDF đã quét (ví dụ, `Scanned.pdf`) | Tài liệu nguồn mà từ đó văn bản sẽ được trích xuất. |

Cài đặt gói bằng .NET CLI:

```bash
dotnet add package Aspose.Pdf.AI
```

## Bước 1: Thiết lập client Aspose.Pdf.AI

Trước khi bạn có thể gọi bất kỳ endpoint OCR nào, bạn phải tạo một client chứa thông tin xác thực API của mình. Client này an toàn với đa luồng và có thể tái sử dụng cho nhiều tài liệu.

```csharp
using Aspose.Pdf.AI;
using Aspose.Pdf.AI.Models;

// Replace with your actual API key and base URL if you use a private cloud.
var client = new PdfAiClient(new PdfAiConfiguration
{
    ApiKey = "YOUR_API_KEY",
    // BaseUrl = "https://api.aspose.cloud" // default, change only if needed
});
```

**Tại sao bước này cần thiết** – Dịch vụ Aspose xác thực mỗi yêu cầu dựa trên thuê bao của bạn. Tạo client một lần giúp tránh các lần bắt tay mạng lặp lại và giữ cho mã sạch sẽ.

## Bước 2: Tạo một OCR copilot cho tài liệu PDF đã quét

`AICopilotFactory` xây dựng một OCR copilot chuyên biệt biết cách xử lý tệp mà bạn chỉ định. Bạn truyền `client` và một đối tượng `OpenAIOcrOptions` chỉ tới đường dẫn PDF.

```csharp
using Aspose.Pdf.AI;

// Step 2: Build the OCR copilot
var ocrCopilot = AICopilotFactory.CreateOcrCopilot(
    client,                                   // Your Aspose.Pdf.AI client instance
    OpenAIOcrOptions.Create()
        .WithDocument("YOUR_DIRECTORY/Scanned.pdf") // Path to the scanned PDF
);
```

**Giải thích** – `CreateOcrCopilot` bao gói tất cả các cuộc gọi HTTP cấp thấp. Phương thức `WithDocument` cho dịch vụ biết tệp nào cần phân tích; bạn cũng có thể cung cấp một `Stream` nếu PDF nằm trong bộ nhớ.

## Bước 3: Trích xuất văn bản đã nhận dạng một cách bất đồng bộ

Gọi `GetTextAsync` thực hiện thao tác OCR trên đám mây và trả về kết quả dạng văn bản thuần. Vì thao tác này có thể mất vài giây, phương thức được thiết kế bất đồng bộ.

```csharp
// Step 3: Perform OCR and get the text
string ocrText = await ocrCopilot.GetTextAsync();
```

**Tại sao phải bất đồng bộ?** – Độ trễ mạng và thời gian xử lý OCR không thể đoán trước. Sử dụng `await` ngăn ứng dụng của bạn bị chặn luồng chính, điều này đặc biệt quan trọng trong các kịch bản UI hoặc dịch vụ web.

## Bước 4: Sử dụng văn bản đã trích xuất

Tại thời điểm này bạn đã có một `string` .NET thông thường chứa toàn bộ bản sao của PDF đã quét. Bạn có thể ghi nó ra console, lưu vào cơ sở dữ liệu, hoặc đưa vào công cụ tìm kiếm.

```csharp
// Step 4: Display the result
Console.WriteLine("=== OCR Result ===");
Console.WriteLine(ocrText);
```

### Đầu ra mong đợi

Nếu `Scanned.pdf` chứa một trang duy nhất với câu “Hello, world!”, console sẽ hiển thị:

```
=== OCR Result ===
Hello, world!
```

Đối với tài liệu đa trang, đầu ra sẽ nối các văn bản của từng trang lại với nhau, giữ nguyên các ngắt dòng.

## Ví dụ đầy đủ, có thể chạy ngay

Dưới đây là một chương trình hoàn chỉnh mà bạn có thể dán vào một dự án console mới (`dotnet new console`). Nó minh họa **cách sử dụng Aspose** từ đầu đến cuối, bao gồm xử lý lỗi cho các vấn đề thường gặp.

```csharp
using System;
using System.Threading.Tasks;
using Aspose.Pdf.AI;
using Aspose.Pdf.AI.Models;

namespace AsposeOcrDemo
{
    class Program
    {
        static async Task Main(string[] args)
        {
            // 1️⃣ Initialize the Aspose.Pdf.AI client
            var client = new PdfAiClient(new PdfAiConfiguration
            {
                ApiKey = "YOUR_API_KEY"
                // BaseUrl = "https://api.aspose.cloud" // optional
            });

            // 2️⃣ Build the OCR copilot for the target PDF
            var pdfPath = "YOUR_DIRECTORY/Scanned.pdf";
            var ocrCopilot = AICopilotFactory.CreateOcrCopilot(
                client,
                OpenAIOcrOptions.Create().WithDocument(pdfPath)
            );

            try
            {
                // 3️⃣ Extract text asynchronously
                string ocrText = await ocrCopilot.GetTextAsync();

                // 4️⃣ Use the extracted text (display in console)
                Console.WriteLine("=== OCR Result ===");
                Console.WriteLine(ocrText);
            }
            catch (Exception ex)
            {
                // Common errors: invalid API key, missing file, unsupported PDF version
                Console.Error.WriteLine($"Error during OCR: {ex.Message}");
            }
        }
    }
}
```

**Các điểm quan trọng trong ví dụ**

* `await` đảm bảo thực thi không chặn.
* Khối `try/catch` hiển thị lỗi mạng hoặc dịch vụ, điều này rất cần thiết khi **đọc PDF đã quét** ở quy mô lớn.
* Thay `YOUR_API_KEY` và `YOUR_DIRECTORY/Scanned.pdf` bằng giá trị thực tế trước khi chạy.

## Xử lý các trường hợp đặc biệt và mẹo thực hành tốt

| Tình huống | Phương pháp đề xuất |
|-----------|----------------------|
| **PDF lớn ( > 50 MB )** | Chia tài liệu thành các phần nhỏ hơn phía client và xử lý mỗi phần bằng một copilot riêng. Điều này giảm áp lực bộ nhớ và cải thiện độ tin cậy. |
| **Quét chất lượng thấp** | Điều chỉnh chất lượng OCR bằng cách thêm `.WithLanguage("eng")` hoặc `.WithEnhanceImage(true)` vào `OpenAIOcrOptions`. Dịch vụ hỗ trợ gợi ý ngôn ngữ giúp tăng độ chính xác. |
| **Nhiều ngôn ngữ** | Cung cấp danh sách ngăn cách bằng dấu phẩy, ví dụ `.WithLanguage("eng,spa")`. Engine OCR sẽ phát hiện và sao chép cả hai ngôn ngữ. |
| **Tệp ảnh không phải PDF** | Chuyển đổi ảnh sang PDF trước (`Aspose.Pdf` library) hoặc sử dụng `OpenAIOcrOptions.WithImage` để gửi ảnh trực tiếp. |
| **Vượt quá giới hạn tốc độ** | Thực hiện back‑off theo cấp số nhân và logic retry; API Aspose trả về HTTP 429 khi bạn vượt quá hạn ngạch. |

### Mẹo chuyên nghiệp

Lưu cache kết quả `ocrText` nếu bạn dự định tái sử dụng sau này. Thao tác OCR là phần tốn kém nhất của quy trình, và việc tái sử dụng chuỗi sẽ tránh các cuộc gọi API trùng lặp và tiết kiệm credit.

## Câu hỏi thường gặp

**H: Điều này có hoạt động với PDF được bảo mật bằng mật khẩu không?**  
Đ: Có. Thêm `.WithPassword("yourPassword")` vào builder tùy chọn trước khi tạo copilot.

**H: Tôi có thể trích xuất văn bản ở định dạng có cấu trúc (ví dụ, JSON kèm số trang) không?**  
Đ: Sử dụng `GetTextStructureAsync()` thay vì `GetTextAsync()`. Phương thức này trả về payload JSON bao gồm chỉ số trang, bounding box và điểm tin cậy.

**H: Nếu PDF chứa bảng thì sao?**  
Đ: Việc trích xuất văn bản thuần sẽ làm phẳng các bảng thành các hàng ngăn cách bằng ngắt dòng. Để có dữ liệu phong phú hơn, yêu cầu chuyển PDF sang HTML (`GetHtmlAsync`) và phân tích các phần tử bảng trong HTML.

## Kết luận

Bạn đã biết **cách sử dụng Aspose** để đọc PDF đã quét, trích xuất văn bản PDF đã quét, và **chuyển PDF sang văn bản** bằng một chương trình C# tối thiểu. Quy trình bao gồm tạo OCR copilot, gọi `GetTextAsync`, và xử lý chuỗi kết quả. Bằng cách tuân theo các khuyến nghị cho các trường hợp đặc biệt, bạn có thể mở rộng giải pháp cho các lô tài liệu lớn, nội dung đa ngôn ngữ và PDF bảo mật.

Tiếp theo, bạn có thể khám phá:

* **Cách trích xuất văn bản** với bảo toàn bố cục (`GetHtmlAsync`).
* Sử dụng Aspose.Pdf.AI để **trích xuất bảng** và xuất chúng ra CSV.
* Tích hợp đầu ra OCR với Azure Cognitive Search để tạo kho lưu trữ tài liệu có thể tìm kiếm.

Chúc lập trình vui vẻ, và tận hưởng độ chính xác mà OCR AI của Aspose mang lại cho quy trình PDF đã quét của bạn!

## Bạn nên học gì tiếp theo?

Các tutorial sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm mã mẫu đầy đủ với giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Extract Text from PDF Files Using Aspose.PDF for .NET](/pdf/english/net/text-operations/extract-text-pdf-aspose-dotnet/)
- [How to Extract Text from Specific Regions in PDFs Using Aspose.PDF for .NET](/pdf/english/net/text-operations/extract-text-specific-region-aspose-pdf-net/)
- [How to Extract Highlighted Text from PDFs Using Aspose.PDF for .NET](/pdf/english/net/text-operations/extract-highlighted-text-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}