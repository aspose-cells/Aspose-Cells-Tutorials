---
category: general
date: 2026-08-20
description: Học cách viết JSON sang Excel và điền dữ liệu vào workbook Excel từ JSON
  bằng cách sử dụng Aspose Smart Markers và Java – hướng dẫn từng bước.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- aspose smart markers
- convert json to excel
- write json to excel
- populate excel from json
- create excel workbook java
language: vi
lastmod: 2026-08-20
og_description: aspose smart markers cho phép bạn ghi JSON vào Excel và tạo ví dụ
  mã Java cho workbook Excel. Hãy làm theo hướng dẫn này để nhanh chóng điền dữ liệu
  từ JSON vào Excel.
og_image_alt: Screenshot of an Excel file generated from a JSON array using Aspose.Cells
og_title: 'aspose smart markers: chuyển đổi JSON sang Excel trong Java – hướng dẫn
  đầy đủ'
schemas:
- author: Aspose
  dateModified: '2026-08-20'
  description: Learn to write JSON to Excel and populate an Excel workbook from JSON
    using aspose smart markers and Java – step‑by‑step guide.
  headline: How to use aspose smart markers to convert JSON to Excel in Java
  type: TechArticle
- description: Learn to write JSON to Excel and populate an Excel workbook from JSON
    using aspose smart markers and Java – step‑by‑step guide.
  name: How to use aspose smart markers to convert JSON to Excel in Java
  steps:
  - name: Expected output
    text: 'When you open `JsonArraySingleCell.xlsx`, cell **A1** contains:'
  - name: 1. Populating multiple cells with different JSON objects
    text: 'If you need to fill a table rather than a single cell, omit `ArrayAsSingle`
      and use the default array handling:'
  - name: 2. Using a JSON file instead of a hard‑coded string
    text: '```java String jsonPath = "data/people.json"; String jsonArray = new String(Files.readAllBytes(Paths.get(jsonPath)),
      StandardCharsets.UTF_8); ```'
  - name: 3. Handling nested JSON structures
    text: 'For nested objects, reference sub‑properties in the smart marker:'
  - name: 4. License activation
    text: 'To avoid the evaluation watermark, activate your license before creating
      the workbook:'
  type: HowTo
tags:
- Aspose
- Java
- Excel
- JSON
title: Cách sử dụng Aspose Smart Markers để chuyển đổi JSON sang Excel trong Java
url: /vi/java/excel-import-export/how-to-use-aspose-smart-markers-to-convert-json-to-excel-in/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách sử dụng aspose smart markers để chuyển đổi JSON sang Excel trong Java

Nếu bạn cần **aspose smart markers** để chuyển đổi JSON sang Excel, hướng dẫn này cung cấp một giải pháp sẵn sàng chạy. Bạn sẽ thấy cách ghi JSON vào Excel, điền một workbook Excel từ JSON, và tạo tệp chỉ với một dòng lệnh.

Ví dụ sử dụng Aspose.Cells for Java, một thư viện loại bỏ nhu cầu cài đặt Microsoft Office trên máy chủ. Khi kết thúc hướng dẫn, bạn sẽ có một chương trình Java hoàn chỉnh tạo một workbook Excel, chèn một mảng JSON vào một ô duy nhất, và lưu kết quả dưới tên `JsonArraySingleCell.xlsx`.

## Các yêu cầu trước

Trước khi bắt đầu, hãy chắc chắn rằng bạn đã có:

* Java Development Kit 17 hoặc mới hơn được cài đặt.
* Maven hoặc Gradle để quản lý phụ thuộc (ví dụ sử dụng Maven).
* Giấy phép Aspose.Cells for Java (phiên bản dùng thử miễn phí đủ cho việc thử nghiệm).
* Kiến thức cơ bản về cú pháp Java và định dạng JSON.

> **Mẹo chuyên nghiệp:** Nếu chạy mã mà không có giấy phép, workbook được tạo sẽ có một watermark đánh dấu dùng thử nhỏ trên sheet đầu tiên.

## Thêm Aspose.Cells vào dự án của bạn

Thêm phụ thuộc sau vào file `pom.xml` (Maven) hoặc tương đương trong Gradle:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest stable version -->
</dependency>
```

Thư viện cung cấp các lớp `Workbook`, `Worksheet`, `JsonDataSource`, và `SmartMarker` được sử dụng xuyên suốt trong hướng dẫn này.

## Bước 1: Tạo một workbook Excel trong Java

Đầu tiên, khởi tạo một đối tượng `Workbook` mới. Đối tượng này đại diện cho một tệp Excel trống trong bộ nhớ.

