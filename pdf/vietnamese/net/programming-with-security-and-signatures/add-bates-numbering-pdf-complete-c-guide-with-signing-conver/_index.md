---
category: general
date: 2026-06-21
description: Thêm đánh số Bates vào PDF và học cách thêm số Bates, chuyển PDF sang
  PDF/X-4, chuyển PDF sang PDF/A-4, và ký số PDF bằng C# trong một hướng dẫn duy nhất.
draft: false
keywords:
- add bates numbering pdf
- how to add bates numbers
- digitally sign pdf c#
- convert pdf to pdf/x-4
- convert pdf to pdfa-4
language: vi
og_description: Thêm đánh số Bates vào PDF, xem cách thêm số Bates, chuyển PDF sang
  PDF/X-4, chuyển PDF sang PDF/A-4, và ký số PDF bằng C# với Aspose.Pdf.
og_title: Thêm số Bates vào PDF – Hướng dẫn C# chi tiết từng bước
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Add bates numbering pdf and learn how to add bates numbers, convert
    pdf to pdf/x-4, convert pdf to pdfa-4, and digitally sign pdf c# in a single walkthrough.
  headline: Add Bates Numbering PDF – Complete C# Guide with Signing & Conversion
  type: TechArticle
- questions:
  - answer: Yes. Use `BatesNumberingOptions` properties such as `Location` and `FontSize`
      to fine‑tune placement.
    question: Can I change the position of the Bates numbers?
  - answer: Switch `PdfFormat.PDF_X_4` to `PdfFormat.PDFA_4` in the conversion options.
      That satisfies the **convert pdf to pdfa-4** requirement.
    question: What if I need PDF/A‑4 instead of PDF/X‑4?
  - answer: Absolutely. Replace `DigestHashAlgorithm.Sha384` with `DigestHashAlgorithm.Sha256`
      (or any supported algorithm).
    question: My certificate uses a different hash algorithm—can I use SHA‑256?
  - answer: 'Not strictly. In this flow we save after conversion and after Bates numbering
      to give you intermediate files. You could defer saving until the end if you
      prefer a single write operation. ## Wrap‑Up We’ve just demonstrated a practical,
      end‑to‑end solution that **add bates numbering pdf**, explains **'
    question: Do I need to call `document.Save` after each step?
  type: FAQPage
tags:
- Aspose.Pdf
- C#
- PDF processing
- Bates numbering
title: Thêm Số Bates vào PDF – Hướng Dẫn Toàn Diện C# với Chữ Ký & Chuyển Đổi
url: /vi/net/programming-with-security-and-signatures/add-bates-numbering-pdf-complete-c-guide-with-signing-conver/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Thêm Số Bates vào PDF – Hướng Dẫn C# Hoàn Chỉnh với Chữ Ký & Chuyển Đổi

Bạn đã bao giờ tự hỏi **cách thêm bates numbering pdf** mà không phải rối bời chưa? Bạn không phải là người duy nhất. Các đội ngũ pháp lý, kiểm toán viên và bất kỳ ai cần tài liệu có thể truy xuất luôn hỏi *cách thêm số bates* vào PDF, và sau đó họ còn cần tệp đáp ứng tiêu chuẩn PDF/X‑4 hoặc PDF/A‑4 và được ký số.  

Trong hướng dẫn này, chúng ta sẽ đi qua toàn bộ quy trình—sử dụng Aspose.Pdf cho .NET, chúng ta sẽ **add bates numbering pdf**, trình bày **cách thêm số bates**, **chuyển pdf sang pdf/x-4**, **chuyển pdf sang pdfa-4**, và cuối cùng **ký số pdf c#**. Khi kết thúc, bạn sẽ có một chương trình sẵn sàng chạy tạo ra ba PDF đã hoàn thiện: một phiên bản PDF/X‑4, một phiên bản có số Bates, và một phiên bản đã ký số.

![add bates numbering pdf example](image-placeholder.png "Screenshot showing add bates numbering pdf in action")

## Những Gì Bạn Cần Chuẩn Bị

- **.NET 6+** (hoặc .NET Framework 4.6+). Aspose.Pdf hỗ trợ cả hai.
- Một **giấy phép Aspose.Pdf for .NET hợp lệ** (hoặc bạn có thể dùng bản đánh giá, nhưng sẽ xuất hiện watermark).
- Một **tệp chứng chỉ PKCS#7** (`.pfx`) và mật khẩu của nó để ký.
- **PDF mẫu** mà bạn muốn chuyển đổi (đặt nó trong một thư mục bạn kiểm soát).
- Visual Studio, Rider, hoặc bất kỳ IDE C# nào bạn thích.

Đó là tất cả—không cần thêm gói NuGet nào ngoài `Aspose.Pdf`. Nếu bạn chưa thêm thư viện, chạy:

```bash
dotnet add package Aspose.Pdf
```

Bây giờ hãy bắt đầu với mã nguồn.

## Bước 1: Tải Tài Liệu PDF Nguồn

