---
category: general
date: 2026-08-20
description: Tạo smart markers cho các worksheet trong Java bằng Aspose.Cells và kiểm
  soát việc đặt tên sheet chi tiết bằng SmartMarkerOptions.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create worksheets smart markers
- Aspose.Cells Java
- smart marker options
- duplicate sheet names
- detail sheet naming
language: vi
lastmod: 2026-08-20
og_description: Tạo smart markers cho các worksheet trong Java với Aspose.Cells. Tìm
  hiểu cách đặt tên cho các sheet chi tiết một cách động bằng SmartMarkerOptions.
og_image_alt: create worksheets smart markers example diagram
og_title: Tạo smart markers cho bảng tính – Hướng dẫn Java với Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-08-20'
  description: Create worksheets smart markers in Java using Aspose.Cells and control
    detail sheet naming with SmartMarkerOptions.
  headline: How to create worksheets smart markers with Aspose.Cells
  type: TechArticle
- description: Create worksheets smart markers in Java using Aspose.Cells and control
    detail sheet naming with SmartMarkerOptions.
  name: How to create worksheets smart markers with Aspose.Cells
  steps:
  - name: Set up the Maven project and add Aspose.Cells
    text: 'Create a new Maven module (or Gradle project) and add the Aspose.Cells
      dependency:'
  - name: Load the master workbook that contains smart markers
    text: '```java import com.aspose.cells.*;'
  - name: Configure SmartMarkerOptions for custom detail sheet names
    text: '```java // Define naming pattern for detail sheets. SmartMarkerOptions
      smartMarkerOptions = new SmartMarkerOptions(); // {0} is automatically replaced
      by the row index (starting at 1). smartMarkerOptions.setDetailSheetNewName("DetailSheet_{0}");
      ```'
  - name: Build a DataTable that matches the smart marker fields
    text: '```java // Build a simple DataTable with two columns. DataTable data =
      new DataTable(); data.getColumns().add("Id", DataType.INTEGER); data.getColumns().add("Value",
      DataType.STRING); // Add sample rows. data.getRows().add(new Object[] { 1, "A"
      }); data.getRows().add(new Object[] { 2, "B" }); ```'
  - name: Apply the data to the smart markers with the naming options
    text: '```java // Apply the data to the first worksheet (index 0). workbook.getWorksheets().get(0).getSmartMarkers().apply(data,
      smartMarkerOptions); ```'
  - name: Save the workbook and verify the result
    text: '```java // Save the expanded workbook. workbook.save("YOUR_DIRECTORY/MasterDetailDuplicatedNames.xlsx");
      } } ```'
  - name: Multiple master sheets
    text: 'If your template contains more than one master sheet, iterate over each
      sheet’s smart markers:'
  - name: Custom naming beyond the row index
    text: 'You can embed any data column into the sheet name by using placeholders
      like `{ColumnName}`:'
  - name: Preventing overly long sheet names
    text: 'Excel limits sheet names to 31 characters. If your naming pattern risks
      exceeding this limit, truncate or hash the value:'
  type: HowTo
tags:
- Java
- Aspose.Cells
- Smart Markers
- Excel Automation
title: Cách tạo smart markers cho worksheet bằng Aspose.Cells
url: /vi/java/templates-reporting/how-to-create-worksheets-smart-markers-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách tạo smart markers cho worksheets bằng Aspose.Cells

Nếu bạn cần **tạo smart markers cho worksheets** trong một workbook Java, hướng dẫn này sẽ chỉ cho bạn các bước chính xác để thực hiện với Aspose.Cells. Bạn sẽ thấy cách cấu hình `SmartMarkerOptions` để mỗi sheet chi tiết nhận được một tên duy nhất, có thể dự đoán được.

Việc tạo báo cáo Excel mở rộng một mẫu master‑detail là yêu cầu phổ biến trong các hệ thống tài chính, tồn kho và báo cáo. Sử dụng smart markers loại bỏ việc sao chép sheet thủ công và cho phép bạn tập trung vào dữ liệu thay vì các công việc nền tảng.

## Bạn sẽ học được gì

* Cách tải một workbook master chứa smart markers.  
* Cách thiết lập `SmartMarkerOptions` để điều khiển việc đặt tên cho các sheet chi tiết được tạo ra.  
* Cách cung cấp một `DataTable` với dữ liệu mẫu và áp dụng nó cho smart markers.  
* Cách lưu kết quả sao cho mỗi worksheet chi tiết có một tên riêng, tránh trùng lặp tên sheet.

**Yêu cầu trước**  
* Java 17 hoặc mới hơn (mã cũng biên dịch được với JDK 8+).  
* Aspose.Cells for Java 23.9 hoặc mới hơn – thư viện cung cấp các lớp `Workbook`, `SmartMarkerOptions`, và các lớp liên quan.  
* Một IDE như IntelliJ IDEA, Eclipse, hoặc VS Code.

Các khái niệm phụ bạn sẽ gặp bao gồm **Aspose.Cells Java**, **smart marker options**, và cách xử lý **duplicate sheet names** khi mẫu được mở rộng.

## Tạo smart markers cho worksheets – hướng dẫn từng bước

Các phần dưới đây chia quy trình thành các bước rời rạc, có thể tái sử dụng. Mỗi bước bao gồm một đoạn mã, giải thích lý do quan trọng và các mẹo thực tế để tránh những lỗi thường gặp.

### Bước 1: Thiết lập dự án Maven và thêm Aspose.Cells

Tạo một module Maven mới (hoặc dự án Gradle) và thêm phụ thuộc Aspose.Cells:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
</dependency>
```

