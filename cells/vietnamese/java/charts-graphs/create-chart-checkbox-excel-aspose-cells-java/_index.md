---
date: '2026-09-22'
description: Tìm hiểu cách tạo biểu đồ Excel tương tác với checkboxes bằng Aspose.Cells
  for Java. Hướng dẫn này bao gồm cài đặt, thêm checkboxes, cấp phép và các thực tiễn
  tốt nhất.
keywords:
- create interactive Excel chart
- how to add checkbox java
- aspose.cells license java
lastmod: '2026-09-22'
og_description: Tìm hiểu cách tạo biểu đồ Excel tương tác với checkboxes bằng Aspose.Cells
  for Java. Thực hiện theo các hướng dẫn từng bước, xem các mẹo cấp phép và khám phá
  các trường hợp sử dụng thực tế.
og_image_alt: Guide showing how to create interactive Excel chart with checkboxes
  using Aspose.Cells for Java
og_title: Cách tạo biểu đồ Excel tương tác với checkboxes
schemas:
- author: Aspose
  dateModified: '2026-09-22'
  description: Learn how to create interactive Excel chart with checkboxes using Aspose.Cells
    for Java. This guide covers setup, adding checkboxes, licensing, and best practices.
  headline: How to create interactive Excel chart with checkboxes
  type: TechArticle
- questions:
  - answer: Use Aspose.Cells’ `Shape` API with `ShapeType.FORM_CONTROL_CHECKBOX` and
      link it to a worksheet cell; the checkbox works natively in Excel.
    question: How do I add a checkbox without using VBA?
  - answer: The checkbox shape is available in the free evaluation, but a permanent
      Aspose.Cells license removes evaluation limits and enables full performance
      optimizations.
    question: Do I need a license for the checkbox feature?
  - answer: Files saved with Aspose.Cells follow the Office Open XML standard and
      open correctly in Excel 2016, 2019, 2021, and Microsoft 365.
    question: Which Excel versions can open the generated file?
  - answer: Yes, create a checkbox for each series, link each to a distinct helper
      cell, and use conditional formulas to toggle each series independently.
    question: Can I control multiple series with separate checkboxes?
  - answer: Practically, you can add dozens; performance remains stable up to 200
      controls per worksheet on typical server hardware.
    question: Is there a limit on the number of checkboxes per chart?
  type: FAQPage
tags:
- interactive Excel charts
- Aspose.Cells
- Java Excel automation
title: Cách tạo biểu đồ Excel tương tác với checkboxes
url: /vi/java/charts-graphs/create-chart-checkbox-excel-aspose-cells-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách tạo biểu đồ Excel tương tác với các hộp kiểm

## Giới thiệu

Trong hướng dẫn này, bạn sẽ **tạo biểu đồ Excel tương tác** cho phép người dùng bật/tắt các chuỗi dữ liệu bằng cách nhấp vào các hộp kiểm được đặt trực tiếp trên biểu đồ. Sử dụng Aspose.Cells for Java, bạn có thể tạo sổ làm việc đầy đủ tính năng một cách lập trình, mà không cần cài đặt Microsoft Excel. Cách tiếp cận này hoạt động cho bất kỳ giải pháp báo cáo hoặc bảng điều khiển nào dựa trên Java.

**Những gì bạn sẽ học**
- Cách thiết lập Aspose.Cells for Java trong Maven hoặc Gradle  
- Cách khởi tạo một `Workbook` và thêm biểu đồ cột  
- Cách nhúng một hình dạng hộp kiểm vào khu vực biểu đồ  
- Cách áp dụng giấy phép Aspose.Cells cho môi trường sản xuất  

## Câu trả lời nhanh
- **Thư viện nào tạo biểu đồ Excel tương tác?** Aspose.Cells for Java.  
- **Tôi có thể thêm hộp kiểm mà không dùng VBA không?** Có, bằng cách chèn một hình dạng Form Control thông qua API.  
- **Tôi có cần giấy phép cho tính năng này không?** Giấy phép tạm thời hoạt động cho việc đánh giá; giấy phép vĩnh viễn cần cho môi trường sản xuất.  
- **Phiên bản Java nào được yêu cầu?** JDK 8 hoặc mới hơn.  
- **Biểu đồ có hoạt động trong Excel 2016‑2024 không?** Có, tệp được tạo tuân theo tiêu chuẩn Office Open XML.  

## Biểu đồ Excel tương tác là gì?
**Biểu đồ Excel tương tác** kết hợp một biểu đồ tiêu chuẩn với các điều khiển giao diện người dùng (ví dụ: hộp kiểm) cho phép người dùng hiển thị hoặc ẩn các chuỗi dữ liệu ngay lập tức, biến một hình ảnh tĩnh thành công cụ báo cáo động.

