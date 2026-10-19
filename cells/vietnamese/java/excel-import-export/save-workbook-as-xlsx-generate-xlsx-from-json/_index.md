---
category: general
date: 2026-06-21
description: Lưu sổ làm việc dưới dạng XLSX bằng SmartMarkerProcessor để tạo XLSX
  từ JSON và dễ dàng điền dữ liệu vào Excel từ JSON.
draft: false
keywords:
- save workbook as xlsx
- generate xlsx from json
- populate excel from json
language: vi
og_description: Lưu workbook dưới dạng XLSX chỉ bằng một đoạn mã Java. Tìm hiểu cách
  tạo XLSX từ JSON và điền dữ liệu vào Excel từ JSON bằng SmartMarker.
og_title: Lưu Workbook dưới dạng XLSX – Tạo XLSX từ JSON
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Save workbook as XLSX using SmartMarkerProcessor to generate XLSX from
    JSON and easily populate Excel from JSON data.
  headline: Save Workbook as XLSX – Generate XLSX from JSON
  type: TechArticle
- description: Save workbook as XLSX using SmartMarkerProcessor to generate XLSX from
    JSON and easily populate Excel from JSON data.
  name: Save Workbook as XLSX – Generate XLSX from JSON
  steps:
  - name: Expected Result
    text: 'After you run the program, open `output.xlsx`. You’ll see a sheet named
      **Sheet1** with two rows of data:'
  - name: Customizing the Template
    text: 'If you’d rather control column order or add a header row, create a tiny
      template before running the code:'
  - name: 1. Nested JSON Objects
    text: SmartMarker can dive into nested structures using dot notation (`${jsonArray.Address.City}`).
      Just ensure your JSON string reflects that hierarchy.
  - name: 2. Large Datasets
    text: 'When dealing with thousands of rows, disable workbook calculation before
      processing:'
  - name: 3. Data Types
    text: 'Dates, numbers, and booleans are inferred automatically, but you can force
      a format:'
  - name: 4. Multiple Placeholders
    text: You can feed several JSON arrays into the same workbook by using distinct
      placeholder names (`${orders}`, `${customers}`) and calling `processor.apply`
      for each.
  type: HowTo
- questions:
  - answer: No. The library is self‑contained; just add the JAR (or Maven dependency)
      and you’re ready to **save workbook as xlsx**.
    question: Do I need to install anything besides the Aspose Cells JAR?
  - answer: 'Absolutely. Replace `workbook.save("output.xlsx", SaveFormat.XLSX);`
      with: ```java try (FileOutputStream out = new FileOutputStream("output.xlsx"))
      { workbook.save(out, SaveFormat.XLSX); } ```'
    question: Can I write directly to a stream instead of a file?
  - answer: 'Use the `SmartMarkerProcessor.setCustomFieldNames` method to map JSON
      keys to placeholder names. ## Conclusion We’ve covered everything you need to
      **save workbook as xlsx** while **generating XLSX from JSON** and **populating
      Excel from JSON** using Aspose Cells’ SmartMarker. The short program show'
    question: What if my JSON keys don’t match Excel column names?
  type: FAQPage
tags:
- Aspose.Cells
- Java
- Excel Automation
title: Lưu sổ làm việc dưới dạng XLSX – Tạo XLSX từ JSON
url: /vi/java/excel-import-export/save-workbook-as-xlsx-generate-xlsx-from-json/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Lưu Workbook dưới dạng XLSX – Tạo XLSX từ JSON

Bạn đã bao giờ cần **save workbook as xlsx** nhưng chỉ có dữ liệu JSON trong tay? Bạn không phải là người duy nhất gặp khó khăn này. Dù bạn đang lấy phản hồi API, đọc tệp cấu hình, hay chỉ thử nghiệm các báo cáo Excel dựa trên dữ liệu, việc chuyển JSON thành một bảng tính gọn gàng là một yêu cầu thường gặp.

Trong hướng dẫn này, chúng tôi sẽ đi qua một ví dụ Java hoàn chỉnh, sẵn sàng chạy, mà **generates XLSX from JSON** và cho bạn thấy chính xác cách **populate Excel from JSON** bằng bộ xử lý SmartMarker của Aspose Cells. Không có những tham chiếu mơ hồ—chỉ có mã bạn có thể sao chép, dán và chạy.