Đầu tiên, chúng ta cần đưa tệp gốc vào bộ nhớ. Đây là nền tảng cho mọi thao tác sau này.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Forms;
using Aspose.Pdf.Security;
using Aspose.Pdf.Saving;

// Load the source PDF – adjust the path to your environment
var document = new Document("YOUR_DIRECTORY/sample.pdf");
```

> **Tại sao lại quan trọng:** Việc tải PDF tạo ra một đối tượng `Document` đại diện cho toàn bộ tệp, cho phép chúng ta truy cập các API chuyển đổi, trường biểu mẫu và bảo mật.

## Bước 2: Chuyển Đổi PDF sang PDF/X‑4 (Tuân Thủ PDF/A‑4)

Nếu quy trình của bạn yêu cầu chất lượng lưu trữ, PDF/X‑4 (một phần của PDF/A‑4) là lựa chọn phù hợp. Dưới đây là cách **convert pdf to pdf/x-4** bằng Aspose.

```csharp
// Set conversion options – PDF/X‑4 is the target format
var conversionOptions = new PdfFormatConversionOptions(PdfFormat.PDF_X_4, ConvertErrorAction.Delete);

// Perform the conversion
document.Convert(conversionOptions);
```

> **Mẹo:** Cờ `ConvertErrorAction.Delete` sẽ loại bỏ bất kỳ nội dung nào có thể phá vỡ tiêu chuẩn, đảm bảo đầu ra PDF/X‑4 sạch sẽ.

## Bước 3: Lưu Phiên Bản PDF/X‑4

Khi tài liệu đã tuân thủ PDF/X‑4, chúng ta ghi nó ra đĩa.

```csharp
document.Save("YOUR_DIRECTORY/sample_pdfx4.pdf");
```

Bây giờ bạn đã có một tệp **convert pdf to pdfa-4**‑tương thích (PDF/X‑4 là một thành viên của họ PDF/A‑4). Bạn có thể mở nó trong Acrobat để kiểm tra biểu tượng tuân thủ.

## Bước 4: Thêm Số Bates – Phần Cốt Lõi của “Add Bates Numbering PDF”

Số Bates là một định danh tuần tự được đặt trên mỗi trang. Đây là câu trả lời chính xác cho *cách thêm số bates* một cách lập trình.

```csharp
// Configure Bates numbering options
var batesOptions = new BatesNumberingOptions
{
    Prefix = "CASE-",   // Optional prefix
    Start = 5000        // Starting number
};

// Apply Bates numbering to the document
document.AddBatesNumbering(batesOptions);
```

> **Tại sao cách này hoạt động:** `AddBatesNumbering` duyệt qua mọi trang và dán số vào vị trí mặc định (góc dưới‑phải). Bạn có thể tùy chỉnh vị trí sau này bằng `BatesNumberingOptions` nếu cần.

## Bước 5: Lưu PDF Đã Thêm Số Bates

Sau khi **add bates numbering pdf**, chúng ta cần một tệp riêng để giữ lại các số đã được đánh.

```csharp
document.Save("YOUR_DIRECTORY/sample_bates.pdf");
```

Mở tệp; bạn sẽ thấy “CASE‑5000”, “CASE‑5001”,… ở cuối mỗi trang.

## Bước 6: Ký Số PDF – “Digitally Sign PDF C#” trong Hành Động

Chữ ký số đảm bảo tính xác thực và toàn vẹn. Dưới đây chúng ta sẽ **digitally sign pdf c#** bằng hàm băm SHA‑384.

```csharp
// Prepare the signature handler
var signature = new PdfFileSignature(document);

// Load the PKCS#7 certificate (adjust password)
var pkcs7 = new PKCS7Detached(
    "YOUR_DIRECTORY/mycert.pfx", // Path to .pfx
    "pwd",                       // Certificate password
    DigestHashAlgorithm.Sha384   // Strong hashing algorithm
);

