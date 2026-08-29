---
category: general
date: 2026-08-20
description: Tạo workbook Excel trong Java bằng Aspose.Cells, thiết lập định dạng
  tiền tệ, thêm phông chữ in đậm và nhập mảng kiểu cho các ô đã định dạng.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- set currency format
- format cells currency
- how to import style
- add bold font
language: vi
lastmod: 2026-08-20
og_description: Tạo workbook Excel trong Java, đặt định dạng tiền tệ, thêm phông chữ
  đậm và học cách nhập kiểu dáng bằng Aspose.Cells.
og_image_alt: Screenshot of an excel workbook created with currency format and bold
  font using Aspose.Cells
og_title: Tạo workbook Excel với các ô tiền tệ được định dạng trong Java
schemas:
- author: Aspose
  dateModified: '2026-08-20'
  description: Create excel workbook in Java using Aspose.Cells, set currency format,
    add bold font, and import style array for styled cells.
  headline: How to create excel workbook with currency format and bold font in Java
  type: TechArticle
- description: Create excel workbook in Java using Aspose.Cells, set currency format,
    add bold font, and import style array for styled cells.
  name: How to create excel workbook with currency format and bold font in Java
  steps:
  - name: Initialise the workbook and worksheet
    text: Creating a fresh workbook gives you a clean container for all subsequent
      formatting.
  - name: Build a DataTable with numeric data
    text: A `DataTable` mimics a database table, making it easy to import rows in
      bulk.
  - name: Define a style – currency format and bold font
    text: Here we **set currency format** and **add bold font** to a `Style` object.
  - name: Configure import options to use the style array
    text: Aspose.Cells lets you pass a `Style[]` via `ImportTableOptions`. This is
      the official **how to import style** method.
  - name: Import the DataTable into the worksheet
    text: Now we bring the data into the sheet at cell `A1`, applying the style array
      automatically.
  - name: Save the workbook to disk
    text: Finally, write the in‑memory workbook to a physical file.
  - name: Expected output
    text: 'When you open `DataTableWithStyleArray.xlsx` in Microsoft Excel, you should
      see:'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel
- Formatting
title: Cách tạo workbook Excel với định dạng tiền tệ và phông chữ in đậm trong Java
url: /vi/java/formatting/how-to-create-excel-workbook-with-currency-format-and-bold-f/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách tạo workbook Excel với định dạng tiền tệ và phông chữ đậm trong Java

Nếu bạn cần **tạo workbook Excel** một cách lập trình, hướng dẫn này sẽ chỉ cho bạn cách thực hiện. Chúng ta sẽ đi qua việc xây dựng một workbook, áp dụng định dạng tiền tệ, thêm phông chữ đậm, và sử dụng tính năng **how to import style** của Aspose.Cells để mọi ô được nhập vào đều có cùng kiểu.

Bạn sẽ hoàn thành với một tệp `DataTableWithStyleArray.xlsx` sẵn sàng sử dụng, hiển thị các số dưới dạng đô la và làm nổi bật chúng bằng chữ đậm. Không cần định dạng thủ công trong Excel.

## Các yêu cầu trước

Trước khi bắt đầu, hãy chắc chắn rằng bạn có:

- Java 17 hoặc phiên bản mới hơn đã được cài đặt.
- Giấy phép Aspose.Cells for Java (hoặc khóa dùng thử miễn phí).
- Maven hoặc Gradle để quản lý phụ thuộc `aspose-cells`.
- Kiến thức cơ bản về các collection trong Java và `DataTable`.

```xml
<!-- Maven dependency -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version>
</dependency>
```

> **Mẹo chuyên nghiệp:** Nếu gặp lỗi `LicenseException`, đặt tệp giấy phép của bạn vào classpath và gọi `License license = new License(); license.setLicense("Aspose.Total.Java.lic");` trước khi tạo workbook.

## Cách tạo excel workbook với các ô tiền tệ có kiểu dáng

Phần này chứa các bước cốt lõi. Mỗi bước giải thích **tại sao** nó quan trọng, không chỉ **phải** gõ gì.

### Bước 1: Khởi tạo workbook và worksheet

Tạo một workbook mới giúp bạn có một container sạch cho mọi định dạng tiếp theo.

```java
// Step 1: Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();                     // creates an empty .xlsx file in memory
Worksheet worksheet = workbook.getWorksheets().get(0); // first sheet is index 0
Cells cells = worksheet.getCells();                     // shortcut to work with cells
```

