---
date: '2026-04-08'
description: Học cách tạo biểu đồ cột trong Java bằng Aspose.Cells, bao gồm tạo biểu
  đồ Java, thêm trang biểu đồ và xuất workbook Excel.
keywords:
- generate column chart
- create chart java
- add chart sheet
- populate excel cells
- set chart title
- export workbook excel
title: Tạo biểu đồ cột với hướng dẫn Aspose.Cells Java
url: /vi/java/charts-graphs/aspose-cells-java-create-customize-charts/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Tạo biểu đồ cột với Aspose.Cells Java

Trong các ứng dụng dựa trên dữ liệu ngày nay, **việc generate column chart** nhanh chóng và lập trình có thể biến các con số thô thành những hiểu biết trực quan rõ ràng. Dù bạn đang xây dựng một bảng điều khiển báo cáo, một công cụ phân tích, hay một tính năng xuất đơn giản, Aspose.Cells cho Java cung cấp cho bạn một API mượt mà để **create chart java** mà không cần thao tác với giao diện Excel. Trong hướng dẫn này, bạn sẽ học cách cài đặt thư viện, **populate Excel cells**, thêm một **chart sheet**, tùy chỉnh **chart title**, và cuối cùng **export workbook excel** ra một tệp.

## Câu trả lời nhanh
- **“generate column chart” có nghĩa là gì?** Nó tạo ra một biểu đồ dạng thanh dọc từ dữ liệu dạng bảng.  
- **Thư viện nào được yêu cầu?** Aspose.Cells for Java (free trial available).  
- **Có cần cài đặt Excel không?** Không, thư viện hoạt động độc lập với Microsoft Excel.  
- **Có thể xuất sang các định dạng khác ngoài XLS không?** Có – PDF, PNG, SVG, v.v., qua `workbook.save()`.  
- **Giấy phép có bắt buộc cho môi trường sản xuất không?** Có, cần giấy phép mua hoặc tạm thời.

## Biểu đồ cột là gì?
Biểu đồ cột hiển thị các chuỗi dữ liệu dưới dạng các thanh dọc, giúp dễ dàng so sánh giá trị giữa các danh mục như khu vực, tháng hoặc dòng sản phẩm. Aspose.Cells cho phép bạn xây dựng biểu đồ này hoàn toàn bằng mã, cung cấp kiểm soát đầy đủ đối với dữ liệu, kiểu dáng và định dạng xuất.

## Tại sao nên sử dụng Aspose.Cells để tạo chart java?
- **No COM interop** – hoạt động trên bất kỳ hệ điều hành nào có JVM.  
- **Rich styling options** – hình ảnh, gradient, chú giải và phông chữ tùy chỉnh.  
- **High performance** – phù hợp với bộ dữ liệu lớn.  
- **Multiple export formats** – XLS, XLSX, PDF, PNG và hơn nữa.

## Yêu cầu trước
- **Java Development Kit (JDK) 8+** đã được cài đặt.  
- Kiến thức cơ bản về Java và hiểu biết về các khái niệm Excel.  

### Thư viện cần thiết
Thêm Aspose.Cells vào dự án của bạn bằng một trong các đoạn mã dưới đây.

#### Maven
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

#### Gradle
```gradle
implementation group: 'com.aspose', name: 'aspose-cells', version: '25.3'
```

### Nhận giấy phép
Aspose cung cấp bản dùng thử miễn phí và giấy phép tạm thời cho việc thử nghiệm mở rộng.

