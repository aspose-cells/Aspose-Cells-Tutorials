---
title: Thiết lập mẫu theo chương trình trong Excel
linktitle: Thiết lập mẫu theo chương trình trong Excel
second_title: API xử lý Excel Aspose.Cells .NET
description: Tìm hiểu cách thiết lập mẫu theo chương trình trong Excel bằng Aspose.Cells cho .NET với hướng dẫn từng bước này.
weight: 12
url: /vi/net/excel-borders-and-formatting-options/setting-pattern/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Thiết lập mẫu theo chương trình trong Excel

## Giới thiệu
Bạn đã bao giờ thấy mình vật lộn với các tùy chọn định dạng của Excel, ước gì bạn có thể tự động hóa quy trình này chưa? Cho dù bạn là một nhà phát triển đang tìm cách tạo các bảng tính được đánh bóng hay một người chỉ muốn làm cho bản trình bày dữ liệu của mình trở nên hấp dẫn hơn, Aspose.Cells cho .NET chính là vũ khí bí mật của bạn. Trong hướng dẫn này, chúng ta sẽ tìm hiểu cách thiết lập các mẫu theo chương trình trong Excel bằng Aspose.Cells. Chúng tôi sẽ chia nhỏ từng bước, đảm bảo bạn nắm bắt được từng khái niệm như một chuyên gia. Vậy hãy lấy đồ uống yêu thích của bạn và bắt đầu thôi!
## Điều kiện tiên quyết
Trước khi bắt đầu hành trình, hãy đảm bảo rằng bạn có mọi thứ cần thiết để thành công:
1. Visual Studio: Đảm bảo bạn đã cài đặt Visual Studio trên máy của mình. Đây là nơi phép thuật sẽ xảy ra!
2.  Aspose.Cells cho .NET: Bạn sẽ cần phải thiết lập thư viện Aspose.Cells trong dự án của mình. Bạn có thể tải xuống từ[đây](https://releases.aspose.com/cells/net/).
3. Kiến thức cơ bản về C#: Hiểu biết cơ bản về lập trình C# sẽ giúp bạn xử lý mã một cách dễ dàng.
4. .NET Framework: Đảm bảo bạn đang sử dụng phiên bản .NET Framework tương thích có hỗ trợ Aspose.Cells.
Khi đã đáp ứng được những điều kiện tiên quyết này, bạn đã sẵn sàng để tiến hành!
## Nhập gói
Để bắt đầu, bạn cần nhập các không gian tên Aspose.Cells cần thiết vào dự án của mình. Sau đây là cách thực hiện:
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
```
Các không gian tên này sẽ cung cấp cho bạn quyền truy cập vào tất cả các chức năng cần thiết cho các hoạt động Excel của chúng tôi. Bây giờ chúng ta đã có các gói của mình, hãy cùng tìm hiểu hướng dẫn từng bước!
## Bước 1: Thiết lập môi trường của bạn
Trước khi bắt đầu viết mã, hãy thiết lập môi trường. Điều này bao gồm việc tạo một dự án mới trong Visual Studio và thêm tham chiếu đến thư viện Aspose.Cells.
1. Tạo một dự án mới: Mở Visual Studio và tạo một dự án Ứng dụng bảng điều khiển C# mới.
2. Thêm tham chiếu Aspose.Cells: Nhấp chuột phải vào dự án của bạn trong Solution Explorer, chọn “Manage NuGet Packages” và tìm kiếm Aspose.Cells. Cài đặt phiên bản mới nhất.
Bây giờ bạn đã sẵn sàng để viết mã!
## Bước 2: Khởi tạo một Workbook
 Bước đầu tiên trong việc tạo tệp Excel của chúng tôi là khởi tạo một`Workbook` đối tượng. Đối tượng này sẽ đại diện cho bảng tính Excel của bạn.
```csharp
// Đường dẫn đến thư mục tài liệu.
string dataDir = "Your Document Directory";
// Khởi tạo một đối tượng Workbook
Workbook workbook = new Workbook();
Worksheet sheet = workbook.Worksheets[0];
```
 Trong đoạn trích này, hãy thay thế`"Your Document Directory"` với đường dẫn mà bạn muốn lưu tệp Excel của mình.`Workbook` đối tượng được tạo và chúng ta tham chiếu đến trang tính đầu tiên, đây sẽ là sân chơi của chúng ta.
## Bước 3: Thêm Định dạng có điều kiện
Bây giờ, hãy thêm một chút phong cách cho bảng tính của chúng ta bằng cách áp dụng định dạng có điều kiện. Điều này cho phép chúng ta thay đổi giao diện của các ô dựa trên giá trị của chúng.
```csharp
// Thêm định dạng có điều kiện trống
int index = sheet.ConditionalFormattings.Add();
FormatConditionCollection fcs = sheet.ConditionalFormattings[index];
```
Ở đây, chúng ta thêm một bộ sưu tập định dạng có điều kiện trống vào bảng tính của mình. Đây là nơi chúng ta sẽ chỉ định các quy tắc định dạng.
## Bước 4: Xác định phạm vi cho định dạng có điều kiện
Tiếp theo, chúng ta cần xác định phạm vi ô sẽ bị ảnh hưởng bởi các quy tắc định dạng có điều kiện.
```csharp
// Thiết lập phạm vi định dạng có điều kiện.
CellArea ca = new CellArea();
ca.StartRow = 0;
ca.EndRow = 5;
ca.StartColumn = 0;
ca.EndColumn = 3;
fcs.AddArea(ca);
```
Trong ví dụ này, chúng tôi thiết lập định dạng có điều kiện để áp dụng cho các ô từ A1 (0,0) đến D6 (5,3). Điều chỉnh các giá trị này để nhắm mục tiêu đến các ô khác nhau theo nhu cầu của bạn.
## Bước 5: Thêm Điều kiện Định dạng Có điều kiện
Bây giờ chúng ta đã thiết lập phạm vi, đã đến lúc xác định điều kiện cho định dạng của chúng ta. Trong trường hợp này, chúng ta sẽ định dạng các ô có giá trị từ 50 đến 100.
```csharp
// Thêm điều kiện.
int conditionIndex = fcs.AddCondition(FormatConditionType.CellValue, OperatorType.Between, "50", "100");
FormatCondition fc = fcs[conditionIndex];
```
Đoạn mã này tạo ra một điều kiện mới để kiểm tra xem giá trị ô có nằm trong khoảng từ 50 đến 100 hay không. Nếu có, định dạng mà chúng ta xác định tiếp theo sẽ được áp dụng.
## Bước 6: Xác định Kiểu cho Định dạng có Điều kiện
Với điều kiện đã thiết lập, giờ đây chúng ta có thể xác định kiểu sẽ được áp dụng cho các ô đáp ứng điều kiện.
```csharp
fc.Style.Pattern = BackgroundType.ReverseDiagonalStripe;
fc.Style.ForegroundColor = Color.FromArgb(255, 255, 0);
fc.Style.BackgroundColor = Color.FromArgb(0, 255, 255);
```
Trong ví dụ này, chúng tôi áp dụng mẫu sọc chéo ngược cho các ô. Màu nền trước được đặt thành màu vàng và màu nền được đặt thành màu lục lam. Hãy thoải mái tùy chỉnh các màu sắc và mẫu này để phù hợp với chủ đề bảng tính của bạn!
## Bước 7: Lưu sổ làm việc
Sau khi áp dụng định dạng, đã đến lúc lưu kiệt tác của chúng ta. Thao tác này sẽ tạo một tệp Excel với định dạng có điều kiện được chỉ định được áp dụng.
```csharp
workbook.Save(dataDir + "output.xlsx");
```
Đảm bảo điều chỉnh tên tệp và đường dẫn thư mục khi cần. Chạy ứng dụng của bạn và voilà! Tệp Excel đã định dạng của bạn đã sẵn sàng để thực hiện.
## Phần kết luận
Xin chúc mừng! Bạn đã thiết lập thành công một mẫu theo chương trình trong Excel bằng Aspose.Cells cho .NET. Với khả năng tự động định dạng, bạn có thể tiết kiệm rất nhiều thời gian và đảm bảo tính nhất quán trong bảng tính của mình. Cho dù bạn đang tạo báo cáo, phân tích dữ liệu hay chỉ muốn gây ấn tượng với sếp, kỹ năng này là một bổ sung có giá trị cho bộ công cụ của bạn. 
## Câu hỏi thường gặp
### Aspose.Cells là gì?
Aspose.Cells là một thư viện mạnh mẽ dành cho .NET cho phép các nhà phát triển tạo, thao tác và chuyển đổi các tệp Excel mà không cần cài đặt Microsoft Excel.
### Tôi có thể sử dụng Aspose.Cells miễn phí không?
 Có, Aspose.Cells cung cấp bản dùng thử miễn phí, cho phép bạn khám phá các tính năng của nó. Hãy xem thử[đây](https://releases.aspose.com/).
### Tôi có thể tạo những loại tệp Excel nào?
Bạn có thể tạo và thao tác nhiều định dạng Excel khác nhau, bao gồm XLS, XLSX, CSV, v.v. bằng Aspose.Cells.
### Có cách nào để nhận được hỗ trợ cho Aspose.Cells không?
 Chắc chắn rồi! Nếu bạn gặp bất kỳ vấn đề nào, bạn có thể tìm kiếm sự trợ giúp từ cộng đồng Aspose[đây](https://forum.aspose.com/c/cells/9).
### Làm thế nào tôi có thể áp dụng các mẫu khác nhau cho các phạm vi ô khác nhau?
 Bạn có thể xác định nhiều`CellArea` các đối tượng và áp dụng các quy tắc và kiểu định dạng có điều kiện khác nhau cho từng khu vực khi cần.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
