---
category: general
date: 2026-06-08
description: Tìm hiểu cách chuyển đổi XLSX sang PPTX và giữ cho các hình dạng có thể
  chỉnh sửa bằng Aspose. Mã Java từng bước cho thấy cách xuất các hình dạng mà không
  mất khả năng chỉnh sửa.
draft: false
keywords:
- convert xlsx to pptx
- how to export shapes
- how to keep shapes
- aspose export pptx
language: vi
og_description: Chuyển đổi XLSX sang PPTX đồng thời giữ nguyên khả năng chỉnh sửa
  hình dạng. Hướng dẫn này sẽ đưa bạn qua mã Java và giải thích cách giữ lại các hình
  dạng bằng Aspose.
og_title: Chuyển đổi XLSX sang PPTX – Xuất các hình dạng có thể chỉnh sửa với Aspose
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Learn how to convert XLSX to PPTX and keep shapes editable using Aspose.
    Step‑by‑step Java code shows how to export shapes without losing editability.
  headline: Convert XLSX to PPTX – Complete Guide to Export Editable Shapes
  type: TechArticle
- description: Learn how to convert XLSX to PPTX and keep shapes editable using Aspose.
    Step‑by‑step Java code shows how to export shapes without losing editability.
  name: Convert XLSX to PPTX – Complete Guide to Export Editable Shapes
  steps:
  - name: Expected Output
    text: '- A PowerPoint file named `editable.pptx` located in the directory you
      specified. - Each worksheet appears as a separate slide. - All shapes (text
      boxes, arrows, charts) remain fully editable, just as they were in Excel.'
  - name: 1. Shapes Turn Into Images
    text: '> **Symptom:** After conversion, clicking a shape shows no resize handles.'
  - name: 2. Missing Slides for Some Worksheets
    text: '> **Symptom:** Only the first sheet appears in the PPTX.'
  - name: 3. File Not Found Exceptions
    text: '> **Symptom:** Java throws `FileNotFoundException` for the source Excel.'
  - name: Wrap‑Up
    text: We’ve walked through the entire process of **convert xlsx to pptx**, showing
      exactly **how to export shapes** and **how to keep shapes** editable using the
      Aspose API. The complete Java program is ready to drop into any Maven project,
      and the optional tweaks let you tailor the conversion to your exa
  type: HowTo
- questions:
  - answer: Yes, you could use OpenXML SDK, but you’d lose the high‑level shape preservation
      that Aspose handles automatically.
    question: Can I convert XLSX to PPTX without Aspose?
  - answer: The conversion strips out VBA; only visual elements are transferred. If
      you need macro logic in PowerPoint, you’ll have to recreate it manually.
    question: Does this work with macros or VBA code inside the workbook?
  - answer: Aspose processes them efficiently, but memory usage can spike. Consider
      converting sheet‑by‑sheet or increasing the JVM heap (`-Xmx2g`).
    question: What about large workbooks with hundreds of shapes?
  type: FAQPage
tags:
- Aspose.Cells
- Aspose.Slides
- Java
- File Conversion
title: Chuyển đổi XLSX sang PPTX – Hướng dẫn toàn diện về xuất các hình dạng có thể
  chỉnh sửa
url: /vi/java/excel-import-export/convert-xlsx-to-pptx-complete-guide-to-export-editable-shape/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Chuyển đổi XLSX sang PPTX – Hướng dẫn toàn diện để xuất các hình dạng có thể chỉnh sửa

Bạn đã bao giờ tự hỏi làm thế nào để **convert XLSX to PPTX** mà không biến các biểu đồ và sơ đồ đẹp mắt của mình thành hình ảnh phẳng chưa? Bạn không phải là người duy nhất. Nhiều nhà phát triển gặp khó khăn khi cần một bộ PowerPoint vẫn cho phép người nhận chỉnh sửa các hình dạng, thay đổi kích thước hộp văn bản hoặc điều chỉnh các kết nối. Tin tốt là gì? Aspose làm cho việc này trở nên dễ dàng, và trong tutorial này chúng tôi sẽ chỉ cho bạn **cách xuất các hình dạng** và **cách giữ các hình dạng** có thể chỉnh sửa trong quá trình chuyển đổi.

