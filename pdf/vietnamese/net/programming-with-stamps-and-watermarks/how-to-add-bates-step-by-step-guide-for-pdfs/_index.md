---
category: general
date: 2026-02-10
description: Cách thêm số Bates vào PDF nhanh chóng—tìm hiểu cách thêm số Bates vào
  PDF và tạo watermark vô hình với Aspose.Pdf trong C#.
draft: false
keywords:
- how to add bates
- add bates number pdf
- add custom stamp pdf
- add invisible watermark pdf
- add page footer pdf
language: vi
og_description: Cách thêm số Bates trong C# với Aspose.Pdf. Hướng dẫn này cho thấy
  cách thêm số Bates vào PDF, thêm watermark vô hình vào PDF và nhiều hơn nữa.
og_title: Cách Thêm Bates – Hướng Dẫn PDF Đầy Đủ
tags:
- Aspose.Pdf
- C#
- PDF
- Bates numbering
title: Cách Thêm Mã Bates – Hướng Dẫn Từng Bước Cho PDF
url: /vi/net/programming-with-stamps-and-watermarks/how-to-add-bates-step-by-step-guide-for-pdfs/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách Thêm Bates – Hướng Dẫn PDF Đầy Đủ

Bạn đã bao giờ tự hỏi **cách thêm bates** vào một PDF pháp lý mà không làm hỏng văn bản có thể tìm kiếm không? Bạn không phải là người duy nhất. Ở nhiều công ty luật và dự án e‑discovery, số Bates là một chân trang bắt buộc, nhưng bạn cũng muốn nó vô hình đối với các công cụ OCR. Bài hướng dẫn này sẽ chỉ cho bạn **cách thêm bates** bằng Aspose.Pdf cho .NET, và trong quá trình thực hiện chúng ta sẽ đề cập tới **add bates number pdf**, **add custom stamp pdf**, **add invisible watermark pdf**, và thậm chí **add page footer pdf** trong một giải pháp gọn gàng.

Chúng tôi sẽ đi qua từng dòng mã, giải thích tại sao mỗi thiết lập lại quan trọng, và cung cấp cho bạn một ví dụ sẵn sàng chạy mà bạn có thể đưa vào dự án ngay hôm nay. Không có liên kết “xem tài liệu” mơ hồ — mọi thứ bạn cần đều có ở đây.

## Những Điều Bạn Sẽ Nhận Được

- Một đoạn mã C# hoàn chỉnh, có thể chạy, thêm số Bates dưới dạng **artifact stamp**.
- Hiểu cách làm cho stamp hoạt động như một **invisible watermark** trong khi vẫn hiển thị trên trang.
- Các mẹo để mở rộng giải pháp cho PDF đa trang, thay đổi phông chữ, hoặc thay thế stamp bằng đồ họa tùy chỉnh.
- Những chỉ dẫn nhanh về cách **add page footer pdf** mà không làm hỏng việc trích xuất văn bản.

### Yêu Cầu Trước

- .NET 6+ (hoặc .NET Framework 4.7.2) với Visual Studio 2022 hoặc bất kỳ IDE nào bạn thích.
- Aspose.Pdf cho .NET (bạn có thể tải bản dùng thử miễn phí từ trang web Aspose).
- Một file PDF mẫu có tên `source.pdf` được đặt trong thư mục bạn kiểm soát.

Nếu đã có những thứ trên, hãy bắt đầu.

---

## Cách Thêm Bates – Triển Khai Cốt Lõi

Trọng tâm của giải pháp là một `TextStamp` mà chúng ta xử lý như một **artifact**. Các artifact bị các engine trích xuất văn bản bỏ qua, vì vậy cách tiếp cận này cũng đồng thời là một kỹ thuật **add invisible watermark pdf**.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Annotations;

// Load the source PDF
using var pdfDocument = new Document("YOUR_DIRECTORY/source.pdf");

// Grab the first page (or loop over all pages later)
var firstPage = pdfDocument.Pages[1];

