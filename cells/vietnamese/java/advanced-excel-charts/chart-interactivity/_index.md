---
date: 2025-12-06
description: Học cách thay đổi loại biểu đồ Excel và tạo biểu đồ tương tác bằng Java
  sử dụng Aspose.Cells. Thêm chú giải công cụ vào biểu đồ, nhãn dữ liệu và chức năng
  drill‑down để có hình ảnh dữ liệu phong phú hơn.
language: vi
linktitle: Change Excel Chart Type
second_title: Aspose.Cells Java Excel Processing API
title: Thay đổi loại biểu đồ Excel bằng Aspose.Cells Java
url: /java/advanced-excel-charts/chart-interactivity/
weight: 19
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Thay Đổi Loại Biểu Đồ Excel và Thêm Tính Tương Tác

## Giới thiệu

Biểu đồ tương tác mang lại cho báo cáo Excel của bạn một cấp độ hiểu biết mới, cho phép người dùng di chuột, nhấp và khám phá các điểm dữ liệu trực tiếp. Trong hướng dẫn này, bạn sẽ **thay đổi loại biểu đồ Excel** và **tạo các giải pháp biểu đồ tương tác Java** với Aspose.Cells for Java. Chúng tôi sẽ hướng dẫn cách thêm tooltip vào biểu đồ, nhãn dữ liệu và một siêu liên kết drill‑down đơn giản để khán giả của bạn có thể đào sâu hơn vào các con số.

## Câu Hỏi Nhanh
- **Thư viện nào được sử dụng?** Aspose.Cells for Java  
- **Tôi có thể thay đổi loại biểu đồ không?** Có – chỉ cần sửa đổi enum `ChartType` khi tạo biểu đồ.  
- **Làm sao để thêm tooltip vào biểu đồ?** Sử dụng API nhãn dữ liệu (`setHasDataLabels(true)`) và bật hiển thị giá trị.  
- **Có hỗ trợ drill‑down không?** Bạn có thể gắn siêu liên kết vào các điểm dữ liệu để thực hiện hành vi drill‑down cơ bản.  
- **Yêu cầu trước?** IDE Java, Aspose.Cells JAR, và một tệp Excel có dữ liệu mẫu.

## Yêu Cầu Trước

Trước khi bắt đầu, hãy chắc chắn rằng bạn đã có:

