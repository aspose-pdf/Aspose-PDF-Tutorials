---
category: general
date: 2026-06-21
description: Tạo trường textbox PDF bằng C# và học cách sao chép trường biểu mẫu PDF
  hoặc thêm textbox vào biểu mẫu PDF chỉ với vài dòng mã.
draft: false
keywords:
- create pdf textbox field
- duplicate pdf form field
- add textbox to pdf form
- pdf form automation
- c# pdf library
language: vi
og_description: Tạo nhanh trường textbox PDF. Hướng dẫn này chỉ cách sao chép trường
  biểu mẫu PDF và thêm textbox vào biểu mẫu PDF bằng thư viện PDF hiện đại C#.
og_title: Tạo trường textbox PDF – Hướng dẫn C# đầy đủ
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Create PDF textbox field with C# and learn how to duplicate PDF form
    field or add textbox to PDF form in just a few lines of code.
  headline: Create PDF Textbox Field – Step‑by‑Step Guide
  type: TechArticle
- description: Create PDF textbox field with C# and learn how to duplicate PDF form
    field or add textbox to PDF form in just a few lines of code.
  name: Create PDF Textbox Field – Step‑by‑Step Guide
  steps:
  - name: What if I need the field on *more* than two pages?
    text: Just repeat the clone‑and‑add steps for each additional page. The underlying
      data object stays the same, so all widgets stay in sync.
  - name: How do I change the appearance (font, border, background)?
    text: Each `Widget` has a `SetBorderColor`, `SetBorderWidth`, and `SetBackgroundColor`
      method. You can also assign a default appearance string (`DA`) to control the
      font and size.
  - name: Can I make the field read‑only after the user fills it?
    text: Yes. Set the `ReadOnly` flag on the field after you’ve collected the data,
      or toggle it based on your workflow.
  - name: What about PDFs that already contain a form?
    text: If the document already has an AcroForm, `doc.GetForm()` simply returns
      it. You can then add new fields without disturbing existing ones. Just be careful
      to use unique field names.
  type: HowTo
tags:
- PDF
- C#
- FormFields
title: Tạo Trường Văn Bản PDF – Hướng Dẫn Từng Bước
url: /vi/net/programming-with-forms/create-pdf-textbox-field-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo Trường Văn Bản PDF – Hướng Dẫn C# Đầy Đủ

Bạn đã bao giờ cần **tạo trường văn bản PDF** nhưng không chắc nên gọi API nào? Bạn không phải là người duy nhất. Dù bạn đang xây dựng một cổng ký hợp đồng hay một bảng thu thập dữ liệu đơn giản, việc thêm các ô nhập liệu tương tác vào PDF là kỹ năng cốt lõi cho bất kỳ nhà phát triển tự động hoá biểu mẫu nào.  

Trong hướng dẫn này, chúng ta sẽ đi qua một ví dụ thực tế không chỉ **thêm textbox vào biểu mẫu PDF**, mà còn cho thấy cách **nhân bản trường biểu mẫu PDF** để cùng một dữ liệu xuất hiện trên nhiều trang. Khi hoàn thành, bạn sẽ có một chương trình chạy được mà có thể đưa vào bất kỳ dự án .NET nào.

## Những Điều Cần Chuẩn Bị

- .NET 6.0 trở lên (mã cũng chạy trên .NET Core)  
- Thư viện PDF C# hiện đại – đoạn mã dưới đây sử dụng **PDFTron SDK**, nhưng các khái niệm cũng áp dụng cho iText 7, PdfSharp, hoặc các thư viện khác.  
- Visual Studio 2022 (hoặc bất kỳ IDE nào bạn thích)  

Đó là tất cả – không cần dịch vụ phụ trợ, không có phụ thuộc lạ. Nếu bạn đã có một file PDF muốn bổ sung, chỉ cần trỏ mã tới nó.

---

## Bước 1: Thiết Lập Dự Án và Nhập SDK

Đầu tiên, tạo một ứng dụng console:

```bash
dotnet new console -n PdfFormDemo
cd PdfFormDemo
```

Thêm gói NuGet PDFTron:

```bash
dotnet add package PDFTron.NET
```

Bây giờ mở `Program.cs` và khai báo các namespace cần thiết:

```csharp
using System;
using pdftron;
using pdftron.Common;
using pdftron.PDF;
using pdftron.SDF;
```

> **Mẹo chuyên nghiệp:** Nếu bạn dùng thư viện khác, thay thế các câu lệnh `using` bằng các tương đương (ví dụ, `iText.Kernel.Pdf` cho iText 7).

## Bước 2: Khởi Tạo Tài Liệu PDF và Biểu Mẫu

Chúng ta sẽ bắt đầu với một PDF mới có hai trang – trang nguồn cho textbox gốc và trang đích cho bản sao.

