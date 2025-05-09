---
"description": "Học cách tạo các phạm vi có thể chỉnh sửa trong bảng tính Excel bằng Aspose.Cells cho .NET, cho phép chỉnh sửa các ô cụ thể trong khi bảo vệ phần còn lại bằng tính năng bảo vệ bảng tính."
"linktitle": "Cho phép người dùng chỉnh sửa phạm vi trong bảng tính bằng Aspose.Cells"
"second_title": "API xử lý Excel Aspose.Cells .NET"
"title": "Cho phép người dùng chỉnh sửa phạm vi trong bảng tính bằng Aspose.Cells"
"url": "/vi/net/worksheet-security/allow-edit-ranges/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Cho phép người dùng chỉnh sửa phạm vi trong bảng tính bằng Aspose.Cells

## Giới thiệu
Tài liệu Excel thường chứa dữ liệu nhạy cảm hoặc nội dung có cấu trúc mà bạn muốn bảo vệ khỏi việc chỉnh sửa không mong muốn. Tuy nhiên, có thể có những ô hoặc phạm vi cụ thể mà bạn muốn cho phép chỉnh sửa đối với một số người dùng nhất định. Đó là lúc Aspose.Cells for .NET xuất hiện như một công cụ mạnh mẽ cho phép bạn bảo vệ toàn bộ bảng tính trong khi vẫn cấp quyền chỉnh sửa cho các phạm vi được chỉ định. Hãy tưởng tượng việc chia sẻ bảng tính ngân sách trong đó chỉ một số ô nhất định có thể chỉnh sửa và những ô khác vẫn được bảo mật—Aspose.Cells giúp việc này trở nên dễ dàng và hiệu quả.
## Điều kiện tiên quyết
Trước khi bắt đầu phần mã hóa, hãy đảm bảo rằng bạn có mọi thứ cần thiết:
- Aspose.Cells cho .NET: Đảm bảo bạn đã cài đặt thư viện Aspose.Cells cho .NET. Bạn có thể tải xuống [đây](https://releases.aspose.com/cells/net/).
- Môi trường phát triển: Visual Studio hoặc bất kỳ IDE nào tương thích với C#.
- .NET Framework: Phiên bản 4.0 trở lên.
- Giấy phép: Hãy cân nhắc việc xin giấy phép để tránh những hạn chế dùng thử. Bạn có thể xin [giấy phép tạm thời ở đây](https://purchase.aspose.com/temporary-license/).
## Nhập gói
Đảm bảo bao gồm không gian tên Aspose.Cells cần thiết vào đầu mã của bạn:
```csharp
using System.IO;
using Aspose.Cells;
```
Điều này sẽ đảm bảo rằng bạn có thể truy cập tất cả các lớp và phương thức cần thiết để thiết lập phạm vi được bảo vệ trong tệp Excel.
Bây giờ nền tảng đã sẵn sàng, chúng ta hãy cùng xem xét mã một cách chi tiết, từng bước một.
## Bước 1: Thiết lập thư mục
Trước khi làm việc với tệp, bạn cần thiết lập thư mục nơi bạn sẽ lưu tệp Excel. Điều này đảm bảo tệp của bạn được sắp xếp hợp lý và lưu trữ an toàn.
```csharp
// Xác định đường dẫn đến thư mục tài liệu của bạn
string dataDir = "Your Document Directory";
// Kiểm tra xem thư mục có tồn tại không, nếu không, hãy tạo nó
bool isExists = Directory.Exists(dataDir);
if (!isExists)
{
    Directory.CreateDirectory(dataDir);
}
```
Phần mã này đảm bảo rằng thư mục của bạn đã sẵn sàng cho các hoạt động tệp. Hãy nghĩ về nó như việc đặt nền tảng cho mọi thứ tiếp theo.
## Bước 2: Khởi tạo Workbook và Worksheet
Bây giờ, chúng ta hãy tiếp tục bằng cách tạo một bảng tính mới và truy cập vào trang tính mặc định của bảng tính đó.
```csharp
// Khởi tạo một Workbook mới
Workbook book = new Workbook();
// Truy cập trang tính đầu tiên trong sổ làm việc
Worksheet sheet = book.Worksheets[0];
```
Ở đây, chúng ta đang khởi tạo một sổ làm việc Excel và chọn trang tính đầu tiên trong đó. Trang tính này sẽ là canvas nơi chúng ta áp dụng các thiết lập bảo vệ và xác định phạm vi có thể chỉnh sửa.
## Bước 3: Truy cập Bộ sưu tập Cho phép chỉnh sửa phạm vi
Aspose.Cells có một tính năng được gọi là `AllowEditRanges`, là tập hợp các phạm vi có thể chỉnh sửa được, ngay cả khi bảng tính được bảo vệ.
```csharp
// Truy cập bộ sưu tập Cho phép chỉnh sửa phạm vi
ProtectedRangeCollection allowRanges = sheet.AllowEditRanges;
```
Dòng này thiết lập quyền truy cập vào một tập hợp các phạm vi đặc biệt có thể chỉnh sửa được. Hãy coi nó như một vùng “VIP” trong bảng tính của bạn, nơi chỉ những phạm vi cụ thể mới được phép bỏ qua chế độ bảo vệ.
## Bước 4: Xác định và tạo phạm vi được bảo vệ
Bây giờ, hãy định nghĩa và tạo một phạm vi được bảo vệ trong bảng tính của chúng ta. Chúng ta sẽ chỉ định ô bắt đầu và kết thúc cho phạm vi này.
```csharp
// Xác định biến ProtectedRange
ProtectedRange protectedRange;
// Thêm một phạm vi mới vào bộ sưu tập với tên và vị trí ô cụ thể
int idx = allowRanges.Add("EditableRange", 1, 1, 3, 3);
protectedRange = allowRanges[idx];
```
Trong khối mã này:
- `EditableRange` là tên được gán cho phạm vi.
- Các số (1, 1, 3, 3) xác định tọa độ phạm vi, nghĩa là nó bắt đầu từ ô B2 (hàng 1, cột 1) đến ô D4 (hàng 3, cột 3).
## Bước 5: Đặt mật khẩu cho phạm vi được bảo vệ
Để tăng thêm tính bảo mật, bạn có thể đặt mật khẩu cho phạm vi được bảo vệ. Bước này thêm một lớp bảo vệ để đảm bảo rằng chỉ những người dùng được ủy quyền mới có thể chỉnh sửa phạm vi.
```csharp
// Đặt mật khẩu cho phạm vi có thể chỉnh sửa
protectedRange.Password = "123";
```
Ở đây, chúng tôi đã thêm mật khẩu (`"123"`) vào phạm vi được bảo vệ. Yêu cầu về mật khẩu này cung cấp thêm một cấp độ kiểm soát đối với những người có thể thực hiện thay đổi.
## Bước 6: Bảo vệ bảng tính
Với phạm vi có thể chỉnh sửa được thiết lập, bước tiếp theo là bảo vệ toàn bộ bảng tính. Thiết lập bảo vệ này sẽ đảm bảo rằng tất cả các ô nằm ngoài phạm vi đã xác định đều bị khóa và không thể chỉnh sửa.
```csharp
// Áp dụng bảo vệ cho trang tính, khiến tất cả các ô khác không thể chỉnh sửa được
sheet.Protect(ProtectionType.All);
```
Các `Protect` phương pháp khóa toàn bộ bảng tính, ngoại trừ các phạm vi chúng ta đã xác định là có thể chỉnh sửa. Bước này về cơ bản tạo ra một môi trường "chỉ đọc" an toàn, với quyền truy cập vào các ô cụ thể khi cần.
## Bước 7: Lưu sổ làm việc
Bước cuối cùng là lưu sổ làm việc để các thiết lập của bạn được áp dụng và lưu trữ.
```csharp
// Lưu tệp Excel vào thư mục đã chỉ định
book.Save(dataDir + "protectedrange.out.xls");
```
Ở bước này, chúng ta sẽ lưu sổ làm việc của mình dưới dạng “protectedrange.out.xls” trong thư mục đã thiết lập ở Bước 1. Bây giờ, bạn đã có một tệp Excel an toàn, đầy đủ chức năng, trong đó chỉ có thể chỉnh sửa một số phạm vi nhất định!
## Phần kết luận
Aspose.Cells for .NET cung cấp một cách tuyệt vời để quản lý bảo vệ và quyền trong các tệp Excel của bạn. Bằng cách tạo các phạm vi có thể chỉnh sửa, bạn có thể bảo mật các bảng tính của mình trong khi vẫn cho phép các khu vực cụ thể vẫn có thể truy cập được. Chức năng này đặc biệt hữu ích cho các tài liệu cộng tác, trong đó chỉ một vài ô được mở để chỉnh sửa trong khi các ô khác vẫn bị khóa.
## Câu hỏi thường gặp
### Tôi có thể thêm nhiều phạm vi có thể chỉnh sửa vào một bảng tính không?
Có, bạn có thể thêm nhiều phạm vi bằng cách chỉ cần lặp lại `allowRanges.Add()` phương pháp cho mỗi phạm vi mới.
### Nếu sau này tôi muốn xóa phạm vi được bảo vệ thì sao?
Sử dụng `allowRanges.RemoveAt()` phương pháp với chỉ số của phạm vi bạn muốn xóa.
### Tôi có thể đặt mật khẩu khác nhau cho mỗi phạm vi không?
Hoàn toàn. Mỗi `ProtectedRange` có thể có mật khẩu riêng, giúp bạn kiểm soát chặt chẽ hơn.
### Điều gì xảy ra nếu tôi bảo vệ bảng tính mà không có bất kỳ phạm vi nào có thể chỉnh sửa?
Nếu bạn không xác định phạm vi có thể chỉnh sửa, toàn bộ bảng tính sẽ không thể chỉnh sửa được sau khi được bảo vệ.
### Phạm vi được bảo vệ có hiển thị cho người dùng khác không?
Không, bảo vệ là nội bộ. Người dùng sẽ chỉ được nhắc nhập mật khẩu nếu họ cố gắng chỉnh sửa vùng được bảo vệ.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}