---
"date": "2025-04-05"
"description": "Tìm hiểu cách chuyển đổi tệp Excel sang định dạng PNG, TIFF và PDF khi sử dụng phông chữ tùy chỉnh với Aspose.Cells cho .NET. Đảm bảo kiểu chữ nhất quán trong tất cả các lần chuyển đổi tài liệu."
"title": "Kết xuất Excel thành PNG, TIFF, PDF với Phông chữ tùy chỉnh trong .NET bằng Aspose.Cells"
"url": "/vi/net/workbook-operations/render-excel-custom-fonts-aspose-net/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# Kết xuất tệp Excel thành PNG, TIFF và PDF với phông chữ tùy chỉnh bằng Aspose.Cells cho .NET

## Giới thiệu

Duy trì tính toàn vẹn của phông chữ trong quá trình chuyển đổi tệp Excel thành hình ảnh hoặc PDF là rất quan trọng đối với tính nhất quán của thương hiệu. Aspose.Cells for .NET cung cấp giải pháp mạnh mẽ bằng cách cho phép bạn chỉ định phông chữ mặc định tùy chỉnh trong quá trình chuyển đổi tài liệu của mình.

Trong hướng dẫn này, chúng tôi sẽ hướng dẫn bạn cách kết xuất các tệp Excel thành định dạng PNG, TIFF và PDF bằng Aspose.Cells cho .NET với phông chữ mặc định tùy chỉnh được chỉ định. Điều này lý tưởng nếu bạn:
- Hướng tới kiểu chữ thống nhất trong các tài liệu được kết xuất.
- Cần tùy chỉnh cài đặt phông chữ trong quá trình chuyển đổi.
- Bạn muốn khám phá các tùy chọn cấu hình trong Aspose.Cells cho .NET.

Hãy thiết lập môi trường của bạn và triển khai các tính năng này một cách liền mạch.

### Điều kiện tiên quyết

Trước khi bắt đầu, hãy đảm bảo bạn có những điều sau:
- **Môi trường .NET**: Cài đặt trên máy của bạn (tốt nhất là .NET Core hoặc .NET Framework).
- **Aspose.Cells cho thư viện .NET**: Đã cài đặt trong dự án của bạn.
- **Tệp Excel**: Một bảng tính Excel có dữ liệu cần chuyển đổi.

### Thiết lập Aspose.Cells cho .NET

Để bắt đầu, hãy thêm thư viện Aspose.Cells vào dự án của bạn:

**Sử dụng .NET CLI:**
```bash
dotnet add package Aspose.Cells
```

**Sử dụng Trình quản lý gói:**
```powershell
PM> NuGet\Install-Package Aspose.Cells
```

