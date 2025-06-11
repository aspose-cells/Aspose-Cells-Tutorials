---
"description": "Tìm hiểu cách quản lý các kết nối bên ngoài trong các tệp XLSB bằng Aspose.Cells cho .NET trong hướng dẫn toàn diện này."
"linktitle": "Đọc và ghi kết nối bên ngoài của tệp XLSB"
"second_title": "Tài liệu tham khảo API Aspose.Cells cho .NET"
"title": "Đọc và ghi kết nối bên ngoài của tệp XLSB"
"url": "/vi/net/excel-workbook/read-and-write-external-connection-of-xlsb-file/"
"weight": 130
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Đọc và ghi kết nối bên ngoài của tệp XLSB

## Giới thiệu

Xin chào, những người đam mê Excel! Bạn đã sẵn sàng để đắm mình vào thế giới hấp dẫn của các tệp XLSB và kết nối bên ngoài chưa? Nếu bạn đã từng làm việc với Excel, bạn sẽ biết nó mạnh mẽ và đa năng như thế nào, nhưng đôi khi nó cũng có những điểm kỳ quặc—đặc biệt là khi xử lý các kết nối với cơ sở dữ liệu bên ngoài. Đó là lúc Aspose.Cells for .NET xuất hiện để giải cứu! Thư viện tiện lợi này cho phép bạn thao tác các tệp Excel theo cách đơn giản. Trong bài viết này, chúng tôi sẽ hướng dẫn bạn từng bước về cách đọc và ghi các kết nối bên ngoài trong tệp XLSB.

## Điều kiện tiên quyết

Trước khi bắt đầu, đây là một số thứ bạn cần:

