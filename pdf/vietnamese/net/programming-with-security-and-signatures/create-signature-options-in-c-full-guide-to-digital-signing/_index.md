---
category: general
date: 2026-08-14
description: Tạo các tùy chọn chữ ký trong C# để áp dụng chữ ký số. Tìm hiểu cách
  cấu hình chữ ký, triển khai hàm băm tùy chỉnh và ký tài liệu một cách lập trình.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create signature options
- custom hash function
- apply digital signature
- how to sign document
- how to configure signature
language: vi
lastmod: 2026-08-14
og_description: Tạo các tùy chọn chữ ký trong C# và áp dụng chữ ký số. Hướng dẫn này
  sẽ chỉ cho bạn cách cấu hình chữ ký, thêm hàm băm tùy chỉnh và ký một tài liệu.
og_image_alt: Code editor view showing C# creation of signature options and document
  signing
og_title: Tạo các tùy chọn chữ ký trong C# – hướng dẫn ký số từng bước
schemas:
- author: GroupDocs
  dateModified: '2026-08-14'
  description: Create signature options in C# to apply digital signature. Learn how
    to configure signature, implement a custom hash function, and sign documents programmatically.
  headline: Create signature options in C# – full guide to digital signing
  type: TechArticle
- description: Create signature options in C# to apply digital signature. Learn how
    to configure signature, implement a custom hash function, and sign documents programmatically.
  name: Create signature options in C# – full guide to digital signing
  steps:
  - name: '**Hash calculation** – now delegated to your custom hash function.'
    text: '**Hash calculation** – now delegated to your custom hash function.'
  - name: '**Signature generation** – using the private key supplied to the library’s
      configuration.'
    text: '**Signature generation** – using the private key supplied to the library’s
      configuration.'
  - name: '**Embedding** – the generated signature is attached to the output file.'
    text: '**Embedding** – the generated signature is attached to the output file.'
  type: HowTo
tags:
- digital signature
- C#
- security
title: Tạo các tùy chọn chữ ký trong C# – hướng dẫn đầy đủ về ký số
url: /vi/net/programming-with-security-and-signatures/create-signature-options-in-c-full-guide-to-digital-signing/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo tùy chọn chữ ký trong C# – hướng dẫn đầy đủ về ký số

Tạo tùy chọn chữ ký trong C# để cấu hình quy trình ký số. Hướng dẫn này cho thấy cách áp dụng chữ ký số, triển khai hàm băm tùy chỉnh, và ký một tài liệu bằng lớp `SignatureOptions`. Nếu bạn từng cần ký một tệp PDF, XML, hoặc bất kỳ tải trọng nhị phân nào từ ứng dụng .NET, các bước dưới đây sẽ cung cấp cho bạn một giải pháp sẵn sàng chạy.

Bạn sẽ học cách:

* cấu hình `SignatureOptions` với thuật toán băm tùy chỉnh,
* gọi phương thức ký một cách chính xác,
* xác minh rằng chữ ký đã được áp dụng,
* tránh các lỗi thường gặp khi cấu hình chữ ký.

Các yêu cầu tiên quyết duy nhất là một .NET SDK mới (≥ .NET 6) và một thư viện ký mà cung cấp `SignatureOptions` (ví dụ, **GroupDocs.Signature**, **Aspose.Signature**, hoặc một API tương tự). Không cần công cụ bên ngoài.

---

## Prerequisites

| Requirement | Why it matters |
|-------------|----------------|
| .NET 6 SDK hoặc phiên bản mới hơn | Cung cấp các tính năng ngôn ngữ hiện đại được sử dụng trong các ví dụ. |
| Gói NuGet của thư viện ký (ví dụ, `GroupDocs.Signature`) | Cung cấp kiểu `SignatureOptions` và phương thức mở rộng `Sign`. |
| Truy cập vào khóa riêng hoặc chứng chỉ | Cần thiết để tạo chữ ký số có thể xác thực được. |

Cài đặt thư viện bằng CLI tiêu chuẩn:

```bash
dotnet add package GroupDocs.Signature
```

---

## Step 1: Create signature options

Bước đầu tiên là khởi tạo `SignatureOptions` và đặt các thuộc tính kiểm soát quá trình ký. Đối tượng này cho thư viện biết *cái gì* cần ký và *cách* ký nó.

```csharp
using GroupDocs.Signature;
using GroupDocs.Signature.Options;

// Create a new SignatureOptions instance
var signatureOptions = new SignatureOptions
{
    // The signing algorithm (e.g., RSA‑SHA256) is defined by the library.
    // You can also set visual appearance, page number, etc., here.
    // For this tutorial we focus on the custom hash function.
};
```

