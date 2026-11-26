---
category: general
date: 2026-11-25
description: Tạo ví dụ mã Java tạo sổ làm việc Excel sử dụng smart markers của Aspose.Cells
  để liên kết các mảng JSON thành giá trị đơn.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook java
- Aspose.Cells smart marker
- Java JSON to Excel
- setSmartMarkerData
- Excel export Java
language: vi
lastmod: 2026-11-25
og_description: Tạo workbook Excel bằng Java với Aspose.Cells để dễ dàng xuất các
  mảng JSON thành các ô riêng lẻ. Thực hiện theo hướng dẫn từng bước.
og_image_alt: Screenshot of an Excel workbook created in Java using Aspose.Cells smart
  markers
og_title: Tạo sổ làm việc Excel bằng Java – Hướng dẫn smart marker của Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-11-25'
  description: Create Excel workbook Java code example using Aspose.Cells smart markers
    to bind JSON arrays as single values.
  headline: How to create Excel workbook Java with Aspose.Cells markers
  type: TechArticle
- description: Create Excel workbook Java code example using Aspose.Cells smart markers
    to bind JSON arrays as single values.
  name: How to create Excel workbook Java with Aspose.Cells markers
  steps:
  - name: '**Creates a fresh workbook** – `new Workbook()` gives you an in‑memory
      Excel file with a default sheet.'
    text: '**Creates a fresh workbook** – `new Workbook()` gives you an in‑memory
      Excel file with a default sheet.'
  - name: '**Places a smart marker in cell A1** – `{{jsonArray:ArrayAsSingle}}` tells
      Aspose.Cells to replace the marker with the *entire* array, joined by commas.'
    text: '**Places a smart marker in cell A1** – `{{jsonArray:ArrayAsSingle}}` tells
      Aspose.Cells to replace the marker with the *entire* array, joined by commas.'
  - name: '**Builds a `Map` data source** – The key `"jsonArray"` matches the marker
      name; the value is a `String[]`.'
    text: '**Builds a `Map` data source** – The key `"jsonArray"` matches the marker
      name; the value is a `String[]`.'
  - name: '**Calls `setSmartMarkerData`** – This binds the map to the marker and performs
      the replacement.'
    text: '**Calls `setSmartMarkerData`** – This binds the map to the marker and performs
      the replacement.'
  - name: '**Saves the file** – `workbook.save(...)` writes `JsonSingleValue.xlsx`
      to disk.'
    text: '**Saves the file** – `workbook.save(...)` writes `JsonSingleValue.xlsx`
      to disk.'
  - name: Open `JsonSingleValue.xlsx` in Microsoft Excel, LibreOffice Calc, or Google
      Sheets.
    text: Open `JsonSingleValue.xlsx` in Microsoft Excel, LibreOffice Calc, or Google
      Sheets.
  - name: Confirm that cell **A1** reads `One, Two, Three`.
    text: Confirm that cell **A1** reads `One, Two, Three`.
  - name: Check that no extra rows or columns were added – the smart marker performed
      an in‑place replacement.
    text: Check that no extra rows or columns were added – the smart marker performed
      an in‑place replacement.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Cách tạo workbook Excel trong Java với các marker của Aspose.Cells
url: /vi/java/templates-reporting/how-to-create-excel-workbook-java-with-aspose-cells-markers/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách tạo workbook Excel Java với các marker của Aspose.Cells

Nếu bạn cần **tạo workbook Excel Java** có mã viết một mảng JSON vào một ô duy nhất, hướng dẫn này sẽ chỉ cho bạn cách thực hiện. Sử dụng các smart marker của Aspose.Cells, bạn có thể xử lý toàn bộ mảng như một giá trị duy nhất, tránh việc phải viết vòng lặp thủ công và ghi từng ô một.

Bạn sẽ học cách thiết lập một workbook, định nghĩa một smart marker, liên kết nguồn dữ liệu `Map` chứa một mảng kiểu JSON, và cuối cùng lưu file. Ví dụ này hoạt động với Java 17+, Maven, và thư viện dùng thử miễn phí Aspose.Cells for Java.

---

