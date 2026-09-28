---
category: general
date: 2026-09-11
description: Tạo worksheet mới và sao chép phạm vi Excel bằng Aspose.Cells. Tìm hiểu
  cách sao chép phạm vi giữa các sheet mà vẫn giữ nguyên các bảng pivot.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create new worksheet
- copy excel range
- copy range between sheets
- copy range aspose.cells
language: vi
lastmod: 2026-09-11
og_description: Tạo bảng tính mới và sao chép phạm vi Excel bằng Aspose.Cells. Hướng
  dẫn này trình bày các bước chính xác để sao chép phạm vi giữa các sheet và giữ nguyên
  các bảng pivot.
og_image_alt: Screenshot of a Java IDE showing code that creates a new worksheet and
  copies an Excel range
og_title: Tạo trang tính mới và sao chép phạm vi Excel – Hướng dẫn Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-09-11'
  description: Create new worksheet and copy Excel range using Aspose.Cells. Learn
    how to copy range between sheets while preserving pivot tables.
  headline: Create new worksheet and copy Excel range with Aspose.Cells
  type: TechArticle
- questions:
  - answer: The `copy` method also copies merge information, so merged cells appear
      unchanged on the destination sheet.
    question: What if the source range contains merged cells?
  - answer: Yes. Load a second `Workbook` instance, create a destination range in
      that workbook, and call `sourceRange.copy(destinationRange)`. The method handles
      cross‑workbook copying automatically.
    question: Can I copy to a different workbook?
  - answer: The copy operation overwrites any existing cells that intersect the destination
      range. To avoid data loss, ensure the destination area is empty or use a different
      start cell (e.g., `"B2"`).
    question: What if the destination sheet already has data?
  - answer: Aspose.Cells reuses the original pivot cache, which means the new pivot
      table remains linked to the same source data. If you need an independent cache,
      you must recreate the pivot table after copying.
    question: Is the pivot cache duplicated?
  type: FAQPage
tags:
- Aspose.Cells
- Excel automation
- Java
title: Tạo bảng tính mới và sao chép phạm vi Excel bằng Aspose.Cells
url: /vi/java/range-management/create-new-worksheet-and-copy-excel-range-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo worksheet mới và sao chép vùng Excel bằng Aspose.Cells

Nếu bạn cần **tạo worksheet mới** và di chuyển dữ liệu trong một tệp Excel, Aspose.Cells giúp thực hiện một cách đơn giản. Hướng dẫn này chỉ ra cách sao chép một vùng Excel từ sheet này sang sheet khác đồng thời giữ nguyên các pivot table có trong vùng.

Bạn sẽ học cách **sao chép vùng excel**, cách **sao chép vùng giữa các sheet**, và lý do tại sao phương thức `copy` của Aspose.Cells giữ nguyên định nghĩa pivot table. Không cần công cụ bên ngoài—chỉ cần một dự án Java có thư viện Aspose.Cells.

## Yêu cầu trước

Trước khi bắt đầu, hãy chắc chắn rằng bạn đã có:

- Java 17 hoặc mới hơn được cài đặt
- Aspose.Cells for Java (phiên bản 23.12 trở lên) đã được thêm vào classpath của dự án
- Một workbook nguồn (`input.xlsx`) chứa pivot table trong vùng bạn muốn sao chép
- Kiến thức cơ bản về cú pháp Java và quản lý phụ thuộc Maven/Gradle

## Bước 1: Thiết lập dự án và nhập Aspose.Cells