Chúng tôi sẽ đi qua một ví dụ thực tế bằng Java, tải một workbook Excel, bật tùy chọn đúng và ghi ra một tệp PPTX mà bạn có thể mở trong PowerPoint và chỉnh sửa ngay lập tức. Khi kết thúc, bạn sẽ biết không chỉ *cái gì* để gọi, mà còn *tại sao* mỗi cài đặt lại quan trọng, cùng một vài mẹo để tránh những bẫy thường gặp.

## Prerequisites – Những gì bạn cần trước khi bắt đầu

Trước khi chúng ta đi vào mã, hãy chắc chắn rằng bạn đã có những thứ sau trên máy:

- **Java Development Kit (JDK) 8 hoặc mới hơn** – mã sẽ biên dịch với bất kỳ JDK hiện đại nào.
- **Aspose.Cells for Java** và **Aspose.Slides for Java** JARs – bạn có thể lấy chúng từ kho Maven của Aspose hoặc tải phiên bản mới nhất từ trang web Aspose.
- Một **tệp Excel (`shapes.xlsx`)** chứa các hình dạng bạn muốn giữ lại. Một workbook đơn giản với vài đối tượng vẽ là đủ để thử nghiệm.
- IDE yêu thích của bạn (IntelliJ IDEA, Eclipse, VS Code…) hoặc chỉ một trình soạn thảo văn bản và một terminal.

Nếu bất kỳ mục nào ở trên nghe lạ, đừng hoảng. Cài đặt các JAR chỉ cần thêm hai dependency vào `pom.xml` của bạn:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- check for the latest -->
</dependency>
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-slides</artifactId>
    <version>23.12</version>
</dependency>
```

Bây giờ chúng ta đã bao quát các kiến thức cơ bản, hãy bắt tay vào thực hành.

## Step 1: Load the Excel Workbook Containing the Shapes

Điều đầu tiên bạn cần làm là đọc tệp `.xlsx` chứa các đối tượng vector. Aspose.Cells ẩn đi các chi tiết OpenXML cấp thấp, vì vậy bạn chỉ cần khởi tạo một `Workbook`.

```java
import com.aspose.cells.*;

