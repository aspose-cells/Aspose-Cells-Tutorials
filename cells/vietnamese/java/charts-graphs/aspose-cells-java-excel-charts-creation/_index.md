---
date: '2026-04-08'
description: Tìm hiểu cách tạo biểu đồ đường có dấu đánh dấu bằng Aspose.Cells cho
  Java, thêm biểu đồ vào bảng tính và tùy chỉnh biểu đồ Excel cho báo cáo tự động.
keywords:
- line chart with markers
- add chart to worksheet
- automate excel chart creation
- populate data for chart
- export styled chart excel
title: Tạo biểu đồ đường có dấu đánh dấu bằng Aspose.Cells cho Java
url: /vi/java/charts-graphs/aspose-cells-java-excel-charts-creation/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Tạo và Định dạng Biểu đồ Excel với Aspose.Cells Java

## Giới thiệu

Trong thế giới hiện nay dựa trên dữ liệu, một **line chart with markers** là một trong những cách hiệu quả nhất để trực quan hoá xu hướng và các điểm ngoại lệ. Cho dù bạn đang xây dựng báo cáo tự động hoặc một bảng điều khiển cập nhật hàng ngày, khả năng thêm một line chart with markers vào worksheet một cách lập trình sẽ tiết kiệm vô số bước thủ công. Hướng dẫn này sẽ chỉ cho bạn cách sử dụng Aspose.Cells cho Java để tạo, định dạng và xuất các biểu đồ như vậy, để bạn có thể tập trung vào những hiểu biết thay vì phải thao tác tẻ nhạt trong Excel.

**Bạn sẽ học được gì**
- Khởi tạo một workbook và điền dữ liệu vào bằng Aspose.Cells.  
- **Cách thêm một line chart with markers vào worksheet** và cấu hình giao diện của nó.  
- Tùy chỉnh màu sắc series, markers và các tùy chọn định dạng khác.  
- Lưu workbook dưới dạng tệp Excel có bao gồm biểu đồ đã định dạng của bạn.

## Câu trả lời nhanh

- **Lớp chính để bắt đầu là gì?** `Workbook` khởi tạo một tệp Excel mới.  
- **Loại biểu đồ nào tạo line chart with markers?** `ChartType.LINE_WITH_DATA_MARKERS`.  
- **Làm thế nào để đặt màu tùy chỉnh cho các điểm series?** Sử dụng `chart.getNSeries().setColorVaried(true)` và đặt màu cho vùng marker.  
- **Có cần giấy phép để có đầy đủ chức năng không?** Có, giấy phép Aspose.Cells trả phí hoặc tạm thời sẽ loại bỏ các giới hạn đánh giá.  
- **Tôi có thể xuất kết quả dưới dạng XLSX không?** Chắc chắn—`workbook.save("StyledChart.xlsx")` tạo tệp XLSX.

## Yêu cầu trước

Trước khi tạo và định dạng biểu đồ bằng Aspose.Cells cho Java, hãy chắc chắn rằng bạn đã có cấu hình sau:

### Thư viện cần thiết

Bao gồm Aspose.Cells như một phụ thuộc trong dự án của bạn. Dưới đây là hướng dẫn cho cả người dùng Maven và Gradle:

**Maven:**
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**Gradle:**
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

### Yêu cầu thiết lập môi trường

- Java Development Kit (JDK) được cài đặt trên hệ thống của bạn.  
- Một Integrated Development Environment (IDE) như IntelliJ IDEA hoặc Eclipse để lập trình và kiểm thử.

### Kiến thức cần thiết

Cần có hiểu biết cơ bản về lập trình Java, cùng với sự quen thuộc với workbook Excel và các khái niệm về biểu đồ.

### Mua giấy phép

Aspose.Cells là một sản phẩm thương mại yêu cầu giấy phép để có đầy đủ chức năng. Bạn có thể nhận bản dùng thử miễn phí để đánh giá tính năng, yêu cầu giấy phép tạm thời để thử nghiệm kéo dài, hoặc mua sản phẩm để sử dụng lâu dài.

