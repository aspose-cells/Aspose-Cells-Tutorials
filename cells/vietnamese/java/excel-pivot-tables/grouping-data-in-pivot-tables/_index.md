---
title: Nhóm dữ liệu trong bảng Pivot
linktitle: Nhóm dữ liệu trong bảng Pivot
second_title: API xử lý Excel Java của Aspose.Cells
description: Tìm hiểu cách tạo bảng trục trong Excel bằng Aspose.Cells for Java. Tự động hóa việc nhóm và phân tích dữ liệu với các ví dụ về mã nguồn.
weight: 14
url: /vi/java/excel-pivot-tables/grouping-data-in-pivot-tables/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Nhóm dữ liệu trong bảng Pivot


Pivot table là một công cụ mạnh mẽ để phân tích và tóm tắt dữ liệu trong bảng tính. Chúng cho phép bạn nhóm và phân loại dữ liệu để có được những hiểu biết có giá trị. Trong bài viết này, chúng ta sẽ khám phá cách nhóm dữ liệu hiệu quả trong pivot table bằng Aspose.Cells for Java, cùng với các ví dụ về mã nguồn.

## Giới thiệu

Bảng Pivot cung cấp một cách linh hoạt để sắp xếp và tóm tắt dữ liệu từ các tập dữ liệu lớn. Chúng cho phép bạn tạo chế độ xem tùy chỉnh cho dữ liệu của mình bằng cách nhóm dữ liệu vào các danh mục hoặc phân cấp. Điều này có thể giúp bạn xác định xu hướng, mẫu và giá trị ngoại lệ trong dữ liệu của mình dễ dàng hơn.

## Bước 1: Tạo Bảng Pivot

Chúng ta hãy bắt đầu bằng cách tạo một bảng trục bằng Aspose.Cells for Java. Dưới đây là ví dụ về cách tạo một bảng trục từ một tệp Excel mẫu.

```java
// Tải tệp Excel
Workbook workbook = new Workbook("sample.xlsx");

// Truy cập vào bảng tính chứa dữ liệu
Worksheet worksheet = workbook.getWorksheets().get(0);

// Chỉ định phạm vi dữ liệu
CellArea sourceData = new CellArea();
sourceData.startRow = 0;
sourceData.endRow = 19; // Giả sử có 20 hàng dữ liệu
sourceData.startColumn = 0;
sourceData.endColumn = 3; // Giả sử 4 cột dữ liệu

// Tạo bảng trục dựa trên phạm vi dữ liệu
int index = worksheet.getPivotTables().add(sourceData, "A1", "PivotTable1");

// Lấy bảng trục theo chỉ mục
PivotTable pivotTable = worksheet.getPivotTables().get(index);

// Thêm trường vào hàng và cột
pivotTable.addFieldToArea("Product", PivotFieldType.ROW);
pivotTable.addFieldToArea("Region", PivotFieldType.COLUMN);

// Thêm giá trị và áp dụng tổng hợp
pivotTable.addFieldToArea("Sales", PivotFieldType.DATA);
pivotTable.getDataFields().get(0).setFunction(PivotFieldFunction.SUM);

// Lưu tệp Excel đã sửa đổi
workbook.save("output.xlsx");
```

## Bước 2: Nhóm dữ liệu

 Trong Aspose.Cells cho Java, bạn có thể nhóm dữ liệu trong bảng trục bằng cách sử dụng`PivotField` lớp. Sau đây là ví dụ về cách nhóm một trường trong bảng trục:

```java
// Truy cập trường "Sản phẩm" trong bảng trục
PivotField productField = pivotTable.getPivotFields().get("Product");

//Nhóm trường "Sản phẩm" theo tiêu chí cụ thể, ví dụ, theo chữ cái bắt đầu
productField.setIsAutoSubtotals(false);
productField.setBaseField("Product");
productField.setAutoSort(true);
productField.setAutoShow(true);

// Lưu tệp Excel đã sửa đổi với dữ liệu được nhóm lại
workbook.save("output_grouped.xlsx");
```

## Bước 3: Tùy chỉnh nhóm

Bạn có thể tùy chỉnh thêm các thiết lập nhóm, chẳng hạn như chỉ định khoảng thời gian nhóm theo ngày hoặc các quy tắc nhóm tùy chỉnh. Sau đây là ví dụ về tùy chỉnh nhóm theo ngày:

```java
// Truy cập trường "Ngày" trong bảng trục (giả sử đó là trường ngày)
PivotField dateField = pivotTable.getPivotFields().get("Date");

// Nhóm ngày theo tháng
dateField.setIsAutoSubtotals(false);
dateField.setIsDateGroup(true);
dateField.setDateGroupingType(PivotFieldDateGroupingType.MONTHS);

// Lưu tệp Excel đã sửa đổi với nhóm ngày tùy chỉnh
workbook.save("output_custom_grouping.xlsx");
```

## Phần kết luận

Nhóm dữ liệu trong các bảng trục là một kỹ thuật có giá trị để phân tích và tóm tắt dữ liệu trong Excel và Aspose.Cells for Java giúp bạn dễ dàng tự động hóa quy trình này. Với các ví dụ về mã nguồn được cung cấp, bạn có thể tạo các bảng trục, tùy chỉnh nhóm và thu thập thông tin chi tiết từ dữ liệu của mình một cách hiệu quả.

## Câu hỏi thường gặp

### 1. Mục đích của bảng Pivot trong Excel là gì?

Bảng Pivot trong Excel được sử dụng để tóm tắt và phân tích các tập dữ liệu lớn. Chúng cho phép bạn tạo chế độ xem tùy chỉnh cho dữ liệu của mình, giúp xác định các mẫu và xu hướng dễ dàng hơn.

### 2. Làm thế nào để tùy chỉnh nhóm dữ liệu trong bảng tổng hợp?

 Bạn có thể tùy chỉnh nhóm dữ liệu trong bảng trục bằng cách sử dụng`PivotField` lớp trong Aspose.Cells cho Java. Điều này cho phép bạn chỉ định tiêu chí nhóm, chẳng hạn như khoảng thời gian dựa trên ngày hoặc quy tắc tùy chỉnh.

### 3. Tôi có thể tự động tạo bảng trục bằng Aspose.Cells cho Java không?

Có, bạn có thể tự động tạo bảng tổng hợp trong Excel bằng Aspose.Cells cho Java, như được minh họa trong các ví dụ về mã nguồn được cung cấp.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
