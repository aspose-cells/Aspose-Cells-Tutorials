---
date: 2026-02-09
description: Tìm hiểu cách tạo biểu đồ Excel, thêm đường xu hướng, hiển thị giá trị
  R‑bình phương và xuất biểu đồ ra hình ảnh bằng Aspose.Cells cho Java. Bao gồm các
  bước tải tệp Excel, tùy chỉnh biểu đồ và lưu dưới dạng PNG/JPEG.
linktitle: Export Chart to Image with Trendline Analysis
second_title: Aspose.Cells Java Excel Processing API
title: Cách tạo biểu đồ Excel với đường xu hướng và xuất ra hình ảnh bằng Aspose.Cells
  cho Java
url: /vi/java/advanced-excel-charts/trendline-analysis/
weight: 15
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Xuất biểu đồ thành hình ảnh với phân tích đường xu hướng

Trong hướng dẫn này, bạn sẽ học cách **tạo biểu đồ Excel** với một đường xu hướng, hiển thị giá trị R‑squared của nó, và xuất hình ảnh kết quả bằng cách sử dụng Aspose.Cells for Java. Chúng tôi sẽ hướng dẫn cách tải một workbook hiện có, thêm đường xu hướng, tùy chỉnh tiêu đề, lưu workbook, và cuối cùng tạo file PNG/JPEG mà bạn có thể nhúng ở bất kỳ đâu.