Nhận giấy phép để có quyền truy cập đầy đủ tính năng:
- **Dùng thử miễn phí**: Thăm nom [Dùng thử miễn phí Aspose](https://releases.aspose.com/cells/net/) để truy cập ban đầu.
- **Giấy phép tạm thời**: Lấy nó từ [Giấy phép tạm thời Aspose](https://purchase.aspose.com/temporary-license/).
- **Mua**: Để có giấy phép vĩnh viễn, hãy đến [Mua Aspose](https://purchase.aspose.com/buy).

Sau khi có được giấy phép, hãy khởi tạo Aspose.Cells trong ứng dụng của bạn:
```csharp
// Thiết lập giấy phép cho Aspose.Cells.
License license = new License();
license.SetLicense("path_to_your_license_file");
```

## Hướng dẫn thực hiện

### Hiển thị sang PNG với Phông chữ mặc định tùy chỉnh

Việc kết xuất bảng tính Excel thành PNG trong khi thiết lập phông chữ mặc định tùy chỉnh đảm bảo tính nhất quán về mặt hình ảnh. Sau đây là cách thực hiện:

#### Bước 1: Cấu hình Tùy chọn hình ảnh

Cấu hình tùy chọn kết xuất cho hình ảnh đầu ra của bạn.
```csharp
using Aspose.Cells;
using Aspose.Cells.Rendering;

// Chỉ định thư mục.
string SourceDir = @"YOUR_SOURCE_DIRECTORY";
string outputDir = @"YOUR_OUTPUT_DIRECTORY";

// Mở một tệp Excel.
Workbook workbook = new Workbook(SourceDir + "sampleSetDefaultFontPropertyOfPdfSaveOptionsAndImageOrPrintOptions.xlsx");

// Thiết lập tùy chọn hiển thị hình ảnh.
ImageOrPrintOptions imgOpt = new ImageOrPrintOptions();
imgOpt.ImageType = Drawing.ImageType.Png;
imgOpt.CheckWorkbookDefaultFont = false; // Sử dụng phông chữ tùy chỉnh cho các phông chữ bị thiếu trong sổ làm việc.
imgOpt.DefaultFont = "Times New Roman";
```

#### Bước 2: Kết xuất và Lưu

Kết xuất bảng tính của bạn thành tệp hình ảnh bằng cách sử dụng các cài đặt này.
```csharp
// Kết xuất bảng tính đầu tiên thành hình ảnh PNG.
SheetRender sr = new SheetRender(workbook.Worksheets[0], imgOpt);
sr.ToImage(0, outputDir + "out1_imagePNG.png");
```

### Hiển thị sang TIFF với Phông chữ mặc định tùy chỉnh

Định dạng TIFF lý tưởng cho hình ảnh chất lượng cao. Sau đây là cách bạn có thể hiển thị toàn bộ sổ làm việc dưới dạng tệp TIFF:

#### Bước 3: Thiết lập tùy chọn hình ảnh cho TIFF

Cấu hình tùy chọn kết xuất dành riêng cho đầu ra TIFF.
```csharp
// Sử dụng lại các thư mục đã xác định trước đó và mở tệp Excel.
Workbook workbook = new Workbook(SourceDir + "sampleSetDefaultFontPropertyOfPdfSaveOptionsAndImageOrPrintOptions.xlsx");

// Cấu hình tùy chọn hiển thị hình ảnh cho TIFF.
imgOpt.ImageType = Drawing.ImageType.Tiff;
```

#### Bước 4: Kết xuất toàn bộ bảng tính thành TIFF

Chuyển đổi toàn bộ bảng tính thành một tệp TIFF duy nhất.
```csharp
// Hiển thị bảng tính dưới dạng hình ảnh TIFF.
WorkbookRender wr = new WorkbookRender(workbook, imgOpt);
wr.ToImage(outputDir + "out1_imageTIFF.tiff");
```

### Kết xuất sang PDF với Phông chữ mặc định tùy chỉnh

Việc lưu bảng tính Excel dưới dạng PDF trong khi vẫn đảm bảo tính nhất quán của phông chữ là rất quan trọng đối với tài liệu chuyên nghiệp.

#### Bước 5: Cấu hình tùy chọn lưu PDF

Thiết lập các tùy chọn cần thiết để lưu tệp của bạn dưới dạng PDF.
```csharp
using Aspose.Cells;

// Mở lại sổ làm việc.
Workbook workbook = new Workbook(SourceDir + "sampleSetDefaultFontPropertyOfPdfSaveOptionsAndImageOrPrintOptions.xlsx");

// Thiết lập tùy chọn lưu PDF.
PdfSaveOptions saveOptions = new PdfSaveOptions();
saveOptions.DefaultFont = "Times New Roman";
saveOptions.CheckWorkbookDefaultFont = false; // Sử dụng phông chữ tùy chỉnh cho các phông chữ bị thiếu trong sổ làm việc.
```

#### Bước 6: Lưu dưới dạng PDF

Xuất bảng tính của bạn sang tài liệu PDF.
```csharp
// Lưu bảng tính dưới dạng tệp PDF.
workbook.Save(outputDir + "out1_pdf.pdf", saveOptions);
```

## Ứng dụng thực tế

- **Báo cáo kinh doanh**: Đảm bảo tính nhất quán về thương hiệu trong tất cả các báo cáo được xuất ra bằng cách sử dụng phông chữ tùy chỉnh.
- **Lưu trữ tài liệu**: Chuyển đổi các tệp Excel cũ sang PDF để dễ dàng chia sẻ và lưu trữ với kiểu chữ thống nhất.
- **Thiết kế đồ họa**: Tạo hình ảnh TIFF có độ phân giải cao từ dữ liệu Excel để trình bày hoặc thiết kế dự án.

Việc tích hợp với các hệ thống khác, chẳng hạn như nền tảng CRM hoặc giải pháp quản lý tài liệu, có thể cải thiện hơn nữa các trường hợp sử dụng này bằng cách tự động xuất dữ liệu dựa trên các sự kiện hoặc tác nhân kích hoạt cụ thể.

## Cân nhắc về hiệu suất

Việc tối ưu hóa quy trình kết xuất của bạn là rất quan trọng:
- **Quản lý bộ nhớ**: Xử lý `Workbook`, `SheetRender`, Và `WorkbookRender` các đối tượng kịp thời để giải phóng tài nguyên.
- **Xử lý hàng loạt**Nếu xử lý nhiều tệp, hãy triển khai xử lý hàng loạt để xử lý hiệu quả.
- **Hoạt động không đồng bộ**:Sử dụng các phương pháp không đồng bộ khi có thể để cải thiện khả năng phản hồi trong các ứng dụng.

## Phần kết luận

Bây giờ bạn đã thành thạo việc kết xuất sổ làm việc Excel thành các định dạng PNG, TIFF và PDF trong khi thiết lập phông chữ mặc định tùy chỉnh bằng Aspose.Cells cho .NET. Khả năng này đảm bảo tài liệu của bạn duy trì tính toàn vẹn trực quan trên nhiều nền tảng và mục đích sử dụng khác nhau.

Khám phá các tính năng bổ sung do Aspose.Cells cung cấp để nâng cao hơn nữa khả năng xử lý tài liệu. Để biết thêm thông tin hoặc trợ giúp, hãy truy cập [Diễn đàn Aspose](https://forum.aspose.com/c/cells/9).

## Phần Câu hỏi thường gặp

**1. Aspose.Cells dành cho .NET là gì?**
   — Aspose.Cells for .NET là thư viện cung cấp các tính năng mạnh mẽ để quản lý và chuyển đổi các tệp Excel theo chương trình.

**2. Tôi có thể sử dụng Aspose.Cells trong ứng dụng web không?**
   — Có, Aspose.Cells có thể được tích hợp vào ASP.NET hoặc bất kỳ ứng dụng web nào khác dựa trên .NET.

**3. Tôi phải xử lý thế nào khi thiếu phông chữ trong quá trình kết xuất?**
   — Bằng cách thiết lập `CheckWorkbookDefaultFont` để sai và chỉ định một `DefaultFont`, bạn đảm bảo rằng toàn bộ văn bản đều sử dụng phông chữ bạn chọn, ngay cả khi không có phông chữ gốc.

**4. Có hỗ trợ các định dạng khác ngoài PNG, TIFF và PDF không?**
   — Có, Aspose.Cells hỗ trợ nhiều định dạng hình ảnh như JPEG, BMP, v.v. và cung cấp khả năng chuyển đổi tài liệu mở rộng.

**5. Một số biện pháp tốt nhất để sử dụng Aspose.Cells trong các ứng dụng quy mô lớn là gì?**
   — Sử dụng các kỹ thuật quản lý bộ nhớ hiệu quả, xử lý hàng loạt để xử lý nhiều tệp và xem xét các hoạt động không đồng bộ để nâng cao hiệu suất ứng dụng.

## Tài nguyên
- **Tài liệu**: [Tài liệu Aspose.Cells](https://reference.aspose.com/cells/net/)
- **Tải về**: [Aspose.Cells phát hành](https://releases.aspose.com/cells/net/)
- **Mua**: [Mua Aspose.Cells](https://purchase.aspose.com/buy)
- **Dùng thử miễn phí**: [Dùng thử Aspose.Cells miễn phí](https://releases.aspose.com/cells/net/)
- **Giấy phép tạm thời**: [Xin giấy phép tạm thời](https://purchase.aspose.com/temporary-license/) 


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}