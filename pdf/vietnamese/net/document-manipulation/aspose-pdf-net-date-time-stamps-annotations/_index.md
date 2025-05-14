---
"date": "2025-04-11"
"description": "Tìm hiểu cách thêm ngày tháng và thời gian hoặc chú thích hiệu quả vào tài liệu PDF của bạn bằng Aspose.PDF cho .NET. Nâng cao khả năng quản lý tài liệu bằng các bước dễ thực hiện sau."
"title": "Thêm Dấu Ngày & Giờ vào PDF Sử dụng Aspose.PDF cho .NET"
"url": "/vi/net/document-manipulation/aspose-pdf-net-date-time-stamps-annotations/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# Thêm Dấu Ngày & Giờ vào PDF Sử dụng Aspose.PDF cho .NET

## Giới thiệu

Trong thời đại kỹ thuật số ngày nay, quản lý tài liệu hiệu quả là điều tối quan trọng đối với doanh nghiệp và cá nhân. Thêm dấu ngày tháng và thời gian hoặc chú thích vào PDF của bạn có thể tăng cường tính toàn vẹn và tổ chức dữ liệu. Hướng dẫn này trình bày cách tích hợp các tính năng này bằng Aspose.PDF cho .NET.

**Những điểm chính cần ghi nhớ:**
- Thêm ngày và giờ hiện tại dưới dạng dấu văn bản trên trang PDF được chỉ định.
- Tạo chú thích văn bản tự do tại các vị trí mong muốn trong tài liệu.
- Thực hiện theo các biện pháp tốt nhất để có hiệu suất tối ưu với Aspose.PDF cho .NET.

## Điều kiện tiên quyết
Trước khi bắt đầu, hãy đảm bảo bạn có:

### Thư viện và phiên bản bắt buộc
- **Aspose.PDF cho .NET**: Một thư viện mạnh mẽ để thao tác PDF mà không cần Adobe Acrobat. Sử dụng phiên bản 21.x trở lên.

### Yêu cầu thiết lập môi trường
- Môi trường phát triển với .NET Framework 4.5+ hoặc .NET Core 2.0+
- Visual Studio hoặc một IDE khác hỗ trợ lập trình C#

### Điều kiện tiên quyết về kiến thức
- Hiểu biết cơ bản về cấu trúc dự án C# và .NET
- Quen thuộc với việc xử lý các tập tin trong cấu trúc thư mục

## Thiết lập Aspose.PDF cho .NET
Cài đặt Aspose.PDF bằng một trong các phương pháp sau:

**Sử dụng .NET CLI:**
```bash
dotnet add package Aspose.PDF
```

**Sử dụng Trình quản lý gói:**
```powershell
Install-Package Aspose.PDF
```

**Thông qua Giao diện người dùng của Trình quản lý gói NuGet:**
- Mở Trình quản lý gói NuGet trong IDE của bạn.
- Tìm kiếm "Aspose.PDF" và cài đặt phiên bản mới nhất.

### Các bước xin cấp giấy phép
Để sử dụng đầy đủ Aspose.PDF:
1. **Dùng thử miễn phí:** Tải xuống giấy phép tạm thời để khám phá tất cả các tính năng.
2. **Giấy phép tạm thời:** Yêu cầu gia hạn giấy phép đánh giá nếu cần thiết.
3. **Mua:** Mua giấy phép sử dụng lâu dài từ trang web Aspose.

Khởi tạo giấy phép của bạn trong mã:
```csharp
Aspose.Pdf.License license = new Aspose.Pdf.License();
license.SetLicense("Path to License File");
```

## Hướng dẫn thực hiện
Hãy thêm dấu ngày tháng và thời gian vào tệp PDF.

### Tính năng 1: Thêm Dấu Ngày Giờ vào PDF
Tính năng này thêm ngày và giờ hiện tại dưới dạng dấu văn bản vào trang đầu tiên của tài liệu PDF được chỉ định.

#### Thực hiện từng bước

##### 1. Mở tài liệu PDF hiện có
Tải tài liệu mục tiêu của bạn:
```csharp
document pdfDocument = new Document("YOUR_DOCUMENT_DIRECTORY/AddTextStamp.pdf");
```

##### 2. Lấy Ngày và Giờ Hiện Tại dưới dạng Chuỗi
Định dạng ngày và giờ hiện tại:
```csharp
string annotationText = DateTime.Now.ToString("MM/dd/yy hh:mm:ss tt ");
```

##### 3. Tạo con dấu văn bản với ngày và giờ hiện tại
Tạo một `TextStamp` ví dụ sử dụng chuỗi định dạng:
```csharp
TextStamp textStamp = new TextStamp(annotationText);
textStamp.BottomMargin = 10;
textStamp.RightMargin = 20;
textStamp.HorizontalAlignment = HorizontalAlignment.Right;
textStamp.VerticalAlignment = VerticalAlignment.Bottom;
```

