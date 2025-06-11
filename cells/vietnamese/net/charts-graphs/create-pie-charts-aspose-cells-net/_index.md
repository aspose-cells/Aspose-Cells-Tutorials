---
"date": "2025-04-05"
"description": "Tìm hiểu cách tạo biểu đồ hình tròn động với các đường dẫn bằng Aspose.Cells cho .NET. Thực hiện theo hướng dẫn này để nâng cao kỹ năng trực quan hóa dữ liệu của bạn."
"title": "Tạo biểu đồ hình tròn có đường dẫn trong Aspose.Cells .NET&#58; Hướng dẫn toàn diện"
"url": "/vi/net/charts-graphs/create-pie-charts-aspose-cells-net/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# Tạo biểu đồ hình tròn có đường dẫn bằng Aspose.Cells .NET

## Giới thiệu
Cải thiện khả năng trực quan hóa dữ liệu của bạn bằng cách tạo biểu đồ hình tròn nhiều thông tin hơn với Aspose.Cells cho .NET. Hướng dẫn từng bước này sẽ chỉ cho bạn cách thêm đường dẫn vào các phân đoạn biểu đồ hình tròn, giúp bạn dễ dàng xác định các danh mục dữ liệu tương ứng chỉ trong nháy mắt. Bằng cách làm theo hướng dẫn này, khả năng trực quan hóa của bạn sẽ vừa hấp dẫn về mặt thị giác vừa có chức năng cao.

**Những gì bạn sẽ học được:**
- Thiết lập Aspose.Cells cho .NET trong môi trường của bạn
- Tạo biểu đồ hình tròn đường dẫn tùy chỉnh bằng C#
- Lưu biểu đồ dưới dạng hình ảnh hoặc trong sổ làm việc Excel

Đảm bảo bạn đã chuẩn bị mọi thứ để thực hiện hiệu quả.

## Điều kiện tiên quyết
Trước khi bắt đầu, hãy đảm bảo bạn đáp ứng các điều kiện tiên quyết sau:

- **Thư viện và Phiên bản**: Cài đặt Aspose.Cells cho .NET. Đảm bảo dự án của bạn được thiết lập với phiên bản mới nhất.
- **Thiết lập môi trường**: Hướng dẫn này giả định rằng có một môi trường .NET tương thích với Aspose.Cells.
- **Điều kiện tiên quyết về kiến thức**Có kiến thức cơ bản về lập trình C# và các thao tác trên Excel sẽ rất có lợi.

## Thiết lập Aspose.Cells cho .NET
Để bắt đầu, hãy cài đặt Aspose.Cells vào dự án của bạn thông qua:

**.NETCLI**
```bash
dotnet add package Aspose.Cells
```

**Trình quản lý gói**
```powershell
PM> NuGet\Install-Package Aspose.Cells
```

