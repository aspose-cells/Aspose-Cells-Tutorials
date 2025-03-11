---
title: Tạo Tổng phụ trong Excel
linktitle: Tạo Tổng phụ trong Excel
second_title: API xử lý Excel Aspose.Cells .NET
description: Tìm hiểu cách tạo tổng phụ trong Excel bằng Aspose.Cells cho .NET với hướng dẫn từng bước dễ dàng này.
weight: 10
url: /vi/net/excel-subtotal-calculation/create-subtotals-in-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo Tổng phụ trong Excel

## Giới thiệu
Bạn đã sẵn sàng nâng cao kỹ năng Excel và làm cho bảng tính của mình năng động hơn chưa? Việc tạo tổng phụ trong Excel có thể giúp bạn phân loại và tóm tắt dữ liệu hiệu quả, cho phép diễn giải và báo cáo dữ liệu tốt hơn. Nếu bạn là người thường xuyên phải vật lộn với hàng đống số liệu, thì việc tạo tóm tắt có cấu trúc là điều cần thiết. Hôm nay, chúng ta sẽ tìm hiểu cách tạo tổng phụ dễ dàng bằng Aspose.Cells for .NET, một thư viện mạnh mẽ được thiết kế để xử lý mọi thao tác tệp Excel của bạn.
## Điều kiện tiên quyết
Trước khi đi sâu vào cách tạo tổng phụ trong Excel, bạn cần đáp ứng một số điều kiện tiên quyết sau:
1.  Đã cài đặt Aspose.Cells cho .NET: Đảm bảo bạn đã thiết lập thư viện Aspose.Cells trong môi trường phát triển của mình. Nếu bạn chưa thực hiện việc này, bạn có thể dễ dàng[tải xuống ở đây](https://releases.aspose.com/cells/net/).
2. Môi trường .NET: Bạn nên có môi trường .NET đang hoạt động để chúng ta có thể làm việc với thư viện. Cho dù là Visual Studio hay bất kỳ IDE nào khác, hãy đảm bảo rằng bạn thoải mái khi viết mã bằng C#.
3. Kiến thức cơ bản về C#: Sự quen thuộc với C# sẽ có lợi. Các ví dụ chúng tôi sẽ cung cấp bằng cú pháp C#, vì vậy, việc quen thuộc với nó sẽ giúp bạn hiểu được quy trình.
4.  Bảng tính Excel: Một tệp Excel mẫu để thực hành. Chúng tôi sẽ sử dụng một tệp có tên là`book1.xls` trong hướng dẫn của chúng tôi.
5.  Truy cập vào Tài liệu và Hỗ trợ Trực tuyến: Làm quen với[Tài liệu Aspose.Cells](https://reference.aspose.com/cells/net/) có thể cực kỳ hữu ích khi bạn nâng cao kỹ năng sử dụng thư viện.
Bây giờ chúng ta đã có nền tảng vững chắc, hãy cùng chuyển sang phần kỹ thuật nhé!
## Nhập gói
Trước khi bắt đầu với mã thực tế, chúng ta cần đảm bảo rằng chúng ta có tất cả các gói cần thiết. Dưới đây là cách bạn có thể nhập không gian tên cần thiết vào dự án của mình:
```csharp
using System.IO;
using Aspose.Cells;
```
Lệnh này nhập mọi thứ chúng ta cần từ thư viện Aspose để thao tác với các tệp Excel. Bây giờ, chúng ta hãy phân tích từng bước mã để tạo tổng phụ trong bảng tính Excel.
## Bước 1: Thiết lập đường dẫn tệp
Để bắt đầu, chúng ta cần xác định vị trí tệp Excel của mình. Đây là nơi chúng ta cho chương trình biết về thư mục tài liệu của mình.
```csharp
string dataDir = "Your Document Directory";
```
 Thay thế`"Your Document Directory"` với con đường thực tế nơi bạn`book1.xls` được lưu trữ. Điều này cho chương trình biết nơi tìm tệp Excel mà chúng ta sẽ thao tác.
## Bước 2: Tạo một Workbook mới
Tiếp theo, chúng ta sẽ tạo một phiên bản mới của đối tượng Workbook. Điều này sẽ cho phép chúng ta mở và chỉnh sửa tệp Excel của mình.
```csharp
Workbook workbook = new Workbook(dataDir + "book1.xls");
```
 Ở đây, chúng ta đang tạo ra một đối tượng`Workbook` và tải nó với những gì chúng tôi đã chỉ định`book1.xls` tệp. Đối tượng sổ làm việc này hiện chứa tất cả thông tin từ tệp Excel và cho phép chúng ta sửa đổi nó.
## Bước 3: Truy cập Bộ sưu tập tế bào
Để thao tác trên nội dung của bảng tính Excel, chúng ta cần truy cập vào bộ sưu tập “Cells”.
```csharp
Cells cells = workbook.Worksheets[0].Cells;
```
 Thao tác này sẽ lấy các ô từ trang tính đầu tiên (chỉ mục 0) của sổ làm việc của chúng tôi.`cells` đối tượng sẽ cho phép chúng ta tương tác với từng ô riêng lẻ trong bảng tính.
## Bước 4: Xác định diện tích ô cho tổng phụ
Bây giờ là lúc xác định phạm vi ô mà chúng ta muốn áp dụng tổng phụ. 
```csharp
CellArea ca = new CellArea();
ca.StartRow = 2; // B3
ca.StartColumn = 1; 
ca.EndRow = 18; // C19
ca.EndColumn = 2;
```
 Ở đây, chúng tôi định nghĩa một`CellArea` chỉ định phạm vi mà chúng ta quan tâm. Trong trường hợp này, chúng ta đã chọn vùng từ B3 (Hàng 2, Cột 1) đến C19 (Hàng 18, Cột 2). Đây là nơi chúng ta sẽ tính tổng phụ của mình.
## Bước 5: Áp dụng Tổng phụ
Đây là cốt lõi trong hoạt động của chúng tôi – áp dụng tổng phụ vào diện tích ô đã xác định.
```csharp
cells.Subtotal(ca, 0, ConsolidationFunction.Sum, new int[] { 1 });
```
 Trong dòng này, chúng ta gọi là`Subtotal` phương pháp. Các tham số được xác định là:
- `ca`: Phạm vi ô mà chúng ta đã xác định trước đó.
- `0`: Chỉ mục này đề cập đến cột chứa các giá trị cần tính tổng phụ. 
- `ConsolidationFunction.Sum`Điều này chỉ rõ rằng chúng ta muốn tính tổng các giá trị.
- `new int[] { 1 }`:Điều này cho biết chúng ta đang tính tổng các giá trị từ cột thứ hai (Cột C).
## Bước 6: Lưu tệp Excel đã sửa đổi
Cuối cùng, chúng ta cần lưu những thay đổi vào một tệp Excel mới. 
```csharp
workbook.Save(dataDir + "output.out.xls");
```
 Các`Save` phương pháp ghi các thay đổi vào một tập tin mới có tên`output.out.xls`. Bạn có thể chỉ định bất kỳ tên nào cho tệp đầu ra theo yêu cầu của bạn.
## Phần kết luận
Với các bước đơn giản này, bạn đã tạo thành công các tổng phụ trong bảng tính Excel của mình bằng Aspose.Cells cho .NET! Từ việc khởi tạo một bảng tính đến áp dụng các tổng phụ và lưu kết quả, chúng tôi đã đề cập đến tất cả các cơ sở. Thư viện này không chỉ đơn giản hóa các thao tác Excel của bạn mà còn trao quyền cho bạn xử lý dữ liệu hiệu quả hơn.
Bây giờ, hãy thử xem! Bạn sẽ ngạc nhiên khi thấy việc quản lý dữ liệu trong bảng tính trở nên dễ dàng hơn nhiều khi bạn biết cách sử dụng đúng công cụ. 
## Câu hỏi thường gặp
### Aspose.Cells dành cho .NET là gì?
Aspose.Cells for .NET là một thư viện mạnh mẽ cho phép các nhà phát triển thao tác các tệp Excel trong các ứng dụng .NET theo cách lập trình.
### Tôi có cần cài đặt thứ gì đặc biệt để sử dụng Aspose.Cells không?
 Có, bạn cần tải xuống và thêm thư viện Aspose.Cells vào dự án .NET của mình.[Tải xuống tại đây](https://releases.aspose.com/cells/net/).
### Có thể tạo các loại tính năng Excel khác bằng Aspose.Cells không?
Chắc chắn rồi! Aspose.Cells cho phép bạn thực hiện nhiều thao tác Excel khác nhau như tạo biểu đồ, quản lý bảng tính và sửa đổi định dạng ô cùng nhiều thao tác khác.
### Tôi có thể sử dụng Aspose.Cells miễn phí không?
 Bạn có thể[hãy thử dùng thử miễn phí](https://releases.aspose.com/) của Aspose.Cells để khám phá các tính năng của nó trước khi quyết định mua.
### Có những tùy chọn hỗ trợ nào?
 Đối với bất kỳ vấn đề nào, bạn có thể truy cập[Diễn đàn hỗ trợ Aspose](https://forum.aspose.com/c/cells/9) để nhận trợ giúp và chia sẻ hiểu biết với cộng đồng người dùng và nhà phát triển.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