##### 4. Thêm Dấu Văn Bản vào Trang Đầu Tiên
Thêm dấu vào trang đầu tiên của tài liệu:
```csharp
document.Pages[1].AddStamp(textStamp);
```

##### 5. Tạo và Thêm FreeTextAnnotation (Tùy chọn)
Đối với các chú thích phức tạp hơn, hãy tạo một `FreeTextAnnotation`:
```csharp
DefaultAppearance default_appearance = new DefaultAppearance("Arial", 6, System.Drawing.Color.Black);
FreeTextAnnotation textAnnotation = new FreeTextAnnotation(document.Pages[1], new Aspose.Pdf.Rectangle(0, 0, 0, 0), default_appearance)
{
    Name = "Stamp",
    Contents = textStamp.Value
};
textAnnotation.Border = new Border(textAnnotation) { Width = 0 };
document.Pages[1].Annotations.Add(textAnnotation);
```

##### 6. Lưu tài liệu đã sửa đổi
Lưu thay đổi của bạn:
```csharp
string outputDir = "YOUR_OUTPUT_DIRECTORY/AddDateTimeStamp_out.pdf";
document.Save(outputDir);
```

### Tính năng 2: Thêm chú thích FreeText vào PDF
Thêm chú thích văn bản tự do vào bất kỳ vị trí mong muốn nào trong tài liệu PDF.

#### Thực hiện từng bước

##### 1. Mở một tài liệu PDF hiện có
Tải tài liệu mục tiêu của bạn:
```csharp
document pdfDocument = new Document("YOUR_DOCUMENT_DIRECTORY/Sample.pdf");
```

##### 2. Xác định diện tích hình chữ nhật cho chú thích
Chỉ định nơi đặt chú thích trên trang:
```csharp
Aspose.Pdf.Rectangle rect = new Aspose.Pdf.Rectangle(100, 400, 200, 450);
```

##### 3. Tạo FreeTextAnnotation với Giao diện và Vị trí được Chỉ định
Khởi tạo chú thích của bạn với cài đặt văn bản và giao diện mong muốn:
```csharp
DefaultAppearance default_appearance = new DefaultAppearance("Arial", 12, System.Drawing.Color.Blue);
FreeTextAnnotation freeTextAnnotation = new FreeTextAnnotation(pdfDocument.Pages[1], rect, default_appearance)
{
    Contents = "This is a sample annotation",
    Title = "Sample Annotation"
};
```

##### 4. Đặt Kiểu Đường viền và Thêm Chú thích
Đảm bảo kiểu đường viền phù hợp với nhu cầu của bạn (vô hình trong trường hợp này):
```csharp
freeTextAnnotation.Border = new Border(freeTextAnnotation) { Width = 0 };
pdfDocument.Pages[1].Annotations.Add(freeTextAnnotation);
```

##### 5. Lưu tài liệu đã sửa đổi
Lưu tài liệu của bạn với chú thích mới được thêm vào:
```csharp
string outputDir = "YOUR_OUTPUT_DIRECTORY/FreeTextAnnotation_out.pdf";
document.Save(outputDir);
```

## Ứng dụng thực tế
Việc thêm dấu ngày tháng và chú thích vào tệp PDF rất hữu ích trong nhiều ngành công nghiệp khác nhau:
- **Văn bản pháp lý**: Đảm bảo tuân thủ bằng cách đóng dấu thời gian cho những thay đổi.
- **Bài báo học thuật**: Hỗ trợ chỉnh sửa cộng tác bằng chú thích.
- **Hồ sơ tài chính**: Duy trì các dấu vết kiểm toán chính xác với các báo cáo có dấu thời gian.
- **Tài liệu kỹ thuật**: Làm nổi bật các bản cập nhật hoặc ghi chú quan trọng trong sách hướng dẫn.

## Cân nhắc về hiệu suất
Để có hiệu suất tối ưu khi sử dụng Aspose.PDF cho .NET:
- **Xử lý hàng loạt**: Xử lý nhiều tệp PDF theo từng đợt để giảm chi phí.
- **Quản lý bộ nhớ**: Sử dụng `Dispose` phương pháp giải phóng tài nguyên bộ nhớ sau khi xử lý mỗi tài liệu.
- **Phông chữ và hình ảnh được tối ưu hóa**: Giới hạn kiểu phông chữ và độ phân giải hình ảnh để giảm kích thước tệp.

## Phần kết luận
Tích hợp Aspose.PDF cho .NET cho phép bạn thêm tính năng đóng dấu ngày tháng và chú thích vào tài liệu PDF, tăng cường chức năng. Các công cụ này cải thiện tính toàn vẹn của dữ liệu và hợp lý hóa việc quản lý tài liệu.

Thử nghiệm với nhiều cấu hình khác nhau và khám phá các tính năng bổ sung do Aspose.PDF cung cấp để đáp ứng nhu cầu cụ thể của bạn.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}