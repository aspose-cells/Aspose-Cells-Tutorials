---
date: 2026-02-16
description: Tìm hiểu cách đặt phạm vi dữ liệu cho biểu đồ và tạo biểu đồ thác nước
  trong Java bằng Aspose.Cells. Hướng dẫn từng bước để thêm biểu đồ chuỗi dữ liệu,
  tùy chỉnh và xuất ra XLSX.
linktitle: Waterfall Charts
second_title: Aspose.Cells Java Excel Processing API
title: Thiết lập phạm vi dữ liệu biểu đồ – Biểu đồ thác nước Aspose.Cells cho Java
url: /vi/java/advanced-excel-charts/waterfall-charts/
weight: 18
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Biểu đồ Waterfall

## Giới thiệu về Biểu đồ Waterfall sử dụng Aspose.Cells cho Java

Trong tutorial này, bạn sẽ học cách **set chart data range** và tạo một **waterfall chart** với Aspose.Cells cho Java. Biểu đồ waterfall là công cụ thiết yếu trong việc trực quan hoá dữ liệu vì chúng cho phép bạn thấy hiệu ứng cộng dồn của một loạt các giá trị dương và âm. Dù bạn đang chuẩn bị báo cáo tài chính, báo cáo hiệu suất bán hàng, hay bất kỳ phân tích dựa trên dữ liệu nào khác, biểu đồ waterfall có thể biến các con số thô thành những hiểu biết rõ ràng, có thể hành động.

## Quick Answers
- **What is a waterfall chart?** Biểu đồ waterfall là gì?  
  Một hình ảnh trực quan cho thấy cách một giá trị ban đầu được tăng và giảm bởi một loạt các giá trị trung gian, kết thúc bằng tổng cuối cùng.  
- **Which library is used?** Thư viện nào được sử dụng?  
  Aspose.Cells cho Java.  
- **Do I need a license?** Tôi có cần giấy phép không?  
  Bản dùng thử miễn phí hoạt động cho phát triển; giấy phép thương mại cần thiết cho môi trường sản xuất.  
- **Can I save the file as XLSX?** Tôi có thể lưu tệp dưới dạng XLSX không?  
  Có – sử dụng `workbook.save("FileName.xlsx")`.  
- **Is it suitable for Java data visualization?** Có phù hợp cho việc trực quan hoá dữ liệu Java không?  
  Chắc chắn; Aspose.Cells cung cấp các tính năng biểu đồ phong phú mà không cần cài đặt Office.

## What is a Waterfall Chart?
Biểu đồ waterfall hiển thị các đóng góp dương và âm theo thứ tự vào một giá trị bắt đầu, giúp bạn hiểu cách mỗi thành phần ảnh hưởng đến kết quả tổng thể.

## Why Use Aspose.Cells for Java to Add a Waterfall Chart?
- **No Microsoft Excel required** – Không cần Microsoft Excel – tạo biểu đồ trên bất kỳ máy chủ hoặc pipeline CI nào.  
- **Full control over formatting** – Kiểm soát hoàn toàn việc định dạng – màu sắc, nhãn dữ liệu và trục có thể được tùy chỉnh bằng mã.  
- **Supports multiple output formats** – Hỗ trợ nhiều định dạng xuất – XLSX, PDF, HTML và hơn nữa.  
- **High performance** – Hiệu năng cao – lý tưởng cho sổ làm việc lớn và báo cáo tự động.

## Prerequisites

Trước khi chúng ta bắt đầu với mã, hãy đảm bảo bạn đã chuẩn bị các yêu cầu sau:

- Aspose.Cells cho Java: Bạn sẽ cần cài đặt Aspose.Cells cho Java. Bạn có thể tải xuống từ [here](https://releases.aspose.com/cells/java/).

- Môi trường phát triển Java: Đảm bảo bạn đã cài đặt Java trên hệ thống của mình.

Bây giờ, hãy bắt đầu tạo biểu đồ waterfall từng bước.

## How to Set Chart Data Range for a Waterfall Chart in Java

### Step 1: Import Aspose.Cells

```java
import com.aspose.cells.*;
```

Đầu tiên, bạn cần nhập thư viện Aspose.Cells vào dự án Java của mình. Thư viện này cung cấp chức năng phong phú để làm việc với tệp Excel, bao gồm việc tạo biểu đồ.

### Step 2: Initialize Workbook and Worksheet

```java
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.getWorksheets().get(0);
```

Tạo một workbook mới và thêm một worksheet vào đó. Chúng ta sẽ sử dụng worksheet này để nhập dữ liệu và **add chart to worksheet**.

### Step 3: Enter Data

Bây giờ, hãy điền dữ liệu vào worksheet mà chúng ta muốn biểu diễn trong biểu đồ waterfall.

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

### Step 4: Create the Waterfall Chart

```java
int chartIndex = worksheet.getCharts().add(ChartType.WATERFALL, 5, 0, 15, 5);
Chart waterfallChart = worksheet.getCharts().get(chartIndex);
waterfallChart.getNSeries().add("B2:B6", true);
waterfallChart.getNSeries().setCategoryData("A2:A6");
```

Chúng tôi đã thêm một waterfall chart vào worksheet, chỉ định series dữ liệu và dữ liệu danh mục. Đây là bước cốt lõi mà **adds waterfall chart** vào sheet của bạn. Lưu ý cách phương thức `add` sử dụng phạm vi `"B2:B6"` – đây là nơi chúng ta **set chart data range** cho series. Bạn có thể tùy chỉnh thêm giao diện biểu đồ (màu sắc, nhãn dữ liệu, v.v.) bằng cách sử dụng các thuộc tính của đối tượng `Chart`.

### Step 5: Save the Workbook

```java
workbook.save("WaterfallChart.xlsx");
```

Lưu workbook vào một tệp. Ví dụ sử dụng định dạng XLSX, nhưng Aspose.Cells cũng cho phép bạn **export excel pdf java**‑compatible như PDF, CSV và nhiều định dạng khác. Điều này đáp ứng yêu cầu **save workbook xlsx**.

## Common Issues and Solutions

- **Chart appears blank** – Kiểm tra xem các tham chiếu phạm vi dữ liệu (`B2:B6` và `A2:A6`) có khớp với các ô thực tế chứa giá trị và danh mục của bạn không.  
- **Negative values not displayed correctly** – Đảm bảo loại series được đặt thành `ChartType.WATERFALL`; các loại biểu đồ khác xử lý giá trị âm khác nhau.  
- **File not opening in Excel** – Đảm bảo bạn đang sử dụng phiên bản mới nhất của Aspose.Cells (bản phát hành mới nhất) và phần mở rộng tệp phù hợp với định dạng (`.xlsx` cho Excel).

## Frequently Asked Questions

### How can I customize the appearance of my waterfall chart?

Bạn có thể tùy chỉnh giao diện của biểu đồ waterfall bằng cách sửa đổi các thuộc tính như màu sắc, nhãn dữ liệu và nhãn trục. Tham khảo tài liệu Aspose.Cells để biết hướng dẫn chi tiết.

### Can I create multiple waterfall charts in the same worksheet?

Có, bạn có thể tạo nhiều biểu đồ waterfall trong cùng một worksheet bằng cách thực hiện các bước tương tự với các phạm vi dữ liệu khác nhau.

### Is Aspose.Cells compatible with different Java development environments?

Có, Aspose.Cells cho Java tương thích với nhiều môi trường phát triển Java, bao gồm Eclipse, IntelliJ IDEA và NetBeans.

### Can I add additional data series to my waterfall chart?

Chắc chắn, bạn có thể thêm nhiều series dữ liệu vào biểu đồ waterfall để biểu diễn các kịch bản dữ liệu phức tạp một cách hiệu quả. Đây là một ví dụ về cách bạn có thể **add data series chart** bằng chương trình.

### Where can I find more resources and examples for Aspose.Cells for Java?

Bạn có thể khám phá tài liệu cho Aspose.Cells cho Java tại [reference.aspose.com/cells/java/](https://reference.aspose.com/cells/java/) để có thông tin chi tiết và các ví dụ mã.

## FAQ

**Q: How do I set the chart data range for a financial waterfall chart?**  
A: Sử dụng phương thức `add` trên series của biểu đồ, truyền vào phạm vi ô chứa giá trị của bạn, ví dụ, `"B2:B6"`.

**Q: Can I export the workbook to PDF instead of XLSX?**  
A: Có, gọi `workbook.save("WaterfallChart.pdf", SaveFormat.PDF);` để **export excel pdf java**‑compatible output.

**Q: What if I need to create a financial waterfall chart with more categories?**  
A: Mở rộng phạm vi dữ liệu trong cả cột giá trị và cột danh mục, sau đó cập nhật các lời gọi `add` và `setCategoryData` cho phù hợp.

**Q: Is there a way to automatically format positive and negative bars?**  
A: Bạn có thể duyệt qua collection `Series` và đặt màu `FillFormat` dựa trên dấu của mỗi giá trị.

**Q: Does Aspose.Cells support dynamic data updates for charts?**  
A: Có, bạn có thể sửa đổi giá trị ô sau khi biểu đồ được tạo; biểu đồ sẽ phản ánh các thay đổi khi workbook được lưu.

---

**Last Updated:** 2026-02-16  
**Tested With:** Aspose.Cells cho Java (phiên bản mới nhất)  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}