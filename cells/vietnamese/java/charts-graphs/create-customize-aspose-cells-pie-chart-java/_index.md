---
date: '2026-09-27'
description: Tìm hiểu cách tạo pie chart java bằng Aspose.Cells. Hướng dẫn từng bước
  để tùy chỉnh Excel pie chart, thiết lập Maven dependency và tạo biểu đồ chuyên nghiệp.
keywords:
- create pie chart java
- customize excel pie chart
- maven dependency aspose cells
lastmod: '2026-09-27'
og_description: Tạo pie chart java bằng Aspose.Cells cho Java. Tìm hiểu cách tùy chỉnh
  Excel pie chart, thêm Maven dependency và tạo biểu đồ chuyên nghiệp trong vài phút.
og_image_alt: Java code generating a customized pie chart in Excel with Aspose.Cells
og_title: Tạo pie chart java với Aspose.Cells – Hướng dẫn Java đầy đủ
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Learn how to create pie chart java using Aspose.Cells. Step‑by‑step
    guide to customize Excel pie chart, set up Maven dependency, and generate professional
    charts.
  headline: How to create pie chart java with Aspose.Cells
  type: TechArticle
- questions:
  - answer: Yes, repeat the chart‑creation steps for each data range; each chart is
      independent.
    question: Can I generate multiple pie charts in the same workbook?
  - answer: It does; set the chart type to `ChartType.PIE_3D` when adding the chart.
    question: Does Aspose.Cells support 3‑D pie charts?
  - answer: Use the `Workbook.setDefaultTheme` method before creating any charts.
    question: How do I apply a custom theme to all charts?
  - answer: Over 30 formats, including XLSX, CSV, PDF, and HTML.
    question: What file formats can I export the workbook to?
  - answer: Yes, a valid license removes evaluation watermarks and unlocks full functionality.
    question: Is a license required for commercial deployment?
  type: FAQPage
tags:
- Aspose.Cells
- Java charting
- Excel automation
- data visualization
title: Cách tạo pie chart java với Aspose.Cells
url: /vi/java/charts-graphs/create-customize-aspose-cells-pie-chart-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách tạo biểu đồ tròn java với Aspose.Cells

## Giới thiệu
Việc tạo **pie chart** một cách lập trình thường cảm giác như một câu đố, đặc biệt khi bạn cần kiểm soát chi tiết màu sắc, chú giải và tiêu đề. Trong hướng dẫn này, bạn sẽ học cách **create pie chart java** bằng Aspose.Cells, sau đó tùy chỉnh biểu đồ tròn Excel để phù hợp với thương hiệu hoặc phong cách báo cáo của bạn. Chúng tôi sẽ hướng dẫn qua việc thiết lập môi trường, điền dữ liệu, tạo biểu đồ và tinh chỉnh hình ảnh — tất cả mà không rời khỏi IDE Java của bạn.

**Bạn sẽ học được**
- Thêm **Maven dependency Aspose.Cells** vào dự án của bạn.
- Tạo một workbook, điền dữ liệu vào các ô và tạo biểu đồ tròn.
- Áp dụng màu sắc tùy chỉnh, tiêu đề và chú giải cho biểu đồ.
- Xuất workbook ra tệp XLSX sẵn sàng chia sẻ.

Trước khi bắt đầu, bạn nên quen thuộc với cú pháp Java cơ bản và đã cài đặt Maven hoặc Gradle.

## Câu trả lời nhanh
- **Thư viện nào tạo biểu đồ tròn trong Java?** Aspose.Cells for Java.
- **Tôi có cần giấy phép không?** Bản dùng thử miễn phí hoạt động cho phát triển; giấy phép trả phí cần thiết cho môi trường sản xuất.
- **Các tọa độ Maven cần thiết là gì?** `com.aspose:aspose-cells:24.10`.
- **Tôi có thể thay đổi màu sắc các lát không?** Có, thông qua phương thức `setAreaColor` trên mỗi series.
- **Biểu đồ có thể xuất ra XLSX không?** Chắc chắn — chỉ cần gọi `workbook.save("output.xlsx")`.

## Biểu đồ tròn trong Excel là gì?
Biểu đồ tròn hiển thị một chuỗi dữ liệu duy nhất dưới dạng các lát tỷ lệ của một vòng tròn, giúp dễ dàng so sánh các phần của tổng thể. Góc của mỗi lát tương ứng với giá trị của nó so với tổng, cho phép nhanh chóng nắm bắt sự phân bố qua các danh mục như thị phần, phân bổ ngân sách, hoặc tỷ lệ dân số.

## Tại sao nên sử dụng Aspose.Cells để tạo biểu đồ tròn java?
Aspose.Cells hỗ trợ hơn 50 loại biểu đồ và có thể xử lý các worksheet lên tới một triệu hàng mà không cần tải toàn bộ tệp vào bộ nhớ. Ưu điểm về hiệu năng này cho phép bạn tạo các báo cáo lớn trên phần cứng vừa phải, đồng thời cung cấp kiểm soát chi tiết về giao diện biểu đồ, ràng buộc dữ liệu và định dạng xuất, khiến nó trở thành lựa chọn vượt trội so với nhiều thư viện mã nguồn mở.

