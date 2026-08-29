---
category: general
date: 2026-07-03
description: Cách định dạng tệp Excel bằng Java. Học cách định dạng cột ngày trong
  Excel, áp dụng định dạng số trong Excel, xuất DataTable sang XLSX và nhập DataTable
  vào Excel bằng Aspose Cells.
draft: false
keywords:
- how to style excel
- format column date excel
- apply number format excel
- export datatable to xlsx
- import datatable into excel
language: vi
og_description: Cách định dạng tệp Excel trong Java. Hướng dẫn này cho thấy cách định
  dạng ngày cho cột trong Excel, áp dụng định dạng số trong Excel, xuất DataTable
  sang XLSX và nhập DataTable vào Excel.
og_title: Cách Định Dạng Excel – Hướng Dẫn Java cho Định Dạng Cột Tùy Chỉnh
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: How to style Excel files using Java. Learn to format column date Excel,
    apply number format Excel, export DataTable to XLSX and import DataTable into
    Excel with Aspose Cells.
  headline: How to Style Excel – Import DataTable with Custom Formatting in Java
  type: TechArticle
tags:
- Java
- Excel
- Aspose.Cells
title: Cách Định Dạng Excel – Nhập DataTable với Định Dạng Tùy Chỉnh trong Java
url: /vi/java/excel-import-export/how-to-style-excel-import-datatable-with-custom-formatting-i/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách Định Dạng Excel – Nhập DataTable với Định Dạng Tùy Chỉnh trong Java

Bạn đã bao giờ tự hỏi **cách định dạng Excel** một cách lập trình mà không cần mở file thủ công chưa? Bạn không phải là người duy nhất. Nhiều nhà phát triển cần tạo báo cáo trong đó cột đầu tiên in đậm, cột thứ hai hiển thị ngày tháng, và phần còn lại có bố cục gọn gàng. Trong hướng dẫn này, chúng ta sẽ đi qua một ví dụ hoàn chỉnh, có thể chạy được, **nhập một DataTable vào Excel**, áp dụng tiêu đề in đậm, định dạng cột ngày, và cuối cùng **xuất DataTable ra XLSX**.

Chúng ta sẽ sử dụng Aspose.Cells for Java, nhưng các khái niệm này cũng áp dụng cho bất kỳ thư viện nào cho phép bạn làm việc với kiểu dáng. Khi kết thúc, bạn sẽ có một mẫu có thể tái sử dụng để **apply number format Excel** cho các ô, **format column date Excel**, và cung cấp một workbook được tinh chỉnh cho người dùng của mình.

## Yêu cầu trước

- Java 17 (hoặc bất kỳ JDK hiện đại nào)  
- Aspose.Cells for Java 23.9 trở lên (bản dùng thử miễn phí hoạt động tốt)  
- Cấu trúc kiểu `DataTable` (ví dụ này sử dụng một mock đơn giản)  
- IDE yêu thích của bạn (IntelliJ IDEA, Eclipse, VS Code…)

Không cần plugin Maven bổ sung; chỉ cần thêm JAR Aspose.Cells vào classpath của bạn.

---

## Bước 1: Lấy DataTable Nguồn – Chuẩn Bị “Export DataTable to XLSX”

Trước khi chúng ta có thể **import datatable into excel**, chúng ta cần một đối tượng `DataTable` đại diện cho dữ liệu bạn muốn xuất. Trong các dự án thực tế, bạn có thể lấy dữ liệu này từ cơ sở dữ liệu, file CSV, hoặc một API. Đối với tutorial này, chúng ta sẽ mô phỏng một bảng nhỏ:

```java
import java.util.*;
import com.aspose.cells.*;

public class DemoData {
    public static DataTable getDataTable() {
        // Create a simple table with three columns: ID, Date, Amount
        DataTable dt = new DataTable();
        dt.getColumns().add("ID", DataType.INTEGER);
        dt.getColumns().add("OrderDate", DataType.DATE_TIME);
        dt.getColumns().add("Total", DataType.DOUBLE);

        // Add a few rows
        dt.getRows().add(new Object[]{1, new Date(), 125.50});
        dt.getRows().add(new Object[]{2, new Date(System.currentTimeMillis() - 86400000L), 99.99});
        dt.getRows().add(new Object[]{3, new Date(System.currentTimeMillis() - 2*86400000L), 250.00});
        return dt;
    }
}
```

