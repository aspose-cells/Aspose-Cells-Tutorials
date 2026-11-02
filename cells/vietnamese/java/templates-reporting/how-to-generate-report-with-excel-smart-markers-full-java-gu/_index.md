---
category: general
date: 2026-07-03
description: Cách tạo báo cáo bằng cách điền dữ liệu vào mẫu Excel sử dụng Smart Markers.
  Học cách tạo sheet chi tiết, sử dụng Smart Markers và tự động chèn dữ liệu.
draft: false
keywords:
- how to generate report
- populate excel template
- how to create detail
- create detail sheet
- use smart markers
language: vi
og_description: Cách tạo báo cáo bằng Smart Markers trong Java. Hướng dẫn này chỉ
  ra cách điền dữ liệu vào mẫu Excel, tạo sheet chi tiết và tự động hoá báo cáo master‑detail.
og_title: Cách tạo báo cáo với Excel Smart Markers – Hướng dẫn Java
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: How to generate report by populating an Excel template using Smart
    Markers. Learn to create detail sheet, use smart markers and automate data insertion.
  headline: How to Generate Report with Excel Smart Markers – Full Java Guide
  type: TechArticle
- description: How to generate report by populating an Excel template using Smart
    Markers. Learn to create detail sheet, use smart markers and automate data insertion.
  name: How to Generate Report with Excel Smart Markers – Full Java Guide
  steps:
  - name: What the code does, step by step
    text: '| Step | Explanation | |------|-------------| | **Load workbook** | Reads
      the template, preserving all formatting. | | **Insert marker** | Guarantees
      the placeholder exists even if you built the template programmatically. | |
      **Prepare data** | The `Map` key (`"Orders"`) must match the Smart Marker '
  - name: 5.1 Multiple Detail Datasets
    text: 'You can embed several Smart Markers in the same template, e.g., `{{Detail:Customers}}`
      and `{{Detail:Orders}}`. Just add corresponding entries to the `Map`:'
  - name: 5.2 Custom Sheet Names per Row
    text: 'If you need a unique sheet per order (instead of a single detail sheet),
      use the `DetailSheetNewName` pattern with placeholders:'
  - name: 5.3 Handling Large Datasets
    text: 'When dealing with thousands of rows, enable streaming to keep memory usage
      low:'
  - name: 5.4 Formatting Numbers and Dates
    text: Smart Markers respect the cell’s existing format. If column B in the template
      is formatted as **Currency**, the amounts will automatically display with the
      correct symbol. For custom date formats, just set the cell’s number format before
      processing.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel Automation
title: Cách tạo báo cáo với Excel Smart Markers – Hướng dẫn Java đầy đủ
url: /vi/java/templates-reporting/how-to-generate-report-with-excel-smart-markers-full-java-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách Tạo Báo Cáo với Excel Smart Markers – Hướng Dẫn Java Đầy Đủ

Bạn đã bao giờ tự hỏi **cách tạo báo cáo** từ một mẫu Excel mà không phải viết hàng triệu dòng code lặp lại không? Bạn không phải là người duy nhất. Nhiều nhà phát triển gặp khó khăn khi cần lấy dữ liệu từ cơ sở dữ liệu, đưa nó vào một workbook master‑detail, và vẫn giữ giao diện trông chuyên nghiệp.  

Tin tốt? Với Aspose.Cells **Smart Markers** bạn có thể **điền dữ liệu vào mẫu Excel** chỉ bằng một lời gọi duy nhất, dễ đọc—không cần các thao tác phức tạp từng ô một. Trong hướng dẫn này, chúng tôi sẽ đi qua toàn bộ quy trình, từ việc chuẩn bị mẫu đến lưu file cuối cùng, và cũng sẽ chỉ cho bạn **cách tạo sheet chi tiết** một cách nhanh chóng.

Khi hoàn thành hướng dẫn này, bạn sẽ có thể:

* Tải một workbook đã được thiết kế trước, đóng vai trò là sheet master của bạn.  
* Chèn một placeholder Smart Marker mà Aspose sẽ thay thế bằng dữ liệu đơn hàng thực tế.  
* Cung cấp một `Map` Java làm nguồn dữ liệu và cấu hình các tùy chọn **create detail sheet**.  
* Chạy bộ xử lý và có được một báo cáo master‑detail hoàn thiện, sẵn sàng chia sẻ.

> **Mẹo chuyên nghiệp:** Nếu bạn đã có một mẫu mà đội ngũ kinh doanh của bạn yêu thích, bạn không cần chỉnh sửa giao diện—chỉ cần đặt các thẻ Smart Marker vào các ô phù hợp.

---

## Yêu Cầu Trước

Trước khi chúng ta bắt đầu với mã, hãy chắc chắn rằng bạn có những thứ sau:

| Yêu cầu | Lý do quan trọng |
|-------------|----------------|
| **Aspose.Cells for Java** (phiên bản mới nhất) | Cung cấp `SmartMarkerProcessor`, `Workbook`, và các API liên quan. |
| **Java 8+** | Ví dụ sử dụng streams và phương thức factory `Map.of` được giới thiệu trong Java 9; điều chỉnh nếu bạn đang dùng Java 8. |
| **Mẫu Excel** (`template.xlsx`) có một ô placeholder cho Smart Marker | Đây là file bạn sẽ tải và sau đó lưu thành `masterDetail.xlsx`. |
| **Mô hình dữ liệu đơn giản** (ví dụ, lớp `Order`) | Cung cấp cho bộ xử lý một đối tượng cụ thể để thay thế các marker. |

Nếu bạn chưa có Aspose.Cells, hãy tải bản dùng thử miễn phí từ trang chính thức và thêm JAR vào classpath của dự án.

## Bước 1: Thiết Lập Mẫu Excel (populate excel template)

Mở Excel và tạo một workbook có tên `template.xlsx`. Trong ô **A1** của sheet đầu tiên, nhập thẻ Smart Marker:

```
{{Detail:Orders}}
```

Thẻ đó cho Aspose biết rằng tập hợp `Orders` là một dataset **detail** và sẽ tạo các hàng cho mỗi mục. Lưu file vào một thư mục bạn sẽ tham chiếu sau, ví dụ `C:/Reports/`.

> **Tại sao điều này quan trọng:** Bằng cách nhúng marker trực tiếp vào mẫu, bạn giữ thiết kế trực quan tách biệt khỏi mã. Các nhà thiết kế có thể điều chỉnh phông chữ, màu sắc và công thức mà không cần chạm vào Java.

## Bước 2: Tạo Cấu Trúc Dự Án Java

Dưới đây là một đoạn `pom.xml` Maven tối thiểu để kéo Aspose.Cells:

```xml
<dependencies>
    <dependency>
        <groupId>com.aspose</groupId>
        <artifactId>aspose-cells</artifactId>
        <version>24.9</version> <!-- Use the latest version -->
    </dependency>
</dependencies>
```

Tạo một package `com.example.report` và thêm hai lớp: `ReportGenerator` (trình điều khiển chính) và `Order` (mô hình dữ liệu của chúng ta).

```java
package com.example.report;

public class Order {
    public String orderId;
    public String customer;
    public double amount;

    public Order(String orderId, String customer, double amount) {
        this.orderId = orderId;
        this.customer = customer;
        this.amount = amount;
    }

    // Getters are optional for Smart Marker; public fields work fine.
}
```

## Bước 3: Tải Workbook và Chèn Smart Marker (use smart markers)

Bây giờ chúng ta sẽ viết logic cốt lõi. Lưu ý cách mã phản chiếu đoạn mã gốc nhưng thêm các import, xử lý lỗi và chú thích để rõ ràng.

