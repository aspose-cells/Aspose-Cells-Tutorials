---
date: 2025-12-04
description: Tìm hiểu cách tạo biểu đồ tương tác trong Java bằng Aspose.Cells, thêm
  chú giải công cụ vào biểu đồ và thêm biểu đồ drill‑down để có hình ảnh dữ liệu phong
  phú hơn.
language: vi
linktitle: Create Interactive Chart Java
second_title: Aspose.Cells Java Excel Processing API
title: Tạo biểu đồ tương tác Java với Aspose.Cells
url: /java/advanced-excel-charts/chart-interactivity/
weight: 19
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Tạo Biểu Đồ Tương Tác Java

## Giới thiệu

Biểu đồ tương tác cho phép người dùng khám phá các điểm dữ liệu, xem chi tiết khi di chuột, và thậm chí đi sâu vào các bộ dữ liệu sâu hơn — tất cả mà không rời khỏi bảng tính. Trong hướng dẫn này, bạn sẽ học **cách tạo biểu đồ tương tác Java** bằng cách sử dụng Aspose.Cells. Chúng tôi sẽ hướng dẫn cách thêm tooltip, nhãn dữ liệu và triển khai trải nghiệm drill‑down, để biểu đồ của bạn trở nên sinh động và cung cấp thông tin hơn.

## Câu trả lời nhanh
- **Thư viện nào được sử dụng?** Aspose.Cells for Java  
- **Tôi có thể thêm tooltip vào biểu đồ không?** Có, sử dụng API nhãn dữ liệu NSeries  
- **Có hỗ trợ drill‑down không?** Có, bằng cách gắn siêu liên kết vào các điểm dữ liệu  
- **Định dạng tệp nào được tạo ra?** Sổ làm việc XLSX tiêu chuẩn với biểu đồ nhúng  
- **Tôi có cần giấy phép không?** Bản dùng thử miễn phí đủ cho đánh giá; cần giấy phép thương mại cho môi trường sản xuất  

## Yêu cầu trước

