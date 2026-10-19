---
date: 2026-09-02
description: Tìm hiểu cách tạo biểu đồ thác nước trong Excel bằng Java với Aspose.Cells,
  thiết lập phạm vi dữ liệu cho biểu đồ, tùy chỉnh nhãn và xuất ra XLSX.
keywords:
- create excel waterfall chart
- waterfall chart data labels
- Aspose.Cells Java chart
lastmod: 2026-09-02
linktitle: Biểu đồ Thác Nước
og_description: Tạo biểu đồ thác nước trong Excel bằng Aspose.Cells cho Java – thiết
  lập phạm vi dữ liệu cho biểu đồ, thêm nhãn dữ liệu và xuất ra XLSX trong vài bước.
og_image_alt: 'Tutorial: create excel waterfall chart with Aspose.Cells Java'
og_title: Tạo biểu đồ thác nước trong Excel bằng Aspose.Cells cho Java
schemas:
- author: Aspose
  dateModified: '2026-09-02'
  description: Learn how to create excel waterfall chart in Java with Aspose.Cells,
    set the chart data range, customize labels and export to XLSX.
  headline: Create excel waterfall chart with Aspose.Cells for Java
  type: TechArticle
- description: Learn how to create excel waterfall chart in Java with Aspose.Cells,
    set the chart data range, customize labels and export to XLSX.
  name: Create excel waterfall chart with Aspose.Cells for Java
  steps:
  - name: import Aspose.Cells
    text: The `com.aspose.cells` package contains all classes required for Excel manipulation,
      including workbook creation, worksheet handling, and chart generation.
  - name: initialize workbook and worksheet
    text: A **Workbook** represents an Excel file, and a **Worksheet** is a single
      sheet within that file. Creating these objects provides the canvas for both
      raw data and the chart.
  - name: enter data
    text: Column A holds category labels, while column B contains the numeric values
      for the waterfall. This layout matches the typical profit‑and‑loss flow used
      in financial analysis.
  - name: create the waterfall chart
    text: The **Chart** object creates a visual representation; setting its type to
      `ChartType.WATERFALL` configures it as a waterfall chart. Use the `add` method
      to set the chart data range for the series (`"B2:B6"`), and link the category
      axis to `"A2:A6"`.
  - name: save the workbook
    text: Saving the workbook writes the chart and data to the specified file format.
      Call `workbook.save("WaterfallChart.xlsx")` to generate an XLSX file, or change
      the format parameter to export to PDF, CSV, or HTML.
  type: HowTo
- questions:
  - answer: Use the `add` method on the chart’s series, passing the cell range that
      contains your values, e.g., `"B2:B6"`.
    question: How do I set the chart data range for a financial waterfall chart?
  - answer: Yes, call `workbook.save("WaterfallChart.pdf", SaveFormat.PDF);` to generate
      a PDF version.
    question: Can I export the workbook to PDF instead of XLSX?
  - answer: Extend the data range in both the values column and the category column,
      then update the `add` and `setCategoryData` calls accordingly.
    question: What if I need to create a waterfall chart with more categories?
  - answer: Iterate through the `Series` collection and set the `FillFormat` color
      based on each value’s sign; Aspose.Cells lets you apply conditional formatting
      programmatically.
    question: Is there a way to automatically format positive and negative bars?
  - answer: Yes. After modifying cell values, simply re‑save the workbook—the chart
      will reflect the new data automatically.
    question: Does Aspose.Cells support dynamic data updates for charts?
  type: FAQPage
second_title: Aspose.Cells Java Excel Processing API
tags:
- waterfall chart
- Aspose.Cells
- java excel charts
- excel automation
title: Tạo biểu đồ thác nước trong Excel bằng Aspose.Cells cho Java
url: /vi/java/advanced-excel-charts/waterfall-charts/
weight: 18
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Biểu đồ thác nước

## Giới thiệu về biểu đồ thác nước sử dụng Aspose.Cells cho Java

Trong tutorial này, bạn sẽ học cách **tạo biểu đồ thác nước Excel** và **đặt phạm vi dữ liệu cho biểu đồ** với Aspose.Cells cho Java. Biểu đồ thác nước chuyển một loạt các số dương và âm thành một câu chuyện trực quan rõ ràng, khiến chúng lý tưởng cho báo cáo tài chính, đánh giá hiệu suất bán hàng, và bất kỳ kịch bản nào bạn cần xem cách các mục riêng lẻ đóng góp vào tổng cộng.

## Câu trả lời nhanh
- **Biểu đồ thác nước là gì?** Một hình ảnh trực quan cho thấy cách một giá trị ban đầu được tăng và giảm bởi một loạt các giá trị trung gian, kết thúc bằng tổng cuối cùng.  
- **Thư viện nào được sử dụng?** Aspose.Cells cho Java.  
- **Tôi có cần giấy phép không?** Bản dùng thử miễn phí hoạt động cho phát triển; giấy phép thương mại cần thiết cho môi trường sản xuất.  
- **Có thể lưu tệp dưới dạng XLSX không?** Có – sử dụng `workbook.save("FileName.xlsx")`.  
- **Có phù hợp cho việc trực quan dữ liệu Java không?** Chắc chắn; Aspose.Cells cung cấp các tính năng biểu đồ phong phú mà không cần cài đặt Office.