> **Why this matters:** Việc có dữ liệu đúng ngay từ đầu có nghĩa là phần còn lại của logic định dạng có thể tập trung hoàn toàn vào việc trình bày, không phải xử lý dữ liệu.

---

## Bước 2: Tạo Mảng Để Giữ Định Nghĩa Kiểu Dáng Cho Mỗi Cột

Aspose.Cells cho phép bạn truyền một mảng **Style[]** khi nhập một `DataTable`. Mỗi phần tử tương ứng với một cột và quyết định cách cột đó sẽ hiển thị sau khi nhập. Hãy cấp phát mảng dựa trên số lượng cột:

```java
DataTable dataTable = DemoData.getDataTable();
Style[] columnStyles = new Style[dataTable.getColumns().size()];
```

> **Tip:** Nếu bạn có nhiều cột, hãy cân nhắc xây dựng mảng trong một vòng lặp và tái sử dụng một đối tượng `Style` duy nhất cho những cột có cùng định dạng. Điều này giảm tải bộ nhớ.

---

## Bước 3: Định Nghĩa Các Kiểu Dáng – Tiêu Đề In Đậm & Định Dạng Ngày

Bây giờ chúng ta trả lời câu hỏi cổ điển **format column date excel** và đồng thời minh họa **apply number format excel** cho các cột khác.

```java
// --- Style for the first column (header bold) ---
columnStyles[0] = new Style();
columnStyles[0].getFont().setBold(true);          // Makes header text bold

// --- Style for the second column (date formatting) ---
columnStyles[1] = new Style();
columnStyles[1].setNumber(StyleNumberFormat.DATE); // Uses the built‑in DATE format

// --- Optional: Style for the third column (currency) ---
columnStyles[2] = new Style();
columnStyles[2].setNumber(StyleNumberFormat.CURRENCY_USD);
```

**What’s happening here?**  
- `StyleNumberFormat.DATE` thông báo cho Excel rằng giá trị ô là ngày ngắn (ví dụ, *01/31/2024*).  
- `StyleNumberFormat.CURRENCY_USD` tự động thêm ký hiệu `$` và hai chữ số thập phân.  
- Đặt phông chữ in đậm cho cột đầu tiên làm cho tiêu đề nổi bật, đây là yêu cầu thường gặp khi bạn **how to style excel** bảng tính để dễ đọc.

> **Edge case:** Nếu dữ liệu nguồn của bạn đã chứa các chuỗi đã định dạng, bạn có thể cần chuyển chúng thành đối tượng `java.util.Date` trước khi nhập; nếu không Excel sẽ coi chúng là văn bản thuần.

---

## Bước 4: Tạo Workbook Mới và Truy Cập Worksheet Đầu Tiên

Một workbook mới cung cấp một canvas sạch sẽ. Chúng ta sẽ lấy worksheet đầu tiên, nơi dữ liệu sẽ được nhập.

```java
Workbook workbook = new Workbook();               // New empty workbook
Worksheet worksheet = workbook.getWorksheets().get(0); // First sheet (index 0)
```

> **Why a new workbook?** Bắt đầu từ đầu đảm bảo không có kiểu dáng thừa hoặc hàng ẩn can thiệp vào kết quả cuối cùng—điều quan trọng khi bạn **how to style excel** các file một cách nhất quán qua nhiều lần chạy.

---

## Bước 5: Nhập DataTable Với Các Kiểu Dáng Cột

Đây là phần cốt lõi của hoạt động: đưa `DataTable` vào sheet đồng thời áp dụng mảng kiểu dáng mà chúng ta đã xây dựng.

```java
// The third argument (true) tells Aspose.Cells to include column headers.
worksheet.getCells().importDataTable(dataTable, true, columnStyles);
```

**Explanation:**  
- `importDataTable` sao chép cả hàng tiêu đề và các hàng dữ liệu.  
- Mảng `columnStyles` khớp với từng cột, vì vậy tiêu đề của cột đầu tiên sẽ in đậm, cột thứ hai hiển thị ngày, và cột thứ ba hiển thị dưới dạng tiền tệ.  
- Dòng lệnh duy nhất này thay thế hàng chục bước định dạng ô thủ công, minh họa cách **apply number format excel** một cách sạch sẽ bằng lập trình.

---

## Bước 6: Lưu Workbook Đã Định Dạng – Hoàn Thành “Export DataTable to XLSX”

Cuối cùng chúng ta ghi workbook ra đĩa. Điều chỉnh đường dẫn tới một thư mục có quyền ghi trên máy của bạn.