## Những gì bạn cần

- Java 17 (hoặc bất kỳ JDK gần đây nào)  
- Thư viện Aspose Cells cho Java (phiên bản dùng thử miễn phí hoạt động tốt)  
- Một IDE đơn giản hoặc công cụ xây dựng dòng lệnh (Maven/Gradle)  
- Đoạn JSON mà chúng ta sẽ đưa vào workbook  

Chỉ vậy—không có dịch vụ phụ, không có bước ẩn. Hãy bắt đầu.

## Lưu Workbook dưới dạng XLSX – Quy trình đầy đủ

Dưới đây là toàn bộ chương trình, từ việc nhập thư viện đến việc lưu tệp trên đĩa. Hãy chú ý đến các chú thích; chúng giải thích **why** mỗi dòng quan trọng, không chỉ **what** nó làm.

```java
// ---------------------------------------------------------------
// Save Workbook as XLSX – Complete Java Example
// ---------------------------------------------------------------
import com.aspose.cells.*;
import com.google.gson.JsonArray; // For parsing raw JSON string

public class JsonToExcelDemo {

    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook that will receive the data
        Workbook workbook = new Workbook();

        // Step 2: Initialize the SmartMarker processor for the workbook
        SmartMarkerProcessor processor = new SmartMarkerProcessor(workbook);

        // Step 3: Enable the flag to treat an array as a single record.
        // This tells SmartMarker to iterate over each element in the JSON array.
        processor.setArrayAsSingle(true);

        // Step 4: Prepare the JSON array source.
        // In a real‑world scenario you might read this from a file or API.
        String json = "[{\"Name\":\"John\",\"Age\":30},{\"Name\":\"Anna\",\"Age\":25}]";

        // Step 5: Apply the JSON data to the SmartMarker using the placeholder ${jsonArray}
        // The JsonArray class from Aspose wraps the raw string so SmartMarker can understand it.
        processor.apply("${jsonArray}", new JsonArray(json));

        // OPTIONAL: Save the workbook to see the result.
        // This is the line that actually **save workbook as xlsx**.
        workbook.save("output.xlsx", SaveFormat.XLSX);

        System.out.println("Workbook saved successfully as output.xlsx");
    }
}
```

> **Mẹo chuyên nghiệp:** Nếu bạn đang sử dụng Maven, thêm các phụ thuộc sau vào `pom.xml` của bạn:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- check for the latest version -->
</dependency>
<dependency>
    <groupId>com.google.code.gson</groupId>
    <artifactId>gson</artifactId>
    <version>2.10.1</version>
