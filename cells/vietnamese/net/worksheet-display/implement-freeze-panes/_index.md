---
title: Triển khai Freeze Panes trong Worksheet
linktitle: Triển khai Freeze Panes trong Worksheet
second_title: API xử lý Excel Aspose.Cells .NET
description: Tìm hiểu cách triển khai ngăn đóng băng trong Excel bằng Aspose.Cells cho .NET với hướng dẫn chi tiết từng bước này. Nâng cao khả năng sử dụng bảng tính của bạn một cách hiệu quả.
weight: 15
url: /vi/net/worksheet-display/implement-freeze-panes/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Triển khai Freeze Panes trong Worksheet

## Giới thiệu
Hãy tưởng tượng bạn có một bảng tính Excel với một tập dữ liệu khổng lồ và mỗi lần bạn cuộn xuống hoặc cuộn ngang, bạn lại mất dấu những tiêu đề quan trọng đó. Sẽ tiện lợi biết bao nếu những tiêu đề đó có thể giữ nguyên vị trí khi bạn cuộn? Đó chính là lúc các ngăn cố định xuất hiện, giúp việc điều hướng trở nên mượt mà và hiệu quả. Aspose.Cells for .NET đơn giản hóa quy trình này, giúp bạn có thể triển khai các ngăn cố định một cách liền mạch. Hướng dẫn này sẽ hướng dẫn bạn thực hiện quy trình, chia nhỏ từng bước để bạn có thể thiết lập các tiêu đề cố định đó ngay lập tức.
## Điều kiện tiên quyết
Trước khi bắt đầu, hãy đảm bảo bạn đã chuẩn bị sẵn một số thứ:
-  Aspose.Cells cho Thư viện .NET: Bạn sẽ cần tải xuống thư viện này từ[Trang phát hành của Aspose](https://releases.aspose.com/cells/net/).
- Đã cài đặt .NET Framework: Đảm bảo bạn đã thiết lập .NET trong môi trường phát triển của mình.
- Kiến thức cơ bản về C#: Sự quen thuộc với C# sẽ hữu ích cho việc theo dõi.
- Tệp Excel: Chuẩn bị sẵn một tệp Excel (ví dụ: “book1.xls”) mà bạn sẽ áp dụng khung đóng băng vào.
Bạn có thể khám phá thêm chi tiết về Aspose.Cells trên[trang tài liệu](https://reference.aspose.com/cells/net/).

## Nhập gói
Hãy bắt đầu bằng cách nhập các gói cần thiết. Mở dự án C# của bạn và đảm bảo nhập những gói này:
```csharp
using System.IO;
using Aspose.Cells;
```
Sau khi chuẩn bị xong các gói, chúng ta hãy cùng xem hướng dẫn từng bước.
Chúng ta sẽ xem xét từng giai đoạn thiết lập ngăn đóng băng bằng Aspose.Cells cho .NET. Thực hiện từng bước một cách cẩn thận và bạn sẽ có ngăn đóng băng được áp dụng vào bảng tính của mình một cách dễ dàng.
## Bước 1: Xác định đường dẫn đến thư mục tài liệu của bạn
 Trước khi bạn có thể mở tệp Excel, bạn sẽ cần chỉ định đường dẫn đến tài liệu của mình. Thiết lập`dataDir` biến giữ đường dẫn thư mục cho các tập tin của bạn.
```csharp
// Đường dẫn đến thư mục tài liệu.
string dataDir = "Your Document Directory";
```
 Thay thế`"Your Document Directory"` với đường dẫn thực tế đến nơi lưu trữ tệp Excel của bạn. Điều này sẽ giúp chương trình xác định vị trí tệp của bạn.
## Bước 2: Mở tệp Excel bằng FileStream
Tiếp theo, chúng ta cần tải tệp Excel để Aspose.Cells có thể thực hiện phép thuật của nó. Để thực hiện việc này, chúng ta sẽ tạo một luồng tệp và mở tệp Excel bằng luồng đó.
```csharp
// Tạo luồng tệp chứa tệp Excel cần mở
FileStream fstream = new FileStream(dataDir + "book1.xls", FileMode.Open);
```
Bằng cách sử dụng luồng tệp, bạn sẽ mở tệp để Aspose.Cells truy cập mà không làm thay đổi tệp gốc cho đến khi bạn lưu rõ ràng mọi thay đổi.
## Bước 3: Khởi tạo đối tượng Workbook
 Với luồng tập tin đã có, đã đến lúc tạo một`Workbook` đối tượng. Đối tượng này rất cần thiết vì nó đại diện cho toàn bộ sổ làm việc Excel của bạn, cho phép bạn làm việc với từng trang tính, ô và cài đặt riêng lẻ trong tệp.
```csharp
// Khởi tạo một đối tượng Workbook
// Mở tệp Excel thông qua luồng tệp
Workbook workbook = new Workbook(fstream);
```
 Nghĩ về`Workbook` như một bìa kẹp giữ tất cả các tờ giấy của bạn lại với nhau. Khi bạn mở bìa kẹp, bạn có thể truy cập bất kỳ trang nào (bảng tính) bên trong.
## Bước 4: Truy cập vào trang tính đầu tiên
Bây giờ sổ làm việc của bạn đã được tải, bạn có thể chọn trang tính nào để áp dụng khung cố định. Trong ví dụ này, chúng ta sẽ làm việc với trang tính đầu tiên. Aspose.Cells giúp bạn dễ dàng chọn trang tính bằng cách lập chỉ mục.
```csharp
// Truy cập vào trang tính đầu tiên trong tệp Excel
Worksheet worksheet = workbook.Worksheets[0];
```
 Nếu bạn cần làm việc trên một trang tính khác, chỉ cần điều chỉnh chỉ mục trong`workbook.Worksheets[0]`.
## Bước 5: Áp dụng Cài đặt Freeze Panes
 Đây là nơi phép thuật xảy ra! Để thiết lập các ngăn đông lạnh, hãy sử dụng`FreezePanes`phương pháp này chỉ định hàng và cột mà bạn muốn bắt đầu đóng băng, cũng như số lượng hàng và cột sẽ đóng băng.
```csharp
// Áp dụng cài đặt khung đóng băng
worksheet.FreezePanes(3, 2, 3, 2);
```
Chúng ta hãy phân tích các thông số:
- Hàng đầu tiên (3): Bắt đầu đông lạnh ở hàng 3.
- Cột đầu tiên (2): Bắt đầu đóng băng ở cột 2.
- Số hàng (3): Đóng băng 3 hàng.
- Số cột (2): Đóng băng 2 cột.
Điều chỉnh các giá trị này dựa trên nhu cầu cụ thể của bạn. Điểm đóng băng sẽ là giao điểm của hàng và cột được chỉ định.
## Bước 6: Lưu tệp Excel đã sửa đổi
 Sau khi áp dụng các ngăn đóng băng, đã đến lúc lưu các thay đổi của bạn. Việc lưu tệp sổ làm việc đã sửa đổi đảm bảo các thiết lập đóng băng của bạn được giữ nguyên. Bạn có thể lưu tệp đã cập nhật bằng cách sử dụng`Save` phương pháp.
```csharp
// Lưu tệp Excel đã sửa đổi
workbook.Save(dataDir + "output.xls");
```
Hãy lưu tệp đó với tên khác nếu bạn muốn giữ nguyên tệp gốc.
## Bước 7: Đóng luồng tập tin
Cuối cùng, hãy nhớ đóng luồng tệp. Thao tác này giải phóng tài nguyên hệ thống và hoàn tất mọi kết nối mở tới tệp.
```csharp
// Đóng luồng tệp để giải phóng tất cả tài nguyên
fstream.Close();
```
Hãy nghĩ việc đóng luồng giống như việc đặt tệp trở lại giá sau khi bạn hoàn tất. Đây là thói quen quản lý tốt.

## Phần kết luận
Xin chúc mừng! Bạn đã áp dụng thành công freeze panes vào một bảng tính Excel bằng Aspose.Cells for .NET. Kỹ thuật này cực kỳ hữu ích để quản lý các tập dữ liệu lớn, đảm bảo rằng các tiêu đề hoặc hàng và cột cụ thể vẫn hiển thị khi cuộn qua dữ liệu. Bằng cách làm theo hướng dẫn từng bước này, bạn có thể tự tin triển khai freeze panes và nâng cao khả năng sử dụng của bảng tính.
## Câu hỏi thường gặp
### Tôi có thể đóng băng nhiều trang tính trong một bảng tính không?
 Vâng, chỉ cần lặp lại`FreezePanes` phương pháp này trên mỗi trang tính mà bạn muốn áp dụng.
### Điều gì xảy ra nếu tôi sử dụng các giá trị hàng và cột vượt quá phạm vi của trang tính?
Aspose.Cells sẽ đưa ra ngoại lệ, vì vậy hãy đảm bảo các giá trị của bạn nằm trong giới hạn của bảng tính.
### Tôi có thể điều chỉnh cài đặt khung đóng băng sau khi áp dụng không?
 Chắc chắn rồi! Chỉ cần gọi`FreezePanes`phương pháp một lần nữa với các tham số mới để cập nhật cài đặt.
### Tính năng đóng băng có hoạt động trên mọi phiên bản tệp Excel không?
Có, các ngăn đóng băng sẽ được lưu giữ ở hầu hết các định dạng Excel (ví dụ: XLS, XLSX) được Aspose.Cells hỗ trợ.
### Tôi có thể rã đông các ô kính không?
 Để xóa các khung đóng băng, chỉ cần gọi`UnfreezePanes()` trên phiếu bài tập.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
