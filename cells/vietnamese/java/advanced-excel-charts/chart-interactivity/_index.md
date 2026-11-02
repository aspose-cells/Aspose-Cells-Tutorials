---
date: 2026-08-21
description: Tìm hiểu cách thêm tooltip, data labels và thay đổi loại biểu đồ trong
  biểu đồ Excel bằng Aspose.Cells for Java – hướng dẫn từng bước với các ví dụ tương
  tác.
keywords:
- how to add tooltips
- how to change chart type
- how to add data labels
lastmod: 2026-08-21
linktitle: Thay đổi loại biểu đồ Excel
og_description: Tìm hiểu cách thêm tooltip, data labels và thay đổi loại biểu đồ trong
  biểu đồ Excel bằng Aspose.Cells for Java – hướng dẫn từng bước với các ví dụ tương
  tác.
og_image_alt: 'Developer guide: Adding tooltips and data labels to Excel charts with
  Aspose.Cells for Java'
og_title: Cách thêm tooltip và data labels vào biểu đồ Excel trong Java
schemas:
- author: Aspose
  dateModified: '2026-08-21'
  description: Learn how to add tooltips, data labels, and change chart type in Excel
    charts using Aspose.Cells for Java – step‑by‑step guide with interactive examples.
  headline: How to add tooltips and data labels to Excel charts in Java
  type: TechArticle
