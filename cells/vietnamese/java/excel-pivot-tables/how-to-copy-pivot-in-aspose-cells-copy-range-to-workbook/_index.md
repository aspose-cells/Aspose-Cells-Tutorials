---
category: general
date: 2026-08-08
description: Cách sao chép pivot trong Aspose.Cells và sao chép phạm vi vào workbook
  bằng Java. Tìm hiểu các bước chính xác để sao chép một bảng pivot bằng CopyOptions.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot
- copy range to workbook
- aspose.cells copy range
language: vi
lastmod: 2026-08-08
og_description: Cách sao chép pivot trong Aspose.Cells và sao chép vùng dữ liệu vào
  workbook bằng Java. Hãy theo dõi hướng dẫn đầy đủ này để nhân bản bảng pivot bằng
  cách sử dụng CopyOptions.
og_image_alt: Diagram showing how to copy pivot in Aspose.Cells
og_title: Cách sao chép Pivot trong Aspose.Cells – sao chép phạm vi vào workbook
schemas:
- author: Aspose
  dateModified: '2026-08-08'
  description: How to copy pivot in Aspose.Cells and copy range to workbook using
    Java. Learn the exact steps to duplicate a pivot table with CopyOptions.
  headline: How to copy pivot in Aspose.Cells – copy range to workbook
  type: TechArticle
- description: How to copy pivot in Aspose.Cells and copy range to workbook using
    Java. Learn the exact steps to duplicate a pivot table with CopyOptions.
  name: How to copy pivot in Aspose.Cells – copy range to workbook
  steps:
  - name: Add Aspose.Cells to your project
    text: 'If you use Maven, add the following dependency to your `pom.xml`:'
  - name: Load the source workbook
    text: '```java import com.aspose.cells.*;'
  - name: Configure copy options to include the pivot table
    text: '```java // Define copy options to include the pivot table in the copied
      range CopyOptions copyOptions = new CopyOptions() .setCopyPivotTable(true);
      ```'
  - name: Copy the desired range with the pivot table
    text: '```java // Copy the range A1:H20, preserving the pivot table workbook.getWorksheets().get(0).getCells()
      .copyRange("A1:H20", copyOptions); ```'
  - name: Save the modified workbook
    text: '```java // Save the workbook with the copied pivot table workbook.save("YOUR_DIRECTORY/output.xlsx");
      } } ```'
  - name: Expected result
    text: '* `output.xlsx` contains the same data as `input.xlsx`. * The pivot table
      that originally occupied the source range appears in the destination cells,
      fully functional (filters, refresh capability, etc.). * All cell formatting,
      formulas, and column widths are preserved because `copyRange` copies the '
  type: HowTo
tags:
- Aspose.Cells
- Java
- PivotTable
- CopyRange
title: Cách sao chép pivot trong Aspose.Cells – sao chép phạm vi vào sổ làm việc
url: /vi/java/excel-pivot-tables/how-to-copy-pivot-in-aspose-cells-copy-range-to-workbook/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách sao chép pivot trong Aspose.Cells – sao chép phạm vi vào workbook

Nếu bạn cần **cách sao chép pivot** trong một tệp Excel bằng Aspose.Cells, hướng dẫn này sẽ cho bạn quy trình chính xác. Khi kết thúc tutorial, bạn sẽ có thể **sao chép phạm vi vào workbook** trong khi giữ nguyên định nghĩa của bảng pivot.

Ví dụ sử dụng Java, nhưng các khái niệm tương tự áp dụng cho bất kỳ ngôn ngữ .NET nào làm việc với Aspose.Cells. Không cần công cụ bên ngoài—chỉ cần thư viện Aspose.Cells cho Java và môi trường phát triển cơ bản.

## Yêu cầu trước

Trước khi bắt đầu, hãy chắc chắn rằng bạn có:

* Java Development Kit (JDK) 8 hoặc mới hơn.
* Maven hoặc Gradle để quản lý các phụ thuộc (ví dụ sử dụng Maven).
* Aspose.Cells for Java 23.9 (hoặc phiên bản mới nhất) được thêm vào dự án của bạn.
* Một workbook đầu vào (`input.xlsx`) chứa ít nhất một bảng pivot trên worksheet đầu tiên.

Có sẵn các mục này sẽ ngăn ngừa lỗi thời gian chạy khi mã truy cập workbook.

## Cách sao chép pivot với Aspose.Cells

Phần này hướng dẫn từng bước cần thiết để **cách sao chép pivot** từ một phần của sheet sang phần khác, sử dụng lớp `CopyOptions`.

### Bước 1: Thêm Aspose.Cells vào dự án của bạn

Nếu bạn sử dụng Maven, thêm phụ thuộc sau vào file `pom.xml` của bạn:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
    <classifier>jdk17</classifier> <!-- adjust JDK version as needed -->
</dependency>
```

