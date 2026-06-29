---
category: general
date: 2026-06-27
description: Cách xuất biểu đồ từ Excel sang PowerPoint bằng Java. Học cách chuyển
  bảng tính sang PowerPoint, lưu tệp PPTX và xuất dữ liệu Excel sang PPT một cách
  dễ dàng.
draft: false
keywords:
- how to export charts
- convert spreadsheet to powerpoint
- how to save pptx
- excel to powerpoint slide
- export excel data ppt
language: vi
og_description: Cách xuất biểu đồ từ Excel sang PowerPoint bằng Java. Hướng dẫn chi
  tiết này chỉ cho bạn cách chuyển bảng tính sang PowerPoint, lưu tệp PPTX và xuất
  dữ liệu Excel sang PPT.
og_title: Cách xuất biểu đồ từ Excel sang PowerPoint – Hướng dẫn Java
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: How to export charts from Excel to PowerPoint using Java. Learn to
    convert spreadsheet to PowerPoint, save PPTX files, and export Excel data PPT
    effortlessly.
  headline: How to Export Charts from Excel to PowerPoint – Full Java Guide
  type: TechArticle
- description: How to export charts from Excel to PowerPoint using Java. Learn to
    convert spreadsheet to PowerPoint, save PPTX files, and export Excel data PPT
    effortlessly.
  name: How to Export Charts from Excel to PowerPoint – Full Java Guide
  steps:
  - name: '**Load** the workbook you want to transform.'
    text: '**Load** the workbook you want to transform.'
  - name: '**Configure** a `PresentationOptions` instance to tell Aspose which elements
      (charts, OLE objects, etc.) should make it into the slide deck.'
    text: '**Configure** a `PresentationOptions` instance to tell Aspose which elements
      (charts, OLE objects, etc.) should make it into the slide deck.'
  - name: '**Save** the workbook using the `PPTX` format and the options you configured.'
    text: '**Save** the workbook using the `PPTX` format and the options you configured.'
  type: HowTo
tags:
- Java
- Aspose.Cells
- Excel
- PowerPoint
title: Cách xuất biểu đồ từ Excel sang PowerPoint – Hướng dẫn Java đầy đủ
url: /vi/java/integration-interoperability/how-to-export-charts-from-excel-to-powerpoint-full-java-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách Xuất Biểu Đồ Từ Excel Sang PowerPoint – Hướng Dẫn Java Đầy Đủ

Bạn đã bao giờ tự hỏi **cách xuất biểu đồ** từ một workbook Excel trực tiếp vào một slide PowerPoint chưa? Bạn không phải là người duy nhất—các nhà phát triển thường cần chuyển các bảng tính dựa trên dữ liệu thành các bộ trình chiếu sẵn sàng mà không phải thực hiện việc sao chép‑dán thủ công rườm rà. Trong hướng dẫn này, chúng tôi sẽ trình bày một giải pháp lập trình sạch sẽ, cho phép bạn **chuyển đổi spreadsheet sang PowerPoint**, lưu kết quả dưới dạng PPTX và thậm chí tinh chỉnh việc xử lý biểu đồ ngay trong quá trình thực thi.

Bạn sẽ có ngay một đoạn mã Java sẵn sàng chạy, nhận bất kỳ workbook nào, trích xuất các biểu đồ (và các đối tượng OLE nếu muốn), và tạo ra một file **excel to powerpoint slide** hoàn chỉnh. Không có UI phụ trợ, không có VBA rắc rối, chỉ có mã Java thuần túy mà bạn có thể đưa vào dự án ngay hôm nay.

## Yêu Cầu Trước

Trước khi bắt đầu, hãy chắc chắn rằng bạn đã có:

- **Java 17** trở lên (API hoạt động trên bất kỳ JDK mới nào)
- Thư viện **Aspose.Cells for Java** (mã sử dụng `PresentationOptions` và `SaveFormat.PPTX`)
- Kiến thức cơ bản về cấu hình dự án Java (Maven/Gradle)
- Một file Excel (`.xlsx`) chứa ít nhất một biểu đồ bạn muốn xuất

