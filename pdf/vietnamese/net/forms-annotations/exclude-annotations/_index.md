---
title: So sánh PDF Side‑by‑Side loại trừ chú thích với Aspose.Pdf for .NET
weight: 101
limit:
description: Hướng dẫn từng bước để so sánh PDF và loại trừ các vùng chú thích bằng Aspose.Pdf for .NET.
keywords: [pdf comparison, exclude annotations, Aspose.Pdf for .NET, side by side comparison, annotation bounding boxes, diff pdf]
url: /net/forms-annotations/exclude-annotations/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Hướng dẫn từng bước để so sánh PDF và loại trừ các vùng chú thích bằng
    Aspose.Pdf for .NET.
  headline: So sánh PDF Side‑by‑Side loại trừ chú thích với Aspose.Pdf for .NET
  type: TechArticle
- description: Hướng dẫn từng bước để so sánh PDF và loại trừ các vùng chú thích bằng
    Aspose.Pdf for .NET.
  name: So sánh PDF Side‑by‑Side loại trừ chú thích với Aspose.Pdf for .NET
  steps:
  - name: Xác định đường dẫn tệp cho PDF chính, PDF phụ và PDF diff đầu ra.
    text: Xác định đường dẫn tệp cho PDF chính, PDF phụ và PDF diff đầu ra.
  - name: Kiểm tra xem cả hai tệp PDF đầu vào có tồn tại hay không và dừng lại với
      thông báo lỗi nếu bất kỳ tệp nào bị thiếu.
    text: Kiểm tra xem cả hai tệp PDF đầu vào có tồn tại hay không và dừng lại với
      thông báo lỗi nếu bất kỳ tệp nào bị thiếu.
  - name: Mở hai tệp PDF dưới dạng các đối tượng Document (pdfA và pdfB) trong một
      khối using để chúng được giải phóng tự động.
    text: Mở hai tệp PDF dưới dạng các đối tượng Document (pdfA và pdfB) trong một
      khối using để chúng được giải phóng tự động.
  - name: Thu thập các hình chữ nhật bao quanh của mọi chú thích trong pdfA và lưu
      chúng vào ignoredRectsA.
    text: Thu thập các hình chữ nhật bao quanh của mọi chú thích trong pdfA và lưu
      chúng vào ignoredRectsA.
  - name: Thu thập các hình chữ nhật bao quanh của mọi chú thích trong pdfB và lưu
      chúng vào ignoredRectsB.
    text: Thu thập các hình chữ nhật bao quanh của mọi chú thích trong pdfB và lưu
      chúng vào ignoredRectsB.
  - name: Tạo một đối tượng SideBySideComparisonOptions và gán các hình chữ nhật chú
      thích đã thu thập trước đó cho ExcludeAreas1 và ExcludeAreas2 để các vùng đó
      bị bỏ qua trong quá trình so sánh.
    text: Tạo một đối tượng SideBySideComparisonOptions và gán các hình chữ nhật chú
      thích đã thu thập trước đó cho ExcludeAreas1 và ExcludeAreas2 để các vùng đó
      bị bỏ qua trong quá trình so sánh.
  - name: Thực hiện so sánh PDF side‑by‑side bằng cách sử dụng hai đối tượng Document
      và các tùy chọn đã cấu hình, ghi kết quả vào outputPdf.
    text: Thực hiện so sánh PDF side‑by‑side bằng cách sử dụng hai đối tượng Document
      và các tùy chọn đã cấu hình, ghi kết quả vào outputPdf.
  - name: Giải phóng các đối tượng Document và thoát khỏi khối using.
    text: Giải phóng các đối tượng Document và thoát khỏi khối using.
  - name: In ra thông báo xác nhận cho biết việc so sánh đã hoàn tất và PDF diff đã
      được lưu ở đâu.
    text: In ra thông báo xác nhận cho biết việc so sánh đã hoàn tất và PDF diff đã
      được lưu ở đâu.
  type: HowTo
