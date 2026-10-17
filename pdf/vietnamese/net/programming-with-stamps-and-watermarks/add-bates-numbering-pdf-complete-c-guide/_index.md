---
category: general
date: 2026-02-14
description: Thêm đánh số Bates PDF vào tài liệu của bạn một cách dễ dàng. Tìm hiểu
  cách thêm số trang ở chân trang và đánh số tuần tự PDF với Aspose.Pdf trong vài
  phút.
draft: false
keywords:
- add bates numbering pdf
- add footer page numbers
- how to add bates numbers
- add sequential numbers pdf
language: vi
og_description: Thêm số Bates vào PDF nhanh chóng. Hướng dẫn này chỉ cách thêm số
  trang ở chân trang và các số thứ tự liên tiếp vào PDF bằng Aspose.Pdf, kèm mã đầy
  đủ và các mẹo.
og_title: Thêm số Bates vào PDF – Hướng dẫn C# từng bước
tags:
- Aspose.Pdf
- C#
- PDF automation
title: Thêm Đánh Số Bates vào PDF – Hướng Dẫn C# Toàn Diện
url: /vi/net/programming-with-stamps-and-watermarks/add-bates-numbering-pdf-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Thêm Số Bates vào PDF – Hướng Dẫn C# Đầy Đủ

Bạn đã bao giờ cần **thêm số Bates vào file PDF** nhưng không biết bắt đầu từ đâu chưa? Bạn không phải là người duy nhất. Các đội ngũ pháp lý, kiểm toán viên và bất kỳ ai xử lý một lượng lớn tài liệu đều thường hỏi: “Làm sao để thêm số Bates mà không làm hỏng bố cục?” Tin tốt là với Aspose.Pdf cho .NET, bạn có thể chèn những số này dưới dạng một footer đơn giản—không cần chỉnh sửa thủ công.

Trong tutorial này, chúng ta sẽ đi qua một giải pháp thực tế, từ đầu đến cuối, không chỉ **thêm số trang ở footer** mà còn cho phép bạn **thêm số thứ tự PDF** với tiền tố tùy chỉnh, kích thước phông chữ và căn chỉnh. Khi kết thúc, bạn sẽ có một chương trình C# sẵn sàng chạy, hiểu rõ lý do mỗi thiết lập quan trọng, và một vài mẹo chuyên nghiệp để tránh những lỗi phổ biến nhất.

## Những Điều Bạn Sẽ Học

- Cách tải một PDF hiện có và chuẩn bị cho việc đánh số Bates.  
- Những thuộc tính của **BatesNumberingOptions** kiểm soát giao diện và vị trí.  
- Cách áp dụng đánh số cho mọi trang chỉ bằng một lệnh.  
- Các cách tùy chỉnh tiền tố, số bắt đầu và lề cho các định dạng pháp lý khác nhau.  
- Xử lý các trường hợp đặc biệt—làm gì với PDF được mã hoá hoặc tài liệu đã có footer.

**Điều kiện tiên quyết**: .NET 6+ (hoặc .NET Framework 4.7+), phiên bản Aspose.Pdf mới (ví dụ dùng 23.10), và một file PDF mà bạn có quyền chỉnh sửa. Không cần thư viện bên thứ ba nào khác.

---

## Bước 1 – Tải PDF Cần Đánh Số

Điều đầu tiên chúng ta làm là tạo một thể hiện `Document` trỏ tới file nguồn. Sử dụng mẫu `using var` giúp tự động giải phóng handle của file.

```csharp
using Aspose.Pdf;

// Replace with the path to your source PDF
using var doc = new Document("YOUR_DIRECTORY/input.pdf");
```

> **Tại sao điều này quan trọng:** Aspose.Pdf đọc toàn bộ cấu trúc PDF vào bộ nhớ, cho phép chúng ta thao tác các trang, chú thích và siêu dữ liệu mà không chạm vào file gốc trên đĩa. Nếu PDF được bảo vệ bằng mật khẩu, bạn có thể truyền mật khẩu vào constructor—xem chú thích “PDF được mã hoá” ở cuối.