**Tại sao bước này quan trọng** – Thư viện cung cấp lớp `Workbook` để đọc và ghi file Excel, cùng với engine smart‑marker tự động mở rộng mẫu của bạn. Nếu thiếu phụ thuộc đúng, trình biên dịch sẽ không thể giải quyết các lời gọi API được sử dụng sau này.

> **Pro tip:** Nếu bạn làm việc phía sau proxy công ty, hãy cấu hình `settings.xml` của Maven để kéo về repository Aspose một cách an toàn.

### Bước 2: Tải workbook master chứa smart markers

```java
import com.aspose.cells.*;

public class DuplicateDetailSheetNames {
    public static void main(String[] args) throws Exception {
        // Load the template that holds the smart marker tags.
        Workbook workbook = new Workbook("YOUR_DIRECTORY/MasterDetailTemplate.xlsx");
```

**Tại sao bước này quan trọng** – Workbook master định nghĩa bố cục, công thức và các thẻ placeholder (`«SmartMarker»`) mà engine sẽ thay thế. Việc tải file một lần giúp giảm tiêu thụ bộ nhớ và cho phép bạn tái sử dụng cùng một workbook cho nhiều bộ dữ liệu.

### Bước 3: Cấu hình SmartMarkerOptions để đặt tên sheet chi tiết tùy chỉnh

```java
        // Define naming pattern for detail sheets.
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions();
        // {0} is automatically replaced by the row index (starting at 1).
        smartMarkerOptions.setDetailSheetNewName("DetailSheet_{0}");
```

**Tại sao bước này quan trọng** – Mặc định Aspose.Cells tạo các sheet chi tiết với tên chung như “DetailSheet”. Khi mẫu mở rộng cho nhiều hàng, những tên này sẽ xung đột, gây **duplicate sheet names** và ném ra ngoại lệ thời chạy. Mẫu `"DetailSheet_{0}"` đảm bảo mỗi hàng có một tên duy nhất, giải quyết vấn đề trùng lặp.

### Bước 4: Xây dựng DataTable khớp với các trường smart marker

```java
        // Build a simple DataTable with two columns.
        DataTable data = new DataTable();
        data.getColumns().add("Id", DataType.INTEGER);
        data.getColumns().add("Value", DataType.STRING);
        // Add sample rows.
        data.getRows().add(new Object[] { 1, "A" });
        data.getRows().add(new Object[] { 2, "B" });
```

**Tại sao bước này quan trọng** – `DataTable` cung cấp các giá trị thực sẽ thay thế các placeholder smart marker. Tên cột phải khớp với tên marker trong mẫu; nếu không engine sẽ bỏ qua việc thay thế một cách im lặng.

> **Sai lầm phổ biến:** Sử dụng tên cột khác nhau về chữ hoa/thường (ví dụ, “id” so với “Id”) sẽ dẫn đến dữ liệu bị thiếu trong các sheet được tạo.

### Bước 5: Áp dụng dữ liệu cho smart markers với các tùy chọn đặt tên

```java
        // Apply the data to the first worksheet (index 0).
        workbook.getWorksheets().get(0).getSmartMarkers().apply(data, smartMarkerOptions);
```

