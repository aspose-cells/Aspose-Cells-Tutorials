---
category: general
date: 2026-11-16
description: Cách sao chép ô giữa các workbook Excel trong Java – tải một workbook,
  sao chép phạm vi giữa các workbook (bao gồm cả bảng pivot), và lưu tệp workbook.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy cells
- copy range between workbooks
- copy pivot table workbook
- save workbook file
- load excel workbook java
language: vi
lastmod: 2026-11-16
og_description: Cách sao chép ô giữa các workbook Excel trong Java. Học cách tải một
  workbook Excel, sao chép một phạm vi (bao gồm cả bảng tổng hợp) giữa các workbook
  và lưu tệp workbook.
og_image_alt: Screenshot of Java code copying a cell range from one Excel workbook
  to another
og_title: Cách sao chép ô giữa các workbook Excel trong Java – hướng dẫn đầy đủ
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: How to copy cells between Excel workbooks in Java – load a workbook,
    copy range between workbooks (including a pivot table), and save the workbook
    file.
  headline: How to copy cells between Excel workbooks in Java
  type: TechArticle
- description: How to copy cells between Excel workbooks in Java – load a workbook,
    copy range between workbooks (including a pivot table), and save the workbook
    file.
  name: How to copy cells between Excel workbooks in Java
  steps:
  - name: Load the source workbook
    text: '```java import com.aspose.cells.*;'
  - name: Define the range that includes the pivot table
    text: '```java // Define the cell range that you want to copy. // Adjust "A1:G20"
      to match the area that contains your data/pivot table. Range srcRange = srcWs.getCells().createRange("A1:G20");
      ```'
  - name: Create the destination workbook
    text: '```java // Create a new, empty workbook that will receive the copied range.
      Workbook destWb = new Workbook(); // defaults to a single empty sheet Worksheet
      destWs = destWb.getWorksheets().get(0); ```'
  - name: Copy the range to the destination workbook
    text: '```java // Copy the source range to cell A1 of the destination worksheet.
      destWs.getCells().copyRange(srcRange, destWs.getCells().get("A1")); ```'
  - name: Save the destination workbook
    text: '```java // Save the new workbook to disk. destWb.save("YOUR_DIRECTORY/dest.xlsx");
      } } ```'
  type: HowTo
tags:
- Java
- Excel
- Aspose.Cells
- Workbook manipulation
title: Cách sao chép các ô giữa các workbook Excel trong Java
url: /vi/java/workbook-operations/how-to-copy-cells-between-excel-workbooks-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách sao chép ô giữa các workbook Excel trong Java

Nếu bạn cần **copy cells** từ một Excel workbook sang một workbook khác bằng Java, hướng dẫn này sẽ cho bạn một cách đáng tin cậy để thực hiện. Bạn sẽ học cách **load Excel workbook Java**, sao chép một phạm vi có thể chứa pivot table, và cuối cùng **save workbook file** với dữ liệu đã sao chép.

Bài hướng dẫn này bao gồm:

* Tải workbook nguồn và chọn một worksheet.  
* Xác định phạm vi chính xác bạn muốn di chuyển (bao gồm cả pivot table).  
* Tạo workbook đích và sao chép phạm vi.  
* Lưu file đích.  

Ví dụ sử dụng thư viện Aspose.Cells for Java, cho phép làm việc với các file Excel mà không cần Microsoft Office. Mã chạy trên Java 8+ và bất kỳ IDE hiện đại nào (IntelliJ IDEA, Eclipse, VS Code, v.v.).

---

## Yêu cầu trước

Trước khi bắt đầu, hãy chắc chắn rằng bạn có:

| Yêu cầu | Lý do |
|---------|-------|
| Java Development Kit (JDK) 8 or newer | Cần thiết để biên dịch và chạy mã. |
| Maven or Gradle build tool | Đơn giản hoá việc thêm phụ thuộc Aspose.Cells. |
| Aspose.Cells for Java library (latest version) | Cung cấp các lớp `Workbook`, `Worksheet`, và `Range` được sử dụng trong ví dụ. |
| Two Excel files (`source.xlsx` và một thư mục trống cho `dest.xlsx`) | File nguồn phải chứa dữ liệu và, tùy chọn, một pivot table bạn muốn sao chép. |

Thêm phụ thuộc Aspose.Cells vào `pom.xml` (Maven) hoặc `build.gradle` (Gradle). Ví dụ cho Maven:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- use the latest version -->
</dependency>
```

---

## Cách sao chép ô với Aspose.Cells

Các bước sau sẽ hướng dẫn bạn qua toàn bộ quy trình. Mỗi bước bao gồm mã Java, giải thích **tại sao** bước đó quan trọng, và một mẹo để tránh các lỗi thường gặp.

