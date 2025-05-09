---
"description": "Tìm hiểu cách chuyển đổi JSON sang CSV theo chương trình trong .NET bằng Aspose.Cells. Làm theo hướng dẫn từng bước của chúng tôi để đảm bảo chuyển đổi dữ liệu liền mạch."
"linktitle": "Chuyển đổi JSON sang CSV theo chương trình trong .NET"
"second_title": "API xử lý Excel Aspose.Cells .NET"
"title": "Chuyển đổi JSON sang CSV theo chương trình trong .NET"
"url": "/vi/net/converting-excel-files-to-other-formats/converting-json-to-csv/"
"weight": 15
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Chuyển đổi JSON sang CSV theo chương trình trong .NET

## Giới thiệu
Trong thế giới kỹ thuật số ngày nay, việc xử lý dữ liệu ở nhiều định dạng đã trở nên phổ biến và JSON (JavaScript Object Notation) là một trong những định dạng được sử dụng rộng rãi nhất để trao đổi dữ liệu. Nhưng điều gì xảy ra khi bạn cần chuyển đổi JSON đó thành định dạng dễ phân tích hơn, như CSV (Comma Separated Values)? Hướng dẫn này sẽ hướng dẫn bạn quy trình chuyển đổi JSON sang CSV theo chương trình bằng Aspose.Cells for .NET—một API thao tác bảng tính dễ sử dụng nhưng mạnh mẽ. 
## Điều kiện tiên quyết
Trước khi đi sâu vào mã, điều quan trọng là phải đảm bảo bạn có tất cả các thành phần cần thiết và hiểu biết cơ bản về các công cụ chúng ta sẽ sử dụng. Hãy phác thảo những gì bạn cần:
- Aspose.Cells cho .NET: Đây là thư viện chính mà chúng ta sẽ sử dụng để chuyển đổi JSON sang CSV. Bạn có thể [tải xuống ở đây](https://releases.aspose.com/cells/net/).
- Visual Studio: Bạn sẽ cần một môi trường phát triển tích hợp (IDE) như Visual Studio để viết và thực thi mã .NET.
- .NET Framework: Đảm bảo bạn đã cài đặt .NET Framework. Aspose.Cells tương thích với cả .NET Core và .NET Framework.
- Kiến thức cơ bản về C#: Mặc dù hướng dẫn này sẽ phân tích từng phần của mã, nhưng sẽ hữu ích hơn nếu bạn đã quen với C#.
## Nhập gói
Để sử dụng Aspose.Cells trong dự án .NET của bạn, trước tiên bạn cần cài đặt thư viện. Bạn có thể thực hiện việc này thông qua NuGet Package Manager:
1. Mở Visual Studio.
2. Vào Công cụ > Trình quản lý gói NuGet > Quản lý gói NuGet cho Solution.
3. Tìm kiếm Aspose.Cells và cài đặt phiên bản mới nhất.
Sau khi cài đặt, hãy đảm bảo bạn bao gồm các không gian tên sau vào mã của mình:
```csharp
using Aspose.Cells.Utility;
using System;
using System.IO;
```
Bây giờ mọi thứ đã được thiết lập, chúng ta hãy phân tích mã theo từng bước để bạn có thể thấy cách dễ dàng chuyển đổi tệp JSON sang CSV bằng Aspose.Cells.
## Bước 1: Đọc tệp JSON
Điều đầu tiên chúng ta cần làm là đọc dữ liệu JSON từ một tệp. Chúng tôi sẽ giả sử bạn đã có một tệp JSON (hãy gọi nó là `SampleJson.json`) được lưu trữ trong một thư mục trên hệ thống của bạn.
Bạn có thể sử dụng `File.ReadAllText()` phương pháp trong C# để đọc nội dung của tệp JSON thành chuỗi.
```csharp
// Thư mục nguồn
string sourceDir = "Your Document Directory";
// Đọc tệp JSON
string str = File.ReadAllText(sourceDir + "SampleJson.json");
```

Bước này rất quan trọng vì bạn cần dữ liệu JSON thô để bắt đầu quá trình chuyển đổi. Bằng cách đọc nó dưới dạng chuỗi, bạn đang chuẩn bị để Aspose.Cells xử lý.
## Bước 2: Tạo một Workbook trống
Aspose.Cells hoạt động chủ yếu trên sổ làm việc (tệp Excel). Để bắt đầu nhập dữ liệu JSON, trước tiên bạn cần tạo một sổ làm việc trống nơi dữ liệu này sẽ được chèn vào.
```csharp
// Tạo sổ làm việc trống
Workbook workbook = new Workbook();
```
Ở đây, bạn đang khởi tạo một sổ làm việc trống cuối cùng sẽ chứa dữ liệu định dạng CSV. Hãy nghĩ về việc tạo một bảng tính trống trong Excel sẽ sớm được điền dữ liệu JSON của bạn.
## Bước 3: Truy cập các ô trong sổ làm việc
Bây giờ chúng ta có một bảng tính trống, chúng ta cần truy cập vào các ô của nó. `Cells` bộ sưu tập trong Aspose.Cells đại diện cho tất cả các ô trong một bảng tính, nơi bạn sẽ đặt dữ liệu JSON của mình.
```csharp
// Nhận tế bào
Cells cells = workbook.Worksheets[0].Cells;
```
Đoạn mã này chọn trang tính đầu tiên (trang tính ở chỉ mục 0) và lấy `Cells` bộ sưu tập. Các ô này giống như lưới của bảng tính nơi dữ liệu sẽ được thêm vào.
## Bước 4: Thiết lập JsonLayoutOptions
Aspose.Cells cung cấp một số tùy chọn tùy chỉnh về cách dữ liệu JSON của bạn sẽ được nhập. Ở đây, chúng tôi định nghĩa `JsonLayoutOptions` để chỉ định cách Aspose xử lý mảng, dữ liệu số và tiêu đề đối tượng.
```csharp
// Đặt JsonLayoutOptions
JsonLayoutOptions importOptions = new JsonLayoutOptions();
importOptions.ConvertNumericOrDate = true;
importOptions.ArrayAsTable = true;
importOptions.IgnoreArrayTitle = true;
importOptions.IgnoreObjectTitle = true;
```

- ConvertNumericOrDate: Tự động chuyển đổi các giá trị chuỗi là giá trị số hoặc giá trị ngày.
- ArrayAsTable: Xử lý các mảng trong JSON như các bảng trong sổ làm việc.
- IgnoreArrayTitle và IgnoreObjectTitle: Các tùy chọn này bỏ qua tiêu đề của mảng và đối tượng, đảm bảo rằng chỉ có dữ liệu thô được nhập.
## Bước 5: Nhập dữ liệu JSON
Sau khi các tùy chọn bố cục được thiết lập, đã đến lúc đưa dữ liệu JSON vào. `JsonUtility.ImportData()` phương pháp này thực hiện công việc khó khăn ở đây, chèn dữ liệu JSON vào các ô của sổ làm việc.
```csharp
JsonUtility.ImportData(str, cells, 0, 0, importOptions);
```
Phương pháp này có một số tham số:
- `str`: Chuỗi JSON mà chúng ta đã đọc ở Bước 1.
- `cells`: Tập hợp các ô nơi dữ liệu sẽ được đưa vào.
- `0, 0`:Đây là các chỉ mục hàng và cột cho biết dữ liệu sẽ bắt đầu từ đâu (tức là góc trên cùng bên trái).
- `importOptions`: Các tùy chọn bố cục mà chúng ta thiết lập ở Bước 4.
## Bước 6: Lưu sổ làm việc dưới dạng CSV
Bây giờ dữ liệu JSON đã có trong sổ làm việc, chúng ta có thể dễ dàng lưu sổ làm việc dưới dạng tệp CSV. CSV là định dạng đơn giản, nhẹ để lưu trữ dữ liệu dạng bảng, rất lý tưởng cho việc phân tích dữ liệu.
```csharp
// Thư mục đầu ra
string outputDir = "Your Document Directory";
// Lưu sổ làm việc
workbook.Save(outputDir + @"SampleJson_out.csv");
```
Trong bước này, chúng ta lưu sổ làm việc dưới dạng tệp CSV. Bạn chỉ định đường dẫn và tên tệp (`SampleJson_out.csv`) nơi tệp CSV sẽ được lưu.
## Bước 7: Xác nhận quy trình
Để đảm bảo mọi thứ hoạt động như mong đợi, chúng ta có thể in thông báo xác nhận trong bảng điều khiển.
```csharp
Console.WriteLine("ConvertJsonToCsv executed successfully.");
```
Một thông báo thành công đơn giản sẽ giúp xác nhận quá trình diễn ra suôn sẻ.
## Phần kết luận
Chuyển đổi JSON sang CSV bằng Aspose.Cells cho .NET là một quá trình đơn giản nhưng mạnh mẽ. Chỉ với một vài dòng mã, bạn có thể chuyển đổi dữ liệu JSON phức tạp thành định dạng CSV dễ truy cập hơn. Cho dù bạn đang xử lý mảng, đối tượng hay dữ liệu số, Aspose.Cells giúp bạn dễ dàng cấu hình quy trình chuyển đổi để phù hợp với nhu cầu của mình.
## Câu hỏi thường gặp
### Aspose.Cells có thể xử lý các tệp JSON lớn không?
Có, Aspose.Cells được thiết kế để xử lý các tập dữ liệu lớn một cách hiệu quả, phù hợp để xử lý các tệp JSON lớn mà không gặp vấn đề về hiệu suất.
### Làm thế nào tôi có thể tùy chỉnh đầu ra CSV?
Bạn có thể tùy chỉnh đầu ra CSV bằng cách điều chỉnh `JsonLayoutOptions` hoặc thay đổi định dạng của sổ làm việc trước khi lưu dưới dạng CSV.
### Có cách nào để loại trừ một số dữ liệu nhất định khỏi JSON trong quá trình chuyển đổi không?
Có, bằng cách điều chỉnh JSON hoặc sử dụng logic mã tùy chỉnh trước khi nhập, bạn có thể loại trừ hoặc lọc ra các trường dữ liệu cụ thể.
### Aspose.Cells có hỗ trợ các định dạng tệp khác ngoài CSV không?
Chắc chắn rồi! Aspose.Cells hỗ trợ nhiều định dạng khác nhau bao gồm Excel (XLS, XLSX), PDF, HTML và nhiều định dạng khác nữa.
### Làm thế nào tôi có thể dùng thử Aspose.Cells miễn phí?
Bạn có thể [tải xuống bản dùng thử miễn phí tại đây](https://releases.aspose.com/) để kiểm tra tất cả các tính năng trước khi mua.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}