## Biểu đồ thác nước là gì?
Biểu đồ thác nước hiển thị các đóng góp dương và âm theo thứ tự vào một giá trị bắt đầu, giúp bạn hiểu cách mỗi thành phần ảnh hưởng đến kết quả tổng thể. Bằng cách trực quan hóa lợi nhuận và lỗ lãi cạnh nhau, nó làm cho các luồng tài chính phức tạp trở nên dễ đọc ngay lập tức.

## Tại sao nên sử dụng Aspose.Cells cho Java để thêm biểu đồ thác nước?
Aspose.Cells cho phép bạn tạo biểu đồ Excel trên bất kỳ máy chủ, pipeline CI, hoặc máy tính để bàn nào mà không cần Microsoft Excel. Nó hỗ trợ **hơn 15 định dạng xuất** (XLSX, PDF, HTML, CSV, và hơn nữa), xử lý sổ làm việc với **hơn 500 dòng** trong chưa đầy một giây, và cung cấp khả năng kiểm soát lập trình cho mọi thành phần của biểu đồ—từ màu sắc đến nhãn dữ liệu.

## Yêu cầu trước
Trước khi chúng ta bắt đầu với mã, hãy chắc chắn rằng bạn đã có các yêu cầu sau:

- Aspose.Cells cho Java: Bạn cần cài đặt Aspose.Cells cho Java. Bạn có thể tải xuống từ trang phát hành Aspose.Cells cho Java: [Aspose.Cells for Java releases](https://releases.aspose.com/cells/java/).
- Môi trường phát triển Java: Đảm bảo bạn đã cài đặt Java trên hệ thống và có công cụ xây dựng (Maven/Gradle) sẵn sàng.

Bây giờ, hãy bắt đầu tạo biểu đồ thác nước từng bước.

## Cách đặt phạm vi dữ liệu cho biểu đồ thác nước trong Java
Tải một workbook mới, điền dữ liệu vào, thêm một đối tượng `Chart`, xác định phạm vi series, và cuối cùng lưu tệp. Quy trình này đơn giản: bạn tạo một workbook, điền các ô với danh mục và giá trị, tạo một biểu đồ, liên kết các phạm vi dữ liệu, và sau đó xuất workbook. Kết quả là một biểu đồ thác nước hoàn chỉnh, sẵn sàng sử dụng trong báo cáo hoặc bảng điều khiển.

### Bước 1: nhập Aspose.Cells
Gói `com.aspose.cells` chứa tất cả các lớp cần thiết cho việc thao tác Excel, bao gồm tạo workbook, xử lý worksheet và tạo biểu đồ.

### Bước 2: khởi tạo workbook và worksheet
**Workbook** đại diện cho một tệp Excel, và **Worksheet** là một sheet duy nhất trong tệp đó. Tạo các đối tượng này cung cấp nền cho cả dữ liệu thô và biểu đồ.

### Bước 3: nhập dữ liệu
Cột A chứa nhãn danh mục, trong khi cột B chứa các giá trị số cho biểu đồ thác nước. Bố cục này phù hợp với luồng lợi nhuận‑lỗ tiêu chuẩn được sử dụng trong phân tích tài chính.

### Bước 4: tạo biểu đồ thác nước
Đối tượng **Chart** tạo ra một biểu diễn trực quan; đặt loại của nó thành `ChartType.WATERFALL` cấu hình nó thành biểu đồ thác nước. Sử dụng phương thức `add` để đặt phạm vi dữ liệu cho series (`"B2:B6"`), và liên kết trục danh mục tới `"A2:A6"`.

### Bước 5: lưu workbook
Lưu workbook sẽ ghi biểu đồ và dữ liệu vào định dạng tệp đã chỉ định. Gọi `workbook.save("WaterfallChart.xlsx")` để tạo tệp XLSX, hoặc thay đổi tham số định dạng để xuất ra PDF, CSV, hoặc HTML.

## Các vấn đề thường gặp và giải pháp
- **Biểu đồ hiển thị trống** – Kiểm tra rằng các tham chiếu phạm vi dữ liệu (`B2:B6` và `A2:A6`) khớp với các ô thực tế chứa giá trị và danh mục của bạn.  
- **Giá trị âm không hiển thị đúng** – Đảm bảo loại series được đặt thành `ChartType.WATERFALL`; các loại biểu đồ khác xử lý giá trị âm khác nhau.  
- **Tệp không mở được trong Excel** – Sử dụng phiên bản Aspose.Cells mới nhất và xác nhận phần mở rộng tệp khớp với định dạng (`.xlsx` cho Excel).

## Câu hỏi thường gặp
### Làm thế nào tôi có thể tùy chỉnh giao diện của biểu đồ thác nước?
Bạn có thể sửa đổi các thuộc tính như `Chart.getSeries().get(0).getFillFormat().setColor(Color.getRed())` để thay đổi màu thanh, bật nhãn dữ liệu với `setShowDataLabels(true)`, và điều chỉnh tiêu đề trục qua `getCategoryAxis().setTitle("Stage")`. Tham khảo API Aspose.Cells cung cấp danh sách đầy đủ các tùy chọn có thể tùy chỉnh.

### Tôi có thể tạo nhiều biểu đồ thác nước trong cùng một worksheet không?
Có. Sau khi thêm biểu đồ đầu tiên, lặp lại các bước tạo biểu đồ với một phạm vi dữ liệu khác và một đối tượng `Chart` mới. Mỗi biểu đồ là độc lập và có thể được đặt ở bất kỳ vị trí nào trên sheet.

### Aspose.Cells có tương thích với các môi trường phát triển Java khác nhau không?
Chắc chắn. Thư viện hoạt động với Eclipse, IntelliJ IDEA, NetBeans, và bất kỳ hệ thống xây dựng nào hỗ trợ Maven hoặc Gradle. Không cần plugin bổ sung.

### Tôi có thể thêm series dữ liệu bổ sung vào biểu đồ thác nước của mình không?
Bạn có thể thêm nhiều series bằng cách gọi `chart.getNSeries().add("C2:C6", true)` và cấu hình từng series riêng biệt. Điều này cho phép bạn so sánh nhiều kịch bản cạnh nhau.

### Tôi có thể tìm thêm tài nguyên và ví dụ cho Aspose.Cells cho Java ở đâu?
Khám phá tài liệu đầy đủ tại tham chiếu API Aspose.Cells Java: [Aspose.Cells Java API reference](https://reference.aspose.com/cells/java/).

## Câu hỏi thường gặp
**Q: Làm thế nào để đặt phạm vi dữ liệu cho biểu đồ thác nước tài chính?**  
A: Sử dụng phương thức `add` trên series của biểu đồ, truyền phạm vi ô chứa giá trị của bạn, ví dụ, `"B2:B6"`.

**Q: Tôi có thể xuất workbook ra PDF thay vì XLSX không?**  
A: Có, gọi `workbook.save("WaterfallChart.pdf", SaveFormat.PDF);` để tạo phiên bản PDF.

**Q: Nếu tôi cần tạo biểu đồ thác nước với nhiều danh mục hơn thì sao?**  
A: Mở rộng phạm vi dữ liệu trong cả cột giá trị và cột danh mục, sau đó cập nhật các lời gọi `add` và `setCategoryData` cho phù hợp.

**Q: Có cách nào để tự động định dạng các thanh dương và âm không?**  
A: Duyệt qua bộ sưu tập `Series` và đặt màu `FillFormat` dựa trên dấu của mỗi giá trị; Aspose.Cells cho phép bạn áp dụng định dạng có điều kiện bằng lập trình.

**Q: Aspose.Cells có hỗ trợ cập nhật dữ liệu động cho biểu đồ không?**  
A: Có. Sau khi sửa đổi giá trị ô, chỉ cần lưu lại workbook—biểu đồ sẽ tự động phản ánh dữ liệu mới.

---

**Cập nhật lần cuối:** 2026-09-02  
**Được kiểm tra với:** Aspose.Cells cho Java (mới nhất)  
**Tác giả:** Aspose  









```java
import com.aspose.cells.*;
```

```java
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.getWorksheets().get(0);
```

```java
Cells cells = worksheet.getCells();

// Insert data
cells.get("A1").putValue("Categories");
cells.get("A2").putValue("Start");
cells.get("A3").putValue("Positive Value 1");
cells.get("A4").putValue("Negative Value 1");
cells.get("A5").putValue("Positive Value 2");
cells.get("A6").putValue("End");

cells.get("B1").putValue("Values");
cells.get("B2").putValue(0);
cells.get("B3").putValue(20);
cells.get("B4").putValue(-10);
cells.get("B5").putValue(15);
cells.get("B6").putValue(25);
```

```java
int chartIndex = worksheet.getCharts().add(ChartType.WATERFALL, 5, 0, 15, 5);
Chart waterfallChart = worksheet.getCharts().get(chartIndex);
waterfallChart.getNSeries().add("B2:B6", true);
waterfallChart.getNSeries().setCategoryData("A2:A6");
```

```java
workbook.save("WaterfallChart.xlsx");
```

## Hướng dẫn liên quan

- [Tùy chỉnh nhãn dữ liệu biểu đồ Excel bằng Aspose.Cells cho Java: Hướng dẫn từng bước](/cells/java/charts-graphs/customize-chart-data-labels-aspose-cells-java/)
- [Thêm nhãn dữ liệu vào biểu đồ Excel với Aspose.Cells Java](/cells/java/advanced-excel-charts/chart-interactivity/)
- [Cách tạo và xuất biểu đồ trong Java sử dụng Aspose.Cells: Hướng dẫn đầy đủ](/cells/java/charts-graphs/aspose-cells-java-create-export-charts/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}