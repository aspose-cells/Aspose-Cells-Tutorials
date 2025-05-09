---
"description": "Tìm hiểu cách tách nhóm các hàng và cột trong Excel bằng Aspose.Cells cho .NET với hướng dẫn toàn diện này. Đơn giản hóa thao tác dữ liệu Excel của bạn."
"linktitle": "Tách nhóm các hàng và cột trong Excel bằng Aspose.Cells"
"second_title": "API xử lý Excel Aspose.Cells .NET"
"title": "Tách nhóm các hàng và cột trong Excel bằng Aspose.Cells"
"url": "/vi/net/row-and-column-management/ungrouping-rows-and-columns/"
"weight": 15
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Tách nhóm các hàng và cột trong Excel bằng Aspose.Cells

## Giới thiệu
Khi nói đến việc xử lý các tệp Excel, bạn có thể thấy mình trong những tình huống cần phải tách nhóm các hàng và cột. Cho dù bạn đang dọn dẹp bảng tính hay định dạng lại dữ liệu để trình bày tốt hơn, Aspose.Cells for .NET là một công cụ tuyệt vời giúp đơn giản hóa quy trình. Trong hướng dẫn này, tôi sẽ hướng dẫn bạn các bước tách nhóm các hàng và cột trong Excel bằng Aspose.Cells. Cuối cùng, bạn sẽ hiểu rõ cách làm việc với các tệp Excel theo chương trình.
## Điều kiện tiên quyết
Trước khi đi sâu vào mã, hãy đảm bảo bạn đã thiết lập mọi thứ. Sau đây là những gì bạn cần:
1. Visual Studio: Bạn nên cài đặt phiên bản Visual Studio đang hoạt động trên máy của mình. Nếu bạn chưa có, bạn có thể tải xuống từ [Trang web của Visual Studio](https://visualstudio.microsoft.com/).
2. Aspose.Cells cho .NET: Bạn sẽ cần tải xuống thư viện Aspose.Cells. Bạn có thể lấy nó từ [Trang phát hành Aspose](https://releases.aspose.com/cells/net/)Đảm bảo bạn có các giấy phép cần thiết, có thể được mua hoặc có được thông qua [giấy phép tạm thời](https://purchase.aspose.com/temporary-license/).
3. Kiến thức cơ bản về C#: Hiểu biết cơ bản về lập trình C# sẽ giúp bạn theo dõi dễ dàng hơn.
Khi bạn đã chuẩn bị mọi thứ xong, chúng ta có thể bắt đầu phần thú vị: viết mã!
## Nhập gói
Để bắt đầu, bạn cần nhập các gói cần thiết vào dự án C# của mình. Sau đây là cách thực hiện:
1. Mở dự án của bạn trong Visual Studio.
2. Thêm tham chiếu đến thư viện Aspose.Cells. Bạn có thể thực hiện việc này bằng cách nhấp chuột phải vào References trong dự án của bạn và chọn Add Reference. Duyệt đến vị trí bạn đã lưu Aspose.Cells DLL.
3. Ở đầu tệp C# của bạn, hãy thêm lệnh using sau:
```csharp
using System.IO;
using Aspose.Cells;
```
Bây giờ mọi thứ đã được thiết lập, chúng ta hãy cùng thực hiện các bước để hủy nhóm các hàng và cột trong bảng tính Excel của bạn. 
## Bước 1: Xác định thư mục tài liệu
Đầu tiên, bạn cần chỉ định thư mục chứa tệp Excel của bạn. Bạn có thể thiết lập như sau:
```csharp
// Đường dẫn đến thư mục tài liệu.
string dataDir = "Your Document Directory";
```
Thay thế `"Your Document Directory"` với đường dẫn thực tế trên máy tính của bạn nơi tệp Excel được lưu. 
## Bước 2: Tạo luồng tệp
Tiếp theo, bạn cần tạo một luồng tệp để mở tệp Excel. Đây là cách bạn có thể thực hiện:
```csharp
// Tạo luồng tệp chứa tệp Excel cần mở
FileStream fstream = new FileStream(dataDir + "book1.xls", FileMode.Open);
```
Ở đây, bạn đang mở tệp có tên `book1.xls`. Hãy đảm bảo rằng tệp này tồn tại trong thư mục bạn chỉ định, nếu không bạn sẽ gặp lỗi không tìm thấy tệp.
## Bước 3: Khởi tạo một đối tượng Workbook
Bây giờ, hãy tải tệp Excel vào đối tượng Workbook. Điều này cho phép bạn thao tác workbook theo chương trình:
```csharp
// Khởi tạo một đối tượng Workbook
// Mở tệp Excel thông qua luồng tệp
Workbook workbook = new Workbook(fstream);
```
Với dòng mã này, bạn đã tải thành công tệp Excel vào bộ nhớ và sẵn sàng làm việc với tệp đó.
## Bước 4: Truy cập vào Bảng tính
Sau khi bạn có sổ làm việc, bước tiếp theo là truy cập vào trang tính cụ thể mà bạn muốn tách nhóm các hàng và cột. Sau đây là cách thực hiện:
```csharp
// Truy cập vào trang tính đầu tiên trong tệp Excel
Worksheet worksheet = workbook.Worksheets[0];
```
Trong trường hợp này, chúng ta đang truy cập vào trang tính đầu tiên. Nếu dữ liệu của bạn nằm trên một trang tính khác, bạn có thể thay đổi chỉ mục cho phù hợp.
## Bước 5: Tách nhóm các hàng
Bây giờ đến phần thú vị! Chúng ta hãy tách nhóm sáu hàng đầu tiên (từ hàng 0 đến hàng 5). Sử dụng mã sau:
```csharp
// Tách sáu hàng đầu tiên (từ 0 đến 5)
worksheet.Cells.UngroupRows(0, 5);
```
Phương pháp này xóa bất kỳ nhóm nào đã được áp dụng cho các hàng đã chỉ định. Thật dễ dàng!
## Bước 6: Tách nhóm các cột
Giống như hàng, bạn cũng có thể tách nhóm các cột. Sau đây là cách tách nhóm ba cột đầu tiên (từ cột 0 đến cột 2):
```csharp
// Tách ba cột đầu tiên (từ 0 đến 2)
worksheet.Cells.UngroupColumns(0, 2);
```
## Bước 7: Lưu tệp Excel đã sửa đổi
Sau khi bạn đã tách nhóm các hàng và cột, bước tiếp theo là lưu các thay đổi trở lại tệp Excel. Bạn có thể thực hiện việc này bằng cách sử dụng `Save` phương pháp:
```csharp
// Lưu tệp Excel đã sửa đổi
workbook.Save(dataDir + "output.xls");
```
Trong ví dụ này, chúng tôi đang lưu tệp đã sửa đổi dưới dạng `output.xls`. Bạn có thể thay đổi tên tệp thành bất kỳ tên nào bạn thích.
## Bước 8: Đóng luồng tập tin
Cuối cùng, để giải phóng tài nguyên, bạn nên đóng luồng tệp:
```csharp
// Đóng luồng tệp để giải phóng tất cả tài nguyên
fstream.Close();
```
Đây là một biện pháp tốt để đảm bảo ứng dụng của bạn không giữ các tệp xử lý lâu hơn mức cần thiết.
## Phần kết luận
Và bạn đã có nó! Bạn đã học thành công cách tách nhóm các hàng và cột trong tệp Excel bằng Aspose.Cells cho .NET. Chỉ với một vài dòng mã, bạn có thể thực hiện những thay đổi đáng kể cho các tệp Excel của mình theo chương trình. Cho dù bạn đang tự động hóa báo cáo hay chuẩn bị dữ liệu để phân tích, việc thành thạo các kỹ thuật này có thể giúp bạn tiết kiệm rất nhiều thời gian.
## Câu hỏi thường gặp
### Aspose.Cells là gì?
Aspose.Cells là một thư viện mạnh mẽ để làm việc với các tệp Excel trong các ứng dụng .NET, cho phép thao tác, chuyển đổi và tạo bảng tính dễ dàng.
### Tôi có thể hủy nhóm các hàng và cột trong Excel bằng các thư viện khác không?
Có, còn có các thư viện khác có sẵn để thao tác với Excel trong .NET, nhưng Aspose.Cells cung cấp nhiều tính năng mở rộng và dễ sử dụng.
### Có cách nào để hoàn tác thay đổi sau khi lưu không?
Sau khi lưu tệp Excel, trạng thái trước đó không thể khôi phục được trừ khi bạn có bản sao lưu của tệp gốc.
### Làm thế nào để tôi nhận được hỗ trợ cho Aspose.Cells?
Bạn có thể tìm thấy sự hỗ trợ bằng cách truy cập [Diễn đàn hỗ trợ Aspose](https://forum.aspose.com/c/cells/9), nơi bạn có thể đặt câu hỏi và tìm giải pháp.
### Tôi có thể sử dụng Aspose.Cells mà không cần giấy phép không?
Có, bạn có thể sử dụng Aspose.Cells miễn phí với một số hạn chế nhất định và bạn có thể bắt đầu với [giấy phép tạm thời](https://purchase.aspose.com/temporary-license/) để có đầy đủ chức năng.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}