</dependency>
```

### Kết quả mong đợi

Sau khi chạy chương trình, mở `output.xlsx`. Bạn sẽ thấy một sheet có tên **Sheet1** với hai hàng dữ liệu:

| Name | Age |
|------|-----|
| John | 30  |
| Anna | 25  |

Đó là toàn bộ trải nghiệm **populate excel from json** trong chưa đầy 30 dòng Java.

![ví dụ lưu workbook dưới dạng xlsx](example.png)

*Văn bản thay thế hình ảnh: “ví dụ lưu workbook dưới dạng xlsx”*

## Tạo XLSX từ JSON – Cách SmartMarker Hoạt động

SmartMarker về cơ bản là một công cụ tạo mẫu cho Excel. Bằng cách đặt `${jsonArray}` vào bất kỳ ô (hoặc phạm vi) nào của một workbook trống, bạn nói với bộ xử lý “thay thế placeholder này bằng dữ liệu từ mảng JSON”. Khi `processor.apply` chạy, nó:

1. Phân tích JSON thành một tập hợp các bản ghi.  
2. Ánh xạ mỗi thuộc tính (`Name`, `Age`) tới một cột dựa trên ngữ cảnh của placeholder.  
3. Tự động chèn các hàng, xử lý kiểu dữ liệu cho bạn.

Vì chúng tôi đã gọi `processor.setArrayAsSingle(true)`, toàn bộ mảng được coi là một tập hợp bản ghi logic duy nhất, đây là mẫu phổ biến nhất khi **generating XLSX from JSON**.

### Tùy chỉnh mẫu

Nếu bạn muốn kiểm soát thứ tự cột hoặc thêm một hàng tiêu đề, hãy tạo một mẫu nhỏ trước khi chạy mã:

| A            | B   |
|--------------|-----|
| **Name**     | **Age** |
| ${jsonArray.Name} | ${jsonArray.Age} |

Lưu tệp này dưới tên `template.xlsx` và tải nó thay vì một workbook trống:

```java
Workbook workbook = new Workbook("template.xlsx");
```

Phần còn lại của các bước vẫn giống nhau, và đầu ra sẽ giữ lại hàng tiêu đề mà bạn đã định nghĩa.

## Populate Excel từ JSON – Các trường hợp đặc biệt & Mẹo

### 1. Đối tượng JSON lồng nhau

SmartMarker có thể đi sâu vào cấu trúc lồng nhau bằng cách sử dụng ký hiệu chấm (`${jsonArray.Address.City}`). Chỉ cần đảm bảo chuỗi JSON của bạn phản ánh cấu trúc đó.

### 2. Bộ dữ liệu lớn

Khi xử lý hàng nghìn dòng, tắt tính toán workbook trước khi xử lý:

```java
workbook.getSettings().setCalculateFormula(false);
```

Bật lại sau khi lưu để duy trì hiệu suất nhanh.

### 3. Kiểu dữ liệu

Ngày, số và boolean được suy ra tự động, nhưng bạn có thể ép buộc một định dạng:

```java
processor.apply("${jsonArray.BirthDate}", new JsonArray(json));
workbook.getWorksheets().get(0).getCells().get("C2").setNumberFormat("mm/dd/yyyy");
```

### 4. Nhiều placeholder

Bạn có thể đưa nhiều mảng JSON vào cùng một workbook bằng cách sử dụng các tên placeholder riêng biệt (`${orders}`, `${customers}`) và gọi `processor.apply` cho mỗi cái.

## Các câu hỏi thường gặp được trả lời

**Q: Tôi có cần cài đặt gì thêm ngoài JAR của Aspose Cells không?**  
A: Không. Thư viện tự chứa; chỉ cần thêm JAR (hoặc phụ thuộc Maven) và bạn đã sẵn sàng **save workbook as xlsx**.

**Q: Tôi có thể ghi trực tiếp vào một stream thay vì tệp không?**  
A: Chắc chắn. Thay thế `workbook.save("output.xlsx", SaveFormat.XLSX);` bằng:

```java
try (FileOutputStream out = new FileOutputStream("output.xlsx")) {
    workbook.save(out, SaveFormat.XLSX);
}
```

**Q: Nếu các khóa JSON của tôi không khớp với tên cột Excel thì sao?**  
A: Sử dụng phương thức `SmartMarkerProcessor.setCustomFieldNames` để ánh xạ các khóa JSON tới tên placeholder.

## Kết luận

Chúng tôi đã bao phủ mọi thứ bạn cần để **save workbook as xlsx** trong khi **generating XLSX from JSON** và **populating Excel from JSON** bằng SmartMarker của Aspose Cells. Chương trình ngắn này cho thấy vòng đời đầy đủ: tạo workbook, cấu hình SmartMarker, đưa một mảng JSON vào, và cuối cùng lưu tệp.

Tiếp theo, hãy thử mở rộng mẫu với công thức, định dạng, hoặc nhiều worksheet—mỗi khái niệm này được xây dựng trực tiếp trên nền tảng bạn vừa nắm vững. Nếu gặp khó khăn, việc xem lại phần “Các trường hợp đặc biệt & Mẹo” thường giúp giải quyết.

Chúc lập trình vui vẻ, và mong các bảng tính của bạn luôn sạch sẽ như JSON của bạn!

## Bạn nên học gì tiếp theo?

Các hướng dẫn sau đây bao gồm các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoạt động đầy đủ với giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Cách lưu tệp XLSX bằng Aspose.Cells cho .NET: Hướng dẫn từng bước](/cells/english/net/workbook-operations/save-xlsx-files-aspose-cells-dotnet/)
- [Cách lưu Workbook Excel trong Java bằng Aspose.Cells](/cells/english/java/automation-batch-processing/excel-automation-java-aspose-cells-guide/)
- [Cách tạo và lưu Workbook Excel dưới dạng SVG bằng Aspose.Cells cho Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}