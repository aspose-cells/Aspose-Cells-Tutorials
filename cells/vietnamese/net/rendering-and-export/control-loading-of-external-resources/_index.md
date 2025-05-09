---
"description": "Khám phá cách kiểm soát tài nguyên bên ngoài khi chuyển đổi Excel sang PDF bằng Aspose.Cells cho .NET với hướng dẫn dễ làm theo của chúng tôi."
"linktitle": "Kiểm soát các tài nguyên bên ngoài trong Excel sang PDF trong Aspose.Cells"
"second_title": "API xử lý Excel Aspose.Cells .NET"
"title": "Kiểm soát các tài nguyên bên ngoài trong Excel sang PDF trong Aspose.Cells"
"url": "/vi/net/rendering-and-export/control-loading-of-external-resources/"
"weight": 12
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Kiểm soát các tài nguyên bên ngoài trong Excel sang PDF trong Aspose.Cells

## Giới thiệu
Trong thời đại kỹ thuật số ngày nay, việc chuyển đổi bảng tính Excel sang tài liệu PDF là một nhiệm vụ phổ biến. Cho dù đó là chuẩn bị báo cáo, dữ liệu tài chính hay tài liệu thuyết trình, bạn đều muốn đảm bảo rằng PDF của mình trông chính xác như bạn mong muốn. Aspose.Cells for .NET là một thư viện mạnh mẽ cho phép bạn kiểm soát quy trình chuyển đổi này đến từng chi tiết nhỏ nhất, đặc biệt là khi xử lý các tài nguyên bên ngoài như hình ảnh đi kèm với tệp Excel của bạn. Trong hướng dẫn này, chúng tôi sẽ đi sâu vào cách kiểm soát các tài nguyên bên ngoài trong quá trình chuyển đổi Excel sang PDF bằng Aspose.Cells. Vì vậy, hãy lấy đồ uống yêu thích của bạn và bắt đầu thôi!
## Điều kiện tiên quyết
Trước khi đi sâu vào chi tiết, hãy đảm bảo bạn có mọi thứ cần thiết để bắt đầu. Sau đây là danh sách kiểm tra nhanh:
1. Visual Studio hoặc bất kỳ IDE nào tương thích với .NET: Bạn sẽ cần một môi trường để viết và kiểm tra mã của mình.
2. Aspose.Cells cho .NET: Nếu bạn chưa cài đặt, hãy truy cập [Tải xuống Aspose](https://releases.aspose.com/cells/net/) trang và tải phiên bản mới nhất.
3. Kiến thức cơ bản về C#: Sự quen thuộc với ngôn ngữ lập trình C# sẽ hữu ích. Nếu bạn không chắc chắn về bất kỳ khái niệm nào, đừng ngần ngại tra cứu chúng.
4. Tệp Excel mẫu: Chuẩn bị tệp Excel với bất kỳ tài nguyên bên ngoài nào bạn muốn chuyển đổi. Bạn có thể sử dụng tệp mẫu được cung cấp "samplePdfSaveOptions_StreamProvider.xlsx".
5. Tệp hình ảnh để kiểm tra: Tệp này sẽ được sử dụng làm tài nguyên bên ngoài trong quá trình chuyển đổi. Tệp hình ảnh "newPdfSaveOptions_StreamProvider.png" là một trình giữ chỗ tốt.
## Nhập gói
Để bắt đầu, bạn sẽ cần nhập các không gian tên cần thiết từ thư viện Aspose.Cells. Điều này rất quan trọng để truy cập các chức năng của nó. Đảm bảo thêm các chỉ thị using sau vào đầu tệp của bạn:
```csharp
using System.IO;
using System.Drawing;
using System.Drawing.Imaging;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using Aspose.Cells.Rendering;
using System;
```
Các gói này sẽ cung cấp tất cả các lớp và phương pháp thiết yếu mà bạn cần để thực hiện nhiệm vụ của mình.
## Bước 1: Tạo lớp nhà cung cấp luồng của bạn
Nhiệm vụ đầu tiên là tạo một lớp nhà cung cấp luồng thực hiện `IStreamProvider` giao diện. Lớp này sẽ cho phép bạn kiểm soát cách tải các tài nguyên bên ngoài.
```csharp
class MyStreamProvider : IStreamProvider
{
    public void CloseStream(StreamProviderOptions options)
    {
        Debug.WriteLine("-----Close Stream-----");
    }
    public void InitStream(StreamProviderOptions options)
    {
        string sourceDir = "Your Document Directory";
        Debug.WriteLine("-----Init Stream-----");
        // Đọc hình ảnh mới trong luồng bộ nhớ và gán nó vào thuộc tính Stream
        byte[] bts = File.ReadAllBytes(sourceDir + "newPdfSaveOptions_StreamProvider.png");
        MemoryStream ms = new MemoryStream(bts);
        options.Stream = ms;
    }
}
```
Trong lớp này:
- CloseStream: Phương thức này sẽ được gọi khi luồng đóng. Hiện tại, chúng ta chỉ viết một thông báo gỡ lỗi để theo dõi.
- InitStream: Đây là nơi phép thuật bắt đầu. Tại đây, bạn sẽ đọc hình ảnh bên ngoài của mình dưới dạng một mảng byte, chuyển đổi nó thành một luồng bộ nhớ và gán nó cho `options.Stream` tài sản.
## Bước 2: Thiết lập thư mục nguồn và đầu ra
Bây giờ nhà cung cấp luồng của bạn đã sẵn sàng, đã đến lúc xác định vị trí tệp Excel và nơi bạn muốn lưu tệp PDF.
```csharp
// Thư mục nguồn
string sourceDir = "Your Document Directory";
// Thư mục đầu ra
string outputDir = "Your Document Directory";
```
Chỉ cần thay thế `"Your Document Directory"` với đường dẫn thực tế trên máy tính nơi lưu trữ các tệp của bạn. Việc sắp xếp các tệp của bạn là điều quan trọng!
## Bước 3: Tải tệp Excel của bạn
Tiếp theo, bạn sẽ tải tệp Excel mà bạn muốn dùng để tạo PDF.
```csharp
// Tải tệp Excel nguồn có chứa hình ảnh bên ngoài
Workbook wb = new Workbook(sourceDir + "samplePdfSaveOptions_StreamProvider.xlsx");
```
Chúng tôi đang sử dụng `Workbook` lớp từ Aspose.Cells, đại diện cho tệp Excel của bạn. Tệp có thể bao gồm nhiều tài nguyên bên ngoài như hình ảnh mà bạn muốn kiểm soát trong quá trình chuyển đổi.
## Bước 4: Thiết lập tùy chọn lưu PDF
Trước khi lưu sổ làm việc dưới dạng PDF, hãy chỉ định cách bạn muốn lưu. Bạn có thể điều chỉnh các tùy chọn này theo yêu cầu của mình.
```csharp
// Chỉ định Tùy chọn Lưu PDF - Nhà cung cấp Luồng
PdfSaveOptions opts = new PdfSaveOptions();
opts.OnePagePerSheet = true; // Lưu mỗi trang tính trên một trang mới
```
Ở đây, chúng ta đang tạo một phiên bản mới của `PdfSaveOptions`cho phép bạn tùy chỉnh cách định dạng PDF của mình. `OnePagePerSheet` Tùy chọn này rất tiện lợi để đảm bảo mỗi trang tính Excel đều có trang riêng trong tệp PDF cuối cùng.
## Bước 5: Chỉ định Nhà cung cấp Luồng của Bạn
Sau khi thiết lập các tùy chọn PDF, bạn cần yêu cầu Aspose sử dụng nhà cung cấp luồng tùy chỉnh của bạn cho các tài nguyên bên ngoài.
```csharp
wb.Settings.StreamProvider = new MyStreamProvider();
```
Dòng này kết nối bạn `Workbook` ví dụ với `MyStreamProvider` lớp bạn đã tạo trước đó. Điều này có nghĩa là bất cứ khi nào gặp phải tài nguyên bên ngoài trong quá trình chuyển đổi, nhà cung cấp của bạn sẽ xử lý chúng theo đúng chỉ định.
## Bước 6: Lưu Workbook dưới dạng PDF
Khi mọi thứ đã hoàn tất, cuối cùng đã đến lúc lưu bảng tính Excel của bạn dưới dạng PDF.
```csharp
// Lưu sổ làm việc vào Pdf
wb.Save(outputDir + "outputPdfSaveOptions_StreamProvider.pdf", opts);
```
Bằng cách gọi `Save` phương pháp trên đối tượng sổ làm việc và truyền vào thư mục đầu ra cùng với các tùy chọn PDF, bạn đang chuyển đổi tệp Excel thành tệp PDF được định dạng đẹp mắt.
## Bước 7: Xác nhận thực hiện thành công
Cuối cùng, thật tuyệt khi xác nhận rằng quá trình của bạn đã thành công!
```csharp
Console.WriteLine("ControlLoadingOfExternalResourcesInExcelToPDF executed successfully.\r\n");
```
In thông báo thành công vào bảng điều khiển giúp bạn luôn cập nhật về trạng thái hoạt động của mình. Một thói quen tốt là đưa những xác nhận nhỏ này vào mã của bạn.
## Phần kết luận
Bạn đã có nó rồi! Bằng cách làm theo các bước đơn giản này, bạn có thể kiểm soát một cách chuyên nghiệp cách xử lý các tài nguyên bên ngoài trong quá trình chuyển đổi Excel sang PDF bằng Aspose.Cells. Điều này có nghĩa là tài liệu của bạn giờ đây có thể bao gồm hình ảnh và các thành phần bên ngoài khác một cách chính xác, đảm bảo sản phẩm cuối cùng được trau chuốt mọi lúc.
## Câu hỏi thường gặp
### Aspose.Cells là gì?  
Aspose.Cells là một thư viện mạnh mẽ dành cho các nhà phát triển .NET, cho phép bạn tạo, chỉnh sửa, chuyển đổi và hiển thị các tệp Excel ở nhiều định dạng khác nhau.
### Làm thế nào để tải xuống Aspose.Cells?  
Bạn có thể tải xuống phiên bản mới nhất của Aspose.Cells từ [Liên kết tải xuống](https://releases.aspose.com/cells/net/).
### Tôi có thể dùng thử Aspose.Cells miễn phí không?  
Có! Bạn có thể dùng thử miễn phí bằng cách truy cập [Trang dùng thử miễn phí](https://releases.aspose.com/).
### Tôi có thể tìm thấy hỗ trợ cho Aspose.Cells ở đâu?  
Đối với bất kỳ thắc mắc nào liên quan đến hỗ trợ, bạn có thể truy cập [Diễn đàn hỗ trợ Aspose](https://forum.aspose.com/c/cells/9).
### Làm thế nào tôi có thể xin được giấy phép tạm thời cho Aspose.Cells?  
Bạn có thể nộp đơn xin giấy phép tạm thời [đây](https://purchase.aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}