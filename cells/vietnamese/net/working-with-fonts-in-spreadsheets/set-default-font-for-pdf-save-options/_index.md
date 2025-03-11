---
title: Đặt Phông chữ Mặc định cho Tùy chọn Lưu PDF
linktitle: Đặt Phông chữ Mặc định cho Tùy chọn Lưu PDF
second_title: API xử lý Excel Aspose.Cells .NET
description: Tìm hiểu cách thiết lập phông chữ mặc định cho tùy chọn lưu PDF bằng Aspose.Cells cho .NET, đảm bảo tài liệu của bạn luôn trông hoàn hảo.
weight: 11
url: /vi/net/working-with-fonts-in-spreadsheets/set-default-font-for-pdf-save-options/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Đặt Phông chữ Mặc định cho Tùy chọn Lưu PDF

## Giới thiệu
Khi nói đến việc tạo báo cáo, hóa đơn hoặc bất kỳ tài liệu nào khác ở định dạng PDF, việc đảm bảo rằng nội dung của bạn trông hoàn hảo là điều tối quan trọng. Phông chữ đóng vai trò quan trọng trong việc duy trì tính hấp dẫn trực quan và khả năng đọc của tài liệu. Tuy nhiên, điều gì sẽ xảy ra khi phông chữ bạn sử dụng trong tệp Excel không khả dụng trên hệ thống nơi bạn tạo PDF? Đó là lúc Aspose.Cells for .NET trở nên hữu ích. Thư viện mạnh mẽ này cho phép bạn đặt phông chữ mặc định cho các tùy chọn lưu PDF của mình, đảm bảo tài liệu của bạn trông chuyên nghiệp và nhất quán, bất kể chúng được mở ở đâu.
## Điều kiện tiên quyết
Trước khi bắt đầu, hãy đảm bảo bạn có những điều sau:
1. Visual Studio: Bạn sẽ cần một môi trường phát triển như Visual Studio để viết và thực thi mã của mình.
2.  Aspose.Cells cho .NET: Bạn có thể tải xuống phiên bản mới nhất từ[liên kết này](https://releases.aspose.com/cells/net/). Ngoài ra, bạn có thể cài đặt nó thông qua NuGet Package Manager trong Visual Studio.
3. Kiến thức cơ bản về C#: Hiểu được những kiến thức cơ bản về C# sẽ giúp bạn theo dõi các ví dụ về mã.
4. Tệp Excel mẫu: Chuẩn bị một tệp Excel mẫu để thử nghiệm. Bạn có thể tạo một tệp với nhiều phông chữ và kiểu khác nhau để xem Aspose.Cells xử lý các phông chữ bị thiếu như thế nào.
## Nhập gói
Trước khi bạn có thể sử dụng Aspose.Cells trong dự án của mình, bạn cần phải nhập các gói cần thiết. Sau đây là cách thực hiện:
1. Mở dự án của bạn: Khởi chạy Visual Studio và mở dự án hiện có hoặc tạo dự án mới.
2. Thêm tham chiếu: Nhấp chuột phải vào dự án của bạn trong Solution Explorer và chọn "Quản lý gói NuGet".
3. Cài đặt Aspose.Cells: Tìm kiếm "Aspose.Cells" và nhấp vào nút "Cài đặt".
4. Thêm bằng cách sử dụng Chỉ thị: Ở đầu tệp C# của bạn, hãy bao gồm các không gian tên sau:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;
```
## Bước 1: Thiết lập thư mục của bạn
Trước khi làm việc với các tệp, điều quan trọng là phải xác định thư mục nguồn và thư mục đầu ra. Điều này sẽ giúp bạn dễ dàng định vị tệp Excel đầu vào và lưu các tệp đầu ra đã tạo.
```csharp
// Thư mục nguồn
string sourceDir = "Your Document Directory";
// Thư mục đầu ra
string outputDir = "Your Document Directory";
```
 Thay thế`"Your Document Directory"` với đường dẫn thực tế tới thư mục của bạn.
## Bước 2: Mở tệp Excel
 Bây giờ chúng ta đã thiết lập xong các thư mục, hãy mở tệp Excel mà bạn muốn làm việc.`Workbook` lớp trong Aspose.Cells được sử dụng để tải tài liệu Excel.
```csharp
// Mở một tập tin Excel
Workbook workbook = new Workbook(sourceDir + "sampleSetDefaultFontPropertyOfPdfSaveOptionsAndImageOrPrintOptions.xlsx");
```
Hãy đảm bảo thay thế tên tệp bằng tên tệp thực tế của bạn.
## Bước 3: Thiết lập tùy chọn kết xuất hình ảnh
Tiếp theo, chúng ta cần cấu hình các tùy chọn kết xuất để chuyển đổi bảng tính Excel của mình sang định dạng hình ảnh. Chúng ta sẽ tạo một phiên bản của`ImageOrPrintOptions`, chỉ định loại hình ảnh và phông chữ mặc định.
```csharp
// Kết xuất sang định dạng tệp PNG
ImageOrPrintOptions imgOpt = new ImageOrPrintOptions();
imgOpt.ImageType = Drawing.ImageType.Png;
imgOpt.CheckWorkbookDefaultFont = false;
imgOpt.DefaultFont = "Times New Roman";
```
 Trong đoạn mã này, chúng tôi thiết lập`CheckWorkbookDefaultFont` tài sản để`false`, nghĩa là nếu thiếu bất kỳ phông chữ nào, phông chữ mặc định đã chỉ định (“Times New Roman”) sẽ được sử dụng thay thế.
## Bước 4: Hiển thị trang tính dưới dạng hình ảnh
 Bây giờ, hãy kết xuất trang tính đầu tiên của sổ làm việc dưới dạng hình ảnh PNG. Chúng ta sẽ sử dụng`SheetRender` lớp để thực hiện điều này.
```csharp
// Hiển thị trang tính đầu tiên thành hình ảnh
SheetRender sr = new SheetRender(workbook.Worksheets[0], imgOpt);
sr.ToImage(0, outputDir + "out1_imagePNG.png");
```
## Bước 5: Thay đổi loại hình ảnh và kết xuất thành TIFF
 Nếu bạn muốn hiển thị cùng một trang tính sang một định dạng hình ảnh khác, như TIFF, bạn chỉ cần thay đổi`ImageType` thuộc tính và lặp lại quá trình kết xuất.
```csharp
// Đặt thành định dạng TIFF
imgOpt.ImageType = Drawing.ImageType.Tiff;
WorkbookRender wr = new WorkbookRender(workbook, imgOpt);
wr.ToImage(outputDir + "out1_imageTIFF.tiff");
```
## Bước 6: Cấu hình tùy chọn lưu PDF
 Tiếp theo, chúng ta hãy thiết lập các tùy chọn lưu PDF. Chúng ta sẽ tạo một phiên bản của`PdfSaveOptions`đặt phông chữ mặc định và chỉ định rằng chúng ta muốn kiểm tra các phông chữ bị thiếu.
```csharp
// Cấu hình tùy chọn lưu PDF
PdfSaveOptions saveOptions = new PdfSaveOptions();
saveOptions.DefaultFont = "Times New Roman";
saveOptions.CheckWorkbookDefaultFont = false;
```
## Bước 7: Lưu Workbook dưới dạng PDF
Sau khi đã thiết lập xong các tùy chọn lưu, đã đến lúc lưu bảng tính Excel của chúng ta dưới dạng tệp PDF. 
```csharp
// Lưu sổ làm việc vào PDF
workbook.Save(outputDir + "out1_pdf.pdf", saveOptions);
```
## Bước 8: Xác nhận thực hiện
Cuối cùng, một cách làm tốt là cho người dùng biết rằng quá trình đã hoàn tất thành công. Bạn có thể thực hiện điều này bằng cách sử dụng một thông báo bảng điều khiển đơn giản.
```csharp
Console.WriteLine("SetDefaultFontPropertyOfPdfSaveOptionsAndImageOrPrintOptions executed successfully.\r\n");
```
## Phần kết luận
Aspose.Cells cung cấp một cách linh hoạt và mạnh mẽ để xử lý các thao tác tệp Excel, giúp các nhà phát triển dễ dàng tạo các tài liệu hấp dẫn về mặt hình ảnh mà vẫn duy trì định dạng của chúng. Cho dù bạn đang làm việc trên các báo cáo, tài liệu tài chính hay bất kỳ hình thức trình bày dữ liệu nào khác, việc kiểm soát việc hiển thị phông chữ có thể cải thiện đáng kể chất lượng đầu ra của bạn.
## Câu hỏi thường gặp
### Aspose.Cells là gì?
Aspose.Cells là một thư viện .NET mạnh mẽ cho phép các nhà phát triển thao tác với các tệp Excel mà không cần cài đặt Microsoft Excel. Nó hỗ trợ nhiều định dạng tệp khác nhau và cung cấp các tính năng phong phú để làm việc với bảng tính.
### Làm thế nào để thiết lập phông chữ mặc định cho các tệp Excel của tôi?
 Bạn có thể thiết lập phông chữ mặc định bằng cách sử dụng`PdfSaveOptions` lớp và chỉ định tên phông chữ mong muốn. Điều này đảm bảo rằng ngay cả khi thiếu phông chữ, tài liệu của bạn sẽ sử dụng phông chữ mặc định mà bạn đã chỉ định.
### Tôi có thể chuyển đổi tệp Excel sang định dạng khác ngoài PDF không?
Chắc chắn rồi! Aspose.Cells cho phép bạn chuyển đổi các tệp Excel sang nhiều định dạng khác nhau, bao gồm hình ảnh (PNG, TIFF), HTML, CSV, v.v.
### Aspose.Cells có miễn phí sử dụng không?
Aspose.Cells là một sản phẩm thương mại, nhưng bạn có thể dùng thử miễn phí với phiên bản dùng thử giới hạn. Để có đầy đủ chức năng, bạn sẽ cần mua giấy phép.
### Tôi có thể tìm thấy hỗ trợ cho Aspose.Cells ở đâu?
 Bạn có thể tìm thấy sự hỗ trợ cho Aspose.Cells bằng cách truy cập[Diễn đàn Aspose](https://forum.aspose.com/c/cells/9), nơi bạn có thể đặt câu hỏi và chia sẻ hiểu biết với những người dùng và nhà phát triển khác.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
