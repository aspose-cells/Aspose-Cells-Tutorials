---
category: general
date: 2026-08-17
description: Tìm hiểu cách tạo các trang chi tiết trùng lặp với Aspose.Cells cho Java
  và cho phép tên trang trùng lặp bằng SmartMarkerProcessor.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create duplicate detail sheets
- allow duplicate sheet names
language: vi
lastmod: 2026-08-17
og_description: Tạo các sheet chi tiết trùng lặp trong Aspose.Cells cho Java và cho
  phép tên sheet trùng lặp. Hãy theo dõi hướng dẫn đầy đủ này để có kết quả ngay lập
  tức.
og_image_alt: Generated Excel workbook showing multiple detail sheets with the same
  name
og_title: Tạo các trang chi tiết trùng lặp trong Aspose.Cells cho Java – hướng dẫn
  từng bước
schemas:
- author: Aspose
  dateModified: '2026-08-17'
  description: Learn how to create duplicate detail sheets with Aspose.Cells for Java
    and allow duplicate sheet names using SmartMarkerProcessor.
  headline: How to create duplicate detail sheets in Aspose.Cells for Java
  type: TechArticle
- description: Learn how to create duplicate detail sheets with Aspose.Cells for Java
    and allow duplicate sheet names using SmartMarkerProcessor.
  name: How to create duplicate detail sheets in Aspose.Cells for Java
  steps:
  - name: Load the master template workbook.
    text: Load the master template workbook.
  - name: Configure `SmartMarkerProcessor` to **allow duplicate sheet names**.
    text: Configure `SmartMarkerProcessor` to **allow duplicate sheet names**.
  - name: Process the workbook so that a new detail sheet is created for each data
      group.
    text: Process the workbook so that a new detail sheet is created for each data
      group.
  - name: Save the resulting workbook that now contains duplicated detail sheets.
    text: Save the resulting workbook that now contains duplicated detail sheets.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Cách tạo các sheet chi tiết trùng lặp trong Aspose.Cells cho Java
url: /vi/java/worksheet-management/how-to-create-duplicate-detail-sheets-in-aspose-cells-for-ja/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách tạo các sheet chi tiết trùng lặp trong Aspose.Cells cho Java

Nếu bạn cần **tạo các sheet chi tiết trùng lặp** trong một workbook Excel, Aspose.Cells cho Java giúp thực hiện một cách đơn giản. Hướng dẫn này chỉ ra cách cho phép tên sheet trùng lặp khi tạo các sheet chi tiết bằng SmartMarkerProcessor, để bạn có thể tạo một workbook chứa nhiều sheet có cùng tên.

Bạn sẽ thấy một ví dụ đầy đủ, có thể chạy được, phân tích từng tùy chọn cấu hình, và các mẹo để xử lý các trường hợp đặc biệt thường gặp như xung đột tên và tập dữ liệu lớn. Không cần tham chiếu bên ngoài—mọi thứ bạn cần đều có trong mã dưới đây.

## Yêu cầu trước

Trước khi bắt đầu, hãy đảm bảo bạn có:

* Java Development Kit (JDK) 8 hoặc mới hơn.
* Maven hoặc Gradle để quản lý phụ thuộc.
* Thư viện Aspose.Cells cho Java (phiên bản 23.9 hoặc mới hơn). Thêm phụ thuộc Maven sau vào tệp `pom.xml` của bạn:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
</dependency>
```

* Một workbook mẫu master (`master_template.xlsx`) chứa một vùng Smart Marker cho dữ liệu chi tiết.

## Tổng quan về giải pháp

Giải pháp bao gồm bốn bước logic:

1. Tải workbook mẫu master.
2. Cấu hình `SmartMarkerProcessor` để **cho phép tên sheet trùng lặp**.
3. Xử lý workbook để tạo một sheet chi tiết mới cho mỗi nhóm dữ liệu.
4. Lưu workbook kết quả, hiện chứa các sheet chi tiết đã được sao chép.

Mỗi bước được giải thích chi tiết bên dưới, và tệp nguồn đầy đủ được cung cấp ở cuối hướng dẫn.

## Bước 1: Tải workbook mẫu master

Hoạt động đầu tiên tạo một thể hiện `Workbook` đại diện cho tệp mẫu. Mẫu phải chứa một placeholder Smart Marker (ví dụ, `&=DetailData`) để chỉ định cho bộ xử lý vị trí chèn dữ liệu.

```java
import com.aspose.cells.*;