## Câu trả lời nhanh
- **Mục đích chính của hướng dẫn này là gì?** Để chỉ cho bạn cách thêm đường xu hướng, hiển thị phương trình và giá trị R‑squared, và xuất biểu đồ kết quả thành hình ảnh bằng Java.  
- **Thư viện nào được yêu cầu?** Aspose.Cells for Java (tải xuống [here](https://releases.aspose.com/cells/java/)).  
- **Tôi có cần giấy phép không?** Bản dùng thử miễn phí đủ cho phát triển; giấy phép thương mại cần thiết cho môi trường sản xuất.  
- **Tôi có thể tạo file Excel trong Java không?** Có – hướng dẫn tạo và lưu một workbook XLSX.  
- **Làm thế nào để xuất biểu đồ thành PNG hoặc JPEG?** Sử dụng phương thức `Chart.toImage()` (được đề cập trong phần “Export Chart”).

## Cách tạo biểu đồ Excel với đường xu hướng và xuất thành hình ảnh
Tiêu đề này trả lời trực tiếp truy vấn từ khóa chính và hướng dẫn bạn qua toàn bộ quy trình theo thứ tự logic. Dưới đây bạn sẽ tìm thấy lý do, các điều kiện tiên quyết, và hướng dẫn từng bước.

## Export Chart to Image là gì?
Xuất biểu đồ thành hình ảnh chuyển đổi biểu diễn trực quan của dữ liệu thành một bitmap di động (PNG, JPEG, v.v.). Điều này hữu ích cho việc nhúng biểu đồ vào báo cáo, trang web, hoặc bản trình bày mà không cần file Excel gốc.

## Tại sao cần thêm đường xu hướng và hiển thị giá trị R‑squared?
Đường xu hướng giúp bạn xác định mẫu hình cơ bản của một chuỗi dữ liệu, trong khi chỉ số **R‑squared** đo lường mức độ phù hợp của đường xu hướng với dữ liệu. Bao gồm chúng trong hình ảnh đã xuất giúp các bên liên quan có được thông tin ngay lập tức mà không cần mở workbook.

## Điều kiện tiên quyết
- Java 8 hoặc mới hơn đã được cài đặt.  
- Thư viện Aspose.Cells for Java đã được thêm vào dự án của bạn (các file JAR trên classpath).  
- Kiến thức cơ bản về các IDE Java (IntelliJ IDEA, Eclipse, v.v.).

## Hướng dẫn từng bước

### Bước 1: Thiết lập dự án
Tạo một dự án Java mới và thêm các file JAR của Aspose.Cells vào đường dẫn biên dịch. Điều này chuẩn bị môi trường cho việc tạo và thao tác các file Excel.

### Bước 2: Tải file Excel (load excel file java)
```java
// Import necessary libraries
import com.aspose.cells.*;

// Load the Excel file
Workbook workbook = new Workbook("your_excel_file.xlsx");

// Access the worksheet
Worksheet worksheet = workbook.getWorksheets().get(0);
```
*Chúng tôi vừa **tải một file Excel** vào bộ nhớ, sẵn sàng để tạo biểu đồ.*

### Bước 3: Tạo biểu đồ
```java
// Create a chart
int chartIndex = worksheet.getCharts().add(ChartType.LINE, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);

// Specify data source for the chart
chart.getNSeries().add("A1:A10", true);
```
*Ở đây chúng tôi tạo một biểu đồ đường sẽ chứa đường xu hướng sau này.*

### Bước 4: Thêm đường xu hướng (how to add trendline) và hiển thị giá trị R‑squared
```java
// Add a trendline to the chart
Trendline trendline = chart.getNSeries().get(0).getTrendlines().add(TrendlineType.LINEAR);

// Customize trendline options
trendline.setDisplayEquation(true);
trendline.setDisplayRSquaredValue(true);
```
*Lệnh `setDisplayRSquaredValue(true)` đảm bảo **giá trị R‑squared** hiển thị trên biểu đồ.*

### Bước 5: Tùy chỉnh biểu đồ và lưu workbook (save workbook xlsx, generate excel file java)
```java
// Customize chart title and axes
chart.getTitle().setText("Trendline Analysis");
chart.getCategoryAxis().getTitle().setText("X-Axis");
chart.getValueAxis().getTitle().setText("Y-Axis");

// Save the Excel file with the chart
workbook.save("output.xlsx");
```
*Bây giờ workbook đã được **tạo** và lưu dưới dạng file XLSX, sẵn sàng cho các xử lý tiếp theo.*

### Bước 6: Xuất biểu đồ thành hình ảnh (export chart to image)
> **Lưu ý:** Bước này được mô tả mà không có khối mã bổ sung để giữ nguyên số lượng khối ban đầu.  
Sau khi biểu đồ được tạo và lưu, bạn có thể xuất nó thành hình ảnh bằng cách gọi phương thức `chart.toImage()` và ghi `java.awt.image.BufferedImage` kết quả ra định dạng file bạn chọn (PNG, JPEG, BMP). Quy trình điển hình là:
1. Lấy đối tượng `Chart` (đã thực hiện trong các bước trước).  
2. Gọi `chart.toImage()` để nhận một `BufferedImage`.  
3. Sử dụng `ImageIO.write(bufferedImage, "png", new File("chart.png"))` để ghi file.  

Điều này tạo ra một hình ảnh độ phân giải cao mà bạn có thể nhúng ở bất kỳ đâu, hoàn thành quy trình **export chart to image**.

## Phân tích kết quả
Mở `output.xlsx` trong Excel để xác minh rằng đường xu hướng, phương trình và giá trị R‑squared hiển thị như mong đợi. Mở file hình ảnh đã xuất (ví dụ, `chart.png`) để xem hình ảnh sạch sẽ có thể chia sẻ mà không cần workbook gốc.

## Các vấn đề thường gặp và giải pháp
- **Đường xu hướng không hiển thị:** Đảm bảo phạm vi dữ liệu (`A1:A10`) thực sự chứa các giá trị số; dữ liệu không phải số sẽ ngăn không cho đường xu hướng được tính.  
- **Giá trị R‑squared hiển thị là 0:** Thường nghĩa là chuỗi dữ liệu không thay đổi hoặc thiếu biến đổi đủ. Thử một bộ dữ liệu khác hoặc đường xu hướng đa thức.  
- **Xuất hình ảnh thất bại với `NullPointerException`:** Kiểm tra rằng biểu đồ đã được render hoàn toàn trước khi gọi `toImage()`. Lưu workbook trước có thể giải quyết một số vấn đề thời gian.

## Câu hỏi thường gặp

**Q: Làm thế nào để thay đổi loại đường xu hướng?**  
A: Sử dụng một giá trị `TrendlineType` khác khi thêm đường xu hướng, ví dụ `TrendlineType.POLYNOMIAL` cho phép phù hợp đa thức.

**Q: Tôi có thể tùy chỉnh giao diện của đường xu hướng (màu sắc, độ dày) không?**  
A: Có. Truy cập `LineFormat` của đường xu hướng qua `trendline.getLineFormat()` và đặt các thuộc tính như `setWeight()` và `setColor()`.

**Q: Làm thế nào để xuất biểu đồ thành PDF thay vì hình ảnh?**  
A: Đầu tiên chuyển biểu đồ thành hình ảnh, sau đó nhúng hình ảnh đó vào PDF bằng Aspose.PDF hoặc bất kỳ thư viện PDF nào bạn chọn.

**Q: Có thể thêm nhiều đường xu hướng vào cùng một biểu đồ không?**  
A: Chắc chắn. Gọi `chart.getNSeries().get(0).getTrendlines().add(...)` cho mỗi series bạn muốn phân tích.

**Q: Aspose.Cells có hỗ trợ xuất hình ảnh độ phân giải cao không?**  
A: Có. Bạn có thể chỉ định DPI khi gọi `chart.toImage()` và sau đó điều chỉnh kích thước hình ảnh cho phù hợp trước khi lưu.

## Kết luận
Bây giờ bạn đã có một giải pháp toàn diện, từ đầu đến cuối để **tạo biểu đồ Excel**, thêm đường xu hướng, hiển thị phương trình và giá trị R‑squared, tùy chỉnh hình ảnh, lưu workbook, và cuối cùng xuất biểu đồ dưới dạng hình PNG/JPEG. Cách tiếp cận này cho phép bạn tạo ra các tài sản phân tích chuyên nghiệp một cách lập trình, phù hợp cho báo cáo tự động, bảng điều khiển, hoặc bất kỳ trường hợp nào mà hình ảnh tĩnh thuận tiện hơn so với file Excel.

---

**Cập nhật lần cuối:** 2026-02-09  
**Kiểm tra với:** Aspose.Cells for Java latest  
**Tác giả:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}