*​Tại sao bước này quan trọng*: Thư viện cung cấp các lớp `Workbook`, `CopyOptions`, và các lớp khác cần thiết cho các thao tác **aspose.cells copy range**. Nếu thiếu phụ thuộc, trình biên dịch sẽ không thể giải quyết các kiểu này.

### Bước 2: Tải workbook nguồn

```java
import com.aspose.cells.*;

public class CopyPivotTableRange {
    public static void main(String[] args) throws Exception {
        // Load the workbook that contains the pivot table
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

Việc tải tệp tạo ra một biểu diễn trong bộ nhớ của bảng tính. Đối tượng `Workbook` cho phép bạn truy cập vào worksheets, cells và pivot tables.

### Bước 3: Cấu hình tùy chọn sao chép để bao gồm bảng pivot

```java
        // Define copy options to include the pivot table in the copied range
        CopyOptions copyOptions = new CopyOptions()
                .setCopyPivotTable(true);
```

`CopyOptions.setCopyPivotTable(true)` thông báo cho Aspose.Cells rằng thao tác này nên giữ nguyên siêu dữ liệu của bảng pivot. Nếu bạn bỏ qua cờ này, bảng pivot sẽ bị chuyển thành dữ liệu tĩnh, mất tính tương tác.

### Bước 4: Sao chép phạm vi mong muốn cùng với bảng pivot

```java
        // Copy the range A1:H20, preserving the pivot table
        workbook.getWorksheets().get(0).getCells()
                .copyRange("A1:H20", copyOptions);
```

Phương thức `copyRange` sao chép các ô, định dạng, và—do các tùy chọn được thiết lập ở bước trước—bất kỳ bảng pivot nào giao nhau với phạm vi. Đây là phần cốt lõi của chức năng **copy range to workbook**.

### Bước 5: Lưu workbook đã chỉnh sửa

```java
        // Save the workbook with the copied pivot table
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

Lưu sẽ ghi các thay đổi vào một tệp mới (`output.xlsx`). Bây giờ bạn có thể mở tệp này trong Excel và thấy bảng pivot đã được sao chép chính xác ở vị trí mà phạm vi được sao chép.

## Ví dụ đầy đủ, có thể chạy

Kết hợp tất cả các phần lại, đây là chương trình hoàn chỉnh mà bạn có thể biên dịch và chạy:

