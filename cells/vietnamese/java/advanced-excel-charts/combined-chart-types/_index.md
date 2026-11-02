---
date: 2026-09-02
description: Tìm hiểu cách xuất chart sang PNG, thêm data series, kết hợp line column
  chart, lưu workbook dưới dạng XLSX và thêm legend chart bằng Aspose.Cells for Java.
keywords:
- export chart to png
- combine line and column chart
- save workbook as xlsx
- generate chart image java
lastmod: 2026-09-02
linktitle: Xuất chart sang PNG và thêm data series cho combined chart
og_description: Xuất chart sang PNG với Aspose.Cells for Java, kết hợp line và column
  chart, thêm data series, và lưu workbook dưới dạng XLSX trong một hướng dẫn duy
  nhất.
og_image_alt: Developer guide showing combined line‑column chart export to PNG using
  Aspose.Cells for Java
og_title: Xuất chart sang PNG và thêm data series cho combined chart
schemas:
- author: Aspose
  dateModified: '2026-09-02'
  description: Learn how to export chart to PNG, add data series, combine line column
    chart, save workbook as XLSX and add legend chart using Aspose.Cells for Java.
  headline: Export chart to PNG and add data series for combined chart
  type: TechArticle
- description: Learn how to export chart to PNG, add data series, combine line column
    chart, save workbook as XLSX and add legend chart using Aspose.Cells for Java.
  name: Export chart to PNG and add data series for combined chart
  steps:
  - name: import aspose.cells classes
    text: '`Workbook` is Aspose.Cells’ core object that represents an entire Excel
      file in memory.'
  - name: create a new workbook
    text: '`Worksheet` represents a single sheet inside a `Workbook` and provides
      access to cells, rows, and charts.'
  - name: access the first worksheet
    text: '`Chart` is the object that holds all chart‑related settings, series, and
      rendering options.'
  - name: add a combined chart object to the worksheet
    text: We’ll start with a line chart and later add a column series to achieve a
      **combined line column chart** effect.
  - name: define the data ranges and add data series
    text: '`NSeries` is the collection that stores each data series for a chart. Adding
      a series links a range of cells to the chart. > **Pro tip:** The first parameter
      (`"A1:A5"`) is the range for the first series, and the second (`"B1:B5"`) creates
      a second series that will be combined with the first.'
  - name: set the category (X‑axis) data
    text: '`CategoryAxis` represents the horizontal axis of the chart, controlling
      the labels displayed along the X‑axis.'
  - name: set chart axis labels and title
    text: '`Title` sets the main title of the chart, and `Axis` objects represent
      the X and Y axes.'
  - name: add legend chart and adjust its position
    text: '`Legend` controls the placement and appearance of the series legend in
      the chart.'
  - name: save the workbook as an Excel file (XLSX)
    text: '`Workbook.save` writes the in‑memory workbook to a file in the specified
      format.'
  - name: export chart to PNG
    text: '`Chart.toImage` renders the chart as an image file in the chosen format.
      > The `chart.toImage` method **generates Excel chart** images that can be used
      in web pages, reports, or emails.'
  type: HowTo
