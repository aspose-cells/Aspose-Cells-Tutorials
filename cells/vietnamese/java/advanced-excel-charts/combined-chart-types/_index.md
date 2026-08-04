---
date: 2026-02-14
description: Tìm hiểu cách xuất biểu đồ sang PNG, thêm chuỗi dữ liệu, kết hợp biểu
  đồ đường và cột, lưu sổ làm việc dưới dạng XLSX và thêm chú giải cho biểu đồ bằng
  Aspose.Cells cho Java.
linktitle: Export chart to PNG and add data series for combined chart
second_title: Aspose.Cells Java Excel Processing API
title: Xuất biểu đồ sang PNG và thêm chuỗi dữ liệu cho biểu đồ kết hợp
url: /vi/java/advanced-excel-charts/combined-chart-types/
weight: 12
---

: Define the data ranges and **add data series**" we kept bold phrase.

In "Step 7: **Set chart axis labels** and title" keep bold phrase.

In "Step 8: **Add legend chart** and adjust its position" keep bold phrase.

In "Step 10: **Export chart to PNG**" keep bold phrase.

In table, we kept code unchanged.

Now produce final answer.{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Xuất biểu đồ sang PNG và thêm chuỗi dữ liệu cho biểu đồ kết hợp

Trong tutorial này, bạn sẽ **thêm chuỗi dữ liệu** vào một workbook Excel, **kết hợp các biểu đồ đường và cột** và học cách **xuất biểu đồ sang PNG** bằng Aspose.Cells for Java. Chúng tôi sẽ hướng dẫn từng bước—từ việc thiết lập workbook, thêm biểu đồ vào worksheet, tùy chỉnh legend, đến **save workbook as xlsx** và tạo ảnh PNG của biểu đồ. Khi hoàn thành, bạn sẽ có một biểu đồ kết hợp sẵn sàng để sử dụng, có thể nhúng vào báo cáo hoặc bảng điều khiển.

## Câu trả lời nhanh
- **Thư viện nào tạo biểu đồ kết hợp?** Aspose.Cells for Java  
- **Làm thế nào để thêm một chuỗi dữ liệu?** Sử dụng `chart.getNSeries().add(...)`  
- **Làm sao để xuất biểu đồ sang png?** Gọi `chart.toImage("file.png", ImageFormat.getPng())`  
- **Định dạng tệp nào có thể lưu workbook?** Chuẩn `.xlsx` (save workbook as xlsx)  
- **Có cần giấy phép cho môi trường production không?** A valid Aspose.Cells license is required  

## **export chart to PNG** là gì trong Aspose.Cells?
Xuất một biểu đồ sang PNG tạo ra một hình ảnh raster của biểu đồ Excel có thể hiển thị trên các trang web, báo cáo hoặc email mà không cần ứng dụng Excel.

## Tại sao tạo **combined line column chart**?
Biểu đồ kết hợp cho phép bạn hiển thị các bộ dữ liệu khác nhau với các dạng biểu diễn trực quan riêng biệt (ví dụ: một chuỗi đường trên một chuỗi cột) trong một khung nhìn duy nhất. Điều này rất phù hợp để so sánh xu hướng với tổng số, làm nổi bật mối tương quan, hoặc cung cấp những hiểu biết sâu hơn trong một định dạng gọn gàng.

## Yêu cầu trước
- Java Development Kit (JDK) 8 trở lên  
- Thư viện Aspose.Cells for Java (tải xuống từ liên kết bên dưới)  
- Kiến thức cơ bản về cú pháp Java và các khái niệm Excel  

## Bắt đầu

Đầu tiên, tải xuống thư viện Aspose.Cells for Java từ trang chính thức:

[Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/)

Sau khi thêm JAR vào classpath của dự án, bạn có thể bắt đầu xây dựng biểu đồ.

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

### Bước 4: Thêm đối tượng biểu đồ kết hợp vào worksheet  
Chúng ta sẽ bắt đầu với một biểu đồ đường và sau đó thêm một chuỗi cột để đạt được hiệu ứng **combined line column chart**.
```java
int chartIndex = worksheet.getCharts().add(ChartType.LINE, 0, 0, 20, 10);
Chart chart = worksheet.getCharts().get(chartIndex);
```

## Thêm dữ liệu vào biểu đồ

Bây giờ khi container biểu đồ đã tồn tại, chúng ta cần cung cấp dữ liệu cho nó.

### Bước 5: Xác định phạm vi dữ liệu và **add data series**
```java
Cells cells = worksheet.getCells();
chart.getNSeries().add("A1:A5", true);
chart.getNSeries().add("B1:B5", true);
```
> **Mẹo:** Tham số đầu tiên (`"A1:A5"`) là phạm vi cho chuỗi đầu tiên, và tham số thứ hai (`"B1:B5"`) tạo ra một chuỗi thứ hai sẽ được kết hợp với chuỗi đầu tiên.

### Bước 6: Đặt dữ liệu danh mục (trục X)
```java
chart.getNSeries().setCategoryData("C1:C5");
```

## Tùy chỉnh biểu đồ

Một biểu đồ tốt kể một câu chuyện. Hãy đặt tiêu đề, nhãn trục và một legend rõ ràng cho nó.

### Bước 7: **Set chart axis labels** và tiêu đề
```java
chart.getTitle().setText("Combined Chart Example");
chart.getCategoryAxis().getTitle().setText("Categories");
chart.getValueAxis().getTitle().setText("Values");
```

### Bước 8: **Add legend chart** và điều chỉnh vị trí của nó
```java
chart.getLegend().setPosition(LegendPositionType.BOTTOM);
chart.getLegend().setOverlay(true);
```

## Lưu và xuất biểu đồ

Sau khi tùy chỉnh, bạn sẽ muốn **save workbook as xlsx** và cũng tạo ra một hình ảnh.

### Bước 9: Lưu workbook dưới dạng tệp Excel (xlsx)
```java
workbook.save("CombinedChart.xlsx");
```

### Bước 10: **Export chart to PNG**
```java
chart.toImage("CombinedChart.png", ImageFormat.getPng());
```
> Phương thức `chart.toImage` **generates excel chart** tạo ra các hình ảnh biểu đồ Excel có thể được sử dụng trong các trang web, báo cáo hoặc email.

## Các vấn đề thường gặp & Khắc phục

| Vấn đề | Giải pháp |
|-------|----------|
| **Không có dữ liệu xuất hiện** | Xác minh rằng các phạm vi ô (`A1:A5`, `B1:B5`, `C1:C5`) thực sự chứa dữ liệu trước khi tạo biểu đồ. |
| **Legend chồng lên biểu đồ** | Đặt `chart.getLegend().setOverlay(false)` hoặc di chuyển legend tới vị trí khác (ví dụ: `RIGHT`). |
| **Tệp hình ảnh trống** | Đảm bảo biểu đồ có ít nhất một series và `chart.toImage` được gọi sau tất cả các tùy chỉnh. |
| **Lưu gây ra ngoại lệ** | Kiểm tra rằng bạn có quyền ghi vào thư mục đích và tệp không được mở trong Excel. |

## Câu hỏi thường gặp

**Q: Làm thế nào để cài đặt Aspose.Cells for Java?**  
**A:** Tải JAR từ trang chính thức và thêm vào classpath của dự án. Liên kết tải xuống là: [Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/).

**Q: Tôi có thể tạo các loại biểu đồ khác ngoài đường và cột không?**  
**A:** Có, Aspose.Cells hỗ trợ các loại biểu đồ thanh, tròn, scatter, area và nhiều loại biểu đồ khác. Tham khảo tài liệu API để xem danh sách đầy đủ.

**Q: Có cần giấy phép cho việc sử dụng trong môi trường production không?**  
**A:** Một giấy phép Aspose.Cells hợp lệ là bắt buộc cho các triển khai trong môi trường production. Một bản dùng thử miễn phí có sẵn để đánh giá.

**Q: Làm sao tôi có thể thay đổi màu sắc của từng series?**  
**A:** Sử dụng `chart.getNSeries().get(i).setAreaColor(Color.getRed())` (hoặc tương tự) sau khi đã thêm series.

**Q: Tôi có thể tìm thêm ví dụ mã ở đâu?**  
**A:** Tài liệu đầy đủ và các mẫu bổ sung có sẵn trên trang tham chiếu của Aspose: [here](https://reference.aspose.com/cells/java/).

---

**Cập nhật lần cuối:** 2026-02-14  
**Kiểm tra với:** Aspose.Cells for Java latest version  
**Tác giả:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}