```java
// Step 1: Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();               // Creates a blank .xlsx file
Worksheet worksheet = workbook.getWorksheets().get(0);
Cells cells = worksheet.getCells();
```

`Workbook` là điểm vào cho mọi thao tác Excel. Mặc định nó chứa một worksheet, chúng ta sẽ lấy worksheet này để thực hiện các thao tác tiếp theo.

## Bước 2: Chuẩn bị mảng JSON bạn muốn ghi vào Excel

Chuỗi JSON có thể đến từ file, dịch vụ web, hoặc được tạo lập bằng mã. Trong hướng dẫn này, chúng ta sử dụng một mảng nội tuyến đơn giản:

```java
// Step 2: Define the JSON array that will be used as the data source
String jsonArray = "[{\"Name\":\"John\"},{\"Name\":\"Jane\"}]";
```

Cấu trúc JSON phù hợp với định dạng mà Aspose.Cells smart markers mong đợi: một mảng các đối tượng, mỗi đối tượng chứa thuộc tính `Name`.

## Bước 3: Chèn một smart marker để xử lý mảng như một ô duy nhất

Aspose smart markers cho phép bạn nhúng các placeholder trực tiếp vào ô. Tùy chọn `ArrayAsSingle` chỉ định cho engine đặt toàn bộ mảng JSON vào một ô thay vì mở rộng thành bảng.

```java
// Step 3: Insert a smart marker that tells Aspose.Cells to treat the array as a single cell
cells.putValue("A1", "${jsonArray,ArrayAsSingle}");
```

Khi workbook được xử lý, `${jsonArray,ArrayAsSingle}` sẽ được thay thế bằng văn bản JSON thô.

## Bước 4: Đăng ký nguồn dữ liệu JSON với tên smart marker

Liên kết tên placeholder (`jsonArray`) với một thể hiện `JsonDataSource`. Bước này sẽ ràng buộc chuỗi JSON với marker.

```java
// Step 4: Register the JSON data source with the smart marker name
JsonDataSource dataSource = new JsonDataSource(jsonArray);
worksheet.getSmartMarkers().setDataSource("jsonArray", dataSource);
```

`JsonDataSource` phân tích JSON và cung cấp nó cho engine smart marker. Lệnh `setDataSource` đăng ký nguồn dữ liệu dưới tên được sử dụng trong ô (`jsonArray`).

## Bước 5: Lưu workbook ra đĩa

Cuối cùng, ghi workbook vào một tệp vật lý. Bạn có thể chọn bất kỳ thư mục nào bạn muốn.

```java
// Step 5: Save the workbook to a file
String outputPath = "YOUR_DIRECTORY/JsonArraySingleCell.xlsx";
workbook.save(outputPath);
System.out.println("Workbook saved to " + outputPath);
```

Chạy chương trình sẽ tạo ra một tệp Excel chứa mảng JSON trong ô **A1**. Mở tệp bằng Excel, LibreOffice, hoặc bất kỳ trình xem nào hỗ trợ `.xlsx` để kiểm tra kết quả.

![Workbook Excel được tạo bằng Aspose.Cells hiển thị dữ liệu JSON](/images/json-to-excel.png)

*Văn bản thay thế ảnh: Ảnh chụp màn hình của một tệp Excel được tạo từ một mảng JSON bằng Aspose.Cells.*

## Mã nguồn đầy đủ

Kết hợp tất cả các phần lại, đây là lớp Java hoàn chỉnh, có thể chạy được:

```java
import com.aspose.cells.*;

public class JsonArraySmartMarker {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook and access the first worksheet
        Workbook workbook = new Workbook();                       // Empty workbook
        Worksheet worksheet = workbook.getWorksheets().get(0);
        Cells cells = worksheet.getCells();

        // Step 2: Define the JSON array that will be used as the data source
        String jsonArray = "[{\"Name\":\"John\"},{\"Name\":\"Jane\"}]";

        // Step 3: Insert a smart marker that tells Aspose.Cells to treat the array as a single cell
        cells.putValue("A1", "${jsonArray,ArrayAsSingle}");

        // Step 4: Register the JSON data source with the smart marker name
        JsonDataSource dataSource = new JsonDataSource(jsonArray);
        worksheet.getSmartMarkers().setDataSource("jsonArray", dataSource);

        // Step 5: Save the workbook to a file
        String outputPath = "YOUR_DIRECTORY/JsonArraySingleCell.xlsx";
        workbook.save(outputPath);
        System.out.println("Workbook saved to " + outputPath);
    }
}
```

### Kết quả mong đợi

Khi mở `JsonArraySingleCell.xlsx`, ô **A1** sẽ chứa:

```
[{"Name":"John"},{"Name":"Jane"}]
```

Không có hàng hay cột bổ sung nào được thêm — điều này chứng minh **aspose smart markers** cho phép **ghi JSON vào Excel** trong khi giữ nguyên payload JSON.

## Các biến thể phổ biến và trường hợp đặc biệt

### 1. Điền nhiều ô với các đối tượng JSON khác nhau

Nếu bạn muốn điền một bảng thay vì một ô duy nhất, bỏ `ArrayAsSingle` và sử dụng xử lý mảng mặc định:

```java
cells.putValue("A1", "${jsonArray}");
```

Aspose.Cells sẽ mở rộng mảng thành các hàng, tạo một cột cho mỗi thuộc tính (`Name` trong trường hợp này). Điều này hữu ích khi bạn muốn một giao diện bảng truyền thống.

### 2. Sử dụng file JSON thay vì chuỗi cứng

```java
String jsonPath = "data/people.json";
String jsonArray = new String(Files.readAllBytes(Paths.get(jsonPath)), StandardCharsets.UTF_8);
```

Đọc nội dung file vào một chuỗi, sau đó thực hiện các Bước 3‑5 mà không thay đổi. Cách này phù hợp cho payload lớn hoặc dữ liệu nhận từ API bên ngoài.

### 3. Xử lý cấu trúc JSON lồng nhau

Đối với các đối tượng lồng nhau, tham chiếu các thuộc tính con trong smart marker:

```java
cells.putValue("B2", "${jsonArray.Address.City}");
```

Aspose.Cells sẽ tự động duyệt qua cấu trúc phân cấp, cho phép bạn điền các báo cáo phức tạp mà không cần phân tích thủ công.

### 4. Kích hoạt giấy phép

Để loại bỏ watermark dùng thử, kích hoạt giấy phép trước khi tạo workbook:

```java
License license = new License();
license.setLicense("Aspose.Total.Java.lic");
```

Đặt đoạn mã này ngay đầu hàm `main`. File giấy phép có thể được nhúng dưới dạng tài nguyên hoặc tải từ vị trí an toàn.

## Mẹo cho môi trường production

* **Tái sử dụng đối tượng workbook** – Nếu bạn tạo nhiều báo cáo trong một lần chạy, hãy tạo một `Workbook` duy nhất và sao chép các worksheet thay vì khởi tạo workbook mới mỗi lần.
* **Stream đầu ra** – Đối với tệp lớn, sử dụng `workbook.save(OutputStream, SaveFormat.XLSX)` để ghi trực tiếp vào luồng phản hồi trong các ứng dụng web.
* **Xác thực JSON** – Trước khi truyền dữ liệu cho `JsonDataSource`, hãy xác thực định dạng JSON để tránh lỗi thời gian chạy.
* **Hiệu năng** – Smart markers được tối ưu cho các thao tác bulk; tránh trộn lẫn ghi từng ô với xử lý smart marker trong cùng một sheet.

## Kết luận

Bây giờ bạn đã biết cách sử dụng **aspose smart markers** để **chuyển đổi JSON sang Excel**, **ghi JSON vào Excel**, và **điền Excel từ JSON** bằng Java. Ví dụ đầy đủ tạo một workbook Excel, chèn một mảng JSON vào một ô duy nhất, và lưu tệp — tất cả chỉ với năm bước ngắn gọn.

Tiếp theo, bạn có thể khám phá:

* Tạo báo cáo đa sheet từ các cấu trúc JSON phức tạp.
* Kết hợp smart markers với công thức Excel để thực hiện các phép tính động.
* Sử dụng `JsonDataSource` cùng với `DataTable` để xuất CSV.

Hãy tự do thử nghiệm với các payload JSON khác nhau, phạm vi ô, và các tùy chọn định dạng. Với Aspose.Cells, việc biến dữ liệu JSON thành các workbook Excel chuyên nghiệp trở nên đơn giản, tập trung vào code. Chúc bạn lập trình vui!

## Bạn nên học gì tiếp theo?

Các hướng dẫn sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật đã trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh với giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Tạo một Excel Workbook bằng Aspose.Cells trong Java&#58; Hướng dẫn chi tiết](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)
- [Tạo báo cáo Excel động bằng Aspose.Cells Java và Smart Markers](/cells/english/java/templates-reporting/dynamic-excel-reports-aspose-cells-java-smart-markers/)
- [Thành thạo Aspose.Cells Java&#58; Triển khai Smart Markers & Formulas cho tự động hóa Excel](/cells/english/java/formulas-functions/aspose-cells-java-smart-markers-formulas/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}