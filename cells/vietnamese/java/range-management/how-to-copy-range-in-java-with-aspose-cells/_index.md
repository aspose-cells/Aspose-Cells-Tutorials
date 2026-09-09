---
category: general
date: 2026-09-08
description: Cách sao chép phạm vi trong Java bằng Aspose.Cells – học cách sao chép
  bảng pivot, tạo bản sao bảng pivot và xuất bảng pivot trong khi giữ nguyên định
  dạng.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy range
- copy pivot table
- duplicate pivot table
- export pivot table
- copy range with formatting
language: vi
lastmod: 2026-09-08
og_description: Cách sao chép phạm vi trong Java với Aspose.Cells. Hướng dẫn này chỉ
  cho bạn cách sao chép bảng tổng hợp, tạo bản sao bảng tổng hợp và xuất bảng tổng
  hợp trong khi giữ nguyên định dạng.
og_image_alt: Screenshot of Java code copying a pivot table range in Aspose.Cells
og_title: Cách sao chép phạm vi trong Java – hướng dẫn đầy đủ Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-09-08'
  description: How to copy range in Java using Aspose.Cells – learn to copy pivot
    table, duplicate pivot table, and export pivot table while preserving formatting.
  headline: How to copy range in Java with Aspose.Cells
  type: TechArticle
- description: How to copy range in Java using Aspose.Cells – learn to copy pivot
    table, duplicate pivot table, and export pivot table while preserving formatting.
  name: How to copy range in Java with Aspose.Cells
  steps:
  - name: Copy pivot table to an existing workbook
    text: 'If you need to **duplicate pivot table** inside a workbook that already
      has data, use the same `copyRange` call but point to a different destination
      address:'
  - name: Export pivot table only (without surrounding data)
    text: 'Sometimes you want just the pivot table, not the source data. Identify
      the pivot table’s display range via its `getPivotTable` method:'
  - name: Preserve conditional formatting
    text: 'Conditional formatting rules are part of the style collection. The `PasteType.ALL`
      flag already copies them, but you can be explicit:'
  - name: Edge cases and troubleshooting
    text: '| Situation | What to watch for | Recommended fix | |-----------|-------------------|-----------------|
      | Source and destination workbooks use different Excel versions | Some newer
      pivot features (e.g., data model) may not render correctly | Use the latest
      Aspose.Cells version and set `Workbook.setF'
  - name: Next steps
    text: '- Explore **copy range with formatting** for charts and images (use `PasteType.PICTURES`).
      - Automate batch processing: loop over multiple source files and consolidate
      their pivot tables into a summary workbook. - Combine this technique with Aspose.Slides
      to generate PowerPoint reports that embed th'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Cách sao chép phạm vi trong Java với Aspose.Cells
url: /vi/java/range-management/how-to-copy-range-in-java-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách sao chép phạm vi trong Java với Aspose.Cells

Nếu bạn cần **cách sao chép phạm vi** trong Java, Aspose.Cells làm cho công việc trở nên đơn giản. Cho dù bạn đang di chuyển một khối ô thông thường hay một bảng tổng hợp đầy đủ tính năng, thư viện sẽ xử lý thao tác sao chép đồng thời giữ nguyên công thức, kiểu dáng và bộ nhớ đệm pivot. Trong hướng dẫn này, bạn sẽ học cách **sao chép bảng tổng hợp**, **nhân bản bảng tổng hợp**, và thậm chí **xuất bảng tổng hợp** sang một workbook mới với đầy đủ định dạng.

Hướng dẫn bao gồm mọi thứ từ thiết lập dự án đến bước kiểm tra cuối cùng, vì vậy bạn có thể chạy mã ngay sau khi đọc. Không cần công cụ bên ngoài nào ngoài JAR Aspose.Cells cho Java.

## Yêu cầu trước

- Java 17 (hoặc bất kỳ JDK nào được hỗ trợ) đã được cài đặt và cấu hình trong IDE của bạn.
- Maven hoặc Gradle để quản lý phụ thuộc (các ví dụ sử dụng Maven).
- Một tệp Excel nguồn (`source.xlsx`) chứa bảng tổng hợp trong phạm vi `A1:H20`.
- Kiến thức cơ bản về lập trình Java.

## Bước 1: Thêm Aspose.Cells vào dự án của bạn

Aspose.Cells là một thư viện thương mại, nhưng phiên bản đánh giá miễn phí vẫn có sẵn. Thêm phụ thuộc vào `pom.xml` của bạn:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest version -->
</dependency>
```

> **Mẹo chuyên nghiệp:** Nếu bạn thích Gradle, mục tương đương là:
> ```gradle
> implementation 'com.aspose:aspose-cells:24.9'
> ```