**Tại sao bước này quan trọng** – Phương thức `apply` kích hoạt engine smart‑marker. Nó đọc từng hàng, tạo một sheet chi tiết mới dựa trên mẫu đặt tên từ `SmartMarkerOptions`, và điền dữ liệu của hàng vào sheet. Lệnh duy nhất này thay thế hàng chục dòng mã sao chép sheet và điền ô thủ công.

### Bước 6: Lưu workbook và kiểm tra kết quả

```java
        // Save the expanded workbook.
        workbook.save("YOUR_DIRECTORY/MasterDetailDuplicatedNames.xlsx");
    }
}
```

Sau khi thực thi, mở `MasterDetailDuplicatedNames.xlsx`. Bạn sẽ thấy:

* Sheet master gốc không thay đổi.  
* Hai worksheet mới có tên `DetailSheet_1` và `DetailSheet_2`.  
* Mỗi sheet chi tiết chứa các giá trị từ hàng tương ứng của `DataTable`.

**Tại sao bước này quan trọng** – Việc ghi workbook hoàn thiện quá trình mở rộng smart‑marker. File giờ có thể được gửi tới các hệ thống downstream, đính kèm email, hoặc mở trong Excel để phân tích thêm.

## Xử lý các trường hợp đặc biệt và biến thể

### Nhiều sheet master

Nếu mẫu của bạn có hơn một sheet master, hãy lặp qua các smart marker của mỗi sheet:

```java
for (int i = 0; i < workbook.getWorksheets().getCount(); i++) {
    workbook.getWorksheets().get(i).getSmartMarkers().apply(data, smartMarkerOptions);
}
```

### Đặt tên tùy chỉnh vượt qua chỉ số hàng

Bạn có thể nhúng bất kỳ cột dữ liệu nào vào tên sheet bằng cách sử dụng placeholder như `{ColumnName}`:

```java
smartMarkerOptions.setDetailSheetNewName("Order_{OrderId}");
```

Đảm bảo cột `OrderId` tồn tại trong `DataTable` đã cung cấp.

### Ngăn tên sheet quá dài

Excel giới hạn tên sheet tối đa 31 ký tự. Nếu mẫu đặt tên của bạn có khả năng vượt quá giới hạn này, hãy cắt ngắn hoặc băm giá trị:

```java
String pattern = "Detail_{0}_{1}";
smartMarkerOptions.setDetailSheetNewName(pattern);
```

Sau đó xử lý tên đã tạo bằng `StringUtils.abbreviate` trước khi truyền cho Aspose.

## Ví dụ đầy đủ có thể chạy được

Dưới đây là toàn bộ file nguồn bạn có thể sao chép, điều chỉnh đường dẫn file và chạy trực tiếp:

```java
import com.aspose.cells.*;

public class DuplicateDetailSheetNames {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the master workbook that contains smart markers
        Workbook workbook = new Workbook("YOUR_DIRECTORY/MasterDetailTemplate.xlsx");

        // 2️⃣ Define how detail sheets will be named when they are created
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions();
        // {0} is replaced by the row index (starting at 1)
        smartMarkerOptions.setDetailSheetNewName("DetailSheet_{0}");

        // 3️⃣ Prepare sample data to populate the smart markers
        DataTable data = new DataTable();
        data.getColumns().add("Id", DataType.INTEGER);
        data.getColumns().add("Value", DataType.STRING);
        data.getRows().add(new Object[] { 1, "A" });
        data.getRows().add(new Object[] { 2, "B" });

        // 4️⃣ Apply the data to the smart markers using the naming options
        workbook.getWorksheets().get(0).getSmartMarkers().apply(data, smartMarkerOptions);

        // 5️⃣ Save the workbook – each detail sheet now has a unique name
        workbook.save("YOUR_DIRECTORY/MasterDetailDuplicatedNames.xlsx");
    }
}
```

**Kết quả mong đợi**

* `MasterDetailDuplicatedNames.xlsx` chứa:

## Bạn nên học gì tiếp theo?

Các hướng dẫn sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh với giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Mastering Aspose.Cells Java: Utilize Smart Markers for Dynamic Data in Worksheets](/cells/english/java/worksheet-management/aspose-cells-java-smart-markers-worksheets/)
- [Create Dynamic Charts with Smart Markers in Aspose.Cells for Java | Step-by-Step Guide](/cells/english/java/charts-graphs/dynamic-charts-smart-markers-aspose-cells-java/)
- [Aspose Cells Java Smart Markers Worksheets](/cells/german/java/worksheet-management/aspose-cells-java-smart-markers-worksheets/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}