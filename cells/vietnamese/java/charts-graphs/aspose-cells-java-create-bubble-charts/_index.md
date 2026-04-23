---
date: '2026-04-02'
description: Học cách tạo biểu đồ và tạo biểu đồ bong bóng Excel bằng Aspose.Cells
  cho Java. Hướng dẫn này sẽ đưa bạn qua quá trình cài đặt, dữ liệu và lưu biểu đồ.
keywords:
- how to create chart
- generate excel bubble chart
- set bubble chart data
title: 'Cách tạo biểu đồ: Biểu đồ bong bóng Excel bằng Aspose.Cells Java'
url: /vi/java/charts-graphs/aspose-cells-java-create-bubble-charts/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Cách Tạo Biểu Đồ: Biểu Đồ Bong Bóng Excel với Aspose.Cells Java

Nâng cao các báo cáo Excel của bạn bằng các biểu đồ bong bóng động sử dụng Aspose.Cells cho Java. Trong hướng dẫn này, bạn sẽ học **cách tạo biểu đồ** dưới dạng các đối tượng hiển thị dữ liệu dưới dạng biểu đồ bong bóng, giúp bản trình bày của bạn trở nên sâu sắc và tương tác hơn. Chúng tôi sẽ hướng dẫn từng bước — từ việc thiết lập môi trường phát triển đến cấu hình dữ liệu biểu đồ và cuối cùng là lưu workbook.

## Câu Hỏi Nhanh
- **Thư viện nào là tốt nhất cho biểu đồ Excel trong Java?** Aspose.Cells cho Java.  
- **Tôi có thể tạo biểu đồ bong bóng Excel bằng chương trình không?** Có, sử dụng API biểu đồ được trình bày bên dưới.  
- **Có cần giấy phép để chạy mã không?** Bản dùng thử miễn phí hoạt động, nhưng giấy phép đầy đủ sẽ mở khóa tất cả tính năng.  
- **Các công cụ xây dựng Java nào được hỗ trợ?** Maven và Gradle đều được hỗ trợ.  
- **Phương thức chính để đặt dữ liệu biểu đồ bong bóng là gì?** Sử dụng `setBubbleSizes`, `setXValues` và `setValues` trên series.

## Biểu Đồ Bong Bóng Là Gì?
Biểu đồ bong bóng là một biến thể của biểu đồ phân tán, trong đó mỗi điểm dữ liệu được biểu diễn bằng một bong bóng. Trục X và trục Y xác định vị trí, trong khi kích thước bong bóng truyền tải một chiều thông tin thứ ba — rất phù hợp để trực quan hoá dữ liệu tài chính, bán hàng hoặc khoa học.

## Tại Sao Nên Sử Dụng Aspose.Cells cho Java?
- **Động cơ Excel không cần cài đặt** – không cần Microsoft Office trên máy chủ.  
- **API biểu đồ phong phú** – hỗ trợ mọi loại biểu đồ hiện đại, bao gồm cả biểu đồ bong bóng.  
- **Đa nền tảng** – hoạt động trên Windows, Linux và macOS.  
- **Hiệu năng cao** – tối ưu cho tập dữ liệu lớn và việc tạo báo cáo khối lượng cao.

## Điều Kiện Tiên Quyết
Để tạo biểu đồ bong bóng bằng Aspose.Cells cho Java, hãy đảm bảo bạn đáp ứng các yêu cầu sau:

### Thư Viện và Phụ Thuộc Cần Thiết
- **Aspose.Cells cho Java**: Cài đặt phiên bản mới nhất (ví dụ: 25.3).

### Yêu Cầu Thiết Lập Môi Trường
- JDK (Java Development Kit) tương thích đã được cài đặt.  
- Cấu hình dự án để sử dụng Maven hoặc Gradle.

### Kiến Thức Tiên Quyết
- Hiểu biết cơ bản về lập trình Java.  
- Quen thuộc với cấu trúc file Excel và các loại biểu đồ.