- **Dùng thử miễn phí:** [Download Free Trial](https://releases.aspose.com/cells/java/)  
- **Giấy phép tạm thời:** [Request Temporary License](https://purchase.aspose.com/temporary-license/)  
- **Mua:** [Buy Aspose.Cells](https://purchase.aspose.com/buy)

## Cài đặt Aspose.Cells cho Java

Sau khi bạn đã cài đặt các phụ thuộc cần thiết, hãy thiết lập môi trường phát triển để sử dụng Aspose.Cells. Bắt đầu bằng việc nhập thư viện và khởi tạo một đối tượng `Workbook` trong ứng dụng Java của bạn:

```java
import com.aspose.cells.*;

public class SetupAsposeCells {
    public static void main(String[] args) throws Exception {
        // Initialize a new workbook instance
        Workbook workbook = new Workbook();
        
        System.out.println("Workbook initialized successfully!");
    }
}
```

## Hướng dẫn triển khai

Trong phần này, chúng ta sẽ chia nhỏ việc triển khai thành các tính năng riêng biệt: Khởi tạo Workbook và Điền dữ liệu, Tạo biểu đồ và Cấu hình, Tùy chỉnh Series, và Lưu Workbook.

### Tính năng 1: Khởi tạo Workbook và Điền dữ liệu

**Tổng quan:** Tính năng này tập trung vào việc tạo một workbook mới, truy cập worksheet đầu tiên và điền dữ liệu để tạo biểu đồ.

#### Bước 1: Khởi tạo Workbook

Bắt đầu bằng cách tạo một đối tượng `Workbook`:

```java
import com.aspose.cells.*;

public class FeatureWorkbookInitialization {
    public static void main(String[] args) throws Exception {
        // Instantiate a workbook
        Workbook workbook = new Workbook();
        
        // Access first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);
```

#### Bước 2: Đặt tiêu đề cột và điền dữ liệu

Xác định tiêu đề cột và điền các hàng dữ liệu mẫu:

```java
        // Set columns title 
        worksheet.getCells().get(0, 0).setValue("X");
        worksheet.getCells().get(0, 1).setValue("Y");

        // Create random data for series 1
        for (int i = 1; i < 21; i++) {
            worksheet.getCells().get(i, 0).setValue(i);
            worksheet.getCells().get(i, 1).setValue(0.8);
        }

        // Create random data for series 2
        for (int i = 21; i < 41; i++) {
            worksheet.getCells().get(i, 0).setValue(i - 20);
            worksheet.getCells().get(i, 1).setValue(0.9);
        }
    }
}
```

### Tính năng 2: Tạo biểu đồ và Cấu hình

**Tổng quan:** Tính năng này minh họa cách thêm một biểu đồ vào worksheet của workbook, đặt kiểu dáng và cấu hình các thuộc tính cơ bản.

#### Bước 3: Thêm biểu đồ vào Worksheet

Thêm một line chart with data markers:

```java
import com.aspose.cells.*;

public class FeatureChartCreation {
    public static void main(String[] args) throws Exception {
        // Instantiate a workbook
        Workbook workbook = new Workbook();
        
        // Access first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);
        
        // Add chart to the worksheet
        int idx = worksheet.getCharts().add(ChartType.LINE_WITH_DATA_MARKERS, 1, 3, 20, 20);

        // Access and configure the chart
        Chart chart = worksheet.getCharts().get(idx);
        chart.setStyle(3); // Set a predefined style
        chart.setAutoScaling(true);
        chart.getTitle().setText("Sample Chart");
        chart.getCategoryAxis().getTitle().setText("Units");
    }
}
```

### Tính năng 3: Cấu hình và Tùy chỉnh Series

**Tổng quan:** Nâng cao tính thẩm mỹ của biểu đồ bằng cách tùy chỉnh cài đặt series, như màu sắc đa dạng và kiểu marker.

#### Bước 4: Tùy chỉnh cài đặt Series

Cấu hình dữ liệu series, áp dụng định dạng tùy chỉnh và điều chỉnh markers:

```java
import com.aspose.cells.*;

public class FeatureSeriesConfiguration {
    public static void main(String[] args) throws Exception {
        // Instantiate a workbook
        Workbook workbook = new Workbook();
        
        // Access first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);
        
        // Add series to the chart
        Chart chart = worksheet.getCharts().add(ChartType.LINE_WITH_DATA_MARKERS, 1, 3, 20, 20).get(0);

        int s2_idx = chart.getNSeries().add("A2: A21", true);
        int s3_idx = chart.getNSeries().add("A22: A41", true);

        // Enable varied colors for series points
        chart.getNSeries().setColorVaried(true);

        // Customize first series marker styles and colors
        chart.getNSeries().get(s2_idx).getArea().setFormatting(FormattingType.CUSTOM);
        chart.getNSeries().get(s2_idx).getMarker().getArea().setForegroundColor(Color.getYellow());
        chart.getNSeries().get(s2_idx).getMarker().getBorder().setVisible(false);

        // Set X and Y values for the first series
        chart.getNSeries().get(s2_idx).setXValues("A2: A21");
        chart.getNSeries().get(s2_idx).setValues("B2: B21");

        // Customize second series marker styles and colors
        chart.getNSeries().get(s3_idx).getArea().setFormatting(FormattingType.CUSTOM);
        chart.getNSeries().get(s3_idx).getMarker().getArea().setForegroundColor(Color.getGreen());
        chart.getNSeries().get(s3_idx).getMarker().getBorder().setVisible(false);

        // Set X and Y values for the second series
        chart.getNSeries().get(s3_idx).setXValues("A22: A41");
        chart.getNSeries().get(s3_idx).setValues("B22: B41");
    }
}
```

### Tính năng 4: Lưu Workbook

**Tổng quan:** Cuối cùng, lưu workbook để lưu lại các thay đổi và đảm bảo biểu đồ được bao gồm trong tệp Excel.

#### Bước 5: Lưu Workbook

Lưu workbook của bạn cùng với các biểu đồ mới tạo:

```java
import com.aspose.cells.*;

public class FeatureWorkbookSaving {
    public static void main(String[] args) throws Exception {
        // Instantiate a workbook
        Workbook workbook = new Workbook();
        
        // Access first worksheet and add data, chart configuration as per previous steps...
        Worksheet worksheet = workbook.getWorksheets().get(0);
        // (Implementation of adding data and configuring the chart would be here)

        // Save the workbook to an Excel file
        workbook.save("StyledChart.xlsx");
    }
}
```

### Vấn đề thường gặp và Khắc phục

- **Biểu đồ hiện ra trống:** Kiểm tra lại các phạm vi ô được sử dụng trong `setXValues` và `setValues` có tham chiếu đúng tới các ô đã được điền dữ liệu hay không.  
- **Màu sắc không được áp dụng:** Đảm bảo `chart.getNSeries().setColorVaried(true)` được gọi trước khi tùy chỉnh từng series riêng lẻ.  
- **Lỗi giấy phép:** Giấy phép dùng thử có thể giới hạn số lượng biểu đồ; cài đặt giấy phép đầy đủ để loại bỏ các hạn chế.

## Câu hỏi thường gặp

**Hỏi: Tôi có thể tạo các loại biểu đồ khác (ví dụ: cột, bánh) với Aspose.Cells không?**  
A: Có, Aspose.Cells hỗ trợ nhiều loại biểu đồ; chỉ cần thay thế `ChartType.LINE_WITH_DATA_MARKERS` bằng giá trị enum mong muốn.

**Hỏi: Tôi có cần đóng workbook hoặc giải phóng tài nguyên không?**  
A: Lớp `Workbook` tự động quản lý tài nguyên, nhưng bạn có thể gọi `workbook.dispose()` trong các ứng dụng chạy lâu để giải phóng bộ nhớ.

**Hỏi: Có thể thêm nhiều biểu đồ vào cùng một worksheet không?**  
A: Chắc chắn—gọi `worksheet.getCharts().add(...)` cho mỗi biểu đồ bạn muốn chèn.

**Hỏi: Làm thế nào để xuất tệp dưới dạng Excel cũ hơn (XLS)?**  
A: Sử dụng `workbook.save("StyledChart.xls", SaveFormat.EXCEL_97_TO_2003);`.

**Hỏi: Biểu đồ có giữ nguyên định dạng khi mở trong Microsoft Excel không?**  
A: Có, Aspose.Cells ghi các đối tượng biểu đồ Excel gốc, vì vậy tất cả các kiểu, màu sắc và markers sẽ hiển thị chính xác như đã định nghĩa.

---

**Cập nhật lần cuối:** 2026-04-08  
**Kiểm tra với:** Aspose.Cells 25.3 cho Java  
**Tác giả:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}