// Sign page 1, place signature rectangle at (100,100)-(200,150)
signature.Sign(
    pageNumber: 1,
    signatureAppearance: true,
    rectangle: new Rectangle(100, 100, 200, 150),
    pkcs7: pkcs7
);
```

> **Pro tip:** `Rectangle` xác định vị trí hiển thị của chữ ký. Nếu bạn không cần hiển thị, đặt `signatureAppearance` thành `false`.

## Bước 7: Lưu PDF Đã Ký Số

Cuối cùng, ghi tài liệu đã ký ra đĩa.

```csharp
signature.Save("YOUR_DIRECTORY/sample_signed.pdf");
```

Bây giờ bạn đã có một tệp **digitally sign pdf c#** có thể được xác thực trong bất kỳ trình đọc PDF nào hỗ trợ chữ ký số.

## Toàn Bộ Mã Nguồn – Giải Pháp Một Cửa

Dưới đây là chương trình hoàn chỉnh, sẵn sàng chạy, kết nối tất cả các bước lại với nhau. Sao chép‑dán, điều chỉnh đường dẫn, và nhấn **F5**.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Forms;
using Aspose.Pdf.Security;
using Aspose.Pdf.Saving;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Load the source PDF document
        // -------------------------------------------------
        var document = new Document("YOUR_DIRECTORY/sample.pdf");

        // -------------------------------------------------
        // Step 2: Convert the document to PDF/X‑4 format
        // (PDF/A‑4 compliance)
        // -------------------------------------------------
        var conversionOptions = new PdfFormatConversionOptions(
            PdfFormat.PDF_X_4,
            ConvertErrorAction.Delete);
        document.Convert(conversionOptions);

        // -------------------------------------------------
        // Step 3: Save the PDF/X‑4 version
        // -------------------------------------------------
        document.Save("YOUR_DIRECTORY/sample_pdfx4.pdf");

        // -------------------------------------------------
        // Step 4: Add Bates numbering – how to add bates numbers
        // -------------------------------------------------
        var batesOptions = new BatesNumberingOptions
        {
            Prefix = "CASE-",
            Start = 5000
        };
        document.AddBatesNumbering(batesOptions);

        // -------------------------------------------------
        // Step 5: Save the Bates‑numbered PDF
        // -------------------------------------------------
        document.Save("YOUR_DIRECTORY/sample_bates.pdf");

        // -------------------------------------------------
        // Step 6: Sign the document using SHA‑384 hashing
        // -------------------------------------------------
        var signature = new PdfFileSignature(document);
        var pkcs7 = new PKCS7Detached(
            "YOUR_DIRECTORY/mycert.pfx",
            "pwd",
            DigestHashAlgorithm.Sha384);
        signature.Sign(
            pageNumber: 1,
            signatureAppearance: true,
            rectangle: new Rectangle(100, 100, 200, 150),
            pkcs7: pkcs7);

        // -------------------------------------------------
        // Step 7: Save the digitally signed PDF
        // -------------------------------------------------
        signature.Save("YOUR_DIRECTORY/sample_signed.pdf");
    }
}
```

### Kết Quả Mong Đợi

| Tệp | Mục Đích | Tính Năng Chính |
|------|---------|-------------|
| `sample_pdfx4.pdf` | Phiên bản PDF/X‑4 | Đáp ứng tiêu chuẩn PDF/A‑4 |
| `sample_bates.pdf` | PDF có số Bates | Áp dụng **add bates numbering pdf** |
| `sample_signed.pdf` | PDF đã ký số | **digitally sign pdf c#** với SHA‑384 |

Mở bất kỳ tệp nào trong ba tệp này bằng Adobe Acrobat Reader; bạn sẽ thấy số Bates trên tệp thứ hai và trường chữ ký trên tệp thứ ba.

## Câu Hỏi Thường Gặp (FAQ)

**H: Tôi có thể thay đổi vị trí của số Bates không?**  
Đ: Có. Sử dụng các thuộc tính của `BatesNumberingOptions` như `Location` và `FontSize` để tinh chỉnh vị trí.

**H: Nếu tôi cần PDF/A‑4 thay vì PDF/X‑4 thì sao?**  
Đ: Thay `PdfFormat.PDF_X_4` bằng `PdfFormat.PDFA_4` trong tùy chọn chuyển đổi. Điều này đáp ứng yêu cầu **convert pdf to pdfa-4**.

**H: Chứng chỉ của tôi dùng thuật toán băm khác—có thể dùng SHA‑256 không?**  
Đ: Chắc chắn. Thay `DigestHashAlgorithm.Sha384` bằng `DigestHashAlgorithm.Sha256` (hoặc bất kỳ thuật toán nào được hỗ trợ).

**H: Tôi có cần gọi `document.Save` sau mỗi bước không?**  
Đ: Không bắt buộc. Trong quy trình này chúng ta lưu sau khi chuyển đổi và sau khi thêm số Bates để cung cấp các tệp trung gian. Bạn có thể hoãn việc lưu cho đến cuối cùng nếu muốn chỉ thực hiện một lần ghi.

## Tổng Kết

Chúng ta vừa trình diễn một giải pháp thực tế, đầu‑cuối, giúp **add bates numbering pdf**, giải thích **cách thêm số bates**, minh họa **convert pdf to pdf/x-4**, và bao quát  

## Bạn Nên Học Gì Tiếp Theo?


Các hướng dẫn sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật đã trình bày trong bài viết này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh với giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Aspose Pdf Net Add Attachments Convert Pdfa](/pdf/german/net/pdfa-compliance/aspose-pdf-net-add-attachments-convert-pdfa/)
- [Aspose Pdf Net Add Attachments Convert Pdfa](/pdf/french/net/pdfa-compliance/aspose-pdf-net-add-attachments-convert-pdfa/)
- [Aspose Pdf Net Add Attachments Convert Pdfa](/pdf/japanese/net/pdfa-compliance/aspose-pdf-net-add-attachments-convert-pdfa/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}