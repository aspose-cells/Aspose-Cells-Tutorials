---
"description": "Tìm hiểu cách thiết lập định dạng trường trang trong PivotTable theo chương trình bằng Aspose.Cells cho .NET. Làm theo hướng dẫn từng bước của chúng tôi để quản lý dữ liệu liền mạch."
"linktitle": "Thiết lập Định dạng Trường Trang theo Chương trình trong .NET"
"second_title": "API xử lý Excel Aspose.Cells .NET"
"title": "Thiết lập Định dạng Trường Trang theo Chương trình trong .NET"
"url": "/vi/net/creating-and-configuring-pivot-tables/setting-page-field-format/"
"weight": 21
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Thiết lập Định dạng Trường Trang theo Chương trình trong .NET

## Giới thiệu
Việc tạo và thao tác các tệp Excel thông qua mã có thể khá hữu ích, đặc biệt là khi bạn cần phân tích các tập dữ liệu lớn. Một trong những công cụ tuyệt vời trong kho vũ khí của bạn là Aspose.Cells cho .NET, cho phép bạn tương tác theo chương trình với các tệp Excel và tạo các cấu trúc báo cáo phức tạp. Trong hướng dẫn này, chúng ta sẽ đi sâu vào cách bạn có thể thiết lập các định dạng trường trang trong PivotTable bằng thư viện mạnh mẽ này. Cho dù bạn là nhà phát triển có kinh nghiệm hay người mới bắt đầu, thì khi kết thúc hướng dẫn này, bạn sẽ nắm vững cách vận hành PivotTable và các cài đặt khác nhau của chúng trong .NET.
## Điều kiện tiên quyết
Trước khi bắt đầu viết mã, hãy đảm bảo rằng bạn đã thiết lập mọi thứ đúng cách. Bạn sẽ cần những thứ sau:
- Visual Studio: Môi trường làm việc nơi bạn có thể viết và thực thi mã .NET của mình.
- Aspose.Cells: Bạn có thể tải xuống thư viện [đây](https://releases.aspose.com/cells/net/).
- Kiến thức cơ bản về C#: Sự quen thuộc với lập trình C# sẽ giúp bạn hiểu các đoạn mã tốt hơn.
- Tệp Excel: Chuẩn bị sẵn một tệp Excel (như `Book1.xls`) chứa dữ liệu phù hợp để tạo PivotTable. 
Nếu bạn chưa dùng thử, hãy dùng thử miễn phí Aspose.Cells [đây](https://releases.aspose.com/).
## Nhập gói
Để bắt đầu, bạn sẽ cần nhập đúng gói vào dự án của mình. Bắt đầu bằng cách thêm tham chiếu đến thư viện Aspose.Cells vào dự án C# của bạn. Sau đây là cách thực hiện:
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
using Aspose.Cells.Pivot;
```
Lệnh này sẽ sử dụng tất cả các lớp và phương thức cần thiết để thao tác với các tệp Excel bằng Aspose.Cells.
## Bước 1: Thiết lập không gian làm việc của bạn
Bắt đầu bằng cách xác định thư mục làm việc của bạn nơi các tệp Excel của bạn sẽ được lưu trữ. Ví dụ, bạn có thể khai báo một biến như thế này:
```csharp
string dataDir = "Your Document Directory";
```
## Đang tải Sổ làm việc
Tiếp theo, chúng ta cần tải mẫu Excel của mình. Đây là bước thiết yếu vì nó thiết lập bối cảnh cho các hoạt động của chúng ta:
```csharp
Workbook workbook = new Workbook(dataDir + "Book1.xls");
```
Dòng này tải bảng tính hiện có từ thư mục được chỉ định.
## Bước 2: Truy cập vào Bảng tính
Sau khi sổ làm việc của bạn được tải, đã đến lúc truy cập vào trang tính chứa PivotTable hoặc dữ liệu bạn muốn phân tích. Sau đây là cách bạn có thể thực hiện:
```csharp
Worksheet worksheet = workbook.Worksheets[0];
```
Thao tác này sẽ lấy trang tính đầu tiên của sổ làm việc đã tải. Bạn có thể dễ dàng sửa đổi mục lục nếu bạn đang làm việc với nhiều trang tính.
## Bước 3: Truy cập PivotTable
Tiếp tục, chúng ta hãy truy cập PivotTable trong bảng tính đã chọn của chúng ta. Nếu bạn đang sử dụng một PivotTable duy nhất, bạn có thể đặt chỉ mục của nó thành `0`:
```csharp
int pivotindex = 0;
// Truy cập PivotTable
PivotTable pivotTable = worksheet.PivotTables[pivotindex];
```
Đoạn mã này chọn PivotTable đầu tiên trong bảng tính. 
## Bước 4: Cấu hình PivotTable
Bây giờ đến phần thú vị! Hãy thiết lập PivotTable để hiển thị tổng số cho các hàng:
```csharp
pivotTable.RowGrand = true;
```
Dòng này đảm bảo báo cáo của bạn sẽ hiển thị tổng số, có thể là bản tóm tắt hữu ích cho việc phân tích dữ liệu.
## Bước 5: Truy cập và cấu hình trường hàng
Tiếp theo, chúng ta cần truy cập vào các trường hàng của PivotTable:
```csharp
Aspose.Cells.Pivot.PivotFieldCollection pivotFields = pivotTable.RowFields;
```
Bộ sưu tập này cho phép chúng ta thao tác các trường khi cần thiết.
## Cấu hình trường hàng đầu tiên
Bạn muốn thiết lập các loại tổng phụ cụ thể? Hãy truy cập vào trường đầu tiên trong bộ sưu tập của chúng ta và cấu hình nó:
```csharp
Aspose.Cells.Pivot.PivotField pivotField = pivotFields[0];
// Thiết lập Tổng phụ.
pivotField.SetSubtotals(Aspose.Cells.Pivot.PivotFieldSubtotalType.Sum, true);
pivotField.SetSubtotals(Aspose.Cells.Pivot.PivotFieldSubtotalType.Count, true);
```
Bằng cách cho phép `Sum` Và `Count` tổng phụ, chúng ta có thể nhanh chóng tóm tắt dữ liệu trong báo cáo của mình.
## Bước 6: Thiết lập tùy chọn tự động sắp xếp
Tiếp theo, hãy đưa một số sắp xếp thông minh vào hoạt động. Theo cách này, PivotTable của bạn sẽ sắp xếp dữ liệu theo thứ tự có ý nghĩa:
```csharp
// Thiết lập tùy chọn tự động sắp xếp.
pivotField.IsAutoSort = true;
pivotField.IsAscendSort = true;
pivotField.AutoSortField = -5; // Sử dụng trường sắp xếp được xác định trước.
```
Đoạn mã này cho phép sắp xếp tự động và chỉ định thứ tự tăng dần. 
## Bước 7: Thiết lập tùy chọn AutoShow
Bạn có muốn lọc dữ liệu của mình thêm không? Tùy chọn AutoShow hữu ích để hiển thị các điểm dữ liệu cụ thể theo các điều kiện được xác định:
```csharp
// Thiết lập tùy chọn tự động hiển thị.
pivotField.IsAutoShow = true;
pivotField.IsAscendShow = false;
pivotField.AutoShowField = 0; // Chỉ định trường để tự động hiển thị.
```
Điều này đảm bảo rằng PivotTable của bạn chỉ hiển thị dữ liệu có liên quan, tăng cường tính rõ ràng và tập trung.
## Bước 8: Lưu công việc của bạn
Sau tất cả những cấu hình đó, bạn sẽ không muốn mất công sức của mình! Lưu sổ làm việc đã sửa đổi như thế này:
```csharp
workbook.Save(dataDir + "output.xls");
```
Bây giờ, bạn có thể tìm thấy tệp Excel mới tạo trong thư mục tài liệu của mình.
## Phần kết luận
Và bạn đã có nó! Chúng tôi đã hướng dẫn một cách tiếp cận toàn diện và thực tế để thiết lập định dạng trường trang theo chương trình trong PivotTable bằng Aspose.Cells cho .NET. Với các bước đơn giản được cung cấp, bạn sẽ cảm thấy tự tin khi sửa đổi dữ liệu Excel của mình để phù hợp với nhu cầu báo cáo của bạn. Thật đáng kinh ngạc những gì bạn có thể đạt được khi kết hợp sức mạnh của C# với Aspose.Cells.
## Câu hỏi thường gặp
### Aspose.Cells là gì?
Aspose.Cells là thư viện .NET cho phép các nhà phát triển tạo, thao tác và chuyển đổi các tệp Excel theo cách lập trình.
### Làm thế nào để cài đặt Aspose.Cells?
Bạn có thể tải xuống trực tiếp từ [Trang web Aspose](https://releases.aspose.com/cells/net/).
### Tôi có thể sử dụng Aspose.Cells mà không cần cài đặt Excel không?
Có, Aspose.Cells là một thư viện độc lập không yêu cầu phải cài đặt Microsoft Excel.
### Tôi có thể tìm thấy hỗ trợ chi tiết ở đâu?
Bạn có thể truy cập hỗ trợ chi tiết và diễn đàn tại [Hỗ trợ Aspose](https://forum.aspose.com/c/cells/9).
### Tôi có thể xin giấy phép tạm thời bằng cách nào?
Bạn có thể có được giấy phép tạm thời từ [đây](https://purchase.aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}