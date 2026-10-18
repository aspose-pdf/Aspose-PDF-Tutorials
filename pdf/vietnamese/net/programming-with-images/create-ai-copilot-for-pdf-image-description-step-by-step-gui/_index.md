---
category: general
date: 2026-08-04
description: Tạo AI Copilot để tạo mô tả hình ảnh cho các tệp PDF. Tìm hiểu cách cấu
  hình các tùy chọn hình ảnh của OpenAI và trích xuất mô tả hình ảnh một cách hiệu
  quả.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create AI copilot
- generate image description
- image description PDF
- OpenAI image options
- extract image description
language: vi
lastmod: 2026-08-04
og_description: Tạo AI Copilot để tạo mô tả hình ảnh cho các tệp PDF. Hướng dẫn này
  chỉ cho bạn cách cấu hình các tùy chọn hình ảnh của OpenAI, chạy copilot và trích
  xuất mô tả hình ảnh bằng C#.
og_image_alt: Screenshot of C# code that creates an AI copilot for PDF image description
og_title: Tạo AI Copilot cho mô tả hình ảnh PDF – hướng dẫn đầy đủ
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Create AI Copilot to generate image description for PDF files. Learn
    how to configure OpenAI image options and extract image description efficiently.
  headline: Create AI Copilot for PDF image description – step‑by‑step guide
  type: TechArticle
tags:
- Aspose.Pdf.AI
- C#
- PDF processing
title: Tạo AI Copilot cho mô tả hình ảnh PDF – hướng dẫn từng bước
url: /vi/net/programming-with-images/create-ai-copilot-for-pdf-image-description-step-by-step-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo AI Copilot cho mô tả hình ảnh PDF – hướng dẫn đầy đủ

Nếu bạn cần **tạo AI Copilot** tự động viết mô tả cho các hình ảnh được nhúng trong một tệp PDF, hướng dẫn này sẽ chỉ cho bạn cách thực hiện chính xác. Bạn sẽ học cách cấu hình các tùy chọn hình ảnh OpenAI, chạy copilot và **trích xuất mô tả hình ảnh** mà không rời khỏi dự án C# của mình.

Việc tạo nội dung văn bản cho các hình ảnh trong PDF là một yêu cầu phổ biến cho khả năng tiếp cận, lập chỉ mục nội dung và báo cáo tự động. Khi kết thúc tutorial này, bạn sẽ có một thành phần có thể tái sử dụng để **tạo mô tả hình ảnh** cho bất kỳ tài liệu PDF nào bạn chỉ định.

## Yêu cầu trước

