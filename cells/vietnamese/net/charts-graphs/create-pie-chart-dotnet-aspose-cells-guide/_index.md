---
"date": "2025-04-05"
"description": "Hướng dẫn mã cho Aspose.Cells Net"
"title": "Tạo biểu đồ hình tròn trong .NET với Aspose.Cells&#58; Hướng dẫn đầy đủ"
"url": "/vi/net/charts-graphs/create-pie-chart-dotnet-aspose-cells-guide/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# Cách tạo biểu đồ hình tròn trong .NET bằng Aspose.Cells: Hướng dẫn từng bước

## Giới thiệu

Tạo biểu diễn trực quan của dữ liệu là một kỹ năng thiết yếu, đặc biệt là khi cố gắng truyền đạt thông tin phức tạp một cách đơn giản và hiệu quả. Cho dù bạn đang làm báo cáo kinh doanh hay phân tích số liệu thống kê nhân khẩu học, biểu đồ hình tròn cung cấp một cách trực tiếp để minh họa các phần của tổng thể. Hướng dẫn này sẽ hướng dẫn bạn quy trình tạo biểu đồ hình tròn trong .NET bằng Aspose.Cells—một thư viện mạnh mẽ giúp đơn giản hóa việc làm việc với các tài liệu Excel theo chương trình.

**Những gì bạn sẽ học được:**
- Cách khởi tạo và thiết lập bảng tính Excel.
- Điền dữ liệu vào các ô của bảng tính để trực quan hóa.
- Tạo và cấu hình biểu đồ hình tròn bằng Aspose.Cells cho .NET.
- Tùy chỉnh màu sắc của lát cắt trong biểu đồ hình tròn để tăng tính hấp dẫn về mặt thị giác.
- Tự động điều chỉnh các cột và lưu bảng tính của bạn.

Hãy cùng tìm hiểu cách bạn có thể tận dụng Aspose.Cells để tạo biểu đồ hình tròn hấp dẫn một cách dễ dàng. Trước khi bắt đầu, hãy đảm bảo bạn đáp ứng các điều kiện tiên quyết để có thể thực hiện suôn sẻ.

## Điều kiện tiên quyết

Để bắt đầu với hướng dẫn này, hãy đảm bảo bạn có:

- **Thư viện cần thiết:** Bạn sẽ cần thư viện Aspose.Cells cho .NET. Đảm bảo dự án của bạn được thiết lập để sử dụng thư viện này.
- **Yêu cầu thiết lập môi trường:** Một môi trường phát triển phù hợp như Visual Studio được cài đặt trên hệ thống của bạn.
- **Điều kiện tiên quyết về kiến thức:** Hiểu biết cơ bản về lập trình C# và quen thuộc với cấu trúc tài liệu Excel.

## Thiết lập Aspose.Cells cho .NET

Trước khi bắt đầu viết code, bạn cần cài đặt thư viện Aspose.Cells vào dự án của mình. Cách thực hiện như sau:

### Cài đặt thông qua CLI
Mở terminal hoặc dấu nhắc lệnh và chạy:
```bash
dotnet add package Aspose.Cells
```

### Cài đặt thông qua Trình quản lý gói
Nếu bạn đang sử dụng Visual Studio, hãy mở NuGet Package Manager Console và thực hiện:
```powershell
PM> Install-Package Aspose.Cells
```

#### Các bước xin cấp giấy phép
Bạn có thể bắt đầu bằng bản dùng thử miễn phí để đánh giá Aspose.Cells. Để sử dụng lâu dài, hãy cân nhắc việc mua giấy phép tạm thời hoặc mua trực tiếp từ trang web của họ.

#### Khởi tạo và thiết lập cơ bản

Để khởi tạo thư viện trong dự án C# của bạn:
```csharp
using Aspose.Cells;

// Tạo một thể hiện của lớp Workbook
Workbook workbook = new Workbook();
```

Thiết lập cơ bản này cho phép bạn bắt đầu làm việc với các tệp Excel theo chương trình.

## Hướng dẫn thực hiện

### Tính năng 1: Khởi tạo Workbook và Worksheet

**Tổng quan:** Tính năng này thiết lập một bảng tính mới và truy cập vào trang tính đầu tiên của bảng tính đó, chuẩn bị giai đoạn nhập dữ liệu và tạo biểu đồ.

#### Khởi tạo từng bước
```csharp
using Aspose.Cells;

class InitializeWorkbook {
    public void Run() {
        // Tạo một đối tượng sổ làm việc mới
        Workbook workbook = new Workbook();
        
        // Truy cập trang tính đầu tiên trong sổ làm việc
        Worksheet worksheet = workbook.Worksheets[0];
    }
}
```
Đây, `Workbook` đại diện cho một tập tin Excel và truy cập `Worksheets[0]` cung cấp cho bạn trang tính đầu tiên.

### Tính năng 2: Điền dữ liệu cho biểu đồ hình tròn