> **Tại sao:** Đối tượng `Workbook` đại diện cho toàn bộ tệp Excel. Truy cập `Worksheet` đầu tiên cho phép bạn bắt đầu điền dữ liệu ngay lập tức.

### Bước 2: Xây dựng DataTable với dữ liệu số

`DataTable` mô phỏng một bảng cơ sở dữ liệu, giúp nhập nhiều hàng cùng lúc một cách dễ dàng.

```java
// Step 2: Build a DataTable with sample numeric data
DataTable dataTable = new DataTable();
dataTable.getColumns().add("Amount", DataType.DOUBLE); // column type DOUBLE ensures numeric handling
dataTable.getRows().add(new Object[]{1234.56});
dataTable.getRows().add(new Object[]{7890.12});
```

> **Tại sao:** Sử dụng `DOUBLE` đảm bảo các giá trị giữ được độ chính xác thập phân, điều này rất quan trọng khi bạn sau này **format cells currency**.

### Bước 3: Định nghĩa style – định dạng tiền tệ và phông chữ đậm

Ở đây chúng ta **đặt định dạng tiền tệ** và **thêm phông chữ đậm** vào một đối tượng `Style`.

```java
// Step 3: Define a style (currency format and bold font) for the imported cells
Style currencyStyle = workbook.createStyle();                // create a reusable style instance
currencyStyle.getNumber().setFormat("$#,##0.00");            // set currency format (e.g., $1,234.56)
currencyStyle.getFont().setBold(true);                      // make the font bold
Style[] styleArray = new Style[] { currencyStyle };          // style array required by ImportTableOptions
```

> **Tại sao:** Chuỗi định dạng `Number` `$#,##0.00` báo cho Excel biết ô này là giá trị tiền tệ, trong khi `setBold(true)` làm cho số nổi bật hơn. Đặt style vào mảng chuẩn bị cho bước **how to import style**.

### Bước 4: Cấu hình tùy chọn nhập để sử dụng mảng style

Aspose.Cells cho phép bạn truyền một `Style[]` qua `ImportTableOptions`. Đây là phương pháp **how to import style** chính thức.

```java
// Step 4: Set up import options to use the style array
ImportTableOptions importOptions = new ImportTableOptions();
importOptions.setStyleArray(styleArray); // tells the importer to apply our currencyStyle to every column
```

> **Tại sao:** Nếu không có `ImportTableOptions`, các ô được nhập sẽ kế thừa style mặc định, mất đi định dạng tiền tệ và chữ đậm mà chúng ta đã định nghĩa.

### Bước 5: Nhập DataTable vào worksheet

Bây giờ chúng ta đưa dữ liệu vào sheet tại ô `A1`, tự động áp dụng mảng style.

```java
// Step 5: Import the DataTable into the worksheet at A1, applying the style
cells.importDataTable(dataTable, true, "A1", importOptions);
```

- `true` chỉ ra rằng hàng đầu tiên của `DataTable` chứa tiêu đề cột.
- `"A1"` là góc trên‑trái nơi quá trình nhập bắt đầu.

> **Tại sao:** Nhập dữ liệu kèm mảng style đảm bảo mỗi ô được nhập nhận được style **format cells currency** mà chúng ta đã chuẩn bị trước.

### Bước 6: Lưu workbook ra đĩa

Cuối cùng, ghi workbook đang ở bộ nhớ vào một tệp thực tế.

```java
// Step 6: Save the workbook to a file
String outputPath = "YOUR_DIRECTORY/DataTableWithStyleArray.xlsx";
workbook.save(outputPath);
System.out.println("Workbook saved to: " + outputPath);
```

> **Tại sao:** Việc lưu giúp giữ lại các định dạng, cho phép bạn hoặc các quy trình tiếp theo mở tệp trong Excel với giao diện mong muốn.

## Toàn bộ mã nguồn

Dưới đây là lớp Java hoàn chỉnh, sẵn sàng chạy. Sao chép vào IDE, thay `YOUR_DIRECTORY` bằng thư mục tồn tại, và thực thi.

