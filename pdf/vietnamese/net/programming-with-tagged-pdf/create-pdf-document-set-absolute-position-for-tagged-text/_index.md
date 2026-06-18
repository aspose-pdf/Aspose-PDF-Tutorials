---
category: general
date: 2026-03-24
description: Tạo tài liệu PDF và học cách đặt vị trí tuyệt đối cho văn bản được gắn
  thẻ. Hướng dẫn này cho thấy cách thêm phần tử span, cách thêm nội dung được gắn
  thẻ và cách định vị văn bản trên trang.
draft: false
keywords:
- create pdf document
- set absolute position
- add span element
- how to add tagged
- position text on page
language: vi
og_description: Tạo tài liệu PDF và ngay lập tức xem cách đặt vị trí tuyệt đối, thêm
  phần tử span và định vị văn bản trên trang với nội dung PDF có thẻ.
og_title: Tạo tài liệu PDF – Định vị tuyệt đối cho văn bản được gắn thẻ
tags:
- Aspose.Pdf
- C#
- PDF Tagging
title: Tạo tài liệu PDF – Đặt vị trí tuyệt đối cho văn bản được gắn thẻ
url: /vi/net/programming-with-tagged-pdf/create-pdf-document-set-absolute-position-for-tagged-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo Tài Liệu PDF – Đặt Vị Trí Tuyệt Đối cho Văn Bản Đánh Thẻ

Bạn đã bao giờ cần **tạo tài liệu pdf** chứa văn bản có thể truy cập, được đánh thẻ và đặt chính xác ở vị trí mong muốn chưa? Có thể bạn đang xây dựng một PDF dạng biểu mẫu, trong đó nhãn phải nằm ở một tọa độ chính xác, hoặc bạn đang tạo một chứng chỉ và tên phải căn chỉnh hoàn hảo với hình nền.

Trong hướng dẫn này, chúng ta sẽ đi qua một ví dụ hoàn chỉnh, có thể chạy được, cho thấy **cách thêm nội dung được đánh thẻ**, **đặt vị trí tuyệt đối**, và **thêm phần tử span** để bạn có thể **đặt văn bản trên trang** mà không phải đoán mò. Không có tham chiếu bên ngoài—chỉ có mã bạn có thể sao chép‑dán, cùng với giải thích “tại sao” cho mỗi dòng.

## Prerequisites

- .NET 6+ (hoặc .NET Framework 4.6+) với trình biên dịch C#  
- Aspose.Pdf for .NET (phiên bản mới nhất tại thời điểm viết, 23.12) được cài đặt qua NuGet  
- Kiến thức cơ bản về cú pháp C#  

Nếu bạn đã có những thứ trên, hãy bắt đầu nào.

---

## Tạo Tài Liệu PDF – Đặt Vị Trí Tuyệt Đối

Điều đầu tiên chúng ta làm là khởi tạo một `Document` rỗng. Đối tượng này đại diện cho toàn bộ tệp PDF và cho phép chúng ta truy cập vào cây nội dung được đánh thẻ.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Tagged;

