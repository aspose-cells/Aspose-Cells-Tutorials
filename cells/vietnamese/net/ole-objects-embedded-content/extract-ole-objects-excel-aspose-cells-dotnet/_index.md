---
"date": "2025-04-05"
"description": "Hướng dẫn mã cho Aspose.Cells Net"
"title": "Trích xuất các đối tượng OLE từ Excel bằng Aspose.Cells"
"url": "/vi/net/ole-objects-embedded-content/extract-ole-objects-excel-aspose-cells-dotnet/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# Trích xuất các đối tượng OLE từ tệp Excel bằng Aspose.Cells .NET

## Giới thiệu

Bạn có đang gặp khó khăn trong việc trích xuất các đối tượng nhúng từ các tệp Excel một cách hiệu quả không? Cho dù đó là tài liệu, bản trình bày hay các loại tệp khác được ẩn dưới dạng đối tượng OLE trong bảng tính của bạn, việc quản lý chúng một cách liền mạch có thể là một thách thức. Hướng dẫn này sẽ hướng dẫn bạn cách tận dụng thư viện Aspose.Cells for .NET mạnh mẽ để trích xuất và lưu các đối tượng nhúng này một cách dễ dàng dựa trên loại định dạng của chúng.

**Những gì bạn sẽ học được:**
- Cách thiết lập Aspose.Cells trong môi trường .NET của bạn
- Trích xuất các đối tượng OLE từ các tệp Excel bằng Aspose.Cells
- Lưu các đối tượng được trích xuất dựa trên định dạng tệp của chúng
- Xử lý các loại đối tượng khác nhau một cách dễ dàng

Trước khi bắt đầu triển khai, hãy đảm bảo rằng bạn đã sẵn sàng mọi thứ.

## Điều kiện tiên quyết (H2)

Để thực hiện hướng dẫn này một cách hiệu quả, hãy đảm bảo rằng bạn có:

- **Aspose.Cells cho .NET**:Đây là thư viện toàn diện cho phép bạn làm việc với các tệp Excel trong các ứng dụng .NET của mình.
  - Phiên bản: Đảm bảo khả năng tương thích bằng cách kiểm tra phiên bản mới nhất trên [Trang web của Aspose](https://reference.aspose.com/cells/net/).
- **Thiết lập môi trường**:
  - Một môi trường phát triển như Visual Studio hoặc một IDE khác hỗ trợ các dự án .NET
- **Điều kiện tiên quyết về kiến thức**:
  - Hiểu biết cơ bản về các khái niệm lập trình C# và .NET

## Thiết lập Aspose.Cells cho .NET (H2)

### Cài đặt

Để bắt đầu sử dụng Aspose.Cells trong dự án của bạn, bạn cần cài đặt nó. Bạn có thể thực hiện việc này thông qua các trình quản lý gói sau:

**.NETCLI**
```bash
dotnet add package Aspose.Cells
```

**Bảng điều khiển quản lý gói**
```powershell
PM> NuGet\Install-Package Aspose.Cells
```

### Mua lại giấy phép

Aspose.Cells cho .NET cung cấp bản dùng thử miễn phí, bạn có thể tải xuống từ [đây](https://releases.aspose.com/cells/net/). Để sử dụng lâu dài, hãy cân nhắc mua giấy phép hoặc yêu cầu cấp giấy phép tạm thời qua [Trang mua hàng của Aspose](https://purchase.aspose.com/buy) hoặc của họ [trang giấy phép tạm thời](https://purchase.aspose.com/temporary-license/).

### Khởi tạo cơ bản

Sau đây là cách bạn có thể khởi tạo và thiết lập Aspose.Cells trong dự án của mình:

```csharp
using Aspose.Cells;

// Khởi tạo một phiên bản sổ làm việc từ một tệp Excel
Workbook workbook = new Workbook("path_to_your_file.xlsx");
```

## Hướng dẫn thực hiện (H2)

Chúng ta hãy phân tích quá trình trích xuất các đối tượng OLE được nhúng trong tệp Excel thành các phần hợp lý.

### Trích xuất các đối tượng OLE

Tính năng này cho phép bạn trích xuất các loại tệp khác nhau được nhúng trong trang tính Excel của bạn và lưu chúng dựa trên định dạng của chúng.

#### Bước 1: Tải sổ làm việc của bạn
```csharp
string SourceDir = "YOUR_SOURCE_DIRECTORY";
Workbook workbook = new Workbook(SourceDir + "/book1.xls");
```

#### Bước 2: Truy cập các đối tượng OLE
```csharp
Aspose.Cells.Drawing.OleObjectCollection oles = workbook.Worksheets[0].OleObjects;
```

#### Bước 3: Lặp lại và Lưu dựa trên Định dạng

Mỗi đối tượng nhúng được xử lý dựa trên loại định dạng tệp của nó.

```csharp
for (int i = 0; i < oles.Count; i++)
{
    Aspose.Cells.Drawing.OleObject ole = oles[i];
    string fileName = "YOUR_OUTPUT_DIRECTORY/ole_" + i + ".";

    switch (ole.FileFormatType)
    {
        case FileFormatType.Doc:
            fileName += "doc";
            break;
        case FileFormatType.Xlsx:
            fileName += "Xlsx";
            break;
        case FileFormatType.Ppt:
            fileName += "Ppt";
            break;
        case FileFormatType.Pdf:
            fileName += "Pdf";
            break;
        default:
            fileName += "Jpg";  // Xử lý các định dạng không xác định dưới dạng hình ảnh
            break;
    }

    if (ole.FileFormatType == FileFormatType.Xlsx)
    {
        MemoryStream ms = new MemoryStream();
        ms.Write(ole.ObjectData, 0, ole.ObjectData.Length);
        
        Workbook oleBook = new Workbook(ms);
        oleBook.Settings.IsHidden = false; // Đảm bảo sổ làm việc không bị ẩn
        oleBook.Save("YOUR_OUTPUT_DIRECTORY/Excel_File" + i + ".out.xlsx");
    }
    else
    {
        using (FileStream fs = File.Create(fileName))
        {
            fs.Write(ole.ObjectData, 0, ole.ObjectData.Length);
        }
    }
}
```

### Giải thích các bộ phận chính

- **Kiểu Định dạng Tệp**: Xác định cách lưu đối tượng đã trích xuất. Mỗi trường hợp sẽ thêm phần mở rộng tệp có liên quan.
- **Bộ nhớ Stream**: Được sử dụng để xử lý các tệp Excel do cấu trúc phức tạp của chúng.

### Mẹo khắc phục sự cố
- Đảm bảo đường dẫn được thiết lập chính xác và có thể truy cập được trong môi trường của bạn.
- Kiểm tra quyền truy cập tệp nếu bạn gặp sự cố khi ghi tệp.

## Ứng dụng thực tế (H2)

Hiểu được cách trích xuất các đối tượng OLE có thể mở ra nhiều ứng dụng thực tế khác nhau:

1. **Lưu trữ dữ liệu**: Tự động trích xuất các tài liệu nhúng để lưu trữ hoặc xem xét dễ dàng hơn.
2. **Tích hợp với Hệ thống quản lý tài liệu**: Tích hợp liền mạch các đối tượng đã trích xuất vào quy trình quản lý tài liệu của bạn.
3. **Tái sử dụng nội dung**:Sử dụng lại các bài thuyết trình, tệp PDF và các loại phương tiện khác cho các nền tảng hoặc định dạng khác nhau.

## Cân nhắc về hiệu suất (H2)

- Tối ưu hóa việc sử dụng bộ nhớ bằng cách loại bỏ các luồng (`MemoryStream`, `FileStream`) đúng cách sau khi sử dụng.
- Khi xử lý các tệp lớn, hãy cân nhắc xử lý theo từng đợt để tránh tiêu tốn quá nhiều tài nguyên.
  
### Thực hành tốt nhất

- Cập nhật Aspose.Cells thường xuyên để được hưởng lợi từ những cải tiến về hiệu suất và các tính năng mới.
- Tạo hồ sơ ứng dụng của bạn để xác định những điểm nghẽn liên quan đến quy trình trích xuất tệp.

## Phần kết luận

Trong hướng dẫn này, bạn đã học cách trích xuất hiệu quả các đối tượng OLE được nhúng trong các tệp Excel bằng Aspose.Cells cho .NET. Khả năng này có thể là một bước ngoặt trong việc quản lý quy trình làm việc của tài liệu và các dự án tích hợp dữ liệu.

Để khám phá thêm khả năng của Aspose.Cells, hãy cân nhắc thử nghiệm các tính năng khác như thao tác bảng tính hoặc chuyển đổi dữ liệu.

## Phần Câu hỏi thường gặp (H2)

1. **Tôi có thể trích xuất những định dạng tệp nào dưới dạng đối tượng OLE?**
   - Các định dạng được hỗ trợ phổ biến bao gồm DOC, XLSX, PPT và PDF. Các định dạng không được nhận dạng được lưu dưới dạng JPG theo mặc định.
   
2. **Làm thế nào để xử lý các tệp Excel lớn có nhiều đối tượng nhúng?**
   - Tối ưu hóa hiệu suất bằng cách xử lý theo từng phần hoặc từng đợt có thể quản lý được.

3. **Phương pháp này có thể trích xuất hình ảnh từ bảng tính Excel không?**
   - Có, hình ảnh có thể được trích xuất và lưu riêng biệt bằng các tính năng của Aspose.Cells.

4. **Có giới hạn số lượng đối tượng OLE có thể trích xuất cùng một lúc không?**
   - Không có giới hạn cụ thể, nhưng hạn chế về tài nguyên có thể đòi hỏi phải xử lý hàng loạt đối với số lượng lớn.

5. **Tôi phải xử lý lỗi trong quá trình trích xuất như thế nào?**
   - Triển khai các khối try-catch xung quanh mã của bạn để quản lý các ngoại lệ và đảm bảo thực thi trơn tru.

## Tài nguyên

- [Tài liệu Aspose.Cells](https://reference.aspose.com/cells/net/)
- [Tải xuống Aspose.Cells](https://releases.aspose.com/cells/net/)
- [Mua giấy phép](https://purchase.aspose.com/buy)
- [Dùng thử miễn phí](https://releases.aspose.com/cells/net/)
- [Đơn xin cấp giấy phép tạm thời](https://purchase.aspose.com/temporary-license/)
- [Diễn đàn hỗ trợ Aspose](https://forum.aspose.com/c/cells/9)

Bằng cách làm theo hướng dẫn này, giờ đây bạn đã có thể tự tin xử lý các đối tượng nhúng trong tệp Excel bằng Aspose.Cells cho .NET. Chúc bạn viết mã vui vẻ!

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}