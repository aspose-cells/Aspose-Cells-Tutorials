---
title: Bảo vệ các ô và phạm vi trong trang tính bằng Aspose.Cells
linktitle: Bảo vệ các ô và phạm vi trong trang tính bằng Aspose.Cells
second_title: API xử lý Excel Aspose.Cells .NET
description: Tìm hiểu cách bảo vệ các ô và phạm vi trong bảng tính Excel bằng Aspose.Cells cho .NET. Làm theo hướng dẫn từng bước này để bảo mật bảng tính của bạn.
weight: 11
url: /vi/net/worksheet-security/protect-cells-and-ranges/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Bảo vệ các ô và phạm vi trong trang tính bằng Aspose.Cells

## Giới thiệu
Làm việc với bảng tính thường liên quan đến việc bảo vệ một số phần nhất định của trang tính khỏi những sửa đổi không mong muốn, đặc biệt là trong môi trường cộng tác. Trong hướng dẫn này, chúng ta sẽ khám phá cách bảo vệ các ô và phạm vi cụ thể trong bảng tính bằng Aspose.Cells cho .NET. Chúng tôi sẽ hướng dẫn bạn quy trình thiết lập trang tính được bảo vệ, chỉ định phạm vi nào có thể chỉnh sửa và lưu tệp. Đây có thể là một tính năng cực kỳ hữu ích khi bạn muốn hạn chế quyền truy cập vào dữ liệu nhạy cảm trong khi cho phép những người khác sửa đổi một số phần nhất định.
## Điều kiện tiên quyết
Trước khi bắt đầu hướng dẫn, hãy đảm bảo bạn đã đáp ứng đủ các điều kiện tiên quyết sau:
1. Aspose.Cells cho .NET: Bạn cần cài đặt thư viện Aspose.Cells trong dự án của mình. Nếu bạn chưa cài đặt, bạn có thể tải xuống từ[Trang web Aspose](https://releases.aspose.com/cells/net/).
2. Visual Studio: Hướng dẫn này giả định rằng bạn đang sử dụng Visual Studio hoặc bất kỳ IDE tương tự nào hỗ trợ phát triển C#.
3. Kiến thức cơ bản về C#: Bạn nên quen thuộc với những kiến thức cơ bản về lập trình C# và cách thiết lập một dự án trong Visual Studio.
4.  Giấy phép Aspose.Cells: Trong khi Aspose cung cấp bản dùng thử miễn phí, một giấy phép hợp lệ sẽ cho phép bạn sử dụng toàn bộ bộ tính năng của thư viện. Nếu bạn không có, bạn có thể lấy một[giấy phép tạm thời ở đây](https://purchase.aspose.com/temporary-license/).
Khi bạn đã đảm bảo chuẩn bị đầy đủ những điều trên, chúng ta có thể chuyển sang phần mã hóa.
## Nhập gói
Để làm việc với Aspose.Cells, trước tiên bạn phải nhập các không gian tên cần thiết vào tệp C# của mình. Sau đây là cách bạn có thể nhập chúng:
```csharp
using System.IO;
using Aspose.Cells;
```
 Các`Aspose.Cells` không gian tên cung cấp cho bạn quyền truy cập vào các chức năng cốt lõi để thao tác các tệp Excel và`System.IO` được sử dụng cho các thao tác với tệp như lưu sổ làm việc.
Bây giờ, chúng ta hãy cùng tìm hiểu các bước để bảo vệ các ô và phạm vi trong bảng tính bằng Aspose.Cells.
## Bước 1: Thiết lập môi trường của bạn
Trước tiên, hãy tạo một thư mục nơi bạn muốn lưu các tệp Excel của mình. Nếu thư mục chưa tồn tại, chúng tôi sẽ tạo một thư mục. Điều này giúp đảm bảo rằng bạn có một nơi để lưu trữ tệp đầu ra của mình.
```csharp
// Xác định đường dẫn đến thư mục tài liệu của bạn
string dataDir = "Your Document Directory";
// Kiểm tra xem thư mục có tồn tại không, nếu không, hãy tạo nó
bool IsExists = Directory.Exists(dataDir);
if (!IsExists)
    Directory.CreateDirectory(dataDir);
```
 Ở đây, chúng tôi đang sử dụng`System.IO.Directory.Exists()` để kiểm tra xem thư mục có tồn tại không, nếu không, chúng ta tạo nó bằng cách sử dụng`Directory.CreateDirectory()`.
## Bước 2: Tạo một Workbook mới
Bây giờ, hãy khởi tạo một đối tượng Workbook mới. Đối tượng này sẽ đóng vai trò là tệp Excel trong đó chúng ta sẽ xác định các ô và phạm vi của mình.
```csharp
// Khởi tạo một đối tượng Workbook mới
Workbook book = new Workbook();
```
 Các`Workbook` lớp là điểm vào để làm việc với các tệp Excel trong Aspose.Cells. Nó đại diện cho tài liệu Excel.
## Bước 3: Truy cập Bảng tính mặc định
Mỗi sổ làm việc mới tạo đều có một bảng tính mặc định. Chúng tôi sẽ lấy nó để làm việc với nội dung của nó.
```csharp
// Lấy trang tính đầu tiên (mặc định) trong sổ làm việc
Worksheet sheet = book.Worksheets[0];
```
 Đây,`Worksheets[0]` cung cấp cho chúng ta trang tính đầu tiên trong bảng tính (chỉ mục bắt đầu từ 0).
## Bước 4: Xác định phạm vi có thể chỉnh sửa
Để bảo vệ một số phần nhất định của bảng tính trong khi cho phép người dùng chỉnh sửa các ô cụ thể, chúng ta cần xác định phạm vi có thể chỉnh sửa. Chúng ta sẽ tạo một phạm vi có thể chỉnh sửa và thêm vào bộ sưu tập AllowEditRanges của bảng tính.
```csharp
// Nhận bộ sưu tập AllowEditRanges
ProtectedRangeCollection allowRanges = sheet.AllowEditRanges;
// Xác định một ProtectedRange và thêm nó vào bộ sưu tập
int idx = allowRanges.Add("r2", 1, 1, 3, 3);
ProtectedRange protectedRange = allowRanges[idx];
```
Trong đoạn mã trên:
- `"r2"` là tên của phạm vi có thể chỉnh sửa.
-  Các con số`1, 1, 3, 3` biểu diễn chỉ số hàng và cột bắt đầu và kết thúc cho phạm vi (tức là từ ô B2 đến D4).
## Bước 5: Đặt mật khẩu cho phạm vi được bảo vệ
Bây giờ chúng ta đã xác định phạm vi có thể chỉnh sửa, hãy thêm mật khẩu để bảo vệ phạm vi đó. Điều này có nghĩa là người dùng sẽ cần mật khẩu để chỉnh sửa phạm vi cụ thể này.
```csharp
// Chỉ định mật khẩu cho phạm vi có thể chỉnh sửa
protectedRange.Password = "123";
```
 Ở đây, chúng tôi đã đặt mật khẩu là`"123"`, nhưng bạn có thể chọn bất kỳ mật khẩu an toàn nào. Bước này rất cần thiết để kiểm soát quyền truy cập vào các khu vực có thể chỉnh sửa.
## Bước 6: Bảo vệ toàn bộ trang tính
Ở giai đoạn này, chúng ta sẽ bảo vệ toàn bộ trang tính. Bảo vệ trang tính đảm bảo rằng các phần khác của trang tính, ngoại trừ các phạm vi được phép, không thể chỉnh sửa được.
```csharp
// Bảo vệ trang tính bằng loại bảo vệ được chỉ định (Tất cả)
sheet.Protect(ProtectionType.All);
```
Thao tác này đảm bảo rằng tất cả các ô trong trang tính đều bị khóa, ngoại trừ những ô nằm trong phạm vi có thể chỉnh sửa.
## Bước 7: Lưu sổ làm việc
Cuối cùng, chúng ta lưu sổ làm việc vào một tệp. Trang tính được bảo vệ sẽ được lưu dưới tên bạn chỉ định.
```csharp
// Lưu tệp Excel vào thư mục đã chỉ định
book.Save(dataDir + "protectedrange.out.xls");
```
 Tại đây, tệp Excel sẽ được lưu dưới dạng`protectedrange.out.xls` trong thư mục chúng tôi đã xác định trước đó. Nếu bạn muốn lưu dưới tên hoặc định dạng khác, bạn có thể sửa đổi tên tệp và phần mở rộng.
## Phần kết luận
Bằng cách làm theo hướng dẫn này, bạn đã học cách bảo vệ các ô và phạm vi trong bảng tính Excel bằng Aspose.Cells for .NET. Phương pháp này cung cấp cho bạn sự linh hoạt trong việc kiểm soát những vùng nào trong bảng tính của bạn có thể chỉnh sửa và những vùng nào không thể. Bây giờ bạn có thể áp dụng những kỹ năng này vào các dự án của riêng mình, đảm bảo dữ liệu nhạy cảm của bạn được bảo mật trong khi cung cấp các vùng có thể chỉnh sửa cho người dùng.
Hãy nhớ rằng Aspose.Cells cung cấp một bộ công cụ mạnh mẽ để làm việc với các tệp Excel và đây chỉ là một trong nhiều tính năng bạn có thể sử dụng. 
## Câu hỏi thường gặp
### Tôi có thể chỉ bảo vệ một số ô nhất định trong bảng tính không?
 Có, bằng cách sử dụng`AllowEditRanges` thuộc tính, bạn có thể chỉ định ô hoặc phạm vi nào có thể được chỉnh sửa trong khi phần còn lại của bảng tính vẫn được bảo vệ.
### Tôi có thể gỡ bỏ chế độ bảo vệ sau này không?
 Có, bạn có thể bỏ bảo vệ một bảng tính bằng cách sử dụng`Unprotect()` phương pháp này và nếu đã đặt mật khẩu, bạn sẽ cần phải cung cấp mật khẩu.
### Làm thế nào để bảo vệ toàn bộ trang tính bằng mật khẩu?
 Để bảo vệ toàn bộ trang tính, bạn chỉ cần sử dụng`Protect()` phương pháp có hoặc không có mật khẩu. Ví dụ,`sheet.Protect("password")`.
### Tôi có thể thêm nhiều phạm vi có thể chỉnh sửa không?
 Chắc chắn rồi! Bạn có thể thêm nhiều phạm vi có thể chỉnh sửa tùy theo nhu cầu của bạn bằng cách gọi`allowRanges.Add()` nhiều lần.
### Aspose.Cells còn cung cấp những tính năng bảo mật nào khác?
Aspose.Cells hỗ trợ nhiều tính năng bảo mật như mã hóa sổ làm việc, đặt mật khẩu tệp và bảo vệ ô và trang tính.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
