---
category: general
date: 2026-08-17
description: Cách sao chép trang tính trong Java bằng Aspose.Cells, giữ nguyên bảng
  pivot, sao chép bảng pivot sang workbook mới, và tạo workbook từ một sheet.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to duplicate worksheet
- how to copy pivot
- how to preserve pivot
- copy pivot to workbook
- create workbook from sheet
language: vi
lastmod: 2026-08-17
og_description: Cách sao chép bảng tính trong Java bằng Aspose.Cells, giữ nguyên bảng
  tổng hợp, sao chép bảng tổng hợp sang workbook mới, và tạo workbook từ một sheet—tất
  cả các bước được giải thích.
og_image_alt: Screenshot of Java code duplicating an Excel worksheet with a pivot
  table using Aspose.Cells
og_title: Cách sao chép bảng tính và giữ lại các bảng pivot – Hướng dẫn Java
schemas:
- author: Aspose
  dateModified: '2026-08-17'
  description: How to duplicate worksheet in Java using Aspose.Cells, preserving the
    pivot table, copying pivot to a new workbook, and creating a workbook from a sheet.
  headline: How to duplicate worksheet and preserve pivot tables in Java
  type: TechArticle
- description: How to duplicate worksheet in Java using Aspose.Cells, preserving the
    pivot table, copying pivot to a new workbook, and creating a workbook from a sheet.
  name: How to duplicate worksheet and preserve pivot tables in Java
  steps:
  - name: – Load the workbook that contains the pivot table
    text: '```java import com.aspose.cells.*;'
  - name: – Create a new workbook and duplicate the entire worksheet
    text: '```java // Create an empty destination workbook Workbook destinationWorkbook
      = new Workbook();'
  - name: – Save the new workbook
    text: '```java // Save the duplicated workbook; the pivot remains functional destinationWorkbook.save("YOUR_DIRECTORY/copy_with_pivot.xlsx");
      } } ```'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel
- Pivot Table
- Workbook
title: Cách sao chép bảng tính và giữ nguyên bảng tổng hợp trong Java
url: /vi/java/excel-pivot-tables/how-to-duplicate-worksheet-and-preserve-pivot-tables-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách sao chép worksheet và giữ nguyên bảng pivot trong Java

Việc sao chép worksheet trong khi giữ nguyên bảng pivot là một nhu cầu thường gặp khi bạn tự động hoá báo cáo Excel. Hướng dẫn này chỉ cho bạn cách sao chép pivot sang một workbook mới bằng Aspose.Cells for Java, và cũng đề cập cách giữ nguyên pivot khi bạn tạo một workbook từ một sheet.

Bạn sẽ học cách tải một workbook hiện có, sao chép worksheet chứa bảng pivot, và lưu kết quả thành một tệp mới. Hướng dẫn giả định bạn đã có môi trường phát triển Java cơ bản và một giấy phép Aspose.Cells hợp lệ (phiên bản dùng thử miễn phí đủ cho việc thử nghiệm). Không cần công cụ bên ngoài nào ngoài JAR của Aspose.Cells.

## Yêu cầu trước

Trước khi bắt đầu, hãy chắc chắn rằng bạn có:

* Java Development Kit (JDK) 8 hoặc mới hơn.
* Maven hoặc Gradle để quản lý phụ thuộc Aspose.Cells.
* Một tệp Excel (`source.xlsx`) chứa ít nhất một bảng pivot trên worksheet đầu tiên.
* Một thư mục nơi bạn có thể đọc tệp nguồn và ghi workbook đã sao chép.

Thêm phụ thuộc Aspose.Cells vào `pom.xml` (Maven) hoặc `build.gradle` (Gradle). Đối với Maven:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- use the latest version -->
</dependency>
```

## Cách sao chép worksheet có bảng pivot

Hoạt động cốt lõi là một quy trình ba bước: tải, sao chép và lưu. Mỗi bước được giải thích dưới đây.

### Bước 1 – Tải workbook chứa bảng pivot

```java
import com.aspose.cells.*;

public class CopyPivotTable {
    public static void main(String[] args) throws Exception {
        // Load the source workbook that holds the pivot table
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
        Worksheet sourceWorksheet = sourceWorkbook.getWorksheets().get(0);
```

*Why this step matters*: Đối tượng `Workbook` đại diện cho toàn bộ tệp Excel. Bằng cách lấy worksheet đầu tiên (`get(0)`), bạn nhắm vào sheet chứa bảng pivot mà bạn muốn sao chép.

### Bước 2 – Tạo một workbook mới và sao chép toàn bộ worksheet

```java
        // Create an empty destination workbook
        Workbook destinationWorkbook = new Workbook();

        // Duplicate the source worksheet, preserving its pivot table
        destinationWorkbook.getWorksheets().addCopy(sourceWorksheet);
```

`addCopy` sao chép worksheet **including** tất cả các đối tượng nhúng, công thức và pivot caches. Đây là cách được khuyến nghị để **how to copy pivot** vì định nghĩa pivot và nguồn dữ liệu của nó được chuyển cùng nhau.

