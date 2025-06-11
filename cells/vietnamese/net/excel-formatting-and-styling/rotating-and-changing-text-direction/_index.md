---
"description": "Chuyển đổi hướng văn bản trong Excel bằng Aspose.Cells cho .NET. Làm theo hướng dẫn từng bước của chúng tôi để xoay và điều chỉnh văn bản dễ dàng."
"linktitle": "Xoay và thay đổi hướng văn bản trong Excel"
"second_title": "API xử lý Excel Aspose.Cells .NET"
"title": "Xoay và thay đổi hướng văn bản trong Excel"
"url": "/vi/net/excel-formatting-and-styling/rotating-and-changing-text-direction/"
"weight": 22
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Xoay và thay đổi hướng văn bản trong Excel

## Giới thiệu
Khi làm việc với các tệp Excel theo chương trình, chúng ta thường phải đối mặt với thách thức là hiển thị dữ liệu theo định dạng mong muốn. Bạn đã bao giờ muốn thay đổi hướng văn bản trong ô Excel chưa? Có thể bạn cần văn bản đọc từ phải sang trái, đặc biệt là nếu bạn đang làm việc với các ngôn ngữ như tiếng Ả Rập hoặc tiếng Do Thái. Hoặc có thể bạn chỉ đang tìm cách tăng cường sức hấp dẫn trực quan cho bảng tính của mình. Dù lý do của bạn là gì, Aspose.Cells for .NET cung cấp giải pháp đơn giản để thao tác hướng văn bản trong các tệp Excel. Trong hướng dẫn này, chúng tôi sẽ chia nhỏ các bước cần thiết để xoay và thay đổi hướng văn bản trong Excel bằng Aspose.Cells.
## Điều kiện tiên quyết
Trước khi đi sâu vào phần mã hóa, hãy đảm bảo bạn đã chuẩn bị một số thứ:
1. Visual Studio: Đảm bảo rằng bạn đã cài đặt Visual Studio trên máy tính của mình. Thư viện Aspose.Cells hoạt động tốt với nó.
2. Thư viện Aspose.Cells: Bạn sẽ cần thư viện Aspose.Cells cho .NET. Bạn có thể tải xuống từ [địa điểm](https://releases.aspose.com/cells/net/).
3. Kiến thức cơ bản về C#: Sự quen thuộc với lập trình C# sẽ giúp bạn dễ dàng theo dõi hướng dẫn hơn.
4. .NET Framework: Đảm bảo dự án của bạn nhắm mục tiêu đến .NET Framework vì Aspose.Cells được thiết kế để hoạt động trong môi trường đó.
Khi bạn đã chuẩn bị đầy đủ mọi điều kiện tiên quyết, bạn đã sẵn sàng để bắt đầu!
## Nhập gói
Bây giờ, hãy chuẩn bị dự án của chúng ta bằng cách nhập các gói cần thiết. Sau đây là cách bạn có thể thực hiện:
### Tạo một dự án mới
- Mở Visual Studio và tạo một dự án mới.
- Chọn Ứng dụng bảng điều khiển từ các mẫu, đặt tên phù hợp như "ExcelTextDirectionDemo".
### Thêm thư viện Aspose.Cells
- Nhấp chuột phải vào dự án trong Solution Explorer và chọn Manage NuGet Packages.
- Tìm Aspose.Cells và cài đặt nó.
### Nhập các không gian tên cần thiết
Bây giờ là lúc đưa vào các không gian tên cần thiết. Ở đầu trang của bạn `Program.cs` tập tin, bao gồm những nội dung sau:
```csharp
using System.IO;
using Aspose.Cells;
```
Với điều đó, bạn đã sẵn sàng để bắt đầu sửa đổi các tệp Excel! Bây giờ, chúng ta hãy bắt đầu mã hóa thực tế.
## Bước 1: Thiết lập thư mục tài liệu của bạn
Để đảm bảo chúng ta lưu tệp Excel ở đúng nơi, chúng ta cần xác định một thư mục. Sau đây là cách thực hiện:
```csharp
// Đường dẫn đến thư mục tài liệu.
string dataDir = "Your Document Directory"; // Điều chỉnh đường dẫn thư mục của bạn
// Tạo thư mục nếu thư mục đó chưa có.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```

Mã này thiết lập một thư mục để lưu tệp Excel. Nó kiểm tra xem thư mục có tồn tại không và tạo thư mục nếu không. Đảm bảo thay thế `"Your Document Directory"` với một đường dẫn hợp lệ.
## Bước 2: Khởi tạo một đối tượng Workbook
Tiếp theo, chúng ta hãy tạo một bảng tính Excel mới. Đây là nơi chúng ta sẽ thao tác với các ô của mình.
```csharp
// Khởi tạo một đối tượng Workbook
Workbook workbook = new Workbook();
```

Bằng cách tạo ra một `Workbook` đối tượng, về cơ bản bạn đang bắt đầu với một tệp Excel mới, trống mà bạn có thể sửa đổi.
## Bước 3: Lấy tham chiếu của bảng tính
Bây giờ, hãy truy cập vào bảng tính mà bạn muốn thực hiện thay đổi.
```csharp
// Lấy tham chiếu của bảng tính
Worksheet worksheet = workbook.Worksheets[0];
```

Các `Worksheet` đối tượng tham chiếu đến trang tính đầu tiên trong sổ làm việc của bạn. Bạn có thể truy cập các trang tính khác bằng cách thay đổi chỉ mục.
## Bước 4: Truy cập vào một ô cụ thể
Hãy tập trung vào một ô cụ thể, trong trường hợp này là "A1". 
```csharp
// Truy cập ô "A1" từ bảng tính
Aspose.Cells.Cell cell = worksheet.Cells["A1"];
```

Dòng mã này sẽ truy cập vào ô "A1", chúng ta sẽ sớm sửa đổi ô này.
## Bước 5: Thêm giá trị vào ô
Đã đến lúc đưa dữ liệu vào ô của chúng ta.
```csharp
// Thêm một số giá trị vào ô "A1"
cell.PutValue("Visit Aspose!");
```

Ở đây, chúng ta chỉ cần thêm văn bản "Visit Aspose!" vào ô "A1". Bạn có thể thay đổi thành bất kỳ nội dung nào bạn thích.
## Bước 6: Thiết lập kiểu văn bản
Bây giờ đến phần chúng ta thay đổi hướng văn bản. 
```csharp
// Thiết lập căn chỉnh theo chiều ngang của văn bản trong ô "A1"
Style style = cell.GetStyle();
```

Thao tác này khôi phục lại kiểu hiện tại của tế bào, mở đường cho việc sửa đổi.
## Bước 7: Thay đổi hướng văn bản 
Đây chính là nơi phép thuật xảy ra! Bạn có thể thay đổi hướng văn bản như thế này:
```csharp
// Thiết lập hướng văn bản từ phải sang trái
style.TextDirection = TextDirectionType.RightToLeft;
```

Dòng này thiết lập hướng văn bản từ phải sang trái, điều này rất cần thiết cho các ngôn ngữ như tiếng Ả Rập hoặc tiếng Do Thái. 
## Bước 8: Áp dụng Kiểu cho Ô
Sau khi thay đổi kiểu hướng văn bản, hãy áp dụng những thay đổi sau vào ô:
```csharp
cell.SetStyle(style);
```

Bạn áp dụng lại kiểu đã sửa đổi vào ô, đảm bảo nó phản ánh hướng văn bản mới.
## Bước 9: Lưu tệp Excel
Cuối cùng, hãy lưu những thay đổi vào một tệp Excel mới.
```csharp
// Lưu tệp Excel
workbook.Save(dataDir + "book1.out.xls", SaveFormat.Excel97To2003);
```

Mã này lưu sổ làm việc với tên tệp được chỉ định trong thư mục được xác định. Định dạng được chỉ định là Excel 97-2003.
## Phần kết luận
Và thế là xong! Bạn đã học thành công cách xoay và thay đổi hướng văn bản trong ô Excel bằng Aspose.Cells cho .NET. Thật tuyệt vời khi chỉ cần một vài dòng mã có thể thay đổi hoàn toàn bố cục và khả năng truy cập ngôn ngữ của bảng tính của bạn phải không? Khả năng thao tác các tệp Excel theo chương trình mở ra một thế giới khả năng, từ tự động hóa báo cáo đến cải thiện trình bày dữ liệu.
## Câu hỏi thường gặp
### Tôi có thể thay đổi hướng văn bản cho nhiều ô không?  
Có, bạn có thể lặp qua một loạt ô và áp dụng những thay đổi tương tự.
### Aspose.Cells có miễn phí sử dụng không?  
Aspose.Cells cung cấp bản dùng thử miễn phí, nhưng cần phải có giấy phép để tiếp tục sử dụng.
### Tôi có thể lưu ở những định dạng nào khác?  
Aspose.Cells hỗ trợ nhiều định dạng như XLSX, CSV và PDF.
### Tôi có cần cài đặt gì khác ngoài Visual Studio không?  
Chỉ cần thêm thư viện Aspose.Cells vào dự án của bạn.
### Tôi có thể tìm thêm thông tin về Aspose.Cells ở đâu?  
Bạn có thể kiểm tra [tài liệu](https://reference.aspose.com/cells/net/) để có hướng dẫn toàn diện và tài liệu tham khảo API.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}