1. Kiến thức cơ bản về C#: Biết cách sử dụng ngôn ngữ lập trình C# sẽ giúp ích rất nhiều. Nếu bạn thoải mái khi viết mã C#, bạn đã sẵn sàng!
2. Aspose.Cells cho .NET: Bạn sẽ cần cài đặt thư viện này trong môi trường phát triển của mình. Nếu bạn chưa làm điều đó, bạn có thể dễ dàng tải xuống [đây](https://releases.aspose.com/cells/net/). 
3. IDE: Bạn sẽ cần một trình soạn thảo mã hoặc Môi trường phát triển tích hợp (IDE) như Visual Studio. 
4. Tệp XLSB mẫu: Chúng ta sẽ làm việc với tệp XLSB mẫu có chứa các kết nối bên ngoài. Bạn có thể tự tạo hoặc tải xuống các mẫu trực tuyến. 

Khi bạn đã có đủ tất cả các điều kiện tiên quyết này, chúng ta đã sẵn sàng bắt tay vào viết mã!

## Nhập gói

Để bắt đầu, hãy nhập các gói cần thiết vào dự án của chúng ta. Đảm bảo bạn đã thêm tham chiếu đến Aspose.Cells vào dự án của mình. Sau đây là cách bạn có thể thực hiện điều đó trong C#:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

Các lệnh nhập này cung cấp cho bạn quyền truy cập vào chức năng bạn cần để thao tác với các tệp Excel và kết nối của chúng.

## Bước 1: Thiết lập thư mục

Trước khi làm việc với tệp XLSB, bạn cần thiết lập thư mục nguồn và thư mục đầu ra. Bước này rất cần thiết để giữ cho các tệp của bạn được sắp xếp.

```csharp
// Thư mục nguồn
string sourceDir = "Your Document Directory";
// Thư mục đầu ra
string outputDir = "Your Output Directory";
```

Trong đoạn mã này, `"Your Document Directory"` Và `"Your Document Directory"` được cho là sẽ lấy các đường dẫn tương ứng cho nơi các tệp đầu vào và đầu ra của bạn sẽ nằm. Bạn có thể thay thế các phương pháp này bằng các đường dẫn được mã hóa cứng nếu bạn thích.

## Bước 2: Tải tệp XLSB

Bây giờ là lúc tải tệp Excel của bạn vào đối tượng Workbook. Điều này giúp bạn có khả năng thao tác dữ liệu bên trong.

```csharp
// Tải tệp Excel Xlsb nguồn
Workbook wb = new Workbook(sourceDir + "sampleExternalConnection_XLSB.xlsb");
```

Chỉ cần đảm bảo rằng tệp XLSB của bạn nằm trong thư mục đã chỉ định `sourceDir`. Nếu đường dẫn đúng, bảng tính của bạn sẽ sẵn sàng để thao tác!

## Bước 3: Truy cập kết nối bên ngoài

Khi sổ làm việc được tải, bạn có thể truy cập các kết nối bên ngoài của nó. Trong trường hợp của chúng tôi, chúng tôi sẽ truy xuất kết nối cơ sở dữ liệu đầu tiên.

```csharp
// Đọc kết nối bên ngoài đầu tiên thực chất là một DB-Connection
Aspose.Cells.ExternalConnections.DBConnection dbCon = wb.DataConnections[0] as Aspose.Cells.ExternalConnections.DBConnection;
```

Đây, `DataConnections[0]` đề cập đến kết nối đầu tiên trong sổ làm việc. Chúng tôi đang đúc nó như một `DBConnection` nhập để thao tác thêm.

## Bước 4: Trích xuất thông tin kết nối

Bây giờ bạn đã có quyền truy cập vào kết nối cơ sở dữ liệu, hãy trích xuất và in thông tin chi tiết của nó vào bảng điều khiển. Điều này sẽ giúp chúng ta thấy chính xác những gì chúng ta đang làm việc.

```csharp
// In Tên, Lệnh và Thông tin Kết nối của DB-Connection
Console.WriteLine("Connection Name: " + dbCon.Name);
Console.WriteLine("Command: " + dbCon.Command);
Console.WriteLine("Connection Info: " + dbCon.ConnectionInfo);
```

Bước này cho phép bạn xác minh trạng thái hiện tại của kết nối bên ngoài. Bạn sẽ thấy tên kết nối, lệnh được sử dụng và thông tin kết nối được in ra bảng điều khiển.

## Bước 5: Sửa đổi kết nối

Đôi khi, chỉ cần đổi tên là mọi thứ trở nên rõ ràng hơn hoặc phù hợp với quy ước đặt tên mới. Hãy đổi tên kết nối hiện tại thành tên phù hợp hơn.

```csharp
// Sửa đổi tên kết nối
dbCon.Name = "NewCust";
```

Dòng mã này sẽ đổi tên kết nối của bạn từ tên gốc thành "NewCust". Đây là một thay đổi đơn giản nhưng có tác động lớn!

## Bước 6: Lưu thay đổi của bạn

Sau khi thực hiện sửa đổi, bạn sẽ muốn lưu các thay đổi của mình trở lại tệp XLSB. Sau đây là cách thực hiện:

```csharp
// Lưu tệp Excel Xlsb
wb.Save(outputDir + "outputExternalConnection_XLSB.xlsb");
```

Dòng mã này sẽ lưu bảng tính đã cập nhật của bạn, giữ lại tất cả các thay đổi, bao gồm cả tên kết nối mới.

## Bước 7: Xác nhận thực hiện

Cuối cùng, hãy xác nhận mọi thứ hoạt động trơn tru. Một thông báo đơn giản ở cuối sẽ làm rõ điều đó.

```csharp
Console.WriteLine("ReadAndWriteExternalConnectionOfXLSBFile executed successfully.\r\n");
```

Thông báo này sẽ đảm bảo với bạn rằng mã của bạn đã chạy thành công và mọi thay đổi đã được lưu như mong đợi.

## Phần kết luận

Và bạn đã có nó! Bạn đã học thành công cách đọc và ghi các kết nối bên ngoài trong các tệp XLSB bằng Aspose.Cells cho .NET. Bằng cách làm theo các bước này, bạn có thể quản lý hiệu quả các kết nối dữ liệu Excel của mình, giúp công việc của bạn với Excel trở nên hợp lý hơn nhiều và ít gây bực bội hơn. Hãy nhớ rằng, cho dù bạn đang xử lý các tập dữ liệu mở rộng hay chỉ đơn giản là sắp xếp thông tin của mình, Aspose.Cells đều có các công cụ bạn cần.

## Câu hỏi thường gặp

### Tệp XLSB là gì?  
Tệp XLSB là định dạng tệp Excel nhị phân lưu trữ dữ liệu bảng tính ở định dạng nhị phân, giúp tệp nhỏ gọn hơn và mở nhanh hơn.

### Làm thế nào để cài đặt Aspose.Cells cho .NET?  
Bạn có thể dễ dàng tải xuống từ trang web Aspose [đây](https://releases.aspose.com/cells/net/).

### Tôi có thể sử dụng Aspose.Cells miễn phí không?  
Có! Bạn có thể bắt đầu với bản dùng thử miễn phí, có sẵn [đây](https://releases.aspose.com/).

### Aspose.Cells có hỗ trợ các định dạng tệp khác không?  
Chắc chắn rồi! Aspose.Cells hỗ trợ nhiều định dạng tệp khác nhau, bao gồm XLSX, CSV, v.v.

### Tôi có thể tìm kiếm sự trợ giúp ở đâu nếu gặp vấn đề?  
Bạn có thể nhận được sự hỗ trợ từ diễn đàn Aspose [đây](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}