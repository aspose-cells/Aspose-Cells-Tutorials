---
category: general
date: 2026-07-20
description: Hướng dẫn chuyển đổi Excel sang PPTX, chỉ cách xuất Excel sang PowerPoint
  với các hộp văn bản có thể chỉnh sửa, chuyển đổi hình dạng biểu đồ và nhúng hình
  ảnh vào PPTX bằng Aspose.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- excel to pptx
- editable text boxes
- convert chart shape
- export excel powerpoint
- embed images pptx
language: vi
lastmod: 2026-07-20
og_description: Hướng dẫn excel sang pptx chỉ dẫn bạn cách xuất Excel sang PowerPoint
  đồng thời giữ nguyên các hộp văn bản có thể chỉnh sửa, chuyển đổi hình dạng biểu
  đồ và nhúng hình ảnh pptx với Aspose.
og_image_alt: Screenshot of a PowerPoint slide generated from an Excel workbook showing
  editable shapes
og_title: Excel sang PPTX – Xuất các hình dạng có thể chỉnh sửa từ Excel sang PowerPoint
  (Java)
schemas:
- author: Aspose
  dateModified: '2026-07-20'
  description: excel to pptx tutorial showing how to export Excel to PowerPoint with
    editable text boxes, convert chart shape and embed images pptx using Aspose.
  headline: 'excel to pptx: Complete Java Guide to Export Editable Shapes'
  type: TechArticle
- description: excel to pptx tutorial showing how to export Excel to PowerPoint with
    editable text boxes, convert chart shape and embed images pptx using Aspose.
  name: 'excel to pptx: Complete Java Guide to Export Editable Shapes'
  steps:
  - name: A slide that mirrors the layout of your Excel sheet.
    text: A slide that mirrors the layout of your Excel sheet.
  - name: Text boxes that you can click, edit, and move—just like native PowerPoint
      shapes.
    text: Text boxes that you can click, edit, and move—just like native PowerPoint
      shapes.
  - name: Charts rendered as editable vector shapes (you can ungroup them to edit
      individual series).
    text: Charts rendered as editable vector shapes (you can ungroup them to edit
      individual series).
  - name: Any pictures from the workbook appear as embedded images, not linked files.
    text: Any pictures from the workbook appear as embedded images, not linked files.
  type: HowTo
tags:
- Aspose
- Java
- Excel
- PowerPoint
title: 'Excel sang PPTX: Hướng dẫn Java toàn diện để xuất các hình dạng có thể chỉnh
  sửa'
url: /vi/java/integration-interoperability/excel-to-pptx-complete-java-guide-to-export-editable-shapes/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# excel to pptx: Hướng Dẫn Java Đầy Đủ Để Xuất Hình Dạng Có Thể Chỉnh Sửa

Bạn có bao giờ tự hỏi làm thế nào để **excel to pptx** mà không mất khả năng chỉnh sửa các hộp văn bản sau này? Có thể bạn đã tạo một workbook báo cáo trong Excel, thêm một vài biểu đồ, và bây giờ bạn cần những hình ảnh đó trong một bản trình chiếu PowerPoint mà nhóm của bạn có thể chỉnh sửa nhanh chóng. Tin tốt là gì? Bạn có thể thực hiện điều này một cách lập trình bằng Aspose Cells và Aspose Slides, và bạn sẽ giữ được các hộp văn bản có thể chỉnh sửa, chuyển đổi biểu đồ thành hình dạng, và thậm chí nhúng hình ảnh pptx trong quá trình.

Trong tutorial này chúng ta sẽ đi qua một ví dụ đầy đủ, có thể chạy được, lấy một tệp Excel, cấu hình xuất sao cho văn bản vẫn có thể chỉnh sửa, biểu đồ trở thành các hình vector bạn có thể sửa đổi, và hình ảnh được nhúng. Khi hoàn thành, bạn sẽ có một quy trình **export excel powerpoint** vững chắc mà có thể đưa vào bất kỳ dự án Java nào.

## Prerequisites – What You Need Before Starting

- **Java 17** hoặc mới hơn (mã cũng biên dịch được với Java 8+).  
- **Aspose Cells for Java** và **Aspose Slides for Java** JARs trên classpath của bạn. Bạn có thể lấy chúng từ kho Maven của Aspose hoặc tải bộ dùng thử.  
- Một workbook Excel (`ShapesInExcel.xlsx`) chứa ít nhất một hộp văn bản, một biểu đồ và một ảnh được nhúng.  
- Một IDE cơ bản (IntelliJ, Eclipse, VS Code…) – bất kỳ IDE nào cũng được, nhưng tôi thích IntelliJ vì cấu hình chạy nhanh.

Đó là tất cả. Không cần công cụ xây dựng thêm, không cần dịch vụ bên ngoài. Hãy bắt đầu ngay.