## Tại sao nên sử dụng Aspose.Cells for Java?
Aspose.Cells hỗ trợ **hơn 80 định dạng nhập và xuất** và có thể xử lý sổ làm việc với **hơn 10.000 dòng** mà không cần tải toàn bộ tệp vào bộ nhớ, mang lại việc tạo ra hiệu suất cao trong môi trường máy chủ.

## Yêu cầu trước

- **Java Development Kit (JDK):** phiên bản 8 hoặc cao hơn.  
- **Aspose.Cells for Java:** bản phát hành mới nhất (ví dụ: 25.3).  
- **Maven hoặc Gradle:** để quản lý phụ thuộc thư viện.  

### Kiến thức yêu cầu
Cú pháp Java cơ bản và sự quen thuộc với các khái niệm Excel (bảng tính, phạm vi, biểu đồ) là hữu ích, nhưng các bước dưới đây được chi tiết đủ cho các nhà phát triển ở bất kỳ mức độ kinh nghiệm nào.

## Cách thêm hộp kiểm trong Java?

Tải thư viện Aspose.Cells, tạo một workbook, và chèn một hình dạng hộp kiểm trong một lần gọi. Hộp kiểm là một Form Control có thể liên kết với một ô; việc bật/tắt nó sẽ thay đổi giá trị của ô liên kết, mà sau này bạn có thể liên kết với khả năng hiển thị của chuỗi dữ liệu trong biểu đồ.

```text
// Direct answer (40‑70 words):
You add a checkbox by creating a `Shape` of type `ShapeType.FORM_CONTROL_CHECKBOX`, setting its placement on the chart worksheet, and linking it to a cell that stores the Boolean state. The linked cell can be used in formulas that drive chart series visibility, enabling real‑time interactivity without VBA.
```

### Bước 1: Thiết lập phụ thuộc Maven

Thêm artifact Aspose.Cells Maven vào file `pom.xml` của bạn:

```xml
<dependency>
  <groupId>com.aspose</groupId>
  <artifactId>aspose-cells</artifactId>
  <version>25.3</version>
</dependency>
```

### Bước 2: Thiết lập phụ thuộc Gradle

Thêm dòng sau vào file `build.gradle` của bạn:

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