## Cài Đặt Aspose.Cells cho Java
Việc thiết lập môi trường là rất quan trọng. Dưới đây là cách bắt đầu:

### Cài Đặt qua Maven
Thêm phụ thuộc sau vào file `pom.xml` của bạn:
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

### Cài Đặt qua Gradle
Đối với những người dùng Gradle, thêm đoạn này vào file `build.gradle`:
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

### Mua Giấy Phép
Aspose.Cells cung cấp bản dùng thử miễn phí với chức năng hạn chế. Để có đầy đủ khả năng:
- **Mua**: Truy cập [trang mua](https://purchase.aspose.com/buy) để xem các tùy chọn cấp phép.  
- **Giấy phép tạm thời**: Nhận giấy phép tạm thời từ [đây](https://purchase.aspose.com/temporary-license/) để thử nghiệm đầy đủ.

### Khởi Tạo Cơ Bản
Trước khi sử dụng Aspose.Cells, hãy khởi tạo nó trong dự án Java của bạn:
```java
import com.aspose.cells.Workbook;

// Initialize a new Workbook object
Workbook workbook = new Workbook();
```

## Hướng Dẫn Thực Hiện
Hãy cùng phân tích quy trình tạo và cấu hình biểu đồ bong bóng với Aspose.Cells.

### Cách Tạo Biểu Đồ: Khởi Tạo Đối Tượng Workbook
`Workbook` đại diện cho toàn bộ file Excel, cho phép bạn thao tác với các sheet, ô và nhiều hơn nữa. Khởi tạo như sau:
```java
import com.aspose.cells.Workbook;

// Create a new Workbook instance
Workbook workbook = new Workbook();
```

### Cách Đặt Dữ Liệu Biểu Đồ Bong Bóng: Truy Cập và Xử Lý Worksheet
Chuẩn bị dữ liệu sẽ cung cấp cho biểu đồ bong bóng:
```java
import com.aspose.cells.WorksheetCollection;
import com.aspose.cells.Cells;
import com.aspose.cells.Cell;

// Get the collection of worksheets
WorksheetCollection worksheets = workbook.getWorksheets();
Worksheet sheet = worksheets.get(0);
Cells cells = sheet.getCells();

// Set values in specific cells to prepare data for charting
cells.get("A1").setValue(50);
cells.get("A2").setValue(100);
cells.get("A3").setValue(150);
cells.get("B1").setValue(4);
cells.get("B2").setValue(20);
cells.get("B3").setValue(180);
cells.get("C1").setValue(320);
cells.get("C2").setValue(110);
cells.get("C3").setValue(180);
cells.get("D1").setValue(40);
cells.get("D2").setValue(120);
cells.get("D3").setValue(250);
```

### Cách Tạo Biểu Đồ Bong Bóng Excel: Tạo và Cấu Hình Biểu Đồ
Tạo biểu đồ bong bóng bằng cách thêm nó vào worksheet và thiết lập nguồn dữ liệu:
```java
import com.aspose.cells.ChartCollection;
import com.aspose.cells.Chart;
import com.aspose.cells.SeriesCollection;
import com.aspose.cells.ChartType;

// Access the collection of charts in the sheet
ChartCollection charts = sheet.getCharts();
int chartIndex = charts.add(ChartType.BUBBLE, 5, 0, 15, 5);
Chart chart = charts.get(chartIndex);

// Add series to the chart and set data sources
SeriesCollection serieses = chart.getNSeries();
serieses.add("A1:B3", true);

// Set bubble sizes, X values, and Y values for the chart
chart.getNSeries().get(0).setBubbleSizes("B2:D2");
chart.getNSeries().get(0).setXValues("B3:D3");
chart.getNSeries().get(0).setValues("B1:D1");
```

### Cách Lưu Biểu Đồ: Lưu Workbook
Lưu workbook (và biểu đồ nhúng) vào đĩa:
```java
import com.aspose.cells.SaveFormat;

// Define the directory to save the file
String dataDir = "YOUR_DATA_DIRECTORY";
workbook.save(dataDir + "/HToCrBChart_out.xls", SaveFormat.EXCEL_97_TO_2003);
```

## Ứng Dụng Thực Tiễn
- **Báo cáo tài chính** – Trực quan hoá doanh thu, lợi nhuận và thị phần trong một cửa sổ.  
- **Phân tích dữ liệu bán hàng** – Nổi bật hiệu suất bán hàng theo khu vực, trong đó kích thước bong bóng thể hiện khối lượng.  
- **Nghiên cứu khoa học** – Hiển thị kết quả thí nghiệm với ba biến số cùng lúc.

## Cân Nhắc Về Hiệu Suất
- Giải phóng các đối tượng không dùng ngay để giải phóng bộ nhớ.  
- Giữ phạm vi dữ liệu càng chặt chẽ càng tốt; các phạm vi lớn không cần thiết có thể làm chậm quá trình render.  
- Áp dụng các thực hành quản lý bộ nhớ của Java khi xử lý tập dữ liệu khổng lồ.

## Các Vấn Đề Thường Gặp và Giải Pháp
| Vấn đề | Nguyên nhân | Giải pháp |
|-------|-------------|-----------|
| **Biểu đồ trống** | Phạm vi dữ liệu không khớp với series | Kiểm tra lại rằng `setBubbleSizes`, `setXValues` và `setValues` tham chiếu đúng các ô. |
| **Kích thước bong bóng không đúng** | Độ dài phạm vi không đồng nhất | Đảm bảo cả ba phạm vi đều chứa cùng số điểm dữ liệu. |
| **Lỗi giấy phép** | Chạy mà không có giấy phép hợp lệ | Áp dụng giấy phép tạm thời hoặc đã mua trước khi tạo workbook. |

## Câu Hỏi Thường Gặp

**Q: Phiên bản tối thiểu của Aspose.Cells yêu cầu là gì?**  
A: Đề nghị sử dụng phiên bản 25.3 cho hướng dẫn này để đảm bảo tương thích với tất cả các tính năng được trình bày.

**Q: Làm sao tôi có thể tùy chỉnh màu sắc của biểu đồ bong bóng?**  
A: Sử dụng các phương thức định dạng của series, chẳng hạn `chart.getNSeries().get(0).getArea().getFillFormat().setForeColor(Color.getRed())`.

**Q: Tôi có thể chạy mã này trên máy chủ Linux không?**  
A: Có, Aspose.Cells cho Java hoàn toàn đa nền tảng và hoạt động trên bất kỳ hệ điều hành nào có JDK tương thích.

**Q: Nếu tôi nhận được lỗi “Data source size mismatch” thì phải làm gì?**  
A: Kiểm tra lại rằng các phạm vi cho kích thước bong bóng, giá trị X và giá trị Y đều chứa cùng số ô.

**Q: Tôi có thể lấy giấy phép tạm thời để thử nghiệm ở đâu?**  
A: Truy cập [trang giấy phép tạm thời của Aspose](https://purchase.aspose.com/temporary-license/) để yêu cầu giấy phép dùng thử.

## Tài Nguyên
- **Tài liệu**: Để biết thêm chi tiết, tham khảo [tài liệu chính thức](https://reference.aspose.com/cells/java/).  
- **Tải về**: Nhận phiên bản mới nhất từ [trang phát hành](https://releases.aspose.com/cells/java/).  
- **Mua**: Khám phá các tùy chọn cấp phép trên [trang này](https://purchase.aspose.com/buy).  
- **Dùng thử miễn phí**: Bắt đầu với bản dùng thử để kiểm tra khả năng tại [phần releases của Aspose](https://releases.aspose.com/cells/java/).  
- **Diễn đàn hỗ trợ**: Đối với bất kỳ câu hỏi nào, có thể truy cập [diễn đàn hỗ trợ](https://forum.aspose.com/c/cells/9).

---

**Cập nhật lần cuối:** 2026-04-02  
**Đã kiểm tra với:** Aspose.Cells 25.3 cho Java  
**Tác giả:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}