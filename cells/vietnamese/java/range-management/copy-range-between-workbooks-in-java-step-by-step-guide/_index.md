---
category: general
date: 2026-08-14
description: Sao chép vùng dữ liệu giữa các workbook bằng Java sử dụng Aspose.Cells.
  Học cách sao chép workbook chứa bảng pivot, xuất hình ảnh sang PowerPoint và loại
  bỏ AutoFilter khỏi bảng Excel.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy range between workbooks
- copy pivot table workbook
- export picture to powerpoint
- copy excel range to new workbook
- remove autofilter from excel table
language: vi
lastmod: 2026-08-14
og_description: Sao chép phạm vi giữa các workbook trong Java. Hướng dẫn này chỉ cách
  sao chép workbook bảng pivot, xuất hình ảnh sang PowerPoint và loại bỏ AutoFilter
  khỏi bảng Excel.
og_image_alt: Screenshot of Java code copying range between workbooks with Aspose.Cells
og_title: Sao chép phạm vi giữa các workbook trong Java – hướng dẫn đầy đủ Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: Copy range between workbooks with Java using Aspose.Cells. Learn to
    copy pivot table workbook, export picture to PowerPoint and remove AutoFilter
    from Excel table.
  headline: Copy range between workbooks in Java – step‑by‑step guide
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel automation
- PowerPoint export
title: Sao chép phạm vi giữa các sổ làm việc trong Java – hướng dẫn từng bước
url: /vi/java/range-management/copy-range-between-workbooks-in-java-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Sao chép phạm vi giữa các workbook trong Java – hướng dẫn chi tiết

Nếu bạn cần **sao chép phạm vi giữa các workbook** trong Java, Aspose.Cells cung cấp một API sạch sẽ để xử lý các đối tượng phức tạp như pivot table và hình ảnh. Bài hướng dẫn này cho thấy cách **sao chép workbook chứa pivot table**, **xuất hình ảnh ra PowerPoint**, và **xóa AutoFilter khỏi bảng Excel** đồng thời giữ cho mã dễ đọc và bảo trì.

Bạn sẽ học được cách:

* Tải một workbook nguồn và xác định phạm vi nguồn.  
* Tạo một workbook đích và sao chép phạm vi sao cho pivot table vẫn nguyên vẹn.  
* Xuất hình ảnh đầu tiên trên sheet dưới dạng đối tượng PowerPoint có thể chỉnh sửa.  
* Xóa AutoFilter khỏi bảng Excel đầu tiên.  
* Tải một workbook với `SmartMarkerOptions` để xử lý mảng JSON như một giá trị ô duy nhất.

Ví dụ sử dụng Aspose.Cells 23.10 cho Java, nhưng các khái niệm cũng áp dụng cho các phiên bản trước.

---

## Các yêu cầu trước

| Yêu cầu | Lý do |
|-------------|----------------|
| Java 17 trở lên | Được yêu cầu bởi runtime mới nhất của Aspose.Cells. |
| Aspose.Cells for Java (artifact Maven `com.aspose:aspose-cells`) | Cung cấp các lớp `Workbook`, `Worksheet`, `Range` và các lớp liên quan được sử dụng trong mã. |
| Một file Excel nguồn (`src.xlsx`) chứa pivot table, hình ảnh và bảng có AutoFilter. | Bài hướng dẫn thao tác các đối tượng này để minh họa từng tính năng. |

Thêm dependency Maven vào `pom.xml` của bạn:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

---

## Sao chép phạm vi giữa các workbook – tải nguồn và đích

Bước đầu tiên là mở workbook nguồn, chọn phạm vi chứa dữ liệu cần sao chép, và tạo một workbook đích trống.

```java
import com.aspose.cells.*;

public class CopyRangeDemo {
    public static void main(String[] args) throws Exception {
        // Load the source workbook that holds the pivot table, picture, and table.
        Workbook sourceWb = new Workbook("YOUR_DIRECTORY/src.xlsx");
        Worksheet sourceWs = sourceWb.getWorksheets().get(0);

        // Define the range that includes the pivot table (A1:G20 in this example).
        Range sourceRange = sourceWs.getCells().createRange("A1:G20");

        // Create a new workbook that will receive the copied range.
        Workbook destWb = new Workbook();
        Worksheet destWs = destWb.getWorksheets().get(0);
        Range destRange = destWs.getCells().createRange("A1");
```

> **Tại sao điều này quan trọng:** Khi sử dụng `Range.copy`, Aspose.Cells không chỉ sao chép giá trị ô thô mà còn sao chép cache của pivot, giữ cho pivot table hoạt động trong workbook đích.

---

## Sao chép workbook chứa pivot table khi sao chép phạm vi

Bây giờ sao chép phạm vi đã định nghĩa từ workbook nguồn sang workbook đích. Pivot table được giữ lại tự động vì phạm vi bao gồm cache của pivot.

```java
        // Copy the source range to the destination range.
        destRange.copy(sourceRange);

        // Save the intermediate workbook to verify that the pivot table was copied.
        destWb.save("YOUR_DIRECTORY/destination.xlsx");
```

> **Kết quả:** Mở `destination.xlsx` sẽ hiển thị cùng bố cục pivot table như `src.xlsx`. Không cần mã bổ sung để xây dựng lại pivot cache.

---

## Xuất hình ảnh ra PowerPoint

Aspose.Cells có thể đánh dấu một hình ảnh để xuất ra đối tượng PowerPoint có thể chỉnh sửa. Đoạn mã dưới đây chọn hình ảnh đầu tiên trên sheet đích và đặt cờ xuất.

