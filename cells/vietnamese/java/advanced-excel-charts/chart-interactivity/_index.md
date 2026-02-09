---
date: 2026-02-09
description: Tìm hiểu cách thêm nhãn dữ liệu vào biểu đồ Excel và thay đổi loại biểu
  đồ bằng Aspose.Cells cho Java, cùng với chú giải công cụ và tính năng drill‑down
  tương tác.
linktitle: Change Excel Chart Type
second_title: Aspose.Cells Java Excel Processing API
title: Thêm Nhãn Dữ liệu vào Biểu đồ Excel bằng Aspose.Cells Java
url: /vi/java/advanced-excel-charts/chart-interactivity/
weight: 19
---

ữ Liệu vào Biểu Đồ Excel và Thay Đổi Loại Biểu Đồ – Aspose.Cells Java". Keep dash.

Paragraph: "Interactive charts give your Excel reports a new level..." translate.

We'll translate all.

Make sure code block placeholders remain as is.

Table: translate Issue, Solution headings, and content.

FAQ: translate questions and answers, but keep code terms.

Let's craft.

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Thêm Nhãn Dữ Liệu vào Biểu Đồ Excel và Thay Đổi Loại Biểu Đồ – Aspose.Cells Java

Biểu đồ tương tác mang lại cho báo cáo Excel của bạn một cấp độ hiểu biết mới, và **việc thêm nhãn dữ liệu vào biểu đồ Excel** giúp thông tin trở nên dễ đọc ngay lập tức. Trong hướng dẫn này, bạn sẽ học cách **thêm nhãn dữ liệu vào biểu đồ Excel**, thay đổi loại biểu đồ, và tạo các giải pháp Java tương tác với Aspose.Cells. Chúng tôi cũng sẽ chỉ cho bạn cách thêm tooltip và một siêu liên kết drill‑down đơn giản để người xem có thể khám phá dữ liệu chi tiết.

## Câu trả lời nhanh
- **Thư viện nào được sử dụng?** Aspose.Cells for Java  
- **Tôi có thể thay đổi loại biểu đồ không?** Có – chỉ cần sửa enum `ChartType` khi tạo biểu đồ.  
- **Làm thế nào để thêm tooltip cho biểu đồ?** Sử dụng API nhãn dữ liệu (`setHasDataLabels(true)`) và bật hiển thị giá trị.  
- **Có hỗ trợ drill‑down không?** Bạn có thể gắn siêu liên kết vào các điểm dữ liệu để thực hiện hành vi drill‑down cơ bản.  
- **Yêu cầu trước?** IDE Java, Aspose.Cells JAR, và một tệp Excel có dữ liệu mẫu.

## Yêu cầu trước

Trước khi bắt đầu, hãy chắc chắn bạn đã có:

- Môi trường phát triển Java (khuyến nghị JDK 8+ )  
- Thư viện Aspose.Cells for Java (tải về từ [here](https://releases.aspose.com/cells/java/))  
- Một workbook mẫu (`data.xlsx`) chứa dữ liệu bạn muốn trực quan hoá  

## Bước 1: Thiết lập Dự án Java

1. Tạo một dự án Java mới trong IDE yêu thích của bạn (IntelliJ IDEA, Eclipse, v.v.).  
2. Thêm Aspose.Cells JAR vào đường dẫn biên dịch của dự án hoặc vào các phụ thuộc Maven/Gradle.

## Bước 2: Tải Dữ liệu

Để làm việc với biểu đồ, trước tiên bạn cần một workbook được nạp vào bộ nhớ.

```java
// Load the Excel file
Workbook workbook = new Workbook("data.xlsx");
Worksheet worksheet = workbook.getWorksheets().get(0);
```

## Bước 3: Tạo Biểu Đồ (và Thay Đổi Loại)

Bạn có thể chọn bất kỳ loại biểu đồ nào phù hợp với phân tích của mình. Dưới đây chúng tôi tạo một **biểu đồ cột**, nhưng bạn có thể dễ dàng chuyển sang biểu đồ đường, bánh, hoặc thanh bằng cách thay đổi enum `ChartType`.

```java
// Create a column chart
int chartIndex = worksheet.getCharts().add(ChartType.COLUMN, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);
```

> **Mẹo chuyên nghiệp:** Để **thay đổi loại biểu đồ Excel**, thay `ChartType.COLUMN` bằng `ChartType.LINE`, `ChartType.PIE`, v.v.

## Bước 4: Thêm Tính Năng Tương Tác

### 4.1. Thêm Tooltip (Add Tooltips to Chart)

Tooltip xuất hiện khi người dùng di chuột qua một điểm dữ liệu. Đoạn mã sau bật nhãn dữ liệu và hiển thị giá trị dưới dạng tooltip.

```java
// Enable tooltips for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowValue(true);
```

### 4.2. Thêm Nhãn Dữ Liệu – **add data labels to excel chart**

Nhãn dữ liệu cung cấp một chỉ báo trực quan cố định trên biểu đồ. Bạn có thể hiển thị chúng dưới dạng callout để tăng khả năng đọc.

```java
// Enable data labels for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowLabelAsDataCallout(true);
```

> **Tại sao cần thêm nhãn dữ liệu?** Việc đưa nhãn dữ liệu trực tiếp lên biểu đồ loại bỏ nhu cầu người dùng phải di chuột hoặc đoán giá trị, giúp báo cáo rõ ràng hơn.

### 4.3. Thực hiện Drill‑Down (Siêu liên kết trên một Điểm Dữ Liệu)

Một cách đơn giản để thêm khả năng drill‑down là gắn siêu liên kết vào một điểm cụ thể. Khi nhấp vào điểm đó, một trang web với thông tin chi tiết sẽ được mở.

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
|-------|----------|
| **Tooltip không hiển thị** | Đảm bảo gọi `setHasDataLabels(true)` trước khi cấu hình `setShowValue(true)`. |
| **Siêu liên kết không thể nhấp** | Kiểm tra định dạng đầu ra có hỗ trợ siêu liên kết không (ví dụ: XLSX, không phải CSV). |
| **Loại biểu đồ không thay đổi** | Kiểm tra lại bạn đã sửa enum `ChartType` đúng khi tạo biểu đồ. |

## Câu Hỏi Thường Gặp

**H: Làm sao để thay đổi loại biểu đồ sau khi đã tạo?**  
Đ: Bạn cần tạo một biểu đồ mới với `ChartType` mong muốn. Aspose.Cells không hỗ trợ chuyển đổi loại biểu đồ ngay tại chỗ, vì vậy hãy xóa biểu đồ cũ và thêm biểu đồ mới.

**H: Tôi có thể tùy chỉnh giao diện của tooltip không?**  
Đ: Có. Sử dụng các thuộc tính của `DataLabel` như `setFontSize`, `setFontColor`, và `setBackgroundColor` để định dạng văn bản tooltip.

**H: Làm sao xử lý tương tác người dùng trong ứng dụng web?**  
Đ: Xuất workbook ra file HTML hoặc XLSX và dùng JavaScript phía client để bắt sự kiện click trên các thành phần biểu đồ.

**H: Tôi có thể tìm thêm ví dụ và tài liệu ở đâu?**  
Đ: Truy cập [Aspose.Cells Java API Reference](https://reference.aspose.com/cells/java/) để xem danh sách đầy đủ các lớp và phương thức liên quan đến biểu đồ.

## Kết luận

Bây giờ bạn đã biết cách **thêm nhãn dữ liệu vào biểu đồ Excel**, **thay đổi loại biểu đồ Excel**, **tạo giải pháp biểu đồ Java tương tác**, và làm phong phú chúng bằng tooltip, nhãn dữ liệu, và siêu liên kết drill‑down bằng Aspose.Cells for Java. Những cải tiến này giúp báo cáo Excel của bạn trở nên hấp dẫn và sâu sắc hơn đối với người dùng cuối.

---

**Cập nhật lần cuối:** 2026-02-09  
**Đã kiểm tra với:** Aspose.Cells for Java 24.12  
**Tác giả:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}