```csharp
PDFNet.Initialize();                     // Initialize the PDFTron runtime

// Create a new PDF document
using (PDFDoc doc = new PDFDoc())
{
    // Add two blank pages (letter size)
    Page sourcePage = doc.PageCreate(new Size(612, 792));
    doc.PagePushBack(sourcePage);
    Page targetPage = doc.PageCreate(new Size(612, 792));
    doc.PagePushBack(targetPage);

    // Get (or create) the AcroForm object
    Form form = doc.GetForm();
```

Đối tượng `Form` là nơi chứa tất cả các trường tương tác. Nếu tài liệu chưa có biểu mẫu, `GetForm()` sẽ tạo một biểu mẫu cho chúng ta.

## Bước 3: **Tạo Trường Văn Bản PDF** trên Trang Đầu Tiên

Tiếp theo là phần cốt lõi của tutorial – tạo một trường textbox. Các tọa độ hình chữ nhật được biểu diễn bằng điểm (1 inch = 72 điểm). Ví dụ đặt ô gần phần trên‑giữa của trang đầu.

```csharp
    // Step 1: Create a text box field on the first page and set its initial value
    TextBoxField textBoxField = new TextBoxField(sourcePage, new Rect(100, 500, 300, 520))
    {
        Value = "Sample"
    };
```

Tại sao chúng ta đặt `Value` ngay lập tức? Việc điền sẵn giá trị giúp người dùng có gợi ý về dữ liệu mong muốn, đồng thời chứng minh trường hoạt động đầy đủ.

## Bước 4: Thêm Trường Vào Biểu Mẫu – **Thêm Textbox vào Biểu Mẫu PDF**

Tiếp theo, chúng ta đăng ký trường với biểu mẫu bằng một tên logic. Tên này sẽ được dùng khi bạn cần đọc hoặc sửa dữ liệu của trường bằng mã.

```csharp
    // Step 2: Add the field to the form with a logical name
    form.Add(textBoxField, "multiBox");
```

Chọn một tên rõ ràng (như `"multiBox"`) sẽ giúp code sau này dễ hiểu hơn, đặc biệt khi bạn có hàng chục trường.

## Bước 5: **Nhân Bản Trường Biểu Mẫu PDF** trên Trang Khác

Một yêu cầu phổ biến là hiển thị cùng một trường trên nhiều trang – ví dụ ô “Tên Khách Hàng” xuất hiện trên mọi trang hoá đơn. PDFTron cho phép chúng ta sao chép widget annotation, tức là phần hiển thị của trường.

```csharp
    // Step 3: Clone the field's widget annotation so it can appear on another page
    Widget clonedWidget = textBoxField.CreateWidgetAnnotation();

    // Step 4: Place the cloned widget on the second page
    targetPage.Annotations.Add(clonedWidget);
```

Widget được sao chép chia sẻ cùng một dữ liệu nền với textbox gốc. Khi người dùng nhập vào một instance, các instance khác sẽ tự động cập nhật – đó là sức mạnh của **duplicate PDF form field**.

## Bước 6: Lưu Tài Liệu và Dọn Dẹp

Cuối cùng, ghi PDF ra đĩa và tắt runtime PDFNet.

```csharp
    // Save the resulting PDF
    doc.Save("output.pdf", SDFDoc.SaveOptions.e_linearized);
    Console.WriteLine("PDF created: output.pdf");
}

// Shut down PDFNet (optional but good practice)
PDFNet.Terminate();
```

Chạy chương trình sẽ tạo một PDF hai trang (`output.pdf`). Mở nó bằng Adobe Acrobat Reader, nhấp vào textbox trên trang 1, gõ một vài ký tự, rồi chuyển sang trang 2 – cùng một văn bản sẽ xuất hiện ngay lập tức. Đây là một ví dụ **create pdf textbox field** hoàn chỉnh với trường đã được nhân bản.

---

## Ví Dụ Hoàn Chỉnh (Sẵn Sàng Sao Chép‑Dán)

```csharp
// Program.cs
using System;
using pdftron;
using pdftron.Common;
using pdftron.PDF;
using pdftron.SDF;

class Program
{
    static void Main()
    {
        PDFNet.Initialize();

        using (PDFDoc doc = new PDFDoc())
        {
            // Create two pages
            Page sourcePage = doc.PageCreate(new Size(612, 792));
            doc.PagePushBack(sourcePage);
            Page targetPage = doc.PageCreate(new Size(612, 792));
            doc.PagePushBack(targetPage);

            // Get the form (creates one if missing)
            Form form = doc.GetForm();

            // Step 1: Create a text box field on the first page
            TextBoxField textBoxField = new TextBoxField(sourcePage,
                new Rect(100, 500, 300, 520))
            {
                Value = "Sample"
            };

            // Step 2: Add the field to the form
            form.Add(textBoxField, "multiBox");

            // Step 3: Clone the widget so it appears on page 2
            Widget clonedWidget = textBoxField.CreateWidgetAnnotation();

            // Step 4: Attach the cloned widget to the second page
            targetPage.Annotations.Add(clonedWidget);

            // Save the file
            doc.Save("output.pdf", SDFDoc.SaveOptions.e_linearized);
            Console.WriteLine("PDF created: output.pdf");
        }

        PDFNet.Terminate();
    }
}
```

