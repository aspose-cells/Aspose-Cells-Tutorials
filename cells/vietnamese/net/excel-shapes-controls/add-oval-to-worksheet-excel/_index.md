---
title: Thêm Oval vào trang tính trong Excel
linktitle: Thêm Oval vào trang tính trong Excel
second_title: API xử lý Excel Aspose.Cells .NET
description: Tìm hiểu cách thêm hình bầu dục vào bảng tính Excel bằng Aspose.Cells cho .NET. Hướng dẫn từng bước có giải thích mã chi tiết.
weight: 17
url: /vi/net/excel-shapes-controls/add-oval-to-worksheet-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Thêm Oval vào trang tính trong Excel

## Giới thiệu
Tạo các tệp Excel tuyệt đẹp và tương tác có thể liên quan đến nhiều thứ hơn là chỉ các con số và công thức. Các hình dạng như hình bầu dục có thể tăng thêm sức hấp dẫn về mặt thị giác hoặc cung cấp các thành phần chức năng trong bảng tính của bạn. Trong hướng dẫn này, chúng ta sẽ khám phá cách sử dụng Aspose.Cells cho .NET để thêm hình bầu dục vào bảng tính Excel theo chương trình. Cho dù bạn đang muốn thêm một chút phong cách hay chức năng, chúng tôi đều có hướng dẫn từng bước chi tiết cho bạn.
## Điều kiện tiên quyết
Trước khi tìm hiểu về mã, bạn cần chuẩn bị một số điều sau:
1.  Thư viện Aspose.Cells cho .NET: Bạn có thể tải xuống từ[đây](https://releases.aspose.com/cells/net/) hoặc cài đặt bằng NuGet trong Visual Studio.
2. Môi trường phát triển: AC# IDE như Visual Studio.
3. Hiểu biết cơ bản về C#: Bạn nên quen thuộc với các khái niệm lập trình cơ bản trong C#.
 Ngoài ra, hãy nhớ thiết lập dự án của bạn bằng cách cài đặt thư viện Aspose.Cells cho .NET. Nếu bạn chưa có giấy phép, bạn có thể đăng ký[giấy phép tạm thời](https://purchase.aspose.com/temporary-license/) hoặc sử dụng[dùng thử miễn phí](https://releases.aspose.com/) phiên bản.
## Nhập gói
Trước khi viết bất kỳ mã nào, hãy đảm bảo bạn đã bao gồm các không gian tên bắt buộc. Sau đây là đoạn mã C# để đảm bảo bạn đang sử dụng đúng thư viện:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
## Bước 1: Thiết lập thư mục của bạn
Bước đầu tiên để thêm hình bầu dục vào bảng tính Excel là chỉ định nơi tệp Excel của bạn sẽ được lưu. Hãy xác định đường dẫn thư mục và đảm bảo thư mục tồn tại trước khi lưu công việc của chúng ta.

Chúng tôi sẽ tạo một đường dẫn thư mục và xác minh xem nó có tồn tại không. Nếu thư mục không tồn tại, nó sẽ được tạo.
```csharp
// Đường dẫn đến thư mục tài liệu.
string dataDir = "Your Document Directory";
// Tạo thư mục nếu thư mục đó chưa có.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Bước này rất quan trọng vì nó đảm bảo tệp của bạn được lưu ở đúng vị trí và bạn không gặp phải sự cố về đường dẫn tệp sau này.
## Bước 2: Khởi tạo một Workbook mới
Tiếp theo, chúng ta cần tạo một sổ làm việc mới trong đó chúng ta sẽ thêm các hình bầu dục của mình. Sổ làm việc này đại diện cho một tệp Excel và chúng ta có thể thêm nội dung hoặc hình dạng vào đó.

 Trong bước này, chúng tôi khởi tạo một cái mới`Workbook` đối tượng sẽ đóng vai trò là nơi chứa tệp Excel của chúng ta.
```csharp
// Tạo một Workbook mới.
Workbook excelbook = new Workbook();
```
## Bước 3: Thêm hình bầu dục đầu tiên
Bây giờ đến phần thú vị—thêm hình bầu dục vào bảng tính. Hình bầu dục này có thể biểu diễn một thành phần trực quan như nút hoặc điểm nổi bật. Chúng ta sẽ bắt đầu bằng cách thêm hình bầu dục đầu tiên vào bảng tính đầu tiên của sổ làm việc.

 Ở đây, chúng tôi sử dụng`Shapes.AddOval()` phương pháp tạo hình bầu dục trên bảng tính tại một hàng và cột cụ thể.
```csharp
// Thêm hình bầu dục.
Aspose.Cells.Drawing.Oval oval1 = excelbook.Worksheets[0].Shapes.AddOval(2, 0, 2, 0, 130, 160);
```
 Các thông số bên trong`AddOval()` như sau:
- Hai số đầu tiên biểu thị hàng và cột ở góc trên bên trái của hình bầu dục.
- Hai số tiếp theo biểu thị chiều cao và chiều rộng của hình bầu dục.
## Bước 4: Thiết lập vị trí và kiểu dáng của hình bầu dục
 Sau khi hình bầu dục được tạo, chúng ta có thể thiết lập vị trí, độ dày đường nét và kiểu nét gạch ngang của nó.`Placement` Thuộc tính này xác định cách hình bầu dục hoạt động khi bạn thay đổi kích thước hoặc di chuyển các ô trong bảng tính.

Chúng tôi làm cho hình bầu dục nổi tự do và điều chỉnh hình dáng của nó.
```csharp
// Thiết lập vị trí của hình bầu dục.
oval1.Placement = PlacementType.FreeFloating;
// Thiết lập độ dày của đường.
oval1.Line.Weight = 1;
// Thiết lập kiểu nét gạch ngang của hình bầu dục.
oval1.Line.DashStyle = MsoLineDashStyle.Solid;
```
Điều này cho phép hình bầu dục di chuyển tự do trong bảng tính và độ đậm nét cũng như kiểu dáng của nó được thiết lập để có sự nhất quán về mặt thị giác.
## Bước 5: Thêm một hình bầu dục (hình tròn) khác
Tại sao lại dừng lại ở một hình? Ở bước này, chúng ta sẽ thêm một hình bầu dục khác, lần này tạo ra một hình tròn hoàn hảo bằng cách làm cho chiều cao và chiều rộng bằng nhau.

Chúng ta tạo một hình bầu dục khác, đặt nó ở một vị trí khác và đảm bảo nó có hình tròn bằng cách thiết lập chiều cao và chiều rộng bằng nhau.
```csharp
// Thêm một hình bầu dục (hình tròn) nữa.
Aspose.Cells.Drawing.Oval oval2 = excelbook.Worksheets[0].Shapes.AddOval(9, 0, 2, 15, 130, 130);
```
## Bước 6: Tạo kiểu cho hình bầu dục thứ hai
Giống như trước, chúng ta sẽ điều chỉnh vị trí, độ đậm và kiểu nét gạch ngang của hình bầu dục (hoặc hình tròn) thứ hai này.

Chúng tôi áp dụng các đặc tính tương tự cho hình bầu dục thứ hai để phù hợp với phong cách của hình đầu tiên.
```csharp
// Thiết lập vị trí của hình bầu dục.
oval2.Placement = PlacementType.FreeFloating;
// Thiết lập độ dày của đường.
oval2.Line.Weight = 1;
// Thiết lập kiểu nét gạch ngang của hình bầu dục.
oval2.Line.DashStyle = MsoLineDashStyle.Solid;
```
## Bước 7: Lưu sổ làm việc
Cuối cùng, chúng ta cần lưu sổ làm việc với các hình bầu dục mà chúng ta vừa thêm vào. Việc lưu tệp đảm bảo rằng tất cả các thay đổi của chúng ta đều được lưu trữ.

Chúng tôi lưu sổ làm việc vào đường dẫn thư mục đã xác định trước đó.
```csharp
// Lưu tệp excel.
excelbook.Save(dataDir + "book1.out.xls");
```
Và thế là xong! Bạn đã thêm hình bầu dục vào bảng tính Excel thành công và lưu tệp.
## Phần kết luận
Thêm các hình dạng như hình bầu dục vào bảng tính Excel bằng Aspose.Cells cho .NET không chỉ đơn giản mà còn là cách thú vị để nâng cao bảng tính của bạn bằng các thành phần trực quan bổ sung. Cho dù là vì mục đích thiết kế hay thêm các thành phần có thể nhấp, hình dạng có thể đóng vai trò quan trọng trong cách các tệp Excel của bạn trông như thế nào và hoạt động ra sao. Vì vậy, lần tới khi bạn làm việc trên một dự án đòi hỏi các bảng tính Excel tương tác hoặc hấp dẫn về mặt trực quan, bạn sẽ biết chính xác cách thêm các hình bầu dục hoàn hảo đó!
## Câu hỏi thường gặp
### Tôi có thể thêm các hình dạng khác như hình chữ nhật hoặc đường thẳng bằng Aspose.Cells cho .NET không?
 Có, bạn có thể thêm nhiều hình dạng khác nhau như hình chữ nhật, đường thẳng và mũi tên bằng cách sử dụng`Shapes` bộ sưu tập trong Aspose.Cells.
### Có thể thay đổi kích thước hình bầu dục sau khi thêm chúng không?
Hoàn toàn được! Bạn có thể sửa đổi các thuộc tính chiều cao và chiều rộng của hình bầu dục sau khi thêm chúng.
### Ngoài XLS, tôi có thể lưu bảng tính ở định dạng tệp nào?
Aspose.Cells hỗ trợ nhiều định dạng như XLSX, CSV và PDF, cùng nhiều định dạng khác.
### Tôi có thể thay đổi màu sắc của đường viền hình bầu dục không?
 Có, bạn có thể thay đổi màu đường viền của hình bầu dục bằng cách sử dụng`Line.Color` tài sản.
### Tôi có cần phải có giấy phép sử dụng Aspose.Cells không?
 Mặc dù bạn có thể dùng thử Aspose.Cells với bản dùng thử miễn phí, nhưng bạn sẽ cần[giấy phép](https://purchase.aspose.com/buy) để sử dụng lâu dài hoặc để truy cập các tính năng nâng cao.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