public class DuplicateDetailSheet {
    public static void main(String[] args) throws Exception {
        // Load the master template workbook from the file system
        Workbook workbook = new Workbook("YOUR_DIRECTORY/master_template.xlsx");
```

**Tại sao điều này quan trọng:** Việc tải mẫu tách riêng bố cục và định dạng khỏi logic tạo dữ liệu, giúp mã của bạn sạch sẽ và dễ tái sử dụng cùng một mẫu cho các tập dữ liệu khác nhau.

## Bước 2: Cấu hình SmartMarkerProcessor để cho phép tên sheet trùng lặp

Mặc định, Aspose.Cells tạo ra các tên sheet duy nhất khi tạo các sheet chi tiết. Để **cho phép tên sheet trùng lặp**, đặt tùy chọn `DetailSheetNewName` thành một giá trị cố định. Bộ xử lý sẽ tái sử dụng tên này cho mỗi sheet được tạo.

```java
        // Create a SmartMarkerProcessor instance
        SmartMarkerProcessor processor = new SmartMarkerProcessor();

        // Enable duplicate detail sheet names by assigning a fixed name
        processor.getOptions().setDetailSheetNewName("DetailSheet");

        // Optional: if you want to keep the original sheet after processing, set this flag
        // processor.getOptions().setKeepOriginalDetailSheet(true);
```

**Tại sao điều này quan trọng:** Đặt `DetailSheetNewName` cho phép engine tái sử dụng cùng một tên cho mọi sheet chi tiết, đáp ứng trực tiếp yêu cầu **cho phép tên sheet trùng lặp**. Cách này hữu ích khi các công cụ downstream xác định sheet dựa trên vị trí thay vì tên.

## Bước 3: Xử lý workbook để tạo các sheet chi tiết

Sau khi cấu hình, gọi `process` trên workbook. Bộ xử lý sẽ đọc vùng Smart Marker, tạo một sheet mới cho mỗi nhóm dữ liệu và điền dữ liệu vào các hàng tương ứng.

```java
        // Process the workbook; this creates the duplicate detail sheets
        processor.process(workbook);
```

**Tại sao điều này quan trọng:** Lệnh `process` thực hiện phần công việc nặng—phân tích Smart Markers, sao chép sheet mẫu và chèn dữ liệu. Vì tùy chọn `DetailSheetNewName` đã được đặt, mỗi sheet mới sẽ nhận cùng một tên, tạo ra các tên sheet trùng lặp trong tệp cuối cùng.

## Bước 4: Lưu workbook kết quả

Cuối cùng, ghi workbook đã chỉnh sửa vào một tệp mới. Tệp đầu ra sẽ chứa số tab “DetailSheet” tương ứng với số nhóm dữ liệu.

```java
        // Save the workbook with duplicated detail sheets
        workbook.save("YOUR_DIRECTORY/duplicate_detail.xlsx");
    }
}
```

**Tại sao điều này quan trọng:** Lưu tệp hoàn thiện các thay đổi do bộ xử lý thực hiện. Workbook kết quả có thể mở bằng Microsoft Excel, LibreOffice hoặc bất kỳ ứng dụng bảng tính nào hỗ trợ định dạng XLSX.

## Mã nguồn đầy đủ

Kết hợp tất cả các phần lại, đây là chương trình đầy đủ mà bạn có thể sao chép, dán và chạy:

```java
import com.aspose.cells.*;

public class DuplicateDetailSheet {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the master template workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/master_template.xlsx");

        // Step 2: Create a SmartMarkerProcessor and allow duplicate detail sheet names
        SmartMarkerProcessor processor = new SmartMarkerProcessor();
        processor.getOptions().setDetailSheetNewName("DetailSheet"); // same name allowed for each detail sheet

        // Step 3: Process the workbook to generate the detail sheets
        processor.process(workbook);

