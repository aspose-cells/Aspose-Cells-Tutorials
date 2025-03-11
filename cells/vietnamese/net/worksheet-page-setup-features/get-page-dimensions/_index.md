---
title: Lấy kích thước trang của bảng tính
linktitle: Lấy kích thước trang của bảng tính
second_title: API xử lý Excel Aspose.Cells .NET
description: Tìm hiểu cách lấy kích thước trang trong bảng tính Excel bằng Aspose.Cells cho .NET. Hướng dẫn từng bước để tùy chỉnh kích thước giấy A2, A3, A4 và Letter.
weight: 13
url: /vi/net/worksheet-page-setup-features/get-page-dimensions/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Lấy kích thước trang của bảng tính

## Giới thiệu
Nếu bạn đang làm việc với các tệp Excel theo chương trình bằng Aspose.Cells for .NET, có thể có lúc bạn cần truy cập và thiết lập kích thước trang của một bảng tính. Biết được kích thước có thể giúp ích cho việc bố trí, in ấn và tùy chỉnh các trang tính Excel cho các mục đích cụ thể. Trong bài viết này, chúng ta sẽ khám phá cách truy xuất và hiển thị nhiều kích thước trang khác nhau trong Excel bằng Aspose.Cells for .NET. Chúng ta sẽ thực hiện hướng dẫn từng bước để đảm bảo bạn có đủ thông tin chi tiết để bắt đầu một cách tự tin.
## Điều kiện tiên quyết
Trước khi bắt đầu, hãy đảm bảo rằng bạn có mọi thứ cần thiết để làm theo hướng dẫn này.
1.  Aspose.Cells cho .NET: Đảm bảo bạn đã cài đặt Aspose.Cells cho .NET. Bạn có thể[tải xuống thư viện ở đây](https://releases.aspose.com/cells/net/) hoặc cài đặt nó thông qua NuGet trong dự án .NET của bạn.
2. Môi trường .NET: Môi trường phát triển .NET tương thích (ví dụ: Visual Studio).
3.  Thiết lập giấy phép: Để có đầy đủ chức năng của Aspose.Cells, hãy áp dụng giấy phép. Bạn có thể[yêu cầu giấy phép tạm thời miễn phí](https://purchase.aspose.com/temporary-license/) cho mục đích đánh giá.
Bắt đầu với phiên bản dùng thử miễn phí của Aspose.Cells nếu đây là lần đầu tiên bạn sử dụng.
## Nhập gói
Trước khi tìm hiểu mã, bạn sẽ cần nhập không gian tên Aspose.Cells vào dự án của mình để truy cập tất cả các lớp và phương thức cần thiết.
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Hãy chia nhỏ quy trình thành các bước dễ dàng. Ở đây, chúng ta sẽ truy cập các kích thước giấy khác nhau, áp dụng chúng vào bảng tính và in kích thước cho từng kích thước.
## Bước 1: Tạo một phiên bản Workbook
 Bước đầu tiên là tạo một phiên bản của`Workbook` lớp. Đối tượng này sẽ hoạt động như sổ làm việc chính chứa các bảng tính mà chúng ta có thể thao tác.
```csharp
Workbook book = new Workbook();
```
 Nghĩ về`Workbook` là nơi chứa chính cho tệp Excel của bạn. Chúng tôi cần nó để truy cập và kiểm soát từng bảng tính riêng lẻ.
## Bước 2: Truy cập vào Bảng tính đầu tiên
 Tiếp theo, chúng ta hãy truy cập vào trang tính đầu tiên trong sổ làm việc. Theo mặc định, một sổ làm việc mới đi kèm với một trang tính, vì vậy chúng ta có thể tham chiếu trực tiếp đến nó bằng cách sử dụng chỉ mục`0`.
```csharp
Worksheet sheet = book.Worksheets[0];
```
 Các`Worksheets` bộ sưu tập trong`Workbook` cho phép chúng ta truy cập từng trang tính theo chỉ mục. Ở đây, chúng ta lấy trang tính đầu tiên để bắt đầu thiết lập kích thước trang.
## Bước 3: Đặt Kích thước giấy thành A2 và Kích thước hiển thị
Bây giờ chúng ta đã có quyền truy cập vào bảng tính của mình, hãy đặt kích thước giấy của nó thành A2. Việc đặt kích thước giấy rất hữu ích để định dạng trang trước khi in hoặc xuất trang. Sau khi đặt kích thước giấy, chúng ta sẽ in kích thước trang theo inch.
```csharp
sheet.PageSetup.PaperSize = PaperSizeType.PaperA2;
Console.WriteLine("PaperA2: " + sheet.PageSetup.PaperWidth + "x" + sheet.PageSetup.PaperHeight);
```
 Ở đây, chúng ta thay đổi`PaperSize` tài sản để`PaperA2` . Sau khi thiết lập kích thước,`PageSetup.PaperWidth` Và`PageSetup.PaperHeight` lấy chiều rộng và chiều cao của trang tính bằng inch. Điều này cung cấp cho chúng ta cái nhìn tổng quan nhanh về kích thước trang.
## Bước 4: Đặt Kích thước giấy thành A3 và Kích thước hiển thị
Thực hiện theo các bước tương tự như trên, hãy điều chỉnh kích thước trang thành khổ A3. Thay đổi này hữu ích cho các bản in lớn hơn một chút hoặc để đưa nhiều nội dung hơn vào một trang.
```csharp
sheet.PageSetup.PaperSize = PaperSizeType.PaperA3;
Console.WriteLine("PaperA3: " + sheet.PageSetup.PaperWidth + "x" + sheet.PageSetup.PaperHeight);
```
Kích thước A3 gấp đôi kích thước A4, là lựa chọn tốt cho các bảng lớn hoặc biểu đồ chi tiết. Thay đổi kích thước giấy giúp điều chỉnh bố cục bảng tính cho phù hợp.
## Bước 5: Đặt Kích thước giấy thành A4 và Kích thước hiển thị
Bây giờ, hãy đặt kích thước giấy thành A4. Đây là kích thước trang được sử dụng phổ biến nhất để in tài liệu. Chúng tôi sẽ hiển thị kích thước được cập nhật sau.
```csharp
sheet.PageSetup.PaperSize = PaperSizeType.PaperA4;
Console.WriteLine("PaperA4: " + sheet.PageSetup.PaperWidth + "x" + sheet.PageSetup.PaperHeight);
```
Nếu mục tiêu của bạn là định dạng tài liệu chuẩn, A4 thường là kích thước phù hợp nhất. Biết kích thước có thể giúp điều chỉnh bố cục nội dung để tránh sự cố in ấn.
## Bước 6: Đặt Kích thước giấy thành Letter và Kích thước hiển thị
Cuối cùng, chúng ta sẽ thiết lập kích thước giấy theo định dạng Letter, thường được sử dụng ở Bắc Mỹ. Hãy in kích thước lần cuối.
```csharp
sheet.PageSetup.PaperSize = PaperSizeType.PaperLetter;
Console.WriteLine("PaperLetter: " + sheet.PageSetup.PaperWidth + "x" + sheet.PageSetup.PaperHeight);
```
Kích thước Letter được sử dụng rộng rãi cho các tài liệu ở Bắc Mỹ, do đó, việc thiết lập kích thước này sẽ hữu ích khi cộng tác với các nhóm hoặc khách hàng tại đó.
## Phần kết luận
Trong hướng dẫn này, chúng tôi đã hướng dẫn cách thiết lập và truy xuất kích thước trang cho các kích thước giấy khác nhau bằng Aspose.Cells cho .NET. Bằng cách cấu hình các kích thước trang như A2, A3, A4 và Letter, bạn có thể định dạng các bảng tính Excel để phù hợp với nhu cầu in ấn và bố cục cụ thể. Việc kiểm soát kích thước trang này đặc biệt có giá trị đối với báo cáo và trình bày chuyên nghiệp, vì nó đảm bảo nội dung của bạn vừa vặn hoàn hảo trên mỗi kích thước trang.
## Câu hỏi thường gặp
### Làm thế nào để tôi có thể thay đổi hướng của trang trong Aspose.Cells?  
 Bạn có thể thay đổi hướng bằng cách sử dụng`PageSetup.Orientation` thuộc tính, đặt nó thành`PageOrientationType.Portrait` hoặc`PageOrientationType.Landscape`.
### Tôi có thể thiết lập kích thước trang tùy chỉnh trong Aspose.Cells không?  
 Có, bạn có thể thiết lập kích thước trang tùy chỉnh bằng cách điều chỉnh lề và tùy chọn tỷ lệ bên dưới`PageSetup` để kiểm soát tốt hơn.
### Kích thước giấy mặc định trong Aspose.Cells là bao nhiêu?  
Kích thước giấy mặc định thường là A4. Tuy nhiên, kích thước này có thể phụ thuộc vào cài đặt khu vực và có thể điều chỉnh khi cần.
### Có thể xem trước bố cục trang trong Aspose.Cells không?  
Mặc dù Aspose.Cells không cung cấp bản xem trước đồ họa, bạn vẫn có thể thiết lập bố cục theo chương trình và sử dụng bản xem trước khi in trong Excel.
### Làm thế nào để cài đặt Aspose.Cells cho .NET?  
 Bạn có thể cài đặt Aspose.Cells bằng NuGet Package Manager trong Visual Studio hoặc tải xuống DLL từ[Trang tải xuống Aspose.Cells](https://releases.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