Việc thêm JAR sẽ cho phép bạn truy cập các lớp `Workbook`, `Worksheet`, `Range` và `CopyOptions` được sử dụng xuyên suốt trong hướng dẫn này.

## Bước 2: Tải workbook nguồn và chọn worksheet đầu tiên

Phần đầu tiên của **cách sao chép phạm vi** là mở workbook chứa dữ liệu bạn muốn di chuyển.

```java
import com.aspose.cells.*;

public class CopyRangeDemo {
    public static void main(String[] args) throws Exception {
        // Load the source workbook
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
        // Select the first worksheet (index 0)
        Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);
```

> **Tại sao điều này quan trọng:** Mở workbook tạo ra một biểu diễn trong bộ nhớ mà API có thể thao tác mà không chạm tới tệp gốc trên đĩa.

## Bước 3: Xác định phạm vi chứa bảng tổng hợp

Bảng tổng hợp tồn tại trong một khối hình chữ nhật. Bạn phải chỉ định khối đó để Aspose.Cells biết cần sao chép gì.

```java
        // Define the range that holds the pivot table and its source data
        Range sourceRange = sourceSheet.getCells().createRange("A1:H20");
```

> **Lưu ý:** Phương thức `createRange` **không** sao chép bất cứ thứ gì ở thời điểm này; nó chỉ tạo một đối tượng `Range` trỏ tới các ô bạn dự định nhân bản.

## Bước 4: Tạo một workbook mới và lấy worksheet đầu tiên

Bây giờ tạo workbook đích nơi phạm vi đã sao chép sẽ được đặt.

```java
        // Create an empty workbook for the destination
        Workbook destWorkbook = new Workbook();
        // Get its first (and only) worksheet
        Worksheet destSheet = destWorkbook.getWorksheets().get(0);
```

> **Tại sao lại là một workbook mới?** Sử dụng một tệp mới đảm bảo không có kiểu ẩn hoặc named range can thiệp vào thao tác sao chép, điều này đặc biệt quan trọng khi bạn **xuất bảng tổng hợp** sang một tệp riêng.

## Bước 5: Sao chép phạm vi (bao gồm bảng tổng hợp) sang sheet đích

Đây là phần cốt lõi của **cách sao chép phạm vi với định dạng**. Đối tượng `CopyOptions` chỉ định cho Aspose.Cells giữ nguyên mọi thứ: giá trị, công thức, kiểu dáng và bộ nhớ đệm pivot.

```java
        // Prepare copy options – preserve formatting and pivot cache
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setPasteType(PasteType.ALL); // copies everything
        copyOptions.setSkipBlanks(false);        // keep blank cells

        // Copy the defined range to cell A1 of the destination sheet
        destSheet.getCells().copyRange(sourceRange, "A1", copyOptions);
```

> **Sao chép bảng tổng hợp:** Vì phạm vi nguồn bao gồm bảng tổng hợp, API tự động nhân bản bộ nhớ đệm pivot, vì vậy worksheet mới chứa một bảng tổng hợp hoàn toàn hoạt động giống hệt bản gốc.

## Bước 6: Lưu workbook đích

Cuối cùng, ghi kết quả ra đĩa.

```java
        // Save the destination workbook
        destWorkbook.save("YOUR_DIRECTORY/dest.xlsx");
    }
}
```

Khi bạn mở `dest.xlsx`, bạn sẽ thấy một bản sao chính xác của bảng tổng hợp gốc, đầy đủ định dạng, slicer và các trường tính toán.

## Kết quả mong đợi

- `dest.xlsx` chứa một worksheet có tên **Sheet1**.
- Các ô `A1:H20` giữ cùng dữ liệu và bảng tổng hợp như nguồn.
- Tất cả kiểu dáng ô (phông chữ, màu sắc, viền) được giữ nguyên.
- Bảng tổng hợp hoàn toàn tương tác; việc làm mới nó sẽ phản ánh dữ liệu nền trong phạm vi đã sao chép.

## Cách sao chép phạm vi với định dạng – khám phá sâu hơn

Ví dụ trước đây cho thấy kịch bản đơn giản nhất, nhưng bạn có thể gặp các biến thể yêu cầu cách tiếp cận hơi khác.

### Sao chép bảng tổng hợp vào một workbook hiện có

Nếu bạn cần **nhân bản bảng tổng hợp** trong một workbook đã có dữ liệu, hãy sử dụng cùng một lời gọi `copyRange` nhưng chỉ tới một địa chỉ đích khác:

```java
// Assume destWorkbook already contains other sheets
Worksheet targetSheet = destWorkbook.getWorksheets().get(2);
targetSheet.getCells().copyRange(sourceRange, "B5", copyOptions);
```

### Xuất chỉ bảng tổng hợp (không kèm dữ liệu xung quanh)

