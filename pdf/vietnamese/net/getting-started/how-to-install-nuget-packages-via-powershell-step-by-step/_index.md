---
category: general
date: 2026-02-20
description: Học cách cài đặt các gói NuGet bằng PowerShell, chạy PowerShell với quyền
  admin, liệt kê các gói đã cài và xác minh gói đã cài trong vài phút.
draft: false
keywords:
- how to install nuget
- run powershell as admin
- list installed packages
- how to verify package
- verify installed package
language: vi
og_description: cách cài đặt các gói NuGet bằng PowerShell, chạy PowerShell với quyền
  quản trị, liệt kê các gói đã cài và xác minh gói đã cài—hướng dẫn chi tiết.
og_title: cách cài đặt các gói NuGet qua PowerShell – hướng dẫn nhanh
tags:
- PowerShell
- NuGet
- Package Management
title: Cách cài đặt các gói NuGet qua PowerShell – từng bước
url: /vi/net/getting-started/how-to-install-nuget-packages-via-powershell-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# cách cài đặt các gói nuget qua PowerShell – từng bước

Bạn có bao giờ tự hỏi **cách cài đặt nuget** mà không mở Visual Studio không? Bạn không phải là người duy nhất. Trong nhiều pipeline CI hoặc trên các máy mới, cách nhanh nhất là vào PowerShell—tốt nhất là *run powershell as admin*—và để trình quản lý gói thực hiện công việc của nó.

Trong tutorial này, chúng ta sẽ đi qua toàn bộ quy trình: mở console phù hợp, tải xuống một phiên bản cụ thể của thư viện, và cuối cùng xác nhận rằng gói đã thực sự được cài đặt trên hệ thống của bạn. Khi kết thúc, bạn sẽ có thể **list installed packages**, biết **how to verify package** integrity, và tự tin rằng bước **verify installed package** đã thành công mỗi lần.

## Những gì bạn sẽ học

- Cách khởi chạy PowerShell với quyền thích hợp.  
- Cú pháp lệnh `Install-Package` chính xác cho NuGet.  
- Các cách để **list installed packages** và xác nhận số phiên bản.  
- Các bẫy thường gặp (thiếu quyền admin, không khớp phiên bản) và cách tránh chúng.  

Không cần kinh nghiệm trước với NuGet, chỉ cần một máy Windows hoạt động và một chút tò mò.

---

## Cách cài đặt các gói NuGet bằng PowerShell

> **Mẹo chuyên nghiệp:** Nếu bạn thường xuyên thêm cùng một gói, hãy cân nhắc đưa chúng vào một file script và chạy nó với `-File`. Điều này giúp bạn tránh việc gõ lại cùng một dòng nhiều lần.

### Bước 1: Mở PowerShell với quyền cần thiết

Điều đầu tiên bạn cần làm là **run powershell as admin**. Nếu không có quyền nâng cao, cmdlet `Install-Package` có thể thất bại im lặng hoặc yêu cầu xác nhận mà bạn không muốn xử lý.

1. Nhấn nút Start.  
2. Gõ **PowerShell**.  
3. Nhấp chuột phải vào *Windows PowerShell* và chọn **Run as administrator**.  

Bạn sẽ thấy thông báo UAC; nhấn **Yes**. Bây giờ bạn có một phiên làm việc có quyền sẵn sàng cho việc cài đặt gói.

> *Tại sao cần admin?*  
> NuGet ghi các tệp vào thư mục gói toàn cục (`C:\Program Files\PackageManagement\NuGet\Packages` theo mặc định). Vị trí này được bảo vệ, vì vậy chỉ một tiến trình được nâng cao mới có thể ghi vào đó.

### Bước 2: Cài đặt gói NuGet và phiên bản mong muốn

With the console open, the core command is straightforward:

```powershell
# Install the Aspose.PDF library, version 25.3
Install-Package Aspose.PDF -Version 25.3
```

- `Install-Package` là wrapper PowerShell cho client của NuGet.  
- `-Version` cố định bản dựng chính xác bạn cần, ngăn ngừa việc nâng cấp nhầm.  

Nếu bạn bỏ qua `-Version`, PowerShell sẽ tải phiên bản ổn định mới nhất—đôi khi ổn, đôi khi bạn muốn phiên bản chính xác mà bạn đã kiểm thử.

#### Điều gì xảy ra phía sau?

