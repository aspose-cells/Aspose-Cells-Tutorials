---
"description": "Tìm hiểu cách thêm hộp văn bản có thể tùy chỉnh vào Excel bằng Aspose.Cells cho .NET trong hướng dẫn từng bước này."
"linktitle": "Thêm TextBox vào trang tính trong Excel"
"second_title": "API xử lý Excel Aspose.Cells .NET"
"title": "Thêm TextBox vào trang tính trong Excel"
"url": "/vi/net/excel-shapes-controls/add-textbox-to-worksheet-excel/"
"weight": 14
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Thêm TextBox vào trang tính trong Excel

## Giới thiệu
Bạn có muốn cải thiện bảng tính Excel của mình bằng hình ảnh độc đáo có thể thu hút khán giả của bạn không? Thêm hộp văn bản là một cách tuyệt vời để thực hiện điều này! Với Aspose.Cells cho .NET, bạn có thể dễ dàng tích hợp hộp văn bản vào bảng tính Excel của mình, giúp tài liệu của bạn có nhiều thông tin hơn và hấp dẫn hơn về mặt hình ảnh. Hướng dẫn từng bước này sẽ hướng dẫn bạn thực hiện quy trình đơn giản để thêm hộp văn bản bằng Aspose.Cells, giới thiệu cách cá nhân hóa chúng bằng văn bản, màu sắc, siêu liên kết, v.v.!
## Điều kiện tiên quyết
Trước khi đi sâu vào quá trình mã hóa kỳ diệu này, sau đây là những điều kiện tiên quyết cần thiết để đảm bảo trải nghiệm diễn ra suôn sẻ:
1. Môi trường phát triển .NET: Bạn sẽ cần một .NET framework đang hoạt động cùng với một IDE như Visual Studio. Hãy đảm bảo rằng nó được cập nhật lên phiên bản mới nhất!
2. Aspose.Cells cho .NET: Đảm bảo rằng bạn đã tải xuống thư viện Aspose.Cells. Bạn có thể tải xuống phiên bản mới nhất từ [đây](https://releases.aspose.com/cells/net/).
3. Kiến thức lập trình cơ bản: Sự quen thuộc với C# và một số khái niệm chung về xử lý tệp Excel sẽ giúp hướng dẫn này dễ dàng hơn!
## Nhập gói
Hãy đảm bảo nhập các gói cần thiết vào đầu tệp C# của bạn. Sau đây là cách bạn có thể thực hiện:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
## Cài đặt Aspose.Cells
Nếu bạn chưa thực hiện, bạn có thể thêm Aspose.Cells thông qua Trình quản lý gói NuGet trong Visual Studio:
1. Mở Visual Studio.
2. Đi đến `Tools` -> `NuGet Package Manager` -> `Manage NuGet Packages for Solution`.
3. Tìm kiếm “Aspose.Cells” và cài đặt cho dự án của bạn.
Bây giờ chúng ta đã đặt nền tảng xong, hãy cùng bắt đầu phần thú vị nhé!
## Bước 1: Thiết lập thư mục tài liệu của bạn
Trước tiên, hãy thiết lập thư mục nơi lưu trữ tất cả các tài liệu Excel của bạn. Điều cần thiết là phải đảm bảo rằng thư mục này tồn tại trước khi chúng ta bắt đầu tạo sổ làm việc.
```csharp
// Đường dẫn đến thư mục tài liệu.
string dataDir = "Your Document Directory"; 
// Tạo thư mục nếu thư mục đó chưa có.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists) 
    System.IO.Directory.CreateDirectory(dataDir);
```
Đoạn mã này sẽ tạo một thư mục có tên `Your Document Directory` (vui lòng thay thế bằng đường dẫn thực tế của bạn) nếu nó chưa tồn tại. Quá dễ phải không?
## Bước 2: Khởi tạo một Workbook mới
Tiếp theo, chúng ta cần tạo một sổ làm việc mới để thêm hộp văn bản. Điều này có thể dễ dàng thực hiện bằng một vài dòng mã:
```csharp
// Tạo một Workbook mới.
Workbook workbook = new Workbook();
```
Dòng mã này tạo ra một bảng tính Excel mới. Đơn giản và dễ hiểu!
## Bước 3: Truy cập trang tính đầu tiên
Bây giờ chúng ta đã có bảng tính sẵn sàng, hãy lấy bảng tính đầu tiên để thêm hộp văn bản:
```csharp
// Nhận bài tập đầu tiên trong sách.
Worksheet worksheet = workbook.Worksheets[0];
```
Chỉ cần như vậy, bây giờ bạn đã có quyền truy cập vào bảng tính đầu tiên có tên `worksheet`. Đã đến lúc làm cho nó tỏa sáng!
## Bước 4: Thêm một hộp văn bản
Được rồi, đã đến lúc thêm hộp văn bản đầu tiên của chúng ta! Đây là cách thực hiện:
```csharp
// Thêm hộp văn bản mới vào bộ sưu tập.
int textboxIndex = worksheet.TextBoxes.Add(2, 1, 160, 200);
```
Trong dòng này, chúng tôi sẽ chỉ định hàng và cột nơi hộp văn bản sẽ được đặt, cũng như thiết lập chiều rộng và chiều cao của nó (lần lượt là 160 và 200). Hãy thoải mái điều chỉnh các con số này dựa trên bố cục của bạn!
## Bước 5: Lấy đối tượng TextBox
Sau khi thêm hộp văn bản, chúng ta cần tham chiếu đến hộp đó để có thể tùy chỉnh nội dung của hộp:
```csharp
// Lấy đối tượng hộp văn bản.
Aspose.Cells.Drawing.TextBox textbox0 = worksheet.TextBoxes[textboxIndex];
```
Hiện nay, `textbox0` là tấm vé vàng để bạn sửa đổi hộp văn bản này!
## Bước 6: Điền nội dung vào TextBox
Tiếp theo, chúng ta hãy cung cấp một số văn bản cho hộp văn bản:
```csharp
// Điền vào văn bản.
textbox0.Text = "ASPOSE______The .NET & JAVA Component Publisher!";
```
Chèn văn bản vào hộp văn bản của bạn chỉ đơn giản như vậy thôi! 
## Bước 7: Tùy chỉnh giao diện hộp văn bản
Chúng ta hãy làm cho nó đẹp hơn một chút nhé? Bạn có thể điều chỉnh màu phông chữ, kiểu chữ và nhiều thứ khác nữa!
```csharp
// Đặt màu phông chữ.
textbox0.Font.Color = Color.Blue;
// Đặt phông chữ thành chữ đậm.
textbox0.Font.IsBold = true;
// Đặt kích thước phông chữ.
textbox0.Font.Size = 14;
// Đặt thuộc tính phông chữ thành in nghiêng.
textbox0.Font.IsItalic = true;
```
Hãy thoải mái thử nghiệm với nhiều màu sắc và kiểu dáng khác nhau để xem kiểu nào trông đẹp nhất!
## Bước 8: Thêm siêu liên kết
Bạn muốn biến hộp văn bản của mình thành liên kết có thể nhấp được? Hãy thực hiện như sau:
```csharp
// Thêm siêu liên kết vào hộp văn bản.
textbox0.AddHyperlink("http://www.aspose.com/");
```
Bây giờ bất kỳ ai nhấp vào hộp văn bản của bạn sẽ được chuyển đến trang web Aspose. Thật giống như phép thuật!
## Bước 9: Thiết lập Kiểu Vị trí Hộp Văn bản
Bạn có nhiều lựa chọn khác nhau về cách bạn muốn hộp văn bản hoạt động liên quan đến bảng tính của mình. Sau đây là ví dụ về cách thiết lập nó thành dạng tự do trôi nổi:
```csharp
// Thiết lập vị trí.
textbox0.Placement = PlacementType.FreeFloating;
```
Ngoài ra, nếu bạn muốn thay đổi kích thước và di chuyển theo ô, bạn có thể thiết lập như sau:
```csharp
// Đặt kiểu vị trí để hộp văn bản sẽ di chuyển và thay đổi kích thước theo ô.
textbox1.Placement = PlacementType.MoveAndSize;
```
## Bước 10: Tùy chỉnh Định dạng Dòng và Tô
Sau đây là cách bạn có thể thay đổi giao diện đường viền và phần tô của hộp văn bản:
```csharp
// Lấy định dạng điền của hộp văn bản.
Aspose.Cells.Drawing.FillFormat fillformat = textbox0.Fill;            
// Lấy kiểu định dạng dòng của hộp văn bản.
Aspose.Cells.Drawing.LineFormat lineformat = textbox0.Line;           
// Thiết lập độ dày của đường.
lineformat.Weight = 6;
// Đặt kiểu gạch ngang thành squaredot.
lineformat.DashStyle = MsoLineDashStyle.SquareDot;
```
Với tính năng này, bạn có thể tùy chỉnh hộp văn bản hơn nữa, thêm hình ảnh phù hợp với phong cách của bạn.
## Bước 11: Thêm một hộp văn bản khác
Không ai nói rằng chúng ta chỉ có thể thêm một hộp văn bản! Hãy thêm một hộp khác với một số văn bản khác:
```csharp
// Thêm một hộp văn bản khác.
textboxIndex = worksheet.TextBoxes.Add(15, 4, 85, 120);
// Nhận hộp văn bản thứ hai.
Aspose.Cells.Drawing.TextBox textbox1 = worksheet.TextBoxes[textboxIndex];
// Nhập một số văn bản vào đó.
textbox1.Text = "This is another simple text box";
```
Bây giờ bạn có thể làm cho bảng tính Excel của mình trở nên thú vị hơn với nhiều hộp văn bản!
## Bước 12: Lưu sổ làm việc của bạn
Cuối cùng, đã đến lúc lưu lại kiệt tác của chúng ta! Đây là dòng mã cuối cùng trong ngày:
```csharp
// Lưu tệp excel.
workbook.Save(dataDir + "book1.out.xls");
```
Chỉ với một dòng mã này, bạn đã tạo và sửa đổi một tệp Excel với các hộp văn bản có thể tùy chỉnh!
## Phần kết luận
Xin chúc mừng! Bạn đã điều hướng thành công qua thế giới hộp văn bản trong Excel bằng Aspose.Cells cho .NET. Bạn không chỉ học cách thêm hộp văn bản mà còn học cách tùy chỉnh để làm cho bảng tính của bạn hấp dẫn hơn. Từ việc thay đổi màu sắc và kiểu dáng đến thậm chí thêm siêu liên kết, khả năng thực tế là vô tận! 
Bạn đã sẵn sàng để bắt đầu chuyển đổi tài liệu Excel của mình chưa? Hãy để sự sáng tạo của bạn tỏa sáng và thử nghiệm với nhiều bố cục khác nhau!
## Câu hỏi thường gặp
### Aspose.Cells dành cho .NET là gì?
Aspose.Cells for .NET là một thư viện mạnh mẽ cho phép các nhà phát triển tạo, thao tác và chuyển đổi các tệp Excel một cách dễ dàng.
### Tôi có thể dùng thử Aspose.Cells trước khi mua không?
Có! Bạn có thể tải xuống và sử dụng phiên bản dùng thử miễn phí [đây](https://releases.aspose.com/).
### Tôi có thể tìm tài liệu về Aspose.Cells ở đâu?
Bạn có thể truy cập tài liệu toàn diện tại [Tài liệu Aspose.Cells](https://reference.aspose.com/cells/net/).
### Tôi có được hỗ trợ nếu gặp vấn đề không?
Chắc chắn rồi! Nếu bạn cần trợ giúp, hãy đến [Diễn đàn Aspose](https://forum.aspose.com/c/cells/9) để được hỗ trợ.
### Tôi có thể sử dụng Aspose.Cells mà không cần giấy phép không?
Mặc dù bạn có thể sử dụng phiên bản dùng thử miễn phí, để truy cập đầy đủ chức năng, bạn sẽ cần phải mua giấy phép. Kiểm tra giá [đây](https://purchase.aspose.com/buy).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}