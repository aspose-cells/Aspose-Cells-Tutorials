---
"description": "Học cách thêm vòng cung vào bảng tính Excel bằng Aspose.Cells cho .NET. Làm theo hướng dẫn từng bước của chúng tôi để cải thiện thiết kế bảng tính của bạn."
"linktitle": "Thêm Arc vào trang tính trong Excel"
"second_title": "API xử lý Excel Aspose.Cells .NET"
"title": "Thêm Arc vào trang tính trong Excel"
"url": "/vi/net/excel-shapes-controls/add-arc-to-worksheet-excel/"
"weight": 16
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Thêm Arc vào trang tính trong Excel

## Giới thiệu
Tạo bảng tính Excel hấp dẫn về mặt hình ảnh là rất quan trọng đối với việc trình bày dữ liệu và thư viện Aspose.Cells cung cấp cho các nhà phát triển các công cụ mạnh mẽ để hoàn thành nhiệm vụ này. Một tính năng thú vị mà bạn có thể muốn kết hợp vào tài liệu Excel của mình là khả năng thêm hình dạng, chẳng hạn như cung tròn. Trong hướng dẫn này, chúng tôi sẽ hướng dẫn từng bước cách thêm cung tròn vào bảng tính Excel bằng Aspose.Cells cho .NET. Đến cuối bài viết này, bạn sẽ không chỉ học cách thêm cung tròn mà còn hiểu sâu hơn về cách quản lý hình dạng nói chung.
## Điều kiện tiên quyết
Trước khi đi sâu vào những phức tạp của việc thêm cung tròn vào bảng tính của bạn, điều quan trọng là phải đảm bảo bạn có một vài thứ tại chỗ. Sau đây là các điều kiện tiên quyết bạn cần để bắt đầu:
1. Visual Studio: Bạn cần cài đặt Visual Studio trên máy tính vì chúng ta sẽ sử dụng C# làm ngôn ngữ lập trình.
2. .NET Framework: Đảm bảo bạn đã cài đặt .NET Framework hoặc .NET Core. Aspose.Cells hỗ trợ cả hai.
3. Aspose.Cells cho .NET: Bạn phải có thư viện Aspose.Cells. Bạn có thể tải xuống từ [Tải xuống Aspose.Cells](https://releases.aspose.com/cells/net/) trang.
4. Hiểu biết cơ bản về C#: Sự quen thuộc với C# sẽ giúp bạn theo dõi các đoạn mã mà không gặp nhiều khó khăn.
## Nhập gói
Để bắt đầu làm việc với Aspose.Cells trong dự án của bạn, bạn cần nhập các gói cần thiết. Sau đây là cách thực hiện:
### Tạo một dự án mới
- Mở Visual Studio.
- Chọn "Tạo dự án mới".
- Chọn một mẫu hoạt động với .NET (như Console Application).
  
### Thêm tham chiếu Aspose.Cells
- Nhấp chuột phải vào dự án của bạn trong Solution Explorer.
- Chọn "Quản lý gói NuGet".
- Tìm kiếm “Aspose.Cells” và cài đặt.
Bây giờ bạn đã sẵn sàng để bắt đầu mã hóa phép cộng cung.
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
Sau đây là phân tích từng bước về mã minh họa cách thêm cung tròn vào bảng tính trong Excel.
## Bước 1: Thiết lập thư mục
Bước đầu tiên là thiết lập một thư mục nơi bạn sẽ lưu tệp Excel của mình. Điều này giúp quản lý các tệp đầu ra của bạn dễ dàng.
```csharp
string dataDir = "Your Document Directory";
// Tạo thư mục nếu thư mục đó chưa có.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Trong đoạn mã này, chúng tôi chỉ định đường dẫn đến thư mục tài liệu. Chúng tôi cũng kiểm tra xem thư mục có tồn tại không; nếu không, chúng tôi sẽ tạo thư mục đó. Điều này đặt nền tảng cho đầu ra của chúng tôi.
## Bước 2: Khởi tạo một Workbook
Tiếp theo, chúng ta hãy tạo một phiên bản sổ làm việc mới.
```csharp
// Tạo một Workbook mới.
Workbook excelbook = new Workbook();
```
Dòng này tạo một sổ làm việc Excel mới. Hãy coi đây như một khung vẽ trống nơi chúng ta có thể thêm hình dạng, dữ liệu và nhiều thứ khác.
## Bước 3: Thêm Hình vòng cung đầu tiên
Bây giờ, chúng ta hãy thêm hình cung đầu tiên vào bảng tính.
```csharp
// Thêm hình vòng cung.
Aspose.Cells.Drawing.ArcShape arc1 = excelbook.Worksheets[0].Shapes.AddArc(2, 0, 2, 0, 130, 130);
```
Ở đây, chúng ta đang thêm một cung tròn vào bảng tính đầu tiên. Các tham số xác định vị trí và kích thước của cung tròn: `(left, top, width, height, startAngle, endAngle)`. Giống như việc vẽ một cung tròn vậy!
## Bước 4: Tùy chỉnh Arc đầu tiên
Sau khi thêm vòng cung, bạn có thể muốn tùy chỉnh giao diện của vòng cung đó.
```csharp
// Đặt màu hình dạng tô
arc1.Fill.FillType = FillType.Solid;
arc1.Fill.SolidFill.Color = Color.Blue;
// Thiết lập vị trí của cung tròn.
arc1.Placement = PlacementType.FreeFloating;           
// Thiết lập độ dày của đường.
arc1.Line.Weight = 1;      
// Thiết lập kiểu nét gạch ngang của cung tròn.
arc1.Line.DashStyle = MsoLineDashStyle.Solid;
```
Trong phần này, chúng ta sẽ tùy chỉnh cung tròn. Chúng ta sẽ đặt loại tô của cung tròn thành màu đặc (màu xanh lam trong trường hợp này), xác định cách đặt cung tròn, thiết lập độ dày đường và chọn kiểu nét đứt. Về cơ bản, chúng ta sẽ tô điểm cho cung tròn để cung tròn trông hấp dẫn hơn về mặt thị giác!
## Bước 5: Thêm Hình vòng cung thứ hai
Hãy thêm một hình cung khác để cung cấp thêm bối cảnh.
```csharp
// Thêm một hình vòng cung khác.
Aspose.Cells.Drawing.ArcShape arc2 = excelbook.Worksheets[0].Shapes.AddArc(9, 0, 2, 0, 130, 130);
```
Tương tự như cung đầu tiên, chúng ta sẽ thêm cung thứ hai vào cùng một bảng tính. Tọa độ ở đây được dịch chuyển một chút để định vị nó theo cách khác.
## Bước 6: Tùy chỉnh vòng cung thứ hai
Giống như những gì chúng ta đã làm với phần đầu tiên, chúng ta cũng sẽ tùy chỉnh phần thứ hai.
```csharp
// Đặt màu đường kẻ
arc2.Line.FillType = FillType.Solid;
arc2.Line.SolidFill.Color = Color.Blue;
// Thiết lập vị trí của cung tròn.
arc2.Placement = PlacementType.FreeFloating;          
// Thiết lập độ dày của đường.
arc2.Line.Weight = 1;           
// Thiết lập kiểu nét gạch ngang của cung tròn.
arc2.Line.DashStyle = MsoLineDashStyle.Solid;
```
Ở đây, chúng tôi sẽ cung cấp cho cung thứ hai cùng kiểu dáng như cung đầu tiên. Bạn có thể thay đổi màu sắc hoặc kiểu dáng tùy theo ý muốn để tạo sự độc đáo hoặc mục đích theo chủ đề.
## Bước 7: Lưu sổ làm việc
Cuối cùng, đã đến lúc lưu bảng tính mới tạo cùng với các vòng cung.
```csharp
// Lưu tệp excel.
excelbook.Save(dataDir + "book1.out.xls");
```
Dòng này hoạt động giống như nhấn nút lưu. Chúng tôi đang lưu tác phẩm của mình vào vị trí đã chỉ định với tên tệp được chỉ định. Hãy đảm bảo kiểm tra thư mục của bạn để xem kiệt tác của bạn ở định dạng Excel!
## Phần kết luận
Trong hướng dẫn này, chúng tôi đã khám phá quy trình thêm hình vòng cung vào bảng tính Excel bằng Aspose.Cells for .NET. Thông qua hướng dẫn từng bước đơn giản, bạn đã học cách tạo sổ làm việc mới, thêm vòng cung, tùy chỉnh giao diện của chúng và lưu tài liệu của mình. Khả năng này không chỉ tăng cường sức hấp dẫn trực quan cho bảng tính của bạn mà còn giúp các bài thuyết trình dữ liệu của bạn có nhiều thông tin hơn. Cho dù bạn đang tạo biểu đồ, báo cáo hay chỉ đang thử nghiệm, việc sử dụng các hình dạng như vòng cung có thể thêm nét sáng tạo cho các dự án của bạn.
## Câu hỏi thường gặp
### Aspose.Cells là gì?
Aspose.Cells là một thư viện mạnh mẽ cho phép các nhà phát triển tạo, thao tác và chuyển đổi các tệp Excel theo chương trình mà không cần đến Microsoft Excel.
### Tôi có cần cài đặt Microsoft Excel để sử dụng Aspose.Cells không?
Không, Aspose.Cells hoàn toàn độc lập và không yêu cầu phải cài đặt Microsoft Excel.
### Tôi có thể dùng thử Aspose.Cells miễn phí không?
Có, bạn có thể dùng thử Aspose.Cells bằng cách sử dụng [Dùng thử miễn phí](https://releases.aspose.com/).
### Aspose.Cells hỗ trợ những ngôn ngữ lập trình nào?
Aspose.Cells hỗ trợ nhiều ngôn ngữ, bao gồm C#, VB.NET, v.v.
### Tôi có thể nhận hỗ trợ cho Aspose.Cells ở đâu?
Bạn có thể nhận được hỗ trợ thông qua [Diễn đàn Aspose](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}