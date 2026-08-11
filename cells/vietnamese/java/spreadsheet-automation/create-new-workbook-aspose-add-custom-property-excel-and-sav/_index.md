---
category: general
date: 2026-08-11
description: Tạo workbook mới bằng Aspose trong Java, thêm thuộc tính tùy chỉnh Excel,
  sau đó lưu workbook dưới dạng XLSB với ví dụ chi tiết từng bước.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create new workbook aspose
- save workbook as xlsb
- add custom property excel
- Aspose.Cells Java
- custom properties Excel
- workbook serialization
language: vi
lastmod: 2026-08-11
og_description: Tạo một workbook mới bằng Aspose trong Java, thêm thuộc tính tùy chỉnh
  cho Excel và lưu workbook dưới dạng XLSB với một ví dụ hoàn chỉnh, sẵn sàng chạy.
og_image_alt: Java code screenshot that creates a new workbook Aspose, adds a custom
  Excel property, and saves it as an XLSB file
og_title: Tạo sổ làm việc mới Aspose – thêm thuộc tính tùy chỉnh Excel
schemas:
- author: Aspose
  dateModified: '2026-08-11'
  description: Create new workbook Aspose in Java, add a custom property Excel, then
    save workbook as XLSB with a full step‑by‑step example.
  headline: Create new workbook Aspose – add custom property Excel and save as XLSB
  type: TechArticle
- description: Create new workbook Aspose in Java, add a custom property Excel, then
    save workbook as XLSB with a full step‑by‑step example.
  name: Create new workbook Aspose – add custom property Excel and save as XLSB
  steps:
  - name: What if I need to store a string property?
    text: '```java worksheet.getCustomProperties().add("Owner", "Alice"); ```'
  - name: Can I add multiple custom properties at once?
    text: Yes. Call `add` repeatedly for each name/value pair. Aspose.Cells does not
      limit the number of custom properties, but keep the total size reasonable to
      avoid bloating the file.
  - name: How does the binary format affect performance?
    text: XLSB files load faster because they avoid XML parsing. This is especially
      noticeable for workbooks with many rows, formulas, or embedded images.
  - name: What if I need to work with an existing XLSX file?
    text: Replace the `new Workbook()` constructor with `new Workbook("ExistingFile.xlsx")`.
      The rest of the steps (adding properties, saving as XLSB) remain identical.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel
- XLSB
- Custom Properties
title: Tạo sổ làm việc mới Aspose – thêm thuộc tính tùy chỉnh Excel và lưu dưới dạng
  XLSB
url: /vi/java/spreadsheet-automation/create-new-workbook-aspose-add-custom-property-excel-and-sav/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo workbook mới Aspose – thêm custom property Excel và lưu dưới dạng XLSB

Nếu bạn cần **create new workbook Aspose** trong một ứng dụng Java, hướng dẫn này sẽ chỉ cho bạn cách thực hiện chính xác. Bạn sẽ học cách **add custom property Excel**, lấy lại giá trị, và **save workbook as XLSB** mà không mất bất kỳ metadata nào.

Bài hướng dẫn bao gồm mọi thứ từ thiết lập dự án đến việc xác minh tệp đã lưu. Không cần tài liệu bên ngoài; chỉ cần làm theo các bước và chạy mã.

## Yêu cầu trước

- Java Development Kit (JDK) 8 hoặc cao hơn đã được cài đặt.
- Maven hoặc Gradle để quản lý phụ thuộc (ví dụ sử dụng Maven).
- Giấy phép Aspose.Cells for Java đang hoạt động (hoặc sử dụng chế độ đánh giá miễn phí để thử nghiệm).

## Bước 1: Thêm Aspose.Cells vào dự án của bạn

Thêm artifact Aspose.Cells Maven vào file `pom.xml` của bạn. Phụ thuộc này cung cấp các lớp cần thiết để **create new workbook Aspose**.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- Use the latest stable version -->
</dependency>
```

> **Mẹo chuyên nghiệp:** Nếu bạn thích Gradle, hãy thay thế đoạn mã Maven bằng dòng tương đương `implementation "com.aspose:aspose-cells:23.12"`.

## Bước 2: Tạo một workbook Aspose mới

Bước chức năng đầu tiên là khởi tạo một đối tượng `Workbook`. Đối tượng này đại diện cho một tệp Excel trong bộ nhớ và là điểm vào cho tất cả các thao tác tiếp theo.

```java
import com.aspose.cells.*;

public class CustomPropertiesXlsb {

