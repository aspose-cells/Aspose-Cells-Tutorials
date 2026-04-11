---
date: '2026-04-11'
description: Học tự động hoá Excel bằng Java với Aspose.Cells. Hướng dẫn này cho thấy
  cách tạo workbook Excel bằng Java, điền dữ liệu Excel bằng Java và lưu file Excel
  bằng Java kèm biểu đồ.
keywords:
- excel automation java
- create excel workbook java
- save excel file java
- populate excel data java
- aspose cells java
title: 'Tự động hoá Excel bằng Java: Tạo sổ làm việc và biểu đồ bằng Aspose'
url: /vi/java/charts-graphs/aspose-cells-java-excel-workbook-charts/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Tự động hoá Excel Java: Tạo Sổ làm việc & Biểu đồ bằng Aspose

## Giới thiệu

Tự động hoá các tác vụ Excel bằng Java có thể tiết kiệm hàng giờ công việc thủ công, đặc biệt khi bạn cần tạo báo cáo, bảng điều khiển, hoặc các biểu đồ dựa trên dữ liệu một cách nhanh chóng. **Excel automation java** với Aspose.Cells cung cấp một API sạch sẽ, hiệu năng cao, xử lý mọi thứ từ việc tạo sổ làm việc đến định dạng biểu đồ tinh vi. Trong hướng dẫn này, bạn sẽ học cách thiết lập Aspose.Cells, **tạo một Excel workbook java**, điền dữ liệu, thêm biểu đồ, áp dụng định dạng 3‑D, và cuối cùng **lưu tệp Excel java**.

### Câu trả lời nhanh
- **Thư viện nào đơn giản hoá việc tự động hoá Excel trong Java?** Aspose.Cells for Java.  
- **Tôi có thể thêm biểu đồ 3‑D bằng chương trình không?** Có – API hỗ trợ định dạng 3‑D và hiệu ứng ánh sáng.  
- **Tôi có cần giấy phép cho việc phát triển không?** Giấy phép dùng thử miễn phí có sẵn; giấy phép thương mại cần cho môi trường sản xuất.  
- **Công cụ xây dựng Java nào được hỗ trợ?** Maven và Gradle đều được hỗ trợ đầy đủ.  
- **Các định dạng tệp nào tôi có thể xuất?** XLS, XLSX, CSV, PDF và nhiều hơn nữa.

## Excel automation java là gì?

Excel automation java đề cập đến quá trình tạo, sửa đổi và lưu các sổ làm việc Excel một cách lập trình bằng mã Java. Nó loại bỏ việc chỉnh sửa bảng tính thủ công, đảm bảo tính nhất quán và cho phép tích hợp với các hệ thống khác như cơ sở dữ liệu hoặc dịch vụ web.

## Tại sao nên sử dụng Aspose.Cells cho Java?

- **Bộ tính năng phong phú** – từ giá trị ô đơn giản đến biểu đồ phức tạp, bảng pivot và định dạng có điều kiện.  
- **Không phụ thuộc vào Microsoft Office** – hoạt động trên bất kỳ môi trường máy chủ nào.  
- **Hiệu năng cao** – được tối ưu cho bộ dữ liệu lớn và các kịch bản đa luồng.  
- **Hỗ trợ đa định dạng** – đọc/ghi XLS, XLSX, ODS, CSV, PDF, HTML và nhiều hơn nữa.

## Yêu cầu trước

- **Java Development Kit (JDK) 8+**  
- **Maven hoặc Gradle** để quản lý phụ thuộc  
- **Aspose.Cells for Java 25.3 hoặc mới hơn** (dùng thử hoặc có giấy phép)  

## Cài đặt Aspose.Cells cho Java

Thêm thư viện vào dự án của bạn bằng một trong các cấu hình sau.

### Maven
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

### Gradle
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

#### Cách lấy giấy phép

Yêu cầu giấy phép dùng thử miễn phí từ trang web Aspose, hoặc mua giấy phép đầy đủ cho môi trường sản xuất. Đặt tệp giấy phép vào dự án và tải nó tại thời gian chạy.

## Khởi tạo và Cấu hình Cơ bản

Sau khi phụ thuộc đã được giải quyết, bạn có thể bắt đầu viết mã.

```java
import com.aspose.cells.Workbook;

public class ExcelDemo {
    public static void main(String[] args) throws Exception {
        String dataDir = "YOUR_DATA_DIRECTORY";
        String outDir = "YOUR_OUTPUT_DIRECTORY";

        // Initialize a new Workbook object
        Workbook book = new Workbook();
        System.out.println("Workbook initialized successfully.");
    }
}
```

## Hướng dẫn Từng bước

### Bước 1: Cách tạo excel workbook java

Tạo một thể hiện workbook mới sẽ chứa tất cả các worksheet của bạn.

```java
import com.aspose.cells.Workbook;
// Initialize a new Workbook object
Workbook book = new Workbook();
```

### Bước 2: Thêm các worksheet (bao gồm một sheet biểu đồ)

```java
import com.aspose.cells.Worksheet;
Worksheet dataSheet = book.getWorksheets().add("DataSheet");
Worksheet chartSheet = book.getWorksheets().add("MyChart");
System.out.println("Worksheets added successfully.");
```

### Bước 3: Cách điền dữ liệu Excel bằng Java

