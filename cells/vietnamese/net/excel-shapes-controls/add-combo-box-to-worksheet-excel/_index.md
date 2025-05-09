---
"description": "Tìm hiểu cách thêm hộp kết hợp vào bảng tính Excel theo chương trình bằng Aspose.Cells cho .NET. Hướng dẫn từng bước này sẽ hướng dẫn bạn từng chi tiết."
"linktitle": "Thêm Combo Box vào trang tính trong Excel"
"second_title": "API xử lý Excel Aspose.Cells .NET"
"title": "Thêm Combo Box vào trang tính trong Excel"
"url": "/vi/net/excel-shapes-controls/add-combo-box-to-worksheet-excel/"
"weight": 21
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Thêm Combo Box vào trang tính trong Excel

## Giới thiệu
Tạo bảng tính Excel tương tác có thể cải thiện đáng kể trải nghiệm của người dùng, đặc biệt là khi bạn thêm các thành phần biểu mẫu như hộp kết hợp. Hộp kết hợp cho phép người dùng chọn các tùy chọn từ danh sách được xác định trước, giúp nhập dữ liệu dễ dàng và hiệu quả hơn. Với Aspose.Cells for .NET, bạn có thể lập trình tạo hộp kết hợp trong các trang tính Excel mà không cần sử dụng Excel trực tiếp. Thư viện mạnh mẽ này cho phép các nhà phát triển thao tác các tệp Excel theo nhiều cách khác nhau, bao gồm khả năng tự động hóa các điều khiển biểu mẫu.
Trong hướng dẫn này, chúng tôi sẽ hướng dẫn bạn quy trình thêm hộp kết hợp vào bảng tính trong Excel bằng Aspose.Cells cho .NET. Nếu bạn đang muốn xây dựng bảng tính động, thân thiện với người dùng, hướng dẫn này sẽ giúp bạn bắt đầu.
## Điều kiện tiên quyết
Trước khi đi sâu vào mã, hãy đảm bảo rằng bạn có mọi thứ cần thiết:
- Aspose.Cells cho .NET: Tải xuống và cài đặt thư viện Aspose.Cells cho .NET từ [trang tải xuống](https://releases.aspose.com/cells/net/).
- .NET Framework: Đảm bảo bạn đã cài đặt .NET Framework trên máy của mình. Bất kỳ phiên bản nào được Aspose.Cells hỗ trợ đều có thể sử dụng.
- Môi trường phát triển: Sử dụng IDE như Visual Studio để quản lý dự án và viết mã.
- Giấy phép Aspose: Bạn có thể làm việc mà không cần giấy phép ở chế độ đánh giá, nhưng đối với phiên bản đầy đủ, bạn sẽ cần phải áp dụng giấy phép. Nhận một [giấy phép tạm thời](https://purchase.aspose.com/temporary-license/) nếu cần.
## Nhập gói
Để bắt đầu, bạn cần nhập các không gian tên cần thiết vào dự án của mình. Sau đây là những gì bạn cần:
```csharp
using System.IO;
using Aspose.Cells;
```
Đây là những điều cần thiết để tương tác với các tệp Excel và thao tác các thành phần biểu mẫu như hộp kết hợp trong sổ làm việc.
Chúng ta hãy chia nhỏ quá trình thêm hộp kết hợp thành nhiều bước đơn giản để dễ hiểu hơn.
## Bước 1: Thiết lập thư mục tài liệu
Bước đầu tiên là tạo một thư mục nơi các tệp Excel của bạn sẽ được lưu. Bạn có thể tạo một thư mục mới nếu nó chưa tồn tại.
```csharp
// Đường dẫn đến thư mục tài liệu.
string dataDir = "Your Document Directory";
// Tạo thư mục nếu thư mục đó chưa có.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
- dataDir: Chỉ định vị trí lưu tệp đầu ra.
- System.IO.Directory.Exists: Kiểm tra xem thư mục đã tồn tại hay chưa.
- System.IO.Directory.CreateDirectory: Tạo thư mục nếu thư mục đó bị thiếu.
## Bước 2: Tạo một Workbook mới
Bây giờ, hãy tạo một bảng tính Excel mới để thêm hộp kết hợp.

```csharp
// Tạo một Workbook mới.
Workbook workbook = new Workbook();
```

- Workbook workbook: Khởi tạo một phiên bản mới của lớp Workbook, biểu diễn một tệp Excel.
## Bước 3: Lấy bảng tính và ô
Tiếp theo, truy cập trang tính đầu tiên từ sổ làm việc và lấy tập hợp các ô mà bạn sẽ nhập dữ liệu.

```csharp
// Nhận bài tập đầu tiên.
Worksheet sheet = workbook.Worksheets[0];
// Nhận bộ sưu tập ô bảng tính.
Cells cells = sheet.Cells;
```

- Bảng tính: Lấy bảng tính đầu tiên từ sổ làm việc.
- Cells cells: Lấy tập hợp các ô từ bảng tính.
## Bước 4: Nhập giá trị cho hộp kết hợp
Bây giờ, chúng ta cần nhập một số giá trị vào các ô. Các giá trị này sẽ đóng vai trò là tùy chọn cho hộp kết hợp.

```csharp
// Nhập giá trị.
cells["B3"].PutValue("Employee:");
// In đậm.
cells["B3"].GetStyle().Font.IsBold = true;
// Nhập một số giá trị biểu thị phạm vi đầu vào cho hộp kết hợp.
cells["A2"].PutValue("Emp001");
cells["A3"].PutValue("Emp002");
cells["A4"].PutValue("Emp003");
cells["A5"].PutValue("Emp004");
cells["A6"].PutValue("Emp005");
cells["A7"].PutValue("Emp006");
```

- cells["B3"].PutValue: Đặt nhãn "Nhân viên" vào ô B3.
- Font.IsBold = true: Đặt văn bản thành chữ in đậm để làm nổi bật.
- Phạm vi đầu vào: Nhập nhiều ID nhân viên vào các ô từ A2 đến A7. Những ID này sẽ xuất hiện trong hộp thả xuống kết hợp.
## Bước 5: Thêm Combo Box vào Worksheet
Bước tiếp theo là thêm điều khiển hộp kết hợp vào bảng tính của bạn. Hộp kết hợp này sẽ cho phép người dùng chọn một trong các ID nhân viên mà bạn đã nhập trước đó.

```csharp
// Thêm hộp kết hợp mới.
Aspose.Cells.Drawing.ComboBox comboBox = sheet.Shapes.AddComboBox(2, 0, 2, 0, 22, 100);
```

- AddComboBox: Thêm một hộp kết hợp mới vào bảng tính. Các số (2, 0, 2, 0, 22, 100) biểu thị vị trí và kích thước của hộp kết hợp.
## Bước 6: Liên kết hộp kết hợp với một ô và thiết lập phạm vi đầu vào
Để hộp kết hợp hoạt động, chúng ta cần liên kết nó với một ô cụ thể và xác định phạm vi ô mà nó sẽ lấy các tùy chọn.

```csharp
// Đặt ô được liên kết.
comboBox.LinkedCell = "A1";
// Thiết lập phạm vi đầu vào.
comboBox.InputRange = "A2:A7";
```

- LinkedCell: Liên kết lựa chọn của hộp kết hợp với ô A1. Giá trị được chọn từ hộp kết hợp sẽ xuất hiện trong ô này.
- InputRange: Xác định phạm vi ô (A2:A7) chứa các giá trị sẽ điền vào các tùy chọn hộp kết hợp.
## Bước 7: Tùy chỉnh giao diện của hộp kết hợp
Bạn có thể tùy chỉnh hộp kết hợp thêm bằng cách chỉ định số dòng thả xuống và bật đổ bóng 3D để có tính thẩm mỹ tốt hơn.

```csharp
// Thiết lập số lượng dòng danh sách hiển thị trong phần danh sách của hộp kết hợp.
comboBox.DropDownLines = 5;
// Thiết lập hộp kết hợp với đổ bóng 3-D.
comboBox.Shadow = true;
```

- DropDownLines: Kiểm soát số lượng tùy chọn sẽ hiển thị trong hộp thả xuống kết hợp cùng một lúc.
- Bóng đổ: Thêm hiệu ứng đổ bóng 3D vào hộp tổ hợp.
## Bước 8: Tự động điều chỉnh cột và lưu sổ làm việc
Cuối cùng, hãy tự động điều chỉnh các cột để có bố cục gọn gàng và lưu sổ làm việc.

```csharp
// Cột tự động điều chỉnh
sheet.AutoFitColumns();
// Lưu tập tin.
workbook.Save(dataDir + "book1.out.xls");
```

- AutoFitColumns: Tự động điều chỉnh độ rộng của cột cho phù hợp với nội dung.
- Lưu: Lưu bảng tính dưới dạng tệp Excel trong thư mục được chỉ định.

## Phần kết luận
Thêm hộp kết hợp vào bảng tính Excel của bạn bằng Aspose.Cells cho .NET là một quy trình đơn giản giúp cải thiện đáng kể tính linh hoạt khi nhập dữ liệu. Bằng cách tạo điều khiển biểu mẫu theo chương trình, bạn có thể dễ dàng xây dựng bảng tính tương tác. Hướng dẫn này chỉ cho bạn cách thêm hộp kết hợp, liên kết hộp đó với ô và định cấu hình phạm vi nhập của hộp, tất cả đều sử dụng Aspose.Cells.
Aspose.Cells cung cấp nhiều tính năng để thao tác tệp Excel, khiến nó trở thành lựa chọn lý tưởng cho các nhà phát triển muốn tự động hóa các tác vụ bảng tính. Hãy dùng thử với [dùng thử miễn phí](https://releases.aspose.com/).
## Câu hỏi thường gặp
### Tôi có thể sử dụng Aspose.Cells mà không cần cài đặt Excel không?
Có, Aspose.Cells hoạt động độc lập với Excel và không yêu cầu phải cài đặt Excel.
### Làm thế nào để áp dụng giấy phép trong Aspose.Cells?
Bạn có thể áp dụng giấy phép bằng cách lấy nó từ [đây](https://purchase.aspose.com/buy) và gọi `License.SetLicense()` trong mã của bạn.
### Aspose.Cells hỗ trợ những định dạng nào để lưu tệp?
Aspose.Cells hỗ trợ lưu tệp ở nhiều định dạng như XLSX, XLS, CSV, PDF, v.v.
### Có giới hạn số lượng hộp kết hợp mà tôi có thể thêm không?
Không, không có giới hạn nghiêm ngặt nào; bạn có thể thêm nhiều hộp kết hợp tùy theo yêu cầu của dự án.
### Làm thế nào để tôi nhận được hỗ trợ cho Aspose.Cells?
Bạn có thể nhận được sự hỗ trợ từ [Diễn đàn Aspose](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}