Nếu bạn chưa có JAR của Aspose.Cells, hãy thêm nó qua Maven:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- check for the latest version -->
</dependency>
```

Hoặc tải JAR trực tiếp từ trang web Aspose và đặt vào classpath của bạn.

## Cách Xuất Biểu Đồ – Tổng Quan

Ở mức cao, quy trình như sau:

1. **Tải** workbook bạn muốn chuyển đổi.
2. **Cấu hình** một thể hiện `PresentationOptions` để chỉ định cho Aspose những thành phần (biểu đồ, đối tượng OLE, v.v.) sẽ được đưa vào bộ slide.
3. **Lưu** workbook dưới định dạng `PPTX` cùng với các tùy chọn bạn đã cấu hình.

Đó là tất cả. Thư viện sẽ thực hiện phần lớn công việc—kết xuất mỗi biểu đồ dưới dạng đồ họa vector, giữ nguyên bố cục, và tạo file PowerPoint mà PowerPoint có thể mở mà không gặp lỗi.

Dưới đây chúng tôi sẽ phân tích từng bước, giải thích *tại sao* chúng quan trọng, và cung cấp đoạn mã chính xác mà bạn cần.

## Bước 1: Tải Workbook và Cấu Hình Các Tùy Chọn Xuất

Đầu tiên, chúng ta cần chỉ định cho Aspose những gì sẽ được bao gồm khi tạo PowerPoint. Lớp `PresentationOptions` cho phép kiểm soát chi tiết. Thiết lập `setExportCharts(true)` đảm bảo mọi biểu đồ đều trở thành một thành phần slide, trong khi `setExportOleObjects(true)` sẽ đưa vào bất kỳ đối tượng nhúng nào (như bảng Excel) mà bạn có thể có.

```java
import com.aspose.cells.*;

public class ExcelToPowerPointExporter {

    public static void main(String[] args) throws Exception {
        // -------------------------------------------------
        // 1️⃣ Load the source Excel workbook
        // -------------------------------------------------
        String srcPath = "C:/data/sourceWorkbook.xlsx";
        Workbook workbook = new Workbook(srcPath);

        // -------------------------------------------------
        // 2️⃣ Configure presentation export options
        // -------------------------------------------------
        PresentationOptions presentationOptions = new PresentationOptions();
        presentationOptions.setExportCharts(true);          // <-- how to export charts
        presentationOptions.setExportOleObjects(true);     // include embedded OLE objects

        // The next lines are optional but often useful:
        presentationOptions.setExportFormulas(false);      // skip raw formulas if you only need visuals
        presentationOptions.setExportImages(true);         // grab any pictures as well
```

**Tại sao bước này quan trọng:**  
Nếu bạn bỏ qua `setExportCharts(true)`, Aspose sẽ xử lý biểu đồ như các ô thông thường, đổ dữ liệu của chúng vào slide thay vì hiển thị dưới dạng biểu đồ trực quan. Điều này làm mất mục đích của một bản trình chiếu. Tương tự, bật/tắt xuất OLE cho phép bạn giữ các đối tượng phức tạp (như pivot table) mà không cần viết mã bổ sung.

> **Mẹo chuyên nghiệp:** Khi làm việc với workbook lớn, hãy cân nhắc tắt `setExportFormulas` để tăng tốc độ chuyển đổi. Kết quả hình ảnh vẫn giữ nguyên, nhưng quá trình sẽ nhẹ hơn về bộ nhớ.

## Bước 2: Lưu Workbook Dưới Dạng File PowerPoint

Khi các tùy chọn đã sẵn sàng, việc chuyển đổi thực tế chỉ cần một dòng lệnh: gọi `workbook.save(...)` với enum `SaveFormat.PPTX`. Đây là phần trả lời **cách lưu pptx** trong Java.

```java
        // -------------------------------------------------
        // 3️⃣ Save the workbook as a PowerPoint file
        // -------------------------------------------------
        String outPath = "C:/output/slide.pptx";
        workbook.save(outPath, SaveFormat.PPTX, presentationOptions);

        System.out.println("✅ Conversion complete! Check " + outPath);
    }
}
```

**Bên trong thực tế xảy ra gì?**  
Aspose duyệt qua từng worksheet, trích xuất mọi biểu đồ, chuyển chúng thành một shape PowerPoint (thường là vector EMF), và đặt vào một slide mới. Nếu bạn có nhiều worksheet, mỗi worksheet sẽ có một slide mặc định. Bạn có thể sắp xếp lại các slide sau này bằng Apache POI hoặc chính PowerPoint.

### Kết Quả Mong Đợi

Mở `slide.pptx` trong Microsoft PowerPoint, bạn sẽ thấy:

- Một slide cho mỗi worksheet (hoặc cho mỗi biểu đồ, tùy thuộc vào nguồn)
- Các biểu đồ được hiển thị sắc nét, giữ nguyên màu sắc và nhãn dữ liệu
- Bất kỳ đối tượng OLE nào (như bảng Excel nhúng) xuất hiện dưới dạng đối tượng có thể chỉnh sửa

Nếu bạn không thấy biểu đồ, hãy kiểm tra lại workbook nguồn thực sự có chứa đối tượng biểu đồ và `setExportCharts(true)` không bị ghi đè ở nơi khác.

## Phương Án Thay Thế: Xuất Một Biểu Đồ Đơn Lẻ Thành PPTX Độc Lập

Đôi khi bạn chỉ cần **excel to powerpoint slide** cho một biểu đồ cụ thể, không phải toàn bộ workbook. Bạn có thể thực hiện điều này bằng cách tạo một workbook tạm thời chỉ chứa biểu đồ bạn quan tâm.

```java
        // -------------------------------------------------
        // 4️⃣ Export a single chart (optional)
        // -------------------------------------------------
        // Assume the chart is on the first worksheet, first chart
        Worksheet sheet = workbook.getWorksheets().get(0);
        int chartIndex = 0; // change if you have multiple charts
        Chart chart = sheet.getCharts().get(chartIndex);

        // Clone the chart into a new workbook
        Workbook singleChartWb = new Workbook();
        Worksheet newSheet = singleChartWb.getWorksheets().get(0);
        newSheet.getCharts().addCopy(chart);

        // Use the same PresentationOptions
        singleChartWb.save("C:/output/singleChart.pptx", SaveFormat.PPTX, presentationOptions);
