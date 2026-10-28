---
category: general
date: 2026-09-05
description: Tìm hiểu cách sao chép phạm vi trong Excel, xuất Excel sang PowerPoint
  và chuyển đổi Excel sang pptx với một ví dụ Java đầy đủ.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy range
- export excel to powerpoint
- convert excel to pptx
- copy pivot table sheet
- how to export excel
language: vi
lastmod: 2026-09-05
og_description: Cách sao chép phạm vi và xuất Excel sang PowerPoint bằng Java. Hãy
  làm theo hướng dẫn từng bước này để chuyển đổi Excel sang PPTX một cách hiệu quả.
og_image_alt: Screenshot showing how to copy range from Excel to PowerPoint in a Java
  IDE
og_title: Cách sao chép vùng dữ liệu từ Excel và xuất ra PowerPoint bằng Java
schemas:
- author: Aspose
  dateModified: '2026-09-05'
  description: Learn how to copy range in Excel, export excel to PowerPoint and convert
    excel to pptx with a complete Java example.
  headline: How to copy range from Excel and export it to PowerPoint using Java
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel automation
- PowerPoint export
title: Cách sao chép phạm vi từ Excel và xuất ra PowerPoint bằng Java
url: /vi/java/integration-interoperability/how-to-copy-range-from-excel-and-export-it-to-powerpoint-usi/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách sao chép phạm vi từ Excel và xuất ra PowerPoint bằng Java

Nếu bạn cần **how to copy range** từ một workbook Excel và sau đó **export excel to PowerPoint**, hướng dẫn này cung cấp cho bạn một giải pháp hoàn chỉnh, sẵn sàng chạy. Bạn sẽ thấy chính xác cách sao chép một phạm vi chứa pivot‑table, tạo một worksheet mới cho bản sao, và cuối cùng **convert Excel to PPTX** bằng một lời gọi phương thức duy nhất.

Sao chép phạm vi và xuất workbook là một yêu cầu phổ biến khi bạn tạo báo cáo, slide deck hoặc dashboard một cách tự động. Khi kết thúc tutorial này, bạn sẽ có một chương trình Java mà:

* Tải một tệp `.xlsx` hiện có.
* Sao chép phạm vi `A1:H20` (bao gồm một pivot table) sang một sheet mới.
* Lưu workbook dưới dạng bản trình bày `.pptx` có thể chỉnh sửa.

Bạn chỉ cần thư viện Aspose.Cells for Java; không cần phụ thuộc bổ sung nào.

## Yêu cầu trước

Trước khi bắt đầu, hãy chắc chắn rằng bạn có:

* Java 17 (hoặc mới hơn) đã được cài đặt.
* Maven hoặc Gradle để quản lý các phụ thuộc.
* Aspose.Cells for Java 23.9 (hoặc phiên bản mới nhất) – thêm nó vào dự án của bạn như trong đoạn mã Maven bên dưới.
* Một tệp Excel (`input.xlsx`) chứa dữ liệu và pivot table mà bạn muốn sao chép.

```xml
<!-- Maven dependency -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
    <classifier>jdk17</classifier>
</dependency>
```

## Bước 1: Tải workbook từ tệp

Hoạt động đầu tiên trong **how to copy range** là mở workbook nguồn. Điều này cho phép bạn truy cập vào worksheets, cells và pivot tables.

