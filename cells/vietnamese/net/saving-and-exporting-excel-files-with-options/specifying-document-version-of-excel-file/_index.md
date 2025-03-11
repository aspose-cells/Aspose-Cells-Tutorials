---
title: Chỉ định phiên bản tài liệu của tệp Excel theo chương trình trong .NET
linktitle: Chỉ định phiên bản tài liệu của tệp Excel theo chương trình trong .NET
second_title: API xử lý Excel Aspose.Cells .NET
description: Tìm hiểu cách chỉ định các thuộc tính tài liệu như phiên bản, tác giả và tiêu đề trong tệp Excel theo chương trình sử dụng Aspose.Cells cho .NET với hướng dẫn từng bước.
weight: 12
url: /vi/net/saving-and-exporting-excel-files-with-options/specifying-document-version-of-excel-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Chỉ định phiên bản tài liệu của tệp Excel theo chương trình trong .NET

## Giới thiệu
Aspose.Cells for .NET là một thư viện mạnh mẽ cho phép các nhà phát triển dễ dàng thao tác theo chương trình các tệp Excel. Cho dù bạn muốn tạo tệp Excel từ đầu hay sửa đổi các tệp hiện có, Aspose.Cells đều cung cấp API toàn diện để đạt được mục tiêu của bạn. Một trong những tính năng đó là chỉ định các thuộc tính tài liệu như phiên bản, tác giả hoặc tiêu đề. Hướng dẫn này sẽ hướng dẫn bạn cách chỉ định phiên bản tài liệu của tệp Excel theo chương trình bằng Aspose.Cells for .NET.
## Điều kiện tiên quyết
Trước khi đi sâu vào chi tiết, hãy đảm bảo rằng bạn có mọi thứ cần thiết để làm theo hướng dẫn này:
1. Aspose.Cells cho .NET: Bạn có thể tải xuống phiên bản mới nhất[đây](https://releases.aspose.com/cells/net/) . Nếu bạn chưa mua giấy phép, bạn có thể lựa chọn[giấy phép tạm thời](https://purchase.aspose.com/temporary-license/) để khám phá các tính năng.
2. Môi trường phát triển .NET: Bạn có thể sử dụng Visual Studio hoặc bất kỳ IDE nào tương thích với .NET.
3. Kiến thức cơ bản về C#: Hiểu biết về lập trình C# sẽ giúp bạn dễ dàng theo dõi hơn.
## Nhập gói
Trước khi bạn có thể bắt đầu mã hóa, bạn cần nhập các không gian tên cần thiết từ thư viện Aspose.Cells. Điều này sẽ cho phép bạn truy cập vào các lớp và phương thức cần thiết để thao tác tệp Excel.
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Hai không gian tên này sẽ rất cần thiết để tương tác với sổ làm việc và các thuộc tính tài liệu tích hợp của nó.
Bây giờ, chúng ta hãy phân tích quy trình chỉ định thuộc tính tài liệu trong tệp Excel, bao gồm phiên bản, tiêu đề và tác giả.
## Bước 1: Khởi tạo đối tượng Workbook
 Bước đầu tiên là tạo một phiên bản mới của`Workbook` đối tượng. Đối tượng này đại diện cho toàn bộ tệp Excel mà bạn sẽ làm việc.
```csharp
Workbook wb = new Workbook();
```
 Các`Workbook`lớp cung cấp một biểu diễn của một tệp Excel. Bằng cách khởi tạo nó, chúng ta tạo một sổ làm việc Excel trống mà chúng ta có thể thao tác.
## Bước 2: Truy cập Thuộc tính Tài liệu Tích hợp
 Aspose.Cells cung cấp các thuộc tính tài liệu tích hợp, bao gồm các trường như tiêu đề, tác giả và phiên bản tài liệu. Bạn có thể truy cập các thuộc tính này thông qua`BuiltInDocumentProperties`bộ sưu tập.
```csharp
Aspose.Cells.Properties.BuiltInDocumentPropertyCollection bdpc = wb.BuiltInDocumentProperties;
```
 Các`BuiltInDocumentPropertyCollection` Lớp này cung cấp quyền truy cập vào bộ sưu tập các thuộc tính tích hợp của tài liệu, chẳng hạn như tiêu đề, tác giả và các siêu dữ liệu khác thường được liên kết với tài liệu.
## Bước 3: Đặt Tiêu đề cho Tài liệu Excel
Tiếp theo, chúng ta sẽ đặt tiêu đề cho tài liệu Excel. Siêu dữ liệu này giúp xác định và quản lý tệp sau này.
```csharp
bdpc.Title = "Aspose File Format APIs";
```
Việc đặt tiêu đề rất quan trọng đối với việc tổ chức tài liệu. Siêu dữ liệu này có thể được nhìn thấy trong thuộc tính tệp và có thể được các hệ thống bên ngoài sử dụng để lập danh mục hoặc xác định tài liệu hiệu quả hơn.
## Bước 4: Chỉ định tác giả
Tác giả của tài liệu cũng có thể được chỉ định để phản ánh người đã tạo hoặc chỉnh sửa tệp.
```csharp
bdpc.Author = "Aspose APIs Developers";
```
Bước này giúp xác định người tạo tài liệu, cung cấp siêu dữ liệu bổ sung cho mục đích quản lý tài liệu hoặc các tình huống cộng tác.
## Bước 5: Chỉ định Phiên bản Tài liệu
Một trong những thuộc tính quan trọng nhất mà chúng tôi đề cập trong hướng dẫn này là phiên bản tài liệu. Bước này cho phép bạn chỉ định phiên bản của tài liệu, điều này hữu ích khi làm việc trong môi trường yêu cầu kiểm soát phiên bản.
```csharp
bdpc.DocumentVersion = "Aspose.Cells Version - 18.3";
```
Thiết lập phiên bản tài liệu cung cấp sự rõ ràng về phiên bản nào của tài liệu hoặc thư viện được sử dụng để tạo tệp. Điều này đặc biệt quan trọng trong các môi trường cần theo dõi các bản sửa đổi tệp hoặc khả năng tương thích với các phiên bản thư viện khác nhau.
## Bước 6: Lưu tệp Excel
 Cuối cùng, bạn có thể lưu tệp Excel với tất cả các thuộc tính bạn vừa thiết lập. Aspose.Cells cho phép bạn lưu tệp ở nhiều định dạng khác nhau, nhưng đối với ví dụ này, chúng tôi sẽ sử dụng`.xlsx` định dạng.
```csharp
wb.Save("outputSpecifyDocumentVersionOfExcelFile.xlsx", SaveFormat.Xlsx);
```
 Các`Save` phương pháp được sử dụng để lưu tệp vào thư mục bạn chỉ định. Ở đây, chúng tôi lưu nó dưới dạng tệp Excel trong`.xlsx`định dạng. Nếu cần, Aspose.Cells cũng hỗ trợ các định dạng như`.xls`, `.csv` , Và`.pdf`, mang lại sự linh hoạt dựa trên nhu cầu của dự án bạn.
## Phần kết luận
Trong hướng dẫn này, chúng tôi sẽ hướng dẫn cách chỉ định thuộc tính tài liệu, đặc biệt là phiên bản tài liệu, trong tệp Excel bằng Aspose.Cells cho .NET. Aspose.Cells là một công cụ cực kỳ linh hoạt và mạnh mẽ cho phép bạn thao tác các tệp Excel theo chương trình, khiến nó trở thành một công cụ tuyệt vời cho bất kỳ nhà phát triển .NET nào làm việc với bảng tính.
## Câu hỏi thường gặp
### Tôi có thể sửa đổi các thuộc tính tích hợp khác bằng Aspose.Cells không?  
Có, bạn có thể sửa đổi các thuộc tính tích hợp khác như chủ đề, từ khóa, bình luận, v.v.
### Aspose.Cells hỗ trợ những định dạng tệp nào?  
 Aspose.Cells hỗ trợ nhiều định dạng khác nhau bao gồm`.xls`, `.xlsx`, `.csv`, `.pdf`và nhiều hơn nữa.
### Tôi có cần giấy phép để sử dụng Aspose.Cells cho .NET không?  
 Bạn có thể khám phá Aspose.Cells bằng[dùng thử miễn phí](https://releases.aspose.com/) hoặc nộp đơn xin[giấy phép tạm thời](https://purchase.aspose.com/temporary-license/) để thử nghiệm mở rộng.
### Tôi có thể sử dụng Aspose.Cells trong ứng dụng web không?  
Có, Aspose.Cells có thể được sử dụng trong cả ứng dụng máy tính để bàn và web. Nó rất linh hoạt và tích hợp tốt với các khuôn khổ web .NET.
### Tôi có thể nhận hỗ trợ cho Aspose.Cells ở đâu?  
 Bạn có thể tiếp cận cộng đồng và hỗ trợ thông qua[Diễn đàn hỗ trợ Aspose.Cells](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