```java
import com.aspose.cells.*;

public class StyleArrayImportTutorial {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);
        Cells cells = worksheet.getCells();

        // Step 2: Build a DataTable with sample numeric data
        DataTable dataTable = new DataTable();
        dataTable.getColumns().add("Amount", DataType.DOUBLE);
        dataTable.getRows().add(new Object[]{1234.56});
        dataTable.getRows().add(new Object[]{7890.12});

        // Step 3: Define a style (currency format and bold font) for the imported cells
        Style currencyStyle = workbook.createStyle();
        currencyStyle.getNumber().setFormat("$#,##0.00");   // set currency format
        currencyStyle.getFont().setBold(true);             // add bold font
        Style[] styleArray = new Style[] { currencyStyle };

        // Step 4: Set up import options to use the style array
        ImportTableOptions importOptions = new ImportTableOptions();
        importOptions.setStyleArray(styleArray);           // how to import style

        // Step 5: Import the DataTable into the worksheet at A1, applying the style
        cells.importDataTable(dataTable, true, "A1", importOptions);

        // Step 6: Save the workbook to a file
        workbook.save("YOUR_DIRECTORY/DataTableWithStyleArray.xlsx");
        System.out.println("Workbook created successfully.");
    }
}
```

### Kết quả mong đợi

Khi mở `DataTableWithStyleArray.xlsx` trong Microsoft Excel, bạn sẽ thấy:

| Số tiền |
|--------|
| **$1,234.56** |
| **$7,890.12** |

- Các số được hiển thị với **định dạng tiền tệ** (`$` và hai chữ số thập phân).
- Phông chữ của cả hai ô là **đậm**, làm chúng nổi bật.

## Các biến thể phổ biến và trường hợp đặc biệt

| Kịch bản | Cần thay đổi | Lý do |
|----------|--------------|-------|
| **Tiền tệ khác** | `currencyStyle.getNumber().setFormat("€#,##0.00");` | Sử dụng ký hiệu Euro hoặc bất kỳ định dạng theo địa phương nào. |
| **Nhiều cột với các style khác nhau** | Tạo nhiều đối tượng `Style`, điền `styleArray` theo cùng thứ tự với các cột. | Mỗi cột có thể có định dạng số, phông chữ, nền, v.v. riêng. |
| **Bộ dữ liệu lớn** | Dùng `cells.importDataTable(dataTable, false, "A1", importOptions);` và đặt `importOptions.setImportDataOptions(ImportDataOptions.DATA_ONLY);` | Cải thiện hiệu năng bằng cách bỏ qua hàng tiêu đề hoặc siêu dữ liệu không cần thiết. |
| **Áp dụng style sau khi nhập** | Gọi `cells.get("A2").setStyle(currencyStyle);` cho các ô riêng lẻ. | Hữu ích khi chỉ một phần các hàng cần định dạng đặc biệt. |

## Mẹo cho môi trường sản xuất

- **Cấp giấy phép sớm**: Đăng ký giấy phép Aspose.Cells trước khi tạo workbook để tránh dấu watermark đánh giá.
- **An toàn đa luồng**: Các thể hiện `Workbook` **không** an toàn với đa luồng. Tạo một thể hiện riêng cho mỗi luồng nếu bạn tạo nhiều tệp đồng thời.
- **Quản lý bộ nhớ**: Đối với các sheet rất lớn, cân nhắc sử dụng API streaming của `Workbook` (`Workbook` → `WorkbookDesigner`) để giảm tiêu thụ bộ nhớ.
- **Kiểm thử**: Bao gồm một unit test mở tệp đã lưu bằng Apache POI và xác nhận rằng định dạng số của ô khớp với `"$#,##0.00"`.

## Kết luận

Bây giờ bạn đã biết cách **tạo workbook Excel** trong Java, **đặt định dạng tiền tệ**, **thêm phông chữ đậm**, và đúng cách **how to import style** bằng `ImportTableOptions` của Aspose.Cells. Giải pháp đầu‑cuối này loại bỏ các bước thủ công trong Excel và đảm bảo mọi ô được nhập đều tuân theo cùng một style **format cells currency**.

Sẵn sàng cho thử thách tiếp theo? Hãy thử thêm định dạng có điều kiện, nhúng biểu đồ, hoặc xuất workbook ra PDF — tất cả đều sử dụng kỹ thuật mảng style đã học. Chúc bạn lập trình vui vẻ!

## Bạn nên học gì tiếp theo?

Các hướng dẫn sau đây bao gồm các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên đều có mã mẫu đầy đủ và giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Create an Excel Workbook using Aspose.Cells in Java: A Step-by-Step Guide](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)
- [How to Create & Format Excel Cells Using Aspose.Cells for Java: A Step-by-Step Guide](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)
- [How to Style Excel Cells and Add Hyperlinks Using Aspose.Cells for Java](/cells/english/java/formatting/style-excel-cells-hyperlinks-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}