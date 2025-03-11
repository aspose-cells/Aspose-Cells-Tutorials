---
title: Thêm Arc Control với Điểm Kết Nối
linktitle: Thêm Arc Control với Điểm Kết Nối
second_title: API xử lý Excel Aspose.Cells .NET
description: Khám phá cách thêm điều khiển vòng cung với các điểm kết nối bằng Aspose.Cells cho .NET trong hướng dẫn chi tiết này.
weight: 27
url: /vi/net/excel-shapes-controls/add-arc-control-with-connection-points/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Thêm Arc Control với Điểm Kết Nối

## Giới thiệu
Khi nói đến việc tạo báo cáo Excel hấp dẫn về mặt thị giác, hình minh họa đóng vai trò quan trọng. Cho dù bạn đang soạn thảo báo cáo tài chính hay phân tích dự án, việc sử dụng các hình dạng như cung tròn có thể tăng thêm chiều sâu và độ rõ nét cho bản trình bày dữ liệu của bạn. Hôm nay, chúng ta sẽ đi sâu vào cách sử dụng Aspose.Cells cho .NET để thêm các điều khiển cung tròn có điểm kết nối vào bảng tính Excel của bạn. Vì vậy, nếu bạn từng tự hỏi làm thế nào để làm cho bảng tính của mình hấp dẫn hơn hoặc làm cho dữ liệu của bạn trở nên hấp dẫn hơn, hãy đọc tiếp!
## Điều kiện tiên quyết
Trước khi bắt đầu vào phần thú vị của việc lập trình, hãy đảm bảo rằng bạn đã thiết lập xong mọi thứ. Sau đây là những gì bạn cần:
1. .NET Framework: Đảm bảo bạn đã cài đặt phiên bản tương thích. Aspose.Cells hoạt động với nhiều phiên bản, bao gồm .NET Core.
2.  Aspose.Cells cho .NET: Bạn sẽ cần tải xuống và cài đặt thư viện Aspose.Cells. Bạn có thể dễ dàng lấy nó từ[liên kết tải xuống](https://releases.aspose.com/cells/net/).
3. Một IDE tốt: Visual Studio, người bạn đồng hành trung thành của bất kỳ nhà phát triển .NET nào, sẽ giúp hợp lý hóa trải nghiệm lập trình của bạn.
4. Kiến thức cơ bản về C#: Nếu bạn biết cách sử dụng C#, bạn sẽ thấy hướng dẫn này rất dễ hiểu.
5. Truy cập vào thư mục tài liệu của bạn: Biết nơi bạn sẽ lưu các tệp Excel của mình. Điều này rất cần thiết để sắp xếp đầu ra của bạn một cách hiệu quả.
## Nhập gói
Bước tiếp theo là đảm bảo bạn đã nhập đúng các gói vào dự án của mình. Aspose.Cells cho .NET có nhiều chức năng khác nhau, vì vậy chúng tôi sẽ giữ cho nó đơn giản. Sau đây là những gì bạn cần đưa vào:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
Các không gian tên này sẽ cung cấp cho bạn quyền truy cập vào tất cả các tính năng vẽ và chức năng quản lý ô mà bạn sẽ sử dụng trong hướng dẫn này.
## Bước 1: Thiết lập thư mục tài liệu của bạn
Trước tiên, hãy tạo một thư mục nơi bạn sẽ lưu các tệp Excel mới sáng bóng đó. Đây là cách chúng tôi thực hiện:
```csharp
string dataDir = "Your Document Directory";
// Tạo thư mục nếu thư mục đó chưa có.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Đoạn mã này kiểm tra xem thư mục bạn chỉ định có tồn tại không. Nếu không, nó sẽ tạo một thư mục. Đơn giản, phải không? Luôn tốt khi có một vị trí cụ thể cho các tệp của bạn để tránh lộn xộn.
## Bước 2: Khởi tạo một Workbook
Bây giờ chúng ta đã có thư mục sẵn sàng, hãy tạo một bảng tính Excel mới.
```csharp
Workbook excelbook = new Workbook();
```
 Bằng cách gọi`Workbook` constructor, về cơ bản bạn đang nói, "Này, hãy bắt đầu một tệp Excel mới!" Đây sẽ là khung vẽ cho tất cả các hình dạng và dữ liệu của bạn.
## Bước 3: Thêm Hình vòng cung đầu tiên
Đây là nơi niềm vui bắt đầu! Chúng ta hãy thêm hình vòng cung đầu tiên.
```csharp
Aspose.Cells.Drawing.ArcShape arc1 = excelbook.Worksheets[0].Shapes.AddArc(2, 0, 2, 0, 130, 130);
```
Dòng mã này thêm hình cung vào bảng tính đầu tiên. Các tham số chỉ định tọa độ của cung và các góc xác định độ cong của cung. 
## Bước 4: Tùy chỉnh giao diện của Arc
Một hình cung trống giống như một bức tranh không có sơn—nó cần một chút điểm nhấn!
### Đặt màu tô vòng cung
```csharp
arc1.Fill.FillType = FillType.Solid;
arc1.Fill.SolidFill.Color = Color.Blue;
```
Điều này làm cho vòng cung có màu xanh lam đặc. Bạn có thể thay đổi màu sắc thành bất kỳ sắc thái nào bạn thích bằng cách hoán đổi`Color.Blue` để có màu khác.
### Đặt vị trí vòng cung
```csharp
arc1.Placement = PlacementType.FreeFloating;
```
Thiết lập vị trí thành "FreeFloating" cho phép vòng cung di chuyển độc lập với ranh giới ô, mang lại cho bạn sự linh hoạt trong việc định vị.
### Điều chỉnh độ dày và kiểu đường kẻ
```csharp
arc1.Line.Weight = 1;      
arc1.Line.DashStyle = MsoLineDashStyle.Solid;
```
Tại đây, bạn xác định độ đậm nhạt và kiểu dáng của đường, làm cho nó nổi bật hơn và hấp dẫn hơn về mặt thị giác.
## Bước 5: Thêm một hình vòng cung khác
Tại sao lại dừng lại ở một hình? Hãy thêm một hình cung khác để làm phong phú thêm hình ảnh Excel của chúng ta.
```csharp
Aspose.Cells.Drawing.ArcShape arc2 = excelbook.Worksheets[0].Shapes.AddArc(9, 0, 2, 0, 130, 130);
```
Giống như cung đầu tiên, cung này được thêm vào ở một vị trí khác—đây chính là nơi phép thuật thiết kế diễn ra!
## Bước 6: Tùy chỉnh vòng cung thứ hai
Hãy cùng thêm chút cá tính cho phần thứ hai nhé!
### Thay đổi màu đường cong
```csharp
arc2.Line.FillType = FillType.Solid;
arc2.Line.SolidFill.Color = Color.Blue;
```
Chúng tôi giữ nguyên màu xanh lam, nhưng bạn luôn có thể kết hợp để xem màu nào phù hợp nhất với thiết kế của mình!
### Thiết lập Thuộc tính Tương tự như Arc Đầu tiên
Hãy đảm bảo sao chép những lựa chọn thẩm mỹ đó:
```csharp
arc2.Placement = PlacementType.FreeFloating;
arc2.Line.Weight = 1;           
arc2.Line.DashStyle = MsoLineDashStyle.Solid;
```
Ở đây, bạn chỉ cần đảm bảo rằng cung thứ hai khớp với cung đầu tiên, tạo nên giao diện thống nhất trong toàn bộ bảng tính của bạn.
## Bước 7: Lưu sổ làm việc của bạn
Không có kiệt tác nào hoàn thiện nếu không được lưu lại, đúng không? Đã đến lúc viết các cung của bạn vào tệp Excel.
```csharp
excelbook.Save(dataDir + "book1.out.xls");
```
Dòng này lưu các cung mới tạo của bạn vào tệp Excel có tên "book1.out.xls" trong thư mục được chỉ định.
## Phần kết luận
Xin chúc mừng! Bạn vừa nắm vững những điều cơ bản về cách thêm điều khiển vòng cung với các điểm kết nối vào bảng tính Excel của mình bằng Aspose.Cells for .NET. Chức năng này không chỉ làm đẹp bảng tính của bạn mà còn có thể giúp dữ liệu phức tạp dễ tiêu hóa hơn. Cho dù bạn là một nhà phát triển dày dạn kinh nghiệm hay chỉ mới bắt đầu, các thành phần trực quan này có thể biến báo cáo của bạn từ nhạt nhẽo thành hoành tráng.
## Câu hỏi thường gặp
### Aspose.Cells là gì?
Aspose.Cells là một thư viện .NET mạnh mẽ cho phép các nhà phát triển tạo và thao tác các tệp Excel theo chương trình.
### Tôi có thể sử dụng Aspose.Cells miễn phí không?
 Có! Bạn có thể dùng thử miễn phí. Truy cập[liên kết này](https://releases.aspose.com/) để bắt đầu.
### Làm thế nào để thêm các hình dạng khác ngoài hình cung?
Bạn có thể sử dụng các lớp khác nhau có sẵn trong không gian tên Aspose.Cells.Drawing để thêm nhiều hình dạng khác nhau như hình chữ nhật, hình tròn, v.v.
### Tôi có thể tạo loại tệp nào bằng Aspose.Cells?
Bạn có thể tạo và thao tác nhiều định dạng Excel khác nhau bao gồm XLS, XLSX, CSV, v.v.
### Có hỗ trợ kỹ thuật cho Aspose.Cells không?
 Chắc chắn rồi! Bạn có thể truy cập[Diễn đàn hỗ trợ Aspose](https://forum.aspose.com/c/cells/9) để được hỗ trợ.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
