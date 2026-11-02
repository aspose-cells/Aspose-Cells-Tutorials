---
category: general
date: 2026-09-27
description: Tạo workbook Excel bằng Java, nhập dữ liệu SQL, đặt định dạng số cho
  cột và lưu workbook dưới dạng XLSX bằng Aspose.Cells trong Java.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook java
- save workbook as xlsx
- import sql data excel
- add number format excel
- set number format column
language: vi
lastmod: 2026-09-27
og_description: Tạo workbook Excel bằng Java, nhập dữ liệu SQL, đặt định dạng số cho
  cột và lưu workbook dưới dạng XLSX với ví dụ Java hoạt động đầy đủ.
og_image_alt: Screenshot of a Java program creating an Excel workbook with styled
  numeric columns
og_title: Tạo workbook Excel bằng Java – nhập dữ liệu SQL và đặt định dạng số cho
  cột
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Create Excel workbook java, import SQL data, set number format column,
    and save workbook as XLSX using Aspose.Cells in Java.
  headline: Create Excel workbook java and apply column number formats
  type: TechArticle
tags:
- Java
- Aspose.Cells
- Excel automation
- Data import
title: Tạo workbook Excel bằng Java và áp dụng định dạng số cho cột
url: /vi/java/formatting/create-excel-workbook-java-and-apply-column-number-formats/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo workbook Excel bằng Java và áp dụng định dạng số cho cột

Nếu bạn cần **create Excel workbook java** và định dạng các cột số, hướng dẫn này sẽ chỉ cho bạn cách thực hiện. Bạn sẽ học cách nhập dữ liệu SQL vào Excel, đặt định dạng số cho mỗi cột, và **save workbook as XLSX** bằng thư viện Aspose.Cells.

Làm việc với bảng tính từ Java thường cảm thấy rời rạc—các nhà phát triển sao chép‑dán các đoạn mã, quên định dạng số, hoặc kết thúc với các tệp CSV thay vì các tệp Excel thực sự. Bài hướng dẫn này loại bỏ sự khó khăn đó bằng cách cung cấp một giải pháp duy nhất, từ đầu đến cuối mà bạn có thể đưa vào bất kỳ dự án Java nào.

Bằng cách đọc hết bài viết, bạn sẽ có thể:

* Kết nối tới cơ sở dữ liệu và lấy một `DataTable` (hoặc `ResultSet`)  
* Tạo một workbook mới với Aspose.Cells  
* Áp dụng một kiểu **add number format excel** nhất quán cho mọi cột  
* **Save workbook as XLSX** tới một vị trí bạn chọn  

Yêu cầu duy nhất là môi trường phát triển Java (khuyến nghị JDK 8+) và JAR Aspose.Cells cho Java trong classpath của bạn.

---

## Yêu cầu trước

| Yêu cầu | Lý do quan trọng |
|-------------|----------------|
| JDK 8 hoặc mới hơn | Cung cấp các tính năng ngôn ngữ được sử dụng trong ví dụ. |
| Aspose.Cells cho Java (phiên bản mới nhất) | Xử lý việc tạo, định dạng và lưu Excel mà không cần cài Office. |
| Cơ sở dữ liệu tương thích JDBC (ví dụ: MySQL, PostgreSQL) | Cung cấp dữ liệu SQL mà chúng ta sẽ nhập. |
| Maven hoặc Gradle (tùy chọn) | Đơn giản hoá việc quản lý phụ thuộc. |