// Step 1: Create a new PDF document
using var pdfDocument = new Document();
```

**Tại sao điều này quan trọng:**  
`Document` là gốc của cấu trúc PDF. Bằng cách tạo nó trước, chúng ta đảm bảo có một canvas cho cả các phần tử trực quan (trang, đồ họa) và cấu trúc logic (thẻ). Câu lệnh `using` đảm bảo tệp được giải phóng đúng cách, tránh rò rỉ handle trên Windows.

## Bật Nội Dung Đánh Thẻ (Cách Thêm Đánh Thẻ)

Trước khi chèn bất kỳ phần tử đánh thẻ nào, tài liệu phải được đánh dấu là *đánh thẻ*. Aspose.Pdf tự động tạo một đối tượng `TaggedContent`, nhưng bạn vẫn cần bật cờ này.

```csharp
// Step 2: Mark the document as tagged (required for accessibility)
pdfDocument.TaggedContent = true;
```

**Điều gì xảy ra bên trong?**  
Đặt `TaggedContent` thành `true` thông báo cho trình đọc PDF rằng tệp chứa một cây cấu trúc logic. Điều này rất quan trọng đối với các trình đọc màn hình và để phương thức `SetPosition` hoạt động đúng trên một phần tử span.

## Lấy Phần Tử Gốc của Cây Nội Dung Đánh Thẻ

Phần tử gốc là điểm vào cho tất cả các thẻ cấu trúc (như `<Document>`, `<Section>`, `<Span>`). Hãy nghĩ nó như “body” vô hình của PDF.

```csharp
// Step 3: Retrieve the root element of the tag tree
var rootElement = pdfDocument.TaggedContent.RootElement;
```

**Tại sao chúng ta cần phần tử gốc:**  
Tất cả các thẻ tiếp theo phải được gắn vào một vị trí nào đó trong cây; nếu không chúng sẽ không xuất hiện trong cây khả năng truy cập.

## Thêm Phần Tử Span – Khối Xây Dựng cho Văn Bản Nội Dung

Một *span* là tương đương PDF của thẻ HTML `<span>`—hoàn hảo cho những đoạn văn bản ngắn mà bạn muốn đặt chính xác.

```csharp
// Step 4: Create a span element that will hold the text
var spanElement = rootElement.CreateSpanElement();
```

**Ghi chú thiết kế:**  
Nếu bạn cần định dạng phong phú hơn (đậm, nghiêng, siêu liên kết), bạn có thể bọc span trong một `<Paragraph>` hoặc sử dụng các đối tượng `TextFragment` sau này. Đối với vị trí tuyệt đối, một span đơn giản là nhẹ nhất.

## Đặt Vị Trí Tuyệt Đối – X=100, Y=200

Bây giờ đến phần thú vị: đặt span ở một vị trí chính xác trên trang. Hệ tọa độ bắt đầu từ góc dưới‑trái (0,0) và sử dụng đơn vị point (1 pt ≈ 1/72 in).

```csharp
// Step 5: Position the span at an absolute location (X=100, Y=200)
spanElement.SetPosition(100, 200);
```

**Tại sao lại dùng vị trí tuyệt đối?**  
Khi bạn cần bố cục pixel‑perfect—như chứng chỉ, hoá đơn, hoặc biểu mẫu—luồng tương đối (như văn bản từ trái sang phải) không đủ. `SetPosition` bỏ qua luồng văn bản bình thường và cố định phần tử ở vị trí bạn chỉ định.

## Thêm Văn Bản vào Span

Sau khi span đã được đặt, chúng ta chèn chuỗi ký tự thực tế vào.

```csharp
// Step 6: Add the desired text to the span
spanElement.AddText("Positioned tagged text");
```

**Mẹo:**  
Nếu bạn cần ký tự Unicode hoặc script viết từ phải sang trái, chỉ cần truyền chuỗi; Aspose.Pdf sẽ tự động xử lý mã hoá.

## Gắn Span vào Phần Tử Gốc

Cuối cùng, chúng ta gắn span vào cây logic của tài liệu để nó trở thành một phần của PDF cuối cùng.

```csharp
// Step 7: Append the span to the root so it becomes part of the PDF structure
rootElement.AppendChild(spanElement);
```

**Nếu bỏ qua bước này thì sao?**  
Span sẽ tồn tại trong bộ nhớ nhưng không bao giờ được ghi vào tệp, vì vậy bạn sẽ không thấy văn bản và cây khả năng truy cập sẽ không đầy đủ.

## Ví Dụ Hoàn Chỉnh, Có Thể Chạy Được

Dưới đây là chương trình đầy đủ mà bạn có thể dán vào một ứng dụng console. Nó tạo một PDF một trang, thêm một span được đánh thẻ tại (100, 200), và lưu tệp dưới tên `TaggedPositioned.pdf`.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Tagged;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new PDF document
        using var pdfDocument = new Document();

        // 2️⃣ Enable tagging for accessibility
        pdfDocument.TaggedContent = true;

        // 3️⃣ Add a blank page (required for visual placement)
        var page = pdfDocument.Pages.Add();

        // 4️⃣ Get the root element of the tagged‑content tree
        var rootElement = pdfDocument.TaggedContent.RootElement;

        // 5️⃣ Create a span element that will hold the text
        var spanElement = rootElement.CreateSpanElement();

        // 6️⃣ Position the span at an absolute location on the page (X=100, Y=200)
        spanElement.SetPosition(100, 200);

        // 7️⃣ Add the desired text to the span
        spanElement.AddText("Positioned tagged text");

        // 8️⃣ Append the span to the root so it becomes part of the PDF structure
        rootElement.AppendChild(spanElement);

        // 9️⃣ Save the document
        pdfDocument.Save("TaggedPositioned.pdf");

        Console.WriteLine("PDF created successfully – check TaggedPositioned.pdf");
    }
}
```

