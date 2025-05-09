---
"description": "Tìm hiểu cách thêm hộp danh sách vào bảng tính Excel bằng Aspose.Cells cho .NET. Làm theo hướng dẫn từng bước dễ dàng của chúng tôi và làm cho bảng tính Excel của bạn trở nên tương tác."
"linktitle": "Thêm hộp danh sách vào trang tính trong Excel"
"second_title": "API xử lý Excel Aspose.Cells .NET"
"title": "Thêm hộp danh sách vào trang tính trong Excel"
"url": "/vi/net/excel-shapes-controls/add-list-box-to-worksheet-excel/"
"weight": 20
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Thêm hộp danh sách vào trang tính trong Excel

## Giới thiệu
Thêm các thành phần tương tác vào bảng tính Excel của bạn, như hộp danh sách, có thể cải thiện đáng kể việc quản lý và trình bày dữ liệu. Cho dù bạn đang tạo biểu mẫu tương tác hay công cụ nhập dữ liệu tùy chỉnh, khả năng kiểm soát đầu vào của người dùng bằng hộp danh sách là vô giá. Aspose.Cells for .NET cung cấp một cách hiệu quả để thêm và quản lý các điều khiển này trong các tệp Excel của bạn. Trong hướng dẫn này, chúng tôi sẽ hướng dẫn bạn quy trình thêm hộp danh sách vào bảng tính bằng Aspose.Cells for .NET.
## Điều kiện tiên quyết
Trước khi bắt đầu viết mã, hãy đảm bảo bạn có các công cụ và tài nguyên sau:
- Thư viện Aspose.Cells cho .NET: Bạn có thể tải xuống từ [Trang tải xuống Aspose.Cells cho .NET](https://releases.aspose.com/cells/net/).
- Môi trường phát triển: Bất kỳ IDE nào hỗ trợ phát triển .NET, chẳng hạn như Visual Studio.
- .NET Framework: Đảm bảo rằng dự án của bạn đang hướng tới phiên bản được hỗ trợ của .NET Framework.
Ngoài ra, hãy cân nhắc việc có được một [giấy phép tạm thời](https://purchase.aspose.com/temporary-license/) nếu bạn muốn khám phá tất cả các tính năng mà không có giới hạn.
## Nhập gói
Trước khi bắt đầu, hãy đảm bảo bạn đã nhập các không gian tên Aspose.Cells cần thiết. Sau đây là cách thực hiện:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
```
Trong hướng dẫn này, chúng tôi sẽ chia nhỏ quy trình thêm hộp danh sách thành nhiều bước đơn giản. Thực hiện chặt chẽ từng bước để đảm bảo mọi thứ hoạt động như mong đợi.
## Bước 1: Thiết lập thư mục tài liệu của bạn
Trước khi tạo bất kỳ tệp Excel nào, bạn cần một vị trí để lưu tệp đó. Sau đây là cách thiết lập thư mục:
```csharp
// Đường dẫn đến thư mục tài liệu.
string dataDir = "Your Document Directory";
// Tạo thư mục nếu nó chưa tồn tại.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Trong bước này, bạn sẽ xác định nơi lưu trữ tệp của mình. Mã sẽ kiểm tra xem thư mục có tồn tại không và nếu không, nó sẽ tạo một thư mục cho bạn. Điều này đảm bảo rằng bạn không gặp phải bất kỳ lỗi "không tìm thấy tệp" nào sau này.
## Bước 2: Tạo một bảng tính mới và truy cập vào bảng tính đầu tiên
Tiếp theo, chúng ta sẽ tạo một bảng tính mới và truy cập vào trang tính đầu tiên nơi chúng ta sẽ thêm hộp danh sách.
```csharp
// Tạo một Workbook mới.
Workbook workbook = new Workbook();
// Nhận bài tập đầu tiên.
Worksheet sheet = workbook.Worksheets[0];
```
Về cơ bản, sổ làm việc là tệp Excel của bạn. Ở đây, chúng ta đang tạo một sổ làm việc mới và truy cập vào trang tính đầu tiên, nơi chúng ta sẽ đặt hộp danh sách của mình. Hãy nghĩ về điều này như việc tạo một khung vẽ trống nơi bạn sẽ tô màu các điều khiển.
## Bước 3: Nhập dữ liệu cho hộp danh sách
Trước khi thêm hộp danh sách, chúng ta cần nhập một số dữ liệu mà hộp danh sách sẽ tham chiếu.
```csharp
// Nhận bộ sưu tập ô bảng tính.
Cells cells = sheet.Cells;
// Nhập giá trị cho nhãn.
cells["B3"].PutValue("Choose Dept:");
// Đặt nhãn thành chữ in đậm.
cells["B3"].GetStyle().Font.IsBold = true;
// Nhập giá trị cho hộp danh sách.
cells["A2"].PutValue("Sales");
cells["A3"].PutValue("Finance");
cells["A4"].PutValue("MIS");
cells["A5"].PutValue("R&D");
cells["A6"].PutValue("Marketing");
cells["A7"].PutValue("HRA");
```
Ở đây, chúng tôi đang thêm một số văn bản vào bảng tính. Nhãn "Chọn Phòng ban:" được đặt trong ô B3 và phông chữ của nó được đặt thành đậm. Trong cột A, chúng tôi đang chèn các giá trị sẽ đóng vai trò là phạm vi đầu vào cho hộp danh sách của chúng tôi, đại diện cho các phòng ban khác nhau. Phạm vi đầu vào này là những gì người dùng sẽ chọn khi tương tác với hộp danh sách.
## Bước 4: Thêm Hộp danh sách vào Trang tính
Bây giờ chúng ta đã thiết lập dữ liệu, hãy thêm chính hộp điều khiển danh sách.
```csharp
// Thêm hộp danh sách mới.
Aspose.Cells.Drawing.ListBox listBox = sheet.Shapes.AddListBox(2, 0, 3, 0, 122, 100);
```
Mã này thêm hộp danh sách vào bảng tính. Các tham số xác định vị trí và kích thước của hộp danh sách. Hộp danh sách được đặt ở hàng 2, cột 0 với chiều rộng là 122 và chiều cao là 100. Đây là các tọa độ và kích thước xác định vị trí hộp danh sách sẽ xuất hiện trong bảng tính.
## Bước 5: Thiết lập Thuộc tính Hộp Danh sách
Tiếp theo, chúng ta sẽ thiết lập nhiều thuộc tính khác nhau cho hộp danh sách để nó có đầy đủ chức năng.
```csharp
// Đặt loại vị trí.
listBox.Placement = PlacementType.FreeFloating;
// Đặt ô được liên kết.
listBox.LinkedCell = "A1";
// Thiết lập phạm vi đầu vào.
listBox.InputRange = "A2:A7";
// Đặt loại lựa chọn.
listBox.SelectionType = SelectionType.Single;
// Thiết lập hộp danh sách với bóng đổ 3-D.
listBox.Shadow = true;
```
- PlacementType.FreeFloating: Thuộc tính này đảm bảo hộp danh sách giữ nguyên vị trí bất kể bảng tính được sửa đổi như thế nào.
- LinkedCell: Thiết lập một ô (trong trường hợp này là A1) nơi giá trị được chọn từ hộp danh sách sẽ được hiển thị.
- InputRange: Điều này cho hộp danh sách biết nơi tìm danh sách các tùy chọn của nó (A2 đến A7, chúng ta đã thiết lập trước đó).
- SelectionType.Single: Tùy chọn này hạn chế người dùng chỉ được chọn một mục từ hộp danh sách.
- Bóng đổ: Hiệu ứng bóng đổ giúp hộp danh sách trông ba chiều hơn, hấp dẫn hơn về mặt thị giác.
## Bước 6: Lưu tệp Excel
Cuối cùng, hãy lưu bảng tính của chúng ta với hộp danh sách được bao gồm.
```csharp
// Lưu bảng tính.
workbook.Save(dataDir + "book1.out.xls");
```
Dòng mã này lưu sổ làm việc vào thư mục chúng ta đã thiết lập trước đó. Tệp có tên là "book1.out.xls" nhưng bạn có thể chọn bất kỳ tên nào phù hợp với dự án của mình.
## Phần kết luận
Và bạn đã có nó! Bạn đã thêm thành công một hộp danh sách vào bảng tính Excel bằng Aspose.Cells cho .NET. Chỉ với một vài dòng mã, chúng tôi đã tạo ra một hộp danh sách đầy đủ chức năng, giúp bảng tính tương tác và năng động hơn. Hướng dẫn này sẽ cung cấp cho bạn nền tảng vững chắc để khám phá các điều khiển và tính năng khác trong Aspose.Cells cho .NET. Hãy tiếp tục thử nghiệm và sớm thôi, bạn sẽ thành thạo chức năng rộng lớn của thư viện!
## Câu hỏi thường gặp
### Tôi có thể cho phép nhiều lựa chọn trong hộp danh sách không?  
Vâng, bạn có thể thay đổi `SelectionType` ĐẾN `SelectionType.Multi` để cho phép nhiều lựa chọn.
### Tôi có thể thay đổi giao diện của hộp danh sách không?  
Hoàn toàn có thể! Aspose.Cells cho phép bạn tùy chỉnh giao diện của hộp danh sách, bao gồm kích thước, phông chữ và thậm chí cả màu sắc.
### Nếu sau này tôi cần xóa hộp danh sách thì sao?  
Bạn có thể truy cập và xóa hộp danh sách khỏi `Shapes` bộ sưu tập sử dụng `sheet.Shapes.RemoveAt(index)`.
### Tôi có thể liên kết hộp danh sách tới một ô khác không?  
Vâng, chỉ cần thay đổi `LinkedCell` thuộc tính vào bất kỳ ô nào khác mà bạn muốn hiển thị giá trị đã chọn.
### Làm thế nào để thêm nhiều mục hơn vào hộp danh sách?  
Chỉ cần cập nhật phạm vi đầu vào bằng cách chèn thêm giá trị vào các ô được chỉ định và hộp danh sách sẽ tự động cập nhật.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}