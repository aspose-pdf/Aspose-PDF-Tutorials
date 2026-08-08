---
category: general
date: 2026-04-12
description: Thêm hình vào Word nhanh chóng bằng C#. Tìm hiểu cách định vị hình trong
  Word, chèn hình vào file docx và thêm XML tùy chỉnh cho bố cục nâng cao.
draft: false
keywords:
- add figure to word
- position figure in word
- insert figure into docx
- how to add custom xml
- how to position shape word
language: vi
og_description: Thêm hình vào Word nhanh chóng bằng C#. Tìm hiểu cách định vị hình
  trong Word, chèn hình vào file docx và thêm XML tùy chỉnh cho bố cục nâng cao.
og_title: Thêm Hình Vào Word – Hướng Dẫn Lập Trình C# Toàn Diện
tags:
- C#
- Word Automation
- Document Generation
title: Thêm Hình vào Word – Hướng Dẫn Lập Trình C# Đầy Đủ
url: /vi/net/programming-with-images/add-figure-to-word-complete-c-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Thêm Figure vào Word – Hướng Dẫn Lập Trình C# Đầy Đủ

Bạn đã bao giờ cần **add figure to Word** nhưng không chắc bắt đầu từ đâu? Bạn không phải là người duy nhất. Trong nhiều dự án tự động hoá văn phòng, phần còn thiếu là một hình ảnh hoặc sơ đồ được đặt hợp lý trong một phần custom XML. Hướng dẫn này sẽ chỉ cho bạn cách **position figure in Word**, chèn figure vào tệp *.docx*, và thậm chí chỉnh sửa custom XML bên dưới để shape hoạt động như bất kỳ đối tượng Word gốc nào.

Chúng tôi sẽ hướng dẫn một ví dụ thực tế sử dụng thư viện GemBox.Document (miễn phí cho tệp nhỏ, thương mại cho khối lượng công việc lớn). Khi kết thúc, bạn sẽ có một chương trình tự chứa, có thể chạy được, đặt một figure tại tọa độ X = 50, Y = 200 trong một container tagged‑content. Không có các phím tắt mơ hồ “xem tài liệu”—chỉ có mã rõ ràng, lý do hoạt động và các mẹo bạn có thể sao chép ngay vào dự án của mình.

## Yêu cầu trước

- .NET 6.0 hoặc sau (mã sẽ biên dịch với .NET Core 3.1 cũng được)
- **GemBox.Document** gói NuGet (`Install-Package GemBox.Document`)
- Tệp Word mẫu (`input.docx`) đã chứa một thẻ custom XML nơi bạn muốn figure xuất hiện
- Kiến thức cơ bản về C# (bạn sẽ thấy tại sao mỗi dòng quan trọng)

> **Pro tip:** Nếu bạn chưa có tài liệu đã được gắn thẻ trước, bạn có thể tạo một tài liệu trong Word bằng cách chèn *Content Control* → *XML Mapping Pane* → ánh xạ một phần custom XML. Thư viện sẽ coi điều khiển đó là `TaggedContent`.

## Bước 1 – Tải Tài Liệu Nguồn

Điều đầu tiên chúng ta làm là mở tệp *.docx* hiện có. `Document` là điểm vào cho tất cả các thao tác của GemBox.

```csharp
using GemBox.Document;
using System.Drawing;

// Set the license key (free version uses a limited license key)
ComponentInfo.SetLicense("FREE-LIMITED-KEY");

// Step 1: Load the source document
Document doc = new Document(@"YOUR_DIRECTORY\input.docx");
```

*Tại sao?* Việc tải tệp cho phép chúng ta truy cập các phần nội bộ, bao gồm bất kỳ container custom XML nào. Nếu không có bước này, chúng ta không thể xác định nút `TaggedContent` sẽ chứa figure của mình.

## Bước 2 – Truy Cập Nội Dung Được Gắn Thẻ (Custom XML Container)

Custom XML được lưu trong một *content control* trong Word. GemBox cung cấp nó dưới dạng `TaggedContent`. 

```csharp
// Step 2: Access the document's tagged content (the container for custom XML)
TaggedContent taggedContent = doc.TaggedContent;
```

Nếu tài liệu có nhiều phần được gắn thẻ, `TaggedContent` sẽ trả về **đầu tiên**. Bạn cũng có thể liệt kê `doc.TaggedContents` để chọn một thẻ cụ thể theo tên.

## Bước 3 – Tạo Phần Tử Figure

`FigureElement` đại diện cho một hình ảnh, biểu đồ, hoặc bất kỳ đối tượng trực quan nào mà Word coi là một *shape*. Chúng ta sẽ tạo nó bên trong container được gắn thẻ.

```csharp
// Step 3: Create a new figure element that will be placed inside the tagged content
FigureElement figure = taggedContent.CreateFigureElement();
```

*Tại sao tạo figure ở đây?* Khi gắn nó vào nút custom XML, Word biết rằng figure thuộc về phần logic đó, điều này quan trọng cho việc chỉnh sửa sau này hoặc quy trình dựa trên content‑control.

## Bước 4 – Định Vị Figure Một Cách Chính Xác

Word sử dụng đơn vị point (1 pt ≈ 1/72 in) để định vị. Cấu trúc `PointF` cho phép chúng ta đặt tọa độ X/Y một cách dễ dàng.

```csharp
// Step 4: Position the figure at the desired coordinates (X = 50, Y = 200)
figure.Position = new PointF(50, 200);
```

> **Cách định vị shape trong Word:** Thuộc tính `Position` nhận một `PointF` trong đó giá trị đầu tiên là độ lệch ngang (trái) và giá trị thứ hai là độ lệch dọc (trên) so với lề trang. Điều chỉnh các số này để tinh chỉnh vị trí.

