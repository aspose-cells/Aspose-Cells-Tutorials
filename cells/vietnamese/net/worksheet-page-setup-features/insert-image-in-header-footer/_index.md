---
title: Chèn hình ảnh vào Header Footer của Worksheet
linktitle: Chèn hình ảnh vào Header Footer của Worksheet
second_title: API xử lý Excel Aspose.Cells .NET
description: Tìm hiểu cách chèn hình ảnh vào đầu trang/chân trang dễ dàng bằng Aspose.Cells cho .NET trong hướng dẫn toàn diện này.
weight: 15
url: /vi/net/worksheet-page-setup-features/insert-image-in-header-footer/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Chèn hình ảnh vào Header Footer của Worksheet

## Giới thiệu
Khi nói đến việc tạo bảng tính Excel trông chuyên nghiệp, những chi tiết nhỏ có thể tạo ra sự khác biệt lớn. Một trong những chi tiết như vậy là thêm hình ảnh vào đầu trang hoặc chân trang của bảng tính. Đây là một cách chắc chắn để tạo thương hiệu cho tài liệu của bạn và thấm nhuần chúng với một chút tính chuyên nghiệp. Mặc dù điều này có vẻ phức tạp, đặc biệt là nếu bạn không phải là chuyên gia công nghệ, nhưng việc sử dụng Aspose.Cells cho .NET sẽ đơn giản hóa quy trình đáng kể. Vì vậy, hãy cùng tìm hiểu cách thực hiện từng bước một!
## Điều kiện tiên quyết
Trước khi bắt đầu chèn hình ảnh vào phần đầu trang và chân trang, hãy đảm bảo bạn đã chuẩn bị một số thứ sau:
1. Visual Studio: Đảm bảo bạn đã cài đặt Visual Studio trên máy tính của mình. IDE này là một công cụ mạnh mẽ cho phát triển .NET.
2.  Aspose.Cells cho .NET: Bạn có thể dùng thử miễn phí hoặc mua nếu bạn thực sự muốn tối đa hóa khả năng Excel của mình. Tải xuống[đây](https://releases.aspose.com/cells/net/).
3. Kiến thức cơ bản về C#: Hiểu biết cơ bản về C# và cách chạy ứng dụng .NET sẽ rất có lợi.
4. Tệp hình ảnh: Chuẩn bị một tệp hình ảnh như logo công ty. Trong ví dụ này, chúng tôi sẽ gọi nó là`aspose-logo.jpg`.
## Nhập gói
Để bắt đầu hành trình lập trình của chúng ta, hãy đảm bảo bạn đã nhập các gói cần thiết vào dự án C# của mình. Bạn cần không gian tên Aspose.Cells chứa tất cả các lớp và phương thức mà bạn sẽ làm việc.
Sau đây là cách đưa nó vào mã của bạn:
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
Bây giờ chúng ta đã thiết lập xong mọi thứ, hãy cùng thực hiện quy trình theo các bước dễ làm theo.
## Bước 1: Thiết lập thư mục của bạn
Xác định nơi lưu trữ tệp của bạn.
 Trước tiên, chúng ta cần chỉ định đường dẫn đến thư mục tài liệu của chúng ta nơi tệp Excel và hình ảnh được đặt. Bạn có thể đặt bất kỳ đường dẫn nào; chỉ cần thay thế`"Your Document Directory"` với đường dẫn thư mục thực tế của bạn.
```csharp
string dataDir = "Your Document Directory";
```
## Bước 2: Tạo một đối tượng Workbook
Tạo một phiên bản cho bảng tính Excel của bạn.
Sau khi thiết lập đường dẫn, bây giờ chúng ta cần tạo một phiên bản mới của bảng tính để chèn hình ảnh vào đó. 
```csharp
Workbook workbook = new Workbook();
```
## Bước 3: Tải hình ảnh của bạn
Mở và đọc tệp hình ảnh, chuyển đổi nó thành mảng byte để xử lý.
Tiếp theo, chúng ta sẽ thiết lập đường dẫn cho hình ảnh của mình (logo, trong trường hợp này) và khởi tạo một`FileStream` đối tượng để đọc hình ảnh. Sau đây là cách thực hiện:
```csharp
string logo_url = dataDir + "aspose-logo.jpg";
// Khai báo đối tượng FileStream
FileStream inFile;
byte[] binaryData;
// Tạo phiên bản của đối tượng FileStream
inFile = new FileStream(logo_url, FileMode.Open, FileAccess.Read);
```
## Bước 4: Đọc hình ảnh vào một mảng byte
Chuyển đổi dữ liệu tệp hình ảnh thành mảng byte.
Để làm việc với hình ảnh, chúng ta cần đọc nó vào một mảng byte. Điều này rất cần thiết vì nó cho phép chúng ta thao tác hình ảnh trong ứng dụng.
```csharp
// Khởi tạo mảng byte của kích thước đối tượng FileStream
binaryData = new byte[inFile.Length];
// Đọc một khối byte từ luồng và ghi dữ liệu vào bộ đệm của mảng byte đã cho.
long bytesRead = inFile.Read(binaryData, 0, (int)inFile.Length);
```
## Bước 5: Cấu hình Thiết lập Trang cho Đầu trang/Chân trang
Truy cập đối tượng PageSetup để thao tác phần đầu trang và chân trang.
Để chèn hình ảnh của chúng ta, chúng ta cần cấu hình đối tượng thiết lập trang. Điều này cho phép chúng ta tùy chỉnh tiêu đề của bảng tính:
```csharp
PageSetup pageSetup = workbook.Worksheets[0].PageSetup;
```
## Bước 6: Chèn Logo vào Header
Nhúng hình ảnh vào phần tiêu đề của bảng tính.
Đây chính là khoảnh khắc kỳ diệu! Chúng tôi sẽ chèn logo của mình vào phần trung tâm của tiêu đề:
```csharp
// Đặt logo/hình ảnh vào phần trung tâm của tiêu đề trang.
pageSetup.SetHeaderPicture(1, binaryData);
// Thiết lập kịch bản cho logo/hình ảnh
pageSetup.SetHeader(1, "&G");
// Đặt tên của Sheet ở phần bên phải của tiêu đề trang bằng tập lệnh
pageSetup.SetHeader(2, "&A");
```
## Bước 7: Lưu sổ làm việc của bạn
Lưu những thay đổi của bạn vào một tệp Excel mới.
Sau khi cấu hình mọi thứ, đã đến lúc lưu sổ làm việc của chúng ta. Đảm bảo cung cấp tên mới cho tệp đầu ra của bạn:
```csharp
workbook.Save(dataDir + "InsertImageInHeaderFooter_out.xls");
```
## Bước 8: Dọn dẹp tài nguyên
Đóng FileStream để giải phóng tài nguyên.
 Cuối cùng, sau khi thao tác xong, đừng quên dọn dẹp bằng cách đóng lại`FileStream`!
```csharp
inFile.Close();
```
## Phần kết luận
Và bạn đã có nó! Bạn đã chèn thành công một hình ảnh vào phần đầu trang/chân trang của một bảng tính Excel bằng Aspose.Cells cho .NET. Thật đơn giản phải không? Khi bạn hiểu các bước, bạn có thể tùy chỉnh thêm để phù hợp với nhu cầu cụ thể của mình. Cho dù bạn đang muốn tạo thương hiệu cho báo cáo cho doanh nghiệp của mình hay chỉ đơn giản là thêm nét cá nhân, thì kỹ thuật này vô cùng hữu ích. 
## Câu hỏi thường gặp
### Tôi có thể sử dụng bất kỳ định dạng hình ảnh nào không?
Có, Aspose.Cells hỗ trợ nhiều định dạng hình ảnh bao gồm JPEG, PNG và BMP cho hình ảnh đầu trang và chân trang.
### Aspose.Cells có miễn phí sử dụng không?
 Aspose.Cells cung cấp bản dùng thử miễn phí, nhưng để tiếp tục sử dụng, bạn sẽ cần mua giấy phép. Tìm hiểu thêm về giá cả[đây](https://purchase.aspose.com/buy).
### Làm thế nào để truy cập tài liệu Aspose.Cells?
 Bạn có thể tìm hiểu sâu hơn về các tính năng và chức năng của Aspose.Cells bằng cách truy cập[tài liệu](https://reference.aspose.com/cells/net/).
### Tôi có thể sử dụng Aspose.Cells mà không cần Visual Studio không?
Có, miễn là bạn có môi trường chạy .NET, bạn có thể sử dụng Aspose.Cells trong bất kỳ môi trường phát triển nào tương thích với .NET.
### Tôi phải làm gì nếu gặp vấn đề?
 Nếu bạn gặp bất kỳ vấn đề nào hoặc cần hỗ trợ, hãy kiểm tra[Diễn đàn hỗ trợ Aspose](https://forum.aspose.com/c/cells/9) để được cộng đồng và nhà phát triển giúp đỡ.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