```

**Lý do bạn có thể muốn làm như vậy:**  
Nếu bạn đang tạo một bộ slide “on‑the‑fly” (ví dụ, dịch vụ báo cáo gửi một biểu đồ mỗi email), việc tạo một workbook tối thiểu sẽ giảm sử dụng bộ nhớ và tăng tốc độ thực thi.

## Những Sai Lầm Thường Gặp & Cách Tránh

| Vấn đề | Triệu chứng | Giải pháp |
|-------|-------------|-----------|
| Biểu đồ biến mất | Các slide trống hoặc chỉ chứa bảng dữ liệu | Đảm bảo `presentationOptions.setExportCharts(true)` được gọi **trước** `workbook.save`. |
| Kích thước file lớn | PPTX > 30 MB chỉ với vài biểu đồ | Tắt xuất hình ảnh (`setExportImages(false)`) hoặc nén hình ảnh trong PowerPoint sau khi tạo. |
| Thiếu đối tượng OLE | Bảng Excel nhúng chuyển thành hình ảnh tĩnh | Đặt `setExportOleObjects(true)`; đồng thời kiểm tra các đối tượng OLE nguồn không bị bảo vệ. |
| Lỗi tương thích | PowerPoint báo file bị hỏng | Sử dụng phiên bản mới nhất của Aspose.Cells; các phiên bản cũ có thể có lỗi khi tạo PPTX. |

## Xuất Biểu Đồ Trong Quy Trình CI/CD

Nếu bạn tự động hoá việc tạo báo cáo trong quá trình build, bạn có thể nhúng đoạn mã trên vào một plugin Maven hoặc một task Gradle. Chỉ cần đảm bảo JVM có đủ heap (ví dụ, `-Xmx2g`) khi xử lý các workbook lớn.

```groovy
task exportCharts(type: JavaExec) {
    classpath = sourceSets.main.runtimeClasspath
    main = 'com.example.ExcelToPowerPointExporter'
    args = []
    jvmArgs = ['-Xmx2g']
}
```

Chạy `./gradlew exportCharts` sẽ tạo ra file PPTX mà không cần bất kỳ can thiệp thủ công nào—hoàn hảo cho các job báo cáo hàng đêm.

## Ví Dụ Hoàn Chỉnh (Sẵn Sàng Sao Chép‑Dán)

Dưới đây là lớp Java hoàn chỉnh, tự chứa, bạn có thể đưa vào bất kỳ IDE nào. Nó bao gồm tất cả các import, xử lý lỗi, và chú thích giải thích từng dòng.

```java
// FullExample.java
import com.aspose.cells.*;

