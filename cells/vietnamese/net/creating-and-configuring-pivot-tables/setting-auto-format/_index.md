---
"description": "Tìm hiểu cách thiết lập định dạng tự động cho bảng trục Excel theo chương trình bằng Aspose.Cells cho .NET trong hướng dẫn từng bước chi tiết này."
"linktitle": "Thiết lập Định dạng Tự động của Bảng Pivot theo Chương trình trong .NET"
"second_title": "API xử lý Excel Aspose.Cells .NET"
"title": "Thiết lập Định dạng Tự động của Bảng Pivot theo Chương trình trong .NET"
"url": "/vi/net/creating-and-configuring-pivot-tables/setting-auto-format/"
"weight": 18
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Thiết lập Định dạng Tự động của Bảng Pivot theo Chương trình trong .NET

## Giới thiệu
Khi nói đến việc phân tích dữ liệu, các bảng trục trong Excel có thể là một công cụ thay đổi cuộc chơi. Chúng cho phép bạn tóm tắt và phân tích dữ liệu một cách năng động, giúp bạn thu thập những thông tin chi tiết mà gần như không thể trích xuất theo cách thủ công. Nhưng nếu bạn muốn tự động hóa quá trình định dạng các bảng trục của mình trong .NET thì sao? Ở đây, tôi sẽ chỉ cho bạn cách lập trình để thiết lập định dạng tự động của một bảng trục bằng cách sử dụng thư viện Aspose.Cells mạnh mẽ cho .NET.
Trong hướng dẫn này, chúng ta sẽ khám phá những điều cần thiết, hướng dẫn qua các điều kiện tiên quyết, nhập các gói cần thiết và sau đó đi sâu vào hướng dẫn từng bước để giúp bạn định dạng bảng trục như một chuyên gia. Nghe có vẻ hay phải không? Hãy bắt đầu ngay thôi!
## Điều kiện tiên quyết
Trước khi bắt đầu, hãy đảm bảo rằng bạn có mọi thứ cần thiết để bắt đầu:
1. Môi trường phát triển .NET: Đảm bảo bạn có phiên bản Visual Studio đang hoạt động (hoặc bất kỳ IDE nào hỗ trợ .NET).
2. Thư viện Aspose.Cells: Để làm việc với các tệp Excel một cách trơn tru, bạn sẽ cần cài đặt thư viện Aspose.Cells. Nếu bạn chưa cài đặt, bạn có thể tải xuống từ [trang tải xuống](https://releases.aspose.com/cells/net/).
3. Kiến thức cơ bản về C#: Sự quen thuộc với lập trình C# sẽ giúp bạn hiểu các bước tốt hơn.
4. Tệp Excel (Mẫu): Bạn sẽ cần một tệp mẫu Excel để bắt đầu, tệp này sẽ được xử lý trong ví dụ của chúng tôi. Để đơn giản, bạn có thể tạo một tệp mẫu có tên `Book1.xls`.
## Nhập gói
Để bắt đầu sử dụng Aspose.Cells trong dự án của bạn, bạn sẽ cần phải nhập các gói cần thiết. Sau đây là cách bạn có thể thiết lập điều đó trong dự án .NET của mình:
### Tạo một dự án mới
Bắt đầu bằng cách tạo một dự án .NET mới trong IDE mà bạn thích. 
### Thêm tài liệu tham khảo
Đảm bảo thêm tham chiếu đến thư viện Aspose.Cells. Nếu bạn đã tải xuống thư viện, hãy thêm DLL từ bản trích xuất. Nếu bạn đang sử dụng NuGet, bạn chỉ cần chạy:
```bash
Install-Package Aspose.Cells
```
### Nhập không gian tên
Bây giờ, trong tệp mã của bạn, bạn sẽ cần nhập không gian tên Aspose.Cells. Bạn có thể thực hiện việc này bằng cách thêm dòng sau vào đầu tệp C# của bạn:
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
using Aspose.Cells.Pivot;
```
Sau khi hoàn tất các bước trên, bạn đã sẵn sàng để viết code!
Bây giờ, chúng ta hãy phân tích mã bạn cung cấp thành các bước chi tiết kèm theo lời giải thích về chức năng của từng phần. 
## Bước 1: Xác định thư mục tài liệu của bạn
Để bắt đầu, bạn cần thiết lập đường dẫn đến thư mục tài liệu nơi chứa các tệp Excel của bạn. Trong ví dụ của chúng tôi, chúng tôi sẽ định nghĩa nó như sau:
```csharp
string dataDir = "Your Document Directory";  // Sửa đổi khi cần thiết
```
Dòng này tạo ra một biến chuỗi `dataDir` giữ đường dẫn tệp đến tài liệu của bạn. Hãy đảm bảo thay thế `"Your Document Directory"` với đường dẫn thực tế trên hệ thống của bạn.
## Bước 2: Tải tệp mẫu
Tiếp theo, bạn sẽ muốn tải một bảng tính hiện có chứa bảng trục của bạn:
```csharp
Workbook workbook = new Workbook(dataDir + "Book1.xls");
```
Dòng này khởi tạo một cái mới `Workbook` đối tượng bằng cách tải tệp Excel đã chỉ định. Tệp phải chứa ít nhất một bảng trục để các bước tiếp theo có hiệu lực.
## Bước 3: Truy cập vào bảng tính mong muốn
Xác định bảng tính nào bạn cần làm việc để truy cập bảng trục. Trong trường hợp này, chúng ta sẽ chỉ lấy bảng tính đầu tiên:
```csharp
int pivotIndex = 0;  // Mục lục của Bảng Pivot
Worksheet worksheet = workbook.Worksheets[0];
```
Đây, `worksheet` lấy lại bảng tính đầu tiên từ sổ làm việc. Chỉ mục bảng trục được đặt thành `0`, nghĩa là chúng ta đang truy cập bảng trục đầu tiên trong bảng tính đó.
## Bước 4: Xác định vị trí Bảng Pivot
Sau khi đã có bảng tính, đã đến lúc truy cập vào bảng tổng hợp của bạn:
```csharp
PivotTable pivotTable = worksheet.PivotTables[pivotIndex];
```
Điều này khởi tạo một cái mới `PivotTable` đối tượng bằng cách lấy bảng trục ở chỉ mục đã chỉ định từ bảng tính.
## Bước 5: Thiết lập Thuộc tính Định dạng Tự động
Bây giờ đến phần quan trọng: thiết lập tùy chọn định dạng tự động cho bảng trục của bạn.
```csharp
pivotTable.IsAutoFormat = true; // Bật định dạng tự động
```
Dòng này cho phép tính năng định dạng tự động cho bảng trục. Khi được đặt thành `true`, bảng trục sẽ tự động định dạng dựa trên các kiểu được xác định trước.
## Bước 6: Chọn một loại định dạng tự động cụ thể
Chúng tôi cũng muốn chỉ định kiểu định dạng tự động nào mà bảng trục nên áp dụng. Aspose.Cells có nhiều định dạng khác nhau mà chúng ta có thể lựa chọn. Sau đây là cách thiết lập:
```csharp
pivotTable.AutoFormatType = Aspose.Cells.Pivot.PivotTableAutoFormatType.Report5;
```
Với dòng này, chúng ta chỉ định một kiểu định dạng tự động cụ thể cho bảng trục. `Report5` chỉ là một ví dụ về một phong cách; bạn có thể lựa chọn từ nhiều tùy chọn khác nhau tùy theo nhu cầu của mình. 
## Bước 7: Lưu sổ làm việc
Cuối cùng, đừng quên lưu bảng tính của bạn sau khi thực hiện tất cả các thay đổi:
```csharp
workbook.Save(dataDir + "output.xls");
```
Dòng mã này lưu sổ làm việc đã sửa đổi vào một tệp mới có tên là `output.xls` trong thư mục đã chỉ định. Hãy đảm bảo kiểm tra tệp này để xem bảng trục được định dạng đẹp mắt của bạn!
## Phần kết luận
Xin chúc mừng! Bạn vừa lập trình một bảng trục Excel để tự động định dạng bằng Aspose.Cells trong .NET. Quy trình này không chỉ giúp bạn tiết kiệm thời gian khi chuẩn bị báo cáo mà còn đảm bảo tính nhất quán về cách dữ liệu của bạn trông như thế nào sau mỗi lần chạy. Chỉ với một vài dòng mã, bạn có thể cải thiện đáng kể các tệp Excel của mình—giống như một nhà ảo thuật kỹ thuật số.
## Câu hỏi thường gặp
### Aspose.Cells là gì?
Aspose.Cells là một thư viện .NET mạnh mẽ để xử lý các tệp Excel mà không cần cài đặt Microsoft Excel.
### Tôi có thể định dạng nhiều bảng trục trong một bảng tính không?
Có, bạn có thể lặp qua nhiều đối tượng bảng trục trong sổ làm việc của mình để định dạng chúng từng cái một.
### Có bản dùng thử miễn phí cho Aspose.Cells không?
Chắc chắn rồi! Bạn có thể bắt đầu với phiên bản dùng thử miễn phí có sẵn [đây](https://releases.aspose.com/).
### Nếu bảng trục của tôi không được định dạng đúng thì sao?
Đảm bảo rằng bảng trục được tham chiếu chính xác và có loại định dạng tự động—nếu không, bảng có thể trở về cài đặt mặc định.
### Tôi có thể tự động hóa quy trình này bằng các tác vụ đã lên lịch không?
Có! Bằng cách kết hợp mã này vào tác vụ theo lịch trình, bạn có thể tự động tạo báo cáo và định dạng thường xuyên.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}