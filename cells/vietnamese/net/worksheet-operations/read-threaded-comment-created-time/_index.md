---
title: Đọc Thời gian tạo của Bình luận có chủ đề trong Bảng tính
linktitle: Đọc Thời gian tạo của Bình luận có chủ đề trong Bảng tính
second_title: API xử lý Excel Aspose.Cells .NET
description: Học cách đọc thời gian tạo chú thích theo luồng trong Excel bằng Aspose.Cells cho .NET. Hướng dẫn từng bước có kèm ví dụ về mã.
weight: 21
url: /vi/net/worksheet-operations/read-threaded-comment-created-time/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Đọc Thời gian tạo của Bình luận có chủ đề trong Bảng tính

## Giới thiệu
Khi làm việc với các tệp Excel, việc quản lý các bình luận có thể là một khía cạnh quan trọng của sự cộng tác và phản hồi dữ liệu. Nếu bạn đang sử dụng Aspose.Cells cho .NET, bạn sẽ thấy nó cực kỳ mạnh mẽ để xử lý nhiều chức năng Excel khác nhau, bao gồm cả các bình luận theo luồng. Trong hướng dẫn này, chúng ta sẽ tập trung vào cách đọc thời gian tạo các bình luận theo luồng trong một bảng tính. Cho dù bạn là một nhà phát triển dày dạn kinh nghiệm hay chỉ mới bắt đầu, hướng dẫn này sẽ hướng dẫn bạn từng bước trong quy trình.
## Điều kiện tiên quyết
Trước khi đi sâu vào mã, hãy đảm bảo rằng bạn có mọi thứ cần thiết để bắt đầu:
1. Aspose.Cells cho .NET: Đảm bảo rằng bạn đã cài đặt thư viện Aspose.Cells. Bạn có thể tải xuống từ[Trang web Aspose](https://releases.aspose.com/cells/net/).
2. Visual Studio: Bản cài đặt Visual Studio hoặc bất kỳ IDE .NET nào khác mà bạn có thể viết và thực thi mã C#.
3. Kiến thức cơ bản về C#: Sự quen thuộc với lập trình C# sẽ giúp bạn hiểu các đoạn mã tốt hơn.
4.  Tệp Excel: Chuẩn bị một tệp Excel với một số chú thích có chủ đề. Đối với ví dụ này, chúng tôi sẽ sử dụng một tệp có tên`ThreadedCommentsSample.xlsx`.
Bây giờ chúng ta đã đáp ứng được các điều kiện tiên quyết, hãy nhập các gói cần thiết.
## Nhập gói
Để bắt đầu với Aspose.Cells, bạn cần nhập các không gian tên cần thiết. Sau đây là cách thực hiện:
### Nhập không gian tên Aspose.Cells
Mở dự án C# của bạn trong Visual Studio và thêm lệnh using sau vào đầu tệp mã của bạn:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Không gian tên này cho phép bạn truy cập tất cả các lớp và phương thức được cung cấp bởi thư viện Aspose.Cells.
Bây giờ chúng ta đã thiết lập xong bối cảnh, hãy chia nhỏ quá trình đọc thời gian tạo bình luận theo chuỗi thành các bước dễ quản lý.
## Bước 1: Xác định thư mục nguồn
Đầu tiên, bạn cần chỉ định thư mục chứa tệp Excel của bạn. Điều này rất quan trọng vì chương trình cần biết nơi tìm tệp.
```csharp
// Thư mục nguồn
string sourceDir = "Your Document Directory";
```
 Thay thế`"Your Document Directory"`với đường dẫn thực tế đến tệp Excel của bạn. Điều này có thể giống như`"C:\\Documents\\"`.
## Bước 2: Tải Workbook
Tiếp theo, bạn sẽ tải sổ làm việc Excel có chứa các chú thích theo luồng. Sau đây là cách thực hiện:
```csharp
Workbook workbook = new Workbook(sourceDir + "ThreadedCommentsSample.xlsx");
```
 Dòng mã này tạo ra một cái mới`Workbook` đối tượng bằng cách tải tệp Excel đã chỉ định. Nếu không tìm thấy tệp, ngoại lệ sẽ được đưa ra, do đó hãy đảm bảo đường dẫn là chính xác.
## Bước 3: Truy cập vào Bảng tính
Sau khi sổ làm việc được tải, bước tiếp theo là truy cập vào trang tính cụ thể có chứa các bình luận. Trong trường hợp của chúng tôi, chúng tôi sẽ truy cập vào trang tính đầu tiên:
```csharp
// Truy cập bảng tính đầu tiên
Worksheet worksheet = workbook.Worksheets[0];
```
Dòng này lấy trang tính đầu tiên (chỉ mục 0) từ sổ làm việc. Nếu bình luận của bạn nằm trên một trang tính khác, hãy điều chỉnh chỉ mục cho phù hợp.
## Bước 4: Nhận bình luận theo chủ đề
Bây giờ, đã đến lúc lấy các bình luận theo luồng từ một ô cụ thể. Trong ví dụ này, chúng ta sẽ lấy các bình luận từ ô A1:
```csharp
// Nhận bình luận theo chủ đề
ThreadedCommentCollection threadedComments = worksheet.Comments.GetThreadedComments("A1");
```
Dòng này lấy tất cả các chú thích có luồng liên quan đến ô A1. Nếu không có chú thích nào, bộ sưu tập sẽ trống.
## Bước 5: Lặp lại qua các bình luận
Sau khi lấy được các bình luận theo chủ đề, giờ đây chúng ta có thể lặp qua chúng và hiển thị thông tin chi tiết, bao gồm cả thời gian tạo:
```csharp
foreach (ThreadedComment comment in threadedComments)
{
    Console.WriteLine("Comment: " + comment.Notes);
    Console.WriteLine("Author: " + comment.Author.Name);
    Console.WriteLine("Created Time: " + comment.CreatedTime);
}
```
 Vòng lặp này đi qua từng bình luận trong`threadedComments` bộ sưu tập và in ra nội dung bình luận, tên tác giả và thời gian tạo bình luận.
## Bước 6: Tin nhắn xác nhận
Cuối cùng, sau khi thực hiện logic đọc bình luận, luôn là một ý tưởng hay khi cung cấp một thông báo xác nhận. Điều này giúp gỡ lỗi và đảm bảo rằng mã đã thực thi thành công:
```csharp
Console.WriteLine("ReadThreadedCommentCreatedTime executed successfully.");
```
## Phần kết luận
Xin chúc mừng! Bạn đã học thành công cách đọc thời gian tạo của các bình luận theo luồng trong bảng tính Excel bằng Aspose.Cells cho .NET. Chức năng này có thể cực kỳ hữu ích để theo dõi phản hồi và cộng tác trong các tài liệu Excel của bạn. Chỉ với một vài dòng mã, bạn có thể trích xuất thông tin có giá trị có thể nâng cao quy trình phân tích dữ liệu và báo cáo của mình.
## Câu hỏi thường gặp
### Aspose.Cells dành cho .NET là gì?
Aspose.Cells for .NET là một thư viện mạnh mẽ cho phép các nhà phát triển tạo, thao tác và chuyển đổi các tệp Excel trong các ứng dụng .NET.
### Làm thế nào tôi có thể tải xuống Aspose.Cells cho .NET?
 Bạn có thể tải nó xuống từ[Trang web Aspose](https://releases.aspose.com/cells/net/).
### Có bản dùng thử miễn phí không?
 Có, bạn có thể dùng thử Aspose.Cells miễn phí bằng cách truy cập[trang dùng thử miễn phí](https://releases.aspose.com/).
### Tôi có thể truy cập vào bình luận từ các ô khác không?
Chắc chắn rồi! Bạn có thể sửa đổi tham chiếu ô trong`GetThreadedComments` phương pháp truy cập vào các bình luận từ bất kỳ ô nào.
### Tôi có thể nhận hỗ trợ cho Aspose.Cells ở đâu?
 Để được hỗ trợ, bạn có thể truy cập[Diễn đàn Aspose](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