```java
package com.example.report;

import com.aspose.cells.*;
import java.util.*;

public class ReportGenerator {

    public static void main(String[] args) {
        try {
            // 1️⃣ Load the workbook that contains the master sheet
            Workbook wb = new Workbook("C:/Reports/template.xlsx");

            // 2️⃣ Grab the first worksheet (the master)
            Worksheet master = wb.getWorksheets().get(0);

            // 3️⃣ Insert a Smart Marker placeholder if you prefer to do it programmatically.
            //    This is optional because we already placed {{Detail:Orders}} in A1.
            master.getCells().putValue("A1", "{{Detail:Orders}}");

            // 4️⃣ Prepare the data source for the Smart Marker
            Map<String, Object> data = new HashMap<>();
            data.put("Orders", getOrders()); // getOrders() returns List<Order>

            // 5️⃣ Configure Smart Marker options – this is where we **create detail sheet**
            SmartMarkerOptions smOpt = new SmartMarkerOptions();
            smOpt.setDetailSheetNewName("OrderDetail"); // New sheet will be named "OrderDetail"

            // 6️⃣ Process the Smart Marker to generate the master‑detail report
            SmartMarkerProcessor processor = new SmartMarkerProcessor();
            processor.process(master, data, smOpt);

            // 7️⃣ Save the resulting workbook
            wb.save("C:/Reports/masterDetail.xlsx");

            System.out.println("Report generated successfully!");
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    /**
     * Simulates fetching order data from a database or service.
     * In a real‑world scenario replace this with JDBC/ORM calls.
     */
    private static List<Order> getOrders() {
        return Arrays.asList(
            new Order("ORD001", "Acme Corp", 1250.75),
            new Order("ORD002", "Beta Ltd.", 980.00),
            new Order("ORD003", "Gamma Inc.", 432.50)
        );
    }
}
```

### Những gì mã thực hiện, từng bước một

| Bước | Giải thích |
|------|-------------|
| **Load workbook** | Đọc mẫu, giữ nguyên mọi định dạng. |
| **Insert marker** | Đảm bảo placeholder tồn tại ngay cả khi bạn tạo mẫu bằng mã. |
| **Prepare data** | Khóa `Map` (`"Orders"`) phải khớp với thẻ Smart Marker (`{{Detail:Orders}}`). |
| **Configure options** | `setDetailSheetNewName` cho Aspose tạo một **create detail sheet** có tên *OrderDetail*. |
| **Process** | `SmartMarkerProcessor` duyệt workbook, thay thế thẻ và tạo các hàng trên sheet mới. |
| **Save** | Ghi `masterDetail.xlsx` cuối cùng ra đĩa. |

> **Tại sao nên dùng Smart Markers?** Chúng cho phép bạn mô tả *cái gì* bạn muốn (bảng đơn hàng) thay vì *cách* lặp qua các hàng và cột. Thư viện tự động xử lý phân trang, sao chép kiểu, và thậm chí tính lại công thức.

## Bước 4: Xác Minh Kết Quả (how to generate report – verification)

Chạy lớp `ReportGenerator`. Sau khi thực thi bạn sẽ thấy hai worksheet:

1. **Sheet1** – sheet master gốc (vẫn chứa `{{Detail:Orders}}` nhưng bộ xử lý sẽ ẩn nó).  
2. **OrderDetail** – một sheet mới hoàn toàn với một hàng cho mỗi đối tượng `Order`:

| Mã Đơn | Khách hàng | Số tiền |
|----------|------------|--------|
| ORD001   | Acme Corp  | 1250.75|
| ORD002   | Beta Ltd.  | 980.00 |
| ORD003   | Gamma Inc. | 432.50 |

Nếu bạn mở file trong Excel, bạn sẽ thấy độ rộng cột, phông chữ và bất kỳ kiểu đã áp dụng trước đó từ mẫu vẫn được giữ nguyên. Đó là ưu điểm của **use smart markers**: chúng bảo tồn giao diện trong khi chèn dữ liệu.