- questions:
  - answer: 'Download the JAR from the official site and add it to your project’s
      classpath. The download link is: [Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/).'
    question: How do I install Aspose.Cells for Java?
  - answer: Yes, Aspose.Cells supports bar, pie, scatter, area, and many more chart
      types. Refer to the API documentation for the full list.
    question: Can I create other chart types besides line and column?
  - answer: A valid Aspose.Cells license is required for production deployments. A
      free trial is available for evaluation.
    question: Is a license required for production use?
  - answer: Use `chart.getNSeries().get(i).setAreaColor(Color.getRed())` (or similar)
      after adding the series.
    question: How can I change the colors of each series?
  - answer: 'Comprehensive documentation and additional samples are available at the
      Aspose reference site: [Aspose Cells Java reference documentation](https://reference.aspose.com/cells/java/).'
    question: Where can I find more code examples?
  type: FAQPage
second_title: Aspose.Cells Java Excel Processing API
tags:
- export chart to png
- Aspose.Cells
- Java Excel charts
title: Xuất chart sang PNG và thêm data series cho combined chart
url: /vi/java/advanced-excel-charts/combined-chart-types/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Xuất biểu đồ ra PNG và thêm chuỗi dữ liệu cho biểu đồ kết hợp

Trong hướng dẫn này bạn sẽ **thêm chuỗi dữ liệu** vào một workbook Excel, **kết hợp các yếu tố biểu đồ đường và cột**, và học cách **xuất biểu đồ ra PNG** bằng Aspose.Cells for Java. Chúng tôi sẽ hướng dẫn từng bước — từ thiết lập workbook, thêm biểu đồ vào worksheet, tùy chỉnh chú giải, đến **lưu workbook dưới dạng XLSX** và tạo ảnh PNG của biểu đồ. Khi hoàn thành, bạn sẽ có một biểu đồ kết hợp sẵn sàng để nhúng vào báo cáo hoặc bảng điều khiển.

## Câu trả lời nhanh
- **Thư viện nào tạo biểu đồ kết hợp?** Aspose.Cells for Java.  
- **Làm thế nào để thêm một chuỗi dữ liệu?** Gọi `chart.getNSeries().add(...)` với phạm vi thích hợp.  
- **Làm sao để xuất biểu đồ ra PNG?** Sử dụng `chart.toImage("chart.png", ImageFormat.getPng())`.  
- **Tôi có thể lưu workbook dưới định dạng nào?** Định dạng chuẩn `.xlsx` (lưu workbook dưới dạng XLSX).  
- **Có cần giấy phép cho môi trường production không?** Có — cần một giấy phép Aspose.Cells hợp lệ cho các triển khai production.

## Export chart to PNG trong Aspose.Cells là gì?
Việc xuất biểu đồ ra PNG tạo ra một hình ảnh raster của biểu đồ Excel có thể hiển thị trong trang web, báo cáo hoặc email mà không cần ứng dụng Excel. Phương pháp này ghi lại bố cục hình ảnh, màu sắc và các dấu dữ liệu một cách chính xác, tạo ra một tệp ảnh di động.

## Tại sao tạo biểu đồ kết hợp đường‑cột?
Biểu đồ kết hợp đường‑cột cho phép bạn hiển thị các bộ dữ liệu khác nhau với các dạng biểu diễn trực quan riêng (ví dụ: một chuỗi đường trên một chuỗi cột) trong một cửa sổ duy nhất. Cách tiếp cận này lý tưởng để so sánh xu hướng với tổng hợp, làm nổi bật mối tương quan, hoặc cung cấp những hiểu biết sâu hơn trong khi giữ kích thước hình ảnh nhỏ gọn.

## Yêu cầu trước
- Java Development Kit (JDK) 8 trở lên  
- Thư viện Aspose.Cells for Java (tải xuống từ liên kết bên dưới)  
- Kiến thức cơ bản về cú pháp Java và các khái niệm Excel  

## Bắt đầu

Đầu tiên, tải thư viện Aspose.Cells for Java từ trang chính thức:

[Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/)

Sau khi thêm JAR vào classpath của dự án, bạn có thể bắt đầu xây dựng biểu đồ.

### Bước 1: nhập các lớp aspose.cells
`Workbook` là đối tượng cốt lõi của Aspose.Cells đại diện cho toàn bộ tệp Excel trong bộ nhớ.  
```java
import com.aspose.cells.*;
```

### Bước 2: tạo một workbook mới
`Worksheet` đại diện cho một sheet duy nhất trong `Workbook` và cung cấp quyền truy cập vào các ô, hàng và biểu đồ.  
```java
Workbook workbook = new Workbook();
```

### Bước 3: truy cập worksheet đầu tiên
`Chart` là đối tượng chứa tất cả các cài đặt liên quan đến biểu đồ, chuỗi dữ liệu và tùy chọn render.  
```java
Worksheet worksheet = workbook.getWorksheets().get(0);
```

### Bước 4: thêm đối tượng biểu đồ kết hợp vào worksheet  
Chúng ta sẽ bắt đầu với một biểu đồ đường và sau đó thêm chuỗi cột để đạt được hiệu ứng **biểu đồ kết hợp đường‑cột**.  
```java
int chartIndex = worksheet.getCharts().add(ChartType.LINE, 0, 0, 20, 10);
Chart chart = worksheet.getCharts().get(chartIndex);
```

## Thêm dữ liệu vào biểu đồ

Bây giờ container biểu đồ đã tồn tại, chúng ta cần cung cấp dữ liệu cho nó.

### Bước 5: định nghĩa phạm vi dữ liệu và thêm chuỗi dữ liệu
`NSeries` là tập hợp lưu trữ mỗi chuỗi dữ liệu cho một biểu đồ. Thêm một chuỗi sẽ liên kết một phạm vi ô với biểu đồ.  
```java
Cells cells = worksheet.getCells();
chart.getNSeries().add("A1:A5", true);
chart.getNSeries().add("B1:B5", true);
```
> **Mẹo:** Tham số đầu tiên (`"A1:A5"`) là phạm vi cho chuỗi đầu tiên, và tham số thứ hai (`"B1:B5"`) tạo chuỗi thứ hai sẽ được kết hợp với chuỗi đầu.

### Bước 6: đặt dữ liệu danh mục (trục X)
`CategoryAxis` đại diện cho trục ngang của biểu đồ, điều khiển các nhãn hiển thị trên trục X.  
```java
chart.getNSeries().setCategoryData("C1:C5");
```

## Tùy chỉnh biểu đồ

Một biểu đồ tốt kể một câu chuyện. Hãy thêm tiêu đề, nhãn trục và chú giải rõ ràng.

### Bước 7: đặt nhãn trục và tiêu đề cho biểu đồ
`Title` đặt tiêu đề chính của biểu đồ, và các đối tượng `Axis` đại diện cho các trục X và Y.  
```java
chart.getTitle().setText("Combined Chart Example");
chart.getCategoryAxis().getTitle().setText("Categories");
chart.getValueAxis().getTitle().setText("Values");
```

### Bước 8: thêm chú giải cho biểu đồ và điều chỉnh vị trí
`Legend` kiểm soát vị trí và giao diện của chú giải chuỗi trong biểu đồ.  
```java
chart.getLegend().setPosition(LegendPositionType.BOTTOM);
chart.getLegend().setOverlay(true);
```

## Lưu và xuất biểu đồ

Sau khi tùy chỉnh, bạn sẽ muốn **lưu workbook dưới dạng XLSX** và đồng thời tạo một hình ảnh.

### Bước 9: lưu workbook dưới dạng tệp Excel (XLSX)
`Workbook.save` ghi workbook trong bộ nhớ ra tệp với định dạng đã chỉ định.  
```java
workbook.save("CombinedChart.xlsx");
```

### Bước 10: xuất biểu đồ ra PNG
`Chart.toImage` render biểu đồ thành tệp ảnh ở định dạng đã chọn.  
```java
chart.toImage("CombinedChart.png", ImageFormat.getPng());
```
> Phương thức `chart.toImage` **tạo ra hình ảnh biểu đồ Excel** có thể dùng trong trang web, báo cáo hoặc email.

## Các vấn đề thường gặp & khắc phục

| Vấn đề | Giải pháp |
|-------|----------|
| **Không có dữ liệu hiển thị** | Kiểm tra lại các phạm vi ô (`A1:A5`, `B1:B5`, `C1:C5`) thực sự chứa dữ liệu trước khi tạo biểu đồ. |
| **Chú giải chồng lên biểu đồ** | Đặt `chart.getLegend().setOverlay(false)` hoặc di chuyển chú giải tới vị trí khác (ví dụ: `RIGHT`). |
| **Tệp ảnh trống** | Đảm bảo biểu đồ có ít nhất một chuỗi và `chart.toImage` được gọi sau khi hoàn tất mọi tùy chỉnh. |
| **Lưu gây ra ngoại lệ** | Kiểm tra quyền ghi vào thư mục đích và chắc chắn tệp không đang mở trong Excel. |

## Câu hỏi thường gặp

**H: Làm sao để cài đặt Aspose.Cells for Java?**  
Đ: Tải JAR từ trang chính thức và thêm vào classpath của dự án. Liên kết tải xuống: [Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/).

**H: Tôi có thể tạo các loại biểu đồ khác ngoài đường và cột không?**  
Đ: Có, Aspose.Cells hỗ trợ biểu đồ thanh, bánh, phân tán, diện tích và nhiều loại khác. Tham khảo tài liệu API để biết danh sách đầy đủ.

**H: Cần giấy phép cho việc sử dụng trong môi trường production không?**  
Đ: Cần một giấy phép Aspose.Cells hợp lệ cho các triển khai production. Có bản dùng thử miễn phí để đánh giá.

**H: Làm sao thay đổi màu sắc của từng chuỗi?**  
Đ: Sử dụng `chart.getNSeries().get(i).setAreaColor(Color.getRed())` (hoặc tương tự) sau khi đã thêm chuỗi.

**H: Tôi có thể tìm thêm ví dụ mã nguồn ở đâu?**  
Đ: Tài liệu chi tiết và các mẫu bổ sung có sẵn tại trang tham khảo Aspose: [Aspose Cells Java reference documentation](https://reference.aspose.com/cells/java/).

---

**Cập nhật lần cuối:** 2026-09-02  
**Đã kiểm tra với:** Phiên bản mới nhất của Aspose.Cells for Java  
**Tác giả:** Aspose

## Các hướng dẫn liên quan

- [Cách Thêm Nhãn vào Biểu Đồ Excel Sử Dụng Aspose.Cells for Java](/cells/java/charts-graphs/adding-labels-to-charts-aspose-cells-java-tutorial/)
- [Cách Tạo Biểu Đồ Excel với Đường Xu hướng và Xuất ra Ảnh Sử Dụng Aspose.Cells for Java](/cells/java/advanced-excel-charts/trendline-analysis/)
- [Xuất Biểu Đồ Excel ra PDF Bằng Aspose.Cells for Java: Hướng Dẫn Kích Thước Trang Tùy Chỉnh](/cells/java/charts-graphs/export-excel-charts-pdf-aspose-cells-java/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}