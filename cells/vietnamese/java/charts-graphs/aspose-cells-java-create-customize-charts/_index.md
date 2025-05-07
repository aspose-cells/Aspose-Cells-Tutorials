---
"date": "2025-04-08"
"description": "Hướng dẫn mã cho Aspose.Words Java"
"title": "Aspose.Cells Java&#58; Tạo & Tùy chỉnh Biểu đồ"
"url": "/vi/java/charts-graphs/aspose-cells-java-create-customize-charts/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}


# Làm chủ việc tạo và tùy chỉnh biểu đồ với Aspose.Cells Java

Trong thế giới dữ liệu ngày nay, việc trực quan hóa các tập dữ liệu phức tạp là rất quan trọng để đưa ra quyết định sáng suốt. Cho dù bạn là một nhà phát triển dày dạn kinh nghiệm hay chỉ mới bắt đầu, việc tạo biểu đồ hấp dẫn trong ứng dụng của bạn có thể cải thiện đáng kể trải nghiệm của người dùng. Hướng dẫn này sẽ hướng dẫn bạn quy trình sử dụng Aspose.Cells for Java để tạo và tùy chỉnh biểu đồ một cách dễ dàng.

## Những gì bạn sẽ học được

- Cách thiết lập Aspose.Cells cho Java
- Tạo và đặt tên cho các trang tính
- Điền dữ liệu vào ô
- Thêm một bảng biểu đồ và tạo biểu đồ cột
- Tùy chỉnh biểu đồ của bạn bằng hình ảnh, tiêu đề và cấu hình chuỗi
- Lưu sổ làm việc

Với các bước này, bạn sẽ có thể tạo ra các biểu đồ hấp dẫn về mặt thị giác chỉ trong thời gian ngắn.

## Điều kiện tiên quyết

Trước khi tìm hiểu sâu hơn về Aspose.Cells for Java, hãy đảm bảo bạn có:

- **Bộ phát triển Java (JDK) 8 trở lên** được cài đặt trên máy của bạn.
- Hiểu biết cơ bản về lập trình Java và quen thuộc với các thao tác trong Excel.
  
### Thư viện bắt buộc

Để bắt đầu sử dụng Aspose.Cells, hãy đưa phần phụ thuộc sau vào công cụ quản lý dự án của bạn.

#### Maven
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

#### Tốt nghiệp
```gradle
implementation group: 'com.aspose', name: 'aspose-cells', version: '25.3'
```

### Mua lại giấy phép

Aspose cung cấp bản dùng thử miễn phí, cho phép bạn kiểm tra đầy đủ các tính năng của thư viện trước khi mua. Bạn cũng có thể mua giấy phép tạm thời để thử nghiệm mở rộng.