- Môi trường phát triển Java (khuyến nghị JDK 8+)  
- Thư viện Aspose.Cells for Java (tải xuống từ [trang phát hành chính thức của Aspose](https://releases.aspose.com/cells/java/))  
- Tệp Excel mẫu có tên **data.xlsx** chứa dữ liệu bạn muốn trực quan hoá  

## Bước 1: Thiết lập dự án Java của bạn

1. Tạo một dự án Java mới trong IDE yêu thích của bạn (IntelliJ IDEA, Eclipse, VS Code, v.v.).  
2. Thêm file JAR Aspose.Cells vào classpath của dự án — bằng cách đặt JAR trong thư mục `libs` hoặc thêm phụ thuộc Maven/Gradle.  

## Bước 2: Tải dữ liệu

Để xây dựng biểu đồ tương tác, trước tiên bạn cần một worksheet chứa dữ liệu. Đoạn mã dưới đây mở một workbook hiện có và lấy worksheet đầu tiên.

```java
// Load the Excel file
Workbook workbook = new Workbook("data.xlsx");
Worksheet worksheet = workbook.getWorksheets().get(0);
```

> **Mẹo:** Đảm bảo phạm vi dữ liệu bạn muốn vẽ biểu đồ là liên tục; Aspose.Cells sẽ tự động phát hiện phạm vi khi bạn ràng buộc series.

## Bước 3: Tạo biểu đồ

Bây giờ chúng ta tạo một biểu đồ cột và đặt nó trên worksheet. Bạn có thể thay đổi `ChartType.COLUMN` thành bất kỳ loại nào khác (ví dụ, `ChartType.LINE`) nếu muốn phong cách hiển thị khác.

```java
// Create a column chart
int chartIndex = worksheet.getCharts().add(ChartType.COLUMN, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);
```

> **Tại sao điều này quan trọng:** Thêm biểu đồ bằng mã cho phép bạn kiểm soát hoàn toàn kích thước, vị trí và nguồn dữ liệu, điều này thiết yếu cho việc xây dựng trải nghiệm tương tác.

## Bước 4: Thêm tính tương tác

### Cách thêm tooltip vào biểu đồ

Tooltip (hoặc nhãn dữ liệu hiển thị giá trị) giúp người dùng ngay lập tức thấy con số chính xác phía sau mỗi cột. Đoạn mã dưới đây bật nhãn dữ liệu và cấu hình chúng để hiển thị giá trị.

```java
// Enable tooltips for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowValue(true);
```

### Cách thêm nhãn dữ liệu (callout)

Nếu bạn muốn nhãn hiển thị dưới dạng callout thay vì văn bản thường, hãy chuyển thuộc tính `ShowLabelAsDataCallout`.

```java
// Enable data labels for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowLabelAsDataCallout(true);
```

### Cách thêm biểu đồ drill‑down

Drill‑down cho phép người dùng nhấp vào một điểm dữ liệu và chuyển tới một view chi tiết liên quan — thường được thực hiện bằng siêu liên kết. Dưới đây chúng tôi gắn một URL vào điểm đầu tiên trong series.

```java
// Add a hyperlink to a data point
String url = "https://example.com/data-details";
chart.getNSeries().get(0).getPoints().get(0).getHyperlinks().add(url);
```

> **Cạm bẫy thường gặp:** Hãy nhớ đặt đích của siêu liên kết tới một trang có thể hiển thị dữ liệu chi tiết (ví dụ, báo cáo web hoặc một sheet Excel khác). Nếu không, việc nhấp sẽ dẫn tới liên kết chết.

## Bước 5: Lưu workbook

Sau khi cấu hình biểu đồ, lưu workbook. Tệp kết quả chứa biểu đồ tương tác sẵn sàng mở trong Excel hoặc bất kỳ trình xem tương thích nào.

```java
// Save the workbook
workbook.save("interactive_chart_output.xlsx");
```

## Kết luận

Trong hướng dẫn này, bạn đã học **cách tạo biểu đồ tương tác Java** với Aspose.Cells, bao gồm:

- Tải dữ liệu từ một workbook hiện có  
- Tạo biểu đồ cột bằng mã  
- Thêm tooltip và nhãn dữ liệu dạng callout  
- Triển khai chức năng drill‑down qua siêu liên kết  
- Lưu workbook cuối cùng  

Những kỹ thuật này biến bảng tính tĩnh thành bảng điều khiển động, thân thiện với người dùng, giúp nâng cao khả năng hiểu dữ liệu và ra quyết định.

## Câu hỏi thường gặp

**Q: Làm sao tôi có thể thay đổi loại biểu đồ?**  
A: Thay đổi enum `ChartType` trong phương thức `add` (ví dụ, `ChartType.LINE` cho biểu đồ đường).

**Q: Tôi có thể tùy chỉnh giao diện của tooltip không?**  
A: Có, bạn có thể điều chỉnh kích thước phông chữ, màu sắc, nền và các thuộc tính kiểu khác thông qua đối tượng `DataLabels`.

**Q: Làm sao tôi xử lý tính tương tác của biểu đồ trong ứng dụng web?**  
A: Xuất workbook ra định dạng XLSX, sau đó sử dụng thư viện biểu đồ JavaScript (ví dụ, Highcharts) để render dữ liệu phía client, hoặc nhúng tệp Excel trong Office Web Viewer hỗ trợ siêu liên kết.

**Q: Tôi có thể tìm thêm ví dụ ở đâu?**  
A: Truy cập [Tham chiếu API Aspose.Cells Java chính thức](https://reference.aspose.com/cells/java/) để xem danh sách đầy đủ các lớp và phương thức liên quan tới biểu đồ.

**Q: Tôi có cần giấy phép cho việc sử dụng trong môi trường sản xuất không?**  
A: Có, cần giấy phép thương mại để triển khai; giấy phép đánh giá miễn phí có sẵn cho việc thử nghiệm.

---

**Cập nhật lần cuối:** 2025-12-04  
**Kiểm thử với:** Aspose.Cells for Java 24.12 (phiên bản mới nhất tại thời điểm viết)  
**Tác giả:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}