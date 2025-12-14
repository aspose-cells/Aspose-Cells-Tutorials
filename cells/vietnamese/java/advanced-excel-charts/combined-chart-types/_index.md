---
date: 2025-12-06
description: Tìm hiểu cách thêm chuỗi dữ liệu, tạo các loại biểu đồ kết hợp, lưu workbook
  Excel và xuất biểu đồ sang PNG với Aspose.Cells cho Java.
linktitle: Add data series to create combined chart using Aspose.Cells
second_title: Aspose.Cells Java Excel Processing API
title: Thêm chuỗi dữ liệu để tạo biểu đồ kết hợp bằng Aspose.Cells
url: /vi/java/advanced-excel-charts/combined-chart-types/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Thêm chuỗi dữ liệu để tạo biểu đồ kết hợp bằng Aspose.Cells

Trong hướng dẫn này, bạn sẽ **thêm chuỗi dữ liệu** vào một workbook Excel và học cách **tạo biểu đồ kết hợp** bằng Aspose.Cells cho Java. Chúng tôi sẽ hướng dẫn từng bước—từ việc thiết lập workbook, thêm chuỗi, tùy chỉnh chú giải, đến **lưu workbook Excel** và xuất **biểu đồ ra PNG**. Khi hoàn thành, bạn sẽ có một biểu đồ kết hợp sẵn sàng để nhúng vào báo cáo hoặc bảng điều khiển.

## Câu trả lời nhanh
- **Thư viện nào tạo biểu đồ kết hợp?** Aspose.Cells for Java  
- **Làm thế nào để thêm chuỗi dữ liệu?** Sử dụng `chart.getNSeries().add(...)`  
- **Tôi có thể xuất biểu đồ dưới dạng hình ảnh không?** Có, với `chart.toImage(...)` (PNG)  
- **Định dạng tệp nào tôi có thể lưu workbook?** `.xlsx` tiêu chuẩn (Excel)  
- **Tôi có cần giấy phép cho môi trường sản xuất không?** Cần một giấy phép Aspose.Cells hợp lệ  

## **Thêm chuỗi dữ liệu** là gì trong Aspose.Cells?
Thêm một chuỗi dữ liệu cho biểu đồ biết các ô chứa giá trị bạn muốn vẽ. Mỗi chuỗi có thể đại diện cho một đường, cột, hoặc bất kỳ loại biểu đồ nào khác, và bạn có thể kết hợp chúng để tạo một **biểu đồ kết hợp**.

## Tại sao tạo **biểu đồ kết hợp**?
Biểu đồ kết hợp cho phép bạn hiển thị các bộ dữ liệu khác nhau với các biểu diễn trực quan riêng (ví dụ: một chuỗi đường trên một chuỗi cột) trong một cửa sổ duy nhất. Điều này rất phù hợp để so sánh xu hướng với tổng số, làm nổi bật mối tương quan, hoặc cung cấp những hiểu biết sâu hơn trong một định dạng gọn gàng.

## Yêu cầu trước
- Java Development Kit (JDK) 8 hoặc cao hơn  
- Thư viện Aspose.Cells cho Java (tải xuống từ liên kết bên dưới)  
- Kiến thức cơ bản về cú pháp Java và các khái niệm Excel  

## Bắt đầu

Đầu tiên, tải thư viện Aspose.Cells cho Java từ trang chính thức:

[Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/)

Sau khi JAR được thêm vào classpath của dự án, bạn có thể bắt đầu xây dựng biểu đồ.

### Bước 1: Nhập các lớp Aspose.Cells
```java
import com.aspose.cells.*;
```

### Bước 2: Tạo một workbook mới
```java
Workbook workbook = new Workbook();
```

### Bước 3: Truy cập worksheet đầu tiên
```java
Worksheet worksheet = workbook.getWorksheets().get(0);
```

### Bước 4: Thêm đối tượng biểu đồ kết hợp  
Chúng ta sẽ bắt đầu với một biểu đồ đường và sau đó thêm các chuỗi khác để đạt được hiệu ứng **biểu đồ kết hợp**.
```java
int chartIndex = worksheet.getCharts().add(ChartType.LINE, 0, 0, 20, 10);
Chart chart = worksheet.getCharts().get(chartIndex);
```

## Thêm dữ liệu vào biểu đồ