![Screenshot of an Excel workbook created in Java using Aspose.Cells smart markers](excel-workbook-java.png){: .center-image alt="Ảnh chụp màn hình của một workbook Excel được tạo bằng Java sử dụng các smart marker của Aspose.Cells"}

## Yêu cầu trước

| Yêu cầu | Lý do quan trọng |
|-------------|----------------|
| Java 17 hoặc mới hơn | Các tính năng ngôn ngữ mới nhất và các bản cập nhật bảo mật |
| Maven 3.6+ | Đơn giản hoá việc quản lý phụ thuộc |
| Aspose.Cells for Java (v23.12 hoặc mới hơn) | Cung cấp các API `Workbook`, `Worksheet` và smart‑marker được sử dụng trong mẫu |
| Kiến thức cơ bản về các collection của Java | Bạn sẽ tạo một `Map<String, Object>` làm nguồn dữ liệu |

Thêm phụ thuộc Aspose.Cells vào file `pom.xml` của bạn:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>
    <classifier>jdk17</classifier>
</dependency>
```

---

## Tạo workbook Excel Java – ví dụ đầy đủ

Chương trình sau là một giải pháp **đầy đủ, có thể chạy**. Sao chép nó vào một file có tên `ExcelSmartMarkerDemo.java`, biên dịch và chạy.

```java
package com.example.excel;

import com.aspose.cells.*;
import java.util.HashMap;
import java.util.Map;

/**
 * Demonstrates how to create Excel workbook Java using Aspose.Cells smart markers.
 * The smart marker "{{jsonArray:ArrayAsSingle}}" treats the whole array as a single cell value.
 */