        // Step 4: Save the resulting workbook with duplicated detail sheets
        workbook.save("YOUR_DIRECTORY/duplicate_detail.xlsx");
    }
}
```

### Kết quả mong đợi

Khi bạn mở `duplicate_detail.xlsx`, bạn sẽ thấy nhiều tab có tên **DetailSheet**. Mỗi tab chứa tập dữ liệu tương ứng với một nhóm Smart Marker cụ thể trong mẫu. Bố cục, định dạng và công thức từ mẫu master được giữ nguyên trên mỗi sheet trùng lặp.

## Xử lý các vấn đề thường gặp

| Vấn đề | Giải thích | Cách khắc phục |
|-------|-------------|--------|
| Excel hiển thị cảnh báo về tên sheet trùng lặp | Excel cho phép tên trùng lặp nhưng có thể hiển thị cảnh báo khi mở tệp. | Cảnh báo không gây hại; workbook hoạt động bình thường. Nếu muốn tắt cảnh báo, hãy đổi tên sheet sau khi xử lý bằng `Workbook.getWorksheets().get(i).setName("DetailSheet" + i);`. |
| Tập dữ liệu lớn gây sử dụng bộ nhớ cao | Mỗi sheet trùng lặp tạo một bản sao đầy đủ của mẫu, có thể tiêu tốn RAM. | Bật chế độ streaming với `Workbook.setMemorySetting(MemorySetting.MEMORY_PREFERENCE);` trước khi tải mẫu. |
| Không tìm thấy vùng Smart Marker | Bộ xử lý không thể xác định `&=DetailData` trong mẫu. | Kiểm tra cú pháp placeholder có khớp với nguồn dữ liệu và sheet mẫu không bị ẩn. |

## Mẹo chuyên nghiệp: tùy chỉnh scheme đặt tên trùng lặp

Nếu bạn cần một mẫu đặt tên có thể dự đoán trong khi vẫn cho phép trùng lặp, hãy kết hợp tên cơ sở với chỉ mục:

```java
processor.getOptions().setDetailSheetNewName("DetailSheet_{0}");
```

Placeholder `{0}` sẽ được thay thế bằng chỉ mục của sheet, tạo ra các tên như `DetailSheet_1`, `DetailSheet_2`, v.v. Điều này vẫn đáp ứng yêu cầu **cho phép tên sheet trùng lặp** vì tên cơ sở vẫn không thay đổi.

## Các bước tiếp theo

Bây giờ bạn đã có thể **tạo các sheet chi tiết trùng lặp**, bạn có thể khám phá các chủ đề sau:

* **Điền hình ảnh vào sheet chi tiết** – sử dụng các đối tượng `Picture` để nhúng logo hoặc biểu đồ.
* **Áp dụng định dạng có điều kiện** – thêm các quy tắc `FormatCondition` để làm nổi bật các hàng dựa trên giá trị.
* **Xuất ra PDF** – gọi `workbook.save("output.pdf", SaveFormat.PDF);` để tạo phiên bản PDF của các sheet đã được sao chép.

Mỗi phần mở rộng này dựa trên cùng quy trình Smart Marker được trình bày ở đây, cho phép bạn tự động hoá các nhiệm vụ báo cáo Excel phức tạp một cách tự tin.

---

*Bạn đã học cách tạo các sheet chi tiết trùng lặp trong Aspose.Cells cho Java và cách cho phép tên sheet trùng lặp bằng SmartMarkerProcessor. Áp dụng mã, điều chỉnh mẫu, và tích hợp kỹ thuật này vào quy trình báo cáo của bạn.*

## Bạn nên học gì tiếp theo?

Các hướng dẫn sau đây bao gồm các chủ đề liên quan chặt chẽ, dựa trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh với giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Create & Access Excel Sheets, Add PDF Bookmarks Using Aspose.Cells for Java](/cells/english/java/workbook-operations/create-access-excel-sheets-add-pdf-bookmarks-aspose-cells-java/)
- [Create Access Excel Sheets Add Pdf Bookmarks Aspose Cells Java](/cells/german/java/workbook-operations/create-access-excel-sheets-add-pdf-bookmarks-aspose-cells-java/)
- [Create Access Excel Sheets Add Pdf Bookmarks Aspose Cells Java](/cells/french/java/workbook-operations/create-access-excel-sheets-add-pdf-bookmarks-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}