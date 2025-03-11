---
title: Vị trí hình ảnh (Tỷ lệ) trong Excel
linktitle: Vị trí hình ảnh (Tỷ lệ) trong Excel
second_title: API xử lý Excel Aspose.Cells .NET
description: Tìm hiểu cách định vị hình ảnh theo tỷ lệ trong Excel bằng Aspose.Cells cho .NET. Làm cho bảng tính của bạn hấp dẫn hơn về mặt thị giác.
weight: 14
url: /vi/net/excel-ole-picture-objects/position-picture-proportional-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vị trí hình ảnh (Tỷ lệ) trong Excel

## Giới thiệu
Bạn có thấy chán những hình ảnh pixel không bao giờ vừa vặn trong bảng tính Excel của mình không? Hãy tưởng tượng: bạn có một logo đẹp cần được hiển thị nổi bật trong bảng tính Excel của mình, nhưng cuối cùng nó lại bị đè bẹp, kéo giãn hoặc đặt không đúng vị trí. Không ai muốn điều đó! Vâng, hãy giữ nguyên chỗ ngồi của bạn vì hôm nay bạn sẽ học cách định vị hình ảnh theo tỷ lệ trong Excel bằng thư viện Aspose.Cells dành cho .NET. Thư viện mạnh mẽ này giúp bạn dễ dàng thao tác với các tệp Excel, cho dù là để báo cáo, phân tích dữ liệu hay chỉ để làm đẹp cho bài thuyết trình của bạn. Hãy cùng tìm hiểu sâu hơn về cách căn chỉnh hình ảnh của bạn một cách hoàn hảo!
## Điều kiện tiên quyết
Trước khi đi sâu vào mã hóa thực tế, có một số thứ bạn cần thiết lập trên máy của mình:
1. Visual Studio: Hãy đảm bảo bạn đã cài đặt Visual Studio vì nó sẽ cung cấp môi trường thuận tiện cho dự án .NET của bạn.
2.  Thư viện Aspose.Cells: Bạn sẽ cần thư viện Aspose.Cells. Bạn có thể dùng thử miễn phí hoặc mua từ[Trang web Aspose](https://purchase.aspose.com/buy).
3. Kiến thức cơ bản về C#: Một chút quen thuộc với lập trình C# sẽ giúp bạn hiểu rõ hơn các ví dụ mà chúng ta sẽ thảo luận.
4. Tệp hình ảnh: Chuẩn bị sẵn một hình ảnh (như logo của bạn) mà bạn muốn chèn vào bảng tính Excel.
Bây giờ bạn đã có mọi thứ cần thiết, chúng ta hãy bắt đầu viết mã nhé!
## Nhập gói
Để bắt đầu sử dụng Aspose.Cells trong dự án của bạn, bạn cần nhập các không gian tên cụ thể. Sau đây là cách thực hiện:
### Tạo một dự án mới
Trong Visual Studio, tạo một dự án mới:
- Mở Visual Studio.
- Nhấp vào "Tạo dự án mới".
- Chọn "Class Library (.NET Framework)" hoặc "Console Application", tùy theo sở thích của bạn.
### Cài đặt Aspose.Cells
Bạn có thể thêm gói Aspose.Cells vào dự án của mình thông qua NuGet. Đây là cách thực hiện:
- Nhấp chuột phải vào dự án của bạn trong Solution Explorer.
- Chọn "Quản lý gói NuGet".
- Tìm kiếm "Aspose.Cells" và nhấp vào "Cài đặt".
### Thêm Sử dụng Chỉ thị
Ở đầu tệp mã của bạn, hãy bao gồm các chỉ thị sau:
```csharp
using System.IO;
using Aspose.Cells;
```
Các chỉ thị này sẽ cung cấp cho bạn quyền truy cập vào các lớp bạn cần để thao tác với các tệp Excel của mình.
Bây giờ, chúng ta hãy chia nhỏ thành các bước chi tiết để định vị hình ảnh theo tỷ lệ thành công trong Excel.
## Bước 1: Thiết lập thư mục của bạn
Trước tiên, hãy đảm bảo rằng bạn có một thư mục được chỉ định cho các tài liệu của mình. Sau đây là cách tạo thư mục nếu nó không tồn tại:
```csharp
string dataDir = "Your Document Directory";
// Tạo thư mục nếu thư mục đó chưa có.
bool isExists = System.IO.Directory.Exists(dataDir);
if (!isExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
 Đoạn mã này tạo một thư mục mới (nếu nó không tồn tại) để lưu trữ các tệp Excel của bạn. Chỉ cần thay thế`"Your Document Directory"` với đường dẫn thực tế mà bạn muốn lưu tập tin của mình.
## Bước 2: Khởi tạo một Workbook
Tiếp theo, chúng ta hãy tạo một bảng tính mới:
```csharp
Workbook workbook = new Workbook();
```
Dòng này khởi tạo một đối tượng sổ làm việc mới, cung cấp cho bạn một khung làm việc trống để làm việc.
## Bước 3: Thêm một bảng tính mới
Bây giờ chúng ta đã thiết lập xong bảng tính, hãy thêm một bảng tính mới vào đó:
```csharp
int sheetIndex = workbook.Worksheets.Add();
```
Thao tác này sẽ thêm một bảng tính mới và trả về chỉ mục của bảng tính đó, mà chúng ta có thể sử dụng để thao tác sau.
## Bước 4: Truy cập vào Bảng tính mới
Để thao tác trên bảng tính mới được thêm vào, bạn cần truy cập vào bảng tính đó:
```csharp
Worksheet worksheet = workbook.Worksheets[sheetIndex];
```
 Hiện nay,`worksheet` sẽ cho phép chúng ta thêm nội dung và hình ảnh vào trang tính cụ thể đó.
## Bước 5: Chèn hình ảnh
Bây giờ đến phần thú vị! Hãy thêm hình ảnh đẹp của bạn. Thay thế`"logo.jpg"` với tên tệp hình ảnh của bạn:
```csharp
int pictureIndex = worksheet.Pictures.Add(5, 5, dataDir + "logo.jpg");
```
 Dòng này thêm hình ảnh vào ô F6 (vì các hàng và cột được lập chỉ mục bằng 0,`5` đề cập đến ô thứ sáu).
## Bước 6: Truy cập vào hình ảnh đã thêm
Sau khi chèn hình ảnh, bạn có thể truy cập vào hình ảnh như sau:
```csharp
Aspose.Cells.Drawing.Picture picture = worksheet.Pictures[pictureIndex];
```
Tính năng này cho phép bạn thay đổi các thuộc tính của hình ảnh.
## Bước 7: Đặt hình ảnh theo tỷ lệ
Bây giờ, chúng ta hãy định vị hình ảnh theo tỷ lệ:
```csharp
picture.UpperDeltaX = 200;
picture.UpperDeltaY = 200;
```
 Đây,`UpperDeltaX` Và`UpperDeltaY` điều chỉnh vị trí của hình ảnh so với kích thước của ô. Bạn có thể điều chỉnh các giá trị này để có được hình ảnh vừa ý.
## Bước 8: Lưu thay đổi của bạn
Cuối cùng, hãy lưu sổ làm việc của bạn để giữ nguyên mọi thay đổi:
```csharp
workbook.Save(dataDir + "book1.out.xls");
```
 Dòng này lưu sổ làm việc của bạn dưới dạng`book1.out.xls` trong thư mục được chỉ định.
## Phần kết luận
Và bạn đã có nó! Bạn vừa học cách định vị hình ảnh theo tỷ lệ trong Excel bằng Aspose.Cells cho .NET. Không chỉ là chèn hình ảnh; mà là làm cho chúng trông hoàn hảo trong bảng tính của bạn. Chỉ cần nhớ rằng: một hình ảnh được đặt đúng chỗ có thể nâng cao đáng kể cách trình bày dữ liệu của bạn.
Hãy vui vẻ thử nghiệm với các hình ảnh và vị trí khác nhau, và đừng ngần ngại khám phá sâu hơn các tính năng phong phú mà Aspose.Cells cung cấp. Các trang tính Excel của bạn sắp được thay đổi hoàn toàn!
## Câu hỏi thường gặp
### Aspose.Cells là gì?
Aspose.Cells là một thư viện mạnh mẽ dành cho .NET cho phép người dùng tạo, thao tác và chuyển đổi các tệp Excel mà không cần cài đặt Microsoft Excel.
### Tôi có thể sử dụng Aspose.Cells miễn phí không?
 Có, Aspose.Cells cung cấp bản dùng thử miễn phí, bạn có thể tải xuống[đây](https://releases.aspose.com/).
### Tôi có thể tìm tài liệu ở đâu?
 Bạn có thể truy cập toàn diện[tài liệu](https://reference.aspose.com/cells/net/) dành cho Aspose.Cells.
### Aspose.Cells có hỗ trợ tất cả các định dạng hình ảnh không?
Aspose.Cells hỗ trợ nhiều định dạng khác nhau bao gồm JPEG, PNG, BMP, GIF và TIFF.
### Tôi có thể nhận được hỗ trợ cho Aspose.Cells như thế nào?
 Nếu có bất kỳ thắc mắc nào, vui lòng truy cập[diễn đàn hỗ trợ](https://forum.aspose.com/c/cells/9)nơi bạn có thể đặt câu hỏi.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
