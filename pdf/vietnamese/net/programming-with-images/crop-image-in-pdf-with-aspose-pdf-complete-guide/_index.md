---
category: general
date: 2026-06-08
description: Cắt ảnh trong PDF bằng Aspose.PDF trong C#. Tìm hiểu cách tạo PDF có
  ảnh, lưu PDF có ảnh và thêm ảnh vào PDF chỉ trong vài dòng.
draft: false
keywords:
- crop image in pdf
- create pdf with image
- save pdf with image
- how to add image to pdf
- how to crop image pdf
language: vi
og_description: Cắt ảnh trong PDF bằng Aspose.PDF trong C#. Hướng dẫn này cho thấy
  cách tạo PDF có ảnh, lưu PDF có ảnh và thêm ảnh vào PDF một cách nhanh chóng.
og_title: Cắt ảnh trong PDF bằng Aspose.PDF – Hướng dẫn đầy đủ
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Crop image in PDF using Aspose.PDF in C#. Learn how to create PDF with
    image, save PDF with image, and add image to PDF in just a few lines.
  headline: Crop Image in PDF with Aspose.PDF – Complete Guide
  type: TechArticle
- description: Crop image in PDF using Aspose.PDF in C#. Learn how to create PDF with
    image, save PDF with image, and add image to PDF in just a few lines.
  name: Crop Image in PDF with Aspose.PDF – Complete Guide
  steps:
  - name: '**Image stream** – the raw bytes of your picture.'
    text: '**Image stream** – the raw bytes of your picture.'
  - name: '**Placement rectangle** – where on the page the image lives.'
    text: '**Placement rectangle** – where on the page the image lives.'
  - name: '**Crop rectangle** – the portion of the image you actually want to render.'
    text: '**Crop rectangle** – the portion of the image you actually want to render.'
  type: HowTo
tags:
- Aspose.PDF
- C#
- PDF manipulation
- Image processing
title: Cắt ảnh trong PDF bằng Aspose.PDF – Hướng dẫn toàn diện
url: /vi/net/programming-with-images/crop-image-in-pdf-with-aspose-pdf-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cắt ảnh trong PDF bằng Aspose.PDF – Hướng dẫn đầy đủ

Bạn đã bao giờ tự hỏi làm thế nào để **crop image in PDF** mà không cần mở một trình chỉnh sửa đồ họa không? Bạn không phải là người duy nhất. Trong nhiều báo cáo, hoá đơn, hoặc sách điện tử, bạn chỉ cần một phần của hình ảnh—có thể là góc logo hoặc một đoạn biểu đồ—và bạn muốn nó trực tiếp trong PDF.  

Hướng dẫn này sẽ chỉ cho bạn cách thực hiện: chúng ta sẽ **create PDF with image**, **add image to PDF**, và sau đó **crop image in PDF** bằng thư viện Aspose.PDF cho C#. Khi kết thúc, bạn cũng sẽ biết cách **save PDF with image** để có thể gửi file cho bất kỳ ai.

---

## Những gì bạn cần

- .NET 6.0 hoặc mới hơn (mã cũng chạy được với .NET Framework 4.6+)  
- Một bản sao có giấy phép hoặc bản dùng thử của **Aspose.PDF for .NET** (cài đặt qua NuGet `Install-Package Aspose.PDF`)  
- Một tệp ảnh (JPEG/PNG) trên đĩa – chúng tôi sẽ gọi nó là `image.jpg`  
- Bất kỳ IDE nào bạn thích (Visual Studio, Rider, VS Code)

Đó là tất cả. Không cần dịch vụ bổ sung, không cần công cụ bên ngoài.

---

## Bước 1: Thiết lập dự án và các import

Đầu tiên, tạo một ứng dụng console và nhập các namespace chúng ta sẽ sử dụng. Các câu lệnh `using` giúp mã gọn gàng và làm cho các bước tiếp theo dễ đọc hơn.

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;   // for text fragments if you want captions later
```

> **Mẹo chuyên nghiệp:** Nếu bạn đang dùng Visual Studio, nhấp chuột phải vào dự án → *Manage NuGet Packages* → tìm “Aspose.PDF” và cài đặt. Thư viện này xử lý cả việc đặt ảnh và cắt ảnh nội bộ, vì vậy bạn sẽ không cần bất kỳ thư viện ảnh bên thứ ba nào.

---

## Bước 2: Tạo PDF với ảnh

Bây giờ chúng ta thực sự **create pdf with image**. Đoạn mã dưới tạo một `Document` mới, thêm một trang trống, và chuẩn bị một luồng ảnh.

```csharp
// Initialize a new PDF document
Document pdf = new Document();