**Why this matters:** `SignatureOptions` hoạt động như một hợp đồng giữa mã của bạn và engine ký. Bằng cách cấu hình trước, bạn tránh việc lặp lại mã boilerplate khi ký nhiều tài liệu.

---

## Step 2: Implement a custom hash function

Một *custom hash function* cho phép bạn kiểm soát hoàn toàn digest mà thuật toán chữ ký sẽ ký. Điều này hữu ích khi hàm băm mặc định (SHA‑256) không đáp ứng yêu cầu tuân thủ hoặc khi bạn cần băm một phần của tài liệu.

```csharp
using System.Security.Cryptography;
using System.Text;

// Define a delegate that matches the library’s expected signature
Func<byte[], byte[]> MyHash = data =>
{
    // Example: compute SHA‑512 and then truncate to 256 bits
    using var sha512 = SHA512.Create();
    var fullHash = sha512.ComputeHash(data);

    // Truncate to the first 32 bytes (256 bits)
    var truncated = new byte[32];
    Buffer.BlockCopy(fullHash, 0, truncated, 0, truncated.Length);
    return truncated;
};

// Attach the custom hash to the options
signatureOptions.CustomSignHash = hash => MyHash(hash);
```

**Why this matters:** Bằng cách gán `CustomSignHash`, bạn thay thế bước băm nội bộ của thư viện bằng `MyHash`. Engine ký sẽ ký các byte do hàm của bạn trả về, đảm bảo tuân thủ bất kỳ chính sách tùy chỉnh nào.

---

## Step 3: Load the document and apply digital signature

Với các tùy chọn đã chuẩn bị, bạn có thể mở tệp mục tiêu và gọi phương thức ký. Phương thức `Sign` được cung cấp bởi thư viện và sử dụng `SignatureOptions` đã cấu hình.

```csharp
using System.IO;

// Path to the file you want to sign
string inputPath = @"C:\Docs\contract.pdf";
string outputPath = @"C:\Docs\contract.signed.pdf";

// Load the document into the Signature object
using var signature = new Signature(inputPath);

// Sign the document using the previously created options
bool result = signature.Sign(outputPath, signatureOptions);

if (!result)
{
    throw new InvalidOperationException("The document could not be signed.");
}
```

**Why this matters:** Lệnh gọi `Sign` thực hiện ba hành động nội bộ:

1. **Hash calculation** – hiện được giao cho hàm băm tùy chỉnh của bạn.  
2. **Signature generation** – sử dụng khóa riêng được cung cấp trong cấu hình của thư viện.  
3. **Embedding** – chữ ký đã tạo được gắn vào tệp đầu ra.  

Nếu bất kỳ bước nào thất bại, phương thức sẽ trả về `false`, cho phép bạn xử lý lỗi một cách nhẹ nhàng.

---

## Step 4: Verify that the document is signed

Một bước xác minh nhanh giúp chắc chắn rằng chữ ký đã được áp dụng đúng cách. Hầu hết các thư viện cung cấp phương thức `Verify` để kiểm tra tính toàn vẹn của tệp đã ký.

```csharp
using var verifier = new Signature(outputPath);
var verificationResult = verifier.Verify();

Console.WriteLine(verificationResult
    ? "Signature verified successfully."
    : "Signature verification failed.");
```

**Why this matters:** Việc xác minh đảm bảo tài liệu đã ký không bị thay đổi sau khi ký và hàm băm tùy chỉnh đã tạo ra một digest tương thích.

---

## How to configure signature for different file types

Cùng một đối tượng `SignatureOptions` có thể được tái sử dụng cho PDF, tài liệu Word, hình ảnh, hoặc các tệp nhị phân thuần. Thay đổi duy nhất cần thiết là lớp tùy chọn cụ thể (ví dụ, `PdfSignatureOptions`, `WordSignatureOptions`). Dưới đây là một ví dụ nhanh cho ảnh JPEG:

```csharp
using GroupDocs.Signature.Options;

var imageOptions = new ImageSignatureOptions
{
    // Position the signature on the image
    Left = 100,
    Top = 50,
    Width = 150,
    Height = 50,
    CustomSignHash = hash => MyHash(hash)   // reuse the same custom hash
};

using var imgSignature = new Signature(@"C:\Images\photo.jpg");
imgSignature.Sign(@"C:\Images\photo.signed.jpg", imageOptions);
```

**Why this matters:** Hiểu cách *configure signature* cho mỗi định dạng cho phép bạn mở rộng cùng một codebase sang nhiều loại tài liệu mà không phải viết lại logic băm.