```java
// Load the workbook from a file
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

*Why this step?*  
*Tại sao cần bước này?*  

Việc tải tệp tạo ra một biểu diễn trong bộ nhớ của tài liệu Excel, cho phép bạn thao tác nội dung mà không làm ảnh hưởng tới tệp gốc.

## Bước 2: Lấy worksheet nguồn chứa dữ liệu

Thông thường sheet đầu tiên chứa dữ liệu bạn muốn sao chép. Bạn có thể lấy nó bằng chỉ số.

```java
// Get the source worksheet (first sheet) that contains the data/pivot table
Worksheet sourceSheet = workbook.getWorksheets().get(0);
```

Nếu workbook của bạn lưu pivot table trên một sheet khác, thay `0` bằng chỉ số phù hợp hoặc sử dụng `get("SheetName")`.

## Bước 3: Thêm một worksheet mới cho phạm vi đã sao chép

Tạo một sheet đích giúp tách biệt dữ liệu đã sao chép và làm cho quá trình xuất sau này gọn gàng hơn.

```java
// Add a new worksheet that will receive the copied range
Worksheet destinationSheet = workbook.getWorksheets().add("Copy");
```

Bạn có thể đặt tên cho sheet bất kỳ; tên “Copy” rõ ràng cho biết nó chứa phạm vi đã sao chép.

## Bước 4: Sao chép phạm vi (how to copy range) bao gồm pivot table

Bây giờ chúng ta thực hiện thao tác cốt lõi **how to copy range**. Phương thức `copyRange` sao chép cả giá trị và định dạng, và nó giữ nguyên định nghĩa của pivot table.

```java
// Copy the range A1:H20 (including the pivot table) to the new sheet starting at A1
sourceSheet.getCells().copyRange(
        "A1:H20",
        destinationSheet.getCells().get("A1"),
        new CopyOptions()   // default options copy values, formats, and objects
);
```

*Why use `CopyOptions`?*  
*Tại sao sử dụng `CopyOptions`?*  

Cung cấp một instance của `CopyOptions` cho phép bạn tinh chỉnh những gì sẽ được sao chép (ví dụ: công thức, độ rộng cột). Constructor mặc định sao chép mọi thứ, điều này lý tưởng khi bạn muốn một bản sao chính xác của một **copy pivot table sheet**.

## Bước 5: Chuẩn bị các tùy chọn để xuất workbook dưới dạng bản trình bày PowerPoint có thể chỉnh sửa

Xuất ra PowerPoint được thực hiện thông qua `ImageOrPrintOptions`. Đặt định dạng lưu thành `SaveFormat.PPTX` cho Aspose.Cells biết tạo tệp PowerPoint thay vì hình ảnh.

```java
// Prepare options to export the workbook as an editable PowerPoint presentation
ImageOrPrintOptions pptOptions = new ImageOrPrintOptions();
pptOptions.setSaveFormat(SaveFormat.PPTX);   // this enables export excel to powerpoint
```

Bạn cũng có thể điều chỉnh kích thước slide, DPI và các cài đặt trình bày khác qua `pptOptions` nếu cần bố cục tùy chỉnh.

## Bước 6: Lưu workbook dưới dạng tệp PPTX (convert excel to pptx)

Cuối cùng, gọi `workbook.save` với các tùy chọn PPTX. Bước này **how to export excel** vào một slide deck.

```java
// Save the workbook to a PPTX file using the configured options
workbook.save("YOUR_DIRECTORY/output.pptx", pptOptions);
```

Sau khi chương trình kết thúc, `output.pptx` sẽ chứa một slide duy nhất trong đó phạm vi đã sao chép hiển thị chính xác như trong Excel, bao gồm cả các điều khiển của pivot table.

### Kết quả mong đợi

Mở `output.pptx` trong Microsoft PowerPoint hoặc bất kỳ trình xem nào tương thích. Bạn sẽ thấy một slide với phạm vi `A1:H20` được hiển thị, giữ nguyên màu ô, viền và bố cục pivot table. Slide này hoàn toàn có thể chỉnh sửa — bạn có thể di chuyển, thay đổi kích thước hoặc định dạng bảng giống như bất kỳ nội dung PowerPoint gốc nào.

## Ví dụ đầy đủ có thể chạy

Kết hợp tất cả các bước lại với nhau sẽ cho bạn một lớp Java tự chứa:

```java
import com.aspose.cells.*;

