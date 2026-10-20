---
category: general
date: 2026-10-07
description: Tìm hiểu cách sao chép bảng tổng hợp trong Excel bằng Java và Aspose.Cells.
  Sao chép một bảng tổng hợp bằng cách sao chép phạm vi của nó giữa các workbook một
  cách nhanh chóng.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to duplicate pivot
- copy pivot table
- copy excel range
- copy range between workbooks
- how to copy pivot table
language: vi
lastmod: 2026-10-07
og_description: Cách sao chép bảng tổng hợp trong Excel bằng Java và Aspose.Cells.
  Hãy làm theo hướng dẫn này để sao chép một bảng tổng hợp bằng cách sao chép phạm
  vi của nó giữa các workbook.
og_image_alt: Illustration of copying an Excel pivot table from one workbook to another
og_title: Cách sao chép bảng tổng hợp trong Excel bằng Java – hướng dẫn đầy đủ
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Learn how to duplicate pivot tables in Excel using Java and Aspose.Cells.
    Copy a pivot table by copying its range between workbooks quickly.
  headline: How to duplicate pivot tables in Excel with Java – step‑by‑step guide
  type: TechArticle
- description: Learn how to duplicate pivot tables in Excel using Java and Aspose.Cells.
    Copy a pivot table by copying its range between workbooks quickly.
  name: How to duplicate pivot tables in Excel with Java – step‑by‑step guide
  steps:
  - name: Explanation of each step
    text: '| Step | What the code does | Why it matters for **copy pivot table** |
      |------|-------------------|----------------------------------------| | **1️⃣
      Load source workbook** | `new Workbook(srcPath)` reads `Source.xlsx`. | The
      source file is the only place where the original pivot exists. | | **2️⃣ D'
  - name: 1️⃣ Copying a pivot that spans multiple sheets
    text: 'If the pivot’s source data lives on a different sheet than the pivot itself,
      include both sheets in the copy operation. The simplest approach is to copy
      the entire source sheet first, then copy the pivot sheet:'
  - name: 2️⃣ Dealing with named ranges
    text: 'Aspose.Cells preserves named ranges when you copy a range. However, if
      the destination workbook already contains a name with the same identifier, a
      `CellsException` is thrown. Resolve this by renaming the conflicting name before
      the copy:'
  - name: 3️⃣ Large workbooks and performance
    text: 'Copying very large ranges (hundreds of thousands of rows) can be memory‑intensive.
      Enable **memory optimization**:'
  - name: 4️⃣ Keeping formulas intact
    text: If the source range contains formulas that reference cells outside the copied
      area, those references become broken after the copy. To avoid this, expand the
      range to include all dependent cells, or use `copyRange` with the `CopyOptions`
      flag `CopyOptions.COPY_FORMULA`.
  type: HowTo
tags:
- Excel
- Java
- Aspose.Cells
- PivotTable
- Data manipulation
title: Cách sao chép bảng tổng hợp trong Excel bằng Java – hướng dẫn từng bước
url: /vi/java/excel-pivot-tables/how-to-duplicate-pivot-tables-in-excel-with-java-step-by-ste/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách sao chép bảng tổng hợp (pivot) trong Excel bằng Java – hướng dẫn chi tiết

Nếu bạn cần **cách sao chép bảng tổng hợp** trong một workbook Excel, hướng dẫn này sẽ cung cấp cho bạn một giải pháp hoàn chỉnh, sẵn sàng chạy. Sử dụng Aspose.Cells cho Java, bạn có thể sao chép một bảng tổng hợp cùng với dữ liệu nguồn bằng cách sao chép phạm vi (range) nền tảng, sau đó lưu kết quả thành một workbook mới.

Việc sao chép bảng tổng hợp thường cảm thấy khó khăn vì bộ nhớ đệm (pivot cache) được ẩn bên trong sheet. Bằng cách sao chép toàn bộ phạm vi chứa bảng tổng hợp, Aspose.Cells tự động tái tạo bộ nhớ đệm trong workbook đích, vì vậy bạn nhận được một bản sao hoạt động đầy đủ mà không cần can thiệp XML thủ công.

Trong hướng dẫn này bạn sẽ:

* Tải workbook nguồn có chứa bảng tổng hợp.  
* Xác định phạm vi chính xác chứa bảng tổng hợp.  
* Sao chép phạm vi đó vào một workbook mới, giữ nguyên định nghĩa của bảng tổng hợp.  
* Lưu file mới và xác minh rằng bảng tổng hợp hoạt động bình thường.  