---

## Common pitfalls and best practices

| Pitfall | Recommended fix |
|---------|-----------------|
| Quên đặt `CustomSignHash` sau khi tạo `SignatureOptions` | Gán delegate ngay sau khi khởi tạo đối tượng tùy chọn. |
| Sử dụng thuật toán băm mà chứng chỉ ký không hỗ trợ | Kiểm tra rằng mục đích sử dụng khóa của chứng chỉ phù hợp với độ dài băm (ví dụ, RSA‑2048 với SHA‑512). |
| Bỏ qua việc giải phóng các đối tượng `Signature` | Đặt thể hiện `Signature` trong khối `using` để giải phóng các handle tệp. |
| Ghi đè tệp đã ký lên nguồn gốc | Luôn ghi vào một đường dẫn tệp mới (`outputPath`) để bảo toàn tài liệu gốc. |

---

## Full working example

Dưới đây là một chương trình tự chứa, kết hợp tất cả các phần lại với nhau. Sao chép nó vào một dự án console mới và chạy; console sẽ báo thành công hoặc thất bại.

```csharp
using System;
using System.IO;
using System.Security.Cryptography;
using GroupDocs.Signature;
using GroupDocs.Signature.Options;

class Program
{
    // Custom hash implementation (SHA‑512 truncated to 256 bits)
    private static byte[] MyHash(byte[] data)
    {
        using var sha512 = SHA512.Create();
        var full = sha512.ComputeHash(data);
        var truncated = new byte[32];
        Buffer.BlockCopy(full, 0, truncated, 0, truncated.Length);
        return truncated;
    }

    static void Main()
    {
        // Paths
        string input = @"C:\Docs\contract.pdf";
        string output = @"C:\Docs\contract.signed.pdf";

        // Step 1: create signature options
        var signatureOptions = new SignatureOptions
        {
            CustomSignHash = hash => MyHash(hash)
        };

        // Step 2: sign the document
        using var signer = new Signature(input);
        bool signed = signer.Sign(output, signatureOptions);
        if (!signed)
        {
            Console.WriteLine("Signing failed.");
            return;
        }

        // Step 3: verify the signature
        using var verifier = new Signature(output);
        bool verified = verifier.Verify();
        Console.WriteLine(verified
            ? "Signature verified successfully."
            : "Signature verification failed.");
    }
}
```

**Expected output**

```
Signature verified successfully.
```

Nếu console in ra “Signing failed.” hoặc “Signature verification failed.”, hãy kiểm tra lại cấu hình chứng chỉ và đảm bảo hàm băm tùy chỉnh trả về một mảng byte có kích thước mong đợi.

---

## Conclusion

Bạn giờ đã biết cách **create signature options** trong C#, đính kèm **custom hash function**, và **apply digital signature** cho bất kỳ tài liệu nào được hỗ trợ. Hướng dẫn đã bao quát toàn bộ vòng đời: cấu hình tùy chọn, ký tệp, và xác minh kết quả. Bằng cách tái sử dụng cùng một thể hiện `SignatureOptions`, bạn cũng có thể **how to configure signature** cho hình ảnh, tệp Word, hoặc các binary thô.

---

## What’s next?

* Khám phá các thuộc tính bổ sung của `SignatureOptions` như dấu ấn trực quan, máy chủ timestamp, và chuỗi chứng chỉ – những yếu tố này phù hợp với từ khóa **apply digital signature**.  
* Thử nghiệm các thuật toán băm khác (ví dụ, Blake2b) bằng cách thay đổi triển khai trong `MyHash`.  
* Tích hợp quy trình ký vào một Web API để cho phép ký tài liệu ngay tại thời điểm yêu cầu – một mở rộng tự nhiên của **how to sign document** trong kiến trúc dịch vụ.

Hãy tự do điều chỉnh mã cho các chính sách bảo mật của bạn, và chia sẻ trải nghiệm trong phần bình luận. Chúc bạn ký thành công!

## What Should You Learn Next?

Các hướng dẫn sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật đã trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh với giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Cách thay đổi ngôn ngữ chữ ký PDF với Aspose.PDF cho .NET](/pdf/english/net/digital-signatures/change-pdf-signature-language-aspose-net/)
- [Hướng dẫn chữ ký số Aspose Pdf Net](/pdf/german/net/digital-signatures/digital-signature-aspose-pdf-net-tutorial/)
- [Hướng dẫn chữ ký số Aspose Pdf Net](/pdf/french/net/digital-signatures/digital-signature-aspose-pdf-net-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}