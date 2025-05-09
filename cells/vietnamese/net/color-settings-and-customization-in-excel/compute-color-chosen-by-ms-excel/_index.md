---
"description": "Tìm hiểu cách tính toán màu được MS Excel chọn bằng Aspose.Cells cho .NET. Thực hiện theo hướng dẫn từng bước này để truy cập màu định dạng có điều kiện của Excel theo chương trình."
"linktitle": "Tính toán màu được chọn bởi MS Excel theo chương trình"
"second_title": "API xử lý Excel Aspose.Cells .NET"
"title": "Tính toán màu được chọn bởi MS Excel theo chương trình"
"url": "/vi/net/color-settings-and-customization-in-excel/compute-color-chosen-by-ms-excel/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Tính toán màu được chọn bởi MS Excel theo chương trình

## Giới thiệu
Bạn đã bao giờ làm việc với các tệp Excel và tự hỏi làm thế nào một số màu nhất định được tự động chọn để định dạng chưa? Bạn không đơn độc. Định dạng có điều kiện của Excel có thể hơi bí ẩn, đặc biệt là khi cố gắng trích xuất màu chính xác mà Excel chỉ định. Nhưng đừng lo lắng, chúng tôi đã hỗ trợ bạn! Trong hướng dẫn này, chúng ta sẽ đi sâu vào cách tính toán theo chương trình màu được MS Excel chọn bằng Aspose.Cells cho .NET. Chúng tôi sẽ chia nhỏ từng bước để bạn có thể làm theo và áp dụng vào các dự án của riêng mình một cách dễ dàng. Hãy bắt đầu thôi!
## Điều kiện tiên quyết
Trước khi tìm hiểu mã, chúng ta hãy xem qua những gì bạn cần để làm theo hướng dẫn này:
- Aspose.Cells cho .NET đã được cài đặt. Nếu bạn chưa có, bạn có thể [tải xuống ở đây](https://releases.aspose.com/cells/net/).
- Có kiến thức cơ bản về C# và .NET framework.
- Một tệp Excel mẫu (Book1.xlsx) có áp dụng một số định dạng có điều kiện.
Bạn cũng có thể dùng thử miễn phí Aspose.Cells cho .NET nếu bạn chưa có giấy phép. Tải phiên bản dùng thử [đây](https://releases.aspose.com/).
## Nhập gói
Trước khi bắt đầu mã hóa, chúng ta cần nhập các gói cần thiết để đảm bảo mọi thứ chạy trơn tru. Đảm bảo bạn bao gồm các không gian tên sau trong dự án của mình:
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
using System;
```
Các bản nhập này cung cấp quyền truy cập vào các lớp Aspose.Cells chính và thư viện vẽ hệ thống gốc của .NET để xử lý màu sắc.

Bây giờ chúng ta đã có mọi thứ, hãy chia nhỏ nhiệm vụ này thành các bước dễ thực hiện:
## Bước 1: Thiết lập đối tượng Workbook
Điều đầu tiên chúng ta cần làm là khởi tạo một `Workbook` đối tượng và tải tệp Excel mà chúng ta muốn làm việc. Đây là nơi cuộc hành trình bắt đầu!
```csharp
// Đường dẫn đến thư mục tài liệu.
string dataDir = "Your Document Directory";
// Khởi tạo một đối tượng sổ làm việc và mở tệp mẫu
Workbook workbook = new Workbook(dataDir + "Book1.xlsx");
```
Trong bước này, chúng tôi đang tạo một phiên bản mới của `Workbook` lớp từ Aspose.Cells. `Workbook` lớp biểu thị một tệp Excel và bằng cách cung cấp đường dẫn đến tệp của chúng ta, chúng ta có thể dễ dàng tải tệp đó để thao tác thêm.
## Bước 2: Truy cập vào Bảng tính đầu tiên
Sau khi tải xong bảng tính, chúng ta cần truy cập vào trang tính cụ thể mà chúng ta muốn trích xuất màu. Trong ví dụ này, chúng ta sẽ làm việc với trang tính đầu tiên.
```csharp
// Nhận bảng tính đầu tiên
Worksheet worksheet = workbook.Worksheets[0];
```
Ở đây, chúng tôi đang lấy bảng tính đầu tiên trong sổ làm việc bằng cách sử dụng `Worksheets[0]` chỉ mục. Aspose.Cells cho phép bạn truy cập bất kỳ bảng tính nào trong tệp Excel theo chỉ mục hoặc tên của nó.
## Bước 3: Chọn ô quan tâm
Tiếp theo, chúng ta sẽ chọn một ô cụ thể trong bảng tính. Đối với hướng dẫn này, chúng ta sẽ tập trung vào ô "A1", nhưng bạn có thể chọn bất kỳ ô nào có áp dụng định dạng có điều kiện.
```csharp
// Lấy ô A1
Cell a1 = worksheet.Cells["A1"];
```
Chúng tôi sử dụng `Cells` thuộc tính để tham chiếu đến một ô cụ thể theo địa chỉ của nó. Trong trường hợp này, chúng tôi chọn ô “A1” vì chúng tôi muốn trích xuất kết quả định dạng có điều kiện được áp dụng cho ô này.
## Bước 4: Lấy kết quả định dạng có điều kiện
Bây giờ, đây là nơi phép thuật xảy ra! Chúng ta sẽ sử dụng Aspose.Cells để lấy kết quả định dạng có điều kiện cho ô đã chọn. Đây là cách Excel tính toán định dạng động, bao gồm cả màu sắc.
```csharp
// Nhận đối tượng kết quả định dạng có điều kiện
ConditionalFormattingResult cfr1 = a1.GetConditionalFormattingResult();
```
Các `GetConditionalFormattingResult()` Phương pháp này rất quan trọng trong bước này. Nó trả về một đối tượng chứa kết quả của bất kỳ định dạng có điều kiện nào được áp dụng cho ô. Đây là nơi chúng ta bắt đầu khai thác thông tin màu sắc mà Excel đang sử dụng.
## Bước 5: Truy cập ColorScaleResult
Khi đã có kết quả định dạng có điều kiện, chúng ta có thể tìm hiểu sâu hơn và truy cập thang màu mà Excel đã sử dụng cho ô cụ thể này.
```csharp
// Lấy đối tượng màu kết quả ColorScale
Color c = cfr1.ColorScaleResult;
```
Định dạng có điều kiện trong Excel thường dựa vào thang màu. Dòng này cho phép chúng ta trích xuất màu kết quả được áp dụng dựa trên các quy tắc định dạng có điều kiện.
## Bước 6: Xuất thông tin màu
Cuối cùng, chúng ta muốn xem màu Excel được áp dụng. Hãy in chi tiết màu theo định dạng dễ hiểu, bao gồm cả giá trị ARGB và tên của màu.
```csharp
// Đọc màu sắc
Console.WriteLine(c.ToArgb().ToString());
Console.WriteLine(c.Name);
```
Các `ToArgb()` phương pháp cung cấp cho chúng ta màu sắc theo định dạng ARGB (Alpha, Đỏ, Xanh lục, Xanh lam), trong khi `Name` thuộc tính cung cấp tên màu theo định dạng dễ đọc hơn với con người. Bạn có thể sử dụng các chi tiết màu này để khớp với chúng trong các ứng dụng khác hoặc sửa đổi tệp Excel của bạn theo chương trình.

## Phần kết luận
Và bạn đã có nó! Bằng cách làm theo các bước này, bạn vừa học được cách tính toán theo chương trình màu được MS Excel chọn bằng Aspose.Cells cho .NET. Cách tiếp cận này có thể cực kỳ hữu ích để tự động hóa các tác vụ dựa trên Excel, đặc biệt là khi xử lý định dạng có điều kiện phức tạp. Bây giờ, lần tới khi bạn gặp một màu bí ẩn trong Excel, bạn sẽ biết chính xác cách tiết lộ bí mật của nó.
## Câu hỏi thường gặp
### Tôi có thể áp dụng định dạng có điều kiện theo chương trình bằng Aspose.Cells không?
Có, Aspose.Cells cho phép bạn áp dụng, sửa đổi và thậm chí xóa định dạng có điều kiện trong các tệp Excel theo cách lập trình.
### Aspose.Cells có hỗ trợ tất cả các phiên bản Excel không?
Chắc chắn rồi! Aspose.Cells hỗ trợ Excel 97-2003 (XLS), Excel 2007-2019/365 (XLSX) và nhiều định dạng khác, bao gồm PDF, HTML và CSV.
### Aspose.Cells có khả dụng cho các nền tảng khác ngoài .NET không?
Có, Aspose.Cells có sẵn trên nhiều nền tảng khác nhau, bao gồm Java, C++ và Android thông qua Java.
### Làm thế nào tôi có thể nhận được bản dùng thử miễn phí Aspose.Cells?
Bạn có thể tải xuống bản dùng thử miễn phí của Aspose.Cells cho .NET từ [đây](https://releases.aspose.com/).
### Làm thế nào để xử lý các tệp Excel lớn bằng Aspose.Cells?
Aspose.Cells được tối ưu hóa cho hiệu suất, ngay cả khi xử lý các tệp lớn. Bạn có thể sử dụng API phát trực tuyến để xử lý dữ liệu lớn một cách hiệu quả.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}