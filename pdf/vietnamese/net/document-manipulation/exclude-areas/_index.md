---
title: So sánh PDF trong khi bỏ qua các khu vực cụ thể bằng Aspose.Pdf cho .NET
weight: 201
limit:
description: Học cách so sánh PDF cạnh nhau và bỏ qua các vùng đã chọn bằng Aspose.Pdf cho .NET.
keywords: [Aspose.Pdf for .NET, pdf comparison, exclude areas pdf, ignore regions pdf diff, side-by-side pdf comparison, pdf diff highlighting]
url: /net/document-manipulation/exclude-areas/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Học cách so sánh PDF cạnh nhau và bỏ qua các vùng đã chọn bằng Aspose.Pdf
    cho .NET.
  headline: So sánh PDF trong khi bỏ qua các khu vực cụ thể bằng Aspose.Pdf cho .NET
  type: TechArticle
- description: Học cách so sánh PDF cạnh nhau và bỏ qua các vùng đã chọn bằng Aspose.Pdf
    cho .NET.
  name: So sánh PDF trong khi bỏ qua các khu vực cụ thể bằng Aspose.Pdf cho .NET
  steps:
  - name: Xác định đường dẫn tệp cho hai PDF nguồn và PDF diff đầu ra.
    text: Xác định đường dẫn tệp cho hai PDF nguồn và PDF diff đầu ra.
  - name: Kiểm tra xem cả hai tệp PDF nguồn có tồn tại hay không và hủy bỏ với thông
      báo lỗi nếu thiếu bất kỳ tệp nào.
    text: Kiểm tra xem cả hai tệp PDF nguồn có tồn tại hay không và hủy bỏ với thông
      báo lỗi nếu thiếu bất kỳ tệp nào.
  - name: Tạo một mảng chứa vùng hình chữ nhật cần bỏ qua trong PDF đầu tiên.
    text: Tạo một mảng chứa vùng hình chữ nhật cần bỏ qua trong PDF đầu tiên.
  - name: Tạo một mảng chứa vùng hình chữ nhật cần bỏ qua trong PDF thứ hai.
    text: Tạo một mảng chứa vùng hình chữ nhật cần bỏ qua trong PDF thứ hai.
  - name: Cấu hình việc so sánh cạnh nhau, gán các mảng vùng bỏ qua vào các thuộc
      tính tương ứng.
    text: Cấu hình việc so sánh cạnh nhau, gán các mảng vùng bỏ qua vào các thuộc
      tính tương ứng.
  - name: Tải cả hai PDF và thực hiện so sánh cạnh nhau, tạo ra tệp diff tại đường
      dẫn đã chỉ định.
    text: Tải cả hai PDF và thực hiện so sánh cạnh nhau, tạo ra tệp diff tại đường
      dẫn đã chỉ định.
  - name: In ra thông báo xác nhận cho biết việc so sánh đã hoàn thành và PDF diff
      đã được lưu ở đâu.
    text: In ra thông báo xác nhận cho biết việc so sánh đã hoàn thành và PDF diff
      đã được lưu ở đâu.
  type: HowTo
- questions:
  - answer: Các tọa độ được tính bằng điểm (1/72 inch) với gốc tọa độ ở góc dưới‑trái
      của trang, vì vậy hai số đầu là X/Y góc dưới‑trái và hai số cuối là X/Y góc
      trên‑phải.
    question: Hệ tọa độ nào mà các giá trị `Rectangle` sử dụng khi định nghĩa các
      vùng bỏ qua?
  - answer: Có – cung cấp nhiều đối tượng `Aspose.Pdf.Rectangle` trong mảng `ExcludeAreas1`
      (hoặc `ExcludeAreas2`); mỗi hình chữ nhật sẽ được loại trừ độc lập trong quá
      trình so sánh.
    question: Tôi có thể bỏ qua hơn một vùng hình chữ nhật trong cùng một tài liệu
      không?
  - answer: Không. `ExcludeAreas1` áp dụng cho PDF đầu tiên và `ExcludeAreas2` cho
      PDF thứ hai, vì vậy bạn có thể chỉ định các tọa độ khác nhau cho mỗi tài liệu.
    question: Các hình chữ nhật bỏ qua có phải giống hệt nhau trong cả hai PDF không?
  - answer: Aspose.Pdf im lặng bỏ qua các hình chữ nhật nằm hoàn toàn ngoài trang;
      chúng không ảnh hưởng đến kết quả so sánh.
    question: Điều gì sẽ xảy ra nếu một hình chữ nhật được định nghĩa ngoài ranh giới
      của trang?
  - answer: Các mảng `ExcludeAreas` áp dụng cho từng trang, vì vậy bạn cần thêm cùng
      một `Rectangle` vào bộ sưu tập của mỗi trang (ví dụ, lặp qua `pdf.Pages` và
      gán mảng) trước khi gọi `SideBySidePdfComparer.Compare`.
    question: Làm thế nào tôi có thể loại trừ cùng một vùng trên mỗi trang của một
      PDF?
  type: FAQPage