- Môi trường phát triển Java (khuyến nghị JDK 8+ )  
- Thư viện Aspose.Cells for Java (tải về từ [here](https://releases.aspose.com/cells/java/))  
- Một workbook mẫu (`data.xlsx`) chứa dữ liệu bạn muốn trực quan hoá  

## Bước 1: Thiết Lập Dự Án Java

1. Tạo một dự án Java mới trong IDE yêu thích của bạn (IntelliJ IDEA, Eclipse, v.v.).  
2. Thêm Aspose.Cells JAR vào đường dẫn xây dựng của dự án hoặc vào các phụ thuộc Maven/Gradle.

## Bước 2: Tải Dữ Liệu

Để làm việc với biểu đồ, trước tiên bạn cần tải một workbook vào bộ nhớ.

```java
// Load the Excel file
Workbook workbook = new Workbook("data.xlsx");
Worksheet worksheet = workbook.getWorksheets().get(0);
```

## Bước 3: Tạo Biểu Đồ (và Thay Đổi Loại)

Bạn có thể chọn bất kỳ loại biểu đồ nào phù hợp với phân tích của mình. Dưới đây chúng tôi tạo một **biểu đồ cột**, nhưng bạn có thể dễ dàng chuyển sang biểu đồ đường, bánh hoặc thanh bằng cách thay đổi enum `ChartType`.

```java
// Create a column chart
int chartIndex = worksheet.getCharts().add(ChartType.COLUMN, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);
```

> **Mẹo chuyên nghiệp:** Để **thay đổi loại biểu đồ Excel**, thay `ChartType.COLUMN` bằng `ChartType.LINE`, `ChartType.PIE`, v.v.

## Bước 4: Thêm Tính Tương Tác

### 4.1. Thêm Tooltip (Thêm Tooltip vào Biểu Đồ)

Tooltip xuất hiện khi người dùng di chuột qua một điểm dữ liệu. Đoạn mã sau bật nhãn dữ liệu và hiển thị giá trị dưới dạng tooltip.

```java
// Enable tooltips for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowValue(true);
```

### 4.2. Thêm Nhãn Dữ Liệu

Nhãn dữ liệu cung cấp một chỉ dẫn trực quan cố định trên biểu đồ. Bạn có thể hiển thị chúng dưới dạng callout để dễ đọc hơn.

```java
// Enable data labels for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowLabelAsDataCallout(true);
```

### 4.3. Thực Hiện Drill‑Down (Siêu Liên Kết trên Điểm Dữ Liệu)

Một cách đơn giản để thêm khả năng drill‑down là gắn một siêu liên kết vào một điểm cụ thể. Khi nhấp vào điểm đó, một trang web với thông tin chi tiết sẽ được mở.

```java
// Add a hyperlink to a data point
String url = "https://example.com/data-details";
chart.getNSeries().get(0).getPoints().get(0).getHyperlinks().add(url);
```

## Bước 5: Lưu Workbook

Sau khi cấu hình biểu đồ, lưu workbook lại để các tính năng tương tác được lưu trong tệp đầu ra.

```java
// Save the workbook
workbook.save("interactive_chart_output.xlsx");
```

## Các Vấn Đề Thường Gặp & Giải Pháp

| Vấn đề | Giải pháp |
|-------|-----------|
| **Tooltip không hiển thị** | Đảm bảo `setHasDataLabels(true)` được gọi trước khi cấu hình `setShowValue(true)`. |
| **Siêu liên kết không thể nhấp** | Kiểm tra định dạng đầu ra có hỗ trợ siêu liên kết không (ví dụ: XLSX, không phải CSV). |
| **Loại biểu đồ không thay đổi** | Kiểm tra lại bạn đã sửa đổi enum `ChartType` đúng khi thêm biểu đồ. |

## Câu Hỏi Thường Gặp

**H: Làm sao tôi có thể thay đổi loại biểu đồ sau khi đã tạo?**  
Đ: Bạn cần tạo một biểu đồ mới với `ChartType` mong muốn. Aspose.Cells không hỗ trợ chuyển đổi loại biểu đồ tại chỗ, vì vậy hãy xóa biểu đồ cũ và thêm biểu đồ mới.

**H: Tôi có thể tùy chỉnh giao diện của tooltip không?**  
Đ: Có. Sử dụng các thuộc tính của `DataLabel` như `setFontSize`, `setFontColor` và `setBackgroundColor` để định dạng văn bản tooltip.

**H: Làm sao tôi xử lý tương tác người dùng trong một ứng dụng web?**  
Đ: Xuất workbook ra tệp HTML hoặc XLSX và sử dụng JavaScript phía client để bắt các sự kiện nhấp vào các phần tử biểu đồ.

**H: Tôi có thể tìm thêm ví dụ và tài liệu ở đâu?**  
Đ: Truy cập [Aspose.Cells Java API Reference](https://reference.aspose.com/cells/java/) để xem danh sách đầy đủ các lớp và phương thức liên quan đến biểu đồ.

## Kết Luận

Bây giờ bạn đã biết cách **thay đổi loại biểu đồ Excel**, **tạo các giải pháp biểu đồ tương tác Java**, và làm phong phú chúng bằng tooltip, nhãn dữ liệu và siêu liên kết drill‑down sử dụng Aspose.Cells for Java. Những cải tiến này sẽ làm cho báo cáo Excel của bạn trở nên hấp dẫn và sâu sắc hơn đối với người dùng cuối.

---

**Cập Nhật Lần Cuối:** 2025-12-06  
**Đã Kiểm Tra Với:** Aspose.Cells for Java 24.12  
**Tác Giả:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}