**Tổng quan:** Việc điền dữ liệu rất quan trọng vì nó tạo thành cơ sở cho biểu đồ của bạn. Bước này bao gồm việc nhập tên quốc gia và tỷ lệ phần trăm dân số thế giới tương ứng vào các ô cụ thể.

#### Dữ liệu từng bước
```csharp
using Aspose.Cells;

class PopulateData {
    public void Run() {
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];
        
        // Nhập dữ liệu quốc gia vào cột C
        worksheet.Cells["C3"].PutValue("India");
        worksheet.Cells["C4"].PutValue("China");
        worksheet.Cells["C5"].PutValue("United States");
        worksheet.Cells["C6"].PutValue("Russia");
        worksheet.Cells["C7"].PutValue("United Kingdom");
        worksheet.Cells["C8"].PutValue("Others");

        // Nhập dữ liệu phần trăm vào cột D
        worksheet.Cells["D2"].PutValue("% of world population");
        worksheet.Cells["D3"].PutValue(25);
        worksheet.Cells["D4"].PutValue(30);
        worksheet.Cells["D5"].PutValue(10);
        worksheet.Cells["D6"].PutValue(13);
        worksheet.Cells["D7"].PutValue(9);
        worksheet.Cells["D8"].PutValue(13);
    }
}
```
Bước này đảm bảo dữ liệu của bạn đã sẵn sàng để trực quan hóa.

### Tính năng 3: Tạo và cấu hình biểu đồ hình tròn

**Tổng quan:** Tính năng này bao gồm việc tạo biểu đồ hình tròn, thiết lập dữ liệu chuỗi và cấu hình nhiều thuộc tính khác nhau như vị trí tiêu đề và chú thích.

#### Tạo biểu đồ hình tròn từng bước
```csharp
using Aspose.Cells;
using Aspose.Cells.Charts;

class CreatePieChart {
    public void Run() {
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];
        
        // Thêm biểu đồ hình tròn vào bảng tính
        int pieIdx = worksheet.Charts.Add(ChartType.Pie, 1, 6, 15, 14);
        Chart pie = worksheet.Charts[pieIdx];

        // Đặt chuỗi dữ liệu cho biểu đồ
        pie.NSeries.Add("D3:D8", true);

        // Xác định dữ liệu danh mục và cấu hình tiêu đề
        pie.NSeries.CategoryData = "=Sheet1!$C$3:$C$8";
        pie.Title.LinkedSource = "D2";
        pie.Legend.Position = LegendPositionType.Bottom;
        pie.Title.Font.Name = "Calibri";
        pie.Title.Font.Size = 18;
    }
}
```
Mã này tạo ra biểu đồ hấp dẫn về mặt thị giác được liên kết với dữ liệu của bạn.

### Tính năng 4: Tùy chỉnh màu lát cắt trong biểu đồ hình tròn

**Tổng quan:** Cá nhân hóa giao diện của từng lát cắt giúp tăng khả năng đọc và tính thẩm mỹ. Bước này bao gồm việc chỉ định màu sắc riêng cho các lát cắt khác nhau.

#### Tùy chỉnh màu sắc từng bước
```csharp
using Aspose.Cells;
using Aspose.Cells.Charts;
using System.Drawing;

class CustomizeSliceColors {
    public void Run() {
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        int pieIdx = worksheet.Charts.Add(ChartType.Pie, 1, 6, 15, 14);
        Chart pie = worksheet.Charts[pieIdx];
        
        Series srs = pie.NSeries[0];

        // Gán màu tùy chỉnh cho từng lát cắt
        srs.Points[0].Area.ForegroundColor = Color.FromArgb(0, 246, 22, 219);
        srs.Points[1].Area.ForegroundColor = Color.FromArgb(0, 51, 34, 84);
        srs.Points[2].Area.ForegroundColor = Color.FromArgb(0, 46, 74, 44);
        srs.Points[3].Area.ForegroundColor = Color.FromArgb(0, 19, 99, 44);
        srs.Points[4].Area.ForegroundColor = Color.FromArgb(0, 208, 223, 7);
        srs.Points[5].Area.ForegroundColor = Color.FromArgb(0, 222, 69, 8);
    }
}
```
Bước này sẽ thêm nét sống động cho biểu đồ của bạn.

### Tính năng 5: Tự động điều chỉnh cột và lưu sổ làm việc

**Tổng quan:** Các bước cuối cùng bao gồm điều chỉnh độ rộng cột để hiển thị dữ liệu tốt hơn và lưu bảng tính ở định dạng Excel.

#### Điều chỉnh và lưu cột từng bước
```csharp
using Aspose.Cells;

class SaveWorkbook {
    public void Run() {
        string outputDir = "YOUR_OUTPUT_DIRECTORY";
        
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];
        
        // Tự động điều chỉnh các cột cho phù hợp với nội dung
        worksheet.AutoFitColumns();

        // Lưu sổ làm việc dưới dạng tệp Excel
        workbook.Save(outputDir + "outputCustomSliceSectorColorsPieChart.xlsx", SaveFormat.Xlsx);
    }
}
```
Điều này đảm bảo tài liệu cuối cùng của bạn được chỉnh sửa và sẵn sàng để trình bày.