### Bước 3 – Lưu workbook mới

```java
        // Save the duplicated workbook; the pivot remains functional
        destinationWorkbook.save("YOUR_DIRECTORY/copy_with_pivot.xlsx");
    }
}
```

Sau khi thực thi, `copy_with_pivot.xlsx` chứa một bản sao chính xác của sheet gốc, và bảng pivot hoạt động mà không cần cấu hình thêm.

**Expected result**: Mở `copy_with_pivot.xlsx` trong Excel sẽ hiển thị worksheet đã sao chép với cùng bố cục pivot, bộ lọc và các trường tính toán như tệp nguồn.

## Cách sao chép pivot sang một workbook khác

Nếu bạn cần di chuyển một bảng pivot mà không sao chép toàn bộ sheet, bạn có thể trích xuất pivot cache và gắn nó vào một worksheet mới. Đoạn mã sau minh họa cách tiếp cận này:

```java
// Assume sourceWorkbook and sourceWorksheet are already loaded
PivotTable pivot = sourceWorksheet.getPivotTables().get(0);

// Create a new workbook and a blank worksheet
Workbook targetWorkbook = new Workbook();
Worksheet targetSheet = targetWorkbook.getWorksheets().add("PivotCopy");

// Import the pivot table definition
targetSheet.getPivotTables().addCopy(pivot);
targetWorkbook.save("YOUR_DIRECTORY/pivot_only_copy.xlsx");
```

Mã này trả lời **how to copy pivot** bằng cách sao chép chỉ đối tượng pivot, không phải toàn bộ worksheet. Phương thức `addCopy` trên collection `PivotTables` đảm bảo pivot cache được sao chép, đáp ứng yêu cầu **how to preserve pivot**.

## Cách giữ pivot khi tạo workbook từ một sheet

Đôi khi bạn bắt đầu với một sheet không thuộc về bất kỳ workbook nào (ví dụ, bạn tạo sheet trong bộ nhớ). Để **create workbook from sheet** trong khi giữ pivot, hãy thực hiện các bước sau:

```java
// Create a worksheet in memory
Worksheet tempSheet = new Worksheet();
PivotTable pivot = tempSheet.getPivotTables().add("A1", "B10", "MyPivot");

// Configure the pivot source range, rows, columns, data fields, etc.
// (Omitted for brevity – see Aspose.Cells docs for detailed setup)

// Wrap the worksheet in a new workbook
Workbook newWorkbook = new Workbook();
newWorkbook.getWorksheets().addCopy(tempSheet);
newWorkbook.save("YOUR_DIRECTORY/created_from_sheet.xlsx");
```

Bằng cách thêm worksheet vào một `Workbook` mới sau khi pivot đã được định nghĩa đầy đủ, bạn đảm bảo rằng **how to preserve pivot** hoạt động ngay cả khi worksheet được tạo ra bên ngoài một tệp hiện có.

## Mẹo thực tế và những lỗi thường gặp

| Mẹo | Tại sao quan trọng |
|-----|--------------------|
| Use `addCopy` instead of `copy` | `addCopy` clones the underlying pivot cache; a plain `copy` may lose the connection to the data source. |
| Keep source and destination files on the same file system | Relative paths in the pivot’s data source resolve correctly, reducing “source not found” errors. |
| Verify the pivot’s cache after copying | Call `pivot.refresh()` if the source data changed between the copy and the save operation. |
| Dispose of workbooks when done | `sourceWorkbook.dispose();` frees native resources, which is important for large files. |

## Các trường hợp đặc biệt bạn có thể gặp

* **Multiple worksheets with inter‑dependent pivots** – Sao chép từng worksheet riêng lẻ; các cache được chia sẻ sẽ tự động được sao chép, nhưng bạn có thể cần gán lại các kết nối dữ liệu bên ngoài.  
* **Pivot tables based on external SQL queries** – Đảm bảo môi trường đích có thể truy cập cùng một cơ sở dữ liệu; nếu không pivot sẽ hiển thị lỗi “#REF!”.  
* **Large workbooks (>100 MB)** – Sử dụng `WorkbookSettings.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` để giảm áp lực bộ nhớ trong quá trình sao chép.

## Ví dụ đầy đủ, có thể chạy

Dưới đây là chương trình đầy đủ tích hợp tất cả các bước đã thảo luận. Lưu lại dưới tên `CopyPivotTable.java`, điều chỉnh các đường dẫn tệp, và chạy bằng IDE ưa thích hoặc qua `javac`/`java`.



## Bạn nên học gì tiếp theo?

Các hướng dẫn sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh, có thể chạy, kèm theo giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Cách tạo bảng Pivot trong Excel bằng Aspose.Cells cho Java: Hướng dẫn toàn diện](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [Cách cập nhật nguồn dữ liệu của bảng Pivot trong Excel bằng Aspose.Cells cho Java: Hướng dẫn toàn diện](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Cách triển khai Slicers trong bảng Pivot bằng Aspose.Cells cho Java: Hướng dẫn toàn diện](/cells/english/java/data-analysis/implement-slicers-pivot-tables-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}