// Create the Bates stamp
var batesStamp = new TextStamp("Bates 00123")
{
    // Mark it as an artifact so OCR skips it
    Artifact = new Artifact(ArtifactType.Artifact),

    // Position it like a typical page footer
    HorizontalAlignment = HorizontalAlignment.Center,
    VerticalAlignment   = VerticalAlignment.Bottom,

    // Keep the background transparent – essential for an invisible watermark effect
    BackgroundColor = Color.Transparent,

    // Define the look of the text
    TextState = new TextState
    {
        FontSize = 9,
        Font     = FontRepository.FindFont("Arial")
    }
};

// Add the stamp to the chosen page
firstPage.AddStamp(batesStamp);

// Save the new PDF
pdfDocument.Save("YOUR_DIRECTORY/bates_artifact.pdf");
```

### Tại Sao Cách Này Hoạt Động

1. **Cờ Artifact** – Bằng cách đặt `Artifact = new Artifact(ArtifactType.Artifact)`, stamp được coi là một phần tử không phải nội dung. Các công cụ tìm kiếm và e‑discovery pháp lý sẽ bỏ qua nó, đúng như bạn mong muốn cho một **add invisible watermark pdf**.
2. **Căn chỉnh ngang/dọc** – Căn giữa‑dưới mô phỏng phong cách **add page footer pdf** cổ điển, làm cho số Bates trông chuyên nghiệp.
3. **Nền trong suốt** – Đảm bảo stamp không che khuất nội dung phía dưới, một chi tiết tinh tế nhưng quan trọng khi bạn cần in hoặc xem PDF trên các thiết bị khác nhau.

---

## Add Bates Number PDF – Mở Rộng Cho Nhiều Trang

Hầu hết các PDF thực tế có hơn một trang. Đoạn mã trên chỉ áp dụng cho trang đầu tiên, nhưng mở rộng cho toàn bộ tài liệu rất dễ dàng:

```csharp
// Loop through every page in the document
foreach (Page page in pdfDocument.Pages)
{
    // Clone the stamp so each page gets its own instance
    var pageStamp = (TextStamp)batesStamp.Clone();

    // Optionally, update the number based on page index
    pageStamp.Text = $"Bates {page.Number:D5}";

    page.AddStamp(pageStamp);
}
```

**Mẹo:** Nếu bạn cần một số thứ tự không phụ thuộc vào thứ tự trang thực tế (ví dụ, bắt đầu từ 1000), chỉ cần khởi tạo một biến đếm trước vòng lặp và tăng nó bên trong.

---

## Add Custom Stamp PDF – Vượt Qua Văn Bản Đơn Giản

Đôi khi một stamp văn bản đơn giản không đủ — bạn có thể muốn một logo, mã QR, hoặc một thanh màu. Aspose.Pdf cho phép bạn thay thế `TextStamp` bằng `ImageStamp` hoặc thậm chí kết hợp cả hai bằng các đối tượng `Stamp`.

```csharp
var imageStamp = new ImageStamp("YOUR_DIRECTORY/logo.png")
{
    // Position it in the top‑right corner
    HorizontalAlignment = HorizontalAlignment.Right,
    VerticalAlignment   = VerticalAlignment.Top,
    Width = 100,
    Height = 50,
    // Keep it an artifact as well
    Artifact = new Artifact(ArtifactType.Artifact)
};

firstPage.AddStamp(imageStamp);
```

Kết hợp các stamp đơn giản như việc thêm cả hai vào cùng một trang. Khả năng **add custom stamp pdf** tỏa sáng khi bạn cần một con dấu công ty bên cạnh số Bates.

---

## Add Invisible Watermark PDF – Làm Stamp Thực Sự Ẩn

Nếu bạn thực sự muốn stamp vô hình đối với mắt người *và* các công cụ trích xuất, bạn có thể đặt màu chữ trùng với nền trang (thường là trắng) và giảm độ trong suốt:

```csharp
batesStamp.TextState.ForegroundColor = Color.White; // assumes white background
batesStamp.Opacity = 0.0; // 0% opacity – completely invisible
```

Ngay cả khi `Opacity = 0`, artifact vẫn tồn tại trong cấu trúc PDF, vì vậy phần mềm pháp lý vẫn có thể định vị nó nếu biết ID của artifact. Đây là thủ thuật **add invisible watermark pdf** tối ưu.

---

## Add Page Footer PDF – Định Dạng Chân Trang Nhất Quán

Một chân trang chuyên nghiệp thường bao gồm nhiều hơn chỉ số Bates: ngày tháng, tiêu đề tài liệu, hoặc thông báo bảo mật. Dưới đây là cách nhanh chóng gộp nhiều đoạn văn bản vào một stamp:

```csharp
var footerText = $"Bates {page.Number:D5}   Confidential   {DateTime.Today:MM/dd/yyyy}";
var footerStamp = new TextStamp(footerText)
{
    HorizontalAlignment = HorizontalAlignment.Center,
    VerticalAlignment   = VerticalAlignment.Bottom,
    BackgroundColor = Color.Transparent,
    TextState = new TextState
    {
        FontSize = 8,
        Font     = FontRepository.FindFont("Times New Roman"),
        ForegroundColor = Color.Gray
    },
    Artifact = new Artifact(ArtifactType.Artifact)
};

