---
title: Thêm Group Box vào trang tính trong Excel
linktitle: Thêm Group Box vào trang tính trong Excel
second_title: API xử lý Excel Aspose.Cells .NET
description: Tìm hiểu cách thêm hộp nhóm và nút radio trong Excel bằng Aspose.Cells cho .NET. Hướng dẫn từng bước dành cho nhà phát triển ở mọi cấp độ.
weight: 24
url: /vi/net/excel-shapes-controls/add-group-box-to-worksheet-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Thêm Group Box vào trang tính trong Excel

## Giới thiệu
Khi nói đến trình bày dữ liệu, Excel là vua. Thêm các thành phần tương tác như hộp nhóm có thể làm cho bảng tính của bạn hấp dẫn và thân thiện với người dùng hơn. Hôm nay, chúng ta sẽ khám phá thế giới của Aspose.Cells cho .NET, một thư viện mạnh mẽ giúp bạn thao tác các trang tính Excel một cách dễ dàng. Nhưng đừng lo lắng nếu bạn không phải là một phù thủy lập trình—hướng dẫn này chia nhỏ mọi thứ thành các bước đơn giản. Bạn đã sẵn sàng để nâng cao kỹ năng Excel của mình chưa? Hãy bắt đầu thôi!
## Điều kiện tiên quyết
Trước khi tìm hiểu về mã, bạn cần có một số thứ sau:
1. Visual Studio: Đảm bảo rằng bạn đã cài đặt Visual Studio trên máy của mình; đây là nơi bạn sẽ viết mã .NET.
2.  Aspose.Cells cho .NET: Bạn cần tải xuống thư viện này. Bạn có thể tìm thấy nó[đây](https://releases.aspose.com/cells/net/). 
3. Kiến thức cơ bản về C#: Mặc dù tôi sẽ giải thích mọi thứ theo từng bước, nhưng một chút hiểu biết về C# sẽ giúp bạn theo dõi dễ hơn.
## Nhập gói
Đối với bất kỳ dự án nào, trước tiên bạn cần nhập các gói cần thiết. Ở đây, Aspose.Cells sẽ là trọng tâm chính của bạn. Sau đây là cách thực hiện:
## Bước 1: Mở dự án của bạn trong Visual Studio
Khởi chạy Visual Studio và mở dự án hiện tại của bạn hoặc tạo một dự án mới. 
## Bước 2: Thêm tham chiếu đến Aspose.Cells
- Nhấp chuột phải vào dự án của bạn trong Solution Explorer.
- Chọn "Quản lý gói NuGet".
- Tìm kiếm "Aspose.Cells" và cài đặt nó. Điều này sẽ cho phép bạn sử dụng tất cả các lớp và phương thức được cung cấp bởi thư viện Aspose.Cells.
## Bước 3: Bao gồm sử dụng Chỉ thị
Ở đầu tệp C# của bạn, hãy bao gồm không gian tên Aspose.Cells:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
Điều này giúp bạn truy cập vào các lớp cần thiết để làm việc với các tệp Excel.
Bây giờ chúng ta đã thiết lập xong, hãy cùng đi sâu vào trọng tâm của hướng dẫn—thêm hộp nhóm có nút radio vào bảng tính Excel. Chúng tôi sẽ chia nhỏ quy trình này thành nhiều bước để rõ ràng hơn.
## Bước 1: Thiết lập thư mục tài liệu của bạn
Trước khi tạo bất kỳ tệp Excel nào, bạn cần xác định nơi bạn muốn lưu tệp đó. Hãy tạo một thư mục nếu nó chưa tồn tại.
```csharp
// Đường dẫn đến thư mục tài liệu
string dataDir = "Your Document Directory"; // Chỉ định đường dẫn mong muốn của bạn
// Tạo thư mục nếu thư mục đó chưa có.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Mã này kiểm tra xem thư mục lưu tệp Excel có tồn tại không. Nếu không, nó sẽ tạo một thư mục—giống như việc chuẩn bị không gian làm việc của bạn trước khi bắt tay vào dự án!
## Bước 2: Tạo một Workbook mới
Tiếp theo, bạn cần tạo một bảng tính Excel để thêm hộp nhóm vào đó.
```csharp
// Tạo một Workbook mới.
Workbook excelbook = new Workbook();
```
Dòng này khởi tạo một phiên bản mới của Workbook. Hãy nghĩ về điều này như việc mở một tệp Excel mới, trống sẵn sàng để sửa đổi.
## Bước 3: Thêm hộp nhóm
Bây giờ, chúng ta hãy thêm hộp nhóm đó. 
```csharp
// Thêm hộp nhóm vào bảng tính đầu tiên.
GroupBox box = excelbook.Worksheets[0].Shapes.AddGroupBox(1, 0, 1, 0, 300, 250);
```
Ở đây, bạn đang thêm một hộp nhóm tại tọa độ được chỉ định trong bảng tính đầu tiên. Các tham số xác định vị trí và kích thước của hộp, giống như việc định vị đồ đạc trong phòng!
## Bước 4: Đặt tiêu đề cho hộp nhóm
Bây giờ, chúng ta hãy đặt tên cho hộp nhóm của bạn nhé!
```csharp
// Đặt tiêu đề cho hộp nhóm.
box.Text = "Age Groups";
box.Placement = PlacementType.FreeFloating;
```
 Chuỗi “Nhóm tuổi” thiết lập nhãn xuất hiện trên hộp nhóm. Thiết lập`Placement` BẰNG`FreeFloating` cho phép hộp có thể di chuyển được—tính linh hoạt là yếu tố quan trọng!
## Bước 5: Tạo hộp nhóm 2 chiều
Mặc dù 3D nghe có vẻ lạ mắt, nhưng chúng tôi sẽ hướng đến giao diện cổ điển.
```csharp
// Làm cho nó thành hộp 2 chiều.
box.Shadow = false;
```
Mã này loại bỏ hiệu ứng đổ bóng, làm cho hộp trông phẳng hơn—giống như một tờ giấy đơn giản!
## Bước 6: Thêm nút radio
Hãy làm mọi thứ trở nên thú vị hơn bằng cách thêm một số nút radio để người dùng nhập dữ liệu.
## Bước 6.1: Thêm nút radio đầu tiên
```csharp
// Thêm nút radio.
Aspose.Cells.Drawing.RadioButton radio1 = excelbook.Worksheets[0].Shapes.AddRadioButton(3, 0, 2, 0, 30, 110);
// Đặt chuỗi văn bản của nó.
radio1.Text = "20-29";
// Đặt ô A1 làm ô được liên kết cho nút radio.
radio1.LinkedCell = "A1";
```
Bạn tạo một nút radio cho nhóm tuổi 20-29, liên kết nó với ô A1 trong bảng tính. Điều này có nghĩa là khi nút này được chọn, ô A1 sẽ phản ánh lựa chọn đó!
## Bước 6.2: Tùy chỉnh nút radio đầu tiên
Bây giờ chúng ta hãy thêm chút phong cách cho nó.
```csharp
// Làm cho nút radio có dạng 3 chiều.
radio1.Shadow = true;
// Đặt trọng lượng của nút radio.
radio1.Line.Weight = 4;
// Đặt kiểu gạch ngang của nút radio.
radio1.Line.DashStyle = MsoLineDashStyle.Solid;
```
Bằng cách thêm bóng đổ và điều chỉnh kiểu đường kẻ, chúng tôi sẽ tăng cường khả năng hiển thị của nút. Giống như thêm đồ trang trí để làm cho nó nổi bật trên trang!
## Bước 6.3: Lặp lại cho nhiều nút radio hơn
Lặp lại quy trình này cho các nhóm tuổi khác:
```csharp
// Nút radio thứ hai
Aspose.Cells.Drawing.RadioButton radio2 = excelbook.Worksheets[0].Shapes.AddRadioButton(6, 0, 2, 0, 30, 110);
radio2.Text = "30-39";
radio2.LinkedCell = "A1";
radio2.Shadow = true;
radio2.Line.Weight = 4;
radio2.Line.DashStyle = MsoLineDashStyle.Solid;
// Nút radio thứ ba
Aspose.Cells.Drawing.RadioButton radio3 = excelbook.Worksheets[0].Shapes.AddRadioButton(9, 0, 2, 0, 30, 110);
radio3.Text = "40-49";
radio3.LinkedCell = "A1";
radio3.Shadow = true;
radio3.Line.Weight = 4;
radio3.Line.DashStyle = MsoLineDashStyle.Solid;
```
Mỗi nút radio đóng vai trò là lựa chọn cho các độ tuổi khác nhau, được liên kết trở lại cùng một ô A1. Điều này cho phép thực hiện quy trình lựa chọn đơn giản, thân thiện với người dùng.
## Bước 7: Nhóm các hình dạng
Khi mọi thứ đã vào đúng vị trí, hãy sắp xếp mọi thứ lại bằng cách nhóm các hình dạng lại với nhau. 
```csharp
// Nhận các hình dạng.
Aspose.Cells.Drawing.Shape[] shapeobjects = new Shape[] { box, radio1, radio2, radio3 };
// Nhóm các hình dạng lại với nhau.
Aspose.Cells.Drawing.GroupShape group = excelbook.Worksheets[0].Shapes.Group(shapeobjects);
```
Bước này kết hợp mọi thứ thành một khối thống nhất. Giống như việc đóng khung bộ sưu tập nghệ thuật của bạn vậy—nó gắn kết chúng lại với nhau một cách tuyệt đẹp!
## Bước 8: Lưu tệp Excel
Cuối cùng, hãy cùng lưu lại kiệt tác của chúng ta!
```csharp
// Lưu tệp excel.
excelbook.Save(dataDir + "book1.out.xls");
```
Dòng mã này ghi các thay đổi của bạn vào một tệp Excel mới có tên "book1.out.xls" trong thư mục bạn chỉ định. Giống như việc niêm phong một phong bì, công việc của bạn hiện được lưu trữ an toàn!
## Phần kết luận
Và đó là hướng dẫn đầy đủ về cách thêm hộp nhóm và nút radio vào bảng tính Excel bằng Aspose.Cells cho .NET! Với mỗi bước, bạn đã học cách thao tác Excel theo chương trình, mở ra cánh cửa đến vô số khả năng tùy chỉnh báo cáo, hình ảnh hóa dữ liệu, v.v. Vẻ đẹp của lập trình là bạn có thể tự động hóa các tác vụ và tạo giao diện thân thiện với người dùng một cách tương đối dễ dàng—hãy tưởng tượng tiềm năng!
## Câu hỏi thường gặp
### Aspose.Cells là gì?
Aspose.Cells là thư viện .NET dùng để quản lý các tệp Excel, cho phép thực hiện các tác vụ như đọc, viết và thao tác bảng tính theo chương trình.
### Tôi có cần kinh nghiệm lập trình để sử dụng Aspose.Cells không?
Mặc dù một số kiến thức về lập trình có thể hữu ích, nhưng hướng dẫn này sẽ hướng dẫn bạn những điều cơ bản, giúp người mới bắt đầu dễ hiểu!
### Tôi có thể tùy chỉnh giao diện của hộp nhóm và nút không?
Chắc chắn rồi! Aspose.Cells cung cấp nhiều tùy chọn để tạo kiểu cho hình dạng, bao gồm màu sắc, kích thước và hiệu ứng 3D.
### Có bản dùng thử miễn phí cho Aspose.Cells không?
 Vâng! Bạn có thể dùng thử miễn phí bằng cách truy cập[Dùng thử miễn phí Aspose](https://releases.aspose.com/).
### Tôi có thể tìm thêm tài nguyên hoặc hỗ trợ cho Aspose.Cells ở đâu?
 Các[Diễn đàn hỗ trợ Aspose](https://forum.aspose.com/c/cells/9) là nơi tuyệt vời để tìm kiếm sự giúp đỡ và chia sẻ kiến thức với cộng đồng.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
