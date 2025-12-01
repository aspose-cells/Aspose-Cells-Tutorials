---
date: 2025-12-01
description: Tìm hiểu cách thay đổi loại biểu đồ Excel và thêm các tính năng tương
  tác như chú giải công cụ, nhãn dữ liệu và drill‑down bằng Aspose.Cells cho Java.
language: vi
linktitle: Change Excel chart type and add interactivity
second_title: Aspose.Cells Java Excel Processing API
title: Thay đổi loại biểu đồ Excel và thêm tính tương tác – Aspose.Cells Java
url: /java/advanced-excel-charts/chart-interactivity/
weight: 19
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Thay đổi loại biểu đồ Excel và thêm tính tương tác

## Giới thiệu

Biểu đồ tương tác cho phép khán giả khám phá dữ liệu ngay lập tức, trong khi khả năng **thay đổi loại biểu đồ Excel** mang lại sự linh hoạt để trình bày thông tin bằng định dạng hình ảnh hiệu quả nhất. Trong hướng dẫn này, bạn sẽ học cách sử dụng Aspose.Cells cho Java để thay đổi loại biểu đồ, thêm tooltip, nhúng nhãn dữ liệu, và thậm chí tạo liên kết drill‑down — tất cả mà không rời khỏi mã Java của bạn. Khi hoàn thành, bạn sẽ có một workbook Excel đầy đủ tính năng, tương tác, có thể nhúng vào báo cáo, bảng điều khiển hoặc ứng dụng web.

## Câu trả lời nhanh
- **Có thể thay đổi loại biểu đồ bằng lập trình không?** Có – sử dụng enum `ChartType` khi tạo hoặc cập nhật biểu đồ.  
- **Làm sao để thêm tooltip cho biểu đồ?** Bật nhãn dữ liệu và đặt `ShowValue` thành true.  
- **Cách dễ nhất để thêm liên kết drill‑down là gì?** Gắn hyperlink vào một điểm dữ liệu qua `getHyperlinks().add(url)`.  
- **Có cần giấy phép cho Aspose.Cells không?** Bản dùng thử miễn phí đủ cho phát triển; giấy phép bắt buộc cho môi trường sản xuất.  
- **Phiên bản Java nào được hỗ trợ?** Java 8 trở lên được hỗ trợ đầy đủ.

## “Thay đổi loại biểu đồ Excel” là gì?

Thay đổi loại biểu đồ có nghĩa là hoán đổi cách hiển thị (ví dụ: từ biểu đồ cột sang biểu đồ đường) trong khi giữ nguyên dữ liệu gốc. Điều này hữu ích khi bạn nhận ra một loại biểu đồ khác truyền tải xu hướng, so sánh hoặc phân bố dữ liệu tốt hơn.

## Tại sao cần thêm tính tương tác cho biểu đồ Excel?

- **Cải thiện hiểu biết dữ liệu:** Tooltip và nhãn dữ liệu cho phép người dùng xem giá trị chính xác mà không cần cuộn.  
- **Bài thuyết trình sinh động:** Các yếu tố tương tác giữ cho người xem luôn quan tâm.  
- **Khả năng drill‑down:** Hyperlink cho phép người dùng chuyển đến các sheet chi tiết hoặc tài nguyên bên ngoài.  
- **Tài sản tái sử dụng:** Một workbook có thể phục vụ nhiều kịch bản báo cáo khác nhau chỉ bằng cách chuyển đổi loại biểu đồ.

## Yêu cầu trước