```java
        // Retrieve the first picture on the destination sheet.
        Shape picture = destWs.getPictures().get(0);

        // Instruct Aspose.Cells to export this picture as a PowerPoint object.
        picture.getPictureFormat().setExportToPptx(true);

        // Optionally, save the workbook as PPTX to see the result.
        destWb.save("YOUR_DIRECTORY/destination.pptx");
```

> **Bạn sẽ thấy:** Mở `destination.pptx` trong PowerPoint sẽ hiển thị hình ảnh dưới dạng shape gốc mà bạn có thể chỉnh sửa, thay đổi kích thước hoặc tạo hoạt ảnh.

---

## Xóa AutoFilter khỏi bảng Excel

Nếu sheet nguồn chứa bảng có AutoFilter, bạn có thể muốn xóa nó sau khi sao chép. Mã dưới đây truy cập bảng đầu tiên và loại bỏ bộ lọc.

```java
        // Access the first table on the destination sheet.
        Table table = destWs.getTables().get(0);

        // Remove the AutoFilter by assigning null.
        table.setAutoFilter(null);

        // Save the final workbook.
        destWb.save("YOUR_DIRECTORY/final_output.xlsx");
```

> **Hiệu quả:** Bảng vẫn tồn tại trong workbook, nhưng các mũi tên lọc thả xuống biến mất, cho bạn một chế độ xem dữ liệu sạch sẽ.

---

## Tải workbook với tùy chọn SmartMarker – xử lý mảng JSON như một ô duy nhất

Khi tạo báo cáo từ JSON, Aspose.Cells có thể xem toàn bộ mảng như một giá trị ô duy nhất. Điều này hữu ích khi nhúng chuỗi JSON vào mẫu mà không cần mở rộng thành nhiều ô.

```java
        // Configure LoadOptions to enable SmartMarker array handling.
        LoadOptions loadOptions = new LoadOptions();
        SmartMarkerOptions smOptions = new SmartMarkerOptions();
        smOptions.setArrayAsSingle(true);
        loadOptions.setSmartMarkerOptions(smOptions);

        // Load a template workbook using the configured options.
        Workbook smartMarkerWb = new Workbook("YOUR_DIRECTORY/template.xlsx", loadOptions);

        // Continue processing (e.g., populate markers) as needed.
        // ...

        // Save the processed workbook.
        smartMarkerWb.save("YOUR_DIRECTORY/template_filled.xlsx");
    }
}
```

> **Lý do bạn có thể dùng:** Nếu payload JSON của bạn chứa một mảng cần hiển thị dưới dạng chuỗi JSON trong một ô duy nhất, `setArrayAsSingle(true)` sẽ ngăn Aspose.Cells mở rộng mảng thành các hàng hoặc cột riêng biệt.

---

![Copy range between workbooks in Java – Aspose.Cells code example](copy-range-workbooks.png)

*Văn bản thay thế hình ảnh:* **Sao chép phạm vi giữa các workbook trong Java – ví dụ mã Aspose.Cells** (khớp với từ khóa chính).

---

## Đầu ra dự kiến

| Tên file                | Nội dung |
|--------------------------|----------|
| `destination.xlsx`       | Phạm vi đã sao chép với pivot table hoạt động. |
| `destination.pptx`       | Hình ảnh đã xuất dưới dạng shape PowerPoint có thể chỉnh sửa. |
| `final_output.xlsx`      | Bảng không có mũi tên AutoFilter. |
| `template_filled.xlsx`   | Mảng JSON được lưu dưới dạng giá trị ô duy nhất. |

Mở mỗi file trong ứng dụng tương ứng (Excel hoặc PowerPoint) để xác nhận các thao tác đã thành công.

---

## Kết luận

Bạn đã biết cách **sao chép phạm vi giữa các workbook** trong Java bằng Aspose.Cells, đồng thời giữ pivot table, xuất hình ảnh ra PowerPoint và xóa AutoFilter khỏi bảng Excel. Mẫu này có thể mở rộng để sao chép bất kỳ phạm vi Excel nào sang workbook mới, xử lý mảng JSON với SmartMarker, hoặc chuỗi các biến đổi bổ sung.

Các bước tiếp theo bạn có thể khám phá:

* **Sao chép phạm vi Excel sang workbook mới** với nhiều worksheet.  
* Sử dụng **xuất hình ảnh ra PowerPoint** để trích xuất hàng loạt hình ảnh.  
* Áp dụng **xóa autofilter khỏi bảng excel** trong các pipeline báo cáo lớn hơn.  
* Kết hợp các kỹ thuật này với Aspose.Slides để tự động hoá toàn bộ quy trình Excel‑to‑PowerPoint.

Hãy thoải mái thử nghiệm với các địa chỉ phạm vi khác nhau, nhiều pivot table, hoặc định dạng hình ảnh tùy chỉnh. API Aspose.Cells được thiết kế để linh hoạt lập trình, vì vậy bạn có thể điều chỉnh các mẫu đã trình bày để phù hợp với bất kỳ kịch bản tự động hoá Excel doanh nghiệp nào.

## Bạn Nên Học Gì Tiếp Theo?


Các hướng dẫn sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật đã được trình bày trong bài viết này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh với giải thích chi tiết từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Copy Images Between Sheets in Excel Using Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/images-shapes/copy-images-between-sheets-excel-aspose-cells-java/)
- [Copy Page Setup Settings Between Worksheets in Excel Using Aspose.Cells Java](/cells/english/java/headers-footers/copy-page-setup-excel-aspose-cells-java/)
- [Excel Copy Worksheets Between Workbooks](/cells/english/net/excel-copy-worksheet/excel-copy-worksheets-between-workbooks/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}