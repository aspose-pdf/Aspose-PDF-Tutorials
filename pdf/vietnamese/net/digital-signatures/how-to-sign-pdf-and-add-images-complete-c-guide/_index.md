---
category: general
date: 2026-03-29
description: Cách ký PDF bằng chữ ký số và thêm hình ảnh đã cắt trong C#. Học cách
  thêm chữ ký số vào PDF, cắt hình ảnh cho PDF và chèn hình ảnh vào PDF một cách dễ
  dàng.
draft: false
keywords:
- how to sign pdf
- add digital signature pdf
- crop image for pdf
- add image to pdf
- digital signature pdf page
language: vi
og_description: Cách ký PDF bằng chữ ký số và chèn hình ảnh đã cắt bằng Aspose.Pdf
  trong C#. Hãy theo dõi hướng dẫn này để có giải pháp hoàn chỉnh.
og_title: Cách ký PDF và thêm hình ảnh – Hướng dẫn C# từng bước
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Cách ký PDF và thêm hình ảnh – Hướng dẫn C# đầy đủ
url: /vi/net/digital-signatures/how-to-sign-pdf-and-add-images-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách ký PDF và Thêm Hình Ảnh – Hướng Dẫn C# Đầy Đủ

Bạn đã bao giờ tự hỏi **cách ký PDF** một cách lập trình đồng thời chèn một hình ảnh tùy chỉnh chưa? Có thể bạn đang xây dựng quy trình phê duyệt và cần một chữ ký pháp lý *và* một hình thu nhỏ của ảnh người ký trên cùng một trang. Nói ngắn gọn, bạn muốn **add digital signature pdf** vào nội dung, cắt hình ảnh đó, và sau đó **add image to pdf** mà không gặp khó khăn.  

Bài hướng dẫn này sẽ đưa bạn qua từng bước — từ việc tải chứng chỉ ECDSA PKCS#7 đến việc cắt JPEG và dán nó lên trang đã ký. Khi hoàn thành, bạn sẽ có một tệp C# duy nhất, có thể chạy được, ký trang 1, cắt ảnh thành 400 × 400 px và đặt nó vào vị trí chính xác. Không có script bên ngoài, không có phép thuật, chỉ có mã rõ ràng và giải thích.

## Yêu Cầu Trước

- .NET 6.0 hoặc mới hơn (mã cũng hoạt động với .NET Framework 4.7+)
- **Aspose.Pdf for .NET** package NuGet (phiên bản 23.9 hoặc mới hơn)
- Chứng chỉ ECDSA P‑256 ở định dạng PKCS#7 (`.pfx`) và mật khẩu của nó
- Hình ảnh JPEG mà bạn muốn nhúng (ví dụ: `photo.jpg`)

> **Mẹo chuyên nghiệp:** Giữ tệp chứng chỉ của bạn ra khỏi source control và bảo vệ mật khẩu bằng một trình quản lý bí mật.

---

## Bước 1: Thiết Lập Dự Án và Nhập Khẩu

Đầu tiên, tạo một ứng dụng console (hoặc tích hợp vào bất kỳ dịch vụ hiện có nào). Thêm tham chiếu Aspose.Pdf:

```bash
dotnet add package Aspose.Pdf
```

Sau đó, bao gồm các namespace cần thiết:

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Forms;
using Aspose.Pdf.Drawing;
```

Các câu lệnh `using` này cho phép bạn truy cập các lớp `Document`, `Signature`, và `Rectangle` mà chúng ta sẽ dùng sau.

## Bước 2: Tải PDF và Chuẩn Bị Chữ Ký

Chúng ta sẽ mở một tệp PDF hiện có (`source.pdf`) và tạo một đối tượng **digital signature pdf** sử dụng chữ ký PKCS#7 tách rời. Chứng chỉ là khóa ECDSA P‑256, được chấp nhận rộng rãi cho việc tuân thủ.

```csharp
// Load the PDF you want to sign
var doc = new Document("YOUR_DIRECTORY/source.pdf");

// Initialize the signature appearance (optional but recommended)
var signature = new Signature(doc);
signature.Contact = "John Doe";
signature.Location = "New York, USA";
signature.Reason = "Document approval";

// Load the PKCS#7 certificate (ECDSA P‑256) for signing
var pkcsSignature = new PKCS7Detached(
    "YOUR_DIRECTORY/ecdsa.pfx",   // certificate file
    "YOUR_PASSWORD");             // certificate password