public class ExportEditableShapes {
    public static void main(String[] args) throws Exception {
        // Load the source workbook – replace the path with your actual file location
        Workbook workbook = new Workbook("YOUR_DIRECTORY/shapes.xlsx");
        // From here on we can manipulate the workbook or pass it straight to Slides
```

> **Why this matters:** Việc tải workbook đúng cách đảm bảo bất kỳ đối tượng vẽ nhúng nào (biểu đồ, SmartArt, hình dạng vẽ tự do) được giữ trong bộ nhớ dưới dạng các đối tượng gốc của Aspose. Nếu bỏ qua bước này hoặc dùng một luồng tệp chung, engine chuyển đổi có thể xử lý sheet như một hình ảnh tĩnh, mất khả năng chỉnh sửa.

## Step 2: Tell Aspose to Keep Shapes Editable

Aspose.Slides cung cấp một flag gọi là `setSaveEditableShape`. Khi đặt thành `true`, thư viện sẽ giữ lại dữ liệu hình dạng gốc thay vì raster hoá chúng. Đây là phần **how to keep shapes** trong tutorial của chúng ta.

```java
        // Create save options for PPTX output
        ImageOrPrintOptions pptxSaveOptions = new ImageOrPrintOptions();

        // Enable editable shape preservation – this is the key switch
        pptxSaveOptions.setSaveEditableShape(true);
```

> **Pro tip:** Giá trị mặc định của `SaveEditableShape` là `false`. Quên bật flag này là lý do phổ biến nhất khiến các nhà phát triển nhận được một PPTX đầy ảnh phẳng. Hãy kiểm tra lại dòng này nếu kết quả của bạn trông “bị kẹt”.

## Step 3: Convert and Save the Workbook as PPTX

Bây giờ chúng ta gọi phương thức `save`, truyền enum `SaveFormat.PPTX` và các tùy chọn tùy chỉnh của chúng ta. Đây là phần cốt lõi của **convert xlsx to pptx**.

```java
        // Save the workbook as a PPTX file with editable shapes preserved
        workbook.save("YOUR_DIRECTORY/editable.pptx", SaveFormat.PPTX, pptxSaveOptions);
    }
}
```

Khi bạn chạy chương trình, Aspose sẽ đọc sheet Excel, chuyển mỗi worksheet thành một slide, và ghi tệp vào `editable.pptx`. Mở tệp này trong PowerPoint và bạn sẽ thấy các hình dạng gốc vẫn nguyên vẹn—sẵn sàng di chuyển, thay đổi màu hoặc thay đổi kích thước.

### Expected Output

- Một tệp PowerPoint có tên `editable.pptx` nằm trong thư mục bạn chỉ định.
- Mỗi worksheet xuất hiện dưới dạng một slide riêng.
- Tất cả các hình dạng (hộp văn bản, mũi tên, biểu đồ) vẫn hoàn toàn có thể chỉnh sửa, giống như trong Excel.

Nếu bạn mở PPTX và cố gắng chỉnh sửa một hình dạng, bạn sẽ thấy các tay cầm giống như khi bạn tạo một hình dạng mới trong PowerPoint.

## Common Pitfalls and How to Avoid Them

### 1. Shapes Turn Into Images

> **Symptom:** Sau khi chuyển đổi, khi nhấp vào một hình dạng không có tay cầm thay đổi kích thước.

**Cause:** `setSaveEditableShape(false)` (giá trị mặc định) hoặc dùng phiên bản Aspose cũ không hỗ trợ flag này.

**Fix:** Đảm bảo bạn gọi `pptxSaveOptions.setSaveEditableShape(true);` *trước* khi gọi `save`, và xác nhận bạn đang dùng Aspose.Cells/Slides phiên bản 23.x trở lên.

### 2. Missing Slides for Some Worksheets

> **Symptom:** Chỉ sheet đầu tiên xuất hiện trong PPTX.

**Cause:** Workbook được lưu với các worksheet ẩn, hoặc `SaveOptions` được cấu hình không đúng.

**Fix:** Sử dụng `workbook.getWorksheets().setVisible(true);` để chắc chắn mọi sheet đều hiển thị, hoặc điều chỉnh `LoadOptions` nếu bạn đang tải một tệp có bảo mật bằng mật khẩu.

### 3. File Not Found Exceptions

> **Symptom:** Java ném `FileNotFoundException` cho tệp Excel nguồn.

**Cause:** Đường dẫn không đúng hoặc thiếu quyền truy cập tệp.

**Fix:** Dùng đường dẫn tuyệt đối hoặc đặt tệp vào thư mục `resources` của dự án và tải nó qua `getClass().getResourceAsStream("/shapes.xlsx")`.

## Advanced: Converting Specific Sheets Only

Đôi khi bạn không cần chuyển đổi toàn bộ workbook—có thể chỉ muốn sheet “Dashboard” trở thành một slide. Đây là một chỉnh sửa nhanh:

```java
        // Create a new workbook that contains only the desired sheet
        Workbook source = new Workbook("YOUR_DIRECTORY/shapes.xlsx");
        int sheetIndex = source.getWorksheets().get("Dashboard").getIndex();

        // Clone the target sheet into a fresh workbook
        Workbook singleSheet = new Workbook();
        singleSheet.getWorksheets().addCopy(source.getWorksheets().get(sheetIndex));

        // Save the single‑sheet workbook as PPTX
        singleSheet.save("YOUR_DIRECTORY/dashboard.pptx", SaveFormat.PPTX, pptxSaveOptions);
