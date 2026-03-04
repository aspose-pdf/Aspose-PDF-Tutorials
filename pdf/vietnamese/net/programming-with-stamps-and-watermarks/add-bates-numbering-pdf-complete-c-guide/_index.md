---
category: general
date: 2026-03-03
description: Học cách thêm đánh số Bates vào PDF và khám phá cách thêm Bates, tạo
  trường biểu mẫu PDF, cũng như cách chuyển đổi PDFX4 trong một hướng dẫn rõ ràng.
draft: false
keywords:
- add bates numbering pdf
- how to add bates
- create pdf form field
- how to convert pdfx4
language: vi
og_description: Thêm đánh số Bates vào PDF, học cách thêm Bates, tạo trường biểu mẫu
  PDF và cách chuyển đổi PDFX4 bằng mã C# thực tế.
og_title: Thêm Số Bates vào PDF – Hướng Dẫn Toàn Diện C#
tags:
- PDF
- CSharp
- DocumentAutomation
title: Thêm Đánh Số Bates vào PDF – Hướng Dẫn C# Toàn Diện
url: /vi/net/programming-with-stamps-and-watermarks/add-bates-numbering-pdf-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Thêm Số Bates vào PDF – Hướng Dẫn C# Đầy Đủ

Bạn có bao giờ tự hỏi **cách thêm bates** vào một PDF mà không làm rối mình không? Bạn không phải là người duy nhất. Trong nhiều dự án pháp lý hoặc lưu trữ, **add bates numbering pdf** là mục đầu tiên trong danh sách việc cần làm, và nếu bạn bỏ lỡ một bước, toàn bộ hệ thống lưu trữ có thể sụp đổ.  

Trong hướng dẫn này, chúng ta sẽ thực hiện bốn nhiệm vụ thực tế: phát hiện chữ ký bị xâm phạm, **add bates numbering pdf**, chuyển đổi tệp **how to convert pdfx4**, và cuối cùng **create PDF form field** với hai chú thích widget. Khi kết thúc, bạn sẽ có một chương trình C# duy nhất, có thể chạy được, thực hiện tất cả các công việc này, cùng với các mẹo về những khó khăn bạn có thể gặp.

## Yêu Cầu Trước

- .NET 6 SDK hoặc phiên bản mới hơn (mã sử dụng các tính năng ngôn ngữ mới nhất, nhưng .NET 5 cũng hoạt động được)
- Thư viện xử lý PDF cung cấp các lớp `Document`, `BatesNumberingOptions`, `PdfFormatConversionOptions`, `TextBoxField`, v.v. (các ví dụ dựa trên một SDK thương mại điển hình; thay đổi không gian tên nếu bạn dùng SDK khác)
- Một thư mục có tên `YOUR_DIRECTORY` chứa một vài PDF mẫu (`signed.pdf`, `input.pdf`, `source.pdf`) để bạn có thể thấy các tệp đầu ra xuất hiện bên cạnh chúng
- Visual Studio 2022 hoặc bất kỳ IDE nào bạn thích

Bây giờ chúng ta đã chuẩn bị xong, hãy bắt đầu.

## Bước 1 – Phát Hiện Chữ Ký PDF Bị Xâm Phạm

Trước khi bạn bắt đầu dán dấu hoặc chuyển đổi, việc kiểm tra xem bất kỳ chữ ký số nào hiện có vẫn còn hợp lệ là thực hành tốt. Một chữ ký bị xâm phạm có thể có nghĩa là tài liệu đã bị thay đổi sau khi ký, và việc thêm số Bates một cách mù quáng sẽ làm mất tính tuân thủ pháp lý.

```csharp
using System;
using YourPdfLibrary;   // replace with the actual namespace of your PDF SDK

// Load the signed PDF
Document signedDoc = new Document("YOUR_DIRECTORY/signed.pdf");

// Check the signature status
bool isCompromised = signedDoc.IsSignatureCompromised();

// Output the result – true means the signature is no longer trustworthy
Console.WriteLine($"Signature compromised? {isCompromised}");
```

**Tại sao điều này quan trọng:**  
Nếu `isCompromised` trả về `true`, bạn nên từ chối tệp hoặc yêu cầu một chữ ký mới trước khi tiếp tục. Thêm số Bates vào tài liệu đã bị giả mạo có thể bị coi là gian lận trong phòng xử án.

**Mẹo chuyên nghiệp:** Một số SDK cho phép bạn lấy *lý do* chữ ký thất bại (ví dụ: nội dung bị thay đổi, chứng chỉ hết hạn). Ghi lại thông tin đó để làm hồ sơ kiểm toán.

## Bước 2 – Thêm Số Bates vào PDF