```java
import com.aspose.cells.*;

public class CopyPivotTableRange {
    public static void main(String[] args) throws Exception {
        // 1. Load the workbook that contains the pivot table
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // 2. Define copy options to include the pivot table
        CopyOptions copyOptions = new CopyOptions()
                .setCopyPivotTable(true);

        // 3. Copy the range A1:H20 with the specified options
        workbook.getWorksheets().get(0).getCells()
                .copyRange("A1:H20", copyOptions);

        // 4. Save the modified workbook
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

### Kết quả mong đợi

* `output.xlsx` chứa cùng dữ liệu với `input.xlsx`.
* Bảng pivot ban đầu chiếm phạm vi nguồn sẽ xuất hiện trong các ô đích, hoạt động đầy đủ (bộ lọc, khả năng làm mới, v.v.).
* Tất cả định dạng ô, công thức và độ rộng cột được giữ nguyên vì `copyRange` sao chép toàn bộ khối ô.

## Các câu hỏi thường gặp và trường hợp đặc biệt

**Nếu phạm vi đích trùng lặp với một bảng pivot hiện có thì sao?**  
Aspose.Cells sẽ ghi đè lên các ô mục tiêu. Để tránh mất dữ liệu, hãy đảm bảo khu vực đích trống hoặc di chuyển bảng pivot hiện có trước.

**Tôi có thể sao chép một bảng pivot sang các worksheet khác không?**  
Có. Sử dụng `workbook.getWorksheets().get(targetSheetIndex).getCells().copyRange(sourceRange, copyOptions);` trong đó `targetSheetIndex` chỉ tới sheet đích.

**`setCopyPivotTable(true)` có sao chép nguồn dữ liệu nền không?**  
Phương thức chỉ sao chép tham chiếu đến pivot cache. Nếu dữ liệu nguồn nằm trong cùng một workbook, pivot đích sẽ trỏ tới cùng cache. Để sao chép cache, bạn phải tạo một pivot cache mới thủ công.

**Làm sao sao chép một phạm vi lớn một cách hiệu quả?**  
Khi sao chép các phạm vi rất lớn, hãy cân nhắc chỉ sử dụng `CopyOptions.setCopyFormula(true)` và `setCopyDataValidation(true)` khi cần thiết. Giảm số lượng tùy chọn có thể cải thiện hiệu năng.

## Mẹo để sử dụng **aspose.cells copy range** một cách đáng tin cậy

* **Mẹo chuyên nghiệp:** Luôn gọi `workbook.calculateFormula()` sau khi sao chép nếu phạm vi chứa công thức phụ thuộc vào pivot cache.
* **Cảnh báo:** Các worksheet ẩn. `copyRange` chỉ hoạt động trên các worksheet hiển thị trừ khi bạn tham chiếu rõ ràng đến sheet ẩn bằng chỉ số.
* **Kiểm tra phiên bản:** Cờ `setCopyPivotTable` có sẵn từ Aspose.Cells 20.9. Đảm bảo phiên bản thư viện của bạn hỗ trợ tính năng này.

## Kết luận

Bây giờ bạn đã biết **cách sao chép pivot** trong Aspose.Cells và cách **sao chép phạm vi vào workbook** trong khi giữ nguyên toàn bộ chức năng của pivot. Các bước—thêm thư viện, tải workbook, cấu hình `CopyOptions`, thực hiện sao chép và lưu—tạo thành một mẫu lặp lại mà bạn có thể áp dụng cho các kịch bản sao chép‑dán khác.

Tiếp theo, khám phá các chủ đề liên quan như **aspose.cells copy range** cho biểu đồ, định dạng có điều kiện và xác thực dữ liệu. Thử nghiệm sao chép giữa các định dạng tệp khác nhau (XLSX → XLS) để mở rộng khả năng tự động hoá của bạn. Chúc lập trình vui vẻ!

## Bạn Nên Học Gì Tiếp Theo?

Các tutorial sau đây bao gồm các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoạt động đầy đủ với giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Cách Tạo Bảng Pivot trong Excel Sử Dụng Aspose.Cells cho Java: Hướng Dẫn Toàn Diện](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [Cách Cập Nhật Nguồn Bảng Pivot Excel với Aspose.Cells cho Java: Hướng Dẫn Toàn Diện](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Cách Triển Khai Slicer trong Bảng Pivot Sử Dụng Aspose.Cells cho Java: Hướng Dẫn Toàn Diện](/cells/english/java/data-analysis/implement-slicers-pivot-tables-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}