Thêm Aspose.Cells vào file `pom.xml` của Maven:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- use the latest stable version -->
</dependency>
```

Hoặc tải JAR trực tiếp từ trang web Aspose và thêm nó vào classpath của dự án.

## Bước 1: Tạo workbook Excel bằng Java

Khối logic đầu tiên là khởi tạo một `Workbook` mới. Đối tượng này đại diện cho toàn bộ tệp Excel trong bộ nhớ và cung cấp cho bạn quyền truy cập vào các worksheet, ô và kiểu.

```java
// Step 1: Create a new workbook instance
Workbook workbook = new Workbook();
```

Việc tạo workbook ngay từ đầu cũng cung cấp cho chúng ta một nhà máy `Style` mà chúng ta sẽ cần sau này khi **set number format column**.

## Bước 2: Lấy dữ liệu từ SQL (import sql data excel)

Dưới đây chúng ta mở một kết nối JDBC, thực thi một câu lệnh `SELECT` đơn giản, và tải result set vào một `DataTable` của Aspose. Lớp `DataTable` mô phỏng .NET `DataTable` và hoạt động liền mạch với phương thức `importDataTable`.

```java
// Step 2: Pull data from a database and fill a DataTable
private static DataTable getDataTableFromDb() throws SQLException {
    // Replace with your actual connection string, user, and password
    String url = "jdbc:mysql://localhost:3306/yourdb";
    String user = "your_user";
    String password = "your_password";

    try (Connection conn = DriverManager.getConnection(url, user, password);
         Statement stmt = conn.createStatement();
         ResultSet rs = stmt.executeQuery("SELECT Id, Amount, CreatedDate FROM Payments")) {

        // Aspose.Cells provides a utility to convert ResultSet → DataTable
        return CellsHelper.getDataTableFromResultSet(rs);
    }
}
```

> **Mẹo:** Nếu bạn đã có một `DataTable` từ nguồn khác (ví dụ: phân tích CSV), bạn có thể bỏ qua mã JDBC và trả về bảng đó trực tiếp.

## Bước 3: Chuẩn bị kiểu có thể tái sử dụng (add number format excel)

Chúng ta muốn mọi cột số hiển thị số với hai chữ số thập phân và dấu phân cách hàng nghìn. Thay vì định dạng từng ô riêng lẻ, chúng ta tạo một đối tượng `Style` một lần cho mỗi cột và tái sử dụng nó trong quá trình nhập. Đây là cách hiệu quả nhất để **add number format excel**.

```java
// Step 3: Build a style array – one style per column
private static Style[] buildColumnStyles(Workbook workbook, int columnCount) {
    Style[] styles = new Style[columnCount];
    for (int i = 0; i < columnCount; i++) {
        styles[i] = workbook.createStyle();
        // "0.00" = two decimal places; "#,##0.00" adds thousands separator
        styles[i].setNumber("#,##0.00");
    }
    return styles;
}
```

Bạn có thể điều chỉnh chuỗi định dạng (`"#,##0.00"`) cho bất kỳ định dạng số Excel nào bạn cần. Đối với ngày, sử dụng `styles[i].setCustom("mm-dd-yyyy")`, v.v.

## Bước 4: Nhập DataTable và áp dụng kiểu cho cột

Bây giờ chúng ta kết hợp mọi thứ lại. Phương thức overload `importDataTable` cho phép chúng ta truyền `DataTable`, chỉ định liệu hàng đầu tiên có được coi là tiêu đề cột hay không, và cung cấp mảng kiểu. Điều này tự động **set number format column** cho mỗi ô trong cột tương ứng.

```java
// Step 4: Import data with styles into the first worksheet
private static void importDataWithStyles(Workbook workbook, DataTable dataTable) {
    // Build a style for each column based on the number of columns in the DataTable
    Style[] columnStyles = buildColumnStyles(workbook, dataTable.getColumns().size());

    // Import the DataTable starting at cell A1 (row 0, column 0)
    workbook.getWorksheets().get(0).getCells()
            .importDataTable(dataTable, true, 0, 0, columnStyles);
}
```

Vì chúng ta đã truyền `true` cho cờ `importColumnNames`, hàng đầu tiên của worksheet chứa tên cột từ `DataTable`. Mỗi hàng tiếp theo nhận dữ liệu, đã được định dạng theo kiểu chúng ta đã định nghĩa.

## Bước 5: Lưu workbook dưới dạng xlsx

Bước cuối cùng là lưu workbook đang ở trong bộ nhớ ra một tệp vật lý. Aspose.Cells hỗ trợ nhiều định dạng; chúng ta sẽ sử dụng định dạng XLSX hiện đại, là định dạng mà hầu hết các ứng dụng ngày nay mong đợi.

```java
// Step 5: Save the workbook to an .xlsx file
private static void saveWorkbook(Workbook workbook, String filePath) throws IOException {
    workbook.save(filePath, com.aspose.cells.SaveFormat.XLSX);
}
```

Bạn có thể thay đổi `filePath` thành bất kỳ vị trí hợp lệ nào trên hệ thống của mình. Phương thức sẽ ném `IOException` nếu thư mục không tồn tại hoặc bạn không có quyền ghi.

## Ví dụ đầy đủ, có thể chạy được

Kết hợp tất cả các phần lại với nhau tạo ra một chương trình tự chứa mà bạn có thể biên dịch và chạy ngay lập tức.

```java
import com.aspose.cells.*;
import java.sql.*;

