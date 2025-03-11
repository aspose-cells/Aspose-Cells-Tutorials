---
title: Mở tệp CSV bằng Preferred Parser
linktitle: Mở tệp CSV bằng Preferred Parser
second_title: API xử lý Excel Aspose.Cells .NET
description: Tìm hiểu cách mở và phân tích cú pháp tệp CSV bằng trình phân tích cú pháp tùy chỉnh trong Aspose.Cells cho .NET. Xử lý văn bản và ngày tháng một cách dễ dàng. Hoàn hảo cho các nhà phát triển.
weight: 11
url: /vi/net/csv-file-handling/csv-file-opening-csv-files-with-preferred-parser/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Mở tệp CSV bằng Preferred Parser

## Giới thiệu
Khi xử lý tệp CSV, đôi khi bạn muốn xử lý các kiểu dữ liệu khác nhau bằng trình phân tích cú pháp tùy chỉnh. Hướng dẫn này sẽ hướng dẫn bạn cách mở tệp CSV bằng trình phân tích cú pháp ưa thích bằng Aspose.Cells cho .NET. Cho dù bạn muốn xử lý văn bản, ngày tháng hay các định dạng tùy chỉnh khác, hướng dẫn này sẽ hướng dẫn bạn từng bước với lời giải thích rõ ràng.
## Điều kiện tiên quyết
Trước khi tìm hiểu về mã, chúng ta hãy cùng tìm hiểu những mục thiết yếu bạn cần để bắt đầu.
1.  Aspose.Cells cho Thư viện .NET: Đảm bảo bạn đã cài đặt thư viện Aspose.Cells. Bạn có thể tải xuống[đây](https://releases.aspose.com/cells/net/) . Bạn cũng có thể sử dụng bản dùng thử miễn phí[đây](https://releases.aspose.com/).
2. Môi trường phát triển .NET: Khuyến khích sử dụng Visual Studio, nhưng bất kỳ IDE nào tương thích với .NET đều có thể sử dụng được.
3. Kiến thức cơ bản về C#: Hướng dẫn này giả định rằng bạn đã quen thuộc với C# và lập trình hướng đối tượng.
## Nhập gói
Để sử dụng Aspose.Cells, bạn sẽ cần phải nhập các không gian tên cần thiết ở đầu tệp C# của mình:
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
Bây giờ chúng ta đã thiết lập xong, hãy cùng tìm hiểu cách mở tệp CSV bằng trình phân tích cú pháp ưa thích, xử lý các định dạng dữ liệu khác nhau như văn bản và ngày tháng.
## Bước 1: Xác định trình phân tích cú pháp tùy chỉnh
 Để xử lý các kiểu dữ liệu khác nhau, chẳng hạn như văn bản hoặc định dạng ngày cụ thể, bạn cần xác định trình phân tích cú pháp tùy chỉnh. Trong Aspose.Cells, trình phân tích cú pháp tùy chỉnh triển khai`ICustomParser` giao diện.
### 1.1 Tạo một trình phân tích cú pháp văn bản
Bộ phân tích cú pháp này xử lý các giá trị văn bản thông thường. Nó không sửa đổi định dạng, do đó giá trị được trả về nguyên trạng.
```csharp
class TextParser : ICustomParser
{
    public object ParseObject(string value)
    {
        return value;
    }
    public string GetFormat()
    {
        return "";
    }
}
```
 Các`ParseObject` phương pháp này chỉ trả về giá trị đầu vào. Giống như nói rằng, "Đừng thay đổi bất cứ điều gì, chỉ cần đưa cho tôi văn bản!"
### 1.2 Tạo một trình phân tích ngày
 Đối với ngày, bạn sẽ muốn đảm bảo rằng dữ liệu CSV được phân tích chính xác thành`DateTime` đối tượng. Sau đây là cách bạn có thể tạo trình phân tích ngày:
```csharp
class DateParser : ICustomParser
{
    public object ParseObject(string value)
    {
        DateTime myDate = DateTime.ParseExact(value, "dd/MM/yyyy", 
            System.Globalization.CultureInfo.InvariantCulture);
        return myDate;
    }
    public string GetFormat()
    {
        return "dd/MM/yyyy";
    }
}
```
 Trong trình phân tích cú pháp này, chúng tôi sử dụng`ParseExact` để đảm bảo ngày được diễn giải chính xác dựa trên định dạng được xác định trước (`"dd/MM/yyyy"`). Theo cách này, bất kỳ ngày nào trong tệp CSV của bạn theo định dạng này sẽ được xử lý mà không có vấn đề gì.
## Bước 2: Cấu hình Tùy chọn Tải
 Tiếp theo, bạn cần cấu hình cách tệp CSV được tải. Điều này được thực hiện bằng cách sử dụng`TxtLoadOptions` lớp cho phép bạn chỉ định các tùy chọn phân tích cú pháp, bao gồm mã hóa và trình phân tích cú pháp tùy chỉnh.
### 2.1 Thiết lập tùy chọn tải
 Chúng ta sẽ bắt đầu bằng cách khởi tạo`TxtLoadOptions` và xác định các tham số chính như dấu phân cách và mã hóa:
```csharp
TxtLoadOptions oTxtLoadOptions = new TxtLoadOptions(LoadFormat.Csv);
oTxtLoadOptions.Separator = Convert.ToChar(",");
oTxtLoadOptions.Encoding = Encoding.UTF8;
oTxtLoadOptions.ConvertDateTimeData = true;
```
- Dấu phân cách: Xác định ký tự được sử dụng để phân tách các giá trị trong tệp CSV (trong trường hợp này là dấu phẩy).
- Mã hóa: Chúng tôi sử dụng mã hóa UTF-8 để xử lý nhiều loại ký tự.
-  ConvertDateTimeData: Đặt thành true đảm bảo rằng các giá trị ngày sẽ được tự động chuyển đổi thành`DateTime` các đối tượng khi có thể.
### 2.2 Áp dụng Bộ phân tích cú pháp tùy chỉnh
Tiếp theo, chúng ta sẽ chỉ định các trình phân tích cú pháp đã tạo trước đó để xử lý các giá trị trong CSV:
```csharp
oTxtLoadOptions.PreferredParsers = new ICustomParser[] 
{ 
    new TextParser(), 
    new DateParser() 
};
```
 Điều này cho biết Aspose.Cells sử dụng`TextParser` cho các giá trị văn bản chung và`DateParser`cho bất kỳ trường ngày nào có trong tệp CSV.
## Bước 3: Tải và đọc tệp CSV
 Bây giờ các tùy chọn tải đã được cấu hình, bạn có thể tải tệp CSV vào`Aspose.Cells.Workbook` sự vật.
### 3.1 Tải tệp CSV
 Chúng tôi tải tệp CSV bằng cách truyền đường dẫn tệp và cấu hình`TxtLoadOptions` đến`Workbook` người xây dựng:
```csharp
string sourceDir = "Your Document Directory";
Workbook oExcelWorkBook = new Aspose.Cells.Workbook(sourceDir + "samplePreferredParser.csv", oTxtLoadOptions);
```
Bước này chuyển đổi dữ liệu CSV của bạn thành một bảng tính Excel đầy đủ chức năng, trong đó mỗi giá trị được phân tích cú pháp theo các quy tắc bạn muốn.
## Bước 4: Truy cập và hiển thị dữ liệu ô
Sau khi tệp CSV được tải vào sổ làm việc, bạn có thể bắt đầu làm việc với dữ liệu. Ví dụ, bạn có thể muốn in loại và giá trị của các ô cụ thể.
### 4.1 Lấy và Hiển thị Ô A1
Hãy lấy ô đầu tiên (A1) và hiển thị giá trị và kiểu của nó:
```csharp
Cell oCell = oExcelWorkBook.Worksheets[0].Cells["A1"];
Console.WriteLine("A1: " + oCell.Type.ToString() + " - " + oCell.DisplayStringValue);
```
 Ở đây,`Type` thuộc tính hiển thị kiểu dữ liệu (chẳng hạn như`String` hoặc`DateTime` ), Và`DisplayStringValue` cung cấp cho bạn giá trị được định dạng.
### 4.2 Lấy và Hiển thị Ô B1
Tương tự như vậy, chúng ta có thể lấy và hiển thị một ô khác, chẳng hạn như B1:
```csharp
oCell = oExcelWorkBook.Worksheets[0].Cells["B1"];
Console.WriteLine("B1: " + oCell.Type.ToString() + " - " + oCell.DisplayStringValue);
```
Quá trình này có thể được lặp lại với nhiều ô tùy theo nhu cầu kiểm tra của bạn.
## Bước 5: Lưu sổ làm việc
 Sau khi làm việc với dữ liệu, bạn có thể muốn lưu sổ làm việc vào một tệp mới. Aspose.Cells giúp bạn thực hiện việc này dễ dàng bằng một`Save` phương pháp:
```csharp
string outputDir = "Your Document Directory";
oExcelWorkBook.Save(outputDir + "outputsamplePreferredParser.xlsx");
```
Thao tác này sẽ lưu bảng tính dưới dạng tệp Excel, bảo toàn mọi định dạng và phân tích dữ liệu mà bạn đã áp dụng.
## Phần kết luận
Mở tệp CSV bằng trình phân tích cú pháp ưa thích trong Aspose.Cells cho .NET là một cách linh hoạt và mạnh mẽ để xử lý các loại dữ liệu khác nhau. Bằng cách tạo trình phân tích cú pháp tùy chỉnh và cấu hình tùy chọn tải, bạn có thể đảm bảo rằng tệp CSV của mình được phân tích cú pháp chính xác theo cách bạn cần, cho dù bạn đang xử lý văn bản, ngày tháng hay các định dạng tùy chỉnh khác. Với hướng dẫn này, giờ đây bạn đã được trang bị để xử lý các tình huống phân tích cú pháp dữ liệu phức tạp hơn trong các dự án của mình.
## Câu hỏi thường gặp
### Mục đích của trình phân tích cú pháp tùy chỉnh trong Aspose.Cells dành cho .NET là gì?
Trình phân tích cú pháp tùy chỉnh cho phép bạn xác định cách phân tích cú pháp các loại dữ liệu cụ thể, chẳng hạn như văn bản hoặc ngày tháng, khi tải tệp CSV.
### Tôi có thể sử dụng ký tự phân cách khác trong tệp CSV không?
 Có, bạn có thể chỉ định bất kỳ ký tự nào làm dấu phân cách trong`TxtLoadOptions.Separator` tài sản.
### Tôi phải xử lý mã hóa trong Aspose.Cells như thế nào khi tải tệp CSV?
 Bạn có thể thiết lập`Encoding` tài sản của`TxtLoadOptions` với bất kỳ chương trình mã hóa nào như UTF-8, ASCII, v.v.
### Điều gì xảy ra nếu định dạng ngày tháng trong CSV khác?
Bạn có thể xác định định dạng ngày cụ thể bằng trình phân tích cú pháp tùy chỉnh, đảm bảo phân tích cú pháp giá trị ngày chính xác.
### Tôi có thể lưu bảng tính ở định dạng khác không?
Có, Aspose.Cells cho phép bạn lưu bảng tính ở nhiều định dạng khác nhau như XLSX, CSV, PDF, v.v.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