Chèn dữ liệu mẫu mà biểu đồ sẽ tham chiếu.

```java
import com.aspose.cells.Cells;
Cells cells = dataSheet.getCells();
cells.get("B1").putValue(1);
cells.get("B2").putValue(2);
cells.get("B3").putValue(3);
cells.get("A1").putValue("A");
cells.get("A2").putValue("B");
cells.get("A3").putValue("C");
System.out.println("Data populated successfully.");
```

### Bước 4: Thêm biểu đồ cột vào workbook

```java
import com.aspose.cells.Chart;
import com.aspose.cells.ChartCollection;
import com.aspose.cells.ChartType;
ChartCollection charts = chartSheet.getCharts();
charts.add(ChartType.COLUMN, 5, 0, 25, 15);
Chart chart = book.getWorksheets().get(2).getCharts().get(0);
System.out.println("Chart added successfully.");
```

### Bước 5: Áp dụng định dạng màu cho vùng biểu đồ

```java
import com.aspose.cells.Color;
chart.getPlotArea().getArea().setBackgroundColor(Color.getWhite());
chart.getChartArea().getArea().setBackgroundColor(Color.getWhite());
chart.getPlotArea().getArea().setForegroundColor(Color.getWhite());
chart.getChartArea().getArea().setForegroundColor(Color.getWhite());
System.out.println("Color formatting applied successfully.");
```

### Bước 6: Cấu hình chú giải và chuỗi dữ liệu

```java
import com.aspose.cells.Series;
chart.setShowLegend(false);
chart.getNSeries().add("DataSheet!B1:B3", true);
chart.getNSeries().setCategoryData("DataSheet!A1:A3");
Series ser = chart.getNSeries().get(0);
System.out.println("Chart series configured successfully.");
```

### Bước 7: Áp dụng định dạng 3D cho chuỗi

```java
import com.aspose.cells.Bevel;
import com.aspose.cells.BevelPresetType;
import com.aspose.cells.Format3D;
import com.aspose.cells.LightRigType;
import com.aspose.cells.PresetMaterialType;
import com.aspose.cells.ShapePropertyCollection;
ShapePropertyCollection spPr = ser.getShapeProperties();
Format3D fmt3d = spPr.getFormat3D();

Bevel bevel = fmt3d.getTopBevel();
bevel.setType(BevelPresetType.CIRCLE);
bevel.setHeight(5);
bevel.setWidth(9);
fmt3d.setSurfaceMaterialType(PresetMaterialType.WARM_MATTE);
fmt3d.setSurfaceLightingType(LightRigType.THREE_POINT);
fmt3d.setLightingAngle(20);
System.out.println("3D formatting applied successfully.");
```

### Bước 8: Đặt màu cho chuỗi để phân biệt rõ hơn

```java
ser.getArea().setBackgroundColor(Color.getMaroon());
ser.getArea().setForegroundColor(Color.getMaroon());
ser.getBorder().setColor(Color.getMaroon());
System.out.println("Series color formatting applied successfully.");
```

### Bước 9: Cách lưu tệp Excel bằng Java

```java
book.save(outDir + "A3DFormat_out.xls");
System.out.println("Workbook saved successfully.");
```

## Ứng dụng Thực tế

- **Báo cáo Tài chính** – Tạo báo cáo quý với biểu đồ động.  
- **Bảng điều khiển Phân tích Dữ liệu** – Xây dựng bảng điều khiển tương tác tự động làm mới.  
- **Quản lý Kho** – Xuất mức tồn kho và xu hướng sang Excel để các bên liên quan xem xét.  
- **Lập kế hoạch Dự án** – Tạo biểu đồ kiểu Gantt trực tiếp từ hệ thống lập lịch dựa trên Java.

## Mẹo Hiệu năng cho Excel Automation Java

- **Tái sử dụng các đối tượng Workbook** khi xử lý nhiều sheet để giảm tiêu thụ bộ nhớ.  
- **Cập nhật ô theo lô** bằng `Cells.importArray` cho bộ dữ liệu lớn thay vì gọi `putValue` từng ô.  
- **Giải phóng tài nguyên** bằng cách gọi `book.dispose()` sau khi lưu các tệp lớn.

## Câu hỏi Thường gặp

**Q: Tôi có thể tạo XLSX thay vì XLS không?**  
A: Có – chỉ cần thay đổi phần mở rộng tệp trong `book.save("output.xlsx")`; Aspose sẽ tự động chọn định dạng đúng.

**Q: Có cần giấy phép cho việc phát triển không?**  
A: Giấy phép dùng thử miễn phí đủ cho việc phát triển và kiểm thử. Đối với triển khai sản xuất cần mua giấy phép.

**Q: Làm thế nào để thêm các loại biểu đồ khác?**  
A: Sử dụng enum `ChartType` (ví dụ `ChartType.PIE`, `ChartType.LINE`) khi gọi `charts.add(...)`.

**Q: Nếu tôi cần bảo vệ workbook thì sao?**  
A: Gọi `book.getSettings().setPassword("yourPassword")` trước khi lưu.

**Q: Aspose.Cells có hỗ trợ tệp có macro không?**  
A: Có – bạn có thể tạo hoặc giữ lại macro VBA trong workbook XLSM.

**Last Updated:** 2026-04-11  
**Tested With:** Aspose.Cells 25.3 (Java)  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}