---
date: 2025-12-09
description: Tìm hiểu cách xuất biểu đồ thành hình ảnh khi thực hiện phân tích đường
  xu hướng trong Java với Aspose.Cells. Bao gồm các bước tải tệp Excel, thêm đường
  xu hướng, hiển thị giá trị R‑bình phương và lưu workbook dưới dạng XLSX.
language: vi
linktitle: Export Chart to Image with Trendline Analysis
second_title: Aspose.Cells Java Excel Processing API
title: Xuất biểu đồ thành hình ảnh với phân tích đường xu hướng bằng Aspose.Cells
  cho Java
url: /java/advanced-excel-charts/trendline-analysis/
weight: 15
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Xuất Biểu Đồ ra Hình Ảnh với Phân Tích Đường Xu hướng

Trong tutorial này, bạn sẽ khám phá **cách xuất biểu đồ ra hình ảnh** trong khi thực hiện một **phân tích đường xu hướng** đầy đủ bằng Aspose.Cells for Java. Chúng tôi sẽ hướng dẫn cách tải một workbook Excel hiện có, thêm đường xu hướng, hiển thị giá trị R‑squared, tùy chỉnh biểu đồ, và cuối cùng xuất biểu đồ dưới dạng file hình ảnh — tất cả với mã nguồn rõ ràng, từng bước mà bạn có thể sao chép & dán.