---

## Bước 2 – Định Nghĩa Các Tùy Chọn Đánh Số Bates

Số Bates thực chất là footer trang với một tiền tố có thể cấu hình và một bộ đếm tuần tự. Lớp `BatesNumberingOptions` cho phép bạn tinh chỉnh mọi khía cạnh hình ảnh.

```csharp
var batesOptions = new BatesNumberingOptions
{
    // The text that will appear before the numeric part
    Prefix = "ABC-",

    // Starting number; the library will increment this automatically
    StartNumber = 1000,

    // Font size of the footer text (points)
    FontSize = 12,

    // Align the number to the right side of the page
    HorizontalAlignment = HorizontalAlignment.Right,

    // Place the number at the bottom of the page
    VerticalAlignment = VerticalAlignment.Bottom,

    // Margins: left, top, right, bottom (in points)
    Margin = new MarginInfo(0, 20, 0, 0)
};
```

### Mẹo nhanh

- **Prefix**: Dùng một định danh ngắn, duy nhất (ví dụ: số vụ) để footer dễ đọc.  
- **StartNumber**: Các công ty luật thường bắt đầu từ `1` hoặc một giá trị offset tùy chỉnh; chọn gì phù hợp với hệ thống lưu trữ của bạn.  
- **Margins**: Lề dưới `20` điểm giúp văn bản tránh xa các chú thích hoặc chữ ký có thể đã nằm gần mép trang.

---

## Bước 3 – Áp Dụng Đánh Số Cho Tất Cả Các Trang

Sau khi đã cấu hình các tùy chọn, việc chèn thực tế chỉ cần một dòng lệnh. Aspose.Pdf tự động xử lý phân trang, cập nhật các stream nội dung hiện có và tôn trọng độ xoay của trang.

```csharp
doc.Pages.AddBatesNumbering(batesOptions);
```

> **Điều gì đang diễn ra phía sau?** Thư viện lặp qua từng đối tượng `Page`, tạo một `TextFragment` kết hợp tiền tố và bộ đếm hiện tại, rồi vẽ nó bằng hệ tọa độ của trang. Vì chúng ta đặt `HorizontalAlignment.Right` và `VerticalAlignment.Bottom`, văn bản sẽ tự động dính góc dưới‑phải bất kể kích thước trang.

---

## Bước 4 – Lưu PDF Đã Được Sửa Đổi

Cuối cùng, ghi kết quả ra một file mới. Ghi đè lên file gốc là có thể, nhưng việc giữ một bản sao giúp quản lý phiên bản dễ dàng hơn.

```csharp
doc.Save("YOUR_DIRECTORY/output.pdf");
```

Nếu bạn cần giữ nguyên siêu dữ liệu gốc (tác giả, ngày tạo), Aspose.Pdf sẽ sao chép chúng theo mặc định. Bạn cũng có thể chỉ định một đối tượng `SaveOptions` để tuân thủ PDF/A hoặc nén file.

---

## Ví Dụ Hoàn Chỉnh

Dưới đây là chương trình đầy đủ, sẵn sàng chạy. Dán vào một dự án console app, chỉnh đường dẫn file, và nhấn **F5**.

```csharp
using Aspose.Pdf;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source PDF
        using var doc = new Document("YOUR_DIRECTORY/input.pdf");

        // 2️⃣ Configure Bates numbering options
        var batesOptions = new BatesNumberingOptions
        {
            Prefix = "ABC-",
            StartNumber = 1000,
            FontSize = 12,
            HorizontalAlignment = HorizontalAlignment.Right,
            VerticalAlignment = VerticalAlignment.Bottom,
            Margin = new MarginInfo(0, 20, 0, 0)
        };

        // 3️⃣ Apply numbering to every page
        doc.Pages.AddBatesNumbering(batesOptions);

        // 4️⃣ Save the output PDF
        doc.Save("YOUR_DIRECTORY/output.pdf");

        System.Console.WriteLine("Bates numbering added successfully!");
    }
}
```