## Ứng dụng thực tế

- **Báo cáo kinh doanh:** Sử dụng biểu đồ hình tròn để mô tả phân phối doanh số theo khu vực.
- **Nghiên cứu nhân khẩu học:** Hình dung dữ liệu dân số ở nhiều quốc gia hoặc khu vực khác nhau.
- **Công cụ giáo dục:** Tạo phương tiện hỗ trợ trực quan hấp dẫn cho sinh viên trong các khóa học thống kê.
- **Phân tích chăm sóc sức khỏe:** Hiển thị phân bố dữ liệu bệnh nhân trong các cơ sở chăm sóc sức khỏe.

## Cân nhắc về hiệu suất

Để đảm bảo hiệu suất tối ưu khi sử dụng Aspose.Cells, hãy cân nhắc những điều sau:

- **Xử lý dữ liệu hiệu quả:** Quản lý các tập dữ liệu lớn bằng cách xử lý chúng thành từng phần nếu cần.
- **Quản lý bộ nhớ:** Xử lý các đối tượng đúng cách để giải phóng tài nguyên và tránh rò rỉ bộ nhớ.
- **Cấu hình biểu đồ được tối ưu hóa:** Giảm thiểu các phép tính hoặc kết xuất phức tạp trong quá trình tạo biểu đồ để có hiệu suất nhanh hơn.

## Phần kết luận

Bây giờ bạn đã học cách tạo biểu đồ hình tròn trong .NET bằng Aspose.Cells. Thư viện mạnh mẽ này đơn giản hóa thao tác tài liệu Excel, cho phép bạn tập trung vào phân tích dữ liệu thay vì sự phức tạp của việc xử lý tệp. Thử nghiệm với các loại biểu đồ và tùy chọn tùy chỉnh khác nhau có sẵn trong Aspose.Cells để cải thiện hơn nữa các ứng dụng của bạn.

**Các bước tiếp theo:**
- Khám phá các loại biểu đồ khác như biểu đồ thanh hoặc biểu đồ đường.
- Tích hợp các chức năng của Aspose.Cells vào các dự án .NET lớn hơn để tạo báo cáo tự động.

Sẵn sàng đưa kỹ năng trực quan hóa dữ liệu của bạn lên một tầm cao mới? Hãy khám phá sâu hơn bằng cách khám phá thêm nhiều tính năng của Aspose.Cells và bắt đầu triển khai chúng vào các dự án của bạn ngay hôm nay!

## Phần Câu hỏi thường gặp

1. **Aspose.Cells được sử dụng để làm gì?**
   - Đây là thư viện dùng để quản lý các tệp Excel theo chương trình, cho phép bạn tạo, sửa đổi và phân tích bảng tính.

2. **Tôi có thể sử dụng Aspose.Cells mà không cần giấy phép không?**
   - Có, nhưng có giới hạn. Bản dùng thử miễn phí hoặc giấy phép tạm thời cho phép truy cập đầy đủ vào các tính năng.

3. **Làm thế nào để tùy chỉnh thêm giao diện biểu đồ hình tròn của tôi?**
   - Sử dụng các thuộc tính bổ sung như `pie.NSeries[0].Area.Formatting` để kiểm soát tính thẩm mỹ tốt hơn.

4. **Một số vấn đề thường gặp khi tạo biểu đồ trong Aspose.Cells là gì?**
   - Đảm bảo phạm vi dữ liệu được chỉ định chính xác và bạn đã cấu hình tất cả các thuộc tính biểu đồ cần thiết trước khi kết xuất.

5. **Làm thế nào tôi có thể tích hợp Aspose.Cells với các thư viện .NET khác?**
   - Sử dụng Aspose.Cells như một phần của giải pháp .NET lớn hơn, tận dụng khả năng của nó cùng với các thư viện khác để tạo ra các ứng dụng toàn diện.

## Tài nguyên

- **Tài liệu:** [Tài liệu Aspose.Cells](https://reference.aspose.com/cells/net/)
- **Tải xuống:** [Aspose.Cells phát hành](https://releases.aspose.com/cells/net/)
- **Mua:** [Mua Aspose.Cells](https://purchase.aspose.com/buy)
- **Dùng thử miễn phí:** [Dùng thử miễn phí Aspose.Cells](https://releases.aspose.com/cells/net/)
- **Giấy phép tạm thời:** [Xin giấy phép tạm thời](https://purchase.aspose.com/temporary-license/)
- **Ủng hộ:** [Diễn đàn Aspose](https://forum.aspose.com/c/cells/9)

Bằng cách làm theo hướng dẫn này, giờ đây bạn đã có thể tạo biểu đồ hình tròn hấp dẫn về mặt thị giác trong các ứng dụng .NET bằng Aspose.Cells. Chúc bạn viết mã vui vẻ!

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}