- questions:
  - answer: Có. Mã chỉ không thêm bất kỳ hình chữ nhật nào vào danh sách `ignoredRects`
      tương ứng, vì vậy `ExcludeAreas1`/`ExcludeAreas2` nhận một mảng rỗng và bộ so
      sánh sẽ xử lý toàn bộ trang.
    question: Điều gì sẽ xảy ra nếu một trang PDF không có chú thích – so sánh vẫn
      hoạt động không?
  - answer: Đặt `ExcludeAreas1` (hoặc `ExcludeAreas2`) thành các hình chữ nhật đã
      thu thập và để thuộc tính còn lại là một mảng rỗng; bộ so sánh sẽ bỏ qua các
      vùng chỉ trong tài liệu được chỉ định.
    question: Tôi có thể chỉ loại trừ chú thích từ một tài liệu trong khi giữ lại
      chú thích của tài liệu còn lại trong diff không?
  - answer: Các hình chữ nhật chồng lên nhau được bộ so sánh hợp nhất nội bộ, vì vậy
      các giới hạn chú thích chồng chéo được loại trừ một cách an toàn mà không bị
      đếm lại.
    question: Các hình chữ nhật chú thích chồng lên nhau có gây ra vấn đề nào với
      `ExcludeAreas` không?
  - answer: Có, đặt `compareOpts.ExcludeTables = true;` – cờ này hoạt động cùng với
      `ExcludeAreas1`/`ExcludeAreas2` để cũng bỏ qua các vùng bảng.
    question: Có cách nào để loại trừ bảng bên cạnh chú thích bằng cùng một đối tượng
      tùy chọn không?
  - answer: Mã kiểm tra `if (a != null && a.Rect != null)` trước khi thêm vào danh
      sách, vì vậy các hình chữ nhật null chỉ bị bỏ qua và không có ngoại lệ nào được
      ném.
    question: Nếu thuộc tính `Rect` của một chú thích là null – mã sẽ ném ngoại lệ
      không?
  type: FAQPage
images:
- /net/forms-annotations/exclude-annotations/og-image.png
og_title: So sánh PDF không có chú thích
og_description: Thực hiện một PDF diff side‑by‑side bỏ qua tất cả các dấu chú thích.
og_image_alt: Hướng dẫn cho thấy một so sánh PDF side‑by‑side loại trừ các vùng chú thích bằng Aspose.Pdf for .NET
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# So sánh PDF Side‑by‑Side loại trừ chú thích với Aspose.Pdf
Hướng dẫn này cho thấy cách so sánh hai tệp PDF bằng Aspose.Pdf for .NET trong khi bỏ qua bất kỳ nội dung chú thích nào. Nó trích xuất các hộp giới hạn của tất cả các chú thích từ mỗi tài liệu, đưa các vùng đó vào SideBySideComparisonOptions, và sau đó thực hiện so sánh side‑by‑side. Kết quả là một PDF diff chỉ làm nổi bật các thay đổi không phải chú thích.

---

{{< tutorial-widget sourcePath="pdf/net/forms-annotations/exclude-annotations" >}}


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

**Q: Điều gì sẽ xảy ra nếu một trang PDF không có chú thích – so sánh vẫn hoạt động không?**  
A: Có. Mã chỉ không thêm bất kỳ hình chữ nhật nào vào danh sách `ignoredRects` tương ứng, vì vậy `ExcludeAreas1`/`ExcludeAreas2` nhận một mảng rỗng và bộ so sánh sẽ xử lý toàn bộ trang.

**Q: Tôi có thể chỉ loại trừ chú thích từ một tài liệu trong khi giữ lại chú thích của tài liệu còn lại trong diff không?**  
A: Đặt `ExcludeAreas1` (hoặc `ExcludeAreas2`) thành các hình chữ nhật đã thu thập và để thuộc tính còn lại là một mảng rỗng; bộ so sánh sẽ bỏ qua các vùng chỉ trong tài liệu được chỉ định.

**Q: Các hình chữ nhật chú thích chồng lên nhau có gây ra vấn đề nào với `ExcludeAreas` không?**  
A: Các hình chữ nhật chồng lên nhau được bộ so sánh hợp nhất nội bộ, vì vậy các giới hạn chú thích chồng chéo được loại trừ một cách an toàn mà không bị đếm lại.

**Q: Có cách nào để loại trừ bảng bên cạnh chú thích bằng cùng một đối tượng tùy chọn không?**  
A: Có, đặt `compareOpts.ExcludeTables = true;` – cờ này hoạt động cùng với `ExcludeAreas1`/`ExcludeAreas2` để cũng bỏ qua các vùng bảng.

**Q: Nếu thuộc tính `Rect` của một chú thích là null – mã sẽ ném ngoại lệ không?**  
A: Mã kiểm tra `if (a != null && a.Rect != null)` trước khi thêm vào danh sách, vì vậy các hình chữ nhật null chỉ bị bỏ qua và không có ngoại lệ nào được ném.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}