- **Dùng thử miễn phí**: [Tải xuống miễn phí](https://releases.aspose.com/cells/java/)
- **Giấy phép tạm thời**: [Yêu cầu ở đây](https://purchase.aspose.com/temporary-license/)

## Thiết lập Aspose.Cells cho Java

Khi bạn đã có môi trường sẵn sàng, hãy khởi tạo thư viện bằng cách tạo một thư viện mới `Workbook` Ví dụ. Đây sẽ là nền tảng cho hành trình tạo biểu đồ của chúng ta.

```java
import com.aspose.cells.Workbook;

// Khởi tạo một Workbook mới
Workbook workbook = new Workbook();
```

## Hướng dẫn thực hiện

### 1. Tạo và đặt tên cho một trang tính

#### Tổng quan
Bắt đầu bằng cách thiết lập bảng dữ liệu, bảng này sẽ lưu trữ tất cả dữ liệu cần thiết cho biểu đồ.

#### Các bước thực hiện:

**Tạo một Workbook mới**
```java
import com.aspose.cells.Worksheet;

// Tạo một phiên bản Workbook mới
Workbook workbook = new Workbook();
```

**Đặt tên cho bảng tính**

```java
// Truy cập vào bảng tính đầu tiên và đặt tên cho nó là "Dữ liệu"
Worksheet sheet = workbook.getWorksheets().get(0);
sheet.setName("Data");
```

### 2. Điền dữ liệu vào ô

#### Tổng quan
Việc điền dữ liệu vào bảng tính là điều cần thiết để tạo ra các biểu đồ có ý nghĩa.

#### Các bước thực hiện:

**Truy cập Bộ sưu tập tế bào**

```java
import com.aspose.cells.Cells;

// Lấy bộ sưu tập tế bào từ trang tính "Dữ liệu"
Cells cells = sheet.getCells();
```

**Chèn dữ liệu**

```java
// Chèn tên khu vực và số liệu bán hàng
cells.get("A1").putValue("Region");
cells.get("B1").putValue("Sale");

String[] regions = {"France", "Germany", "England", "Sweden", "Italy", "Spain", "Portugal"};
int[] sales = {70000, 55000, 30000, 40000, 35000, 32000, 10000};

for (int i = 0; i < regions.length; i++) {
    cells.get("A" + (i+2)).putValue(regions[i]);
    cells.get("B" + (i+2)).putValue(sales[i]);
}
```

### 3. Thêm một bảng biểu đồ

#### Tổng quan
Thêm một bảng biểu đồ chuyên dụng để tách biệt dữ liệu và hình ảnh trực quan.

#### Các bước thực hiện:

**Tạo bảng biểu đồ**

```java
import com.aspose.cells.SheetType;

// Thêm một bảng biểu đồ mới
int sheetIndex = workbook.getWorksheets().add(SheetType.CHART);
Worksheet chartSheet = workbook.getWorksheets().get(sheetIndex);

// Đặt tên cho bảng tính là "Biểu đồ"
chartSheet.setName("Chart");
```

### 4. Tạo biểu đồ

#### Tổng quan
Tạo biểu đồ cột để trực quan hóa dữ liệu bán hàng theo khu vực.

#### Các bước thực hiện:

**Tạo biểu đồ cột**

```java
import com.aspose.cells.Chart;
import com.aspose.cells.ChartType;

// Thêm biểu đồ cột mới vào trang tính "Biểu đồ"
int chartIndex = chartSheet.getCharts().add(ChartType.COLUMN, 1, 1, 25, 10);
Chart chart = chartSheet.getCharts().get(chartIndex);
```

### 5. Đặt hình ảnh làm nền điền vào vùng vẽ biểu đồ

#### Tổng quan
Tăng tính hấp dẫn trực quan cho biểu đồ của bạn bằng cách thêm hình ảnh nền.

#### Các bước thực hiện:

**Đặt dữ liệu hình ảnh**

```java
import java.io.FileInputStream;
import com.aspose.cells.Color;

String dataDir = "YOUR_DATA_DIRECTORY";
File file = new FileInputStream(dataDir + "aspose-logo.png");
byte[] data = new byte[(int)file.length()];
file.read(data);

chart.getPlotArea().getArea().getFillFormat().setImageData(data);
chart.getPlotArea().getBorder().setVisible(false);
```

### 6. Cấu hình Tiêu đề và Chuỗi Biểu đồ

#### Tổng quan
Tùy chỉnh biểu đồ của bạn bằng tiêu đề, dữ liệu chuỗi và vị trí chú giải.

#### Các bước thực hiện:

**Đặt tiêu đề biểu đồ**

```java
// Cấu hình thuộc tính tiêu đề của biểu đồ
chart.getTitle().setText("Sales By Region");
chart.getTitle().getFont().setColor(Color.getBlue());
chart.getTitle().getFont().setBold(true);
chart.getTitle().getFont().setSize(12);
```

**Cấu hình dữ liệu chuỗi**

```java
// Đặt dữ liệu chuỗi và danh mục cho biểu đồ
chart.getNSeries().add("Data!B2:B8", true);
chart.getNSeries().setCategoryData("Data!A2:A8");
chart.getNSeries().setColorVaried(true);

// Đặt chú giải ở đầu biểu đồ
import com.aspose.cells.Legend;
import com.aspose.cells.LegendPositionType;

Legend legend = chart.getLegend();
legend.setPosition(LegendPositionType.TOP);
```

### 7. Lưu sổ làm việc

#### Tổng quan
Đảm bảo mọi công sức của bạn được lưu lại bằng cách xuất bảng tính.

#### Các bước thực hiện:

**Lưu sổ làm việc**

```java
String outDir = "YOUR_OUTPUT_DIRECTORY";
workbook.save(outDir + "SPAsBFillInChart_out.xls");
```

## Ứng dụng thực tế

- **Báo cáo kinh doanh**: Tạo báo cáo hiệu suất và doanh số năng động.
- **Công cụ phân tích dữ liệu**: Nâng cao khả năng trực quan hóa dữ liệu trong phần mềm phân tích.
- **Tích hợp bảng điều khiển**: Tích hợp biểu đồ vào bảng thông tin để cập nhật theo thời gian thực.

## Cân nhắc về hiệu suất

- Tối ưu hóa bằng cách giảm thiểu số lượng thao tác trên các tập dữ liệu lớn.
- Quản lý bộ nhớ hiệu quả bằng cách loại bỏ ngay những đối tượng không sử dụng.

## Phần kết luận

Bây giờ bạn đã thành thạo việc tạo và tùy chỉnh biểu đồ bằng Aspose.Cells trong Java. Để tiếp tục hành trình của mình, hãy khám phá thêm các tính năng như phạm vi dữ liệu động hoặc các loại biểu đồ khác nhau. 

## Phần Câu hỏi thường gặp

1. **Làm thế nào để thêm nhiều chuỗi vào biểu đồ?**
   - Sử dụng `add` phương pháp trên `NSeries` với nhiều phạm vi.

2. **Tôi có thể tùy chỉnh nhãn trục của biểu đồ không?**
   - Có, truy cập và cấu hình các trục bằng cách sử dụng `chart.getCateghoặcyAxis()` or `chart.getValueAxis()`.

3. **Phải làm sao nếu tệp hình ảnh của tôi không hiển thị đúng trong vùng vẽ?**
   - Đảm bảo đường dẫn tệp là chính xác và định dạng hình ảnh được Aspose.Cells hỗ trợ.

4. **Làm thế nào để xử lý các tập dữ liệu lớn một cách hiệu quả?**
   - Hãy cân nhắc việc đọc dữ liệu theo từng phần và cập nhật các ô theo từng bước.

5. **Có thể xuất biểu đồ sang các định dạng khác như PDF hoặc PNG không?**
   - Có, sử dụng `workbook.save()` với phần mở rộng tệp phù hợp cho các định dạng khác nhau.

## Tài nguyên

- [Tài liệu Aspose.Cells](https://reference.aspose.com/cells/java/)
- [Tải xuống Aspose.Cells](https://releases.aspose.com/cells/java/)
- [Mua giấy phép](https://purchase.aspose.com/buy)
- [Dùng thử miễn phí](https://releases.aspose.com/cells/java/)
- [Yêu cầu cấp giấy phép tạm thời](https://purchase.aspose.com/temporary-license/)
- [Diễn đàn hỗ trợ](https://forum.aspose.com/c/cells/9)

Bằng cách làm theo hướng dẫn này, bạn sẽ có thể dễ dàng tạo và tùy chỉnh biểu đồ trong các ứng dụng Java bằng Aspose.Cells. Chúc bạn viết mã vui vẻ!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}