---
"description": "Tìm hiểu cách bảo vệ các hàng cụ thể trong bảng tính Excel bằng Aspose.Cells cho .NET với hướng dẫn từng bước này. Bảo vệ dữ liệu của bạn hiệu quả."
"linktitle": "Bảo vệ các hàng cụ thể trong bảng tính bằng Aspose.Cells"
"second_title": "API xử lý Excel Aspose.Cells .NET"
"title": "Bảo vệ các hàng cụ thể trong bảng tính bằng Aspose.Cells"
"url": "/vi/net/worksheet-security/protect-specific-rows/"
"weight": 16
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Bảo vệ các hàng cụ thể trong bảng tính bằng Aspose.Cells

## Giới thiệu
Trong hướng dẫn này, chúng tôi sẽ hướng dẫn bạn quy trình bảo vệ các hàng cụ thể trong bảng tính Excel bằng Aspose.Cells cho .NET. Chúng tôi sẽ hướng dẫn chi tiết từng bước, bao gồm các điều kiện tiên quyết, nhập các gói cần thiết và chia nhỏ mã thành các hướng dẫn dễ làm theo. Cuối cùng, bạn sẽ được trang bị kiến thức để áp dụng bảo vệ hàng trong các ứng dụng của riêng mình.
## Điều kiện tiên quyết
Trước khi bắt đầu thực hiện, bạn cần đáp ứng một số điều kiện tiên quyết để làm theo hướng dẫn này:
1. Aspose.Cells cho .NET: Bạn cần phải cài đặt Aspose.Cells cho .NET. Nếu bạn chưa cài đặt, bạn có thể tải phiên bản mới nhất bằng cách truy cập trang web Aspose.
2. Hiểu biết cơ bản về C# và .NET: Hướng dẫn này giả định rằng bạn đã quen thuộc với C# và có kiến thức cơ bản về lập trình .NET. Nếu bạn chưa quen với những điều này, trước tiên bạn có thể muốn xem qua một số tài nguyên giới thiệu.
3. Visual Studio hoặc bất kỳ IDE .NET nào: Bạn sẽ cần một môi trường phát triển tích hợp (IDE) như Visual Studio để chạy mã. Điều này cung cấp tất cả các công cụ cần thiết và khả năng gỡ lỗi.
4. Giấy phép Aspose.Cells: Nếu bạn muốn tránh các giới hạn phiên bản đánh giá, hãy đảm bảo bạn có giấy phép Aspose.Cells hợp lệ. Bạn cũng có thể sử dụng giấy phép tạm thời nếu bạn mới bắt đầu.
Để biết thông tin chi tiết về Aspose.Cells và cài đặt, bạn có thể kiểm tra [tài liệu](https://reference.aspose.com/cells/net/).
## Nhập gói
Để bắt đầu sử dụng Aspose.Cells, bạn cần nhập các không gian tên cần thiết vào dự án C# của mình. Các không gian tên này cung cấp cho bạn quyền truy cập vào các lớp và phương thức cần thiết để thao tác với các tệp Excel.
Sau đây là cách bạn nhập các không gian tên cần thiết:
```csharp
using System.IO;
using Aspose.Cells;
```
Những lần nhập này rất quan trọng vì chúng cung cấp quyền truy cập vào chức năng của Aspose.Cells và cho phép bạn tương tác với các tệp Excel trong dự án .NET của mình.
Bây giờ bạn đã thiết lập các điều kiện tiên quyết và các mục nhập cần thiết, đã đến lúc đi sâu vào mã thực tế. Chúng tôi sẽ chia nhỏ quy trình thành nhiều bước để đảm bảo rõ ràng.
## Bước 1: Thiết lập thư mục dự án của bạn
Trong bất kỳ chương trình nào, việc sắp xếp các tệp của bạn là chìa khóa. Trước tiên, hãy tạo một thư mục nơi chúng ta có thể lưu trữ sổ làm việc. Chúng ta kiểm tra xem thư mục có tồn tại không và tạo thư mục đó nếu cần.
```csharp
// Xác định đường dẫn đến thư mục tài liệu.
string dataDir = "Your Document Directory";
// Tạo thư mục nếu thư mục đó chưa có.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Tại đây, bạn xác định đường dẫn nơi các tệp Excel của bạn sẽ được lưu trữ. Nếu thư mục không tồn tại, chúng tôi sẽ tạo thư mục đó. Bước này rất quan trọng để đảm bảo sổ làm việc của bạn có nơi để lưu.
## Bước 2: Tạo một Workbook mới
Tiếp theo, chúng ta tạo một bảng tính mới bằng cách sử dụng `Workbook` Lớp này cung cấp tất cả các chức năng cần thiết để làm việc với các tệp Excel.
```csharp
// Tạo một bảng tính mới.
Workbook wb = new Workbook();
```
Lúc này, chúng ta đã có một bảng tính mới để làm việc.
## Bước 3: Truy cập vào Bảng tính
Bây giờ chúng ta truy cập vào worksheet đầu tiên của workbook mới tạo. Một workbook có thể chứa nhiều worksheet, nhưng trong trường hợp này, chúng ta tập trung vào worksheet đầu tiên.
```csharp
// Tạo một đối tượng bảng tính và lấy trang tính đầu tiên.
Worksheet sheet = wb.Worksheets[0];
```
Đây, `Worksheets[0]` đề cập đến trang tính đầu tiên trong sổ làm việc (được lập chỉ mục bắt đầu từ 0).
## Bước 4: Mở khóa tất cả các cột
Trong Excel, các ô bị khóa theo mặc định khi trang tính được bảo vệ. Nếu bạn muốn bảo vệ các hàng cụ thể, trước tiên bạn phải mở khóa các cột. Trong bước này, chúng ta lặp qua tất cả các cột và mở khóa chúng.
```csharp
// Xác định đối tượng kiểu.
Style style;
// Xác định đối tượng styleflag.
StyleFlag flag;
// Lặp qua tất cả các cột trong bảng tính và mở khóa chúng.
for (int i = 0; i <= 255; i++)
{
    style = sheet.Cells.Columns[(byte)i].Style;
    style.IsLocked = false;
    flag = new StyleFlag();
    flag.Locked = true;
    sheet.Cells.Columns[(byte)i].ApplyStyle(style, flag);
}
```
Ở đây, chúng ta duyệt qua các cột từ 0 đến 255 (tổng số cột trong một bảng tính Excel) và mở khóa chúng. Điều này đảm bảo rằng các hàng chúng ta muốn bảo vệ vẫn có thể tương tác được, trong khi các hàng khác vẫn bị khóa.
## Bước 5: Khóa hàng đầu tiên
Bây giờ tất cả các cột đã được mở khóa, chúng ta có thể chuyển sang bảo vệ các hàng. Trong bước này, chúng ta khóa hàng đầu tiên, điều này sẽ khiến hàng đó không thể chỉnh sửa được sau khi trang tính được bảo vệ.
```csharp
// Nhận kiểu hàng đầu tiên.
style = sheet.Cells.Rows[0].Style;
// Khóa nó lại.
style.IsLocked = true;
// Tạo cờ.
flag = new StyleFlag();
// Thiết lập cài đặt khóa.
flag.Locked = true;
// Áp dụng kiểu cho hàng đầu tiên.
sheet.Cells.ApplyRowStyle(0, style, flag);
```
Mã này khóa hàng đầu tiên, đảm bảo hàng này vẫn được bảo vệ sau khi chúng ta áp dụng chế độ bảo vệ cho trang tính.
## Bước 6: Bảo vệ bảng tính
Tại thời điểm này, chúng ta đã sẵn sàng bảo vệ bảng tính. Bước này áp dụng các thiết lập bảo vệ cho toàn bộ bảng tính, đảm bảo rằng bất kỳ ô nào bị khóa đều không thể chỉnh sửa được.
```csharp
// Bảo vệ tờ giấy.
sheet.Protect(ProtectionType.All);
```
Bằng cách sử dụng `ProtectionType.All`, chúng tôi đảm bảo rằng tất cả các ô, ngoại trừ những ô được mở khóa rõ ràng (như các cột của chúng tôi), đều được bảo vệ. Đây là bước áp dụng bảo vệ cho bảng tính.
## Bước 7: Lưu tệp Excel
Cuối cùng, sau khi áp dụng bảo vệ, chúng ta lưu sổ làm việc. Bạn có thể chỉ định định dạng bạn muốn lưu tệp. Trong ví dụ này, chúng ta lưu sổ làm việc dưới dạng tệp Excel 97-2003.
```csharp
// Lưu tệp excel.
wb.Save(dataDir + "output.out.xls", SaveFormat.Excel97To2003);
```
Bước này lưu tệp vào đường dẫn đã chỉ định, hoàn thành nhiệm vụ bảo vệ các hàng cụ thể trong bảng tính.
## Phần kết luận
Bảo vệ các hàng cụ thể trong bảng tính Excel bằng Aspose.Cells cho .NET là một quy trình đơn giản khi bạn chia nhỏ từng bước. Bằng cách mở khóa các cột, khóa các hàng cụ thể và áp dụng các thiết lập bảo vệ, bạn đảm bảo dữ liệu của mình vẫn an toàn và chỉ có thể chỉnh sửa khi cần thiết. Hướng dẫn này bao gồm tất cả các bước chính, từ thiết lập thư mục dự án của bạn đến lưu sổ làm việc cuối cùng.
Cho dù bạn đang tạo mẫu, báo cáo hay bảng tính tương tác, sử dụng bảo vệ hàng là cách đơn giản nhưng hiệu quả để duy trì quyền kiểm soát dữ liệu của bạn. Hãy thử quy trình này trong các dự án của riêng bạn và khám phá toàn bộ tiềm năng của Aspose.Cells cho .NET.
## Câu hỏi thường gặp
### Tôi có thể bảo vệ nhiều hàng trong bảng tính không?  
Có, bạn có thể áp dụng các bước bảo vệ giống nhau cho nhiều hàng bằng cách sửa đổi vòng lặp hoặc áp dụng kiểu cho các hàng khác.
### Điều gì xảy ra nếu tôi không mở khóa bất kỳ cột nào trước khi bảo vệ trang tính?  
Nếu bạn không mở khóa các cột, chúng sẽ bị khóa khi trang tính được bảo vệ và người dùng sẽ không thể tương tác với chúng.
### Làm thế nào để mở khóa các ô cụ thể thay vì toàn bộ cột?  
Bạn có thể mở khóa các ô cụ thể bằng cách truy cập vào kiểu của chúng và thiết lập `IsLocked` tài sản để `false`.
### Tôi có thể sử dụng phương pháp này để bảo vệ toàn bộ bảng tính không?  
Có, bạn có thể bảo vệ toàn bộ bảng tính bằng cách áp dụng tính năng bảo vệ cho tất cả các ô và không để ô nào bị mở khóa.
### Làm thế nào để bỏ bảo vệ một bảng tính?  
Bạn có thể xóa bảo vệ bằng cách gọi `Unprotect` phương pháp trên bảng tính và cung cấp mật khẩu bảo vệ (nếu có).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}