### Bước 1: Tải workbook nguồn

```java
import com.aspose.cells.*;

public class ExcelCopyDemo {
    public static void main(String[] args) throws Exception {
        // Load the source Excel file (replace with your actual path)
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/source.xlsx");

        // Get the first worksheet (index 0)
        Worksheet srcWs = srcWb.getWorksheets().get(0);
```

**Tại sao?**  
`Workbook` đại diện cho toàn bộ file Excel. Việc tải nó cho phép bạn truy cập tất cả các worksheet, ô và các đối tượng như pivot table. Sử dụng worksheet đầu tiên là phổ biến, nhưng bạn có thể chọn bất kỳ sheet nào bằng tên (`srcWb.getWorksheets().get("Sheet2")`).

**Mẹo chuyên nghiệp:**  
Nếu file nguồn lớn, hãy cân nhắc tải nó ở chế độ *memory‑efficient*: `new Workbook("file.xlsx", new LoadOptions(LoadFormat.XLSX) {{ setMemorySetting(MemorySetting.MEMORY_PREFERENCE); }});`

### Bước 2: Xác định phạm vi bao gồm pivot table

```java
        // Define the cell range that you want to copy.
        // Adjust "A1:G20" to match the area that contains your data/pivot table.
        Range srcRange = srcWs.getCells().createRange("A1:G20");
```

**Tại sao?**  
Đối tượng `Range` đại diện cho một khối hình chữ nhật các ô. Bằng cách chỉ định `"A1:G20"` bạn cho Aspose.Cells biết chính xác những ô nào—bao gồm bất kỳ pivot table nào được nhúng—để sao chép. Thư viện tự động sao chép dữ liệu nền, kiểu dáng và định nghĩa pivot.

**Trường hợp đặc biệt:**  
Nếu pivot table mở rộng ra ngoài phạm vi đã định, hãy mở rộng địa chỉ (ví dụ, `"A1:Z100"`). Bạn cũng có thể sử dụng `srcWs.getCells().getMaxDataColumn()` và `getMaxDataRow()` để tính toán vùng dữ liệu đã sử dụng một cách động.

### Bước 3: Tạo workbook đích

```java
        // Create a new, empty workbook that will receive the copied range.
        Workbook destWb = new Workbook();               // defaults to a single empty sheet
        Worksheet destWs = destWb.getWorksheets().get(0);
```

**Tại sao?**  
Một workbook mới đảm bảo không có định dạng không mong muốn hoặc các sheet ẩn can thiệp vào nội dung đã sao chép. Workbook mặc định đã chứa một worksheet, chúng ta sẽ dùng nó làm đích.

### Bước 4: Sao chép phạm vi vào workbook đích

```java
        // Copy the source range to cell A1 of the destination worksheet.
        destWs.getCells().copyRange(srcRange, destWs.getCells().get("A1"));
```

**Tại sao?**  
`copyRange` xử lý tất cả các thuộc tính của ô: giá trị, công thức, định dạng và thậm chí cache của pivot. Bằng cách sao chép tới `"A1"` bạn đặt phạm vi ở góc trên‑trái của sheet đích, giữ nguyên bố cục gốc.

**Câu hỏi thường gặp:** *Pivot table có vẫn hoạt động không?*  
Có. Aspose.Cells sao chép định nghĩa pivot table và cache của nó, vì vậy pivot hoạt động chính xác như trong workbook nguồn.

### Bước 5: Lưu workbook đích

```java
        // Save the new workbook to disk.
        destWb.save("YOUR_DIRECTORY/dest.xlsx");
    }
}
```

**Tại sao?**  
Gọi `save` ghi workbook trong bộ nhớ ra file `.xlsx` thực tế. Bạn cũng có thể lưu sang các định dạng khác (`.xls`, `.csv`, `.pdf`) bằng cách thay đổi phần mở rộng file hoặc sử dụng `SaveOptions`.

**Mẹo:**  
Nếu bạn cần truyền file dưới dạng stream tới phản hồi web, hãy dùng `destWb.save(OutputStream, SaveFormat.XLSX);` thay vì đường dẫn file.

---

## Sao chép phạm vi giữa các workbook – mã nguồn đầy đủ

Dưới đây là lớp Java đầy đủ, sẵn sàng để chạy. Thay `YOUR_DIRECTORY` bằng thư mục thực tế trên máy của bạn.

