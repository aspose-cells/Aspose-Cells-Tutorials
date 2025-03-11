---
title: Pivot Table Sắp xếp tùy chỉnh theo chương trình trong .NET
linktitle: Pivot Table Sắp xếp tùy chỉnh theo chương trình trong .NET
second_title: API xử lý Excel Aspose.Cells .NET
description: Tìm hiểu cách sắp xếp theo chương trình Pivot Tables trong .NET bằng Aspose.Cells. Hướng dẫn từng bước bao gồm thiết lập, cấu hình, sắp xếp và lưu kết quả dưới dạng tệp Excel và PDF.
weight: 29
url: /vi/net/creating-and-configuring-pivot-tables/pivot-table-custom-sort/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Pivot Table Sắp xếp tùy chỉnh theo chương trình trong .NET

## Giới thiệu
Khi nói đến việc làm việc với Excel trong môi trường .NET, có một thư viện nổi bật hơn hẳn so với các thư viện còn lại: Aspose.Cells. Bây giờ, bạn có thích không khi một công cụ cho phép bạn thao tác bảng tính theo chương trình? Đó chính xác là những gì Aspose.Cells làm! Trong hướng dẫn hôm nay, chúng ta sẽ đi sâu vào thế giới của Pivot Table và chỉ cho bạn cách triển khai sắp xếp tùy chỉnh theo chương trình bằng thư viện đa năng này.
## Điều kiện tiên quyết
Trước khi bắt tay vào viết mã, hãy đảm bảo rằng bạn đã chuẩn bị một số thứ sau:
1. Visual Studio: Bạn sẽ cần một phiên bản Visual Studio đang hoạt động. Đây là sân chơi nơi mọi điều kỳ diệu diễn ra.
2. .NET Framework: Sự quen thuộc với lập trình .NET là điều cần thiết. Cho dù bạn là người đam mê .NET Core hay .NET Framework, bạn đều có thể bắt đầu.
3.  Thư viện Aspose.Cells: Bạn cần cài đặt thư viện Aspose.Cells. Bạn có thể lấy nó từ[Liên kết tải xuống](https://releases.aspose.com/cells/net/) và thêm nó vào dự án của bạn.
4. Hiểu biết cơ bản về Bảng Pivot: Mặc dù bạn không cần phải là chuyên gia, nhưng một chút kiến thức về cách hoạt động của Bảng Pivot sẽ có ích khi chúng ta thực hiện hướng dẫn này.
5.  Tệp Excel mẫu: Có một tệp Excel mẫu có tên`SamplePivotSort.xlsx` sẵn sàng trong thư mục làm việc của bạn để thử nghiệm.
## Nhập gói
Sau khi bạn đã sắp xếp xong tất cả các điều kiện tiên quyết, bước đầu tiên là nhập các gói cần thiết. Để thực hiện việc này, hãy bao gồm các dòng sau ở đầu mã của bạn:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells;
using Aspose.Cells.Pivot;
```
Gói này cung cấp tất cả các chức năng bạn cần để xử lý tệp Excel bằng Aspose.Cells.

Được rồi, chúng ta hãy cùng đến với phần thú vị! Chúng ta sẽ chia nhỏ quy trình tạo Bảng Pivot và áp dụng sắp xếp tùy chỉnh thành các bước dễ quản lý.
## Bước 1: Thiết lập sổ làm việc
Để bắt đầu, chúng ta cần thiết lập sổ làm việc của mình. Sau đây là cách thực hiện:
```csharp
string sourceDir = "Your Document Directory";
string outputDir = "Your Document Directory";
Workbook wb = new Workbook(sourceDir + "SamplePivotSort.xlsx");
```
 Trong bước này, chúng tôi khởi tạo một cái mới`Workbook` trường hợp có đường dẫn đến tệp Excel của chúng ta. Điều này đóng vai trò như một khung vẽ nơi Bảng Pivot của chúng ta sẽ trở nên sống động.
## Bước 2: Truy cập vào Bảng tính
Tiếp theo, chúng ta cần truy cập vào bảng tính nơi chúng ta sẽ thêm Bảng Pivot.
```csharp
Worksheet sheet = wb.Worksheets[0];
PivotTableCollection pivotTables = sheet.PivotTables;
```
 Ở đây, chúng ta lấy bảng tính đầu tiên trong sổ làm việc của mình và gọi`PivotTableCollection`. Bộ sưu tập này cho phép chúng ta quản lý tất cả các Bảng Pivot trên bảng tính này.
## Bước 3: Tạo Bảng Pivot đầu tiên của bạn
Bây giờ là lúc tạo Bảng Pivot của chúng ta.
```csharp
int index = pivotTables.Add("=Sheet1!A1:C10", "E3", "PivotTable1");
PivotTable pivotTable = pivotTables[index];
```
Chúng tôi thêm một Bảng Pivot mới vào bảng tính của mình, chỉ định phạm vi dữ liệu và vị trí của nó. "E3" cho biết nơi chúng tôi muốn Bảng Pivot của mình bắt đầu. Sau đó, chúng tôi tham chiếu Bảng Pivot mới này bằng chỉ mục của nó.
## Bước 4: Cấu hình Cài đặt Bảng Pivot
Hãy cấu hình Bảng Pivot của chúng ta! Điều này có nghĩa là kiểm soát các khía cạnh như tổng số và sắp xếp trường.
```csharp
pivotTable.RowGrand = false;
pivotTable.ColumnGrand = false;
pivotTable.AddFieldToArea(PivotFieldType.Row,1);
PivotField rowField = pivotTable.RowFields[0];
rowField.IsAutoSort = true;
rowField.IsAscendSort = true;
```
Chúng tôi đảm bảo rằng tổng số cho các hàng và cột không được hiển thị, điều này có thể làm cho dữ liệu sạch hơn. Sau đó, chúng tôi thêm trường đầu tiên vào vùng hàng, cho phép tự động sắp xếp và sắp xếp theo thứ tự tăng dần.
## Bước 5: Thêm Cột và Trường Dữ liệu
Sau khi thiết lập các hàng, hãy thêm cột và trường dữ liệu.
```csharp
pivotTable.AddFieldToArea(PivotFieldType.Column,0);
PivotField colField = pivotTable.ColumnFields[0];
colField.NumberFormat = "dd/mm/yyyy";
colField.IsAutoSort = true;
colField.IsAscendSort = true;
```
Chúng tôi thêm trường thứ hai dưới dạng cột và định dạng nó thành ngày. Một lần nữa, chúng tôi bật tính năng tự động sắp xếp và thứ tự tăng dần để giữ mọi thứ được sắp xếp. Cuối cùng, chúng tôi cần thêm trường thứ ba vào vùng dữ liệu của mình:
```csharp
pivotTable.AddFieldToArea(PivotFieldType.Data,2);
```
## Bước 6: Làm mới và tính toán Bảng Pivot
Sau khi thêm tất cả các trường cần thiết, hãy đảm bảo Bảng Pivot của chúng ta đã mới và sẵn sàng.
```csharp
pivotTable.RefreshData();
pivotTable.CalculateData();
```
Các phương pháp này làm mới dữ liệu và tính toán lại, đảm bảo mọi thứ được cập nhật và hiển thị chính xác trong Bảng Pivot của chúng tôi.
## Bước 7: Sắp xếp tùy chỉnh dựa trên giá trị trường hàng
Hãy thêm một chút thú vị bằng cách sắp xếp Bảng Pivot dựa trên các giá trị cụ thể, như "Hải sản".
```csharp
index = pivotTables.Add("=Sheet1!A1:C10", "E10", "PivotTable2");
pivotTable = pivotTables[index];
```
Chúng tôi đang lặp lại quy trình bằng cách tạo một Bảng Pivot khác và thiết lập tương tự như Bảng đầu tiên. Bây giờ chúng ta có thể tùy chỉnh thêm:
```csharp
pivotTable.AddFieldToArea(PivotFieldType.Row,1);
rowField = pivotTable.RowFields[0];
rowField.IsAutoSort = true;
rowField.IsAscendSort = true;
```
## Bước 8: Tùy chỉnh sắp xếp bổ sungHãy thử một phương pháp sắp xếp khác dựa trên một ngày cụ thể:
```csharp
// Thêm một Bảng Pivot khác để sắp xếp theo ngày
index = pivotTables.Add("=Sheet1!A1:C10", "E18", "PivotTable3");
pivotTable = pivotTables[index];
// Lặp lại các thiết lập hàng và cột tương tự như các bước trước đó
```
Bạn chỉ cần lặp lại quy trình tương tự, tạo Bảng Pivot thứ ba với tiêu chí sắp xếp phù hợp với nhu cầu của bạn.
## Bước 9: Lưu sổ làm việcĐã đến lúc lưu lại mọi công sức mà chúng ta đã bỏ ra!
```csharp
wb.Save(outputDir + "out.xlsx");
PdfSaveOptions options = new PdfSaveOptions();
options.OnePagePerSheet = true;
wb.Save(outputDir + "out.pdf", options);
```
 Tại đây, bạn lưu sổ làm việc dưới dạng tệp Excel và PDF.`PdfSaveOptions` cho phép định dạng tốt hơn, đảm bảo mỗi trang tính xuất hiện trên một trang riêng biệt khi chuyển đổi.
## Bước 10: Kết thúcKết thúc bằng cách cho người dùng biết mọi thứ đều ổn.
```csharp
Console.WriteLine("PivotTableCustomSort executed successfully.");
```
## Phần kết luận
Bây giờ, bạn đã biết cách khai thác sức mạnh của Aspose.Cells để tạo và tùy chỉnh Pivot Table trong các ứng dụng .NET của mình. Từ thiết lập ban đầu đến sắp xếp tùy chỉnh, mỗi bước kết hợp lại để mang lại trải nghiệm liền mạch. Cho dù bạn cần trình bày dữ liệu bán hàng hàng năm hay theo dõi số liệu thống kê hàng tồn kho, những kỹ năng này sẽ phục vụ bạn rất tốt!
## Câu hỏi thường gặp
### Bảng Pivot là gì?
Bảng Pivot là công cụ xử lý dữ liệu trong Excel cho phép bạn tóm tắt và phân tích dữ liệu, cung cấp một cách linh hoạt để dễ dàng trích xuất thông tin chi tiết.
### Làm thế nào để cài đặt Aspose.Cells?
 Bạn có thể cài đặt nó thông qua NuGet trong Visual Studio hoặc tải xuống trực tiếp từ[Liên kết tải xuống](https://releases.aspose.com/cells/net/).
### Có phiên bản dùng thử của Aspose.Cells không?
 Vâng! Bạn có thể dùng thử miễn phí bằng cách truy cập[Liên kết dùng thử miễn phí](https://releases.aspose.com/).
### Tôi có thể sắp xếp nhiều trường trong một Bảng Pivot không?
Chắc chắn rồi! Bạn có thể thêm và sắp xếp nhiều trường dựa trên yêu cầu của mình.
### Tôi có thể tìm thấy hỗ trợ cho Aspose.Cells ở đâu?
 Cộng đồng này khá năng động và bạn có thể đặt câu hỏi trên diễn đàn của họ[đây](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