// Add a blank page – think of it as a clean canvas
Page page = pdf.Pages.Add();

// Open the source image file
using (FileStream imgStream = new FileStream("YOUR_DIRECTORY/image.jpg", FileMode.Open))
{
    // We'll place the whole image first; cropping comes next
    // Define where the image should sit on the page (in points; 1 point = 1/72 inch)
    Rectangle placement = new Rectangle(0, 0, 600, 800); // width=600pt, height=800pt

    // Add the image without cropping yet – just to see the full picture
    page.AddImage(imgStream, placement);
}
```

Chạy đoạn mã này sẽ cho bạn một PDF với toàn bộ hình ảnh được kéo dài tới kích thước bạn chỉ định. Đây là một kiểm tra nhanh tốt trước khi bạn bắt đầu cắt.

---

## Bước 3: Cách thêm ảnh vào PDF (và chuẩn bị cho việc cắt)

Nếu bạn đã biết chính xác vùng muốn cắt, bạn có thể bỏ qua bước tạo ảnh toàn kích thước và chuyển thẳng tới phần **how to add image to pdf**. Phương thức `AddImage` nhận ba tham số:

1. **Image stream** – các byte thô của ảnh của bạn.  
2. **Placement rectangle** – vị trí trên trang mà ảnh sẽ hiển thị.  
3. **Crop rectangle** – phần của ảnh mà bạn thực sự muốn hiển thị.

Dưới đây là phiên bản ngắn gọn thực hiện cả việc đặt **và** cắt trong một lời gọi.

```csharp
using (FileStream imgStream = new FileStream("YOUR_DIRECTORY/image.jpg", FileMode.Open))
{
    // Full‑size placement rectangle (you can adjust X/Y if you need margins)
    Rectangle placement = new Rectangle(0, 0, 600, 800);

    // Crop area: upper‑left quarter of the original image
    Rectangle crop = new Rectangle(0, 0, placement.Width / 2, placement.Height / 2);

    // This single line both adds the image and crops it
    page.AddImage(imgStream, placement, crop);
}
```

> **Tại sao cách này hoạt động:** Aspose.PDF nội bộ ánh xạ rectangle cắt tới kích thước pixel của ảnh, sau đó chỉ render phần đó trong khu vực `placement`. Không cần xử lý bitmap bổ sung, giúp giữ kích thước PDF nhỏ.

---

## Bước 4: Cách cắt ảnh PDF – Tùy chọn nâng cao

Đôi khi việc cắt một phần tư không đủ. Có thể bạn cần một rectangle tùy chỉnh hoặc muốn giữ tỷ lệ khung hình của ảnh. Đây là cách tiếp cận linh hoạt hơn:

```csharp
using (FileStream imgStream = new FileStream("YOUR_DIRECTORY/image.jpg", FileMode.Open))
{
    // Placement on the page (centered, 300pt wide, keep original height)
    Rectangle placement = new Rectangle(150, 400, 450, 1200);

    // Suppose you want a 200 × 150 pixel region starting at (50, 30) in the source image
    // First, convert pixel coordinates to points (assuming 72 DPI)
    float dpi = 72f;
    float left   = 50  / dpi * 72; // = 50 points
    float bottom = 30  / dpi * 72; // = 30 points
    float width  = 200 / dpi * 72; // = 200 points
    float height = 150 / dpi * 72; // = 150 points

    Rectangle crop = new Rectangle(left, bottom, left + width, bottom + height);

    page.AddImage(imgStream, placement, crop);
}
```

**Xử lý các trường hợp đặc biệt:**  
- **Null streams** – luôn bao bọc `FileStream` trong một khối `using`, như ví dụ, để tránh rò rỉ.  
- **Large images** – nếu ảnh nguồn quá lớn, hãy cân nhắc thu nhỏ rectangle `placement`; Aspose sẽ tự động giảm mẫu.  
- **Transparent PNGs** – thư viện tôn trọng kênh alpha, vì vậy vùng đã cắt sẽ giữ độ trong suốt.

---

## Bước 5: Lưu PDF với ảnh (và xác minh)

Cuối cùng, chúng ta **save pdf with image**. Phương thức `Save` ghi tài liệu ra đĩa. Bạn cũng có thể stream nó trở lại cho client web nếu đang xây dựng một API.

```csharp
// Save the final PDF to the output folder
pdf.Save("YOUR_DIRECTORY/output.pdf");

