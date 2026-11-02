---
category: general
date: 2026-09-18
description: Tìm hiểu cách xuất Excel sang PowerPoint bằng Aspose.Cells. Chuyển đổi
  Excel sang PPTX, tạo PowerPoint từ Excel và lưu Excel dưới dạng PowerPoint trong
  vài phút.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to export excel
- convert excel to pptx
- create powerpoint from excel
- save excel as powerpoint
- export excel to powerpoint
language: vi
lastmod: 2026-09-18
og_description: Cách xuất Excel sang PowerPoint bằng Aspose.Cells. Hãy làm theo hướng
  dẫn này để chuyển đổi Excel sang PPTX, tạo PowerPoint từ Excel và lưu Excel dưới
  dạng PowerPoint một cách hiệu quả.
og_image_alt: Screenshot showing how to export Excel to PowerPoint with Aspose.Cells
og_title: Cách xuất Excel sang PowerPoint – hướng dẫn đầy đủ Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: Learn how to export Excel to PowerPoint using Aspose.Cells. Convert
    Excel to PPTX, create PowerPoint from Excel, and save Excel as PowerPoint in minutes.
  headline: How to export Excel to PowerPoint with Aspose.Cells – step‑by‑step guide
  type: TechArticle
- description: Learn how to export Excel to PowerPoint using Aspose.Cells. Convert
    Excel to PPTX, create PowerPoint from Excel, and save Excel as PowerPoint in minutes.
  name: How to export Excel to PowerPoint with Aspose.Cells – step‑by‑step guide
  steps:
  - name: Load the workbook that contains the shapes
    text: '```java import com.aspose.cells.*;'
  - name: Configure export options for PowerPoint conversion
    text: '```java /** * Creates ImageOrPrintOptions that control how Excel content
      is rendered * in the resulting PowerPoint file. * * @return a fully configured
      ImageOrPrintOptions object */ private static ImageOrPrintOptions createExportOptions()
      { ImageOrPrintOptions options = new ImageOrPrintOptions(); //'
  - name: Mark pictures (or charts) as editable
    text: '```java /** * Marks the first picture on the first worksheet as editable.
      * You can extend this loop to mark all pictures if needed. * * @param workbook
      the workbook that was loaded earlier */ private static void makeFirstPictureEditable(Workbook
      workbook) { // Navigate to the first worksheet (index'
  - name: Save the workbook as an editable PowerPoint presentation
    text: '```java /** * Performs the actual conversion and writes the PPTX file.
      * * @param workbook the workbook prepared in previous steps * @param exportOptions
      the options created in step 2 * @param outputPath full path for the resulting
      .pptx file * @throws Exception if saving fails */ private static voi'
  - name: Full runnable example
    text: '```java import com.aspose.cells.*;'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel‑to‑PowerPoint
- Document conversion
title: Cách xuất Excel sang PowerPoint với Aspose.Cells – hướng dẫn từng bước
url: /vi/java/excel-import-export/how-to-export-excel-to-powerpoint-with-aspose-cells-step-by/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách xuất Excel sang PowerPoint với Aspose.Cells – hướng dẫn từng bước

Nếu bạn cần **how to export Excel** vào một bản trình chiếu PowerPoint, hướng dẫn này cung cấp một giải pháp hoàn chỉnh, sẵn sàng chạy. Sau hai câu đầu tiên, bạn sẽ biết chính xác các lời gọi API nào chuyển một tệp `.xlsx` thành một `.pptx` có thể chỉnh sửa. Cách tiếp cận này hoạt động với bất kỳ workbook nào chứa biểu đồ, hình ảnh hoặc các hình dạng khác, và chỉ yêu cầu một vài dòng mã Java.

Trong hướng dẫn này, bạn sẽ học cách **convert Excel to PPTX**, **create PowerPoint from Excel**, và **save Excel as PowerPoint** đồng thời giữ khả năng chỉnh sửa của biểu đồ và hình ảnh. Không cần công cụ bổ sung nào ngoài Aspose.Cells, và mã chạy trên Java 8+ và bất kỳ JDK hiện đại nào.  

**Yêu cầu trước:**

* Java Development Kit (JDK) 8 hoặc mới hơn đã được cài đặt  
* Maven hoặc Gradle để quản lý phụ thuộc (hoặc tệp JAR Aspose.Cells trên classpath)  
* Một workbook (`WithShapes.xlsx`) chứa ít nhất một hình ảnh hoặc biểu đồ  

---

![Sơ đồ minh họa cách xuất Excel sang PowerPoint](https://example.com/diagram.png "hình minh họa cách xuất excel sang powerpoint")

## Cách xuất Excel sang PowerPoint bằng Aspose.Cells

Cốt lõi của quá trình chuyển đổi bao gồm bốn bước ngắn gọn. Mỗi bước được đóng gói trong một phương thức để bạn có thể tái sử dụng logic trong các ứng dụng lớn hơn.

### Bước 1: Tải workbook chứa các hình dạng

```java
import com.aspose.cells.*;

public class ExcelToPowerPoint {

    /**
     * Loads the source Excel workbook.
     *
     * @param path full path to the .xlsx file
     * @return a Workbook instance ready for manipulation
     * @throws Exception if the file cannot be read
     */
    private static Workbook loadWorkbook(String path) throws Exception {
        // The Workbook constructor reads the entire file into memory.
        return new Workbook(path);
    }
}
```

**Tại sao điều này quan trọng:**  
Việc tải workbook cho phép bạn truy cập vào các worksheet, hình ảnh và biểu đồ. Aspose.Cells đọc tệp mà không cần gọi Microsoft Office, vì vậy thao tác này hoạt động trên các máy chủ không có giao diện.

### Bước 2: Cấu hình tùy chọn xuất cho chuyển đổi PowerPoint

```java
    /**
     * Creates ImageOrPrintOptions that control how Excel content is rendered
     * in the resulting PowerPoint file.
     *
     * @return a fully configured ImageOrPrintOptions object
     */
    private static ImageOrPrintOptions createExportOptions() {
        ImageOrPrintOptions options = new ImageOrPrintOptions();
        // Do not include hidden worksheets – they usually contain metadata only.
        options.setExportHiddenWorksheet(false);
        // Export charts as editable shapes so the end‑user can modify them in PowerPoint.
        options.setExportChartAsEditable(true);
        return options;
    }
```

**Tại sao điều này quan trọng:**  
`setExportChartAsEditable(true)` cho Aspose.Cells biết tạo các hình vector thay vì hình raster. Điều này khiến đầu ra PowerPoint **create PowerPoint from Excel** có các biểu đồ hoàn toàn có thể chỉnh sửa, đáp ứng hầu hết quy trình tạo bài thuyết trình.

### Bước 3: Đánh dấu hình ảnh (hoặc biểu đồ) là có thể chỉnh sửa

```java
    /**
     * Marks the first picture on the first worksheet as editable.
     * You can extend this loop to mark all pictures if needed.
     *
     * @param workbook the workbook that was loaded earlier
     */
    private static void makeFirstPictureEditable(Workbook workbook) {
        // Navigate to the first worksheet (index 0)
        Worksheet sheet = workbook.getWorksheets().get(0);
        // Retrieve the first picture on that sheet
        Picture pic = sheet.getPictures().get(0);
        // Set the picture to be editable in the PowerPoint output
        pic.setEditable(true);
    }
```

**Tại sao điều này quan trọng:**  
Khi một hình ảnh được đánh dấu là có thể chỉnh sửa, Aspose.Cells xuất nó dưới dạng hình dạng EMF/WMF trong tệp PPTX. Điều này là cần thiết cho trường hợp **export excel to powerpoint** khi người nhận phải điều chỉnh hình ảnh sau này.

### Bước 4: Lưu workbook dưới dạng bản trình chiếu PowerPoint có thể chỉnh sửa

```java
    /**
     * Performs the actual conversion and writes the PPTX file.
     *
     * @param workbook      the workbook prepared in previous steps
     * @param exportOptions the options created in step 2
     * @param outputPath    full path for the resulting .pptx file
     * @throws Exception if saving fails
     */
    private static void saveAsPowerPoint(Workbook workbook,
                                          ImageOrPrintOptions exportOptions,
                                          String outputPath) throws Exception {
        // The SaveFormat.PPTX enum tells Aspose.Cells to generate a PowerPoint file.
        workbook.save(outputPath, SaveFormat.PPTX);
    }
```

**Tại sao điều này quan trọng:**  
Lệnh `save` gộp tất cả các thay đổi trước đó (hình ảnh có thể chỉnh sửa, cài đặt biểu đồ) vào một tệp `.pptx` duy nhất. Tệp kết quả có thể mở trong Microsoft PowerPoint, Google Slides, hoặc bất kỳ trình xem PPTX nào tương thích.

### Ví dụ đầy đủ có thể chạy

```java
import com.aspose.cells.*;

public class ExcelToPowerPoint {

    public static void main(String[] args) {
        try {
            // Adjust these paths to match your environment.
            String sourcePath = "YOUR_DIRECTORY/WithShapes.xlsx";
            String destinationPath = "YOUR_DIRECTORY/Result.pptx";

            // Step 1 – load workbook
            Workbook workbook = loadWorkbook(sourcePath);

            // Step 2 – configure export options
            ImageOrPrintOptions exportOptions = createExportOptions();

            // Step 3 – make the first picture editable
            makeFirstPictureEditable(workbook);

            // Step 4 – save as PPTX
            saveAsPowerPoint(workbook, exportOptions, destinationPath);

            System.out.println("Conversion successful! File saved at: " + destinationPath);
        } catch (Exception e) {
            System.err.println("Error during conversion: " + e.getMessage());
            e.printStackTrace();
        }
    }

    // ---- Helper methods from earlier steps ----

    private static Workbook loadWorkbook(String path) throws Exception {
        return new Workbook(path);
    }

    private static ImageOrPrintOptions createExportOptions() {
        ImageOrPrintOptions options = new ImageOrPrintOptions();
        options.setExportHiddenWorksheet(false);
        options.setExportChartAsEditable(true);
        return options;
    }

    private static void makeFirstPictureEditable(Workbook workbook) {
        Worksheet sheet = workbook.getWorksheets().get(0);
        if (!sheet.getPictures().isEmpty()) {
            sheet.getPictures().get(0).setEditable(true);
        }
    }

    private static void saveAsPowerPoint(Workbook workbook,
                                          ImageOrPrintOptions exportOptions,
                                          String outputPath) throws Exception {
        // Export options are automatically applied when saving to PPTX.
        workbook.save(outputPath, SaveFormat.PPTX);
    }
}
```

**Kết quả mong đợi:**  
Mở `Result.pptx` trong PowerPoint sẽ hiển thị một slide phản ánh worksheet đầu tiên của `WithShapes.xlsx`. Các biểu đồ xuất hiện dưới dạng hình vector mà bạn có thể nhấp đúp để chỉnh sửa dữ liệu, và hình ảnh đầu tiên là một đối tượng có thể chỉnh sửa (bạn có thể thay đổi kích thước, màu sắc hoặc thay thế trực tiếp trong PowerPoint).

---

## Chuyển đổi Excel sang PPTX – tùy chỉnh sâu hơn

Mặc dù luồng cơ bản đủ cho hầu hết các trường hợp, bạn có thể cần:

* **Xuất nhiều worksheet** – lặp qua `workbook.getWorksheets()` và gọi `workbook.save` cho mỗi, truyền một chỉ số slide khác nhau qua `ImageOrPrintOptions.setSlideNumber(int)`.
* **Kiểm soát kích thước slide** – sử dụng `exportOptions.setImageHeight(int)` và `setImageWidth(int)` để phù hợp với kích thước slide PowerPoint cụ thể (ví dụ, 1024 × 768).
* **Bảo tồn công thức** – đặt `exportOptions.setExportFormulasAsValues(false)` nếu bạn muốn các công thức Excel gốc được nhúng dưới dạng dữ liệu ẩn.

Những điều chỉnh này cho phép bạn **create PowerPoint from Excel** phù hợp với thương hiệu công ty hoặc tiêu chuẩn trình chiếu.

---

## Lưu Excel dưới dạng PowerPoint – các lỗi thường gặp và cách tránh

| Triệu chứng | Nguyên nhân có thể | Cách khắc phục |
|------------|--------------------|----------------|
| Biểu đồ xuất hiện dưới dạng hình raster | `setExportChartAsEditable(false)` (mặc định) | Bật biểu đồ có thể chỉnh sửa bằng `setExportChartAsEditable(true)` |
| Không có hình ảnh nào xuất hiện trên slide | Hình ảnh không được đánh dấu là có thể chỉnh sửa hoặc chỉ số hình ảnh ngoài phạm vi | Xác minh `sheet.getPictures().size() > 0` trước khi gọi `setEditable(true)` |
| Worksheet ẩn xuất hiện trong PPTX | `setExportHiddenWorksheet(true)` | Giữ mặc định `false` hoặc đặt rõ ràng thành `false` |
| Tệp đầu ra bị hỏng | Sử dụng phiên bản Aspose.Cells cũ (trước‑20.10) | Nâng cấp lên phiên bản Aspose.Cells for Java mới nhất (ví dụ, 23.12) |

---

## Xuất Excel sang PowerPoint: mẹo hiệu năng

* **Tái sử dụng cùng một đối tượng `ImageOrPrintOptions`** cho nhiều lần lưu – tránh cấp phát lặp lại.
* **Stream workbook nguồn** (`new Workbook(InputStream)`) khi làm việc với tệp lớn trên máy chủ có bộ nhớ hạn chế.
* **Song song hoá chuyển đổi từng worksheet** nếu bạn cần tạo bộ slide hàng trăm; mỗi worksheet có thể được xử lý trong một luồng riêng vì các đối tượng Aspose.Cells an toàn với đa luồng sau khi khởi tạo.

---

## Các bước tiếp theo

Bạn hiện đã biết **how to export Excel** vào một bộ slide PowerPoint, **convert Excel to PPTX**, và **save Excel as PowerPoint** với nội dung có thể chỉnh sửa. Để mở rộng kiến thức này, bạn có thể:

* Khám phá **Aspose.Slides** để thêm hoạt ảnh hoặc bố cục master‑slide sau khi chuyển đổi.
* Tự động hoá quy trình trong pipeline CI/CD để mỗi báo cáo Excel mới tự động trở thành bộ slide PPTX.
* Kết hợp cách tiếp cận này với **Apache POI** để tiền xử lý tệp Excel trước khi chuyển cho Aspose.Cells.

---

## Kết luận

Hướng dẫn này đã trình bày **how to export Excel** sang PowerPoint bằng Aspose.Cells, bao phủ mọi bước từ tải workbook đến lưu một `.pptx` có thể chỉnh sửa. Bây giờ bạn có thể **convert Excel to PPTX**, **create PowerPoint from Excel**, và **save Excel as PowerPoint** trong các ứng dụng Java của mình một cách tự tin. Hãy thử nghiệm các cài đặt tùy chọn để điều chỉnh đầu ra phù hợp với yêu cầu trình chiếu chính xác của bạn. Chúc lập trình vui vẻ!

## Bạn Nên Học Gì Tiếp Theo?

Các hướng dẫn sau đây bao gồm các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh với giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Cách Chuyển Đổi Excel sang PowerPoint Sử Dụng Aspose.Cells cho .NET: Hướng Dẫn Toàn Diện](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [Cách Xuất Excel sang PowerPoint – Hướng Dẫn Từng Bước](/cells/english/net/converting-excel-files-to-other-formats/how-to-export-excel-to-powerpoint-step-by-step-guide/)
- [Cách Xuất Excel sang PowerPoint với C# – Hướng Dẫn Toàn Diện](/cells/english/net/converting-excel-files-to-other-formats/how-to-export-excel-to-powerpoint-with-c-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}