public class ExcelToPowerPoint {
    public static void main(String[] args) throws Exception {
        // 1. Load the workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // 2. Get the source worksheet (first sheet)
        Worksheet sourceSheet = workbook.getWorksheets().get(0);

        // 3. Add a destination worksheet
        Worksheet destinationSheet = workbook.getWorksheets().add("Copy");

        // 4. Copy the range A1:H20 (including pivot table)
        sourceSheet.getCells().copyRange(
                "A1:H20",
                destinationSheet.getCells().get("A1"),
                new CopyOptions()
        );

        // 5. Configure export options for PowerPoint
        ImageOrPrintOptions pptOptions = new ImageOrPrintOptions();
        pptOptions.setSaveFormat(SaveFormat.PPTX);

        // 6. Save as PPTX
        workbook.save("YOUR_DIRECTORY/output.pptx", pptOptions);

        System.out.println("Export completed: output.pptx created successfully.");
    }
}
```

Chạy lớp này từ IDE của bạn hoặc qua dòng lệnh:

```bash
mvn compile exec:java -Dexec.mainClass=ExcelToPowerPoint
```

Bạn sẽ thấy thông báo xác nhận khi tệp đã được ghi.

## Các câu hỏi thường gặp và các trường hợp đặc biệt

| Question | Answer |
|----------|--------|
| **Tôi có thể sao chép một phạm vi không liên tiếp không?** | Sử dụng `copyRange` với một named range bao gồm nhiều vùng, hoặc gọi `copyRange` nhiều lần cho mỗi khối. |
| **Nếu sheet nguồn chứa nhiều pivot table thì sao?** | Mỗi pivot table nằm trong hình chữ nhật đã sao chép sẽ được chuyển. Đối với các bảng nằm ngoài hình chữ nhật, hãy sao chép chúng riêng. |
| **Làm sao để xuất nhiều sheet thành các slide riêng biệt?** | Duyệt qua các worksheet, sao chép mỗi cái vào một sheet tạm thời, và gọi `workbook.save` với `pptOptions` cho mỗi vòng lặp, thêm vào cùng một PPTX thông qua API `Presentation`. |
| **PPTX được tạo có thể chỉnh sửa không?** | Có. Quá trình xuất tạo ra các đối tượng PowerPoint gốc, vì vậy bạn có thể chỉnh sửa văn bản, thay đổi kích thước bảng, hoặc thêm hoạt ảnh sau khi tạo. |
| **Còn các workbook lớn thì sao?** | Tăng `pptOptions.setDpi(300)` để có độ chính xác cao hơn, nhưng cần chú ý đến việc sử dụng bộ nhớ; xử lý các sheet theo lô nếu cần. |

## Mẹo chuyên nghiệp

* **Giữ nguyên độ rộng cột** – đặt `CopyOptions.setColumnWidth(true)` trước khi sao chép nếu bạn cần độ rộng chính xác.  
* **Sử dụng kích thước slide tùy chỉnh** – `pptOptions.setImageHeight(720); pptOptions.setImageWidth(1280);` để phù hợp với bản trình bày 16:9.  
* **Thêm slide tiêu đề** – sau khi xuất, mở PPTX bằng Aspose.Slides và chèn một slide đầu tiên có tiêu đề và ngày tháng.

## Kết luận

Bây giờ bạn đã biết **how to copy range** từ một workbook Excel, **export excel to PowerPoint**, và **convert excel to pptx** bằng Java. Bằng cách thực hiện sáu bước trên, bạn có thể tự động tạo báo cáo, tạo slide deck từ dữ liệu trực tiếp, và giữ nguyên chức năng của pivot‑table.

### Tiếp theo là gì?

* Khám phá các biến thể **copy pivot table sheet** như sao chép chỉ pivot cache.  
* Kết hợp quy trình này với **Aspose.Slides** để thêm hoạt ảnh hoặc thương hiệu tùy chỉnh.  
* Tự động xử lý hàng loạt cho hàng chục workbook trong một công việc định kỳ.

Hãy tự do thử nghiệm các tùy chọn và điều chỉnh mã cho quy trình báo cáo của riêng bạn. Nếu gặp bất kỳ vấn đề nào, tài liệu Aspose.Cells for Java cung cấp thông tin chi tiết hơn về `CopyOptions` và `ImageOrPrintOptions`. Chúc lập trình vui vẻ!

## Bạn nên học gì tiếp theo?

Các tutorial sau đây bao gồm các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh với giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [How to Export Excel to PowerPoint – Step‑by‑Step Guide](/cells/english/net/converting-excel-files-to-other-formats/how-to-export-excel-to-powerpoint-step-by-step-guide/)
- [How to Copy Multiple Columns in Excel Using Aspose.Cells Java&#58; A Complete Guide](/cells/english/java/range-management/copy-multiple-columns-excel-aspose-cells-java/)
- [How to Convert Excel to PowerPoint Using Aspose.Cells for .NET&#58; A Complete Guide](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}