* .NET 6.0 hoặc mới hơn đã được cài đặt  
* Giấy phép Aspose.Pdf.AI (hoặc bản dùng thử miễn phí)  
* Khóa API OpenAI mà client Aspose có thể sử dụng  
* Visual Studio 2022 (hoặc bất kỳ IDE nào hỗ trợ C#)  

Không cần thêm bất kỳ gói NuGet nào ngoài `Aspose.Pdf.AI`.

## Bước 1: Thiết lập client Aspose.Pdf.AI

Bước đầu tiên là khởi tạo client AI với chi tiết xác thực của bạn. Client sẽ xử lý việc giao tiếp với dịch vụ OpenAI phía sau.

```csharp
using Aspose.Pdf.AI;
using Aspose.Pdf.AI.Models;

// Replace with your actual credentials
var client = new AiClient(new AiClientOptions
{
    ApiKey = Environment.GetEnvironmentVariable("OPENAI_API_KEY"),
    // Optional: set a custom endpoint if you use Azure OpenAI
    // Endpoint = "https://my-openai-instance.openai.azure.com/"
});
```

**Tại sao điều này quan trọng:** `AiClient` bao bọc tất cả các cài đặt cấp yêu cầu (API key, timeout, retry policy). Tạo một lần và tái sử dụng nó cho nhiều instance copilot giảm tải và đảm bảo xác thực nhất quán.

## Bước 2: Tạo một Image Description Copilot

Bây giờ bạn sẽ tạo **AI copilot** sẽ đọc PDF và tạo mô tả cho mỗi hình ảnh. Phương thức factory `CreateImageDescriptionCopilot` nhận client và một tập hợp các tùy chọn xác định cách mô tả được tạo.

```csharp
// Configure OpenAI image options – this is where you control model, temperature, etc.
var imageOptions = OpenAIImageDescriptionOptions.Create()
    .WithModel("gpt-4o-mini")           // Choose a model that balances cost and quality
    .WithTemperature(0.7)               // Controls creativity; 0 = deterministic
    .WithMaxTokens(150);                // Maximum length of each description

// Point the copilot at the PDF you want to process
var imgCopilot = AICopilotFactory.CreateImageDescriptionCopilot(
    client,
    imageOptions.WithDocument(@"C:\Reports\AnnualReport.pdf"));
```

**Tại sao điều này quan trọng:**  
* `OpenAIImageDescriptionOptions` (the **OpenAI image options**) cho phép bạn tinh chỉnh mô hình ngôn ngữ. Điều chỉnh temperature hoặc model có thể cải thiện độ liên quan cho sơ đồ kỹ thuật so với ảnh tự nhiên.  
* Xác định đường dẫn tài liệu cho copilot biết PDF nào cần quét. Copilot sẽ trích xuất mọi hình raster, gửi chúng tới model và trả về mô tả có thể đọc được bởi con người.

## Bước 3: Lấy mô tả đã tạo một cách bất đồng bộ

Copilot hoạt động bất đồng bộ vì có thể cần tải lên vài megabyte dữ liệu hình ảnh và chờ phản hồi từ model. Sử dụng `await` để đảm bảo lời gọi hoàn thành trước khi bạn truy cập kết quả.

```csharp
try
{
    // Get a dictionary where the key is the page number and the value is the description
    var descriptionMap = await imgCopilot.GetDescriptionAsync();

    // Example: iterate over each image description
    foreach (var entry in descriptionMap)
    {
        Console.WriteLine($"Page {entry.Key}: {entry.Value}");
    }
}
catch (AiException ex)
{
    Console.Error.WriteLine($"AI service error: {ex.Message}");
}
```

**Tại sao điều này quan trọng:** Phương thức trả về một `Dictionary<int, string>` ánh xạ mỗi trang (hoặc chỉ mục hình ảnh) tới mô tả của nó. Xử lý `AiException` cho phép bạn hiển thị lỗi mạng hoặc hạn ngạch thay vì làm ứng dụng bị sập.

## Bước 4: Hiển thị hoặc lưu mô tả

Bạn có thể ghi các mô tả ra console, tệp log, hoặc nhúng chúng trở lại PDF dưới dạng alt‑text để tăng khả năng tiếp cận. Dưới đây là một ví dụ nhanh ghi đầu ra vào tệp JSON để sử dụng sau.

```csharp
using System.Text.Json;

// Serialize the map to JSON
var json = JsonSerializer.Serialize(descriptionMap, new JsonSerializerOptions { WriteIndented = true });
File.WriteAllText(@"C:\Reports\ImageDescriptions.json", json);

Console.WriteLine("Image descriptions saved to ImageDescriptions.json");
```

**Tại sao điều này quan trọng:** Lưu đầu ra dưới dạng JSON giữ nguyên mối liên kết giữa mỗi trang và mô tả của nó, giúp các quy trình downstream (lập chỉ mục tìm kiếm, hiển thị UI, v.v.) dễ dàng tiêu thụ dữ liệu.

## Xử lý nhiều hình ảnh trên mỗi trang

Nếu một trang chứa nhiều hình ảnh, copilot trả về một mô tả nối liền được ngăn cách bằng dấu ngắt dòng. Để tách chúng, kiểm tra kết quả thô và tách bằng `\n\n` (dòng mới đôi). Dưới đây là một phương thức trợ giúp:

```csharp
static IEnumerable<string> SplitDescriptions(string combined)
{
    return combined.Split(new[] { "\n\n" }, StringSplitOptions.RemoveEmptyEntries);
}
```

Bạn có thể lặp qua từng mô tả hình ảnh riêng lẻ và lưu chúng riêng nếu cần.

## Trường hợp đặc biệt: PDF lớn và quản lý timeout

Xử lý một PDF lớn hơn 100 MB có thể vượt quá timeout HTTP mặc định. Điều chỉnh cài đặt timeout của client khi bạn tạo `AiClient`:

```csharp
var client = new AiClient(new AiClientOptions
{
    ApiKey = Environment.GetEnvironmentVariable("OPENAI_API_KEY"),
    Timeout = TimeSpan.FromMinutes(5)   // Increase timeout for heavy workloads
});
```

Tăng timeout ngăn việc kết thúc sớm khi dịch vụ đang xử lý nhiều hình ảnh độ phân giải cao.

## Mẹo chuyên nghiệp: Lưu cache kết quả để giảm chi phí

OpenAI tính phí theo token, và mô tả hình ảnh có thể lặp lại qua các phiên bản của cùng một báo cáo. Lưu cache đầu ra JSON và tái sử dụng khi hash PDF trùng với tệp đã xử lý trước đó. Thực hành này tiết kiệm tiền và tăng tốc các lần chạy sau.

```csharp
static string ComputeFileHash(string path)
{
    using var sha256 = System.Security.Cryptography.SHA256.Create();
    using var stream = File.OpenRead(path);
    var hash = sha256.ComputeHash(stream);
    return Convert.ToHexString(hash);
}
```

Lưu hash cùng với tệp JSON; nếu hash trùng trong lần chạy sau, bỏ qua lời gọi AI.

## Ví dụ đầy đủ có thể chạy được

Kết hợp mọi thứ lại, đây là một ứng dụng console tự chứa mà bạn có thể dán vào một dự án .NET mới.

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using System.Text.Json;
using System.Threading.Tasks;
using Aspose.Pdf.AI;
using Aspose.Pdf.AI.Models;

class Program
{
    static async Task Main()
    {
        // 1️⃣ Initialize AI client
        var client = new AiClient(new AiClientOptions
        {
            ApiKey = Environment.GetEnvironmentVariable("OPENAI_API_KEY"),
            Timeout = TimeSpan.FromMinutes(5)
        });

        // 2️⃣ Configure OpenAI image options and create copilot
        var imageOptions = OpenAIImageDescriptionOptions.Create()
            .WithModel("gpt-4o-mini")
            .WithTemperature(0.7)
            .WithMaxTokens(150);

        string pdfPath = @"C:\Reports\AnnualReport.pdf";

        var imgCopilot = AICopilotFactory.CreateImageDescriptionCopilot(
            client,
            imageOptions.WithDocument(pdfPath));

        // 3️⃣ Retrieve descriptions
        Dictionary<int, string> descriptionMap;
        try
        {
            descriptionMap = await imgCopilot.GetDescriptionAsync();
        }
        catch (AiException ex)
        {
            Console.Error.WriteLine($"Error from AI service: {ex.Message}");
            return;
        }

        // 4️⃣ Output results
        foreach (var entry in descriptionMap)
        {
            Console.WriteLine($"Page {entry.Key}:");
            Console.WriteLine(entry.Value);
            Console.WriteLine(new string('-', 40));
        }

        // 5️⃣ Save to JSON for later use
        string json = JsonSerializer.Serialize(descriptionMap, new JsonSerializerOptions { WriteIndented = true });
        string jsonPath = Path.ChangeExtension(pdfPath, ".descriptions.json");
        await File.WriteAllTextAsync(jsonPath, json);
        Console.WriteLine($"Descriptions saved to {jsonPath}");
    }
}
```

**Expected output (truncated)**

```
Page 2:
A bar chart showing quarterly revenue growth, with blue bars representing Q1–Q4.
----------------------------------------
Page 5:
A high‑resolution photograph of the new manufacturing facility, showing the assembly line in operation.
...
Descriptions saved to C:\Reports\AnnualReport.descriptions.json
```

Chương trình đọc `AnnualReport.pdf`, tạo một **AI copilot**, và ghi một tệp JSON ánh xạ mỗi trang tới mô tả đã tạo.

## Câu hỏi thường gặp

* **Liệu điều này có hoạt động với PDF được mã hóa không?**  
  Có, nhưng bạn phải cung cấp mật khẩu khi tạo copilot:  
  `imageOptions.WithPassword("mySecret")`.

* **Tôi có thể giới hạn xử lý chỉ ở một số trang cụ thể không?**  
  Sử dụng `imageOptions.WithPageRange(1, 10)` để giới hạn copilot chỉ xử lý các trang 1‑10.

* **Nếu một hình ảnh chứa văn bản thì sao?**  
  Model cố gắng mô tả nội dung hình ảnh; để trích xuất văn bản dạng OCR, bạn nên sử dụng `CreateTextExtractionCopilot` thay thế.

## Kết luận

Bây giờ bạn đã biết cách **tạo AI Copilot** để **tạo mô tả hình ảnh** cho các tệp PDF, cấu hình **các tùy chọn hình ảnh OpenAI**, và **trích xuất mô tả hình ảnh** một cách lập trình trong C#. Ví dụ đầy đủ minh họa các thực tiễn tốt nhất như xử lý async, quản lý lỗi, và lưu cache kết quả.

Tiếp theo, bạn có thể khám phá:

* Thêm các mô tả đã tạo trở lại PDF dưới dạng alt‑text để cải thiện khả năng tiếp cận (`PdfDocument` → `PdfImage.AlternativeText`).  
* Sử dụng cùng mẫu copilot để **tạo báo cáo PDF mô tả hình ảnh** cho xử lý hàng loạt.  
* Thử nghiệm các model OpenAI khác nhau hoặc cài đặt temperature để tinh chỉnh phong cách mô tả.

Hãy tự do điều chỉnh mã, thử nghiệm với tài liệu lớn hơn, và tích hợp đầu ra vào pipeline lập chỉ mục của bạn. Chúc lập trình vui vẻ!

## Bạn nên học gì tiếp theo?

Các tutorial sau đây bao gồm các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoạt động đầy đủ với các giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Create Pdf With Tagged Image In Java](/pdf/hindi/java/pdf-structure-elements/create-pdf-with-tagged-image-in-java/)
- [Create Pdf With Tagged Image](/pdf/hindi/net/programming-with-tagged-pdf/create-pdf-with-tagged-image/)
- [Create Tagged Pdf Image Dotnet](/pdf/hindi/net/images-graphics/create-tagged-pdf-image-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}