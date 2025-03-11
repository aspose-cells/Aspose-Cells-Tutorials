---
title: Thêm điều khiển hình chữ nhật vào trang tính trong Excel
linktitle: Thêm điều khiển hình chữ nhật vào trang tính trong Excel
second_title: API xử lý Excel Aspose.Cells .NET
description: Tìm hiểu cách thêm điều khiển hình chữ nhật vào bảng tính Excel bằng Aspose.Cells cho .NET với hướng dẫn chi tiết từng bước.
weight: 25
url: /vi/net/excel-shapes-controls/add-rectangle-control-to-worksheet-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Thêm điều khiển hình chữ nhật vào trang tính trong Excel

## Giới thiệu
Khi nói đến việc tự động hóa các tác vụ Excel, Aspose.Cells for .NET là một công cụ mạnh mẽ có thể giúp bạn đạt được nhiều mục tiêu khác nhau, một trong số đó là thêm các hình dạng như hình chữ nhật vào bảng tính của bạn. Trong hướng dẫn này, chúng ta sẽ khám phá cách thêm điều khiển hình chữ nhật vào bảng tính Excel bằng Aspose.Cells for .NET. Cuối cùng, bạn sẽ có thể tạo, tùy chỉnh và lưu bảng tính có điều khiển hình chữ nhật được nhúng trong đó.
Nhưng trước khi đi sâu hơn, chúng ta hãy nói về các điều kiện tiên quyết.
## Điều kiện tiên quyết
Để thực hiện theo hướng dẫn này, hãy đảm bảo bạn có đủ các điều kiện tiên quyết sau:
1.  Thư viện Aspose.Cells cho .NET: Nếu bạn chưa có,[tải xuống thư viện](https://releases.aspose.com/cells/net/) hoặc cài đặt bằng NuGet trong Visual Studio.
2. .NET Framework: Bạn cần thiết lập môi trường phát triển .NET trên máy của mình.
3. Kiến thức cơ bản về C#: Mặc dù chúng tôi sẽ hướng dẫn bạn từng bước, nhưng việc quen thuộc cơ bản với C# và lập trình hướng đối tượng sẽ rất có lợi.
4.  Giấy phép: Sử dụng Aspose.Cells ở chế độ đánh giá hoạt động tốt cho các tác vụ cơ bản, nhưng để có đầy đủ chức năng, hãy cân nhắc sử dụng[giấy phép tạm thời](https://purchase.aspose.com/temporary-license/)hoặc mua một cái từ[đây](https://purchase.aspose.com/buy).
Bây giờ, chúng ta hãy cùng tìm hiểu mã nhé!
## Nhập gói
Để bắt đầu với Aspose.Cells, hãy đảm bảo bạn đã nhập các không gian tên cần thiết vào dự án của mình. Các lần nhập này sẽ cho phép truy cập vào nhiều lớp và phương thức khác nhau mà bạn cần để tương tác với các tệp Excel.
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
Những dòng này đảm bảo rằng dự án của bạn có thể tương tác với các thư mục tệp (`System.IO`), sổ làm việc Excel (`Aspose.Cells`), và vẽ hình dạng (`Aspose.Cells.Drawing`).
Bây giờ, chúng ta hãy chia nhỏ quy trình thành các bước đơn giản để bạn có thể dễ dàng làm theo và áp dụng vào dự án của mình.
## Bước 1: Thiết lập đường dẫn thư mục
Điều đầu tiên bạn cần làm là xác định thư mục nơi tệp Excel của bạn sẽ được lưu. Bước này đảm bảo rằng dự án của bạn biết nơi tạo và lưu trữ tệp đầu ra.
### Xác định thư mục dữ liệu
```csharp
// Đường dẫn đến thư mục tài liệu.
string dataDir = "Your Document Directory";
```
 Tại đây, bạn chỉ định đường dẫn thư mục nơi tệp Excel sẽ được lưu trữ. Bạn có thể thay thế`"Your Document Directory"` bằng đường dẫn thực tế trên máy của bạn hoặc tạo thư mục động nếu thư mục không tồn tại.
### Kiểm tra và tạo thư mục
```csharp
// Tạo thư mục nếu thư mục đó chưa có.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Khối này kiểm tra xem thư mục có tồn tại không. Nếu không, nó sẽ tạo một thư mục. Hãy nghĩ về nó giống như việc chuẩn bị tủ hồ sơ trước khi bạn lưu trữ bất kỳ tài liệu nào.
## Bước 2: Khởi tạo một Workbook mới
 Trong bước này, bạn tạo một bảng tính Excel mới bằng cách sử dụng`Aspose.Cells.Workbook` lớp. Đây sẽ là nơi chứa bảng tính và hình dạng của bạn.
```csharp
// Tạo một Workbook mới.
Workbook excelbook = new Workbook();
```
 Bằng cách gọi`Workbook` constructor, bây giờ bạn đã có một bảng tính Excel trống sẵn sàng để tùy chỉnh.
## Bước 3: Thêm điều khiển hình chữ nhật
Đây chính là nơi phép thuật xảy ra. Bạn sẽ thêm hình chữ nhật vào trang tính đầu tiên của sổ làm việc.
```csharp
// Thêm điều khiển hình chữ nhật.
Aspose.Cells.Drawing.RectangleShape rectangle = excelbook.Worksheets[0].Shapes.AddRectangle(3, 0, 2, 0, 70, 130);
```
Chúng ta hãy phân tích điều này:
- `excelbook.Worksheets[0]`: Thao tác này sẽ truy cập vào trang tính đầu tiên trong sổ làm việc của bạn.
- `.Shapes.AddRectangle(3, 0, 2, 0, 70, 130)`: Thao tác này sẽ thêm hình chữ nhật vào trang tính. Các tham số ở đây xác định vị trí (hàng và cột), cũng như chiều rộng và chiều cao của hình chữ nhật.
## Bước 4: Tùy chỉnh hình chữ nhật
Chỉ thêm một hình chữ nhật là không đủ—bạn sẽ muốn tùy chỉnh nó. Trong bước này, chúng ta sẽ thiết lập vị trí, độ dày đường và kiểu nét đứt của hình chữ nhật.
### Thiết lập vị trí
```csharp
// Thiết lập vị trí của hình chữ nhật.
rectangle.Placement = PlacementType.FreeFloating;
```
Điều này chỉ rõ rằng hình chữ nhật là hình nổi tự do, nghĩa là nó sẽ không bị giới hạn bởi kích thước ô.
### Thiết lập độ dày của đường
```csharp
// Thiết lập độ dày của đường.
rectangle.Line.Weight = 4;
```
Ở đây, chúng ta đặt độ dày của đường kẻ hình chữ nhật là 4 điểm. Số càng cao, đường kẻ càng dày.
### Thiết lập kiểu Dash
```csharp
// Đặt kiểu gạch ngang cho hình chữ nhật.
rectangle.Line.DashStyle = MsoLineDashStyle.Solid;
```
 Dòng này thiết lập kiểu nét đứt của đường viền hình chữ nhật thành nét liền. Bạn có thể thử nghiệm với các kiểu khác nhau như`Dash` hoặc`Dot` tùy thuộc vào yêu cầu của bạn.
## Bước 5: Lưu sổ làm việc
Sau khi thêm và tùy chỉnh hình chữ nhật, bước cuối cùng là lưu sổ làm việc vào thư mục đã chỉ định.
```csharp
// Lưu tệp excel.
excelbook.Save(dataDir + "book1.out.xls");
```
 Điều này lưu sổ làm việc dưới dạng`.xls` tập tin trong thư mục bạn đã xác định trước đó. Bạn có thể sửa đổi định dạng tập tin bằng cách thay đổi phần mở rộng, chẳng hạn như`.xlsx` nếu bạn thích định dạng Excel mới hơn.
## Phần kết luận
Và bạn đã có nó! Thêm điều khiển hình chữ nhật vào bảng tính Excel bằng Aspose.Cells cho .NET là một quá trình đơn giản khi bạn chia nhỏ từng bước. Cho dù bạn cần thêm hình dạng để thu hút thị giác, làm nổi bật các phần dữ liệu hay tùy chỉnh báo cáo, Aspose.Cells cung cấp cho bạn sự linh hoạt để thực hiện theo chương trình.
Hướng dẫn này sẽ cung cấp cho bạn mọi kiến thức cần thiết để bắt đầu thêm hình dạng như hình chữ nhật vào bảng tính Excel của bạn bằng Aspose.Cells. Bây giờ là lúc thử nghiệm và xem bạn có thể đạt được những gì khác với thư viện mạnh mẽ này!
## Câu hỏi thường gặp
### Tôi có thể thêm các hình dạng khác như hình tròn hoặc đường thẳng bằng Aspose.Cells cho .NET không?  
Có, Aspose.Cells cho phép bạn thêm nhiều hình dạng khác nhau, bao gồm hình tròn, đường thẳng, mũi tên, v.v.
### Tôi có thể thiết lập những thuộc tính nào khác cho điều khiển hình chữ nhật?  
Bạn có thể tùy chỉnh màu tô, màu đường kẻ, độ trong suốt và thậm chí thêm văn bản vào hình chữ nhật.
### Aspose.Cells có tương thích với .NET Core không?  
Có, Aspose.Cells hỗ trợ .NET Core cũng như .NET Framework và các nền tảng khác dựa trên .NET.
### Tôi có thể định vị hình chữ nhật theo một ô cụ thể không?  
 Có, bạn có thể đặt hình chữ nhật trong các hàng và cột cụ thể hoặc sử dụng`PlacementType` để kiểm soát cách neo giữ.
### Có bản dùng thử miễn phí cho Aspose.Cells không?  
 Vâng, bạn có thể nhận được một[dùng thử miễn phí](https://releases.aspose.com/) từ trang web để kiểm tra các tính năng của thư viện trước khi mua.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