Bây giờ là phần quan trọng nhất: **add bates numbering pdf**. Số Bates là các định danh tuần tự thường xuất hiện ở phần đầu hoặc chân trang của mỗi trang. Phương thức `AddBatesNumbering` của SDK thực hiện phần lớn công việc, nhưng bạn vẫn cần quyết định tiền tố, số bắt đầu và vị trí đặt.

```csharp
// Load the source PDF you want to number
Document batesSource = new Document("YOUR_DIRECTORY/input.pdf");

// Configure Bates numbering options
var batesOptions = new BatesNumberingOptions
{
    Prefix = "2025-",    // optional text before the numeric part
    Start = 1000,        // first number in the sequence
    // You can also set Font, FontSize, Color, Position, etc.
};

// Apply the numbering to every page
batesSource.AddBatesNumbering(batesOptions);

// Save the newly numbered PDF
batesSource.Save("YOUR_DIRECTORY/bates.pdf");

// Verify quickly – the console will show the file path
Console.WriteLine("Bates‑numbered PDF saved as bates.pdf");
```

**How to add bates** correctly:  

- **Placement:** Hầu hết các luật sư muốn số xuất hiện ở góc dưới‑phải. Nếu SDK mặc định ở vị trí khác, đặt `batesOptions.Position = BatesNumberPosition.BottomRight;`.
- **Zero‑padding:** Để việc sắp xếp dễ dàng, sử dụng `batesOptions.NumberFormat = "D6";` (tạo ra `001000`, `001001`, …).
- **Multiple prefixes:** Nếu bạn có nhiều lô tài liệu, nối một mã lô vào tiền tố (`"2025-AB-"`).

**Trường hợp đặc biệt:** Nếu PDF nguồn đã có chân trang, số mới có thể chồng lên nhau. Hãy thử trên một trang mẫu và điều chỉnh giá trị `Margin` hoặc `Offset` cho phù hợp.