    public static void main(String[] args) throws Exception {
        // Step 2: Create a new workbook Aspose
        Workbook workbook = new Workbook();               // In‑memory workbook
        Worksheet worksheet = workbook.getWorksheets().get(0); // Default first sheet
```

Việc tạo một workbook Aspose mới sẽ cung cấp cho bạn một workbook sạch với một worksheet mặc định, sẵn sàng để tùy chỉnh.

## Bước 3: Thêm custom property Excel

Các thuộc tính tùy chỉnh cho phép bạn lưu trữ metadata tùy ý bên trong tệp Excel. Ở đây chúng tôi **add custom property Excel** có tên `ProjectId` với giá trị số.

```java
        // Step 3: Add a custom property named "ProjectId" with a numeric value
        worksheet.getCustomProperties().add("ProjectId", 12345);
```

Phương thức `add` nhận một tên thuộc tính và một giá trị của bất kỳ kiểu nào được hỗ trợ (string, number, date, v.v.). Metadata này sẽ đi cùng tệp bất kể bạn sao chép nó tới đâu.

## Bước 4: Lấy và hiển thị custom property

Đọc lại thuộc tính sẽ xác minh rằng nó đã được lưu đúng. Bạn cũng có thể sử dụng giá trị đã lấy trong logic nghiệp vụ của mình.

```java
        // Step 4: Retrieve the custom property value and display it
        int projectId = (int) worksheet.getCustomProperties()
                                      .get("ProjectId")
                                      .getValue();
        System.out.println("ProjectId = " + projectId);
```

Ép kiểu sang `int` hoạt động vì chúng ta đã lưu một giá trị số. Nếu bạn lưu một chuỗi, hãy sử dụng `(String)` thay thế.

## Bước 5: Lưu workbook dưới dạng XLSB

Bây giờ bạn **save workbook as XLSB**. Định dạng XLSB lưu workbook dưới dạng nhị phân, giúp mở nhanh hơn và kích thước trên đĩa nhỏ hơn. Tất cả các custom property sẽ được tự động giữ lại.

```java
        // Step 5: Save the workbook as an XLSB file (custom properties are preserved)
        workbook.save("WithCustomProps.xlsb", SaveFormat.XLSB);
    }
}
```

Thay thế `"WithCustomProps.xlsb"` bằng đường dẫn tuyệt đối nếu bạn cần tệp trong một thư mục cụ thể. Enum `SaveFormat.XLSB` cho Aspose.Cells biết ghi dưới dạng nhị phân.

## Bước 6: Xác minh đầu ra

Chạy chương trình từ IDE hoặc dòng lệnh:

```bash
mvn compile exec:java -Dexec.mainClass=CustomPropertiesXlsb
```

Bạn sẽ thấy:

```
ProjectId = 12345
```

Mở `WithCustomProps.xlsb` trong Excel. Điều hướng tới **File → Info → Properties → Advanced Properties → Custom**. Mục `ProjectId` với giá trị `12345` sẽ được liệt kê, xác nhận rằng bước **add custom property excel** đã thành công và thao tác **save workbook as xlsb** đã giữ lại metadata.

## Các câu hỏi thường gặp và trường hợp đặc biệt

### Nếu tôi cần lưu một thuộc tính kiểu chuỗi thì sao?

```java
worksheet.getCustomProperties().add("Owner", "Alice");
```

Lấy nó bằng:

```java
String owner = (String) worksheet.getCustomProperties().get("Owner").getValue();
```

### Tôi có thể thêm nhiều custom property cùng lúc không?

Có. Gọi `add` liên tục cho mỗi cặp tên/giá trị. Aspose.Cells không giới hạn số lượng custom property, nhưng hãy giữ tổng kích thước ở mức hợp lý để tránh làm tệp quá lớn.

### Định dạng nhị phân ảnh hưởng như thế nào đến hiệu năng?

Các tệp XLSB tải nhanh hơn vì chúng tránh việc phân tích XML. Điều này đặc biệt rõ rệt với các workbook có nhiều hàng, công thức hoặc hình ảnh nhúng.

### Nếu tôi cần làm việc với tệp XLSX hiện có thì sao?

Thay thế hàm khởi tạo `new Workbook()` bằng `new Workbook("ExistingFile.xlsx")`. Các bước còn lại (thêm thuộc tính, lưu dưới dạng XLSB) vẫn giống nhau.

## Mã nguồn đầy đủ

Dưới đây là ví dụ hoàn chỉnh, sẵn sàng để chạy. Sao chép nó vào một tệp có tên `CustomPropertiesXlsb.java` trong thư mục `src/main/java` của bạn.

```java
import com.aspose.cells.*;

public class CustomPropertiesXlsb {
    public static void main(String[] args) throws Exception {
        // Step 2: Create a new workbook Aspose
        Workbook workbook = new Workbook();                       // In‑memory workbook
        Worksheet worksheet = workbook.getWorksheets().get(0);    // Default first sheet

        // Step 3: Add a custom property named "ProjectId" with a numeric value
        worksheet.getCustomProperties().add("ProjectId", 12345);

        // Step 4: Retrieve the custom property value and display it
        int projectId = (int) worksheet.getCustomProperties()
                                      .get("ProjectId")
                                      .getValue();
        System.out.println("ProjectId = " + projectId);

        // Step 5: Save the workbook as an XLSB file (custom properties are preserved)
        workbook.save("WithCustomProps.xlsb", SaveFormat.XLSB);
    }
}
```

Chạy lớp này sẽ tạo ra một tệp XLSB chứa custom property và có thể mở được trong bất kỳ phiên bản Microsoft Excel hiện đại nào.

## Kết luận

Bây giờ bạn đã biết cách **create new workbook Aspose**, **add custom property Excel**, và **save workbook as XLSB** bằng Java. Ví dụ minh họa toàn bộ vòng đời: khởi tạo, chèn metadata, xác minh và tuần tự hoá nhị phân.

Tiếp theo, khám phá các chủ đề liên quan như **setting document properties**, **working with Excel formulas**, hoặc **converting between XLSX and XLSB**. Mỗi chủ đề này dựa trên cùng một API Aspose.Cells mà bạn vừa sử dụng, vì vậy bạn có thể mở rộng giải pháp mà không cần học thư viện mới.

Bạn có thể thoải mái thử nghiệm với các kiểu dữ liệu khác nhau, nhiều worksheet, hoặc bảo vệ bằng mật khẩu—Aspose.Cells hỗ trợ tất cả các kịch bản này ngay từ đầu. Chúc lập trình vui vẻ!

## Bạn nên học gì tiếp theo?

Các hướng dẫn sau đây bao gồm các chủ đề liên quan chặt chẽ, dựa trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoạt động đầy đủ với giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Create Save Excel Workbook Aspose Cells Java](/cells/english/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)
- [How to Create and Save an Excel Workbook as SVG using Aspose.Cells for Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)
- [Create Excel Workbook and Add Labels with Aspose.Cells for Java](/cells/english/java/advanced-excel-charts/data-labeling/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}