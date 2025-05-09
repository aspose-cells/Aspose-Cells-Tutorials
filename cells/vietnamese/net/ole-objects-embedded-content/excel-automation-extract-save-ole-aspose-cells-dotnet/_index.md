---
"date": "2025-04-05"
"description": "Học cách tự động trích xuất và lưu các đối tượng OLE từ các tệp Excel bằng Aspose.Cells cho .NET, nâng cao quy trình xử lý dữ liệu của bạn."
"title": "Tự động trích xuất và lưu đối tượng Excel OLE bằng Aspose.Cells cho .NET"
"url": "/vi/net/ole-objects-embedded-content/excel-automation-extract-save-ole-aspose-cells-dotnet/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# Tự động trích xuất và lưu đối tượng Excel OLE với Aspose.Cells cho .NET

## Giới thiệu

Bạn có muốn hợp lý hóa quy trình làm việc của mình bằng cách tự động trích xuất các đối tượng nhúng trong tệp Excel của mình không? Cho dù bạn là nhà phát triển hay nhà phân tích dữ liệu, hãy tận dụng **Aspose.Cells cho .NET** có thể giảm đáng kể công sức và lỗi thủ công. Hướng dẫn này sẽ hướng dẫn bạn cách trích xuất và lưu các đối tượng Liên kết và Nhúng đối tượng (OLE) từ sổ làm việc Excel dựa trên định dạng tệp của chúng.

### Những gì bạn sẽ học được:
- Mở và tải bảng tính Excel bằng Aspose.Cells.
- Truy cập bộ sưu tập các đối tượng OLE trong một bảng tính.
- Trích xuất và lưu các đối tượng OLE theo định dạng cụ thể của chúng.

Hãy thiết lập môi trường của bạn và triển khai tính năng hiệu quả này!

## Điều kiện tiên quyết

Trước khi bắt đầu, hãy đảm bảo bạn đã đáp ứng các điều kiện tiên quyết sau:

### Thư viện cần thiết:
- **Aspose.Cells cho .NET** - Cần thiết để xử lý các tệp Excel trong môi trường .NET.

### Thiết lập môi trường:
- Môi trường phát triển như Visual Studio hoặc bất kỳ IDE tương thích nào hỗ trợ C# và .NET.

### Điều kiện tiên quyết về kiến thức:
- Hiểu biết cơ bản về lập trình C#.
- Quen thuộc với .NET framework, đặc biệt là các hoạt động I/O tệp.

## Thiết lập Aspose.Cells cho .NET

Để sử dụng Aspose.Cells cho .NET, bạn cần cài đặt nó vào dự án của mình. Sau đây là cách thực hiện:

### Hướng dẫn cài đặt:

**Sử dụng .NET CLI:**
```bash
dotnet add package Aspose.Cells
```

**Sử dụng Trình quản lý gói:**
```powershell
PM> NuGet\Install-Package Aspose.Cells
```

### Mua giấy phép:
- **Dùng thử miễn phí:** Bắt đầu với bản dùng thử miễn phí 30 ngày để khám phá tất cả các tính năng.
- **Giấy phép tạm thời:** Yêu cầu cấp giấy phép tạm thời để truy cập mở rộng.
- **Mua:** Mua giấy phép đầy đủ nếu công cụ này đáp ứng nhu cầu của bạn.

Sau khi cài đặt, hãy khởi tạo Aspose.Cells trong dự án của bạn như sau:

```csharp
using Aspose.Cells;

// Khởi tạo thư viện
Aspose.Cells.License license = new Aspose.Cells.License();
license.SetLicense("Path to License File");
```

## Hướng dẫn thực hiện

### Tính năng 1: Mở và Tải Workbook

Hãy tải một bảng tính Excel từ một thư mục được chỉ định.

#### Thực hiện từng bước:

**Xác định thư mục nguồn:**
```csharp
string sourceDir = "YOUR_SOURCE_DIRECTORY";
```

**Tạo phiên bản sổ làm việc:**
```csharp
Workbook workbook = new Workbook(sourceDir + "sampleExtractOLEObjects.xlsx");
```
Bước này tải tệp Excel của bạn vào một `Workbook` đối tượng, cho phép bạn thao tác nội dung của nó theo chương trình.

### Tính năng 2: Truy cập OleObject Collection trong Worksheet

Bây giờ, hãy truy cập các đối tượng OLE được nhúng trong trang tính đầu tiên của sổ làm việc.

#### Thực hiện từng bước:

**Truy cập trang tính đầu tiên:**
```csharp
OleObjectCollection oles = workbook.Worksheets[0].OleObjects;
```
Đoạn mã này sẽ lấy tất cả các đối tượng OLE từ bảng tính đã chỉ định để xử lý thêm.

### Tính năng 3: Trích xuất và lưu các đối tượng OLE dựa trên định dạng

Tiếp theo, lặp qua từng đối tượng OLE để trích xuất dữ liệu của đối tượng đó và lưu theo định dạng của đối tượng đó.

#### Thực hiện từng bước:

**Lặp lại qua các đối tượng OLE:**
```csharp
using System.IO;

for (int i = 0; i < oles.Count; i++)
{
    OleObject ole = oles[i];
    byte[] oleData = ole.ObjectData;
    string fileName = outputDir + "outputExtractOLEObjects" + (i+1) + ".";

    switch (ole.FileFormatType)
    {
        case FileFormatType.Doc:
            fileName += "doc";
            break;
        case FileFormatType.Docx:
            fileName += "docx";
            break;
        case FileFormatType.Excel97To2003:
            fileName += "xls";
            break;
        case FileFormatType.Xlsx:
            // Xử lý đặc biệt cho các định dạng XLSX
            using (MemoryStream ms = new MemoryStream())
            {
                ms.Write(ole.ObjectData, 0, ole.ObjectData.Length);
                Workbook oleBook = new Workbook(ms);
                oleBook.Settings.IsHidden = false;

                ms.SetLength(0); // Xóa luồng
                oleBook.Save(ms, SaveFormat.Xlsx);

                ms.Position = 0;
                byte[] bts = new byte[ms.Length];
                ms.Read(bts, 0, (int)ms.Length);
                oleData = bts;
            }
            fileName += "xlsx";
            break;
        case FileFormatType.Ppt:
            fileName += "ppt";
            break;
        case FileFormatType.Pdf:
            fileName += "pdf";
            break;
        case FileFormatType.Unknown:
            Guid g = new Guid(ole.ClassIdentifier);
            if (g.ToString() == "b801ca65-a1fc-11d0-85ad-444553540000")
            {
                fileName += "pdf";
            }
            else
            {
                fileName += "jpg";
            }                      
            break;
        default:
            // Xử lý các định dạng khác hoặc đưa ra ngoại lệ
            break;
    }

    File.WriteAllBytes(fileName, oleData);
}
```
Phần này trình bày cách xử lý động các định dạng tệp khác nhau và lưu chúng một cách phù hợp.

## Ứng dụng thực tế

Sau đây là một số trường hợp sử dụng thực tế để trích xuất các đối tượng OLE từ tệp Excel:
1. **Báo cáo dữ liệu tự động:** Tự động trích xuất tài liệu hoặc hình ảnh nhúng như một phần của quy trình báo cáo dữ liệu.
2. **Hệ thống lưu trữ dữ liệu:** Lưu trữ nội dung nhúng trong bảng tính cho mục đích tuân thủ.
3. **Tích hợp với Hệ thống quản lý tài liệu:** Tích hợp liền mạch các đối tượng OLE đã trích xuất vào các nền tảng quản lý tài liệu khác.

## Cân nhắc về hiệu suất

Để đảm bảo hiệu suất tối ưu khi làm việc với Aspose.Cells:
- **Tối ưu hóa việc sử dụng bộ nhớ:** Sử dụng `MemoryStream` một cách khôn ngoan để quản lý bộ nhớ hiệu quả trong quá trình xử lý tập tin.
- **Xử lý hàng loạt:** Xử lý tệp theo từng đợt nếu xử lý các tập dữ liệu lớn để tránh sử dụng quá nhiều tài nguyên.
- **Thực hành tốt nhất:** Cập nhật thường xuyên thư viện .NET của bạn và tận dụng các tính năng mới nhất của Aspose.Cells để có hiệu suất tốt hơn.

## Phần kết luận

Bằng cách làm theo hướng dẫn này, bạn đã học cách tự động trích xuất các đối tượng OLE từ sổ làm việc Excel bằng Aspose.Cells cho .NET. Kỹ năng này nâng cao hiệu quả xử lý dữ liệu và giảm lỗi xử lý thủ công trong quy trình làm việc của bạn.

### Các bước tiếp theo:
- Thử nghiệm với nhiều định dạng tập tin khác nhau.
- Khám phá các tính năng bổ sung do Aspose.Cells cung cấp để đơn giản hóa hơn nữa các tác vụ của bạn.

Bạn đã sẵn sàng thử chưa? Hãy bắt đầu áp dụng những kỹ thuật này vào dự án của bạn ngay hôm nay!

## Phần Câu hỏi thường gặp

1. **Tôi phải xử lý các định dạng đối tượng OLE không được hỗ trợ như thế nào?**
   - Đối với các định dạng không xác định hoặc không được hỗ trợ, hãy sử dụng `FileFormatType.Unknown` trường hợp và triển khai logic tùy chỉnh khi cần thiết.

2. **Aspose.Cells có thể xử lý các tệp Excel lớn một cách hiệu quả không?**
   - Có, nó được tối ưu hóa cho hiệu suất. Hãy cân nhắc xử lý hàng loạt cho các tập dữ liệu rất lớn để duy trì hiệu quả.

3. **Nếu định dạng tệp giải nén của tôi không đúng thì sao?**
   - Kiểm tra lại `FileFormatType` trong câu lệnh chuyển đổi của bạn và đảm bảo ánh xạ đúng các định dạng.

4. **Aspose.Cells .NET có miễn phí sử dụng không?**
   - Bạn có thể bắt đầu dùng thử miễn phí 30 ngày và mua giấy phép để sử dụng lâu dài.

5. **Làm thế nào để tích hợp các đối tượng OLE đã trích xuất vào các hệ thống khác?**
   - Sử dụng các thao tác I/O tệp chuẩn hoặc các công cụ tích hợp để di chuyển tệp đến hệ thống mong muốn.

## Tài nguyên
- **Tài liệu:** [Tài liệu Aspose.Cells .NET](https://reference.aspose.com/cells/net/)
- **Tải xuống:** [Bản phát hành mới nhất](https://releases.aspose.com/cells/net/)
- **Mua giấy phép:** [Mua ngay](https://purchase.aspose.com/buy)
- **Dùng thử miễn phí:** [Bắt đầu](https://releases.aspose.com/cells/net/)
- **Giấy phép tạm thời:** [Yêu cầu ở đây](https://purchase.aspose.com/temporary-license/)
- **Diễn đàn hỗ trợ:** [Hỗ trợ Aspose](https://forum.aspose.com/c/cells/9)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}