// Optional: Open the file automatically (only works on Windows)
System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo
{
    FileName = "YOUR_DIRECTORY/output.pdf",
    UseShellExecute = true
});
```

Khi bạn mở `output.pdf`, bạn sẽ chỉ thấy phần đã cắt của `image.jpg` được đặt chính xác ở vị trí bạn định nghĩa. Nếu ảnh bị kéo dài, hãy điều chỉnh chiều rộng/chiều cao của rectangle `placement` để phù hợp với tỷ lệ khung hình của rectangle cắt.

---

## Câu hỏi thường gặp & Lưu ý

| Question | Answer |
|----------|--------|
| **Tôi có thể cắt nhiều ảnh trên cùng một trang không?** | Chắc chắn. Gọi `page.AddImage` cho mỗi ảnh với rectangle placement và crop riêng. |
| **Nếu ảnh của tôi ở định dạng khác (ví dụ: BMP) thì sao?** | Aspose.PDF hỗ trợ JPEG, PNG, BMP, GIF và TIFF ngay lập tức. Chỉ cần thay đổi phần mở rộng tệp. |
| **Tôi có cần giấy phép cho việc sử dụng trong môi trường production không?** | Bản dùng thử hoạt động tối đa 5 trang. Đối với triển khai thực tế, mua giấy phép để loại bỏ watermark. |
| **Làm sao để xoay ảnh đã cắt?** | Sau khi thêm ảnh, lấy đối tượng `Image` và đặt thuộc tính `Rotate` (`Rotate = RotationAngle.Rotate90`). |
| **Có cách nào cắt bằng phần trăm thay vì điểm tuyệt đối không?** | Có—tính kích thước rectangle dựa trên `image.Width * 0.25` etc., sau đó chuyển sang điểm như trong Bước 4. |

---

## Ví dụ hoàn chỉnh (Sẵn sàng sao chép‑dán)

```csharp
using System;
using System.IO;
using Aspose.Pdf;

namespace CropImageInPdfDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create a new PDF document and add a blank page
            Document pdf = new Document();
            Page page = pdf.Pages.Add();

            // 2️⃣ Open the image that will be placed on the page
            using (FileStream imgStream = new FileStream("YOUR_DIRECTORY/image.jpg", FileMode.Open))
            {
                // 3️⃣ Define where the image will sit on the page (points)
                Rectangle placement = new Rectangle(0, 0, 600, 800);

                // 4️⃣ Define the crop area – upper‑left quarter of the image
                Rectangle crop = new Rectangle(0, 0, placement.Width / 2, placement.Height / 2);

                // 5️⃣ Add the image using both placement and crop rectangles
                page.AddImage(imgStream, placement, crop);
            }

            // (Optional) Save the PDF to verify the result
            pdf.Save("YOUR_DIRECTORY/output.pdf");

            Console.WriteLine("PDF created and image cropped successfully!");
        }
    }
}
```

Chạy chương trình, mở `output.pdf`, và bạn sẽ chỉ thấy phần tư trên‑trái của `image.jpg` được render ở góc trên‑trái của trang. Thay đổi giá trị rectangle `crop` để thử nghiệm các phần cắt khác nhau.

---

## Kết luận

Chúng tôi đã hướng dẫn toàn bộ quy trình **crop image in pdf** bằng Aspose.PDF cho C#. Bắt đầu từ một tài liệu mới, chúng ta **create pdf with image**, minh họa **how to add image to pdf**, áp dụng một rectangle **how to crop image pdf** tùy chỉnh, và cuối cùng **save pdf with image**.  

Bây giờ bạn có thể nhúng các hình ảnh đã cắt chính xác vào bất kỳ PDF nào bạn tạo—hoàn hảo cho hoá đơn, brochure marketing, hoặc báo cáo tự động. Tiếp theo, hãy cân nhắc thêm chú thích văn bản (`TextFragment`) hoặc vẽ các hình dạng quanh ảnh đã cắt để làm nổi bật hơn.  

Có thêm các kịch bản bạn muốn khám phá? Để lại bình luận, và chúc bạn lập trình vui vẻ!

## Bạn nên học gì tiếp theo?

Các hướng dẫn sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật đã trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh với giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Cách đặt kích thước ảnh trong PDF bằng Aspose.PDF cho .NET](/pdf/english/net/images-graphics/set-image-size-pdf-aspose-dotnet/)
- [Cách thêm Image Stamp vào PDF bằng Aspose.PDF cho .NET&#58; Hướng dẫn toàn diện](/pdf/english/net/images-graphics/add-image-stamp-pdf-aspose-dotnet/)
- [Cách trích xuất thông tin ảnh từ PDF bằng Aspose.PDF cho .NET](/pdf/english/net/images-graphics/extract-image-info-pdf-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}