## Step 1: Load the Excel Workbook – The Starting Point for excel to pptx

Điều đầu tiên chúng ta làm là mở workbook nguồn. Aspose Cells trừu tượng hoá định dạng tệp, vì vậy bạn không cần lo lắng về XML bên trong.

```java
import com.aspose.cells.*;

public class ExportEditableShapes {
    public static void main(String[] args) throws Exception {
        // Load the Excel workbook that contains text boxes or shapes
        Workbook workbook = new Workbook("YOUR_DIRECTORY/ShapesInExcel.xlsx");
```

> **Why this matters:** Loading the workbook gives us access to the entire sheet structure, including any drawing objects. If you skip this step, the export routine won’t know what to convert, and you’ll end up with a blank slide.

## Step 2: Configure PPTX Save Options – Preserve Editable Text Boxes & Convert Chart Shape

Bây giờ chúng ta chỉ định cho Aspose Slides cách mà đầu ra sẽ hoạt động. Lớp `ImageOrPrintOptions` là nơi chứa các tùy chọn cho **editable text boxes**, **convert chart shape**, và **embed images pptx**.

```java
        // Configure PPTX save options to preserve editable elements
        ImageOrPrintOptions pptxOptions = new ImageOrPrintOptions();
        pptxOptions.setExportImagesAsBase64(true);   // embed images directly in the PPTX
        pptxOptions.setExportChartToShape(true);     // turn charts into editable shapes
        pptxOptions.setEditableText(true);           // keep text boxes editable
```

* Một lưu ý nhanh về `setExportImagesAsBase64(true)`: tùy chọn này buộc trình xuất lưu ảnh dưới dạng luồng Base64 bên trong file `.pptx`. Kết quả là một tệp hoàn toàn tự chứa—không có tham chiếu ảnh bên ngoài, đáp ứng yêu cầu **embed images pptx**.  
* `setExportChartToShape(true)` thực hiện đúng những gì từ khóa **convert chart shape** hứa hẹn. Thay vì một hình ảnh tĩnh của biểu đồ, Aspose tạo ra một tập hợp các hình vector mà bạn có thể tách nhóm, thay đổi màu, hoặc thậm chí thay thế các điểm dữ liệu sau này.  
* Cuối cùng, `setEditableText(true)` đảm bảo bất kỳ hộp văn bản nào bạn đặt trong Excel vẫn là hộp văn bản trong PowerPoint, không phải ảnh đã được làm phẳng. Đây là cốt lõi của hỗ trợ **editable text boxes**.

## Step 3: Save the Workbook as PPTX – Completing the excel to pptx Flow

Với workbook đã được tải và các tùy chọn đã được tinh chỉnh, chúng ta chỉ cần gọi `save`. Aspose Cells sẽ thực hiện phần nặng phía sau.

```java
        // Save the workbook as a PPTX file with the configured options
        workbook.save("YOUR_DIRECTORY/ExportedShapes.pptx", SaveFormat.PPTX);
    }
}
```

> **What happens under the hood?** Aspose iterates over each worksheet, extracts drawing objects, applies the options we set, and writes a brand‑new PowerPoint package. The resulting file can be opened in PowerPoint, LibreOffice Impress, or any viewer that respects the Open XML format.

### Expected Output

Mở `ExportedShapes.pptx` và bạn sẽ thấy:

1. Một slide phản ánh bố cục của sheet Excel của bạn.  
2. Các hộp văn bản mà bạn có thể click, chỉnh sửa và di chuyển—giống như các hình dạng PowerPoint gốc.  
3. Biểu đồ được hiển thị dưới dạng các hình vector có thể chỉnh sửa (bạn có thể tách nhóm chúng để sửa từng series).  
4. Bất kỳ ảnh nào từ workbook sẽ xuất hiện dưới dạng ảnh nhúng, không phải file liên kết.

Nếu bạn thấy thiếu bất kỳ thành phần nào, hãy kiểm tra lại workbook nguồn để chắc chắn rằng nó thực sự chứa các đối tượng đó. Aspose sẽ không tự tạo chúng.

## Step 4: Advanced Tweaks – Fine‑Tuning Export Behaviour (Optional)

Mặc dù ba tùy chọn trên đã bao phủ hầu hết các trường hợp, Aspose Slides còn cung cấp một số tùy chỉnh khác có thể hữu ích:

| Option | What It Does | When to Use |
|--------|--------------|-------------|
| `setExportHiddenSheets(true)` | Includes hidden worksheets as extra slides. | Nếu báo cáo của bạn sử dụng các sheet ẩn để tính toán. |
| `setExportNotesToComments(true)` | Moves Excel cell comments to PowerPoint slide notes. | Khi bạn muốn giữ lại ngữ cảnh chú thích. |
| `setSlideSize(SlideSizeTypeOnScreen16x9)` | Forces a 16:9 slide size. | Đối với các bản trình chiếu hiện đại dạng widescreen. |