- Môi trường phát triển Java (JDK 8+)
- Thư viện Aspose.Cells cho Java (tải về từ [đây](https://releases.aspose.com/cells/java/))
- Một file Excel mẫu (`data.xlsx`) chứa dữ liệu bạn muốn trực quan hoá

## Hướng dẫn từng bước

### Bước 1: Thiết lập dự án Java

1. Tạo một dự án Java mới trong IDE yêu thích (IntelliJ IDEA, Eclipse, VS Code, …).  
2. Thêm file JAR Aspose.Cells vào classpath của dự án.

### Bước 2: Tải workbook nguồn

Chúng ta bắt đầu bằng việc tải một workbook hiện có chứa dữ liệu cho biểu đồ.

```java
// Load the Excel file
Workbook workbook = new Workbook("data.xlsx");
Worksheet worksheet = workbook.getWorksheets().get(0);
```

### Bước 3: Tạo biểu đồ và **thay đổi loại của nó**

Dưới đây chúng ta tạo một biểu đồ cột, sau đó ngay lập tức minh họa cách chuyển sang biểu đồ đường nếu cần.

```java
// Create a column chart
int chartIndex = worksheet.getCharts().add(ChartType.COLUMN, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);

// OPTIONAL: Change the chart type to LINE
chart.setChartType(ChartType.LINE);
```

> **Mẹo chuyên nghiệp:** Thay đổi loại biểu đồ sau khi tạo chỉ cần gọi `setChartType(...)`. Điều này đáp ứng từ khóa chính **change Excel chart type** mà không cần tạo đối tượng biểu đồ mới.

### Bước 4: Thêm tính tương tác

#### 4.1 Thêm tooltip cho biểu đồ

Tooltip hiển thị khi người dùng di chuột qua một điểm dữ liệu. Trong Aspose.Cells chúng được triển khai qua nhãn dữ liệu.

```java
// Enable tooltips for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowValue(true);
```

#### 4.2 Thêm nhãn dữ liệu (**add data labels chart**)

Nhãn dữ liệu có thể hiển thị giá trị chính xác, tên danh mục, hoặc cả hai. Ở đây chúng ta sử dụng kiểu callout.

```java
// Enable data labels for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowLabelAsDataCallout(true);
```

#### 4.3 Triển khai drill‑down (**add drill down excel**)

Liên kết drill‑down cho phép người dùng nhấp vào một điểm và chuyển đến chế độ xem chi tiết, có thể trong cùng workbook hoặc trên một trang web.

```java
// Add a hyperlink to a data point
String url = "https://example.com/data-details";
chart.getNSeries().get(0).getPoints().get(0).getHyperlinks().add(url);
```

### Bước 5: Lưu workbook

```java
// Save the workbook
workbook.save("interactive_chart_output.xlsx");
```

## Các vấn đề thường gặp và giải pháp

| Vấn đề | Lý do | Cách khắc phục |
|-------|--------|----------------|
| Tooltip không hiển thị | `HasDataLabels` chưa được bật | Đảm bảo gọi `setHasDataLabels(true)` trước khi cấu hình `ShowValue`. |
| Liên kết drill‑down không hoạt động | URL của hyperlink sai định dạng | Kiểm tra URL bắt đầu bằng `http://` hoặc `https://`. |
| Loại biểu đồ không thay đổi | Sử dụng phiên bản Aspose.Cells cũ | Nâng cấp lên phiên bản mới nhất (đã kiểm tra với 24.12). |

## Câu hỏi thường gặp

**H: Làm sao tôi có thể thay đổi loại biểu đồ sau khi đã tạo?**  
Đ: Gọi `chart.setChartType(ChartType.YOUR_CHOICE)` trên đối tượng `Chart` hiện có. Điều này trực tiếp đáp ứng yêu cầu **change Excel chart type**.

**H: Tôi có thể tùy chỉnh giao diện của tooltip không?**  
Đ: Có. Sử dụng `chart.getNSeries().get(0).getPoints().getDataLabels()` để đặt kích thước phông chữ, màu sắc và nền.

**H: Có thể thêm nhiều liên kết drill‑down trong một biểu đồ không?**  
Đ: Chắc chắn. Duyệt qua các điểm và gọi `getHyperlinks().add(url)` cho mỗi điểm muốn liên kết.

**H: Aspose.Cells có hỗ trợ các loại biểu đồ khác như bánh hoặc radar không?**  
Đ: Tất cả các loại biểu đồ được định nghĩa trong enum `ChartType` đều được hỗ trợ, bao gồm `PIE`, `RADAR`, `AREA`, v.v.

**H: Tôi có thể tìm thêm ví dụ ở đâu?**  
Đ: Tham khảo trang [Aspose.Cells Java API Reference](https://reference.aspose.com/cells/java/) để xem danh sách đầy đủ các phương thức liên quan đến biểu đồ.

## Kết luận

Bây giờ bạn đã biết cách **thay đổi loại biểu đồ Excel**, nhúng **tooltip**, thêm **nhãn dữ liệu**, và tạo các liên kết **drill‑down** bằng Aspose.Cells cho Java. Những tính năng tương tác này biến các bảng tính tĩnh thành công cụ khám phá dữ liệu động, hoàn hảo cho bảng điều khiển, báo cáo và phân tích trên web.

---

**Cập nhật lần cuối:** 2025-12-01  
**Kiểm thử với:** Aspose.Cells 24.12 cho Java  
**Tác giả:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}