**Kết quả mong đợi:**  
Mở `TaggedPositioned.pdf` bằng bất kỳ trình xem nào (Adobe Acrobat, Foxit, v.v.). Bạn sẽ thấy cụm từ **“Positioned tagged text”** nằm chính xác 100 pt từ mép trái và 200 pt từ mép dưới của trang. Nếu bạn kiểm tra bảng *Tags*, một phần tử `<Span>` sẽ được liệt kê dưới gốc của tài liệu, xác nhận nội dung đã được đánh thẻ đúng cách.

## Câu Hỏi Thường Gặp & Trường Hợp Cạnh

### Nếu tôi cần đặt văn bản trên một trang cụ thể khác với trang đầu tiên thì sao?

Thêm trang bạn muốn (`var page = pdfDocument.Pages[3];`) trước khi gọi `SetPosition`. Span sẽ tự động gắn vào ngữ cảnh trang đang hoạt động.

### Tôi có thể đặt vị trí bằng inch hoặc centimet không?

`SetPosition` chỉ nhận đơn vị point. Chuyển đổi bằng công thức:  
- **Inch → point:** `points = inches * 72`  
- **Centimet → point:** `points = cm * 28.3465`

### Làm sao thay đổi phông chữ hoặc màu sắc của span?

Sau khi tạo span, bạn có thể lấy `TextState` của nó và sửa đổi:

```csharp
var textState = spanElement.TextState;
textState.Font = FontRepository.FindFont("Arial");
textState.FontSize = 12;
textState.ForegroundColor = Color.GetBlack();
```

### Nếu tài liệu đã có các thẻ tồn tại thì sao?

Bạn vẫn có thể tạo một span mới và gắn nó vào bất kỳ phần tử nào hiện có (`rootElement`, một `<Section>` cụ thể, v.v.). Chỉ cần duy trì cấu trúc logic—các trình đọc màn hình yêu cầu cây được tổ chức tốt.

### Điều này có hoạt động với chuẩn PDF/A hoặc PDF/UA không?

Có. PDF được đánh thẻ là yêu cầu cốt lõi của PDF/UA. Nếu bạn cần PDF/A, hãy đặt `pdfDocument.Convert(new PdfAConversionOptions(PdfAStandard.PdfA_1b));` sau khi xây dựng nội dung.

## Mẹo Chuyên Gia & Những Cạm Bẫy

- **Mẹo chuyên gia:** Luôn thêm một trang trước khi đặt nội dung. Nếu không có trang, `SetPosition` sẽ im lặng thất bại vì không có nơi để render.  
- **Cẩn thận với đơn vị:** Trộn lẫn pixel từ thiết kế UI với point PDF sẽ làm văn bản bị lệch. Kiểm tra lại phép chuyển đổi.  
- **Gợi ý hiệu năng:** Nếu bạn tạo hàng ngàn PDF, hãy tái sử dụng một đối tượng `Document` duy nhất và gọi `pdfDocument.Pages.Clear()` giữa các lần chạy để tránh cấp phát bộ nhớ quá mức.  
- **Nhắc nhở về khả năng truy cập:** Đánh thẻ không chỉ là tính năng phụ; nhiều quy định (Section 508, EN 301 549) yêu cầu nó. Sử dụng `CreateSpanElement` đảm bảo văn bản có thể được công nghệ hỗ trợ người dùng tiếp cận phát hiện.

## Kết Luận

Chúng ta vừa **tạo tài liệu pdf** từ đầu, **đặt vị trí tuyệt đối**, **thêm phần tử span**, và minh họa **cách thêm nội dung được đánh thẻ** để bạn có thể **đặt văn bản trên trang** với độ chính xác pixel‑perfect. Ví dụ đầy đủ đã sẵn sàng để chạy, và phần giải thích đã bao phủ cả *cách* và *lý do*—đúng những gì các nhà phát triển (và trợ lý AI) cần khi tìm giải pháp đáng tin cậy.

Tiếp theo, bạn có thể khám phá:

- Thêm hình ảnh phía sau văn bản đã đặt để tạo chứng chỉ có dấu nước.  
- Sử dụng `CreateParagraphElement` cho các khối đa dòng vẫn cần vị trí tuyệt đối.  
- Xuất ra PDF/UA để đáp ứng các cuộc kiểm toán khả năng truy cập nghiêm ngặt.  

Hãy thoải mái điều chỉnh tọa độ, phông chữ hoặc màu sắc—thử nghiệm là cách nhanh nhất để thành thạo việc tạo PDF có thẻ. Nếu gặp khó khăn, hãy để lại bình luận bên dưới; chúc bạn lập trình vui vẻ!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}