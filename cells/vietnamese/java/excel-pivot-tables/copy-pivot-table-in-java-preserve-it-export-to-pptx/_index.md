---
category: general
date: 2026-03-01
description: Sao chép bảng pivot trong Java đồng thời giữ nguyên pivot, sau đó xuất
  Excel sang PPTX, tắt AutoFilter của Excel và sử dụng Smart Marker cho các mảng JSON
  – hướng dẫn chi tiết từng bước.
draft: false
keywords:
- copy pivot table
- preserve pivot table
- use smart marker
- disable excel autofilter
- export excel to pptx
language: vi
og_description: Sao chép bảng pivot trong Java, giữ nguyên định nghĩa pivot, xuất
  ra PPTX, tắt AutoFilter và sử dụng Smart Marker – hướng dẫn đầy đủ cho nhà phát
  triển.
og_title: Sao chép Pivot Table trong Java – Bảo tồn nó, Xuất ra PPTX
tags:
- Aspose.Cells
- Java
- Excel Automation
title: Sao chép Pivot Table trong Java – Bảo tồn, Xuất ra PPTX
url: /vi/java/excel-pivot-tables/copy-pivot-table-in-java-preserve-it-export-to-pptx/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Sao chép Pivot Table trong Java – Bảo tồn, Xuất ra PPTX

Bạn đã bao giờ cần **copy pivot table** từ một workbook sang workbook khác mà không mất định nghĩa pivot bên dưới chưa? Bạn không phải là người duy nhất bối rối về vấn đề này. Trong nhiều dự án thực tế, bạn sẽ phải di chuyển dữ liệu, và điều cuối cùng bạn muốn là một pivot bị hỏng gây lỗi khi chạy.  

Trong hướng dẫn này, chúng ta sẽ đi qua một giải pháp hoàn chỉnh không chỉ **copy pivot table** mà còn chỉ cho bạn cách **preserve pivot table** khi sao chép, **export Excel to PPTX**, **disable Excel AutoFilter**, và **use smart marker** để chèn một mảng JSON vào một ô duy nhất. Khi kết thúc, bạn sẽ có một chương trình Java duy nhất, có thể chạy được, bao gồm cả bốn kịch bản.

## Yêu cầu trước

- Java 8 hoặc mới hơn (mã vẫn hoạt động với Java 11)  
- Thư viện Aspose.Cells for Java (phiên bản 23.9 trở lên) – bạn có thể tải từ Maven Central  
- Kiến thức cơ bản về các khái niệm Excel như pivot tables, tables và text boxes  

Nếu bạn thiếu file JAR của Aspose.Cells, hãy thêm đoạn này vào `pom.xml` của bạn:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
</dependency>
```

Bây giờ, chúng ta cùng bắt đầu.

## Bước 1: Sao chép Pivot Table – Bảo tồn Định nghĩa Pivot

Khi bạn chỉ sao chép phạm vi ô chứa pivot table, siêu dữ liệu pivot thường bị bỏ lại. Aspose.Cells cung cấp cho chúng ta một cách gọn gàng để giữ nguyên định nghĩa bằng cách sử dụng `copyRange` cùng một đối tượng `CopyOptions`.

```java
import com.aspose.cells.*;

public class PivotCopyDemo {

    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the source workbook that contains the pivot table
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/src.xlsx");
        Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);

        // 2️⃣ Define the range that includes the pivot (A1:G20 is just an example)
        Range pivotRange = sourceSheet.getCells().createRange("A1:G20");

        // 3️⃣ Prepare the destination workbook
        Workbook destWorkbook = new Workbook();
        Worksheet destSheet = destWorkbook.getWorksheets().get(0);

        // 4️⃣ Copy the range – the pivot definition travels with it
        destSheet.getCells().copyRange(pivotRange,
                new CellArea(0, 0, 19, 6), // destination area (rows 0‑19, cols 0‑6)
                new CopyOptions());

        // 5️⃣ Save the result
        destWorkbook.save("YOUR_DIRECTORY/dest.xlsx");
    }
}
```

**Tại sao cách này hoạt động:** `CopyOptions` chỉ cho Aspose.Cells sao chép mọi thứ, bao gồm pivot cache và cài đặt trường. Nếu không có nó, bạn sẽ chỉ nhận được giá trị thuần và mất khả năng làm mới pivot.

**Trường hợp đặc biệt:** Nếu pivot nguồn của bạn mở rộng hơn phạm vi cứng `A1:G20`, hãy điều chỉnh phạm vi cho phù hợp hoặc sử dụng `sourceSheet.getPivotTables().get(0).getDataRange()` để lấy động.

![Ví dụ sao chép pivot table](image.png "Sao chép pivot table trong Java")

*Văn bản thay thế hình ảnh: sơ đồ sao chép pivot table trong Java*

## Bước 2: Xuất Worksheet có TextBox có thể chỉnh sửa ra PPTX

Thường bạn cần chuyển một sheet Excel thành một slide PowerPoint—như các bảng điều khiển hàng tuần cần trình bày. Aspose.Cells có thể trực tiếp lưu một worksheet dưới dạng file PPTX đồng thời bảo tồn các hình dạng như text boxes.

```java
import com.aspose.cells.*;