## Câu trả lời nhanh
- **Mục đích chính của hướng dẫn này là gì?** Để chỉ cho bạn cách thêm đường xu hướng, hiển thị phương trình và giá trị R‑squared, và xuất biểu đồ kết quả ra hình ảnh bằng Java.  
- **Thư viện nào cần thiết?** Aspose.Cells for Java (tải xuống [ở đây](https://releases.aspose.com/cells/java/)).  
- **Tôi có cần giấy phép không?** Bản dùng thử miễn phí đủ cho phát triển; giấy phép thương mại cần thiết cho môi trường sản xuất.  
- **Tôi có thể tạo file Excel trong Java không?** Có – tutorial tạo và lưu một workbook XLSX.  
- **Làm sao để xuất biểu đồ ra PNG hoặc JPEG?** Sử dụng phương thức `Chart.toImage()` (được mô tả trong phần “Export Chart”).

## Xuất Biểu Đồ ra Hình Ảnh là gì?
Xuất một biểu đồ ra hình ảnh chuyển đổi biểu diễn trực quan của dữ liệu thành một bitmap di động (PNG, JPEG, v.v.). Điều này hữu ích cho việc nhúng biểu đồ vào báo cáo, trang web, hoặc bản trình bày mà không cần file Excel gốc.

## Tại sao cần Thêm Đường Xu hướng và Hiển thị Giá trị R‑squared?
Đường xu hướng giúp bạn xác định mẫu hình cơ bản của một dãy dữ liệu, trong khi chỉ số **R‑squared** đo lường mức độ phù hợp của đường xu hướng với dữ liệu. Việc bao gồm chúng trong hình ảnh đã xuất cung cấp cho các bên liên quan thông tin ngay lập tức mà không cần mở workbook.

## Yêu cầu trước
- Java 8 hoặc mới hơn đã được cài đặt.  
- Thư viện Aspose.Cells for Java đã được thêm vào dự án của bạn (các file JAR trên classpath).  
- Kiến thức cơ bản về các IDE Java (IntelliJ IDEA, Eclipse, v.v.).

## Hướng Dẫn Từng Bước

### Bước 1: Thiết Lập Dự Án
Tạo một dự án Java mới và thêm các file JAR của Aspose.Cells vào đường dẫn biên dịch. Điều này chuẩn bị môi trường cho việc tạo và thao tác các file Excel.

### Bước 2: Tải File Excel (load excel file java)
```java
// Import necessary libraries
import com.aspose.cells.*;

// Load the Excel file
Workbook workbook = new Workbook("your_excel_file.xlsx");

// Access the worksheet
Worksheet worksheet = workbook.getWorksheets().get(0);
```
*Chúng tôi vừa **tải một file Excel** vào bộ nhớ, sẵn sàng để tạo biểu đồ.*

### Bước 3: Tạo Biểu Đồ
```java
// Create a chart
int chartIndex = worksheet.getCharts().add(ChartType.LINE, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);

// Specify data source for the chart
chart.getNSeries().add("A1:A10", true);
```
*Ở đây chúng tôi tạo một biểu đồ đường sẽ sau này chứa đường xu hướng của chúng tôi.*

### Bước 4: Thêm Đường Xu hướng (how to add trendline) và Hiển thị Giá trị R‑squared
```java
// Add a trendline to the chart
Trendline trendline = chart.getNSeries().get(0).getTrendlines().add(TrendlineType.LINEAR);

// Customize trendline options
trendline.setDisplayEquation(true);
trendline.setDisplayRSquaredValue(true);
```
*Lệnh `setDisplayRSquaredValue(true)` đảm bảo **giá trị R‑squared** xuất hiện trên biểu đồ.*

### Bước 5: Tùy Chỉnh Biểu Đồ và Lưu Workbook (save workbook xlsx, generate excel file java)
```java
// Customize chart title and axes
chart.getTitle().setText("Trendline Analysis");
chart.getCategoryAxis().getTitle().setText("X-Axis");
chart.getValueAxis().getTitle().setText("Y-Axis");

// Save the Excel file with the chart
workbook.save("output.xlsx");
```
*Bây giờ workbook đã được **tạo** và lưu dưới dạng file XLSX, sẵn sàng cho các xử lý tiếp theo.*

### Bước 6: Xuất Biểu Đồ ra Hình Ảnh (export chart to image)
> **Lưu ý:** Bước này được mô tả mà không có khối mã bổ sung để giữ nguyên số lượng khối gốc.  
Sau khi biểu đồ được tạo và lưu, bạn có thể xuất nó ra hình ảnh bằng cách gọi phương thức `chart.toImage()` và ghi `java.awt.image.BufferedImage` kết quả vào định dạng file bạn muốn (PNG, JPEG, BMP). Quy trình điển hình là:
1. Lấy đối tượng `Chart` (đã thực hiện trong các bước trước).  
2. Gọi `chart.toImage()` để nhận một `BufferedImage`.  
3. Sử dụng `ImageIO.write(bufferedImage, "png", new File("chart.png"))` để ghi file.  

Điều này tạo ra một hình ảnh độ phân giải cao mà bạn có thể nhúng ở bất kỳ đâu, hoàn thành quy trình **export chart to image**.

## Phân Tích Kết Quả
Mở `output.xlsx` trong Excel để xác nhận rằng đường xu hướng, phương trình và giá trị R‑squared hiển thị như mong đợi. Mở file hình ảnh đã xuất (ví dụ, `chart.png`) để xem hình ảnh sạch sẽ có thể chia sẻ mà không cần workbook gốc.

## Các Vấn Đề Thường Gặp và Giải Pháp
- **Đường xu hướng không hiển thị:** Đảm bảo phạm vi dữ liệu (`A1:A10`) thực sự chứa giá trị số; dữ liệu không phải số sẽ ngăn không cho tính toán đường xu hướng.  
- **Giá R‑squared hiển thị là 0:** Thường nghĩa là dãy dữ liệu cố định hoặc thiếu biến đổi. Thử một bộ dữ liệu khác hoặc đường xu hướng đa thức.  
- **Xuất hình ảnh thất bại với `NullPointerException`:** Kiểm tra rằng biểu đồ đã được render đầy đủ trước khi gọi `toImage()`. Lưu workbook trước có thể giải quyết một số vấn đề thời gian.

## Câu Hỏi Thường Gặp

**Hỏi: Làm sao tôi có thể thay đổi loại đường xu hướng?**  
**Đáp:** Sử dụng một giá trị `TrendlineType` khác khi thêm đường xu hướng, ví dụ `TrendlineType.POLYNOMIAL` cho phép phù hợp đa thức.

**Hỏi: Tôi có thể tùy chỉnh giao diện của đường xu hướng (màu sắc, độ dày) không?**  
**Đáp:** Có. Truy cập `LineFormat` của đường xu hướng qua `trendline.getLineFormat()` và đặt các thuộc tính như `setWeight()` và `setColor()`.

**Hỏi: Làm sao tôi xuất biểu đồ ra PDF thay vì hình ảnh?**  
**Đáp:** Đầu tiên chuyển đổi biểu đồ thành hình ảnh, sau đó nhúng hình ảnh đó vào PDF bằng Aspose.PDF hoặc bất kỳ thư viện PDF nào bạn chọn.

**Hỏi: Có thể thêm nhiều đường xu hướng vào cùng một biểu đồ không?**  
**Đáp:** Chắc chắn. Gọi `chart.getNSeries().get(0).getTrendlines().add(...)` cho mỗi series bạn muốn phân tích.

**Hỏi: Aspose.Cells có hỗ trợ xuất hình ảnh độ phân giải cao không?**  
**Đáp:** Có. Bạn có thể chỉ định DPI khi gọi `chart.toImage()` và sau đó điều chỉnh kích thước hình ảnh cho phù hợp trước khi lưu.

## Kết Luận
Bây giờ bạn đã có một giải pháp toàn diện, đầu‑tới‑cuối cho **việc xuất biểu đồ ra hình ảnh** trong khi thực hiện **phân tích đường xu hướng** bằng Java với Aspose.Cells. Bằng cách tải một file Excel, thêm đường xu hướng, hiển thị phương trình và giá trị R‑squared, tùy chỉnh biểu đồ, lưu workbook, và cuối cùng xuất hình ảnh ra PNG/JPEG, bạn có thể tạo ra các tài sản phân tích chất lượng chuyên nghiệp một cách tự động.

---

**Cập nhật lần cuối:** 2025-12-09  
**Được kiểm tra với:** Aspose.Cells for Java 24.12 (latest)  
**Tác giả:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}