```

**Tại sao điều này quan trọng:** Sử dụng chữ ký PKCS#7 tách rời giữ nguyên nội dung PDF gốc trong khi nhúng một hàm băm mật mã. Đây là cách tiếp cận tiêu chuẩn trong ngành cho các PDF pháp lý.

## Bước 3: Áp Dụng Chữ Ký Kỹ Thuật Số vào Trang Cụ Thể

Bây giờ chúng ta sẽ đặt trường chữ ký hiển thị trên **page 1**. Hình chữ nhật xác định vị trí của hộp chữ ký (tọa độ tính bằng points, trong đó 1 inch = 72 points).

```csharp
// Apply the digital signature to page 1, covering a rectangular area
signature.Sign(
    pageNumber: 1,
    isVisible: true,
    signatureRect: new Rectangle(100, 100, 300, 300),
    pkcsSignature);
```

Nếu bạn không cần hộp hiển thị, đặt `isVisible` thành `false`. `signatureRect` có thể điều chỉnh để phù hợp với bố cục tài liệu của bạn.

## Bước 4: Mở Luồng Hình Ảnh và Xác Định Vùng Cắt

Chúng ta sẽ đọc tệp JPEG vào một luồng và chỉ định một **source rectangle** chọn vùng 400 × 400 pixel ở góc trên‑trái. Đây là thao tác **crop image for pdf**.

```csharp
// Open the image file that will be added to the PDF
using var imageStream = File.OpenRead("YOUR_DIRECTORY/photo.jpg");