**Kết quả mong đợi:** Một file tên `output.pdf` chứa hai trang. Cả hai trang đều hiển thị cùng một textbox có thể chỉnh sửa mang nhãn “Sample”. Việc chỉnh sửa một textbox sẽ cập nhật ngay lập tức textbox còn lại.

---

## Các Câu Hỏi Thường Gặp & Trường Hợp Cạnh

### Nếu tôi cần trường trên *nhiều hơn* hai trang thì sao?

Chỉ cần lặp lại các bước sao chép‑và‑thêm cho mỗi trang bổ sung. Đối tượng dữ liệu nền vẫn giữ nguyên, vì vậy tất cả widget sẽ đồng bộ.

```csharp
Widget anotherClone = textBoxField.CreateWidgetAnnotation();
thirdPage.Annotations.Add(anotherClone);
```

### Làm sao thay đổi giao diện (phông chữ, viền, nền)?

Mỗi `Widget` có các phương thức `SetBorderColor`, `SetBorderWidth`, và `SetBackgroundColor`. Bạn cũng có thể gán một chuỗi appearance mặc định (`DA`) để điều khiển phông chữ và kích thước.

```csharp
textBoxField.SetBorderColor(new ColorPt(0, 0, 1), 3); // blue border
textBoxField.SetBackgroundColor(new ColorPt(0.9, 0.9, 0.9), 3); // light gray fill
textBoxField.SetDefaultAppearance("Helvetica 12 Tf 0 g");
```

### Có thể đặt trường thành chỉ‑đọc sau khi người dùng nhập không?

Có. Đặt cờ `ReadOnly` trên trường sau khi đã thu thập dữ liệu, hoặc bật/tắt tùy theo luồng công việc của bạn.

```csharp
textBoxField.SetFlag(Field.Flag.e_readonly, true);
```

### Còn các PDF đã có sẵn biểu mẫu thì sao?

Nếu tài liệu đã có AcroForm, `doc.GetForm()` chỉ trả về nó. Bạn có thể thêm các trường mới mà không làm ảnh hưởng tới các trường hiện có. Chỉ cần chú ý dùng tên trường duy nhất.

---

## Mẹo Cho Các Dự Án Thực Tế

- **Quy tắc đặt tên:** Đặt tiền tố cho tên trường theo trang hoặc phần (ví dụ, `invoice_customer_name`) để tránh xung đột.  
- **Kiểm tra hợp lệ:** Sử dụng hành động JavaScript (`field.SetAction(Field.Action.e_keystroke, "event.rc = /^[A-Za-z]+$/.test(event.change);")`) nếu cần xác thực phía client.  
- **Hiệu năng:** Khi làm việc với PDF lớn, gọi `doc.Lock()` trước các thao tác bulk để giảm tải I/O.  
- **Khả năng truy cập:** Đặt thuộc tính `AlternateName` để trình đọc màn hình mô tả trường.

---

## Kết Luận

Chúng ta vừa **tạo một trường văn bản PDF**, trình bày cách **nhân bản trường biểu mẫu PDF** trên các trang, và minh họa cách **thêm textbox vào biểu mẫu PDF** bằng C#. Mã đầy đủ, có thể chạy được nằm ở trên, và bạn có thể mở rộng nó với kiểu dáng, kiểm tra hợp lệ, hoặc thêm trang tùy nhu cầu.

Sẵn sàng bước tiếp? Hãy thử nhúng một dropdown (`ChoiceField`) hoặc widget chữ ký, hoặc khám phá cách flatten biểu mẫu sau khi nhập dữ liệu để lưu trữ. PDFTron SDK (hoặc bất kỳ thư viện tương đương nào) cung cấp các khối xây dựng—trí tưởng tượng của bạn quyết định hình dạng cuối cùng.

Nếu gặp khó khăn, để lại bình luận bên dưới hoặc tham khảo tài liệu chính thức của thư viện; chúng chứa rất nhiều ví dụ bổ trợ cho những gì chúng ta đã trình bày. Chúc bạn lập trình vui vẻ, và hy vọng các biểu mẫu của bạn luôn đồng bộ!

## Bạn Nên Học Gì Tiếp Theo?


Các tutorial sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật đã được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh với giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Cách Tạo PDF với Aspose – Thêm Trường Biểu Mẫu và Trang](/pdf/english/net/programming-with-forms/how-to-create-pdf-with-aspose-add-form-field-and-pages/)
- [Thêm Trường Biểu Mẫu trong Tài Liệu PDF bằng Java](/pdf/english/java/pdf-form-fields/add-form-field-in-pdf-document-using-java/)
- [Thêm Trường Biểu Mẫu trong Tài Liệu PDF bằng Java](/pdf/german/java/pdf-form-fields/add-form-field-in-pdf-document-using-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}