---
"date": "2025-04-05"
"description": "Tìm hiểu cách tùy chỉnh tổng phụ trong bảng tính Excel bằng Aspose.Cells cho .NET. Hướng dẫn này bao gồm thiết lập, triển khai và ứng dụng thực tế."
"title": "Cách triển khai Tổng phụ tùy chỉnh trong Excel bằng Aspose.Cells cho .NET"
"url": "/vi/net/data-analysis/custom-subtotals-aspose-cells-net/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# Cách triển khai Tổng phụ tùy chỉnh trong Excel với Aspose.Cells cho .NET

## Giới thiệu

Bạn có muốn tạo báo cáo tùy chỉnh với nhãn tổng phụ cụ thể trong tệp Excel của mình không? Hướng dẫn này sẽ chỉ cho bạn cách thực hiện điều này bằng thư viện Aspose.Cells mạnh mẽ dành cho .NET. Chúng tôi sẽ tập trung vào việc tạo tổng phụ trung bình phù hợp với nhu cầu của bạn.

**Những gì bạn sẽ học được:**
- Thiết lập và sử dụng Aspose.Cells cho .NET
- Triển khai một lớp tùy chỉnh để ghi đè tên tổng phụ mặc định
- Thêm tổng phụ tùy chỉnh vào bảng tính Excel
- Tính toán công thức và điều chỉnh độ rộng cột tự động

## Điều kiện tiên quyết

Trước khi bắt đầu, hãy đảm bảo bạn có:
- **Aspose.Cells cho .NET** thư viện được cài đặt trong dự án của bạn (các bước cài đặt bên dưới)
- Môi trường phát triển với Visual Studio hoặc IDE tương tự hỗ trợ các dự án C# và .NET
- Kiến thức cơ bản về lập trình C# và các thao tác trên Excel

## Thiết lập Aspose.Cells cho .NET

Để bắt đầu, hãy cài đặt thư viện Aspose.Cells cho .NET bằng NuGet Package Manager hoặc .NET CLI.

**.NETCLI:**
```bash
dotnet add package Aspose.Cells
```

**Bảng điều khiển quản lý gói:**
```powershell
PM> Install-Package Aspose.Cells
```