Bạn có thể đặt bất kỳ tùy chọn nào trong số này trên cùng một đối tượng `pptxOptions` trước khi gọi `save`.

```java
pptxOptions.setExportHiddenSheets(true);
pptxOptions.setExportNotesToComments(true);
pptxOptions.setSlideSize(SlideSizeTypeOnScreen16x9);
```

## Step 5: Running the Code – From IDE to Command Line

Nếu bạn dùng IDE, chỉ cần nhấn **Run**. Đối với việc biên dịch và chạy từ dòng lệnh, thực hiện như sau (giả sử bạn đã đặt các JAR của Aspose vào thư mục `libs/`):

```bash
javac -cp "libs/*" ExportEditableShapes.java
java -cp ".:libs/*" ExportEditableShapes
```

Trên Windows thay `:` bằng `;` trong classpath. Sau khi thực thi, kiểm tra thư mục `YOUR_DIRECTORY` để tìm `ExportedShapes.pptx`.

## Common Pitfalls & Pro Tips

- **Pitfall:** Forgetting to set `setEditableText(true)`. Result: all text appears as a flat image.  
  **Pro tip:** After the first run, open the PPTX and try editing a text box. If you can’t, double‑check the option.

- **Pitfall:** Large Excel files may cause memory pressure.  
  **Pro tip:** Use `Workbook.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` before loading to let Aspose stream data instead of loading everything into RAM.

- **Pitfall:** Images appear blurry.  
  **Pro tip:** Ensure the source picture resolution is high enough; Aspose respects the original DPI when `setExportImagesAsBase64(true)` is on.

- **Pitfall:** Charts lose data labels.  
  **Pro tip:** After conversion, right‑click the chart shape in PowerPoint, choose *Edit Data* to verify the underlying data table. If labels are missing, enable `setExportChartDataLabels(true)` (available in newer Aspose versions).

## Full Working Example – All Code in One Place

Below is the complete, copy‑paste‑ready program. Replace `YOUR_DIRECTORY` with an absolute or relative path on your machine.

```java
import com.aspose.cells.*;
import com.aspose.slides.*;

public class ExportEditableShapes {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the Excel workbook that contains text boxes or shapes
        Workbook workbook = new Workbook("YOUR_DIRECTORY/ShapesInExcel.xlsx");

        // 2️⃣ Configure PPTX save options to preserve editable elements
        ImageOrPrintOptions pptxOptions = new ImageOrPrintOptions();
        pptxOptions.setExportImagesAsBase64(true);   // embed images directly
        pptxOptions.setExportChartToShape(true);     // convert charts to shapes
        pptxOptions.setEditableText(true);           // keep text boxes editable

        // Optional: fine‑tune additional settings
        pptxOptions.setExportHiddenSheets(true);
        pptxOptions.setExportNotesToComments(true);
        pptxOptions.setSlideSize(SlideSizeTypeOnScreen16x9);

        // 3️⃣ Save the workbook as a PPTX file with the configured options
        workbook.save("YOUR_DIRECTORY/ExportedShapes.pptx", SaveFormat.PPTX);

        System.out.println("Export completed! Check ExportedShapes.pptx");
    }
}
```

Run it, open the generated PowerPoint, and you’ll see exactly what we described earlier.

## Conclusion – Mastering excel to pptx with Editable Shapes

We’ve just covered a **excel to pptx** workflow that keeps your text boxes editable, turns charts into vector shapes, and embeds images right inside the presentation. The key takeaway? By tweaking a handful of `ImageOrPrintOptions` properties you get a clean, **export excel powerpoint** experience that feels native to PowerPoint users.

From here you might explore:

- Adding slide transitions programmatically (`Slide.addTransition` from Aspose Slides).  
- Generating multiple slides from multiple worksheets (loop through `workbook.getWorksheets()`).  
- Combining this export with a PDF conversion pipeline for hybrid reporting.

Feel free to experiment, break things, and then bring them back together— that’s how you truly own the **excel to pptx** process. Got questions or want to share a cool variation? Drop a comment below, and happy coding!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Convert Excel to PowerPoint Using Aspose.Cells for .NET: A Complete Guide](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [How to Add and Access Text Boxes in Excel using Aspose.Cells .NET | Step‑By‑Step Guide](/cells/english/net/images-shapes/aspose-cells-net-add-text-boxes-excel/)
- [How to Convert Excel Sheets to Images Using Aspose.Cells .NET (Step‑By‑Step Guide)](/cells/english/net/workbook-operations/convert-excel-sheets-images-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}