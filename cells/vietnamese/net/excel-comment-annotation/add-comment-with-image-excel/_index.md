---
title: Thêm bình luận bằng hình ảnh trong Excel
linktitle: Thêm bình luận bằng hình ảnh trong Excel
second_title: API xử lý Excel Aspose.Cells .NET
description: Tìm hiểu cách thêm chú thích bằng hình ảnh trong Excel bằng Aspose.Cells cho .NET. Cải thiện bảng tính của bạn bằng chú thích được cá nhân hóa.
weight: 10
url: /vi/net/excel-comment-annotation/add-comment-with-image-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Thêm bình luận bằng hình ảnh trong Excel

## Giới thiệu
Excel là một công cụ mạnh mẽ để quản lý và phân tích dữ liệu, nhưng đôi khi bạn cần thêm nét cá nhân vào bảng tính của mình, đúng không? Có thể bạn muốn chú thích dữ liệu, cung cấp phản hồi hoặc thậm chí thêm một chút phong cách bằng hình ảnh. Đó là lúc các bình luận trở nên hữu ích! Trong hướng dẫn này, chúng ta sẽ khám phá cách thêm bình luận bằng hình ảnh trong Excel bằng thư viện Aspose.Cells cho .NET. Cách tiếp cận này có thể đặc biệt hữu ích để tạo các bảng tính tương tác và hấp dẫn hơn về mặt hình ảnh.
## Điều kiện tiên quyết
Trước khi đi sâu vào cách thêm chú thích bằng hình ảnh trong Excel, hãy đảm bảo rằng bạn có mọi thứ cần thiết để bắt đầu:
1. Visual Studio: Đảm bảo bạn đã cài đặt Visual Studio trên máy tính của mình. Đây là nơi bạn sẽ viết và thực thi mã của mình.
2.  Aspose.Cells cho .NET: Bạn cần có thư viện Aspose.Cells. Nếu bạn chưa cài đặt, bạn có thể tải xuống từ[đây](https://releases.aspose.com/cells/net/).
3. Kiến thức cơ bản về C#: Sự quen thuộc với lập trình C# sẽ giúp bạn hiểu các đoạn mã tốt hơn.
4. Tệp hình ảnh: Chuẩn bị sẵn tệp hình ảnh (như logo) mà bạn muốn nhúng vào bình luận Excel của mình. Đối với hướng dẫn này, chúng tôi sẽ giả sử bạn có tệp có tên`logo.jpg`.
5. .NET Framework: Đảm bảo bạn đã cài đặt .NET Framework vì Aspose.Cells yêu cầu .NET Framework để hoạt động bình thường.
Bây giờ chúng ta đã hoàn thành các điều kiện tiên quyết, hãy chuyển sang phần viết mã thực tế!
## Nhập gói
Trước tiên, chúng ta cần nhập các gói cần thiết. Trong dự án C# của bạn, hãy đảm bảo thêm tham chiếu đến thư viện Aspose.Cells. Bạn có thể thực hiện việc này bằng cách sử dụng NuGet Package Manager trong Visual Studio. Sau đây là cách thực hiện:
1. Mở Visual Studio.
2. Tạo một dự án mới hoặc mở một dự án hiện có.
3. Nhấp chuột phải vào dự án của bạn trong Solution Explorer.
4. Chọn Quản lý gói NuGet.
5. Tìm Aspose.Cells và cài đặt nó.

```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
```

Sau khi đã cài đặt thư viện, bạn có thể bắt đầu viết mã. Sau đây là cách thực hiện từng bước.
## Bước 1: Thiết lập thư mục tài liệu của bạn
Để bắt đầu, chúng ta cần thiết lập một thư mục nơi chúng ta có thể lưu các tệp Excel của mình. Đây là một bước quan trọng vì chúng ta muốn giữ cho công việc của mình được tổ chức.
```csharp
// Đường dẫn đến thư mục tài liệu.
string dataDir = "Your Document Directory";
// Tạo thư mục nếu thư mục đó chưa có.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
- dataDir: Biến này giữ đường dẫn đến thư mục tài liệu của bạn. Thay thế`"Your Document Directory"` bằng đường dẫn thực tế mà bạn muốn lưu tệp Excel của mình.
- Directory.Exists: Kiểm tra xem thư mục đã tồn tại hay chưa.
- Directory.CreateDirectory: Nếu thư mục không tồn tại, lệnh này sẽ tạo thư mục.
## Bước 2: Khởi tạo một Workbook
 Tiếp theo, chúng ta cần tạo một phiên bản của`Workbook` lớp. Lớp này biểu diễn một bảng tính Excel trong bộ nhớ.
```csharp
//Khởi tạo một Workbook
Workbook workbook = new Workbook();
```
- Workbook: Đây là lớp chính trong Aspose.Cells cho phép bạn tạo và thao tác các tệp Excel. Bằng cách khởi tạo nó, về cơ bản bạn đang tạo một workbook Excel mới.
## Bước 3: Nhận Bộ sưu tập Bình luận
Bây giờ chúng ta đã có bảng tính, hãy truy cập vào bộ sưu tập chú thích của bảng tính đầu tiên.
```csharp
// Nhận tham chiếu của bộ sưu tập bình luận với trang tính đầu tiên
CommentCollection comments = workbook.Worksheets[0].Comments;
```
- Phiếu bài tập[ 0]: Điều này truy cập vào trang tính đầu tiên trong sổ làm việc. Hãy nhớ rằng, chỉ mục dựa trên số không, vì vậy`[0]` đề cập đến tờ đầu tiên.
- Bình luận: Thuộc tính này cho phép chúng ta truy cập vào bộ sưu tập bình luận trên bảng tính đó.
## Bước 4: Thêm chú thích vào ô
Hãy thêm chú thích vào một ô cụ thể. Trong trường hợp này, chúng ta sẽ thêm chú thích vào ô A1.
```csharp
// Thêm bình luận vào ô A1
int commentIndex = comments.Add(0, 0);
Comment comment = comments[commentIndex];
comment.Note = "First note.";
comment.Font.Name = "Times New Roman";
```
- comments.Add(0, 0): Phương pháp này thêm một chú thích vào ô A1 (hàng 0, cột 0).
- bình luận.Lưu ý: Ở đây, chúng ta thiết lập văn bản của bình luận.
- comment.Font.Name: Thiết lập phông chữ cho văn bản bình luận.
## Bước 5: Tải hình ảnh vào luồng
 Bây giờ là lúc tải hình ảnh mà chúng ta muốn nhúng vào bình luận của mình. Chúng ta sẽ sử dụng`MemoryStream` để lưu trữ dữ liệu hình ảnh.
```csharp
// Tải một hình ảnh vào luồng
Bitmap bmp = new Bitmap(dataDir + "logo.jpg");
MemoryStream ms = new MemoryStream();
bmp.Save(ms, System.Drawing.Imaging.ImageFormat.Png);
```
- Bitmap: Lớp này được sử dụng để tải tệp hình ảnh. Đảm bảo đường dẫn là chính xác.
- MemoryStream: Đây là luồng mà chúng ta sẽ sử dụng để lưu hình ảnh vào bộ nhớ.
- bmp.Save: Lưu ảnh bitmap vào luồng bộ nhớ theo định dạng PNG.
## Bước 6: Đặt Dữ liệu Hình ảnh vào Hình dạng Bình luận
Bây giờ chúng ta cần thiết lập dữ liệu hình ảnh theo hình dạng liên quan đến bình luận mà chúng ta đã tạo trước đó.
```csharp
// Đặt dữ liệu hình ảnh thành hình dạng liên quan đến bình luận
comment.CommentShape.Fill.ImageData = ms.ToArray();
```
- comment.CommentShape.Fill.ImageData: Thuộc tính này cho phép bạn thiết lập hình ảnh cho hình dạng bình luận. Chúng tôi chuyển đổi`MemoryStream` đến một mảng byte sử dụng`ms.ToArray()`.
## Bước 7: Lưu sổ làm việc
Cuối cùng, hãy lưu bảng tính của chúng ta cùng với bình luận và hình ảnh.
```csharp
// Lưu sổ làm việc
workbook.Save(dataDir + "book1.out.xlsx", Aspose.Cells.SaveFormat.Xlsx);
```
- workbook.Save: Phương pháp này lưu sổ làm việc vào đường dẫn đã chỉ định. Chúng tôi lưu nó dưới dạng tệp XLSX.
## Phần kết luận
Và bạn đã có nó! Bạn đã thêm thành công một bình luận có hình ảnh vào tệp Excel bằng Aspose.Cells cho .NET. Tính năng này có thể làm cho bảng tính của bạn nhiều thông tin hơn và hấp dẫn hơn về mặt hình ảnh. Cho dù bạn đang chú thích dữ liệu, cung cấp phản hồi hay chỉ đơn giản là thêm nét cá nhân, bình luận có hình ảnh có thể nâng cao đáng kể trải nghiệm của người dùng.
## Câu hỏi thường gặp
### Tôi có thể thêm nhiều bình luận vào cùng một ô không?
Không, Excel không cho phép nhiều bình luận trên cùng một ô. Bạn chỉ có thể có một bình luận cho mỗi ô.
### Những định dạng hình ảnh nào được hỗ trợ?
Aspose.Cells hỗ trợ nhiều định dạng hình ảnh, bao gồm PNG, JPEG và BMP.
### Tôi có cần giấy phép để sử dụng Aspose.Cells không?
Aspose.Cells cung cấp bản dùng thử miễn phí, nhưng để có đầy đủ chức năng, bạn sẽ cần phải mua giấy phép.
### Tôi có thể tùy chỉnh giao diện của bình luận không?
Có, bạn có thể tùy chỉnh phông chữ, kích thước và màu sắc của văn bản bình luận và bạn cũng có thể thay đổi hình dạng và kích thước của chính bình luận đó.
### Tôi có thể tìm thêm tài liệu về Aspose.Cells ở đâu?
 Bạn có thể tìm thấy tài liệu toàn diện về Aspose.Cells[đây](https://reference.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
