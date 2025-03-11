---
title: Thêm Dấu trang PDF với Điểm đến được Đặt tên trong Aspose.Cells
linktitle: Thêm Dấu trang PDF với Điểm đến được Đặt tên trong Aspose.Cells
second_title: API xử lý Excel Aspose.Cells .NET
description: Tìm hiểu cách tạo PDF tương tác với dấu trang bằng Aspose.Cells cho .NET. Hướng dẫn từng bước này giúp bạn thực hiện dễ dàng.
weight: 10
url: /vi/net/rendering-and-export/add-pdf-bookmarks/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Thêm Dấu trang PDF với Điểm đến được Đặt tên trong Aspose.Cells

## Giới thiệu
Nếu bạn đã từng làm việc với các tài liệu PDF dài, bạn sẽ biết việc điều hướng qua các trang thông tin có thể khó khăn như thế nào. Dấu trang đóng vai trò quan trọng trong việc nâng cao trải nghiệm của người dùng bằng cách cung cấp các điểm điều hướng nhanh. Trong hướng dẫn này, chúng ta sẽ khám phá cách thêm dấu trang có đích đến được đặt tên vào PDF được tạo từ tệp Excel bằng Aspose.Cells cho .NET.
## Điều kiện tiên quyết
Trước khi đi sâu vào chi tiết, hãy đảm bảo bạn đã chuẩn bị mọi thứ. Để làm theo hướng dẫn này, bạn cần:
1. Visual Studio: Đây là IDE dành cho phát triển .NET. Hãy đảm bảo bạn đã cài đặt nó trên máy của mình.
2.  Aspose.Cells cho .NET: Bạn cần có thư viện Aspose.Cells. Bạn có thể[tải xuống ở đây](https://releases.aspose.com/cells/net/) . Nếu bạn muốn thử trước, hãy lấy[dùng thử miễn phí tại đây](https://releases.aspose.com/).
3. .NET Framework: Đảm bảo bạn đã cài đặt phiên bản tương thích. Aspose.Cells hỗ trợ nhiều phiên bản .NET.
4. Kiến thức cơ bản về C#: Nắm được cú pháp C# sẽ giúp bạn hiểu đoạn mã tốt hơn.
Với những mục này trong bộ công cụ, chúng ta đã sẵn sàng tạo tài liệu PDF có đánh dấu trang!
## Nhập gói
Trước tiên, chúng ta cần đảm bảo rằng dự án của chúng ta có thể sử dụng các chức năng của Aspose.Cells. Bắt đầu bằng cách tạo một dự án C# mới trong Visual Studio. Sau đó, bạn sẽ muốn nhập các gói cần thiết. Bạn thường sẽ thực hiện việc này ở đầu tệp mã của mình:
```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;
```
Bạn có thấy điều đó dễ dàng không? Chỉ cần thêm một vài dòng sẽ mở khóa một bộ công cụ mạnh mẽ để xử lý các tệp Excel.
## Bước 1: Thiết lập các thư mục
Để bắt đầu, bạn cần chỉ định thư mục nguồn và thư mục đầu ra. Đây là nơi tệp Excel ban đầu của bạn tồn tại và nơi tệp PDF của bạn sẽ được lưu.
```csharp
string sourceDir = "Your Document Directory"; // ví dụ, "C:\\MyFiles\\"
string outputDir = "Your Document Directory"; // ví dụ, "C:\\MyOutput\\"
```
Hãy nghĩ về bước này như việc chuẩn bị không gian làm việc của bạn. Giống như một họa sĩ sẽ không bắt đầu nếu không có giá vẽ hoặc vải bạt, bạn không nên bắt đầu viết mã nếu không chỉ định vị trí tệp của mình.
## Bước 2: Tải tệp Excel nguồn
Tiếp theo, chúng ta cần tải tệp Excel của bạn vào bộ nhớ bằng cách sử dụng lớp sổ làm việc.
```csharp
Workbook wb = new Workbook(sourceDir + "samplePdfBookmarkEntry_DestinationName.xlsx");
```
Tải sổ làm việc giống như mở một tài liệu đầy tiềm năng. Nó cung cấp quyền truy cập vào tất cả các trang tính, ô và khả năng định dạng của tệp Excel gốc của bạn.
## Bước 3: Truy cập vào Bảng tính
Bây giờ chúng ta đã tải xong bảng tính, hãy truy cập vào bảng tính đầu tiên. Các ô chúng ta sẽ tham chiếu cho dấu trang của mình nằm ở đây.
```csharp
Worksheet ws = wb.Worksheets[0];
```
Mỗi nghệ sĩ đều cần một tấm vải! Trong trường hợp này, bảng tính đóng vai trò như tấm vải của bạn, nơi bạn sẽ xác định ô nào sẽ chứa dấu trang.
## Bước 4: Tạo dấu trang
### Truy cập các ô cụ thể
Hãy tạo một dấu trang cho một ô cụ thể—giả sử ô C5. Chúng ta sẽ tạo một mục đánh dấu, liên kết mục đó với ô đó và chỉ định một tên. 
```csharp
Cell cell = ws.Cells["C5"];
PdfBookmarkEntry bookmarkEntry = new PdfBookmarkEntry();
bookmarkEntry.Text = "Text"; // Thay đổi tên dấu trang ưa thích của bạn
bookmarkEntry.Destination = cell;
bookmarkEntry.DestinationName = "AsposeCells--" + cell.Name;
```
Bạn có thể nghĩ về điều này như việc dán một ghi chú dán lên tài liệu của bạn. Tiêu đề cho biết dấu trang của bạn dẫn đến đâu, trong khi đích đến (ô C5) là nơi nó đưa bạn đến trong PDF.
### Thêm dấu trang phụ
Chúng ta có thể nâng cao trải nghiệm người dùng bằng cách thêm các dấu trang phụ. Bây giờ chúng ta sẽ truy cập vào hai ô bổ sung (G56 và L4) và thiết lập chúng làm dấu trang phụ.
```csharp
cell = ws.Cells["G56"];
PdfBookmarkEntry subbookmarkEntry1 = new PdfBookmarkEntry();
subbookmarkEntry1.Text = "Text1"; // Dấu trang phụ đầu tiên
subbookmarkEntry1.Destination = cell;
subbookmarkEntry1.DestinationName = "AsposeCells--" + cell.Name;
cell = ws.Cells["L4"];
PdfBookmarkEntry subbookmarkEntry2 = new PdfBookmarkEntry();
subbookmarkEntry2.Text = "Text2"; // Dấu trang phụ thứ hai
subbookmarkEntry2.Destination = cell;
subbookmarkEntry2.DestinationName = "AsposeCells--" + cell.Name;
```
Các dấu trang phụ này hoạt động giống như các chương của một cuốn sách, hướng dẫn người dùng đến nội dung cụ thể hơn trong tài liệu.
### Thêm Dấu trang phụ vào Danh sách
Tiếp theo, chúng ta sẽ nhóm các dấu trang phụ vào dấu trang chính mà chúng ta đã tạo trước đó.
```csharp
ArrayList list = new ArrayList();
list.Add(subbookmarkEntry1);
list.Add(subbookmarkEntry2);
bookmarkEntry.SubEntry = list;
```
Tổ chức này tạo ra một cấu trúc phân cấp giúp đơn giản hóa việc điều hướng—tuân thủ “các nguyên tắc cơ bản về đánh dấu trang” để có trải nghiệm tối ưu cho người dùng!
## Bước 5: Lưu PDF bằng Bookmarks
### Tạo PdfSaveOptions
Đã đến lúc tạo tùy chọn lưu PDF và thêm dấu trang mà chúng ta đã tạo.
```csharp
PdfSaveOptions opts = new PdfSaveOptions();
opts.Bookmark = bookmarkEntry;
```
Bước này là nơi tất cả các bước chuẩn bị trước đó của bạn kết hợp lại với nhau. Về cơ bản, bạn đang nói rằng, "Tôi muốn tệp PDF của mình không chỉ là một tài liệu phẳng mà còn là một hướng dẫn tương tác!"
### Lưu tài liệu
Cuối cùng, chúng ta lưu sổ làm việc ở định dạng PDF, kết hợp dấu trang vào hành động này.
```csharp
wb.Save(outputDir + "outputPdfBookmarkEntry_DestinationName.pdf", opts);
```
Cứ như vậy, mọi công sức của bạn sẽ được đền đáp bằng một tài liệu PDF có cấu trúc tốt và đầy đủ dấu trang tiện dụng!
## Phần kết luận
Xin chúc mừng! Bạn đã tạo thành công một tệp PDF có dấu trang và đích đến được đặt tên bằng Aspose.Cells cho .NET. Bạn đã học cách điều hướng qua các tệp Excel, truy cập các ô cụ thể và tạo dấu trang giúp tăng cường tương tác của người dùng. Hãy tưởng tượng xem việc điều hướng các tài liệu PDF của bạn sẽ dễ dàng hơn bao nhiêu với các dấu trang tiện dụng này.
## Câu hỏi thường gặp
### Aspose.Cells dành cho .NET là gì?
Aspose.Cells là một thư viện mạnh mẽ để làm việc với các tệp Excel, cho phép bạn tạo, sửa đổi và chuyển đổi bảng tính theo chương trình.
### Tôi có thể sử dụng Aspose.Cells trong một dự án miễn phí không?
Có! Aspose cung cấp bản dùng thử miễn phí nếu bạn muốn khám phá các tính năng trước khi mua giấy phép.
### Làm thế nào để tôi có được giấy phép sử dụng Aspose.Cells?
 Bạn có thể mua giấy phép trực tiếp từ họ[trang mua hàng](https://purchase.aspose.com/buy).
### Aspose.Cells có thể làm việc với những loại tài liệu nào?
Nó có thể hoạt động với nhiều định dạng khác nhau, bao gồm XLSX, XLS, CSV, PDF và nhiều định dạng khác.
### Tôi có thể nhận trợ giúp ở đâu nếu gặp vấn đề?
 Bạn có thể tìm thấy sự hỗ trợ trong[Diễn đàn Aspose](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
