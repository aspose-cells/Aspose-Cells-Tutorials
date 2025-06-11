---
"date": "2025-04-05"
"description": "Tìm hiểu cách triển khai định dạng số tùy chỉnh trong .NET bằng Aspose.Cells để trình bày dữ liệu Excel chính xác. Hướng dẫn này bao gồm thiết lập, định dạng ngày, phần trăm và tiền tệ."
"title": "Cách sử dụng Định dạng số tùy chỉnh trong .NET với Aspose.Cells&#58; Hướng dẫn từng bước"
"url": "/vi/net/formatting/custom-number-formats-net-aspose-cells-guide/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# Cách sử dụng Định dạng số tùy chỉnh trong .NET với Aspose.Cells: Hướng dẫn từng bước

## Giới thiệu

Cải thiện thao tác tệp Excel của bạn bằng C# và .NET với khả năng kiểm soát chính xác các định dạng số. Hướng dẫn này hướng dẫn bạn cách thiết lập định dạng số tùy chỉnh trong các ứng dụng .NET bằng Aspose.Cells for .NET, một thư viện mạnh mẽ được thiết kế để thao tác Excel.

Bằng cách tận dụng Aspose.Cells, áp dụng nhiều kiểu khác nhau vào dữ liệu một cách dễ dàng, đảm bảo tính rõ ràng và chính xác trong báo cáo của bạn. Cho dù định dạng ngày tháng, phần trăm hay giá trị tiền tệ, việc thành thạo chức năng này sẽ hợp lý hóa quy trình làm việc của bạn.

**Những gì bạn sẽ học được:**
- Thiết lập Aspose.Cells cho .NET
- Triển khai định dạng số tùy chỉnh bằng C#
- Áp dụng các kiểu theo chương trình cho các ô Excel
- Ứng dụng thực tế của định dạng số tùy chỉnh

## Điều kiện tiên quyết

Hãy đảm bảo bạn có những điều sau trước khi bắt đầu:
1. **Môi trường phát triển**: Thiết lập hoạt động của .NET với Visual Studio hoặc bất kỳ IDE tương thích nào.
2. **Aspose.Cells cho thư viện .NET**: Cần có phiên bản 22.x trở lên để sử dụng hướng dẫn này.
3. **Kiến thức cơ bản về C#**:Sự quen thuộc với cú pháp C# và các khái niệm lập trình sẽ giúp bạn theo dõi dễ dàng.

## Thiết lập Aspose.Cells cho .NET

Để sử dụng Aspose.Cells trong dự án của bạn, hãy cài đặt thư viện bằng .NET CLI hoặc Package Manager Console trong Visual Studio.

**Cài đặt .NET CLI:**
```bash
dotnet add package Aspose.Cells
```

**Cài đặt Trình quản lý gói:**
```powershell
PM> NuGet\Install-Package Aspose.Cells
```

### Mua lại giấy phép