Các bước này áp dụng cho bất kỳ phiên bản Excel nào được Aspose.Cells hỗ trợ (2007‑2024) và chỉ yêu cầu vài dòng mã Java.

## Yêu cầu trước

| Yêu cầu | Lý do quan trọng |
|-------------|----------------|
| **Java 8 hoặc mới hơn** | Aspose.Cells được xây dựng cho Java 8+. |
| **Aspose.Cells for Java** (phiên bản mới nhất) | Cung cấp các API `Workbook`, `Range` và `CopyRange` được sử dụng trong ví dụ. |
| **Workbook nguồn** có bảng tổng hợp (ví dụ: `Source.xlsx`) | Bảng tổng hợp bạn muốn sao chép. |
| **Quyền ghi** vào thư mục đích | Cần để lưu `CopyWithPivot.xlsx`. |

Thêm phụ thuộc Aspose.Cells Maven vào file `pom.xml` của bạn (hoặc tải JAR thủ công):

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>   <!-- use the latest stable version -->
</dependency>
```

## Cách sao chép bảng tổng hợp – triển khai đầy đủ

Dưới đây là một chương trình Java tự chứa, minh họa **cách sao chép bảng tổng hợp** bằng cách sao chép phạm vi chứa bảng tổng hợp. Mã nguồn bao gồm xử lý lỗi, chú thích và bước xác minh.

```java
// File: DuplicatePivot.java
import com.aspose.cells.*;

public class DuplicatePivot {
    public static void main(String[] args) {
        // 1️⃣ Load the source workbook that holds the pivot table.
        String srcPath = "YOUR_DIRECTORY/Source.xlsx";
        Workbook srcWb;
        try {
            srcWb = new Workbook(srcPath);
        } catch (Exception e) {
            System.err.println("Failed to load source workbook: " + e.getMessage());
            return;
        }

        // 2️⃣ Identify the range that encloses the pivot table.
        // Adjust the sheet index (0‑based) and address as needed.
        Worksheet srcSheet = srcWb.getWorksheets().get(0);
        // Example address "A1:G20" – includes the pivot and its data source.
        String pivotRangeAddress = "A1:G20";
        Range srcRange = srcSheet.getCells().createRange(pivotRangeAddress);

        // 3️⃣ Create a destination workbook and copy the identified range.
        Workbook destWb = new Workbook(); // starts with a blank workbook
        Worksheet destSheet = destWb.getWorksheets().get(0);
        try {
            // copyRange copies both values and the internal pivot cache.
            destSheet.getCells().copyRange(srcRange, "A1");
        } catch (Exception e) {
            System.err.println("Failed to copy range: " + e.getMessage());
            return;
        }

        // 4️⃣ (Optional) Refresh the pivot so it reflects the copied data.
        // Aspose.Cells automatically rebuilds the cache, but calling refresh
        // guarantees up‑to‑date results if the source data has changed.
        for (int i = 0; i < destSheet.getPivotTables().getCount(); i++) {
            destSheet.getPivotTables().get(i).refresh();
        }

        // 5️⃣ Save the new workbook that now contains the duplicated pivot.
        String destPath = "YOUR_DIRECTORY/CopyWithPivot.xlsx";
        try {
            destWb.save(destPath);
            System.out.println("Pivot table duplicated successfully to: " + destPath);
        } catch (Exception e) {
            System.err.println("Failed to save destination workbook: " + e.getMessage());
        }
    }
}
```

### Giải thích từng bước

| Bước | Mã thực hiện | Tại sao quan trọng đối với **sao chép bảng tổng hợp** |
|------|-------------------|----------------------------------------|
| **1️⃣ Tải workbook nguồn** | `new Workbook(srcPath)` đọc `Source.xlsx`. | File nguồn là nơi duy nhất chứa bảng tổng hợp gốc. |
| **2️⃣ Xác định phạm vi** | `createRange("A1:G20")` tạo đối tượng `Range` bao phủ bảng tổng hợp và dữ liệu của nó. | Bảng tổng hợp được lưu cùng với bộ nhớ đệm; sao chép toàn bộ phạm vi đảm bảo bộ nhớ đệm cũng được chuyển. |
| **3️⃣ Sao chép phạm vi** | `copyRange(srcRange, "A1")` ghi phạm vi vào sheet đích. | Đây là lõi của **sao chép phạm vi giữa các workbook** – API tự động xử lý các đối tượng ẩn. |
| **4️⃣ Làm mới bảng tổng hợp** | `pivotTable.refresh()` buộc bảng tổng hợp tính lại. | Đảm bảo bảng tổng hợp sao chép hiển thị cùng giá trị như bản gốc, đặc biệt sau khi có thay đổi. |
| **5️⃣ Lưu workbook** | `destWb.save(destPath)` ghi file ra đĩa. | Tạo ra kết quả cuối cùng **sao chép phạm vi Excel** mà bạn có thể mở trong Excel. |

#### Kết quả mong đợi

Sau khi chạy chương trình, mở `CopyWithPivot.xlsx`. Bạn sẽ thấy một worksheet trông giống hệt sheet nguồn, và bảng tổng hợp hoạt động đúng như bản gốc – bạn có thể mở rộng hàng, lọc trường và làm mới dữ liệu mà không gặp lỗi.

## Các biến thể phổ biến và trường hợp đặc biệt

### 1️⃣ Sao chép bảng tổng hợp trải rộng trên nhiều sheet

Nếu dữ liệu nguồn của bảng tổng hợp nằm trên một sheet khác với chính bảng tổng hợp, hãy bao gồm cả hai sheet trong thao tác sao chép. Cách đơn giản nhất là sao chép toàn bộ sheet nguồn trước, sau đó sao chép sheet chứa bảng tổng hợp:

```java
// Copy source data sheet
Workbook temp = new Workbook(); // temporary workbook for the data sheet
temp.getWorksheets().addCopy(srcWb.getWorksheets().get(0));
Workbook dest = new Workbook();
dest.getWorksheets().addCopy(temp.getWorksheets().get(0));