```java
String outputPath = "C:/temp/styledImport.xlsx";
workbook.save(outputPath);
System.out.println("Workbook saved to " + outputPath);
```

Mở file trong Excel và bạn sẽ thấy:

- Tiêu đề cột **ID** in đậm.  
- Cột **OrderDate** được định dạng dưới dạng ngày (ví dụ, *04/27/2024*).  
- Cột **Total** hiển thị với ký hiệu đô la và hai chữ số thập phân.

> **Pro tip:** Nếu bạn cần hỗ trợ các phiên bản Excel cũ hơn, hãy gọi `workbook.save(outputPath, SaveFormat.XLS)` thay vì định dạng mặc định XLSX.

---

## Bước 7: Xác Minh Kết Quả & Các Điều Chỉnh Tùy Chọn

Thực hành tốt là kiểm tra lại file đã tạo, đặc biệt khi tự động hoá báo cáo cho các bên liên quan.

```java
// Quick verification: read the first cell's style
Cell firstHeader = worksheet.getCells().get(0, 0);
boolean isBold = firstHeader.getStyle().getFont().isBold();
System.out.println("Header bold? " + isBold);
```

Nếu `isBold` in ra `true`, quy trình **how to style excel** của bạn đã hoạt động như mong đợi. Từ đây bạn có thể:

- Thêm định dạng có điều kiện (ví dụ, làm nổi bật tổng > $200).  
- Đóng băng hàng trên cùng để cuộn dễ dàng hơn.  
- Chèn biểu đồ tham chiếu dữ liệu đã nhập.

Tất cả các mở rộng này tuân theo cùng một mẫu: định nghĩa một `Style`, áp dụng nó, và lưu lại.

---

## Các Câu Hỏi Thường Gặp & Trường Hợp Cạnh

| Question | Answer |
|----------|--------|
| **Can I style more than one column the same way?** | Yes—reuse a single `Style` instance for all columns that share formatting. |
| **What if my DataTable has more columns than styles?** | Any column without a corresponding entry in `columnStyles` will use the default style. |
| **How do I change the date format to “dd‑MMM‑yyyy”?** | Use `columnStyles[1].setCustom("#dd-MMM-yyyy#");` instead of the built‑in `DATE`. |
| **Is there a way to auto‑size columns after import?** | Call `worksheet.autoFitColumns();` after `importDataTable`. |
| **Will this work on Linux/macOS?** | Absolutely—Aspose.Cells is platform‑agnostic as long as you have a compatible JDK. |

---

## Kết Luận

Bạn giờ đã có một ví dụ toàn diện, đầu‑tới‑cuối về **how to style Excel** workbook bằng cách **importing datatable into excel**, **format column date excel**, và **apply number format excel** sử dụng Java. Đoạn mã hiển thị toàn bộ quy trình từ **export datatable to xlsx** đến việc mở file trong Excel, bao gồm cả *what* và *why* của mỗi bước.

Hãy thử nghiệm: điều chỉnh mảng kiểu dáng, thêm nhiều cột hơn, hoặc kết nối với truy vấn cơ sở dữ liệu thực. Mẫu tương tự sẽ cho phép bạn tạo các báo cáo chuyên nghiệp chỉ với một cú nhấp chuột, không cần định dạng thủ công.

![Styled Excel worksheet generated by the tutorial code](https://example.com/images/styled-worksheet.png "Screenshot of styled Excel worksheet created using Java and Aspose.Cells")

*Image alt text: “Bảng tính Excel đã định dạng được tạo bằng Java và Aspose.Cells, hiển thị tiêu đề in đậm và cột ngày đã định dạng.”*

## Bạn Nên Học Gì Tiếp Theo?

Các tutorial sau đây liên quan chặt chẽ và mở rộng các kỹ thuật đã trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm mã nguồn hoàn chỉnh cùng các giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Cách Tạo & Định Dạng Ô Excel Sử Dụng Aspose.Cells cho Java: Hướng Dẫn Chi Tiết](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)
- [Cách Định Dạng Ô Excel và Thêm Liên Kết Siêu Văn Bản Sử Dụng Aspose.Cells cho Java](/cells/english/java/formatting/style-excel-cells-hyperlinks-aspose-cells-java/)
- [Aspose.Cells cho Java: Cách Tạo và Định Dạng Workbook Excel Một Cách Hiệu Quả](/cells/english/java/getting-started/aspose-cells-java-workbook-creation-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}