## Bước 5 – Chèn Figure vào Cây Nội Dung Được Gắn Thẻ

Bây giờ chúng ta gắn figure vào phần tử gốc của cây custom XML. Điều này thực sự thêm shape vào tài liệu Word.

```csharp
// Step 5: Insert the figure into the root element of the tagged content tree
taggedContent.RootElement.AppendChild(figure);
```

Ở thời điểm này, figure đã nằm trong tài liệu, nhưng chưa có nguồn ảnh. Hãy thêm một file PNG đơn giản từ đĩa.

```csharp
// Optional: Load an image and assign it to the figure
using (var imageStream = System.IO.File.OpenRead(@"YOUR_DIRECTORY\sample.png"))
{
    figure.Image = new Image(imageStream);
}
```

## Bước 6 – Lưu Tài Liệu Đã Sửa Đổi

Cuối cùng, chúng ta ghi các thay đổi trở lại một tệp *.docx* mới.

```csharp
// Step 6: Save the updated document
doc.Save(@"YOUR_DIRECTORY\output.docx");
```

Khi bạn mở `output.docx` trong Word, bạn sẽ thấy hình ảnh được đặt chính xác tại (50, 200) bên trong khối custom‑XML mà bạn đã chỉ định.

### Ví Dụ Hoạt Động Đầy Đủ

```csharp
using GemBox.Document;
using System.Drawing;
using System.IO;

class Program
{
    static void Main()
    {
        // License (free version)
        ComponentInfo.SetLicense("FREE-LIMITED-KEY");

        // Load the source DOCX
        Document doc = new Document(@"YOUR_DIRECTORY\input.docx");

        // Access the first tagged content container
        TaggedContent taggedContent = doc.TaggedContent;

        // Create a new figure element
        FigureElement figure = taggedContent.CreateFigureElement();

        // Position the figure (X = 50 pt, Y = 200 pt)
        figure.Position = new PointF(50, 200);

        // Load an image file and assign it
        using (FileStream fs = File.OpenRead(@"YOUR_DIRECTORY\sample.png"))
        {
            figure.Image = new Image(fs);
        }

        // Append the figure to the custom XML root
        taggedContent.RootElement.AppendChild(figure);

        // Save the result
        doc.Save(@"YOUR_DIRECTORY\output.docx");
    }
}
```

**Kết quả mong đợi:** Khi mở `output.docx` sẽ hiển thị PNG được đặt chính xác ở vị trí bạn chỉ định, nằm trong phần custom XML. Nếu bạn kiểm tra XML của tài liệu (`.docx` → giải nén → `word/document.xml`), bạn sẽ thấy một phần tử `<w:pict>` với tọa độ `<v:shape>` đúng.

## Câu Hỏi Thường Gặp & Trường Hợp Đặc Biệt

### Nếu tài liệu có nhiều phần được gắn thẻ thì sao?

Sử dụng `doc.TaggedContents` để liệt kê và chọn theo tên thẻ:

```csharp
TaggedContent myTag = doc.TaggedContents.First(tc => tc.TagName == "MyCustomTag");
```

### Cách thêm chú thích cho figure?

```csharp
figure.Caption = new CaptionElement("Figure 1 – Sample Diagram");
```

### Điều này có hoạt động với Word 2010 và các phiên bản sau không?

Có. GemBox.Document nhắm tới tiêu chuẩn Open XML, tương thích với Word 2007 + (bao gồm 2010, 2013, 2016, 2019 và Microsoft 365).

### Nếu tôi cần xoay shape thì sao?

```csharp
figure.Rotation = 45; // degrees
```

### Cách thêm đồ họa vector thay vì ảnh raster?

```csharp
figure.Image = new Image(@"YOUR_DIRECTORY\vector.svg");
```

## Mẹo Chuyên Nghiệp & Những Cạm Bẫy

- **File paths:** Sử dụng `Path.Combine` để tránh các dấu phân tách được mã hoá cứng, đặc biệt trên các nền tảng không phải Windows.
- **License limits:** Giấy phép GemBox miễn phí giới hạn kích thước tài liệu ở 20 KB. Đối với tệp lớn hơn, mua khóa thương mại.
- **Performance:** Tái sử dụng một thể hiện `Document` duy nhất cho xử lý hàng loạt giảm đáng kể mức sử dụng bộ nhớ.
- **Shape overflow:** Nếu kích thước của figure vượt quá lề trang, Word sẽ cắt nó. Điều chỉnh `figure.Width` và `figure.Height` cho phù hợp.

## Kết Luận

Bây giờ bạn đã biết **how to add figure to Word**, **position figure in Word** một cách chính xác, và thao tác với custom XML bên dưới để shape hoạt động như bất kỳ phần tử gốc nào. Ví dụ hoàn chỉnh, có thể chạy được minh họa mọi bước—từ tải tài liệu, tạo `FigureElement`, đặt tọa độ, gắn ảnh, và cuối cùng lưu tệp *.docx* đã cập nhật.

Tiếp theo, hãy thử nghiệm với **insert figure into docx** bằng cách thêm nhiều figure, sử dụng vòng lặp, hoặc tạo biểu đồ ngay lập tức. Bạn cũng có thể khám phá **how to add custom xml** để có các content control phong phú hơn hoặc học **how to position shape word** trong bảng và header. Các khả năng là vô hạn, và với những nền tảng đã được trình bày, bạn đã sẵn sàng tự động hoá tài liệu Word như một chuyên gia.

Chúc bạn lập trình vui vẻ, và đừng ngần ngại để lại bình luận nếu gặp bất kỳ khó khăn nào!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}