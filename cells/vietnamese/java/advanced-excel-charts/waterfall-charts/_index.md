---
date: 2025-12-10
description: Tìm hiểu cách tạo biểu đồ thác nước trong Java bằng Aspose.Cells. Hướng
  dẫn từng bước để thêm biểu đồ vào bảng tính, tùy chỉnh và lưu workbook dưới dạng
  XLSX.
linktitle: Waterfall Charts
second_title: Aspose.Cells Java Excel Processing API
title: Cách tạo biểu đồ thác nước bằng Aspose.Cells cho Java
url: /vi/java/advanced-excel-charts/waterfall-charts/
weight: 18
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Biểu đồ Thác nước

## Giới thiệu về Biểu đồ Thác nước sử dụng Aspose.Cells cho Java

Trong hướng dẫn này, bạn sẽ học cách **tạo biểu đồ thác nước** với Aspose.Cells cho Java. Biểu đồ thác nước là công cụ thiết yếu trong việc trực quan dữ liệu vì chúng cho phép bạn nhìn thấy hiệu ứng tích lũy của một chuỗi các giá trị dương và âm. Dù bạn đang chuẩn bị báo cáo tài chính, báo cáo hiệu suất bán hàng, hay bất kỳ phân tích dựa trên dữ liệu nào khác, biểu đồ thác nước có thể biến các con số thô thành những hiểu biết rõ ràng, có thể hành động.

## Câu trả lời nhanh
- **Biểu đồ thác nước là gì?** Một hình ảnh trực quan cho thấy cách một giá trị ban đầu được tăng và giảm bởi một loạt các giá trị trung gian, kết thúc bằng tổng cuối cùng.  
- **Thư viện nào được sử dụng?** Aspose.Cells cho Java.  
- **Tôi có cần giấy phép không?** Bản dùng thử miễn phí đủ cho phát triển; giấy phép thương mại cần thiết cho môi trường sản xuất.  
- **Tôi có thể lưu tệp dưới dạng XLSX không?** Có – sử dụng `workbook.save("FileName.xlsx")`.  
- **Có phù hợp cho việc trực quan dữ liệu Java không?** Chắc chắn; Aspose.Cells cung cấp các tính năng biểu đồ phong phú mà không cần cài đặt Office.

## Biểu đồ Thác nước là gì?
Biểu đồ thác nước hiển thị các đóng góp dương và âm tuần tự vào một giá trị khởi đầu, giúp bạn hiểu cách mỗi thành phần ảnh hưởng đến kết quả tổng thể.

## Tại sao nên sử dụng Aspose.Cells cho Java để thêm biểu đồ thác nước?
- **Không cần Microsoft Excel** – tạo biểu đồ trên bất kỳ máy chủ hoặc pipeline CI nào.  
- **Kiểm soát đầy đủ định dạng** – màu sắc, nhãn dữ liệu và trục có thể được tùy chỉnh bằng mã.  
- **Hỗ trợ nhiều định dạng xuất** – XLSX, PDF, HTML và hơn nữa.  
- **Hiệu năng cao** – lý tưởng cho sổ làm việc lớn và báo cáo tự động.

## Yêu cầu trước

Trước khi chúng ta đi sâu vào mã, hãy chắc chắn rằng bạn đã chuẩn bị các yêu cầu sau:

- Aspose.Cells cho Java: Bạn cần cài đặt Aspose.Cells cho Java. Bạn có thể tải xuống từ [here](https://releases.aspose.com/cells/java/).

- Môi trường phát triển Java: Đảm bảo bạn đã cài đặt Java trên hệ thống.

Bây giờ, hãy bắt đầu tạo biểu đồ thác nước từng bước.

## Cách tạo biểu đồ Thác nước trong Java

### Bước 1: Nhập Aspose.Cells

```java
import com.aspose.cells.*;
```

Đầu tiên, bạn cần nhập thư viện Aspose.Cells vào dự án Java của mình. Thư viện này cung cấp chức năng phong phú để làm việc với tệp Excel, bao gồm cả việc tạo biểu đồ.

### Bước 2: Khởi tạo Workbook và Worksheet

```java
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.getWorksheets().get(0);
```

Tạo một workbook mới và thêm một worksheet vào đó. Chúng ta sẽ sử dụng worksheet này để nhập dữ liệu và **thêm biểu đồ vào worksheet**.

### Bước 3: Nhập dữ liệu

Bây giờ, hãy điền dữ liệu vào worksheet mà chúng ta muốn biểu diễn trong biểu đồ thác nước.

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

Trong ví dụ này, chúng ta có các danh mục ở cột A và các giá trị tương ứng ở cột B. Bạn có thể thay thế dữ liệu này bằng bộ dữ liệu của riêng mình.

### Bước 4: Tạo biểu đồ Thác nước

```java
int chartIndex = worksheet.getCharts().add(ChartType.WATERFALL, 5, 0, 15, 5);
Chart waterfallChart = worksheet.getCharts().get(chartIndex);
waterfallChart.getNSeries().add("B2:B6", true);
waterfallChart.getNSeries().setCategoryData("A2:A6");
```

Chúng ta đã thêm một biểu đồ thác nước vào worksheet, chỉ định series dữ liệu và dữ liệu danh mục. Đây là bước cốt lõi mà **thêm biểu đồ thác nước** vào sheet của bạn. Bạn có thể tùy chỉnh thêm giao diện biểu đồ (màu sắc, nhãn dữ liệu, v.v.) bằng cách sử dụng các thuộc tính của đối tượng `Chart`.

### Bước 5: Lưu Workbook

```java
workbook.save("WaterfallChart.xlsx");
```

Lưu workbook vào một tệp. Ví dụ sử dụng định dạng XLSX, nhưng Aspose.Cells cũng cho phép bạn xuất ra PDF, CSV và nhiều định dạng khác. Điều này đáp ứng yêu cầu **save workbook xlsx**.

## Các vấn đề thường gặp và giải pháp

- **Biểu đồ hiện ra trống** – Kiểm tra rằng các tham chiếu phạm vi dữ liệu (`B2:B6` và `A2:A6`) khớp với các ô thực tế chứa giá trị và danh mục của bạn.  
- **Giá trị âm không hiển thị đúng** – Đảm bảo loại series được đặt thành `ChartType.WATERFALL`; các loại biểu đồ khác xử lý giá trị âm khác nhau.  
- **Tệp không mở được trong Excel** – Đảm bảo bạn đang sử dụng phiên bản mới nhất của Aspose.Cells (bản phát hành mới nhất) và phần mở rộng tệp khớp với định dạng (`.xlsx` cho Excel).

## Câu hỏi thường gặp

### Làm thế nào tôi có thể tùy chỉnh giao diện của biểu đồ thác nước?

Bạn có thể tùy chỉnh giao diện của biểu đồ thác nước bằng cách thay đổi các thuộc tính như màu sắc, nhãn dữ liệu và nhãn trục. Tham khảo tài liệu Aspose.Cells để biết hướng dẫn chi tiết.

### Tôi có thể tạo nhiều biểu đồ thác nước trong cùng một worksheet không?

Có, bạn có thể tạo nhiều biểu đồ thác nước trong cùng một worksheet bằng cách thực hiện các bước tương tự với các phạm vi dữ liệu khác nhau.

### Aspose.Cells có tương thích với các môi trường phát triển Java khác nhau không?

Có, Aspose.Cells cho Java tương thích với nhiều môi trường phát triển Java, bao gồm Eclipse, IntelliJ IDEA và NetBeans.

### Tôi có thể thêm series dữ liệu bổ sung vào biểu đồ thác nước của mình không?

Chắc chắn, bạn có thể thêm nhiều series dữ liệu vào biểu đồ thác nước để biểu diễn các kịch bản dữ liệu phức tạp một cách hiệu quả.

### Tôi có thể tìm thêm tài nguyên và ví dụ cho Aspose.Cells cho Java ở đâu?

Bạn có thể khám phá tài liệu cho Aspose.Cells cho Java tại [reference.aspose.com/cells/java/](https://reference.aspose.com/cells/java/) để có thông tin chi tiết và các ví dụ mã.

---

**Cập nhật lần cuối:** 2025-12-10  
**Kiểm tra với:** Aspose.Cells for Java 24.12 (mới nhất)  
**Tác giả:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}