- questions:
  - answer: You need to create a new chart with the desired `ChartType`. Aspose.Cells
      does not provide an in‑place type conversion, so remove the old chart and add
      a new one.
    question: How can I change the chart type after it’s created?
  - answer: Yes. Use the `DataLabel` properties such as `setFontSize`, `setFontColor`,
      and `setBackgroundColor` to style the tooltip text.
    question: Can I customize the appearance of tooltips?
  - answer: Export the workbook to an HTML or XLSX file and use JavaScript on the
      client side to capture click events on chart elements.
    question: How do I handle user interactions in a web application?
  - answer: Visit the [Aspose.Cells Java API Reference](https://reference.aspose.com/cells/java/)
      for a full list of chart‑related classes and methods.
    question: Where can I find more examples and documentation?
  type: FAQPage
second_title: Aspose.Cells Java Excel Processing API
tags:
- Aspose.Cells
- Java chart
- Excel interactivity
- tooltips
- data labels
title: Cách thêm tooltip và data labels vào biểu đồ Excel trong Java
url: /vi/java/advanced-excel-charts/chart-interactivity/
weight: 19
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Thêm nhãn dữ liệu vào biểu đồ Excel và thay đổi loại biểu đồ – Aspose.Cells Java

Biểu đồ tương tác mang lại cho báo cáo Excel của bạn mức độ hiểu sâu mới, và **cách thêm tooltip** giúp thông tin ngay lập tức có thể đọc được. Trong hướng dẫn này, bạn sẽ học cách **thêm nhãn dữ liệu vào biểu đồ Excel**, **thay đổi loại biểu đồ**, và tạo các giải pháp Java tương tác với Aspose.Cells. Chúng tôi cũng sẽ chỉ cho bạn cách thêm tooltip và một siêu liên kết drill‑down đơn giản để khán giả của bạn có thể khám phá dữ liệu một cách chi tiết.

## Câu trả lời nhanh
- **Thư viện nào được sử dụng?** Aspose.Cells for Java  
- **Tôi có thể thay đổi loại biểu đồ không?** Yes – just modify the `ChartType` enum when you create the chart.  
- **Làm thế nào để thêm tooltip vào biểu đồ?** Use the data‑label API (`setHasDataLabels(true)`) and enable value display.  
- **Có hỗ trợ drill‑down không?** You can attach hyperlinks to data points for basic drill‑down behavior.  
- **Yêu cầu tiên quyết?** Java IDE, Aspose.Cells JAR, and an Excel file with sample data.

## Cách thêm tooltip là gì?
**Cách thêm tooltip** đề cập đến quá trình bật văn bản khi di chuột lên (hover‑over) hiển thị giá trị của điểm dữ liệu hoặc thông tin tùy chỉnh trên biểu đồ Excel. Trong Aspose.Cells, điều này được thực hiện thông qua cài đặt nhãn dữ liệu của biểu đồ. Tooltip giúp người dùng nhanh chóng hiểu dữ liệu mà không làm lộn xộn biểu đồ, và chúng có thể được tùy chỉnh về phông chữ, màu sắc và định dạng.

## Tại sao nên sử dụng biểu đồ tương tác với Aspose.Cells?
Aspose.Cells hỗ trợ **hơn 50 định dạng nhập và xuất**—bao gồm XLSX, CSV, PDF và HTML—và có thể xử lý sổ làm việc với **hơn 1 000 sheet** mà không cần tải toàn bộ tệp vào bộ nhớ, cung cấp việc tạo biểu đồ nhanh chóng phía máy chủ cho báo cáo doanh nghiệp. Biểu đồ tương tác cũng cho phép nhúng siêu liên kết, cập nhật dữ liệu động và xuất ra các định dạng thân thiện với web, làm cho chúng trở nên lý tưởng cho bảng điều khiển và cổng báo cáo.

## Yêu cầu tiên quyết

Trước khi bắt đầu, hãy chắc chắn rằng bạn có những thứ sau:

- Môi trường phát triển Java (JDK 8+ được khuyến nghị)  
- Thư viện Aspose.Cells cho Java (tải xuống từ [trang tải Aspose.Cells cho Java](https://releases.aspose.com/cells/java/))  
- Một sổ làm việc mẫu (`data.xlsx`) chứa dữ liệu bạn muốn trực quan hoá  

## Bước 1: thiết lập dự án Java của bạn

1. Tạo một dự án Java mới trong IDE ưa thích của bạn (IntelliJ IDEA, Eclipse, v.v.).  
2. Thêm file JAR Aspose.Cells vào đường dẫn xây dựng của dự án hoặc các phụ thuộc Maven/Gradle.  

## Bước 2: tải dữ liệu

Để làm việc với biểu đồ, trước tiên bạn cần một sổ làm việc được tải vào bộ nhớ.

`Workbook` đại diện cho một tệp Excel, và `Worksheet` đại diện cho một sheet duy nhất trong tệp đó.

```java
// Load the Excel file
Workbook workbook = new Workbook("data.xlsx");
Worksheet worksheet = workbook.getWorksheets().get(0);
```

## Cách thay đổi loại biểu đồ trong Aspose.Cells?

Tạo một biểu đồ mới với enum `ChartType` mong muốn; Aspose.Cells không thay đổi loại của biểu đồ hiện có tại chỗ, vì vậy bạn phải thêm một biểu đồ mới đúng loại và tùy chọn loại bỏ biểu đồ cũ. Cách tiếp cận này đảm bảo rằng tất cả các series và trục được xây dựng lại chính xác cho biểu diễn hình ảnh mới.

## Bước 3: tạo biểu đồ (và thay đổi loại của nó)

Bạn có thể chọn bất kỳ loại biểu đồ nào phù hợp với phân tích của mình. Dưới đây chúng tôi tạo một **biểu đồ cột**, nhưng bạn có thể dễ dàng chuyển sang biểu đồ đường, tròn, hoặc thanh bằng cách thay đổi enum `ChartType`.

`Chart` cung cấp các phương thức để cấu hình cách hiển thị dữ liệu trong worksheet.

```java
// Create a column chart
int chartIndex = worksheet.getCharts().add(ChartType.COLUMN, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);
```

> **Mẹo chuyên nghiệp:** Để **thay đổi loại biểu đồ Excel**, thay thế `ChartType.COLUMN` bằng `ChartType.LINE`, `ChartType.PIE`, v.v.

## Cách thêm tooltip vào biểu đồ Excel?

Tải biểu đồ của bạn, bật nhãn dữ liệu và đặt cờ `showValue`. Tooltip sẽ hiển thị giá trị ô nền mỗi khi người dùng di chuột lên một điểm dữ liệu trong tệp Excel đã render hoặc trong chế độ xem HTML. Bạn cũng có thể tùy chỉnh phông chữ, màu sắc và nền của tooltip để phù hợp với phong cách báo cáo.

Lớp `DataLabel` kiểm soát giao diện và nội dung của nhãn dữ liệu, đồng thời cũng đóng vai trò là tooltip.

```java
// Enable tooltips for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowValue(true);
```

## Bước 4: thêm tính tương tác

### 4.1. Thêm tooltip (thêm tooltip vào biểu đồ)

Tooltip xuất hiện khi người dùng di chuột lên một điểm dữ liệu. Đoạn mã sau bật nhãn dữ liệu và hiển thị giá trị dưới dạng tooltip.

```java
// Enable data labels for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowLabelAsDataCallout(true);
```

### 4.2. Thêm nhãn dữ liệu – **thêm nhãn dữ liệu vào biểu đồ excel**

Nhãn dữ liệu cung cấp một dấu hiệu trực quan cố định trên biểu đồ. Bạn có thể hiển thị chúng dưới dạng callout để dễ đọc hơn.

Lớp `DataLabel` kiểm soát giao diện của nhãn trên mỗi series. Bằng cách gọi `setHasDataLabels(true)` và cấu hình các thuộc tính như `setShowValue(true)`, bạn nhúng giá trị số trực tiếp lên biểu đồ, làm cho nó ngay lập tức hiển thị mà không cần tương tác. Các tùy chọn bổ sung cho phép bạn hiển thị tên series, phần trăm, hoặc văn bản tùy chỉnh để cung cấp ngữ cảnh phong phú hơn.

> **Tại sao lại thêm nhãn dữ liệu?** Việc đưa nhãn dữ liệu trực tiếp lên biểu đồ loại bỏ nhu cầu người dùng phải di chuột hoặc đoán giá trị, cải thiện độ rõ ràng của báo cáo.

### 4.3. Thực hiện drill‑down (siêu liên kết trên một điểm dữ liệu)

Cách đơn giản để thêm khả năng drill‑down là gắn một siêu liên kết vào một điểm cụ thể. Nhấp vào điểm đó sẽ mở một trang web với thông tin chi tiết.

Lớp `Hyperlink` gắn một liên kết có thể nhấp vào vào phần tử biểu đồ, cho phép điều hướng drill‑down.

```java
// Add a hyperlink to a data point
String url = "https://example.com/data-details";
chart.getNSeries().get(0).getPoints().get(0).getHyperlinks().add(url);
```

## Cách thêm nhãn dữ liệu vào biểu đồ Excel?

Lớp `DataLabel` kiểm soát giao diện của nhãn trên mỗi series. Bằng cách gọi `setHasDataLabels(true)` và cấu hình các thuộc tính như `setShowValue(true)`, bạn nhúng giá trị số trực tiếp lên biểu đồ, làm cho nó ngay lập tức hiển thị mà không cần tương tác. Các tùy chọn bổ sung cho phép bạn hiển thị tên series, phần trăm, hoặc văn bản tùy chỉnh để cung cấp ngữ cảnh phong phú hơn.

## Bước 5: lưu sổ làm việc

Sau khi cấu hình biểu đồ, lưu sổ làm việc để các tính năng tương tác được lưu trong tệp đầu ra.

Gọi `workbook.save` sẽ ghi sổ làm việc đã sửa đổi vào một tệp ở định dạng đã chọn.

```java
// Save the workbook
workbook.save("interactive_chart_output.xlsx");
```

## Các vấn đề thường gặp & giải pháp

| Vấn đề | Giải pháp |
|-------|----------|
| **Tooltip không hiển thị** | Đảm bảo `setHasDataLabels(true)` được gọi trước khi cấu hình `setShowValue(true)`. |
| **Siêu liên kết không thể nhấp** | Xác minh định dạng đầu ra hỗ trợ siêu liên kết (ví dụ: XLSX, không phải CSV). |
| **Loại biểu đồ không thay đổi** | Kiểm tra lại bạn đã sửa đổi enum `ChartType` đúng khi thêm biểu đồ. |

## Câu hỏi thường gặp

**Q: Làm thế nào tôi có thể thay đổi loại biểu đồ sau khi nó đã được tạo?**  
A: Bạn cần tạo một biểu đồ mới với `ChartType` mong muốn. Aspose.Cells không cung cấp chuyển đổi loại tại chỗ, vì vậy hãy loại bỏ biểu đồ cũ và thêm một biểu đồ mới.

**Q: Tôi có thể tùy chỉnh giao diện của tooltip không?**  
A: Có. Sử dụng các thuộc tính của `DataLabel` như `setFontSize`, `setFontColor`, và `setBackgroundColor` để tạo kiểu cho văn bản tooltip.

**Q: Làm thế nào tôi xử lý tương tác người dùng trong ứng dụng web?**  
A: Xuất sổ làm việc ra tệp HTML hoặc XLSX và sử dụng JavaScript phía client để bắt sự kiện click trên các phần tử biểu đồ.

**Q: Tôi có thể tìm thêm ví dụ và tài liệu ở đâu?**  
A: Truy cập [Aspose.Cells Java API Reference](https://reference.aspose.com/cells/java/) để xem danh sách đầy đủ các lớp và phương thức liên quan đến biểu đồ.

## Kết luận

Bây giờ bạn đã biết cách **thêm nhãn dữ liệu vào biểu đồ Excel**, **thay đổi loại biểu đồ Excel**, **tạo các giải pháp biểu đồ Java tương tác**, và làm phong phú chúng bằng tooltip, nhãn dữ liệu, và siêu liên kết drill‑down bằng Aspose.Cells cho Java. Những cải tiến này làm cho báo cáo Excel của bạn trở nên hấp dẫn và sâu sắc hơn đối với người dùng cuối.

---

**Cập nhật lần cuối:** 2026-08-21  
**Kiểm thử với:** Aspose.Cells for Java 24.12  
**Tác giả:** Aspose

## Hướng dẫn liên quan

- [Cách sửa đổi biểu đồ Excel và nhãn dữ liệu bằng Aspose.Cells cho Java](/cells/java/charts-graphs/aspose-cells-java-modify-excel-charts-data-labels/)
- [Trích xuất nhãn trục biểu đồ Excel bằng Aspose.Cells Java: Hướng dẫn toàn diện](/cells/java/charts-graphs/aspose-cells-java-excel-chart-axis-labels/)
- [Tạo biểu đồ bong bóng trong Excel bằng Aspose.Cells cho Java: Hướng dẫn từng bước](/cells/java/charts-graphs/aspose-cells-java-create-bubble-charts/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}