// Then copy the pivot sheet as shown earlier
```

### 2️⃣ Xử lý các phạm vi có tên (named ranges)

Aspose.Cells giữ lại các named range khi bạn sao chép một phạm vi. Tuy nhiên, nếu workbook đích đã chứa một tên trùng với identifier, sẽ ném ra `CellsException`. Giải quyết bằng cách đổi tên đối tượng gây xung đột trước khi sao chép:

```java
if (destWb.getWorksheets().get(0).getNames().containsKey("MyRange")) {
    destWb.getWorksheets().get(0).getNames().remove("MyRange");
}
```

### 3️⃣ Workbook lớn và hiệu năng

Sao chép các phạm vi rất lớn (hàng chục ngàn) có thể tốn nhiều bộ nhớ. Kích hoạt **tối ưu hóa bộ nhớ**:

```java
LoadOptions loadOptions = new LoadOptions(LoadFormat.XLSX);
loadOptions.setMemorySetting(MemorySetting.MEMORY_PREFERENCE);
Workbook largeSrc = new Workbook(srcPath, loadOptions);
```

### 4️⃣ Giữ công thức nguyên vẹn

Nếu phạm vi nguồn chứa công thức tham chiếu tới các ô ngoài vùng đã sao chép, các tham chiếu đó sẽ bị phá vỡ sau khi sao chép. Để tránh, mở rộng phạm vi để bao gồm tất cả các ô phụ thuộc, hoặc sử dụng `copyRange` với cờ `CopyOptions` là `CopyOptions.COPY_FORMULA`.

```java
CopyOptions options = new CopyOptions();
options.setCopyFormula(true);
destSheet.getCells().copyRange(srcRange, "A1", options);
```

## Mẹo chuyên nghiệp để **sao chép phạm vi giữa các workbook** một cách đáng tin cậy

* **Luôn sử dụng địa chỉ tuyệt đối** (`$A$1:$G$20`) khi sheet nguồn có thể được đổi tên.  
* **Làm mới sau khi sao chép** – mặc dù Aspose.Cells tự xây dựng lại cache, việc gọi `refresh()` loại bỏ các cảnh báo cache lỗi thời trong Excel.  
* **Xác thực bảng tổng hợp**: sau khi lưu, mở file bằng chương trình và gọi `pivotTable.validate()` để chắc chắn không có tham chiếu bị hỏng.  
* **Tương thích phiên bản**: mã hoạt động với các file Excel 2007‑2024 (`.xlsx`, `.xlsm`). Đối với file `.xls` cũ, đặt `LoadOptions.setLoadFormat(LoadFormat.XLS)`.

## Danh sách mã nguồn đầy đủ (sẵn sàng biên dịch)



## Bạn nên học gì tiếp theo?

Các hướng dẫn sau đây đề cập đến các chủ đề liên quan chặt chẽ, mở rộng các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh với giải thích chi tiết từng bước, giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [How to Copy Pivot Table in Java – Complete Aspose.Cells Guide](/cells/english/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-complete-aspose-cells-guide/)
- [How to Create Pivot Tables in Excel Using Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [How to Update Excel Pivot Table Source with Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}