```java
import com.aspose.cells.*;

public class ExcelCopyDemo {
    public static void main(String[] args) throws Exception {
        // Load the source workbook
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/source.xlsx");
        Worksheet srcWs = srcWb.getWorksheets().get(0);

        // Define the range that includes the data and pivot table
        Range srcRange = srcWs.getCells().createRange("A1:G20");

        // Create a new destination workbook
        Workbook destWb = new Workbook();
        Worksheet destWs = destWb.getWorksheets().get(0);

        // Copy the defined range to the destination workbook
        destWs.getCells().copyRange(srcRange, destWs.getCells().get("A1"));

        // Save the destination workbook
        destWb.save("YOUR_DIRECTORY/dest.xlsx");
    }
}
```

**Kết quả mong đợi:**  
`dest.xlsx` chứa một bản sao chính xác của phạm vi `A1:G20` từ `source.xlsx`. Nếu phạm vi nguồn chứa pivot table, file đích sẽ hiển thị cùng một pivot với nguồn dữ liệu được liên kết đúng với các ô đã sao chép.

Bạn có thể mở `dest.xlsx` trong Excel, LibreOffice, hoặc bất kỳ trình xem nào hỗ trợ `.xlsx` để xác nhận rằng các giá trị, định dạng và chức năng pivot đều được giữ nguyên.

---

## Sao chép workbook pivot table – những gì bạn nên biết

* **Pivot cache được sao chép tự động.** Thư viện chuyển cache nền, vì vậy pivot không cần phải làm mới thủ công.
* **Nguồn dữ liệu bên ngoài không được chuyển.** Nếu pivot lấy dữ liệu từ cơ sở dữ liệu bên ngoài, bạn phải đảm bảo workbook đích có thể truy cập cùng nguồn, hoặc tạo lại cache cục bộ.
* **Pivot table lớn có thể tăng mức sử dụng bộ nhớ.** Đối với các workbook rất lớn, hãy cân nhắc tăng heap JVM (`-Xmx2g`) để tránh `OutOfMemoryError`.

---

## Lưu file workbook ở các định dạng khác nhau

Aspose.Cells cho phép bạn lưu kết quả sang nhiều định dạng mà không cần thay đổi mã:

```java
// Save as XLS (Excel 97-2003)
destWb.save("dest.xls");

// Save as CSV (first worksheet only)
destWb.save("dest.csv");

// Save as PDF (visual representation)
destWb.save("dest.pdf");
```

Chọn định dạng phù hợp với quy trình downstream của bạn. Logic `copyRange` vẫn hoạt động bất kể định dạng cuối cùng.

---

## Tải workbook Excel Java – mẹo bổ sung

* **Tải file được mã hoá:** Sử dụng `LoadOptions` với mật khẩu:  
  ```java
  LoadOptions opt = new LoadOptions(LoadFormat.XLSX);
  opt.setPassword("myPassword");
  Workbook wb = new Workbook("encrypted.xlsx", opt);
  ```
* **Đọc chỉ các sheet cụ thể:**  
  ```java
  LoadOptions opt = new LoadOptions(LoadFormat.XLSX);
  opt.setLoadDataOnly(true); // faster if you only need values
  Workbook wb = new Workbook("file.xlsx", opt);
  ```

Các tùy chọn này có thể tăng tốc bước **load excel workbook java**, đặc biệt với các file lớn.

---

## Kết luận

Bây giờ bạn đã biết **cách sao chép ô** giữa các workbook Excel trong Java, cách **sao chép phạm vi giữa các workbook** chứa **pivot table**, và cách **lưu file workbook** ở định dạng bạn cần. Bằng cách làm theo các bước trên, bạn có thể tích hợp việc xử lý dữ liệu Excel vào bất kỳ ứng dụng Java nào—cho dù bạn đang xây dựng một engine báo cáo, một pipeline ETL, hoặc một công cụ chuyển đổi file đơn giản.

**Các bước tiếp theo** bạn có thể khám phá:

* Sử dụng **copy range between workbooks** để hợp nhất nhiều báo cáo vào

## Bạn Nên Học Gì Tiếp Theo?

Các hướng dẫn sau đây bao gồm các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh với giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Lưu Workbook Mới trong Java – Hướng Dẫn Sao Chép Phạm Vi Giữa Các Workbook](/cells/english/java/workbook-operations/save-new-workbook-in-java-copy-range-between-workbooks-tutor/)
- [Cách sao chép pivot tables giữa các workbook Excel trong Java](/cells/english/java/excel-pivot-tables/how-to-copy-pivot-tables-between-excel-workbooks-in-java/)
- [Cách sao chép phạm vi trong Java – Sao chép Pivot Table với Aspose.Cells](/cells/english/java/excel-pivot-tables/how-to-copy-range-in-java-copy-pivot-table-with-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}