images:
- /net/document-manipulation/exclude-areas/og-image.png
og_title: Bỏ qua các vùng khi so sánh PDF
og_description: Xem cách bỏ qua các khu vực đã chọn trong so sánh PDF cạnh nhau và nhận được một PDF diff sạch sẽ.
og_image_alt: Hướng dẫn hiển thị so sánh PDF cạnh nhau với các vùng hình chữ nhật bị loại trừ bằng Aspose.Pdf cho .NET
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# So sánh PDF trong khi bỏ qua các khu vực cụ thể bằng Aspose.Pdf cho .NET
Hướng dẫn này trình bày cách so sánh hai tài liệu PDF cạnh nhau bằng Aspose.Pdf cho .NET trong khi loại trừ các vùng hình chữ nhật được chỉ định khỏi quá trình phân tích. Bằng cách định nghĩa các khu vực loại trừ trong mỗi tệp, PDF diff được tạo ra chỉ làm nổi bật những thay đổi quan trọng, giúp dễ dàng tập trung vào các khác biệt liên quan.

---

{{< tutorial-widget sourcePath="pdf/net/document-manipulation/exclude-areas" >}}


{{< /blocks/products/pf/tutorial-page-section >}}

{{< blocks/products/pf/tutorial-page-section >}}
## Installation Instructions
1. Download Aspose.Pdf for .NET:
   Get the latest version from the [Aspose Downloads page](https://releases.aspose.com/pdf/net/).

2. Install via NuGet:
   - Open your Visual Studio project.
   - Navigate to the NuGet Package Manager (Tools > NuGet Package Manager > Manage NuGet Packages for Solution).
   - Search for "Aspose.Pdf" and click Install.

3. Add Namespace References:
   Add the following namespace at the top of your code file:
   ```csharp
   using Aspose.Pdf;
   using Aspose.Pdf.Devices;
   using Aspose.Pdf.Operators;
   ```

4. Apply License (Optional):
   To use the full version, [apply a license](https://purchase.aspose.com/temporary-license/) or use a [free trial](https://releases.aspose.com/).

## Also See
[Aspose.Pdf for .NET Documentation](https://docs.aspose.com/pdf/net/)
[Aspose.Pdf for .NET References](https://reference.aspose.com/pdf/net/)

## Frequently asked questions

**Q: Hệ tọa độ nào mà các giá trị `Rectangle` sử dụng khi định nghĩa các vùng bỏ qua?**  
A: Các tọa độ được tính bằng điểm (1/72 inch) với gốc tọa độ ở góc dưới‑trái của trang, vì vậy hai số đầu là X/Y góc dưới‑trái và hai số cuối là X/Y góc trên‑phải.

**Q: Tôi có thể bỏ qua hơn một vùng hình chữ nhật trong cùng một tài liệu không?**  
A: Có – cung cấp nhiều đối tượng `Aspose.Pdf.Rectangle` trong mảng `ExcludeAreas1` (hoặc `ExcludeAreas2`); mỗi hình chữ nhật sẽ được loại trừ độc lập trong quá trình so sánh.

**Q: Các hình chữ nhật bỏ qua có phải giống hệt nhau trong cả hai PDF không?**  
A: Không. `ExcludeAreas1` áp dụng cho PDF đầu tiên và `ExcludeAreas2` cho PDF thứ hai, vì vậy bạn có thể chỉ định các tọa độ khác nhau cho mỗi tài liệu.

**Q: Điều gì sẽ xảy ra nếu một hình chữ nhật được định nghĩa ngoài ranh giới của trang?**  
A: Aspose.Pdf im lặng bỏ qua các hình chữ nhật nằm hoàn toàn ngoài trang; chúng không ảnh hưởng đến kết quả so sánh.

**Q: Làm thế nào tôi có thể loại trừ cùng một vùng trên mỗi trang của một PDF?**  
A: Các mảng `ExcludeAreas` áp dụng cho từng trang, vì vậy bạn cần thêm cùng một `Rectangle` vào bộ sưu tập của mỗi trang (ví dụ, lặp qua `pdf.Pages` và gán mảng) trước khi gọi `SideBySidePdfComparer.Compare`.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}