---
"description": "Tìm hiểu cách lấy dữ liệu từ các ô Excel bằng Aspose.Cells cho .NET trong hướng dẫn từng bước này, hoàn hảo cho cả người mới bắt đầu và nhà phát triển có kinh nghiệm."
"linktitle": "Lấy dữ liệu từ các ô trong Excel"
"second_title": "API xử lý Excel Aspose.Cells .NET"
"title": "Lấy dữ liệu từ các ô trong Excel"
"url": "/vi/net/excel-data-export-retrieval/retrieve-data-from-cells-in-excel/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Lấy dữ liệu từ các ô trong Excel

## Giới thiệu

Khi nói đến việc quản lý dữ liệu trong Excel, khả năng đọc và lấy thông tin từ các ô là rất quan trọng. Aspose.Cells for .NET là một thư viện mạnh mẽ cho phép các nhà phát triển thao tác các tệp Excel một cách liền mạch. Trong hướng dẫn này, chúng ta sẽ tìm hiểu cách lấy dữ liệu từ các ô trong sổ làm việc Excel bằng Aspose.Cells. Cho dù bạn là một nhà phát triển dày dạn kinh nghiệm hay chỉ mới bắt đầu, hướng dẫn này sẽ hướng dẫn bạn từng bước trong quy trình.

## Điều kiện tiên quyết

Trước khi đi sâu vào mã, bạn cần phải có một số điều kiện tiên quyết sau:

1. Visual Studio: Đảm bảo bạn đã cài đặt Visual Studio trên máy của mình. Đây là IDE mà chúng ta sẽ sử dụng để viết và thực thi mã của mình.
2. Aspose.Cells cho .NET: Bạn cần có thư viện Aspose.Cells. Bạn có thể tải xuống từ [Trang web Aspose](https://releases.aspose.com/cells/net/).
3. Kiến thức cơ bản về C#: Sự quen thuộc với lập trình C# sẽ giúp bạn hiểu các ví dụ tốt hơn.
4. Tệp Excel: Chuẩn bị sẵn một tệp Excel (ví dụ: `book1.xls`) mà bạn sẽ sử dụng cho hướng dẫn này.

Khi đã sắp xếp xong các điều kiện tiên quyết này, chúng ta có thể bắt đầu khám phá cách lấy dữ liệu từ các ô Excel.

## Nhập gói

Để bắt đầu, bạn cần nhập các không gian tên cần thiết vào dự án C# của mình. Điều này sẽ cho phép bạn sử dụng các lớp và phương thức do Aspose.Cells cung cấp.

```csharp
using System.IO;
using Aspose.Cells;
using System;
```

Với các không gian tên đã nhập, bạn đã sẵn sàng để bắt đầu viết mã. Hãy chia nhỏ quy trình thành các bước dễ quản lý.

## Bước 1: Thiết lập thư mục tài liệu của bạn

Bước đầu tiên là xác định đường dẫn đến thư mục tài liệu nơi tệp Excel của bạn nằm. Điều này rất quan trọng vì nó cho ứng dụng biết nơi tìm tệp bạn muốn làm việc.


```csharp
// Đường dẫn đến thư mục tài liệu.
string dataDir = "Your Document Directory";
```

Thay thế `"Your Document Directory"` với con đường thực tế nơi bạn `book1.xls` tệp được lưu trữ. Đường dẫn này là nơi Aspose.Cells sẽ tìm kiếm tệp khi bạn cố gắng mở tệp đó.

## Bước 2: Mở Workbook hiện có

Bây giờ bạn đã thiết lập xong thư mục tài liệu, bước tiếp theo là mở bảng tính (tệp Excel) mà bạn muốn làm việc.


```csharp
// Mở một bảng tính hiện có
Workbook workbook = new Workbook(dataDir + "book1.xls");
```

Ở đây, chúng tôi tạo ra một `Workbook` đối tượng bằng cách truyền đường dẫn đầy đủ của tệp Excel. Bước này khởi tạo sổ làm việc và chuẩn bị cho việc truy xuất dữ liệu.

## Bước 3: Truy cập vào trang tính đầu tiên

Sau khi mở sổ làm việc, bạn sẽ muốn truy cập vào trang tính cụ thể mà bạn muốn lấy dữ liệu. Trong trường hợp này, chúng ta sẽ truy cập trang tính đầu tiên.


```csharp
// Truy cập vào bảng tính đầu tiên
Worksheet worksheet = workbook.Worksheets[0];
```

Các `Worksheets` bộ sưu tập cho phép bạn truy cập vào các trang tính khác nhau trong sổ làm việc. Chỉ mục `[0]` tham chiếu đến trang tính đầu tiên. Nếu bạn muốn truy cập các trang tính tiếp theo, bạn có thể thay đổi chỉ mục cho phù hợp.

## Bước 4: Lặp qua các ô

Bây giờ bạn đã có bảng tính, đã đến lúc lặp qua từng ô để lấy dữ liệu. Đây chính là nơi phép thuật xảy ra!


```csharp
foreach (Cell cell1 in worksheet.Cells)
{
    // Biến để lưu trữ giá trị của các kiểu dữ liệu khác nhau
    string stringValue;
    double doubleValue;
    bool boolValue;
    DateTime dateTimeValue;

    // Truyền loại dữ liệu chứa trong ô để đánh giá
    switch (cell1.Type)
    {
        // Đánh giá kiểu dữ liệu của dữ liệu ô cho giá trị chuỗi
        case CellValueType.IsString:
            stringValue = cell1.StringValue;
            Console.WriteLine("String Value: " + stringValue);
            break;

        // Đánh giá kiểu dữ liệu của dữ liệu ô cho giá trị kép
        case CellValueType.IsNumeric:
            doubleValue = cell1.DoubleValue;
            Console.WriteLine("Double Value: " + doubleValue);
            break;

        // Đánh giá kiểu dữ liệu của dữ liệu ô cho giá trị boolean
        case CellValueType.IsBool:
            boolValue = cell1.BoolValue;
            Console.WriteLine("Bool Value: " + boolValue);
            break;

        // Đánh giá kiểu dữ liệu của dữ liệu ô cho giá trị ngày/giờ
        case CellValueType.IsDateTime:
            dateTimeValue = cell1.DateTimeValue;
            Console.WriteLine("DateTime Value: " + dateTimeValue);
            break;

        // Đánh giá kiểu dữ liệu chưa biết của dữ liệu ô
        case CellValueType.IsUnknown:
            stringValue = cell1.StringValue;
            Console.WriteLine("Unknown Value: " + stringValue);
            break;

        // Kết thúc việc kiểm tra kiểu dữ liệu ô là null
        case CellValueType.IsNull:
            break;
    }
}
```

Trong bước này, chúng ta lặp qua từng ô trong bảng tính. Đối với mỗi ô, chúng ta kiểm tra kiểu dữ liệu của nó bằng cách sử dụng `switch` statement. Tùy thuộc vào loại, chúng tôi sẽ lấy giá trị và in nó ra bảng điều khiển. Sau đây là phân tích các trường hợp:

- IsString: Nếu ô chứa một chuỗi, chúng ta sẽ lấy nó bằng cách sử dụng `StringValue`.
- IsNumeric: Đối với các giá trị số, chúng tôi sử dụng `DoubleValue`.
- IsBool: Nếu ô chứa giá trị boolean, chúng ta truy cập nó bằng cách sử dụng `BoolValue`.
- IsDateTime: Đối với các giá trị ngày và giờ, chúng tôi sử dụng `DateTimeValue`.
- IsUnknown: Nếu kiểu dữ liệu không xác định, chúng ta vẫn lấy được biểu diễn chuỗi.
- IsNull: Nếu ô trống, chúng ta chỉ cần bỏ qua ô đó.

## Phần kết luận

Truy xuất dữ liệu từ các ô Excel bằng Aspose.Cells cho .NET là một quá trình đơn giản. Bằng cách làm theo các bước này, bạn có thể trích xuất hiệu quả nhiều loại dữ liệu khác nhau từ các tệp Excel của mình. Cho dù bạn đang xây dựng một công cụ báo cáo, tự động nhập dữ liệu hay chỉ cần phân tích dữ liệu, Aspose.Cells cung cấp tính linh hoạt và sức mạnh bạn cần để hoàn thành công việc.

## Câu hỏi thường gặp

### Aspose.Cells là gì?  
Aspose.Cells là thư viện .NET cho phép các nhà phát triển tạo, thao tác và chuyển đổi các tệp Excel mà không cần cài đặt Microsoft Excel.

### Tôi có thể sử dụng Aspose.Cells miễn phí không?  
Có, Aspose.Cells cung cấp bản dùng thử miễn phí mà bạn có thể sử dụng để kiểm tra các tính năng của nó. Bạn có thể tải xuống [đây](https://releases.aspose.com/).

### Tôi có thể lấy những loại dữ liệu nào từ ô Excel?  
Bạn có thể lấy nhiều kiểu dữ liệu khác nhau, bao gồm chuỗi, số, boolean và giá trị ngày/giờ.

### Làm thế nào để tôi nhận được hỗ trợ cho Aspose.Cells?  
Bạn có thể nhận được hỗ trợ bằng cách truy cập [Diễn đàn Aspose](https://forum.aspose.com/c/cells/9) nơi bạn có thể đặt câu hỏi và nhận trợ giúp từ cộng đồng.

### Có giấy phép tạm thời không?  
Có, Aspose cung cấp giấy phép tạm thời cho mục đích đánh giá. Bạn có thể tìm thêm thông tin [đây](https://purchase.aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}