![Ảnh chụp màn hình cho thấy việc thêm số Bates vào PDF trong C# với các số tuần tự hiển thị](add-bates-numbering-pdf.png "add bates numbering pdf")

*Văn bản thay thế ảnh: “Ảnh chụp màn hình cho thấy việc thêm số Bates vào PDF trong C# với các số tuần tự hiển thị.”*

## Bước 3 – Cách Chuyển Đổi PDFX4

Định dạng PDF/X‑4 là một phần của PDF được thiết kế cho việc in ấn và lưu trữ đáng tin cậy. Chuyển đổi sang PDF/X‑4 loại bỏ các tính năng không được hỗ trợ và đảm bảo tính nhất quán của hồ sơ màu. Dưới đây là **how to convert pdfx4** bằng cách sử dụng cùng lớp `Document`.

```csharp
// Load the original PDF you wish to convert
Document pdfSource = new Document("YOUR_DIRECTORY/source.pdf");

// Set up conversion options – we want PDF/X‑4 and we’ll delete any pages that cause errors
var conversionOptions = new PdfFormatConversionOptions(
    PdfFormat.PDF_X_4,               // target format
    ConvertErrorAction.Delete);     // action on conversion errors

// Perform the conversion
pdfSource.Convert(conversionOptions);

// Persist the new PDF/X‑4 file
pdfSource.Save("YOUR_DIRECTORY/pdfx4.pdf");

// Quick confirmation
Console.WriteLine("Converted to PDF/X‑4 and saved as pdfx4.pdf");
```

**Tại sao PDF/X‑4?**  
- Đảm bảo mọi phông chữ đều được nhúng.  
- Giữ nguyên độ trong suốt, không giống các phiên bản PDF/X‑1a cũ.  
- Thích hợp cho các máy in cao cấp yêu cầu quy trình nghiêm ngặt.

**Các khó khăn thường gặp khi bạn hỏi “how to convert pdfx4”:**  

- **Không hỗ trợ không gian màu:** Nếu nguồn sử dụng DeviceCMYK, quá trình chuyển đổi có thể thất bại trừ khi bạn nhúng một hồ sơ ICC.  
- **Hình ảnh lớn:** Quá trình chuyển đổi có thể làm tăng kích thước tệp; hãy cân nhắc giảm độ phân giải (`conversionOptions.ImageResolution = 300;`).  
- **Trường biểu mẫu:** Một số biến thể PDF/X loại bỏ các yếu tố tương tác. Nếu bạn cần giữ chúng, hãy kiểm tra lại mức độ tuân thủ của SDK.

## Bước 4 – Tạo Trường Biểu Mẫu PDF (Hai Widget Annotation)

Cuối cùng, chúng ta sẽ **create PDF form field** xuất hiện trên hai trang khác nhau. Một trường logic duy nhất có thể có nhiều biểu diễn trực quan (widget). Điều này hoàn hảo cho các phần “Ghi chú” cần được truy cập xuyên suốt tài liệu.

```csharp
// Start with a fresh document
Document formDoc = new Document();

// Add the first page and place the field there
Page firstPage = formDoc.Pages.Add();
var notesField = new TextBoxField(firstPage,
    new Rectangle(50, 700, 300, 750))   // left, bottom, right, top
{
    Name = "Notes",
    Value = "Enter your comments here..."
};

// Add a second page and attach a second widget to the same field
Page secondPage = formDoc.Pages.Add();
notesField.AddWidgetAnnotation(secondPage, new Rectangle(50, 500, 300, 550));

// Register the field with the document’s form collection
formDoc.Form.Add(notesField, notesField.Name);

// Save the result
formDoc.Save("YOUR_DIRECTORY/twoWidgets.pdf");
Console.WriteLine("PDF with two widget annotations saved as twoWidgets.pdf");
```

**Điều gì đang diễn ra bên trong:**  

- Đối tượng `TextBoxField` chứa *dữ liệu* (văn bản thực tế) và *giao diện mặc định* (phông chữ, kích thước).  
- `AddWidgetAnnotation` tạo một biểu diễn trực quan trên một trang khác nhưng lại trỏ về cùng một trường cơ bản, vì vậy bất kỳ nội dung người dùng nhập trên trang 1 sẽ tự động xuất hiện trên trang 2.  
- Khi thêm trường vào `formDoc.Form`, PDF trở nên **tương tác** và có thể được điền trong bất kỳ trình xem PDF nào.

**Mẹo cho các trường biểu mẫu đáng tin cậy:**  

- **Đặt phông chữ phù hợp** (`notesField.Font = FontTimesRoman;`) để tránh cảnh báo thay thế.  
- **Bật xác thực JavaScript** nếu quy trình của bạn yêu cầu (`notesField.Actions.OnBlur = "if (this.value.length > 200) app.alert('Too long');"`).  
- **Làm phẳng biểu mẫu** (`formDoc.Form.Flatten();`) khi bạn cuối cùng cần một phiên bản chỉ đọc để lưu trữ.

## Ví Dụ Hoàn Chỉnh Hoạt Động

Kết hợp tất cả lại, đây là một chương trình duy nhất bạn có thể sao chép‑dán, biên dịch và chạy. Nó minh họa **add bates numbering pdf**, **how to convert pdfx4**, và **create PDF form field** trong một luồng thống nhất.

```csharp
using System;
using YourPdfLibrary;   // Replace with your actual PDF SDK namespace

class Program
{
    static void Main()
    {
        // 1️⃣ Detect compromised signature
        Document signedDoc = new Document("YOUR_DIRECTORY/signed.pdf");
        bool compromised = signedDoc.IsSignatureCompromised();
        Console.WriteLine($"Signature compromised? {compromised}");

        // 2️⃣ Add Bates numbering – this is the core “add bates numbering pdf” step
        Document batesSource = new Document("YOUR_DIRECTORY/input.pdf");
        var batesOpts = new BatesNumberingOptions
        {
            Prefix = "2025-",
            Start = 1000,
            NumberFormat = "D6",
            Position = BatesNumberPosition.BottomRight,
            Margin = 20
        };
        batesSource.AddBatesNumbering(batesOpts);
        batesSource.Save("YOUR_DIRECTORY/bates.pdf");
        Console.WriteLine("Bates‑numbered PDF saved.");

        // 3️⃣ Convert to PDF/X‑4 – “how to convert pdfx4”
        Document pdfSource = new Document("YOUR_DIRECTORY/source.pdf");
        var convOpts = new PdfFormatConversionOptions(
            PdfFormat.PDF_X_4,
            ConvertErrorAction.Delete);
        pdfSource.Convert(convOpts);
        pdfSource.Save("YOUR_DIRECTORY/pdfx4.pdf");
        Console.WriteLine("Converted to PDF/X‑4.");

        // 4️⃣ Create a form field with two widgets – “create PDF form field”
        Document formDoc = new Document();
        Page p1 = formDoc.Pages.Add();
        var notes = new TextBoxField(p1,
            new Rectangle(50, 700, 300, 750))
        {
            Name = "Notes",
            Value = "Enter your comments here..."
        };
        Page p2 = formDoc.Pages.Add();
        notes.AddWidgetAnnotation(p2, new Rectangle(50, 500, 300, 550));
        formDoc.Form.Add(notes, notes.Name);
        formDoc.Save("YOUR_DIRECTORY/twoWidgets.pdf");
        Console.WriteLine("Form PDF with two widgets saved.");
    }
}
```

**Kết quả mong đợi:**  

```
Signature compromised? False

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}