public class CreateExcelWorkbookJava {
    public static void main(String[] args) {
        try {
            // 1️⃣ Obtain data from the database
            DataTable dataTable = getDataTableFromDb();

            // 2️⃣ Create a new workbook that will hold the imported data
            Workbook workbook = new Workbook();

            // 3️⃣ Import the DataTable with a numeric style per column
            importDataWithStyles(workbook, dataTable);

            // 4️⃣ Save the workbook as XLSX
            String outputPath = "DataTableWithNumberFormat.xlsx";
            saveWorkbook(workbook, outputPath);

            System.out.println("Workbook created successfully at: " + outputPath);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    // ---- Helper methods (see earlier sections) ----
    private static DataTable getDataTableFromDb() throws SQLException {
        String url = "jdbc:mysql://localhost:3306/yourdb";
        String user = "your_user";
        String password = "your_password";

        try (Connection conn = DriverManager.getConnection(url, user, password);
             Statement stmt = conn.createStatement();
             ResultSet rs = stmt.executeQuery("SELECT Id, Amount, CreatedDate FROM Payments")) {

            return CellsHelper.getDataTableFromResultSet(rs);
        }
    }

    private static Style[] buildColumnStyles(Workbook workbook, int columnCount) {
        Style[] styles = new Style[columnCount];
        for (int i = 0; i < columnCount; i++) {
            styles[i] = workbook.createStyle();
            styles[i].setNumber("#,##0.00"); // two decimals with thousands separator
        }
        return styles;
    }

    private static void importDataWithStyles(Workbook workbook, DataTable dataTable) {
        Style[] columnStyles = buildColumnStyles(workbook, dataTable.getColumns().size());
        workbook.getWorksheets().get(0).getCells()
                .importDataTable(dataTable, true, 0, 0, columnStyles);
    }

    private static void saveWorkbook(Workbook workbook, String filePath) throws IOException {
        workbook.save(filePath, SaveFormat.XLSX);
    }
}
```

### Kết quả mong đợi

Chạy chương trình sẽ tạo một tệp có tên **DataTableWithNumberFormat.xlsx** trong thư mục làm việc. Mở nó bằng Microsoft Excel, LibreOffice Calc, hoặc bất kỳ trình xem XLSX nào và bạn sẽ thấy:

| Id | Amount | CreatedDate |
|----|--------|-------------|
| 1  | 1,234.56 | 2023‑01‑15 |
| 2  | 78,900.00 | 2023‑02‑20 |
| …  | … | … |

*​Cột **Amount** hiển thị số với hai chữ số thập phân và dấu phân cách hàng nghìn, nhờ vào kiểu **add number format excel** mà chúng ta đã áp dụng.*

## Câu hỏi thường gặp và xử lý các trường hợp đặc biệt

| Câu hỏi | Trả lời |
|----------|--------|
| **Nếu truy vấn của tôi không trả về dòng nào?** | `DataTable` sẽ rỗng nhưng vẫn chứa định nghĩa các cột. Workbook sẽ chỉ có hàng tiêu đề, điều này thường đủ cho các quy trình downstream. |
| **Làm thế nào để áp dụng các định dạng khác nhau cho mỗi cột?** | Sửa đổi `buildColumnStyles` để kiểm tra tên cột hoặc kiểu dữ liệu và gán một định dạng tùy chỉnh (ví dụ: ngày, phần trăm). |
| **Tôi có thể ghi trực tiếp vào `ByteArrayOutputStream` không?** | Có. Thay thế `workbook.save(filePath, SaveFormat.XLSX);` bằng

## Bạn nên học gì tiếp theo?

Các hướng dẫn sau đây bao gồm các chủ đề liên quan chặt chẽ, xây dựng dựa trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh với giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [How to Create and Save an Excel Workbook as SVG using Aspose.Cells for Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)
- [Create Save Excel Workbook Aspose Cells Java](/cells/hindi/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)
- [Create Save Excel Workbook Aspose Cells Java](/cells/german/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}