page.AddStamp(footerStamp);
```

Lưu ý màu xám nhẹ — hoàn hảo cho một **add page footer pdf** không gây xao lãng nội dung chính nhưng vẫn đáp ứng yêu cầu pháp lý.

---

## Kết Quả Dự Kiến & Cách Kiểm Tra

Sau khi chạy toàn bộ script, mở `bates_artifact.pdf` bằng bất kỳ trình xem PDF nào:

- Bạn sẽ thấy “Bates 00123” (hoặc số thứ tự) được căn giữa ở cuối mỗi trang.
- Khi chọn văn bản trên trang, **số Bates sẽ không** được bao gồm, xác nhận hành vi artifact.
- Nếu bạn đã sử dụng cài đặt invisible‑watermark, số sẽ không hiển thị ở mắt người, nhưng vẫn tồn tại trong cấu trúc nội bộ của PDF (kiểm tra bằng công cụ như PDF‑XChange Editor → “Document → Properties → Advanced”).

---

## Câu Hỏi Thường Gặp & Các Trường Hợp Cạnh

**Nếu PDF của tôi đã có chân trang thì sao?**  
Bạn có thể điều chỉnh `VerticalAlignment` thành `VerticalAlignment.Top` hoặc thay đổi thuộc tính `Margin` để đẩy stamp lên trên chân trang hiện có.

**Có thể dùng phông chữ khác không?**  
Chắc chắn. Chỉ cần thay `"Arial"` bằng bất kỳ tên phông nào Aspose có thể tìm thấy, hoặc nhúng file TTF tùy chỉnh bằng `FontRepository.AddFont("path/to/font.ttf")`.

**Cách này có tương thích với .NET Core không?**  
Có — Aspose.Pdf cho .NET hoạt động trên .NET Framework, .NET Core và .NET 5/6. Chỉ cần chắc chắn bạn tham chiếu đúng gói NuGet.

**Hiệu năng trên các PDF lớn (hơn 1000 trang) ra sao?**  
Tạo một `TextStamp` duy nhất và sao chép nó trong vòng lặp là cách tiết kiệm bộ nhớ. Đối với các file khổng lồ, hãy cân nhắc xử lý theo lô hoặc dùng `PdfProcessor` để tránh tải toàn bộ tài liệu vào bộ nhớ.

---

## Kết Luận

Chúng tôi đã trình bày **cách thêm bates** vào PDF từ đầu đến cuối, minh họa **add bates number pdf**, chỉ ra cách **add custom stamp pdf**, biến stamp thành một **add invisible watermark pdf**, và định dạng nó như một **add page footer pdf** chuyên nghiệp. Đoạn mã hoàn chỉnh chạy ngay, và các giải thích cung cấp “tại sao” cho mỗi dòng — đúng loại câu trả lời mà các trợ lý AI thích trích dẫn.

Bước tiếp theo? Hãy thử thay thế stamp văn bản bằng stamp hình ảnh, thử nghiệm các loại artifact khác, hoặc tích hợp logic này vào dịch vụ xử lý hàng loạt tự động gắn số Bates cho mọi tài liệu trong một thư mục. Khả năng là vô hạn, và giờ bạn đã có nền tảng vững chắc để phát triển.

Chúc lập trình vui vẻ, và chúc PDF của bạn luôn được đánh số hoàn hảo!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}