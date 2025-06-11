---
"description": "Tìm hiểu cách bảo vệ các hàng trong bảng tính Excel bằng Aspose.Cells cho .NET. Bảo vệ dữ liệu của bạn bằng tính năng bảo vệ cấp hàng và ngăn ngừa các thay đổi vô tình."
"linktitle": "Bảo vệ các hàng trong bảng tính bằng Aspose.Cells"
"second_title": "API xử lý Excel Aspose.Cells .NET"
"title": "Bảo vệ các hàng trong bảng tính bằng Aspose.Cells"
"url": "/vi/net/worksheet-security/protect-rows/"
"weight": 18
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Bảo vệ các hàng trong bảng tính bằng Aspose.Cells

## Giới thiệu
Làm việc với các tệp Excel theo chương trình thường là một nhiệm vụ không chỉ đòi hỏi thao tác dữ liệu mà còn đòi hỏi bảo vệ dữ liệu. Cho dù bạn cần bảo vệ dữ liệu nhạy cảm hay ngăn chặn việc chỉnh sửa vô tình, việc bảo vệ các hàng trong bảng tính có thể là một bước quan trọng. Trong hướng dẫn này, chúng ta sẽ đi sâu vào cách bảo vệ các hàng cụ thể trong bảng tính Excel bằng Aspose.Cells cho .NET. Chúng ta sẽ hướng dẫn tất cả các bước cần thiết, từ việc chuẩn bị môi trường của bạn đến việc triển khai các tính năng bảo vệ theo cách đơn giản, dễ làm theo.
## Điều kiện tiên quyết
Trước khi bạn có thể bắt đầu bảo vệ các hàng trong bảng tính, bạn cần phải chuẩn bị một số thứ sau:
1. Aspose.Cells cho .NET: Đảm bảo bạn đã cài đặt Aspose.Cells cho .NET trên máy phát triển của mình. Nếu bạn chưa thực hiện việc này, bạn có thể dễ dàng tải xuống từ [Trang tải xuống Aspose Cells](https://releases.aspose.com/cells/net/).
2. Visual Studio hoặc bất kỳ IDE .NET nào: Để triển khai giải pháp, bạn cần thiết lập môi trường phát triển. Visual Studio là một lựa chọn tuyệt vời, nhưng bất kỳ IDE tương thích .NET nào cũng có thể hoạt động.
3. Kiến thức cơ bản về C#: Hiểu được những kiến thức cơ bản về lập trình C# sẽ giúp bạn theo dõi hướng dẫn và sửa đổi mã ví dụ cho phù hợp với nhu cầu của mình.
4. Tài liệu API Aspose.Cells: Làm quen với [Aspose.Cells cho tài liệu .NET](https://reference.aspose.com/cells/net/) để có cái nhìn tổng quan về cấu trúc lớp và các phương thức được sử dụng trong thư viện.
Nếu bạn đã chuẩn bị đầy đủ các điều kiện tiên quyết, chúng ta có thể bắt tay ngay vào triển khai.
## Nhập gói
Để bắt đầu, bạn cần nhập các gói cần thiết. Các thư viện này rất quan trọng để tương tác với các tệp Excel trong dự án C# của bạn.
```csharp
using System.IO;
using Aspose.Cells;
```
Sau khi đã nhập các gói cần thiết, bạn có thể bắt đầu viết mã. 
Bây giờ, chúng ta hãy chia nhỏ quy trình thành các bước nhỏ hơn để bạn có thể dễ dàng thực hiện. Mỗi bước sẽ tập trung vào một phần cụ thể của quá trình triển khai, đảm bảo bạn có thể hiểu và áp dụng nhanh chóng. 
## Bước 1: Tạo một bảng tính và bảng tính mới
Trước khi bạn có thể áp dụng bất kỳ thiết lập bảo vệ nào, bạn cần tạo một sổ làm việc mới và chọn trang tính bạn muốn làm việc. Đây sẽ là tài liệu làm việc của bạn.
```csharp
// Đường dẫn đến thư mục tài liệu.
string dataDir = "Your Document Directory";
// Tạo thư mục nếu thư mục đó chưa có.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
	System.IO.Directory.CreateDirectory(dataDir);
// Tạo một bảng tính mới.
Workbook wb = new Workbook();
// Tạo một đối tượng bảng tính và lấy trang tính đầu tiên.
Worksheet sheet = wb.Worksheets[0];
```
Trong ví dụ này, chúng ta đang tạo một sổ làm việc mới với một trang tính duy nhất (là thiết lập mặc định khi bạn tạo một sổ làm việc mới bằng Aspose.Cells). Sau đó, chúng ta lấy trang tính đầu tiên trong sổ làm việc, đây sẽ là mục tiêu để bảo vệ hàng của chúng ta.
## Bước 2: Xác định đối tượng Style và StyleFlag
Bước tiếp theo là xác định các đối tượng kiểu và cờ kiểu. Các đối tượng này cho phép bạn sửa đổi các thuộc tính của ô, chẳng hạn như ô đó bị khóa hay mở khóa.
```csharp
// Xác định đối tượng kiểu.
Style style;
// Xác định đối tượng styleflag.
StyleFlag flag;
```
Bạn sẽ sử dụng các đối tượng này ở các bước sau để tùy chỉnh thuộc tính ô và áp dụng chúng vào bảng tính của mình.
## Bước 3: Mở khóa tất cả các cột trong bảng tính
Theo mặc định, tất cả các ô trong bảng tính Excel đều bị khóa. Tuy nhiên, khi bạn bảo vệ một bảng tính, trạng thái khóa sẽ được áp dụng. Để đảm bảo chỉ các hàng hoặc ô cụ thể được bảo vệ, trước tiên bạn có thể mở khóa tất cả các cột. Bước này rất cần thiết nếu bạn chỉ muốn bảo vệ một số hàng nhất định.
```csharp
// Lặp qua tất cả các cột trong bảng tính và mở khóa chúng.
for (int i = 0; i <= 255; i++)
{
    style = sheet.Cells.Columns[(byte)i].Style;
    style.IsLocked = false;
    flag = new StyleFlag();
    flag.Locked = true;
    sheet.Cells.Columns[(byte)i].ApplyStyle(style, flag);
}
```
Trong mã này, chúng tôi lặp qua tất cả 256 cột trong bảng tính (bảng tính Excel có tối đa 256 cột, được lập chỉ mục từ 0 đến 255) và đặt chúng `IsLocked` tài sản để `false`Hành động này đảm bảo rằng tất cả các cột đều được mở khóa, nhưng chúng tôi vẫn sẽ khóa các hàng cụ thể sau.
## Bước 4: Khóa hàng đầu tiên
Sau khi bạn đã mở khóa các cột, bước tiếp theo là khóa các hàng cụ thể mà bạn muốn bảo vệ. Trong ví dụ này, chúng tôi sẽ khóa hàng đầu tiên. Điều này đảm bảo rằng người dùng không thể sửa đổi hàng đó trong khi các hàng khác vẫn được mở khóa.
```csharp
// Nhận kiểu hàng đầu tiên.
style = sheet.Cells.Rows[0].Style;
// Khóa nó lại.
style.IsLocked = true;
// Tạo cờ.
flag = new StyleFlag();
// Thiết lập cài đặt khóa.
flag.Locked = true;
// Áp dụng kiểu cho hàng đầu tiên.
sheet.Cells.ApplyRowStyle(0, style, flag);
```
Ở đây, chúng ta truy cập vào kiểu của hàng đầu tiên và thiết lập nó `IsLocked` tài sản để `true`. Sau đó, chúng ta sử dụng `ApplyRowStyle()` phương pháp áp dụng kiểu khóa cho toàn bộ hàng. Bạn có thể lặp lại bước này để khóa bất kỳ hàng nào khác mà bạn muốn bảo vệ.
## Bước 5: Bảo vệ tờ giấy
Bây giờ chúng ta đã mở khóa và khóa các hàng cần thiết, đã đến lúc bảo vệ bảng tính. Việc bảo vệ đảm bảo rằng không ai có thể sửa đổi các hàng hoặc ô đã khóa trừ khi họ xóa mật khẩu bảo vệ (nếu được cung cấp).
```csharp
// Bảo vệ tờ giấy.
sheet.Protect(ProtectionType.All);
```
Trong bước này, chúng tôi áp dụng bảo vệ cho toàn bộ trang tính bằng cách sử dụng `ProtectionType.All`. Kiểu bảo vệ này có nghĩa là mọi khía cạnh của trang tính, bao gồm cả các hàng và ô bị khóa, đều được bảo vệ. Bạn cũng có thể tùy chỉnh kiểu bảo vệ này bằng cách chỉ định các kiểu bảo vệ khác nhau nếu cần.
## Bước 6: Lưu sổ làm việc
Cuối cùng, chúng ta cần lưu sổ làm việc sau khi áp dụng các kiểu và bảo vệ cần thiết. Sổ làm việc có thể được lưu ở nhiều định dạng khác nhau, chẳng hạn như Excel 97-2003, Excel 2010, v.v.
```csharp
// Lưu tệp Excel.
wb.Save(dataDir + "output.out.xls", SaveFormat.Excel97To2003);
```
Dòng mã này lưu sổ làm việc ở định dạng Excel 97-2003 với các thay đổi được áp dụng. Bạn có thể thay đổi định dạng tệp theo nhu cầu của mình bằng cách chọn từ nhiều định dạng `SaveFormat` tùy chọn.
## Phần kết luận
Và bạn đã có nó! Bạn đã học thành công cách bảo vệ các hàng trong bảng tính bằng Aspose.Cells cho .NET. Bằng cách làm theo các bước trên, bạn có thể mở khóa hoặc khóa bất kỳ hàng hoặc cột nào khi cần và áp dụng bảo vệ để đảm bảo tính toàn vẹn của dữ liệu.
## Câu hỏi thường gặp
### Làm thế nào tôi có thể bảo vệ nhiều hàng cùng một lúc?  
Bạn có thể lặp qua nhiều hàng và áp dụng kiểu khóa cho từng hàng riêng lẻ. Chỉ cần thay thế `0` với chỉ số hàng bạn muốn khóa.
### Tôi có thể đặt mật khẩu để bảo vệ trang tính không?  
Vâng! Bạn có thể chuyển mật khẩu cho `sheet.Protect()` phương pháp thực thi bảo vệ bằng mật khẩu.
### Tôi có thể mở khóa ô thay vì toàn bộ cột không?  
Có! Thay vì mở khóa các cột, bạn có thể mở khóa từng ô bằng cách sửa đổi thuộc tính kiểu của chúng.
### Điều gì xảy ra nếu tôi cố gắng chỉnh sửa một hàng được bảo vệ?  
Khi một hàng được bảo vệ, Excel sẽ ngăn chặn mọi chỉnh sửa được thực hiện trên các ô bị khóa trừ khi bạn bỏ bảo vệ trang tính.
### Tôi có thể bảo vệ các phạm vi cụ thể liên tiếp không?  
Có! Bạn có thể khóa các phạm vi riêng lẻ trong một hàng bằng cách thiết lập `IsLocked` thuộc tính cho các ô cụ thể trong phạm vi.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}