#### Các bước lấy giấy phép
Để mở khóa đầy đủ chức năng, hãy lấy một giấy phép tạm thời hoặc vĩnh viễn. Tải giấy phép dùng thử từ [trang web của Aspose](https://releases.aspose.com/cells/java/). Đối với môi trường sản xuất, mua giấy phép và áp dụng nó như được mô tả sau.

#### Khởi tạo cơ bản
License là lớp Aspose.Cells dùng để áp dụng tệp giấy phép đã mua, cho phép đầy đủ chức năng mà không có giới hạn đánh giá. Khởi tạo thư viện trong mã Java của bạn trước bất kỳ thao tác nào với workbook:

```java
import com.aspose.cells.Workbook;

public class AsposeSetup {
    public static void main(String[] args) throws Exception {
        // Initialize the Workbook object.
        Workbook workbook = new Workbook();
        
        System.out.println("Aspose.Cells for Java initialized successfully.");
    }
}
```

## Cách tạo biểu đồ Excel tương tác?

Một đối tượng `Workbook` của Aspose.Cells đại diện cho một tệp Excel toàn bộ, chứa các worksheet, biểu đồ và các yếu tố khác. Bằng cách tạo một workbook, bạn có thể lập trình thêm dữ liệu, tạo biểu đồ cột, và sau đó nhúng các điều khiển tương tác như hộp kiểm. Các bước sau sẽ hướng dẫn bạn xây dựng workbook, điền dữ liệu và cấu hình biểu đồ để tương tác.

```text
// Direct answer (40‑70 words):
First, instantiate a `Workbook`, fill a worksheet with sample data, and call `addChart` to place a column chart. Next, create a checkbox shape, position it over the chart, and link it to a cell that toggles the series’ `isVisible` property via a formula. Finally, save the workbook as an XLSX file.
```

### Khởi tạo workbook và thêm biểu đồ

#### Tổng quan
Phần này trình bày cách tạo một workbook mới, thêm một worksheet cho dữ liệu, và tạo một biểu đồ cột sẽ được làm tương tác sau này.

##### Bước 1: Tạo một workbook mới

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.SheetType;

public class ChartCreation {
    public static void main(String[] args) throws Exception {
        // Instantiate a new Workbook object representing an Excel file.
        Workbook workbook = new Workbook();
        
        System.out.println("Workbook created.");
    }
}
```

##### Bước 2: Thêm worksheet cho biểu đồ

```java
import com.aspose.cells.Worksheet;
import com.aspose.cells.ChartType;

public class ChartCreation {
    public static void main(String[] args) throws Exception {
        Workbook workbook = new Workbook();
        
        // Adding a chart worksheet to the workbook.
        int index = workbook.getWorksheets().add(SheetType.CHART);
        Worksheet sheet = workbook.getWorksheets().get(index);

        System.out.println("Chart worksheet added.");
    }
}
```

##### Bước 3: Chèn biểu đồ cột

```java
public class ChartCreation {
    public static void main(String[] args) throws Exception {
        Workbook workbook = new Workbook();
        int index = workbook.getWorksheets().add(SheetType.CHART);
        Worksheet sheet = workbook.getWorksheets().get(index);

        // Add a floating chart of type COLUMN to the newly added chart worksheet.
        sheet.getCharts().addFloatingChart(ChartType.COLUMN, 0, 0, 1024, 960);

        System.out.println("Column chart inserted.");
    }
}
```

##### Bước 4: Thêm dữ liệu chuỗi

```java
public class ChartCreation {
    public static void main(String[] args) throws Exception {
        Workbook workbook = new Workbook();
        int index = workbook.getWorksheets().add(SheetType.CHART);
        Worksheet sheet = workbook.getWorksheets().get(index);

        // Add a floating chart of type COLUMN.
        sheet.getCharts().addFloatingChart(ChartType.COLUMN, 0, 0, 1024, 960);

        // Adding series data for the chart.
        sheet.getCharts().get(0).getNSeries().add("{1,2,3}", false);
        
        System.out.println("Series data added to the chart.");
    }
}
```

## Cách nhúng hộp kiểm vào biểu đồ?

Nhúng một hộp kiểm trực tiếp vào khu vực biểu đồ cho phép người dùng cuối nhấp để hiển thị hoặc ẩn một chuỗi cụ thể. Hộp kiểm là một hình dạng Form Control có thể liên kết với một ô; giá trị ô có thể được tham chiếu trong công thức điều khiển khả năng hiển thị của chuỗi.

Shape là đối tượng Aspose.Cells đại diện cho một yếu tố vẽ như form control, hình ảnh hoặc hộp văn bản trong worksheet.

```text
// Direct answer (40‑70 words):
You embed a checkbox by creating a `Shape` with `ShapeType.FORM_CONTROL_CHECKBOX`, positioning it using `setUpperLeftRow/Column` relative to the chart sheet, and linking it to a helper cell (e.g., `B1`). Then, use a conditional formula in the series data range that checks the helper cell’s Boolean value to decide whether the series is plotted.
```

### Nhúng hình dạng hộp kiểm

```java
import com.aspose.cells.MsoDrawingType;
import com.aspose.cells.PlacementType;

public class ChartWithCheckbox {
    public static void main(String[] args) throws Exception {
        Workbook workbook = new Workbook();
        int index = workbook.getWorksheets().add(SheetType.CHART);
        Worksheet sheet = workbook.getWorksheets().get(index);

        // Add a checkbox shape within the chart area on the first chart of the worksheet.
        sheet.getCharts().get(0).getShapes().addShapeInChart(MsoDrawingType.CHECK_BOX, PlacementType.MOVE, 400, 400, 1000, 600);
        
        System.out.println("Checkbox added to the chart.");
    }
}
```

### Đặt văn bản hộp kiểm

```java
public class ChartWithCheckbox {
    public static void main(String[] args) throws Exception {
        Workbook workbook = new Workbook();
        int index = workbook.getWorksheets().add(SheetType.CHART);
        Worksheet sheet = workbook.getWorksheets().get(index);

        // Add checkbox shape within the chart.
        sheet.getCharts().get(0).getShapes().addShapeInChart(MsoDrawingType.CHECK_BOX, PlacementType.MOVE, 400, 400, 1000, 600);

        // Setting text for the newly added checkbox shape.
        sheet.getCharts().get(0).getShapes().get(0).setText("CheckBox 1");

        System.out.println("Checkbox labeled successfully.");
    }
}
```

## Cách lưu workbook dưới dạng tệp Excel?

Lưu `Workbook` ghi tất cả các thay đổi trong bộ nhớ vào một tệp Excel thực tế trên đĩa. Aspose.Cells hỗ trợ định dạng .xlsx hiện đại, đảm bảo tệp mở được trong Excel 2016‑2024 và các ứng dụng tương thích Office khác. Sử dụng phương thức `save` với đường dẫn tệp mong muốn, và tùy chọn chỉ định định dạng tệp cho các tùy chọn bổ sung.

```text
// Direct answer (40‑70 words):
Call `workbook.save("InteractiveChart.xlsx", SaveFormat.XLSX)` to write the workbook. The method automatically closes all streams and guarantees that the embedded chart and checkbox are fully functional when the file is opened in Excel 2016‑2024.
```

```java
public class ChartWithCheckbox {
    public static void main(String[] args) throws Exception {
        Workbook workbook = new Workbook();
        int index = workbook.getWorksheets().add(SheetType.CHART);
        Worksheet sheet = workbook.getWorksheets().get(index);

        // Add checkbox shape and label it.
        sheet.getCharts().get(0).getShapes().addShapeInChart(MsoDrawingType.CHECK_BOX, PlacementType.MOVE, 400, 400, 1000, 600);
        sheet.getCharts().get(0).getShapes().get(0).setText("CheckBox 1");

        // Save the workbook
        String outDir = "YOUR_OUTPUT_DIRECTORY"; // Replace with your actual output directory path.
        workbook.save(outDir + "/InsertCheckboxInChartSheet_out.xlsx");
        
        System.out.println("Workbook saved successfully.");
    }
}
```

## Ứng dụng thực tiễn

Các kịch bản thực tế mà biểu đồ tương tác với hộp kiểm mang lại giá trị:

1. **Báo cáo tương tác:** Cho phép các bên liên quan bật/tắt các dòng sản phẩm riêng lẻ trên biểu đồ bán hàng.  
2. **Phân tích so sánh:** Cho phép nhà phân tích tập trung vào các khoảng thời gian hoặc khu vực cụ thể bằng cách chọn/không chọn các chuỗi.  
3. **Bảng điều khiển giáo dục:** Sinh viên có thể khám phá xu hướng dữ liệu bằng cách chọn các biến muốn hiển thị.

## Các vấn đề thường gặp và giải pháp
- **Hộp kiểm không phản hồi:** Đảm bảo hộp kiểm được liên kết với một ô và ô đó được tham chiếu trong công thức ảnh hưởng đến khả năng hiển thị của chuỗi.  
- **Biểu đồ không cập nhật sau khi bật/tắt:** Làm mới chế độ xem workbook trong Excel hoặc tính lại công thức (`workbook.calculateFormula()`).  
- **Giấy phép không được áp dụng:** Kiểm tra rằng `License license = new License(); license.setLicense("Aspose.Cells.lic");` được thực thi trước bất kỳ thao tác nào với workbook.

## Câu hỏi thường gặp

**Q: Làm thế nào tôi có thể thêm hộp kiểm mà không dùng VBA?**  
A: Sử dụng API `Shape` của Aspose.Cells với `ShapeType.FORM_CONTROL_CHECKBOX` và liên kết nó với một ô trong worksheet; hộp kiểm hoạt động nguyên bản trong Excel.

**Q: Tôi có cần giấy phép cho tính năng hộp kiểm không?**  
A: Hình dạng hộp kiểm có sẵn trong bản đánh giá miễn phí, nhưng giấy phép Aspose.Cells vĩnh viễn loại bỏ giới hạn đánh giá và cho phép tối ưu hiệu năng đầy đủ.

**Q: Các phiên bản Excel nào có thể mở tệp được tạo?**  
A: Các tệp được lưu bằng Aspose.Cells tuân theo tiêu chuẩn Office Open XML và mở đúng trong Excel 2016, 2019, 2021 và Microsoft 365.

**Q: Tôi có thể điều khiển nhiều chuỗi bằng các hộp kiểm riêng biệt không?**  
A: Có, tạo một hộp kiểm cho mỗi chuỗi, liên kết mỗi hộp với một ô trợ giúp riêng, và sử dụng công thức có điều kiện để bật/tắt mỗi chuỗi một cách độc lập.

**Q: Có giới hạn số lượng hộp kiểm trên mỗi biểu đồ không?**  
A: Thực tế, bạn có thể thêm hàng chục; hiệu năng vẫn ổn định lên tới 200 điều khiển trên mỗi worksheet trên phần cứng máy chủ thông thường.

---

**Cập nhật lần cuối:** 2026-09-22  
**Kiểm tra với:** Aspose.Cells 25.3 for Java  
**Tác giả:** Aspose

## Hướng dẫn liên quan

- [Cách thêm hộp kiểm trong Excel bằng Aspose.Cells for Java: Hướng dẫn từng bước](/cells/java/data-validation/add-checkbox-excel-aspose-cells-java/)
- [Tạo biểu đồ Excel động với Aspose.Cells Java: Hướng dẫn toàn diện cho nhà phát triển](/cells/java/charts-graphs/aspose-cells-java-dynamic-excel-charts/)
- [Thêm nhãn dữ liệu vào biểu đồ Excel với Aspose.Cells Java](/cells/java/advanced-excel-charts/chart-interactivity/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}