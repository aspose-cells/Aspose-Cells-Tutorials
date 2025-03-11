---
title: Chèn Đối tượng OLE vào Excel
linktitle: Chèn Đối tượng OLE vào Excel
second_title: API xử lý Excel Aspose.Cells .NET
description: Tìm hiểu cách chèn các đối tượng OLE vào tệp Excel bằng Aspose.Cells cho .NET trong hướng dẫn toàn diện này có hướng dẫn từng bước.
weight: 11
url: /vi/net/excel-ole-picture-objects/insert-ole-object-into-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Chèn Đối tượng OLE vào Excel

## Giới thiệu
Cho dù bạn đang nhúng hình ảnh, biểu đồ hay bất kỳ tệp nào khác, sử dụng Aspose.Cells cho .NET cung cấp một cách đơn giản để thực hiện việc này. Trong hướng dẫn này, chúng ta sẽ khám phá các bước cần thiết để chèn đối tượng OLE vào trang tính Excel. Cuối cùng, bạn sẽ có thể cải thiện sổ làm việc Excel của mình bằng các nhúng được cá nhân hóa có thể gây ấn tượng với khán giả của bạn hoặc phục vụ nhiều nhu cầu chuyên nghiệp khác nhau. 
## Điều kiện tiên quyết
Trước khi đi sâu vào chi tiết của mã, bạn cần chuẩn bị một số thứ sau:
1. Visual Studio: Lý tưởng nhất là bạn nên làm việc trong môi trường hỗ trợ .NET, như Visual Studio. IDE này giúp bạn dễ dàng viết, kiểm tra và gỡ lỗi ứng dụng của mình.
2. Thư viện Aspose.Cells: Bạn phải cài đặt thư viện Aspose.Cells. Bạn có thể tải xuống thông qua trình quản lý gói NuGet hoặc tải xuống trực tiếp từ[Trang web Aspose](https://releases.aspose.com/cells/net/).
3.  Tệp mẫu: Để minh họa, hãy đảm bảo bạn có hình ảnh (như`logo.jpg`) và một tệp Excel (`book1.xls`) để làm việc. Những điều này sẽ được tham chiếu trong mã.
4. Hiểu biết cơ bản về C#: Sự quen thuộc với C# sẽ giúp bạn hiểu các bước liên quan và thực hiện các sửa đổi nếu cần thiết.
Khi bạn đã chuẩn bị mọi thứ xong xuôi, đã đến lúc xắn tay áo và bắt đầu chèn các đối tượng OLE vào Excel!
## Nhập gói
Để thao tác các tệp Excel bằng Aspose.Cells, trước tiên bạn cần nhập các gói cần thiết. Thêm các không gian tên sau vào đầu tệp C# của bạn:
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
Thiết lập cơ bản này cho phép bạn tương tác với sổ làm việc, bảng tính và các thành phần thiết yếu khác cần thiết cho nhiệm vụ của bạn.
Chúng ta hãy chia nhỏ điều này thành các bước dễ hiểu hơn.
## Bước 1: Thiết lập thư mục tài liệu của bạn
Bước đầu tiên là xác định nơi lưu trữ tài liệu của bạn. Điều này khá đơn giản.
```csharp
// Đường dẫn đến thư mục tài liệu.
string dataDir = "Your Document Directory";
```
 Hãy chắc chắn thay thế`"Your Document Directory"` với đường dẫn thư mục thực tế trên hệ thống nơi bạn dự định lưu các tệp của mình.
## Bước 2: Tạo thư mục nếu nó không tồn tại
Tiếp theo, chúng ta muốn đảm bảo rằng thư mục này tồn tại. Nếu không, chúng ta cần tạo nó.
```csharp
// Tạo thư mục nếu thư mục đó chưa có.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Kiểm tra đơn giản này giúp chương trình của bạn tránh phát sinh những lỗi không cần thiết sau này.
## Bước 3: Tạo một Workbook mới
Bây giờ, hãy tạo một bảng tính mới để làm việc với các đối tượng OLE.
```csharp
// Tạo một Workbook mới.
Workbook workbook = new Workbook();
```
Sổ làm việc mới này sẽ đóng vai trò như khung vẽ cho đối tượng OLE mà bạn dự định chèn.
## Bước 4: Nhận bảng tính đầu tiên
Sau khi có sổ làm việc, chúng ta cần lấy bảng tính đầu tiên. Thông thường, đây là nơi bạn sẽ làm việc tích cực nhất.
```csharp
// Nhận bài tập đầu tiên.
Worksheet sheet = workbook.Worksheets[0];
```
Thật tuyệt và đơn giản! Chúng ta đã sẵn sàng để bắt đầu thêm nội dung vào bảng tính này.
## Bước 5: Xác định đường dẫn cho hình ảnh
Bây giờ, hãy thiết lập đường dẫn cho hình ảnh bạn muốn nhúng vào tệp Excel.
```csharp
//Xác định biến chuỗi để lưu trữ đường dẫn hình ảnh.
string ImageUrl = dataDir + "logo.jpg";
```
 Hãy đảm bảo đường dẫn này phản ánh chính xác vị trí của bạn`logo.jpg` tập tin được lưu trữ.
## Bước 6: Tải hình ảnh vào một mảng byte
Chúng ta cần đọc hình ảnh thành định dạng mà chúng ta có thể làm việc. Để làm điều này, chúng ta mở luồng tệp và đọc dữ liệu của nó vào một mảng byte.
```csharp
// Đưa hình ảnh vào luồng.
FileStream fs = File.OpenRead(ImageUrl);
// Định nghĩa một mảng byte.
byte[] imageData = new Byte[fs.Length];
// Lấy hình ảnh vào mảng byte từ các luồng.
fs.Read(imageData, 0, imageData.Length);
// Đóng luồng.
fs.Close();
```
Bằng cách đọc hình ảnh vào một mảng byte, chúng ta chuẩn bị hình ảnh để chèn vào bảng tính Excel.
## Bước 7: Lấy đường dẫn tệp Excel
Bây giờ, chúng ta hãy xác định vị trí lưu trữ tệp Excel của bạn.
```csharp
// Nhận đường dẫn tệp Excel trong một biến.
string path = dataDir + "book1.xls";
```
Một lần nữa, hãy đảm bảo rằng đường dẫn này là chính xác và trỏ đến đúng tệp.
## Bước 8: Tải tệp Excel vào một mảng byte
Giống như cách chúng ta đã làm với hình ảnh, chúng ta cần tải chính tệp Excel vào một mảng byte.
```csharp
// Đưa tập tin vào luồng.
fs = File.OpenRead(path);
//Định nghĩa một mảng byte.
byte[] objectData = new Byte[fs.Length];
// Lưu trữ tệp từ các luồng.
fs.Read(objectData, 0, objectData.Length);
// Đóng luồng.
fs.Close();
```
Thao tác này chuẩn bị tệp Excel để nhúng đối tượng OLE của chúng ta.
## Bước 9: Thêm Đối tượng OLE vào Bảng tính
Sau khi dữ liệu đã sẵn sàng, chúng ta có thể chèn đối tượng OLE vào bảng tính.
```csharp
// Thêm đối tượng OLE vào bảng tính có hình ảnh.
sheet.OleObjects.Add(14, 3, 200, 220, imageData);
// Đặt dữ liệu đối tượng OLE nhúng.
sheet.OleObjects[0].ObjectData = objectData;
```
 Dòng này tạo ra một đối tượng nhúng trong tài liệu Excel. Các tham số`(14, 3, 200, 220)` chỉ định vị trí và kích thước của đối tượng nhúng. Điều chỉnh các giá trị này khi cần thiết cho trường hợp sử dụng cụ thể của bạn.
## Bước 10: Lưu tệp Excel
Cuối cùng, đã đến lúc lưu những thay đổi của bạn vào tệp Excel.
```csharp
// Lưu tệp excel
workbook.Save(dataDir + "output.out.xls");
```
Dòng này lưu sổ làm việc với đối tượng OLE được chèn vào. Hãy chắc chắn sử dụng tên có ý nghĩa!
## Phần kết luận
Chèn các đối tượng OLE vào các tệp Excel bằng Aspose.Cells cho .NET không chỉ có lợi mà còn đơn giản khi bạn chia nhỏ thành các bước dễ quản lý. Công cụ mạnh mẽ này cho phép bạn cải thiện các tài liệu Excel của mình, khiến chúng trở nên tương tác và hấp dẫn về mặt hình ảnh. Cho dù bạn là nhà phát triển muốn tự động hóa các báo cáo hay nhà phân tích muốn trình bày dữ liệu hiệu quả, việc thành thạo nhúng OLE có thể là một tài sản quan trọng trong bộ công cụ của bạn.
## Câu hỏi thường gặp
### Đối tượng OLE là gì?
Đối tượng OLE là một tệp có thể nhúng vào tài liệu, cho phép các ứng dụng khác nhau tích hợp với nhau. Ví dụ bao gồm hình ảnh, tài liệu Word và bản trình bày.
### Tôi có thể sử dụng Aspose.Cells miễn phí không?
 Bạn có thể dùng thử Aspose.Cells miễn phí bằng cách tải xuống phiên bản dùng thử có sẵn trên[trang web](https://releases.aspose.com/).
### Tôi có thể sử dụng định dạng tệp nào với các đối tượng OLE?
Bạn có thể sử dụng nhiều định dạng khác nhau bao gồm hình ảnh (JPEG, PNG), tài liệu Word, PDF, v.v., tùy thuộc vào ứng dụng của bạn.
### Aspose.Cells có được hỗ trợ trên mọi nền tảng không?
Aspose.Cells for .NET chủ yếu được thiết kế cho nền tảng .NET. Tuy nhiên, chức năng có thể khác nhau giữa các môi trường Windows, Mac hoặc đám mây khác nhau.
### Tôi có thể nhận được trợ giúp như thế nào nếu gặp vấn đề?
 Bạn có thể truy cập hỗ trợ thông qua[Diễn đàn Aspose](https://forum.aspose.com/c/cells/9) nơi các nhà phát triển chia sẻ hiểu biết và giải pháp.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