public class ExportToPptxDemo {

    public static void main(String[] args) throws Exception {
        // Load workbook that contains a TextBox shape
        Workbook wb = new Workbook("YOUR_DIRECTORY/textbox.xlsx");

        // Export the first worksheet to PPTX
        wb.save("YOUR_DIRECTORY/output.pptx", SaveFormat.PPTX);

        System.out.println("Worksheet exported to PPTX successfully.");
    }
}
```

**Điều gì đang xảy ra:** Phương thức `save` với `SaveFormat.PPTX` chuyển đổi toàn bộ sheet, bao gồm bất kỳ TextBox có thể chỉnh sửa nào, thành một slide PowerPoint. Văn bản bên trong hộp vẫn có thể chỉnh sửa khi bạn mở PPTX trong PowerPoint.

**Mẹo:** Nếu bạn có nhiều sheet và chỉ muốn một sheet cụ thể, hãy gọi `wb.getWorksheets().removeAt(index)` cho các sheet còn lại trước khi lưu.

## Bước 3: Vô hiệu hoá Excel AutoFilter từ một Table

AutoFilter hữu ích cho người dùng cuối, nhưng đôi khi bạn cần tắt nó bằng chương trình—có thể trước khi xuất dữ liệu hoặc khi tạo báo cáo sạch. Đây là cách **disable excel autofilter** trên một Table trong Excel.

```java
import com.aspose.cells.*;

public class DisableAutoFilterDemo {

    public static void main(String[] args) throws Exception {
        Workbook wb = new Workbook("YOUR_DIRECTORY/textbox.xlsx");
        Worksheet sheet = wb.getWorksheets().get(0);

        // Assume the first table in the sheet is the target
        Table table = sheet.getTables().get(0);

        // Turn off the AutoFilter arrows
        table.setShowAutoFilter(false);

        // Save the modified workbook
        wb.save("YOUR_DIRECTORY/noFilter.xlsx");
        System.out.println("AutoFilter disabled and workbook saved.");
    }
}
```

**Lý do bạn có thể cần điều này:** Khi xuất sang các định dạng không hỗ trợ AutoFilter (như CSV hoặc PDF) có thể xuất hiện các biểu tượng lọc lạ. Việc tắt nó đảm bảo đầu ra sạch sẽ.

**Cạm bẫy thường gặp:** Nếu sheet không có table, `getTables().get(0)` sẽ ném `IndexOutOfBoundsException`. Luôn kiểm tra `sheet.getTables().size()` trước trong mã production.

## Bước 4: Sử dụng Smart Marker – Chèn một Mảng JSON làm Giá trị Ô Đơn

Smart Marker là công cụ tạo mẫu của Aspose. Một mẹo hữu ích là coi toàn bộ mảng JSON như một giá trị ô duy nhất, rất phù hợp cho việc ghi log hoặc truyền dữ liệu có cấu trúc xuống phía dưới. Hãy **use smart marker** để thực hiện điều này.

```java
import com.aspose.cells.*;

public class SmartMarkerDemo {

    public static void main(String[] args) throws Exception {
        Workbook wb = new Workbook("YOUR_DIRECTORY/textbox.xlsx");

        // Initialise the SmartMarker processor with the workbook
        SmartMarkerProcessor processor = new SmartMarkerProcessor(wb);

        // JSON array we want to embed
        String jsonArray = "[{\"Name\":\"John\",\"Age\":30},{\"Name\":\"Anna\",\"Age\":28}]";

        // Configure the processor to treat arrays as a single cell
        processor.setOptions(SmartMarkerOptions.ArrayAsSingle);

        // Apply the marker – assume cell A1 contains the marker ${json}
        processor.apply(jsonArray);

        // Save the result
        wb.save("YOUR_DIRECTORY/smartMarkerResult.xlsx");
        System.out.println("JSON array inserted via Smart Marker.");
    }
}
```

**Cách hoạt động:** Marker `${json}` trong workbook sẽ được thay thế bằng toàn bộ chuỗi JSON vì chúng ta đã đặt `ArrayAsSingle`. Nếu không có tùy chọn này, Aspose sẽ cố gắng mở rộng mỗi phần tử mảng thành các hàng riêng biệt.

**Biến thể:** Nếu bạn muốn mảng được chia thành nhiều hàng, chỉ cần bỏ qua `ArrayAsSingle` và để Smart Marker tự động mở rộng.

## Ví dụ Hoạt động Đầy đủ – Kết hợp Tất cả Các Bước

Dưới đây là một lớp Java duy nhất kết hợp mọi thao tác chúng ta đã đề cập. Chạy nó như một phương thức `main` thông thường; chỉ cần điều chỉnh các đường dẫn file cho phù hợp với môi trường của bạn.

```java
import com.aspose.cells.*;

public class CompleteExcelAutomation {

    public static void main(String[] args) throws Exception {
        // ----------- Step 1: Copy Pivot Table -----------
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/src.xlsx");
        Worksheet srcSheet = srcWb.getWorksheets

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}