Aspose.Cells cung cấp bản dùng thử miễn phí để đánh giá và tùy chọn sử dụng mở rộng thông qua giấy phép tạm thời hoặc mua.
- **Dùng thử miễn phí**: Tải xuống từ [đây](https://releases.aspose.com/cells/net/).
- **Giấy phép tạm thời**: Nộp đơn tại [Trang giấy phép tạm thời Aspose](https://purchase.aspose.com/temporary-license/) để loại bỏ những hạn chế trong việc đánh giá.
- **Mua**: Để truy cập đầy đủ, hãy truy cập [Trang mua hàng](https://purchase.aspose.com/buy).

Để khởi tạo Aspose.Cells trong dự án của bạn:
```csharp
// Nhập không gian tên
using Aspose.Cells;

// Khởi tạo một đối tượng Workbook mới
Workbook workbook = new Workbook();
```

## Hướng dẫn thực hiện

Chúng tôi sẽ giới thiệu các tính năng chính để tùy chỉnh định dạng số bằng Aspose.Cells.

### Thêm định dạng ngày tùy chỉnh
**Tổng quan**: Học cách định dạng ngày tháng trong ô Excel theo kiểu tùy chỉnh.
1. **Tạo hoặc truy cập một bảng tính**
   ```csharp
   int sheetIndex = workbook.Worksheets.Add();
   Worksheet worksheet = workbook.Worksheets[sheetIndex];
   ```
2. **Đặt ngày hệ thống hiện tại với định dạng tùy chỉnh**
   Thêm ngày hiện tại vào ô "A1" và áp dụng định dạng hiển thị tùy chỉnh.
   ```csharp
   // Chèn ngày hệ thống hiện tại vào A1
   worksheet.Cells["A1"].PutValue(DateTime.Now);

   // Lấy đối tượng kiểu để tùy chỉnh
   Style style = worksheet.Cells["A1"].GetStyle();

   // Đặt định dạng số tùy chỉnh thành "d-mmm-yy"
   style.Custom = "d-mmm-yy";

   // Áp dụng kiểu tùy chỉnh trở lại ô A1
   worksheet.Cells["A1"].SetStyle(style);
   ```

### Định dạng giá trị số theo phần trăm
**Tổng quan**: Hiển thị giá trị số theo định dạng phần trăm.
1. **Chèn và Định dạng Giá trị**
   ```csharp
   // Thêm giá trị số vào ô A2
   worksheet.Cells["A2"].PutValue(20);

   // Lấy kiểu để định dạng
   Style style = worksheet.Cells["A2"].GetStyle();

   // Áp dụng định dạng số tùy chỉnh dưới dạng phần trăm
   style.Custom = "0.0%";

   // Đặt lại kiểu định dạng cho ô A2
   worksheet.Cells["A2"].SetStyle(style);
   ```

### Áp dụng định dạng tiền tệ
**Tổng quan**: Hiển thị số theo định dạng tiền tệ, với định dạng cụ thể cho các giá trị âm.
1. **Chèn và định dạng giá trị tiền tệ**
   ```csharp
   // Thêm giá trị vào ô A3
   worksheet.Cells["A3"].PutValue(2546);

   // Truy cập đối tượng kiểu
   Style style = worksheet.Cells["A3"].GetStyle();

   // Đặt định dạng tiền tệ tùy chỉnh
   style.Custom = "\u00a3#,##0;[Red]$-#,##0";

   // Áp dụng cho ô A3
   worksheet.Cells["A3"].SetStyle(style);
   ```

## Ứng dụng thực tế

Định dạng số tùy chỉnh rất có giá trị trong các trường hợp như:
1. **Báo cáo tài chính**: Định dạng giá trị tiền tệ để rõ ràng hơn.
2. **Bảng điều khiển bán hàng**: Hiển thị số liệu bán hàng dưới dạng phần trăm để làm nổi bật số liệu hiệu suất.
3. **Lập kế hoạch sự kiện**: Sử dụng định dạng ngày tháng để sắp xếp và trình bày lịch trình sự kiện một cách liền mạch.

## Cân nhắc về hiệu suất
Khi làm việc với các tập dữ liệu lớn, hãy tối ưu hóa hiệu suất của Aspose.Cells:
- Giảm thiểu việc sử dụng bộ nhớ bằng cách loại bỏ các đối tượng kịp thời bằng cách sử dụng `GC.Collect()` sau khi lưu tập tin.
- Sử dụng luồng để đọc/ghi tệp Excel thay vì tải toàn bộ tài liệu vào bộ nhớ.
- Triển khai các biện pháp tốt nhất trong quản lý bộ nhớ .NET để duy trì hiệu quả.

## Phần kết luận
Bằng cách làm theo hướng dẫn này, bạn đã học cách triển khai định dạng số tùy chỉnh trong ứng dụng .NET của mình bằng Aspose.Cells. Khả năng này cải thiện khả năng trình bày dữ liệu và đảm bảo tính chính xác và hấp dẫn trực quan trong báo cáo và bảng tính.

**Các bước tiếp theo**Thử nghiệm các tùy chọn định dạng khác có sẵn trong Aspose.Cells, chẳng hạn như định dạng có điều kiện hoặc cải tiến biểu đồ.

## Phần Câu hỏi thường gặp
1. **Làm thế nào để tôi có được giấy phép tạm thời cho Aspose.Cells?**
   - Nộp đơn tại [Trang giấy phép tạm thời](https://purchase.aspose.com/temporary-license/).
2. **Những định dạng nào được hỗ trợ cho kiểu số tùy chỉnh trong Aspose.Cells?**
   - Ngày tháng, phần trăm, tiền tệ và nhiều thông tin khác bằng cách sử dụng chuỗi định dạng Excel chuẩn.
3. **Tôi có thể sử dụng Aspose.Cells với các ngôn ngữ .NET khác như VB.NET không?**
   - Có, thư viện này tương thích với tất cả các ngôn ngữ hỗ trợ .NET.
4. **Tôi phải làm gì nếu số được định dạng của tôi không hiển thị đúng?**
   - Kiểm tra lại chuỗi định dạng số tùy chỉnh của bạn để tìm lỗi đánh máy hoặc lỗi cú pháp.
5. **Tôi có thể tìm thêm ví dụ về cách sử dụng Aspose.Cells ở đâu?**
   - Khám phá tài liệu chi tiết và mã mẫu tại [Tài liệu Aspose](https://reference.aspose.com/cells/net/).

## Tài nguyên
- [Tài liệu Aspose.Cells cho .NET](https://reference.aspose.com/cells/net/)
- [Tải xuống phiên bản mới nhất](https://releases.aspose.com/cells/net/)
- [Mua giấy phép](https://purchase.aspose.com/buy)
- [Tải xuống dùng thử miễn phí](https://releases.aspose.com/cells/net/)
- [Yêu cầu cấp giấy phép tạm thời](https://purchase.aspose.com/temporary-license/)
- [Diễn đàn hỗ trợ Aspose](https://forum.aspose.com/c/cells/9)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}