public class ExcelSmartMarkerDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();                       // empty workbook
        Worksheet worksheet = workbook.getWorksheets().get(0);    // first (default) sheet

        // Step 2: Define a smart marker that treats a JSON array as a single value
        // The "ArrayAsSingle" option concatenates the array elements with commas.
        String smartMarker = "{{jsonArray:ArrayAsSingle}}";
        worksheet.getCells().get("A1").putValue(smartMarker);

        // Step 3: Prepare the data source – a simple string array
        Map<String, Object> dataSource = new HashMap<>();
        dataSource.put("jsonArray", new String[] { "One", "Two", "Three" });

        // Step 4: Bind the data to the smart marker and save the workbook
        worksheet.getCells().get("A1").setSmartMarkerData(dataSource);
        workbook.save("JsonSingleValue.xlsx");   // workbook saved to project root
        System.out.println("Workbook created successfully.");
    }
}
```

### Những gì mã thực hiện

1. **Tạo một workbook mới** – `new Workbook()` cung cấp cho bạn một file Excel trong bộ nhớ với một sheet mặc định.  
2. **Đặt một smart marker vào ô A1** – `{{jsonArray:ArrayAsSingle}}` cho Aspose.Cells biết thay thế marker bằng *toàn bộ* mảng, các phần tử được nối bằng dấu phẩy.  
3. **Xây dựng nguồn dữ liệu `Map`** – Khóa `"jsonArray"` phải trùng với tên marker; giá trị là một `String[]`.  
4. **Gọi `setSmartMarkerData`** – Phương thức này liên kết map với marker và thực hiện việc thay thế.  
5. **Lưu file** – `workbook.save(...)` ghi `JsonSingleValue.xlsx` vào đĩa.

Khi bạn mở file Excel đã tạo, ô **A1** sẽ chứa:

```
One, Two, Three
```

Mảng được hiển thị dưới dạng một chuỗi duy nhất, các phần tử ngăn cách bằng dấu phẩy vì tùy chọn `ArrayAsSingle`.

---

## Sử dụng smart marker của Aspose.Cells để liên kết dữ liệu JSON

Smart marker của Aspose.Cells là một cách mạnh mẽ để ánh xạ các đối tượng phức tạp (bao gồm các cấu trúc giống JSON) trực tiếp lên các worksheet. Cú pháp `{{fieldName:Option}}` hoạt động giống như một engine mẫu:

* **fieldName** – khóa trong nguồn dữ liệu của bạn (`Map`, POJO, hoặc `DataTable`).  
* **Option** – điều khiển cách các collection được xử lý. `ArrayAsSingle` coi toàn bộ collection như một giá trị; các tùy chọn khác như `Array` sẽ mở rộng mảng ra các hàng.

**Tại sao nên dùng smart marker thay vì vòng lặp?**  
Một vòng lặp đòi hỏi tính toán địa chỉ ô thủ công, chỉ mục dễ gây lỗi, và mã bổ sung cho việc định dạng. Smart marker cho phép bạn viết các placeholder khai báo, giữ cho mã Java ngắn gọn, và để thư viện xử lý các chi tiết bố cục.

---

## Thiết lập nguồn dữ liệu Map trong Java

`Map<String, Object>` là container dữ liệu đơn giản nhất cho Aspose.Cells:

```java
Map<String, Object> dataSource = new HashMap<>();
dataSource.put("jsonArray", new String[] { "One", "Two", "Three" });
```

*Khóa (`jsonArray`) phải khớp chính xác với tên marker.*  
Bạn cũng có thể sử dụng `List<String>`, một POJO tùy chỉnh, hoặc thậm chí một `Map` lồng nhau cho các cấu trúc JSON phức tạp hơn. Aspose.Cells sẽ tự động duyệt qua đồ thị đối tượng.

**Mẹo:** Nếu bạn cần định dạng chuỗi đã nối khác (ví dụ: dùng dấu chấm phẩy), hãy tiền xử lý mảng trong Java trước khi gán nó vào map:

```java
String joined = String.join(";", new String[] {"One","Two","Three"});
dataSource.put("jsonArray", new String[] { joined });
```

---

## Lưu workbook và xác minh đầu ra

```java
workbook.save("JsonSingleValue.xlsx");
```

Phương thức `save` hỗ trợ nhiều định dạng (`.xlsx`, `.xls`, `.csv`, `.pdf`). Trong hướng dẫn này chúng tôi giữ định dạng mặc định Excel Open XML.

**Các bước xác minh**

1. Mở `JsonSingleValue.xlsx` bằng Microsoft Excel, LibreOffice Calc, hoặc Google Sheets.  
2. Xác nhận rằng ô **A1** hiển thị `One, Two, Three`.  
3. Kiểm tra không có hàng hoặc cột bổ sung nào được thêm – smart marker đã thực hiện việc thay thế tại chỗ.

Nếu ô hiển thị văn bản marker thô (`{{jsonArray:ArrayAsSingle}}`), hãy kiểm tra lại rằng:

* Tên marker phải khớp chính xác với khóa trong map (phân biệt chữ hoa/thường).  
* `setSmartMarkerData` được gọi **sau** khi marker đã được đặt.  
* Phiên bản Aspose.Cells hỗ trợ tùy chọn `ArrayAsSingle` (có từ v20.3 trở lên).

---

## Các biến thể phổ biến và trường hợp đặc biệt

| Kịch bản | Điều chỉnh |
|----------|------------|
| **Dấu phân cách khác** | Sử dụng `ArrayAsSingle` kết hợp với việc nối tùy chỉnh trong Java (xem mẹo ở trên). |
| **Nhiều mảng trong một sheet** | Đặt các marker bổ sung như `{{anotherArray:ArrayAsSingle}}` vào các ô khác và thêm các mục tương ứng vào map. |
| **Đối tượng JSON lồng nhau** | Cung cấp một `Map<String, Object>` lồng nhau; tham chiếu các trường bằng ký hiệu chấm (`{{parent.child}}`). |
| **Bộ dữ liệu lớn** | Đối với hàng ngàn dòng, nên dùng tùy chọn `Array` để Aspose.Cells tự động mở rộng các hàng, điều này |

## Bạn nên học gì tiếp theo?

Những hướng dẫn sau đây bao gồm các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên đều có các ví dụ mã hoàn chỉnh, kèm theo giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Cách tạo và xuất Excel sang HTML bằng Aspose.Cells Java \| Hướng dẫn thao tác Workbook](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [Xuất workbook Excel dưới dạng hình ảnh bằng Aspose.Cells cho Java: Hướng dẫn từng bước](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)
- [Cách tạo và lưu workbook Excel dưới dạng SVG bằng Aspose.Cells cho Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}