- **Bản dùng thử miễn phí**: [Download Free](https://releases.aspose.com/cells/java/)  
- **Giấy phép tạm thời**: [Request Here](https://purchase.aspose.com/temporary-license/)

## Cài đặt Aspose.Cells cho Java

Đầu tiên, tạo một thể hiện `Workbook` – đây sẽ là canvas cho dữ liệu và biểu đồ của chúng ta.

```java
import com.aspose.cells.Workbook;

// Initialize a new Workbook
Workbook workbook = new Workbook();
```

## Hướng dẫn từng bước

### 1. Tạo và đặt tên cho Worksheet
Chúng ta sẽ lưu dữ liệu thô trong một sheet có tên **Data**.

```java
import com.aspose.cells.Worksheet;

// Create a new Workbook instance
Workbook workbook = new Workbook();
```

```java
// Access the first worksheet and set its name to "Data"
Worksheet sheet = workbook.getWorksheets().get(0);
sheet.setName("Data");
```

### 2. Điền dữ liệu vào các ô Excel
Chèn tên khu vực và số liệu bán hàng mà biểu đồ cột sẽ hiển thị.

```java
import com.aspose.cells.Cells;

// Get the cells collection from the "Data" sheet
Cells cells = sheet.getCells();
```

```java
// Insert region names and sales figures
cells.get("A1").putValue("Region");
cells.get("B1").putValue("Sale");

String[] regions = {"France", "Germany", "England", "Sweden", "Italy", "Spain", "Portugal"};
int[] sales = {70000, 55000, 30000, 40000, 35000, 32000, 10000};

for (int i = 0; i < regions.length; i++) {
    cells.get("A" + (i+2)).putValue(regions[i]);
    cells.get("B" + (i+2)).putValue(sales[i]);
}
```

### 3. Thêm Chart Sheet
Tách biểu đồ ra khỏi dữ liệu thô giúp workbook gọn gàng hơn.

```java
import com.aspose.cells.SheetType;

// Add a new chart sheet
int sheetIndex = workbook.getWorksheets().add(SheetType.CHART);
Worksheet chartSheet = workbook.getWorksheets().get(sheetIndex);

// Name the worksheet "Chart"
chartSheet.setName("Chart");
```

### 4. Tạo biểu đồ cột
Bây giờ chúng ta thực sự **generate column chart** các đối tượng.

```java
import com.aspose.cells.Chart;
import com.aspose.cells.ChartType;

// Add a new column chart to the "Chart" sheet
int chartIndex = chartSheet.getCharts().add(ChartType.COLUMN, 1, 1, 25, 10);
Chart chart = chartSheet.getCharts().get(chartIndex);
```

### 5. Đặt hình ảnh làm nền trong vùng vẽ
Một hình nền có thể làm cho biểu đồ nổi bật hơn.

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

### 6. Đặt tiêu đề biểu đồ
Tùy chỉnh **set chart title** giúp tăng khả năng đọc hiểu.

```java
// Configure the chart's title properties
chart.getTitle().setText("Sales By Region");
chart.getTitle().getFont().setColor(Color.getBlue());
chart.getTitle().getFont().setBold(true);
chart.getTitle().getFont().setSize(12);
```

### 7. Cấu hình dữ liệu series và chú giải
Liên kết phạm vi dữ liệu với biểu đồ và đặt vị trí cho chú giải.

```java
// Set series and category data for the chart
chart.getNSeries().add("Data!B2:B8", true);
chart.getNSeries().setCategoryData("Data!A2:A8");
chart.getNSeries().setColorVaried(true);

// Position the legend at the top of the chart
import com.aspose.cells.Legend;
import com.aspose.cells.LegendPositionType;

Legend legend = chart.getLegend();
legend.setPosition(LegendPositionType.TOP);
```

### 8. Xuất Workbook Excel
Cuối cùng, **export workbook excel** ra một tệp XLS (hoặc bất kỳ định dạng hỗ trợ nào).

```java
String outDir = "YOUR_OUTPUT_DIRECTORY";
workbook.save(outDir + "SPAsBFillInChart_out.xls");
```

## Ứng dụng thực tiễn
- **Business Reports** – Tự động tạo biểu đồ bán hàng cho các PDF hàng tháng.  
- **Data Analysis Tools** – Nhúng biểu đồ động vào các bảng điều khiển phân tích tùy chỉnh.  
- **Enterprise Dashboards** – Làm mới hình ảnh biểu đồ ngay lập tức cho việc giám sát thời gian thực.

## Các cân nhắc về hiệu năng
- Cập nhật ô theo lô khi làm việc với bộ dữ liệu lớn để giảm tải.  
- Giải phóng tài nguyên (`workbook.dispose()`) nếu bạn xử lý nhiều workbook trong vòng lặp.  

## Các vấn đề thường gặp và giải pháp
- **Image not showing** – Kiểm tra đường dẫn tệp và đảm bảo định dạng ảnh (PNG, JPEG) được hỗ trợ.  
- **Chart appears blank** – Đảm bảo các tham chiếu phạm vi dữ liệu (`Data!B2:B8`) khớp với các ô đã được điền.  
- **Out‑of‑memory errors** – Xử lý dữ liệu theo khối và gọi `System.gc()` sau các lần lưu lớn.

## Câu hỏi thường gặp

**Q: Làm thế nào để thêm nhiều series vào một biểu đồ cột?**  
A: Gọi `chart.getNSeries().add()` liên tục với các phạm vi dữ liệu khác nhau, ví dụ, `"Data!C2:C8"` cho series thứ hai.

**Q: Tôi có thể thay đổi nhãn trục không?**  
A: Có. Sử dụng `chart.getCategoryAxis().setTitle("Regions")` và `chart.getValueAxis().setTitle("Sales")`.

**Q: Những định dạng nào tôi có thể xuất ngoài XLS?**  
A: Dùng `workbook.save("chart.pdf")`, `workbook.save("chart.png")`, hoặc `workbook.save("chart.xlsx")` cho PDF, PNG và XLSX tương ứng.

**Q: Giấy phép có bắt buộc cho bản build phát triển không?**  
A: Bản dùng thử miễn phí đủ cho việc đánh giá, nhưng cần giấy phép vĩnh viễn hoặc tạm thời cho triển khai sản xuất.

**Q: Làm sao cải thiện tốc độ render cho hàng nghìn dòng?**  
A: Điền ô bằng `cells.importArray()` và giảm việc vẽ lại biểu đồ bằng cách tạo biểu đồ sau khi đã tải hết dữ liệu.

---

**Cập nhật lần cuối:** 2026-04-08  
**Đã kiểm tra với:** Aspose.Cells 25.3 for Java  
**Tác giả:** Aspose  

## Tài nguyên

- [Tài liệu Aspose.Cells](https://reference.aspose.com/cells/java/)
- [Tải xuống Aspose.Cells](https://releases.aspose.com/cells/java/)
- [Mua giấy phép](https://purchase.aspose.com/buy)
- [Bản dùng thử miễn phí](https://releases.aspose.com/cells/java/)
- [Yêu cầu giấy phép tạm thời](https://purchase.aspose.com/temporary-license/)
- [Diễn đàn hỗ trợ](https://forum.aspose.com/c/cells/9)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}