public class FullExample {
    public static void main(String[] args) {
        try {
            // 👉 1️⃣ Load the Excel workbook you want to convert
            String srcFile = "C:/data/analysis.xlsx";
            Workbook wb = new Workbook(srcFile);

            // 👉 2️⃣ Set up export options – this is the core of how to export charts
            PresentationOptions opts = new PresentationOptions();
            opts.setExportCharts(true);          // include every chart
            opts.setExportOleObjects(true);     // keep OLE objects (tables, etc.)
            opts.setExportImages(true);         // optionally keep pictures
            opts.setExportFormulas(false);      // skip formulas for speed

            // 👉 3️⃣ Choose where the PPTX will be saved – answer to how to save pptx
            String outFile = "C:/output/analysis.pptx";

            // 👉 4️⃣ Perform the conversion
            wb.save(outFile, SaveFormat.PPTX, opts);

            System.out.println("✅ Excel file converted to PowerPoint successfully!");
        } catch (Exception e) {
            System.err.println("❌ Conversion failed: " + e.getMessage());
            e.printStackTrace();
        }
    }
}
```

Chạy lớp này, mở `analysis.pptx`, và bạn sẽ thấy mọi biểu đồ từ bảng tính gốc giờ đã hiện diện trong một bộ PowerPoint. Đó là bản chất của **export excel data ppt**—không có bước thủ công, không có lỗi sao chép‑dán.

## Tóm Tắt Hình Ảnh

![Sơ đồ mô tả cách xuất biểu đồ từ Excel sang PowerPoint bằng Aspose.Cells](/images/export-charts-diagram.png "Cách xuất biểu đồ từ Excel sang PowerPoint")

*Hình minh họa trên mô tả luồng từ một workbook Excel → PresentationOptions → file PPTX.*

## Kết Luận

Chúng ta đã đề cập **cách xuất biểu đồ** từ Excel sang PowerPoint bằng Java, trình bày đoạn mã chính xác để **chuyển đổi spreadsheet sang PowerPoint**, và giải thích **cách lưu pptx** một cách đáng tin cậy. Bằng cách tinh chỉnh `PresentationOptions` bạn có thể kiểm soát mọi thứ từ việc bao gồm biểu đồ đến xử lý đối tượng OLE, mang lại một cầu nối linh hoạt giữa phân tích dữ liệu và lớp trình chiếu.

Bước tiếp theo? Hãy thử kết hợp chuyển đổi này với **Apache POI** để sắp xếp lại các slide một cách lập trình, hoặc nhúng quy trình vào một microservice Spring Boot cung cấp báo cáo PPTX theo yêu cầu. Bạn cũng có thể khám phá việc xuất sang **PDF** hoặc **HTML** bằng cùng một thư viện—Aspose.Cells hỗ trợ rất dễ dàng.

Có câu hỏi về các trường hợp đặc biệt,

## Bạn Nên Học Gì Tiếp Theo?


Các hướng dẫn sau đây liên quan chặt chẽ đến các kỹ thuật đã trình bày trong bài viết này. Mỗi tài nguyên bao gồm mã mẫu đầy đủ cùng các giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [How to Create and Export Charts in Java Using Aspose.Cells&#58; A Complete Guide](/cells/english/java/charts-graphs/aspose-cells-java-create-export-charts/)
- [How to Export Excel Charts as SVG Using Aspose.Cells Java for Scalable Vector Graphics](/cells/english/java/charts-graphs/export-excel-charts-svg-aspose-cells-java/)
- [Export Excel Charts to PDF Using Aspose.Cells for Java&#58; Custom Page Sizes Guide](/cells/english/java/charts-graphs/export-excel-charts-pdf-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}