// Define the source rectangle that selects the portion to crop (0‑400 pixels)
var sourceRect = new Rectangle(0, 0, 400, 400);
```

> **Trường hợp đặc biệt:** Nếu hình ảnh của bạn nhỏ hơn 400 × 400, việc cắt sẽ tự động giới hạn tới kích thước thực tế của ảnh — không có ngoại lệ nào được ném.

## Bước 5: Xác Định Vị Trí Hiển Thị Hình Ảnh Đã Cắt

Tiếp theo, đặt **destination rectangle** trên trang PDF. Trong ví dụ này chúng tôi đặt hình ảnh tại (50, 50) với kích thước 200 × 200 points (≈2.78 inch vuông).

```csharp
// Define the destination rectangle where the cropped image will be placed on the page
var destinationRect = new Rectangle(50, 50, 200, 200);
```

Bạn có thể thử nghiệm: thay đổi tọa độ X/Y để di chuyển hình ảnh, hoặc điều chỉnh chiều rộng/chiều cao để thay đổi tỷ lệ.

## Bước 6: Chèn Hình Ảnh Đã Cắt vào Trang Đã Ký

Cuối cùng, chúng ta thêm hình ảnh vào **page 1** (cùng trang hiện đang có chữ ký). Phương thức `AddImage` overload mà chúng ta dùng chấp nhận các hình chữ nhật nguồn và đích, thực hiện việc cắt và đặt vị trí trong một lời gọi.

```csharp
// Insert the cropped image onto page 1 at the specified location
doc.Pages[1].AddImage(imageStream, sourceRect, destinationRect);
```

Trong nền, Aspose.Pdf sẽ trích xuất vùng 400 × 400 pixel, thay đổi kích thước thành 200 × 200 points và ghi vào luồng nội dung PDF.

## Bước 7: Lưu PDF Đã Ký và Được Thêm Hình Ảnh

Sau khi thực hiện mọi thay đổi, lưu tài liệu. Bạn có thể ghi đè lên tệp gốc hoặc tạo một tệp mới.

```csharp
// Save the final document
doc.Save("YOUR_DIRECTORY/output_signed.pdf");
Console.WriteLine("PDF signed and image added successfully!");
```

Khi mở `output_signed.pdf` trong Adobe Acrobat hoặc bất kỳ trình xem PDF nào, bạn sẽ thấy:

- Một trường chữ ký hiển thị tại tọa độ bạn đã chỉ định.
- Ảnh đã cắt được đặt tại (50, 50) trên page 1.
- Chữ ký kỹ thuật số được xác thực (miễn là trình xem tin tưởng chứng chỉ của bạn).

---

## Câu Hỏi Thường Gặp (FAQ)

| Câu hỏi | Trả lời |
|----------|--------|
| **Tôi có thể ký trang khác không?** | Thay đổi đối số `pageNumber` trong `signature.Sign` thành bất kỳ chỉ số trang hợp lệ nào (đánh số từ 1). |
| **Nếu tôi cần nhiều chữ ký thì sao?** | Tạo một thể hiện `Signature` mới cho mỗi trang hoặc vị trí, sử dụng lại `pkcsSignature` nếu cùng một chứng chỉ được áp dụng. |
| **Việc cắt ảnh có bị giới hạn ở hình chữ nhật không?** | Có, `AddImage` của Aspose.Pdf hoạt động với các vùng hình chữ nhật. Đối với hình dạng phức tạp, bạn cần tiền xử lý ảnh (ví dụ, dùng System.Drawing) trước khi nhúng. |
| **Làm sao để làm chữ ký không hiển thị?** | Đặt `isVisible` thành `false` và bỏ qua `signatureRect`. Chữ ký vẫn sẽ hợp lệ về mặt mật mã. |
| **Ngoài JPEG, tôi có thể nhúng định dạng nào khác?** | PNG, BMP, GIF và TIFF đều được hỗ trợ. Chỉ cần thay đổi đường dẫn tệp và đảm bảo luồng đọc đúng byte. |

## Ví Dụ Hoàn Chỉnh

Dưới đây là chương trình hoàn chỉnh, tự chứa. Sao chép‑dán vào `Program.cs`, điều chỉnh các đường dẫn và chạy.

```csharp
// Program.cs
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Forms;
using Aspose.Pdf.Drawing;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source PDF
        var doc = new Document("YOUR_DIRECTORY/source.pdf");

        // 2️⃣ Prepare the digital signature appearance
        var signature = new Signature(doc)
        {
            Contact = "John Doe",
            Location = "New York, USA",
            Reason = "Document approval"
        };

        // 3️⃣ Load the PKCS#7 ECDSA P‑256 certificate
        var pkcsSignature = new PKCS7Detached(
            "YOUR_DIRECTORY/ecdsa.pfx",
            "YOUR_PASSWORD");

        // 4️⃣ Apply a visible signature on page 1
        signature.Sign(
            pageNumber: 1,
            isVisible: true,
            signatureRect: new Rectangle(100, 100, 300, 300),
            pkcsSignature);

        // 5️⃣ Open the image to be added
        using var imageStream = File.OpenRead("YOUR_DIRECTORY/photo.jpg");

        // 6️⃣ Define crop (source) and placement (destination) rectangles
        var sourceRect = new Rectangle(0, 0, 400, 400);      // crop 400×400 px from top‑left
        var destinationRect = new Rectangle(50, 50, 200, 200); // place at (50,50) with 200×200 pt size

        // 7️⃣ Insert the cropped image onto the same page
        doc.Pages[1].AddImage(imageStream, sourceRect, destinationRect);

        // 8️⃣ Save the final PDF
        doc.Save("YOUR_DIRECTORY/output_signed.pdf");
        Console.WriteLine("PDF signed and image added successfully!");
    }
}
```

**Kết quả mong đợi:** Khi mở `output_signed.pdf` sẽ hiển thị một trường chữ ký (100 × 100 → 300 × 300 points) và một hình ảnh 200 × 200 point được lấy từ góc trên‑trái của `photo.jpg`. Chữ ký được xác thực dựa trên chứng chỉ ECDSA đã cung cấp.

## Kết Luận

Chúng ta đã đề cập đến **cách ký PDF** files, cách **add digital signature pdf** vào một trang cụ thể, cách **crop image for pdf**, và cuối cùng cách **add image to pdf** bằng Aspose.Pdf trong C#. Toàn bộ quy trình — từ tải chứng chỉ đến lưu tài liệu cuối cùng — được gói gọn trong một tệp nguồn duy nhất, dễ đọc.

Nếu bạn đã sẵn sàng cho thử thách tiếp theo, hãy cân nhắc:

- Thêm **nhiều chữ ký** trên các trang khác nhau (sử dụng khái niệm “digital signature pdf page”).
- Nhúng **mã QR** liên kết tới các dịch vụ xác thực.
- Tự động hoá quy trình trong một API ASP.NET Core để tạo PDF ngay lập tức.

Hãy nhớ, chìa khóa để tự động hoá PDF mạnh mẽ là tách biệt rõ ràng các mối quan tâm: xử lý chữ ký, xử lý hình ảnh và lắp ráp tài liệu cuối cùng. Thử nghiệm với các tọa độ, thay đổi định dạng ảnh, hoặc thử nghiệm với timestamp — quy trình của bạn giờ đã hoàn toàn mở rộng.

Có câu hỏi, trường hợp đặc biệt, hoặc một ví dụ thú vị muốn chia sẻ? Để lại bình luận bên dưới, và chúc bạn lập trình vui vẻ!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}