Tạo một dự án Maven đơn giản (hoặc Gradle, nếu bạn thích) và thêm phụ thuộc Aspose.Cells:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>
</dependency>
```

Sau đó nhập các lớp cần thiết trong file nguồn Java của bạn:

```java
import com.aspose.cells.*;
import java.io.IOException;
```

*Lý do bước này quan trọng*: Việc nhập đúng các lớp cho phép bạn truy cập `Workbook`, `Worksheet`, `Range` và phương thức `copy` sẽ thực hiện việc chuyển vùng.

## Bước 2: Tải workbook nguồn

Mở workbook chứa dữ liệu bạn muốn sao chép. Đoạn mã sau tải `input.xlsx` từ thư mục bạn chỉ định:

```java
public class ExcelRangeCopy {
    public static void main(String[] args) throws IOException {
        // Load the source workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

*Giải thích*: `Workbook` đại diện cho toàn bộ tệp Excel. Khi tải một lần, bạn có quyền đọc/ghi trên mọi sheet và tập hợp ô.

## Bước 3: Xác định vùng nguồn có chứa pivot table

Chọn worksheet chứa pivot table và xác định khối ô chính xác mà bạn muốn sao chép. Trong ví dụ này chúng ta sao chép các ô A1 tới D20:

```java
        // Get the first worksheet (index 0) that contains the pivot table
        Worksheet sourceSheet = workbook.getWorksheets().get(0);

        // Define the source range – this range includes the pivot table
        Range sourceRange = sourceSheet.getCells().createRange("A1:D20");
```

*Lý do điều này quan trọng*: Bằng cách tạo một đối tượng `Range`, bạn nói với Aspose.Cells chính xác những ô (kèm theo các đối tượng nhúng như pivot table) cần được nhân bản.

## Bước 4: **Tạo worksheet mới** sẽ nhận dữ liệu đã sao chép

Bây giờ chúng ta thêm một sheet mới vào cùng workbook. Đây là điểm mà từ khóa chính xuất hiện:

```java
        // Create a new worksheet named "Copy"
        Worksheet destinationSheet = workbook.getWorksheets().add("Copy");

        // Define the top‑left cell of the destination range
        Range destinationRange = destinationSheet.getCells().createRange("A1");
```

*Giải thích*: Thêm một sheet mới giúp cô lập dữ liệu đã sao chép, dễ dàng kiểm tra rằng thao tác **copy excel range** đã thành công mà không ảnh hưởng đến sheet gốc.

## Bước 5: Sao chép vùng – pivot table được giữ tự động

Sử dụng phương thức `copy` để di chuyển vùng từ sheet nguồn sang sheet đích. Aspose.Cells sao chép công thức, định dạng và định nghĩa pivot‑table:

```java
        // Copy the range – the pivot table inside the range is preserved
        sourceRange.copy(destinationRange);
```

*Lý do cách này hoạt động*: Phương thức `copy` thực hiện sao chép sâu (deep copy) các ô nguồn. Nó không chỉ sao chép giá trị mà còn sao chép toàn bộ cấu trúc ô, bao gồm cả pivot cache. Vì vậy bạn có thể **copy range aspose.cells** và vẫn thấy một pivot table hoạt động trên sheet mới.

## Bước 6: Lưu workbook với worksheet mới

Cuối cùng, ghi workbook đã chỉnh sửa ra đĩa:

```java
        // Save the workbook with the copied data
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

*Kết quả*: `output.xlsx` bây giờ chứa sheet gốc cộng với một sheet mới có tên **Copy** chứa đúng cùng một vùng, bao gồm cả pivot table.

## Ví dụ hoàn chỉnh

Kết hợp tất cả các phần lại, đây là chương trình đầy đủ, có thể chạy được:

```java
import com.aspose.cells.*;
import java.io.IOException;

public class ExcelRangeCopy {
    public static void main(String[] args) throws IOException {
        // Step 1: Load the source workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Step 2: Get the worksheet that contains the pivot table and define the source range
        Worksheet sourceSheet = workbook.getWorksheets().get(0);
        Range sourceRange = sourceSheet.getCells().createRange("A1:D20");

        // Step 3: Create a new worksheet that will receive the copied range
        Worksheet destinationSheet = workbook.getWorksheets().add("Copy");
        Range destinationRange = destinationSheet.getCells().createRange("A1");

        // Step 4: Copy the range – the pivot table inside the range is preserved
        sourceRange.copy(destinationRange);

        // Step 5: Save the workbook with the copied data
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

**Kết quả mong đợi**: Mở `output.xlsx` trong Excel. Bạn sẽ thấy một sheet tên **Copy** với các ô A1:D20 chứa cùng dữ liệu, định dạng và một pivot table hoạt động giống như bản gốc.

## Các câu hỏi thường gặp và trường hợp đặc biệt

- **Nếu vùng nguồn chứa các ô đã gộp thì sao?**  
  Phương thức `copy` cũng sao chép thông tin gộp, vì vậy các ô đã gộp sẽ xuất hiện không thay đổi trên sheet đích.

- **Có thể sao chép sang một workbook khác không?**  
  Có. Tải một instance `Workbook` thứ hai, tạo một vùng đích trong workbook đó và gọi `sourceRange.copy(destinationRange)`. Phương thức tự động xử lý việc sao chép giữa các workbook.

- **Nếu sheet đích đã có dữ liệu thì sao?**  
  Thao tác sao chép sẽ ghi đè lên bất kỳ ô nào giao nhau với vùng đích. Để tránh mất dữ liệu, hãy đảm bảo khu vực đích trống hoặc sử dụng ô bắt đầu khác (ví dụ: `"B2"`).

- **Pivot cache có được nhân bản không?**  
  Aspose.Cells tái sử dụng pivot cache gốc, nghĩa là pivot table mới vẫn liên kết với cùng nguồn dữ liệu. Nếu bạn cần một cache độc lập, phải tạo lại pivot table sau khi sao chép.

## Mẹo và thực tiễn tốt

- **Mẹo chuyên nghiệp**: Sử dụng `Workbook.setForceFormulaRecalculation(true)` trước khi lưu nếu vùng của bạn chứa công thức phụ thuộc vào dữ liệu bên ngoài khối đã sao chép.
- **Cảnh báo** với các vùng lớn: sao chép các sheet khổng lồ có thể tiêu tốn nhiều bộ nhớ. Hãy cân nhắc sao chép theo các phần nhỏ hơn nếu gặp `OutOfMemoryError`.
- **Mẹo hiệu năng**: Tắt cập nhật màn hình (`workbook.getSettings().setCalculateFormulaOnOpen(false)`) khi làm việc với tệp rất lớn để tăng tốc quá trình sao chép.

## Kết luận

Bây giờ bạn đã biết cách **tạo worksheet mới** và **sao chép vùng excel** giữa các sheet bằng Aspose.Cells, giữ nguyên pivot table và mọi thuộc tính ô. Kỹ thuật này cho phép bạn sao chép khối dữ liệu một cách tự động, xây dựng mẫu báo cáo, hoặc tái cấu trúc workbook mà không cần sao chép‑dán thủ công.

Tiếp theo, khám phá các chủ đề liên quan như **copy range aspose.cells** cho các thao tác giữa các workbook, tự động làm mới pivot‑table, hoặc xuất sheet đã sao chép ra PDF. Thử nghiệm với các vùng nguồn và tên sheet khác nhau để phù hợp với kịch bản tự động hoá của bạn. Chúc lập trình vui vẻ!

## Bạn Nên Học Gì Tiếp Theo?

Các hướng dẫn sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật đã trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh với giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Copy Shapes Between Excel Sheets Using Aspose.Cells for .NET&#58; A Complete Guide](/cells/english/net/images-shapes/copy-shapes-between-sheets-aspose-cells-dotnet/)
- [Copy Images Between Sheets in Excel Using Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/images-shapes/copy-images-between-sheets-excel-aspose-cells-java/)
- [Excel Aspose Cells Dotnet Copy Range Data](/cells/hindi/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}