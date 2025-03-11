---
title: Nhận Điểm Kết Nối của Hình Dạng trong Excel
linktitle: Nhận Điểm Kết Nối của Hình Dạng trong Excel
second_title: API xử lý Excel Aspose.Cells .NET
description: Tìm hiểu cách lấy điểm kết nối hình dạng trong Excel bằng Aspose.Cells cho .NET. Làm theo hướng dẫn từng bước của chúng tôi để dễ dàng trích xuất và hiển thị điểm hình dạng theo chương trình.
weight: 11
url: /vi/net/excel-shapes-controls/get-connection-points-shape-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Nhận Điểm Kết Nối của Hình Dạng trong Excel

## Giới thiệu
Khi làm việc với các tệp Excel theo chương trình, chúng ta thường cần tương tác với các hình dạng được nhúng trong các trang tính. Một trong những tác vụ nâng cao hơn mà bạn có thể thực hiện là trích xuất các điểm kết nối từ một hình dạng. Các điểm kết nối được sử dụng để gắn các hình dạng với các đầu nối và quản lý bố cục của chúng chính xác hơn. Nếu bạn đang muốn lấy các điểm kết nối của một hình dạng trong Excel, Aspose.Cells for .NET là công cụ bạn cần. Trong hướng dẫn này, chúng tôi sẽ hướng dẫn bạn từng bước để thực hiện việc này.
## Điều kiện tiên quyết
Trước khi tìm hiểu về mã, hãy đảm bảo bạn có đủ các điều kiện tiên quyết sau:
- Aspose.Cells cho .NET: Bạn sẽ cần phải cài đặt Aspose.Cells trong môi trường phát triển của mình. Nếu bạn chưa có, bạn có thể[tải phiên bản mới nhất tại đây](https://releases.aspose.com/cells/net/).
- Môi trường phát triển: Đảm bảo bạn có cài đặt Visual Studio hoặc bất kỳ IDE nào tương thích với .NET.
- Kiến thức cơ bản về C#: Hướng dẫn này giả định rằng bạn có hiểu biết cơ bản về lập trình C# và các nguyên tắc hướng đối tượng.
 Bạn cũng có thể đăng ký một[dùng thử miễn phí Aspose.Cells](https://releases.aspose.com/) nếu bạn chưa làm như vậy. Điều này sẽ giúp bạn truy cập vào tất cả các tính năng cần thiết cho hướng dẫn này.

## Nhập gói
Để làm việc với Aspose.Cells trong dự án của bạn, bạn cần bao gồm các không gian tên cần thiết. Các câu lệnh import sau đây phải được đặt ở đầu mã của bạn:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
Các không gian tên này cho phép bạn truy cập vào chức năng cốt lõi của Aspose.Cells và cho phép bạn thao tác trên bảng tính và hình dạng.

## Hướng dẫn từng bước để có được các điểm kết nối của một hình dạng
Trong phần này, chúng tôi sẽ hướng dẫn bạn cách trích xuất các điểm kết nối của một hình dạng trong bảng tính Excel. Thực hiện từng bước một cách cẩn thận để hiểu rõ.
## Bước 1: Khởi tạo một Workbook mới
 Trước tiên, chúng ta cần tạo một phiên bản của`Workbook` class. Đây là tệp Excel trong Aspose.Cells. Nếu bạn không có tệp hiện có, không vấn đề gì—bạn có thể bắt đầu bằng một sổ làm việc trống.
```csharp
// Tạo một Workbook mới
Workbook workbook = new Workbook();
```
 Trong bước này, chúng tôi đã tạo một bảng tính Excel trống, nhưng bạn cũng có thể tải một bảng tính hiện có bằng cách chuyển đường dẫn tệp đến`Workbook` người xây dựng.
## Bước 2: Truy cập vào Bảng tính đầu tiên
Tiếp theo, chúng ta cần truy cập vào worksheet mà chúng ta muốn làm việc với các hình dạng. Trong trường hợp này, chúng ta sẽ sử dụng worksheet đầu tiên của workbook.
```csharp
// Nhận bảng tính đầu tiên trong sổ làm việc
Worksheet worksheet = workbook.Worksheets[0];
```
 Dòng này truy cập vào trang tính đầu tiên từ bộ sưu tập các trang tính trong sổ làm việc. Nếu bạn đang làm việc với một trang tính cụ thể, bạn có thể thay thế chỉ mục`0` với chỉ số mong muốn.
## Bước 3: Thêm hộp văn bản mới (Hình dạng)
Bây giờ, hãy thêm một hình dạng mới vào bảng tính. Chúng ta sẽ tạo một hộp văn bản, đây là một loại hình dạng. Bạn cũng có thể thêm các loại hình dạng khác, nhưng để đơn giản, chúng ta sẽ sử dụng hộp văn bản trong hướng dẫn này.
```csharp
// Thêm hộp văn bản mới vào bộ sưu tập
int textboxIndex = worksheet.TextBoxes.Add(2, 1, 160, 200);
```
Sau đây là những gì chúng tôi đã làm:
-  Đã thêm hộp văn bản ở hàng`2` , cột`1`.
-  Đặt kích thước của hộp văn bản thành`160` đơn vị chiều rộng và`200` đơn vị chiều cao.
## Bước 4: Truy cập Hình dạng từ Bộ sưu tập Hình dạng
 Sau khi chúng ta thêm hộp văn bản, nó sẽ trở thành một phần của bộ sưu tập hình dạng của bảng tính. Bây giờ chúng ta sẽ truy cập hình dạng đó bằng cách sử dụng`Shapes`bộ sưu tập.
```csharp
// Truy cập hình dạng (hộp văn bản) từ bộ sưu tập hình dạng
Shape shape = workbook.Worksheets[0].Shapes[0];
```
Trong bước này, chúng ta sẽ lấy hình dạng đầu tiên (hộp văn bản của chúng ta) từ bộ sưu tập. Nếu bạn có nhiều hình dạng, bạn có thể chỉ định chỉ mục hoặc thậm chí tìm hình dạng theo tên.
## Bước 5: Lấy lại các điểm kết nối
Bây giờ chúng ta đã có hình dạng của mình, hãy trích xuất các điểm kết nối của nó. Các điểm này được sử dụng để gắn các đầu nối vào hình dạng.`ConnectionPoints` thuộc tính của hình dạng trả về tất cả các điểm kết nối có sẵn.
```csharp
// Lấy tất cả các điểm kết nối trong hình dạng này
var connectionPoints = shape.ConnectionPoints;
```
Điều này cung cấp cho chúng ta một tập hợp tất cả các điểm kết nối có sẵn cho hình dạng đó.
## Bước 6: Hiển thị các điểm kết nối
Cuối cùng, chúng ta muốn hiển thị tọa độ của từng điểm kết nối. Đây là nơi chúng ta lặp qua các điểm kết nối và in chúng ra bảng điều khiển.
```csharp
// Hiển thị tất cả các điểm hình dạng
foreach (var pt in connectionPoints)
{
    System.Console.WriteLine(string.Format("X = {0}, Y = {1}", pt.X, pt.Y));
}
```
 Vòng lặp này lặp lại qua từng điểm kết nối và in ra`X` Và`Y` tọa độ. Điều này có thể hữu ích để gỡ lỗi hoặc xác nhận trực quan các điểm kết nối của một hình dạng.
## Bước 7: Thực hiện và Hoàn tất
Sau khi thiết lập tất cả các bước trên, bạn có thể chạy mã. Đây là dòng cuối cùng đảm bảo quá trình hoàn tất thành công:
```csharp
System.Console.WriteLine("GetShapeConnectionPoints executed successfully.");
```
Dòng này chỉ đơn giản là ghi lại thông báo vào bảng điều khiển cho biết quá trình đã hoàn tất.

## Phần kết luận
Trong hướng dẫn này, chúng tôi đã trình bày cách lấy các điểm kết nối của một hình dạng trong Excel bằng Aspose.Cells cho .NET. Bằng cách chia nhỏ nhiệm vụ thành các bước nhỏ, dễ hiểu, chúng tôi đã khám phá quy trình tạo sổ làm việc, thêm hình dạng và trích xuất các điểm kết nối.
Bằng cách hiểu cách thao tác các hình dạng theo chương trình, bạn sẽ mở ra một thế giới khả năng để xây dựng các bảng tính Excel động và tương tác. Cho dù bạn đang xây dựng báo cáo, thiết kế bảng thông tin hay tạo sơ đồ, kiến thức này sẽ hữu ích.
## Câu hỏi thường gặp
### Điểm kết nối trong hình dạng là gì?
Điểm kết nối là điểm cụ thể trên một hình dạng mà bạn có thể gắn các đầu nối hoặc liên kết nó với các hình dạng khác.
### Tôi có thể lấy điểm kết nối cho tất cả các hình dạng trong một bảng tính không?
Có, Aspose.Cells cho phép bạn lấy các điểm kết nối cho bất kỳ hình dạng nào hỗ trợ chúng. Chỉ cần lặp qua bộ sưu tập hình dạng trong bảng tính.
### Tôi có cần giấy phép để sử dụng Aspose.Cells không?
Có, mặc dù bạn có thể dùng thử miễn phí, nhưng cần phải có giấy phép để có đầy đủ tính năng. Bạn có thể[mua giấy phép ở đây](https://purchase.aspose.com/buy)hoặc nhận được một[giấy phép tạm thời](https://purchase.aspose.com/temporary-license/).
### Làm thế nào tôi có thể thêm các loại hình dạng khác nhau vào Aspose.Cells?
Bạn có thể sử dụng`Add` phương pháp cho các hình dạng như hình chữ nhật, hình elip, v.v. Mỗi hình dạng có các tham số cụ thể mà bạn có thể tùy chỉnh.
### Làm thế nào để tải tệp Excel hiện có thay vì tạo tệp mới?
 Để tải một tệp hiện có, hãy chuyển đường dẫn tệp đến`Workbook` constructor, như thế này:  
```csharp
Workbook workbook = new Workbook("path_to_file.xlsx");
```
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