PowerShell liên hệ với nguồn gói đã cấu hình (mặc định `https://www.nuget.org/api/v2`) và tải về tệp `.nupkg`. Sau đó nó giải nén các DLL vào thư mục gói toàn cục và đăng ký gói với nhà cung cấp gói cục bộ. Toàn bộ quá trình thường hoàn thành trong vài giây trừ khi mạng chậm.

### Bước 3: Xác minh gói đã được cài đặt thành công

Bây giờ gói đã có trên đĩa, bạn có thể sẽ hỏi, **“Làm sao để verify the package?”** Câu trả lời nằm trong một truy vấn đơn giản:

```powershell
# List all installed NuGet packages
Get-Package -Name Aspose.PDF
```

Chạy lệnh này sẽ trả về một cái gì đó như:

```
Name        Version   Source
----        -------   ------
Aspose.PDF  25.3      nuget.org
```

Kết quả này xác nhận hai điều:

1. Gói **Aspose.PDF** có mặt.  
2. Phiên bản của nó khớp với phiên bản bạn yêu cầu, đáp ứng yêu cầu **verify installed package**.

Nếu bạn muốn xem *tất cả* gói trên máy, bỏ bộ lọc `-Name`:

```powershell
Get-Package | Where-Object {$_.ProviderName -eq 'NuGet'}
```

Cách hiển thị **list installed packages** này hữu ích cho việc kiểm toán hoặc khi bạn cần dọn dẹp các thư viện cũ.

### Bước 4: Tùy chọn – xử lý các trường hợp đặc biệt

#### a) Gói không tìm thấy hoặc không khớp phiên bản

Nếu PowerShell trả lời *“Package not found”* hoặc *“Version not available”*, hãy kiểm tra lại chính tả và số phiên bản. NuGet không phân biệt chữ hoa/thường, nhưng một khoảng trắng thừa sẽ làm lệnh bị lỗi.

```powershell
# Search the NuGet feed for available versions
Find-Package Aspose.PDF -AllVersions
```

#### b) Chạy mà không có quyền admin

Nếu bạn quên **run powershell as admin**, cmdlet sẽ ném lỗi quyền. Cách khắc phục đơn giản là đóng cửa sổ và mở lại với quyền nâng cao—không cần cài đặt lại gì.

#### c) Sử dụng nguồn tùy chỉnh

Trong môi trường doanh nghiệp, bạn có thể có một feed NuGet nội bộ:

```powershell
Install-Package MyCompany.Logging -Source https://nuget.mycompany.local/api/v2
```

Bước xác minh vẫn giống; chỉ cần nhớ thêm `-Source` khi bạn cài đặt.

---

## Bảng tham chiếu nhanh

| Hành động | Lệnh PowerShell | Lý do quan trọng |
|-----------|-----------------|-------------------|
| Mở console nâng cao | *Run PowerShell as Administrator* | Cần cho cài đặt toàn cục |
| Cài đặt một phiên bản cụ thể | `Install-Package <pkg> -Version <x.y.z>` | Đảm bảo xây dựng có thể tái tạo |
| Liệt kê một gói duy nhất | `Get-Package -Name <pkg>` | Xác nhận **how to verify package** |
| Liệt kê tất cả các gói NuGet | `Get-Package | Where-Object {$_.ProviderName -eq 'NuGet'}` | Hữu ích cho **list installed packages** |
| Tìm kiếm các phiên bản có sẵn | `Find-Package <pkg> -AllVersions` | Giúp khi không biết phiên bản |

## Kết luận

Chúng ta đã bao quát **how to install nuget** packages bằng PowerShell từ đầu đến cuối—mở console **run powershell as admin**, tải xuống một phiên bản cụ thể, và cuối cùng **list installed packages** để **verify installed package**. Với những lệnh này trong bộ công cụ của bạn, bạn có thể tự động quản lý thư viện trên bất kỳ máy Windows nào, dù bạn đang viết script cho pipeline CI hay chỉ sửa một DLL thiếu trên máy dev của mình.

Bước tiếp theo? Hãy thử thêm nhiều gói vào một script duy nhất, khám phá tham số `-Scope` để cài đặt cục bộ cho một dự án, hoặc kết hợp các lệnh này với `Invoke-Expression` để xây dựng một trình cài đặt nhẹ cho đội của bạn. Và nếu gặp vấn đề, hãy nhớ bước **how to verify package**—nhìn thấy phiên bản trong `Get-Package` thường là cách nhanh nhất để phát hiện lỗi.

Chúc bạn PowerShell vui vẻ! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}