Bây giờ khi đã có container biểu đồ, chúng ta cần cung cấp dữ liệu cho nó.

### Bước 5: Xác định phạm vi dữ liệu và **thêm chuỗi dữ liệu**
```java
Cells cells = worksheet.getCells();
chart.getNSeries().add("A1:A5", true);
chart.getNSeries().add("B1:B5", true);
```
> **Mẹo:** Tham số đầu tiên (`"A1:A5"`) là phạm vi cho chuỗi đầu tiên, và tham số thứ hai (`"B1:B5"`) tạo ra chuỗi thứ hai sẽ được kết hợp với chuỗi đầu.

### Bước 6: Đặt dữ liệu danh mục (trục X)
```java
chart.getNSeries().setCategoryData("C1:C5");
```

## Tùy chỉnh biểu đồ

Một biểu đồ tốt kể một câu chuyện. Hãy đặt tiêu đề, nhãn trục và chú giải rõ ràng.

### Bước 7: Đặt tiêu đề biểu đồ và nhãn trục
```java
chart.getTitle().setText("Combined Chart Example");
chart.getCategoryAxis().getTitle().setText("Categories");
chart.getValueAxis().getTitle().setText("Values");
```

### Bước 8: **Thêm chú giải cho biểu đồ** và điều chỉnh vị trí của nó
```java
chart.getLegend().setPosition(LegendPositionType.BOTTOM);
chart.getLegend().setOverlay(true);
```

## Lưu và xuất biểu đồ

Sau khi tùy chỉnh, bạn sẽ muốn **lưu workbook Excel** và cũng tạo một hình ảnh.

### Bước 9: Lưu workbook dưới dạng tệp Excel
```java
workbook.save("CombinedChart.xlsx");
```

### Bước 10: Xuất **biểu đồ ra PNG**
```java
chart.toImage("CombinedChart.png", ImageFormat.getPng());
```
> Phương thức `chart.toImage` **tạo ra hình ảnh biểu đồ Excel** có thể được sử dụng trong trang web, báo cáo hoặc email.

## Các vấn đề thường gặp & Khắc phục

| Vấn đề | Giải pháp |
|-------|----------|
| **Không có dữ liệu hiển thị** | Xác minh rằng các phạm vi ô (`A1:A5`, `B1:B5`, `C1:C5`) thực sự chứa dữ liệu trước khi tạo biểu đồ. |
| **Chú giải chồng lên biểu đồ** | Đặt `chart.getLegend().setOverlay(false)` hoặc di chuyển chú giải đến vị trí khác (ví dụ: `RIGHT`). |
| **Tệp hình ảnh trống** | Đảm bảo biểu đồ có ít nhất một chuỗi và `chart.toImage` được gọi sau khi hoàn tất tất cả các tùy chỉnh. |
| **Lưu gây ra ngoại lệ** | Kiểm tra bạn có quyền ghi vào thư mục đích và tệp không đang mở trong Excel. |

## Câu hỏi thường gặp

**H: Làm thế nào để cài đặt Aspose.Cells cho Java?**  
Đ: Tải JAR từ trang chính thức và thêm vào classpath của dự án. Liên kết tải xuống là: [Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/).

**H: Tôi có thể tạo các loại biểu đồ khác ngoài đường và cột không?**  
Đ: Có, Aspose.Cells hỗ trợ biểu đồ thanh, bánh, phân tán, diện tích và nhiều loại biểu đồ khác. Tham khảo tài liệu API để biết danh sách đầy đủ.

**H: Có cần giấy phép cho việc sử dụng trong môi trường sản xuất không?**  
Đ: Cần một giấy phép Aspose.Cells hợp lệ cho các triển khai sản xuất. Một bản dùng thử miễn phí có sẵn để đánh giá.

**H: Làm thế nào để thay đổi màu của từng chuỗi?**  
Đ: Sử dụng `chart.getNSeries().get(i).setAreaColor(Color.getRed())` (hoặc tương tự) sau khi đã thêm chuỗi.

**H: Tôi có thể tìm thêm ví dụ mã ở đâu?**  
Đ: Tài liệu đầy đủ và các mẫu bổ sung có sẵn tại trang tham chiếu Aspose: [here](https://reference.aspose.com/cells/java/).

---

**Last Updated:** 2025-12-06  
**Tested With:** Aspose.Cells for Java 24.12  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