**Kết quả mong đợi:** Mỗi trang của `output.pdf` giờ sẽ hiển thị một footer như `ABC-1000`, `ABC-1001`, … được gắn ở góc dưới‑phải. Mở file trong bất kỳ trình đọc PDF nào để kiểm tra.

---

## Xử Lý Các Biến Thể Thông Thường

### Chỉ Thêm Số Trang Ở Footer

Nếu bạn chỉ cần số trang đơn giản mà không có tiền tố, đặt `Prefix = ""` và có thể điều chỉnh lề để tránh va chạm với footer hiện có.

```csharp
batesOptions.Prefix = "";
batesOptions.StartNumber = 1; // classic page numbering
```

### Thay Đổi Căn Chỉnh

Một số tài liệu pháp lý yêu cầu số được căn giữa ở đáy trang. Thay đổi căn chỉnh như sau:

```csharp
batesOptions.HorizontalAlignment = HorizontalAlignment.Center;
```

### Xử Lý PDF Được Mã Hoá

Khi PDF nguồn được bảo vệ bằng mật khẩu, cung cấp mật khẩu như sau:

```csharp
using var doc = new Document("secure.pdf", new LoadOptions { Password = "mySecret" });
```

Các bước còn lại của quy trình vẫn giống nhau.

### Bỏ Qua Các Footer Đã Tồn Tại

Nếu tài liệu đã có một footer mà bạn không muốn ghi đè, bạn có thể thêm một chuỗi tùy chỉnh phía trước để số mới trở nên riêng biệt, hoặc tự lặp qua các trang và chỉ thêm `TextFragment` ở những trang không có footer. Lớp `Page` của thư viện cung cấp các collection `Annotations` và `Contents` để kiểm soát chi tiết.

---

## Mẹo Chuyên Nghiệp & Những Cạm Bẫy Thường Gặp

- **Tránh cắt ngắn**: Lề dưới quá nhỏ có thể khiến văn bản bị cắt khi in. Hãy thử in ra bản giấy nếu bạn sẽ phát hành bản cứng.  
- **Hiệu năng**: Thêm số Bates vào PDF 500 trang mất dưới một giây trên laptop hiện đại, nhưng khi xử lý hàng loạt lớn, việc song song sẽ hữu ích—chỉ cần nhớ `Document` không an toàn với đa luồng, mỗi luồng cần một thể hiện riêng.  
- **Tương thích phiên bản**: Mã này hoạt động với Aspose.Pdf 23.10 trở lên. Nếu bạn dùng phiên bản cũ hơn, tên thuộc tính vẫn giống nhưng hàm khởi tạo `MarginInfo` có thể yêu cầu đối số kiểu `float`.  
- **Tuân thủ pháp lý**: Một số khu vực yêu cầu số Bates phải đặt ở vị trí cụ thể (ví dụ: dưới‑trái). Điều chỉnh `HorizontalAlignment` cho phù hợp.

---

## Kết Luận

Chúng ta vừa minh họa cách **thêm số Bates vào file PDF** bằng Aspose.Pdf cho .NET, bao gồm từ việc tải tài liệu đến lưu phiên bản cuối cùng với footer sạch sẽ. Bằng cách tinh chỉnh một vài thuộc tính, bạn cũng có thể **thêm số trang ở footer**, **thêm số thứ tự PDF**, hoặc tùy chỉnh giao diện để đáp ứng bất kỳ tiêu chuẩn pháp lý nào.

Sẵn sàng cho bước tiếp theo? Hãy thử kết hợp kỹ thuật này với việc trích xuất OCR để nhúng từ khóa có thể tìm kiếm cùng với số Bates, hoặc tự động hoá quy trình cho toàn bộ thư mục bằng `Directory.GetFiles`. Khả năng là vô hạn, và nền tảng bạn vừa có sẽ giúp các mở rộng trở nên nhẹ nhàng.

Chúc lập trình vui vẻ, và chúc các PDF của bạn luôn được đánh số hoàn hảo!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}