```

Đoạn mã này minh họa **cách xuất các hình dạng** từ một worksheet duy nhất trong khi vẫn giữ khả năng chỉnh sửa.

## Step‑by‑Step Recap (Quick Reference)

| Bước | Hành động | API chính |
|------|-----------|-----------|
| 1 | Tải `.xlsx` | `new Workbook(path)` |
| 2 | Bật hình dạng có thể chỉnh sửa | `pptxSaveOptions.setSaveEditableShape(true)` |
| 3 | Lưu dưới dạng PPTX | `workbook.save(pptPath, SaveFormat.PPTX, pptxSaveOptions)` |

Có bảng này bên tay sẽ giúp bạn tiết kiệm thời gian khi quay lại mã sau này.

## Testing the Result

Sau khi chạy chương trình, mở `editable.pptx` trong PowerPoint và:

1. Nhấp vào bất kỳ hình dạng nào – bạn sẽ thấy khung bao chuẩn.
2. Thử thay đổi màu nền – nó sẽ cập nhật ngay lập tức.
3. Di chuyển hình dạng đến vị trí mới – PowerPoint sẽ giữ lại tọa độ mới.

Nếu cả ba hành động đều hoạt động, bạn đã **convert xlsx to pptx** thành công đồng thời giữ các hình dạng có thể chỉnh sửa. Nếu có gì không ổn, hãy kiểm tra lại flag `setSaveEditableShape` và xác nhận phiên bản Aspose của bạn.

## Frequently Asked Questions

- **Can I convert XLSX to PPTX without Aspose?**  
  Có, bạn có thể dùng OpenXML SDK, nhưng sẽ mất khả năng bảo tồn hình dạng cấp cao mà Aspose tự động xử lý.

- **Does this work with macros or VBA code inside the workbook?**  
  Quá trình chuyển đổi sẽ loại bỏ VBA; chỉ các yếu tố trực quan được chuyển. Nếu bạn cần logic macro trong PowerPoint, sẽ phải tự tạo lại thủ công.

- **What about large workbooks with hundreds of shapes?**  
  Aspose xử lý chúng hiệu quả, nhưng việc sử dụng bộ nhớ có thể tăng đột biến. Hãy cân nhắc chuyển đổi từng sheet hoặc tăng kích thước heap JVM (`-Xmx2g`).

## Next Steps – Nâng cao kỹ năng chuyển đổi của bạn

Bây giờ bạn đã nắm vững các kiến thức cơ bản của **convert xlsx to pptx** với các đối tượng có thể chỉnh sửa, bạn có thể khám phá:

- **Embedding videos or audio** bằng các API media của Aspose.Slides.
- **Applying slide themes** một cách lập trình để tạo phong cách đồng nhất cho bộ slide.
- **Batch converting multiple workbooks** bằng một vòng lặp đơn giản—lý tưởng cho các pipeline báo cáo tự động.
- **Exporting to other formats** như PDF hoặc HTML trong khi vẫn bảo tồn dữ liệu hình dạng (`SaveFormat.PDF` với các tùy chọn tương tự).

Mỗi chủ đề này dựa trên các khái niệm cốt lõi mà chúng ta đã đề cập, vì vậy bạn sẽ thấy đường cong học tập nhẹ nhàng.

---

![sơ đồ chuyển đổi xlsx sang pptx](image.png "Sơ đồ hiển thị bảng Excel → chuyển đổi Aspose → PPTX có thể chỉnh sửa")

*Image alt text: “sơ đồ quy trình chuyển đổi xlsx sang pptx”*

---

### Wrap‑Up

Chúng tôi đã đi qua toàn bộ quy trình **convert xlsx to pptx**, chỉ ra chính xác **cách xuất các hình dạng** và **cách giữ các hình dạng** có thể chỉnh sửa bằng API của Aspose. Chương trình Java hoàn chỉnh đã sẵn sàng để đưa vào bất kỳ dự án Maven nào, và các tùy chỉnh tùy chọn cho phép bạn điều chỉnh chuyển đổi theo nhu cầu cụ thể. Hãy thử, khám phá các sheet khác nhau, và để sức mạnh của Aspose xử lý phần công việc nặng nhọc.

Nếu gặp bất kỳ khó khăn nào, hãy kiểm tra tài liệu Aspose để biết các thuộc tính `ImageOrPrintOptions` mới nhất, hoặc để lại bình luận bên dưới. Chúc bạn lập trình vui vẻ, và tận hưởng tự do của các bộ PowerPoint có thể chỉnh sửa được tạo trực tiếp từ Excel!

## What Should You Learn Next?

Các tutorial sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật đã trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm mã mẫu hoàn chỉnh cùng giải thích chi tiết từng bước, giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Cách chuyển đổi Excel sang PDF trong Java bằng Aspose.Cells: Hướng dẫn từng bước](/cells/english/java/workbook-operations/convert-excel-to-pdf-aspose-cells-java/)
- [Chuyển đổi SmartArt thành Nhóm Hình trong Java sử dụng Aspose.Cells: Hướng dẫn toàn diện](/cells/english/java/images-shapes/convert-smartart-group-shapes-java/)
- [Cách Thêm và Định dạng Hình dạng trong Excel bằng Aspose.Cells Java](/cells/english/java/images-shapes/aspose-cells-java-add-styling-shapes-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}