Đôi khi bạn chỉ muốn bảng tổng hợp, không cần dữ liệu nguồn. Xác định phạm vi hiển thị của bảng tổng hợp qua phương thức `getPivotTable`:

```java
PivotTable pt = sourceSheet.getPivotTables().get(0);
String ptArea = pt.getDisplayRange(); // e.g., "C5:G15"
Range pivotOnly = sourceSheet.getCells().createRange(ptArea);
destSheet.getCells().copyRange(pivotOnly, "A1", copyOptions);
```

### Bảo tồn định dạng có điều kiện

Các quy tắc định dạng có điều kiện là một phần của bộ sưu tập kiểu. Cờ `PasteType.ALL` đã sao chép chúng, nhưng bạn có thể chỉ định rõ ràng:

```java
copyOptions.setPasteType(PasteType.FORMATS);
copyOptions.setPasteType(PasteType.ALL); // overrides previous, ensures everything
```

### Trường hợp đặc biệt và khắc phục sự cố

| Tình huống | Điều cần chú ý | Cách khắc phục đề xuất |
|-----------|-------------------|-----------------|
| Workbook nguồn và đích sử dụng các phiên bản Excel khác nhau | Một số tính năng pivot mới hơn (ví dụ: data model) có thể không hiển thị đúng | Sử dụng phiên bản Aspose.Cells mới nhất và đặt `Workbook.setFileFormatType(FileFormatType.XLSX)` cho cả hai workbook |
| Bảng tổng hợp rất lớn (> 10 000 dòng) gây áp lực bộ nhớ | Lỗi thiếu bộ nhớ trong quá trình sao chép | Bật `Workbook.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` trước khi tải |
| Worksheet đích đã chứa một named range có cùng tên với nguồn | Xung đột tên dẫn đến lỗi `CopyOptions` | Gọi `copyOptions.setIgnoreNameConflicts(true)` |

## Ví dụ đầy đủ, có thể chạy

Dưới đây là chương trình hoàn chỉnh bạn có thể sao chép‑dán vào một lớp Java. Nó bao gồm tất cả các import, xử lý lỗi và chú thích.

```java
import com.aspose.cells.*;

public class CopyRangeDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the source workbook
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
        Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);

        // 2️⃣ Define the range that includes the pivot table
        Range sourceRange = sourceSheet.getCells().createRange("A1:H20");

        // 3️⃣ Create a new destination workbook
        Workbook destWorkbook = new Workbook();
        Worksheet destSheet = destWorkbook.getWorksheets().get(0);

        // 4️⃣ Configure copy options to keep everything (values, formulas, formatting, pivot cache)
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setPasteType(PasteType.ALL);
        copyOptions.setSkipBlanks(false);
        copyOptions.setIgnoreNameConflicts(true); // avoid name collisions

        // 5️⃣ Perform the copy
        destSheet.getCells().copyRange(sourceRange, "A1", copyOptions);

        // 6️⃣ Save the result
        destWorkbook.save("YOUR_DIRECTORY/dest.xlsx");
        System.out.println("Copy completed – dest.xlsx now contains the duplicated pivot table.");
    }
}
```

Chạy chương trình, sau đó mở `dest.xlsx` để xác nhận rằng bảng tổng hợp hoạt động chính xác như bản gốc.

## Kết luận

Bạn giờ đã biết **cách sao chép phạm vi** trong Java bằng Aspose.Cells, bao gồm cách **sao chép bảng tổng hợp**, **nhân bản bảng tổng hợp**, và **xuất bảng tổng hợp** trong khi giữ nguyên mọi định dạng. Thư viện trừu tượng hoá các chi tiết cấp thấp của cấu trúc XML Excel, cho phép bạn tập trung vào logic nghiệp vụ.

### Các bước tiếp theo

- Khám phá **sao chép phạm vi với định dạng** cho biểu đồ và hình ảnh (sử dụng `PasteType.PICTURES`).
- Tự động hoá xử lý hàng loạt: lặp qua nhiều tệp nguồn và hợp nhất các bảng tổng hợp của chúng vào một workbook tổng hợp.
- Kết hợp kỹ thuật này với Aspose.Slides để tạo báo cáo PowerPoint nhúng bảng tổng hợp đã sao chép

## Bạn nên học gì tiếp theo?

Các hướng dẫn sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh với giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Cách Cập Nhật Nguồn Bảng Tổng Hợp Excel với Aspose.Cells cho Java: Hướng Dẫn Toàn Diện](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Tối Ưu Tải Bảng Tổng Hợp trong Java bằng Aspose.Cells – Hướng Dẫn Toàn Diện](/cells/english/java/data-analysis/optimize-pivot-table-loading-aspose-cells-java/)
- [Cách Sao Chép Bảng Tổng Hợp trong C# – Chuyển Excel sang PPTX, Sao Chép Phạm Vi & Tạo Hộp Văn Bản](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}