Nhận giấy phép sử dụng đầy đủ chức năng bằng cách chọn một trong các tùy chọn sau:
- **Dùng thử miễn phí**: Bắt đầu dùng thử miễn phí của bạn trên [Trang tải xuống Aspose](https://releases.aspose.com/cells/net/).
- **Giấy phép tạm thời**: Xin giấy phép tạm thời [đây](https://purchase.aspose.com/temporary-license/).
- **Mua**: Để có đầy đủ tính năng, hãy mua giấy phép [đây](https://purchase.aspose.com/buy).

Khởi tạo Aspose.Cells trong dự án của bạn bằng cách tạo một phiên bản của `Workbook` lớp học.

## Hướng dẫn thực hiện

### Tạo Sổ làm việc và Bảng tính
1. **Khởi tạo sổ làm việc**
   Tạo một bảng tính mới ở định dạng XLSX:
   ```csharp
   Workbook workbook = new Workbook(FileFormatType.Xlsx);
   ```

2. **Truy cập vào trang tính đầu tiên**
   Sử dụng bảng tính đầu tiên để nhập dữ liệu:
   ```csharp
   Worksheet worksheet = workbook.Worksheets[0];
   ```

3. **Thêm dữ liệu cho biểu đồ hình tròn**
   Điền các danh mục và giá trị vào bảng tính của bạn:
   ```csharp
   worksheet.Cells["A1"].PutValue("Retail");
   // Thêm tên danh mục còn lại...
   worksheet.Cells["B1"].PutValue(10.4);
   // Thêm các giá trị tương ứng...
   ```

### Thêm biểu đồ hình tròn vào bảng tính
1. **Tạo biểu đồ hình tròn**
   Tạo biểu đồ hình tròn và thêm vào bộ sưu tập biểu đồ của bảng tính:
   ```csharp
   int id = worksheet.Charts.Add(ChartType.Pie, 3, 3, 23, 13);
   ```

2. **Cấu hình Dữ liệu Chuỗi và Danh mục**
   Liên kết dữ liệu cho các chuỗi và danh mục:
   ```csharp
   Chart chart = worksheet.Charts[id];
   chart.NSeries.Add("B1:B16", true);
   chart.NSeries.CategoryData = "A1:A16";
   ```

3. **Tùy chỉnh nhãn dữ liệu**
   Tắt hiển thị chú giải, đặt nhãn dữ liệu để hiển thị tên danh mục và phần trăm:
   ```csharp
   chart.ShowLegend = false;
   DataLabels dataLabels = chart.NSeries[0].DataLabels;
   dataLabels.ShowCategoryName = true;
   dataLabels.ShowPercentage = true;
   dataLabels.Position = LabelPositionType.OutsideEnd;
   ```

### Thực hiện các đường dẫn
1. **Bật Đường Dẫn**
   Bật các đường dẫn để có kết nối trực quan rõ ràng hơn:
   ```csharp
   chart.NSeries[0].HasLeaderLines = true;
   ```

2. **Điều chỉnh vị trí nhãn dữ liệu**
   Đảm bảo khả năng hiển thị bằng cách điều chỉnh vị trí nhãn:
   ```csharp
   int DELTA = 100;
   foreach (var point in chart.NSeries[0].Points)
   {
       int X = point.DataLabels.X;
       if (X > 2000) 
           point.DataLabels.X += DELTA;
       else 
           point.DataLabels.X -= DELTA;
   }
   ```

### Lưu biểu đồ và bảng tính
1. **Lưu dưới dạng hình ảnh**
   Kết xuất biểu đồ thành tệp hình ảnh:
   ```csharp
   ImageOrPrintOptions options = new ImageOrPrintOptions { ImageType = Drawing.ImageType.Png, HorizontalResolution = 200, VerticalResolution = 200 };
   chart.ToImage("output_out.png", options);
   ```

2. **Lưu sổ làm việc**
   Lưu bảng tính để xem biểu đồ trong Excel:
   ```csharp
   workbook.Save("output_out.xlsx");
   ```

## Ứng dụng thực tế
- **Báo cáo tài chính**: Thể hiện rõ ràng việc phân bổ ngân sách.
- **Phân tích tiếp thị**: Hình dung dữ liệu thị phần một cách hiệu quả trong các bài thuyết trình hoặc báo cáo.
- **Phân tích bán hàng**Hiển thị phân phối doanh số giữa các khu vực/sản phẩm khác nhau một cách dễ dàng.

Các khả năng tích hợp bao gồm xuất các hình ảnh trực quan này sang ứng dụng web hoặc nhúng chúng vào các công cụ báo cáo tự động.

## Cân nhắc về hiệu suất
Khi sử dụng Aspose.Cells, hãy cân nhắc những điều sau để có hiệu suất tối ưu:
- Giảm thiểu các tập dữ liệu lớn được tải vào bộ nhớ cùng một lúc.
- Sử dụng vòng lặp hiệu quả và tránh các tính toán không cần thiết bên trong vòng lặp.
- Thường xuyên dọn dẹp các tài nguyên như đối tượng sổ làm việc để tránh rò rỉ bộ nhớ.

## Phần kết luận
Bạn đã học cách tạo biểu đồ hình tròn có đường dẫn bằng Aspose.Cells for .NET. Chức năng này giúp tăng cường độ rõ nét của hình ảnh dữ liệu, giúp chúng dễ tiếp cận và có tác động hơn. 

**Các bước tiếp theo:**
Khám phá thêm các tùy chỉnh về giao diện biểu đồ hoặc thử nghiệm các loại biểu đồ khác có sẵn trong Aspose.Cells.

## Phần Câu hỏi thường gặp
1. **Đường dẫn trong biểu đồ hình tròn là gì?**
   Các đường dẫn kết nối các nhãn dữ liệu với các đoạn tương ứng, giúp cải thiện khả năng đọc.

2. **Tôi có thể sử dụng Aspose.Cells miễn phí không?**
   Có, bạn có thể bắt đầu bằng bản dùng thử miễn phí, nhưng để sử dụng đầy đủ tính năng thì cần phải có giấy phép.

3. **Có thể xuất biểu đồ dưới dạng hình ảnh không?**
   Chắc chắn rồi! Sử dụng `ImageOrPrintOptions` để lưu biểu đồ của bạn ở định dạng hình ảnh như PNG hoặc JPEG.

4. **Làm thế nào để điều chỉnh vị trí nhãn dữ liệu theo cách thủ công?**
   Sửa đổi tọa độ X và Y của nhãn dữ liệu trong vòng lặp điểm chuỗi.

5. **Aspose.Cells có thể tích hợp với các hệ thống khác không?**
   Có, có thể sử dụng kết hợp với cơ sở dữ liệu, dịch vụ web và nhiều thứ khác để tạo ra giải pháp báo cáo tự động.

## Tài nguyên
- [Tài liệu Aspose.Cells](https://reference.aspose.com/cells/net/)
- [Tải xuống Aspose.Cells](https://releases.aspose.com/cells/net/)
- [Mua giấy phép](https://purchase.aspose.com/buy)
- [Dùng thử miễn phí](https://releases.aspose.com/cells/net/)
- [Giấy phép tạm thời](https://purchase.aspose.com/temporary-license/)
- [Diễn đàn hỗ trợ](https://forum.aspose.com/c/cells/9)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}