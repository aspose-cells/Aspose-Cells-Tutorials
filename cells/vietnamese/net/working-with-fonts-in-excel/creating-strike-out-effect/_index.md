---
title: Tạo hiệu ứng gạch ngang trên văn bản trong Excel
linktitle: Tạo hiệu ứng gạch ngang trên văn bản trong Excel
second_title: API xử lý Excel Aspose.Cells .NET
description: Tìm hiểu cách áp dụng hiệu ứng gạch ngang vào văn bản trong Excel bằng Aspose.Cells cho .NET trong hướng dẫn từng bước chi tiết này.
weight: 15
url: /vi/net/working-with-fonts-in-excel/creating-strike-out-effect/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo hiệu ứng gạch ngang trên văn bản trong Excel

## Giới thiệu
Khi nói đến Excel, các thành phần trực quan cũng quan trọng như chính dữ liệu. Cho dù bạn đang làm nổi bật những thay đổi quan trọng hay đánh dấu các mục không còn liên quan nữa, hiệu ứng gạch bỏ trên văn bản là một cách cổ điển để quản lý biểu diễn trực quan trong bảng tính. Trong hướng dẫn này, chúng tôi sẽ hướng dẫn bạn quy trình triển khai hiệu ứng gạch bỏ trên văn bản trong Excel bằng Aspose.Cells cho .NET. Hướng dẫn này không chỉ đề cập đến các điều kiện tiên quyết cần thiết mà còn cung cấp phương pháp từng bước để đảm bảo bạn có thể sao chép hiệu ứng này một cách dễ dàng.
## Điều kiện tiên quyết
Trước khi bắt đầu hướng dẫn, hãy đảm bảo bạn đã đáp ứng các điều kiện tiên quyết sau:
1. Môi trường phát triển: Bạn nên thiết lập môi trường phát triển .NET. Có thể là Visual Studio hoặc bất kỳ IDE nào khác mà bạn thích hỗ trợ phát triển .NET.
2. Aspose.Cells cho .NET: Đảm bảo rằng bạn đã cài đặt Aspose.Cells trong dự án của mình. Bạn có thể tải xuống từ liên kết sau:[Tải xuống Aspose.Cells](https://releases.aspose.com/cells/net/).
3. Kiến thức cơ bản về C#: Hiểu biết cơ bản về lập trình C# rất hữu ích vì các ví dụ sẽ được mã hóa bằng C#.
4. .NET Framework: Đảm bảo rằng dự án của bạn đang hướng tới phiên bản .NET Framework tương thích, thường là .NET Core hoặc .NET Framework 4.5 trở lên.
## Nhập gói
Trước khi viết bất kỳ mã nào, bạn cần nhập các không gian tên cần thiết từ Aspose.Cells. Điều này rất quan trọng để truy cập các tính năng khác nhau do thư viện cung cấp. Sau đây là cách bạn có thể nhập các không gian tên cần thiết:
```csharp
using System.IO;
using Aspose.Cells;
```
Với các lần nhập này, bạn sẽ có quyền truy cập vào các lớp Workbook, Worksheet và Style sẽ được sử dụng trong toàn bộ hướng dẫn này.
Bây giờ chúng ta đã thiết lập xong bối cảnh, hãy chia nhỏ quy trình thành các bước dễ quản lý. Mỗi bước sẽ đi kèm với hướng dẫn rõ ràng để hướng dẫn bạn tạo hiệu ứng gạch ngang trên văn bản trong Excel.
## Bước 1: Xác định thư mục tài liệu
Bắt đầu bằng cách xác định đường dẫn nơi lưu trữ tài liệu Excel của bạn. Đây sẽ là vị trí lưu các tệp đầu ra của bạn.
```csharp
// Đường dẫn đến thư mục tài liệu.
string dataDir = "Your Document Directory";
```
 Thay thế`"Your Document Directory"` với đường dẫn thư mục thực tế mà bạn muốn lưu tệp Excel của mình. Điều này thiết lập thư mục cho đầu ra của bạn.
## Bước 2: Tạo thư mục
Tiếp theo, bạn cần đảm bảo rằng thư mục bạn chỉ định ở bước trước tồn tại. Nếu không tồn tại, bạn có thể tạo nó theo chương trình.
```csharp
// Tạo thư mục nếu thư mục đó chưa có.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Mã này kiểm tra xem thư mục có tồn tại không và tạo thư mục nếu không. Điều này giúp tránh lỗi khi bạn cố lưu tệp sau này.
## Bước 3: Khởi tạo một đối tượng Workbook
Bây giờ, đã đến lúc tạo một đối tượng Workbook mới. Đây là nền tảng của tệp Excel nơi bạn sẽ thêm dữ liệu và áp dụng định dạng.
```csharp
// Khởi tạo một đối tượng Workbook
Workbook workbook = new Workbook();
```
 Các`Workbook` lớp biểu diễn một tệp Excel. Bằng cách tạo một thể hiện của lớp này, về cơ bản bạn đang tạo một tài liệu Excel mới.
## Bước 4: Thêm một bảng tính mới
Mỗi sổ làm việc có thể chứa nhiều trang tính. Chúng ta hãy tiếp tục và tạo một trang tính mới trong sổ làm việc của bạn.
```csharp
// Thêm một bảng tính mới vào đối tượng Excel
int i = workbook.Worksheets.Add();
```
 Các`Add` phương pháp của`Worksheets` bộ sưu tập thêm một bảng tính mới vào sổ làm việc và trả về chỉ mục của bảng tính đó. 
## Bước 5: Lấy tham chiếu của bảng tính mới
Sau khi tạo xong bảng tính, bạn cần tham khảo nó cho các hoạt động sau này.
```csharp
// Lấy tham chiếu của bảng tính mới được thêm vào bằng cách chuyển chỉ mục trang tính của nó
Worksheet worksheet = workbook.Worksheets[i];
```
Tại đây, bạn đang lấy bảng tính mới được tạo bằng cách sử dụng chỉ mục của nó (`i`). Điều này cho phép bạn truy cập để thao tác trên bảng tính.
## Bước 6: Truy cập vào một ô
 Bạn sẽ muốn truy cập vào một ô cụ thể trong bảng tính của mình, nơi bạn sẽ áp dụng định dạng gạch bỏ. Trong ví dụ này, chúng tôi đang sử dụng ô`A1`.
```csharp
// Truy cập ô "A1" từ bảng tính
Aspose.Cells.Cell cell = worksheet.Cells["A1"];
```
 Trong Excel, các ô được tham chiếu theo số nhận dạng cột và hàng của chúng (ví dụ: "A1"). Chúng tôi đang lấy tham chiếu đến ô`A1` để thao tác thêm.
## Bước 7: Thêm giá trị vào ô
 Tiếp theo, chúng ta hãy chèn một số văn bản vào ô. Chúng ta sẽ viết "Xin chào Aspose!" trong ô`A1`.
```csharp
// Thêm một số giá trị vào ô "A1"
cell.PutValue("Hello Aspose!");
```
 Các`PutValue` phương pháp này được sử dụng để gán giá trị chuỗi cho ô. Bạn có thể sửa đổi chuỗi này thành bất kỳ giá trị nào bạn muốn hiển thị.
## Bước 8: Lấy Kiểu của Ô
Bây giờ chúng ta đã có văn bản trong ô, đã đến lúc truy cập vào kiểu của ô để áp dụng định dạng mong muốn, bao gồm cả hiệu ứng gạch ngang.
```csharp
// Lấy kiểu của tế bào
Style style = cell.GetStyle();
```
 Các`GetStyle` phương pháp này lấy kiểu hiện tại của ô, cho phép bạn sửa đổi các thuộc tính như kiểu phông chữ, kích thước và hiệu ứng.
## Bước 9: Thiết lập hiệu ứng gạch ngang
Hãy áp dụng hiệu ứng gạch ngang vào văn bản trong ô. Chúng ta sẽ sửa đổi kiểu phông chữ của ô.
```csharp
// ExStart:Đặt Strikeout
// Thiết lập hiệu ứng gạch ngang trên phông chữ
style.Font.IsStrikeout = true;
// ExEnd:ĐặtStrikeout
```
 Bằng cách thiết lập`IsStrikeout` đúng, bạn đang hướng dẫn Excel gạch bỏ trực quan văn bản trong ô được chọn - giống như cách đánh dấu trực quan một mục nào đó trong danh sách.
## Bước 10: Áp dụng Kiểu cho Ô
Sau khi sửa đổi kiểu, bạn cần áp dụng lại kiểu đó vào ô để phản ánh những thay đổi.
```csharp
// Áp dụng kiểu cho ô
cell.SetStyle(style);
```
 Các`SetStyle` phương pháp này cập nhật ô theo kiểu mới, hiện bao gồm định dạng gạch ngang.
## Bước 11: Lưu tệp Excel
 Cuối cùng, đã đến lúc lưu sổ làm việc của bạn vào thư mục đã chỉ định. Trong ví dụ này, chúng tôi đang lưu tệp có tên`book1.out.xls`.
```csharp
// Lưu tệp Excel
workbook.Save(dataDir + "book1.out.xls", SaveFormat.Excel97To2003);
```
 Các`Save`phương pháp ghi sổ làm việc vào đĩa theo định dạng Excel 97-2003. Bạn có thể chỉ định các định dạng khác nếu cần.
## Phần kết luận
Tạo hiệu ứng gạch ngang trên văn bản trong Excel bằng Aspose.Cells cho .NET là một quá trình đơn giản khi bạn chia nhỏ từng bước. Bằng cách làm theo hướng dẫn này, giờ đây bạn đã có kỹ năng để cải thiện bảng tính của mình bằng các tín hiệu trực quan, giúp dữ liệu của bạn không chỉ mang tính thông tin mà còn hấp dẫn về mặt trực quan.
## Câu hỏi thường gặp
### Aspose.Cells là gì?
Aspose.Cells là một thư viện mạnh mẽ để quản lý các tệp Excel trong các ứng dụng .NET, cho phép bạn tạo, thao tác và chuyển đổi các tài liệu Excel theo chương trình.
### Tôi có thể sử dụng Aspose.Cells miễn phí không?
 Có, bạn có thể sử dụng miễn phí trong thời gian dùng thử. Bản dùng thử miễn phí có tại[Dùng thử miễn phí Aspose.Cells](https://releases.aspose.com/).
### Làm thế nào để tôi mua Aspose.Cells?
 Bạn có thể mua giấy phép cho Aspose.Cells thông qua trang web của họ[Mua Aspose.Cells](https://purchase.aspose.com/buy).
### Có ví dụ nào về cách sử dụng Aspose.Cells không?
 Có, bạn có thể tìm thấy rất nhiều ví dụ và đoạn mã trong[Tài liệu Aspose.Cells](https://reference.aspose.com/cells/net/).
### Tôi có thể nhận hỗ trợ cho Aspose.Cells ở đâu?
 Bạn có thể nhận được sự hỗ trợ và giúp đỡ của cộng đồng từ[Diễn đàn Aspose](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
