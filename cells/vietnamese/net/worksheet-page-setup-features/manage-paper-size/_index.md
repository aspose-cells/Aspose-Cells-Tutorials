---
title: Quản lý kích thước giấy của bảng tính
linktitle: Quản lý kích thước giấy của bảng tính
second_title: API xử lý Excel Aspose.Cells .NET
description: Tìm hiểu cách thiết lập kích thước trang tùy chỉnh trong Excel bằng Aspose.Cells cho .NET với hướng dẫn từng bước dễ dàng này.
weight: 16
url: /vi/net/worksheet-page-setup-features/manage-paper-size/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Quản lý kích thước giấy của bảng tính

## Giới thiệu
Quản lý kích thước giấy trong bảng tính Excel có thể là điều cần thiết, đặc biệt là khi bạn cần in tài liệu theo kích thước cụ thể hoặc chia sẻ tệp theo bố cục được định dạng chung. Trong hướng dẫn này, chúng tôi sẽ hướng dẫn bạn sử dụng Aspose.Cells cho .NET để thiết lập kích thước giấy của bảng tính trong Excel một cách dễ dàng. Chúng tôi sẽ đề cập đến mọi thứ bạn cần, từ các điều kiện tiên quyết và các gói nhập đến phân tích đầy đủ về mã theo các bước dễ làm theo.
## Điều kiện tiên quyết
Trước khi bắt đầu, bạn cần chuẩn bị một số thứ sau:
-  Aspose.Cells cho Thư viện .NET: Hãy đảm bảo bạn đã tải xuống và cài đặt[Aspose.Cells cho .NET](https://releases.aspose.com/cells/net/). Đây là thư viện cốt lõi mà chúng ta sẽ sử dụng để thao tác các tệp Excel theo chương trình.
- Môi trường .NET: Bạn phải cài đặt .NET trên máy của mình. Bất kỳ phiên bản nào gần đây đều có thể hoạt động.
- Trình soạn thảo hoặc IDE: Trình soạn thảo mã như Visual Studio, Visual Studio Code hoặc JetBrains Rider để viết và chạy mã của bạn.
- Kiến thức cơ bản về C#: Mặc dù chúng tôi sẽ hướng dẫn bạn từng bước, nhưng một số kiến thức quen thuộc về C# sẽ rất hữu ích.
## Nhập gói
Chúng ta hãy bắt đầu bằng cách nhập các gói cần thiết cho Aspose.Cells.
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
Dòng này nhập gói Aspose.Cells cần thiết, cung cấp tất cả các lớp và phương thức cần thiết để thao tác với tệp Excel.
Bây giờ, chúng ta hãy đi sâu vào các bước cốt lõi! Chúng ta sẽ xem xét từng dòng mã, giải thích chức năng của nó và lý do tại sao nó lại cần thiết.
## Bước 1: Thiết lập thư mục tài liệu
Đầu tiên, chúng ta cần một nơi để lưu tệp Excel. Thiết lập đường dẫn thư mục đảm bảo tệp của chúng ta được lưu ở một vị trí xác định.
```csharp
// Đường dẫn đến thư mục tài liệu.
string dataDir = "Your Document Directory";
```
 Thay thế`"Your Document Directory"` với đường dẫn mà bạn muốn lưu tệp. Đây có thể là một thư mục cụ thể trên máy tính của bạn, như`"C:\\Documents\\ExcelFiles\\"`.
## Bước 2: Khởi tạo một Workbook mới
Chúng ta cần tạo một bảng tính mới (tệp Excel) để áp dụng những thay đổi về kích thước trang.
```csharp
// Khởi tạo một đối tượng Workbook
Workbook workbook = new Workbook();
```
 Các`Workbook` lớp biểu diễn một tệp Excel. Bằng cách tạo một thể hiện của lớp này, về cơ bản chúng ta đang tạo một sổ làm việc Excel trống mà chúng ta có thể thao tác theo bất kỳ cách nào chúng ta muốn.
## Bước 3: Truy cập vào trang tính đầu tiên
Mỗi sổ làm việc chứa nhiều trang tính. Ở đây, chúng ta sẽ truy cập trang tính đầu tiên để áp dụng các thiết lập của mình.
```csharp
// Truy cập vào trang tính đầu tiên trong tệp Excel
Worksheet worksheet = workbook.Worksheets[0];
```
 Các`Worksheets`bộ sưu tập chứa tất cả các trang tính trong sổ làm việc. Bằng cách sử dụng`workbook.Worksheets[0]`, chúng ta đang chọn trang tính đầu tiên. Bạn có thể sửa đổi chỉ mục này để chọn các trang tính khác.
## Bước 4: Đặt Kích thước giấy thành A4
Bây giờ đến phần chính của nhiệm vụ của chúng ta—thiết lập kích thước giấy thành A4.
```csharp
// Thiết lập kích thước giấy thành A4
worksheet.PageSetup.PaperSize = PaperSizeType.PaperA4;
```
 Các`PageSetup` tài sản của`Worksheet` lớp cho phép chúng ta truy cập vào cài đặt bố cục trang.`PaperSizeType.PaperA4` đặt kích thước trang là A4, đây là một trong những kích thước giấy tiêu chuẩn được sử dụng phổ biến trên toàn thế giới.
 Bạn muốn sử dụng một kích thước giấy khác? Aspose.Cells cung cấp nhiều tùy chọn như`PaperSizeType.PaperLetter`, `PaperSizeType.PaperLegal` và nhiều hơn nữa. Chỉ cần thay thế`PaperA4` với kích thước bạn thích!
## Bước 5: Lưu sổ làm việc
Cuối cùng, chúng ta sẽ lưu bảng tính với kích thước giấy đã điều chỉnh.
```csharp
// Lưu sổ làm việc.
workbook.Save(dataDir + "ManagePaperSize_out.xls");
```
 Các`Save` phương pháp lưu sổ làm việc vào đường dẫn bạn chỉ định. Tên tệp`"ManagePaperSize_out.xls"` có thể tùy chỉnh dựa trên sở thích của bạn. Ở đây, nó được lưu dưới dạng tệp Excel trong`.xls` định dạng, nhưng bạn có thể lưu nó trong`.xlsx` hoặc các định dạng được hỗ trợ khác bằng cách thay đổi phần mở rộng tệp.
## Phần kết luận
Và bạn đã có nó! Bằng cách làm theo các bước đơn giản này, bạn đã đặt kích thước giấy của bảng tính Excel thành A4 bằng Aspose.Cells cho .NET. Phương pháp này vô cùng hữu ích khi bạn cần đảm bảo tài liệu của mình duy trì kích thước giấy nhất quán, đặc biệt là khi in hoặc chia sẻ. 
Với Aspose.Cells, bạn không chỉ bị giới hạn ở khổ giấy A4 mà còn có thể chọn từ nhiều kích cỡ giấy khác nhau và tùy chỉnh thêm các cài đặt thiết lập trang, biến nó thành công cụ mạnh mẽ để tự động hóa và tùy chỉnh các tài liệu Excel.
## Câu hỏi thường gặp
### Tôi có thể thiết lập kích thước giấy khác nhau cho mỗi trang tính không?
 Vâng, chắc chắn rồi! Chỉ cần truy cập từng trang tính riêng lẻ và thiết lập kích thước giấy duy nhất bằng cách sử dụng`worksheet.PageSetup.PaperSize`.
### Aspose.Cells có tương thích với .NET Core không?
Có, Aspose.Cells tương thích với cả .NET Framework và .NET Core, khiến nó trở nên linh hoạt cho nhiều dự án .NET khác nhau.
### Làm thế nào để lưu bảng tính ở định dạng PDF?
 Chỉ cần thay thế`.Save(dataDir + "ManagePaperSize_out.xls")` với`.Save(dataDir + "ManagePaperSize_out.pdf", SaveFormat.Pdf)`và Aspose.Cells sẽ lưu nó dưới dạng PDF.
### Tôi có thể tùy chỉnh các thiết lập trang khác bằng Aspose.Cells không?
Có, Aspose.Cells cho phép bạn điều chỉnh nhiều cài đặt như hướng, tỷ lệ, lề và đầu trang/chân trang thông qua`worksheet.PageSetup`.
### Làm thế nào để tôi có thể dùng thử Aspose.Cells miễn phí?
 Bạn có thể tải xuống phiên bản dùng thử miễn phí từ[Trang tải xuống Aspose.Cells](https://releases.aspose.com/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