### Mua lại giấy phép
Aspose cung cấp giấy phép dùng thử miễn phí trong 30 ngày, cho phép bạn kiểm tra tất cả các tính năng mà không có giới hạn. Nhận ngay [đây](https://purchase.aspose.com/temporary-license/). Để sử dụng liên tục, hãy cân nhắc mua giấy phép đầy đủ hoặc khám phá các tùy chọn đăng ký trên [trang mua hàng](https://purchase.aspose.com/buy).

### Khởi tạo và thiết lập
Sau khi cài đặt, hãy nhập các không gian tên cần thiết:
```csharp
using Aspose.Cells;
```

## Hướng dẫn thực hiện

Chúng tôi sẽ chia nhỏ quá trình triển khai này thành các bước để giúp bạn hiểu từng phần của quy trình.

### Bước 1: Tạo lớp cài đặt tùy chỉnh
Đầu tiên, tạo một lớp tùy chỉnh mở rộng `GlobalizationSettings`:
```csharp
class CustomSettings : GlobalizationSettings
{
    public override string GetTotalName(ConsolidationFunction functionType)
    {
        switch (functionType)
        {
            case ConsolidationFunction.Average:
                return "AVG";
            default:
                return base.GetTotalName(functionType);
        }
    }

    public override string GetGrandTotalName(ConsolidationFunction functionType)
    {
        switch (functionType)
        {
            case ConsolidationFunction.Average:
                return "GRD AVG";
            default:
                return base.GetGrandTotalName(functionType);
        }
    }
}
```
**Giải thích:** Lớp này tùy chỉnh cách đặt tên tổng phụ cho các hàm khác nhau, như hàm Trung bình.

### Bước 2: Tải sổ làm việc của bạn
Tải bảng tính Excel hiện có chứa dữ liệu bạn muốn thao tác:
```csharp
Workbook book = new Workbook("sampleCustomLabelsSubtotals.xlsx");
```
**Giải thích:** Thay thế `"sampleCustomLabelsSubtotals.xlsx"` với đường dẫn tệp của bạn. Điều này khởi tạo `Workbook` sự vật.

### Bước 3: Thiết lập cài đặt toàn cầu hóa tùy chỉnh
Gán các thiết lập tùy chỉnh của chúng tôi vào sổ làm việc:
```csharp
book.Settings.GlobalizationSettings = new CustomSettings();
```
**Giải thích:** Điều này đảm bảo bất kỳ tính toán tổng phụ nào cũng sử dụng nhãn tùy chỉnh của chúng tôi từ `CustomSettings`.

### Bước 4: Thêm chức năng Tổng phụ
Thêm tổng phụ vào bảng tính của bạn trong phạm vi được chỉ định bằng cách sử dụng hàm trung bình:
```csharp
Worksheet sheet = book.Worksheets[0];
sheet.Cells.Subtotal(CellArea.CreateCellArea("A2", "B9"), 0, ConsolidationFunction.Average, new int[] { 1 });
```
**Giải thích:** Mục tiêu này nhắm vào các ô từ A2 đến B9 và thêm tổng phụ trung bình dựa trên cột đầu tiên (chỉ mục 1).

### Bước 5: Tính toán công thức và điều chỉnh cột
Sau khi thêm tổng phụ, hãy tính toán bất kỳ công thức nào và tự động điều chỉnh cột:
```csharp
book.CalculateFormula();
sheet.AutoFitColumns();
```
**Giải thích:** `CalculateFormula()` đảm bảo tất cả các tính toán đều được cập nhật. `AutoFitColumns()` điều chỉnh độ rộng của cột cho phù hợp với nội dung.

### Bước 6: Lưu sổ làm việc của bạn
Lưu những thay đổi của bạn trở lại vào một tập tin mới:
```csharp
book.Save("outputCustomLabelsSubtotals.xlsx");
```
**Giải thích:** Thao tác này sẽ lưu bảng tính đã sửa đổi của bạn với tổng phụ tùy chỉnh và các cột đã điều chỉnh.

## Ứng dụng thực tế
Sau đây là một số tình huống thực tế mà tổng phụ tùy chỉnh có thể hữu ích:
1. **Báo cáo tài chính**Tùy chỉnh nhãn tổng phụ để phản ánh các điều khoản tài chính cụ thể như "Trung bình ròng" hoặc "Tổng doanh thu điều chỉnh".
2. **Quản lý hàng tồn kho**: Sử dụng tổng phụ được thiết kế riêng cho các danh mục hoặc nhà cung cấp khác nhau trong báo cáo hàng tồn kho của bạn.
3. **Phân tích dữ liệu bán hàng**: Triển khai các tính toán trung bình tự động cập nhật khi có dữ liệu bán hàng mới.
4. **Hệ thống chấm điểm giáo dục**: Tùy chỉnh nhãn để thể hiện điểm trung bình của học sinh trong các môn học.
5. **Bảng thông tin kinh doanh thông minh**: Điều chỉnh nhãn tổng phụ để phù hợp với các KPI hoặc số liệu cụ thể nhằm mang lại sự rõ ràng hơn.

## Cân nhắc về hiệu suất
Khi làm việc với Aspose.Cells, hãy cân nhắc những mẹo sau để tối ưu hóa hiệu suất:
- **Sử dụng bộ nhớ hiệu quả**: Loại bỏ các đối tượng không còn cần thiết bằng cách sử dụng `Dispose()` phương pháp.
- **Xử lý hàng loạt**: Nếu xử lý nhiều sổ làm việc, hãy thực hiện các thao tác hàng loạt để giảm thiểu chi phí.
- **Hoạt động không đồng bộ**Đối với các tệp lớn, hãy triển khai các phương pháp không đồng bộ khi có thể.

## Phần kết luận
Hướng dẫn này khám phá cách triển khai tổng phụ tùy chỉnh với Aspose.Cells cho .NET. Bằng cách tạo một `GlobalizationSettings` lớp và xử lý dữ liệu Excel theo chương trình, bạn có thể nâng cao khả năng báo cáo của mình.

**Các bước tiếp theo:** Thử nghiệm thêm bằng cách thêm các chức năng hợp nhất khác hoặc tích hợp các chức năng này vào các ứng dụng lớn hơn.

## Phần Câu hỏi thường gặp
1. **Aspose.Cells dành cho .NET là gì?**
   - Đây là thư viện cho phép các nhà phát triển làm việc với các tệp Excel theo chương trình mà không cần cài đặt Microsoft Office.
2. **Tôi phải xử lý lỗi khi tính toán công thức như thế nào?**
   - Đảm bảo tất cả các phạm vi ô được chỉ định chính xác và kiểm tra các tham chiếu vòng tròn trong sổ làm việc của bạn.
3. **Tôi có thể áp dụng nhãn tổng phụ tùy chỉnh cho các chức năng khác nhau không?**
   - Vâng, mở rộng `GetTotalName` phương pháp xử lý nhiều loại hàm hợp nhất khác nhau ngoài giá trị trung bình.
4. **Aspose.Cells có miễn phí sử dụng không?**
   - Phiên bản dùng thử có sẵn với quyền truy cập đầy đủ tính năng trong 30 ngày. Để tiếp tục sử dụng, cần phải mua giấy phép.
5. **Tôi có thể xử lý nhiều bảng tính cùng lúc bằng thư viện này không?**
   - Có, bằng cách lặp lại từng sổ làm việc theo vòng lặp và áp dụng các thao tác tương tự như đã trình bày ở trên.

## Tài nguyên
- [Tài liệu Aspose.Cells](https://reference.aspose.com/cells/net/)
- [Tải xuống Aspose.Cells cho .NET](https://releases.aspose.com/cells/net/)
- [Mua giấy phép](https://purchase.aspose.com/buy)
- [Phiên bản dùng thử miễn phí](https://releases.aspose.com/cells/net/)
- [Đơn xin cấp giấy phép tạm thời](https://purchase.aspose.com/temporary-license/)
- [Diễn đàn hỗ trợ cộng đồng](https://forum.aspose.com/c/cells/9)

Bằng cách làm theo hướng dẫn này, giờ đây bạn đã được trang bị để khai thác sức mạnh của Aspose.Cells cho .NET trong việc tạo tổng phụ tùy chỉnh và hơn thế nữa. Chúc bạn viết mã vui vẻ!


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}