## Yêu cầu trước
- **Java Development Kit (JDK)** 8 hoặc mới hơn.
- **IDE** như IntelliJ IDEA hoặc Eclipse.
- **Maven** hoặc **Gradle** để quản lý phụ thuộc.
- Một **giấy phép Aspose.Cells dùng thử hoặc đã mua**.

### Thư viện và phụ thuộc cần thiết
Thêm artifact Aspose.Cells Maven vào tệp `pom.xml` của bạn:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

Hoặc tương đương Gradle:

```gradle
implementation 'com.aspose:aspose-cells:25.3'
```

### Các bước lấy giấy phép
Aspose.Cells for Java là phần mềm thương mại, nhưng bạn có thể bắt đầu với bản dùng thử miễn phí. Truy cập [trang mua hàng](https://purchase.aspose.com/buy) để nhận khóa giấy phép tạm thời.

## Cài đặt Aspose.Cells cho Java
Đầu tiên, đảm bảo thư viện đã có trong classpath của bạn. Sau khi thêm phụ thuộc, bạn có thể khởi tạo API như dưới đây.

```java
import com.aspose.cells.Workbook;

// Initialize a new workbook instance
Workbook workbook = new Workbook();
```

## Hướng dẫn triển khai

### Tạo và cấu hình workbook
Lớp `Workbook` đại diện cho toàn bộ tệp Excel trong bộ nhớ.

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;
import com.aspose.cells.Cells;
import com.aspose.cells.ChartType;
import com.aspose.cells.Chart;
import com.aspose.cells.Series;
import com.aspose.cells.Color;
import com.aspose.cells.LegendPositionType;
import com.aspose.cells.SaveFormat;
```

#### Bước 1: khởi tạo một workbook
```java
// Creates an empty workbook instance to work with.
Workbook workbook = new Workbook();
```  
Điều này tạo ra một workbook mới, trống, mà bạn có thể ngay lập tức bắt đầu điền dữ liệu.

### Truy cập hoặc sửa đổi các ô worksheet
Một `Worksheet` đại diện cho một sheet duy nhất trong workbook, chứa các ô, hàng và cột.  
Bạn sẽ ghi dữ liệu điều khiển biểu đồ tròn vào một worksheet.

#### Bước 2: lấy worksheet đầu tiên và các ô của nó
```java
// Access the first worksheet in the workbook.
Worksheet worksheet = workbook.getWorksheets().get(0);
Cells cells = worksheet.getCells();

// Put sample values used for a pie chart into specific cells.
cells.get("C3").putValue("India");
cells.get("C4").putValue("China");
cells.get("C5").parseNumber("United States", true, null);
cells.get("C6").setValue("Russia");
cells.get("C7").setValue("United Kingdom");
cells.get("C8").setValue("Others");

// Put percentage values for a pie chart into specific cells.
cells.get("D2").putValue("% of world population");
cells.get("D3").putValue(25);
cells.get("D4").putValue(30);
cells.get("D5").putValue(10);
cells.get("D6").putValue(13);
cells.get("D7").putValue(9);
cells.get("D8").putValue(13);
```  
Điền các ô với tên danh mục và giá trị mà biểu đồ sẽ sử dụng.

### Tạo biểu đồ tròn
Các đối tượng `Chart` hiển thị dữ liệu trong một worksheet và hỗ trợ nhiều loại như pie, column và line.

#### Bước 3: thêm biểu đồ tròn vào worksheet
```java
// Create a pie chart in the worksheet.
int pieIdx = worksheet.getCharts().add(ChartType.PIE, 1, 6, 15, 14);
Chart pie = worksheet.getCharts().get(pieIdx);
```  

### Cấu hình series và dữ liệu cho biểu đồ tròn
`Series` xác định phạm vi dữ liệu và định dạng cho một biểu đồ, liên kết các ô worksheet với các yếu tố trực quan.

#### Bước 4: đặt series cho biểu đồ
```java
// Configure the series data range for the chart.
pie.getNSeries().add("D3:D8", true);
pie.getNSeries().setCategoryData("=Sheet1!$C$3:$C$8");

// Link the pie chart title to a cell containing the title text.
pie.getTitle().setLinkedSource("D2");
```  

### Cấu hình giao diện chú giải và tiêu đề biểu đồ
Một `Legend` của biểu đồ hiển thị tên series và màu sắc, giúp người đọc nhận diện mỗi lát.

#### Bước 5: tùy chỉnh chú giải và tiêu đề biểu đồ
```java
// Set legend position at bottom of the chart.
pie.getLegend().setPosition(LegendPositionType.BOTTOM);

// Set font properties for the chart title.
pie.getTitle().getFont().setName("Calibri");
pie.getTitle().getFont().setSize(18);
```  

### Tùy chỉnh màu sắc series biểu đồ
`setAreaColor` đặt màu nền cho một lát series của biểu đồ bằng giá trị RGB.

#### Bước 6: thay đổi màu sắc các đoạn của biểu đồ tròn
```java
import com.aspose.cells.Color;

// Access and customize colors of individual pie chart segments.
Series srs = pie.getNSeries().get(0);
srs.getPoints().get(0).getArea().setForegroundColor(Color.fromArgb(0, 246, 22, 219));
srs.getPoints().get(1).getArea().setForegroundColor(Color.fromArgb(0, 51, 34, 84));
srs.getPoints().get(2).getArea().setForegroundColor(Color.fromArgb(0, 46, 74, 44));
srs.getPoints().get(3).getArea().setForegroundColor(Color.fromArgb(0, 19, 99, 44));
srs.getPoints().get(4).getArea().setForegroundColor(Color.fromArgb(0, 208, 223, 7));
srs.getPoints().get(5).getArea().setForegroundColor(Color.fromArgb(0, 222, 69, 8));
```  

### Tự động điều chỉnh cột và lưu workbook
`autoFitColumns` tự động điều chỉnh độ rộng cột để phù hợp với nội dung ô.

#### Bước 7: điều chỉnh độ rộng cột và lưu tệp
```java
// Autofit all columns.
worksheet.autoFitColumns();

// Define output directory placeholder path for saving the workbook.
String outDir = "YOUR_OUTPUT_DIRECTORY";

// Save the modified workbook to an Excel file in the specified directory.
workbook.save(outDir + "/CSOrSColorsPieChart_out.xlsx", SaveFormat.XLSX);
```  

## Các trường hợp sử dụng phổ biến
- **Phân tích dân số:** Hiển thị phân bố dân cư theo các khu vực.
- **Báo cáo thị phần:** Trực quan hoá phần thị phần của từng đối thủ trong một cái nhìn.
- **Phân bổ ngân sách:** Nổi bật cách phân chia ngân sách giữa các phòng ban.

## Các lưu ý về hiệu năng
- Giải phóng các đối tượng (`workbook.dispose()`) khi không còn cần thiết để giải phóng bộ nhớ native.
- Đối với bộ dữ liệu lớn, sử dụng `WorkbookDesigner` để truyền dữ liệu theo luồng thay vì tải toàn bộ một lúc.
- Sử dụng Java Flight Recorder để phân tích và phát hiện các điểm nghẽn trong quá trình tạo biểu đồ.

## Câu hỏi thường gặp

**Q: Tôi có thể tạo nhiều biểu đồ tròn trong cùng một workbook không?**  
A: Có, lặp lại các bước tạo biểu đồ cho mỗi phạm vi dữ liệu; mỗi biểu đồ là độc lập.

**Q: Aspose.Cells có hỗ trợ biểu đồ tròn 3‑D không?**  
A: Có; đặt loại biểu đồ thành `ChartType.PIE_3D` khi thêm biểu đồ.

**Q: Làm thế nào để áp dụng giao diện tùy chỉnh cho tất cả các biểu đồ?**  
A: Sử dụng phương thức `Workbook.setDefaultTheme` trước khi tạo bất kỳ biểu đồ nào.

**Q: Tôi có thể xuất workbook sang những định dạng tệp nào?**  
A: Hơn 30 định dạng, bao gồm XLSX, CSV, PDF và HTML.

**Q: Có cần giấy phép cho việc triển khai thương mại không?**  
A: Có, giấy phép hợp lệ sẽ loại bỏ watermark đánh giá và mở khóa đầy đủ chức năng.

## Kết luận
Bây giờ bạn đã có một công thức hoàn chỉnh, từ đầu đến cuối để **create pie chart java** với Aspose.Cells. Bằng cách làm theo các bước trên, bạn có thể tạo ra các biểu đồ tròn Excel chuyên nghiệp, tùy chỉnh màu sắc và tiêu đề, và nhúng chúng vào bất kỳ quy trình báo cáo nào. Khám phá các loại biểu đồ khác—cột, đường, radar—để mở rộng bộ công cụ trực quan hoá dữ liệu của bạn.

---

**Cập nhật lần cuối:** 2026-09-27  
**Đã kiểm tra với:** Aspose.Cells 24.10 for Java  
**Tác giả:** Aspose

## Hướng dẫn liên quan

- [Tùy chỉnh nhãn dữ liệu biểu đồ Excel bằng Aspose.Cells cho Java&#58; Hướng dẫn từng bước](/cells/java/charts-graphs/customize-chart-data-labels-aspose-cells-java/)
- [Tạo biểu đồ Excel động với Aspose.Cells Java&#58; Hướng dẫn toàn diện cho nhà phát triển](/cells/java/charts-graphs/aspose-cells-java-dynamic-excel-charts/)
- [Tạo và tùy chỉnh sổ làm việc Excel bằng Aspose.Cells Java&#58; Hướng dẫn từng bước](/cells/java/workbook-operations/create-customize-excel-workbooks-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}