## Bước 5: Các Biến Thể Thông Thường & Trường Hợp Cạnh (populate excel template, how to create detail)

### 5.1 Nhiều Dataset Detail

Bạn có thể nhúng nhiều Smart Markers trong cùng một mẫu, ví dụ `{{Detail:Customers}}` và `{{Detail:Orders}}`. Chỉ cần thêm các mục tương ứng vào `Map`:

```java
data.put("Customers", getCustomers());
data.put("Orders", getOrders());
```

Mỗi marker sẽ tạo một sheet riêng nếu bạn đặt `DetailSheetNewName` một cách phù hợp.

### 5.2 Tên Sheet Tùy Chỉnh cho Mỗi Hàng

Nếu bạn cần một sheet duy nhất cho mỗi đơn hàng (thay vì một sheet detail duy nhất), hãy sử dụng mẫu `DetailSheetNewName` có placeholder:

```java
smOpt.setDetailSheetNewName("Order_{OrderId}");
```

Aspose sẽ thay thế `{OrderId}` bằng giá trị thực tế từ mỗi hàng.

### 5.3 Xử Lý Datasets Lớn

Khi làm việc với hàng nghìn dòng, bật streaming để giảm mức sử dụng bộ nhớ:

```java
WorkbookSettings ws = wb.getSettings();
ws.setMemorySetting(MemorySetting.MEMORY_PREFERENCE);
```

### 5.4 Định Dạng Số và Ngày

Smart Markers tuân theo định dạng hiện có của ô. Nếu cột B trong mẫu được định dạng là **Currency**, các số tiền sẽ tự động hiển thị với ký hiệu đúng. Đối với định dạng ngày tùy chỉnh, chỉ cần đặt định dạng số của ô trước khi xử lý.

## Bước 6: Mẹo & Lưu Ý (how to create detail, use smart markers)

* **Không bao giờ hard‑code đường dẫn file** trong môi trường production. Sử dụng file cấu hình hoặc biến môi trường.  
* **Luôn đóng các tài nguyên** nếu bạn mở stream thủ công; lớp `Workbook` triển khai `AutoCloseable` trong các phiên bản mới.  
* **Cẩn thận với xung đột tên**—nếu đã tồn tại sheet cùng tên, Aspose sẽ thêm hậu tố số. Để đảm bảo duy nhất, hãy đặt tiền tố thời gian.  
* **Kiểm tra với collection rỗng**. Nếu `Orders` rỗng, bộ xử lý vẫn tạo sheet nhưng để trống—xử lý ở downstream nếu bạn không muốn các tab thừa.  
* **Debug Smart Markers**: đặt `smOpt.setThrowExceptionOnMissingData(true)` để nhận ngoại lệ rõ ràng khi một marker không khớp với bất kỳ trường dữ liệu nào.  

![How to generate report using Smart Markers in Java](/images/how-to-generate-report-smart-markers.png "how to generate report")

*Chú thích hình ảnh: File `masterDetail.xlsx` cuối cùng hiển thị sheet master và sheet **OrderDetail** đã được tạo.*

## Kết Luận

Chúng tôi vừa trình diễn **cách tạo báo cáo** bằng cách **điền dữ liệu vào mẫu Excel** với Aspose.Cells Smart Markers, và đã bao phủ mọi thứ bạn cần để **tự động tạo sheet detail**. Cách tiếp cận này giữ

## Bạn Nên Học Gì Tiếp Theo?

Các hướng dẫn sau đây bao gồm các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật đã trình bày trong hướng dẫn này. Mỗi tài nguyên đều có ví dụ mã đầy đủ, kèm giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [How to Automate Excel Smart Markers with Aspose.Cells for Java](/cells/english/java/automation-batch-processing/aspose-cells-java-smart-markers-excel/)
- [Populate Excel with Data Using Aspose.Cells and Smart Markers](/cells/english/java/cell-operations/populate-excel-aspose-cells-smart-markers/)
- [How to Create Pivot Tables in Excel Using Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}